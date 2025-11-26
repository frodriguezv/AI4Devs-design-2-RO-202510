# User Stories — LTI ATS

**Version:** 1.0  
**Date:** November 25, 2025  
**Owner:** Product Team

---

## Executive Summary

This document contains **28 INVEST-compliant user stories** for the LTI ATS system, covering all 8 feature domains and 4 primary user personas. Each story includes detailed Gherkin acceptance criteria, dependencies, and traceability to PRD requirements and epics/features.

### Story Distribution

**By Priority:**
- P0 (Must Have): 16 stories
- P1 (Should Have): 10 stories
- P2 (Nice to Have): 2 stories

**By Persona:**
- Recruiter: 14 stories
- Hiring Manager: 6 stories
- Interviewer: 4 stories
- Candidate: 4 stories

**By Epic:**
- E-001 (Job Lifecycle Management): 3 stories
- E-002 (Intelligent Candidate Sourcing): 3 stories
- E-003 (AI-Powered Screening & Matching): 4 stories
- E-004 (Collaborative Evaluation): 5 stories
- E-005 (Pipeline & Workflow Automation): 4 stories
- E-006 (Multi-Channel Communication): 4 stories
- E-007 (Analytics & Predictive Insights): 3 stories
- E-008 (Integrations & Extensions): 2 stories

---

## Summary Tables

### Stories by Priority

| Priority | Story ID | Title | Persona | Epic |
|----------|----------|-------|---------|------|
| P0 | US-001 | Create Job Requisition with AI Assistance | Recruiter | E-001 |
| P0 | US-002 | Approve Job Requisition | Hiring Manager | E-001 |
| P0 | US-003 | Publish Job to Multiple Channels | Recruiter | E-001 |
| P0 | US-004 | Search Internal Candidate Database | Recruiter | E-002 |
| P0 | US-005 | Import Candidate from LinkedIn | Recruiter | E-002 |
| P0 | US-006 | Parse Resume Automatically | Recruiter | E-003 |
| P0 | US-007 | View AI Matching Score | Recruiter | E-003 |
| P0 | US-008 | Complete Interview Scorecard | Interviewer | E-004 |
| P0 | US-009 | Comment on Candidate Profile | Interviewer | E-004 |
| P0 | US-010 | View Consolidated Evaluation | Hiring Manager | E-004 |
| P0 | US-011 | Manage Pipeline with Kanban Board | Recruiter | E-005 |
| P0 | US-012 | Configure Automated Workflows | Recruiter | E-005 |
| P0 | US-013 | Send Email from Template | Recruiter | E-006 |
| P0 | US-014 | Receive Automated Email Updates | Candidate | E-006 |
| P0 | US-015 | View Executive Dashboard | Hiring Manager | E-007 |
| P0 | US-016 | Sync with HRIS System | Recruiter | E-008 |
| P1 | US-017 | View Market Salary Benchmarks | Hiring Manager | E-001 |
| P1 | US-018 | Manage Talent Pools | Recruiter | E-002 |
| P1 | US-019 | Review AI Red Flags | Recruiter | E-003 |
| P1 | US-020 | Assess Cultural Fit | Hiring Manager | E-003 |
| P1 | US-021 | Conduct Video Interview | Interviewer | E-004 |
| P1 | US-022 | Receive Proactive Alerts | Recruiter | E-005 |
| P1 | US-023 | Perform Bulk Operations | Recruiter | E-005 |
| P1 | US-024 | Schedule Interview with Smart Calendar | Recruiter | E-006 |
| P1 | US-025 | Analyze Funnel Metrics | Hiring Manager | E-007 |
| P1 | US-026 | Track Source ROI | Recruiter | E-007 |
| P2 | US-027 | Use AI Chatbot for Questions | Candidate | E-006 |
| P2 | US-028 | View Predictive Analytics | Hiring Manager | E-007 |

### Stories by Persona

| Persona | Story Count | Story IDs |
|---------|-------------|-----------|
| Recruiter | 14 | US-001, US-003, US-004, US-005, US-006, US-007, US-011, US-012, US-013, US-016, US-018, US-019, US-022, US-023, US-024, US-026 |
| Hiring Manager | 6 | US-002, US-010, US-015, US-017, US-020, US-025, US-028 |
| Interviewer | 4 | US-008, US-009, US-021 |
| Candidate | 4 | US-014, US-027 |

### Stories by Epic

| Epic | Story Count | Story IDs |
|------|-------------|-----------|
| E-001 (Job Lifecycle Management) | 3 | US-001, US-002, US-003, US-017 |
| E-002 (Intelligent Candidate Sourcing) | 3 | US-004, US-005, US-018 |
| E-003 (AI-Powered Screening & Matching) | 4 | US-006, US-007, US-019, US-020 |
| E-004 (Collaborative Evaluation) | 5 | US-008, US-009, US-010, US-021 |
| E-005 (Pipeline & Workflow Automation) | 4 | US-011, US-012, US-022, US-023 |
| E-006 (Multi-Channel Communication) | 4 | US-013, US-014, US-024, US-027 |
| E-007 (Analytics & Predictive Insights) | 3 | US-015, US-025, US-026, US-028 |
| E-008 (Integrations & Extensions) | 2 | US-016 |

---

## Complete User Stories


### **User Story US-001**
**ID:** `US-001`  
**Epic:** E-001 (Job Lifecycle Management)  
**Feature:** F-001 (Intelligent Job Requisition Creation)  
**Priority:** P0  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** create job requisitions using AI-powered templates that suggest required skills and generate optimized descriptions,  
**So that** I can reduce job creation time from 2 hours to 20 minutes while ensuring quality and consistency.

### **Description**
Recruiters need an efficient way to create comprehensive job requisitions without starting from scratch. The system should provide intelligent templates based on role type, suggest relevant skills from similar positions, and generate SEO-optimized job descriptions that attract qualified candidates.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Create job requisition from template**
- **Given** I am a recruiter logged into the LTI ATS
- **When** I select "Create New Job" and choose the "Software Engineer" template
- **Then** the system pre-fills common fields (required skills, responsibilities, qualifications)
- **And** displays AI-suggested skills based on similar roles in my organization
- **And** allows me to customize all fields before saving

**Scenario 2: AI generates job description**
- **Given** I have entered basic job information (title, department, level)
- **When** I click "Generate Description" using AI
- **Then** the system creates an SEO-optimized job description within 10 seconds
- **And** includes relevant keywords for search visibility
- **And** maintains my company's tone and branding
- **And** allows me to edit the generated content

**Scenario 3: Save draft and version history**
- **Given** I am creating a job requisition
- **When** I make changes to any field
- **Then** the system auto-saves my draft every 30 seconds
- **And** maintains version history of all changes
- **And** allows me to restore previous versions if needed

**Scenario 4: Preview candidate-facing view**
- **Given** I have completed the job requisition
- **When** I click "Preview"
- **Then** the system displays how candidates will see the job posting
- **And** shows the description formatted for mobile and desktop
- **And** highlights any missing required fields

**Scenario 5: Duplicate detection**
- **Given** I am creating a new job requisition
- **When** the system detects a similar active job (same title, department, location)
- **Then** it alerts me about the potential duplicate
- **And** shows the existing job details for comparison
- **And** allows me to proceed if intentional

### **Dependencies**
- **Technical:** PostgreSQL database, AI content generation service (GPT-based), job template library
- **Data:** Job templates by role/department, skills taxonomy, historical job postings
- **Integration:** None for MVP
- **Prerequisite Stories:** None (foundational story)

### **Notes**
- **Assumptions:** AI service has access to company's historical job postings for context
- **Open Questions:** Should AI suggestions learn from user edits over time? What's the fallback if AI service is unavailable?
- **Technical Considerations:** API endpoint: POST /api/jobs, GET /api/jobs/templates, POST /api/jobs/generate-description

---

### **User Story US-002**
**ID:** `US-002`  
**Epic:** E-001 (Job Lifecycle Management)  
**Feature:** F-002 (Configurable Approval Workflows)  
**Priority:** P0  
**Persona:** Hiring Manager

**As a** Hiring Manager,  
**I want to** review and approve job requisitions with clear visibility into requirements and budget impact,  
**So that** I can ensure proper authorization and alignment with hiring plans before jobs are published.

### **Description**
Hiring managers need a streamlined approval process that provides all necessary context for decision-making, including job details, budget implications, and organizational alignment. The system should enable quick approvals while maintaining audit trails and supporting rejection with feedback.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Receive approval notification**
- **Given** a recruiter has submitted a job requisition for my approval
- **When** the requisition enters my approval queue
- **Then** I receive an email notification with a direct link to review
- **And** I receive an in-app notification in my dashboard
- **And** the notification includes key details (job title, department, salary range)

**Scenario 2: Review job requisition details**
- **Given** I have opened a pending approval request
- **When** I view the requisition
- **Then** I see all job details (description, requirements, salary, headcount)
- **And** I see budget impact and remaining headcount allocation
- **And** I see the recruiter's justification for the role
- **And** I can view the complete approval chain and who else needs to approve

**Scenario 3: Approve requisition**
- **Given** I have reviewed a job requisition
- **When** I click "Approve" and optionally add comments
- **Then** the system records my approval with timestamp
- **And** routes the requisition to the next approver if required
- **And** notifies the recruiter of approval progress
- **And** auto-publishes the job if I am the final approver

**Scenario 4: Reject with feedback**
- **Given** I have concerns about a job requisition
- **When** I click "Reject" and provide mandatory comments explaining the reason
- **Then** the system returns the requisition to the recruiter as draft status
- **And** notifies the recruiter with my feedback
- **And** allows the recruiter to revise and resubmit

**Scenario 5: Mobile approval**
- **Given** I receive an approval notification while away from my desk
- **When** I open the approval link on my mobile device
- **Then** the interface is optimized for mobile viewing
- **And** I can approve or reject with minimal clicks
- **And** all approval actions are recorded identically to desktop

### **Dependencies**
- **Technical:** Workflow engine, notification service (email + in-app), mobile-responsive UI
- **Data:** Approval workflows configuration, budget/headcount data, user permissions
- **Integration:** Email service (SendGrid/AWS SES), calendar for deadline tracking
- **Prerequisite Stories:** US-001 (job requisition creation)

### **Notes**
- **Assumptions:** Approval workflows are pre-configured by admin based on department and salary thresholds
- **Open Questions:** Should there be SLA tracking for approval response times? What happens if an approver is out of office?
- **Technical Considerations:** API endpoints: GET /api/approvals/pending, POST /api/approvals/{id}/approve, POST /api/approvals/{id}/reject

---

### **User Story US-003**
**ID:** `US-003`  
**Epic:** E-001 (Job Lifecycle Management)  
**Feature:** F-003 (Multi-Channel Job Publishing)  
**Priority:** P0  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** publish approved jobs to multiple job boards and platforms with a single action,  
**So that** I can maximize candidate reach while reducing manual posting effort from 30 minutes to 2 minutes per job.

