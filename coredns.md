# Coredns pending, node NotReady

Events:
  Type     Reason            Age                  From               Message
  ----     ------            ----                 ----               -------
  Warning  FailedScheduling  96s (x73 over 6h2m)  default-scheduler  0/2 nodes are available: 2 node(s) had untolerated taint {node.kubernetes.io/not-ready: }. preemption: 0/2 nodes are available: 2 Preemption is not helpful for scheduling.

CoreDNS wont run without network add-on
```bash
kubectl apply -f calico.yaml
kubectl get pods -A --watch
```