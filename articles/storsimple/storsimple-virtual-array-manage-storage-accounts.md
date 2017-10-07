---
title: "aaaManage StorSimple sanal dizi depolama hesabının kimlik bilgilerini | Microsoft Docs"
description: "StorSimple sanal dizinin hello ile ilişkili depolama hesabı kimlik bilgileri hello StorSimple Aygıt Yöneticisi'ni Yapılandır sayfası tooadd, düzenleme, silme veya döndürme hello güvenlik anahtarları nasıl kullanabileceğinizi açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 234bf8bb-d5fe-40be-9d25-721d7482bc3b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: 22a0341eae0b89020065be4dbfaae77999f8be0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-storage-account-credentials-for-storsimple-virtual-array"></a>StorSimple sanal dizinin StorSimple cihaz Yöneticisi'ni kullanın toomanage depolama hesabı kimlik bilgileri

## <a name="overview"></a>Genel Bakış
Merhaba **yapılandırma** hello StorSimple cihaz Yöneticisi hizmeti dikey, StorSimple sanal dizinin bölümünü hello StorSimple Yöneticisi hizmeti oluşturulabilir hello genel hizmet parametreleri gösterir. Bu parametreler cihazları toohello hizmet bağlanır ve dahil uygulanan tooall hello olabilir:

