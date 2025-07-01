# Quick Reference

## Namespace: kube-system

### Kubernetes Proxy

Responsible for routing network traffic to load-balanced service in the cluster. 
Must be present in every node of cluster

    `kubectl get daemonSets --namespace=kube-system kube-proxy`
kube-proxy container will be running on all nodes in cluster

### Kubernetes DNS

K8s runs a DNS server for naming and discovery of services defined in cluster.
DNS server runs as replicated service on the cluster. (one or more depending on size of cluster)

    kubectl get deployments --namespace=kube-system coredns

K8s service to perform load balancing for DNS server

    kubectl get services --namespace=kube-system kube-dns

## Contexts

Contexts are used to change the default namespace permanently. This is recorded in config file present in $HOME/.kube/config.

    kubectl config set-context my-context --namespace=mystuff

To use the newly created context,

    kubectl config use-context my-context

## Kubernetes API Objects

Everything in K8s is represented by RESTful resources. Sample URI: `https://k8s-server.com/api/v1/namespace/default/pods/my-pod`

To get the details of a particular objects you can use `kubectl get <object-name>`

You can view multiple objects of differenttypes by using comma separated list of types.

    kubectl get pods,services

For getting detailed information of a particular object, use `kubectl describe< resource-name> <object-name>`


To get list of supported fields for each type, use `kubectl explain pods`

