---
title: "Azure Site kurtarma Hyper-V çoğaltma tooAzure iş aaaHow mu? | Microsoft Belgeleri"
description: "Bu makalede, bileşenleri ve çoğaltma Hyper-V sanal makineleri tooAzure hello Azure Site Recovery hizmeti ile şirket içi kullanılan mimarisi genel bakış sağlar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 3b64156307f37764a8315dec68cf297acf279530
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-hyper-v-replication-tooazure-work-in-site-recovery"></a>Hyper-V çoğaltma tooAzure Site Recovery nasıl çalışır?


Bu makalede hello bileşenleri açıklar ve işlemler çoğaltırken söz konusu şirket içi Hyper-V sanal makineleri, hello kullanarak tooAzure [Azure Site Recovery](site-recovery-overview.md) hizmet.

Site Recovery, System Center Virtual Machine Manager (VMM) ile veya VMM olmadan yönetilen Hyper-V kümelerindeki ve bağımsız konaklardaki Hyper-V VM'lerini çoğaltabilir.

Bu makalenin veya hello hello altındaki tüm yorumlar sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Mimari bileşenler

Bir dizi bileşen dahil olan Hyper-V sanal makineleri tooAzure çoğaltırken.

**Bileşen** | **Konum** | **Ayrıntılar**
--- | --- | ---
**Azure** | Azure’da bir Microsoft Azure hesabına, bir Azure depolama hesabına ve bir Azure ağına ihtiyacınız vardır. | Çoğaltılan veriler hello depolama hesabında depolanır ve şirket içi sitenizdeki yük devretme durumunda Azure Vm'leri çoğaltılan hello verilerle oluşturulur.<br/><br/> Hello Azure VM'ler, oluşturuldukları zaman toohello Azure sanal ağı bağlayın.
**VMM sunucusu** | Hyper-V konakları VMM bulutlarında bulunur | VMM bulutlarındaki Hyper-V konakları yönetiliyorsa, Kurtarma Hizmetleri kasası hello hello VMM sunucusunu kaydedin.<br/><br/> Merhaba VMM sunucusuna Azure ile Merhaba Site kurtarma sağlayıcısı tooorchestrate çoğaltma yükleyin.<br/><br/> VM ağları tooconfigure ağ eşlemesi ayarlamanız ve mantıksal gerekir. Bir VM ağı hello bulutla ilişkilendirilen mantıksal ağ bağlantılı tooa olmalıdır.
**Hyper-V konağı** | Hyper-V konakları ve kümeleri, VMM sunucusu ile veya sunucu olmadan dağıtılabilir. | VMM sunucusu yoksa üzerinden Site Recovery ile Merhaba konak tooorchestrate çoğaltma üzerindeki Site Recovery sağlayıcısı yüklü hello Internet hello. Bir VMM sunucusu ise, hello sağlayıcısı üzerindeki ve hello konaktaki yüklenir.<br/><br/> Merhaba kurtarma Hizmetleri Aracısı hello konak toohandle veri çoğaltmayı yüklenir.<br/><br/> Merhaba sağlayıcısı ve hello Aracısı gelen iletişimler güvenli ve şifrelidir. Azure depolama alanında çoğaltılan veriler de şifrelenir.
**Hyper-V VM’leri** | Hyper-V konak sunucusunda çalışan bir veya daha fazla VM'nizin olması gerekir. | Hiçbir şey Vm'lere yüklü tooexplicitly gerekir.

Merhaba dağıtımının önkoşulları ve hello de bu bileşenlerin her birini gereksinimleri hakkında bilgi edinin [destek matrisi](site-recovery-support-matrix-to-azure.md).

**Şekil 1: Hyper-V sitesi tooAzure çoğaltma**

