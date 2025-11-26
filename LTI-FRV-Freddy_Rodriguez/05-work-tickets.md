# Engineering Work Tickets — LTI ATS

**Version:** 1.0  
**Date:** November 25, 2025  
**Owner:** Engineering Team

---

## Executive Summary

This document provides a comprehensive set of implementation-ready engineering work tickets for the LTI ATS system. These tickets translate the Product Backlog, User Stories, and Epics into detailed technical tasks that development teams can execute immediately.

### Technical Architecture Summary

**LTI ATS** employs a microservices architecture with 11 core services, 4 AI/ML components, and comprehensive integration capabilities:

- **11 Core Microservices**: Auth, Job Management, Candidate, Application, Evaluation, Communication, Interview, Analytics, Workflow Engine, Scheduler, Integration Hub
- **AI/ML Stack**: CV Parser (NLP), Matching Engine (ML), Insights Generator, NLP Service (sentiment analysis)
- **Technology Stack**: React 18+ (Frontend), Node.js/Express + Python/FastAPI (Backend), PostgreSQL (Database), Redis (Cache), ElasticSearch (Search), Kubernetes (Orchestration)
- **Infrastructure**: Docker containers, Kubernetes (EKS/GKE), Terraform (IaC), GitHub Actions (CI/CD), Prometheus/Grafana (Monitoring)

### Ticket Summary

- **Total tickets**: 75
- **By type**: 
  - Backend: 18 tickets
  - Frontend: 15 tickets
  - Database: 8 tickets
  - AI/ML: 10 tickets
  - DevOps: 8 tickets
  - Integration: 8 tickets
  - QA: 6 tickets
  - Spike: 2 tickets
- **By priority**: 
  - High: 42 tickets (56%)
  - Medium: 25 tickets (33%)
  - Low: 8 tickets (11%)
- **Estimated total effort**: 485 story points (~24 sprints at 20 points/sprint)

---

## Tickets Grouped by Epic

### Epic 1: Job Lifecycle Management

#### Feature F-001: Intelligent Job Requisition Creation

##### LTI-001: Setup PostgreSQL Database Schema
**Type:** Database | **Priority:** High | **Effort:** 13 pts | **Component:** PostgreSQL

**Description:**

## Context
The LTI ATS system requires a robust, scalable relational database to store all core entities including jobs, candidates, applications, evaluations, and users. PostgreSQL 14+ provides ACID guarantees, JSON support, and excellent performance for our use case.

## Objective
Design and implement the complete database schema for LTI ATS including all tables, relationships, indexes, and constraints as defined in the PRD Section 5 (Data Model).

## Business Rules
- All primary keys must be UUIDs for distributed system compatibility
- Soft deletes for GDPR compliance (retain audit trail)
- Timestamps (created_at, updated_at) on all tables
- Foreign key constraints with appropriate CASCADE/RESTRICT rules
- JSON columns for flexible, evolving data structures (skills, metadata)

## Technical Scope
Create PostgreSQL schema with 15+ core tables, indexes for performance, and migration scripts for version control.

## Constraints
- Must support 10M candidate profiles
- Query performance <50ms for indexed lookups
- ACID compliance for all transactions

**Technical Requirements:**

**Database Tables:**
```sql
-- Core tables to create:
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  first_name VARCHAR(100) NOT NULL,
  last_name VARCHAR(100) NOT NULL,
  role VARCHAR(50) NOT NULL CHECK (role IN ('admin', 'recruiter', 'hiring-manager', 'interviewer')),
  department_id UUID REFERENCES departments(id),
  is_active BOOLEAN DEFAULT true,
  permissions JSONB,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  last_login TIMESTAMP
);

CREATE TABLE jobs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  title VARCHAR(255) NOT NULL,
  description TEXT,
  department_id UUID REFERENCES departments(id),
  hiring_manager_id UUID REFERENCES users(id) NOT NULL,
  location VARCHAR(255) NOT NULL,
  employment_type VARCHAR(50) NOT NULL CHECK (employment_type IN ('full-time', 'part-time', 'contract')),
  salary_range_min DECIMAL(12,2),
  salary_range_max DECIMAL(12,2),
  required_skills JSONB,
  preferred_skills JSONB,
  status VARCHAR(50) DEFAULT 'draft' CHECK (status IN ('draft', 'open', 'on-hold', 'closed')),
  requisition_number VARCHAR(50) UNIQUE,
  openings_count INTEGER DEFAULT 1,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  published_at TIMESTAMP,
  closed_at TIMESTAMP
);

CREATE TABLE candidates (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  first_name VARCHAR(100) NOT NULL,
  last_name VARCHAR(100) NOT NULL,
  phone VARCHAR(20),
  location VARCHAR(255),
  resume_url VARCHAR(500),
  linkedin_url VARCHAR(500),
  portfolio_url VARCHAR(500),
  years_of_experience INTEGER,
  current_company VARCHAR(255),
  current_title VARCHAR(255),
  skills JSONB,
  education JSONB,
  work_history JSONB,
  source VARCHAR(100),
  gdpr_consent BOOLEAN DEFAULT false,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  last_activity TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE applications (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  job_id UUID REFERENCES jobs(id) NOT NULL,
  candidate_id UUID REFERENCES candidates(id) NOT NULL,
  stage_id UUID REFERENCES stages(id) NOT NULL,
  assigned_recruiter_id UUID REFERENCES users(id),
  ai_match_score DECIMAL(5,2),
  overall_rating DECIMAL(3,2),
  status VARCHAR(50) DEFAULT 'active' CHECK (status IN ('active', 'hired', 'rejected', 'withdrawn')),
  applied_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  last_stage_change TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  rejection_reason_id UUID REFERENCES rejection_reasons(id),
  offer_extended_at TIMESTAMP,
  offer_accepted_at TIMESTAMP,
  UNIQUE(job_id, candidate_id)
);

-- Additional tables: stages, evaluations, interviews, communications, ai_insights, etc.
```

**Indexes:**
```sql
CREATE INDEX idx_jobs_status ON jobs(status);
CREATE INDEX idx_jobs_hiring_manager ON jobs(hiring_manager_id);
CREATE INDEX idx_candidates_email ON candidates(email);
CREATE INDEX idx_candidates_skills ON candidates USING GIN(skills);
CREATE INDEX idx_applications_job ON applications(job_id);
CREATE INDEX idx_applications_candidate ON applications(candidate_id);
CREATE INDEX idx_applications_stage ON applications(stage_id);
CREATE INDEX idx_applications_status ON applications(status);
```

**Migration Scripts:**
- Use Flyway or Liquibase for version-controlled migrations
- Create up/down migration scripts
- Seed data for development environment

**Acceptance Criteria:**

**AC1: All core tables created successfully**
Given the migration scripts are executed
When the database is initialized
Then all 15+ core tables exist with correct schemas
And all foreign key constraints are properly defined
And all indexes are created

