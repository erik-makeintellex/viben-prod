# Agent Prompt Structures

This document outlines prompt structure strategies and inheritance models used for MCP agents. It includes templates, delegation chains, and examples of role-based prompt setups for various agent tasks (cloud ops, dev, SRE, gaming).

---

## Table of Contents

- [Overview](#overview)
- [Core Prompt Templates](#core-prompt-templates)
- [Prompt Inheritance Design](#prompt-inheritance-design)
- [Use Case Templates](#use-case-templates)
- [References](#references)

---

## Overview

Agents can inherit system prompts and behavior templates based on task type, platform, or priority. Prompts are modular, injected at run time, and can reference JSON/YAML configuration for reuse across agents.

See also:
- [`system-prompt-inheritance.json`](../config/templates/system-prompt-inheritance.json)
- [`cloud-agent-template.json`](../config/templates/cloud-agent-template.json)
- [`game-dev-agent-template.json`](../config/templates/game-dev-agent-template.json)

---

## Core Prompt Templates

MCP supports configurable prompt templates to maintain standardization across agents. Templates include:

- **System prompts** with role alignment
- **Tool contexts** and skills
- **Conversation memory toggles**
- **Security & authorization hints**

See: [`system-prompt-inheritance.json`](../config/templates/system-prompt-inheritance.json)

---

## Prompt Inheritance Design

Prompt inheritance allows defining roles and toolsets at a high level, then extending or overriding specific fields per agent.

Example (conceptual):

```json
{
  "base_prompt": {
    "model": "gpt-4",
    "system": "You are an expert SRE focused on uptime and Kubernetes ops."
  },
  "child_prompt": {
    "inherits": "base_prompt",
    "system": "You also handle advanced observability with Grafana and Loki."
  }
}
```

# Use Case Templates

Each use-case template applies prompt logic to specific workflows. Examples include:

- [cloud-agent-template.json](../../config/templates/cloud-agent-template.json) – for orchestrating cloud tasks
- [game-dev-agent-template.json](../../config/templates/game-dev-agent-template.json) – for local indie game workflows
- [system-prompt-inheritance.json](../../config/templates/system-prompt-inheritance.json) – role-based inheritance logic

# References

- 🧠 [Model Context Protocol Site](https://mcp.so/)
- 🔧 [MCP Server Templates](https://github.com/modelcontextprotocol/servers)
- 📘 [Prompt Engineering for Agent Chains](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools)