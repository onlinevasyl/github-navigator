# Setup & Deployment Guide

## Table of Contents
- [Prerequisites](#prerequisites)
- [MCP Server Setup](#mcp-server-setup)
- [Copilot Studio Configuration](#copilot-studio-configuration)
- [Testing & Validation](#testing--validation)
- [Troubleshooting](#troubleshooting)

## Prerequisites

### Required
- GitHub account with API access
- GitHub Personal Access Token (PAT) with `repo` scope
- Microsoft Copilot Studio access
- Microsoft 365 subscription (for Teams/M365 Copilot deployment)

### GitHub PAT Setup
1. Go to [GitHub Settings → Developer Settings → Personal Access Tokens](https://github.com/settings/tokens)
2. Click "Generate new token (classic)"
3. Select scopes:
   - `repo` (full control of private repositories)
   - `read:org` (read organization data)
   - `read:user` (read user profile)
4. Save the token securely (you won't see it again)

## MCP Server Setup

### Option 1: Using Pre-built MCP Server (Recommended)

The GitHub MCP Server is maintained by [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers).

**Installation:**
```bash
pip install github-mcp-server
```

**Configuration:**
Create a config file `~/.mcp/github-config.json`:
```json
{
  "github_token": "your_github_pat_here",
  "timeout": 30,
  "cache_enabled": true
}
```

**Start the server:**
```bash
mcp-run-github --config ~/.mcp/github-config.json
```

### Option 2: Manual MCP Server Setup

Clone and configure the GitHub MCP Server:
```bash
git clone https://github.com/modelcontextprotocol/servers.git
cd servers/src/github
npm install
npm start
```

Set environment variables:
```bash
export GITHUB_TOKEN=your_github_pat_here
export MCP_PORT=3000
```

## Copilot Studio Configuration

### Step 1: Create New Agent
1. Open [Microsoft Copilot Studio](https://copilotstudio.microsoft.com/)
2. Click "Create" → "New Agent"
3. Name: "GitHub Navigator"
4. Description: "MCP-powered DevOps assistant for GitHub navigation"

### Step 2: Add MCP Connector
1. In Copilot Studio, go to "Actions" → "MCP Connectors"
2. Click "New Connector"
3. Configure:
   - **Name:** GitHub MCP Server
   - **Endpoint:** `http://localhost:3000` (or your MCP server URL)
   - **Auth Type:** Bearer Token
   - **Token:** `your_github_pat_here`
4. Test the connection
5. Save

### Step 3: Import Agent Instructions
1. Go to "Agent Instructions" tab
2. Copy-paste the content from [agent-instructions.md](./agent-instructions.md)
3. Adjust instructions for your specific use cases
4. Save

### Step 4: Configure Available Tools
In the MCP Connector setup, enable these tools:
- `search_repositories` - Search GitHub repositories
- `search_code` - Search code across repositories
- `get_repository` - Retrieve repository information
- `list_commits` - Get commit history
- `list_issues` - Retrieve issues
- `list_pull_requests` - Get pull requests
- `get_file_content` - Read file contents
- `search_commits` - Search commit history

## Testing & Validation

### Unit Testing
Create a test file to validate MCP server responses:
```bash
curl -X POST http://localhost:3000/tools/search_repositories \
  -H "Authorization: Bearer $GITHUB_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"query": "github-navigator", "limit": 5}'
```

### Agent Testing in Copilot Studio
Test these scenarios:
1. **Basic Search:** "Find repositories named 'github-navigator'"
2. **Cross-Repo Search:** "Search for function 'getUserData' across repos"
3. **Issue Tracking:** "Show all open issues in onlinevasyl/github-navigator"
4. **Commit Analysis:** "What was changed in the latest commit?"

### Deployment Testing
1. Deploy agent to Teams channel
2. Test with sample queries
3. Verify MCP server response times
4. Check error handling

## Troubleshooting

### MCP Server Won't Connect
- Verify GitHub PAT is valid and hasn't expired
- Check if MCP server is running: `curl http://localhost:3000/health`
- Review server logs for errors
- Ensure firewall isn't blocking port 3000

### Agent Returning "Tool Not Available"
- Verify MCP connector is properly configured
- Check that tool names match exactly
- Confirm GitHub PAT has required scopes
- Restart MCP server and Copilot Studio

### Slow Response Times
- Enable caching in MCP config
- Increase timeout values
- Check GitHub API rate limits: `curl -H "Authorization: token $GITHUB_TOKEN" https://api.github.com/rate_limit`
- Consider implementing request queuing

### GitHub API Rate Limiting
**Limits:**
- Unauthenticated: 60 requests/hour
- Authenticated: 5,000 requests/hour
- GraphQL: 5,000 points/hour

**Mitigation:**
- Use GitHub Personal Access Token
- Implement caching
- Use GraphQL for complex queries (more efficient)
- Monitor rate limit headers

## Next Steps

After successful setup:
1. Customize agent instructions for your workflows
2. Add additional MCP connectors if needed
3. Deploy to Microsoft Teams
4. Gather user feedback and iterate
5. Monitor agent performance and usage metrics

## Support

For issues with:
- **GitHub MCP Server:** See [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers)
- **Copilot Studio:** Visit [Microsoft Learn - Copilot Studio](https://learn.microsoft.com/en-us/microsoft-copilot-studio/)
- **GitHub API:** Check [GitHub REST API Docs](https://docs.github.com/en/rest)
