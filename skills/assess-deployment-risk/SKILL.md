---
name: assess-deployment-risk
description: Assess deployment risk before merging. Discovers affected services, scores risk, checks blast radius, and reviews recent incidents. Use before any production code merge or when asked about deployment safety.
---

# Assess Deployment Risk

See what breaks before it does. This skill checks if your changes are safe to deploy.

## When to Use

- Before merging a PR that touches production code
- When asked "is this safe to deploy?"
- After modifying service configuration or dependencies
- Before suggesting a deployment strategy

## Instructions

### 1. Identify the affected service

Look at the files being changed and determine which service(s) they belong to. Search NOFire to confirm:

```
nofire_search_entities(name="<service-name>", cluster="prod")
```

If unsure which service, search by partial name. NOFire supports fuzzy matching.

### 2. Score deployment risk

```
nofire_assess_deployment_risk(entity_name="<service>", cluster="prod")
```

Report the risk score and level to the user:
- **LOW (0-39)**: Safe for standard deployment.
- **MEDIUM (40-59)**: Recommend canary rollout (10% → 50% → 100%).
- **HIGH (60-79)**: Staged rollout required. Deploy during business hours.
- **CRITICAL (80-100)**: Peer review + feature flags. Never deploy Fridays.

### 3. For HIGH or CRITICAL, check blast radius

```
nofire_analyze_blast_radius(entity_name="<service>", cluster="prod")
```

Show which downstream services would be affected by a failure.

### 4. Check for recent incidents

```
nofire_find_related_incidents(entity_name="<service>", cluster="prod", days=30)
```

Warn if the service had recent failures — deploying into an unstable service compounds risk.

### 5. Summarize for the user

Present: risk score, affected services, blast radius (if high risk), recent incidents, and a recommended deployment strategy.
