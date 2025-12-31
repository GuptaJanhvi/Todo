cd ~/Desktop/todo_project
cat > README.md << 'EOF'
# 📝 To-Do List Application

A modern, full-featured To-Do List web application built with Django, featuring both a beautiful web interface and a RESTful API.

![To-Do List App](https://img.shields.io/badge/Built%20with-Django-green)
![Python](https://img.shields.io/badge/Python-3.11-blue)
![License](https://img.shields.io/badge/License-MIT-yellow)

## ✨ Features

- ✅ **Modern UI** - Clean, responsive interface with Tailwind CSS
- ✅ **Full CRUD Operations** - Create, Read, Update, Delete tasks
- ✅ **RESTful API** - Complete API for programmatic access
- ✅ **Advanced Search** - Search tasks by title or description
- ✅ **Status Filtering** - Filter by task status
- ✅ **Statistics Dashboard** - Real-time task statistics
- ✅ **Due Date Management** - Set and track task deadlines
- ✅ **Responsive Design** - Works on mobile, tablet, and desktop
- ✅ **Comprehensive Testing** - Full test suite with 90%+ coverage

## 📋 Table of Contents

- [Quick Start](#quick-start)
- [Installation](#installation)
- [Usage](#usage)
- [API Documentation](#api-documentation)
- [Testing](#testing)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

## 🚀 Quick Start

### Prerequisites
- Python 3.8+
- pip (Python package manager)

### Installation & Setup

```bash
# 1. Clone or create project directory
cd ~/Desktop
mkdir todo_project
cd todo_project

# 2. Create and activate virtual environment
python3 -m venv venv
source venv/bin/activate

# 3. Install dependencies
pip install django djangorestframework

# 4. Create Django project
django-admin startproject todo_project .
python manage.py startapp todo_app

# 5. Apply the code from this repository
# (Copy all the provided files to their respective locations)

# 6. Apply database migrations
python manage.py makemigrations
python manage.py migrate

# 7. Create superuser (optional, for admin panel)
python manage.py createsuperuser

# 8. Run the development server
python manage.py runserver



##🌐 Access the Application
Web Interface: http://127.0.0.1:8000

Admin Panel: http://127.0.0.1:8000/admin

API Endpoint: http://127.0.0.1:8000/api/tasks/

API Statistics: http://127.0.0.1:8000/api/tasks/stats/

🖥️ Usage Guide
Web Interface
1. Viewing Tasks
Visit the homepage to see all your tasks

Use the search bar to find specific tasks

Filter by status using the dropdown

View real-time statistics in the dashboard

2. Creating Tasks
Click "Add New Task" button

Fill in task details:

Title (required)

Description (optional)

Due Date (optional)

Status (default: Pending)

Click "Create Task"

3. Updating Tasks
Click on any task card

Modify the task details

Click "Update Task"

4. Deleting Tasks
Click the trash icon (🗑️) on any task

Confirm deletion when prompted

Keyboard Shortcuts
Enter in search box: Apply search filter

Click task: Edit task

Cancel button: Go back to task list


# 📚 API Documentation

## Base URL - http://localhost:8000/api/


### Authentication
No authentication required for this demo application.

# Endpoints

# 1. Get All Tasks
GET /api/tasks/
Example 
curl "http://localhost:8000/api/tasks/?search=important&status=pending"
Response - 
[
  {
    "id": 1,
    "title": "Important Meeting",
    "description": "Prepare presentation for clients",
    "due_date": "2024-12-31",
    "status": "pending",
    "created_at": "2024-01-15T10:30:00Z"
  }
]

2. Create New Task
POST /api/tasks/
{
  "title": "New Task",
  "description": "Task description (optional)",
  "due_date": "2024-12-31",
  "status": "pending"
}
Field Requirements:

title: Required, max 200 characters

description: Optional

due_date: Optional, format: YYYY-MM-DD

status: Optional, defaults to "pending"

Example Request:
curl -X POST http://localhost:8000/api/tasks/ \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Complete Project",
    "description": "Finish the Django project",
    "due_date": "2024-12-31",
    "status": "in_progress"
  }'

Response (201 Created):
{
  "id": 2,
  "message": "Task created successfully"
}

3. Get Single Task
GET /api/tasks/{id}/
Example Request:
curl http://localhost:8000/api/tasks/1/
Response (200):
{
  "id": 1,
  "title": "Important Meeting",
  "description": "Prepare presentation for clients",
  "due_date": "2024-12-31",
  "status": "pending",
  "created_at": "2024-01-15T10:30:00Z"
}
Error Response (404 Not Found):
{
  "error": "Task not found"
}
4. Update Task
http
PUT /api/tasks/{id}/
Path Parameters:

Parameter	Type	Required	Description
id	integer	Yes	Task ID
Request Body:

json
{
  "title": "Updated Task Title",
  "status": "completed"
}
Note: All fields are optional for updates.

Example Request:
curl -X PUT http://localhost:8000/api/tasks/1/ \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Meeting Completed",
    "status": "completed"
  }'
Response (200 OK):

json
{
  "message": "Task updated successfully"
}


5. Delete Task
http
DELETE /api/tasks/{id}/
Path Parameters:

Parameter	Type	Required	Description
id	integer	Yes	Task ID
Example Request:
curl -X DELETE http://localhost:8000/api/tasks/1/
Response (200 OK):
json
{
  "message": "Task deleted successfully"
}

6. Get Statistics
GET /api/tasks/stats/
Example Request:
curl http://localhost:8000/api/tasks/stats/
Response (200 OK):
{
  "total": 10,
  "completed": 4,
  "pending": 3,
  "in_progress": 3,
  "completion_rate": 40.0
}