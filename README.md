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

```
