---
title: "Azure ölçüm uyarılar hakkında aaaConfigure kancalarını | Microsoft Docs"
description: "Azure uyarıları tooother Azure olmayan sistemleri yeniden yönlendir."
author: johnkemnetz
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 8b3ae540-1d19-4f3d-a635-376042f8a5bb
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: johnkem
ms.openlocfilehash: bc4153ccdcff41c5b9d3c081e59a1bf260d8a283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-webhook-on-an-azure-metric-alert"></a>Bir Web kancası Azure ölçüm uyarıyı yapılandırın
Web kancası tooroute Azure izin uyarı bildirim tooother sistemleri işlem sonrası ya da özel eylemler için. Bir uyarı tooroute üzerinde bir Web kancası kullanabilirsiniz, SMS gönder tooservices oturum hatalar, sohbet ve mesajlaşma Servisleri üzerinden takım bildirmek veya herhangi bir sayıda diğer eylemleri yapın. Bu makalede nasıl tooset bir Web kancası Azure ölçüm uyarı ve hello HTTP POST tooa Web kancası için hangi hello yükü gibi görünüyor. Hello kurulumu ve bir Azure etkinlik günlüğü uyarı (uyarı) olayları için şema hakkında bilgiler için [bunun yerine bu sayfaya bakın](insights-auditlog-to-webhook-email.md).

HTTP POST hello uyarı içeriği JSON biçiminde Azure uyarıları şeması tanımlanan tooa Web kancası hello uyarı oluştururken sağladığınız URI aşağıda. Bu URI geçerli bir HTTP veya HTTPS uç noktası olması gerekir. Bir uyarı etkinleştirildiğinde azure istek başına bir giriş gönderir.

## <a name="configuring-webhooks-via-hello-portal"></a>Web kancası hello Portalı aracılığıyla yapılandırma
Ekleyebilir veya hello'ndaki hello oluştur/güncelleştir uyarıları ekranında URI hello Web kancası güncelleştirme [portal](https://portal.azure.com/).

![Bir uyarı kuralı Ekle](./media/insights-webhooks-alerts/Alertwebhook.png)

