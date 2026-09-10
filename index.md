# AWS_MN Meetup 2026-09-10
# Team
Ryan Lindstedt
https://www.linkedin.com/in/ryanlindstedt/

John Spaulding
https://www.linkedin.com/in/jospaulding/

Brett Dykes
https://www.linkedin.com/in/brett-i-dykes/

Max Anderson
https://www.linkedin.com/in/mxande/

Paul DeLaria
https://www.linkedin.com/in/pauldelaria/

Norman Owens
https://www.linkedin.com/in/normanowens/

# Slide Deck
https://github.com/Atlasticity/AWS_MN/blob/main/AWS_MN--2026-09-10.pdf

# Lab
## Lab Access
https://catalog.us-east-1.prod.workshops.aws/join?access-code=99dc-0e999a-5c

**Feel free to ask an Atlasticity team-member if you or stuck!**

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

The full client.py should be:
```
import os
import logging
from mcp.client.streamable_http import streamable_http_client
from strands.tools.mcp.mcp_client import MCPClient

logger = logging.getLogger(__name__)

# ExaAI MCP endpoint for web search
EXAMPLE_MCP_ENDPOINT = "https://mcp.exa.ai/mcp"


def get_streamable_http_mcp_client() -> MCPClient:
    """Returns an MCP Client for Exa AI web search"""
    return MCPClient(lambda: streamable_http_client(EXAMPLE_MCP_ENDPOINT))


def get_gateway_mcp_client() -> MCPClient | None:
    """Returns an MCP Client for AgentCore Gateway, if configured"""
    url = os.environ.get("AGENTCORE_GATEWAY_MY_GATEWAY_URL")
    if not url:
        logger.warning("Gateway URL not set — gateway tools unavailable")
        return None
    return MCPClient(lambda: streamable_http_client(url))
```
**NOTE:** If you have previously deployed with ```agentcore deploy -y -v``` you'll need to do it again after making the changes.


**NOTE:** If you are running into errors, make sure you saved the changes to the **MCPClient** to **streamable_http_client**

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
