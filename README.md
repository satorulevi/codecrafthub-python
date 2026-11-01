# CodeCraftHub

CodeCraftHub is a beginner-friendly Python Flask REST API for tracking courses that developers want to learn.

The application allows users to create, view, update, and delete courses. Course data is stored in a local `courses.json` file instead of a database, making the project simple to understand while learning REST API concepts.

> This project uses **Python and Flask**. It is not the JavaScript or Express version.

---

## Features

- Create new courses
- Retrieve all courses
- Retrieve one course by ID
- Update an existing course
- Delete a course
- Automatically generate course IDs
- Automatically record course creation timestamps
- Validate required fields
- Validate target dates
- Validate course status values
- Store course data in a JSON text file
- Automatically create `courses.json` if it does not exist
- Return JSON responses and appropriate HTTP status codes
- Provide JSON error responses for invalid requests

---

## Technologies Used

- Python 3
- Flask
- JSON file storage
- PowerShell or `curl.exe` for API testing
- Visual Studio Code

---

## Project Structure

The project can use the following structure:

```text
CodeCraftHub/
├── app.py
├── courses.json
├── requirements.txt
└── README.md
```

### `app.py`

The main Flask application. It contains:

- Flask configuration
- API routes
- Course validation
- JSON file reading and writing
- Error handling
- CRUD operations

### `courses.json`

The local file used to store courses.

The Flask application creates this file automatically if it does not exist.

An empty file contains:

```json
[]
```

After courses are added, it contains course objects similar to:

```json
[
  {
    "id": 1,
    "name": "Python Basics",
    "description": "Learn Python fundamentals.",
    "target_date": "2026-12-31",
    "status": "Not Started",
    "created_at": "2026-11-01T12:00:00.000000Z"
  }
]
```

### `requirements.txt`

This file should be created in the project directory if it does not already exist.

Its contents should be:

```text
Flask
```

Install the dependency with:

```powershell
pip install -r requirements.txt
```

### `README.md`

This documentation file explains how to install, run, use, and test the API.

---

## Prerequisites

Before starting, install the following:

1. Python 3
2. Visual Studio Code
3. The Visual Studio Code Python extension
4. PowerShell, which is included with Windows

You can download Python from:

<https://www.python.org/downloads/>

During Python installation, enable:

```text
Add Python to PATH
```

This option allows Python and pip to be used from the Visual Studio Code terminal.

---

## Installation on Windows

### 1. Create or open the project folder

Create a folder named `CodeCraftHub`, for example:

```text
C:\Users\YourName\CodeCraftHub
```

Open the folder in Visual Studio Code.

You can also open it from PowerShell:

```powershell
mkdir CodeCraftHub
cd CodeCraftHub
code .
```

If the `code` command is not available, open Visual Studio Code manually and select:

```text
File > Open Folder
```

---

### 2. Open the Visual Studio Code terminal

In Visual Studio Code, select:

```text
Terminal > New Terminal
```

Make sure the terminal is opened in the project folder.

Check the current folder with:

```powershell
Get-Location
```

---

### 3. Check that Python is installed

Run:

```powershell
python --version
```

Example output:

```text
Python 3.12.5
```

You can also check pip:

```powershell
python -m pip --version
```

---

### 4. Create a virtual environment

A virtual environment keeps this project's Python packages separate from other projects.

Run:

```powershell
python -m venv venv
```

This creates a folder named `venv`.

The project will now look similar to:

```text
CodeCraftHub/
├── venv/
├── app.py
├── courses.json
├── requirements.txt
└── README.md
```

The `venv` folder should normally not be committed to Git.

---

### 5. Activate the virtual environment

In PowerShell, run:

```powershell
.\venv\Scripts\Activate.ps1
```

After activation, the terminal usually displays `(venv)` at the beginning of the prompt:

```text
(venv) PS C:\Users\YourName\CodeCraftHub>
```

---

### 6. If PowerShell blocks activation

You may see an error about script execution being disabled.

Open PowerShell as your normal user and run:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Confirm the change if prompted, then try activation again:

```powershell
.\venv\Scripts\Activate.ps1
```

Alternatively, activate the environment using the Command Prompt script:

```powershell
.\venv\Scripts\activate.bat
```

---

### 7. Create `requirements.txt`

If the file does not already exist, create a file named `requirements.txt` with this content:

```text
Flask
```

Install Flask:

```powershell
pip install -r requirements.txt
```

You can verify that Flask is installed with:

