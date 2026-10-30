# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-TECH-STACK · approved · source: requirements:technology stack

Product owner approved an exact technology stack for this lightweight-scope v1: FastAPI backend, AWS cloud, PostgreSQL 16 database, React 19 frontend.

Delivery scope: lightweight; requirements version 1. Approved stack to design against exactly, no substitutions: Backend -- FastAPI 0.115, chosen because the backend only needs CRUD on notes plus per-user isolation and sign-up/sign-in, a small clearly-scoped API. Cloud -- AWS, chosen for low-cost reliable hosting of app, database, and email from one account, platform default with no special regional/regulatory needs. Database -- PostgreSQL 16, chosen because the data (users, notes belonging to a user) is simple and relational, and its built-in text search covers the search-by-text feature without an extra search service. Frontend -- React 19, chosen to handle the interactive screens (sign up, sign in, notes list, note editor) including auto-save/live search, and to cover desktop and mobile from one codebase.

**Related:** EPIC-001, EPIC-002, EPIC-003, EPIC-004, EPIC-005

### REQ-SERVICES · approved · source: requirements:services

SendGrid approved as the email delivery service, required for account-related email.

Service: SendGrid (SaaS), configured via env var SENDGRID_API_KEY. Rationale: email/password sign-up requires sending account emails -- password resets and, if chosen, a verify-your-address link -- reliably delivered to users' inboxes without running a mail server. Required API key for this app: SENDGRID_API_KEY.

**Related:** US-001, US-002

- ⚠ Whether a verify-your-address email is actually sent at sign-up is left as an 'if you choose' option in the input, not a firm decision.

### REQ-SCOPE · approved · source: requirements:scope

Explicit in-scope and out-of-scope boundaries for this version, to prevent scope creep during design/build.

Out of scope -- do not design or build: image/file attachments on notes; rich text formatting (bold, lists, headings); folders, tags, pinning/favourites for notes; native mobile/desktop app with offline support. In-scope capabilities: create, view, edit and delete notes; note with a title and plain-text body; single notes list ordered newest-first; search notes by their text; email and password sign-up and sign-in; private per-user notes visible only to their owner; auto-save or explicit save of a note; responsive web app for desktop and mobile browsers; free to use with no payments or billing.

### US-001 · draft · source: requirements:US-001

Allows new visitors to self-service create an account using an email address and password, establishing a private account.

Critical priority. On the sign-up page, entering a valid, not-yet-registered email and a password meeting the password rules and submitting creates the account, signs the user in, and routes to an empty notes list (AC-001). If the email is already registered, no account is created and a message explains the email is already in use (AC-002). If the email is missing/malformed or the password fails the rules, no account is created and a validation message indicates what to correct (AC-003). Authentication is email+password with self-service sign-up, confirmed as an open assumption at the epic level. The app has no paid tier, subscription, or billing-related account state.

**Related:** AC-001, AC-002, AC-003, EPIC-001

- ⚠ Exact password rules (minimum length/complexity) are not specified in the input.
- ⚠ Whether a verify-your-address email is sent at sign-up is left open ('if you choose').

### US-002 · draft · source: requirements:US-002

Returning users sign in with email and password to reach their private notes list.

Critical priority. Entering the correct email and password on the sign-in page and submitting signs the user in and routes to their notes list (AC-004). If the email/password combination does not match an account, the user is not signed in and sees an error that does not reveal whether the email exists, per NFR-003 (AC-005).

**Related:** AC-004, AC-005, NFR-003, EPIC-001

### US-003 · draft · source: requirements:US-003

Signed-in users can sign out to end their session and prevent others on the same device from seeing their notes.

High priority. Choosing to sign out ends the session and returns the user to the sign-in page (AC-006). After sign-out, using the browser back button or a direct URL to a notes page shows no note content and prompts the user to sign in, per NFR-004 (AC-007).

**Related:** AC-006, AC-007, NFR-004, EPIC-001

### US-004 · draft · source: requirements:US-004

