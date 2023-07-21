
## Yolo Orchestration
### Description
In this project, Kubernetes (K8) is used to organize and control the YOLO app on a group of computers (cluster) and make it accessible. The YOLO app has two parts, the client-side and backend. The project ensures that the app is deployed and managed smoothly by leveraging Kubernetes features.

### Setup Instructions
To get started with the YOLO Kubernetes Orchestration, follow the steps below:
1. Make sure you have `minikube` and `kubect`l installed on your computer. These tools enable you to run Kubernetes clusters locally for testing and development. If you haven't installed them yet, refer to the installation instructions.
2. Clone the YOLO Kubernetes Orchestration repository to your computer using the command `git clone <repository-url>`.
3. Start Minikube on your computer by executing the appropriate command:
```
minikube start
```
4. In each directory, `client`, `backend` and `database`, you will find necessary Kubernetes manifests:
    - Deployment: Define the desired state and number of replicas for the client, backend and mongo components.
    - Service: Expose the client, backend and mongo components as Kubernetes services.
    - Secrets: Configure any environment-specific secrets or configuration required by the application as defined in the resctive directories secret files.
    - PVC (PersistentVolumeClaim): If applicable, set up persistent storage for the backend component.
    
   
5. To run the app, start by running the database, followed by the backend and then the client. at each stage make sure to update the secrets as required i.e. the backend uses the exposed url of the database and the client used the esposed endpoint of the backend service.
6. Apply the Kubernetes manifests using the `kubectl apply` command. For example for the mongo database:
Navigate to the respective folder e.g 
```
cd database
```
Run `kubectl apply` commands on each of the defined file starting with the `secrets` down to the `service`
```
kubectl apply -f mongo-pv.yaml
kubectl apply -f mongo-pvc.yaml
kubectl apply -f mongo-secrets.yaml
kubectl apply -f deployment.yaml
kubectl apply -f mongo-service.yaml
```
7. To use the orchestrated app, you can simply visit the link provided in the deployment tab of your Kubernetes user interface. Alternatively, you can find the external IP of the client service by running a specific command:
```
kubectl get svc
```

### Technology Used
The YOLO Kubernetes Orchestration project is primarily created using YAML, which is a common language used to write Kubernetes configuration files. These files define how Kubernetes objects like Deployments, Services, and PersistentVolumeClaims should be set up and managed.
