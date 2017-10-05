---
title: "OMS günlük analizi uyarılarını yanıtlarını | Microsoft Docs"
description: "Günlük analizi uyarılarını OMS deponuzun önemli bilgileri tanımlamak ve önceden sorunları size bildiren veya düzeltmenize girişiminde Eylemler çağırma.  Bu makalede, bir uyarı kuralı ve ayrıntıları yapabilecekleri farklı eylemler oluşturmayı açıklar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b8731e1fe48b7d809b113eb5273e3962542b8f34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-actions-to-alert-rules-in-log-analytics"></a>Günlük analizi uyarı kurallarında eylemleri ekleyin
Zaman bir [uyarı günlük analizi oluşturulan](log-analytics-alerts.md), seçeneğiniz vardır [uyarı kuralı yapılandırma](log-analytics-alerts.md) bir veya daha fazla eylemleri gerçekleştirmek için.  Bu makalede, her tür yapılandırma hakkında ayrıntılar ve kullanılabilir farklı eylemler açıklanmaktadır.

| Eylem | Açıklama |
|:--|:--|
| [E-posta](#email-actions) | Bir veya daha fazla alıcıya uyarı ayrıntılarını içeren bir e-posta gönderin. |
| [Web kancası](#webhook-actions) | Bir dış işlem tek bir HTTP POST isteği üzerinden çağırır. |
| [Runbook](#runbook-actions) | Bir runbook, Azure Automation'da başlatın. |


## <a name="email-actions"></a>E-posta Eylemler
E-posta Eylemler bir veya daha fazla alıcıya uyarı ayrıntılarını içeren bir e-posta gönderin.  Posta konusunu belirtebilirsiniz, ancak buna ait günlük analizi tarafından oluşturulan standart bir biçim içeriktir.  Uyarı günlüğü araması tarafından döndürülen en fazla on kayıt ayrıntılarını yanı sıra adı gibi özet bilgileri içerir.  Ayrıca, kayıt kümesinin tamamını Bu sorgudan döndürülecek günlük analizi günlük arama bağlantısını içerir.   Posta gönderen *Microsoft Operations Management Suite ekibi &lt; noreply@oms.microsoft.com &gt;* . 

E-posta eylemler özellikler aşağıdaki tabloda gerektirir.

| Özellik | Açıklama |
|:--- |:--- |
| Konu |E-postayla konu.  Posta gövdesini değiştiremezsiniz. |
| Alıcıları |Tüm e-posta alıcıları adresleri.  Birden fazla adres belirtirseniz, adreslerini noktalı virgül (;) ayırın. |


## <a name="webhook-actions"></a>Web kancası eylemleri

Web kancası eylemleri, bir dış işlem tek bir HTTP POST isteği üzerinden çağırma olanak tanır.  Çağrılan Hizmet Web kancalarını destekleyen ve tüm yükü nasıl kullanacağınızı belirleyin aldığı.  Ayrıca, istek API özelliğini algılayan bir biçimde olduğu sürece, özellikle Web kancalarını desteklemeyen bir REST API'si çağırabilirsiniz.  Bir Web kancası yanıt olarak bir uyarı kullanma örnekleri bir ileti gönderiyorsunuz [Slack'e](http://slack.com) veya bir olay oluşturma [PagerDuty](http://pagerduty.com/).  Kayma çağırmak için bir Web kancası ile bir uyarı kuralı oluşturma izlenecek tam yol şu adresten edinilebilir [Kancalarını günlük analizi uyarılar](log-analytics-alerts-webhooks.md).

Web kancası eylemleri özellikler aşağıdaki tabloda gerektirir.

| Özellik | Açıklama |
|:--- |:--- |
| Web kancası URL'si |Web kancası URL'si. |
| Özel JSON yükü |Web kancası ile göndermek için özel yükü.  Ayrıntılar için aşağıya bakın. |


Web kancası bir URL ve dış hizmete gönderilen veriler JSON biçimli bir yükü içerir.  Varsayılan olarak, aşağıdaki tabloda değerleri yükü içerir.  Bu yük özel bir kendi tarihle seçebilirsiniz.  Bu durumda, değişkenleri tabloda her parametre için değer özel yükünüzü dahil etmek için kullanabilirsiniz.

| Parametre | Değişken | Açıklama |
|:--- |:--- |:--- |
| AlertRuleName |#alertrulename |Uyarı kuralı adı. |
| AlertThresholdOperator |#thresholdoperator |Uyarı kuralı için eşik işleci.  *Büyük* veya *değerinden*. |
| AlertThresholdValue |#thresholdvalue |Uyarı kuralı için eşik değer. |
| LinkToSearchResults |#linktosearchresults |Günlük analizi günlük kayıtları uyarı oluşturulan sorgudan döndüren bir arama bağlayın. |
| ResultCount |#searchresultcount |Arama sonuçlarında kayıt sayısı. |
| SearchIntervalEndtimeUtc |#searchintervalendtimeutc |Bitiş saati UTC biçiminde bir sorgu için. |
| SearchIntervalInSeconds |#searchinterval |Zaman penceresi için uyarı kuralı. |
| SearchIntervalStartTimeUtc |#searchintervalstarttimeutc |Sorgu saati UTC biçiminde başlatın. |
| SearchQuery |#searchquery |Uyarı kuralı tarafından kullanılan günlük arama sorgusu. |
| SearchResults |Aşağıya bakın |JSON biçiminde sorgu tarafından döndürülen kaydeder.  5. 000'ilk kayıtları sınırlıdır. |
| Workspaceıd |#workspaceid |OMS çalışma alanı kimliği. |

Örneğin, adlı tek bir parametre içeren aşağıdaki özel yükü belirtebilir *metin*.  Bu Web kancası çağırır hizmet, bu parametre bekleniyor.

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

Bu örnek yükü için Web kancası gönderildiğinde aşağıdaki gibi bir şey çözümlemek.

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

Özel bir yükte arama sonuçlarında en üst düzey özelliği json yükü olarak aşağıdaki satırı ekleyin.  

    "IncludeSearchResults":true

Örneğin, yalnızca uyarı adı ve arama sonuçlarını içeren özel bir yükü oluşturmak için aşağıdakileri kullanabilirsiniz. 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


Dış bir hizmeti başlatmak için bir Web kancası ile bir uyarı kuralı oluşturma tam bir örnek size yol [Slack'e ileti göndermek için OMS günlük analizi uyarı Web kancası eylem oluşturma](log-analytics-alerts-webhooks.md).

## <a name="runbook-actions"></a>Runbook eylemleri
Runbook eylemleri, Azure Automation'da bir runbook başlatın.  Bu eylemin türünü kullanmak için bilmeniz gereken [Otomasyon çözümünü](log-analytics-add-solutions.md) yüklenir ve OMS çalışma alanınızda yapılandırılır.  Otomasyon çözümünü yapılandırılmış Otomasyon hesabında runbook'ları arasından seçim yapabilirsiniz.

Runbook eylemleri özellikler aşağıdaki tabloda gerektirir.

| Özellik | Açıklama |
|:--- |:---|
| Runbook | Bir uyarı oluşturulduğunda başlatmak istediğiniz Runbook. |
| Üzerinde çalışır | Belirtin **Azure** runbook bulutta çalıştırmak için.  Belirtin **karma çalışanı** runbook'u ile bir aracı çalıştırmayı [karma Runbook çalışanı](../automation/automation-hybrid-runbook-worker.md ) yüklü.  |

Runbook eylemleri başlatmak kullanarak runbook bir [Web kancası](../automation/automation-webhooks.md).  Uyarı kuralı oluşturduğunuzda, runbook için yeni bir Web kancası adı ile otomatik olarak oluşturacağı **OMS uyarı düzeltme** bir GUID ile birlikte.  

Runbook'un parametreleri doğrudan doldurulamıyor ancak [$WebhookData parametresi](../automation/automation-webhooks.md) oluşturulduğu günlük arama sonuçları dahil olmak üzere Uyarı ayrıntılarını içerir.  Runbook tanımlamanız gereken **$WebhookData** uyarı özelliklerine erişmek için bir parametre olarak.  Uyarı verileri json biçiminde adlı tek bir özellik bulunur **SearchResults** içinde **RequestBody** özelliği **$WebhookData**.  Bu, aşağıdaki tabloda özelliklere sahip olacaktır.

| Node | Açıklama |
|:--- |:--- |
| id |Yol ve arama GUID. |
| __metadata |Arama sonuçlarını durumunu ve kayıt sayısı dahil olmak üzere uyarı hakkında bilgi. |
| değer |Arama sonuçlarında her kayıt için ayrı girişi.  Giriş ayrıntılarını özellikleri ve kayıt değerleri ile eşleşir. |

Örneğin, aşağıdaki runbook, günlük araması tarafından döndürülen kayıtları Ayıkla ve her kayıt türüne göre farklı özellikler atayın.  Runbook dönüştürerek başlatır Not **RequestBody** , BT ile PowerShell nesne olarak çalışılabilecek biçimde json öğesinden.

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a>Sonraki adımlar
- İzlenecek yollar için tamamlamak [bir webook yapılandırma](log-analytics-alerts-webhooks.md) bir uyarı kuralı ile.  
- Nasıl yazılacağını öğrenmek [Azure automation'daki runbook'lar](https://azure.microsoft.com/documentation/services/automation) uyarılar tarafından tanımlanan sorunları düzeltmek için.