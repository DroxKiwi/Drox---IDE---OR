# Drox IDE 1.4.1

## Avertissement — plus stable, encore expérimentale

La **1.4.1 est nettement plus stable que la 1.4.0** : intent probe, patch rail VERIFY, plan interne, tool folders, profil moteur unique, Settings release simplifiés.

**Elle reste expérimentale** : réservée au **dogfood, au développement et aux early adopters** — pas un IDE agent « quotidien » en production. Des boucles, lenteurs modèle ou comportements inattendus sont encore possibles.

Polish UI chat → **1.4.2** · index / graphe → **1.4.3**.

---

## Nouveautés (moteur)

- **Intent probe** : routage discuss vs edit plus fiable (anglais moteur, marqueurs gates).
- **Patch rail 1.4.1.2** : hold READ→PLAN, VERIFY sans mutation, gate `done`, anti-spirale `file_write`, bash Windows.
- **Context frame & tool folders** : protocole outils par dossier, plan interne L2 (`internal_plan_write`), nudges protocole `[tool_use]`.
- **Profil produit unique** : fin des réglages utilisateur `engine.strictness` / `engine.tuning.*` — tuning moteur fixe côté KDDS.
- **Observabilité** : export transcript + engine trace (parties A/E), événements `LlmTurnPrepared` / run rail.

## Nouveautés (IDE)

- **`droxSurface`** : build **release** = catalogue Settings minimal (~15 clés) ; **dev** (F5) = réglages LLM avancés et `drox.executablePath` (Settings IDE uniquement).
- Stamp build moteur (epoch + git) en surface dev ; header chat semver seul en release.
- Export discussion (dev), layout chat par fenêtre, garde-fous bundle avant publication.

## Prérequis

- Windows 10 ou plus récent (64 bits)
- [WebView2 Runtime](https://developer.microsoft.com/microsoft-edge/webview2/)
- [Ollama](https://ollama.com/) pour le chat local (recommandé)

## Publication de cette version

Manifestes versionnés dans ce dépôt. L’installeur Windows est publié via **GitHub Release** (`v1.4.1`) — voir le guide sources `drox-engine/docs/operations/GUIDE-PUBLICATION-WIN32.md` :

```powershell
# Sources Drox---IDE : droxVersion = 1.4.1 puis
npm run drox:ship
# Puis commit + push ici (stable/) et gh release create avec _upload\*.exe
```

## Licence

Basé sur Code OSS (MIT). Voir [NOTICE.md](../../NOTICE.md).
