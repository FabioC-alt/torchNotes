
# Microservices Background

Traditional applications were built as monolithic, single unit applications. To address increasing or decreasing load, monoliths can horizontally scale by deploying more instances of the entire application. Some issues with the monolithic architecture style include development cycles of distinct components being tied together, having to rebuild and redeploy the entire application at each cycle (often with entirely unchanged components), and scaling the entire application (as opposed to just the components that are facing changes in load).
# Kubernetes Background

The different components in a microservices architecture are called *Services*. To manage or better to say to "orchestrate" all of the a tool is used and that tool is **Kubernetes**.
# Pillars of Observability
The three pillars of observability in distributed systems are *logs*, *metrics* and *traces*. This three components have different purpouse but are crucial from an observability point of view.
- **Logs**: are files that record errors, warnings, events and other types of information during the executions
- **Metrics**: This are measurements that records the health status and the performance of the application or the system.
- **Distributed Tracing**: These are the paths that an applicatiion requests follow as it changes the context during the execution.
To observe **logs** and **traces** an instrumentation is required in the target application. Instead, the system metrics can be collected by running the application without instrumentation.
By the utility point of view is possible to observe more statistical data by using the metrics. Logs are mostly unstructured data and needs to be parsed either client or server side before being collected and analyzed.

# eBPF
Is a linux kernel technology that can enable low level observability. It allowds low level sandboxed programs to run in th OS kernel without changing and recompiling the kernel.
It is possible to use the eBPF programs to add simple monitoring mechanism to the syscalls, such as the `malloc` or the `execv`.

This mechanism can expose interesting app-agnostic performace metrics.

(To see important implementation charateristics of the eBPF programs [[Articoli]]) -> Observatory
# Traditional Observability
Traditional Observability is based upon 3 main phases that are focused on the data.
-  **Data Collection**: Acquiring raw systems or application metrics and performing some form of sampling, aggregation or filtering
- **Data Ingestion**: Data are exported from global collectors with a centralized processing pipeline.
- **Insight Generation**: Once the data are collected and ingested is possible to analyze them and generate insight.

****
Cambio Articolo
# Quality of Service Aware Orchestration for Cloud–Edge Continuum Applications
## Intro
Ochestration tools like **Docker Swarm** and **Kubernetes** are called COE (*Container Orchestration Engines*). COEs are in charge of determining the containers that needs to be executed, decide the best target location for each of them, deploy the container to the selected nodes, executes it, monitor the system and redeploy services in case of failure.

### Edge Computing
Edge devices can offer a timely responses to applications that otherwise would not be feasible through Cloud computing. Being closer to the physical entities monitored. But the amount of power and informations provided by these technology are not on the same level as their cloud counterparts.

The introduction of the **Edge** paradigm creates the necessity for scalability and dynamicity, thus moving toward a **cloud-edge** continuum paradigm. This type of systems can easely become well populated. To tackle the management problem is possible to partition the infrastructure in smaller sub-clusters. The partition of the infrastructure leads to temporary unavailability of the applications. 
In this scenarios QoS awareness arises as an important goal for the system. 
Anyway, modern COEs do not consider interrelations between the containers 

FR1 -> Latency and reliability
FR2 -> Workload definition 
FR3 -> Intra-components connection
FR4 -> Inter-components connection

NFR1 -> Cloud-Edge systems.
NFR2 -> Dynamic adptment to infrastructure changes

   FR1: characterize inter-node metrics;
• FR2: characterize inter-component requirements;
• FR3: schedule based on intra-component requirements;
• FR4: schedule based on inter-component requirements;
• NFR1: support system scalability;
• NFR2: enable infrastructure dynamicity


## Architecture Components 
The architecture is splitted into two planes: **Control Plane** and **Execution Plane**. 

The control plane is in charge of management related tasks and is divided into *system control layer* and *application control layer*. 
The execution plane is where the application components are deployed.
![[Pasted image 20250423152810.png]]

The components have the following jobs:
- **System Control Components**: it is deployed in every node that joins the homonymous layer. It is composed by the System Scheduler, the API server and the State Database.
- **Application Control Components**: It is deployed in the corresponding layer.
- **System Deamons**: This components are deployed in every node that needs to join the system. There are two kind of deamons that are deployed the *node deamon* and the *monitoring deamon.*
The **API Server** is in charge of the system control component, which allows the remaining of the system components to interact among them using **RESTful** API. 
The **State Database** is a system control component, therefore, part of the system control layer. The database is used a checkpoint for the system which saves informations about the current state. 
The **System Scheduler** is the remaining system control component and is part of the layer with the same name.
The **Application Schedulers**, these are applications components, that are deployed in the application control layer. Those will use the state information available in the state databases in order to select the nodes in which the applications components will be deployed to maximize the QoS. 
**Node Daemons** are systems daemons that are in charge of the execution and monitoring of the containers working on the corresponding nodes.
**Monitoring Daemons** this daemons are deployed in every node in order to monitor the state of the surrounding network. 

### Infrastructure Model 
The Cloud-edge continuum can be represented using this infrastructure: 
![[Pasted image 20250423154521.png]]
This is a generic model and representation of the top view of a possible cloud-edge architecture and can be further specialized. 

