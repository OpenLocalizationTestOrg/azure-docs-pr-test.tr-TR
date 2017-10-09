---
title: "aaaManage StorSimple depolama hesabınız | Microsoft Docs"
description: "Bir depolama hesabı için nasıl hello StorSimple Yöneticisi yapılandırma sayfası tooadd, düzenleme, silme veya döndürme hello güvenlik anahtarları kullanabileceğiniz açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 93207c40-e0eb-489e-8724-59fb94907081
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/29/2016
ms.author: v-sharos
ms.openlocfilehash: 78f408818ee8532dfaac445200048145547c987c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-storage-account"></a>Depolama hesabınızı Hello StorSimple Yöneticisi hizmet toomanage kullanın
## <a name="overview"></a>Genel Bakış
Merhaba **yapılandırma** hello StorSimple Yöneticisi hizmeti oluşturulan tüm hello genel hizmet parametreleri sayfası gösterir. Bu parametreler cihazları toohello hizmet bağlanır ve dahil uygulanan tooall hello olabilir:

* Depolama hesapları 
* Bant genişliği şablonları 
* Erişim denetimi kayıtları 

Bu öğretici hello nasıl kullanabileceğinizi açıklar **yapılandırma** sayfa tooadd, düzenleme veya silme depolama hesapları veya bir depolama hesabının hello güvenlik anahtarlarını döndürün.

 ![Yapılandırma sayfası](./media/storsimple-manage-storage-accounts/HCS_ConfigureService.png)  

Depolama hesapları aygıt kullanır tooaccess depolama hesabınızı bulut hizmeti sağlayıcısı ile Merhaba hello kimlik bilgilerini içerir. Microsoft Azure depolama hesapları için bu hello hesap adı ve hello birincil erişim anahtarı gibi kimlik bilgileridir. 

Merhaba üzerinde **yapılandırma** sayfası, tüm depolama abonelik faturalama hello için oluşturulan hesapları aşağıdaki bilgilerle hello içeren bir tablo biçiminde görüntülenir:

* **Ad** – oluşturulduğunda atanan benzersiz bir ad toohello hesabı hello.
* **SSL özellikli** – hello SSL etkin ve cihaz bulut iletişimidir hello güvenli kanal üzerinden olup olmadığını.
* **Tarafından kullanılan** – hello hello depolama hesabı kullanarak birimlerin sayısı.

Merhaba en yaygın görevleri ile ilgili hello üzerinde gerçekleştirilebilir toostorage hesapları **yapılandırma** sayfa şunlardır:

* Depolama hesabı ekleme 
* Bir depolama hesabı Düzenle 
* Bir depolama hesabını silme 
* Depolama hesaplarının anahtar döndürme 

## <a name="types-of-storage-accounts"></a>Depolama hesabı türleri
Üç tür StorSimple cihazınızla kullanılabilir depolama hesabı vardır.

* **Otomatik olarak oluşturulan depolama hesapları** – hello adı da anlaşılacağı gibi bu depolama hesap türü hello hizmet ilk oluşturulduğunda otomatik olarak oluşturulur. Bu depolama hesabının nasıl oluşturulduğu hakkında daha fazla toolearn bkz [1. adım: yeni bir hizmet Oluştur](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service) içinde [şirket içi StorSimple Cihazınızı dağıtma](storsimple-deployment-walkthrough.md). 
* **Merhaba hizmet Abonelikteki depolama hesapları** – hello ile ilişkili hello Azure depolama hesapları bunlar hello hizmeti, aynı abonelik. Bu depolama hesaplarından nasıl oluşturulduğunu, hakkında daha fazla toolearn bkz [Azure Storage hesapları hakkında](../storage/common/storage-create-storage-account.md). 
* **Depolama hesapları hello hizmet aboneliği dışında** – bunlar hizmetiniz ile ilişkili olmayan hello Azure depolama hesapları ve büyük olasılıkla önce önceden hello hizmeti oluşturuldu.

## <a name="add-a-storage-account"></a>Depolama hesabı ekleme
Benzersiz bir sağlayarak bir depolama hesabı ekleyebilirsiniz kolay adı ve erişim kimlik bilgilerini bağlı toohello depolama hesabıyla (Merhaba belirtilen bulut hizmeti sağlayıcısı). Cihaz ve hello bulut arasındaki ağ iletişimi için güvenli bir kanal hello Güvenli Yuva Katmanı (SSL) modunda toocreate etkinleştirme hello seçeneğiniz de vardır.

Verilen bulut hizmeti sağlayıcı için birden çok hesabı oluşturabilirsiniz. Ancak, bir depolama hesabı oluşturulduktan sonra hello bulut hizmet sağlayıcısı değiştirilemiyor unutmayın.

Merhaba depolama hesabı kaydedilirken, hello hizmeti toocommunicate bulut hizmeti sağlayıcısı ile çalışır. Merhaba kimlik bilgilerini ve sağladığınız hello erişim malzemeleri şu anda doğrulanır. Bir depolama hesabı yalnızca hello kimlik doğrulaması başarılı olursa oluşturulur. Merhaba kimlik doğrulama başarısız olursa, ilgili hata iletisi görüntülenir.

