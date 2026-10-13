# ResumeQuick MCP Server

Remote MCP server for [ResumeQuick](https://resumequick.app), a job-search companion. It gives Claude, ChatGPT, Codex, Cursor and any remote MCP client your real job-search context: your resumes and their history, the jobs you track and their fit analyses, the matches your job radar finds, mock interview results, offers, reminders and career memory. The client reads what is already there instead of asking you to retype it, and can act on it: edit or translate a resume, analyze a posting, tune the job search, export a PDF.

- **Endpoint:** `https://mcp.resumequick.app/mcp`
- **Transport:** streamable HTTP
- **Auth:** OAuth sign-in with your ResumeQuick account; a personal API key for clients without a browser
- **Registry:** `app.resumequick/resumequick` in the [official MCP Registry](https://registry.modelcontextprotocol.io)
- **Claude:** [ResumeQuick in Claude's connector directory](https://claude.ai/directory/connectors/resumequick)
- **Price:** included on every ResumeQuick plan, the free one too

This repository holds documentation and the registry manifest. The server is hosted by ResumeQuick; there is nothing to install or run.

## Connect

Add `https://mcp.resumequick.app/mcp` as a remote MCP server in your client and keep sign-in on. The client opens a ResumeQuick page: you sign in (or create a free account on the spot) and allow access. Your password never reaches the client.

For example, Claude Code:

```bash
claude mcp add --transport http resumequick https://mcp.resumequick.app/mcp
```

Step-by-step guides for each client live on the site and stay current there: **[resumequick.app/en/integrations](https://resumequick.app/en/integrations)** — Claude, ChatGPT, Codex, Cursor, OpenCode.

### Install from this repository

This repository is also a plugin or extension for clients that install from Git:

- **Cursor:** a Cursor plugin (`.cursor-plugin/plugin.json` and `mcp.json`). The `auth` block with `"CLIENT_ID": "cursor"` lets Cursor sign in.
- **Gemini CLI:** `gemini extensions install https://github.com/resumequick/resumequick-mcp`, then `/mcp auth resumequick` to sign in.
- **Cline and other agents:** setup steps for an agent to follow are in [`llms-install.md`](llms-install.md).

Scripts and clients that can't open a sign-in page use a personal API key from your ResumeQuick settings, sent as `Authorization: Bearer <key>`.

## What it can do

The client sees the full list of tools with descriptions once connected. They cover:

- **Resumes** — read, edit, rewrite from an instruction, translate, style, check against ATS, export to PDF, restore an earlier version.
- **Job tracker** — analyze a posting against your resume, tailor the resume to it, write a cover letter, track status and notes.
- **Job radar** — read and sort the matches it found, analyze one, change what and where it searches.
- **Interviews and offers** — mock interview results, offer analysis with negotiation scripts.
- **Career memory and reminders** — what the agent should remember about you, and when to nudge you.
- **Next step** — the one step worth taking now, the same one the app and its career agent suggest.

Read tools only fetch data. Write tools change only your own data, and a tool says so in its description when an action uses a plan limit.

## Try it

- "Read my resume and tell me the one thing to fix before I apply to this posting: …"
- "What did my job radar find this week? Analyze the best match."
- "Translate my resume into German as a separate copy."
- "Remind me on Friday to follow up with Acme."

## Data and security

- Every tool works on the account that signed in or owns the key. No tool takes a user id.
- Tokens and keys travel only in the `Authorization` header, never in a URL.
- Disconnect a client or revoke a key in your ResumeQuick settings at any time.

## Links

- Setup guides: [resumequick.app/en/integrations](https://resumequick.app/en/integrations)
- Product: [resumequick.app](https://resumequick.app)
- Support: hello@resumequick.app
