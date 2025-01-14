---
tags:
  - work/eminence/placement-automation
  - brainstorming
project_name: FutureScope
---
# FutureScope - Entities Involved

## Business-Level Entities

These entities will remain generic and used across clients.

### Business-Level Entities | Document Models

#### File Storage Map

Files will be uploaded to a file storage. Links to the uploaded files and their metadata will be stored in the database.

```mermaid
erDiagram
  FileStorage {
    uuid id PK "A unique identifier for the file"
    boolean is_active "Whether the file is active or not"
    json metadata "Raw metadata of the file. E.g. EXIF data for photos, Hashes"
    string description "The description of the file"
    string path UK "The path of the file in the file storage system"
    string type "The type of the file: IDENTIFICATION, PHOTO, PROMOTIONAL, PROOF, RESUME"
    string url UK "The URL of the file"
    string mime_type "The MIME type of the file"
    string original_name "Original filename when uploaded"
    number file_size "Size of file in bytes"
  }
```

### Business-Level Entities | Relational Models

#### Client

The B2B Clients which we are operating for. It can be a college for now.

```mermaid
erDiagram
  Client {
    uuid id PK "A unique identifier for the client"
    boolean is_active "Whether the client is active or not"
    string name UK "The name of the client"
    string plan_id FK "Identifies the Plan the client is on, determining what features they get"
  }
```

#### Plan-Feature Mapping

The plan which the client is on determines what features they get.

```mermaid
erDiagram
  Plan {
    uuid id PK "A unique identifier for the plan"
    boolean is_active "Whether the plan is active or not"
    string description "A description of the plan"
    string name "The name of the plan"
  }

  Feature {
    uuid id PK "A unique identifier for the feature"
    boolean is_active "Whether the feature is active or not"
    string description "A description of the feature"
    string name "The name of the feature"
  }

  PlanFeatureMapping {
    string id PK "A hash ID for the plan feature mapping generate by concatenating plan_id and feature_id"
    boolean is_active "Whether the plan feature mapping is active or not"
    string feature_id FK "Identifies the feature the plan has"
    string plan_id FK "Identifies the plan in the system which has the feature"
  }

  Plan ||--o{ PlanFeatureMapping : "has"
  Feature ||--o{ PlanFeatureMapping : "has"
```

##### Plan-Feature Mapping Cache

Features will be few and Plans will be fewer. So, we can cache all of the features available to a client at the client level.

#### Role-Permission Mapping

Different Roles have different Permissions and access levels.

```mermaid
erDiagram
  Role {
    uuid id PK "A unique identifier for the role"
    boolean is_active "Whether the role is active or not"
    string description "A description of the role"
    string name "The name of the role"
  }

  Permission {
    uuid id PK "A unique identifier for the permission"
    boolean is_active "Whether the permission is active or not"
    string description "A description of the permission"
    string name "The name of the permission"
  }

  
  RolePermissionMapping {
    string id PK "A hash ID for the role permission mapping generate by concatenating role_id and permission_id"
    boolean is_active "Whether the role permission mapping is active or not"
    string permission_id FK "Identifies the permission the role has"
    string role_id FK "Identifies the role in the system which has the permission"
  }

  Role ||--o{ RolePermissionMapping : "has"
  Permission ||--o{ RolePermissionMapping : "has"
```

##### Role-Permission Mapping Cache

Permissions will be few and Roles will be fewer. So, we can cache all of the permissions available to a user at the user level.

#### User Authorisation

The user authorisation which the client can get.

```mermaid
erDiagram
  UserAuthorisation {
    uuid id PK "A unique identifier for the user"
    boolean is_active "Whether the user is active or not"
    string email UK "The email of the user"
    string name "The name of the user"
    string phone UK "The phone number of the user"
    string role_id FK "Identifies the role the user has, determining what permissions they get"
    string secret_hash "The hash of the user's secret used to login"
    string user_id UK "Frontend-facing ID of the user"
    boolean email_verified "Email verification status" 
    boolean phone_verified "Phone verification status"
  }

  UserAuthorisation ||--|| Role : "has"
```

