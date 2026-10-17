---
description: Retrieve an existing HappyHorse task without generating again
---

Use `happyhorse_get_task` with the existing task ID in $ARGUMENTS. Inspect mcp_task_guidance and the returned state/error. Wait between polls; return the final video_url only on terminal success. A green tool call is not proof of generation completion. Never create a new task to retrieve this result.
