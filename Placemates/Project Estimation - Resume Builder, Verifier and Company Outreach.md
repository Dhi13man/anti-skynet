# Project Estimation - Resume Builder, Verifier and Company Outreach

## Assumptions

1. Founders handle product management & design at no cost
2. Only Junior Software Development Engineers (SDEs) are hired
3. 8-hour work days, 5-day work weeks
4. Basic cloud infrastructure available
5. Third-party AI APIs (voice processing, NLP) available with 2-week integration buffer
6. 20% buffer added for integration risks
7. Parallel task execution where no dependencies exist

## Team Compositions

| Scenario         | Team Size     | Experience Level     | Coordination Needs         |
| ---------------- | ------------- | -------------------- | -------------------------- |
| Under-resourced  | 3 SDEs        | 0-1 year experience  | Daily standups + mentoring |
| Well-structured  | 5 SDEs        | 1-2 years experience | Bi-weekly checkins         |
| Over-provisioned | 4 Senior SDEs | 2-3 years experience | Weekly syncs               |

## Work Breakdown Structure (WBS)

### Feature 1: AI-Powered Student Profiling

| Task ID | Task Description                      | Standard Duration | Dependencies |
| ------- | ------------------------------------- | ----------------- | ------------ |
| F1.1    | Profile Data Backend (NoSQL DB + API) | 14 days           | -            |
| F1.2    | Voice Interface Development           | 18 days           | F1.1         |
| F1.3    | Dynamic Flowchart Generator           | 12 days           | F1.1         |
| F1.4    | Document Parsing Integration          | 10 days           | F1.1         |

### Feature 2: AI-Driven Goal Setting

| Task ID | Task Description                  | Standard Duration | Dependencies |
| ------- | --------------------------------- | ----------------- | ------------ |
| F2.1    | Career Path Recommendation Engine | 21 days           | F1.1         |
| F2.2    | Roadmap Generator UI              | 10 days           | F2.1         |
| F2.3    | Domain Comparison System          | 15 days           | F2.1         |

### Feature 3: AI-Powered CV Maker

| Task ID | Task Description       | Standard Duration | Dependencies |     |
| ------- | ---------------------- | ----------------- | ------------ | --- |
| F3.1    | Resume Template Engine | 12 days           | F1.1         |     |
| F3.2    | Gap Analysis Module    | 18 days           | F1.3, F2.1   |     |
| F3.3    | CV Verification System | 14 days           | F3.1         |     |

### Feature 4: Placement Tracking

| Task ID | Task Description      | Standard Duration | Dependencies |
| ------- | --------------------- | ----------------- | ------------ |
| F4.1    | Priority List Manager | 10 days           | F2.1         |
| F4.2    | Live Status Tracker   | 12 days           | F3.3         |
| F4.3    | Interview Prep System | 16 days           | F2.3         |

### Admin Portal

| Task ID | Task Description       | Standard Duration | Dependencies |
| ------- | ---------------------- | ----------------- | ------------ |
| A1.1    | Company CRM Backend    | 18 days           | -            |
| A1.2    | Automated Email System | 14 days           | A1.1         |
| A1.3    | Placement Analytics    | 12 days           | F4.2         |

```mermaid
gantt
    title Project Timeline - Critical Path Analysis
    dateFormat YYYY-MM-DD
    axisFormat %b %d
    
    section Student Profiling
    F1.1 Profile Data Backend      :a1, 2023-10-01, 14d
    F1.2 Voice Interface           :a2, after a1, 18d
    F1.3 Flowchart Generator       :a3, after a1, 12d
    F1.4 Document Parsing          :a4, after a1, 10d
    
    section Goal Setting
    F2.1 Recommendation Engine     :b1, after a1, 21d
    F2.2 Roadmap Generator UI      :b2, after b1, 10d
    F2.3 Domain Comparison         :b3, after b1, 15d
    
    section CV Maker
    F3.1 Resume Template Engine    :c1, after a1, 12d
    F3.2 Gap Analysis Module       :c2, after a3 and b1, 18d
    F3.3 CV Verification System    :c3, after c1, 14d
    
    section Placement Tracking
    F4.1 Priority List Manager     :d1, after b1, 10d
    F4.2 Live Status Tracker       :d2, after c3, 12d
    F4.3 Interview Prep System     :d3, after b3, 16d
    
    section Admin Portal
    A1.1 Company CRM Backend       :e1, 2023-10-01, 18d
    A1.2 Automated Email System    :e2, after e1, 14d
    A1.3 Placement Analytics       :e3, after d2, 12d
    
    section Milestones
    Profiling MVP                  :milestone, 2023-11-11, 0d
    Goal Setting Prototype         :milestone, 2023-12-06, 0d
    End-to-End Integration         :milestone, 2024-01-09, 0d
    Final Security Audit           :milestone, 2024-01-23, 0d
```

