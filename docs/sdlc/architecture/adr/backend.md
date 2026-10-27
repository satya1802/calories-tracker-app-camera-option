<!-- sdlc:auto:start adr -->
# ADR-0002: Use FastAPI (Python) for Backend

Status: Accepted  
Date: 2026-10-05

## Context and Problem Statement

Which Backend technology does the project use? Decided in architecture v1.

## Considered Options

- FastAPI (Python)
- Node.js/NestJS
- Django REST Framework

## Decision Outcome

Chosen option: FastAPI (Python), because Approved stack. Python is where the vision-call, catalogue mapping and portion math live, and FastAPI's async request handling means a photo waiting several seconds on the model does not block other users. Recording the original estimate versus the user correction is a simple table write in the same service.

## Consequences

CPU-bound work is minimal here; the slow path is an external API call, so async I/O is the right fit and no separate worker tier is needed at beta scale.
<!-- sdlc:auto:end adr -->