---
title: "Hyper-V çoğaltma tooAzure Site Recovery işlerinde aaaHow mu? | Microsoft Belgeleri"
description: "Bu makalede, Hyper-V çoğaltmasının Azure Site Recovery’de nasıl çalıştığına dair genel bir bakış sağlanmaktadır"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-architecture-hyper-v-to-azure
ms.openlocfilehash: e982806b4d6cdec2f71f82d8c73c17cc50ad3c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-hyper-v-replication-tooazure-work"></a>Hyper-V çoğaltma tooAzure nasıl çalışır?

Bu makale toounderstand hello mimarisi ve Hyper-V çoğaltma tooAzure hello kullanarak iş akışları okuma [Azure Site Recovery](site-recovery-overview.md) hizmet.

Bu makalenin veya hello hello altındaki tüm yorumlar sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

TooAzure aşağıdaki hello çoğaltabilirsiniz:
- **VMM ile Hyper-V**: System Center Virtual MAchine Manager (VMM) bulutlarında yönetilen şirket içi Hyper-V ana bilgisayarlarında yer alan VM'ler. Ana bilgisayarlar, [desteklenen herhangi bir işletim sistemini](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers) çalıştırıyor olabilir. [Hyper-V ve Azure tarafından desteklenen](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) herhangi bir konuk işletim sistemini çalıştıran Hyper-V VM’lerini çoğaltabilirsiniz.
- **VMM olmadan Hyper-V**: VMM bulutlarında yönetilmeyen Hyper-V ana bilgisayarlarında bulunan şirket içi VM’ler. Konaklar hello hiçbirini çalıştırabilirsiniz [desteklenen işletim sistemleri](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). [Hyper-V ve Azure tarafından desteklenen](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) herhangi bir konuk işletim sistemini çalıştıran Hyper-V VM’lerini çoğaltabilirsiniz.


## <a name="architectural-components"></a>Mimari bileşenler

**Alan** | **Bileşen** | **Ayrıntılar**
--- | --- | ---
**Azure** | Azure’da bir Microsoft Azure hesabına, bir Azure depolama hesabına ve bir Azure ağına ihtiyacınız vardır. | Depolama ve ağ, Kaynak Yöneticisi tabanlı veya klasik hesaplar olabilir.<br/><br/> Çoğaltılan veriler hello depolama hesabında depolanır ve şirket içi sitenizdeki yük devretme durumunda Azure Vm'leri çoğaltılan hello verilerle oluşturulur.<br/><br/> Hello Azure VM'ler, oluşturuldukları zaman toohello Azure sanal ağı bağlayın.
**VMM sunucusu** | VMM bulutlarında bulunan Hyper-V ana bilgisayarları | VMM bulutlarındaki Hyper-V konakları yönetiliyorsa, Kurtarma Hizmetleri kasası hello hello VMM sunucusunu kaydedin.<br/><br/> Merhaba VMM sunucusuna Azure ile Merhaba Site kurtarma sağlayıcısı tooorchestrate çoğaltma yükleyin.<br/><br/> VM ağları tooconfigure ağ eşlemesi ayarlamanız ve mantıksal gerekir. Bir VM ağı hello bulutla ilişkilendirilen mantıksal ağ bağlantılı tooa olmalıdır.
**Hyper-V konağı** | Hyper-V sunucuları VMM sunucusu ile veya sunucu olmadan dağıtılabilir. | VMM sunucusu yoksa üzerinden Site Recovery ile Merhaba konak tooorchestrate çoğaltma üzerindeki Site Recovery sağlayıcısı yüklü hello Internet hello. Bir VMM sunucusu ise, hello sağlayıcısı üzerindeki ve hello konaktaki yüklenir.<br/><br/> Merhaba kurtarma Hizmetleri Aracısı hello konak toohandle veri çoğaltmayı yüklenir.<br/><br/> Merhaba sağlayıcısı ve hello Aracısı gelen iletişimler güvenli ve şifrelidir. Azure depolama alanında çoğaltılan veriler de şifrelenir.
**Hyper-V VM’leri** | Hello Hyper-V konak sunucusunda bir veya daha fazla VM gerekir. | Hiçbir şey Vm'lere yüklü tooexplicitly gerekiyor

## <a name="deployment-steps"></a>Dağıtım adımları

