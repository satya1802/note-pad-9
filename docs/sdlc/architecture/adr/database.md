<!-- sdlc:auto:start adr -->
# ADR-0003: Use PostgreSQL 16 for Database

Status: Proposed  
Date: 2026-10-30

## Context and Problem Statement

Which Database technology does the project use? Decided in architecture v1.

## Considered Options

- PostgreSQL 16
- MySQL
- SQLite

## Decision Outcome

Chosen option: PostgreSQL 16, because Stores users and per-user notes relationally and powers the search box with built-in full-text search (tsvector + GIN), keeping the system to one data store.

## Consequences

Full-text search is sufficient for plain-text notes at this scale; ranking is simpler than a dedicated engine, which is not needed here.
<!-- sdlc:auto:end adr -->