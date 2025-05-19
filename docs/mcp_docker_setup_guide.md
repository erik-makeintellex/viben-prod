# MCP Docker Setup Guide: Cross-Platform Local and Cloud Deployment

## Purpose

This guide provides a straightforward, generic Docker-based setup for hosting MCP services, designed to work seamlessly across local environments and cloud platforms.

---

## Prerequisites

- Docker installed (Docker Desktop recommended for Windows/Mac).  
- Basic knowledge of Docker commands and container management.

---

## Step 1: Clone the MCP Docker Repository

```bash
git clone https://github.com/modelcontextprotocol/mcp-docker.git
cd mcp-docker

(This repository contains the official Docker setup for Model Context Protocol MCP services.)
```

---

## Step 2: Review the Docker Compose File

- docker-compose.yml defines MCP service containers, including:
- Core MCP runtime containers
- API gateways
- Supporting services (e.g., Redis for caching, PostgreSQL for state persistence)

## Step 3: Configure Environment Variables

- Copy .env.example to .env and modify variables to suit your environment:
- MCP_API_TOKEN – Authentication token for secure access
- REDIS_URL – Redis service connection string
- POSTGRES_URL – PostgreSQL connection string

## Step 4: Start the MCP Services

```bash
docker-compose up -d
```

## Step 5: Verify Running Services

```bash
docker-compose ps
```

- Ensure all containers show as "Up".
- Optionally, check logs for errors:

```bash
docker-compose logs -f
```

## Step 6: Access MCP Services

- Use a REST client or cURL to interact with MCP service endpoints.
- Authenticate using the token configured in .env.

## Step 7: Scaling and Management

- To scale MCP runtime containers:

```bash
docker-compose up --scale mcp-runtime=3 -d
```

- To stop and remove containers:

```bash
docker-compose down
```

## Additional Resources

- Model Context Protocol GitHub:
    https://github.com/modelcontextprotocol
    Contains core MCP repositories, including runtimes, tools, and documentation.

- MCP Official Website:
    https://mcp.so/
    Provides detailed information, official specs, and community resources for MCP.

# Summary

This guide streamlines MCP service deployment using Docker Compose, enabling rapid local setup and serving as a foundation for cloud migration. It prioritizes ease of use, security, and scalability.

# Next Steps

After setup, explore the [MCP Service Architecture](mcp_service_architecture.md) to understand how the runtimes, APIs, and storage interact.

# External Resources

- [MCP GitHub Repository](https://docs.roocode.com/features/mcp/recommended-mcp-servers)
- [Docker Official Documentation](https://docs.docker.com/)
- [MCP Servers](https://glama.ai/mcp/servers)
