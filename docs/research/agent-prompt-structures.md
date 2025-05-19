# Agent Prompt Structures & Reference Patterns

This document catalogs effective multi-agent prompt design strategies, drawing from notable open-source AI tools and research projects. These can be used to structure MCP-compatible agent services and improve clarity, coordination, and adaptability in agent orchestration.

---

## 🧠 Prompt Design References

### 1. **Devin (Sourcegraph)**
**Structure: Code Deployment Assistant Prompt**
- Prompt encourages hypothesis-driven task management.
- Goal framing, code ownership, and verification checkpoints.

🔗 [View Prompt](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/main/devin-prompts/deployment-prompt.txt)

### 2. **Cursor**
**Structure: VSCode Context-Aware Agent Prompt**
- Full memory of code context.
- User-guided refactor suggestions and inline memory of decisions.

🔗 [View Prompt](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/main/cursor-prompts/system-prompt.txt)

### 3. **Dia / Windsurf**
**Structure: Browser Interaction Prompt**
- Fluent web navigation with reasoning over open tabs.
- Temporal and semantic intent tracking.

🔗 [View Prompt](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools/blob/main/windsurf/windsurf-browser.txt)

---

## 🔧 Multi-Agent Prompt Features

| Feature                     | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| Role-bound Context Memory  | Assign role-based memory per agent chain.                                  |
| Decentralized Authority    | Enables agent-cloud models without fixed central controller.               |
| Response Verification Loop | Promotes agents verifying peer-generated outputs.                          |
| Modular Reasoning Flow     | Steps can be segmented, scheduled, or replayed across agents.              |

---

## 🧰 Template Inheritance and Extension

Each agent type can reference a base system prompt and override only the required elements.

**Example JSON Inheritance:**

```json
{
  "base": "default-reasoning-agent",
  "override": {
    "task_style": "inquisitive",
    "context_scope": "code_navigation",
    "verifier_enabled": true
  }
}
```

📚 Additional Reading / GitHub References

- [System Prompts and Models of AI Tools (GitHub)](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools)
- [OpenDevin](https://github.com/sourcegraph/opendevin)
- [Microsoft AutoGen](https://github.com/microsoft/autogen)
- [LangGraph](https://github.com/langflow/langflow)

```text
These patterns are intended to inform and evolve agent architectures across secure, scalable, and intelligent MCP ecosystems.
```

## Config Files

- [cloud-agent-template.json](../../config/cloud-agent-template.json)  
- [system-prompt-inheritance.json](../../config/system-prompt-inheritance.json)

## Related Docs

- [README](../../README.md)  
- [Multi-Agent Orchestration](../multi_agent_orchestration.md)