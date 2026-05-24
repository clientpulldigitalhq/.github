🧠 CLIENTPULL DIGITAL — ENGINEERING WORKFLOW CONTRACT
(Frontend ↔ Backend Collaboration Rules)

1. Core Principle (NON-NEGOTIABLE)

We do not build features directly. We build contracts first, then implementation.

Every feature must follow this order:

1. Define behavior (what it should do)
2. Define API contract (how frontend + backend communicate)
3. Implement backend
4. Implement frontend
5. Test integration
6. Merge to production

No step can be skipped.

2. ROLE BOUNDARIES (VERY IMPORTANT)
   🎨 Frontend Developer (You)
   Responsibilities:
   Build UI based on design system
   Consume backend APIs (do NOT design API logic)
   Validate API responses in frontend usage
   Handle UI states:
   loading
   success
   error
   Ensure responsiveness and UX consistency
   You DO NOT:
   change backend logic
   assume API behavior without documentation
   bypass API contracts
   ⚙️ Backend Developer (Simon)
   Responsibilities:
   Design API structure
   Build business logic
   Manage database and data flow
   Ensure API stability
   Provide documentation for every endpoint
   Ensure predictable responses
   He DOES NOT:
   assume frontend needs
   change API without versioning
   deploy untested endpoints
3. API CONTRACT RULE (MOST IMPORTANT RULE)

Every feature MUST include a contract before coding.

Example Contract:
Feature: “Create Delivery Request”
POST /delivery/request
Request:
{
"businessId": "string",
"pickupLocation": "string",
"destination": "string",
"itemDescription": "string"
}
Response:
{
"success": true,
"requestId": "string",
"status": "pending"
}
RULE:

Frontend can ONLY build based on this contract.

4. FEATURE WORKFLOW (TEAM RULE)

Every feature MUST follow this lifecycle:

Step 1 — Feature Definition
Write what problem we are solving
Step 2 — API Contract Draft
Backend writes endpoints + request/response
Step 3 — Agreement
Frontend + Backend approve contract
Step 4 — Backend Implementation
Backend builds logic
Step 5 — Frontend Integration
Frontend consumes API
Step 6 — Testing
Both verify behavior using real requests
Step 7 — Pull Request Review 5. GIT BRANCH RULES

Inside GitHub:

Branch Structure:
main → production (DO NOT TOUCH DIRECTLY)
dev → integration
feature/\* → individual work
RULE:
No direct push to main
Every feature must go through Pull Request
Every PR must pass CI checks 6. API CHANGE RULE (CRITICAL FOR BACKEND)

Backend CANNOT:

change request format without warning
rename endpoints without versioning
break existing responses
If change is required:

Must:

create new version

Example:

/v1/delivery/request
/v2/delivery/request 7. FRONTEND API USAGE RULE

Frontend MUST:

never guess API response
never hardcode backend behavior
always handle failure states
Required UI states:
loading state
success state
error state
empty state 8. COMMUNICATION RULE

Before building any feature:

Required discussion:
What is being built?
What endpoints are needed?
What does success look like?
What are failure cases?

No silent implementation.

9. TESTING RULE (PREVENTS BREAKING PRODUCTION)

Before merging:

Backend must provide:
sample request
sample response
test proof (Postman / logs)
Frontend must verify:
API works in UI
error handling works
no broken states 10. PRODUCTION SAFETY RULE (MOST IMPORTANT)

A feature is ONLY allowed into production if:

✔ API contract is followed
✔ CI checks pass
✔ PR approved
✔ Both frontend and backend tested integration
✔ No breaking changes

11. FINAL PRINCIPLE (TEAM MINDSET)

“We do not push code to production. We push verified systems that behave exactly as defined in the contract.”

If you want next upgrade (VERY RECOMMENDED)

I can help you build:

1. PR Template (forces Simon to document everything)
2. GitHub Issue template (forces structured tasks)
3. API contract template file (so every feature starts correctly)
4. CI checks that validate API format automatically

This combination will basically make your system production-safe even for a beginner team.

I want a refined version of the document like about the rules and roles for the agency including this in the document if it will make sense for it to be there if not just provide anything.
Agency Operational Structure And Roles
ClientPull Digital
Agency Operating System: Roles, Rules, and Engineering Standards

