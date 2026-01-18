# Lesson 2: Tools and Resources

## Tools: Giving LLMs Capabilities

Tools are the core building blocks of an MCP server. They are Python functions that an LLM can execute to perform actions like querying a database or calling an API.

### Advanced Tool Configuration

You can customize how a tool is exposed using decorator arguments:

```python
@mcp.tool(
    name="calculate_sum",
    description="Adds two numbers together.",
    tags={"math", "basic"}
)
def add(a: int, b: int) -> int:
    return a + b
```

## Resources: Providing Data to LLMs

Resources are read-only data sources that an LLM can access. They are identified by unique URIs.

### Static and Dynamic Resources

Resources can be static or dynamic. Dynamic resources use URI templates to accept parameters.

```python
# Static Resource
@mcp.resource("resource://config")
def get_config() -> dict:
    return {"theme": "dark", "version": "1.0"}

# Dynamic Resource with URI Template
@mcp.resource("resource://user/{user_id}/profile")
def get_user_profile(user_id: str) -> str:
    return f"Profile data for user {user_id}"
```

### Return Types

FastMCP automatically handles the serialization of return values:
- `str` is sent as plain text.
- `dict` and `list` are serialized to JSON.
- `bytes` are base64 encoded.
