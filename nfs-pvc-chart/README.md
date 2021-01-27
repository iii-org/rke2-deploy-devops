```sh
helm repo add ckotzbauer https://ckotzbauer.github.io/helm-charts

mkdir /var/iiidevopsNFS
chmod -R 777  /var/iiidevopsNFS
helm install iiidevops-nfs -n devops -f ./nfs-iiidevops-storage.yaml ckotzbauer/nfs-client-provisioner
```

