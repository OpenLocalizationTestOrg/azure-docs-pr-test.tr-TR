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
# <a name="high-density-hosting-on-azure-app-service"></a>Azure uygulama hizmeti üzerinde yüksek yoğunluklu barındırma
Uygulama hizmeti kullanırken, uygulamanız tarafından iki kavramları tooit ayrılan hello kapasiteden ayrılmış:

* **Merhaba uygulama:** hello uygulama ve çalışma zamanı yapılandırmasını temsil eder. Örneğin, hello içeren çalışma zamanı hello .NET sürümü yükü hello uygulaması ayarları.
* **Merhaba App Service planı:** hello hello kapasite, kullanılabilir özellik kümesini ve yere göre hello uygulamasının özelliklerini tanımlar. Örneğin, özellikleri büyük (dört çekirdek) makine, dört örnekleri, Doğu ABD Premium özellikleri olabilir.

Bir uygulama her zaman bağlı tooan uygulama hizmeti planı'dır, ancak bir uygulama hizmeti planı kapasite tooone ya da daha fazla uygulama sağlayabilir.

Sonuç olarak, hello platform hello esneklik tooisolate tek bir uygulamayı sağlar veya bir uygulama hizmeti planı paylaşarak kaynakları paylaşan birden çok uygulamalara sahip.

Ancak, birden fazla uygulama bir uygulama hizmeti planı paylaştığınızda, bu uygulama örneği bu uygulama hizmeti planı her örneği üzerinde çalışır.

## <a name="per-app-scaling"></a>Uygulama ölçeklendirme başına
*Uygulama ölçeklendirme başına* , uygulama hizmeti planı düzeyinde etkinleştirilmiş ve uygulama başına kullanılan bir özelliğidir.

Uygulama ölçeklendirme bir uygulamadan bağımsız olarak onu barındıran uygulama hizmeti planı ölçeklendirir. Bu şekilde, bir uygulama hizmeti planı olabilir too10 örnekleri ölçeği, ancak bir uygulama toouse yalnızca beş ayarlanabilir.

   >[!NOTE]
   >Uygulama ölçeklendirme yalnızca kullanılabilir **Premium** SKU uygulama hizmeti planları
   >

### <a name="per-app-scaling-using-powershell"></a>Ölçeklendirmeyi PowerShell kullanarak uygulama

Olarak yapılandırılmış bir plan oluşturabilirsiniz bir *uygulama ölçeklendirme başına* planı hello geçirerek ```-perSiteScaling $true``` toohello özniteliği ```New-AzureRmAppServicePlan``` komutunu

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

Tooupdate istiyorsanız, var olan bir uygulama hizmeti bu özellik toouse planlayın: 

- Merhaba hedef plan Al```Get-AzureRmAppServicePlan```
- yerel olarak Hello özelliğini değiştirme```$newASP.PerSiteScaling = $true```
- değişiklikleri geri tooazure gönderme```Set-AzureRmAppServicePlan``` 

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

Merhaba uygulama düzeyinde tooconfigure hello hello uygulama hello uygulama hizmeti planında kullanabilirsiniz örneklerinin sayısını gerekir.

Hello örnekte hello sınırlı tootwo örnekleri kaç tane bağımsız olarak hello temel app service planı ölçeklendirebilme çıkışı uygulamasıdır.

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> $newapp. SiteConfig.NumberOfWorkers farklı $newapp biçimidir. MaxNumberOfWorkers. Uygulama ölçeklendirme $newapp kullanır. SiteConfig.NumberOfWorkers toodetermine hello ölçek özelliklerini hello uygulama.

### <a name="per-app-scaling-using-azure-resource-manager"></a>Azure Kaynak Yöneticisi'ni kullanarak uygulama ölçeklendirme başına

Merhaba aşağıdaki *Azure Resource Manager şablonu* oluşturur:

- Too10 örnekleri ölçeklendirilmiş bir uygulama hizmeti planı
- tooscale tooa en fazla beş örneklerinin yapılandırılmış bir uygulama.

Merhaba uygulama hizmeti planı hello Ayarlıyor **PerSiteScaling** özelliği tootrue ```"perSiteScaling": true```. Merhaba uygulama hello ayarı **çalışan sayısı** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.

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

## <a name="recommended-configuration-for-high-density-hosting"></a>Yüksek yoğunluklu barındırmak için önerilen yapılandırma
Uygulama ölçeklendirme başına genel Azure bölgeleri ve App Service ortamları etkinleştirilmiş bir özelliktir. Ancak, hello stratejisi App Service ortamları tootake kendi Gelişmiş özelliklerden yararlanmasını ve kapasite hello büyük havuzlarını kullanmak için önerilir.  

Barındırma, uygulamalarınız için bu adımları tooconfigure yüksek bir yoğunluğu izleyin:

1. Uygulama hizmeti ortamı Hello yapılandırın ve barındırma senaryosunda ayrılmış toohello yüksek yoğunluklu bir çalışan havuzu seçin.
1. Tek bir uygulama hizmeti planı oluşturmak ve toouse ölçeği tüm hello çalışan havuzunda kullanılabilir kapasite hello.
1. Uygulama hizmeti planı hello üzerinde Hello PerSiteScaling bayrağı tootrue ayarlayın.
1. Yeni uygulama oluşturulur ve toothat uygulama hizmeti planı ile atanan **numberOfWorkers** çok ayarlanan özelliği**1**. Bu yapılandırmayı kullanarak hello yüksek yoğunluk olası bu çalışan havuzunda verir.
1. çalışan Hello sayısını gerektiği gibi uygulama toogrant ek kaynaklar bağımsız olarak yapılandırılabilir. Örneğin:
    - Yüksek kullanım uygulama ayarlayabilirsiniz **numberOfWorkers** çok**3** toohave daha fazla kapasite bu uygulama için işleme. 
    - Düşük kullanım uygulamaları ayarlardı **numberOfWorkers** çok**1**.

## <a name="next-steps"></a>Sonraki Adımlar

- [Azure App Service planlarına ayrıntılı genel bakış](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [Giriş tooApp hizmeti ortamı](../app-service-web/app-service-app-service-environment-intro.md)
