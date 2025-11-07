# Configuration

This directory contains configuration examples and templates.

## Environment Variables

Create a `.env` file in your n8n instance with the following variables:

```bash
# Supabase Configuration
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_ANON_KEY=your-anon-key-here
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key-here

# Telegram Configuration
TELEGRAM_BOT_TOKEN=your-telegram-bot-token-here

# Optional: Municipal API (if applicable)
MUNICIPAL_API_URL=https://api.example.com
MUNICIPAL_API_KEY=your-municipal-api-key-here

# n8n Configuration
N8N_BASE_URL=https://your-n8n-instance.com
N8N_WEBHOOK_URL=https://your-n8n-instance.com/webhook
```

## Setup Instructions

1. Copy the environment variables to your n8n instance settings
2. Configure credentials in n8n:
   - Supabase API credentials
   - Telegram Bot API credentials
3. Update webhook URLs in workflow nodes
4. Test workflows with sample data
