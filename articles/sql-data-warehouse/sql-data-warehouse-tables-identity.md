---
title: "KİMLİĞİ kullanarak yedek anahtarları oluşturma | Microsoft Docs"
description: "KİMLİK tablolarınızı yedek anahtarlar oluşturmak için nasıl kullanılacağını öğrenin."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 3ab5d159e6eaeb830135fe134e108b0e4de4b7d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="3c16c-103">Yedek anahtarları kimliği kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="3c16c-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="3c16c-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="3c16c-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="3c16c-105">[Veri türleri][Data Types]</span><span class="sxs-lookup"><span data-stu-id="3c16c-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="3c16c-106">[Dağıt][Distribute]</span><span class="sxs-lookup"><span data-stu-id="3c16c-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="3c16c-107">[Dizin][Index]</span><span class="sxs-lookup"><span data-stu-id="3c16c-107">[Index][Index]</span></span>
> * <span data-ttu-id="3c16c-108">[Bölüm][Partition]</span><span class="sxs-lookup"><span data-stu-id="3c16c-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="3c16c-109">[İstatistikleri][Statistics]</span><span class="sxs-lookup"><span data-stu-id="3c16c-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="3c16c-110">[Geçici][Temporary]</span><span class="sxs-lookup"><span data-stu-id="3c16c-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="3c16c-111">[Kimlik][Identity]</span><span class="sxs-lookup"><span data-stu-id="3c16c-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="3c16c-112">Veri ambarı modelleri tasarlarken kendi tablolarda yedek anahtarlar oluşturmak çok sayıda veri modelers gibi.</span><span class="sxs-lookup"><span data-stu-id="3c16c-112">Many data modelers like to create surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="3c16c-113">IDENTİTY özelliği yükü performansınızı etkilemeden sadece ve etkili bir şekilde bu hedefe ulaşmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3c16c-113">You can use the IDENTITY property to achieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="3c16c-114">KİMLİĞİ ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3c16c-114">Get started with IDENTITY</span></span>
<span data-ttu-id="3c16c-115">Aşağıdaki deyime benzer sözdizimini kullanarak ilk tablonun oluşturduğunuzda kimlik özelliğine sahip olarak bir tablo tanımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3c16c-115">You can define a table as having the IDENTITY property when you first create the table by using syntax that is similar to the following statement:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

<span data-ttu-id="3c16c-116">Daha sonra kullanabilirsiniz `INSERT..SELECT` tabloyu doldurmak için.</span><span class="sxs-lookup"><span data-stu-id="3c16c-116">You can then use `INSERT..SELECT` to populate the table.</span></span>

## <a name="behavior"></a><span data-ttu-id="3c16c-117">Davranışı</span><span class="sxs-lookup"><span data-stu-id="3c16c-117">Behavior</span></span>
<span data-ttu-id="3c16c-118">KİMLİK özelliği, veri ambarındaki tüm dağıtımlar arasında yük performanslarını etkilemeden genişletmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="3c16c-118">The IDENTITY property is designed to scale out across all the distributions in the data warehouse without affecting load performance.</span></span> <span data-ttu-id="3c16c-119">Bu nedenle, kimlik bu hedeflere ulaşmak doğru yönlendirilmiş uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="3c16c-119">Therefore, the implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="3c16c-120">Bu bölümde daha eksiksiz anlamanıza yardımcı olması için uygulama nüanslarını vurgular.</span><span class="sxs-lookup"><span data-stu-id="3c16c-120">This section highlights the nuances of the implementation to help you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="3c16c-121">Değerlerin ayırma</span><span class="sxs-lookup"><span data-stu-id="3c16c-121">Allocation of values</span></span>
<span data-ttu-id="3c16c-122">KİMLİK özelliği, SQL Server ve Azure SQL veritabanı davranışını yansıtan, yedek değerleri ayrılmış, sipariş garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="3c16c-122">The IDENTITY property doesn't guarantee the order in which the surrogate values are allocated, which reflects the behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="3c16c-123">Ancak, Azure SQL veri ambarı'nda bir garanti yokluğu daha belirgin olur.</span><span class="sxs-lookup"><span data-stu-id="3c16c-123">However, in Azure SQL Data Warehouse, the absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="3c16c-124">Aşağıdaki çizim bir örnektir:</span><span class="sxs-lookup"><span data-stu-id="3c16c-124">The following example is an illustration:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

