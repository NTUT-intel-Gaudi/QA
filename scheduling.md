# workload scheduling

## workload scheduling in control node

when scheduling non control plane pods on control node, you may get warning:

`Warning  FailedScheduling  4m30s (x4 over 19m)  default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node-role.kubernetes.io/control-plane: }. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.`

indicates that the scheduler is unable to schedule pods because the only available node has a taint that prevents the pods from being scheduled on it.
The taint is **node-role**. 
kubernetes.io/control-plane:NoSchedule is applied to control plane nodes by default to prevent non-control plane workloads from being scheduled on them.

To resolve this, you can remove the taint

`kubectl taint nodes <control-plane-node-name> node-role.kubernetes.io/control-plane:NoSchedule-`

or

add a new node

or

Edit the pod spec to add the NoSchedule toleration

In the case of deploying ArgoCD plugin, the best practice is to deploy ArgoCD pods in worker node,
ensures the control-plane components are isolated and have dedicated resources.