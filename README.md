# GitHub Navigator (MCP-Powered Copilot Studio Agent)

GitHub Navigator is an AI-powered agent built using Microsoft Copilot Studio and the GitHub Model Context Protocol (MCP).

It enables developers to interact with GitHub using natural language — searching repositories, exploring code, analyzing commits, and retrieving real-time insights.

---

## Features

- Natural language GitHub navigation
- Cross-repository search (files, commits, PRs, issues)
- Real-time data via GitHub MCP server
- Direct links to GitHub resources
- Intelligent summarization and insights
- Secure API access via MCP connector

---

## Architecture

User
↓
Copilot Studio Agent (Claude Sonnet 4.6)
↓
MCP Client
↓
GitHub MCP Server
↓
GitHub APIs

See full architecture: [Architecture](./ARCHITECTURE.md)

The agent dynamically discovers and invokes GitHub tools via MCP, enabling real-time interaction with repositories.

---
## Agent instructions

See agent instructions: [Agent instructions](./docs/agent-instructions.md)

---

## Technologies Used

- Microsoft Copilot Studio
- GitHub MCP Server
- Claude Sonnet 4.6
- Model Context Protocol (MCP)

---

## Use Cases

- Find latest commits in a repo
- Search for functions across multiple repositories
- Explore issues and pull requests
- Understand codebase structure
- Generate insights across projects

---

## Demo

Demo:

---

## Future Improvements

- Pull request automation (create / review / merge)
- CI/CD pipeline analysis
- Multi-step autonomous workflows
- Integration with additional MCP servers

---

## 📸 Screenshots


# Agent Overview
![Agent Overview](./screenshots/overview.png)

### MCP Tools Integration
![MCP Tools](./screenshots/mcp-tools.png)

### Agent Test Panel
![Test Panel](./screenshots/test-panel.png)

---

## Author

Vasyl Martyshko
