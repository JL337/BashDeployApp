# Stage and Deploy an Application to Azure

This demo will describe how to take an application, stage it from GitHub and then deploy it live using Azure.

## Azure

Log into Azure portal with your credentials and open the Azure Command Line Interface (CLI).

### Set Parameters

    gitrepo=https://github.com/Azure-Samples/php-docs-hello-world
    webappname=azureAppDemo100418
    rg=appResourceGroup

To check the contents of a parameter use:

    echo $<parameter>

### Managing the Application

#### Getting Started
Open Azure CLI and create a new Resource Group:

    az group create --location westeurope --name $rg

Create an App Service Plan, S1 tier will be used:

    az appservice plan create --name $webappname --resource-group $rg --sku S1`

Create the Web Application:

    az webapp create --name $webappname --resource-group $rg \
    --plan $webappname`

#### Deploying to Staging Environment

Create a Deployment Slot, eg: "staging":

    az webapp deployment slot create --name $webappname --resource-group $rg \
    --slot staging`

Deploy code to "Staging" slot from GitHub:  

    az webapp deployment source config --name $webappname --resource-group $rg \
    --slot staging --repo-url $gitrepo --branch master --manual-integration`

Use the below command then copy and paste the result into your local browser:
    
    echo http://$webappname-staging.azurewebsites.net`

#### Deploying to Live Production

Deploy the application to live production:
    
    az webapp deployment slot swap --name $webappname --resource-group $rg \`
    --slot staging

Use the below command, to see the application live in production, paste the result into your local browser:
    
    echo http://$webappname.azurewebsites.net

### Removing Resource Group

To delete the resource group and remove all resources accociated with it:
    
    az group delete --name $rg