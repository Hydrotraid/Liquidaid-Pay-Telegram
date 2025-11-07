# Liquidaid Pay Telegram

Production-ready n8n workflows for the Liquidaid Pay Telegram bot automation system. This repository contains workflow configurations for recycling rewards and bill notifications.

## 📋 Table of Contents

- [Overview](#overview)
- [Workflows](#workflows)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Deployment](#deployment)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

Liquidaid Pay Telegram is an automated system built with n8n that handles:
- **Recycling Rewards**: Verifies recycling submissions and calculates rewards for users
- **Bill Notifications**: Sends automated bill payment reminders and notifications

## 🔄 Workflows

### 1. Recycling Rewards

**Location**: `workflows/recycling-rewards.json`

**Description**: This workflow handles the complete recycling rewards process:
- Receives photo submissions via Telegram webhook
- Verifies user identity
- Processes recycling photos and location data
- Performs verification checks using Supabase
- Calculates rewards based on weight and verification score
- Updates user account with credits and points
- Sends confirmation messages to users

**Key Features**:
- Photo verification with location tracking
- Supabase JSONB-based verification database
- Fraud prevention and scoring system
- Automated reward calculation (R5 per kg)
- Point system integration (1 point per R1)

**Webhook Path**: `/recycling-rewards`

### 2. Bill Notifications

**Location**: `workflows/bill-notifications.json`

**Description**: Automated bill payment notification system that:
- Monitors user billing cycles
- Sends timely payment reminders
- Handles payment confirmations
- Manages notification preferences

**Status**: Configuration available (see `workflows/bill-notifications.json`)

## 📦 Prerequisites

Before deploying these workflows, ensure you have:

- **n8n Instance**: n8n v1.0+ (self-hosted or cloud)
- **Telegram Bot**: Bot token from [@BotFather](https://t.me/botfather)
- **Supabase Project**: PostgreSQL database with JSONB support
- **Environment Variables**: Configured in your n8n instance

### Required Environment Variables

```bash
# Supabase Configuration
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key

# Telegram Configuration
TELEGRAM_BOT_TOKEN=your-telegram-bot-token

# Optional: Municipal API (if applicable)
MUNICIPAL_API_URL=https://api.example.com
MUNICIPAL_API_KEY=your-api-key
```

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/Hydrotraid/Liquidaid-Pay-Telegram.git
cd Liquidaid-Pay-Telegram
```

### 2. Import Workflows to n8n

1. Open your n8n instance
2. Navigate to **Workflows** → **Import from File**
3. Select the workflow JSON file from `workflows/` directory
4. Configure credentials for each node:
   - **Supabase**: Add your Supabase credentials
   - **Telegram**: Add your Telegram bot token
   - **HTTP Request**: Configure environment variables

### 3. Configure Webhooks

1. Set up webhook URLs in your n8n instance
2. Configure Telegram bot webhook to point to your n8n webhook URL:
   ```
   https://your-n8n-instance.com/webhook/recycling-rewards
   ```

### 4. Set Up Database

Ensure your Supabase database has the required tables and functions:

- `telegram_users` - User account information
- `recycling_verifications_jsonb` - Verification records
- `recycling_submissions` - Submission history
- `user_rewards` - Reward tracking

See `docs/database-schema.md` for detailed schema documentation.

## ⚙️ Configuration

### Recycling Rewards Workflow

#### Node Configuration Checklist

- [ ] **Webhook Node**: Verify webhook path is `/recycling-rewards`
- [ ] **Get User Node**: Configure Supabase table name and filter conditions
- [ ] **Check Photo Node**: Verify photo and location extraction logic
- [ ] **Create Verification Request**: Set Supabase RPC endpoint and parameters
- [ ] **Perform Verification Checks**: Configure verification logic
- [ ] **Calculate Rewards**: Verify reward calculation formulas
- [ ] **Send Message**: Configure Telegram bot credentials

#### Environment Variables

Ensure these are set in your n8n instance:
- `SUPABASE_URL`
- `SUPABASE_ANON_KEY`

### Bill Notifications Workflow

Configuration details for Bill Notifications workflow are available in `docs/bill-notifications.md`.

## 🚢 Deployment

### Production Deployment Checklist

- [ ] All environment variables are configured
- [ ] Database schema is deployed and tested
- [ ] Webhooks are properly configured
- [ ] Telegram bot webhook is set up
- [ ] Error handling is tested
- [ ] Monitoring and logging are enabled
- [ ] Backup procedures are in place

### Testing

1. **Test Recycling Rewards**:
   ```bash
   # Send a test photo via Telegram bot
   # Verify workflow execution in n8n
   # Check database records
   # Confirm reward calculation
   ```

2. **Test Bill Notifications**:
   ```bash
   # Trigger notification workflow
   # Verify message delivery
   # Check notification preferences
   ```

## 📚 Documentation

Comprehensive documentation is available in the `docs/` directory:

- `database-schema.md` - Database schema and migrations
- `workflow-documentation.md` - Detailed workflow documentation
- `api-reference.md` - API endpoints and webhooks
- `troubleshooting.md` - Common issues and solutions

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow n8n workflow best practices
- Document all node configurations
- Include error handling in workflows
- Test workflows thoroughly before submitting
- Update documentation for any changes

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Links

- **Repository**: [https://github.com/Hydrotraid/Liquidaid-Pay-Telegram](https://github.com/Hydrotraid/Liquidaid-Pay-Telegram)
- **n8n Documentation**: [https://docs.n8n.io](https://docs.n8n.io)
- **Supabase Documentation**: [https://supabase.com/docs](https://supabase.com/docs)

## 📞 Support

For issues and questions:
- Open an issue on GitHub
- Check the documentation in `docs/`
- Review troubleshooting guide

## 🙏 Acknowledgments

- n8n team for the amazing automation platform
- Supabase for the database infrastructure
- Telegram for the bot platform

---

**Made with ❤️ for Liquidaid Pay**