
# 🎓 MaBourse — Scholarship Portal (Demo Showcase)

![Status](https://img.shields.io/badge/status-production-brightgreen.svg) ![Security](https://img.shields.io/badge/security-A%2B-brightgreen.svg) ![Systems](https://img.shields.io/badge/systems-all%20green-brightgreen.svg) ![Demo](https://img.shields.io/badge/demo-8%20min-blue.svg) ![Code](https://img.shields.io/badge/code-private-orange.svg)

> **Public showcase repository** for the *MaBourse Scholarship Portal*.
> The **source code is private** for security and IP reasons. This repository contains a 8-minute demo video and full documentation describing architecture, security, production readiness, and the technical journey to build a production-grade system. **Source code is available only upon request for academic or professional review.**

---

## Table of Contents

* [Overview](#overview)
* [Demo (9 minutes)](#demo-8-minutes)
* [Why this project matters](#why-this-project-matters)
* [Highlights & Achievements](#highlights--achievements)
* [Key Features](#key-features)
* [Technical Architecture](#technical-architecture)
* [Database & Schema Overview](#database--schema-overview)
* [Security & Compliance](#security--compliance)
* [Production Readiness & Performance](#production-readiness--performance)
* [Challenges, Remediation & Lessons Learned](#challenges-remediation--lessons-learned)
* [What’s in this repository](#whats-in-this-repository)
* [How to Verify / Request Code Access](#how-to-verify--request-code-access)
* [Quick CV Blurb & Contact](#quick-cv-blurb--contact)
* [Appendix & Key Documents](#appendix--key-documents)
* [License & Code Access](#license--code-access)

---

## Overview

MaBourse is a **production-grade, full-stack scholarship management platform** that enables students to discover, filter, and apply for scholarships while providing administrators with **advanced tools** to manage listings, users, communications, and campaigns.

The platform evolved from a prototype into a **secure, enterprise-ready system** through multi-phase enhancements:

* Database migration (legacy files → SQLite → Sequelize → PostgreSQL)
* Authentication hardening (JWT, secure cookies, session tracking)
* Security foundations (OWASP compliance, anomaly detection, structured logging)
* Enterprise-level modernization (admin portal redesign, CI/CD readiness, production audits)

> ⚠️ All data in the database are **sample/fake records** created for development and testing only. No real student, institutional, or sensitive data is included.

---

## Demo (8 minutes)

📺 Watch the 8-minute walkthrough demo:

* **Public Portal:** scholarship browsing, search, filters, details, subscriptions
* **Admin Portal:** dashboard, CRUD, bulk import/export, messaging, analytics, security monitoring

> ⚠️ Demo Credentials Note: Admin login shown (`admin123@gmail.com`) is **placeholder only**; password is masked. Production credentials are secured and never exposed.

**Demo video:** [YouTube external Link](https://youtu.be/ZOyEpC9d0eE) *(8:00 — full UI walkthrough: public portal + admin portal + security features)*

---

## Why this project matters

* Bridges the information gap for students worldwide seeking scholarships (multi-language: EN/FR/AR with RTL support).
* Captures real-world engineering complexity: relational DB schema, secure authentication, audit logging, anomaly detection, bulk operations.
* Demonstrates the **full lifecycle of a production system**: prototyping, migrations, remediation, testing, audits, and deployment planning.

---

## Highlights & Achievements

* ✅ **Production-ready:** >95% readiness across audits
* ✅ **Enterprise-grade security:** 2FA (TOTP), device trust, ML anomaly detection, CSP, structured logging
* ✅ **Performance:** API <200ms avg, DB queries <100ms avg, frontend load <3s
* ✅ **Admin Portal:** modernized with Ant Design, unified backend, bulk imports
* ✅ **Database Migration:** legacy → PostgreSQL with clean schema and constraints
* ✅ **Operational Proof:** system status reports confirm all systems operational

---

## Key Features

### Public Portal

* Scholarship browsing with advanced filters (country, level, deadline)
* Scholarship detail pages with metadata, attachments, thumbnails
* Newsletter subscription & social sharing
* Responsive, multilingual UI (EN/FR/AR) with RTL support

### Admin Portal

* Secure login with role-based access & session tracking
* Dashboard with real-time stats & security alerts
* CRUD for scholarships/opportunities with uploads
* Bulk import/export (JSON, CSV)
* Messaging system & newsletter management
* Security dashboard (event logs, device trust, anomaly detection)

### Security & Monitoring

* JWT + HTTP-only cookies, refresh & invalidation
* TOTP-based 2FA with backup codes
* ML anomaly detection & risk scoring
* CSP, HSTS, X-Frame-Options, X-XSS-Protection
* Rate limiting, request signing for critical endpoints
* Structured security event logging & audit trails

---

## Technical Architecture

**Frontend:**

* React 18 + TypeScript
* Tailwind CSS + Ant Design (admin UI)
* React Router v6, Context API for state
* Axios for API calls, lazy loading, code splitting

**Backend:**

* Node.js + Express + TypeScript
* PostgreSQL (production DB) — raw, optimized queries
* Authentication: JWT + secure cookies, session DB tracking
* Validation: express-validator, rate-limiting, input sanitization
* File handling: multer (uploads)
* Email: Nodemailer (dev SMTP / production configurable)

**Security Layer:**

* 2FA (TOTP + backup codes)
* Device trust system
* ML anomaly detection & scoring
* Password history & bcrypt hashing
* CSP violation reporting

**DevOps / Ops:**

* Environment-driven configuration (.env templates)
* Docker-ready setup
* Health checks & monitoring endpoints
* Migration scripts
* Structured logging (Winston-style)

**Testing & QA:**

* Postman collections for API verification
* curl test logs included in `/docs`
* Unit testing: Jest (frontend), JUnit (backend in early phases)
* Manual verification during audits

---

## Database & Schema Overview

**Core PostgreSQL schema (simplified):**

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

**Security tables:** `security_events`, `trusted_devices`, `admin_sessions`, `admin_password_history`, `api_keys`

> ⚠️ All records are **fake/sample data** for development/testing only.

---

## Security & Compliance

* Full OWASP Top 10 coverage (XSS, CSRF, SQLi, SSRF, etc.)
* GDPR-aware data handling: consent, export, delete endpoints
* Strong password policies (bcrypt + history enforcement)
* Security headers: CSP, HSTS, X-XSS-Protection
* Environment-specific CSP violation reporting

---

## Production Readiness & Performance

* Audit score: >95% security validation pass
* API latency: <200ms average
* DB queries: <100ms average
* Frontend load: <3s optimized

**Deployment checklist:**

* Env templates & secret management
* DB migration & backup procedures
* HTTPS/SSL, load balancing, CDN recommendations
* Monitoring & APM integration

---

## Challenges, Remediation & Lessons Learned

* **Admin portal fragmentation** → unified with Ant Design + PostgreSQL
* **Frontend/backend integration issues** → fixed via proxy middleware + CORS credentials
* **Newsletter legacy conflict** → replaced file-based with DB-backed subscribers

> Full remediation steps are documented in `/docs` with before/after evidence

---

## What’s in this repository

* `README.md` (this file)
* `demo.mp4` (or external demo link)
* `assets/` — screenshots, GIFs, visuals
* `docs/` — audit reports, migration logs, remediation notes
* `LICENSE` — Proprietary / Private

> 🔒 **Source code is private** — this repository is **public showcase only**

---

## How to Verify / Request Code Access

Professors, supervisors, or recruiters may request access for academic/professional review:

**Steps:**

1. Email: `REPLACE_WITH_YOUR_EMAIL@example.com` (or open a GitHub issue)
2. Include:

```text
Subject: Request for MaBourse private repo access
Name: <Your Name>
Affiliation: <University / Company>
Purpose: <Review type>
Duration: <e.g., 14 days>
GitHub Username: <your_github_username>
Contact: <email or phone>
```

3. Verified requests get **read-only access** or **secure archive**

**Quick verification for reviewers:**

* `GET /api/health` — confirms server status & version
* `GET /api/test-db` — confirms DB connection & record counts
* Login to admin portal (credentials provided after access granted)
* Watch demo video to cross-verify UI behavior

---

## Quick CV Blurb

> **MaBourse — Production-ready scholarship portal** (React, TypeScript, Node.js, PostgreSQL) with enterprise-grade security (2FA, anomaly detection), admin dashboard, bulk import, multilingual support. Audited & validated for production deployment.

---

## Contact & Verification

* GitHub: [WebDevAbdou](https://github.com/WebDevAbdou)
* LinkedIn: [Abdoulaye Ahmat Abdoulaye](https://www.linkedin.com/in/abdoulaye-ahmat-abdoulaye-3123a629b/)
* Portfolio / CV: Available on request

---

## Appendix — Key Documents (in `/docs`)

* `COMPREHENSIVE_AUDIT_REPORT.md` — full technical report & implementation history
* `PRODUCTION_AUDIT_REPORT.md` — production readiness verification & tests
* `ADMIN_PORTAL_AUDIT.md` — admin portal remediation steps
* `PHASE4_SECURITY_IMPLEMENTATION_REPORT.md` — detailed security architecture
* `DEPLOYMENT_READINESS_PLAN.md` — pre-prod checklist
* `SYSTEM_STATUS_REPORT.md` — operational & performance logs

---

## License & Code Access

* Codebase is **private**; public repo is showcase only
* To request access for academic/professional review, follow **How to Verify / Request Code Access**
* License: Proprietary / By request

---

> **Final Note:** This repository documents the full **production-grade engineering journey**: prototyping → migration → security → audits → deployment readiness. Reviewers may request logs, CI artifacts, or live demo sessions.

*Prepared for academic & professional review — MaBourse Scholarship Portal*

---

This is **full, professional, reviewer-ready**, includes all tech used, sample data disclaimers, clear demo notes, and explicit code access procedure.
---