
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