```powershell
pip show Flask
```

---

## Running the Application

Make sure the virtual environment is active:

```powershell
.\venv\Scripts\Activate.ps1
```

Start the Flask application:

```powershell
python app.py
```

The application runs on:

```text
http://localhost:5000
```

You may also see:

```text
http://127.0.0.1:5000
```

These addresses refer to the local computer.

The application automatically creates `courses.json` if it does not exist.

Keep the terminal running while testing the API.

To stop the Flask application, press:

```text
Ctrl+C
```

---

## API Overview

The API base URL is:

```text
http://localhost:5000/api/courses
```

|
 HTTP Method 
|
 Endpoint 
|
 Description 
|
 Success Status 
|
|
---
|
---
|
---
|
---
|
|
`POST`
|
`/api/courses`
|
 Create a course 
|
`201 Created`
|
|
`GET`
|
`/api/courses`
|
 Get all courses 
|
`200 OK`
|
|
`GET`
|
`/api/courses/<id>`
|
 Get one course 
|
`200 OK`
|
|
`PUT`
|
`/api/courses/<id>`
|
 Update a course 
|
`200 OK`
|
|
`DELETE`
|
`/api/courses/<id>`
|
 Delete a course 
|
`200 OK`
|

All request and response bodies use JSON.

---

## Course Fields

Each course contains the following fields:

|
 Field 
|
 Required from Client? 
|
 Description 
|
|
---
|
---:
|
---
|
|
`id`
|
 No 
|
 Automatically generated integer ID 
|
|
`name`
|
 Yes 
|
 Course name 
|
|
`description`
|
 Yes 
|
 Description of the course 
|
|
`target_date`
|
 Yes 
|
 Target completion date in 
`YYYY-MM-DD`
 format 
|
|
`status`
|
 Yes 
|
 Current learning status 
|
|
`created_at`
|
 No 
|
 Automatically generated UTC timestamp 
|

The client must provide:

```json
{
  "name": "Python Basics",
  "description": "Learn Python fundamentals.",
  "target_date": "2026-12-31",
  "status": "Not Started"
}
```

The client should not provide `id` or `created_at`. These values are generated by the server.

---

## Valid Status Values

The `status` field must be exactly one of these values:

```text
Not Started
In Progress
Completed
```

Status values are case-sensitive.

This is valid:

```json
{
  "status": "In Progress"
}
```

This is invalid:

```json
{
  "status": "in progress"
}
```

---

# API Documentation

## 1. Create a Course

### Request

```text
POST /api/courses
```

### Example JSON request

```json
{
  "name": "Python Basics",
  "description": "Learn Python fundamentals.",
  "target_date": "2026-12-31",
  "status": "Not Started"
}
```

### PowerShell command using `curl.exe`

```powershell
curl.exe -X POST "http://localhost:5000/api/courses" `
  -H "Content-Type: application/json" `
  -d '{"name":"Python Basics","description":"Learn Python fundamentals.","target_date":"2026-12-31","status":"Not Started"}'
```

The backtick character `` ` `` continues a PowerShell command onto the next line.

### Expected status

```text
201 Created
```

### Example JSON response

The `id` and `created_at` values are generated by the application.

```json
{
  "id": 1,
  "name": "Python Basics",
  "description": "Learn Python fundamentals.",
  "target_date": "2026-12-31",
  "status": "Not Started",
  "created_at": "2026-11-01T12:00:00.000000Z"
}
```

The actual timestamp will be different when you run the request.

---

### Create a Course Using `Invoke-RestMethod`

```powershell
$courseBody = @{
    name = "Python Basics"
    description = "Learn Python fundamentals."
    target_date = "2026-12-31"
    status = "Not Started"
} | ConvertTo-Json

$createdCourse = Invoke-RestMethod `
    -Uri "http://localhost:5000/api/courses" `
    -Method Post `
    -ContentType "application/json" `
    -Body $courseBody

$createdCourse | ConvertTo-Json -Depth 5
```

To store the generated ID in a PowerShell variable:

```powershell
$courseId = $createdCourse.id
Write-Host "Created course ID: $courseId"
```

---

## 2. Get All Courses

### Request

```text
GET /api/courses
```

### PowerShell command

```powershell
curl.exe -X GET "http://localhost:5000/api/courses"
```

### Expected status

```text
200 OK
```

### Example response

```json
[
  {
    "id": 1,
    "name": "Python Basics",
    "description": "Learn Python fundamentals.",
    "target_date": "2026-12-31",
    "status": "Not Started",
    "created_at": "2026-11-01T12:00:00.000000Z"
  }
]
```

If no courses exist, the response is:

```json
[]
```

### Using `Invoke-RestMethod`

```powershell
$courses = Invoke-RestMethod `
    -Uri "http://localhost:5000/api/courses" `
    -Method Get

