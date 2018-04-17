# Kubernetes workshop

## For masters

### Install helm

```bash
kubectl create serviceaccount tiller --namespace default
kubectl create clusterrolebinding tiller --clusterrole=cluster-admin --serviceaccount=default:tiller
helm init --service-account tiller --tiller-namespace=default
```

### Install nginx ingress controller

```bash
helm install stable/nginx-ingress --set rbac.create=true --set controller.service.type=ClusterIP --tiller-namespace=default
```

## For students

### Install kubectl configuration

Someone will supply you with a configuration file.

Place it in a suitable location, such as `~/.kube/workshop_config`.

Point the environment variable `KUBECONFIG` to your configuration

```bash
export KUBECONFIG=$HOME/.kube/workshop_config
```

Check with kubectl that the configuration works

```bash
kubectl config view
```

## (Optional) Install helm binary

Get the binary from `tools/k8s/helm` in this repo.

Make it executable, place it somewhere, and add that somewhere to `PATH`.

## Enable our local docker registry

### Linux

```bash
sudo nano /etc/docker/daemon.json
```

Insert this content:

```
{
  "insecure-registries" : ["ubuntu-k8s-1:30603"]
}

```

Then:

```bash
systemctl restart docker
```
