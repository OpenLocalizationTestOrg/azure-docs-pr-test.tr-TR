---
title: aaaMicrosoft Azure StorSimple sanal dizinin sistem gereksinimleri | Microsoft Docs
description: "StorSimple sanal dizinizi hello yazılım ve ağ gereksinimleri hakkında bilgi edinin"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: ea1d3bca-e71b-453d-aa82-440d2638f5e3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.openlocfilehash: 7a124873fdd806d409c7279851456e6347e7ec0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-system-requirements"></a>StorSimple Sanal Dizini sistem gereksinimleri
## <a name="overview"></a>Genel Bakış
Bu makalede hello önemli sistem gereksinimleri ve hello dizi erişme hello depolama istemcileri için Microsoft Azure StorSimple sanal dizinizi açıklanmaktadır. StorSimple sisteminizi dağıtma ve ardından geri tooit gerektiği gibi dağıtım ve sonraki işlemi sırasında başvurmak önce hello bilgileri dikkatle gözden geçirmenizi öneririz.

Merhaba sistem gereksinimleri şunlardır:

* **Depolama istemciler için yazılım gereksinimleri** -hello desteklenen sanallaştırma platformları, web tarayıcıları, iSCSI başlatıcıları, SMB istemcileri, minimum sanal cihaz gereksinimleri ve bu işletim sistemleri için tüm ek gereksinimleri açıklanmaktadır.
* **Merhaba StorSimple cihazı için ağ gereksinimleri** -iSCSI, Bulut veya yönetim trafiği için güvenlik duvarı tooallow açık bu gereksinimi toobe hello bağlantı noktaları hakkında bilgi sağlar.

Bu makalede yayımlanmış bilgiler hello StorSimple sistem gereksinimleri, yalnızca sanal diziler tooStorSimple geçerlidir.

