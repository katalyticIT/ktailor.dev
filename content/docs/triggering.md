---
title: "Triggering the Webhook"
weight: 50
prev: templates/_index.md
---


The mutation is triggered by adding a specific label to the **Deployment** metadata.

## Label Syntax

Add the following label to the metadata section of your deployment:
`ktailor.dev/fit: <scope>.<templateName>`

- `<scope>`: Either `central` or `local`:
  - `central`: The ConfigMap is deployed in kTailors namespace.
  - `local`: The ConfigMap is deployed in the apps namespace.
  - If neither `central` or `local` is given, then the webhook bypasses the deployment without modification.
- `<templateName>`: The name of the ConfigMap containing the template.

### Example: Deployment Trigger
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
  labels:
    ktailor.dev/fit: "central.libfaketime-plus222d"
spec:
  ...
```

## Manual triggering

You can trigger the webhook at any time to redeploy the deployment while
being modified according to the template specified. You just have to add
the label on the command line, e.g.:

```
kubectl label --overwrite deployment my-deployment ktailor.dev/fit="central.my-template"
```

This line adds the label to the deployment which triggers the webhook. If the template
leads to any changes in the deployment description, then new pods are spawned.
