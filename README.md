**VIT BHOPAL UNIVERSITY**
**Course Faculty Name: Sasmita Padhy**
**Slot: A11+A12+A13+D11+D12+A14**
**Name: Nikita Bhardwaj**
**Registration Number: 26MIM10044**

# Student Result & Grade Management System

## Overview
A command-line application for managing student academic records. Admins
can add students, enter/update subject marks, and view class-wide reports.
Students can log in to view only their own results. Built as a Python
fundamentals course project — no external database or GUI framework; all
data is held in memory for the session.

## Features
- **Role-based login** — separate Admin and Student login flows
- **Admin menu**
  - Add new students
  - Enter/update marks per subject (with input validation)
  - Delete student records
  - View all students in a formatted table with percentage, grade, and status
  - View class average and topper
- **Student menu**
  - View own subject-wise marks
  - View total, percentage, grade, and pass/fail status
- **Automatic grade computation** — percentage, letter grade (A+ to F), and
  pass/fail status computed from raw scores

## Technologies / Tools Used
- Python 3
- Standard library only — no third-party dependencies

## Project Structure
```
student_result_system/
├── main.py                  # Entry point — CLI loop
├── models/
│   ├── person.py            # Base class (Person)
│   ├── student.py           # Student (inherits Person)
│   ├── admin.py              # Admin (inherits Person)
│   └── result.py             # Mark, Result (grade computation)
├── core/
│   └── school_system.py      # In-memory data manager (CRUD, auth, stats)
├── cli/
│   ├── login.py               # Login flow / role selection
│   ├── admin_menu.py          # Admin text menu
│   └── student_menu.py        # Student text menu
└── README.md
```

## Steps to Install & Run
1. Ensure Python 3.8+ is installed.
2. Clone/download this repository.
3. From the project root, run:
   ```bash
   python main.py
   ```
4. Follow the on-screen numbered menu prompts.

## Demo Logins (seeded data)
| Role    | ID     | Password  |
|---------|--------|-----------|
| Admin   | admin1 | admin123  |
| Student | S001   | pass123   |
| Student | S002   | pass123   |

## Instructions for Testing
- Core grading logic can be sanity-checked without the GUI:
  ```bash
  python -c "
  from core.school_system import SchoolSystem
  s = SchoolSystem()
  print(s.get_student('S001').get_result().as_dict())
  "
  ```
- Manual CLI test checklist:
  1. Run `python main.py`, log in as admin, add a new student, add marks, confirm they appear via "View All Students".
  2. Enter an invalid score (e.g. negative or above max) — confirm an error message appears and nothing is saved.
  3. Logout, log in as that new student, confirm only their own result is visible via "View My Result".
  4. Delete a student as admin, confirm they disappear from the list and class average updates.

## Non-Functional Requirements Addressed
- **Usability** — guided, minimal GUI with clear labeled sections
- **Reliability** — input validation prevents invalid marks/empty fields from being saved
- **Maintainability** — logic (models/core) is fully separated from GUI code
- **Error handling** — try/except and validation around all numeric input and login attempts

## Future Enhancements
- Persist data to JSON/CSV or SQLite between runs
- Password hashing instead of plaintext comparison
- Export individual result as PDF
- Support subject credits and CGPA calculation