### **Description**
Recruiters need to distribute job postings across multiple channels (LinkedIn, Indeed, Glassdoor, company careers page) efficiently. The system should handle channel-specific formatting, track publishing status, and provide visibility into where each job is live.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Select publishing channels**
- **Given** I have an approved job requisition
- **When** I navigate to the "Publish" section
- **Then** I see a list of available channels (LinkedIn, Indeed, Glassdoor, Careers Page, Social Media)
- **And** I can select multiple channels with checkboxes
- **And** I see estimated reach and cost per channel
- **And** I can preview how the job will appear on each channel

**Scenario 2: Publish to multiple channels**
- **Given** I have selected LinkedIn, Indeed, and Company Careers Page
- **When** I click "Publish Now"
- **Then** the system posts the job to all selected channels within 2 minutes
- **And** optimizes content formatting for each platform
- **And** displays real-time publishing status for each channel
- **And** notifies me when all publications are complete

**Scenario 3: Handle publishing failures**
- **Given** the system attempts to publish to multiple channels
- **When** one channel fails (e.g., LinkedIn API error)
- **Then** the system continues publishing to other channels
- **And** logs the error with details
- **And** notifies me of the failure with suggested remediation
- **And** allows me to retry the failed channel

**Scenario 4: Schedule future publishing**
- **Given** I want to publish a job at a specific date/time
- **When** I select "Schedule" and choose a future date/time
- **Then** the system saves the scheduled publication
- **And** automatically publishes at the specified time
- **And** sends me a confirmation when published
- **And** handles timezone conversions correctly

**Scenario 5: Track publishing status**
- **Given** I have published jobs across multiple channels
- **When** I view the job's publishing dashboard
- **Then** I see the status of each channel (live, pending, failed, expired)
- **And** I see application counts by channel
- **And** I see cost tracking per channel
- **And** I can refresh or unpublish from specific channels

### **Dependencies**
- **Technical:** Job board API integrations (LinkedIn Jobs API, Indeed API, Glassdoor API), job scheduler
- **Data:** Job posting data, channel credentials, publishing history
- **Integration:** LinkedIn Jobs API, Indeed API, Glassdoor API, company CMS for careers page
- **Prerequisite Stories:** US-001 (job creation), US-002 (approval)

### **Notes**
- **Assumptions:** API credentials for all job boards are configured during system setup
- **Open Questions:** What's the retry logic for failed publications? Should we support automatic job refresh before expiration?
- **Technical Considerations:** API endpoints: POST /api/jobs/{id}/publish, GET /api/jobs/{id}/publishing-status, POST /api/jobs/{id}/unpublish

---

### **User Story US-004**
**ID:** `US-004`  
**Epic:** E-002 (Intelligent Candidate Sourcing)  
**Feature:** F-005 (Advanced Candidate Search)  
**Priority:** P0  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** search the internal candidate database using Boolean operators and semantic search,  
**So that** I can find relevant candidates 5x faster with 90%+ accuracy compared to manual review.

### **Description**
Recruiters need powerful search capabilities to discover qualified candidates from the internal database. The system should support Boolean queries, fuzzy matching, semantic understanding, and provide relevance-ranked results with saved search functionality.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Boolean search with operators**
- **Given** I am searching for candidates
- **When** I enter a Boolean query like "Python AND (Django OR Flask) NOT Java"
- **Then** the system returns candidates matching the exact Boolean logic
- **And** ranks results by relevance score
- **And** highlights matching keywords in candidate profiles
- **And** displays result count and search execution time

**Scenario 2: Fuzzy matching for skills**
- **Given** I search for "software engineer"
- **When** the system performs fuzzy matching
- **Then** it also returns candidates with titles like "software developer", "programmer", "SWE"
- **And** indicates the match type (exact, fuzzy, semantic)
- **And** allows me to adjust fuzzy matching sensitivity

**Scenario 3: Semantic search understanding**
- **Given** I search for "machine learning"
- **When** the system applies semantic understanding
- **Then** it includes candidates with related skills (deep learning, neural networks, AI, data science)
- **And** explains why each candidate was included
- **And** ranks by semantic relevance

**Scenario 4: Save and reuse search filters**
- **Given** I have created a complex search query
- **When** I click "Save Search" and provide a name
- **Then** the system saves all search parameters
- **And** allows me to access saved searches from a dropdown
- **And** optionally creates alerts for new candidates matching the criteria
- **And** lets me share saved searches with team members

**Scenario 5: Filter and refine results**
- **Given** I have search results displayed
- **When** I apply filters (location, experience years, education, availability)
- **Then** the results update in real-time
- **And** I see the count of candidates per filter option
- **And** I can combine multiple filters
- **And** I can clear filters individually or all at once

### **Dependencies**
- **Technical:** ElasticSearch for full-text search, semantic search engine, query parser
- **Data:** Candidate profiles, skills taxonomy, search history
- **Integration:** None for MVP
- **Prerequisite Stories:** US-006 (CV parsing to populate candidate database)

### **Notes**
- **Assumptions:** Candidate database is populated with structured data from CV parsing
- **Open Questions:** Should search history influence future search suggestions? What's the maximum result set size?
- **Technical Considerations:** API endpoints: POST /api/candidates/search, GET /api/candidates/saved-searches, POST /api/candidates/save-search

---

### **User Story US-005**
**ID:** `US-005`  
**Epic:** E-002 (Intelligent Candidate Sourcing)  
**Feature:** F-006 (External Platform Integration)  
**Priority:** P0  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** import candidate profiles from LinkedIn with one click,  
**So that** I can eliminate manual data entry and expand my sourcing reach to 500M+ professional profiles.

### **Description**
Recruiters spend significant time manually copying candidate information from LinkedIn to the ATS. The system should provide OAuth-based LinkedIn integration enabling one-click profile import with automatic data mapping, duplicate detection, and profile enrichment.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Connect LinkedIn account**
- **Given** I want to import candidates from LinkedIn
- **When** I click "Connect LinkedIn" in settings
- **Then** the system redirects me to LinkedIn OAuth authorization
- **And** I grant LTI ATS permission to access my LinkedIn Recruiter account
- **And** the system stores my OAuth token securely
- **And** confirms successful connection with my LinkedIn profile details

**Scenario 2: Import candidate profile**
- **Given** I am viewing a candidate profile on LinkedIn
- **When** I click the "Import to LTI ATS" button
- **Then** the system extracts all available data (name, title, company, experience, education, skills)
- **And** maps LinkedIn fields to LTI ATS schema automatically
- **And** displays a preview of the imported data for review
- **And** allows me to edit before saving

**Scenario 3: Duplicate detection**
- **Given** I import a candidate profile from LinkedIn
- **When** the system detects an existing candidate with the same email or LinkedIn URL
- **Then** it alerts me about the potential duplicate
- **And** shows both profiles side-by-side for comparison
- **And** offers to merge profiles or create a new one
- **And** preserves all historical data if merged

**Scenario 4: Associate with job opening**
- **Given** I am importing a candidate
- **When** I select "Associate with Job" during import
- **Then** the system shows a list of my active job openings
- **And** allows me to select one or multiple jobs
- **And** automatically creates applications for selected jobs
- **And** triggers initial screening workflow

**Scenario 5: Bulk import**
- **Given** I have identified multiple candidates on LinkedIn
- **When** I select multiple profiles and click "Bulk Import"
- **Then** the system queues all imports for processing
- **And** shows progress indicator for batch import
- **And** notifies me when all imports are complete
- **And** provides a summary report (successful, failed, duplicates)

### **Dependencies**
- **Technical:** LinkedIn Recruiter API, OAuth 2.0 authentication, data mapping engine, duplicate detection algorithm
- **Data:** LinkedIn OAuth credentials, candidate schema mapping rules
- **Integration:** LinkedIn Recruiter API
- **Prerequisite Stories:** US-006 (CV parsing for data normalization)

### **Notes**
- **Assumptions:** Organization has LinkedIn Recruiter license; API rate limits are sufficient for typical usage
- **Open Questions:** What's the LinkedIn API rate limit? How to handle API quota exhaustion? Should we cache LinkedIn data?
- **Technical Considerations:** API endpoints: POST /api/integrations/linkedin/connect, POST /api/integrations/linkedin/import, GET /api/integrations/linkedin/status

---

### **User Story US-006**
**ID:** `US-006`  
**Epic:** E-003 (AI-Powered Screening & Matching)  
**Feature:** F-009 (Automated CV Parsing)  
**Priority:** P0  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** automatically extract structured data from candidate resumes,  
**So that** I can eliminate 5 minutes of manual data entry per candidate with 95%+ accuracy.

### **Description**
Manual resume data entry is time-consuming and error-prone. The system should use NLP-based parsing to extract contact information, work history, education, skills, and certifications from resumes in multiple formats and languages, creating structured candidate profiles automatically.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Parse resume on upload**
- **Given** a candidate submits an application with a resume
- **When** the resume file is uploaded (PDF, DOC, DOCX)
- **Then** the system automatically parses the resume within 10 seconds
- **And** extracts contact info (name, email, phone, location)
- **And** extracts work history (company, title, dates, responsibilities)
- **And** extracts education (institution, degree, field, graduation date)
- **And** extracts skills and certifications

**Scenario 2: Handle multiple resume formats**
- **Given** candidates submit resumes in various formats
- **When** the system parses chronological, functional, or hybrid resume layouts
- **Then** it correctly identifies sections regardless of format
- **And** handles multi-column layouts
- **And** processes resumes with graphics and tables
- **And** extracts text from scanned PDFs using OCR if needed

**Scenario 3: Multi-language support**
- **Given** a candidate submits a resume in Spanish
- **When** the system detects the language
- **Then** it applies language-specific parsing rules
- **And** correctly extracts data in the source language
- **And** optionally translates to English for review
- **And** supports English, Spanish, Portuguese, French, German

**Scenario 4: Confidence scoring and manual review**
- **Given** the system has parsed a resume
- **When** extraction confidence is below 80% for any field
- **Then** it flags the field for manual review
- **And** highlights low-confidence extractions in yellow
- **And** allows me to correct and confirm the data
- **And** learns from my corrections to improve future parsing

**Scenario 5: Continuous learning**
- **Given** I have manually corrected parsed resume data
- **When** I save the corrections
- **Then** the system records the correction as training data
- **And** improves parsing accuracy for similar resumes
- **And** shows parsing accuracy metrics over time
- **And** identifies patterns in parsing errors for model improvement

### **Dependencies**
- **Technical:** Python/FastAPI AI service, spaCy NLP library, OCR engine (Tesseract), ML model training pipeline
- **Data:** Resume training dataset (1000+ samples), entity recognition models
- **Integration:** None for MVP
- **Prerequisite Stories:** None (foundational AI capability)

### **Notes**
- **Assumptions:** Initial ML model is pre-trained on diverse resume dataset
- **Open Questions:** What's the acceptable parsing accuracy threshold? How to handle resumes with unusual formats (infographics, video resumes)?
- **Technical Considerations:** API endpoints: POST /api/candidates/parse-resume, GET /api/candidates/{id}/parsing-confidence, POST /api/candidates/{id}/correct-parsing

