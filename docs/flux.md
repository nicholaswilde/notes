# Flux

## Installation

```shell
brew install fluxcd/tap/flux
```

## Getting Started

```shell
# ~/.bashrc or ~/.bash_profile
. <(flux completion bash)
```

Check requirements

```shell
flux check --pre
► checking prerequisites
✔ kubectl 1.18.3 >=1.18.0
✔ kubernetes 1.18.2 >=1.16.0
✔ prerequisites checks passed
```

Run the bootstrap command:

```shell
flux bootstrap github \
  --owner=$GITHUB_USER \
  --repository=home-cluster \
  --branch=main \
  --path=./cluster \
  --personal
```

## Helm

### values.yaml

```yaml
---
nfs:
  path: /home/pi/nas/nfs
  server: 192.168.1.192
storageClass:
  defaultClass: false
  name: managed-nfs-storage
```

### Source

```shell
flux create source helm repo-name-charts \
    --url https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/ \
    --export | tee repo-name-charts.yaml
```

### HelmRelease

```shell
flux create helmrelease \
    chart-name \
    --source HelmRepository/repo-name-charts \
    --values values.yaml \
    --chart chart-name \
    --chart-version chart-version \
    --target-namespace namespace-name \
    --export \
    | tee helm-release.yaml
```

## References

- [Getting Started](https://toolkit.fluxcd.io/get-started/)
