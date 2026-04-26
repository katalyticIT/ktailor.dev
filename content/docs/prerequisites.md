---
title: "Prerequisites"
weight: 10
prev: _index.md
next: installation.md
---


To run **kTailor**, your environment must meet the following requirements:

1. **Kubernetes Cluster**: A running cluster (v1.19+ recommended).
2. **cert-manager** (or similar): Installed in the cluster to manage TLS certificates for the webhook.
3. **Build Tools**:if you want to build the image from scratch, you need the following tools.
   - **Go**: v1.21+ (if building from source).
   - **Docker**: For container image creation.

### Installing cert-manager

Mutating webhooks need to offer an encrypted transport because for reasons of security
kubernetes always communicates with webhooks over secure connections. The integrated
webserver therefore needs a TLS certificate. To make things easy, it's recommended
to use a certificate issued by a cluster-internal issuer instance.

If your cluster has no internal certificate manager, then you may install the
cloud native tool [cert-manager](https://cert-manager.io/). It provides dynamic
generation and management of certificates, making secure deployments easy where
you don't have to worry about certificate life cycles etc.

```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.13.0/cert-manager.yaml
```
