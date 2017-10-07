---
title: "Azure mantığı uygulamalardan aaaConnect tooDynamics 365 (çevrimiçi) | Microsoft Docs"
description: "Dynamics 365 (çevrimiçi) varlıklar hello hello Dynamics 365 Bağlayıcısı tarafından sağlanan API aracılığıyla yönetmek uygulama iş akışları mantığı oluşturun"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a>Mantıksal uygulama akışlarından tooDynamics 365 Bağlan

Logic Apps ile tooDynamics (çevrimiçi) 365 bağlama ve kayıtları oluşturma, öğeleri güncelleştirmek veya kayıtlar listesi döndüren kullanışlı iş akışları oluşturma. Merhaba Dynamics 365 Bağlayıcısı ile şunları yapabilirsiniz:

* İş akışınız hello verileri (çevrimiçi) Dynamics 365 Al esas oluşturun.
* Bir yanıt ve daha sonra hello çıkış diğer eylemler için kullanılabilir hale eylemlerini kullanın. Örneğin, bir öğe Dynamics 365'te (çevrimiçi) güncelleştirildiğinde, Office 365 kullanılarak bir e-posta gönderebilirsiniz.

Bu konu, nasıl toocreate bir mantıksal uygulama, bir görev Dynamics 365 oluşturduğunu gösterir. yeni bir sağlama Dynamics 365 oluşturulduğu zaman.

## <a name="prerequisites"></a>Ön koşullar
* Bir Azure hesabı.
* Dynamics 365 (çevrimiçi) hesabı.

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a>Yeni bir sağlama Dynamics 365'te oluşturduğunuzda bir görev oluşturma

