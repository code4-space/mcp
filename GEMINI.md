# Code4

This extension connects Gemini CLI to the Code4 MCP server at `https://mcp.code4.space/mcp`.

Code4 is one workspace for small software teams: issues and boards, git hosting and code review, CI/CD pipelines, deployments, documents, chat and calls, with one knowledge base over all of it.

The server is named `c4`. Its tools cover issues and sprints, code review, repositories, CI/CD pipelines, deployments, documents, time tracking, personal to-dos and team knowledge search.

## Sign-in

The server uses OAuth with the user's own Code4 account. Gemini CLI opens the Code4 sign-in page the first time it calls a Code4 tool. The tools see only what that account can see and act with its permissions.

## Tool annotations

Read-only tools carry `readOnlyHint`. Tools that deploy, merge, delete, rewrite branches, run pipelines or change secrets carry `destructiveHint`. Code4 adds no confirmation step of its own; Gemini CLI asks the user according to its own confirmation settings.

## Links

- Documentation: https://code4.space/docs/#/integrations/mcp
- Privacy policy: https://code4.space/privacy/
- Support: support@code4.space