The **set** of nodes are part of a **cluster**. Each node is identified by a *unique name* within the cluster and defined by a set of static and dynamic properties. 
The **network** is modeled using a set of **links** between the source node and a sink node.
### Workload Model
This is a generic representation of the **applications** that can be deployed onto a particular system.
![[Pasted image 20250423155122.png]]
As multiple application will be run on the system, they need a *unique name* that will act as identifier.
Each application is composed by different **components** which represent an executable piece.  Also each **component** require a unique name per application and are executed by the containers.
The channels define the messages transmitted from a source to sink component. 
Applications can be represented as DG(Directed Graphs), where **components** are graph's vertices and **channels** are the edges.
To manage the infrastructures the orchestrators engines allow setting constraints on which a certain node can deploy the services. 
**Constraints** are the first type of policy. Then there are the **Optimization Criteria** which allows configuring per application basis how the exact node from the set of potential target is choosen.

To fully exploit the **contraints** and **criteria** we need to define the **targets**. The target can be applied per-component basis and/or per-application basis. 
To refer internal application components is possible to use the **paths**. The application are characterized via **channels** that join a set of **components**.

### Application Creation Workflow
![[Pasted image 20250423172855.png]]
 
# Kubernetes
Kubernetes provides an abstraction layer over the containers called pods. Pods allows defining a set of one or more containers that need to be deployed together with their context, resource and network specifications.

Nodes are splitted into **control plane** and **execution plane** which derives that is possible to have **control plane nodes** and **execution nodes.**.
If there are more than one **control plane nodes**, this configuration is called **high availability setups**. 
To implement the Kube architecture there is the necessity to deploy 5 main system components. Four of these five are stored into the control plane and the last is placed inside the execution plane.
The four control plane components are:
- The API server
- The ETCD
- The controllers
- The scheduler

The component that runs on the execution plane is the **kubelet**.
The communication inside the cluster is possible thanks to the **API server**. This component is also in charge of coordinating all the other system components.

The **ETCD** is a NoSQL database that stores all the information about the infrastructure, the workload and the wanted status. 
When multiple nodes are deployed in the control plane of a cluster these two components enhance the performances of the system.

**Controllers** are in charge of implementing the Kube model, they translate the abstractions into pods.The pods configurations are then processed by the scheduler and assigned to one of the nodes in the execution plane.

The last two components do not benefit from increased performance when a high availability setup is configured. 

The last element of the Kube infrastructure is the **kubelet**, it is placed in every node and it is part of the execution plane. It handles the communications with the Kube system using the API server for both reporting the state of the node and executing the pods deployed by the scheduler

## Architecture OverHaul
ACOA (Application Centric Orchestration Architecture) further splits the control plane into two different layers, which requires a new node type.


# Observability with eBPF
The power of the eBPF project lays on three main pillars:
- **eBPF programs** runs at kernel level and react to events
- **User Space Programs** which loads the programs into the kernel and interact with them
- **BPF Maps** allows data storage and information sharing between the user space program and the eBPF program
### Development
During development a program is typically written with a low level language like *C*
or *Rust* and it is compiled into a executable and linkable format. The eBPF programs needs to be loaded into the kernel with a specific bytecode form. 
Compilers like clang/LLVM can be used to compile restricted-C code into the wanted *bytecode*. 
The *bytecode* file is stored inside a *ELF file*, which also contains the definitions of the *Maps* and the *BPF Type Format*.
The *ELF File* is then stored inside the kernel using a monolithic approach and enable by the *bpf system calls*. 
The *Maps* are useful to share the data in a variety of formats and to preserve the state.

### Execution
The eBPF is loaded into the kernel and compiled with JIT techniques. To interact with the kernel some libraries are necessary. Allowed libraries are:
- *GO ebpf-go*
- *C libbpf*

KEPLER for eBPF metrics export and ML analysis:
https://github.com/sustainable-computing-io/kepler

## Container Networking
Using eBPF allowds to skip all the network stack for communication using instead the kernel communication to send messages inside the network.
Also is possible to use a eBPF to deploy a loadbalancer agent and replace the Kube-Proxy which can achieve better performace.
### Service Mesh 
Service Meshes are dedicated infrastructure layer that can be added to applications or CNF micro-services. Service Meshes provide connectivity between applications at service level. 
The traditional service meshes uses a **Shared Library Model**. Then the **Sidecar Model** was introduced, with eBPF is possible to move the Service Mesh functionality to a lower level, the kernel.

#### Sidecar Model
With the Sidecar model is possible to place the common code inside a container and run this container in each pod so that each pod is instrumented in the same manner.
The container is the so-called *Sidecar Container*. Sidecar Container must run in the same *Network Namespace* as the application. The Sidecar deployment deployment can be performed using YAML manifest files or automatic mechanism offered by the Service Mesh implementation. 
The Sidecar model not so efficient because each pod must be configured with adequate memory and CPU quotas for the applications. Also the state configurations must be replicated for each pod, thus consuming more memory.

To encode traffic between application workload is possible to use tools like *IPsec* and *WireGuard*. These solutions are widely used and straightforward to implement.
#### eBPF Model

Since the eBPF program is loaded into the kernel there is no pod configuration modification to perform.
eBPF is attached to the event, the event will trigger independently from the pod status. Also there is no need to restart or reconfigure the pod in question. 
eBPF is also aware of the activities that take place inside the node.
In the service mesh context eBPF is able to create Service Mesh proxy to be shared across multiple pods, reducing the use of resources.
Also the packet do not need to travel more and more times the network stack.

### 
