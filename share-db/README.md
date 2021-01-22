

## 安裝通用的資料庫與網頁管理介面
```sh
helm install -n devops db bitnami/postgresql -f ./share-postgresql-install.yaml
helm install -n devops share-redis bitnami/redis -f ./share-redis-install.yaml
# 非需要安裝的 下面僅是安裝網頁管理介面用於證明資料有儲存而已
helm install -n devops db-gui cetic/adminer
```

## 建立資料庫
harbor: `clair`與`registry`
redmine: `redmine`

## 安裝harbor、sonarqube、redmine
```sh
helm install -n devops devops-harbor harbor/harbor -f ./share-harbor-lite-install.yaml
helm install -n devops devops-redmine bitnami/redmine -f ./share-redmine-install.yaml
```


## 資料庫連線
host: `db-postgresql-headless`  
user: `iiidevops`  
pass: `IIIdevops123!`  
