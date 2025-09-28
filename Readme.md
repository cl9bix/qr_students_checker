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

## API Endpoints

### Teacher: Get Current QR
GET /teacher/sessions/{session_id}/qr

### Teacher: WebSocket Updates
WS /teacher/sessions/{session_id}/ws

### Student: Scan QR
POST /scan

### Student: View Attendance
GET /student/attendance/{student_id}

---

## Security
- One-time signed QR tokens (HMAC-SHA256)
- Expiration window (5–10 seconds)
- Immediate rotation after the first valid scan
- No personal data in QR payloads
- GDPR-compliant: only minimal identifiers stored

---

## MVP Roadmap
1. MVP: Teacher QR page + Student scan + DB records  
2. WebSocket auto-rotation & counter logic  
3. Student dashboard with statistics  
4. Export tools for teachers (CSV/PDF)  
5. Admin/faculty analytics panel  

---

## Testing Scenarios
- Multiple students scanning at the same second  
- QR screenshot forwarding → rejected as expired/used  
- Duplicate scan by the same student  
- Expired payload handling  
- Load test with 100+ scans in under 5 seconds  

