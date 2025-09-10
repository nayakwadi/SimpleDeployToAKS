# Deploy Application to AKS

Follow the steps below to deploy your application to Azure Kubernetes
Service (AKS).

## Steps

### 1. Prepare Deployment File

-   Refer to the `deployment.yaml` file in the project folder.

### 2. Build, Tag, and Push Docker Image

-   Run the docker build, tag, and push commands (refer to commands
    mentioned in `Docker_Image_Steps.txt`).

### 3. Deploy to AKS using kubectl

Open VS Code, navigate to the project folder path, and run the following
commands.\
Ensure that: - The ACR is linked to AKS. - The ACR already has the image
uploaded.

``` bash
# Apply deployment file
kubectl apply -f deployment.yaml

# Check deployments
kubectl get deployments

# Describe the deployment
kubectl describe deployment demoforecastapp

# Get pods
kubectl get pods

# Describe a specific pod
kubectl describe pod <name_of_the_pod>

# View pod logs
kubectl logs <name_of_the_pod>
```

### 4. Expose Application via Service

The application is not accessible yet. You need to create a service file
to access it.

-   Prepare a `service.yaml` file (refer to the file in project
    folder).\
-   Run the following commands:

``` bash
# Apply service file
kubectl apply -f service.yaml

# List all services with ClusterIP & ExternalIP
kubectl get services

# Get specific service details
kubectl get service demoforecastapp-service

# Describe the service. Capture the LoadBalancer IP address.
kubectl describe service demoforecastapp-service
```

### 5. In a browser, go to LoadBalancer IP address, it should take you to the swagger page. 