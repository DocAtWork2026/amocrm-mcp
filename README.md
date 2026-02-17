# amoCRM MCP Server

MCP (Model Context Protocol) server for amoCRM integration with Claude Desktop and other AI assistants.

## Features

- **Leads** -- list, get, create, update
- **Contacts** -- list, get, create
- **Companies** -- list, get, create
- **Tasks** -- list, create
- **Pipelines** -- list pipelines and stages
- **Users** -- list account users
- **Notes** -- add and read notes on any entity
- **Account** -- get account info

## Prerequisites

- Python 3.10+
- amoCRM account with API access
- Long-lived token from amoCRM integration settings

## Installation

```bash
git clone https://github.com/DocAtWork2026/amocrm-mcp.git
cd amocrm-mcp
pip install -r requirements.txt
```

## Configuration

1. Copy `.env.example` to `.env` and fill in your credentials:

```bash
cp .env.example .env
```

```env
AMOCRM_DOMAIN=your_subdomain
AMOCRM_TOKEN=your_long_lived_token
```

- `AMOCRM_DOMAIN` -- your amoCRM subdomain (e.g. if your URL is `https://mycompany.amocrm.ru`, the domain is `mycompany`)
- `AMOCRM_TOKEN` -- long-lived API token from your amoCRM integration settings

### Getting the token

1. Go to amoCRM Settings -> amoMarket
2. Click the three dots menu -> Create integration
3. Choose "External integration", set name and redirect URI (`https://localhost`)
4. Save, then install the integration
5. Open the integration -> "Keys and access" tab
6. Click "Generate token" under "Long-lived token"
7. Copy the token

## Claude Desktop Setup

Add this to your `claude_desktop_config.json`:

**macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "amocrm": {
      "command": "python",
      "args": ["C:/path/to/amocrm-mcp/server.py"],
      "env": {
        "AMOCRM_DOMAIN": "your_subdomain",
        "AMOCRM_TOKEN": "your_long_lived_token"
      }
    }
  }
}
```

Restart Claude Desktop after updating the config.

## Available Tools

| Tool | Description |
|------|-------------|
| `get_account_info` | Get amoCRM account info |
| `get_leads` | List leads (with search) |
| `get_lead` | Get lead details by ID |
| `create_lead` | Create a new lead |
| `update_lead` | Update an existing lead |
| `get_contacts` | List contacts (with search) |
| `get_contact` | Get contact details by ID |
| `create_contact` | Create a new contact |
| `get_companies` | List companies (with search) |
| `get_company` | Get company details by ID |
| `create_company` | Create a new company |
| `get_tasks` | List tasks |
| `create_task` | Create a new task |
| `get_pipelines` | List pipelines and stages |
| `get_users` | List account users |
| `add_note` | Add a note to an entity |
| `get_notes` | Get notes for an entity |

## License

MIT
