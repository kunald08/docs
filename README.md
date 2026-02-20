# RevHire — Complete Project Plan & Module Assignment

## Table of Contents
1. [Project Overview](#project-overview)
2. [Tech Stack](#tech-stack)
3. [Team Module Assignment](#team-module-assignment)
4. [Database Design (ERD)](#database-design-erd)
5. [Package Structure](#package-structure)
6. [API Endpoints (Per Module)](#api-endpoints-per-module)
7. [Entity Definitions](#entity-definitions)
8. [Build Order & Timeline](#build-order--timeline)
9. [Git Workflow](#git-workflow)
10. [Shared Responsibilities](#shared-responsibilities)
11. [Definition of Done Checklist](#definition-of-done-checklist)

---

## Project Overview

RevHire is a full-stack monolithic web application — a job portal connecting **Job Seekers** with **Employers**.

- **Job Seekers** can: Register, build/upload resumes, search jobs, apply, track applications, save favorites, receive notifications.
- **Employers** can: Register company, post jobs, manage postings, view/filter applicants, shortlist/reject, view dashboard stats.

---

## Tech Stack

| Technology      | Version / Details                        |
|-----------------|------------------------------------------|
| Java            | 17+                                      |
| Spring Boot     | 3.x                                      |
| Spring Security | Session-based authentication              |
| Spring Data JPA | ORM & Database access                    |
| **Thymeleaf**   | **Server-side HTML templating engine**   |
| MySQL           | Relational Database                      |
| Maven           | Build & dependency management            |
| JUnit 4         | Unit & Integration testing               |
| Log4J           | Logging framework                        |
| Lombok          | Boilerplate reduction                    |
| Bootstrap 5     | Responsive CSS framework (with Thymeleaf)|
| Git & GitHub    | Version control                          |

---

## Team Module Assignment

### Member: Aswathy — Authentication & User Management
| Item             | Details |
|------------------|---------|
| **Branch**       | `feature/auth` |
| **Package**      | `com.revhire.auth`, `com.revhire.config` |
| **Responsibilities** | |
| | User Registration (Job Seeker + Employer) |
| | Login / Logout |
| | Spring Security configuration (session-based with Thymeleaf form login) |
| | Role-based access control (ROLE_SEEKER, ROLE_EMPLOYER) |
| | Password encoding (BCrypt) |
| | Thymeleaf login, register, register-choice pages |
| **Entities**     | `User` |
| **Endpoints**    | `/auth/*` |
| **Thymeleaf Pages** | `login.html`, `register.html`, `register-choice.html` (pick Seeker/Employer) |
| **Tests**        | Auth service tests, security filter tests |

---

### Member: Likhita — Job Seeker Profile & Resume
| Item             | Details |
|------------------|---------|
| **Branch**       | `feature/profile` |
| **Package**      | `com.revhire.profile` |
| **Responsibilities** | |
| | Job Seeker profile CRUD (create, read, update, delete) |
| | Education management (add, edit, remove education entries) |
| | Work Experience management |
| | Skills management |
| | Certifications management |
| | Textual resume builder (structured sections: objective, education, experience, skills, projects, certifications) |
| | Resume file upload (PDF/DOCX, max 2MB) |
| | Resume file download |
| | Profile view endpoint (for employers to see) |
| **Entities**     | `JobSeekerProfile`, `Education`, `Experience`, `Skill`, `Certification`, `Resume` |
| **Endpoints**    | `/profile/*`, `/resume/*` |
| **Thymeleaf Pages** | `profile.html`, `profile-edit.html`, `resume-builder.html`, `resume-upload.html`, `view-profile.html` (public view) |
| **Tests**        | Profile service tests, resume upload tests |

---

### Member: Chaitanya — Employer Profile & Job Posting
| Item             | Details |
|------------------|---------|
| **Branch**       | `feature/job` |
| **Package**      | `com.revhire.employer`, `com.revhire.job` |
| **Responsibilities** | |
| | Employer/Company profile CRUD |
| | Company info management (name, industry, size, description, website, location) |
| | Job posting CRUD (create, read, update, delete) |
| | Job lifecycle management (close, reopen, mark as filled) |
| | Job detail view (public) |
| | Job statistics per posting (views, applications count) |
| | Company profile public page |
| **Entities**     | `Employer`, `Job` |
| **Endpoints**    | `/employers/*`, `/jobs/*` (CRUD) |
| **Thymeleaf Pages** | `company-profile.html`, `company-edit.html`, `job-create.html`, `job-edit.html`, `job-detail.html`, `my-jobs.html` (employer's job list) |
| **Tests**        | Job service tests, employer service tests |

---

### Member: Shilpa — Job Search & Application
| Item             | Details |
|------------------|---------|
| **Branch**       | `feature/application` |
| **Package**      | `com.revhire.application` |
| **Responsibilities** | |
| | Advanced job search with filters (role, location, experience, company, salary range, job type, date posted) |
| | Search using Spring Data JPA Specifications |
| | One-click apply (saved resume + optional cover letter) |
| | Application status tracking (Applied → Under Review → Shortlisted → Rejected → Withdrawn) |
| | View all my applications with job details and status |
| | Withdraw application (with confirmation + optional reason) |
| | Save jobs to favorites |
| | Remove from favorites |
| | View favorite jobs list |
| **Entities**     | `Application`, `Favorite` |
| **Endpoints**    | `/jobs/search`, `/applications/*`, `/favorites/*` |
| **Thymeleaf Pages** | `job-search.html`, `job-search-results.html`, `apply-job.html`, `my-applications.html`, `application-detail.html`, `favorites.html` |
| **Tests**        | Search filter tests, application service tests |

---

### Member: Harika — Applicant Management & Employer Dashboard
| Item             | Details |
|------------------|---------|
| **Branch**       | `feature/dashboard` |
| **Package**      | `com.revhire.employer.dashboard`, `com.revhire.employer.applicant` |
| **Responsibilities** | |
| | View all applicants for a specific job |
| | View applicant details (profile, textual resume, uploaded resume, cover letter, applied date) |
| | Shortlist application (single) |
| | Reject application (single) |
| | Bulk shortlist / bulk reject |
| | Add optional comments when shortlisting/rejecting |
| | Filter applicants by experience, skills, education, application date, status |
| | Application notes (internal tracking — add, edit, delete notes) |
| | Employer Dashboard API: total jobs, active jobs, total applications, pending reviews |
| **Entities**     | `ApplicationNote` |
| **Endpoints**    | `/employer/applicants/*`, `/employer/dashboard`, `/employer/notes/*` |
| **Thymeleaf Pages** | `employer-dashboard.html`, `applicant-list.html`, `applicant-detail.html`, `applicant-filter.html` |
| **Tests**        | Applicant filter tests, dashboard stats tests, bulk action tests |

---

### Member: Kunal — Notifications, Project Setup & Testing Infrastructure
| Item             | Details |
|------------------|---------|
| **Branch**       | `feature/notification` + initial `main` setup |
| **Package**      | `com.revhire.notification`, `com.revhire.exception`, `com.revhire.common` |
| **Responsibilities** | |
| | **Project Scaffolding:** Spring Boot project creation, Maven config, application.properties |
| | **Database Setup:** MySQL schema, initial config |
| | **Global Exception Handling:** `@ControllerAdvice`, custom exceptions |
| | **Log4J Configuration:** log4j2.xml setup, logging standards |
| | **Notification Entity & Service** |
| | Trigger notifications on: application status change, new job matching profile |
| | Get all notifications for user |
| | Mark notification as read |
| | Mark all as read |
| | Delete notification |
| | Unread notification count |
| | **Common DTOs:** ApiResponse wrapper, Pagination response |
| | **ERD Diagram** (draw.io or dbdiagram.io) |
| | **Architecture Diagram** |
| | **README.md** |
| **Entities**     | `Notification` |
| **Endpoints**    | `/notifications/*` |
| **Thymeleaf Pages** | `notifications.html`, common fragments: `layout.html`, `navbar.html`, `footer.html`, `sidebar.html`, `error.html` |
| **Tests**        | Notification service tests, exception handler tests |

---

## Database Design (ERD)

### Tables & Columns

#### `users`
| Column             | Type         | Constraints              |
|--------------------|--------------|--------------------------|
| id                 | BIGINT       | PK, AUTO_INCREMENT       |
| name               | VARCHAR(100) | NOT NULL                 |
| email              | VARCHAR(100) | NOT NULL, UNIQUE         |
| password           | VARCHAR(255) | NOT NULL                 |
| phone              | VARCHAR(15)  |                          |
| location           | VARCHAR(100) |                          |
| role               | ENUM         | 'SEEKER', 'EMPLOYER'     |
| created_at         | TIMESTAMP    | DEFAULT CURRENT_TIMESTAMP|
| updated_at         | TIMESTAMP    |                          |

#### `job_seeker_profiles`
| Column               | Type         | Constraints              |
|----------------------|--------------|--------------------------|
| id                   | BIGINT       | PK, AUTO_INCREMENT       |
| user_id              | BIGINT       | FK → users.id, UNIQUE    |
| headline             | VARCHAR(200) |                          |
| summary              | TEXT         |                          |
| current_employment_status | VARCHAR(50) |                      |
| profile_picture_url  | VARCHAR(500) |                          |

#### `educations`
| Column       | Type         | Constraints              |
|-------------|--------------|--------------------------|
| id          | BIGINT       | PK, AUTO_INCREMENT       |
| profile_id  | BIGINT       | FK → job_seeker_profiles.id |
| institution | VARCHAR(200) | NOT NULL                 |
| degree      | VARCHAR(100) |                          |
| field       | VARCHAR(100) |                          |
| start_date  | DATE         |                          |
| end_date    | DATE         |                          |
| grade       | VARCHAR(20)  |                          |

#### `experiences`
| Column       | Type         | Constraints              |
|-------------|--------------|--------------------------|
| id          | BIGINT       | PK, AUTO_INCREMENT       |
| profile_id  | BIGINT       | FK → job_seeker_profiles.id |
| company     | VARCHAR(200) | NOT NULL                 |
| title       | VARCHAR(100) |                          |
| location    | VARCHAR(100) |                          |
| start_date  | DATE         |                          |
| end_date    | DATE         |                          |
| description | TEXT         |                          |
| is_current  | BOOLEAN      | DEFAULT FALSE            |

#### `skills`
| Column       | Type         | Constraints              |
|-------------|--------------|--------------------------|
| id          | BIGINT       | PK, AUTO_INCREMENT       |
| profile_id  | BIGINT       | FK → job_seeker_profiles.id |
| name        | VARCHAR(100) | NOT NULL                 |
| proficiency | VARCHAR(50)  |                          |

#### `certifications`
| Column           | Type         | Constraints              |
|-----------------|--------------|--------------------------|
| id              | BIGINT       | PK, AUTO_INCREMENT       |
| profile_id      | BIGINT       | FK → job_seeker_profiles.id |
| name            | VARCHAR(200) | NOT NULL                 |
| issuing_org     | VARCHAR(200) |                          |
| issue_date      | DATE         |                          |
| expiry_date     | DATE         |                          |
| credential_url  | VARCHAR(500) |                          |

#### `resumes`
| Column         | Type         | Constraints              |
|---------------|--------------|--------------------------|
| id            | BIGINT       | PK, AUTO_INCREMENT       |
| profile_id    | BIGINT       | FK → job_seeker_profiles.id |
| objective     | TEXT         |                          |
| file_name     | VARCHAR(255) |                          |
| file_type     | VARCHAR(10)  | 'PDF' or 'DOCX'         |
| file_data     | LONGBLOB     |                          |
| file_size     | BIGINT       | max 2MB (2097152 bytes)  |
| created_at    | TIMESTAMP    |                          |
| updated_at    | TIMESTAMP    |                          |

#### `employers`
| Column       | Type         | Constraints              |
|-------------|--------------|--------------------------|
| id          | BIGINT       | PK, AUTO_INCREMENT       |
| user_id     | BIGINT       | FK → users.id, UNIQUE    |
| company_name| VARCHAR(200) | NOT NULL                 |
| industry    | VARCHAR(100) |                          |
| company_size| VARCHAR(50)  |                          |
| description | TEXT         |                          |
| website     | VARCHAR(500) |                          |
| location    | VARCHAR(200) |                          |
| logo_url    | VARCHAR(500) |                          |

#### `jobs`
| Column            | Type         | Constraints              |
|------------------|--------------|--------------------------|
| id               | BIGINT       | PK, AUTO_INCREMENT       |
| employer_id      | BIGINT       | FK → employers.id        |
| title            | VARCHAR(200) | NOT NULL                 |
| description      | TEXT         | NOT NULL                 |
| required_skills  | VARCHAR(500) |                          |
| experience_min   | INT          |                          |
| experience_max   | INT          |                          |
| education_req    | VARCHAR(100) |                          |
| location         | VARCHAR(200) |                          |
| salary_min       | DECIMAL(12,2)|                          |
| salary_max       | DECIMAL(12,2)|                          |
| job_type         | ENUM         | 'FULL_TIME','PART_TIME','CONTRACT','INTERNSHIP','REMOTE' |
| status           | ENUM         | 'ACTIVE','CLOSED','FILLED','DRAFT' |
| deadline         | DATE         |                          |
| num_openings     | INT          | DEFAULT 1                |
| created_at       | TIMESTAMP    |                          |
| updated_at       | TIMESTAMP    |                          |

#### `applications`
| Column         | Type         | Constraints              |
|---------------|--------------|--------------------------|
| id            | BIGINT       | PK, AUTO_INCREMENT       |
| job_id        | BIGINT       | FK → jobs.id             |
| seeker_id     | BIGINT       | FK → users.id            |
| resume_id     | BIGINT       | FK → resumes.id          |
| cover_letter  | TEXT         |                          |
| status        | ENUM         | 'APPLIED','UNDER_REVIEW','SHORTLISTED','REJECTED','WITHDRAWN' |
| employer_comment | TEXT      |                          |
| withdraw_reason  | TEXT      |                          |
| applied_at    | TIMESTAMP    | DEFAULT CURRENT_TIMESTAMP|
| updated_at    | TIMESTAMP    |                          |

#### `application_notes`
| Column         | Type         | Constraints              |
|---------------|--------------|--------------------------|
| id            | BIGINT       | PK, AUTO_INCREMENT       |
| application_id| BIGINT       | FK → applications.id     |
| employer_id   | BIGINT       | FK → employers.id        |
| note          | TEXT         | NOT NULL                 |
| created_at    | TIMESTAMP    |                          |
| updated_at    | TIMESTAMP    |                          |

#### `favorites`
| Column     | Type      | Constraints              |
|-----------|-----------|--------------------------|
| id        | BIGINT    | PK, AUTO_INCREMENT       |
| seeker_id | BIGINT    | FK → users.id            |
| job_id    | BIGINT    | FK → jobs.id             |
| saved_at  | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP|

#### `notifications`
| Column     | Type         | Constraints              |
|-----------|--------------|--------------------------|
| id        | BIGINT       | PK, AUTO_INCREMENT       |
| user_id   | BIGINT       | FK → users.id            |
| message   | VARCHAR(500) | NOT NULL                 |
| type      | ENUM         | 'APPLICATION_UPDATE','JOB_RECOMMENDATION','SYSTEM' |
| is_read   | BOOLEAN      | DEFAULT FALSE            |
| link      | VARCHAR(500) |                          |
| created_at| TIMESTAMP    | DEFAULT CURRENT_TIMESTAMP|

### Relationships Summary
```
users (1) ──── (1) job_seeker_profiles
users (1) ──── (1) employers
job_seeker_profiles (1) ──── (N) educations
job_seeker_profiles (1) ──── (N) experiences
job_seeker_profiles (1) ──── (N) skills
job_seeker_profiles (1) ──── (N) certifications
job_seeker_profiles (1) ──── (N) resumes
employers (1) ──── (N) jobs
jobs (1) ──── (N) applications
users/seekers (1) ──── (N) applications
applications (1) ──── (N) application_notes
users/seekers (1) ──── (N) favorites
jobs (1) ──── (N) favorites
users (1) ──── (N) notifications
```

---

## Package Structure

```
src/main/java/com/revhire/
│
├── RevHireApplication.java                    ← Main class (Member F)
│
├── auth/                                      ← Member A
│   ├── controller/
│   │   └── AuthController.java                ← Returns Thymeleaf views
│   ├── dto/
│   │   ├── RegisterRequest.java
│   │   └── LoginRequest.java
│   ├── entity/
│   │   └── User.java
│   ├── repository/
│   │   └── UserRepository.java
│   ├── service/
│   │   ├── AuthService.java
│   │   └── AuthServiceImpl.java
│   └── security/
│       └── CustomUserDetailsService.java
│
├── profile/                                   ← Member B
│   ├── controller/
│   │   ├── ProfileController.java
│   │   └── ResumeController.java
│   ├── dto/
│   │   ├── ProfileRequest.java
│   │   ├── ProfileResponse.java
│   │   ├── EducationDto.java
│   │   ├── ExperienceDto.java
│   │   ├── SkillDto.java
│   │   └── CertificationDto.java
│   ├── entity/
│   │   ├── JobSeekerProfile.java
│   │   ├── Education.java
│   │   ├── Experience.java
│   │   ├── Skill.java
│   │   ├── Certification.java
│   │   └── Resume.java
│   ├── repository/
│   │   ├── ProfileRepository.java
│   │   ├── EducationRepository.java
│   │   ├── ExperienceRepository.java
│   │   ├── SkillRepository.java
│   │   ├── CertificationRepository.java
│   │   └── ResumeRepository.java
│   └── service/
│       ├── ProfileService.java
│       ├── ProfileServiceImpl.java
│       ├── ResumeService.java
│       └── ResumeServiceImpl.java
│
├── employer/                                  ← Member C + Member E
│   ├── controller/
│   │   ├── EmployerController.java            ← Member C
│   │   ├── ApplicantController.java           ← Member E
│   │   └── DashboardController.java           ← Member E
│   ├── dto/
│   │   ├── EmployerRequest.java               ← Member C
│   │   ├── EmployerResponse.java              ← Member C
│   │   ├── ApplicantResponse.java             ← Member E
│   │   ├── DashboardStats.java                ← Member E
│   │   └── NoteDto.java                       ← Member E
│   ├── entity/
│   │   ├── Employer.java                      ← Member C
│   │   └── ApplicationNote.java               ← Member E
│   ├── repository/
│   │   ├── EmployerRepository.java            ← Member C
│   │   └── ApplicationNoteRepository.java     ← Member E
│   └── service/
│       ├── EmployerService.java               ← Member C
│       ├── EmployerServiceImpl.java            ← Member C
│       ├── ApplicantService.java              ← Member E
│       ├── ApplicantServiceImpl.java           ← Member E
│       ├── DashboardService.java              ← Member E
│       └── DashboardServiceImpl.java           ← Member E
│
├── job/                                       ← Member C
│   ├── controller/
│   │   └── JobController.java
│   ├── dto/
│   │   ├── JobRequest.java
│   │   ├── JobResponse.java
│   │   └── JobSearchFilter.java
│   ├── entity/
│   │   └── Job.java
│   ├── repository/
│   │   └── JobRepository.java
│   ├── service/
│   │   ├── JobService.java
│   │   └── JobServiceImpl.java
│   └── specification/
│       └── JobSpecification.java              ← Member D uses this
│
├── application/                               ← Member D
│   ├── controller/
│   │   ├── ApplicationController.java
│   │   ├── JobSearchController.java
│   │   └── FavoriteController.java
│   ├── dto/
│   │   ├── ApplicationRequest.java
│   │   ├── ApplicationResponse.java
│   │   ├── WithdrawRequest.java
│   │   └── FavoriteResponse.java
│   ├── entity/
│   │   ├── Application.java
│   │   └── Favorite.java
│   ├── repository/
│   │   ├── ApplicationRepository.java
│   │   └── FavoriteRepository.java
│   └── service/
│       ├── ApplicationService.java
│       ├── ApplicationServiceImpl.java
│       ├── JobSearchService.java
│       ├── JobSearchServiceImpl.java
│       ├── FavoriteService.java
│       └── FavoriteServiceImpl.java
│
├── notification/                              ← Member F
│   ├── controller/
│   │   └── NotificationController.java
│   ├── dto/
│   │   └── NotificationResponse.java
│   ├── entity/
│   │   └── Notification.java
│   ├── repository/
│   │   └── NotificationRepository.java
│   └── service/
│       ├── NotificationService.java
│       └── NotificationServiceImpl.java
│
├── config/                                    ← Member A + Member F
│   ├── SecurityConfig.java                    ← Member A
│   ├── CorsConfig.java                        ← Member F
│   └── AppConfig.java                         ← Member F
│
├── exception/                                 ← Member F
│   ├── GlobalExceptionHandler.java
│   ├── ResourceNotFoundException.java
│   ├── BadRequestException.java
│   ├── UnauthorizedException.java
│   └── FileStorageException.java
│
└── common/                                    ← Member F
    ├── dto/
    │   ├── ApiResponse.java
    │   └── PagedResponse.java
    └── enums/
        ├── Role.java
        ├── ApplicationStatus.java
        ├── JobType.java
        ├── JobStatus.java
        └── NotificationType.java
```

### Thymeleaf Templates Structure (src/main/resources/)
```
src/main/resources/
│
├── application.properties
│
├── templates/                                  ← All Thymeleaf HTML files
│   │
│   ├── fragments/                              ← Member F (shared by all)
│   │   ├── layout.html                         ← Base layout (header, footer, nav)
│   │   ├── navbar.html                         ← Top navigation bar
│   │   ├── footer.html                         ← Footer
│   │   └── sidebar.html                        ← Dashboard sidebar
│   │
│   ├── auth/                                   ← Member A
│   │   ├── login.html
│   │   ├── register-choice.html                ← Choose: Seeker or Employer
│   │   ├── register-seeker.html
│   │   └── register-employer.html
│   │
│   ├── profile/                                ← Member B
│   │   ├── profile.html                        ← View own profile
│   │   ├── profile-edit.html                   ← Edit profile form
│   │   ├── resume-builder.html                 ← Textual resume form
│   │   ├── resume-upload.html                  ← File upload form
│   │   └── view-profile.html                   ← Public profile view
│   │
│   ├── employer/                               ← Member C + Member E
│   │   ├── company-profile.html                ← Member C
│   │   ├── company-edit.html                   ← Member C
│   │   ├── dashboard.html                      ← Member E
│   │   ├── applicant-list.html                 ← Member E
│   │   ├── applicant-detail.html               ← Member E
│   │   └── applicant-filter.html               ← Member E
│   │
│   ├── job/                                    ← Member C + Member D
│   │   ├── job-create.html                     ← Member C
│   │   ├── job-edit.html                       ← Member C
│   │   ├── job-detail.html                     ← Member C
│   │   ├── my-jobs.html                        ← Member C (employer's jobs)
│   │   ├── job-search.html                     ← Member D
│   │   └── job-search-results.html             ← Member D
│   │
│   ├── application/                            ← Member D
│   │   ├── apply-job.html                      ← Apply form
│   │   ├── my-applications.html                ← Seeker's application list
│   │   ├── application-detail.html             ← Single application view
│   │   └── favorites.html                      ← Saved jobs
│   │
│   ├── notification/                           ← Member F
│   │   └── notifications.html                  ← Notification list
│   │
│   ├── home.html                               ← Member F (landing page)
│   └── error.html                              ← Member F (error page)
│
└── static/                                     ← Static assets
    ├── css/
    │   └── style.css                           ← Member F (custom styles)
    ├── js/
    │   └── app.js                              ← Member F (custom scripts)
    └── images/
        └── logo.png
```

---

## API Endpoints (Per Module)

### Member A — Auth (`/auth`)
| Method | Endpoint               | Description                  | Returns              | Access   |
|--------|------------------------|------------------------------|----------------------|----------|
| GET    | `/auth/login`          | Show login page              | `auth/login.html`    | PUBLIC   |
| POST   | `/auth/login`          | Process login form           | Redirect to dashboard| PUBLIC   |
| GET    | `/auth/register`       | Show register choice page    | `auth/register-choice.html` | PUBLIC |
| GET    | `/auth/register/seeker`| Show seeker registration     | `auth/register-seeker.html` | PUBLIC |
| GET    | `/auth/register/employer`| Show employer registration | `auth/register-employer.html`| PUBLIC |
| POST   | `/auth/register`       | Process registration form    | Redirect to login    | PUBLIC   |
| GET    | `/auth/logout`         | Logout & invalidate session  | Redirect to login    | AUTH     |
| GET    | `/auth/me`             | Get current user info        | Profile page redirect| AUTH     |
| POST   | `/auth/password`       | Change password              | Success/error page   | AUTH     |

### Member B — Profile & Resume (`/profile`, `/resume`)
| Method | Endpoint                          | Description                    | Returns                    | Access   |
|--------|-----------------------------------|--------------------------------|----------------------------|----------|
| GET    | `/profile`                        | View my profile page           | `profile/profile.html`     | SEEKER   |
| GET    | `/profile/edit`                   | Show edit profile form         | `profile/profile-edit.html`| SEEKER   |
| POST   | `/profile`                        | Save/update profile            | Redirect to `/profile`     | SEEKER   |
| GET    | `/profile/{userId}`               | View a seeker's public profile | `profile/view-profile.html`| AUTH     |
| POST   | `/profile/education`              | Add education                  | Redirect to `/profile/edit`| SEEKER   |
| POST   | `/profile/education/{id}/update`  | Update education               | Redirect to `/profile/edit`| SEEKER   |
| POST   | `/profile/education/{id}/delete`  | Delete education               | Redirect to `/profile/edit`| SEEKER   |
| POST   | `/profile/experience`             | Add experience                 | Redirect to `/profile/edit`| SEEKER   |
| POST   | `/profile/experience/{id}/update` | Update experience              | Redirect to `/profile/edit`| SEEKER   |
| POST   | `/profile/experience/{id}/delete` | Delete experience              | Redirect to `/profile/edit`| SEEKER   |
| POST   | `/profile/skills`                 | Add skill                      | Redirect to `/profile/edit`| SEEKER   |
| POST   | `/profile/skills/{id}/delete`     | Delete skill                   | Redirect to `/profile/edit`| SEEKER   |
| POST   | `/profile/certifications`         | Add certification              | Redirect to `/profile/edit`| SEEKER   |
| POST   | `/profile/certifications/{id}/delete`| Delete certification        | Redirect to `/profile/edit`| SEEKER   |
| GET    | `/resume`                         | Show resume page               | `profile/resume-builder.html`| SEEKER |
| POST   | `/resume`                         | Save textual resume            | Redirect to `/resume`      | SEEKER   |
| GET    | `/resume/upload`                  | Show upload form               | `profile/resume-upload.html`| SEEKER  |
| POST   | `/resume/upload`                  | Upload resume file (PDF/DOCX)  | Redirect to `/resume`      | SEEKER   |
| GET    | `/resume/download/{id}`           | Download resume file           | File download              | AUTH     |

### Member C — Employer & Jobs (`/employers`, `/jobs`)
| Method | Endpoint                      | Description                    | Returns                        | Access    |
|--------|-------------------------------|--------------------------------|--------------------------------|-----------|
| GET    | `/employers/profile`          | View my company profile        | `employer/company-profile.html`| EMPLOYER  |
| GET    | `/employers/profile/edit`     | Show edit company form         | `employer/company-edit.html`   | EMPLOYER  |
| POST   | `/employers/profile`          | Save/update company profile    | Redirect to `/employers/profile`| EMPLOYER |
| GET    | `/employers/{id}`             | View company public page       | `employer/company-profile.html`| PUBLIC    |
| GET    | `/jobs/create`                | Show create job form           | `job/job-create.html`          | EMPLOYER  |
| POST   | `/jobs`                       | Save new job posting           | Redirect to `/jobs/my`         | EMPLOYER  |
| GET    | `/jobs/{id}`                  | View job detail page           | `job/job-detail.html`          | PUBLIC    |
| GET    | `/jobs/{id}/edit`             | Show edit job form             | `job/job-edit.html`            | EMPLOYER  |
| POST   | `/jobs/{id}/update`           | Update job posting             | Redirect to `/jobs/{id}`       | EMPLOYER  |
| POST   | `/jobs/{id}/delete`           | Delete job posting             | Redirect to `/jobs/my`         | EMPLOYER  |
| POST   | `/jobs/{id}/close`            | Close job posting              | Redirect to `/jobs/my`         | EMPLOYER  |
| POST   | `/jobs/{id}/reopen`           | Reopen job posting             | Redirect to `/jobs/my`         | EMPLOYER  |
| POST   | `/jobs/{id}/fill`             | Mark job as filled             | Redirect to `/jobs/my`         | EMPLOYER  |
| GET    | `/jobs/my`                    | My job postings list           | `job/my-jobs.html`             | EMPLOYER  |
| GET    | `/jobs/{id}/stats`            | Job statistics page            | Fragment / JSON                | EMPLOYER  |

### Member D — Search & Applications (`/jobs/search`, `/applications`, `/favorites`)
| Method | Endpoint                           | Description                        | Returns                              | Access   |
|--------|------------------------------------|------------------------------------|--------------------------------------|----------|
| GET    | `/jobs/search`                     | Show search page with filters      | `job/job-search.html`                | PUBLIC   |
| GET    | `/jobs/search/results`             | Search results with filters        | `job/job-search-results.html`        | PUBLIC   |
| GET    | `/applications/apply/{jobId}`      | Show apply form                    | `application/apply-job.html`         | SEEKER   |
| POST   | `/applications/apply/{jobId}`      | Submit application                 | Redirect to `/applications`          | SEEKER   |
| GET    | `/applications`                    | My applications list               | `application/my-applications.html`   | SEEKER   |
| GET    | `/applications/{id}`               | Application detail view            | `application/application-detail.html`| SEEKER   |
| POST   | `/applications/{id}/withdraw`      | Withdraw application               | Redirect to `/applications`          | SEEKER   |
| POST   | `/favorites/{jobId}`               | Save job to favorites              | Redirect back                        | SEEKER   |
| POST   | `/favorites/{jobId}/remove`        | Remove from favorites              | Redirect back                        | SEEKER   |
| GET    | `/favorites`                       | Favorite jobs list                 | `application/favorites.html`         | SEEKER   |

### Member E — Applicant Management & Dashboard (`/employer`)
| Method | Endpoint                                        | Description                    | Returns                              | Access    |
|--------|-------------------------------------------------|--------------------------------|--------------------------------------|-----------|
| GET    | `/employer/dashboard`                           | Employer dashboard page        | `employer/dashboard.html`            | EMPLOYER  |
| GET    | `/employer/jobs/{jobId}/applicants`             | Applicant list for a job       | `employer/applicant-list.html`       | EMPLOYER  |
| GET    | `/employer/applicants/{appId}`                  | Applicant full detail view     | `employer/applicant-detail.html`     | EMPLOYER  |
| POST   | `/employer/applicants/{appId}/shortlist`        | Shortlist an applicant         | Redirect to applicant list           | EMPLOYER  |
| POST   | `/employer/applicants/{appId}/reject`           | Reject an applicant            | Redirect to applicant list           | EMPLOYER  |
| POST   | `/employer/applicants/bulk-shortlist`           | Bulk shortlist (form submit)   | Redirect to applicant list           | EMPLOYER  |
| POST   | `/employer/applicants/bulk-reject`              | Bulk reject (form submit)      | Redirect to applicant list           | EMPLOYER  |
| GET    | `/employer/jobs/{jobId}/applicants/filter`      | Filter applicants page         | `employer/applicant-filter.html`     | EMPLOYER  |
| POST   | `/employer/notes`                               | Add note to application        | Redirect to applicant detail         | EMPLOYER  |
| POST   | `/employer/notes/{id}/update`                   | Update note                    | Redirect to applicant detail         | EMPLOYER  |
| POST   | `/employer/notes/{id}/delete`                   | Delete note                    | Redirect to applicant detail         | EMPLOYER  |

### Member F — Notifications & Common Pages (`/notifications`, `/`)
| Method | Endpoint                               | Description                  | Returns                            | Access |
|--------|-----------------------------------------|------------------------------|---------------------------------------|--------|
| GET    | `/`                                    | Landing / Home page          | `home.html`                           | PUBLIC |
| GET    | `/notifications`                       | Notifications list page      | `notification/notifications.html`     | AUTH   |
| GET    | `/notifications/unread-count`          | Get unread count (AJAX)      | JSON `{count: N}`                     | AUTH   |
| POST   | `/notifications/{id}/read`             | Mark as read                 | Redirect to `/notifications`          | AUTH   |
| POST   | `/notifications/read-all`              | Mark all as read             | Redirect to `/notifications`          | AUTH   |
| POST   | `/notifications/{id}/delete`           | Delete a notification        | Redirect to `/notifications`          | AUTH   |

---

## Thymeleaf Key Concepts (For the Team)

### How Controllers Return Views (NOT JSON)
```java
// BEFORE (REST API style — DON'T do this with Thymeleaf)
@RestController
public class JobController {
    @GetMapping("/api/jobs/{id}")
    public ResponseEntity<Job> getJob(@PathVariable Long id) {
        return ResponseEntity.ok(jobService.findById(id));
    }
}

// AFTER (Thymeleaf style — DO this)
@Controller  // NOT @RestController
public class JobController {
    @GetMapping("/jobs/{id}")
    public String getJob(@PathVariable Long id, Model model) {
        model.addAttribute("job", jobService.findById(id));
        return "job/job-detail";  // → templates/job/job-detail.html
    }
}
```

### Thymeleaf Template Example
```html
<!-- templates/job/job-detail.html -->
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title th:text="${job.title}">Job Title</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
    <link rel="stylesheet" th:href="@{/css/style.css}">
</head>
<body>
    <!-- Include navbar fragment -->
    <div th:replace="~{fragments/navbar :: navbar}"></div>

    <div class="container mt-4">
        <h1 th:text="${job.title}">Job Title</h1>
        <p th:text="${job.description}">Description</p>
        <span class="badge bg-primary" th:text="${job.jobType}">Full Time</span>
        <p>Salary: <span th:text="${job.salaryMin}">0</span> - <span th:text="${job.salaryMax}">0</span></p>

        <!-- Show apply button only if user is a seeker -->
        <a th:if="${#authorization.expression('hasRole(''SEEKER'')')}" 
           th:href="@{/applications/apply/{id}(id=${job.id})}" 
           class="btn btn-success">Apply Now</a>
    </div>

    <div th:replace="~{fragments/footer :: footer}"></div>
</body>
</html>
```

### Shared Layout Fragment (Member F creates this)
```html
<!-- templates/fragments/navbar.html -->
<nav th:fragment="navbar" class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container">
        <a class="navbar-brand" href="/">RevHire</a>
        <div class="navbar-nav ms-auto">
            <a th:if="${#authorization.expression('isAuthenticated()')}" 
               class="nav-link" th:href="@{/notifications}">
                Notifications <span class="badge bg-danger" id="notif-count"></span>
            </a>
            <a th:unless="${#authorization.expression('isAuthenticated()')}" 
               class="nav-link" th:href="@{/auth/login}">Login</a>
        </div>
    </div>
</nav>
```

### Form Submission Example
```html
<!-- templates/auth/login.html -->
<form th:action="@{/auth/login}" method="post">
    <div class="mb-3">
        <label>Email</label>
        <input type="email" name="email" class="form-control" required>
    </div>
    <div class="mb-3">
        <label>Password</label>
        <input type="password" name="password" class="form-control" required>
    </div>
    <p th:if="${error}" class="text-danger" th:text="${error}">Error message</p>
    <button type="submit" class="btn btn-primary">Login</button>
</form>
```

### Key Thymeleaf Syntax Cheatsheet
| Syntax | Purpose | Example |
|--------|---------|--------|
| `th:text` | Display text | `<p th:text="${user.name}">Name</p>` |
| `th:href` | Dynamic links | `<a th:href="@{/jobs/{id}(id=${job.id})}">` |
| `th:each` | Loop | `<tr th:each="job : ${jobs}">` |
| `th:if` | Conditional | `<div th:if="${user.role == 'SEEKER'}">` |
| `th:unless` | Negative conditional | `<div th:unless="${jobs.empty}">` |
| `th:action` | Form action URL | `<form th:action="@{/auth/login}">` |
| `th:object` | Bind form object | `<form th:object="${job}">` |
| `th:field` | Bind form field | `<input th:field="*{title}">` |
| `th:replace` | Include fragment | `<div th:replace="~{fragments/navbar :: navbar}">` |
| `@{}` | URL expression | `th:href="@{/css/style.css}"` |
| `${}` | Variable expression | `th:text="${job.title}"` |
| `*{}` | Selection expression | `th:field="*{email}"` (inside th:object) |

---

## Entity Definitions

### Member A creates:

```java
@Entity
@Table(name = "users")
public class User {
    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    @Column(unique = true, nullable = false)
    private String email;
    @Column(nullable = false)
    private String password;
    private String phone;
    private String location;
    @Enumerated(EnumType.STRING)
    private Role role;  // SEEKER, EMPLOYER
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;
}
```

**Spring Security Config (Session-based for Thymeleaf):**
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/", "/auth/**", "/css/**", "/js/**", "/images/**").permitAll()
                .requestMatchers("/jobs/search/**", "/jobs/{id}", "/employers/{id}").permitAll()
                .requestMatchers("/profile/**", "/resume/**", "/applications/**", "/favorites/**").hasRole("SEEKER")
                .requestMatchers("/employer/**", "/jobs/create", "/jobs/my").hasRole("EMPLOYER")
                .anyRequest().authenticated()
            )
            .formLogin(form -> form
                .loginPage("/auth/login")
                .defaultSuccessUrl("/", true)
                .failureUrl("/auth/login?error=true")
                .permitAll()
            )
            .logout(logout -> logout
                .logoutUrl("/auth/logout")
                .logoutSuccessUrl("/auth/login?logout=true")
                .permitAll()
            );
        return http.build();
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
}
```

### Member B creates:

```java
@Entity
public class JobSeekerProfile {
    @Id @GeneratedValue private Long id;
    @OneToOne @JoinColumn(name = "user_id") private User user;
    private String headline;
    private String summary;
    private String currentEmploymentStatus;
    @OneToMany(mappedBy = "profile", cascade = ALL) private List<Education> educations;
    @OneToMany(mappedBy = "profile", cascade = ALL) private List<Experience> experiences;
    @OneToMany(mappedBy = "profile", cascade = ALL) private List<Skill> skills;
    @OneToMany(mappedBy = "profile", cascade = ALL) private List<Certification> certifications;
}

@Entity
public class Resume {
    @Id @GeneratedValue private Long id;
    @ManyToOne @JoinColumn(name = "profile_id") private JobSeekerProfile profile;
    private String objective;
    private String fileName;
    private String fileType;
    @Lob private byte[] fileData;
    private Long fileSize;
    private LocalDateTime createdAt;
}
```

### Member C creates:

```java
@Entity
public class Employer {
    @Id @GeneratedValue private Long id;
    @OneToOne @JoinColumn(name = "user_id") private User user;
    private String companyName;
    private String industry;
    private String companySize;
    private String description;
    private String website;
    private String location;
}

@Entity
public class Job {
    @Id @GeneratedValue private Long id;
    @ManyToOne @JoinColumn(name = "employer_id") private Employer employer;
    private String title;
    private String description;
    private String requiredSkills;
    private Integer experienceMin;
    private Integer experienceMax;
    private String educationReq;
    private String location;
    private BigDecimal salaryMin;
    private BigDecimal salaryMax;
    @Enumerated(EnumType.STRING) private JobType jobType;
    @Enumerated(EnumType.STRING) private JobStatus status;
    private LocalDate deadline;
    private Integer numOpenings;
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;
}
```

### Member D creates:

```java
@Entity
public class Application {
    @Id @GeneratedValue private Long id;
    @ManyToOne @JoinColumn(name = "job_id") private Job job;
    @ManyToOne @JoinColumn(name = "seeker_id") private User seeker;
    @ManyToOne @JoinColumn(name = "resume_id") private Resume resume;
    private String coverLetter;
    @Enumerated(EnumType.STRING) private ApplicationStatus status;
    private String employerComment;
    private String withdrawReason;
    private LocalDateTime appliedAt;
    private LocalDateTime updatedAt;
}

@Entity
public class Favorite {
    @Id @GeneratedValue private Long id;
    @ManyToOne @JoinColumn(name = "seeker_id") private User seeker;
    @ManyToOne @JoinColumn(name = "job_id") private Job job;
    private LocalDateTime savedAt;
}
```

### Member E creates:

```java
@Entity
public class ApplicationNote {
    @Id @GeneratedValue private Long id;
    @ManyToOne @JoinColumn(name = "application_id") private Application application;
    @ManyToOne @JoinColumn(name = "employer_id") private Employer employer;
    private String note;
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;
}
```

### Member F creates:

```java
@Entity
public class Notification {
    @Id @GeneratedValue private Long id;
    @ManyToOne @JoinColumn(name = "user_id") private User user;
    private String message;
    @Enumerated(EnumType.STRING) private NotificationType type;
    private Boolean isRead = false;
    private String link;
    private LocalDateTime createdAt;
}
```

---

## Build Order & Timeline

```
┌──────────────────────────────────────────────────────────────────┐
│  WEEK 1 (Days 1-2): PHASE 0 — Project Setup                      │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │  Member F: Spring Boot project, Maven, DB config, packages │  │
│  │  Member A: Start User entity + Auth service                │  │
│  │  ALL: Clone repo, set up local MySQL, draw ERD together    │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                  │
│  WEEK 1 (Days 3-7): PHASE 1 — Auth must be done                  │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │  Member A: Complete Auth (register, login, session, security) │  │
│  │  Member F: Exception handling, common DTOs, enums, Log4J   │  │
│  │  Member B: Start entities (profile, education, etc.)       │  │
│  │  Member C: Start entities (employer, job)                  │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                  │
│  WEEK 2: PHASE 2 — Profiles & Jobs (parallel)                    │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │  Member B: Profile CRUD, Resume builder, File upload       │  │
│  │  Member C: Employer CRUD, Job CRUD, Job lifecycle          │  │
│  │  Member A: Help with security role checks on endpoints     │  │
│  │  Member F: Start notification entity & service             │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                  │
│  WEEK 3: PHASE 3 — Search & Applications (parallel)              │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │  Member D: Job search, Apply, Track, Withdraw, Favorites   │  │
│  │  Member E: View applicants, Shortlist/Reject, Dashboard    │  │
│  │  Member F: Wire notifications to application status        │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                  │
│  WEEK 4: PHASE 4 — Polish & Delivery                             │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │  ALL: Write remaining JUnit tests                          │  │
│  │  ALL: Add Log4J logging to all services                    │  │
│  │  Member F: ERD diagram, Architecture diagram, README       │  │
│  │  ALL: Integration testing, bug fixes, code review          │  │
│  │  ALL: Final demo preparation                              │  │
│  └────────────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────────────┘
```

### Dependency Chain
```
Auth (Member A) → must finish first
       ↓
Profile (Member B) + Employer/Job (Member C) → can run parallel
       ↓
Search/Apply (Member D) + Applicant Mgmt (Member E) → need B & C done
       ↓
Notifications (Member F) → needs D & E events to trigger
```

---

## Git Workflow

### Branch Strategy
```
main (protected — no direct pushes)
 ├── develop (integration branch)
 │    ├── feature/auth           ← Member A
 │    ├── feature/profile        ← Member B
 │    ├── feature/job            ← Member C
 │    ├── feature/application    ← Member D
 │    ├── feature/dashboard      ← Member E
 │    └── feature/notification   ← Member F
 └── release/v1.0 (final)
```

### Daily Workflow for Each Member
```bash
# 1. Start of day — pull latest develop
git checkout develop
git pull origin develop

# 2. Switch to your feature branch & merge develop
git checkout feature/your-module
git merge develop

# 3. Code, commit frequently
git add .
git commit -m "feat(auth): add session-based login"

# 4. Push your branch
git push origin feature/your-module

# 5. When feature is ready — create Pull Request to develop
#    - Get at least 1 teammate to review
#    - Fix review comments
#    - Merge PR
```

### Commit Message Format
```
feat(module): description     ← new feature
fix(module): description      ← bug fix
test(module): description     ← adding tests
docs(module): description     ← documentation
refactor(module): description ← code restructure

Examples:
feat(auth): add user registration endpoint
feat(profile): implement resume file upload
fix(job): fix salary range filter query
test(application): add service layer unit tests
docs(readme): add API documentation
```

---

## Shared Responsibilities (ALL 6 Members)

| Task | Details |
|------|---------|
| **JUnit 4 Tests** | Each member writes tests for their own module (Service layer minimum) |
| **Log4J Logging** | Add `logger.info()`, `logger.error()`, `logger.debug()` in every service method |
| **DTOs** | Never expose entities directly in API responses — always use DTOs |
| **Validation** | Use `@Valid`, `@NotBlank`, `@Email`, `@Size` on request DTOs |
| **Error Handling** | Throw custom exceptions, Member F's `@ControllerAdvice` catches them |
| **Code Reviews** | Review at least 1 PR per day from a teammate |
| **Documentation** | Add Javadoc comments to service methods |

### Logging Standard (Log4J)
```java
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;

@Service
public class JobServiceImpl implements JobService {
    private static final Logger logger = LogManager.getLogger(JobServiceImpl.class);

    public Job createJob(JobRequest request) {
        logger.info("Creating new job posting: {}", request.getTitle());
        // ... logic
        logger.info("Job created successfully with ID: {}", job.getId());
        return job;
    }
}
```

### Testing Standard (JUnit 4)
```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class JobServiceTest {

    @MockBean
    private JobRepository jobRepository;

    @Autowired
    private JobService jobService;

    @Test
    public void testCreateJob_Success() {
        // Arrange
        // Act
        // Assert
    }

    @Test(expected = BadRequestException.class)
    public void testCreateJob_InvalidData_ThrowsException() {
        // ...
    }
}
```

---

## Definition of Done Checklist

### Code Deliverables
- [ ] All 6 modules implemented and working
- [ ] All endpoints tested via Postman/curl
- [ ] JUnit 4 tests written for all service layers
- [ ] Log4J logging implemented in all services
- [ ] Global exception handling working
- [ ] Role-based access control enforced
- [ ] DTOs used for all API request/response
- [ ] Input validation on all endpoints

### Documentation Deliverables
- [ ] ERD (Entity Relationship Diagram) — draw.io or dbdiagram.io
- [ ] Application Architecture Diagram — showing layers (Controller → Service → Repository → DB)
- [ ] README.md with:
  - [ ] Project description
  - [ ] Tech stack
  - [ ] How to run locally
  - [ ] API endpoint summary
  - [ ] Team members & modules
- [ ] Testing Artifacts (test reports, coverage summary)

### Repository Requirements
- [ ] Clean Git history with meaningful commits
- [ ] Feature branches merged via Pull Requests
- [ ] No secrets/passwords in code (use application.properties or env variables)
- [ ] `.gitignore` properly configured

### Demo Requirements
- [ ] Working web application demonstration
- [ ] Job Seeker flow: Register → Profile → Search → Apply → Track
- [ ] Employer flow: Register → Post Job → View Applicants → Shortlist/Reject
- [ ] Notifications working on status changes

---

## Quick Reference Card

| Who | Creates What | Depends On | Branch |
|-----|-------------|------------|--------|
| **Member A** | User, Auth, Security, Login/Register pages | Nothing (starts first) | `feature/auth` |
| **Member B** | Profile, Education, Experience, Skill, Certification, Resume + profile pages | Auth (Member A) | `feature/profile` |
| **Member C** | Employer, Job + job/company pages | Auth (Member A) | `feature/job` |
| **Member D** | Application, Favorite, Job Search + search/apply pages | Auth + Job + Profile (A, C, B) | `feature/application` |
| **Member E** | ApplicationNote, Dashboard, Applicant Mgmt + dashboard/applicant pages | Auth + Job + Application (A, C, D) | `feature/dashboard` |
| **Member F** | Notification, Exceptions, Common, Layout fragments, Home page | All modules (integrates last) | `feature/notification` |

---

*Document created: February 20, 2026*
*Project: RevHire (P2)*
*Team Size: 6 Members*