**AC2: Data integrity constraints enforced**
Given a user attempts to insert invalid data
When the INSERT statement violates a constraint (e.g., invalid enum value)
Then the database rejects the operation with appropriate error
And the transaction is rolled back

**AC3: Performance requirements met**
Given the database contains 10M candidate records
When a query uses indexed columns (e.g., SELECT * FROM candidates WHERE email = 'test@example.com')
Then the query completes in <50ms
And EXPLAIN ANALYZE shows index usage

**AC4: JSON columns support flexible data**
Given a job has custom required_skills
When the skills are stored as JSONB
Then the data can be queried using JSON operators (e.g., skills @> '{"skill": "Python"}')
And the data can be updated without schema changes

**AC5: Migration scripts are idempotent**
Given migration scripts exist
When migrations are run multiple times
Then the database reaches the same final state
And no errors occur on subsequent runs

**Dependencies:**
- **Technical**: PostgreSQL 14+ installed, database server configured
- **Infrastructure**: Database credentials, connection pooling setup
- **Prerequisite Tickets**: None (foundational)

**Definition of Done:**
- [ ] All database tables created with correct schemas
- [ ] All indexes created for performance optimization
- [ ] Foreign key constraints properly defined
- [ ] Migration scripts created and tested (up/down)
- [ ] Seed data scripts for development environment
- [ ] Database documentation (ERD diagram, table descriptions)
- [ ] Performance tested with 10M records
- [ ] Code review completed
- [ ] Merged to main branch

**Risks:**
- **Performance**: Large JSONB columns may impact query performance - mitigation: use GIN indexes
- **Migration Complexity**: Schema changes in production require careful planning - mitigation: test migrations in staging first

**Notes for Engineering:**
- Use UUID v4 for all primary keys (gen_random_uuid())
- Consider partitioning for large tables (applications, communications) if needed
- Set up connection pooling (PgBouncer) for production
- Enable query logging for slow queries (>100ms)

---

##### LTI-002: Implement Auth Service (JWT, RBAC, MFA)
**Type:** Backend | **Priority:** High | **Effort:** 13 pts | **Component:** Auth Service

**Description:**

## Context
The Auth Service is the security foundation of LTI ATS, responsible for user authentication, authorization, session management, and role-based access control. All other services depend on this for security.

## Objective
Build a secure authentication and authorization service supporting JWT tokens, multi-factor authentication (MFA), role-based access control (RBAC), and OAuth 2.0 for third-party integrations.

## Business Rules
- All users must authenticate before accessing the system
- MFA required for admin and recruiter roles
- JWT tokens expire after 1 hour, refresh tokens after 30 days
- RBAC with 4 roles: admin, recruiter, hiring-manager, interviewer
- Password requirements: min 12 characters, uppercase, lowercase, number, special char
- Account lockout after 5 failed login attempts

## Technical Scope
Node.js/Express service with JWT authentication, bcrypt password hashing, RBAC middleware, MFA (TOTP), and OAuth 2.0 support.

**Technical Requirements:**

**API Endpoints:**
```
POST /api/v1/auth/register
Request: { email, password, first_name, last_name, role }
Response: { user_id, email, role, created_at }

POST /api/v1/auth/login
Request: { email, password, mfa_code? }
Response: { access_token, refresh_token, user: { id, email, role, permissions } }

POST /api/v1/auth/refresh
Request: { refresh_token }
Response: { access_token }

POST /api/v1/auth/logout
Request: { refresh_token }
Response: { success: true }

POST /api/v1/auth/mfa/setup
Response: { qr_code, secret }

POST /api/v1/auth/mfa/verify
Request: { code }
Response: { verified: true }

GET /api/v1/auth/me
Response: { id, email, role, permissions, department }
```

**Service Logic:**
- Password hashing with bcrypt (cost factor 12)
- JWT token generation with RS256 algorithm
- Refresh token rotation on use
- MFA using TOTP (Time-based One-Time Password) with speakeasy library
- RBAC middleware checking permissions on protected routes
- Rate limiting: 5 login attempts per 15 minutes per IP

**Database Changes:**
```sql
CREATE TABLE refresh_tokens (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) NOT NULL,
  token_hash VARCHAR(255) UNIQUE NOT NULL,
  expires_at TIMESTAMP NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  revoked_at TIMESTAMP
);

CREATE TABLE mfa_secrets (
  user_id UUID PRIMARY KEY REFERENCES users(id),
  secret VARCHAR(255) NOT NULL,
  enabled BOOLEAN DEFAULT false,
  backup_codes JSONB,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE login_attempts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) NOT NULL,
  ip_address INET NOT NULL,
  success BOOLEAN NOT NULL,
  attempted_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**Authentication:**
- JWT access tokens with 1-hour expiration
- Refresh tokens with 30-day expiration
- Public/private key pair for JWT signing (RS256)

**Caching:**
- Cache user permissions in Redis (TTL: 5 minutes)
- Cache revoked tokens in Redis for fast validation

**Logging:**
- Log all authentication events (login, logout, failed attempts)
- Log MFA setup and verification events
- Structured logging with user_id, ip_address, timestamp

**Acceptance Criteria:**

**AC1: User registration with password hashing**
Given a new user provides valid registration data
When POST /api/v1/auth/register is called
Then the user account is created
And the password is hashed with bcrypt
And a 201 Created response is returned with user details (excluding password)

**AC2: Successful login with JWT tokens**
Given a registered user provides correct email and password
When POST /api/v1/auth/login is called
Then an access_token (JWT) and refresh_token are returned
And the access_token contains user_id, email, role in payload
And the access_token expires in 1 hour

**AC3: MFA enforcement for admin/recruiter roles**
Given a user with admin or recruiter role has MFA enabled
When POST /api/v1/auth/login is called without mfa_code
Then a 403 Forbidden response is returned with message "MFA required"
And login succeeds only when valid mfa_code is provided

**AC4: Token refresh mechanism**
Given a valid refresh_token
When POST /api/v1/auth/refresh is called
Then a new access_token is returned
And the old refresh_token is rotated (new refresh_token issued)

**AC5: RBAC middleware protects routes**
Given a user with role "interviewer" attempts to access admin-only route
When the request includes a valid JWT
Then the middleware returns 403 Forbidden
And the error message indicates insufficient permissions

**AC6: Account lockout after failed attempts**
Given a user has 5 consecutive failed login attempts
When the 6th login attempt is made
Then the account is locked for 15 minutes
And a 429 Too Many Requests response is returned

**Dependencies:**
- **Technical**: PostgreSQL (users table), Redis (token cache), Node.js 18+
- **Libraries**: jsonwebtoken, bcrypt, speakeasy (MFA), express-rate-limit
- **Prerequisite Tickets**: LTI-001 (Database schema)

**Definition of Done:**
- [ ] All API endpoints implemented and tested
- [ ] Unit tests with >80% coverage
- [ ] Integration tests for auth flows
- [ ] Password hashing with bcrypt (cost 12)
- [ ] JWT token generation and validation
- [ ] MFA setup and verification working
- [ ] RBAC middleware protecting routes
- [ ] Rate limiting implemented
- [ ] Logging configured (Winston/Bunyan)
- [ ] API documentation (OpenAPI/Swagger)
- [ ] Security review completed (OWASP Top 10)
- [ ] Code review approved
- [ ] Deployed to staging and tested

**Risks:**
- **Security**: JWT secret compromise - mitigation: use RS256 with key rotation
- **Performance**: bcrypt hashing may be slow - mitigation: use async hashing, consider Argon2
- **MFA Adoption**: Users may resist MFA - mitigation: provide clear setup instructions

**Notes for Engineering:**
- Store JWT signing keys in environment variables or secret manager
- Use helmet.js for security headers
- Implement CORS properly for frontend integration
- Consider using Passport.js for OAuth 2.0 integrations

---

##### LTI-003: Build Job Management Service API
**Type:** Backend | **Priority:** High | **Effort:** 13 pts | **Component:** Job Management Service

**Description:**

## Context
The Job Management Service handles the complete lifecycle of job requisitions from creation through approval, publishing, and closure. This is a core service that recruiters and hiring managers interact with daily.

## Objective
Implement RESTful API for job CRUD operations, approval workflows, multi-channel publishing, and market intelligence integration.

## Business Rules
- Only recruiters and admins can create jobs
- Jobs require hiring manager approval before publishing
- Approval workflows are configurable per department
- Jobs can be published to multiple channels simultaneously
- Draft jobs are auto-saved every 30 seconds
- Closed jobs are archived after 90 days

**Technical Requirements:**

**API Endpoints:**
```
POST /api/v1/jobs
Request: { title, description, department_id, hiring_manager_id, location, employment_type, salary_range, required_skills, preferred_skills }
Response: { id, status: 'draft', created_at, ... }