---

### **User Story US-007**
**ID:** `US-007`  
**Epic:** E-003 (AI-Powered Screening & Matching)  
**Feature:** F-010 (AI Job-Fit Matching Score)  
**Priority:** P0  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** see an AI-calculated matching score for each candidate,  
**So that** I can automatically prioritize the top 10% of candidates and focus on high-potential matches.

### **Description**
Recruiters need an objective way to prioritize candidates from large applicant pools. The system should calculate a 0-100 matching score based on skills, experience, education, and historical success patterns, with explainable AI showing score breakdown and continuous learning from hiring outcomes.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Calculate matching score on application**
- **Given** a candidate applies to a job
- **When** their profile is complete with parsed resume data
- **Then** the system calculates a matching score (0-100) within 5 seconds
- **And** displays the score prominently on the candidate card
- **And** color-codes the score (green 80+, yellow 60-79, red <60)
- **And** ranks candidates by score in the pipeline

**Scenario 2: Explain score breakdown**
- **Given** I am viewing a candidate with a matching score of 85
- **When** I click "View Score Breakdown"
- **Then** the system shows contribution of each factor:
  - Skills match: 40% weight, 90/100 score
  - Experience level: 30% weight, 85/100 score
  - Education: 20% weight, 80/100 score
  - Other factors: 10% weight, 75/100 score
- **And** highlights which requirements are met vs. missing
- **And** explains semantic matches (e.g., "React.js" matched to "React")

**Scenario 3: Adjust matching criteria per job**
- **Given** I am configuring a job requisition
- **When** I access "Matching Criteria Settings"
- **Then** I can adjust the weight of each factor (skills, experience, education)
- **And** I can mark certain skills as must-have vs. nice-to-have
- **And** I can set minimum experience years required
- **And** the system recalculates all candidate scores based on new criteria

**Scenario 4: Continuous learning from outcomes**
- **Given** I have hired or rejected candidates
- **When** I record the final hiring decision
- **Then** the system uses this outcome as training data
- **And** adjusts matching algorithm weights based on successful hires
- **And** improves score accuracy over time
- **And** shows algorithm performance metrics (precision, recall)

**Scenario 5: Handle edge cases**
- **Given** a candidate has incomplete profile data
- **When** the system calculates the matching score
- **Then** it adjusts scoring based on available data
- **And** flags missing information that could improve the score
- **And** suggests requesting additional information from the candidate
- **And** still provides a preliminary score with confidence level

### **Dependencies**
- **Technical:** ML matching algorithm, feature engineering pipeline, model training infrastructure
- **Data:** Job requirements, candidate profiles, historical hiring outcomes (hire/reject decisions)
- **Integration:** None for MVP
- **Prerequisite Stories:** US-006 (CV parsing), US-001 (job creation with requirements)

### **Notes**
- **Assumptions:** Initial algorithm uses rule-based scoring; ML model improves with hiring outcome data
- **Open Questions:** What's the minimum data required for accurate scoring? How to prevent bias in matching algorithm?
- **Technical Considerations:** API endpoints: GET /api/applications/{id}/matching-score, POST /api/jobs/{id}/matching-criteria, POST /api/applications/{id}/record-outcome

---

### **User Story US-008**
**ID:** `US-008`  
**Epic:** E-004 (Collaborative Evaluation & Decision-Making)  
**Feature:** F-013 (Customizable Scorecards)  
**Priority:** P0  
**Persona:** Interviewer

**As an** Interviewer,  
**I want to** complete structured scorecards with weighted criteria for each candidate,  
**So that** I can provide consistent, unbiased evaluations that improve hiring quality.

### **Description**
Interviewers need standardized evaluation templates that ensure all candidates are assessed against the same criteria. The system should provide role-specific scorecards with a mix of quantitative ratings and qualitative feedback, ensuring structured and comparable evaluations.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Access assigned scorecard**
- **Given** I am assigned to interview a candidate
- **When** I access the candidate's profile after the interview
- **Then** I see the pre-configured scorecard template for this role
- **And** the scorecard shows weighted criteria (e.g., Technical Skills 40%, Communication 30%, Culture Fit 30%)
- **And** I see clear instructions for each evaluation criterion

**Scenario 2: Complete scorecard ratings**
- **Given** I am filling out a scorecard
- **When** I rate each criterion on a 1-5 scale
- **Then** the system calculates a weighted overall score automatically
- **And** requires ratings for all mandatory fields before submission
- **And** allows optional fields to be skipped
- **And** shows real-time score calculation as I enter ratings

**Scenario 3: Add qualitative feedback**
- **Given** I am completing a scorecard
- **When** I add comments in the qualitative feedback sections
- **Then** I can write detailed observations for each criterion
- **And** I can use rich text formatting (bold, italic, lists)
- **And** I can attach files (notes, code samples, presentations)
- **And** my comments are private until I submit the scorecard

**Scenario 4: Submit final recommendation**
- **Given** I have completed all required fields
- **When** I select my final recommendation (Strong Yes, Yes, Maybe, No, Strong No)
- **Then** the system saves my evaluation with timestamp
- **And** notifies the hiring manager and recruiter
- **And** adds my evaluation to the consolidated decision view
- **And** prevents further edits after submission (unless unlocked by admin)

**Scenario 5: Save draft and resume later**
- **Given** I am in the middle of completing a scorecard
- **When** I click "Save Draft"
- **Then** the system saves all entered data
- **And** allows me to resume from where I left off
- **And** reminds me if the scorecard is overdue
- **And** auto-saves every 2 minutes to prevent data loss

### **Dependencies**
- **Technical:** Scorecard template engine, weighted scoring calculator, rich text editor
- **Data:** Scorecard templates by role, evaluation history
- **Integration:** None for MVP
- **Prerequisite Stories:** US-001 (job creation with role definition)

### **Notes**
- **Assumptions:** Scorecard templates are pre-configured by admin or hiring manager
- **Open Questions:** Should interviewers see other evaluations before submitting their own? How to handle late scorecard submissions?
- **Technical Considerations:** API endpoints: GET /api/interviews/{id}/scorecard, POST /api/interviews/{id}/scorecard/submit, POST /api/interviews/{id}/scorecard/draft

---

### **User Story US-009**
**ID:** `US-009`  
**Epic:** E-004 (Collaborative Evaluation & Decision-Making)  
**Feature:** F-014 (Real-Time Commenting & Collaboration)  
**Priority:** P0  
**Persona:** Interviewer

**As an** Interviewer,  
**I want to** comment on candidate profiles and @mention team members in real-time,  
**So that** I can collaborate asynchronously and reduce meeting time by 60% while maintaining alignment.

### **Description**
Interview teams need to share insights and discuss candidates without scheduling multiple meetings. The system should provide real-time commenting with @mentions, notifications, and threaded discussions on candidate profiles.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Add comment to candidate profile**
- **Given** I am reviewing a candidate profile
- **When** I click "Add Comment" and type my observation
- **Then** the comment is saved with my name and timestamp
- **And** appears in the candidate's activity timeline
- **And** is visible to all team members with access to this candidate
- **And** supports rich text formatting and links

**Scenario 2: @mention team members**
- **Given** I am writing a comment
- **When** I type "@" followed by a team member's name
- **Then** the system shows an autocomplete list of team members
- **And** I can select a person to mention
- **And** the mentioned person receives an instant notification
- **And** the mention is highlighted in the comment

**Scenario 3: Receive real-time notifications**
- **Given** someone has @mentioned me in a comment
- **When** the comment is posted
- **Then** I receive an in-app notification immediately
- **And** I receive an email notification within 5 minutes
- **And** the notification includes the comment text and a direct link
- **And** I can reply directly from the notification

**Scenario 4: Thread discussions**
- **Given** there is an existing comment on a candidate
- **When** I click "Reply" on that comment
- **Then** my reply is nested under the original comment
- **And** creates a threaded discussion
- **And** notifies the original commenter
- **And** allows multiple levels of threading

**Scenario 5: Edit and delete comments**
- **Given** I have posted a comment
- **When** I realize I need to make changes
- **Then** I can edit my own comments within 24 hours
- **And** the system shows "edited" indicator with timestamp
- **And** I can delete my own comments
- **And** deleted comments show "[Comment deleted]" placeholder to maintain thread context

### **Dependencies**
- **Technical:** WebSocket for real-time updates, notification service, rich text editor
- **Data:** Comment threads, user mentions, notification preferences
- **Integration:** Email service for notifications
- **Prerequisite Stories:** None (foundational collaboration feature)

### **Notes**
- **Assumptions:** All interview team members have access to candidate profiles
- **Open Questions:** Should comments be searchable? How long should comment history be retained?
- **Technical Considerations:** API endpoints: POST /api/candidates/{id}/comments, PUT /api/comments/{id}, DELETE /api/comments/{id}, WebSocket: /ws/candidates/{id}/comments

---

### **User Story US-010**
**ID:** `US-010`  
**Epic:** E-004 (Collaborative Evaluation & Decision-Making)  
**Feature:** F-017 (Consolidated Decision View)  
**Priority:** P0  
**Persona:** Hiring Manager

**As a** Hiring Manager,  
**I want to** view all interviewer feedback in a consolidated dashboard with AI recommendations,  
**So that** I can make data-driven hiring decisions 70% faster with comprehensive visibility.

### **Description**
Hiring managers need a single view aggregating all interviewer scorecards, comments, AI insights, and assessment results to make informed hiring decisions. The system should provide visual summaries, weighted scores, and side-by-side candidate comparisons.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: View consolidated evaluation dashboard**
- **Given** all interviewers have submitted their scorecards for a candidate
- **When** I access the candidate's evaluation summary
- **Then** I see a visual dashboard with all interviewer ratings
- **And** I see the weighted overall score across all evaluations
- **And** I see a breakdown by evaluation criterion
- **And** I see all qualitative comments in chronological order

**Scenario 2: Review AI recommendation**
- **Given** the AI has analyzed all evaluation data
- **When** I view the consolidated decision view
- **Then** I see the AI recommendation (Hire, Maybe, Pass) with confidence score
- **And** I see the explanation for the AI recommendation
- **And** I see how this candidate compares to historical successful hires
- **And** I can override the AI recommendation with my own judgment

**Scenario 3: Compare multiple candidates**
- **Given** I am deciding between multiple finalists
- **When** I select 2-4 candidates for side-by-side comparison
- **Then** the system displays their scores and feedback in parallel columns
- **And** highlights strengths and weaknesses for each candidate
- **And** shows relative ranking on each criterion
- **And** helps identify the best fit based on weighted priorities

**Scenario 4: Track scorecard completion**
- **Given** I am waiting for all interviewers to submit feedback
- **When** I view the evaluation status
- **Then** I see which interviewers have completed scorecards
- **And** I see which scorecards are pending with days overdue
- **And** I can send reminder notifications to pending interviewers
- **And** I can proceed with decision even if some scorecards are missing

