# Setup & Deployment Guide

## Table of Contents
- [Copilot Studio Configuration](#copilot-studio-configuration)
- [GitHub Authentication](#github-authentication)
- [Testing & Validation](#testing--validation)
- [Troubleshooting](#troubleshooting)
- [Advanced Configuration](#advanced-configuration)


## Copilot Studio Configuration

### Step 1: Create Agent
1. Open [Microsoft Copilot Studio](https://copilotstudio.microsoft.com/)
2. Click **Create blank agent**
4. Fill in **Name:** GitHub Navigator
5. **Language:** English (United States)
6. Choose your **Solution** and **Schema name**
7. Click **Create**
8. Edit:
   - **Agent's icon**
   - **Description:** An MCP-powered DevOps assistant for real-time GitHub insights and workflow support.
   - **Instructions:** See [Agent Instructions](./agent-instructions.md)
9. **Select your agent's model:** Claude Sonnet 4.6
10. Add **Knowledge source:** https://github.com/
11. Disable Web Search
    
### Step 2: Add GitHub MCP Server Tool
The GitHub MCP connector is **built-in** to Copilot Studio and ready to use immediately!

### Step 1: Add GitHub Connector (2 minutes)
1. Open [Microsoft Copilot Studio](https://copilotstudio.microsoft.com/)
2. Create a new agent or open existing one
3. Go to **Actions** → **Library** → Search for "GitHub"
4. Click on **GitHub** connector
5. Click **Add to agent**

That's it! The connector is now available as a tool.

### Step 2: Authenticate
1. In your agent, when using the GitHub tool, you'll be prompted to authenticate
2. Click **Sign in with GitHub** (or use existing connection)
3. GitHub OAuth login window appears
4. Authorize Copilot Studio to access your GitHub account
5. Done! You're ready to use all GitHub tools

## GitHub Authentication

### Permissions Required
When you authorize Copilot Studio to access GitHub, it requests:
- Read access to repositories
- Read access to commits, issues, and pull requests
- Read access to user profile and organizations
- (Optional) Write access if you enable PR/issue creation features

### Connection Management
- **View connections:** Copilot Studio → Settings → Connections
- **Revoke access:** GitHub Settings → Apps → Authorized OAuth Apps → Revoke access to "Copilot Studio"
- **Re-authenticate:** Simply click "Sign in with GitHub" again in the agent

### Multi-Account Support
If you have multiple GitHub accounts:
1. The connector uses the currently authenticated GitHub user
2. To switch accounts, revoke and re-authenticate
3. Each Copilot Studio agent can use a different GitHub connection

### Step 3: Configure Agent Instructions
1. Go to **Agent Settings** → **Agent Instructions**
2. Copy-paste content from [agent-instructions.md](./agent-instructions.md)
3. Customize for your workflows and repositories
4. Save

### Step 4: Test the Agent
In the **Test** panel (right side), try:
- "Find the latest commit in onlinevasyl/github-navigator"
- "Search for function `getUserData` in repos"
- "Show open issues in my repositories"

### Step 5: Deploy to Teams (Optional)
1. Go **Publish**
2. Choose deployment channel:
   - **Microsoft Teams** - Add to Teams channels
   - **Microsoft 365 Copilot** - Available in M365 Copilot
   - **Web** - Shareable web link
3. Follow channel-specific deployment steps

## Available GitHub Tools

Once connected, the following tools are available to your agent:

| Tool | Description |
|------|-------------|
| `Search repositories` | Find repositories by name/topic |
| `Get repository details` | Retrieve repo info (stars, description, etc.) |
| `List repository files` | Browse repository structure |
| `Search code` | Find code across repositories |
| `List commits` | Get commit history |
| `Get commit details` | View specific commit changes |
| `Search commits` | Find commits by message |
| `List issues` | Retrieve open/closed issues |
| `Get issue details` | View issue content and comments |
| `Search issues` | Find issues by keyword |
| `List pull requests` | Get PRs by status |
| `Get PR details` | View PR content and review status |
| `Search pull requests` | Find PRs by keyword |

## Testing & Validation

### Test in Agent
1. Open the agent test panel
2. Try these scenarios:

**Basic Repository Search:**
```
Find repositories named "github-navigator"
```
Expected: Agent returns matching repositories with links.

**Code Search:**
```
Search for function "getUserData" across repos
```
Expected: Agent lists files and locations where function exists.

**Issue Tracking:**
```
Show all open issues in onlinevasyl/github-navigator
```
Expected: Agent returns list of open issues with titles and status.

**Commit Analysis:**
```
What was changed in the latest commit of onlinevasyl/github-navigator?
```
Expected: Agent shows files changed, additions, deletions, author, date.

**Cross-Repository Insights:**
```
Find all TODO comments across my repositories
```
Expected: Agent searches code and aggregates results.

### Validate Before Deployment
- [ ] Agent responds to GitHub queries correctly
- [ ] Links in responses work and are accurate
- [ ] Authentication persists across conversations
- [ ] Error messages are helpful (not raw API errors)
- [ ] Response times are acceptable (< 5 seconds typical)

## Troubleshooting

### "GitHub connection not found"
**Solution:**
- Ensure you've clicked "Sign in with GitHub"
- Check that OAuth window completed successfully
- Try revoking and re-authenticating
- Check Copilot Studio → Settings → Connections

### "Access denied" or "Unauthorized"
**Possible causes:**
- GitHub account doesn't have access to the repository
- Personal Access Token (if used) expired
- Insufficient permissions

**Solution:**
- Verify you can access the repo on GitHub.com
- Re-authenticate with GitHub
- Check repository access permissions

### Tool returns "Repository not found"
**Check:**
- Repository name is correct (case-sensitive)
- Repository is public or you have access
- Repository actually exists on GitHub.com
- Try full path: `owner/repo` format

### Slow responses from GitHub
**Typical causes:**
- GitHub API is under load
- Large repository or complex queries
- Network latency

**Mitigation:**
- Retry the query
- Use more specific search terms
- Check [GitHub Status](https://www.githubstatus.com/) for outages
- Be patient (can take 10-30 seconds for complex searches)

### "Rate limit exceeded"
GitHub has API rate limits:
- Authenticated: 5,000 requests/hour
- Unauthenticated: 60 requests/hour

**Solution:**
- Re-authenticate with GitHub (already done in Copilot Studio)
- Wait an hour for limit reset
- Use more specific queries to reduce requests
- Combine multiple queries into one agent request

### Agent ignores GitHub tools
**Check:**
- GitHub connector is added to agent (see Step 2 above)
- Agent instructions mention GitHub tools
- Test panel shows tools as available
- Refresh browser and try again

## Advanced Configuration

### Customizing Agent Instructions

Edit [agent-instructions.md](./agent-instructions.md) to customize:
- Available workflows and commands
- Response format and tone
- Error handling approach
- Examples and use cases

**Example customization:**
```markdown
### Skills
- Search repositories for vulnerabilities
- Analyze commit patterns for code quality
- Track issue resolution progress
- Aggregate insights from multiple repos
```

### Monitoring Agent Usage

In Copilot Studio:
1. Go to **Analytics**
2. View:
   - Total conversations
   - Common questions
   - Tools used most frequently
   - Error rates

### Setting Up Team Collaboration

To allow team members to use the agent:
1. Publish agent to **Microsoft Teams**
2. Add to team channel
3. Team members authenticate individually with their GitHub account
4. Each user's queries use their GitHub access

## Next Steps

1. ✅ Set up agent with GitHub connector
2. ✅ Test core scenarios
3. 📋 Customize agent instructions for your team
4. 📤 Deploy to Teams or M365 Copilot
5. 📊 Monitor usage and gather feedback
6. 🔄 Iterate and improve agent behavior

## Support & Resources

- **GitHub Connector Issues:** [Microsoft Learn - GitHub Connector](https://learn.microsoft.com/en-us/microsoftteams/platform/m365-apps/github-enterprise-integration)
- **Copilot Studio Help:** [Microsoft Learn - Copilot Studio](https://learn.microsoft.com/en-us/microsoft-copilot-studio/)
- **GitHub API Docs:** [GitHub REST API](https://docs.github.com/en/rest)
- **GitHub Status:** [Check API Status](https://www.githubstatus.com/)

---

**Pro Tip:** Bookmark the [agent-instructions.md](./agent-instructions.md) file to easily customize your agent's behavior and add new workflows over time.
