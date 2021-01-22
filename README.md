# rke2-deploy-devops(下列需以ROOT)

## Install rke2
```sh
curl -sfL https://get.rke2.io | sh -
systemctl enable rke2-server.service
systemctl start rke2-server.service
# Wait a bit
export KUBECONFIG=/etc/rancher/rke2/rke2.yaml PATH=$PATH:/var/lib/rancher/rke2/bin
kubectl get nodes
# for k8s self-cert or http01 dns method
kubectl create ns cert-manager
# create ns for manage install easy
kubectl create ns devops
```

## Install helm and list
```sh
snap install helm --classic
export PATH=$PATH:/snap/bin
# cert-manager
helm repo add jetstack https://charts.jetstack.io
# rancher
helm repo add rancher-stable https://releases.rancher.com/server-charts/stable
# bitnami(這裡使用redmine)
helm repo add bitnami https://charts.bitnami.com/bitnami
# harbor
helm repo add harbor https://helm.goharbor.io
```

## (選擇性, 可選擇任何的公私有雲的儲存空間) Install NFS
```
apt install nfs-kernel-server -y
mkdir /var/iiidevopsNFS
chmod -R 777 /var/iiidevopsNFS
修改 /etc/exports 添加 /var/iiidevopsNFS *(no_root_squash,rw,sync,no_subtree_check)
systemctl restart nfs-kernel-server
showmount -e 10.20.0.68
```

## Install cert-manager as Share Service
```
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.0.4/cert-manager.crds.yaml
helm install cert-manager jetstack/cert-manager --namespace cert-manager --version v1.0.4
```

## 參考來源
* [rke2](https://github.com/rancher/rke2)
* [iii-org/devops-lite-test](https://github.com/iii-org/devops-lite-test)
