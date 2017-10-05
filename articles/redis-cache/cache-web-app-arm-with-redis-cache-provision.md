---
title: "Redis önbelleği ile Web uygulaması sağla"
description: "Redis önbelleği ile web uygulaması dağıtmak için Azure Resource Manager şablonunu kullanın."
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
ms.openlocfilehash: 810c1cedd4fe0bd6ecdf9bd32dfb241f5f345300
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="736b0-103">Bir Web uygulaması artı bir şablon kullanarak Redis önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="736b0-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="736b0-104">Bu konuda, Azure Web uygulaması Redis önbelleği ile dağıtan bir Azure Resource Manager şablonunun nasıl oluşturulacağını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="736b0-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="736b0-105">Nasıl tanımlamak için hangi kaynağın dağıtılan ve ne zaman dağıtım yürütülen parametreler tanımlamak nasıl belirtilen öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="736b0-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="736b0-106">Bu şablonu kendi dağıtımlarınız için kullanabilir veya kendi gereksinimlerinize göre özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="736b0-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="736b0-107">Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="736b0-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="736b0-108">Tam şablon için bkz: [Web uygulamasını Redis önbelleği şablonuyla](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="736b0-108">For the complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="736b0-109">Dağıtmak</span><span class="sxs-lookup"><span data-stu-id="736b0-109">What you will deploy</span></span>
<span data-ttu-id="736b0-110">Bu şablon, dağıtacağınız:</span><span class="sxs-lookup"><span data-stu-id="736b0-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="736b0-111">Azure Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="736b0-111">Azure Web App</span></span>
* <span data-ttu-id="736b0-112">Azure Redis önbelleği.</span><span class="sxs-lookup"><span data-stu-id="736b0-112">Azure Redis Cache.</span></span>

<span data-ttu-id="736b0-113">Dağıtımı otomatik olarak çalıştırmak için aşağıdaki düğmeye tıklayın:</span><span class="sxs-lookup"><span data-stu-id="736b0-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="736b0-114">[![Azure’a dağıtma](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="736b0-114">[![Deploy to Azure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-to-specify"></a><span data-ttu-id="736b0-115">Belirtmek üzere Parametreler</span><span class="sxs-lookup"><span data-stu-id="736b0-115">Parameters to specify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="736b0-116">Adları için değişkenleri</span><span class="sxs-lookup"><span data-stu-id="736b0-116">Variables for names</span></span>
<span data-ttu-id="736b0-117">Bu şablon değişkenleri kaynakların adları oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="736b0-117">This template uses variables to construct names for the resources.</span></span> <span data-ttu-id="736b0-118">Kullandığı [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) işlevi bir değer oluşturmak için temel kaynak grubunun kimliği.</span><span class="sxs-lookup"><span data-stu-id="736b0-118">It uses the [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function to construct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-to-deploy"></a><span data-ttu-id="736b0-119">Dağıtılacak kaynaklar</span><span class="sxs-lookup"><span data-stu-id="736b0-119">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="736b0-120">Redis Önbelleği</span><span class="sxs-lookup"><span data-stu-id="736b0-120">Redis Cache</span></span>
<span data-ttu-id="736b0-121">Web uygulaması ile kullanılan Azure Redis önbelleği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="736b0-121">Creates the Azure Redis Cache that is used with the web app.</span></span> <span data-ttu-id="736b0-122">İçinde belirtilen önbellek adı **cacheName** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="736b0-122">The name of the cache is specified in the **cacheName** variable.</span></span>

<span data-ttu-id="736b0-123">Şablon Önbelleği kaynak grubu ile aynı konumda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="736b0-123">The template creates the cache in the same location as the resource group.</span></span>

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


### <a name="web-app"></a><span data-ttu-id="736b0-124">Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="736b0-124">Web app</span></span>
<span data-ttu-id="736b0-125">Belirtilen ada sahip web uygulamasını oluşturur **webSiteName** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="736b0-125">Creates the web app with name specified in the **webSiteName** variable.</span></span>

<span data-ttu-id="736b0-126">Web uygulamasını Redis önbelleği ile çalışacak şekilde etkinleştirmek uygulama ayarı özellikleri ile yapılandırıldığını dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="736b0-126">Notice that the web app is configured with app setting properties that enable it to work with the Redis Cache.</span></span> <span data-ttu-id="736b0-127">Ayarları dinamik olarak oluşturulan bu uygulama dağıtımı sırasında sağlanan değerlere göre.</span><span class="sxs-lookup"><span data-stu-id="736b0-127">This app settings are dynamically created based on values provided during deployment.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="736b0-128">Dağıtımı çalıştırma komutları</span><span class="sxs-lookup"><span data-stu-id="736b0-128">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="736b0-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="736b0-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="736b0-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="736b0-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
