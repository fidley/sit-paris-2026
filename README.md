# SAP Inisde Track Paris 2026
Agentic ABAP in Action: Building SAP Development Agents with ARC-1 MCP and GitHub Copilot


# 01. Workshop Overview

## Agenda
- MCP, agents, and ARC-1 overview 
- ARC-1 installation on Docker installation and SAP connection 
- Eclipse and Copilot MCP setup
- Explore a package and ABAP object 
- Dependencies, where-used, lint, diagnosis 
- Controlled `$TMP` write and activation 
- Skills, agents, troubleshooting, Q&A 

## Prerequisites

- Eclipse with SAP ABAP Development Tools (ADT), already connected to SAP.
- GitHub Copilot for Eclipse with Agent Mode.
- Docker Desktop installed and running.
- A reachable SAP ABAP development or integration system.
- An SAP user with the ADT authorizations required for the exercises.
- A safe test object or package. Use `$TMP` or an approved workshop package for writes.

# 02.  MCP, agents, and ARC-1

[MCP](https://modelcontextprotocol.io/) lets an AI client discover and call
structured tools exposed by an MCP server:

```text
GitHub Copilot for Eclipse -> MCP -> ARC-1 MCP server -> SAP ADT REST API -> SAP ABAP system
```

An agent understands a goal, selects a skill or tool, calls it, inspects the
result, and continues with human review. It is not a replacement for SAP
authorization, code review, testing, or transport governance.

[ARC-1](https://github.com/arc-mcp/arc-1) is an open-source TypeScript MCP
server for SAP ABAP systems created by Marian Zeis. It connects AI clients through the [SAP ADT REST
API](https://help.sap.com/docs/abap-cloud/abap-development-tools-user-guide/about-abap-development-tools).
It is distributed as the npm package [`arc-1`](https://www.npmjs.com/package/arc-1),
the Docker image [`ghcr.io/arc-mcp/arc-1`](https://github.com/arc-mcp/arc-1/pkgs/container/arc-1),
and an Agent Plugins package containing the server and bundled skills.

ARC-1 uses 12 intent-based tools instead of hundreds of low-level operations. It
is read-only by default. Writes, table preview, free SQL, transport mutations,
and Git mutations are separate opt-ins.

[Full documentation](https://docs.arc-1-mcp.com/)
