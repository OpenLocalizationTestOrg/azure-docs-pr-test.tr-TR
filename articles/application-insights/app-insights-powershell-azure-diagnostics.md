---
title: "Azure’da Application Insights’ı kurmak için PowerShell’i kullanma | Microsoft Belgeleri"
description: "Application Insights’a kanal oluşturmak için Azure Tanılama’yı yapılandırmayı otomatikleştirme"
services: application-insights
documentationcenter: .net
author: sbtron
manager: carmonm
ms.assetid: 4ac803a8-f424-4c0c-b18f-4b9c189a64a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/17/2015
ms.author: bwren
ms.openlocfilehash: 3b6da89cc33cda713b483a2af3cbb493a03d6bec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="using-powershell-to-set-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="bd827-103">Bir Azure web uygulaması için Application Insights’ı kurmak üzere PowerShell’i kullanma</span><span class="sxs-lookup"><span data-stu-id="bd827-103">Using PowerShell to set up Application Insights for an Azure web app</span></span>
<span data-ttu-id="bd827-104">[Microsoft Azure](https://azure.com), [Azure Application Insights](app-insights-overview.md)'a [Azure Tanılama verileri gönderecek şekilde yapılandırılabilir.](app-insights-azure-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="bd827-104">[Microsoft Azure](https://azure.com) can be [configured to send Azure Diagnostics](app-insights-azure-diagnostics.md) to [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="bd827-105">Tanılama verileri Azure Cloud Services ve Azure VM’leriyle ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="bd827-105">The diagnostics relate to Azure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="bd827-106">Uygulama içinde Application Insights SDK’sı kullanarak gönderdiğiniz telemetriyi tamamlar.</span><span class="sxs-lookup"><span data-stu-id="bd827-106">They complement the telemetry that you send from within the app using the Application Insights SDK.</span></span> <span data-ttu-id="bd827-107">Azure’da yeni kaynaklar oluşturma işlemini otomatikleştirmenin bir parçası olarak tanılamayı PowerShell kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd827-107">As part of automating the process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="bd827-108">Azure şablonu</span><span class="sxs-lookup"><span data-stu-id="bd827-108">Azure template</span></span>
<span data-ttu-id="bd827-109">web uygulaması Azure’deyse ve Azure Resource Manager şablonu kullanarak kaynaklarınızı oluşturuyorsanız, bunu kaynak düğümüne ekleyerek Application Insights’ı yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bd827-109">If the web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this to the resources node:</span></span>

    {
      resources: [
        /* Create Application Insights resource */
        {
          "apiVersion": "2015-05-01",
          "type": "microsoft.insights/components",
          "name": "nameOfAIAppResource",
          "location": "centralus",
          "kind": "web",
          "properties": { "ApplicationId": "nameOfAIAppResource" },
          "dependsOn": [
            "[concat('Microsoft.Web/sites/', myWebAppName)]"
          ]
        }
       ]
     } 

* <span data-ttu-id="bd827-110">`nameOfAIAppResource` - Application Insights kaynağı adı</span><span class="sxs-lookup"><span data-stu-id="bd827-110">`nameOfAIAppResource` - a name for the Application Insights resource</span></span>
* <span data-ttu-id="bd827-111">`myWebAppName` - web uygulaması kimliği</span><span class="sxs-lookup"><span data-stu-id="bd827-111">`myWebAppName` - the id of the web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="bd827-112">Bulut Hizmeti dağıtımının bir parçası olarak tanılama uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bd827-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="bd827-113">`New-AzureDeployment` cmdlet’i, bir dizi tanılama yapılandırması içeren `ExtensionConfiguration` parametresine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bd827-113">The `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="bd827-114">Bunlar, `New-AzureServiceDiagnosticsExtensionConfig` cmdlet’i kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="bd827-114">These can be created using the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="bd827-115">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="bd827-115">For example:</span></span>

```ps

    $service_package = "CloudService.cspkg"
    $service_config = "ServiceConfiguration.Cloud.cscfg"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

    $primary_storagekey = (Get-AzureStorageKey `
     -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
       -StorageAccountName $diagnostics_storagename `
       -StorageAccountKey $primary_storagekey

    $webrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WebRole" -Storage_context $storageContext `
      -DiagnosticsConfigurationPath $webrole_diagconfigpath
    $workerrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WorkerRole" `
      -StorageContext $storage_context `
      -DiagnosticsConfigurationPath $workerrole_diagconfigpath

    New-AzureDeployment `
      -ServiceName $service_name `
      -Slot Production `
      -Package $service_package `
      -Configuration $service_config `
      -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)

``` 

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="bd827-116">Mevcut bir Bulut Hizmetinde tanılama uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bd827-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="bd827-117">Mevcut bir hizmet üzerinde `Set-AzureServiceDiagnosticsExtension` kullanma</span><span class="sxs-lookup"><span data-stu-id="bd827-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

```ps

    $service_name = "MyService"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"
    $primary_storagekey = (Get-AzureStorageKey `
         -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
        -StorageAccountName $diagnostics_storagename `
        -StorageAccountKey $primary_storagekey

    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $webrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WebRole" 
    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $workerrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WorkerRole"
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="bd827-118">Güncel tanılama uzantı yapılandırmasını alma</span><span class="sxs-lookup"><span data-stu-id="bd827-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="bd827-119">Tanılama uzantısını kaldırma</span><span class="sxs-lookup"><span data-stu-id="bd827-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="bd827-120">Tanılama uzantısını Rol parametresi olmadan `Set-AzureServiceDiagnosticsExtension` veya `New-AzureServiceDiagnosticsExtensionConfig` ile etkinleştirdiyseniz, uzantıyı Rol parametresi olmadan `Remove-AzureServiceDiagnosticsExtension` kullanarak kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd827-120">If you enabled the diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without the Role parameter, then you can remove the extension using `Remove-AzureServiceDiagnosticsExtension` without the Role parameter.</span></span> <span data-ttu-id="bd827-121">Uzantı etkinleştirilirken Rol parametresi kullanıldıysa, uzantı kaldırılırken de kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd827-121">If the Role parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="bd827-122">Tanılama uzantısını her bir rolden kaldırmak için:</span><span class="sxs-lookup"><span data-stu-id="bd827-122">To remove the diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="bd827-123">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="bd827-123">See also</span></span>
* [<span data-ttu-id="bd827-124">Application Insights’la Azure Cloud Services uygulamalarını izleme</span><span class="sxs-lookup"><span data-stu-id="bd827-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="bd827-125">Azure Tanılama verilerini Application Insights’a gönderme</span><span class="sxs-lookup"><span data-stu-id="bd827-125">Send Azure Diagnostics to Application Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="bd827-126">Yapılandırma uyarılarını otomatik hale getirme</span><span class="sxs-lookup"><span data-stu-id="bd827-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

