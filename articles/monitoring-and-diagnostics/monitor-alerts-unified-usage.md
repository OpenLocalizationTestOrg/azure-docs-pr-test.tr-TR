---
title: "Oluşturun, görüntüleyin ve Uyarıları (Önizleme) uyarıları Azure İzleyici kullanarak - yönetme | Microsoft Docs"
description: "Yazar, görüntülemek ve ölçüm yönetmek ve uyarı kuralları tek bir yerden oturum için yeni birleşik Azure uyarıları deneyimi kullanın."
author: msvijayn
manager: kmadnani1
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/12/2017
ms.author: vinagara
ms.openlocfilehash: e3902ec5fc27c829fa97042d15552c8c895c6408
ms.sourcegitcommit: b7adce69c06b6e70493d13bc02bd31e06f291a91
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/19/2017
---
# <a name="create-view-and-manage-alerts-using-azure-monitor---alerts-preview"></a>Oluşturun, görüntüleyin ve Uyarıları yönetme Azure İzleyicisi - uyarıları (Önizleme) kullanma

## <a name="overview"></a>Genel Bakış
Bu makalede Azure portalın içinde yeni uyarılar (Önizleme) arabirimini kullanarak uyarıları ayarlama gösterilmiştir. Bir uyarı kuralı tanımını üç bölümlerinde şöyledir:
- Hedef: izlenmesi için belirli Azure kaynağı,
- Ölçüt: Belirli bir koşulun veya mantığı, sinyalin görülen, eylem tetiklemesi gereken
- Eylem: Belirli çağrısı bir bildirim - alıcıya gönderilen, SMS, Web kancası vb. e-posta.

Uyarıları (Önizleme) kullanan terimi **günlük uyarıları** sinyal dayalı özel sorgu olduğu uyarıları açıklamak için [Azure günlük analizi](../log-analytics/log-analytics-tutorial-viewdata.md). Ölçüm uyarı yetenek adlı [yakın gerçek zamanlı ölçüm uyarıları](monitoring-near-real-time-metric-alerts.md) varolan uyarıları deneyimi olarak adlandırılır **ölçüm uyarıları** uyarılar (Önizleme). İçinde *ölçüm uyarıları*, bazı kaynak türleri sağlar [çok boyutlu ölçümleri](monitoring-metric-charts.md) belirli Azure kaynak için ve bu nedenle böyle kaynak ek filtreler kullanarak daha belirgin hale getirilebilir için uyarılar Boyutlar; Bu tür uyarılar denir **çok boyutlu ölçüm uyarıları**. Azure uyarıları (Önizleme), ayrıca tüm uyarı kuralları ve tek bir konumdan yönetme becerisini birleşik bir görünüm sağlar; Çözümlenmemiş tüm uyarıları görüntüleme dahil olmak üzere. İşlevinden hakkında daha fazla bilgi [Azure Alerts(Preview) - genel bakış](monitoring-overview-unified-alerts.md).

> [!NOTE]
> Azure Uyarıları'ni (Önizleme) ile Azure uyarıları oluşturmak için yeni ve geliştirilmiş bir deneyim sunan yapılırken. Varolan [Azure uyarıları](monitoring-overview-alerts.md) deneyimi kullanılabilir kalır
>

Aşağıdaki ayrıntılı Azure Uyarıları'ni (Önizleme) kullanarak adım adım kılavuzu olandır.

