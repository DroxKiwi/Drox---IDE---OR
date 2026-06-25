# Drox IDE 1.5.4

## Correctifs (juin 2026)

- **Questionnaire chat** (`ask_user_question`) : les formulaires multi-questions conservent toutes les réponses (y compris quand le modèle envoie le JSON en chaîne).
- **Carte Questions** : plus de perte de réponses lors d’un `agent/done` tardif d’un run précédent ; validation avant envoi vide.

## Nouveautés

- **Release Linux** : paquet `.deb` amd64 (`linux-x64`).
- **Galerie extensions** : Open VSX (recherche et installation depuis la vue Extensions).
- **Ouvrir avec Drox** : menu contextuel Windows et Linux (fichiers et dossiers).
- **UI chat TUI** : cadres carrés, questionnaire et plans.
- **Base VS Code** : **1.127.0** (intégration upstream).

## Prérequis

**Windows** : Windows 10+ 64 bits · [WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) · [Ollama](https://ollama.com/) ou LLM compatible

**Linux** : Ubuntu 22.04 / 24.04 amd64 · dépendances graphiques standard · Ollama ou LLM compatible

## Licence

Produit Drox — voir [NOTICE.md](../../NOTICE.md).