## Resource Allocation

```mermaid
pie
    title "Resource Allocation by Feature Area"
    "Student Profiling" : 25
    "Goal Setting" : 20
    "CV Maker" : 20
    "Placement Tracking" : 15
    "Admin Portal" : 15
    "Integration & Testing" : 5
```

The resource allocation shows the distribution of development effort across the major feature areas of the project. Student profiling receives the highest allocation as it forms the foundation of the platform.

## Feature Dependencies Flowchart

```mermaid
flowchart TD
    F1[Student Profiling] --> F2[Goal Setting]
    F1 --> F3[CV Maker]
    F2 --> F3
    F2 --> F4[Placement Tracking]
    F3 --> F4
    F4 --> A1[Admin Portal Analytics]
    
    subgraph "Core Features"
    F1
    F2
    F3
    F4
    end
    
    subgraph "Admin Features"
    A1
    end
```

## Risk Assessment Matrix

```mermaid
quadrantChart
    title Risk Assessment Matrix
    x-axis Low Impact --> High Impact
    y-axis Low Probability --> High Probability
    quadrant-1 "Monitor"
    quadrant-2 "High Priority"
    quadrant-3 "Low Priority"
    quadrant-4 "Contingency Plan"
    "API Integration Issues": [0.7, 0.6]
    "Team Turnover": [0.8, 0.3]
    "Scope Creep": [0.9, 0.7]
    "Technology Changes": [0.5, 0.2]
    "Performance Issues": [0.6, 0.5]
    "Security Vulnerabilities": [0.7, 0.4]
```

## Timeline Estimation

### Effort Table

| Task ID | Effort (Days) | Parallelizable? |
|---------|---------------|-----------------|
| F1.1    | 14            | No              |
| F1.2    | 18            | No              |
| F1.3    | 12            | Yes             |
| F2.1    | 21            | No              |
| F2.3    | 15            | No              |
| F3.2    | 18            | No              |
| F4.3    | 16            | Yes             |
| A1.2    | 14            | Yes             |

### Duration Scenarios

1. **Under-resourced Team (3 SDEs)**
   - Multiplier: 1.6x (learning curve)
   - Critical Path: (14+18+21+15+18+16) \* 1.6 = 163 days
   - Buffer: 32 days (20%)
   - **Total: 195 days**

2. **Well-structured Team (5 SDEs)**
   - Multiplier: 1x
   - Critical Path: 14+18+21+15+18+16 = 102 days
   - Buffer: 20 days
   - **Total: 122 days**

3. **Over-provisioned Team (8 SDEs)**
   - Multiplier: 0.8x (diminishing returns)
   - Critical Path: (102) \* 0.8 = 82 days
   - Buffer: 16 days
   - **Total: 98 days**

## Cost Estimation

- Junior SDE Rate: ₹700/day (8hrs)
- Buffer Costs calculated at 50% of base rate

| Scenario            | Direct Cost                     | Buffer Cost              | Total Cost               |
|---------------------|---------------------------------|--------------------------|--------------------------|
| Under-resourced     | 3 devs × 163d × ₹700 = ₹342,300 | ₹171,150                | ₹513,450                |
| Well-structured     | 5 devs × 102d × ₹700 = ₹357,000 | ₹178,500                | ₹535,500                |
| Over-provisioned    | 8 devs × 82d × ₹700 = ₹459,200  | ₹229,600                | ₹688,800                |

## Summary Table

