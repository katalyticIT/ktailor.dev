---
title: "Installation"
weight: 20
prev: prerequisites.md
next: configuration.md
---

## Installation from scratch

If you like to build your own kTailor image, then you can do so using the provided `Makefile`.

1. **Clone the repository and change the path into it:**
   ```bash
   git clone https://github.com/katalyticIT/kTailor.git
   cd kTailor
   ```

2. **Build and Push**:
   Set your registry and repository variables.
   ```bash
   export IMAGE_RGST=my-registry.io
   export IMAGE_REPO=ktailor
   make docker-build docker-push
   ```

3. **Deploy**:
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

## Installation with manifest

The git repository contains some yaml files that can be used to install kTailor,
using the prebuilt image ```katalytic/ktailor```. Prerequisite is that 
```cert-manager``` is installed.

1. Clone the repository and change the path into it:
```bash
git clone https://github.com/katalyticIT/kTailor.git
cd kTailor/deploy
```

2. Generate the SSL certificates for the webhook:
```bash
kubectl apply -f certs.yaml
```

3. Create the service account and cluster role that are needed for kTailor to enable it to read the configmaps in other namespaces:
```bash
kubectl apply -f rbac.yaml
```
4. Install ktailor with service, configmaps etc.:
```bash
kubectl apply -f manifests.yaml
```

That's all. The following command should show the running kTailor pods:
```bash
kubectl get pods -n ktailor
```

If you want to try kTailor in a sandbox environment first, then try the [killercoda scenario](https://killercoda.com/ktailor-demo).
