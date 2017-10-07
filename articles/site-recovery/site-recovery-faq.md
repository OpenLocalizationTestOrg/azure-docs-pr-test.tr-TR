---
title: "Azure Site Recovery: Sık sorulan sorular | Microsoft Docs"
description: "Bu makalede, Azure Site Recovery hakkında yaygın sorular açıklanır."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5cdc4bcd-b4fe-48c7-8be1-1db39bd9c078
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/22/2017
ms.author: raynew
ms.openlocfilehash: 6d0bd2475466e5745e1f084bd2267d954d624ebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-frequently-asked-questions-faq"></a>Azure Site Recovery: Sık sorulan sorular (SSS)
Bu makale, Azure Site Recovery hakkında sık sorulan sorular içermektedir. Bu makaleyi okuduktan sonra sorularınız varsa, bunları üzerinde hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).

## <a name="general"></a>Genel
### <a name="what-does-site-recovery-do"></a>Site Recovery ne işe yarar?
Site Recovery yönetme ve Azure sanal makinelerini çoğaltma bölgeler, şirket içi sanal makineleri ve fiziksel sunucuları tooAzure arasında otomatikleştirme tooyour iş devamlılığı ve olağanüstü durum kurtarma (BCDR) stratejinize katkı ve şirket içi makineler tooa İkincil veri merkezi. [Daha fazla bilgi edinin](site-recovery-overview.md).

### <a name="what-can-site-recovery-protect"></a>Hangi Site Recovery koruyabilir miyim?
* **Azure VM'ler**: Site Recovery, desteklenen bir Azure VM'de çalışan herhangi bir iş yükünü çoğaltabilir
* **Hyper-V sanal makineleri**: Site Recovery, bir Hyper-V VM'de çalışan tüm iş yüklerini koruyabilir.
* **Fiziksel sunucuları**: Site Recovery, Windows veya Linux çalıştıran fiziksel sunucuları koruyabilir.
* **VMware sanal makineleri**: Site Recovery, bir VMware VM içinde çalışan tüm iş yüklerini koruyabilir.

### <a name="does-site-recovery-support-hello-azure-resource-manager-model"></a>Site Recovery hello Azure Resource Manager modeli destekliyor mu?
Site Recovery hello Azure portalı desteği için Resource Manager ile de kullanılabilir. Site Recovery hello Klasik Azure portalı eski dağıtımlarını destekler. Yeni kasa hello Klasik Portalı'nda oluşturulamıyor ve yeni özellikler desteklenmez.

### <a name="can-i-replicate-azure-vms"></a>Azure VM'ler çoğaltabilir miyim?
Evet, desteklenen Azure sanal Azure bölgeler arasında çoğaltabilirsiniz. [Daha fazla bilgi edinin](site-recovery-azure-to-azure.md).

### <a name="what-do-i-need-in-hyper-v-tooorchestrate-replication-with-site-recovery"></a>Site Recovery ile Hyper-V tooorchestrate çoğaltmasındaki ne gerekiyor?
Merhaba Hyper-V ana bilgisayarı sunucusu için gerekenler hello dağıtım senaryosuna bağlıdır. Merhaba Hyper-V önkoşulları denetleyin:

* [Hyper-V Vm'lerini (VMM olmadan) tooAzure çoğaltma](site-recovery-hyper-v-site-to-azure.md)
* [Hyper-V Vm'lerini (VMM ile) tooAzure çoğaltma](site-recovery-vmm-to-azure.md)
* [Hyper-V sanal makineleri tooa ikincil veri merkezine çoğaltma](site-recovery-vmm-to-vmm.md)
* Veri Merkezi tooa ikincil çoğaltıyorsanız okuyun [desteklenen konuk işletim sistemleri için Hyper-V sanal makineleri](https://technet.microsoft.com/library/mt126277.aspx).
* TooAzure çoğaltma yapıyorsanız Site Recovery tüm hello konuk işletim sistemlerini destekler [Azure tarafından desteklenen](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).

### <a name="can-i-protect-vms-when-hyper-v-is-running-on-a-client-operating-system"></a>Hyper-V istemci işletim sisteminde çalışırken Vm'leri koruyabilir miyim?
Hayır, VM'lerin desteklenen bir Windows sunucusu makinesinde çalışan Hyper-V ana bilgisayar sunucusunda bulunması gerekir. Tooprotect gerekiyorsa bir istemci bilgisayar, fiziksel bir makine olarak çok çoğaltma[Azure](site-recovery-vmware-to-azure.md) veya [ikincil veri merkezine](site-recovery-vmware-to-vmware.md).

### <a name="what-workloads-can-i-protect-with-site-recovery"></a>Site Recovery ile hangi iş yüklerini koruyabilirim?
Desteklenen VM veya fiziksel sunucu üzerinde çalışan çoğu iş yükleri Site Recovery tooprotect kullanabilirsiniz. Site Recovery uygulamaları olabilmesi Bu destek uygulamaya duyarlı çoğaltma için sunar tooan akıllı duruma kurtarıldı. SharePoint, Exchange, Dynamics, SQL Server ve Active Directory gibi Microsoft uygulamalarıyla tümleşir ve Oracle, SAP, IBM ve Red Hat gibi lider satıcılarla yakın bir tümleştirmede çalışır. İş yükü koruması hakkında [daha fazla bilgi edinin](site-recovery-workload.md).

### <a name="do-hyper-v-hosts-need-toobe-in-vmm-clouds"></a>Hyper-V konakları VMM bulutlarındaki toobe gerekiyor mu?
Hyper-V sanal makineleri olmalıdır sonra tooreplicate tooa ikincil veri merkezine, isterseniz, Hyper-V VMM bulutta konumlandırılmış sunucular barındırır. Tooreplicate tooAzure istiyorsanız ile ve VMM Bulutları olmadan Hyper-V ana bilgisayar sunucuları üzerinde sanal makineleri çoğaltabilirsiniz. [Daha fazla bilgi](site-recovery-hyper-v-site-to-azure.md).

### <a name="can-i-deploy-site-recovery-with-vmm-if-i-only-have-one-vmm-server"></a>Tek bir VMM sunucusuna sahip olsam da Site Recovery'yi VMM ile dağıtabilir miyim?

Evet. Hyper-V sunucularında hello VMM bulut tooAzure içinde sanal makineleri çoğaltabilirsiniz veya, hello üzerinde VMM bulutlarının arasında aynı çoğaltabilirsiniz sunucu. Şirket içi tooon içi çoğaltma için her iki hello birincil ve ikincil sitelere de bir VMM sunucusu sahip olmasını öneririz.  

### <a name="what-physical-servers-can-i-protect"></a>Hangi fiziksel sunucuları koruyabilirim?
Windows ve Linux tooAzure veya tooa ikincil sitesinde çalışan fiziksel sunucuları çoğaltabilirsiniz. [Hakkında bilgi edinin](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) işletim sistemi gereksinimleri.  Merhaba fiziksel sunucuları tooAzure veya tooa ikincil siteye çoğaltma yapıyorsanız olup olmadığını aynı gereksinimleri geçerlidir.


Şirket içi sunucu kullanılamaz hale gelirse fiziksel sunucuları azure'da VM olarak çalışacağını unutmayın. Yeniden çalışma tooan fiziksel sunucu şu anda desteklenmiyor şirket içi. Fiziksel olarak korumalı bir makine için yalnızca geri dönme tooa VMware sanal makine olabilir.

### <a name="what-vmware-vms-can-i-protect"></a>Hangi VMware VM'lerini koruyabilirim?

VMware Vm'leri tooprotect bir vSphere hiper yöneticisine ve VMware araçlarında çalışan sanal makineleri gerekir. Ayrıca, bir VMware vCenter server toomanage hello hiper olmasını öneririz. [Daha fazla bilgi edinin](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) VMware sunucularını ve Vm'leri tooAzure veya tooa ikincil site çoğaltılması gereksinimlerinin tamamı hakkında.


### <a name="can-i-manage-disaster-recovery-for-my-branch-offices-with-site-recovery"></a>Site Recovery ile şubelerim için olağanüstü durum kurtarma işlemini yönetebilir miyim?
Evet. Site Recovery tooorchestrate çoğaltma ve yük devretme şubelerinizde kullandığınızda, merkezi bir konumda bir birleşik orchestration ve tüm dal office yükleri görünümünü elde edersiniz. Kolay yük devretmeler çalıştırabilirsiniz ve tüm dalları olağanüstü durum kurtarma baş ofisinizden hello şubelerinizi ziyaret etmenize gerek kalmadan yönetebilirsiniz.

## <a name="pricing"></a>Fiyatlandırma

### <a name="what-charges-do-i-incur-while-using-azure-site-recovery"></a>Hangi ı Azure Site Recovery kullanırken ücretlendirme?
Site Recovery kullandığınızda, hello Site Recovery lisans, Azure depolama, depolama işlemleri ve giden veri aktarımı için ücret doğurur. [Daha fazla bilgi edinin](https://azure.microsoft.com/pricing/details/site-recovery).

Merhaba Site Recovery lisans örneği bir VM veya fiziksel sunucu olduğu korumalı örneğidir.

- Bir VM disk tooa standart depolama hesabı çoğaltır, hello Azure depolama ücret hello depolama tüketimini olur. Örneğin, hello kaynak disk boyutu ise 1 TB ve 400 GB kullanılabilir, Site Recovery, Azure'da 1 TB VHD oluşturur, ancak 400 GB (artı hello çoğaltma günlükleri için kullanılan depolama alanı miktarı) ücret hello depolama dir.
- VM disk tooa premium depolama hesabı çoğaltılırsa, hello Azure depolama ücretsiz olarak sağlanan hello depolama boyutu, premium depolama diski seçeneği en yakın hello için yuvarlanmasını içindir. Örneğin, hello kaynak disk boyutu 50 GB ise, Site Recovery, Azure'da 50 GB disk oluşturur ve bu toohello premium depolama diskini (P10) en yakın Azure eşler.  Maliyetleri P10 ve hello 50 GB disk boyutu değil, hesaplanır.  [Daha fazla bilgi edinin](https://aka.ms/premium-storage-pricing).  Premium depolama kullanıyorsanız, bir standart depolama hesabı çoğaltma günlüğü için de gereklidir ve bu günlükler için kullanılan standart depolama alanı miktarının hello ayrıca faturalandırılır.
- Hiçbir disk yük devretme testi veya bir yük devretme oluşturulur. Merhaba çoğaltma durumunun depolama ücretlendirilen "Sayfa blobu ve disk" Merhaba kategorisi altında göredir hello [depolama fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/en-in/pricing/calculator/) alınan. Bu ücretlerden premium/standart ve hello veri artıklık depolama türü hello temelinde - LRS, GRS, RA-GRS vb. yazın.
- Bir yük devretme üzerinde yönetilen disklerde Hello seçeneği toouse seçilirse, [ücretleri yönetilen diskleri için](https://azure.microsoft.com/en-in/pricing/details/managed-disks/) bir yük devretme ve test yük devretme sonrasında uygulayın. Yönetilen disklerde ücretleri çoğaltma sırasında uygulanmaz.
- Bir yük devretme Hello seçeneği toouse yönetilen disklerde seçili değilse, depolama "Sayfa blobu ve disk" Merhaba kategorisi altında hello başına ücretlendirilen. [depolama fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/en-in/pricing/calculator/) yük devretme sonrasında ücrete. Bu ücretlerden premium/standart ve hello veri artıklık depolama türü hello temelinde - LRS, GRS, RA-GRS vb. yazın.
- Depolama işlemleri kararlı durum çoğaltma sırasında ve düzenli VM işlemleri için bir yük devretme sonrasında ücretlendirilen / yük devretme sınamasını. Ancak bu ücretlerden önemsizdir.

Ayrıca hello VM, depolama, çıkış ve depolama işlem maliyetleri nereye uygulanacağını test yük devretmesi sırasında maliyetlere.



## <a name="security"></a>Güvenlik
### <a name="is-replication-data-sent-toohello-site-recovery-service"></a>Çoğaltma verilerinin toohello Site Recovery hizmetine gönderilir mi?
Hayır, Site Recovery çoğaltılan verilere müdahale etmez ve hangi sanal makineleri veya fiziksel sunucuları üzerinde çalışan hakkında herhangi bir bilgi yoktur.
Çoğaltma verileri şirket içi Hyper-V ana bilgisayarları, VMware hiper yöneticileri veya fiziksel sunucular ile Azure depolama alanı ya da ikincil siteniz arasında değiştirilir. Site Kurtarma özelliği toointercept bu verilere sahip. Meta veri hello tooorchestrate çoğaltma gerekli ve yük devretme toohello Site Recovery hizmetine gönderilir.  

Site Recovery ISO 27001: 2013, 27018, HIPAA, DPA sertifikalı, SOC2 ile FedRAMP JAB değerlendirmelerini hello işleminde ise.

### <a name="for-compliance-reasons-even-our-on-premises-metadata-must-remain-within-hello-same-geographic-region-can-site-recovery-help-us"></a>Uyumluluk nedenleriyle bile bizim şirket içi meta veri hello içinde kalması gereken aynı coğrafi bölgede. Site Recovery bize yardımcı olabilir?
Evet. Bir bölgede Site Recovery kasası oluşturduğunuzda, tooenable gerekir ve çoğaltmayı düzenlemek ve yük devretme kalır, bölge içinde tüm meta veriler coğrafi olun sınır.

### <a name="does-site-recovery-encrypt-replication"></a>Site Recovery çoğaltma işlemini şifreleyebilir mi?
Şirket içi siteler şifreleme-aktarım sırasında arasında çoğaltma sanal makineleri ve fiziksel sunucular için desteklenir. Sanal makineler ve fiziksel sunucuları tooAzure, hem şifreleme-aktarım sırasında çoğaltmak için ve [rest belirli konumunda şifreleme (azure'da)](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) desteklenir.

## <a name="replication"></a>Çoğaltma

### <a name="can-i-replicate-over-a-site-to-site-vpn-tooazure"></a>Siteden siteye VPN tooAzure çoğaltabilir miyim?
Azure Site Recovery veri tooan Azure depolama hesabı, genel bir uç nokta çoğaltır. Çoğaltma, siteden siteye VPN üzerinden değil. Bir Azure sanal ağı ile bir siteden siteye VPN oluşturabilirsiniz. Bu Site Recovery çoğaltma ile engellemez.

### <a name="can-i-use-expressroute-tooreplicate-virtual-machines-tooazure"></a>ExpressRoute tooreplicate sanal makineleri tooAzure kullanabilir miyim?
Evet, ExpressRoute kullanılan tooreplicate sanal makineleri tooAzure olabilir. Azure Site Recovery genel bir uç nokta üzerinden veri tooan Azure depolama hesabı çoğaltır. Yukarı tooset gerek [ortak eşleme](../expressroute/expressroute-circuit-peerings.md#public-peering) toouse ExpressRoute Site Recovery çoğaltma için. Azure sanal ağı tooan Hello sanal makineleri başarısız olmasından sonra bunlara erişebileceği hello kullanarak [özel eşleme](../expressroute/expressroute-circuit-peerings.md#private-peering) Kurulum hello Azure sanal ağı ile.

### <a name="are-there-any-prerequisites-for-replicating-virtual-machines-tooazure"></a>Sanal makineler tooAzure çoğaltmak için Önkoşullar bulunur?
Tooreplicate tooAzure istediğiniz sanal makineleri ile uyumlu olması gerekir [Azure gereksinimleri](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

Azure kullanıcı hesabınızın toohave belirli gereken [izinleri](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) yeni bir sanal makine tooAzure tooenable çoğaltması.

### <a name="can-i-replicate-hyper-v-generation-2-virtual-machines-tooazure"></a>Hyper-V nesil 2 sanal makine tooAzure çoğaltabilir miyim?
Evet. Site Recovery 2. nesil toogeneration 1 ' yük devretme sırasında dönüştürür. Yeniden çalışmada hello dönüştürülen geri toogeneration 2 makinesidir. [Daha fazla bilgi](http://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/).

### <a name="if-i-replicate-tooazure-how-do-i-pay-for-azure-vms"></a>TooAzure çoğaltma yaparsam ne Azure VM'ler için ödeme?
Normal çoğaltma sırasında veri çoğaltılmış toogeo yedekli Azure depolama ve önemli bir avantajı sağlayan herhangi bir Azure Iaas sanal makine ücret toopay gerekmez. Bir yük devretme tooAzure, Site Recovery otomatik olarak çalıştırdığınızda Azure Iaas sanal makineleri oluşturur ve bundan sonra Azure'da tüketen hello işlem kaynakları için faturalandırılırsınız.

### <a name="can-i-automate-site-recovery-scenarios-with-an-sdk"></a>Site kurtarma senaryolarına bir SDK'sı otomatik hale getirebilirsiniz?
Evet. Merhaba Rest API'si, PowerShell veya hello Azure SDK kullanarak Site Recovery iş akışlarını otomatikleştirebilirsiniz. Site Recovery PowerShell kullanarak dağıtmak için şu anda desteklenen senaryolar:

* [VMMs Bulutlar tooAzure PowerShell Resource Manager Hyper-V Vm'lerini çoğaltma](site-recovery-vmm-to-azure-powershell-resource-manager.md)
* [VMM tooAzure PowerShell Resource Manager Hyper-V Vm'lerini çoğaltma](site-recovery-deploy-with-powershell-resource-manager.md)

### <a name="if-i-replicate-tooazure-what-kind-of-storage-account-do-i-need"></a>TooAzure çoğaltma yaparsam ne tür bir depolama hesabı ihtiyacım var mı?
* **Klasik Azure portalı**: hello Klasik Azure portalında Site Recovery dağıtıyorsanız gerekir bir [standart coğrafi olarak yedekli depolama hesabı](../storage/common/storage-redundancy.md#geo-redundant-storage). Premium depolama şu anda desteklenmiyor. Merhaba hesabı hello olmalıdır hello Site Recovery kasasıyla aynı bölgede.
* **Azure portal**: hello Azure portalında Site Recovery dağıtıyorsanız, bir LRS veya GRS depolama hesabınızın olması gerekir. Böylece bölgesel bir kesinti oluşursa veya hello birincil bölgenin kurtarılamaması durumunda verilerin esnektir GRS öneririz. Merhaba hesabı hello olmalıdır hello aynı bölgede kurtarma Hizmetleri kasası. Hello Azure portalında Site Recovery dağıttığınızda premium depolama artık VMware VM, Hyper-V VM ve fiziksel sunucu çoğaltma için desteklenir.

### <a name="how-often-can-i-replicate-data"></a>Verileri ne sıklıkta çoğaltabilirim?
* **Hyper-V:** her (dışında premium depolama) 30 saniye, 5 dakika veya 15 dakika Hyper-V sanal makineleri'nin çoğaltılabilir. SAN çoğaltması ayarladıysanız çoğaltma uyumludur.
* **VMware ve fiziksel sunucular:** Burada çoğaltma sıklığı geçerli değildir. Çoğaltma sürekli ' dir.

### <a name="can-i-extend-replication-from-existing-recovery-site-tooanother-tertiary-site"></a>Var olan kurtarma sitesinden site tooanother üçüncül çoğaltma genişletebilir miyim?
Genişletilmiş veya zincir çoğaltma desteklenmez. Bu özellik isteği [geri bildirim Forumunda](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6097959-support-for-exisiting-extended-replication).

### <a name="can-i-do-an-offline-replication-hello-first-time-i-replicate-tooazure"></a>TooAzure çoğaltma ilk kez bir çevrimdışı çoğaltma hello yapabilirim?
Bu özellik desteklenmez. Bu özelliği hello isteği [geri bildirim Forumunda](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6227386-support-for-offline-replication-data-transfer-from).

### <a name="can-i-exclude-specific-disks-from-replication"></a>Belirli diskleri çoğaltmanın dışında tutabilir miyim?
Bunu olduğunuzda destekleniyorsa [VMware Vm'lerini ve Hyper-V Vm'lerini çoğaltma](site-recovery-exclude-disk.md) hello Azure portal kullanarak tooAzure.

### <a name="can-i-replicate-virtual-machines-with-dynamic-disks"></a>Sanal makineleri dinamik disklerle çoğaltabilir miyim?
Dinamik diskler, Hyper-V sanal makineleri çoğaltılırken desteklenir. VMware Vm'lerini ve fiziksel makineler tooAzure çoğaltırken de desteklenir. Merhaba işletim sistemi diski temel disk olması gerekir.

### <a name="can-i-add-a-new-machine-tooan-existing-replication-group"></a>Yeni bir makine tooan mevcut çoğaltma grubu ekleyebilir miyim?
Yeni makineleri tooexisting çoğaltma grupları ekleme desteklenir. Bu nedenle, toodo hello çoğaltma grubundan ('Çoğaltılan öğeler' dikey) ve hello çoğaltma grubunu sağ tıklatın/seçmek bağlam menüsünde seçin ve hello uygun seçeneği belirleyin.

![Tooreplication grubu Ekle](./media/site-recovery-faq/add-server-replication-group.png)

### <a name="can-i-throttle-bandwidth-allotted-for-hyper-v-replication-traffic"></a>Hyper-V çoğaltma trafiği için ayrılan bant genişliğini kısıtlayabilir miyim?
Evet. Daha fazla bilgiyi hello dağıtım makalelerinin bant genişliği azaltma hakkında:

* [Kapasite VMware Vm'lerini ve fiziksel sunucuları çoğaltmak için planlama](site-recovery-plan-capacity-vmware.md)
* [Kapasite VMM bulutlarındaki Hyper-V sanal makineleri çoğaltmak için planlama](site-recovery-vmm-to-azure.md#capacity-planning)
* [Kapasite VMM olmadan Hyper-V sanal makineleri çoğaltmak için planlama](site-recovery-hyper-v-site-to-azure.md)

## <a name="failover"></a>Yük devretme
### <a name="if-im-failing-over-tooazure-how-do-i-access-hello-azure-virtual-machines-after-failover"></a>TooAzure başarısız, nasıl erişebilirim hello Azure sanal makineleri yük devretme sonrasında?
Hello Azure Vm'lerine güvenli bir Internet bağlantısı üzerinden, siteden siteye VPN üzerinden veya Azure ExpressRoute üzerinden erişebilirsiniz. Tooprepare sipariş tooconnect şeyler sayısı gerekir. [Daha fazla bilgi](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)


### <a name="if-i-fail-over-tooazure-how-does-azure-make-sure-my-data-is-resilient"></a>Verilerim nasıl Azure emin tooAzure başarısız olursa esnek mi?
Azure esneklik için tasarlanmıştır. Site Recovery ile yük devretme tooa ikincil Azure veri merkezi, Azure hello gerekiyorsa SLA ortaya hello uygun olarak zaten geliştirilmiştir. Bu durum, biz meta verileriniz emin olun ve kasa kalırsa hello içinde kasanız için seçtiğiniz aynı coğrafi bölgede.  

### <a name="if-im-replicating-between-two-datacenters-what-happens-if-my-primary-datacenter-experiences-an-unexpected-outage"></a>İki veri merkezi arasında çoğaltma yapıyorsam my birincil veri merkezi beklenmeyen bir kesinti oluşursa ne olur?
Merhaba ikincil siteden planlanmamış yük devretme tetikleyebilirsiniz. Site Recovery hello birincil site tooperform hello yük devretme bağlantısını gerekmez.

### <a name="is-failover-automatic"></a>Yük devretme işlemi otomatik midir?
Yük devretme işlemi otomatik değildir. Yük devretme işlemlerini tek bir tıklatmayla hello portalında başlatmak veya kullanabilirsiniz [Site Recovery PowerShell](/powershell/module/azurerm.siterecovery) tootrigger bir yük devretme. Geri başarısız hello Site Recovery portalında basit bir işlemdir.

kullanabileceğinizi tooautomate içi Orchestrator veya Operations Manager toodetect sanal makine hatasını ve ardından tetikleyici hello yük devretme kullanarak hello SDK.

* [Daha fazla bilgi](site-recovery-create-recovery-plans.md) kurtarma planları hakkında.
* [Daha fazla bilgi](site-recovery-failover.md) yük devretme hakkında.
* [Daha fazla bilgi](site-recovery-failback-azure-to-vmware.md) VMware Vm'lerini ve fiziksel sunucuları hakkında başarısız geri

### <a name="if-my-on-premises-host-is-not-responding-or-crashed-can-i-failover-back-tooa-different-host"></a>My şirket içi konak yanıt vermeyen veya çöken değilse yapabilirim yük devretme geri tooa farklı ana bilgisayar?
Evet, hello alternatif konuma kurtarma toofailback tooa farklı ana bilgisayardan Azure kullanabilirsiniz. VMware ve Hyper-v sanal makineleri için aşağıdaki bağlantıları hello hello seçeneklerinde hakkında daha fazlasını okuyun.

* [VMware sanal makineleri için](site-recovery-how-to-failback-azure-to-vmware.md#fail-back-to-the-original-or-alternate-location)
* [Hyper-v sanal makineleri için](site-recovery-failback-from-azure-to-hyper-v.md#failback-to-an-alternate-location)

## <a name="service-providers"></a>Hizmet sağlayıcıları
### <a name="im-a-service-provider-does-site-recovery-work-for-dedicated-and-shared-infrastructure-models"></a>Bir hizmet sağlayıcısı ben. Site Recovery adanmış ve paylaşılan altyapı modelleri için çalışıyor mu?
Evet, Site Recovery hem adanmış hem de paylaşılan altyapı modellerini destekler.

### <a name="for-a-service-provider-is-hello-identity-of-my-tenant-shared-with-hello-site-recovery-service"></a>Bir hizmet sağlayıcısı için hello kimliğini hello Site Recovery hizmetiyle paylaşılır mı?
Hayır. Kiracı kimlik anonim kalır. Kiracılarınızın erişim toohello Site Recovery portalında gerek yoktur. Yalnızca hello hizmet sağlayıcı Yöneticisi hello portal ile etkileşim sağlar.

### <a name="will-tenant-application-data-ever-go-tooazure"></a>Kiracı uygulama verileri, herhangi bir zamanda tooAzure gider mi?
Hizmet sağlayıcının sahip olduğu siteler arasında çoğaltma yapılırken uygulama verileri asla tooAzure gider. Aktarım sırasında ve çoğaltılmış hello hizmet sağlayıcı siteleri arasında doğrudan veri şifrelenir.

TooAzure çoğaltıyorsanız uygulama verilerini tooAzure depolama ancak toohello Site Recovery hizmetine gönderilir. Veriler şifrelenmiş aktarım sırasında ve Azure'da şifrelenmiş olarak kalır.

### <a name="will-my-tenants-receive-a-bill-for-any-azure-services"></a>Kiracılarıma herhangi bir Azure hizmeti için fatura gönderilir mi?
Hayır. Azure'nın faturalama bağlantısı doğrudan hello hizmet sağlayıcı ile kurulur. Hizmet sağlayıcılar, kiracıları için belirli faturaları oluşturmaktan sorumludur.

### <a name="if-im-replicating-tooazure-do-we-need-toorun-virtual-machines-in-azure-at-all-times"></a>TooAzure çoğaltma işlemi gerçekleştirirken Azure toorun sanal makinelerin her zaman ihtiyacımız var?
Hayır, çoğaltılmış tooan aboneliğinizde Azure depolama hesabı verilerdir. Yük devretme testi (DR detayı) veya gerçek bir yük devretme gerçekleştirdiğinizde, Site Recovery otomatik olarak aboneliğinizde sanal makineler oluşturur.

### <a name="do-you-ensure-tenant-level-isolation-when-i-replicate-tooazure"></a>TooAzure çoğaltma yaptığımda Kiracı düzeyinde yalıtım sağlanır mı?
Evet.

### <a name="what-platforms-do-you-currently-support"></a>Şu anda hangi platformları destekliyorsanız?
Azure Pack, Cloud Platform System destekliyoruz ve System Center tabanlı (2012 ve üstü) dağıtımlarının. [Daha fazla bilgi edinin](https://technet.microsoft.com/library/dn850370.aspx) Azure Pack ve Site Recovery tümleştirmesi hakkında.

### <a name="do-you-support-single-azure-pack-and-single-vmm-server-deployments"></a>Tek bir Azure Paketi'ni ve tek bir VMM sunucusu dağıtımını destekliyor musunuz?
Evet, Hyper-V sanal makineleri tooAzure çoğaltabilirsiniz veya hizmet sağlayıcı siteleri arasında.  Hizmet sağlayıcı siteleri arasında çoğaltma yaparsanız Azure runbook tümleştirmesinin kullanılamayacağını unutmayın.

## <a name="next-steps"></a>Sonraki adımlar
* Okuma hello [Site Kurtarma'ya genel bakış](site-recovery-overview.md)
* [Site Recovery mimarisi](site-recovery-components.md) hakkında bilgi edinin.  
