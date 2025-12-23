## The Problem
The Nautilus DevOps team has been tasked with setting up a containerized application. They need to create a Azure Container Registry (ACR) to store their Docker images. Once the repository is created, they will build a Docker image from a Dockerfile located on the azure-client host and push this image to the ACR repository. This process is essential for maintaining and deploying containerized applications in a streamlined manner.

1. Create a ACR repository named xfusionacr13935 under East US.

2. Pricing plan must be Basic.

3. Dockerfile already exists under /root/pyapp directory on azure-client host.

4. Build a Docker image using this Dockerfile and push the same to the newly created ACR repo. The image tag must be latest i.e xfusionacr13935:latest.

## The Solution
I'll start this by saying I'm quite comfortable with Docker and DockerHub. I have however, never used ACR so this should be pretty fun, I will expect plenty of Google. As always I'm going to try and do this with Azure CLI.


I first of all ran ```az acr list``` to see if any Azure Continer Registries were already created. They were not. So I got the name of the resource group with  ```az group list``` then created a new registry with the specified sku, location and name

```
az acr create --resource-group kml_rg_main-fd33d083ea89467f --name xfusionacr13935 --sku Basic --location eastus
```

Next, I logged into the ACR
```az acr login --name xfusionacr13935```

Then I ran ```cd /root/pyapp``` to get to the directory then built the image. The username is the name of the resitry with .azurecr.io on the end and the image name is exactly as requested. 
```
docker build -t xfusionacr13935.azurecr.io/xfusionacr13935:latest .
```

Next step was to push it to the ACR which is more or less exactly how you would push it to DockerHub.
```
docker push xfusionacr13935.azurecr.io/xfusionacr13935:latest
```

And finally, I couldnt find a way to list the images in the repo via the CLI. I tried and arguably spend most of my time trying to work this bit out. In the end the closest I got was this command which pretty much just confirmed it existed. 
```
az acr repository show --name xfusionacr13935 --image xfusionacr13935:latest
```

## Thoughts and takeaways

Thaty was fun :smile: I imagine if your org is fully intergrated into the Azure space, you likly use ACR, Azure DevOps, Azure Repos and all that good stuff. It's good to get some hands on with this stuff. Time for tea. 
