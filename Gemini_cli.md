# Getting Started with Gemini CLI - Step-by-Step Guide

Welcome to this comprehensive guide on Gemini CLI! This README is designed as a detailed, step-by-step tutorial to help you install, configure, authenticate, and use Gemini CLI. It's based on the official documentation and structured for easy following, especially if you're creating a YouTube video tutorial. We'll cover everything from basics to advanced features, without skipping details. At the end, I'll include an example project you can build step-by-step in your video to demonstrate real-world usage.

This guide assumes you're familiar with basic terminal commands. We'll use Markdown for clarity, with code blocks for commands and configurations.

---

## Table of Contents

- Introduction to Gemini CLI
- Installation
- Authentication
- Configuration
- Basic Usage
- Commands and Shortcuts
- Advanced Features
- Sandboxing and Security
- Telemetry and Usage Statistics
- Deployment and Architecture
- Example Project: Building a Simple Node.js App with Gemini CLI

---

## Introduction to Gemini CLI

Gemini CLI is an AI-powered command-line tool that brings advanced language models to your terminal. It helps with tasks like code generation, file editing, document review, and more. Powered by Google's Gemini models, it's great for developers, writers, and anyone who works in the terminal.

### Key Features:

- **AI Assistance:** Generate code, explain files, summarize content.
- **Tools Integration:** Built-in tools for file operations, shell commands, web searches.
- **Customization:** Configure models, themes, extensions, and more.
- **Security:** Sandboxing for safe tool execution.
- **Modes:** Interactive, headless (non-interactive) for scripting.

### Quickstart Overview:

- Install via npm.
- Authenticate with Google.
- Configure settings.
- Run commands like `gemini` to start chatting with AI.

---

## Installation

The standard way to install Gemini CLI is using npm (Node.js package manager). You need Node.js installed (version 18+ recommended).

### Standard Installation (Recommended for Most Users)

Open your terminal. Run the global install command:



npm install -g @google/gemini-cli



Verify installation by running:

gemini --version



This should display the version number.

### Alternative: Run without global install using npx:

npx @google/gemini-cli



### Run in a Sandbox (For Security)

For isolated execution, use Docker or Podman. Pull and run the sandbox image:

docker run --rm -it us-docker.pkg.dev/gemini-code-dev/gemini-cli/sandbox:0.1.1



Or, if Gemini CLI is installed locally, use the flag:

gemini --sandbox -y -p "your prompt here"



### Run from Source (For Developers/Contributors)

Clone the repository:

git clone https://github.com/google-gemini/gemini-cli.git
cd gemini-cli



Install dependencies:

npm install



Run in development mode:

npm run start



For production-like environment:

npm link packages/cli
gemini


### Run Latest from GitHub

npx https://github.com/google-gemini/gemini-cli



> **Note**: If you encounter permission issues on macOS/Linux, use `sudo` or check your npm configuration.

---

## Authentication

Gemini CLI requires Google authentication. We'll cover interactive and headless modes.

### Quick Check: Running in Google Cloud Shell?

If yes, authentication is automatic using Cloud Shell credentials. Skip to configuration.

### Interactive Mode (Recommended)

Run `gemini` after installation. You'll see:

How would you like to authenticate for this project?

Login with Google

Use Gemini API key

Vertex AI

text

Select option 1: Login with Google (easiest for Google AI Pro/Ultra subscribers). A browser window opens. Sign in with your Google account. Credentials are cached locally.

### Optional: Set Google Cloud Project (if prompted, e.g., for Workspace accounts):

export GOOGLE_CLOUD_PROJECT="YOUR_PROJECT_ID"

text

Enable Gemini for Cloud API in your Google Cloud Console. Make persistent by adding to `~/.bashrc` or `.env`.

### Use Gemini API Key

