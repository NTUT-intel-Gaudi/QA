# Mostly used commands in k8s cluster

## Reconfiguring a kubeadm cluster

```bash
# edit ClusterConfiguration (vim)
kubectl edit cm -n kube-system kubeadm-config
```

## get nodes/pods/services

```bash
# all
kubectl get [nodes/pods/services/deployments/namespaces] [-A/-n <namespace>]
# single
kubectl get [node/pod/service/deployment/namespace] <name> -n <namespace>

# available tags:
#   nodes: --show-labels
#   -o wide # out with more info
```

## get description

```bash
# all
kubectl describe pods -A > tmp
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

## print join command

kubeadm token create --print-join-command
kubeadm token list

[cheat sheet](https://intellipaat.com/blog/tutorial/devops-tutorial/kubernetes-cheat-sheet/)