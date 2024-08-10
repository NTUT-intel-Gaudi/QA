# Container runtime interface (CRI)

## Configure containerd cri

containerd vs containerd.io

## [ERROR CRI]: container runtime is not running

output: time="2024-07-11T18:07:23+08:00" level=fatal msg="validate service connection: validate CRI v1 runtime API for endpoint \"unix:///var/run/dockershim.sock\": rpc error: code = Unavailable desc = connection error: desc = \"transport: Error while dialing: dial unix /var/run/dockershim.sock: connect: no such file or directory\"

Docker Engine does not implement the CRI to work with Kubernetes, so an additional service *cri-dockerd*, which is removed from the kubelet in version 1.24.

in my case, containerd was installed and used as a container runtime interface

ref: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#installing-runtime