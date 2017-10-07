---
title: Azure tooVMware gelen geri aaaHow toofail | Microsoft Docs
description: "Sanal makineler tooAzure, yük devretme sonrasında bir yeniden çalışma toobring sanal makineleri geri tooon içi başlatabilirsiniz. Toofail nasıl geri hello adımlarını öğrenin."
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
ms.openlocfilehash: b82abf6b15db9dccab49edbd14298b121e9fdc6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-from-azure-tooan-on-premises-site"></a>Geri Azure tooan şirket içi siteden başarısız

Bu makalede nasıl toofail geri sanal makineleri Azure sanal makineleri toohello şirket içi siteden açıklanmaktadır. Bu makale toofail hello yönergeleri izleyin, VMware sanal makineleri veya Windows/Linux fiziksel sunucuları bunlar hello şirket içi site tooAzure hello kullanarak devredilir sonra geri [çoğaltmak VMware sanal makineleri ve fiziksel Azure Site Recovery ile sunucuları tooAzure](site-recovery-vmware-to-azure-classic.md) Öğreticisi.

> [!WARNING]
> Varsa [tamamlandı geçiş](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)taşınan hello sanal makine tooanother kaynak grubu veya silinen hello Azure sanal makine, yeniden çalışma bundan sonra olamaz.

> [!NOTE]
> VMware sanal makineleri üzerinde başarısız olursa yeniden çalışma tooa Hyper-v konak yapılamıyor.

## <a name="overview-of-failback"></a>Yeniden çalışma genel bakış
Yeniden çalışma şeklini aşağıda verilmiştir. TooAzure başarısız olmuş sonra birkaç aşamada geri tooyour şirket içi site başarısız olur:

1. [Koruyun](site-recovery-how-to-reprotect.md) tooreplicate tooVMware sanal makineleri şirket içi sitenizdeki başlatmaları böylece Azure sanal makinelerde hello. Bu işlemin bir parçası olarak, ayrıca gerekir:
    1. Bir şirket içi ana hedef ayarlama: Windows ana hedef Windows sanal makineler için ve [Linux ana hedefinin](site-recovery-how-to-install-linux-master-target.md) Linux sanal makineleri için.
    2. Ayarlanmış bir [işlem sunucusu](site-recovery-vmware-setup-azure-ps-resource-manager.md).
    3. Başlatma [koruyun](site-recovery-how-to-reprotect.md). Bu hello şirket içi sanal makineyi kapatın ve hello Azure eşitleme sanal makinenin verilerini hello ile şirket içi diskler.
5. Azure'da sanal makinelerinizi tooyour şirket içi siteye çoğaltma yapıyorsanız sonra bir hata üzerinden Azure toohello şirket içi siteden başlatır.

Verilerinizi geri başarısız oldu sonra böylece tooreplicate tooAzure başlatmaları geri için başarısız hello şirket içi sanal makineleri koruyun.

Hızlı bir genel bakış için nasıl Azure tooan gelen üzerinden toofail site içi hakkında video aşağıdaki hello izleyin.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]

### <a name="fail-back-toohello-original-or-alternate-location"></a>Geri toohello özgün veya alternatif konuma başarısız

Bir VMware sanal makinesi üzerinde başarısız olduysa, aynı kaynak şirket içi sanal onu oluşmaya devam makine var. geri toohello başarısız olabilir. Bu senaryoda, yalnızca hello değişiklikler geri çoğaltılır. Bu senaryo, özgün konuma kurtarma bilinir. Merhaba şirket içi sanal makine yoksa hello alternatif bir konum kurtarma senaryodur.

> [!NOTE]
> Yalnızca geri dönme toohello özgün vCenter ve yapılandırma sunucusu kullanabilirsiniz. Yeni yapılandırma sunucusu ve kullanmaya geri dönme dağıtamazsınız. Ayrıca, yeni vCenter toohello mevcut yapılandırma sunucusu ve yeniden çalışma hello yeni vCenter ekleyemezsiniz.

#### <a name="original-location-recovery"></a>Özgün konuma kurtarma

Geri toohello özgün sanal makine başarısız olursa, aşağıdaki koşullar hello gereklidir:
* Merhaba sanal makine bir vCenter sunucusu tarafından yönetiliyorsa, ardından hello ana hedefin ESX konak erişim toohello sanal makinenin veri deposu olması gerekir.
* Merhaba sanal makine bir ESX konağında ancak hello sabit disk hello sanal makinenin bir veri deposunda olmalıdır vCenter tarafından yönetilmiyor hello ana hedefin ait ana erişebilir.
* Sanal makinenize bir ESX konağında ise ve vCenter kullanmaz, koruyun önce bulma hello ana hedefinin hello ESX konağının tamamlamanız gerekir. Geri fiziksel sunucuları, çok çalıştırma işlemini gerçekleştiriyorsanız bu geçerlidir.
* Geri tooa sanal depolama alanı ağı (vSAN) veya hello diskleri zaten var ve bağlı toohello şirket içi sanal makine (RDM) eşleme ham aygıtta temel bir disk başarısız olabilir.

