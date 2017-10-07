---
title: "OMS günlük analizi içinde aaaResponses tooalerts | Microsoft Docs"
description: "Günlük analizi uyarılarını OMS deponuzun önemli bilgileri tanımlamak ve önceden sorunları size bildiren veya Eylemler tooattempt toocorrect çağırma bunları.  Bu makalede nasıl toocreate bir uyarı kuralı ve ayrıntıları hello farklı eylemlerini yapabilecekleri açıklanmaktadır."
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
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a>Günlük analizi Eylemler tooalert kuralları ekleme
Zaman bir [uyarı günlük analizi oluşturulan](log-analytics-alerts.md), hello seçeneğiniz vardır [yapılandırma hello uyarı kuralı](log-analytics-alerts.md) tooperform bir veya daha fazla eylem.  Bu makalede, her tür yapılandırma üzerinde kullanılabilir hello farklı eylemler ve Ayrıntılar açıklanmaktadır.

| Eylem | Açıklama |
|:--|:--|
| [E-posta](#email-actions) | Merhaba uyarı tooone veya daha fazla alıcı hello ayrıntılarını içeren bir e-posta gönderin. |
| [Web kancası](#webhook-actions) | Bir dış işlem tek bir HTTP POST isteği üzerinden çağırır. |
| [Runbook](#runbook-actions) | Bir runbook, Azure Automation'da başlatın. |


## <a name="email-actions"></a>E-posta Eylemler
E-posta Eylemler hello uyarı tooone veya daha fazla alıcı hello ayrıntılarını içeren bir e-posta gönderin.  Merhaba konu hello posta belirtebilirsiniz, ancak buna ait günlük analizi tarafından oluşturulan standart bir biçim içeriktir.  Merhaba günlük araması tarafından döndürülen tooten kayıtları yukarı toplama toodetails hello uyarı hello adı gibi özet bilgileri içerir.  Bunu ayrıca bir bağlantı tooa günlük arama hello tüm kayıt kümesini Bu sorgudan döndürülecek günlük analizi içerir.   Merhaba gönderen hello posta *Microsoft Operations Management Suite ekibi &lt; noreply@oms.microsoft.com &gt;* . 

E-posta eylemleri aşağıdaki tablonun hello hello özelliklerinde gerektirir.

| Özellik | Açıklama |
|:--- |:--- |
| Konu |Merhaba e-postayla konu.  Merhaba hello posta gövdesini değiştiremezsiniz. |
| Alıcıları |Tüm e-posta alıcıları adresleri.  Noktalı virgül (;) birden fazla adres sonra ayrı hello adresleri belirtirseniz. |


## <a name="webhook-actions"></a>Web kancası eylemleri

Web kancası eylemleri tooinvoke bir dış işlem tek bir HTTP POST isteği üzerinden izin verin.  çağrılan hello Hizmet Web kancalarını destekleyen ve tüm yükü nasıl kullanacağınızı belirleyin aldığı.  Ayrıca hello isteği bir biçimde API anlar bu hello olduğu sürece, özellikle Web kancalarını desteklemeyen bir REST API'si çağırabilirsiniz.  Bir Web kancası yanıt tooan uyarıda kullanma örnekleri bir ileti gönderiyorsunuz [Slack'e](http://slack.com) veya bir olay oluşturma [PagerDuty](http://pagerduty.com/).  Bir Web kancası toocall kayma bir uyarı kuralı oluşturma izlenecek tam yol şu adresten edinilebilir [Kancalarını günlük analizi uyarılar](log-analytics-alerts-webhooks.md).

Web kancası eylemleri aşağıdaki tablonun hello hello özelliklerinde gerektirir.

| Özellik | Açıklama |
|:--- |:--- |
| Web kancası URL'si |Merhaba Web kancası URL'si Hello. |
| Özel JSON yükü |Özel yük toosend hello Web kancası ile.  Ayrıntılar için aşağıya bakın. |


Web kancası URL ekleme ve toohello dış hizmet hello veriler JSON biçimlendirilmiş bir yükü gönderilir.  Varsayılan olarak, aşağıdaki tablonun hello hello değerleri hello yükü içerir.  Bu yük kendi özel bir tane ile tooreplace seçebilirsiniz.  Bu durumda, hello tablosundaki hello değişkenler her hello parametreleri tooinclude değerlerine özel yükünüzü kullanabilirsiniz.

| Parametre | Değişken | Açıklama |
|:--- |:--- |:--- |
| AlertRuleName |#alertrulename |Merhaba uyarı kuralının adı. |
| AlertThresholdOperator |#thresholdoperator |Merhaba uyarı kuralı için eşik işleci.  *Büyük* veya *değerinden*. |
| AlertThresholdValue |#thresholdvalue |Merhaba uyarı kuralı için eşik değer. |
| LinkToSearchResults |#linktosearchresults |Merhaba uyarı oluşturulan hello sorgudan hello kayıtları döndüren tooLog Analytics günlük arama bağlayın. |
| ResultCount |#searchresultcount |Merhaba arama sonuçlarında kayıt sayısı. |
| SearchIntervalEndtimeUtc |#searchintervalendtimeutc |Bitiş saati UTC biçiminde hello sorgu için. |
| SearchIntervalInSeconds |#searchinterval |Merhaba uyarı kuralı için zaman penceresi. |
| SearchIntervalStartTimeUtc |#searchintervalstarttimeutc |UTC biçiminde hello sorgunun süresi başlatın. |
| SearchQuery |#searchquery |Merhaba uyarı kuralı tarafından kullanılan günlük arama sorgusu. |
| SearchResults |Aşağıya bakın |JSON biçiminde hello sorgu tarafından döndürülen kaydeder.  Sınırlı toohello ilk 5.000 kaydeder. |
| Workspaceıd |#workspaceid |OMS çalışma alanı kimliği. |

Örneğin, adlı tek bir parametre içeren özel yükü aşağıdaki hello belirtebilir *metin*.  Bu Web kancası çağırır hello hizmet, bu parametre bekleniyor.

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

Bu örnek yükü hello olduğunda aşağıdaki gibi toosomething toohello Web kancası gönderilen çözümlemek.

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

özel bir yükü tooinclude arama sonuçlarında en üst düzey özellik hello json yükü olarak satırı aşağıdaki hello ekleyin.  

    "IncludeSearchResults":true

Örneğin, toocreate yalnızca hello uyarı adı ve hello arama sonuçlarını içeren özel bir yükü, aşağıdaki hello kullanabilirsiniz. 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


Bir uyarı kuralı, bir dış hizmeti ile bir Web kancası toostart oluşturma tam bir örnek size yol [OMS günlük analizi toosend ileti tooSlack uyarı Web kancası eylem oluşturma](log-analytics-alerts-webhooks.md).

## <a name="runbook-actions"></a>Runbook eylemleri
Runbook eylemleri, Azure Automation'da bir runbook başlatın.  İçinde bu tür eylem toouse sipariş, hello olmalıdır [Otomasyon çözümünü](log-analytics-add-solutions.md) yüklenir ve OMS çalışma alanınızda yapılandırılır.  Merhaba Otomasyon çözümünü yapılandırılmış hello Otomasyon hesabı hello runbook'lar arasından seçim yapabilirsiniz.

Runbook eylemleri aşağıdaki tablonun hello hello özelliklerinde gerektirir.

| Özellik | Açıklama |
|:--- |:---|
| Runbook | Runbook bir uyarı oluşturulduğunda toostart istiyor. |
| Üzerinde çalışır | Belirtin **Azure** toorun hello runbook hello bulutta.  Belirtin **karma çalışanı** toorun hello runbook ile bir aracı üzerinde [karma Runbook çalışanı](../automation/automation-hybrid-runbook-worker.md ) yüklü.  |

Runbook eylemleri başlatmak runbook hello kullanarak bir [Web kancası](../automation/automation-webhooks.md).  Merhaba uyarı kuralı oluşturduğunuzda, yeni bir Web kancası hello runbook için hello adıyla otomatik olarak oluşturacağı **OMS uyarı düzeltme** bir GUID ile birlikte.  

Doğrudan hello runbook'un herhangi bir parametre doldurmak, ancak hello [$WebhookData parametresi](../automation/automation-webhooks.md) hello hello oluşturulduğu hello günlük arama sonuçlarını da dahil olmak üzere hello uyarı ayrıntılarını içerir.  Merhaba runbook toodefine gerekir **$WebhookData** bir parametre olarak hello uyarı özelliklerini tooaccess hello.  Merhaba uyarı verileri adlı tek bir özellik json biçiminde kullanılabilir **SearchResults** hello içinde **RequestBody** özelliği **$WebhookData**.  Bu, aşağıdaki tablonun hello hello özellikleriyle gerekir.

| Node | Açıklama |
|:--- |:--- |
| id |Yol ve hello GUİD'si arayın. |
| __metadata |Merhaba uyarı dahil olmak üzere hello kayıt sayısını ve hello arama sonuçlarının durumu hakkındaki bilgileri. |
| değer |Ayrı giriş hello arama sonuçlarında her kayıt için.  Merhaba girdisinin Hello ayrıntıları hello özellikleri ve değerleri hello kaydının eşleşir. |

Örneğin, hello aşağıdaki runbook hello günlük araması tarafından döndürülen hello kayıtları ayıklayın ve hello her kayıt türüne göre farklı özelliklerini atayın.  Bu hello runbook başlatır dönüştürerek Not **RequestBody** , BT ile PowerShell nesne olarak çalışılabilecek biçimde json öğesinden.

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
- Öğrenin nasıl toowrite [Azure automation'daki runbook'lar](https://azure.microsoft.com/documentation/services/automation) tooremediate sorunları uyarıları ile tanımlanır.
