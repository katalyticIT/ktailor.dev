---
title: "Templates Overview"
weight: 40
pre: "/configuration/"
next: "/templates/modifycontainers/"
---

Templates are the heart of kTailor. They are stored as Kubernetes `ConfigMaps` with the label `ktailor.io/template: "true"`.

## Scope: Central vs. Local
* **Central**: The webhook looks for the ConfigMap in its own namespace (usually `ktailor`). These are globally managed.
* **Local**: The webhook looks for the ConfigMap in the target Deployment's namespace.

## The 4 Phases Overview
kTailor applies modifications in four distinct phases:
1.  **modifyContainers**: Alters existing containers.
2.  **addContainers**: Injects new sidecar containers.
3.  **addInitContainers**: Injects initialization containers.
4.  **addVolumes**: Injects new Pod volumes.

> **Important Note**: All elements within these phases (like environment variables, container definitions, volume mounts, and volumes) are written **exactly as they are in a standard Kubernetes Deployment manifest**. You do not need to learn a new syntax!
