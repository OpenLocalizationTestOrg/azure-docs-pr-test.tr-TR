---
title: "aaaManage StorSimple 8000 serisi aygıt denetleyicileri | Microsoft Docs"
description: "Nasıl toostop, yeniden başlatın, kapatmak veya StorSimple cihaz denetleyicilerinin sıfırlama öğrenin."
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
ms.date: 06/19/2017
ms.author: alkohli
ms.openlocfilehash: 5c59582b7ccf7cfeae9e7efbd0e4df9dc1d3871c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>StorSimple cihaz Denetleyicilerini Yönet

## <a name="overview"></a>Genel Bakış

Bu öğretici, StorSimple cihaz denetleyicileri üzerinde gerçekleştirilen hello farklı işlemler açıklanmaktadır. StorSimple Cihazınızı Hello denetleyicileri yedek (eş) denetleyicileri bir Aktif-Pasif yapılandırmasında etkilenir. Belirli bir zamanda yalnızca bir denetleyici etkindir ve tüm hello disk ve ağ işlemlerini işleme. Merhaba diğer denetleyicisi edilgen modda değil. Merhaba etkin denetleyicisi başarısız olursa, hello pasif denetleyiciyi otomatik olarak etkinleşir.

Bu öğretici kullanarak adım adım yönergeler toomanage hello aygıt denetleyicileri içerir:

* **Denetleyicileri** dikey aygıtınızın hello StorSimple cihaz Yöneticisi hizmeti.
* StorSimple için Windows PowerShell.

Merhaba StorSimple cihaz Yöneticisi hizmeti üzerinden hello cihaz Denetleyicilerini Yönet öneririz. Bir eylem yalnızca StorSimple için Windows PowerShell kullanarak gerçekleştirilebilir, hello öğretici Not yapar.

Bu öğretici okuduktan sonra aşağıdakileri gerçekleştirebilirsiniz:

* Yeniden başlatma veya kapatma StorSimple cihaz denetleyicisi
* Bir StorSimple cihazı kapatmak
* StorSimple cihaz toofactory Varsayılanları sıfırla

## <a name="restart-or-shut-down-a-single-controller"></a>Yeniden başlatma veya kapatma tek bir denetleyici
Bir denetleyici yeniden başlatma veya kapatma normal sistem işleminin bir parçası olarak gerekli değildir. Kapatma işlemleri tek aygıt denetleyicisi için yalnızca bir başarısız aygıt donanım bileşeni değiştirme gerektiren durumlarda yaygındır. Denetleyici yeniden başlatma, performans aşırı bellek kullanımı veya düzgün çalışmayan bir denetleyici tarafından etkilenir durumda da gerekebilir. Tooenable istiyor ve test yerini hello denetleyicisi başarılı denetleyicisi değiştirme işleminden toorestart bir denetleyici de gerekebilir.

Bir aygıt yeniden başlatma hello pasif denetleyiciyi kullanılabilir olduğunu varsayarak, kesintiye uğratan tooconnected başlatıcılarını değil. Bir pasif denetleyiciyi kullanılabilir değilse veya hello yeniden başlatarak kapalı, etkin açık denetleyicisi hizmeti ve kapalı kalma süresi hello kesilme neden olabilir.

> [!IMPORTANT]
> * **Bu artıklık kaybı ve kalma süresi riskin artmasına neden olur olarak çalışan bir denetleyicisinin hiçbir zaman fiziksel olarak kaldırılması gerekir.**
> * Merhaba aşağıdaki yordam yalnızca toohello StorSimple fiziksel cihazı geçerlidir. Toostart, durdurma ve yeniden başlatma hello StorSimple bulut uygulaması nasıl görürüm hakkında bilgi için [iş hello bulut uygulaması ile](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance).

Yeniden başlatın veya tek bir aygıtta denetleyicisini hello hello StorSimple cihaz Yöneticisi hizmeti Windows PowerShell veya Azure portal aracılığıyla StorSimple için kapatın.

hello Azure portalı, cihazı denetleyicilerinden toomanage gerçekleştirmek hello adımları izleyin.

#### <a name="toorestart-or-shut-down-a-controller-in-azure-portal"></a>toorestart veya Azure portalında bir denetleyici kapatma
1. StorSimple cihaz Yöneticisi hizmetinize çok Git**aygıtları**. Cihazınızı hello aygıtları listesinden seçin. 

    ![Bir cihaz seçin](./media/storsimple-8000-manage-device-controller/manage-controller1.png)

2. Çok Git**ayarlar > denetleyicileri**.
   
    ![StorSimple cihaz denetleyicilerinin sağlıklı olduğunu doğrula](./media/storsimple-8000-manage-device-controller/manage-controller2.png)
3. Merhaba, **denetleyicileri** dikey penceresinde, hem hello denetleyicileri aygıtınızda hello durumunu doğrulayın **sağlıklı**. Bir denetleyici seçin, sağ tıklayın ve ardından **yeniden** veya **kapatma**.

    ![StorSimple cihaz denetleyicilerinin kapatın veya yeniden başlatma seçin](./media/storsimple-8000-manage-device-controller/manage-controller3.png)

