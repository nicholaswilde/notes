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
