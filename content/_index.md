---
title: Modify your pods but not your deployments.
toc: false
---

<p style="text-align:center;font-size:14pt;">With nothing more than a configmap.</p>

## What is kTailor?

kTailor is a lightweight and blazing-fast Kubernetes **Mutating Webhook** that
dynamically modifies Deployments *on the fly*. By utilizing simple, reusable
YAML templates stored in ConfigMaps, it effortlessly injects sidecars,
environment variables, or volumes *without* requiring changes to the original
source manifests.

## How does it work - in short?

All your deployment needs is a special label which triggers kTailor to
modify it according to the specified template - which is simply stored
in a configmap in your applications namespace or kTailors own namespace.

If you know how to write a deployment, then you know how to write a kTailor
template. *No specific programming language, no steep learning curve. Just YAML.*

## Do you have a simple example?

Sure. Let's inject a proxy setting into a container. The template would look
like this:

```yaml
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: set-http-proxy
  labels:
    ktailor.io/template: "true"
data:
  template: |
    ---
    modifyContainers:
      insertOrOverwrite:
        env:
          - name: http_proxy
            value: http://yourProxy-ip:port/
```

The kTailor webhook transparently inserts (or overwrites) the environment variable
and the binary in the pod will then use the proxy for HTTP connections.

Easy, quick, done.

## What does it need to run kTailor?

Just an own namespace and a bit of memory for a couple of kTailor pods.

kTailor uses *no database*, reducing latency and dependencies, thus making
it *reliable and real fast*. The templates are stored in plain configmaps,
making it easy to make them part of your CICD process.


## Explore

{{< cards >}}
  {{< card link="docs" title="Docs" icon="book-open" >}}
  {{< card link="https://github.com/katalyticIT/kTailor" title="Github" icon="book-open" >}}
{{< /cards >}}

