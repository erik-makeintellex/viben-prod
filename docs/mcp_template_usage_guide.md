# Using MCP Templates: Step-by-Step Guide

This guide walks you through using the MCP agent configuration templates, integrating them into your environment (CLI, AnythingLLM, FooCode), and customizing them for real-world deployment.

---

## Step 1: Clone or Pull the Repository

```bash
git clone https://github.com/erik-makeintellex/viben-prod.git
cd viben-prod
```

---

## Step 2: Install MCP Agent

Make sure `mcp-agent` is installed and available. You can use it in:

* **Command line (CLI)** via direct invocation or scripts
* **AnythingLLM** via Roo Plugin
* **FooCode** through linked workflows

### Pip Install (General Local Use)

```bash
pip install mcp-agent
```

> This allows you to run MCP agents via Python or terminal commands. Useful for local prototyping and scripting.

### Docker Install (For Containerized Agents)

```dockerfile
RUN pip install mcp-agent
```

> This installs `mcp-agent` inside Docker containers. Useful when scaling via Docker/Kubernetes.

**Configuration Tip**: You will still need config files mounted or built into the image. Use volume mapping or build context accordingly.

See: [`docker/mcp-compose.yaml`](https://github.com/erik-makeintellex/viben-prod/blob/main/docker/mcp-compose.yaml)

---

## Step 3: Review and Modify Configuration Templates

Navigate to:

```
/config/templates/
```

Templates include:

* `system-prompt-inheritance.json`
* `cloud-agent-template.json`
* `game-dev-agent-group.json`

### Key Parameters to Configure:

```json
{
  "default_model": "llama3",
  "context_window": 8192,
  "instruction_styles": ["conversational", "structured"],
  "linked_workflows": ["generate_gdscript", "summarize_level_logic"]
}
```

> Each template has embedded comments for context. For parameter breakdowns, see:
> [Agent Prompt Structures](https://github.com/erik-makeintellex/viben-prod/blob/main/docs/agent_prompt_structures.md)

---

## Step 4: Start a Local MCP Server (Optional)

Use Docker Compose to bring up your MCP node locally:

```bash
docker-compose -f docker/mcp-compose.yaml up --build
```

> This creates a local orchestration engine for agents defined in your config. Dockerfiles are designed to preload templates.

For Kubernetes setup, see:
[Kubernetes Deployment Overview](https://github.com/erik-makeintellex/viben-prod/blob/main/docs/kubernetes_deployment_guide.md)

---

## Step 5: Use Templates to Instantiate Agents

### In CLI or Scripts:

```python
from mcp_agent import AgentManager

agents = AgentManager.from_template("./config/templates/game-dev-agent-group.json")
agent = agents.get("godot_helper")
response = agent.run("How do I add physics to a GDScript object?")
```

### In AnythingLLM:

* Configure via **Roo Plugin Format**
* Register your agents as REST endpoints
* Point to MCP via exposed URLs and map actions

See: [Roo Plugin Format](https://docs.anythingllm.xyz/plugins/roo)

### In FooCode:

* Link agent endpoints or embed workflows
* Extend MCP JSON templates to export FooCode-ready formats

---

## Step 6: Develop and Iterate

* Extend configuration templates with new roles, behavior chains, or instructions
* Add container startup entries for any additional services
* Share workflows across agents (via linked\_workflows)

---

## Reference Links

* [Glama MCP Servers](https://glama.ai/mcp/servers)
* [AnythingLLM Roo Plugin Format](https://docs.anythingllm.xyz/plugins/roo)
* [Docker MCP Templates](./docker)
* [Agent Prompt Structures](./docs/agent_prompt_structures.md)
* [MCP Service Architecture](./docs/mcp_service_architecture.md)
* [Multi-Agent Orchestration](./docs/multi_agent_orchestration.md)

---

## Next Steps

* Explore `config/templates/game-dev-agent-group.json` to build AI helpers for Godot and GDScript.
* Use the Kubernetes guide to launch scalable self-hosted agents.
* Connect workflows with real assets via `linked_workflows`.
* Leverage Roo for seamless AnythingLLM integration.
