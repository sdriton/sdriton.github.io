---
layout: default
title: Bearer Token Authentication
permalink: /confomeety-bearer-auth/
nav_order: 20
---

# Bearer Token Authentication Guide

## Overview

The Confomeety API now uses Bearer Token authentication for all endpoints. This provides secure access control using Odoo 19's API key mechanism.

## How to Generate API Keys

### Method 1: User Preferences (Recommended)

1. Log into your Odoo instance
2. Go to **Settings** → **Users & Companies** → **Users**
3. Select your user account
4. Go to the **API Keys** tab
5. Click **New API Key**
6. Enter a description (e.g., "Confomeety API Access")
7. Copy the generated API key (it will only be shown once!)
8. Use this key as your Bearer token

### Method 2: Via Odoo UI

1. Navigate to your user profile (top-right corner)
2. Click on **Preferences** or **My Profile**
3. Look for the **API Keys** section
4. Generate a new API key with a descriptive name

## Using Bearer Tokens

### Authentication Header Format

All API requests must include the `Authorization` header with the Bearer token:

```
Authorization: Bearer <your-api-key>
```

### Example API Calls

#### Using cURL

```bash
# Get all boards
curl -X GET "https://your-odoo-instance.com/api/boards" \
  -H "Authorization: Bearer YOUR_API_KEY_HERE"

# Get specific board
curl -X GET "https://your-odoo-instance.com/api/boards/1" \
  -H "Authorization: Bearer YOUR_API_KEY_HERE"

# Create a new board
curl -X POST "https://your-odoo-instance.com/api/boards" \
  -H "Authorization: Bearer YOUR_API_KEY_HERE" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "New Board",
    "description": "Board description",
    "type_id": 1
  }'
```

#### Using Python Requests

```python
import requests

API_KEY = "your_api_key_here"
BASE_URL = "https://your-odoo-instance.com"

headers = {
    "Authorization": f"Bearer {API_KEY}",
    "Content-Type": "application/json"
}

# GET request
response = requests.get(f"{BASE_URL}/api/boards", headers=headers)
boards = response.json()

# POST request
new_board = {
    "name": "New Board",
    "description": "Board description",
    "type_id": 1
}
response = requests.post(f"{BASE_URL}/api/boards", headers=headers, json=new_board)
result = response.json()
```

#### Using JavaScript (Fetch API)

```javascript
const API_KEY = 'your_api_key_here';
const BASE_URL = 'https://your-odoo-instance.com';

// GET request
fetch(`${BASE_URL}/api/boards`, {
  method: 'GET',
  headers: {
    'Authorization': `Bearer ${API_KEY}`,
    'Content-Type': 'application/json'
  }
})
  .then(response => response.json())
  .then(data => console.log(data));

// POST request
fetch(`${BASE_URL}/api/boards`, {
  method: 'POST',
  headers: {
    'Authorization': `Bearer ${API_KEY}`,
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    name: 'New Board',
    description: 'Board description',
    type_id: 1
  })
})
  .then(response => response.json())
  .then(data => console.log(data));
```

## Error Responses

### Missing Authorization Header
**Status Code:** 401 Unauthorized
```json
{
  "status": "error",
  "message": "Missing Authorization header. Please provide Bearer token."
}
```

### Invalid Header Format
**Status Code:** 401 Unauthorized
```json
{
  "status": "error",
  "message": "Invalid Authorization header format. Use: Bearer <token>"
}
```

### Invalid Token
**Status Code:** 401 Unauthorized
```json
{
  "status": "error",
  "message": "Invalid or expired bearer token"
}
```

## Security Best Practices

1. **Keep API keys secure**: Never commit API keys to version control
2. **Use environment variables**: Store API keys in environment variables or secure vaults
3. **Rotate keys regularly**: Generate new keys periodically and revoke old ones
4. **Use HTTPS**: Always use secure connections (HTTPS) for API calls
5. **Limit key scope**: Create separate API keys for different applications or use cases
6. **Monitor usage**: Keep track of API key usage and revoke suspicious keys
7. **Revoke compromised keys**: Immediately revoke any API key that may have been exposed

## API Endpoints Protected

All the following endpoints now require Bearer token authentication:

### Board Endpoints
- `GET /api/boards` - List all boards
- `GET /api/boards/<int:board_id>` - Get specific board
- `POST /api/boards` - Create new board
- `PUT /api/boards/<int:board_id>` - Update board
- `DELETE /api/boards/<int:board_id>` - Delete board

### Meeting Endpoints
- `GET /api/meetings` - List all meetings
- `GET /api/meetings/<int:meeting_id>` - Get specific meeting
- `POST /api/meetings` - Create new meeting
- `PUT /api/meetings/<int:meeting_id>` - Update meeting
- `DELETE /api/meetings/<int:meeting_id>` - Delete meeting

### Topic Endpoints
- `GET /api/topics` - List all topics
- `GET /api/topics/<int:topic_id>` - Get specific topic
- `POST /api/topics` - Create new topic
- `PUT /api/topics/<int:topic_id>` - Update topic
- `DELETE /api/topics/<int:topic_id>` - Delete topic

## Permissions

API key authentication respects Odoo's standard security rules:
- The user associated with the API key must have appropriate permissions
- Record rules defined in [security.xml](../security/security.xml) still apply
- Confomeety User group: Read-only access to boards and topics
- Confomeety Manager group: Full CRUD access to all resources

## Troubleshooting

### Token authentication not working

1. Verify the API key is correctly generated in Odoo
2. Check that the Authorization header is correctly formatted
3. Ensure the user account associated with the API key is active
4. Verify the user has the necessary permissions (Confomeety groups)
5. Check Odoo logs for detailed error messages

### Testing with Postman

1. Create a new request
2. Set the request URL (e.g., `https://your-instance.com/api/boards`)
3. Go to the **Authorization** tab
4. Select **Bearer Token** type
5. Paste your API key in the **Token** field
6. Send the request

## Migration Notes

If you were previously using session-based authentication:
- All endpoints have been changed from `auth='user'` to `auth='public'` with bearer token validation
- Old session-based authentication will no longer work
- You must generate and use API keys for all API access
- Update all client applications to use Bearer token authentication

## Support

For issues or questions regarding bearer token authentication, please refer to:
- [Odoo 19 API Documentation](https://www.odoo.com/documentation/19.0/developer/reference/external_api.html)
- Confomeety module documentation:  [Confomeety Rest API Documentation]({{ '/confomeety-api/' | relative_url }})
