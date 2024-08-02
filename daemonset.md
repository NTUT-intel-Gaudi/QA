# Daemonset

A DaemonSet ensures that all (or some) Nodes run a copy of a Pod.
Some typical uses of a DaemonSet are:

- running a cluster storage daemon on every node
- running a logs collection daemon on every node
- running a node monitoring daemon on every node

for NVIDIA GPU nodes, nvidia-device-plugin.yml is used with tolerant key nvidia.com/gpu

[text](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)