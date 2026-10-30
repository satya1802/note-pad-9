<!-- sdlc:auto:start adr -->
# ADR-0002: Use FastAPI 0.115 for Backend

Status: Accepted  
Date: 2026-10-30

## Context and Problem Statement

Which Backend technology does the project use? Decided in architecture v1.

## Considered Options

- FastAPI 0.115
- Flask
- Django REST Framework

## Decision Outcome

Chosen option: FastAPI 0.115, because Hosts the small, clearly scoped auth + note CRUD + search API with Pydantic validation and automatic OpenAPI docs.

## Consequences

Minimal batteries-included scaffolding means auth and email integration are assembled from libraries, which is appropriate for this small surface.
<!-- sdlc:auto:end adr -->