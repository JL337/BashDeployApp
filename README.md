# Stage and Deploy an Application on Azure

This demo will describe how to take an application, stage it and then Deploy to Azure.

## Using Azure CLI

Using premade application: 

`gitrepo=https://github.com/Azure-Samples/php-docs-hello-world`
`webappname=mywebapp01`

Open Azure CLI and create the Resource Group:

`az group create --location westeurope --name appResourceGroup`

Create an App Service Plan, S1 tier:

`az appservice plan create --name $webappname --resource-group myResourceGroup --sku S1`

Create the web application:

`az webapp create --name $webappname --resource-group myResourceGroup \`
`--plan $webappname`