<span data-ttu-id="3c16c-125">Önceki örnekte, iki satır dağıtım 1 landed.</span><span class="sxs-lookup"><span data-stu-id="3c16c-125">In the preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="3c16c-126">İlk satırı sütun yedek değeri 1 olan `C1`, ve ikinci satırında 61 yedek değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="3c16c-126">The first row has the surrogate value of 1 in column `C1`, and the second row has the surrogate value of 61.</span></span> <span data-ttu-id="3c16c-127">Bu değerlerin her ikisi de kimlik özelliği tarafından üretildi.</span><span class="sxs-lookup"><span data-stu-id="3c16c-127">Both of these values were generated by the IDENTITY property.</span></span> <span data-ttu-id="3c16c-128">Ancak, değerleri ayırma bitişik değil.</span><span class="sxs-lookup"><span data-stu-id="3c16c-128">However, the allocation of the values is not contiguous.</span></span> <span data-ttu-id="3c16c-129">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="3c16c-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="3c16c-130">Çarpık veri</span><span class="sxs-lookup"><span data-stu-id="3c16c-130">Skewed data</span></span> 
<span data-ttu-id="3c16c-131">Veri türü için değer aralığını dağıtımlar arasında eşit olarak yayılır.</span><span class="sxs-lookup"><span data-stu-id="3c16c-131">The range of values for the data type are spread evenly across the distributions.</span></span> <span data-ttu-id="3c16c-132">Dağıtılmış bir tablo çarpık verileri varsa, ardından veri türü için kullanılabilir değerleri aralığı erken tükendi.</span><span class="sxs-lookup"><span data-stu-id="3c16c-132">If a distributed table suffers from skewed data, then the range of values available to the datatype can be exhausted prematurely.</span></span> <span data-ttu-id="3c16c-133">Tüm verileri sona eriyor, tek bir dağıtım Örneğin, ardından etkili bir şekilde tablo yalnızca bir-sixtieth veri türü değerlerinin erişebilir.</span><span class="sxs-lookup"><span data-stu-id="3c16c-133">For example, if all the data ends up in a single distribution, then effectively the table has access to only one-sixtieth of the values of the data type.</span></span> <span data-ttu-id="3c16c-134">Bu nedenle, kimlik özelliği sınırlıdır `INT` ve `BIGINT` veri türleri yalnızca.</span><span class="sxs-lookup"><span data-stu-id="3c16c-134">For this reason, the IDENTITY property is limited to `INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="3c16c-135">SEÇİN... İÇİNE</span><span class="sxs-lookup"><span data-stu-id="3c16c-135">SELECT..INTO</span></span>
<span data-ttu-id="3c16c-136">Varolan bir kimlik sütunu yeni bir tabloya seçildiğinde, yeni bir sütun aşağıdaki koşullardan biri doğru olmadıkça kimlik özelliği alır:</span><span class="sxs-lookup"><span data-stu-id="3c16c-136">When an existing IDENTITY column is selected into a new table, the new column inherits the IDENTITY property, unless one of the following conditions is true:</span></span>
- <span data-ttu-id="3c16c-137">SELECT deyimi bir birleştirme içerir.</span><span class="sxs-lookup"><span data-stu-id="3c16c-137">The SELECT statement contains a join.</span></span>
- <span data-ttu-id="3c16c-138">Birden çok SELECT deyimine birleşim kullanılarak birleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3c16c-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="3c16c-139">KİMLİK sütunu SELECT listesinde birden fazla kez listelenir.</span><span class="sxs-lookup"><span data-stu-id="3c16c-139">The IDENTITY column is listed more than one time in the SELECT list.</span></span>
- <span data-ttu-id="3c16c-140">KİMLİK sütunu bir ifadenin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="3c16c-140">The IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="3c16c-141">Bu koşulların herhangi biri doğruysa, sütun kimlik özelliğini devralan yerine NOT NULL oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3c16c-141">If any one of these conditions is true, the column is created NOT NULL instead of inheriting the IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="3c16c-142">TABLE AS SELECT OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="3c16c-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="3c16c-143">OLUŞTURMA tablo AS seçin (CTAS) için SELECT belgelenen aynı SQL Server davranışı izleyen... .</span><span class="sxs-lookup"><span data-stu-id="3c16c-143">CREATE TABLE AS SELECT (CTAS) follows the same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="3c16c-144">Ancak, bir kimlik özelliği sütun tanımında belirtemezsiniz `CREATE TABLE` deyim parçası.</span><span class="sxs-lookup"><span data-stu-id="3c16c-144">However, you can't specify an IDENTITY property in the column definition of the `CREATE TABLE` part of the statement.</span></span> <span data-ttu-id="3c16c-145">Ayrıca kimlik işlevinde kullanamazsınız `SELECT` CTAS bir parçası.</span><span class="sxs-lookup"><span data-stu-id="3c16c-145">You also can't use the IDENTITY function in the `SELECT` part of the CTAS.</span></span> <span data-ttu-id="3c16c-146">Bir tabloyu doldurmak için kullanmanız gerekir `CREATE TABLE` arkasından tablosu tanımlamak için `INSERT..SELECT` onu doldurmak için.</span><span class="sxs-lookup"><span data-stu-id="3c16c-146">To populate a table, you need to use `CREATE TABLE` to define the table followed by `INSERT..SELECT` to populate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="3c16c-147">Açıkça değerleri bir kimlik sütununa ekleme</span><span class="sxs-lookup"><span data-stu-id="3c16c-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="3c16c-148">SQL veri ambarı destekleyen `SET IDENTITY_INSERT <your table> ON|OFF` sözdizimi.</span><span class="sxs-lookup"><span data-stu-id="3c16c-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="3c16c-149">Açıkça kimlik sütununa değerleri eklemek için şu sözdizimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="3c16c-149">You can use this syntax to explicitly insert values into the IDENTITY column.</span></span>

<span data-ttu-id="3c16c-150">Birçok veri modelers kendi boyutlarını belirli satırlar için önceden tanımlanmış negatif değerler kullanmak ister.</span><span class="sxs-lookup"><span data-stu-id="3c16c-150">Many data modelers like to use predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="3c16c-151">-1 veya "Bilinmeyen bir üyeye" satır örneğidir.</span><span class="sxs-lookup"><span data-stu-id="3c16c-151">An example is the -1 or "unknown member" row.</span></span> 

<span data-ttu-id="3c16c-152">Sonraki komut dosyası açıkça AYARLAMAK IDENTITY_INSERT kullanarak bu satır eklemek nasıl gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="3c16c-152">The next script shows how to explicitly add this row by using SET IDENTITY_INSERT:</span></span>

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="3c16c-153">KİMLİĞİNE sahip bir tabloya veri yükleme</span><span class="sxs-lookup"><span data-stu-id="3c16c-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="3c16c-154">IDENTİTY özelliği varlığını veri yükleme kodunuza bazı etkilere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3c16c-154">The presence of the IDENTITY property has some implications to your data-loading code.</span></span> <span data-ttu-id="3c16c-155">Bu bölüm kimliği kullanarak verileri tablolara yüklemek için bazı temel düzenlerden vurgular.</span><span class="sxs-lookup"><span data-stu-id="3c16c-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="3c16c-156">PolyBase ile veri yükleyin</span><span class="sxs-lookup"><span data-stu-id="3c16c-156">Load data with PolyBase</span></span>
<span data-ttu-id="3c16c-157">Verileri bir tabloya yüklemek ve bir yedek anahtar kimliği kullanarak oluşturmak, tablo oluştur ve Ekle kullanmak için... Seç veya Ekle... Yükleme gerçekleştirmek için değerler.</span><span class="sxs-lookup"><span data-stu-id="3c16c-157">To load data into a table and generate a surrogate key by using IDENTITY, create the table and then use INSERT..SELECT or INSERT..VALUES to perform the load.</span></span>

<span data-ttu-id="3c16c-158">Aşağıdaki örnek temel düzeni vurgular:</span><span class="sxs-lookup"><span data-stu-id="3c16c-158">The following example highlights the basic pattern:</span></span>
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT to populate the table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> <span data-ttu-id="3c16c-159">Kullanmak mümkün değil `CREATE TABLE AS SELECT` şu anda verileri bir kimlik sütunu olan bir tabloya yüklenirken.</span><span class="sxs-lookup"><span data-stu-id="3c16c-159">It's not possible to use `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="3c16c-160">Toplu kopyalama programı (BCP) aracını kullanarak veri yükleme ile ilgili daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="3c16c-160">For more information on loading data by using the bulk copy program (BCP) tool, see the following articles:</span></span>