$courses | ConvertTo-Json -Depth 5
```

---

## 3. Get a Specific Course

Replace `1` with the ID of the course you want to retrieve.

### Request

```text
GET /api/courses/1
```

### PowerShell command

```powershell
curl.exe -X GET "http://localhost:5000/api/courses/1"
```

### Expected status

```text
200 OK
```

### Example response

```json
{
  "id": 1,
  "name": "Python Basics",
  "description": "Learn Python fundamentals.",
  "target_date": "2026-12-31",
  "status": "Not Started",
  "created_at": "2026-11-01T12:00:00.000000Z"
}
```

---

## 4. Update a Course

The `PUT` endpoint updates an existing course.

The current implementation expects all editable fields in the request:

- `name`
- `description`
- `target_date`
- `status`

The existing `id` and `created_at` values are preserved.

### Request

```text
PUT /api/courses/1
```

### Example JSON request

```json
{
  "name": "Python and Flask Basics",
  "description": "Learn Python fundamentals and create a Flask REST API.",
  "target_date": "2026-11-30",
  "status": "In Progress"
}
```

### PowerShell command using `curl.exe`

```powershell
curl.exe -X PUT "http://localhost:5000/api/courses/1" `
  -H "Content-Type: application/json" `
  -d '{"name":"Python and Flask Basics","description":"Learn Python fundamentals and create a Flask REST API.","target_date":"2026-11-30","status":"In Progress"}'
```

### Expected status

```text
200 OK
```

### Example response

```json
{
  "id": 1,
  "name": "Python and Flask Basics",
  "description": "Learn Python fundamentals and create a Flask REST API.",
  "target_date": "2026-11-30",
  "status": "In Progress",
  "created_at": "2026-11-01T12:00:00.000000Z"
}
```

The `id` and `created_at` values should remain unchanged.

---

### Update a Course Using `Invoke-RestMethod`

```powershell
$updateBody = @{
    name = "Python and Flask Basics"
    description = "Learn Python fundamentals and create a Flask REST API."
    target_date = "2026-11-30"
    status = "In Progress"
} | ConvertTo-Json

$updatedCourse = Invoke-RestMethod `
    -Uri "http://localhost:5000/api/courses/1" `
    -Method Put `
    -ContentType "application/json" `
    -Body $updateBody

$updatedCourse | ConvertTo-Json -Depth 5
```

---

## 5. Delete a Course

Replace `1` with the course ID to delete.

### Request

```text
DELETE /api/courses/1
```

### PowerShell command

```powershell
curl.exe -X DELETE "http://localhost:5000/api/courses/1"
```

### Expected status

```text
200 OK
```

### Example response

```json
{
  "message": "Course deleted successfully.",
  "course": {
    "id": 1,
    "name": "Python and Flask Basics",
    "description": "Learn Python fundamentals and create a Flask REST API.",
    "target_date": "2026-11-30",
    "status": "In Progress",
    "created_at": "2026-11-01T12:00:00.000000Z"
  }
}
```

---

# Error Handling

The API returns JSON error messages instead of HTML error pages.

## Common HTTP status codes

|
 Status Code 
|
 Meaning 
|
|
---
|
---
|
|
`200 OK`
|
 Request completed successfully 
|
|
`201 Created`
|
 A new course was created 
|
|
`400 Bad Request`
|
 The request contains invalid or missing data 
|
|
`404 Not Found`
|
 The course or endpoint was not found 
|
|
`405 Method Not Allowed`
|
 The HTTP method is not supported 
|
|
`500 Internal Server Error`
|
 A file storage error occurred 
|

---

## Missing Required Field

This request is missing `description`:

```powershell
curl.exe -X POST "http://localhost:5000/api/courses" `
  -H "Content-Type: application/json" `
  -d '{"name":"Incomplete Course","target_date":"2026-12-31","status":"Not Started"}'
