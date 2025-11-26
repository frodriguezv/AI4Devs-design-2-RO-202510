# Claude Sonnet 4.5 Prompt — LTI ATS Product Roadmap

## Persona
Act as a **Senior Product Manager** with expertise in SaaS platforms, AI-powered ATS systems, and long-term strategic product planning. You excel at turning comprehensive PRDs into strategic, phased roadmaps aligned with business value, technical feasibility, and market differentiation.

## Context
You are given the Product Requirements Document for **LTI ATS** - a next-generation Applicant Tracking System that transforms reactive recruitment into an intelligent, collaborative, and data-driven process.

**LTI ATS Key Differentiators:**
1. **Contextual AI Engine**: Advanced semantic analysis for candidate-job matching beyond simple keyword matching
2. **Native Collaboration**: Built-in real-time collaboration with live commenting, synchronized scorecards, and team debriefs
3. **Adaptive Automation**: AI that learns from team decisions to continuously improve recommendations
4. **Predictive Analytics**: Time-to-hire predictions, funnel analysis, bottleneck detection, and early warning systems
5. **Premium Candidate Experience**: Dedicated candidate portal with real-time updates and transparent communication

**Core Feature Domains (8 categories):**
- Job Management (requisitions, approvals, multi-channel publishing, market analysis)
- Sourcing & Attraction (search, platform integration, talent pools, Chrome extension)
- Intelligent Screening (CV parsing, AI matching, cultural fit analysis, red flag detection)
- Collaborative Evaluation (scorecards, real-time commenting, video interviews, consolidated decisions)
- Pipeline Management (Kanban board, automated workflows, intelligent assignment, proactive alerts)
- Communication (email templates, automation, AI chatbot, smart scheduling, multi-channel)
- Analytics & Insights (dashboards, funnel analysis, source ROI, diversity metrics, predictive analytics)
- Integrations (HRIS, calendars, communication tools, background checks, assessments, RESTful API)

The PRD includes detailed requirements, use cases, data model, technical architecture, and a future roadmap (sections 1-11).

## Task
Using the attached LTI ATS PRD (`lti_ats_prd.md`), create a **clear, structured, implementation-ready Product Roadmap** that aligns with the product vision and technical constraints.

## Roadmap Requirements

### 1. Phases
Break down the roadmap into **logical, sequential phases**, considering:
- MVP/Beta requirements
- Core v1.0 features (P0 priorities)
- Enhanced capabilities (P1 priorities)
- Advanced AI and automation features
- Future innovations (P2 priorities)

Suggested phase structure (adapt based on PRD analysis):
- Phase 1 — MVP / Beta Launch
- Phase 2 — Core Platform v1.0
- Phase 3 — AI & Automation Enhancement
- Phase 4 — Advanced Collaboration & Integrations
- Phase 5 — Predictive Intelligence & Scaling

### 2. For EACH phase include:
- **Goals** (what this phase achieves)
- **Business Value** (why this matters strategically - tie to the 40% time-to-hire reduction goal)
- **Key Deliverables** (features, modules, integrations from the 8 feature domains)
- **Technical Components** (services, APIs, data model changes, infrastructure)
- **Cross-functional Considerations**:
  - **Security**: Authentication, authorization, data protection, compliance
  - **Compliance**: GDPR, CCPA, EEO/EEOC, SOC 2 Type II
  - **Performance**: Response times, throughput, scalability requirements (from NFR section)
  - **Observability**: Logging, monitoring, metrics, distributed tracing
  - **Scalability**: Horizontal scaling, multi-region support, data volume handling

### 3. Include:
- **Timeline Estimates** (effort ranges in weeks/months, not fixed dates)
- **Risk & Mitigation Section** (technical risks, market risks, adoption risks)
- **Dependencies Map** (prerequisite features, external integrations, data requirements)
- **Success Metrics** (aligned with PRD Section 8: product, usage, technical, and customer success metrics)

### 4. Alignment with Future Vision
Reference the future roadmap from PRD Section 11 (Versions 1.1, 1.2, 2.0) and ensure your phased roadmap creates a clear path toward those capabilities.

## Output Format
Return everything in **clean, structured Markdown** with these sections:

1. **Executive Summary** (2-3 paragraphs on roadmap strategy)
2. **Roadmap Overview** (visual timeline, phase names, duration estimates)
3. **Phase-by-Phase Breakdown** (detailed breakdown for each phase)
4. **Cross-Cutting Concerns** (security, compliance, performance, observability that span all phases)
5. **Timeline Estimates** (consolidated view of effort and sequencing)
6. **Risks & Mitigation** (categorized by type: technical, market, adoption, regulatory)
7. **Dependencies Map** (visual or hierarchical view of dependencies)
8. **Success Criteria** (how to measure successful phase completion)

## Final Instruction
Start by reading the LTI ATS PRD and summarizing the product vision, key differentiators, and strategic objectives in 3–5 sentences to confirm your understanding. Then generate the comprehensive product roadmap following the structure above.
