---
title: "aaaProvision Redis önbelleği ile Web uygulaması"
description: "Azure Resource Manager şablonu toodeploy web uygulamasını Redis önbelleği ile kullanın."
services: app-service
documentationcenter: 
author: steved0x
manager: erickson-doug
editor: 
ms.assetid: 6e99c71f-ef8e-4570-a307-e4c059e60c35
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: b95b5e230dc40c1157940c2017cba836975b6930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="6d1bf-103">Bir Web uygulaması artı bir şablon kullanarak Redis önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d1bf-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="6d1bf-104">Bu konuda, öğreneceksiniz nasıl toocreate Redis önbelleği ile Azure Web uygulaması dağıtan bir Azure Resource Manager şablonu.</span><span class="sxs-lookup"><span data-stu-id="6d1bf-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="6d1bf-105">Şunları öğreneceksiniz nasıl toodefine hangi kaynağın dağıtılan ve nasıl toodefine parametreler hello dağıtım zaman yürütülür belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="6d1bf-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="6d1bf-106">Kendi dağıtımlar için bu şablonu kullanabilir veya toomeet özelleştirebilirsiniz gereksinimlerinizi.</span><span class="sxs-lookup"><span data-stu-id="6d1bf-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="6d1bf-107">Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6d1bf-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="6d1bf-108">Merhaba tam şablonu için bkz: [Web uygulamasını Redis önbelleği şablonuyla](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="6d1bf-108">For hello complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="6d1bf-109">Dağıtmak</span><span class="sxs-lookup"><span data-stu-id="6d1bf-109">What you will deploy</span></span>
<span data-ttu-id="6d1bf-110">Bu şablon, dağıtacağınız:</span><span class="sxs-lookup"><span data-stu-id="6d1bf-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="6d1bf-111">Azure Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="6d1bf-111">Azure Web App</span></span>
* <span data-ttu-id="6d1bf-112">Azure Redis önbelleği.</span><span class="sxs-lookup"><span data-stu-id="6d1bf-112">Azure Redis Cache.</span></span>

<span data-ttu-id="6d1bf-113">toorun dağıtım otomatik olarak Merhaba, düğme aşağıdaki hello tıklatın:</span><span class="sxs-lookup"><span data-stu-id="6d1bf-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="6d1bf-114">[![TooAzure dağıtma](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="6d1bf-114">[![Deploy tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-toospecify"></a><span data-ttu-id="6d1bf-115">Parametreleri toospecify</span><span class="sxs-lookup"><span data-stu-id="6d1bf-115">Parameters toospecify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="6d1bf-116">Adları için değişkenleri</span><span class="sxs-lookup"><span data-stu-id="6d1bf-116">Variables for names</span></span>
<span data-ttu-id="6d1bf-117">Bu şablon hello kaynaklar için değişkenleri tooconstruct adlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="6d1bf-117">This template uses variables tooconstruct names for hello resources.</span></span> <span data-ttu-id="6d1bf-118">Merhaba kullanan [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) bir değer kaynağı Grup kimliğine göre tooconstruct işlev.</span><span class="sxs-lookup"><span data-stu-id="6d1bf-118">It uses hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function tooconstruct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-toodeploy"></a><span data-ttu-id="6d1bf-119">Kaynakları toodeploy</span><span class="sxs-lookup"><span data-stu-id="6d1bf-119">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="6d1bf-120">Redis Önbelleği</span><span class="sxs-lookup"><span data-stu-id="6d1bf-120">Redis Cache</span></span>
<span data-ttu-id="6d1bf-121">Hello Azure Redis önbelleği hello web uygulaması ile kullanılan oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d1bf-121">Creates hello Azure Redis Cache that is used with hello web app.</span></span> <span data-ttu-id="6d1bf-122">hello belirtilen hello önbellek Hello adı **cacheName** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="6d1bf-122">hello name of hello cache is specified in hello **cacheName** variable.</span></span>

<span data-ttu-id="6d1bf-123">Merhaba şablon oluşturur hello önbellek hello hello kaynak grubu olarak aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="6d1bf-123">hello template creates hello cache in hello same location as hello resource group.</span></span>

    {
      "name": "[variables('cacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[resourceGroup().location]",
      "apiVersion": "2015-08-01",
      "dependsOn": [ ],
      "tags": {
        "displayName": "cache"
      },
      "properties": {
        "sku": {
          "name": "[parameters('cacheSKUName')]",
          "family": "[parameters('cacheSKUFamily')]",
          "capacity": "[parameters('cacheSKUCapacity')]"
        }
      }
    }


### <a name="web-app"></a><span data-ttu-id="6d1bf-124">Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="6d1bf-124">Web app</span></span>
<span data-ttu-id="6d1bf-125">Hello belirtilen adla Hello web uygulamasını oluşturur **webSiteName** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="6d1bf-125">Creates hello web app with name specified in hello **webSiteName** variable.</span></span>

<span data-ttu-id="6d1bf-126">Bu başlangıç web uygulaması toowork hello Redis önbelleği ile etkinleştirmek özelliklerini ayarlama uygulama ile yapılandırılmış dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6d1bf-126">Notice that hello web app is configured with app setting properties that enable it toowork with hello Redis Cache.</span></span> <span data-ttu-id="6d1bf-127">Ayarları dinamik olarak oluşturulan bu uygulama dağıtımı sırasında sağlanan değerlere göre.</span><span class="sxs-lookup"><span data-stu-id="6d1bf-127">This app settings are dynamically created based on values provided during deployment.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Web/serverFarms/', variables('hostingPlanName'))]",
        "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "appsettings",
          "dependsOn": [
            "[concat('Microsoft.Web/Sites/', variables('webSiteName'))]",
            "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
          ],
          "properties": {
            "CacheConnection": "[concat(variables('cacheName'),'.redis.cache.windows.net,abortConnect=false,ssl=true,password=', listKeys(resourceId('Microsoft.Cache/Redis', variables('cacheName')), '2015-08-01').primaryKey)]"
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a><span data-ttu-id="6d1bf-128">Komutları toorun dağıtımı</span><span class="sxs-lookup"><span data-stu-id="6d1bf-128">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="6d1bf-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d1bf-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="6d1bf-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6d1bf-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
