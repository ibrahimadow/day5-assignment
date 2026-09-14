# Exercise B: API Reference Entry
## Create Task

`POST /api/v1/projects/{projectId}/tasks`

## Description

Creates a new task within the specified project. The requesting user must be authenticated and have permission to create tasks in the target project. On success, the newly created task is returned, including server-generated fields such as its ID and creation timestamp.

## Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `projectId` | string (UUID) | Required | The unique identifier of the project the task will be created in. |

## Request Body Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `title` | string | Required | The name of the task. Must be 1–200 characters. |
| `description` | string | Optional | Additional details about the task. Plain text or Markdown, up to 5,000 characters. |
| `assigneeId` | string (UUID) | Optional | The user ID of the person the task should be assigned to. If omitted, the task is left unassigned. |
| `dueDate` | string (ISO 8601 date) | Required | The date by which the task should be completed, formatted as `YYYY-MM-DD`. |
| `priority` | string (enum) | Required | The task's priority