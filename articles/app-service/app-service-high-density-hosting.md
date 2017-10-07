---
title: "Azure uygulama hizmeti yoğunluğu aaaHigh barındırma | Microsoft Docs"
description: "Azure uygulama hizmeti üzerinde yüksek yoğunluklu barındırma"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: a903cb78-4927-47b0-8427-56412c4e3e64
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: byvinyal
ms.openlocfilehash: a10cb81ace13ba6992b572a44361061ecf72b266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="6b64a-103">Azure uygulama hizmeti üzerinde yüksek yoğunluklu barındırma</span><span class="sxs-lookup"><span data-stu-id="6b64a-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="6b64a-104">Uygulama hizmeti kullanırken, uygulamanız tarafından iki kavramları tooit ayrılan hello kapasiteden ayrılmış:</span><span class="sxs-lookup"><span data-stu-id="6b64a-104">When using App Service, your application is decoupled from hello capacity allocated tooit by two concepts:</span></span>

* <span data-ttu-id="6b64a-105">**Merhaba uygulama:** hello uygulama ve çalışma zamanı yapılandırmasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="6b64a-105">**hello Application:** Represents hello app and its runtime configuration.</span></span> <span data-ttu-id="6b64a-106">Örneğin, hello içeren çalışma zamanı hello .NET sürümü yükü hello uygulaması ayarları.</span><span class="sxs-lookup"><span data-stu-id="6b64a-106">For example, it includes hello version of .NET that hello runtime should load, hello app settings.</span></span>
* <span data-ttu-id="6b64a-107">**Merhaba App Service planı:** hello hello kapasite, kullanılabilir özellik kümesini ve yere göre hello uygulamasının özelliklerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6b64a-107">**hello App Service Plan:** Defines hello characteristics of hello capacity, available feature set, and locality of hello application.</span></span> <span data-ttu-id="6b64a-108">Örneğin, özellikleri büyük (dört çekirdek) makine, dört örnekleri, Doğu ABD Premium özellikleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="6b64a-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="6b64a-109">Bir uygulama her zaman bağlı tooan uygulama hizmeti planı'dır, ancak bir uygulama hizmeti planı kapasite tooone ya da daha fazla uygulama sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="6b64a-109">An app is always linked tooan App Service plan, but an App Service plan can provide capacity tooone or more apps.</span></span>

<span data-ttu-id="6b64a-110">Sonuç olarak, hello platform hello esneklik tooisolate tek bir uygulamayı sağlar veya bir uygulama hizmeti planı paylaşarak kaynakları paylaşan birden çok uygulamalara sahip.</span><span class="sxs-lookup"><span data-stu-id="6b64a-110">As a result, hello platform provides hello flexibility tooisolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="6b64a-111">Ancak, birden fazla uygulama bir uygulama hizmeti planı paylaştığınızda, bu uygulama örneği bu uygulama hizmeti planı her örneği üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="6b64a-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="6b64a-112">Uygulama ölçeklendirme başına</span><span class="sxs-lookup"><span data-stu-id="6b64a-112">Per app scaling</span></span>
<span data-ttu-id="6b64a-113">*Uygulama ölçeklendirme başına* , uygulama hizmeti planı düzeyinde etkinleştirilmiş ve uygulama başına kullanılan bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="6b64a-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="6b64a-114">Uygulama ölçeklendirme bir uygulamadan bağımsız olarak onu barındıran uygulama hizmeti planı ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="6b64a-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="6b64a-115">Bu şekilde, bir uygulama hizmeti planı olabilir too10 örnekleri ölçeği, ancak bir uygulama toouse yalnızca beş ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="6b64a-115">This way, an App Service plan can be scaled too10 instances, but an app can be set toouse only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="6b64a-116">Uygulama ölçeklendirme yalnızca kullanılabilir **Premium** SKU uygulama hizmeti planları</span><span class="sxs-lookup"><span data-stu-id="6b64a-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="6b64a-117">Ölçeklendirmeyi PowerShell kullanarak uygulama</span><span class="sxs-lookup"><span data-stu-id="6b64a-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="6b64a-118">Olarak yapılandırılmış bir plan oluşturabilirsiniz bir *uygulama ölçeklendirme başına* planı hello geçirerek ```-perSiteScaling $true``` toohello özniteliği ```New-AzureRmAppServicePlan``` komutunu</span><span class="sxs-lookup"><span data-stu-id="6b64a-118">You can create a plan configured as a *Per app scaling* plan by passing in hello ```-perSiteScaling $true``` attribute toohello ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="6b64a-119">Tooupdate istiyorsanız, var olan bir uygulama hizmeti bu özellik toouse planlayın:</span><span class="sxs-lookup"><span data-stu-id="6b64a-119">If you want tooupdate an existing App Service plan toouse this feature:</span></span> 

