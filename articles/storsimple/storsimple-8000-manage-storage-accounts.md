---
title: "StorSimple depolama hesabınızı Microsoft Azure StorSimple 8000 serisi cihazlar için kimlik bilgileri aaaManage | Microsoft Docs"
description: "Bir depolama hesabı için nasıl hello StorSimple Aygıt Yöneticisi'ni Yapılandır sayfası tooadd, düzenleme, silme veya döndürme hello güvenlik anahtarları kullanabileceğiniz açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 132ee46509b39db4d1b97b0f1077800a253e8da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-storage-account-credentials"></a>Depolama hesabı kimlik bilgilerinizi Hello StorSimple cihaz Yöneticisi hizmeti toomanage kullanın

## <a name="overview"></a>Genel Bakış

Merhaba **yapılandırma** hello StorSimple cihaz Yöneticisi hizmeti dikey bölümde hello StorSimple cihaz Yöneticisi hizmeti oluşturulan tüm hello genel hizmet parametreleri gösterir. Bu parametreler cihazları toohello hizmet bağlanır ve dahil uygulanan tooall hello olabilir:

* Depolama hesabı kimlik bilgileri
* Bant genişliği şablonları 
* Erişim denetimi kayıtları 

Bu öğretici nasıl tooadd, düzenleme, depolama hesabının kimlik bilgilerini silmek veya bir depolama hesabı için hello güvenlik anahtarları döndürme açıklanmaktadır.

 ![Depolama hesabı kimlik bilgileri listesi](./media/storsimple-8000-manage-storage-accounts/createnewstorageacct6.png)  

Depolama hesapları StorSimple cihaz kullanan tooaccess depolama hesabınızı bulut hizmeti sağlayıcısı ile Merhaba hello kimlik bilgilerini içerir. Microsoft Azure depolama hesapları için bu hello hesap adı ve hello birincil erişim anahtarı gibi kimlik bilgileridir. 

Merhaba üzerinde **depolama hesabının kimlik bilgilerini** dikey penceresinde, tüm depolama abonelik faturalama hello için oluşturulan hesapları aşağıdaki bilgilerle hello içeren bir tablo biçiminde görüntülenir:

* **Ad** – oluşturulduğunda atanan benzersiz bir ad toohello hesabı hello.
* **SSL özellikli** – hello SSL etkin ve cihaz bulut iletişimidir hello güvenli kanal üzerinden olup olmadığını.
* **Tarafından kullanılan** – hello hello depolama hesabı kullanarak birimlerin sayısı.

gerçekleştirilebilir hello en yaygın görevleri ilgili toostorage hesaplar şunlardır:

* Depolama hesabı ekleme 
* Bir depolama hesabı Düzenle 
* Bir depolama hesabını silme 
* Depolama hesaplarının anahtar döndürme 

## <a name="types-of-storage-accounts"></a>Depolama hesabı türleri

Üç tür StorSimple cihazınızla kullanılabilir depolama hesabı vardır.

* **Otomatik olarak oluşturulan depolama hesapları** – hello adı da anlaşılacağı gibi bu depolama hesap türü hello hizmet ilk oluşturulduğunda otomatik olarak oluşturulur. Bu depolama hesabının nasıl oluşturulduğu hakkında daha fazla toolearn bkz [1. adım: yeni bir hizmet Oluştur](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service) içinde [şirket içi StorSimple Cihazınızı dağıtma](storsimple-8000-deployment-walkthrough-u2.md). 
* **Merhaba hizmet Abonelikteki depolama hesapları** – hello ile ilişkili hello Azure depolama hesapları bunlar hello hizmeti, aynı abonelik. Bu depolama hesaplarından nasıl oluşturulduğunu, hakkında daha fazla toolearn bkz [Azure Storage hesapları hakkında](../storage/common/storage-create-storage-account.md). 
* **Depolama hesapları hello hizmet aboneliği dışında** – bunlar hizmetiniz ile ilişkili olmayan hello Azure depolama hesapları ve büyük olasılıkla önce önceden hello hizmeti oluşturuldu.

## <a name="add-a-storage-account"></a>Depolama hesabı ekleme

