---
title: "aaaMigrate, var olan Azure veri ambarı toopremium depolama | Microsoft Docs"
description: "Varolan bir veri ambarı toopremium depolama geçirmek için yönergeler"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a>Veri ambarı toopremium deponuzda geçirme
En yeni Azure SQL Data Warehouse [büyük performans öngörülebilirlik için premium depolama][premium storage for greater performance predictability]. Mevcut veri ambarları şu anda standart depolama artık olabilir toopremium depolama geçişi. Otomatik geçiş yararlanabilir veya toocontrol tercih ederseniz, (hangi miktar kapalı kalma süresi içerir) toomigrate yapabileceğiniz geçiş kendiniz hello.

Birden fazla veri ambarı varsa, hello kullanın [otomatik geçiş zamanlama] [ automatic migration schedule] de geçirilecek zaman toodetermine.

## <a name="determine-storage-type"></a>Depolama türü belirlenemiyor
Veri ambarı tarihleri aşağıdaki hello önce oluşturduysanız, standart depolama kullanmakta olduğunuz.

| **Bölge** | **Bu tarihten önce oluşturulan veri ambarı** |
|:--- |:--- |
| Avustralya Doğu |Premium depolama henüz kullanılamıyor |
| Çin Doğu |1 Kasım 2016 |
| Çin Kuzey |1 Kasım 2016 |
| Almanya Orta |1 Kasım 2016 |
| Almanya Kuzeydoğu |1 Kasım 2016 |
| Hindistan Batı |Premium depolama henüz kullanılamıyor |
| Japonya Batı |Premium depolama henüz kullanılamıyor |
| Orta Kuzey ABD |10 Kasım 2016 |

## <a name="automatic-migration-details"></a>Otomatik geçiş ayrıntıları
Varsayılan olarak, biz veritabanınız için 6: 00'dan 6: 00'da, bölgenin yerel saat arasındaki hello sırasında geçiş yapacağınız [otomatik geçiş zamanlama][automatic migration schedule]. Mevcut veri ambarınız hello geçiş sırasında kullanılamaz. Merhaba geçiş veri ambarına terabayt depolama alanı başına yaklaşık bir saat sürer. Hello otomatik geçiş herhangi bir kısmının sırasında ücret alınmaz.

> [!NOTE]
> Merhaba geçiş tamamlandığında, veri Ambarınızı tekrar çevrimiçi ve kullanılabilir olacaktır.
>
>

Microsoft, aşağıdaki adımları toocomplete hello geçiş (Bu tüm katılımı yapmanıza gerek yoktur) hello sürüyor. Bu örnekte, var olan veri ambarınız standart depolama üzerinde şu anda "MyDW." adlı düşünün

1. Microsoft "MyDW" çok yeniden adlandırır "MyDW_DO_NOT_USE_ [zaman damgası]."
2. Microsoft duraklatır "MyDW_DO_NOT_USE_ [zaman damgası]." Bu süre boyunca, bir yedekleme gerçekleştirilir. Biz bu işlem sırasında herhangi bir sorunla karşılaşırsanız, birden çok duraklatır ve sürdürür görebilirsiniz.
3. Microsoft, "2. adımda alınan MyDW" premium depolama hello yedekten adlı yeni bir veri ambarını oluşturur. Merhaba geri yükleme tamamlandıktan sonra "MyDW" kadar görünmez.
4. Merhaba geri yükleme tamamlandıktan sonra "MyDW" aynı veri ambarı birimlerini ve durum toohello (duraklatılmış ya da etkin) döndürür hello geçişten önce olan.
5. Merhaba geçiş tamamlandıktan sonra Microsoft "MyDW_DO_NOT_USE_ [zaman damgası]" siler.

> [!NOTE]
> Merhaba aşağıdaki ayarları hello geçişin bir parçası taşınmaz:
>
> * Merhaba veritabanı düzeyinde denetimi yeniden etkin toobe gerekir.
> * Merhaba veritabanı düzeyinde güvenlik duvarı kuralları yeniden eklendi toobe gerekir. Merhaba sunucu düzeyinde güvenlik duvarı kuralları etkilenmez.
>
>

### <a name="automatic-migration-schedule"></a>Otomatik geçiş zamanlama
Otomatik geçişler 6:00 ile 6: 00'da (her bölge yerel saat) arasında kesinti zamanlama uyarınca hello sırasında oluşur.

