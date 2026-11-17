<p align="center">
  <a href="https://zuperbase.co/ai-apps">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="assets/zuperbase-logo-white.svg">
      <img src="assets/zuperbase-logo.svg" alt="Zuperbase" height="44">
    </picture>
  </a>
</p>

<h3 align="center">Run your business from Claude, ChatGPT or any MCP app</h3>

<p align="center">
  The Zuperbase connector and skill. Ask your AI app about the business, and let it do the routine work:
  set-up, bills, invoices, bank lines and month-end, with the access you choose.
</p>

<p align="center">
  <a href="#connect-in-a-minute"><b>Connect</b></a> ·
  <a href="docs/tools.md">Tools</a> ·
  <a href="docs/prompts.md">Prompts</a> ·
  <a href="docs/access-levels.md">Access levels</a> ·
  <a href="docs/security-and-privacy.md">Security</a> ·
  <a href="https://zuperbase.co/ai-apps">Website</a>
</p>

<p align="center">
  <img alt="MCP: streamable HTTP" src="https://img.shields.io/badge/MCP-streamable%20HTTP-00bf63">
  <img alt="Sign-in: OAuth 2.1" src="https://img.shields.io/badge/sign--in-OAuth%202.1%20%2B%20PKCE-272b2c">
  <img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-272b2c">
</p>

---

[Zuperbase](https://zuperbase.co) is one workspace to run a business: sales, purchases, banking, tax and the books,
with your team and your accountant in the same place. This repository connects it to the AI app you already use.

```text
You:        Enter this bill from Sharma Logistics.            📎 bill-0412.pdf
AI app:     Saved a draft bill SL/0412 for Sharma Logistics: freight 18,000, GST under
            reverse charge. Zuperbase's total matches the bill, and the PDF is kept with it.
            Review it: https://books.zuperbase.co/purchases/bills/…
You:        Post it.
AI app:     Posted. It is in the audit log with this app's name.
```

## What it does

| | |
|---|---|
| **Set up the business** | A one-question-at-a-time interview fills in the business profile, tax registration, bank accounts, invoice numbering and what you sell. |
| **Bills from a photo** | Reads the vendor's bill, finds the vendor, picks accounts and tax (India: GST source of supply, reverse charge, blocked credit), keeps the file with the bill and checks Zuperbase's total against the paper. |
| **Invoices in a sentence** | Drafts the invoice from your items, rates and tax rates, ready to send from Zuperbase. |
| **Bank lines** | Matches statement lines that clearly belong to an entry, categorises bank charges and interest, and asks you about the rest. |
| **Questions** | Profit and loss, balance sheet, who owes you and how overdue, why an account has its balance, every payment to a vendor. |
| **Month-end** | Runs the month-end checklist and the books health check, explains the month and lists what needs a look. |

Everything it makes is saved in your workspace. Zuperbase works out the tax and the totals, refuses an entry that
does not balance or falls in a locked period, and records every action with the app's name.

## Connect in a minute

The connector address is:

```text
https://mcp.zuperbase.co/mcp
```

| App | How |
|---|---|
| **Claude Code** | Install the plugin below, or run `claude mcp add --transport http zuperbase https://mcp.zuperbase.co/mcp` |
| **Claude** (web and desktop) | Settings › Connectors › Add custom connector. [Steps](docs/connect/claude.md) |
| **ChatGPT** | Settings › Apps & Connectors › developer mode › create a connector. [Steps](docs/connect/chatgpt.md) |
| **Cursor, VS Code and others** | Add an HTTP MCP server with the address. [Steps](docs/connect/other-apps.md) |

Each app opens Zuperbase in your browser. You sign in there (the AI app never sees your password), choose the
organisation and what the app may do, and allow it.

### Claude Code plugin (connector and skill together)

```text
/plugin marketplace add zuperbase/zuperbase-mcp
/plugin install zuperbase@zuperbase
```

Then type `/mcp`, choose **zuperbase** and sign in. The plugin adds the connector and the
[Zuperbase skill](plugins/zuperbase/skills/zuperbase/SKILL.md), which teaches Claude how to work in Zuperbase:
the set-up interview, entering bills, drafting invoices and journals, bank lines and month-end.

Other apps get the same rules from the connector itself, and its [prompts](docs/prompts.md) appear as ready-made
commands where the app supports MCP prompts.

## You stay in control

| Level | What the app may do |
|---|---|
| **Read only** | Reports, statements and search. Changes nothing. |
| **Prepare drafts** *(default)* | Also draft invoices, bills and journals, add customers, vendors and items, keep source documents. Nothing posts. |
| **Bookkeeper** | Also post invoices, bills and journals and match bank lines, up to a limit per document. Chosen by an owner or admin. |

- An app can never do more than the person who connected it, and only in the areas they allowed.
- Owners and admins can connect AI apps; anyone else only when an owner allows them.
- One switch turns AI apps off for the whole organisation. Change or disconnect any app at any time.
- **At no level** can an AI app make a payment, file a return, void a document, close a period, change users or
  export data. A person does those in Zuperbase.

More in [access levels](docs/access-levels.md) and [security and privacy](docs/security-and-privacy.md).

## Try asking

- *Help me set up my business in Zuperbase.*
- *How much profit did we make last quarter, and what drove it?*
- *Who owes us money, and how long overdue is each one?*
- *Go through the unmatched bank lines and match the obvious ones.*
- *Run the month-end checklist for October and list what is open.*

## For builders

| | |
|---|---|
| Address | `https://mcp.zuperbase.co/mcp` |
| Transport | Streamable HTTP, JSON responses |
| Sign-in | OAuth 2.1, PKCE (S256), dynamic client registration; discovery at `/.well-known/oauth-protected-resource` |
| Tools | [docs/tools.md](docs/tools.md); `tools/list` shows only what a connection may use |
| Prompts | [docs/prompts.md](docs/prompts.md) |

## In this repository

```text
.claude-plugin/marketplace.json        the Claude Code plugin marketplace
plugins/zuperbase/                     the plugin: connector address and the Zuperbase skill
docs/                                  setup for each app, tools, prompts, access levels, security
```

The connector itself runs at Zuperbase; this repository holds what you install in your AI app. The tool and
prompt lists in `docs/` are generated from the running connector's code, so they match what you get.

## Good to know

AI apps can make mistakes. Read what they prepare before you approve it. Nothing an AI app says is tax or legal
advice; ask your accountant about judgement calls. What an app reads from your workspace is sent to that app's
provider and handled under the provider's terms.

## Support

Questions and bug reports: [open an issue](../../issues) or write to support@zuperbase.co.
Security issues: see [SECURITY.md](SECURITY.md).

Zuperbase is a product of TrueAxis Private Limited. The contents of this repository are under the [MIT licence](LICENSE).
