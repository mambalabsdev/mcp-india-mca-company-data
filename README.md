# India MCA Company Data MCP Server

[![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-india-mca-company-data)](https://www.npmjs.com/package/@mambalabsdev/mcp-india-mca-company-data) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-india-mca-company-data)](https://github.com/mambalabsdev/mcp-india-mca-company-data/blob/main/LICENSE)

An MCP server for the Mamba Labs India MCA Company Data actor on Apify. Indian company records as rows.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Takes CINs, LLPINs, ZaubaCorp URLs, or company names and returns one row per Indian company or LLP with MCA status, ROC, category, class, incorporation date, capital, registered address, registered email, other names, and current directors with DIN and appointment date.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-india-mca-company-data": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-india-mca-company-data"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `get_india_company_data` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Look up the directors and paid-up capital of CIN L85110KA1981PLC013115."
- "Find the MCA record for Razorpay Software and list its current directors."

## Tool

`get_india_company_data`. One tool. Example arguments:

```json
{
  "companies": [
    "L85110KA1981PLC013115"
  ]
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `companies` | array | no | One entry per company: a CIN (L85110KA1981PLC013115), an LLPIN (AAA-1234), a ZaubaCorp company URL, or a company name. A name is searched on ZaubaCorp and the top matches are read. From Clay, put the column inside a one item list. |
| `name_matches` | number | no | For a company name: how many search results to read, from 1 (default) to 10. Each company read is one company row. |
| `max_charge_usd` | number | no | Optional. The run stops before a charge that would pass this amount. Summary rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `company-row`, one company read | $0.006 | $0.0057 | $0.0054 | $0.0051 |
| `apify-actor-start`, per run start | $0.004 | $0.004 | $0.004 | $0.004 |

Repeats, missing companies, blocked pages, search summaries, and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/india-mca-company-data](https://apify.com/mambalabs/india-mca-company-data)

## License

MIT. See [LICENSE](LICENSE).
