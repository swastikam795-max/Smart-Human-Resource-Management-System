.
# Orbit HRMS

An AI-powered Human Resource Management System prototype — single-file, client-side, built to demonstrate a full HR workflow (auth, employee records, attendance, leave, payroll, AI-assisted HR decisions) without a backend.

## Overview

Orbit HRMS is a role-based HR platform covering the core operations a small company needs: onboarding data, daily attendance, leave requests and approvals, payroll visibility, and an AI assistant layered on top for HR decision support. It was built as a self-contained demo — one HTML file, no build step, no server — so it can be opened, shared, or deployed anywhere static files are served.

## Features

**Authentication & roles**
- Role-based sign-in for Admin, HR, and Employee, each with a different dashboard and navigation set.

**Dashboard**
- Employee view: attendance rate, leave balance, pending requests, this month's net pay.
- Admin/HR view: headcount, attendance trend, department breakdown, pending approvals, and an AI-generated absenteeism risk summary.

**Employee directory** (Admin/HR)
- Search, add, edit, and remove employee records; salary edits automatically recompute payroll.

**My Profile**
- Personal and job details, mock documents, salary structure; employees can edit their own phone/address.

**Attendance**
- Daily check-in/check-out, personal attendance log, department-level analytics for Admin/HR.

**Leave management**
- Apply for leave with balance and date validation; Admin/HR can approve, reject, or ask the AI assistant for a recommendation based on the employee's history and attendance.

**Payroll**
- Read-only payslip view for employees (downloadable), full payroll table for Admin/HR.

**AI Reports**
- One-click narrative HR report generated from live headcount, attendance, leave, and payroll data.

**Orbit Assistant**
- Floating chat widget that answers HR policy questions using the company's leave rules and the logged-in user's own data as context.

## Demo accounts

| Role | Username | Password |
|---|---|---|
| Admin | `admin` | `admin123` |
| HR | `hr` | `hr123` |
| Employee | `employee` | `emp123` |

## Tech stack

- Vanilla HTML/CSS/JS — no framework, no build step
- Chart.js for dashboard visualizations
- Anthropic API (`claude-sonnet-4-6`) called directly from the client for AI features
- `window.storage` (shared demo key-value store) in place of a real database

## Architecture notes

- **Single file, single source of truth.** All state lives in one in-memory `DB` object, persisted to `window.storage` under one key (`orbit-hrms-db`) and shared across everyone using this demo instance.
- **No backend.** Login, validation, and business rules all run client-side. This is intentional for a prototype but means it is not suitable for real employee data.
- **AI calls are stateless.** Each AI feature (risk analysis, leave suggestion, report generation, chat) sends the relevant slice of data to the model per request; nothing is fine-tuned or persisted on the model side.

## Known limitations

- No real authentication — passwords are hardcoded in client-side JS for demo purposes only.
- No server-side validation — all checks (leave balance, email format, etc.) are enforced in the browser only.
- Shared demo storage — anyone using this deployment can see and modify the same data.
- No calendar-based date picker for leave — uses native date inputs rather than a visual monthly calendar with attendance markers.
- No email verification flow, despite being referenced in the original requirements spec.

## Accessibility

- Semantic landmarks (`nav`, `header`, `main`), skip-to-content link.
- Keyboard-operable navigation, role picker, and modals (focus trapped, Escape to close, focus restored on close).
- Status conveyed by icon + text, not color alone.
- `aria-live` regions on AI output and chat so responses are announced to screen readers.

## Running it

Just open the HTML file in a browser, or host it on any static file server (GitHub Pages, Vercel, Netlify). No build step or environment variables required.

## Possible next steps

- Replace client-side demo storage with a real backend (Node/Express + PostgreSQL) and proper authentication.
- Add a visual calendar component for leave applications, per the original requirements spec.
- Automated accessibility audit (axe/Lighthouse) and WCAG AA contrast pass.
- Mobile-first redesign of the navigation shell instead of a desktop layout adapted down.
