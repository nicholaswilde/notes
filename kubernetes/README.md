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

## [Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## Resources

* [keel](https://keel.sh/)
* [flux2](https://toolkit.fluxcd.io/)
* [rook ceph](http://rook.io)
* [k3s](https://k3s.io/)
* [taskfile](https://taskfile.dev/#/)
* [helm-docs](https://github.com/norwoodj/helm-docs)
* [OpenEBS](https://openebs.io/)
