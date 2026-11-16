# Changelog

All notable changes to the public Code4 MCP listing files are recorded here. Versions match `version` in `server.json` and the plugin manifests.

## Unreleased

Documentation only; `server.json` and the manifests keep version 1.0.0.

- README: sign-in status per client (tested with Claude and Cursor), product description, knowledge base sources (source code is not in it).
- README: added `read_docs`, `list_clusters`, `list_namespace_options` and `create_environment` to the tool tables.
- Updated the path to connected AI clients (Preferences → AI Integrations → AI clients) and the note on call transcripts.

## 1.0.0

First public release.

- Remote MCP server at `https://mcp.code4.space/mcp` over Streamable HTTP, with OAuth 2.1 sign-in and Dynamic Client Registration.
- More than 200 tools for issues, sprints and boards, code review, repositories, CI/CD pipelines, deployments, documents, time tracking, personal to-dos and team knowledge search.
- Every tool has a human-readable title and MCP annotations (`readOnlyHint`, `destructiveHint`, `idempotentHint`, `openWorldHint`).
- `server.json` for the MCP Registry as `space.code4/mcp`.
- Plugin manifests for Claude Code, Agent Plugins (ChatGPT, Codex and Cursor) and Gemini CLI.
- Icons in SVG and PNG.