| **Bölge** | **Tahmini Başlangıç tarihi** | **Tahmini Bitiş tarihi** |
|:--- |:--- |:--- |
| Avustralya Doğu |Henüz karar değil |Henüz karar değil |
| Çin Doğu |9 Ocak 2017 |13 Ocak 2017 |
| Çin Kuzey |9 Ocak 2017 |13 Ocak 2017 |
| Almanya Orta |9 Ocak 2017 |13 Ocak 2017 |
| Almanya Kuzeydoğu |9 Ocak 2017 |13 Ocak 2017 |
| Hindistan Batı |Henüz karar değil |Henüz karar değil |
| Japonya Batı |Henüz karar değil |Henüz karar değil |
| Orta Kuzey ABD |9 Ocak 2017 |13 Ocak 2017 |

## <a name="self-migration-toopremium-storage"></a>Kendi kendine geçiş toopremium depolama
Kapalı kalma süresi ortaya çıktığında toocontrol istiyorsanız, adımları toomigrate mevcut bir veri ambarı standart depolama toopremium depolama alanında aşağıdaki hello kullanabilirsiniz. Bu seçeneği seçerseniz, bu bölgede hello otomatik geçiş başlamadan önce hello kendi kendine geçiş tamamlamanız gerekir. Bu herhangi bir çakışmasına neden hello otomatik geçiş riskini önlemek sağlar (toohello başvuran [otomatik geçiş zamanlama][automatic migration schedule]).

### <a name="self-migration-instructions"></a>Kendi kendine geçiş yönergeleri
Verilerinizi kendiniz ambar, hello yedekleme ve geri yükleme özellikleri toomigrate. Merhaba geri yükleme hello Geçiş beklenen tootake yaklaşık bir saat başına veri ambarına başına depolama terabayt bölümüdür. Geçiş tamamlandıktan sonra aynı adı tookeep hello istiyorsanız hello izleyin [adımları toorename geçiş sırasında][steps toorename during migration].

1. [Duraklatma] [ Pause] , veri ambarı. Otomatik yedekleme alır.
2. [Geri yükleme] [ Restore] en son anlık.
3. Mevcut veri ambarınız standart depolama silin. **Bu adımı toodo başarısız olursa, hem veri ambarlarında için sizden ücret alınır.**

> [!NOTE]
> Merhaba aşağıdaki ayarları hello geçişin bir parçası taşınmaz:
>
> * Merhaba veritabanı düzeyinde denetimi yeniden etkin toobe gerekir.
> * Merhaba veritabanı düzeyinde güvenlik duvarı kuralları yeniden eklendi toobe gerekir. Merhaba sunucu düzeyinde güvenlik duvarı kuralları etkilenmez.
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a>Veri ambarı (isteğe bağlı) geçiş sırasında yeniden adlandırma
İki veritabanı aynı mantıksal sunucu olamaz hello üzerinde hello aynı adı. SQL veri ambarı artık hello özelliği toorename bir veri ambarı destekler.

Bu örnekte, var olan veri ambarınız standart depolama üzerinde şu anda "MyDW." adlı düşünün

1. "MyDW" ALTER DATABASE komutu aşağıdaki hello kullanarak yeniden adlandırın. (Bu örnekte, biz "MyDW_BeforeMigration." yeniden adlandırmadan)  Bu komut, tüm mevcut işlemleri durdurur ve hello ana veritabanı toosucceed yapılması gerekir.
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. [Duraklatma] [ Pause] "MyDW_BeforeMigration." Otomatik yedekleme alır.
3. [Geri yükleme] [ Restore] , en son anlık hello ada sahip yeni bir veritabanı toobe (örneğin, "MyDW") kullanılır.
4. "MyDW_BeforeMigration." Sil **Bu adımı toodo başarısız olursa, hem veri ambarlarında için sizden ücret alınır.**


## <a name="next-steps"></a>Sonraki adımlar
Toopremium depolama Hello ile değiştirmek, veritabanı blob dosyaları sayısının artması hello temel alınan veri ambarınız mimarisinde de. Bu değişikliğin toomaximize hello performans avantajı, kümelenmiş columnstore dizinleri yeniden betik aşağıdaki hello kullanarak oluşturun. mevcut veri toohello ek bloblarınızın bazıları zorlayarak Hello betik çalışır. Hiçbir eylemde bulunmamanız halinde, tablolara daha fazla veri yükleme gibi hello veri zamanla doğal olarak dağıtan.

**Ön koşullar:**

- Merhaba veri ambarı 1.000 data warehouse birimleri veya sonrası çalıştırmanız gerekir (bkz [işlem güç ölçeklendirme][scale compute power]).
- Merhaba hello betiği yürütülürken kullanıcı hello olmalıdır [mediumrc rol] [ mediumrc role] ya da daha yüksek. bir kullanıcı toothis rolü tooadd hello aşağıdakileri yürütün:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

Veri ambarınız ile herhangi bir sorunla karşılaştığınızda [destek bileti oluşturma] [ create a support ticket] ve başvuru "geçiş toopremium depolama" Merhaba olası neden olarak.

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
