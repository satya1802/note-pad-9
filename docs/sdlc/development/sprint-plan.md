# Sprint Plan

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start sprints -->
## Sprint 1: Sprint 1

Stand up accounts: sign-up, sign-in, sign-out, and secure credential handling.

Capacity: 20 points · Committed: 18

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-001 | Story | Sign up for a new account | 8 | backend-agent | — |
| ↳ US-001-T1 | Task | Add users table migration | — | backend-agent | — |
| ↳ US-001-T2 | Task | Implement POST /auth/signup endpoint | — | backend-agent | — |
| ↳ US-001-T3 | Task | Build sign-up screen | — | frontend-agent | — |
| US-002 | Story | Sign in to my account | 5 | backend-agent | US-001 |
| US-003 | Story | Sign out of my account | 2 | backend-agent | US-002 |
| US-012 | Story | Protect account credentials | 3 | security-agent | US-001, US-002 |

## Sprint 2: Sprint 2

Deliver core note CRUD: create, save, view, and delete notes.

Capacity: 20 points · Committed: 18

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-004 | Story | Create a new note | 8 | backend-agent | US-001 |
| ↳ US-004-T1 | Task | Add notes table migration | — | backend-agent | — |
| ↳ US-004-T2 | Task | Implement POST /notes endpoint | — | backend-agent | — |
| ↳ US-004-T3 | Task | Build note creation UI | — | frontend-agent | — |
| US-005 | Story | Save changes to a note | 5 | backend-agent | US-004 |
| US-006 | Story | View a note | 2 | frontend-agent | US-004 |
| US-008 | Story | Delete a note | 3 | frontend-agent | US-004 |

## Sprint 3: Sprint 3

Add note editing, the newest-first list, text search, and per-user privacy enforcement.

Capacity: 20 points · Committed: 19

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-007 | Story | Edit an existing note | 3 | frontend-agent | US-004, US-005 |
| US-009 | Story | See all my notes in a single newest-first list | 5 | frontend-agent | US-004 |
| US-010 | Story | Search my notes by text | 8 | backend-agent | US-009 |
| ↳ US-010-T1 | Task | Add full-text search index to notes | — | backend-agent | — |
| ↳ US-010-T2 | Task | Implement search parameter on GET /notes | — | backend-agent | — |
| ↳ US-010-T3 | Task | Build search box UI | — | frontend-agent | — |
| US-011 | Story | Keep each user's notes private to them | 3 | security-agent | US-004, US-001 |

## Sprint 4: Sprint 4

Polish responsive layout across devices and confirm the app is fully free of billing surfaces.

Capacity: 20 points · Committed: 6

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-013 | Story | Use the app on desktop and mobile browsers | 5 | frontend-agent | US-001, US-004, US-009 |
| US-014 | Story | Use the app for free with no billing | 1 | qa-agent | — |

## Unscheduled

_Nothing unscheduled._
<!-- sdlc:auto:end sprints -->
