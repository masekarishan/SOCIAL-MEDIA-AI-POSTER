# Social Media AI Poster (n8n workflow)

Type one idea, get ready-to-post content for **Instagram, Facebook and LinkedIn**, review it, then publish with one approval.

## How it works

```text
Webhook (prompt + platforms)
   ├─► Gemini – Instagram  ─► Parse ─┐
   ├─► Gemini – Facebook   ─► Parse ─┼─► Merge ─► Combine Results
   └─► Gemini – LinkedIn   ─► Parse ─┘
                                        │
                     Generate Image (Pollinations, 1080×1080)
                                        │
                     Prepare Post Data ─► Respond to Webhook (HTML preview)
                                        │
                     Wait for approval (webhook resume)
                                        │
                     Split by Platform ─► Platform Router
                          ├─► Instagram: Create Container ─► Wait ─► Publish
                          ├─► Facebook: coming soon
                          └─► LinkedIn: Create Post
```

1. A POST request to the webhook sends the idea (`body.prompt`) and the target platforms.
2. Gemini writes a platform-specific caption, 20 hashtags and a cinematic image prompt.
3. An image is generated from that prompt.
4. A preview of every post is returned so you can check it.
5. After approval, the workflow posts to the selected platforms.

## Setup

1. Install / open [n8n](https://n8n.io) (cloud or self-hosted).
2. **Import** `Social_Media_AI_Poster_Final.json` (Workflows → Import from file).
3. Add credentials / replace placeholders:

| Where | What to add |
|-------|-------------|
| Gemini nodes | A **Query Auth** credential: name `key`, value = your Google AI Studio API key |
| Instagram nodes | Replace `YOUR_INSTAGRAM_ACCESS_TOKEN` and `YOUR_INSTAGRAM_USER_ID` |
| LinkedIn nodes | Replace `YOUR_LINKEDIN_ACCESS_TOKEN` and `YOUR_LINKEDIN_PERSON_ID` |

4. Activate the workflow and call the webhook URL shown on the Webhook node.

> ⚠️ Never commit real tokens. Keep them in n8n credentials or environment variables.

## Files

| File | Purpose |
|------|---------|
| `Social_Media_AI_Poster_Final.json` | The importable n8n workflow |
| `EXECUTION.md` | Screenshots of the workflow running |

## Author

Ishan Masekar, masekarishan@gmail.com
