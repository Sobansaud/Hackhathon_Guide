# How to Use Claude Code with Qwen Models --- 100% Free

This guide explains how to run **Claude Code (ccr)** using **Qwen
models** locally for free.

## Requirements

-   Qwen CLI (installed & authenticated)
-   Node.js v18+

------------------------------------------------------------------------

## 1. Install Qwen Code CLI

Run:

``` bash
npm install -g @qwen-code/qwen-code@latest
```

Verify:

``` bash
qwen --version
```

------------------------------------------------------------------------

## 2. Find Your Qwen Access Token

After running:

``` bash
qwen
```

Your token is stored here:

    C:\Users\PC_USER\.qwen\oauth_creds.json

Example:

``` json
{
  "access_token": "YOUR_QWEN_ACCESS_TOKEN_HERE",
  "token_type": "Bearer",
  "refresh_token": "YOUR_QWEN_REFRESH_TOKEN_HERE",
  "resource_url": "portal.qwen.ai",
  "expiry_date": 1764876220290
}
```

------------------------------------------------------------------------

## 3. Update Claude Code Router Config

Paste this full config:

``` json
{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,
  "Providers": [
    {
      "name": "qwen",
      "api_base_url": "https://portal.qwen.ai/v1/chat/completions",
      "api_key": "YOUR_QWEN_ACCESS_TOKEN_HERE",
      "models": [
        "qwen3-coder-plus",
        "qwen3-coder-plus",
        "qwen3-coder-plus"
      ]
    }
  ],
  "Router": {
    "default": "qwen,qwen3-coder-plus",
    "background": "qwen,qwen3-coder-plus",
    "think": "qwen,qwen3-coder-plus",
    "longContext": "qwen,qwen3-coder-plus",
    "longContextThreshold": 60000,
    "webSearch": "qwen,qwen3-coder-plus"
  }
}
```

------------------------------------------------------------------------

## 4. Start Using Claude Code with Qwen

Restart router:

``` bash
ccr restart
```

Start Claude Code:

``` bash
ccr code
```

Test:

    > hi

------------------------------------------------------------------------

## 5. Fixing 401 Unauthorized Token Errors

If token expires:

1.  Delete file:

```{=html}
<!-- -->
```
    C:\Users\PC_USER\.qwen\oauth_creds.json

2.  Re-login:

``` bash
qwen
```

3.  Copy new access_token and paste into config:

```{=html}
<!-- -->
```
    "api_key": "YOUR_QWEN_ACCESS_TOKEN_HERE"

------------------------------------------------------------------------

## Support

Subscribe on YouTube:\
**CodeVerse Soban**\
http://www.youtube.com/@CodeVerseSoban
