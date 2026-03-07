---
name: production-context
description: Get production context while coding — what changed recently, what broke before, what depends on what. Use when the user asks about a service, wants to understand recent changes, or needs production knowledge to make better code decisions.
---

# Production Context

Code with production context. Know what's happening in production without leaving your IDE.

## When to Use

- User asks "what changed in X recently?"
- User is debugging and needs to know what happened in production
- User wants to understand how a service behaves in production
- Before refactoring shared code — check what depends on it
- When correlating a code change with production behavior

## Instructions

### 1. Find the service

```
nofire_search_entities(name="<service>", cluster="prod")
```

### 2. Check what changed

```
nofire_get_entity_changes(entity_name="<service>", cluster="prod", hours=24)
```

Returns infrastructure changes (deployments, config updates, scaling, restarts) and correlated VCS activity (commits, PRs) in the same time window. Use commit SHAs to search the codebase for the actual code diff.

### 3. Check if it broke before

```
nofire_find_related_incidents(entity_name="<service>", cluster="prod", days=30)
```

Shows past investigations and root cause patterns. Useful for understanding recurring issues before introducing new changes.

### 4. Understand dependencies

```
nofire_get_entity_dependencies(entity_name="<service>", cluster="prod")
```

Shows upstream and downstream connections. Helps assess whether a change in one service affects others.

### 5. Cluster-wide view

When the user doesn't name a specific service or wants a broader picture:

```
nofire_get_cluster_summary(cluster="prod", hours=6)
nofire_get_recent_deploys(cluster="prod", hours=6)
```

### 6. Connect to code

Use commit SHAs and PR references from changes to search the codebase. This bridges production events back to the code that caused them.
