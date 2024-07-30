# CNI (container network interface)

```yaml
# Kubeconfig template for Calico CNI plugin. Installed by calico/node.
apiVersion: v1
kind: Config
clusters:
- name: local
  cluster:
    server: https://10.96.0.1:443
    certificate-authority-data: <long hashed data here>
users:
- name: calico
  user:
    token: <long token here>
contexts:
- name: calico-context
  context:
    cluster: local
    user: calico
current-context: calico-context
```

## issue

sometimes you get

```bash
Warning  FailedCreatePodSandBox  21s                kubelet            Failed to create pod sandbox: rpc error: code = Unknown desc = failed to set up sandbox container "cf45c6c707da0955e90bfacda9e01bf792167a81d7a0e84542047b48e865e09c" network for pod "coredns-7db6d8ff4d-v7mg4": networkPlugin cni failed to set up pod "coredns-7db6d8ff4d-v7mg4_kube-system" network: plugin type="calico" failed (add): error creating calico client: stat /etc/cni/net.d/calico-kubeconfig: no such file or directory
```

and there's nothing under /etc/cni/net.d/, and somehow execute the entrypoint script in branch `v1.0.0` once will solve the issue (pending recreate method and resolve methods)
