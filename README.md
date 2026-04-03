# 📚 TutoringPal — Tutor Scheduling App

A full-stack web application built for **UF CEN3031 (Introduction to Software Engineering) — Summer 2025, Group #8**. TutoringPal connects students with tutors, allowing them to search for available tutors, book appointments, manage schedules, and leave ratings — all through a clean browser-based interface.

---

## ✨ Features

**For Students**
- Register and log in with a dedicated student account
- Search for tutors by name and subject
- Browse tutor profiles including their subjects, availability, and average rating
- Book 30-minute appointment slots within a tutor's available hours
- View and cancel upcoming appointments from the student dashboard
- Rate tutors and leave comments after sessions

**For Tutors**
- Register with subject specializations and availability windows
- View all booked sessions from the tutor dashboard
- Update availability hours at any time
- Cancel appointments when needed

**Shared**
- Secure session-based authentication
- Account settings (update name, delete account)
- Flash notifications for all key actions

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python, Flask |
| Forms & Validation | Flask-WTF, WTForms |
| Database | MongoDB Atlas (via PyMongo) |
| Frontend | HTML/CSS (Jinja2 templates) |
| Auth | Flask sessions |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- A [MongoDB Atlas](https://www.mongodb.com/atlas) account (or use the existing cluster connection in `db.py`)
- `pip` for package management

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/gonzaherman99/cen3031-group-project.git
cd cen3031-group-project

# 2. Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows

# 3. Install dependencies
pip install flask flask-wtf wtforms pymongo dnspython email-validator

# 4. Run the app
python main.py
```

Then open your browser and go to `http://127.0.0.1:5000`.

---

## 📁 Project Structure

```
cen3031-group-project/
├── main.py             # Flask app — all routes and form definitions
├── db.py               # MongoDB Atlas connection
├── UserCreator.py      # User registration logic (students & tutors)
├── UserLogin.py        # Authentication logic
├── Meetings.py         # Appointment creation and rating logic
├── Month.py            # Calendar/time utility helpers
├── Demos.py            # Demo/seed data helpers
├── templates/          # Jinja2 HTML templates
│   ├── index.html
│   ├── login.html
│   ├── register.html
│   ├── student_dashboard.html
│   ├── tutor_dashboard.html
│   ├── make_appointment.html
│   ├── search_results.html
│   ├── select_time.html
│   ├── tutor_profile.html
│   ├── rate_tutor.html
│   ├── settings.html
│   └── availability_settings.html
└── venv/               # Virtual environment (not committed)
```

---

## 🗺️ Route Overview

| Route | Method | Description |
|---|---|---|
| `/` | GET | Landing page |
| `/register` | GET, POST | Create a student or tutor account |
| `/login` | GET, POST | Log in |
| `/logout` | GET | End session |
| `/student_dashboard` | GET | View upcoming appointments (students) |
| `/tutor_dashboard` | GET | View booked sessions (tutors) |
| `/make_appointment` | GET, POST | Search tutors and book a session |
| `/select_time` | GET | Choose a 30-minute slot from tutor availability |
| `/tutor_profile/<email>` | GET | View a tutor's profile and ratings |
| `/rate_tutor` | GET, POST | Submit a rating and comment for a past session |
| `/cancel_appointment` | POST | Cancel a booked appointment |
| `/settings` | GET, POST | Update name or delete account |
| `/availability_settings` | GET, POST | Update tutor availability hours (tutors only) |

---

## 🗄️ Database Schema

The app uses a MongoDB database (`stjohn`) with two main collections:

**`users`**
```json
{
  "name": "string",
  "email": "string",
  "password": "hashed string",
  "role": "Student | Tutor",
  "subjects": ["string"],           // Tutors only
  "start_availability": "HH:MM",   // Tutors only
  "end_availability": "HH:MM"      // Tutors only
}
```

**`meetings`**
```json
{
  "tutorEmail": "string",
  "studentEmail": "string",
  "scheduledDate": "YYYY-MM-DD",
  "scheduledTime": "HH:MM",
  "subject": "string",
  "rating": "number",              // Set after session
  "comment": "string"             // Set after session
}
```

---

## 🔄 Booking Flow

```
Student logs in
    └─▶ Search for tutors by name/subject + date
            └─▶ Browse search results (with avg. ratings)
                    └─▶ Click a tutor → select a 30-min time slot
                            └─▶ Appointment saved to DB
                                    └─▶ Appears on both dashboards
```

Conflict detection prevents double-booking the same tutor at the same date and time. Availability is validated against the tutor's set hours before confirming a booking.

---

## 👥 Team

Built by **CEN3031 Group #8** — University of Florida, Summer 2025.  
Forked from [Mo-Sanchez/tutoring-pal](https://github.com/Mo-Sanchez/tutoring-pal).

---

## 📄 License

Open source — built for academic purposes as part of a software engineering course project.