Signed-in users create a new note with a title and plain-text body only.

Critical priority. Creating a note with a title and/or plain-text body saves it to the account and places it at the top of the newest-first notes list (AC-008). The editor accepts only plain text for the body and provides no rich-text, image, or attachment controls, consistent with those being out of scope (AC-009).

**Related:** AC-008, AC-009, EPIC-002

### US-005 · draft · source: requirements:US-005

Note edits are persisted reliably, either automatically or via an explicit save action, with failure handling.

Critical priority. When a save occurs, the change is persisted to the account and reflected when the note is reopened (AC-010). Whether saving is automatic or via an explicit action is an open assumption to be resolved during design; this requirement covers both possibilities. If a save fails (e.g. network error), the user is informed the change was not saved and the unsaved text remains visible so they can retry (AC-011).

**Related:** AC-010, AC-011, EPIC-002

- ⚠ Save mechanism (auto-save vs. explicit save button) is an open assumption; no architecture/design input exists yet to resolve it.

### US-006 · draft · source: requirements:US-006

Signed-in users open a note from the list to read its full title and body.

High priority. Selecting a note from the list displays its title and full plain-text body (AC-012).

**Related:** AC-012, EPIC-002

### US-007 · draft · source: requirements:US-007

Users can change a note's title or body, keeping content up to date, with the list reordering to reflect the edit.

High priority. Changing and saving a note's title or body persists the update and shows it on reopening (AC-013). When editing makes a note the most recently changed, it moves to reflect its updated newest-first position in the list on return to the list view (AC-014).

**Related:** AC-013, AC-014, EPIC-002

### US-008 · draft · source: requirements:US-008

Users can delete a note they no longer need, with a confirmation step to prevent accidental loss.

High priority. Choosing to delete a note and confirming removes it from the account so it no longer appears in the list or search results (AC-015). Cancelling the confirmation leaves the note unchanged and not deleted (AC-016).

**Related:** AC-015, AC-016, EPIC-002

### US-009 · draft · source: requirements:US-009

All of a user's notes display in a single newest-first list, with an empty state for new users and no organisational controls.

Critical priority. The notes list shows all of a signed-in user's notes in one list ordered so the most recently created or updated appears first (AC-017). Users with no notes see an empty state indicating they have none yet and a way to create one (AC-018). No folders, tags, pinning, or favourite controls are present, consistent with those being out of scope (AC-019).

**Related:** AC-017, AC-018, AC-019, EPIC-003

### US-010 · draft · source: requirements:US-010

A search box filters the notes list to notes whose title or body text matches the search term.

High priority. Typing text into the search box filters the list to only notes whose title or body matches the term (AC-020). If no note matches, a clear 'no results' message is shown (AC-021). Clearing the search box restores the full newest-first list (AC-022). PostgreSQL's built-in text search was specifically chosen to support this without an extra search service.

**Related:** AC-020, AC-021, AC-022, EPIC-003

### US-011 · draft · source: requirements:US-011

Each user's notes are visible only to them; there is no sharing or collaboration between users.

Critical priority. Viewing the notes list or any note shows only notes belonging to the signed-in user's own account, never another user's, per NFR-001 (AC-023). Attempting to access another user's note directly (e.g. via its URL or identifier) is denied and content is not shown (AC-024). No controls exist to share or collaborate on a note with another user; sharing/collaboration is explicitly out of scope, and no cross-user collaboration is confirmed as an open assumption at the epic level (AC-025).

**Related:** AC-023, AC-024, AC-025, NFR-001, EPIC-004

### US-012 · draft · source: requirements:US-012

Account passwords are stored securely via one-way hashing and transmitted only over HTTPS.

High priority. Passwords are stored using a secure one-way hashing mechanism and never stored or displayed in plain text (AC-026, NFR-002). Password data entered at sign-up or sign-in is sent to the server over an encrypted HTTPS connection (AC-027, NFR-002).

**Related:** AC-026, AC-027, NFR-002, EPIC-004

