---
title: "aaaCollect Azure günlük analizi için Hizmet Günlükleri ve ölçümleri | Microsoft Docs"
description: "Tanılama Azure kaynaklarını toowrite günlüklerini ve ölçümleri tooLog analiz yapılandırın."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 84105740-3697-4109-bc59-2452c1131bfe
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1cede9a94ec83c4e3a95853dc2ec355d8df06d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-azure-service-logs-and-metrics-for-use-in-log-analytics"></a>Azure Hizmeti günlüklerini ve günlük analizi kullanımda ölçümlerini Topla

Günlükleri ve Azure Hizmetleri için ölçümleri toplama dört farklı yolu vardır:

1. Azure tanılama doğrudan tooLog Analytics (*tanılama* hello aşağıdaki tablonun içinde)
2. Azure tanılama tooAzure depolama tooLog Analytics (*depolama* hello aşağıdaki tablonun içinde)
3. Azure Hizmetleri için bağlayıcıları (*Bağlayıcılar* hello aşağıdaki tablonun içinde)
4. Günlük analizi (boşlukları aşağıdaki tablonun hello ve için listelenmeyen Hizmetleri) içine toocollect ve gönderme verisi komutlar


| Hizmet                 | Kaynak Türü                           | Günlükler        | Ölçümler     | Çözüm |
| --- | --- | --- | --- | --- |
| Uygulama ağ geçitleri    | Microsoft.Network/applicationGateways   | Tanılama | Tanılama | [Azure uygulama ağ geçidi analizi](log-analytics-azure-networking-analytics.md#azure-application-gateway-analytics-solution-in-log-analytics) |
| Application ınsights    |                                         | Bağlayıcı   | Bağlayıcı   | [Uygulama Öngörüler Bağlayıcısı](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) (Önizleme) |
| Automation hesapları     | Microsoft.Automation/AutomationAccounts | Tanılama |             | [Daha fazla bilgi](../automation/automation-manage-send-joblogs-log-analytics.md)|
| Toplu hesaplar          | Microsoft.Batch/batchAccounts           | Tanılama | Tanılama | |
| Klasik bulut Hizmetleri  |                                         | Depolama     |             | [Daha fazla bilgi](log-analytics-azure-storage-iis-table.md) |
| Bilişsel Hizmetler      | Microsoft.CognitiveServices/accounts    |             | Tanılama | |
| Data Lake analizi     | Microsoft.DataLakeAnalytics/accounts    | Tanılama |             | |
| Veri Gölü deposu         | Microsoft.DataLakeStore/accounts        | Tanılama |             | |
| Olay Hub'ad alanı     | Microsoft.EventHub/namespaces           | Tanılama | Tanılama | |
| IOT hub'ları                | Microsoft.Devices/IotHubs               |             | Tanılama | |
| Anahtar Kasası               | Microsoft.KeyVault/vaults               | Tanılama |             | [KeyVault analizi](log-analytics-azure-key-vault.md) |
| Yük Dengeleyici          | Microsoft.Network/loadBalancers         | Tanılama |             |  |
| Logic Apps              | Microsoft.Logic/workflows <br> Microsoft.Logic/integrationAccounts | Tanılama | Tanılama | |
| Ağ Güvenlik Grupları | Microsoft.Network/networksecuritygroups | Tanılama |             | [Azure ağ güvenlik grubu analizi](log-analytics-azure-networking-analytics.md#azure-network-security-group-analytics-solution-in-log-analytics) |
| Kurtarma kasaları         | Microsoft.RecoveryServices/vaults       |             |             | [Analytics (Önizleme) Azure kurtarma Hizmetleri](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
| Hizmet ara         | Microsoft.Search/searchServices         | Tanılama | Tanılama | |
| Hizmet veri yolu ad alanı   | Microsoft.ServiceBus/namespaces         | Tanılama | Tanılama | [Hizmet veri yolu Analytics (Önizleme)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
| Service Fabric          |                                         | Depolama     |             | [Service Fabric Analytics (Önizleme)](log-analytics-service-fabric.md) |
| SQL (v12)               | Microsoft.Sql/servers/databases <br> Microsoft.Sql/servers/elasticPools |             | Tanılama | [Azure SQL analizi (Önizleme)](log-analytics-azure-sql.md) |
| Depolama                 |                                         |             | Betik      | [Azure depolama çözümlemeleri (Önizleme)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution) |
| Virtual Machines        | Microsoft.Compute/virtualMachines       | Dahili numara   | Dahili numara <br> Tanılama  | |
| Sanal makine ölçek kümeleri | Microsoft.Compute/virtualMachines <br> Microsoft.Compute/virtualMachineScaleSets/virtualMachines |             | Tanılama | |
| Web sunucu grupları        | Microsoft.Web/serverfarms               |             | Tanılama | |
| Web Siteleri               | Microsoft.Web/sites <br> Microsoft.Web/sites/slots |             | Tanılama | [Azure Web uygulamaları analizi (Önizleme)](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) |


> [!NOTE]
> Azure sanal makine (Linux ve Windows'da) izlemek için hello yüklemenizi öneririz [günlük analizi VM uzantısı](log-analytics-azure-vm-extension.md). Hello Aracısı sanal makinelerinizin içinde toplanan Öngörüler sunar. Merhaba uzantısı sanal makine ölçek kümeleri için de kullanabilirsiniz.
>
>

## <a name="azure-diagnostics-direct-toolog-analytics"></a>Azure tanılama doğrudan tooLog analizi
TooLog analizi ve bu değer doğrudan çözümleme hello verilerini toplayan hello tercih edilen yol birçok Azure mümkün toowrite tanılama günlüklerini ve ölçümleri kaynaklardır. Azure tanılama kullanırken, veriler hemen tooLog Analytics yazılır ve hiçbir gerek toofirst yazma hello veri toostorage yok.

Destek azure kaynaklarını [Azure İzleyici](../monitoring-and-diagnostics/monitoring-overview.md) kendi günlüklerini ve ölçümleri gönderebilirsiniz doğrudan tooLog Analytics.

* Merhaba kullanılabilir ölçümler Hello ayrıntılarını çok başvuran[ölçümleri Azure İzleyicisi ile desteklenen](../monitoring-and-diagnostics/monitoring-supported-metrics.md).
* Merhaba kullanılabilir günlüklerini Hello ayrıntılarını çok başvuran[desteklenen Hizmetleri ve şema için tanılama günlüklerini](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

### <a name="enable-diagnostics-with-powershell"></a>PowerShell ile tanılamayı etkinleştirme
Kasım 2016 (v2.3.0) hello veya sonraki sürümünün gerek [Azure PowerShell](/powershell/azure/overview).

PowerShell örnekteki nasıl aşağıdaki hello toouse [Set-AzureRmDiagnosticSetting](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting) tooenable tanılama bir ağ güvenlik grubu. Merhaba aynı yaklaşım çalışır desteklenen tüm kaynaklar için - ayarlamak `$resourceId` tooenable tanılama için istediğiniz hello kaynağın toohello kaynak kimliği.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO"

Set-AzureRmDiagnosticSetting -ResourceId $ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="enable-diagnostics-with-resource-manager-templates"></a>Resource Manager şablonları ile tanılamayı etkinleştirin

Bunu oluşturulduğunda ve hello tanılama tooyour günlük analizi çalışma alanı altında bir şablon benzer toohello birini kullanabilirsiniz gönderdiğiniz bir kaynakta tooenable tanılama. Bu örnek bir Otomasyon hesabı, ancak tüm desteklenen kaynak türleri için çalışır içindir.

```json
        {
            "type": "Microsoft.Automation/automationAccounts/providers/diagnosticSettings",
            "name": "[concat(parameters('omsAutomationAccountName'), '/', 'Microsoft.Insights/service')]",
            "apiVersion": "2015-07-01",
            "dependsOn": [
                "[concat('Microsoft.Automation/automationAccounts/', parameters('omsAutomationAccountName'))]",
                "[concat('Microsoft.OperationalInsights/workspaces/', parameters('omsWorkspaceName'))]"
            ],
            "properties": {
                "workspaceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('omsWorkspaceName'))]",
                "logs": [
                    {
                        "category": "JobLogs",
                        "enabled": true
                    },
                    {
                        "category": "JobStreams",
                        "enabled": true
                    }
                ]
            }
        }
```

[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="azure-diagnostics-toostorage-then-toolog-analytics"></a>Azure tanılama toostorage sonra tooLog analizi

Bazı kaynaklar içinde günlükleri toplama, bu olası toosend hello günlükleri tooAzure depolama ve günlük analizi depolama hello günlüklerinden tooread yapılandırın.

Günlük analizi hello için bu yaklaşım toocollect tanılama Azure depolama biriminden kullanabileceğiniz kaynaklar ve günlükleri aşağıdaki:

| Kaynak | Günlükler |
| --- | --- |
| Service Fabric |ETWEvent <br> İşlem olayı <br> Güvenilir aktör olay <br> Güvenilir hizmet olayı |
| Virtual Machines |Linux Syslog <br> Windows olayı <br> IIS günlüğü <br> Windows ETWEvent |
| Web rolleri <br> Çalışan rolleri |Linux Syslog <br> Windows olayı <br> IIS günlüğü <br> Windows ETWEvent |

> [!NOTE]
> Azure normal veri ücretleri depolama ve tooa depolama hesabına tanılama gönderdiğinizde, işlemler ve ne zaman günlük analizi depolama hesabınızdan hello veri okuyan için sizden ücret kesilir.
>
>

Bkz: [olayları için IIS ve tablo depolama alanı için kullanım blob depolama](log-analytics-azure-storage-iis-table.md) toolearn günlük analizi Bu günlükler nasıl toplayabilirsiniz hakkında daha fazla bilgi.

## <a name="connectors-for-azure-services"></a>Azure Hizmetleri için bağlayıcılar

Application Insights toobe tooLog Analytics gönderilen tarafından toplanan verileri sağlayan Application Insights için bir bağlayıcı yoktur.

Merhaba hakkında daha fazla bilgi [Application Insights Bağlayıcısı](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/).

## <a name="scripts-toocollect-and-post-data-toolog-analytics"></a>Komut dosyaları toocollect ve post veri tooLog analizi

Doğrudan yolu toosend günlüklerini ve ölçümleri tooLog sağlamaz, Azure Hizmetleri için kullanabileceğiniz bir Azure Otomasyonu betik toocollect Analytics günlük ve ölçümleri hello. Merhaba betik can sonra gönderme hello verileri tooLog analizi kullanarak hello [veri toplayıcı API](log-analytics-data-collector-api.md)

Hello Azure Şablon Galerisi sahip [Azure otomasyon kullanma örnekleri](https://azure.microsoft.com/en-us/resources/templates/?term=OMS) toocollect verilerden Hizmetleri ve tooLog Analytics gönderme.

## <a name="next-steps"></a>Sonraki adımlar

* [Olaylar için IIS ve tablo depolama için BLOB storage kullanma](log-analytics-azure-storage-iis-table.md) tooread hello günlükleri depolama veya IIS günlüklerini yazılı tooblob depolama tanılama tootable yazma Azure Hizmetleri için.
* [Çözümlerle](log-analytics-add-solutions.md) hello veri tooprovide fikirler.
* [Arama sorguları kullanmak](log-analytics-log-searches.md) tooanalyze hello veri.
