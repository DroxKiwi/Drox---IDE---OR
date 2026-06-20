# Drox IDE 1.5.0

## Nouveautés

- **Nouveau moteur** : remplacement complet du rail 1.4.x par la mono-boucle TUI (`tui_mono`) + shim RPC vers l’IDE.
- Intégration **VS Code upstream 1.126.0**.
- Installeur Windows user (`Drox-IDE-UserSetup-1.5.0-win32-x64.exe`).
- Chat Drox + vignettes Configuration / Architecte + modes permission conservés.
- Dogfood validé (exploration, mutations fichier via `tool/exec`).

## Statut

Toujours **expérimental** — pas un produit de production — mais **nettement plus stable** que la 1.4.2 (stack moteur refondue, plus de rail observateur 1.4).

## Prérequis

- Windows 10 ou plus récent (64 bits)
- [WebView2 Runtime](https://developer.microsoft.com/microsoft-edge/webview2/) (souvent déjà installé)
- [Ollama](https://ollama.com/) pour le chat local (optionnel mais recommandé)

## Licence

Basé sur Code OSS (MIT). Voir [NOTICE.md](../../NOTICE.md).
