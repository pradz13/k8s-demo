# K8S

Kubernetes is a container orchestration tool.

**K8S Architecture**

K8S Cluster is made up of one master node and multiple worker nodes. Each node has _kubelet_ agent running on it for communication.

Worker nodes have applications deployed on them.

The master node runs _API Server_ which is the entry point to the K8S cluster. API Server can interact with the Command Line, UI or APIs. The master node also has _Controller Manager_ which keeps track of what is happening in the cluster. It also has a _Scheduler_ responsible for Pod replacement. It also has _etcd_ which is a data store that holds the current status of any k8s component.

Master node and Worker nodes are connected through a _Virtual Machine_. In production, multiple master nodes can run.

**K8S Components**

Pod - Smaller deployment unit, abstraction on the container. Each pod has an IP address associated with it. Pods can die easily, a new pod gets created.

Service - Permanent IP address which does not change even if the Pod dies. It works as a load balancer.

Ingress - Makes application available externally. Request comes to Ingress first then it gets forwarded to Service.

ConfigMap and Secret - ConfigMap keeps the configurations of the application. Secret configurations are kept in Secret.

Volume - Attaches physical storage(local or remote) on a hard drive to the Pod. Even if the pod dies, data remains.

Deployment - Blueprint of Pods.

StatefulSet - For stateful apps like databases to ensure database consistency. Setting up StatefulSet is very difficult, so it is recommended to use an external database.

**Kubernetes Configuration**

Configurations are sent to API Server through YML or JSON file. Each configuration file has 3 parts - metadata, specification, and status(automatically managed by k8s).

**Minikube and kubetctl**

Minikube - One node cluster for local testing. Minikube runs as a Docker container.

Start minikube cluster : _minikube start —driver docker_

kubectl - Command line tool for k8s. It will automatically get installed with Minikube.

Shows all the nodes in kubectl cluster - kubectl get node

kubectl apply -f <file_name.yaml> - Runs the configurations written in a yaml file.

====================================================================================================

Create the config -
kubectl apply -f mongo-config.yaml

Create the secrets -
kubectl apply -f mongo-secret.yaml

Create the database -
kubectl apply -f mongo.yaml

Create the web applcation -
kubectl apply -f webapp.yaml

Run the following commands to validate the deployments -

kubectl get all - Gives all the deployed objects
kubectl get configmap - Shows configmap
kubectl get secret - Shows secret
kubectl describe service webapp-service - Shows details of the service
kubectl logs <pod name> - Shows the logs of a pod (Add -f option to steam the logs)
kubectl get svc - Get the service
kubectl get node -o wide - Check the INTERNAL-IP from the output of this command
minikube service webapp-service --url - Shows the URL for accessing the webapp
