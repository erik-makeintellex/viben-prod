
# MCP Agent Cloud Platform

Welcome to the **Model Context Protocol (MCP) Agent Cloud** project—a modular, open-source framework for deploying, coordinating, and extending intelligent agents across distributed and local environments.

This project provides:
- A full-stack agent orchestration architecture
- Reusable system and agent templates
- Infrastructure setup using Docker and Kubernetes
- Model hosting and coordination with Ollama
- Configurable agent contexts (game dev, SRE, consultant, etc.)

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-org/mcp-agent-cloud.git
cd mcp-agent-cloud
```

### 2. Spin Up Local MCP Services via Docker

```bash
docker-compose -f docker/docker-compose.mcp.yml up --build
```

> See [`docker/`](./docker/) for all container templates.

## Docker MCP Templates

MCP can be containerized and orchestrated using Docker for flexible deployment and portability. Template configurations for Docker Compose and MCP agent containers will be available soon under:

📁 `docker/`  

- [MCP Docker Setup Guide](./docs/mcp_docker_setup_guide.md)
- [MCP Template Usage Guide](./docs/mcp_template_usage_guide.md)

These templates support:

- Self-hosted MCP Agent nodes
- Ollama-backed model runners (optionally containerized)
- Container orchestration ready for Kubernetes clusters
- Volume mounting for shared prompts/configs

> 🛠️ Template generation pending — see documentation for planned structure and how to extend.



### 3. Deploy Ollama with Agents

Install [Ollama](https://ollama.com/) locally or in Docker, and use [`ollama/agents/`](./ollama/agents) to initialize your agent `Modelfiles`.

```bash
ollama run -f ollama/agents/game-dev-agent/Modelfile
```

---

## 🧠 Project Structure

### ── 📁 `docs/`
All documentation and technical guides for MCP agents, prompt systems, infrastructure, and research.

- [`docs/README.md`](./docs/README.md) – Full Documentation Index  
- [`docs/research/agent-prompt-structures.md`](./docs/research/agent-prompt-structures.md)  
- [`docs/infra/kubernetes-deployment.md`](./docs/infra/kubernetes-deployment.md)  
- [`docs/infra/ollama-agent-modelfiles.md`](./docs/infra/ollama-agent-modelfiles.md)  

---

## 📦 Core Components

### 🧩 Agents
- System-level templates: [`config/templates/system-prompt-inheritance.json`](./config/templates/system-prompt-inheritance.json)  
- Agent roles: [`config/templates/cloud-agent-template.json`](./config/templates/cloud-agent-template.json)  
- Game development config: [`config/templates/game-dev-agent-template.json`](./config/templates/game-dev-agent-template.json)  

### 🐳 Docker & Services
- Docker Compose setup: [`docker/docker-compose.mcp.yml`](./docker/docker-compose.mcp.yml)  
- Ollama setup with agents: [`ollama/`](./ollama/)  

### ☁️ Kubernetes
- Local development with Windows Desktop Kubernetes  
- Kubernetes YAML templates (MCP nodes, Ollama, Gateway API): [`docs/infra/kubernetes-deployment.md`](./docs/infra/kubernetes-deployment.md)  

---

## 🔧 Development Profiles

Each dev persona uses pre-built templates:

| Profile        | Description |
|----------------|-------------|
| Gamer Agent    | Game planning, system tuning, scripting logic |
| SRE Agent      | Infrastructure management, deployment diagnostics |
| Consultant AI  | Prompt reflection, strategic planning for teams |

> Full breakdowns in [`docs/profiles/`](./docs/profiles/)

---

## 🔁 Prompt Structures

- Templates for inheritance: [`system-prompt-inheritance.json`](./config/templates/system-prompt-inheritance.json)  
- Prompt chaining: [`docs/research/agent-prompt-structures.md`](./docs/research/agent-prompt-structures.md)  

---

## 🧪 Research & Background

- Agent prompt ecosystems  
- Open-source LLM comparisons  
- Agent interoperability methods  

See [`docs/research/`](./docs/research/)

---

## 📚 Reference Links

- 🌐 [Model Context Protocol](https://mcp.so/)  
- 🧠 [GitHub - MCP Core](https://github.com/modelcontextprotocol)  
- 📘 [LLM Prompt Libraries](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools)  
- [Docker MCP Templates](./docs/docker/docker-mcp-templates.md)


---

## ✅ Roadmap

- [ ] Add GPU-aware Ollama scaling in Kubernetes  
- [ ] Implement autoscaling for prompt microservices  
- [ ] Build WebSocket routing for real-time agent interaction  
- [ ] Package game dev agent for immediate onboarding  

---

## 🧭 Contribution Guide

We welcome contributions from agents and humans alike.

```bash
# Run all lint & style checks
./scripts/lint.sh
```

Open a PR or issue if you'd like to extend this framework with a new agent archetype, workflow, or container template.

---

> ✨ This framework was built to explore deep contextual synergy between humans and LLM agents through shared structure, clarity, and extendability.