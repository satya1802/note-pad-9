# note pad — SDLC Documentation

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start overview -->
simple note pad

**Documentation version:** v2
<!-- sdlc:auto:end overview -->

## Contents

<!-- sdlc:auto:start contents -->
| Document | State |
|---|---|
| [Requirements](requirements/README.md) | v1 approved |
| [Architecture](architecture/README.md) | 12 entries |
| [Development](development/README.md) | 1 entry |
| [Testing](testing/README.md) | 1 entry |
| [Deployment](deployment/README.md) | 1 entry |
| [Maintenance](maintenance/README.md) | 1 entry |
| [Data model](architecture/data-model.md) | generated |
| [API (OpenAPI)](architecture/api/openapi.yaml) | generated |
| [Decisions (ADRs)](architecture/adr/README.md) | 4 decisions |
| [Sprint plan](development/sprint-plan.md) | not generated yet |
| [Developer guide](development/developer-guide.md) | not generated yet |
| [API reference](development/api-reference.md) | 0 routes |
| [Test report](testing/test-report.md) | not run yet |
| [Tests](testing/test-cases.md) | 0 tests |
| [Deployment guide](deployment/deployment-guide.md) | not deployed yet |
| [Runbook](deployment/runbook.md) | not deployed yet |
| [Release notes](deployment/release-notes.md) | 0 releases |
| [Traceability matrix](traceability-matrix.md) | 14 requirements |
| [Changelog](CHANGELOG.md) | 2 versions |
<!-- sdlc:auto:end contents -->

## Open gaps

<!-- sdlc:auto:start open-gaps -->
### Requirements

- Whether a verify-your-address email is actually sent at sign-up is left as an 'if you choose' option in the input, not a firm decision.
- Exact password rules (minimum length/complexity) are not specified in the input.
- Whether a verify-your-address email is sent at sign-up is left open ('if you choose').
- Save mechanism (auto-save vs. explicit save button) is an open assumption; no architecture/design input exists yet to resolve it.
- No named industry or regulatory framework was given to verify against; this is an accepted-risk statement only, not a confirmed compliance posture.

### Architecture

- No explicit mapping given from this architecture to specific requirement IDs (US-001..US-014); traceability between requirements and architecture elements could not be confirmed and should be verified by a human.
- Choice between ECS Fargate and App Runner for the API is left open ('ECS Fargate / App Runner') and not finalized in this input.

### Development

- Development phase has not started; no tickets, code, or implementation notes exist yet to document.

### Testing

- Testing phase has not started; no test plans or results exist yet to document.

### Deployment

- No deployment recorded yet; nothing to document about hosting, release, or environment configuration.

### Maintenance

- No maintenance phase activity exists yet since the application has not been deployed.
<!-- sdlc:auto:end open-gaps -->
