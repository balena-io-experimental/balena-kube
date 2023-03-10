# balena-kube

Run a Kubernetes cluster on balenaCloud via k3s!

## Remote development

There is a bastion host with a pre-configured kubectl binary on every agent.

Just open a terminal in the `kubectl` service via the balenaCloud dashboard or run

```bash
balena ssh $UUID kubectl
```

## Local development

If you have local access to the IP of the server, you can use your workstation to run kubectl commands.

First, copy the configuration from the server to your workstation. Keep this file secure!

```bash
SERVER_IP=192.168.1.167
echo 'cat /etc/rancher/k3s/k3s.yaml' | balena ssh "${SERVER_IP}" agent | sed "s/127.0.0.1/${SERVER_IP}/" > k3s.yaml
```

Then set your kubectl config path and run any commands.

```bash
export KUBECONFIG="${PWD}/k3s.yaml"
kubectl get nodes
```
