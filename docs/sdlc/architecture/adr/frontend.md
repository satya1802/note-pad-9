<!-- sdlc:auto:start adr -->
# ADR-0001: Use React 19 for Frontend

Status: Accepted  
Date: 2026-10-30

## Context and Problem Statement

Which Frontend technology does the project use? Decided in architecture v1.

## Considered Options

- React 19
- Vue
- Svelte

## Decision Outcome

Chosen option: React 19, because Drives the SPA's interactive note editing, auto-save, live search filtering and responsive layouts across desktop and mobile from a single codebase.

## Consequences

A client-rendered SPA needs explicit auth/session handling in the browser and route guards to block note pages after sign-out (NFR-004).
<!-- sdlc:auto:end adr -->