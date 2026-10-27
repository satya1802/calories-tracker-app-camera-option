# Calories tracker app camera option — SDLC Documentation

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start overview -->
calories tracker app with camera option where user can take phtotos and will show the calories of the pic

**Documentation version:** v1
<!-- sdlc:auto:end overview -->

## Contents

<!-- sdlc:auto:start contents -->
| Document | State |
|---|---|
| [Requirements](requirements/README.md) | v1 approved |
| [Architecture](architecture/README.md) | 4 entries |
| [Development](development/README.md) | 9 entries |
| [Testing](testing/README.md) | 1 entry |
| [Deployment](deployment/README.md) | 1 entry |
| [Maintenance](maintenance/README.md) | 1 entry |
| [Data model](architecture/data-model.md) | generated |
| [API (OpenAPI)](architecture/api/openapi.yaml) | generated |
| [Decisions (ADRs)](architecture/adr/README.md) | 5 decisions |
| [Sprint plan](development/sprint-plan.md) | 7 sprints |
| [Developer guide](development/developer-guide.md) | not generated yet |
| [API reference](development/api-reference.md) | 0 routes |
| [Test report](testing/test-report.md) | not run yet |
| [Tests](testing/test-cases.md) | 0 tests |
| [Deployment guide](deployment/deployment-guide.md) | not deployed yet |
| [Runbook](deployment/runbook.md) | not deployed yet |
| [Release notes](deployment/release-notes.md) | 0 releases |
| [Traceability matrix](traceability-matrix.md) | 32 requirements |
| [Changelog](CHANGELOG.md) | 1 version |
<!-- sdlc:auto:end contents -->

## Open gaps

<!-- sdlc:auto:start open-gaps -->
### Requirements

- Calorie/macro target calculation formula and activity multipliers are explicitly described as proposed but not agreed with the business (AC-014) -- needs confirmation before target accuracy can be relied on.
- No numeric accuracy target (e.g. +/-15%) has been agreed for calorie estimates -- explicitly a deferred product decision per AC-031, not a defect, but still open.
- Licence review of IFCT/USDA FoodData Central/Open Food Facts terms and the required in-app attribution (AC-092) is not confirmed as complete in any input provided -- needs sign-off before launch.

### Development

- The input gives sprint goals and a separate flat backlog of stories/tasks, but does not state which specific backlog items were assigned to which sprint -- that mapping could not be reconstructed without guessing.
- No completion, in-progress, or blocked status is reported for any sprint or backlog item, so it cannot be confirmed how much of this plan has actually been executed.
- No implementation status (done/in-progress/blocked) reported for any task in this epic.
- No implementation status reported for any task in this epic.
- No record confirming the licence review mentioned in AC-092 was actually carried out as part of this backlog work.
- No record of the qa-agent audits (feature-gating, clinical-language) actually being run or their results.

### Testing

- Testing phase has not started (or at least no record of it exists) -- no test plan, cases, or results were provided for any requirement or sprint.

### Deployment

- No deployment has been recorded yet -- the approved architecture's deployment nodes (ALB, ECS Fargate, RDS, S3) have no corresponding evidence of being stood up or released.

### Maintenance

- No maintenance phase activity has been recorded -- there is nothing yet to document for ongoing support, monitoring, or the in-field accuracy analysis the product design calls for.
<!-- sdlc:auto:end open-gaps -->
