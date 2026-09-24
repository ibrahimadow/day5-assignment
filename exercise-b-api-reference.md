# Create Task

**Method and path:** `POST /v1/projects/{project_id}/tasks`

## Description

Creates a new task inside an existing project and assigns it to a team member. The task starts with the status `todo`. The request must come from an authenticated user who is a member of the project. On success, the endpoint returns the complete task, including the fields the server generates (`id`, `status`, `created_by`, `created_at`, `updated_at`).

## Path parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `project_id` | string | Required | The unique ID of the project the task is added to, for example `prj_1029`. |

## Query parameters

None.

## Request headers

| Header | Required | Description |
|--------|----------|-------------|
| `Authorization` | Required | Your access token in the format `Bearer <token>`. Requests without a valid token are rejected. |
| `Content-Type` | Required | Must be `application/json`. |
| `Accept` | Optional | `application/json`. The response is always JSON. |

## Request body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `title` | string | Required | A short name for the task. 1 to 200 characters. |
| `description` | string | Optional | More detail about the task. Up to 2,000 characters. If left out, the response returns `null`. |
| `assignee_id` | string | Required | The ID of the user who will do the task, for example `usr_4821`. The user must be a member of the project. |
| `due_date` | string | Required | The date the task is due, in ISO 8601 format `YYYY-MM-DD`. It cannot be in the past. |
| `priority` | string | Required | How urgent the task is. Allowed values: `low`, `medium`, `high`. |

## Example request

```
POST /v1/projects/prj_1029/tasks
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
Content-Type: application/json
```

```json
{
  "title": "Design the login screen",
  "description": "Create wireframes for the mobile login screen, including the forgot-password link.",
  "assignee_id": "usr_4821",
  "due_date": "2026-10-15",
  "priority": "high"
}
```

## Response codes

| Code | Meaning | When it happens |
|------|---------|-----------------|
| `201 Created` | The task was created. | The request was valid, and the new task is returned in the response body. |
| `400 Bad Request` | The request could not be read. | The body is not valid JSON, or a required field is missing. |
| `401 Unauthorized` | You are not signed in. | The `Authorization` header is missing, expired, or invalid. |
| `403 Forbidden` | You are not allowed to do this. | Your token is valid, but you are not a member of this project or your role does not allow creating tasks. |
| `404 Not Found` | Something you referred to does not exist. | The `project_id` does not exist, or the `assignee_id` is not a user in this project. |
| `415 Unsupported Media Type` | The wrong content type was sent. | The `Content-Type` header is not `application/json`. |
| `422 Unprocessable Entity` | The JSON is readable, but a value is not acceptable. | The title is empty or longer than 200 characters, the `priority` is not `low`, `medium`, or `high`, or the `due_date` is in the past or not in `YYYY-MM-DD` format. |
| `429 Too Many Requests` | You are sending requests too quickly. | You went over the rate limit. Wait a moment, then try again. |
| `500 Internal Server Error` | Something went wrong on our side. | An unexpected server error. Try again later, and contact support if it continues. |

## Example response (201 Created)

```json
{
  "id": "tsk_98317",
  "project_id": "prj_1029",
  "title": "Design the login screen",
  "description": "Create wireframes for the mobile login screen, including the forgot-password link.",
  "assignee_id": "usr_4821",
  "due_date": "2026-10-15",
  "priority": "high",
  "status": "todo",
  "created_by": "usr_1173",
  "created_at": "2026-09-24T14:32:08Z",
  "updated_at": "2026-09-24T14:32:08Z"
}
```

## Example error response (422 Unprocessable Entity)

```json
{
  "error": {
    "code": "invalid_value",
    "message": "priority must be one of: low, medium, high.",
    "field": "priority"
  }
}
```