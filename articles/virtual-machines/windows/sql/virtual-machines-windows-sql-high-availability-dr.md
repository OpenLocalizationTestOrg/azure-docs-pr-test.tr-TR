---
title: "aaaHigh kullanılabilirlik ve olağanüstü durum kurtarma için SQL Server | Microsoft Docs"
description: "Tartışma için Azure sanal makinelerinde çalışan SQL Server için çeşitli türlerde HADR stratejileri hello."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 53981f7e-8370-4979-b26a-93a5988d905f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: mikeray
ms.openlocfilehash: 2b62d8b30520952ba6b7da7177a2c2de95bea8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-and-disaster-recovery-for-sql-server-in-azure-virtual-machines"></a>Azure Sanal Makineler’de SQL Server için yüksek kullanılabilirlik ve olağanüstü durum kurtarma

Microsoft Azure sanal makinelerle (VM'ler) SQL Server yüksek kullanılabilirlik ve olağanüstü durum kurtarma (HADR) veritabanı çözümü daha düşük hello maliyeti yardımcı olabilir. SQL Server HADR çözümlerinin çoğu hem de yalnızca Azure karma çözüm olarak Azure sanal makinelerde desteklenir. Yalnızca Azure bir çözümde hello tüm HADR sistem Azure üzerinde çalışır. Bir karma yapılandırmasında hello çözümün parçası Azure üzerinde çalışır ve diğer bölümü çalıştırır şirket içi kuruluşunuzdaki hello. Merhaba hello Azure ortamı esnekliğini toomove sağlar kısmen veya tamamen sistemleri veritabanı tooAzure toosatisfy hello bütçe ve SQL Server'ın HADR gereksinimleri.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="understanding-hello-need-for-an-hadr-solution"></a>HADR çözümünü hello gereksinimini anlama
Bu, tooyou tooensure veritabanı sisteminizdeki hello hizmet düzeyi sözleşmesi (SLA) gerektiren hello HADR yetenekleri sahip olduğunu gösterir. Azure bulut Hizmetleri ve sanal makineler için hata kurtarma algılama için hizmet onarma gibi yüksek kullanılabilirlik mekanizmaları sağlar hello olgu kendisini istenen hello SLA karşılayabilecek garanti etmez. Bu mekanizmaların hello VM'ler yüksek kullanılabilirliğini hello ancak değil yüksek kullanılabilirliğini hello VM'ler içinde çalışan SQL Server hello koruyun. Merhaba VM çevrimiçi ve iyi durumda olsa da hello SQL Server örneği toofail için mümkündür. Ayrıca, Azure tarafından sağlanan çift hello yüksek kullanılabilirlik mekanizmaları hello VM'ler kalma süresi için izin yazılım veya donanım hataları ve işletim sistemi yükseltmeleri kurtarma gibi son tooevents.

Ayrıca, coğrafi olarak yedekli depolama (GRS) coğrafi çoğaltma adlı bir özelliği ile uygulanır, Azure bir veritabanınız için yeterli olağanüstü durum kurtarma çözümü olmayabilir. Coğrafi çoğaltma veri zaman uyumsuz olarak gönderdiğinden, en son güncelleştirmeleri olağanüstü durum hello olayda kaybedilebilir. Coğrafi çoğaltma sınırlamalar hakkında daha fazla bilgi hello ele alınmıştır [coğrafi çoğaltma veri ve günlük dosyalarını ayrı diskler üzerinde desteklenmiyor](#geo-replication-support) bölümü.

## <a name="hadr-deployment-architectures"></a>HADR dağıtım mimarisi
Azure'da desteklenen SQL Server HADR teknolojileri şunları içerir:

* [Always On kullanılabilirlik grupları](https://technet.microsoft.com/library/hh510230.aspx)
* [Her zaman yük devretme kümesi örnekleri](https://technet.microsoft.com/library/ms189134.aspx)
* [Günlük aktarma](https://technet.microsoft.com/library/ms187103.aspx)
* [SQL Server Yedekleme ve geri yükleme ile Azure Blob Depolama Birimi hizmeti](https://msdn.microsoft.com/library/jj919148.aspx)
* [Veritabanı yansıtma](https://technet.microsoft.com/library/ms189852.aspx) - SQL Server 2016'de kullanım dışı

Bu, olası toocombine hello teknolojileri birlikte tooimplement yüksek kullanılabilirlik ve olağanüstü durum kurtarma özelliklerine sahip bir SQL Server çözüm olur. Kullandığınız hello teknolojisine bağlı olarak, karma bir dağıtım hello Azure sanal ağı ile VPN tüneli gerektirebilir. Aşağıdaki bölümler Hello hello örnek dağıtım mimarilerinin bazıları gösterir.

## <a name="azure-only-high-availability-solutions"></a>Yalnızca Azure: yüksek oranda kullanılabilirlik çözümleri

Always On kullanılabilirlik kullanılabilirlik grupları adı verilen grupları ile-veritabanı düzeyinde SQL Server için yüksek oranda kullanılabilirlik çözümü olabilir. Yüksek oranda kullanılabilirlik çözümü bir örnek düzeyinde her zaman üzerinde yük devretme kümesi örnekleri ile - yük devretme kümesi örnekleri oluşturabilirsiniz. Ek artıklık için kullanılabilirlik grupları yük devretme kümesi örnekleri oluşturarak iki düzeyde artıklık oluşturabilirsiniz. 

| Teknoloji | Örnek mimarisi |
| --- | --- |
| **Kullanılabilirlik grupları:** |Azure Vm'lerinde çalışan kullanılabilirlik çoğaltmalarının hello aynı bölge yüksek kullanılabilirlik sağlar. Windows Yük Devretme Kümelemesi bir Active Directory etki alanı gerektirdiğinden tooconfigure VM, etki alanı denetleyicisi gerekir.<br/> ![Kullanılabilirlik grupları:](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_ha_always_on.gif)<br/>Daha fazla bilgi için bkz: [kullanılabilirlik gruplarını yapılandırma Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md). |
| **Yük devretme kümesi örnekleri** |Paylaşılan depolama gerektirir, yük devretme kümesi örneği'ne (FCI) 3 farklı yollarla oluşturulabilir.<br/><br/>1. Bağlı depolama kullanarak Azure Vm'lerde çalıştıran iki düğümlü bir yük devretme [Windows Server 2016 depolama alanları doğrudan \(S2D\) ](virtual-machines-windows-portal-sql-create-failover-cluster.md) tooprovide yazılım tabanlı bir sanal SAN.<br/><br/>2. Bir üçüncü taraf kümeleme çözümü tarafından desteklenen depolama ile Azure Vm'lerde çalıştıran iki düğümlü yük devretme kümesi. SIOS DataKeeper kullanan bir örnek için bkz: [yüksek kullanılabilirlik için Yük Devretme Kümelemesi ve 3 taraf yazılımları SIOS DataKeeper kullanarak bir dosya paylaşımı](https://azure.microsoft.com/blog/high-availability-for-a-file-share-using-wsfc-ilb-and-3rd-party-software-sios-datakeeper/).<br/><br/>3. Azure Vm'lerinde uzak iSCSI hedef paylaşılan blok depolama ile ExpressRoute aracılığıyla çalıştıran iki düğümlü yük devretme kümesi. Örneğin, NetApp özel depolama (NPS), ExpressRoute aracılığıyla iSCSI hedefi Equinix tooAzure VM'ler ile kullanıma sunar.<br/><br/>Üçüncü taraf paylaşılan depolama alanı ve veri çoğaltma çözümleri için herhangi bir yük devretme sorunları ilgili tooaccessing veri hello satıcısına başvurmanız gerekir.<br/><br/>Bu kullanarak not üstünde FCI [Azure File storage](https://azure.microsoft.com/services/storage/files/) Bu çözüm, Premium depolama alanını değil çünkü henüz desteklenmiyor. Bu yakında toosupport çalışıyoruz. |

## <a name="azure-only-disaster-recovery-solutions"></a>Yalnızca Azure: olağanüstü durum kurtarma çözümleri
Kullanılabilirlik grupları, veritabanı yansıtma veya Yedekleme kullanarak Azure, SQL Server veritabanları için olağanüstü durum kurtarma çözümüne sahip ve depolama BLOB'lar ile geri yükleyin.

| Teknoloji | Örnek mimarisi |
| --- | --- |
| **Kullanılabilirlik grupları:** |Olağanüstü durum kurtarma için Azure VM'de birden çok veri merkezi arasında çalışan kullanılabilirlik çoğaltmalarının. Bu bölgeler arası çözüm eksiksiz site kesilmesine karşı korur. <br/> ![Kullanılabilirlik grupları:](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_alwayson.png)<br/>Bir bölge içinde tüm çoğaltmalar Merhaba içinde aynı bulut hizmeti ve aynı sanal ağı hello olması gerekir. Her bölge ayrı VNet olmanız gerekir, çünkü bu çözümleri VNet tooVNet bağlantısı gerektirir. Daha fazla bilgi için bkz: [hello Azure portal yapılandırma bir VNet-VNet bağlantısı kullanarak](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md). Ayrıntılı yönergeler için bkz: [de farklı bölgelerdeki Azure Virtual Machines'de SQL Server kullanılabilirlik grubu yapılandırma](virtual-machines-windows-portal-sql-availability-group-dr.md).|
| **Veritabanı yansıtma** |Asıl ve yansıtma ve olağanüstü durum kurtarma için farklı veri merkezlerinde çalıştıran sunucular. Bir active directory etki alanı birden çok veri merkezi yayılamaz sunucu sertifikaları kullanarak dağıtmanız gerekir.<br/>![Veritabanı yansıtma](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_dbmirroring.gif) |
| **Yedekleme ve geri yükleme ile Azure Blob Depolama Birimi hizmeti** |Üretim veritabanları doğrudan tooblob depolama olağanüstü durum kurtarma için farklı bir veri merkezinde yedeklendi.<br/>![Yedekleme ve Geri Yükleme](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_backup_restore.gif)<br/>Daha fazla bilgi için bkz: [yedekleme ve Azure Virtual Machines'de SQL Server için geri yükleme](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="hybrid-it-disaster-recovery-solutions"></a>Karma BT: Olağanüstü durum kurtarma çözümleri
Kullanılabilirlik grupları, veritabanı yansıtma, günlük aktarma ve Yedekleme kullanarak karma BT ortamında, SQL Server veritabanları için olağanüstü durum kurtarma çözümüne sahip ve Azure blogu depolama ile geri yükleyin.

| Teknoloji | Örnek mimarisi |
| --- | --- |
| **Kullanılabilirlik grupları:** |Azure Vm'leri ve şirket içi siteler arası olağanüstü durum kurtarma için çalışan diğer çoğaltmaları çalışan bazı kullanılabilirlik çoğaltmalarının. Merhaba üretim site ya da şirket içi olabilir veya bir Azure veri merkezi.<br/>![Kullanılabilirlik grupları:](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_alwayson.gif)<br/>Tüm kullanılabilirlik çoğaltmalarının olması gerektiğinden aynı yük devretme kümesi, hello hello küme hem ağları (birden çok alt ağ yük devretme kümesi) yayılmış gerekir. Bu yapılandırma, Azure ve hello şirket içi ağ arasında bir VPN bağlantısı gerektirir.<br/><br/>Veritabanlarınızın başarılı olağanüstü durum kurtarma için bir kopya etki alanı denetleyicisi hello olağanüstü durum kurtarma sitesinde de yüklemeniz gerekir.<br/><br/>Bu, olası toouse hello Ekle çoğaltma Sihirbazı'nda SSMS tooadd her zaman kullanılabilirlik grubu üzerinde var olan bir Azure çoğaltma tooan olur. Daha fazla bilgi için bkz: her zaman üzerindeki kullanılabilirlik grubu tooAzure genişletir. |
| **Veritabanı yansıtma** |Bir Azure VM ve hello diğer çalışan bir iş ortağı şirket içi sunucu sertifikaları kullanarak siteler arası olağanüstü durum kurtarma için çalışıyor. İş ortakları, toobe gerek yoktur aynı Active Directory etki alanı hello ve hiçbir VPN bağlantısı gereklidir.<br/>![Veritabanı yansıtma](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_dbmirroring.gif)<br/>Bir ortak bir Azure VM'de çalıştıran başka bir veritabanı yansıtma senaryo içerir ve hello diğer çalışan hello aynı şirket içi siteler arası olağanüstü durum kurtarma için Active Directory etki alanı. A [hello Azure sanal ağ ve hello şirket içi ağ arasında VPN bağlantısı](../../../vpn-gateway/vpn-gateway-site-to-site-create.md) gereklidir.<br/><br/>Veritabanlarınızın başarılı olağanüstü durum kurtarma için bir kopya etki alanı denetleyicisi hello olağanüstü durum kurtarma sitesinde de yüklemeniz gerekir. |
| **Günlük aktarma** |Bir Azure VM ve hello diğer çalıştıran bir sunucu şirket içi siteler arası olağanüstü durum kurtarma için çalışıyor. Şirket ağı gereklidir hello Azure sanal ağı ve hello arasında bir VPN bağlantısı için Windows dosya paylaşımı, günlük aktarma bağlıdır.<br/>![Günlük aktarma](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_log_shipping.gif)<br/>Veritabanlarınızın başarılı olağanüstü durum kurtarma için bir kopya etki alanı denetleyicisi hello olağanüstü durum kurtarma sitesinde de yüklemeniz gerekir. |
| **Yedekleme ve geri yükleme ile Azure Blob Depolama Birimi hizmeti** |Böylece, şirket içi üretim veritabanları doğrudan olağanüstü durum kurtarma için blob depolama tooAzure yedeklendi.<br/>![Yedekleme ve Geri Yükleme](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_backup_restore.gif)<br/>Daha fazla bilgi için bkz: [yedekleme ve Azure Virtual Machines'de SQL Server için geri yükleme](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="important-considerations-for-sql-server-hadr-in-azure"></a>Azure SQL Server HADR için önemli noktalar
Azure VM'ler, depolama ve ağ bir şirket içi BT altyapısı sanallaştırılmamış daha farklı işletimsel özelliklere sahiptir. Bir başarılı, Azure HADR SQL Server çözümde bu farkları anlamak ve çözüm tooaccommodate tasarlama gerektirir bunları.

### <a name="high-availability-nodes-in-an-availability-set"></a>Bir kullanılabilirlik kümesinde yüksek kullanılabilirlik düğümler
Azure kullanılabilirlik kümeleri tooplace hello yüksek kullanılabilirlik düğümleri, ayrı hata etki alanlarını (FDs) ve güncelleme etki alanına (UDs) etkinleştirin. Toobe Azure VM'ler için hello aynı yerleştirilen kullanılabilirlik kümesi dağıtmanız gerekir bunları hello aynı bulut hizmeti. Aynı bulut hizmetine katılabilirsiniz hello yalnızca düğümler aynı kullanılabilirlik kümesinde hello. Daha fazla bilgi için bkz: [Yönet hello sanal makinelerin kullanılabilirliğini](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="failover-cluster-behavior-in-azure-networking"></a>Azure ağı yük devretme kümesi davranışı
azure'da Hello RFC uyumlu olmayan DHCP hizmet toohello küme ağ adı yinelenen bir IP adresi atanmış olması nedeniyle belirli bir yük devretme küme yapılandırmaları toofail hello oluşturulmasına neden olabilir, hello gibi aynı IP adresi hello küme düğümlerinden biri. Merhaba Windows Yük devretme kümesi özelliğini bağlıdır kullanılabilirlik grupları uygularken bu bir sorundur.

İki düğümlü bir küme oluşturduğunuzda ve çevrimiçi duruma hello senaryoyu göz önünde bulundurun:

1. Merhaba küme çevrimiçi olduğunu ve ardından Düğüm1 hello küme ağ adı için dinamik olarak atanmış bir IP adresi ister.
2. Bu hello istek Düğüm1'den gelen Hello DHCP hizmeti tanıdığı hello DHCP hizmeti tarafından verilen Düğüm1'ın kendi IP adresini dışında hiçbir IP adresi kendisi.
3. Windows, yinelenen bir adresi tooNODE1 ve toohello yük devretme küme ağ adı atanır ve çevrimiçi toocome hello varsayılan küme grubu başarısız algılar.
4. Merhaba varsayılan küme grubu Düğüm1'ın IP adresi hello küme IP adresi olarak değerlendirir ve hello varsayılan küme grubu çevrimiçi duruma getirir, tooNODE2 taşır.
5. Düğüm2 Düğüm1 tooestablish bağlanabilirlik çalıştığında Düğüm1'ın IP adresi tooitself çözümler çünkü Düğüm1 yönlendirilmiş paketleri hiçbir zaman Düğüm2 bırakın. Düğüm2 Düğüm1 ile bağlantı kurulamıyor, daha sonra çekirdek kaybeder ve hello kümeyi kapatır.
6. Bu sırada hello, Düğüm1 paketleri tooNODE2 gönderebilir, ancak Düğüm2 yanıt. Düğüm1 çekirdek kaybeder ve hello kümeyi kapatır.

Bu senaryo, kullanılmayan bir statik IP adresi, bağlantı-yerel IP adresi 169.254.1.1 gibi sipariş toobring hello küme ağ adı çevrimiçi toohello küme ağ adı gibi atayarak önlenebilir. toosimplify bu işlem, bkz: [yapılandırma Windows Yük devretme kümesinde Azure kullanılabilirlik grupları için](http://social.technet.microsoft.com/wiki/contents/articles/14776.configuring-windows-failover-cluster-in-windows-azure-for-alwayson-availability-groups.aspx).

Daha fazla bilgi için bkz: [(GUI) Azure kullanılabilirlik gruplarını yapılandırma](virtual-machines-windows-portal-sql-alwayson-availability-groups.md).

### <a name="availability-group-listener-support"></a>Kullanılabilirlik grubu dinleyicisi desteği
Kullanılabilirlik grubu dinleyicileri Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 ve Windows Server 2016 çalışan Azure Vm'lerinde desteklenir. Yük dengeli uç noktaları hello Azure Vm'lerinde kullanılabilirlik grubu düğümler etkin hello kullanılarak bu desteği mümkün hale getirilir. Azure yanı sıra bu şirket içi çalışan çalışan iki istemci uygulamaları için hello dinleyicileri toowork için özel yapılandırma adımları gerekir.

Dinleyiciyi ayarlamak için iki ana seçeneğiniz vardır: dış (Genel) veya dahili. internet'e yönelik Yük Dengeleyici ve ile bir genel sanal IP (üzerinden erişilebilen VIP) ilişkili hello dış (Genel) dinleyici kullandığı Internet hello. Aynı sanal ağ içinde yalnızca istemcileri destekler hello ve bir iç yük dengeleyici bir iç dinleyicisi kullanır. İçin yük dengeleyici türü, doğrudan sunucu dönüşü etkinleştirmeniz gerekir. 

Merhaba kullanılabilirlik grubu (örneğin, Azure bölgeleri kestiği dağıtımı) birden fazla Azure alt yayılırsa Merhaba istemci bağlantı dizesi içermelidir "**MultisubnetFailover = True**". Bu, paralel bağlantı denemeleri toohello çoğaltmaları hello farklı alt ağlarda sonuçlanır. Dinleyici ayarlama hakkında yönergeler için bkz:

* [Kullanılabilirlik grupları için bir ILB dinleyicisi Azure'da yapılandırın](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md).
* [Kullanılabilirlik grupları için dış dinleyici Azure'da yapılandırın](../classic/ps-sql-ext-listener.md).

Tooeach kullanılabilirlik çoğaltması toohello hizmet örneği doğrudan bağlanarak, ayrı ayrı hala bağlanabilir. Ayrıca, kullanılabilirlik grupları istemcileri yansıtma veritabanı ile geriye dönük olarak uyumlu olduğundan, veritabanı hello çoğaltmaları yapılandırılmış olduğu sürece ortakları yansıtma gibi toohello kullanılabilirlik çoğaltmalarının bağlanabilir benzer toodatabase yansıtma:

* Bir birincil çoğaltma ve bir ikincil çoğaltma
* Merhaba ikincil çoğaltma olarak okunabilir olmayan yapılandırılır (**okunabilir ikincil** çok Ayarla seçeneğini**Hayır**)

ADO.NET veya SQL Server Native Client kullanarak toothis veritabanı yansıtma benzeri yapılandırması karşılık gelen bir örnekte istemci bağlantı dizesi aşağıdadır:

    Data Source=ReplicaServer1;Failover Partner=ReplicaServer2;Initial Catalog=AvailabilityDatabase;

İstemci bağlantısı hakkında daha fazla bilgi için bkz:

* [SQL Server Native Client ile bağlantı dizesi anahtar sözcükleri kullanma](https://msdn.microsoft.com/library/ms130822.aspx)
* [İstemcileri tooa veritabanı yansıtma oturumu (SQL Server) bağlanma](https://technet.microsoft.com/library/ms175484.aspx)
* [Karma BT grubu dinleyicisinde tooAvailability bağlanma](http://blogs.msdn.com/b/sqlalwayson/archive/2013/02/14/connecting-to-availability-group-listener-in-hybrid-it.aspx)
* [Kullanılabilirlik grubu dinleyicileri, istemci bağlantısı ve uygulama yük devretme (SQL Server)](https://technet.microsoft.com/library/hh213417.aspx)
* [Veritabanı yansıtma bağlantı dizeleri kullanılabilirlik grupları ile kullanma](https://technet.microsoft.com/library/hh213417.aspx)

### <a name="network-latency-in-hybrid-it"></a>Karma BT'de ağ gecikmesi
Şirket içi ağınız ve Azure arasında yüksek ağ gecikme süresi ile süreler olabilir hello varsayım HADR çözümünüzle dağıtmanız gerekir. Çoğaltmaları tooAzure dağıtırken, zaman uyumsuz tamamlama yerine zaman uyumlu yürütme hello eşitleme modu için kullanmanız gerekir. Ne zaman veritabanı yansıtma sunucuları dağıtma hem şirket içi ve Azure'da hello yüksek performanslı modu yerine hello yüksek güvenlik modunu kullanın.

### <a name="geo-replication-support"></a>Coğrafi çoğaltma desteği
Coğrafi çoğaltma Azure disklerde hello veri dosyası ve günlük dosyası aynı veritabanı toobe ayrı disklerinde depolanan hello desteklemez. GRS değişiklikleri her diskte bağımsız olarak ve zaman uyumsuz olarak çoğaltır. Bu mekanizma tek bir disk olarak hello coğrafi olarak çoğaltılmış kopyalama, ancak olmayan birden çok disk coğrafi olarak çoğaltılmış kopyalarını içinde hello yazma sırayı garanti altına alır. Bir veritabanı toostore kendi veri dosyası ve günlük dosyası ayrı disklerde yapılandırırsanız, bir olağanüstü durum hello veri dosyasının daha güncel bir kopyasını hangi sonları SQL Server'daki yazma tamamlanan günlük hello ve ACID hello hello günlük dosyası,'den içerebilir sonra hello diskleri kurtarıldı işlem özellikleri. Merhaba depolama hesabında hello seçeneği toodisable coğrafi çoğaltma yoksa, tüm verileri tutmalısınız ve günlük dosyaları hello verilen bir veritabanı için aynı disk. Merhaba veritabanının toohello boyutu nedeniyle birden fazla disk kullanmanız gerekiyorsa, tooensure veri artıklığı listelenen hello olağanüstü durum kurtarma çözümleri birinin toodeploy gerekir.

## <a name="next-steps"></a>Sonraki adımlar
SQL Server ile bir Azure sanal makinesi toocreate gerekirse bkz [Azure üzerinde bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).

tooget hello en iyi performansı bir Azure VM üzerinde çalışan SQL Server hello kılavuzunda bkz [Azure Virtual Machines'de SQL Server için performans en iyi uygulamaları](virtual-machines-windows-sql-performance.md).

Azure vm'lerinde SQL Server toorunning ilgili diğer konular için bkz: [Azure Virtual Machines'de SQL Server](virtual-machines-windows-sql-server-iaas-overview.md).

### <a name="other-resources"></a>Diğer kaynaklar
* [Azure'da yeni bir Active Directory ormanı yüklemek](../../../active-directory/active-directory-new-forest-virtual-machine.md)
* [Azure VM'de kullanılabilirlik grupları için yük devretme kümesi oluşturma](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a)

