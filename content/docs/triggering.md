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
