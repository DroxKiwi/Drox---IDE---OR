# Drox IDE 1.5.11

## Nouveautés

- **Chat natif Drox** : le panneau **Drox** de l’IDE utilise désormais le fil `ChatWidget` + `drox.exe` (même stack que la fenêtre Agents). L’onglet webview legacy reste disponible via `drox.ideLegacyWebviewChat.enabled`.
- **Config partagée** : serveur, modèle et mode de permission sont stockés une fois (scope utilisateur) et restent alignés entre l’IDE et la fenêtre Agents.
- **Historique sessions** : rouvrir `.drox/sessions` depuis le panneau Drox ou la barre latérale Agents ; les choix restent synchronisés entre les deux surfaces.
- **Modifications de fichiers dans le fil natif** : cartes diff inline avec undo/redo.
- **Open in Agents** : raccourci barre de titre pour passer de l’éditeur à la fenêtre Agents sur le même projet.

## Correctifs

- Persistance du modèle architecte entre IDE et fenêtre Agents (plus d’écrasement au focus AW).
- Titres de session lisibles · clic historique AW · premier chargement AW.

## Base

- **1.5.10** + chat natif nominal IDE, historique partagé, CFG unifiée.
- **Base VS Code** : **1.127.0** (inchangée).

## Prérequis

**Windows** : Windows 10+ 64 bits · [WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) · [Ollama](https://ollama.com/) ou LLM compatible

**Linux** : Ubuntu 22.04 / 24.04 amd64 · dépendances graphiques standard · Ollama ou LLM compatible

## Licence

Produit Drox — voir [NOTICE.md](../../NOTICE.md).
