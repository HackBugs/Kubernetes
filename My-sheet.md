
### Detailed Tree with Nested Pods and Containers
Tree diagram representing the architecture of Kubernetes:

```plaintext
Kubernetes Cluster
├── Master Node
│   ├── API Server
│   ├── Controller Manager
│   ├── Scheduler
│   └── etcd
│
└── Worker Nodes
    ├── Kubelet
    ├── Kube Proxy
    ├── Container Runtime (e.g., Docker, containerd)
    └── Pods
        ├── Container 1
        ├── Container 2
        └── ...
```

### Components Explanation

#### Master Node
1. **API Server**:
   - The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. It is the front end of the Kubernetes control plane and handles RESTful requests from users and other components.

2. **Controller Manager**:
   - The controller manager is a daemon that runs in the master node and is responsible for running the various controllers that regulate the state of the cluster (e.g., Node Controller, Replication Controller).

3. **Scheduler**:
   - The scheduler is responsible for assigning newly created pods to nodes in the cluster based on resource requirements and other constraints.

4. **etcd**:
   - etcd is a key-value store used by Kubernetes to store all cluster data, including configuration data, state data, and metadata.

#### Worker Nodes
1. **Kubelet**:
   - The kubelet is an agent that runs on each worker node and ensures that containers are running in a pod. It communicates with the master node to get instructions and reports back the status of the pods running on the node.

2. **Kube Proxy**:
   - The kube proxy is responsible for maintaining network rules on the nodes. It enables network communication to your pods from network sessions inside or outside of the cluster.

3. **Container Runtime**:
   - The container runtime is the software that is responsible for running containers. Examples include Docker and containerd.

4. **Pods**:
   - A pod is the smallest and simplest Kubernetes object. A pod represents a set of running containers on your cluster. Each pod runs one or more containers (such as Docker containers).

### Detailed Tree with Nested Pods and Containers

```plaintext
Kubernetes Cluster
├── Master Node
│   ├── API Server
│   ├── Controller Manager
│   ├── Scheduler
│   └── etcd
│
└── Worker Nodes
    ├── Node 1
    │   ├── Kubelet
    │   ├── Kube Proxy
    │   ├── Container Runtime (e.g., Docker, containerd)
    │   └── Pods
    │       ├── Pod 1
    │       │   ├── Container 1
    │       │   └── Container 2
    │       └── Pod 2
    │           ├── Container 1
    │           ├── Container 2
    │           └── Container 3
    │
    ├── Node 2
    │   ├── Kubelet
    │   ├── Kube Proxy
    │   ├── Container Runtime (e.g., Docker, containerd)
    │   └── Pods
    │       ├── Pod 1
    │       │   └── Container 1
    │       └── Pod 2
    │           ├── Container 1
    │           ├── Container 2
    │           └── Container 3
    │
    └── Node 3
        ├── Kubelet
        ├── Kube Proxy
        ├── Container Runtime (e.g., Docker, containerd)
        └── Pods
            ├── Pod 1
            │   ├── Container 1
            │   └── Container 2
            └── Pod 2
                ├── Container 1
                ├── Container 2
                └── Container 3
```
________________________________________________________________________________________________________________________________

This tree structure provides a visual representation of how Kubernetes components are organized and interact within a cluster.

#### Basic Commands

1. **Check Cluster Info**
   ```bash
   kubectl cluster-info
   ```

2. **Get Nodes**
   ```bash
   kubectl get nodes
   ```

3. **Get Pods**
   ```bash
   kubectl get pods
   ```

4. **Get Services**
   ```bash
   kubectl get services
   ```

5. **Get Deployments**
   ```bash
   kubectl get deployments
   ```

#### Creating Resources

1. **Create a Deployment**
   ```bash
   kubectl create deployment <deployment-name> --image=<image-name>
   ```

2. **Create a Service**
   ```bash
   kubectl expose deployment <deployment-name> --type=<service-type> --port=<port>
   ```

3. **Apply a Configuration**
   ```bash
   kubectl apply -f <file.yaml>
   ```

#### Updating Resources

1. **Update a Deployment**
   ```bash
   kubectl set image deployment/<deployment-name> <container-name>=<new-image>
   ```

2. **Scale a Deployment**
   ```bash
   kubectl scale deployment <deployment-name> --replicas=<number-of-replicas>
   ```

#### Viewing and Debugging

1. **Describe a Resource**
   ```bash
   kubectl describe <resource-type> <resource-name>
   ```

2. **View Logs of a Pod**
   ```bash
   kubectl logs <pod-name>
   ```

3. **Execute a Command in a Pod**
   ```bash
   kubectl exec -it <pod-name> -- <command>
   ```

#### Deleting Resources

1. **Delete a Pod**
   ```bash
   kubectl delete pod <pod-name>
   ```

2. **Delete a Deployment**
   ```bash
   kubectl delete deployment <deployment-name>
   ```

3. **Delete a Service**
   ```bash
   kubectl delete service <service-name>
   ```

#### Namespaces

1. **Get Namespaces**
   ```bash
   kubectl get namespaces
   ```

2. **Create a Namespace**
   ```bash
   kubectl create namespace <namespace-name>
   ```

3. **Set Namespace Context**
   ```bash
   kubectl config set-context --current --namespace=<namespace-name>
   ```

#### ConfigMaps and Secrets

1. **Create a ConfigMap**
   ```bash
   kubectl create configmap <configmap-name> --from-literal=<key>=<value>
   ```

2. **Create a Secret**
   ```bash
   kubectl create secret generic <secret-name> --from-literal=<key>=<value>
   ```

3. **Get ConfigMaps**
   ```bash
   kubectl get configmaps
   ```

4. **Get Secrets**
   ```bash
   kubectl get secrets
   ```

#### Additional Commands

1. **Get All Resources**
   ```bash
   kubectl get all
   ```

2. **View Resource Usage**
   ```bash
   kubectl top nodes
   kubectl top pods
   ```

3. **Get Events**
   ```bash
   kubectl get events
   ```

### Useful Tips

- **Use Labels** to organize and select groups of resources.
  ```bash
  kubectl get pods --selector=<label-key>=<label-value>
  ```

- **Use Annotations** for storing non-identifying metadata.
  ```bash
  kubectl annotate <resource-type> <resource-name> <key>=<value>
  ```

- **Dry-run Mode** to see what will be applied.
  ```bash
  kubectl apply -f <file.yaml> --dry-run=client
  ```

This cheatsheet covers common Kubernetes commands and concepts. For more advanced usage and detailed documentation, refer to the [official Kubernetes documentation](https://kubernetes.io/docs/home/).
