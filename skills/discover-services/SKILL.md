---
name: discover-services
description: Discover production services, understand dependencies, and explore infrastructure topology. Use for onboarding, architecture questions, or understanding what runs in production.
---

# Discover Services

Prevent change-driven incidents by understanding what runs in production and how services connect.

## When to Use

- Onboarding to a new codebase or team
- Understanding service architecture and dependencies
- Checking what services exist in a cluster
- Before making changes to shared infrastructure

## Instructions

### 1. Search for services

```
nofire_search_entities(name="<query>", cluster="prod")
```

Supports partial name matching. Omit `cluster` to search across all clusters.

### 2. Map dependencies

For a specific service:

```
nofire_get_entity_dependencies(entity_name="<service>", cluster="prod")
```

Shows upstream (what it depends on) and downstream (what depends on it) services.

### 3. Check available metrics

```
nofire_get_entity_metrics(entity_name="<service>", cluster="prod")
```

Shows available Prometheus metrics and ready-to-use PromQL queries.

### 4. Review recent activity

```
nofire_get_entity_changes(entity_name="<service>", cluster="prod", hours=24)
```

Shows recent deployments, config changes, scaling events, and correlated VCS activity.

### 5. Present clearly

When showing service topology, explain:
- What the service does (infer from name and dependencies)
- What depends on it (blast radius)
- Recent stability (changes, incidents)
- Critical path services to be careful with
