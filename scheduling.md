# workload scheduling

## Related terms

Node Selector, Node affinity, Pod Affinity, Taints, Tolerations

## Pod scheduling

for a example pod config:

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: api
spec:
    contianers:
    - name: api
      image: api:v1
      resources:
        requests:
          cpu: "2"
          memory: "4Gi"
```

when we apply this config, scheduler in control plane:

1. Filter out node that meet the resource request -> feasible nodes
2. Score across feasible nodes and choose the highest one
3. Bind, create the pod with containers in the selected node

In a cluster, there might be:

1. windows nodes
2. high-cpu nodes
3. high-memory nodes
4. spot nodes
5. arm nodes
6. GPU nodes
7. Storage(SSD) nodes

And for a default cluster, it might not able to decide the best place to run the pods, so we can give k8s some extra instructions to help it.

## Node selector

for example:
In node config file:
  kubeletExtraArgs.node-labels = "key0=value0,environment=production,region=us-west"

And In deployment/stateful set/job/other objects:
  spec.nodeSelector:
    environment: production

## Node affinity

In node config, taints are used to specified the key/value pairs
  [ref]<https://kubernetes.io/docs/reference/config-api/kubeadm-config.v1beta3/#kubeadm-k8s-io-v1beta3-NodeRegistrationOptions>

And In deployment/stateful set/job/other objects:
  spec.nodeSelector.{[key,value]}
  For node affinity, there are:
  **affinity.nodeAffinity.requiredDuringSchedulingIgnoreDuringExecution**

  1. wont reschedule execution pods
  2. wont schedule pods if not preferences not matched (pending)

  **affinity.nodeAffinity.preferredDuringSchedulingIgnoreDuringExecution**

  1. wont reschedule execution pods
  2. still schedule pods if not preferences not matched

## pod affinity

Deploy pods at node as possible to reduce latency if different pods need to communicate with each other
In deployment/stateful set/job/other objects:
  **affinity.podAffinity.requiredDuringSchedulingIgnoreDuringExecution**
  **affinity.podAffinity.preferredDuringSchedulingIgnoreDuringExecution**
**warning: namespace**

## pod anti-affinity

Deploy pods at different node as possible to reduce impact of nodes going down, frequently used in deploying Nginx and other ingress controllers
In deployment/stateful set/job/other objects:
  **affinity.podAntiAffinity.requiredDuringSchedulingIgnoreDuringExecution**
  **affinity.podAntiAffinity.preferredDuringSchedulingIgnoreDuringExecution**
**warning: all nodes should have the same key: topologyKey: "kubernetes.io/hostname"**

## taints & toleration

For example, when scheduling non control plane pods on control node, you may get warning:

`Warning  FailedScheduling  4m30s (x4 over 19m)  default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node-role.kubernetes.io/control-plane: }. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.`

indicates that the scheduler is unable to schedule pods because the only available node has a taint that prevents the pods from being scheduled on it.
The taint is:

```yaml
# Taints: key=value:effect
taints:
  - key: "node-role.kubernetes.io/control-plane"
    value: null
    effect: NoSchedule
```

To resolve this, you can remove the taint

`kubectl taint nodes <control-plane-node-name> node-role.kubernetes.io/control-plane:NoSchedule-`

or

add a new node

or

Edit the pod spec to add the NoSchedule toleration

In the case of deploying ArgoCD plugin, the best practice is to deploy ArgoCD pods in worker node,
ensures the control-plane components are isolated and have dedicated resources.

[ref](https://www.youtube.com/watch?v=rX4v_L0k4Hc)