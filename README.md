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

The automatic provisioning requires minimal inputs as the default values are supplied in the template files. It is advisable to login to deploy this template in a new resource group.

# The quickest way to deploy this template is as follows

## Azure CLI via Azure Portal
- Login to Azure Portal
- Open Cloud Shell
- Create a new resource group (preferred) by executing the following command. Replace the placeholder <resource-group-name> with the actual value. E.g. 'demo-app'
	
`az group create --name <resource-group-name> --location 'North Europe'`
- Deploy the template by executing the following command. Replace the placeholder <resource-group-name> with the actual value. E.g. 'demo-app'

`az deployment group create --resource-group <resource-group-name> --template-uri https://raw.githubusercontent.com/ramamurthyk/app-deploy/master/azuredeploy.json`

**OR**

## Deploy To Azure
- Login to Azure Portal
- Control/Command + Click [Deploy To Azure](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Framamurthyk%2Fapp-deploy%2Fmaster%2Fazuredeploy.json) to open the Azure custom deployment in a new tab
- Select the Azure subscription where you want the services to be deployed
- Create a new resource group (preferred)
- Review and change rest of the parameters which are already pre-populated with default values
- Agree to T&C and click on Purchase

Please note that the Azure Cosmos DB instance provisioning takes a while (up to 10 minutes). Please monitor the status of the deployment which should create the following resources:
- Azure app service
- Azure app service plan
- Cosmos DB instance

## Post deployment verification
Obtain the URL of the newly created web application. Issue the POST request as shown below:

`curl -X POST https://web-appb4movm6kck2ms.azurewebsites.net/app -d ''`

Please note that the URL will be different based on your Azure environment.

On successful execution, the API should result in a response containing the id and timestamp of the newly created item in the database.

`{
	"id":"050f71eb-eae1-4736-b8b8-6d6453989992",
	"timestamp":"2020-07-05T19:08:14.0528635Z"
}`
