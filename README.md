
# 🛠️ IT Project Management API (Backend Only)

This repository contains the backend component of the **IT Project Management System**, built using **ASP.NET Core Web API**, **Entity Framework Core**, and **SQL Server**. It supports role-based user management, project and task tracking, and secure authentication.

> 🔐 **Roles supported**: Administrator, Project Manager, Systems Analyst, Web Developer

---

## 📚 Features

### 🔑 Authentication & Authorization
- ASP.NET Identity-based registration and login.
- Role-based access:
  - **Administrator**: Manage users and assign roles.
  - **Project Manager**: Create projects and assign tasks.
  - **Systems Analyst & Web Developer**: View and update assigned tasks.

### 👥 Admin
- Add, update, delete users.
- Assign roles: `Project Manager`, `Systems Analyst`, `Web Developer`.

### 🗂️ Project Management
- Create and manage projects.
- Assign tasks to Systems Analysts and Web Developers.
- View employees by role or name.

### 📌 Task Management
- Task attributes: Title, Description, Status, Assignment Info, Timestamps.
- Status flow: `To Start` → `In Progress` → `Complete`.
- Task filtering by status.

---

## 🧱 Technology Stack

| Layer            | Technology               |
|------------------|--------------------------|
| Backend API      | ASP.NET Core Web API     |
| ORM              | Entity Framework Core    |
| Authentication   | ASP.NET Identity          |
| Database         | SQL Server               |
| Role Management  | Identity Roles            |

---

## 🧑‍💻 Models Overview

### `User`
```csharp
public class User: IdentityUser
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string JobTitle { get; set; }
    public DateTime CreatedAt { get; set; }
    public DateTime UpdatedAt { get; set; }

    public ICollection<Task> Tasks { get; set; }
    public ICollection<Project> ManagedProjects { get; set; }
}
```

### `Project`
```csharp
public class Project
{
    public int ProjectId { get; set; }
    public string ProjectName { get; set; }
    public string Description { get; set; }
    public string ProjectManagerId { get; set; }
    public User ProjectManager { get; set; }
    public ICollection<Task> Tasks { get; set; }
}
```

### `Task`
```csharp
public class Task
{
    public int TaskId { get; set; }
    public string Title { get; set; }
    public string Description { get; set; }
    public string AssignedToId { get; set; }
    public User AssignedTo { get; set; }
    public int ProjectId { get; set; }
    public Project Project { get; set; }
    public string Status { get; set; }
}
```

---

## 🔐 Role Access Summary

| Role              | Can Create Projects | Can Assign Tasks | Can View Tasks | Can Update Task Status | Can Manage Users |
|-------------------|---------------------|------------------|----------------|-------------------------|------------------|
| Administrator     | ❌                  | ❌               | ❌             | ❌                      | ✅               |
| Project Manager   | ✅                  | ✅               | ✅             | ❌                      | ❌               |
| Systems Analyst   | ❌                  | ❌               | ✅             | ✅                      | ❌               |
| Web Developer     | ❌                  | ❌               | ✅             | ✅                      | ❌               |

---

## 🧪 Sample API Endpoints (Swagger APIs)

- `POST /api/auth/login`
- `POST /api/auth/register`
- `GET /api/users`
- `POST /api/projects`
- `POST /api/tasks`
- `PUT /api/tasks/{id}/status`

> Swagger UI may be enabled for testing.

---

## ✍️ Author

- **Maselaelo Glen**
- Final-Year Software Engineering Student

---

**Contributions, suggestions, and forks are welcome.**
**⚠️Note: This code may contain Errors, Still Under Construction! 🏗️**

> Check the *fullstack repo* for UI implementation.
