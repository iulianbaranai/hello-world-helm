# Hello World Helm

##### Create a kubernetes service with three pods via a helm chart and expose the service with ingress

--- 

### Install chart on local minikube cluster

Prerequisites

* Make sure you have a local cluster: https://kubernetes.io/docs/setup/minikube
* Make sure helm is installed: https://github.com/helm/helm/blob/master/docs/install.md

Deploy the service and ingress

    $ helm install hello-world-helm/ 

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

Cleanup the cluster by uninstalling the release

    $ helm delete $(helm list | grep DEPLOYED | cut -f1)
