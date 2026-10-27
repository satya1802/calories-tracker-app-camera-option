<!-- sdlc:auto:start adr -->
# ADR-0003: Use Amazon RDS for PostgreSQL for Database

Status: Accepted  
Date: 2026-10-05

## Context and Problem Statement

Which Database technology does the project use? Decided in architecture v1.

## Considered Options

- Amazon RDS for PostgreSQL
- MySQL
- MongoDB

## Decision Outcome

Chosen option: Amazon RDS for PostgreSQL, because Approved stack. Everything tracked is structured and related (users, targets, meals, items, portions, weight history, curated catalogue). Postgres full-text search powers Indian-dish and alias lookups without a separate search service, and versioned targets plus denormalised item values keep past-day totals correct while catalogue data evolves.

## Consequences

Full-text search covers the launch catalogue well; if fuzzy/multilingual matching is needed later, pg_trgm or a dedicated search engine can be added without schema change.
<!-- sdlc:auto:end adr -->