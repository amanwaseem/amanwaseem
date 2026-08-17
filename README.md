# Aman Ullah Waseem

4th-year Computer Science student focused on backend systems engineering. Most recently completed a two-month capstone project building an optical mark recognition (OMR) pipeline for automated exam grading.

---

### Projects

**OMR Exam Grading System** | Capstone (COSC 499), team of 6 | Private repository | Completed

A grading pipeline built for UBCO that processes scanned bubble sheets and produces released grades with minimal manual intervention. Instructors define exams with one or more variants and QR-coded metadata, generate and print bubble sheets, and scan completed sheets back into the system. The pipeline deskews and classifies scanned pages, reads student IDs and bubble marks, resolves exam variants, scores against the answer key, and flags low-confidence results for manual review. Reviewed results are released and synced to Canvas.

I owned the admin/telemetry and OMR pipeline layers of the system: 174 commits, accounting for approximately 16% of the codebase by surviving lines (second-largest contribution across 6 team members).

Key contributions:
- Designed and implemented the metrics and telemetry system, including periodic system snapshots, per-service resource probing (PostgreSQL, Redis, SeaweedFS), and the admin dashboards used to visualize this data
- Designed a swappable grading-engine interface (`GraderEngine` protocol) to decouple the OMR backend from a specific grading implementation
- Implemented variant detection and per-variant answer-key routing
- Implemented student ID resolution across multi-page, QR-based, and field-label sources
- Developed a marker-free skew-correction method using projection sharpness over Hough-detected bubble centroids, for sheets without fiducial markers
- Built analytics and export functionality, including class statistics, score distributions, and CSV export with formula-injection protection
- Implemented the notification system and course/section data model rules
- Approximately 45% of my contributed code consists of automated tests

**Technology stack:** FastAPI, SQLAlchemy (async), Alembic, Celery, arq, PostgreSQL, Redis, SeaweedFS, React, TypeScript, Vite, Docker Compose, OpenCV

---

**SnackOverflow** | Food delivery platform, university team project | [Repository](https://github.com/aliyanm564/SnackOverflow)

A layered FastAPI backend (domain, infrastructure, application, and presentation layers) supporting authentication, restaurant management, order processing, delivery tracking, payments, and reviews, with a Next.js frontend.

I implemented the orders and notifications module end to end, including the service layer, API routes, repository, and full test coverage:
- `OrderService`: order placement, cancellation, completion, filtering, and reordering, with notification dispatch on order events
- Notification system: read/unread state management, mark-all-as-read, deletion, with ownership validation
- Refactored error handling across 9 routers into a shared `handle_app_errors` decorator, removing repetitive exception-handling code (net reduction of 66 lines)

**Technology stack:** FastAPI, Pydantic v2, SQLAlchemy, JWT authentication, pytest, Docker

---

### Technical skills

Python, TypeScript, FastAPI, React, SQLAlchemy, PostgreSQL, Docker, Celery

### Contact

LinkedIn: [linkedin.com/in/amanullahwaseem](https://www.linkedin.com/in/amanullahwaseem/)
Email: amanullahwaseem2005@gmail.com
