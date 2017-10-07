---
title: aaaStorSimple 8000 serisi sistem gereksinimleri | Microsoft Docs
description: "Yazılım, ağ ve yüksek oranda kullanılabilirlik gereksinimleri ve Microsoft Azure StorSimple çözümünüzle için en iyi uygulamaları açıklar."
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
ms.date: 07/10/2017
ms.author: alkohli
ms.openlocfilehash: f13ccdb7cb317d72c60e9c2fe49937764d10b43e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-software-high-availability-and-networking-requirements"></a>StorSimple 8000 serisi yazılım, yüksek kullanılabilirlik ve ağ gereksinimleri

## <a name="overview"></a>Genel Bakış

Azure StorSimple tooMicrosoft Hoş Geldiniz. Bu makalede önemli sistem gereksinimleri ve StorSimple cihazınız için ve hello depolama istemciler hello cihaza erişmek için en iyi uygulamaları açıklar. StorSimple sisteminizi dağıtma ve ardından geri tooit gerektiği gibi dağıtım ve sonraki işlemi sırasında başvurmak önce hello bilgileri dikkatle gözden geçirmenizi öneririz.

Merhaba sistem gereksinimleri şunlardır:

* **Depolama istemciler için yazılım gereksinimleri** -hello desteklenen işletim sistemleri ve bu işletim sistemleri için tüm ek gereksinimleri açıklanmaktadır.
* **Merhaba StorSimple cihazı için ağ gereksinimleri** -iSCSI, Bulut veya yönetim trafiği için güvenlik duvarı tooallow açık bu gereksinimi toobe hello bağlantı noktaları hakkında bilgi sağlar.
* **StorSimple için yüksek kullanılabilirlik gereksinimlerini** - yüksek kullanılabilirlik gereksinimlerini açıklar ve StorSimple cihaz ve ana bilgisayar için'en iyi uygulamalar.

## <a name="software-requirements-for-storage-clients"></a>Depolama istemciler için yazılım gereksinimleri

yazılım gereksinimleri aşağıdaki hello StorSimple Cihazınızı erişen hello depolama için istemcileridir.

| Desteklenen işletim sistemleri | Gerekli sürümü | Ek gereksinimler/Notlar |
| --- | --- | --- |
| Windows Server |2008 R2 SP1, 2012, 2012 R2'DE, 2016 |StorSimple iSCSI birimleri, yalnızca şu Windows disk türlerini hello üzerinde kullanım için desteklenir:<ul><li>Temel diskteki basit birim</li><li>Dinamik diskteki basit ve yansıtılmış birim</li></ul>Yalnızca hello yazılım iSCSI başlatıcıları yerel hello işletim sisteminde mevcut desteklenir. Donanım iSCSI başlatıcıları desteklenmez.<br></br>Bir StorSimple iSCSI birim kullanıyorsanız, Windows Server 2012 ve 2016 ölçülü kaynak sağlama ve ODX özellikler desteklenir.<br><br>Ölçülü kaynak kullanan ve tamamen sağlanan StorSimple oluşturabilir birimler. Kısmen sağlanan birimler oluşturamazsınız.<br><br>Ölçülü kaynak kullanan bir birim yeniden biçimlendirme uzun sürebilir. Merhaba toplu silme ve yeniden biçimlendirme yerine yeni bir tane oluşturma öneririz. Ancak, yine tooreformat bir birim tercih:<ul><li>Merhaba yeniden biçimlendirme tooavoid alan geri kazanma gecikmeler önce komutunu aşağıdaki hello çalıştırın: <br>`fsutil behavior set disabledeletenotify 1`</br></li><li>Merhaba biçimlendirme tamamlandıktan sonra kullanım hello aşağıdaki toore etkinleştir alan geri kazanma komutu:<br>`fsutil behavior set disabledeletenotify 0`</br></li><li>Bölümünde açıklandığı gibi Hello Windows Server 2012 düzeltmeyi [KB 2878635](https://support.microsoft.com/kb/2870270) tooyour Windows Server bilgisayarı.</li></ul></li></ul></ul> SharePoint için StorSimple Snapshot Manager veya StorSimple bağdaştırıcısı yapılandırıyorsanız, çok Git[isteğe bağlı bileşenler için yazılım gereksinimleri](#software-requirements-for-optional-components). |
| VMware ESX |5.5 ve 6.0 |VMware vSphere ile iSCSI istemcisi olarak desteklenir. VAAI engelleme özelliği, VMware vsphere StorSimple cihazlarda desteklenir. |
| Linux RHEL/CentOS |5, 6 ve 7 |Açık iSCSI başlatıcısı sürümlerini 5, 6 ve 7 Linux iSCSI istemciler için destek. |
| Linux |SUSE Linux 11 | |

