---
title: "addInitContainers"
weight: 50
pre: "/templates/modifycontainers/remove/"
next: "/templates/addcontainers/"
---


This phase injects entirely new Initialization Containers (`initContainers`) into the Pod specification.

> **Important Note**: The container definitions you provide here must be written **exactly as they are in a standard Kubernetes Deployment manifest**. All standard fields like `image`, `command`, `env`, and `volumeMounts` are fully supported.

## Example

```yaml
addInitContainers:
  - name: inject-libfaketime
    image: katalytic/libfaketime_init:1.0
    imagePullPolicy: IfNotPresent
    env:
      - name: LFT_DESTPATH
        value: /lft_volume
    volumeMounts:
      - name: shared-lft-volume
        mountPath: /lft_volume
```
