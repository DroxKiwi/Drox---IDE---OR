# Drox IDE — releases officielles

## But du projet — souveraineté

Drox vise la **souveraineté numérique** : IDE et moteur agent en local, LLM via **Ollama** (ou API que tu configures), données de session dans **`.drox/`** sur ton disque — pas de compte cloud KDDS obligatoire, pas de télémétrie Microsoft dans l’installeur.

**Seule exception réseau** : la **vérification de version** (lecture de `stable/latest.json` sur ce dépôt) pour proposer une MAJ si une release plus récente existe. Rien d’autre n’est requis pour coder avec l’agent.

---

## ⚠️ STATUT — version 1.5.0 (juin 2026)

> **Drox 1.5.0 remplace entièrement le moteur 1.4.x** (rail observateur, `role_split`, orchestration IDE — tout ça est **mort**).  
> Toujours **expérimental** — pas un IDE agent de prod — mais **nettement plus stable** qu’en 1.4.2 : mono-boucle TUI éprouvée, shim RPC, dogfood validé.

| | |
|---|---|
| **Version** | [**1.5.0**](https://github.com/DroxKiwi/Drox---IDE---OR/releases/latest) (juin 2026) · socle VS Code **1.126.0** |
| **Utilisable au quotidien ?** | **Non** — early adopters / dogfood / curieux qui acceptent bugs et changements sans préavis. |
| **Pourquoi essayer quand même ?** | Stack moteur **refondue** (plus de rail 1.4 bricolé) ; installeur Windows, Ollama local, mutations fichier validées en dogfood. |
| **1.4.x** | **Obsolète** — dernière livraison 1.4.2 ; ne plus documenter ni bâtir dessus. |

**En bref** : *expérimental oui, laboratoire cassant non — c’est la première release de la nouvelle base moteur.*

---

**Ce dépôt** : binaires Windows, manifestes MAJ (`stable/latest.json`), notes de version.  
**Pas les sources** — moteur & branding propriétaires [KDDS](https://github.com/DroxKiwi). Socle IDE : Code OSS (MIT) — [NOTICE.md](NOTICE.md).

**Dernière version** : [1.5.0](https://github.com/DroxKiwi/Drox---IDE---OR/releases/latest) · notes [RELEASE_NOTES](stable/1.5.0/RELEASE_NOTES.md)

| | |
|---|---|
| Installer | [Télécharger](https://github.com/DroxKiwi/Drox---IDE---OR/releases/latest) |
| MAJ auto | `stable/latest.json` |
| Ollama (recommandé) | [ollama.com](https://ollama.com/) |
| SmartScreen | Installeur **non signé** — « Éditeur inconnu » au premier lancement (normal) |

---

## FR — Vue globale

Tu installes **Drox IDE**, tu fais tourner **Ollama** avec un modèle (Qwen, Gemma, etc.), tu ouvres ton projet. Quand tu écris dans **Drox Chat**, l’IDE parle au moteur **`drox.exe`** en local ; le moteur appelle ton modèle et te redemande l’IDE pour ce qu’il ne peut pas faire seul (LSP, diff, écriture fichier côté workspace, questions bloquantes).

**La pile**

```mermaid
flowchart LR
  DEV(["Toi + ton repo"])
  IDE(["Drox IDE"])
  MOT(["drox.exe"])
  OLL(["Ollama"])
  MDL(["Ton modele"])

  DEV <-->|fichiers terminal| IDE
  IDE <-->|stdio NDJSON| MOT
  MOT <-->|HTTP localhost| OLL
  OLL --- MDL
```

**Un message dans le chat**

```mermaid
flowchart TB
  U(["Tu envoies un message"])
  I(["Drox IDE"])
  S(["Shim RPC drox-cli"])
  M(["Boucle agent TUI"])
  L(["LLM via Ollama"])
  O(["Outils locaux + tool/exec client"])

  U --> I
  I -->|agent.run| S
  S --> M
  M -->|prompt + historique| L
  L -->|texte + tool_calls| M
  M --> O
  O -->|LSP diff file_write| I
  I -->|resultats| S
  S -->|agent/event| I
  I --> U
```

| Brique | Rôle |
|--------|------|
| **Ollama** | Inférence locale — le modèle que **tu** choisis |
| **drox.exe** | Mono-boucle agent TUI + shim JSON-RPC vers l’IDE |
| **Drox IDE** | Éditeur + chat + exécution outils « client » dans le workspace |
| **Toi** | Repo, modèle, vignettes Config / Architecte, mode permission |

Pas de compte cloud KDDS obligatoire. Données session dans **`.drox/`** sur ton disque.

---

## FR — Architecture 1.5.0 : trois couches

Le produit = **IDE Electron** + **moteur Rust** séparés. Le moteur 1.5 n’est **plus** le conducteur rail 1.4 : c’est la boucle TUI d’origine, avec un **adaptateur** pour parler au chat existant.

```mermaid
flowchart TB
  subgraph IDE["Drox IDE — webview composer"]
    CFG["Vignette Configuration"]
    ARC["Vignette Architecte"]
    PERM["Modes permission"]
    UI["Stream chat + timeline rail"]
  end

  subgraph SHIM["Adaptateur drox-cli/jsonrpc"]
    RPC["agent.run · tool/exec · user/ask"]
    EVT["ide_event_shim — phases + rail synthetique"]
  end

  subgraph CORE["Coeur TUI — agent.rs"]
    LOOP["Boucle LLM + outils + permissions"]
    PH["Phases phase: …"]
  end

  subgraph EXT["Externe"]
    OLL["Ollama / API compatible"]
    FS["Workspace + .drox/"]
  end

  CFG --> RPC
  ARC --> RPC
  PERM --> RPC
  RPC --> LOOP
  LOOP --> PH
  LOOP <-->|stream| OLL
  LOOP --> FS
  LOOP -->|tool/exec| IDE
  EVT --> UI
  LOOP --> EVT
```

| Couche | Responsabilité |
|--------|----------------|
| **IDE** | UI chat, lance `drox --serve`, exécute LSP/diff/`file_write` client, affiche le stream. **Ne pilote pas** la logique agent. |
| **Shim RPC** | Traduit `AgentRunParams` (vignettes) → `LlmConfig` + `PermissionMode` ; relaie les events TUI ; synthétise `rail_station_*` pour la timeline. |
| **Cœur TUI** | Tours LLM, protocole `[phase: …]`, outils, permissions, session, compaction. Pipeline `tui_mono` — **pas** de `role_split`. |
| **Ollama** | Inférence. Le moteur envoie prompts + schémas outils ; reçoit tokens + `tool_calls`. |

Connexion IDE ↔ moteur : **pipe stdio**, messages **NDJSON** (JSON-RPC + events `agent/event`).

---

## FR — Un message → un run (`tui_mono`)

Chaque envoi déclenche **`agent.run`**. Le moteur exécute **une seule boucle** — plus de routage discuss/edit 1.4, plus d’intent probe, plus d’orchestration multi-rôles.

```mermaid
flowchart TD
  MSG["Message utilisateur"] --> RUN["agent.run"]
  RUN --> CFG["LlmConfig depuis vignettes + mode permission"]
  CFG --> LOOP["Boucle agent TUI"]
  LOOP --> PH{"Marqueur phase: …"}
  PH -->|done| END["Fin run — agent/done"]
  PH -->|autre| LOOP
```

**Modes permission** (vignettes chat) — mappés côté moteur :

| Vignette IDE | `PermissionMode` moteur |
|--------------|-------------------------|
| Analyze | `plan` (lecture / conseil, écritures bloquées) |
| Trust edit | `acceptEdits` (mutations auto-autorisées) |
| I'm not crazy | `default` (allow / ask / deny) |

Les champs RPC hérités 1.4 (`orchestrationMode`, `architectInteractionMode`) sont **ignorés** par le moteur 1.5.

---

## FR — Phases agent (moteur réel)

Le modèle structure son travail avec des lignes **`[phase: nom]`**. Seul **`[phase: done]`** clôt le run. Le texte sous **`[phase: answering]`** est la réponse visible ; le reste alimente **Thinking** / blocs repliés.

```mermaid
flowchart LR
  A[analyzing] --> R[reading]
  R --> C[clarifying]
  C --> P[planning]
  P --> X[acting]
  R --> X
  X --> T[testing]
  T --> V[verifying]
  X --> V
  V --> AN[answering]
  AN --> D[done]
```

Les phases intermédiaires sont **optionnelles** ; le chemin dépend de la tâche. Boucles `(acting → verifying)+` possibles avant la réponse finale.

**Timeline rail dans l’IDE** : le shim **`ide_event_shim`** projette les phases TUI en stations `read` / `propose` / `plan` / `act` / `verify` / `answer` — **affichage uniquement**, pas un conducteur moteur comme en 1.4.

```mermaid
sequenceDiagram
  autonumber
  participant U as Utilisateur
  participant IDE as IDE
  participant SH as Shim RPC
  participant M as Boucle TUI
  participant L as LLM

  U->>IDE: message
  IDE->>SH: agent.run + params vignettes
  SH->>M: demarrage run
  loop Chaque tour
    M->>L: prompt + outils + historique
    L-->>M: phase: + texte + tool_calls
    M->>SH: AgentEvent
    SH->>IDE: phase_enter + rail_station synthetique
    opt outil client
      M->>IDE: tool/exec
      IDE-->>M: resultat
    end
  end
  M->>SH: phase done + stop
  SH->>IDE: agent/done
```

---

## FR — Garde-fous

| Mécanisme | Effet |
|-----------|--------|
| `PermissionMode` | `plan` / `acceptEdits` / `default` / hooks |
| Permissions chemins + bash | Allow / ask / deny sur le workspace |
| `[phase: done]` | Clôture explicite du run |
| Compaction contexte | Snip / résumé quand la fenêtre LLM déborde |
| `maxIterations` | Plafond de tours (vignette Configuration) |

**Retiré avec la 1.4.x** : run rail observateur, ACL par station, `tool_folders`, `delegate_executor`, intent probe, `internal_plan_write` moteur 1.4, orchestration `role_split`.

---

## FR — Persistance session

```mermaid
flowchart TB
  subgraph DISK[".drox/ (workspace)"]
    TR["transcript JSONL par session"]
    UIJ["journal UI replay"]
    MEM["memory/ — DROX.md, notes"]
    SESS["metadonnees session"]
  end

  MOTEUR["Moteur TUI"] --> TR
  IDE["IDE"] --> UIJ
  MOTEUR --> MEM
```

---

## FR — Ce que le produit n’est pas

| Pas | Détail |
|-----|--------|
| IDE agent « prod » | Toujours expérimental — mais base 1.5 bien plus saine que 1.4 |
| Moteur 1.4.x | Rail observateur **obsolète** — archivé |
| Index sémantique / graphe | Piste 1.5.2+ |
| Signature Authenticode | Prévu 1.5.1+ — SmartScreen « Éditeur inconnu » |
| Code source moteur ouvert | — |

---

## EN — Project goal — sovereignty

Drox aims for **digital sovereignty**: local IDE and agent engine, LLM via **Ollama** (or an API you configure), session data in **`.drox/`** on your disk — no mandatory KDDS cloud account, no Microsoft telemetry in the installer.

**Only network exception**: **version check** (reading `stable/latest.json` on this repo) to offer an update when a newer release exists. Nothing else is required to work with the agent.

---

## EN — Status (1.5.0)

> **Drox 1.5.0 fully replaces the 1.4.x engine** (observer rail, `role_split`, IDE orchestration — all **gone**).  
> Still **experimental** — not a production daily driver — but **much more stable** than 1.4.2: proven TUI mono-loop, RPC shim, validated dogfood.

| | |
|---|---|
| **Version** | [**1.5.0**](https://github.com/DroxKiwi/Drox---IDE---OR/releases/latest) (June 2026) · VS Code base **1.126.0** |
| **Daily driver?** | **No** — early adopters / dogfood / curious users accepting bugs and breaking changes. |
| **Why try anyway?** | **Rewritten** engine stack (no patched 1.4 rail); Windows installer, local Ollama, file mutations validated in dogfood. |
| **1.4.x** | **Obsolete** — last ship 1.4.2; do not build or document on it. |

**In short**: *experimental yes, brittle lab no — first release on the new engine foundation.*

---

## EN — Overview

Install **Drox IDE**, run **Ollama**, open your project. **Drox Chat** talks to local **`drox.exe`** over stdio NDJSON; the engine calls your model and asks the IDE back for client-side work (LSP, diffs, workspace file writes, blocking questions).

**The stack** — same coarse diagrams as FR: IDE ↔ `drox.exe` ↔ Ollama, with the **RPC shim** between IDE wire format and the **TUI agent loop**.

| Piece | Role |
|-------|------|
| **Ollama** | Local inference — your chosen model |
| **drox.exe** | TUI mono-loop agent + JSON-RPC shim to the IDE |
| **Drox IDE** | Editor + chat + client tool execution |
| **You** | Repo, model, Config / Architect vignettes, permission mode |

No mandatory KDDS cloud. Session data in **`.drox/`** on disk.

---

## EN — Architecture 1.5.0: three layers

**Electron IDE** + **Rust engine**. Engine 1.5 is **not** the 1.4 rail conductor: it is the original TUI loop with an **adapter** for the existing chat UI.

1. **IDE** — chat webview, spawns `drox --serve`, runs client tools, renders stream. Does **not** drive agent logic.  
2. **RPC shim** (`drox-cli/jsonrpc`) — maps vignette params → `LlmConfig` + `PermissionMode`; relays TUI events; synthesizes `rail_station_*` for the timeline.  
3. **TUI core** (`agent.rs`) — LLM turns, `[phase: …]` protocol, tools, permissions, session. Pipeline **`tui_mono`** — no `role_split`.

---

## EN — One message → one run

Each send triggers **`agent.run`** → single **TUI loop**. No 1.4 discuss/edit routing, no intent probe, no multi-role orchestration.

Permission vignettes map to engine modes: **Analyze** → `plan`, **Trust edit** → `acceptEdits`, **I'm not crazy** → `default`. Legacy RPC fields (`orchestrationMode`, `architectInteractionMode`) are **ignored**.

Phases: `analyzing` → `reading` → optional `clarifying` / `planning` → `acting` → `testing` / `verifying` → `answering` → **`done`**. Only **`[phase: done]`** ends the run. **`answering`** text is the visible chat reply.

The IDE rail timeline is **synthetic** (`ide_event_shim`) for display — not a 1.4-style engine conductor.

---

## EN — Guardrails & session

Same as FR: `PermissionMode`, path/bash permissions, explicit `done`, context compaction, `maxIterations`. **Removed with 1.4.x**: observer rail, per-station ACL, `tool_folders`, `delegate_executor`, intent probe, 1.4 `internal_plan_write`, `role_split`.

`.drox/` holds JSONL transcript, UI replay journal, memory files.

---

## EN — What the product is not

| Not | Detail |
|-----|--------|
| Production agent IDE | Still experimental — 1.5 foundation is much healthier than 1.4 |
| 1.4.x engine | Observer rail **obsolete** — archived |
| Semantic index / graph | Planned 1.5.2+ |
| Authenticode signing | Planned 1.5.1+ |
| Open engine source | — |

---

## Liens / Links

| FR | EN |
|----|-----|
| [NOTICE.md](NOTICE.md) | License & attributions |
| [stable/1.5.0/RELEASE_NOTES.md](stable/1.5.0/RELEASE_NOTES.md) | Release notes |
| [Issues](https://github.com/DroxKiwi/Drox---IDE---OR/issues) | Install & update issues |
| Sources (privé) | Branche `1.5.0` sur dépôt KDDS |

---

*KDDS — Drox IDE. Built on Code OSS. Engine & branding proprietary.*
