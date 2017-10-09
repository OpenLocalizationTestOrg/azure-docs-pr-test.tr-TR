---
title: "aaaCheck durum günlüğe kaydetmeyi ayarlayın ve Uyarıları - Azure mantıksal uygulamaları alma | Microsoft Docs"
description: "Durum ve logic apps için performans izleme, tanılama verilerini günlüğe ve uyarılarını ayarlama"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a>Durum İzleme, tanılama günlük ayarlama ve Azure Logic Apps için uyarılarını Aç

Çalıştırdıktan sonra [oluşturma ve bir mantıksal uygulama çalıştırma](../logic-apps/logic-apps-create-a-logic-app.md), çalışır geçmişi, tetikleyici geçmişi, durumunu ve performansını kontrol edebilirsiniz. Gerçek zamanlı Olay izleme ve daha zengin hata ayıklama için ayarlanmış [tanılama günlükleri](#azure-diagnostics) mantığı uygulamanız için. Bu şekilde yapabilecekleriniz [bulma ve görüntüleme olayları](#find-events)tetikleyici olayları, çalışma olayları ve eylem olayları gibi. Bu da kullanabilirsiniz [tanılama verilerini diğer hizmetlerle](#extend-diagnostic-data)Azure Storage ve Azure Event Hubs gibi. 

hataları veya diğer olası sorunları hakkında tooget bildirimler ayarlanan [uyarıları](#add-azure-alerts). Örneğin, "beşten fazla çalıştığında bir saat içinde başarısız olduğunda." algıladığında bir uyarı oluşturabilir. Ayrıca izleme, izleme ve program aracılığıyla kullanarak oturum ayarlayabilirsiniz [Azure tanılama olay ayarlarını ve özelliklerini](#diagnostic-event-properties).

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a>Görünüm çalıştırır ve mantıksal uygulamanız için tetikleyici geçmişi

1. toofind mantıksal uygulamanızı hello [Azure portal](https://portal.azure.com), üzerinde hello Azure ana menü, seçin **daha fazla hizmet**. Merhaba arama kutusuna "logic apps" bulun ve seçin **Logic apps**.

   ![Mantıksal uygulamanızı Bul](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   Hello Azure portal, Azure aboneliğinizle ilişkili tüm hello mantıksal uygulamaları gösterir. 

2. Mantıksal uygulamanızı seçin, sonra seçin **genel bakış**.

   Hello Azure portal hello çalıştırır geçmişi ve mantıksal uygulamanızı için tetikleyici geçmişini gösterir. Örneğin:

   ![Mantıksal uygulama geçmişi ve tetikleyici geçmişi çalıştırır](media/logic-apps-monitor-your-logic-apps/overview.png)

   * **Geçmiş çalıştıran** mantıksal uygulamanızı tüm hello çalıştırmalarında gösterir. 
   * **Tetiklemek geçmişi** mantığı uygulamanız için tüm hello tetikleyici etkinliğini gösterir.

   Durum açıklamaları için bkz: [mantıksal uygulamanızı sorun giderme](../logic-apps/logic-apps-diagnosing-failures.md).

   > [!TIP]
   > Merhaba araç çubuğunda, beklediğiniz hello veri bulamazsanız seçin **yenileme**.

3. tooview hello adımları belirli bir çalışma altında **çalıştıran geçmişi**, çalıştırılan seçin. 

   Merhaba İzleyicisi görünümü her adım, çalışan gösterir. Örneğin:

   ![Belirli bir çalıştırma için Eylemler](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. tooget Çalıştır hello hakkında daha fazla ayrıntı seçin **çalıştırma ayrıntıları**. Bu bilgileri özetler hello adımları, durumu girişleri ve çıkışları hello için çalıştırın. 

   ![Seçin "Ayrıntıları Çalıştır"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   Örneğin, hello elde edebilirsiniz çalışmanın **bağıntı kimliği**, hello kullandığınızda, gereksinim duyabileceğiniz [Logic Apps için REST API](https://docs.microsoft.com/rest/api/logic).

5. belirli bir adıma tooget ayrıntılarını bu adımı seçin. Şimdi girişleri ve çıkışları Bu adım için gerçekleşen hataları gibi ayrıntıları gözden geçirebilirsiniz. Örneğin:

   ![Adım ayrıntıları](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > Tüm çalışma zamanı ayrıntılarını ve olayları Logic Apps hizmet hello içinde şifrelenir. Yalnızca bir kullanıcı bu verileri tooview istediğinde şifresi çözülür. Erişimi toothese olaylarını kontrol edebilirsiniz [Azure rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-what-is.md).

6. belirli tetikleyici olay tooget ayrıntılarını Geri Git toohello **genel bakış** bölmesi. Altında **tetiklemek geçmişi**seçin hello tetikleyici olay. Şimdi girişleri ve çıkışları, gibi ayrıntıları örneğin gözden geçirebilirsiniz:

   ![Tetikleyici olay çıkış ayrıntıları](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a>Tanılama mantığı uygulamanız için oturum açma

Daha zengin çalışma zamanı ayrıntılarını ve olayları ile hata ayıklama, tanılama ile oturum ayarlayabilirsiniz [Azure günlük analizi](../log-analytics/log-analytics-overview.md). Günlük analizi olan bir hizmet olarak [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) bulut izler ve şirket içi ortamları toohelp kendi kullanılabilirliğini ve performansını korumak. 

Başlamadan önce toohave bir OMS çalışma alanı gerekir. Bilgi [nasıl toocreate bir OMS çalışma](../log-analytics/log-analytics-get-started.md).

1. Merhaba, [Azure portal](https://portal.azure.com), bulma ve mantıksal uygulamanızı seçin. 

2. Merhaba mantığı uygulama dikey menüsünde altında **izleme**, seçin **tanılama** > **tanılama ayarlarını**.

   ![TooMonitoring, tanılama, tanılama ayarlarına Git](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. Altında **tanılama ayarları**, seçin **üzerinde**.

   ![Tanılama günlüklerini Aç](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. Şimdi gösterildiği gibi günlüğe kaydetme için hello OMS çalışma ve olay kategorisi seçin:

   1. Seçin **tooLog Analytics Gönder**. 
   2. Altında **günlük analizi**, seçin **yapılandırma**. 
   3. Altında **OMS çalışma alanları**, hello OMS çalışma toouse günlüğü için seçin.
   4. Altında **günlük**seçin hello **WorkflowRuntime** kategorisi.
   5. Merhaba ölçüm aralığını seçin.
   6. İşiniz bittiğinde seçin **kaydetmek**.

   ![OMS çalışma ve günlük verilerini seçin](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

Şimdi, olaylar ve eylem olaylar çalıştırmak tetikleyici olaylar için olayları ve diğer verileri bulabilirsiniz.

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a>Mantıksal uygulamanız için olaylar ve veri Bul

Tetikleyici olaylar, olaylar, çalıştırmak ve eylem olaylar gibi mantıksal uygulamanızı toofind ve görünüm olayları aşağıdaki adımları izleyin.

1. Merhaba, [Azure portal](https://portal.azure.com), seçin **daha Hizmetleri**. "İçin günlük analizi" arayın, ardından seçin **günlük analizi** aşağıda gösterildiği gibi:

   !["Günlük analizi" seçin](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. Altında **günlük analizi**, bulma ve OMS çalışma alanınızı seçin. 

   ![OMS çalışma alanınızı seçin](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. Altında **Yönetim**, seçin **OMS portalı**.

   !["OMS portalı" seçin](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. OMS giriş sayfanızda seçin **günlük arama**.

   ![OMS giriş sayfanızda "Günlük arama" seçin](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   -veya-

   ![Merhaba OMS menüsünde "Günlük arama" öğesini seçin](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. Merhaba arama kutusuna, toofind, istediğiniz bir alanı belirtin ve basın **Enter**. Yazmaya başladığınızda, OMS olası eşleşmeler ve kullanabileceğiniz işlemleri gösterir. 

   Örneğin, toofind hello ilk 10 olayları girin ve bu arama sorgusuna seçin: **kategori WorkflowRuntime = | üst 10**

   ![Arama dizesini girin](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   Daha fazla bilgi edinmek [nasıl günlük analizi toofind verileri](../log-analytics/log-analytics-log-searches.md).

6. Merhaba sonuçları sayfasında hello sol çubuğunda hello zaman dilimi seçin tooview istiyor.
bir filtre ekleyerek sorgunuzu toorefine seçin **+ Ekle**.

   ![Sorgu sonuçları ilişkin zaman çerçevesini seçin](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. Altında **filtreler Ekle**, istediğiniz hello filtre bulabilmesi hello filtre adı girin. Merhaba filtresini seçin ve **+ Ekle**.

   Kullandığı hello word "Durum" toofind Bu örnek altındaki olaylarını başarısız **AzureDiagnostics**.
   Burada, filtre için hello **status_s** zaten seçilidir.

   ![Filtreyi seçin](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. Hello sol çubuğunda toouse istediğiniz ve seçin hello filtre değeri seçin **Uygula**.

   ![Filtre değeri seçin, "Uygula"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. Şimdi oluşturmakta olduğunuz toohello sorgu döndür. Sorgunuz seçili filtresi ve değer ile güncelleştirilir. Önceki sonuçlarınızı artık çok filtrelenir.

   ![Filtrelenmiş sonuçlar tooyour sorgu döndürme](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. Sorgunuz gelecekte kullanım için toosave seçin **kaydetmek**. Bilgi [nasıl toosave sorgunuzu](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>Nasıl ve tanılama verilerini diğer hizmetleri ile kullandığınız genişletme

Azure günlük analizi ile birlikte nasıl mantığı uygulamanızın tanılama verilerini diğer Azure hizmetleriyle örneğin kullandığınız genişletebilirsiniz: 

* [Azure depolama alanında Azure tanılama günlüklerini arşiv](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [Akış Azure tanılama günlükleri tooAzure olay hub'ları](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

Telemetri ve diğer hizmetlerden analizi kullanarak izleme Get gerçek zamanlı ister sonra şunları yapabilirsiniz [Azure akış analizi](../stream-analytics/stream-analytics-introduction.md) ve [Power BI](../log-analytics/log-analytics-powerbi.md). Örneğin:

* [Olay hub'ları tooStream Analytics akış verileri](../stream-analytics/stream-analytics-define-inputs.md)
* [Akış Analizi ile akış verilerini çözümleme ve gerçek zamanlı analiz Pano Power BI'da oluşturma](../stream-analytics/stream-analytics-power-bi-dashboard.md)

Ayarlamak istediğiniz hello seçenekleri bağlı olarak, olduğundan emin olun, ilk [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md) veya [Azure olay hub'ı oluşturma](../event-hubs/event-hubs-create.md). Ardından toosend tanılama verilerini istediğiniz hello seçeneklerini seçin:

![Veri tooAzure depolama hesabı veya olay hub'ı Gönder](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> Yalnızca, bir depolama hesabı toouse'ı seçtiğinizde bekletme dönemleri uygulamak.

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a>Mantıksal uygulamanız için uyarıları ayarlama

toomonitor belirli ölçümleri veya mantıksal uygulamanızı aşıldı eşikler ayarlanmış [Azure içindeki uyarıları](../monitoring-and-diagnostics/monitoring-overview-alerts.md). Hakkında bilgi edinin [Azure ölçümlerini](../monitoring-and-diagnostics/monitoring-overview-metrics.md). 

Uyarılar tooset [Azure günlük analizi](../log-analytics/log-analytics-overview.md), şu adımları izleyin. Uyarı ölçütleri ve Eylemler, daha gelişmiş [günlük analizi ayarlamak](#azure-diagnostics) çok.

1. Merhaba mantığı uygulama dikey menüsünde altında **izleme**, seçin **tanılama** > **uyarı kuralları** > **UyarıEkle**aşağıda gösterildiği gibi:

   ![Mantıksal uygulamanız için uyarı ekleme](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. Hello üzerinde **uyarı kuralı eklemek** dikey penceresinde, uyarı gösterildiği gibi oluşturun:

   1. Altında **kaynak**, mantıksal uygulamanızı seçin, seçili değilse. 
   2. Bir ad ve açıklama için uyarı verir.
   3. Seçin bir **ölçüm** veya tootrack istediğiniz olay.
   4. Seçin bir **koşulu**, belirtin bir **eşik** hello ölçüm ve select hello **süresi** Bu ölçüm izleme.
   5. Toosend posta olup olmadığını hello uyarı için seçin. 
   6. Diğer tüm e-posta adreslerini hello uyarı göndermek için belirtin. 
   Toosend hello uyarı istediğiniz bir Web kancası URL'si de belirtebilirsiniz.

   Örneğin, bu kural beş olduğunda bir uyarı gönderir veya daha fazla çalıştığında bir saat içinde başarısız:

   ![Ölçüm uyarı kuralı oluştur](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> bir mantıksal uygulama toorun bir uyarıdan hello içerebilir [isteği tetikleyici](../connectors/connectors-native-reqres.md) , iş akışınızı olanak sağlayan bu örnekler gibi görevleri gerçekleştirmenize:
> 
> * [POST tooSlack](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [Bir metin Gönder](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [Bir ileti tooa sırası Ekle](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a>Azure Tanılama Olay ayarları ve ayrıntıları

Mantıksal uygulamanızı ve bu olay, örneğin, hello durumu hakkındaki ayrıntıları her Tanılama Olay sahipse, başlangıç saati, bitiş saati ve benzeri. İzleme, izleme ve günlüğe kaydetme ayarlama tooprogrammatically ou kullanabilir bu ayrıntıları ile Merhaba [Azure Logic Apps için REST API](https://docs.microsoft.com/rest/api/logic) ve hello [Azure tanılama için REST API](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).

Örneğin, hello `ActionCompleted` olayında hello `clientTrackingId` ve `trackedProperties` izleme ve izleme için kullanabileceğiniz özellikler:

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* `clientTrackingId`: Değilse tüm iç içe geçmiş iş akışları dahil olmak üzere Azure otomatik olarak bu kimliği oluşturur ve olayları çalıştırmak bir mantıksal uygulama arasında karşılık gelen sağlanan hello mantığı uygulamadan çağrılan. Bu kimliği bir tetikleyiciden geçirerek el ile belirtebilirsiniz bir `x-ms-client-tracking-id` üstbilgisi, özel hello tetikleyici isteği kimliği değere sahip. Bir istek tetikleyici, HTTP tetikleyicisini ya da Web kancası tetikleyici kullanabilirsiniz.

* `trackedProperties`: tootrack girişleri veya çıkışları tanılama verilerdeki, ekleyebilirsiniz izlenen özellikleri tooactions mantığı uygulamanızın JSON tanımında. İzlenen özellikleri yalnızca tek bir eylemin girişleri ve çıkışları izleyebilirsiniz, ancak hello kullanabilirsiniz `correlation` çalıştırmada eylemler arasında olayları toocorrelate özelliklerini.

  tootrack bir veya daha fazla özellik eklemek hello `trackedProperties` toohello eylem tanımı istediğiniz bölüm ve hello özellikleri. Örneğin, "Düzeni kimliği" gibi tootrack veri, telemetri istediğinizi varsayalım:

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a>Sonraki adımlar

* [Mantıksal uygulama dağıtımı için şablonlar oluşturma ve yayın Yönetimi](../logic-apps/logic-apps-create-deploy-template.md)
* [B2B senaryolarını Kurumsal tümleştirme paketi](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [B2B iletilerini izleme](../logic-apps/logic-apps-monitor-b2b-message.md)