# AWS_MN Meetup 2026-09-10
## Lab Access
https://future.link

## Issues

### Lab 1 - Step 4

Fix typo in app/CustomerSupport/mcp_client/client.py 

Line #3 should be:
```
from mcp.client.streamable_http import streamable_http_client
 ```

Line #14 should be: 
```
return MCPClient(lambda: streamable_http_client(EXAMPLE_MCP_ENDPOINT))
```

### Lab 3 - Step 4

Added Code Snippet should look this:

```
def get_gateway_mcp_client() -> MCPClient | None:
    """Returns an MCP Client for AgentCore Gateway, if configured"""
    url = os.environ.get("AGENTCORE_GATEWAY_MY_GATEWAY_URL")
    if not url:
        logger.warning("Gateway URL not set — gateway tools unavailable")
        return None
    return MCPClient(lambda: streamable_http_client(url))
```

### Lab 4 - Step 5

Fixed File:

```
import os
import logging
from mcp.client.streamable_http import streamable_http_client
from strands.tools.mcp.mcp_client import MCPClient
 
logger = logging.getLogger(__name__)
 
# ExaAI provides information about code through web searches, crawling and code context searches through their platform. Requires no authentication
EXAMPLE_MCP_ENDPOINT = "https://mcp.exa.ai/mcp"
 
def get_streamable_http_mcp_client() -> MCPClient:
    """Returns an MCP Client compatible with Strands"""
    # to use an MCP server that supports bearer authentication, add headers={"Authorization": f"Bearer {access_token}"}
    return MCPClient(lambda: streamable_http_client(EXAMPLE_MCP_ENDPOINT))
 
def get_gateway_mcp_client(auth_header: str) -> MCPClient | None:
    """Returns an MCP Client for AgentCore Gateway, if configured"""
    url = os.environ.get("AGENTCORE_GATEWAY_MY_GATEWAY_SECURE_URL")
    if not url:
        logger.warning("Gateway URL not set — gateway tools unavailable")
        return None
    return MCPClient(lambda: streamable_http_client(
        url=url,
        headers={"Authorization": auth_header}
    ))
```
