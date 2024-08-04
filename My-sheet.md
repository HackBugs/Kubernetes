### ✍️ Author : HackBugs
### This is Product of Google 

### Kubernetes Commands
[All-Commands for installation](https://phoenixnap.com/kb/install-kubernetes-on-ubuntu)</br>
[All-Commands for installation-2](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

- Declarative - write in menifest file .yml
- imperative - Use cmd to do anything

- This cmd like `Sqlplus / as sysdba` - use of `strtup `
- `Minikube status`
- `Minikube start`
_________________________________________________________________________________________________
### Use this cmd for installtionn on ubuntu
```sh
sudo su
apt-get update
apt-get install apt-transport-https

apt install docker.io -y
docker --version
systemctl start docker
systemctl enable docker

sudo curl -s https://packages.cloud.google.com/apt... | sudo apt-key add 


nano /etc/apt/sources.list.d/kubernetes.list

deb http://apt.kubernetes.io/ kubernetes-xenial main


apt-get update

apt-get install -y kubelet kubeadm kubectl kubernetes-cni


BOOTSTRAPPING THE MASTER NODE (IN MASTER)

kubeadm init
 

COPY THE COMMAND TO RUN IN NODES & SAVE IN NOTEPAD

mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config


chown $(id -u):$(id -g) $HOME/.kube/config

kubectl apply -f https://raw.githubusercontent.com/cor...

kubectl apply -f https://raw.githubusercontent.com/cor...

CONFIGURE WORKER NODES (IN NODES)

COPY LONG CODE PROVIDED MY MASTER IN NODE NOW LIKE CODE GIVEN BELOW

e.g- kubeadm join 172.31.6.165:6443 --token kl9fhu.co2n90v3rxtqllrs --discovery-token-ca-cert-hash sha256:b0f8003d23dbf445e0132a53d7aa1922bdef8d553d9eca06e65c928322b3e7c0

GO TO MASTER AND RUN THIS COMMAND
kubectl get nodes
```
- The ```actual state``` is the current condition of the system, while the ```desired state``` is the condition you want the system to achieve.
- We write Kubernetes configuration code in a ```manifest.yml file.``` The manifest file contains definitions for Kubernetes objects.
- Pod ➡️ Service ➡️ volume ➡️ Namespace ➡️ replication ➡️ Secerets ➡️ Confg map ➡️ Deployments ➡️ Jobs ➡️ daemonset
- Managing Kubernetes can be done using imperative commands and declarative configurations. Here's how:

1. **Imperative Commands**: Directly instruct Kubernetes what to do with a single command.
   - Example: `kubectl create deployment nginx --image=nginx`
   - Useful for quick changes or testing.

2. **Declarative Configurations**: Define the desired state of your Kubernetes objects in YAML or JSON files, which Kubernetes continuously ensures.
   - Example: Writing the desired state in a `deployment.yml` file:
     ```yaml
     apiVersion: apps/v1
     kind: Deployment
     metadata:
       name: nginx
     spec:
       replicas: 3
       selector:
         matchLabels:
           app: nginx
       template:
         metadata:
           labels:
             app: nginx
         spec:
           containers:
           - name: nginx
             image: nginx
     ```
   - Apply the configuration: `kubectl apply -f deployment.yml`

- Using imperative commands is faster for small tasks and immediate actions, while declarative configurations are better for managing complex setups and ensuring consistency over time.

### Kubernetes Configurations
- All-in-one single node installation to help with Minikube - we use this only for learning purposes and not for production.
- Single node etcd or single master and multi-worker installation.
- Single-node etcd, multi-master, and multi-worker installations.

### Why Use kubeadm, kubectl, and Minikube

#### kubeadm
- **Purpose**: Simplifies the process of setting up a Kubernetes cluster.
- **Use Case**: Ideal for bootstrapping clusters in a consistent and repeatable way.
- **Functionality**: Initializes the Kubernetes control plane and nodes.

#### kubectl
- **Purpose**: Command-line tool to interact with the Kubernetes API.
- **Use Case**: Manages and deploys applications, inspects and manages cluster resources.
- **Functionality**: Allows you to run commands against Kubernetes clusters to manage resources.

#### Minikube
- **Purpose**: Runs a single-node Kubernetes cluster on your local machine.
- **Use Case**: Perfect for learning and development environments.
- **Functionality**: Provides a sandbox environment for testing Kubernetes features without the need for a full-scale cluster.

### Summary
- **kubeadm** is used for setting up and initializing Kubernetes clusters.
- **kubectl** is the command-line tool for managing and interacting with Kubernetes clusters.
- **Minikube** provides a local Kubernetes environment for development and testing purposes.
__________________________________________________________________________________________________________________________________________________________
# ✍️ Installtion
Kubernetes can be configured in various ways depending on your requirements, and one of the simplest setups is installing everything on a single node. Here's a step-by-step guide to installing Kubernetes on a single node using Minikube, which is a tool that makes it easy to run Kubernetes locally.

### Step-by-Step Guide to Install Kubernetes on a Single Node Using Minikube

#### Prerequisites:
1. **Operating System**: Ubuntu or any Linux distribution.
2. **Hardware Requirements**: Minimum 2GB RAM and 20GB disk space.

#### Step 1: Install Dependencies

Update your package list and install dependencies:

```sh
sudo apt-get update -y
sudo apt-get install -y apt-transport-https ca-certificates curl
```

#### Step 2: Install Docker

Minikube requires Docker as its container runtime. Install Docker:

```sh
sudo apt-get install -y docker.io
sudo systemctl enable docker
sudo systemctl start docker
```

#### Step 3: Install Minikube

Download the Minikube binary and install it:

```sh
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

#### Step 4: Start Minikube

Start Minikube with Docker driver:

```sh
minikube start --driver=docker
```

This command starts a single-node Kubernetes cluster using Minikube.

#### Step 5: Install Kubectl

Kubectl is a command-line tool for interacting with Kubernetes clusters. Install it:

```sh
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

#### Step 6: Verify Installation

Check the status of your Minikube cluster:

```sh
minikube status
```

You should see that the cluster is running. Also, you can check the nodes in the cluster:

```sh
kubectl get nodes
```

You should see a single node listed.

### Step 7: Create a Deployment

Create a simple Nginx deployment to verify that everything is working:

```sh
kubectl create deployment nginx --image=nginx
```

Expose the deployment as a service:

```sh
kubectl expose deployment nginx --port=80 --type=NodePort
```

### Step 8: Access the Application

To access the Nginx application, you can get the URL using:

```sh
minikube service nginx --url
```

Open the URL in your web browser to see the Nginx welcome page.

### Summary

You now have a single-node Kubernetes cluster running on your machine using Minikube. This setup is ideal for learning and development purposes. For production environments, consider using a multi-node cluster with proper high availability configurations.
________________________________________________________________________________________________________________________

# ✍️ Docker installation
- sudo apt update
- sudo apt install docker.io -y
- sudo systemctl enable docker
- sudo systemctl status docker
- sudo systemctl start docker

### Master cmd and installation
- This cmd use on master node
- Kubeadm init
- Bootstraping means establishing a connection between the master and node, typically through ports or other methods.
- mkdir -p $HOME/.kube
- sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
- sudo chown $(id -u):$(id -g) $HOME/.kube/config
- kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml
- kubectl taint nodes --all node-role.kubernetes.io/control-plane-
- 

` etcd - Metadata means - Data of Data - Store in key value format`
` Maste and node both together make cluster`

### Higher level Kubernetes abject - use for auto acaling auto healing
   - Versioing and rollback
   - Higher level service - can create static ip 
   - volume
     
________________________________________________________________________________________________________________________________________________
# ✍️ Master ➡️ Node
ist of the key components of a Kubernetes master node and the components of a Kubernetes worker node:

### Master Node Components

1. **API Server**: 
   - Exposes the Kubernetes API.
   - Acts as the front-end of the Kubernetes control plane.

2. **etcd**: 
   - Key-value store.
   - Stores all cluster data.

3. **Controller Manager**:
   - Node Controller: Manages node health.
   - Replication Controller: Ensures the desired number of pods.
   - Deployment Controller: Manages deployments.
   - ReplicaSet Controller: Ensures stable pod replicas.
   - StatefulSet Controller: Manages StatefulSets.
   - DaemonSet Controller: Ensures pod copies on nodes.
   - Job Controller: Manages job objects.
   - CronJob Controller: Manages CronJobs.
   - Service Controller: Manages service objects.
   - Endpoint Controller: Populates endpoint objects.
   - Namespace Controller: Manages namespaces.
   - Service Account Controller: Manages service accounts.
   - Resource Quota Controller: Manages resource quotas.

4. **Scheduler**: 
   - Assigns pods to nodes.
   - Ensures pods are placed based on resource requirements and policies.

### Worker Node Components

1. **Kubelet**: 
   - Agent running on each node.
   - Ensures containers are running in pods.

2. **Kube-Proxy**: 
   - Network proxy.
   - Maintains network rules and handles communication between pods.

3. **Container Runtime**: 
   - Runs containers.
   - Examples include Docker, containerd, and CRI-O.

This list provides an overview of the primary components on both the master and worker nodes in a Kubernetes cluster.
__________________________________________________________________________________________________________________________________________

- API Server ➡️ Controller Manage ➡️ etcd clusterr ➡️ Kube - Scheduler - Kube Scheduler it's handle pod creation and manage of them ➡️

### Script writing
- We write code in manifest file Language can use `YAML` and `JSON`
- This code apply one cluster 
- Pod run on node which controlled by master
________________________________________________________________________________________________________________________________________________

# ✍️ Controller Manager Components and Diagram

The Controller Manager in Kubernetes is a key component of the master node. It is responsible for running various controller processes that manage different aspects of the cluster's state. Here are the main controllers contained within the Controller Manager:

```plaintext
Controller Manager
├── Node Controller
│   ├── Monitors node health
│   └── Responds to node additions/removals and failures
│
├── Replication Controller
│   ├── Ensures desired number of pod replicas
│   └── Creates/deletes pods to maintain desired state
│
├── Deployment Controller
│   ├── Manages deployments
│   └── Updates pods according to deployment strategy
│
├── ReplicaSet Controller
│   ├── Maintains stable set of replica pods
│   └── Ensures desired number of pods are running
│
├── StatefulSet Controller
│   ├── Manages StatefulSets
│   └── Ensures correct number and order of pods
│
├── DaemonSet Controller
│   ├── Ensures a pod copy on selected nodes
│   └── Manages pod deployment on nodes
│
├── Job Controller
│   ├── Manages job objects
│   └── Ensures successful termination of specified pods
│
├── CronJob Controller
│   ├── Manages CronJobs
│   └── Creates jobs on schedule
│
├── Service Controller
│   ├── Manages service objects
│   └── Maps services to endpoints
│
├── Endpoint Controller
│   ├── Populates endpoint objects
│   └── Maintains service-to-pod mapping
│
├── Namespace Controller
│   ├── Manages namespaces
│   └── Handles namespace lifecycle
│
├── Service Account Controller
│   ├── Manages service accounts
│   └── Creates default accounts for namespaces
│
└── Resource Quota Controller
    ├── Manages resource quotas
    └── Ensures resource usage within limits
```

This breakdown shows how each controller within the Controller Manager has a specific role and function, contributing to the overall management and operation of the Kubernetes cluster.

________________________________________________________________________________________________________________________________________________
In Kubernetes, the master node is responsible for managing the entire cluster and coordinating all activities within the cluster. Here are the main components contained in the master node:

# ✍️ Master Node Components

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
# ✍️ Detailed Tree with Nested Pods and Containers
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

# ✍️ Basic Commands

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
______________________________________________________________________________________________________________________________________________________

# ✍️ Labels, Selectors, ReplicationController and replicaset in Kubernetes
### Kubernetes mein Labels, Selectors, ReplicationController aur ReplicaSet ka Explanation aur Commands

**Labels**:
Labels simple key-value pairs hote hain jo Kubernetes objects ko describe aur categorize karte hain. Yeh aapko specific resources ko search aur organize karne mein madad karte hain.

**Example**:
```yaml
metadata:
  labels:
    app: myapp
    environment: production
```

**Commands**:
- `kubectl get pods --show-labels`: Sabhi pods ke labels dekhne ke liye.
- `kubectl label pods <pod-name> app=myapp`: Ek pod ko label karne ke liye.

**Selectors**:
Selectors ka use karke aap specific labels wale objects ko select kar sakte hain. Yeh labels ke basis par filtering karne mein madad karte hain.

**Example**:
```yaml
spec:
  selector:
    matchLabels:
      app: myapp
```

**Commands**:
- `kubectl get pods -l app=myapp`: Specific label wale pods ko retrieve karne ke liye.

**ReplicationController**:
ReplicationController ensure karta hai ki specified number of pod replicas hammesha running state mein rahein. Agar koi pod fail ho jaye toh yeh automatically naye pods create kar deta hai.

**Example**:
```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: myapp-rc
spec:
  replicas: 3
  selector:
    app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp-container
        image: nginx
```

**Commands**:
- `kubectl create -f replication-controller.yaml`: ReplicationController create karne ke liye.
- `kubectl get rc`: Sabhi ReplicationControllers dekhne ke liye.
- `kubectl delete rc <rc-name>`: Ek ReplicationController delete karne ke liye.

**ReplicaSet**:
ReplicaSet bhi similar function perform karta hai jaise ReplicationController, but yeh more flexible selector support karta hai. Yeh ensure karta hai ki specified number of pod replicas running rahein.

**Example**:
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-rs
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp-container
        image: nginx
```

**Commands**:
- `kubectl create -f replica-set.yaml`: ReplicaSet create karne ke liye.
- `kubectl get rs`: Sabhi ReplicaSets dekhne ke liye.
- `kubectl delete rs <rs-name>`: Ek ReplicaSet delete karne ke liye.

Some advanced commands for working with Labels, Selectors, ReplicationController, and ReplicaSet in Kubernetes, explained in Hinglish.

### Labels

**Advanced Commands**:
- **Updating Labels**:
  ```bash
  kubectl label pods <pod-name> app=myapp --overwrite
  ```
  Yeh command existing label ko overwrite karne ke liye use hoti hai.

- **Filtering Pods using Multiple Labels**:
  ```bash
  kubectl get pods -l app=myapp,environment=production
  ```
  Yeh command multiple labels ke basis par filtering karne ke liye hai.

### Selectors

**Advanced Commands**:
- **Using Set-Based Selectors**:
  ```bash
  kubectl get pods --selector='app in (myapp, yourapp)'
  ```
  Yeh command specific set-based selectors ko use karte hue pods retrieve karne ke liye hai.

- **Using Not Equal Selector**:
  ```bash
  kubectl get pods -l 'app!=myapp'
  ```
  Yeh command specific label ke not equal condition par pods retrieve karne ke liye hai.

### ReplicationController

**Advanced Commands**:
- **Scaling ReplicationController**:
  ```bash
  kubectl scale rc <rc-name> --replicas=5
  ```
  Yeh command ReplicationController ke replicas count ko change karne ke liye hai.

- **Updating ReplicationController**:
  ```bash
  kubectl rolling-update <old-rc-name> --image=<new-image>
  ```
  Yeh command rolling update perform karne ke liye hai, jo safe way mein existing pods ko new image ke sath replace karti hai.

### ReplicaSet

**Advanced Commands**:
- **Scaling ReplicaSet**:
  ```bash
  kubectl scale rs <rs-name> --replicas=5
  ```
  Yeh command ReplicaSet ke replicas count ko change karne ke liye hai.

- **Describe ReplicaSet**:
  ```bash
  kubectl describe rs <rs-name>
  ```
  Yeh command specific ReplicaSet ka detailed description dekhne ke liye hai.

- **Update Image in ReplicaSet**:
  ```bash
  kubectl set image rs/<rs-name> <container-name>=<new-image>
  ```
  Yeh command specific container ka image update karne ke liye hai.

- **Deleting Pods and Checking Auto-Scaling**:
  ```bash
  kubectl delete pod <pod-name>
  ```
  Yeh command specific pod ko delete karne ke liye hai aur dekhna ki ReplicaSet automatically new pod create karta hai ya nahi.

Yeh advanced commands aur concepts aapko Kubernetes mein Labels, Selectors, ReplicationController, aur ReplicaSet ke saath aur bhi effectively kaam karne mein madad karenge.
_________________________________________________________________________________________________________________________________________________________

