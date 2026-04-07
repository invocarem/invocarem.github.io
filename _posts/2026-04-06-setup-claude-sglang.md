---
layout: post
title: "Setup and Use Claude with SGLang"
date: 2026-04-06
categories: ai llm
tags: claude sglang setup lmrouter
---

# Setup and Use Claude with SGLang

## Introduction

In this post, I'll walk through setting up Claude with SGLang using lmrouter for efficient local inference.

### Prepare lmrouter-sglang.yaml

Create a configuration file named `lmrouter-sglang.yaml`:

```yaml
server:
  host: 127.0.0.1
  port: 3000
  logging: prod

auth:
  enabled: false

responses_store:
  type: in_memory

access_keys:
  - sk-sglang

providers:
  sglang:
    type: openai
    base_url: http://localhost:30000/v1
    api_key: ""

models:
  "*":
    providers:
      - provider: sglang
        model: ""
```

## Step 1: Setup lmrouter

First, ensure pnpm is installed ([pnpm.io/installation](https://pnpm.io/installation)), then run the following command to launch LMRouter:
```bash
pnpx @lmrouter/cli lmrouter-sglang.yaml
```

This launches the LMRouter server with your SGLang configuration.

## Setup Claude CLI

To use the `claude` command, you need to configure your Claude CLI client to point to the LMRouter server. Add the following to your shell configuration file (`~/.bashrc`, `~/.zshrc`, or equivalent):

```bash
export ANTHROPIC_BASE_URL="http://127.0.0.1:3000/v1"
export ANTHROPIC_API_KEY="sk-sglang"
alias claude="claude"
```

Or if you're using a specific Claude CLI wrapper, configure it to use the LMRouter endpoint:

```bash
# Example for claude-cli or similar tools
export CLAUDE_API_BASE="http://127.0.0.1:3000/v1"
export CLAUDE_API_KEY="sk-sglang"
```

## Step 2: Using Claude via Command Line

Once lmrouter is configured, you can interact with Claude directly from the command line:

```bash
echo "analyze latin word: invenietur, provide lemma (first person present form), conjugation number and translation in JSON" | claude
```

**How it works:** The `echo "xxx" | claude` pattern pipes your text as input to Claude, which processes it and returns a response. Claude treats the piped text as your prompt.

**Note on different environments:** Some Claude CLI implementations may behave differently:
- **Expected behavior:** Claude processes the piped input and returns a response directly
- **Alternative behavior:** Some CLI tools may prompt for setup, look into the current folder for context, or enter interactive mode

If you experience unexpected behavior (e.g., Claude asks to set up or scan your folder), check your CLI tool's documentation. The setup above configures the API endpoint, but the `claude` command's behavior depends on which CLI wrapper you're using.

## Example Output

The response comes back in structured JSON format:

```json
{
  "word": "invenietur",
  "lemma": "invenio",
  "conjugation": 4,
  "form": "3rd person singular future passive indicative",
  "translation": "it/he/she will be found"
}
```

## Benefits

- **Simple CLI interface**: Pipe any prompt to `claude`
- **Structured output**: Get JSON responses for easy parsing
- **Fast inference**: SGLang backend optimized for performance
- **Flexible routing**: lmrouter handles model management

## Using Claude for Coding

You can also use Claude to generate code files directly. For example, to create a `claude.md` file in your working folder:

```bash
echo "Generate a comprehensive guide for using Claude effectively in coding projects, including best practices for prompts, context management, and output formatting. Save as claude.md" | claude > claude.md
```

This pipes your request to Claude and redirects the output to a file. You can adapt this pattern for any code generation task:

```bash
# Generate a Python script
echo "Create a Python script that parses JSON and converts it to CSV" | claude > script.py

# Generate documentation
echo "Write API documentation for a REST endpoint that handles user authentication" | claude > docs.md

# Generate test cases
echo "Generate unit tests for a function that validates email addresses" | claude > tests.py
```

## Tips for Coding with Claude

- **Be specific**: Include language, framework, and requirements in your prompt
- **Request formatting**: Ask for code blocks, comments, or specific styles
- **Iterate**: Refine outputs by piping follow-up questions
- **Save outputs**: Use `> filename` to save directly to files

## Conclusion

This setup provides a streamlined way to use Claude locally with SGLang, perfect for automation scripts and CLI workflows.

---

*Happy coding!*