Get key from [Google AI Studio](https://aistudio.google.com). Set environment variable:

export GEMINI_API_KEY="YOUR_GEMINI_API_KEY"

text

> **Warning:** Keep this secret!

### Use Vertex AI

Set required variables:

export GOOGLE_CLOUD_PROJECT="YOUR_PROJECT_ID"
export GOOGLE_CLOUD_LOCATION="us-central1"

text

#### ADC with gcloud:

unset GOOGLE_API_KEY GEMINI_API_KEY

gcloud auth application-default login

text

#### Service Account JSON

Create in Google Cloud, download JSON, then:

export GOOGLE_APPLICATION_CREDENTIALS="/path/to/keyfile.json"


#### Google Cloud API Key:

export GOOGLE_API_KEY="YOUR_GOOGLE_API_KEY"



### Headless/Non-Interactive Mode

Use environment variables (e.g., `GEMINI_API_KEY`) or cached credentials. If none, CLI errors out.

### Persisting Environment Variables

Add to shell config (e.g., `~/.bashrc`):

echo 'export GEMINI_API_KEY="YOUR_KEY"' >> ~/.bashrc
source ~/.bashrc

=

Or use `.env` file in `~/.gemini/.env`:

mkdir -p ~/.gemini
echo 'GEMINI_API_KEY="YOUR_KEY"' > ~/.gemini/.env

text

---

## Configuration

Configuration uses layers: defaults, settings files, environment variables, CLI arguments. Settings are in JSON files.

### Settings Files Locations

- System defaults: `/etc/gemini-cli/system-defaults.json` (override with env var).
- User: `~/.gemini/settings.json`.
- Project: `./.gemini/settings.json`.
- System overrides: `/etc/gemini-cli/settings.json`.

Use schema for validation:  
[https://raw.githubusercontent.com/google-gemini/gemini-cli/main/schemas/settings.schema.json](https://raw.githubusercontent.com/google-gemini/gemini-cli/main/schemas/settings.schema.json)

### Available Settings Categories

(Place under top-level keys in `settings.json`)

- general
- output
- ui
- ide
- privacy
- model
- context
- tools
- mcp
- security
- advanced
- experimental
- telemetry

### Example `settings.json`:

{
"general": {
"vimMode": true,
"preferredEditor": "code"
},
"ui": {
"theme": "GitHub",
"hideBanner": true
},
"model": {
"name": "gemini-1.5-pro-latest"
}
}

text

### Environment Variables

Some important ones:

| Variable                     | Description                        |
| ----------------------------| ---------------------------------|
| `GEMINI_API_KEY`             | API key                          |
| `GEMINI_MODEL`               | Default model (e.g., "gemini-2.5-flash") |
| `GOOGLE_API_KEY`             | For Vertex AI                    |
| `GOOGLE_CLOUD_PROJECT`       | Project ID                      |
| `GOOGLE_APPLICATION_CREDENTIALS` | Path to JSON key             |
| `GOOGLE_CLOUD_LOCATION`      | Location (e.g., "us-central1")  |
| `GEMINI_SANDBOX`             | Sandbox mode                    |
| `SEATBELT_PROFILE`           | macOS sandbox profile           |
| `GEMINI_TELEMETRY_ENABLED`   | Enable telemetry (true/false)   |

More available for telemetry and advanced configurations.

Automatically loads `.env` files from `~/.gemini/`.

### Command-Line Arguments

Some useful CLI flags:

- `--model <name>`: Set model.
- `--prompt <text>`: Non-interactive prompt.
- `--sandbox`: Enable sandbox.
- `--yolo`: Auto-approve tools.
- `--debug`: Verbose output.

### Context Files (`GEMINI.md`)

Instructional files to provide AI context.  

Locations:  
- Global: `~/.gemini/GEMINI.md`  
- Project: In root and subdirectories.

Commands to manage context: `/memory add/show/refresh/list`

Example `GEMINI.md` content:

Project Instructions
Use 2 spaces for indentation.

Follow functional programming.

text

---

## Basic Usage

Run the CLI by typing:

gemini

text

Then type prompts, e.g.,

Generate a Hello World in JS.

text

Use `@` to refer to files:

@file.js Explain this.

text

Use `!` for shell commands:

!ls

text

Non-interactive usage:

echo "Prompt" | gemini

text

### Examples:

- Generate code:

Write a Python script for Fibonacci.

text

- Edit files (with tools like `replace`, `write_file`).

---

## Commands and Shortcuts

### Slash Commands (`/`)

- `/bug`: File issue.
- `/chat save/resume/list/delete/share`: Manage conversations.
- `/clear`: Clear screen (Ctrl+L).
- `/compress`: Summarize context.
- `/copy`: Copy last output.
- `/directory add/show`: Manage workspaces.
- `/editor`: Select editor.
- `/extensions`: List extensions.
- `/help`: Show help.
- `/mcp list/desc/schema/auth/refresh`: Manage MCP servers.
- `/model`: Select model.
- `/memory add/show/refresh/list`: Manage context.
- `/restore`: Undo changes.
- `/settings`: Edit settings.
- `/stats`: Show stats.
- `/theme`: Change theme.
- `/auth`: Change auth.
- `/about`: Version info.
- `/tools`: List tools.
- `/privacy`: Privacy notice.
- `/quit`: Exit.
- `/vim`: Toggle vim mode.
- `/init`: Create `GEMINI.md`.

### At Commands (`@`)

- `@path`: Inject file/directory content.

### Exclamation Commands (`!`)

- `!cmd`: Run shell command.
- `!`: Toggle shell mode.

### Custom Commands

Create in `~/.gemini/commands/` or project directory as `.toml` files.

Example, `refactor/pure.toml`:

description = "Refactor to pure function."

prompt = "Refactor this code into a pure function: {{args}}"

text

### Keyboard Shortcuts

- Ctrl+A: Home.
- Ctrl+E: End.
- Ctrl+C: Clear/Cancel.
- Ctrl+Z: Undo.
- Ctrl+L: Clear screen.
- Tab: Accept suggestion.

Full list available in documentation.

---

## Advanced Features

- Checkpointing: Enable in settings; auto-saves before changes. Use `/restore`.
- Enterprise Config: See enterprise docs.
- Telemetry: Configure in settings/telemetry.
- Token Caching: Optimizes API calls (API key only).
- Trusted Folders: Security for projects.
- Ignoring Files: Use `.geminiignore`.
- Non-Interactive Mode: For scripts, e.g., `gemini -p "Prompt" --output-format json`.
- Themes: Use `/theme`.
- Extensions: Manage with experimental settings.
- Model Selection: `/model` for Auto/Pro/Flash.

---

## Sandboxing and Security

- Enable with `--sandbox` or environment variable.
- Custom Dockerfile in `.gemini/sandbox.Dockerfile`.
- YOLO mode: Auto-approve (use carefully).
- Folder Trust: Configure in security settings.

---

## Telemetry and Usage Statistics

Gemini CLI collects anonymized data such as tool calls, API requests, and session info. Does not collect PII, prompts, or file contents.

Opt-out by setting in privacy:

{
"privacy": {
"usageStatisticsEnabled": false
}
}

text

---

## Deployment and Architecture

- NPM Packages: `@google/gemini-cli-core` (backend), `@google/gemini-cli` (frontend).
- Build Tools: `tsc` for NPM, `esbuild` for GitHub.
- Docker: Support for sandbox.
- Release Process: GitHub Actions.

---

## Example Project: Building a Simple Node.js App with Gemini CLI

In your YouTube video, demonstrate building a basic Node.js todo app using Gemini CLI step-by-step. This covers installation, authentication, configuration, and usage.

### Step 1: Setup Project

mkdir todo-app
cd todo-app
npm init -y
gemini

text

### Step 2: Authenticate

Follow interactive Google login.

### Step 3: Configure (Add `GEMINI.md`)

Run `/init` to generate, or manually create:

Todo App Instructions
Use Express.js.

Store todos in memory.

Follow REST API style.

text

### Step 4: Generate Code

Prompt:

Generate a basic Express.js server for a todo API. @GEMINI.md

text

Use Gemini CLI tools to write files like `server.js` and `routes.js`.

### Step 5: Edit and Debug

Run commands like:

@server.js "Fix this bug: todos not saving."
!node server.js



### Step 6: Add Features

For example, add authentication middleware:

Add authentication middleware.


Use `/chat save todo-base` to checkpoint.

### Step 7: Finalize

- Use `/tools` to list available tools.
- Use `/stats` to check CLI usage.
- Commit code with custom command:

Create `git/commit.toml` and run `/git:commit`.

---

## Conclusion

This README provides a full overview to help you get started with Gemini CLI, from installation to building a real-world project. Use it to guide your YouTube tutorial and help viewers learn step by step.
