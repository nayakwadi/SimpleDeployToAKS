# Build and Push Docker Image to Azure Container Registry (ACR)

Follow the steps below to create a Docker image, tag it, and push it to
Azure Container Registry (ACR).

## Steps

Navigate to the project folder in your terminal and run the following
commands:

``` bash
# Login to Azure Container Registry
az acr login --name <ACR_NAME>

# Check Docker version
docker --version

# Build Docker image (this may take 15–20 minutes)
docker build -t demoforecastapp:latest -f ./DemoForecastProject/Dockerfile .

# Tag the image
docker tag demoforecastapp:latest <ACR_NAME>.azurecr.io/demoforecastapp:latest

# Push the image to ACR
docker push <ACR_NAME>.azurecr.io/demoforecastapp:latest
```
### In azure portal, go to the ACR--> Services-->Repositories. You should see the image