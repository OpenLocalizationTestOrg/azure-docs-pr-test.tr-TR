---
title: "aaaManage işlem güç Azure SQL Data warehouse'da (genel bakış) | Microsoft Docs"
description: "Azure SQL veri ambarı özellikleri genişletme performans. Dwu ayarlayarak ölçeğini veya duraklatma ve işlem kaynakları toosave maliyetlerini sürdürme."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a>Azure SQL Data warehouse'da (genel bakış) işlem güç yönetimi
> [!div class="op_single_selector"]
> * [Genel Bakış](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

SQL veri ambarı Hello mimarisi, depolama ve işlem, her tooscale bağımsız olarak izin verme ayırır. Sonuç olarak, işlem ölçeklendirilmiş toomeet performans taleplerini hello veri miktarını bağımsız olabilir. Bu mimarinin doğal bir sonuç [fatura] [ billed] işlem ve depolama için ayrıdır. 

Bu genel bakış açıklanmaktadır nasıl ölçeğini SQL veri ambarı ve tooutilize nasıl hello duraklatma, sürdürme ve SQL Data Warehouse ölçek özelliklerini çalışır. Merhaba başvurun [veri ambarı birimlerini (Dwu'lar)] [ data warehouse units (DWUs)] sayfa toolearn nasıl Dwu ve performans ilişkilidir. 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a>SQL veri ambarı'nda yönetim işlemlerini iş nasıl işlem
Merhaba mimarisi SQL veri ambarı için bir denetim düğümü oluşur, işlem düğümleri ve 60 dağıtımları yayılan hello depolama katmanı. 

Normal etkin oturum SQL Data warehouse'da sırasında sisteminizin baş düğüm hello meta verileri yönetir ve hello dağıtılmış sorgu iyileştiricisi içerir. Bu baş düğümü altında işlem düğümlerini ve depolama katmanı olan. DWU 400 için sisteminizi bir baş düğüm, dört işlem düğümlerini ve 60 dağıtımlarını oluşan hello depolama katmanı vardır. 

Bir ölçek uygulanabilecek veya işlemi duraklatmak, hello sistem ilk tüm gelen sorguları sonlandırır ve işlemleri tooensure tutarlı bir duruma geri alınır. Bu işlem geri alma işlemi tamamlandıktan sonra ölçek işlemleri için ölçeklendirme yalnızca meydana gelir. Bir ölçek büyütme işleminin hello sistem hükümleri fazladan istenen işlem düğümleri sayısını hello ve hello işlem düğümleri toohello depolama katmanı yeniden takmanız başlar. Bir ölçek azaltma işlemi için hello gereksiz düğümleri yayımlanan ve hello kalan işlem düğümleri kendilerini dağıtımları uygun sayıda toohello yeniden ekleyin. Duraklatma işlemi için tüm düğümler yayımlanan ve sisteminizin meta veri işlemleri tooleave çeşitli son kararlı bir duruma sisteminizdeki yapılacaktır işlem.

| DWU  | \#işlem düğümleri | \#Düğüm başına dağıtımları |
| ---- | ------------------ | ---------------------------- |
| 100  | 1                  | 60                           |
| 200  | 2                  | 30                           |
| 300  | 3                  | 20                           |
| 400  | 4                  | 15                           |
| 500  | 5                  | 12                           |
| 600  | 6                  | 10                           |
| 1000 | 10                 | 6                            |
| 1200 | 12                 | 5                            |
| 1500 | 15                 | 4                            |
| 2000 | 20                 | 3                            |
| 3000 | 30                 | 2                            |
| 6000 | 60                 | 1                            |

işlem yönetmek için hello üç birincil işlev şunlardır:

1. Duraklat
2. Sürdür
3. Ölçek

Bu işlemlerin her biri, birkaç dakika toocomplete devam edebilir. Otomatik olarak ölçeklendirme/duraklatma/sürdürme varsa, tooimplement mantığı tooensure başka bir eylem işlemine devam etmeden önce işlem tamamlandığında, belirli isteyebilirsiniz. 

Çeşitli uç noktaları aracılığıyla Hello veritabanı durumunu denetleme toocorrectly uygulama Otomasyon böyle işlemlerinin izin verir. Merhaba portalı bir işlemi ve hello veritabanları geçerli durumu tamamlanmasından sonra bildirim sağlar ancak programlı durumunu denetlemek için izin vermiyor. 

>  [!NOTE]
>
>  İşlem yönetimi işlevselliği tüm uç noktalar arasında yok.
>
>  

|              | Duraklat/Sürdür | Ölçek | Veritabanı durumunu kontrol edin |
| ------------ | ------------ | ----- | -------------------- |
| Azure portalına | Evet          | Evet   | **Hayır**               |
| PowerShell   | Evet          | Evet   | Evet                  |
| REST API     | Evet          | Evet   | Evet                  |
| T-SQL        | **Hayır**       | Evet   | Evet                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Bilgi işlem

SQL veri ambarı performans ölçülür [veri ambarı birimlerini (Dwu'lar)] [ data warehouse units (DWUs)] CPU, bellek ve g/ç bant genişliği gibi işlem kaynakları abstracted bir ölçü değil. Kendi sistem performansını tooscale isteyen bir kullanıcı çeşitli yollarla gibi hello portal, T-SQL ve REST API'leri bunu yapabilirsiniz. 

### <a name="how-do-i-scale-compute"></a>İşlem nasıl ölçeklendirme?
İşlem gücü, SQL Data Warehouse hello DWU ayarını değiştirerek yönetilir. Performans artışı [doğrusal olarak] [ linearly] gibi belirli işlemler için daha fazla DWU ekleyin.  Yukarı veya aşağı sisteminizi ne zaman ölçeklendirme, performansı belirgin şekilde değişir olun DWU teklifleri sunuyoruz. 

tooadjust Dwu, tek tek bu yöntemlerden birini kullanabilirsiniz.

* [Azure portal ile güç işlem ölçeklendirme][Scale compute power with Azure portal]
* [İşlem PowerShell ile güç ölçeklendirme][Scale compute power with PowerShell]
* [REST API'leri ile ölçek işlem gücü][Scale compute power with REST APIs]
* [TSQL ile güç işlem ölçeklendirme][Scale compute power with TSQL]

### <a name="how-many-dwus-should-i-use"></a>Kaç tane Dwu kullanmalıyım?

hangi, ideal DWU değerdir, toounderstand yukarı ve aşağı doğru ölçeklendirme ve verilerinizi yükledikten sonra birkaç sorgu çalıştırmayı deneyin. Ölçeklendirme hızla gerçekleştiği bir saat veya daha az çeşitli performans düzeylerini deneyebilirsiniz. 

> [!Note] 
> SQL veri ambarı tasarlanmış tooprocess büyük miktarlarda verinin ' dir. toosee, özellikle büyük Dwu ölçeklendirmeye yönelik gerçek kapasitesini istediğiniz toouse, 1 TB yaklaşıyor veya büyük bir veri kümesi.

Bulma için öneriler, iş yükü için en iyi DWU hello:

1. Geliştirme bir veri ambarı için daha küçük bir DWU performans düzeyi seçerek başlayın.  İyi bir başlangıç noktası DW400 veya DW200 ' dir.
2. Uygulama performansı izleme, seçili Dwu sayısı hello Gözlemleme, gözlemlemek toohello performans karşılaştırılan.
3. Ne kadar hızlı veya daha yavaş performans, tooreach hello en iyi performansı düzeyi için gereksinimlerinizi doğrusal ölçek üstlenerek olacağını belirleyebilirsiniz.
4. Artırma veya azaltma hello numarası oranı toohow çok daha hızlı veya daha yavaş Dwu, iş yükü tooperform istiyor. 
5. İş gereksinimleriniz için en iyi performansı düzeyi ulaşana kadar ayarlamaları devam edin.

> [!NOTE]
>
> Merhaba iş işlem düğümleri arasında bölünebilir, sorgu performansı ile daha fazla paralelleştirme yalnızca artırır. Ölçeklendirme performansınızı değişmeyen olduğunu fark ederseniz, lütfen bizim performans makaleleri toocheck verilerinizi düz olmayan şekilde dağıtılmış olup olmadığını veya çok miktarda veri taşıma giriş varsa ayarlama denetleyin. 

### <a name="when-should-i-scale-dwus"></a>Dwu zaman ölçeklendirmeniz gerekir?
Dwu ölçeklendirme önemli senaryolar aşağıdaki hello değiştirir:

1. Doğrusal olarak taramaları, toplamalar ve CTAS deyimleri hello sistem performansını değiştirme
2. PolyBase ile birlikte yüklenirken okuyucuları ve yazıcıları Hello sayısını artırmayı
3. Maksimum eş zamanlı sorgular ve eşzamanlılık yuva sayısı

Ne zaman için öneriler tooscale Dwu:

1. Çok miktarda verinin yüklendiği veya dönüştürüldüğü işlemi gerçekleştirmeden önce verilerinizin daha hızlı kullanılabilir olmasını sağlamak Dwu ölçeklendirin.
2. Yoğun iş saatlerinde tooaccommodate çok sayıda eş zamanlı sorguları ölçeklendirin. 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Duraklatma işlem
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

bir veritabanı toopause tek tek bu yöntemlerden birini kullanın.

* [Azure portal ile Duraklat işlem][Pause compute with Azure portal]
* [PowerShell ile Duraklat işlem][Pause compute with PowerShell]
* [REST API'leri ile Duraklat işlem][Pause compute with REST APIs]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Resume işlem
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

bir veritabanı tooresume tek tek bu yöntemlerden birini kullanın.

* [Azure portal ile Sürdür işlem][Resume compute with Azure portal]
* [PowerShell ile Sürdür işlem][Resume compute with PowerShell]
* [REST API'leri ile Sürdür işlem][Resume compute with REST APIs]

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a>Veritabanı durumunu kontrol edin 

bir veritabanı tooresume tek tek bu yöntemlerden birini kullanın.

- [T-SQL ile veritabanı durumunu kontrol edin][Check database state with T-SQL]
- [PowerShell ile veritabanı durumunu kontrol edin][Check database state with PowerShell]
- [REST API'leri ile veritabanı durumunu kontrol edin][Check database state with REST APIs]

## <a name="permissions"></a>İzinler

Ölçeklendirme hello veritabanı açıklanan hello izinleri gerektirir [ALTER DATABASE][ALTER DATABASE].  Duraklatma ve sürdürme gerektiren hello [SQL DB Katılımcısı] [ SQL DB Contributor] izni, özellikle Microsoft.Sql/servers/databases/action.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Sonraki adımlar
Bazı ek anahtar performans kavramları anlamanız makaleleri toohelp aşağıdaki toohello bakın:

* [İş yükü ve eşzamanlılık Yönetimi][Workload and concurrency management]
* [Tablo Tasarım genel bakış][Table design overview]
* [Tablo dağıtım][Table distribution]
* [Tablo dizin oluşturma][Table indexing]
* [Tablo bölümleme][Table partitioning]
* [Tablo istatistikleri][Table statistics]
* [En iyi uygulamalar][Best practices]

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
