<div align="center">

# ClientPull Digital

### Agency Operating System

**Roles, Rules & Standards**

![Version](https://img.shields.io/badge/Version-1.0-orange?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active-green?style=flat-square)
![Classification](https://img.shields.io/badge/Classification-Internal%20Only-gray?style=flat-square)

---

_We do not build features directly._
_We build systems through agreed contracts, structured workflows, and controlled releases._

</div>

---

## Table of Contents

- [Introduction](#1-introduction)
- [Agency Vision](#2-agency-vision)
- [Team Roles](#3-team-roles--responsibilities)
- [Feature Workflow](#4-feature-development-workflow)
- [API Contract Standard](#5-api-contract-standard)
- [Git & GitHub Workflow](#6-git--github-workflow)
- [Team Rules](#7-team-rules)
- [Communication Protocol](#8-communication-protocol)
- [Production Safety Checklist](#9-production-safety-checklist)
- [Long-Term Direction](#10-long-term-direction)

---

## 1. Introduction

This document defines the operational, technical, and collaboration standards of **ClientPull Digital**. It is a binding internal working guide for all team members and must be followed on every project.

This document exists to ensure:

- Predictable software delivery on every project
- Clear boundaries between roles to avoid confusion or overlap
- Stable, safe production systems that never break unexpectedly
- Reduced communication ambiguity across the team
- Scalable practices that grow with the agency

---

## 2. Agency Vision

ClientPull Digital builds digital systems that solve real operational problems for businesses. We deliver functional, reliable systems — not just beautiful interfaces.

**Core Focus Areas:**

- Business websites and customer-facing interfaces
- Operational management and workflow systems
- Inventory and sales tracking platforms
- Delivery and logistics coordination systems
- Custom business automation and integration tools

> **We prioritize system efficiency over visual complexity.**
> **We deliver verified systems, not just shipped code.**

---

## 3. Team Roles & Responsibilities

### 🖥️ Sadick Sulley — Frontend Developer

**Core Responsibility:** Transforms UI/UX designs and backend APIs into functional, responsive user interfaces.

| Responsibilities                                                | Restrictions                                        |
| --------------------------------------------------------------- | --------------------------------------------------- |
| Build frontend interfaces based on approved designs             | Must not modify backend logic or database structure |
| Consume backend APIs strictly via documented contracts          | Must not assume API behavior without documentation  |
| Handle all UI states: loading, success, error, and empty        | Must not bypass or work around API contracts        |
| Ensure responsive and accessible design implementation          | Must not push directly to the `main` branch         |
| Maintain frontend architecture and reusable components          |                                                     |
| Collaborate with designer to implement design tokens accurately |                                                     |

---

### 🎨 Benjamin Arkorful — UI/UX Designer

**Core Responsibility:** Defines user experience structure and interface design systems.

**Responsibilities:**

- Design user flows and full system layouts for every feature
- Create wireframes, mockups, and interactive prototypes
- Define visual hierarchy, spacing, and interaction patterns
- Provide design tokens: colors, typography, breakpoints, and spacing
- Ensure usability and visual consistency across all screens
- Deliver mobile, tablet, and desktop designs for every page

---

### ⚙️ Simon Tindanzor — Backend Developer

**Core Responsibility:** Builds system logic, APIs, and data architecture.

| Responsibilities                                              | Restrictions                                               |
| ------------------------------------------------------------- | ---------------------------------------------------------- |
| Design and implement all backend systems and business logic   | Must not change API structure without versioning           |
| Define API endpoints and write data contracts before building | Must not deploy untested or undocumented endpoints         |
| Manage database structure, migrations, and data integrity     | Must not assume frontend requirements without discussion   |
| Ensure system security, authentication, and reliability       | Must not break existing responses without a migration path |
| Provide complete API documentation for every endpoint         |                                                            |
| Maintain backward compatibility across all API versions       |                                                            |

---

## 4. Feature Development Workflow

Every feature — no matter how small — must follow this lifecycle **without skipping any step.**

| Step | Name                       | Requirement                                                                                         |
| :--: | -------------------------- | --------------------------------------------------------------------------------------------------- |
| `01` | **Feature Definition**     | Write clearly what problem is being solved and what the expected outcome is. No ambiguity.          |
| `02` | **API Contract Draft**     | Backend defines all endpoints, request structure, response structure, and error formats in writing. |
| `03` | **Team Agreement**         | Frontend and backend both review and approve the contract before any code is written.               |
| `04` | **Backend Implementation** | Backend builds the logic based on the approved contract. No deviation from the agreed structure.    |
| `05` | **Frontend Integration**   | Frontend builds the UI and connects to the API strictly according to the documented contract.       |
| `06` | **Integration Testing**    | Both sides validate real API behavior together. All UI states must be verified.                     |
| `07` | **Pull Request & Review**  | Code is submitted via PR, reviewed, and merged only after passing all checks.                       |

---

## 5. API Contract Standard

An API contract is a **written agreement** between frontend and backend that defines exactly how they will communicate for a given feature. No feature is built without one.

**Every contract must include:**

- The feature name and what problem it solves
- The HTTP method and endpoint URL
- The full request body structure with field types
- The full success response structure
- All possible error responses and their codes

### Contract Example — Create Delivery Request

```
Feature:   Create Delivery Request
Endpoint:  POST /api/v1/delivery/request
```

**Request Body:**

```json
{
  "businessId": "string",
  "pickupLocation": "string",
  "destination": "string",
  "itemDescription": "string"
}
```

**Success Response `200`:**

```json
{
  "success": true,
  "requestId": "string",
  "status": "pending"
}
```

**Error Response `400`:**

```json
{
  "success": false,
  "error": "Missing required field: destination"
}
```

---

> ### ⚠️ API Versioning Rule — Critical
>
> If any existing API endpoint needs to change, the backend **must create a new version**. The old version must remain functional until both sides have fully migrated.
>
> ```
> Old:  /api/v1/delivery/request
> New:  /api/v2/delivery/request  ← Create this, do NOT modify v1
> ```

---

## 6. Git & GitHub Workflow

All projects use a structured branching strategy. This protects production from untested or incomplete code.

| Branch      | Purpose                 | Rule                                                              |
| ----------- | ----------------------- | ----------------------------------------------------------------- |
| `main`      | Live production code    | **PROTECTED** — No direct pushes. PRs only, must be approved.     |
| `dev`       | Integration / staging   | All reviewed work merges here first before going to `main`.       |
| `feature/*` | Individual feature work | Each feature gets its own branch. PRs target `dev`, never `main`. |

**Branch naming examples:**

```
feature/contact-form-api
feature/delivery-request-ui
feature/auth-login
```

---

## 7. Team Rules

|     | Rule                         | Requirement                                                                                     |
| :-: | ---------------------------- | ----------------------------------------------------------------------------------------------- |
| 📋  | **Contract First**           | Every feature must have an approved API contract before any implementation begins.              |
| 🔒  | **No Direct Push to Main**   | All code changes must go through a pull request. No exceptions.                                 |
| 📖  | **API Documentation**        | Every endpoint must be documented with full request, response, and error formats.               |
| 🔄  | **API Versioning**           | Backend cannot modify existing endpoint structure. New behavior requires a new version.         |
| ⚡  | **Handle All UI States**     | Frontend must handle loading, success, error, and empty states for every API-connected element. |
| 🚫  | **No Hardcoded Values**      | Credentials, API keys, base URLs must use environment variables — never hardcoded in code.      |
| 🧪  | **Test Before Merge**        | Backend provides Postman proof. Frontend verifies all states in the actual UI.                  |
| 💬  | **No Silent Implementation** | No feature may be built without prior team discussion on objectives, contract, and edge cases.  |

---

## 8. Communication Protocol

Before any feature is built, the team must align on these four questions. Every feature discussion must answer all of them before anyone starts coding.

> ❓ **What exactly are we building and what problem does it solve?**

> 🔗 **What API endpoints are needed and what is the contract?**

> ✅ **What does a successful implementation look like?**

> ⚠️ **What are the failure cases and how should they be handled?**

---

## 9. Production Safety Checklist

A feature is only allowed into `main` when **every item** on this checklist is satisfied.

- [ ] API contract was agreed upon and followed exactly
- [ ] All CI checks pass on the pull request
- [ ] Pull request has been reviewed and approved
- [ ] Backend has provided sample request, sample response, and Postman verification
- [ ] Frontend has verified API integration works correctly in the UI
- [ ] All UI states tested: loading, success, error, and empty
- [ ] No breaking changes to existing endpoints
- [ ] No credentials, keys, or secrets are hardcoded in the codebase
- [ ] Feature branch was merged into `dev` first and tested there

---

## 10. Long-Term Direction

ClientPull Digital is evolving toward becoming a structured digital agency focused on building real operational systems. Our long-term roadmap focuses on:

- Business operational management systems for SMEs
- Logistics and delivery coordination platforms
- Scalable backend architectures designed for growth
- Maintainable and component-driven frontend systems
- Real-world digital transformation solutions for African businesses

---

<div align="center">

---

_"We do not deploy code._
_We deploy verified, contract-driven systems_
_that behave predictably in production."_

---

**ClientPull Digital** — Internal Use Only

</div>
