---
title: "Configuration"
weight: 30
prev: installation.md
next: templates/_index.md
---


The webhook is configured via a `ktailor.yaml` file mounted from a ConfigMap which is
currently part of the file `deploy/manifests.yaml`.

## Cluster-Internal Certificates
kTailor relies on **cert-manager** to handle TLS. The deployment includes a `Certificate` resource that cert-manager uses to generate a secret. kTailor then mounts this secret to secure the webhook communication.

## allowCustomTemplates: Security vs. Simplicity

Depending on the nature of your cluster you may want users to be able to write their own templates, e.g.
in development clusters. Or you want all templates to be controlled and managed by the admins. To address
your security concerns kTailor offers the following settings for the variable `allowCustomTemplates`:

* `allowCustomTemplates: true`: Allows users to use "local" templates stored as configmap in their own namespaces. *High flexibility.*
* `allowCustomTemplates: false`: Only "central" templates (managed by admins) are allowed. *Higher security.*

## Namespace Control
You can control which namespaces are processed by the webhook.

### Internal Forbidden List

The following namespaces are managed in an internal list and are *always blocked*:
* `kube-system`
* `kube-node-lease`
* `kube-public`
* `cert-manager`
* and the ktailor namespace itself

### Mode
Define here if you want to allow or deny modifications in the listed namespaces.

* `blocklist`: All namespaces are allowed to be modified except those in the list.
* `allowlist`: Only namespaces in the list are allowed to be modified.

### Custom Lists
Define the namespaces that you want be allowed or denied (depending
on `mode`) in lists under `namespaces.match`.*matchType*. Regex
expressions or similar are not supported. To keep the code simple and robust
and nonetheless make it flexible kTailor works with the 
following three *matchTypes*:

* `exact` - must match the given name exactly
* `startsWith` - must start with one of the listed entries; useful e.g. if you're applying a name convention like `dev-`, `qa-` or `prod-`.
* `endsWith` - must end with one of the listed strings; useful 


## Example: Configuration Snippet

```yaml
namespaces:
  mode: blocklist
  match:
    startsWith: ["dev-", "test-"]
    exact: ["legacy-apps"]
```
