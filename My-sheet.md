## etcd - Metadata means - Data of Data - Store in key value format
### Script writing
- We write code in manifest file Language can use `YAML` and `JSON`
- This code apply one cluster 
- Pod run on node which controlled by master
- 

In Kubernetes, the master node is responsible for managing the entire cluster and coordinating all activities within the cluster. Here are the main components contained in the master node:

### Master Node Components

1. **API Server**:
   - **Role**: Acts as the front-end for the Kubernetes control plane.
   - **Function**: Exposes the Kubernetes API. It handles RESTful requests from users, tools, and other components, ensuring that the cluster's desired state matches the current state.

2. **Controller Manager**:
   - **Role**: Runs controllers that regulate the state of the cluster.
   - **Function**: Monitors the state of the cluster through the API server and makes decisions to drive the cluster towards the desired state. Examples of controllers include the Node Controller (responsible for noticing and responding when nodes go down), the Replication Controller (responsible for maintaining the correct number of pods for every replication controller object in the system), and others.

3. **Scheduler**:
   - **Role**: Assigns pods to nodes.
   - **Function**: Watches newly created pods that have no node assigned, and selects a node for them to run on based on resource requirements, policies, and constraints. It considers factors like node capacity, affinity/anti-affinity specifications, data locality, and workload spread.

4. **etcd**:
   - **Role**: A distributed key-value store.
   - **Function**: Stores all cluster data, including the configuration data, state data, and metadata. It acts as the source of truth for the cluster's desired state and is used by the API server to store all the data about the cluster.

### Additional Details

- **API Server**:
  - **Endpoints**: Exposes various API endpoints for different resources like pods, services, deployments, etc.
  - **Security**: Manages authentication, authorization, and admission control.

- **Controller Manager**:
  - **Types of Controllers**: Includes multiple controllers like the Replication Controller, Endpoint Controller, Namespace Controller, and Service Account Controller.
  - **Monitoring**: Constantly monitors the state of the cluster through the API server and takes corrective actions.

- **Scheduler**:
  - **Policies**: Can be configured with various scheduling policies and priorities to determine where pods should be placed.
  - **Extensibility**: Supports custom schedulers for specific requirements.

- **etcd**:
  - **High Availability**: Often set up as a cluster of etcd nodes to ensure high availability and data redundancy.
  - **Backup**: Regular backups are crucial to prevent data loss in case of failures.

### Master Node Diagram

```plaintext
Master Node
├── API Server
│   ├── Handles RESTful requests
│   ├── Exposes Kubernetes API
│   ├── Manages security (authentication, authorization)
│   └── Admission control
│
├── Controller Manager
│   ├── Node Controller
│   ├── Replication Controller
│   ├── Endpoint Controller
│   ├── Namespace Controller
│   └── Service Account Controller
│
├── Scheduler
│   ├── Watches for unassigned pods
│   ├── Assigns pods to nodes based on policies
│   ├── Considers resource requirements
│   ├── Supports custom scheduling
│   └── Data locality and workload spread
│
└── etcd
    ├── Distributed key-value store
    ├── Stores all cluster data
    ├── Source of truth for desired state
    ├── High availability setup
    └── Regular backups
```

- This structure shows how the master node's components work together to manage and control the Kubernetes cluster.
________________________________________________________________________
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
