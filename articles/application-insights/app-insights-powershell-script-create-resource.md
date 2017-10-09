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
# <a name="powershell-script-toocreate-an-application-insights-resource"></a><span data-ttu-id="6c8df-103">PowerShell komut dosyası toocreate Application Insights kaynağı</span><span class="sxs-lookup"><span data-stu-id="6c8df-103">PowerShell script toocreate an Application Insights resource</span></span>


<span data-ttu-id="6c8df-104">İstediğiniz zaman toomonitor yeni bir uygulama - veya bir uygulamanın yeni sürümü - ile [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), Microsoft Azure içinde yeni bir kaynak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6c8df-104">When you want toomonitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="6c8df-105">Bu, burada, uygulamanızın hello telemetri verilerini analiz görüntülenir ve kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="6c8df-105">This resource is where hello telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="6c8df-106">PowerShell kullanarak yeni bir kaynak hello oluşturulmasını otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c8df-106">You can automate hello creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="6c8df-107">Örneğin, bir mobil cihaz uygulama geliştiriyorsanız, herhangi bir zamanda olacaktır, birçok yayımlanan sürümü uygulamanızı müşterilerinizin tarafından kullanılıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="6c8df-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="6c8df-108">Karma farklı sürümlerini tooget hello telemetri sonuçlarından istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="6c8df-108">You don't want tooget hello telemetry results from different versions mixed up.</span></span> <span data-ttu-id="6c8df-109">Bu nedenle, derleme işlemi toocreate her yapı için yeni bir kaynak alın.</span><span class="sxs-lookup"><span data-stu-id="6c8df-109">So you get your build process toocreate a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="6c8df-110">Kaynakları tüm kümesi toocreate istiyorsanız aynı hello saat, göz önünde bulundurun [bir Azure şablonu kullanarak hello kaynakları oluşturma](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6c8df-110">If you want toocreate a set of resources all at hello same time, consider [creating hello resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a><span data-ttu-id="6c8df-111">Komut dosyası toocreate Application Insights kaynağı</span><span class="sxs-lookup"><span data-stu-id="6c8df-111">Script toocreate an Application Insights resource</span></span>
<span data-ttu-id="6c8df-112">Merhaba ilgili cmdlet özelliklerine göz atın:</span><span class="sxs-lookup"><span data-stu-id="6c8df-112">See hello relevant cmdlet specs:</span></span>

* [<span data-ttu-id="6c8df-113">AzureRmResource yeni</span><span class="sxs-lookup"><span data-stu-id="6c8df-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="6c8df-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="6c8df-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="6c8df-115">*PowerShell Betiği*</span><span class="sxs-lookup"><span data-stu-id="6c8df-115">*PowerShell Script*</span></span>  

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

## <a name="what-toodo-with-hello-ikey"></a><span data-ttu-id="6c8df-116">Hangi toodo hello iKey ile</span><span class="sxs-lookup"><span data-stu-id="6c8df-116">What toodo with hello iKey</span></span>
<span data-ttu-id="6c8df-117">Her kaynak kendi izleme anahtarını (iKey) tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="6c8df-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="6c8df-118">Merhaba iKey hello kaynak oluşturma komut çıktısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="6c8df-118">hello iKey is an output of hello resource creation script.</span></span> <span data-ttu-id="6c8df-119">Derleme betiğinizin uygulamanıza Application Insights SDK'sı hello iKey toohello sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="6c8df-119">Your build script should provide hello iKey toohello Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="6c8df-120">İki yolu toomake hello iKey kullanılabilir toohello SDK'sı vardır:</span><span class="sxs-lookup"><span data-stu-id="6c8df-120">There are two ways toomake hello iKey available toohello SDK:</span></span>

* <span data-ttu-id="6c8df-121">İçinde [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="6c8df-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="6c8df-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="6c8df-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="6c8df-123">Veya [başlatma kodu](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="6c8df-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="6c8df-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="6c8df-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="6c8df-125">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="6c8df-125">See also</span></span>
* [<span data-ttu-id="6c8df-126">Application Insights ve web test kaynakları Şablondan Oluştur</span><span class="sxs-lookup"><span data-stu-id="6c8df-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="6c8df-127">PowerShell ile Azure Tanılama izleme işlevini ayarlama</span><span class="sxs-lookup"><span data-stu-id="6c8df-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="6c8df-128">PowerShell kullanarak Uyarıları Ayarla</span><span class="sxs-lookup"><span data-stu-id="6c8df-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

