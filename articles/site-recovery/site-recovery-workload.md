---
title: "aaaWhat iş yükleri için Azure Site Recovery ile korumak?"
description: "Merhaba çoğaltma, yük devretme ve şirket içi sanal makinelerin ve fiziksel sunucuları tooAzure veya tooa içi ikincil site kurtarma iletişime geçerek Azure Site Recovery iş yüklerini ve uygulamaları korur"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: 4953948f-26c0-4699-8fe7-59d3bfc1d3da
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/08/2017
ms.author: raynew
ms.openlocfilehash: cab2e1ce3c2b7b2c5f899d957219f5c12eb5965c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-workloads-can-you-protect-with-azure-site-recovery"></a>Azure Site Recovery ile hangi iş yüklerini koruyabilirsiniz?
Bu makalede, iş yüklerini ve uygulamaları hello Azure Site Recovery hizmeti ile çoğaltabilirsiniz açıklanmaktadır.

Tüm yorumlarınızı ve sorularınızı bu makalenin veya hello hello altındaki sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="overview"></a>Genel Bakış
Kuruluşlar, iş devamlılığı ve olağanüstü durum kurtarma (BCDR) stratejinize tookeep iş yüklerinin ve verilerin planlanmış ve Planlanmamış kapalı kalma süresi sırasında güvenli ve kullanılabilir gerekir ve tooregular çalışma koşullarına mümkün olan en kısa sürede kurtarın.

Site Recovery, tooyour BCDR stratejinize katkı sağlayan bir Azure hizmetidir. Site Kurtarma'yı kullanarak, uygulamaya duyarlı çoğaltma toohello Bulut veya tooa ikincil site dağıtabilirsiniz. Olup uygulamalarınızın Windows tabanlı veya Linux tabanlı, fiziksel sunucularda, Vmware'de ya da Hyper-V, çalışan, Site Recovery tooorchestrate çoğaltma, olağanüstü durum kurtarma testi gerçekleştirmek ve kullanabilirsiniz yük devretme ve yeniden çalıştırın.

Site Recovery; SharePoint, Exchange, Dynamics, SQL Server ve Active Directory dahil olmak üzere Microsoft uygulamalarıyla tümleşik bir şekilde çalışır. Microsoft; Oracle, SAP, IBM ve Red Hat gibi önde gelen satıcılarla da yakın bir şekilde çalışır. Çoğaltma çözümlerini her uygulama için ayrı olarak özelleştirebilirsiniz.

## <a name="why-use-site-recovery-for-application-replication"></a>Uygulama çoğaltma için neden Site Recovery'yi kullanmam gerekir?
Site Recovery, tooapplication düzeyinde koruma ve kurtarma gibi katkıda bulunur:

* Desteklenen makinede çalışan iş yükleri için uygulaması belirsiz çoğaltma.
* RPO değerleriyle Itanium tabanlı sistemler için 30 saniye toomeet hello gereksinimleri en kritik iş uygulamalarının yakın zaman uyumlu çoğaltma.
* Tek veya çok katmanlı uygulamalar için uygulamayla tutarlı anlık görüntüler.
* SQL Server AlwaysOn tümleştirmesinin yanı sıra, AD çoğaltması, SQL AlwaysOn, Exchange Veritabanı Kullanılabilirlik Grupları (DAG'ler) ve Oracle Data Guard'ın içinde bulunduğu diğer uygulama düzeyi çoğaltma teknolojileriyle ortaklık.
* Tek bir tıklatmayla tüm uygulama yığınını toorecover sağlayan ve tooinclude dış komut dosyaları ve el ile gerçekleştirilen eylemleri hello plana dahil esnek kurtarma planları.
* Site Recovery ve Azure toosimplify ağ yönetimi Gelişmiş hello özelliği tooreserve IP adresleri de dahil olmak üzere, uygulama ağ gereksinimlerini Yük Dengeleme ve tümleştirme Azure Traffic Manager ile düşük RTO ağ geçişleri için yapılandırın.
* İndirilebilen ve kurtarma planlarıyla tümleştirilebilen üretime hazır ve uygulamaya özgü betikler sağlayan zengin bir otomasyon kitaplığı.

## <a name="workload-summary"></a>İş yükü özeti
Site Recovery, desteklenen bir makinede çalışan herhangi bir uygulamayı çoğaltabilir. Ayrıca uygulamaya özgü ek sınama çıkışı ürün ekipleri toocarry ile işbirliği yaptık.

| **İş yükü** | **Hyper-V sanal makineleri tooa ikincil siteye çoğaltma** | **Hyper-V sanal makineleri tooAzure Çoğalt** | **VMware Vm'lerini tooa ikincil siteye çoğaltma** | **VMware Vm'leri tooAzure Çoğalt** |
| --- | --- | --- | --- | --- |
| Active Directory, DNS |E |E |E |E |
| Web uygulamaları (IIS, SQL) |E |E |E |E |
| System Center Operations Manager |E |E |E |E |
| SharePoint |E |E |E |E |
| SAP<br/><br/>Küme olmayan için SAP sitesini tooAzure Çoğalt |E (Microsoft tarafından test edildi) |E (Microsoft tarafından test edildi) |E (Microsoft tarafından test edildi) |E (Microsoft tarafından test edildi) |
| Exchange (DAG olmayan) |E |E |E |E |
| Uzak Masaüstü/VDI |E |E |E |Yok |
| Linux (işletim sistemi ve uygulamalar) |E (Microsoft tarafından test edildi) |E (Microsoft tarafından test edildi) |E (Microsoft tarafından test edildi) |E (Microsoft tarafından test edildi) |
| Dynamics AX |E |E |E |E |
| Dynamics CRM |E |Çok yakında |E |Çok yakında |
| Oracle |E (Microsoft tarafından test edildi) |E (Microsoft tarafından test edildi) |E (Microsoft tarafından test edildi) |E (Microsoft tarafından test edildi) |
| Windows Dosya Sunucusu |E |E |E |E |
| Citrix XenApp ve XenDesktop |Yok |E |Yok |E |

## <a name="replicate-active-directory-and-dns"></a>Active Directory'yi ve DNS'yi çoğaltma
Bir Active Directory ve DNS altyapısı temel toomost Kurumsal uygulamaları şunlardır. Olağanüstü durum kurtarma sırasında tooprotect gerekir ve iş yüklerinizi ve uygulamalarınızı kurtarmadan önce bu altyapı bileşenlerini kurtarın.

Site Recovery toocreate tam otomatik olağanüstü durum kurtarma planı, Active Directory ve DNS için kullanabilirsiniz. Örneğin, SharePoint ve SAP birincil tooa ikincil siteden üzerinden toofail istiyorsanız, Active Directory ilk başarısız bir kurtarma planı ayarlayabilirsiniz ve ardından başka bir uygulamaya özgü kurtarma planı toofail hello etkin kullanan diğer uygulamalar Dizin.

Active Directory'yi ve DNS'yi koruma hakkında [daha fazla bilgi edinin](site-recovery-active-directory.md).

## <a name="protect-sql-server"></a>SQL Server'ı koruma
SQL Server, şirket içi bir veri merkezinde birçok iş uygulamasına yönelik veri hizmetleri için bir veri hizmetleri altyapısı sağlar.  Site Recovery, SQL Server kullanan tooprotect çok katmanlı Kurumsal uygulamaları SQL Server HA/DR teknolojileriyle birlikte kullanılabilir. Site Recovery şunları sağlar:

* SQL Server için basit ve ekonomik bir olağanüstü durum kurtarma çözümü. Birden çok sürümleri ve SQL Server tek başına sunucular ve kümeler, tooAzure veya tooa ikincil site sürümleri çoğaltılır.  
* SQL AlwaysOn Kullanılabilirlik grupları, toomanage yük devretme ve yeniden çalışma Azure Site Recovery kurtarma planlarında ile tümleştirme.
* Uçtan uca kurtarma Merhaba hello SQL Server veritabanları dahil olmak üzere bir uygulamadaki tüm katmanlar planları.
* SQL Server'ın, azami yükleri Site Recovery ile Azure içindeki daha büyük IaaS sanal makinesi boyutlarına "yığılarak" ölçeklendirilmesi.
* Kolay SQL Server olağanüstü durum kurtarma testi Yük devretme sınaması işlemlerini tooanalyze veri çalıştırın ve üretim ortamınızı etkilemeden uyumluluk denetimlerini çalıştırın.

SQL Server'ı koruma hakkında [daha fazla bilgi edinin](site-recovery-sql.md).

## <a name="protect-sharepoint"></a>SharePoint'i koruma
Azure Site Recovery, SharePoint dağıtımlarının korunmasına şu şekilde yardımcı olur:

* Merhaba gereksinimi ve olağanüstü durum kurtarma için yedek grubu için ilgili altyapı maliyetini ortadan kaldırır. Site Recovery tooreplicate bir grubun tümünü (Web, uygulama ve veritabanı katmanları) tooAzure veya tooa ikincil sitesi kullanın.
* Uygulama dağıtımını ve yönetimini basitleştirir. Dağıtılan güncelleştirmelerin toohello birincil site otomatik olarak çoğaltılır ve böylece yük devretme ve kurtarma grubundan bir ikincil sitedeki sonra kullanılabilir. Merhaba yönetim karmaşıklığı ve beklemeyi grubun güncel tutulmasına ilişkin maliyetleri de düşürür.
* Test ve hata ayıklama işlemleri için üretim benzeri isteğe bağlı bir kopya çoğaltma ortamı oluşturarak SharePoint uygulaması için geliştirme sürecini basitleştirir.
* Site Recovery toomigrate SharePoint dağıtımlarını tooAzure kullanarak geçiş toohello bulut basitleştirir.

SharePoint'i koruma hakkında [daha fazla bilgi edinin](site-recovery-sharepoint.md).

## <a name="protect-dynamics-ax"></a>Dynamics AX'i koruma
Azure Site Recovery, Dynamics AX ERP çözümünüzün korunmasına şu şekillerde yardımcı olur:

* Tüm Dynamics AX ortamınızı (Web ve AOS katmanları, veritabanı katmanları, SharePoint) çoğaltılmasını tooAzure, veya tooa ikincil site.
* Dynamics AX dağıtımlarının toohello buluta (Azure'a) geçişini basitleştirir.
* Test ve hata ayıklama işlemleri için üretim benzeri isteğe bağlı bir kopya oluşturarak Dynamics AX uygulamasının geliştirme ve test sürecini basitleştirir.

Dynamic AX'i koruma hakkında [daha fazla bilgi edinin](site-recovery-dynamicsax.md) 

## <a name="protect-rds"></a>RDS'yi koruma
Uzak Masaüstü Hizmetleri (RDS) sanal masaüstü altyapısı (VDI), oturum tabanlı masaüstlerini ve uygulamaları, kullanıcıların toowork herhangi bir yere etkinleştirir. Azure Site Recovery ile şunları yapabilirsiniz:

* Yönetilen veya yönetilmeyen havuza alınmış sanal masaüstlerini tooa ikincil site ve uzak uygulamaları ve oturumları tooa ikincil site veya Azure çoğaltılır.
* Şunları çoğaltabilirsiniz:

| **RDS** | **Hyper-V sanal makineleri tooa ikincil siteye çoğaltma** | **Hyper-V sanal makineleri tooAzure Çoğalt** | **VMware Vm'lerini tooa ikincil siteye çoğaltma** | **VMware Vm'leri tooAzure Çoğalt** | **Fiziksel sunucuları tooa ikincil siteye çoğaltma** | **Fiziksel sunucuları tooAzure Çoğalt** |
| --- | --- | --- | --- | --- | --- | --- |
| **Havuza Alınmış Sanal Masaüstü (yönetilmeyen)** |Evet |Hayır |Yes |Hayır |Yes |Hayır |
| **Havuza Alınmış Sanal Masaüstü (yönetilen ve UPD'siz)** |Evet |Hayır |Yes |Hayır |Yes |Hayır |
| **Uzak uygulamalar ve Masaüstü oturumları (UPD'siz)** |Evet |Evet |Evet |Evet |Evet |Yes |

RDS'yi koruma hakkında [daha fazla bilgi edinin](https://gallery.technet.microsoft.com/Remote-Desktop-DR-Solution-bdf6ddcb).

## <a name="protect-exchange"></a>Exchange'i koruma
Site Recovery, Exchange'in korunmasına şu şekilde yardımcı olur:

* Tek veya tek başına sunucular gibi küçük Exchange dağıtımları için Site Recovery çoğaltabilir ve tooAzure veya tooa ikincil sitesi başarısız.
* Site Recovery, daha büyük dağıtımlar için Exchange DAG'leri ile tümleşir.
* Exchange Dag'leri çözüm bir kuruluştaki Exchange olağanüstü durum kurtarma için önerilen hello ' dir.  Site Recovery kurtarma planları Dag'leri, siteler arasında tooorchestrate DAG yük devretme içerebilir.

Exchange'i koruma hakkında [daha fazla bilgi edinin](https://gallery.technet.microsoft.com/Exchange-DR-Solution-using-11a7dcb6).

## <a name="protect-sap"></a>SAP'yi koruma
Site Recovery tooprotect SAP dağıtımınızı şu şekilde kullanın:

* Şirket içi bileşenleri tooAzure yineleyerek çalışan SAP NetWeaver ve NetWeaver üretim dışı uygulamalarının korumasını etkinleştirin.
* Bileşenleri tooanother Azure veri merkezi yineleyerek Azure, çalışan SAP NetWeaver ve NetWeaver üretim dışı uygulamalarının korumasını etkinleştirin.
* Buluta geçiş, Site Recovery toomigrate kullanarak SAP dağıtım tooAzure basitleştirin.
* SAP uygulamaları test etmek için talep üzerine üretim kopyası oluşturarak SAP proje yükseltmelerini, testlerini ve prototip oluşturma işlemlerini basitleştirin.

SAP'yi koruma hakkında [daha fazla bilgi edinin](site-recovery-sap.md).

## <a name="protect-iis"></a>IIS Koruma
Site Recovery tooprotect IIS dağıtımınız aşağıdaki şekilde kullanın:

Azure Site Recovery ortamı tooa soğuk uzak siteniz veya Microsoft Azure gibi genel bulut kritik bileşenlerinde hello yineleyerek olağanüstü durum kurtarma sağlar. Çoğaltılmış toohello kurtarma sitesi Hello sanal makineyle hello web sunucusu ve hello veritabanı olan beri gereksinim toobackup yapılandırma dosyalarını veya yoktur sertifikaları ayrı olarak. uygulama eşlemeleri hello ve değiştirilen gönderme yük devretme ortam değişkenleri bağlamaları bağımlı hello olağanüstü durum kurtarma planları tümleşik komut dosyaları aracılığıyla güncelleştirilebilir. Sanal makineler hello kurtarma sitesinde yalnızca bir yük devretme hello olay getirdiği. Yalnızca bu, Azure Site Recovery ayrıca hello son tooend yük devretme yetenekleri aşağıdaki hello sağlayarak düzenlemek yardımcı olur:

-   Sıralama hello kapatma ve sanal makinelerin başlangıç çeşitli katmanları hello.
-   Bunlar başlatılmış sonra uygulama bağımlılıklarını ve bağlamaları betikleri tooallow güncelleştirmesini hello sanal makineleri ekleniyor. Merhaba komut dosyaları da kullanılan tooupdate hello DNS sunucusu toopoint toohello kurtarma sitesi olabilir.
-   IP adreslerini toovirtual makineler öncesi yük devretme hello birincil ve kurtarma ağları eşleyerek ayırabilir ve bu nedenle güncelleştirilmiş toobe post yük devretme gerekmez betiklerini kullanın.
-   Böylece hello kapsam için bir olağanüstü durum hello olay karışıklığı ortadan kaldırılır hello web sunucularında, birden çok web uygulamaları için tek tıklamayla yük devretme özelliği.
-   DR ayrıntısına için yalıtılmış bir ortamda özelliği tootest hello kurtarma planları.

IIS web grubunu koruma hakkında [daha fazla bilgi edinin](https://aka.ms/asr-iis).

## <a name="protect-citrix-xenapp-and-xendesktop"></a>Citrix XenApp ve XenDesktop’u koruma
Site Recovery tooprotect, Citrix XenApp ve XenDesktop dağıtımlarınızın aşağıdaki şekilde kullanın:

* (AD DNS sunucusu, SQL veritabanı sunucusu, Citrix teslim denetleyicisi mağaza sunucusu XenApp ana (VDA), Citrix XenApp lisans) dahil olmak üzere hello farklı dağıtım çoğaltma tarafından Citrix XenApp ve XenDesktop dağıtımı etkinleştir koruma katmanları tooAzure.
* Buluta geçiş, Citrix XenApp ve XenDesktop dağıtım tooAzure Site Recovery toomigrate kullanarak basitleştirin.
* Test ve hata ayıklama uygulamaları için isteğe bağlı üretim benzeri bir kopya oluşturarak Citrix XenApp/XenDesktop testlerini basitleştirin.
* Bu çözüm yalnızca Windows Server işletim sistemi sanal masaüstleri için geçerli olup, istemci sanal masaüstlerinin lisanslaması Azure’da henüz desteklenmediğinden istemci sanal masaüstleri için geçerli değildir.
Azure’da istemci/sunucu masaüstlerini lisanslama hakkında [daha fazla bilgi edinin](https://azure.microsoft.com/pricing/licensing-faq/).

Citrix XenApp ve XenDesktop dağıtımlarını koruma hakkında [daha fazla bilgi edinin](site-recovery-citrix-xenapp-and-xendesktop.md). Alternatif olarak, hello başvurabilir [teknik incelemesi Citrix gelen](https://aka.ms/citrix-xenapp-xendesktop-with-asr) ayrıntılı, hello aynı.

## <a name="next-steps"></a>Sonraki adımlar
[Önkoşulları denetleme](site-recovery-prereq.md)
