---
title: "addVolumes"
weight: 70
pre: "/templates/addcontainers/"
next: "/triggering/"
---


This phase attaches entirely new volumes to the Pod specification, which can then be mounted by your containers or init containers.

> **Important Note**: The volume definitions must be written **exactly as they are in a standard Kubernetes Deployment manifest**. Whether it's an `emptyDir`, `configMap`, `secret`, or `persistentVolumeClaim`, the native Kubernetes syntax applies.

## Example

```yaml
addVolumes:
  volumes:
    - name: shared-lft-volume
      emptyDir: {}
    - name: custom-config
      configMap:
        name: my-app-config
```