1.  [İçinde tooAzure oturum](https://portal.azure.com).

2.  Hello Azure arama kutusuna yazın `Logic apps`, ve ENTER tuşuna basın.

      ![Logic Apps Bul](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  Altında **Logic apps**, tıklatın **Ekle**.

      ![LogicApp Ekle](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  toocreate hello mantıksal uygulama, tam hello **adı**, **abonelik**, **kaynak grubu**, ve **konumu** alanları ve 'ıtıklatın **Oluşturma**.

5.  Merhaba yeni mantıksal uygulama seçin. Merhaba aldığınızda **dağıtımı başarılı oldu** bildirimi tıklatın **yenileme**.

6.  Altında **geliştirme araçları**, tıklatın **mantığı Uygulama Tasarımcısı**. Merhaba şablon listesinde tıklayın **boş mantıksal uygulama**.

7.  Merhaba arama kutusuna yazın `Dynamics 365`. Hello Dynamics 365 listesi tetikler, seçin **Dynamics 365 bir kayıt oluşturulduğunda –**.

8.  İstendiğinde toosign tooDynamics 365 de varsa, bunu şimdi yapın.

9.  Aşağıdaki bilgilerle hello Hello tetikleyici ayrıntıları girin:

  * **Kuruluş adı**. Merhaba mantığı uygulama toolisten istediğiniz hello Dynamics 365 örneği seçin.

  * **Varlık adı**. Toolisten için istediğiniz hello varlığı seçin. Bu olay bir tetikleyici toostart hello mantıksal uygulama davranır. 
  Bu kılavuzda **müşteri adayları** seçilir.

  * **Ne sıklıkta toocheck öğeleri istiyor musunuz?** Bu değerleri ne sıklıkta ayarlayın hello mantıksal uygulama güncelleştirmeleri ilgili toohello tetikleyici için denetler. güncelleştirmeleri üç dakikada toocheck Hello varsayılan ayardır.

    * **Sıklık**. Saniye, dakika, saat veya gün seçin.

    * **Aralığı**. Merhaba saniye, dakika, saat veya toopass hello sonraki onay önce istediğiniz gün sayısını girin.

      ![Mantıksal uygulama tetikleyici ayrıntıları](./media/connectors-create-api-crmonline/trigger-details.png)

10. Tıklatın **yeni adım**ve ardından **Eylem Ekle**.

11. Merhaba arama kutusuna yazın `Dynamics 365`. Merhaba eylemler listesinden **Dynamics 365 – yeni bir kayıt oluşturmak**.

12. Aşağıdaki bilgilerle hello girin:

    * **Kuruluş adı**. Merhaba Dynamics 365 örneği hello akış toocreate hello kaydetmek istediğiniz yeri seçin. 
    Bu örnek aynı hello toobe yok bildirim burada hello olay tetiklenir gelen örneği.

    * **Varlık adı**. Merhaba olay tetiklendiğinde toocreate bir kaydı istediğiniz hello varlığı seçin. 
    Bu kılavuzda **görevleri** seçilir.

13. Tıklatın hello **konu** görüntülenen kutusunda. Görüntülenen hello dinamik içerik listesinden, bu alanlardan birini seçebilirsiniz:

    * **Soyadı**. Merhaba görev kayıt oluşturulduğunda bu alanın seçilmesi hello görevin hello Konu alanına hello Soyadı hello sağlama için ekler.
    * **Konu**. Bu alan ekler hello konu alan hello görevin hello Konu alanına hello sağlama için seçerek, ne zaman hello görev kaydı oluşturulur. 
    Tıklatın **konu** tooadd bu toohello **konu** kutusu.

      ![Mantıksal uygulama oluşturma yeni kayıt ayrıntıları](./media/connectors-create-api-crmonline/create-record-details.png)

14. Merhaba mantığı uygulama Designer araç çubuğundan, **kaydetmek**.

    ![Mantıksal Uygulama Tasarımcısı araç Kaydet](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. toostart hello mantıksal uygulama'ı tıklatın **çalıştırmak**.

    ![Mantıksal Uygulama Tasarımcısı araç Kaydet](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. Artık Dynamics 365 satış sağlama kaydı oluşturun ve akışınız eylem bakın!

## <a name="set-advanced-options-for-a-logic-app-step"></a>Bir mantıksal uygulama adımı için Gelişmiş seçenekleri ayarlama

bir mantıksal uygulama adımı toofilter verileri nasıl tıklatın toospecify **Gelişmiş Seçenekleri Göster** sorgu tarafından filtre veya düzeni sonra bu adımda, ekleyin.

Örneğin, bir filtre sorgu tooget yalnızca etkin hesapları kullanın ve hello hesap adıyla sipariş. tooperform bu görev, hello OData filtre sorgusu girin `statuscode eq 1`seçip **hesap adı** hello dinamik içerik listesinden. Daha fazla bilgi: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) ve [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).

![Gelişmiş Seçenekleri mantıksal uygulama](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a>Gelişmiş seçenekleri kullanırken en iyi uygulamalar

Değer tooa alanı eklediğinizde, bir değer yazın ya da hello dinamik içerik listeden bir değer seçin hello alan türüyle eşleşmelidir.

Alan türü  |Nasıl toouse  |Burada toofind  |Ad  |Veri türü  
---------|---------|---------|---------|---------
Metin alanları|Metin alanları tek satırlık bir metin veya metin türü alan dinamik içerik gerektirir. Örnekler hello kategori ve alt kategori alanları içerir.|Ayarlar > özelleştirmeleri > Özelleştir hello Sistem > varlıklar > Görev > alanları |category |Tek satırlık metin        
Tamsayı alanları | Bazı alanlar, tamsayı veya tamsayı türünde bir alan dinamik içerik gerektirir. Örnek tamamlanma yüzdesi ve süre verilebilir. |Ayarlar > özelleştirmeleri > Özelleştir hello Sistem > varlıklar > Görev > alanları |TamamlanmaYüzdesi |Tam sayı         
Tarih alanları | Bazı alanlar, tarih gg/aa/yyyy biçiminde veya bir tarih alanı dinamik içerik girilmesini gerektirir. Oluşturma tarihi, başlangıç tarihi, gerçek başlatma, son zaman tutun, gerçek bitiş ve son tarih örnekler. | Ayarlar > özelleştirmeleri > Özelleştir hello Sistem > varlıklar > Görev > alanları |createdon |Tarih ve saat
Bir kayıt kimliği hem arama gerektiren alanlar yazın |Başka bir varlık kaydı başvuru bazı alanları hello kayıt kimliği ve hello arama türü gerektirir. |Ayarlar > özelleştirmeleri > Özelleştir hello Sistem > varlıklar > hesabı > alanları  | Hesap Kimliği  | Birincil anahtar

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a>Daha fazla örnekleri bir kayıt kimliği ve arama gerektiren alanlar yazın
Önceki tabloda Hello genişleterek, daha fazla hello dinamik içerik listeden seçilen değerlerle çalışmıyor alanları örnekleri aşağıda verilmiştir. Bunun yerine, bu alanların PowerApps hello alanlarına girilen hem bir kayıt kimliği ve arama türü gerektirir.  
* Sahibi ve sahip türü. Merhaba sahibi alan geçerli bir kullanıcı veya takım kayıt kimliği olmalıdır Merhaba sahip türü ya da olmalıdır **systemusers** veya **takımlar**.
* Müşteri ve müşteri türü. Merhaba müşteri alan geçerli bir hesap olması veya kayıt kimliği başvurun Merhaba sahip türü ya da olmalıdır **hesapları** veya **kişiler**.
* İlgili ve ilgili türü. Merhaba alan ilgili bir hesap gibi bir geçerli kayıt kimliği olması veya kayıt kimliği başvurun Merhaba ilgili türü hello kaydına hello arama türü gibi olmalıdır **hesapları** veya **kişiler**.

Merhaba aşağıdaki görev oluşturma eylem örneği hello görev alanının ilgili toohello ekleme toohello kayıt Kimliğine karşılık gelen bir hesap kaydı ekler.

![Akış RecordID ve türü hesabı](./media/connectors-create-api-crmonline/recordid-type-account.png)

Bu örnek ayrıca hello kullanıcının kaydı kimliğine göre hello görev tooa belirli bir kullanıcı atar

![Akış RecordID ve türü hesabı](./media/connectors-create-api-crmonline/recordid-type-user.png)

toofind bir kayıt kimliği, kullanıcının bölümden hello bkz: *Bul hello kayıt kimliği*

## <a name="find-hello-record-id"></a>Merhaba kayıt kimliği bulunamıyor

1. Hesap kaydı gibi bir kaydı açın.

2. Merhaba Eylemler araç çubuğunda tıklatın **öne çıkar** ![açılan kayıt](./media/connectors-create-api-crmonline/popout-record.png).
Alternatif olarak, hello Eylemler araç çubuğunda, varsayılan e-posta programınız içine toocopy hello tam URL'yi tıklatın **e-posta A bağlantı**.

   Merhaba kayıt kimliği hello URL'nin karakter kodlama hello 7b ve %7 %d Between görüntülenir.

   ![Akış RecordID ve türü hesabı](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a>Sorun giderme
bir mantıksal uygulama, görünüm hello durum hello olay ayrıntılarını başarısız bir adımda tootroubleshoot.

1. Altında **Logic Apps**, mantıksal uygulamanızı seçin ve ardından **genel bakış**. 

   Merhaba Özet alanı gösterilir ve hello mantıksal uygulama için Çalıştır hello durumunu sağlar. 

   ![Mantıksal uygulama çalışma durumu](./media/connectors-create-api-crmonline/tshoot1.png)

2. tooview herhangi başarısız çalışmaları hakkında daha fazla bilgi tıklatın başarısız hello olay. tooexpand başarısız adımı bu adımı'ı tıklatın.

   ![Başarısız olan adımda genişletin](./media/connectors-create-api-crmonline/tshoot2.png)

   Merhaba adım ayrıntıları görünür ve hello hatanın nedenini hello gidermenize yardımcı olacak.

   ![Adım ayrıntıları başarısız oldu](./media/connectors-create-api-crmonline/tshoot3.png)

Logic apps sorunlarını giderme hakkında daha fazla bilgi için bkz: [mantığı uygulama hatalarını tanılama](../logic-apps/logic-apps-diagnosing-failures.md).

## <a name="connector-specific-details"></a>Bağlayıcı özgü ayrıntıları

Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/crm/). 

## <a name="next-steps"></a>Sonraki adımlar
Araştır Logic Apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).