- <span data-ttu-id="3c16c-161">[PolyBase ile yükleme][]</span><span class="sxs-lookup"><span data-stu-id="3c16c-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="3c16c-162">[PolyBase en iyi uygulamalar][]</span><span class="sxs-lookup"><span data-stu-id="3c16c-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="3c16c-163">BCP ile veri yükleme</span><span class="sxs-lookup"><span data-stu-id="3c16c-163">Load data with BCP</span></span>
<span data-ttu-id="3c16c-164">BCP SQL Data Warehouse'a veri yüklemek için kullanabileceğiniz bir komut satırı aracıdır.</span><span class="sxs-lookup"><span data-stu-id="3c16c-164">BCP is a command-line tool that you can use to load data into SQL Data Warehouse.</span></span> <span data-ttu-id="3c16c-165">Parametrelerinden biri (-E) verileri bir kimlik sütunu olan bir tabloya yüklenirken BCP davranışını denetler.</span><span class="sxs-lookup"><span data-stu-id="3c16c-165">One of its parameters (-E) controls the behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="3c16c-166">-E belirtildiğinde, sütun için giriş dosyasındaki KİMLİKLE tutulan değerleri korunur.</span><span class="sxs-lookup"><span data-stu-id="3c16c-166">When -E is specified, the values held in the input file for the column with IDENTITY are retained.</span></span> <span data-ttu-id="3c16c-167">-E ise *değil* belirtilen sonra da bu sütundaki değerleri yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="3c16c-167">If -E is *not* specified, then the values in this column are ignored.</span></span> <span data-ttu-id="3c16c-168">Kimlik sütununun dahil edilmezse, verileri normal olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="3c16c-168">If the identity column is not included, then the data is loaded as normal.</span></span> <span data-ttu-id="3c16c-169">Değerleri özelliği artırma ve çekirdek ilkesine göre oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3c16c-169">The values are generated according to the increment and seed policy of the property.</span></span>

