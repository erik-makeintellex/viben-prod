# MCP Docker Setup Guide

This guide explains how to deploy and run MCP agents using Docker. These templates enable reproducible, isolated agent environments for local development or production deployment.

---

## 📁 Directory Overview

The `docker/` directory includes the following key files:

```
/docker
├── mcp-compose.yaml               # Main Docker Compose setup
├── .env                           # Optional: secrets or config overrides
├── game-dev-agent-group.json      # Sample config for a group of dev agents
└── templates/
    ├── agents-base.yaml           # Generic multi-agent definition
    ├── ollama-models.yaml         # Optional: Ollama LLM model setup
    └── volumes/
        ├── config/
        │   ├── game-dev-agent-group.json
        │   ├── godot_gdscript_agent.json
        │   └── unity_csharp_agent.json
        └── ollama/
```

---

## 🐳 Launching MCP with Docker Compose

### Step 1: Local Launch Command

```bash
docker compose -f docker/mcp-compose.yaml up --build -d
```

* `--build` ensures Docker rebuilds layers if anything has changed.
* Use `-d` to run it in detached mode.

---

## ⚙️ Configuration Files

### 🔹 MCP Agent Group Config

[`game-dev-agent-group.json`](../docker/templates/volumes/config/game-dev-agent-group.json):

```json
{
  "group_name": "game-dev-agents",
  "default_model": "codellama:7b",
  "agents": {
    "godot_helper": {
      "role": "game_engine_assistant",
      "model": "codellama:7b",
      "system_prompt": "You are a GDScript expert..."
    }
  }
}
```

### 🔹 Docker Compose File

[`mcp-compose.yaml`](../docker/mcp-compose.yaml):

```yaml
services:
  mcp-node:
    image: ghcr.io/glamaai/mcp-agent:latest
    ports:
      - "8080:8080"
    volumes:
      - ./templates/volumes/config:/app/config
    environment:
      - MCP_ENV=production
      - CONFIG_PATH=/app/config/game-dev-agent-group.json
```

---

## 🧠 Optional: Ollama Setup

Use [`ollama-models.yaml`](../docker/templates/ollama-models.yaml) to define local model access for Ollama. This mounts the model directory and exposes port 11434:

```yaml
  ollama:
    image: ollama/ollama:latest
    ports:
      - "11434:11434"
    volumes:
      - ./templates/volumes/ollama:/root/.ollama
    restart: unless-stopped
```

---

## 🔑 Notes

* You may use `.env` in the `docker/` directory for secrets or tokenized settings.
* The MCP image is pulled from `ghcr.io/glamaai/mcp-agent:latest`.
* Agent JSON configurations live under `/docker/templates/volumes/config/`.

---

## ✅ Next Steps

* Add more agents to `volumes/config/`
* Optionally integrate with [Ollama](https://ollama.com/)
* Reference agent groups in `CONFIG_PATH` for other agent compositions
