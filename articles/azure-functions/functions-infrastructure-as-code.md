---
title: "Azure işlevleri bir işlev uygulaması aaaAutomate kaynak dağıtım | Microsoft Docs"
description: "Bilgi nasıl toobuild işlevi uygulamanızı dağıtan bir Azure Resource Manager şablonu."
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, sunucusuz mimarisi, kod, azure kaynak yöneticisi olarak altyapısı"
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="5c301-104">Azure işlevleri işlev uygulamanız için kaynak dağıtımı otomatik hale getir</span><span class="sxs-lookup"><span data-stu-id="5c301-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="5c301-105">Azure Resource Manager şablonu toodeploy bir işlev uygulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c301-105">You can use an Azure Resource Manager template toodeploy a function app.</span></span> <span data-ttu-id="5c301-106">Bu makalede hello gerekli kaynakları ve bunu parametrelerinin özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="5c301-106">This article outlines hello required resources and parameters for doing so.</span></span> <span data-ttu-id="5c301-107">Merhaba bağlı olarak toodeploy ek kaynaklar gerekebilecek [Tetikleyicileri ve bağlamaları](functions-triggers-bindings.md) işlevi uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="5c301-107">You might need toodeploy additional resources, depending on hello [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="5c301-108">Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5c301-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="5c301-109">Örnek şablonları için bkz:</span><span class="sxs-lookup"><span data-stu-id="5c301-109">For sample templates, see:</span></span>
- <span data-ttu-id="5c301-110">[işlev uygulaması tüketim plan üzerinde]</span><span class="sxs-lookup"><span data-stu-id="5c301-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="5c301-111">[işlev uygulaması Azure uygulama hizmeti plan üzerinde]</span><span class="sxs-lookup"><span data-stu-id="5c301-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="5c301-112">Gerekli kaynakları</span><span class="sxs-lookup"><span data-stu-id="5c301-112">Required resources</span></span>

<span data-ttu-id="5c301-113">Bir işlev uygulaması bu kaynakları gerektirir:</span><span class="sxs-lookup"><span data-stu-id="5c301-113">A function app requires these resources:</span></span>

* <span data-ttu-id="5c301-114">Bir [Azure Storage](../storage/index.md) hesabı</span><span class="sxs-lookup"><span data-stu-id="5c301-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="5c301-115">Bir barındırma planı (tüketim planı veya uygulama hizmeti planı)</span><span class="sxs-lookup"><span data-stu-id="5c301-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="5c301-116">Bir işlev uygulaması</span><span class="sxs-lookup"><span data-stu-id="5c301-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="5c301-117">Depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="5c301-117">Storage account</span></span>

<span data-ttu-id="5c301-118">Bir Azure depolama hesabı için bir işlev uygulaması gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5c301-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="5c301-119">BLOB'lar, tablolar, kuyruklar ve dosyaları destekleyen bir genel amaçlı hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c301-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="5c301-120">Daha fazla bilgi için bkz: [Azure işlevleri depolama hesabı gereksinimleri](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="5c301-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

<span data-ttu-id="5c301-121">Ayrıca, Özellikler hello `AzureWebJobsStorage` ve `AzureWebJobsDashboard` uygulama ayarları hello site yapılandırması olarak belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="5c301-121">In addition, hello properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in hello site configuration.</span></span> <span data-ttu-id="5c301-122">Hello Azure işlevleri çalışma zamanı kullanan hello `AzureWebJobsStorage` bağlantı dizesi toocreate iç sıralar.</span><span class="sxs-lookup"><span data-stu-id="5c301-122">hello Azure Functions runtime uses hello `AzureWebJobsStorage` connection string toocreate internal queues.</span></span> <span data-ttu-id="5c301-123">Hello bağlantı dizesi `AzureWebJobsDashboard` kullanılan toolog, tooAzure tablo depolama ve güç hello olan **İzleyici** hello portal sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="5c301-123">hello connection string `AzureWebJobsDashboard` is used toolog tooAzure Table storage and power hello **Monitor** tab in hello portal.</span></span>

<span data-ttu-id="5c301-124">Bu özellikleri hello belirtilen `appSettings` hello koleksiyonda `siteConfig` nesnesi:</span><span class="sxs-lookup"><span data-stu-id="5c301-124">These properties are specified in hello `appSettings` collection in hello `siteConfig` object:</span></span>

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a><span data-ttu-id="5c301-125">Barındırma planı</span><span class="sxs-lookup"><span data-stu-id="5c301-125">Hosting plan</span></span>

<span data-ttu-id="5c301-126">barındırma planı hello Hello tanımı, bir tüketim veya uygulama hizmeti planı kullanmadığınıza bağlı olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="5c301-126">hello definition of hello hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="5c301-127">Bkz: [hello tüketim plan üzerinde bir işlev uygulaması dağıtma](#consumption) ve [hello uygulama hizmeti planı üzerinde bir işlev uygulaması dağıtma](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="5c301-127">See [Deploy a function app on hello Consumption plan](#consumption) and [Deploy a function app on hello App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="5c301-128">İşlev uygulaması</span><span class="sxs-lookup"><span data-stu-id="5c301-128">Function app</span></span>

<span data-ttu-id="5c301-129">Merhaba işlevi uygulama kaynak türünde bir kaynak kullanılarak tanımlanmış **Microsoft.Web/Site** ve tür **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="5c301-129">hello function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a><span data-ttu-id="5c301-130">Merhaba tüketim plan üzerinde bir işlev uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="5c301-130">Deploy a function app on hello Consumption plan</span></span>

<span data-ttu-id="5c301-131">Bir işlev uygulaması iki farklı modda çalıştırabilirsiniz: Tüketim planlama ve uygulama hizmeti planı hello hello.</span><span class="sxs-lookup"><span data-stu-id="5c301-131">You can run a function app in two different modes: hello Consumption plan and hello App Service plan.</span></span> <span data-ttu-id="5c301-132">kodunuzu çalışıyorsa, çıkışı gerekli toohandle yükü olarak ölçeklendirir ve kod çalışmadığı zaman sonra ölçeklendirir hello tüketim planı otomatik olarak işlem gücü ayırır.</span><span class="sxs-lookup"><span data-stu-id="5c301-132">hello Consumption plan automatically allocates compute power when your code is running, scales out as necessary toohandle load, and then scales down when code is not running.</span></span> <span data-ttu-id="5c301-133">Bu nedenle, boşta VM'ler için toopay yok ve önceden tooreserve kapasitesine sahip değilseniz.</span><span class="sxs-lookup"><span data-stu-id="5c301-133">So, you don't have toopay for idle VMs, and you don't have tooreserve capacity in advance.</span></span> <span data-ttu-id="5c301-134">barındırma planları, hakkında daha fazla toolearn bkz [Azure işlevleri tüketim ve uygulama hizmeti planları](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="5c301-134">toolearn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="5c301-135">Örnek Azure Resource Manager şablonu için bkz: [işlev uygulaması tüketim plan üzerinde].</span><span class="sxs-lookup"><span data-stu-id="5c301-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="5c301-136">Tüketim planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c301-136">Create a Consumption plan</span></span>

<span data-ttu-id="5c301-137">Tüketim planı "serverfarm" kaynak özel bir türde değil.</span><span class="sxs-lookup"><span data-stu-id="5c301-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="5c301-138">Hello kullanarak belirtin `Dynamic` hello için değer `computeMode` ve `sku` özellikleri:</span><span class="sxs-lookup"><span data-stu-id="5c301-138">You specify it by using hello `Dynamic` value for hello `computeMode` and `sku` properties:</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="5c301-139">İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c301-139">Create a function app</span></span>

<span data-ttu-id="5c301-140">Ayrıca, bir tüketim planı hello site yapılandırması iki ek ayarlar gerektirir: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` ve `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="5c301-140">In addition, a Consumption plan requires two additional settings in hello site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="5c301-141">Bu özellikleri hello işlevi uygulama kodu ve yapılandırma depolandığı hello depolama hesabı ve dosya yolu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5c301-141">These properties configure hello storage account and file path where hello function app code and configuration are stored.</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a><span data-ttu-id="5c301-142">Merhaba uygulama hizmeti planı üzerinde bir işlev uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="5c301-142">Deploy a function app on hello App Service plan</span></span>

<span data-ttu-id="5c301-143">Hello uygulama hizmeti planı, temel, standart ve Premium SKU'ları benzer tooweb uygulamalarını özel VM'ler işlevi uygulamanızı çalışır.</span><span class="sxs-lookup"><span data-stu-id="5c301-143">In hello App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar tooweb apps.</span></span> <span data-ttu-id="5c301-144">Merhaba hello uygulama hizmeti planı nasıl çalıştığı hakkında daha fazla bilgi için bkz [Azure App Service planlarına ayrıntılı genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c301-144">For details about how hello App Service plan works, see hello [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="5c301-145">Örnek Azure Resource Manager şablonu için bkz: [işlev uygulaması Azure uygulama hizmeti plan üzerinde].</span><span class="sxs-lookup"><span data-stu-id="5c301-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="5c301-146">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c301-146">Create an App Service plan</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="5c301-147">İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c301-147">Create a function app</span></span> 

<span data-ttu-id="5c301-148">Ölçeklendirme seçeneği seçtikten sonra bir işlev uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5c301-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="5c301-149">Merhaba uygulama tüm işlevlerinizi tutan hello kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="5c301-149">hello app is hello container that holds all your functions.</span></span>

<span data-ttu-id="5c301-150">Bir işlev uygulaması, uygulama ayarları ve kaynak denetimi seçenekleri de dahil olmak üzere, dağıtımınızdaki kullanabileceğiniz birçok alt kaynaklara sahip.</span><span class="sxs-lookup"><span data-stu-id="5c301-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="5c301-151">Tooremove hello tercih edebilirsiniz **sourcecontrols** alt kaynak ve farklı bir kullanım [dağıtım seçeneği](functions-continuous-deployment.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="5c301-151">You also might choose tooremove hello **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c301-152">toosuccessfully Azure Kaynak Yöneticisi'ni kullanarak uygulamanızı dağıtmak, kaynakları Azure içinde nasıl dağıtıldığını önemli toounderstand.</span><span class="sxs-lookup"><span data-stu-id="5c301-152">toosuccessfully deploy your application by using Azure Resource Manager, it's important toounderstand how resources are deployed in Azure.</span></span> <span data-ttu-id="5c301-153">Aşağıdaki örneğine hello kullanarak üst düzey yapılandırmaları uygulanan **siteConfig**.</span><span class="sxs-lookup"><span data-stu-id="5c301-153">In hello following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="5c301-154">Çalışma zamanı ve dağıtım bilgileri toohello işlevleri altyapısı iletmek Bu yapılandırmalar bir üst düzey, önemli tooset demektir.</span><span class="sxs-lookup"><span data-stu-id="5c301-154">It's important tooset these configurations at a top level, because they convey information toohello Functions runtime and deployment engine.</span></span> <span data-ttu-id="5c301-155">Üst düzey bilgileri hello alt önce gerekli **sourcecontrols/web** kaynak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="5c301-155">Top-level information is required before hello child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="5c301-156">Olası tooconfigure olmasına rağmen bu ayarları alt düzey hello **config/appSettings** işlevi uygulamanızı dağıtılmalıdır bazı durumlarda kaynak *önce* **config/appSettings**  uygulanır.</span><span class="sxs-lookup"><span data-stu-id="5c301-156">Although it's possible tooconfigure these settings in hello child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="5c301-157">Örneğin, kullanırken işlevleriyle [Logic Apps](../logic-apps/index.md), başka bir kaynak bağımlılığı, işlevlerdir.</span><span class="sxs-lookup"><span data-stu-id="5c301-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> <span data-ttu-id="5c301-158">Bu şablon hello kullanır [proje](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) hello temel dizin hangi hello işlevleri dağıtım altyapısı (Kudu) görünüyor için dağıtılabilir kod ayarlar uygulama ayarları değeri.</span><span class="sxs-lookup"><span data-stu-id="5c301-158">This template uses hello [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets hello base directory in which hello Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="5c301-159">Bizim deposunda bizim hello bir alt klasörü işlevlerdir **src** klasör.</span><span class="sxs-lookup"><span data-stu-id="5c301-159">In our repository, our functions are in a subfolder of hello **src** folder.</span></span> <span data-ttu-id="5c301-160">Bu nedenle, örnek önceki hello hello uygulama ayarları değeri çok ayarlarız`src`.</span><span class="sxs-lookup"><span data-stu-id="5c301-160">So, in hello preceding example, we set hello app settings value too`src`.</span></span> <span data-ttu-id="5c301-161">İşlevlerinizi deponuz hello kök dizininde ise ya da kaynak denetiminden dağıtıyorsanız değil, bu uygulama ayarları değeri kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c301-161">If your functions are in hello root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="5c301-162">Şablonunuzu dağıtma</span><span class="sxs-lookup"><span data-stu-id="5c301-162">Deploy your template</span></span>

<span data-ttu-id="5c301-163">Aşağıdaki yolları toodeploy hello şablonunuzu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5c301-163">You can use any of hello following ways toodeploy your template:</span></span>

* [<span data-ttu-id="5c301-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c301-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="5c301-165">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5c301-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="5c301-166">Azure portal</span><span class="sxs-lookup"><span data-stu-id="5c301-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="5c301-167">REST API</span><span class="sxs-lookup"><span data-stu-id="5c301-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a><span data-ttu-id="5c301-168">Dağıt tooAzure düğmesi</span><span class="sxs-lookup"><span data-stu-id="5c301-168">Deploy tooAzure button</span></span>

<span data-ttu-id="5c301-169">Değiştir ```<url-encoded-path-to-azuredeploy-json>``` ile bir [URL kodlanmış](https://www.bing.com/search?q=url+encode) hello ham yolunu sürümü, `azuredeploy.json` GitHub dosyasında.</span><span class="sxs-lookup"><span data-stu-id="5c301-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of hello raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="5c301-170">Markdown kullanan örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5c301-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="5c301-171">HTML kullanan örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5c301-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="5c301-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5c301-172">Next steps</span></span>

<span data-ttu-id="5c301-173">Hakkında daha fazla bilgi toodevelop ve Azure işlevleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5c301-173">Learn more about how toodevelop and configure Azure Functions.</span></span>

* [<span data-ttu-id="5c301-174">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="5c301-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="5c301-175">Nasıl tooconfigure Azure işlev uygulama ayarları</span><span class="sxs-lookup"><span data-stu-id="5c301-175">How tooconfigure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="5c301-176">İlk Azure işlevinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c301-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[işlev uygulaması tüketim plan üzerinde]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[işlev uygulaması Azure uygulama hizmeti plan üzerinde]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
