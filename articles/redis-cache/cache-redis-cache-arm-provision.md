---
title: "Azure Resource Manager kullanarak bir Redis önbelleği aaaProvision | Microsoft Docs"
description: "Azure Resource Manager şablonu toodeploy bir Azure Redis önbelleği kullanın."
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
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="ca461-103">Şablon kullanarak Redis Önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca461-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="ca461-104">Bu konuda, bilgi toocreate bir Azure Resource Manager şablonu dağıtan nasıl bir Azure Redis önbelleği.</span><span class="sxs-lookup"><span data-stu-id="ca461-104">In this topic, you learn how toocreate an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="ca461-105">Merhaba önbelleği bir var olan depolama hesabı tookeep Tanılama verileri ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca461-105">hello cache can be used with an existing storage account tookeep diagnostic data.</span></span> <span data-ttu-id="ca461-106">Da bilgi nasıl toodefine hangi kaynağın dağıtılan ve nasıl toodefine parametreler hello dağıtım zaman yürütülür belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="ca461-106">You also learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="ca461-107">Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="ca461-107">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="ca461-108">Şu anda tanılama ayarları için tüm önbellekleri hello paylaşılan aynı bölge için bir abonelik.</span><span class="sxs-lookup"><span data-stu-id="ca461-108">Currently, diagnostic settings are shared for all caches in hello same region for a subscription.</span></span> <span data-ttu-id="ca461-109">Merhaba bölgede bulunan bir önbellek güncelleştirme hello bölgedeki tüm diğer önbellekleri etkiler.</span><span class="sxs-lookup"><span data-stu-id="ca461-109">Updating one cache in hello region affects all other caches in hello region.</span></span>

<span data-ttu-id="ca461-110">Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ca461-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="ca461-111">Merhaba tam şablonu için bkz: [Redis önbelleği şablon](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="ca461-111">For hello complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="ca461-112">Resource Manager şablonları hello yeni için [Premium katmanı](cache-premium-tier-intro.md) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca461-112">Resource Manager templates for hello new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="ca461-113">Kümeleme Premium Redis önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca461-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="ca461-114">Premium Redis önbelleği ile veri kalıcılığını oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca461-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="ca461-115">VNet ve isteğe bağlı kümeleme Premium Redis önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca461-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="ca461-116">toocheck hello son şablonları için bkz: [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/) arayın ve `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="ca461-116">toocheck for hello latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="ca461-117">Dağıtmak</span><span class="sxs-lookup"><span data-stu-id="ca461-117">What you will deploy</span></span>
<span data-ttu-id="ca461-118">Bu şablonda bir Azure Redis Tanılama verileri için mevcut bir depolama hesabını kullanan önbelleği dağıtır.</span><span class="sxs-lookup"><span data-stu-id="ca461-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="ca461-119">toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:</span><span class="sxs-lookup"><span data-stu-id="ca461-119">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="ca461-120">[![TooAzure dağıtma](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="ca461-120">[![Deploy tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="ca461-121">Parametreler</span><span class="sxs-lookup"><span data-stu-id="ca461-121">Parameters</span></span>
<span data-ttu-id="ca461-122">Azure Resource Manager ile tanımladığınız parametreler için değerler hello şablon dağıtıldığında toospecify istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="ca461-122">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="ca461-123">Merhaba şablonu tüm hello parametre değerlerini içeren parametreleri adlı bir bölüm içerir.</span><span class="sxs-lookup"><span data-stu-id="ca461-123">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="ca461-124">Dağıttığınız hello projesini temel alan veya dağıttığınız hello ortamı dayanarak farklılık bu değerleri için bir parametre tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca461-124">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="ca461-125">Her zaman kalın değerleri aynı hello için parametreleri tanımlamayın.</span><span class="sxs-lookup"><span data-stu-id="ca461-125">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="ca461-126">Her parametre değeri dağıtılan hello şablonu toodefine hello kaynaklarında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ca461-126">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="ca461-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="ca461-127">redisCacheLocation</span></span>
<span data-ttu-id="ca461-128">Merhaba Redis önbelleği başlangıç konumu.</span><span class="sxs-lookup"><span data-stu-id="ca461-128">hello location of hello Redis Cache.</span></span> <span data-ttu-id="ca461-129">En iyi performans için kullanım hello aynı hello önbelleği ile kullanılan uygulama toobe hello gibi konumu.</span><span class="sxs-lookup"><span data-stu-id="ca461-129">For best performance, use hello same location as hello app toobe used with hello cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="ca461-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="ca461-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="ca461-131">Tanılama hello varolan depolama hesabı toouse adı Hello.</span><span class="sxs-lookup"><span data-stu-id="ca461-131">hello name of hello existing storage account toouse for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="ca461-132">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="ca461-132">enableNonSslPort</span></span>
<span data-ttu-id="ca461-133">Gösteren bir Boole değeri tooallow SSL olmayan bağlantı noktaları erişim olup olmadığını.</span><span class="sxs-lookup"><span data-stu-id="ca461-133">A boolean value that indicates whether tooallow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="ca461-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="ca461-134">diagnosticsStatus</span></span>
<span data-ttu-id="ca461-135">Tanılama etkin olup olmadığını belirten bir değer.</span><span class="sxs-lookup"><span data-stu-id="ca461-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="ca461-136">Kullanım açık veya kapalı.</span><span class="sxs-lookup"><span data-stu-id="ca461-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="ca461-137">Kaynakları toodeploy</span><span class="sxs-lookup"><span data-stu-id="ca461-137">Resources toodeploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="ca461-138">Redis Önbelleği</span><span class="sxs-lookup"><span data-stu-id="ca461-138">Redis Cache</span></span>
<span data-ttu-id="ca461-139">Hello Azure Redis önbelleği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ca461-139">Creates hello Azure Redis Cache.</span></span>

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



## <a name="commands-toorun-deployment"></a><span data-ttu-id="ca461-140">Komutları toorun dağıtımı</span><span class="sxs-lookup"><span data-stu-id="ca461-140">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="ca461-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca461-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="ca461-142">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ca461-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


