# INSTALANDO VIA MINIKUBE
https://gitlab.com/nanuchi/argocd-app-config

Estou partindo do presuposto que o minikube já foi instalando. (https://minikube.sigs.k8s.io/docs/start/ )

## Ative o minikube:
```

minikube delete && minikube start

minikube status 
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

```

# CRIE UM NAMESPACE
# instalando  ArgoCD em  k8s
``` kubectl create namespace argocd
```

# BAIXE O YAML
```
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
# VERIFIQUE OS PODS
``` 
argocd$ kubectl get pods -n argocd
NAME                                                READY   STATUS    RESTARTS   AGE
argocd-application-controller-0                     1/1     Running   0          24m
argocd-applicationset-controller-5877955b59-s4k4k   1/1     Running   0          24m
argocd-dex-server-6c87968c75-jqn94                  1/1     Running   0          24m
argocd-notifications-controller-64bb8dcf46-5v6v2    1/1     Running   0          24m
argocd-redis-7d8d46cc7f-2m2dz                       1/1     Running   0          24m
argocd-repo-server-665d6b7b59-4fmq8                 1/1     Running   0          24m
argocd-server-5986f74c99-f55sf                      1/1     Running   0          24m
``` 


# MAPEANDO AS PORTAS
Precisamos mapear as portas para rodar local 
``` 
kubectl get svc -n argocd 
NAME                                      TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
argocd-applicationset-controller          ClusterIP   10.98.232.255    <none>        7000/TCP,8080/TCP            26m
argocd-dex-server                         ClusterIP   10.109.120.61    <none>        5556/TCP,5557/TCP,5558/TCP   26m
argocd-metrics                            ClusterIP   10.100.251.102   <none>        8082/TCP                     26m
argocd-notifications-controller-metrics   ClusterIP   10.107.128.46    <none>        9001/TCP                     26m
argocd-redis                              ClusterIP   10.105.213.183   <none>        6379/TCP                     26m
argocd-repo-server                        ClusterIP   10.103.161.187   <none>        8081/TCP,8084/TCP            26m
argocd-server                             ClusterIP   10.101.74.196    <none>        80/TCP,443/TCP               26m
argocd-server-metrics                     ClusterIP   10.107.189.165   <none>        8083/TCP                     26m


kubectl port-forward svc/argocd-server 8080:443 -n argocd
``` 

# PEGUE A SENHA ADMIN
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo

## ABRA NO BROWSER 
localhost:8080  admin 


#### Links
SITES DE REFERÊNCIAS QUE USEI: 

* Config repo: [https://gitlab.com/nanuchi/argocd-app-config](https://gitlab.com/nanuchi/argocd-app-config)

* Docker repo: [https://hub.docker.com/repository/docker/nanajanashia/argocd-app](https://hub.docker.com/repository/docker/nanajanashia/argocd-app)

* Install ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd)

* Login to ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli](https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli)

* ArgoCD Configuration: [https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/)
