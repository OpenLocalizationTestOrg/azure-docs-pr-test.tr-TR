---
title: "Kamu portalında aaaDeploy StorSimple 8000 serisi cihaz | Microsoft Docs"
description: "Güncelleştirme 3'ü çalıştıran StorSimple 8000 serisi cihaz hello ve daha sonra ve hello hello Azure kamu portal hizmet dağıtımı için hello adımları ve en iyi uygulamaları açıklar."
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
ms.workload: NA
ms.date: 06/22/2017
ms.author: alkohli
ms.openlocfilehash: ea643cd59dcdf17482268d14c1348a3b5fb098b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-hello-government-portal"></a>Şirket içi StorSimple Cihazınızı hello kamu portalında dağıtma

## <a name="overview"></a>Genel Bakış
TooMicrosoft Azure StorSimple cihaz dağıtımına Hoş Geldiniz. Bu dağıtım öğreticileri toohello StorSimple 8000 serisi çalışan güncelleştirme 3'ü yazılım ya da daha sonra da hello Azure kamu portal geçerlidir. Bu dizi öğreticiler bir yapılandırma denetim listesi, yapılandırma önkoşulları ve StorSimple cihazınız için ayrıntılı yapılandırma adımlarını listesini içerir.

Bu öğreticilerdeki bilgiler Hello hello güvenlik önlemlerini gözden geçirdiğinizi ve açılmış, yerleştirdiğinizi ve StorSimple Cihazınızı kablolu olduğunu varsayar. Bu görevler tooperform hala gerekiyorsa, hello inceleyerek başlayın [güvenlik önlemlerini](storsimple-safety.md). Toounpack, rafa monte etme ve Cihazınızı kablo hello cihaza özel yönergeleri izleyin.

* [8100 model cihazınızı kutusundan çıkarma, rafa takma ve kablolarını bağlama](storsimple-8100-hardware-installation.md)
* [8600 model cihazınızı kutusundan çıkarma, rafa takma ve kablolarını bağlama](storsimple-8600-hardware-installation.md)

Kurulum ve yapılandırma yönetici ayrıcalıkları toocomplete hello işlemi gerekir. Başlamadan önce hello yapılandırma denetim listesini gözden geçirmenizi öneririz. Merhaba dağıtım ve yapılandırma işlemi biraz zaman toocomplete alabilir.

