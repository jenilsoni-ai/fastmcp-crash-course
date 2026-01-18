# Lesson 3: Prompts and Context

## Prompts: Reusable Message Templates

Prompts allow you to define parameterized message templates that guide the LLM's behavior.

```python
from fastmcp import FastMCP

mcp = FastMCP("PromptServer")

@mcp.prompt
def explain_code(language: str, code: str) -> str:
    """Ask the LLM to explain a snippet of code."""
    return f"Please explain the following {language} code:\n\n{code}"
```

## Accessing MCP Context

Sometimes your tools or resources need access to the underlying MCP context, such as the request ID or client information. You can do this by adding a `Context` parameter to your function.

```python
from fastmcp import FastMCP, Context

mcp = FastMCP("ContextServer")

@mcp.tool
async def get_request_info(ctx: Context) -> dict:
    """Returns information about the current request."""
    return {
        "request_id": ctx.request_id,
        "client_id": ctx.client_id if hasattr(ctx, 'client_id') else "unknown"
    }
```

## Summary

In this crash course, we've covered:
1. **Introduction**: What FastMCP is and how to install it.
2. **Tools**: How to give LLMs executable capabilities.
3. **Resources**: How to provide read-only data via URIs.
4. **Prompts**: How to create reusable message templates.
5. **Context**: How to access request-specific metadata.

FastMCP provides a powerful yet simple way to build production-ready MCP servers in Python.