- <span data-ttu-id="6b64a-120">Merhaba hedef plan Al```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="6b64a-120">get hello target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="6b64a-121">yerel olarak Hello özelliğini değiştirme```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="6b64a-121">modifying hello property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="6b64a-122">değişiklikleri geri tooazure gönderme```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="6b64a-122">posting your changes back tooazure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get hello new App Service Plan and modify hello "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify hello local copy toouse "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back tooazure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="6b64a-123">Merhaba uygulama düzeyinde tooconfigure hello hello uygulama hello uygulama hizmeti planında kullanabilirsiniz örneklerinin sayısını gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b64a-123">At hello app level, we need tooconfigure hello number of instances hello app can use in hello app service plan.</span></span>

<span data-ttu-id="6b64a-124">Hello örnekte hello sınırlı tootwo örnekleri kaç tane bağımsız olarak hello temel app service planı ölçeklendirebilme çıkışı uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="6b64a-124">In hello example below, hello app is limited tootwo instances regardless of how many instances hello underlying app service plan scales out to.</span></span>

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="6b64a-125">$newapp. SiteConfig.NumberOfWorkers farklı $newapp biçimidir. MaxNumberOfWorkers.</span><span class="sxs-lookup"><span data-stu-id="6b64a-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="6b64a-126">Uygulama ölçeklendirme $newapp kullanır. SiteConfig.NumberOfWorkers toodetermine hello ölçek özelliklerini hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="6b64a-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers toodetermine hello scale characteristics of hello app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="6b64a-127">Azure Kaynak Yöneticisi'ni kullanarak uygulama ölçeklendirme başına</span><span class="sxs-lookup"><span data-stu-id="6b64a-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="6b64a-128">Merhaba aşağıdaki *Azure Resource Manager şablonu* oluşturur:</span><span class="sxs-lookup"><span data-stu-id="6b64a-128">hello following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="6b64a-129">Too10 örnekleri ölçeklendirilmiş bir uygulama hizmeti planı</span><span class="sxs-lookup"><span data-stu-id="6b64a-129">An App Service plan that's scaled out too10 instances</span></span>
- <span data-ttu-id="6b64a-130">tooscale tooa en fazla beş örneklerinin yapılandırılmış bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="6b64a-130">an app that's configured tooscale tooa max of five instances.</span></span>

<span data-ttu-id="6b64a-131">Merhaba uygulama hizmeti planı hello Ayarlıyor **PerSiteScaling** özelliği tootrue ```"perSiteScaling": true```.</span><span class="sxs-lookup"><span data-stu-id="6b64a-131">hello App Service plan is setting hello **PerSiteScaling** property tootrue ```"perSiteScaling": true```.</span></span> <span data-ttu-id="6b64a-132">Merhaba uygulama hello ayarı **çalışan sayısı** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span><span class="sxs-lookup"><span data-stu-id="6b64a-132">hello app is setting hello **number of workers** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

```
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters":{
        "appServicePlanName": { "type": "string" },
        "appName": { "type": "string" }
        },
    "resources": [
    {
        "comments": "App Service Plan with per site perSiteScaling = true",
        "type": "Microsoft.Web/serverFarms",
        "sku": {
            "name": "P1",
            "tier": "Premium",
            "size": "P1",
            "family": "P",
            "capacity": 10
            },
        "name": "[parameters('appServicePlanName')]",
        "apiVersion": "2015-08-01",
        "location": "West US",
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "perSiteScaling": true
        }
    },
    {
        "type": "Microsoft.Web/sites",
        "name": "[parameters('appName')]",
        "apiVersion": "2015-08-01-preview",
        "location": "West US",
        "dependsOn": [ "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" ],
        "properties": { "serverFarmId": "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" },
        "resources": [ {
                "comments": "",
                "type": "config",
                "name": "web",
                "apiVersion": "2015-08-01",
                "location": "West US",
                "dependsOn": [ "[resourceId('Microsoft.Web/Sites', parameters('appName'))]" ],
                "properties": { "numberOfWorkers": "5" }
            } ]
        }]
}
```

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="6b64a-133">Yüksek yoğunluklu barındırmak için önerilen yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6b64a-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="6b64a-134">Uygulama ölçeklendirme başına genel Azure bölgeleri ve App Service ortamları etkinleştirilmiş bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="6b64a-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="6b64a-135">Ancak, hello stratejisi App Service ortamları tootake kendi Gelişmiş özelliklerden yararlanmasını ve kapasite hello büyük havuzlarını kullanmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="6b64a-135">However, hello recommended strategy is to use App Service Environments tootake advantage of their advanced features and hello larger pools of capacity.</span></span>  

<span data-ttu-id="6b64a-136">Barındırma, uygulamalarınız için bu adımları tooconfigure yüksek bir yoğunluğu izleyin:</span><span class="sxs-lookup"><span data-stu-id="6b64a-136">Follow these steps tooconfigure high density hosting for your apps:</span></span>

1. <span data-ttu-id="6b64a-137">Uygulama hizmeti ortamı Hello yapılandırın ve barındırma senaryosunda ayrılmış toohello yüksek yoğunluklu bir çalışan havuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="6b64a-137">Configure hello App Service Environment and choose a worker pool that is dedicated toohello high density hosting scenario.</span></span>
1. <span data-ttu-id="6b64a-138">Tek bir uygulama hizmeti planı oluşturmak ve toouse ölçeği tüm hello çalışan havuzunda kullanılabilir kapasite hello.</span><span class="sxs-lookup"><span data-stu-id="6b64a-138">Create a single App Service plan, and scale it toouse all hello available capacity on hello worker pool.</span></span>
1. <span data-ttu-id="6b64a-139">Uygulama hizmeti planı hello üzerinde Hello PerSiteScaling bayrağı tootrue ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6b64a-139">Set hello PerSiteScaling flag tootrue on hello App Service plan.</span></span>
1. <span data-ttu-id="6b64a-140">Yeni uygulama oluşturulur ve toothat uygulama hizmeti planı ile atanan **numberOfWorkers** çok ayarlanan özelliği**1**.</span><span class="sxs-lookup"><span data-stu-id="6b64a-140">New apps are created and assigned toothat App Service plan with the **numberOfWorkers** property set too**1**.</span></span> <span data-ttu-id="6b64a-141">Bu yapılandırmayı kullanarak hello yüksek yoğunluk olası bu çalışan havuzunda verir.</span><span class="sxs-lookup"><span data-stu-id="6b64a-141">Using this configuration yields hello highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="6b64a-142">çalışan Hello sayısını gerektiği gibi uygulama toogrant ek kaynaklar bağımsız olarak yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="6b64a-142">hello number of workers can be configured independently per app toogrant additional resources as needed.</span></span> <span data-ttu-id="6b64a-143">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="6b64a-143">For example:</span></span>
    - <span data-ttu-id="6b64a-144">Yüksek kullanım uygulama ayarlayabilirsiniz **numberOfWorkers** çok**3** toohave daha fazla kapasite bu uygulama için işleme.</span><span class="sxs-lookup"><span data-stu-id="6b64a-144">A high-use app can set **numberOfWorkers** too**3** toohave more processing capacity for that app.</span></span> 
    - <span data-ttu-id="6b64a-145">Düşük kullanım uygulamaları ayarlardı **numberOfWorkers** çok**1**.</span><span class="sxs-lookup"><span data-stu-id="6b64a-145">Low-use apps would set **numberOfWorkers** too**1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b64a-146">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="6b64a-146">Next Steps</span></span>

- [<span data-ttu-id="6b64a-147">Azure App Service planlarına ayrıntılı genel bakış</span><span class="sxs-lookup"><span data-stu-id="6b64a-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="6b64a-148">Giriş tooApp hizmeti ortamı</span><span class="sxs-lookup"><span data-stu-id="6b64a-148">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
