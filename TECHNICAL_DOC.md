# Technical Documentation — Daily Financial Research + Email Agent

## Overview
This n8n workflow generates a daily financial report email by:
1. Pulling headlines from RSS feeds
2. Merging and selecting top 15 headlines
3. Asking OpenAI to generate a structured brief
4. Sending the final report through Gmail

---

## Node-by-Node Flow

### 1) Schedule Trigger
Purpose: Runs workflow automatically (daily)

Recommended:
- Frequency: Daily
- Timezone: Asia/Kolkata

Output: Trigger event item

---

### 2) RSS Nodes (Multiple)
Purpose: Pull headlines from different sources

Each RSS node returns items containing:
- title
- link
- pubDate
- contentSnippet (sometimes)

Examples:
- Reuters Business (via RSS / Google RSS)
- CNBC
- Moneycontrol
- LiveMint Markets

---

### 3) Merge Nodes (Append)
Purpose: Combine all RSS outputs into one list

Mode:
- Append

Output:
- Combined list of all news items from all sources

---

### 4) Top 15 Headlines (Function Node)
Purpose:
- Keep only 15 items for the report

Logic:
- Take merged array
- Slice first 15 items

Output:
- 15 headline items

---

### 5) Merge News + Prices (Append)
Purpose:
- Combine headline items with other optional inputs
(Current version: news-only)

Mode:
- Append

Output:
- Final dataset passed to OpenAI

---

### 6) Build Email (Function Node)
Purpose:
- Prepare clean input for OpenAI
- Optionally format into a readable structure

Output:
- Clean JSON / text fields used by OpenAI

---

### 7) OpenAI (Message a model)
Purpose:
- Generate structured report from provided headlines only

Prompt ensures:
- No hallucination
- No invented facts
- Uses only input

Output:
- Plain text email-ready report

---

### 8) Gmail (Send message)
Purpose:
- Send report to target email address

Fields:
- To: your email
- Subject: "Daily Financial Report - DD MMM YYYY"
- Body: OpenAI output text

---

## Data Rules
- The model must only use provided RSS input
- If not enough info, it must say "Not enough data provided."
- No stock prices are included in current version

---

## Future Improvements
- Add deduplication of similar headlines
- Add sentiment scoring per headline
- Add separate India vs Global sections
- Add attachments / HTML email formatting
