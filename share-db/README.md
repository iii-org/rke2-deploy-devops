

## 安裝通用的資料庫與網頁管理介面
```sh
helm install -n devops share-postgresql bitnami/postgresql -f ./share-postgresql-install.yaml
helm install -n devops share-redis bitnami/redis -f ./share-redis-install.yaml
```

## 安裝harbor、sonarqube、redmine
```sh
```
