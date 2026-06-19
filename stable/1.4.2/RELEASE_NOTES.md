# Drox IDE 1.4.2

## Avertissement — moteur obsolète, phase expérimentale agressive

La **1.4.2** clôt la branche 1.4.x sur le plan **rail observateur + contexte en 4 couches**. C’est la **dernière livraison** de cette architecture : le moteur **va complètement changer** — ne pas bâtir dessus.

**Usage recommandé** : **dogfood, curiosité, early adopers** qui acceptent régressions, comportements inattendus et builds cassants sans préavis. **Pas** un IDE agent de production.

Installeur **non signé** (SmartScreen « Éditeur inconnu ») — normal jusqu’à la signature prévue en 1.4.3+.

---

## Nouveautés majeures (moteur)

- **Rail observateur** : fin du rail prescriptif — plus d’ACL outils par station, plus de `tool_folders`, plus de nudges coercitifs (`stall_read`, `stall_act`, `force_act`, mutation forcée sur `done`).
- **Palette outils stable** : tous les outils wire visibles tout le run EDIT ; protocole compact unique.
- **Contexte 4 couches** : cadre boot + hint rail · outils · snapshot run + plan interne · transcript + compaction checkpoint.
- **Routage statique** : `discuss` / `analyze` / `edit` via mode IDE ou RPC — **suppression de l’intent probe** LLM au boot.
- **Plan interne seul** : `internal_plan_write` remplace `todo_write` ; gates todo retirées.
- **Mémoire unifiée** : `DROX.md` seul ; boot allégé ; checkpoint compaction → snapshot `## Run context (engine)`.
- **Prompt observateur** : `01_core_rail_solo.md` réécrit — rail = hint informatif, pas de `[gate:]` prescriptif.

## Nouveautés (IDE)

- Sélecteur **num_ctx** architecte (16k → 1M) — panneau Architecte.
- Surface **release** : header chat semver seul, catalogue Settings minimal.
- Garde-fous bundle alignés sur `droxVersion` avant publication.

## Prérequis

- Windows 10 ou plus récent (64 bits)
- [WebView2 Runtime](https://developer.microsoft.com/microsoft-edge/webview2/)
- [Ollama](https://ollama.com/) pour le chat local (recommandé)

## Après cette version

Refonte moteur **profonde** annoncée — pas un simple polish UI. Voir dépôt sources `Drox---IDE` (README racine).

## Licence

Basé sur Code OSS (MIT). Voir [NOTICE.md](../../NOTICE.md).
