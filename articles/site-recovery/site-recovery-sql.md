---
title: SQL Server ve Azure Site Recovery ile aaaReplicate uygulamalar | Microsoft Docs
description: "Bu makalede nasıl tooreplicate Azure Site Recovery için SQL Server olağanüstü durum özellikleri kullanarak SQL Server."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 99755f2cd2f7e924071f1e230ac4a0bda88f0a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-sql-server-using-sql-server-disaster-recovery-and-azure-site-recovery"></a>SQL Server olağanüstü durum kurtarma ve Azure Site Recovery kullanarak SQL Server koruma

Bu makalede nasıl tooprotect hello SQL Server Yedekleme SQL Server iş devamlılığı ve olağanüstü durum kurtarma (BCDR) teknolojileri kullanan bir uygulama sonuna açıklar ve [Azure Site Recovery](site-recovery-overview.md).

Başlamadan önce yük devretme kümelemesi, Always On kullanılabilirlik grupları, veritabanı yansıtma ve günlük aktarma dahil olmak üzere, SQL Server olağanüstü durum kurtarma özellikleri anladığınızdan emin olun.


## <a name="sql-server-deployments"></a>SQL Server dağıtımları

Birçok iş yükü, bir temel SQL Server kullanmak ve SharePoint, Dynamics ve SAP, tooimplement Veri Hizmetleri gibi uygulamaları ile tümleştirilebilir.  SQL Server çeşitli şekillerde dağıtılabilir:

* **Tek başına SQL Server**: SQL Server ve tüm veritabanlarını tek bir makinede (fiziksel veya sanal) barındırılır. Sanallaştırılmış kümeleme konak yerel yüksek kullanılabilirlik için kullanılır. Konuk düzeyinde yüksek kullanılabilirlik uygulanmadı.
* **SQL Server Yük Devretme Kümelemesi örnekleri (her zaman üzerinde FCI)**: paylaşılan diskler ile instanced SQL Server çalıştıran iki veya daha fazla düğüm, Windows Yük devretme kümesinde yapılandırılır. Bir düğüm kapalı ise, hello küme tooanother örneği üzerinde SQL Server başarısız olabilir. Bu ayar genellikle kullanılan tooimplement yüksek oranda kullanılabilir bir birincil sitede ' dir. Bu dağıtım hatası veya kesinti hello paylaşılan depolama katmanında karşı koruma sağlamaz. Paylaşılan bir diskin iSCSI, fiber kanal veya paylaşılan vhdx'i kullanılarak uygulanabilir.
* **SQL Always On kullanılabilirlik grupları**: iki veya daha fazla düğüm ayarlanır paylaşılan hiçbir şey küme, zaman uyumlu çoğaltma ve otomatik yük devretme ile bir kullanılabilirlik grubunda yapılandırılmış SQL Server veritabanları ile.

 Bu makalede veritabanları tooa uzak site kurtarma için yerel SQL olağanüstü durum kurtarma teknolojileri aşağıdaki hello yararlanır:

* SQL Always On kullanılabilirlik grupları, SQL Server 2012 veya 2014 Enterprise sürümleri için olağanüstü durum kurtarma için tooprovide.
* SQL veritabanı yüksek güvenilirlik modunda, SQL Server 2008 R2 veya SQL Server Standard edition (tüm sürümler) için yansıtma.

## <a name="site-recovery-support"></a>Site kurtarma desteği

### <a name="supported-scenarios"></a>Desteklenen senaryolar
Site Recovery, SQL Server hello tabloda özetlendiği gibi koruyabilirsiniz.

**Senaryo** | **tooa ikincil site** | **tooAzure**
--- | --- | ---
**Hyper-V** | Evet | Evet
**VMware** | Evet | Evet
**Fiziksel sunucu** | Evet | Evet

### <a name="supported-sql-server-versions"></a>Desteklenen SQL Server sürümleri
Bu SQL Server sürümleri, desteklenen hello senaryoları için desteklenir:

* SQL Server 2016 Enterprise ve Standard
* SQL Server 2014 Enterprise ve Standard
* SQL Server 2012 Enterprise ve Standard
* SQL Server 2008 R2 Enterprise ve Standard

### <a name="supported-sql-server-integration"></a>Desteklenen SQL Server Integration

Site Recovery tooprovide bir olağanüstü durum kurtarma çözümü hello tabloda özetlenen yerel SQL Server BCDR teknolojileri ile tümleştirilebilir.

**Özellik** | **Ayrıntılar** | **SQL Server** |
--- | --- | ---
**AlwaysOn kullanılabilirlik grubu** | Tek başına birden çok SQL Server'ın birden fazla düğüme sahip bir yük devretme kümesinde çalıştırın.<br/><br/>Veritabanlarını SQL Server örneklerinde (yansıtılmış) kopyalanabilir ve böylece paylaşılan depolama gerekli yük devretme gruplar halinde gruplandırılabilir.<br/><br/>Bir birincil site ve bir veya daha fazla ikincil siteler arasında olağanüstü durum kurtarma sağlar. İki düğüm bir paylaşılan bir kullanılabilirlik grubuna zaman uyumlu çoğaltma ve otomatik yük devretme kümesi SQL Server veritabanları ile yapılandırılmış hiçbir şey ayarlanabilir. | SQL Server 2014 & 2012 Enterprise edition
**Yük Devretme Kümelemesi (her zaman üzerinde FCI)** | SQL Server yüksek kullanılabilirlik, şirket içi SQL Server iş yükleri için Windows Yük Devretme Kümelemesi yararlanır.<br/><br/>Düğümleri paylaşılan diskler ile SQL Server örneklerini çalıştıran bir yük devretme kümesinde yapılandırılır. Bir örneği çalışmıyorsa hello küme toodifferent bir başarısız olur.<br/><br/>Merhaba küme hatası veya paylaşılan depolama alanında kesintilere karşı koruma sağlamaz. Merhaba paylaşılan disk iSCSI, fiber kanal uygulanabilir veya paylaşılan Vhdx'ler. | SQL Server Enterprise sürümleri<br/><br/>SQL Server Standard edition (yalnızca sınırlı tootwo düğümler)
**Veritabanı yansıtma (yüksek güvenilirlik mod)** | Tek veritabanı tooa tek ikincil kopya korur. Her iki yüksek güvenilirlik (zaman uyumlu) kullanılabilir ve yüksek performans (zaman uyumsuz) çoğaltma modları. Bir yük devretme kümesi gerektirmez. | SQL Server 2008 R2<br/><br/>SQL Server Enterprise tüm sürümler
**Tek başına SQL Server** | Merhaba SQL Server ve veritabanı tek bir sunucuda (fiziksel veya sanal) barındırılır. Merhaba sanal sunucusuysa kümeleme konak yüksek kullanılabilirlik için kullanılır. Konuk düzeyinde yüksek kullanılabilirliği. | Enterprise veya Standard edition

## <a name="deployment-recommendations"></a>Dağıtım önerileri

Bu tablo, SQL Server BCDR teknolojileri Site Recovery ile tümleştirmek için bizim önerileri özetler.

| **Sürüm** | **Sürüm** | **Dağıtım** | **Şirket içi tooon içi** | **Şirket içi tooAzure** |
| --- | --- | --- | --- | --- |
| SQL Server 2012 veya 2014 |Enterprise |Yük devretme kümesi örneği |Always On kullanılabilirlik grupları |Always On kullanılabilirlik grupları |
|| Enterprise |Always On kullanılabilirlik grupları için yüksek kullanılabilirlik |Always On kullanılabilirlik grupları |Always On kullanılabilirlik grupları | |
|| Standart |Yük devretme kümesi örneği (FCI) |Site Recovery çoğaltma yerel yansıtma ile |Site Recovery çoğaltma yerel yansıtma ile | |
|| Enterprise veya Standard |Tek Başına |Site Recovery çoğaltma |Site Recovery çoğaltma | |
| SQL Server 2008 R2 veya 2008 |Enterprise veya Standard |Yük devretme kümesi örneği (FCI) |Site Recovery çoğaltma yerel yansıtma ile |Site Recovery çoğaltma yerel yansıtma ile |
|| Enterprise veya Standard |Tek Başına |Site Recovery çoğaltma |Site Recovery çoğaltma | |
| SQL Server (tüm sürümler) |Enterprise veya Standard |Yük devretme kümesi örneği - DTC uygulama |Site Recovery çoğaltma |Desteklenmiyor |

