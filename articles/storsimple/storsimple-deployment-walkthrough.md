---
title: "bir şirket içi StorSimple Cihazınızı aaaDeploy | Microsoft Docs"
description: "Merhaba adımları ve dağıtma hello StorSimple cihazını ve hizmetini için en iyi uygulamaları açıklar. (TooMicrosoft Azure StorSimple sürüm.3 uygular ve daha önceki.)"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b27f87a2-1363-4e0d-90f7-37b5dd1f21c9
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d45abba1786ceae586a99ca77b90de3f290c2f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device"></a>Şirket içi StorSimple cihazınızı dağıtma
> [!div class="op_single_selector"]
> * [Güncelleştirme 2](storsimple-deployment-walkthrough-u2.md)
> * [Güncelleştirme 1](storsimple-deployment-walkthrough-u1.md)
> * [GA Sürümü](storsimple-deployment-walkthrough.md)
> 
> 

## <a name="overview"></a>Genel Bakış
TooMicrosoft Azure StorSimple cihaz dağıtımına Hoş Geldiniz. Bu dağıtım öğreticileri geçerlidir tooStorSimple 8000 serisi yayınlanan sürüm, StorSimple 8000 serisi güncelleştirme 0.1, StorSimple 8000 serisi güncelleştirme 0.2 ve StorSimple 8000 serisi güncelleştirme 0.3. Bu öğreticiler dizi açıklar nasıl tooconfigure StorSimple cihazınız ve yapılandırma denetim listesi, yapılandırma önkoşulları ve ayrıntılı yapılandırma içerir adımları.

Bu öğreticilerdeki bilgiler Hello hello güvenlik önlemlerini gözden geçirdiğinizi ve açılmış, yerleştirdiğinizi ve StorSimple Cihazınızı kablolu olduğunu varsayar. Bu görevler tooperform hala gerekiyorsa, hello inceleyerek başlayın [güvenlik önlemlerini](storsimple-safety.md). Aygıt modeline bağlı olarak, kutusundan çıkarabilir, rafa monte ve hello yönergeleri izleyerek kablo:

* [8100 model cihazınızı kutusundan çıkarma, rafa takma ve kablolarını bağlama](storsimple-8100-hardware-installation.md)
* [8600 model cihazınızı kutusundan çıkarma, rafa takma ve kablolarını bağlama](storsimple-8600-hardware-installation.md)

Kurulum ve yapılandırma yönetici ayrıcalıkları toocomplete hello işlemi gerekir. Başlamadan önce hello yapılandırma denetim listesini gözden geçirmenizi öneririz. Merhaba dağıtım ve yapılandırma işlemi biraz zaman toocomplete alabilir.

