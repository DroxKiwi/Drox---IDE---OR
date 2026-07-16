# Drox IDE 1.5.14

## Nouveautés

- **Sessions background (Plan B)** : persistance optionnelle des sessions hors premier plan (toggle sur la carte, confirmation au switch, snapshots de layout en mémoire).
- **Template workspace** : à l’ouverture, chat + Changes ; l’éditeur reste masqué jusqu’à l’ouverture d’un fichier ou d’un shell.
- **Dashboard sessions** : lampes (shell / modèle / git / input) et métriques CPU, RAM, disque, download / upload (historique ~1 h, sparkline au survol).
- **Loading UI unifié** : kit de chargement partagé (Agents + IDE natif).
- **Moteur** : LoopDetector après les gates « done » ; prompts LLM en anglais.

## Correctifs

- **Menus** : fermeture instantanée (plus de layout retardé au focus).
- **Restore workspace** : restauration correcte lors d’un changement de répertoire.
- **Cold boot** : layouts différés via timers (évite le freeze au démarrage).

## Base

- **1.5.13** + Plan B sessions / loading / LoopDetector.
- **Base VS Code** : **1.127.0** (inchangée).

## Prérequis

**Windows** : Windows 10+ 64 bits · [WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) · [Ollama](https://ollama.com/) ou LLM compatible

**Linux** : Ubuntu 22.04 / 24.04 amd64 · dépendances graphiques standard · Ollama ou LLM compatible

## Licence

Produit Drox — voir [NOTICE.md](../../NOTICE.md).
