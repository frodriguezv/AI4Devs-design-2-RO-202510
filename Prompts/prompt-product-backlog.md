# Claude Sonnet 4.5 Prompt — LTI ATS Product Backlog

## Persona
Act as an expert **Agile Product Owner**, skilled in backlog creation, refinement, prioritization, and slicing complex AI-powered features into actionable items for engineering teams.

## Context
You are given the comprehensive Product Requirements Document for **LTI ATS** - a next-generation Applicant Tracking System powered by artificial intelligence.

**System Overview:**
LTI ATS is designed to transform recruitment through:
- **AI-powered automation**: CV parsing, candidate matching, cultural fit analysis, red flag detection
- **Real-time collaboration**: Live commenting, synchronized scorecards, team debriefs
- **Intelligent workflows**: Automated email triggers, smart scheduling, proactive alerts
- **Predictive analytics**: Time-to-hire predictions, funnel analysis, source ROI tracking
- **Seamless integrations**: HRIS, calendars, job boards, assessment platforms, communication tools

**Target Outcome:** 40% reduction in time-to-hire, 60% reduction in recruiter administrative burden

**Priority Framework (from PRD):**
- **P0 (Must Have)**: Critical for MVP and v1.0 launch - core functionality without which the product cannot operate
- **P1 (Should Have)**: Important for competitive differentiation and user satisfaction - needed for v1.0 or early v1.x
- **P2 (Nice to Have)**: Enhancement features for future versions - nice-to-haves that can be deferred

**Non-Functional Requirements (NFRs) from PRD Section 7:**
1. **Performance**: API response <200ms (p95), page load <2s, search <500ms, support 10K concurrent users
2. **Scalability**: Horizontal scaling, multi-region deployment, 10M candidate profiles, 1M active applications
3. **Availability**: 99.9% uptime SLA, <1hr RPO, <4hr RTO, zero-downtime deployments
4. **Security**: MFA, RBAC, OAuth 2.0, AES-256 encryption at rest, TLS 1.3 in transit, OWASP compliance
5. **Usability**: WCAG 2.1 AA compliance, mobile-responsive, support latest 2 browser versions
6. **Compliance**: GDPR, CCPA, EEO/EEOC, SOC 2 Type II, right to erasure, data portability

**Success Metrics (from PRD Section 8):**
- Product: $500K MRR by Year 1, 200 customers, <5% churn, NPS >50
- Usage: 70% DAU/seats, <30 days time-to-value, >60% AI feature adoption
- Technical: 99.9% uptime, <200ms API response (p95), >80% code coverage
- Customer Success: 95% onboarding completion in 30 days, 90% tickets resolved in 24hr

You have (or will generate) using previous prompts:
- Product Roadmap (strategic phases and timelines)
- Epics & Features (hierarchical functional breakdown)
- User Stories (INVEST-compliant stories with Gherkin criteria)

## Task
Transform the LTI ATS PRD into a **complete, prioritized Product Backlog** organized and ready for sprint planning and implementation.

## Backlog Requirements
Your product backlog MUST include:

### 1. Prioritized Backlog Items
- List ALL backlog items starting from highest business value
- Use clear prioritization criteria:
  - **Business value**: Impact on time-to-hire, user experience, competitive differentiation
  - **Risk**: Technical complexity, dependencies, unknowns
  - **Dependencies**: Prerequisites, external systems, data requirements
  - **Effort**: Estimated complexity and time
- Apply MoSCoW method aligned with P0/P1/P2 framework:
  - **Must Have (P0)**: MVP/v1.0 critical path
  - **Should Have (P1)**: Important for v1.0 or early v1.x
  - **Could Have (P2)**: Future enhancements
  - **Won't Have (this release)**: Out of scope items to explicitly defer

### 2. Backlog Item Organization
Group and categorize items by multiple dimensions:

**By Epic & Feature:**
- Epic Name (from prompt-epics output)
- Feature Name
- Related User Story IDs

**By Type:**
- Epic (strategic initiative)
- Feature (user-facing capability)
- User Story (specific user need)
- Spike (research/investigation task)
- Technical Task (infrastructure, architecture, tooling)
- Bug/Defect (known issues)
- NFR (non-functional requirement)

**By Component/Domain:**
- Job Management
- Sourcing & Attraction
- Intelligent Screening
- Collaborative Evaluation
- Pipeline Management
- Communication
- Analytics & Insights
- Integrations
- Platform & Infrastructure

### 3. Backlog Item Details
Each backlog item must include:

- **ID**: Unique identifier (e.g., BI-001)
- **Title**: Clear, concise description
- **Type**: Epic / Feature / Story / Spike / Technical Task / NFR
- **Priority**: P0 / P1 / P2
- **MoSCoW**: Must / Should / Could / Won't
- **Effort Estimate**: Story points (Fibonacci: 1, 2, 3, 5, 8, 13) or T-shirt sizing (XS, S, M, L, XL)
- **Business Value**: High / Medium / Low
- **Description**: 1-2 sentence summary
- **Acceptance Criteria**: High-level success criteria
- **Dependencies**: Prerequisite items, external systems, data needs
- **Risk Level**: High / Medium / Low
- **Target Release**: MVP / v1.0 / v1.1 / v2.0 / Future

