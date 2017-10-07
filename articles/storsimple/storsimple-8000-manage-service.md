---
title: "aaaDeploy hello Azure StorSimple Aygıt Yöneticisi'ni hizmetinde | Microsoft Docs"
description: "Nasıl toocreate ve delete hello Azure portal StorSimple Aygıt Yöneticisi'ni hizmetinde hello açıklar ve nasıl toomanage hello hizmet kayıt anahtarını açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: alkohli
ms.openlocfilehash: b84a907d6b735c8fee7bdc51f9c0074857297d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-8000-series-devices"></a>Merhaba StorSimple cihaz Yöneticisi hizmeti StorSimple 8000 serisi cihazlar için dağıtma

## <a name="overview"></a>Genel Bakış

Merhaba StorSimple cihaz Yöneticisi hizmeti Microsoft Azure üzerinde çalışır ve toomultiple StorSimple cihazları bağlanır. Hello hizmeti oluşturduktan sonra onu bağlı toohello StorSimple Aygıt Yöneticisi'ni tüm hello cihazlar hizmet toomanage tek, merkezi bir konumdan böylece yönetim yükünü en aza kullanabilirsiniz.

Bu öğreticide gerekli hello oluşturma, silme, hello hizmetinin geçişini ve hello hizmet kayıt anahtarını hello yönetimi için hello adımları açıklanmıştır. Bu makalede bulunan hello geçerli yalnızca tooStorSimple 8000 serisi cihazlar bilgilerdir. StorSimple sanal diziler hakkında daha fazla bilgi için çok Git[, StorSimple sanal dizisi için StorSimple Aygıt Yöneticisi'ni hizmet dağıtma](storsimple-virtual-array-manage-service.md).

## <a name="create-a-service"></a>Hizmet oluşturma
toocreate StorSimple cihaz Yöneticisi hizmeti, toohave gerekir:

* Bir aboneliği bir kurumsal anlaşma ile
* Etkin bir Microsoft Azure depolama hesabı
* Merhaba, erişim yönetimi için kullanılan bilgileri faturalama

Yalnızca bir kurumsal anlaşma ile Merhaba aboneliklerine izin verilir. Merhaba Klasik Azure portalı izin verilmekteydi Microsoft Sponsorship abonelikleri hello Azure portal desteklenmez. Desteklenmeyen bir abonelik kullanırken iletiden hello görürsünüz:

![Abonelik geçerli değil](./media/storsimple-8000-manage-service/subscription-not-valid.jpg)

Merhaba hizmeti oluşturduğunuzda, toogenerate varsayılan depolama hesabı seçebilirsiniz.

Tek bir hizmet birden çok cihazları yönetebilirsiniz. Ancak, bir aygıt birden fazla hizmet yayılamaz. Büyük bir kuruluş birden çok hizmet örnekleri toowork farklı Aboneliklerde, kuruluşlar veya bile dağıtım konumlarında olabilir. 

> [!NOTE]
> StorSimple cihaz Yöneticisi hizmeti toomanage StorSimple 8000 serisi cihazlar ve StorSimple sanal diziler ayrı örnekleri gerekir.

Aşağıdaki adımları toocreate hizmet hello gerçekleştirin.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]


Her StorSimple cihaz Yöneticisi hizmeti için öznitelikler aşağıdaki hello mevcuttur:

* **Ad** – oluşturulduğunda tooyour StorSimple cihaz Yöneticisi hizmeti atanan hello adı. **Merhaba hizmet adı Hello hizmeti oluşturulduktan sonra değiştirilemez. Bu, aynı zamanda cihazları, birimler, birim kapsayıcıları ve hello Azure portalında yeniden adlandırılamaz yedekleme ilkeleri gibi diğer varlıklar için de geçerlidir.**
* **Durum** – hello olabilir hello hizmetinin durumunu **etkin**, **oluşturma**, veya **çevrimiçi**.
* **Konum** – hello hello StorSimple cihaz dağıtılacak coğrafi konum.
* **Abonelik** – hello hizmetiniz ile ilişkili abonelik faturalama.

