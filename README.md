# Hello World Helm

###### Create a kubernetes service with three pods via a helm chart and expose the service with ingress

--- 

### Install chart on local minikube cluster

Deploy the service and ingress

    $ helm install hello-world-helm/ 

Check the installed chart

    $ helm list 

Check the service and ingress

    $ kubectl get services
    $ kubectl get pods
    $ kubectl describe ingress 

Enable Ingress addon

    $ minikube addons enable ingress
    
Find out the minikube IP

    $ echo "$(minikube ip)"

Access the services from the cluster via a browser

    https://[minikube IP]
    
The nginx default page, "Welcome to nginx!", should appear
