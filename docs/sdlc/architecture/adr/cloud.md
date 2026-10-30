<!-- sdlc:auto:start adr -->
# ADR-0004: Use AWS for Cloud

Status: Proposed  
Date: 2026-10-30

## Context and Problem Statement

Which Cloud technology does the project use? Decided in architecture v1.

## Considered Options

- AWS
- Google Cloud
- Azure

## Decision Outcome

Chosen option: AWS, because Hosts the static SPA (S3/CloudFront), the API container, and the managed PostgreSQL (RDS) from one low-cost account that scales if the app grows.

## Consequences

Managed services simplify ops but add some AWS-specific configuration; costs stay low at expected consumer scale.
<!-- sdlc:auto:end adr -->