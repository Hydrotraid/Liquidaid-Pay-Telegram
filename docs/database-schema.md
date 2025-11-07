# Database Schema Documentation

## Tables

### telegram_users
User account information stored in Supabase.

**Columns**:
- `id` (uuid, primary key)
- `chat_id` (bigint, unique)
- `username` (text)
- `first_name` (text)
- `last_name` (text)
- `created_at` (timestamp)
- `updated_at` (timestamp)

### recycling_verifications_jsonb
Verification records using JSONB for flexible document storage.

**Columns**:
- `id` (uuid, primary key)
- `user_id` (uuid, foreign key)
- `data` (jsonb) - Contains all verification data
- `status` (text) - Verification status
- `created_at` (timestamp)
- `updated_at` (timestamp)

**JSONB Structure**:
```json
{
  "photo_url": "string",
  "photo_file_id": "string",
  "location": {
    "latitude": number,
    "longitude": number,
    "address": "string"
  },
  "estimated_weight_kg": number,
  "material_type": "string",
  "verification_result": {
    "verified": boolean,
    "score": number,
    "confidence": number,
    "weight_kg": number
  }
}
```

### recycling_submissions
Submission history records.

**Columns**:
- `id` (uuid, primary key)
- `user_id` (uuid, foreign key)
- `verification_id` (uuid, foreign key)
- `weight_kg` (numeric)
- `credit_amount` (numeric)
- `points` (integer)
- `created_at` (timestamp)

### user_rewards
User reward tracking.

**Columns**:
- `id` (uuid, primary key)
- `user_id` (uuid, foreign key)
- `credit_amount` (numeric)
- `points` (integer)
- `transaction_type` (text)
- `created_at` (timestamp)

## Functions

### create_verification_jsonb()
Creates a new verification request with JSONB data.

**Parameters**:
- `p_user_id` (uuid)
- `p_photo_url` (text)
- `p_photo_file_id` (text)
- `p_location_latitude` (numeric)
- `p_location_longitude` (numeric)
- `p_location_address` (text)
- `p_estimated_weight_kg` (numeric)
- `p_material_type` (text)

**Returns**: `verification_id` (uuid)

### perform_verification_jsonb()
Performs verification checks on a submission.

**Parameters**:
- `p_verification_id` (uuid)

**Returns**: Verification result (jsonb)

### get_verification_jsonb()
Retrieves verification record by ID.

**Parameters**:
- `p_verification_id` (uuid)

**Returns**: Verification record (jsonb)
