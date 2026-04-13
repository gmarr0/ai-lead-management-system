# Architecture Notes

## Infrastructure Overview

The system runs entirely on a self-hosted machine with no cloud compute costs.
All services are containerized or run as local processes.

## Data Flow

1. User submits form via public URL (Cloudflare Tunnel → local n8n instance)
2. n8n workflow triggers immediately on submission
3. Form data passed to Ollama LLM running locally on the same machine
4. LLM returns structured JSON: `{"category": "...", "ai_response": "..."}`
5. JavaScript node parses and validates the JSON output
6. Edit Fields node structures all data into clean named fields
7. Google Sheets node appends a new row (Date, Name, Phone, Email, Class, Category, AI Response)
8. Pushover node fires HTTP request to Pushover API with lead summary
9. Switch node evaluates `ai_category` field against 5 routing rules
10. Matched email node sends branded HTML email via Gmail SMTP

## AI Classification Logic

The LLM prompt instructs the model to:
- Return ONLY valid JSON (no prose, no markdown)
- Classify based on the "Interested Class" field and message content
- Categories: Beginner, Advanced, Client, Kids, Custom
- Generate a warm, relevant ai_response for each category

## Security Model

- Cloudflare Tunnel handles all TLS termination
- n8n runs on internal network only, never directly exposed
- No API keys or credentials stored in workflow expressions
- Google Sheets uses OAuth2 service account
- Gmail uses App Password (not main account password)

## Scaling Notes

- Each new client business gets a subdomain via Cloudflare
- New workflow can be duplicated and customized per client in ~30 minutes
- Ollama model is shared across workflows (low resource usage for classification tasks)
