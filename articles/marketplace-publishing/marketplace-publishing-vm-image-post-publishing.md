---
title: "Sanal makineniz hello Azure Market görüntü aaaManaging | Microsoft Docs"
description: "Nasıl toomanage sanal makineniz görüntü hello Azure Marketi sonra ilk yayın üzerinde ayrıntılı kılavuz"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: cc8648d4-59c2-4678-b47d-992300677537
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/03/2016
ms.author: hascipio;
ms.openlocfilehash: 47a082e686e1248ceacb844d3c0f2f5c33133dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="post-production-guide-for-virtual-machine-offers-in-hello-azure-marketplace"></a>Sanal makine için sonrası üretim Kılavuzu hello Azure Market sunar
Bu makalede, bir dinamik sanal makine teklif hello Azure Marketi'nde nasıl güncelleştirebileceğinizi açıklanmaktadır. Bu, bir veya daha fazla yeni SKU'ları tooan varolan teklif ekleme hello işleminde size rehberlik eder. Bu da dinamik sanal makine teklif veya SKU Market hello kaldırmanın hello sürecinde size kılavuzluk.

Bir teklif/SKU hello hazırlanan sonra [Azure portal](http://portal.azure.com), metin kutuları aşağıdaki hello değiştiremezsiniz:

* **Tanımlayıcı teklif**: hello portal, yayımlama Git çok**sanal makineleri** ve teklifiniz seçin. Ardından **VM GÖRÜNTÜLERİ** > **teklif tanımlayıcı**.
* **SKU tanımlayıcı**: hello portal, yayımlama Git çok**sanal makineleri** ve teklifiniz seçin. Ardından **SKU'ları** > **bir SKU eklemek**.
* **Yayımcı Namespace**: hello portal, yayımlama Git çok**sanal makineleri** > **izlenecek** > **söyleyin bize hakkında şirketiniz** ("Adım 2 kayıt şirketiniz altında" bulunur) > **yayımcı Namespace** > **Namespace**.

Merhaba teklif/SKU hello listelenen sonra [Market](http://azure.microsoft.com/marketplace), metin kutuları aşağıdaki hello değiştiremezsiniz:

* **Tanımlayıcı teklif**: hello portal, yayımlama Git çok**sanal makineleri** ve teklifiniz seçin. Ardından **VM GÖRÜNTÜLERİ** > **teklif tanımlayıcı**.
* **SKU tanımlayıcı**: hello portal, yayımlama Git çok**sanal makineleri** ve teklifiniz seçin. Ardından **SKU'ları** > **bir SKU eklemek**.
* **Yayımcı Namespace**: hello portal, yayımlama Git çok**sanal makineleri** > **izlenecek** > **söyleyin bize hakkında şirketiniz** ("Adım 2 Register altında" bulunur) **Yayımcı Namespace** > **Namespace**.
* **Bağlantı noktaları**: hello portal, yayımlama Git çok**sanal makineleri** ve teklifiniz seçin. Ardından **VM GÖRÜNTÜLERİ** > **açık bağlantı noktalarını**.
* **Listelenen SKU(s) değişikliği fiyatlandırma**
* **Listelenen SKU(s) faturalama modeli değişikliği**
* **Listelenen SKU(s) bölgelerinin faturalama kaldırma**
* **Listelenen SKU(s) sayısını değiştirme hello veri diski**

## <a name="update-hello-technical-details-of-a-sku"></a>Merhaba teknik bir SKU ayrıntılarını güncelleştir
Yeni bir sürüm toohello tooadd SKU listelenen ve teklifiniz yeniden yayımlamanız, şu adımları izleyin:

1. İçinde toohello oturum [portalını yayımlama](https://publish.windowsazure.com).
2. Toohello Git **sanal makineleri** sekmesini tıklatın ve teklifiniz seçin.
3. Hello'nde hello sol tarafta, hello menüsünü **VM GÖRÜNTÜLERİ** sekmesi.
4. Merhaba, **SKU'ları** bölümünde, hello tooupdate istediğiniz SKU bulun.
5. Merhaba SKU için yeni bir sürüm numarası ekleyin ve hello  **+**  düğmesi. Merhaba yeni sürümü X, Y ve Z tamsayılar olduğu bir X.Y.Z biçiminde olmalıdır. Sürüm değişikliklerini yalnızca artımlı olmalıdır.
6. Merhaba, **OS VHD URL'si** kutusuna hello paylaşılan erişim imzası hello işletim sistemi VHD için oluşturulan URI girin ve hello değişiklikleri kaydedin.

   > [!IMPORTANT]
   > Artışı/hello veri diski sayısı listelenen sku'sunun azaltma olamaz. Bu durumda, yeni bir SKU toocreate gerekir. Ayrıntılı yönergeler için toohello bölümüne bakın [listelenen teklif altında yeni bir SKU eklemek](#add-a-new-sku-under-a-listed-offer).
   >
   >
7. Toohello Git **Yayımla** sekmesine ve tıklayın **İTME tooSTAGING**. Ortamı hazırlama hello teklifiniz sınama ayrıntılı yönergeler için bkz [VM teklifiniz hello Market için Test](marketplace-publishing-vm-image-test-in-staging.md).
8. Teklifiniz test ettikten sonra hazırlamada toohello Git **Yayımla** hello sekmesinde portalını yayımlama. Tıklatın **isteği onayı tooPUSH tooPRODUCTION** toorepublish teklifiniz hello Market içinde.

    ![VM Görüntüleri](media/marketplace-publishing-vm-image-post-publishing/img01_07.png)

## <a name="update-hello-nontechnical-details-of-an-offer-or-a-sku"></a>Bir teklif veya bir SKU yedeğin ayrıntılarını Hello güncelleştir
Merhaba yedeğin (pazarlama, yasal, destek, kategoriler) güncelleştirebilirsiniz hello Market Canlı teklif veya SKU ayrıntıları.

### <a name="update-hello-offer-description-and-logos"></a>Güncelleştirme hello teklif açıklaması ve logo
tooupdate hello Teklif Ayrıntıları ve teklifiniz yeniden yayımlamanız, şu adımları izleyin:

1. İçinde toohello oturum [portalını yayımlama](https://publish.windowsazure.com).
2. Toohello Git **sanal makineleri** sekmesini tıklatın ve teklifiniz seçin.
3. Hello'nde hello sol tarafta, hello menüsünü **pazarlama** sekmesi.
4. Tıklatın **İngilizce (ABD)**.
5. Merhaba tıklatın **ayrıntıları** sekmesi. Merhaba, **açıklama** bölümü, güncelleştirme hello teklif **başlık**, **Özet**, ve **uzun özeti** ve hello değişiklikleri kaydedin.

   > [!NOTE]
   > Merhaba SKU Ayrıntılar'ı güncelleştirdiğinizde bu kısıtlamalarını dikkat edin: 
   * Merhaba teklif açıklama ve hello SKU açıklama için yinelenen metin girmeyin.
   * Merhaba SKU başlık ve hello teklif uzun Özet için yinelenen metin girmeyin. 
   * Merhaba SKU başlık ve hello özeti için yinelenen metin girmeyin.
   >
   >

    ![Ayrıntılar](media/marketplace-publishing-vm-image-post-publishing/img02.1_05.png)
6. Merhaba, **LOGOLAR** hello bölümünü **ayrıntıları** sekmesinde, hello logolar güncelleştirin. Merhaba logolar hello uyduğundan emin [Azure Marketi yönergeleri](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).

   > [!NOTE]
   > İsteğe bağlı bir kahramanı simgedir. Bir kahramanı simgesi değil tooupload seçebilirsiniz. Ancak, bir kahramanı simgesi yüklendikten sonra yoktur sağlama toodelete hello ondan portalını yayımlama. Merhaba izleyin [kahramanı simgesi yönergeleri](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
   >
   >
7. Toohello Git **Yayımla** sekmesine ve tıklayın **İTME tooSTAGING**. Ortamı hazırlama hello teklifiniz sınama ayrıntılı yönergeler için bkz [VM teklifiniz hello Market için Test](marketplace-publishing-vm-image-test-in-staging.md).
8. Teklifiniz test ettikten sonra hazırlamada toohello Git **Yayımla** hello sekmesinde portalını yayımlama. Tıklatın **isteği onayı tooPUSH tooPRODUCTION** toorepublish teklifiniz hello Market içinde.

    ![Logo](media/marketplace-publishing-vm-image-post-publishing/img02.1_08.png)

### <a name="update-hello-sku-description"></a>Merhaba SKU güncelleştirmesi
teklifiniz, yeniden yayımlamanız ve ayrıntıları SKU tooupdate hello şu adımları izleyin:

1. İçinde toohello oturum [portalını yayımlama](https://publish.windowsazure.com).
2. Toohello Git **sanal makineleri** sekmesini tıklatın ve teklifiniz seçin.
3. Hello'nde hello sol tarafta, hello menüsünü **pazarlama** sekmesi.
4. Tıklatın **İngilizce (ABD)**.
5. Merhaba tıklatın **planları** sekmesi. Merhaba, **SKU'ları** bölümünde, hello SKU güncelleştirme **başlık**, **Özet**, ve **açıklama** ve hello değişiklikleri kaydedin.

   > [!NOTE]
   > Merhaba SKU Ayrıntılar'ı güncelleştirdiğinizde bu kısıtlamalarını dikkat edin: 
   * Merhaba teklif açıklama ve hello SKU açıklama için yinelenen metin girmeyin. 
   * Merhaba SKU başlık ve hello teklif uzun Özet için yinelenen metin girmeyin. 
   * Merhaba SKU başlık ve hello özeti için yinelenen metin girmeyin.
   >
   >
6. Toohello Git **Yayımla** sekmesine ve tıklayın **İTME tooSTAGING**. Ortamı hazırlama hello teklifiniz sınama ayrıntılı yönergeler için bkz [VM teklifiniz hello Market için Test](marketplace-publishing-vm-image-test-in-staging.md).
7. Teklifiniz test ettikten sonra hazırlamada toohello Git **Yayımla** hello sekmesinde portalını yayımlama. Tıklatın **isteği onayı tooPUSH tooPRODUCTION** toorepublish teklifiniz hello Market içinde.

    ![Planlar](media/marketplace-publishing-vm-image-post-publishing/img02.2_07.png)

### <a name="change-existing-links-or-add-new-links"></a>Varolan bağlantılar değiştirin veya yeni bağlantı Ekle
toochange varolan bağlantılar veya yeni bağlantılar ekleyebilir ve teklifiniz yeniden yayımlamanız, şu adımları izleyin:

1. İçinde toohello oturum [portalını yayımlama](https://publish.windowsazure.com).
2. Toohello Git **sanal makineleri** sekmesini tıklatın ve teklifiniz seçin.
3. Hello'nde hello sol tarafta, hello menüsünü **pazarlama** sekmesi.
4. Tıklatın **İngilizce (ABD)**.
5. Merhaba tıklatın **bağlantılar** sekmesi.
6. tooadd hello içinde yeni bir bağlantı **bağlantılar** 'yi tıklatın **+ Bağlantı Ekle**. Merhaba, **Bağlantı Ekle** iletişim kutusunda, hello bağlantıyı girin **başlık** ve **URL** ve hello değişiklikleri kaydedin. Müşterilere yardımcı olabilecek bilgilerini içeren herhangi bir bağlantıyı girebilirsiniz.
7. tooupdate ya da delete varolan bir bağlantıyı hello bağlantıyı tıklatıp hello **Düzenle** düğmesini veya hello **silmek** düğmesi.

   > [!NOTE]
   > Bu bağlantılar, üretim isteği işlemi sırasında doğrulanmış için bu bölümdeki girmiş olduğunuz hello bağlantılar düzgün çalıştığından emin olun.
   >
   >
8. Toohello Git **Yayımla** sekmesine ve tıklayın **İTME tooSTAGING**. Ortamı hazırlama hello teklifiniz sınama ayrıntılı yönergeler için bkz [VM teklifiniz hello Market için Test](marketplace-publishing-vm-image-test-in-staging.md).
9. Teklifiniz test ettikten sonra hazırlamada toohello Git **Yayımla** hello sekmesinde portalını yayımlama. Tıklatın **isteği onayı tooPUSH tooPRODUCTION** toorepublish teklifiniz hello Market içinde.

    ![Bağlantılar](media/marketplace-publishing-vm-image-post-publishing/img02.3_09-01.png)

    ![Bağlantı Ekle](media/marketplace-publishing-vm-image-post-publishing/img02.3-2.png)

### <a name="change-an-existing-sample-image-or-add-a-new-sample-image"></a>Var olan bir örnek görüntüsünü değiştirebilir veya yeni bir örnek görüntüsü ekleme
Varolan bir örnek toochange görüntü veya yeni örnek görüntüleri ekleme ve teklifiniz yeniden yayımlamanız, şu adımları izleyin:

> [!NOTE]
> Yalnızca bir örnek görüntü hello görüntülenen [Azure portal](https://portal.azure.com).
>
>

1. İçinde toohello oturum [portalını yayımlama](https://publish.windowsazure.com).
2. Toohello Git **sanal makineleri** sekmesini tıklatın ve teklifiniz seçin.
3. Hello'nde hello sol tarafta, hello menüsünü **pazarlama** sekmesi.
4. Tıklatın **İngilizce (ABD)**.
5. Merhaba tıklatın **örnek GÖRÜNTÜLERİ** sekmesi.
6. tooadd yeni bir örnek görüntüsü, hello **örnek görüntüleri** 'yi tıklatın **yeni GÖRÜNTÜYÜ karşıya** ve hello değişiklikleri kaydedin.

   > [!NOTE]
   > Bir örnek görüntüsü de dahil olmak üzere isteğe bağlıdır.
   >
7. Toohello Git **Yayımla** sekmesine ve tıklayın **İTME tooSTAGING**. Ortamı hazırlama hello teklifiniz sınama ayrıntılı yönergeler için bkz [VM teklifiniz hello Market için Test](marketplace-publishing-vm-image-test-in-staging.md).
8. Teklifiniz test ettikten sonra hazırlamada toohello Git **Yayımla** hello sekmesinde portalını yayımlama. Tıklatın **isteği onayı tooPUSH tooPRODUCTION** toorepublish teklifiniz hello Market içinde.

    ![Örnek görüntüleri](media/marketplace-publishing-vm-image-post-publishing/img02.4_09.png)

### <a name="update-hello-legal-content"></a>Merhaba yasal içeriği güncelleştirme
tooupdate Merhaba yasal içerik ve teklifiniz yeniden yayımlamanız, şu adımları izleyin:

1. İçinde toohello oturum [portalını yayımlama](https://publish.windowsazure.com).
2. Toohello Git **sanal makineleri** sekmesini tıklatın ve teklifiniz seçin.
3. Hello'nde hello sol tarafta, hello menüsünü **pazarlama** sekmesi.
4. Tıklatın **İngilizce (ABD)**.
5. Merhaba tıklatın **yasal** sekmesi. Merhaba, **yasal** bölümünde, ilkeleri/koşulları kullanım güncelleştirin. Girin veya hello ilkeleri/koşulları hello yapıştırın **Kullanım Koşulları'nı** kutusunda ve hello değişiklikleri kaydedin.
6. Merhaba karakter sınırı hello yasal kullanım koşulları için 1 milyon karakterdir.
7. Toohello Git **Yayımla** sekmesine ve tıklayın **İTME tooSTAGING**. Ortamı hazırlama hello teklifiniz sınama ayrıntılı yönergeler için bkz [VM teklifiniz hello Market için Test](marketplace-publishing-vm-image-test-in-staging.md).
8. Teklifiniz test ettikten sonra hazırlamada toohello Git **Yayımla** hello sekmesinde portalını yayımlama. Tıklatın **isteği onayı tooPUSH tooPRODUCTION** toorepublish teklifiniz hello Market içinde.

    ![Yasal Bilgiler](media/marketplace-publishing-vm-image-post-publishing/img02.5_08.png)

### <a name="update-hello-support-information"></a>Merhaba destek bilgilerini güncelleştirin
tooupdate hello destek bilgileri ve teklifiniz yeniden yayımlamanız, şu adımları izleyin:

1. İçinde toohello oturum [portalını yayımlama](https://publish.windowsazure.com).
2. Toohello Git **sanal makineleri** sekmesini tıklatın ve teklifiniz seçin.
3. Hello'nde hello sol tarafta, hello menüsünü **Destek** sekmesi.
4. Merhaba, **mühendislik başvurun** bölümünde, güncelleştirme hello mühendislik kişi ayrıntıları. Bu ayrıntılar için iç iletişiminde hello ortak ve Microsoft arasında yalnızca kullanılır.
5. Merhaba, **müşteri desteği** bölümünde, güncelleştirme hello destek ilgili kişi ayrıntıları ve hello **destek URL**. Bu ayrıntılar için iç iletişiminde hello ortak ve Microsoft arasında yalnızca kullanılır.

   > [!NOTE]
   > Tooprovide yalnızca e-posta desteği istiyorsanız hello bir kukla telefon numarası girin **müşteri desteği** bölümü. Bu durumda, e-posta sağladığınız hello yerine kullanılır.
   >
   >
6. Toohello Git **Yayımla** sekmesine ve tıklayın **İTME tooSTAGING**. Ortamı hazırlama hello teklifiniz sınama ayrıntılı yönergeler için bkz [VM teklifiniz hello Market için Test](marketplace-publishing-vm-image-test-in-staging.md).
7. Teklifiniz test ettikten sonra hazırlamada toohello Git **Yayımla** hello sekmesinde portalını yayımlama. Tıklatın **isteği onayı tooPUSH tooPRODUCTION** toorepublish teklifiniz hello Market içinde.

    ![Destek](media/marketplace-publishing-vm-image-post-publishing/img02.6_07.png)

### <a name="update-hello-categories"></a>Güncelleştirme hello kategorileri
Kategoriler teklifiniz için bölüm ve teklifiniz, yeniden yayımlamanız tooupdate hello şu adımları izleyin:

1. İçinde toohello oturum [portalını yayımlama](https://publish.windowsazure.com).
2. Toohello Git **sanal makineleri** sekmesini tıklatın ve teklifiniz seçin.
3. Hello'nde hello sol tarafta, hello menüsünü **KATEGORİLERİ** sekmesi.
4. Merhaba, **kategorileri** bölümünde hello kategoriler teklifiniz için güncelleştirme ve hello değişiklikleri kaydedin. Hello Azure Marketi galeri toofive kategorileri yukarı seçebilirsiniz.
5. Toohello Git **Yayımla** sekmesine ve tıklayın **İTME tooSTAGING**. Ortamı hazırlama hello teklifiniz sınama ayrıntılı yönergeler için bkz [VM teklifiniz hello Market için Test](marketplace-publishing-vm-image-test-in-staging.md).
6. Teklifiniz test ettikten sonra hazırlamada toohello Git **Yayımla** hello sekmesinde portalını yayımlama. Tıklatın **isteği onayı tooPUSH tooPRODUCTION** toorepublish teklifiniz hello Market içinde.

    ![Kategoriler](media/marketplace-publishing-vm-image-post-publishing/img02.7_06.png)

## <a name="add-a-new-sku-under-a-listed-offer"></a>Listelenen bir teklif altında yeni bir SKU ekleme
tooadd Canlı teklifiniz yeni SKU'da şu adımları izleyin:

1. İçinde toohello oturum [portalını yayımlama](https://publish.windowsazure.com).
2. Toohello Git **sanal makineleri** sekmesini tıklatın ve teklifiniz seçin.
3. Hello'nde hello sol tarafta, hello menüsünü **SKU'ları** sekmesi. Ardından **bir SKU eklemek**. 
4. Merhaba iletişim kutusuna bir **SKU tanımlayıcı** küçük. Select hello **kendi lisans (KLG) fatura modelini** toopublish isterseniz onay kutusunu hello yeni SKU KLG faturalama modeli. Aksi takdirde hello onay kutusunu temizleyin. Merhaba onay işareti toocreate yeni bir SKU'ı tıklatın. Merhaba KLG faturalama modelini seçmediyseniz, hello faturalama modeli toohourly otomatik olarak ayarlanır. Merhaba hello saatlik faturalama modeli için 30 günlük ücretsiz deneme sürümü istiyorsanız seçin **bir ay** için **ücretsiz deneme sürümü kullanılabilir?** Aksi takdirde seçin **Hayır deneme**. (**Ücretsiz deneme sürümü kullanılabilir?**  oluşturma hello ederken yeni SKU yalnızca KLG henüz seçtiyseniz görünür.)

   > [!IMPORTANT]
   > **Bu her zaman bir çözüm şablonu satın alınması çünkü bu SKU hello Market Gizle** olmalıdır **Evet** *yalnızca* bir çözüm şablonu yayımlamak için onaylanmış durumunda. Aksi takdirde, bu seçenek her zaman olmalıdır **Hayır**.
   >
   >
4. Hello'nde hello sol tarafta, hello menüsünü **VM GÖRÜNTÜLERİ** sekmesi ve bulma hello oluşturduğunuz yeni SKU.
5. tooset en yeni SKU Merhaba, bkz: [VM görüntüsü için sertifika elde](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image) Kılavuzu.
6. pazarlama malzemeleri için tooadd yeni SKU Merhaba, bkz: [içerik pazarlama Market sağlamak](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
7. Fiyatlandırma bilgileri için tooadd yeni SKU Merhaba, bkz: [fiyatları ayarlamak](marketplace-publishing-push-to-staging.md#step-2-set-your-prices).
8. Toohello Git **Yayımla** sekmesine ve tıklayın **İTME tooSTAGING**. Ortamı hazırlama hello teklifiniz sınama ayrıntılı yönergeler için bkz [VM teklifiniz hello Market için Test](marketplace-publishing-vm-image-test-in-staging.md).
9. Teklifiniz test ettikten sonra hazırlamada toohello Git **Yayımla** hello sekmesinde portalını yayımlama. Tıklatın **isteği onayı tooPUSH tooPRODUCTION** toorepublish teklifiniz hello Market içinde.

    ![SKU'ları](media/marketplace-publishing-vm-image-post-publishing/img03_09-01.png)

    ![Bir SKU ekleme](media/marketplace-publishing-vm-image-post-publishing/img03_09-02.png)

## <a name="change-hello-data-disk-count-for-a-listed-sku"></a>Listelenen SKU Hello veri diski sayısı değiştirme
Artışı/hello veri diski sayısı listelenen sku'sunun azaltma olamaz. Bu durumda, yeni bir SKU toocreate gerekir. Ayrıntılı yönergeler için toohello bölümüne bakın [listelenen teklif altında yeni bir SKU eklemek](#add-a-new-sku-under-a-listed-offer).

## <a name="delete-a-listed-offer-from-hello-marketplace"></a>Market hello listelenen teklifi Sil
Çeşitli yönlerini isteği tooremove canlı bir teklif hello durumda dikkate toobe gerekir. Merhaba destek ekibi tooremove hello Market, listelenen tekliften tooget kılavuzluğu şu adımları izleyin:

1. Bir destek bileti hello üzerinde Yükselt [bir olay oluşturmak](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) sayfası.

2. Seçin **sorun türü** olarak **teklifleri yönetme**seçip **kategori** olarak **bir teklif ve/veya SKU üretimde zaten değiştirme**.
3. Merhaba isteği gönderin.

Merhaba destek ekibi hello teklif/SKU silme işleminde size rehberlik eder.

> [!NOTE]
> Taslak durumuna (ancak hazırlama veya üretim içinde) olsa, her zaman hello teklif silebilirsiniz. Merhaba üzerinde **GEÇMİŞİ** sekmesini tıklatın, **ATMAK taslak**.
>
>

## <a name="delete-a-listed-sku-from-hello-marketplace"></a>Market hello listelenen SKU Sil
toodelete hello Market, listelenen bir SKU şu adımları izleyin:

1. İçinde toohello oturum [portalını yayımlama](https://publish.windowsazure.com).

2. Toohello Git **sanal makineleri** sekmesini tıklatın ve teklifiniz seçin.
3. Merhaba hello soldaki hello bölmesinde **SKU'ları** sekmesi.
4. Select hello toodelete istediğiniz ve hello tıklatın SKU **silmek** düğmesi.
5. Toohello Git **Yayımla** hello sekmesinde portalını yayımlama. Tıklatın **isteği onayı tooPUSH tooPRODUCTION** hello Market toorepublish hello teklif.
6. Merhaba teklif hello Market yeniden yayımlanması sonra hello SKU hello Market ve hello Azure portal silinir.

## <a name="delete-hello-current-version-of-a-listed-sku-from-hello-marketplace"></a>Market hello Hello listelenen SKU geçerli sürümünü silmek
toodelete hello geçerli sürümü hello Market, listelenen bir SKU, şu adımları izleyin: 

1. İçinde toohello oturum [portalını yayımlama](https://publish.windowsazure.com).

2. Toohello Git **sanal makineleri** sekmesini tıklatın ve teklifiniz seçin.
3. Hello'nde hello sol tarafta, hello menüsünü **VM GÖRÜNTÜLERİ** sekmesi.
4. Merhaba SKU seçin, geçerli toodelete istediğiniz ve hello tıklatın sürüm **silmek** düğmesi.
5. Toohello Git **Yayımla** hello sekmesinde portalını yayımlama. Tıklatın **isteği onayı tooPUSH tooPRODUCTION** hello Market toorepublish hello teklif.
6. Merhaba teklif hello Market yeniden yayımlanması sonra listelenen SKU hello Market ve hello Azure portal silinir hello geçerli sürümü hello. Merhaba SKU, tooits önceki sürümünü geri alınır.

## <a name="revert-hello-listing-price-tooproduction-values"></a>Fiyat tooproduction değerleri listeleme hello geri
toorevert hello listeleme fiyat tooproduction değerleri, şu adımları izleyin:

1. İçinde toohello oturum [portalını yayımlama](https://publish.windowsazure.com).
2. Toohello Git **sanal makineleri** sekmesini tıklatın ve teklifiniz seçin.
3. Hello'nde hello sol tarafta, hello menüsünü **fiyatlandırma** sekmesi.
4. Fiyatlandırma istediğiniz bölgeyi seçin tooreset.

    ![Fiyatlandırma bölgeleri](media/marketplace-publishing-vm-image-post-publishing/img08-04.png)
5. Üretim hello seçili bölge için olduğu gibi SKU'ları için saatlik bir faturalama modeli, tüm hello çekirdekleri hello fiyatlar sıfırlayın. Hello hello SKU hello onay kutusunu seçerek hello bölgede SKU hello için SKU'ları KLG faturalama modeli, olun **EXTERNALLY-LICENSED (KLG) SKU kullanılabilirlik** bölümü.

    ![Fiyatlandırma modelleriyle](media/marketplace-publishing-vm-image-post-publishing/img08-05.png)
6. Tıklatın **AUTOPRICE diğer PAZARDA DAYALI FİYATLARI Amerika Birleşik DEVLETLERİ'nde**.

   > [!NOTE]
   > Merhaba düğmenin etiketi seçtiğiniz hello bölge bağlı olarak farklı olabilir. Amerika Birleşik Devletleri seçtik çünkü hello düğme etiketlenir **AUTOPRICE diğer PAZARDA göre ON FİYATLAR IN birleşik DURUMLARINI**.
   >
   >

    ![Autoprice](media/marketplace-publishing-vm-image-post-publishing/img08-06.png)
7. Üzerinde sayfasında 1 hello Autoprice Sihirbazı'nın, hello temel Pazar'ı seçin ve hello tıklayın **ok** düğmesi.

    ![Temel Pazar](media/marketplace-publishing-vm-image-post-publishing/img08-07.png)
8. Üzerinde sayfasında 2, hizmeti planları ve ölçümler (çekirdekler) seçin ve hello tıklayın **ok** düğmesi.

    ![Hizmet planları ve ölçümler](media/marketplace-publishing-vm-image-post-publishing/img08-08.png)
9. 3 sayfasında, tıklatın **geçiş tüm** tooselect tüm bölgeler. Veya belirli bölgeler için onay kutularını el ile seçebilirsiniz. Merhaba tıklatın **ok** düğmesi.

    ![Pazarda seçin](media/marketplace-publishing-vm-image-post-publishing/img08-09.png)
10. Üzerinde sayfasında 4 hello döviz kuru gözden geçirin ve tıklayın **son**. Merhaba Sihirbazı according tooyour seçimleri fiyatlandırma hello sıfırlar.

11. Merhaba üzerinde **fiyatlandırma** sekmesini tıklatın, **Görünüm Özeti ve değişiklikleri**.
    İçin **görünüm sürüm**seçin **taslak**ve **karşılaştırmak**seçin **üretim**. Fiyatlandırma fark görürseniz, hello fiyatlandırma toohello üretim değerleri başarıyla geri döndürüldü.

    ![Özet görüntüleyin ve değişiklikleri](media/marketplace-publishing-vm-image-post-publishing/img08-11.png)
12. Toohello Git **Yayımla** sekmesine ve tıklayın **İTME tooSTAGING**. Ortamı hazırlama hello teklifiniz sınama ayrıntılı yönergeler için bkz [VM teklifiniz hello Market için Test](marketplace-publishing-vm-image-test-in-staging.md).
13. Teklifiniz test ettikten sonra hazırlamada toohello Git **Yayımla** hello sekmesinde portalını yayımlama. Tıklatın **isteği onayı tooPUSH tooPRODUCTION** toorepublish teklifiniz hello Market içinde.

## <a name="revert-hello-billing-model-tooproduction-values"></a>Modeli tooproduction değerlerini faturalama hello geri
toorevert hello faturalama modeli tooproduction değerleri, şu adımları izleyin:

1. İçinde toohello oturum [portalını yayımlama](https://publish.windowsazure.com).

2. Toohello Git **sanal makineleri** sekmesini tıklatın ve teklifiniz seçin.
3. Hello'nde hello sol tarafta, hello menüsünü **SKU'ları** sekmesi.
4. Merhaba tıklatın **Düzenle** düğmesini toorevert hello faturalama modeli. Açılır hello penceresinde seçin veya temizleyin hello **faturalama ve lisanslama yapılır dışarıdan (diğer adıyla kendi lisansını Getir) Azure'dan** onay kutusu.

    ![Faturalama Düzenle](media/marketplace-publishing-vm-image-post-publishing/img09-04.png)
5. Bu makalede "Revert hello fiyat tooproduction değerleri listeleme" Merhaba adımları izleyin.
6. Toohello Git **Yayımla** sekmesine ve tıklayın **İTME tooSTAGING**. Ortamı hazırlama hello teklifiniz sınama ayrıntılı yönergeler için bkz [VM teklifiniz hello Market için Test](marketplace-publishing-vm-image-test-in-staging.md).
7. Teklifiniz test ettikten sonra hazırlamada toohello Git **Yayımla** hello sekmesinde portalını yayımlama. Tıklatın **isteği onayı tooPUSH tooPRODUCTION** toorepublish teklifiniz hello Market içinde.

## <a name="revert-hello-visibility-setting-of-a-listed-sku-toohello-production-value"></a>Listelenen bir SKU toohello üretim değeri Hello görünürlük ayarını geri
listelenen bir SKU toohello üretim değeri, toorevert hello görünürlük ayarını şu adımları izleyin:

1. İçinde toohello oturum [portalını yayımlama](https://publish.windowsazure.com).

2. Toohello Git **sanal makineleri** sekmesini tıklatın ve teklifiniz seçin.
3. Hello'nde hello sol tarafta, hello menüsünü **SKU'ları** sekmesi.
4. SKU seçin ve hello SKU toohello üretim değeri hello görünürlük ayarlarını geri.

    ![Görünürlüğü](media/marketplace-publishing-vm-image-post-publishing/img10-04.png)
5. Merhaba değişikliklerle bitirdikten sonra tıklatın **isteği onayı tooPUSH tooPRODUCTION** toorepublish teklifiniz hello Market içinde.

## <a name="see-also"></a>Ayrıca bkz.
* [Başlarken: Teklif toohello Azure Marketi'nde yayımlama](marketplace-publishing-getting-started.md)
* [Ödeme raporlama anlama](marketplace-publishing-report-payout.md)
* [Bulut çözümü sağlayıcısı satıcınızla ıncentive değiştirme](marketplace-publishing-csp-incentive.md)
* [Ortak yayımlama hello Market sorunlarını giderme](marketplace-publishing-support-common-issues.md)
* [Bir yayımcı olarak destek alma](marketplace-publishing-get-publisher-support.md)
* [Şirket içi bir VM görüntüsü oluşturma](marketplace-publishing-vm-image-creation-on-premise.md)
* [Windows hello Azure Önizleme portalında çalıştıran bir sanal makine oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
