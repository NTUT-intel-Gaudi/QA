# Mostly used commands in k8s cluster

## get nodes/pods/services

```bash
# all
kubectl get [nodes/pods/services] [-A/-n <namespace>]
# single
kubectl get [node/pod/service] <name> -n <namespace>
```

## get description

```bash
# all
kubectl describe [nodes/pods/services] [-A/-n <namespace>]
# single
kubectl describe [node/pod/service] <name> -n <namespace>
```

## remove pods with namespace

```bash
# all
kubectl delete [nodes/pods/services] --all -n <namespace>
# single
kubectl delete pod [node/pod/service] <name> -n <namespace>
```
