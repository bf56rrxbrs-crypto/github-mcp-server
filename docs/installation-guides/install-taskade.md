# Install GitHub MCP Server in Taskade

## Prerequisites

1. [Taskade](https://taskade.com/) account with AI Agent access
2. [GitHub Personal Access Token](https://github.com/settings/personal-access-tokens/new) with appropriate scopes
3. For local installation: [Docker](https://www.docker.com/) installed and running

## Remote Server Setup (Recommended)

Uses GitHub's hosted server at `https://api.githubcopilot.com/mcp/`. Taskade supports connecting to external MCP servers via its AI Agent tools configuration.

### Install steps

1. Open Taskade and go to the **Agents** tab
2. Select an existing agent or create a new one
3. Edit the agent and navigate to the **Tools** tab
4. Click **Add** to add a new MCP tool
5. Select **MCP** as the tool type and configure with the JSON below
6. Replace `YOUR_GITHUB_PAT` with your actual [GitHub Personal Access Token](https://github.com/settings/tokens)
7. Save the agent configuration

### Streamable HTTP Configuration

```json
{
  "mcpServers": {
    "github": {
      "url": "https://api.githubcopilot.com/mcp/",
      "headers": {
        "Authorization": "Bearer YOUR_GITHUB_PAT"
      }
    }
  }
}
```

## Local Server Setup

### Docker Installation

**Important**: The npm package `@modelcontextprotocol/server-github` is no longer supported as of April 2025. Use the official Docker image `ghcr.io/github/github-mcp-server` instead.

```json
{
  "mcpServers": {
    "github": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "GITHUB_PERSONAL_ACCESS_TOKEN",
        "ghcr.io/github/github-mcp-server"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "YOUR_GITHUB_PAT"
      }
    }
  }
}
```

## Verify Installation

1. Open the agent's **Tools** tab and confirm the GitHub MCP server is listed
2. Start a conversation with the agent
3. Test with: "List my GitHub repositories"
4. Verify the agent can access GitHub tools

## Troubleshooting

### Remote Server Issues

- **Authentication failures**: Verify your PAT has the correct scopes and hasn't expired
- **Connection errors**: Check firewall/proxy settings for HTTPS connections

### Local Server Issues

- **Docker errors**: Ensure Docker Desktop is running
- **Image pull failures**: Try `docker logout ghcr.io` then retry
- **Docker not found**: Install Docker Desktop and ensure it's running

### General Issues

- **Tools not appearing**: Re-save the agent configuration and refresh
- **Check logs**: Look for MCP-related errors in the Taskade agent's activity log
- **Tool limits**: Taskade recommends keeping total enabled tools under a reasonable limit for optimal performance

## Important Notes

- **Official repository**: [github/github-mcp-server](https://github.com/github/github-mcp-server)
- **Remote server URL**: `https://api.githubcopilot.com/mcp/`
- **Docker image**: `ghcr.io/github/github-mcp-server` (official and supported)
- **npm package**: `@modelcontextprotocol/server-github` (deprecated as of April 2025 - no longer functional)
- **Taskade docs**: Refer to [Taskade Help Center](https://help.taskade.com/en/articles/9314171-tools-for-ai-agents) for the latest agent tools configuration details
