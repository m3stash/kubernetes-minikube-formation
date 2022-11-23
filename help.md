# Start Cluster
[kube-doc](https://minikube.sigs.k8s.io/docs/handbook/pushing/)
```yaml
    minikube start
```

# Docker 
* Load local docker image in kube cluster
```yaml
    minikube image load <DOCKE_IMAGE>:<VERSION>
```
* accès to docker daemon inside minikube
```yaml
    # active
    eval $(minikube docker-env)
    # test
    docker ps
    # get docker image list
    docker image list
```

# DEPLOYMENT

* Set deployment by YAML file 
```yaml
    kubectl apply -f ./application/<DEPLOYMENT_FILE_NAME>.yaml
```

* Display information about current deployment
```yaml
    kubectl describe deployment <DEPLOYMENT_NAME>
```

* Delete deployment 
```yaml
    kubectl delete deployment <DEPLOYMENT_NAME>
```

* Reload deployment
```yaml
    kubectl rollout restart deployment <DEPLOYMENT_NAME>
```

# Namespace

* set context namespace
```yaml
    kubectl config set-context --current --namespace=<NAMESPACE_NAME>
    # validate it
    kubectl config view --minify | grep namespace:
```

* get Namespace
```yaml
    kubectl get namespace
```

# PODS

* get pod instance by name
```yaml
    kubectl get pods -l app=<APP_NAME>
```
* Display information about specific pod
```yaml
    kubectl describe pod <pod-name>
```
* set Pod by YAML config
```yaml
    kubectl apply -f ./pods/nginx-pod.yaml
```
* get pod list
```yaml
    kubectl get pod
    # avec plus d'infos (IP etc.)
    kubectl get pod -o wide
```
* get pod in all namespace
```yaml
    kubectl get pods -A
```

# Services

* create service
```yaml
    kubectl create -f service.yaml
```
* get service 
```yaml
    kubectl get svc
```
* get IP of services
```yaml
    kubectl get pods -l app=<APP_NAME> \
    -o go-template='{{range .items}}{{.status.podIP}}{{"\n"}}{{end}}'
```
* Apply service with yaml conf
```yaml
    kubectl apply -f ./service/networking/<SERVICE_NAME>.yaml
    #or
    kubectl expose deployment/<POD_NAME>
```



