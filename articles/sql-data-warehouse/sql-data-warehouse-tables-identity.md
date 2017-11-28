---
title: "KİMLİK kullanarak aaaCreate yedek anahtarları | Microsoft Docs"
description: "Nasıl toouse kimlik toocreate yedek tablolarınızı anahtarları hakkında bilgi edinin."
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
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="d1135-103">Yedek anahtarları kimliği kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="d1135-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="d1135-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="d1135-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="d1135-105">[Veri türleri][Data Types]</span><span class="sxs-lookup"><span data-stu-id="d1135-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="d1135-106">[Dağıt][Distribute]</span><span class="sxs-lookup"><span data-stu-id="d1135-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="d1135-107">[Dizin][Index]</span><span class="sxs-lookup"><span data-stu-id="d1135-107">[Index][Index]</span></span>
> * <span data-ttu-id="d1135-108">[Bölüm][Partition]</span><span class="sxs-lookup"><span data-stu-id="d1135-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="d1135-109">[İstatistikleri][Statistics]</span><span class="sxs-lookup"><span data-stu-id="d1135-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="d1135-110">[Geçici][Temporary]</span><span class="sxs-lookup"><span data-stu-id="d1135-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="d1135-111">[Kimlik][Identity]</span><span class="sxs-lookup"><span data-stu-id="d1135-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="d1135-112">Veri ambarı modelleri tasarlarken birçok veri modelers tablolarıyla toocreate yedek anahtarları ister.</span><span class="sxs-lookup"><span data-stu-id="d1135-112">Many data modelers like toocreate surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="d1135-113">Merhaba kimlik özelliği tooachieve sadece ve etkili bir şekilde bu hedef yükü performansınızı etkilemeden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1135-113">You can use hello IDENTITY property tooachieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="d1135-114">KİMLİĞİ ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d1135-114">Get started with IDENTITY</span></span>
<span data-ttu-id="d1135-115">Aşağıdaki ifadeyi benzer toohello olan sözdizimini kullanarak ilk hello tablo oluşturduğunuzda hello kimlik özelliğine sahip olarak bir tablo tanımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d1135-115">You can define a table as having hello IDENTITY property when you first create hello table by using syntax that is similar toohello following statement:</span></span>

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

<span data-ttu-id="d1135-116">Daha sonra `INSERT..SELECT` toopopulate hello tablo.</span><span class="sxs-lookup"><span data-stu-id="d1135-116">You can then use `INSERT..SELECT` toopopulate hello table.</span></span>

## <a name="behavior"></a><span data-ttu-id="d1135-117">Davranışı</span><span class="sxs-lookup"><span data-stu-id="d1135-117">Behavior</span></span>
<span data-ttu-id="d1135-118">Merhaba kimlik özelliği çıkışı tasarlanmış tooscale yük performanslarını etkilemeden hello veri ambarındaki tüm hello dağıtımlar arasında değil.</span><span class="sxs-lookup"><span data-stu-id="d1135-118">hello IDENTITY property is designed tooscale out across all hello distributions in hello data warehouse without affecting load performance.</span></span> <span data-ttu-id="d1135-119">Bu nedenle, hello kimlik bu hedeflere ulaşmak doğru yönlendirilmiş uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="d1135-119">Therefore, hello implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="d1135-120">Bu bölüm hello nüanslarını vurgular hello uygulama toohelp siz bunları daha tam olarak anlamak.</span><span class="sxs-lookup"><span data-stu-id="d1135-120">This section highlights hello nuances of hello implementation toohelp you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="d1135-121">Değerlerin ayırma</span><span class="sxs-lookup"><span data-stu-id="d1135-121">Allocation of values</span></span>
<span data-ttu-id="d1135-122">Merhaba kimlik özelliği hangi hello ayrılan yedek değerleri, SQL Server ve Azure SQL veritabanı hello davranışını yansıtan hello sipariş garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="d1135-122">hello IDENTITY property doesn't guarantee hello order in which hello surrogate values are allocated, which reflects hello behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="d1135-123">Ancak, Azure SQL veri ambarı'nda bir garanti hello yokluğu daha belirgin olur.</span><span class="sxs-lookup"><span data-stu-id="d1135-123">However, in Azure SQL Data Warehouse, hello absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="d1135-124">Aşağıdaki örnek hello çizim şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d1135-124">hello following example is an illustration:</span></span>

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

