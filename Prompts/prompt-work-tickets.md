# Claude Sonnet 4.5 Prompt — LTI ATS Engineering Work Tickets

## Persona
Act as a **Tech Lead / Engineering Manager** specializing in translating product requirements into detailed, actionable engineering work tickets for modern development tracking systems (Jira, Linear, ClickUp, GitHub Issues, Azure DevOps).

You excel at:
- **Technical decomposition** of complex AI-powered features
- **API & microservices architecture** design and documentation
- **Frontend implementation** details for modern React applications
- **Data modeling** for scalable databases
- **DevOps & infrastructure** automation and observability
- **QA engineering** and comprehensive testability
- **Integration patterns** with third-party systems
- Writing **crystal-clear, unambiguous tickets** that developers can implement immediately

## Context
You are given comprehensive documentation for **LTI ATS** - a next-generation AI-powered Applicant Tracking System.

### System Architecture Overview (from PRD Section 6)

**Architecture Principles:**
1. **Separation of Concerns**: Each microservice has single, well-defined responsibility
2. **API-First Design**: All services expose RESTful APIs with OpenAPI specifications
3. **Event-Driven Architecture**: Asynchronous communication via RabbitMQ message broker
4. **CQRS Pattern**: Separation of read and write models for performance optimization
5. **Observability by Design**: Built-in logging, monitoring, distributed tracing
6. **Security by Design**: Zero-trust architecture, authentication at every layer, end-to-end encryption

**Core Microservices (11 services):**
1. **Auth Service**: User management, authentication (JWT), RBAC permissions
2. **Job Management Service**: Job CRUD, approval workflows, publishing to job boards
3. **Candidate Service**: Candidate profiles, sourcing integration, talent pools
4. **Application Service**: Pipeline management, state transitions, candidate-job assignments
5. **Evaluation Service**: Scorecards, ratings, collaborative decision workflows
6. **Communication Service**: Multi-channel messaging (email, SMS), templates, delivery tracking
7. **Interview Service**: Scheduling, calendar sync, feedback collection, meeting coordination
8. **Analytics Service**: Metrics aggregation, reporting, dashboard data
9. **Workflow Engine**: Business process orchestration, automation rules, triggers
10. **Scheduler Service**: Recurring jobs, follow-ups, reminders, background tasks
11. **Integration Hub**: External system connectors, webhooks, API gateway for third-party integrations

**AI/ML Layer (4 components):**
1. **Matching Engine**: Proprietary candidate-job scoring algorithm with semantic analysis
2. **CV Parser**: Structured data extraction from resumes (PDF, DOC, DOCX)
3. **Insights Generator**: Predictions, recommendations, pattern detection, anomaly identification
4. **NLP Service**: Sentiment analysis, entity extraction, text classification

**Technology Stack:**

*Frontend:*
- **Framework**: React 18+ with TypeScript
- **State Management**: Redux Toolkit
- **UI Library**: Material-UI (MUI)
- **Server State**: React Query (TanStack Query)
- **Real-time**: WebSocket for live updates
- **Build Tool**: Webpack / Vite
- **Testing**: Jest, React Testing Library, Cypress (E2E)

*Backend Services:*
- **API Services**: Node.js with Express or Fastify
- **AI/ML Services**: Python with FastAPI
- **Primary Database**: PostgreSQL 14+ (transactional data)
- **Cache**: Redis 7+ (session storage, distributed cache)
- **Search**: ElasticSearch 8+ (full-text search, faceted filtering)
- **Object Storage**: AWS S3 / GCP Cloud Storage (resumes, attachments)
- **Message Queue**: RabbitMQ (async event processing)

*AI/ML Stack:*
- **ML Frameworks**: TensorFlow / PyTorch
- **NLP**: Hugging Face Transformers, spaCy
- **Custom Models**: Trained models for candidate matching and screening

*Infrastructure:*
- **Containerization**: Docker
- **Orchestration**: Kubernetes (EKS / GKE)
- **Cloud**: AWS / GCP (multi-cloud support)
- **IaC**: Terraform
- **CI/CD**: GitHub Actions
- **Monitoring**: Prometheus + Grafana
- **Logging**: ELK Stack (Elasticsearch, Logstash, Kibana)
- **Tracing**: Jaeger (distributed tracing)

