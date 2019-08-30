# Microsoft Azure Cheat Sheet



## Azure Resource Manager
Main site: https://docs.microsoft.com/en-us/azure/azure-resource-manager/


### Template Deployment

Template format:

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "",
      "apiProfile": "",
      "parameters": {  },
      "variables": {  },
      "functions": [  ],
      "resources": [  ],
      "outputs": {  }
    }

Example:

    "resources": [
      {
        "apiVersion": "2016-01-01",
        "type": "Microsoft.Storage/storageAccounts",
        "name": "mystorageaccount",
        "location": "westus",
        "sku": {
          "name": "Standard_LRS"
        },
        "kind": "Storage",
        "properties": {
        }
      }
    ]

Example with parameters:

    "parameters": {
      "storageSKU": {
        "type": "string",
        "allowedValues": [
          "Standard_LRS",
          "Standard_ZRS",
          "Standard_GRS",
          "Standard_RAGRS",
          "Premium_LRS"
        ],
        "defaultValue": "Standard_LRS",
        "metadata": {
          "description": "The type of replication to use for the storage account."
        }
      }   
    },
    "resources": [
      {
        "type": "Microsoft.Storage/storageAccounts",
        "sku": {
          "name": "[parameters('storageSKU')]"
        },
        ...
      }
    ]

More info:
- https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates
- [Azure Resource Manager template best practices](https://docs.microsoft.com/en-us/azure/azure-resource-manager/template-best-practices)
    - Parameter names should be camelCase
    - Each parameter should have a description
    - Each resource should have a comment
- [Azure Resource Manager Schemas](https://github.com/Azure/azure-resource-manager-schemas)
    - Includes validation tool
    - [Schemas for resources](https://docs.microsoft.com/en-us/azure/templates/)
- Get keys from Microsoft.DocumentDB/databaseAccounts:
    - Via REST: https://docs.microsoft.com/en-us/rest/api/cosmos-db-resource-provider/DatabaseAccounts/ListKeys
    - On Stack Overflow: https://stackoverflow.com/questions/42486845/azure-arm-templates-documentdb-primarymasterkey-as-output
    - https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-template-functions-resource#reference



