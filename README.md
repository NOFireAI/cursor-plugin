# NOFire AI — Cursor Plugin

**AI for Prevention.** See what breaks before it does. Prevent change-driven incidents. Stop repeating failures.

## What This Plugin Does

NOFire AI brings production context into your IDE. Before you merge, you know the risk. While you code, you know what's happening in production. When onboarding, you understand the architecture.

**No dashboards. No context switching. Code with production context.**

### Capabilities

| Capability | What it does |
|-----------|-------------|
| **Deployment Risk** | Score risk before you deploy. Get the right rollout strategy. |
| **Blast Radius** | See which services cascade if something fails. |
| **Change Timeline** | What changed, when, and where — infra + code. |
| **Past Failures** | Has this service failed before? What was the root cause? |
| **Service Discovery** | What runs in production, how it connects, what depends on what. |
| **Cluster Overview** | Cluster-wide health when you don't know where to start. |

## Setup

### 1. Get an API token

Generate an MCP token from your [NOFire AI dashboard](https://my.nofire.ai/dashboard/api-keys).

### 2. Set the environment variable

```bash
export NOFIRE_API_TOKEN="your-token-here"
```

Or add it to your shell profile (`~/.zshrc`, `~/.bashrc`).

### 3. Install the plugin

Install from the [Cursor Marketplace](https://cursor.com/marketplace) or add manually:

**Via Marketplace:** Search "NOFire" in Cursor's plugin panel.

**Via MCP config** (if not using the plugin): Add to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "NOFireAI": {
      "url": "https://mcp.nofire.ai/mcp",
      "headers": {
        "Authorization": "Bearer ${NOFIRE_API_TOKEN}"
      }
    }
  }
}
```

### 4. Restart Cursor

Fully quit and restart Cursor. A window reload is not enough.

## What's Included

| Component | Description |
|-----------|-------------|
| **MCP Server** | Remote connection to NOFire AI — no local install needed |
| **Rules** | Always-on guidance for prevention-first development |
| **Skills** | Guided workflows: deployment risk, production context, service discovery |

## Try It

```
What's the deployment risk for payment-service?
```

```
What changed in payment-service in the last 24 hours?
```

```
Has checkout-service failed before? What was the root cause?
```

```
Show me the dependencies of api-gateway
```

## Prerequisites

- [NOFire AI account](https://nofire.ai) with connected infrastructure
- NOFire AI Edge agent deployed or observability tools connected
- MCP API token from dashboard

## Security

MCP tokens are **read-only**. They cannot modify infrastructure, trigger deployments, or execute commands.

## Links

- [Documentation](https://docs.nofire.ai/mcp/getting-started)
- [API Token Guide](https://docs.nofire.ai/mcp/api-keys)
- [NOFire AI](https://nofire.ai)
