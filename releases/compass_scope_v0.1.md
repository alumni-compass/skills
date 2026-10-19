# RIT Alumni Association Portal — Version 0.1 Scope

## 1. Objective

Build the first version of the RIT Alumni Association portal with four core pages:

1. Landing Page
2. Home Page
3. Alumni Directory
4. About the Association

Keep Version 0.1 focused on these pages and the shared requirements needed to support them.

## 2. Scope

### 2.1 Landing Page

- Present RIT Alumni Association branding and a clear welcome message.
- Provide clear navigation to the portal's main pages.
- Include a primary call to action that directs visitors into the portal.
- Support mobile, tablet, and desktop layouts.

### 2.2 Home Page

- Provide a simple, attractive overview of the association.
- Show a short introduction, key statistics, and selected highlights where data is available.
- Optionally show a preview of the alumni map and featured alumni.
- Link visitors to the full Alumni Directory and About the Association pages.
- Avoid duplicating the full content of the About the Association page.

### 2.3 Alumni Directory

- Display approved alumni profile information.
- Support search and filtering by agreed fields, such as name, department, graduation year, company/designation, and location.
- Display results as profile cards or a clear list, with pagination when needed.
- Use the same approved alumni dataset as any alumni map or statistics shown elsewhere.
- Respect privacy rules and show only fields approved for public display.
- Do not include alumni self-registration or self-service profile editing in Version 0.1 unless separately approved.

### 2.4 About the Association

- Present the association's background, history, mission, vision, leadership, activities, and contact information as content is provided and approved.
- Provide an admin-managed content editor with a simple drag-and-drop or block-based interface.
- Allow authorized admins to add, edit, delete, and reorder content blocks, including text and images.
- Allow admins to preview changes, save drafts, and publish content.
- Ensure published changes appear on the public page without requiring a code deployment.
- Keep this CMS limited to the About the Association page; a universal page builder is out of scope.

## 3. Shared Requirements

### 3.1 Role-Based Access Control (RBAC)

- Define permissions for Public Visitor, Authenticated Alumni, Administrator, and Super Administrator.
- Enforce permissions in backend APIs and data access—not only by hiding frontend controls.
- Allow only authorized administrators to edit or publish About page content.
- Prevent unauthorized access to drafts, admin functions, protected data, and role-management actions.
- Test both allowed and denied actions for each role.
- Audit important administrative actions, especially role changes and content publishing.

### 3.2 Design and Accessibility

- Use a consistent visual design, navigation, typography, and components across all pages.
- Ensure responsive behavior across common screen sizes.
- Provide clear loading, empty, and error states.
- Use accessible labels, keyboard navigation, readable contrast, and meaningful image text where applicable.

### 3.3 Data and Privacy

- Define the alumni fields that may be displayed publicly.
- Avoid exposing private contact details or precise residential locations without explicit approval.
- Handle missing or incomplete profile data gracefully.
- Keep directory results, counts, and any map preview consistent with the underlying approved dataset.

### 3.4 Quality and Deployment

- Test the four pages and their navigation.
- Test directory search, filters, pagination, and empty-result behavior.
- Test About page editing, draft preview, and publishing.
- Test RBAC permissions and unauthorized API requests.
- Verify responsive layouts and basic accessibility.
- Provide a reliable deployment process and rollback approach.

## 4. Out of Scope

The following are not part of Version 0.1:

- Jobs, referrals, and career management
- Mentorship management
- Event management, ticketing, and payments
- Fundraising and financial management
- Marketplace and entrepreneur ecosystem
- Digital alumni cards
- Gamification and engagement rewards
- Social media publishing and campaign automation
- AI recommendations and advanced analytics
- Alumni self-registration or self-service profile management
- A universal CMS or workflow builder

## 5. Acceptance Criteria

Version 0.1 is ready for release when:

- All four in-scope pages are implemented and navigable.
- The Landing Page and Home Page are distinct and do not unnecessarily duplicate content.
- The Alumni Directory search and filters work with approved public data.
- Authorized administrators can manage About page content, preview drafts, and publish updates.
- RBAC is enforced by the backend for all protected operations.
- Public pages do not expose unpublished drafts or unapproved alumni information.
- Core functionality, responsive layouts, error states, and access restrictions pass testing.
- No out-of-scope modules are added without an explicit scope change.

## 6. Scope Rule

Any feature not listed in this document is excluded from Version 0.1 unless it is explicitly reviewed and approved as a scope change.
