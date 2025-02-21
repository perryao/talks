+++
title = "My presentation"
outputs = ["Reveal"]
+++

## K8S Controllers

Steven White

---

{{% section %}}

### What is a controller?

- More generic term for "operator"
- Controllers enable you to watch resources / other structured data in K8s and perform custom actions
- Often paried with a custom resource, providing a **declarative** API
- Full integration with K8s tooling, such as `kubectl`

---

### How do controllers work?

- Controllers "watch" types defined in the K8s API
- Reconcile the desired state of an object with the current state in response to changes
- Can be deployed / registered in a cluster just as any other workload

---

### Diagram showing data flowing from controller <-> k8s api

{{% /section %}}

---

{{% section %}}

### What is a CRD?

- **C**ustom **R**esource **D**efinition
- Set of endpoints in the K8s API that store a collection of API objects for a distinct kind
- `Spec` can be anything you want
- Can be versioned, but must provide backward compatibility

---

### What can you do with CRDs?

- Create an "aggregate" resource type for common patterns in your cluster (demo later)
- Perform actions external to your cluster in response to lifecycle actions of resources in your cluster (demo later)
- Many other examples. See [prometheus operator](https://github.com/coreos/prometheus-operator), [nginx ingress controller](https://github.com/kubernetes/ingress-nginx), [istio operator](https://github.com/banzaicloud/istio-operator) for inspiration.

{{% /section %}}

---

{{% section %}}

### Building custom controllers / CRDs

- Several tools are available for building custom kubernetes applications
  - [kubebuilder](https://github.com/kubernetes-sigs/kubebuilder)
  - [operator-sdk](https://github.com/operator-framework/operator-sdk)
  - Others probably
- Most have come to settle on the [controller-runtime](https://github.com/kubernetes-sigs/controller-runtime) as a common set of libraries

{{% /section %}}

---

{{% section %}}

### Aggregate CRD Demo

---

### Aggregate CRD Demo

- We'll create a new CRD, called `MyApp`
- `MyApp` will have an associated controller watching for instances to be created / modified
- The controller will reconcile the `MyApp` spec with the created deployment, service, and ingress objects

---

{{< slide transition="slide-in" transition-speed="fast" >}}

### Aggregate CRD Demo

<pre><code class="hljs yaml" data-trim data-line-numbers="1-2">
apiVersion: 'cn.meetup.com/v1'
kind: MyApp
metadata:
  name: test-app
  namespace: default
spec:
  image: 'nginx:latest'
  port: 80
</code></pre>

---

{{< slide transition="none" transition-speed="fast" >}}

### Aggregate CRD Demo

<pre><code class="hljs yaml" data-trim data-line-numbers="3-5">
apiVersion: 'cn.meetup.com/v1'
kind: MyApp
metadata:
  name: test-app
  namespace: default
spec:
  image: 'nginx:latest'
  port: 80
</code></pre>

---

{{< slide transition="none" transition-speed="fast" >}}

### Aggregate CRD Demo

<pre><code class="hljs yaml" data-trim data-line-numbers="6-8">
apiVersion: 'cn.meetup.com/v1'
kind: MyApp
metadata:
  name: test-app
  namespace: default
spec:
  image: 'nginx:latest'
  port: 80
</code></pre>

{{% /section %}}

---

{{% section %}}

### Notification Demo

- We'll deploy a controller only, no CRD
- This controller will watch for new deployment objects to be created and send a SMS in response
- Hope is to demonstrate that controllers are not limited to in cluster functionality

---

### Diagram showing data flowing from k8s api <-> controller <-> twilio API

{{% /section %}}

---

# Thank you!
