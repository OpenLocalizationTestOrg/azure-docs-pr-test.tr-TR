---
title: "aaaUpgrade Site Recovery kasası tooan Azure kurtarma Hizmetleri kasası"
description: "Nasıl tooupgrade bir Azure Site Recovery kasası tooa kurtarma Hizmetleri kasası öğrenin"
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a>Site Recovery kasası tooan Azure Resource Manager tabanlı kurtarma Hizmetleri kasası yükseltme

Bu makalede, Azure Site Recovery tooupgrade tooAzure Resource Manager tabanlı kurtarma hizmeti kasalarını devam eden çoğaltma üzerinde hiçbir etkisi olmadan nasıl kasaları açıklanmaktadır. Azure Kaynak Yöneticisi özellikleri ve avantajları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).

## <a name="introduction"></a>Giriş
Kurtarma Hizmetleri kasası, yedekleme ve olağanüstü durum kurtarma hello bulut yerel olarak yönetmek için bir Azure Resource Manager kaynaktır. Merhaba yeni Azure Portalı'nda kullanabileceğiniz birleşik bir kasa olan ve hello Klasik yedekleme değiştirir ve Site Recovery kasaları.

Kurtarma Hizmetleri kasaları dahil olmak üzere özellikleri, bir dizi sunar:

* Azure Resource Manager desteği: korumak ve sanal makineleri ve fiziksel makineler üzerinden bir Azure Resource Manager yığına başarısız.

* Diski dışarıda: geçici dosyalar veya tüm bant toouse istemediğiniz yüksek bir karmaşıklık verileri varsa, birimleri çoğaltma dışında bırakabilirsiniz. Bu özellik şu anda etkin *VMware tooAzure* ve *Hyper-V tooAzure* ve tooother senaryoları genişletilir.

* Premium ve yerel olarak yedekli depolama için destek: artık sunucuları koruyabilir premium depolama alanına müşteriler tooprotect uygulamalarla yüksek izin hesapları giriş/saniye başına işlemi (IOPS) çıkış. Bu özellik şu anda etkin *VMware tooAzure*.

* Hızlandırıldı başlama deneyimi: Gelişmiş hello başlama deneyimi tasarlanmış toomake olağanüstü durum kurtarma Kurulumu kolay.

* Yedekleme ve Site Recovery yönetimden hello aynı Kasa: şimdi olağanüstü durum kurtarma korumak veya hello yedekleme, yönetim yükünü önemli ölçüde azaltabilir aynı kasası.

Hello yükseltilmiş hello deneyimi ve özellikleri hakkında daha fazla bilgi için bkz: [depolama, yedekleme ve kurtarma blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).

## <a name="salient-features"></a>Dikkat çekici özellikleri

* Devam eden çoğaltma üzerindeki etkisi: devam eden çoğaltma sırasında herhangi bir kesintiye uğratmadan devam etmek ve yükseltme sonrası.

* Ek ücret ödemeden: güncelleştirilmiş özellikleri kümesinin tamamını hiçbir ek ücret ödemeden.

* Veri kaybı: Bu işlem, yükseltme ve bir geçiş olduğundan, var olan çoğaltma kurtarma noktalarının ve ayarları sırasında ve hello yükselttikten sonra değişmeden kalır.


## <a name="what-happens-during-hello-vault-upgrade"></a>Merhaba kasası yükseltme sırasında ne olur?

Merhaba yükseltme sırasında yeni bir sunucu kaydetme veya bir sanal makine (VM) için çoğaltma etkinleştirme gibi işlemleri gerçekleştiremezsiniz. Verileri okuma veya yazma korumalı öğelerin toohello kasasının, devam eden çoğaltma gibi veri toohello kasası içeren işlemleri kesintisiz devam edin.

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a>Değişiklikleri tooautomation ve araç hello yükselttikten sonra
Merhaba Klasik dağıtım modeli toohello Resource Manager dağıtım modelinden yükseltme hello kasa türü gibi hello var olan Otomasyon veya onu toowork hello yükseltme sonrasında devam araç tooensure güncelleştirin.

### <a name="prepare-your-environment-for-hello-upgrade"></a>Merhaba yükseltme için ortamınızı hazırlama