**Scenario 5: Record final decision**
- **Given** I have reviewed all evaluation data
- **When** I make my final hiring decision (Hire, Reject, Additional Round)
- **Then** I must provide a written justification
- **And** the system records my decision with timestamp
- **And** triggers the appropriate workflow (offer, rejection, next interview)
- **And** creates an audit trail for compliance

### **Dependencies**
- **Technical:** Data aggregation engine, visualization library (Chart.js/D3.js), AI recommendation service
- **Data:** Scorecard evaluations, AI insights, historical hiring data
- **Integration:** None for MVP
- **Prerequisite Stories:** US-008 (scorecard completion), US-007 (AI matching)

### **Notes**
- **Assumptions:** All interviewers submit scorecards before hiring manager makes final decision
- **Open Questions:** What's the minimum number of completed scorecards required for a decision? Should there be a deadline for scorecard submission?
- **Technical Considerations:** API endpoints: GET /api/candidates/{id}/consolidated-evaluation, POST /api/candidates/{id}/final-decision, GET /api/candidates/compare

---

### **User Story US-011**
**ID:** `US-011`  
**Epic:** E-005 (Pipeline & Workflow Automation)  
**Feature:** F-018 (Visual Kanban Pipeline Board)  
**Priority:** P0  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** manage candidates through pipeline stages using a drag-and-drop Kanban board,  
**So that** I can visualize pipeline status and move candidates efficiently with instant updates.

### **Description**
Recruiters need visual pipeline management to track candidate progress through hiring stages. The system should provide a customizable Kanban board with drag-and-drop functionality, filters, and real-time updates for efficient candidate management.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: View Kanban pipeline board**
- **Given** I am managing a job requisition
- **When** I navigate to the pipeline view
- **Then** I see all pipeline stages as columns (Applied, Phone Screen, Technical, Offer, etc.)
- **And** I see candidate cards in each stage
- **And** each card shows key info (name, AI score, days in stage, priority)
- **And** I see candidate count at the top of each column

**Scenario 2: Drag and drop candidates**
- **Given** I want to move a candidate to the next stage
- **When** I drag the candidate card from "Phone Screen" to "Technical Interview"
- **Then** the candidate moves to the new stage instantly
- **And** the system updates the candidate's stage in the database
- **And** triggers any automated workflows configured for that stage
- **And** records the stage transition in the activity log

**Scenario 3: Filter and search candidates**
- **Given** I have many candidates in the pipeline
- **When** I apply filters (recruiter, rating, source, date range)
- **Then** the board shows only candidates matching the filters
- **And** I can search by candidate name or email
- **And** I can save filter combinations for quick access
- **And** I can clear all filters with one click

**Scenario 4: Customize pipeline stages**
- **Given** I want to tailor the pipeline for this job
- **When** I access "Configure Pipeline" settings
- **Then** I can add, remove, or rename stages
- **And** I can reorder stages by dragging
- **And** I can set stage-specific automation rules
- **And** changes apply only to this job without affecting others

**Scenario 5: Mobile-responsive view**
- **Given** I am accessing the pipeline on a mobile device
- **When** I view the Kanban board
- **Then** the interface adapts to mobile screen size
- **And** I can swipe horizontally to view all stages
- **And** I can tap to expand candidate cards for details
- **And** drag-and-drop works with touch gestures

### **Dependencies**
- **Technical:** React drag-and-drop library, WebSocket for real-time updates, responsive UI framework
- **Data:** Pipeline stages configuration, candidate applications, stage transition history
- **Integration:** None for MVP
- **Prerequisite Stories:** US-001 (job creation), US-006 (candidate profiles)

### **Notes**
- **Assumptions:** Pipeline stages are configurable per job or use default template
- **Open Questions:** What's the maximum number of candidates per stage for performance? Should there be bulk stage transitions?
- **Technical Considerations:** API endpoints: GET /api/jobs/{id}/pipeline, POST /api/applications/{id}/move-stage, PUT /api/jobs/{id}/pipeline-config

---

### **User Story US-012**
**ID:** `US-012`  
**Epic:** E-005 (Pipeline & Workflow Automation)  
**Feature:** F-019 (Automated Workflow Engine)  
**Priority:** P0  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** configure automated actions triggered by stage transitions,  
**So that** I can eliminate 80% of manual follow-up tasks and ensure consistent candidate communication.

### **Description**
Recruiters spend significant time on repetitive tasks like sending emails, creating reminders, and updating fields when candidates move through stages. The system should provide a workflow automation engine with trigger-action configuration, conditional logic, and audit logging.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Configure workflow trigger**
- **Given** I am setting up automation for a job
- **When** I access the workflow designer
- **Then** I can select a trigger event (e.g., "Candidate moved to Interview stage")
- **And** I can add conditions (e.g., "If AI score > 80")
- **And** I can configure multiple triggers for different stages
- **And** I see a visual representation of the workflow

**Scenario 2: Define automated actions**
- **Given** I have configured a trigger
- **When** I add actions to execute
- **Then** I can choose from action types: send email, create task, send notification, update field, call webhook
- **And** I can configure action parameters (email template, task assignee, field value)
- **And** I can add multiple actions to a single trigger
- **And** I can set action execution order

**Scenario 3: Use email templates with merge fields**
- **Given** I am configuring an "send email" action
- **When** I select an email template
- **Then** the template includes merge fields ({{candidate_name}}, {{job_title}}, {{interview_date}})
- **And** the system automatically populates merge fields with candidate data
- **And** I can preview the email with sample data
- **And** I can customize the template for this specific workflow

**Scenario 4: Execute workflow automatically**
- **Given** I have configured a workflow: "When moved to Interview → Send interview invitation email"
- **When** I move a candidate to the Interview stage
- **Then** the system automatically sends the email within 1 minute
- **And** logs the action in the candidate's activity timeline
- **And** tracks email delivery status
- **And** notifies me if the action fails

**Scenario 5: Audit and troubleshoot workflows**
- **Given** I have multiple workflows configured
- **When** I access the workflow audit log
- **Then** I see all workflow executions with timestamps
- **And** I see success/failure status for each action
- **And** I see error messages for failed actions
- **And** I can disable/enable workflows without deleting them

### **Dependencies**
- **Technical:** Workflow engine, job scheduler, email service (SMTP), webhook caller
- **Data:** Workflow configurations, email templates, execution logs
- **Integration:** Email service (SendGrid/AWS SES), webhook endpoints
- **Prerequisite Stories:** US-011 (pipeline stages), US-013 (email templates)

### **Notes**
- **Assumptions:** Workflow engine supports conditional logic and multiple action types
- **Open Questions:** What's the maximum number of workflows per job? Should workflows be shareable across jobs?
- **Technical Considerations:** API endpoints: POST /api/jobs/{id}/workflows, GET /api/workflows/{id}/executions, PUT /api/workflows/{id}/enable

---

### **User Story US-013**
**ID:** `US-013`  
**Epic:** E-006 (Multi-Channel Communication)  
**Feature:** F-023 (Email Template Library)  
**Priority:** P0  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** send emails using customizable templates with merge fields,  
**So that** I can ensure consistent, professional communication while saving 10 minutes per email.

### **Description**
Recruiters send many similar emails throughout the hiring process. The system should provide a template library organized by use case, with dynamic merge fields, HTML editing, and preview functionality to streamline communication.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Browse template library**
- **Given** I want to send an email to a candidate
- **When** I click "Send Email" and access the template library
- **Then** I see templates organized by category (Application Received, Interview Invitation, Rejection, Offer)
- **And** I can search templates by name or keyword
- **And** I can preview each template before selecting
- **And** I see which templates are most frequently used

**Scenario 2: Use merge fields**
- **Given** I have selected the "Interview Invitation" template
- **When** I view the template content
- **Then** I see merge fields like {{candidate_name}}, {{job_title}}, {{interview_date}}, {{company_name}}
- **And** the system automatically populates merge fields with candidate and job data
- **And** I can manually edit any field before sending
- **And** I see a preview with actual data populated

**Scenario 3: Customize template with HTML editor**
- **Given** I want to modify a template
- **When** I click "Edit Template"
- **Then** I access a WYSIWYG HTML editor
- **And** I can format text (bold, italic, headings, lists)
- **And** I can add links and images
- **And** I can switch between visual and HTML code views
- **And** I can save as a new template or update the existing one

**Scenario 4: Preview before sending**
- **Given** I have customized an email
- **When** I click "Preview"
- **Then** I see exactly how the email will appear to the recipient
- **And** I see both HTML and plain text versions
- **And** I can send a test email to myself
- **And** I can make final edits before sending

**Scenario 5: Manage template library**
- **Given** I am an admin or recruiter
- **When** I access template management
- **Then** I can create new templates from scratch
- **And** I can edit existing templates
- **And** I can archive unused templates
- **And** I can set templates as organization-wide or personal
- **And** I can version templates and restore previous versions

### **Dependencies**
- **Technical:** Email service (SMTP), HTML editor (WYSIWYG), template engine
- **Data:** Email templates, merge field mappings, candidate/job data
- **Integration:** Email service (SendGrid/AWS SES)
- **Prerequisite Stories:** None (foundational communication feature)

### **Notes**
- **Assumptions:** Email templates support HTML and plain text formats
- **Open Questions:** Should there be approval workflow for template changes? How to handle multi-language templates?
- **Technical Considerations:** API endpoints: GET /api/email-templates, POST /api/email-templates, POST /api/candidates/{id}/send-email

---

### **User Story US-014**
**ID:** `US-014`  
**Epic:** E-006 (Multi-Channel Communication)  
**Feature:** F-024 (Automated Email Triggers)  
**Priority:** P0  
**Persona:** Candidate

**As a** Candidate,  
**I want to** receive timely automated email updates about my application status,  
**So that** I stay informed throughout the hiring process and have a positive candidate experience.

### **Description**
Candidates expect transparent communication about their application status. The system should automatically send email updates at key milestones (application received, interview scheduled, decision made) with personalized content and tracking.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Receive application confirmation**
- **Given** I have submitted an application through the careers portal
- **When** my application is successfully received
- **Then** I receive a confirmation email within 5 minutes
- **And** the email includes the job title and company name
- **And** the email sets expectations for next steps and timeline
- **And** the email includes a link to track my application status

**Scenario 2: Receive interview invitation**
- **Given** the recruiter has moved me to the interview stage
- **When** the stage transition occurs
- **Then** I receive an interview invitation email within 10 minutes
- **And** the email includes interview details (date, time, location/link, interviewers)
- **And** the email includes a calendar invite attachment
- **And** the email provides instructions for preparation

**Scenario 3: Receive status updates**
- **Given** my application progresses through stages
- **When** I move to a new stage (e.g., Technical Review, Final Interview)
- **Then** I receive an email update within 1 hour
- **And** the email explains the current stage and what to expect
- **And** the email provides an estimated timeline for next steps
- **And** the email maintains a professional, encouraging tone

