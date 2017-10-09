---
title: aaaManage StorSimple cihaz denetleyicilerinin | Microsoft Docs
description: "Nasıl toostop, yeniden başlatın, kapatmak veya StorSimple cihaz denetleyicilerinin sıfırlama öğrenin."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4ee989d0-956f-4c14-951e-fd4e490ea09d
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/11/2016
ms.author: alkohli
ms.openlocfilehash: 9a86aa0f4a8fd96c36df206774972602c47a49a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>StorSimple cihaz Denetleyicilerini Yönet
## <a name="overview"></a>Genel Bakış
Bu öğretici, StorSimple cihaz denetleyicileri üzerinde gerçekleştirilen hello farklı işlemler açıklanmaktadır. StorSimple Cihazınızı Hello denetleyicileri yedek (eş) denetleyicileri bir Aktif-Pasif yapılandırmasında etkilenir. Belirli bir zamanda yalnızca bir denetleyici etkindir ve tüm hello disk ve ağ işlemlerini işleme. Merhaba diğer denetleyicisi edilgen modda değil. Merhaba etkin denetleyicisi başarısız olursa, hello pasif denetleyiciyi otomatik olarak etkinleşir.

Bu öğretici kullanarak adım adım yönergeler toomanage hello aygıt denetleyicileri içerir:

* **Denetleyicileri** hello bölümünü **Bakım** hello StorSimple Yöneticisi hizmet sayfası
* StorSimple için Windows PowerShell.

Merhaba StorSimple Yöneticisi hizmeti üzerinden hello cihaz Denetleyicilerini Yönet öneririz. Bir eylem yalnızca StorSimple için Windows PowerShell kullanarak gerçekleştirilebilir, hello öğretici Not yapar.

Bu öğretici okuduktan sonra aşağıdakileri gerçekleştirebilirsiniz:

* Yeniden başlatma veya kapatma StorSimple cihaz denetleyicisi
* Bir StorSimple cihazı kapatmak
* StorSimple cihaz toofactory Varsayılanları sıfırla

## <a name="restart-or-shut-down-a-single-controller"></a>Yeniden başlatma veya kapatma tek bir denetleyici
Bir denetleyici yeniden başlatma veya kapatma normal sistem işleminin bir parçası olarak gerekli değildir. Kapatma işlemleri tek aygıt denetleyicisi için yalnızca bir başarısız aygıt donanım bileşeni değiştirme gerektiren durumlarda yaygındır. Denetleyici yeniden başlatma, performans aşırı bellek kullanımı veya düzgün çalışmayan bir denetleyici tarafından etkilenir durumda da gerekebilir. Tooenable istiyor ve test yerini hello denetleyicisi başarılı denetleyicisi değiştirme işleminden toorestart bir denetleyici de gerekebilir.

Bir aygıt yeniden başlatma hello pasif denetleyiciyi kullanılabilir olduğunu varsayarak, kesintiye uğratan tooconnected başlatıcılarını değil. Bir pasif denetleyiciyi kullanılabilir değilse veya hello yeniden başlatarak kapalı, etkin açık denetleyicisi hizmeti ve kapalı kalma süresi hello kesilme neden olabilir.

> [!IMPORTANT]
> * **Bu artıklık kaybı ve kalma süresi riskin artmasına neden olur olarak çalışan bir denetleyicisinin hiçbir zaman fiziksel olarak kaldırılması gerekir.**
> * Merhaba aşağıdaki yordam yalnızca toohello StorSimple fiziksel cihazı geçerlidir. Toostart, durdurma ve yeniden başlatma hello sanal cihaz, nasıl görürüm hakkında bilgi için [iş hello sanal cihazla](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device).
> 
> 

Yeniden başlatma veya StorSimple için hello hello StorSimple Yöneticisi hizmeti Windows PowerShell veya Azure Klasik portalı kullanarak bir tek aygıt denetleyicisi kapatın

Merhaba Klasik Azure portalı, cihazı denetleyicilerinden toomanage gerçekleştirmek hello adımları izleyin.