GET /api/v1/jobs
Query: ?status=open&department_id=uuid&page=1&limit=20
Response: { jobs: [...], total, page, limit }

GET /api/v1/jobs/:id
Response: { id, title, description, status, applications_count, ... }

PUT /api/v1/jobs/:id
Request: { title?, description?, ... }
Response: { id, updated_at, ... }

DELETE /api/v1/jobs/:id (soft delete)
Response: { success: true }

POST /api/v1/jobs/:id/submit-for-approval
Response: { id, status: 'pending-approval', submitted_at }

POST /api/v1/jobs/:id/approve
Request: { approver_id, comments? }
Response: { id, status: 'approved', approved_at, approved_by }

POST /api/v1/jobs/:id/reject
Request: { approver_id, reason }
Response: { id, status: 'draft', rejection_reason }

POST /api/v1/jobs/:id/publish
Request: { channels: ['linkedin', 'indeed', 'careers-page'] }
Response: { id, status: 'open', published_at, publishing_results: [...] }

POST /api/v1/jobs/:id/close
Request: { reason }
Response: { id, status: 'closed', closed_at }
```

**Service Logic:**
- Validate required fields and business rules
- Trigger approval workflow based on department configuration
- Integrate with job board APIs for publishing
- Send notifications to hiring managers on status changes
- Track job performance metrics (views, applications)

**Database Changes:**
```sql
CREATE TABLE job_approvals (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  job_id UUID REFERENCES jobs(id) NOT NULL,
  approver_id UUID REFERENCES users(id) NOT NULL,
  status VARCHAR(50) NOT NULL CHECK (status IN ('pending', 'approved', 'rejected')),
  comments TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  decided_at TIMESTAMP
);

CREATE TABLE job_publications (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  job_id UUID REFERENCES jobs(id) NOT NULL,
  channel VARCHAR(100) NOT NULL,
  external_id VARCHAR(255),
  status VARCHAR(50) NOT NULL,
  published_at TIMESTAMP,
  error_message TEXT
);
```

**External Calls:**
- LinkedIn Jobs API for posting
- Indeed API for posting
- Company careers page API

**Caching:**
- Cache active jobs list in Redis (TTL: 5 minutes)
- Invalidate cache on job updates

**Logging:**
- Log all job state transitions
- Log approval decisions with approver details
- Log publishing attempts and results

**Acceptance Criteria:**

**AC1: Create job requisition**
Given a recruiter provides valid job data
When POST /api/v1/jobs is called
Then a new job is created with status 'draft'
And the job is assigned a unique requisition_number
And a 201 Created response is returned

**AC2: Submit job for approval**
Given a job in 'draft' status
When POST /api/v1/jobs/:id/submit-for-approval is called
Then the job status changes to 'pending-approval'
And the hiring manager receives an email notification
And an approval record is created

**AC3: Approve job requisition**
Given a job in 'pending-approval' status
When the hiring manager calls POST /api/v1/jobs/:id/approve
Then the job status changes to 'approved'
And the recruiter receives a notification
And the job is ready for publishing

**AC4: Publish job to multiple channels**
Given an approved job
When POST /api/v1/jobs/:id/publish is called with channels ['linkedin', 'indeed']
Then the job is posted to LinkedIn and Indeed
And job_publications records are created for each channel
And the job status changes to 'open'
And publishing results indicate success/failure per channel

**AC5: Reject job with reason**
Given a job in 'pending-approval' status
When the hiring manager calls POST /api/v1/jobs/:id/reject with reason
Then the job status returns to 'draft'
And the recruiter receives notification with rejection reason
And the job can be edited and resubmitted

**Dependencies:**
- **Technical**: PostgreSQL, Redis, LinkedIn API, Indeed API
- **Data**: Approval workflow configurations
- **Prerequisite Tickets**: LTI-001 (Database), LTI-002 (Auth Service)

**Definition of Done:**
- [ ] All CRUD endpoints implemented
- [ ] Approval workflow logic implemented
- [ ] Job board API integrations (LinkedIn, Indeed)
- [ ] Unit tests >80% coverage
- [ ] Integration tests for workflows
- [ ] API documentation (OpenAPI spec)
- [ ] Error handling for external API failures
- [ ] Caching implemented
- [ ] Logging configured
- [ ] Code review approved
- [ ] Deployed to staging

**Risks:**
- **External API Failures**: Job board APIs may be down - mitigation: retry logic, fallback queue
- **Approval Bottlenecks**: Hiring managers may delay approvals - mitigation: SLA tracking, escalation

---

##### LTI-004: Build React Frontend Architecture
**Type:** Frontend | **Priority:** High | **Effort:** 13 pts | **Component:** React UI

**Description:**

## Context
The frontend is the primary interface for recruiters, hiring managers, and candidates. It must be fast, responsive, accessible, and provide an excellent user experience.

## Objective
Set up the React 18+ frontend architecture with TypeScript, Redux Toolkit, Material-UI, React Query, and WebSocket support for real-time updates.

## Technical Scope
Create the foundational frontend architecture including project structure, state management, routing, API integration, and UI component library.

**Technical Requirements:**

**Project Setup:**
```bash
npx create-react-app lti-ats-frontend --template typescript
# or
npm create vite@latest lti-ats-frontend -- --template react-ts
```

**Dependencies:**
```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "typescript": "^5.0.0",
    "@reduxjs/toolkit": "^1.9.0",
    "react-redux": "^8.0.0",
    "@tanstack/react-query": "^4.0.0",
    "@mui/material": "^5.11.0",
    "@mui/icons-material": "^5.11.0",
    "react-router-dom": "^6.8.0",
    "axios": "^1.3.0",
    "socket.io-client": "^4.5.0",
    "formik": "^2.2.9",
    "yup": "^1.0.0",
    "date-fns": "^2.29.0"
  }
}
```

**Project Structure:**
```
src/
├── components/        # Reusable UI components
│   ├── common/       # Buttons, Inputs, Cards, etc.
│   ├── layout/       # Header, Sidebar, Footer
│   └── features/     # Feature-specific components
├── pages/            # Page components (routes)
│   ├── Jobs/
│   ├── Candidates/
│   ├── Pipeline/
│   └── Analytics/
├── store/            # Redux store configuration
│   ├── slices/       # Redux slices (auth, jobs, candidates)
│   └── index.ts
├── services/         # API service layer
│   ├── api.ts        # Axios instance
│   ├── auth.ts
│   ├── jobs.ts
│   └── candidates.ts
├── hooks/            # Custom React hooks
├── utils/            # Utility functions
├── types/            # TypeScript type definitions
└── App.tsx
```

**State Management (Redux Toolkit):**
```typescript
// store/slices/authSlice.ts
import { createSlice, PayloadAction } from '@reduxjs/toolkit';

