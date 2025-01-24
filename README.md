# Kubernetes-based Voting App Deployment on AWS EKS

This project demonstrates the deployment of a 3-tier voting application on AWS Elastic Kubernetes Service (EKS).

---

## Architecture

<img width="500"  alt="Screenshot 2025-01-24 at 11 36 44 PM" src="https://github.com/user-attachments/assets/9e0d7f4b-e503-41ce-b9e5-a4a56a933406" /> 
<img width="1279" alt="Screenshot 2025-01-25 at 12 45 15 AM" src="https://github.com/user-attachments/assets/8774962d-0886-4279-b444-4e03c9be7448" />


The application consists of the following components:

- **Frontend**: Web UI for users to view and vote on programming languages.
- **Backend API**: Handles CRUD operations and interacts with the database.
- **Database**: MongoDB for storing language data and vote counts.

These components are containerized and deployed to an EKS cluster.

---

## Key Features

- **Containerized Microservices**: Each component runs in isolated Docker containers.
- **Kubernetes Orchestration**: Leverages EKS for container management and scaling.
- **Persistent Database Storage**: MongoDB data persisted using Kubernetes volumes.
- **Secure Communication**: Configured Kubernetes secrets for database credentials.
- **Load Balancing**: Ingress controller and LoadBalancer services for external access.
- **Monitoring**: Health checks to ensure reliable operation.

---

## Deployment Steps

1. **Create an EKS cluster on AWS.**
2. **Install required tools** (e.g., `kubectl`, `AWS CLI`) on a management EC2 instance.
3. **Clone the Git repository**:
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```
4. **Configure Kubernetes context** to access the EKS cluster:
   ```bash
   aws eks update-kubeconfig --region <region> --name <cluster-name>
   ```
5. **Create a namespace** for the application:
   ```bash
   kubectl create namespace voting-app
   ```
6. **Deploy MongoDB StatefulSet and Service**:
   ```bash
   kubectl apply -f k8s/mongodb-statefulset.yaml
   kubectl apply -f k8s/mongodb-service.yaml
   ```
7. **Initialize the MongoDB replica set** (if needed).
8. **Load sample data** into the database.
9. **Deploy the backend API and frontend components**:
   ```bash
   kubectl apply -f k8s/backend-deployment.yaml
   kubectl apply -f k8s/frontend-deployment.yaml
   ```
10. **Expose the frontend service** via a LoadBalancer:
    ```bash
    kubectl apply -f k8s/frontend-service.yaml
    ```
11. **Access the application** using the frontend URL obtained from the LoadBalancer service.

---

## Validating the Deployment

1. **Verify API endpoints** by making HTTP requests to the API service.
2. **Observe the database contents** by executing commands on the MongoDB pods.
3. **Test full functionality** by interacting with the frontend application.

---

## Troubleshooting

### Database Connection Problems
- Check environment variables in Kubernetes secrets.
- Inspect logs of the MongoDB and API pods:
  ```bash
  kubectl logs <pod-name> -n voting-app
  ```

### Frontend Accessibility
- Verify the LoadBalancer service configuration.
- Ensure DNS propagation is complete.

---

## Contributing

Contributions are welcome! Please follow the standard GitHub workflow:

1. **Fork the repository**.
2. **Create a new branch**:
   ```bash
   git checkout -b <branch-name>
   ```
3. **Make your changes**.
4. **Submit a pull request**.

---

## License

This project is licensed under the [MIT License](LICENSE).
