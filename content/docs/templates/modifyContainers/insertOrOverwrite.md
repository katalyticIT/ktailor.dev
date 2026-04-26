---
title: "insertOrOverwrite"
weight: 20
pre: "/templates/modifycontainers/insertifnotexists/"
next: "/templates/modifycontainers/setorappend/"
---


This operation forcefully adds the specified elements. If an element with the same name already exists in the container, its value will be **overwritten** by the template's value. 

> **Reminder**: Define the `env` and `volumeMounts` **exactly** as you would in a standard Kubernetes manifest.

## Example

```yaml
modifyContainers:
  insertOrOverwrite:
    env:
      - name: FAKETIME
        value: "+222d"
```
