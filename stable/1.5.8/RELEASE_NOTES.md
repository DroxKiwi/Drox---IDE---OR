# Drox IDE 1.5.8

## Nouveautés

- **Native thinking** : le flux de raisonnement Ollama s’affiche à nouveau dans les blocs **Reasoning** du panneau Work (fil chronologique).
- **Fil Work** : lectures et outils (`file_read`, `grep`, etc.) reprennent leur place **inline** dans la chronologie du tour, dans l’ordre des événements.
- **Vignette Planifier** : libellé aligné sur le mode Plan moteur (ex-« Analyze »).
- **Questionnaire** : padding gauche corrigé sur les cartes `ask_user`.

## Correctifs

- Phrase de warmup (statut geek) de retour **dans le fil** scrollable, pas collée au composer.
- Listes markdown et espacement chat légèrement améliorés.

## Technique

- Webview : `beginLinearRunStrip` au démarrage de run, routage `getLogMountParent` → chronologie strip.
- Roadmap : MCP + modes Ask/Analyse reportés en **1.5.9** ; Agents Window en **1.5.10**.

## Base

- **1.5.7** + polish UX chat.
- **Base VS Code** : **1.127.0** (inchangée).

## Prérequis

**Windows** : Windows 10+ 64 bits · [WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) · [Ollama](https://ollama.com/) ou LLM compatible

**Linux** : Ubuntu 22.04 / 24.04 amd64 · dépendances graphiques standard · Ollama ou LLM compatible

## Licence

Produit Drox — voir [NOTICE.md](../../NOTICE.md).
