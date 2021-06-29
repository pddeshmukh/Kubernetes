# Kubernetes Tutorial

Kubernetes is a container management technology developed in Google lab to manage containerized applications in different kind of environments such as physical, virtual, and cloud infrastructure. It is an open source system which helps in creating and managing containerization of application. This section provides an overview of different kind of features and functionalities of Kubernetes.

# Features of Kubernetes

#### Following are some of the important features of Kubernetes.

* Continues development, integration and deployment

* Containerized infrastructure

* Application-centric management

* Auto-scalable infrastructure

* Environment consistency across development testing and production

* Loosely coupled infrastructure, where each component can act as a separate unit

* Higher density of resource utilization

* Predictable infrastructure which is going to be created

# Kubernetes - Cluster Architecture

![alt text](https://github.com/pddeshmukh/Kubernetes/blob/main/Images/kubernetes-architecture.png?raw=true)

### Kubernetes - Master/Control Plane Machine Components

Following are the components of Kubernetes Master/Control Plane Machine.

#### etcd
It stores the configuration information which can be used by each of the nodes in the cluster. It is a high availability key value store that can be distributed among multiple nodes. It is accessible only by Kubernetes API server as it may have some sensitive information. It is a distributed key value Store which is accessible to all.

#### API Server
Kubernetes is an API server which provides all the operation on cluster using the API. API server implements an interface, which means different tools and libraries can readily communicate with it. API Server helps to communicate kubernetes from CLI and console.

#### Controller Manager
This component is responsible for most of the collectors that regulates the state of cluster and performs a task. In general, it can be considered as a daemon which runs in nonterminating loop and is responsible for collecting and sending information to API server. It works toward getting the shared state of cluster and then make changes to bring the current status of the server to the desired state. The key controllers are replication controller, endpoint controller, namespace controller, and service account controller. The controller manager runs different kind of controllers to handle nodes, endpoints, etc.

#### Scheduler
This is one of the key components of Kubernetes master. It is a service in master responsible for distributing the workload. It is responsible for tracking utilization of working load on cluster nodes and then placing the workload on which resources are available and accept the workload. In other words, this is the mechanism responsible for allocating pods to available nodes.

###  Kubernetes - Node Components

Following are the key components of Node server which are necessary to communicate with Kubernetes master/Control Plane.

#### Docker
The first requirement of each node is Docker which helps in running the encapsulated application containers in a relatively isolated but lightweight operating environment.

#### Kubelet Service
This is a small service in each node responsible for relaying information to and from control plane service. It interacts with etcd store to read configuration details. This communicates with the master component to receive commands and work. The kubelet process then assumes responsibility for maintaining the state of work and the node server. It manages network rules, port forwarding, etc.

#### Kubernetes Proxy Service
This is a proxy service which runs on each node and helps in making services available to the external host. It helps in forwarding the request to correct containers and is capable of performing primitive load balancing. It manages pods on node, volumes, secrets, creating new containers’ health checkup, etc.

### Kubernetes - Labels & Selectors

#### Labels
Labels are key/value pairs that are attached to objects, such as pods. Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users, but do not directly imply semantics to the core system

```
"metadata": {
  "labels": {
    "key1" : "value1",
    "key2" : "value2"
  }
}

```
For example, here's the configuration file for a Pod that has two labels `environment: production` and `app: nginx`

```
apiVersion: v1
kind: Pod
metadata:
  name: label-demo
  labels:
    environment: production
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80

```

### Label selectors
Via a label selector, the client/user can identify a set of objects. The label selector is the core grouping primitive in Kubernetes.

One usage scenario for equality-based label requirement is for Pods to specify node selection criteria. For example, the sample Pod below selects nodes with the label `accelerator=nvidia-tesla-p100`

```
apiVersion: v1
kind: Pod
metadata:
  name: cuda-test
spec:
  containers:
    - name: cuda-test
      image: "k8s.gcr.io/cuda-vector-add:v0.1"
      resources:
        limits:
          nvidia.com/gpu: 1
  nodeSelector:
    accelerator: nvidia-tesla-p100
```

You can also use CLI tool to perform operations related to labels. For example, below command helps to add label to a node
`kubectl label nodes <node-name> <label-key>=<label-value>`

You can verify that it worked by re-running below command and checking that the node now has a label.
`kubectl get nodes --show-labels`