**Data Layer:**
- **PostgreSQL**: Primary transactional database with ACID guarantees
- **Redis**: Distributed cache for session management and hot data
- **ElasticSearch**: Full-text search index for candidates, jobs, and applications
- **S3 Object Storage**: Resume files, attachments, exports
- **Data Warehouse**: (Snowflake / BigQuery) for historical analytics and reporting

**Key Integration Requirements (from PRD Section 3.8):**
1. **HRIS**: BambooHR, Workday, SAP SuccessFactors (employee data sync, SSO)
2. **Calendars**: Google Calendar, Outlook (availability, scheduling, meeting creation)
3. **Communication**: Slack, Microsoft Teams (notifications, approvals, slash commands)
4. **Job Boards**: LinkedIn, Indeed, Glassdoor (automated posting)
5. **Background Checks**: Checkr, Sterling (verification automation)
6. **Assessments**: Codility, HackerRank (technical testing)
7. **RESTful API**: Public API with OAuth 2.0, rate limiting, webhooks, SDKs

**Non-Functional Requirements:**
- API response time: <200ms (95th percentile)
- Support: 10,000 concurrent users
- Uptime: 99.9% SLA
- Data volume: 10M candidate profiles, 1M active applications
- Security: AES-256 encryption at rest, TLS 1.3 in transit, MFA, RBAC
- Compliance: GDPR, CCPA, SOC 2 Type II

### Available Inputs
You have access to (or will receive):
- **LTI ATS PRD** (`lti_ats_prd.md`) - comprehensive product requirements
- **Product Roadmap** (optional) - strategic phases and timelines
- **Epics & Features** (optional) - hierarchical functional breakdown
- **User Stories** (optional) - INVEST-compliant stories with acceptance criteria
- **Product Backlog** (optional) - prioritized backlog items

## Task
Generate a **complete, detailed set of engineering work tickets** required to build the LTI ATS system as described in the PRD and supporting documentation.

These tickets must be:
- **Immediately actionable**: Developers can start work without clarification
- **Technically detailed**: Specific APIs, schemas, services, integrations
- **Fully testable**: Clear acceptance criteria and testing requirements
- **Properly organized**: Grouped by epic, feature, component, and ticket type

---

## Ticket Structure Requirements

### 1. Ticket Metadata (Mandatory for Each Ticket)

- **Ticket ID**: Format `LTI-XXX` (sequential numbering)
- **Title**: Clear, descriptive, action-oriented (e.g., "Implement Job Requisition Creation API")
- **Type**: Choose one:
  - `Backend` - API, business logic, data processing
  - `Frontend` - UI components, pages, user interactions
  - `API` - REST endpoints, GraphQL, WebSocket
  - `Database` - Schema changes, migrations, indexes
  - `DevOps` - Infrastructure, deployment, monitoring
  - `QA` - Test automation, test plans
  - `Spike` - Research, POC, investigation
  - `Technical Design` - Architecture, design documents
  - `Integration` - Third-party system connections
  - `AI/ML` - Model training, ML pipeline
- **Priority**: High / Medium / Low (based on P0/P1/P2 from PRD)
- **Effort Estimate**: Story points (Fibonacci: 1, 2, 3, 5, 8, 13) or T-shirt size (XS, S, M, L, XL)
- **Epic**: Which epic this ticket belongs to (from prompt-epics output)
- **Feature**: Which feature this implements (from prompt-epics output)
- **Component**: Technical component (e.g., Auth Service, Candidate Service, React UI)
- **Assignee**: Suggested role (e.g., Backend Engineer, Frontend Engineer, DevOps Engineer)

---

### 2. Description (Comprehensive Context)

Write a complete description including:

- **What needs to be built**: Specific deliverable (API endpoint, UI component, database table, etc.)
- **Why it exists**: Business value, user need, technical requirement
- **Expected outcome**: What success looks like
- **Business rules**: Relevant rules from PRD (validation, workflow, permissions)
- **Constraints**: Technical limitations, performance requirements, security needs
- **Assumptions**: What is assumed to be in place or true

**Format:**
```
## Context
[Business context and user need]

## Objective
[What this ticket accomplishes]

## Business Rules
- [Rule 1]
- [Rule 2]

## Technical Scope
[What will be built - specific components, files, services]

## Constraints
- [Constraint 1: e.g., Must support 10K concurrent users]
- [Constraint 2: e.g., API response time <200ms]
```

---

### 3. Technical Requirements (Deeply Detailed)

Provide specific technical implementation details:

**For Backend Tickets:**
- **API Endpoints**: HTTP method, path, request/response schemas  
  ```
  POST /api/v1/jobs
  Request: { title, description, department_id, salary_range, ... }
  Response: { id, status, created_at, ... }
  ```
- **Service Logic**: Business logic, validation rules, error handling
- **Database Changes**: Tables, columns, indexes, constraints, migrations
- **Authentication**: Required permissions, RBAC roles
- **External Calls**: Third-party APIs, message queue events
- **Caching**: Redis keys, TTL, invalidation strategy
- **Logging**: What to log, log levels, structured logging format

**For Frontend Tickets:**
- **Components**: React components to create/modify
- **State Management**: Redux slices, actions, selectors
- **API Integration**: API calls, React Query hooks
- **UI/UX**: Wireframes, design specs, Material-UI components
- **Routing**: React Router paths, navigation
- **Validation**: Form validation, error handling
- **Accessibility**: WCAG 2.1 AA compliance requirements

**For Database Tickets:**
- **Schema Changes**: DDL statements (CREATE TABLE, ALTER TABLE)
- **Migrations**: Migration scripts (up/down)
- **Indexes**: Index creation for performance
- **Constraints**: Foreign keys, unique constraints, check constraints
- **Data Seeding**: Initial data or migration scripts

**For DevOps Tickets:**
- **Infrastructure**: Kubernetes manifests, Terraform modules
- **CI/CD**: GitHub Actions workflows, deployment pipelines
- **Monitoring**: Prometheus metrics, Grafana dashboards
- **Logging**: ELK stack configuration, log forwarding
- **Security**: Secrets management, network policies, RBAC

**For Integration Tickets:**
- **Third-Party API**: Authentication method (OAuth, API key)
- **Data Mapping**: How to map external data to internal models
- **Error Handling**: Retry logic, circuit breakers, fallbacks
- **Webhooks**: Event subscriptions, payload handling
- **Rate Limiting**: Respect third-party limits

---

### 4. Acceptance Criteria (Gherkin Format)

Use structured **Given-When-Then** scenarios:

```
**AC1: [Scenario name]**
Given [initial state and preconditions]
When [user action or system event]
Then [expected outcome and system state]

**AC2: [Error scenario]**
Given [invalid state or input]
When [action is attempted]
Then [appropriate error is returned with message]

**AC3: [Edge case]**
Given [boundary condition]
When [action occurs]
Then [system handles gracefully]
```

**Minimum 3-5 acceptance criteria per ticket**, covering:
- Happy path (successful flow)
- Error cases (validation failures, permissions, system errors)
- Edge cases (boundary conditions, empty states, race conditions)
- Performance (response time, resource usage)
- Security (authentication, authorization, input sanitization)

---

### 5. Dependencies

List all dependencies with specific references:

**Technical Dependencies:**
- **Prerequisite Tickets**: `LTI-XXX` (must be completed first)
- **Services**: Which microservices must be running
- **APIs**: External or internal APIs required
- **Data**: Required database tables, seed data, migrations
- **Infrastructure**: Kubernetes cluster, databases, message queues

**External Dependencies:**
- **Third-Party Systems**: LinkedIn API, Google Calendar API, etc.
- **Credentials**: API keys, OAuth tokens, service accounts
- **Vendor Availability**: SLAs, maintenance windows

**Execution Order:**
- **Sequential**: Tickets that must be done in order
- **Parallel**: Tickets that can be worked on simultaneously
- **Blocking**: Tickets that block other work

---

### 6. Definition of Done (Comprehensive Checklist)

Standard DoD for all tickets:

- [ ] **Code Complete**: All code written and committed
- [ ] **Code Review**: Peer reviewed and approved
- [ ] **Unit Tests**: Written with >80% code coverage
- [ ] **Integration Tests**: API/service integration tests passing
- [ ] **E2E Tests** (if UI): Cypress tests for user flows
- [ ] **Documentation**: API docs, code comments, README updated
- [ ] **Security Review**: No vulnerabilities, input sanitization, auth checks
- [ ] **Performance Tested**: Meets NFR requirements (<200ms API response)
- [ ] **QA Validated**: Tested in staging environment
- [ ] **Acceptance Criteria**: All ACs met and verified
- [ ] **Migration Scripts**: Database migrations tested (up/down)
- [ ] **Monitoring**: Logs, metrics, and alerts configured
- [ ] **Product Owner Approval**: PO has accepted the work
- [ ] **Merged to Main**: Code merged via PR to main/master branch
- [ ] **Deployed**: Successfully deployed to production (or ready for deployment)

