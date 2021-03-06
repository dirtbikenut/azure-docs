---
title: Azure Resource Manager template functions - resources | Microsoft Docs
description: Describes the functions to use in an Azure Resource Manager template to retrieve values about resources.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn

ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/24/2019
ms.author: tomfitz

---
# Resource functions for Azure Resource Manager templates

Resource Manager provides the following functions for getting resource values:

* [list*](#list)
* [providers](#providers)
* [reference](#reference)
* [resourceGroup](#resourcegroup)
* [resourceId](#resourceid)
* [subscription](#subscription)

To get values from parameters, variables, or the current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).

<a id="listkeys" />
<a id="list" />

## list*

`list{Value}(resourceName or resourceIdentifier, apiVersion, functionValues)`

The syntax for this function varies by name of the list operations. Each implementation returns values for the resource type that supports a list operation. The operation name must start with `list`. Some common usages are `listKeys` and `listSecrets`. 

### Parameters

| Parameter | Required | Type | Description |
|:--- |:--- |:--- |:--- |
| resourceName or resourceIdentifier |Yes |string |Unique identifier for the resource. |
| apiVersion |Yes |string |API version of resource runtime state. Typically, in the format, **yyyy-mm-dd**. |
| functionValues |No |object | An object that has values for the function. Only provide this object for functions that support receiving an object with parameter values, such as **listAccountSas** on a storage account. | 

### Implementations

The possible uses of list* are shown in the following table.

| Resource type | Function name |
| ------------- | ------------- |
| Microsoft.Addons/supportProviders | listsupportplaninfo |
| Microsoft.AnalysisServices/servers | listGatewayStatus |
| Microsoft.Automation/automationAccounts | listKeys |
| Microsoft.AzureStack/registrations/products | listDetails |
| Microsoft.Batch/batchAccounts | listkeys |
| Microsoft.BatchAI/workspaces/experiments/jobs | listoutputfiles |
| Microsoft.BingMaps/mapApis | listSecrets |
| Microsoft.BingMaps/mapApis | listSingleSignOnToken |
| Microsoft.Cache/redis | listKeys |
| Microsoft.Cache/redis | listUpgradeNotifications |
| Microsoft.CognitiveServices/accounts | listKeys |
| Microsoft.ContainerRegistry/registries/buildTasks | listSourceRepositoryProperties |
| Microsoft.ContainerRegistry/registries/buildTasks/steps | listBuildArguments |
| Microsoft.ContainerRegistry/registries | listBuildSourceUploadUrl |
| Microsoft.ContainerRegistry/registries | listCredentials |
| Microsoft.ContainerRegistry/registries | listPolicies |
| Microsoft.ContainerRegistry/registries | listUsages |
| Microsoft.ContainerRegistry/registries/runs | listLogSasUrl |
| Microsoft.ContainerRegistry/registries/tasks | listDetails |
| Microsoft.ContainerRegistry/registries/webhooks | listEvents |
| Microsoft.ContainerService/managedClusters/accessProfiles | listCredential |
| Microsoft.ContainerService/managedClusters | listClusterAdminCredential |
| Microsoft.ContainerService/managedClusters | listClusterUserCredential |
| Microsoft.ContentModerator/applications | listSecrets |
| Microsoft.ContentModerator/applications | listSingleSignOnToken |
| Microsoft.ContentModerator | listCommunicationPreference |
| Microsoft.DataBox/jobs | listCredentials |
| Microsoft.DataFactory/datafactories/gateways | listauthkeys |
| Microsoft.DataFactory/factories/integrationruntimes | listauthkeys |
| Microsoft.DataLakeAnalytics/accounts/storageAccounts/Containers | listSasTokens |
| Microsoft.Devices/elasticPools/iotHubTenants/iotHubKeys | listkeys |
| Microsoft.Devices/elasticPools/iotHubTenants | listKeys |
| Microsoft.Devices/iotHubs/iotHubKeys | listkeys |
| Microsoft.Devices/iotHubs | listkeys |
| Microsoft.Devices/provisioningServices/keys | listkeys |
| Microsoft.Devices/provisioningServices | listkeys |
| Microsoft.DevSpaces/controllers | listConnectionDetails |
| Microsoft.DevTestLab/labs | ListVhds |
| Microsoft.DevTestLab/labs/schedules | ListApplicable |
| Microsoft.DevTestLab/labs/users/serviceFabrics | ListApplicableSchedules |
| Microsoft.DevTestLab/labs/virtualMachines | ListApplicableSchedules |
| Microsoft.DocumentDB/databaseAccounts | listConnectionStrings |
| Microsoft.DocumentDB/databaseAccounts | listKeys |
| Microsoft.DomainRegistration | listDomainRecommendations |
| Microsoft.DomainRegistration/topLevelDomains | listAgreements |
| Microsoft.EventGrid/topics | listKeys |
| Microsoft.EventHub/namespaces/authorizationRules | listkeys |
| Microsoft.EventHub/namespaces/disasterRecoveryConfigs/authorizationRules | listkeys |
| Microsoft.EventHub/namespaces/eventhubs/authorizationRules | listkeys |
| Microsoft.ImportExport/jobs | listBitLockerKeys |
| Microsoft.Insights | ListMigrationDate |
| Microsoft.LabServices/users | ListEnvironments |
| Microsoft.LabServices/users | ListLabs |
| Microsoft.LocationBasedServices/accounts | listKeys |
| Microsoft.LocationServices/accounts | listKeys |
| Microsoft.Logic/integrationAccounts/agreements | listContentCallbackUrl |
| Microsoft.Logic/integrationAccounts/assemblies | listContentCallbackUrl |
| Microsoft.Logic/integrationAccounts | listCallbackUrl |
| Microsoft.Logic/integrationAccounts | listKeyVaultKeys |
| Microsoft.Logic/integrationAccounts/maps | listContentCallbackUrl |
| Microsoft.Logic/integrationAccounts/partners | listContentCallbackUrl |
| Microsoft.Logic/integrationAccounts/schemas | listContentCallbackUrl |
| Microsoft.Logic/workflows/accessKeys | list |
| Microsoft.Logic/workflows | listCallbackUrl |
| Microsoft.Logic/workflows | listSwagger |
| Microsoft.Logic/workflows/runs/actions | listExpressionTraces |
| Microsoft.Logic/workflows/runs/actions/repetitions | listExpressionTraces |
| Microsoft.Logic/workflows/triggers | listCallbackUrl |
| Microsoft.Logic/workflows/versions/triggers | listCallbackUrl |
| Microsoft.MachineLearning/webServices | listkeys |
| Microsoft.MachineLearning/Workspaces | listworkspacekeys |
| Microsoft.MachineLearningCompute/operationalizationClusters | listKeys |
| Microsoft.MachineLearningServices/workspaces/computes | listKeys |
| Microsoft.MachineLearningServices/workspaces | listKeys |
| Microsoft.Maps/accounts | listKeys |
| Microsoft.MarketplaceApps/ClassicDevServices | listSecrets |
| Microsoft.MarketplaceApps/ClassicDevServices | listSingleSignOnToken |
| Microsoft.Media/mediaservices/assets | listContainerSas |
| Microsoft.Media/mediaservices/assets | listStreamingLocators |
| Microsoft.Media/mediaservices/streamingLocators | listContentKeys |
| Microsoft.Media/mediaservices/streamingLocators | listPaths |
| Microsoft.Network/applicationSecurityGroups | listIpConfigurations |
| microsoft.network/vpngateways | listvpnconnectionshealth |
| Microsoft.NotificationHubs/Namespaces/authorizationRules | listkeys |
| Microsoft.NotificationHubs/Namespaces/NotificationHubs/authorizationRules | listkeys |
| Microsoft.OperationalInsights/workspaces | listKeys |
| Microsoft.OperationalInsights/workspaces | listKeys |
| Microsoft.PolicyInsights/remediations | listDeployments |
| Microsoft.Relay/namespaces/authorizationRules | listkeys |
| Microsoft.Relay/namespaces/disasterRecoveryConfigs/authorizationRules | listkeys |
| Microsoft.Relay/namespaces/HybridConnections/authorizationRules | listkeys |
| Microsoft.Relay/namespaces/WcfRelays/authorizationRules | listkeys |
| Microsoft.SaaS/saasresources | listaccesstoken |
| Microsoft.Search/searchServices | listAdminKeys |
| Microsoft.Search/searchServices | listQueryKeys |
| Microsoft.ServiceBus/namespaces/authorizationRules | listkeys |
| Microsoft.ServiceBus/namespaces/disasterRecoveryConfigs/authorizationRules | listkeys |
| Microsoft.ServiceBus/namespaces/queues/authorizationRules | listkeys |
| Microsoft.ServiceBus/namespaces/topics/authorizationRules | listkeys |
| Microsoft.SignalRService/SignalR | listFeatures |
| Microsoft.SignalRService/SignalR | listkeys |
| Microsoft.Storage/storageAccounts | listAccountSas |
| Microsoft.Storage/storageAccounts | listkeys |
| Microsoft.Storage/storageAccounts | listServiceSas |
| Microsoft.StorSimple/managers/devices | listFailoverSets |
| Microsoft.StorSimple/managers/devices | listFailoverTargets |
| Microsoft.StorSimple/managers | listActivationKey |
| Microsoft.StorSimple/managers | listPublicEncryptionKey |
| microsoft.web/apimanagementaccounts/apis/connections | listconnectionkeys |
| microsoft.web/apimanagementaccounts/apis/connections | listsecrets |
| Microsoft.Web/connectionGateways | ListStatus |
| microsoft.web/connections | listconsentlinks |
| Microsoft.Web/customApis | listWsdlInterfaces |
| microsoft.web/locations | listwsdlinterfaces |
| microsoft.web/sites/backups | list |
| Microsoft.Web/sites/config | list |
| microsoft.web/sites/functions | listsecrets |
| microsoft.web/sites/hybridconnectionnamespaces/relays | listkeys |
| microsoft.web/sites | listsyncfunctiontriggerstatus |
| microsoft.web/sites/slots/backups | list |
| Microsoft.Web/sites/slots/config | list |
| microsoft.web/sites/slots/functions | listsecrets |


### Return value

The returned object varies by the list function you use. For example, the listKeys for a storage account returns the following format:

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

Other list functions have different return formats. To see the format of a function, include it in the outputs section as shown in the example template. 

### Remarks

The [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*. To use this function in a template, provide an object with the body parameter values.

To determine which resource types have a list operation, you have the following options:

* View the [REST API operations](/rest/api/) for a resource provider, and look for list operations. For example, storage accounts have the [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).
* Use the [Get-​Azure​Rm​Provider​Operation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet. The following example gets all list operations for storage accounts:

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* Use the following Azure CLI command to filter only the list operations:

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

Specify the resource by using either the resource name or the [resourceId function](#resourceid). When using this function in the same template that deploys the referenced resource, use the resource name.

### Example

The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/listkeys.json) shows how to return the primary and secondary keys from a storage account in the outputs section. It also returns a SAS token for the storage account. To get that token, it passes an object to listAccountSas function. This example is intended to show how you use the list functions. Typically, you would use the SAS token in a resource value rather than return it as an output value. Output values are stored in the deployment history and aren't secure. You must specify an expiry time in the future for the deployment to succeed.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storagename": {
            "type": "string"
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus"
        },
        "accountSasProperties": {
            "type": "object",
            "defaultValue": {
                "signedServices": "b",
                "signedPermission": "r",
                "signedExpiry": "2018-08-20T11:00:00Z",
                "signedResourceTypes": "s"
            }
        }
    },
    "resources": [
        {
            "apiVersion": "2018-02-01",
            "name": "[parameters('storagename')]",
            "location": "[parameters('location')]",
            "type": "Microsoft.Storage/storageAccounts",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "StorageV2",
            "properties": {
                "supportsHttpsTrafficOnly": false,
                "accessTier": "Hot",
                "encryption": {
                    "services": {
                        "blob": {
                            "enabled": true
                        },
                        "file": {
                            "enabled": true
                        }
                    },
                    "keySource": "Microsoft.Storage"
                }
            },
            "dependsOn": []
        }
    ],
    "outputs": {
        "keys": {
            "type": "object",
            "value": "[listKeys(parameters('storagename'), '2018-02-01')]"
        },
        "accountSAS": {
            "type": "object",
            "value": "[listAccountSas(parameters('storagename'), '2018-02-01', parameters('accountSasProperties'))]"
        }
    }
}
``` 

To deploy this example template with Azure CLI, use:

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/listkeys.json --parameters storagename=<your-storage-account>
```

To deploy this example template with PowerShell, use:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/listkeys.json -storagename <your-storage-account>
```

<a id="providers" />

## providers
`providers(providerNamespace, [resourceType])`

Returns information about a resource provider and its supported resource types. If you don't provide a resource type, the function returns all the supported types for the resource provider.

### Parameters

| Parameter | Required | Type | Description |
|:--- |:--- |:--- |:--- |
| providerNamespace |Yes |string |Namespace of the provider |
| resourceType |No |string |The type of resource within the specified namespace. |

### Return value

Each supported type is returned in the following format: 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

Array ordering of the returned values isn't guaranteed.

### Example

The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/providers.json) shows how to use the provider function:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "providerNamespace": {
            "type": "string"
        },
        "resourceType": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers(parameters('providerNamespace'), parameters('resourceType'))]",
            "type" : "object"
        }
    }
}
```

For the **Microsoft.Web** resource provider and **sites** resource type, the preceding example returns an object in the following format:

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

To deploy this example template with Azure CLI, use:

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/providers.json --parameters providerNamespace=Microsoft.Web resourceType=sites
```

To deploy this example template with PowerShell, use:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/providers.json -providerNamespace Microsoft.Web -resourceType sites
```

<a id="reference" />

## reference
`reference(resourceName or resourceIdentifier, [apiVersion], ['Full'])`

Returns an object representing a resource's runtime state.

### Parameters

| Parameter | Required | Type | Description |
|:--- |:--- |:--- |:--- |
| resourceName or resourceIdentifier |Yes |string |Name or unique identifier of a resource. |
| apiVersion |No |string |API version of the specified resource. Include this parameter when the resource isn't provisioned within same template. Typically, in the format, **yyyy-mm-dd**. |
| 'Full' |No |string |Value that specifies whether to return the full resource object. If you don't specify `'Full'`, only the properties object of the resource is returned. The full object includes values such as the resource ID and location. |

### Return value

Every resource type returns different properties for the reference function. The function doesn't return a single, predefined format. Also, the returned value differs based on whether you specified the full object. To see the properties for a resource type, return the object in the outputs section as shown in the example.

### Remarks

The reference function retrieves the runtime state of either a previously deployed resource or a resource deployed in the current template. This article shows examples for both scenarios. When referencing a resource in the current template, provide only the resource name as a parameter. When referencing a previously deployed resource, provide the resource ID and an API version for the resource. You can determine valid API versions for your resource in the [template reference](/azure/templates/).

The reference function can only be used in the properties of a resource definition and the outputs section of a template or deployment.

By using the reference function, you implicitly declare that one resource depends on another resource if the referenced resource is provisioned within same template and you refer to the resource by its name (not resource ID). You don't need to also use the dependsOn property. The function isn't evaluated until the referenced resource has completed deployment.

To see the property names and values for a resource type, create a template that returns the object in the outputs section. If you have an existing resource of that type, your template returns the object without deploying any new resources. 

Typically, you use the **reference** function to return a particular value from an object, such as the blob endpoint URI or fully qualified domain name.

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

Use `'Full'` when you need resource values that aren't part of the properties schema. For example, to set key vault access policies, get the identity properties for a virtual machine.

```json
{
  "type": "Microsoft.KeyVault/vaults",
  "properties": {
    "tenantId": "[reference(concat('Microsoft.Compute/virtualMachines/', variables('vmName')), '2017-03-30', 'Full').identity.tenantId]",
    "accessPolicies": [
      {
        "tenantId": "[reference(concat('Microsoft.Compute/virtualMachines/', variables('vmName')), '2017-03-30', 'Full').identity.tenantId]",
        "objectId": "[reference(concat('Microsoft.Compute/virtualMachines/', variables('vmName')), '2017-03-30', 'Full').identity.principalId]",
        "permissions": {
          "keys": [
            "all"
          ],
          "secrets": [
            "all"
          ]
        }
      }
    ],
    ...
```

For the complete example of the preceding template, see [Windows to Key Vault](https://github.com/rjmax/AzureSaturday/blob/master/Demo02.ManagedServiceIdentity/demo08.msiWindowsToKeyvault.json). A similar example is available for [Linux](https://github.com/rjmax/AzureSaturday/blob/master/Demo02.ManagedServiceIdentity/demo07.msiLinuxToArm.json).

### Example

The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/referencewithstorage.json) deploys a resource, and references that resource.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      },
      "fullReferenceOutput": {
        "type": "object",
        "value": "[reference(parameters('storageAccountName'), '2016-12-01', 'Full')]"
      }
    }
}
``` 

The preceding example returns the two objects. The properties object is in the following format:

```json
{
   "creationTime": "2017-10-09T18:55:40.5863736Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

The full object is in the following format:

```json
{
  "apiVersion":"2016-12-01",
  "location":"southcentralus",
  "sku": {
    "name":"Standard_LRS",
    "tier":"Standard"
  },
  "tags":{},
  "kind":"Storage",
  "properties": {
    "creationTime":"2017-10-09T18:55:40.5863736Z",
    "primaryEndpoints": {
      "blob":"https://examplestorage.blob.core.windows.net/",
      "file":"https://examplestorage.file.core.windows.net/",
      "queue":"https://examplestorage.queue.core.windows.net/",
      "table":"https://examplestorage.table.core.windows.net/"
    },
    "primaryLocation":"southcentralus",
    "provisioningState":"Succeeded",
    "statusOfPrimary":"available",
    "supportsHttpsTrafficOnly":false
  },
  "subscriptionId":"<subscription-id>",
  "resourceGroupName":"functionexamplegroup",
  "resourceId":"Microsoft.Storage/storageAccounts/examplestorage",
  "referenceApiVersion":"2016-12-01",
  "condition":true,
  "isConditionTrue":true,
  "isTemplateResource":false,
  "isAction":false,
  "provisioningOperation":"Read"
}
```

To deploy this example template with Azure CLI, use:

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/referencewithstorage.json --parameters storageAccountName=<your-storage-account>
```

To deploy this example template with PowerShell, use:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/referencewithstorage.json -storageAccountName <your-storage-account>
```

The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/reference.json) references a storage account that isn't deployed in this template. The storage account already exists within the same subscription.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageResourceGroup": {
            "type": "string"
        },
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageAccountName')), '2018-07-01')]",
            "type": "object"
        }
    }
}
```

To deploy this example template with Azure CLI, use:

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/reference.json --parameters storageResourceGroup=<rg-for-storage> storageAccountName=<your-storage-account>
```

