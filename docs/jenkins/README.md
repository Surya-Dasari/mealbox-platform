# MealBox Backend Jenkinsfile Template

This Jenkinsfile is the **gold standard** for all backend services.

## Mandatory Features
- Multibranch pipeline
- SNAPSHOT artifact support
- Docker build with --no-cache (prevents stale JARs)
- Helm-based OpenShift deployment
- Actuator health endpoint support

## Service-specific changes
Only update:
- SERVICE_NAME
- IMAGE_NAME
- VALUES_FILE

Nothing else should be modified per service.