| Scenario         | Duration | Total Cost | Risk Profile      |
| ---------------- | -------- | ---------- | ----------------- |
| Under-resourced  | 195 days | ₹513k      | High burnout risk |
| Well-structured  | 122 days | ₹535k      | Balanced delivery |
| Over-provisioned | 98 days  | ₹688k      | Fast but costly   |

## Technology Stack

```mermaid
graph TD
    subgraph "Frontend"
    F1[React.js] --- F2[Material UI]
    F2 --- F3[Chart.js]
    F1 --- F4[Redux]
    end
    
    subgraph "Backend"
    B1[Node.js] --- B2[Express]
    B2 --- B3[MongoDB]
    B1 --- B4[Python ML Services]
    end
    
    subgraph "AI Services"
    A1[NLP Processing API] --- A2[Voice Recognition]
    A2 --- A3[Document OCR]
    A1 --- A4[Recommendation Engine]
    end
    
    subgraph "DevOps"
    D1[AWS/Azure Cloud] --- D2[CI/CD Pipeline]
    D2 --- D3[Monitoring]
    end
    
    F1 --> B2
    B4 --> A1
    A4 --> B1
    B1 --> D1
    
    style F1 fill:#d0e8ff,stroke:#0366d6
    style F2 fill:#d0e8ff,stroke:#0366d6
    style F3 fill:#d0e8ff,stroke:#0366d6
    style F4 fill:#d0e8ff,stroke:#0366d6
    style B1 fill:#d8f9d6,stroke:#22863a
    style B2 fill:#d8f9d6,stroke:#22863a
    style B3 fill:#d8f9d6,stroke:#22863a
    style B4 fill:#d8f9d6,stroke:#22863a
    style A1 fill:#f9e8d2,stroke:#d15704
    style A2 fill:#f9e8d2,stroke:#d15704
    style A3 fill:#f9e8d2,stroke:#d15704
    style A4 fill:#f9e8d2,stroke:#d15704
    style D1 fill:#e6d1ff,stroke:#6f42c1
    style D2 fill:#e6d1ff,stroke:#6f42c1
    style D3 fill:#e6d1ff,stroke:#6f42c1
```

The proposed technology stack balances modern frameworks with stability and performance. The stack is designed to support AI integration while maintaining a responsive user experience. Third-party AI services will be leveraged where appropriate to accelerate development while custom ML models will be developed for core recommendation features.

## Contingency Plan

```mermaid
flowchart TD
    subgraph "Risk Categories"
        R1[Technical Risks]
        R2[Resource Risks]
        R3[Integration Risks]
    end
    
    subgraph "Mitigation Strategies"
        M1[Alternative Solutions]
        M2[Team Redundancy]
        M3[Vendor Backups]
    end
    
    R1 --> |AI Integration Issues| M1
    R1 --> |Performance Bottlenecks| M1
    R2 --> |Team Member Unavailability| M2
    R2 --> |Skill Gap| M2
    R3 --> |Third-Party API Changes| M3
    R3 --> |Data Format Inconsistencies| M3
    
    M1 --> C1[2-week buffer for alternative API providers]
    M1 --> C2[Fallback to simpler algorithms if needed]
    M2 --> C3[10% overlap in skills for cross-functional backups]
    M2 --> C4[Documentation to enable quick onboarding]
    M3 --> C5[Pre-vetted fallback vendors for critical components]
    M3 --> C6[Data normalization layer]
    
    style R1 fill:#ffdddd,stroke:#990000
    style R2 fill:#ffdddd,stroke:#990000
    style R3 fill:#ffdddd,stroke:#990000
    style M1 fill:#ddffdd,stroke:#009900
    style M2 fill:#ddffdd,stroke:#009900
    style M3 fill:#ddffdd,stroke:#009900
```

The contingency plan addresses key risk areas with specific mitigation strategies. Each strategy includes concrete actions that will be taken if the risk materializes. The plan is designed to minimize disruption to the project timeline while maintaining quality standards.

## Feedback Checkpoints

1. Profiling MVP (Week 6)
2. Goal Setting Prototype (Week 10)
3. End-to-End Integration (Week 15)
4. Final Security Audit (Week 17)

## Blockers and Mitigation Strategies

