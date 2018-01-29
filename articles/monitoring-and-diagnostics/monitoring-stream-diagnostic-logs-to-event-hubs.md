---
title: "Olay hub'ına Azure tanılama günlükleri akış | Microsoft Docs"
description: "Bir olay hub'ına Azure tanılama günlüklerini akış öğrenin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 42bc4845-c564-4568-b72d-0614591ebd80
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/22/2017
ms.author: johnkem
ms.openlocfilehash: bcb9fcb2371217e7082d96ddbba4a095e6d9a00f
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/22/2017
---
# <a name="stream-azure-diagnostic-logs-to-an-event-hub"></a>Bir olay hub'ına akış Azure tanılama günlükleri
**[Azure tanılama günlüklerini](monitoring-overview-of-diagnostic-logs.md)**  portalında veya Azure aracılığıyla tanılama ayarında olay hub'ı yetkilendirme kuralı kimliği etkinleştirerek yerleşik "Dışarı aktarmak için Event Hubs" seçeneğini kullanarak herhangi bir uygulama için yakın gerçek zamanlı akış PowerShell cmdlet'lerini veya Azure CLI.

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a>Tanılama günlüklerini ve olay hub'ları ile yapabilecekleriniz
Tanılama günlüklerini akış özelliği kullanabilir birkaç yollar şunlardır:

* **Akış günlükleri için 3. taraf günlüğe kaydetme ve telemetri sistemi** – tüm tanılama günlüklerinize kanal günlük verileri bir üçüncü taraf SIEM veya günlük analizi aracı için tek bir olay hub'ına akış.
* **Powerbı "etkin yolunuzda" veri akışı tarafından hizmet durumu görüntülemek** – olay hub'ı kullanarak, akış analizi ve Powerbı, kolayca dönüştürme tanılama verilerinizi Azure hizmetlerinizi üzerinde gerçek zamanlı Öngörüler yakınında için. [Bu belge makalesi nasıl olay hub'ları ayarlamak, akış Analizi ile verileri işlemek ve Powerbı çıkış olarak kullanmak iyi bir genel bakış sağlayan](../stream-analytics/stream-analytics-power-bi-dashboard.md). Aşağıda, tanılama günlükleri ile ayarlanan için birkaç ipucu verilmiştir:
  
  * Portal seçeneğinde denetlemek veya olay hub'ı ile başlayan ad alanında adıyla seçmek istediğiniz şekilde PowerShell aracılığıyla etkinleştirmek bir event hub'tanılama günlükleri kategorisi için otomatik olarak oluşturulan **ınsights -**.
  * Aşağıdaki SQL kodunu tüm günlük verileri Powerbı tabloya ayrıştırmak için kullanabileceğiniz bir örnek Stream Analytics sorgu aşağıdaki gibidir:

    ```sql
    SELECT
    records.ArrayValue.[Properties you want to track]
    INTO
    [OutputSourceName – the PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* **Özel telemetri ve günlüğe kaydetme platform derleme** – yayımlama-abone yapısı bir özel olarak geliştirilmiş telemetri platform veya olan biri, yüksek düzeyde ölçeklenebilir oluşturma hakkında düşünüyorum yalnızca zaten varsa Event Hubs, esnek tanılama günlüklerini alma olanak sağlar. [Olay hub'ları bir küresel ölçekteki telemetri platform burada kullanmanın Dan Rosanova'nın Kılavuzu'na bakın](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="enable-streaming-of-diagnostic-logs"></a>Tanılama günlüklerini akışı etkinleştir
Tanılama günlüklerini portalı yoluyla programlı olarak akış veya kullanarak etkinleştirebilirsiniz [Azure İzleyici REST API'lerini](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings). Her iki durumda da, oluşturduğunuz bir tanılama ayarını bir olay hub'ları ad alanı ve günlük kategorileri ve ölçümleri istediğiniz ad alanına göndermek için belirttiğiniz içinde. Bir olay hub'ı etkinleştirmeniz her günlük kategori için ad alanı oluşturulur. Bir tanılama **günlük kategori** kaynak toplayabilir günlük türüdür.

> [!WARNING]
> Etkinleştirme ve işlem kaynakları (örneğin, VM'ler veya Service Fabric) tanılama günlükleri akış [adımları farklı bir dizi gerektirir](../event-hubs/event-hubs-streaming-azure-diags-data.md).
> 
> 

Her iki aboneliğin uygun RBAC erişimi ayarı yapılandıran kullanıcının sahip olduğu sürece günlükleri yayma kaynak ile aynı abonelikte olması olay hub'ları ad alanı yok.

## <a name="stream-diagnostic-logs-using-the-portal"></a>Portalı kullanarak akış tanılama günlükleri
1. Portal, Azure izleyicisine gidin ve tıklayın **tanılama ayarları**

    ![Azure İzleyicisi İzleme bölümü](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. İsteğe bağlı olarak kaynak grubu veya kaynak türü listeyi filtrelemek sonra tanılama ayarını ayarlamak istediğiniz kaynak'ı tıklatın.

3. Hiçbir ayar kaynağı varsa, sizden istenir bir ayar oluşturmak için seçtiğiniz. "Tanılamayı açın."'i tıklatın

   ![Tanılama ayarını - ayar Ekle](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   Kaynak üzerinde var olan ayarları varsa, bu kaynak üzerinde zaten yapılandırılmış ayarları listesini görürsünüz. "Tanılama ayarını Ekle" yi tıklatın.

   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. Ayarı, bir ad verin ve için kutuyu **bir olay hub'ına akış**, bir olay hub'ları ad alanı seçin.
   
   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   Seçili ad alanı, olay hub'ı (Bu, ilk zaman akış tanılama günlükleri varsa) oluşturulur veya için akışı olacaktır (olup olmadığını zaten bu ad alanına günlük kategoriye akış kaynakları), ve izinleri ilkeyi tanımlar, Akış mekanizması vardır. Bugün, olay hub'ına akış yönetme, gönderme ve dinleme izinleri gerektirir. Oluşturun veya olay hub'ları ad alanı paylaşılan erişim ilkeleri Yapılandır sekmesi altında portalında ad alanınız için değiştirin. Bu tanılama ayarları birini güncelleştirmek için istemci olay hub'ları yetkilendirme kuralı ListKey izni olmalıdır. Ayrıca isteğe bağlı olarak, bir olay hub'ı adı belirtebilirsiniz. Bir olay hub'ı adı belirtirseniz, günlükleri, olay hub'ına yerine her günlük kategori yeni oluşturulan olay hub'ına yönlendirilir.

4. **Kaydet**’e tıklayın.

Birkaç dakika sonra yeni ayar, bu kaynak için ayarları listesi görüntülenir ve yeni olay verilerini oluşturulan hemen tanılama günlükleri, olay hub'ına akışa alınır.

### <a name="via-powershell-cmdlets"></a>PowerShell cmdlet'leri
Aracılığıyla akışını etkinleştirmek için [Azure PowerShell cmdlet'leri](insights-powershell-samples.md), kullanabileceğiniz `Set-AzureRmDiagnosticSetting` Bu parametreler cmdlet'iyle:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

Hizmet veri yolu kural kimliği bu biçiminde bir dizedir: `{Service Bus resource ID}/authorizationrules/{key name}`, örneğin, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`. PowerShell ile belirli bir olay hub'ı adı şu anda seçemezsiniz.

