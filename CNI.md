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