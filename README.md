# University Exam System

A desktop Java application for managing university exams, grading, and user administration. Lecturers create and publish exams, students take them and submit feedback, and administrators oversee users and results.

## Features

### Students
- Take published exams and receive automatic grading
- View exam details and results once published
- Request re-correction with justification
- Submit feedback on completed exams

### Lecturers
- Create exams with multiple question types
- Publish exams for student access
- Publish exam results
- Manage assigned subjects

### Administrators
- Manage all user accounts (create, update, delete)
- Search and list users
- Assign subjects to lecturers
- Control exam and results publication

## Running It

You can run the pre-compiled jar directly if you have Java installed:

```bash
java -jar UniSystem.jar
```

If you want to build it from source yourself:

```bash
javac -d out $(find src -name "*.java")
jar cfe UniSystem.jar Main -C out .
java -jar UniSystem.jar
```

## Prerequisites

JDK 21 or higher to build and run.

## Default Account

On startup, the application seeds a default admin account:

| Username | Password | Role |
|----------|----------|------|
| `admin` | `admin123` | Administrator |

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Language | Java 21 |
| UI | Swing |
| Persistence | Native Java Object Serialization |
| Dependencies | None — fully self-contained |

## Architecture

```
src/
├── Main.java                  # Entry point
├── exception/                 # Custom exceptions
├── models/
│   ├── academic/              # Exam, Question models
│   └── users/                 # User, Student, Lecturer, Admin
├── services/
│   ├── interfaces/            # Service contracts
│   └── impl/                  # Service implementations
├── storage/
│   └── DataManager.java       # Singleton data persistence
└── views/
    ├── auth/                  # Login UI
    ├── admin/                 # Admin dashboard
    ├── lecturer/              # Lecturer dashboard
    └── student/               # Student dashboard + exam UI
```

## Data Storage

All application state is saved locally to a `university_data.ser` file in the working directory. To reset the system, delete this file and restart.

> **Note:** This serialization approach works for a single-user desktop app, but concurrency is not supported. If you modify domain models without managing `serialVersionUID`, the data file will become unreadable — delete it and start fresh.

## Academic Context

Developed as a course project for **Analysis and Design of Information Systems 1 (IS3-51)**.

## License

This project is licensed under the [GNU General Public License v3.0](LICENSE).