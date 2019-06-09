# Hello World Helm

##### Helm is a tool for Kubernetes that helps installing and managing applications. 
##### Create a kubernetes service with three pods via a helm chart and expose the service with ingress.

--- 

### Install chart on local minikube cluster

Prerequisites

* Make sure you have a local cluster: https://kubernetes.io/docs/setup/minikube
* Make sure helm is installed: https://github.com/helm/helm/blob/master/docs/install.md

Clone this repository

    $ https://github.com/iulianbaranai/hello-world-helm.git

Navigate to the directory and install the chart

    $ helm install ./

Check the installed chart - should be in DEPLOYED state

    $ helm list 

Check the created resources

    $ kubectl get pods
    $ kubectl get replicaset
    $ kubectl get deployments
    $ kubectl get services
    $ kubectl get all # displays the above four resources at once
    $ kubectl describe ingress 

Enable Ingress addon

    $ minikube addons enable ingress
    
Find out the minikube IP

    $ echo "$(minikube ip)"

Access the cluster service via a browser - "Welcome to nginx!" default page should appear

    https://[minikube IP]

### Update values and upgrade helm installation

Check the current version of nginx installed on pods

    k exec [pod-name] -- nginx -v

Update the values.yaml file

    scale: 10
    tag: "1.13"

Upgrade to new version

    # helm upgrade [helm-release-name] [chart-location]
    $ helm upgrade $(helm list | grep DEPLOYED | cut -f1) ./

Check the helm revision, pods number, current version of nginx installed on pods

    $ helm list # see REVISION on DEPLOYED chart
    $ kubectl get pods
    $ kubectl exec [pod-name] -- nginx -v

### Rollback to previous version

    # helm rollback [helm-release-name] [helm-release-revision]
    $ helm rollback $(helm list | grep DEPLOYED | cut -f1) 1

Check the helm revision, pods number, current version of nginx installed on pods

    $ helm list # see REVISION on DEPLOYED chart
    $ kubectl get pods
    $ kubectl exec [pod-name] -- nginx -v

### Cleanup the cluster

Uninstall the deployed release

    # helm delete [helm-release-name]
    $ helm delete $(helm list | grep DEPLOYED | cut -f1)
