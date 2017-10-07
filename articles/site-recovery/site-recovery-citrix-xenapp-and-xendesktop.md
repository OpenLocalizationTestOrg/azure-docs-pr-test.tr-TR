---
title: "Azure Site Recovery kullanarak çok katmanlı Citrix XenDesktop ve XenApp dağıtım aaaReplicate | Microsoft Docs"
description: "Bu makalede nasıl Azure Site Recovery kullanarak tooprotect ve kurtarma Citrix XenDesktop ve XenApp dağıtımları."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a>Azure Site Recovery kullanarak çok katmanlı Citrix XenApp ve XenDesktop dağıtım Çoğalt

## <a name="overview"></a>Genel Bakış

Citrix XenDesktop masaüstleri ve uygulamalar bir ondemand hizmet tooany kullanıcısı olarak, herhangi bir yere teslim eden bir Masaüstü Sanallaştırma çözümüdür. FlexCast teslim teknolojisiyle XenDesktop hızlı ve güvenli bir şekilde uygulamalar ve Masaüstü toousers sunabilir.
Bugün, Citrix XenApp herhangi olağanüstü durum kurtarma özellikleri sağlamaz.

İyi olağanüstü durum kurtarma çözümü kurtarma planları hello geçici modelleme karmaşık uygulama mimarilerindeki izin ver ve bu nedenle sağlayan çeşitli katmanları arasındaki hello özelliği özelleştirilmiş tooadd adımları toohandle uygulama eşlemeleri de bir tek çözüm hello tooa önde gelen bir olağanüstü durumda görüntüsü tıklatma emin RTO düşürün.

Bu belge, Hyper-V ve VMware vSphere platformlarda Citrix XenApp dağıtımları için şirket içi olağanüstü durum kurtarma çözümü oluşturmak için adım adım yönergeler sağlar. Ayrıca bu belgede açıklanan nasıl tooperform yük devretme testi (olağanüstü durum kurtarma ayrıntıya) ve kurtarma planları, hello desteklenen yapılandırmalar ve önkoşullar kullanarak planlanmamış yük devretme tooAzure.


## <a name="prerequisites"></a>Ön koşullar

Başlamadan önce hello aşağıdaki anladığınızdan emin olun:

1. [Bir sanal makine tooAzure çoğaltma](site-recovery-vmware-to-azure.md)
1. Nasıl çok[kurtarma ağını tasarlama](site-recovery-network-design.md)
1. [Bir test yük devretme tooAzure yapılması](site-recovery-test-failover-to-azure.md)
1. [Bir yük devretme tooAzure yapılması](site-recovery-failover.md)
1. Nasıl çok[bir etki alanı denetleyicisi çoğaltma](site-recovery-active-directory.md)
1. Nasıl çok[SQL Server çoğaltma](site-recovery-sql.md)

## <a name="deployment-patterns"></a>Dağıtım modelleri

Citrix XenApp ve XenDesktop grubu genel dağıtım desen aşağıdaki hello sahiptir:

**Dağıtım modeli**

Citrix XenApp ve XenDesktop dağıtımı ile AD DNS sunucusu, SQL veritabanı sunucusu, Citrix teslim denetleyicisi mağaza sunucusu XenApp ana (VDA), Citrix XenApp lisans

