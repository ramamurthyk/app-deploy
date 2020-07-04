# Provision database node and web node via Azure ARM

This template creates an Azure Cosmos account and Azure Web App, then automatically deploys the [Web application](https://github.com/ramamurthyk/web-app) hosted on GitHub and injects the Cosmos DB endpoint and auth key into the Web App's Application Settings allowing it to connect automatically upon first run.

This template enables automatic provisioning of Azure resources and automated deployment of the web application in a ready to run state without any manual intervention. There is no need to add/update database connection details manually.

Below are the parameters which can be user configured in the parameters file including:

- **Application Name:** Name of the Cosmos DB account, App Plan and Web App.
- **Location:** Azure region for all the resources.
- **App Service Plan Tier:** App Service Plan's pricing tier.
- **App Service Plan Instances:** App Service Plan's instance count.
- **Repository URL:** The URL for the GitHub repository that contains the Web app project to deploy.
- **Branch:** The branch of the GitHub repository to use.
- **Database Name:** The Cosmos DB database name.
- **Container Name:** The Cosmos DB container name.

[Deploy To Azure](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Framamurthyk%2Fapp-deploy%2Fmaster%2Fazuredeploy.json)