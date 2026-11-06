# EduGest — Engineering Decisions

## 1. Introduction

This document describes the main technical and architectural decisions reflected in the EduGest implementation.

It explains the reasoning behind the selected technologies, architectural organization and engineering trade-offs.

The objective is to document the technical approach adopted during development, including its advantages, limitations and opportunities for improvement.

These decisions are documented based on the existing implementation. They should not be interpreted as proof that every choice was originally made through a formal architecture decision process.

---

## 2. Modular Monolithic Architecture

**Decision:** Organize the application as a modular monolith rather than distributing functionality across independent microservices.

The backend centralizes HTTP request handling while separating business operations into domain-oriented service modules.

**Rationale:**
- Keeps the application relatively simple to deploy and maintain.
- Organizes business responsibilities into identifiable modules.
- Avoids the operational overhead of managing multiple independent services.
- Allows the application to evolve without introducing unnecessary infrastructure complexity.

**Trade-offs:**

As the application grows, service boundaries and shared dependencies require careful management to prevent excessive coupling.

---

## 3. Vercel as the Deployment Platform

**Decision:** Use Vercel to host the frontend and execute backend operations through serverless functions.

The API uses a centralized entry point for HTTP request handling.

**Rationale:**
- Simplifies application deployment.
- Supports serverless backend execution.
- Integrates frontend and backend deployment workflows.
- Reduces the need to maintain a dedicated application server.

**Trade-offs:**

Serverless execution introduces considerations around:
- Function execution limits.
- Cold starts.
- Database connection management.
- Connection pooling.
- Runtime configuration.

---

## 4. PostgreSQL as the Primary Database

**Decision:** Use PostgreSQL as the primary relational database.

The platform manages interconnected entities such as students, teachers, classes, courses, payments and academic records.

**Rationale:**
- Supports relational data structures.
- Provides transactional capabilities.
- Enables structured queries and reporting.
- Offers flexibility as the data model evolves.
- Helps maintain consistency across interconnected records.

**Trade-offs:**

Database access, indexing, connection pooling and query optimization require deliberate management as data volume increases.

---

## 5. Domain-Oriented Service Organization

**Decision:** Separate backend business operations into domain-oriented service modules.

Examples include student management, teachers, classes, payments, school configuration and academic records.

**Rationale:**
- Makes business responsibilities easier to identify.
- Improves code organization.
- Makes individual modules easier to understand and maintain.
- Reduces the need to place all business logic inside HTTP handlers.

**Trade-offs:**

Shared functionality must be managed carefully to avoid duplicated logic, excessive coupling and circular dependencies.

---

## 6. Native Frontend Technologies

**Decision:** Build the frontend using HTML, CSS and JavaScript ES Modules instead of adopting a large frontend framework.

**Rationale:**
- Keeps the frontend relatively lightweight.
- Provides direct control over interface behavior.
- Avoids introducing framework-specific complexity.
- Makes use of browser-native capabilities.

**Trade-offs:**

As the number of screens and interactions increases, state management, component reuse and interface consistency become more important.

---

## 7. API-Based Communication

**Decision:** Separate frontend interactions from backend operations through API endpoints.

The frontend communicates with backend routes to perform application operations.

**Rationale:**
- Establishes a boundary between presentation and business operations.
- Centralizes sensitive backend operations.
- Allows backend validation and authorization.
- Makes frontend and backend evolution more independent.

**Trade-offs:**

API contracts must remain consistent, and error handling must be predictable across the application.

---

## 8. Authentication and Authorization

**Decision:** Include authentication utilities and role-based access concepts to support differentiated access to application operations.

The codebase includes JWT-related functionality, password hashing utilities and session-related components.

**Engineering considerations:**

Authentication and authorization must be enforced server-side.

Client-provided identity information must never be treated as a trusted source of authentication.

The current implementation requires further security hardening, particularly around:
- Server-side session verification.
- Identity validation.
- Role-based authorization.
- Protected API endpoints.
- School-level data isolation.

These are important requirements for protecting institutional information.

---

## 9. Data Export and Portability

**Decision:** Include data export and document generation capabilities in selected operational workflows.

Libraries such as XLSX and jsPDF support spreadsheet and PDF-related operations.

**Rationale:**
- Facilitates administrative reporting.
- Reduces repetitive manual data handling.
- Makes selected information easier to share and archive.
- Supports practical school administration workflows.

**Trade-offs:**

Exported information must be handled carefully to prevent unauthorized disclosure of student and institutional data.

---

## 10. Privacy and Source Code Protection

**Decision:** Keep the production source code, database credentials, configuration secrets and real institutional records private.

The public repository documents the product and its engineering approach without distributing the operational application.

**Rationale:**
- Protects institutional information.
- Prevents accidental exposure of production credentials.
- Preserves the confidentiality of the original product.
- Allows technical work to be presented publicly without publishing sensitive implementation details.

The public repository is therefore a technical showcase, not an open-source distribution.

---

## 11. Technical Debt and Improvement Priorities

The existing implementation provides a functional foundation, but several areas require further engineering attention.

Identified priorities include:

| Area | Improvement |
|---|---|
| Authentication | Strengthen server-side session verification |
| Authorization | Review permissions across protected endpoints |
| Multi-school isolation | Verify tenant-level data access restrictions |
| Database | Review indexing and connection management |
| Testing | Expand automated integration and authorization tests |
| Debugging | Remove development debugging utilities from production |
| Account security | Review account creation and default credential handling |
| Maintainability | Improve separation between routing, business logic and persistence |
| Observability | Introduce structured logging and monitoring |

These priorities should be addressed according to their security impact and operational importance.

---

## 12. Architectural Evolution

EduGest was developed as a complete school management application with multiple operational domains sharing a common backend and relational database.

The architecture prioritizes:
- Practical deployment.
- Clear separation of responsibilities.
- Relational data management.
- Maintainable business modules.
- Manageable infrastructure complexity.

Future architectural changes should be driven by actual product requirements rather than adopting additional technologies without a clear purpose.

---

## Conclusion

The engineering approach behind EduGest reflects a practical balance between functionality, architectural organization and operational complexity.

The objective was to build a centralized school management platform using technologies capable of supporting interconnected academic, administrative and financial workflows.

Documenting both the strengths and limitations of the implementation provides a more accurate representation of the engineering work and creates a foundation for future improvements.