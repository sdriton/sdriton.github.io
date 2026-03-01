---
layout: default
title: Confomeety Rest API Documentation
permalink: /confomeety-api/
---

# Confomeety REST API Documentation

## Authentication

**All API endpoints require Bearer Token authentication.**

You must include an `Authorization` header with a valid Bearer token in all requests:

```
Authorization: Bearer YOUR_API_KEY
```

### How to get an API Key

1. Log into your Odoo instance
2. Go to **Settings** → **Users & Companies** → **Users**
3. Select your user account
4. Go to the **API Keys** tab
5. Click **New API Key** and save the generated key

For detailed authentication instructions, see the [Confomeety Bearer Token Authentication]({{ '/confomeety-bearer-auth/' | relative_url }})

### Authentication Errors

- **401 Unauthorized**: Missing, invalid, or empty token
- **403 Forbidden**: Valid token but insufficient permissions

## Base URL

All endpoints are relative to your Odoo instance URL.

---

## Pagination

All list endpoints support pagination via query parameters:

| Parameter | Default | Max  | Description                 |
|-----------|---------|------|-----------------------------|
| `limit`   | 100     | 1000 | Number of records to return |
| `offset`  | 0       | —    | Number of records to skip   |

Paginated responses include a `metadata` object:

```json
{
  "status": "success",
  "metadata": {
    "limit": 100,
    "offset": 0,
    "total": 42
  },
  "data": [...]
}
```

---

## Multi-Company Support

All endpoints automatically filter records based on the authenticated user's allowed companies. To further restrict results to a specific company, pass `?company_id=<id>` as a query parameter.

## Date and Datetime

### UTC Time

The system expects that the `Date` and `Datetime` fields will be provided as UTC time. The presentation tier displays them in the local time.

### Format

All GET datetime fields use ISO 8601 format: `YYYY-MM-DDTHH:MM:SS`

Examples:
- `"2026-02-15T09:00:00"` — February 15, 2026 at 9:00 AM
- `"2026-02-15T14:30:00"` — February 15, 2026 at 2:30 PM

All POST and PUT datetime fields use ISO 8601 format `YYYY-MM-DD HH:MM:SS` (without the `T`)

Examples:
- `"2026-02-15 09:00:00"` — February 15, 2026 at 9:00 AM
- `"2026-02-15 14:30:00"` — February 15, 2026 at 2:30 PM

---

## Boards

### List all boards

```
GET /api/boards
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
```

**Query Parameters:**
- `type_id` (optional): Filter by board type ID (integer)
- `company_id` (optional): Filter by company ID
- `limit` (optional): Number of records (default: 100, max: 1000)
- `offset` (optional): Pagination offset (default: 0)

**Response:**
```json
{
  "status": "success",
  "metadata": {
    "limit": 100,
    "offset": 0,
    "total": 3
  },
  "data": [
    {
      "id": 1,
      "name": "Executive Board",
      "description": "Main executive board",
      "type": "Board",
      "type_id": 1,
      "type_name": "Board",
      "company_id": 1,
      "company_name": "My Company",
      "meeting_count": 5
    }
  ]
}
```

### Get a specific board

```
GET /api/boards/<board_id>
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
```

**Response:**
```json
{
  "status": "success",
  "data": {
    "id": 1,
    "name": "Executive Board",
    "description": "Main executive board",
    "type": "Board",
    "type_id": 1,
    "type_name": "Board",
    "company_id": 1,
    "company_name": "My Company",
    "meeting_count": 5
  }
}
```

### Create a board

```
POST /api/boards
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

**Request Body:**
```json
{
  "name": "New Board",
  "description": "Board description",
  "type_id": 1,
  "company_id": 1
}
```

**Response:** `201 Created` with the created board object.

### Update a board

```
PUT /api/boards/<board_id>
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

**Request Body**:
```json
{
  "name": "Updated Board Name",
  "description": "Updated description",
  "type_id": 2,
  "company_id": 1
}
```

### Delete a board

```
DELETE /api/boards/<board_id>
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
```

---

## Meetings

### List all meetings

```
GET /api/meetings
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
```

**Query Parameters:**
- `board_id` (optional): Filter by board ID
- `company_id` (optional): Filter by company ID
- `state` (optional): Filter by state (`draft`, `confirmed`, `in_progress`, `done`, `cancelled`)
- `from_date` (optional): Filter meetings starting on or after this datetime (ISO 8601)
- `to_date` (optional): Filter meetings ending on or before this datetime (ISO 8601)
- `tag` (optional): Filter meetings matching the tags specified in the parameter. Example: `tag=Sales,Finance`
- `limit` (optional): Number of records (default: 100, max: 1000)
- `offset` (optional): Pagination offset (default: 0)

**Response:**
```json
{
  "status": "success",
  "metadata": {
    "limit": 100,
    "offset": 0,
    "total": 10
  },
  "data": [
    {
      "id": 1,
      "title": "Q1 Review Meeting",
      "start_datetime": "2026-02-15T09:00:00",
      "stop_datetime": "2026-02-15T11:00:00",
      "duration": 2.0,
      "location": "Conference Room A",
      "board_id": 1,
      "company_id": 1,
      "company_name": "My Company",
      "state": "confirmed",
      "tag_ids": [
        {"id": 3, "name": "Important"}
      ],
      "active": true
    }
  ]
}
```