## Client-Level Entities

### Client-Level Entities | Document Models

#### Case Comps

Represents the case competitions that the students can participate in.

```mermaid
erDiagram
  CaseComp {
    uuid id PK "A unique identifier for the case competition"
    boolean is_active "Whether the case competition is active or not"
    string client_id FK "Identifies the client the case competition has been highlighted to"
    string description "A description of the case competition"
    string end_date "The end date of the case competition"
    string name "The name of the case competition"
    string start_date "The start date of the case competition"
    string status "The status of the case competition: COMPLETE, ONGOING, UPCOMING"
    string url "The URL of the case competition to get more information"
  }
```

#### Resume

Represents the resume of a student.

```mermaid
erDiagram
  Resume {
    uuid id PK "A unique identifier for the resume"
    boolean is_active "Whether the resume is active or not."
    string client_id FK "Identifies the client the resume belongs to"
    string comment_permission_group_id FK "Identifies the student group which has permission to comment on the resume, if any"
    string edit_permission_group_id FK "Identifies the student group which has permission to edit the resume, if any"
    string file_id FK "Identifies the stored file which is the resume"
    string resume_type "The type of the resume: MASTER, SECTORAL. A student can have only one MASTER resume"
    string[] section_order "The order of the sections in the resume"
    string sector_id FK "Identifies the sector of the resume. NULL for MASTER Resumes"
    string status "The status of the resume: DRAFT, ACTIVE"
    string student_id FK "Identifies the student the resume belongs to"
    string view_permission_group_id FK "Identifies the student group which has permission to view the resume, if any"
  }

  ResumePoint {
    uuid id PK "A unique identifier for the resume point"
    boolean is_active "Whether the resume point is active or not"
    boolean should_show "Whether the resume point should be shown in the resume"
    string client_id FK "Identifies the client the resume point belongs to"
    string proof_file_id FK "Identifies the stored file which is the proof of the resume point"
    string resume_id FK "Identifies the resume the point belongs to"
    string section "The section of the resume point: EDUCATION, EXPERIENCE, PROJECT, SKILLS, ACHIEVEMENTS"
    string text "The text of the resume point"
    string verification_status "The verification status of the experience: PENDING, REJECTED, VERIFIED"
  }

  Resume }|--o{ ResumePoint : "has"
  Resume ||--o{ StudentGroup : "contains"
```

#### Student

Represents the critical information of students of a client.

```mermaid
erDiagram
  Student {
    uuid id PK "A unique identifier for the student"
    boolean is_active "Whether the student is active or not"
    string aadhar_file_id FK "Identifies the stored file which is the Aadhar card of the student"
    string address "The address of the student"
    string batch "The batch year of the student"
    string client_id FK "Identifies the client the student belongs to"
    date dob "The date of birth of the student"
    string emergency_contact_name "The name of the emergency contact of the student"
    string emergency_contact_phone "The phone number of emergency contact of the student"
    string lifecycle_type "The lifecycle type of the student: NONE, JPR, PR, ALUMNI"
    string name "The name of the student"
    string photo_file_id FK "Identifies the stored file which is the photo of the student"
    string roll_number UK "The roll number of the student"
    string user_id FK "Identifies the user that the student is"
  }

  Alumni {
    %% Inherits all fields from Student %%
    string lifecycle_type "The lifecycle type of the student: ALUMNI"
    string additional_field "Any additional field specific to ALUMNI"
  }

  JuniorPlacementRepresentative {
    %% Inherits all fields from Student %%
    string lifecycle_type "The lifecycle type of the student: JPR"
    string additional_field "Any additional field specific to JPR"
  }
  
  SeniorPlacementRepresentative {
    %% Inherits all fields from Student %%
    string lifecycle_type "The lifecycle type of the student: PR"
    string additional_field "Any additional field specific to PR"
  }

  Student ||--|| UserAuthorisation: "has"
  Student ||--|| FileStorage : "has"
  Student ||--|| Alumni : "is a"
  Student ||--|| JuniorPlacementRepresentative : "is a"
  Student ||--|| SeniorPlacementRepresentative : "is a"
```

