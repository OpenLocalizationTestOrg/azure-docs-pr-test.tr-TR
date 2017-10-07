---
title: "mantıksal uygulamanızı hakkında aaaMonitor ve get Öngörüler çalıştıran OMS - Azure mantıksal uygulamaları kullanma | Microsoft Docs"
description: "Logic app çalışmalarınız günlük analizi ve Operations Management Suite (OMS) tooget Öngörüler ve sorun giderme ve tanılama daha zengin hata ayıklama ayrıntılarını ile izleme"
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a>İzleyici ve get Öngörüler mantıksal uygulama hakkında Operations Management Suite (OMS) ve günlük analizi ile çalışır

İzleme ve daha zengin hata ayıklama bilgileri almak için günlük analizi hello kapatabilirsiniz bir mantıksal uygulama'ı oluşturduğunuzda aynı zamanda. Günlük analizi günlüğe kaydetme ve izleme mantığı uygulamanız için tanılama hello Operations Management Suite (OMS) portalı üzerinden çalışan sağlar. Merhaba Logic Apps yönetim çözümü tooOMS eklediğinizde, logic app çalıştırır ve durumu, yürütme süresi, yeniden gönderme durumu ve bağıntı kimlikleri gibi belirli Ayrıntılar için toplanan durumunu alın.

