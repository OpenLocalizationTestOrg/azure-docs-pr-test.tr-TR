---
title: SQL Server Azure sanal makinelerinde SSS | Microsoft Docs
description: "Bu makale Azure Vm'lerinde SQL Server çalıştıran hakkında sık sorulan soruların yanıtlarını sağlar."
services: virtual-machines-windows
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
tags: azure-service-management
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: v-shysun
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 447ece9653a4cf69153f9c85e222e3ea4e8bae16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-azure-virtual-machines"></a>Azure sanal makinelerinde SQL Server için sık sorulan sorular
Bu konuda çalıştırma hakkında en yaygın sorulara yanıtlar sağlayan [Azure Virtual Machines'de SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="frequently-asked-questions"></a>Sık Sorulan Sorular

1. **SQL Server ile nasıl bir Azure sanal makinesi oluşturulur?**

    SQL Server içeren bir sanal makine oluşturmak için en kolay çözüm olur. Azure'a kaydolma ve Portalı'ndan bir SQL VM oluşturma bir öğretici için bkz: [Azure Portal'da bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md). Dakika başına ödeme SQL Server Lisans kullanan bir sanal makine görüntüsünü seçebilir veya kendi SQL Server lisansınızı getirebilir olanak tanıyan bir görüntü kullanabilirsiniz. El ile bir VM üzerinde SQL Server yükleme ve bir şirket içi lisans yeniden kullanma seçeneğiniz de vardır. Kendi lisansını Getir seçerseniz bulunmalıdır [azure'da Yazılım Güvencesi ile lisans taşınabilirliği](https://azure.microsoft.com/pricing/license-mobility/). Daha fazla bilgi için bkz. [SQL Server Azure VM’leri için fiyatlandırma kılavuzu](virtual-machines-windows-sql-server-pricing-guidance.md).

1. **SQL veritabanı hizmetinin SQL VMs arasındaki fark nedir?**

    Kavramsal olarak, SQL Server olmayan bir uzak veri merkezinde SQL Server çalıştıran farklı olan bir Azure sanal makine üzerinde çalışan. Buna karşılık, [SQL veritabanı](../../../sql-database/sql-database-technical-overview.md) hizmet olarak veritabanı sunar. SQL veritabanı ile veritabanlarınızı barındırmak makinelere erişimi sahip değil. Tam bir karşılaştırması için bkz: [bir bulut SQL Server seçeneği seçin: Azure SQL (PaaS) veritabanı veya SQL Server (Iaas) Azure vm'lerinde](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md).

1. **Nasıl şirket içi SQL Server veritabanını buluta geçişini sağlayabilir miyim?**

    İlk Azure sanal makinesi ile bir SQL Server örneği oluşturun. Ardından, şirket içi veritabanlarını bu örneğe geçirin. Veri geçiş stratejileri için bkz: [Azure VM'deki SQL Server için SQL Server veritabanını geçirme](virtual-machines-windows-migrate-sql.md).

1. **Aynı VM'de SQL Server ikinci bir örneğini yükleyebilir miyim? Varsayılan örnek yüklü özelliklerini değiştirebilir miyim?**

    Evet. SQL Server yükleme ortamının bir klasörde bulunan **C** sürücü. Çalıştırma **Setup.exe** yeni SQL Server örnekleri eklemek için bu konuma veya bu makinede SQL Server'ın yüklü değişiklik diğer özellikleri. Otomatik yedekleme, otomatik düzeltme eki uygulama ve Azure anahtar kasası tümleştirmeyi gibi bazı özellikler yalnızca varsayılan örnek karşı çalıştığını unutmayın.

1. **SQL Server'ın varsayılan örneğinin kaldırabilir miyim?**

    Evet. Ancak bazı noktalar vardır. Önceki yanıtında belirtildiği gibi özellikler, Bel [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md) yalnızca varsayılan örneğinde çalışır. Varsayılan örnek kaldırırsanız, uzantısı aramanız olmaya devam eder ve olay günlüğünü hatalara neden. Bu hatalar aşağıdaki iki kaynaktan kaynaklanır: **Microsoft SQL Server kimlik bilgileri yönetimi** ve **Microsoft SQL Server Iaas Aracısı**. Hatalardan biri, aşağıdakine benzer olabilir:
    
        A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. 
        
    Varsayılan örnek kaldırmaya karar verirseniz ayrıca kaldırma [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md) de.

1. **Bir Azure VM'de SQL Server'ın yeni bir sürümü/yayını için nasıl yükseltme?**

    Şu anda hiçbir yerinde yükseltme bir Azure VM içinde çalışan SQL Server için yoktur. İstenen SQL Server sürümü/yayını ile yeni bir Azure sanal makine oluşturma ve ardından veritabanlarınızı standart kullanarak yeni sunucuya geçiş [veri geçiş teknikleri](virtual-machines-windows-migrate-sql.md).

1. **Azure VM temelinde my lisanslı SQL Server kopyası nasıl yükleyebilirim?**

    Bunu yapmanın iki yolu vardır. Aşağıdakilerden birini sağlayabilirsiniz [lisansları destekleyen sanal makine görüntülerini](virtual-machines-windows-sql-server-iaas-overview.md#BYOL). Windows Server VM için SQL Server yükleme medyasını kopyalayın ve ardından SQL Server VM yüklemeniz ise başka bir seçenektir. Nedenlerden lisans için sahip olmanız gerekir [azure'da Yazılım Güvencesi ile lisans taşınabilirliği](https://azure.microsoft.com/pricing/license-mobility/). Daha fazla bilgi için bkz. [SQL Server Azure VM’leri için fiyatlandırma kılavuzu](virtual-machines-windows-sql-server-pricing-guidance.md).

1. **Kullandıkça Öde galeri görüntülerden birini oluşturulduysa, kendi SQL Server lisansınızı kullanmak için bir VM değiştirebilir miyim?**

    Hayır. Kendi lisansınızı kullanmak için dakika başına ödeme lisans geçebilirsiniz değil. Yeni Azure birini kullanarak sanal makine oluşturma [KLG görüntüleri](virtual-machines-windows-sql-server-iaas-overview.md#BYOL), ve veritabanlarınızı standart kullanarak yeni sunucusuna geçirmenize [veri geçiş teknikleri](virtual-machines-windows-migrate-sql.md).

1. **Azure Vm'lerinde SQL Server Yük devretme kümesi örneği (FCI) destekleniyor mu?**

   Evet. Yapabilecekleriniz [Windows Server 2016 Windows Yük devretme kümesi oluşturma](virtual-machines-windows-portal-sql-create-failover-cluster.md) ve küme depolaması için depolama alanları doğrudan (S2D) kullanın. Alternatif olarak, açıklandığı gibi üçüncü taraf kümeleme veya depolama çözümleri kullanabilirsiniz [Azure Virtual Machines'de SQL Server için yüksek kullanılabilirlik ve olağanüstü durum kurtarma](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions).

1. **Azure VM'de SQL Server Lisans için yalnızca bekleme/yük devretme için kullanılıyorsa ödeme var mı?**

    Bir HA dağıtımında, pasif bir ikincil çoğaltma olarak çalıştırıyorsanız, Yazılım Güvencesi ve lisans taşınabilirliği açıklandığı gibi kullanın katılan bir SQL Server Lisans ödeme gerekmez [sanal makine Lisansı hakkında SSS](http://azure.microsoft.com/pricing/licensing-faq/).

1. **Nasıl güncelleştirmeleri ve hizmet paketleri bir SQL Server VM üzerinde uygulanır?**

    Ne zaman ve nasıl güncelleştirmeleri uygulamak gibi konak makinesi üzerinde denetim sanal makineleri sağlar. İşletim sistemi için windows güncelleştirmelerini el ile uygulayabilirsiniz veya adı verilen bir zamanlama hizmeti etkinleştirebilirsiniz [otomatik düzeltme eki uygulama](virtual-machines-windows-sql-automated-patching.md). Otomatik Düzeltme Eki Uygulama, önemli olarak işaretlenmiş tüm güncelleştirmeleri, bu kategorideki SQL Server güncelleştirmeleri de dahil olmak üzere yükler. SQL Server için diğer isteğe bağlı güncelleştirmeler el ile yüklenmelidir.

1. **Sanal makineye Galerisi (örneğin Windows 2008 R2 + SQL Server 2012) içinde gösterilmez yapılandırmaları ayarlamak mümkün mü?**

    Hayır. SQL Server içeren sanal makineye Galerisi görüntüler için sağlanan görüntülerden birini seçmeniz gerekir.

1. **My Azure VM nasıl SQL Data araçları yükleme?**

     SQL veri Araçları'ndan yükleyip [Microsoft SQL Server veri araçları - Visual Studio 2013 iş zekası](https://www.microsoft.com/en-us/download/details.aspx?id=42313).

## <a name="resources"></a>Kaynaklar

Azure Virtual Machines'de SQL Server genel bakış videosunu izleyin [Azure VM, SQL Server 2016 için en iyi platformdur](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016). İyi bir giriş konusunda alabilirsiniz [Azure sanal makinelere genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).

Diğer kaynaklar şunlardır:

* [Azure Portal’da bir SQL Server sanal makinesi sağlama](virtual-machines-windows-portal-sql-server-provision.md)
* [SQL Server Azure VM'de bir veritabanını geçirme](virtual-machines-windows-migrate-sql.md)
* [Yüksek kullanılabilirlik ve olağanüstü durum kurtarma için Azure sanal makinelerde SQL Server](virtual-machines-windows-sql-high-availability-dr.md)
* [Azure Sanal Makineler’de SQL Server için performansa yönelik en iyi uygulamalar](virtual-machines-windows-sql-performance.md)
* [Azure Sanal Makineler'de SQL Server için Uygulama Desenleri ve Geliştirme Stratejileri](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md) 