* Depolama hesabı kimlik bilgileri
* Erişim denetimi kayıtları
  
  ![Aygıt Yöneticisi'ni hizmet Panosu](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccts-dashboard.png)  

Bu öğretici nasıl ekleyebilir, düzenleme veya StorSimple sanal dizisi için depolama hesabının kimlik bilgilerini sil açıklanmaktadır. Bu öğreticide Hello bilgiler, yalnızca toohello StorSimple sanal dizinin geçerlidir. 8000 serisi içindeki nasıl toomanage depolama hesapları hakkında daha fazla bilgi için bkz: [kullanım hello StorSimple Yöneticisi hizmet toomanage depolama hesabınız](storsimple-manage-storage-accounts.md).

Depolama hesabı kimlik bilgilerini cihaz hello hello kimlik bilgilerini içeren bulut hizmeti sağlayıcısı ile depolama hesabınız tooaccess kullanır. Microsoft Azure depolama hesapları için bu hello hesap adı ve hello birincil erişim anahtarı gibi kimlik bilgileridir.

Merhaba üzerinde **depolama hesabının kimlik bilgilerini** dikey penceresinde, tüm depolama hesabı için abonelik faturalama hello oluşturulan kimlik bilgisinden hello içeren bir tablo biçiminde görüntülenir:

* **Ad** – oluşturulduğunda atanan benzersiz bir ad toohello hesabı hello.
* **SSL özellikli** – hello SSL etkin ve cihaz bulut iletişimidir hello güvenli kanal üzerinden olup olmadığını.
  
  ![Yapılandırma bölümü](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccountcredentials-blade.png)

Merhaba en yaygın görevleri ilgili hello üzerinde gerçekleştirilebilir toostorage hesap kimlik bilgilerini **depolama hesabının kimlik bilgilerini** dikey şunlardır:

* Depolama hesabı kimlik bilgisi ekleyin
* Bir depolama hesabı kimlik bilgilerini Düzenle
* Bir depolama hesabı kimlik bilgilerini sil

## <a name="types-of-storage-account-credentials"></a>Türleri depolama hesabı kimlik bilgileri
StorSimple cihazınızla kullanılabilir depolama hesabı kimlik bilgileri üç tür vardır.

* **Otomatik olarak oluşturulan depolama hesabının kimlik bilgilerini** – hello adı da anlaşılacağı gibi bu tür bir depolama hesabı kimlik bilgilerini hello hizmet ilk oluşturulduğunda otomatik olarak oluşturulur. Bu depolama hesabı kimlik bilgilerinin nasıl oluşturulduğu hakkında daha fazla toolearn bkz [yeni bir hizmet Oluştur](storsimple-virtual-array-manage-service.md#create-a-service).
* **Depolama hesabı kimlik bilgilerini hello hizmet aboneliği** – hello Azure depolama hesabı bunlar ile ilişkili kimlik bilgilerini hello hello hizmeti, aynı abonelik. Bu depolama hesabının kimlik bilgilerini nasıl oluşturulduğunu, hakkında daha fazla toolearn bkz [Azure Storage hesapları hakkında](../storage/common/storage-create-storage-account.md).
* **Depolama hesabının kimlik bilgilerini hello hizmet aboneliği dışında** – bunlar hizmetiniz ile ilişkili olmayan hello Azure depolama hesabı kimlik bilgileri ve büyük olasılıkla önce önceden hello hizmeti oluşturuldu.

## <a name="add-a-storage-account-credential"></a>Depolama hesabı kimlik bilgisi ekleyin
Benzersiz bir sağlayarak bir depolama hesabı kimlik bilgileri tooyour StorSimple cihaz Yöneticisi hizmet yapılandırması ekleyebilirsiniz kolay adı ve erişim kimlik bilgilerini toohello depolama hesabına bağlanır. Cihaz ve hello bulut arasındaki ağ iletişimi için güvenli bir kanal hello Güvenli Yuva Katmanı (SSL) modunda toocreate etkinleştirme hello seçeneğiniz de vardır.

Verilen bulut hizmeti sağlayıcı için birden çok hesabı oluşturabilirsiniz. Merhaba depolama hesabı kimlik bilgilerini kaydedilirken, hello hizmeti toocommunicate bulut hizmeti sağlayıcısı ile çalışır. Merhaba kimlik bilgilerini ve sağladığınız hello erişim malzemeleri şu anda doğrulanır. Bir depolama hesabı kimlik bilgilerini yalnızca hello kimlik doğrulaması başarılı olursa oluşturulur. Merhaba kimlik doğrulama başarısız olursa, ilgili hata iletisi görüntülenir.

Aşağıdaki yordamlar tooadd Azure depolama hesabı kimlik bilgileri hello kullan:

* tooadd sahip bir depolama hesabı kimlik bilgilerini hello hello Aygıt Yöneticisi hizmeti aynı Azure abonelik
* tooadd hello Aygıt Yöneticisi'ni hizmet aboneliği dışında bir Azure depolama hesabı kimlik bilgileri

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>tooadd sahip bir depolama hesabı kimlik bilgilerini hello hello Aygıt Yöneticisi hizmeti aynı Azure abonelik

1. Aygıt Yöneticisi hizmeti, select tooyour gidin ve çift tıklatın. Merhaba açılır **genel bakış** dikey.
2. Seçin **depolama hesabının kimlik bilgilerini** hello içinde **yapılandırma** bölümü.
3. **Ekle**'ye tıklayın.
4. Merhaba, **depolama hesabı ekleme** dikey penceresinde, aşağıdaki hello:
   
    1. İçin **abonelik**seçin **geçerli**.
    2. Hello Azure depolama hesabınızın adını sağlayın.
    3. Seçin **etkinleştirmek** toocreate StorSimple cihaz ve hello bulut arasındaki ağ iletişimi için güvenli bir kanal. Seçin **devre dışı** yalnızca özel bir bulutta işlem yapıyorsanız.
    4. **Ekle**'ye tıklayın. Merhaba depolama hesabı başarıyla oluşturulduktan sonra size bildirilir.<br></br>
   
        ![Varolan bir depolama hesabı kimlik bilgileri Ekle](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

#### <a name="tooadd-an-azure-storage-account-credential-that-is-outside-of-hello-device-manager-service-subscription"></a>tooadd hello Aygıt Yöneticisi'ni hizmet aboneliği dışında bir Azure depolama hesabı kimlik bilgileri

1. Aygıt Yöneticisi hizmeti, select tooyour gidin ve çift tıklatın. Merhaba açılır **genel bakış** dikey.
2. Seçin **depolama hesabının kimlik bilgilerini** hello içinde **yapılandırma** bölümü. Merhaba StorSimple cihaz Yöneticisi hizmeti ile ilişkili tüm var olan depolama hesabının kimlik bilgilerini listeler.
3. **Ekle**'ye tıklayın.
4. Merhaba, **depolama hesabı ekleme** dikey penceresinde, aşağıdaki hello:
   
    1. İçin **abonelik**seçin **diğer**.
   
    2. Azure depolama hesabı kimlik bilgilerinizi Hello adını sağlayın.
   
    3. Merhaba, **depolama hesabının erişim anahtarı** metin kutusu, tedarik hello Azure depolama hesabı kimlik bilgileriniz için birincil erişim anahtarı. tooget bu anahtar toohello Azure depolama hizmeti gidin, depolama hesabı kimlik bilgilerinizi seçin ve'ı tıklatın **hesabı anahtarları Yönet**. Şimdi hello birincil erişim anahtarını kopyalayabilirsiniz.
   
    4. tooenable SSL tıklatın hello **etkinleştirmek** düğmesini toocreate StorSimple cihaz Yöneticisi hizmeti ve hello bulut arasındaki ağ iletişimi için güvenli bir kanal. Hello tıklatın **devre dışı** yalnızca özel bir bulutta işlem yapıyorsanız düğmesine tıklayın.
   
    5. **Ekle**'ye tıklayın. Merhaba depolama hesabı kimlik bilgilerini başarıyla oluşturulduktan sonra size bildirilir.

5. Merhaba yeni oluşturulan depolama hesabı kimlik bilgileri altında hello StorSimple yapılandırma Aygıt Yöneticisi'ni hizmet dikey penceresinde görüntülenir **depolama hesabının kimlik bilgilerini**.
   
    ![Hello Aygıt Yöneticisi'ni hizmet aboneliği dışında bir depolama hesabı kimlik bilgileri Ekle](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-outside-storageacct.png)

## <a name="edit-a-storage-account-credential"></a>Bir depolama hesabı kimlik bilgilerini Düzenle
Cihazınız tarafından kullanılan depolama hesabı kimlik bilgilerini düzenleyebilirsiniz. Şu anda kullanılmakta olan bir depolama hesabı kimlik bilgilerini düzenleyin, hello alanlar kullanılabilir toomodify hello erişim anahtarı ve hello hello depolama hesabı kimlik bilgisi için SSL modu demektir. Tedarik hello yeni depolama erişim tuşu veya hello değiştirmek **SSL'yi etkinleştir modu** seçimi ve güncelleştirilmiş hello ayarları kaydedin.

#### <a name="tooedit-a-storage-account-credential"></a>tooedit bir depolama hesabı kimlik bilgileri
1. Aygıt Yöneticisi hizmeti, select tooyour gidin ve çift tıklatın. Merhaba açılır **genel bakış** dikey.
2. Seçin **depolama hesabının kimlik bilgilerini** hello içinde **yapılandırma** bölümü. Merhaba StorSimple cihaz Yöneticisi hizmeti ile ilişkili tüm var olan depolama hesabının kimlik bilgilerini listeler.
3. Merhaba sekmeli liste depolama hesabı kimlik bilgileri seçin ve toomodify istediğiniz hello hesabını çift tıklatın.
4. Merhaba depolama hesabı kimlik bilgilerini de **özellikleri** dikey penceresinde, aşağıdaki hello:
   
   1. Gerekirse, hello değiştirebileceğiniz varsa **SSL'yi etkinleştir** mod seçimi.
   2. Depolama hesabı kimlik bilgileri erişim tuşlarınızı tooregenerate seçebilirsiniz. Daha fazla bilgi için bkz: [hello depolama hesabı anahtarlarını yeniden](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys). Merhaba yeni depolama hesabı kimlik bilgisi anahtarı sağlayın. Bir Azure depolama hesabı için hello birincil erişim anahtarını budur.
   3. Tıklatın **kaydetmek** hello hello üstündeki **özellikleri** dikey toosave hello ayarları. Hello ayarlarının üzerinde hello güncelleştirilmesini **depolama hesabının kimlik bilgilerini** dikey.
      
      ![Bir depolama hesabı kimlik bilgilerini Düzenle](./media/storsimple-virtual-array-manage-storage-accounts/ova-edit-storageacct.png)

## <a name="delete-a-storage-account-credential"></a>Bir depolama hesabı kimlik bilgilerini sil
> [!IMPORTANT]
> Yalnızca kullanımda değilse, bir depolama hesabı kimlik bilgilerini silebilirsiniz. Bir depolama hesabı kimlik bilgisi kullanımda olduğunda size bildirilir.
> 
> 

#### <a name="toodelete-a-storage-account-credential"></a>toodelete bir depolama hesabı kimlik bilgileri
1. Aygıt Yöneticisi hizmeti, select tooyour gidin ve çift tıklatın. Merhaba açılır **genel bakış** dikey.
2. Seçin **depolama hesabının kimlik bilgilerini** hello içinde **yapılandırma** bölümü. Merhaba StorSimple cihaz Yöneticisi hizmeti ile ilişkili tüm var olan depolama hesabının kimlik bilgilerini listeler.
3. Merhaba sekmeli liste depolama hesabı kimlik bilgileri seçin ve toodelete istediğiniz hello hesabını çift tıklatın.
4. Merhaba depolama hesabı kimlik bilgilerini de **özellikleri** dikey penceresinde, aşağıdaki hello:
   
   1. Tıklatın **silmek** toodelete hello kimlik bilgileri.
   2. Onayınız istendiğinde tıklatın **Evet** toocontinue hello silme işlemi ile. Merhaba tablo güncelleştirilmiş tooreflect hello değişiklikleri listedir.
      
      ![Bir depolama hesabı kimlik bilgilerini sil](./media/storsimple-virtual-array-manage-storage-accounts/ova-del-storageacct.png)

## <a name="synchronizing-storage-account-credential-keys"></a>Depolama hesabı kimlik bilgileri anahtarları eşitleniyor
Güvenlik nedenleriyle, anahtar döndürme genellikle veri merkezlerinde gerekli değildir. Microsoft Azure yönetici yeniden oluşturmak veya hello depolama hesabı kimlik bilgilerini (aracılığıyla Microsoft Azure depolama hizmeti hello) doğrudan erişerek hello birincil veya ikincil anahtarı değiştirin. Merhaba StorSimple cihaz Yöneticisi hizmeti bu değişikliği otomatik olarak görmez.

tooinform hello StorSimple cihaz Yöneticisi hizmeti hello değişimin ihtiyacınız tooaccess hello StorSimple cihaz Yöneticisi hizmeti, erişim hello depolama kimlik bilgisi hesabı ve (hangisinin bağlı olarak değiştirildi) hello birincil veya ikincil anahtarı Eşitle. Merhaba hizmeti ardından hello en son anahtarın alır, hello anahtarları şifreler ve anahtar toohello aygıt hello şifrelenmiş gönderir.

#### <a name="toosynchronize-keys-for-storage-account-credentials-in-hello-same-subscription-as-hello-service-azure-only"></a>Depolama hesabı kimlik bilgilerini toosynchronize tuşları hello hizmet (yalnızca Azure) aynı abonelik hello
1. Merhaba hizmet giriş dikey penceresinde, hizmetinizi seçin, hello hizmet adını ve ardından hello çift **yapılandırma** 'yi tıklatın **depolama hesabının kimlik bilgilerini**.
2. Merhaba üzerinde **depolama hesabının kimlik bilgilerini** dikey penceresinde hello listesinde depolama hesabının kimlik bilgilerini seçin hello depolama hesabı kimlik bilgilerini toosynchronize istediğiniz, anahtarları.
3. Merhaba, **özellikleri** hello dikey penceresinde seçili depolama hesabı kimlik bilgileri, aşağıdaki hello:
   
    1. Tıklatın **daha fazla**ve ardından **eşitleme erişim tuşu**.
   
    2. Onayınız istendiğinde tıklatın **eşitleme anahtarı** toocomplete hello eşitleme.
    
4. Hello StorSimple cihaz Yöneticisi hizmeti, daha önce Microsoft Azure depolama hizmeti hello değiştirildi tooupdate hello anahtarı gerekir. Merhaba, **Eşitle depolama hesabı anahtarı** hello birincil erişim anahtarını (oluşturuldu) değiştirilmişse, dikey penceresinde, birincil tıklayın ve ardından **eşitleme anahtarı**. Merhaba ikincil anahtarı değiştirildiyse tıklatın **ikincil**ve ardından **eşitleme anahtarı**.
   
    ![Eşitleme erişim anahtarı](./media/storsimple-virtual-array-manage-storage-accounts/ova-sync-acess-key.png)

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[StorSimple sanal dizinizi yönetmek](storsimple-ova-web-ui-admin.md).