## <a name="move-a-service-tooazure-portal"></a>Bir hizmet tooAzure portalı taşıma
StorSimple 8000 serisi artık hello Azure portal yönetilebilir. Var olan bir hizmeti toomanage hello StorSimple cihazları varsa, hizmet toohello Azure portal taşıma öneririz. Merhaba hello StorSimple Yöneticisi hizmetiniz için Klasik Azure portalı 30 Eylül 2017 sonra kullanılabilir değil.

Merhaba seçeneği toomigrate toohello Azure portal aşamalı olarak kullanılabilir. Bir seçenek toomigrate tooAzure portal görüyor musunuz ancak toomove istediğiniz ve hello açıklandığı gibi hello geçiş işleminin etkisini gözden geçirdikten [geçiş için ilgili önemli noktalar](#considerations-for-transition), yapabilecekleriniz [bir istek göndermek](https://aka.ms/ss8000-cx-signup).

### <a name="considerations-for-transition"></a>Geçiş için ilgili önemli noktalar

Merhaba hizmetini taşımadan önce geçirme toohello yeni Azure portalına hello etkisini gözden geçirin.

#### <a name="before-you-transition"></a>Önce geçiş

* Cihazınızı güncelleştirme 3.0 veya üstü çalışıyor. Cihazınızı daha eski bir sürümü çalıştırıyorsa, hello en son güncelleştirmeleri yükleyin. Daha fazla bilgi için çok Git[yükleme güncelleştirme 4](storsimple-8000-install-update-4.md). Bir StorSimple bulut uygulaması (8010/8020) kullanıyorsanız, yeni bir bulut Gereci güncelleştirme 4.0 ile oluşturun. 

* Yeni Azure portalına geçti toohello olduktan sonra StorSimple Cihazınızı hello Azure Klasik portalı toomanage kullanamazsınız.

* Merhaba geçiş benzer ve hello cihaz için kapalı kalma süresi yok.

* Tüm hello StorSimple cihaz yöneticileri hello altında abonelik geçti belirtilmiş.

#### <a name="during-hello-transition"></a>Merhaba geçişi sırasında

* Cihazınızı hello portalından yönetemez.
* Katmanlama ve zamanlanmış yedeklemeler gibi işlemleri toooccur devam edin.
* Silmeyin hello geçiş işlemi devam ederken eski StorSimple cihaz yöneticileri hello.

#### <a name="after-hello-transition"></a>Merhaba geçişten sonra

* Bu gibi durumlarda, cihazlarınızı artık hello Klasik portalından yönetebilirsiniz.

* Merhaba mevcut Azure Hizmet Yönetimi (ASM) PowerShell cmdlet'lerini desteklenmez. Merhaba betikleri toomanage aygıtlarınızı hello Azure Resource Manager aracılığıyla güncelleştirin.

* Hizmet ve cihaz yapılandırmanızı korunur. Ayrıca tüm birimler ve yedekleme geçti toohello Azure portal değildir.

### <a name="begin-transition"></a>Begin geçiş

Aşağıdaki adımları tootransition Merhaba, hizmet toohello Azure portal gerçekleştirin.

1. Tooyour varolan StorSimple Yöneticisi hizmeti hello Klasik Portalı'nda gidin.

2. Merhaba StorSimple cihaz Yöneticisi hizmeti hello Azure portalında kullanılabilir olduğunu bildiren bir bildirim görür. Hello Azure portal, başvurulan tooas StorSimple cihaz Yöneticisi hizmeti hello hizmet olduğuna dikkat edin.

    ![Geçiş bildirim](./media/storsimple-8000-manage-service/service-transition1.jpg)

    1. Merhaba tam geçiş işleminin etkisini gözden geçirdiğinizden emin olun.
    2. Merhaba Klasik portalından taşınır StorSimple cihaz yöneticileri Hello listesini gözden geçirin.

3. Tıklatın **geçirmek**. Merhaba geçiş başlar ve birkaç dakika toocomplete alır.

Merhaba geçiş tamamlandıktan sonra aygıtlarınızı hello StorSimple Aygıt Yöneticisi'ni hizmetinde hello Azure portal aracılığıyla yönetebilirsiniz.

Hello Azure portal, yalnızca güncelleştirme 3.0 çalıştıran StorSimple cihazlar hello ve üzeri desteklenir. eski sürümlerini çalıştıran hello cihazlara sınırlı bir desteği. Merhaba, aşağıdaki tabloda summrizes hello Klasik toohello Azure Portalı ' geçirdikten sonra versios önceki tooUpdate 3.0 çalıştıran hello cihazda hangi işlemler desteklenir.

| İşlem                                                                                                                       | Destekleniyor      |
|---------------------------------------------------------------------------------------------------------------------------------|----------------|
| Bir cihaz kaydetme                                                                                                               | Evet            |
| Cihaz ayarları genel gibi ağ ve güvenlik yapılandırma                                                                | Evet            |
| Tarama, indirme ve güncelleştirmeleri yükle                                                                                             | Evet            |
| Aygıt devre dışı bırakma                                                                                                               | Evet            |
| Aygıtı silme                                                                                                                   | Evet            |
| Oluşturma, değiştirme ve bir birim kapsayıcısı Sil                                                                                   | Hayır             |
| Oluşturma, değiştirme ve bir birim Sil                                                                                             | Hayır             |
| Oluşturma, değiştirme ve bir yedekleme ilkesi silme                                                                                      | Hayır             |
| El ile yedekleyin                                                                                                            | Hayır             |
| Zamanlanmış yedekleyin                                                                                                         | Uygulanamaz |
| Bir yedekleme kümesini geri yükleme                                                                                                        | Hayır             |
| Güncelleştirme 3.0 ve sonraki sürümleri çalıştıran kopya tooa aygıt <br> Merhaba kaynak aygıt sürüm önceki tooUpdate 3.0 çalışıyor.                                | Evet            |
| Sürümleri önceki tooUpdate 3.0 çalıştıran kopya tooa cihaz                                                                          | Hayır             |
| Yük devretme kaynak aygıt olarak <br> (sürüm 3.0 önceki tooUpdate tooa aygıt güncelleştirme 3.0 ve sonraki sürümleri çalıştıran çalıştıran bir aygıttan)                                                               | Evet            |
| Hedef aygıt olarak yük devretme <br> (yazılım sürüm önceki tooUpdate 3.0 çalıştıran tooa cihaz)                                                                                   | Hayır             |
| Bir uyarı temizleyin                                                                                                                  | Evet            |
| Görünüm yedekleme ilkeleri, yedekleme kataloğu, birimler, birim kapsayıcıları, izleme grafikleri, işleri ve klasik Portalı'nda oluşturulan uyarılar | Evet            |
| Açma veya aygıt denetleyicileri kapatma                                                                                              | Evet            |


## <a name="delete-a-service"></a>Bir hizmeti silin

Bir hizmet silmeden önce hiçbir bağlı aygıtlar, kullandığınızdan emin olun. Merhaba hizmet kullanımdaysa hello bağlı aygıtları devre dışı bırakın. Merhaba, işlemi devre dışı bırakma hello bağlantı hello hizmeti ile Merhaba aygıt arasında sever ancak hello bulutta hello aygıt verilerini korumak.

> [!IMPORTANT]
> Hizmet silindikten sonra hello işlem geri alınamaz. Başka bir hizmetle kullanılabilmesi için önce hello hizmeti tarafından kullanılan herhangi bir aygıt toobe sıfırlama toofactory Varsayılanları gerekir. Bu senaryoda, hello yapılandırma yanı sıra hello aygıt hello yerel veriler kaybolur.

Aşağıdaki adımları toodelete hizmet hello gerçekleştirin.

### <a name="toodelete-a-service"></a>toodelete bir hizmeti

1. Arama hello hizmeti için toodelete istiyor. Tıklatın **kaynakları** simgesini ve sonra giriş hello uygun koşulları toosearch. Merhaba arama sonuçlarında toodelete istediğiniz hello hizmete tıklayın.

    ![Arama hizmeti toodelete](./media/storsimple-8000-manage-service/deletessdevman1.png)

2. Bu toohello StorSimple cihaz Yöneticisi hizmeti dikey götürür. **Sil**'e tıklayın.

    ![Hizmet silme](./media/storsimple-8000-manage-service/deletessdevman2.png)

3. Tıklatın **Evet** hello onay bildirim. Silinen hello hizmet toobe birkaç dakika sürebilir.

    ![Silme işlemini onaylama](./media/storsimple-8000-manage-service/deletessdevman3.png)

## <a name="get-hello-service-registration-key"></a>Merhaba hizmet kayıt anahtarını alın

Bir hizmeti başarıyla oluşturduktan sonra StorSimple cihazınızla hello hizmet tooregister gerekir. tooregister ilk StorSimple Cihazınızı hizmet kayıt anahtarını hello. tooregister ek cihazlar var olan bir StorSimple hizmeti ile Merhaba kayıt anahtarını ve (Merhaba ilk cihazda kayıt sırasında oluşturulan) hello hizmet verileri şifreleme anahtarı gerekir. Merhaba hizmet verileri şifreleme anahtarı hakkında daha fazla bilgi için bkz: [StorSimple güvenlik](storsimple-8000-security.md). Merhaba kayıt anahtarı erişerek alabileceğiniz **anahtarları** StorSimple Aygıt Yöneticisi'ni dikey penceresinde.

Aşağıdaki adımları tooget hello hizmet kayıt anahtarını hello gerçekleştirin.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

Merhaba hizmet kayıt anahtarı güvenli bir yerde tutun. Bu anahtar, yanı sıra hello hizmet verileri şifreleme anahtarı, bu hizmetiyle ek cihazlar tooregister gerekir. Merhaba hizmet kayıt anahtarı aldıktan sonra hello Windows PowerShell aracılığıyla cihazınızın StorSimple arabirimi için yapılandırmanız gerekir.

Ayrıntılar için toouse bu kayıt anahtarı, bkz: [adım 3: yapılandırmak ve storsimple için Windows PowerShell üzerinden hello cihazı](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Merhaba hizmet kayıt anahtarını yeniden oluşturma
Gerekli tooperform anahtar döndürme veya hizmet yöneticilerinin listesini hello değişip değişmediğini varsa tooregenerate hizmet kayıt anahtarı gerekir. Başlangıç anahtarı yeniden oluşturmak zaman hello yeni anahtar yalnızca sonraki cihazları kaydetmek için kullanılır. Bu işlem tarafından zaten kayıtlı olan hello aygıtları etkilenmez.

Aşağıdaki adımları tooregenerate hizmet kayıt anahtarını hello gerçekleştirin.

### <a name="tooregenerate-hello-service-registration-key"></a>tooregenerate hello hizmet kayıt anahtarı
1. Merhaba, **StorSimple Aygıt Yöneticisi'ni** dikey penceresinde çok Git**Yönetim &gt;**  **anahtarları**.
    
    ![Anahtarlar dikey penceresi](./media/storsimple-8000-manage-service/regenregkey2.png)

2. Merhaba, **anahtarları** dikey penceresinde tıklatın **yeniden**.

    ![Yeniden tıklatın](./media/storsimple-8000-manage-service/regenregkey3.png)
3. Merhaba, **üretme hizmet kayıt anahtarını** dikey penceresinde, gözden geçirme hello eylem gerekli hello zaman anahtarları yeniden oluşturuldu. Bu hizmetle kaydedilen tüm hello sonraki cihazlar hello yeni kayıt anahtarını kullanın. Tıklatın **yeniden** tooconfirm. Merhaba yeniden oluşturma işlemi tamamlandıktan sonra size bildirilir.

    ![Yeniden onaylayın](./media/storsimple-8000-manage-service/regenregkey4.png)

4. Yeni bir hizmet kayıt anahtarı görüntülenir.

5. Bu anahtarı kopyalayın ve bu hizmeti ile yeni aygıtları kaydetme için kaydedin.



## <a name="change-hello-service-data-encryption-key"></a>Değişiklik hello hizmet verileri şifreleme anahtarı
Hizmet veri şifreleme anahtarları kullanılan tooencrypt gizli müşteri, StorSimple Yöneticisi hizmet toohello StorSimple Cihazınızı gönderilen depolama hesabının kimlik bilgilerini gibi verilerdir. BT kuruluşunuzun hello depolama cihazlarında bir anahtar döndürme ilkesi varsa toochange bu anahtarlar düzenli aralıklarla gerekir. Merhaba anahtar değiştirme işlemi bağlı olarak biraz farklı olabilir bir tek veya birden çok cihazı hello StorSimple Yöneticisi hizmeti tarafından yönetilen yoktur. Daha fazla bilgi için çok Git[StorSimple güvenlik ve veri koruması](storsimple-8000-security.md).

Değişen hello hizmet verileri şifreleme anahtarı 3 adımlı bir işlemdir:

1. Azure Resource Manager için Windows PowerShell komut dosyalarını kullanarak bir aygıtı toochange hello hizmet verileri şifreleme anahtarı yetkilendirin.
2. StorSimple için Windows PowerShell kullanarak hello hizmet verileri şifreleme anahtarı değişikliği başlatır.
3. Birden çok StorSimple cihazınız varsa, hello hizmet verileri şifreleme anahtarı hello üzerindeki diğer cihazlar güncelleştirin.

### <a name="step-1-use-windows-powershell-script-tooauthorize-a-device-toochange-hello-service-data-encryption-key"></a>1. adım: Kullanım Windows PowerShell komut dosyası tooAuthorize bir aygıt toochange hello hizmet verileri şifreleme anahtarı
Genellikle, hello Aygıt Yöneticisi bu hello Hizmet Yöneticisi bir cihaz toochange hizmeti veri şifreleme anahtarları yetkilendirmek ister. Merhaba Hizmet Yöneticisi ardından hello aygıt toochange hello anahtarı yetkilendirecek.

Bu adım, hello Azure Resource Manager temelli betik kullanarak gerçekleştirilir. Merhaba Hizmet Yöneticisi uygun toobe yetkili bir CİHAZDAN seçebilirsiniz. yetkili toostart hello hizmet verileri şifreleme anahtarı değiştirin ardından işlem hello aygıttır. 

Merhaba komut dosyası kullanma hakkında daha fazla bilgi için çok Git[Authorize ServiceEncryptionRollover.ps1](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Hangi cihazların olabilir toochange hizmeti veri şifreleme anahtarları yetkili?
Bir aygıt hello yetkili tooinitiate hizmeti veri şifreleme anahtarı değişiklikleri kullanılabilmesi için öncelikle aşağıdaki ölçütleri karşılamalıdır:

* Merhaba cihaz çevrimiçi toobe hizmeti veri şifreleme anahtarı değişiklik yetkilendirme için uygun olmalıdır.
* Aynı aygıt yeniden 30 dakika sonra hello anahtar değiştirirseniz değil başlatıldı hello yetki verebilir.
* Merhaba anahtar değişikliği hello daha önceden yetkili aygıt tarafından başlatılmamış olması koşuluyla farklı bir cihaz yetki verebilir. Merhaba yeni cihaz yetkilendirildikten sonra hello eski aygıt hello değişiklik başlatamaz.
* Merhaba hizmet verileri şifreleme anahtarı Hello geçişi işlemi devam ederken bir aygıtı yetkilendirilemiyor.
* Başkalarının olmamasına karşın bazı hello hizmetine kayıtlı hello cihazların Merhaba şifrelemeyi gezinirken bir aygıtı yetki verebilir. 

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>2. adım: StorSimple tooinitiate hello hizmet verileri şifreleme anahtarı değişikliği için Windows PowerShell'i kullanın
StorSimple cihaz StorSimple hello arabirimde yetkili için bu adımı Windows PowerShell hello gerçekleştirilir.

> [!NOTE]
> Merhaba anahtar geçişi tamamlanana kadar hiçbir işlem hello Azure portal, StorSimple Yöneticisi hizmetinin gerçekleştirilebilir.
> 
> 

Merhaba cihaz seri Konsolu tooconnect toohello Windows PowerShell arabirimini kullanıyorsanız, hello aşağıdaki adımları gerçekleştirin.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>tooinitiate hello hizmet verileri şifreleme anahtarı değiştirme
1. Seçenek 1 toolog tam erişimle seçin.
2. Merhaba komut satırına aşağıdakini yazın:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Merhaba cmdlet'i başarıyla tamamlandıktan sonra yeni bir hizmet verileri şifreleme anahtarı alır. Kopyalayın ve bu anahtarı kullanmak için bu işlem 3. adımında kaydedin. Bu anahtar olacaktır hello StorSimple Yöneticisi hizmetine kayıtlı cihazlar kalan tüm hello tooupdate kullanılır.
   
   > [!NOTE]
   > Bu işlem, StorSimple cihaz yetkilendirme dört saat içinde başlatılmalıdır.
   > 
   > 
   
   Bu yeni anahtar hello hizmetine kayıtlı toohello gönderilen toobe tooall hello cihazları hizmetten daha sonra gönderilir. Bir uyarı sonra hello hizmet panosunda görüntülenir. Hello hizmet hello kayıtlı cihazlarda tüm hello işlemleri devre dışı bırakır ve hello Aygıt Yöneticisi ardından diğer cihazları tooupdate hello hizmeti veri şifreleme anahtarını hello gerekir. Ancak, hello g/ç (ana bilgisayar veri toohello bulut gönderme) kesilmiş olabilir değil.
   
   Tek bir cihazı kayıtlı tooyour hizmet varsa hello geçiş işlemi tamamlanmıştır ve hello sonraki adımı atlayabilirsiniz. Birden çok aygıtları kayıtlı tooyour hizmetiniz varsa, toostep 3 devam edin.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>3. adım: hello hizmet verileri şifreleme anahtarı başka StorSimple cihazlar üzerinde güncelleştir
Birden çok aygıtları kayıtlı tooyour StorSimple Yöneticisi hizmetiniz varsa bu adımları hello Windows PowerShell arabiriminde StorSimple Cihazınızı gerçekleştirilmesi gerekir. 2. adımda elde ettiğiniz hello anahtar StorSimple Cihazınızı StorSimple Yöneticisi hizmeti hello ile kayıtlı kalan tüm hello kullanılan tooupdate olmalıdır.

Adımları tooupdate hello hizmet verileri şifreleme aygıtınızda aşağıdaki hello gerçekleştirin.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>tooupdate hello hizmet verileri şifreleme anahtarı
1. Windows PowerShell için StorSimple tooconnect toohello konsolunu kullanın. Seçenek 1 toolog tam erişimle seçin.
2. Merhaba komut satırına aşağıdakini yazın:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Makalesinde aldığınız hello hizmet verileri şifreleme anahtarı sağlayan [2. adım: StorSimple tooinitiate hello hizmet verileri şifreleme anahtarı değişikliği için Windows PowerShell'i kullanın](#to-initiate-the-service-data-encryption-key-change).


## <a name="next-steps"></a>Sonraki adımlar
* Merhaba hakkında daha fazla bilgi [StorSimple dağıtım işlemi](storsimple-8000-deployment-walkthrough-u2.md).
* Daha fazla bilgi edinmek [StorSimple depolama hesabınızı yönetme](storsimple-8000-manage-storage-accounts.md).
* Hakkında daha fazla çok bilgi[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).
