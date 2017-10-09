---
title: "Azure Virtual Machines'de SQL Server'ın aaaOverview | Microsoft Docs"
description: "Nasıl toorun tam Azure sanal makinelerde SQL Server sürümleri hakkında bilgi edinin. Doğrudan bağlantılar tooall SQL Server VM görüntüleri ve ilgili içerik alın."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: c505089e-6bbf-4d14-af0e-dd39a1872767
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: 07be567c76f4435961592fc0872fe41cd45bd79d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-sql-server-on-azure-virtual-machines"></a>Azure Virtual Machines’de SQL Server’a Genel Bakış
Bu konu ile birlikte Azure sanal makinelerde (VM'ler) SQL Server çalıştıran seçeneklerinizi açıklar [tooportal görüntüleri bağlantılar](#option-1-create-a-sql-vm-with-per-minute-licensing) genel bakış [ortak görevleri](#manage-your-sql-vm).

> [!NOTE]
> Zaten SQL Server ile tanıdık ve yalnızca toosee nasıl toodeploy bir SQL Server VM görmek istediğiniz [hello Azure portal'ın SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).
> 
> 

## <a name="overview"></a>Genel Bakış
Veritabanı Yöneticisi veya bir geliştirici, Azure VM'ler, şirket içi SQL Server iş yüklerini ve uygulamaları toohello bulut şekilde toomove sağlar. Merhaba aşağıdaki video SQL Server Azure Vm'lerinin teknik genel bakış sağlar.

> [!VIDEO https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016/player]
> 
> 

Merhaba video alanları aşağıdaki hello kapsar:

| Zaman | Alan |
| --- | --- |
| 00:21 |Azure VM’leri nedir? |
| 01:45 |Güvenlik |
| 02:50 |Bağlantı |
| 03:30 |Depolama güvenilirliği ve performansı |
| 05:20 |VM boyutları |
| 05:54 |Yüksek kullanılabilirlik ve SLA |
| 07:30 |Yapılandırma desteği |
| 08:00 |İzleme |
| 08:32 |Demo: SQL Server 2016 VM’si oluşturma |

> [!NOTE]
> SQL Server 2016 Hello video odaklanır, ancak Azure VM görüntüleri için SQL Server 2012, 2014 ve 2016 dahil, birçok sürümleri sağlar. 
> 
> 

## <a name="scenarios"></a>Senaryolar
Verilerinizi Azure'da toohost seçebilirsiniz pek çok neden vardır. Uygulamanızı tooAzure taşıyorsanız, performans tooalso taşıma hello verileri artırır. Bununla birlikte, başka avantajları da vardır. Otomatik olarak erişim toomultiple veri merkezlerinde genel varlık ve olağanüstü durum kurtarma için var. Merhaba de son derece güvenli ve sağlam verilerdir.

Azure VM’lerinde çalışan SQL Server, ilişkisel verilerinizi Azure’da depolamak için yararlanabileceğiniz bir seçenektir. Birkaç senaryo için iyi bir seçimdir. Örneğin, tooconfigure hello Azure VM olası tooan şirket içi SQL Server makinesinde olarak benzer bir şekilde isteyebilirsiniz. Toorun ek uygulamalar ve hizmetler hello istediğiniz veya aynı veritabanı sunucusu. Daha fazla senaryoyu ve dikkat edilmesi gereken noktayı göz önünde bulundurmanıza yardım edebilecek iki ana kaynak vardır:

* [Azure virtual machines'de SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/) Azure Vm'lerinde SQL Server kullanmak için hello en iyi senaryolarına genel bir bakış sağlar. 
* [Bir bulut SQL Server seçeneği belirleyin: Azure SQL (PaaS) Veritabanı ya da Azure VM’lerde SQL Server (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md), SQL Veritabanı ve VM’de çalışan SQL Server arasında ayrıntılı bir karşılaştırma sağlar.

## <a name="create-a-new-sql-vm"></a>Yeni bir SQL sanal makinesi oluşturma
Merhaba aşağıdaki bölümler doğrudan bağlantılar toohello Azure portal hello SQL Server sanal makineye Galerisi görüntülerde sağlar. Seçtiğiniz hello görüntü bağlı olarak SQL Server Lisans maliyetleri için dakika başına temelinde ya da ödeme olabilir veya kendi lisansını (KLG) kullanıma sunabilirsiniz.

Merhaba öğreticide, yeni bir SQL VM oluşturmak için adım adım yönergeler Bul [hello Azure portal'ın SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md). Ayrıca, hello gözden [SQL Server VM'ler için performans en iyi uygulamaları](virtual-machines-windows-sql-performance.md), nasıl tooselect hello uygun makine boyutunu ve diğer sağlama işlemi sırasında kullanılabilir özellikleri açıklanmaktadır.

## <a name="option-1-create-a-sql-vm-with-per-minute-licensing"></a>Seçenek 1: Dakika başına lisanslama ile SQL sanal makinesi oluşturma
Merhaba aşağıdaki tabloda hello sanal makineye Galerisi hello en son SQL Server görüntülerinin bir matrisi verilmektedir. Belirtilen sürüm, sürümü ve işletim sistemi ile yeni bir SQL VM oluşturma herhangi bir bağlantı toobegin tıklayın. 

> [!TIP]
> toounderstand hello VM ve bu görüntüleri için SQL fiyatlandırma bkz [Kılavuzu SQL Server Azure VM'ler için fiyatlandırma](virtual-machines-windows-sql-server-pricing-guidance.md).

| Sürüm | İşletim Sistemi | Sürüm |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1ExpressWindowsServer2016), [Developer](https://portal.azure.com/#create/Microsoft.SQLServer2016SP1DeveloperWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2014SP2ExpressWindowsServer2012R2) |
| **SQL Server 2012 SP3** |Windows Server 2012 R2 |[Enterprise](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2), [Web](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2), [Express](https://portal.azure.com/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2) |

Ayrıca toothis listesinde, diğer SQL Server sürümleri ve işletim sistemleri kullanılabilir birleşimleridir. Market arama yoluyla diğer görüntüleri hello Azure portal bulur. 

## <a id="BYOL"></a> Seçenek 2: Var olan bir lisans ile SQL sanal makinesi oluşturma
Ayrıca kendi lisansınızı getirebilirsiniz (KLG). Bu senaryoda, yalnızca SQL Server Lisans için hiçbir ek bir ücret olmadan hello VM için ödeme yaparsınız. toouse kendi lisansını, SQL Server sürümleri, sürümleri ve işletim sistemleri aşağıdaki hello matrisini kullanın. Merhaba Portalı'nda bu görüntü adları ile önek **{KLG}**.

> [!TIP]
> Kendi lisansınızı getirmek, sürekli üretim iş yüklerinde zaman içinde paradan tasarruf etmenizi sağlayabilir. Daha fazla bilgi için bkz. [SQL Server Azure VM’leri için fiyatlandırma kılavuzu](virtual-machines-windows-sql-server-pricing-guidance.md).

| Sürüm | İşletim sistemi | Sürüm |
| --- | --- | --- |
| **SQL Server 2016 SP1** |Windows Server 2016 |[Enterprise KLG](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016), [Standard KLG](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016) |
| **SQL Server 2014 SP2** |Windows Server 2012 R2 |[Enterprise KLG](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2EnterpriseWindowsServer2012R2), [Standard KLG](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2014SP2StandardWindowsServer2012R2) |
| **SQL Server 2012 SP2** |Windows Server 2012 R2 |[Enterprise KLG](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3EnterpriseWindowsServer2012R2), [Standard KLG](https://portal.azure.com/#create/Microsoft.BYOLSQLServer2012SP3StandardWindowsServer2012R2) |

Ayrıca toothis listesinde, diğer SQL Server sürümleri ve işletim sistemleri kullanılabilir birleşimleridir. Hello Azure portal ("{KLG} SQL Server" Ara) Market arama yoluyla diğer görüntüleri bulun.

> [!IMPORTANT]
> toouse KLG VM görüntüleri, bir Kuruluş Sözleşmesi ile olmalıdır [azure'da Yazılım Güvencesi ile lisans taşınabilirliği](https://azure.microsoft.com/pricing/license-mobility/). Geçerli bir lisans da gerekir hello sürümü/yayını için SQL Server'ın toouse istiyor. Yapmanız gerekenler [hello gerekli KLG bilgilerini tooMicrosoft sağlamak](http://d36cz9buwru1tt.cloudfront.net/License_Mobility_Customer_Verification_Guide.pdf) içinde **10** VM'nizi sağladıktan gün. 

> [!NOTE]
> Dakika başına ödeme SQL Server VM toouse modelinin kendi lisansını lisans olası toochange hello olmadığı. Bu durumda, yeni bir KLG VM oluşturmalı ve veritabanları toohello geçirmek yeni VM. 

## <a name="manage-your-sql-vm"></a>SQL VM’nizi yönetme
SQL Server sanal makinenizi sağladıktan sonra isteğe bağlı birkaç yönetim görevi vardır. Birçok yönden, SQL Server’ı tam olarak şirket içi SQL Server örneğindeki gibi yapılandırır ve yönetirsiniz. Ancak, bazı belirli tooAzure görevlerdir. Merhaba aşağıdaki bölümlerde bağlantılar toomore bilgi ile birlikte bu alanlardan bazıları vurgulayın.

### <a name="connect-toohello-vm"></a>Toohello VM Bağlan
Merhaba en temel yönetim adımları araçları, SQL Server Management Studio (SSMS) gibi aracılığıyla tooconnect tooyour SQL Server VM biridir. Yönergeler için nasıl yeni SQL Server VM tooconnect tooyour bkz [tooa Azure ile ilgili SQL Server sanal makinesine bağlanmak](virtual-machines-windows-sql-connect.md).

### <a name="migrate-your-data"></a>Verilerinizi geçirme
Varolan bir veritabanınız varsa, toomove isteyeceksiniz bu toohello yeni SQL VM sağlandı. Geçiş seçenekleri ve kılavuzların listesi için bkz: [veritabanı tooSQL bir Azure VM sunucuda geçiş](virtual-machines-windows-migrate-sql.md).

### <a name="configure-high-availability"></a>Yüksek kullanılabilirliği yapılandırma
Size yüksek kullanılabilirlik gerekiyorsa, SQL Server Kullanılabilirlik gruplarını yapılandırmayı dikkate alın. Bu, bir sanal ağda birden fazla Azure VM’yi içerir. Hello Azure portal bu yapılandırmayı sizin için ayarlayan bir şablona sahiptir. Daha fazla bilgi için bkz. [Azure Resource Manager sanal makinelerde AlwaysOn Kullanılabilirlik grubu yapılandırma](virtual-machines-windows-portal-sql-alwayson-availability-groups.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Kullanılabilirlik grubu ve ilgili dinleyiciyi istiyorsanız toomanually yapılandırma Bkz [Azure VM'de AlwaysOn Kullanılabilirlik Grupları Yapılandırma](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Diğer yüksek kullanılabilirlik dikkate alınacak noktaları için bkz. [Azure Virtual Machines’de SQL Server için Yüksek Kullanılabilirlik ve Olağanüstü Durum Kurtarma](virtual-machines-windows-sql-high-availability-dr.md).

### <a name="back-up-your-data"></a>Verilerinizi yedekleme
Azure VM'ler yararlanabilir [otomatik yedekleme](virtual-machines-windows-sql-automated-backup.md), hangi düzenli olarak veritabanı tooblob depolama yedeklerini oluşturur. Bu tekniği el ile de kullanabilirsiniz. Daha fazla bilgi için. bkz. [SQL Server Yedekleme ve Geri Yükleme için Azure Storage’ı Kullanma](virtual-machines-windows-use-storage-sql-server-backup-restore.md). Tüm yedekleme ve geri yükleme seçeneklerine genel bakış için bkz. [Azure Virtual Machines’de SQL Server için Yedekleme ve geri Yükleme](virtual-machines-windows-sql-backup-recovery.md).

### <a name="automate-updates"></a>Otomatik güncelleştirmeler
Azure VM'ler kullanabileceğiniz [otomatik düzeltme eki uygulama](virtual-machines-windows-sql-automated-patching.md) tooschedule önemli windows ve SQL Server yüklemek için bir bakım penceresi otomatik olarak güncelleştirir.

### <a name="customer-experience-improvement-program-ceip"></a>Müşteri deneyimini geliştirme programı (CEIP)
Merhaba Müşteri Deneyimi Geliştirme Programı (CEIP) varsayılan olarak etkindir. TooMicrosoft toohelp SQL Server'ın geliştirilmesine bu düzenli aralıklarla gönderir raporlar. CEIP ile toodisable istemediğiniz sürece gerekli yönetim görev yok sağlama sonra. Uzak Masaüstü'nü toohello VM bağlanarak hello CEIP devre dışı bırakın ya da özelleştirin. Merhaba çalıştırmak **SQL Server hata ve kullanım raporlama** yardımcı programı. Merhaba yönergeleri toodisable raporlama izleyin. 

Daha fazla bilgi için bkz: hello hello CEIP bölümüne [lisans koşullarını kabul](https://msdn.microsoft.com/library/ms143343.aspx) konu. 

## <a name="next-steps"></a>Sonraki adımlar

Fiyatlandırma hakkında sorular için bkz: [Kılavuzu SQL Server Azure VM'ler için fiyatlandırma](virtual-machines-windows-sql-server-pricing-guidance.md) ve hello [Azure fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Hedef sürümünüz SQL Server'ın hello seçin **işletim sistemi/yazılım** listesi. Daha sonra farklı boyutlu sanal makineler için hello fiyatları görüntüleyin.

Başka sorunuz mu var? İlk olarak, hello bkz [Azure sanal makineler ile ilgili SSS SQL Server'da](virtual-machines-windows-sql-server-iaas-faq.md). Ancak ayrıca herhangi bir SQL VM konuları toointeract, soru veya yorum toohello alt Microsoft ve hello toplulukla ekleyin.
