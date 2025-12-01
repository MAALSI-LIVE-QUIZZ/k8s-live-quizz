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

## Cluster with multipass

### 1. Create VMs with multipass:

```bash
multipass launch --name master --cpus 2 --memory 4G --disk 10G
multipass launch --name worker1 --cpus 2 --memory 4G --disk 10G
multipass launch --name worker2 --cpus 2 --memory 4G --disk 10G
multipass launch --name worker3 --cpus 2 --memory 4G --disk 10G
```

### 2. Install K3s on the master node:

```bash
multipass exec master -- curl -sfL https://get.k3s.io | sh -
```

### 3. Get the join token from the master node:

```bash
multipass exec master -- sudo cat /var/lib/rancher/k3s/server/node-token
```

### 4. Join worker nodes to the cluster:

```bash
multipass exec worker1 -- curl -sfL https://get.k3s.io | K3S_URL=https://<master-ip>:6443 K3S_TOKEN=<token> sh -
multipass exec worker2 -- curl -sfL https://get.k3s.io | K3S_URL=https://<master-ip>:6443 K3S_TOKEN=<token> sh -
multipass exec worker3 -- curl -sfL https://get.k3s.io | K3S_URL=https://<master-ip>:6443 K3S_TOKEN=<token> sh -
```

5. Verify the cluster status:

```bash
multipass exec master -- sudo k3s kubectl get nodes
```

You should see all nodes (master and workers) listed as Ready.
