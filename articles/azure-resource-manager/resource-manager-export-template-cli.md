---
title: "aaaExport Resource Manager şablonu Azure CLI ile | Microsoft Docs"
description: "Azure Resource Manager ve Azure CLI tooexport bir kaynak grubundan bir şablon kullanın."
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
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="60aeb-103">Azure CLI ile Azure Resource Manager şablonları dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="60aeb-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="60aeb-104">Resource Manager tooexport, aboneliğinizdeki mevcut kaynaklardan bir Resource Manager şablonu sağlar.</span><span class="sxs-lookup"><span data-stu-id="60aeb-104">Resource Manager enables you tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="60aeb-105">Bu oluşturulan şablonu toolearn hello şablon söz dizimi veya tooautomate hello çözümünüzün yeniden dağıtımını gerektiği gibi çözümünüzü hakkında kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60aeb-105">You can use that generated template toolearn about hello template syntax or tooautomate hello redeployment of your solution as needed.</span></span>

<span data-ttu-id="60aeb-106">Bir şablon iki farklı şekilde tooexport olduğunu önemli toonote şöyledir:</span><span class="sxs-lookup"><span data-stu-id="60aeb-106">It is important toonote that there are two different ways tooexport a template:</span></span>

* <span data-ttu-id="60aeb-107">Bir dağıtım için kullanılan hello gerçek şablonu dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60aeb-107">You can export hello actual template that you used for a deployment.</span></span> <span data-ttu-id="60aeb-108">Merhaba özgün şablonda tam olarak göründüğü gibi hello dışarı aktarılan şablonu tüm hello parametreler ve değişkenler içerir.</span><span class="sxs-lookup"><span data-stu-id="60aeb-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="60aeb-109">Bu yaklaşım, tooretrieve şablon gerektiğinde faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="60aeb-109">This approach is helpful when you need tooretrieve a template.</span></span>
* <span data-ttu-id="60aeb-110">Merhaba hello kaynak grubunun geçerli durumunu temsil eden bir şablonu dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60aeb-110">You can export a template that represents hello current state of hello resource group.</span></span> <span data-ttu-id="60aeb-111">Merhaba dışarı aktarılan şablon dağıtımı için kullanılan herhangi bir şablonu dayanmıyor.</span><span class="sxs-lookup"><span data-stu-id="60aeb-111">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="60aeb-112">Bunun yerine, hello kaynak grubunun bir anlık görüntüdür bir şablon oluşturur.</span><span class="sxs-lookup"><span data-stu-id="60aeb-112">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="60aeb-113">Merhaba dışarı aktarılan şablon birçok sabit kodlu değer ve normalde tanımlayacağınız kadar fazla büyük olasılıkla parametre vardır.</span><span class="sxs-lookup"><span data-stu-id="60aeb-113">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="60aeb-114">Bu yaklaşım, hello kaynak grubu değiştirdiniz. yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="60aeb-114">This approach is useful when you have modified hello resource group.</span></span> <span data-ttu-id="60aeb-115">Şimdi, şablon olarak toocapture hello kaynak grubu gerekir.</span><span class="sxs-lookup"><span data-stu-id="60aeb-115">Now, you need toocapture hello resource group as a template.</span></span>

<span data-ttu-id="60aeb-116">Bu konuda, iki yaklaşım ortaya koyulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="60aeb-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="60aeb-117">Bir çözüm dağıtma</span><span class="sxs-lookup"><span data-stu-id="60aeb-117">Deploy a solution</span></span>

<span data-ttu-id="60aeb-118">bir şablonu dışarı aktarmak için iki tooillustrate yaklaşıyor, bir çözüm tooyour abonelik dağıtarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="60aeb-118">tooillustrate both approaches for exporting a template, let's start by deploying a solution tooyour subscription.</span></span> <span data-ttu-id="60aeb-119">Aboneliğinizi tooexport istediğiniz bir kaynak grubu zaten varsa, bu çözüm toodeploy sahip değil.</span><span class="sxs-lookup"><span data-stu-id="60aeb-119">If you already have a resource group in your subscription that you want tooexport, you do not have toodeploy this solution.</span></span> <span data-ttu-id="60aeb-120">Ancak, bu makalenin sonraki bölümlerinde hello toohello şablonu bu çözüm için ifade eder.</span><span class="sxs-lookup"><span data-stu-id="60aeb-120">However, hello remainder of this article refers toohello template for this solution.</span></span> <span data-ttu-id="60aeb-121">Merhaba örnek betik, bir depolama hesabı dağıtır.</span><span class="sxs-lookup"><span data-stu-id="60aeb-121">hello example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="60aeb-122">Şablonu dağıtım geçmişinden Kaydet</span><span class="sxs-lookup"><span data-stu-id="60aeb-122">Save template from deployment history</span></span>

