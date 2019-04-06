## Start Minikube
![alt text](minikube-start.png "Start Minikube")
```
$ minikube config set memory 10240
$ minikube start
```

## Install Zookeeper
![alt text](helm-install-zookeeper.png "Install Zookeeper")
```
$ helm init
$ helm install bitnami/zookeeper \
--set replicaCount=3
```
You may need to run `helm repo add bitnami https://charts.bitnami.com`
to add bitnami's repo.

## Deploy Nifi
```
$ kubectl create -f https://raw.githubusercontent.com/whs-dot-hk/kubernetes-nifi-refined/master/nifi-statefulset-minikube-cluster.yaml
```
![alt text](kubectl-get-po.png "Get Pods")

## Deploy Frontend
![alt text](kubectl-logs.png "Nifi-0 Logs")
Here, we run `kubectl logs nifi-0` and found the primary node `nifi-2`.
So we deploy the nifi service with external name `nifi-2.nifi-headless.default.svc.cluster.local`.

```
$ kubectl create -f https://raw.githubusercontent.com/whs-dot-hk/kubernetes-nifi-refined/master/cluster-guide/nifi-service-externalname-2.yaml
$ kubectl create -f https://raw.githubusercontent.com/whs-dot-hk/kubernetes-nifi-refined/master/frontend.yaml
```

## Port Forward Frontend
![alt text](port-forward.png "Port Forward Frontend")

## Enjoy
![alt text](nifi.png "Nifi")