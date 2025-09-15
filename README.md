
# 🎓 MaBourse — Scholarship Portal (Demo Showcase)

![Status](https://img.shields.io/badge/status-production-brightgreen.svg) ![Security](https://img.shields.io/badge/security-A%2B-brightgreen.svg) ![Systems](https://img.shields.io/badge/systems-all%20green-brightgreen.svg) ![Demo](https://img.shields.io/badge/demo-9%20min-blue.svg) ![Code](https://img.shields.io/badge/code-private-orange.svg)

> **Public showcase repository** for the *MaBourse Scholarship Portal*.
> The **source code is private** for security and IP reasons. This repository contains a 9-minute demo video and full documentation describing the architecture, security, production readiness, and technical journey to build a production-grade system.
> Source code is available **only upon request** for academic or professional review (see [How to request access](#how-to-verify--request-code-access)).

---

## Table of Contents

* [Overview](#overview)
* [Demo (9 minutes)](#demo-9-minutes)
* [Why this project matters](#why-this-project-matters)
* [Highlights & Achievements](#highlights--achievements)
* [Key Features](#key-features)
* [Technical architecture](#technical-architecture)
* [Database & schema overview](#database--schema-overview)
* [Security & compliance](#security--compliance)
* [Production readiness & performance](#production-readiness--performance)
* [Challenges, remediation & lessons learned](#challenges-remediation--lessons-learned)
* [What’s in this repository](#whats-in-this-repository)
* [How to verify / request code access](#how-to-verify--request-code-access)
* [Quick CV blurb & contact](#quick-cv-blurb--contact)
* [Appendix & key documents](#appendix--key-documents)
* [License & code access](#license--code-access)

---

## Overview

MaBourse is a production-grade, full-stack scholarship management platform that helps students discover, filter, and apply for scholarships while providing administrators with advanced tools for managing listings, users, communications, and campaigns.

The platform evolved from an early prototype into a **secure, enterprise-capable system** through a multi-phase process:

* Database migration (file → SQLite → Sequelize → PostgreSQL)
* Authentication hardening (JWT, secure cookies, session DB tracking)
* Security foundations (OWASP compliance, event logging, anomaly detection)
* Enterprise-level modernization (admin portal redesign, CI readiness, production audits)

This repository is the **public showcase**. The **codebase is intentionally private**, but this README + demo are designed for reviewers (professors, supervisors, recruiters) to evaluate the project’s technical depth and production readiness.

---

## Demo (9 minutes)

📺 **Watch the 9-minute walkthrough demo**:

* Public portal: browsing, search, filters, details, subscriptions
* Admin portal: dashboard, CRUD, bulk import/export, messaging, analytics, security monitoring

**Demo file**: `demo.mp4` (included here)
**External link**: `REPLACE_WITH_UNLISTED_YOUTUBE_OR_REPO_DEMO_LINK`

> ⚠️ **Demo Credentials Note**: The admin login shown (`admin123@gmail.com`) is a **placeholder email** used for demonstration only.
> The password is masked. Real production credentials are **different, secured, and never exposed** in this repository or video.

---

## Why this project matters

* 🌍 Bridges the **information gap** for students worldwide seeking scholarships (multi-language: English, French, Arabic with RTL support).
* 🔧 Captures **real-world engineering complexity**: relational database schema, secure auth, audit logging, anomaly detection, bulk operations.
* 🚀 Demonstrates the **full lifecycle** of building a production system: prototyping, migrations, remediation, testing, audits, deployment planning.

---

## Highlights & Achievements

* ✅ **Production-ready** — 95%+ readiness across audits, validated via multiple technical reviews.
* ✅ **Enterprise security** — 2FA (TOTP), device trust, ML anomaly detection, CSP, structured logging.
* ✅ **Performance** — APIs <200 ms avg, DB queries <100 ms avg, frontend load <3s.
* ✅ **Modernized admin portal** — rebuilt with Ant Design, consolidated backend, bulk imports.
* ✅ **Database migration** — legacy → PostgreSQL with clean schema & constraints.
* ✅ **Operational proof** — system status reports confirm *All systems operational*.

---

## Key Features

### 🎓 Public Portal

* Browse scholarships with advanced filters (country, level, deadline)
* Detail pages with metadata, attachments, thumbnails
* Newsletter subscription + social sharing
* Responsive, multilingual UI (EN/FR/AR)

### 🔑 Admin Portal

* Secure login with role-based access + session tracking
* Dashboard with real-time stats & security alerts
* CRUD for scholarships/opportunities + uploads
* Bulk import/export (JSON/CSV)
* Messaging + newsletter management
* Security dashboard (event logs, device trust, anomaly detection)

### 🔒 Security & Monitoring

* JWT + HTTP-only cookie session management
* TOTP-based 2FA + backup codes
* ML anomaly detection + risk scoring
* CSP, HSTS, X-Frame-Options, rate limiting, input sanitization
* Structured security event logging

---

## Technical architecture

### Frontend

* React 18 + TypeScript
* Tailwind CSS + Ant Design
* React Router v6, Context API for state
* Axios for API calls, lazy loading, code splitting

### Backend

* Node.js + Express (TypeScript)
* PostgreSQL with optimized raw queries
* Authentication: JWT + secure cookies + DB-tracked sessions
* Validation: express-validator
* Security: bcrypt, helmet, rate-limiting, CORS config
* File handling: multer (for uploads)
* Email: Nodemailer (dev SMTP / configurable for production)

### Security Layer

* 2FA (TOTP, backup codes)
* Device trust system
* ML anomaly detection & scoring
* Password history & bcrypt hashing
* CSP violation reporting

### DevOps / Ops

* Env-driven config (`.env` templates)
* Docker-ready setup
* Health checks & monitoring endpoints
* Migration scripts
* Structured logging (Winston-style)

### Testing & QA

* Postman collections for API verification
* curl test logs (included in `/docs`)
* Unit testing (Jest/JUnit in earlier phases)
* Manual verification during audits

---

## Database & schema overview

Core schema (simplified, PostgreSQL):

```prisma
model Scholarship {
  id          Int      @id @default(autoincrement())
  title       String
  description String
  level       String?
  country     String?
  deadline    DateTime
  thumbnail   String?
  createdBy   Int
  createdAt   DateTime @default(now())
}
```

**Security tables**: `security_events`, `trusted_devices`, `admin_sessions`, `admin_password_history`, `api_keys`.

> ⚠️ **Note on data**: All records in the database are **sample/fake data created for development and testing only**.
> No real student, institutional, or sensitive data is included.

---

## Security & compliance

* Full OWASP Top 10 coverage (XSS, CSRF, SQLi, SSRF, etc.).
* GDPR-aware data handling: consent, export, delete.
* Strong password policy (bcrypt + history enforcement).
* Security headers: CSP, HSTS, X-XSS-Protection, etc.
* Configurable environment-specific CSP violation reporting.

---

## Production readiness & performance

* **Audit score**: 95%+ security validation pass.
* **API latency**: <200 ms avg.
* **DB queries**: <100 ms avg.
* **Frontend load**: <3s with optimized builds.

**Deployment checklist** includes:

* Env templates & secret mgmt.
* DB migration & backup procedures.
* HTTPS/SSL, load balancing, CDN.
* Monitoring + APM integration.

---

## Challenges, remediation & lessons learned

* **Admin portal fragmentation** → unified with Ant Design + PostgreSQL.
* **Frontend/backend integration issues** → fixed via proxy middleware + CORS credentials.
* **Newsletter legacy conflict** → replaced file-based with DB-backed subscriber mgmt.

Full remediation steps are detailed in `/docs` with before/after evidence.

---

## What’s in this repository

* `README.md` (this file)
* `demo.mp4` (9-minute walkthrough)
* `assets/` (screenshots & visuals)
* `docs/` (audit reports, migration logs, remediation notes)
* `LICENSE` — *Proprietary / Private*

> 🔒 The **source code is private**. This repository is a **public showcase**.

---

## How to verify & request code access

Professors, supervisors, or recruiters may request access for academic/professional review.

**Steps**:

1. Email: `REPLACE_WITH_YOUR_EMAIL@example.com` (or open an issue).
2. Include:

   ```
   Subject: Request for MaBourse private repo access
   Name: <Your Name>
   Affiliation: <University / Company>
   Purpose: <Review type>
   Duration: <e.g., 14 days>
   GitHub Username: <your_github_username>
   ```
3. Verified requests get read-only access or secure archive.

---

## Quick CV blurb

> **MaBourse — Production-ready scholarship portal** (React, TypeScript, Node.js, PostgreSQL) with enterprise-grade security (2FA, anomaly detection), admin dashboard, bulk import, multilingual support. Audited & validated for deployment.

---

## Contact & verification

* GitHub: [WebDevAbdou](https://github.com/WebDevAbdou)
* LinkedIn: [Abdoulaye Ahmat Abdoulaye](https://www.linkedin.com/in/abdoulaye-ahmat-abdoulaye-3123a629b/)
* Portfolio / CV: *Available on request*

---

## Appendix — Key documents (in `/docs`)

* `COMPREHENSIVE_AUDIT_REPORT.md`
* `PRODUCTION_AUDIT_REPORT.md`
* `ADMIN_PORTAL_AUDIT.md`
* `PHASE4_SECURITY_IMPLEMENTATION_REPORT.md`
* `DEPLOYMENT_READINESS_PLAN.md`
* `SYSTEM_STATUS_REPORT.md`

---

## License & code access

* Codebase is **private**.
* Public repo = showcase only.
* License: *Proprietary / By request*.

---

> **Final note:** This project represents a full production-level engineering journey: prototyping → migration → remediation → audits → production readiness. Reviewers may request additional logs, CI artifacts, or a live demo session.

---