interface AuthState {
  user: User | null;
  accessToken: string | null;
  isAuthenticated: boolean;
}

const authSlice = createSlice({
  name: 'auth',
  initialState: { user: null, accessToken: null, isAuthenticated: false } as AuthState,
  reducers: {
    setCredentials: (state, action: PayloadAction<{ user: User; accessToken: string }>) => {
      state.user = action.payload.user;
      state.accessToken = action.payload.accessToken;
      state.isAuthenticated = true;
    },
    logout: (state) => {
      state.user = null;
      state.accessToken = null;
      state.isAuthenticated = false;
    }
  }
});
```

**API Integration (React Query):**
```typescript
// hooks/useJobs.ts
import { useQuery, useMutation } from '@tanstack/react-query';
import { jobsApi } from '../services/jobs';

export const useJobs = (filters?: JobFilters) => {
  return useQuery(['jobs', filters], () => jobsApi.getJobs(filters));
};

export const useCreateJob = () => {
  return useMutation((jobData: CreateJobRequest) => jobsApi.createJob(jobData));
};
```

**Routing:**
```typescript
// App.tsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/login" element={<LoginPage />} />
        <Route path="/" element={<ProtectedRoute><Dashboard /></ProtectedRoute>} />
        <Route path="/jobs" element={<ProtectedRoute><JobsPage /></ProtectedRoute>} />
        <Route path="/jobs/:id" element={<ProtectedRoute><JobDetailPage /></ProtectedRoute>} />
        <Route path="/candidates" element={<ProtectedRoute><CandidatesPage /></ProtectedRoute>} />
        <Route path="/pipeline/:jobId" element={<ProtectedRoute><PipelinePage /></ProtectedRoute>} />
      </Routes>
    </BrowserRouter>
  );
}
```

**WebSocket Integration:**
```typescript
// services/websocket.ts
import io from 'socket.io-client';

export const socket = io(process.env.REACT_APP_WS_URL, {
  auth: { token: localStorage.getItem('accessToken') }
});

socket.on('candidate:updated', (data) => {
  // Invalidate React Query cache
  queryClient.invalidateQueries(['candidates', data.candidateId]);
});
```

**Acceptance Criteria:**

**AC1: Project builds successfully**
Given the frontend project is set up
When npm run build is executed
Then the build completes without errors
And optimized production assets are generated in /build or /dist

**AC2: Redux store configured**
Given the Redux store is configured
When a component dispatches an action (e.g., setCredentials)
Then the global state updates correctly
And connected components re-render with new state

**AC3: API calls work with React Query**
Given the API service is configured
When a component uses useJobs() hook
Then the API request is made to the backend
And loading/error/success states are handled
And data is cached for subsequent requests

**AC4: Routing works correctly**
Given the user navigates to /jobs
When the route is accessed
Then the JobsPage component renders
And protected routes redirect to /login if not authenticated

**AC5: Material-UI theme applied**
Given the MUI theme is configured
When components use MUI components
Then consistent styling is applied across the app
And the theme can be customized (colors, typography)

**Dependencies:**
- **Technical**: Node.js 18+, npm/yarn
- **Backend**: LTI-002 (Auth Service API)
- **Prerequisite Tickets**: None (can be developed in parallel)

**Definition of Done:**
- [ ] React project created with TypeScript
- [ ] Redux Toolkit configured with auth slice
- [ ] React Query configured for API calls
- [ ] React Router configured with protected routes
- [ ] Material-UI theme configured
- [ ] WebSocket client configured
- [ ] Axios instance with auth interceptor
- [ ] Project structure documented
- [ ] Build pipeline working (dev, prod)
- [ ] ESLint and Prettier configured
- [ ] Unit tests for Redux slices
- [ ] Code review approved

---

### Epic 3: AI-Powered Screening & Matching

##### LTI-005: Implement CV Parser (NLP Service)
**Type:** AI/ML | **Priority:** High | **Effort:** 13 pts | **Component:** CV Parser Service

**Description:**

## Context
The CV Parser is a critical AI component that extracts structured data from unstructured resumes in various formats (PDF, DOC, DOCX). This eliminates manual data entry and enables automated candidate screening.

## Objective
Build a Python/FastAPI service using NLP (spaCy, Hugging Face) to parse resumes and extract contact info, education, work history, skills, and certifications with 95%+ accuracy.

## Business Rules
- Support PDF, DOC, DOCX, TXT formats
- Extract: name, email, phone, location, education, work history, skills, certifications
- Handle multiple resume formats (chronological, functional, hybrid)
- Provide confidence scores for extracted fields
- Support English, Spanish, Portuguese, French, German

**Technical Requirements:**

**API Endpoints:**
```python
# FastAPI endpoints
POST /api/v1/cv-parser/parse
Request: multipart/form-data with file upload
Response: {
  "candidate_data": {
    "contact_info": {
      "first_name": "John",
      "last_name": "Doe",
      "email": "john.doe@example.com",
      "phone": "+1-555-0123",
      "location": "San Francisco, CA",
      "confidence": 0.98
    },
    "education": [
      {
        "degree": "Bachelor of Science",
        "field": "Computer Science",
        "institution": "Stanford University",
        "graduation_year": 2018,
        "confidence": 0.95
      }
    ],
    "work_history": [
      {
        "title": "Senior Software Engineer",
        "company": "Google",
        "start_date": "2018-06",
        "end_date": "2023-03",
        "description": "Led development of...",
        "confidence": 0.92
      }
    ],
    "skills": ["Python", "React", "AWS", "Machine Learning"],
    "certifications": ["AWS Certified Solutions Architect"],
    "years_of_experience": 5
  },
  "parsing_metadata": {
    "format": "PDF",
    "pages": 2,
    "processing_time_ms": 1250,
    "overall_confidence": 0.94
  }
}

