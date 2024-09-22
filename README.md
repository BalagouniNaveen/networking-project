# networking-project

                                                      ** Kubernetes Networking Project**


**1. Architecture**

**Master Node:** The control plane that manages the Kubernetes cluster. It includes several key components:
**API Server:** The interface for all communication in the cluster, handling REST requests.
**etcd:** A distributed key-value store for storing cluster data and configuration.
**Controller Manager:** Manages controllers that regulate the state of the cluster.
**Scheduler:** Assigns pods to nodes based on resource availability and policies.
**Worker Nodes:** The nodes that run application workloads. Each worker node includes:
**Kubelet:** An agent that communicates with the API server, ensuring that containers are running as intended.
**Kube-Proxy:** Manages network rules to route traffic to the appropriate pods.
**Container Runtime:** Software responsible for running containers (e.g., Docker, containerd).


**2. Core Concepts**

**Pod:** The smallest deployable unit in Kubernetes, which can contain one or more containers that share storage, network, and specifications.
**Service:** An abstraction that defines a logical set of pods and a policy to access them, providing stable networking.
**Deployment:**  Manages the desired state for a set of pods, facilitating updates and scaling.
**ReplicaSet:** Ensures a specified number of pod replicas are running at all times.
**StatefulSet:** Manages stateful applications with stable identities and persistent storage.
**DaemonSet:** Ensures that a copy of a pod runs on all nodes, useful for system-level tasks.


**3. Networking**

**Flat Networking Model:** Every pod gets its own IP address, allowing direct communication between pods.
**Service Discovery:** Kubernetes uses DNS to allow services to find and communicate with each other.
**Ingress:** Manages external access to services, allowing for HTTP/S routing.
**Network Policies:** Control the communication between pods and enhance security.


**4. Storage Management**

**Persistent Volumes (PV):** Abstract storage resources in the cluster.
**Persistent Volume Claims (PVC):** Requests for storage by users or applications.
**Storage Classes:** Define different types of storage that can be dynamically provisioned.


**5. Scalability and Load Balancing**

**Horizontal Pod Autoscaler:** Automatically adjusts the number of pod replicas based on observed CPU utilization or other select metrics.
**Service Types:** Includes ClusterIP, NodePort, and LoadBalancer to expose applications and distribute traffic.


**6. Security**

**Role-Based Access Control (RBAC):** Manages permissions for users and service accounts.
**Secrets and ConfigMaps:** Manage sensitive information and application configurations securely.
**Network Policies:** Control pod-to-pod communication and enforce security boundaries.


**7. Monitoring and Logging**
**Metrics Server:** Provides resource metrics for monitoring.
**Prometheus:** Commonly used for monitoring and alerting.
ELK Stack (Elasticsearch, Logstash, Kibana): Often used for logging and visualizing log data.


**8. Extensibility**
**Custom Resource Definitions (CRDs)**: Allow users to extend Kubernetes with their resource types.
**Operators:** Controller patterns that manage the lifecycle of complex applications.


**9. Ecosystem and Tools**
**Helm:** A package manager for Kubernetes that simplifies deployment and management of applications.
**Kubectl:** The command-line tool for interacting with the Kubernetes API.
**Kubernetes Dashboard:** A web-based UI for managing cluster resources.


**10. Use Cases**

**Microservices Architecture:** Facilitates the deployment and management of microservices applications.
**CI/CD Pipelines:** Integrates with continuous integration and continuous deployment tools to automate application updates.
**Hybrid and Multi-Cloud Deployments:** Enables running applications across different cloud providers and on-premises environments.


                 **Kubernetes resources**
                 
**1. Pod** The smallest and simplest Kubernetes object, representing a single instance of a running process in a cluster.

**2. Deployment**  A resource that provides declarative updates to pods and replica sets.

**3. Service**  An abstraction that defines a logical set of pods and a policy for accessing them.

**4. ReplicaSet**  A resource that ensures a specified number of pod replicas are running at any given time.

**5. StatefulSet**  A resource designed for managing stateful applications.

**6. DaemonSet**  A resource that ensures that a copy of a specific pod runs on all (or a subset of) nodes in the cluster.

**7. Job**  A resource that manages the execution of a batch job.

**8. CronJob**  A resource that creates jobs on a scheduled basis.

**9. ConfigMap**  A resource used to store configuration data in key-value pairs.

**10. Secret**  A resource designed to store sensitive information, such as passwords, tokens, or SSH keys.

**11. PersistentVolume (PV)**  A resource that represents a piece of storage in the cluster.

**12. PersistentVolumeClaim (PVC)**  A request for storage by a user or application.

**13. Ingress**  A resource that manages external access to services, typically HTTP/S traffic.

**14. NetworkPolicy**  A resource that controls the traffic flow at the IP address or port level between pods.




                                     ** Deploy Core Resources**

**Create Deployment and Service for Your Application
● Purpose:** Deploys your application (e.g., nginx) and exposes it via a Service of type NodePort, allowing it to be accessed within the cluster and from outside on a specified port.
                    Step 1: Deployment.yaml
                            kubectl apply -f deployment.yaml

Step 2: **networkpolicy.yaml**
**Apply Network Policies - Allow Traffic to Your Application Pods
● Purpose:** Allows incoming traffic to your application pods on port 80, specifying which pods are allowed to receive traffic.


**Step 3: egress.yaml
Allow Egress Traffic to Specific IP
● Purpose:** Allows your application pods to send outgoing traffic to a specific IP range on port 80, controlling where your pods can send data.



**Step 4: ingress-controller.yaml
Deploy Ingress Controller
● Purpose:** Deploys the NGINX Ingress Controller in the namespace, managing external access to services within the cluster.



**Step 5: service.yaml
Expose Ingress Controller Service
● Purpose:** Exposes the NGINX Ingress Controller via NodePort, allowing external access to the Ingress Controller on specific ports (30080 for HTTP, 30443 for HTTPS).

**Step 6: ingress.yaml
Create Ingress Resource
● Purpose:** Configures routing rules to direct external traffic to the my-app-service based on the hostname and path, enabling access to your application via a friendly URL. 


**Step 7:  Verify Deployments and Services
Check Pod and Service Status
kubectl get all - get the status of all pods , deployment** , 

**kubectl get ingress - get status of ingress
● Purpose: Ensure that all pods and services, including the Ingress Controller, are running and available as expected.**












kubectl port-forward service/my-app-service -n namespace 
8080:80



