Kubernetes Cluster Architecture

Overview

Kubernetes cluster architecture consists of a Control Plane and Worker Nodes that run containerized applications. Every cluster must have at least one worker node to run Pods.

The Control Plane manages the worker nodes and the Pods in the cluster, ensuring fault tolerance and high availability.
![image](https://github.com/user-attachments/assets/3cc62807-2aea-4ad7-84ef-cbc60e76f23e)


Cluster Components

1. Control Plane Components

The Control Plane is responsible for managing the cluster, making scheduling decisions, and responding to cluster events.

1.1 kube-apiserver

Exposes the Kubernetes API.

Acts as the front end for the Kubernetes Control Plane.

Scales horizontally by deploying multiple instances.

1.2 etcd

A consistent and highly available key-value store used as Kubernetes' backing store.

Stores all cluster data.

Requires a backup plan for data security.

1.3 kube-scheduler

Watches for newly created Pods with no assigned node.

Assigns a node based on resource requirements, constraints, and policies.

1.4 kube-controller-manager

Runs controller processes that regulate the cluster.

Includes multiple controllers such as:

Node Controller: Monitors node health.

Job Controller: Manages batch jobs.

EndpointSlice Controller: Links Services to Pods.

ServiceAccount Controller: Creates default ServiceAccounts for new namespaces.

1.5 cloud-controller-manager

Integrates Kubernetes with cloud providers.

Manages cloud-specific controllers such as:

Node Controller (detects deleted cloud nodes)

Route Controller (manages cloud routes)

Service Controller (manages cloud load balancers)

2. Node Components

Each node in the cluster runs necessary components to maintain the Kubernetes runtime environment.

2.1 kubelet

Runs on each node and ensures containers in Pods are running.

Manages PodSpecs and their lifecycle.

2.2 kube-proxy (Optional)

Network proxy that maintains Kubernetes networking rules.

Allows communication between Pods and external services.

Uses OS packet filtering or forwards traffic itself.

2.3 Container Runtime

Manages the execution and lifecycle of containers.

Examples: containerd, CRI-O, or any Kubernetes CRI-compliant runtime.

Add-ons in Kubernetes

Add-ons provide additional functionalities using Kubernetes resources like DaemonSets and Deployments.

1. DNS

Essential for service discovery.

Automatically included in containers’ DNS settings.

2. Web UI (Dashboard)

Web-based interface for managing Kubernetes clusters.

3. Container Resource Monitoring

Records container metrics and provides visualization.

4. Cluster-Level Logging

Collects logs from all containers and stores them centrally for analysis.

5. Network Plugins

Implements the Container Network Interface (CNI).

Allocates IPs and enables Pod communication.

Architecture Variations

Kubernetes architecture is flexible and can be deployed in different ways based on operational needs.

1. Control Plane Deployment Options

Traditional Deployment: Runs on dedicated machines or VMs.

Static Pods: Managed by kubelet on specific nodes (used by kubeadm).

Self-Hosted: Runs within Kubernetes using Deployments and StatefulSets.

Managed Kubernetes Services: Cloud providers manage the control plane.

2. Workload Placement Considerations

Small clusters may run control plane components and workloads on the same nodes.

Production environments separate control plane nodes from worker nodes.

Cluster Management Tools

kubeadm → Simplifies cluster setup.

kops → Manages Kubernetes clusters in the cloud.

Kubespray → Provides multi-cloud deployment support.
