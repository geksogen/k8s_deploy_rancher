# Deploy k8s

## Pre requirements
* 3 VPS (CPU 2: RAM 4gb: HDD 40gb)
* Ubuntu 18
* Docker on each hosts

## Generate and copy ssh key on each host
```BASH
ssh-keygen
ssh-copy-id root@<ip each host>
```

## Install RKE CLI
```BASH
curl -s https://api.github.com/repos/rancher/rke/releases/latest | grep download_url | grep amd64 | cut -d '"' -f 4 | wget -qi -
chmod +x rke_linux-amd64
sudo mv rke_linux-amd64 /usr/local/bin/rke
rke --version
```
## Config cluster
To configure the future cluster, you need to fill in the cluster_conf.yml file.
```BASH
rke up
```

## Install kubectl
```BASH
kubectl --kubeconfig kube_config_cluster.yml get nodes
mkdir ~/.kube/
cat kube_config_cluster.yml >~/.kube/k8s-hls &
export KUBECONFIG=$(find ~/.kube -maxdepth 1 -type f -name '*' | tr "\n" ":")
```

## Referens
[Rancher Doc](https://rancher.com/docs/rke/latest/en/example-yamls/#minimal-cluster-yml-example)