![Dağıtım modeli 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a>Site kurtarma desteği

Merhaba amacı, bu makalenin için VMware sanal makineleri Citrix dağıtımlarında 6.0 vSphere tarafından yönetilen / System Center VMM 2012 R2 olan kullanılan toosetup DR.

### <a name="source-and-target"></a>Kaynak ve hedef

**Senaryo** | **tooa ikincil site** | **tooAzure**
--- | --- | ---
**Hyper-V** | Kapsamda değil | Evet
**VMware** | Kapsamda değil | Evet
**Fiziksel sunucu** | Kapsamda değil | Evet

### <a name="versions"></a>Sürümler
Müşteriler XenApp bileşenlerini Hyper-V veya VMware üzerinde çalışan sanal makineleri veya fiziksel sunucuları olarak dağıtabilirsiniz. Azure Site Recovery hem fiziksel ve sanal dağıtımları tooAzure koruyabilirsiniz.
Azure'da XenApp 7.7 veya sonraki desteklenen olduğundan, yalnızca bu sürümleri dağıtımlar olağanüstü durum kurtarma veya geçiş için tooAzure çalışılabilir.

### <a name="things-tookeep-in-mind"></a>Şeyler tookeep unutmayın

1. Koruma ve kurtarma şirket içi sunucu işletim sistemi makineler toodeliver kullanarak XenApp yayımlanan uygulama ve XenApp yayımlanan Masaüstü dağıtımları desteklenir.

2. Koruma ve Windows 10 ' da dahil olmak üzere istemci sanal masaüstleri için masaüstü işletim sistemi makineler toodeliver Masaüstü VDI kullanarak şirket içi dağıtımları kurtarma desteklenmez. ASR Masaüstü OS'es makinelerle hello kurtarılmasını desteklemediğinden budur.  Ayrıca, bazı istemci sanal masaüstü (ör. flavours Windows 7), Azure'da lisans için henüz desteklenmiyor. Azure’da istemci/sunucu masaüstlerini lisanslama hakkında [daha fazla bilgi edinin](https://azure.microsoft.com/pricing/licensing-faq/).

3.  Azure Site Recovery çoğaltabilir ve mevcut şirket içi MCS veya PV'ler klonlar koruyun.
Azure RM teslim denetleyicisinden sağlama kullanarak bu klonlar toorecreate gerekir.

4. NetScaler NetScaler FreeBSD üzerinde temel alır ve Azure Site Recovery koruması FreeBSD işletim sistemi desteklemiyor gibi Azure Site Recovery kullanarak korunamaz. Toodeploy gerekir ve yük devretme tooAzure sonra yeni bir NetScaler Gereci Azure Market yerden yapılandırmak.


## <a name="replicating-virtual-machines"></a>Çoğaltma sanal makineler

Merhaba Citrix XenApp dağıtım bileşenlerini aşağıdaki hello korumalı toobe tooenable çoğaltma ve kurtarma gerekir.

* AD DNS sunucusunun koruma
* SQL veritabanı sunucusuna koruma
* Citrix teslim denetleyicisinin koruma
* Mağaza sunucusunun korumasını.
* Koruma XenApp yöneticisinin (VDA)
* Citrix XenApp lisans sunucusu koruma


**AD DNS sunucusu çoğaltma**

Lütfen çok başvurun[korumak Active Directory ve Azure Site Recovery ile DNS](site-recovery-active-directory.md) çoğaltma ve bir etki alanı denetleyicisi Azure'da yapılandırma kılavuzu üzerinde.

**SQL veritabanı sunucusu çoğaltma**

Lütfen çok başvurun[SQL Server olağanüstü durum kurtarma ve Azure Site Recovery ile SQL Server'ı koruma](site-recovery-sql.md) hello ayrıntılı teknik kılavuzluk etmesi için önerilen SQL sunucuları koruma için Seçenekler.

İzleyin [bu kılavuz](site-recovery-vmware-to-azure.md) hello diğer bileşen sanal makineleri tooAzure toostart çoğaltılıyor.

![XenApp bileşenlerinin koruma](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

**İşlem ve ağ ayarları**

Merhaba makineler korunduktan sonra (durum gösterildiği çoğaltılan öğeler altında "korumalı" gibi), hello işlem ve ağ ayarlarını yapılandırılmış toobe gerekir.
Buna işlem ve ağ > işlem özellikleri, hello Azure VM adını ve hedef boyutu belirtebilirsiniz.
Gerekirse hello adı toocomply Azure gereksinimleri ile değiştirin. Ayrıca, görüntülemek ve hello hedef ağ, alt ağ ve toohello Azure VM atanacak IP adresi hakkında bilgi ekleyebilirsiniz.

Merhaba aşağıdakileri göz önünde bulundurun:

* Merhaba hedef IP adresini ayarlayabilirsiniz. Bir adresi sağlamazsanız, yükü devredilen makine üzerinde hello DHCP kullanır. Yük devretmede kullanılamayan bir adres ayarlarsanız hello yük devretme çalışmaz. Merhaba hello test yük devretme ağı testinde Hello adresi varsa, yük devretme sınaması için aynı hedef IP adresi kullanılabilir.

* Merhaba AD/DNS sunucusu için hello korunuyor hello hello Azure sanal ağı için DNS sunucusu olarak aynı adres hello belirtmenizi adres sağlar şirket içi.

ağ bağdaştırıcısı Hello sayısını hello hedef sanal makine için aşağıdaki gibi belirtin hello boyuta göre dikte edilir:

*   Merhaba hello kaynak makinedeki ağ bağdaştırıcısı sayısı küçük veya buna eşit ise toohello bağdaştırıcı sayısı hello hedef makine boyutu için izin verilen sonra hello hedef olacaktır hello aynı sayıda bağdaştırıcıya hello kaynağı olarak.
*   Merhaba hello kaynak sanal makinenin bağdaştırıcı sayısı hello hedef boyutu sonra hello maksimum hedef boyutu kullanılır için izin verilen hello sayıyı aşarsa.
* Örneğin, kaynak makinenin iki bağdaştırıcısı varsa ve hello hedef makine boyutu dört adet bağdaştırıcıyı destekliyorsa hello hedef makinenin iki bağdaştırıcısı gerekir. Merhaba kaynak makinenin iki bağdaştırıcısı varsa, ancak hello hedef boyut yalnızca bir destekler hello hedef makine yalnızca bir bağdaştırıcısı olur.
*   Merhaba sanal makinede birden fazla ağ bağdaştırıcısı varsa bunların tümü toohello bağlanır aynı ağ.
*   Merhaba sanal makinede birden fazla ağ bağdaştırıcısı varsa, daha sonra hello birinci hello listede gösterilen hello varsayılan hello Azure sanal makine ağ bağdaştırıcısı olur.


## <a name="creating-a-recovery-plan"></a>Bir kurtarma planı oluşturma

Çoğaltma hello XenApp bileşen VM'ler için etkinleştirildikten sonra hello sonraki toocreate bir kurtarma planı adımdır.
Bir kurtarma grupları birlikte sanal makinelerle yük devretme ve kurtarma için benzer gereksinimlerini planlayın.  

**Adımları toocreate bir kurtarma planı**

1. Merhaba XenApp bileşen sanal makineleri hello Kurtarma planlaması ekleyin.
2. Kurtarma planları tıklatın -> + kurtarma planı. Hello kurtarma planı için kullanımı kolay bir ad girin.
3. VMware sanal makineler için: VMware işlem sunucusu, hedef olarak Microsoft Azure ve Resource Manager ve öğeleri seçebilir tıklayarak dağıtım modeli olarak kaynak seçme.
4. Hyper-V sanal makineleri için: kaynak VMM sunucusunu seçin, hedef Microsoft Azure ve olarak Resource Manager dağıtım modeli olarak ve Select öğelerde'ı tıklatın ve ardından hello XenApp dağıtım VM'ler seçin.

### <a name="adding-virtual-machines-toofailover-groups"></a>Sanal makineler toofailover grupları ekleme

Kurtarma planları belirli başlangıç düzeni, komut dosyaları veya el ile eylemler için özelleştirilmiş tooadd yük devretme grupları olabilir. grupları aşağıdaki hello toobe eklenen toohello kurtarma planına ihtiyacınız vardır.

1. Yük devretme Group1: AD DNS
2. Yük devretme grup2: SQL Server Vm'leri
2. Yük devretme Group3: VDA ana görüntü VM
3. Yük devretme Grup4: Teslim denetleyici ve mağaza server Vm'leri


### <a name="adding-scripts-toohello-recovery-plan"></a>Toohello kurtarma planı komutlar ekleme

Komut dosyaları önce veya sonra belirli bir grubu bir kurtarma planı çalıştırabilirsiniz. El ile yapılan eylemler olabilir de dahil ve yük devretme sırasında gerçekleştirilir.

Merhaba özelleştirilmiş kurtarma planı hello aşağıdaki gibi görünür:

1. Yük devretme Group1: AD DNS
2. Yük devretme grup2: SQL Server Vm'leri
3. Yük devretme Group3: VDA ana görüntü VM

   >[!NOTE]     
   >Adım 4, 6 ve 7 el ile veya komut dosyası eylemleri içeren olan geçerli tooonly bir şirket içi XenApp > MCS/PV'ler kataloglarıyla ortamı.

4. Grup 3 el ile veya komut dosyası eylemi: kapatma ana VDA VM hello ana VDA tooAzure başarısız olduğunda VM çalışır durumda olacaktır. Azure ARM barındırma kullanarak toocreate yeni MCS kataloglar, hello VDA VM durduruldu (ayrılan de) içinde gerekli toobe yöneticisidir durumu. Kapatma hello Azure portalından VM.

5. Yük devretme Grup4: Teslim denetleyici ve mağaza server Vm'leri
6. Group3 el ile veya komut dosyası eylemi 1:

    ***Azure RM ana bilgisayar bağlantı Ekle***

    Azure ARM ana bilgisayar bağlantı teslim denetleyicisi makine tooprovision Azure yeni MCS kataloglarında oluşturun. Bu konuda açıklandığı gibi Hello adımları [makale](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).

7. Group3 el ile veya komut dosyası eylemi 2:

    ***MCS kataloglar azure'da yeniden oluşturun***

    MCS veya PV'ler klonlar hello birincil sitede mevcut hello çoğaltılmış tooAzure olmaz. Hello kullanarak bu klonlar ana VDA ve Azure sağlama ARM teslim denetleyicisinden çoğaltılan toorecreate gerekir. Bu konuda açıklandığı gibi Hello adımları [makale](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS Azure'da kataloglar.

![Kurtarma planı XenApp bileşenleri](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   >Komut dosyalarını en kullanabilirsiniz [konumu](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) Merhaba, yeni IP başarısız üzerinden hello ile tooupdate hello DNS > sanal makine ya da tooattach hello yük dengeleyicide gerekirse, sanal makine üzerinde başarısız.


## <a name="doing-a-test-failover"></a>Yük devretme sınamasını yapmak

İzleyin [bu kılavuz](site-recovery-test-failover-to-azure.md) toodo yük devretme sınaması.

![Kurtarma planı](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a>Bir yük devretme işleminden

İzleyin [bu kılavuz](site-recovery-failover.md) , yaparken bir yük devretme.

## <a name="next-steps"></a>Sonraki adımlar

Yapabilecekleriniz [daha fazla bilgi edinin](https://aka.ms/citrix-xenapp-xendesktop-with-asr) Bu teknik incelemede Citrix XenApp ve XenDesktop dağıtımlarda çoğaltma hakkında. Merhaba Kılavuzu çok Ara[diğer uygulamaları çoğaltmak](site-recovery-workload.md) Site RECOVERY'yi kullanarak.
