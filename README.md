# Homelab

Here lies my homelab, which is a self-hosted two node kubernetes cluster.  I have 
been wanting to do this for a long time, and am pleased with the result.

This repo contains GitOps ArgoCD application manifests for all applications that I 
host on my cluster and an ansible install of the full cluster.

A more detailed report can be found on my [blog](https://gradyarnold.com/blog/folder/homelab)

## Stack

### Cluster

* [K3s](https://k3s.io/)
* [Cilium](https://github.com/cilium/cilium)
* [Longhorn](https://longhorn.io/)
* [NVIDIA](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/index.html)
* [Tailscale](https://tailscale.com/kb/1185/kubernetes)

### Observability/CD

* [Hubble](https://github.com/cilium/hubble)
* [ArgoCD](https://argo-cd.readthedocs.io/)
* [Grafana / Prometheus](https://prometheus.io/docs/visualization/grafana/)

### Applications

* [Postgresql](https://www.postgresql.org/) - [helm](https://github.com/bitnami/charts/tree/main/bitnami/postgresql)
* [MLflow](https://mlflow.org/) - [helm](https://github.com/community-charts/helm-charts/tree/main/charts/mlflow)
* [Minio](https://min.io/) - [helm](https://github.com/minio/minio/blob/master/helm/minio/README.md)
* [Filestash](https://www.filestash.app/) - [helm](https://github.com/sebagarayco/helm-filestash/tree/master/charts/filestash)
* [Dashy](https://dashy.to/) - [helm](https://github.com/vyrtualsynthese/selfhosted-helmcharts/tree/main/charts/dashy)

## Usage

### Deps

```bash
ansible-galaxy collection install community.kubernetes
```

### Install

```yaml
# values.yaml
tailscale_client_id: 
tailscale_client_secret:
```

```ini
# inventory
[main]
private-cloud-1  ansible_connection=ssh

[agent]
private-cloud-2  ansible_connection=ssh
```

```bash
ansible-playbook ansible/install.yaml -i inventory -e @values.yaml --ask-become-pass 
```
