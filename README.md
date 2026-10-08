# Relay Agent Console

An interactive front-end for an LLM agent workspace, designed to connect a server-side agent route with multiple model providers and MCP tools.

## What is included

- An agent console with model selection, prompt composer, tool policy selector, thread display, and tool status panel.
- `backend/mcp.servers.example.json`: an editable registry for local-command and HTTP MCP servers.
- `backend/.env.example`: server-only environment names for provider and MCP credentials.

## Wire a production backend

1. Copy `backend/mcp.servers.example.json` to `backend/mcp.servers.json` and tailor the enabled servers.
2. Configure the environment values in your deployment secret store.
3. Implement `POST /api/agent/run` on the server. It should select the requested provider, load only enabled MCP servers, call the model, and return the reply/tool trace.
4. Change the `send()` handler in `dist/index.html` from the current local prototype message to a fetch call to that endpoint.

Never ship API keys, bearer tokens, or MCP credentials to the browser.