### US-013 · draft · source: requirements:US-013

The app must work and adapt its layout on both modern desktop and mobile browsers, keeping all core actions usable.

High priority. In a modern desktop browser, the notes list, a note, and the sign-in/sign-up pages are usable, with all core actions available: create, view, edit, delete, search, sign in/out (AC-028, NFR-005). In a modern mobile browser, the same pages adapt to the smaller screen with all core actions usable without horizontal scrolling or overlap (AC-029, NFR-005).

**Related:** AC-028, AC-029, NFR-005, EPIC-005

### US-014 · draft · source: requirements:US-014

The app is entirely free to use, with no payment prompts, paywalls, or billing screens anywhere.

Medium priority. Signing up and using any feature (creating, editing, searching, deleting notes) never prompts for payment details and no feature is locked behind a paywall (AC-030). No billing, subscription, or payment screens exist anywhere in the application, consistent with the app being free to use (AC-031).

**Related:** AC-030, AC-031, EPIC-005

### NFR-006 · draft · source: requirements:NFR-006

Accepted risk: no industry-specific regulatory compliance is treated as in scope beyond credential protection and standard regional privacy practice.

Applies to the whole system. Beyond protecting account credentials (secure hashing, HTTPS -- see NFR-002/US-012) and following standard privacy practices in the operator's default region, no industry-specific regulatory or data-sensitivity compliance is treated as in scope for this version. This is recorded in the input as an accepted risk, not as a reviewed legal/compliance determination.

**Related:** NFR-002

- ⚠ No named industry or regulatory framework was given to verify against; this is an accepted-risk statement only, not a confirmed compliance posture.
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v1  
**Delivery scope:** lightweight  
**Approved:** 2026-10-30

**Capabilities in scope:** Create, view, edit and delete notes, Note with a title and plain-text body, Single notes list ordered newest-first, Search notes by their text, Email and password sign-up and sign-in, Private per-user notes visible only to their owner, Auto-save or explicit save of a note, Responsive web app for desktop and mobile browsers, Email and password login with self-service sign-up, Free to use, no payments or billing

**Approved technology stack:**

| Layer | Choice | Rationale |
|---|---|---|
| backend | FastAPI | The backend only needs to do create/view/edit/delete on notes, enforce that each user sees only their own, and handle sign-up and sign-in. FastAPI is a lightweight, well-suited choice for this small, clearly-scoped API and keeps the server simple and fast to build. |
| cloud | AWS | A small, free consumer web app needs reliable, low-cost hosting that can grow if the app catches on. AWS covers hosting the app, the database, and sending email from one account, and at your expected scale the cost stays low. It's the platform default and fits a general-audience tool with no special regional or regulatory needs. |
| database | PostgreSQL | Your data is simple and structured -- users, and notes belonging to a user -- which is exactly what a relational database is built for. PostgreSQL also has strong built-in text search, so the 'find notes by their text' search box is handled without any extra search service, keeping the system to a single moving part. |
| frontend | React | Your product is a responsive web app that works on desktop and mobile browsers, with a handful of simple screens: sign up, sign in, a notes list, and a note editor. React handles exactly this kind of interactive editing (typing, auto-save, live search filtering) and adapts to any screen size, so one codebase covers both desktop and phone as you specified. |
<!-- sdlc:auto:end summary -->

<!-- sdlc:auto:start epics -->
## EPIC-001: Account Access & Authentication

Self-service account management so each person has a private account. Authentication is email + password with self-service sign-up (confirmed as an open assumption). The app is free to use with no payments or billing, so there is no paid tier, subscription, or billing-related account state.

### US-001: Sign up for a new account

**Priority:** critical

> As a new visitor, I want to create an account using my email address and a password, so that I can start keeping my own private notes.

