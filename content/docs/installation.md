---
title: "Installation"
weight: 20
prev: prerequisites.md
next: configuration.md
---

At present, kTailor can only be deployed using the provided `Makefile`. Other installation methods are currently being developed, and documentation for these will follow shortly.

1. **Build and Push**:
   Set your registry and repository variables.
   ```bash
   export IMAGE_RGST=my-registry.io
   export IMAGE_REPO=ktailor
   make docker-build docker-push
   ```

2. **Deploy**:
   This applies RBAC, certificates, and the webhook deployment.
   ```bash
   make deploy
   ```

Run the `make` command without parameter to let it print all parameters available.

### Example: Makefile Build Command
```bash
# Build the local binary
make build
# Build and restart the pod in the cluster
make rollout
```