#### <a name="alternate-location-recovery"></a>Alternatif konuma kurtarma
Hello şirket içi sanal makine hello sanal makineyi yeniden korumayı önce mevcut değilse, alternatif bir konum kurtarma hello Senaryo adı verilir. Merhaba yeniden koruma iş akışı hello şirket içi sanal makine yeniden oluşturur. Bu ayrıca tam veri indirme neden olur.

* Geri tooan alternatif bir konum başarısız olduğunda, kurtarılan toohello hello sanal makine olacaktır aynı ESX konak üzerinde hangi hello ana hedef sunucusu dağıtılır. Merhaba toocreate hello disk kullanılan veri deposu olacaktır hello hello sanal makineyi yeniden korumayı zaman seçilmedi aynı veri deposu.
* Geri yalnızca tooa sanal makine dosya sistemi (VMFS) veri deposu başarısız olabilir. Bir vSAN veya RDM varsa, yeniden koruma ve geri dönme çalışmaz.
* Yeniden koruma hello değişiklikleri tarafından izlenen bir büyük ilk veri aktarımını içerir. Merhaba sanal makine şirket içinde var olmadığından bu işlem bulunmaktadır. Merhaba tam veri geri çoğaltılan toobe gerekir. Bu yeniden koruma ayrıca bir özgün konuma kurtarma daha uzun sürer.
* Diskleri yeniden toovSAN veya RDM tabanlı kapatamazsınız. Yalnızca yeni sanal makine disklerini (VMDKs) VMFS veri deposu üzerinde oluşturulabilir.

Fiziksel makine tooAzure başarısız olduğunda başarısız geri yalnızca bir VMware sanal makinesi olarak (aynı zamanda, başvurulan tooas P2A2V). Bu akış hello alternatif konuma kurtarma altında döner.

* Bir Windows Server 2008 R2 SP1 fiziksel sunucuda korumalı ve tooAzure başarısız geri başarısız olamaz.
* Geri toofail gereken en az bir ana hedef sunucusu ve hello gerekli ESX/ESXi konakları toowhich Bul emin olun.

## <a name="have-you-completed-reprotection"></a>Yükü tamamladınız mı?
Devam etmeden önce tam hello koruyun adımları böylece hello sanal makinelerin çoğaltılmış bir durumda olduğunu ve bir yük devretme geri tooan şirket içi site başlatabilirsiniz. Daha fazla bilgi için bkz: [nasıl tooreprotect Azure tooon içi](site-recovery-how-to-reprotect.md).

## <a name="prerequisites"></a>Ön koşullar

* Bir yeniden çalışma işlemi yaptığınızda, yapılandırma sunucusu şirket içinde gereklidir. Yeniden çalışma sırasında hello sanal makine hello yapılandırma sunucusu veritabanında mevcut olmalıdır veya geri dönme başarılı olmaz. Bu nedenle, sunucunuzun düzenli olarak zamanlanmış yedeklemeler ele emin olun. Bir olağanüstü durum varsa, toorestore hello hello sunucusuyla ihtiyacınız olacak yeniden çalışma toowork için aynı IP adresi.
* Merhaba ana hedef sunucusu yeniden çalışma tetiklemeden önce tüm anlık görüntüleri sahip olmamalıdır.

## <a name="steps-toofail-back"></a>Adımları toofail

> [!IMPORTANT]
> Yeniden başlatmadan önce hello sanal makine yükü tamamladığınızdan emin olun. Merhaba sanal makinelerin korumalı durumda olması gerekir ve durumlarını olmalıdır **Tamam**. Okuma tooreprotect hello sanal makineleri [nasıl tooreprotect](site-recovery-how-to-reprotect.md).

1. Merhaba çoğaltılan öğeler sayfasında, hello sanal makine seçin ve sağ tooselect **planlanmamış yük devretme**.
2. İçinde **onaylayın yük devretme**hello yük devretme yönünden (Azure) doğrulayın ve ardından toouse hello yük devretme için istediğiniz hello kurtarma noktası (son veya hello en son uygulama tutarlı) seçin. Merhaba uygulama tutarlı noktası hello son noktası zamanında ve bazı veri kaybına neden olur.
3. Yük devretme sırasında hello sanal makinelere Azure Site Recovery kapatır. Bu geri dönme beklendiği gibi tamamlandı denetledikten sonra Azure sanal makinelerde hello kapatılmışsa, kontrol edebilirsiniz.

