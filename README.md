# Aman Ullah Waseem

4th-year Computer Science student focused on backend systems engineering. Most recently completed a two-month capstone project building an optical mark recognition (OMR) pipeline for automated exam grading.

---

### Projects

**FPL Predictor** | Personal project, solo | [Repository](https://github.com/amanwaseem/fpl-predictor) | [Live site](https://fpl-predictor-aman.fly.dev) | Ongoing

Points predictions for every Fantasy Premier League player, committed to git before each gameweek deadline and scored against what actually happened. CI rejects any edit to a committed prediction, so the track record is public and falsifiable rather than a tuned historical holdout. A squad optimiser, public API and website sit on top of the log.

<details>
<summary>Full details</summary>

Every gameweek runs through an automated loop on GitHub Actions: snapshot the FPL API, have every model predict from that one snapshot, verify the entries, merge them through a self-merging PR before the deadline, then score them once the gameweek settles.

- Built an append-only prediction log with CI-enforced immutability: no committed entry can be rewritten, and a missed deadline stays missed
- Three logged models with fixed roles: a rolling-form baseline, a component model that predicts minutes, goals, assists, clean sheets, saves, defensive contributions and bonus separately, and a LightGBM challenger trained on ten past seasons (~254,000 player-fixture rows)
- A model is only logged if it beats the baseline on held-out past seasons; each is scored weekly by MAE and Spearman correlation against FPL's own `form` figure
- Squad optimiser formulated as an integer programme (HiGHS): maximises expected points under the £100m budget, formation and three-per-club rules, and transfer costs, over one gameweek or a plan of up to six
- Git is the source of truth: Postgres holds a projection of the log that CI rebuilds and checks against git on every PR
- FastAPI service with an OpenAPI contract fuzzed in CI by schemathesis, serving a React + TypeScript site with Playwright end-to-end tests
- Seven GitHub Actions workflows covering CI, deploys to Fly.io, daily ingest, the weekly entry, deadline alerts and uptime checks; design decisions recorded as ADRs

**Technology stack:** Python 3.13, LightGBM, HiGHS, FastAPI, SQLAlchemy, Alembic, PostgreSQL (Neon), React, TypeScript, Vite, Docker, Fly.io, GitHub Actions

</details>

---

**OMR Exam Grading System** | Capstone (COSC 499), team of 6 | Private repository | Completed

A grading pipeline built for UBCO that processes scanned bubble sheets and produces released grades with minimal manual intervention. I owned the admin/telemetry and OMR pipeline layers: 174 commits, approximately 16% of the codebase by surviving lines (second-largest contribution across 6 team members).

<details>
<summary>Full details</summary>

Instructors define exams with one or more variants and QR-coded metadata, generate and print bubble sheets, and scan completed sheets back into the system. The pipeline deskews and classifies scanned pages, reads student IDs and bubble marks, resolves exam variants, scores against the answer key, and flags low-confidence results for manual review. Reviewed results are released and synced to Canvas.

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

</details>

---

**SnackOverflow** | Food delivery platform, university team project | [Repository](https://github.com/aliyanm564/SnackOverflow)

Layered FastAPI backend with a Next.js frontend. I implemented the orders and notifications module end to end, including service layer, API routes, repository, and full test coverage.

<details>
<summary>Full details</summary>

A layered FastAPI backend (domain, infrastructure, application, and presentation layers) supporting authentication, restaurant management, order processing, delivery tracking, payments, and reviews, with a Next.js frontend.

- `OrderService`: order placement, cancellation, completion, filtering, and reordering, with notification dispatch on order events
- Notification system: read/unread state management, mark-all-as-read, deletion, with ownership validation
- Refactored error handling across 9 routers into a shared `handle_app_errors` decorator, removing repetitive exception-handling code (net reduction of 66 lines)

**Technology stack:** FastAPI, Pydantic v2, SQLAlchemy, JWT authentication, pytest, Docker

</details>

---

### Technical skills

Python, TypeScript, FastAPI, React, SQLAlchemy, PostgreSQL, Docker, Celery

### Contact

LinkedIn: [linkedin.com/in/amanullahwaseem](https://www.linkedin.com/in/amanullahwaseem/)
Email: amanullahwaseem2005@gmail.com
