# Drox IDE 1.5.12

## Nouveautés

- **Workspace Agents façon Cursor** : panneau Changes branché sur le moteur Drox, diff inline, liste chronologique, onglets fichier · terminal · browser unifiés.
- **Git depuis le composer** : actions commit, commit & push et création de PR (via agent) dans la fenêtre Agents.
- **Marketplace MCP curated OSS** : catalogue embarqué (`drox-engine/mcp-registry`) — installation vers `.mcp.json` sans registry Copilot.
- **Open in Browser** : ouvrir une session dans le navigateur depuis la barre de titre Agents.
- **Reset workspace** : « Reset Drox data for this workspace » dans le chat natif IDE et fenêtre Agents.
- **Phrases thinking Drox** : plus de « Working » générique dans le header thinking.
- **Branding Drox** : footers, permissions et quotas sans mention « GitHub Copilot » ; chemins customizations `.drox/agents`.

## Correctifs & fiabilité

- **Installateur Windows** : exclusion `@opentelemetry` et du bundle `extensions/copilot` en release — corrige l’erreur NSIS « impossible de renommer un fichier » à la mise à jour.
- Remote session access / tunnel host désactivés par défaut (surface Microsoft off).
- Surfaces Copilot / chat MS masquées (`droxMicrosoftAgentsSurfaceEnabled: false`).

## Base

- **1.5.11** + workspace Cursor natif, MCP marketplace, purge bundle Copilot release.
- **Base VS Code** : **1.127.0** (inchangée).

## Prérequis

**Windows** : Windows 10+ 64 bits · [WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) · [Ollama](https://ollama.com/) ou LLM compatible

**Linux** : Ubuntu 22.04 / 24.04 amd64 · dépendances graphiques standard · Ollama ou LLM compatible

## Licence

Produit Drox — voir [NOTICE.md](../../NOTICE.md).
