---
title: "Azure tooan şirket içi siteden aaaReprotect | Microsoft Docs"
description: "Sanal makineleri tooAzure, yük devretme sonrasında bir yeniden çalışma toobring VM'ler geri tooon içi başlatabilirsiniz. Bilgi nasıl tooreprotect bir yeniden çalışma önce."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 94c86e79cba4cd3f0c5821fdd5509cca1d0e7820
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-azure-tooan-on-premises-site"></a>Azure tooan şirket içi siteden koruyun



## <a name="overview"></a>Genel Bakış
Bu makalede nasıl tooreprotect Azure sanal makineleri Azure tooan şirket içi siteden. Toofail hazır olduğunuzda, bu makaledeki hello yönergeleri izleyin, VMware sanal makineleri veya Windows/Linux fiziksel sunucuları bunlar hello şirket içi site tooAzure devredilir sonra geri (açıklandığı gibi [VMware sanal Çoğalt makineler ve Azure Site Recovery ile fiziksel sunucuları tooAzure](site-recovery-failover.md)).

> [!WARNING]
> Sonra size geri kapatamazsınız [tamamlamak geçiş](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), bir sanal makine tooanother kaynak grubuna taşımak veya bir Azure sanal makinesini silme.


Yükü bittikten sonra hello korumalı sanal makineleri çoğaltma yapıyorsanız, yeniden çalışma hello sanal makineleri toobring üzerinde başlatabilirsiniz bunları toohello şirket içi site.

POST yorumlarınızı ve sorularınızı bu makalenin veya hello hello sonunda [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Hızlı bir genel bakış için nasıl Azure tooan gelen üzerinden toofail site içi hakkında video aşağıdaki hello izleyin.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]


## <a name="prerequisites"></a>Ön koşullar
Tooreprotect sanal makineleri hazırladığınızda alın veya önkoşul eylemleri aşağıdaki hello göz önünde bulundurun:

* Bir vCenter sunucusu yönetiyorsa toofail istediğiniz hello sanal makineleri yedekleyebilir, hello sahip olduğunuzdan emin olun [gerekli izinleri](site-recovery-vmware-to-azure-classic.md) vCenter sunucuları üzerindeki sanal makinelerin bulma.

  > [!WARNING]
  > Anlık görüntü üzerinde hello mevcut olup olmadığını ana hedef veya hello sanal makine yükü başarısız şirket içi. Tooreprotect devam etmeden önce hello ana hedef hello anlık görüntü silebilirsiniz. Merhaba sanal makineye Hello anlık görüntüleri otomatik olarak yeniden koruma işi sırasında birleştirilir.

