# SimpleDeployToAKS

## What is this project?
 This is a starter kind of project to get a hands-on practice for Containarizing and Delpoying  simple ASP.Net core web app (weather forecast) into Azure Kubernetes Cluster

## Disclaimer: The Azure resources used in this project may incur costs. Please review the potential charges carefully and ensure that you delete the resources after practice to avoid unnecessary expenses.

<img width="573" height="580" alt="image" src="https://github.com/user-attachments/assets/ab7cc29a-9d26-4743-a066-78cef35d78c2" />


## Steps

### 1. Prepare Local Set up

-   Refer to the 'Initial_setup.md' file in the project folder.

### 2. Prepare the ASP.Net core Web App 

-   Refer to the 'DemoForecastSolution' Folder
-   Please note some changes in the file Program.cs are made to app.UseSwaggerUI to access the swagger endpoint directly(without mentioning any paths)
-   Please note the settings mentioned in 'launchSettings.json' file

### 3. Build, Tag, and Push Docker Image

-   Run the docker build, tag, and push commands (refer to commands mentioned in `docker_acr_instructions.md`).

### 4. Deploy to AKS using kubectl

-   Prepare Deployment manifest, service manifest and deploy the application in AKS(refer to commands mentioned in `aks_deployment_instructions.md`).
