# Overview

Project to manage Flux tasks needed to standardize kubernetes HPC scheduling interfaces

## Maturity Level

<!-- Check one of the values: Sample, Alpha, Beta, GA -->

- [x] Sample (for demonstrating and inspiring purpose)
- [ ] Alpha (used in companies for pilot projects)
- [ ] Beta (used in companies and developed actively)
- [ ] Stable (used in companies for production workloads)

<!-- TODO: write some useful KubeFlux documentation -->

## Quick Start

```bash
git clone https://github.com/kubernetes-sigs/scheduler-plugins.git
cd scheduler-plugins
# build image , you can control the repo, image and tag using 
# LOCAL_REGISTRY=my.repo.example
# LOCAL_IMAGE=kube-scheduler:latest
# If not set they default to local host registry
make local-image
# Edit manifests/kubeflux/deploy.yaml to reflect your repo:image
kubectl apply -f manifests/kubeflux/rbac.yaml
kubectl apply -f manifests/kubeflux/configmap.yaml
kubectl apply -f manifests/kubeflux/deploy.yaml

kubectl get pods -n kube-system | grep flux
```

Once the scheduler-plugin pod is running, you need to select it on the pod spec

```yaml
        spec:
          schedulerName: kubeflux
          containers:
          - image: hello-world:latest
            name: hello-world
```
