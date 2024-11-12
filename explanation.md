## Explanation of Key Design Choices
# 1. Kubernetes Objects Used for Deployment
Frontend & Backend Deployments:

I chose to use Deployments for the frontend and backend services to ensure high availability and scalability. The ReplicaSet feature of Deployments manages pod replicas and enables seamless updates.
MongoDB StatefulSet:
MongoDB is deployed using a StatefulSet to maintain stable network identities for each pod. This choice ensures consistent data storage and retrieval, crucial for a database system. Using a PersistentVolumeClaim (PVC) with the StatefulSet allows data to persist even if the pod is restarted or rescheduled.

# 2. Exposing Pods to Internet Traffic
LoadBalancer Services:
The frontend and backend pods are exposed using LoadBalancer services, which provide an external IP for internet access. This approach simplifies exposing services to external traffic on Google Kubernetes Engine (GKE).
ClusterIP for MongoDB:
The MongoDB service uses ClusterIP to restrict access to internal cluster communications only, ensuring that the database is secure and only accessible by the backend.

# 3. Persistent Storage
MongoDB Persistent Storage:
Persistent storage is implemented using PersistentVolume and PersistentVolumeClaim. This setup ensures that MongoDB data is not lost if a pod is deleted or restarted, providing data reliability and continuity.
No Persistent Storage for Frontend/Backend:
The frontend and backend do not require persistent storage because they serve transient data and are stateless by design. This helps in optimizing resource usage.

# 4. Git Workflow
Branching Strategy:
The main branch is always kept in a deployable state. Feature branches are created for new features or fixes, merged through pull requests after code review.
Commit and Push:
Changes are committed frequently with descriptive messages. The final version is pushed to the main branch for deployment on GKE.