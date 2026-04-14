# helm-charts

## Advantages
1. We can templatise the kubernetes manifest file
2. We can use as a package manager

### Helm Charts templatise
- If we have manifest file, we can configure the frequently changed values through helm charts
- Helm charts will maintain the required kubernetes structure as a template and configure the values at runtime.
- Rollback is pretty simple in helm as it maintain the revision of each install/deployment

### Folder structure 
1. Chart.yaml -> It defines the Chart version, Name of the chart and etc for the required module.
2. values.yaml -> contains the actual values to configure for the templates ar runtime
3. templates/ folder -> all kubernetes files here with placeholders
4. templates/deployment.yaml
5. templates/service.yaml
6. templates/configmap.yaml
7. and etc


### Install Helm

```shell
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh

helm version
```

### Helm commands

```shell
kubectl create namespace roboshop
kubens roboshop

helm install <chart-name> .               -> First time install the app
helm list                                 -> list of the charts installed
helm uninstall <chart-name>               -> removes the app
helm histroy <chart-name>                 -> to see the histroy of the revision of the same app
helm upgrade --install <chart-name> .     -> Upgrade the app, otherwise, install the app
helm upgrade --install <chart-name> --set deployment.imageVersion="<value>"  --version 0.0.1 --description "Upgrading to new image"
helm rollback <chart-name>                -> rollback to previous version
helm rollback <chart-name>  2             -> rollback to specific version 2
```

## Helm-Roboshop

### Mongodb

```shell
$ helm upgrade --install mongodb .
Release "mongodb" does not exist. Installing it now.
NAME: mongodb
LAST DEPLOYED: Tue Apr 14 11:44:30 2026
NAMESPACE: roboshop
STATUS: deployed
REVISION: 1
TEST SUITE: None

$ helm list
NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
mongodb roboshop        1               2026-04-14 11:44:30.189137373 +0000 UTC deployed        mongodb-0.0.1


$ kubectl get pods
NAME                       READY   STATUS    RESTARTS   AGE
mongodb-5f5cd96878-hpljh   1/1     Running   0          71s

$ kubectl get deployment
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
mongodb   1/1     1            1           82s

$ kubectl get service
NAME      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)     AGE
mongodb   ClusterIP   10.100.182.86   <none>        27017/TCP   89s

```


### Catalogue

```shell
$ helm upgrade --install catalogue .
Release "catalogue" does not exist. Installing it now.
NAME: catalogue
LAST DEPLOYED: Tue Apr 14 12:00:42 2026
NAMESPACE: roboshop
STATUS: deployed
REVISION: 1
TEST SUITE: None
```

### Redis

```shell
$ helm upgrade --install redis .
Release "redis" does not exist. Installing it now.
NAME: redis
LAST DEPLOYED: Tue Apr 14 12:11:11 2026
NAMESPACE: roboshop
STATUS: deployed
REVISION: 1
TEST SUITE: None

```

### User
```shell
$ helm upgrade --install user .
Release "user" does not exist. Installing it now.
NAME: user
LAST DEPLOYED: Tue Apr 14 12:18:10 2026
NAMESPACE: roboshop
STATUS: deployed
REVISION: 1
TEST SUITE: None
```

### Cart
```shell
$ helm upgrade --install cart .
Release "cart" does not exist. Installing it now.
Error: 1 error occurred:
        * ConfigMap in version "v1" cannot be handled as a ConfigMap: json: cannot unmarshal number into Go struct field ConfigMap.data of type string


Add quotes to numeric values ex: at configmap.yaml see CATALOGUE_PORT: "{{ .Values.configMap.CATALOGUE_PORT }}"


 helm upgrade --install cart .
Release "cart" does not exist. Installing it now.
NAME: cart
LAST DEPLOYED: Tue Apr 14 12:33:10 2026
NAMESPACE: roboshop
STATUS: deployed
REVISION: 1
TEST SUITE: None

```

### MySql

````shell

````