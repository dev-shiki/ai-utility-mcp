# AI & Developer Utility Suite — Hosted MCP & n8n Workflows

[![MCP](https://img.shields.io/badge/MCP-Streamable%20HTTP%20%2B%20x402-7C3AED?style=flat-square)](https://mcp-utility-suite.nandaleoardana.workers.dev/mcp)
[![Cloudflare Workers](https://img.shields.io/badge/Edge-Cloudflare%20Workers-F38020?style=flat-square)](https://mcp-utility-suite.nandaleoardana.workers.dev/health)

Zero-dependency edge utility tools for **AI Agents, n8n Automations, and Developer Pipelines** — hosted remotely via Streamable HTTP MCP with **`x402` Pay-Per-Call (USDC on Base)** or API Key authentication.

## Included Tools

| Tool | Purpose |
|---|---|
| `validate_email` | Validate syntax, disposable/role domains, typo suggestions, and risk score |
| `heal_json` | Repair malformed LLM/JSON output (trailing commas, unquoted keys, markdown fences) |
| `redact_pii` | Detect and redact emails, phones, SSNs, credit cards, and API keys |
| `parse_user_agent` | Detect bots, crawlers, AI scrapers, browser, OS, and device type |
| `generate_svg_qr` | Generate clean vector SVG QR codes for URLs and text |

---

## 1. Hosted MCP Configuration

Connect via [`mcp_config.json`](./mcp_config.json):

```json
{
  "mcpServers": {
    "ai-utility-suite": {
      "url": "https://mcp-utility-suite.nandaleoardana.workers.dev/mcp",
      "headers": {
        "Authorization": "Bearer ${MCP_API_KEY}"
      }
    }
  }
}
```

- **Free Discovery**: `initialize` and `tools/list` are open without authentication.
- **AI Agent Pay-Per-Call (`x402`)**: Calling `tools/call` without an API key or `X-PAYMENT` header returns `402 Payment Required` (`$0.002` USDC on Base).
- **RapidAPI REST Subscriptions**: All APIs are also available via [RapidAPI Provider Portfolio](https://rapidapi.com/user/shikiv-ZkrHCuwAa).

---

## 2. Free n8n Workflow Templates

Ready-to-import workflows (each includes **Sticky Notes** and an **Error Trigger**):

- [`n8n/ai-output-sanitizer.workflow.json`](./n8n/ai-output-sanitizer.workflow.json) — Chain `json-heal` -> `pii-shield` to repair & sanitize LLM outputs before saving to your DB/CRM.
- [`n8n/signup-spam-guard.workflow.json`](./n8n/signup-spam-guard.workflow.json) — Chain `email-guard` + `ua-bot-intel` to block disposable emails & bot signups.
