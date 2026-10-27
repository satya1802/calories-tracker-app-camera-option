<!-- sdlc:auto:start adr -->
# ADR-0004: Use AWS (ap-south-1, Mumbai) for Cloud

Status: Accepted  
Date: 2026-10-05

## Context and Problem Statement

Which Cloud technology does the project use? Decided in architecture v1.

## Considered Options

- AWS (ap-south-1, Mumbai)
- GCP Mumbai
- Azure Central India

## Decision Outcome

Chosen option: AWS (ap-south-1, Mumbai), because Approved stack. One account covers all three needs: managed PostgreSQL (RDS), S3 for user-deletable meal photos, and ECS Fargate to run FastAPI, all in-country for upload speed on Indian mobile networks and data residency. At ~1,000 users the bill is small and later freemium limits change nothing about hosting.

## Consequences

Fargate over EC2 avoids server management for a small team; the external hosted vision API is the one dependency outside the region, used only for analysis with user-deletable photos.
<!-- sdlc:auto:end adr -->