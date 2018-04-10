# Stage and Deploy an Application on Azure

This demo will describe how to take a premade application, stage it from GitHub and then deploy it live to Azure.

## Azure

Log into Azure portal and open the Azure Command Line Interface (CLI).

### Set Parameters

    gitrepo=https://github.com/Azure-Samples/php-docs-hello-world
    webappname=azureAppDemo100418
    rg=appResourceGroup

To check the contents of a parameter use:

    echo <parameter>

### Using Azure Command Line Interface

Open Azure CLI and create a new Resource Group:

    az group create --location westeurope --name $rg

Create an App Service Plan, S1 tier:

    az appservice plan create --name $webappname --resource-group $rg --sku S1`

Create the Web Application:

    az webapp create --name $webappname --resource-group $rg \
    --plan $webappname`

Create a deployment slot, eg: "staging":

`az webapp deployment slot create --name $webappname --resource-group $rg \`

`--slot staging`

Deploy code to "Staging" slot from GitHub:

`az webapp deployment source config --name $webappname --resource-group $rg \`

`--slot staging --repo-url $gitrepo --branch master --manual-integration`

In the CLI, use the below command then copy and paste the result into your local browser:

`echo http://$webappname-staging.azurewebsites.net`

Deploy the application to live production:

`az webapp deployment slot swap --name $webappname --resource-group $rg \`

`--slot staging`

Again use the CLI, use the below command, to see the application live in production, paste the result into your local browser:

`echo http://$webappname.azurewebsites.net`

### Removing Resource Group

To delete the resource group and remove all resources accociated with it:

`az group delete --name $rg`