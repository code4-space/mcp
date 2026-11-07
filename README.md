<p align="center">
  <img src="icons/png/code4-icon-256.png" width="96" height="96" alt="Code4">
</p>

<h1 align="center">Code4 MCP server</h1>

<p align="center">
  Connect Claude, ChatGPT, Cursor, VS Code, Gemini CLI and other AI assistants to your Code4 workspace.
</p>

<p align="center">
  <a href="https://cursor.com/en/install-mcp?name=c4&config=eyJ1cmwiOiJodHRwczovL21jcC5jb2RlNC5zcGFjZS9tY3AifQ%3D%3D"><img src="https://cursor.com/deeplink/mcp-install-dark.svg" alt="Add to Cursor" height="32"></a>
  <a href="https://vscode.dev/redirect/mcp/install?name=c4&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.code4.space%2Fmcp%22%7D"><img src="https://img.shields.io/badge/VS_Code-Install_Code4-0098FF?logo=visualstudiocode&logoColor=white" alt="Install in VS Code" height="32"></a>
</p>

[Code4](https://code4.space) is one workspace for small software teams: issues and boards, git hosting and code review, CI/CD pipelines, deployments to your own Kubernetes, documents, chat and calls. Everything the team writes is indexed into one knowledge base that answers under each person's own permissions.

The Code4 MCP server is a hosted [Model Context Protocol](https://modelcontextprotocol.io) server. With it, your AI assistant works with your issues, code reviews, repositories, pipelines, deployments and documents, and searches what your team discussed and decided, as you and with your permissions.

This repository holds the public listing files for MCP directories and clients: `server.json`, plugin manifests, icons and this guide. The server itself is hosted by Code4; there is nothing to install or run locally.

| | |
|---|---|
| Server URL | `https://mcp.code4.space/mcp` |
| Transport | Streamable HTTP |
| Sign-in | OAuth 2.1 with your Code4 account |
| Recommended server name | `c4` |
| Registry name | `space.code4/mcp` |
| Tools | more than 200 |

## Contents

- [Before you start](#before-you-start)
- [Connect your client](#connect-your-client)
- [How sign-in works](#how-sign-in-works)
- [Tools](#tools)
- [Permissions and security](#permissions-and-security)
- [Data handling](#data-handling)
- [Troubleshooting](#troubleshooting)
- [Support](#support)
- [Files in this repository](#files-in-this-repository)

## Before you start

- You need a Code4 account and membership in at least one organization. [Sign up](https://code4.space/signup) if you do not have one.
- Your AI client must support remote MCP servers over Streamable HTTP **with OAuth sign-in**. Code4 does not accept a static token in a header, so clients that only support API keys cannot connect.
- If you add the server by hand, name it `c4`. The ready-made commands and prompts that Code4 gives you for coding agents call the tools as `mcp__c4__*`. When you install Code4 from a client's directory or as a plugin, the client picks the name, and that is fine.

Ready-made commands are also in the Code4 app under **Preferences → AI Integrations**.

We test new client versions as they come out. If a client below does not connect, write to support@code4.space with the client name and version.

## Connect your client

On first use, your client opens a browser window with the Code4 sign-in page. Sign in, then approve access on the consent screen. The name shown on the consent screen is the name the client gave itself.

### Claude Code

```sh
claude mcp add --scope user --transport http c4 https://mcp.code4.space/mcp
```

Then run `/mcp` in Claude Code, select `c4` and choose **Authenticate**. `--scope user` makes the server available in every project, not only in the current folder.

You can also install it as a Claude Code plugin from this repository:

```text
/plugin marketplace add code4-space/mcp
/plugin install code4@code4
```

### Claude (web, desktop and mobile)

1. Open **Customize → Connectors**, click **+ Add**, then **Add custom connector**.
2. Name: `Code4`. Remote MCP server URL: `https://mcp.code4.space/mcp`.
3. Under **Advanced settings → OAuth client**, choose **Register automatically**.
4. Click **Connect** and sign in to Code4.

On Team and Enterprise plans, an Owner first adds the connector in **Organization settings → Connectors**. Turn the connector on for a conversation from the **+** menu → **Connectors**. Connectors you add in Claude on the web also work in Claude Desktop and the mobile apps.

### ChatGPT

1. Open **Settings → Apps → Advanced settings** and turn on **Developer mode**.
2. In **Settings → Apps**, click **Create app**.
3. Name: `Code4`. MCP server URL: `https://mcp.code4.space/mcp`. Authentication: **OAuth**.
4. Sign in to Code4 when asked.

To use it, choose **Developer mode** from the **+** menu in a conversation and select Code4. Developer mode availability depends on your ChatGPT plan.

### Codex CLI

```sh
codex mcp add c4 --url https://mcp.code4.space/mcp
codex mcp login c4
```

If sign-in fails at the client registration step, run `codex mcp login c4 --oauth-client-registration dcr`.

### Cursor

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name=c4&config=eyJ1cmwiOiJodHRwczovL21jcC5jb2RlNC5zcGFjZS9tY3AifQ%3D%3D)

The button opens Cursor with this deeplink. You can also paste it into your browser:

```text
cursor://anysphere.cursor-deeplink/mcp/install?name=c4&config=eyJ1cmwiOiJodHRwczovL21jcC5jb2RlNC5zcGFjZS9tY3AifQ%3D%3D
```

Or add this to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "c4": { "url": "https://mcp.code4.space/mcp" }
  }
}
```

Open **Cursor Settings → MCP** and click **Connect** next to `c4` if Cursor asks you to sign in.

### VS Code (GitHub Copilot)

[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Code4-0098FF?logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect/mcp/install?name=c4&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.code4.space%2Fmcp%22%7D)

The button opens VS Code with this install link:

```text
vscode:mcp/install?%7B%22name%22%3A%22c4%22%2C%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.code4.space%2Fmcp%22%7D
```

For VS Code Insiders, replace `vscode:` with `vscode-insiders:`.

Or from the command line:

```sh
code --add-mcp '{"name":"c4","type":"http","url":"https://mcp.code4.space/mcp"}'
```

Or in `.vscode/mcp.json`:

```json
{
  "servers": {
    "c4": { "type": "http", "url": "https://mcp.code4.space/mcp" }
  }
}
```

VS Code sends at most 128 tools per request. Code4 has more, so open **Configure Tools** in the chat view and keep the groups you need.

### Gemini CLI

Install the extension from this repository:

```sh
gemini extensions install https://github.com/code4-space/mcp
```

Or add the server directly:

```sh
gemini mcp add --transport http c4 https://mcp.code4.space/mcp
```

Or in `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "c4": { "httpUrl": "https://mcp.code4.space/mcp" }
  }
}
```

Gemini CLI opens the sign-in page the first time it calls a Code4 tool.

### Devin Desktop (formerly Windsurf)

Add this to `~/.config/devin/mcp_config.json` (on Windows, `%APPDATA%\devin\mcp_config.json`):

```json
{
  "mcpServers": {
    "c4": { "url": "https://mcp.code4.space/mcp" }
  }
}
```

Versions released as Windsurf read `~/.codeium/windsurf/mcp_config.json` and use `serverUrl` instead of `url`:

```json
{
  "mcpServers": {
    "c4": { "serverUrl": "https://mcp.code4.space/mcp" }
  }
}
```

When the server shows **Needs auth**, click **Authenticate**.

### Zed

Add this to your Zed `settings.json`:

```json
{
  "context_servers": {
    "c4": { "url": "https://mcp.code4.space/mcp" }
  }
}
```

Zed starts the sign-in flow on its own.

### Cline

In **MCP Servers → Configure**, add this to `cline_mcp_settings.json`:

```json
{
  "mcpServers": {
    "c4": { "type": "streamableHttp", "url": "https://mcp.code4.space/mcp" }
  }
}
```

The type must be exactly `streamableHttp`. See also [llms-install.md](llms-install.md).

### Other clients

Any client that supports remote MCP servers with OAuth can connect. Most accept this configuration:

```json
{
  "mcpServers": {
    "c4": { "type": "http", "url": "https://mcp.code4.space/mcp" }
  }
}
```

## How sign-in works

- The server answers an unauthenticated request with `401` and a `WWW-Authenticate` header that points to its OAuth protected resource metadata: `https://mcp.code4.space/.well-known/oauth-protected-resource/mcp`.
- The metadata names the Code4 authorization server.
- Your client registers itself there automatically (Dynamic Client Registration), then signs you in with the authorization code flow and PKCE (S256). Requested scopes: `openid profile email offline_access`.
- You sign in with your Code4 account and approve access on the consent screen. Your client stores the tokens; the configuration never contains a key or a password.
- Personal access tokens work with the Code4 API, not with the MCP server.

## Tools

The server has more than 200 tools. Each tool has a human-readable title and MCP annotations: read-only tools carry `readOnlyHint`, and tools that change data that is hard to restore carry `destructiveHint`. The lists below are grouped by area; **read** marks a read-only tool, **write** marks a tool that changes data.

<details>
<summary><b>Issues</b> (40)</summary>

| Tool | Title | Kind |
|---|---|---|
| `list_issues` | List issues | read |
| `get_issue` | Get issue | read |
| `list_issue_statuses` | List issue statuses | read |
| `create_issue` | Create issue | write |
| `create_subtask` | Create subtask | write |
| `create_subtasks` | Create subtasks in bulk | write |
| `set_issue_parents` | Set issue parents | write |
| `list_checklist` | List issue checklist | read |
| `add_checklist` | Add checklist items | write |
| `complete_checklist_items` | Check off checklist items | write |
| `update_checklist_item` | Update checklist item | write |
| `delete_checklist_item` | Delete checklist item | write |
| `promote_checklist_item` | Turn checklist item into issue | write |
| `update_issue` | Update issue | write |
| `comment_issue` | Comment on issue | write |
| `list_issue_comments` | List issue comments | read |
| `update_issue_comment` | Edit my issue comment | write |
| `delete_issue_comment` | Delete my issue comment | write |
| `toggle_reaction` | Toggle reaction | write |
| `list_boards` | List boards | read |
| `list_issue_boards` | List boards of an issue | read |
| `add_issue_to_board` | Add issue to board | write |
| `remove_issue_from_board` | Remove issue from board | write |
| `bulk_update_issues` | Update issues in bulk | write |
| `bulk_delete_issues` | Delete issues in bulk | write |
| `delete_issue` | Delete issue | write |
| `list_deleted_issues` | List deleted issues | read |
| `restore_issue` | Restore deleted issue | write |
| `purge_issue` | Permanently erase issue | write |
| `list_project_tags` | List project tags | read |
| `move_issue` | Move issue to another project | write |
| `list_issue_code_links` | List issue code links | read |
| `link_issue_code` | Link code to issue | write |
| `unlink_issue_code` | Unlink code from issue | write |
| `list_issue_watchers` | List issue watchers | read |
| `add_issue_watcher` | Add issue watcher | write |
| `remove_issue_watcher` | Remove issue watcher | write |
| `list_description_versions` | List issue history versions | read |
| `get_description_version` | Get issue history version | read |
| `restore_description_version` | Restore issue history version | write |

</details>

<details>
<summary><b>Issue fields, statuses and boards</b> (22)</summary>

| Tool | Title | Kind |
|---|---|---|
| `list_issue_fields` | List issue fields | read |
| `create_issue_field` | Create issue field | write |
| `update_issue_field` | Update issue field | write |
| `delete_issue_field` | Delete issue field | write |
| `reorder_issue_fields` | Reorder issue fields | write |
| `add_issue_field_option` | Add issue field option | write |
| `update_issue_field_option` | Update issue field option | write |
| `delete_issue_field_option` | Delete issue field option | write |
| `reorder_issue_field_options` | Reorder issue field options | write |
| `set_issue_custom_values` | Set issue custom field values | write |
| `create_issue_status` | Create issue status | write |
| `update_issue_status` | Update issue status | write |
| `delete_issue_status` | Delete issue status | write |
| `reorder_issue_statuses` | Reorder issue statuses | write |
| `get_status_usage` | Get issue status usage | read |
| `reassign_issue_status` | Move all issues to another status | write |
| `get_board` | Get board | read |
| `create_board` | Create board | write |
| `update_board` | Update board | write |
| `set_board_columns` | Set board columns | write |
| `delete_board` | Delete board | write |
| `set_card_rank` | Reorder board card | write |

</details>

<details>
<summary><b>Sprints</b> (9)</summary>

| Tool | Title | Kind |
|---|---|---|
| `list_sprints` | List sprints | read |
| `create_sprint` | Create sprint | write |
| `update_sprint` | Update sprint | write |
| `start_sprint` | Start sprint | write |
| `complete_sprint` | Complete sprint | write |
| `delete_sprint` | Delete sprint | write |
| `add_issue_to_sprint` | Add issue to sprint | write |
| `remove_issue_from_sprint` | Remove issue from sprint | write |
| `carry_over_sprint_issues` | Carry over sprint issues | write |

</details>

<details>
<summary><b>Code review</b> (24)</summary>

| Tool | Title | Kind |
|---|---|---|
| `list_code_reviews` | List code reviews | read |
| `get_code_review` | Get code review | read |
| `get_code_review_diff` | Get full code review diff | read |
| `get_review_outline` | Get code review outline | read |
| `get_code_review_changes` | List code review changed files | read |
| `get_code_review_commits` | List code review commits | read |
| `get_code_review_message` | Get code review message | read |
| `get_code_review_messages` | List code review discussion | read |
| `get_review_patch` | Get code review patch | read |
| `get_review_merge_policy` | Check if code review can merge | read |
| `list_review_viewed_files` | List viewed review files | read |
| `list_review_issues` | List issues linked to review | read |
| `create_code_review` | Create merge request | write |
| `reply_code_review` | Reply in code review | write |
| `set_review_file_viewed` | Mark review file as viewed | write |
| `set_code_review_status` | Set code review status | write |
| `set_code_review_reviewers` | Set code review reviewers | write |
| `add_code_review_reviewer` | Add code review reviewer | write |
| `remove_code_review_reviewer` | Remove code review reviewer | write |
| `set_my_review_status` | Set my reviewer verdict | write |
| `finish_review_work` | Hand review back to reviewers | write |
| `resume_review_work` | Take review back to fix | write |
| `merge_code_review` | Merge code review | write |
| `delete_code_review` | Delete code review | write |

</details>

<details>
<summary><b>Repositories and code</b> (21)</summary>

| Tool | Title | Kind |
|---|---|---|
| `get_repository` | Get repository | read |
| `get_repository_url` | Get repository clone URL | read |
| `list_branches` | List branches | read |
| `get_branch` | Get branch | read |
| `list_refs` | List branches and tags | read |
| `list_commits` | List commits | read |
| `get_commit_diff` | Get commit diff | read |
| `get_commit_patch` | Get commit patch | read |
| `compare_refs` | Compare branches or commits | read |
| `list_repo_files` | List repository directory | read |
| `read_repo_file` | Read repository file | read |
| `search_repo_files` | Search repository files by path | read |
| `search_repo_code` | Search repository code | read |
| `find_symbol` | Find symbol definition | read |
| `list_file_commits` | List file history | read |
| `blame_repo_file` | Blame repository file | read |
| `explain_code_history` | Explain code history | read |
| `commit_repo_files` | Commit files to repository | write |
| `merge_branch` | Merge branch without review | write |
| `rebase_branch` | Rebase branch | write |
| `delete_branch` | Delete branch | write |

</details>

<details>
<summary><b>CI/CD pipelines</b> (10)</summary>

| Tool | Title | Kind |
|---|---|---|
| `list_pipelines` | List pipelines | read |
| `list_pipeline_runs` | List pipeline runs | read |
| `get_pipeline_run` | Get pipeline run | read |
| `get_step_logs` | Get pipeline step logs | read |
| `get_run_logs` | Get pipeline run logs | read |
| `get_run_tests` | Get pipeline run test results | read |
| `run_pipeline` | Run pipeline | write |
| `cancel_pipeline_run` | Cancel pipeline run | write |
| `rerun_pipeline_run` | Rerun pipeline run | write |
| `rerun_step` | Rerun pipeline step | write |

</details>

<details>
<summary><b>Environments and deployments</b> (19)</summary>

| Tool | Title | Kind |
|---|---|---|
| `list_environments` | List environments | read |
| `list_deployments` | List deployments | read |
| `get_deployment` | Get deployment | read |
| `get_deployment_changes` | Get deployment changes | read |
| `preview_deployment` | Preview deployment | read |
| `preview_rollback` | Preview service rollback | read |
| `compare_environments` | Compare environments | read |
| `get_service_declaration` | Get service declaration | read |
| `get_service_operations` | List service operations | read |
| `get_service_operation` | Get service operation | read |
| `get_service_pods` | Get service pods | read |
| `get_service_logs` | Get service logs | read |
| `deploy_service` | Deploy service | write |
| `approve_deployment` | Approve deployment | write |
| `rollback_service` | Roll back service | write |
| `restart_service` | Restart service | write |
| `scale_service` | Scale service | write |
| `promote_environment` | Promote between environments | write |
| `update_environment_config` | Replace environment config | write |

</details>

<details>
<summary><b>Packages and secrets</b> (7)</summary>

| Tool | Title | Kind |
|---|---|---|
| `list_packages` | List packages | read |
| `list_package_versions` | List package versions | read |
| `list_package_files` | List package files | read |
| `get_package_download_url` | Get package download link | read |
| `list_secrets` | List secret names | read |
| `set_secret` | Set secret | write |
| `delete_secret` | Delete secret | write |

</details>

<details>
<summary><b>Documents</b> (18)</summary>

| Tool | Title | Kind |
|---|---|---|
| `list_document_folders` | List document folders | read |
| `list_documents` | List documents | read |
| `get_document` | Get document | read |
| `list_document_revisions` | List document revisions | read |
| `get_document_revision` | Get document revision | read |
| `create_document` | Create document | write |
| `update_document` | Update document | write |
| `move_document` | Move document | write |
| `archive_document` | Archive document | write |
| `restore_document` | Restore document | write |
| `delete_document` | Delete document | write |
| `restore_document_revision` | Restore document revision | write |
| `create_document_folder` | Create document folder | write |
| `rename_document_folder` | Rename document folder | write |
| `move_document_folder` | Move document folder | write |
| `archive_document_folder` | Archive document folder | write |
| `restore_document_folder` | Restore document folder | write |
| `delete_document_folder` | Delete document folder | write |

</details>

<details>
<summary><b>Knowledge and calls</b> (7)</summary>

| Tool | Title | Kind |
|---|---|---|
| `search_knowledge` | Search team knowledge | read |
| `get_entity_context` | Get full context of an item | read |
| `get_thread` | Get conversation thread | read |
| `list_related` | List related items | read |
| `find_by_reference` | Find by key or reference | read |
| `read_call_transcript` | Read call transcript | read |
| `read_call_analysis` | Read call summary | read |

</details>

<details>
<summary><b>Projects, people, agent rules and skills</b> (21)</summary>

| Tool | Title | Kind |
|---|---|---|
| `whoami` | Get my profile | read |
| `find_people` | Find people by name | read |
| `resolve_people` | Resolve people by ID | read |
| `list_projects` | List projects | read |
| `get_project` | Get project | read |
| `list_project_members` | List project members | read |
| `list_repositories` | List repositories | read |
| `create_project` | Create project | write |
| `update_project` | Update project and members | write |
| `create_repository` | Create repository | write |
| `get_platform_guide` | Get platform guide | read |
| `get_organization_rules` | Get organization rules for agents | read |
| `get_project_rules` | Get project rules for agents | read |
| `set_organization_rules` | Set organization rules for agents | write |
| `set_project_rules` | Set project rules for agents | write |
| `list_skills` | List team skills | read |
| `get_skill` | Get team skill | read |
| `read_skill_file` | Read team skill file | read |
| `create_skill` | Create team skill | write |
| `update_skill` | Update team skill | write |
| `delete_skill` | Delete team skill | write |

</details>

<details>
<summary><b>Personal to-dos and time tracking</b> (17)</summary>

| Tool | Title | Kind |
|---|---|---|
| `list_todo` | List my to-dos | read |
| `list_todo_history` | List completed to-dos | read |
| `create_todo` | Create to-do | write |
| `update_todo` | Update to-do | write |
| `complete_todo` | Complete to-do | write |
| `reopen_todo` | Reopen to-do | write |
| `reorder_todo` | Reorder to-dos | write |
| `delete_todo` | Delete to-do | write |
| `convert_todo_to_issue` | Convert to-do to issue | write |
| `list_time_entries` | List time entries | read |
| `get_current_timer` | Get my running timer | read |
| `log_time` | Log time | write |
| `update_time_entry` | Update time entry | write |
| `delete_time_entry` | Delete time entry | write |
| `start_timer` | Start timer | write |
| `pause_timer` | Pause timer | write |
| `resume_timer` | Resume timer | write |

</details>

The live list, with full descriptions and annotations, is what your client receives from `tools/list` after sign-in.

### Example prompts

- "Show my open issues in project WEB, highest priority first."
- "Create an issue in WEB: the export button does nothing in Safari. Assign it to me."
- "Summarize merge request #128 and list the unresolved threads."
- "Find where `OrderTotal` is defined and who changed it last."
- "Why did the last pipeline run on main fail?"
- "What would change if I deployed the latest build to staging? Show the preview first."
- "What did the team decide about the release schedule? Link the sources."

## Permissions and security

**The assistant acts as you.** It signs in with your Code4 account and gets exactly your permissions. It sees the organizations, projects, documents and chats you can see, and nothing else. Knowledge search results are filtered by your permissions before the search runs.

**Tools say what they do.** Every tool carries MCP annotations:

- Read-only tools, almost half of them, are marked `readOnlyHint`.
- Tools that deploy, roll back, merge or rebase, delete, commit to a branch, run pipelines, change secrets, delete or bulk-edit issues, change a project's visibility or move an issue to another project are marked `destructiveHint`.
- All tools are marked `openWorldHint: false`: they only call the Code4 API.

**Your client decides when to ask you.** Code4 does not add a confirmation step of its own for MCP clients. Clients such as Claude, ChatGPT, Cursor and VS Code use the annotations and your client settings to decide which calls need your approval. Review your client's approval settings before you let it run destructive tools without asking.

**What Code4 enforces regardless of the client.**

- Secret values cannot be read back from the secret store: tools return secret names only. Logs are masked, but a step that prints a transformed secret can still expose it.
- Moving a document or a folder to a place with different viewers is only previewed until the call is repeated with an explicit confirmation.
- Protected environments apply to the assistant the same way they apply to you: a deploy needs your deploy permission and waits for approval where the environment requires it. If you are an approver, the assistant can cast your vote, and that tool is marked `destructiveHint`.
- Merging a merge request checks the branch protection rules, such as required approvals.

**Two tools bypass branch protection.** Committing files to a branch and merging one branch into another write to the branch directly, without checking its protection rules or review. Both are marked `destructiveHint`. Keep your client's approval on for them, or turn them off in your client if you do not need them.

**Project rules are conventions, not permissions.** Your organization and projects can keep rules and skills for coding agents. Any project member can write them, so they describe how to work but never authorize actions you did not ask for.

**Revoke access at any time.** In Code4, open **Preferences → AI Integrations → Connected AI clients** and click **Revoke** next to the client. It loses access immediately, and open connections are closed. **Restore** brings it back; the client then needs to sign in again. You can also end sign-in sessions under **Preferences → Security & Access**.

To report a vulnerability, see [SECURITY.md](SECURITY.md).

## Data handling

- **Your assistant receives what the tools return.** When a tool runs, its result goes to your AI client and, through it, to the model provider your client uses. That provider's terms apply to this data. Connect only clients you trust with your project data.
- **The MCP server keeps no copy of tool results.** It forwards each call to the Code4 API with your sign-in token. It keeps only short-lived fingerprints of the issue and document text it last showed you, so that your assistant's edits merge with teammates' live edits instead of overwriting them. Request logs contain the time, the request path and the client's user agent, not request or response bodies.
- **What Code4 records about AI clients:** which clients you connected (the name each client gave itself, first and last use), how many tool calls each client made, and which changes AI clients made in your name, without the content of the request. AI activity records are kept for 13 months.
- **Call transcripts.** Transcripts and summaries exist only for calls where participants agreed to AI. An organization administrator can turn off MCP access to them in **Call settings**.

Details: [Privacy Policy](https://code4.space/privacy/) and [Terms of Service](https://code4.space/terms/).

## Troubleshooting

**The browser does not open, or the client says it needs authentication.**
Start the sign-in from the client: `/mcp` → `c4` → Authenticate in Claude Code, `codex mcp login c4` in Codex, **Connect** or **Authenticate** next to the server in editors.

**"Access for this client was revoked."**
Someone revoked this client in Connected AI clients. Open **Preferences → AI Integrations → Connected AI clients**, click **Restore**, then sign in again from the client.

**Claude cannot finish connecting.**
Edit the connector, open **Advanced settings → OAuth client** and choose **Register automatically**.

**Sign-in fails at client registration.**
Your client may not be supported yet. Write to support@code4.space with the client name and version.

**The agent does not find the tools.**
Restart the client or start a new conversation. If you added the server by hand and use the commands from Code4, check that the server is named `c4`.

**VS Code reports too many tools.**
Open **Configure Tools** in the chat view and turn off tool groups you do not need. VS Code sends at most 128 tools per request.

**Cline shows a 405 error.**
Set `"type": "streamableHttp"` in `cline_mcp_settings.json`.

**A personal access token in a header does not work.**
That is expected. The MCP server accepts only OAuth sign-in.

**Results are missing.**
The assistant sees only what your account can see. Check that you are a member of the project, and name the organization if you belong to several.

## Support

Email [support@code4.space](mailto:support@code4.space) or use the [contact page](https://code4.space/contact/). Include your client name and version and the time of the problem. Never send your password or tokens.

## Files in this repository

| File | Used by |
|---|---|
| `server.json` | [MCP Registry](https://registry.modelcontextprotocol.io) entry `space.code4/mcp` |
| `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`, `.mcp.json` | Claude Code plugin and plugin marketplace |
| `plugin.json`, `mcp.json` | [Agent Plugins](https://agent-plugins.org) package for ChatGPT, Codex and Cursor |
| `gemini-extension.json`, `GEMINI.md` | Gemini CLI extension |
| `llms-install.md` | Install notes for Cline and other agents that set up servers themselves |
| `icons/` | Code4 icons in SVG and PNG |

This repository contains configuration and documentation only. The files are under the [MIT License](LICENSE). Code4 and the Code4 logo belong to Code4 Space, Inc.
