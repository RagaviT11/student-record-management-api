# Student Record Management API

A RESTful backend API for managing students, courses, and enrollments using Node.js, Express.js, and MySQL.

## Project Overview

The Student Record Management API manages student records, course information, and student-course enrollments through RESTful APIs.

### Features

- Student management
- Course management
- Enrollment management
- Search and filtering
- Sorting and pagination
- Request validation
- Error handling
- MySQL relational database
- CRUD operations
- Parameterized SQL queries

## Technology Stack

| Technology | Purpose |
|---|---|
| Node.js | JavaScript runtime |
| Express.js | Backend web framework |
| MySQL | Relational database |
| mysql2 | MySQL database connectivity |
| dotenv | Environment variable management |
| Postman | API testing |
| Git | Version control |
| GitHub | Source code hosting |

## Project Structure

```text
Task1-Student-Record-API/
├── src/
│   ├── config/
│   │   └── db.js
│   ├── controllers/
│   │   ├── studentController.js
│   │   ├── courseController.js
│   │   └── enrollmentController.js
│   ├── routes/
│   │   ├── studentRoutes.js
│   │   ├── courseRoutes.js
│   │   └── enrollmentRoutes.js
│   └── app.js
├── .env
├── .gitignore
├── package.json
├── package-lock.json
└── README.md
```

## Database Setup

The application uses MySQL.

Create the database:

```sql
CREATE DATABASE student_record_db;
USE student_record_db;
```

### Students Table

```sql
CREATE TABLE students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) NOT NULL UNIQUE,
    phone VARCHAR(15),
    date_of_birth DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Courses Table

```sql
CREATE TABLE courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    course_code VARCHAR(20) NOT NULL UNIQUE,
    description VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Enrollments Table

```sql
CREATE TABLE enrollments (
    enrollment_id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT NOT NULL,
    course_id INT NOT NULL,
    enrollment_date DATE NOT NULL,
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id),
    UNIQUE (student_id, course_id)
);
```

The enrollments table connects students and courses. Foreign keys maintain relationships, while the unique constraint prevents duplicate enrollment of the same student in the same course.

## Environment Configuration

Create a `.env` file in the project root:

```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=YOUR_MYSQL_PASSWORD
DB_NAME=student_record_db
DB_PORT=3306
PORT=5000
```

Replace `YOUR_MYSQL_PASSWORD` with your local MySQL password. Do not upload your `.env` file or database credentials to GitHub.

## Installation

### 1. Clone the Repository

Replace the placeholder with the URL of your GitHub repository.

```bash
git clone <YOUR_REPOSITORY_URL>
```

### 2. Navigate to the Project

```bash
cd Task1-Student-Record-API
```

### 3. Install Dependencies

```bash
npm install
```

### 4. Start the Application

Make sure MySQL is running and the database and tables are created.

```bash
node src/app.js
```

The expected output may include:

```text
Server running on port 5000
MySQL database connected successfully
```

## API Base URL

```text
http://localhost:5000
```

## API Endpoints

### Student APIs

| Method | Endpoint | Description |
|---|---|---|
| POST | `/students` | Create a student |
| GET | `/students` | Get all students |
| GET | `/students/:id` | Get a student by ID |
| PUT | `/students/:id` | Update a student |
| DELETE | `/students/:id` | Delete a student |

Example request to create a student:

```json
{
  "name": "Sample Student",
  "email": "student@example.com",
  "phone": "9876543210",
  "date_of_birth": "2005-10-09"
}
```

Search students:

```text
GET /students?search=Sample
```

Sort students:

```text
GET /students?sort=name&order=asc
```

Paginate students:

```text
GET /students?page=1&limit=5
```

### Course APIs

| Method | Endpoint | Description |
|---|---|---|
| POST | `/courses` | Create a course |
| GET | `/courses` | Get all courses |
| GET | `/courses/:id` | Get a course by ID |
| PUT | `/courses/:id` | Update a course |

Example request to create a course:

```json
{
  "course_name": "Programming Fundamentals",
  "course_code": "PROG101",
  "description": "Introduction to programming"
}
```

Search courses:

```text
GET /courses?search=Programming
```

Sort courses:

```text
GET /courses?sort=course_name&order=asc
```

Paginate courses:

```text
GET /courses?page=1&limit=5
```

### Enrollment APIs

| Method | Endpoint | Description |
|---|---|---|
| POST | `/enrollments` | Create an enrollment |
| GET | `/enrollments` | Get all enrollments |
| GET | `/enrollments/:id` | Get an enrollment by ID |
| PUT | `/enrollments/:id` | Update an enrollment |
| DELETE | `/enrollments/:id` | Delete an enrollment |

Example request to create an enrollment:

```json
{
  "student_id": 1,
  "course_id": 1,
  "enrollment_date": "2026-10-01"
}
```

Filter enrollments by student:

```text
GET /enrollments?student_id=1
```

Filter enrollments by course:

```text
GET /enrollments?course_id=1
```

Paginate enrollments:

```text
GET /enrollments?page=1&limit=5
```

## Validation and Error Handling

The API includes validation for required fields, email addresses, phone numbers, dates, course codes, and related student and course records.

It also handles duplicate email addresses, duplicate course codes, duplicate enrollments, invalid requests, missing resources, and database errors.

### HTTP Status Codes

| Status Code | Meaning |
|---|---|
| 200 | Request completed successfully |
| 201 | Resource created |
| 400 | Invalid request data |
| 404 | Resource not found |
| 409 | Duplicate or conflicting data |
| 500 | Internal server or database error |

## Security

The application uses parameterized SQL queries to help reduce SQL injection risks.

Example:

```javascript
await pool.execute(
  "SELECT * FROM students WHERE student_id = ?",
  [id]
);
```

Environment variables are used to configure database credentials and application settings.

## API Testing

Use Postman to test the API endpoints.

Recommended tests include:

- Creating, retrieving, updating, and deleting student records
- Creating and retrieving courses
- Managing student-course enrollments
- Searching, filtering, sorting, and pagination
- Input validation and duplicate-record handling
- Error responses and HTTP status codes

## Future Improvements

- Authentication and authorization
- Role-based access control
- Course deletion endpoint
- Swagger/OpenAPI documentation
- Automated API testing
- Student and course reports
- Dashboard
- Cloud deployment
- Docker support

## Conclusion

The Student Record Management API provides a modular backend for managing students, courses, and enrollments using Node.js, Express.js, and MySQL. It demonstrates REST API development, relational database integration, CRUD operations, validation, error handling, and data retrieval features.
