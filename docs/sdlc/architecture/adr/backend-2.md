<!-- sdlc:auto:start adr -->
# ADR-0005: Use Amazon S3 (object store) for meal photos for Backend

Status: Accepted  
Date: 2026-10-05

## Context and Problem Statement

Which Backend technology does the project use? Decided in architecture v1.

## Considered Options

- Amazon S3 (object store) for meal photos
- Store images as DB blobs
- EFS file storage

## Decision Outcome

Chosen option: Amazon S3 (object store) for meal photos, because Supporting technology the design genuinely needs: meal photos must be stored in-country, served only to the owning account via pre-signed URLs, and hard-deleted when the user deletes the meal. S3 lifecycle and object deletion map directly onto AC-075/100.

## Consequences

Photos live outside the database, so deletion is a two-step (DB row + S3 object) handled in the delete path; keeps Postgres small and photo serving cheap.
<!-- sdlc:auto:end adr -->