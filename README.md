<div align="center">

<img src="https://camo.githubusercontent.com/5b298bf6b0596795602bd771c5bddbb963e83e0f/68747470733a2f2f692e696d6775722e636f6d2f7031527a586a512e706e67" align="center" width="144px" height="144px"/>

### Multi-Cluster Kubernetes Operations Repository

_... managed with Flux, Renovate, and GitHub Actions_ 🤖

</div>

---

## 📖 Overview

This is a mono repository for Hulk AG infrastructure and Kubernetes cluster. We try to adhere to Infrastructure as Code (IaC) and GitOps practices using tools like [Terraform](https://www.terraform.io/), [Kubernetes](https://kubernetes.io/), [Flux](https://github.com/fluxcd/flux2), [Renovate](https://github.com/renovatebot/renovate), and [GitHub Actions](https://github.com/features/actions).

---

## ⛵ Kubernetes

### Repository Structure

Flux watches any folder in `clusters` (see Directories below) and makes the changes to the clusters based on the YAML manifests.

```
.
├── applications
│   ├── base
│   │   ├── echo-server
│   │   │   ├── helmrelease.yaml
│   │   │   ├── kustomization.yaml
│   │   │   └── namespace.yaml
│   │   ├── external-secrets
│   │   │   ├── helmrelease.yaml
│   │   │   ├── kustomization.yaml
│   │   │   └── namespace.yaml
│   │   ├── monitoring
│   │   │   ├── helmrelease.yaml
│   │   │   ├── kustomization.yaml
│   │   │   └── namespace.yaml
│   │   └── podinfo
│   │       ├── helmrelease.yaml
│   │       ├── kustomization.yaml
│   │       └── namespace.yaml
│   ├── dev
│   │   ├── echo-server
│   │   │   └── kustomization.yaml
│   │   ├── external-secrets
│   │   │   ├── kustomization.yaml
│   │   │   └── secret_store.yaml
│   │   ├── monitoring
│   │   │   ├── kube-prometheus-stack.values.yaml
│   │   │   └── kustomization.yaml
│   │   ├── podinfo
│   │   │   ├── kustomization.yaml
│   │   │   └── podinfo.values.yaml
│   │   └── kustomization.yaml
│   └── staging
│       ├── kustomization.yaml
│       └── podinfo.values.yaml
├── clusters                                            # Entrypoint for Kubernetes Clusters
│   ├── infra-kind-dev                                  # Entrypoint for infra-kind-dev
│   │   ├── flux-system                                 # Main Flux Configuration for infra-kind-dev
│   │   │   ├── gotk-components.yaml
│   │   │   ├── gotk-sync.yaml
│   │   │   └── kustomization.yaml
│   │   ├── applications.yaml                           # Kustomization for Applications that are deployed in infra-kind-dev
│   │   ├── cluster-vars.yaml                           # General cluster variables (ConfigMap)
│   │   └── infrastructure.yaml                         # Kustomization for Infrastructure, Components that are needed for cluster functionality
│   └── infra-kind-staging
│       ├── flux-system
│       │   ├── gotk-components.yaml
│       │   ├── gotk-sync.yaml
│       │   └── kustomization.yaml
│       └── applications.yaml
├── infrastructure
│   ├── base
│   │   └── cert-manager
│   │       ├── helmrelease.yaml
│   │       ├── kustomization.yaml
│   │       └── namespace.yaml
│   ├── infra-kind-dev
│   │   └── cert-manager
│   │       ├── clusterissuer.yaml
│   │       ├── kustomization.yaml
│   │       └── secret.sops.yaml
│   └── infra-kind-staging
└── README.md
```

### Infrastructure/Core Components

The `Infrastructure` kustomization defines a set of applications, which are responsible for the cluster functionality. These components are the same on each GKE cluster.

- [autoneg-controller](https://github.com/GoogleCloudPlatform/gke-autoneg-controller/tree/master)
- 