Bir uyarı toopost tooa Web kancası URI de yapılandırabilirsiniz hello kullanarak [Azure PowerShell cmdlet'leri](insights-powershell-samples.md#create-metric-alerts), [platformlar arası CLI](insights-cli-samples.md#work-with-alerts), veya [Azure İzleyici REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).

## <a name="authenticating-hello-webhook"></a>Merhaba Web kancası kimlik doğrulaması
Merhaba Web kancası belirteci tabanlı bir yetkilendirme kullanarak kimlik doğrulaması yapabilir. Merhaba Web kancası URI bir belirteç Kimliğiyle ör kaydedilir. `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`

## <a name="payload-schema"></a>Yükü şeması
Merhaba POST işlemine JSON yükü ve ölçüm tabanlı tüm uyarılar için şema aşağıdaki hello içerir.

```JSON
{
"status": "Activated",
"context": {
            "timestamp": "2015-08-14T22:26:41.9975398Z",
            "id": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.insights/alertrules/ruleName1",
            "name": "ruleName1",
            "description": "some description",
            "conditionType": "Metric",
            "condition": {
                        "metricName": "Requests",
                        "metricUnit": "Count",
                        "metricValue": "10",
                        "threshold": "10",
                        "windowSize": "15",
                        "timeAggregation": "Average",
                        "operator": "GreaterThanOrEqual"
                },
            "subscriptionId": "s1",
            "resourceGroupName": "useast",                                
            "resourceName": "mysite1",
            "resourceType": "microsoft.foo/sites",
            "resourceId": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1",
            "resourceRegion": "centralus",
            "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1"
},
"properties": {
              "key1": "value1",
              "key2": "value2"
              }
}
```


| Alan | Zorunlu | Sabit değer kümesi | Notlar |
|:--- |:--- |:--- |:--- |
| durum |E |"Etkin", "Çözülmüş" |Merhaba koşullara dışına hello uyarı ayarladığınız durumu. |
| bağlam |E | |Merhaba uyarı bağlamı. |
| timestamp |E | |hangi Merhaba uyarıyı tetikleyen hello süre. |
| id |E | |Her uyarı kuralı benzersiz bir kimliği var. |
| ad |E | |Merhaba uyarı adı. |
| Açıklama |E | |Merhaba uyarı açıklaması. |
| Koşul türü |E |"Ölçüm", "Olay" |Uyarı iki türleri desteklenir. Ölçüm bir koşula göre ve diğer temel alınarak hello etkinlik günlüğü olayda hello. Merhaba uyarı ölçüm veya olay temel alan, bu değer toocheck kullanın. |
| Koşul |E | |Merhaba belirli alanları toocheck hello koşul türü üzerinde temel. |
| metricName |Ölçüm uyarıları | |hangi hello kuralı tanımlayan hello ölçüm Hello adını izler. |
| metricUnit |Ölçüm uyarıları |"Bayt sayısı", "BytesPerSecond", "Count", "CountPerSecond", "Yüzde", "Saniye" |Merhaba ölçümünde izin hello birimi. [Değerleri burada listelenen izin verilen](https://msdn.microsoft.com/library/microsoft.azure.insights.models.unit.aspx). |
| metricValue |Ölçüm uyarıları | |Merhaba hello uyarıya neden hello ölçümün gerçek değer. |
| Eşik |Ölçüm uyarıları | |Merhaba eşik değeri hangi hello uyarı etkinleştirilir. |
| pencereboyutu |Ölçüm uyarıları | |Merhaba, süreyi hello eşiğine dayalı kullanılan toomonitor uyarı etkinliktir. 5 dakika ile 1 gün arasında olmalıdır. ISO 8601 süre biçimi. |
| timeAggregation |Ölçüm uyarıları |"Ortalama", "Son", "En", "Minimum", "None", "Toplam" |Toplanan hello veri zaman içinde nasıl birleştirilmelidir. Ortalama Hello varsayılan değerdir. [Değerleri burada listelenen izin verilen](https://msdn.microsoft.com/library/microsoft.azure.insights.models.aggregationtype.aspx). |
| işleci |Ölçüm uyarıları | |Merhaba işleci toocompare hello Geçerli ölçüm verileri toohello ayarlanan eşik kullanılır. |
| subscriptionId |E | |Azure abonelik kimliği |
| resourceGroupName |E | |Merhaba hello kaynak grubunun adı, kaynak etkilenmiş. |
| resourceName |E | |Kaynak adı hello kaynak etkilenmiş. |
| Kaynak türü |E | |Kaynak türü hello kaynak etkilenmiş. |
| resourceId |E | |Kaynak Kimliğini hello kaynak etkilenmiş. |
| resourceRegion |E | |Bölge veya hello konumunu kaynak etkilenmiş. |
| portalLink |E | |Doğrudan bağlantı toohello portal kaynak özet sayfası. |
| properties |N |İsteğe bağlı |Kümesi `<Key, Value>` çiftleri (yani `Dictionary<String, String>`) hello olay ayrıntılarını içerir. Merhaba özellikleri alan isteğe bağlıdır. Özel kullanıcı Arabirimi veya mantığı uygulama tabanlı iş akışlarında, kullanıcıların hello yükü geçirilen anahtar/değer girebilirsiniz. Merhaba alternatif bir yol toopass özel özellikler geri toohello Web kancası hello Web kancası URI kendisini (gibi sorgu parametrelerini) durumda |

> [!NOTE]
> Merhaba özellikleri alanı yalnızca ayarlanabilir hello kullanarak [Azure İzleyici REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).
>
>

## <a name="next-steps"></a>Sonraki adımlar
* Azure uyarıları ve Web kancalarını hello videoda hakkında daha fazla bilgi [Azure uyarılarla tümleştirmek PagerDuty](http://go.microsoft.com/fwlink/?LinkId=627080)
* [Azure Otomasyonu komut dosyaları (Runbook'lar) Azure uyarılar yürütme](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Bir Azure uyarıdan mantıksal uygulama toosend Twilio aracılığıyla bir SMS kullanın](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
* [Mantıksal uygulama toosend Azure uyarı Slack iletiden kullanın](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
* [Mantıksal uygulama toosend Azure bir uyarıdan ileti tooan Azure kuyruk kullanın](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)