## <a name="create-an-alert-rule-with-the-azure-portal"></a>Azure portalıyla bir uyarı kuralı oluşturma
1. İçinde [portal](https://portal.azure.com/)seçin **İzleyici** ve izleme bölümü altında - **uyarıları (Önizleme)**.  
    ![İzleme](./media/monitor-alerts-unified/AlertsPreviewMenu.png)

2. Seçin **yeni uyarı kuralı** Azure'da yeni bir uyarı oluşturma düğmesi.
    ![Uyarı ekleme](./media/monitor-alerts-unified/AlertsPreviewOption.png)

3. Uyarı oluşturma bölümüne üç bölümden oluşan ile gösterilir: *Uyarı koşulu tanımla*, *uyarı ayrıntılarını tanımlayın*, ve *tanımla eylem grubu*.
    ![Kural oluşturma](./media/monitor-alerts-unified/AlertsPreviewAdd.png)

4.  İlk kullanarak Uyarı koşulu tanımlamak **Select Resource** bağlantı ve bir kaynak seçerek hedef belirleme. Uygun şekilde seçerek gerekli filtre *abonelik*, *kaynak türü*, ve son olarak seçilmesi gereken *kaynak*. Azure Uyarıları'ni (Önizleme) çeşitli türde bir uyarı tekil arabiriminden oluşturulmasını sağlar gibi; İstenen uyarı türüne göre sonraki adım olarak seçin:
    - İçin **ölçüm uyarıları**: 5-7 adımları; ardından doğrudan 11. adıma gidin
    - İçin **günlük uyarıları**, adım 8 ve sonraki sürümleri geçin

5. *Ölçüm uyarıları*: sağlamak **kaynak türü** seçili platform ya da İzleyici hizmeti (dışında *günlük analizi*), sonra bir kez uygun **kaynak** olduğu Seçilen tıklatın *Bitti* oluşturma uyarısı dönmek için düğmesini. Sonraki kullanmak **ölçüt eklemek** daha önce seçilen kaynak için kullanılabilir olan belirli sinyal sinyal seçenekleri, izleme hizmeti ve listelenen - türü listesinden seçmek için düğmesi.
    ![Bir kaynak seçin](./media/monitor-alerts-unified/AlertsPreviewResourceSelection.png)

    > [!NOTE]
    > Yalnızca hızlı bir uyarı kullanıma sunulan yeni ölçüm yetenekler sinyal türlerinde platform hizmetinden ölçümleri olarak dahil edilen
  

6. *Ölçüm uyarıları*: sinyal seçtikten sonra uyarı verme mantığı belirtilebilir. Başvuru için geçmiş veriler sinyali zaman penceresini kullanarak ince ayar seçeneğiyle gösterilir **geçmişini göster**, geçen hafta için son altı saat değişen. Görselleştirme, yerinde ile **uyarı mantığı** koşul, toplama ve son olarak eşik gösterilen seçeneklerinden seçilebilir. Önizleme sağlanan mantığı uyarıyı tetikleyen belirten koşul görselleştirme sinyal geçmişi birlikte gösterilir. Son olarak hangi süre için uyarı için belirtilen koşul seçerek görünmelidir belirtin **süresi** seçerek uyarı ne sıklıkla çalışmalı birlikte seçeneği **sıklığı**.
    ![Ölçüm için sinyal mantığını yapılandırın](./media/monitor-alerts-unified/AlertsPreviewCriteria.png)

7. *Ölçüm uyarıları*: durumunda sinyal olan bir ölçüm sonra uyarı pencere konusu Azure kaynağı için birden fazla veri noktası veya boyutları kullanarak filtre uygulanmış. Benzer şekilde ölçüm uyarıları, görselleştirme sinyal geçmişinin süresini belirterek seçilebilir **geçmişini göster** açılır. Ayrıca, seçilen ölçüm için boyutları için gereken zaman serisi filtrelemek için seçilebilir; Boyutları seçme isteğe bağlıdır ve yukarı-için beş boyutlar kullanılabilir. **Uyarı mantığı** koşul, toplama ve son olarak eşik gösterilen seçeneklerinden seçilebilir. Önizleme sağlanan mantığı geçmişte uyarının belirten koşul görselleştirme sinyal geçmişi birlikte gösterilir. Son olarak hangi süre için uyarı için belirtilen koşul seçerek görünmelidir belirtin **süresi** seçerek uyarı ne sıklıkla çalışmalı birlikte seçeneği **sıklığı**.
    ![Çok boyutlu ölçüm için sinyal mantığını yapılandırın](./media/monitor-alerts-unified/AlertsPreviewCriteriaMultiDim.png)

8. *Oturum uyarıları*: emin olun **kaynak türü** gibi analytics kaynağıdır *günlük analizi*, sonra bir kez uygun **kaynak** olan seçilen tıklatın*Bitti* düğmesi. Sonraki kullanmak **ölçüt eklemek** sinyal seçenekleri kaynağın ve sinyal listesinden kullanılabilir bir listesini görüntüle düğmesini **özel günlük arama** seçeneği.
   ![Bir kaynak - özel günlük arama seçin](./media/monitor-alerts-unified/AlertsPreviewResourceSelectionLog.png)

9.  *Oturum uyarıları*: içinde seçildikten sonra uyarı verme sorgu belirtilebilir **arama sorgusu** sorgu sözdizimi yanlışsa alan kırmızı hata görüntüler; alan. Sorgu Sözdizimi doğruysa - başvuru için belirtilen sorgu geçmiş verileri son altı saat zaman penceresinden geçen hafta için ince ayar seçeneğiyle bir grafik olarak gösterilir. 
   ![Uyarı kuralı yapılandırma](./media/monitor-alerts-unified/AlertsPreviewAlertLog.png)

    > [!NOTE]
    > Geçmiş verileri görselleştirme yalnızca sorgu sonuçlarını saati ayrıntıları varsa gösterilebilir. Sorgunuz özetlenmiş veri veya belirli sütun değerleri - sonuçlanırsa aynı tekil bir çizim gösterilir 

10.  *Oturum uyarıları*: Görselleştirme, yerinde ile **uyarı mantığı** koşul, toplama ve son olarak eşik gösterilen seçeneklerinden seçilebilir. Son olarak mantığında belirtmek için belirtilen koşul, değerlendirmek için zaman kullanarak **süresi** seçeneği. Seçerek uyarı ne sıklıkla çalışmalı birlikte **sıklığı**.
İçin **günlük uyarıları** uyarıları temel:
   - *Kayıt sayısı*: sorgu tarafından döndürülen kayıt sayısını daha büyük ya da sağlanan değerden daha az ise bir uyarı oluşturulur.
   - *Ölçüm ölçüm*: her değilse bir uyarı oluşturulur *toplama değeri* sonuçlarında sağlanan eşik değerini aşıyor ve bu *göre gruplandırılmış* değeri seçilir. Bir uyarı için dizi seçilen bir zaman diliminde eşiğini sayısıdır. Sonuç kümesi veya ihlallerini ardışık örnekler içinde gerçekleşmelidir gerektirecek şekilde ardışık ihlallerini arasında herhangi bir bileşimini ihlallerini için toplam ihlal belirtebilirsiniz.

   Daha fazla bilgi edinmek [günlük uyarılar ve bunların türleri](monitor-alerts-unified-log.md)

    > [!TIP]
    > Uyarıları (Önizleme) - günlük arama uyarıları şu anda özel sürebilir *süresi* ve *sıklığı* dakika değeri. Değerleri 1440 dakika (yani) 24 saat için 5 dakika arasında değişebilir. Uyarı dönemi deyin üç saat olmasını istiyorsanız, bu nedenle dönüştürmeden dakika içinde - kullanmadan önce 180 dakika

11. İkinci adım olarak, uyarı için bir ad tanımlayın **uyarı kuralı adı** alanı ile birlikte bir **açıklama** uyarı özellikleri ayrıntılı ve **önem** değeri sağlanan seçenekleri. Bu ayrıntılar tüm uyarı e-postalar, bildirimleri veya Azure İzleyici tarafından yapılan itme yeniden kullanılır. Kullanıcı uygun şekilde değiştirerek uyarı kuralı, oluşturulduktan hemen etkinleştirmeye ek olarak, seçebilir **etkinleştir kural oluşturulduktan sonra** seçeneği.

İçin **günlük uyarıları** yalnızca, bazı ek işlevler uyarı ayrıntıları kullanılabilir:
- *Uyarıları bastırma*: gizleme uyarı kuralı için etkinleştirdiğinizde, Eylemler kural için yeni bir uyarı oluşturduktan sonra tanımlı bir süre için devre dışı bırakılmış. Kural hala çalışıyor ve ölçütleri karşılanıyorsa sağlanan uyarı kayıtları oluşturur. Yinelenen eylemler çalıştırmadan sorunu düzeltmek için izin verme, süre.
    ![Günlük uyarılar için uyarıları bastırma](./media/monitor-alerts-unified/AlertsPreviewSuppress.png)

12. Üçüncü ve son adımı belirttiğiniz varsa **eylem grubu** Uyarı koşulu karşılandığında için uyarı kuralı tetiklenmesi gerekiyor. Varolan bir eylem grubu uyarı ile seçin veya yeni bir eylem grubu oluşturun. Uyarı tetikleyici Azure olur olduğunda göre eylem, seçili grubu: email(s) göndermek, SMS(s) göndermek, Webhook(s) çağrısı, Azure runbook'ları, anında iletme ITSM aracı, vb. kullanarak düzeltin. Daha fazla bilgi edinmek [Eylem grupları](monitoring-action-groups.md).

İçin **günlük uyarıları** varsayılan eylemleri geçersiz kılmak bazı ek işlevler kullanılabilir:
- *E-posta bildirimi*: eylem grubu gönderilen e-posta, bu geçersiz kılmaları konu. Posta gövdesini değiştiremezsiniz.
- *Özel Json yükünü dahil et*: Eylem grupları tarafından kullanılan Json Web kancası geçersiz kılar ve bunun yerine varsayılan yükü ile özel bir yükü Değiştir ![eylem günlüğü uyarılar için geçersiz kılar](./media/monitor-alerts-unified/AlertsPreviewOverrideLog.png)

13. Tüm alanlar geçerliyse ve yeşil onay **uyarı kuralı oluştur** düğmesini ve uyarı Azure İzleyicisi'nde - oluşturulan uyarılar (Önizleme). Tüm uyarıları uyarılar (Önizleme) panodan görüntülenebilir.
    ![Kural oluşturma](./media/monitor-alerts-unified/AlertsPreviewCreate.png)

Birkaç dakika içinde uyarı etkindir ve daha önce açıklandığı şekilde tetikler.

## <a name="view-your-alerts-in-azure-portal"></a>Azure Portalı'nda, uyarıları görüntüleme
1. İçinde [portal](https://portal.azure.com/)seçin **İzleyici** ve izleme bölümü altında - **uyarıları (Önizleme)**.  

2. **(Önizleme) Panosu uyarıları** görüntülenir - tüm Azure uyarıları birleşik ve tekil panosunda görüntülenir; burada görüntülerle ![uyarı Panosu](./media/monitoring-overview-unified/alerts-preview-overview.png)
1. Üst soldan sağa, Pano ayrıntılı listesini görmek için tıklattığınız aşağıdaki - bir bakışta gösterir:
    - *Uyarıları harekete*: mantığı karşılanır ve içinde durum harekete uyarılar şu anda sayısı
    - *Toplam uyarı kuralları*: oluşturulan uyarı kuralları ve alt, şu an etkin olan numarasını sayısı
2. Tüm Mazotlu uyarıların bir listesi, kullanıcının ayrıntılarını görüntülemek için tıklatabileceği gösterilir
3. Bulma özel uyarıları kuruluşlara yardımcı olmaktayız; bir kullanabileceğiniz üstteki açılan seçenekleri belirli filtreleme için *abonelik, kaynak grubu ve/veya kaynak*. Herhangi bir çözümlenmemiş uyarı için bir kullanım başka *filtre uyarı* seçeneği bulmak için sağlanan anahtar - belirli eşleşen uyarılarla *adı, Uyarı ölçütleri, kaynak grubu ve hedef kaynak*

## <a name="managing-your-alerts-in-azure-portal"></a>Azure portalında, Uyarıları yönetme
1. İçinde [portal](https://portal.azure.com/)seçin **İzleyici** ve izleme bölümü altında - **uyarıları (Önizleme)**.  
2. Seçin **yönetmek kuralları** düğmesini oluşturulan tüm uyarı kuralları burada listelenen kural Yönetimi bölümüne - gitmek için üst çubukta; devre dışı bırakılmış uyarıları dahil olmak üzere.
3. Belirli uyarı kuralları için bulmak için bir ya da aşağı açılan filtreleri shortlist uyarı kuralları için özel izin üstteki kullanabilirsiniz *abonelik, kaynak grupları ve/veya kaynak*. Uyarı kuralı listesinin bölmesi arama'yı kullanarak alternatif olarak işaretlenmiş *filtre uyarıları*, bir karşı eşleşen anahtar sözcüğü sağlayabilir *uyarı adı, koşul ve hedef kaynak*; yalnızca görüntülemek için eşleştirme kuralları. 
   ![Uyarı kurallarını yönetme](./media/monitoring-overview-unified/alerts-preview-rules.png)
4. Görüntülemek veya belirli uyarı kuralı değiştirmek için tıklatılabilir bir bağlantı gösterilen adını tıklatın.
5. Tanımlanan uyarısı gösterilir - üç aşama yapısındaki: 1) Uyarı koşulu 2) uyarı ayrıntı 3) eylem grubu. **Hedef ölçütleri** uyarı mantığı ya da yeni bir değişiklik için tıklattığınız ölçütleri önceki mantığı silmek için Kutusu'nu kullandıktan sonra eklenebilir. Benzer şekilde, uyarı Ayrıntıları bölümünde - **açıklama** ve **önem** değiştirilebilir. Eylem grubunu değiştirilebilir ve yeni bir uyarı kullanmaya bağlama için hazırlanmış **yeni eylem grubu** düğmesini ![uyarı kuralı Değiştir](./media/monitor-alerts-unified/AlertsPreviewEdit.png)
6. Üst panelde kullanarak, değişiklikler uyarıya yansıtıcı dahil olabilir: *kaydetmek* uyarı için yapılan değişiklikleri yürütmek için *atmak* uyarı için yapılan tüm değişiklikleri kaydetmeden geri dönmek için *devre dışı bırak*  olacağı artık çalışır veya herhangi bir eylemi tetikleyen uyarı - devre dışı bırakmak için. Ve son olarak, *silmek* tüm uyarı kuralı Azure'dan kalıcı olarak kaldırmak için.

## <a name="next-steps"></a>Sonraki adımlar

* Yeni hakkında daha fazla bilgi [yakın gerçek zamanlı ölçüm uyarıları (Önizleme)](monitoring-near-real-time-metric-alerts.md)
* Alma bir [ölçümleri toplama genel bakış](insights-how-to-customize-monitoring.md) hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin olmak için.
* Hakkında bilgi edinin [günlük uyarıları Azure uyarılar (Önizleme)](monitor-alerts-unified-log.md)