<span data-ttu-id="d1135-125">Örnek önceki hello iki satır dağıtım 1 landed.</span><span class="sxs-lookup"><span data-stu-id="d1135-125">In hello preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="d1135-126">Hello ilk satır sütununda hello yedek değeri 1 olan `C1`, ve hello ikinci satırında 61 hello yedek değeri.</span><span class="sxs-lookup"><span data-stu-id="d1135-126">hello first row has hello surrogate value of 1 in column `C1`, and hello second row has hello surrogate value of 61.</span></span> <span data-ttu-id="d1135-127">Bu değerlerin her ikisi de hello kimlik özelliği tarafından üretildi.</span><span class="sxs-lookup"><span data-stu-id="d1135-127">Both of these values were generated by hello IDENTITY property.</span></span> <span data-ttu-id="d1135-128">Ancak, hello ayırma hello değerlerin bitişik değil.</span><span class="sxs-lookup"><span data-stu-id="d1135-128">However, hello allocation of hello values is not contiguous.</span></span> <span data-ttu-id="d1135-129">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="d1135-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="d1135-130">Çarpık veri</span><span class="sxs-lookup"><span data-stu-id="d1135-130">Skewed data</span></span> 
<span data-ttu-id="d1135-131">Merhaba hello veri türünün değer aralığını hello dağıtımlar arasında eşit olarak yayılır.</span><span class="sxs-lookup"><span data-stu-id="d1135-131">hello range of values for hello data type are spread evenly across hello distributions.</span></span> <span data-ttu-id="d1135-132">Dağıtılmış bir tablo çarpık verileri varsa, kullanılabilir toohello datatype erken tükenmiş olabilir değerlerin hello.</span><span class="sxs-lookup"><span data-stu-id="d1135-132">If a distributed table suffers from skewed data, then hello range of values available toohello datatype can be exhausted prematurely.</span></span> <span data-ttu-id="d1135-133">Tüm hello verileri sona eriyor, tek bir dağıtım, örneğin, etkili bir şekilde hello tablo hello veri türünün hello değerlerin erişim tooonly bir sixtieth yoktur.</span><span class="sxs-lookup"><span data-stu-id="d1135-133">For example, if all hello data ends up in a single distribution, then effectively hello table has access tooonly one-sixtieth of hello values of hello data type.</span></span> <span data-ttu-id="d1135-134">Bu nedenle, hello kimlik özelliği çok sınırlı`INT` ve `BIGINT` veri türleri yalnızca.</span><span class="sxs-lookup"><span data-stu-id="d1135-134">For this reason, hello IDENTITY property is limited too`INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="d1135-135">SEÇİN... İÇİNE</span><span class="sxs-lookup"><span data-stu-id="d1135-135">SELECT..INTO</span></span>
<span data-ttu-id="d1135-136">Varolan bir kimlik sütunu yeni bir tabloya seçildiğinde, hello koşullar aşağıdaki koşullardan biri sürece hello yeni bir sütun hello kimlik özelliği alır:</span><span class="sxs-lookup"><span data-stu-id="d1135-136">When an existing IDENTITY column is selected into a new table, hello new column inherits hello IDENTITY property, unless one of hello following conditions is true:</span></span>
- <span data-ttu-id="d1135-137">Merhaba SELECT deyimi bir birleştirme içerir.</span><span class="sxs-lookup"><span data-stu-id="d1135-137">hello SELECT statement contains a join.</span></span>
- <span data-ttu-id="d1135-138">Birden çok SELECT deyimine birleşim kullanılarak birleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d1135-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="d1135-139">Merhaba kimlik sütunu hello SELECT listesinde birden fazla kez listelenir.</span><span class="sxs-lookup"><span data-stu-id="d1135-139">hello IDENTITY column is listed more than one time in hello SELECT list.</span></span>
- <span data-ttu-id="d1135-140">Merhaba kimlik sütunu bir ifadenin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="d1135-140">hello IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="d1135-141">Bu koşulların herhangi biri doğruysa hello sütun hello kimlik özelliğini devralan yerine NOT NULL oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d1135-141">If any one of these conditions is true, hello column is created NOT NULL instead of inheriting hello IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="d1135-142">TABLE AS SELECT OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="d1135-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="d1135-143">OLUŞTURMA tablo AS seçin (CTAS) aşağıdaki seçim belgelenen aynı SQL Server davranışı hello... .</span><span class="sxs-lookup"><span data-stu-id="d1135-143">CREATE TABLE AS SELECT (CTAS) follows hello same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="d1135-144">Ancak, bir kimlik özelliği hello sütun tanımında hello belirtemezsiniz `CREATE TABLE` hello deyimi parçası.</span><span class="sxs-lookup"><span data-stu-id="d1135-144">However, you can't specify an IDENTITY property in hello column definition of hello `CREATE TABLE` part of hello statement.</span></span> <span data-ttu-id="d1135-145">Merhaba kimlik işlevi hello kullanamazsınız `SELECT` hello CTAS bir parçası.</span><span class="sxs-lookup"><span data-stu-id="d1135-145">You also can't use hello IDENTITY function in hello `SELECT` part of hello CTAS.</span></span> <span data-ttu-id="d1135-146">toopopulate bir tablo, gereksinim duyduğunuz toouse `CREATE TABLE` toodefine hello tablo arkasından `INSERT..SELECT` toopopulate onu.</span><span class="sxs-lookup"><span data-stu-id="d1135-146">toopopulate a table, you need toouse `CREATE TABLE` toodefine hello table followed by `INSERT..SELECT` toopopulate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="d1135-147">Açıkça değerleri bir kimlik sütununa ekleme</span><span class="sxs-lookup"><span data-stu-id="d1135-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="d1135-148">SQL veri ambarı destekleyen `SET IDENTITY_INSERT <your table> ON|OFF` sözdizimi.</span><span class="sxs-lookup"><span data-stu-id="d1135-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="d1135-149">Merhaba kimlik sütununa Bu sözdizimi tooexplicitly Ekle değerlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1135-149">You can use this syntax tooexplicitly insert values into hello IDENTITY column.</span></span>

<span data-ttu-id="d1135-150">Toouse önceden tanımlanmış negatif belirli kendi boyutlarını satır değerleri gibi çok sayıda veri modelers.</span><span class="sxs-lookup"><span data-stu-id="d1135-150">Many data modelers like toouse predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="d1135-151">Merhaba -1 veya "Bilinmeyen bir üyeye" satır örneğidir.</span><span class="sxs-lookup"><span data-stu-id="d1135-151">An example is hello -1 or "unknown member" row.</span></span> 

<span data-ttu-id="d1135-152">Merhaba sonraki komut dosyası nasıl tooexplicitly eklemek bu satır KÜMESİ IDENTITY_INSERT kullanarak gösterir:</span><span class="sxs-lookup"><span data-stu-id="d1135-152">hello next script shows how tooexplicitly add this row by using SET IDENTITY_INSERT:</span></span>

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

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="d1135-153">KİMLİĞİNE sahip bir tabloya veri yükleme</span><span class="sxs-lookup"><span data-stu-id="d1135-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="d1135-154">Merhaba kimlik özelliği Hello varlığını bazı etkileri tooyour veri yükleme koduna sahip.</span><span class="sxs-lookup"><span data-stu-id="d1135-154">hello presence of hello IDENTITY property has some implications tooyour data-loading code.</span></span> <span data-ttu-id="d1135-155">Bu bölüm kimliği kullanarak verileri tablolara yüklemek için bazı temel düzenlerden vurgular.</span><span class="sxs-lookup"><span data-stu-id="d1135-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="d1135-156">PolyBase ile veri yükleyin</span><span class="sxs-lookup"><span data-stu-id="d1135-156">Load data with PolyBase</span></span>
<span data-ttu-id="d1135-157">bir tabloya tooload veri ve kimliği kullanarak bir yedek anahtar oluşturmak, hello tablo oluşturmayı ve ardından Ekle... Seç veya Ekle... DEĞERLERİ tooperform hello yük.</span><span class="sxs-lookup"><span data-stu-id="d1135-157">tooload data into a table and generate a surrogate key by using IDENTITY, create hello table and then use INSERT..SELECT or INSERT..VALUES tooperform hello load.</span></span>

<span data-ttu-id="d1135-158">Merhaba aşağıdaki örnek hello temel düzeni vurgular:</span><span class="sxs-lookup"><span data-stu-id="d1135-158">hello following example highlights hello basic pattern:</span></span>
 
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

--Use INSERT..SELECT toopopulate hello table from an external table
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
> <span data-ttu-id="d1135-159">Olası toouse değil `CREATE TABLE AS SELECT` şu anda verileri bir kimlik sütunu olan bir tabloya yüklenirken.</span><span class="sxs-lookup"><span data-stu-id="d1135-159">It's not possible toouse `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="d1135-160">Merhaba toplu kopyalama programı (BCP) aracını kullanarak veri yükleme ile ilgili daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="d1135-160">For more information on loading data by using hello bulk copy program (BCP) tool, see hello following articles:</span></span>