#### Student Profile

```mermaid
erDiagram
  StudentProfile {
    uuid id PK "A unique identifier for the placement profile"
    boolean is_active "Whether the placement profile is active or not"
    number grade_10_score "The aggregated score of the student in the 10th grade out of 100"
    number grade_12_score "The aggregated score of the student in the 12th grade out of 100"
    string client_id FK "Identifies the client the placement profile belongs to"
    string master_resume_id FK "Identifies the Resume which is the master resume of the student"
    string status "The status of the placement profile: NOT_ENROLLED, ENROLLED, EOP, BANNED"
    string student_id FK "Identifies the student the placement profile belongs to"
    string[] skills "Array of skill identifiers"
    string[] languages "Array of languages known"
    number cgpa "Current CGPA"
    number backlogs "Number of backlogs the student has"
  }

  ProfileExperience {
    uuid id PK "A unique identifier for the experience"
    boolean is_active "Whether the experience is active or not"
    date end_date "The end date of the experience. NULL if ONGOING status"
    date start_date "The start date of the experience"
    string client_id FK "Identifies the client the experience belongs to"
    string profile_experience_type "The type of the experience: AWARD, EDUCATION, PROJECT, WORK, RESEARCH"
    string proof_file_id FK "Identifies the stored file which is the proof of the experience"
    string status "The status of the education experience: COMPLETED, ONGOING"
    string student_profile_id FK "Identifies the student profile the experience belongs to. Student might choose to show only some of the experiences in their profile"
    string verification_status "The verification status of the experience: PENDING, REJECTED, VERIFIED"
  }

  AwardExperience {
    %% Inherits all fields from ProfileExperience %%
    string description "The description of the award experience"
    string name "The name of the award / achievement / competition"
    string organisation "The organisation in which the award was received"
    string position "Position achieved in the competition"
  }

  EducationExperience {
    %% Inherits all fields from ProfileExperience %%
    number score "The score achieved in the education experience out of 100"
    string degree "The degree of the education experience"
    string institution "The institution of the education experience"
    string major "The major course of the education experience"
    string[] minors "The minor courses of the education experience"
  }

  ProjectExperience {
    %% Inherits all fields from ProfileExperience %%
    string description "The description of the project experience"
    string domain "The domain of the project experience"
    string name "The name of the project experience"
    string organisation "The organisation in which the project was created, if any"
  }

  WorkExperience {
    %% Inherits all fields from ProfileExperience %%
    string company "The company of the work experience"
    string designation "The designation of the work experience"
    string sector_id FK "Identifies the sector of the work experience"
  }

  ResearchExperience {
    %% Inherits all fields from ProfileExperience %%
    string description "The description of the research experience"
    string domain "The domain of the research experience"
    string organisation "The organisation in which the research was performed, if any"
    string[] publications "The publications of the research experience, if any"
    string title "The title of the research experience"
  }


  Student ||--|{ StudentProfile : "has"
  StudentProfile ||--o{ Resume : "has"
  StudentProfile ||--|{ ProfileExperience : "has"
  ProfileExperience ||--o{ AwardExperience : "is a"
  ProfileExperience ||--o{ EducationExperience : "is a"
  ProfileExperience ||--o{ ProjectExperience : "is a"
  ProfileExperience ||--o{ WorkExperience : "is a"
  ProfileExperience ||--o{ ResearchExperience : "is a"
```

### Client-Level Entities | Relational Models

#### Company

Represents the companies which are hiring.

```mermaid
erDiagram
  Company {
    uuid id PK "A unique identifier for the company"
    boolean is_active "Whether the company is active or not"
    string client_id FK "Identifies the client the company is hiring for"
    string description "A description of the company"
    string name "The name of the company"
    string logo_file_id FK "Identifies the stored file which is the logo of the company"
    string url "The URL to the website of the company"
  }
```

#### Events

Represents the events that the companies or institute is hosting.

