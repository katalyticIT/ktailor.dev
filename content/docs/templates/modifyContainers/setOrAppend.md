---
title: "setOrAppend"
weight: 30
pre: "/templates/modifycontainers/insertoroverwrite/"
next: "/templates/modifycontainers/remove/"
---


This operation adds the specified element. However, if the element already exists, the new value is **appended** to the existing one. You can optionally specify a `separator` (like a colon `:` or comma `,`).

This is particularly useful for variables like `LD_PRELOAD` or `PATH`.

> **Reminder**: The basic structure mirrors standard Kubernetes manifests, but we introduce a custom `separator` field for this specific operation.

## Example

```yaml
modifyContainers:
  setOrAppend:
    env:
      - name: LD_PRELOAD
        value: "/lft_volume/libfaketime.so.1"
        separator: ":"
```
