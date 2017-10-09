---
title: "aaaSQL sunucu üzerinde Azure sanal makineler ile ilgili SSS | Microsoft Docs"
description: "Bu makalede yanıtlar sağlayan Azure Vm'lerinde SQL Server çalıştıran hakkında sorular toofrequently."
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
ms.openlocfilehash: 70a8777bf765dcc69f433aa1fb59eb94929caab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-azure-virtual-machines"></a>Azure sanal makinelerinde SQL Server için sık sorulan sorular
Bu konu, çalışan ilgili en sık sorulan soruların yanıtları toosome Merhaba, sağlar [Azure Virtual Machines'de SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="frequently-asked-questions"></a>Sık Sorulan Sorular

1. **SQL Server ile nasıl bir Azure sanal makinesi oluşturulur?**

    Merhaba kolay toocreate SQL Server içeren bir sanal makine çözümüdür. Azure'a kaydolma ve hello Portalı'ndan bir SQL VM oluşturma bir öğretici için bkz: [hello Azure Portal'ın SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md). Dakika başına ödeme SQL Server Lisans kullanan bir sanal makine görüntüsünü seçebilir veya kendi SQL Server lisansınızı toobring sağlayan bir görüntü kullanabilirsiniz. El ile bir VM üzerinde SQL Server yükleme ve bir şirket içi lisans yeniden hello seçeneğiniz de vardır. Kendi lisansını Getir seçerseniz bulunmalıdır [azure'da Yazılım Güvencesi ile lisans taşınabilirliği](https://azure.microsoft.com/pricing/license-mobility/). Daha fazla bilgi için bkz. [SQL Server Azure VM’leri için fiyatlandırma kılavuzu](virtual-machines-windows-sql-server-pricing-guidance.md).

1. **Merhaba SQL VM'ler ve hello SQL veritabanı hizmetinin arasındaki fark nedir?**

    Kavramsal olarak, SQL Server olmayan bir uzak veri merkezinde SQL Server çalıştıran farklı olan bir Azure sanal makine üzerinde çalışan. Buna karşılık, [SQL veritabanı](../../../sql-database/sql-database-technical-overview.md) hizmet olarak veritabanı sunar. SQL veritabanı ile veritabanlarınızı barındırmak erişim toohello makineler sahip değil. Tam bir karşılaştırması için bkz: [bir bulut SQL Server seçeneği seçin: Azure SQL (PaaS) veritabanı veya SQL Server (Iaas) Azure vm'lerinde](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md).

1. **My şirket içi SQL Server veritabanı toohello bulut nasıl geçirebilir miyim?**

    İlk Azure sanal makinesi ile bir SQL Server örneği oluşturun. Ardından, şirket içi veritabanlarını toothat örneğinizin geçirin. Veri geçiş stratejileri için bkz: [bir SQL Server veritabanı tooSQL sunucusu Azure VM'deki geçirmek](virtual-machines-windows-migrate-sql.md).

1. **İkinci bir SQL Server örneği üzerinde hello yükleyebilirsiniz aynı VM? Merhaba varsayılan örnek yüklü özelliklerini değiştirebilir miyim?**

    Evet. Merhaba SQL Server yükleme medyasını hello bir klasörde bulunan **C** sürücü. Çalıştırma **Setup.exe** o konum tooadd yeni SQL Server örnekleri veya hello makinede SQL Server'ın yüklü toochange diğer özellikleri. Otomatik yedekleme, otomatik düzeltme eki uygulama ve Azure anahtar kasası tümleştirmeyi gibi bazı özellikler yalnızca hello varsayılan örnek karşı çalıştığını unutmayın.

1. **SQL Server varsayılan örneğini hello kaldırabilir miyim?**

    Evet. Ancak bazı noktalar vardır. Merhaba önceki yanıtında, üzerinde hello kullanan özellikler belirtildiği gibi [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md) yalnızca hello varsayılan örneğinde çalışır. Merhaba varsayılan örnek kaldırırsanız, hello uzantısı toolook devam eder ve olay günlüğünü hatalara neden. Bu hatalar aşağıdaki iki kaynaklar hello olur: **Microsoft SQL Server kimlik bilgileri yönetimi** ve **Microsoft SQL Server Iaas Aracısı**. Merhaba hataları benzer toohello aşağıdakilerden biri olabilir:
    
        A network-related or instance-specific error occurred while establishing a connection tooSQL Server. hello server was not found or was not accessible. 
        
    Toouninstall hello varsayılan örnek karar verirseniz, aynı zamanda hello kaldırma [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md) de.

1. **Tooa yeni sürümü/yayını hello Azure VM'deki SQL Server'ın nasıl yükseltme?**

    Şu anda hiçbir yerinde yükseltme bir Azure VM içinde çalışan SQL Server için yoktur. İstenen hello SQL Server sürümü/yayını ile yeni bir Azure sanal makine oluşturun ve standart kullanarak veritabanlarını toohello yeni sunucuya geçirme [veri geçiş teknikleri](virtual-machines-windows-migrate-sql.md).

1. **Azure VM temelinde my lisanslı SQL Server kopyası nasıl yükleyebilirim?**

    Var olan iki yolu toodo bu. Merhaba birini sağlayabilirsiniz [lisansları destekleyen sanal makine görüntülerini](virtual-machines-windows-sql-server-iaas-overview.md#BYOL). Başka bir seçenek toocopy hello SQL Server yükleme medyası tooa Windows Server VM ve VM hello üzerinde SQL Server'i yükleyin. Nedenlerden lisans için sahip olmanız gerekir [azure'da Yazılım Güvencesi ile lisans taşınabilirliği](https://azure.microsoft.com/pricing/license-mobility/). Daha fazla bilgi için bkz. [SQL Server Azure VM’leri için fiyatlandırma kılavuzu](virtual-machines-windows-sql-server-pricing-guidance.md).

1. **Merhaba Kullandıkça Öde galeri görüntülerden birini oluşturulduysa, kendi SQL Server Lisans VM toouse değiştirebilirim?**

    Hayır. Dakika başına ödeme lisans toousing kendi lisansını geçebilirsiniz değil. Yeni Azure hello birini kullanarak sanal makine oluşturma [KLG görüntüleri](virtual-machines-windows-sql-server-iaas-overview.md#BYOL), ve standart kullanarak veritabanlarını toohello yeni sunucuya geçirme [veri geçiş teknikleri](virtual-machines-windows-migrate-sql.md).

1. **Azure Vm'lerinde SQL Server Yük devretme kümesi örneği (FCI) destekleniyor mu?**

   Evet. Yapabilecekleriniz [Windows Server 2016 Windows Yük devretme kümesi oluşturma](virtual-machines-windows-portal-sql-create-failover-cluster.md) ve depolama alanları doğrudan (S2D) hello küme depolama alanını kullanın. Alternatif olarak, açıklandığı gibi üçüncü taraf kümeleme veya depolama çözümleri kullanabilirsiniz [Azure Virtual Machines'de SQL Server için yüksek kullanılabilirlik ve olağanüstü durum kurtarma](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions).

1. **Toopay toolicense Azure VM'de SQL Server, yalnızca bekleme/yük devretme için kullanılıyorsa var mı?**

    Çalıştırıyorsanız, Yazılım Güvencesi ve lisans taşınabilirliği açıklandığı gibi kullanmak toopay toolicense bir SQL Server HA dağıtımında, pasif bir ikincil çoğaltma olarak katılan yok [sanal makine Lisansı hakkında SSS](http://azure.microsoft.com/pricing/licensing-faq/).

1. **Nasıl güncelleştirmeleri ve hizmet paketleri bir SQL Server VM üzerinde uygulanır?**

    Ne zaman ve nasıl güncelleştirmeleri uygulamak gibi hello konak makinesi üzerinde denetim sanal makineleri sağlar. Merhaba işletim sistemi için windows güncelleştirmelerini el ile uygulayabilirsiniz veya adı verilen bir zamanlama hizmeti etkinleştirebilirsiniz [otomatik düzeltme eki uygulama](virtual-machines-windows-sql-automated-patching.md). Otomatik Düzeltme Eki Uygulama, önemli olarak işaretlenmiş tüm güncelleştirmeleri, bu kategorideki SQL Server güncelleştirmeleri de dahil olmak üzere yükler. Diğer isteğe bağlı güncelleştirmeler tooSQL sunucu elle yüklenmesi gerekir.

1. **Merhaba sanal makineye Galerisi (örneğin Windows 2008 R2 + SQL Server 2012) içinde gösterilmez yapılandırmaları yukarı olası tooset mi?**

    Hayır. SQL Server içeren sanal makineye Galerisi görüntüler için sağlanan görüntüler hello birini seçmeniz gerekir.

1. **My Azure VM nasıl SQL Data araçları yükleme?**

     Merhaba SQL veri Araçları'ndan yükleyip [Microsoft SQL Server veri araçları - Visual Studio 2013 iş zekası](https://www.microsoft.com/en-us/download/details.aspx?id=42313).

## <a name="resources"></a>Kaynaklar

Azure Virtual Machines'de SQL Server genel bakış için hello videoyu izleyin [Azure VM, SQL Server 2016 için en iyi platformdur hello](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016). İyi bir giriş hello konudaki alabilirsiniz [Azure sanal makinelere genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).

Diğer kaynaklar şunlardır:

* [Hello Azure Portal'ın SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md)
* [Veritabanı tooSQL bir Azure VM sunucuda geçirme](virtual-machines-windows-migrate-sql.md)
* [Yüksek kullanılabilirlik ve olağanüstü durum kurtarma için Azure sanal makinelerde SQL Server](virtual-machines-windows-sql-high-availability-dr.md)
* [Azure Sanal Makineler’de SQL Server için performansa yönelik en iyi uygulamalar](virtual-machines-windows-sql-performance.md)
* [Azure Sanal Makineler'de SQL Server için Uygulama Desenleri ve Geliştirme Stratejileri](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md) 