---
title: "addContainers"
weight: 60
pre: "/templates/addinitcontainers/"
next: "/templates/addvolumes/"
---


This phase injects new sidecar containers into the Pod specification alongside your existing application containers.

> **Important Note**: The container definition must be written **exactly as it is in a standard Kubernetes Deployment manifest**. 

## Example

```yaml
addContainers:
  - name: prometheus-exporter-sidecar
    image: prom/node-exporter:v1.3.1
    ports:
      - containerPort: 9100
        name: metrics
```
