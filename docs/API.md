# ChronosCraft AI API Documentation

> **Note:** This file is now maintained in `/docs/addenda/API.md`. For the main project vision, MVP, and actionable tasks, see `ROADMAP.md`, `MVP_CHECKLIST.md`, and `NEXT_STEPS.md` in the docs root.

## Calendar API

Base URL: `/calendar`

### Data Models

#### Calendar

```typescript
interface Calendar {
  id: string;
  year: number;
  selectedMonths: string[];
  events: CalendarEvent[];
  backgroundUrl?: string;
  createdAt: string;
  updatedAt: string;
}

interface CalendarEvent {
  date: string;
  title: string;
}
```

### Endpoints

#### GET /calendar

Returns all calendars and available months.

**Query Parameters:**

- `id` (optional): Get a specific calendar by ID

**Response:**

- Without ID:
  ```json
  {
    "calendars": Calendar[],
    "months": string[]
  }
  ```
- With ID:
  ```json
  Calendar
  ```

**Status Codes:**

- 200: Success
- 404: Calendar not found (when using ID)

#### POST /calendar

Create a new calendar.

**Request Body:**

```json
{
  "year": number,
  "selectedMonths": string[],
  "events"?: CalendarEvent[],
  "backgroundUrl"?: string
}
```

**Response:**

```json
Calendar
```

**Status Codes:**

- 201: Created
- 400: Bad Request (missing required fields)

#### PUT /calendar/:id

Update an existing calendar.

**URL Parameters:**

- `id`: Calendar ID

**Request Body:**

```json
{
  "year"?: number,
  "selectedMonths"?: string[],
  "events"?: CalendarEvent[],
  "backgroundUrl"?: string
}
```

**Response:**

```json
Calendar
```

**Status Codes:**

- 200: Success
- 404: Calendar not found

#### DELETE /calendar/:id

Delete a calendar.

**URL Parameters:**

- `id`: Calendar ID

**Response:** None

**Status Codes:**

- 204: No Content
- 404: Calendar not found

### Error Responses

All error responses follow this format:

```json
{
  "message": string
}
```

### Test Coverage

The API has comprehensive test coverage:

- Statements: 100%
- Branches: 84.21%
- Functions: 100%
- Lines: 100%

Tests include both success and error cases for all endpoints.

## Project Save/Load API (Planned)

Base URL: `/project`

- Endpoints for saving and loading project data will be documented here as implemented.

## GenAI Integration API (Planned)

Base URL: `/genai`

- Endpoints for GenAI-powered theme/styling will be documented here as implemented.

## PDF Export Utility (Frontend)

- The frontend provides a utility to export calendar data to PDF.
- See `client/src/app/utils/pdfExport.ts` for implementation details.
- Tests for this utility are in `client/__tests__/pdfExport.test.ts`.
