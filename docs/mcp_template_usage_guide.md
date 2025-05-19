# Using MCP Templates: Step-by-Step Guide

This guide walks you through using the MCP agent configuration templates, integrating them into your environment, and customizing them for real-world deployment.

---

## Step 1: Clone or Pull the Repository

```bash
git clone https://github.com/erik-makeintellex/viben-prod.git
cd viben-prod
```

---

## Step 2: Install MCP Agent

Ensure `mcp-agent` is available globally or as part of your containerized environment.

```bash
pip install mcp-agent
```

Or install in Dockerfile:

```dockerfile
RUN pip install mcp-agent
```

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

Each template contains role, model, and behavior definitions. Modify the following as needed:

* `default_model`
* `context_window`
* `instruction_styles`
* `linked_workflows`

> See comments in each file for explanation of keys.

---

## Step 4: Start a Local MCP Server (Optional)

Use Docker Compose to bring up your MCP node locally.

```bash
docker-compose -f docker/mcp-compose.yaml up --build
```

---

## Step 5: Use Templates to Instantiate Agents

If using `mcp-agent` programmatically:

```python
from mcp_agent import AgentManager

agents = AgentManager.from_template("./config/templates/game-dev-agent-group.json")
agent = agents.get("godot_helper")
response = agent.run("How do I add physics to a GDScript object?")
```

---

## Step 6: AnythingLLM Integration (Optional)

If you're connecting to AnythingLLM:

1. Register agents with exposed endpoints.
2. Use Roo Agent Plugin format.
3. Define routing rules in `agent-routing.yaml`.

---

## Step 7: Develop and Iterate

You can now:

* Extend templates.
* Add new agents.
* Create or edit workflows.
* Use Roo or custom LLM wrappers to manage I/O.

---

## Reference Links

* [Glama MCP Servers](https://glama.ai/mcp/servers)
* AnythingLLM Roo Plugin Format
* [Docker MCP Templates](https://github.com/erik-makeintellex/viben-prod/tree/main/docker)

---

## Next Steps

* Use the Kubernetes deployment guide to scale your agent cloud.
* Expand with more workflows or connect to open game assets via AI agents.
* Run GDScript tutorials via the Godot agent to auto-generate project scaffolds.

---