* 8000 serisi cihazlar için çok Git[StorSimple 8000 serisi cihazınız için sistem gereksinimleri](storsimple-system-requirements.md).
* 7000 Serisi cihazlar için çok Git[StorSimple 5000-7000 Serisi cihazınız için sistem gereksinimleri](http://onlinehelp.storsimple.com/1_StorSimple_System_Requirements).

## <a name="software-requirements"></a>Yazılım gereksinimleri
Merhaba yazılım gereksinimleri hello hello desteklenen web tarayıcıları, SMB sürümleri, sanallaştırma platformları ve hello minimum sanal cihaz gereksinimleri hakkında bilgi içerir.

### <a name="supported-virtualization-platforms"></a>Desteklenen sanallaştırma platformları
| **Hiper yönetici** | **Sürüm** |
| --- | --- |
| Hyper-V |Windows Server 2008 R2 SP1 ve sonraki sürümler |
| VMware ESXi |5.5 ve sonraki sürümleri |

### <a name="virtual-device-requirements"></a>Sanal cihaz gereksinimleri
| **Bileşen** | **Gereksinim** |
| --- | --- |
| En az sayıda sanal işlemci (çekirdek) |4 |
| Minimum bellek (RAM) |8 GB <br> Bir dosya sunucusu, 8 GB 2 milyondan az dosyaları için ve 2-4 milyon dosyaları için 16 GB|
| Disk alanı<sup>1</sup> |İşletim sistemi diski - 80 GB <br></br>Veri diski - 500 GB too8 TB |
| Ağ arabirimi en az durum sayısı |1 |
| En düşük Internet bant genişliği<sup>2</sup> |5 MB/sn |

<sup>1</sup> - ince sağlanan

<sup>2</sup> -ağ gereksinimleri hello günlük veri değişim oranı bağlı olarak değişebilir. Bir cihazın bir günde 10 GB veya daha fazla değişiklik tooback gerekiyorsa (Merhaba veri sıkıştırılmış yinelenenleri kaldırılmış veya bulunamadı) Örneğin, ardından hello 5 MB/sn bağlantı üzerinden günlük yedekleme too4.25 saatleri ele geçirebilir.

### <a name="supported-web-browsers"></a>Desteklenen web tarayıcıları
| **Bileşen** | **Sürüm** | **Ek gereksinimler/Notlar** |
| --- | --- | --- |
| Microsoft Edge |En son sürümü | |
| Internet Explorer |En son sürümü |Internet Explorer 11 ile test |
| Google Chrome |En son sürümü |Chrome 46 ile test |

### <a name="supported-storage-clients"></a>Desteklenen depolama istemcileri
StorSimple sanal (iSCSI sunucusu olarak yapılandırılmış) dizinizi erişim hello iSCSI başlatıcıları yazılım gereksinimleri aşağıdaki hello içindir.

| **Desteklenen işletim sistemleri** | **Gerekli sürümü** | **Ek gereksinimler/Notlar** |
| --- | --- | --- |
| Windows Server |2008R2 SP1, 2012, 2012 R2 |Ölçülü kaynak kullanan ve tamamen sağlanan StorSimple oluşturabilir birimler. Kısmen sağlanan birimler oluşturamazsınız. StorSimple iSCSI birimleri için yalnızca desteklenir: <ul><li>Windows temel disklerdeki basit birimler.</li><li>Windows bir birimi biçimlendirmek için NTFS.</li> |

yazılım gereksinimleri aşağıdaki hello Merhaba, StorSimple sanal (dosya sunucusu olarak yapılandırılmış) dizi erişen SMB istemcileridir.

| **SMB sürümü** |
| --- |
| SMB 2.x |
| SMB 3.0 |
| SMB 3.02 |

> [!IMPORTANT]
> Kopyalamayın veya Windows şifreleme dosya sistemi (EFS) toohello StorSimple sanal dizinin dosya sunucusu tarafından korunan dosyaları depolamak; Bu, desteklenmeyen bir yapılandırmada neden olacaktır. 
> 

### <a name="supported-storage-format"></a>Desteklenen depolama biçimi
Yalnızca Azure blok blob depolama hello desteklenir. Sayfa bloblarını desteklenmez. Daha fazla bilgi [blok blobları ve sayfa BLOB'ları hakkında](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).

## <a name="networking-requirements"></a>Ağ gereksinimleri
Merhaba aşağıdaki tabloda, güvenlik duvarı tooallow iSCSI, SMB, Bulut veya yönetim trafiği için açılır toobe gereksinim hello bağlantı noktalarını listeler. Bu tabloda *içinde* veya *gelen* gelen istemci isteklerini erişim Cihazınızı toohello yönünü belirtir. *Out* veya *giden* toohello yönü, StorSimple Cihazınızı verileri gönderir harici olarak hello dağıtım başvuruyor: Örneğin, giden toohello Internet.

| **Bağlantı noktası No<sup>1</sup>** | **Giriş veya çıkış** | **Bağlantı noktası kapsamı** | **Gerekli** | **Notlar** |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP) |Çıkışı |WAN |Hayır |Giden bağlantı noktası, Internet erişimi tooretrieve güncelleştirmeler için kullanılır. <br></br>Merhaba giden web proxy yapılandırılabilir kullanıcıdır. |
| TCP 443 (HTTPS) |Çıkışı |WAN |Evet |Giden bağlantı noktası hello bulut veri erişimi için kullanılır. <br></br>Merhaba giden web proxy yapılandırılabilir kullanıcıdır. |
| UDP 53 (DNS) |Çıkışı |WAN |Bazı durumlarda; notlarına bakın. |Yalnızca bir Internet tabanlı DNS sunucusu kullanıyorsanız, bu bağlantı noktası gereklidir. <br></br> Bir dosya sunucusu dağıtma, yerel DNS sunucusu kullanmanızı öneririz olduğunu unutmayın. |
| UDP 123 (NTP) |Çıkışı |WAN |Bazı durumlarda; notlarına bakın. |Yalnızca bir Internet tabanlı NTP sunucusu kullanıyorsanız, bu bağlantı noktası gereklidir.<br></br> Bir dosya sunucusu dağıtma, Active Directory etki alanı denetleyicileriniz ile eşitleme süresi öneririz olduğunu unutmayın. |
| TCP 80 (HTTP) |İçinde |LAN |Evet |Bu olduğu hello gelen bağlantı noktası hello StorSimple cihazı yerel yönetim için yerel kullanıcı Arabirimi için. <br></br> Merhaba erişen HTTP üzerinden yerel kullanıcı Arabirimi otomatik olarak tooHTTPS yönlendirir olduğunu unutmayın. |
| TCP 443 (HTTPS) |İçinde |LAN |Evet |Bu olduğu hello gelen bağlantı noktası hello StorSimple cihazı yerel yönetim için yerel kullanıcı Arabirimi için. |
| TCP 3260 (iSCSI) |İçinde |LAN |Hayır |Bu bağlantı noktası kullanılan tooaccess üzerinde iSCSI verilerdir. |

<sup>1</sup> hiçbir gelen bağlantı noktalarının açılan toobe gereken genel Internet hello.

> [!IMPORTANT]
> Merhaba güvenlik duvarının değiştirmeyin veya tüm SSL trafiği hello StorSimple cihazı ve Azure arasında şifresini emin olun.
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>Güvenlik duvarı kuralları için URL düzenleri
Ağ yöneticileri genellikle hello URL desenlerini toofilter hello üzerinde dayalı kurallar gelen ve giden trafiği hello Gelişmiş Güvenlik Duvarı yapılandırabilirsiniz. Sanal dizinin ve hello StorSimple cihaz Yöneticisi hizmeti Azure Service Bus, Azure Active Directory erişim denetimi, depolama hesapları ve Microsoft Update sunucuları gibi diğer Microsoft uygulamaları bağlıdır. Bu uygulamalarla ilişkili hello URL desenlerini kullanılan tooconfigure güvenlik duvarı kuralları olabilir. Bu uygulamalarla ilişkili hello URL desenlerini değiştirebilirsiniz önemli toounderstand olur. Bu sırayla hello ağ yöneticisi toomonitor gerektirir ve güvenlik duvarı kuralları, StorSimple için ve gerektiğinde güncelleştirin. 

Çoğu durumda liberally sabit IP adresleri, StorSimple göre giden trafiği için güvenlik duvarı kuralları ayarlamanızı öneririz. Ancak, gerekli toocreate güvenli ortamları güvenlik duvarı kuralları Gelişmiş tooset aşağıda hello bilgileri kullanabilirsiniz.

> [!NOTE]
> 
> * Merhaba aygıt (kaynak) IP'leri her zaman tooall hello bulut etkin ağ arabirimleri ayarlamanız gerekir. 
> * IP çok ayarlanmalıdır hello hedef[Azure veri merkezi IP aralıkları](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).
> 
> 

| URL deseni | Bileşen/işlevi |
| --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |StorSimple cihaz Yöneticisi hizmeti<br>Access Control Service<br>Azure Service Bus |
| `http://*.backup.windowsazure.com` |Cihaz kaydı |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Sertifika iptali |
| `https://*.core.windows.net/*`<br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Azure depolama hesapları ve izleme |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Microsoft Update sunucularına<br> |
| `http://*.deploy.akamaitechnologies.com` |Akamai CDN |
| `https://*.partners.extranet.microsoft.com/*` |Destek Paketi |
| `http://*.data.microsoft.com ` |Windows, telemetri hizmetinde bkz hello [müşteri deneyimi ve tanılama telemetri güncelleştirmesi](https://support.microsoft.com/en-us/kb/3068708) |

## <a name="next-step"></a>Sonraki adım
* [StorSimple sanal dizinizi Hello portal toodeploy hazırlama](storsimple-virtual-array-deploy1-portal-prep.md)