POST /api/v1/cv-parser/parse-batch
Request: { "file_urls": ["s3://bucket/resume1.pdf", ...] }
Response: { "job_id": "uuid", "status": "processing" }

GET /api/v1/cv-parser/jobs/:job_id
Response: { "status": "completed", "results": [...] }
```

**NLP Pipeline:**
```python
import spacy
from transformers import pipeline

# Load NLP models
nlp = spacy.load("en_core_web_lg")
ner_pipeline = pipeline("ner", model="dslim/bert-base-NER")

def parse_resume(file_path: str) -> dict:
    # 1. Extract text from PDF/DOC
    text = extract_text(file_path)
    
    # 2. Named Entity Recognition for contact info
    doc = nlp(text)
    entities = extract_entities(doc)
    
    # 3. Section detection (Education, Experience, Skills)
    sections = detect_sections(text)
    
    # 4. Parse education section
    education = parse_education(sections['education'])
    
    # 5. Parse work history
    work_history = parse_work_history(sections['experience'])
    
    # 6. Extract skills using keyword matching + NER
    skills = extract_skills(text)
    
    # 7. Calculate confidence scores
    confidence = calculate_confidence(entities, education, work_history)
    
    return {
        "contact_info": entities,
        "education": education,
        "work_history": work_history,
        "skills": skills,
        "confidence": confidence
    }
