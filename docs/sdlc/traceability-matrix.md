# Traceability Matrix

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start legend -->
Built from recorded links, not written by a model: requirement key → plan item (`source_stable_key`) → development ticket (`stable_key`) → the ticket's test steps → the last live deployment that started after the work finished. **AC tests** counts the story's acceptance criteria that have a test case, and those whose test cases all passed in the latest finished E2E run.
<!-- sdlc:auto:end legend -->

<!-- sdlc:auto:start matrix -->
| Requirement | Epic | Title | Plan items | Sprint | Design | Code | Commits | Ticket | Tests | AC tests | Deployed |
|---|---|---|---|---|---|---|---|---|---|---|---|
| US-001 | EPIC-001 | Sign up for a new account | US-001, US-001-T1, US-001-T2, US-001-T3 | 1 | POST /auth/signup, api, db, users, web | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-002 | EPIC-001 | Sign in to my account | US-002 | 1 | POST /auth/signin, api, db, users, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-003 | EPIC-001 | Sign out of my account | US-003 | 1 | POST /auth/signout, api, users, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-004 | EPIC-002 | Create a new note | US-004, US-004-T1, US-004-T2, US-004-T3 | 2 | POST /notes, api, db, notes, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-005 | EPIC-002 | Save changes to a note | US-005 | 2 | PUT /notes/{id}, api, notes, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-006 | EPIC-002 | View a note | US-006 | 2 | GET /notes/{id}, api, notes, web | — | — | not started | not run | 0/1 tested · 0/1 passing | — |
| US-007 | EPIC-002 | Edit an existing note | US-007 | 3 | PUT /notes/{id}, api, notes, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-008 | EPIC-002 | Delete a note | US-008 | 2 | DELETE /notes/{id}, api, notes, web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-009 | EPIC-003 | See all my notes in a single newest-first list | US-009 | 3 | GET /notes, api, notes, web | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-010 | EPIC-003 | Search my notes by text | US-010, US-010-T1, US-010-T2, US-010-T3 | 3 | GET /notes, api, db, notes, web | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-011 | EPIC-004 | Keep each user's notes private to them | US-011 | 3 | GET /notes, GET /notes/{id}, api, db, notes, users | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-012 | EPIC-004 | Protect account credentials | US-012 | 1 | api, db, users | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-013 | EPIC-005 | Use the app on desktop and mobile browsers | US-013 | 4 | web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-014 | EPIC-005 | Use the app for free with no billing | US-014 | 4 | web | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
<!-- sdlc:auto:end matrix -->
