# Martial-arts academy website + CMS

A public website and an admin panel for a martial-arts academy. The owner edits texts, images, programmes, the class timetable, the team, contacts and SEO, with drafts and publishing.

**Stack:** Laravel 13 · PHP · MariaDB, on shared hosting · **Test tooling:** PHPUnit (feature and unit tests) · Larastan · Pint

## What I did

- Built the site and the CMS together with their test suite.
- Tested access control on every admin route, the difference between owner and editor roles, and the draft-versus-publish workflow.
- Checked that every content editor renders and saves, and that unpublished changes never leak to the public site.

## Test strategy

| Level | Tool | What it covers |
|---|---|---|
| Feature (HTTP + database) | PHPUnit with Laravel's testing helpers | Admin access, roles, drafts and publishing, content editors, public pages |
| Unit | PHPUnit | Content schemas, helpers |
| Static analysis | Larastan, Pint | Types and code style (not counted as test cases) |

## Highlights

- **CMS-U-002**: every admin route rejects anonymous visitors.
- **CMS-U-003**: there is no public registration.
- **CMS-U-012**: an editor gets 403 on publish but can still save a draft.
- **CMS-U-008**: saving a draft does not change the public site.

## Catalogue

Test titles come from the test method names. Client and product names are anonymized.

<!-- catalog:cms:start -->
**123 test cases** · 0 end-to-end · 123 unit & integration

#### Unit & integration

<details><summary><b>Account</b> · 1 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-001 | Account | Account page only offers password security settings |

</details>

<details><summary><b>AdminAccess</b> · 3 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-002 | AdminAccess | Every admin route rejects anonymous visitors |
| CMS-U-003 | AdminAccess | There is no public registration |
| CMS-U-004 | AdminAccess | Only owners publish and manage users |

</details>

<details><summary><b>AdminDocuments</b> · 10 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-005 | AdminDocuments | Owner sees settings form with status |
| CMS-U-006 | AdminDocuments | All singleton content editors render |
| CMS-U-007 | AdminDocuments | Physical prep editor exposes the visual content fields |
| CMS-U-008 | AdminDocuments | Saving draft does not change public site |
| CMS-U-009 | AdminDocuments | Stale version returns conflict and keeps typed input |
| CMS-U-010 | AdminDocuments | Publish intent goes to confirmation page with diff |
| CMS-U-011 | AdminDocuments | Confirming publishes and records audit |
| CMS-U-012 | AdminDocuments | Editor gets 403 on publish but can save draft |
| CMS-U-013 | AdminDocuments | Restore from history creates revision |
| CMS-U-014 | AdminDocuments | Preview intent redirects to public url with preview param |

</details>

<details><summary><b>AdminFormCoverage</b> · 2 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-015 | AdminFormCoverage | Every schema field has an input in its admin form |
| CMS-U-016 | AdminFormCoverage | Repeater rows keep the fields added for the original layout |

</details>

<details><summary><b>Auth</b> · 11 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-017 | Auth | Login page is served in portuguese |
| CMS-U-018 | Auth | Owner logs in and reaches the dashboard |
| CMS-U-019 | Auth | Wrong password and unknown email get the same message |
| CMS-U-020 | Auth | Login is blocked after five failed attempts even with the right password |
| CMS-U-021 | Auth | Inactive user cannot log in |
| CMS-U-022 | Auth | User deactivated mid session is logged out on the next request |
| CMS-U-023 | Auth | Password reset request does not reveal whether the email exists |
| CMS-U-024 | Auth | Logout ends the session |
| CMS-U-025 | Auth | Two factor authentication routes are not available |
| CMS-U-026 | Auth | Create owner command creates an active owner and sends a link |
| CMS-U-027 | Auth | Create owner refuses an existing email |

</details>

<details><summary><b>ContentSchemas</b> · 4 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-028 | ContentSchemas | Each content schema accepts a complete normalized document |
| CMS-U-029 | ContentSchemas | Testimonial without consent does not block the document |
| CMS-U-030 | ContentSchemas | Legacy team members default to the main coach group |
| CMS-U-031 | ContentSchemas | Testimonial section copy and second program video are normalized |

</details>

