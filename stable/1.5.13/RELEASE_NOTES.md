# Drox IDE 1.5.13

## Nouveautés

- **Sessions parallèles** : envoi non bloquant — une discussion peut continuer en arrière-plan pendant que vous ouvrez une autre session.
- **Nouvelle discussion** : le bouton New ouvre le compositeur sans héritage du dossier actif ; choix explicite du projet.

## Correctifs (2026-07-04 — hotfix layout, suppression session)

- **Relance app** : la zone web + terminal est de nouveau restaurée après fermeture / réouverture (working set éditeur + visibilité du panel persistés).
- **Écran vide au démarrage** : relayout automatique après restauration des sessions — plus besoin d’un clic pour afficher le contenu.
- **Supprimer une discussion** : le menu contextuel **Delete...** supprime réellement la conversation (fichiers `.drox/sessions`) au lieu de créer un brouillon **New Session** ; bascule vers une autre discussion existante si possible.

## Correctifs (2026-07-03 — hotfix streaming arrière-plan)

- **Discussion en cours** : changer de session pendant une réponse du modèle ne coupe plus le run — le stream continue en arrière-plan et le fil est intact au retour.
- **Liste Sessions** : indicateur **In Progress** (spinner) sur la discussion pendant le traitement en arrière-plan.

## Correctifs (2026-07-03 — hotfix rebuild)

- Rebuild installateur Windows et paquet Linux (même version **1.5.13**, nouveaux SHA256 sur OR).
- Si au relancement vous voyez l’écran **Electron** (« path-to-app ») : utiliser le raccourci **Menu Démarrer → Drox IDE → Drox IDE** (install `%LocalAppData%\Programs\Drox IDE`), pas un ancien raccourci pointant vers un dossier de développement. Désépingler puis réépingler depuis ce raccourci si besoin.

## Correctifs & fiabilité

- **Fil chat au switch** : historique visible après changement de session ou de dossier (ProjectBar), avec replay tail et résolution workspace corrigés.
- **Stabilisation Agents** : correction des boucles observables git/changes au boot et après réponse modèle (plus de freeze ni crash systématique).
- **Chargement initial** : écran New Session et arborescence projets visibles dès l’ouverture, sans clic ou alt-tab.
- **Liste Sessions** : projets et discussions apparaissent immédiatement dans le panneau gauche.

## Base

- **1.5.12** + stabilisation fenêtre Agents.
- **Base VS Code** : **1.127.0** (inchangée).

## Prérequis

**Windows** : Windows 10+ 64 bits · [WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) · [Ollama](https://ollama.com/) ou LLM compatible

**Linux** : Ubuntu 22.04 / 24.04 amd64 · dépendances graphiques standard · Ollama ou LLM compatible

## Licence

Produit Drox — voir [NOTICE.md](../../NOTICE.md).