<span data-ttu-id="3c16c-170">BCP kullanarak veri yükleme ile ilgili daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="3c16c-170">For more information on loading data by using BCP, see the following articles:</span></span>

- <span data-ttu-id="3c16c-171">[BCP ile yükleme][]</span><span class="sxs-lookup"><span data-stu-id="3c16c-171">[Load with BCP][]</span></span>
- <span data-ttu-id="3c16c-172">[BCP MSDN'de][]</span><span class="sxs-lookup"><span data-stu-id="3c16c-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="3c16c-173">Katalog görünümleri</span><span class="sxs-lookup"><span data-stu-id="3c16c-173">Catalog views</span></span>
<span data-ttu-id="3c16c-174">SQL veri ambarı destekleyen `sys.identity_columns` Katalog görünümü.</span><span class="sxs-lookup"><span data-stu-id="3c16c-174">SQL Data Warehouse supports the `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="3c16c-175">Bu görünüm, kimlik özelliğine sahip bir sütunu tanımlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3c16c-175">This view can be used to identify a column that has the IDENTITY property.</span></span>

<span data-ttu-id="3c16c-176">Veritabanı şeması daha iyi anlamanıza yardımcı olması için bu örnek nasıl tümleştirileceği gösterir `sys.identity_columns` diğer sistem Katalog görünümleri ile:</span><span class="sxs-lookup"><span data-stu-id="3c16c-176">To help you better understand the database schema, this example shows how to integrate `sys.identity_columns` with other system catalog views:</span></span>

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a><span data-ttu-id="3c16c-177">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="3c16c-177">Limitations</span></span>
<span data-ttu-id="3c16c-178">KİMLİK özelliği aşağıdaki senaryolarda kullanılamaz:</span><span class="sxs-lookup"><span data-stu-id="3c16c-178">The IDENTITY property can't be used in the following scenarios:</span></span>
- <span data-ttu-id="3c16c-179">Burada sütun veri türü tamsayı veya büyük tamsayı değil</span><span class="sxs-lookup"><span data-stu-id="3c16c-179">Where the column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="3c16c-180">Sütun dağıtım anahtarı da olduğu</span><span class="sxs-lookup"><span data-stu-id="3c16c-180">Where the column is also the distribution key</span></span>
- <span data-ttu-id="3c16c-181">Tablo bir dış tablo olduğu</span><span class="sxs-lookup"><span data-stu-id="3c16c-181">Where the table is an external table</span></span> 

<span data-ttu-id="3c16c-182">SQL veri ambarı'nda aşağıdaki ilgili işlevleri desteklenmez:</span><span class="sxs-lookup"><span data-stu-id="3c16c-182">The following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="3c16c-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="3c16c-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="3c16c-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="3c16c-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="3c16c-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="3c16c-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="3c16c-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="3c16c-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="3c16c-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="3c16c-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="3c16c-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="3c16c-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="3c16c-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="3c16c-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="3c16c-190">Görevler</span><span class="sxs-lookup"><span data-stu-id="3c16c-190">Tasks</span></span>

<span data-ttu-id="3c16c-191">Bu bölümde kimlik sütunu ile çalışırken ortak görevleri gerçekleştirmek için kullanabileceğiniz bazı örnek kodu sağlıyor.</span><span class="sxs-lookup"><span data-stu-id="3c16c-191">This section provides some sample code you can use to perform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="3c16c-192">Sütun C1 tüm aşağıdaki görevler kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="3c16c-192">Column C1 is the IDENTITY in all the following tasks.</span></span>
> 
 
### <a name="find-the-highest-allocated-value-for-a-table"></a><span data-ttu-id="3c16c-193">Bir tablo için en yüksek ayrılmış değeri Bul</span><span class="sxs-lookup"><span data-stu-id="3c16c-193">Find the highest allocated value for a table</span></span>
<span data-ttu-id="3c16c-194">Kullanım `MAX()` işlevi dağıtılmış bir tablo için ayrılan en yüksek değeri belirlemek için:</span><span class="sxs-lookup"><span data-stu-id="3c16c-194">Use the `MAX()` function to determine the highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-the-seed-and-increment-for-the-identity-property"></a><span data-ttu-id="3c16c-195">Çekirdek ve Artım kimlik özelliği için Bul</span><span class="sxs-lookup"><span data-stu-id="3c16c-195">Find the seed and increment for the IDENTITY property</span></span>
<span data-ttu-id="3c16c-196">Katalog görünümleri aşağıdaki sorguyu kullanarak bir tablo için kimlik artırma ve çekirdek yapılandırma değerlerini bulmak için kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3c16c-196">You can use the catalog views to discover the identity increment and seed configuration values for a table by using the following query:</span></span> 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a><span data-ttu-id="3c16c-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3c16c-197">Next steps</span></span>

* <span data-ttu-id="3c16c-198">Tabloları geliştirme hakkında daha fazla bilgi için bkz: [tablo genel bakış][Overview], [tablo veri türleri][Data Types], [bir tabloDağıt] [ Distribute], [Tablo dizin][Index], [tablo bölüm][Partition], ve [ Geçici tablolara][Temporary].</span><span class="sxs-lookup"><span data-stu-id="3c16c-198">To learn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="3c16c-199">En iyi uygulamalar hakkında daha fazla bilgi için bkz: [SQL veri ambarı en iyi yöntemler][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="3c16c-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<span data-ttu-id="3c16c-200">[BCP ile yükleme]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/</span><span class="sxs-lookup"><span data-stu-id="3c16c-200">[Load with bcp]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/</span></span>
<span data-ttu-id="3c16c-201">[PolyBase ile yükleme]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/</span><span class="sxs-lookup"><span data-stu-id="3c16c-201">[Load with PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/</span></span>
<span data-ttu-id="3c16c-202">[PolyBase en iyi uygulamalar]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/</span><span class="sxs-lookup"><span data-stu-id="3c16c-202">[PolyBase best practices]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/</span></span>


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
<span data-ttu-id="3c16c-203">[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx</span><span class="sxs-lookup"><span data-stu-id="3c16c-203">[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx</span></span>
<span data-ttu-id="3c16c-204">[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx</span><span class="sxs-lookup"><span data-stu-id="3c16c-204">[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx</span></span>
<span data-ttu-id="3c16c-205">[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx</span><span class="sxs-lookup"><span data-stu-id="3c16c-205">[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx</span></span>
<span data-ttu-id="3c16c-206">[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx</span><span class="sxs-lookup"><span data-stu-id="3c16c-206">[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx</span></span>
<span data-ttu-id="3c16c-207">[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx</span><span class="sxs-lookup"><span data-stu-id="3c16c-207">[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx</span></span>
<span data-ttu-id="3c16c-208">[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx</span><span class="sxs-lookup"><span data-stu-id="3c16c-208">[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx</span></span>
<span data-ttu-id="3c16c-209">[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx</span><span class="sxs-lookup"><span data-stu-id="3c16c-209">[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx</span></span>

<span data-ttu-id="3c16c-210">[BCP MSDN'de]: https://msdn.microsoft.com/library/ms162802.aspx</span><span class="sxs-lookup"><span data-stu-id="3c16c-210">[bcp in MSDN]: https://msdn.microsoft.com/library/ms162802.aspx</span></span>
  

<!--Other Web references-->  
