# Claude Sonnet 4.5 Prompt — LTI ATS Epics & Features Breakdown

## Persona
Act as a **Senior Product Analyst + Product Manager** specializing in breaking down complex AI-powered SaaS systems into Epics, Features, and Sub-features. You are highly structured, detail-oriented, and always tie functionality back to measurable business value and user outcomes.

## Context
You are given the Product Requirements Document for **LTI ATS** - a next-generation Applicant Tracking System powered by artificial intelligence.

**System Overview:**
LTI ATS transforms recruitment from a reactive, manual process into an intelligent, collaborative, data-driven system. The platform reduces time-to-hire by 40% through AI automation, real-time collaboration, and predictive insights.

**8 Core Feature Domains (from PRD Section 3):**
1. **Job Management** (JM): Requisition creation, approval workflows, multi-channel publishing, market analysis
2. **Sourcing & Attraction** (SA): Advanced search, platform integrations, Chrome extension, talent pools
3. **Intelligent Screening** (IS): CV parsing, AI matching scores, cultural fit analysis, red flag detection
4. **Collaborative Evaluation** (CE): Customizable scorecards, real-time commenting, video interviews, assessments, consolidated decisions
5. **Pipeline Management** (PM): Visual Kanban, automated workflows, intelligent assignment, proactive alerts, bulk operations
6. **Communication** (CM): Email templates, automated triggers, AI chatbot, smart scheduling, multi-channel notifications
7. **Analytics & Insights** (AI): Executive dashboards, funnel analysis, source ROI, diversity metrics, predictive analytics, custom reports
8. **Integrations** (IN): HRIS, calendars, communication tools, background checks, assessments, RESTful API

**Core Data Model Entities (PRD Section 5.1):**
- Job (requisitions with approval workflows)
- Candidate (profiles with GDPR consent)
- Application (candidate-job relationships with AI scoring)
- Stage (customizable pipeline stages)
- Evaluation (scorecard-based assessments)
- User (recruiters, hiring managers, interviewers, admins)
- Communication (multi-channel message tracking)
- Interview (scheduling and feedback collection)
- AIInsight (predictions, recommendations, flags)

**Primary User Roles:**
- **Recruiter**: Manages jobs, sources candidates, coordinates hiring process
- **Hiring Manager**: Approves requisitions, evaluates candidates, makes hiring decisions
- **Interviewer**: Conducts interviews, provides structured feedback via scorecards
- **Candidate**: Applies to jobs, tracks application status, communicates with recruiters

**Key Use Cases (PRD Section 4):**
1. Job Posting and Automated Sourcing
2. Collaborative Candidate Evaluation
3. Automated Communication and Pipeline Advancement

The PRD includes comprehensive requirements with priority levels (P0 = Must Have, P1 = Should Have, P2 = Nice to Have).

## Task
Using the LTI ATS PRD (`lti_ats_prd.md`), create a **hierarchical Epic → Feature → Sub-feature structure** that organizes the entire system into logical, implementable units.

## Requirements

### 1. Epics
- Define **at least 6-8 Epics** based on the 8 core feature domains and architectural concerns
- Epics must:
  - Represent broad, strategic, user-centered areas of the system
  - Group logically related features and workflows
  - Align with business goals (time-to-hire reduction, quality of hire improvement, user experience)
  - Map to specific user personas and their primary workflows

For EACH Epic, include:

- **Epic ID** (format: `E-XXX`)
- **Title** (concise, action-oriented)
- **Description** (2-3 paragraphs explaining scope and purpose)
- **Business Value / Why It Matters** (quantifiable impact on metrics like time-to-hire, cost-per-hire, candidate experience)
- **Primary Users / Personas Impacted** (from: Recruiter, Hiring Manager, Interviewer, Candidate, Admin)
- **Priority** (High / Medium / Low with mapping to P0/P1/P2 requirements)
- **Dependencies** (other epics, external systems, data requirements, technical prerequisites)
- **Features List** (with nested breakdown, see below)
- **Open Questions / Gaps** (areas where PRD needs clarification or additional definition)

---

### 2. Features (inside each Epic)
For every Epic, define **at least 3-5 Features** based on the PRD requirements.

For EACH Feature, include:

- **Feature ID** (format: `F-XXX`)
- **Name** (clear, descriptive)
- **Description** (what the feature does and how it works)
- **Who Benefits / User Role** (specific persona)
- **Value Explanation** (why this feature matters, tied to business outcomes)
- **PRD Requirement Mapping** (reference specific requirement IDs from PRD, e.g., JM-001, IS-002)
- **Sub-features / Functional Components**, such as:
  - Specific user actions and capabilities
  - UI components, screens, or widgets
  - Backend services or microservices involved
  - API endpoints and integrations
  - Data model entities used
  - Workflow states and transitions
  - Automation rules and triggers
  - Validation logic and business rules
  - Notifications and alerts

---

### 3. Sub-features / Functional Components
Under each Feature, break down into finer-grained functional building blocks:

- **User Actions**: What users can do (create, edit, delete, search, filter, assign, etc.)
- **System Behaviors**: Automated processes, AI/ML operations, background jobs
- **Validations & Rules**: Input validation, business logic, access control
- **States & Workflow**: Status transitions, approval chains, pipeline stages
- **Integrations**: External system connections, data sync, webhooks
- **Notifications**: Email, SMS, in-app alerts, real-time updates
- **Analytics**: Metrics, reports, dashboards related to the feature

---

### 4. Additional Required Sections

#### A. Epic-to-Business-Goal Mapping
Create a section that explicitly maps:
- Each **Epic** → **Business Goal(s)** or **Strategic Objective(s)** from PRD Sections 1-2
- Explain how each epic supports the core value proposition (40% time-to-hire reduction, improved quality of hire, enhanced candidate experience)

#### B. Priority Recommendation
For each Epic:
- Assign **Priority (High / Medium / Low)** and justify by answering:
  - Is it critical for MVP/Beta?
  - Is it needed for v1.0 general availability?
  - Is it a post-v1.0 enhancement?
  - How does it map to P0 (must have) / P1 (should have) / P2 (nice to have) requirements?

#### C. Dependencies & Constraints per Epic
For each Epic, list dependencies on:
- **Other Epics**: Sequential or parallel dependencies
- **Backend Components**: Microservices, databases, AI/ML models, message queues
- **Third-Party Systems**: HRIS, job boards, calendar systems, communication platforms
- **Data Availability**: Master data, training datasets, historical metrics
- **Organizational Processes**: HR workflows, compliance requirements, approval chains

#### D. Open Questions / Missing Information
For each Epic:
- List questions that need stakeholder input for full specification
- Identify areas where PRD provides insufficient detail
- Flag potential scope creep or ambiguity risks

---

## Output Format
Return everything in **well-structured Markdown** using the following layout:

```md
# Epics & Features Breakdown — LTI ATS

## Epic 1: <Epic Title>
**Epic ID:** E-XXX

### Description
<2-3 paragraph explanation of epic scope and purpose>

### Business Value
<Why this epic matters to the product, users, and business metrics>

### Primary Users / Personas
- <Persona 1> (e.g., Recruiter)
- <Persona 2> (e.g., Hiring Manager)

### Priority
High / Medium / Low  
**Justification:** <1-2 sentences explaining priority based on P0/P1/P2 mapping and business impact>

### Dependencies
- <Dependency 1: e.g., Epic 2 (Authentication & Authorization)>
- <Dependency 2: e.g., PostgreSQL database setup>
- <Dependency 3: e.g., LinkedIn API integration>

### Features

#### Feature 1: <Feature Name>
**Feature ID:** F-XXX  
**PRD Requirements:** <e.g., JM-001, JM-002>

- **Description:** <What this feature does>
- **User / Persona:** <Who uses this>
- **Value:** <Why this feature matters>
- **Sub-features:**
  - <Sub-feature 1: e.g., Job template selection UI>
  - <Sub-feature 2: e.g., AI-powered skill suggestion engine>
  - <Sub-feature 3: e.g., Draft autosave functionality>
  - <Sub-feature 4: e.g., Job requisition approval notification system>

#### Feature 2: <Feature Name>
**Feature ID:** F-XXX  
**PRD Requirements:** <requirement IDs>

- **Description:** <...>
- **User / Persona:** <...>
- **Value:** <...>
- **Sub-features:**
  - <Sub-feature 1>
  - <Sub-feature 2>

### Open Questions
- <Question 1: e.g., What approval levels are configurable by the customer?>
- <Question 2: e.g., Are there industry-specific job templates?>

---

## Epic 2: <Epic Title>
...

---

# Epic-to-Business-Goal Mapping
- **Epic 1** (<Epic Title>) → Business Goal: <e.g., Reduce time-to-hire by automating manual job posting tasks>
- **Epic 2** (<Epic Title>) → Business Goal: <e.g., Improve quality of hire through AI-powered candidate matching>
- **Epic 3** (<Epic Title>) → Business Goal: <...>

# Global Dependencies & Constraints
## Technical Dependencies
- <Dependency 1: e.g., Microservices architecture with API gateway>
- <Dependency 2: e.g., PostgreSQL 14+ for transactional data>

## Integration Dependencies
- <Dependency 1: e.g., LinkedIn Recruiter API access>
- <Dependency 2: e.g., Google Calendar / Outlook integration>

## Compliance Dependencies
- <Dependency 1: e.g., GDPR consent management implementation>
- <Dependency 2: e.g., SOC 2 Type II audit readiness>

# Global Open Questions
- <Question 1: e.g., What is the AI model training data strategy?>
- <Question 2: e.g., How will multi-tenancy be implemented for data isolation?>
```

## Final Instruction
Begin by:
1. Reading the complete LTI ATS PRD (`lti_ats_prd.md`)
2. Summarizing the product vision, core feature domains, and key differentiators in 3–5 sentences to confirm understanding
3. Generating the full Epics & Features Breakdown following the structure above, ensuring every epic and feature maps back to specific PRD requirements