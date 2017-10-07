---
title: "Azure Site kurtarma aaaTest yük devretme (VMM tooVMM) | Microsoft Docs"
description: "Azure Site Recovery hello çoğaltma, yük devretme ve sanal makinelerin ve fiziksel sunucuları kurtarma düzenler. Yük devretme tooAzure veya ikincil veri merkezine hakkında bilgi edinin."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: pratshar
ms.openlocfilehash: 6b4f65ab692cbb0665102c4f51ea0694151cd3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="test-failover-vmm-toovmm-in-site-recovery"></a>Site Recovery (VMM tooVMM) bir yük devretmeyi sınama


Bu makalede bilgiler sağlanmaktadır ve yük devretme testi veya bir olağanüstü durum kurtarma (DR) ayrıntıya sanal makineleri (VM'ler) ve fiziksel sunucuların, yapmaya yönelik yönergeler Azure Site Recovery ile korunur. System Center Virtual Machine Manager VMM tarafından yönetilen şirket içi site hello kurtarma sitesi olarak kullanacaksınız.

Bir test yük devretme toovalidate çoğaltma stratejinizi çalıştırmak veya DR detayı herhangi bir veri kaybı veya kapalı kalma süresi olmadan gerçekleştirin. Yük devretme testi etkilerini hello devam eden çoğaltmayı veya üretim ortamınıza sahip değil. Bir sanal makine ya da bir çalıştırabilirsiniz [kurtarma planı](site-recovery-create-recovery-plans.md). Yük devretme testi tetiklendiğinde hello test sanal makineleri bağlanacağı toospecify hello ağ gerekir. Merhaba üzerinde hello yük devretme testi hello ilerlemesini izleyebilirsiniz **işleri** sayfası.  

Tüm yorumlarınızı ve sorularınızı varsa, bu makalenin veya hello hello altındaki bunları sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hello-infrastructure-for-test-failover"></a>Yük devretme sınaması için Hello altyapıyı hazırlama
Varolan bir ağ kullanarak yük devretme testi toorun istiyorsanız, Active Directory, DHCP ve DNS, ağ hazırlayın.

Merhaba seçeneği toocreate VM ağları otomatik olarak kullanarak toorun yük devretme testi istiyorsanız, hello yük devretme sınaması için toouse oluşturacağız hello kurtarma planında Grup 1 önce el ile bir adım ekleyin. Ardından, ağ hello test yük devretmesi çalıştırmadan önce otomatik olarak oluşturulan hello altyapı kaynakları toohello ekleyin.

### <a name="things-toonote"></a>Şeyler toonote
Ne zaman tooa ikincil site, hello çoğaltma makineyi kullandığı toomatch hello yük devretme sınaması için kullanılan mantıksal ağ türünde gerek değil, ancak bazı birleşimleri çalışmayabilir ağ hello türü çoğaltma yapıyorsanız. DHCP ve VLAN tabanlı yalıtım Hello çoğaltma kullanıyorsa, hello VM ağı hello çoğaltma için bir statik IP adresi havuzu gerekmez. Herhangi bir adres havuzu kullanılabilir olmadığından bunu hello yük devretme sınaması için Windows ağ sanallaştırma kullanarak çalışmaz. 

Ayrıca, hello yük devretme testi hello çoğaltma ağ yalıtımı kullanır ve Windows ağ sanallaştırma hello test ağı kullanıyorsa çalışmaz. Bir Windows ağ sanallaştırma ağ Hello yalıtımsız ağ hello alt ağlar gerekli toocreate sahip olmadığından budur.

Yük devretme hello VM ağı hello VMM konsolunda nasıl yapılandırıldığına bağlıdır sonra nasıl çoğaltma sanal makineleri bağlı toomapped VM ağlardır.

#### <a name="vm-network-configured-with-no-isolation-or-vlan-isolation"></a>Hiçbir yalıtım veya VLAN yalıtımı ile yapılandırılmış VM ağı
Merhaba VM ağı için DHCP tanımlanmışsa hello çoğaltma sanal makinesi hello hello ilişkili mantıksal ağ bir ağ sitesi için belirtilen hello ayarları aracılığıyla bağlı toohello VLAN Kimliği ' dir. Merhaba sanal makinenin IP adresini hello kullanılabilir DHCP sunucusundan alır. 

Merhaba hedef VM ağı için statik bir IP adresi havuzu toodefine gerekmez. Bir statik IP adresi havuzu hello VM ağı için kullanılırsa, hello çoğaltma sanal makinesi hello hello ilişkili mantıksal ağ bir ağ sitesi için belirtilen hello ayarları aracılığıyla bağlı toohello VLAN Kimliği ' dir.

Merhaba sanal makinenin IP adresini hello VM ağ için tanımlı hello havuzundan alır. Bir statik IP adresi havuzu hello hedef VM ağı üzerinde tanımlı değil, IP adresi ayırma başarısız olur. Koruma ve kurtarma için kullanacağınız her iki hello kaynak ve hedef VMM sunucularında Hello IP adresi havuzu oluşturun.

#### <a name="vm-network-with-windows-network-virtualization"></a>Windows ağ sanallaştırma ile VM ağı
Bir VM ağı Windows ağ sanallaştırma ile yapılandırılmışsa, hello kaynak VM ağına yapılandırılmış toouse DHCP olmasına bakılmaksızın hello hedef VM ağı için statik bir havuz veya bir statik IP adresi havuzu tanımlamanız gerekir. 

DHCP tanımlarsanız, hello hedef VMM sunucusunda bir DHCP sunucusu gibi davranan ve hello hedef VM ağı için tanımlanan hello havuzundan bir IP adresi sağlar. Bir statik IP adresi havuzu kullanımı hello kaynak sunucu için tanımlanmış olması durumunda, hello hedef VMM sunucusunda hello havuzundan bir IP adresi ayırır. Her iki durumda da, bir statik IP adresi havuzu tanımlanmazsa, IP adresi ayırma başarısız olur.


### <a name="prepare-dhcp"></a>DHCP hazırlama
Merhaba sanal makineleri katılan yük devretme testi DHCP kullanmak, bir test DHCP sunucusu yük devretme sınamasının hello amaçla hello yalıtılmış ağ içindeki oluşturun.

### <a name="prepare-active-directory"></a>Active Directory hazırlama
bir yük devretme sınaması için sınama uygulama toorun, test ortamınızda hello üretim Active Directory ortamında bir kopyasını gerekir. Daha fazla bilgi için hello gözden [test Active Directory için yük devretme konuları](site-recovery-active-directory.md#test-failover-considerations).

### <a name="prepare-dns"></a>DNS hazırlama
Bir DNS sunucusu hello yük devretme sınaması için aşağıdaki gibi hazırlayın:

* **DHCP**: sanal makineler DHCP kullanıyorsanız, başlangıç IP adresi DNS hello testinin hello test DHCP sunucusunda güncelleştirilmesi gerekir. Bir ağ türü Windows ağ sanallaştırma kullanıyorsanız, hello VMM sunucusu hello DHCP sunucu gibi davranır. Bu nedenle, başlangıç IP adresi DNS hello test yük devretme ağı testinde güncelleştirilmesi gerekir. Bu durumda, hello sanal makineler kendilerini toohello ilgili DNS sunucusunu kaydedin.
* **Statik adresi**: sanal makinelere statik IP adresi kullanırsanız, DNS sunucusu yük devretme ağı içinde güncelleştirilecek hello test IP adresini hello. Tooupdate DNS hello test sanal makinelerin hello IP adresiyle gerekebilir. Bu amaç için örnek komut dosyası izleyen hello kullanabilirsiniz:

        Param(
        [string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="run-a-test-failover"></a>Yük devretme testi çalıştırma
Bu yordam açıklar nasıl toorun bir yük devretme sınaması için bir kurtarma planı. Alternatif olarak, tek bir sanal makine için yük devretme hello hello üzerinde çalıştırabilirsiniz **sanal makineleri** sekmesi.

![Test yük devretme dikey penceresi](./media/site-recovery-test-failover-vmm-to-vmm/TestFailover.png)

1. Seçin **kurtarma planları** > *recoveryplan_name*. Tıklatın **yük devretme** > **yük devretme testi**.
1. Merhaba üzerinde **sınama yük devretmesi** dikey penceresinde, sanal makineleri bağlı toonetworks hello test yük devretme sonrasında nasıl gerektiğini belirtin. Daha fazla bilgi için bkz: Merhaba [ağ seçenekleri](#network-options-in-site-recovery).
1. Merhaba üzerinde yük devretme işleminin ilerleyişini izlemek **işleri** sekmesi.
1. Yük devretme işlemi tamamlandıktan sonra hello sanal makineler başarıyla başlatıldığını doğrulayın.
1. İşiniz bittiğinde tıklatın **temizleme yük devretme testi** hello kurtarma planı üzerinde. İçinde **notları**hello yük devretme testiyle ilişkili gözlemlerinizi kaydetmek ve kaydedin. Bu adım hello sanal makineler ve yük devretme testi sırasında oluşturulan ağlar siler.


## <a name="network-options-in-site-recovery"></a>Site Recovery içindeki ağ seçenekleri

Yük devretme testi çalıştırdığınızda, test yineleme makineler için tooselect ağ ayarlarını sorulur. Birden fazla seçeneği vardır.  

| **Test yük devretme seçeneği** | **Açıklama** | **Yük devretme denetimi** | **Ayrıntılar** |
| --- | --- | --- | --- |
| **Tooa ikincil VMM sitesi--ağ olmadan yük devri** |Bir VM ağı seçmeyin. |Yük devretme test makinelerini oluşturduğunuz denetler.<br/><br/>Merhaba test sanal makinesi hello çoğaltma sanal makinesi bulunduğu hello konakta oluşturulur. Merhaba çoğaltma sanal makinesi bulunduğu toohello bulut eklenmez. |<p>Merhaba başarısız üzerinden makine bağlı tooany ağ değil.<br/><br/>oluşturulduktan sonra hello makine bağlı tooa VM ağı olabilir. |
| **Tooa ikincil VMM sitesi--ağ ile yük devri** |Var olan bir VM ağı seçin. |Sanal makineler oluşturulan yük devretme denetler. |Merhaba test sanal makinesi hello çoğaltma sanal makinesi bulunduğu hello konakta oluşturulur. Merhaba çoğaltma sanal makinesi bulunduğu toohello bulut eklenmez.<br/><br/>Üretim ağınızdan yalıtılmış olan bir VM ağı oluşturun.<br/><br/>VLAN tabanlı ağ kullanıyorsanız (üretimde kullanılmaz) ayrı bir mantıksal ağ oluşturma VMM'de bu amaç için öneririz. Kullanılan toocreate VM ağları yük devretme sınaması işlemlerini için bu mantıksal ağdır.<br/><br/>Merhaba mantıksal ağ hello sunucularının ağ bağdaştırıcıları, sanal makineleri barındıran tüm hello Hyper-V en az biriyle ilişkili olmalıdır.<br/><br/>VLAN Mantıksal ağlar için hello toohello mantıksal ağ Ekle ağ siteleri yalıtılmış olması gerekir.<br/><br/>Windows ağ sanallaştırma tabanlı bir mantıksal ağ kullanıyorsanız, Azure Site Recovery yalıtılmış VM ağları otomatik olarak oluşturur. |
| **Başarısız bir ağ tooa ikincil VMM sitesi--oluşturma** |Bir geçici test ağı belirttiğiniz hello ayarına göre otomatik olarak oluşturulan **mantıksal ağ** ve onun ilişkili ağ siteleri. |Sanal makineler oluşturulan yük devretme denetler. |Merhaba kurtarma planı birden fazla VM ağı kullanıyorsa bu seçeneği kullanın. Windows ağ Sanallaştırması ağlarına kullanıyorsanız, bu seçenek otomatik olarak VM ağları hello ile aynı ayarları (alt ağlar ve IP adresi havuzları) hello çoğaltma sanal makinesi hello ağında oluşturabilirsiniz. Merhaba test yük devretme işlemi tamamlandıktan sonra bu VM ağları otomatik olarak temizlenir.</p><p>Merhaba test sanal makinesi hello çoğaltma sanal makinesi bulunduğu hello konakta oluşturulur. Merhaba çoğaltma sanal makinesi bulunduğu toohello bulut eklenmez. |

> [!TIP]
> Merhaba tooa sanal makine yük devretme testi sırasında verilen IP adresi olduğundan hello sanal makine hello aynı IP adresi almasını (Merhaba IP adresi hello test yük devretme ağda kullanılabilir olduğunu pek fazla) planlanmış veya planlanmamış bir yük devretme için. Merhaba aynı IP adresini hello test yük devretme ağında kullanılabilir değilse, hello sanal makine hello test yük devretme ağı testinde kullanılabilirse başka bir IP adresi alır.
>
>


## <a name="test-failover-tooa-production-network-on-a-recovery-site"></a>Kurtarma sitesinde test yük devretme tooa üretim ağı
Yük devretme testi yaparken, sağladığınız üretim ağınızdan kurtarma sitesini farklı bir ağ seçmenizi öneririz [ağ eşlemesi](https://docs.microsoft.com/azure/site-recovery/site-recovery-network-mapping). Ancak, gerçekten toovalidate uçtan uca ağ bağlantısı başarısız oldu üzerinden sanal makinede istiyorsanız, aşağıdaki noktaları hello dikkat edin:

* Merhaba test yük devretme yapılırken hello birincil sanal makinenin kapatılması emin olun. Bunu yapmazsanız, aynı kimlik çalışıyor. aynı ağ konumundaki hello içinde hello iki sanal makinelerle aynı hello zaman. Bu durum tooundesired sonuçlara yol açabilir.
* Yük devretme sanal makineleri hello temizleme test ettiğinizde yük devretme sanal makineleri test toohello yaptığınız tüm değişiklikler kaybedilir. Bu değişiklikler çoğaltılmış geri toohello birincil sanal makine olup olmadığı.
* Bu şekilde test yapmanın toodowntime üretim uygulamanız için yol gösterir. Merhaba uygulaması değil toouse kullanıcılarının hello DR ayrıntısına gittiğinizde hello uygulama sürüyor isteyin.  


## <a name="next-steps"></a>Sonraki adımlar
Yük devretme testi başarıyla çalıştırdıktan sonra deneyebilirsiniz bir [yük devretme](site-recovery-failover.md).