<details><summary><b>Dashboard</b> · 1 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-032 | Dashboard | Dashboard shows shortcuts pending drafts alt warning and last publication |

</details>

<details><summary><b>Diff</b> · 4 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-033 | Diff | Lists changed fields with labels |
| CMS-U-034 | Diff | Added repeater rows are numbered from one |
| CMS-U-035 | Diff | First publication lists every filled field and booleans read naturally |
| CMS-U-036 | Diff | Identical documents have no changes |

</details>

<details><summary><b>DocumentWorkflow</b> · 11 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-037 | DocumentWorkflow | Saving a draft bumps the version and leaves the public data alone |
| CMS-U-038 | DocumentWorkflow | Saving with a stale version is refused and keeps the newer draft |
| CMS-U-039 | DocumentWorkflow | Publish copies the draft and records a revision |
| CMS-U-040 | DocumentWorkflow | Public content serves the published version not the draft |
| CMS-U-041 | DocumentWorkflow | Content reflects a new publication immediately |
| CMS-U-042 | DocumentWorkflow | Publishing with a stale version is refused |
| CMS-U-043 | DocumentWorkflow | Publish is blocked when required content is missing |
| CMS-U-044 | DocumentWorkflow | Restore creates a new revision and keeps history |
| CMS-U-045 | DocumentWorkflow | Discard returns the draft to the published version |
| CMS-U-046 | DocumentWorkflow | Preview shows the draft only for the previewed document |
| CMS-U-047 | DocumentWorkflow | Publishing is recorded in the audit log with a truncated ip |

</details>

<details><summary><b>Health</b> · 3 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-048 | Health | Health endpoint responds |
| CMS-U-049 | Health | Application speaks european portuguese |
| CMS-U-050 | Health | Dates use lisbon time |

</details>

<details><summary><b>ImportArchive</b> · 9 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-051 | ImportArchive | Import creates drafts without publishing |
| CMS-U-052 | ImportArchive | Import with publicar publishes all created documents |
| CMS-U-053 | ImportArchive | Import is idempotent and does not replace an edited draft |
| CMS-U-054 | ImportArchive | Unconfirmed items keep review notes |
| CMS-U-055 | ImportArchive | Missing archive file fails with a clear message before importing |
| CMS-U-056 | ImportArchive | Substituir replaces edited content as a new revision without duplicates |
| CMS-U-057 | ImportArchive | Substituir does not bring back a program the owner deleted |
| CMS-U-058 | ImportArchive | Bundled initial content fits the limits of every schema |
| CMS-U-059 | ImportArchive | Publicar publishes nothing when any document is not ready |

</details>

<details><summary><b>Media</b> · 12 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-060 | Media | Valid jpeg creates webp variants and social jpeg |
| CMS-U-061 | Media | Exif rotated photo is stored upright |
| CMS-U-062 | Media | Heic is rejected with portuguese message |
| CMS-U-063 | Media | Renamed non image is rejected |
| CMS-U-064 | Media | File over limit is rejected |
| CMS-U-065 | Media | Same file twice returns existing media |
| CMS-U-066 | Media | Media in use cannot be trashed and lists references |
| CMS-U-067 | Media | Trash restore and purge after 30 days |
| CMS-U-068 | Media | Replace keeps id and removes old files |
| CMS-U-069 | Media | Media files are served without session cookies or queries |
| CMS-U-070 | Media | Fallback route serves media and blocks traversal |
| CMS-U-071 | Media | Editor can upload |

</details>

<details><summary><b>MediaReferences</b> · 2 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-072 | MediaReferences | Collects single and list references at any depth |
| CMS-U-073 | MediaReferences | Document without media has no references |

</details>

<details><summary><b>OriginalLayout</b> · 11 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-074 | OriginalLayout | Pages link the self hosted brand fonts |
| CMS-U-075 | OriginalLayout | Header shows the partner logo and social icons |
| CMS-U-076 | OriginalLayout | Class map section shows the poster image |
| CMS-U-077 | OriginalLayout | Program cards use their own title and image |
| CMS-U-078 | OriginalLayout | Program page follows the original structure |
| CMS-U-079 | OriginalLayout | Home gallery offers one filter per category |
| CMS-U-080 | OriginalLayout | Team members are grouped and biographies open only on request |
| CMS-U-081 | OriginalLayout | Program page places up to two videos beside the description |
| CMS-U-082 | OriginalLayout | Reviews section shows background google summary and approved reviews |
| CMS-U-083 | OriginalLayout | Schools show map and contact links |
| CMS-U-084 | OriginalLayout | Contact section embeds the school map |

