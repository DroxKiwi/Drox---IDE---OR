# Drox IDE 1.5.7

## Nouveautés

- **Reprise après erreur LLM** : quand un run est coupé (erreur serveur, timeout, etc.), la dernière bulle utilisateur affiche **Reprendre** et **Recommencer**.
  - **Reprendre** — relance depuis le point de coupure (sortie partielle du modèle conservée).
  - **Recommencer** — efface tout ce que le modèle a produit depuis ce message, puis relance.

## Technique

- Moteur : `agent.run` avec `skipUserTurn`, RPC `session.truncateAfterLastUser`.
- Splash « What's new » dédié à cette version (plus de renvoi vers la doc générique).

## Base

- **1.5.6** + correctifs chat webview.
- **Base VS Code** : **1.127.0** (inchangée).

## Prérequis

**Windows** : Windows 10+ 64 bits · [WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) · [Ollama](https://ollama.com/) ou LLM compatible

**Linux** : Ubuntu 22.04 / 24.04 amd64 · dépendances graphiques standard · Ollama ou LLM compatible

## Licence

Produit Drox — voir [NOTICE.md](../../NOTICE.md).