<span data-ttu-id="60aeb-123">Hello kullanarak bir şablonu dağıtım geçmişinden alabilirsiniz [az grubu dağıtım verme](/cli/azure/group/deployment#export) komutu.</span><span class="sxs-lookup"><span data-stu-id="60aeb-123">You can retrieve a template from your deployment history by using hello [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="60aeb-124">daha önce dağıttığınız örnek kaydeder hello şablonu aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="60aeb-124">hello following example saves hello template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="60aeb-125">Merhaba şablon döndürür.</span><span class="sxs-lookup"><span data-stu-id="60aeb-125">It returns hello template.</span></span> <span data-ttu-id="60aeb-126">Merhaba JSON kopyalayın ve bir dosya olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="60aeb-126">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="60aeb-127">Merhaba tam şablon dağıtımı için kullanılan olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="60aeb-127">Notice that it is hello exact template you used for deployment.</span></span> <span data-ttu-id="60aeb-128">Merhaba parametreleri ve değişkenleri hello şablonunu github'dan eşleşir.</span><span class="sxs-lookup"><span data-stu-id="60aeb-128">hello parameters and variables match hello template from GitHub.</span></span> <span data-ttu-id="60aeb-129">Bu şablonu yeniden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60aeb-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="60aeb-130">Kaynak grubunu şablon olarak dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="60aeb-130">Export resource group as template</span></span>

<span data-ttu-id="60aeb-131">Bir şablon hello dağıtım geçmişinden almanın yerine hello kullanarak hello kaynak grubunun geçerli durumunu temsil eden bir şablonu alabilir [az grup verme](/cli/azure/group#export) komutu.</span><span class="sxs-lookup"><span data-stu-id="60aeb-131">Instead of retrieving a template from hello deployment history, you can retrieve a template that represents hello current state of a resource group by using hello [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="60aeb-132">Birçok değişiklikleri tooyour kaynak grubu yaptığınız ve varolan bir şablonu tüm hello değişiklikleri temsil ettiğinde bu komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="60aeb-132">You use this command when you have made many changes tooyour resource group and no existing template represents all hello changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="60aeb-133">Merhaba şablon döndürür.</span><span class="sxs-lookup"><span data-stu-id="60aeb-133">It returns hello template.</span></span> <span data-ttu-id="60aeb-134">Merhaba JSON kopyalayın ve bir dosya olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="60aeb-134">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="60aeb-135">GitHub hello şablonunda farklı olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="60aeb-135">Notice that it is different than hello template in GitHub.</span></span> <span data-ttu-id="60aeb-136">Farklı parametreler ve değişken vardır.</span><span class="sxs-lookup"><span data-stu-id="60aeb-136">It has different parameters and no variables.</span></span> <span data-ttu-id="60aeb-137">Merhaba depolama SKU ve konumu sabit kodlanmış toovalues önemlidir.</span><span class="sxs-lookup"><span data-stu-id="60aeb-137">hello storage SKU and location are hard-coded toovalues.</span></span> <span data-ttu-id="60aeb-138">Hello aşağıdaki örnekte gösterir hello dışarı aktarılan şablonu, ancak biraz farklı parametre adı şablonunuzu vardır:</span><span class="sxs-lookup"><span data-stu-id="60aeb-138">hello following example shows hello exported template, but your template has a slightly different parameter name:</span></span>

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

<span data-ttu-id="60aeb-139">Bu şablonu yeniden dağıtabilirsiniz, ancak tahmin hello depolama hesabı için benzersiz bir ad gerektirir.</span><span class="sxs-lookup"><span data-stu-id="60aeb-139">You can redeploy this template, but it requires guessing a unique name for hello storage account.</span></span> <span data-ttu-id="60aeb-140">Merhaba, parametre adını biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="60aeb-140">hello name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="60aeb-141">Dışarı aktarılan şablonu özelleştirme</span><span class="sxs-lookup"><span data-stu-id="60aeb-141">Customize exported template</span></span>

<span data-ttu-id="60aeb-142">Bu şablon toomake değiştirebilir, daha kolay toouse ve daha esnektir.</span><span class="sxs-lookup"><span data-stu-id="60aeb-142">You can modify this template toomake it easier toouse and more flexible.</span></span> <span data-ttu-id="60aeb-143">Daha fazla konumları, değişiklik hello konum özelliği toouse tooallow hello kaynak grubu ile aynı konumda hello:</span><span class="sxs-lookup"><span data-stu-id="60aeb-143">tooallow for more locations, change hello location property toouse hello same location as hello resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="60aeb-144">tooavoid tooguess Kaldır hello parametresi hello depolama hesabı adı için depolama hesabı için bir uniques adına sahip.</span><span class="sxs-lookup"><span data-stu-id="60aeb-144">tooavoid having tooguess a uniques name for storage account, remove hello parameter for hello storage account name.</span></span> <span data-ttu-id="60aeb-145">Bir depolama alanı adı soneki ve depolama SKU için bir parametre ekleyin:</span><span class="sxs-lookup"><span data-stu-id="60aeb-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="60aeb-146">Hello depolama hesabı adı hello uniqueString işleviyle oluşturan bir değişkeni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="60aeb-146">Add a variable that constructs hello storage account name with hello uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="60aeb-147">Merhaba hello depolama hesabı toohello değişkeninin adını ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="60aeb-147">Set hello name of hello storage account toohello variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="60aeb-148">Merhaba SKU toohello parametresini ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="60aeb-148">Set hello SKU toohello parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="60aeb-149">Şablonunuz şimdi şuna benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="60aeb-149">Your template now looks like:</span></span>

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

<span data-ttu-id="60aeb-150">Merhaba değiştirilmiş şablonunu yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="60aeb-150">Redeploy hello modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60aeb-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="60aeb-151">Next steps</span></span>
* <span data-ttu-id="60aeb-152">Merhaba portal tooexport bir şablon kullanma hakkında daha fazla bilgi için bkz: [mevcut kaynaklardan Azure Resource Manager şablonunu dışarı aktarma](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="60aeb-152">For information about using hello portal tooexport a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="60aeb-153">Şablon toodefine parametrelerinde bkz [şablonları yazma](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="60aeb-153">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="60aeb-154">Genel dağıtım hatalarını giderme ipuçları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="60aeb-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>