Bu konu, nasıl tooturn günlük analizi veya yükleme hello Logic Apps yönetim çözümüne OMS çalışma olaylarını görüntüleyebilir ve veri mantığı uygulamanız için çalıştırmaları için gösterir.

 > [!TIP]
 > toomonitor mevcut mantıksal uygulamalarınızı adımları çok [tanılama günlük özelliğini açar ve mantığı uygulama çalışma zamanı verileri tooOMS Gönder](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

## <a name="requirements"></a>Gereksinimler

Başlamadan önce toohave bir OMS çalışma alanı gerekir. Bilgi [nasıl toocreate bir OMS çalışma](../log-analytics/log-analytics-get-started.md). 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a>Logic apps oluştururken tanılama günlüğünü etkinleştirme

1. İçinde [Azure portal](https://portal.azure.com), bir mantıksal uygulama oluşturma. Seçin **yeni** > **Kurumsal tümleştirme** > **mantıksal uygulama** > **oluşturma**.

   ![Mantıksal uygulama oluşturma](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. Merhaba, **oluşturma mantıksal uygulama** sayfasında, gösterildiği gibi bu görevleri gerçekleştirmek:

   1. Mantıksal uygulamanız için bir ad ve Azure aboneliğinizi seçin. 
   2. Bir Azure kaynak grubu seçin veya oluşturun.
   3. Ayarlama **günlük analizi** çok**üzerinde**. 
   Çok mantığı uygulamanız için veri göndermek istediğiniz yeri seçin hello OMS çalışma çalışır. 
   4. Hazır olduğunuzda, seçin **PIN toodashboard** > **oluşturma**.

      ![Mantıksal uygulama oluşturma](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      Bu adımı tamamladıktan sonra artık mantıksal uygulamanızı Azure oluşturur, OMS çalışma alanıyla ilişkilendirilmiş. 
      Ayrıca, bu adım OMS çalışma alanınızda hello Logic Apps yönetimi çözümü de otomatik olarak yükler.

3. mantıksal uygulamanızı çalıştıran OMS içinde tooview [bu adımlarla devam](#view-logic-app-runs-oms).

## <a name="install-hello-logic-apps-management-solution-in-oms"></a>Merhaba Logic Apps yönetimi çözümü içinde OMS yükleyin

Mantıksal uygulamanızı oluşturduğunuzda günlük analizi zaten etkinleştirdiyseniz, bu adımı atlayın. Merhaba Logic Apps yönetimi çözümü içinde OMS yüklenmiş zaten var.

1. Merhaba, [Azure portal](https://portal.azure.com), seçin **daha Hizmetleri**. Filtre olarak "günlük analizi" arayın ve seçin **günlük analizi** gösterildiği gibi:

   !["Günlük analizi" seçin](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. Altında **günlük analizi**, bulma ve OMS çalışma alanınızı seçin. 

   ![OMS çalışma alanınızı seçin](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. Altında **Yönetim**, seçin **OMS portalı**.

   !["OMS portalı" seçin](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. Merhaba yükseltme başlık görünürse, OMS sayfanız OMS çalışma alanınızı yükseltmeniz hello başlığı seçin. Ardından **Çözümleri Galerisi**.

   !["Çözümleri Galerisi" seçin](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. Altında **tüm çözümleri**, bulun ve hello bölme hello için seçin **Logic Apps Yönetim** çözümü.

   !["Logic Apps Yönetimi" seçin](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. OMS çalışma alanınızdaki tooinstall hello çözümü seçme **Ekle**.

   !["" Logic Apps yönetimi için"Ekle" yi seçin](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a>OMS çalışma alanınızda mantıksal uygulamanızı çalıştıran görünümü

1. tooview hello sayısı ve mantıksal uygulamanızı durumunun gidin toohello genel bakış sayfasında OMS çalışma alanınız için çalışır. Merhaba hello ayrıntıları gözden **Logic Apps Yönetim** döşeme.

   ![Mantığı çalıştırmak uygulama sayısı ve durumunu gösteren genel bakış kutucuğu](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > Bu yükseltme başlık hello Logic Apps yönetim döşeme yerine görünürse, böylece OMS çalışma alanınızı yükseltmeniz hello başlığını seçin.
  
   > ![Yükseltme "OMS çalışma"](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. tooview mantığı uygulama çalışmalarınız hakkında daha fazla ayrıntı özeti seçin hello **Logic Apps Yönetim** döşeme.

   Burada, logic app çalışmalarınız adına veya yürütme durumu göre gruplandırılır.

   ![Mantıksal uygulamanız için Özet durum çalıştırır](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. belirli mantıksal uygulama veya durum, bir mantıksal uygulama veya bir durum için select hello satır için tüm hello tooview çalışır.

   Belirli mantıksal uygulama için tüm hello çalıştırmalarını gösteren bir örnek aşağıda verilmiştir:

   ![Bir mantıksal uygulama veya bir durum görünümü çalıştırır](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > Merhaba **yeniden gönderme** sütun yeniden gönderilen bir çalıştırma sonucu çalışmaları için "Evet" gösterir.

4. Bu sonuçları toofilter, istemci tarafı ve sunucu tarafı filtreleme gerçekleştirebilirsiniz.

   * İstemci tarafı filtresi: her sütun için istediğiniz hello filtrelerini seçin. 
   İşte bazı örnekler:

     ![Örnek sütun filtreleri](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * Sunucu tarafı filtresi: toochoose belirli bir zaman penceresi veya toolimit hello çeşitli görüntülenir, hello sayfanın üst kısmındaki hello kullan hello kapsam denetim çalıştırır. 
   Varsayılan olarak, aynı anda yalnızca 1.000 kayıtları görünür. 
   
     ![Değişiklik hello zaman penceresi](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. Tüm tooview hello günlük arama sayfası açılır bir satır Eylemler ve bunların ayrıntılarını belirli bir çalışma, select hello. 

   * Bu bilgileri bir tabloda tooview seçme **tablo**.
   * toochange hello sorgu hello sorgu dizesi hello arama çubuğunda düzenleyebilirsiniz. 
   Daha iyi bir deneyim için seçin **Advanced Analytics**.

     ![Eylemler ve Çalıştır bir mantıksal uygulama ayrıntılarını görüntüleyin](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     Burada hello Azure günlük analizi sayfasında, sorgular ve görünüm güncelleştirebilirsiniz hello hello tablosundan sonuçlanır. 
     Bu sorgu kullanan [Kusto sorgu dili](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), tooview farklı sonuçlar istiyorsanız düzenleyebileceğiniz. 

     ![Azure günlük analizi - sorgu görünümü](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a>Sonraki adımlar

* [B2B iletilerini izleme](../logic-apps/logic-apps-monitor-b2b-message.md)