1. **Azure**: Azure bileşenleri hello ayarlayın. Site Recovery dağıtımına başlamadan önce depolama ve ağ hesapları ayarlamanızı öneririz.
2. **Kasa**: Site Recovery için bir Kurtarma Hizmetleri kasası oluşturun ve kaynak ile hedef ayarlarını yapılandırma, bir çoğaltma ilkesi ayarlama ve çoğaltmayı etkinleştirilme de dahil olmak üzere kasa ayarlarını yapılandırın.
3. **Kaynak ve hedef**:
    - **VMM bulutlarındaki Hyper-V konakları**: parçası olarak, kaynak ayarlarını belirtme, indirin ve hello Azure Site Recovery sağlayıcısı hello VMM sunucusunu ve her Hyper-V ana bilgisayarda hello Azure kurtarma Hizmetleri aracısını yükleyin. Merhaba kaynak hello VMM sunucusu olacaktır. Merhaba, Azure hedefidir.
    - Hyper-V konakları VMM olmadan: kaynak ayarları belirttiğinizde, yükleyip hello sağlayıcı ve aracı her Hyper-V ana bilgisayarda. Dağıtımı sırasında Hyper-V siteye hello ana bilgisayarları toplayın ve bu site hello kaynağı olarak belirtin. Merhaba, Azure hedefidir.

    ![Hyper-V/VMM çoğaltma tooAzure](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png) ![Hyper-V sitesi çoğaltma tooAzure](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)


4. **Çoğaltma İlkesi**: hello Hyper-V sitesi veya VMM bulutu için bir çoğaltma ilkesi oluşturun. Merhaba, uygulanan tooall VM'ler hello site veya Bulut ana bilgisayar üzerindeki ilkesidir.
5. **Çoğaltmayı etkinleştir**: Hyper-V VM’leri için çoğaltmayı etkinleştir. İlk çoğaltma hello Çoğaltma İlkesi ayarlarına uygun şekilde gerçekleştirilir. Veri değişiklikleri izlenir ve delta değişiklikleri tooAzure çoğaltmasını hello ilk çoğaltma sonlandırıldıktan sonra başlar. Bir öğe için izlenen değişiklikler bir .hrl dosyasında saklanır.
6. **Yük devretme sınamasını**: bir test yük devretme toomake her şeyi çalıştığını beklendiği gibi emin çalıştırın.

Dağıtım hakkında daha fazla bilgi edinin:
- [Hyper-V VM çoğaltma tooAzure - VMM ile kullanmaya başlama](site-recovery-vmm-to-azure.md)
- [Hyper-V VM çoğaltma tooAzure - VMM olmadan kullanmaya başlama](site-recovery-hyper-v-site-to-azure.md)

## <a name="hyper-v-replication-workflow"></a>Hyper-V çoğaltma iş akışı

### <a name="enable-protection"></a>Korumayı etkinleştir

1. Hyper-V sanal makine için koruma etkinleştirildikten sonra Azure portalına veya şirket içi, hello hello **korumayı etkinleştir** başlatır.
2. Merhaba iş o hello makine hello çağırmadan önce önkoşulları ile uyumlu denetler [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), yapılandırdığınız hello ayarlarla çoğaltma tooset.
3. Merhaba işini hello çağırarak ilk çoğaltmayı başlatır [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) yöntemi, tam bir VM çoğaltmasını tooinitialize ve gönderme hello sanal makinenin sanal diskleri tooAzure.
4. Merhaba hello işinde izleyebilirsiniz **işleri** sekmesi.      ![İşler listesi](media/site-recovery-hyper-v-azure-architecture/image1.png) ![Korumayı etkinleştir ayrıntıları](media/site-recovery-hyper-v-azure-architecture/image2.png)

### <a name="initial-replication"></a>İlk çoğaltma