> [!NOTE]
> IBM AIX StorSimple ile şu anda desteklenmiyor.


## <a name="software-requirements-for-optional-components"></a>İsteğe bağlı bileşenler için yazılım gereksinimleri

yazılım gereksinimleri aşağıdaki hello hello isteğe bağlı StorSimple bileşenleri (StorSimple Snapshot Manager ve SharePoint için StorSimple bağdaştırıcısı) içindir.

| Bileşen | Ana bilgisayar platformu | Ek gereksinimler/Notlar |
| --- | --- | --- |
| StorSimple Snapshot Manager |Windows Server 2008 R2 SP1, 2012, 2012 R2 |Kullanım StorSimple anlık görüntü Yöneticisi'nin Windows Server Yedekleme/geri yükleme yansıtılmış dinamik disklerin ve herhangi bir uygulamayla tutarlı yedeklemeler için gereklidir.<br> StorSimple Snapshot Manager yalnızca Windows Server 2008 R2 SP1 (64 bit), Windows Server 2012 R2 ve Windows Server 2012 desteklenir.<ul><li>Pencere Server 2012 kullanıyorsanız, StorSimple Snapshot Manager yüklemeden önce .NET 3.5 – 4.5 yüklemeniz gerekir.</li><li>Windows Server 2008 R2 SP1'i kullanıyorsanız, StorSimple Snapshot Manager yüklemeden önce Windows Management Framework 3.0 yüklemeniz gerekir.</li></ul> |
| SharePoint için StorSimple Bağdaştırıcısı |Windows Server 2008 R2 SP1, 2012, 2012 R2 |<ul><li>SharePoint için StorSimple bağdaştırıcısı yalnızca SharePoint 2010 ve SharePoint 2013 üzerinde desteklenir.</li><li>KKY SQL Server Enterprise Edition, sürüm 2008 R2 veya 2012 gerektirir.</li></ul> |

## <a name="networking-requirements-for-your-storsimple-device"></a>StorSimple cihazınız için ağ gereksinimleri

StorSimple Cihazınızı kilitli aygıttır. Ancak, bağlantı noktaları iSCSI, Bulut ve yönetim trafiği için güvenlik duvarı tooallow açılır toobe gerekir. Merhaba aşağıdaki tabloda, Güvenlik Duvarı'nda açılan toobe gereksinim hello bağlantı noktalarını listeler. Bu tabloda *içinde* veya *gelen* gelen istemci isteklerini erişim Cihazınızı toohello yönünü belirtir. *Out* veya *giden* toohello yönü, StorSimple Cihazınızı verileri gönderir harici olarak hello dağıtım başvuruyor: Örneğin, giden toohello Internet.

