---
title: NWS@stackconf Hackathon
---

## Briefing

You're the newest addition to the NWS team and are tasked with bringing up the _NWS@stackconf_ website,
which will run on top of Kubernetes.

In your terminal, you've got **admin privileges within your namespace** to fulfill this task,
meaning that you can edit and create pretty much anything within the already configured context
using `kubectl`.

Because this is a production cluster, [Kyverno](https://kyverno.io) is in place to **enforce certain policies** -
unfortunately, the team wasn't able to tell you which exactly from the top of their heads. **You'll have to
see for yourself!**

The team already provided _everything you might need_ for you within the namespace,
especially the `Service` and `Ingress` objects, so that the website will appear on the
correct domain in the end, but it's up to you to get the **website workload up and running.**

```terminal:execute
prefix: Click to Run
title: Display the nws-at-stackconf Service and Ingress
command: |
  kubectl get svc,ingress
```

The last information the team gave you was to use the following `Deployment` blueprint:

```workshop:copy
prefix: Click to Copy
title: Copy the Deployment manifest to your clipboard
text: |
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: nws-at-stackconf
  spec:
    selector:
      matchLabels:
        app: nws-at-stackconf
    replicas: 3
    template:
      metadata:
        labels:
          app: nws-at-stackconf
      spec:
        containers:
          - name: nws-at-stackconf
            image: registry.netways.de/netways-managed-services/devrel/nws-at-stackconf/app:2024
            imagePullPolicy: Always
            ports:
              - containerPort: 8080
                protocol: TCP
                name: http
```

They told you to get back to them with the **code shown on the website** once it is reachable on the web.