**Scenario 4: Track email engagement**
- **Given** the system has sent me an email
- **When** I open the email or click links
- **Then** the system tracks open and click events
- **And** the recruiter can see engagement metrics
- **And** my privacy is respected (no tracking pixels if I block them)
- **And** I can opt out of tracking while still receiving emails

**Scenario 5: Manage communication preferences**
- **Given** I am receiving automated emails
- **When** I access my candidate portal
- **Then** I can view my communication preferences
- **And** I can choose email frequency (all updates, major milestones only, none)
- **And** I can update my email address
- **And** I can unsubscribe from non-essential emails while keeping critical updates

### **Dependencies**
- **Technical:** Email service with delivery tracking, workflow automation engine, candidate portal
- **Data:** Email templates, candidate preferences, delivery logs
- **Integration:** Email service (SendGrid/AWS SES) with tracking capabilities
- **Prerequisite Stories:** US-012 (workflow automation), US-013 (email templates)

### **Notes**
- **Assumptions:** All automated emails comply with CAN-SPAM and GDPR regulations
- **Open Questions:** What's the email delivery SLA? How to handle bounced emails?
- **Technical Considerations:** API endpoints: POST /api/candidates/{id}/send-automated-email, GET /api/candidates/{id}/email-history, PUT /api/candidates/{id}/communication-preferences

---

### **User Story US-015**
**ID:** `US-015`  
**Epic:** E-007 (Analytics & Predictive Insights)  
**Feature:** F-028 (Executive Dashboard)  
**Priority:** P0  
**Persona:** Hiring Manager

**As a** Hiring Manager,  
**I want to** view real-time KPI dashboards with key recruitment metrics,  
**So that** I can make data-driven decisions and track hiring performance across my team.

### **Description**
Hiring managers need instant visibility into recruitment performance to identify bottlenecks, optimize processes, and demonstrate ROI. The system should provide an executive dashboard with key metrics, visual charts, customizable date ranges, and export capabilities.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: View key metrics**
- **Given** I access the executive dashboard
- **When** the page loads
- **Then** I see key metrics: time-to-hire, cost-per-hire, source effectiveness, offer acceptance rate
- **And** each metric shows current value, trend (up/down), and comparison to previous period
- **And** metrics are color-coded (green for good, yellow for warning, red for concern)
- **And** I can click any metric to drill down into details

**Scenario 2: Visualize data with charts**
- **Given** I am viewing the dashboard
- **When** I scroll through the visualizations
- **Then** I see line charts for trends over time
- **And** I see bar charts for comparisons across departments
- **And** I see pie charts for distribution (sources, stages)
- **And** all charts are interactive with hover tooltips

**Scenario 3: Customize date ranges**
- **Given** I want to analyze a specific time period
- **When** I select a date range (last 7 days, 30 days, quarter, year, custom)
- **Then** all metrics and charts update to reflect the selected period
- **And** I can compare to previous period automatically
- **And** I can save custom date ranges as presets

**Scenario 4: Filter by dimensions**
- **Given** I manage multiple departments
- **When** I apply filters (department, location, job type, recruiter)
- **Then** the dashboard updates to show filtered data only
- **And** I can combine multiple filters
- **And** I see how many jobs/candidates match the current filters

**Scenario 5: Export dashboard**
- **Given** I want to share dashboard insights
- **When** I click "Export"
- **Then** I can choose format (PDF, Excel, PNG)
- **And** the export includes all visible charts and metrics
- **And** the export is generated within 30 seconds
- **And** I can schedule automated email delivery of the dashboard

### **Dependencies**
- **Technical:** Data warehouse, analytics service, visualization library (Chart.js/D3.js)
- **Data:** Historical hiring data, time-series metrics, aggregated statistics
- **Integration:** None for MVP
- **Prerequisite Stories:** All previous stories generate data for analytics

### **Notes**
- **Assumptions:** Dashboard updates in near real-time (5-minute refresh)
- **Open Questions:** What's the data retention period for historical metrics? Should there be role-based dashboard customization?
- **Technical Considerations:** API endpoints: GET /api/analytics/dashboard, GET /api/analytics/export, POST /api/analytics/schedule-report

---

### **User Story US-016**
**ID:** `US-016`  
**Epic:** E-008 (Integrations & Extensions)  
**Feature:** IN-001 (HRIS Integration)  
**Priority:** P0  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** automatically transfer hired candidate data to our HRIS system,  
**So that** I can eliminate manual data entry and ensure seamless onboarding.

### **Description**
When candidates are hired, their information needs to be transferred to the HRIS for onboarding. The system should provide OAuth-based integration with major HRIS platforms (BambooHR, Workday, SAP SuccessFactors) with automatic data sync and SSO support.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Connect HRIS system**
- **Given** I am an admin configuring integrations
- **When** I select "Connect HRIS" and choose BambooHR
- **Then** the system redirects me to BambooHR OAuth authorization
- **And** I grant LTI ATS permission to access employee data
- **And** the system stores OAuth credentials securely
- **And** confirms successful connection with sync status

**Scenario 2: Automatic data transfer on hire**
- **Given** a candidate has accepted an offer
- **When** I mark the candidate as "Hired" in the system
- **Then** the system automatically creates an employee record in the HRIS
- **And** transfers all relevant data (name, email, phone, start date, department, title, salary)
- **And** maps LTI ATS fields to HRIS fields correctly
- **And** notifies me when the transfer is complete

**Scenario 3: Handle sync errors**
- **Given** the system attempts to sync data to HRIS
- **When** the sync fails (e.g., missing required field, API error)
- **Then** the system logs the error with details
- **And** notifies me of the failure
- **And** provides suggested remediation steps
- **And** allows manual retry after fixing the issue

**Scenario 4: Sync organizational structure**
- **Given** the HRIS integration is active
- **When** I trigger "Sync Organization Data"
- **Then** the system imports departments, locations, and reporting structure from HRIS
- **And** updates LTI ATS organizational hierarchy
- **And** maps HRIS departments to LTI ATS departments
- **And** handles new, updated, and deleted departments

**Scenario 5: SSO authentication**
- **Given** HRIS integration supports SSO
- **When** users access LTI ATS
- **Then** they can log in using their HRIS credentials
- **And** user permissions sync from HRIS roles
- **And** new employees automatically get ATS access based on role
- **And** terminated employees lose access immediately

### **Dependencies**
- **Technical:** OAuth 2.0, HRIS API integrations (BambooHR, Workday, SAP), data mapping engine
- **Data:** Employee data schema, field mappings, organizational structure
- **Integration:** BambooHR API, Workday API, SAP SuccessFactors API
- **Prerequisite Stories:** US-001 (job creation with department), candidate hire workflow

### **Notes**
- **Assumptions:** Organization has active HRIS subscription with API access
- **Open Questions:** Should sync be real-time or batch? How to handle data conflicts between systems?
- **Technical Considerations:** API endpoints: POST /api/integrations/hris/connect, POST /api/integrations/hris/sync-employee, GET /api/integrations/hris/status

---

### **User Story US-017**
**ID:** `US-017`  
**Epic:** E-001 (Job Lifecycle Management)  
**Feature:** F-004 (Market Intelligence & Benchmarking)  
**Priority:** P1  
**Persona:** Hiring Manager

**As a** Hiring Manager,  
**I want to** view market salary benchmarks and competitive intelligence for job roles,  
**So that** I can make competitive offers and reduce offer rejection rate by 25%.

### **Description**
Hiring managers need market data to set competitive salaries and position jobs effectively. The system should provide real-time salary benchmarking, competitive analysis, and market demand insights integrated from external data sources.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: View salary recommendations**
- **Given** I am creating or reviewing a job requisition
- **When** I access the "Market Intelligence" section
- **Then** I see recommended salary ranges for this role, location, and experience level
- **And** I see 25th, 50th (median), and 75th percentile data
- **And** I see how my proposed salary compares to market
- **And** I see data sources and last update timestamp

**Scenario 2: Analyze competitive landscape**
- **Given** I want to understand competition for talent
- **When** I view competitive intelligence
- **Then** I see similar job postings from other companies
- **And** I see their salary ranges (if disclosed)
- **And** I see their key requirements and benefits
- **And** I see market demand indicators (high/medium/low)

**Scenario 3: Identify skills gaps**
- **Given** I am hiring for a technical role
- **When** I review skills analysis
- **Then** I see which skills are in high demand
- **And** I see which skills are hard to find (supply/demand ratio)
- **And** I see trending skills in my industry
- **And** I get recommendations for alternative skill combinations

**Scenario 4: Predict time-to-fill**
- **Given** I want to set realistic hiring timelines
- **When** I view time-to-fill predictions
- **Then** I see estimated time-to-fill based on role, location, and market conditions
- **And** I see historical data for similar roles in my organization
- **And** I see confidence intervals for the prediction
- **And** I can adjust job parameters to see impact on time-to-fill

**Scenario 5: Export market report**
- **Given** I need to justify salary decisions to leadership
- **When** I click "Export Market Report"
- **Then** the system generates a PDF with all market data
- **And** includes salary benchmarks, competitive analysis, and recommendations
- **And** includes charts and visualizations
- **And** is formatted for executive presentation

### **Dependencies**
- **Technical:** Market data API integrations, data analytics engine
- **Data:** Salary benchmark data, job posting aggregator data, skills taxonomy
- **Integration:** Glassdoor API, Payscale API, LinkedIn Salary API, Indeed API
- **Prerequisite Stories:** US-001 (job creation)

### **Notes**
- **Assumptions:** Market data APIs provide sufficient coverage for target markets
- **Open Questions:** What's the data refresh frequency? How to handle markets with limited data?
- **Technical Considerations:** API endpoints: GET /api/jobs/{id}/market-intelligence, GET /api/market-data/salary-benchmark, POST /api/market-data/export-report

---

### **User Story US-018**
**ID:** `US-018`  
**Epic:** E-002 (Intelligent Candidate Sourcing)  
**Feature:** F-008 (Talent Pool Management)  
**Priority:** P1  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** create and nurture segmented talent pools for passive candidates,  
**So that** I can build long-term pipelines reducing time-to-fill by 40% for future roles.

### **Description**
Recruiters need to maintain relationships with qualified candidates who aren't actively looking but might be interested in future opportunities. The system should provide talent pool creation, automated nurturing campaigns, engagement tracking, and easy activation for new jobs.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Create talent pool**
- **Given** I want to build a pipeline for future hiring needs
- **When** I click "Create Talent Pool" and define criteria
- **Then** I can name the pool (e.g., "Senior Backend Engineers - Bay Area")
- **And** I can set inclusion criteria (skills, location, experience, availability)
- **And** I can manually add candidates or import from search results
- **And** the system shows pool size and growth over time

**Scenario 2: Automated nurturing campaigns**
- **Given** I have created a talent pool
- **When** I configure a nurturing campaign
- **Then** I can select email templates for the campaign
- **And** I can set email frequency (monthly newsletter, quarterly check-in)
- **And** I can personalize content based on candidate attributes
- **And** the system automatically sends emails to all pool members