- <span data-ttu-id="d1135-161">[PolyBase ile yükleme][]</span><span class="sxs-lookup"><span data-stu-id="d1135-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="d1135-162">[PolyBase en iyi uygulamalar][]</span><span class="sxs-lookup"><span data-stu-id="d1135-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="d1135-163">BCP ile veri yükleme</span><span class="sxs-lookup"><span data-stu-id="d1135-163">Load data with BCP</span></span>
<span data-ttu-id="d1135-164">BCP, SQL Data Warehouse'a tooload veri kullanabileceğiniz bir komut satırı aracıdır.</span><span class="sxs-lookup"><span data-stu-id="d1135-164">BCP is a command-line tool that you can use tooload data into SQL Data Warehouse.</span></span> <span data-ttu-id="d1135-165">Parametrelerinden biri (-E) denetimleri hello BCP davranışını verileri bir kimlik sütunu olan bir tabloya yüklenirken.</span><span class="sxs-lookup"><span data-stu-id="d1135-165">One of its parameters (-E) controls hello behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="d1135-166">-E belirtildiğinde, hello sütun için hello giriş dosyasındaki KİMLİKLE tutulan hello değerleri korunur.</span><span class="sxs-lookup"><span data-stu-id="d1135-166">When -E is specified, hello values held in hello input file for hello column with IDENTITY are retained.</span></span> <span data-ttu-id="d1135-167">-E ise *değil* hello bu sütundaki değerleri yoksayılır belirtilen.</span><span class="sxs-lookup"><span data-stu-id="d1135-167">If -E is *not* specified, then hello values in this column are ignored.</span></span> <span data-ttu-id="d1135-168">Merhaba kimlik sütunu dahil edilmezse, hello veriler normal olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d1135-168">If hello identity column is not included, then hello data is loaded as normal.</span></span> <span data-ttu-id="d1135-169">Merhaba değerleri toohello artırma ve çekirdek İlkesi hello özelliğinin göre oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d1135-169">hello values are generated according toohello increment and seed policy of hello property.</span></span>

