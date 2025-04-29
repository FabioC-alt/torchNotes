eBPF allowds for:

- **Fine-grained monitoring data**: It is possible to archieve very fine-grained container networks metrics of almost all the kernel operations based on eBPF 
- **Non-intrusive design**: no need to modify any kernel and application code, transparent to the user application
- **Scalability and low overhead**: the use of eBPF program can be dynamically updated to monitor the required events or system calls, while the system has low overhead.
- **Accurate and detailed performace analysis**: located the pod instance and correlate the analysis of event-related context based on fine-grained data


https://www.brendangregg.com/ebpf.html
# Cilium 
Mostly Service Mesh but can be used in combination with Hubble for observability.

# Pixie
## How it uses eBPF to collect data
Pixies sets up eBPF probes to trigger a number of kernel or user-space events.
When a probe triggers Pixies collects the data of interest from the event.

The main feature of Pixie is the ability to automatically trace protocol messages.

When Pixie is deployed to the nodes in your cluster, it deploys eBPF kernel probes (kprobes) that are set up to trigger on Linux syscalls used for networking. Then, when your application makes network-related syscalls -- such as `send()` and `recv()` -- Pixie's eBPF probes snoop the data and send it to the [Pixie Edge Module (PEM)](https://docs.px.dev/about-pixie/what-is-pixie/#architecture). In the PEM, the data is parsed according the detected protocol and stored for querying.

![[Pasted image 20250429104832.png]]

It is also possible to trace TLS/SSL Connections using an TLS library (`openssl`).

## Inspector Gadget
Contains gadget to monitor most of the metrics necessary inside a microservice system.

Based upon the gadgets which are the central component in the Inspektor Gadget framework. 

The that the eBPF collects from the kernel inclu