---
title: "Sunucu uygulama düzenleri vm'lerde aaaSQL | Microsoft Docs"
description: "Bu makalede Azure Vm'lerde SQL Server için uygulama düzenleri yer almaktadır. Bu çözüm mimarları ve geliştiricileri bir temel iyi uygulama mimarisi ve tasarım sağlar."
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 41863c8d-f3a3-4584-ad86-b95094365e05
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: ninarn
ms.openlocfilehash: e18597598fdf9fe534ed07331d6f531d4dca0601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-patterns-and-development-strategies-for-sql-server-in-azure-virtual-machines"></a>Azure Sanal Makineler'de SQL Server için Uygulama Desenleri ve Geliştirme Stratejileri
[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="summary"></a>Özeti:
Hangi uygulama düzeni veya desenleri toouse belirleme için SQL Server tabanlı uygulamalarınızı Azure ortamı önemli tasarım kararı ve SQL Server ve Azure her altyapı bileşeni birlikte nasıl çalışır, tam olarak anlaşılması gerektirir . Azure altyapı Hizmetleri'nde SQL Server ile kolayca geçirmek, korumanıza ve var olan SQL Server uygulamaları yerleşik üzerinde Windows Server toovirtual makinelerinizi Azure izleyin.

Bu makalenin Hello hedef tooprovide çözüm mimarları ve geliştiricileri iyi uygulama mimarisi ve mevcut uygulamalar tooAzure olarak geçirilirken takip edebilirsiniz tasarımı için temel bir yanı sıra Azure olarak geliştirme yeni uygulamalar.

Her uygulama düzeni için teknik öneri hello ilgili ve bir şirket içi senaryo, kendi ilgili bulut etkin çözüm, bulacaksınız. Ayrıca, böylece uygulamalarınızı doğru şekilde tasarlayabilirsiniz hello makalede Azure özgü geliştirme stratejileri anlatılmaktadır. Son toohello birçok olası uygulama düzenleri mimarları ve geliştiricileri uygulamalarını ve kullanıcılar için en uygun deseni hello seçmelisiniz önerilir.

**Teknik katkıda:** Haluk Carlos Vargas Herring Madhan Arumugam Ramakrishnan

**Teknik İnceleme:** Corey Sanders, Drew McDaniel, Narayan Annamalai, Nir Mashkowski, Sanjay Mishra, Silvano Coriani, Stefan Schackow Tim Hickey, Tim Wieman, Xin Jin

## <a name="introduction"></a>Giriş
N katmanlı uygulamalar türlerde hello farklı uygulama katmanları ayrı bileşenler olduğu gibi de farklı makinelerde hello bileşenlerinin ayırarak geliştirebilirsiniz. Örneğin, Merhaba istemci uygulaması yerleştirebilirsiniz ve bir makine, ön uç web katmanı ve veri erişim katmanı bileşenlerinin başka bir makinede ve başka bir makine arka uç veritabanı katmanında bileşenlerinde iş kuralları. Bu tür yapılandırma, her katman birbirinden yalıtmak yardımcı olur. Veri nereden geldiğini değiştirirseniz, toochange Merhaba istemci ya da web uygulaması gerekiyor ancak yalnızca veri erişim katmanı bileşenleri hello yok.

Tipik bir *n katmanlı* hello sunu katmanı, hello iş katmanı ve hello veri katmanı uygulama içerir:

| Katman | Açıklama |
| --- | --- |
| **Sunu** |Merhaba *sunu katmanı* (web katmanı, ön uç katmanı) olan kullanıcıların bir uygulama ile etkileşim hello katmanı. |
| **İş** |Merhaba *iş katmanı* (orta katman) hello katman bu hello sunu katmanı ve hello veri katmanı kullanım toocommunicate birbirleriyle ve hello sistem hello çekirdek işlevselliğini içerir. |
| **Veriler** |Merhaba *veri katmanı* temelde (örneğin, SQL Server çalıştıran bir sunucu) uygulama verilerini depolayan hello sunucusudur. |

Uygulama katmanları hello işlevselliği ve uygulama bileşenleri mantıksal gruplandırmalarını hello açıklar; Katmanları ayrı fiziksel sunucular, bilgisayarlar, ağlar veya uzak konumlardaki hello fiziksel dağıtım hello işlevselliği ve bileşenlerinin açıklamak ise. Merhaba uygulama katmanları hello üzerinde aynı bulunabilir fiziksel bilgisayar (Merhaba aynı katman) ya da ayrı bilgisayarlar (n katmanlı) dağıtılabilir ve hello bileşenleri her katmandaki diğer katmanları iyi tanımlanmış arabirimleri aracılığıyla bileşenlerinde ile iletişim kurabilir. İki katmanlı ve üç katmanlı n katmanlı gibi toophysical dağıtım modelleri başvuran olarak hello terim katmanının düşünebilirsiniz. A **2 katmanlı uygulama düzeni** iki uygulama katmanı içerir: uygulama sunucusu ve veritabanı sunucusu. Merhaba doğrudan iletişim hello uygulama sunucusu ve hello veritabanı sunucusu arasında gerçekleşir. Merhaba uygulama sunucusu, web katmanı ve iş katmanı bileşenleri içerir. İçinde **3 katmanlı uygulama deseni**, üç uygulama katmanı vardır: web sunucusu, hello iş mantığı katmanından ve/veya iş katmanı veri erişimi bileşenleri içeren uygulama sunucusu ve hello veritabanı sunucusu. Merhaba web sunucusu hello veritabanı sunucusu arasındaki Hello iletişimi hello uygulama sunucusu gerçekleşir. Uygulama katmanları ve katmanları hakkında ayrıntılı bilgi için bkz: [Microsoft Uygulama Mimarisi Kılavuzu](https://msdn.microsoft.com/library/ff650706.aspx).

Bu makaleyi okuduktan başlamadan önce SQL Server ve Azure hello temel kavramlar hakkında bilgi olmalıdır. Bilgi için bkz: [SQL Server Books Online](https://msdn.microsoft.com/library/bb545450.aspx), [Azure Virtual Machines'de SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) ve [Azure.com](https://azure.microsoft.com/).

Bu makalede, basit uygulamalar yanı sıra hello oldukça karmaşık kurumsal uygulamalar uygun olabilir birkaç uygulama desenleri açıklar. Her desen ayrıntılı önce azure'da hello kullanılabilir veri depolama hizmetleri gibi öğrenmeniz olduğunu öneririz [Azure Storage](../../../storage/common/storage-introduction.md), [Azure SQL veritabanı](../../../sql-database/sql-database-technical-overview.md), ve [ Bir Azure sanal makinesinde SQL Server](virtual-machines-windows-sql-server-iaas-overview.md). toomake Merhaba, uygulamalarınız için en iyi tasarım kararlarını anlamak hangi veri depolama hizmeti açıkça toouse.

### <a name="choose-sql-server-in-an-azure-virtual-machine-when"></a>Bir Azure sanal makine içinde SQL Server'ı seçin:
* SQL Server ve Windows üzerinde denetim gerekir. Örneğin, bu içerebilir hello SQL Server sürümü, özel düzeltmeleri, performans yapılandırması vb..
* Şirket içi SQL Server ile tam uyumluluk gerekir ve toomove mevcut uygulamaları tooAzure olarak istediğiniz-değil.
* Hello Azure ortamı tooleverage hello yeteneklerini istiyor ancak Azure SQL veritabanı uygulamanızın gerektirdiği tüm hello özellikleri desteklemiyor. Bu alanlar aşağıdaki hello içerebilir:
  
  * **Veritabanı boyutu**: Bu makalede güncelleştirilen hello anda SQL veritabanı bir veritabanı too1 TB'lık veriyi yukarı destekler. Birden fazla 1 TB'lık veriyi uygulamanızın gerektirdiği ve tooimplement özel parçalama çözümleri istemiyorsanız, bir Azure sanal makinede SQL Server kullanmanız önerilir. Merhaba en son bilgiler için bkz: [Azure SQL veritabanlarını kullanıma ölçeklendirme](https://msdn.microsoft.com/library/azure/dn495641.aspx) ve [Azure SQL Database hizmet katmanları ve performans düzeyleri](../../../sql-database/sql-database-service-tiers.md).
  * **HIPAA Uyumluluk**: sağlık müşteriler ve bağımsız yazılım satıcıları (ISV) seçin [Azure Virtual Machines'de SQL Server](virtual-machines-windows-sql-server-iaas-overview.md) yerine [Azure SQL veritabanı](../../../sql-database/sql-database-technical-overview.md) olduğundan SQL Sunucu bir Azure sanal makine HIPAA iş ilişkilendirmek anlaşması (BAA) tarafından ele alınmıştır. Uyumluluk hakkında daha fazla bilgi için bkz: [Microsoft Azure Trust Center: Uyumluluk](https://azure.microsoft.com/support/trust-center/compliance/).
  * **Örnek düzeyinde Özellikler**: şu anda SQL veritabanı hello veritabanı dışında Canlı özellikleri desteklemez (bağlantılı sunucular gibi Aracısı işleri, FILESTREAM, hizmet Aracısı vb..). Daha fazla bilgi için bkz: [Azure SQL veritabanı yönergeleri ve sınırlamaları](https://msdn.microsoft.com/library/azure/ff394102.aspx).

## <a name="1-tier-simple-single-virtual-machine"></a>1 katmanlı (Basit): tek bir sanal makine
Bu uygulama modelinde SQL Server uygulama ve veritabanı tooa tek başına sanal makine azure'da dağıtın. Merhaba aynı sanal makine istemci/web uygulaması, bir iş bileşenleri, veri erişim katmanı ve hello veritabanı sunucusu içerir. Merhaba sunu, iş ve veri erişim kodu mantıksal olarak ayrılır ancak fiziksel bir tek sunucu makinede bulunan. Bu uygulama düzeni müşterilerin çoğu başlatın ve sonra bunlar daha fazla web rolleri ya da sanal makineleri tootheir sistemi ekleyerek ölçeğini.

Bu uygulama düzeni ne zaman yararlı olur:

* Merhaba platform veya uygulamanızın gereksinimleri yanıtlar olup olmadığını tooperform basit geçiş tooAzure platform tooevaluate istiyor.
* Tüm hello barındırılan uygulama katmanları tookeep istediğiniz hello aynı sanal hello aynı makine Azure veri merkezi katmanları arasındaki tooreduce hello gecikme süresi.
* Kısa süreyle ortamlarında test ve tooquickly sağlama geliştirme istiyorsunuz.
* İş yükü düzeyleri değişen için ancak etmez tooown istediğiniz ve birçok fiziksel korumak aynı anda tüm hello zaman makineleri hello tooperform stres testleri istiyor.

Merhaba Aşağıdaki diyagramda basit bir senaryo ve tek bir sanal makine azure'da etkin bulut çözümünün nasıl dağıtabileceğiniz içi gösterir.

![1 katmanlı uygulama düzeni](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728008.png)

Merhaba iş Katmanı (iş mantığı ve verileri bileşenlerine erişmek) üzerinde hello dağıtma hello sunu katmanı olarak aynı fiziksel katman en üst düzeye çıkarmak uygulama performansı tooscalability veya güvenlik sorunları nedeniyle ayrı bir katman kullanmadığınız sürece.

Bu çok yaygın bir desen toostart sahip olduğundan, geçiş, veri tooyour SQL Server VM taşımak için yararlı makalede aşağıdaki hello bulabilirsiniz: [veritabanı tooSQL bir Azure VM sunucuda geçiş](virtual-machines-windows-migrate-sql.md).

## <a name="3-tier-simple-multiple-virtual-machines"></a>3 katmanlı (Basit): birden çok sanal makineler
Bu uygulama modelinde farklı bir sanal makinede her uygulama katmanı koyarak 3 katmanlı uygulama azure'da dağıtın. Bu, kolay bir ölçek büyütme ve ölçek genişletme senaryoları için esnek bir ortam sağlar. Bir sanal makine istemci/web uygulamanızı içerdiğinde, diğeri hello iş bileşenlerinizi barındırır ve başka bir ana bilgisayar hello veritabanı sunucusu hello.

Bu uygulama düzeni ne zaman yararlı olur:

* Tooperform karmaşık veritabanı uygulamaları tooAzure sanal makinelerin geçişini istediğiniz.
* Farklı bölgelerde barındırılan farklı uygulama katmanları toobe istiyor. Örneğin, raporlama amacıyla dağıtılan toomultiple bölgeler veritabanı paylaşılan.
* Şirket içi toomove kurumsal uygulamalar platformları tooAzure sanal makineleri sanallaştırılmış istiyor. Kurumsal uygulamalar hakkında ayrıntılı bilgi için bkz: [Kurumsal uygulama nedir](https://msdn.microsoft.com/library/aa267045.aspx).
* Kısa süreyle ortamlarında test ve tooquickly sağlama geliştirme istiyorsunuz.
* İş yükü düzeyleri değişen için ancak etmez tooown istediğiniz ve birçok fiziksel korumak aynı anda tüm hello zaman makineleri hello tooperform stres testleri istiyor.

Merhaba Aşağıdaki diyagramda Azure içinde farklı bir sanal makinede her uygulama katmanı koyarak Basit 3 katmanlı uygulama nasıl yerleştirebilirsiniz gösterir.

![3 katmanlı uygulama düzeni](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728009.png)

Bu uygulama modelinde, her katman içinde yalnızca bir sanal makine (VM) yoktur. Azure içinde birden çok VM varsa, sanal bir ağ ayarlamanızı öneririz. [Azure sanal ağı](../../../virtual-network/virtual-networks-overview.md) güvenilir güvenlik sınırı oluşturur ve ayrıca hello özel IP adresi üzerinden VM'ler toocommunicate aralarında sağlar. Ayrıca, her zaman tüm Internet bağlantıları yalnızca toohello sunu katmanı Git emin olun. Bu uygulama düzeni aşağıdaki hello ağ güvenlik grubu kuralları toocontrol erişimi yönetebilirsiniz. Daha fazla bilgi için bkz: [izin dış erişim tooyour VM kullanarak hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Merhaba şemada Internet protokolleri TCP, UDP, HTTP veya HTTPS olabilir.

> [!NOTE]
> Azure sanal ağında ayarlama ücretsizdir. Ancak, tooon içi bağlayan hello VPN ağ geçidi için sizden ücret kesilir. Bu ücret hello bağlantı sağlandı ve kullanılabilir durumda süre miktarını temel alır.
> 
> 

## <a name="2-tier-and-3-tier-with-presentation-tier-scale-out"></a>Katman 2 ve 3 katmanlı sunu katmanı ölçek genişletme ile
Bu uygulama modelinde Katman 2 veya 3 katmanlı veritabanı uygulama tooAzure sanal makineleri farklı bir sanal makinede her uygulama katmanı koyarak dağıtın. Ayrıca, gelen istemci isteklerini tooincreased hacmi nedeniyle hello sunu katmanı ölçeği genişletme.

Bu uygulama düzeni ne zaman yararlı olur:

* Şirket içi toomove kurumsal uygulamalar platformları tooAzure sanal makineleri sanallaştırılmış istiyor.
* Merhaba sunu katmanı gelen istemci isteklerini tooincreased hacmi nedeniyle çıkışı tooscale istiyor.
* Kısa süreyle ortamlarında test ve tooquickly sağlama geliştirme istiyorsunuz.
* İş yükü düzeyleri değişen için ancak etmez tooown istediğiniz ve birçok fiziksel korumak aynı anda tüm hello zaman makineleri hello tooperform stres testleri istiyor.
* İsteğe bağlı olarak yukarı ve aşağı ölçeklenebilen bir altyapı ortam tooown istiyor.

Merhaba Aşağıdaki diyagramda nasıl, hello uygulama katmanları birden çok sanal makine azure'da hello sunu katmanı gelen istemci isteklerini tooincreased hacmi nedeniyle ölçeğini yerleştirebilirsiniz gösterir. Merhaba diyagramda görüldüğü gibi Azure yük dengeleyici trafiği birden çok sanal makineler arasında dağıtma ve ayrıca hangi web sunucusu tooconnect belirleme sorumludur. Merhaba web sunucuları yük dengeleyici arkasında birden çok örneğini sahip hello yüksek düzeyde kullanılabilirliğini hello sunu katmanı sağlar.

![Uygulama düzeni - sunu katmanı ölçek genişletme](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728010.png)

### <a name="best-practices-for-2-tier-3-tier-or-n-tier-patterns-that-have-multiple-vms-in-one-tier"></a>Birden çok VM'ye sahip bir katman 2 katmanlı, 3 katmanlı veya n katmanlı modelleri için en iyi uygulamalar
Aynı katmanı aynı bulut hizmetine ve içinde hello aynı hello toohello ait hello sanal makineleri yerleştirmeniz önerilir hello kullanılabilirlik kümesi. Örneğin, web sunucularının bir kümesi yerleştirin **CloudService1** ve **AvailabilitySet1** ve veritabanı sunucuları kümesi **CloudService2** ve  **AvailabilitySet2**. Kullanılabilirlik kümesi Azure'da tooplace hello yüksek kullanılabilirlik düğümlerin, yükseltme etki alanları ve ayrı hata etki alanına sağlar.

tooleverage birden çok VM örnekleri katmanı, Azure yük dengeleyici uygulama katmanları arasında tooconfigure gerekir. Her katmandaki tooconfigure yük dengeleyici oluşturun yük dengeli bir uç nokta her katmanın Vm'lerinde ayrı olarak. Belirli bir katman için ilk VM'ler oluşturmak hello aynı bulut hizmeti. Bu hello sahip olmasını sağlar aynı genel sanal IP adresi. Ardından, o katman sanal makinelerde hello birinde bir uç nokta oluşturun. Ardından, Ata hello aynı uç nokta toohello Yük Dengeleme için bu katmanda diğer sanal makineler. Yük dengeli kümesi oluşturarak, trafiği birden çok sanal makinelerde dağıtmak ve arka uç VM düğüm başarısız olduğunda hello yük dengeleyici toodetermine hangi düğümü tooconnect da izin. Örneğin, hello web sunucuları yük dengeleyici arkasında birden çok örneğini sahip hello yüksek düzeyde kullanılabilirliğini hello sunu katmanı sağlar.

En iyi uygulama, her zaman tüm internet bağlantıları ilk toohello sunu katmanı Git emin olun. Merhaba sunu katmanı hello iş katmanı erişir ve ardından hello iş katmanı hello veri katmanı erişir. Nasıl tooallow erişim toohello sunu katmanı ile ilgili daha fazla bilgi için bkz: [izin dış erişim tooyour VM kullanarak hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Yük Dengeleyici azure'da hello Not benzer tooload dengeleyicileri bir şirket içi ortamda çalışır. Daha fazla bilgi için bkz: [Yük Dengeleme için Azure altyapı hizmetleri](../tutorial-load-balancer.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Ayrıca, Azure sanal ağı kullanarak, sanal makineleriniz için özel bir ağ ayarlamanızı öneririz. Bu hello özel IP adresi üzerinden aralarında toocommunicate sağlar. Daha fazla bilgi için bkz: [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md).

## <a name="2-tier-and-3-tier-with-business-tier-scale-out"></a>Katman 2 ve 3 katmanlı iş katmanı ölçek genişletme ile
Bu uygulama modelinde Katman 2 veya 3 katmanlı veritabanı uygulama tooAzure sanal makineleri farklı bir sanal makinede her uygulama katmanı koyarak dağıtın. Ayrıca, toodistribute hello uygulama sunucusu bileşenleri toomultiple sanal makineleri, uygulamanızın toohello karmaşıklığı nedeniyle isteyebilirsiniz.

Bu uygulama düzeni ne zaman yararlı olur:

* Şirket içi toomove kurumsal uygulamalar platformları tooAzure sanal makineleri sanallaştırılmış istiyor.
* Toodistribute hello uygulama sunucusu bileşenleri toomultiple sanal makineleri, uygulamanızın toohello karmaşıklığı nedeniyle istiyor.
* Toomove iş mantığı ağır şirket içi LOB (iş,) uygulamaları tooAzure sanal makineleri istiyor. İş KOLU uygulamaları, önemli toorunning hesap, İnsan Kaynakları (HR), bordro, tedarik zinciri yönetimi ve kaynak planlama uygulamaları gibi kuruluş kritik bilgisayar uygulamalar kümesidir.
* Kısa süreyle ortamlarında test ve tooquickly sağlama geliştirme istiyorsunuz.
* İş yükü düzeyleri değişen için ancak etmez tooown istediğiniz ve birçok fiziksel korumak aynı anda tüm hello zaman makineleri hello tooperform stres testleri istiyor.
* İsteğe bağlı olarak yukarı ve aşağı ölçeklenebilen bir altyapı ortam tooown istiyor.

Aşağıdaki diyagramda hello bir şirket içi senaryo ve etkin bulut çözümünün gösterir. Bu senaryoda, hello iş mantığı katmanı ve veri erişim bileşenlerini içeren hello iş katmanı, ölçeklendirme tarafından birden çok sanal makine azure'da hello uygulama katmanında yerleştirin. Merhaba diyagramda görüldüğü gibi Azure yük dengeleyici trafiği birden çok sanal makineler arasında dağıtma ve ayrıca hangi web sunucusu tooconnect belirleme sorumludur. Merhaba uygulama sunucuları yük dengeleyici arkasında birden çok örneğini sahip hello yüksek düzeyde kullanılabilirliğini hello iş katmanı sağlar. Daha fazla bilgi için bkz: [bir katmanında birden çok sanal makineye sahip Katman 2, 3 katmanlı veya n katmanlı uygulama düzenleri için en iyi uygulamaları](#best-practices-for-2-tier-3-tier-or-n-tier-patterns-that-have-multiple-vms-in-one-tier).

![İş katmanı ölçek genişletmeli uygulama düzeni](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728011.png)

## <a name="2-tier-and-3-tier-with-presentation-and-business-tiers-scale-out-and-hadr"></a>Katman 2 ve 3 katmanlı sunu ve iş katmanları genişleme ve HADR ile
Bu uygulama modelinde hello sunu katmanı (web sunucusu) dağıtarak Katman 2 veya 3 katmanlı veritabanı uygulama tooAzure sanal makineleri dağıtmak ve iş Katmanı (uygulama sunucusu) bileşenleri toomultiple sanal makineleri hello. Ayrıca, veritabanlarınızı Azure sanal makineler için yüksek kullanılabilirlik ve olağanüstü durum kurtarma çözümleri uygulayın.

Bu uygulama düzeni ne zaman yararlı olur:

* SQL Server yüksek kullanılabilirlik ve olağanüstü durum kurtarma özellikleri uygulayarak toomove kuruluş sanallaştırılmış platformları şirket içi tooAzure uygulamalarından istiyor.
* Merhaba sunu katmanı ve hello iş katmanı gelen istemci isteklerini tooincreased hacmi ve uygulamanızın hello karmaşıklığı nedeniyle tooscale istiyor.
* Kısa süreyle ortamlarında test ve tooquickly sağlama geliştirme istiyorsunuz.
* İş yükü düzeyleri değişen için ancak etmez tooown istediğiniz ve birçok fiziksel korumak aynı anda tüm hello zaman makineleri hello tooperform stres testleri istiyor.
* İsteğe bağlı olarak yukarı ve aşağı ölçeklenebilen bir altyapı ortam tooown istiyor.

Aşağıdaki diyagramda hello bir şirket içi senaryo ve etkin bulut çözümünün gösterir. Bu senaryoda, hello sunu katmanı ve birden çok sanal makine azure'da hello iş katmanı bileşen ölçeğini. Ayrıca, Azure'da SQL Server veritabanları için yüksek kullanılabilirlik ve olağanüstü durum kurtarma (HADR) teknikleri uygulayın.

Bir uygulama birden çok kopyasını farklı çalıştıran VM'ler istekleri arasında gezinmek dengelemesini olduğundan emin olun. Birden çok sanal makine varsa, tüm Vm'leriniz zamanında erişilebilir bir noktada olduğundan ve çalıştığından emin toomake gerekir. Yük Dengeleme yapılandırırsanız, Azure yük dengeleyici parçaları VM'ler durumunu hello ve gelen çağrıları toohello iyi çalışan VM düğümleri düzgün şekilde yönlendirir. Hakkında bilgi için hello sanal makinelerin Yük Dengeleme yukarı tooset bkz [Yük Dengeleme için Azure altyapı hizmetleri](../tutorial-load-balancer.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Web ve uygulama sunucularını bir yük dengeleyici arkasında birden çok örneğini sahip hello yüksek kullanılabilirliğini hello sunu ve iş katmanı sağlar.

![Genişletme ve yüksek kullanılabilirlik](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728012.png)

### <a name="best-practices-for-application-patterns-requiring-sql-hadr"></a>SQL HADR gerektiren uygulama düzenleri için en iyi yöntemler
SQL Server yüksek kullanılabilirlik ve olağanüstü durum kurtarma çözümleri Azure Virtual Machines'de ayarladığınızda, bir sanal ağ kullanarak, sanal makineleriniz ayarlama [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md) zorunludur.  Bir sanal ağ içindeki sanal makineleri kararlı ve özel bir IP adresi sonra bile bir hizmet kesintisi olacaktır, böylece DNS ad çözümlemesi için gereken hello güncelleştirme zamanı önleyebilirsiniz. Ayrıca, tooextend sağlar hello sanal ağı şirket içi tooAzure ağ ve güvenilir güvenlik sınırı oluşturur. Örneğin, uygulamanız (örneğin, Windows kimlik doğrulaması, Active Directory), şirket etki alanı kısıtlamaları sahipse ayarlama [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md) gereklidir.

Üretim kodu Azure üzerinde çalıştırıyorsanız, müşterilerin çoğu, birincil ve ikincil çoğaltmaları Azure'da önlüyor.

Kapsamlı bilgi ve yüksek kullanılabilirlik ve olağanüstü durum kurtarma teknikleri öğreticiler için bkz: [yüksek kullanılabilirlik ve olağanüstü durum kurtarma Azure Virtual Machines'de SQL Server için](virtual-machines-windows-sql-high-availability-dr.md).

## <a name="2-tier-and-3-tier-using-azure-vms-and-cloud-services"></a>Katman 2 ve 3 katmanlı Azure Vm'leri ve bulut Hizmetleri kullanma
Bu uygulama modelinde Katman 2 veya 3 katmanlı uygulama tooAzure her ikisini de kullanarak dağıttığınız [Azure Cloud Services](../../../cloud-services/cloud-services-choose-me.md#tellmecs) (web ve çalışan rolleri - (PaaS) hizmet olarak Platform) ve [Azure sanal makineleri](../overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) () Hizmet olarak altyapı (Iaas)). Kullanarak [Azure Cloud Services](https://azure.microsoft.com/documentation/services/cloud-services/) hello sunu katmanı/iş katmanı ve SQL Server için [Azure sanal makineleri](../overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello veri katmanı Azure üzerinde çalışan çoğu uygulamalar için yararlıdır. Merhaba neden bulut hizmetlerini çalıştıran bir işlem örneğinde sahip bir kolay yönetimi, dağıtım, izleme ve genişleme sağlamasıdır.

Bulut Hizmetleri ile Azure hello altyapı sizin için tutar, bakım gerçekleştirir, hello işletim sistemleri düzeltme ekleri ve hizmet ve donanım hatalardan toorecover çalışır. Uygulamanızı genişleme gerektiğinde otomatik ve el ile genişletme seçenekleri artırarak veya azaltarak hello sayısı örneği veya uygulamanız tarafından kullanılan sanal makine tarafından bulut hizmeti projenizi için kullanılabilir. Ayrıca, şirket içi Visual Studio toodeploy uygulama tooa bulut hizmeti projenizi Azure içinde kullanabilirsiniz.

Özet olarak, Azure Cloud Services tooown kapsamlı yönetim görevleri için hello sunu/iş katmanı istemediğiniz ve uygulamanızı yazılım veya hello işletim sisteminin karmaşık herhangi bir yapılandırma gerektirmez, kullanın. Azure SQL veritabanı aradığınız tüm hello özellikleri desteklemiyorsa, SQL Server hello veri katmanı için bir Azure sanal makinede kullanın. Azure Cloud Services üzerinde bir uygulama çalıştıran ve Azure sanal makinelerinde veri depolama her iki hizmet hello yararları birleştirir. Ayrıntılı bir karşılaştırması için bu konudaki hello bölümüne bakın [azure'da geliştirme stratejileri karşılaştırma](#comparing-web-development-strategies-in-azure).

Bu uygulama modelinde bir bulut hizmetleri bileşeni hello Azure yürütme ortamında çalışan ve IIS ve ASP.NET tarafından desteklenen gibi web uygulama programlama için özelleştirilmiş bir web rolü hello sunu katmanı içerir. Bulut hizmetleri bileşeni hello Azure yürütme ortamında çalışan genelleştirilmiş geliştirme için yararlıdır ve web rolü için arka plan işlemleri gerçekleştirebilir ve çalışan rolü Hello iş veya arka uç katmanı içerir. bir SQL Server sanal makine azure'da Hello veritabanı katmanı bulunur. Merhaba sunu katmanı hello veritabanı katmanı arasındaki Hello iletişimi, doğrudan ya da hello iş katmanı – çalışan rolü bileşenleri üzerinden gerçekleşir.

Bu uygulama düzeni ne zaman yararlı olur:

* SQL Server yüksek kullanılabilirlik ve olağanüstü durum kurtarma özellikleri uygulayarak toomove kuruluş sanallaştırılmış platformları şirket içi tooAzure uygulamalarından istiyor.
* İsteğe bağlı olarak yukarı ve aşağı ölçeklenebilen bir altyapı ortam tooown istiyor.
* Azure SQL veritabanı uygulamanızı veya veritabanı gereken tüm hello özellikleri desteklemiyor.
* İş yükü düzeyleri değişen için ancak etmez tooown istediğiniz ve birçok fiziksel korumak aynı anda tüm hello zaman makineleri hello tooperform stres testleri istiyor.

Aşağıdaki diyagramda hello bir şirket içi senaryo ve etkin bulut çözümünün gösterir. Bu senaryoda, yerleştirdiğiniz hello sunu katmanı web rollerinde, çalışan rollerinde hello iş katmanı ancak azure'daki sanal makinelerde hello veri katmanı. Birden çok kopyasını hello sunu katmanı farklı web rollerinde çalıştıran tooload bakiye istekleri arasında gezinmek sağlar. Azure bulut Hizmetleri ile Azure sanal makineleri birleştirdiğinizde ayarlamanız önerilir [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md) de. İle [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md), kararlı olabilir ve aynı bulut hizmetinde hello içindeki kalıcı özel IP adresleri hello bulut. Bir sanal ağ, sanal makineleriniz için tanımlama ve bulut Hizmetleri zaman kendilerini arasında hello özel IP adresi iletişim kurmasını başlayabilirsiniz. Ayrıca, sanal makineler ve Azure web/çalışan rolleri aynı hello sahip [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md) düşük gecikme süresi ve daha güvenli bir bağlantı sağlar. Daha fazla bilgi için bkz: [bir bulut hizmeti nedir](../../../cloud-services/cloud-services-choose-me.md).

Merhaba diyagramda görüldüğü gibi Azure yük dengeleyici trafiği birden çok sanal makine genelinde dağıtır ve ayrıca hangi web sunucusu veya uygulama sunucusu belirler tooconnect için. Merhaba web ve uygulama sunucularını bir yük dengeleyici arkasında birden çok örneğini sahip hello sunu katmanı ve hello iş katmanı hello yüksek kullanılabilirlik sağlar. Daha fazla bilgi için bkz: [en iyi yöntemler uygulaması gerektiren SQL HADR desenler için](#best-practices-for-application-patterns-requiring-sql-hadr).

![Bulut Hizmetleri ile uygulama düzenleri](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728013.png)

Başka bir yaklaşım tooimplement bu uygulama düzeni toouse içeren sunu katmanı ve iş katmanı bileşenleri hello aşağıda gösterildiği gibi birleştirilmiş web rolü olan diyagramı. Bu uygulama düzeni durum bilgisi olan tasarım gerektiren uygulamalar için kullanışlıdır. Azure durum bilgisiz işlem düğümleri üzerinde web ve çalışan rolleri sağlar. bu yana teknolojileri aşağıdaki hello birini kullanarak bir mantık toostore oturum durumu uygulamak öneririz: [Azure önbelleğe alma](https://azure.microsoft.com/documentation/services/redis-cache/), [Azure Table Storage](../../../cosmos-db/table-storage-how-to-use-dotnet.md) veya [Azure SQL veritabanı](../../../sql-database/sql-database-technical-overview.md).

![Bulut Hizmetleri ile uygulama düzenleri](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728014.png)

## <a name="pattern-with-azure-vms-azure-sql-database-and-azure-app-service-web-apps"></a>Azure VM'ler, Azure SQL Database ve Azure uygulama hizmeti (Web uygulamaları) deseni
Bu uygulama düzeni Hello birincil amacı olan tooshow, nasıl toocombine Azure hizmet olarak platform (PaaS) bileşenlerinde çözümünüzü hizmet (Iaas) bileşenleriyle olarak Azure altyapısı. Bu desen ilişkisel veri depolama için Azure SQL veritabanı üzerinde odaklanmıştır. Bu SQL Server bir Azure sanal makinesi hello hizmet sunumu olarak Azure altyapısı parçası olduğu içermez.

Bu uygulama modelinde hello sunu koyarak veritabanı uygulama tooAzure dağıtın ve iş katmanlarında aynı sanal makine ve Azure SQL veritabanı (SQL veritabanı) sunucuları bir veritabanına erişim hello. Geleneksel IIS tabanlı web çözümleri kullanarak hello sunu katmanı uygulayabilirsiniz. Veya, bir birleşik sunu ve iş katmanı kullanarak uygulayabileceğiniz [Azure Web Apps](https://azure.microsoft.com/documentation/services/app-service/web/).

Bu uygulama düzeni ne zaman yararlı olur:

* Azure üzerinde yapılandırılmış varolan bir SQL veritabanı sunucusuna zaten var ve tootest uygulamanızın hızla istediğiniz.
* Azure ortamı tootest hello yeteneklerini istiyor.
* Kısa süreyle ortamlarında test ve tooquickly sağlama geliştirme istiyorsunuz.
* İş mantığı ve verileri erişim bileşenleri bir web uygulamasının içinden müstakil olabilir.

Aşağıdaki diyagramda hello bir şirket içi senaryo ve etkin bulut çözümünün gösterir. Bu senaryoda, Azure SQL veritabanı Azure ve erişim verilerini tek bir sanal makine hello uygulama katmanında yerleştirin.

![Karma uygulama düzeni](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728015.png)

Tooimplement seçerseniz Azure Web Apps kullanarak bir birleşik web ve uygulama katmanı, bir web uygulaması hello bağlamında dinamik bağlantı kitaplıkları (dll) olarak hello Orta katmanda veya uygulama katmanı tutmanızı öneririz.

Ayrıca, hello verilen hello önerileri gözden [Azure web geliştirme stratejilerine karşılaştırma](#comparing-web-development-strategies-in-azure) teknikleri programlama hakkında daha fazla Bu makale toolearn hello sonunda bölüm.

## <a name="n-tier-hybrid-application-pattern"></a>N katmanlı karma uygulama düzeni
N katmanlı karma uygulama düzeni şirket içi ve Azure arasında dağıtılmış birden çok katman uygulamanızda uygulayın. Bu nedenle, değiştirme veya ekleme esnek ve yeniden kullanılabilir karma sistem oluşturma değiştirmeden belirli bir katman hello diğer katmanları. şirket ağı toohello tooextend bulut, kullandığınız [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md) hizmet.

Bu karma uygulama düzeni ne zaman yararlı olur:

* Kısmen hello bulutta çalışacak ve kısmen şirket içi toobuild uygulamalar istiyor.
* Mevcut şirket içi uygulama toohello bulutunun bazı veya tüm öğeleri toomigrate istiyor.
* Şirket içi sanallaştırılmış platformları tooAzure toomove kuruluş uygulamalarından istiyor.
* İsteğe bağlı olarak yukarı ve aşağı ölçeklenebilen bir altyapı ortam tooown istiyor.
* Kısa süreyle ortamlarında test ve tooquickly sağlama geliştirme istiyorsunuz.
* Kurumsal veritabanı uygulamaları için düşük maliyetli şekilde tootake yedeklemeler istiyor.

Aşağıdaki diyagramda hello şirket içi ve Azure üzerinden yayılan bir n katmanlı karma uygulama düzeni gösterir. Merhaba diyagramda gösterildiği gibi altyapı içeren şirket içi [Active Directory etki alanı Hizmetleri](https://technet.microsoft.com/library/hh831484.aspx) etki alanı denetleyicisi toosupport kullanıcı kimlik doğrulaması ve yetkilendirme. Merhaba diyagramlarda Azure'da hello veri katmanı bazı bölümleri Canlı ancak bir şirket içi veri merkezinde burada hello veri katmanı bazı bölümleri canlı bir senaryo gösterir unutmayın. Uygulamanızın gereksinimlerine bağlı olarak birkaç diğer karma senaryolar uygulayabilirsiniz. Örneğin, bir şirket içi ortamına ancak hello veri katmanına azure'da hello sunu katmanı ve hello iş katmanı tutabilirsiniz.

![N katmanlı uygulama düzeni](./media/virtual-machines-windows-sql-server-app-patterns-dev-strategies/IC728016.png)

Azure'da, Active Directory tek başına bulut dizini olarak kuruluşunuz için kullanabileceğiniz ya da mevcut şirket içi Active Directory ile de tümleştirebilir [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/). Merhaba diyagramda görüldüğü gibi hello iş katmanı bileşenleri toomultiple veri kaynakları gibi çok erişebilirsiniz[Azure SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md) özel bir iç IP adresi tooon içi SQL Server aracılığıyla aracılığıyla [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md), ya da çok[SQL veritabanı](../../../sql-database/sql-database-technical-overview.md) hello .NET Framework veri sağlayıcısı teknolojilerini kullanarak. Bu diyagramda, Azure SQL veritabanı bir isteğe bağlı veri depolama hizmetidir.

N katmanlı karma uygulama düzeni iş akışı belirtilen hello sırasıyla aşağıdaki hello uygulayabilirsiniz:

1. Hello kullanarak toocloud taşınır toobe gereken Kurumsal veritabanı uygulamaları belirlemek [Microsoft Assessment ve planlama (MAP) Araç Seti](http://microsoft.com/map). Merhaba MAP Araç Kiti sanallaştırma için dikkate bilgisayarlardan Envanter ve performans verilerini toplar ve kapasite ve değerlendirme planlama önerileri sağlar.
2. Merhaba kaynakları ve hello depolama hesapları ve sanal makineler gibi Azure platformu gerekli yapılandırma planlayın.
3. Merhaba şirket ağı şirket içi arasında ağ bağlantısı ayarlama ve [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md). Merhaba şirket ağı şirket içi ve Azure, bir sanal makine arasında hello bağlantı tooset hello aşağıdaki iki yöntemden birini kullanın:
   
   1. Azure'da bir sanal makinede ortak uç noktaları yoluyla şirket içi ve Azure arasında bir bağlantı oluşturun. Bu yöntem, kolay kurulum sağlar ve sanal makineniz toouse SQL Server kimlik doğrulamasını etkinleştirir. Buna ek olarak, ağ güvenlik grubu kuralları toocontrol ortak trafiğin toohello VM ayarlayın. Daha fazla bilgi için bkz: [izin dış erişim tooyour VM kullanarak hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
   2. Azure sanal özel ağ (VPN) tüneli yoluyla şirket içi ve Azure arasında bağlantı kurun. Bu yöntem, Azure'da tooextend etki alanı ilkeleri tooa sanal makine sağlar. Ayrıca, güvenlik duvarı kuralları ayarlamak ve sanal makinenizde Windows kimlik doğrulaması kullanın. Şu anda, Azure güvenli siteden siteye VPN ve noktadan siteye VPN bağlantılarını destekler:
      
      * Güvenli siteden siteye bağlantı ile ağ bağlantısı şirket içi ağınız ile sanal ağınız arasında Azure'da kurabilirsiniz. Şirket içi veri merkezi ortamında tooAzure bağlanmak için önerilir.
      * Güvenli noktadan siteye bağlantı ile Azure sanal ağınızda ve herhangi bir yere çalıştıran bağımsız bilgisayar arasında ağ bağlantısı kurabilirsiniz. Geliştirme ve test amaçları için çoğunlukla önerilir.
      
      Hakkında bilgi için tooconnect tooSQL Azure, Server'da bkz [tooa Azure ile ilgili SQL Server sanal makinesine bağlanmak](virtual-machines-windows-sql-connect.md).
4. Zamanlanan işler ve şirket içi verileri azure'da bir sanal makine disk yedekleme Uyarıları ayarlayın. Daha fazla bilgi için bkz: [SQL Server Yedekleme ve geri yükleme ile Azure Blob Depolama hizmetinin](https://msdn.microsoft.com/library/jj919148.aspx) ve [yedekleme ve Azure Virtual Machines'de SQL Server için geri yükleme](virtual-machines-windows-sql-backup-recovery.md).
5. Uygulamanızın gereksinimlerine bağlı olarak üç yaygın senaryo aşağıdaki hello birini uygulayabilirsiniz:
   
   1. Merhaba hassas verileri şirket içi tutmak ancak azure'da veritabanı sunucusundaki web sunucusu, uygulama sunucusu ve duyarlı verileri tutabilirsiniz.
   2. Web sunucunuzun tutabilir ve uygulama sunucusu şirket içi ise bir sanal makinede azure'da hello veritabanı sunucusu.
   3. Tutabilirsiniz veritabanı sunucusu, web sunucusu ve uygulama sunucusu azure'daki sanal makinelerde hello veritabanı çoğaltmaları tutmak ancak şirket içi. Bu ayar hello web sunucuları şirket içi veya raporlama uygulamaları tooaccess veritabanı çoğaltmaları azure'da hello sağlar. Bu nedenle, bir şirket içi veritabanına toolower hello iş yükü elde edebilirsiniz. Bu senaryo için ağır uygulamak öneririz iş yükleri ve gelişim amacıyla okuyun. AlwaysOn Kullanılabilirlik grupları adresindeki Azure'da veritabanı çoğaltmaları oluşturma hakkında daha fazla bilgi için bkz [yüksek kullanılabilirlik ve olağanüstü durum kurtarma Azure Virtual Machines'de SQL Server için](virtual-machines-windows-sql-high-availability-dr.md).

## <a name="comparing-web-development-strategies-in-azure"></a>Azure Web geliştirme stratejilerine karşılaştırma
tooimplement ve çok katmanlı bir SQL Server tabanlı bir uygulama azure'da dağıtmak için aşağıdaki iki programlama yöntemleri hello birini kullanabilirsiniz:

* Azure Virtual Machines'de SQL Server'ın Azure ve erişim veritabanlarındaki bir geleneksel web sunucusu (IIS - Internet Information Services) ayarlayın.
* Uygulama ve bir bulut hizmeti tooAzure dağıtın. Ardından, bu bulut hizmeti SQL Server'da veritabanlarını Azure sanal makinelerinde erişebildiğinden emin olun. Bir bulut hizmeti birden çok web ve çalışan rolleri ekleyebilirsiniz.

Aşağıdaki tablonun hello saygı tooSQL Azure Virtual Machines'de Server ile Azure Cloud Services ve Azure Web uygulamaları ile geleneksel web geliştirme karşılaştırması sağlar. Genel sanal IP adresi veya DNS adı aracılığıyla Azure Web uygulamaları için bir veri kaynağı olarak olası toouse Azure VM'deki SQL Server olduğu gibi hello tablo Azure Web uygulamaları içerir.

|  | Azure Virtual Machines'de geleneksel web geliştirme | Azure bulut Hizmetleri | Web barındırma ile Azure Web uygulamaları |
| --- | --- | --- | --- |
| **Şirket içi uygulama geçiş** |Var olan uygulamalar olarak-değil. |Uygulamaları, web ve çalışan rolleri gerekir. |Var olan uygulamalar olarak-kendi içindeki web uygulamaları ve hızlı ölçeklenebilirlik gerektiren web hizmetleri için ancak uygundur. |
| **Geliştirme ve dağıtım** |Visual Studio, WebMatrix, Visual Web Developer, WebDeploy, FTP, TFS, IIS Yöneticisi, PowerShell. |Visual Studio, Azure SDK, TFS, PowerShell. Her bir bulut hizmet yapılandırma ve hizmet paketi dağıtabilirsiniz iki ortamları toowhich sahiptir: hazırlama ve üretim. Ortam tootest hazırlama bir bulut hizmeti toohello dağıtabilmeniz için önce tooproduction Yükselt. |Visual Studio, WebMatrix, Visual Web Developer, FTP, GIT, BitBucket, CodePlex, DropBox, GitHub, Mercurial, TFS, Web PowerShell dağıtın. |
| **Yönetim ve Kur** |Merhaba uygulaması, verileri, güvenlik duvarı kuralları, sanal ağ ve işletim sistemi yönetim görevlerini siz sorumlusunuz. |Merhaba uygulaması, verileri, güvenlik duvarı kuralları ve sanal ağ üzerindeki yönetim görevleri için siz sorumlusunuz. |Yönetim görevlerini hello uygulama ve verileri yalnızca siz sorumlusunuz. |
| **Yüksek kullanılabilirlik ve olağanüstü durum kurtarma (HADR)** |Sanal makineler aynı kullanılabilirlik kümesi ve de aynı hello hello yerleştirmenizi öneririz bulut hizmeti. Vm'leriniz tutma, hello aynı kullanılabilirlik kümesi yükseltme etki alanları ve ayrı hata etki alanına bu Azure tooplace hello yüksek kullanılabilirlik düğümleri sağlar. Benzer şekilde, Vm'leriniz tutma hello aynı bulut hizmeti, Yük Dengeleme sağlar ve sanal makineleri doğrudan birbiriyle bir Azure veri merkezi içinde hello yerel ağ üzerinden iletişim kurabilir.<br/><br/>Yüksek kullanılabilirlik ve olağanüstü durum kurtarma çözümü SQL Server için Azure sanal makineleri tooavoid kapalı kalma süresi uygulamak için sorumlu. Desteklenen HADR teknolojileri için bkz: [yüksek kullanılabilirlik ve olağanüstü durum kurtarma Azure Virtual Machines'de SQL Server için](virtual-machines-windows-sql-high-availability-dr.md).<br/><br/>Kendi veri ve uygulama yedekleme için sorumlu.<br/><br/>Merhaba ana makine hello veri merkezinde toohardware sorunları başarısız olursa, azure sanal makinelerinizi taşıyabilirsiniz. Ayrıca, olabilir, VM'nin planlanan kapalı kalma süresi hello ana makine güvenlik veya yazılım güncelleştirildiğinde güncelleştirmeler. Bu nedenle, en az iki VM her uygulama katmanı tooensure hello sürekli kullanılabilirlik korumanızı öneririz. Azure SLA için tek bir sanal makine sağlamaz. Daha fazla bilgi için bkz: [Azure dayanıklılık teknik kılavuz](../../../resiliency/resiliency-technical-guidance.md). |Azure temel alınan donanım veya işletim sistemi yazılım hello kaynaklanan hello hataları yönetir. Bir web veya çalışan rolü tooensure hello yüksek kullanılabilirlik, uygulamanızın birden çok örneğini uygulamak öneririz. Bilgi için bkz: [bulut Hizmetleri, sanal makineler ve sanal ağ hizmet düzeyi sözleşmesi](http://www.microsoft.com/download/details.aspx?id=38427) ve [Azure uygulamaları için yüksek kullanılabilirlik ve olağanüstü durum kurtarma](../../../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)<br/><br/>Kendi veri ve uygulama yedekleme için sorumlu.<br/><br/>Azure VM'de SQL Server veritabanında bulunan veritabanları için bir yüksek kullanılabilirlik ve olağanüstü durum kurtarma çözümü tooavoid kapalı kalma süresi uygulamak için sorumlu. Desteklenen HDAR teknolojileri için Azure Virtual Machines'de SQL Server için yüksek kullanılabilirlik ve olağanüstü durum kurtarma bakın.<br/><br/>**SQL Server veritabanı yansıtma**: Azure bulut hizmetlerine (web/çalışan rolleri) kullanın. SQL Server VM'ler ve bulut hizmeti projesi olması içinde hello aynı Azure sanal ağı. SQL Server VM içinde değilse, aynı sanal ağ Merhaba, toocreate bir SQL Server diğer adı tooroute iletişimi toohello SQL Server örneği gerekir. Ayrıca, hello diğer ad hello SQL Server adı eşleşmelidir. |Yüksek kullanılabilirlik Azure çalışan rolleri, Azure blob depolama ve Azure SQL veritabanı devralınır. Örneğin, Azure Storage tüm blob, tablo ve kuyruk veri üç çoğaltmalarını korur. Herhangi bir zamanda Azure SQL Database çalıştıran verilerin üç çoğaltmalarının tutar — bir birincil çoğaltma ve iki ikincil çoğaltma. Daha fazla bilgi için bkz: [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) ve [Azure SQL veritabanı](../../../sql-database/sql-database-technical-overview.md).<br/><br/>SQL Server Azure Web uygulamaları için bir veri kaynağı olarak Azure VM'de kullanırken, Azure Web uygulamaları Azure sanal ağı desteklemiyor göz önünde bulundurun. Diğer bir deyişle, Azure Web Apps tooSQL Server VM'ler için Azure'da gelen tüm bağlantıları sanal makinelerin genel Uç noktalara gitmeniz gerekir. Bu, yüksek kullanılabilirlik ve olağanüstü durum kurtarma senaryoları için bazı sınırlamalar neden olabilir. Veritabanı yansıtma Azure sanal ağ içinde SQL Server ana VM'ler arasında kurma gerektirdiğinden Örneğin, Azure Web Apps tooSQL Server VM veritabanı yansıtma ile bağlanma hello istemci uygulaması mümkün tooconnect toohello yeni birincil sunucu olmaz Azure. Bu nedenle, kullanarak **SQL Server veritabanı yansıtma** Azure Web Apps ile şu anda desteklenmiyor.<br/><br/>**SQL Server AlwaysOn Kullanılabilirlik grupları**: Azure Web Apps ile Azure SQL Server Vm'lerinin kullanırken AlwaysOn Kullanılabilirlik grupları ayarlayabilirsiniz. Ancak tooconfigure AlwaysOn Kullanılabilirlik grubu dinleyicisi tooroute hello iletişimi toohello birincil çoğaltma ortak yük dengeli uç noktaları aracılığıyla gerekir. |
| **Şirket içi bağlantılar** |Azure Virtual Network tooconnect tooon içi kullanabilirsiniz. |Azure Virtual Network tooconnect tooon içi kullanabilirsiniz. |Azure sanal ağı desteklenir. Daha fazla bilgi için bkz: [Web uygulamaları sanal ağ tümleştirmesinin](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/). |
| **Ölçeklenebilirlik** |Büyütme hello sanal makine boyutlarını artırmayı veya daha fazla disk ekleme kullanılabilir. Sanal makine boyutları hakkında daha fazla bilgi için bkz: [Azure için sanal makine boyutlarını](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).<br/><br/>**Veritabanı sunucusu için**: genişleme veritabanı bölümleme teknikleri ve SQL Server AlwaysOn Kullanılabilirlik grupları aracılığıyla kullanılabilir.<br/><br/>Yoğun okuma iş yükleri için kullandığınız [AlwaysOn Kullanılabilirlik grupları](https://msdn.microsoft.com/library/hh510230.aspx) SQL Server çoğaltması yanı sıra birden fazla ikincil düğümü.<br/><br/>Ağır yazma iş yükleri için birden çok fiziksel sunucuları tooprovide uygulama genişleme arasında yatay bölümleme veri uygulayabilirsiniz.<br/><br/>Kullanarak bir genişletme ayrıca uygulayabilirsiniz [SQL Server veri bağımlı yönlendirme ile](https://technet.microsoft.com/library/cc966448.aspx). İle verileri bağımlı yönlendirme (DDR), hello istemci uygulamasında, genellikle hello iş katmanı katmanı yönteminde bölümleme tooimplement hello gerekir, tooroute hello veritabanı toomultiple SQL Server düğümlerinin ister. Merhaba iş katmanını içeren eşlemeleri toohow hello veri bölümlenmiş ve hangi düğümün hello verileri içerir.<br/><br/>Sanal makineler çalışmakta olan uygulamalar ölçeklendirebilirsiniz. Daha fazla bilgi için bkz: [nasıl tooScale uygulama](../../../cloud-services/cloud-services-how-to-scale.md).<br/><br/>**Önemli Not**: Merhaba **otomatik ölçeklendirme** azure'daki özelliği tooautomatically artış izin verir veya Merhaba, uygulamanız tarafından kullanılan sanal makineleri azaltın. Bu özellik yoğun dönemlerde hello son kullanıcı deneyimi olumsuz etkilenmez ve hello isteğe bağlı düşük olduğunda VM'ler kapatıldığından güvence altına alır. SQL Server Vm'lerinin içeriyorsa hello otomatik ölçeklendirme seçeneği'ı bulut hizmetinizin ayarlamayın önerilir. Merhaba, hello otomatik ölçeklendirme özelliği, hello CPU kullanımı, düşük olduğunda hello CPU kullanımı bu VM'de bazı eşik ve bir sanal makine kapalı tooturn daha yüksek olduğunda, bir sanal makinede Azure tooturn olanak tanır nedenidir. Merhaba otomatik ölçeklendirme özelliği, tüm VM hello iş yükü tüm başvuruları tooany önceki durumu olmadan yönetebileceği web sunucuları gibi durum bilgisiz uygulamaları için kullanışlıdır. Ancak, hello otomatik ölçeklendirme özelliğini toohello veritabanı yazma yalnızca bir örneği burada sağlar, SQL Server gibi durum bilgisi olan uygulamalar için yararlı değildir. |Büyütme birden çok web ve çalışan rolleri ile kullanılabilir. Web rolleri ve çalışan rolleri için sanal makine boyutları hakkında daha fazla bilgi için bkz: [Cloud Services boyutları yapılandırma](../../../cloud-services/cloud-services-sizes-specs.md).<br/><br/>Kullanırken **bulut Hizmetleri**, birden çok rol toodistribute işlemeyi tanımlayın ve ayrıca uygulamanızı esnek ölçeklemeyi elde etmek. Her bir bulut hizmeti bir veya daha fazla web rolleri ve/veya çalışan rolleri, her biri kendi uygulama dosyalarını ve yapılandırma içerir. Bir bulut hizmeti için bir rol dağıtılan hello sayıda rol örneği (sanal makineler) artırarak büyütme ve ölçek bir bulut hizmeti hello rol örneklerinin sayısını azaltarak açılır. Ayrıntılı bilgi için bkz: [Azure yürütme modelleri](../../../cloud-services/cloud-services-choose-me.md).<br/><br/>Azure yerleşik yüksek kullanılabilirlik desteğini aracılığıyla genişleme kullanılabilir [bulut Hizmetleri, sanal makineler ve sanal ağ hizmet düzeyi sözleşmesi](http://www.microsoft.com/download/details.aspx?id=38427) ve yük dengeleyici.<br/><br/>Çok katmanlı bir uygulama için web/çalışan rolleri uygulama toodatabase sunucusu sanal makineleri Azure sanal ağ üzerinden bağlanma öneririz. Ayrıca, Azure VM'ler için hello aynı yük dengelemesini sağlar bulut hizmeti, kullanıcı isteklerini arasında gezinmek yayılmak. Bu şekilde bağlı sanal makinelere, bir Azure veri merkezi içinde hello yerel ağ üzerinden doğrudan birbiriyle iletişim kurabilir.<br/><br/>Ayarlayabilirsiniz **otomatik ölçeklendirme** hello Azure portal ve bunun yanı sıra hello zamanlar. Daha fazla bilgi için bkz: [tooconfigure otomatik olarak nasıl hello portalında bulut hizmeti için ölçeklendirme](../../../cloud-services/cloud-services-how-to-scale-portal.md). |**Yukarı ve aşağı doğru ölçeklendirme**:, artırma/hello örneğinin (VM), web siteniz için ayrılmış hello boyutunu azaltma.<br/><br/>Ölçeği genişletme: web siteniz için daha ayrılmış örnekler (VM'ler) ekleyebilirsiniz.<br/><br/>Ayarlayabilirsiniz **otomatik ölçeklendirme** hello portal ve bunun yanı sıra hello zamanlar. Daha fazla bilgi için bkz: [nasıl tooScale Web Apps](../../../app-service-web/web-sites-scale.md). |

Bu programlama yöntemleri arasında seçme hakkında daha fazla bilgi için bkz: [Azure Web uygulamaları, bulut Hizmetleri ve sanal makineleri: zaman toouse hangi](../../../app-service-web/choose-web-site-cloud-service-vm.md).

## <a name="next-steps"></a>Sonraki Adımlar
SQL Server Azure sanal makinelerde çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makineleri genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).

