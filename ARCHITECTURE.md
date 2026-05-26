# Architecture

## Overview

GitHub Navigator uses Microsoft Copilot Studio as the conversational layer and integrates with GitHub through the Model Context Protocol (MCP).

## Flow

1. User sends a natural language request
2. Copilot Studio agent interprets intent
3. MCP client selects appropriate tool
4. GitHub MCP server executes request
5. GitHub API returns real-time data
6. Agent formats and returns response

## Key Concept

MCP enables:
- Dynamic tool discovery
- Real-time external data access
- Action-oriented AI agents
