# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Smithery Python MCP (Model Context Protocol) server project that provides tools, resources, and prompts through a FastMCP server with session-scoped configuration support.

## Common Commands

### Development
```bash
# Run development server with hot reload
uv run dev
uv run dev --reload

# Test interactively with playground
uv run playground

# Run production server
uv run start
```

### Testing
Currently no test framework is configured. When adding tests, update this section.

### Dependencies
```bash
# Install/sync dependencies
uv sync

# Build distribution
uv build
```

## Architecture

### Core Structure
The server is built using:
- **FastMCP** with Smithery decorators for session management
- **Pydantic** models for configuration schemas
- Entry point: `src/hello_server/server.py:create_server`

### Session Configuration Pattern
The server uses session-scoped configuration via the `@smithery.server()` decorator:
- Config schema defined as Pydantic BaseModel
- Session config accessed via `ctx.session_config` in tools/resources
- Configuration passed as URL parameters to the MCP endpoint

### MCP Primitives
The server implements three core MCP primitives:
1. **Tools** - Executable functions via `@server.tool()`
2. **Resources** - Static data sources via `@server.resource()`
3. **Prompts** - Interaction templates via `@server.prompt()`

### Key Configuration Files
- `pyproject.toml` - Defines the server entry point in `[tool.smithery]` section
- `smithery.yaml` - Specifies runtime as Python
- Server module path configured as `hello_server.server:create_server`

## Development Notes

- Default development port is **8081** (not 8000)
- Session IDs are logged when created for testing purposes
- Reserved config parameter names to avoid: `api_key`, `profile`, `config`
- The project currently uses the default `hello_server` module name - rename when customizing