#### <a name="toorestart-or-shut-down-a-controller-in-classic-portal"></a>toorestart veya Klasik Portalı'nda bir denetleyici kapatma
1. Çok gidin**cihazlar > Bakım**.
2. Çok Git**donanım durumu** ve hem hello denetleyicileri aygıtınızda hello durumunu olduğundan emin olun **sağlıklı**.
   
    ![StorSimple cihaz denetleyicilerinin sağlıklı olduğunu doğrula](./media/storsimple-manage-device-controller/IC766017.png)
3. Merhaba, hello Alttan **Bakım** sayfasında, **Denetleyicilerini Yönet**.
   
    ![StorSimple cihaz Denetleyicilerini Yönet](./media/storsimple-manage-device-controller/IC766018.png)</br>
   
   > [!NOTE]
   > Göremiyorsanız **Denetleyicilerini Yönet**, tooinstall güncelleştirmeleri yüklemeniz gerekir. Daha fazla bilgi için bkz: [StorSimple Cihazınızı güncelleştirin](storsimple-update-device.md).
   > 
   > 
4. Merhaba, **denetleyicisi ayarlarını değiştir** iletişim kutusunda, aşağıdaki hello:
   
   1. Merhaba gelen **Select Controller** açılan listesinden, select hello denetleyicisi toomanage istiyor. Merhaba denetleyici 0 ve denetleyici 1 seçeneklerdir. Bu denetleyicileri da etkin veya pasif olarak tanımlanır.
      
      > [!NOTE]
      > Bu bir denetleyici yönetilemez kullanılamıyor veya kapalı kapalı ve hello aşağı açılan listede görünmez.
      > 
      > 
   2. Merhaba gelen **Eylem Seç** aşağı açılan listesinde, seçin **yeniden denetleyicisi** veya **denetleyicisi Kapat**.
      
       ![StorSimple cihazı pasif denetleyiciyi yeniden Başlat](./media/storsimple-manage-device-controller/IC766020.png)
   3. Merhaba onay simgesine tıklayın ![Onay simgesi](./media/storsimple-manage-device-controller/IC740895.png).

Yeniden başlatın veya hello denetleyicisi kapatın. Merhaba tabloda özetlenmiştir hello yaptığınız hello seçimleri bağlı olarak neler hello ayrıntıları **denetleyicisi ayarlarını değiştir** iletişim kutusu.  

| Seçim # | İsterseniz... | Bu gerçekleşir. |
| --- | --- | --- |
| 1. |Merhaba pasif denetleyiciyi yeniden başlatın. |Bir işi toorestart hello denetleyicisi oluşturulur ve hello iş başarıyla oluşturulduktan sonra size bildirilecek. Bu hello denetleyicisi yeniden başlatır. Erişerek hello yeniden başlatma işlemi izleyebilirsiniz **hizmet > Pano > görüntülemek işlem günlükleri** ve parametreleri belirli tooyour hizmeti tarafından filtreleme. |
| 2. |Merhaba etkin denetleyicisini yeniden başlatın. |Uyarı aşağıdaki hello görürsünüz: "Merhaba etkin denetleyicisi yeniden başlatırsanız, hello aygıt toohello pasif denetleyiciyi başarısız olur. Toocontinue istiyorsunuz?" </br>Bu işlemle tooproceed seçerseniz, hello sonraki adımlar kullanılan aynı toothose toorestart hello pasif denetleyiciyi olacaktır (bkz. Seçimi 1). |
| 3. |Merhaba pasif denetleyiciyi kapatın. |İletiden hello görürsünüz: "kapatma tamamlandıktan sonra toopush gerekir hello güç düğmesine, denetleyici tooturn onu. Bu denetleyici aşağı tooshut istediğinizden emin misiniz?" </br>Bu işlemle tooproceed seçerseniz, hello sonraki adımlar kullanılan aynı toothose toorestart hello pasif denetleyiciyi olacaktır (bkz. Seçimi 1). |
| 4. |Merhaba etkin denetleyicisi kapatın. |İletiden hello görürsünüz: "kapatma tamamlandıktan sonra toopush gerekir hello güç düğmesine, denetleyici tooturn onu. Bu denetleyici aşağı tooshut istediğinizden emin misiniz?" </br>Bu işlemle tooproceed seçerseniz, hello sonraki adımlar kullanılan aynı toothose toorestart hello pasif denetleyiciyi olacaktır (bkz. Seçimi 1). |

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart veya StorSimple için Windows PowerShell'de denetleyicisi kapatma
Aşağı adımları tooshut aşağıdaki hello gerçekleştirmek veya tek bir denetleyici StorSimple Cihazınızı hello Klasik Azure portalı üzerinde yeniden başlatın.

