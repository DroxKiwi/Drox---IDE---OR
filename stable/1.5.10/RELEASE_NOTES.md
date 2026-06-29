# Drox IDE 1.5.10

## Nouveautés

- **Run recovery toujours dispo** : **Reprendre** et **Recommencer** restent sur votre dernier message utilisateur — pendant un run, après annulation, ou après une erreur LLM. **Recommencer** fonctionne même pendant un run actif (arrêt + relance propre).
- **Recovery après redémarrage** : en rouvrant une session, les boutons reviennent sur le dernier message user (contexte sauvegardé dans `.drox/sessions/`).
- **Changement de modèle en plein run** : le respawn du moteur est **reporté** à la fin du run — plus de `drox client closed` en milieu de conversation.
- **Métriques live** : la barre `↑ ↓ ctx` se met à jour pendant le run, pas seulement à la fin.
- **Composer** : padding intérieur du champ de saisie (placeholder plus lisible).

## Correctifs

- Rattachement des boutons recovery après rejeu du journal UI / historique session.
- Fallback recovery depuis le transcript si le fichier de persistance est absent.

## Base

- **1.5.9** + run recovery, respawn différé, métriques live.
- **Base VS Code** : **1.127.0** (inchangée).

## Prérequis

**Windows** : Windows 10+ 64 bits · [WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) · [Ollama](https://ollama.com/) ou LLM compatible

**Linux** : Ubuntu 22.04 / 24.04 amd64 · dépendances graphiques standard · Ollama ou LLM compatible

## Licence

Produit Drox — voir [NOTICE.md](../../NOTICE.md).
