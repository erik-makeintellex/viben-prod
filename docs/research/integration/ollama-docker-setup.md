# Ollama Integration for Internal Projects (Docker Setup)

This guide provides production-ready configurations to launch Ollama inside containerized environments for local/private inference and agent orchestration.

Ollama enables running open language models (like LLaMA, Mistral, Phi, etc.) locally and efficiently, ideal for MCP agent setups or developer prototyping.

---

## 🧠 Why Use Ollama in MCP Projects?

- ✅ Run local inference with GPU/CPU acceleration
- 🔒 Keep data on-premise for privacy
- 🔁 Integrate with MCP agents as a backend LLM interface
- 🔧 Extend into DevOps, game agents, or creative workflows with portable containerized agents

---

## 📦 Production Dockerfile

This is a minimal example to build an Ollama runtime container:

```Dockerfile
# Dockerfile
FROM ollama/ollama

# Optionally preload a model
RUN ollama pull mistral
```

## ⚙️ Docker Compose (With Volume + Port + Model Bootstrap)

This docker-compose.yml provides:

- persistent volume
- published port (11434)
- model preload (Mistral or any supported model)

```yaml
# docker-compose.yml
version: '3.8'

services:
  ollama:
    image: ollama/ollama
    container_name: ollama
    ports:
      - "11434:11434"
    volumes:
      - ollama-data:/root/.ollama
    environment:
      - OLLAMA_MODELS=mistral
    restart: unless-stopped

volumes:
  ollama-data:
```

```text
🔄 Preload models in entrypoint if needed with:
docker exec -it ollama ollama pull phi or ollama pull llama2
```

## 🔗 Integration with MCP Agent Nodes

In your MCP agent templates (system-prompt-inheritance.json, etc.), set the LLM provider endpoint like this:

```json
{
  "llm_provider": {
    "type": "local",
    "url": "http://localhost:11434/api/generate",
    "model": "mistral"
  }
}
```

## 🚀 Launch & Test

Start the container:
```bash
docker-compose up -d
```

Test the Ollama endpoint:
```bash
curl http://localhost:11434/api/generate -d '{
  "model": "mistral",
  "prompt": "What is the Model Context Protocol?",
  "stream": false
}'
```

expected results:
```json
{
  "response": "The Model Context Protocol (MCP) enables...",
  ...
}
```

# 🛠️ Notes & Resources

- 🧰 Full list of available models: ollama.com/library
- 🧪 Run on CPU: add --no-gpu to entrypoint or build script
- 📎 Can be paired with langchain, llama.cpp, or other tools