**Scenario 3: Track engagement metrics**
- **Given** I am running nurturing campaigns
- **When** I view pool analytics
- **Then** I see engagement metrics (email open rate, click rate, response rate)
- **And** I see which candidates are most engaged
- **And** I see pool health score (engagement level, profile freshness)
- **And** I can segment by engagement level for targeted outreach

**Scenario 4: Activate pool for new job**
- **Given** I have a new job opening
- **When** I select "Source from Talent Pool"
- **Then** I see all relevant talent pools based on job requirements
- **And** I can preview matching candidates from each pool
- **And** I can bulk-invite candidates to apply with one click
- **And** the system sends personalized job opportunity emails

**Scenario 5: Maintain pool freshness**
- **Given** talent pools can become stale over time
- **When** the system detects inactive candidates (no engagement in 6 months)
- **Then** it sends re-engagement emails automatically
- **And** it flags candidates for removal if still no response
- **And** it suggests updating pool criteria based on market changes
- **And** it notifies me of candidates who've been hired elsewhere (via LinkedIn integration)

### **Dependencies**
- **Technical:** Email campaign engine, engagement tracking, pool analytics
- **Data:** Candidate profiles, engagement history, pool configurations
- **Integration:** Email service (SendGrid/AWS SES), LinkedIn API for status updates
- **Prerequisite Stories:** US-004 (candidate search), US-013 (email templates)

### **Notes**
- **Assumptions:** Candidates have consented to being added to talent pools (GDPR compliance)
- **Open Questions:** What's the maximum pool size? Should pools be shareable across recruiters?
- **Technical Considerations:** API endpoints: POST /api/talent-pools, POST /api/talent-pools/{id}/campaigns, GET /api/talent-pools/{id}/analytics, POST /api/talent-pools/{id}/activate

---

### **User Story US-019**
**ID:** `US-019`  
**Epic:** E-003 (AI-Powered Screening & Matching)  
**Feature:** F-012 (Red Flag Detection)  
**Priority:** P1  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** be alerted to potential red flags in candidate resumes,  
**So that** I can identify concerns early and prevent bad hires.

### **Description**
Recruiters need to identify resume inconsistencies, employment gaps, and anomalous career progressions that might indicate concerns. The system should use AI to detect red flags, provide explanations, and allow recruiter override with justification.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Detect employment gaps**
- **Given** a candidate has a gap in employment history
- **When** the AI analyzes the resume
- **Then** it flags gaps longer than 6 months
- **And** indicates the gap duration and dates
- **And** assigns severity level (low/medium/high)
- **And** allows me to mark as "explained" with notes

**Scenario 2: Identify anomalous career progression**
- **Given** a candidate's work history shows unusual patterns
- **When** the AI detects a significant step backward (e.g., VP to junior role)
- **Then** it flags the anomaly with explanation
- **And** shows the specific role transition that triggered the flag
- **And** suggests questions to ask during screening
- **And** allows me to override if there's a valid explanation

**Scenario 3: Flag conflicting information**
- **Given** a resume contains inconsistent data
- **When** the AI detects conflicts (e.g., overlapping employment dates, education dates after work dates)
- **Then** it highlights the conflicting information
- **And** shows both conflicting data points side-by-side
- **And** assigns high severity to the flag
- **And** requires recruiter review before proceeding

**Scenario 4: Detect frequent job changes**
- **Given** a candidate has changed jobs frequently
- **When** the AI detects more than 5 jobs in 3 years
- **Then** it flags as potential job-hopping concern
- **And** calculates average tenure per role
- **And** considers industry norms (tech vs. retail)
- **And** allows me to assess if it's a concern for this role

**Scenario 5: Override and justify**
- **Given** the AI has flagged a concern
- **When** I review the flag and determine it's not a real issue
- **Then** I can mark the flag as "Not a Concern"
- **And** I must provide a justification for the override
- **And** the system records my override for audit purposes
- **And** the AI learns from overrides to improve future detection

### **Dependencies**
- **Technical:** AI analysis engine, pattern detection algorithms, audit logging
- **Data:** Resume data, employment history, industry benchmarks
- **Integration:** None for MVP
- **Prerequisite Stories:** US-006 (CV parsing)

### **Notes**
- **Assumptions:** Red flag detection is advisory, not blocking; recruiters make final decisions
- **Open Questions:** What's the acceptable false positive rate? Should flags be visible to hiring managers?
- **Technical Considerations:** API endpoints: GET /api/candidates/{id}/red-flags, POST /api/red-flags/{id}/override

---

### **User Story US-020**
**ID:** `US-020`  
**Epic:** E-003 (AI-Powered Screening & Matching)  
**Feature:** F-011 (Cultural Fit Analysis)  
**Priority:** P1  
**Persona:** Hiring Manager

**As a** Hiring Manager,  
**I want to** assess candidate cultural compatibility using AI analysis,  
**So that** I can reduce cultural mismatch turnover by 30% through proactive assessment.

### **Description**
Cultural fit is a key predictor of long-term success and retention. The system should analyze candidate communications, resume language, and social profiles to assess cultural compatibility against the company culture profile, while monitoring for bias.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Define company culture profile**
- **Given** I am setting up cultural fit analysis
- **When** I access "Company Culture Configuration"
- **Then** I can define our culture attributes (values, work style, communication preferences)
- **And** I can select from predefined culture frameworks (e.g., collaborative, innovative, results-driven)
- **And** I can customize with specific values important to our organization
- **And** I can set different profiles for different departments

**Scenario 2: Analyze candidate cultural fit**
- **Given** a candidate has submitted application materials
- **When** the AI performs cultural fit analysis
- **Then** it analyzes resume language and tone
- **And** it analyzes cover letter sentiment and value alignment
- **And** it analyzes LinkedIn profile (if available) for cultural indicators
- **And** it generates a compatibility score (0-100)

**Scenario 3: View compatibility insights**
- **Given** the AI has calculated a cultural fit score
- **When** I view the candidate's cultural fit analysis
- **Then** I see the overall compatibility score
- **And** I see breakdown by culture dimension (values, work style, communication)
- **And** I see specific examples from candidate materials supporting the score
- **And** I see potential cultural alignment strengths and concerns

**Scenario 4: Flag cultural misalignments**
- **Given** the AI detects potential cultural incompatibility
- **When** the compatibility score is below 60
- **Then** it flags specific areas of concern
- **And** it explains which cultural attributes are misaligned
- **And** it suggests interview questions to explore the concerns
- **And** it allows me to proceed if I believe the concerns are addressable

**Scenario 5: Monitor for bias**
- **Given** cultural fit analysis could introduce bias
- **When** the AI generates cultural fit scores
- **Then** it monitors for protected class correlations
- **And** it alerts if certain demographics consistently score lower
- **And** it provides bias audit reports to admins
- **And** it allows disabling cultural fit analysis if bias is detected

### **Dependencies**
- **Technical:** NLP engine, sentiment analysis, bias detection algorithms
- **Data:** Company culture profile, candidate communications, LinkedIn data
- **Integration:** LinkedIn API (optional)
- **Prerequisite Stories:** US-006 (CV parsing), US-005 (LinkedIn integration)

### **Notes**
- **Assumptions:** Cultural fit is one factor among many, not a sole decision criterion
- **Open Questions:** How to balance cultural fit with diversity goals? Should cultural fit scores be visible to all interviewers?
- **Technical Considerations:** API endpoints: POST /api/company/culture-profile, GET /api/candidates/{id}/cultural-fit, GET /api/analytics/bias-audit

---

### **User Story US-021**
**ID:** `US-021`  
**Epic:** E-004 (Collaborative Evaluation & Decision-Making)  
**Feature:** F-015 (Video Interview Platform)  
**Priority:** P1  
**Persona:** Interviewer

**As an** Interviewer,  
**I want to** review asynchronous video interview responses with AI transcription and sentiment analysis,  
**So that** I can conduct flexible screening reducing scheduling overhead by 80%.

### **Description**
Asynchronous video interviews enable scalable screening without scheduling constraints. The system should provide video question creation, candidate recording interface, automated transcription, sentiment analysis, and collaborative review capabilities.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Create video interview questions**
- **Given** I am setting up a video interview for a role
- **When** I access the video interview builder
- **Then** I can add multiple questions (text or video)
- **And** I can set time limits for each response (1-5 minutes)
- **And** I can set the number of allowed retakes (0-3)
- **And** I can preview the candidate experience

**Scenario 2: Candidate records responses**
- **Given** a candidate receives a video interview invitation
- **When** they access the interview link
- **Then** they see each question one at a time
- **And** they can record their response using webcam (web-based, no app required)
- **And** they can review and re-record within allowed retakes
- **And** they can see remaining time during recording
- **And** the system saves all responses automatically

**Scenario 3: Automated transcription**
- **Given** a candidate has completed the video interview
- **When** the system processes the recordings
- **Then** it generates automated transcripts within 10 minutes
- **And** it highlights key words and phrases
- **And** it timestamps each segment for easy navigation
- **And** it achieves 90%+ transcription accuracy

**Scenario 4: AI sentiment analysis**
- **Given** the system has transcribed the video responses
- **When** it performs sentiment analysis
- **Then** it detects overall sentiment (positive, neutral, negative) for each response
- **And** it identifies confidence and enthusiasm indicators
- **And** it flags concerning language patterns
- **And** it provides sentiment scores alongside transcripts

**Scenario 5: Collaborative review**
- **Given** multiple interviewers need to review the video interview
- **When** I access the video interview results
- **Then** I can watch responses with playback controls (speed, skip, timestamp notes)
- **And** I can add comments on specific timestamps
- **And** I can share video links with the interview team
- **And** I can see other interviewers' comments and ratings

### **Dependencies**
- **Technical:** Video streaming infrastructure, speech-to-text API, sentiment analysis engine, video storage
- **Data:** Interview questions, video recordings, transcripts
- **Integration:** Video transcription service (AWS Transcribe, Google Speech-to-Text)
- **Prerequisite Stories:** US-008 (scorecard evaluation)

### **Notes**
- **Assumptions:** Candidates have webcam and stable internet connection
- **Open Questions:** What's the video storage retention policy? What's the maximum video length per interview?
- **Technical Considerations:** API endpoints: POST /api/video-interviews, GET /api/video-interviews/{id}/transcript, GET /api/video-interviews/{id}/sentiment

---

### **User Story US-022**
**ID:** `US-022`  
**Epic:** E-005 (Pipeline & Workflow Automation)  
**Feature:** F-021 (Proactive Alerts & Reminders)  
**Priority:** P1  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** receive proactive alerts for stalled candidates and overdue tasks,  
**So that** I can prevent candidate drop-off and reduce time-to-hire by 25%.

### **Description**
Candidates can fall through the cracks when there's no activity for extended periods. The system should monitor candidate inactivity, send proactive alerts with suggested actions, and provide snooze/dismiss options to manage notification volume.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Configure inactivity thresholds**
- **Given** I want to set up proactive alerts
- **When** I access alert configuration
- **Then** I can set inactivity thresholds by stage (e.g., 5 days in Phone Screen, 3 days in Offer)
- **And** I can customize thresholds per job or use defaults
- **And** I can enable/disable alerts globally or per job