* [PowerShell yüklemek veya tooversion 5 veya sonraki sürümünü yükseltme](https://www.microsoft.com/download/details.aspx?id=50395)
* [Azure PowerShell MSI Hello en son sürümünü yükleyin](https://github.com/Azure/azure-powershell/releases)
* [Merhaba kurtarma Hizmetleri kasası yükseltme betiğini indir](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a>Ön koşullar
tooAzure Resource Manager tabanlı kurtarma hizmeti kasalar Site kurtarma'dan tooupgrade kasaları, hello aşağıdaki gereksinimleri karşılamalıdır:

* En düşük aracı sürümü: hello sunucunuzda yüklü Azure Site Recovery sağlayıcısı sürümü 5.1.1700.0 olmalıdır veya sonraki bir sürümü.

* Desteklenen yapılandırma: depolama alanı ağı (SAN) veya SQL Server AlwaysOn Kullanılabilirlik grupları ile kasanızı yapılandıramazsınız. Tüm diğer yapılandırmalar desteklenmez.

    >[!NOTE]
    >Merhaba yükseltmeden sonra depolama eşlemesi yalnızca PowerShell aracılığıyla yönetebilirsiniz.

* Desteklenen dağıtım senaryosu: kasanızı hello olmamalıdır *VMware tooAzure* eski dağıtım modeli. Devam etmeden önce toohello gelişmiş dağıtım modeli taşıyın.

* Yönetimi ile ilgili hiç etkin kullanıcı tarafından başlatılan iş düzlemine işlemleri: hello yükseltilmesini önce erişim toohello yönetim düzlemi yükseltme sırasında sınırlı olduğundan, tüm yönetim düzlemi eylemleri tamamlayın. Bu işlem, devam eden çoğaltmayı içermez.

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

**Bu yükseltme my devam eden çoğaltma etkiliyor mu?**

Hayır. Devam eden çoğaltmayı kesintiye uğramadan sırasında ve hello yükseltme sonrasında devam eder.

**Siteden siteye VPN ve IP ayarları gibi toonetwork ayarları ne olur?**

Merhaba yükseltme hello ağ ayarlarını etkilemez. Tüm Azure-için-şirket içi bağlantılar sürdürülür.

**Yakın zaman hello tooupgrade planlamıyorsanız toomy kasalarını ne olur?**

Eylül 2017 başlangıç hello eski Azure portalında Site Recovery kasası desteği kullanım dışı kalacaktır. Merhaba yükseltme özelliği toomove toohello yeni portalı kullanmanızı öneririz.

**Bu geçiş planı için varolan my araç anlamı nedir?**  

Araç toohello Resource Manager dağıtım modeli güncelleştirmek yükseltme planlarınızı için dikkate almalı hello en önemli değişikliklerden biri kullanılır. Merhaba kurtarma Hizmetleri kasalarının hello Resource Manager dağıtım modeline dayanır. 

**Ne kadar süreyle Yönetim düzeyi kapalı kalma süresi en son hello mu?**

Merhaba yükseltmenin normalde yaklaşık 15 too30 dakika sürer ve tooa bir saatlik maksimum ele geçirebilir.

**I yükselttikten sonra geri alabilirsiniz?**

Hayır. Merhaba kaynakları başarılı bir şekilde yükselttikten sonra geri alma desteklenmiyor.

**Yükseltilebilmesi için olup olmadığını ı my abonelik veya kaynak toosee doğrulayabilirsiniz?**

Evet. Merhaba platformu tarafından desteklenen yükseltme, hello yükseltme ilk adımda hello hello kaynakları yükseltme kapasitesi toovalidate seçenektir. Merhaba doğrulama başarısız olursa, ilgili hata iletisi veya uyarı alırsınız.

**Merhaba yükseltme ile ilgili bir sorunu nasıl bildirebilirim?**

Merhaba yükseltme sırasında hatalar karşılaşırsanız, hello hata listelenen hello işlem kimliği unutmayın. Microsoft Support hello sorunu çözümlemek için proaktif olarak çalışır. Merhaba Destek ekibiyle abonelik kimliği, kasa adını ve işlem kimliği de başvurabilirsiniz Destek tooresolve hello sorunu mümkün olan en kısa sürede çalışır. Açıkça belirtildiği toodo olmadıkça hello işlemi yeniden deneyin değil Microsoft tarafından bunu.

## <a name="run-hello-script"></a>Merhaba komut dosyasını çalıştır

PowerShell'de hello aşağıdaki komutu çalıştırın:

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* Subscriptionıd: yükseltme yapıyorsanız hello kasayla ilişkili hello abonelik kimliği.

* VaultName: yükseltme yapıyorsanız hello kasa hello adı.

* Konumu: yükseltme yapıyorsanız hello kasası başlangıç konumu.

* ResourceType: Site Recovery için HyperVRecoveryManagerVault kasaları.

* TargetResourceGroupName: hello istediğiniz hello kaynak grubu yerleştirilen kasa toobe yükseltildi. Azure Resource Manager veya yeni bir tane var olan bir kaynak grubunda TargetResourceGroupName olabilir. Merhaba sağlanan TargetResourceGroupName mevcut değilse hello yükseltmesinin bir parçası hello aynı oluşturulduğu konumu hello kasası olarak. Daha fazla bilgi için hello "Kaynak grupları" bölümüne bakın [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md#resource-groups).

    >[!NOTE]
    >Kaynak grubu adlandırma konu toocertain kısıtlamaları edilir. tooprevent kasa yükseltme hatası, adlandırma emin tooobserve hello dikkatli olun.
    >
    >Örneğin:
    >
    >.\RecoveryServicesVaultUpgrade-1.0.0.ps1 - Subscriptionıd 1234-54123-354354-56416-8645 - VaultName gen2dr-konum "Kuzey Avrupa" - ResourceType hypervrecoverymanagervault - TargetResourceGroupName abc

Alternatif olarak, komut dosyası izleyen hello çalıştırabilirsiniz. Merhaba değerleri gerekli hello parametrelerini girin.

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. Merhaba PowerShell komut dosyası, tooenter kimlik bilgilerinizi ister. Bunları, iki kez hello Klasik dağıtım modeli hesabı için bir kez ve bir kez hello Azure Resource Manager hesabı girin.

2. Kimlik bilgilerinizi girdikten sonra altyapı Kurulum karşılıyor hello gereksinimleri daha önce bahsedilen bakılmaksızın hello betik onay toodetermine çalışır.

3. Hello önkoşulları işaretli ve onaylandıktan sonra istendiğinde tooproceed hello kasası yükseltme işlemine olursunuz. Merhaba yükseltme işlemi kasanızı yükseltmeyi başlatır. Merhaba tüm yükseltme 15 too30 dakika toocomplete alabilir.

4. Hello Yükseltme başarıyla tamamlandıktan sonra hello yükseltilmiş kasaya hello yeni Azure portalına erişebilir.

## <a name="post-upgrade-vault-management"></a>Yükseltme sonrası kasa yönetimi

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a>Kurtarma Hizmetleri kasası hello Azure Site Recovery kullanarak çoğaltma

* Bu gibi durumlarda, Azure Vm'leriniz artık tek bir bölge tooanother koruyabilirsiniz. Daha fazla bilgi için bkz: [Azure Site Recovery ile bölgeler arasında Azure sanal makineleri çoğaltmak](site-recovery-azure-to-azure.md).

* VMware Vm'lerini tooAzure çoğaltma hakkında daha fazla bilgi için bkz: [Site Recovery ile çoğaltmak VMware Vm'lerini tooAzure](vmware-walkthrough-overview.md).

* Hyper-V Vm'lerini (VMM olmadan) tooAzure çoğaltma hakkında daha fazla bilgi için bkz: [çoğaltmak Hyper-V sanal makineleri (VMM olmadan) tooAzure](hyper-v-site-walkthrough-overview.md).

* Hyper-V Vm'lerini (VMM ile) tooAzure çoğaltma hakkında daha fazla bilgi için bkz: [çoğaltmak Hyper-V sanal makineleri Site RECOVERY'yi kullanarak VMM Bulutları tooAzure içinde hello Azure portal](vmm-to-azure-walkthrough-overview.md).

* Hyper-Vm'lerini (VMM ile) tooa ikincil siteye çoğaltma hakkında daha fazla bilgi için bkz: [VMM Bulutları tooa ikincil VMM sitesi kullanarak Hyper-V çoğaltma sanal makineleri hello Azure portal](site-recovery-vmm-to-vmm.md).

* VMware Vm'lerini tooa ikincil siteye çoğaltma hakkında daha fazla bilgi için bkz: [Replicate şirket içi VMware sanal makineleri veya fiziksel sunucuları tooa ikincil site hello Klasik Azure portalında](site-recovery-vmware-to-vmware.md).

### <a name="view-your-replicated-items"></a>Çoğaltılmış öğelerinizi görüntüleme

Merhaba aşağıdaki görüntüde hello kasa için anahtar varlıklar görüntüler hello kurtarma Hizmetleri kasası Pano sayfası gösterilir. tooview hello kasadaki korunan varlıklar listesi seçin **Site Recovery** > **öğeleri çoğaltılan**.


![Çoğaltılan öğe](./media/upgrade-site-recovery-vaults/replicateditems.png)

Merhaba aşağıdaki görüntüde çoğaltılan öğeler ve hello görüntüleme hello iş akışı gösterilmektedir **yük devretme** bir yük devretmeyi başlatmadan için komutu.

![Çoğaltılan öğe](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a>Çoğaltma ayarlarınızı görüntüleyin

Merhaba Site kurtarma kasasına her koruma grubu kopyalama sıklığı, kurtarma noktası bekletme, uygulama ile tutarlı anlık görüntü sıklığı ve diğer çoğaltma ayarları ile yapılandırılır. Merhaba kurtarma Hizmetleri kasasına bu ayarları bir çoğaltma ilkesi yapılandırılır. Merhaba hello İlkesi adıdır hello hello koruma grubu adı veya hello *primarycloud_Policy*.

Çoğaltma İlkesi hakkında daha fazla bilgi için bkz: [VMware tooAzure için çoğaltma ilkesini yönetme](site-recovery-setup-replication-settings-vmware.md).
