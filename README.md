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

Create or update objects using JSON/YAML file by `kubectl apply -f obj.yaml` command.
For testing the changes before applying, use `kubectl apply -f --dry-run obj.yaml` command.

Interactive edits to object instead of use of file can be done using `kubectl edit <resource-name> <object-name>`

You can view/edit/set last applied information using `edit-last-applied, set-last-applied and view-last-applied` commands

    `kubectl apply -f myobj.yaml view-last-applied`

Delete the object using file: `kubectl delete -f obj.yaml` or by command: `kubectl delete <resource-name> <object-name>`

## Labels and Annotations

Labels and annotations are tags to objects. E.g. `kubectl label pods bar color=red`
Remove a labe by using `<label-name>-` syntax. E.g. `kubectl label pods bar color-`

## Debugging Commands

We can access logs of containers using `kubectl logs <pod-name>`

You can use the `exec` command to execute command in running container

    `kubectl exec -it <pod-name> -- bash`

The attach command is an alternative if there is no bash or any terminal available to send input to running process (assuming it is set up to read from std input)

    `kubectl attach -it <pod-name>`

Copying files to and from container using cp command

    `kubectl cp <pod-name>:</path/to/remote/file> </path/to/local/file>

Port forwarding from the host machine to container port: `kubectl port-forward <pod-name> <host-machine-port>:<container-port>`

Same can be userd for port forwarding services by replacing `<pod-name>` with `<service-name>`

Viewing events in kubernetes can be done using `kubectl get events`

To get stats of how cluster is using resources, `kubectl top <nodes/pods>`
Note: If Metrics API is not available, fix is available in https://medium.com/@cloudspinx/fix-error-metrics-api-not-available-in-kubernetes-aa10766e1c2f

## Cluster Management

Cordon and draining nodes to ensure preventing future pods from being scheduled while removing the pods remaining on the machine.
Use case: Physical machine repairs or upgrades

`kubectl cordon` `kubectl drain`

Once the maintenance is completed, uncordon will re-enable pods scheduling on the node. No un-drain command. Duh!
`kubectl uncordon`

Getting the list of options and manual for k8s can be done by `kubectl help` or `kubectl help <command-name>`