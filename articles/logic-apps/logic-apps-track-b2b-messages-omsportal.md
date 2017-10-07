---
title: Operations Management Suite - Azure Logic Apps aaaTrack B2B iletilerinde | Microsoft Docs
description: "B2B iletişimi tümleştirme hesabı ve mantığı uygulamalarınız için Azure günlük analizi ile Operations Management Suite (OMS) içinde izleme"
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
ms.openlocfilehash: f385a72008b19408bb45d61c440df0505b688175
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="track-b2b-communication-in-hello-microsoft-operations-management-suite-oms"></a>Microsoft Operations Management Suite (OMS) hello B2B iletişiminde izleme

İkisi arasındaki B2B iletişim kurduktan sonra iş süreçlerini veya tümleştirme hesabınızı aracılığıyla uygulamaları çalıştıran bu varlıkların birbirleriyle iletileri değiştirebilir. toocheck bu iletiler doğru olarak işlenir, AS2, X12, izleyebilir ve EDIFACT iletileri ile olup olmadığını [Azure günlük analizi](../log-analytics/log-analytics-overview.md) hello içinde [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Örneğin, iletileri izlemek için bu izleme web tabanlı özellikleri kullanabilirsiniz:

* İleti sayısı ve durumu
* İlgili kaynaklar durumu
* İlgili kaynaklar ile iletileri ilişkilendirmek
* Hataları için ayrıntılı hata açıklaması
* Arama özellikleri

## <a name="requirements"></a>Gereksinimler

* Tanılama Günlüğü ile ayarlanmış bir mantıksal uygulama. Bilgi [nasıl toocreate bir mantıksal uygulama](logic-apps-create-a-logic-app.md) ve [nasıl tooset bu mantıksal uygulama günlüklerini](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* İzleme ve günlük ile ayarlanan bir tümleştirme hesabı. Bilgi [nasıl toocreate bir tümleştirme hesap](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) ve [nasıl izleme ve o hesap için oturum tooset](../logic-apps/logic-apps-monitor-b2b-message.md).

* Henüz yapmadıysanız [tanılama veri tooLog Analytics yayımlama](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) OMS içinde.

> [!NOTE]
> Merhaba önceki gereksinimlerini karşılamanızın sonra hello çalışma olmalıdır [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Kullanmanız gereken Merhaba, OMS B2B iletişiminde izleme için aynı OMS çalışma. 
>  
> Bir OMS çalışma alanı yoksa, bilgi [nasıl toocreate bir OMS çalışma](../log-analytics/log-analytics-get-started.md).

## <a name="add-hello-logic-apps-b2b-solution-toohello-operations-management-suite-oms"></a>Merhaba Logic Apps B2B çözüm toohello Operations Management Suite (OMS) Ekle

toohave OMS B2B iletileri mantığı uygulamanız için izleme, hello eklemelisiniz **Logic Apps B2B** çözüm toohello OMS portalı. Daha fazla bilgi edinmek [çözümleri tooOMS ekleme](../log-analytics/log-analytics-get-started.md).

1. Merhaba, [Azure portal](https://portal.azure.com), seçin **daha Hizmetleri**. "İçin günlük analizi" araması yapın ve ardından **günlük analizi** aşağıda gösterildiği gibi:

   ![Günlük analizi Bul](media/logic-apps-track-b2b-messages-omsportal/browseloganalytics.png)

2. Altında **günlük analizi**, bulma ve OMS çalışma alanınızı seçin. 

   ![OMS çalışma alanınızı seçin](media/logic-apps-track-b2b-messages-omsportal/selectla.png)

3. Altında **Yönetim**, seçin **OMS portalı**.

   ![OMS portalı seçin](media/logic-apps-track-b2b-messages-omsportal/omsportalpage.png)

4. Merhaba OMS giriş sayfası açıldıktan sonra Seç **Çözümleri Galerisi**.    

   ![Çözümleri Galerisi seçin](media/logic-apps-track-b2b-messages-omsportal/omshomepage1.png)

5. Altında **tüm çözümleri**, bulun ve seçin **Logic Apps B2B**.     

   ![Logic Apps B2B seçin](media/logic-apps-track-b2b-messages-omsportal/omshomepage2.png)

6. Altında **Logic Apps B2B**, seçin **Ekle**.

   ![Seçin ekleme](media/logic-apps-track-b2b-messages-omsportal/omshomepage3.png)

   Bölme için Hello OMS giriş sayfasında hello **Logic Apps B2B iletileri** artık görünür. 
   B2B iletilerinizi işlendiğinde bu kutucuğu hello ileti sayısı güncelleştirir.

   ![OMS giriş sayfası, Logic Apps B2B iletileri döşeme](media/logic-apps-track-b2b-messages-omsportal/omshomepage4.png)

<a name="message-status-details"></a>

## <a name="track-message-status-and-details-in-hello-operations-management-suite"></a>İleti durumu ve ayrıntıları hello Operations Management Suite izleme

1. B2B iletilerinizi işlendikten sonra hello durumunu ve bu iletileri ayrıntılarını görüntüleyebilirsiniz. Merhaba Hello OMS giriş sayfasında, seçin **Logic Apps B2B iletileri** döşeme.

   ![Güncelleştirilmiş ileti sayısı](media/logic-apps-track-b2b-messages-omsportal/omshomepage6.png)

   > [!NOTE]
   > Varsayılan olarak, hello **Logic Apps B2B iletileri** döşeme tek bir günde göre verileri gösterir. toochange hello veri tooa farklı aralığı, kapsam hello kapsam denetim hello sayfanın üst kısmındaki hello OMS seçin:
   > 
   > ![Veri Kapsamı Değiştir](media/logic-apps-track-b2b-messages-omsportal/change-interval.png)
   >

2. Pano tarafından görünür Hello ileti durumu sonra verileri tek bir gün bazında gösteren bir belirli bir ileti türü için daha fazla bilgi görüntüleyebilirsiniz. Merhaba bölme için seçin **AS2**, **X12**, veya **EDIFACT**.

   ![İleti durumunu görüntüle](media/logic-apps-track-b2b-messages-omsportal/omshomepage5.png)

   Seçilen bölme için iletilerinin bir listesi görüntülenir. 
   her ileti türü için hello özellikleri hakkında daha fazla toolearn bu ileti özelliği açıklamalar bakın:

   * [AS2 ileti özellikleri](#as2-message-properties)
   * [X12 ileti özelliklerinin](#x12-message-properties)
   * [EDIFACT ileti özellikleri](#EDIFACT-message-properties)

   Örneğin, işte AS2 ileti listesi aşağıdaki gibi görünmelidir:

   ![AS2 iletilerini görüntüleme](media/logic-apps-track-b2b-messages-omsportal/as2messagelist.png)

3. tooview veya dışarı aktarma hello girişleri ve çıkışları belirli iletileri için bu iletileri seçin ve **karşıdan**. İstendiğinde, hello .zip dosya tooyour yerel bilgisayara kaydedin ve sonra o dosyasını ayıklayın. 

   Merhaba ayıklanan klasörü, seçilen her ileti için bir klasör içerir. 
   Onayları ayarlarsanız, hello ileti klasörünü bildirim ayrıntılarla dosyalarını da içerir. 
   Her ileti klasörün en az bu dosyaları vardır: 
   
   * Merhaba okunabilir dosyalarıyla yükü ve çıktı yükü ayrıntıları giriş
   * Merhaba girişleri ve çıkışları ile kodlanmış dosyalar

   Her ileti türü için hello klasör ve dosya adı biçimleri burada bulabilirsiniz:

   * [AS2 klasör ve dosya adı biçimleri](#as2-folder-file-names)
   * [X12 klasör ve dosya adı biçimleri](#x12-folder-file-names)
   * [EDIFACT klasör ve dosya adı biçimleri](#edifact-folder-file-names)

   ![İleti dosyaları indirme](media/logic-apps-track-b2b-messages-omsportal/download-messages.png)

4. tooview aynı hello tüm eylemleri çalıştırmak kimliği üzerinde hello **günlük arama** sayfasında, bir ileti hello ileti listesinden seçin.

   Bu eylemler sütun ya da belirli sonuçları Ara sıralayabilirsiniz.

   ![Merhaba eylemlerle aynı kimliği çalıştırın](media/logic-apps-track-b2b-messages-omsportal/logsearch.png)

   * önceden oluşturulmuş sorgularla toosearch sonuçları seçin **Sık Kullanılanlar**.

   * Bilgi [filtreleri ekleyerek toobuild nasıl sorgular](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md). 
   Veya daha fazla bilgi edinmek [nasıl günlük toofind verilerle günlük analizi arama](../log-analytics/log-analytics-log-searches.md).

   * Merhaba arama kutusuna, filtre olarak toouse istediğiniz güncelleştirme hello sorgusu hello sütunlar ve değerler ile toochange sorgu.

<a name="message-list-property-descriptions"></a>

## <a name="property-descriptions-and-name-formats-for-as2-x12-and-edifact-messages"></a>Özellik açıklamaları adı için ve biçimleri AS2, X 12 ve EDIFACT iletileri

Her ileti türü için hello özellik açıklamalarını ve indirilen ileti dosyaları için ad biçimleri aşağıda verilmiştir.

<a name="as2-message-properties"></a>

### <a name="as2-message-property-descriptions"></a>AS2 ileti özellik açıklamaları

Burada, her AS2 ileti için hello özellik açıklamaları bulunmaktadır.

| Özellik | Açıklama |
| --- | --- |
| Gönderen | Belirtilen hello Konuk iş ortağı **alma ayarı**, veya hello ana iş ortağı belirtilen **gönderme ayarları** AS2 sözleşmesi için |
| Alıcı | Belirtilen hello ana iş ortağı **alma ayarı**, veya hello Konuk iş ortağı belirtilen **gönderme ayarları** AS2 sözleşmesi için |
| Logic App | Merhaba mantıksal uygulama hello AS2 Eylemler burada ayarlama |
| Durum | Merhaba AS2 ileti durumu <br>Başarı alınan = ya da geçerli bir AS2 iletisi gönderdi. Hiçbir MDN ayarlayın. <br>Başarı alınan = ya da geçerli bir AS2 iletisi gönderdi. MDN ayarlama ve alınan veya MDN gönderilir. <br>Başarısız alınan geçersiz bir AS2 ileti =. Hiçbir MDN ayarlayın. <br>Bekleyen alınan = ya da geçerli bir AS2 iletisi gönderdi. MDN ayarlama ve MDN beklenir. |
| ACK | Merhaba MDN ileti durumu <br>Kabul alınan = ya da pozitif MDN gönderilir. <br>Bekleyen = tooreceive bekliyor veya bir MDN gönderin. <br>Reddedilen alınan = ya da negatif MDN gönderilir. <br>Gerekli değil = MDN ayarlı değil hello anlaşmasında. |
| Yön | Merhaba AS2 ileti yönü |
| Bağıntı Kimliği | Tüm hello tetikleyiciler ve Eylemler bir mantıksal uygulama içinde karşılık gelen hello kimliği |
| İleti kimliği | Merhaba AS2 ileti üstbilgilerini Hello AS2 ileti kimliği |
| zaman damgası | Merhaba zaman zaman hello AS2 eylemin hello ileti işleme |
|          |             |

<a name="as2-folder-file-names"></a>

### <a name="as2-name-formats-for-downloaded-message-files"></a>İndirilen ileti dosyaları için AS2 adı biçimleri

Her indirilen AS2 ileti klasör ve dosyaları hello adı biçimler şunlardır.

| Klasör veya dosya | Ad biçimi |
| :------------- | :---------- |
| İleti klasörü | [Gönderen] \_[Alıcı]\_AS2\_[correlation-ID]\_[ileti kimliği]\_[zaman damgası] |
| Giriş, çıkış ve bildirim dosyaları, ayarlanmışsa | **Giriş yükü**: [Gönderen]\_[Alıcı]\_AS2\_[correlation-ID]\_input_payload.txt </p>**Çıktı yükü**: [Gönderen]\_[Alıcı]\_AS2\_[correlation-ID]\_çıkış\_payload.txt </p></p>**Girişleri**: [Gönderen]\_[Alıcı]\_AS2\_[correlation-ID]\_inputs.txt </p></p>**Çıkış**: [Gönderen]\_[Alıcı]\_AS2\_[correlation-ID]\_outputs.txt |
|          |             |

<a name="x12-message-properties"></a>

### <a name="x12-message-property-descriptions"></a>Özellik açıklamaları X12 iletisi

Her X12 hello özellik açıklamalarını İşte ileti.

| Özellik | Açıklama |
| --- | --- |
| Gönderen | Belirtilen hello Konuk iş ortağı **alma ayarı**, veya hello ana iş ortağı belirtilen **gönderme ayarları** bir X12 için Sözleşmesi |
| Alıcı | Belirtilen hello ana iş ortağı **alma ayarı**, ya da belirtilen hello Konuk iş ortağı **gönderme ayarları** bir X12 için Sözleşmesi |
| Logic App | Merhaba mantıksal uygulama hello X12 Eylemler burada ayarlama |
| Durum | Merhaba X12 ileti durumu <br>Başarı alınan = ya da geçerli X12 gönderilen ileti. Hiçbir işlev ack ayarlayın. <br>Başarı alınan = ya da geçerli X12 gönderilen ileti. İşlev ack ayarlama ve alınan veya işlevsel bir ack gönderilir. <br>Başarısız alınan = ya da geçersiz bir X12 gönderilen ileti. <br>Bekleyen alınan = ya da geçerli X12 gönderilen ileti. İşlev ack ayarlama ve işlevsel bir ack beklenir. |
| ACK | İşlev Ack (997) durumu <br>Kabul alınan = ya da pozitif bir işlev bildirim gönderildi <br>Reddedilen alınan = veya negatif bir işlev bildirim gönderildi <br>Bekleyen bir işlev onayı bekleniyor = ancak alınmadı. <br>İşlevsel bir ack = oluşturulan ancak toopartner gönderemez. <br>Gerekli değil işlevsel = ack ayarlı değil. |
| Yön | Merhaba X12 ileti yönü |
| Bağıntı Kimliği | Tüm hello tetikleyiciler ve Eylemler bir mantıksal uygulama içinde karşılık gelen hello kimliği |
| Msg türü | Merhaba EDI X 12 ileti türü |
| ICN | Merhaba değişim kontrol numarası hello X12 iletisi |
| TSCN | Merhaba X12 ileti Merhaba işlem kümesi denetim sayısı |
| zaman damgası | Merhaba zaman zaman hello X12 eylemin hello ileti işleme |
|          |             |

<a name="x12-folder-file-names"></a>

### <a name="x12-name-formats-for-downloaded-message-files"></a>X12 biçimleri için indirilen ileti dosyası adı

Merhaba adı biçimler şunlardır her X12 yüklenen ileti klasör ve dosyaları.

| Klasör veya dosya | Ad biçimi |
| :------------- | :---------- |
| İleti klasörü | [Gönderen] \_[Alıcı]\_X12\_[Değişim Denetimi numarası]\_[genel denetim-numarası]\_[işlem-set-denetim-number]\_[zaman damgası] |
| Giriş, çıkış ve bildirim dosyaları, ayarlanmışsa | **Giriş yükü**: [Gönderen]\_[Alıcı]\_X12\_[Değişim Denetimi numarası]\_input_payload.txt </p>**Çıktı yükü**: [Gönderen]\_[Alıcı]\_X12\_[Değişim Denetimi numarası]\_çıkış\_payload.txt </p></p>**Girişleri**: [Gönderen]\_[Alıcı]\_X12\_[Değişim Denetimi numarası]\_inputs.txt </p></p>**Çıkış**: [Gönderen]\_[Alıcı]\_X12\_[Değişim Denetimi numarası]\_outputs.txt |
|          |             |

<a name="EDIFACT-message-properties"></a>

### <a name="edifact-message-property-descriptions"></a>EDIFACT ileti özellik açıklamaları

Burada, her EDIFACT ileti için hello özellik açıklamaları bulunmaktadır.

| Özellik | Açıklama |
| --- | --- |
| Gönderen | Belirtilen hello Konuk iş ortağı **alma ayarı**, veya hello ana iş ortağı belirtilen **gönderme ayarları** EDIFACT sözleşmesi için |
| Alıcı | Belirtilen hello ana iş ortağı **alma ayarı**, veya hello Konuk iş ortağı belirtilen **gönderme ayarları** EDIFACT sözleşmesi için |
| Logic App | Merhaba mantıksal uygulama hello EDIFACT Eylemler burada ayarlama |
| Durum | Merhaba EDIFACT ileti durumu <br>Başarı alınan = ya da geçerli bir EDIFACT iletisi gönderdi. Hiçbir işlev ack ayarlayın. <br>Başarı alınan = ya da geçerli bir EDIFACT iletisi gönderdi. İşlev ack ayarlama ve alınan veya işlevsel bir ack gönderilir. <br>Başarısız alınan = ya da geçersiz bir EDIFACT ileti gönderildi <br>Bekleyen alınan = ya da geçerli bir EDIFACT iletisi gönderdi. İşlev ack ayarlama ve işlevsel bir ack beklenir. |
| ACK | İşlev Ack (997) durumu <br>Kabul alınan = ya da pozitif bir işlev bildirim gönderildi <br>Reddedilen alınan = veya negatif bir işlev bildirim gönderildi <br>Bekleyen bir işlev onayı bekleniyor = ancak alınmadı. <br>İşlevsel bir ack = oluşturulan ancak toopartner gönderemez. <br>Gerekli değil = işlevsel Ack ayarlı değil. |
| Yön | Merhaba EDIFACT ileti yönü |
| Bağıntı Kimliği | Tüm hello tetikleyiciler ve Eylemler bir mantıksal uygulama içinde karşılık gelen hello kimliği |
| Msg türü | Merhaba EDIFACT ileti türü |
| ICN | Merhaba değişim kontrol numarası hello EDIFACT iletisi |
| TSCN | Merhaba EDIFACT ileti Merhaba işlem kümesi denetim sayısı |
| zaman damgası | Merhaba zaman zaman hello EDIFACT eylemin hello ileti işleme |
|          |               |

<a name="edifact-folder-file-names"></a>

### <a name="edifact-name-formats-for-downloaded-message-files"></a>İndirilen ileti dosyaları için EDIFACT adı biçimleri

Her indirilen EDIFACT ileti klasör ve dosyaları hello adı biçimler şunlardır.

| Klasör veya dosya | Ad biçimi |
| :------------- | :---------- |
| İleti klasörü | [Gönderen] \_[Alıcı]\_EDIFACT\_[Değişim Denetimi numarası]\_[genel denetim-numarası]\_[işlem-set-denetim-number]\_[zaman damgası] |
| Giriş, çıkış ve bildirim dosyaları, ayarlanmışsa | **Giriş yükü**: [Gönderen]\_[Alıcı]\_EDIFACT\_[Değişim Denetimi numarası]\_input_payload.txt </p>**Çıktı yükü**: [Gönderen]\_[Alıcı]\_EDIFACT\_[Değişim Denetimi numarası]\_çıkış\_payload.txt </p></p>**Girişleri**: [Gönderen]\_[Alıcı]\_EDIFACT\_[Değişim Denetimi numarası]\_inputs.txt </p></p>**Çıkış**: [Gönderen]\_[Alıcı]\_EDIFACT\_[Değişim Denetimi numarası]\_outputs.txt |
|          |             |

## <a name="next-steps"></a>Sonraki adımlar

* [Operations Management Suite B2B iletiler için sorgu](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)
* [AS2 izleme şemaları](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [X12 izleme şemaları](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Özel İzleme şemaları](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)