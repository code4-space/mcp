# Code4

This extension connects Gemini CLI to the Code4 MCP server at `https://mcp.code4.space/mcp`.

Code4 is a software development platform for teams and AI agents: issues and boards, git hosting and code review, CI/CD pipelines, deployments, documents, chat and calls. Its knowledge base holds chat messages, issues, code reviews, documents, call transcripts and commit messages. Source code is searched with full-text search and symbol lookup: `search_repo_code` and `find_symbol`.

The server is named `c4`. Its tools cover issues and sprints, code review, repositories, CI/CD pipelines, deployments, documents, time tracking, personal to-dos and team knowledge search.

## Sign-in

The server uses OAuth with the user's own Code4 account. Gemini CLI opens the Code4 sign-in page the first time it calls a Code4 tool; `/mcp auth c4` starts sign-in by hand. The tools see only what that account can see and act with its permissions.

## Tool annotations

Read-only tools carry `readOnlyHint`. Tools that deploy, merge, delete, rewrite branches, run pipelines or change secrets carry `destructiveHint`. Code4 adds no confirmation step of its own; Gemini CLI asks the user according to its own confirmation settings.

## Links

- Documentation: https://code4.space/docs/#/integrations/mcp
- Privacy policy: https://code4.space/privacy/
- Support: support@code4.space
