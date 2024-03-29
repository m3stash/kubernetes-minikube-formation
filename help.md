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
* get container of pod
```shell
    kubectl get pods <POD_NAME> -o jsonpath='{.spec.containers[*].name}
```

## Imperativ / declarativ methode 
```shell
    # create -> imperative management (create / delete etc.)
    kubectl create -f pod.yaml
    # create a new kubernetes object ONLY for new object
    # useful for Troubleshootung, learnin, interactive experimentation
```
```shell
    # apply -> Declarativ management
    # useful for reproductible Deployment (define what we want in yaml files!)

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

# others 
* delete pods in error
```
    kubectl get pods | grep Error | cut -d' ' -f 1 | xargs kubectl delete pod
```
* iteration 
```shell
    % for i in `seq 1 3`; do kubectl delete pod nginx$i ; done
```

* get all pod name by deployment 
```shell
    kubectl get pods -o name -l app=<APP_NAME>
```
* boucle dans une liste de pod 
```shell
    for pod in $(kubectl get pods -o name -l app=<APP_NAME>); do echo $pod; done
    # ex: for pod in $(kubectl get pods -o name -l app=try1); do kubectl exec $pod -- touch /tmp/healthy; done;
 ```

* kubectl get pod by namespace and label app
```shell
    kubectl -n formation-ns-dev get -l app=<APP_NAME> pod
    or
    kubectl -n formation-ns-dev get --selector app=<APP_NAME> pod
 ```

# Command Shell

* get list of current PS (process status) and filter by name 
```shell
    ps -elf | grep kube-proxy
```
* journalctl (logs of systemd)
```shell
    journalctl -a | grep proxy
```