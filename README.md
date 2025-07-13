# Quick Reference

## Pods

Kubernetes groups containers into single atomic unit called Pod.

Clubbing of several containers in k8s into a single pod is common.
Use case: Several service mesh implementations use a second sidecar container to inject network mgmt into pod.

### Pods in Kubernetes

Network Namespace: A network namespace in Linux is a feature that provides an isolated view of the network stack for a group of processes. Essentially, it creates a virtualized network environment within the host system, allowing for multiple, independent network stacks to exist simultaneously. Each namespace has its own network devices, IP addresses, routing tables, and firewall rules, effectively creating separate network environments within the same machine. 

UTS Namespace: A UTS namespace in Linux provides isolation of two system identifiers: the hostname and the NIS domain name. This allows processes within a namespace to have their own unique hostname and NIS domain name, separate from the host system or other namespaces. UTS stands for UNIX Time-sharing System.

Manifests: A pod manifest in Kubernetes is a file that defines the configuration of a pod, the smallest deployable unit in Kubernetes. It specifies the pod's metadata, such as its name and labels, and its spec, which includes the containers that run inside the pod.

Kubernes API server accepts and processes manifests before storing in persistent storage (etcd). Scheduler uses the K8S API to find pods that hasn't been scheduled to node. Then, it places the ods onto nodes depending on resources and constraints in manifests.

To create only pods and not deployments, use the `kubectl run <pod-name> --image=<image-source>`. To delete the same, use `kubectl delete pods/<pod-name>`

To get the details of the pods or any resource for that matter, use `kubectl describe <resource-type> <resource-name>`

Apply the pod creation from file using `kubectl apply -f <file-name>.yaml` List the pods using the `kubectl get pods`

Getting more logs from pod `kubectl logs <pod-name>`

### Liveness Probe

Snippet to be added to chec kif the application is healthy and shouldn't be restarted. Defined per container which means each container in a pod is health checked separately.

Sample liveness probe added in the yaml file.

### Readiness Probe

Readiness probe describes when the container is ready to serve requests from users. Containers that fail readiness checks are removed from the service load balancer.

Combine readiness and liveness probes helps ensure only healthy containers are running within the cluster.

### Startup Probe

Starting Probes is for managing slow-starting containers. Enables polling slowly for a slow-starting container while also enabling a responsive liveliness check once the slow-starting container has initialized.

### Other Probes

tcpSocket for TCP Socket health checks. exec scripts are often useful for custom application validation logic. Resource management 

### Minimum Required Resources

Pod can describe the minimum resources required to run a container. Refer to the yaml file for details.

### Capping Resource Usage

We can also set limits t o the maximum resources allocated to the container. This can be referred to in the yaml file.

## Persisting Data with Volumes

### Using Volumes with Pods

