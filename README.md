# K8S

## Words about Kubernetes

- Cluster: ensemble of machines (nodes) that run containerized applications
- Node: a single machine in the cluster (can be physical or virtual)
- Pod: smallest deployable unit in Kubernetes, can contain one or more containers

- Service: an abstraction that defines a logical set of pods and a policy to access them
- Deployment: a controller that manages the deployment and scaling of pods
- Namespace: a virtual cluster within a Kubernetes cluster, used to separate resources

## CLI Commands

    - `kubectl get nodes`: list all nodes in the cluster
    - `kubectl get pods`: list all pods in the current namespace
    - `kubectl get services`: list all services in the current namespace
    - `kubectl get deployments`: list all deployments in the current namespace
    - `kubectl describe pod <pod-name>`: get detailed information about a specific pod
    - `kubectl logs <pod-name>`: fetch logs from a specific pod
    - `kubectl apply -f <file.yaml>`: create or update resources defined in a YAML file
    - `kubectl delete -f <file.yaml>`: delete resources defined in a YAML file
    - `kubectl exec -it <pod-name> -- /bin/bash`: open a terminal session inside a pod
