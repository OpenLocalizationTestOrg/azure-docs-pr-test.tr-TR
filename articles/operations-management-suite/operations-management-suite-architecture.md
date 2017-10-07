---
title: "aaaOperations Yönetim Paketi (OMS) mimarisi | Microsoft Docs"
description: "Microsoft Operations Management Suite (OMS), şirket içi ve bulut altyapınızı yönetmenize ve korumanıza yardımcı olan, Microsoft'un bulut tabanlı BT yönetim çözümüdür.  Bu makalede OMS dahil hello farklı hizmetleri tanımlar ve bağlantılar sağlar tootheir ayrıntılı içerik."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 40e41686-7e35-4d85-bbe8-edbcb295a534
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: fa3227aa9c19219009ebe363b7fd2d6565cec59c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-architecture"></a>OMS mimarisi
[Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/services/operations-management-suite/), şirket içi ve bulut ortamlarınızın yönetilmesine yönelik bulut tabanlı hizmetler koleksiyonudur.  Bu makalede hello farklı şirket içi ve bulut bileşenleri OMS ve yüksek düzey bulut bilgi işlem mimarilerini açıklar.  Daha ayrıntılı bilgi için her bir hizmet için toohello belgelerine başvurun.

## <a name="log-analytics"></a>Log Analytics
Tarafından toplanan tüm veriler [günlük analizi](https://azure.microsoft.com/documentation/services/log-analytics/) Azure üzerinde barındırılan hello OMS deposu depolanır.  Bağlı kaynakları hello OMS depoya toplanan verileri oluşturur.  Şu anda desteklenen üç bağlı kaynak türü mevcuttur.

* Yüklü bir aracı bir [Windows](../log-analytics/log-analytics-windows-agents.md) veya [Linux](../log-analytics/log-analytics-linux-agents.md) bilgisayar bağlı doğrudan tooOMS.
* System Center Operations Manager (SCOM) yönetim grubu [tooLog Analytics bağlı](../log-analytics/log-analytics-om-agents.md) .  SCOM aracıları toocommunicate olaylar ve performans verileri tooLog Analytics iletmek yönetim sunucuları ile devam edin.
* Azure'daki bir çalışan rolünden, web rolünden veya sanal makineden [Azure Tanılama](../cloud-services/cloud-services-dotnet-diagnostics.md) verileri toplayan bir [Azure depolama hesabı](../log-analytics/log-analytics-azure-storage.md).

Veri kaynakları günlük analizi olay günlüklerini ve performans sayaçları dahil olmak üzere bağlı kaynaklardan toplar hello veri tanımlayın.  Çözüm işlevselliği tooOMS ekleyin ve tooyour çalışma hello kolayca eklenebilen [OMS Çözümleri Galerisi](../log-analytics/log-analytics-add-solutions.md).  Başkalarının yüklü bir ek aracı toobe gerektirse bazı çözümleri SCOM aracılardan gelen doğrudan bağlantı tooLog Analytics gerektirebilir.

Günlük analizi toomanage OMS Kaynakları kullanın, Ekle ve OMS çözümler, yapılandırmak ve görüntüleyebilir ve hello OMS deposundaki verileri analiz etmek, bir web tabanlı portal sahiptir.

![Log Analytics üst düzey mimarisi](media/operations-management-suite-architecture/log-analytics.png)

## <a name="azure-automation"></a>Azure Otomasyonu
[Azure Otomasyonu runbook'ları](http://azure.microsoft.com/documentation/services/automation) hello Azure bulut yürütülür ve diğer bulut hizmetlerini Azure ya da erişilebilir olan kaynaklara erişim genel Internet hello.  Ayrıca runbook'ların yerel kaynaklara erişebilmesi için [Karma Runbook Çalışanı](../automation/automation-hybrid-runbook-worker.md)'nı kullanarak yerel veri merkezinizde şirket içi makineler atayabilirsiniz.

[DSC yapılandırmaları](../automation/automation-dsc-overview.md) Azure Otomasyonu'nda depolanan doğrudan uygulanan tooAzure sanal makineler olabilir.  Diğer fiziksel ve sanal makine yapılandırmaları hello Azure Otomasyonu DSC istek sunucusundan isteyebilir.

Azure Otomasyonu istatistiklerini görüntüler ve toolaunch hello herhangi bir işlem için Azure portalı bağlanan bir OMS çözümü vardır.

![Azure Otomasyonu üst düzey mimarisi](media/operations-management-suite-architecture/automation.png)

## <a name="azure-backup"></a>Azure Backup
[Azure Backup](http://azure.microsoft.com/documentation/services/backup)'ta korunan veriler belirli bir coğrafi bölgede yer alan bir yedekleme kasasında depolanır.  Merhaba veri çoğaltıldığında içinde hello aynı bölgede ve kasa hello türüne bağlı olarak, daha fazla artıklık çoğaltılmış tooanother bölge de olabilir.

Azure Backup için üç temel senaryo söz konusudur.

* Azure Backup aracısının bulunduğu Windows makine.  Toobackup dosya ve klasörleri herhangi bir Windows server ya da istemci bu sayede doğrudan tooyour Azure yedekleme kasası.  
* System Center Data Protection Manager (DPM) veya Microsoft Azure Backup Sunucusu. Bu, tooleverage DPM veya Microsoft Azure yedekleme sunucusu toobackup dosyaları ve klasörleri ayrıca tooapplication iş yükleri SQL ve SharePoint toolocal depolama ve ardından çoğaltma tooyour Azure yedekleme kasası gibi sağlar.
* Azure Sanal Makine Uzantıları.  Bu, toobackup Azure sanal makineleri tooyour Azure yedekleme kasası sağlar.

Azure yedekleme istatistiklerini görüntüler ve toolaunch hello herhangi bir işlem için Azure portalı bağlanan bir OMS çözümü vardır.

![Azure Backup üst düzey mimarisi](media/operations-management-suite-architecture/backup.png)

## <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery); sanal makine ve fiziksel sunucu çoğaltma, yük devretme ve yeniden çalışma işlemlerini düzenler. Çoğaltma verilerinin veya hello veri merkezi ve Azure depolama Hyper-V konakları, VMware hiper yöneticileri ve birincil ve ikincil veri merkezlerinde fiziksel sunucuları arasında paylaşılmaz.  Site Recovery, belirli bir coğrafi Azure bölgesinde yer alan kasalardaki meta verileri depolar. Hiçbir çoğaltılan veriler Site Recovery hizmeti hello tarafından depolanır.

Azure Site Recovery için üç temel çoğaltma senaryosu söz konusudur.

**Hyper-V sanal makinelerini çoğaltma**

* VMM bulutlarındaki Hyper-V sanal makineleri yönetiliyorsa tooa ikincil veri merkezi veya tooAzure depolama çoğaltabilirsiniz.  Çoğaltma tooAzure güvenli bir internet bağlantısıdır.  Çoğaltma tooa ikincil veri merkezine hello LAN ' dir.
* Hyper-V sanal makineleri VMM tarafından yönetilmeyen, yalnızca tooAzure depolama çoğaltabilirsiniz.  Çoğaltma tooAzure güvenli bir internet bağlantısıdır.

**VMWare sanal makinelerini çoğaltma**

* VMware veya tooAzure depolama çalıştıran VMware sanal makineleri tooa ikincil veri merkezine çoğaltabilirsiniz.  Çoğaltma tooAzure bir siteden siteye VPN veya Azure ExpressRoute veya güvenli bir Internet bağlantısı üzerinden oluşabilir. Çoğaltma tooa ikincil veri merkezine hello Inmage Scout veri kanalı gerçekleşir.

**Fiziksel Windows ve Linux sunucularını çoğaltma** 

* Fiziksel sunucuları tooa ikincil veri merkezi ya da tooAzure depolama çoğaltabilirsiniz. Çoğaltma tooAzure bir siteden siteye VPN veya Azure ExpressRoute veya güvenli bir Internet bağlantısı üzerinden oluşabilir. Çoğaltma tooa ikincil veri merkezine hello Inmage Scout veri kanalı gerçekleşir.  Azure Site Recovery için bazı istatistiklerini görüntüler OMS çözümünü olsa da, herhangi bir işlem hello Azure portalını kullanmanız gerekir.

![Azure Site Recovery üst düzey mimarisi](media/operations-management-suite-architecture/site-recovery.png)

## <a name="next-steps"></a>Sonraki adımlar
* [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) hakkında bilgi edinme.
* [Azure Otomasyonu](https://azure.microsoft.com/documentation/services/automation) hakkında bilgi edinme.
* [Azure Backup](http://azure.microsoft.com/documentation/services/backup) hakkında bilgi edinme.
* [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) hakkında bilgi edinme.