| ID | Given | When | Then |
|---|---|---|---|
| AC-001 | I am on the sign-up page and not signed in | I enter a valid, not-yet-registered email address and a password that meets the password rules and submit | an account is created for me and I am signed in and taken to my (empty) notes list |
| AC-002 | I am on the sign-up page | I enter an email address that is already registered and submit | the account is not created and I see a message telling me the email is already in use |
| AC-003 | I am on the sign-up page | I submit with a missing or malformed email, or a password that does not meet the rules | the account is not created and I see a validation message indicating what to correct |

### US-002: Sign in to my account

**Priority:** critical

> As a returning user, I want to sign in with my email and password, so that I can access my private notes.

| ID | Given | When | Then |
|---|---|---|---|
| AC-004 | I have an existing account and am on the sign-in page | I enter my correct email and password and submit | I am signed in and taken to my notes list |
| AC-005 | I am on the sign-in page | I enter an email/password combination that does not match an account | I am not signed in and I see an error message that does not reveal whether the email exists |

### US-003: Sign out of my account

**Priority:** high

> As a signed-in user, I want to sign out, so that others using the same device cannot see my notes.

| ID | Given | When | Then |
|---|---|---|---|
| AC-006 | I am signed in | I choose to sign out | my session ends and I am returned to the sign-in page |
| AC-007 | I have signed out | I try to open a notes page using the browser back button or a direct URL | I am not shown any note content and am prompted to sign in |

## EPIC-002: Note Creation, Viewing, Editing & Deletion

Core CRUD on notes. A note consists of a title and a plain-text body only — no rich text formatting, images, or file attachments (those are explicitly out of scope). Edits are persisted either by auto-save or by an explicit save action; the specific mechanism is an open assumption to be resolved during design, and this requirement covers both possibilities by requiring that saved changes persist reliably. There is no export/import and no version history (out of scope for this version).

### US-004: Create a new note

**Priority:** critical

> As a signed-in user, I want to create a note with a title and a plain-text body, so that I can capture something I want to remember.

| ID | Given | When | Then |
|---|---|---|---|
| AC-008 | I am signed in | I create a new note and enter a title and/or plain-text body | the note is saved to my account and appears at the top of my notes list (newest-first) |
| AC-009 | I am creating a note | I attempt to add rich formatting, an image, or a file attachment | the editor accepts only plain text for the body and provides no rich-text, image, or attachment controls |

### US-005: Save changes to a note

**Priority:** critical

> As a signed-in user, I want my note edits to be persisted, so that I do not lose what I have written.

| ID | Given | When | Then |
|---|---|---|---|
| AC-010 | I have entered or changed text in a note | the save takes place (either automatically or via an explicit save action — the chosen mechanism is an open assumption) | the change is persisted to my account and the saved state is reflected when I reopen the note |
| AC-011 | a note is being saved | the save fails (for example due to a network error) | I am informed the change was not saved and my unsaved text remains visible so I can retry |

### US-006: View a note

**Priority:** high

> As a signed-in user, I want to open and read a note, so that I can see its full title and body.

| ID | Given | When | Then |
|---|---|---|---|
| AC-012 | I have at least one note | I select a note from my list | its title and full plain-text body are displayed |

### US-007: Edit an existing note

**Priority:** high

> As a signed-in user, I want to change the title or body of an existing note, so that I can keep my notes up to date.

| ID | Given | When | Then |
|---|---|---|---|
| AC-013 | I have an existing note open | I change the title or body and the change is saved | the updated content is persisted and shown when I reopen the note |
| AC-014 | I edit a note so that it becomes the most recently changed note | I return to my notes list | the note reflects its updated position according to the newest-first ordering |

### US-008: Delete a note

**Priority:** high

> As a signed-in user, I want to delete a note I no longer need, so that my list stays relevant.

| ID | Given | When | Then |
|---|---|---|---|
| AC-015 | I have a note | I choose to delete it and confirm the deletion | the note is removed from my account and no longer appears in my notes list or search results |
| AC-016 | I choose to delete a note | I am asked to confirm and I cancel | the note is not deleted and remains unchanged |

## EPIC-003: Notes List & Search

