# Drox IDE 1.5.9

## Nouveautés

- **Scroll intelligent** : pendant qu’un run est actif, remonter dans le fil pour lire ne vous ramène plus en bas à chaque delta ; le fil reprend le suivi automatique quand vous redescendez en bas.
- **Reset workspace** : le bouton du panneau Sessions supprime aussi **`MEMORY.md`** à la racine du workspace, en plus de `.drox/sessions` et du reste des données Drox (`.drox/.env` conservé).
- **Composer épuré** : retrait des quatre icônes redondantes sous le champ de saisie (réglages, dossier, trombone, rechargement modèles).

## Accès conservés

- Réglages : vignette **Settings** au-dessus du champ de saisie.
- Références fichiers : `@chemin` dans le prompt.
- Images : glisser-déposer ou coller dans le composer.

## Correctifs

- Dialogue et message de confirmation du reset workspace clarifiés (`MEMORY.md`, sessions).

## Base

- **1.5.8** + UX chat (scroll, reset, composer).
- **Base VS Code** : **1.127.0** (inchangée).

## Prérequis

**Windows** : Windows 10+ 64 bits · [WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) · [Ollama](https://ollama.com/) ou LLM compatible

**Linux** : Ubuntu 22.04 / 24.04 amd64 · dépendances graphiques standard · Ollama ou LLM compatible

## Licence

Produit Drox — voir [NOTICE.md](../../NOTICE.md).
