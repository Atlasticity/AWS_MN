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
