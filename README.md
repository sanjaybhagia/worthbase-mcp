<p align="center"><img src="assets/logo-400.png" width="120" alt="Worthbase"></p>

# Worthbase MCP server

**Your household's net worth in any AI assistant.** Connect [Worthbase](https://worthbase.app) to
Claude, ChatGPT, Cursor, Raycast or any app that speaks the
[Model Context Protocol](https://modelcontextprotocol.io), and keep everything your household owns
and owes: shares and ETFs, crypto, gold and silver, retirement accounts, property, cash and loans,
in any currency and owned by people, trusts or companies. Hand your AI a broker export or a
statement to record, and ask what you're worth, how your investments did, or what selling would
make.

```
https://worthbase.app/mcp
```

A hosted, remote server (Streamable HTTP). There's nothing to install and no API key: the first
time a tool is used you sign in to your own Worthbase account in the browser and approve the
connection.

> This repository holds connection instructions and configuration only. The Worthbase service and
> its server code are not here.

## Try asking

- "What's our net worth, and how has it changed this year?"
- "Here's my broker's transaction export. Import it, owned 100% by me, and show me the preview first."
- "How did my shares do over the last three years, as an annual return?"
- "What would selling half my ETF holding make, and which lots would it use?"
- "Which of our values are out of date?"
- "Show my Worthbase dashboard."

Every write is previewed first and saved only when you approve it. Every change is audited and can
be undone. Worthbase calculates every figure with exact decimals, and your AI quotes them rather
than doing the maths itself.

## Connect it

| App | How |
|---|---|
| **ChatGPT** | Listed in ChatGPT's plugin directory: [install the Worthbase plugin](https://chatgpt.com/plugins/plugin_asdk_app_6abee604237481919b53866c9a04d644), or search for Worthbase under Plugins. |
| **Claude** | Settings → Connectors → **Add custom connector**, named Worthbase, with the URL above. Works on the web, desktop and mobile. |
| **Claude Code** | `claude mcp add --transport http worthbase https://worthbase.app/mcp`, then `/mcp` → worthbase → Authenticate. |
| **Cursor** | Settings → MCP → Add new MCP server, or add `mcp.json` from this repo to `~/.cursor/mcp.json`. |
| **VS Code** | Command palette → *MCP: Add Server* → HTTP → `https://worthbase.app/mcp` |
| **Gemini CLI** | `gemini extensions install https://github.com/sanjaybhagia/worthbase-mcp` |
| **Raycast** | In the *Model Context Protocol Registry* extension, under official servers. |
| **Anything else** | Point it at `https://worthbase.app/mcp`; for stdio-only apps use `npx -y mcp-remote https://worthbase.app/mcp` (see [llms-install.md](llms-install.md)). |

Step-by-step guides for each app: **[worthbase.app/setup](https://worthbase.app/setup/)**.

## Tools

Reading:

| Tool | What it returns |
|---|---|
| `whoami` | The signed-in user, their workspaces and roles, and invites waiting for them. |
| `get_overview` | Parties, accounts, the net worth headline, stale items, reconciliation mismatches and recent batches. |
| `get_net_worth` | Assets, liabilities and net worth on a date, by class, party, account or item. |
| `get_history` | Net worth at each month, quarter or year end, with the change over the period. |
| `list_items` | Assets and liabilities with owners and current position: units, price, value, cost base, unrealised gain. |
| `get_item` | One item in full: position, owners, transactions, valuations, open lots and reconciliations. |
| `get_performance` | Money in and out, income, gain, simple return and annual return (XIRR), per item and in total. |
| `get_debt_report` | Every loan with balance, security and offsets, and each property's equity and loan-to-value. |
| `get_goals` | Goals with progress, trend, projected date and whether they're on pace. |
| `get_losses` | Tracked losses carried forward, per party. |
| `simulate_sale` | What selling a holding or property would do: proceeds, lots used, gain or loss per party. Never writes. |
| `list_batches` | Recent writes, with source document and status, for review or undo. |
| `search_instruments` | Find a listed security or crypto coin by name or code. |

Writing (previewed, audited and undoable):

| Tool | What it does |
|---|---|
| `record` | The main write: accounts, items, transactions, transfers, valuations, prices and reconciliation checks. Previews by default. |
| `commit` | Saves a previewed batch. |
| `undo` | Reverses a committed batch; refuses if the ledger would become inconsistent. |
| `show_dashboard` | Net worth at a glance as an interactive dashboard (Claude and ChatGPT render it). |
| `update_values` | A form for new values of property, super, cash and loans. |
| `reconcile` | Checks a statement figure against the calculated one and records match or mismatch. |
| `update_item`, `set_owners`, `link_items`, `archive_item`, `void` | Correct an item, its ownership split, its links (loan to property, offset to loan), or remove records. |
| `set_goal`, `set_loss` | Net worth and debt goals; tracked losses. |
| `refresh_prices` | Fetches the latest prices in the background. Prices also refresh daily. |
| `save_workspace`, `save_party`, `save_account` | Workspaces, owners (individuals, companies, trusts, SMSFs, partnerships) and accounts. |

Every tool has annotations (read-only or destructive). Worthbase has no bank or broker logins, never
moves money or places trades, doesn't calculate tax, and isn't financial advice.

## Plans

One plan: US$3.99 a month with a 7-day free trial, or US$49 once for lifetime access. Every party
type and any number of workspaces. Invited household members join free. See
[worthbase.app/pricing](https://worthbase.app/pricing/).

## Auth details

- OAuth 2.1, PKCE (S256), public clients, through Clerk (`https://clerk.worthbase.app`)
- Client ID metadata documents and dynamic client registration
- Discovery: `https://worthbase.app/.well-known/oauth-protected-resource/mcp`, from the 401 an
  unauthenticated request returns
- Official MCP Registry name: `app.worthbase/worthbase` ([server.json](server.json))

## Links

[worthbase.app](https://worthbase.app) · [Setup guide](https://worthbase.app/setup/) ·
[Developers](https://worthbase.app/developers/) · [Security](https://worthbase.app/security/) ·
[Privacy](https://worthbase.app/privacy/) · [Terms](https://worthbase.app/terms/) ·
support@worthbase.app

Made in Sydney by Arigato Consulting Pty Ltd. The files in this repository are MIT licensed; see
[LICENSE](LICENSE).
