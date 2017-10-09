---
title: "Azure Data Lake Analytics için tanılama günlüklerini aaaViewing | Microsoft Docs"
description: "Nasıl toosetup ve erişim tanılama günlükleri için Azure Data Lake analytics anlama "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a>Azure Data Lake Analytics için tanılama günlüklerine erişme

Tanılama günlük toocollect veri erişimi denetim izleri sağlar. Bu günlükler gibi bilgileri sağlayın:

* Merhaba veri erişilen kullanıcıların listesi.
* Merhaba verileri ne sıklıkla erişilebilir.
* Ne kadar veri hello hesabında depolanır.

## <a name="enable-logging"></a>Günlü kaydını etkinleştir

1. Toohello üzerinde oturum [Azure portal](https://portal.azure.com).

2. Data Lake Analytics hesabınızı açın ve seçin **tanılama günlükleri** hello gelen __İzleyici__ bölümü. Ardından, __tanılamayı açın__.

    ![Tanılama toocollect denetim üzerinde açın ve günlükleri isteği](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. Gelen __tanılama ayarları__hello durum too__On__ ayarlamak ve günlüğe kaydetme seçeneklerini belirleyin.

    ![Tanılama toocollect denetim üzerinde açın ve istek günlükleri](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "tanılama günlüklerini etkinleştirme")

   * Ayarlama **durum** çok**üzerinde** tooenable tanılama günlük.

   * Üç farklı yolla toostore/işlem hello veri seçebilirsiniz.

     * Seçin __arşiv tooa depolama hesabı__ toostore bir Azure depolama hesabında günlüğe kaydeder. Tooarchive hello veri istiyorsanız bu seçeneği kullanın. Bu seçeneği seçerseniz, bir Azure depolama hesabı toosave hello günlüklerine sağlamanız gerekir.

     * Seçin **tooan olay hub'ı akış** toostream günlük veri tooan Azure olay hub'ı. Gerçek zamanlı gelen günlüklerini analiz bir aşağı akış işleme ardışık varsa bu seçeneği kullanın. Bu seçeneği belirlerseniz, hello Azure Event Hub'ın toouse istediğiniz hello ayrıntılarını sağlamanız gerekir.

     * Seçin __tooLog Analytics Gönder__ toosend hello veri toohello günlük analizi hizmeti. Günlüklerini analiz edin ve toouse günlük analizi toogather isterseniz bu seçeneği kullanın.
   * Tooget denetim günlüklerini veya istek günlüklerini ya da hem isteyip istemediğinizi belirtin.  İstek günlüğü her API isteği yakalar. Bir denetim günlüğü bu API isteğiyle tetiklenen tüm işlemleri kaydeder.

   * İçin __arşiv tooa depolama hesabı__, gün tooretain hello veri hello sayısını belirtin.

   * __Kaydet__ düğmesine tıklayın.

        > [!NOTE]
        > Ya da seçmelisiniz __arşiv tooa depolama hesabı__, __tooan olay hub'ı akış__ veya __tooLog Analytics Gönder__ hello tıklatmadan önce __kaydetmek__düğmesi.

Tanılama ayarları etkinleştirildiğinde, toohello döndürebilir __tanılama günlükleri__ dikey tooview hello günlükleri.

## <a name="view-logs"></a>Günlükleri görüntüle

### <a name="use-hello-data-lake-analytics-view"></a>Merhaba Data Lake Analytics görünümünü kullanın

1. , Data Lake Analytics hesabı dikey penceresinde altında **izleme**seçin **tanılama günlüklerini** ve ardından bir girişi toodisplay için günlüğe kaydeder.

    ![Görünüm tanılama günlük](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "tanılama günlükleri görüntüleme")

2. Merhaba günlükleri tarafından ayrılır **denetim günlüklerini** ve **isteği günlükleri**.

    ![günlük girişleri](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * İstek günlüklerini hello Data Lake Analytics hesabı üzerinde yapılan her API isteği yakalayın.
   * Denetim günlüklerini benzer toorequest günlüklerin ancak hello işlemleri çok daha ayrıntılı bir dökümünü sağlar. Örneğin, bir tek karşıya yükleme API çağrısının istek günlüğü, Denetim günlüğü "Ekle" işlemlerinde neden olabilir.

3. Merhaba tıklatın **karşıdan** oturum bir günlük girişi toodownload için bağlantı.

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a>Günlük verilerini içeren hello Azure depolama hesabı kullan

1. Günlüğe kaydetme için Data Lake Analytics ile ilişkili hello Azure depolama hesabı dikey açın ve ardından __BLOB'lar__. Merhaba **Blob hizmeti** iki kapsayıcı dikey penceresinde listelenir.

    ![Görünüm tanılama günlük](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "tanılama günlükleri görüntüleme")

   * Merhaba kapsayıcı **Öngörüler günlükleri denetim** hello denetim günlüklerini içerir.
   * Merhaba kapsayıcı **Öngörüler günlükleri istekleri** hello isteği günlükleri içerir.
2. Bu kapsayıcılara hello günlükleri yapı izlenerek hello altında depolanır:

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > Merhaba `##` hello yolundaki girişleri hello yıl, ay, gün ve hangi hello günlük oluşturulduğu saat. Data Lake Analytics bir dosya kadar her saat oluşturur `m=` her zaman değerini içeren `00`.

    Örnek olarak, hello tam yolunu tooan denetim günlüğü olabilir:

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    Benzer şekilde, hello tam yolunu tooa istek günlüğü olabilir:

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a>Günlük yapısı

Denetim hello ve yapılandırılmış bir JSON biçiminde günlüklerin isteyin.

### <a name="request-logs"></a>İstek günlükleri

Merhaba JSON biçimli istek günlüğünde örnek girişi İşte. Her bir blob olarak adlandırılan bir kök nesnesi vardır **kayıtları** günlük nesnelerinin bir dizisi içerir.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>İstek günlüğü şeması

| Ad | Tür | Açıklama |
| --- | --- | --- |
| time |Dize |Merhaba günlüğünün Hello zaman damgası (UTC) cinsinden |
| resourceId |Dize |işlemi sürdü hello kaynak Hello tanıtıcısı yerleştirin |
| category |Dize |Merhaba günlük kategorisi. Örneğin, **istekleri**. |
| operationName |Dize |Oturum hello işlemin adı. Örneğin, GetAggregatedJobHistory. |
| resultType |Dize |Merhaba işlemi, örneğin, 200 Hello durumu. |
| callerIpAddress |Dize |Merhaba istekte hello istemcinin Hello IP adresi |
| correlationId |Dize |Merhaba günlük Hello tanımlayıcısı. Bu değer, kullanılan toogroup bir dizi ilgili günlük girişlerini olabilir. |
| identity |Nesne |Merhaba günlük oluşturulan hello kimliği |
| properties |JSON |Ayrıntılar için Hello sonraki bölümüne (istek günlük özellikleri Şeması) bakın |

#### <a name="request-log-properties-schema"></a>İstek günlüğü özellikleri şeması

| Ad | Tür | Açıklama |
| --- | --- | --- |
| HttpMethod |Dize |Merhaba HTTP hello işlemi için kullanılan yöntem. Örneğin, alın. |
| Yol |Dize |Merhaba yolu hello işlem üzerinde gerçekleştirildi |
| RequestContentLength |Int |Merhaba HTTP isteğinin Hello içerik uzunluğu |
| ClientRequestId |Dize |Bu istek benzersiz olarak tanıtan hello tanımlayıcısı |
| StartTime |Dize |hangi hello alınan sunucu hello isteği Hello zaman |
| EndTime |Dize |Merhaba zaman hangi hello sunucu bir yanıt gönderdi. |

### <a name="audit-logs"></a>Denetim günlükleri

Merhaba JSON biçimli Denetim günlüğüne örnek girişi İşte. Her bir blob olarak adlandırılan bir kök nesnesi vardır **kayıtları** günlük nesnelerinin bir dizisi içerir.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Denetim günlüğü şeması

| Ad | Tür | Açıklama |
| --- | --- | --- |
| time |Dize |Merhaba günlüğünün Hello zaman damgası (UTC) cinsinden |
| resourceId |Dize |işlemi sürdü hello kaynak Hello tanıtıcısı yerleştirin |
| category |Dize |Merhaba günlük kategorisi. Örneğin, **denetim**. |
| operationName |Dize |Oturum hello işlemin adı. Örneğin, JobSubmitted. |
| resultType |Dize |Bir alt durum hello iş durumu (operationName). |
| resultSignature |Dize |Merhaba iş durumu (operationName) ilgili ek ayrıntılar. |
| identity |Dize |İstenen hello işlemi hello kullanıcı. Örneğin, susan@contoso.com. |
| properties |JSON |Ayrıntılar için Hello sonraki bölümüne (Denetim günlüğü özellikleri Şeması) bakın |

> [!NOTE]
> **resultType** ve **resultSignature** bir işlemin hello sonucunu bilgileri sağlayın ve bir işlemin tamamlanması, yalnızca bir değer içerebilir. Örneğin, yalnızca bir değer içerir, **operationName** değerini içeren **JobStarted** veya **JobEnded**.
>
>

#### <a name="audit-log-properties-schema"></a>Denetim günlüğü özellikleri şeması

| Ad | Tür | Açıklama |
| --- | --- | --- |
| JobId |Dize |Merhaba kimliği atanan toohello işi |
| JobName |Dize |Merhaba işi için sağlanan hello adı |
| JobRunTime |Dize |Merhaba çalışma zamanı tooprocess hello iş kullanılan |
| SubmitTime |Dize |Başlangıç saati (UTC) bu hello iş gönderildi |
| StartTime |Dize |gönderisine (UTC) sonra çalışan Hello zaman hello iş başlatıldı |
| EndTime |Dize |Merhaba süresi hello işi sona erdi |
| Paralellik |Dize |Data Lake Analytics birim gönderme sırasında bu iş için istenen Hello sayısı |

> [!NOTE]
> **SubmitTime**, **StartTime**, **EndTime**, ve **paralellik** üzerinde bir işlemi bilgileri sağlayın. Bu girişler yalnızca bir değer varsa, işlemi başlatıldı veya tamamlanmış olan içerir. Örneğin, **SubmitTime** yalnızca sonra bir değer içeriyor **operationName** hello değerine sahip **JobSubmitted**.

## <a name="process-hello-log-data"></a>İşlem hello günlük verileri

Azure Data Lake Analytics hakkında bir örnek sağlar tooprocess ve hello günlük verilerini çözümleyin. Merhaba örneğini şurada bulabilirsiniz [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md)