1. İlk çoğaltma tetiklendiğinde bir [Hyper-V VM anlık görüntüsü](https://technet.microsoft.com/library/dd560637.aspx) alınır.
2. Tüm kopyalanan tooAzure oluncaya kadar sanal sabit diskler çoğaltılır ' dir. Merhaba VM boyutuna bağlı olarak uzun sürebilir ve ağ bant genişliği. toooptimize, ağ kullanımınızı bkz [nasıl toomanage tooAzure koruma ağ bant genişliği kullanımını içi](https://support.microsoft.com/kb/3056159).
3. İlk çoğaltma işlemi devam ederken disk değişimi meydana gelirse hello Hyper-V çoğaltma çoğaltma İzleyicisi bu değişiklikleri Hyper-V çoğaltma günlükleri (.hrl) izler. Bu dosyalar hello bulunur hello diskleri aynı klasöre. Her diskin toosecondary depolama gönderilecek bir ilişkili .hrl dosyası vardır.
4. ilk çoğaltma işlemi devam ederken hello anlık görüntü ve günlük dosyalarının disk kaynaklarını tüketebilir.
5. Merhaba ilk çoğaltma tamamlandığında hello VM anlık görüntüsü silinir. Değişim diski değişiklikleri hello günlüğünde eşitlenmesi ve birleştirilmiş toohello üst disk var.


### <a name="finalize-protection"></a>Korumayı sonlandırma

1. Merhaba ilk çoğaltma, hello bittikten sonra **hello sanal makinede korumayı Sonlandır** işi, ağ ve diğer çoğaltma sonrası ayarlarını hello sanal makine korunuyor böylece yapılandırır.
    ![Korumayı sonlandır işi](media/site-recovery-hyper-v-azure-architecture/image3.png)
2. TooAzure çoğaltıyorsanız, böylece yük devretme için hazır tootweak hello ayarları hello sanal makine için gerekebilir. Bu noktada, her şeyin beklendiği gibi çalıştığını test yük devretme toocheck çalıştırabilirsiniz.

### <a name="delta-replication"></a>Değişim çoğaltması

1. Merhaba ilk çoğaltma sonrasında delta eşitleme, çoğaltma ayarlarına uygun şekilde başlar.
2. Merhaba Hyper-V çoğaltma çoğaltma İzleyicisi Merhaba değişiklikleri tooa sanal sabit disk .hrl dosyası izler. Çoğaltma için yapılandırılmış her diskin ilişkili bir .hrl dosyası vardır. İlk çoğaltma tamamlandıktan sonra bu günlük toohello müşterinin depolama hesabı gönderilir. Bir günlük transit tooAzure olduğunda, hello değişiklikler hello birincil diski başka bir günlük dosyasında, hello izlenir aynı dizin.
3. Başlangıç ve değişim çoğaltma sırasında VM hello hello VM görünüm izleyebilirsiniz. [Daha fazla bilgi edinin](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="replication-synchronization"></a>Çoğaltma eşitleme

1. Değişim çoğaltması başarısız olursa ve bant genişliği ile zaman açısından tam çoğaltma maliyetli olacaksa, bir VM yeniden eşitleme için işaretlenir. Merhaba .hrl dosyası hello disk boyutunun % 50 ulaştıysanız, örneğin, ardından hello VM yeniden eşitleme için işaretlenir.
2.  Yeniden eşitleme hello hello kaynak ve hedef sanal makine sağlama bilgi işlem ve yalnızca hello değişim verileri gönderme gönderilen veri miktarını azaltır. Yeniden eşitleme, kaynak ve hedef dosyaların sabit öbeklere bölündüğü bir sabit blok kümeleme algoritması kullanır. Her bir öbeğin sağlama oluşturulur ve hello kaynak gerek toobe uygulanan toohello hedeften engeller toodetermine karşılaştırılan.
3. Yeniden eşitleme sona erdikten sonra, normal değişim çoğaltması devam edecektir. Varsayılan olarak yeniden eşitleme ofis saatleri dışında otomatik olarak zamanlanan toorun olmakla birlikte, bir sanal makineyi el ile eşitleyebilirsiniz. Örneğin, bir ağ kesintisi veya başka bir kesinti oluşursa, yeniden eşitlemeyi devam ettirebilirsiniz. toodo hello portal Bu, select hello VM > **eşitlemek**.

    ![El ile yeniden eşitleme](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retries"></a>Yeniden deneme sayısı

Bir çoğaltma hatası meydana gelirse, yerleşik yeniden deneme işlevi vardır. Bu mantık iki kategoride sınıflandırılabilir:

**Kategori** | **Ayrıntılar**
--- | ---
**Kurtarılamaz hatalar** | Yeniden deneme yapılmaya çalışılmaz. VM durumu **Kritik** olacaktır ve yönetici müdahalesi gerekir. Bu hataların örnekler: VHD zinciri; bozuk Geçersiz durum hello çoğaltma VM için; Ağ kimlik doğrulama hataları: Yetkilendirme hataları; VM hataları (tek başına Hyper-V sunucuları için) bulunamadı
**Kurtarılabilir hatalar** | Yeniden deneme bir üstel geri hello yeniden deneme aralığı 1, 2, 4, 8 ilk denemede hello hello başından ve 10 dakika artan dışı kullanarak, her bir çoğaltma aralığı oluşur. Hata devam ederse, 30 dakikada bir yeniden deneyin. Örnekler şunlardır: ağ hataları; düşük disk hataları; yetersiz bellek durumları |

## <a name="protection-and-recovery-lifecycle"></a>Koruma ve kurtarma yaşam döngüsü

![iş akışı](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

## <a name="next-steps"></a>Sonraki adımlar

- [Dağıtım önkoşullarını denetleme](site-recovery-prereq.md)
- Aşağıdakilerle sorun giderme:
    - [Koruma izleme ve sorun giderme](site-recovery-monitoring-and-troubleshooting.md)
    - [Microsoft destekten yardım](site-recovery-monitoring-and-troubleshooting.md#reach-out-for-microsoft-support)
    - [Genel sorunlar ve çözümleri](site-recovery-monitoring-and-troubleshooting.md#common-azure-site-recovery-errors-and-their-resolutions)
