# RevHire — Entity Relationship Diagram

## ER Diagram

```mermaid
erDiagram
    USER {
        Long id PK
        String name
        String email UK
        String password
        String phone
        String location
        Role role "SEEKER / EMPLOYER"
        DateTime createdAt
        DateTime updatedAt
    }

    JOB_SEEKER_PROFILE {
        Long id PK
        Long userId FK
        String headline
        String summary
        DateTime createdAt
        DateTime updatedAt
    }

    EDUCATION {
        Long id PK
        Long profileId FK
        String degree
        String institution
        String fieldOfStudy
        Integer startYear
        Integer endYear
    }

    EXPERIENCE {
        Long id PK
        Long profileId FK
        String title
        String company
        String location
        Date startDate
        Date endDate
        String description
    }

    SKILL {
        Long id PK
        Long profileId FK
        String name
        String proficiency
    }

    CERTIFICATION {
        Long id PK
        Long profileId FK
        String name
        String issuingOrg
        Date issueDate
        Date expiryDate
    }

    RESUME {
        Long id PK
        Long profileId FK
        String fileName
        String filePath
        String fileType
        String objective
        String projects
        DateTime uploadedAt
    }

    EMPLOYER {
        Long id PK
        Long userId FK
        String companyName
        String industry
        String companySize
        String description
        String website
        String location
        String logoPath
        DateTime createdAt
        DateTime updatedAt
    }

    JOB {
        Long id PK
        Long employerId FK
        String title
        String description
        String location
        Double salary
        JobType jobType "FULL_TIME / PART_TIME / CONTRACT / INTERNSHIP / REMOTE"
        JobStatus status "ACTIVE / CLOSED / FILLED / DRAFT"
        Integer views
        DateTime postedAt
        DateTime deadline
    }

    APPLICATION {
        Long id PK
        Long jobId FK
        Long seekerId FK
        String resumePath
        String coverLetter
        ApplicationStatus status "APPLIED / UNDER_REVIEW / SHORTLISTED / REJECTED / WITHDRAWN"
        DateTime appliedAt
        DateTime updatedAt
    }

    FAVORITE {
        Long id PK
        Long userId FK
        Long jobId FK
        DateTime savedAt
    }

    APPLICATION_NOTE {
        Long id PK
        Long applicationId FK
        String content
        DateTime createdAt
        DateTime updatedAt
    }

    NOTIFICATION {
        Long id PK
        Long userId FK
        String message
        NotificationType type "APPLICATION_UPDATE / JOB_RECOMMENDATION / SYSTEM"
        Boolean isRead
        String link
        DateTime createdAt
    }

    USER ||--o| JOB_SEEKER_PROFILE : "has (if SEEKER)"
    USER ||--o| EMPLOYER : "has (if EMPLOYER)"
    JOB_SEEKER_PROFILE ||--o{ EDUCATION : "has"
    JOB_SEEKER_PROFILE ||--o{ EXPERIENCE : "has"
    JOB_SEEKER_PROFILE ||--o{ SKILL : "has"
    JOB_SEEKER_PROFILE ||--o{ CERTIFICATION : "has"
    JOB_SEEKER_PROFILE ||--o{ RESUME : "has"
    EMPLOYER ||--o{ JOB : "posts"
    JOB ||--o{ APPLICATION : "receives"
    USER ||--o{ APPLICATION : "submits (SEEKER)"
    APPLICATION ||--o{ APPLICATION_NOTE : "has"
    USER ||--o{ FAVORITE : "saves"
    JOB ||--o{ FAVORITE : "saved in"
    USER ||--o{ NOTIFICATION : "receives"
```

```
USER → JOB_SEEKER_PROFILE : One-to-One (optional) because a user can have 0 or 1 job seeker profile.

USER → EMPLOYER : One-to-One (optional) because a user can have 0 or 1 employer account.

JOB_SEEKER_PROFILE → EDUCATION : One-to-Many because a job seeker profile can have multiple education records.

JOB_SEEKER_PROFILE → EXPERIENCE : One-to-Many because a job seeker profile can have multiple experiences.

JOB_SEEKER_PROFILE → SKILL : One-to-Many because a job seeker profile can have multiple skills.

JOB_SEEKER_PROFILE → CERTIFICATION : One-to-Many because a job seeker profile can have multiple certifications.

JOB_SEEKER_PROFILE → RESUME : One-to-Many because a job seeker profile can have multiple resumes.

EMPLOYER → JOB : One-to-Many because an employer can post multiple jobs.

JOB → APPLICATION : One-to-Many because one job can receive multiple applications.

USER → APPLICATION : One-to-Many because a user can apply to multiple jobs.

APPLICATION → APPLICATION_NOTE : One-to-Many because an application can have multiple notes.

USER → FAVORITE : One-to-Many because a user can save multiple jobs.

JOB → FAVORITE : One-to-Many because a job can be saved by multiple users.

USER → NOTIFICATION : One-to-Many because a user can receive multiple notifications.
```


## Table Summary

| # | Table | Owner | Module |
|---|-------|-------|--------|
| 1 | User | Ashwathy | Auth |
| 2 | JobSeekerProfile | Likhita | Profile |
| 3 | Education | Likhita | Profile |
| 4 | Experience | Likhita | Profile |
| 5 | Skill | Likhita | Profile |
| 6 | Certification | Likhita | Profile |
| 7 | Resume | Likhita | Profile |
| 8 | Employer | Chaitanya | Job |
| 9 | Job | Chaitanya | Job |
| 10 | Application | Shilpa | Application |
| 11 | Favorite | Shilpa | Application |
| 12 | ApplicationNote | Harika | Dashboard |
| 13 | Notification | Kunal | Notification |
