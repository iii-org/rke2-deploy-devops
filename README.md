# rke2-deploy-devops(下列需以ROOT)

## 警告: /etc/hosts內一定要有Node的IP!!和rke2雖然是rancher的, 但是由於下方安裝的rancher版本老舊因此在rancherUI會無法識別為rke2 goverment, 在後續的版本可讀出為rke goverment
sonarqube: 修改nano /etc/sysctl.conf至需求大小 vm.max_map_count=262144

## ADD ENV
```sh
nano /etc/environment
append->:/var/lib/rancher/rke2/bin:/snap/bin
add->KUBECONFIG="/etc/rancher/rke2/rke2.yaml"

#export KUBECONFIG=/etc/rancher/rke2/rke2.yaml PATH=$PATH:/var/lib/rancher/rke2/bin
#export PATH=$PATH:/snap/bin

```

## Install rke2
```sh
curl -sfL https://get.rke2.io | sh -
systemctl enable rke2-server.service
systemctl start rke2-server.service
# Wait a bit
kubectl get nodes
# for k8s self-cert or http01 dns method
kubectl create ns cert-manager
# create ns for manage install easy
kubectl create ns devops
```

## (選擇性, 可選擇任何的公私有雲的儲存空間) Install NFS and storageclass for iiidevops
```sh
apt install nfs-kernel-server -y
mkdir /var/iiidevopsNFS
chmod -R 777 /var/iiidevopsNFS
修改 /etc/exports 添加 /var/iiidevopsNFS *(no_root_squash,rw,sync,no_subtree_check)
systemctl restart nfs-kernel-server
showmount -e 10.20.0.68
接下來進入到nfsXXX的那個資料夾裡面有寫詳盡的說明
```

## Install cert-manager as Share Service
```sh
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.0.4/cert-manager.crds.yaml
helm install cert-manager jetstack/cert-manager --namespace cert-manager --version v1.0.4
```
## Install rancher
```sh
helm install rancher rancher-stable/rancher -n devops --set hostname=rancher.10.20.0.68.xip.io --set replicas=1 --version 2.4.5
```

## 參考來源
* [rke2](https://github.com/rancher/rke2)
* [iii-org/devops-lite-test](https://github.com/iii-org/devops-lite-test)
