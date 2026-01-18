# Lesson 1: Introduction to FastMCP

## What is FastMCP?

FastMCP is a high-level Python framework designed to simplify the development of Model Context Protocol (MCP) servers. The Model Context Protocol is a standardized way to connect Large Language Models (LLMs) to external tools, data, and prompts. FastMCP acts as a "USB-C port for AI," providing a uniform interface for these connections.

## Why Use FastMCP?

FastMCP is built to be fast, simple, and Pythonic. It abstracts away the complex protocol details, allowing you to focus on your application logic. Key benefits include:

- **Minimal Boilerplate**: Use decorators to expose functions as tools or resources.
- **Automatic Schema Generation**: FastMCP uses Python type hints and docstrings to generate JSON schemas for the LLM.
- **Production Ready**: Includes built-in support for enterprise authentication and deployment tools.

## Installation

To get started, you can install FastMCP using pip:

```bash
pip install fastmcp
```

## Your First Server

Here is a simple example of a FastMCP server with a single tool:

```python
from fastmcp import FastMCP

# Create a server instance
mcp = FastMCP("My First Server")

@mcp.tool
def greet(name: str) -> str:
    """Greet a user by name."""
    return f"Hello, {name}!"

if __name__ == "__main__":
    mcp.run()
```

In this example, the `@mcp.tool` decorator automatically registers the `greet` function as a tool that an LLM can call. The docstring is used as the tool's description, and the type hint `name: str` defines the input schema.
