# Workflow Documentation

## Recycling Rewards Workflow

### Overview
The Recycling Rewards workflow automates the process of verifying recycling submissions and calculating rewards for users.

### Workflow Flow

1. **Webhook** - Receives Telegram webhook with photo submission
2. **Get User** - Retrieves user information from Supabase
3. **Check Photo** - Validates photo presence and extracts location data
4. **Get a file** - Downloads photo file from Telegram
5. **Create Verification Request** - Creates verification record in Supabase
6. **Extract Verification ID** - Extracts verification ID from response
7. **Perform Verification Checks** - Runs verification logic against submission
8. **Calculate Rewards** - Calculates credits and points based on verification
9. **Save Submission** - Saves submission record to database
10. **Add Rewards** - Updates user account with rewards
11. **Success Message** - Generates success message with rewards
12. **Send Message** - Sends confirmation message via Telegram
13. **Webhook Response** - Returns success response

### Node Configuration

#### Webhook Node
- **Path**: `/recycling-rewards`
- **Method**: POST
- **Response Mode**: Response Node

#### Get User Node
- **Operation**: Get
- **Table**: `telegram_users`
- **Filter**: `chat_id == {{ $json.body.chatId }}`

#### Create Verification Request
- **URL**: `{{ $env.SUPABASE_URL }}/rest/v1/rpc/create_verification_jsonb`
- **Method**: POST
- **Headers**:
  - `apikey`: `{{ $env.SUPABASE_ANON_KEY }}`
  - `Authorization`: `Bearer {{ $env.SUPABASE_ANON_KEY }}`
  - `Content-Type`: `application/json`
  - `Prefer`: `return=representation`

#### Perform Verification Checks
- **URL**: `{{ $env.SUPABASE_URL }}/rest/v1/rpc/perform_verification_jsonb`
- **Method**: POST
- **Body**: `{ "p_verification_id": "{{ $json.verification_id }}" }`

### Reward Calculation

- **Credit Rate**: R5 per kg
- **Points**: 1 point per R1
- **Minimum Credit**: R10
- **Maximum Credit**: R500

## Bill Notifications Workflow

### Overview
Automated bill payment notification system. Configuration details will be added once the workflow is imported from Notion.

### Status
Workflow configuration pending - awaiting import from Notion documentation.
