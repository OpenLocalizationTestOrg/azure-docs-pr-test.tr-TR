---
title: "OMS günlük analizi aaaWebhook uyarı eylemi örnek | Microsoft Docs"
description: "Günlük analizi uyarısıdır yanıt tooa içinde çalıştırabilirsiniz hello eylemlerden birini bir * tooinvoke bir dış işlem üzerinden tek bir HTTP isteği sağlayan Web kancası *. Bu makalede bir Web kancası eylem kayma kullanarak günlük analizi uyarıda oluşturma örneği anlatılmaktadır."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a>Bir uyarı Web kancası eylem OMS günlük analizi toosend ileti tooSlack oluşturun
Yanıt tooa çalıştırabilirsiniz hello eylemlerden birini [günlük analizi uyarı](log-analytics-alerts.md) olan bir *Web kancası*, olanak sağlayan tooinvoke bir dış işlem üzerinden tek bir HTTP isteği.  Uyarılar ve Web kancalarını içinde ayrıntıları hakkında bilgi edinebilirsiniz [günlük analizi uyarıları](log-analytics-alerts.md)

Bu makalede, sizi bir ileti sistemi hizmeti olan kayma kullanarak günlük analizi uyarıda bir Web kancası eylem oluşturma örneği adım geçireceğiz.

> [!NOTE]
> Bu örnek Slack hesap toocomplete olması gerekir.  Ücretsiz bir hesap için kaydolabilirsiniz [slack.com](http://slack.com).
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a>1. adım - kayma içinde etkinleştir Web kancaları
1. Oturum açma sırasında tooSlack [slack.com](http://slack.com).
2. Bir kanal hello seçin **kanalları** hello sol bölmesindeki bölümünde.  Bu hello kanalıdır hello ileti gönderilir.  Merhaba varsayılan kanalları birini gibi seçebilirsiniz **genel** veya **rastgele**.  Bir üretim senaryosunda, büyük olasılıkla özel kanal gibi oluşturacak **criticalservicealerts**. <br>
   
   ![Slack kanallarında](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. Tıklatın **bir uygulama veya özel tümleştirme ekleme** tooopen hello uygulama dizini.
4. Tür *kancalarını* hello arama kutusuna ve ardından **gelen Web Kancalarını**. <br>
   
   ![Slack kanallarında](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. Tıklatın **yükleme** sonraki tooyour ekip adı.
6. Tıklatın **yapılandırması eklemek**.
7. Bu örnek için toouse oluşturacağız ve ardından select hello hello kanal **eklemek gelen Web Kancalarını tümleştirme**.  
8. Kopya hello **Web kancası URL'si**.  Bu hello uyarı yapılandırma yapıştırdığınız. <br>
   
    ![Slack kanallarında](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a>2. adım - günlük analizi uyarı kuralı oluştur
1. [Bir uyarı kuralı oluştur](log-analytics-alerts.md) ayarları aşağıdaki hello ile.
   * Sorgu:```    Type=Event EventLevelName=error ```
   * Bu uyarıyı denetleme her: 5 dakika
   * sonuçları Hello sayısıdır: 10'dan büyük
   * Bu zaman penceresi üzerinden: 60 dakika
   * Seçin **Evet** için **Web kancası** ve **Hayır** hello diğer eylemler.
2. Merhaba içine yapıştırma hello kayma URL **Web kancası URL'si** alan.
3. Çok olarak Hello seçeneğini**özel JSON yükünü dahil et**.
4. Kayma JSON'adlı bir parametre ile biçimlendirilmiş bir yükü bekliyor *metin*.  Bu oluşturduğu hello iletisinde görüntüleyecek hello metindir.  Bir veya daha fazla hello kullanarak hello uyarı parametrelerini kullanabilirsiniz  *#*  gibi aşağıdaki örneğine hello olduğu gibi simge.
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![Örnek JSON yükü](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. Tıklatın **kaydetmek** toosave hello uyarı kuralı.
6. Oluşturulan bir uyarı toobe yeterli bir süre bekleyin ve ardından kayma benzer toohello aşağıdaki olacağı bir ileti için denetleyin.
   
   ![Örnek Web kancası kayma içinde](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a>Web kancası yükü kayma için Gelişmiş
Gelen iletiler kayma ile kapsamlı bir şekilde özelleştirebilirsiniz. Daha fazla bilgi için bkz: [gelen Web Kancalarını](https://api.slack.com/incoming-webhooks) hello Slack Web sitesinde. Daha karmaşık bir yükü toocreate biçimlendirmeye sahip zengin bir ileti aşağıdadır:

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


Bu ileti Slack benzer toohello aşağıdakileri oluşturur.

![Kayma örnek iletisi](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a>Özet
Bu uyarı kuralı ile yerinde Hello ölçütleri karşılanıyorsa her zaman gönderilen ileti tooSlack gerekir.  

Bu yalnızca bir yanıt tooan uyarıda oluşturabileceğiniz bir eylem örneğidir.  Bir runbook'un Azure Otomasyon ya da bir e-posta eylem toosend başka bir dış hizmet, bir runbook eylemi toostart çağıran bir Web kancası eylemi posta tooyourself veya diğer alıcılar oluşturabilirsiniz.   

## <a name="next-steps"></a>Sonraki Adımlar
* Diğer hakkında bilgi edinin [uyarı günlük analizi Eylemler](log-analytics-alerts-actions.md) diğer Eylemler dahil olmak üzere.