```mermaid
graph TD
    B1[Voice interface<br>accuracy <95%] -->|Mitigation| M1[Implement hybrid<br>text/voice input]
    B2[Resume parsing<br>inconsistencies] -->|Mitigation| M2[Manual validation<br>layer]
    B3[Company API<br>rate limits] -->|Mitigation| M3[Caching<br>implementation]
    B4[Data integration<br>challenges] -->|Mitigation| M4[Standard API<br>adapters]
    B5[Performance issues<br>under load] -->|Mitigation| M5[Implement load<br>balancing]
    
    style B1 fill:#f9d6d6,stroke:#a41e1e
    style B2 fill:#f9d6d6,stroke:#a41e1e
    style B3 fill:#f9d6d6,stroke:#a41e1e
    style B4 fill:#f9d6d6,stroke:#a41e1e
    style B5 fill:#f9d6d6,stroke:#a41e1e
    style M1 fill:#d6f9d6,stroke:#1ea41e
    style M2 fill:#d6f9d6,stroke:#1ea41e
    style M3 fill:#d6f9d6,stroke:#1ea41e
    style M4 fill:#d6f9d6,stroke:#1ea41e
    style M5 fill:#d6f9d6,stroke:#1ea41e
```

Each identified blocker has a corresponding mitigation strategy to ensure project continuity. The team will proactively monitor these potential issues and implement the mitigation strategies as needed.

## Implementation Roadmap

The implementation follows an agile approach with 2-week sprints. Each sprint will deliver incremental functionality and will be reviewed with stakeholders.

```mermaid
gantt
    title Implementation Roadmap
    dateFormat YYYY-MM-DD
    axisFormat %b %d
    
    section Phase 1: Foundation
    Sprint 1: Profile & DB Setup   :2023-10-01, 14d
    Sprint 2: Core API Development :2023-10-15, 14d
    
    section Phase 2: Core Features
    Sprint 3: Voice & Document Processing :2023-10-29, 14d
    Sprint 4: Recommendation Engine      :2023-11-12, 14d
    Sprint 5: CV Generation              :2023-11-26, 14d
    
    section Phase 3: Integration
    Sprint 6: Placement Tracking         :2023-12-10, 14d
    Sprint 7: Admin Portal               :2023-12-24, 14d
    
    section Phase 4: Finalization
    Sprint 8: Testing & Optimization     :2024-01-07, 14d
    Sprint 9: Deployment & Handover      :2024-01-21, 14d
```

## User Journey

```mermaid
sequenceDiagram
    actor Student
    participant Profile as Profile System
    participant Goals as Goal Setting
    participant CV as CV Maker
    participant Tracking as Placement Tracker
    participant Admin as Admin Portal
    
    Student->>Profile: Upload resume & academic details
    Profile->>Profile: Process & structure data
    Profile->>Student: Generate dynamic profile
    
    Student->>Goals: Request career recommendations
    Goals->>Profile: Fetch student profile data
    Goals->>Goals: Analyze career paths
    Goals->>Student: Present recommendations
    
    Student->>CV: Request CV generation
    CV->>Profile: Fetch profile data
    CV->>Goals: Fetch career goals
    CV->>CV: Generate optimized CV
    CV->>Student: Deliver formatted CV
    
    Student->>Tracking: Set placement preferences
    Tracking->>Profile: Fetch qualifications
    Tracking->>CV: Fetch latest CV
    Tracking->>Tracking: Match with opportunities
    Tracking->>Student: Prioritized placement list
    
    Admin->>Tracking: Access placement analytics
    Tracking->>Admin: Provide status dashboard
    Admin->>Student: Send interview notifications
```

## Conclusion and Recommendations

Based on our analysis, we recommend proceeding with the **Well-structured Team** approach using 5 SDEs with 1-2 years of experience. This option provides the optimal balance between delivery timeline (122 days) and cost (₹535,500).

Key recommendations:

- Begin with the foundation components (Profile Data Backend) as they are critical dependencies
- Implement a bi-weekly stakeholder review process aligned with sprint completions
- Maintain flexible resource allocation to address blockers as they arise
- Consider additional investment in automated testing to ensure quality of the AI components
- Plan for a phased rollout, starting with core features followed by enhanced capabilities

This implementation strategy provides the best mix of risk management, cost efficiency, and timeline certainty while delivering a high-quality product that meets the requirements of IIM Bangalore.
