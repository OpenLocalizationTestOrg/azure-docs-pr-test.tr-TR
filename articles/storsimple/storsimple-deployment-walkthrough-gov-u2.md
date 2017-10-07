---
title: "Kamu portalında aaaDeploy StorSimple cihazı | Microsoft Docs"
description: "Merhaba adımları ve dağıtma hello StorSimple güncelleştirme 2 cihazını ve hizmetini hello Azure kamu portalında için en iyi uygulamaları açıklar."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 5277538c-797e-4e8e-b613-31b5c10cf5a9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/16/2016
ms.author: v-sharos
ms.openlocfilehash: 68104988595341a49a87d78c4a9b1d2675759c27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-in-hello-government-portal-update-2"></a>Merhaba kamu Portal (güncelleştirme 2) kullanarak şirket içi StorSimple Cihazınızı dağıtma
[!INCLUDE [storsimple-version-selector-deploy-gov](../../includes/storsimple-version-selector-deploy-gov.md)]

## <a name="overview"></a>Genel Bakış
TooMicrosoft Azure StorSimple cihaz dağıtımına Hoş Geldiniz. Bu dağıtım öğreticileri toohello StorSimple 8000 serisi güncelleştirme 2 yazılımını çalıştıran hello Azure kamu Portal içinde geçerlidir. Bu dizi öğreticiler bir yapılandırma denetim listesi, yapılandırma önkoşulları ve StorSimple cihazınız için ayrıntılı yapılandırma adımlarını listesini içerir.

Bu öğreticilerdeki bilgiler Hello hello güvenlik önlemlerini gözden geçirdiğinizi ve açılmış, yerleştirdiğinizi ve StorSimple Cihazınızı kablolu olduğunu varsayar. Bu görevler tooperform hala gerekiyorsa, hello inceleyerek başlayın [güvenlik önlemlerini](storsimple-safety.md). Toounpack, rafa monte etme ve Cihazınızı kablo hello cihaza özel yönergeleri izleyin.

* [8100 model cihazınızı kutusundan çıkarma, rafa takma ve kablolarını bağlama](storsimple-8100-hardware-installation.md)
* [8600 model cihazınızı kutusundan çıkarma, rafa takma ve kablolarını bağlama](storsimple-8600-hardware-installation.md)

Kurulum ve yapılandırma yönetici ayrıcalıkları toocomplete hello işlemi gerekir. Başlamadan önce hello yapılandırma denetim listesini gözden geçirmenizi öneririz. Merhaba dağıtım ve yapılandırma işlemi biraz zaman toocomplete alabilir.

