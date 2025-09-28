# Student Attendance Tracking System (QR-based)

A system for tracking university student attendance using dynamic one-time QR codes.  
Developed as a startup project for Pannon Egyetem.

---

## Project Overview
This system allows teachers to generate rotating QR codes during each class session.  
Students scan the QR with their mobile devices to confirm attendance.  

Key features:
- One-time QR codes (expire within seconds, automatically rotated).  
- Teacher panel: live QR display, attendance list, export.  
- Student app/web: scan QR → instant confirmation.  
- Secure: signed tokens (HMAC), SSO login, GDPR-compliant.  
- Analytics: attendance reports for teachers & faculty.  

---

## Tech Stack
- Backend: Python (FastAPI / Django REST)  
- Database: PostgreSQL  
- Cache & Realtime: Redis (counters, pub/sub, locks)  
- Frontend: React / Next.js  
- Authentication: University SSO / OAuth2 / JWT  
- Deployment: Docker + Nginx  

---

## Database Schema

```mermaid
erDiagram
    USERS {
        uuid id PK
        string name
        string email
        string uni_id
    }

    SESSIONS {
        uuid id PK
        uuid course_id
        uuid room_id
        timestamp starts_at
        timestamp ends_at
        uuid created_by FK -> USERS.id
    }

    ATTENDANCE {
        uuid id PK
        uuid session_id FK -> SESSIONS.id
        uuid student_id FK -> USERS.id
        timestamp scanned_at
        int counter
        string ip
        string device_fp
        string status  // ok, expired, duplicate, invalid
    }

    USERS ||--o{ ATTENDANCE : "has"
    SESSIONS ||--o{ ATTENDANCE : "records"
```

