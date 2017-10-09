---
title: aaaWhat Azure Site Recovery nedir? | Microsoft Belgeleri
description: "Hello Azure Site Recovery hizmetine genel bir bakış sağlar ve dağıtım senaryoları özetlenmektedir."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: e9b97b00-0c92-4970-ae92-5166a4d43b68
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: da6755654b8036a03314ec836f014b64428d5518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-site-recovery"></a>Site Recovery nedir?

Toohello Azure Site Recovery hizmeti Hoş Geldiniz! Bu makalede hello hizmeti hızlı bir genel bakış sağlar.

## <a name="business-continuity-and-disaster-recovery-bcdr-with-azure-recovery-services"></a>Azure Kurtarma Hizmetleri ile iş sürekliliği ve olağanüstü durum kurtarma (BCDR)

Planlı çalışan uygulamalar/iş yükleri ve planlanmayan kesintiler meydana ve kuruluş olarak nasıl verilerinizi güvenli tookeep oluşturacağız çıkışı toofigure gerekir.

Azure kurtarma Hizmetleri tooyour BCDR stratejinize katkıda:

- **Site Recovery hizmeti**: Site Recovery, bir site kullanılamaz hale gelirse uygulamalarınızın kullanılabilen VM’lerde ve fiziksel sunucularda çalışmaya devam etmesini sağlayarak iş sürekliliğine yardımcı olur. Site Recovery, böylece hello birincil site kullanılamıyorsa, ikincil bir konumda kullanılabilir kalır sanal makineleri ve fiziksel sunucularda çalışan iş yüklerini çoğaltır. Olduğunda iş yükleri toohello birincil site ve yeniden çalıştırarak kurtarır.
- **Yedekleme hizmeti**: ek olarak, hello [Azure Backup](https://docs.microsoft.com/azure/backup/) hizmet tutar verilerinizi güvenli ve kurtarılabilir tooAzure yedekleyerek.

Site Recovery, şunlar için çoğaltmayı yönetebilir:

- Azure bölgeleri arasında çoğaltılan Azure VM’leri.
- Sanal makineler ve fiziksel sunucuları tooAzure veya tooa ikincil siteye çoğaltma şirket içi.


## <a name="what-does-site-recovery-provide"></a>Site Recovery ne sağlar?

**Özellik** | **Ayrıntılar**
--- | ---
**Basit bir BCDR çözümü dağıtma** | Site Recovery kullanarak ayarlayabilir ve çoğaltma, yük devretme ve yeniden çalışma hello Azure portal'ın tek bir konumdan yönetin.
**Azure VM’lerini çoğaltma** | BCDR stratejinizi Azure VM’lerinin Azure bölgeleri arasında çoğaltılmasını sağlama şeklinde ayarlayabilirsiniz.
**Şirket içi VM’leri şirket dışına çoğaltma** | Şirket içi sanal makineleri ve fiziksel sunucuları tooAzure veya tooa ikincil şirket içi konumu çoğaltabilirsiniz. Çoğaltma tooAzure hello maliyet ve ikincil veri merkezine koruma karmaşıklığını ortadan kaldırır.
**Dilediğiniz iş yükünü çoğaltın** | Desteklenen Azure VM’lerinde, şirket içi Hyper-V VM'lerinde, VMware VM'lerinde ve Windows/Linux fiziksel sunucularında çalışan tüm iş yüklerini çoğaltın.
**Verileri esnek ve güvenli tutun** | Site Recovery, uygulama verilerini kesintiye uğratmadan çoğaltma işlemlerini yönetir. Çoğaltılan veriler sağlayan hello esneklikle birlikte Azure depolama alanında depolanır. Yük devretme durumunda Azure Vm'leri hello çoğaltılmış verileri temel alınarak oluşturulur.
**RTO ve RPO hedeflerinizi yakalayın** | Kurtarma süresi hedeflerini (RTO) ve kurtarma noktası hedeflerini (RPO) kuruluş sınırları içinde tutun. Site Recovery, Azure VM’leri ve VMware VM’leri için sürekli çoğaltma sağlar ve Hyper-V için çoğaltma sıklığı 30 saniyeye kadar düşer. [Azure Traffic Manager](https://azure.microsoft.com/blog/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/) tümleştirmesi sayesinde kurtarma süresi hedeflerini (RTO) daha da düşürebilirsiniz.
**Yük devretme boyunca uygulamalarınızın tutarlı kalmasını sağlayın** | Uygulama içinde tutarlı anlık görüntülerle kurtarma noktaları yapılandırabilirsiniz. Uygulama içinde tutarlı anlık görüntüler, disk verilerini, bellekteki tüm verileri ve devam eden tüm işlemleri yakalar.
**Kesintisiz test edin** | Yük devretme sınaması işlemlerini kolayca toosupport olağanüstü durum kurtarma ayrıntılarını, devam eden çoğaltmayı etkilemeden de çalıştırabilirsiniz.
**Esnek yük devretme işlemleri gerçekleştirin** | Beklenen kesintilere yönelik olarak sıfır veri kaybıyla planlı yük devretme işlemleri çalıştırabileceğiniz gibi, beklenmeyen olağanüstü durumlar için en düşük düzeyde veri kaybıyla sonuçlanan (çoğaltma sıklığına bağlı olarak) plansız yük devretme işlemleri de çalıştırabilirsiniz. Yeniden kullanılabilir olduğunda kolayca geri tooyour birincil site başarısız olabilir.
**Kurtarma planları oluşturma** | Kurtarma planlarını kullanarak birden çok VM’de çok katmanlı uygulamaların yük devretme ve kurtarma işlemlerini özelleştirebilir ve sıralayabilirsiniz. Makineleri planlar içinde gruplandırabilir, betikler ve el ile gerçekleştirilen eylemler ekleyebilirsiniz. Kurtarma planları, Azure Otomasyonu runbook'ları ile tümleştirilebilir.
**Mevcut BCDR teknolojileriyle tümleştirin** | Site Recovery, diğer BCDR teknolojileriyle tümleşir. Örneğin, Site Recovery tooprotect hello SQL Server arka uç SQL Server AlwaysOn Kullanılabilirlik grupları toomanage hello yük devretme için yerel destek dahil olmak üzere kurumsal iş yüklerinin kullanabilirsiniz.
**Merhaba automation kitaplığı ile tümleştirme** | Zengin Azure Otomasyonu kitaplığı, indirilebilen ve Site Recovery ile tümleştirilebilen üretime hazır ve uygulamaya özgü betikler sağlar.
**Ağ ayarlarını yönetin** | Site Recovery, Azure ile tümleşerek IP adresleri ayırma, yük dengeleyicileri yapılandırma ve etkili ağ değişimleri için Azure Traffic Manager ile tümleştirme dahil olmak üzere uygulama ağ gereksinimlerini basitleştirir.


## <a name="what-can-i-replicate"></a>Neleri çoğaltabilirim?

**Destekleniyor** | **Ayrıntılar**
--- | ---
**Neleri çoğaltabilirim?** | Azure bölgeleri arasında Azure VM’lerini çoğaltma (önizlemede)<br/><br/>  Şirket içi VMware sanal makineleri, Hyper-V sanal makineleri, fiziksel sunucular (Windows ve Linux) tooAzure < br /<br/> Böylece, şirket içi VMware sanal makineleri, Hyper-V sanal makineleri, fiziksel sunucuları tooa ikincil site. Hyper-V konakları System Center VMM tarafından yönetiliyorsa Hyper-V VM'ler için çoğaltma tooa ikincil site yalnızca desteklenir.
**Hangi bölgeler Site Recovery için desteklenir?** | [Desteklenen bölgeler](https://azure.microsoft.com/regions/services/) |
**Çoğaltılan makineler için hangi işletim sistemleri gerekir?** | [Azure VM gereksinimleri](site-recovery-support-matrix-azure-to-azure.md#support-for-replicated-machine-os-versions)<br></br>[VMware VM gereksinimleri](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)<br/><br/> Hyper-V VM’ler için Azure ve Hyper-V tarafından desteklenen tüm [konuk işletim sistemleri](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) desteklenir.<br/><br/> [Fiziksel sunucu gereksinimleri](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)
**Hangi VMware sunucularına/ana bilgisayarlarına ihtiyacımız var?** | VMware VM’leri [desteklenen vSphere konaklarında/vCenter sunucularında](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers) bulunabilir
**Hangi iş yüklerini çoğaltabilirim?** | Desteklenen bir çoğaltma makinesinde çalışan tüm iş yüklerini çoğaltabilirsiniz. Ayrıca, hello Site Recovery takım gerçekleştirdikten için uygulamaya özgü test bir [uygulamaları sayısı](site-recovery-workload.md#workload-summary).


## <a name="azure-portal-considerations"></a>Azure portalı hakkında dikkat edilmesi gerekenler

* Site Recovery hello dağıtılabilir [Azure portal](https://portal.azure.com).
* Hello Klasik Azure Portalı'da, Site Recovery hello Klasik Hizmet Yönetimi modeliyle yönetebilirsiniz.
- Merhaba Klasik portal yalnızca kullanılan toomaintain var olan Site Recovery dağıtımları olmalıdır. Yeni kasa hello Klasik Portalı'nda oluşturulamıyor.

## <a name="next-steps"></a>Sonraki adımlar
* [İş yükü desteği](site-recovery-workload.md) hakkında daha fazla bilgi edinin
* Kullanmaya başlama [bölgeler arasında Azure VM çoğaltma](site-recovery-azure-to-azure.md), [VMware çoğaltma tooAzure](vmware-walkthrough-overview.md), veya [Hyper-V çoğaltma tooAzure](hyper-v-site-walkthrough-overview.md).
