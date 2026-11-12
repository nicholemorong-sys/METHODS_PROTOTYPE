# ISKOLAR MARSU

Responsive, multi-page scholarship application and monitoring prototype for Marinduque State University. Built with semantic HTML, CSS, and vanilla JavaScript; no framework or package installation is required.

## Run locally

Serve this folder with a local web server and open `index.html`. For example:

```powershell
python -m http.server 8000
```

Then visit `http://localhost:8000`. A local or hosted web server is recommended for the Web Crypto API and document storage.

The official MarSU seal is bundled at `assets/marsu_logo.png`; a MarSU-colored monogram appears if the image is unavailable.

## Account access

- Students sign in using credentials assigned by MarSU. Public student self-registration is disabled.
- Selecting **Staff / Admin** on the student sign-in page redirects to a separate Staff / Admin sign-in page.
- Staff credentials are not embedded in or displayed by the public interface; this project includes no demo staff account.
- Authorized staff can assign student accounts from the staff-only Student accounts page and share the initial password through an approved private channel.
- The first Staff / Admin account must be provisioned by a trusted administrator or authentication service. There is intentionally no public way to create a privileged account.

The static prototype expects provisioned account records with `email`, `role` (`student` or `admin`), `status`, `passwordSalt`, and `passwordHash` in its browser account store. Production deployments should integrate institution-managed authentication and server-side authorization.

## Pages

- `index.html` — Entry point to student sign-in.
- `login.html` — Student sign-in and role selection; selecting Staff / Admin redirects to the separate staff login.
- `staff-login.html` — Dedicated Staff / Admin sign-in.
- `student-access.html` — Student account access help; it does not create accounts.
- `register.html` — Legacy link to the same account access help page; no registration form.
- `student-dashboard.html` — Student applications, scholarship summaries, and announcements.
- `admin-dashboard.html` — Staff overview, application review queue, and CSV export.
- `student-accounts.html` — Staff-only student credential assignment, directory, and access management.
- `scholarships.html` — Searchable scholarship catalog; staff can add and edit programs.
- `application.html` — Scholarship requirements, application details, and document uploads.
- `profile.html` — Student profile and optional photo management.
- `tracking.html` — Student-only application status timeline and decision notes.
- `announcements.html` — Student announcement board; staff can publish and remove notices.
- `payouts.html` — Payout schedule list; staff can publish, edit, or remove entries.

Shared behavior is in `app.js`; visual styles and responsive rules are in `styles.css`.

## Features

- Separate student and Staff / Admin sign-in flows; the role selector opens the matching sign-in experience.
- Admin-assigned student accounts; there is no public account registration.
- Student and staff dashboards, student profiles, scholarship search and filters, requirements, applications, and document uploads.
- Student-visible status tracking; only staff-facing review controls can update application decisions.
- Staff review includes documents, applicant verification, student account management, application CSV export, scholarship programs, announcements, and payout schedules.
- Notification panel, responsive navigation, accessible status feedback, and input/file validation.

The initial scholarships, announcements, and payout dates are sample content. Confirm eligibility, deadlines, award amounts, and release dates with MarSU and each provider before relying on them.

## Accessibility and responsive design

- Semantic landmarks, headings, lists, forms, labels, and data tables.
- Skip link, visible keyboard focus, native controls, and keyboard-operable actions.
- Accessible names and state attributes for menus, notification panel, review dialog, status updates, and file selection.
- Text alternatives for the university seal and profile image; decorative icons are hidden from assistive technology.
- Desktop uses a persistent side navigation and multi-column layouts; tablet and mobile reduce columns and stack content.
- Mobile navigation collapses into an accessible menu. Tables scroll horizontally on narrow screens.
- Reduced-motion preferences are respected.

## Testing procedures

1. Start the local server. Confirm student sign-in has no account creation option or displayed Staff / Admin credentials.
2. Select Staff / Admin from the role selector and confirm redirection to `staff-login.html`.
3. Provision a Staff / Admin account through a trusted account service before testing staff tools. No starter staff credentials are included.
4. Sign in as staff, assign a student account, and deliver its initial password through an approved private channel.
5. Sign out; sign in as the student using the assigned credentials, update the profile, and submit an application with a small PDF or image.
6. Confirm the student sees only their own application status, cannot access staff pages, and has no decision controls.
7. Sign in as staff, review the application, verify applicant information, download its uploaded document, and save a status decision.
8. Test program search/filters, program edits, announcement publishing, payout schedule management, CSV export, sign-out, and duplicate application prevention.
9. Test keyboard navigation and visible focus, then check layouts at approximately 375 px, 768 px, and 1280 px widths.

## Prototype security boundary

This is a browser-only prototype, not a production scholarship service. Salted, iterated password hashes, account records, profiles, decisions, and schedules live in the current browser's local storage; uploaded files are held in that browser's IndexedDB. A user with browser developer tools can alter local data. Separate login pages and frontend role checks do not provide real authentication or authorization. There is no server-side identity check, audit trail, malware scan, backup, or secure document repository. Production use requires institution-managed authentication, server-enforced role permissions, protected document storage, validation, audit logging, and approved privacy/security practices. Do not enter real student data in this prototype.