> [!NOTE]
> Merhaba Hello Microsoft Azure Web sitesinde yayınlanan StorSimple dağıtım bilgileri tooStorSimple 8000 serisi cihazlar yalnızca geçerlidir. Merhaba 7000 Serisi cihazlar hakkında tam bilgi için: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). 7000 Serisi dağıtım bilgileri için bkz: Merhaba [StorSimple sistemi Hızlı Başlangıç Kılavuzu](http://onlinehelp.storsimple.com/111_Appliance/).


## <a name="deployment-steps"></a>Dağıtım adımları
StorSimple Cihazınızı bu gerekli adımları tooconfigure gerçekleştirin ve tooyour StorSimple cihaz Yöneticisi hizmetine bağlanın. Ayrıca toohello adımlar gerekli, isteğe bağlı adım ve yordamları hello dağıtımı sırasında toocomplete gerekebilir vardır. Bu isteğe bağlı adımların her biri gerçekleştirmesi gereken zaman hello adım adım dağıtım yönergeleri gösterir.

| Adım | Açıklama |
| --- | --- |
| **ÖNKOŞULLAR** |Bunlar hello yaklaşan dağıtıma tamamlandı toobe gerekir. |
| [Dağıtım yapılandırma denetim listesi](#deployment-configuration-checklist) |Bu denetim listesi toogather ve kayıt bilgileri önceki tooand hello dağıtımı sırasında kullanın. |
| [Dağıtım önkoşulları](#deployment-prerequisites) |Bunlar bu hello doğrulamak için dağıtım ortamı hazır. |
|  | |
| **ADIM ADIM DAĞITIM** |Bu adımlar StorSimple Cihazınızı üretimde gerekli toodeploy şunlardır. |
| [1. Adım: Yeni bir hizmet oluşturun](#step-1-create-a-new-service) |StorSimple cihazınız için bulut yönetimi ve depolamayı ayarlayın. *Başka StorSimple cihazlar için bir hizmetiniz varsa, bu adımı atlayın*. |
| [2. adım: hello hizmet kayıt anahtarını alın](#step-2-get-the-service-registration-key) |StorSimple Cihazınızı hello yönetim hizmetine bağlamak ve bu anahtar tooregister kullanın. |
| [3. adım: Yapılandırmak ve storsimple için Windows PowerShell üzerinden hello cihazı](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |Merhaba aygıt tooyour ağa bağlanma ve Azure toocomplete hello Kurulum hello Yönetim hizmetini kullanarak kaydedin. |
| [4. adım: hello minimum cihaz kurulumunu tamamlayın](#step-4-complete-minimum-device-setup) </br>İsteğe bağlı: StorSimple cihazınızı güncelleştirin. |Merhaba management hizmeti toocomplete hello cihaz Kurulumu kullanın ve tooprovide depolama etkinleştirin. |
| [5. Adım: Birim kapsayıcısı oluşturun](#step-5-create-a-volume-container) |Bir kapsayıcı tooprovision birim oluşturun. Bir birim kapsayıcısı, depolama hesabı, bant genişliği ve içerdiği tüm hello birimleri için şifreleme ayarları içerir. |
| [6. Adım: Birim oluşturun](#step-6-create-a-volume) |Sunucularınız için StorSimple cihazı hello depolama birimleri sağlayın. |
| [7. Adım: Bir birimi bağlayın, başlatın ve biçimlendirin](#step-7-mount-initialize-and-format-a-volume) </br>İsteğe bağlı: MPIO’yu yapılandırın. |Merhaba aygıt tarafından sağlanan, sunucuları toohello iSCSI depolama birimini bağlayın. İsteğe bağlı olarak, sunucularınızın bağlantı, ağ ve arabirim hatalarından etkilenmemesini MPIO tooensure yapılandırın. |
| [8. Adım: Yedekleyin](#step-8-take-a-backup) |Verilerinizi, yedekleme İlkesi tooprotect ayarlayın |
|  | |
| **DİĞER YORDAMLAR** |Çözümünüzü dağıtırken toorefer toothese yordamları gerekebilir. |
| [Merhaba hizmet için yeni bir depolama hesabı yapılandırma](#configure-a-new-storage-account-for-the-service) | |
| [PuTTY tooconnect toohello cihaz seri konsoluna kullanın](#use-putty-to-connect-to-the-device-serial-console) | |
| [İçin tarama ve güncelleştirmeleri uygulama](#scan-for-and-apply-updates) | |
| [Merhaba bir Windows Server konağının IQN'ini alın](#get-the-iqn-of-a-windows-server-host) | |
| [El ile yedekleme oluşturun](#create-a-manual-backup) | |


## <a name="deployment-configuration-checklist"></a>Dağıtım yapılandırma denetim listesi
StorSimple Cihazınızı dağıtmadan önce Cihazınızda toocollect bilgi tooconfigure hello yazılım gerekir. Önceden bu bilgilerin bazıları hazırlama hello ortamınızdaki hello StorSimple cihazı dağıtma işlemi kolaylaştırmaya yardımcı olur. Karşıdan yükleyip Cihazınızı dağıtırken bu denetim listesi toonote hello yapılandırma ayrıntıları kullanın.

[StorSimple dağıtım yapılandırma denetim listesini indirme](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a>Dağıtım önkoşulları
Aşağıdaki bölümlerde hello StorSimple cihaz Yöneticisi hizmetiniz ve StorSimple cihazınız için hello yapılandırma önkoşulları açıklanmaktadır.

### <a name="for-hello-storsimple-device-manager-service"></a>Merhaba StorSimple cihaz Yöneticisi hizmeti
Başlamadan önce aşağıdakilerden emin olun:

* Erişim kimlik bilgilerine sahip bir Microsoft hesabınız var.
* Erişim kimlik bilgilerine sahip bir Microsoft Azure Storage hesabınız var.
* Microsoft Azure aboneliğiniz StorSimple cihaz Yöneticisi hizmeti hello için etkinleştirilir. Aboneliğinizi hello satın alınması [Kurumsal Anlaşma](https://azure.microsoft.com/pricing/enterprise-agreement/).
* PuTTY gibi erişim tooterminal öykünme yazılımı var.

### <a name="for-hello-device-in-hello-datacenter"></a>Merhaba veri merkezinde Hello cihaz için
Merhaba cihazı yapılandırmadan önce olduğundan emin olun:

* Cihazınız tam olarak açılmış, bir rafa monte edilmiş ve güç, ağ ve seri erişim için kablolar aşağıdaki şekilde tam olarak bağlanmış:
  
  * [8100 model cihazınızı kutusundan çıkarma, rafa takma ve kablolarını bağlama](storsimple-8100-hardware-installation.md)
  * [8600 model cihazınızı kutusundan çıkarma, rafa takma ve kablolarını bağlama](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Merhaba veri merkezinde Hello ağ için
Başlamadan önce aşağıdakilerden emin olun:

* Merhaba, datacenter güvenlik duvarı bağlantı noktaları iSCSI ve bulut trafiği için açık tooallow açıklandığı gibi olan [StorSimple cihazınız için ağ gereksinimleri](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>Adım adım dağıtım
Adım adım yönergeler toodeploy aşağıdaki hello StorSimple Cihazınızı hello veri merkezinde kullanın.

## <a name="step-1-create-a-new-service"></a>1. Adım: Yeni bir hizmet oluşturun
Bir StorSimple Cihaz Yöneticisi hizmeti birden çok StorSimple cihazını yönetebilir. Aşağıdaki adımları toocreate hello StorSimple Aygıt Yöneticisi hizmetinin yeni bir örneğini hello gerçekleştirin.

[!INCLUDE [storsimple-8000-create-new-service-gov](../../includes/storsimple-8000-create-new-service-gov.md)]

> [!IMPORTANT]
> Hizmetiniz ile Merhaba otomatik bir depolama hesabının oluşturulmasını etkinleştirmediyseniz toocreate ihtiyacınız olacak bir hizmeti başarıyla oluşturduktan sonra en az bir depolama hesabı. Bir birim kapsayıcısı oluşturduğunuzda, bu depolama hesabı kullanılacaktır.
> 
> * Otomatik olarak bir depolama hesabı oluşturmadıysanız, çok Git[hello hizmet için yeni bir depolama hesabı yapılandırma](#configure-a-new-storage-account-for-the-service) ayrıntılı yönergeler için.
> * Depolama hesabı hello otomatik oluşturma etkinleştirilirse, çok Git[2. adım: hello hizmet kayıt anahtarını Al](#step-2-get-the-service-registration-key).


## <a name="step-2-get-hello-service-registration-key"></a>2. adım: hello hizmet kayıt anahtarını alın
Merhaba StorSimple cihaz Yöneticisi hizmeti çalışır durumda sonra tooget hello hizmet kayıt anahtarı gerekir. Bu anahtar kullanılan tooregister ve StorSimple cihaz toohello hizmetine bağlanın.

Aşağıdaki adımları hello kamu portalında hello gerçekleştirin.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>3. adım: Yapılandırmak ve storsimple için Windows PowerShell üzerinden hello cihazı
Windows PowerShell içinde aşağıdaki yordamı hello açıklandığı gibi StorSimple toocomplete hello ilk kurulumu StorSimple cihazınız için kullanın. Bu adım toouse terminal öykünme yazılımı toocomplete gerekir. Daha fazla bilgi için bkz: [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-8000-configure-and-register-device-gov](../../includes/storsimple-8000-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a>4. Adım: Minimum cihaz kurulumunu tamamlayın
En düşük cihaz yapılandırması Hello StorSimple cihazınız için sizin için gereklidir:

* Cihazınız için kolay bir ad sağlayın.
* Merhaba aygıt saat dilimini ayarlayın.
* Tooboth hello denetleyicileri sabit IP adresleri atayın.

Hello Azure kamu portal toocomplete hello minimum cihaz kurulumunu adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-8000-complete-minimum-device-setup-u2](../../includes/storsimple-8000-complete-minimum-device-setup-u2.md)]

## <a name="step-5-create-a-volume-container"></a>5. Adım: Birim kapsayıcısı oluşturun
Bir birim kapsayıcısı, depolama hesabı, bant genişliği ve içerdiği tüm hello birimleri için şifreleme ayarları içerir. StorSimple Cihazınızda birimleri sağlamaya başlamadan önce toocreate birim kapsayıcısı gerekir.

Merhaba kamu portal toocreate birim kapsayıcısı adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-8000-create-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>6. Adım: Birim oluşturun
Birim kapsayıcısı oluşturduktan sonra sunucularınız için StorSimple cihazı hello depolama biriminde sağlayabilirsiniz. Hello kamu portal toocreate bir birimin içindeki adımları izleyerek hello gerçekleştirin.

> [!IMPORTANT]
> StorSimple cihaz Yöneticisi yalnızca ölçülü kaynak kullanan birimler oluşturabilir.  Ancak kısmen sağlanan birimler oluşturamazsınız.

[!INCLUDE [storsimple-8000-create-volume](../../includes/storsimple-8000-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>7. Adım: Bir birimi bağlayın, başlatın ve biçimlendirin
Windows Server ana bilgisayarında aşağıdaki adımları gerçekleştirin.

> [!IMPORTANT]
> * Merhaba, yüksek kullanılabilirlik StorSimple çözümünüzün için ana bilgisayar sunucuları (isteğe bağlı) önceki tooconfiguring iSCSI MPIO'yu yapılandırmanızı öneririz. Ana bilgisayar sunucuları üzerinde MPIO yapılandırması hello sunucuları bağlantı, ağ veya arabirim hatalarına dayanabileceğinden emin olmanızı sağlar.
> * MPIO ve iSCSI yükleme ve yapılandırma yönergeleri için Windows Server ana bilgisayarda, çok Git[StorSimple cihazınız için MPIO yapılandırma](storsimple-configure-mpio-windows-server.md). Bunlar ayrıca hello adımları toomount dahil, başlatmak ve StorSimple birimleri biçimlendirme.
> * MPIO ve iSCSI yükleme ve yapılandırma yönergeleri için bir Linux ana bilgisayar üzerindeki, çok Git[StorSimple Linux konağınız için MPIO yapılandırma](storsimple-configure-mpio-on-linux.md)

Aşağıdaki adımları toomount hello tooconfigure MPIO, karar gerçekleştirirseniz, başlatmak ve Windows Server konağında StorSimple birimlerinizi biçimlendirin.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>8. Adım: Yedekleyin
Yedeklemeler, birimlerin zaman noktası korumasını sağlar ve geri yükleme sürelerini azaltırken kurtarılabilirliği iyileştirir. StorSimple cihazınızda iki tür yedekleme oluşturabilirsiniz: yerel anlık görüntüler ve bulut anlık görüntüleri. Bu yedekleme türlerinin her biri **Zamanlanmış** veya **El ile** olabilir.

Merhaba kamu portal toocreate zamanlanmış yedekleme adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-8000-take-backup](../../includes/storsimple-8000-take-backup.md)]

İstediğiniz zaman el ile yedekleme oluşturabilirsiniz. Yordamlar için çok Git[el ile yedekleme oluşturmak](#create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Merhaba hizmet için yeni bir depolama hesabı yapılandırma
Bu, yalnızca, bir depolama hesabının otomatik oluşturulmasını hello hizmetiniz ile etkinleştirmediyseniz tooperform gereken isteğe bağlı bir adımdır. Bir Microsoft Azure depolama hesabı gerekli toocreate StorSimple birim kapsayıcısı olabilir.

Azure storage hesabı farklı bir bölgede toocreate gerekirse bkz [Azure Storage hesapları hakkında](../storage/common/storage-create-storage-account.md) adım adım yönergeler için.

Aşağıdaki adımları hello kamu portalında, hello hello gerçekleştirmek **StorSimple cihaz Yöneticisi hizmeti** sayfası.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>PuTTY tooconnect toohello cihaz seri konsoluna kullanın
tooconnect tooWindows StorSimple için PowerShell, PuTTY gibi toouse terminal öykünme yazılımı gerekir. Merhaba aygıt hello seri Konsolu aracılığıyla doğrudan veya uzak bir bilgisayardan telnet oturumu açarak eriştiğinizde PuTTY kullanabilirsiniz.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Güncelleştirmeleri tarama ve güncelleştirmeleri uygulama
Cihazınızın güncelleştirilmesi birkaç saat sürebilir. Nasıl tooinstall hello en son güncelleştirme ilişkin ayrıntılı adımlar için gidin çok[güncelleştirme 4 yüklemek](storsimple-8000-install-update-4.md).

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Merhaba bir Windows Server konağının IQN'ini alın
Aşağıdaki adımları tooget hello iSCSI hello gerçekleştirmek tam adını (IQN) Windows Server® 2012 çalıştıran bir Windows konağının.

[!INCLUDE [Get IQN of your Windows Server host](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>El ile yedekleme oluşturun
StorSimple Cihazınızda hello kamu portal toocreate tek bir birim için bir isteğe bağlı el ile yedekleme adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [Create a manual backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>Sonraki adımlar
* [Sanal cihaz](storsimple-8000-cloud-appliance-u2.md) yapılandırın.
* Kullanım hello [StorSimple cihaz Yöneticisi hizmeti](storsimple-8000-manager-service-administration.md) toomanage StorSimple Cihazınızı.

