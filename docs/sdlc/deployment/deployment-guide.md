# Deployment Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start how-it-deploys -->
Pushes to `main` run `.github/workflows/deploy.yml`, which builds the API image (if there is a backend) and deploys the SPA to AWS Amplify. Commits touching only `docs/sdlc/**` don't deploy. Deployments can also be started from the platform's Deployment tab.
<!-- sdlc:auto:end how-it-deploys -->

<!-- sdlc:auto:start environments -->
| Name | Service | Runtime | Scaling | Environment |
|---|---|---|---|---|
| Mobile clients | React Native / Expo app | iOS and Android devices | Client-side, distributed via App Store and Play Store | dev |
| Application Load Balancer | AWS ALB | Managed | Managed, single AZ-group | dev |
| FastAPI service | AWS ECS Fargate | Python 3.12 container (uvicorn/gunicorn) | 1-2 tasks for ~1,000 beta users, horizontal if needed | dev |
| PostgreSQL | Amazon RDS for PostgreSQL | Managed PostgreSQL in ap-south-1 | Single instance (db.t3.small) with automated backups | dev |
| Meal photo bucket | Amazon S3 | Managed object storage in ap-south-1 | Elastic | dev |
| Hosted vision model | External GPT-4o / Gemini-class vision API | Third-party managed | Provider-managed, pay per request | dev |
<!-- sdlc:auto:end environments -->

<!-- sdlc:auto:start live -->
_Not deployed yet._
<!-- sdlc:auto:end live -->

<!-- sdlc:auto:start topology -->
```mermaid
graph LR
  n_Mobile_clients["Mobile clients<br/>React Native / Expo app"]
  n_Application_Load_Balancer["Application Load Balancer<br/>AWS ALB"]
  n_FastAPI_service["FastAPI service<br/>AWS ECS Fargate"]
  n_PostgreSQL["PostgreSQL<br/>Amazon RDS for PostgreSQL"]
  n_Meal_photo_bucket["Meal photo bucket<br/>Amazon S3"]
  n_Hosted_vision_model["Hosted vision model<br/>External GPT-4o / Gemini-class vision API"]
  n_Mobile_clients -->|"HTTPS"| n_Application_Load_Balancer
  n_Application_Load_Balancer -->|"HTTPS"| n_FastAPI_service
  n_FastAPI_service -->|"TCP/TLS (5432)"| n_PostgreSQL
  n_FastAPI_service -->|"HTTPS (S3 API)"| n_Meal_photo_bucket
  n_FastAPI_service -->|"HTTPS"| n_Hosted_vision_model
  n_Mobile_clients -->|"HTTPS (pre-signed URL)"| n_Meal_photo_bucket
```
<!-- sdlc:auto:end topology -->