```

Expected status:

```text
400 Bad Request
```

Expected response:

```json
{
  "error": "Missing required field: description"
}
```

The required fields are:

- `name`
- `description`
- `target_date`
- `status`

---

## Invalid Status

```powershell
curl.exe -X POST "http://localhost:5000/api/courses" `
  -H "Content-Type: application/json" `
  -d '{"name":"Invalid Status Course","description":"Testing an invalid status.","target_date":"2026-12-31","status":"Started"}'
```

Expected status:

```text
400 Bad Request
```

Expected response:

```json
{
  "error": "Invalid status. Status must be one of: Not Started, In Progress, Completed."
}
```

---

## Invalid Target Date Format

The date must use the format:

```text
YYYY-MM-DD
```

This example uses an invalid format:

```powershell
curl.exe -X POST "http://localhost:5000/api/courses" `
  -H "Content-Type: application/json" `
  -d '{"name":"Invalid Date Course","description":"Testing an invalid date format.","target_date":"12-31-2026","status":"Not Started"}'
```

Expected status:

```text
400 Bad Request
```

Expected response:

```json
{
  "error": "target_date must use YYYY-MM-DD format."
}
```

---

## Invalid Calendar Date

This date has the correct format but is not a valid calendar date:

```powershell
curl.exe -X POST "http://localhost:5000/api/courses" `
  -H "Content-Type: application/json" `
  -d '{"name":"Impossible Date Course","description":"Testing an impossible date.","target_date":"2026-02-30","status":"Not Started"}'
```

Expected response:

```json
{
  "error": "target_date must be a valid date in YYYY-MM-DD format."
}
```

---

## Course Not Found

Use an ID that does not exist, such as `9999`.

### Get a nonexistent course

```powershell
curl.exe -X GET "http://localhost:5000/api/courses/9999"
```

Expected status:

```text
404 Not Found
```

Expected response:

```json
{
  "error": "Course with ID 9999 was not found."
}
```

### Update a nonexistent course

```powershell
curl.exe -X PUT "http://localhost:5000/api/courses/9999" `
  -H "Content-Type: application/json" `
  -d '{"name":"Missing Course","description":"This course does not exist.","target_date":"2026-12-31","status":"In Progress"}'
```

Expected status:

```text
404 Not Found
```

### Delete a nonexistent course

```powershell
curl.exe -X DELETE "http://localhost:5000/api/courses/9999"
```

Expected status:

```text
404 Not Found
```

---

## Invalid JSON

This request contains malformed JSON:

```powershell
curl.exe -X POST "http://localhost:5000/api/courses" `
  -H "Content-Type: application/json" `
  -d '{invalid json}'
```

Expected status:

```text
400 Bad Request
```

Expected response:

```json
{
  "error": "Request body must contain valid JSON."
}
```

---

## Empty Required Field

This request has an empty course name:

```powershell
curl.exe -X POST "http://localhost:5000/api/courses" `
  -H "Content-Type: application/json" `
  -d '{"name":"","description":"A course with an empty name.","target_date":"2026-12-31","status":"Not Started"}'
```

Expected response:

```json
{
  "error": "Field 'name' must be a non-empty string."
}
```

---

# Recommended Testing Order

Run the following tests in order:

1. Start Flask:

   ```powershell
   python app.py
   ```

2. Create a course with `POST`.

3. Get all courses with:

   ```text
   GET /api/courses
   ```

4. Get the created course by ID.

5. Update the course with `PUT`.

6. Inspect `courses.json`.

7. Delete the course.

8. Get all courses again and confirm that the deleted course is no longer present.

9. Test the error cases using invalid data and ID `9999`.

---

# Verifying Data in `courses.json`

The file is stored in the same directory as `app.py`.

Display its contents in PowerShell:

```powershell
Get-Content .\courses.json
```

To display formatted JSON:

```powershell
Get-Content .\courses.json -Raw |
    ConvertFrom-Json |
    ConvertTo-Json -Depth 5
