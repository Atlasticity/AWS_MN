# AWS_MN Meetup 2026-09-10
## Lab Access
https://catalog.us-east-1.prod.workshops.aws/join?access-code=99dc-0e999a-5c

## Gotchas/Issues/Fixes

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

For app/CustomerSupport/mcp_client/client.py // Added Code Snippet should look this:

```
def get_gateway_mcp_client() -> MCPClient | None:
    """Returns an MCP Client for AgentCore Gateway, if configured"""
    url = os.environ.get("AGENTCORE_GATEWAY_MY_GATEWAY_URL")
    if not url:
        logger.warning("Gateway URL not set — gateway tools unavailable")
        return None
    return MCPClient(lambda: streamable_http_client(url))
```

### Lab 4 - Step 5 - If Step 5 gives you issues, it should be ok to just skip it and move on

app/CustomerSupport/mcp_client/client.py // Fixed File:

```
import os
import logging
from strands.tools.mcp.mcp_client import MCPClient

logger = logging.getLogger(__name__)

# ExaAI MCP endpoint for web search
EXAMPLE_MCP_ENDPOINT = "https://mcp.exa.ai/mcp"


def get_streamable_http_mcp_client() -> MCPClient:
    """Returns an MCP Client for Exa AI web search"""
    return MCPClient(url=EXAMPLE_MCP_ENDPOINT)


def get_gateway_mcp_client(auth_header: str) -> MCPClient | None:
    """Returns an MCP Client for AgentCore Gateway, if configured"""
    url = os.environ.get("AGENTCORE_GATEWAY_MY_GATEWAY_SECURE_URL")
    if not url:
        logger.warning("Gateway URL not set — gateway tools unavailable")
        return None
    return MCPClient(url=url, headers={"Authorization": auth_header})
```

### Lab 6 - Step 2 // Make sure to click the drop down carrot for frontend.py

### Lab 6 - Step 3 // Make sure to click the drop down carrot for index.html
