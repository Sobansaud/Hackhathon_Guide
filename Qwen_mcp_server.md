# 🎉 Qwen CLI + MCP Servers (GitHub MCP + Context7 MCP) --- Full Setup Guide

This guide shows you **exactly** how to connect:

-   **Qwen CLI**
-   **GitHub MCP server**
-   **Context7 MCP server**

Follow each step in order --- everything is written clearly for
beginners and advanced users.

------------------------------------------------------------------------

## 📌 1. Qwen Settings File Location

Qwen CLI reads your MCP server configuration from:

    .qwen/settings.json

If this folder/file does not exist, create it.

------------------------------------------------------------------------

## 📌 2. Add MCP Servers in `.qwen/settings.json`

``` json

  "mcpServers": {
    "github": {
      "httpUrl": "https://api.githubcopilot.com/mcp/",
      "headers": {
        "Authorization": "Bearer $GITHUB_MCP_PAT"
      }
    },
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"],
      "env": {
        "CONTEXT7_API_KEY": "YOUR_API_KEY"
      }
    }
  }

```

------------------------------------------------------------------------

## 🚀 3. Creating GitHub Fine-Grained Personal Access Token

1.  Open GitHub → Settings → Developer settings → Personal access tokens
    → Fine-grained tokens\
2.  Click **Generate new token → Fine-grained token**\
3.  Select repository access\
4.  Enable permissions:
    -   Contents: Read\
    -   Metadata: Read\
    -   (Optional) Issues: Read, Pull Requests: Read\
5.  Generate token & copy it immediately.

------------------------------------------------------------------------

## 🔐 4. Add GitHub Token to Your Environment

**Mac/Linux**

``` bash
export GITHUB_MCP_PAT="ghp_your_token_here"
```

**Windows PowerShell**

``` powershell
$env:GITHUB_MCP_PAT = "ghp_your_token_here"
```

**.env file**

    GITHUB_MCP_PAT=ghp_your_token_here
    CONTEXT7_API_KEY=your_context7_api_key_here

------------------------------------------------------------------------

## 🔥 5. Setting Up Context7 MCP

1.  Visit Context7 website\
2.  Copy your API key\
3.  Add it to your `.env.local`

------------------------------------------------------------------------

## 🧪 6. Test MCP Servers

``` bash
qwen mcp list
```

------------------------------------------------------------------------

## 📝 Final settings.json Example

``` json
{
  "mcpServers": {
    "github": {
      "httpUrl": "https://api.githubcopilot.com/mcp/",
      "headers": {
        "Authorization": "Bearer $GITHUB_MCP_PAT"
      }
    },
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"],
      "env": {
        "CONTEXT7_API_KEY": "YOUR_API_KEY"
      }
    }
  }
}
```

------------------------------------------------------------------------

## ❤️ Final Note

If this helped you, please subscribe to **Codevrse Soban**! 🙌🔥