### Get a specific meeting

```
GET /api/meetings/<meeting_id>
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
```

**Response:**
```json
{
  "status": "success",
  "data": {
      "id": 1,
      "title": "Q1 Review Meeting",
      "start_datetime": "2026-02-15T09:00:00",
      "stop_datetime": "2026-02-15T11:00:00",
      "duration": 2.0,
      "location": "Conference Room A",
      "board_id": 1,
      "company_id": 1,
      "company_name": "My Company",
      "state": "confirmed",
      "tag_ids": [
        {"id": 3, "name": "Important"}
      ],
      "active": true
    }
}
```

### Create a meeting

```
POST /api/meetings
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

**Request Body:**
```json
{
  "title": "New Meeting",
  "start_datetime": "2026-02-15 14:00:00",
  "stop_datetime": "2026-02-15 16:00:00",
  "location": "Room 101",
  "board_id": 1,
  "state": "draft",
  "company_id": 1
}
```

**Response:** `201 Created` with the created meeting object.

### Update a meeting

```
PUT /api/meetings/<meeting_id>
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

**Request Body**:
```json
{
  "title": "Updated Meeting Title",
  "start_datetime": "2026-02-15 14:00:00",
  "stop_datetime": "2026-02-15 16:00:00",
  "location": "New Room",
  "board_id": 1,
  "state": "confirmed",
  "active": true,
  "company_id": 1
}
```

### Delete a meeting

```
DELETE /api/meetings/<meeting_id>
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
```

---

## Topics

### List all topics

```
GET /api/topics
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
```

**Query Parameters:**
- `meeting_id` (optional): Filter by meeting ID
- `board_id` (optional): Filter by board ID
- `company_id` (optional): Filter by company ID
- `category_id` (optional): Filter by topic category ID
- `status_id` (optional): Filter by topic status ID
- `tag` (optional): Filter topics matching the tags specified in the parameter. Example: `tag=Sales,Finance`
- `limit` (optional): Number of records (default: 100, max: 1000)
- `offset` (optional): Pagination offset (default: 0)

Results are ordered by `sequence` ascending.

**Response:**
```json
{
  "status": "success",
  "metadata": {
    "limit": 100,
    "offset": 0,
    "total": 8
  },
  "data": [
    {
      "id": 1,
      "sequence": 10,
      "meeting": {
        "id": 1,
        "title": "Q1 Review Meeting",
        "start_datetime": "2026-02-15T09:00:00",
        "stop_datetime": "2026-02-15T11:00:00",
        "duration": 2.0
      },
      "board": {
        "id": 1,
        "name": "Executive Board"
      },
      "company_id": 1,
      "company_name": "My Company",
      "category": {
        "id": 1,
        "name": "Budget"
      },
      "subject": "Q1 Budget Review",
      "subject_url": "https://example.com/doc",
      "goal": {
        "id": 2,
        "name": "Decision"
      },
      "meeting_date": "2026-02-15T09:00:00",
      "duration": 1.0,
      "presenter_ids": [
        {"id": 2, "name": "John Doe"}
      ],
      "status": {
        "id": 1,
        "name": "Approved"
      },
      "tag_ids": [
        {"id": 3, "name": "Finance"}
      ],
      "file_count": 2,
      "report": "<p>Budget approved with minor adjustments</p>",
      "active": true
    }
  ]
}
```

### Get a specific topic

```
GET /api/topics/<topic_id>
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
```
**Response:** `200 Success` with the requested topic object.

### Create a topic

```
POST /api/topics
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

**Request Body:**
```json
{
  "board_id": 1,
  "meeting_id": 1,
  "subject": "New Topic Subject",
  "subject_url": "https://example.com/doc",
  "company_id": 1,
  "category_id": 1,
  "goal_id": 2,
  "status_id": 5,
  "sequence": 20,
  "presenter_ids": [2, 3],
  "report": "<p>Topic report</p>",
  "company_id": 1
}
```

**Response:** `201 Created` with the created topic object.

### Update a topic

```
PUT /api/topics/<topic_id>
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

**Request Body** (all fields are optional):
```json
{
  "subject": "Updated Topic Subject",
  "subject_url": "https://example.com/updated-doc",
  "category_id": 2,
  "goal_id": 3,
  "status_id": 1,
  "sequence": 30,
  "presenter_ids": [4],
  "report": "<p>Updated report</p>",
  "active": true,
  "company_id": 1
}
```

**Response:** `200 Success` with the updated topic object.

### Delete a topic

```
DELETE /api/topics/<topic_id>
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
```

---

## Error Responses

All endpoints return errors in the following format:

```json
{
  "status": "error",
  "message": "Error description"
}
```
## Status Codes

Common HTTP status codes:
- `200`: Success
- `201`: Resource created
- `401`: Missing or invalid Bearer token
- `403`: Insufficient permissions
- `404`: Resource not found
- `500`: Internal server error

---

