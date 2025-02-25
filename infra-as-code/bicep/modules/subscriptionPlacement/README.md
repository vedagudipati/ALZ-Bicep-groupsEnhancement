# Module:  Subscription Placement

This module moves one or more subscriptions to be a child of the specified management group. Once the subscription(s) are moved under the management group, Azure Policies assigned to the management group or its parent management group(s) will begin to govern the subscription(s).

> Consider using the `subPlacementAll` orchestration module instead to simplify Subscription placement across your entire Management Group hierarchy in a single module. [infra-as-code/bicep/orchestration/subPlacementAll](https://github.com/Azure/ALZ-Bicep/tree/main/infra-as-code/bicep/orchestration/subPlacementAll)

## Parameters

The module requires the following required input parameters.

 | Parameter                  | Type            | Description                                                                 | Requirement                                  | Example                                                                                                                                                                                        |
 | -------------------------- | --------------- | --------------------------------------------------------------------------- | -------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
 | parSubscriptionIds         | Array | Array of Subscription Ids that should be moved to the new management group. | Mandatory input, default: `[]`                              | Empty: `[]` or <br />1 Subscription: `["yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy"]` or<br />Many Subscriptions: `["xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy"]` |
 | parTargetManagementGroupId | string          | Target management group for the subscription.                               | Mandatory input, management group must exist | `alz-platform-connectivity`                                                                                                                                                                    |
 | parTelemetryOptOut         | bool            | Set Parameter to true to Opt-out of deployment telemetry                    | Optional input, default: `false`                                         | `false`                                                                                                                                                                                        |

## Outputs
*This module does not produce any outputs.*

## Deployment

In this example, the subscription `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` will be moved to `alz-platform-connectivity` management group. The inputs for this module are defined in `parameters/subscriptionPlacement.parameters.all.json`.

> For the  examples below we assume you have downloaded or cloned the Git repo as-is and are in the root of the repository as your selected directory in your terminal of choice.

### Azure CLI
```bash
# For Azure global regions
az deployment mg create \
  --template-file infra-as-code/bicep/modules/subscriptionPlacement/subscriptionPlacement.bicep \
  --parameters @infra-as-code/bicep/modules/subscriptionPlacement/parameters/subscriptionPlacement.parameters.all.json \
  --location eastus \
  --management-group-id alz
```
OR
```bash
# For Azure China regions
az deployment mg create \
  --template-file infra-as-code/bicep/modules/subscriptionPlacement/subscriptionPlacement.bicep \
  --parameters @infra-as-code/bicep/modules/subscriptionPlacement/parameters/subscriptionPlacement.parameters.all.json \
  --location chinaeast2 \
  --management-group-id alz
```

### PowerShell

```powershell
# For Azure global regions
New-AzManagementGroupDeployment `
  -TemplateFile infra-as-code/bicep/modules/subscriptionPlacement/subscriptionPlacement.bicep `
  -TemplateParameterFile infra-as-code/bicep/modules/subscriptionPlacement/parameters/subscriptionPlacement.parameters.all.json `
  -Location eastus `
  -ManagementGroupId alz
```
OR
```powershell
# For Azure China regions
New-AzManagementGroupDeployment `
  -TemplateFile infra-as-code/bicep/modules/subscriptionPlacement/subscriptionPlacement.bicep `
  -TemplateParameterFile infra-as-code/bicep/modules/subscriptionPlacement/parameters/subscriptionPlacement.parameters.all.json `
  -Location chinaeast2 `
  -ManagementGroupId alz
```

## Bicep Visualizer

![Bicep Visualizer](media/bicepVisualizer.png "Bicep Visualizer")
