---
title: "aaaMonitor B2B işlemleri ve günlük - Azure Logic Apps ayarlama | Microsoft Docs"
description: "İzleyici AS2, X 12 ve EDIFACT iletileri tümleştirme hesabınız için tanılama günlüğünü Başlat"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a>İzleme ve tanılama günlüklerini tümleştirme hesaplarındaki B2B iletişimi için ayarlayın

İkisi arasındaki B2B iletişim kurduktan sonra iş süreçlerini veya tümleştirme hesabınızı aracılığıyla uygulamaları çalıştıran bu varlıkların birbirleriyle iletileri değiştirebilir. Bu iletişim tooconfirm beklendiği gibi çalışır, AS2, X12, izleme işlevini ayarlama ve tümleştirme hesabınız hello üzerinden için tanılama günlüğünü birlikte EDIFACT iletileri [Azure günlük analizi](../log-analytics/log-analytics-overview.md) hizmet. Bu hizmet [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) bulut izler ve şirket içi ortamları, bunların kullanılabilirlik ve performans, tutmanıza yardımcı olur ve ayrıca çalışma zamanı Ayrıntılar ve daha zengin hata ayıklama olaylarını toplar. Ayrıca [diğer hizmetlerle tanılama verilerinizi kullanma](#extend-diagnostic-data)Azure Storage ve Azure Event Hubs gibi.

## <a name="requirements"></a>Gereksinimler

* Tanılama Günlüğü ile ayarlanmış bir mantıksal uygulama. Bilgi [nasıl tooset bu mantıksal uygulama günlüklerini](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

  > [!NOTE]
  > Bu gereksinim karşılamanızın sonra hello çalışma olmalıdır [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Kullanmanız gereken tümleştirme hesabınız için günlüğe kaydetmeyi ayarlayın, aynı OMS çalışma hello. Bir OMS çalışma alanı yoksa, bilgi [nasıl toocreate bir OMS çalışma](../log-analytics/log-analytics-get-started.md).

* Tooyour mantıksal uygulama bağlantılı içeren bir tümleştirme hesabı. Bilgi [nasıl toocreate bir tümleştirme hesabı ile bağlantı tooyour mantıksal uygulama](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a>Tanılama tümleştirme hesabınızda oturum açın

Doğrudan tümleştirme hesabınızdan ya da günlük özelliğini açın veya [hello Azure Monitor Hizmeti aracılığıyla](#azure-monitor-service). Azure İzleyicisi temel altyapı düzeyinde verilerle izleme sağlar. Daha fazla bilgi edinmek [Azure İzleyici](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a>Tanılama tümleştirme hesabınızdan doğrudan oturum aç

1. Merhaba, [Azure portal](https://portal.azure.com), bulma ve tümleştirme hesabınızı seçin. Altında **izleme**, seçin **tanılama günlükleri** aşağıda gösterildiği gibi:

   ![Bulma ve tümleştirme hesabınızı seçin, "Tanılama günlükleri"](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. Tümleştirme hesabınızı seçtikten sonra aşağıdaki değerleri hello otomatik olarak seçilir. Bu değerler doğru olup olmadığını seçin **tanılamayı açın**. Aksi takdirde, istediğiniz hello değerleri seçin:

   1. Altında **abonelik**, hello tümleştirme hesabınızla kullandığınız Azure aboneliğini seçin.
   2. Altında **kaynak grubu**seçin tümleştirme hesabınızla kullandığınız hello kaynak grubu.
   3. Altında **kaynak türü**seçin **tümleştirme hesapları**. 
   4. Altında **kaynak**, tümleştirme hesabınızı seçin. 
   5. Seçin **tanılamayı açın**.

   ![Tanılama tümleştirme hesabınız için ayarlama](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. Altında **tanılama ayarları**ve ardından **durum**, seçin **üzerinde**.

   ![Azure tanılamayı açın](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. Şimdi gösterildiği gibi hello OMS çalışma ve veri toouse günlüğü için seçin:

   1. Seçin **tooLog Analytics Gönder**. 
   2. Altında **günlük analizi**, seçin **yapılandırma**. 
   3. Altında **OMS çalışma alanları**, hello OMS çalışma toouse günlüğü için seçin.
   4. Altında **günlük**seçin hello **IntegrationAccountTrackingEvents** kategorisi.
   5. **Kaydet**'i seçin.

   ![Tanılama veri tooa günlük gönderebilmek için günlük analizi ayarlayın](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. Şimdi [OMS B2B iletilerinizi izleme ayarlama](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a>Tanılama günlükleri Azure İzleyicisi üzerinden Aç

1. Merhaba, [Azure portal](https://portal.azure.com), üzerinde hello Azure ana menü, seçin **İzleyici**, **tanılama günlükleri**. Ardından aşağıda gösterildiği gibi tümleştirme hesabınızı seçin:

   !["İzleme", "Tanılama günlükleri" seçin tümleştirme hesabınızı seçin](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. Tümleştirme hesabınızı seçtikten sonra aşağıdaki değerleri hello otomatik olarak seçilir. Bu değerler doğru olup olmadığını seçin **tanılamayı açın**. Aksi takdirde, istediğiniz hello değerleri seçin:

   1. Altında **abonelik**, hello tümleştirme hesabınızla kullandığınız Azure aboneliğini seçin.
   2. Altında **kaynak grubu**seçin tümleştirme hesabınızla kullandığınız hello kaynak grubu.
   3. Altında **kaynak türü**seçin **tümleştirme hesapları**.
   4. Altında **kaynak**, tümleştirme hesabınızı seçin.
   5. Seçin **tanılamayı açın**.

   ![Tanılama tümleştirme hesabınız için ayarlama](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. Altında **tanılama ayarları**, seçin **üzerinde**.

   ![Azure tanılamayı açın](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. Şimdi gösterildiği gibi günlüğe kaydetme için hello OMS çalışma ve olay kategorisi seçin:

   1. Seçin **tooLog Analytics Gönder**. 
   2. Altında **günlük analizi**, seçin **yapılandırma**. 
   3. Altında **OMS çalışma alanları**, hello OMS çalışma toouse günlüğü için seçin.
   4. Altında **günlük**seçin hello **IntegrationAccountTrackingEvents** kategorisi.
   5. İşiniz bittiğinde seçin **kaydetmek**.

   ![Tanılama veri tooa günlük gönderebilmek için günlük analizi ayarlayın](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. Şimdi [OMS B2B iletilerinizi izleme ayarlama](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>Nasıl ve tanılama verilerini diğer hizmetleri ile kullandığınız genişletme

Azure günlük analizi ile birlikte nasıl mantığı uygulamanızın tanılama verilerini diğer Azure hizmetleriyle örneğin kullandığınız genişletebilirsiniz: 

* [Azure depolama alanında Azure tanılama günlüklerini arşiv](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [Akış Azure tanılama günlükleri tooAzure olay hub'ları](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

Telemetri ve diğer hizmetlerden analizi kullanarak izleme Get gerçek zamanlı ister sonra şunları yapabilirsiniz [Azure akış analizi](../stream-analytics/stream-analytics-introduction.md) ve [Power BI](../log-analytics/log-analytics-powerbi.md). Örneğin:

* [Olay hub'ları tooStream Analytics akış verileri](../stream-analytics/stream-analytics-define-inputs.md)
* [Akış Analizi ile akış verilerini çözümleme ve gerçek zamanlı analiz Pano Power BI'da oluşturma](../stream-analytics/stream-analytics-power-bi-dashboard.md)

Ayarlamak istediğiniz hello seçenekleri bağlı olarak, olduğundan emin olun, ilk [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md) veya [Azure olay hub'ı oluşturma](../event-hubs/event-hubs-create.md). Ardından toosend tanılama verilerini istediğiniz hello seçeneklerini seçin:

![Veri tooAzure depolama hesabı veya olay hub'ı Gönder](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> Yalnızca, bir depolama hesabı toouse'ı seçtiğinizde bekletme dönemleri uygulamak.

## <a name="supported-tracking-schemas"></a>Desteklenen izleme şemaları

Azure bunlar tüm özel türü hello dışında şemaları sabit şema türleri, izleme destekler.

* [AS2 izleme şeması](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [X12 izleme şeması](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Özel izleme şeması](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a>Sonraki adımlar

* [OMS B2B iletilerini izlemek](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "OMS izleme B2B iletileri")
* [Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](../logic-apps/logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin")