<span data-ttu-id="d1135-170">BCP kullanarak veri yükleme ile ilgili daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="d1135-170">For more information on loading data by using BCP, see hello following articles:</span></span>

- <span data-ttu-id="d1135-171">[BCP ile yükleme][]</span><span class="sxs-lookup"><span data-stu-id="d1135-171">[Load with BCP][]</span></span>
- <span data-ttu-id="d1135-172">[BCP MSDN'de][]</span><span class="sxs-lookup"><span data-stu-id="d1135-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="d1135-173">Katalog görünümleri</span><span class="sxs-lookup"><span data-stu-id="d1135-173">Catalog views</span></span>
<span data-ttu-id="d1135-174">SQL veri ambarı destekleyen hello `sys.identity_columns` Katalog görünümü.</span><span class="sxs-lookup"><span data-stu-id="d1135-174">SQL Data Warehouse supports hello `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="d1135-175">Bu görünüm, kullanılan tooidentify hello kimlik özelliğine sahip bir sütun olabilir.</span><span class="sxs-lookup"><span data-stu-id="d1135-175">This view can be used tooidentify a column that has hello IDENTITY property.</span></span>

<span data-ttu-id="d1135-176">Bu örnek hello veritabanı şeması daha iyi anlamak toohelp gösterir nasıl toointegrate `sys.identity_columns` diğer sistem Katalog görünümleri ile:</span><span class="sxs-lookup"><span data-stu-id="d1135-176">toohelp you better understand hello database schema, this example shows how toointegrate `sys.identity_columns` with other system catalog views:</span></span>

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

## <a name="limitations"></a><span data-ttu-id="d1135-177">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="d1135-177">Limitations</span></span>
<span data-ttu-id="d1135-178">Merhaba kimlik özelliği senaryoları aşağıdaki hello kullanılamaz:</span><span class="sxs-lookup"><span data-stu-id="d1135-178">hello IDENTITY property can't be used in hello following scenarios:</span></span>
- <span data-ttu-id="d1135-179">Burada hello sütun veri türü tamsayı veya büyük tamsayı değil</span><span class="sxs-lookup"><span data-stu-id="d1135-179">Where hello column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="d1135-180">Merhaba sütun hello dağıtım anahtarı da olduğu</span><span class="sxs-lookup"><span data-stu-id="d1135-180">Where hello column is also hello distribution key</span></span>
- <span data-ttu-id="d1135-181">Merhaba tablosu bir dış tablo olduğu</span><span class="sxs-lookup"><span data-stu-id="d1135-181">Where hello table is an external table</span></span> 

<span data-ttu-id="d1135-182">ilgili işlevleri aşağıdaki hello SQL veri ambarı'nda desteklenmez:</span><span class="sxs-lookup"><span data-stu-id="d1135-182">hello following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="d1135-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="d1135-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="d1135-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="d1135-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="d1135-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="d1135-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="d1135-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="d1135-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="d1135-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="d1135-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="d1135-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="d1135-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="d1135-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="d1135-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="d1135-190">Görevler</span><span class="sxs-lookup"><span data-stu-id="d1135-190">Tasks</span></span>

<span data-ttu-id="d1135-191">Bu bölümde bazı örnek kod, kimlik sütunu ile çalışırken tooperform ortak görevleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1135-191">This section provides some sample code you can use tooperform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="d1135-192">Sütun C1 hello kimlik görevleri aşağıdaki tüm hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="d1135-192">Column C1 is hello IDENTITY in all hello following tasks.</span></span>
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a><span data-ttu-id="d1135-193">Bir tablo için ayrılan hello en yüksek değeri Bul</span><span class="sxs-lookup"><span data-stu-id="d1135-193">Find hello highest allocated value for a table</span></span>
<span data-ttu-id="d1135-194">Kullanım hello `MAX()` işlev dağıtılmış bir tablo için ayrılan toodetermine hello en yüksek değer:</span><span class="sxs-lookup"><span data-stu-id="d1135-194">Use hello `MAX()` function toodetermine hello highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a><span data-ttu-id="d1135-195">Merhaba çekirdek ve Artım Merhaba kimlik özelliği Bul</span><span class="sxs-lookup"><span data-stu-id="d1135-195">Find hello seed and increment for hello IDENTITY property</span></span>
<span data-ttu-id="d1135-196">Sorgu aşağıdaki hello kullanarak bir tablo için hello Katalog görünümleri toodiscover hello kimlik artırma ve çekirdek yapılandırma değerlerini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d1135-196">You can use hello catalog views toodiscover hello identity increment and seed configuration values for a table by using hello following query:</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="d1135-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d1135-197">Next steps</span></span>

* <span data-ttu-id="d1135-198">tablolar, geliştirme hakkında daha fazla toolearn bkz [tablo genel bakışı][Overview], [tablo veri türleri][Data Types], [bir tabloDağıt] [ Distribute], [Tablo dizin][Index], [tablo bölüm][Partition], ve [ Geçici tablolara][Temporary].</span><span class="sxs-lookup"><span data-stu-id="d1135-198">toolearn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="d1135-199">En iyi uygulamalar hakkında daha fazla bilgi için bkz: [SQL veri ambarı en iyi yöntemler][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="d1135-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

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

[BCP ile yükleme]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[PolyBase ile yükleme]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[PolyBase en iyi uygulamalar]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[BCP MSDN'de]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