1. Introduction

This document defines the operational, technical, and collaboration standards of ClientPull Digital.

It exists to ensure:

Predictable software delivery
Clear role separation
Stable production systems
Reduced communication ambiguity
Scalable engineering practices

This is a binding internal working system for all team members.

2. Core Operating Principle

We do not build features directly. We build systems through agreed contracts, structured workflows, and controlled releases.

Every piece of work must follow:

Definition of behavior
API contract agreement
Implementation (backend + frontend)
Testing and validation
Controlled merge to production

No step is optional.

3. Agency Vision

ClientPull Digital builds digital systems that solve real operational problems for businesses.

Focus areas:

Business websites and customer interfaces
Operational management systems
Inventory and sales tracking systems
Delivery and logistics coordination platforms
Custom business automation tools

We prioritize system efficiency over visual complexity.

4. Team Roles and Responsibilities
   4.1 Frontend Developer — Sadick Sulley
   Core Responsibility

Transforms UI/UX designs and backend APIs into functional, responsive user interfaces.

Responsibilities
Build frontend interfaces based on approved designs
Consume backend APIs strictly via documented contracts
Handle UI states (loading, success, error, empty)
Ensure responsive and accessible design implementation
Maintain frontend architecture and reusable components
Restrictions
Must not modify backend logic
Must not assume API behavior without documentation
Must not bypass API contracts
4.2 UI/UX Designer — Benjamin Arkorful
Core Responsibility

Defines user experience structure and interface design systems.

Responsibilities
Design user flows and system layouts
Create wireframes and interface prototypes
Define visual hierarchy and interaction patterns
Ensure usability and consistency across systems
Focus
Clarity over complexity
Function over decoration
4.3 Backend Developer — Simon Tindanzor
Core Responsibility

Builds system logic, APIs, and data architecture.

Responsibilities
Design and implement backend systems
Define API endpoints and data contracts
Manage database structure and logic
Ensure system security and reliability
Provide complete API documentation for all features
Restrictions
Must not change APIs without versioning
Must provide request/response contracts before implementation
Must ensure backward compatibility 5. Engineering Contract (Frontend ↔ Backend Agreement)

Every feature MUST follow this structure before development begins.

Step 1 — Feature Definition

What problem are we solving?

Step 2 — API Contract

Backend defines:

endpoints
request structure
response structure
error formats

Example:

Endpoint

POST /delivery/request

Request
{
"businessId": "string",
"pickupLocation": "string",
"destination": "string",
"itemDescription": "string"
}
Response
{
"success": true,
"requestId": "string",
"status": "pending"
}
Step 3 — Agreement

Frontend and backend must approve contract before coding.

Step 4 — Implementation
Backend builds logic
Frontend builds UI integration
Step 5 — Testing

Both sides validate real API behavior.

Step 6 — Merge Approval

Only allowed after successful validation.

6. GitHub Workflow Standards

All projects must follow structured version control on GitHub.

Branch Structure
main → production (protected)
dev → integration
feature/\* → individual work
Rules
No direct push to main
All changes must go through pull requests
All PRs must pass CI checks 7. API Stability Rules (Backend Critical Rules)

Backend must:

Never change request/response formats without versioning
Never break existing endpoints without migration path
Always maintain backward compatibility

If changes are required:

Example:

/v1/resource
/v2/resource 8. Frontend Integration Rules

Frontend must:

Use only documented API contracts
Handle all UI states:
loading
success
error
empty
Never assume backend behavior 9. Communication Protocol

Before building features, the team must agree on:

Feature objective
API contract
Expected behavior
Edge cases

No silent implementation is allowed.

10. Testing and Quality Assurance

No feature is complete without:

Backend:

sample request/response
test verification (Postman or logs)

Frontend:

UI integration validation
error state validation 11. Production Safety Rule

A feature is only allowed into production when:

API contract is followed
CI checks pass
Pull request is approved
Frontend and backend integration is tested
No breaking changes exist 12. Final Principle

We do not deploy code. We deploy verified, contract-driven systems that behave predictably in production.

13. Long-Term Direction

ClientPull Digital evolves toward a structured systems engineering agency focused on:

Business operational systems
Logistics and delivery platforms
Scalable backend architectures
Maintainable frontend systems
Real-world digital transformation solutions
