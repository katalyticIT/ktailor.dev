---
title: "modifyContainers"
weight: 10
pre: "/templates/"
next: "/templates/modifycontainers/insertifnotexists/"
---


The `modifyContainers` phase iterates through all existing containers in your Deployment and applies specified changes. 

It supports four distinct operations to give you precise control over how environment variables and volume mounts are handled.

> **Important**: The syntax for `env` and `volumeMounts` within these operations is **identical** to standard Kubernetes Pod specifications.
