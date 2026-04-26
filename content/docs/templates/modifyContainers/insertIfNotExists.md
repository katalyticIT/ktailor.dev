---
title: "insertIfNotExists"
weight: 10
pre: "/templates/modifycontainers/"
next: "/templates/modifycontainers/insertoroverwrite/"
---


This operation adds the specified elements (like environment variables or volume mounts) **only if they do not already exist** in the target container. If the container already defines an element with the same name, kTailor will leave the original value intact.

> **Reminder**: Define the `env` and `volumeMounts` **exactly** as you would in a standard Kubernetes manifest.

## Example

```yaml
modifyContainers:
  insertIfNotExists:
    env:
      - name: LOG_LEVEL
        value: "INFO"
    volumeMounts:
      - name: config-volume
        mountPath: /etc/config
```