Benzersiz bir sağlayarak bir depolama hesabı ekleyebilirsiniz kolay adı ve erişim kimlik bilgilerini bağlı toohello depolama hesabıyla (Merhaba belirtilen bulut hizmeti sağlayıcısı). Cihaz ve hello bulut arasındaki ağ iletişimi için güvenli bir kanal hello Güvenli Yuva Katmanı (SSL) modunda toocreate etkinleştirme hello seçeneğiniz de vardır.

Verilen bulut hizmeti sağlayıcı için birden çok hesabı oluşturabilirsiniz. Ancak, bir depolama hesabı oluşturulduktan sonra hello bulut hizmet sağlayıcısı değiştirilemiyor unutmayın.

Merhaba depolama hesabı kaydedilirken, hello hizmeti toocommunicate bulut hizmeti sağlayıcısı ile çalışır. Merhaba kimlik bilgilerini ve sağladığınız hello erişim malzemeleri şu anda doğrulanır. Bir depolama hesabı yalnızca hello kimlik doğrulaması başarılı olursa oluşturulur. Merhaba kimlik doğrulama başarısız olursa, ilgili hata iletisi görüntülenir.

Aşağıdaki yordamlar tooadd Azure depolama hesabı kimlik bilgileri hello kullan:

* tooadd sahip bir depolama hesabı kimlik bilgilerini hello hello Aygıt Yöneticisi hizmeti aynı Azure abonelik
* tooadd hello Aygıt Yöneticisi'ni hizmet aboneliği dışında bir Azure depolama hesabı kimlik bilgileri

