# Development

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
### DEV-PLAN-OVERVIEW · approved · source: plan:v1

The development plan (version 1) is approved and organizes the project into 4 sprints of 20-point capacity each, covering 5 epics and all 14 known user stories plus their engineering sub-tasks.

Plan status: approved, version 1. Sprint goals: Sprint 1 — stand up accounts (sign-up, sign-in, sign-out, secure credential handling); Sprint 2 — deliver core note CRUD (create, save, view, delete); Sprint 3 — add note editing, newest-first list, text search, and per-user privacy enforcement; Sprint 4 — polish responsive layout across devices and confirm the app is fully free of billing surfaces. Epics: EPIC-001 Account Access & Authentication, EPIC-002 Note Creation/Viewing/Editing/Deletion, EPIC-003 Notes List & Search, EPIC-004 Privacy & Data Isolation, EPIC-005 Responsive Web Delivery & Free Access. Backend-agent, frontend-agent, security-agent and qa-agent roles are assigned across stories; no owner is assigned to the epics themselves.

**Related:** US-001, US-002, US-003, US-004, US-005, US-006, US-007, US-008, US-009, US-010, US-011, US-012, US-013, US-014

- ⚠ No development execution status (ticket progress, commits, pull requests, code review outcomes) is present in this input — only the approved backlog/plan structure is available.
- ⚠ The input lists sprints and backlog items as separate lists without explicit sprint-to-item assignment; this documentation infers groupings from sprint goal wording matched to epic themes, and that inference should be confirmed against the actual plan.

### DEV-SPRINT-1 · draft · source: plan:Sprint 1

Sprint 1 targets account access: sign-up, sign-in, sign-out, and secure credential handling, under EPIC-001.

Goal: 'Stand up accounts: sign-up, sign-in, sign-out, and secure credential handling.' Capacity: 20 points. Items (inferred as belonging to this sprint based on goal match to EPIC-001): US-001 Sign up for a new account (8 pts, backend-agent) with sub-tasks US-001-T1 Add users table migration, US-001-T2 Implement POST /auth/signup endpoint (both backend-agent), and US-001-T3 Build sign-up screen (frontend-agent); US-002 Sign in to my account (5 pts, backend-agent); US-003 Sign out of my account (2 pts, backend-agent). Combined estimated points (15) are within the 20-point capacity.

**Related:** US-001, US-002, US-003

- ⚠ No record of task/story completion, blockers, or code delivered for Sprint 1 in this input.
- ⚠ Sprint assignment of these items is inferred from goal wording, not explicitly stated.

### DEV-SPRINT-2 · draft · source: plan:Sprint 2

Sprint 2 targets core note CRUD operations: create, save, view, and delete, under EPIC-002.

Goal: 'Deliver core note CRUD: create, save, view, and delete notes.' Capacity: 20 points. Items (inferred): US-004 Create a new note (8 pts, backend-agent) with sub-tasks US-004-T1 Add notes table migration, US-004-T2 Implement POST /notes endpoint (backend-agent), and US-004-T3 Build note creation UI (frontend-agent); US-005 Save changes to a note (5 pts, backend-agent); US-006 View a note (2 pts, frontend-agent); US-008 Delete a note (3 pts, frontend-agent). Combined estimated points (18) are within the 20-point capacity. US-007 (Edit an existing note) is excluded from this sprint because Sprint 2's goal explicitly covers only create/save/view/delete, and 'editing' is named separately as a Sprint 3 goal item.

**Related:** US-004, US-005, US-006, US-008

- ⚠ No record of task/story completion, blockers, or code delivered for Sprint 2 in this input.
- ⚠ Sprint assignment of these items is inferred from goal wording, not explicitly stated.

### DEV-SPRINT-3 · draft · source: plan:Sprint 3

Sprint 3 targets note editing, the newest-first notes list, text search, and per-user privacy enforcement, spanning EPIC-002, EPIC-003, and EPIC-004.

Goal: 'Add note editing, the newest-first list, text search, and per-user privacy enforcement.' Capacity: 20 points. Items (inferred): US-007 Edit an existing note (3 pts, frontend-agent); US-009 See all my notes in a single newest-first list (5 pts, frontend-agent); US-010 Search my notes by text (8 pts, backend-agent) with sub-tasks US-010-T1 Add full-text search index to notes, US-010-T2 Implement search parameter on GET /notes (backend-agent), and US-010-T3 Build search box UI (frontend-agent); US-011 Keep each user's notes private to them (3 pts, security-agent), matching the goal's 'per-user privacy enforcement.' Combined estimated points for these four stories (19) are within the 20-point capacity.

**Related:** US-007, US-009, US-010, US-011, US-012

- ⚠ No record of task/story completion, blockers, or code delivered for Sprint 3 in this input.
- ⚠ Sprint assignment of these items is inferred from goal wording, not explicitly stated.
- ⚠ US-012 (Protect account credentials, 3 pts, security-agent, EPIC-004) is not clearly covered by any sprint goal's wording — Sprint 1 covers 'secure credential handling' and Sprint 3 covers 'privacy enforcement,' so it is ambiguous which sprint US-012 belongs to; this should be confirmed rather than assumed.

### DEV-SPRINT-4 · draft · source: plan:Sprint 4

Sprint 4 targets responsive layout polish across devices and verification that the app has no billing surfaces, under EPIC-005.

Goal: 'Polish responsive layout across devices and confirm the app is fully free of billing surfaces.' Capacity: 20 points. Items (inferred): US-013 Use the app on desktop and mobile browsers (5 pts, frontend-agent); US-014 Use the app for free with no billing (1 pt, qa-agent). Combined estimated points (6) leave significant unused capacity (14 points) relative to the sprint's 20-point capacity.

**Related:** US-013, US-014

- ⚠ No record of task/story completion, blockers, or code delivered for Sprint 4 in this input.
- ⚠ Sprint assignment of these items is inferred from goal wording, not explicitly stated.
- ⚠ 14 of the sprint's 20-point capacity is unaccounted for by the two listed stories; no other items were identified as belonging to this sprint, which may indicate missing backlog items or an intentionally light sprint — not stated in the input.
<!-- sdlc:auto:end narrative -->