### <a name="toowhat-recovery-point-can-i-fail-back-hello-virtual-machines"></a>toowhat kurtarma noktası geri hello sanal makineler yük devredebilir?

Yeniden çalışma sırasında iki seçenekleri toofail geri hello sanal makine/planlama kurtarma sahip.

Son işlenen hello noktası zamanında seçerseniz, tüm sanal makineleri zamanında tootheir en son kullanılabilir noktası üzerinde devredilir. Durumunda hello kurtarma planı, çoğaltma grubunda her bir sanal makine hello çoğaltma grubunun tooits bağımsız son noktası üzerinde zamanında başarısız olur.

En az bir kurtarma noktası olana kadar bir sanal makine yeniden çalışamazsınız. Tüm sanal makinelerin en az bir kurtarma noktası elde edene kadar bir kurtarma planı geri kapatamazsınız.

> [!NOTE]
> En son kurtarma noktası bir kilitlenme tutarlı kurtarma noktasıdır.

Merhaba uygulama tutarlı bir kurtarma noktası seçerseniz, tek bir sanal makine yeniden çalışma tooits en son kullanılabilir uygulama tutarlı bir kurtarma noktası kurtarır. Bir çoğaltma grubu olan bir kurtarma planı Hello durumda her çoğaltma grubu tooits ortak kullanılabilir kurtarma noktası kurtarır.
Uygulamaları tutarlı kurtarma noktaları arkasında zamanında olabilir ve veri kaybı olabilir unutmayın.

### <a name="what-happens-toovmware-tools-post-failback"></a>Yeniden çalışma tooVMware araçları sonrası ne olur?

Yük devretme tooAzure sırasında hello VMware araçları hello Azure sanal makine üzerinde çalışan olamaz. Yük devretme sırasında hello VMware araçları ASR Windows sanal makine durumunda, devre dışı bırakır. Linux sanal makine durumunda ASR yük devretme sırasında hello VMware araçları kaldırır.

Merhaba Windows sanal makine yeniden çalışma sırasındaki hello VMware araçları yeniden çalışma sırasında yeniden büyük/küçük harf etkinleştiriliyor. Benzer şekilde, bir linux sanal makine için hello VMware araçları hello makinede yeniden çalışma sırasında yeniden yüklenir.

## <a name="next-steps"></a>Sonraki adımlar

Yeniden çalışma sona erdikten sonra toocommit gerekir. Azure sanal makinelerde kurtarılan hello sanal makine tooensure silinir.

### <a name="commit"></a>İşleme
Yürütme gerekli tooremove hello Azure sanal makineden üzerinden başarısız olur.
Korumalı hello öğeyi sağ tıklatın ve ardından **yürütme**. Bir işin azure'da sanal makineler için yük devredildi hello kaldırır.

### <a name="reprotect-from-on-premises-tooazure"></a>Şirket içi tooAzure koruyun

Yürütme sona erdikten sonra sanal makinenize geri hello şirket içi sitede olmakla birlikte korumalı olmaz. toostart tooreplicate tooAzure yeniden hello aşağıdaki:

1. İçinde **kasa** > **ayarı** > **öğeleri çoğaltılan**, select hello geri başarısız olmuş ve ardından sanal makineleri  **Yeniden koruma**.
2. Kullanılan toobe toosend veri tooAzure gereken hello işlem sunucusu Hello değerini verir.
3. Tıklatın **Tamam** toobegin hello yeniden koruma işi.

> [!NOTE]
> Bir şirket içi sanal makine önyükleme sonra tooregister geri toohello yapılandırma sunucusu (yukarı too15 dakika) hello aracısı için biraz zaman alabilir. Bu süre boyunca başarısız olur ve bu hello aracı bildiren bir hata iletisi yüklenmemiş döndürür koruyun. Birkaç dakika bekleyin ve sonra yeniden koruma yeniden deneyin.

Merhaba koruyun sonra işi tamamlanana geri tooAzure hello sanal makinenin çoğaltıldığını ve bir yük devretme yapabilirsiniz.

## <a name="common-issues"></a>Genel sorunlar
Bir yeniden çalışma yapmadan önce bu hello vCenter bağlı durumda olduğundan emin olun. Aksi takdirde, diskleri kesme ve geri toohello ekleyerek sanal makine başarısız olur.
