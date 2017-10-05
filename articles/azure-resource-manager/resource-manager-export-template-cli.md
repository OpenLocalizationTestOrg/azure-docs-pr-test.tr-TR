---
title: "Azure CLI ile Resource Manager şablonu aktarma | Microsoft Docs"
description: "Bir şablonu kaynak grubundan dışarı aktarmak için Azure Resource Manager ve Azure CLI kullanın."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 617664129a5353e25da1e90c742c4b009db172ef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="84a37-103">Azure CLI ile Azure Resource Manager şablonları dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="84a37-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="84a37-104">Resource Manager, aboneliğinizde var olan kaynaklardan bir Resource Manager şablonunu dışarı aktarmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="84a37-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="84a37-105">Bu oluşturulan şablonu şablon söz dizimi hakkında bilgi edinmek veya çözümünüzün yeniden dağıtımını gerektiği gibi otomatikleştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84a37-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="84a37-106">Bir şablonu dışarı aktarmak için iki farklı yol vardır:</span><span class="sxs-lookup"><span data-stu-id="84a37-106">It is important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="84a37-107">Dağıtım için kullandığınız gerçek şablonu dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84a37-107">You can export the actual template that you used for a deployment.</span></span> <span data-ttu-id="84a37-108">Dışarı aktarılan şablonda, tüm parametreler ve değişkenler özgün şablondaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="84a37-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="84a37-109">Bir şablon almanız gerektiğinde, bu yararlı bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="84a37-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="84a37-110">Kaynak grubunun geçerli durumunu temsil eden bir şablonu dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84a37-110">You can export a template that represents the current state of the resource group.</span></span> <span data-ttu-id="84a37-111">Dışarı aktarılan şablon, dağıtım için kullandığınız herhangi bir şablonu temel almaz.</span><span class="sxs-lookup"><span data-stu-id="84a37-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="84a37-112">Bunun yerine, kaynak grubunun anlık görüntüsü olan bir şablon oluşturur.</span><span class="sxs-lookup"><span data-stu-id="84a37-112">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="84a37-113">Dışarı aktarılan şablon birçok sabit kodlu değer ve büyük olasılıkla normalde tanımlayacağınızdan daha az sayıda parametre içerir.</span><span class="sxs-lookup"><span data-stu-id="84a37-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="84a37-114">Bu yaklaşım, kaynak grubu değiştirdiniz. yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="84a37-114">This approach is useful when you have modified the resource group.</span></span> <span data-ttu-id="84a37-115">Şimdi kaynak grubunu bir şablon olarak yakalamalısınız.</span><span class="sxs-lookup"><span data-stu-id="84a37-115">Now, you need to capture the resource group as a template.</span></span>

<span data-ttu-id="84a37-116">Bu konuda, iki yaklaşım ortaya koyulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="84a37-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="84a37-117">Bir çözüm dağıtma</span><span class="sxs-lookup"><span data-stu-id="84a37-117">Deploy a solution</span></span>

<span data-ttu-id="84a37-118">Bir şablonu dışarı aktarmak için her iki yaklaşımın göstermek için Aboneliğinize bir çözümü başlayalım.</span><span class="sxs-lookup"><span data-stu-id="84a37-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="84a37-119">Aboneliğinizdeki vermek istediğiniz bir kaynak grubu zaten varsa, bu çözümü dağıtmak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="84a37-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span></span> <span data-ttu-id="84a37-120">Ancak, bu makalenin sonraki bölümlerinde Bu çözüm için şablonu ifade eder.</span><span class="sxs-lookup"><span data-stu-id="84a37-120">However, the remainder of this article refers to the template for this solution.</span></span> <span data-ttu-id="84a37-121">Örnek komut dosyasını bir depolama hesabı dağıtır.</span><span class="sxs-lookup"><span data-stu-id="84a37-121">The example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="84a37-122">Şablonu dağıtım geçmişinden Kaydet</span><span class="sxs-lookup"><span data-stu-id="84a37-122">Save template from deployment history</span></span>

