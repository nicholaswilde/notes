# Kubernetes

## Pause a pod

`kubectl scale --replicas=0 deployment/<your-deployment>`

## kubectl

### Installation

```
# Ubuntu
$ sudo snap install kubectl --classic
```

### [krew](https://krew.sigs.k8s.io/docs/user-guide/setup/install/)

```shell
(
  set -x; cd "$(mktemp -d)" &&
  curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/krew.tar.gz" &&
  tar zxvf krew.tar.gz &&
  KREW=./krew-"$(uname | tr '[:upper:]' '[:lower:]')_$(uname -m | sed -e 's/x86_64/amd64/' -e 's/arm.*$/arm/' -e 's/aarch64$/arm64/')" &&
  "$KREW" install krew
)
```

```shell
# Update
$ kubectl krew version
```

### [ns](https://github.com/ahmetb/kubectx)

```shell
$ kubectl krew install ns
```

### Short Names List

```shell
$ kubectl api-resources
```

## [knsk](https://github.com/thyarles/knsk)

```shell
$ wget -q https://raw.githubusercontent.com/thyarles/knsk/master/knsk.sh -O - | bash
```

## Config

```shell
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /home/nicholas/.kube/config-turing-pi
$ chmod 600 /home/nicholas/.kube/config-turing-pi
```

## [Change the Reclaim Policy of a PersistentVolume][pv]

List the PersistentVolumes in your cluster:

```shell
kubectl get pv
```

Choose one of your PersistentVolumes and change its reclaim policy:

```shell
kubectl patch pv <your-pv-name> -p '{"spec":{"persistentVolumeReclaimPolicy":"Retain"}}'
```

Apply ROLE label to worker nodes [(#379)].

```shell
kubectl label node worker-02 node-role.kubernetes.io/worker=worker
NAME          STATUS   ROLES    AGE    VERSION
turing-main   Ready    master   106m   v1.19.9+k3s1
worker-07     Ready    worker   105m   v1.19.9+k3s1
worker-06     Ready    worker   105m   v1.19.9+k3s1
worker-05     Ready    worker   105m   v1.19.9+k3s1
worker-04     Ready    worker   105m   v1.19.9+k3s1
worker-03     Ready    worker   105m   v1.19.9+k3s1
worker-02     Ready    worker   105m   v1.19.9+k3s1
```

## [Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## Resources

* [keel](https://keel.sh/)
* [flux2](https://toolkit.fluxcd.io/)
* [rook ceph](http://rook.io)
* [k3s](https://k3s.io/)
* [taskfile](https://taskfile.dev/#/)
* [helm-docs](https://github.com/norwoodj/helm-docs)
* [OpenEBS](https://openebs.io/)

[pv]: https://kubernetes.io/docs/tasks/administer-cluster/change-pv-reclaim-policy/
[(#379)]: https://github.com/k3s-io/k3s/issues/379