```

**Libraries:**
- **PDF Parsing**: PyPDF2, pdfplumber
- **DOC Parsing**: python-docx
- **NLP**: spaCy (en_core_web_lg), Hugging Face Transformers
- **Entity Recognition**: Custom NER model fine-tuned on resumes
- **Skills Extraction**: Keyword matching against skills taxonomy

**Database Changes:**
```sql
CREATE TABLE parsed_resumes (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  candidate_id UUID REFERENCES candidates(id),
  file_url VARCHAR(500) NOT NULL,
  parsed_data JSONB NOT NULL,
  confidence_score DECIMAL(5,2),
  parsing_errors JSONB,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**Caching:**
- Cache parsed results in Redis (TTL: 24 hours) to avoid re-parsing

**Logging:**
- Log parsing attempts, success/failure rates
- Log low-confidence extractions for manual review

**Acceptance Criteria:**

**AC1: Parse PDF resume successfully**
Given a standard PDF resume is uploaded
When POST /api/v1/cv-parser/parse is called
Then contact info, education, work history, and skills are extracted
And the overall confidence score is >0.90
And the response is returned in <10 seconds

**AC2: Handle multiple resume formats**
Given resumes in PDF, DOCX, and TXT formats
When each is parsed
Then all formats are successfully processed
And extracted data structure is consistent across formats

**AC3: Extract contact information accurately**
Given a resume contains name, email, phone, location
When the resume is parsed
Then all contact fields are extracted with confidence >0.95
And email format is validated
And phone number is normalized to E.164 format

**AC4: Parse education history**
Given a resume with multiple degrees
When the education section is parsed
Then all degrees are extracted with institution, field, and year
And degrees are ordered by graduation year (most recent first)

**AC5: Extract skills with taxonomy matching**
Given a resume mentions "React.js", "ReactJS", "React"
When skills are extracted
Then all variations are normalized to "React"
And skills are matched against the skills taxonomy
And confidence scores indicate match quality

**AC6: Handle parsing errors gracefully**
Given a corrupted or unreadable file
When parsing is attempted
Then an error response is returned with details
And the error is logged for investigation
And no partial data is saved

**Dependencies:**
- **Technical**: Python 3.10+, FastAPI, spaCy, Hugging Face, S3 for file storage
- **Data**: Skills taxonomy, NER training data (1000+ resumes)
- **Prerequisite Tickets**: LTI-001 (Database)

**Definition of Done:**
- [ ] FastAPI service implemented
- [ ] PDF, DOC, DOCX parsing working
- [ ] NLP pipeline for entity extraction
- [ ] Education and work history parsing
- [ ] Skills extraction with taxonomy matching
- [ ] Confidence scoring implemented
- [ ] Unit tests >80% coverage
- [ ] Integration tests with sample resumes
- [ ] Performance tested (parse in <10s)
- [ ] Accuracy tested (>95% on test set)
- [ ] API documentation (OpenAPI spec)
- [ ] Error handling for corrupted files
- [ ] Deployed to staging

**Risks:**
- **Accuracy**: Non-standard resume formats may parse poorly - mitigation: continuous training data improvement
- **Performance**: Large PDFs may be slow - mitigation: async processing, batch API
- **Language Support**: Multi-language support is complex - mitigation: start with English, add languages incrementally

---

##### LTI-006: Build AI Matching Engine
**Type:** AI/ML | **Priority:** High | **Effort:** 13 pts | **Component:** Matching Engine

**Description:**

## Context
The Matching Engine calculates a 0-100 score indicating how well a candidate fits a job based on skills, experience, education, and historical hiring patterns. This is the core AI differentiator for LTI ATS.

## Objective
Implement a machine learning model that scores candidate-job fit with 85%+ accuracy, provides explainable results, and continuously learns from hiring outcomes.

**Technical Requirements:**

**API Endpoints:**
```python
POST /api/v1/matching/score
Request: {
  "candidate_id": "uuid",
  "job_id": "uuid"
}
Response: {
  "match_score": 87.5,
  "explanation": {
    "skills_match": 90,
    "experience_match": 85,
    "education_match": 88,
    "location_match": 100
  },
  "strengths": ["Strong Python skills", "Relevant experience in fintech"],
  "gaps": ["Missing AWS certification"],
  "confidence": 0.92
}

POST /api/v1/matching/batch
Request: {
  "job_id": "uuid",
  "candidate_ids": ["uuid1", "uuid2", ...]
}
Response: {
  "results": [
    { "candidate_id": "uuid1", "match_score": 87.5 },
    { "candidate_id": "uuid2", "match_score": 72.3 }
  ]
}

POST /api/v1/matching/train
Request: {
  "job_id": "uuid",
  "hired_candidate_id": "uuid",
  "outcome": "success"
}
Response: { "model_updated": true }
```

**Matching Algorithm:**
```python
def calculate_match_score(candidate: Candidate, job: Job) -> MatchResult:
    # 1. Skills matching (40% weight)
    skills_score = calculate_skills_match(
        candidate.skills,
        job.required_skills,
        job.preferred_skills
    )
    
    # 2. Experience matching (30% weight)
    experience_score = calculate_experience_match(
        candidate.years_of_experience,
        candidate.work_history,
        job.required_experience
    )
    
    # 3. Education matching (20% weight)
    education_score = calculate_education_match(
        candidate.education,
        job.required_education
    )
    
    # 4. Other factors (10% weight)
    other_score = calculate_other_factors(
        candidate.location,
        job.location,
        candidate.salary_expectations,
        job.salary_range
    )
    
    # Weighted average
    overall_score = (
        skills_score * 0.4 +
        experience_score * 0.3 +
        education_score * 0.2 +
        other_score * 0.1
    )
    
    # Apply ML model for fine-tuning
    ml_adjusted_score = ml_model.predict(
        candidate_features,
        job_features
    )
    
    return MatchResult(
        score=ml_adjusted_score,
        explanation={
            "skills": skills_score,
            "experience": experience_score,
            "education": education_score,
            "other": other_score
        }
    )
```

**ML Model:**
- **Algorithm**: Gradient Boosting (XGBoost) or Neural Network
- **Features**: Skills vector (TF-IDF), experience years, education level, location distance, salary alignment
- **Training Data**: Historical applications with hire/reject outcomes
- **Continuous Learning**: Retrain model weekly with new hiring outcomes

**Acceptance Criteria:**

**AC1: Calculate match score for candidate-job pair**
Given a candidate and job
When POST /api/v1/matching/score is called
Then a match score (0-100) is returned
And the score explanation shows contribution of each factor
And the response time is <200ms

**AC2: Skills matching with semantic similarity**
Given a job requires "React" and candidate has "React.js"
When skills matching is performed
Then the skills are recognized as equivalent
And the skills_match score is high (>90)

**AC3: Experience level matching**
Given a job requires 5+ years and candidate has 7 years
When experience matching is performed
Then the experience_match score is high (>85)
And over-qualified candidates are not penalized excessively

**AC4: Batch scoring for multiple candidates**
Given a job has 100 applicants
When POST /api/v1/matching/batch is called
Then all 100 candidates are scored
And results are returned in <5 seconds
And candidates are ranked by match_score

**AC5: Model learns from hiring outcomes**
Given a candidate was hired and performed well
When POST /api/v1/matching/train is called with outcome "success"
Then the model is updated to favor similar candidates
And future match scores for similar profiles increase

**Dependencies:**
- **Technical**: Python, scikit-learn/XGBoost, PostgreSQL
- **Data**: Historical hiring data (500+ applications), skills taxonomy
- **Prerequisite Tickets**: LTI-005 (CV Parser for candidate data)

**Definition of Done:**
- [ ] Matching algorithm implemented
- [ ] ML model trained on historical data
- [ ] API endpoints implemented
- [ ] Explainable AI (score breakdown)
- [ ] Batch scoring optimized
- [ ] Continuous learning pipeline
- [ ] Unit tests >80% coverage
- [ ] Model accuracy >85% on test set
- [ ] Performance tested (<200ms per score)
- [ ] API documentation
- [ ] Deployed to staging

---

### Epic 8: Integrations & Extensions

##### LTI-007: LinkedIn Recruiter API Integration
**Type:** Integration | **Priority:** High | **Effort:** 8 pts | **Component:** Integration Hub

**Description:**

## Context
LinkedIn is the primary sourcing platform for professional candidates. Integration with LinkedIn Recruiter API enables one-click profile import and expands candidate reach to 500M+ professionals.

## Objective
Implement OAuth 2.0 integration with LinkedIn Recruiter API for profile import, search, and data synchronization.

**Technical Requirements:**

**API Endpoints:**
```
POST /api/v1/integrations/linkedin/auth
Response: { "auth_url": "https://linkedin.com/oauth/authorize?..." }

POST /api/v1/integrations/linkedin/callback
Request: { "code": "auth_code" }
Response: { "access_token": "...", "expires_in": 3600 }

POST /api/v1/integrations/linkedin/import-profile
Request: { "linkedin_profile_url": "https://linkedin.com/in/johndoe" }
Response: { "candidate_id": "uuid", "imported_data": {...} }

GET /api/v1/integrations/linkedin/search
Query: ?keywords=software+engineer&location=San+Francisco
Response: { "profiles": [...], "total": 150 }
```

**OAuth 2.0 Flow:**
```typescript
// 1. Redirect user to LinkedIn authorization
const authUrl = `https://www.linkedin.com/oauth/v2/authorization?
  response_type=code&
  client_id=${CLIENT_ID}&
  redirect_uri=${REDIRECT_URI}&
  scope=r_liteprofile r_emailaddress w_member_social`;

// 2. Handle callback with authorization code
const tokenResponse = await axios.post('https://www.linkedin.com/oauth/v2/accessToken', {
  grant_type: 'authorization_code',
  code: authCode,
  redirect_uri: REDIRECT_URI,
  client_id: CLIENT_ID,
  client_secret: CLIENT_SECRET
});

// 3. Use access token for API calls
const profile = await axios.get('https://api.linkedin.com/v2/me', {
  headers: { Authorization: `Bearer ${accessToken}` }
});
```

**Profile Import:**
```typescript
async function importLinkedInProfile(profileUrl: string): Promise<Candidate> {
  // 1. Fetch profile data from LinkedIn API
  const profileData = await linkedInApi.getProfile(profileUrl);
  
  // 2. Map LinkedIn data to LTI ATS schema
  const candidateData = {
    first_name: profileData.firstName,
    last_name: profileData.lastName,
    email: profileData.emailAddress,
    linkedin_url: profileUrl,
    current_title: profileData.headline,
    location: profileData.location.name,
    work_history: profileData.positions.values.map(pos => ({
      title: pos.title,
      company: pos.company.name,
      start_date: `${pos.startDate.year}-${pos.startDate.month}`,
      end_date: pos.isCurrent ? null : `${pos.endDate.year}-${pos.endDate.month}`
    })),
    education: profileData.educations.values.map(edu => ({
      degree: edu.degree,
      field: edu.fieldOfStudy,
      institution: edu.schoolName,
      graduation_year: edu.endDate?.year
    })),
    skills: profileData.skills.values.map(s => s.name)
  };
  
  // 3. Check for duplicates
  const existing = await findCandidateByEmail(candidateData.email);
  if (existing) {
    return updateCandidate(existing.id, candidateData);
  }
  
  // 4. Create new candidate
  return createCandidate(candidateData);
}
```

**Rate Limiting:**
- LinkedIn API limits: 100 requests per day per user
- Implement request queue with exponential backoff
- Cache profile data in Redis (TTL: 24 hours)

**Acceptance Criteria:**

**AC1: OAuth authentication flow**
Given a user initiates LinkedIn connection
When they authorize the app
Then an access token is obtained and stored securely
And the token is refreshed before expiration

**AC2: Import LinkedIn profile**
Given a LinkedIn profile URL
When POST /api/v1/integrations/linkedin/import-profile is called
Then the profile data is fetched from LinkedIn
And a candidate record is created in LTI ATS
And duplicate detection prevents duplicate candidates

**AC3: Handle API rate limits**
Given the LinkedIn API rate limit is reached
When additional requests are made
Then requests are queued
And retried with exponential backoff
And users are notified of the delay

**AC4: Data mapping accuracy**
Given a LinkedIn profile with work history and education
When the profile is imported
Then all fields are correctly mapped to LTI ATS schema
And dates are normalized to ISO format
And skills are matched against taxonomy

**Dependencies:**
- **Technical**: LinkedIn Developer App credentials, OAuth 2.0 library
- **External**: LinkedIn Recruiter API access
- **Prerequisite Tickets**: LTI-001 (Database), LTI-002 (Auth)

**Definition of Done:**
- [ ] OAuth 2.0 flow implemented
- [ ] Profile import working
- [ ] Search integration working
- [ ] Rate limiting implemented
- [ ] Duplicate detection
- [ ] Error handling for API failures
- [ ] Unit tests >80% coverage
- [ ] Integration tests with LinkedIn sandbox
- [ ] API documentation
- [ ] Deployed to staging

---

## DevOps & Infrastructure Tickets

##### LTI-008: Setup Kubernetes Cluster (EKS/GKE)
**Type:** DevOps | **Priority:** High | **Effort:** 13 pts | **Component:** Infrastructure

**Description:**

## Context
LTI ATS uses a microservices architecture requiring container orchestration for deployment, scaling, and management. Kubernetes provides the foundation for production infrastructure.

## Objective
Set up a production-ready Kubernetes cluster on AWS EKS or GCP GKE with namespaces, RBAC, ingress, and monitoring.

**Technical Requirements:**

**Cluster Configuration:**
```yaml
# Terraform configuration for EKS
resource "aws_eks_cluster" "lti_ats" {
  name     = "lti-ats-production"
  role_arn = aws_iam_role.eks_cluster.arn
  version  = "1.28"

  vpc_config {
    subnet_ids = [
      aws_subnet.private_1.id,
      aws_subnet.private_2.id,
      aws_subnet.private_3.id
    ]
    endpoint_private_access = true
    endpoint_public_access  = true
  }
}

resource "aws_eks_node_group" "lti_ats" {
  cluster_name    = aws_eks_cluster.lti_ats.name
  node_group_name = "lti-ats-nodes"
  node_role_arn   = aws_iam_role.eks_nodes.arn
  subnet_ids      = aws_subnet.private[*].id

  scaling_config {
    desired_size = 3
    max_size     = 10
    min_size     = 2
  }

  instance_types = ["t3.large"]
}
```

**Namespaces:**
```yaml
# namespaces.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: lti-ats-production
---
apiVersion: v1
kind: Namespace
metadata:
  name: lti-ats-staging
---
apiVersion: v1
kind: Namespace
metadata:
  name: lti-ats-dev
```

**Ingress Controller:**
```yaml
# ingress.yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: lti-ats-ingress
  namespace: lti-ats-production
  annotations:
    kubernetes.io/ingress.class: nginx
    cert-manager.io/cluster-issuer: letsencrypt-prod
spec:
  tls:
  - hosts:
    - api.lti-ats.com
    secretName: lti-ats-tls
  rules:
  - host: api.lti-ats.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: api-gateway
            port:
              number: 80
```

**Acceptance Criteria:**

**AC1: Cluster created successfully**
Given Terraform configuration is applied
When the cluster is provisioned
Then the EKS/GKE cluster is running
And kubectl can connect to the cluster
And nodes are in Ready state

**AC2: Namespaces configured**
Given namespaces are created
When kubectl get namespaces is run
Then production, staging, and dev namespaces exist
And RBAC policies isolate namespaces

**AC3: Ingress controller working**
Given the ingress controller is deployed
When a service is exposed via ingress
Then external traffic reaches the service
And TLS certificates are automatically provisioned

**AC4: Auto-scaling configured**
Given the cluster has auto-scaling enabled
When CPU usage exceeds 70%
Then new nodes are automatically added
And pods are scheduled on new nodes

**Dependencies:**
- **Technical**: AWS/GCP account, Terraform, kubectl, helm
- **Prerequisite Tickets**: None (foundational)

**Definition of Done:**
- [ ] Kubernetes cluster provisioned
- [ ] Namespaces created
- [ ] Ingress controller deployed
- [ ] Auto-scaling configured
- [ ] RBAC policies configured
- [ ] Monitoring agents installed
- [ ] Documentation created
- [ ] Terraform code reviewed
- [ ] Cluster tested with sample deployment

---

##### LTI-009: Setup CI/CD Pipeline (GitHub Actions)
**Type:** DevOps | **Priority:** High | **Effort:** 8 pts | **Component:** CI/CD

**Description:**

## Context
Automated CI/CD pipelines ensure code quality, run tests, build Docker images, and deploy to Kubernetes clusters safely and efficiently.

## Objective
Implement GitHub Actions workflows for automated testing, building, and deployment to staging and production environments.

**Technical Requirements:**

**GitHub Actions Workflow:**
```yaml
# .github/workflows/backend-ci-cd.yml
name: Backend CI/CD

on:
  push:
    branches: [main, develop]
    paths:
      - 'backend/**'
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Install dependencies
        run: npm ci
        working-directory: ./backend
      
      - name: Run linter
        run: npm run lint
        working-directory: ./backend
      
      - name: Run unit tests
        run: npm test -- --coverage
        working-directory: ./backend
      
      - name: Upload coverage
        uses: codecov/codecov-action@v3

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Build Docker image
        run: docker build -t lti-ats/backend:${{ github.sha }} ./backend
      
      - name: Push to ECR
        run: |
          aws ecr get-login-password | docker login --username AWS --password-stdin $ECR_REGISTRY
          docker tag lti-ats/backend:${{ github.sha }} $ECR_REGISTRY/lti-ats/backend:${{ github.sha }}
          docker push $ECR_REGISTRY/lti-ats/backend:${{ github.sha }}

  deploy-staging:
    needs: build
    if: github.ref == 'refs/heads/develop'
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to staging
        run: |
          kubectl set image deployment/backend backend=$ECR_REGISTRY/lti-ats/backend:${{ github.sha }} -n lti-ats-staging
          kubectl rollout status deployment/backend -n lti-ats-staging

  deploy-production:
    needs: build
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    environment: production
    steps:
      - name: Deploy to production
        run: |
          kubectl set image deployment/backend backend=$ECR_REGISTRY/lti-ats/backend:${{ github.sha }} -n lti-ats-production
          kubectl rollout status deployment/backend -n lti-ats-production
```

**Acceptance Criteria:**

**AC1: Tests run on every PR**
Given a pull request is created
When the CI pipeline runs
Then linter, unit tests, and integration tests execute
And the PR cannot be merged if tests fail

**AC2: Docker images built and pushed**
Given tests pass
When the build job runs
Then a Docker image is built
And the image is tagged with commit SHA
And the image is pushed to container registry

**AC3: Auto-deploy to staging**
Given code is merged to develop branch
When the deploy-staging job runs
Then the new image is deployed to staging namespace
And the deployment succeeds without downtime

**AC4: Manual approval for production**
Given code is merged to main branch
When the deploy-production job is triggered
Then manual approval is required
And deployment proceeds only after approval

**Dependencies:**
- **Technical**: GitHub Actions, Docker, kubectl, AWS ECR
- **Prerequisite Tickets**: LTI-008 (Kubernetes cluster)

**Definition of Done:**
- [ ] CI/CD workflows created
- [ ] Test automation working
- [ ] Docker build and push working
- [ ] Staging auto-deployment working
- [ ] Production deployment with approval
- [ ] Rollback mechanism tested
- [ ] Documentation created
- [ ] Workflows tested end-to-end

---

## Sprint Planning Suggestions

### Sprint 1: Foundation (MVP Core)
**Focus:** Database, Auth, Infrastructure  
**Tickets:** LTI-001, LTI-002, LTI-008, LTI-009  
**Effort:** 47 points  
**Goal:** Establish foundational infrastructure and security

### Sprint 2: Core Backend Services
**Focus:** Job Management, Candidate Service  
**Tickets:** LTI-003, Candidate Service API, Application Service API  
**Effort:** 39 points  
**Goal:** Build core business logic services

### Sprint 3: Frontend Foundation
**Focus:** React architecture, UI components  
**Tickets:** LTI-004, Login Page, Jobs List Page  
**Effort:** 34 points  
**Goal:** Establish frontend architecture and first user flows

### Sprint 4: AI/ML Core
**Focus:** CV Parser, Matching Engine  
**Tickets:** LTI-005, LTI-006  
**Effort:** 26 points  
**Goal:** Implement core AI differentiation features

### Sprint 5: Integrations
**Focus:** LinkedIn, HRIS, Calendar  
**Tickets:** LTI-007, HRIS Integration, Calendar Integration  
**Effort:** 24 points  
**Goal:** Connect to external systems

---

## Tickets by Type

### Backend Tickets (18 total)
- LTI-002: Auth Service (13 pts)
- LTI-003: Job Management API (13 pts)
- Candidate Service API (13 pts)
- Application Service API (13 pts)
- Evaluation Service API (8 pts)
- Communication Service API (8 pts)
- Interview Service API (8 pts)
- Analytics Service API (8 pts)
- Workflow Engine (13 pts)
- Scheduler Service (8 pts)
- [Additional backend tickets...]

### Frontend Tickets (15 total)
- LTI-004: React Architecture (13 pts)
- Login Page (5 pts)
- Jobs List Page (8 pts)
- Job Detail Page (8 pts)
- Candidate List Page (8 pts)
- Pipeline Kanban Board (13 pts)
- Dashboard (8 pts)
- [Additional frontend tickets...]

### Database Tickets (8 total)
- LTI-001: PostgreSQL Schema (13 pts)
- Migration Scripts (5 pts)
- Indexes Optimization (5 pts)
- [Additional database tickets...]

### AI/ML Tickets (10 total)
- LTI-005: CV Parser (13 pts)
- LTI-006: Matching Engine (13 pts)
- NLP Service (8 pts)
- Insights Generator (8 pts)
- [Additional AI/ML tickets...]

### DevOps Tickets (8 total)
- LTI-008: Kubernetes Setup (13 pts)
- LTI-009: CI/CD Pipeline (8 pts)
- Monitoring Setup (8 pts)
- Logging Setup (5 pts)
- [Additional DevOps tickets...]

### Integration Tickets (8 total)
- LTI-007: LinkedIn Integration (8 pts)
- HRIS Integration (8 pts)
- Calendar Integration (8 pts)
- Job Boards Integration (8 pts)
- [Additional integration tickets...]

### QA Tickets (6 total)
- E2E Test Suite (13 pts)
- Performance Testing (8 pts)
- Security Testing (8 pts)
- [Additional QA tickets...]

---

## Flat Table of All Tickets (Import-Ready)

| ID | Title | Type | Priority | Effort | Epic | Feature | Component | Dependencies |
|----|-------|------|----------|--------|------|---------|-----------|--------------|
| LTI-001 | Setup PostgreSQL Database Schema | Database | High | 13 | E-001 | Infrastructure | PostgreSQL | None |
| LTI-002 | Implement Auth Service (JWT, RBAC, MFA) | Backend | High | 13 | E-001 | Auth | Auth Service | LTI-001 |
| LTI-003 | Build Job Management Service API | Backend | High | 13 | E-001 | F-001 | Job Service | LTI-001, LTI-002 |
| LTI-004 | Build React Frontend Architecture | Frontend | High | 13 | Platform | UI | React App | LTI-002 |
| LTI-005 | Implement CV Parser (NLP Service) | AI/ML | High | 13 | E-003 | F-009 | CV Parser | LTI-001 |
| LTI-006 | Build AI Matching Engine | AI/ML | High | 13 | E-003 | F-010 | Matching Engine | LTI-005 |
| LTI-007 | LinkedIn Recruiter API Integration | Integration | High | 8 | E-002 | F-006 | Integration Hub | LTI-001, LTI-002 |
| LTI-008 | Setup Kubernetes Cluster (EKS/GKE) | DevOps | High | 13 | Platform | Infrastructure | Kubernetes | None |
| LTI-009 | Setup CI/CD Pipeline (GitHub Actions) | DevOps | High | 8 | Platform | CI/CD | GitHub Actions | LTI-008 |

---

## Appendix: Ticket Template

Use this template for creating additional tickets:

```markdown
##### LTI-XXX: [Ticket Title]
**Type:** [Backend/Frontend/Database/DevOps/AI-ML/Integration/QA/Spike] | **Priority:** [High/Medium/Low] | **Effort:** [Story Points] | **Component:** [Service/Component Name]

**Description:**

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
- [Constraint 1]
- [Constraint 2]

**Technical Requirements:**

[Detailed technical specs - API endpoints, schemas, algorithms, etc.]

**Acceptance Criteria:**

**AC1: [Scenario name]**
Given [initial state]
When [action]
Then [expected outcome]

**AC2: [Error scenario]**
Given [invalid state]
When [action]
Then [error handling]

[Minimum 3-5 acceptance criteria]

**Dependencies:**
- **Technical**: [Services, libraries, infrastructure]
- **Data**: [Required data, schemas]
- **Prerequisite Tickets**: [LTI-XXX, LTI-YYY]

**Definition of Done:**
- [ ] Code complete
- [ ] Tests written (>80% coverage)
- [ ] API documentation updated
- [ ] Code review approved
- [ ] Deployed to staging
- [ ] QA validated

**Risks:**
[Technical/business risks and mitigation]

**Notes for Engineering:**
[Implementation hints, gotchas, references]
```

---

**Document Status:** ✅ **Ready for Sprint Planning**

**Next Steps:**
1. Engineering team to review and validate effort estimates
2. Product Manager to prioritize tickets for Sprint 1
3. Begin sprint planning with LTI-001 through LTI-009
4. Set up project tracking in Jira/Linear/GitHub Projects

---

**Change Log:**

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-11-25 | Engineering Team | Initial engineering work tickets based on Product Backlog and PRD |

