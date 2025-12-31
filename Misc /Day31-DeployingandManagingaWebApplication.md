## The Problem 
The Nautilus DevOps team is tasked with deploying a Python-based web application on Azure. You need to create a web app using the following specifications:
1) The Web App name should be devops-webapp.
2) It should be created in the West US region under the default resource group.
3) The publish option should be set to Code.
4) The Runtime Stack should be Python with Linux as the operating system.
5) Create a new App Service Plan named devops-learn-python with the SKU Basic B1.
6) Application Insights should be disabled.
7) Add tags:

   - Name: WebAppLearning
   - Environment: Dev
   - 
Make sure the web app is in Running state after creation.

## The Solution
I used the GUI again for this as It's not a service I use a great deal. I'll take a look at how to deploy the exact same setup via the CLI at a later date so watch this space :smile:. First up, the main setup looked like this. Under 'Monitoring', insights is off by default. Leave it be. 
<img width="960" height="795" alt="image" src="https://github.com/user-attachments/assets/370a2db9-7c48-44f5-9caf-9da5872a3f31" />

Create your tags and then create the resource. Once it's running, you're done. 
<img width="781" height="493" alt="image" src="https://github.com/user-attachments/assets/600e406e-c1f1-4a7a-b062-e5a3e593aaac" />

## Thoughts and takeaways
That was an easy one. I've not touched web apps since doing AZ-104 so it was a nice quick refresh. Like all things Azure, I'd like to eventually work out how to do all this via the Azure CLI but I'll review it at a later date. Tea time. 

