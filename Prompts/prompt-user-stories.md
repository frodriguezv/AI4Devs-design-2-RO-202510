# Claude Sonnet 4.5 Prompt — LTI ATS User Stories

## Persona
You are an expert **Product Requirements Analyst + Agile Product Manager**, specializing in writing high-quality, INVEST-compliant user stories with detailed Gherkin acceptance criteria for AI-powered SaaS applications.

## Context
You are given the Product Requirements Document for **LTI ATS** - an intelligent Applicant Tracking System that reduces time-to-hire by 40% through AI automation and real-time collaboration.

**Product Vision:**
LTI ATS transforms recruitment from a manual, reactive process into an intelligent, data-driven operation. The platform serves HR teams in mid-market companies (200-2,000 employees) and progressive tech startups (50-200 employees).

**Primary User Segments & Personas:**

1. **Recruiters**
   - Manage job requisitions from creation to offer
   - Source and screen candidates using AI-powered tools
   - Coordinate interview schedules and communication
   - Track pipeline metrics and optimize sourcing channels
   - *Goal: Reduce administrative burden by 60%, focus on high-value candidate engagement*

2. **Hiring Managers**
   - Approve job requisitions and define requirements
   - Review shortlisted candidates with AI recommendations
   - Participate in collaborative evaluation and decision-making
   - Make final hiring decisions based on data-driven insights
   - *Goal: Make faster, more accurate hiring decisions with structured feedback*

3. **Interviewers**
   - Conduct structured interviews using customizable scorecards
   - Provide real-time feedback and ratings
   - Collaborate with team members through comments and discussions
   - Access consolidated candidate information and interview history
   - *Goal: Deliver consistent, high-quality evaluations that reduce bias*

4. **Candidates**
   - Apply to jobs through a modern, mobile-optimized interface
   - Track application status in real-time via candidate portal
   - Communicate directly with recruiters
   - Schedule interviews with smart calendar integration
   - *Goal: Experience transparent, respectful recruitment process*

**Key Workflows (from PRD Use Cases):**
1. **Job Posting & Automated Sourcing**: Requisition creation → AI-powered job description → approval → multi-channel publishing → proactive candidate matching
2. **Collaborative Candidate Evaluation**: Interview completion → scorecard filling → AI sentiment analysis → team discussion → consolidated recommendation → hiring decision
3. **Automated Communication & Pipeline**: Application → CV parsing → AI screening → auto-assignment → stage transitions → automated emails → interview scheduling → feedback collection

**Core Value Proposition:**
- **40% reduction in time-to-hire** through intelligent automation
- **60% reduction in administrative tasks** for recruiters
- **Data-driven hiring decisions** with AI-powered insights
- **Premium candidate experience** with real-time transparency

The PRD includes detailed feature requirements (8 categories), complete data model, technical architecture, and success metrics.

## Task
Using the LTI ATS PRD (`lti_ats_prd.md`), generate a **comprehensive set of INVEST-compliant User Stories** ready for engineering implementation.

## Requirements

### 1. User Story Count
- Generate **as many user stories as needed** to cover the system comprehensively
- Minimum: **20 user stories** (covering all major workflows and personas)
- Ensure balanced coverage across:
  - All 4 user personas (Recruiter, Hiring Manager, Interviewer, Candidate)
  - All 8 feature domains (Job Management, Sourcing, Screening, Evaluation, Pipeline, Communication, Analytics, Integrations)
  - P0 (must have), P1 (should have), and P2 (nice to have) requirements

### 2. User Story Template (mandatory)
Use this EXACT structure for every story:

---

### **User Story**
**ID:** `US-XXX`  
**Epic:** `<Epic Name from prompt-epics output>`  
**Feature:** `<Feature Name>`  
**Priority:** P0 / P1 / P2  
**Persona:** Recruiter / Hiring Manager / Interviewer / Candidate

**As a** [persona],  
**I want to** [capability],  
**So that** [business value / user benefit]

### **Description**
[2-3 sentences explaining the user need, context, and expected behavior]

### **Acceptance Criteria (Gherkin)**

**Scenario 1:** [Scenario name]
- **Given** [initial context and preconditions]
- **When** [user action or system event]
- **Then** [expected outcome and system behavior]

**Scenario 2:** [Scenario name]
- **Given** [...]
- **When** [...]
- **Then** [...]

**Scenario 3:** [Scenario name - edge case or alternative flow]
- **Given** [...]
- **When** [...]
- **Then** [...]

**Include minimum 3-5 acceptance criteria per story.**

### **Dependencies**
- **Technical:** [e.g., Authentication service, PostgreSQL database, AI matching engine]
- **Data:** [e.g., Job requisitions, Candidate profiles, Historical hiring data]
- **Integration:** [e.g., LinkedIn API, Calendar integration, Email service]
- **Prerequisite Stories:** [e.g., US-001, US-015]

### **Notes**
- **Assumptions:** [Any assumptions made]
- **Open Questions:** [Unresolved items needing stakeholder input]
- **Technical Considerations:** [API endpoints, data model changes, performance needs]

---

### 3. Use INVEST Best Practices
Ensure every user story follows the **INVEST** framework:
- **Independent**: Can be developed independently of other stories (note dependencies if not fully independent)
- **Negotiable**: Details can be discussed and refined with stakeholders
- **Valuable**: Delivers clear value to users or business
- **Estimable**: Developers can estimate effort (story points)
- **Small**: Can be completed within a single sprint (1-2 weeks)
- **Testable**: Clear acceptance criteria enable verification

Focus on:
- **Clarity**: Unambiguous language, specific actions, measurable outcomes
- **User-Centric**: Written from user perspective, not technical implementation
- **Completeness**: All information needed for development and testing
- **Traceability**: Clear mapping to PRD requirements

### 4. Coverage Requirements
Ensure comprehensive coverage of:

**Job Management Domain:**
- Job requisition creation with AI assistance
- Approval workflows
- Multi-channel publishing
- Job editing and closure

**Sourcing & Screening:**
- Candidate search and filtering
- AI-powered matching and ranking
- CV parsing and profile creation
- Talent pool management

**Evaluation & Collaboration:**
- Scorecard creation and completion
- Real-time commenting and discussion
- Video interview management
- Consolidated decision views

**Pipeline & Workflow:**
- Kanban board interaction
- Stage transitions and automation
- Candidate assignment
- Bulk operations

**Communication:**
- Email template management
- Automated email triggers
- Interview scheduling
- Candidate portal updates

**Analytics:**
- Dashboard viewing
- Report generation
- Metrics tracking
- Export functionality

**Integrations:**
- HRIS data sync
- Calendar integration
- Third-party assessment tools
- API access

## Output Format
Return the user stories in **clean, well-organized Markdown**:

1. **Summary Section**: Overview of story count by persona and feature domain
2. **Prioritized Backlog**: Stories grouped by priority (P0, P1, P2)
3. **Persona View**: Stories grouped by persona
4. **Epic/Feature View**: Stories grouped by epic and feature
5. **Complete Story Details**: Full details for all stories

## Final Instruction
Begin by:
1. Reading the LTI ATS PRD (`lti_ats_prd.md`) thoroughly
2. Summarizing the product vision, key user personas, and primary workflows in 3–5 sentences to confirm understanding
3. Generating the complete set of user stories following the structure above, ensuring full coverage of the system and balanced representation of all personas and feature domains
