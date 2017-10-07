---
title: "aaaStream Azure tanılama günlükleri tooan olay hub'ları Namespace | Microsoft Docs"
description: "Nasıl tooan olay hub'ları ad toostream Azure tanılama günlüklerini öğrenin."
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
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: 00092ea8f3fe4fa1476e3a697bf1e8645dd21e6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-azure-diagnostic-logs-tooan-event-hubs-namespace"></a>Azure tanılama günlükleri tooan olay hub'ları Namespace akışı
**[Azure tanılama günlüklerini](monitoring-overview-of-diagnostic-logs.md)**  içinde hello hello Portal içinde yerleşik "TooEvent hub'ları Dışarı Aktar" seçeneğini kullanarak gerçek zamanlı tooany uygulama yakın gönderilebilen ya da hizmet veri yolu kural kimliği'hello Azure PowerShell aracılığıyla tanılama ayarında hello etkinleştirerek Cmdlet'lerini veya Azure CLI.

## <a name="what-you-can-do-with-diagnostics-logs-and-event-hubs"></a>Tanılama günlüklerini ve olay hub'ları ile yapabilecekleriniz
Yetenek akış için tanılama günlükleri hello kullanabilir birkaç yollar şunlardır:

* **Akış günlükleri too3rd taraf günlüğe kaydetme ve telemetri sistemleri** – zaman içinde olay hub'ları akış hello mekanizması toopipe tanılama günlüklerinize toothird taraf Sıem'lerden duruma ve oturum analiz çözümleri.
* **Hizmet durumu "etkin yolunuzda" veri tooPowerBI akış tarafından görüntülemek** – olay hub'ı kullanarak, akış analizi ve Powerbı, Azure hizmetlerinizi toonear gerçek zamanlı Öngörüler tanılama verilerinizi kolayca dönüştürebilirsiniz. [Bu belge makalesi nasıl tooset Event Hubs, Yukarı Akış Analizi ile verileri işlemek ve Powerbı çıkış olarak kullanmak iyi bir genel bakış sağlayan](../stream-analytics/stream-analytics-power-bi-dashboard.md). Aşağıda, tanılama günlükleri ile ayarlanan için birkaç ipucu verilmiştir:
  
  * Merhaba portal hello seçeneğinde denetlemek veya tooselect hello event hub'ında ile başlayan hello adlı ad alanı hello istediğiniz şekilde PowerShell aracılığıyla etkinleştirmek bir event hub'tanılama günlükleri kategorisi için otomatik olarak oluşturulan **ınsights**.
  * SQL koddan hello olan örnek Stream Analytics sorgu tooparse tooa Powerbı tablodaki tüm hello günlük verilerini kullanabilirsiniz:

    ```sql
    SELECT
    records.ArrayValue.[Properties you want tootrack]
    INTO
    [OutputSourceName – hello PowerBI source]
    FROM
    [InputSourceName] AS e
    CROSS APPLY GetArrayElements(e.records) AS records
    ```

* **Bir özel telemetri ve günlüğe kaydetme platformu yapı** – özel olarak geliştirilmiş telemetri platform zaten varsa veya olan yalnızca bir hello yüksek düzeyde ölçeklenebilir yayımlama-abonelik oluşturma hakkında olay hub'ları yapısını tooflexibly verir düşünüyorum alma tanılama günlüğe kaydeder. [Bir küresel ölçekteki telemetri Platform dan Rosanova'nın Kılavuzu toousing olay hub'ları bkz](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).