```

You can open the file in Visual Studio Code with:

```powershell
code .\courses.json
```

After creating a course, the file should contain a JSON array similar to:

```json
[
  {
    "id": 1,
    "name": "Python Basics",
    "description": "Learn Python fundamentals.",
    "target_date": "2026-12-31",
    "status": "Not Started",
    "created_at": "2026-11-01T12:00:00.000000Z"
  }
]
```

After deleting the only course, the file should contain:

```json
[]
```

---

# Troubleshooting

## Python is not recognized

### Problem

You run:

```powershell
python --version
```

But Windows reports that Python is not recognized.

### Solutions

1. Confirm that Python is installed.
2. Reinstall Python from:

   <https://www.python.org/downloads/>
3. During installation, enable:

   ```text
   Add Python to PATH
   ```

4. Restart Visual Studio Code.
5. Try the Python launcher:

   ```powershell
   py --version
   ```

If `py` works but `python` does not, you can create the virtual environment with:

```powershell
py -m venv venv
```

---

## Flask module is missing

### Problem

You see an error similar to:

```text
ModuleNotFoundError: No module named 'flask'
```

### Solution

Activate the virtual environment:

```powershell
.\venv\Scripts\Activate.ps1
```

Install Flask:

```powershell
python -m pip install Flask
```

Or install all dependencies from `requirements.txt`:

```powershell
python -m pip install -r requirements.txt
```

Then run:

```powershell
python app.py
```

---

## Virtual environment will not activate

Try:

```powershell
.\venv\Scripts\Activate.ps1
```

If PowerShell reports that script execution is disabled, run:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Then activate the environment again.

You can also use:

```powershell
.\venv\Scripts\activate.bat
```

A successful activation normally adds `(venv)` to the terminal prompt.

---

## Port 5000 is already in use

### Problem

Flask cannot start because another application is using port `5000`.

### Solutions

1. Stop the other application using port `5000`.
2. Close another running Flask process.
3. Restart Visual Studio Code's terminal.
4. Check for processes using the port:

   ```powershell
   netstat -ano | findstr :5000
   ```

The existing application uses port `5000`. The API commands in this README assume:

```text
http://localhost:5000
```

If you change the port in `app.py`, update all API URLs in your test commands accordingly.

---

## Invalid JSON errors

### Problem

The API returns:

```json
{
  "error": "Request body must contain valid JSON."
}
```

### Solutions

Check the following:

- Use double quotes around JSON property names.
- Use double quotes around JSON string values.
- Do not add a comma after the final property.
- Include the header:

  ```text
  Content-Type: application/json
  ```

Correct JSON:

```json
{
  "name": "Python Basics",
  "description": "Learn Python fundamentals.",
  "target_date": "2026-12-31",
  "status": "Not Started"
}
```

Incorrect JSON:

```json
{
  name: "Python Basics",
  description: "Learn Python fundamentals",
}
```

When using PowerShell, the following format is recommended:

```powershell
-d '{"name":"Python Basics","description":"Learn Python fundamentals.","target_date":"2026-12-31","status":"Not Started"}'
```

---

## The API returns an empty list

If this command returns:

```json
[]
```

```powershell
curl.exe -X GET "http://localhost:5000/api/courses"
```

Then no courses have been created yet, or all courses have been deleted.

Create a course using the `POST` command and try again.

---

## The JSON file cannot be read or written

The application returns a `500` response when it cannot create, read, or write `courses.json`.

Check that:

- The project folder exists.
- `courses.json` is not open with a lock that prevents writing.
- You have permission to modify the project folder.
- `courses.json` contains valid JSON.
- The file starts with an array, such as:

  ```json
  []
  ```

If the file was accidentally corrupted, make a backup and replace its contents with:

```json
[]
```

---

# Learning REST API Concepts

This project demonstrates the basic relationship between HTTP methods and CRUD operations:

|
 CRUD Operation 
|
 HTTP Method 
|
 API Endpoint 
|
|
---
|
---
|
---
|
|
 Create 
|
`POST`
|
`/api/courses`
|
|
 Read all 
|
`GET`
|
`/api/courses`
|
|
 Read one 
|
`GET`
|
`/api/courses/<id>`
|
|
 Update 
|
`PUT`
|
`/api/courses/<id>`
|
|
 Delete 
|
`DELETE`
|
`/api/courses/<id>`
|

The API receives JSON requests, performs an operation, and returns a JSON response with an HTTP status code.

For example:

- `POST` sends course data to the server.
- `GET` requests course data.
- `PUT` replaces the editable data for an existing course.
- `DELETE` removes a course.
- `404` indicates that a requested course does not exist.
- `400` indicates invalid client input.

---

# Limitations

This project intentionally uses a JSON file instead of a database.

That makes it useful for learning, but it also has limitations:

- It is intended for local development and learning.
- It is not designed for many simultaneous users.
- File writes could conflict if multiple requests occur at the same time.
- There is no authentication or user management.
- All courses are stored together in one file.
- There is no frontend interface included.

A database and authentication system could be added later if the project grows.

---

# License

This project is intended for learning and educational use.