![Bileşenler](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**Şekil 2: Hyper-V, VMM Bulutları tooAzure çoğaltma**

![Bileşenler](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replication-process"></a>Çoğaltma işlemi

**Şekil 3: Hyper-V çoğaltma tooAzure için çoğaltma ve kurtarma işlemi**

![iş akışı](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a>Korumayı etkinleştir

1. Hyper-V sanal makine için koruma etkinleştirildikten sonra Azure portalına veya şirket içi, hello hello **korumayı etkinleştir** başlatır.
2. Merhaba iş o hello makine hello çağırmadan önce önkoşulları ile uyumlu denetler [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), yapılandırdığınız hello ayarlarla çoğaltma tooset.
3. Merhaba işini hello çağırarak ilk çoğaltmayı başlatır [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) yöntemi, tam bir VM çoğaltmasını tooinitialize ve gönderme hello sanal makinenin sanal diskleri tooAzure.
4. Merhaba hello işinde izleyebilirsiniz **işleri** sekmesi.      ![İşler listesi](media/site-recovery-hyper-v-azure-architecture/image1.png) ![Korumayı etkinleştir ayrıntıları](media/site-recovery-hyper-v-azure-architecture/image2.png)

### <a name="replicate-hello-initial-data"></a>Merhaba ilk veri çoğaltma

1. İlk çoğaltma tetiklendiğinde bir [Hyper-V VM anlık görüntüsü](https://technet.microsoft.com/library/dd560637.aspx) alınır.
2. Tüm kopyalanan tooAzure oluncaya kadar sanal sabit diskler çoğaltılır ' dir. Merhaba VM boyutuna bağlı olarak uzun sürebilir ve ağ bant genişliği. toooptimize, ağ kullanımınızı bkz [nasıl toomanage tooAzure koruma ağ bant genişliği kullanımını içi](https://support.microsoft.com/kb/3056159).
3. İlk çoğaltma işlemi devam ederken disk değişimi meydana gelirse hello Hyper-V çoğaltma çoğaltma İzleyicisi bu değişiklikleri Hyper-V çoğaltma günlükleri (.hrl) izler. Bu dosyalar hello bulunur hello diskleri aynı klasöre. Her diskin toosecondary depolama gönderilecek bir ilişkili .hrl dosyası vardır.
4. ilk çoğaltma işlemi devam ederken hello anlık görüntü ve günlük dosyalarının disk kaynaklarını tüketebilir.
5. Merhaba ilk çoğaltma tamamlandığında hello VM anlık görüntüsü silinir. Değişim diski değişiklikleri hello günlüğünde eşitlenmesi ve birleştirilmiş toohello üst disk var.


### <a name="finalize-protection"></a>Korumayı sonlandırma

1. Merhaba ilk çoğaltma, hello bittikten sonra **hello sanal makinede korumayı Sonlandır** işi, ağ ve diğer çoğaltma sonrası ayarlarını hello sanal makine korunuyor böylece yapılandırır.
    ![Korumayı sonlandır işi](media/site-recovery-hyper-v-azure-architecture/image3.png)
2. TooAzure çoğaltıyorsanız, böylece yük devretme için hazır tootweak hello ayarları hello sanal makine için gerekebilir. Bu noktada, her şeyin beklendiği gibi çalıştığını test yük devretme toocheck çalıştırabilirsiniz.

### <a name="replicate-hello-delta"></a>Merhaba delta Çoğalt

1. Merhaba ilk çoğaltma sonrasında delta eşitleme, çoğaltma ayarlarına uygun şekilde başlar.
2. Merhaba Hyper-V çoğaltma çoğaltma İzleyicisi Merhaba değişiklikleri tooa sanal sabit disk .hrl dosyası izler. Çoğaltma için yapılandırılmış her diskin ilişkili bir .hrl dosyası vardır. İlk çoğaltma tamamlandıktan sonra bu günlük toohello müşterinin depolama hesabı gönderilir. Bir günlük transit tooAzure olduğunda, hello değişiklikler hello birincil diski başka bir günlük dosyasında, hello izlenir aynı dizin.
3. Başlangıç ve değişim çoğaltma sırasında VM hello hello VM görünüm izleyebilirsiniz. [Daha fazla bilgi edinin](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="synchronize-replication"></a>Çoğaltmayı senkronize etme

1. Değişim çoğaltması başarısız olursa ve bant genişliği ile zaman açısından tam çoğaltma maliyetli olacaksa, bir VM yeniden eşitleme için işaretlenir. Merhaba .hrl dosyası hello disk boyutunun % 50 ulaştıysanız, örneğin, ardından hello VM yeniden eşitleme için işaretlenir.
2.  Yeniden eşitleme hello hello kaynak ve hedef sanal makine sağlama bilgi işlem ve yalnızca hello değişim verileri gönderme gönderilen veri miktarını azaltır. Yeniden eşitleme, kaynak ve hedef dosyaların sabit öbeklere bölündüğü bir sabit blok kümeleme algoritması kullanır. Her bir öbeğin sağlama oluşturulur ve hello kaynak gerek toobe uygulanan toohello hedeften engeller toodetermine karşılaştırılan.
3. Yeniden eşitleme sona erdikten sonra, normal değişim çoğaltması devam edecektir. Varsayılan olarak yeniden eşitleme ofis saatleri dışında otomatik olarak zamanlanan toorun olmakla birlikte, bir sanal makineyi el ile eşitleyebilirsiniz. Örneğin, bir ağ kesintisi veya başka bir kesinti oluşursa, yeniden eşitlemeyi devam ettirebilirsiniz. toodo hello portal Bu, select hello VM > **eşitlemek**.

    ![El ile yeniden eşitleme](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retry-logic"></a>Yeniden deneme mantığı

Bir çoğaltma hatası meydana gelirse, yerleşik yeniden deneme işlevi vardır. Bu mantık iki kategoride sınıflandırılabilir:

**Kategori** | **Ayrıntılar**
--- | ---
**Kurtarılamaz hatalar** | Yeniden deneme yapılmaya çalışılmaz. VM durumu **Kritik** olacaktır ve yönetici müdahalesi gerekir. Bu hataların örnekler: VHD zinciri; bozuk Geçersiz durum hello çoğaltma VM için; Ağ kimlik doğrulama hataları: Yetkilendirme hataları; VM hataları (tek başına Hyper-V sunucuları için) bulunamadı
**Kurtarılabilir hatalar** | Yeniden deneme bir üstel geri hello yeniden deneme aralığı 1, 2, 4, 8 ilk denemede hello hello başından ve 10 dakika artan dışı kullanarak, her bir çoğaltma aralığı oluşur. Hata devam ederse, 30 dakikada bir yeniden deneyin. Örnekler şunlardır: ağ hataları; düşük disk hataları; yetersiz bellek durumları |



## <a name="failover-and-failback-process"></a>Yük devretme ve yeniden çalışma işlemi

1. Planlanmış çalıştırabilirsiniz veya planlanmamış [yük devretme](site-recovery-failover.md) şirket içi Hyper-V sanal makineleri tooAzure gelen. Planlanmış bir yük devretme çalıştırın, sonra kaynak VM'ler tooensure kapatın, veri kaybı.
2. Üzerinde tek bir makine başarısız veya oluşturma [kurtarma planlarına](site-recovery-create-recovery-plans.md) birden fazla makine tooorchestrate yük devretme.
4. Merhaba yük devretme çalıştırdıktan sonra çoğaltma sanal makineleri Azure üzerinde oluşturulan mümkün toosee hello olmalıdır. Gerekli olursa, ortak bir IP adresi toohello VM atayabilirsiniz.
5. Ardından Azure VM hello çoğaltmasından hello iş yükü erişme hello yük devretme toostart yürüttükten.
6. Birincil yerinde siteniz yeniden kullanılabilir olduğunda siteyi [yeniden çalıştırabilirsiniz](site-recovery-failback-from-azure-to-hyper-v.md). Planlanmış bir yük devretme Azure toohello birincil siteden kapalı tetiklersiniz. Yapabilecekleriniz planlanmış bir yük devretme için aynı VM veya tooan alternatif konumu ve eşitleme select toofailback toohello veri kaybı Azure ve şirket içi, tooensure arasında değişir. Şirket içi sanal makineleri oluştururken hello yük devretme uygulayın.




## <a name="next-steps"></a>Sonraki adımlar

Gözden geçirme hello [destek matrisi](site-recovery-support-matrix-to-azure.md)