```mermaid
erDiagram
  Event {
    uuid id PK "A unique identifier for the event"
    boolean is_active "Whether the event is active or not"
    boolean should_show_on_global_timeline "Whether the event should be shown on the global timeline of the institute"
    string client_id FK "Identifies the client the event is for"
    string company_id FK "Identifies the company which is hosting the event, if not the institute"
    string description "A description of the event"
    string dress_code "The dress code of the event: FORMAL, SEMI_FORMAL, INFORMAL"
    string end_date "The end date of the event"
    string invite_type "The type of invitation for the event: OPEN, INVITE_ONLY"
    string name "The name of the event"
    string start_date "The start date of the event"
    string status "The status of the event: COMPLETED, ONGOING, UPCOMING"
    string host "The host of the event: COMPANY, INSTITUTE"
    string url "The URL of the event to get more information"
    string venue "The venue of the event. ONLINE if it is an online event"
  }

  EventAttendee {
    string id PK "A hash ID for the event attendee generated by concatenating event_id and student_id"
    boolean is_active "Whether the event attendee is active or not"
    boolean has_attended "Whether the student has attended the event or not"
    string attendance_type "The type of attendance for the event: MANDATORY, VOLUNTARY"
    string client_id FK "Identifies the client the event attendee is for"
    string event_id FK "Identifies the event the student is attending"
    string rsvp "The RSVP so far of the event attendee: ACCEPTED, DECLINED, MAYBE, NOT_RESPONDED"
    string student_id FK "Identifies the student who is attending the event"
  }

  Event ||--o{ EventAttendee : "has"
```

#### Job Listings

Represents the job listings that the companies have posted.

```mermaid
erDiagram
  JobListing {
    uuid id PK "A unique identifier for the job listing"
    boolean is_active "Whether the job listing is active or not"
    string client_id FK "Identifies the client the job listing is for"
    string company_id FK "Identifies the company which posted the job listing"
    string job_type "The type of the job listing: INTERNSHIP, FULL_TIME, CONTRACT"
    string location "The location of the job listing"
    string sector_id FK "Identifies the sector of the job listing"
    string status "The status of the job listing: OPEN, CLOSED, UPCOMING"
    string title "The title of the job listing"
    string[] tags "The tags based on which the job listing can be filtered. Eg. Dream, Core, Non-Core"
    text description "A description of the job listing"
    number ctc_min "Minimum CTC offered for the job"
    number ctc_max "Maximum CTC offered for the job"
    string[] required_skills "Required skills for the job"
    string[] preferred_skills "Preferred skills for the job"
    number min_cgpa "Minimum CGPA requirement"
    boolean allows_backlogs "Whether backlogs are allowed"
    date application_deadline "Application deadline"
  }
```

#### Sector

Represents the sectors of career paths possible.

```mermaid
erDiagram
  Sector {
    uuid id PK "A unique identifier for the sector"
    boolean is_active "Whether the sector is active or not"
    string client_id FK "Identifies the client the Sector belongs to"
    string description "A description of the sector"
    string name "The name of the sector"
  }
```

#### Student Complaints

Represents the complaints that the students have raised about them.

```mermaid
erDiagram
  StudentComplaint {
    uuid id PK "A unique identifier for the student complaint"
    boolean is_active "Whether the student complaint is active or not"
    string response_status "Status of the response to the student complaint: ONGOING, PENDING, RESOLVED, REJECTED"
    number fine_amount "The amount of fine for the student complaint if the penalty is FINE"
    string academic_subtype "The subtype of the student complaint if the type is ACADEMIC: ATTENDANCE, GRADES, NONE, OTHER"
    string administrative_subtype "The subtype of the student complaint if the type is ADMINISTRATIVE: MISBEHAVIOUR, FAKE_DOCUMENT. NONE, OTHER"
    string client_id FK "Identifies the client the student complaint is for"
    string description "A description of the student complaint"
    string penalty "The penalty for the student complaint: FINE, SUSPENSION, WARNING, EXPULSION"
    string placement_subtype "The subtype of the student complaint if the type is PLACEMENT: DID_NOT_ATTEND_EVENT, USING_PHONE_DURING_EVENT, MISBEHAVIOUR, USING_UNFAIR_MEANS, UNPROFESSIONAL_ATTIRE, NONE, OTHER"
    string rejection_reason "The reason for rejection of the student complaint, if the response status is REJECTED"
    string student_id FK "Identifies the student who has the complaint"
    string type "The type of the student complaint: ACADEMIC, ADMINISTRATIVE, PLACEMENT"
  }
```