### <a name="via-azure-cli"></a>Azure CLI
Aracılığıyla akışını etkinleştirmek için [Azure CLI](insights-cli-samples.md), kullanabileceğiniz `insights diagnostic set` komut şöyle:

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

Aynı biçimde Service Bus kural kimliği için PowerShell cmdlet'i için açıklandığı gibi kullanın. Şu anda Azure CLI belirli bir olay hub'ı adıyla seçemezsiniz.

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a>Olay hub'ları günlük verilerini nasıl kullanabilir?
Olay hub'ları örnek çıktı verilerini şöyledir:

```json
{
    "records": [
        {
            "time": "2016-07-15T18:00:22.6235064Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330013509921957/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Error",
            "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T17:58:55.048482Z",
                "endTime": "2016-07-15T18:00:22.4109204Z",
                "status": "Failed",
                "code": "BadGateway",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330013509921957",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "29a9862f-969b-4c70-90c4-dfbdc814e413",
                    "clientTrackingId": "08587330013509921958"
                }
            }
        },
        {
            "time": "2016-07-15T18:01:15.7532989Z",
            "workflowId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA",
            "resourceId": "/SUBSCRIPTIONS/DF602C9C-7AA0-407D-A6FB-EB20C8BD1192/RESOURCEGROUPS/JOHNKEMTEST/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/JOHNKEMTESTLA/RUNS/08587330012106702630/ACTIONS/SEND_EMAIL",
            "category": "WorkflowRuntime",
            "level": "Information",
            "operationName": "Microsoft.Logic/workflows/workflowActionStarted",
            "properties": {
                "$schema": "2016-04-01-preview",
                "startTime": "2016-07-15T18:01:15.5828115Z",
                "status": "Running",
                "resource": {
                    "subscriptionId": "df602c9c-7aa0-407d-a6fb-eb20c8bd1192",
                    "resourceGroupName": "JohnKemTest",
                    "workflowId": "243aac67fe904cf195d4a28297803785",
                    "workflowName": "JohnKemTestLA",
                    "runId": "08587330012106702630",
                    "location": "westus",
                    "actionName": "Send_email"
                },
                "correlation": {
                    "actionTrackingId": "042fb72c-7bd4-439e-89eb-3cf4409d429e",
                    "clientTrackingId": "08587330012106702632"
                }
            }
        }
    ]
}
```

| Öğe adı | Açıklama |
| --- | --- |
| kayıt |Bu yük tüm günlük olaylar dizisi. |
| time |Olayın gerçekleştiği süre. |
| category |Bu olay günlüğü kategori. |
| resourceId |Bu olayı oluşturan kaynağının kaynak kimliği. |
| operationName |İşlemin adı. |
| düzey |İsteğe bağlı. Günlük olayı düzeyini gösterir. |
| properties |Olay Özellikleri. |

Event Hubs'a akış destekleyen tüm kaynak sağlayıcılarının bir listesini görüntüleyebileceğiniz [burada](monitoring-overview-of-diagnostic-logs.md).

## <a name="stream-data-from-compute-resources"></a>İşlem kaynaklardan veri akışı
Ayrıca, Windows Azure Diagnostics Aracısı'nı kullanarak işlem kaynaklarını tanılama günlükleri akışını sağlayabilirsiniz. [Bu makaleye bakın](../event-hubs/event-hubs-streaming-azure-diags-data.md) , nasıl ayarlanacağını için.

## <a name="next-steps"></a>Sonraki adımlar
* [Azure tanılama günlükleri hakkında daha fazla bilgi](monitoring-overview-of-diagnostic-logs.md)
* [Event Hubs kullanmaya başlayın](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