All of a user's notes appear in a single flat list ordered newest-first, with a search box to find notes by their text. There are no folders, tags, pinning, or favourites (explicitly out of scope).

### US-009: See all my notes in a single newest-first list

**Priority:** critical

> As a signed-in user, I want to see all my notes in one list with the newest first, so that I can quickly find and open recent notes.

| ID | Given | When | Then |
|---|---|---|---|
| AC-017 | I am signed in and have several notes | I view my notes list | all of my notes are shown in a single list ordered so the most recently created or updated note appears first |
| AC-018 | I am signed in and have no notes | I view my notes list | I see an empty state indicating I have no notes yet and a way to create one |
| AC-019 | I am viewing the notes list | I look for organisation controls | no folders, tags, pinning, or favourite controls are present |

### US-010: Search my notes by text

**Priority:** high

> As a signed-in user, I want to search my notes using a search box, so that I can find a specific note by its content.

| ID | Given | When | Then |
|---|---|---|---|
| AC-020 | I have multiple notes | I type text into the search box | the list shows only my notes whose title or body text matches the search term |
| AC-021 | I have entered a search term | no note matches the term | I see a clear 'no results' message |
| AC-022 | I have an active search | I clear the search box | the full newest-first list of my notes is shown again |

## EPIC-004: Privacy & Data Isolation

Each user sees only their own notes; there is no collaboration or sharing between users (open assumption). This is a general-audience consumer tool with no industry-specific regulatory requirements beyond protecting account credentials and standard privacy practices in the operator's default region (open assumption).

### US-011: Keep each user's notes private to them

**Priority:** critical

> As a signed-in user, I want my notes to be visible only to me, so that my private information stays private.

| ID | Given | When | Then |
|---|---|---|---|
| AC-023 | I am signed in | I view my notes list or any note | I see only notes that belong to my own account and never any other user's notes |
| AC-024 | another user's note exists | I attempt to access it directly (for example via its URL or identifier) | access is denied and the note content is not shown |
| AC-025 | I am a user | I use the application | there are no controls to share a note with, or collaborate on a note with, another user (sharing/collaboration is out of scope) |

### US-012: Protect account credentials

**Priority:** high

> As a user, I want my password to be stored and handled securely, so that my account cannot be easily compromised.

| ID | Given | When | Then |
|---|---|---|---|
| AC-026 | I create or change my password | the credential is stored | it is stored using a secure one-way hashing mechanism and never stored or displayed in plain text |
| AC-027 | I enter my password during sign-up or sign-in | the data is transmitted to the server | it is sent over an encrypted (HTTPS) connection |

## EPIC-005: Responsive Web Delivery & Free Access

The product is delivered as a responsive web application that works in desktop and mobile browsers. There is no native app and no offline support (out of scope). The app is free to use with no payments or billing (open assumption).

### US-013: Use the app on desktop and mobile browsers

**Priority:** high

> As a user, I want the app to work and adapt to my screen size, so that I can use it comfortably on a phone or a computer.

| ID | Given | When | Then |
|---|---|---|---|
| AC-028 | I open the app in a modern desktop browser | I view the notes list, a note, and the sign-in/sign-up pages | the layout is usable and all core actions (create, view, edit, delete, search, sign in/out) are available |
| AC-029 | I open the app in a modern mobile browser | I view the same pages | the layout adapts to the smaller screen and all core actions remain usable without horizontal scrolling or overlap |

### US-014: Use the app for free with no billing

**Priority:** medium

> As a user, I want to use all features without paying, so that I am not blocked by payments or subscriptions.

| ID | Given | When | Then |
|---|---|---|---|
| AC-030 | I am using the app | I sign up and use any feature (creating, editing, searching, deleting notes) | I am never asked for payment details and no feature is locked behind a paywall |
| AC-031 | I navigate the whole application | I look for billing, subscription, or payment screens | none exist, consistent with the app being free to use |
<!-- sdlc:auto:end epics -->
