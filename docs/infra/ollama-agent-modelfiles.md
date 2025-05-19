# Ollama Agent Modelfile Guide

## Overview
Brief on how agents are deployed using Ollama and Modelfiles in MCP.

## Sample Modelfiles
- [Coordinator Agent](../../ollama/agents/agent-coordinator/Modelfile)
- [Game Dev Agent](../../ollama/agents/game-dev-agent/Modelfile)
- [Cloud Infra Agent](../../ollama/agents/cloud-infra-agent/Modelfile)

## Commonly Tuned Parameters

```plaintext
PARAMETER num_ctx <tokens>       # Controls context window (e.g., 2048–8192)
PARAMETER temperature <float>    # 0.2–0.9; lower = deterministic, higher = creative
PARAMETER top_k <int>            # Limits token sampling to top-k likely words
PARAMETER top_p <float>          # Cumulative probability for sampling (used in nucleus sampling)
PARAMETER num_batch <int>        # Max tokens per batch (dependent on hardware)
```

# Tips for Production Use

- Align num_ctx to the expected size of chained conversations
- Lower temperature for infra/security agents
- Use GPU monitoring tools to adjust num_batch and prevent OOM