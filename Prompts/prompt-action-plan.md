# Claude Sonnet 4.5 Prompt — LTI ATS Documentation Action Plan

## Purpose
This prompt instructs Claude Sonnet 4.5 **how to execute all LTI ATS documentation tasks in the correct order**, ensuring high‑quality outputs without confusion or overlap.

**About LTI ATS**: LTI is a next-generation Applicant Tracking System that transforms reactive recruitment into an intelligent, collaborative, and data-driven process. By integrating AI at every stage of the hiring lifecycle, LTI ATS enables HR teams to reduce time-to-hire by 40% while focusing on strategic decisions.

Use this action plan when you want Claude Sonnet 4.5 to generate:
- Product Roadmap  
- Epics & Features  
- User Stories  
- Product Backlog  
- Engineering Work Tickets  

And execute them **in the optimal sequence** based on the LTI ATS PRD (`lti_ats_prd.md`).

---

# Action Plan — Execute Prompts in This Order

## **STEP 1 — Generate the Product Roadmap**
**Prompt to use:** `prompt-roadmap.md`
**Document to generate:** `01-product-roadmap.md`

Claude must begin by producing a full strategic roadmap for the LTI ATS system:
- Phases (MVP, Core v1, AI Automation, Scaling)
- Deliverables and key features
- Dependencies across the 8 major feature domains
- Timeline ranges  
- Risks and mitigation strategies
- Cross-cutting concerns (security, compliance, performance, scalability)

This becomes the foundation for every step afterward.

---

## **STEP 2 — Generate Epics & Features**
**Prompt to use:** `prompt-epics.md`
**Document to generate:** `02-epics-and-features.md`
**Document to use:** `01-product-roadmap.md`

Claude must break the LTI ATS PRD into structured components:
- Epics (covering Job Management, Sourcing, Screening, Evaluation, Pipeline, Communication, Analytics, Integrations)
- Features within each epic
- Sub-features and functional components
- Business value and strategic alignment
- Priority (P0/P1/P2 alignment)
- Dependencies (technical, data, and workflow)
- Open questions and gaps

This creates the structural hierarchy for the entire product.

---

## **STEP 3 — Generate User Stories**
**Prompt to use:** `prompt-user-stories.md`
**Document to generate:** `03-user-stories.md`
**Document to use:** `02-epics-and-features.md`

Claude must now convert epics & features into high-quality, INVEST-compliant user stories with Gherkin acceptance criteria.

Each story must follow the standard template for the 4 primary user personas (Recruiter, Hiring Manager, Interviewer, Candidate):
- As a… [persona]
- I want to… [capability]
- So that… [value]
- Description  
- Acceptance criteria (Gherkin format with minimum 3 scenarios)
- Dependencies (technical, data, and integration)
- Notes and assumptions

---

## **STEP 4 — Generate the Product Backlog**
**Prompt to use:** `prompt-product-backlog.md`
**Document to generate:** `04-product-backlog.md`
**Document to use:** `03-user-stories.md`

Using the epics and stories from previous steps:
- Prioritize backlog items by business value
- Add effort estimates (story points or T-shirt sizing)
- Organize into a master backlog table  
- Include Non-Functional Requirements (Performance, Security, Scalability, Compliance)
- Add risks, unknowns, and technical spikes
- Provide a Definition of Ready checklist  

This becomes the product's master execution plan.

---

## **STEP 5 — Generate Engineering Work Tickets**
**Prompt to use:** `prompt-work-tickets.md`
**Document to generate:** `05-work-tickets.md`
**Document to use:** `04-product-backlog.md`

Claude must output detailed, implementation-ready engineering tickets:
- Backend tickets (Node.js/Express, Python/FastAPI services)
- Frontend tickets (React 18+, TypeScript, Material-UI)
- API tickets (RESTful, OAuth 2.0, WebSocket)
- Database tickets (PostgreSQL schema, Redis caching, ElasticSearch indexing)
- DevOps tickets (Kubernetes, Docker, CI/CD, monitoring)
- QA automation tickets (unit, integration, E2E tests)
- Spikes and technical research tasks
- Technical design and architecture tickets

Each ticket must include:
- Ticket ID (format: `LTI-XXX`)
- Title and type
- Priority (High/Medium/Low)
- Effort estimate  
- Description with business context
- Technical requirements (API endpoints, DB changes, services, integrations)
- Acceptance criteria (Gherkin format)
- Dependencies (other tickets, APIs, data, external systems)
- Definition of Done (code, tests, documentation, QA validation)
- Risks and assumptions

This becomes your **implementation layer**.

---

# Final Instruction for Claude Sonnet 4.5

**Follow the steps above in sequential order.**  

Do not skip ahead.  
Do not merge steps.  
Do not generate later artifacts until previous outputs are complete and validated.

Each step should begin by:
1. Reading and analyzing the LTI ATS PRD (`lti_ats_prd.md`)
2. Summarizing the relevant PRD sections in 3–5 sentences to confirm understanding
3. Executing the assigned prompt with full context
4. Waiting for the user to review and approve before continuing to the next step

This ensures high clarity, accuracy, and quality across the entire LTI ATS documentation pipeline.