| Bağlantı noktası No<sup>1,2</sup> | Giriş veya çıkış | Bağlantı noktası kapsamı | Gerekli | Notlar |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP)<sup>3</sup> |Çıkışı |WAN |Hayır |<ul><li>Giden bağlantı noktası, Internet erişimi tooretrieve güncelleştirmeler için kullanılır.</li><li>Merhaba giden web proxy yapılandırılabilir kullanıcıdır.</li><li>tooallow sistem güncelleştirmeleri, bu bağlantı noktası da hello denetleyicisi sabit IP'leri açık olması gerekir.</li></ul> |
| TCP 443 (HTTPS)<sup>3</sup> |Çıkışı |WAN |Evet |<ul><li>Giden bağlantı noktası hello bulut veri erişimi için kullanılır.</li><li>Merhaba giden web proxy yapılandırılabilir kullanıcıdır.</li><li>tooallow sistem güncelleştirmeleri, bu bağlantı noktası da hello denetleyicisi sabit IP'leri açık olması gerekir.</li><li>Bu bağlantı noktası, atık toplama için her iki hello denetleyicilerinde de kullanılır.</li></ul> |
| UDP 53 (DNS) |Çıkışı |WAN |Bazı durumlarda; notlarına bakın. |Yalnızca bir Internet tabanlı DNS sunucusu kullanıyorsanız, bu bağlantı noktası gereklidir. |
| UDP 123 (NTP) |Çıkışı |WAN |Bazı durumlarda; notlarına bakın. |Yalnızca bir Internet tabanlı NTP sunucusu kullanıyorsanız, bu bağlantı noktası gereklidir. |
| TCP 9354 |Çıkışı |WAN |Evet |Merhaba giden bağlantı noktası hello StorSimple cihaz Yöneticisi hizmeti ile Merhaba StorSimple cihaz toocommunicate tarafından kullanılır. |
| 3260 (iSCSI) |İçinde |LAN |Hayır |Bu bağlantı noktası kullanılan tooaccess üzerinde iSCSI verilerdir. |
| 5985 |İçinde |LAN |Hayır |Gelen bağlantı noktası hello StorSimple cihazı ile StorSimple Snapshot Manager toocommunicate tarafından kullanılır.<br>Bu bağlantı noktası, uzaktan tooWindows PowerShell StorSimple için HTTP üzerinden bağlandıklarında da kullanılır. |
| 5986 |İçinde |LAN |Hayır |Uzaktan tooWindows PowerShell StorSimple için HTTPS üzerinden bağlandığınızda bu bağlantı noktası kullanılır. |

<sup>1</sup> hiçbir gelen bağlantı noktalarının açılan toobe gereken genel Internet hello.

