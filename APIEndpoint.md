# InitConfiguration.localAPIEndpoint vs ClusterConfiguration.controlPlaneEndpoint

localAPIEndpoint represents the endpoint of the API server instance that's deployed on this control plane node.

In HA setups, this differs from ClusterConfiguration.controlPlaneEndpoint in the sense that controlPlaneEndpoint is the global endpoint for the cluster, which then load-balances the requests to each individual API server. This configuration object lets you customize what IP/DNS name and port the local API server advertises it's accessible on. By default, kubeadm tries to auto-detect the IP of the default interface and use that, but in case that process fails you may set the desired value here.
