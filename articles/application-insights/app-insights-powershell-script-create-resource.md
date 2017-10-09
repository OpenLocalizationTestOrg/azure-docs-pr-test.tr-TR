---
title: "aaaPowerShell betik toocreate Application Insights kaynağı | Microsoft Docs"
description: "Application Insights kaynakların oluşturulmasını otomatik hale getirme."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: f0082c9b-43ad-4576-a417-4ea8e0daf3d9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/19/2016
ms.author: bwren
ms.openlocfilehash: 2ac00376d38026d64c2c5deabfaca60588924510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-script-toocreate-an-application-insights-resource"></a>PowerShell komut dosyası toocreate Application Insights kaynağı


İstediğiniz zaman toomonitor yeni bir uygulama - veya bir uygulamanın yeni sürümü - ile [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), Microsoft Azure içinde yeni bir kaynak ayarlayın. Bu, burada, uygulamanızın hello telemetri verilerini analiz görüntülenir ve kaynaktır. 

PowerShell kullanarak yeni bir kaynak hello oluşturulmasını otomatik hale getirebilirsiniz.

Örneğin, bir mobil cihaz uygulama geliştiriyorsanız, herhangi bir zamanda olacaktır, birçok yayımlanan sürümü uygulamanızı müşterilerinizin tarafından kullanılıyor olabilir. Karma farklı sürümlerini tooget hello telemetri sonuçlarından istemezsiniz. Bu nedenle, derleme işlemi toocreate her yapı için yeni bir kaynak alın.

> [!NOTE]
> Kaynakları tüm kümesi toocreate istiyorsanız aynı hello saat, göz önünde bulundurun [bir Azure şablonu kullanarak hello kaynakları oluşturma](app-insights-powershell.md).
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a>Komut dosyası toocreate Application Insights kaynağı
Merhaba ilgili cmdlet özelliklerine göz atın:

* [AzureRmResource yeni](https://msdn.microsoft.com/library/mt652510.aspx)
* [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt678995.aspx)

*PowerShell Betiği*  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before hello first 
# execution toologin toohello Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set hello name of hello Application Insights Resource

$appInsightsName = "TestApp"

# Set hello application name used for hello value of hello Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set hello name of hello Resource Group toouse.  
# Default is hello application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create hello Resource and Output hello name and iKey
###################################################

# Select hello azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create hello App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access toohello team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-toodo-with-hello-ikey"></a>Hangi toodo hello iKey ile
Her kaynak kendi izleme anahtarını (iKey) tarafından tanımlanır. Merhaba iKey hello kaynak oluşturma komut çıktısı ' dir. Derleme betiğinizin uygulamanıza Application Insights SDK'sı hello iKey toohello sağlamalıdır.

İki yolu toomake hello iKey kullanılabilir toohello SDK'sı vardır:

* İçinde [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md): 
  * `<instrumentationkey>`*ikey*`</instrumentationkey>`
* Veya [başlatma kodu](app-insights-api-custom-events-metrics.md): 
  * `Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`

## <a name="see-also"></a>Ayrıca bkz.
* [Application Insights ve web test kaynakları Şablondan Oluştur](app-insights-powershell.md)
* [PowerShell ile Azure Tanılama izleme işlevini ayarlama](app-insights-powershell-azure-diagnostics.md) 
* [PowerShell kullanarak Uyarıları Ayarla](app-insights-powershell-alerts.md)

