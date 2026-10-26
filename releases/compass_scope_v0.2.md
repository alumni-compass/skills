# COMPASS Product Requirements — Version 0.2

**Document type:** Product Requirements Document  
**Source:** `COMPASS_Version_0.2.pdf`  
**Purpose:** Product scope, functional requirements, acceptance criteria, and release expectations for team planning.

## 1. Executive Summary

Version 0.2 advances COMPASS from an information-focused website into a practical alumni engagement platform. It retains the four Version 0.1 pages—Landing Page, Home Page, Alumni Directory, and About the Association—and adds:

- A community newsfeed with administrator approval before publication.
- Event management, registration, ticketing, payment, waitlists, and check-in.
- Career listings, internal applications, and referral workflows.

The experiences should let alumni discover what is happening, participate in the community, attend events, and pursue career opportunities. They share profiles and permissions while protecting private information and giving administrators clear control.

## 2. Product Objectives

- Increase meaningful participation through trusted, useful content.
- Make event discovery, registration, payment, ticket access, and check-in one coherent journey.
- Help alumni discover opportunities, request referrals, apply through COMPASS, and understand application status.
- Reduce administrative effort with centralized review queues, event controls, and career workflows.
- Build on Version 0.1 navigation, alumni data, authentication, role-based access control (RBAC), design system, and deployment foundation.

## 3. Scope and Boundaries

### 3.1 Included in Version 0.2

- Retain and maintain the Landing Page, Home Page, Alumni Directory, and About the Association.
- Community newsfeed with alumni submissions, mandatory administrator approval before publication, reactions, and comments.
- Event management, free and paid tickets, payment processing, capacity management, waitlists, QR tickets, check-in, notifications, and reports.
- Job and internship listings, search and filtering, internal applications and tracking, referral requests, and referral status tracking.
- Home Page previews for upcoming events, recent approved community posts, and featured opportunities.
- Shared security, privacy, notifications, audit logging, responsive design, accessibility, and error handling.

### 3.2 Out of Scope Unless Separately Approved

- Mentorship scheduling, fundraising, digital alumni cards, marketplace, entrepreneurship ecosystem, and universal CMS.
- Automated social media publishing, AI recommendations or content generation, gamification, and advanced analytics.
- Anonymous or unmoderated posting, public access to private applications or attendee records, and automated hiring decisions.

## 4. Users, Roles, and Permissions

| Role | Capabilities |
|---|---|
| Public visitor | View public pages, approved public posts, published events, and public job listings. Cannot post, react, comment, register for member-only experiences, or access private records. |
| Alumni | Submit posts for approval; react to and comment on approved posts; register for events and access their own tickets; apply for jobs and view their own applications; request referrals. |
| Administrator | Moderate content by reviewing, approving, rejecting, and removing posts and comments. May also manage events, jobs, applications, and reports based on assigned permissions. |
| Event manager | Manage assigned events, ticket types, capacity, waitlists, attendee lists, check-in, cancellations, and event reports. |
| Career manager | Manage permitted job listings and review applications associated with those listings. |
| Super administrator | Manage platform configuration, role assignments, permissions, and exceptional administrative access. Retains platform-level control. |

Administrative capabilities may be granted through permissions, allowing one administrator to manage multiple areas. Every protected action must be authorized by backend APIs, not merely hidden in the interface.

## 5. Community Newsfeed

### 5.1 Experience and Functional Requirements

- Authenticated alumni can submit text posts with supported images and links.
- Every new post enters **Pending Approval**. Until approved, it is hidden from the normal feed, public pages, search results, and Home Page previews.
- Administrators can approve or reject submissions and optionally provide a reason visible to the author.
- Authors can see their post status: Pending Approval, Approved, Rejected, or Removed. Drafts may be supported if needed by the final design.
- Approved posts appear chronologically. Administrators may feature or pin selected approved posts.
- Authenticated alumni can react to and comment on approved posts.
- Authors can edit or delete their own posts and comments, subject to the workflow. Editing an approved post requires re-approval before the revised content is published.
- Administrators can remove published posts or comments that violate association policy.
- User-facing report-post and report-comment features are not included in Version 0.2.
- Provide pagination or incremental loading, supported image formats and limits, safe link handling, and clear loading, empty, validation, and error states.

### 5.2 Acceptance Criteria

- **NF-01:** A valid post submission records its author, submission time, and Pending Approval status.
- **NF-02:** Pending and rejected posts are not exposed in the normal feed, public pages, search results, or Home Page previews.
- **NF-03:** Only an administrator with content-moderation permission can approve or reject a post.
- **NF-04:** Once approved, a post becomes visible without code redeployment, and the author can see the updated status.
- **NF-05:** A rejected post remains unpublished; the author can see its status and any configured reason.
- **NF-06:** Editing an approved post creates a pending revision. The previous approved version remains visible until the revision is approved, unless an administrator removes it.
- **NF-07:** Only authenticated users can react or comment. A user cannot create duplicate active reactions on the same post.
- **NF-08:** Users can edit or delete only their own content unless an administrator has the required permission.
- **NF-09:** Content removed by an administrator is no longer visible in the normal feed, and the action is audit logged.
- **NF-10:** Invalid submissions and unsupported uploads show a clear error and never publish content accidentally.

