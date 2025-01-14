---
tags:
  - work/eminence/placement-automation
  - brainstorming
---
# Analysis of Competitors

## EdTex - Skynet

### EdTex - Skynet Products

#### Placement Automation

1. CV and profile generation, CV validation.
2. Offer Management with Workflows: Spot, Dream; Day 0, Day 1
3. Statistics and Trends

#### Timetable Management

1. Class Demand Insights
2. Class Clash Management

#### Admission Automation

1. Screening Students: Custom algorithms based on scores.
2. Report Generation: Shortlist and Admit list generation
3. Candidate Transparency: End-to-end visibility for candidates for all stages of processing.
4. Communication: Touch points for prospective student interaction.

### EdTex - Skynet Features

#### Process Automation

1. Connect the Campus: Program enrollments, course scheduling, academic planning, and data management
	1. Maintain programs, courses, student enrollment and schedules
2. Transparency: Openly communicating procedures and events
	1. Broadcast messaging and notifications for students. Can we do better than e-mail?
3. Global Access: Use Across borders and time zones
	1. Seems like a meaningless point.
4. Integrations and AI
	1. What third parties are they integrating with? What AI features are they providing?

#### Analytics

1. Analytics and Insights: For Resource Allocation, Student success initiatives, cross-discipline collaboration
2. Academic Operations Analytics
	1. What does this even mean?
3. Reports and Insights for Decision Makers
4. **RBAC**: Role-based access control for data

#### Systems Integrations

1. SSO Login
2. Modularity

#### Academic ERP

1. Workflow Management: Admission, Scheduling, Grading

#### Consultation

Consulting on academic processes, digital transformation and implementation support.

### EdTex - Skynet User Flows Deep-Dive

#### Key Roles

1. Interview and Event Scheduler
2. Company Volunteer: Touchpoints for companies
3. Front Desk: Touchpoints for students
4. Controls Team: Manage overall process

#### Admin Portal

##### Pre-Placement Automation

1. Add companies
2. Add students (registration time)

##### Placement Automation

1. Schedule interviews: Round wise
2. Track students
	1. Take attendance
	2. Send to interview
	3. State transition and loop

### EdTex - Skynet System Design - 10,000-Feet High and Full of Assumptions

#### Data Involved

1. Student Data
2. Company Data
	1. Panels and Availability

#### Placement Student Interview Workflow
![[skynet-student-online-workflow.png]]

![[skynet-student-offline-workflow.png]]

## Superset

### Superset Products

### Superset Features

### Superset User Flows Deep-Dive

### Superset System Design - 10,000-Feet High and Full of Assumptions

## Generic Learnings

1. My immediate conclusion is that the support team in B2B SaaS is probably more of a factor for adoption than how good of a product you are selling. 
	1. https://www.edtex.in/products/placements-automation-software

## Action Items

1. Figure out what third parties and AI [[Analysis of Competitors#EdTex - Skynet|EdTex]] are integrating with and whether people are even aware of the impact of those integrations.
2. Collect as much data as possible in release 1 so it empowers: 
	1. The Product team to determine what kind of analytics can help empower the institute and its students.
	2. The Institute to extract insights from their student data that they can use. Edtex showed an example of Previous Work Background vs Future Career Domain Interests Heatmap chart
3. Keep in mind whether the pain points you were facing were because of a platform issue or an admin issue