#### Student Groups - Custom

Represents custom groups of students that can be created by the client. These groups can be used for various purposes:

- Sending targeted emails or notifications
- Creating targeted custom case competitions, events, or job listings
- Generate chat rooms and forums for the group

```mermaid
erDiagram
  StudentGroup {
    uuid id PK "A unique identifier for the student group"
    boolean is_active "Whether the student group is active or not"
    string client_id FK "Identifies the client the student group belongs to"
    string description "A description of the student group"
    string name "The name of the student group"
  }

  StudentGroupMember {
    string id PK "A hash ID for the student group member generated by concatenating student_group_id and student_id"
    boolean is_active "Whether the student group member is active or not"
    string client_id FK "Identifies the client the student group member is for"
    string student_group_id FK "Identifies the student group the student is a part of"
    string student_id FK "Identifies the student who is a part of the student group"
  }

  StudentGroupMember ||--|| Student : "is"
  StudentGroup ||--o{ StudentGroupMember : "has"
```

### Client-Level Entities | Derived Models

#### Client Global Timeline

Students can see the client's global placement timeline anytime to stay updated on their placement journey.

```mermaid
erDiagram
  GlobalTimeline {
    string id PK "A hash ID for the client global timeline generated by concatenating client_id and year"
    boolean is_active "Whether the client global timeline is active or not"
    string client_id FK "Identifies the client that the global timeline is for"
    string year "The year of the global timeline"
  }

  GlobalTimelineMilestone {
    string id PK "A hash ID for the client global timeline event generated by concatenating client_global_timeline_id, milestone_type and milestone_id"
    boolean is_active "Whether the client global timeline event is active or not"
    boolean should_show "Whether the milestone should be shown on the global timeline of the client"
    string client_id FK "Identifies the client that the global timeline event is for"
    string global_timeline_id FK "Identifies the global timeline the milestone is for"
    string logo_file_id FK "Identifies the stored file which is the logo of the milestone"
    string milestone_id "Identifies the milestone externally"
    string milestone_type "The type of the milestone: EVENT, CASE_COMP, JOB"
    string name "The name of the milestone"
  }

  EventTimelineMilestone {
    %% Inherits all fields from GlobalTimelineMilestone %%
    string milestone_id FK "Represents the identifier of the event the milestone is for"
    string milestone_type "The type of the milestone: EVENT"
  }

  CaseCompTimelineMilestone {
    %% Inherits all fields from GlobalTimelineMilestone %%
    string milestone_id FK "Represents the identifier of the case competition the milestone is for"
    string milestone_type "The type of the milestone: CASE_COMP"
  }

  JobListingTimelineMilestone {
    %% Inherits all fields from GlobalTimelineMilestone %%
    string milestone_id FK "Represents the identifier of the job listing the milestone is for"
    string milestone_type "The type of the milestone: JOB"
  }

  Event ||--|| EventTimelineMilestone : "creates"
  CaseComp ||--|| CaseCompTimelineMilestone : "creates"
  JobListing ||--|| JobListingTimelineMilestone : "creates"

  GlobalTimeline ||--o{ GlobalTimelineMilestone : "has"
  GlobalTimelineMilestone ||--o{ EventTimelineMilestone : "is a"
  GlobalTimelineMilestone ||--o{ CaseCompTimelineMilestone : "is a"
  GlobalTimelineMilestone ||--o{ JobListingTimelineMilestone : "is a"
```

##### Deriving Client Global Timeline

The client's global timeline can be derived from the events, case competitions, and job listings that the client has.

#### Student Groups - Generated

Represents the groups of students that are generated by the system based on various criteria.

- Based on the same previous Education Experience Degree / Major
- Based on applying for the same Job Listing
- Based on the same previous Project / Research Experience Domain
- Based on the same Sector Resume created
- Based on the same previous Work Experience Sector

