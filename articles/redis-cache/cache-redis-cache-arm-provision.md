---
title: "Azure Resource Manager kullanarak bir Redis önbelleği sağlama | Microsoft Docs"
description: "Bir Azure Redis önbelleği dağıtmak için Azure Resource Manager şablonunu kullanın."
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: cce5d63e8bad2dd066cb4c28e2a8a9cb16c47953
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="fee3a-103">Şablon kullanarak Redis Önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="fee3a-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="fee3a-104">Bu konuda, bir Azure Redis önbelleği dağıtan bir Azure Resource Manager şablonunun nasıl oluşturulacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fee3a-104">In this topic, you learn how to create an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="fee3a-105">Önbellek tanılama verilerini korumak için varolan bir depolama hesabı ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fee3a-105">The cache can be used with an existing storage account to keep diagnostic data.</span></span> <span data-ttu-id="fee3a-106">Ayrıca nasıl tanımlamak için hangi kaynağın dağıtılan ve ne zaman dağıtım yürütülen parametreler tanımlamak nasıl belirtilen öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fee3a-106">You also learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="fee3a-107">Bu şablonu kendi dağıtımlarınız için kullanabilir veya kendi gereksinimlerinize göre özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fee3a-107">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="fee3a-108">Şu anda bir abonelik için aynı bölgede tüm önbellekler için tanılama ayarları paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="fee3a-108">Currently, diagnostic settings are shared for all caches in the same region for a subscription.</span></span> <span data-ttu-id="fee3a-109">Bir önbellek bölgede güncelleştirme bölgedeki tüm diğer önbellekleri etkiler.</span><span class="sxs-lookup"><span data-stu-id="fee3a-109">Updating one cache in the region affects all other caches in the region.</span></span>

<span data-ttu-id="fee3a-110">Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fee3a-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="fee3a-111">Tam şablon için bkz: [Redis önbelleği şablon](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="fee3a-111">For the complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="fee3a-112">Resource Manager şablonları yeni [Premium katmanı](cache-premium-tier-intro.md) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fee3a-112">Resource Manager templates for the new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="fee3a-113">Kümeleme Premium Redis önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="fee3a-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="fee3a-114">Premium Redis önbelleği ile veri kalıcılığını oluşturma</span><span class="sxs-lookup"><span data-stu-id="fee3a-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="fee3a-115">VNet ve isteğe bağlı kümeleme Premium Redis önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="fee3a-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="fee3a-116">Son şablonları denetlemek için bkz: [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/) arayın ve `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="fee3a-116">To check for the latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="fee3a-117">Dağıtmak</span><span class="sxs-lookup"><span data-stu-id="fee3a-117">What you will deploy</span></span>
<span data-ttu-id="fee3a-118">Bu şablonda bir Azure Redis Tanılama verileri için mevcut bir depolama hesabını kullanan önbelleği dağıtır.</span><span class="sxs-lookup"><span data-stu-id="fee3a-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="fee3a-119">Dağıtımı otomatik olarak çalıştırmak için aşağıdaki düğmeye tıklayın:</span><span class="sxs-lookup"><span data-stu-id="fee3a-119">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="fee3a-120">[![Azure’a dağıtma](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="fee3a-120">[![Deploy to Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="fee3a-121">Parametreler</span><span class="sxs-lookup"><span data-stu-id="fee3a-121">Parameters</span></span>
<span data-ttu-id="fee3a-122">Azure Resource Manager sayesinde, şablon dağıtıldığında belirtmek istediğiniz değerlerin parametrelerini siz tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="fee3a-122">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="fee3a-123">Şablon tüm parametre değerleri içeren parametre adlı bir bölüm içerir.</span><span class="sxs-lookup"><span data-stu-id="fee3a-123">The template includes a section called Parameters that contains all of the parameter values.</span></span>
<span data-ttu-id="fee3a-124">Dağıtmakta olduğunuz projeye veya dağıtım yaptığınız ortama göre değişen değerler için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fee3a-124">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="fee3a-125">Her zaman aynı kalan değerler için parametre tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="fee3a-125">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="fee3a-126">Her parametre değeri, dağıtılan kaynakları tanımlamak için şablonda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fee3a-126">Each parameter value is used in the template to define the resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="fee3a-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="fee3a-127">redisCacheLocation</span></span>
<span data-ttu-id="fee3a-128">Redis önbelleği konumu.</span><span class="sxs-lookup"><span data-stu-id="fee3a-128">The location of the Redis Cache.</span></span> <span data-ttu-id="fee3a-129">En iyi performans için aynı konuma önbellek ile kullanılmak üzere bir uygulama olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="fee3a-129">For best performance, use the same location as the app to be used with the cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="fee3a-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="fee3a-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="fee3a-131">Tanılama için kullanmak üzere var olan depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="fee3a-131">The name of the existing storage account to use for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="fee3a-132">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="fee3a-132">enableNonSslPort</span></span>
<span data-ttu-id="fee3a-133">SSL olmayan bağlantı noktaları erişimine izin verilip verilmeyeceğini gösteren bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="fee3a-133">A boolean value that indicates whether to allow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="fee3a-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="fee3a-134">diagnosticsStatus</span></span>
<span data-ttu-id="fee3a-135">Tanılama etkin olup olmadığını belirten bir değer.</span><span class="sxs-lookup"><span data-stu-id="fee3a-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="fee3a-136">Kullanım açık veya kapalı.</span><span class="sxs-lookup"><span data-stu-id="fee3a-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="fee3a-137">Dağıtılacak kaynaklar</span><span class="sxs-lookup"><span data-stu-id="fee3a-137">Resources to deploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="fee3a-138">Redis Önbelleği</span><span class="sxs-lookup"><span data-stu-id="fee3a-138">Redis Cache</span></span>
<span data-ttu-id="fee3a-139">Azure Redis önbelleği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fee3a-139">Creates the Azure Redis Cache.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-to-run-deployment"></a><span data-ttu-id="fee3a-140">Dağıtımı çalıştırma komutları</span><span class="sxs-lookup"><span data-stu-id="fee3a-140">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="fee3a-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fee3a-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="fee3a-142">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fee3a-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


