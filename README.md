# Daily Financial Research Email Agent (n8n + OpenAI + Python + Gmail)

A daily automated agentic AI workflow that fetches top financial headlines (Global + India), summarizes them using OpenAI, and emails a crisp morning brief every day at 9:00 AM.

## Tech Stack
- n8n (workflow automation)
- RSS Feeds (Reuters, Bloomberg, FT, ET, Moneycontrol etc.)
- OpenAI (gpt-4o-mini) for summarization
- Gmail Node (email delivery)

## What It Does
- Pulls top finance/markets headlines from multiple sources
- Selects top 15 headlines
- Generates a structured daily report:
  1) Market Snapshot
  2) Top Headlines + why it matters
  3) Key Themes
  4) Today’s Watchlist
  5) Action Plan
- Emails the final report automatically

## Workflow Files
- `workflow.json` → Import this into n8n

## Setup Instructions (n8n)
1. Create a free n8n cloud account
2. Import the workflow JSON:
   - Open workflow editor
   - Import from file
   - Select `workflow.json`
3. Update RSS URLs if needed
4. Add OpenAI credentials
5. Add Gmail credentials
6. Set schedule trigger to 9:00 AM (Asia/Kolkata)
7. Activate workflow

## OpenAI Prompt Used
The OpenAI node uses a strict prompt to avoid hallucinations and keep output concise.

## Notes
- This workflow is news-only (no stock prices)
- You can extend it later by adding a stock price API node

