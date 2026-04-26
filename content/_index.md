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

## Why kTailor?

In modern Kubernetes environments, developers often need to inject standard infrastructure components (like monitoring sidecars, proxy configurations, or specific environment variables) into their applications. Instead of cluttering every single Deployment manifest, kTailor centralizes these modifications.

kTailor strictly follows the **KISS principle** (Keep It Smart & Simple). It is designed to be:

* **Small & Fast:** Written in Go, it utilizes an efficient In-Memory Informer Cache to observe templates. It introduces near-zero latency to your deployment process.
* **Efficient:** It only targets Deployments carrying a specific trigger label and skips everything else.
* **Easy to Use:** Templates are written in plain Kubernetes-like YAML. No complex programming or policy languages are required.

## What can I use it for?

It's for modifying deployments where you cannot or may not modify the deployment
itself or its parts: the code, the image, the helm chart.

It's useful if
* you've got a third-party application which you cannot modify,
* you need to inject a sidecar for internal monitoring,
* you want to use an initContainer to inject a library, e.g. for time travel,
* you want to overwrite an environment variable, e.g. $http_proxy or $CLASSPATH.

## When NOT to use kTailor

If you need highly complex policy enforcement, conditional logic, or want to
mutate/validate a wide variety of Kubernetes resources beyond standard Deployments,
kTailor might be too simple for your use case. In those scenarios, we highly
recommend looking into established policy engines like [Kyverno](https://kyverno.io/)
or [OPA Gatekeeper](https://openpolicyagent.org/docs/latest/kubernetes-introduction/).


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

*No CRD* are to be defined. kTailor works with plain configMaps, reducing
the learning curve.


## Explore

{{< cards >}}
  {{< card link="docs" title="Docs" icon="book-open" >}}
  {{< card link="https://github.com/katalyticIT/kTailor" title="Github" icon="book-open" >}}
{{< /cards >}}

