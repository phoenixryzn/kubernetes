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

    `kubectl get deployments --namespace=kube-system coredns`

K8s service to perform load balancing for DNS server

    `kubectl get services --n=kube-system kube-dns`