---
title: aaaUsing PowerShell toosetup Azure Application Insights'ta | Microsoft Docs
description: "Yapılandırma Azure tanılama toopipe tooApplication Öngörüler otomatikleştirin."
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
ms.openlocfilehash: c48a5d8eb23df162522860935af876063aaa6976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="52a0a-103">Bir Azure web uygulaması için Application Insights yukarı PowerShell tooset kullanma</span><span class="sxs-lookup"><span data-stu-id="52a0a-103">Using PowerShell tooset up Application Insights for an Azure web app</span></span>
<span data-ttu-id="52a0a-104">[Microsoft Azure](https://azure.com) olabilir [toosend Azure tanılama yapılandırılmış](app-insights-azure-diagnostics.md) çok[Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="52a0a-104">[Microsoft Azure](https://azure.com) can be [configured toosend Azure Diagnostics](app-insights-azure-diagnostics.md) too[Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="52a0a-105">Hello tanılama tooAzure Cloud Services ve Azure Vm'leriyle ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="52a0a-105">hello diagnostics relate tooAzure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="52a0a-106">Bunlar içinde hello uygulamayı hello Application Insights SDK'sı kullanarak gönderdiğiniz hello telemetriyi tamamlar.</span><span class="sxs-lookup"><span data-stu-id="52a0a-106">They complement hello telemetry that you send from within hello app using hello Application Insights SDK.</span></span> <span data-ttu-id="52a0a-107">Bir parçası olarak Azure'da yeni kaynaklar oluşturma hello sürecinin otomatikleştirilmesi tanılamayı PowerShell kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52a0a-107">As part of automating hello process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="52a0a-108">Azure şablonu</span><span class="sxs-lookup"><span data-stu-id="52a0a-108">Azure template</span></span>
<span data-ttu-id="52a0a-109">Merhaba web uygulaması azure'deyse ve Azure Resource Manager şablonu kullanarak kaynaklarınızı oluşturursanız, bu toohello kaynak düğümüne ekleyerek Application Insights yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="52a0a-109">If hello web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this toohello resources node:</span></span>

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

* <span data-ttu-id="52a0a-110">`nameOfAIAppResource`-hello Application Insights kaynağı için bir ad</span><span class="sxs-lookup"><span data-stu-id="52a0a-110">`nameOfAIAppResource` - a name for hello Application Insights resource</span></span>
* <span data-ttu-id="52a0a-111">`myWebAppName`-hello web uygulamasının hello kimliği</span><span class="sxs-lookup"><span data-stu-id="52a0a-111">`myWebAppName` - hello id of hello web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="52a0a-112">Bulut Hizmeti dağıtımının bir parçası olarak tanılama uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="52a0a-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="52a0a-113">Merhaba `New-AzureDeployment` cmdlet'i bir parametresine sahip `ExtensionConfiguration`, bir dizi tanılama yapılandırması alır.</span><span class="sxs-lookup"><span data-stu-id="52a0a-113">hello `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="52a0a-114">Bunlar hello kullanılarak oluşturulabilir `New-AzureServiceDiagnosticsExtensionConfig` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="52a0a-114">These can be created using hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="52a0a-115">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="52a0a-115">For example:</span></span>

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="52a0a-116">Mevcut bir Bulut Hizmetinde tanılama uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="52a0a-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="52a0a-117">Mevcut bir hizmet üzerinde `Set-AzureServiceDiagnosticsExtension` kullanma</span><span class="sxs-lookup"><span data-stu-id="52a0a-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

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

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="52a0a-118">Güncel tanılama uzantı yapılandırmasını alma</span><span class="sxs-lookup"><span data-stu-id="52a0a-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="52a0a-119">Tanılama uzantısını kaldırma</span><span class="sxs-lookup"><span data-stu-id="52a0a-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="52a0a-120">Merhaba tanılama uzantısını kullanarak etkinleştirilirse `Set-AzureServiceDiagnosticsExtension` veya `New-AzureServiceDiagnosticsExtensionConfig` hello rol parametresi sonra hello uzantısını kullanarak kaldırabilirsiniz `Remove-AzureServiceDiagnosticsExtension` hello rol parametresi olmadan.</span><span class="sxs-lookup"><span data-stu-id="52a0a-120">If you enabled hello diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without hello Role parameter, then you can remove hello extension using `Remove-AzureServiceDiagnosticsExtension` without hello Role parameter.</span></span> <span data-ttu-id="52a0a-121">Merhaba uzantı etkinleştirilirken Hello rol parametresi kullanıldıysa, sonra da hello uzantı kaldırılırken kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="52a0a-121">If hello Role parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="52a0a-122">tek tek her rolden tooremove hello tanılama uzantısını:</span><span class="sxs-lookup"><span data-stu-id="52a0a-122">tooremove hello diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="52a0a-123">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="52a0a-123">See also</span></span>
* [<span data-ttu-id="52a0a-124">Application Insights’la Azure Cloud Services uygulamalarını izleme</span><span class="sxs-lookup"><span data-stu-id="52a0a-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="52a0a-125">Azure tanılama tooApplication Öngörüler Gönder</span><span class="sxs-lookup"><span data-stu-id="52a0a-125">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="52a0a-126">Yapılandırma uyarılarını otomatik hale getirme</span><span class="sxs-lookup"><span data-stu-id="52a0a-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

