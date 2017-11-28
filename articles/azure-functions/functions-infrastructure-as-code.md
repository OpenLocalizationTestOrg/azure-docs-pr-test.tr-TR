---
title: "Azure işlevlerinde bir işlev uygulaması için kaynak dağıtım otomatikleştirmek | Microsoft Docs"
description: "İşlev uygulamanızı dağıtan bir Azure Resource Manager şablonu oluşturmayı öğrenin."
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
ms.openlocfilehash: 15496e4ab2858b2aa319d53f1c438a259a3d5e49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="99f0e-104">Azure işlevleri işlev uygulamanız için kaynak dağıtımı otomatik hale getir</span><span class="sxs-lookup"><span data-stu-id="99f0e-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="99f0e-105">Bir işlev uygulaması dağıtmak için bir Azure Resource Manager şablonu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99f0e-105">You can use an Azure Resource Manager template to deploy a function app.</span></span> <span data-ttu-id="99f0e-106">Bu makalede gerekli kaynakları ve bunu parametrelerinin özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="99f0e-106">This article outlines the required resources and parameters for doing so.</span></span> <span data-ttu-id="99f0e-107">Bağlı olarak ek kaynaklar dağıtmak gerekebilecek [Tetikleyicileri ve bağlamaları](functions-triggers-bindings.md) işlevi uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="99f0e-107">You might need to deploy additional resources, depending on the [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="99f0e-108">Şablonları oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="99f0e-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="99f0e-109">Örnek şablonları için bkz:</span><span class="sxs-lookup"><span data-stu-id="99f0e-109">For sample templates, see:</span></span>
- <span data-ttu-id="99f0e-110">[işlev uygulaması tüketim plan üzerinde]</span><span class="sxs-lookup"><span data-stu-id="99f0e-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="99f0e-111">[işlev uygulaması Azure uygulama hizmeti plan üzerinde]</span><span class="sxs-lookup"><span data-stu-id="99f0e-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="99f0e-112">Gerekli kaynakları</span><span class="sxs-lookup"><span data-stu-id="99f0e-112">Required resources</span></span>

<span data-ttu-id="99f0e-113">Bir işlev uygulaması bu kaynakları gerektirir:</span><span class="sxs-lookup"><span data-stu-id="99f0e-113">A function app requires these resources:</span></span>

* <span data-ttu-id="99f0e-114">Bir [Azure Storage](../storage/index.md) hesabı</span><span class="sxs-lookup"><span data-stu-id="99f0e-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="99f0e-115">Bir barındırma planı (tüketim planı veya uygulama hizmeti planı)</span><span class="sxs-lookup"><span data-stu-id="99f0e-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="99f0e-116">Bir işlev uygulaması</span><span class="sxs-lookup"><span data-stu-id="99f0e-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="99f0e-117">Depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="99f0e-117">Storage account</span></span>

<span data-ttu-id="99f0e-118">Bir Azure depolama hesabı için bir işlev uygulaması gereklidir.</span><span class="sxs-lookup"><span data-stu-id="99f0e-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="99f0e-119">BLOB'lar, tablolar, kuyruklar ve dosyaları destekleyen bir genel amaçlı hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="99f0e-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="99f0e-120">Daha fazla bilgi için bkz: [Azure işlevleri depolama hesabı gereksinimleri](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="99f0e-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

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

<span data-ttu-id="99f0e-121">Ayrıca, özellikleri `AzureWebJobsStorage` ve `AzureWebJobsDashboard` uygulama ayarları site yapılandırması olarak belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="99f0e-121">In addition, the properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in the site configuration.</span></span> <span data-ttu-id="99f0e-122">Azure işlevleri çalışma zamanı kullanır `AzureWebJobsStorage` iç kuyruk oluşturmak için bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="99f0e-122">The Azure Functions runtime uses the `AzureWebJobsStorage` connection string to create internal queues.</span></span> <span data-ttu-id="99f0e-123">Bağlantı dizesi `AzureWebJobsDashboard` Azure Table depolama ve güç oturum açmak için kullandığınız **İzleyici** portal sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="99f0e-123">The connection string `AzureWebJobsDashboard` is used to log to Azure Table storage and power the **Monitor** tab in the portal.</span></span>

<span data-ttu-id="99f0e-124">Bu özellikleri belirtilen `appSettings` koleksiyonunda `siteConfig` nesnesi:</span><span class="sxs-lookup"><span data-stu-id="99f0e-124">These properties are specified in the `appSettings` collection in the `siteConfig` object:</span></span>

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

### <a name="hosting-plan"></a><span data-ttu-id="99f0e-125">Barındırma planı</span><span class="sxs-lookup"><span data-stu-id="99f0e-125">Hosting plan</span></span>

<span data-ttu-id="99f0e-126">Barındırma planı tanımı, bir tüketim veya uygulama hizmeti planı kullanmadığınıza bağlı olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="99f0e-126">The definition of the hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="99f0e-127">Bkz: [tüketim plan üzerinde bir işlev uygulaması dağıtma](#consumption) ve [uygulama hizmeti plan üzerinde bir işlev uygulaması dağıtma](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="99f0e-127">See [Deploy a function app on the Consumption plan](#consumption) and [Deploy a function app on the App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="99f0e-128">İşlev uygulaması</span><span class="sxs-lookup"><span data-stu-id="99f0e-128">Function app</span></span>

<span data-ttu-id="99f0e-129">Bir kaynak türü kullanarak tanımlı işlevi Uygulama kaynağı **Microsoft.Web/Site** ve tür **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="99f0e-129">The function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

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

## <a name="deploy-a-function-app-on-the-consumption-plan"></a><span data-ttu-id="99f0e-130">Tüketim plan üzerinde bir işlev uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="99f0e-130">Deploy a function app on the Consumption plan</span></span>

<span data-ttu-id="99f0e-131">Bir işlev uygulaması iki farklı modda çalıştırabilirsiniz: Tüketim planlama ve uygulama hizmeti planı.</span><span class="sxs-lookup"><span data-stu-id="99f0e-131">You can run a function app in two different modes: the Consumption plan and the App Service plan.</span></span> <span data-ttu-id="99f0e-132">Kodunuzu çalışıyorsa, çıkışı yükü işlemek için gerekli olan ölçeklendirir ve kod çalışmadığı zaman sonra ölçeklendirir tüketim planı otomatik olarak işlem gücü ayırır.</span><span class="sxs-lookup"><span data-stu-id="99f0e-132">The Consumption plan automatically allocates compute power when your code is running, scales out as necessary to handle load, and then scales down when code is not running.</span></span> <span data-ttu-id="99f0e-133">Bu nedenle, boşta VM'ler için ödeme gerekmez ve yedek kapasite önceden gerekmez.</span><span class="sxs-lookup"><span data-stu-id="99f0e-133">So, you don't have to pay for idle VMs, and you don't have to reserve capacity in advance.</span></span> <span data-ttu-id="99f0e-134">Barındırma planları hakkında daha fazla bilgi için bkz: [Azure işlevleri tüketim ve uygulama hizmeti planları](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="99f0e-134">To learn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="99f0e-135">Örnek Azure Resource Manager şablonu için bkz: [işlev uygulaması tüketim plan üzerinde].</span><span class="sxs-lookup"><span data-stu-id="99f0e-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="99f0e-136">Tüketim planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="99f0e-136">Create a Consumption plan</span></span>

<span data-ttu-id="99f0e-137">Tüketim planı "serverfarm" kaynak özel bir türde değil.</span><span class="sxs-lookup"><span data-stu-id="99f0e-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="99f0e-138">Kullanarak belirttiğiniz `Dynamic` değerini `computeMode` ve `sku` özellikleri:</span><span class="sxs-lookup"><span data-stu-id="99f0e-138">You specify it by using the `Dynamic` value for the `computeMode` and `sku` properties:</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="99f0e-139">İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="99f0e-139">Create a function app</span></span>

<span data-ttu-id="99f0e-140">Ayrıca, site yapılandırması iki ek ayarlar tüketim planı gerektirir: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` ve `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="99f0e-140">In addition, a Consumption plan requires two additional settings in the site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="99f0e-141">Bu özellikler, yapılandırma ve işlev uygulama kodu depolandığı depolama hesabını ve dosya yolu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="99f0e-141">These properties configure the storage account and file path where the function app code and configuration are stored.</span></span>

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

## <a name="deploy-a-function-app-on-the-app-service-plan"></a><span data-ttu-id="99f0e-142">Uygulama hizmeti plan üzerinde bir işlev uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="99f0e-142">Deploy a function app on the App Service plan</span></span>

<span data-ttu-id="99f0e-143">Uygulama hizmeti planında işlevi uygulamanızı temel, standart ve Premium SKU'ları, web uygulamaları için benzer ayrılmış sanal makineler üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="99f0e-143">In the App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar to web apps.</span></span> <span data-ttu-id="99f0e-144">Uygulama hizmeti planı nasıl çalıştığı hakkında daha fazla bilgi için bkz: [Azure App Service planlarına ayrıntılı genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99f0e-144">For details about how the App Service plan works, see the [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="99f0e-145">Örnek Azure Resource Manager şablonu için bkz: [işlev uygulaması Azure uygulama hizmeti plan üzerinde].</span><span class="sxs-lookup"><span data-stu-id="99f0e-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="99f0e-146">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="99f0e-146">Create an App Service plan</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="99f0e-147">İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="99f0e-147">Create a function app</span></span> 

<span data-ttu-id="99f0e-148">Ölçeklendirme seçeneği seçtikten sonra bir işlev uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="99f0e-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="99f0e-149">Uygulama tüm işlevlerinizi tutan bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="99f0e-149">The app is the container that holds all your functions.</span></span>

<span data-ttu-id="99f0e-150">Bir işlev uygulaması, uygulama ayarları ve kaynak denetimi seçenekleri de dahil olmak üzere, dağıtımınızdaki kullanabileceğiniz birçok alt kaynaklara sahip.</span><span class="sxs-lookup"><span data-stu-id="99f0e-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="99f0e-151">Ayrıca kaldırmak isteyebilirsiniz **sourcecontrols** alt kaynak ve farklı bir kullanım [dağıtım seçeneği](functions-continuous-deployment.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="99f0e-151">You also might choose to remove the **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99f0e-152">Azure Kaynak Yöneticisi'ni kullanarak uygulamanızı başarıyla dağıtmak için kaynakları Azure içinde nasıl dağıtıldığını anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="99f0e-152">To successfully deploy your application by using Azure Resource Manager, it's important to understand how resources are deployed in Azure.</span></span> <span data-ttu-id="99f0e-153">Aşağıdaki örnekte, üst düzey yapılandırmaları kullanılarak uygulanır **siteConfig**.</span><span class="sxs-lookup"><span data-stu-id="99f0e-153">In the following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="99f0e-154">İşlevler çalışma zamanı ve dağıtım altyapısı için bilgi iletmek için bir en üst düzeyde bu yapılandırmaları ayarlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="99f0e-154">It's important to set these configurations at a top level, because they convey information to the Functions runtime and deployment engine.</span></span> <span data-ttu-id="99f0e-155">Üst düzey bilgileri önce alt gerekli **sourcecontrols/web** kaynak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="99f0e-155">Top-level information is required before the child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="99f0e-156">Bu ayarları alt düzey yapılandırmanız mümkün olsa **config/appSettings** işlevi uygulamanızı dağıtılmalıdır bazı durumlarda kaynak *önce* **config/appSettings** uygulanır.</span><span class="sxs-lookup"><span data-stu-id="99f0e-156">Although it's possible to configure these settings in the child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="99f0e-157">Örneğin, kullanırken işlevleriyle [Logic Apps](../logic-apps/index.md), başka bir kaynak bağımlılığı, işlevlerdir.</span><span class="sxs-lookup"><span data-stu-id="99f0e-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

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
> <span data-ttu-id="99f0e-158">Bu şablonu kullanan [proje](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) işlevleri dağıtım altyapısı (Kudu) için dağıtılabilir kod arar temel dizin ayarlar uygulama ayarları değeri.</span><span class="sxs-lookup"><span data-stu-id="99f0e-158">This template uses the [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets the base directory in which the Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="99f0e-159">Bizim deposunda bizim bir alt klasöründe işlevlerdir **src** klasör.</span><span class="sxs-lookup"><span data-stu-id="99f0e-159">In our repository, our functions are in a subfolder of the **src** folder.</span></span> <span data-ttu-id="99f0e-160">Bu nedenle, önceki örnekte, uygulama ayarlarını değeri ayarlarız `src`.</span><span class="sxs-lookup"><span data-stu-id="99f0e-160">So, in the preceding example, we set the app settings value to `src`.</span></span> <span data-ttu-id="99f0e-161">İşlevlerinizi deponuz kök dizininde ise ya da kaynak denetiminden dağıtıyorsanız değil, bu uygulama ayarları değeri kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99f0e-161">If your functions are in the root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="99f0e-162">Şablonunuzu dağıtma</span><span class="sxs-lookup"><span data-stu-id="99f0e-162">Deploy your template</span></span>

<span data-ttu-id="99f0e-163">Şablonunuzu dağıtmak için aşağıdaki yöntemleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="99f0e-163">You can use any of the following ways to deploy your template:</span></span>

* [<span data-ttu-id="99f0e-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="99f0e-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="99f0e-165">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="99f0e-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="99f0e-166">Azure portal</span><span class="sxs-lookup"><span data-stu-id="99f0e-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="99f0e-167">REST API</span><span class="sxs-lookup"><span data-stu-id="99f0e-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-to-azure-button"></a><span data-ttu-id="99f0e-168">Azure düğmesine dağıtma</span><span class="sxs-lookup"><span data-stu-id="99f0e-168">Deploy to Azure button</span></span>

<span data-ttu-id="99f0e-169">Değiştir ```<url-encoded-path-to-azuredeploy-json>``` ile bir [URL kodlanmış](https://www.bing.com/search?q=url+encode) ham yolunu sürümü, `azuredeploy.json` GitHub dosyasında.</span><span class="sxs-lookup"><span data-stu-id="99f0e-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of the raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="99f0e-170">Markdown kullanan örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="99f0e-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="99f0e-171">HTML kullanan örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="99f0e-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="99f0e-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99f0e-172">Next steps</span></span>

<span data-ttu-id="99f0e-173">Geliştirme ve Azure işlevleri yapılandırma hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="99f0e-173">Learn more about how to develop and configure Azure Functions.</span></span>

* [<span data-ttu-id="99f0e-174">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="99f0e-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="99f0e-175">Azure işlevi uygulama ayarlarının nasıl yapılandırılacağı</span><span class="sxs-lookup"><span data-stu-id="99f0e-175">How to configure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="99f0e-176">İlk Azure işlevinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="99f0e-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[işlev uygulaması tüketim plan üzerinde]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[işlev uygulaması Azure uygulama hizmeti plan üzerinde]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
