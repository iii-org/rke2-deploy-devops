

## 安裝通用的資料庫與網頁管理介面
```sh
helm install -n devops db bitnami/postgresql -f ./share-postgresql-install.yaml
helm install -n devops share-redis bitnami/redis -f ./share-redis-install.yaml
# 非需要安裝的 下面僅是安裝網頁管理介面用於證明資料有儲存而已
helm install -n devops db-gui cetic/adminer
```

## 安裝harbor、sonarqube、redmine
```sh

```