To deploy this example template with PowerShell, use:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/reference.json -storageResourceGroup <rg-for-storage> -storageAccountName <your-storage-account>
```

<a id="resourcegroup" />

## resourceGroup
`resourceGroup()`

Returns an object that represents the current resource group. 

### Return value

The returned object is in the following format:

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### Remarks

The `resourceGroup()` function can't be used in a template that is [deployed at the subscription level](deploy-to-subscription.md). It can only be used in templates that are deployed to a resource group.

A common use of the resourceGroup function is to create resources in the same location as the resource group. The following example uses the resource group location to assign the location for a web site.

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### Example

The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/resourcegroup.json) returns the properties of the resource group.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "resourceGroupOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

The preceding example returns an object in the following format:

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

To deploy this example template with Azure CLI, use:

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/resourcegroup.json
```

To deploy this example template with PowerShell, use:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/resourcegroup.json 
```

<a id="resourceid" />

## resourceId
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

Returns the unique identifier of a resource. You use this function when the resource name is ambiguous or not provisioned within the same template. 

### Parameters

| Parameter | Required | Type | Description |
|:--- |:--- |:--- |:--- |
| subscriptionId |No |string (In GUID format) |Default value is the current subscription. Specify this value when you need to retrieve a resource in another subscription. |
| resourceGroupName |No |string |Default value is current resource group. Specify this value when you need to retrieve a resource in another resource group. |
| resourceType |Yes |string |Type of resource including resource provider namespace. |
| resourceName1 |Yes |string |Name of resource. |
| resourceName2 |No |string |Next resource name segment if resource is nested. |

### Return value

The identifier is returned in the following format:

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### Remarks

When used with a [subscription-level deployment](deploy-to-subscription.md), the `resourceId()` function can only retrieve the ID of resources deployed at that level. For example, you can get the ID of a policy definition or role definition, but not the ID of a storage account. For deployments to a resource group, the opposite is true. You can't get the resource ID of resources deployed at the subscription-level.

The parameter values you specify depend on whether the resource is in the same subscription and resource group as the current deployment. To get the resource ID for a storage account in the same subscription and resource group, use:

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

To get the resource ID for a storage account in the same subscription but a different resource group, use:

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

To get the resource ID for a storage account in a different subscription and resource group, use:

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

To get the resource ID for a database in a different resource group, use:

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

To get the resource ID of a subscription-level resource when deploying at the subscription scope, use:

```json
"[resourceId('Microsoft.Authorization/policyDefinitions', 'locationpolicy')]"
```

Often, you need to use this function when using a storage account or virtual network in an alternate resource group. The following example shows how a resource from an external resource group can easily be used:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### Example

The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/resourceid.json) returns the resource ID for a storage account in the resource group:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('11111111-1111-1111-1111-111111111111', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

The output from the preceding example with the default values is:

| Name | Type | Value |
| ---- | ---- | ----- |
| sameRGOutput | String | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | String | /subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | String | /subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | String | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName |

To deploy this example template with Azure CLI, use:

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/resourceid.json
```

To deploy this example template with PowerShell, use:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/resourceid.json 
```

<a id="subscription" />

## subscription
`subscription()`

Returns details about the subscription for the current deployment. 

### Return value

The function returns the following format:

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### Example

The following [example template](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/functions/subscription.json) shows the subscription function called in the outputs section. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

To deploy this example template with Azure CLI, use:

```azurecli-interactive
az group deployment create -g functionexamplegroup --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/subscription.json
```

To deploy this example template with PowerShell, use:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName functionexamplegroup -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/functions/subscription.json 
```

## Next steps
* For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).
* To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).
* To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).
* To see how to deploy the template you've created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).

