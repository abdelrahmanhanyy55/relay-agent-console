# Relay Agent Console

An interactive front-end for an LLM agent workspace, designed to connect a server-side agent route with multiple model providers and MCP tools.

## What is included

- An agent console with model selection, prompt composer, tool policy selector, thread display, and tool status panel.
- `backend/mcp.servers.example.json`: an editable registry for local-command and HTTP MCP servers.
- `backend/.env.example`: server-only environment names for provider and MCP credentials.

## Wire a production backend

1. Copy `backend/mcp.servers.example.json` to `backend/mcp.servers.json` and tailor the enabled servers.
2. Copy `backend/.env.example` to `backend/.env` on your backend host and set `OPENROUTER_API_KEY` there. Keep this file private and out of Git.
3. Implement `GET /api/models` on the server. It should retrieve the models available through OpenRouter and return a safe model list to the browser; the OpenRouter token must remain server-side.
4. Implement `POST /api/agent/run` on the server. It should accept the model selected in the interface, load only enabled MCP servers, call OpenRouter, and return the reply/tool trace.
5. Change the `send()` handler in `dist/index.html` from the current local prototype message to a fetch call to that endpoint.

The deployed Vercel interface should call your backend URL; only your backend calls OpenRouter. Never ship API keys, bearer tokens, or MCP credentials to the browser.