## 6. Events, Registration, and Ticketing

### 6.1 Functional Requirements

- Authorized administrators or event managers can create, edit, preview, publish, unpublish, and cancel events.
- Event details include title, description, category, date and time, timezone, venue or online details, organizer/contact, capacity, registration deadline, and cancellation terms.
- Support free and paid ticket types, configured ticket limits, and event capacity.
- Authenticated users can register, see registration status, access tickets, and cancel where event policy allows.
- Paid registration uses an approved payment provider. Payment and registration states stay consistent, including delayed or duplicate provider callbacks.
- Issue a unique QR ticket only after successful free registration or confirmed payment for a paid ticket.
- When capacity is reached, eligible users can join a waitlist. Promotion order, offer expiry, and payment deadline must be configurable or explicitly defined.
- Authorized event staff can scan and validate QR tickets at check-in. Clearly identify invalid or already-used tickets.
- Send relevant registration confirmations, payment outcomes, waitlist offers, cancellations, and event reminders.
- Provide reports for registrations, cancellations, waitlist conversion, payment status, and attendance.

### 6.2 Acceptance Criteria

- **EV-01:** Only published events open for registration accept new registrations.
- **EV-02:** Capacity cannot be exceeded, including when multiple users attempt to register simultaneously.
- **EV-03:** A free ticket is issued only after registration succeeds and is marked as no payment required by the admin.
- **EV-04:** A paid ticket becomes valid only after payment is confirmed successful. Pending or failed payments do not produce valid paid tickets.
- **EV-05:** Duplicate payment notifications are handled idempotently and do not create duplicate tickets or financial transactions.
- **EV-06:** When capacity is reached, eligible users can join the waitlist and see their status.
- **EV-07:** Waitlist offers follow the defined ordering and expiry policy. An expired offer allows the next eligible user to be considered.
- **EV-08:** QR validation checks ticket authenticity, event association, registration/payment state, and cancellation state.
- **EV-09:** A ticket can be checked in only once. A second scan returns a clear already-checked-in result.
- **EV-10:** Unauthorized users cannot access full attendee lists, private attendee data, or event financial reports.
- **EV-11:** Cancellation and refund outcomes are recorded and communicated to the affected registrant.
- **EV-12:** Reports distinguish registrations, paid tickets, cancellations, waitlisted users, checked-in attendees, and non-attendees.

## 7. Careers: Jobs, Referrals, and Applications

### 7.1 Functional Requirements

- Authorized career managers can create, edit, publish, close, and expire job and internship listings.
- Listings include title, company, location, work mode, employment type, description, requirements, deadline, and referral availability.
- Alumni can search and filter active opportunities and save jobs for later.
- Applicants can apply inside COMPASS using their core profile, resume, and configured job-specific fields.
- Applicants can view their own applications and current status. Authorized reviewers can view applications only for jobs they are permitted to manage.
- Use a defined application status lifecycle. Suggested statuses are Submitted, In Review, Shortlisted, Interview, Offered, Rejected, Withdrawn, and Closed. Confirm the final set before implementation.
- Alumni can opt in to be available referrers. Applicants can request referrals for eligible jobs where referrals are offered.
- Referrers can accept or decline requests and record whether a referral has been submitted. Applicants can track referral status.
- Notify applicants and referrers about relevant status changes without exposing confidential reviewer notes.
- Protect resume files, contact information, application answers, and referral records from unauthorized access.

### 7.2 Acceptance Criteria

- **CR-01:** Users can search and filter active, published job listings.
- **CR-02:** Closed or expired listings cannot receive new applications unless an authorized user reopens them.
- **CR-03:** An eligible applicant can submit a complete application and receives confirmation with an application reference and status.
- **CR-04:** Duplicate applications for the same job are prevented unless a defined resubmission policy permits them.
- **CR-05:** Applicants can access only their own application records; reviewers can access only applications within their assigned scope.
- **CR-06:** Every application status change is validated, timestamped, and attributed to the acting user or system process.
- **CR-07:** Applicants can see appropriate status updates and notifications but cannot see confidential internal reviewer notes.
- **CR-08:** Referral requests can be made only for eligible jobs and available referrers.
- **CR-09:** Referrers can accept or decline a request; the decision and subsequent referral-submitted state are recorded.
- **CR-10:** Unauthorized users cannot impersonate another applicant or referrer or change workflow states through direct API requests.
- **CR-11:** A job owner cannot access unrelated job applications without broader career-management permission.

