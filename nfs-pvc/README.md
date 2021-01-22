# 掛載NFS資料(注意效能可能較低，但具可兼容傳統硬碟與可在一般延遲高網路環境運作的優勢)

#### 群集內權限與角色設定
1. `kubectl apply -f ./nfs-client-provisioner-serviceaccount.yaml`
2. `kubectl apply -f ./nfs-client-provisioner-runner-clusterrole.yaml`
3. `kubectl apply -f ./run-nfs-client-provisioner-clusterrolebinding.yaml`
4. `kubectl apply -f ./leader-locking-nfs-client-provisioner-role.yaml`
5. `kubectl apply -f ./leader-locking-nfs-client-provisioner-rolebinding.yaml`
#### pv 
6. `kubectl apply -f ./nfs-client-provisioner-pv.yaml`
#### pvc
7. `kubectl apply -f ./iiidevops-nfs-storage-storageclass.yaml`

#### 驗證安裝
> `kubectl get storageclass`  
```
localadmin@iiidevops-67:~/devops-lite-test/nfs-pvc$ kubectl get storageclass
NAME                              PROVISIONER                 RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
iiidevops-nfs-storage (default)   iiidevops-nfs-provisioner   Delete          Immediate           false                  114s
```

#### 參考連結(僅供參考)
* [NFS或iSCSI哪個更好](https://www.itread01.com/content/1549403289.html)
* [設定 StorageClass (以 NFS 為例) | 小信豬的原始部落](https://godleon.github.io/blog/Kubernetes/k8s-Config-StorageClass-with-NFS/)