### 4. Non-Functional Requirements (NFRs)
Create dedicated backlog items for each NFR category:

**Performance NFRs:**
- API response time optimization
- Page load performance
- Search query optimization
- Concurrent user handling

**Security NFRs:**
- Authentication & authorization (MFA, RBAC, OAuth 2.0)
- Data encryption (at rest and in transit)
- Security testing (penetration testing, vulnerability scanning)
- Audit logging

**Scalability NFRs:**
- Horizontal scaling architecture
- Database partitioning and sharding
- Caching strategy
- Multi-region support

**Compliance NFRs:**
- GDPR compliance (consent management, right to erasure, data portability)
- CCPA compliance
- EEO/EEOC reporting
- SOC 2 Type II certification prep

**Observability NFRs:**
- Logging infrastructure (ELK stack)
- Monitoring and alerting (Prometheus, Grafana)
- Distributed tracing (Jaeger)
- APM (Application Performance Monitoring)

### 5. Technical Spikes & Research Items
Include investigation tasks for:
- AI/ML model selection and training
- Third-party integration research
- Architecture proof-of-concepts
- Performance benchmarking
- Technology evaluation

### 6. Backlog Health Metrics
Provide metrics on backlog composition:
- Total item count by type
- Priority distribution (P0/P1/P2)
- Effort distribution
- Readiness assessment (% meeting DoR)

## Additional Required Sections

### A. Backlog Risks & Unknowns
Document risks that could impact delivery:
- **Technical Risks**: AI model accuracy, integration complexity, scalability challenges
- **Dependency Risks**: External API availability, vendor delays, data migration issues
- **Resource Risks**: Team skills gaps, hiring needs, training requirements
- **Scope Risks**: Feature creep, changing requirements, unclear specifications

### B. Definition of Ready (DoR) Checklist
Provide a checklist for backlog items to be considered "ready" for sprint planning:

- [ ] User story/requirement is clearly defined
- [ ] Acceptance criteria are specific and testable
- [ ] Dependencies are identified and documented
- [ ] Effort estimate is provided
- [ ] Business value is articulated
- [ ] Technical approach is understood
- [ ] Design/mockups are available (if UI work)
- [ ] API contracts are defined (if integration work)
- [ ] Security and compliance requirements are captured
- [ ] Performance requirements are specified
- [ ] Team has capacity to commit to the item

### C. Definition of Done (DoD)
Provide standard DoD criteria for all backlog items:

- [ ] Code complete and peer reviewed
- [ ] Unit tests written (>80% coverage)
- [ ] Integration tests written (where applicable)
- [ ] API documentation updated
- [ ] User-facing documentation updated
- [ ] All acceptance criteria met
- [ ] Security review completed
- [ ] Performance tested (meets NFRs)
- [ ] QA validated in staging environment
- [ ] Product Owner acceptance
- [ ] Merged to main branch
- [ ] Deployed to production (or ready for deployment)

## Output Format
Return everything in clean, structured Markdown:

```md
# Product Backlog — LTI ATS

## 1. Executive Summary
- Total backlog items: <count>
- Priority distribution: <P0: X%, P1: Y%, P2: Z%>
- Estimated total effort: <story points or weeks>
- Current backlog health: <assessment>

## 2. Prioritized Backlog (Master View)
[Table with all items sorted by priority]

| ID | Title | Type | Priority | MoSCoW | Effort | Value | Epic/Feature | Dependencies | Release |
|----|-------|------|----------|--------|--------|-------|--------------|--------------|---------|
| BI-001 | ... | Story | P0 | Must | 5 | High | Job Management | BI-005 | MVP |

## 3. Backlog by Epic & Feature
### Epic 1: <Epic Name>
#### Feature 1.1: <Feature Name>
- **BI-XXX**: <Story title> (P0, 5 pts)
- **BI-XXX**: <Story title> (P1, 3 pts)

## 4. Non-Functional Requirements Backlog
### Performance
- **BI-XXX**: API response time <200ms
- **BI-XXX**: Page load optimization

### Security
- **BI-XXX**: Implement MFA
- **BI-XXX**: RBAC system

## 5. Technical Spikes & Research
- **BI-XXX**: AI matching algorithm evaluation
- **BI-XXX**: HRIS integration POC

## 6. Backlog Risks & Mitigation
| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| ... | ... | ... | ... |

## 7. Definition of Ready (DoR)
<Checklist as specified above>

## 8. Definition of Done (DoD)
<Checklist as specified above>

## 9. Backlog Health Metrics
- Items meeting DoR: <X%>
- Average item size: <Y story points>
- Velocity trend: <if historical data available>
```

## Final Instruction
Begin by:
1. Reading the complete LTI ATS PRD (`lti_ats_prd.md`)
2. Summarizing the product vision, priority framework, and key success metrics in 3–5 sentences to confirm understanding
3. Generating the comprehensive product backlog following the structure above, ensuring complete coverage of functional requirements, NFRs, and technical needs