<span data-ttu-id="84a37-123">Kullanarak bir şablonu dağıtım geçmişinden alabilirsiniz [az grubu dağıtım verme](/cli/azure/group/deployment#export) komutu.</span><span class="sxs-lookup"><span data-stu-id="84a37-123">You can retrieve a template from your deployment history by using the [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="84a37-124">Aşağıdaki örnek, daha önce dağıttığınız şablonu kaydeder:</span><span class="sxs-lookup"><span data-stu-id="84a37-124">The following example saves the template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="84a37-125">Şablon döndürür.</span><span class="sxs-lookup"><span data-stu-id="84a37-125">It returns the template.</span></span> <span data-ttu-id="84a37-126">JSON kopyalayın ve bir dosya olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="84a37-126">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="84a37-127">Dağıtım için kullanılan tam şablonu olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="84a37-127">Notice that it is the exact template you used for deployment.</span></span> <span data-ttu-id="84a37-128">Parametreler ve değişkenler github'dan şablon eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="84a37-128">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="84a37-129">Bu şablonu yeniden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84a37-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="84a37-130">Kaynak grubunu şablon olarak dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="84a37-130">Export resource group as template</span></span>

<span data-ttu-id="84a37-131">Bir şablonu dağıtım geçmişinden almanın yerine kullanarak bir kaynak grubunun geçerli durumunu temsil eden bir şablonu alabilir [az grup verme](/cli/azure/group#export) komutu.</span><span class="sxs-lookup"><span data-stu-id="84a37-131">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="84a37-132">Kaynak grubu için çok sayıda değişiklik yaptınız ve tüm değişiklikleri olan bir şablonunu temsil ettiğinde bu komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="84a37-132">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="84a37-133">Şablon döndürür.</span><span class="sxs-lookup"><span data-stu-id="84a37-133">It returns the template.</span></span> <span data-ttu-id="84a37-134">JSON kopyalayın ve bir dosya olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="84a37-134">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="84a37-135">GitHub şablonunda farklı olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="84a37-135">Notice that it is different than the template in GitHub.</span></span> <span data-ttu-id="84a37-136">Farklı parametreler ve değişken vardır.</span><span class="sxs-lookup"><span data-stu-id="84a37-136">It has different parameters and no variables.</span></span> <span data-ttu-id="84a37-137">Depolama SKU ve konum değerleri sabit kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="84a37-137">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="84a37-138">Aşağıdaki örnek, dışarı aktarılan şablon gösterir, ancak şablonunuzu biraz farklı parametre adı vardır:</span><span class="sxs-lookup"><span data-stu-id="84a37-138">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

<span data-ttu-id="84a37-139">Bu şablonu yeniden dağıtabilirsiniz, ancak depolama hesabı için benzersiz bir ad tahmin gerektirir.</span><span class="sxs-lookup"><span data-stu-id="84a37-139">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="84a37-140">Parametrenizin adını biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="84a37-140">The name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="84a37-141">Dışarı aktarılan şablonu özelleştirme</span><span class="sxs-lookup"><span data-stu-id="84a37-141">Customize exported template</span></span>

<span data-ttu-id="84a37-142">Bu şablonu kullanmayı daha kolay ve daha esnek hale getirmek için değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84a37-142">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="84a37-143">Daha fazla konumları için izin vermek için aynı konumu kaynak grubu olarak kullanmak üzere konum özelliği değiştirin:</span><span class="sxs-lookup"><span data-stu-id="84a37-143">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="84a37-144">Depolama hesabı için bir uniques ad tahmin yapmak zorunda kalmamak için depolama hesabı adı için parametresini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="84a37-144">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="84a37-145">Bir depolama alanı adı soneki ve depolama SKU için bir parametre ekleyin:</span><span class="sxs-lookup"><span data-stu-id="84a37-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

<span data-ttu-id="84a37-146">Depolama hesabı adı uniqueString işlevi ile oluşturur bir değişkeni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="84a37-146">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="84a37-147">Depolama hesabı adı değişkeni ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="84a37-147">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="84a37-148">SKU parametreyi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="84a37-148">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="84a37-149">Şablonunuz şimdi şuna benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="84a37-149">Your template now looks like:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="84a37-150">Değiştirilen şablon yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="84a37-150">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84a37-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="84a37-151">Next steps</span></span>
* <span data-ttu-id="84a37-152">Bir şablonu dışarı aktarmak için portalı kullanma hakkında daha fazla bilgi için bkz: [mevcut kaynaklardan Azure Resource Manager şablonunu dışarı aktarma](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="84a37-152">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="84a37-153">Şablonda parametreleri tanımlamak için bkz: [şablonları yazma](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="84a37-153">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="84a37-154">Genel dağıtım hatalarını giderme ipuçları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="84a37-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>