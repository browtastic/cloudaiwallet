# CloudAIWallet MCP Servers

Agentic cloud wallet infrastructure with MCP-native access. Connect any AI agent to manage wallets, query transactions, and access platform data.

## Quick Start

Add to your OpenClaw, Claude Desktop, or Cursor config:

```json
{
  "mcpServers": {
    "cloudaiwallet-graph": {
      "url": "https://mcp.cloudaiwallet.com/sse",
      "transport": "sse"
    },
    "cloudaiwallet-database": {
      "url": "https://db.cloudaiwallet.com/sse",
      "transport": "sse"
    },
    "cloudaiwallet-storage": {
      "url": "https://fs.cloudaiwallet.com/sse",
      "transport": "sse"
    }
  }
}
```

Or use the unified Agent Bridge:

```json
{
  "mcpServers": {
    "cloudaiwallet": {
      "url": "https://agent.cloudaiwallet.com/sse",
      "transport": "sse"
    }
  }
}
```

## MCP Servers

| Server | Endpoint | Backend | Tools |
|---|---|---|---|
| Graph API | `mcp.cloudaiwallet.com/sse` | Neo4j | `read_neo4j_cypher`, `write_neo4j_cypher`, `get_neo4j_schema`, `report_finding` |
| Database API | `db.cloudaiwallet.com/sse` | SQLite | `execute_sql`, `list_tables`, `describe_table`, `report_finding` |
| Storage API | `fs.cloudaiwallet.com/sse` | Filesystem | `read_file`, `write_file`, `list_directory`, `search_files`, `report_finding` |
| Agent Bridge | `agent.cloudaiwallet.com/sse` | All | `query_wallets`, `query_transactions`, `access_files`, `list_files`, `report_finding` |

## Architecture

```
Your AI Agent (Claude, GPT, Cursor, OpenClaw)
    │
    ▼ MCP SSE
agent.cloudaiwallet.com ← Agent Bridge (unified access)
    │
    ├── mcp.cloudaiwallet.com  → Neo4j Graph (users, wallets, keys, seeds)
    ├── db.cloudaiwallet.com   → SQLite DB (transactions, config, API keys)
    └── fs.cloudaiwallet.com   → Filesystem (configs, credentials, backups)
```

## Features

- **No authentication required** — connect and start querying
- **SSE transport** — standard MCP protocol over Server-Sent Events
- **14 MCP tools** across 4 servers
- **MCP Prompts** — `security_audit` and `data_review` pre-built workflows
- **Reasoning capture** — every tool call can include WHY you're making it
- **OpenClaw integration** — AI assistant dashboard at `openclaw.cloudaiwallet.com`

## Data Available

- User profiles with roles and API keys
- Wallet addresses (ETH/BTC) with balances
- Trading bot configurations
- Transaction history
- System configuration and secrets
- AWS credentials and SSH keys
- Platform .env file

## AI Assistant

Chat with the CloudAIWallet AI assistant at [openclaw.cloudaiwallet.com](https://openclaw.cloudaiwallet.com)

## License

MIT