Add ticket-specific DoD items as needed.

---

### 7. Additional Sections

**Risks:**
- Technical risks (e.g., integration complexity, performance bottlenecks)
- Third-party risks (e.g., API availability, rate limits)
- Security risks (e.g., data exposure, injection attacks)

**Assumptions:**
- What is assumed to be in place or true
- Decisions made in absence of complete information

**Notes for Engineering:**
- Implementation hints
- Suggested approaches
- Known gotchas or challenges
- Links to relevant documentation or code examples

**Testing Strategy:**
- Unit test approach
- Integration test scenarios
- E2E test flows
- Performance test plan
- Security test considerations

---

## Ticket Organization Requirements

### Group Tickets By:

1. **Epic & Feature**: Organize by functional area (from prompt-epics)
2. **Component**: Technical component (Auth Service, UI, Database, etc.)
3. **Sprint/Phase**: Suggested sprint assignments based on dependencies
4. **Type**: Backend, Frontend, API, Database, DevOps, QA, Integration, AI/ML

### Ticket Types to Generate:

- **Backend Tickets**: API endpoints, business logic, service implementations
- **Frontend Tickets**: UI components, pages, forms, dashboards
- **API Tickets**: REST endpoint definitions, request/response schemas, authentication
- **Database Tickets**: Schema creation, migrations, indexes, constraints
- **DevOps Tickets**: Kubernetes setup, CI/CD pipelines, monitoring, logging
- **QA Tickets**: Test automation (unit, integration, E2E), test plans
- **Integration Tickets**: Third-party system connections (HRIS, calendars, job boards)
- **AI/ML Tickets**: Model training, CV parsing, matching algorithm, NLP services
- **Spike Tickets**: Research tasks, POCs, technology evaluation
- **Technical Design Tickets**: Architecture documents, API designs, data models

---

## Output Format

Provide tickets in the following structure:

```md
# Engineering Work Tickets — LTI ATS

## Summary
- Total tickets: <count>
- By type: Backend (X), Frontend (Y), DevOps (Z), etc.
- By priority: High (X), Medium (Y), Low (Z)
- Estimated total effort: <story points>

---

## Tickets Grouped by Epic

### Epic 1: <Epic Name>

#### Feature 1.1: <Feature Name>

##### LTI-001: <Ticket Title>
**Type:** Backend | **Priority:** High | **Effort:** 5 pts | **Component:** Job Management Service

**Description:**
[Full description as specified above]

**Technical Requirements:**
[Detailed technical specs]

**Acceptance Criteria:**
[Gherkin scenarios]

**Dependencies:**
[Listed dependencies]

**Definition of Done:**
[DoD checklist]

**Risks:**
[Risk list]

**Notes:**
[Engineering notes]

---

##### LTI-002: <Next Ticket>
...

---

## Tickets Grouped by Type

### Backend Tickets
- **LTI-001**: [Title]
- **LTI-015**: [Title]
...

### Frontend Tickets
- **LTI-032**: [Title]
...

---

## Sprint Planning Suggestion

### Sprint 1 (MVP Core - Foundation)
- LTI-001, LTI-002, LTI-003 (Database setup, Auth service, Core APIs)

### Sprint 2 (Job Management)
- LTI-010, LTI-011, LTI-012 (Job CRUD, UI, Publishing)

---

## Flat Table of All Tickets (Import-Friendly CSV Format)

| ID | Title | Type | Priority | Effort | Epic | Feature | Dependencies |
|----|-------|------|----------|--------|------|---------|--------------|
| LTI-001 | Setup PostgreSQL schema | Database | High | 3 | Infrastructure | Data Layer | None |
| LTI-002 | Implement Auth Service | Backend | High | 8 | Authentication | User Login | LTI-001 |
...

```

---

## Final Instruction

**Step 1:** Read and analyze the LTI ATS PRD (`lti_ats_prd.md`) thoroughly

**Step 2:** Summarize the technical architecture, core services, and technology stack in 3–5 sentences to confirm understanding

**Step 3:** Generate the **comprehensive set of engineering work tickets** following the exact structure specified above, ensuring:
- Every ticket is actionable and detailed
- All 8 feature domains are covered
- Infrastructure, security, and observability are included
- Tickets are properly sequenced with clear dependencies
- Both functional and non-functional requirements are addressed

**Step 4:** Organize tickets for easy consumption by engineering teams, product managers, and project managers
