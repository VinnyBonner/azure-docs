---
title: "Trend Micro Vision One (using Azure Function) connector for Microsoft Sentinel"
description: "Learn how to install the connector Trend Micro Vision One (using Azure Function) to connect your data source to Microsoft Sentinel."
author: cwatson-cat
ms.topic: how-to
ms.date: 02/23/2023
ms.service: microsoft-sentinel
ms.author: cwatson
---

# Trend Micro Vision One (using Azure Function) connector for Microsoft Sentinel

The [Trend Micro Vision One](https://www.trendmicro.com/en_us/business/products/detection-response/xdr.html) connector provides the capability to ingest workbench alerts from the Trend Micro Vision One API into Microsoft Sentinel. The connector provides visibility into these log types in Microsoft Sentinel to view dashboards, create custom alerts, and to improve monitoring and investigation capabilities.

## Connector attributes

| Connector attribute | Description |
| --- | --- |
| **Log Analytics table(s)** | TrendMicro_XDR_WORKBENCH_CL<br/> TrendMicro_XDR_RCA_Task_CL<br/> TrendMicro_XDR_RCA_Result_CL<br/> TrendMicro_XDR_OAT_CL<br/> |
| **Data collection rules support** | Not currently supported |
| **Supported by** | [Trend Micro](https://success.trendmicro.com/dcx/s/?language=en_US) |

## Query samples

**Critical & High Severity Workbench Alerts**
   ```kusto
TrendMicro_XDR_WORKBENCH_CL
           
   | where severity_s  == 'critical' or severity_s == 'high'
   ```

**Medium & Low Severity Workbench Alerts**
   ```kusto
TrendMicro_XDR_WORKBENCH_CL
           
   | where severity_s  == 'medium' or severity_s == 'low'
   ```



## Prerequisites

To integrate with Trend Micro Vision One (using Azure Function) make sure you have: 

- **Microsoft.Web/sites permissions**: Read and write permissions to Azure Functions to create a Function App is required. [See the documentation to learn more about Azure Functions](/azure/azure-functions).
- **Trend Micro Vision One API Token**: A Trend Micro Vision One API Token is required. See the documentation to learn more about the [Trend Micro Vision One API](https://automation.trendmicro.com/xdr/home).


## Vendor installation instructions


> [!NOTE]
   >  This connector uses Azure Functions to connect to the Trend Micro Vision One API to pull its logs into Microsoft Sentinel. This might result in additional data ingestion costs. Check the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/) for details.


>**(Optional Step)** Securely store workspace and API authorization key(s) or token(s) in Azure Key Vault. Azure Key Vault provides a secure mechanism to store and retrieve key values. [Follow these instructions](/azure/app-service/app-service-key-vault-references) to use Azure Key Vault with an Azure Function App.


**STEP 1 - Configuration steps for the Trend Micro Vision One API**

 [Follow these instructions](https://docs.trendmicro.com/en-us/enterprise/trend-micro-xdr-help/ObtainingAPIKeys) to create an account and an API authentication token.


**STEP 2 - Use the below deployment option to deploy the connector and the associated Azure Function**

>**IMPORTANT:** Before deploying the Trend Micro Vision One connector, have the Workspace ID and Workspace Primary Key (can be copied from the following), as well as the Trend Micro Vision One API Authorization Token, readily available.



Azure Resource Manager (ARM) Template Deployment

This method provides an automated deployment of the Trend Micro Vision One connector using an ARM Tempate.

1. Click the **Deploy to Azure** button below. 

	[![Deploy To Azure](https://aka.ms/deploytoazurebutton)](https://aka.ms/sentinel-trendmicroxdr-azuredeploy)
2. Select the preferred **Subscription**, **Resource Group** and **Location**. 
3. Enter a unique **Function Name**, **Workspace ID**, **Workspace Key**, **API Token** and **Region Code**. 
 - Note: Provide the appropriate region code based on where your Trend Micro Vision One instance is deployed: us, eu, au, in, sg, jp  
 - Note: If using Azure Key Vault secrets for any of the values above, use the`@Microsoft.KeyVault(SecretUri={Security Identifier})`schema in place of the string values. Refer to [Key Vault references documentation](/azure/app-service/app-service-key-vault-references) for further details. 
4. Mark the checkbox labeled **I agree to the terms and conditions stated above**. 
5. Click **Purchase** to deploy.



## Next steps

For more information, go to the [related solution](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/trendmicro.trend_micro_vision_one_xdr_mss?tab=Overview) in the Azure Marketplace.