> [!NOTE]
> Merhaba Hello Microsoft Azure Web sitesinde yayınlanan StorSimple dağıtım bilgileri tooStorSimple 8000 serisi cihazlar yalnızca geçerlidir. Merhaba 7000 Serisi cihazlar hakkında tam bilgi için: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). 7000 Serisi dağıtım bilgileri için bkz: Merhaba [StorSimple sistemi Hızlı Başlangıç Kılavuzu](http://onlinehelp.storsimple.com/111_Appliance/).
> 
> 

## <a name="deployment-steps"></a>Dağıtım adımları
StorSimple Cihazınızı bu gerekli adımları tooconfigure gerçekleştirin ve tooyour StorSimple Yöneticisi hizmetine bağlanın. Ayrıca toohello adımlar gerekli, isteğe bağlı adım ve yordamları hello dağıtımı sırasında toocomplete gerekebilir vardır. Bu isteğe bağlı adımların her biri gerçekleştirmesi gereken zaman hello adım adım dağıtım yönergeleri gösterir.

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
| [MPIO yapılandırma](#configure-mpio) | |

## <a name="deployment-configuration-checklist"></a>Dağıtım yapılandırma denetim listesi
StorSimple Cihazınızı dağıtmadan önce Cihazınızda toocollect bilgi tooconfigure hello yazılım gerekir. Önceden bu bilgilerin bazıları hazırlama hello ortamınızdaki hello StorSimple cihazı dağıtma işlemi kolaylaştırmaya yardımcı olur. Karşıdan yükleyip Cihazınızı dağıtırken bu denetim listesi toonote hello yapılandırma ayrıntıları kullanın.  

[StorSimple dağıtım yapılandırma denetim listesini indirme](http://www.microsoft.com/download/details.aspx?id=49159)  

## <a name="deployment-prerequisites"></a>Dağıtım önkoşulları
Merhaba aşağıdaki bölümlerde, StorSimple Yöneticisi hizmetiniz ve StorSimple cihazınız için hello yapılandırma önkoşulları açıklanmaktadır.

### <a name="for-hello-storsimple-manager-service"></a>Merhaba StorSimple Yöneticisi hizmeti
Başlamadan önce aşağıdakilerden emin olun:

* Erişim kimlik bilgilerine sahip bir Microsoft hesabınız var.
* Erişim kimlik bilgilerine sahip bir Microsoft Azure Storage hesabınız var.
* Microsoft Azure aboneliğiniz StorSimple Yöneticisi hizmeti hello için etkinleştirilir. Aboneliğinizi hello satın alınması [Kurumsal Anlaşma](https://azure.microsoft.com/pricing/enterprise-agreement/).
* PuTTY gibi erişim tooterminal öykünme yazılımı var.

### <a name="for-hello-device-in-hello-datacenter"></a>Merhaba veri merkezinde Hello cihaz için
Merhaba cihazı yapılandırmadan önce olduğundan emin olun:

* Cihazınız tam olarak açılmış, bir rafa monte edilmiş ve güç, ağ ve seri erişim için kablolar aşağıdaki şekilde tam olarak bağlanmış:
  
  * [8100 model cihazınızı kutusundan çıkarma, rafa takma ve kablolarını bağlama](storsimple-8100-hardware-installation.md)
  * [8600 model cihazınızı kutusundan çıkarma, rafa takma ve kablolarını bağlama](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Merhaba veri merkezinde Hello ağ için
Başlamadan önce aşağıdakilerden emin olun:

* Merhaba, datacenter güvenlik duvarı bağlantı noktaları iSCSI ve bulut trafiği için açık tooallow açıklandığı gibi olan [StorSimple cihazınız için ağ gereksinimleri](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>Adım adım dağıtım
Adım adım yönergeler toodeploy aşağıdaki hello StorSimple Cihazınızı hello veri merkezinde kullanın.

## <a name="step-1-create-a-new-service"></a>1. Adım: Yeni bir hizmet oluşturun
Bir StorSimple Yöneticisi hizmeti birden çok StorSimple cihazını yönetebilir. Aşağıdaki adımları toocreate hello StorSimple Yöneticisi hizmetini yeni bir örneğini hello gerçekleştirin.

[!INCLUDE [storsimple-create-new-service-gov](../../includes/storsimple-create-new-service-gov.md)]

> [!IMPORTANT]
> Hizmetiniz ile Merhaba otomatik bir depolama hesabının oluşturulmasını etkinleştirmediyseniz toocreate ihtiyacınız olacak bir hizmeti başarıyla oluşturduktan sonra en az bir depolama hesabı. Bir birim kapsayıcısı oluşturduğunuzda, bu depolama hesabı kullanılacaktır.
> 
> * Otomatik olarak bir depolama hesabı oluşturmadıysanız, çok Git[hello hizmet için yeni bir depolama hesabı yapılandırma](#configure-a-new-storage-account-for-the-service) ayrıntılı yönergeler için.
> * Depolama hesabı hello otomatik oluşturma etkinleştirilirse, çok Git[2. adım: hello hizmet kayıt anahtarını Al](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>2. adım: hello hizmet kayıt anahtarını alın
Merhaba StorSimple Yöneticisi hizmeti çalışır durumda sonra tooget hello hizmet kayıt anahtarı gerekir. Bu anahtar kullanılan tooregister ve StorSimple cihaz toohello hizmetine bağlanın.

Merhaba kamu Portal adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-get-service-registration-key-gov](../../includes/storsimple-get-service-registration-key-gov.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>3. adım: Yapılandırmak ve storsimple için Windows PowerShell üzerinden hello cihazı
Windows PowerShell içinde aşağıdaki yordamı hello açıklandığı gibi StorSimple toocomplete hello ilk kurulumu StorSimple cihazınız için kullanın. Bu adım toouse terminal öykünme yazılımı toocomplete gerekir. Daha fazla bilgi için bkz: [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device-gov](../../includes/storsimple-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a>4. Adım: Minimum cihaz kurulumunu tamamlayın
En düşük cihaz yapılandırması Hello StorSimple cihazınız için sizin için gereklidir:

* Merhaba ikincil DNS sunucusunu ayarlayın.
* En az bir ağ arabiriminde iSCSI’ı etkinleştirin.
* Tooboth hello denetleyicileri sabit IP adresleri atayın.

Merhaba kamu Portal toocomplete hello en düşük cihaz Kurulumu adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>5. Adım: Birim kapsayıcısı oluşturun
Bir birim kapsayıcısı, depolama hesabı, bant genişliği ve içerdiği tüm hello birimleri için şifreleme ayarları içerir. StorSimple Cihazınızda birimleri sağlamaya başlamadan önce toocreate birim kapsayıcısı gerekir.

Merhaba kamu Portal toocreate birim kapsayıcısı adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>6. Adım: Birim oluşturun
Birim kapsayıcısı oluşturduktan sonra sunucularınız için StorSimple cihazı hello depolama biriminde sağlayabilirsiniz. Hello kamu Portal toocreate bir birimin içindeki adımları izleyerek hello gerçekleştirin.

> [!IMPORTANT]
> Azure StorSimple yalnızca ölçülü kaynak kullanan birimler oluşturabilir.  Tamamen sağlanan veya kısmen sağlanan oluşturulamıyor bir Azure StorSimple sistemi birimlerde.
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>7. Adım: Bir birimi bağlayın, başlatın ve biçimlendirin
Windows Server ana bilgisayarında aşağıdaki adımları gerçekleştirin.

> [!IMPORTANT]
> * Merhaba, yüksek kullanılabilirlik StorSimple çözümünüzün için ana bilgisayar sunucuları (isteğe bağlı) önceki tooconfiguring iSCSI MPIO'yu yapılandırmanızı öneririz. Ana bilgisayar sunucuları üzerinde MPIO yapılandırması hello sunucuları bağlantı, ağ veya arabirim hatalarına dayanabileceğinden emin olmanızı sağlar.
> * MPIO ve iSCSI yükleme ve yapılandırma yönergeleri için Windows Server ana bilgisayarda, çok Git[StorSimple cihazınız için MPIO yapılandırma](storsimple-configure-mpio-windows-server.md). Bunlar ayrıca hello adımları toomount dahil, başlatmak ve StorSimple birimleri biçimlendirme.
> * MPIO ve iSCSI yükleme ve yapılandırma yönergeleri için bir Linux ana bilgisayar üzerindeki, çok Git[StorSimple Linux konağınız için MPIO yapılandırma](storsimple-configure-mpio-on-linux.md)
> 
> 

Aşağıdaki adımları toomount hello tooconfigure MPIO, karar gerçekleştirirseniz, başlatmak ve Windows Server konağında StorSimple birimlerinizi biçimlendirin.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>8. Adım: Yedekleyin
Yedeklemeler, birimlerin zaman noktası korumasını sağlar ve geri yükleme sürelerini azaltırken kurtarılabilirliği iyileştirir. StorSimple cihazınızda iki tür yedekleme oluşturabilirsiniz: yerel anlık görüntüler ve bulut anlık görüntüleri. Bu yedekleme türlerinin her biri **Zamanlanmış** veya **El ile** olabilir.

Merhaba kamu Portal toocreate zamanlanmış yedekleme adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

İstediğiniz zaman el ile yedekleme oluşturabilirsiniz. Yordamlar için çok Git[el ile yedekleme oluşturmak](#create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Merhaba hizmet için yeni bir depolama hesabı yapılandırma
Bu, yalnızca, bir depolama hesabının otomatik oluşturulmasını hello hizmetiniz ile etkinleştirmediyseniz tooperform gereken isteğe bağlı bir adımdır. Bir Microsoft Azure depolama hesabı gerekli toocreate StorSimple birim kapsayıcısı olabilir.

Azure storage hesabı farklı bir bölgede toocreate gerekirse bkz [Azure Storage hesapları hakkında](../storage/common/storage-create-storage-account.md) adım adım yönergeler için.

Merhaba kamu Portal hello üzerinde adımlarını izleyerek hello gerçekleştirmek **StorSimple Yöneticisi hizmeti** sayfası.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>PuTTY tooconnect toohello cihaz seri konsoluna kullanın
tooconnect tooWindows StorSimple için PowerShell, PuTTY gibi toouse terminal öykünme yazılımı gerekir. Merhaba aygıt hello seri Konsolu aracılığıyla doğrudan veya uzak bir bilgisayardan telnet oturumu açarak eriştiğinizde PuTTY kullanabilirsiniz.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Güncelleştirmeleri tarama ve güncelleştirmeleri uygulama
Cihazınızın güncelleştirilmesi birkaç saat sürebilir. Adımları tooscan için aşağıdaki hello gerçekleştirmek ve Cihazınızda güncelleştirmeleri uygulayın.

<!--If you have a gateway configured on a network interface other than Data 0, you will need toodisable Data 2 and Data 3 network interfaces before installing hello update. Go too**Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after hello device is updated.-->

#### <a name="tooupdate-your-device"></a>tooupdate Cihazınızı
1. Merhaba aygıtta **Hızlı Başlangıç** sayfasında, **aygıtları**. Merhaba fiziksel cihazı seçin, **Bakım** ve ardından **Güncelleştirmeleri tara**.  
2. Bir iş tooscan kullanılabilir güncelleştirmeler için oluşturulur. Güncelleştirmeler varsa, hello **Güncelleştirmeleri tara** çok değiştirir**Güncelleştirmeleri Yükle**. **Güncelleştirmeleri Yükle**’ye tıklayın.
3. Bir güncelleştirme işi oluşturulur. Çok giderek hello güncelleştirme durumunu izlemek**işleri**.
   
   > [!NOTE]
   > Merhaba güncelleştirme işi başladığında, yüzde 50 olarak hemen hello durumunu görüntüler. yalnızca hello güncelleştirme işi tamamlandıktan sonra too100 yüzde hello durumu değişir. Merhaba güncelleştirme işlemi için gerçek zamanlı durum yok.
   > 
   > 
4. Merhaba cihaz başarıyla güncelleştirildikten sonra bu devre dışı bırakılmışsa veri 2 ve veri 3 ağ arabirimlerini etkinleştirin.

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Merhaba bir Windows Server konağının IQN'ini alın
Aşağıdaki adımları tooget hello iSCSI hello gerçekleştirmek tam adını (IQN) Windows Server® 2012 çalıştıran bir Windows konağının.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>El ile yedekleme oluşturun
StorSimple Cihazınızda tek bir birim için hello kamu Portal toocreate isteğe bağlı el ile yedekleme adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup-gov.md)]

## <a name="configure-mpio"></a>MPIO yapılandırma
Çok yollu G/Ç (MPIO) isteğe bağlı bir özelliktir ve Windows Server'da varsayılan olarak yüklenmez. Sunucu Yöneticisi aracılığıyla bir özellik olarak yüklenmesi gerekir. MPIO yükleme yönergeleri için çok Git[StorSimple cihazınız için MPIO yapılandırma](storsimple-configure-mpio-windows-server.md).

MPIO yükleme yönergeleri için StorSimple cihazı bağlı tooa Linux ana gidin çok[Linux konağınız için MPIO yapılandırma](storsimple-configure-mpio-on-linux.md).

> [!NOTE]
> MPIO, StorSimple sanal cihazı Azure üzerinde desteklenmiyor.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* [Sanal cihaz](storsimple-virtual-device-u2.md) yapılandırın.
* Kullanım hello [StorSimple Yöneticisi hizmeti](storsimple-manager-service-administration.md) toomanage StorSimple Cihazınızı.

