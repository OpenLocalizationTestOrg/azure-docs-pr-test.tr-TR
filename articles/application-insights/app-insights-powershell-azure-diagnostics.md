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
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a>Bir Azure web uygulaması için Application Insights yukarı PowerShell tooset kullanma
[Microsoft Azure](https://azure.com) olabilir [toosend Azure tanılama yapılandırılmış](app-insights-azure-diagnostics.md) çok[Azure Application Insights](app-insights-overview.md). Hello tanılama tooAzure Cloud Services ve Azure Vm'leriyle ilişkilidir. Bunlar içinde hello uygulamayı hello Application Insights SDK'sı kullanarak gönderdiğiniz hello telemetriyi tamamlar. Bir parçası olarak Azure'da yeni kaynaklar oluşturma hello sürecinin otomatikleştirilmesi tanılamayı PowerShell kullanarak yapılandırabilirsiniz.

## <a name="azure-template"></a>Azure şablonu
Merhaba web uygulaması azure'deyse ve Azure Resource Manager şablonu kullanarak kaynaklarınızı oluşturursanız, bu toohello kaynak düğümüne ekleyerek Application Insights yapılandırabilirsiniz:

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

* `nameOfAIAppResource`-hello Application Insights kaynağı için bir ad
* `myWebAppName`-hello web uygulamasının hello kimliği

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Bulut Hizmeti dağıtımının bir parçası olarak tanılama uzantısını etkinleştirme
Merhaba `New-AzureDeployment` cmdlet'i bir parametresine sahip `ExtensionConfiguration`, bir dizi tanılama yapılandırması alır. Bunlar hello kullanılarak oluşturulabilir `New-AzureServiceDiagnosticsExtensionConfig` cmdlet'i. Örneğin:

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Mevcut bir Bulut Hizmetinde tanılama uzantısını etkinleştirme
Mevcut bir hizmet üzerinde `Set-AzureServiceDiagnosticsExtension` kullanma

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

## <a name="get-current-diagnostics-extension-configuration"></a>Güncel tanılama uzantı yapılandırmasını alma
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a>Tanılama uzantısını kaldırma
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Merhaba tanılama uzantısını kullanarak etkinleştirilirse `Set-AzureServiceDiagnosticsExtension` veya `New-AzureServiceDiagnosticsExtensionConfig` hello rol parametresi sonra hello uzantısını kullanarak kaldırabilirsiniz `Remove-AzureServiceDiagnosticsExtension` hello rol parametresi olmadan. Merhaba uzantı etkinleştirilirken Hello rol parametresi kullanıldıysa, sonra da hello uzantı kaldırılırken kullanılmalıdır.

tek tek her rolden tooremove hello tanılama uzantısını:

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a>Ayrıca bkz.
* [Application Insights’la Azure Cloud Services uygulamalarını izleme](app-insights-cloudservices.md)
* [Azure tanılama tooApplication Öngörüler Gönder](app-insights-azure-diagnostics.md)
* [Yapılandırma uyarılarını otomatik hale getirme](app-insights-powershell-alerts.md)