<sup>2</sup> birden çok bağlantı noktası bir ağ geçidi yapılandırma planlaması yapıyorsanız hello giden yönlendirilen trafiği sipariş hello bağlantı noktası yönlendirme sipariş açıklanan göre belirlenir [bağlantı noktası yönlendirme](#routing-metric), aşağıdaki.

<sup>3</sup> StorSimple Cihazınızda IP'leri sabit hello denetleyicisi yönlendirilebilir olmalıdır ve mümkün tooconnect toohello Internet doğrudan veya hello üzerinden web proxy yapılandırılır. hello sabit IP adresleri hello güncelleştirmeleri toohello aygıt bakım için kullanılır. Merhaba aygıt denetleyicileri hello üzerinden Internet sabit IP'leri toohello bağlanamıyorsanız, mümkün tooupdate olmaz StorSimple Cihazınızı.

> [!IMPORTANT]
> Merhaba güvenlik duvarının değiştirmeyin veya tüm SSL trafiği hello StorSimple cihazı ve Azure arasında şifresini emin olun.


### <a name="url-patterns-for-firewall-rules"></a>Güvenlik duvarı kuralları için URL düzenleri

Ağ yöneticileri genellikle hello URL desenlerini toofilter hello üzerinde dayalı kurallar gelen ve giden trafiği hello Gelişmiş Güvenlik Duvarı yapılandırabilirsiniz. StorSimple cihazı ve hello StorSimple cihaz Yöneticisi hizmeti Azure Service Bus, Azure Active Directory erişim denetimi, depolama hesapları ve Microsoft Update sunucuları gibi diğer Microsoft uygulamaları bağlıdır. Bu uygulamalarla ilişkili hello URL desenlerini kullanılan tooconfigure güvenlik duvarı kuralları olabilir. Bu uygulamalarla ilişkili hello URL desenlerini değiştirebilirsiniz önemli toounderstand olur. Bu sırayla hello ağ yöneticisi toomonitor gerektirir ve güvenlik duvarı kuralları, StorSimple için ve gerektiğinde güncelleştirin.

Çoğu durumda liberally sabit IP adresleri, StorSimple göre giden trafiği için güvenlik duvarı kuralları ayarlamanızı öneririz. Ancak, gerekli toocreate güvenli ortamları güvenlik duvarı kuralları Gelişmiş tooset aşağıda hello bilgileri kullanabilirsiniz.

> [!NOTE]
> Merhaba aygıt (kaynak) IP'leri her zaman tooall etkin hello ağ arabirimleri ayarlamanız gerekir. IP çok ayarlanmalıdır hello hedef[Azure veri merkezi IP aralıkları](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).


#### <a name="url-patterns-for-azure-portal"></a>Azure portal için URL düzenleri

| URL deseni | Bileşen/işlevi | Cihaz IP'leri |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*`<br>`https://login.windows.net` |StorSimple cihaz Yöneticisi hizmeti<br>Access Control Service<br>Azure Service Bus<br>Kimlik doğrulama hizmeti |Bulut etkin ağ arabirimleri |
| `https://*.backup.windowsazure.com` |Cihaz kaydı |Yalnızca veri 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Sertifika iptali |Bulut etkin ağ arabirimleri |
| `https://*.core.windows.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Azure depolama hesapları ve izleme |Bulut etkin ağ arabirimleri |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Microsoft Update sunucularına<br> |IP'ler yalnızca sabit denetleyici |
| `http://*.deploy.akamaitechnologies.com` |Akamai CDN |IP'ler yalnızca sabit denetleyici |
| `https://*.partners.extranet.microsoft.com/*`<br>`https://dcupload.microsoft.com/`<br>`https://*.support.microsoft.com/` |Destek Paketi |Bulut etkin ağ arabirimleri |

#### <a name="url-patterns-for-azure-government-portal"></a>URL desenlerini Azure kamu portalı

| URL deseni | Bileşen/işlevi | Cihaz IP'leri |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.us/*`<br>`https://*.accesscontrol.usgovcloudapi.net/*`<br>`https://*.servicebus.usgovcloudapi.net/*`<br>`https://login-us.microsoftonline.com` |StorSimple cihaz Yöneticisi hizmeti<br>Access Control Service<br>Azure Service Bus<br>Kimlik doğrulama hizmeti |Bulut etkin ağ arabirimleri |
| `https://*.backup.windowsazure.us` |Cihaz kaydı |Yalnızca veri 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Sertifika iptali |Bulut etkin ağ arabirimleri |
| `https://*.core.usgovcloudapi.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Azure depolama hesapları ve izleme |Bulut etkin ağ arabirimleri |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Microsoft Update sunucularına<br> |IP'ler yalnızca sabit denetleyici |
| `http://*.deploy.akamaitechnologies.com` |Akamai CDN |IP'ler yalnızca sabit denetleyici |
| `https://*.partners.extranet.microsoft.com/*`<br>`https://dcupload.microsoft.com/`<br>`https://*.support.microsoft.com/` |Destek Paketi |Bulut etkin ağ arabirimleri |

### <a name="routing-metric"></a>Yönlendirme ölçümü

Bir yönlendirme ölçümü hello arabirimleri ve belirtilen hello veri toohello rota hello ağ geçidi ile ilişkili olduğunu ağlar. Yönlendirme metriği birden çok yol var toohello öğrenir, hedef, verilen hello yönlendirme protokolü toocalculate hello en iyi yolu tooa tarafından kullanılan aynı hedef. Merhaba alt hello yönlendirme ölçüm, hello daha yüksek hello tercih.

Hello toochannel trafiği birden çok ağ arabirimleri ve ağ geçitleri ise StorSimple bağlamında yapılandırılmış, hello yönlendirme ölçümleri hangi hello arabirimleri kullanılan play toodetermine hello göreli sırasına gelecektir. Merhaba yönlendirme ölçümleri hello kullanıcı tarafından değiştirilemez. Merhaba ancak kullanabilirsiniz `Get-HcsRoutingTable` cmdlet tooprint hello yönlendirme tablosunu (ve ölçümleri), StorSimple Cihazınızda. Get-HcsRoutingTable cmdlet hakkında daha fazla bilgi [sorun giderme StorSimple dağıtım](storsimple-troubleshoot-deployment.md).

Güncelleştirme 2 ve sonraki sürümler için kullanılan hello yönlendirme ölçüm algoritması şu şekilde açıklanabilir.

* Önceden tanımlanmış değerler atanan toonetwork arabirimleri.
* Atanan değerlerin toohello ile çeşitli ağ arabirimleri, Bulut-Bulut devre dışı veya etkin ancak yapılandırılmış bir ağ geçidi ile Aşağıda örnek bir tabloyu göz önünde bulundurun. Burada atanan Not hello yalnızca örnek değerler değerlerdir.

    | Ağ arabirimi | Bulut etkin | Ağ geçidi ile Bulut devre dışı |
    |-----|---------------|---------------------------|
    | Veri 0  | 1            | -                        |
    | Veri 1  | 2            | 20                       |
    | Veri 2  | 3            | 30                       |
    | Veri 3  | 4            | 40                       |
    | Veri 4  | 5            | 50                       |
    | Veri 5  | 6            | 60                       |


* Merhaba bulut trafiği hello ağ arabirimleri aracılığıyla yönlendirilecek hello sırası şöyledir:
  
    *Veri 0 > veri 1 > tarih 2 > veri 3 > veri 4 > veri 5*
  
    Bu örnekte aşağıdaki hello tarafından açıklanabilir.
  
    StorSimple cihazı iki bulut etkin ağ arabirimleri, veri 0 ve verileri 5 ile göz önünde bulundurun. Veri 1 ile veri 4 Bulut devre dışı ancak yapılandırılmış bir ağ geçidi sahip. trafiği için bu cihazı yönlendirilecek hello sıralaması olacaktır:
  
    *Veri 0 (1) > veri 5 (6) > veri 1 (20) > veri 2 (30) > veri 3 (40) > veri 4 (50)*
  
    *Parantez içindeki Hello sayılar hello ilgili yönlendirme ölçümleri gösterir.*
  
    Veri 0 başarısız olursa, hello bulut trafiği veri 5'ten yönlendirilmiş. Veri 0 ve verileri 5 toofail olsaydı bir ağ geçidi diğer tüm ağ üzerinde yapılandırılmış koşuluyla, hello bulut trafik verileri 1'den geçer.
* Bir bulut etkin ağ arabiriminin başarısız olursa, 3 yeniden denemeyi 30 ikinci gecikme tooconnect toohello arabirimi olan. Tüm hello yeniden deneme başarısız olursa, hello trafiği hello yönlendirme tablosu tarafından belirlenen yönlendirilmiş toohello sonraki kullanılabilir bulut etkin arabirimidir. Tüm bulut etkin Merhaba, ağ arabirimleri başarısız sonra hello aygıt toohello başarısız olur diğer denetleyici (hiçbir yeniden başlatma bu durumda).
* Bir iSCSI etkin ağ arabiriminin VIP hatası varsa, 3 yeniden denemeyi 2 saniye gecikmeyle olacaktır. Bu davranış stayed aynı hello önceki sürümlerden hello. Tüm hello iSCSI ağ arabirimleri başarısız olursa, denetleyici yük devretmesi (yeniden başlatma işlemi tarafından accompanied) meydana gelir.
* VIP başarısız olduğunda bir uyarı da StorSimple Cihazınızda tetiklenir. Daha fazla bilgi için çok Git[uyarı hızlı başvuru](storsimple-8000-manage-alerts.md).
* Yeniden deneme sayısı bakımından iSCSI bulut üzerinden öncelikli olur.
  
    Aşağıdaki örnek hello göz önünde bulundurun: A aygıtın iki ağ arabirimin StorSimple, veri 0 ve 1 Data. Veri 0 bulut etkin Data 1 hem bulut iken ve iSCSI etkin. Bu aygıtta diğer ağ arabirimleri, bulut ya da iSCSI için etkinleştirilir.
  
    Verilen veri 1 başarısız hello son iSCSI ağ arabirimi ise, bu diğer Denetleyici 1 üzerinde hello denetleyici yük devretme tooData içinde sonuçlanır.

### <a name="networking-best-practices"></a>Ağ en iyi uygulamalar

Ayrıca ağ gereksinimleri, StorSimple çözümünüzün hello en iyi performans için yukarıdaki toohello Lütfen uyması en iyi uygulamaları izleyerek toohello:

* StorSimple Cihazınızı ayrılmış 40 MB/sn bant genişliği (veya daha fazla) sahip olduğundan emin olun her zaman kullanılabilir. Bu bant genişliği Paylaşılmaması gerektiğini (veya ayırma hello QoS ilkeleri kullanarak garanti) diğer uygulamalar ile.
* Ağ bağlantısı toohello Internet her zaman kullanılabilir olduğundan emin olun. Ne olursa olsun, Internet bağlantısı durumlarıyla ya da güvenilir olmayan Internet bağlantıları toohello aygıtlar, desteklenmeyen bir yapılandırmada neden olur.
* Ağ arabirimleri aygıtınızda iSCSI ve bulut erişimi için ayrılmış olarak Hello iSCSI ve bulut trafiği yalıtabilirsiniz. Daha fazla bilgi için bkz. nasıl çok[ağ arabirimleri değiştirme](storsimple-8000-modify-device-config.md#modify-network-interfaces) , StorSimple Cihazınızda.
* Bir bağlantı toplama Denetim Protokolü (LACP) yapılandırması ağ arabirimleri için kullanmayın. Bu desteklenmeyen bir yapılandırmadır.

## <a name="high-availability-requirements-for-storsimple"></a>StorSimple için yüksek oranda kullanılabilirlik gereksinimleri

Merhaba StorSimple çözümünüzle birlikte gelen hello donanım platformu, veri merkezinizdeki bir yüksek oranda kullanılabilir, hataya dayanıklı bir depolama altyapısı için bir temel sağlayan kullanılabilirliği ve güvenilirliği özelliklere sahiptir. Ancak, gereksinimler yoktur ve StorSimple çözümünüzün hello kullanılabilirliğini toohelp ile uyumlu olmalıdır en iyi yöntemleri sağlamak. StorSimple dağıtmadan önce gereksinimleri ve hello StorSimple cihazı için en iyi uygulamaları izleyerek ve ana bilgisayarlarda bağlı hello dikkatle gözden geçirin.

İzleme ve StorSimple Cihazınızı hello donanım bileşenleri bakımı hakkında daha fazla bilgi için çok Git[hello StorSimple cihaz Yöneticisi hizmeti toomonitor donanım bileşenleri ve durum kullanma](storsimple-8000-monitor-hardware-status.md) ve [ StorSimple donanım bileşeni değiştirme](storsimple-8000-hardware-component-replacement.md).

### <a name="high-availability-requirements-and-procedures-for-your-storsimple-device"></a>Yüksek oranda kullanılabilirlik gereksinimleri ve StorSimple cihazınız için yordamlar

Aşağıdaki bilgilerle dikkatle gözden geçirme hello tooensure hello yüksek kullanılabilirliğini StorSimple Cihazınızı.

#### <a name="pcms"></a>PCMs

StorSimple cihazları yedekli, hot Swap güç ve soğutma modülleri (PCMs) içerir. Her PCM hello tüm kasa için yeterli kapasitesi tooprovide hizmeti vardır. tooensure yüksek kullanılabilirlik, her iki PCMs yüklü olması gerekir.

* Güç kaynağı başarısız olursa, PCMs toodifferent güç kaynakları tooprovide kullanılabilirlik bağlayın.
* Bir PCM başarısız olursa, yenisini hemen isteyin.
* Yalnızca hello değiştirme varsa ve hazır tooinstall olan başarısız bir PCM kaldırırsanız.
* Her iki PCMs eşzamanlı olarak kaldırmayın. Merhaba PCM modülü hello yedek pil modülü içerir. Her ikisi de kaldırarak Merhaba pil koruma kapatılmadan PCMs sonuçlanır ve hello cihaz durumu kaydedilmeyecek. Merhaba pil hakkında daha fazla bilgi için çok Git[Koru hello yedek pil Modülü](storsimple-8000-battery-replacement.md#maintain-the-backup-battery-module).

#### <a name="controller-modules"></a>Denetleyici modülleri

StorSimple cihazları yedekli, hot Swap denetleyicisi modülleri içerir. Merhaba denetleyicisi modülleri bir etkin/pasif şekilde çalışır. Herhangi bir anda belirli bir Denetleyici Modülü etkindir ve hizmet sağlama, başlangıç sırasında diğer Denetleyici Modülü pasif. Merhaba pasif denetleyiciyi modülü açık olduğundan ve hello etkin Denetleyici Modülü hata verirse veya işlemsel duruma kaldırıldı. Her Denetleyici Modülü hello tüm kasa için yeterli kapasitesi tooprovide hizmeti vardır. Her iki denetleyicisi modülleri yüklü tooensure yüksek oranda kullanılabilir olması gerekir.

* Her iki denetleyicisi modülleri her zaman yüklü olduğundan emin olun.
* Bir Denetleyici Modülü başarısız olursa, yenisini hemen isteyin.
* Yalnızca hello değiştirme varsa ve hazır tooinstall olan başarısız Denetleyici Modülü kaldırırsanız. Bir modül uzun süreler kaldırma hello hava akışı etkileyebilir ve bu nedenle hello sistemi soğutma hello.
* Merhaba ağ bağlantıları tooboth denetleyicisi modülleri özdeş ve hello bağlı ağ arabirimine sahip bir aynı ağ yapılandırması emin olun.
* Denetleyici Modülü başarısız veya değiştirilmesi gerekiyorsa, o hello emin olun hello başarısız Denetleyici Modülü değiştirmeden önce diğer denetleyici modülü etkin durumda değil. bir denetleyici etkin olduğunu tooverify Git çok[tanımla hello etkin denetleyicisinde Cihazınızı](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device).
* Her iki denetleyicisi modüller hello kaldırmayın aynı anda. Denetleyici yük devretme işlemi devam ediyor, etmeyin hello bekleme Denetleyici Modülü kapatın veya hello kasa kaldırın.
* Denetleyici yük devretme sonrasında, her iki Denetleyici Modülü kaldırmadan önce en az beş dakika bekleyin.

#### <a name="network-interfaces"></a>Ağ arabirimleri

StorSimple cihaz denetleyicisi modülleri her olan dört 1 Gigabit ve iki 10 Gigabit Ethernet ağ arabirimleri.

* Merhaba ağ bağlantıları tooboth denetleyicisi modülleri özdeş ve hello Denetleyici Modülü arabirimler bağlı toohave aynı ağ yapılandırması olduğunu hello ağ arabirimleri emin olun.
* Mümkün olduğunda, farklı anahtarlara tooensure hizmet kullanılabilirliği hello olay bir ağ aygıtı hatanın üzerinden ağ bağlantıları dağıtın.
* Yalnızca başlangıç ya da hello son kalan çıkarırken varsa iSCSI etkin arabirimiyle (IP) atanan, hello arabirimi önce devre dışı bırakın ve hello kabloları çıkarın. Ardından Hello arabirimi ilk takılı ise, onu hello active denetleyicisi toofail toohello pasif denetleyiciyi neden olur. Hello pasif denetleyiciyi de takılı karşılık gelen arabirimlerinden varsa, daha sonra hem hello denetleyicileri birden çok kez bir denetleyicisinde şekilde önce yeniden başlatılır.
* En az iki veri arabirimleri toohello ağ her denetleyici modülünden bağlayın.
* Merhaba iki 10 GbE arabirimleri etkinleştirilirse, farklı anahtarlara kullananlar dağıtın.
* Mümkün olduğunda, MPIO hello sunucuları bağlantı, ağ veya arabirim hatalarına dayanabileceğinden sunucuları tooensure üzerinde kullanın.

Cihazınız yüksek kullanılabilirlik ve performans için ağ hakkında daha fazla bilgi için çok Git[StorSimple 8100 cihazınız yüklemek](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) veya [StorSimple 8600 model Cihazınızı yüklemek](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

#### <a name="ssds-and-hdds"></a>SSD ve HDD

Kullanılarak korunan sabit disk sürücülerinin (HDD'ler) alanları yansıtılmış ve katı hal diskleri (SSD'ler) StorSimple cihazları içerir. Yansıtılmış alanlardaki kullanımını hello aygıt mümkün tootolerate hello hatası veya bir veya daha fazla SSD HDD sağlar.

* Tüm SSD ve HDD modülleri yüklü olduğundan emin olun.
* Bir SSD veya HDD başarısız olursa, yenisini hemen isteyin.
* Bir SSD veya HDD başarısız veya değiştirilmesi gerekiyorsa, yalnızca hello SSD ya da değiştirme gerektirir HDD kaldırdığınızdan emin olun.
* Herhangi bir noktada hello sisteminden birden fazla SSD veya HDD zamanında kaldırmayın.
  2 veya daha fazla disk (HDD, SSD), belirli türde bir hata veya kısa süre içinde art arda başarısız sistemi arızası ve olası veri kaybına neden olabilir. Bu gerçekleşirse, [Microsoft Support başvurun](storsimple-8000-contact-microsoft-support.md) Yardım için.
* Değiştirme sırasında hello izlemek **paylaşılan bileşenleri** hello içinde **donanım durumu** hello dikey penceresinde hello SSD ve HDD sürücüler. Yeşil onay durumu hello disklerde iyi ya da Tamam, kırmızı bir ünlem işaret ise bir başarısız SSD veya HDD gösterir gösterir.
* Bir sistem hatası durumunda tooprotect gereken tüm birimler için bulut anlık görüntüleri yapılandırmanızı öneririz.

#### <a name="ebod-enclosure"></a>EBOD muhafazası

StorSimple cihaz modeli 8600 genişletilmiş demet, diskleri (EBOD) kasası ayrıca toohello birincil muhafazada içerir. Kullanılarak korunan sabit disk sürücülerinin (HDD'ler) alanları yansıtılmış ve bir EBOD EBOD denetleyicisi içerir. Yansıtılmış alanlardaki kullanımını hello cihaz bir veya daha fazla HDD mümkün tootolerate hello başarısızlığını sağlar. Merhaba EBOD muhafazası bağlı toohello birincil yedek SAS kabloları Motoru'nu ' dir.

* Olduğundan emin olun hem EBOD muhafazası denetleyicisi modülleri SAS kabloları hem tüm hello sabit disk sürücülerinin her zaman yüklenir.
* EBOD muhafazası Denetleyici Modülü başarısız olursa, yenisini hemen isteyin.
* EBOD muhafazası Denetleyici Modülü başarısız olursa, o hello emin olun hello başarısız modülü değiştirmeden önce diğer Denetleyici Modülü etkindir. bir denetleyici etkin olduğunu tooverify Git çok[tanımla hello etkin denetleyicisinde Cihazınızı](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device).
* Sürekli bir EBOD denetleyicisi modülü değiştirme sırasında erişerek hello StorSimple cihaz Yöneticisi hizmeti hello bileşeninde hello durumunu izleme **İzleyici** > **donanım durumu** .
* Bir SAS kablosu başarısız veya değiştirme (Microsoft Support söz konusu toomake bir tür belirleme olmalıdır) gerekiyorsa, değiştirme gerektiren hello SAS kablosu kaldırdığınızdan emin olun.
* Aynı anda iki SAS kabloları herhangi bir noktada hello sisteminden zamanında kaldırmayın.

### <a name="high-availability-recommendations-for-your-host-computers"></a>Ana bilgisayarlar için yüksek kullanılabilirlik önerileri

Bu en iyi yöntemler tooensure hello yüksek kullanılabilirliğini konakları bağlı tooyour StorSimple cihazı dikkatle gözden geçirin.

* StorSimple ile yapılandırma [iki düğümlü dosya sunucusu küme yapılandırmaları][1]. Hata ve artıklık hello konak tarafındaki oluşturma tek hata noktaları kaldırarak, çözümün tamamında hello yüksek oranda kullanılabilir hale gelir.
* Kullanılabilir paylaşımları sürekli olarak (CA) kullanılabilir hello depolama alanı denetleyicileri yük devretme sırasında yüksek kullanılabilirlik için Windows Server 2012 (SMB 3.0) kullanın. Dosya sunucusu kümesi ve kullanılabilir paylaşımları sürekli olarak Windows Server 2012 ile yapılandırmak için ek bilgi için toothis başvurun [video demo](http://channel9.msdn.com/Events/IT-Camps/IT-Camps-On-Demand-Windows-Server-2012/DEMO-Continuously-Available-File-Shares).

## <a name="next-steps"></a>Sonraki adımlar

* [StorSimple sistemi sınırları hakkında bilgi almak](storsimple-8000-limits.md).
* [Bilgi nasıl toodeploy StorSimple çözümünüzün](storsimple-8000-deployment-walkthrough-u2.md).

<!--Reference links-->
[1]: https://technet.microsoft.com/library/cc731844(v=WS.10).aspx
