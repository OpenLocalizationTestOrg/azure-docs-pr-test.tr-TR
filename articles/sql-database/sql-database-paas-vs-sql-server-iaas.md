---
title: "aaaSQL (PaaS) veritabanı vs. SQL Server (Iaas) vm'lerinde hello bulutta | Microsoft Docs"
description: "Hangi bulut SQL Server seçeneğinin uygulamanıza uygun olduğunu öğrenin: Azure SQL (PaaS) veritabanı veya hello bulutta Azure Virtual Machines'de SQL Server."
services: sql-database, virtual-machines
keywords: "SQL Server bulut, SQL Server hello bulutta PaaS veritabanı, SQL Server'ı DBaaS bulut"
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cjgronlund
ms.assetid: 7467f422-b77d-4b60-9cb5-0f1ec17ec565
ms.service: sql-database
ms.custom: DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: carlrab
ms.openlocfilehash: 1b462a9a822d04dc5deb8422ed505a5d09279253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-cloud-sql-server-option-azure-sql-paas-database-or-sql-server-on-azure-vms-iaas"></a>Bir bulut SQL Server seçeneği seçin: Azure SQL (PaaS) Veritabanı ya da Azure VM'lerde SQL Server (IaaS)
Azure, SQL Server iş yüklerini Microsoft Azure’da barındırmaya yönelik iki seçenek içerir:

* [Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/): bir SQL veritabanı yerel toohello bulut, bir hizmet (PaaS) veritabanı veya hizmet olarak yazılım (SaaS) uygulaması geliştirme için en iyi duruma getirilmiş hizmet (DBaaS) olarak bir veritabanı olarak platform olarak da bilinir. SQL Server özelliklerinin çoğunluğu ile uyumluluk sağlar. PaaS hakkında daha fazla bilgi için bkz. [PaaS nedir](https://azure.microsoft.com/overview/what-is-paas/).
* [Azure Virtual Machines'de SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/): SQL Server yüklü ve hello bulut olarak da bilinen bir altyapı (ıaas) olarak Azure üzerinde çalışan Windows Server Virtual Machines'de (VM'ler) içinde barındırılır.
  Azure sanal makinelerinde SQL Server, var olan SQL Server uygulamalarını geçirme için optimize edilmiştir. Tüm sürümleri hello ve SQL Server sürümlerinde kullanılabilir. Sayıda veritabanlarını SQL Server, izin verme, toohost ile % 100 uyumluluk gerekli ve yürütülen veritabanları arası işlemler olarak sunar. SQL Server ve Windows üzerinde tam denetim sağlar.

Her bir seçeneğin nasıl hello Microsoft Veri platformuna uygun ve Yardım eşleşen hello doğru seçeneği tooyour iş gereksinimlerini öğrenin. Maliyet tasarrufu ve minimum yönetim tüm diğer unsurlardan öncelik olsun, bu makale, en çok önem verdiğiniz hello iş gereksinimlerinize göre hangi yaklaşımın sunar karar vermenize yardımcı olabilir.

## <a name="microsofts-data-platform"></a>Microsoft'un veri platformu
Merhaba ilk şey toounderstand herhangi bir Azure ile şirket içi SQL Server veritabanlarını tartışmayı içinde hiç kullanabileceğiniz biridir. Microsoft'un veri platformu, SQL Server teknolojisini kullanır ve fiziksel şirket içi makineler, özel bulut ortamları, üçüncü taraflarca barındırılan özel bulut ortamları ve genel bulutta kullanılabilir kılar. Azure virtual machines'de SQL Server kullanarak hello sırasında aynı sunucu ürünleri, geliştirme araçları ve uzmanlık kümesini bunlar arasında toomeet şirket içi ve bulut barındırılan dağıtımların bir birleşimi yoluyla benzersiz ve çeşitli iş gereksinimlerini sağlar ortamlar.

   ![Bulut SQL Server seçenekleri: Iaas ya da SaaS SQL SQL Server'da veritabanı hello bulutta.](./media/sql-database-paas-vs-sql-server-iaas/SQLIAAS_SQL_Server_Cloud_Continuum.png)

Merhaba diyagramda görüldüğü gibi her bir teklif hello (Merhaba X ekseninde) hello altyapı üzerinde sahip olduğunuz yönetim düzeyine göre ve veritabanı düzeyi birleştirme ve Otomasyon (Merhaba Y Ekseninde) tarafından elde edilen maliyet verimliliği hello derecesini tarafından işlemleri.

Bir uygulama tasarlarken, Merhaba uygulaması hello SQL Server kısmını barındırmak için dört temel seçenek mevcuttur:

* Sanallaştırılmamış fiziksel makinelerde SQL Server
* Şirket içi sanallaştırılmış makinelerde SQL Server (özel bulut)
* Azure Sanal Makine'de SQL Server (Microsoft genel bulut)
* Azure SQL Database (Microsoft genel bulut)

Aşağıdaki bölümlerde hello hello Microsoft Genel bulut SQL Server hakkında öğrenin: Azure SQL Database ve Azure vm'lerinde SQL Server. Ayrıca, hangi seçeneğin uygulamanız için en uygun olduğunu belirlemek üzere genel iş teşviklerini inceleyeceksiniz.

## <a name="a-closer-look-at-azure-sql-database-and-sql-server-on-azure-vms"></a>Azure SQL Database ve Azure VM'lerinde SQL Server'a daha ayrıntılı bir bakış
**Azure SQL veritabanı** bir ilişkisel veritabanı-a-hello hello endüstri kategorileri kapsamında Azure bulut barındırılan hizmet olarak (DBaaS) *yazılım olarak-hizmet (SaaS)* ve *hizmet olarak Platform (PaaS)* . [SQL veritabanı](sql-database-technical-overview.md), Microsoft'un sahibi olduğu, barındırdığı ve bakımını yaptığı standartlaştırılmış donanım ve yazılım üzerinde geliştirilmiştir. SQL Database ile yerleşik özellikleri ve işlevleri kullanarak doğrudan hello hizmette geliştirebilirsiniz. SQL veritabanı seçenekleri tooscale veya kesinti olmadan daha fazla güç için ile kullandıkça ödersiniz kullanırken.

**Azure Virtual Machines'de (VM'ler) SQL Server** hello endüstri kategorisine girer *-olarak-hizmet altyapı (Iaas)* ve hello buluttaki bir sanal makine içinde SQL Server toorun sağlar. Benzer tooSQL veritabanı, sahibi, barındırılan ve bakımını yaptığı standartlaştırılmış donanım üzerine inşa edilmiştir. Bir VM’de SQL Server kullanırken SQL Server görüntüsüne zaten dahil edilmiş bir SQL Server lisansı için kullandıkça ödeyebilir veya var olan bir lisansı kolayca kullanabilirsiniz. Ayrıca kolayca ölçek-yukarı/aşağı ve Duraklat/Sürdür hello VM gerektiği gibi erişebilirsiniz.

Genellikle, bu iki SQL seçeneği farklı amaçlar için en iyi hale getirilmiştir:

* **Azure SQL veritabanı** genel maliyetleri en iyi duruma getirilmiş tooreduce olan toohello sağlama ve birçok veritabanı yönetmek için en düşük. Tüm sanal makineler, işletim sistemi veya veritabanı yazılımını toomanage olmadığı için devam eden yönetim maliyetlerini azaltır. Toomanage yükseltme olmayan yüksek kullanılabilirlik veya [yedeklemeleri](sql-database-automated-backups.md). Genel olarak, Azure SQL veritabanı hello tek bir tarafından yönetilen veritabanlarının sayısını önemli ölçüde artırabilir BT veya geliştirme kaynağı.
* **Azure Vm'lerinde çalışan SQL Server** geçirme mevcut uygulamaları tooAzure veya mevcut şirket içi uygulamalar toohello bulut karma dağıtımlarda genişletme için optimize edilmiştir. Ayrıca, bir sanal makine toodevelop SQL Server kullanmak ve geleneksel SQL Server uygulamaları sınayın. Azure vm'lerinde SQL Server ile adanmış bir SQL Server örneği ve bulut tabanlı bir VM üzerinde hello tam yönetim haklarına sahip. Zaten bir kuruluş BT kaynaklarını kullanılabilir toomaintain hello sanal makineleri olduğunda ideal bir seçenektir. Bu özellikler toobuild üst düzeyde özelleştirilmiş sistem tooaddress izin, uygulamanızın belirli performans ve kullanılabilirlik gereksinimlerini.

Aşağıdaki tablonun hello hello SQL Database ve Azure vm'lerinde SQL Server temel özellikleri özetlenmektedir:

| **En iyi kullanım alanı:** | **Azure SQL Veritabanı** | **Azure Sanal Makine'de SQL Server** |
| --- | --- | --- |
|  |Geliştirme ve pazarlama alanında zaman kısıtlamaları olan yeni bulut tasarımlı uygulamalar. |Minimum değişiklikle toohello buluta hızlı geçiş gerektiren var olan uygulamalar. Toobuy şirket içi üretim dışı SQL Server donanım istemediğinizde hızlı geliştirme ve test senaryoları. |
|  | Yerleşik yüksek kullanılabilirlik, olağanüstü durum kurtarma ve yükseltme hello veritabanı için gerekli ekipler. |SQL Server için yüksek kullanılabilirlik, olağanüstü durum kurtarma ve düzeltme eki uygulamayı yapılandırıp yönetebilen ekipler. Sağlanan bazı otomatik özellikler bunu önemli ölçüde basitleştirir. | |
|  | Toomanage hello temel işletim sistemi ve yapılandırma ayarlarını istemediğiniz ekipler. |Tam yönetici haklarına sahip bir özelleştirilmiş ortamı gerekir. | |
|  | Too4 TB, veritabanlarını veya olabilir büyük veritabanları [yatay veya dikey olarak bölümlenmiş](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling) genişleme desenini kullanarak. |SQL Server örneği ile too64 TB depolama. Merhaba örneği gerektiğinde sayıda veritabanlarını destekler. | |
|  | [Hizmet olarak Yazılım (SaaS) uygulamaları oluşturma](sql-database-design-patterns-multi-tenancy-saas-applications.md). |Kuruluş uygulamalarını ve karma uygulamaları geçirme ve derleme. | |
|  | | |
| **Kaynaklar:** |Tooemploy BT istemediğiniz yapılandırması ve yönetimi için altyapı, temel alınan hello kaynakları ancak hello uygulama katmanda toofocus istiyor. |Yapılandırma ve yönetim için bazı BT kaynaklarına sahipsiniz. Sağlanan bazı otomatik özellikler bunu önemli ölçüde basitleştirir. |
| **Toplam sahip olma maliyeti:** |Donanım maliyetlerini ortadan kaldırır ve yönetim maliyetlerini azaltır. |Donanım maliyetlerini ortadan kaldırır. |
| **İş sürekliliği:** |Gibi özellikleri, ayrıca toobuilt içinde hata toleransı altyapı özelliklerine Azure SQL veritabanı sağlar [yedeklemeleri otomatik](sql-database-automated-backups.md), [noktası zaman geri yükleme](sql-database-recovery-using-backups.md#point-in-time-restore), [coğrafi geri yükleme](sql-database-recovery-using-backups.md#geo-restore), ve [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md) tooincrease iş sürekliliği. Daha fazla bilgi için bkz. [SQL Database iş sürekliliğine genel bakış](sql-database-business-continuity.md). |Azure VM’lerde SQL Server, veritabanınızın belirli gereksinimleri için bir yüksek kullanılabilirlik ve olağanüstü durum kurtarma çözümü ayarlamanıza olanak sağlar. Böylece, uygulamanız için en iyi hale getirilmiş bir sisteme sahip olabilirsiniz. Yük devretme işlemlerini ihtiyaç duyulduğunda kendi kendinize test edebilir ve çalıştırabilirsiniz. Daha fazla bilgi için bkz. [Azure Virtual Machines'de SQL Server için Yüksek Kullanılabilirlik ve Olağanüstü Durum Kurtarma](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md). |
| **Karma bulut:** |Şirket içi uygulamanız, Azure SQL Database'deki verilere erişebilir. |Azure vm'lerinde SQL Server ile kısmen hello bulutta çalışan uygulamalar, sahip olabilir ve kısmen şirket içi. Örneğin, şirket içi ağınızı ve Active Directory etki alanı toohello bulut aracılığıyla genişletebilirsiniz [Azure Virtual Network](../virtual-network/virtual-networks-overview.md). Ek olarak, [Azure'da SQL Server Veri Dosyaları](http://msdn.microsoft.com/library/dn385720.aspx)'nı kullanarak şirket içi veri dosyalarını Azure Storage'da depolayabilirsiniz. Daha fazla bilgi için bkz: [Server 2014 karma Bulutu'na giriş tooSQL](http://msdn.microsoft.com/library/dn606154.aspx). |
|  | Destekler [SQL Server işlem çoğaltma](https://msdn.microsoft.com/library/mt589530.aspx) abone tooreplicate veri olarak. |Tam olarak destekler [SQL Server işlem çoğaltma](https://msdn.microsoft.com/library/mt589530.aspx), [AlwaysOn Kullanılabilirlik grupları](../virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr.md), Integration Services ve günlük aktarma tooreplicate verileri. Ayrıca, geleneksel SQL Server yedeklemeleri tam olarak desteklenir | |
|  | | |

## <a name="business-motivations-for-choosing-azure-sql-database-or-sql-server-on-azure-vms"></a>Azure VM'lerinde Azure SQL Database'in veya SQL Server'ın seçilmesine yönelik iş faydaları
### <a name="cost"></a>Maliyet
Nakit için bünyesindeki bir başlangıç olduğunuz, veya bir ekipte fon sınırlı sıkı bütçe kısıtlamaları altında işletilen yerleşik bir şirket genellikle hello birincil sürücü karar verirken olup olmadığını nasıl toohost veritabanlarınızı. Bu bölümde, hello faturalama hakkında bilgi edinmek ve Azure ile temel lisans tahminini toothese iki ilişkisel veritabanı seçenekleri: SQL Database ve Azure vm'lerinde SQL Server. Ayrıca hello toplam uygulama maliyetini hesaplama hakkında bilgi edinin.

#### <a name="billing-and-licensing-basics"></a>Faturalama ve lisanslama ile ilgili temel bilgiler
**SQL veritabanı** toocustomers lisansa sahip olmayan bir hizmet olarak satılır.  [Azure VM’lerde SQL Server](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md) ise dakika başına ödediğiniz bir lisans ile birlikte satılır. Mevcut bir lisansınız varsa onu da kullanabilirsiniz.  

Şu anda **SQL veritabanı** tümü faturalandırılır saatlik seçtiğiniz hello Hizmet katmanını ve performans düzeyi temelinde sabit bir oranda birkaç hizmet katmanları mevcuttur. Buna ek olarak, giden Internet trafiği için normal [veri aktarımı ücretleriyle](https://azure.microsoft.com/pricing/details/data-transfers/) faturalandırılırsınız. Katmanları olan Premium RS hizmeti birden çok performans düzeyleri toomatch ile toodeliver tahmin edilebilir performansı, uygulamanızın en üst sıradaki gereksinimlerini tasarlanmış ve Hello temel, standart, Premium. Hizmet katmanları ve performans düzeyleri toomatch uygulamanızın değişken verimlilik gereken arasında değiştirebilirsiniz. Veritabanınız çok sayıda eşzamanlı kullanıcıyı yüksek işlem birim ve gereksinimlerini toosupport varsa, hello Premium Hizmet katmanını öneririz. Merhaba en son desteklenen hello geçerli hizmet katmanları hakkında bilgi için [Azure SQL Database hizmet katmanları](sql-database-service-tiers.md). Ayrıca oluşturabilirsiniz [esnek havuzlar](sql-database-elastic-pool.md) tooshare performans kaynakları veritabanı örnekleri arasında.

İle **SQL veritabanı**, hello veritabanı yazılımını otomatik olarak yapılandırılan, düzeltme eki ve yönetim maliyetlerinizi azaltır Microsoft tarafından. Ayrıca, [yerleşik yedekleme](sql-database-automated-backups.md) özellikleri, özellikle çok sayıda veritabanınız olduğunda önemli maliyet tasarrufları sağlamanıza yardımcı olur.

İle **Azure Vm'lerde SQL Server**, (lisans içerir) hello platform tarafından sağlanan SQL Server görüntüler birini kullanın ya da SQL Server lisansınızı getirebilirsiniz. Tüm hello desteklenen SQL Server sürümleri (2008R2, 2012, 2014, 2016) ve sürümleri (Geliştirici, Express, Web, Standard, Enterprise) kullanılabilir. Ayrıca, hello görüntülerinin Getir bilgisayarınızı-kendi-lisans sürümleri (KLG) kullanılabilir. Hello Azure tarafından sağlanan görüntüler kullanıldığında hello işletim maliyeti hello VM boyutu ve hello SQL Server sürümü, seçtiğiniz bağlıdır. VM boyutu veya SQL Server sürümünden bağımsız olarak, dakika başına lisanslama ücreti SQL Server ve Windows Server hello hello VM diskleri için Azure Storage maliyetinin yanı sıra ücret ödersiniz. Merhaba dakika başına faturalandırma seçeneği toouse SQL Server toplama SQL Server lisansları satın alma olmadan gerektiği kadar uzun süre sağlar. Kendi SQL Server Lisans tooAzure getirirseniz, Windows Server ve yalnızca depolama maliyetleri için sizden ücret kesilir. Kendi lisansını getir seçeneği hakkında daha fazla bilgi için bkz. [Azure'da Yazılım Güvencesi ile Lisans Mobilitesi](https://azure.microsoft.com/pricing/license-mobility/).

#### <a name="calculating-hello-total-application-cost"></a>Merhaba toplam uygulama maliyetini hesaplama
Bir bulut platformunu kullanmaya başladığınızda, uygulamanızı çalıştıran hello maliyetini hello geliştirme ve yönetim maliyetlerini artı hello genel bulut platformu hizmet maliyetlerini içerir.

İşte Azure Vm'lerinde SQL Database ve SQL Server çalıştıran uygulamanız için ayrıntılı maliyeti hesaplaması hello:

**Azure SQL Veritabanı kullanıldığında:**

*Toplam uygulama maliyeti = Yüksek oranda azaltılmış yönetim maliyetleri + yazılım geliştirme maliyetleri + SQL Veritabanı hizmet maliyetleri*

**Azure VM'lerinde SQL Server kullanıldığında:**

*Toplam uygulama maliyeti = Yüksek oranda azaltılmış yazılım geliştirme/yönetim maliyetleri + SQL Server ve Windows Server lisanslama maliyetleri + Azure Depolama maliyetleri*

Fiyatlandırma hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:

* [SQL Veritabanı Fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-database/)
* [SQL](https://azure.microsoft.com/pricing/details/virtual-machines/#sql) ve [Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#windows) için [Virtual Machine Fiyatlandırması](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Azure Fiyatlandırma Hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/)

> [!NOTE]
> SQL Server'daki özelliklerin küçük bir kısmı, SQL Database için geçerli veya kullanılabilir değildir. Daha fazla bilgi için bkz. [SQL Database Özellikleri](sql-database-features.md) ve [SQL Database Transact-SQL bilgisi](sql-database-transact-sql-information.md). Mevcut bir SQL Server çözüm toohello buluta taşıyorsanız bkz [bir SQL Server veritabanı tooAzure SQL veritabanı geçiş](sql-database-cloud-migrate.md). Varolan bir şirket içi SQL Server uygulama tooSQL veritabanı geçirdiğinizde, hello uygulama tootake yeteneklerinden bulut hizmetlerinin sunduğu hello güncelleştirmeyi deneyin. Örneğin, kullanarak düşünebilirsiniz [Azure Web App Service](https://azure.microsoft.com/services/app-service/web/) veya [Azure Cloud Services](https://azure.microsoft.com/services/cloud-services/) toohost, uygulama katmanı tooincrease maliyet avantajları.
> 
> 

### <a name="administration"></a>Yönetim
Maliyet, yönetim karmaşıklığı boşaltma hakkında çok olduğu gibi birçok işletme için hello karar tootransition tooa bulut hizmetidir. İle **SQL veritabanı**, Microsoft Donanım temel hello yönetir. Microsoft otomatik olarak tüm veri tooprovide yüksek kullanılabilirlik çoğaltır, yapılandırır ve hello veritabanı yazılımını yükselten, yük dengelemeyi yönetir ve bir sunucu hatası ise saydam yük devretme işlemi gerçekleştirir. Veritabanınızı tooadminister devam edebilirsiniz ancak artık toomanage hello veritabanı altyapısı, sunucu işletim sistemi veya donanım gerekmez.  Devam edebilirsiniz öğeleri örnekleri tooadminister veritabanları ve oturum açma, dizin sorgu ayarlama ve denetleme ve güvenlik içerir.

İle **Azure Vm'lerde SQL Server**, hello işletim sistemi ve SQL Server örneği yapılandırması üzerinde tam denetime sahiptir. Bir VM ile tooyou toodecide tooupdate/yükseltme hello ne işletim sistemi ve veritabanı yazılım ve ne zaman olmasından tooinstall virüsten koruma gibi herhangi bir ek yazılım. Toodramatically basitleştirmek düzeltme eki uygulama, yedekleme ve yüksek kullanılabilirlik otomatik bazı özellikleri sağlanır. Ayrıca, hello hello VM boyutunu, disk hello sayısını ve depolama yapılandırmalarını denetleyebilirsiniz. Azure toochange hello gerektiği gibi bir VM'nin boyutunu sağlar. Bilgi için bkz. [Azure için Sanal Makine ve Bulut Hizmeti Boyutları](../virtual-machines/windows/sizes.md). 

### <a name="service-level-agreement-sla"></a>Hizmet Düzeyi Sözleşmesi (SLA)
Birçok BT departmanı için, bir Hizmet Düzeyi Sözleşmesi'nin çalışma süresi yükümlülüklerinin yerine getirilmesi birincil önceliğe sahiptir. Bu bölümde, biz SLA uygular Ara tooeach veritabanı barındırma seçeneği.

**SQL Veritabanı** Temel, Standart, Premium ve Premium RS hizmet katmanları için Microsoft, %99,99 oranında kullanılabilirlik SLA'sı sağlar. Merhaba en son bilgiler için bkz: [hizmet düzeyi sözleşmesi](https://azure.microsoft.com/support/legal/sla/sql-database/). Hello en son SQL veritabanı hizmet katmanları ve desteklenen hello iş sürekliliği planlarına hakkında bilgi için [hizmet katmanları](sql-database-service-tiers.md).

İçin **Azure Vm'lerinde çalışan SQL Server**, Microsoft kapsar yalnızca sanal makine hello SLA 99,95 oranında bir kullanılabilirlik sağlar. Bu SLA hello VM üzerinde çalışan hello işlemleri (SQL Server gibi) kapsamaz ve bir kullanılabilirlik kümesinde en az iki VM örneğini barındırmanızı gerektirir. Merhaba Hello en son bilgiler için bkz: [VM SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Veritabanı için yüksek kullanılabilirlik (HA) VM'ler içinde desteklenen hello yüksek kullanılabilirlik seçeneklerinden birini SQL Server'da aşağıdaki gibi yapılandırmanız gerekiyor [AlwaysOn Kullanılabilirlik grupları](http://blogs.technet.com/b/dataplatforminsider/archive/2014/08/25/sql-server-alwayson-offering-in-microsoft-azure-portal-gallery.aspx). Desteklenen yüksek kullanılabilirlik seçeneği kullanılarak ek bir SLA sağlamaz, ancak tooachieve verir > % 99,99 veritabanı kullanılabilirlik.

### <a name="market"></a>Zaman toomarket
**SQL veritabanı** Geliştirici üretkenliği ve hızlı zaman Pazar kritik olduğunda hello için doğru bulut Tasarımlı uygulamalar çözümdür. Merhaba temel işletim sistemini ve veritabanını yönetmek için hello ihtiyacı azalttığından programlama DBA benzeri işlevsellik ile bulut mimarları ve geliştiricileri için mükemmeldir. Örneğin, hello kullanabilirsiniz [REST API](http://msdn.microsoft.com/library/azure/dn505719.aspx) ve [PowerShell cmdlet'leri](http://msdn.microsoft.com/library/mt740629.aspx) tooautomate ve binlerce veritabanının yönetimsel işlemlerini yönetebilirsiniz. Gibi özellikleri [esnek havuzlar](sql-database-elastic-pool.md) hello uygulama katmanına toofocus izin vermek ve çözüm toohello pazara daha hızlı teslim.

**Azure Vm'lerinde çalışan SQL Server** mevcut veya yeni uygulamalarınızın büyük veritabanlarıyla, birbiriyle ilişkili veritabanlarını veya SQL Server veya Windows tooall özelliklerine erişmek durumunda idealdir. Ayrıca toomigrate varolan istediğinizde iyi bir tercihtir şirket içi uygulamaların ve veritabanlarının tooAzure olarak olduğu-değil. Toochange hello sunu, uygulama ve veri katmanlarını gerekmediği, zamandan ve var olan çözümünüzü bütçeden kaydedin. Bunun yerine, tüm çözümleri tooAzure geçirme ve hello Azure platformu tarafından gerekli kılınabilen bazı performans iyileştirmelerini gerçekleştirmeye odaklanabilirsiniz. Daha fazla bilgi için bkz. [Azure Virtual Machines'de SQL Server için En İyi Performans Uygulamaları](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md).

## <a name="summary"></a>Özet
Bu makalede, SQL Database ve Azure Virtual Machines'de (VM'ler) SQL Server işlenmiş ve kararınızı etkileyebilecek genel iş teşvikleri ele alınmıştır. Merhaba, size tooconsider için önerilerin bir özeti verilmiştir:

**Azure SQL Database**'i aşağıdaki koşullar geçerli olduğunda tercih edin:

* Bulut hizmetlerinin başlangıç maliyet tasarrufu ve performansı en iyi duruma getirme tootake avantajlarından sağlayan yeni bulut tabanlı uygulamaları oluşturma var. Bu yaklaşım, tam olarak yönetilen bir bulut hizmeti hello yararları sağlar, daha düşük ilk zaman pazarlama yardımcı olur ve uzun vadeli maliyet iyileştirmesi sağlayabilir.
* Toohave Microsoft istediğiniz veritabanlarınız üzerinde genel yönetim işlemlerini gerçekleştirmek ve veritabanları için daha güçlü kullanılabilirlik SLA gerektirir.

**Azure VM'lerinde SQL Server**'ı aşağıdaki koşullar geçerli olduğunda tercih edin:

* Toomigrate istediğiniz veya toohello bulut genişletmek mevcut şirket içi uygulamalara sahip veya toobuild kurumsal uygulamalar 4 TB'den büyük istiyorsanız. Bu yaklaşım % 100 SQL Uyumluluk, büyük veritabanı kapasite, SQL Server ve Windows ve güvenli Tünelleme tooon içi üzerinde tam denetim hello avantajı sağlar. Bu yaklaşım var olan uygulamaların geliştirme ve değişiklik maliyetlerini azaltır.
* BT kaynaklarınız var ve sonuçta kendi düzeltme eki uygulama, yedekleme ve veritabanı yüksek kullanılabilirlik özelliklerinize sahip olabilirsiniz. Otomatik özelliklerin bazıları bu işlemleri önemli ölçüde basitleştirebilir. 

## <a name="next-steps"></a>Sonraki adımlar
* Bkz: [ilk Azure SQL veritabanınızı](sql-database-get-started-portal.md) tooget SQL veritabanı ile başlatıldı.
* Bkz. [SQL Veritabanı Fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-database/).
* Bkz: [bir SQL Server sanal makinesi sağlama](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md) tooget Azure Vm'lerde SQL Server ile başlatıldı.

