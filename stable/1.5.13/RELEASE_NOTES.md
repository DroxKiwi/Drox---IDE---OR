# Drox IDE 1.5.13

## Nouveautés

- **Sessions parallèles** : envoi non bloquant — une discussion peut continuer en arrière-plan pendant que vous ouvrez une autre session.
- **Nouvelle discussion** : le bouton New ouvre le compositeur sans héritage du dossier actif ; choix explicite du projet.

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
