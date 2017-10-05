---
title: "Azure SQL Database hizmet ve performans katmanları | Microsoft Docs"
description: "SQL esnek havuzu tanıtır ve SQL Database hizmet katmanları ve performans düzeyleri tek veritabanları için karşılaştırması"
keywords: "veritabanı seçenekleri,veritabanı performansı"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: f5c5c596-cd1e-451f-92a7-b70d4916e974
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: b25ff5331f119efd44c61808f7d1d5decb226bd6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="what-performance-options-are-available-for-an-azure-sql-database"></a>Hangi performans seçenekleri bir Azure SQL veritabanı için kullanılabilir

[Azure SQL veritabanı](sql-database-technical-overview.md) hem tek dört hizmet katmanları sunar ve [havuza alınmış](sql-database-elastic-pool.md) veritabanları. Bu hizmet katmanlarıdır: **temel**, **standart**, **Premium**, ve **Premium RS**. Her bir hizmet katmanına içinde birden çok performans düzeyleri olan ([Dtu'lar](sql-database-what-is-a-dtu.md)) ve farklı iş yükleri ve veri boyutlarını işlemek için Depolama Seçenekleri. Daha yüksek performans düzeyleri giderek daha yüksek verimlilik ve kapasite sağlamak üzere tasarlanmış ek işlem ve depolama kaynaklarını sağlar. Hizmet katmanları, performans düzeyleri ve depolama kapalı kalma süresi olmadan dinamik olarak değiştirebilirsiniz. 
- **Temel**, **standart** ve **Premium** hizmet katmanları tüm çalışma süresi SLA %99.99, esnek iş sürekliliği seçenekleri, güvenlik özellikleri ve saatlik faturalandırma sahip. 
- **Premium RS** katmanı, diğer hizmet katmanları veritabanında'den daha düşük bir sayı yedek kopyaları ile çalıştığı için Premium katmanı azaltılmış SLA ile performans düzeylerinin aynısını sağlar. Bu nedenle, bir hizmet hatası durumunda 5 dakikalık gecikme kadar bir yedekten veritabanınızı kurtarmanız gerekebilir.

> [!IMPORTANT]
> Bir Azure SQL veritabanı garantili bir kaynak kümesini alır ve Azure içinde herhangi bir veritabanı, veritabanınızı beklenen performans özellikleri etkilenmez. 

## <a name="choosing-a-service-tier"></a>Hizmet katmanı seçme
Aşağıdaki tabloda farklı uygulama iş yükleri için en uygun katman örnekleri verilmiştir.

| Hizmet katmanı | Hedef iş yükleri |
| :--- | --- |
| **Temel** | Genellikle belirli bir zamanda tek bir işlemin etkin olmasını destekler ve küçük veritabanları için uygundur. Geliştirme veya test amaçlı kullanılan veritabanları ya da küçük ölçekli ve az sıklıkta kullanılan uygulamalar örnek olarak verilebilir. |
| **Standart** |Birden çok eşzamanlı sorguyu destekleyen ve G/Ç performansı gereksinimleri düşük veya orta olan bulut uygulamaları için en uygun seçenektir. Çalışma grupları ve web uygulamaları örnek olarak verilebilir. |
| **Premium** | Çok sayıda eşzamanlı kullanıcıyı destekleyen ve G/Ç performansı gereksinimleri yüksek olan, yüksek işlem hacimleri için tasarlanmıştır. İş açısından önemli uygulamaları destekleyen veritabanları örnek olarak verilebilir. |
| **Premium RS** | Yüksek oranda kullanılabilirliğini garanti gerektirmeyen g/ç yoğun iş yükleri için tasarlanmıştır. Örnekler, yüksek performanslı iş yükleri veya veritabanı kaydının sistem olduğu analitik bir iş yükü test edilmesini içerir. |
|||

Belirli bir anda bir hizmet katmanı içinde ayrılmış kaynaklarla tek veritabanları oluşturabilirsiniz [performans düzeyi](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) veya içinde veritabanları oluşturabilirsiniz bir [SQL esnek havuzu](sql-database-service-tiers.md#elastic-pool-service-tiers-and-performance-in-edtus). SQL esnek havuzu işlem ve depolama kaynaklarını tek bir mantıksal sunucu içinde birden çok veritabanı arasında paylaşılır. 

Tek veritabanları için kullanılabilir kaynakları veritabanı işlem birimleri (Dtu'lar) cinsinden ifade edilir ve kaynakları SQL esnek havuzlar için esnek veritabanı işlem birimleri (Edtu'lar) cinsinden ifade edilir. Dtu ve Edtu hakkında daha fazla bilgi için bkz: [Dtu ve Edtu nelerdir?](sql-database-what-is-a-dtu.md).

Bir hizmet katmanına karar vermek için, ihtiyacınızı olan en düşük veritabanı özelliklerini belirleyerek başlayın:

| **Hizmet katmanı özellikleri** | **Temel** | **Standart** | **Premium** | **Premium RS**|
| :-- | --: | --: | --: | --: |
| En büyük tek veritabanı boyutu | 2 GB | 250 GB | 4 TB *  | 500 GB  |
| En fazla esnek havuz boyutu | 156 GB | 2,9 TB | 4 TB * | 750 GB |
| Esnek havuzdaki en büyük veritabanı boyutu | 2 GB | 250 GB | 500 GB | 500 GB |
| Veritabanı havuz başına maksimum sayısı | 500  | 500 | 100 | 100 |
| En fazla tek veritabanı Dtu'lar | 5 | 100 | 4000 | 1000 |
| Esnek havuzdaki veritabanı başına maksimum Dtu | 5 | 3000 | 4000 | 1000 |
| Veritabanı yedekleme bekletme süresi | 7 gün | 35 gün | 35 gün | 35 gün |
||||||

> [!IMPORTANT]
> Depolama en fazla 4 TB kullanılabilir şu anda aşağıdaki bölgelerde: BİZE East2, Batı ABD, BİZE kamu Virginia, Batı Avrupa, Orta Almanya, Güney Doğu Asya, Japonya Doğu, Avustralya Doğu, Kanada merkezi ve Doğu Kanada. Bkz: [geçerli 4 TB sınırlamaları](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize)
>

Uygun hizmet katmanını belirledikten sonra performans düzeyi (Dtu'lar sayısı) ve veritabanı için depolama miktarını belirlemek hazırsınız. 

- S2 ve S3 performans düzeyleri **standart** katmanı olan genellikle iyi bir başlangıç noktası. 
- Yüksek CPU veya g/ç gereksinimleri olan veritabanları için performans düzeyleri içinde **Premium** katmanı olan sağındaki başlangıç noktası. 
- **Premium** katmanı daha fazla CPU sunar ve yüksek performans karşılaştırıldığında daha fazla g/ç x 10 düzeyde başlar **standart** katmanı.
- **PremiumRS** katmanı sunuyor performansını **Premium** katmanı daha düşük maliyetle ancak azaltılmış SLA ile.

> [!IMPORTANT]
> Gözden geçirme [SQL esnek havuzu](sql-database-elastic-pool.md) veritabanları işlem ve depolama kaynakları paylaşmak için SQL esnek havuzu halinde gruplandırmayı hakkında ayrıntılı bilgi için konu. Hizmet katmanları ve performans düzeyleri tek veritabanları için bu konunun geri kalanında odaklanır.
>

## <a name="single-database-service-tiers-and-performance-levels"></a>Tek veritabanı hizmet katmanları ve performans düzeyleri
Tek veritabanları için birden çok performans düzeyleri ve her bir hizmet katmanına içinde depolama tutarlar vardır. 

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

## <a name="scaling-up-or-scaling-down-a-single-database"></a>Tek veritabanının ölçeğini artırma veya azaltma

Başlangıçta bir hizmet katmanı ve performans düzeyi seçtikten sonra, gerçek deneyime bağlı olarak tek veritabanının ölçeğini dinamik olarak artırıp azaltabilirsiniz.  

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-dynamically-scale-up-or-scale-down/player]
>

Bir veritabanının hizmet katmanının ve/veya performansının değiştirilmesi, özgün veritabanının yeni performans düzeyinde bir çoğaltmasını oluşturur ve ardından bağlantıları bu çoğaltmaya geçirir. Bu işlem sırasında veri kaybı olmaz, ancak çoğaltmaya geçişin gerçekleştiği kısa süre zarfında veritabanıyla bağlantılar devre dışı bırakılır, bu nedenle uçuştaki bazı işlemler geri alınabilir. Anahtar süreyi değişir, ancak genellikle altında 4 saniyeden 30 saniyeden zamanın % 99 olmasıdır. Varsa büyük sayılar şu anda bağlantıları, yürütülen işlemler devre dışı bırakıldı, anahtar süreyi daha uzun olabilir.  

Tüm ölçek artırma işleminin süresi hem veritabanı boyutuna hem de değişiklikten önceki ve sonraki hizmet katmanına bağlı olarak değişir. Örneğin, Standart hizmet katmanına, Standart hizmet katmanından veya Standart hizmet katmanında değiştirilen 250 GB’lik bir veritabanı 6 saatte tamamlanır. Premium hizmet katmanında performans düzeylerini değiştiren aynı boyuttaki bir veritabanı için bu işlem 3 saat içinde tamamlanır.

> [!TIP]
> Ölçeklendirme işlemi devam eden bir SQL veritabanı durumunu denetlemek için aşağıdaki sorguyu kullanabilirsiniz: ```select * from sys.dm_operation_status```.
>

* Daha yüksek bir hizmet katmanı veya performans düzeyini yükseltme yapıyorsanız, daha büyük bir maksimum boyutu açıkça belirtmediğiniz sürece en fazla veritabanı boyutunu artırmaz.
* Bir veritabanı düşürmek için veritabanı hedef hizmet katmanı maksimum izin verilen boyutundan daha küçük olmalıdır. 
* Bir veritabanıyla yükseltirken [coğrafi çoğaltma](sql-database-geo-replication-portal.md) etkinse, onun ikincil veritabanları için istediğiniz performans katmanı birincil veritabanı (genel rehberlik) yükseltmeden önce yükseltin. İkincil veritabanını ilk farklı edition ugrading için yükseltirken gereklidir. 
* Bir veritabanını önceki sürüme indirme zaman [coğrafi çoğaltma](sql-database-geo-replication-portal.md) istediğiniz performans katmanına birincil veritabanlarını ikincil veritabanı (genel rehberlik) eski sürüme düşürmeyi önce düşürmek etkin. İlk birincil veritabanı eski sürüme düşürmeyi farklı bir sürüme eski sürüme düşürmeyi gerekli olduğunda. 

* Geri yükleme hizmeti teklifleri, çeşitli hizmet katmanları için farklılık gösterir. İçin olana varsa **temel** katmanı, daha düşük bir yedekleme Bekletme dönemi - bkz olacaktır [Azure SQL veritabanı yedeklemeleri](sql-database-automated-backups.md).
* Veritabanının yeni özellikleri, değişiklikler tamamlanana kadar uygulanmaz.


## <a name="current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize"></a>4 TB maxsize P11 ve P15 veritabanlarıyla geçerli sınırlamaları

4 TB P11 ve P15 veritabanı için bir maksimum boyut (daha önce açıklandığı gibi) bazı bölgelerde desteklenir. 4 TB maxsize P11 ve P15 veritabanlarıyla için aşağıdaki konuları ve sınırlamalar uygulanır:

- (4 TB veya 4096 GB değeri kullanarak) bir veritabanı oluşturulurken 4 TB maxsize seçeneği seçerseniz, veritabanı desteklenmeyen bir bölgede sağlandığında Oluştur komutu bir hata ile başarısız olur.
- Desteklenen bölgeleri birinde bulunan mevcut P11 ve P15 veritabanları için 4 TB maxsize depoya artırabilir. Bu kullanılarak denetlenebilir [seçin DATABASEPROPERTYEX](https://msdn.microsoft.com/library/ms186823.aspx) veya Azure portalında veritabanı boyutu inceleniyor. Varolan P11 veya P15 yükseltme veritabanı yalnızca sunucu düzeyinde asıl oturum açma veya dbmanager veritabanı rolünün üyeleri tarafından gerçekleştirilebilir. 
- Bir yükseltme işlemi desteklenen bir bölgede yürütülürse yapılandırma anında güncelleştirilir. Veritabanı yükseltme işlemi sırasında çevrimiçi kalır. Ancak, gerçek veritabanı dosyaları için yeni maxsize yükseltilene kadar tam 4 TB depolama alanını olamaz. Gereken süreyi yükseltilen veritabanı boyutuna bağlıdır.  
- Oluşturma veya güncelleştirme P11 veya P15 bir veritabanı, yalnızca 4 TB maxsize ve 1 TB arasında seçim yapabilirsiniz. Ara depolama boyutları şu anda desteklenmemektedir. P11/P15 oluştururken, varsayılan depolama 1 TB'lık önceden seçilmiş seçeneğidir. Desteklenen bölgeleri birinde bulunan veritabanları için yeni veya varolan bir tek veritabanı için depolama en fazla 4 TB için artırabilir. Diğer tüm bölgeler için 1 TB en büyük boyut yükseltilemez. 4 TB dahil depolama seçtiğinizde fiyat değiştirmez.
- 1 TB kullanılan depolamanın olsa bile, 4 TB veritabanı maxsize 1 TB'ye kadar değiştirilemez. Bu nedenle, bir P11 - 4 TB/P15 - 4 TB bir P11 - 1 TB/P15 - 1 TB veya daha düşük bir performans katmanı P1 P6 için örneğin, düşürülemiyor) biz performans katmanı geri kalanı için ek depolama seçenekleri sağlayarak kadar. Bu kısıtlama noktası zamanında dahil olmak üzere kopyalama senaryoları ve geri yükleme için de geçerlidir coğrafi geri yükleme, uzun-süreli yedekleme-saklama ve veritabanı kopyası. Bir veritabanı 4 TB seçeneğiyle yapılandırıldıktan sonra bu veritabanının tüm geri yükleme işlemleri P11/P15 4 TB maxsize ile çalıştırılması gerekir.
- Oluşturma veya desteklenmeyen bir bölgede bir P11/P15 veritabanı yükseltme, create veya yükseltme işlemi başarısız olursa şu hata iletisiyle: **BİZE East2, Batı ABD, BİZE kamu Virginia, Batı P11 ve P15 veritabanı en fazla 4 TB depolama ile kullanılabilir Avrupa, Orta Almanya, Güneydoğu Asya, Japonya Doğu, Avustralya Doğu, Orta Kanada ve Doğu Kanada.**
- Aktif coğrafi çoğaltma senaryoları için:
   - Bu ilişki bir coğrafi çoğaltma ilişkisi ayarlanırken: birincil veritabanı P11 veya P15 ise, secondary(ies) de P11 veya P15; olması gerekir 4 TB destekleme kapasitesine sahip olmadığından, düşük performans katmanı ikincil kopya reddedilir.
   - Coğrafi çoğaltma ilişkisinde birincil veritabanı yükseltme: maxsize 4 TB birincil veritabanında değiştirme ikincil veritabanını aynı değişiminde tetikler. Her iki yükseltmeyi değişikliğin etkili olması için birincil başarılı olması gerekir. 4TB seçeneği için bölge sınırlamalar (yukarıya bakın) uygulanır. İkincil 4 TB desteklemeyen bir bölgede ise, birincil yükseltilmez.
- P11 - 4 TB/P15 - 4 TB veritabanları yüklenmesi için içeri/dışarı aktarma hizmeti kullanma desteklenmiyor. SqlPackage.exe için kullanmak [alma](sql-database-import.md) ve [verme](sql-database-export.md) veri.

## <a name="manage-single-database-service-tiers-and-performance-levels-using-the-azure-portal"></a>Tek veritabanı hizmet katmanları ve performans düzeyleri Azure Portalı'nı kullanarak yönetme

Ayarlayın veya hizmet katmanı, performans düzeyi ya da Azure Portalı'nı kullanarak yeni veya mevcut bir Azure SQL veritabanı için depolama miktarını değiştirmek için açın **performansını yapılandırın** tıklatarak veritabanınız için pencere **fiyatlandırma Katmanı ( Dtu'lar ölçeklendirme)** - aşağıdaki ekran görüntüsünde gösterildiği gibi. 

- Ayarlayabilir veya iş yükü hizmet katmanı seçerek Hizmet katmanını değiştirebilirsiniz. 
- Ayarlama veya performans düzeyini değiştirme (**Dtu'lar**) kullanarak bir hizmet katmanı içinde **DTU** kaydırıcı.
- Ayarlama veya değiştirme performans düzeyi kullanan bir depolama miktarına **depolama** kaydırıcı. 

  ![Hizmet katmanını ve performans düzeyini yapılandırın](./media/sql-database-service-tiers/service-tier-performance-level.png)

> [!IMPORTANT]
> Gözden geçirme [4 TB maxsize P11 ve P15 veritabanlarıyla geçerli sınırlamalar](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize) P11 veya P15 bir hizmet katmanı seçerken.
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-powershell"></a>Tek veritabanı hizmet katmanları ve performans düzeyleri PowerShell kullanarak yönetme

Azure SQL veritabanı hizmet katmanları, performans düzeyleri ve PowerShell kullanarak depolama miktarını ayarlama veya değiştirme için aşağıdaki PowerShell cmdlet'lerini kullanın. Gerekirse yükleyin veya PowerShell yükseltme, bakın [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps). 

| Cmdlet | Açıklama |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Bir veritabanı oluşturur |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Bir veya daha fazla veritabanı alır|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Bir veritabanı özelliklerini ayarlar ya da varolan bir veritabanını bir esnek havuza taşır|


> [!TIP]
> Bir veritabanı performans ölçümlerini izler bir PowerShell örnek betiği daha yüksek bir performans düzeyine ölçeklendirir ve performans ölçümleri birinde bir uyarı kuralı oluşturur bkz [İzleyici ve ölçek tek bir SQL veritabanı PowerShellkullanma](scripts/sql-database-monitor-and-scale-database-powershell.md).

## <a name="manage-single-database-service-tiers-and-performance-levels-using-the-azure-cli"></a>Tek veritabanı hizmet katmanları ve performans düzeyleri Azure CLI kullanarak yönetme

Ayarlamak veya Azure SQL veritabanlarını değiştirmek için aşağıdaki hizmet katmanları ve performans düzeyleri Azure CLI kullanarak bir depolama miktarını kullanın [Azure CLI SQL veritabanı](/cli/azure/sql/db) komutları. CLI’yi tarayıcınızda çalıştırmak için [Cloud Shell](/azure/cloud-shell/overview) kullanın veya macOS, Linux ya da Windows’da [yükleyin](/cli/azure/install-azure-cli). Oluşturma ve SQL esnek havuzlarını yönetmek için bkz: [esnek havuzlar](sql-database-elastic-pool.md).

| Cmdlet | Açıklama |
| --- | --- |
|[az sql db oluştur](/cli/azure/sql/db#create) |Bir veritabanı oluşturur|
|[az sql db listesi](/cli/azure/sql/db#list)|Veritabanları ve tüm veri ambarlarında bir sunucu veya esnek havuzdaki tüm veritabanları listeler.|
|[az sql db listesi-sürümleri](/cli/azure/sql/db#list-editions)|Listeleri kullanılabilir hizmet hedefleri ve depolama sınırları|
|[az sql db listesi-kullanımları](/cli/azure/sql/db#list-usages)|Kullanımları döndürür veritabanı|
|[az sql db Göster](/cli/azure/sql/db#show)|Bir veritabanı veya veri ambarı alır|
|[az sql db güncelleştirme](/cli/azure/sql/db#update)|Bir veritabanını güncelleştirir|

> [!TIP]
> Veritabanının boyutu bilgileri sorgulama sonra farklı performans düzeyi tek bir Azure SQL veritabanına ölçeklendirilebilen bir Azure CLI örnek komut dosyası için bkz: [kullanımı izlemek ve tek bir SQL veritabanı ölçeklendirmek için CLI](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-transact-sql"></a>Tek veritabanı hizmet katmanları ve performans düzeyleri Transact-SQL kullanarak yönetme

Azure SQL veritabanı hizmet katmanları, performans düzeyleri ve Transact-SQL ile depolama miktarını ayarlama veya değiştirme için aşağıdaki T-SQL komutlarını kullanın. Azure portalını kullanarak bu komutlar gönderebilirsiniz [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), veya bir Azure SQL veritabanı sunucusuna bağlanın ve Transact-SQL geçirmek başka bir programı komutları. 

| Komut | Açıklama |
| --- | --- |
|[Veritabanı (Azure SQL veritabanı) oluşturma](/sql/t-sql/statements/create-database-azure-sql-database)|Yeni bir veritabanı oluşturur. Yeni bir veritabanı oluşturmak için ana veritabanına bağlanması gerekir.|
| [ALTER DATABASE (Azure SQL veritabanı)](/sql/t-sql/statements/alter-database-azure-sql-database) |Bir Azure SQL veritabanı değiştirir. |
|[sys.database_service_objectives (Azure SQL veritabanı)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Edition (hizmet katmanı), hizmet hedefi (fiyatlandırma katmanı) ve esnek havuz adı, varsa Azure SQL veritabanına veya Azure SQL Data Warehouse için döndürür. Azure SQL Database sunucusu ana veritabanında oturum açtıysanız, bilgiler tüm veritabanlarını döndürür. Azure SQL Data Warehouse için ana veritabanına bağlı olmalıdır.|
|[sys.database_usage (Azure SQL veritabanı)](/sql/relational-databases/system-catalog-views/sys-database-usage-azure-sql-database)|Sayısı, türü ve süresi bir Azure SQL veritabanı sunucusu üzerindeki veritabanlarının listeler.|

Aşağıdaki örnek, maxsize gösterir ALTER DATABASE komutunu kullanarak değiştiriliyor:

 ```sql
ALTER DATABASE <myDatabaseName> 
   MODIFY (MAXSIZE = 4096 GB);
```

## <a name="manage-single-databases-using-the-rest-api"></a>REST API kullanarak tek veritabanlarını yönetme

Azure SQL veritabanı hizmet katmanları, performans düzeyleri ve REST API kullanarak depolama miktarını ayarlama veya değiştirme için bkz: [Azure SQL Database REST API'sini](/rest/api/sql/).

## <a name="next-steps"></a>Sonraki adımlar

* Daha fazla bilgi edinmek [Dtu'lar](sql-database-what-is-a-dtu.md).
* DTU kullanımı izleme hakkında bilgi edinmek için [izleme ve performans ayarlama](sql-database-troubleshoot-performance.md).