</details>

<details><summary><b>Preview</b> · 2 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-085 | Preview | Anonymous preview parameter never shows draft but owner can preview it |
| CMS-U-086 | Preview | New schedule session appears in preview and only publicly after publish |

</details>

<details><summary><b>ProgramAdmin</b> · 6 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-087 | ProgramAdmin | Owner creates a program and duplicate slug is rejected |
| CMS-U-088 | ProgramAdmin | Program list create and edit pages render |
| CMS-U-089 | ProgramAdmin | Publishing a changed slug creates a redirect |
| CMS-U-090 | ProgramAdmin | Service cleans untrusted slug before saving |
| CMS-U-091 | ProgramAdmin | Malformed slug written outside the service never becomes a redirect |
| CMS-U-092 | ProgramAdmin | Owner can trash and restore a program |

</details>

<details><summary><b>PublicPages</b> · 5 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-093 | PublicPages | Every public page has language one h1 and canonical |
| CMS-U-094 | PublicPages | Invisible program returns not found |
| CMS-U-095 | PublicPages | Old editing pages are gone without revealing admin |
| CMS-U-096 | PublicPages | Old slug redirects permanently |
| CMS-U-097 | PublicPages | Empty sections unapproved testimonials prices and html are not exposed |

</details>

<details><summary><b>ScheduleSchema</b> · 3 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-098 | ScheduleSchema | Invalid hours and end before start are rejected |
| CMS-U-099 | ScheduleSchema | Normalize reindexes rows and converts checkboxes |
| CMS-U-100 | ScheduleSchema | Problems requires a category in each session |

</details>

<details><summary><b>SecurityHeaders</b> · 5 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-101 | SecurityHeaders | Responses carry a strict content security policy |
| CMS-U-102 | SecurityHeaders | Page assets carry the nonce allowed by the policy |
| CMS-U-103 | SecurityHeaders | Basic hardening headers are present |
| CMS-U-104 | SecurityHeaders | Admin pages are never indexed or cached |
| CMS-U-105 | SecurityHeaders | Noindex mode marks public responses too |

</details>

<details><summary><b>Seo</b> · 3 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-106 | Seo | Sitemap lists public pages and visible programs but never admin |
| CMS-U-107 | Seo | Robots blocks admin and can block the entire staging site |
| CMS-U-108 | Seo | Json ld uses only published factual settings |

</details>

<details><summary><b>Text</b> · 8 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-109 | Text | Paragraphs and bold are rendered |
| CMS-U-110 | Text | Raw html is shown as text not executed |
| CMS-U-111 | Text | Javascript links lose their target |
| CMS-U-112 | Text | Top level headings are demoted to keep a single h1 |
| CMS-U-113 | Text | Empty text renders nothing |
| CMS-U-114 | Text | Headings never break inside a hyphenated word |
| CMS-U-115 | Text | Headings escape markup |
| CMS-U-116 | Text | Card headings put the first word on its own line |

</details>

<details><summary><b>TwoFactorRemoval</b> · 1 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-117 | TwoFactorRemoval | Users table does not store two factor credentials |

</details>

<details><summary><b>UserAdmin</b> · 5 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-118 | UserAdmin | Owner invites editor and reset link is sent |
| CMS-U-119 | UserAdmin | Deactivating user removes database sessions |
| CMS-U-120 | UserAdmin | Last active owner cannot be deactivated or demoted |
| CMS-U-121 | UserAdmin | Editor cannot manage users |
| CMS-U-122 | UserAdmin | Role and active flag cannot be mass assigned |

</details>

<details><summary><b>YouTube</b> · 1 cases</summary>

| ID | Suite | Case |
|---|---|---|
| CMS-U-123 | YouTube | Extracts the video id |

</details>
<!-- catalog:cms:end -->

[← Back to the portfolio](../../README.md)
