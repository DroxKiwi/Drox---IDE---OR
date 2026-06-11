# Drox IDE 1.4.0

## ⚠️ Avertissement — version squelette

Cette release embarque la **refonte moteur 1.4.0** (run rail, architecte solo). Le produit reste en **phase de stabilisation** : usage **dogfood / développement** uniquement, pas pour un travail agent quotidien en production.

Les correctifs session, UI busy, discuss et boucles sont prévus en **1.4.1**.

---

## Nouveautés (moteur)

- **Run rail** : conducteur unique (stations intent → read → plan → act → verify → answer).
- **Architecte solo** : suppression du chemin Executor / `delegate_executor` / segments ACT / Professor / Standard CLI côté IDE.
- Prompt edit unique : `01_core_rail_solo.md`.
- Boucle agent modulaire (`rail/`, `loop/drive/`, `gates/`, `state/`, `stream/`).
- UI chat : retrait executor/delegate dans les réglages et la webview (phase 2d).

## Prérequis

- Windows 10 ou plus récent (64 bits)
- [WebView2 Runtime](https://developer.microsoft.com/microsoft-edge/webview2/)
- [Ollama](https://ollama.com/) pour le chat local (recommandé)

## Licence

Basé sur Code OSS (MIT). Voir [NOTICE.md](../../NOTICE.md).