> [!NOTE]
> Merhaba Hello Microsoft Azure Web sitesinde yayınlanan StorSimple dağıtım bilgileri tooStorSimple 8000 serisi cihazlar yalnızca geçerlidir. Merhaba 5000 ve 7000 Serisi cihazlar hakkında tam bilgi için: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). 5000 ve 7000 Serisi dağıtım bilgileri için bkz: Merhaba [StorSimple sistemi Hızlı Başlangıç Kılavuzu](http://onlinehelp.storsimple.com/111_Appliance/).
> 
> 

## <a name="deployment-steps"></a>Dağıtım adımları
StorSimple Cihazınızı bu gerekli adımları tooconfigure gerçekleştirin ve tooyour StorSimple Yöneticisi hizmetine bağlanın. Ayrıca toohello adımlar gerekli, isteğe bağlı adım ve yordamları hello dağıtım sırasında ihtiyacınız olabilecek vardır. Bu isteğe bağlı adımların her biri gerçekleştirmesi gereken zaman hello adım adım dağıtım yönergeleri gösterir.

| Adım | Açıklama |
| --- | --- |
| **ÖNKOŞULLAR** |Bunlar hello yaklaşan dağıtıma tamamlandı toobe gerekir. |
| Dağıtım yapılandırma denetim listesi. |Bu denetim listesi toogather ve kayıt bilgileri önceki tooand hello dağıtımı sırasında kullanın. |
| Dağıtım önkoşulları. |Bunlar hello doğrulamak için dağıtım ortamı hazır. |
|  | |
| **ADIM ADIM DAĞITIM** |Bu adımlar StorSimple Cihazınızı üretimde gerekli toodeploy şunlardır. |
| 1. Adım: Yeni bir hizmet oluşturun. |StorSimple cihazınız için bulut yönetimi ve depolamayı ayarlayın. Başka StorSimple cihazlar için bir hizmetiniz varsa, bu adımı atlayın. |
| 2. adım: hello hizmet kayıt anahtarını alın. |StorSimple Cihazınızı hello yönetim hizmetine bağlamak & Bu anahtar tooregister kullanın. |
| 3. adım: Yapılandırmak ve storsimple için Windows PowerShell üzerinden hello cihazı. |Merhaba aygıt tooyour ağa bağlanma ve Azure toocomplete hello Kurulum hello Yönetim hizmetini kullanarak kaydedin. |
| 4. Adım: Minimum cihaz kurulumunu tamamlayın</br>İsteğe bağlı: StorSimple cihazınızı güncelleştirin. |Merhaba management hizmeti toocomplete hello cihaz Kurulumu kullanın ve tooprovide depolama etkinleştirin. |
| 5. Adım: Birim kapsayıcısı oluşturun. |Bir kapsayıcı tooprovision birim oluşturun. Bir birim kapsayıcısı, depolama hesabı, bant genişliği ve içerdiği tüm hello birimleri için şifreleme ayarları içerir. |
| 6. Adım: Birim oluşturun. |Sunucularınız için StorSimple cihazı hello depolama birimleri sağlayın. |
| 7. Adım: Bir birimi bağlayın, başlatın ve biçimlendirin.</br>İsteğe bağlı: MPIO’yu yapılandırın. |Merhaba aygıt tarafından sağlanan, sunucuları toohello iSCSI depolama birimini bağlayın. İsteğe bağlı olarak, sunucularınızın bağlantı, ağ ve arabirim hatalarından etkilenmemesini MPIO tooensure yapılandırın. |
| 8. Adım: Yedekleyin. |Verilerinizi, yedekleme İlkesi tooprotect ayarlayın |
|  | |
| **DİĞER YORDAMLAR** |Çözümünüzü dağıtırken toorefer toothese yordamları gerekebilir. |
| Merhaba hizmet için yeni bir depolama hesabı yapılandırın. | |
| PuTTY tooconnect toohello cihaz seri konsoluna kullanın. | |
| Merhaba bir Windows Server konağının IQN'ini alın. | |
| El ile yedekleme oluşturun. | |

## <a name="deployment-configuration-checklist"></a>Dağıtım yapılandırma denetim listesi
Dağıtım yapılandırma denetim listesi aşağıdaki hello önce ve StorSimple Cihazınızda hello yazılım yapılandırırken toocollect gereksinim hello bilgileri açıklar. Önceden bu bilgilerin bazıları hazırlama hello ortamınızdaki hello StorSimple cihazı dağıtma işlemi kolaylaştırmaya yardımcı olur. Cihazınızı dağıtırken yapılandırma ayrıntılarını hello bu denetim listesi tooalso Not kullanın.

| Aşama | Parametre | Ayrıntılar | Değerler |
| --- | --- | --- | --- |
| **Cihazınızın kablolarını bağlama** |Seri erişim |İlk cihaz yapılandırması |Evet/Hayır |
|  | | | |
| **Cihazı yapılandırma ve kaydetme** |Veri 0 ağ ayarları |Veri 0 IP Adresi:</br>Alt ağ maskesi:</br>Ağ geçidi:</br>Birincil DNS sunucusu:</br>Birincil NTP sunucusu:</br>Web proxy sunucusu IP/FQDN (isteğe bağlı):</br>Web proxy bağlantı noktası: | |
| &nbsp; |Cihaz yöneticisi parolası |Parola 8 ile 15 karakter arasında olmalı ve küçük harfler, büyük harfler, sayısal ve özel karakterler içermelidir. | |
| &nbsp; |StorSimple Snapshot Manager parolası |Parola 14 veya 15 karakterden oluşmalı ve küçük harfler, büyük harfler, sayısal ve özel karakterler içermelidir. | |
| &nbsp; |Hizmet Kayıt Anahtarı |Bu anahtarı hello Klasik Azure Portalı ' oluşturulur. | |
| &nbsp; |Hizmeti Verileri Şifreleme Anahtarı |Merhaba cihaz hello Windows PowerShell aracılığıyla hello yönetim hizmetiyle StorSimple için kaydedildiğinde bu anahtarı oluşturulur. Bu anahtarı kopyalayın ve güvenli bir konuma kaydedin. | |
|  | | | |
| **Minimum cihaz kurulumunu tamamlama** |Cihazınızın kolay adı |Merhaba cihaz için açıklayıcı bir ad budur. | |
| &nbsp; |Saat dilimi |Cihazınız zamanlanan tüm işlemler için bu saat dilimini kullanır. | |
| &nbsp; |İkincil DNS sunucusu |Bu gerekli bir yapılandırmadır. | |
| &nbsp; |Ağ arabirimi: Veri 0 denetleyicisi sabit IP'leri |Bu IP'ler yönlendirilebilir toohello Internet olmalıdır.</br>Denetleyici 0 sabit IP adresi:</br>Denetleyici 1 sabit IP adresi: | |
|  | | | |
| **Ek ağ arabirimi ayarları** |Ağ arabirimi: Veri 1</br>İSCSI etkinse hello ağ geçidi yapılandırmayın. |Amaç: Bulut/iSCSI/Kullanılmıyor</br>IP adresi:</br>Alt ağ maskesi:</br>Ağ geçidi: | |
| &nbsp; |Ağ arabirimi: Veri 2</br>İSCSI etkinse hello ağ geçidi yapılandırmayın. |Amaç: Bulut/iSCSI/Kullanılmıyor</br>IP adresi:</br>Alt ağ maskesi:</br>Ağ geçidi: | |
| &nbsp; |Ağ arabirimi: Veri 3</br>İSCSI etkinse hello ağ geçidi yapılandırmayın. |Amaç: Bulut/iSCSI/Kullanılmıyor</br>IP adresi:</br>Alt ağ maskesi:</br>Ağ geçidi: | |
| &nbsp; |Ağ arabirimi: Veri 4</br>İSCSI etkinse hello ağ geçidi yapılandırmayın. |Amaç: Bulut/iSCSI/Kullanılmıyor</br>IP adresi:</br>Alt ağ maskesi:</br>Ağ geçidi: | |
| &nbsp; |Ağ arabirimi: Veri 5</br>İSCSI etkinse hello ağ geçidi yapılandırmayın. |Amaç: Bulut/iSCSI/Kullanılmıyor</br>IP adresi:</br>Alt ağ maskesi:</br>Ağ geçidi: | |
|  | | | |
| **Birim kapsayıcısı oluşturma** |Birim kapsayıcısı adı: |Merhaba kapsayıcı adı | |
| &nbsp; |Azure Storage hesabı: |Depolama hesabı adı ve erişim anahtarı tooassociate bu birim kapsayıcısı ile | |
| &nbsp; |Bulut depolama şifreleme anahtarı: |Her bir kapsayıcıdaki depolama için şifreleme anahtarı | |
|  | | | |
| **Birim oluşturma** |Her birim için ayrıntılar |Birim adı: | |
| &nbsp; |&nbsp; |Boyut: | |
| &nbsp; |&nbsp; |Kullanım türü: | |
| &nbsp; |&nbsp; |ACR adı: | |
| &nbsp; |&nbsp; |Varsayılan yedekleme ilkesi: | |
|  | | | |
| **Birim bağlama, başlatma ve biçimlendirme** |Toohello depolama bağlanan her konak sunucusu için Ayrıntılar |Windows Server adı: | |
| &nbsp; |&nbsp; |Windows Server IQN: | |
| &nbsp; |&nbsp; |Windows Server birim adı: | |
| &nbsp; |&nbsp; |NTFS bağlama noktası/Sürücü harfi: | |

## <a name="deployment-prerequisites"></a>Dağıtım önkoşulları
Merhaba aşağıdaki bölümlerde, StorSimple Yöneticisi hizmetiniz, StorSimple cihazı ve, veri merkezinizdeki hello ağınız için hello yapılandırma önkoşulları açıklanmaktadır.

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
* Merhaba aygıt, veri merkezinizdeki toooutside ağına bağlanabilir. Merhaba aşağıdaki komutu çalıştırarak [Windows PowerShell 4.0](http://www.microsoft.com/download/details.aspx?id=40855) cmdlet'lerini (aşağıdaki tabloda verilmiştir) toovalidate hello bağlantı toohello ağ dışında. Bu doğrulama bağlantısı tooAzure sahip bir bilgisayarda (veri merkezi ağındaki) gerçekleştirmek ve burada dağıtacağınız StorSimple Cihazınızı.  

| Bu parametre için... | toocheck hello geçerlilik... | Bu komutları/cmdlet'leri çalıştırın. |
| --- | --- | --- |
| **IP**</br>**Alt ağ**</br>**Ağ geçidi** |Bu geçerli bir IPv4 veya IPv6 adresi mi?</br>Bu geçerli bir alt ağ mı?</br>Bu geçerli bir ağ geçidi mi?</br>Bu ağ üzerinde yinelenen bir IP mi? |`ping ip`</br>`arp -a`</br>Merhaba `ping` ve `arp` komutları bu IP'yi kullanan hello veri merkezi ağında hiçbir aygıt olduğunu belirten başarısız olmalıdır. |
|  | | |
| **DNS** |Bu Azure URL’lerini çözebilen geçerli bir DNS mi? |`Resolve-DnsName -Name www.bing.com -Server <DNS server IP address>` </br>Kullanılabilir alternatif bir komut şöyledir:</br>`nslookup --dns-ip=<DNS server IP address> www.bing.com` |
| &nbsp; |Bağlantı noktası 53’ün açık olup olmadığını denetleyin. Bu, yalnızca cihazınız için bir dış DNS kullanıyorsanız geçerlidir. İç DNS otomatik olarak hello dış URL'ler çözümlenmelidir. |`Test-Port -comp dc1 -port 53 -udp -UDPtimeout 10000`  </br>[Bu cmdlet hakkında daha fazla bilgi](http://learn-powershell.net/2011/02/21/querying-udp-ports-with-powershell/) |
|  | | |
| **NTP** |NTP sunucusu girildikten hemen sonra bir saat eşitlemesi tetikleriz. `time.windows.com` veya ortak saat sunucuları girdiğinizde UDP bağlantı noktası 123’ün açık olup olmadığını denetleyin). |[Bu betiği indirin ve kullanın](https://gallery.technet.microsoft.com/scriptcenter/Get-Network-NTP-Time-with-07b216ca). |
|  | | |
| **Proxy (isteğe bağlı)** |Bu geçerli bir proxy URI’si ve bağlantı noktası mı? </br> Merhaba kimlik doğrulama modu doğru mu? |<code>wget http://bing.com &#124; % {$_.StatusCode}</code></br>Bu komut, web proxy’si yapılandırdıktan hemen sonra çalıştırılmalıdır. Bir durum kodu 200 döndürülürse, hello bağlantının başarılı olduğunu gösterir. |
| &nbsp; |Trafik proxy üzerinden yönlendirilebilir mi? |Hello DNS doğrulaması, NTP denetimi veya HTTP denetimini Cihazınızda proxy yapılandırdıktan sonra bir kez çalıştırın. Bu, trafiğin proxy veya başka bir engele takılıp takılmadığını gösterir. |
|  | | |
| **Kayıt** |Giden TCP bağlantı noktası 443, 80 ve 9354’ün açık olup olmadığını denetleyin. |`Test-NetConnection -Port   443 -InformationLevel Detailed`</br>[Test-NetConnection cmdlet’i hakkında daha fazla bilgi](https://technet.microsoft.com/library/dn372891.aspx) |

## <a name="step-by-step-deployment"></a>Adım adım dağıtım
Adım adım yönergeler toodeploy aşağıdaki hello StorSimple Cihazınızı hello veri merkezinde kullanın.

## <a name="step-1-create-a-new-service"></a>1. Adım: Yeni bir hizmet oluşturun
Bir StorSimple Yöneticisi hizmeti birden çok StorSimple cihazını yönetebilir. İlk StorSimple Cihazınızı Hello dağıtımı için yeni bir StorSimple Yöneticisi hizmeti toocreate gerekir.

> [!IMPORTANT]
> Bir StorSimple Yöneticisi hizmetiniz varsa ve StorSimple Cihazınızı bu hizmetle toodeploy düşündüğünüz bu adımı atlayın.
> 
> 

Aşağıdaki adımları toocreate hello StorSimple Yöneticisi hizmetini yeni bir örneğini hello gerçekleştirin.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

> [!IMPORTANT]
> Hizmetiniz ile Merhaba otomatik bir depolama hesabının oluşturulmasını etkinleştirmediyseniz toocreate ihtiyacınız olacak bir hizmeti başarıyla oluşturduktan sonra en az bir depolama hesabı. Bir birim kapsayıcısı oluşturduğunuzda, bu depolama hesabı kullanılacaktır.
> 
> Otomatik olarak bir depolama hesabı oluşturmadıysanız, çok Git[hello hizmet için yeni bir depolama hesabı yapılandırma](#configure-a-new-storage-account-for-the-service) ayrıntılı yönergeler için.
> Depolama hesabı hello otomatik oluşturma etkinleştirilirse, çok Git[2. adım: hello hizmet kayıt anahtarını Al](#step-2:-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>2. adım: hello hizmet kayıt anahtarını alın
Merhaba StorSimple Yöneticisi hizmeti çalışır durumda sonra tooget hello hizmet kayıt anahtarı gerekir. Bu anahtar kullanılan tooregister ve StorSimple Cihazınızı hello hizmetiyle bağlama.

Merhaba Klasik Azure Portalı'ndaki adımları izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>3. adım: Yapılandırmak ve storsimple için Windows PowerShell üzerinden hello cihazı
> [!IMPORTANT]
> Önceki tooperforming bu yapılandırma, hello ağ arabirimlerinde veri 0 dışında hem (etkin ve Pasif) hello denetleyicileri çıkarın.
> 
> 

Windows PowerShell içinde aşağıdaki yordamı hello açıklandığı gibi StorSimple toocomplete hello ilk kurulumu StorSimple cihazınız için kullanın. Bu adım toouse terminal öykünme yazılımı toocomplete gerekir. Daha fazla bilgi için bkz: [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device](../../includes/storsimple-configure-and-register-device.md)]

## <a name="step-4-complete-minimum-device-setup"></a>4. Adım: Minimum cihaz kurulumunu tamamlayın
En düşük cihaz yapılandırması Hello StorSimple cihazınız için sizin için gereklidir:

* Merhaba ikincil DNS sunucusunu ayarlayın.
* En az bir ağ arabiriminde iSCSI’ı etkinleştirin.
* Tooboth hello denetleyicileri sabit IP adresleri atayın.

Hello Azure Klasik portalı toocomplete hello minimum cihaz kurulumunu adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup.md)]

Merhaba cihaz yapılandırması tamamlandıktan sonra güncelleştirmeleri taramak ve varsa, güncelleştirmeleri yükleyin. Merhaba güncelleştirmeleri birkaç saat toocomplete sürebilir. Merhaba yönergeleri izleyin [taramak ve güncelleştirmeleri uygulamak](#scan-for-and-apply-updates).

## <a name="step-5-create-a-volume-container"></a>5. Adım: Birim kapsayıcısı oluşturun
Bir birim kapsayıcısı, depolama hesabı, bant genişliği ve içerdiği tüm hello birimleri için şifreleme ayarları içerir. StorSimple Cihazınızda birimleri sağlamaya başlamadan önce toocreate birim kapsayıcısı gerekir.

Hello Azure Klasik portalı toocreate birim kapsayıcısı adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>6. Adım: Birim oluşturun
Birim kapsayıcısı oluşturduktan sonra sunucularınız için StorSimple cihazı hello depolama biriminde sağlayabilirsiniz. Hello Azure Klasik portalı toocreate bir birimin içindeki adımları izleyerek hello gerçekleştirin.

> [!IMPORTANT]
> StorSimple Yöneticisi yalnızca ölçülü kaynak kullanan birimler oluşturabilir.  Tamamen veya kısmen sağlanan birimler oluşturamazsınız.
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>7. Adım: Bir birimi bağlayın, başlatın ve biçimlendirin
> [!IMPORTANT]
> * Merhaba, yüksek kullanılabilirlik StorSimple çözümünüzün için Windows Server ana bilgisayarında, Windows Server ana bilgisayar (isteğe bağlı) önceki tooconfiguring iSCSI MPIO'yu yapılandırmanızı öneririz. Ana bilgisayar sunucuları üzerinde MPIO yapılandırması hello sunucuları bağlantı, ağ veya arabirim hatalarına dayanabileceğinden emin olmanızı sağlar.
> * MPIO ve iSCSI yükleme ve yapılandırma yönergeleri için çok Git[StorSimple cihazınız için MPIO yapılandırma](storsimple-configure-mpio-windows-server.md). Bunlar ayrıca hello adımları toomount dahil, başlatmak ve StorSimple birimleri biçimlendirme.
> 
> 

Aşağıdaki adımları toomount hello tooconfigure MPIO, karar gerçekleştirirseniz, başlatmak ve StorSimple birimlerinizi biçimlendirin.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>8. Adım: Yedekleyin
Yedeklemeler, birimlerin zaman noktası korumasını sağlar ve geri yükleme sürelerini azaltırken kurtarılabilirliği iyileştirir. StorSimple cihazınızda iki tür yedekleme oluşturabilirsiniz: yerel anlık görüntüler ve bulut anlık görüntüleri. Bu yedekleme türlerinin her biri **Zamanlanmış** veya **El ile** olabilir.

Hello Azure Klasik portalı toocreate zamanlanmış yedekleme adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

İstediğiniz zaman el ile yedekleme oluşturabilirsiniz. Yordamlar için çok Git[el ile yedekleme oluşturmak](#Create-a-manual-backup).

## <a name="configure-a-new-storage-account-for-hello-service"></a>Merhaba hizmet için yeni bir depolama hesabı yapılandırma
Bu, yalnızca, bir depolama hesabının otomatik oluşturulmasını hello hizmetiniz ile etkinleştirmediyseniz tooperform gereken isteğe bağlı bir adımdır. Bir Microsoft Azure depolama hesabı gerekli toocreate StorSimple birim kapsayıcısı olabilir.

Azure storage hesabı farklı bir bölgede toocreate gerekirse bkz [Azure Storage hesapları hakkında](../storage/common/storage-create-storage-account.md) adım adım yönergeler için.

Merhaba hello üzerinde Klasik Azure Portalı'ndaki adımları izleyerek hello gerçekleştirmek **StorSimple Yöneticisi hizmeti** sayfası.

[!INCLUDE [storsimple-configure-new-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>PuTTY tooconnect toohello cihaz seri konsoluna kullanın
tooconnect tooWindows StorSimple için PowerShell, PuTTY gibi toouse terminal öykünme yazılımı gerekir. Merhaba aygıt hello seri Konsolu aracılığıyla doğrudan veya uzak bir bilgisayardan telnet oturumu açarak eriştiğinizde PuTTY kullanabilirsiniz.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Güncelleştirmeleri tarama ve güncelleştirmeleri uygulama
Cihazınızın güncelleştirilmesi 1-4 saat sürebilir. Adımları tooscan için aşağıdaki hello gerçekleştirmek ve Cihazınızda güncelleştirmeleri uygulayın.

> [!NOTE]
> Veri 0 dışında bir ağ arabiriminde yapılandırılmış bir ağ geçidi varsa hello güncelleştirmeyi yüklemeden önce toodisable veri 2 ve veri 3 ağ arabirimlerini gerekir. Çok Git**cihazlar > Yapılandır** ve veri 2 ve veri 3 arabirimlerini devre dışı bırakın. Merhaba cihaz güncelleştirildikten sonra bu arabirimleri yeniden etkinleştirmeniz gerekir.
> 
> 

#### <a name="tooupdate-your-device"></a>tooupdate Cihazınızı
1. Merhaba aygıtta **Hızlı Başlangıç** sayfasında, **aygıtları**. Merhaba fiziksel cihazı seçin, **Bakım** ve ardından **Güncelleştirmeleri tara**.  
2. Bir iş tooscan kullanılabilir güncelleştirmeler için oluşturulur. Güncelleştirmeler varsa, hello **Güncelleştirmeleri tara** çok değiştirir**Güncelleştirmeleri Yükle**. **Güncelleştirmeleri Yükle**’ye tıklayın. İstenen toodisable veri 2 ve veri 3 önceki tooinstalling hello güncelleştirmeleri olabilir. Bu ağ arabirimlerini devre dışı bırakmanız gerekir veya hello güncelleştirmeler başarısız olabilir.
3. Bir güncelleştirme işi oluşturulur. Çok giderek hello güncelleştirme durumunu izlemek**işleri**.
   
   > [!NOTE]
   > Merhaba güncelleştirme işi başladığında, yüzde 50 olarak hemen hello durumunu görüntüler. yalnızca hello güncelleştirme işi tamamlandıktan sonra hello durum too100 yüzde sonra değişir. Gerçek zamanlı durum hello güncelleştirmeleri işlem için yok.
   > 
   > 
4. Merhaba cihaz başarıyla güncelleştirildikten sonra bu devre dışı bırakılmışsa veri 2 ve veri 3 ağ arabirimlerini etkinleştirin.

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Merhaba bir Windows Server konağının IQN'ini alın
Aşağıdaki adımları tooget hello iSCSI hello gerçekleştirmek tam adını (IQN) Windows Server 2012 çalıştıran bir Windows konağının.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>El ile yedekleme oluşturun
StorSimple Cihazınızda tek bir birim için hello Azure Klasik portalı toocreate isteğe bağlı el ile yedekleme adımlarını izleyerek hello gerçekleştirin.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="next-steps"></a>Sonraki adımlar
* [Sanal cihaz](storsimple-virtual-device-u2.md) yapılandırın.
* Kullanım hello [StorSimple Yöneticisi hizmeti](https://msdn.microsoft.com/library/azure/dn772396.aspx) toomanage StorSimple Cihazınızı.

