# Drox IDE 1.5.6

## Correctifs (juin 2026)

- **Messages utilisateur** : bulle affichée immédiatement à l'envoi (séparateur de tour), y compris après erreur réseau ou reprise de session.
- **Diffs fichier** : scroll interne restauré (`max-height` + défilement) pour ne plus étirer tout le fil.
- **Réponses assistant** : routage fil corrigé (pas de réponses perdues après l'affichage optimiste user).
- **Indicateur de travail** : ligne warmup (grille + phrase) toujours visible pendant un cycle ; grille réservée à cette phrase uniquement.
- **Bouton envoyer** : style carré TUI + animation pulse en mode run (arrêt).

## Base

- **1.5.5** (fil linéaire) + correctifs chat webview post-release.
- **Base VS Code** : **1.127.0** (inchangée).

## Prérequis

**Windows** : Windows 10+ 64 bits · [WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) · [Ollama](https://ollama.com/) ou LLM compatible

**Linux** : Ubuntu 22.04 / 24.04 amd64 · dépendances graphiques standard · Ollama ou LLM compatible

## Licence

Produit Drox — voir [NOTICE.md](../../NOTICE.md).
