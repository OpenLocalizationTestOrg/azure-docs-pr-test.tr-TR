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
ms.openlocfilehash: b27b78788614d32e6c0c4267fe0ce504ebd2f444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-performance-options-are-available-for-an-azure-sql-database"></a>Hangi performans seçenekleri bir Azure SQL veritabanı için kullanılabilir

[Azure SQL veritabanı](sql-database-technical-overview.md) hem tek dört hizmet katmanları sunar ve [havuza alınmış](sql-database-elastic-pool.md) veritabanları. Bu hizmet katmanlarıdır: **temel**, **standart**, **Premium**, ve **Premium RS**. Her bir hizmet katmanına içinde birden çok performans düzeyleri olan ([Dtu'lar](sql-database-what-is-a-dtu.md)) ve depolama seçenekleri toohandle farklı iş yükleri ve veri boyutları. Depolama kaynaklarını toodeliver giderek daha yüksek performans ve kapasite tasarlanmış ve ek işlem daha yüksek performans düzeyleri sağlar. Hizmet katmanları, performans düzeyleri ve depolama kapalı kalma süresi olmadan dinamik olarak değiştirebilirsiniz. 
- **Temel**, **standart** ve **Premium** hizmet katmanları tüm çalışma süresi SLA %99.99, esnek iş sürekliliği seçenekleri, güvenlik özellikleri ve saatlik faturalandırma sahip. 
- Merhaba **Premium RS** katmanı hello Premium katmanı azaltılmış SLA ile bir veritabanında'den daha düşük bir sayı yedek kopyaları ile çalıştığı için hello gibi diğer hizmet katmanları bu hello aynı performans düzeyleri sağlar. Bu nedenle, bir hizmet hatası hello olayda bir yedeklemeyi ile tooa 5 dakikalık gecikme veritabanınızdan toorecover gerekebilir.

> [!IMPORTANT]
> Azure SQL veritabanını garantili bir kaynak kümesini alır ve Azure içinde herhangi bir veritabanı, veritabanı performans özellikleri etkilenmez hello bekleniyor. 

## <a name="choosing-a-service-tier"></a>Hizmet katmanı seçme
Merhaba aşağıdaki tabloda farklı uygulama iş yükleri için uygun hello katmanları en iyi örnekleri sağlar.

| Hizmet katmanı | Hedef iş yükleri |
| :--- | --- |
| **Temel** | Genellikle belirli bir zamanda tek bir işlemin etkin olmasını destekler ve küçük veritabanları için uygundur. Geliştirme veya test amaçlı kullanılan veritabanları ya da küçük ölçekli ve az sıklıkta kullanılan uygulamalar örnek olarak verilebilir. |
| **Standart** |Merhaba Git-toooption birden çok eşzamanlı sorguyu destekler, düşük toomedium g/ç performans gereksinimleri olan bulut uygulamaları için. Çalışma grupları ve web uygulamaları örnek olarak verilebilir. |
| **Premium** | Çok sayıda eşzamanlı kullanıcıyı destekleyen ve G/Ç performansı gereksinimleri yüksek olan, yüksek işlem hacimleri için tasarlanmıştır. İş açısından önemli uygulamaları destekleyen veritabanları örnek olarak verilebilir. |
| **Premium RS** | Merhaba yüksek kullanılabilirlik garantilerinden gerektirmeyen g/ç yoğun iş yükleri için tasarlanmıştır. Örnekler, yüksek performanslı iş yükleri veya hello veritabanı kaydının hello sistem olduğu analitik bir iş yükü test edilmesini içerir. |
|||

Belirli bir anda bir hizmet katmanı içinde ayrılmış kaynaklarla tek veritabanları oluşturabilirsiniz [performans düzeyi](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) veya içinde veritabanları oluşturabilirsiniz bir [SQL esnek havuzu](sql-database-service-tiers.md#elastic-pool-service-tiers-and-performance-in-edtus). SQL esnek havuzu hello işlem ve depolama kaynaklarını tek bir mantıksal sunucu içinde birden çok veritabanı arasında paylaşılır. 

Tek veritabanları için kullanılabilir kaynakları veritabanı işlem birimleri (Dtu'lar) cinsinden ifade edilir ve kaynakları SQL esnek havuzlar için esnek veritabanı işlem birimleri (Edtu'lar) cinsinden ifade edilir. Dtu ve Edtu hakkında daha fazla bilgi için bkz: [Dtu ve Edtu nelerdir?](sql-database-what-is-a-dtu.md).

toodecide bir hizmet katmanına ihtiyacınız hello minimum veritabanı özellikleri belirleyerek başlayın:

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
> Too4 TB depolama bölgeleri aşağıdaki hello şu anda kullanılabilir: BİZE East2, Batı ABD, BİZE kamu Virginia, Batı Avrupa, Orta Almanya, Güney Doğu Asya, Japonya Doğu, Avustralya Doğu, Kanada merkezi ve Doğu Kanada. Bkz: [geçerli 4 TB sınırlamaları](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize)
>

Merhaba uygun hizmet katmanı belirledikten sonra hazır toodetermine hello performans düzeyi (Dtu'lar hello sayısı) ve hello depolama miktarına hello veritabanı için demektir. 

- Merhaba hello S2 ve S3 performans düzeyleri **standart** katmanı olan genellikle iyi bir başlangıç noktası. 
- Yüksek CPU veya g/ç gereksinimleri olan veritabanları için performans düzeyleri hello içinde hello **Premium** katmanı olan hello sağ başlangıç noktası. 
- Merhaba **Premium** katmanı sunuyor daha fazla CPU ve daha fazla GÇ x 10 başlar karşılaştırıldığında toohello en yüksek performans düzeyi hello içinde **standart** katmanı.
- Merhaba **PremiumRS** katmanı sunuyor hello hello performansını **Premium** katmanı daha düşük maliyetle ancak azaltılmış SLA ile.

> [!IMPORTANT]
> Gözden geçirme hello [SQL esnek havuzu](sql-database-elastic-pool.md) SQL esnek veritabanları gruplandırma hakkında hello Ayrıntılar için konu havuzları tooshare işlem ve depolama kaynaklarını. Hizmet katmanları ve performans düzeyleri tek veritabanları için bu konunun geri kalanı Hello odaklanır.
>

## <a name="single-database-service-tiers-and-performance-levels"></a>Tek veritabanı hizmet katmanları ve performans düzeyleri
Tek veritabanları için birden çok performans düzeyleri ve her bir hizmet katmanına içinde depolama tutarlar vardır. 

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

## <a name="scaling-up-or-scaling-down-a-single-database"></a>Tek veritabanının ölçeğini artırma veya azaltma

Başlangıçta bir hizmet katmanı ve performans düzeyi seçtikten sonra, gerçek deneyime bağlı olarak tek veritabanının ölçeğini dinamik olarak artırıp azaltabilirsiniz.  

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-dynamically-scale-up-or-scale-down/player]
>

Bir veritabanının Hello hizmet katmanı ve/veya performans düzeyini değiştirme hello yeni performans düzeyinde hello özgün veritabanının bir kopyasını oluşturur ve toohello çoğaltma bağlantıları geçiş yapar. Bu işlem sırasında veri kaybı olmamasına ancak biz toohello çoğaltma üzerinde ne zaman geçiş hello kısa süre sırasında bağlantıları toohello veritabanı devre dışı bırakıldı, yürütülen bazı işlemler geri alınamaz böylece. Merhaba süreyi hello anahtar için değişir, ancak genellikle altında 4 saniyeden 30 saniyeden başlangıç saati % 99 olmasıdır. Çok sayıda varsa hello şu anda bağlantıları, yürütülen işlemler devre dışı bırakılır, hello hello anahtar için süre uzun olabilir.  

Merhaba tüm büyütme işleminin Hello süresi iki hello boyutuna bağlıdır ve Hizmet katmanını hello veritabanı önce ve hello değiştirdikten sonra. Örneğin, Standart hizmet katmanına, Standart hizmet katmanından veya Standart hizmet katmanında değiştirilen 250 GB’lik bir veritabanı 6 saatte tamamlanır. Merhaba bir veritabanı için aynı diğer bir deyişle değişen performans düzeyleri boyut hello Premium Hizmet katmanını içinde 3 saat içinde tamamlamanız gerekir.

> [!TIP]
> toocheck hello durumunu ölçeklendirme işlemi devam eden bir SQL veritabanı'nın sorgu aşağıdaki hello kullanabilirsiniz: ```select * from sys.dm_operation_status```.
>

* Tooa daha yüksek hizmet katmanı veya performans düzeyini yükseltme yapıyorsanız, daha büyük bir maksimum boyutu açıkça belirtmediğiniz sürece hello en fazla veritabanı boyutunu artırmaz.
* bir veritabanı toodowngrade, hello veritabanı hello izin verilen maksimum boyut hello hedef hizmet katmanının küçük olması gerekir. 
* Bir veritabanıyla yükseltirken [coğrafi çoğaltma](sql-database-geo-replication-portal.md) etkinse, kendi ikincil veritabanları toohello istediğiniz performans katmanı hello birincil veritabanı (genel rehberlik) yükseltmeden önce yükseltin. Edition ugrading hello ikincil veritabanı ilk tooa farklı yükseltirken gereklidir. 
* Bir veritabanını önceki sürüme indirme zaman [coğrafi çoğaltma](sql-database-geo-replication-portal.md) kendi birincil veritabanları toohello istediğiniz performans katmanı hello ikincil veritabanı (genel rehberlik) eski sürüme düşürmeyi önce düşürmek etkin. Tooa farklı eski sürüme düşürmeyi edition eski sürüme düşürmeyi hello birincil veritabanı ilk gereklidir. 

* Merhaba geri yükleme hizmet teklifleri için farklı çeşitli hizmet katmanları hello. Toohello eski sürüme düşürmeyi varsa **temel** katmanı, daha düşük bir yedekleme Bekletme dönemi - bkz olacaktır [Azure SQL veritabanı yedeklemeleri](sql-database-automated-backups.md).
* Merhaba değişiklikler tamamlanana kadar hello veritabanı için yeni özellikler hello uygulanmaz.


## <a name="current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize"></a>4 TB maxsize P11 ve P15 veritabanlarıyla geçerli sınırlamaları

4 TB P11 ve P15 veritabanı için bir maksimum boyut (daha önce açıklandığı gibi) bazı bölgelerde desteklenir. Merhaba aşağıdaki konuları ve sınırlamalar tooP11 ve 4 TB maxsize P15 veritabanlarıyla uygulanır:

- (4 TB veya 4096 GB değeri kullanarak) bir veritabanı oluşturulurken hello 4 TB maxsize seçeneği belirlerseniz, hello oluşturursanız komutu başarısız bir hata ile Merhaba veritabanı desteklenmeyen bir bölgede sağlanır.
- Merhaba desteklenen bölgeler birinde bulunan P11 ve P15 veritabanlarında hello maxsize depolama too4 TB artırabilir. Bu hello kullanılarak denetlenebilir [seçin DATABASEPROPERTYEX](https://msdn.microsoft.com/library/ms186823.aspx) veya hello Azure portal hello veritabanı boyutunu inceleniyor. Varolan P11 veya P15 yükseltme veritabanı yalnızca sunucu düzeyinde asıl oturum açma veya hello dbmanager veritabanı rolünün üyeleri tarafından gerçekleştirilebilir. 
- Bir yükseltme işlemi yürütülürse desteklenen bölge hello yapılandırma hemen güncelleştirilir. Merhaba veritabanı hello yükseltme işlemi sırasında çevrimiçi kalır. Ancak, tam hello kullanan olamaz 4 TB hello gerçek veritabanı dosyalarını kadar depolama alanı toohello yeni maxsize yükseltildi. Merhaba gereken süre uzunluğunu hello yükseltilen hello veritabanı boyutuna bağlıdır.  
- Oluşturma veya güncelleştirme P11 veya P15 bir veritabanı, yalnızca 4 TB maxsize ve 1 TB arasında seçim yapabilirsiniz. Ara depolama boyutları şu anda desteklenmemektedir. P11/P15 oluştururken, 1 TB'lık hello varsayılan depolama seçeneği önceden seçilmiş. Merhaba desteklenen bölgeler birinde bulunan veritabanları için yeni veya varolan bir tek veritabanı için hello depolama maksimum too4TB artırabilir. Diğer tüm bölgeler için 1 TB en büyük boyut yükseltilemez. 4 TB dahil depolama seçtiğinizde hello fiyat değiştirmez.
- 1 TB kullanılan hello depolamanın olsa bile, hello 4 TB veritabanı maxsize değiştirilen too1 TB olamaz. Bu nedenle, P11 - 4 TB/P15 - 4 TB tooa P11 - 1 TB/P15 - 1 TB veya daha düşük bir performans katmanı Örneğin, tooP1 P6 indirgeyemezsiniz) kadar hello hello geri kalanı için ek depolama seçenekleri performans katmanı sağlanmaktadır. Bu kısıtlama toohello geri yükleme ve kopyalama senaryoları noktası zamanında dahil olmak üzere de geçerlidir coğrafi geri yükleme, uzun-süreli yedekleme-saklama ve veritabanı kopyası. Bir veritabanı hello 4 TB seçeneğiyle yapılandırıldıktan sonra bu veritabanının tüm geri yükleme işlemleri P11/P15 4 TB maxsize ile çalıştırılması gerekir.
- Oluşturma veya desteklenmeyen bir bölge P11/P15 veritabanında hello yükseltme oluşturmak veya yükseltme işlemi aşağıdaki hata iletisini hello ile başarısız olduğunda: **too4TB depolama yukarı P11 ve P15 veritabanı ile kullanılabilir BİZE East2, Batı ABD, BİZE kamu Virginia Batı Avrupa, Orta Almanya, Güneydoğu Asya, Japonya Doğu, Avustralya Doğu, Orta Kanada ve Doğu Kanada.**
- Aktif coğrafi çoğaltma senaryoları için:
   - Bu ilişki bir coğrafi çoğaltma ilişkisi ayarlanırken: hello birincil veritabanı P11 veya P15 ise, hello secondary(ies) de P11 veya P15; olması gerekir 4 TB destekleme kapasitesine sahip olmadığından, düşük performans katmanı ikincil kopya reddedilir.
   - Coğrafi çoğaltma ilişkisinde yükseltme hello birincil veritabanı: hello maxsize too4 TB birincil veritabanında değiştirme aynı değiştirme hello ikincil veritabanı üzerinde hello tetikler. Her iki yükseltmeyi hello birincil tootake etkisi hello değişiklik için başarılı olması gerekir. Merhaba 4TB seçeneği için bölge sınırlamaları (yukarıya bakın) uygulanır. Merhaba ikincil 4 TB desteklemeyen bir bölgede ise, birincil hello yükseltilmez.
- P11 - 4 TB/P15 - 4 TB veritabanları yüklenmesi için hello içeri/dışarı aktarma hizmeti kullanma desteklenmiyor. SqlPackage.exe çok kullanmak[alma](sql-database-import.md) ve [verme](sql-database-export.md) veri.

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-portal"></a>Tek veritabanı hizmet katmanları ve performans düzeyleri hello Azure portal kullanarak yönetme

tooset ya da değişiklik hello hizmet katmanı, performans düzeyine veya depolama miktarına hello Azure portal, açık hello kullanarak yeni veya mevcut bir Azure SQL veritabanı için **performansını yapılandırın** tıklatarak veritabanınız için pencere  **Fiyatlandırma Katmanı (Ölçek Dtu'lar)** - ekran görüntüsü aşağıdaki hello gösterildiği gibi. 

- Ayarlayabilir veya iş yükü hello hizmet katmanı seçerek hello Hizmet katmanını değiştirebilirsiniz. 
- Ayarlama veya değiştirme hello performans düzeyi (**Dtu'lar**) hello kullanarak bir hizmet katmanı içinde **DTU** kaydırıcı.
- Ayarlama veya değiştirme hello depolama miktarına hello kullanarak hello performans düzeyi için **depolama** kaydırıcı. 

  ![Hizmet katmanını ve performans düzeyini yapılandırın](./media/sql-database-service-tiers/service-tier-performance-level.png)

> [!IMPORTANT]
> Gözden geçirme [4 TB maxsize P11 ve P15 veritabanlarıyla geçerli sınırlamalar](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize) P11 veya P15 bir hizmet katmanı seçerken.
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-powershell"></a>Tek veritabanı hizmet katmanları ve performans düzeyleri PowerShell kullanarak yönetme

Azure SQL veritabanı hizmet katmanları tooset veya değiştirme, performans düzeyleri ve PowerShell kullanarak depolama miktarına PowerShell cmdlet'lerini aşağıdaki hello kullanın. PowerShell yükseltme veya tooinstall gerekir, bkz: [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps). 

| Cmdlet | Açıklama |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Bir veritabanı oluşturur |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Bir veya daha fazla veritabanı alır|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Bir veritabanı özelliklerini ayarlar ya da varolan bir veritabanını bir esnek havuza taşır|


> [!TIP]
> Bir veritabanının hello performans ölçümleri izler bir PowerShell örnek betiği tooa daha yüksek performans düzeyi ölçeklendirir ve hello performans ölçümleri, biri bir uyarı kuralı oluşturur bkz [İzleyici ve ölçek tek bir SQL veritabanı kullanma PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-cli"></a>Tek veritabanı hizmet katmanları ve performans düzeyleri hello Azure CLI kullanarak yönetme

Azure SQL veritabanı hizmet katmanları tooset veya değiştirme, performans düzeyleri ve depolama tutarı hello Azure CLI kullanarak kullanmak hello aşağıdaki [Azure CLI SQL veritabanı](/cli/azure/sql/db) komutları. Kullanım hello [bulut Kabuk](/azure/cloud-shell/overview) tarayıcınızda toorun hello CLI veya [yükleme](/cli/azure/install-azure-cli) macOS, Linux veya Windows üzerinde. Oluşturma ve SQL esnek havuzlarını yönetmek için bkz: [esnek havuzlar](sql-database-elastic-pool.md).

| Cmdlet | Açıklama |
| --- | --- |
|[az sql db oluştur](/cli/azure/sql/db#create) |Bir veritabanı oluşturur|
|[az sql db listesi](/cli/azure/sql/db#list)|Veritabanları ve tüm veri ambarlarında bir sunucu veya esnek havuzdaki tüm veritabanları listeler.|
|[az sql db listesi-sürümleri](/cli/azure/sql/db#list-editions)|Listeleri kullanılabilir hizmet hedefleri ve depolama sınırları|
|[az sql db listesi-kullanımları](/cli/azure/sql/db#list-usages)|Kullanımları döndürür veritabanı|
|[az sql db Göster](/cli/azure/sql/db#show)|Bir veritabanı veya veri ambarı alır|
|[az sql db güncelleştirme](/cli/azure/sql/db#update)|Bir veritabanını güncelleştirir|

> [!TIP]
> Hello boyutu bilgileri hello veritabanının sorgulama sonra tek bir Azure SQL veritabanı tooa farklı performans düzeyi ölçeklendirilebilen bir Azure CLI örnek komut dosyası için bkz: [kullanım CLI toomonitor ve ölçek tek bir SQL veritabanı](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-transact-sql"></a>Tek veritabanı hizmet katmanları ve performans düzeyleri Transact-SQL kullanarak yönetme

Azure SQL veritabanı hizmet katmanları tooset veya değiştirme, performans düzeyleri ve Transact-SQL ile depolama miktarını T-SQL komutlarıyla aşağıdaki hello kullanın. Hello Azure portal kullanarak bu komutlar gönderebilirsiniz [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), veya tooan Azure SQL veritabanı sunucusuna bağlanmak ve Transact-SQL geçirmek başka bir programı komutları. 

| Komut | Açıklama |
| --- | --- |
|[Veritabanı (Azure SQL veritabanı) oluşturma](/sql/t-sql/statements/create-database-azure-sql-database)|Yeni bir veritabanı oluşturur. Bağlı toohello ana veritabanı toocreate yeni bir veritabanı olmalıdır.|
| [ALTER DATABASE (Azure SQL veritabanı)](/sql/t-sql/statements/alter-database-azure-sql-database) |Bir Azure SQL veritabanı değiştirir. |
|[sys.database_service_objectives (Azure SQL veritabanı)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Döndürür edition (hizmet katmanı), hizmet hedefi (fiyatlandırma katmanı) ve esnek havuz adı, varsa Azure SQL veritabanına veya Azure SQL Data Warehouse için hello. Azure SQL Database sunucusu ana veritabanında toohello oturum açmış, bilgiler tüm veritabanlarını döndürür. Azure SQL Data Warehouse için bağlı toohello ana veritabanı olmalıdır.|
|[sys.database_usage (Azure SQL veritabanı)](/sql/relational-databases/system-catalog-views/sys-database-usage-azure-sql-database)|Merhaba sayısı, türü ve süresi bir Azure SQL veritabanı sunucusu üzerindeki veritabanlarının listeler.|

Merhaba aşağıdaki örnekte gösterilir hello maxsize hello ALTER DATABASE komutunu kullanarak değiştiriliyor:

 ```sql
ALTER DATABASE <myDatabaseName> 
   MODIFY (MAXSIZE = 4096 GB);
```

## <a name="manage-single-databases-using-hello-rest-api"></a>Tek veritabanlarını Hello REST API kullanarak yönetme

bkz: tooset ya da değişiklik Azure SQL veritabanı hizmet katmanları, performans düzeyleri ve depolama tutarı hello REST API kullanarak [Azure SQL Database REST API'sini](/rest/api/sql/).

## <a name="next-steps"></a>Sonraki adımlar

* Daha fazla bilgi edinmek [Dtu'lar](sql-database-what-is-a-dtu.md).
* DTU kullanımı izleme hakkında toolearn bkz [izleme ve performans ayarlama](sql-database-troubleshoot-performance.md).