```mermaid
erDiagram
  GeneratedStudentGroup {
    uuid id PK "A unique identifier for the generated student group"
    boolean is_active "Whether the generated student group is active or not"
    string client_id FK "Identifies the client the generated student group belongs to"
    string description "A description of the generated student group"
    string name "The name of the generated student group"
    string grouping_type "The type of the generated student group: EDUCATION_DEGREE, EDUCATION_MAJOR, JOB_LISTING_APPLIED, PROJECT_DOMAIN, RESEARCH_DOMAIN, RESUME_SECTOR, WORK_SECTOR"
  }

  GeneratedStudentEducationDegreeGroup {
    %% Inherits all fields from GeneratedStudentGroup %%
    string grouping_type "The type of the generated student group: EDUCATION_DEGREE"
    string degree "The degree of the education experience linking the students"
  }

  GeneratedStudentEducationMajorGroup {
    %% Inherits all fields from GeneratedStudentGroup %%
    string grouping_type "The type of the generated student group: EDUCATION_MAJOR"
    string major "The major course of the education experience linking the students"
  }

  GeneratedStudentJobListingAppliedGroup {
    %% Inherits all fields from GeneratedStudentGroup %%
    string grouping_type "The type of the generated student group: JOB_LISTING_APPLIED"
    string job_listing_id FK "Identifies the job listing the students have applied to"
  }

  GeneratedStudentProjectDomainGroup {
    %% Inherits all fields from GeneratedStudentGroup %%
    string grouping_type "The type of the generated student group: PROJECT_DOMAIN"
    string domain "The domain of the project experience linking the students"
  }

  GeneratedStudentResearchDomainGroup {
    %% Inherits all fields from GeneratedStudentGroup %%
    string grouping_type "The type of the generated student group: RESEARCH_DOMAIN"
    string domain "The domain of the research experience linking the students"
  }

  GeneratedStudentResumeSectorGroup {
    %% Inherits all fields from GeneratedStudentGroup %%
    string grouping_type "The type of the generated student group: RESUME_SECTOR"
    string sector_id FK "Identifies the sector of the resume linking the students"
  }

  GeneratedStudentWorkSectorGroup {
    %% Inherits all fields from GeneratedStudentGroup %%
    string grouping_type "The type of the generated student group: WORK_SECTOR"
    string sector_id FK "Identifies the sector of the work experience linking the students"
  }

  EducationExperience }o--|| GeneratedStudentEducationDegreeGroup : "creates"
  EducationExperience }o--|| GeneratedStudentEducationMajorGroup : "creates"
  JobListing }o--|| GeneratedStudentJobListingAppliedGroup : "creates"
  ProjectExperience }o--|| GeneratedStudentProjectDomainGroup : "creates"
  ResearchExperience }o--|| GeneratedStudentResearchDomainGroup : "creates"
  Resume }o--|| GeneratedStudentResumeSectorGroup : "creates"
  WorkExperience }o--|| GeneratedStudentWorkSectorGroup : "creates"

  GeneratedStudentGroup ||--o{ GeneratedStudentEducationDegreeGroup : "is a"
  GeneratedStudentGroup ||--o{ GeneratedStudentEducationMajorGroup : "is a"
  GeneratedStudentGroup ||--o{ GeneratedStudentJobListingAppliedGroup : "is a"
  GeneratedStudentGroup ||--o{ GeneratedStudentProjectDomainGroup : "is a"
  GeneratedStudentGroup ||--o{ GeneratedStudentResearchDomainGroup : "is a"
  GeneratedStudentGroup ||--o{ GeneratedStudentResumeSectorGroup : "is a"
  GeneratedStudentGroup ||--o{ GeneratedStudentWorkSectorGroup : "is a"
  GeneratedStudentGroup ||--o{ StudentGroupMember : "has"
  StudentGroupMember ||--|| Student : "has"
```

## Notes

1. Multi-tenant structure?
2. We are selling an entire ecosystem: Maybe don't focus too much on feature flags now.
