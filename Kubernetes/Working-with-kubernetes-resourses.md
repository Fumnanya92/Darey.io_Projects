# Deploying Applications in Kubernetes

Deploying applications in Kubernetes is a fundamental skill that every beginner needs to grasp. Deployment involves the process of taking your application code and running it on a Kubernetes cluster, ensuring that it scales, manages resources efficiently, and stays resilient. This hands-on project will guide you through deploying your first application using Minikube, a lightweight, single-node Kubernetes cluster perfect for beginners.

## Deployments in Kubernetes

In Kubernetes, a Deployment is a declarative approach to managing and scaling applications. It provides a blueprint for the desired state of your application, allowing Kubernetes to handle the complexities of deploying and managing replicas. Whether you're running a simple web server or a more complex microservices architecture, Deployments are the cornerstone for maintaining application consistency and availability.

## Services in Kubernetes

Once your application is deployed, it needs a way to be accessed by other parts of your system or external users. This is where Services come into play. In Kubernetes, a Service is an abstraction that defines a logical set of Pods and a policy by which to access them. It acts as a stable endpoint to connect to your application, allowing for easy communication within the cluster or from external sources. Some of the several types of Services in Kubernetes include:

- **ClusterIP**: The default type. Exposes the Service on a cluster-internal IP. Accessible only within the cluster.
- **NodePort**: Exposes the Service on each Node's IP at a static port (NodePort). Accessible externally using the Node IP.
- **LoadBalancer**: Exposes the Service externally using a cloud provider's load balancer. Accessible externally through the load balancer's IP.

## Mini Project: Working with Kubernetes Resources

In subsequent sections, we will dive deep into deployment strategies and service configurations within the Kubernetes ecosystem, delving into the intricacies of these components to ensure a thorough understanding and proficiency in their utilization.

### Deploying a Minikube Sample Application

Using YAML files for deployments and services in Kubernetes is like crafting a detailed plan for your application, while direct deployment with `kubectl` commands is more like giving quick, on-the-spot instructions to launch and manage your application. Let's create a Minikube deployment and service with `kubectl`.

#### Step-by-Step Instructions

1. **Start Minikube**:
   ```sh
   minikube start
   ```

2. **Create a Deployment**:
   ```sh
   kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
   ```
   The command above creates a Kubernetes Deployment named "hello-minikube" running the "kicbase/echo-server:1.0" container image.

3. **Expose the Deployment as a Service**:
   ```sh
   kubectl expose deployment hello-minikube --type=NodePort --port=8080
   ```
   The command above exposes the Kubernetes Deployment named "hello-minikube" as a NodePort service on port 8080.

4. **Get Service Details**:
   ```sh
   kubectl get services hello-minikube
   ```

5. **Access the Service**:
   The easiest way to access this service is to let Minikube launch a web browser for you.
   ```sh
   minikube service hello-minikube
   ```

By following these steps, you will have successfully deployed and exposed a sample application on Minikube using Kubernetes.
