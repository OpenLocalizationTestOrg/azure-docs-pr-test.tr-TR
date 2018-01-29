---
title: "Azure Windows Sanal Makinelerinde SQL Server'a Genel Bakış | Microsoft Docs"
description: "Azure Sanal Makineler’de tam SQL Server sürümlerini çalıştırma hakkında bilgi edinin."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: c505089e-6bbf-4d14-af0e-dd39a1872767
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 12/14/2017
ms.author: jroth
ms.openlocfilehash: 95a18e4b2437ca628e84f6d6f580e12f2f26e111
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/16/2017
---
# <a name="what-is-sql-server-on-azure-virtual-machines-windows"></a>Azure Sanal Makinelerinde SQL Server nedir? (Windows)

> [!div class="op_single_selector"]
> * [Windows](virtual-machines-windows-sql-server-iaas-overview.md)
> * [Linux](../../linux/sql/sql-server-linux-virtual-machines-overview.md)

[Azure sanal makinelerinde SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/), şirket içi donanım yönetmenize gerek kalmadan tam SQL Server sürümlerini Bulut’ta kullanmanıza olanak sağlar. SQL Server VM’leri, kullandıkça ödeme yaptığınızda lisanslama maliyetlerini de basitleştirir.

Azure sanal makineleri dünyanın birçok farklı [coğrafi bölgesinde](https://azure.microsoft.com/regions/) çalışır. Bu makineler, ayrıca çeşitli [makine boyutları](../sizes.md) sunar. Sanal makine resim galerisi, doğru sürüm ve işletim sistemiyle bir SQL Server VM’i oluşturmanızı sağlar. Bu, sanal makineleri birçok farklı SQL Server iş yükleri için iyi bir seçenek yapar.

## <a name="automated-updates"></a>Otomatik güncelleştirmeler

SQL Server Azure sanal makineleri, önemli Windows ve SQL Server güncelleştirmelerini otomatik olarak yüklemek için bir bakım penceresi zamanlamak üzere [Otomatik Düzeltme Eki Uygulama](virtual-machines-windows-sql-automated-patching.md) özelliğini kullanabilir.

## <a name="automated-backups"></a>Otomatik yedeklemeler

SQL Server Azure sanal makineleri, blob depolama alanında düzenli olarak veritabanınızın yedeklerini oluşturan [Otomatik Yedekleme](virtual-machines-windows-sql-automated-backup-v2.md) özelliğinden yararlanabilir. Bu tekniği el ile de kullanabilirsiniz. Daha fazla bilgi için. bkz. [SQL Server Yedekleme ve Geri Yükleme için Azure Storage’ı Kullanma](virtual-machines-windows-use-storage-sql-server-backup-restore.md).

## <a name="high-availability"></a>Yüksek kullanılabilirlik

Size yüksek kullanılabilirlik gerekiyorsa, SQL Server Kullanılabilirlik gruplarını yapılandırmayı dikkate alın. Bu, bir sanal ağda birden fazla SQL Server Azure VM’leri içerir. Yüksek kullanılabilirlik çözümünüzü kendiniz yapılandırabilir veya otomatik yapılandırma için Azure portalındaki şablonları kullanabilirsiniz. Tüm yüksek kullanılabilirlik seçeneklerine genel bir bakış için bkz. [Azure Sanal Makineler’de SQL Server için Yüksek Kullanılabilirlik ve Olağanüstü Durum Kurtarma](virtual-machines-windows-sql-high-availability-dr.md).

## <a name="performance"></a>Performans

Azure sanal makineleri çeşitli iş yükü taleplerini karşılamak üzere farklı makine boyutları sunar. SQL VM'leri ayrıca performans gereksinimleriniz için en iyi duruma getirilmiş otomatik depolama yapılandırması sağlar. SQL VM'lerine ilişkin depolama yapılandırması hakkında daha fazla bilgi için bkz. [SQL Server VM'leri için depolama yapılandırması](virtual-machines-windows-sql-server-storage-configuration.md). Performansı ayarlamak için bkz. [Azure Sanal Makineler’de SQL Server için performansa yönelik en iyi uygulamalar](virtual-machines-windows-sql-performance.md).

## <a name="get-started-with-sql-vms"></a>SQL VM’lerini kullanmaya başlayın

Kullanmaya başlamak için, gerekli olan sürüm ve işletim sisteminizle birlikte bir SQL Server sanal makine resmi seçin. Aşağıdaki bölümlerde SQL Server sanal makine galeri görüntüleri için Azure portalının doğrudan bağlantıları verilmektedir.

> [!TIP]
> Bu görüntülerin VM ve SQL fiyatlandırmasını anlamak için bkz. [SQL Server Azure VM’leri için fiyatlandırma kılavuzu](virtual-machines-windows-sql-server-pricing-guidance.md).

> [!TIP]
> SQL Server sanal makine galeri görüntüleri için güncelleştirme ve yaşam döngüsü ilkesini anlamak üzere bkz. [SQL Server VM'leri SSS](virtual-machines-windows-sql-server-iaas-faq.md#images).

### <a id="payasyougo"></a> Kullandıkça ödeyin
Şu tabloda, kullandıkça öde SQL Server resimlerinin bir matrisi verilmektedir.

| Sürüm | İşletim Sistemi | Sürüm |
| --- | --- | --- |
| **SQL Server 2017** |Windows Server 2016 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2017EnterpriseWindowsServer2016), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2017StandardonWindowsServer2016), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2017WebonWindowsServer2016), [Express](https://portal.azure.com/#create/Microsoft.FreeSQLServerLicenseSQLServer2017ExpressonWindowsServer2016), [Developer](https://portal.azure.com/#create/Microsoft.FreeSQLServerLicenseSQLServer2017DeveloperonWindowsServer2016) |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1ExpressWindowsServer2016), [Developer](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1DeveloperWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2ExpressWindowsServer2012R2) |
| **SQL Server 2012 SP3** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2) |
| **SQL Server 2008 R2 SP3** |Windows Server 2008 R2|[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2008R2SP3EnterpriseWindowsServer2008R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2008R2SP3StandardWindowsServer2008R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2008R2SP3WebWindowsServer2008R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2008R2SP3ExpressWindowsServer2008R2) |