Azure portalında oluşturulan resource Manager depolama hesapları StorSimple ile de desteklenir. Merhaba Resource Manager depolama hesapları hello aşağı açılan listesinde seçimi için bir birim kapsayıcısı toocreate çalışırken gösterilmez yalnızca hello depolama hello Klasik Azure portalında oluşturulan hesapları görüntülenir. Resource Manager depolama hesaplarıyla bir depolama hesabı aşağıda açıklanan hello yordamı tooadd kullanılarak eklenen toobe gerekir.

> [!NOTE]
> bir depolama hesabı eklemek için hello yordamı kullanmakta olduğunuz hello StorSimple yazılım sürümü göre farklılık gösterir. StorSimple sürümünüzün emin toofollow hello doğru yordam olabilir.
> 
> 

[!INCLUDE [add-a-storage-account-update1](../../includes/storsimple-configure-new-storage-account-u1.md)]

[!INCLUDE [add-a-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="edit-a-storage-account"></a>Bir depolama hesabı Düzenle
Bir birim kapsayıcısı tarafından kullanılan bir depolama hesabı düzenleyebilirsiniz. Şu anda kullanımda olduğundan bir depolama hesabı düzenlerseniz, hello yalnızca alan kullanılabilir toomodify hello erişim hello depolama hesabı için bir anahtardır. Merhaba yeni depolama erişim tuşunu sağlayın ve güncelleştirilmiş hello ayarları kaydedin.

#### <a name="tooedit-a-storage-account"></a>tooedit bir depolama hesabı
1. Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adına çift tıklayın ve ardından **yapılandırma**.
2. Tıklatın **depolama hesapları Ekle/Düzenle**.
3. Merhaba, **Ekle/Düzenle depolama hesapları** iletişim kutusunda:
   
   1. Merhaba aşağı açılan listesinde **depolama hesapları**, toomodify istediğiniz var olan bir hesap seçin. Bu ayrıca hello hizmet ilk oluşturulduğunda otomatik olarak oluşturulan hello depolama hesapları ekleyebilirsiniz.
   2. Gerekirse, hello değiştirebileceğiniz varsa **SSL modunu etkinleştir** seçim.
   3. Depolama hesap erişim tuşlarınızı toorotate seçebilirsiniz. Bkz: [anahtar depolama hesapları dönüşünü](#key-rotation-of-storage-accounts) nasıl tooperform anahtar döndürme hakkında daha fazla bilgi.
   4. Merhaba onay simgesine ![onay simgesi](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png) toosave hello ayarları. Hello ayarları üzerinde hello güncelleştirilmeyecek **yapılandırma** sayfası. Tıklatın **kaydetmek** toosave hello yeni ayarları güncelleştirildi.
      
      ![Bir depolama hesabı Düzenle](./media/storsimple-manage-storage-accounts/HCs_AddEditStorageAccount.png)

## <a name="delete-a-storage-account"></a>Bir depolama hesabını silme
> [!IMPORTANT]
> Yalnızca bir birim kapsayıcısı tarafından kullanılmıyorsa, bir depolama hesabı silebilirsiniz. Bir depolama hesabı bir birim kapsayıcısı tarafından kullanılıyorsa, hello birim kapsayıcısı silmeniz ve ilişkili hello depolama hesabı silin.
> 
> 

#### <a name="toodelete-a-storage-account"></a>toodelete bir depolama hesabı
1. Merhaba StorSimple Yöneticisi hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adına çift tıklayın ve ardından **yapılandırma**.
2. Merhaba Tablo listesinde depolama hesapları, toodelete istediğiniz hello hesap gelin.
3. Sil simgesini (**x**) hello aşırı sağ sütundaki bu depolama hesabı için görünür. Merhaba tıklatın **x** simgesi toodelete hello kimlik bilgileri.
4. Onayınız istendiğinde tıklatın **Evet** toocontinue hello silme işlemi ile. Merhaba sekmeli liste güncelleştirilmiş tooreflect hello değişiklikler.

## <a name="key-rotation-of-storage-accounts"></a>Depolama hesaplarının anahtar döndürme
Güvenlik nedenleriyle, anahtar döndürme genellikle veri merkezlerinde gerekli değildir. 

> [!NOTE]
> Aşağıdaki anahtar döndürme bilgileri ve hello döndürme yordamı hello tooMicrosoft Azure storage hesapları yalnızca uygulayın. Başka bir bulut hizmet sağlayıcısı kullanıyorsanız, depolama hesabı anahtarlarını sağlayıcının Pano üzerinden yönetebilirsiniz.
> 
> 

Her bir Microsoft Azure aboneliği bir veya daha fazla ilişkili depolama hesapları olabilir. Merhaba erişim toothese hesapları hello aboneliği ve her depolama hesabının erişim anahtarlarını tarafından denetlenir. 

Bir depolama hesabı oluşturduğunuzda, Microsoft Azure hello depolama hesabı erişildiğinde, kimlik doğrulaması için kullanılan iki 512 bit depolama erişim tuşu oluşturur. İki depolama erişim tuşu sahip olmanız tooregenerate hello anahtarlarla herhangi kesinti tooyour depolama hizmeti veya erişim toothat hizmeti sağlar. Merhaba, şu anda kullanımda hello anahtardır *birincil* anahtar ve hello yedekleme anahtarıdır başvurulan tooas hello *ikincil* anahtarı. Microsoft Azure StorSimple Cihazınızı bulut depolama hizmeti sağlayıcısı eriştiğinde, bu iki anahtarlarından birini sağlanmalıdır.

## <a name="what-is-key-rotation"></a>Anahtar döndürme nedir?
Genellikle, uygulamalar, verilerinizi hello anahtarları tooaccess yalnızca birini kullanın. Belirli bir süre süre sonra toousing hello ikinci anahtarı üzerinde anahtar uygulamalarınız olabilir. Uygulamaları toohello ikincil anahtar geçirildikten sonra hello ilk anahtar devre dışı bırakmak ve ardından yeni bir anahtar oluşturun. Bu şekilde Hello iki tuşlarını kullanarak uygulamaları erişim toohello verilerinizi kapalı kalma süresi olmadan aktarabilmesini sağlar.

Merhaba depolama hesabı anahtarlarını her zaman hello hizmet şifrelenmiş biçimde depolanır. Ancak, bunlar hello StorSimple Yöneticisi hizmeti sıfırlanabilir. Merhaba hizmet hello birincil anahtar alabilir ve ikincil anahtar tüm hello hello varsayılan depolama hesaplarının yanı sıra hello depolama hizmeti içinde oluşturulan hesapların dahil olmak üzere aynı abonelik oluşturulan depolama hesaplarında hello için ne zaman hello StorSimple Yöneticisi hizmeti hizmeti ilk oluşturuldu. Merhaba StorSimple Yöneticisi hizmeti her zaman bu anahtarları hello Klasik Azure Portalı ' almak ve bunları bir şifrelenmiş biçimde depolamak.

## <a name="rotation-workflow"></a>Döndürme iş akışı
Microsoft Azure yönetici yeniden oluşturmak veya hello depolama hesabı (aracılığıyla Microsoft Azure depolama hizmeti hello) doğrudan erişerek hello birincil veya ikincil anahtarı değiştirin. Merhaba StorSimple Yöneticisi hizmeti bu değişikliği otomatik olarak görmez.

tooinform hello StorSimple Yöneticisi hizmeti hello değişikliği gerekir tooaccess hello StorSimple Yöneticisi hizmeti, erişim hello depolama hesabı ve (hangisinin bağlı olarak değiştirildi) hello birincil veya ikincil anahtarı Eşitle. Merhaba hizmeti ardından hello en son anahtarın alır, hello anahtarları şifreler ve anahtar toohello aygıt hello şifrelenmiş gönderir.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service-azure-only"></a>Merhaba hizmet (yalnızca Azure) aynı abonelik toosynchronize anahtarları depolama hesaplarını hello
1. Merhaba üzerinde **Hizmetleri** hello sayfasında, **yapılandırma** sekmesi.
2. Tıklatın **depolama hesapları Ekle/Düzenle**.
3. Merhaba iletişim kutusunda, aşağıdaki hello:
   
   1. Merhaba depolama hesabını hello anahtarla toosynchronize istediğinizi seçin. Bunlar görüntülendiğinde hello depolama hesabı anahtarlarını şifrelenir.
   2. Hello StorSimple Yöneticisi hizmeti, daha önce Microsoft Azure depolama hizmeti hello değiştirildi tooupdate hello anahtarı gerekir. Merhaba birincil erişim anahtarını (oluşturuldu) değiştirilmişse, tıklatın **birincil anahtarı Eşitle**. Merhaba ikincil anahtarı değiştirildiyse tıklatın **ikincil anahtarı Eşitle**.
      
      ![anahtarları Eşitle](./media/storsimple-manage-storage-accounts/HCS_KeyRotationStorageAccountSameSubscriptionAsService.png)

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>Depolama hesapları hello hizmet aboneliği dışında toosynchronize tuşları
1. Merhaba üzerinde **Hizmetleri** hello sayfasında, **yapılandırma** sekmesi.
2. Tıklatın **depolama hesapları Ekle/Düzenle**.
3. Merhaba iletişim kutusunda, aşağıdaki hello:
   
   1. Merhaba depolama hesabı hello erişim anahtarı ile tooupdate istediğinizi seçin.
   2. Tooupdate hello depolama erişim tuşu hello StorSimple Yöneticisi hizmeti gerekir. Bu durumda, hello depolama erişim tuşu görebilirsiniz. Hello Hello yeni anahtarı girin **depolama hesabının erişim anahtarı**y kutusu. 
   3. Yaptığınız değişiklikleri kaydedin. Depolama hesabı erişim anahtarınızı şimdi güncelleştirilmesi gerekir.

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [StorSimple güvenlik](storsimple-security.md).
* Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

