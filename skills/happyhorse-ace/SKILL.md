---
name: happyhorse-ace
description: Generate or edit HappyHorse video through Ace Data Cloud and retrieve the same task’s final result in Kimi Code. Use for explicit HappyHorse requests, not other media providers.
---

# HappyHorse by Ace Data Cloud

This plugin exposes only the HappyHorse workflow through the existing hosted Ace service. It does not change the conversation’s LLM provider.

Start by checking the connected tool schema. For a no-generation setup check call `happyhorse_list_models` only, and report available HappyHorse options. Never read, echo, or ask the user to paste an API Token into the conversation; it belongs in `ACEDATACLOUD_API_TOKEN` before Kimi starts.

For a new request, confirm the requested model/action, required inputs and current price are understood. Submit `happyhorse_generate_video` once only when the user has authorized the operation and its cost. Do not enable automatic generation retries or substitute a different model family.

Save the exact returned task_id. Use `happyhorse_get_task` to query that same task, observing server polling guidance. When it is still pending, explain that status and stop after a bounded check; let the user resume with the same ID. Never submit another generation to poll. Inspect mcp_task_polling and the returned state/error. Wait between polls; return the final video_url only on terminal success. A green tool call is not proof of generation completion.

If the user supplies an existing task ID, query it directly without generating. If a request returns 401/403, explain key/scope or moderation errors without requesting secrets; for 429 wait and reduce concurrency; for 5xx/timeout inspect the existing task before any separately approved resubmission.

Setup and current service information: https://platform.acedata.cloud/documents/happyhorse?utm_source=agent_skill&utm_medium=referral&utm_campaign=evergreen&utm_content=happyhorse_kimi_readme_docs
