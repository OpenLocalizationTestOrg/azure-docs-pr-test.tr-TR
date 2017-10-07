---
title: "Operations Management Suite - Azure Logic Apps B2B iletiler için aaaQuery | Microsoft Docs"
description: "Merhaba Operations Management Suite sorguları tootrack AS2, X 12 ve EDIFACT iletileri oluşturma"
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
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a>Sorgu için AS2, X 12 ve EDIFACT iletilerinde hello Microsoft Operations Management Suite (OMS)

toofind hello AS2, X 12 veya ile takip ettiğiniz EDIFACT iletileri [Azure günlük analizi](../log-analytics/log-analytics-overview.md) hello içinde [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), belirli bağlı eylemleri filtre sorgular oluşturabilirsiniz ölçütleri. Örneğin, belirli Değişim Denetimi sayısına bağlı olarak iletileri bulabilirsiniz.

## <a name="requirements"></a>Gereksinimler

* Tanılama Günlüğü ile ayarlanmış bir mantıksal uygulama. Bilgi [nasıl toocreate bir mantıksal uygulama](../logic-apps/logic-apps-create-a-logic-app.md) ve [nasıl tooset bu mantıksal uygulama günlüklerini](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* İzleme ve günlük ile ayarlanan bir tümleştirme hesabı. Bilgi [nasıl toocreate bir tümleştirme hesap](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) ve [nasıl izleme ve o hesap için oturum tooset](../logic-apps/logic-apps-monitor-b2b-message.md).

* Henüz yapmadıysanız [tanılama veri tooLog Analytics yayımlama](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) ve [ileti OMS içinde izleme ayarlama](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

> [!NOTE]
> Merhaba önceki gereksinimlerini karşılamanızın sonra hello çalışma olmalıdır [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Kullanmanız gereken Merhaba, OMS B2B iletişiminde izleme için aynı OMS çalışma. 
>  
> Bir OMS çalışma alanı yoksa, bilgi [nasıl toocreate bir OMS çalışma](../log-analytics/log-analytics-get-started.md).

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a>Merhaba Operations Management Suite portalına filtreleri ile iletisi sorguları oluşturma

Bu örnek, değişim denetimi numarasına göre iletileri nasıl bulabilirsiniz gösterir.

> [!TIP] 
> OMS çalışma alanı adınız biliyorsanız, tooyour çalışma giriş sayfasına gidin (`https://{your-workspace-name}.portal.mms.microsoft.com`) ve adım 4 olarak başlatın. Aksi takdirde, adım 1'den başlar.

1. Merhaba, [Azure portal](https://portal.azure.com), seçin **daha Hizmetleri**. "İçin günlük analizi" araması yapın ve ardından **günlük analizi** aşağıda gösterildiği gibi:

   ![Günlük analizi Bul](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. Altında **günlük analizi**, bulma ve OMS çalışma alanınızı seçin.

   ![OMS çalışma alanınızı seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. Altında **Yönetim**, seçin **OMS portalı**.

   ![OMS portalı seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. OMS giriş sayfanızda seçin **günlük arama**.

   ![OMS giriş sayfanızda "Günlük arama" seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   -veya-

   ![Merhaba OMS menüsünde "Günlük arama" öğesini seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. Toofind, istediğiniz bir alanı Hello arama kutusuna girin ve basın **Enter**. Yazmaya başladığınızda, OMS olası eşleşmeler ve kullanabileceğiniz işlemleri gösterir. Daha fazla bilgi edinmek [nasıl günlük analizi toofind verileri](../log-analytics/log-analytics-log-searches.md).

   Bu örnekte arama olan olaylar için **türü AzureDiagnostics =**.

   ![Sorgu dizesi yazmaya başlayın](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. Merhaba sol çubuğunda hello zaman dilimi seçin tooview istiyor. tooadd bir filtre tooyour sorgu seçin **+ Ekle**.

   ![Filtre tooquery Ekle](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. Altında **filtreler Ekle**, istediğiniz hello filtre bulabilmesi hello filtre adı girin. Merhaba filtresini seçin ve **+ Ekle**.

   toofind hello değiş tokuş denetim numarası, bu örnek için "değişim" Merhaba word arar ve seçer **event_record_messageProperties_interchangeControlNumber_s** hello filtre olarak.

   ![Filtreyi seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. Hello sol çubuğunda toouse istediğiniz ve seçin hello filtre değeri seçin **Uygula**.

   Bu örnek hello değiş tokuş denetim numarası istiyoruz Merhaba iletileri için seçer.

   ![Filtre değeri seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. Şimdi oluşturmakta olduğunuz toohello sorgu döndür. Sorgunuz seçilen filtre olay ve değeri ile güncelleştirilmiştir. Önceki sonuçlarınızı artık çok filtrelenir.

    ![Filtrelenmiş sonuçlar tooyour sorgu döndürme](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a>Sorgunuz gelecekte kullanım için Kaydet

1. Sorgunuzu hello üzerinde gelen **günlük arama** sayfasında, **kaydetmek**. Sorgunuz bir ad verin, bir kategori seçin ve **kaydetmek**.

   ![Bir ad ve kategori sorgunuz verin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. tooview Sorgunuzdaki seçin **Sık Kullanılanlar**.

   !["Sık Kullanılanlar" seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. Altında **kayıtlı aramaları**, sorgunuzu hello sonuçları görüntüleyebilmesi için seçin. farklı sonuçlar bulabilmesi tooupdate hello sorgu hello sorgu düzenleyin.

   ![Sorgunuz seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a>Bulma ve hello Operations Management Suite Portalı'nda kayıtlı sorgu çalıştırma

1. OMS çalışma giriş sayfanız açın (`https://{your-workspace-name}.portal.mms.microsoft.com`) ve seçin **günlük arama**.

   ![OMS giriş sayfanızda "Günlük arama" seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   -veya-

   ![Merhaba OMS menüsünde "Günlük arama" öğesini seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. Merhaba üzerinde **günlük arama** giriş sayfasını, seçin **Sık Kullanılanlar**.

   !["Sık Kullanılanlar" seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. Altında **kayıtlı aramaları**, sorgunuzu hello sonuçları görüntüleyebilmesi için seçin. farklı sonuçlar bulabilmesi tooupdate hello sorgu hello sorgu düzenleyin.

   ![Sorgunuz seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a>Sonraki adımlar

* [AS2 izleme şemaları](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [X12 izleme şemaları](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Özel İzleme şemaları](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)