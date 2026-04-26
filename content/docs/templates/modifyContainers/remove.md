---
title: "remove"
weight: 40
pre: "/templates/modifycontainers/setorappend/"
next: "/templates/addinitcontainers/"
---


This operation explicitly deletes the specified environment variables or volume mounts from the target container.

> **Reminder**: You must provide the elements as standard Kubernetes objects containing the `name` field, **exactly** as they appear in a Deployment.

## Example

```yaml
modifyContainers:
  remove:
    env:
      - name: UNWANTED_VAR
    volumeMounts:
      - name: unwanted-volume-mount
```