**Scenario 2: Receive stalled candidate alerts**
- **Given** a candidate has had no activity for 5 days in the Interview stage
- **When** the inactivity threshold is exceeded
- **Then** I receive an in-app notification
- **And** I receive an email alert (if email notifications enabled)
- **And** the alert includes candidate name, job, current stage, and days inactive
- **And** the alert suggests next actions (schedule interview, send follow-up, move to next stage)

**Scenario 3: View suggested actions**
- **Given** I have received a stalled candidate alert
- **When** I click on the alert
- **Then** the system suggests context-appropriate next actions
- **And** I can execute actions directly from the alert (send email, schedule interview, move stage)
- **And** I can mark the alert as resolved
- **And** I can snooze the alert for a specified period (1 day, 3 days, 1 week)

**Scenario 4: Daily digest of alerts**
- **Given** I have multiple alerts throughout the day
- **When** I have enabled daily digest mode
- **Then** I receive one consolidated email at my preferred time (e.g., 9 AM)
- **And** the digest lists all pending alerts grouped by priority
- **And** the digest includes summary statistics (total stalled candidates, average days inactive)
- **And** I can click through to take action on each alert

**Scenario 5: Escalation for repeated inactivity**
- **Given** a candidate has been stalled and I snoozed the alert
- **When** the snooze period expires and there's still no activity
- **Then** the system escalates the alert to my manager
- **And** increases the alert priority level
- **And** suggests more urgent actions
- **And** tracks escalation in the audit log

### **Dependencies**
- **Technical:** Job scheduler, notification service, alert engine
- **Data:** Candidate activity logs, inactivity thresholds, alert configurations
- **Integration:** Email service (SendGrid/AWS SES)
- **Prerequisite Stories:** US-011 (pipeline management)

### **Notes**
- **Assumptions:** Alerts are configurable to prevent notification fatigue
- **Open Questions:** What's the optimal alert frequency? Should alerts be role-based (different for recruiters vs. hiring managers)?
- **Technical Considerations:** API endpoints: GET /api/alerts/pending, POST /api/alerts/{id}/snooze, POST /api/alerts/{id}/resolve, PUT /api/alerts/configuration

---

### **User Story US-023**
**ID:** `US-023`  
**Epic:** E-005 (Pipeline & Workflow Automation)  
**Feature:** F-022 (Bulk Operations)  
**Priority:** P1  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** perform bulk operations on multiple candidates simultaneously,  
**So that** I can save 90% of time on repetitive tasks like rejecting 50 candidates.

### **Description**
Recruiters often need to perform the same action on many candidates (e.g., bulk rejection after initial screening). The system should provide multi-select functionality with bulk actions including stage transitions, email sending, tag application, and export.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Select multiple candidates**
- **Given** I am viewing the pipeline or candidate list
- **When** I want to perform bulk actions
- **Then** I can select multiple candidates using checkboxes
- **And** I can select all candidates on the current page
- **And** I can select all candidates matching current filters
- **And** I see the count of selected candidates

**Scenario 2: Bulk stage transition**
- **Given** I have selected 20 candidates
- **When** I choose "Move to Stage" from bulk actions
- **Then** I see a list of available stages
- **And** I can select the target stage
- **And** I see a confirmation dialog showing the number of candidates and target stage
- **And** the system moves all candidates and triggers stage-based workflows

**Scenario 3: Bulk email sending**
- **Given** I have selected 50 candidates to reject
- **When** I choose "Send Email" from bulk actions
- **Then** I can select an email template (e.g., "Rejection - Not Selected")
- **And** I can preview the email with merge fields populated
- **And** I can customize the email before sending
- **And** the system sends personalized emails to all selected candidates

**Scenario 4: Bulk tag application**
- **Given** I have selected candidates from a specific source
- **When** I choose "Add Tags" from bulk actions
- **Then** I can select existing tags or create new ones
- **And** I can add multiple tags at once
- **And** the system applies tags to all selected candidates
- **And** I can also remove tags in bulk

**Scenario 5: Bulk export**
- **Given** I have selected candidates or applied filters
- **When** I choose "Export" from bulk actions
- **Then** I can select export format (CSV, Excel)
- **And** I can choose which fields to include
- **And** the system generates the export file within 30 seconds
- **And** I can download the file or receive it via email

### **Dependencies**
- **Technical:** Batch processing engine, email queue, export generator
- **Data:** Candidate data, email templates, tags
- **Integration:** Email service (SendGrid/AWS SES)
- **Prerequisite Stories:** US-011 (pipeline), US-013 (email templates)

### **Notes**
- **Assumptions:** Bulk operations have reasonable limits (e.g., max 500 candidates per operation)
- **Open Questions:** Should there be undo functionality for bulk operations? What's the maximum batch size?
- **Technical Considerations:** API endpoints: POST /api/candidates/bulk/move-stage, POST /api/candidates/bulk/send-email, POST /api/candidates/bulk/add-tags, POST /api/candidates/bulk/export

---

### **User Story US-024**
**ID:** `US-024`  
**Epic:** E-006 (Multi-Channel Communication)  
**Feature:** F-026 (Smart Interview Scheduling)  
**Priority:** P1  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** schedule interviews using AI-powered calendar integration,  
**So that** I can reduce scheduling time from 15 minutes to 2 minutes and eliminate back-and-forth emails.

### **Description**
Interview scheduling involves coordinating multiple calendars and finding mutually available times. The system should integrate with Google Calendar and Outlook, detect availability, send scheduling options to candidates, and create calendar invites automatically.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Detect interviewer availability**
- **Given** I want to schedule an interview for a candidate
- **When** I select interviewers from the team
- **Then** the system checks their Google Calendar/Outlook for availability
- **And** it identifies 3-5 available time slots within the next 7 days
- **And** it respects working hours and time zones
- **And** it avoids scheduling back-to-back interviews (adds buffer time)

**Scenario 2: Send scheduling options to candidate**
- **Given** the system has identified available time slots
- **When** I click "Send Scheduling Link"
- **Then** the candidate receives an email with 3-5 time slot options
- **And** the email includes a self-scheduling interface
- **And** the candidate can select their preferred time with one click
- **And** the system handles timezone conversion automatically

**Scenario 3: Create calendar invites**
- **Given** the candidate has selected a time slot
- **When** the selection is confirmed
- **Then** the system creates calendar invites for all participants
- **And** it includes meeting details (candidate name, role, interview type)
- **And** it includes video meeting link (Zoom, Teams, or Google Meet)
- **And** it sends invites to interviewers and candidate within 1 minute

**Scenario 4: Send reminder emails**
- **Given** an interview is scheduled
- **When** the interview time approaches
- **Then** the system sends reminder emails 24 hours before
- **And** it sends reminder emails 1 hour before
- **And** reminders include interview details and video link
- **And** reminders include preparation instructions

**Scenario 5: Handle rescheduling**
- **Given** an interview needs to be rescheduled
- **When** I or the candidate request a reschedule
- **Then** the system cancels the existing calendar invite
- **And** it finds new available time slots
- **And** it sends rescheduling options to the candidate
- **And** it updates all participants' calendars automatically

### **Dependencies**
- **Technical:** Calendar API integrations (Google Calendar, Outlook), video conferencing APIs (Zoom, Teams)
- **Data:** Interviewer calendars, interview schedules, timezone data
- **Integration:** Google Calendar API, Microsoft Graph API (Outlook), Zoom API, Microsoft Teams API
- **Prerequisite Stories:** US-008 (interview assignments)

### **Notes**
- **Assumptions:** Interviewers have granted calendar access permissions
- **Open Questions:** Should the system support room booking for on-site interviews? What's the buffer time between interviews?
- **Technical Considerations:** API endpoints: POST /api/interviews/schedule, GET /api/interviews/{id}/availability, POST /api/interviews/{id}/reschedule

---

### **User Story US-025**
**ID:** `US-025`  
**Epic:** E-007 (Analytics & Predictive Insights)  
**Feature:** F-029 (Funnel Analysis)  
**Priority:** P1  
**Persona:** Hiring Manager

**As a** Hiring Manager,  
**I want to** analyze pipeline conversion metrics and identify bottlenecks,  
**So that** I can optimize the hiring process and improve conversion rates.

### **Description**
Understanding where candidates drop off in the pipeline is critical for process improvement. The system should provide funnel visualization, conversion rates between stages, time spent per stage, and drop-off reason analysis.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: View funnel visualization**
- **Given** I want to analyze the hiring funnel
- **When** I access funnel analysis
- **Then** I see a visual funnel chart showing all pipeline stages
- **And** I see candidate counts at each stage
- **And** I see conversion rates between consecutive stages
- **And** I can filter by job, department, date range

**Scenario 2: Identify bottlenecks**
- **Given** I am reviewing funnel metrics
- **When** the system detects low conversion rates
- **Then** it highlights stages with conversion rates below benchmark
- **And** it shows average time spent in each stage
- **And** it identifies stages where candidates spend excessive time
- **And** it suggests process improvements

**Scenario 3: Analyze drop-off reasons**
- **Given** candidates are rejected or withdrawn at various stages
- **When** I view drop-off analysis
- **Then** I see the most common rejection reasons by stage
- **And** I see candidate withdrawal reasons
- **And** I see trends over time (improving or worsening)
- **And** I can drill down into specific rejection categories

**Scenario 4: Compare across dimensions**
- **Given** I manage multiple jobs or departments
- **When** I compare funnel metrics
- **Then** I can compare conversion rates across jobs
- **And** I can compare across departments, locations, or recruiters
- **And** I can identify best practices from high-performing funnels
- **And** I can export comparison reports

**Scenario 5: Track improvements over time**
- **Given** I have implemented process changes
- **When** I view historical funnel trends
- **Then** I see conversion rate trends over time
- **And** I can correlate changes with process improvements
- **And** I can measure the impact of interventions
- **And** I can set conversion rate targets and track progress

### **Dependencies**
- **Technical:** Analytics engine, data visualization library, statistical analysis
- **Data:** Pipeline stage history, rejection reasons, time-series data
- **Integration:** None for MVP
- **Prerequisite Stories:** US-011 (pipeline management), US-015 (dashboard)

### **Notes**
- **Assumptions:** Rejection reasons are consistently recorded by recruiters
- **Open Questions:** What's the benchmark for "good" conversion rates by stage? Should there be industry comparisons?
- **Technical Considerations:** API endpoints: GET /api/analytics/funnel, GET /api/analytics/bottlenecks, GET /api/analytics/drop-off-reasons

---

### **User Story US-026**
**ID:** `US-026`  
**Epic:** E-007 (Analytics & Predictive Insights)  
**Feature:** F-030 (Source ROI Tracking)  
**Priority:** P1  
**Persona:** Recruiter

