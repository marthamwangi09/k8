## Yolo k8 Orchestration
project involves running an application with two parts, the `backend` and `clien`t, along with `MongoDB` on a Kubernetes platform. To achieve this, various Kubernetes resources are used, such as Deployments, Services, PersistentVolume (PV), PersistentVolumeClaim (PVC), and Secrets.

### Choice of Kubernetes Objects for Deployment:
`Deployments` are used to define the desired state of the application and handle multiple copies of the application (replicas). This ensures that the specified number of replicas is always running, and Kubernetes takes care of scaling, updating, and rolling back the application as needed. In this project, we have deployments for the `backend`, `client`, and `MongoDB`.

`Services` are essential for making the backend and client applications accessible to other components within the Kubernetes cluster. By creating Services, we ensure that the pods can be reached using a consistent DNS name and IP.

For the MongoDB database, a `StatefulSet` is used. StatefulSets are ideal for applications like databases that need stable and persistent storage. They provide unique identities and stable hostnames for each replica pod, which is crucial for maintaining data integrity during scaling and updates.

Sensitive information like database passwords and API keys are stored securely using Kubernetes `Secrets`. In this project, Secrets are utilized to store the MongoDB user login credentials, the MongoDB URL used in the backend deployments, and the client's backend URL for making requests.

### Exposing Pods to Internet Traffic:
To expose the pods to internet traffic, Kubernetes Services are used. These Services provide a stable endpoint (IP address and DNS name) that allows other components within or outside the cluster to access the pods. The project employs a LoadBalancer type of Service in Kubernetes for this purpose.

### Use of Persistent Storage:
For the MongoDB database's data integrity, Kubernetes PersistentVolume (PV) and PersistentVolumeClaim (PVC) are utilized. The PersistentVolume represents a physical storage device available cluster-wide, while the PersistentVolumeClaim is a request for storage made by a pod. The PVC binds to the PV, ensuring reliable storage for MongoDB data.

### Git Workflow:
All the Kubernetes configuration files (K8 files) are version-controlled using Git, along with other project files. Any changes to these files are committed and pushed to a Git repository to track and manage the project effectively.
