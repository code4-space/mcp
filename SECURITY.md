# Security policy

This repository holds configuration files and documentation for the hosted Code4 MCP server at `https://mcp.code4.space/mcp`. It contains no server code.

## Reporting a vulnerability

Email **support@code4.space** with the subject line `Security report`. Please include:

- what you found and where (URL, tool name or file);
- steps to reproduce;
- the impact you expect;
- how we can reach you.

Please do not open a public GitHub issue for a security problem, and do not include passwords, access tokens or other people's data in your report.

We confirm receipt and keep you informed while we investigate. Please give us reasonable time to fix the problem before you disclose it publicly.

## Scope

In scope:

- the MCP server at `mcp.code4.space`, including its OAuth metadata and public endpoints;
- sign-in and consent for MCP clients;
- the files in this repository.

Out of scope: denial of service, social engineering, and findings that need a compromised device or account.

## How access works

The server accepts only OAuth sign-in with a Code4 account. Every tool call runs with the signed-in person's permissions. People can revoke a connected AI client at any time in Code4 under **Preferences → AI Integrations → Connected AI clients**.
