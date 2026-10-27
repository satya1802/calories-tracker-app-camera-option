<!-- sdlc:auto:start adr -->
# ADR-0001: Use React Native with Expo (iOS and Android) for Frontend

Status: Accepted  
Date: 2026-10-05

## Context and Problem Statement

Which Frontend technology does the project use? Decided in architecture v1.

## Considered Options

- React Native with Expo (iOS and Android)
- Native Swift + Kotlin
- Flutter

## Decision Outcome

Chosen option: React Native with Expo (iOS and Android), because Approved stack. Expo delivers one codebase for both platforms inside the three-month beta and provides the camera, photo-library and permission primitives the capture flow needs; the estimate-review screen (swap dish, adjust portion, add/remove items) is ordinary React form work.

## Consequences

Hosted vision latency is hidden behind a progress indicator with cancel; heavy image handling stays off-device by uploading to the backend rather than processing locally.
<!-- sdlc:auto:end adr -->