## <a name="deployment-prerequisites"></a>Dağıtım önkoşulları

* Desteklenen bir SQL Server sürümü çalıştıran bir şirket içi SQL Server dağıtımı. Genellikle, ayrıca Active Directory, SQL server için gerekir.
* Hello gereksinimleri toodeploy istediğiniz senaryo hello. Destek gereksinimleri hakkında daha fazla bilgi edinin [çoğaltma tooAzure](site-recovery-support-matrix-to-azure.md) ve [şirket içi](site-recovery-support-matrix.md), ve [dağıtımının önkoşulları](site-recovery-prereq.md).
* azure'da çalıştırma hello kurtarma yukarı tooset [Azure Sanal Makine Hazırlık Değerlendirmesi](http://www.microsoft.com/download/details.aspx?id=40898) toomake Azure Site Recovery ile uyumlu oldukları emin aracı, SQL Server sanal makinelerde.

## <a name="set-up-active-directory"></a>Active Directory'yi ayarlama ayarlayın

Active Directory doğru hello ikincil kurtarma sitedeki SQL Server toorun için ayarlanmış.

* **Küçük işletme**— hello tüm site toofail istiyorsanız, uygulamalar ve hello şirket içi site için tek bir etki alanı denetleyicisi küçük bir sayı ile Site Recovery çoğaltma tooreplicate hello etki alanı denetleyicisi kullandığınız öneririz toohello ikincil veri merkezine veya tooAzure.
* **Orta toolarge Kurumsal**— uygulamalar, bir Active Directory ormanı bulunan çok sayıda varsa ve uygulama ya da iş yükü tarafından yükü devredilene toofail istediğiniz, ayarladığınız hello ikincil veri merkezinde veya içinde bir ek etki alanı denetleyicisi öneririz Azure. Always On kullanılabilirlik grupları toorecover tooa uzak site kullanıyorsanız, başka bir ek etki alanı denetleyicisi hello ikincil sitedeki veya azure'da hello kurtarılan SQL Server örneği için toouse ayarlamanız önerilir.

Bu makaledeki yönergeleri Hello hello ikincil konumda bir etki alanı denetleyicisinin kullanılabilir olduğunu varsayın. [Daha fazla bilgi](site-recovery-active-directory.md) Active Directory Site Recovery ile koruma hakkında.


## <a name="integrate-with-sql-server-always-on-for-replication-tooazure"></a>SQL Server Always On ile çoğaltma tooAzure için tümleştirme

İşte gerekenler toodo:

1. Komut dosyaları Azure Otomasyon hesabınızda içeri aktarın. Bu hello betikleri toofailover SQL kullanılabilirlik grubu içeren içinde bir [Resource Manager sanal makine](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAG.ps1) ve [Klasik sanal makine](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAGClassic.ps1).

    [![TooAzure dağıtma](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)


1. ASR SQL FailoverAG hello ilk grup hello kurtarma planının bir ön eylem olarak ekleyin.

1. Merhaba kullanılabilirlik grupları hello betik toocreate bir Otomasyon değişkeni tooprovide hello adı kullanılabilir Hello yönergeleri izleyin.

### <a name="steps-toodo-a-test-failover"></a>Adımları toodo yük devretme testi

SQL Always On yerel yük devretme testi desteklemiyor. Bu nedenle, hello şunları öneririz:

1. Ayarlanan [Azure Backup](../backup/backup-azure-vms.md) hello sanal makinedeki, azure'da hello kullanılabilirlik grubu çoğaltması barındırır.

1. Merhaba kurtarma planı yük devretme testi tetiklemeden önce hello sanal makine hello önceki adımda gerçekleştirilecek hello yedekleme kurtarın.

    ![Azure yedekten geri yükleyin ](./media/site-recovery-sql/restore-from-backup.png)

1. [Bir çekirdeği zorlama](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum#PowerShellProcedure) hello sanal makinede yedekten geri.

1. IP hello dinleyici tooan IP hello test yük devretme ağı testinde kullanılabilirse güncelleştirin.

    ![Dinleyici güncelleştirme IP](./media/site-recovery-sql/update-listener-ip.png)

1. Dinleyici çevrimiçi duruma getirin.

    ![Dinleyici çevrimiçi duruma getirme](./media/site-recovery-sql/bring-listener-online.png)

1. Bir yük dengeleyici ön uç IP havuzu karşılık gelen tooeach kullanılabilirlik grubu dinleyicisi altında oluşturulan bir IP ile Merhaba arka uç havuzundaki eklenen hello SQL sanal makinesi oluşturun.

     ![Yük Dengeleyici - ön uç IP havuzu oluştur ](./media/site-recovery-sql/create-load-balancer1.png)

    ![Yük Dengeleyici - arka uç havuzu oluşturma ](./media/site-recovery-sql/create-load-balancer2.png)

1. Bir yük devretme testi hello kurtarma planı yapın.

### <a name="steps-toodo-a-failover"></a>Adımları toodo bir yük devretme

Yük devretme testi yaparak hello kurtarma planı ve doğrulanmış hello kurtarma planı hello betik ekledikten sonra hello kurtarma planı yük devretme yapabilirsiniz.


## <a name="integrate-with-sql-server-always-on-for-replication-tooa-secondary-on-premises-site"></a>Çoğaltma tooa içi ikincil site için SQL Server Always On ile tümleştirme

Merhaba SQL Server kullanılabilirlik gruplarını yüksek kullanılabilirlik (veya bir FCI) kullanıyorsa, kullanılabilirlik grupları da hello kurtarma sitesinde kullanmanızı öneririz. Bu dağıtılmış işlemler kullanmayan tooapps geçerli olduğunu unutmayın.

1. [Veritabanlarını yapılandırma](https://msdn.microsoft.com/library/hh213078.aspx) kullanılabilirlik gruplarına.
1. Bir sanal ağ hello ikincil sitede oluşturun.
1. Merhaba sanal ağ ve hello birincil site arasında bir siteden siteye VPN bağlantısı ayarlayın.
1. Merhaba kurtarma sitesinde bir sanal makine oluşturun ve SQL Server yükleyin.
1. Merhaba varolan Always On kullanılabilirlik grupları toohello genişletmek yeni SQL Server VM. Bu SQL Server örneği bir zaman uyumsuz çoğaltma kopya olarak yapılandırın.
1. Bir kullanılabilirlik grubu dinleyicisi oluşturma veya hello varolan dinleyici tooinclude hello zaman uyumsuz çoğaltma sanal makinesi güncelleştirin.
1. Bu hello uygulama grubu hello dinleyicisi kullanılarak ayarlandığından emin olun. Kurulum hello veritabanı sunucu adını kullanarak yukarı ise, tooreconfigure gerekmeyen şekilde toouse hello dinleyicisi, güncelleştirebilir, hello yük devretme sonrasında.

Dağıtılmış işlemler kullanan uygulamaları için Site Recovery ile dağıttığınız olan öneririz [VMware/fiziksel sunucu siteden siteye çoğaltma](site-recovery-vmware-to-vmware.md).

### <a name="recovery-plan-considerations"></a>Kurtarma planı değerlendirmeleri
1. Bu örnek komut dosyası toohello VMM kitaplığına hello birincil ve ikincil sitelerde ekleyin.

        Param(
        [string]$SQLAvailabilityGroupPath
        )
        import-module sqlps
        Switch-SqlAvailabilityGroup -Path $SQLAvailabilityGroupPath -AllowDataLoss -force

1. Merhaba uygulaması için bir kurtarma planı oluşturduğunuzda, kullanılabilirlik grupları hello betik toofail çağıran bir ön eylem tooGroup-1 komut dosyalı adımı, ekleyin.

## <a name="protect-a-standalone-sql-server"></a>Tek başına SQL Server koruma

Bu senaryoda, Site Recovery çoğaltma tooprotect hello SQL Server makinesinde kullanmanızı öneririz. Merhaba tam adımlar, SQL Server VM veya fiziksel sunucu olup olmadığı ve tooreplicate tooAzure istediğiniz ya da ikincil bir site şirket içi bağlı olacaktır. Hakkında bilgi edinin [Site kurtarma senaryoları](site-recovery-overview.md).

## <a name="protect-a-sql-server-cluster-standard-editionwindows-server-2008-r2"></a>Bir SQL Server kümesi (standard edition/Windows Server 2008 R2) koruma

SQL Server Standard edition veya SQL Server 2008 R2 çalıştıran bir küme için Site Recovery çoğaltma tooprotect SQL Server kullanmanızı öneririz.

### <a name="on-premises-tooon-premises"></a>Şirket içi tooon içi

* Dağıtılmış işlemler Hello uygulama kullanıyorsa, dağıttığınız öneririz [Site Recovery SAN çoğaltması ile](site-recovery-vmm-san.md) bir Hyper-V ortamı için veya [VMware/fiziksel sunucu tooVMware](site-recovery-vmware-to-vmware.md) VMware ortamınız için.
* DTC olmayan uygulamalar için yerel yüksek güvenilirlik DB yansıtma yararlanarak hello yaklaşım toorecover hello küme üzerinde tek başına sunucu olarak kullanın.

### <a name="on-premises-tooazure"></a>Şirket içi tooAzure

Site Recovery, Konuk sunmaz tooAzure çoğaltırken küme desteği. SQL Server Standard edition için düşük maliyetli olağanüstü durum kurtarma çözümü aynısını sağlamaz. Bu senaryoda, hello şirket içi SQL Server küme tooa tek başına SQL Server koruma ve Azure'da kurtarma öneririz.

1. Bir ek tek başına SQL Server örneği hello şirket içi sitede yapılandırırsınız.
1. Merhaba, veritabanları için bir yansıtma hello örneği tooserve yapılandırma tooprotect istiyor. Yüksek güvenilirlik modunda yansıtma yapılandırın.
1. Merhaba şirket içi sitede, site kurtarma için yapılandırma ([Hyper-V](site-recovery-hyper-v-site-to-azure.md) veya [VMware VM'ler/fiziksel sunucular)](site-recovery-vmware-to-azure-classic.md).
1. Site Recovery çoğaltma tooreplicate hello yeni SQL Server örneği tooAzure kullanın. Yüksek güvenilirlik yansıtma kopyası olduğundan, hello birincil kümeyle eşitlenir ancak Site Recovery çoğaltma kullanılarak çoğaltılmış tooAzure görüntülenir.


![Standart küme](./media/site-recovery-sql/standalone-cluster-local.png)

### <a name="failback-considerations"></a>Yeniden çalışma hakkında dikkat edilecek noktalar

SQL Server Standard kümeler için SQL server yedekleme ve geri yükleme, kümeden hello yansıtma örneği toohello özgün, hello yansıtmanın reestablishment ile planlanmamış bir yük devretme sonrasında yeniden çalışma gerektirir.

## <a name="next-steps"></a>Sonraki adımlar
[Daha fazla bilgi edinin](site-recovery-components.md) Site Recovery mimarisi hakkında.