[!INCLUDE [add-a-storage-account-update2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

#### <a name="tooadd-an-azure-storage-account-credential-outside-of-hello-storsimple-device-manager-service-subscription"></a>tooadd hello StorSimple Aygıt Yöneticisi'ni hizmet aboneliği dışında bir Azure depolama hesabı kimlik bilgileri

1. StorSimple cihaz Yöneticisi hizmeti, select tooyour gidin ve çift tıklatın. Merhaba açılır **genel bakış** dikey.
2. Seçin **depolama hesabının kimlik bilgilerini** hello içinde **yapılandırma** bölümü. Merhaba StorSimple cihaz Yöneticisi hizmeti ile ilişkili tüm var olan depolama hesabının kimlik bilgilerini listeler.
3. **Ekle**'ye tıklayın.
4. Merhaba, **bir depolama hesabı kimlik bilgileri Ekle** dikey penceresinde, aşağıdaki hello:
   
    1. İçin **abonelik**seçin **diğer**.
   
    2. Azure depolama hesabı kimlik bilgilerinizi Hello adını sağlayın.
   
    3. Merhaba, **depolama hesabının erişim anahtarı** metin kutusu, tedarik hello Azure depolama hesabı kimlik bilgileriniz için birincil erişim anahtarı. tooget bu anahtar toohello Azure depolama hizmeti gidin, depolama hesabı kimlik bilgilerinizi seçin ve'ı tıklatın **hesabı anahtarları Yönet**. Şimdi hello birincil erişim anahtarını kopyalayabilirsiniz.
   
    4. tooenable SSL tıklatın hello **etkinleştirmek** düğmesini toocreate StorSimple cihaz Yöneticisi hizmeti ve hello bulut arasındaki ağ iletişimi için güvenli bir kanal. Hello tıklatın **devre dışı** yalnızca özel bir bulutta işlem yapıyorsanız düğmesine tıklayın.
   
    5. **Ekle**'ye tıklayın. Merhaba depolama hesabı kimlik bilgilerini başarıyla oluşturulduktan sonra size bildirilir.

5. Merhaba yeni oluşturulan depolama hesabı kimlik bilgileri altında hello StorSimple yapılandırma Aygıt Yöneticisi'ni hizmet dikey penceresinde görüntülenir **depolama hesabının kimlik bilgilerini**.
   


## <a name="edit-a-storage-account"></a>Bir depolama hesabı Düzenle

Bir birim kapsayıcısı tarafından kullanılan bir depolama hesabı düzenleyebilirsiniz. Şu anda kullanımda olduğundan bir depolama hesabı düzenlerseniz, hello yalnızca alan kullanılabilir toomodify hello erişim hello depolama hesabı için bir anahtardır. Merhaba yeni depolama erişim tuşunu sağlayın ve güncelleştirilmiş hello ayarları kaydedin.

#### <a name="tooedit-a-storage-account"></a>tooedit bir depolama hesabı

1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin. Merhaba, **yapılandırma** 'yi tıklatın **depolama hesabının kimlik bilgilerini**.

    ![Depolama hesabı kimlik bilgileri](./media/storsimple-8000-manage-storage-accounts/editstorageacct1.png)

2. Merhaba, **depolama hesabının kimlik bilgilerini** dikey penceresinde, depolama hesabı kimlik bilgileri, select hello listesinden ve bir tooedit istediğiniz hello tıklatın. 

3. Merhaba değiştirebileceğiniz **SSL'yi etkinleştir** seçim. Tıklatarak **daha...**  ve ardından **eşitleme erişim anahtar toorotate** depolama hesap erişim tuşlarınızı. Çok Git[anahtar depolama hesapları dönüşünü](#key-rotation-of-storage-accounts) nasıl tooperform anahtar döndürme hakkında daha fazla bilgi. Hello ayarlarını değiştirdikten sonra tıklatın **kaydetmek**. 

    ![Düzenlenen depolama hesabının kimlik bilgilerini Kaydet](./media/storsimple-8000-manage-storage-accounts/editstorageacct3.png)

4. Onayınız istendiğinde **Evet**’e tıklayın. 

    ![Değişiklikleri onaylayın](./media/storsimple-8000-manage-storage-accounts/editstorageacct4.png)

Hello ayarları güncelleştirildi ve depolama hesabınız için kaydedilir. 

## <a name="delete-a-storage-account"></a>Bir depolama hesabını silme

> [!IMPORTANT]
> Yalnızca bir birim kapsayıcısı tarafından kullanılmıyorsa, bir depolama hesabı silebilirsiniz. Bir depolama hesabı bir birim kapsayıcısı tarafından kullanılıyorsa, hello birim kapsayıcısı silmeniz ve ilişkili hello depolama hesabı silin.

#### <a name="toodelete-a-storage-account"></a>toodelete bir depolama hesabı

1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin. Merhaba, **yapılandırma** 'yi tıklatın **depolama hesabının kimlik bilgilerini**.

2. Merhaba Tablo listesinde depolama hesapları, toodelete istediğiniz hello hesap gelin. Tooinvoke hello bağlam menüsü sağ tıklatın ve **silmek**.

    ![Depolama hesabının kimlik bilgilerini sil](./media/storsimple-8000-manage-storage-accounts/deletestorageacct1.png)

3. Onayınız istendiğinde tıklatın **Evet** toocontinue hello silme işlemi ile. Merhaba sekmeli liste güncelleştirilmiş tooreflect hello değişiklikler.

    ![Silmeyi onayla](./media/storsimple-8000-manage-storage-accounts/deletestorageacct2.png)

## <a name="key-rotation-of-storage-accounts"></a>Depolama hesaplarının anahtar döndürme

Güvenlik nedenleriyle, anahtar döndürme genellikle veri merkezlerinde gerekli değildir. Her bir Microsoft Azure aboneliği bir veya daha fazla ilişkili depolama hesapları olabilir. Merhaba erişim toothese hesapları hello aboneliği ve her depolama hesabının erişim anahtarlarını tarafından denetlenir. 

Bir depolama hesabı oluşturduğunuzda, Microsoft Azure hello depolama hesabı erişildiğinde, kimlik doğrulaması için kullanılan iki 512 bit depolama erişim tuşu oluşturur. İki depolama erişim tuşu sahip olmanız tooregenerate hello anahtarlarla herhangi kesinti tooyour depolama hizmeti veya erişim toothat hizmeti sağlar. Merhaba, şu anda kullanımda hello anahtardır *birincil* anahtar ve hello yedekleme anahtarıdır başvurulan tooas hello *ikincil* anahtarı. Microsoft Azure StorSimple Cihazınızı bulut depolama hizmeti sağlayıcısı eriştiğinde, bu iki anahtarlarından birini sağlanmalıdır.

## <a name="what-is-key-rotation"></a>Anahtar döndürme nedir?

Genellikle, uygulamalar, verilerinizi hello anahtarları tooaccess yalnızca birini kullanın. Belirli bir süre süre sonra toousing hello ikinci anahtarı üzerinde anahtar uygulamalarınız olabilir. Uygulamaları toohello ikincil anahtar geçirildikten sonra hello ilk anahtar devre dışı bırakmak ve ardından yeni bir anahtar oluşturun. Bu şekilde Hello iki tuşlarını kullanarak uygulamaları erişim toohello verilerinizi kapalı kalma süresi olmadan aktarabilmesini sağlar.

Merhaba depolama hesabı anahtarlarını her zaman hello hizmet şifrelenmiş biçimde depolanır. Ancak, bunlar hello StorSimple cihaz Yöneticisi hizmeti sıfırlanabilir. Merhaba hizmet hello birincil anahtar alabilir ve ikincil anahtar tüm hello hello varsayılan depolama hesaplarının yanı sıra hello depolama hizmeti içinde oluşturulan hesapların dahil olmak üzere aynı abonelik oluşturulan depolama hesaplarında hello için ne zaman hello StorSimple cihaz Yöneticisi hizmeti ilk oluşturuldu. Merhaba StorSimple cihaz Yöneticisi hizmeti her zaman bu anahtarları hello Klasik Azure Portalı ' almak ve bunları bir şifrelenmiş biçimde depolamak.

## <a name="rotation-workflow"></a>Döndürme iş akışı

Microsoft Azure yönetici yeniden oluşturmak veya hello depolama hesabı (aracılığıyla Microsoft Azure depolama hizmeti hello) doğrudan erişerek hello birincil veya ikincil anahtarı değiştirin. Merhaba StorSimple cihaz Yöneticisi hizmeti bu değişikliği otomatik olarak görmez.

tooinform hello StorSimple cihaz Yöneticisi hizmeti hello değişimin gerekir tooaccess hello StorSimple cihaz Yöneticisi hizmeti, erişim hello depolama hesabı ve (hangisinin bağlı olarak değiştirildi) hello birincil veya ikincil anahtarı Eşitle. Merhaba hizmeti ardından hello en son anahtarın alır, hello anahtarları şifreler ve anahtar toohello aygıt hello şifrelenmiş gönderir.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service"></a>Merhaba hizmet aynı abonelik toosynchronize anahtarları depolama hesaplarını hello 
1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin. Merhaba, **yapılandırma** 'yi tıklatın **depolama hesabının kimlik bilgilerini**.
2. Merhaba Tablo listesi depolama hesapları gelen, toomodify istediğiniz hello birini tıklatın. 

    ![anahtarları Eşitle](./media/storsimple-8000-manage-storage-accounts/syncaccesskey1.png)

3. Tıklatın **... Daha fazla** ve ardından **eşitleme erişim anahtar toorotate**.   

    ![anahtarları Eşitle](./media/storsimple-8000-manage-storage-accounts/syncaccesskey2.png)

4. Hello StorSimple cihaz Yöneticisi hizmeti, daha önce Microsoft Azure depolama hizmeti hello değiştirildi tooupdate hello anahtarı gerekir. Merhaba birincil erişim anahtarını (oluşturuldu) değiştirilmişse, seçin **birincil** anahtarı. Merhaba ikincil anahtarı değiştirildiyse seçin **ikincil** anahtarı. Tıklatın **eşitleme anahtarı**.
      
      ![anahtarları Eşitle](./media/storsimple-8000-manage-storage-accounts/syncaccesskey3.png)

Başlangıç anahtarı sycnhronized başarıyla tamamlandıktan sonra size bildirilecek.

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>Depolama hesapları hello hizmet aboneliği dışında toosynchronize tuşları
1. Merhaba üzerinde **Hizmetleri** hello sayfasında, **yapılandırma** sekmesi.
2. Tıklatın **depolama hesapları Ekle/Düzenle**.
3. Merhaba iletişim kutusunda, aşağıdaki hello:
   
   1. Merhaba depolama hesabı hello erişim anahtarı ile tooupdate istediğinizi seçin.
   2. Tooupdate hello depolama erişim tuşu hello StorSimple cihaz Yöneticisi hizmeti gerekir. Bu durumda, hello depolama erişim tuşu görebilirsiniz. Hello Hello yeni anahtarı girin **depolama hesabının erişim anahtarı** kutusu. 
   3. Yaptığınız değişiklikleri kaydedin. Depolama hesabı erişim anahtarınızı şimdi güncelleştirilmesi gerekir.

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [StorSimple güvenlik](storsimple-8000-security.md).
* Daha fazla bilgi edinmek [StorSimple Cihazınızı hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanarak](storsimple-8000-manager-service-administration.md).

