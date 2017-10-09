---
title: "aaaDeploy kaynakları tooAzure | Microsoft Docs"
description: "Azure PowerShell veya Azure CLI toodeploy kaynakları tooAzure kullanın. Merhaba kaynaklar bir Resource Manager şablonunda tanımlanır."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a><span data-ttu-id="384d2-104">Kaynakları tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="384d2-104">Deploy resources tooAzure</span></span>

<span data-ttu-id="384d2-105">Bu konuda gösterilmektedir nasıl toodeploy kaynakları tooyour Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="384d2-105">This topic shows how toodeploy resources tooyour Azure subscription.</span></span> <span data-ttu-id="384d2-106">Azure PowerShell veya Azure CLI toodeploy Merhaba, çözümünüz için altyapıyı tanımlayan Resource Manager şablonu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="384d2-106">You can use either Azure PowerShell or Azure CLI toodeploy a Resource Manager template that defines hello infrastructure for your solution.</span></span>

<span data-ttu-id="384d2-107">Bir giriş tooconcepts Kaynak Yöneticisi'nin için bkz: [Azure Resource Manager'a genel bakış](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="384d2-107">For an introduction tooconcepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="384d2-108">Dağıtım adımları</span><span class="sxs-lookup"><span data-stu-id="384d2-108">Steps for deployment</span></span>

<span data-ttu-id="384d2-109">Bu konu hello dağıttığınız varsayar [Örnek Depolama şablondaki](#example-storage-template) bu konuda.</span><span class="sxs-lookup"><span data-stu-id="384d2-109">This topic assumes you are deploying hello [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="384d2-110">Farklı bir şablon kullanabilirsiniz, ancak geçirdiğiniz hello parametreleri bu konuda gösterilen değerinden farklı.</span><span class="sxs-lookup"><span data-stu-id="384d2-110">You can use a different template, but hello parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="384d2-111">Bir şablonu oluşturduktan sonra şablonunuzu dağıtmak için hello genel adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="384d2-111">After creating a template, hello general steps for deploying your template are:</span></span>

1. <span data-ttu-id="384d2-112">Tooyour hesabında oturum</span><span class="sxs-lookup"><span data-stu-id="384d2-112">Log in tooyour account</span></span>
2. <span data-ttu-id="384d2-113">Merhaba abonelik toouse (yalnızca birden çok aboneliğiniz varsa ve toouse hello varsayılan abonelik olmayan bir istiyorsanız gerekli) seçin</span><span class="sxs-lookup"><span data-stu-id="384d2-113">Select hello subscription toouse (only necessary if you have multiple subscriptions, and you want toouse one that is not hello default subscription)</span></span>
3. <span data-ttu-id="384d2-114">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="384d2-114">Create a resource group</span></span>
4. <span data-ttu-id="384d2-115">Merhaba şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="384d2-115">Deploy hello template</span></span>
5. <span data-ttu-id="384d2-116">Dağıtım durumunuzu denetleme</span><span class="sxs-lookup"><span data-stu-id="384d2-116">Check your deployment status</span></span>

<span data-ttu-id="384d2-117">Merhaba aşağıdaki bölümlerde tooperform olanlar nasıl adımları ile göster [PowerShell](#powershell) veya [Azure CLI](#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="384d2-117">hello following sections show how tooperform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="384d2-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="384d2-118">PowerShell</span></span>

1. <span data-ttu-id="384d2-119">Azure PowerShell tooinstall bkz [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="384d2-119">tooinstall Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="384d2-120">tooquickly dağıtımına başlayın, hello aşağıdaki cmdlet'leri kullanın:</span><span class="sxs-lookup"><span data-stu-id="384d2-120">tooquickly get started with deployment, use hello following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="384d2-121">Merhaba `Set-AzureRmContext` cmdlet varsayılan aboneliğinizin dışında toouse bir abonelik isterseniz, yalnızca gerekli.</span><span class="sxs-lookup"><span data-stu-id="384d2-121">hello `Set-AzureRmContext` cmdlet is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="384d2-122">Tüm aboneliklerinizi ve kullanıcıların kimlikleri toosee kullanın:</span><span class="sxs-lookup"><span data-stu-id="384d2-122">toosee all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="384d2-123">Merhaba dağıtım birkaç dakika toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="384d2-123">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="384d2-124">Tamamlandığında aşağıdakine benzer bir ileti görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="384d2-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="384d2-125">kaynak grubu ve depolama hesabı olan toosee tooyour abonelik, kullanım dağıtılan:</span><span class="sxs-lookup"><span data-stu-id="384d2-125">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="384d2-126">Şablon dağıtırken, şablon parametrelerini PowerShell parametreleri olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="384d2-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="384d2-127">Hello varsayılan değerleri hello şablonda kullanılan şekilde hello daha önceki örnekteki hiçbir şablon parametreleri içermiyordu.</span><span class="sxs-lookup"><span data-stu-id="384d2-127">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="384d2-128">toodeploy başka bir depolama hesabı ve hello depolama adı öneki ve hello depolama hesabı SKU, kullanımı için parametre değerlerini sağlayın:</span><span class="sxs-lookup"><span data-stu-id="384d2-128">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="384d2-129">Artık kaynak grubunuzda iki depolama hesabı bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="384d2-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="384d2-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="384d2-130">Azure CLI</span></span>

1. <span data-ttu-id="384d2-131">Azure CLI tooinstall bkz [Azure CLI 2.0 yükleme](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="384d2-131">tooinstall Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="384d2-132">tooquickly dağıtımına başlayın, hello aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="384d2-132">tooquickly get started with deployment, use hello following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="384d2-133">Merhaba `az account set` komutu varsayılan aboneliğinizin dışında toouse bir abonelik isterseniz, yalnızca gerekli.</span><span class="sxs-lookup"><span data-stu-id="384d2-133">hello `az account set` command is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="384d2-134">Tüm aboneliklerinizi ve kullanıcıların kimlikleri toosee kullanın:</span><span class="sxs-lookup"><span data-stu-id="384d2-134">toosee all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="384d2-135">Merhaba dağıtım birkaç dakika toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="384d2-135">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="384d2-136">Tamamlandığında aşağıdakine benzer bir ileti görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="384d2-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="384d2-137">kaynak grubu ve depolama hesabı olan toosee tooyour abonelik, kullanım dağıtılan:</span><span class="sxs-lookup"><span data-stu-id="384d2-137">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="384d2-138">Şablon dağıtırken, şablon parametrelerini PowerShell parametreleri olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="384d2-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="384d2-139">Hello varsayılan değerleri hello şablonda kullanılan şekilde hello daha önceki örnekteki hiçbir şablon parametreleri içermiyordu.</span><span class="sxs-lookup"><span data-stu-id="384d2-139">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="384d2-140">toodeploy başka bir depolama hesabı ve hello depolama adı öneki ve hello depolama hesabı SKU, kullanımı için parametre değerlerini sağlayın:</span><span class="sxs-lookup"><span data-stu-id="384d2-140">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="384d2-141">Artık kaynak grubunuzda iki depolama hesabı bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="384d2-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="384d2-142">Örnek depolama şablonu</span><span class="sxs-lookup"><span data-stu-id="384d2-142">Example storage template</span></span>

<span data-ttu-id="384d2-143">Örnek şablon toodeploy bir depolama hesabı tooyour aboneliği aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="384d2-143">Use hello following example template toodeploy a storage account tooyour subscription:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
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
        "description": "hello type of replication toouse for hello storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a><span data-ttu-id="384d2-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="384d2-144">Next steps</span></span>

* <span data-ttu-id="384d2-145">PowerShell toodeploy şablonları kullanma hakkında ayrıntılı bilgi için bkz: [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="384d2-145">For detailed information about using PowerShell toodeploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="384d2-146">Azure CLI toodeploy şablonları kullanma hakkında ayrıntılı bilgi için bkz: [Resource Manager şablonları ve Azure CLI kaynaklarla dağıtmak](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span><span class="sxs-lookup"><span data-stu-id="384d2-146">For detailed information about using Azure CLI toodeploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



