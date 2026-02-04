# API Reference

> **Base URL:** `https://api.platform-akademik.dev/v1`

---

## Authentication

All API requests require authentication using a Bearer token in the header.

```bash
Authorization: Bearer YOUR_API_KEY
```

### Get API Token

```http
POST /auth/token
```

| Parameter  | Type     | Required | Description          |
|------------|----------|----------|----------------------|
| `email`    | string   | Yes      | User email address   |
| `password` | string   | Yes      | User password        |

**Response:**

```json
{
  "success": true,
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "expires_in": 3600,
    "token_type": "Bearer"
  }
}
```

---

## Courses

### List All Courses

```http
GET /courses
```

**Query Parameters:**

| Parameter  | Type    | Default | Description                     |
|------------|---------|---------|---------------------------------|
| `page`     | integer | 1       | Page number for pagination      |
| `limit`    | integer | 10      | Number of items per page        |
| `search`   | string  | -       | Search by course name           |
| `status`   | string  | active  | Filter by status (active/draft) |

**Response:**

```json
{
  "success": true,
  "data": {
    "courses": [
      {
        "id": "crs_12345",
        "name": "Introduction to Programming",
        "code": "CS101",
        "credits": 3,
        "semester": "2025/2026 Ganjil",
        "instructor": {
          "id": "usr_98765",
          "name": "Dr. Ahmad Fauzi"
        },
        "enrolled_count": 45,
        "status": "active",
        "created_at": "2025-08-15T10:30:00Z"
      }
    ],
    "pagination": {
      "current_page": 1,
      "total_pages": 5,
      "total_items": 48
    }
  }
}
```

---

### Get Course by ID

```http
GET /courses/:id
```

**Path Parameters:**

| Parameter | Type   | Description       |
|-----------|--------|-------------------|
| `id`      | string | The course ID     |

**Response:**

```json
{
  "success": true,
  "data": {
    "id": "crs_12345",
    "name": "Introduction to Programming",
    "code": "CS101",
    "description": "Learn the fundamentals of programming using modern languages.",
    "credits": 3,
    "semester": "2025/2026 Ganjil",
    "schedule": [
      {
        "day": "Monday",
        "time": "08:00 - 10:30",
        "room": "Lab Komputer 3"
      },
      {
        "day": "Wednesday",
        "time": "13:00 - 14:40",
        "room": "Ruang 201"
      }
    ],
    "syllabus": [
      "Week 1-2: Variables and Data Types",
      "Week 3-4: Control Structures",
      "Week 5-6: Functions and Modules",
      "Week 7: Midterm Exam",
      "Week 8-10: Object Oriented Programming",
      "Week 11-13: Data Structures",
      "Week 14: Final Project"
    ]
  }
}
```

---

### Create Course

```http
POST /courses
```

**Request Body:**

```json
{
  "name": "Database Systems",
  "code": "CS201",
  "description": "Introduction to relational databases and SQL.",
  "credits": 3,
  "semester": "2025/2026 Genap",
  "instructor_id": "usr_98765"
}
```

**Response:** `201 Created`

```json
{
  "success": true,
  "data": {
    "id": "crs_67890",
    "message": "Course created successfully"
  }
}
```

---

### Update Course

```http
PUT /courses/:id
```

**Request Body:** (partial update supported)

```json
{
  "name": "Advanced Database Systems",
  "credits": 4
}
```

**Response:** `200 OK`

---

### Delete Course

```http
DELETE /courses/:id
```

**Response:** `204 No Content`

---

## Students

### List Students in Course

```http
GET /courses/:id/students
```

**Response:**

```json
{
  "success": true,
  "data": {
    "students": [
      {
        "id": "std_11111",
        "nim": "2023001",
        "name": "Budi Santoso",
        "email": "budi@student.university.ac.id",
        "enrollment_date": "2025-08-20T00:00:00Z",
        "grade": null
      },
      {
        "id": "std_22222",
        "nim": "2023002",
        "name": "Siti Rahayu",
        "email": "siti@student.university.ac.id",
        "enrollment_date": "2025-08-20T00:00:00Z",
        "grade": null
      }
    ],
    "total": 45
  }
}
```

---

### Enroll Student

```http
POST /courses/:id/enroll
```

**Request Body:**

```json
{
  "student_id": "std_33333"
}
```

---

## Grades

### Submit Grade

```http
POST /grades
```

**Request Body:**

```json
{
  "course_id": "crs_12345",
  "student_id": "std_11111",
  "component": "midterm",
  "score": 85,
  "max_score": 100
}
```

### Get Student Transcript

```http
GET /students/:id/transcript
```

**Response:**

```json
{
  "success": true,
  "data": {
    "student": {
      "nim": "2023001",
      "name": "Budi Santoso",
      "program": "Teknik Informatika"
    },
    "gpa": 3.45,
    "total_credits": 72,
    "courses": [
      {
        "code": "CS101",
        "name": "Introduction to Programming",
        "credits": 3,
        "grade": "A",
        "semester": "2023/2024 Ganjil"
      }
    ]
  }
}
```

---

## Error Responses

All errors follow this format:

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "The request body is invalid",
    "details": [
      {
        "field": "email",
        "message": "Email format is invalid"
      }
    ]
  }
}
```

### Common Error Codes

| Code                | HTTP Status | Description                    |
|---------------------|-------------|--------------------------------|
| `UNAUTHORIZED`      | 401         | Missing or invalid token       |
| `FORBIDDEN`         | 403         | Insufficient permissions       |
| `NOT_FOUND`         | 404         | Resource not found             |
| `VALIDATION_ERROR`  | 422         | Invalid request data           |
| `RATE_LIMITED`      | 429         | Too many requests              |
| `SERVER_ERROR`      | 500         | Internal server error          |

---

## Rate Limiting

API requests are limited to:

- **100 requests/minute** for authenticated users
- **10 requests/minute** for unauthenticated requests

Rate limit headers are included in all responses:

```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1699999999
```

---

## Webhooks

Configure webhooks to receive real-time notifications.

### Available Events

| Event                    | Description                        |
|--------------------------|------------------------------------|
| `student.enrolled`       | Student enrolled in a course       |
| `grade.submitted`        | New grade submitted                |
| `course.created`         | New course created                 |
| `assignment.due`         | Assignment deadline approaching    |

### Webhook Payload

```json
{
  "event": "grade.submitted",
  "timestamp": "2025-12-01T14:30:00Z",
  "data": {
    "course_id": "crs_12345",
    "student_id": "std_11111",
    "grade": "A"
  }
}
```

---

*Last updated: February 2026*