**As a** Recruiter,  
**I want to** track the ROI of different sourcing channels,  
**So that** I can optimize sourcing spend and save 25% of recruitment budget.

### **Description**
Understanding which sourcing channels deliver the best candidates at the lowest cost is essential for budget optimization. The system should track applications by source, hire rates, cost per hire, and provide source comparison analytics.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Track applications by source**
- **Given** candidates apply from various sources
- **When** I view source analytics
- **Then** I see application counts by source (LinkedIn, Indeed, Referral, Careers Page, etc.)
- **And** I see source distribution as a pie chart
- **And** I see trends over time (line chart)
- **And** I can filter by job, department, date range

**Scenario 2: Calculate hire rate by source**
- **Given** I want to measure source quality
- **When** I view source effectiveness metrics
- **Then** I see hire rate (hires/applications) for each source
- **And** I see average time-to-hire by source
- **And** I see average quality score (AI match score) by source
- **And** I can rank sources by effectiveness

**Scenario 3: Track cost per hire by source**
- **Given** I have configured costs for paid sources
- **When** I view cost analytics
- **Then** I see total cost per source (job board fees, agency fees, etc.)
- **And** I see cost per application by source
- **And** I see cost per hire by source
- **And** I can calculate ROI (value of hire vs. cost)

**Scenario 4: Compare sources side-by-side**
- **Given** I want to optimize sourcing strategy
- **When** I access source comparison matrix
- **Then** I see all sources compared across metrics (volume, quality, cost, hire rate)
- **And** I can sort by any metric
- **And** I see recommended actions (increase spend on high-ROI sources, reduce low-ROI sources)
- **And** I can export the comparison report

**Scenario 5: Set source budgets and track spend**
- **Given** I have a recruitment budget
- **When** I configure source budgets
- **Then** I can allocate budget by source
- **And** I can track actual spend vs. budget
- **And** I receive alerts when approaching budget limits
- **And** I can reallocate budget based on performance

### **Dependencies**
- **Technical:** Analytics engine, cost tracking system, ROI calculator
- **Data:** Application source data, hire outcomes, source costs
- **Integration:** Job board APIs for cost data
- **Prerequisite Stories:** US-003 (multi-channel publishing), US-015 (dashboard)

### **Notes**
- **Assumptions:** Source costs are manually entered or imported from job board APIs
- **Open Questions:** How to attribute hires to multiple sources (e.g., candidate found on LinkedIn but applied via careers page)?
- **Technical Considerations:** API endpoints: GET /api/analytics/source-roi, POST /api/sources/{id}/cost, GET /api/sources/comparison

---

### **User Story US-027**
**ID:** `US-027`  
**Epic:** E-006 (Multi-Channel Communication)  
**Feature:** F-025 (AI-Powered Chatbot)  
**Priority:** P2  
**Persona:** Candidate

**As a** Candidate,  
**I want to** ask questions about my application using an AI chatbot,  
**So that** I can get instant answers 24/7 without waiting for recruiter response.

### **Description**
Candidates have common questions about application status, job details, and interview process. The system should provide an AI-powered chatbot on the careers portal that answers FAQs, provides application status, and escalates complex queries to recruiters.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Access chatbot on careers portal**
- **Given** I am a candidate visiting the careers portal
- **When** I see the chatbot widget in the bottom right corner
- **Then** I can click to open the chat interface
- **And** I see a welcome message with suggested questions
- **And** I can type my question in natural language
- **And** the chatbot is available 24/7

**Scenario 2: Answer common questions**
- **Given** I have a question about the application process
- **When** I ask "How long does the hiring process take?"
- **Then** the chatbot provides a relevant answer based on the knowledge base
- **And** the answer is specific to the job I applied for (if applicable)
- **And** the chatbot offers related questions I might have
- **And** the chatbot maintains conversation context

**Scenario 3: Provide application status**
- **Given** I want to check my application status
- **When** I ask "What's the status of my application?"
- **Then** the chatbot asks for my email to identify me
- **And** it retrieves my application status from the system
- **And** it tells me the current stage and expected next steps
- **And** it provides an estimated timeline

**Scenario 4: Escalate to recruiter**
- **Given** I have a complex question the chatbot can't answer
- **When** the chatbot detects it cannot help
- **Then** it offers to connect me with a recruiter
- **And** it collects my question and contact information
- **And** it creates a ticket for the recruiter
- **And** it tells me when to expect a response

**Scenario 5: Multi-language support**
- **Given** I am a candidate who speaks Spanish
- **When** I type a question in Spanish
- **Then** the chatbot detects the language automatically
- **And** it responds in Spanish
- **And** it maintains the conversation in Spanish
- **And** it supports English, Spanish, Portuguese, French, German

### **Dependencies**
- **Technical:** NLP chatbot engine, intent classification, knowledge base
- **Data:** FAQ knowledge base, application status data, job information
- **Integration:** None for MVP
- **Prerequisite Stories:** US-014 (candidate communication)

### **Notes**
- **Assumptions:** Chatbot has pre-trained knowledge base covering common recruitment questions
- **Open Questions:** Should chatbot conversations be logged for recruiter review? How to measure chatbot effectiveness?
- **Technical Considerations:** API endpoints: POST /api/chatbot/message, GET /api/chatbot/conversation/{id}, POST /api/chatbot/escalate

---

### **User Story US-028**
**ID:** `US-028`  
**Epic:** E-007 (Analytics & Predictive Insights)  
**Feature:** F-031 (Predictive Analytics)  
**Priority:** P2  
**Persona:** Hiring Manager

**As a** Hiring Manager,  
**I want to** view AI-powered predictions for time-to-close and candidate drop-off,  
**So that** I can proactively intervene and improve hiring outcomes.

### **Description**
Predictive analytics enable proactive hiring management by forecasting outcomes before they occur. The system should use historical data and ML models to predict time-to-close, candidate drop-off probability, and optimal hiring timelines with confidence scores.

### **Acceptance Criteria (Gherkin)**

**Scenario 1: Predict time-to-close for job**
- **Given** I have an open job requisition
- **When** I view predictive analytics
- **Then** I see the predicted time-to-close in days
- **And** I see a confidence interval (e.g., 30-45 days with 80% confidence)
- **And** I see factors influencing the prediction (role difficulty, market conditions, historical data)
- **And** I can adjust job parameters to see impact on prediction

**Scenario 2: Identify at-risk candidates**
- **Given** I have candidates in the pipeline
- **When** the AI analyzes drop-off probability
- **Then** it flags candidates with high drop-off risk (>50% probability)
- **And** it explains why they're at risk (long time in stage, low engagement, competing offers)
- **And** it suggests interventions (faster scheduling, personalized outreach, expedited process)
- **And** I can take action directly from the alert

**Scenario 3: Optimize hiring timeline**
- **Given** I want to plan the hiring process
- **When** I view timeline optimization
- **Then** the AI suggests optimal timeline for each stage
- **And** it balances speed vs. quality based on historical data
- **And** it identifies stages where we can accelerate without compromising quality
- **And** it shows expected impact on time-to-hire

**Scenario 4: View prediction accuracy**
- **Given** the system has made predictions over time
- **When** I view prediction performance metrics
- **Then** I see actual vs. predicted outcomes
- **And** I see prediction accuracy percentage
- **And** I see how accuracy improves over time with more data
- **And** I can provide feedback to improve predictions

**Scenario 5: Scenario planning**
- **Given** I want to understand different hiring scenarios
- **When** I use the scenario planner
- **Then** I can adjust variables (number of interviewers, stage durations, sourcing channels)
- **And** the system predicts outcomes for each scenario
- **And** I can compare scenarios side-by-side
- **And** I can select the optimal scenario for implementation

### **Dependencies**
- **Technical:** ML prediction models, historical data analysis, scenario simulation engine
- **Data:** Historical hiring data (time-to-hire, drop-off rates, outcomes), current pipeline data
- **Integration:** None for MVP
- **Prerequisite Stories:** US-015 (dashboard), US-025 (funnel analysis)

### **Notes**
- **Assumptions:** System has sufficient historical data (6+ months) for accurate predictions
- **Open Questions:** What's the minimum data required for predictions? How often should models be retrained?
- **Technical Considerations:** API endpoints: GET /api/analytics/predictions/time-to-close, GET /api/analytics/predictions/drop-off, POST /api/analytics/scenario-planning

---

## Appendix

### INVEST Compliance Summary

All user stories in this document follow the INVEST framework:

- **Independent**: Each story can be developed independently (dependencies are noted but don't block parallel development)
- **Negotiable**: Details can be refined with stakeholders during sprint planning
- **Valuable**: Each story delivers clear value to users or business (value statements included)
- **Estimable**: Stories are specific enough for developers to estimate effort (1-2 week sprints)
- **Small**: Stories are appropriately sized for single sprint completion
- **Testable**: Clear acceptance criteria enable verification (Gherkin format with 3-5 scenarios)

### Traceability Matrix

All user stories map to PRD requirements and epics/features from `02-epics-and-features.md`:

| Story ID | PRD Requirement | Epic | Feature |
|----------|----------------|------|---------|
| US-001 | JM-001 | E-001 | F-001 |
| US-002 | JM-002 | E-001 | F-002 |
| US-003 | JM-003 | E-001 | F-003 |
| US-004 | SA-001 | E-002 | F-005 |
| US-005 | SA-002 | E-002 | F-006 |
| US-006 | IS-001 | E-003 | F-009 |
| US-007 | IS-002 | E-003 | F-010 |
| US-008 | CE-001 | E-004 | F-013 |
| US-009 | CE-002 | E-004 | F-014 |
| US-010 | CE-005 | E-004 | F-017 |
| US-011 | PM-001 | E-005 | F-018 |
| US-012 | PM-002 | E-005 | F-019 |
| US-013 | CM-001 | E-006 | F-023 |
| US-014 | CM-002 | E-006 | F-024 |
| US-015 | AI-001 | E-007 | F-028 |
| US-016 | IN-001 | E-008 | - |
| US-017 | JM-004 | E-001 | F-004 |
| US-018 | SA-004 | E-002 | F-008 |
| US-019 | IS-004 | E-003 | F-012 |
| US-020 | IS-003 | E-003 | F-011 |
| US-021 | CE-003 | E-004 | F-015 |
| US-022 | PM-004 | E-005 | F-021 |
| US-023 | PM-005 | E-005 | F-022 |
| US-024 | CM-004 | E-006 | F-026 |
| US-025 | AI-002 | E-007 | F-029 |
| US-026 | AI-003 | E-007 | F-030 |
| US-027 | CM-003 | E-006 | F-025 |
| US-028 | AI-005 | E-007 | F-031 |

### Next Steps

This user stories document serves as input for:
1. **Step 4:** Product Backlog generation with effort estimates and prioritization
2. **Step 5:** Engineering Work Tickets with technical implementation details

---

**Document Status:** Complete  
**Total User Stories:** 28  
**Coverage:** All 8 epics, all 4 personas, P0/P1/P2 priorities  
**Format:** INVEST-compliant with Gherkin acceptance criteria