4. Bir iş toorestart oluşturulan veya hello denetleyicisi kapatmak ve varsa geçerli uyarılarla sunulur. toomonitor hello yeniden başlatma veya kapatma, Git çok**hizmet > etkinlik günlükleri** ve parametreleri belirli tooyour hizmeti tarafından filtre. Bir denetleyici kapatıldı sonra toopush hello güç düğmesi tooturn hello denetleyicisi tooturn üzerinde gerekir üzerinde.

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart veya StorSimple için Windows PowerShell'de denetleyicisi kapatma
Aşağı adımları tooshut aşağıdaki hello gerçekleştirmek veya StorSimple Cihazınızı hello Windows PowerShell üzerinde tek bir denetleyici için StorSimple yeniden başlatın.

1. Merhaba seri konsol veya uzak bir bilgisayardan telnet oturumu aracılığıyla erişim hello aygıtı. tooconnect tooController 0 veya denetleyici 1 izleyin hello adımlarda [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**.
3. Merhaba başlık iletisi çok bağlı hello denetleyicisi Not (denetleyici 0 veya denetleyici 1) ve hello etkin veya Pasif (bekleme) denetleyicisi hello olup.
   
   * Merhaba isteminde türü tek bir denetleyici aşağı tooshut:
     
       `Stop-HcsController`
     
       Bu, bağlandığınız hello denetleyicisi kapatır. Merhaba etkin denetleyicisi durdurursanız hello aygıt toohello pasif denetleyiciyi başarısız olur.

   * toorestart bir denetleyicisinde hello istemine aşağıdakileri yazın:
     
       `Restart-HcsController`
     
       Bu, bağlandığınız hello denetleyicisi yeniden başlatır. Merhaba etkin denetleyicisi yeniden başlatırsanız, hello yeniden başlatmadan önce toohello pasif denetleyiciyi başarısız olur.

## <a name="shut-down-a-storsimple-device"></a>Bir StorSimple cihazı kapatmak

Bu bölümde nasıl tooshut tuşunu çalışan bir ya da uzak bir bilgisayardan başarısız bir StorSimple cihazı. Her iki hello aygıt denetleyicileri kapatma sonra bir aygıtı devre dışı bırakılır. Merhaba aygıt fiziksel olarak taşındığında veya hizmet dışı gerçekleştirilecek bir aygıt kapatma yapılır.

> [!IMPORTANT]
> Merhaba cihazı kapatmanız önce hello cihaz bileşenlerini hello durumunu kontrol edin. Tooyour aygıt gidin ve ardından **ayarlar > donanım durumu**. Merhaba, **durumu ve donanım durumunu** dikey penceresinde tüm hello bileşenlerinin hello LED durumunun yeşil olduğunu doğrulayın. Sağlıklı bir aygıtı yeşil durum vardır. Cihazınızı ise olma tooreplace düzgün çalışmayan bir bileşen kapatın, başarısız (kırmızı) görürsünüz veya düşürülmüş (sarı) durumunun hello ilgili bileşenleri.


#### <a name="tooshut-down-a-storsimple-device"></a>StorSimple cihazı aşağı tooshut

1. Kullanım hello [yeniden başlatma veya kapatma denetleyicisi](#restart-or-shut-down-a-single-controller) yordamı tooidentify ve hello pasif denetleyiciyi aygıtınızda kapat. StorSimple için hello Azure portalı veya Windows PowerShell Bu işlemi gerçekleştirebilir.
2. Yukarıdaki adım tooshut hello etkin denetleyicisini Hello yineleyin.
3. Merhaba şimdi geri ve hello aygıt düzlemi benzemelidir. Merhaba iki denetleyicileri tamamen kapatıldığından sonra hello hem hello denetleyicileri LED'leri durumuna kırmızı yanıp sönen. Merhaba aygıt devre dışı tooturn şu anda tamamen gerekiyorsa, güç ve soğutma modülleri (PCMs) Çevir hello güç anahtarları toohello OFF konumu. Bu hello aygıtı kapatıp açmanız gerekir.

## <a name="reset-hello-device-toofactory-default-settings"></a>Merhaba aygıt toofactory varsayılan ayarlarına sıfırlama

> [!IMPORTANT]
> Aygıt toofactory varsayılan ayarlarınızı tooreset gerekiyorsa, Microsoft Support başvurun. aşağıda açıklanan hello yordam yalnızca, Microsoft Support ile birlikte kullanılmalıdır.

Bu yordam açıklar nasıl tooreset StorSimple için Windows PowerShell kullanarak, Microsoft Azure StorSimple cihaz toofactory varsayılan ayarları.
Bir cihazı sıfırlamak tüm veriler ve ayarlar varsayılan olarak tüm küme hello kaldırır.

Aşağıdaki adımları tooreset hello Microsoft Azure StorSimple cihaz toofactory varsayılan ayarlarınızı gerçekleştirin:

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello toodefault için cihaz ayarları Windows PowerShell'de StorSimple
1. Erişim hello cihaz seri Konsolu aracılığıyla. Merhaba başlık iletisi tooensure bağlı toohello olduğunu denetleyin **etkin** denetleyicisi.
2. Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**.
3. Merhaba istemine komut tooreset hello tüm küme aşağıdaki, tüm verileri, meta verilerini ve denetleyici ayarları kaldırılıyor hello yazın:
   
    `Reset-HcsFactoryDefault`
   
    tooinstead sıfırlama tek bir denetleyici, hello kullan [sıfırlama HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) hello cmdlet'iyle `-scope` parametresi.)
   
    Merhaba sistem birden çok kez yeniden başlatılır. Merhaba sıfırlama başarıyla tamamlandığında size bildirilecek. Hello sistem modeline bağlı olarak, bu işlem 45-60 dakika 8100 cihazınız ve 8600 toofinish 60-90 dakika sürebilir.
   
## <a name="questions-and-answers-about-managing-device-controllers"></a>Sorular ve yanıtlar aygıt denetleyicileri yönetme hakkında
Bu bölümde, biz bazı sık sorulan sorular hello özetlenen sahipseniz yönetme StorSimple cihaz denetleyicilerinin ilgili.

**S.** Her ikisi de cihazımı denetleyicilerinde hello ne olur olan sağlıklı ve açıktır ve yeniden başlatma veya hello etkin denetleyicisi kapatma?

**C.** Hem hello denetleyicileri aygıtınızda sağlıklı ve açık ise, onaylamanız istenir. Seçebilirsiniz:

* **Merhaba etkin denetleyicisi yeniden** – denetleyicisini active yeniden hello aygıt toofail toohello pasif denetleyiciyi açtığını bildirilir. Merhaba denetleyicisi yeniden başlatır.
* **Etkin bir denetleyici Kapat** – denetleyicisini active kapatılıyor kapalı kalma süresi ile sonuçları bildirilir. Ayrıca toopush hello güç düğmesine hello aygıt tooturn hello denetleyicisinde gerekir.

**S.** Cihazımı pasif denetleyicisinde hello kullanılamıyor veya açık ise Kapalı ve yeniden başlatın veya hello etkin denetleyicisi Kapat de ne olur?

**C.** Merhaba pasif aygıtınızda denetleyicisiyse kullanılamıyor veya kapalı kapalı ve aktarmayı seçin:

* **Merhaba etkin denetleyicisi yeniden** – hello işleme devam ederseniz hello hizmetinin geçici kesilme neden olur ve onaylamanız istenir bildirilir.
* **Etkin bir denetleyici Kapat** – devam ediliyor hello işlemi kapalı kalma süresi ile sonuçları bildirilir. Ayrıca toopush hello güç düğmesine hello aygıtta biri veya her ikisi denetleyicileri tooturn gerekir. Onayınız istenir.

**S.** Hello denetleyicisi yeniden başlatma veya kapatma başarısız olduğunda tooprogress?

**C.** Başlatma veya kapatma denetleyicisi başarısız olabilir:

* Aygıt güncelleştirmesi devam ediyor.
* Zaten bir denetleyici yeniden başlatma işlemi devam ediyor.
* Bir denetleyici kapatma zaten devam ediyor.

**S.** Nasıl, bir denetleyici veya yeniden kapatma anlayıp?

**C.** Denetleyici dikey penceresinde hello denetleyicisi durumunu kontrol edebilirsiniz. Merhaba denetleyicisi durumu yeniden başlatma veya kapatma hello işlemi bir denetleyicisi olup olmadığını belirtir. Ayrıca, hello **uyarıları** dikey penceresinde hello denetleyicisi yeniden veya kapatıldıysa bir bilgilendirme uyarısı içerir. Merhaba denetleyicisi yeniden başlatma ve kapatma işlemleri de hello acitivity günlüklerine kaydedilir. Acitivity günlükleri hakkında daha fazla bilgi için çok Git[görüntülemek hello etkinlik günlükleri](storsimple-8000-service-dashboard.md#view-the-activity-logs).

**S.** Denetleyici yük devretmesi sonucunda herhangi bir etkisi toohello g/ç var mı?

**C.** Merhaba TCP bağlantılarını başlatıcıları ve etkin denetleyici arasında sonucunda denetleyici yük devretmesi sıfırlanacak, ancak işlemi hello pasif denetleyiciyi varsayar olduğunda yeniden. Bu işlem hello sürecinde g/ç etkinliğini başlatıcıları ve hello aygıtı arasında bir geçici (30 saniyeden daha az) duraklama olabilir.

**S.** Kapatılır ve kaldırılmış sonra nasıl my denetleyicisi tooservice dönüş?

**C.** bir denetleyici tooservice tooreturn, eklemeniz gerekir, hello kasaya açıklandığı gibi [Denetleyici Modülü, StorSimple Cihazınızda Değiştir](storsimple-8000-controller-replacement.md).

## <a name="next-steps"></a>Sonraki adımlar
* Bu öğreticide, listelenen hello yordamları kullanarak çözümlenemiyor, StorSimple cihaz denetleyicilerini ile herhangi bir sorunla karşılaştığınızda [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md).
* Merhaba StorSimple cihaz Yöneticisi hizmetini kullanma hakkında daha fazla toolearn Git çok[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).