## <a name="enable-streaming-of-diagnostic-logs"></a>Tanılama günlüklerini akışı etkinleştir
Tanılama günlüklerini hello portalı yoluyla programlı olarak akış veya hello kullanarak etkinleştirebilirsiniz [Azure İzleyici REST API'lerini](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings). Her iki durumda da, oluşturduğunuz bir tanılama ayarını belirttiğiniz bir olay hub'ları ad alanı ve hello günlük kategorileri ve toosend toohello ad alanında istediğiniz ölçümleri. Bir olay hub'ı etkinleştirmeniz her günlük kategori için hello ad alanı oluşturulur. Bir tanılama **günlük kategori** kaynak toplayabilir günlük türüdür.

> [!WARNING]
> Etkinleştirme ve işlem kaynakları (örneğin, VM'ler veya Service Fabric) tanılama günlükleri akış [adımları farklı bir dizi gerektirir](../event-hubs/event-hubs-streaming-azure-diags-data.md).
> 
> 

ad alanı toobe sahip olmayan Hello hizmet veri yolu veya olay hub'ları uygun RBAC erişim tooboth abonelikleri hello ayarı yapılandıran hello kullanıcının sahip olduğu sürece günlükleri yayma hello kaynak aynı abonelik hello.

## <a name="stream-diagnostic-logs-using-hello-portal"></a>Merhaba portalı kullanarak akış tanılama günlükleri
1. Merhaba portalında tooAzure İzleyici gidin ve tıklayın **tanılama ayarları**

    ![Azure İzleyicisi İzleme bölümü](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-blade.png)

2. İsteğe bağlı olarak kaynak grubu veya kaynak türü tarafından hello listesini filtrelemek ve tooset tanılama ayarını istediğiniz hello kaynakta'i tıklatın.

3. Hiçbir ayar seçmiş olduğunuz hello kaynakta mevcut, istendiğinde toocreate bir ayar demektir. "Tanılamayı açın."'i tıklatın

   ![Tanılama ayarını - ayar Ekle](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-none.png)

   Merhaba kaynakta mevcut ayarları varsa, bu kaynak üzerinde zaten yapılandırılmış ayarları listesini görürsünüz. "Tanılama ayarını Ekle" yi tıklatın.

   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-multiple.png)

3. Ayarı, bir ad verin ve hello kutuyu **tooan event hub'ı akış**, bir olay hub'ları ad alanı seçin.
   
   ![Tanılama ayarını ayarlar varolan - Ekle](media/monitoring-stream-diagnostic-logs-to-event-hubs/diagnostic-settings-configure.png)
    
   Merhaba seçili ad alanı burada hello olay hub'ı (Bu akış tanılama günlükleri, ilk kez kullanıyorsanız) oluşturulur veya çok akışı olacaktır (olup olmadığını zaten o günlük kategori toothis ad akış kaynakları), ve hello İlkesi hello tanımlar Akış mekanizması hello izinlerine sahip değil. Bugün, tooan akış olay hub'ı yönetme, gönderme ve dinleme izinleri gerektirir. Oluşturun veya olay hub'ları ad alanı paylaşılan erişim ilkeleri hello portalında Merhaba yapılandırma sekmesi altında ad alanınız için değiştirin. tooupdate Bu tanılama ayarlardan biri, hello istemci hello olay hub'ları yetkilendirme kuralı hello ListKey izninizin olması gerekir.

4. **Kaydet** düğmesine tıklayın.

Birkaç dakika sonra bu kaynak için ayarları listenizden hello yeni ayar görünür ve yeni olay verilerini oluşturulan hemen tanılama günlüklerini toothat depolama hesabı akışa alınır.

### <a name="via-powershell-cmdlets"></a>PowerShell cmdlet'leri
Merhaba akış tooenable [Azure PowerShell cmdlet'leri](insights-powershell-samples.md), hello kullanabilirsiniz `Set-AzureRmDiagnosticSetting` Bu parametreler cmdlet'iyle:

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource ID] -ServiceBusRuleId [your Service Bus rule ID] -Enabled $true
```

Merhaba Service Bus kural kimliği olduğundan bu biçiminde bir dize: `{Service Bus resource ID}/authorizationrules/{key name}`, örneğin, `/subscriptions/{subscription ID}/resourceGroups/Default-ServiceBus-WestUS/providers/Microsoft.ServiceBus/namespaces/{Service Bus namespace}/authorizationrules/RootManageSharedAccessKey`.

### <a name="via-azure-cli"></a>Azure CLI
Merhaba akış tooenable [Azure CLI](insights-cli-samples.md), hello kullanabilirsiniz `insights diagnostic set` komut şöyle:

```azurecli
azure insights diagnostic set --resourceId <resourceID> --serviceBusRuleId <serviceBusRuleID> --enabled true
```

Aynı hizmet veri yolu kural kimliği için PowerShell Cmdlet hello için açıklandığı gibi biçimi hello kullanın.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>Olay hub'ları hello günlük verilerini nasıl kullanabilir?
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
| kayıtları |Bu yük tüm günlük olaylar dizisi. |
| time |Merhaba olay gerçekleştiği zaman. |
| category |Bu olay günlüğü kategori. |
| resourceId |Bu olayı oluşturan hello kaynağının kaynak kimliği. |
| operationName |Merhaba işlemin adı. |
| düzeyi |İsteğe bağlı. Merhaba günlük olay düzeyini gösterir. |
| properties |Merhaba olay özellikleri. |

TooEvent hub akış destekleyen tüm kaynak sağlayıcılarının bir listesini görüntüleyebileceğiniz [burada](monitoring-overview-of-diagnostic-logs.md).

## <a name="stream-data-from-compute-resources"></a>İşlem kaynaklardan veri akışı
Ayrıca hello Windows Azure Tanılama aracı kullanarak işlem kaynaklarını tanılama günlükleri akışını sağlayabilirsiniz. [Bu makaleye bakın](../event-hubs/event-hubs-streaming-azure-diags-data.md) nasıl tooset o yukarı.

## <a name="next-steps"></a>Sonraki adımlar
* [Azure tanılama günlükleri hakkında daha fazla bilgi](monitoring-overview-of-diagnostic-logs.md)
* [Event Hubs kullanmaya başlayın](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