* Geri dönecek önce iki ek bileşeni oluşturun:

  * **İşlem sunucusu**: Merhaba [işlem sunucusu](site-recovery-vmware-setup-azure-ps-resource-manager.md) azure'da hello korumalı sanal makine verileri alan ve veri toohello şirket içi siteye gönderir. Düşük gecikme süreli ağ hello işlem sunucusu ve korumalı hello sanal makine arasında gereklidir. Bu nedenle, bir Azure ExpressRoute bağlantısı veya bir Azure tabanlı işlem sunucusu ve VPN kullanıyorsanız, bir şirket içi işlem sunucusu olabilir.
  
  * **Ana hedef sunucusu**: hello ana hedef sunucusu yeniden çalışma verileri alır. oluşturduğunuz hello şirket içi yönetim sunucusu varsayılan olarak yüklenen bir ana hedef sunucusu vardır. Ancak, başarısız geri trafik hacmi hello bağlı olarak, toocreate ayrı ana hedef sunucusu yeniden çalışma için gerekebilir.
    * [Linux sanal makine bir Linux ana hedef sunucusunun gerekiyor](site-recovery-how-to-install-linux-master-target.md).
    * Windows sanal makine bir Windows ana hedef sunucusu gerekir. Merhaba şirket içi işlem sunucusu ve ana hedef makinelere yeniden kullanabilirsiniz.

    Hello ana hedefe sahiptir listelenen diğer Önkoşullar [yeniden koruma önce ana hedefte ortak interneti toocheck](site-recovery-how-to-reprotect.md#common-things-to-check-after-completing-installation-of-the-master-target-server).

* Geri başarısız olduğunda bir yapılandırma gerekli şirket içi sunucusudur. Yeniden çalışma sırasında hello sanal makine hello yapılandırma sunucusu veritabanında mevcut olması gerekir. Aksi takdirde, yeniden çalışma başarısız olur. 

> [!IMPORTANT]
> Yapılandırma sunucunuzun düzenli olarak zamanlanmış yedeklemeler ele emin olun. Bir olağanüstü durum varsa, aynı IP adresinin yeniden çalışma çalışır hello hello sunucusuyla geri yükleyin.

* Set hello `disk.EnableUUID=true` hello ana hedef sanal makine VMware hello yapılandırma parametrelerini ayarlama. Bu satır mevcut değilse, bunu ekleyin. Bu ayar gerekli tooprovide tutarlı UUID toohello sanal makine (VMDK) diski, böylelikle doğru bağlar.

* *Depolama VMotion'ı hello ana hedef sunucusunda kullanamazsınız*. Bu hello geri dönme toofail neden olabilir. Merhaba diskleri kullanılabilir tooit olmadığından hello sanal makine başlatılamıyor. tooprevent Bu sorun, VMotion'ı listenizden dışlama hello ana hedef sunucusu.

* Yeni bir sürücü toohello ana hedef Sunucusu Ekle: bekletme sürücüsü. Yeni bir disk ve biçiminde hello sürücüye ekleyin.


### <a name="frequently-asked-questions"></a>Sık sorulan sorular

#### <a name="why-do-i-need-a-s2s-vpn-or-an-expressroute-connection-tooreplicate-data-back-toohello-on-premises-site"></a>S2S VPN veya bir ExpressRoute bağlantı tooreplicate veri geri toohello şirket içi site neden ihtiyacım var mı?
Şirket içi tooAzure Çoğaltmada hello Internet oluşabilir veya bir site siteye (S2S) bir ExpressRoute genel eşliği olan bağlantısı, yükü ve yeniden çalışma gerektiren ancak VPN tooreplicate verileri. Azure'da Hello başarısız üzerinden sanal makineler (ping) hello şirket içi yapılandırma sunucusu erişebilmesi için hello ağ sağlar. Bir işlem sunucusu hello hello başarısız üzerinden sanal makinenin Azure ağı içinde de dağıtabilirsiniz. Bu işlem sunucunun da yapabilir toocommunicate hello şirket içi yapılandırma sunucusu ile olmalıdır.

#### <a name="when-should-i-install-a-process-server-in-azure"></a>Bir işlem sunucusu Azure'da yüklediğimde?


Merhaba sanal makineler tooreprotect istediğiniz Azure üzerinde çoğaltma verileri tooa işlem sunucusuna gönderir. Azure sanal makinelerde Hello hello işlem sunucusu erişebilmesi için ağınızı ayarlayın.

Bir işlem sunucusu azure'da dağıtmak veya yük devretme sırasında kullanılan hello mevcut işlem sunucusunu kullanabilir. Merhaba önemli nokta tooconsider hello gecikme toosend hello Azure toohello işlem sunucusunda hello sanal makinelerden verilerdir.

Ayarlanmış bir ExpressRoute bağlantınız varsa, hello gecikme hello sanal makineyle hello işlem sunucusu arasında düşük olduğundan, bir şirket içi işlem sunucusu toosend verileri kullanabilirsiniz.

 ![ExpressRoute için mimarisi diyagramı](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)



Ancak, yalnızca bir S2S VPN varsa, azure'da hello işlem sunucusu dağıtımı öneririz.

 ![VPN mimarisi diyagramı](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)


Yalnızca hello S2S VPN veya Merhaba, ExpressRoute ağ eşlemesi özel üzerinden çoğaltma olur unutmayın. Yeterli bant genişliği ağ kanal üzerinden kullanılabilir olduğundan emin olun.

Bir Azure tabanlı işlem sunucusu yükleme hakkında daha fazla bilgi için bkz: [Azure'da çalışan bir işlem sunucusu yönetmek](site-recovery-vmware-setup-azure-ps-resource-manager.md).

> [!TIP]
> Bir Azure tabanlı işlem sunucusu yeniden çalışma sırasında kullanmanızı öneririz. Merhaba çoğaltma performans hello işlem sunucusu sanal makine (azure'da hello başarısız üzerinden makine) çoğaltma daha yakından toohello ise yüksek olur. Ancak, prototip (PT) ya da gösterim, kanıtı sırasında özel eşleme toocomplete hello ile POC daha hızlı hello şirket içi işlem sunucusu ExpressRoute ile birlikte kullanabilirsiniz.



#### <a name="what-ports-should-i-open-on-different-components-so-that-reprotection-can-work"></a>Yükü çalışabilmeniz için hangi bağlantı noktalarının t farklı bileşenleri açmalı mısınız?

![Yük devretme ve yeniden çalışma için bağlantı noktaları](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

#### <a name="which-master-target-server-should-i-use-for-reprotection"></a>Yükü için hangi ana hedef sunucusu kullanmalıyım?
Bir şirket içi ana hedef sunucusu hello işlem sunucusu gerekli tooreceive verilerdir ve ardından toohello şirket içi sanal makinenin VMDK yazın. Windows sanal makineleri koruyorsanız, Windows ana hedef sunucusu gerekir. Merhaba şirket içi işlem sunucusu ve ana hedef yeniden<!-- !todo component -->. Linux sanal makineleri için bir şirket içinde ek Linux ana hedefinin yukarı tooset gerekir.


Bir ana hedef sunucusu yükleme hakkında daha fazla bilgi için bkz:

* [Hedef sunucunun nasıl tooinstall Windows Yöneticisi](site-recovery-vmware-to-azure.md)
* [Nasıl tooinstall Linux ana hedef sunucusu](site-recovery-how-to-install-linux-master-target.md)


#### <a name="what-datastore-types-are-supported-on-hello-on-premises-esxi-host-during-failback"></a>Hangi veri deposu türleri hello şirket içi ESXi ana bilgisayarda yeniden çalışma sırasında destekleniyor mu?

Şu anda, başarısız olan Azure Site Recovery destekler, yalnızca tooa sanal makine dosya sistemi (VMFS) veya vSAN veri deposu yedekleyin. NFS veri deposu desteklenmiyor. Toothis sınırlaması yeniden koruma ekran NFS datastores hello durumda boşsa veya hello vSAN veri deposu gösterir ancak hello işi sırasında başarısız üzerinde hello hello veri deposu seçimi girin. Geri toofail düşünüyorsanız, şirket içi bir VMFS veri deposu oluşturma ve geri tooit başarısız. Bu geri dönme hello VMDK tamamını indirmeyi neden olur.

### <a name="common-things-toocheck-after-completing-installation-of-hello-master-target-server"></a>Merhaba ana hedef sunucusunun yüklemesini tamamladıktan sonra ortak interneti toocheck

* Merhaba sanal makine varsa, şirket içi vCenter sunucusu Merhaba, hello ana hedef sunucusu toohello şirket içi sanal makinenin VMDK erişimi gerektirir. Gerekli toowrite hello çoğaltılmış verileri toohello sanal makinenin disklerinin erişilebilir. Merhaba şirket içi sanal makinenin veri deposu okuma/yazma erişimine sahip hello ana hedefin ana bilgisayarına bağlandığından emin olun.

* Merhaba sanal makine mevcut şirket içi hello vCenter sunucusunda değilse, Site Recovery hizmeti hello toocreate yeni bir sanal makine yükü sırasında gerekir. Bu sanal makine hello ana hedef oluşturma hello ESX ana bilgisayarda oluşturulur. Merhaba geri dönme sanal makine istediğiniz hello konakta oluşturulan hello ESX konak dikkatlice seçin.

* *Merhaba ana hedef sunucusu için depolama VMotion'ı kullanamazsınız*. Bu hello geri dönme toofail neden olabilir. Merhaba diskleri kullanılabilir tooit olmadığından hello sanal makine başlatılamıyor.

  > [!WARNING]
  > Bir ana hedef depolama VMotion'ı görev yükü sonra uğradığında, ekli toohello ana hedef hello korumalı sanal makineleri disklerinin toohello hedef hello VMotion'ı görevinin geçirin. Bundan sonra toofail çalışırsanız, hello diskleri bulunamadı ayrılmayı hello diskin başarısız olur. Ardından, depolama hesaplarınıza sabit toofind hello diskleri haline gelir. Toofind ihtiyacınız bunları el ile ve toohello sanal makine ekleyin. Bundan sonra önyükleme hello şirket içi sanal makine.

* Bir bekletme sürücü tooyour mevcut Windows ana hedef sunucu ekleyin. Yeni bir disk ve biçiminde hello sürücüye ekleyin. Merhaba bekletme sürücüsü kullanılan toostop hello noktaları hello sanal makine geri toohello şirket içi siteye ne zaman çoğaltılacağını saattir. Saklama sürücüsünün bazı ölçütlere aşağıda verilmiştir. Bu ölçütler hello sürücü hello ana hedef sunucusu için yer almaz.

   * Merhaba birim, çoğaltma hedefi gibi başka bir amaç için kullanılmaz.

   * Merhaba birim kilidi modunda değil.

   * Merhaba birimi bir önbellek birimi değil. Merhaba ana hedef yükleme bu birimde mevcut döndürmemelidir. Merhaba özel yükleme birimi hello işlem sunucusu ve ana hedef için bekletme birimi için uygun değil. Merhaba işlem sunucusu ve ana hedef birimde yüklendiğinde hello birim hello ana hedef önbellek birimdir.

   * Merhaba birimin Hello dosya sistemi türü, FAT veya FAT32 değil.

   * Merhaba birim kapasitesi sıfırdan farklı.

   * Merhaba varsayılan saklama birimi için Windows hello R birimdir.

   * Merhaba varsayılan saklama Linux için /mnt/retention birimdir.

  > [!IMPORTANT]
  > Var olan bir işlem sunucusu/configuration server makine veya bir ölçekte veya bir işlem sunucusu/ana hedef sunucu makinesi kullanıyorsanız, yeni bir sürücüye tooadd gerekir. Merhaba yeni sürücü hello gereksinimleri önceki karşılamalıdır. Merhaba bekletme sürücüsü yoksa, hello portal hello seçimi aşağı açılan listesinde görünmüyor. Bir sürücü toohello şirket içi ana hedef ekledikten sonra hello sürücü tooappear hello portalındaki hello seçimdeki too15 dakika kaplar. Merhaba sürücü 15 dakika sonra görünmüyorsa hello yapılandırma sunucusu de yenileyebilirsiniz.

* Linux başarısız üzerinden sanal makine bir Linux ana hedef sunucusu gerektirir. Windows başarısız üzerinden sanal makine bir Windows ana hedef sunucusu gerektirir.

* VMware araçları hello ana hedef sunucuya yükleyin. Merhaba VMware araçları hello datastores hello ana Hedef'in ESXi konağına üzerinde algılanamıyor.

* Merhaba etkinleştirmek `disk.EnableUUID=true` hello vCenter özellikleri kullanarak hello ana hedef sanal makineye parametresi. <!-- !todo Needs link. -->

* Merhaba ana hedef en az bir VMFS veri deposu bağlı olması gerekir. Varsa hiçbiri, hello **veri deposu** hello yeniden koruma sayfasında giriş boş olacaktır ve devam edemiyor.

* Merhaba ana hedef sunucusu anlık görüntüleri hello disklerde sahip olamaz. Anlık görüntüler varsa, yükü ve yeniden çalışma başarısız.

* Merhaba ana hedef Paravirtual SCSI denetleyicisine sahip olamaz. Merhaba denetleyicisi yalnızca bir LSI Logic denetleyicisi olabilir. LSI Logic denetleyicisi, yükü başarısız olur.

<!--
### Failback policy
tooreplicate back tooon-premises, you will need a failback policy. This policy get automatically created when you create a forward direction policy. Note that

1. This policy gets auto associated with hello configuration server during creation.
2. This policy is not editable.
3. hello set values of hello policy are (RPO Threshold = 15 Mins, Recovery Point Retention = 24 Hours, App Consistency Snapshot Frequency = 60 Mins)
   ![](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

-->

## <a name="steps-tooreprotect"></a>Adımları tooreprotect

> [!NOTE]
> Azure'da bir sanal makine önyükleme sonra tooregister geri toohello yapılandırma sunucusu (yukarı too15 dakika) hello aracısı için biraz zaman alabilir. Bu süre boyunca yükü başarısız olur ve bu hello aracı yüklü olmadığı bir hata iletisi gösterir. Birkaç dakika bekleyin ve ardından yükü yeniden deneyin.



1. İçinde **kasa** > **öğeleri çoğaltılan**devredilen hello sanal makineye sağ tıklayın ve ardından **yeniden koruma**. Merhaba seçin ve makine tıklatarak **yeniden koruma** hello komut düğmeleri gelen.
2. Bu koruma, hello yönünü Hello dikey penceresinde, fark **Azure tooOn içi**, zaten seçilidir.
3. İçinde **ana hedef sunucusu** ve **işlem sunucusu**hello şirket içi ana hedef sunucusunu seçin ve hello işlem sunucusu.
4. İçin **veri deposu**, istediğiniz toorecover hello diskler şirket içi veri deposu toowhich hello seçin. Bu seçenek hello şirket içi sanal makine silinir ve toocreate yeni diskler ihtiyacınız olmadığında kullanılır. Bu seçenek hello diskleri zaten var, ancak yine de toospecify bir değer gerekir, göz ardı edilir.
5. Merhaba bekletme sürücüsü'ı seçin.
6. Merhaba geri dönme ilkesini otomatik olarak seçilir.
7. Tıklatın **Tamam** toobegin yükü. Bir iş tooreplicate hello sanal makine Azure toohello şirket içi siteden başlar. Merhaba üzerinde hello ilerleme durumunu izleyebilirsiniz **işleri** sekmesi.

(Merhaba şirket içi sanal makine silindiğinde) toorecover tooan alternatif konuma istiyorsanız hello bekletme sürücüsü ve hello ana hedef sunucu için yapılandırılmış veri deposu seçin. Geri toohello şirket içi site başarısız olduğunda hello VMware sanal makineleri hello geri dönme koruma planı kullanımda olarak ana hello aynı veri deposu hello hedef sunucu. Yeni bir sanal makine ardından Vcenter'da oluşturulur.

Azure tooan varolan üzerinde toorecover hello sanal makinenin sanal makine şirket içi istiyorsanız, bağlama hello hello ana hedef sunucunun ESXi ana bilgisayar üzerinde okuma/yazma erişimi olan sanal makinenin datastores şirket içi.
    ![İletişim kutusunu yeniden koruma](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

Ayrıca bir kurtarma planı hello düzeyinde koruyun. Bir çoğaltma grubu yalnızca bir kurtarma planı reprotected. Bir kurtarma planı kullanarak koruyun, korunan her makine için tooprovide hello değerleri gerekir.

> [!NOTE]
> Bir çoğaltma grubu aynı ana hedef sunucusu tooreprotect hello kullanın. Farklı bir ana hedef sunucusu tooreprotect bir çoğaltma grubu kullanıyorsanız, hello sunucu zamanında ortak bir nokta sağlayamaz.

> [!NOTE]
> Merhaba şirket içi sanal makine yükü sırasında kapalıdır. Bu, çoğaltma sırasında veri tutarlılığını sağlamaya yardımcı olur. Yükü bittikten sonra hello sanal makinede etkinleştirmeyin.

Merhaba yükü başarılı olduktan sonra hello sanal makinenin korumalı bir duruma girer.

## <a name="next-steps"></a>Sonraki adımlar

Merhaba sanal makinenin korumalı bir duruma geçtiğini sonra [bir yeniden başlatma](site-recovery-how-to-failback-azure-to-vmware.md#steps-to-fail-back). 

Merhaba geri dönme azure'da hello sanal makine ve önyükleme hello şirket içi sanal makine kapalı kapanır. Bazı hello uygulama kesintiler bekler. Merhaba uygulama kapalı kalma süresi dayanabileceği yeniden çalışma için bir saat seçin.

## <a name="common-problems"></a>Sık karşılaşılan sorunları

* Sanal makinelerinizi bir şablon toocreate kullandıysanız, her bir sanal makine hello diskler için kendi UUID olduğundan emin olun. Merhaba değeriyle hello ana hedef sanal makinenin UUID çakışmalarından hem hello aynı oluşturulmadığından şirket içi, şablon, yükü başarısız olur. Hello aynı oluşturulmamış başka bir ana hedef dağıtmak şablonu.

* Salt okunur kullanıcı vCenter bulma işlemini ve sanal makineleri koruma, koruma başarılı ve yük devretme çalışır. Merhaba datastores bulunan için yükü sırasında yük devretme başarısız olur. Bir belirti datastores yükü sırasında listelenmeyen bu hello olmasıdır. tooresolve bu sorunu izinleri, uygun bir hesapla hello vCenter kimlik bilgileri güncelleştirebilir ve hello işi yeniden deneyin. Daha fazla bilgi için bkz: [çoğaltmak VMware sanal makineleri ve fiziksel sunucuları tooAzure Azure Site Recovery ile](site-recovery-vmware-to-azure-classic.md).

* Linux sanal makine yeniden çalışmak ve şirket içi çalıştırın, o hello ağ yöneticisi paket hello makineden kaldırıldı görebilirsiniz. Azure'da Hello sanal makine kurtarıldığında hello ağ yöneticisi paket kaldırıldığı bu kaldırma işlemi gerçekleşir.

* Linux sanal makine tooAzure üzerinde başarısız oldu ve statik IP adresiyle yapılandırılmış olduğunda, başlangıç IP adresi DHCP'den alınır. Tooon içi başarısız olduğunda hello sanal makine toouse DHCP tooacquire başlangıç IP adresi devam eder. El ile toohello makinede oturum açın ve gerekirse, başlangıç IP adresi geri tooa statik adresi ayarlayın. Windows sanal makinesi statik IP yeniden elde edebilirsiniz.

* ESXi 5.5 ücretsiz sürüm veya 6 vSphere hiper yönetici ücretsiz sürümü kullanıyorsanız, yük devretme başarılı olur, ancak geri dönme başarılı olmaz. tooenable geri dönme, yükseltme tooeither program'ın değerlendirme lisansı.

* Hello işlem sunucusunun yapılandırma sunucusundan hello bağlanamazsa, Telnet toocheck bağlantı toohello yapılandırma sunucusu bağlantı noktası 443 üzerinde kullanın. Merhaba işlem sunucusu tooping hello yapılandırma sunucusundan da deneyebilirsiniz. Bağlı toohello yapılandırma sunucusu olduğunda bir işlem sunucusu bir sinyal de olmalıdır.

* Toofail geri tooan alternatif vCenter çalışıyorsanız, yeni vCenter ve hello ana hedef sunucusunda bulunan emin olun. Tipik bir belirti hello datastores erişilebilir veya hello görünür olmamasıdır **koruyun** iletişim kutusu.

* Fiziksel sunucu şirket içi korunan bir Windows Server 2008 R2 SP1 sunucusu geri Azure tooan şirket içi siteden başarısız olamaz.