Kullanabileceğiniz Linux SQL Server sanal makine görüntülerini görmek için bkz. [Azure Sanal Makinelerinde SQL Server'a Genel Bakış (Linux)](../../linux/sql/sql-server-linux-virtual-machines-overview.md).

### <a id="BYOL"></a> Kendi lisansını getir
Ayrıca kendi lisansınızı getirebilirsiniz (KLG). Bu senaryoda, SQL Server Lisans için hiçbir ek bir ücret olmadan yalnızca VM için ödeme yaparsınız.  Kendi lisansınızı getirmek, sürekli üretim iş yüklerinde zaman içinde paradan tasarruf etmenizi sağlayabilir. Bu seçeneği kullanmaya yönelik gereksinimler için bkz. [SQL Server Azure VM’leri için fiyatlandırma kılavuzu](virtual-machines-windows-sql-server-pricing-guidance.md).

| Sürüm | İşletim sistemi | Sürüm |
| --- | --- | --- |
| **SQL Server 2017** |Windows Server 2016 |[Enterprise KLG](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2017EnterpriseWindowsServer2016), [Standard KLG](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2017StandardonWindowsServer2016) |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise KLG](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016), [Standard KLG](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise KLG](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard KLG](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2StandardWindowsServer2012R2) |
| **SQL Server 2012 SP2** |Windows Server 2012 R2 |[Enterprise KLG](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard KLG](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3StandardWindowsServer2012R2) |

Portalda, bu görüntü adlarına **{KLG}** ön eki getirilir.

### <a name="connect-to-the-vm"></a>VM’ye bağlanma
SQL Server sanal makinenizi oluşturduktan sonra, SQL Server Management Studio (SSMS) gibi uygulamalar veya araçlardan bu makineye bağlanın. Yönergeler için bkz. [Azure’da SQL Server Sanal Makinesine Bağlanma](virtual-machines-windows-sql-connect.md).

### <a name="migrate-your-data"></a>Verilerinizi geçirme
Varolan bir veritabanınız varsa, bunu yeni sağlanan SQL VM'ye taşımak istersiniz. Geçiş seçenekleri ve kılavuzların listesi için bkz. [Azure VM’de bir Veritabanını SQL Server’a Geçirme](virtual-machines-windows-migrate-sql.md).

## <a name="customer-experience-improvement-program-ceip"></a>Müşteri deneyimini geliştirme programı (CEIP)
Müşteri Deneyimini Geliştirme Programı (CEIP) varsayılan olarak etkindir. Bu, SQL Server’ın geliştirilmesine yardımcı olmak için Microsoft’a düzenli olarak raporlar gönderir. CEIP’i hazırladıktan sonra devre dışı bırakmak istemiyorsanız CEIP için herhangi bir yönetim görevi gerekmez. VM’ye uzak masaüstüyle bağlanarak CEIP özelleştirebilir ya da devre dışı bırakabilirsiniz. Ardından **SQL Server Hata ve Kullanım Raporlama** yardımcı programını çalıştırın. Raporlamayı devre dışı bırakmak için yönergeleri izleyin. Veri toplama hakkında daha fazla bilgi için bkz. [SQL Server Gizlilik Bildirimi](https://www.microsoft.com/EN-US/privacystatement/SQLServer/Default.aspx).

## <a name="related-products-and-services"></a>İlgili ürün ve hizmetler
### <a name="windows-virtual-machines"></a>Windows Sanal Makineleri
* [Sanal Makinelere genel bakış](../overview.md)

### <a name="storage"></a>Depolama
* [Microsoft Azure Depolama'ya Giriş](../../../storage/common/storage-introduction.md)

### <a name="networking"></a>Ağ
* [Sanal Ağ’a genel bakış](../../../virtual-network/virtual-networks-overview.md)
* [Azure’da IP adresleri](../../../virtual-network/virtual-network-ip-addresses-overview-arm.md)
* [Azure Portal'da Tam Etki Alanı Adı oluşturma](../portal-create-fqdn.md)

### <a name="sql"></a>SQL
* [SQL Server belgeleri](https://docs.microsoft.com/sql/index)
* [Azure SQL Veritabanı karşılaştırması](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md)

## <a name="next-steps"></a>Sonraki adımlar

Azure sanal makinelerinde SQL Server kullanmaya başlayın:

* [Azure portalında SQL Server VM’i oluşturma](quickstart-sql-vm-create-portal.md)

SQL VM'ler hakkında sık sorulan soruların yanıtlarını alın:

* [Azure Sanal Makineler’de SQL Server ile ilgili SSS](virtual-machines-windows-sql-server-iaas-faq.md)
