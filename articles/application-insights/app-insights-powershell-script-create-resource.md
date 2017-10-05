---
title: "Application Insights kaynağı oluşturmak için PowerShell betiğini | Microsoft Docs"
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
ms.openlocfilehash: a828af9c7d207dd84cc626fc70206018fd67e2dd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="powershell-script-to-create-an-application-insights-resource"></a><span data-ttu-id="27976-103">Application Insights kaynağı oluşturmak için PowerShell betiği</span><span class="sxs-lookup"><span data-stu-id="27976-103">PowerShell script to create an Application Insights resource</span></span>


<span data-ttu-id="27976-104">Ne zaman yeni bir uygulama - veya bir uygulamanın yeni sürümü - izlemek istediğiniz ile [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), Microsoft Azure içinde yeni bir kaynak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="27976-104">When you want to monitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="27976-105">Bu, burada, uygulamanızın telemetri verilerini analiz görüntülenir ve kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="27976-105">This resource is where the telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="27976-106">PowerShell kullanarak yeni bir kaynak oluşturulmasını otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27976-106">You can automate the creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="27976-107">Örneğin, bir mobil cihaz uygulama geliştiriyorsanız, herhangi bir zamanda olacaktır, birçok yayımlanan sürümü uygulamanızı müşterilerinizin tarafından kullanılıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="27976-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="27976-108">Karma farklı sürümlerdeki telemetri sonuçlar almak istemiyorum.</span><span class="sxs-lookup"><span data-stu-id="27976-108">You don't want to get the telemetry results from different versions mixed up.</span></span> <span data-ttu-id="27976-109">Bu nedenle, her yapı için yeni bir kaynak oluşturmak için yapı işleminizin alırsınız.</span><span class="sxs-lookup"><span data-stu-id="27976-109">So you get your build process to create a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="27976-110">Tümü aynı anda bir kaynak kümesi oluşturmak istiyorsanız, göz önünde bulundurun [bir Azure şablonu kullanarak kaynak oluşturma](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="27976-110">If you want to create a set of resources all at the same time, consider [creating the resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-to-create-an-application-insights-resource"></a><span data-ttu-id="27976-111">Application Insights kaynağı oluşturmak için komut dosyası</span><span class="sxs-lookup"><span data-stu-id="27976-111">Script to create an Application Insights resource</span></span>
<span data-ttu-id="27976-112">İlgili cmdlet özelliklerine göz atın:</span><span class="sxs-lookup"><span data-stu-id="27976-112">See the relevant cmdlet specs:</span></span>

* [<span data-ttu-id="27976-113">AzureRmResource yeni</span><span class="sxs-lookup"><span data-stu-id="27976-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="27976-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="27976-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="27976-115">*PowerShell Betiği*</span><span class="sxs-lookup"><span data-stu-id="27976-115">*PowerShell Script*</span></span>  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before the first 
# execution to login to the Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set the name of the Application Insights Resource

$appInsightsName = "TestApp"

# Set the application name used for the value of the Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set the name of the Resource Group to use.  
# Default is the application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create the Resource and Output the name and iKey
###################################################

# Select the azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create the App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access to the team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-to-do-with-the-ikey"></a><span data-ttu-id="27976-116">İle iKey yapmanız gerekenler</span><span class="sxs-lookup"><span data-stu-id="27976-116">What to do with the iKey</span></span>
<span data-ttu-id="27976-117">Her kaynak kendi izleme anahtarını (iKey) tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="27976-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="27976-118">İKey kaynak oluşturma komut çıktısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="27976-118">The iKey is an output of the resource creation script.</span></span> <span data-ttu-id="27976-119">Derleme betiğinizin uygulamanıza Application Insights SDK'sı için iKey sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="27976-119">Your build script should provide the iKey to the Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="27976-120">İKey SDK kullanılabilir yapmak için iki yol vardır:</span><span class="sxs-lookup"><span data-stu-id="27976-120">There are two ways to make the iKey available to the SDK:</span></span>

* <span data-ttu-id="27976-121">İçinde [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="27976-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="27976-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="27976-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="27976-123">Veya [başlatma kodu](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="27976-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="27976-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="27976-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="27976-125">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="27976-125">See also</span></span>
* [<span data-ttu-id="27976-126">Application Insights ve web test kaynakları Şablondan Oluştur</span><span class="sxs-lookup"><span data-stu-id="27976-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="27976-127">PowerShell ile Azure Tanılama izleme işlevini ayarlama</span><span class="sxs-lookup"><span data-stu-id="27976-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="27976-128">PowerShell kullanarak Uyarıları Ayarla</span><span class="sxs-lookup"><span data-stu-id="27976-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