1. Merhaba seri konsol veya uzak bir bilgisayardan telnet oturumu kullanarak hello aygıt erişim. TooController 0 bağlanın veya aşağıdaki hello tarafından Denetleyici 1 adımları [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**.
3. Merhaba başlık iletisi çok bağlı hello denetleyicisi Not (denetleyici 0 veya denetleyici 1) ve hello etkin veya Pasif (bekleme) denetleyicisi hello olup.
   
   * Merhaba isteminde türü tek bir denetleyici aşağı tooshut:
     
       `Stop-HcsController`
     
       Bu bağlı hello denetleyicisi kapatılır. Ardından hello etkin denetleyicisi durdurursanız, onu kapatılmadan önce toohello pasif denetleyiciyi başarısız olur.
   * toorestart bir denetleyicisinde hello istemine aşağıdakileri yazın:
     
       `Restart-HcsController`
     
       Bu, bağlandığınız hello denetleyicisi yeniden başlatılır. Merhaba etkin denetleyicisi yeniden başlatırsanız, hello yeniden başlatmadan önce toohello pasif denetleyiciyi başarısız olur.

## <a name="shut-down-a-storsimple-device"></a>Bir StorSimple cihazı kapatmak
Bu bölümde nasıl tooshut tuşunu çalışan bir ya da uzak bir bilgisayardan başarısız bir StorSimple cihazı. Bir aygıtın hem hello aygıt denetleyicileri kapatılıyor sonra kapalıdır. Merhaba cihaz fiziksel olarak taşındığı veya hizmet dışı gerçekleştirilecek bir aygıt kapatma yapılır.

> [!IMPORTANT]
> Merhaba cihazı kapatmanız önce hello cihaz bileşenlerini hello durumunu kontrol edin. Çok gidin**cihazlar > bakım > donanım durum** ve tüm hello bileşenlerinin hello LED durumunun yeşil olduğunu doğrulayın. Sağlıklı bir aygıtı yeşil durumu olacaktır. Cihazınızı ise olma tooreplace düzgün çalışmayan bir bileşen kapatın, başarısız (kırmızı) görürsünüz veya düşürülmüş (sarı) durumunun hello ilgili bileşenleri.
> 
> 

#### <a name="tooshut-down-a-storsimple-device"></a>StorSimple cihazı aşağı tooshut
1. Kullanım hello [yeniden başlatma veya kapatma denetleyicisi](#restart-or-shut-down-a-single-controller) yordamı tooidentify ve hello pasif denetleyiciyi aygıtınızda kapat. StorSimple için hello Klasik Azure portalı veya Windows PowerShell Bu işlemi gerçekleştirebilir.
2. Yukarıdaki adım tooshut hello etkin denetleyicisini Hello yineleyin.
3. Bu gibi durumlarda, hello adresindeki toolook şimdi geri hello aygıt düzlemi gerekir. Merhaba iki denetleyicileri tamamen kapatıldığından sonra hello hem hello denetleyicileri LED'leri durumuna kırmızı yanıp sönen. Merhaba aygıt devre dışı tooturn şu anda tamamen gerekiyorsa, güç ve soğutma modülleri (PCMs) Çevir hello güç anahtarları toohello OFF konumu. Bu hello aygıtı kapatıp açmanız gerekir.

<!--#### tooshut down a StorSimple device in Windows PowerShell for StorSimple

1. Connect toohello serial console of hello StorSimple device by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-serial-console).

1. In hello serial console menu, verify from hello banner message that hello controller you are connected toois hello passive controller. If you are connected toohello active controller, disconnect from this controller and connect toohello other controller.

1. In hello serial console menu, choose option 1, **log in with full access**.

1. At hello prompt, type:

    `Stop-HCSController`

    This should shut down hello current controller. tooverify whether hello shutdown has finished, check hello back of hello device. hello controller status LED should be solid red.

1. Repeat steps 1 through 4 tooconnect toohello active controller and then shut it down.

1. After both hello controllers are completely shut down, hello status LEDs on both should be blinking red. If you need tooturn off hello device completely at this time, flip hello power switches on both Power and Cooling Modules (PCMs) toohello OFF position.-->

## <a name="reset-hello-device-toofactory-default-settings"></a>Merhaba aygıt toofactory varsayılan ayarlarına sıfırlama
> [!IMPORTANT]
> Aygıt toofactory varsayılan ayarlarınızı tooreset gerekiyorsa, Microsoft Support başvurun. aşağıda açıklanan hello yordam yalnızca, Microsoft Support ile birlikte kullanılmalıdır.
> 
> 

Bu yordam açıklar nasıl tooreset StorSimple için Windows PowerShell kullanarak, Microsoft Azure StorSimple cihaz toofactory varsayılan ayarları.
Bir cihazı sıfırlamak tüm veriler ve ayarlar varsayılan olarak tüm küme hello kaldırır.

Aşağıdaki adımları tooreset hello Microsoft Azure StorSimple cihaz toofactory varsayılan ayarlarınızı gerçekleştirin:

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello toodefault için cihaz ayarları Windows PowerShell'de StorSimple
1. Erişim hello cihaz seri Konsolu aracılığıyla. Merhaba başlık iletisi tooensure bağlı toohello etkin denetleyicisi olduğundan emin olun.
2. Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**.
3. Merhaba istemine komut tooreset hello tüm küme aşağıdaki, tüm verileri, meta verilerini ve denetleyici ayarları kaldırılıyor hello yazın:
   
    `Reset-HcsFactoryDefault`
   
    tooinstead sıfırlama tek bir denetleyici, hello kullan [sıfırlama HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) hello cmdlet'iyle `-scope` parametresi.)
   
    Merhaba sistem birden çok kez yeniden başlatılır. Merhaba sıfırlama başarıyla tamamlandığında size bildirilecek. Hello sistem modeline bağlı olarak, bu işlem 45-60 dakika 8100 cihazınız ve 8600 toofinish 60-90 dakika sürebilir.
   
   > [!TIP]
   > * Daha önce hello kullanın veya güncelleştirme 1.2 kullanıyorsanız `–SkipFirmwareVersionCheck` parametresi tooskip hello bellenim sürümü denetimi (Aksi halde, bellenim uyuşmazlığı hatası görürsünüz: Fabrika sıfırlaması hello bellenim sürümleri tooa uyuşmazlık nedeniyle devam edemiyor. ).
   > * Merhaba Fabrika sıfırlaması yordamı güncelleştirme 1 veya 1.1 hello kamu Portalı'nda çalıştırıyorsanız ve başarılı tek veya çift denetleyicisi değiştirme (denetleyicileriyle öncesi güncelleştirme 1 sevk edilen değiştirme gerçekleştirmiş StorSimple cihazlar için başarısız olabilir yazılım). Merhaba Fabrika sıfırladığınızda görüntü hello dosyasının varlığı, yönetimin bir SHA1 yok hello denetleyicisinde güncelleştirme 1 yazılımı öncesini için için doğrulanır olur. Hata sıfırlama, Microsoft Support tooassist başvurun bu Fabrika görürseniz hello sizinle sonraki adımlar. Bu sorun, güncelleştirme 1 veya sonraki yazılım ile Merhaba Fabrika sevk değiştirme denetleyicileriyle görülmez.
   > 
   > 

## <a name="questions-and-answers-about-managing-device-controllers"></a>Sorular ve yanıtlar aygıt denetleyicileri yönetme hakkında
Bu bölümde, biz bazı sık sorulan sorular hello özetlenen sahipseniz yönetme StorSimple cihaz denetleyicilerinin ilgili.

**S.** Her ikisi de cihazımı denetleyicilerinde hello ne olur olan sağlıklı ve açıktır ve yeniden başlatma veya hello etkin denetleyicisi kapatma?

**C.** Hem hello denetleyicileri aygıtınızda sağlıklı ve açık ise, onaylamanız istenir. Seçebilirsiniz:

* **Merhaba etkin denetleyicisi yeniden** – denetleyicisini active yeniden hello aygıt toofail toohello pasif denetleyiciyi oluşturacağını bildirilir. Merhaba denetleyicisi yeniden başlatılır.
* **Etkin bir denetleyici Kapat** – denetleyicisini active kapatılıyor kapalı kalma sürelerine neden bildirilir. Merhaba aygıt tooturn hello denetleyicisinde toopush hello güç düğmesine de gerekir.

**S.** Cihazımı pasif denetleyicisinde hello kullanılamıyor veya açık ise Kapalı ve yeniden başlatın veya hello etkin denetleyicisi Kapat de ne olur?

**C.** Merhaba pasif aygıtınızda denetleyicisiyse kullanılamıyor veya kapalı kapalı ve aktarmayı seçin:

* **Merhaba etkin denetleyicisi yeniden** – size hello işleme devam ederseniz hello hizmetinin geçici kesilme neden olur ve onaylamanız istenir bildirilecek.
* **Etkin bir denetleyici Kapat** – hello işleme devam ederseniz kapalı kalma sürelerine neden ve biri veya her ikisi denetleyicileri tooturn hello aygıtta toopush hello güç düğmesine gerekir bilgilendirilirsiniz. Onayınız istenir.

**S.** Hello denetleyicisi yeniden başlatma veya kapatma başarısız olduğunda tooprogress?

**C.** Başlatma veya kapatma denetleyicisi başarısız olabilir:

* Aygıt güncelleştirmesi devam ediyor.
* Zaten bir denetleyici yeniden başlatma işlemi devam ediyor.
* Bir denetleyici kapatma zaten devam ediyor.

**S.** Nasıl, bir denetleyici veya yeniden kapatma anlayıp?

**C.** Merhaba bakım sayfasında hello denetleyicisi durumunu kontrol edebilirsiniz. Merhaba denetleyicisi durumunu bir denetleyicisi yeniden veya bırakıldığı kapatma olup olmadığını belirtir. Ayrıca, Hello denetleyicisi yeniden veya kapatıldıysa hello uyarılar sayfasında bir bilgilendirme uyarısı içerir. Merhaba denetleyicisi yeniden başlatma ve kapatma işlemleri de hello işlemi günlüklerine kaydedilir. İşlem günlükleri hakkında daha fazla bilgi için çok Git[görüntülemek hello işlem günlükleri](storsimple-service-dashboard.md#view-the-operations-logs).

**S.** Denetleyici yük devretmesi sonucunda herhangi bir etkisi toohello g/ç var mı?

**C.** Merhaba TCP bağlantılarını başlatıcıları ve etkin denetleyici arasında sonucunda denetleyici yük devretmesi sıfırlanacak, ancak işlemi hello pasif denetleyiciyi varsayar olduğunda yeniden. Bu işlem hello sürecinde g/ç etkinliğini başlatıcıları ve hello aygıtı arasında bir geçici (30 saniyeden daha az) duraklama olabilir.

**S.** Kapatılır ve kaldırılmış sonra nasıl my denetleyicisi tooservice dönüş?

**C.** bir denetleyici tooservice tooreturn, eklemeniz gerekir, hello kasaya açıklandığı gibi [Denetleyici Modülü, StorSimple Cihazınızda Değiştir](storsimple-controller-replacement.md).

## <a name="next-steps"></a>Sonraki adımlar
* Bu öğreticide, listelenen hello yordamları kullanarak çözümlenemiyor, StorSimple cihaz denetleyicilerini ile herhangi bir sorunla karşılaştığınızda [Microsoft Support başvurun](storsimple-contact-microsoft-support.md).
* Merhaba StorSimple Yöneticisi hizmetini kullanma hakkında daha fazla toolearn Git çok[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

