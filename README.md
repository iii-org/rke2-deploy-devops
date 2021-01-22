# rke2-deploy-devops

## Install rke2
```sh
curl -sfL https://get.rke2.io | sh -
systemctl enable rke2-server.service
systemctl start rke2-server.service
# Wait a bit
export KUBECONFIG=/etc/rancher/rke2/rke2.yaml PATH=$PATH:/var/lib/rancher/rke2/bin
kubectl get nodes
```

## Install helm and list
```sh
snap install helm --classic
# cert-manager
microk8s.helm3 repo add jetstack https://charts.jetstack.io
# rancher
microk8s.helm3 repo add rancher-stable https://releases.rancher.com/server-charts/stable
# bitnami(這裡使用redmine)
helm repo add bitnami https://charts.bitnami.com/bitnami
# harbor
helm repo add harbor https://helm.goharbor.io
```


## 參考來源
* [rke2](https://github.com/rancher/rke2)
* [iii-org/devops-lite-test](https://github.com/iii-org/devops-lite-test)
