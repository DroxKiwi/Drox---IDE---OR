# Drox IDE — releases officielles

**Ce dépôt** : binaires Windows, manifestes de mise à jour (`stable/latest.json`), notes de version.  
**Pas les sources** — produit propriétaire [KDDS](https://github.com/DroxKiwi). Socle Code OSS (MIT) + moteur Drox — voir [NOTICE.md](NOTICE.md).

**Dernière version** : [1.3.2](https://github.com/DroxKiwi/Drox---IDE---OR/releases/latest)

---

## FR

### C’est quoi, Drox IDE ?

Un IDE pour coder **avec un agent local** — pas un wrapper Copilot, pas un SaaS qui aspire ton repo. Tu installes, tu branches **Ollama** (ou une API compatible), tu parles à **Drox Chat**. Point.

L’app embarque le binaire **`drox`** (moteur Rust). Pas de compte KDDS obligatoire. Pas de télémétrie Microsoft dans le package. Les MAJ passent par ce repo (`latest.json` + Releases GitHub).

### Le moteur Drox — ce qu’il sait faire (sans spoiler le code)

Le moteur, c’est le cerveau **hors du navigateur** : boucle LLM ↔ outils, en local. L’IDE ne fait que l’UI, le LSP, les diffs et les trucs qu’un binaire ne peut pas faire seul dans ton workspace.

**Deux têtes, un patron**

- **Architecte** — comprend la demande, pose un plan (`todo_write`), découpe le boulot, **délègue** au lieu de tout mâcher dans un seul fil de chat.
- **Exécuteurs** — agents courts, **périmètre verrouillé** (un scope = pas de vadrouille dans tout le monorepo). Plusieurs tâches **en parallèle** si les scopes ne se marchent pas dessus.

**Modes**

- **Discussion** — salut, avis, explication : réponse directe, pas de circus d’outils.
- **Édition** — tu veux du concret : lecture workspace, grep, patches, commandes, livrables dans `.drox/agent-output/`.

**Outils (côté utilisateur, pas côté rust)**

- Fichiers : lire, écrire, éditer, chercher (`grep` / `glob`).
- Terminal contrôlé (`bash`), fetch web en lecture.
- **LSP** (définitions, refs, diagnostics) — exécuté par l’IDE, résultat renvoyé au moteur.
- Plan / todos, questions utilisateur (oui/non, choix multiples).
- **Sessions** persistantes, historique, compaction quand ça grossit.
- Mémoire projet (fichiers `.drox/`, notes de session) pour ne pas repartir de zéro à chaque run.

**Garde-fous (le truc qui évite les runs pourris)**

- Pas de « j’ai fini » tant qu’il reste des todos ouverts.
- Pas de délégation sans plan.
- Pas de scope exécuteur flou du type « refacto tout le projet ».
- Si un exécuteur plante : rapport d’échec structuré, retry ciblé — pas un dump de 400 messages dans ton chat.

**Ce que ce n’est pas (encore)**

- Pas d’index sémantique / RAG maison au niveau 1.3.2 (prévu 1.3.3).
- Pas de cloud KDDS imposé — ton LLM, ta machine.
- Pas open source : on décrit les **capacités**, pas la recette.

### Installer / mettre à jour

1. [Releases](https://github.com/DroxKiwi/Drox---IDE---OR/releases) → `Drox-IDE-Setup-*-win32-x64.exe`
2. **Ollama** recommandé : [ollama.com](https://ollama.com/)
3. L’IDE vérifie `stable/latest.json` au démarrage ; notif si une version plus récente est publiée ici.

### Liens

| | |
|---|---|
| Licence & attributions | [NOTICE.md](NOTICE.md) |
| Notes 1.3.2 | [stable/1.3.2/RELEASE_NOTES.md](stable/1.3.2/RELEASE_NOTES.md) |
| Issues (install, MAJ) | [Issues](https://github.com/DroxKiwi/Drox---IDE---OR/issues) |

---

## EN

### What is Drox IDE?

An IDE built around a **local coding agent** — not a Copilot skin, not a SaaS vacuuming your repo. Install, point **Ollama** (or a compatible API) at it, use **Drox Chat**. Done.

The app ships the **`drox`** engine (Rust). No mandatory KDDS account. No Microsoft telemetry in the package. Updates are served from this repo (`latest.json` + GitHub Releases).

### The Drox engine — what it can do (no implementation spoilers)

The engine is the **brain outside the webview**: LLM ↔ tools loop, on your machine. The IDE handles UI, LSP, diffs, and anything a standalone binary cannot safely do in your workspace.

**Two roles, one boss**

- **Architect** — understands the ask, builds a plan (`todo_write`), splits work, **delegates** instead of rambling in one endless chat thread.
- **Executors** — short-lived agents with a **locked scope** (one scope = no wandering across the whole monorepo). Multiple tasks **in parallel** when scopes do not overlap.

**Modes**

- **Discuss** — hi, opinions, explanations: direct answer, no tool circus.
- **Edit** — you want real work: workspace reads, grep, patches, commands, deliverables under `.drox/agent-output/`.

**Tools (user-facing)**

- Files: read, write, edit, search (`grep` / `glob`).
- Controlled shell (`bash`), read-only web fetch.
- **LSP** (definitions, references, diagnostics) — run by the IDE, results fed back to the engine.
- Plan / todos, user questions (yes/no, multiple choice).
- **Persistent sessions**, history, compaction when context gets fat.
- Project memory (`.drox/` files, session notes) so every run does not start from zero.

**Guardrails (the stuff that stops garbage runs)**

- No “I’m done” while todos are still open.
- No delegation without a plan.
- No vague executor scope like “refactor the entire project”.
- Executor failure → structured failure report, targeted retry — not a 400-message transcript dump in your chat.

**What it is not (yet)**

- No home-grown semantic index / RAG at 1.3.2 level (planned 1.3.3).
- No forced KDDS cloud — your LLM, your machine.
- Not open source: we describe **capabilities**, not the recipe.

### Install / update

1. [Releases](https://github.com/DroxKiwi/Drox---IDE---OR/releases) → `Drox-IDE-Setup-*-win32-x64.exe`
2. **Ollama** recommended: [ollama.com](https://ollama.com/)
3. The IDE checks `stable/latest.json` on startup; you get a notification when a newer release is published here.

### Links

| | |
|---|---|
| License & attributions | [NOTICE.md](NOTICE.md) |
| 1.3.2 notes | [stable/1.3.2/RELEASE_NOTES.md](stable/1.3.2/RELEASE_NOTES.md) |
| Issues (install, updates) | [Issues](https://github.com/DroxKiwi/Drox---IDE---OR/issues) |

---

*KDDS — Drox IDE. Built on Code OSS. Engine & branding proprietary.*
