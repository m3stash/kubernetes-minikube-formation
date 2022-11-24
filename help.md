# Kubectl autocomplete
```shell
    # add autocomplete only into your current shell
    source <(kubectl completion zsh)
    # create an alias 
    alias k=kubectl
    complete -o default -F __start_kubectl k
    # add autocomplete permanently to your zsh shell
```

# Start Cluster
[kube-doc](https://minikube.sigs.k8s.io/docs/handbook/pushing/)
```shell
    minikube start
```

# Docker 
* Load local docker image in kube cluster
```shell
    minikube image load <DOCKE_IMAGE>:<VERSION>
```
* accès to docker daemon inside minikube
```shell
    # active
    eval $(minikube docker-env)
    # test
    docker ps
    # get docker image list
    docker image list
```

# DEPLOYMENT

* Set deployment by YAML file 
```shell
    kubectl apply -f ./application/<DEPLOYMENT_FILE_NAME>.yaml
```

* Display information about current deployment
```shell
    kubectl describe deployment <DEPLOYMENT_NAME>
```

* Delete deployment 
```shell
    kubectl delete deployment <DEPLOYMENT_NAME>
```

* Reload deployment
```shell
    kubectl rollout restart deployment <DEPLOYMENT_NAME>
```

# Namespace

* create Namespace by yaml file
```shell
    kubectl create -f admin/<NAMESPACE_NAME>.yaml
```

* set context namespace
```shell
    kubectl config set-context --current --namespace=<NAMESPACE_NAME>
    # validate it
    kubectl config view --minify | grep namespace:
```

* get Namespace
```shell
    kubectl get namespace
    # get current namespace 
    kubectl config view | grep namespace
```

# PODS

* get pod instance by name
```shell
    kubectl get pods -l app=<APP_NAME>
```
* Display information about specific pod
```shell
    kubectl describe pod <pod-name>
```
* set Pod by YAML config
```shell
    kubectl apply -f ./pods/nginx-pod.yaml
```
* get pod list
```shell
    kubectl get pod
    # avec plus d'infos (IP etc.)
    kubectl get pod -o wide
```
* get pod in all namespace
```shell
    kubectl get pods -A
```

# Services

* create service
```shell
    kubectl create -f ./services/networking/<SERVICE_NAME>.yaml
```
* get service 
```shell
    kubectl get svc
```
* get IP of services
```shell
    kubectl get pods -l app=<APP_NAME> \
    -o go-template='{{range .items}}{{.status.podIP}}{{"\n"}}{{end}}'
```
* Apply service with yaml conf
```shell
    kubectl apply -f ./services/networking/<SERVICE_NAME>.yaml
    #or
    kubectl expose deployment/<POD_NAME>
```

# Container 
* get list of pod containers
```shell
    kubectl get pods <POD_NAME> -o jsonpath='{.spec.containers[*].name}'
```

# Important links 
* [cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)