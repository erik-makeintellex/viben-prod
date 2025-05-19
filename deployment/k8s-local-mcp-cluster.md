# Local Kubernetes Deployment for MCP Agents & Ollama

This guide provides a local Kubernetes deployment plan using Docker Desktop (Windows) to run your Model Context Protocol (MCP) services, Ollama-based LLM inference, and essential agent infrastructure.

---

## 🧱 Overview

You will deploy the following:

| Service             | Purpose                                               |
|---------------------|-------------------------------------------------------|
| 🧠 Ollama LLM        | Local language model runner (e.g., Mistral, Phi)      |
| 🔁 LLM Router        | Handles requests from agents to Ollama                |
| 📋 Prompt Manager    | Manages prompt templates per agent/task               |
| 🧠 Session Memory    | Per-agent memory persistence using Redis/Postgres     |
| 🧑‍💻 Agent Runner     | Launches and orchestrates agent actions               |
| 🌐 Agent UI (optional)| Lightweight UI to monitor or send agent tasks        |

---

## 🧰 Prerequisites

- ✅ Docker Desktop w/ Kubernetes enabled (Windows)
- ✅ `kubectl` installed and working
- ✅ Optional: `k9s` for cluster navigation

---

## 📁 Folder Structure

```bash
k8s/
├── ollama/
│   ├── deployment.yaml
│   └── service.yaml
├── mcp-llm-router/
│   ├── deployment.yaml
│   └── service.yaml
├── mcp-prompt-manager/
├── mcp-memory/
├── mcp-agent-runner/
├── mcp-agent-ui/
└── namespace.yaml
```

## 📌 Step-by-Step Plan

1. Define Namespace

```yaml
# k8s/namespace.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: mcp
```

2. Ollama Deployment
```yaml
# k8s/ollama/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ollama
  namespace: mcp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ollama
  template:
    metadata:
      labels:
        app: ollama
    spec:
      containers:
      - name: ollama
        image: ollama/ollama
        ports:
        - containerPort: 11434
        volumeMounts:
        - name: ollama-data
          mountPath: /root/.ollama
      volumes:
      - name: ollama-data
        emptyDir: {}

---
# k8s/ollama/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: ollama
  namespace: mcp
spec:
  selector:
    app: ollama
  ports:
    - protocol: TCP
      port: 11434
      targetPort: 11434
  type: ClusterIP
```

```text
Tip: You can preload models by exec'ing into the pod or mounting pre-saved volume data.
```

## 3. MCP Core Services

Use this as a pattern (replace llm-router with other service names):

```yaml
# k8s/mcp-llm-router/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mcp-llm-router
  namespace: mcp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mcp-llm-router
  template:
    metadata:
      labels:
        app: mcp-llm-router
    spec:
      containers:
      - name: mcp-llm-router
        image: your-dockerhub/mcp-llm-router:latest
        ports:
        - containerPort: 8080
```

```yaml
# k8s/mcp-llm-router/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: mcp-llm-router
  namespace: mcp
spec:
  selector:
    app: mcp-llm-router
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: ClusterIP
```

## 4. Optional: Redis/PostgreSQL for Memory

Here’s an example Redis service:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis
  namespace: mcp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis
  template:
    metadata:
      labels:
        app: redis
    spec:
      containers:
      - name: redis
        image: redis:7
        ports:
        - containerPort: 6379

---
apiVersion: v1
kind: Service
metadata:
  name: redis
  namespace: mcp
spec:
  selector:
    app: redis
  ports:
    - port: 6379
```

## 🔄 Workflow Summary

```less
[MCP Agent UI]
      |
      v
[Agent Runner] --> [Prompt Manager]
      |
      v
[LLM Router] ---> [Ollama Service (Local Model)]
      |
      v
 [Response to UI or chained agent]
```

## 🚀 Running the Cluster

```bash
kubectl apply -f k8s/namespace.yaml
kubectl apply -f k8s/ollama/
kubectl apply -f k8s/mcp-llm-router/
# ...and so on for all other components
```

## 📡 Accessing Services

To test from your local desktop:

```bash
kubectl port-forward svc/ollama 11434:11434 -n mcp
```

# 🔗 Resources

- Ollama Local Models: https://ollama.com/library
- Docker Desktop + K8s: https://docs.docker.com/desktop/kubernetes/
- MCP Example Configs:
  - [system-prompt-inheritance.json](../config/templates/system-prompt-inheritance.json)
  - [cloud-agent-template.json](../config/templates/cloud-agent-template.json)
  - [game-dev-agent-template.json](../config/templates/game-dev-agent-template.json)