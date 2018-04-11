# Stage and Deploy an Application using Azure Cloud Shell and Bash

This demo will describe how to take an application, stage it from GitHub and then deploy it live using Azure.
The Cloud Shell (Bash) on the Azure portal will be used, however you can also use Bash with Azure CLI.

## Managing your Application

### Prerequisites

Using Bash or CMD:

[Install Latest Version of Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)

Check Azure CLI has been downoaded successfully:

    Az

Log in using your credentials:

    az login

You may need to authenticate your device to log in, so follow the prompt if any.

Enter the code that was displayed into your browser link, then choose your Microsoft account to be associated with Microsoft Azure Cross-platform Command Line Interface. Close the browser window after completed.

Check on your console that you have linked your account successfully.

### Managing the Application

#### Getting Started

### Set Parameters

    gitrepo=https://github.com/Azure-Samples/php-docs-hello-world

    webappname=azureAppDemo100418

    rg=appResourceGroup

To check the contents of a parameter use:

    echo $<parameter>

### Allocate resources and storage

Create a new Resource Group:

    az group create --location westeurope --name $rg

Create an App Service Plan, S1 tier will be used:

    az appservice plan create --name $webappname --resource-group $rg --sku S1

Create the Web Application:

    az webapp create --name $webappname --resource-group $rg \
    --plan $webappname

### Deploying to Staging Environment

Create a Deployment Slot, eg: "staging":

    az webapp deployment slot create --name $webappname --resource-group $rg \
    --slot staging

Deploy code to "Staging" slot from GitHub:  

    az webapp deployment source config --name $webappname --resource-group $rg \
    --slot staging --repo-url $gitrepo --branch master --manual-integration

Use the below command then copy and paste the result into your local browser:
    
    echo http://$webappname-staging.azurewebsites.net

### Deploying to Live Production

Deploy the application to live production:
    
    az webapp deployment slot swap --name $webappname --resource-group $rg \
    --slot staging

Use the below command, to see the application live in production, paste the result into your local browser:
    
    echo http://$webappname.azurewebsites.net

### Removing Resource Group

To delete the resource group and remove all resources accociated with it:
If parameter does not work, check the Resource Group Associated with your application.
    
    az group delete --name $rg