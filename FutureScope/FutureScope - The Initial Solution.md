---
tags:
  - index
  - work/eminence/placement-automation
created: 2025-01-12 21:04
project_name: FutureScope
---
# The Initial Solution Main Notes

```ad-abstract
collapse: open

The initial solution of a B2B SaaS Placement Automation platform, keeping in mind our solution drafts based on the [[Analysis of Competitors]].
```

## Resources

## Requirements

### Functional Requirements

#### Business-Level Requirements

1. Client-level data management should be possible with multi-tenancy in the future.
2. Different plans should provide different features to different clients. OPTIONAL
3. Strong user authorisation should be provided with Role-based Access Control (RBAC).
4. File storage system should support:
   - Multiple file types (IDENTIFICATION, PHOTO, PROMOTIONAL, PROOF, RESUME)
   - Secure URL generation
   - File integrity checks
   - Delight: Version control

#### Client-Level Requirements

1. Student Management
   - Profile management with basic details, photos, and identification
   - Different student types (Regular, JPR, PR, Alumni) with specific features
   - Snitch: Student complaint management system with different categories
   - Placement profile management with academic records
   - Experience tracking (Education, Work, Project, Research)
   - Resume management (Master and Sectoral)
   - Skills and language proficiency tracking
2. Company & Job Management
   - Company profile management with logos and descriptions
   - Job listing management with detailed requirements
   - Job Sector-based categorization
   - CTC ranges and eligibility criteria
   - Application tracking of Candidates
3. Event Management
   - Company and Institute events
   - Event attendance tracking
   - RSVP management: If less than expected, make mandatory
   - Dress code and venue management
   - Timeline integration
4. Case Competition Management
   - Competition lifecycle management
   - Registration and participation tracking
   - Timeline integration
5. Timeline
   - Automated Global placement timeline generation
   - Milestone tracking for events, jobs, and competitions
6. Communication
   - Automated group creation based on various criteria
   - Custom group creation for targeted communication and invitations to case competitions, events, and jobs
7. Resume and Profile Management
   - Experience and Resume Point proof verification
   - Document verification workflow
   - Let custom groups comment, edit or view the resume
   - Delight: Resume version control
8. Interview Management
   - Interview scheduling
   - Interview feedback management
   - Interview timeline integration
   - Interview preparation material
9. Forum & Discussion
   - Forum for Student Groups
   - Discussion boards for case competitions
   - Discussion boards for events
   - Discussion boards for jobs
10. Demo Onboarding
    - Completely frontend-driven
    - Test out every flow
11. History analysis
12. Career Counselling-like conversation bot to extract info

### Non-Functional Requirements

1. User experience should be better than competitors.
   1. Minimal opportunity for bugs.
   2. Faster response times.
2. Migration from competitors should be seamless and easy.

## [[FutureScope - Entities Involved]]

## Codebases Involved

1. Add here.

## Data Involved

1. Add here.

```ad-note
title: ## Unorganized Notes
collapse: open


```