## 8. Home Page and Cross-Module Experience

- **Upcoming Events:** Show date, location or format, and a clear event-details/register action.
- **Community Updates:** Show approved posts only, with links to the full post/feed.
- **Featured Careers:** Show active job opportunities with a clear view/apply action.
- **My Activity** for authenticated alumni: show their post approval status, upcoming registrations/tickets, saved jobs, and application updates.
- Keep the Home Page as a summary and launch point; full workflows belong in their dedicated experiences.
- Use a single source of truth for alumni profiles, posts, events, tickets, jobs, applications, and referrals.

## 9. Shared Product and Technical Requirements

### 9.1 Access Control, Privacy, and Auditability

- Enforce role- and record-level authorization on every protected backend operation.
- Default to privacy for alumni profile fields, attendee information, applications, resumes, and referrals.
- Store payment credentials securely; do not store raw payment-card data in COMPASS.
- Validate uploaded files and safely handle user-submitted links and content.
- Audit administrator approvals, rejections, and removals; role changes; event and payment state changes; check-in actions; and application/referral transitions.
- Define retention and deletion rules for posts, resumes, applications, payment references, and audit records.

### 9.2 Reliability, Accessibility, and Operations

- Support mobile, tablet, and desktop layouts with keyboard-accessible controls and readable contrast.
- Provide clear loading, empty, validation, permission-denied, and failure states across modules.
- Make notifications retry-safe and avoid exposing private information in email or in-app previews.
- Display event timezones and payment currency/amounts clearly and consistently.
- Document production configuration, backups, monitoring, and rollback procedures.

## 10. Release Acceptance Criteria

- All four Version 0.1 pages remain functional, navigable, and visually consistent.
- Every new community post requires administrator approval before publication; edits to approved posts require re-approval.
- Post/comment reporting is not implemented in Version 0.2.
- Free and paid event registration works end to end; paid tickets require confirmed payment.
- Capacity controls, waitlist promotion, QR validation, and duplicate check-in protection pass tests.
- Job applications and referrals follow valid status transitions and enforce record-level permissions.
- Backend authorization tests cover allowed and denied actions for every role and module.
- Private data is not exposed through public pages, Home Page previews, notifications, URLs, or logs.
- Core user journeys have repeatable end-to-end tests, including payment failure, cancellation, expired waitlist offers, and unauthorized access.
- Operational readiness includes production configuration, backups, monitoring, and a tested rollback approach.

## 11. Success Metrics

- **Community engagement:** Posts submitted; median approval turnaround; approved-post views; comments and reactions per active user; repeat contributors.
- **Events:** Event-page-to-registration conversion; payment success rate; waitlist-to-registration conversion; attendance rate; QR check-in failure rate.
- **Careers:** Active job listings; job-view-to-application conversion; completed applications; referral acceptance/submission rate; time to application status update.
- **Product quality:** Task completion rate; authorization defects; payment reconciliation exceptions; failed notifications; mobile usability issues.

## 12. Decisions to Confirm Before Implementation

- **Alumni eligibility:** Does posting require verified alumni status, or is any authenticated alumni account sufficient? Recommended default: verified alumni if reliable verification data exists.
- **Post review service level:** Who covers the approval queue, what is the expected review turnaround, and who is the backup administrator?
- **Comment policy:** Recommended default: comments on approved posts appear immediately for authenticated alumni, with administrator removal controls. Confirm whether comments also need pre-approval.
- **Payments and refunds:** Confirm provider, supported currency, payment expiry, cancellation cut-off, refund rules, reconciliation ownership, and delayed/failed callback handling.
- **Waitlist rules:** Confirm eligibility, ordering, offer window, promotion behavior, and payment deadline after an offer.
- **Event eligibility:** Confirm whether guests can register and whether a member can register multiple attendees.
- **Application requirements:** Confirm mandatory fields, resume file types/limits, final status list, reviewer permissions, and data-retention policy.
- **Referral rules:** Confirm who can opt in, how applicants request a referrer, and what qualifies as a completed referral.
- **Notifications:** Confirm in-app/email channels, templates, retry behavior, and triggering events.

## 13. Product Management Recommendation

The value of Version 0.2 is the connected experience: an alumnus discovers a post, event, or career opportunity; takes action; and tracks the outcome in the same portal. Keep the release focused on trust and completion. Administrator-controlled publishing, payment-to-ticket reliability, accurate attendance, and confidential application tracking are release-critical.

Prioritize a usable administrator workspace, My COMPASS activity, profile reuse, saved jobs, and lightweight event feedback. Treat these as focused usability improvements rather than expanding into AI, gamification, or broad social integrations.
