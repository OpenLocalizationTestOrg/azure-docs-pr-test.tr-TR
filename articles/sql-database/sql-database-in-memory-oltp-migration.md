---
title: "aaaIn bellek içi OLTP artırır SQL işlemlerinin perf | Microsoft Docs"
description: "Varolan bir SQL veritabanında adopt bellek içi OLTP tooimprove işlem performansı."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a><span data-ttu-id="caaea-103">Kullanım bellek içi OLTP tooimprove SQL veritabanında, uygulama performansı</span><span class="sxs-lookup"><span data-stu-id="caaea-103">Use In-Memory OLTP tooimprove your application performance in SQL Database</span></span>
<span data-ttu-id="caaea-104">[Bellek içi OLTP](sql-database-in-memory.md) kullanılan tooimprove hello performansını işlem, veri alımı ve geçici veri senaryoları olabilir [Premium](sql-database-service-tiers.md) artırma olmadan Azure SQL veritabanları hello fiyatlandırma katmanı.</span><span class="sxs-lookup"><span data-stu-id="caaea-104">[In-Memory OLTP](sql-database-in-memory.md) can be used tooimprove hello performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing hello pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="caaea-105">Bilgi nasıl [çekirdek % 70'sql Database tarafından DTU düşürürken anahtar veritabanının iş yükü Katlar](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="caaea-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="caaea-106">Mevcut veritabanını bu adımları tooadopt bellek içi OLTP izleyin.</span><span class="sxs-lookup"><span data-stu-id="caaea-106">Follow these steps tooadopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="caaea-107">1. adım: bir Premium veritabanı kullandığınızdan emin olun</span><span class="sxs-lookup"><span data-stu-id="caaea-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="caaea-108">Bellek içi OLTP yalnızca Premium veritabanlarında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="caaea-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="caaea-109">Bellek içi hello sonucudur 1 döndürülürse desteklenir (0):</span><span class="sxs-lookup"><span data-stu-id="caaea-109">In-Memory is supported if hello returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="caaea-110">*XTP* anlamına gelir *aşırı işlem işleme*</span><span class="sxs-lookup"><span data-stu-id="caaea-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a><span data-ttu-id="caaea-111">2. adım: nesneleri toomigrate tooIn-belleği tanımlayan OLTP</span><span class="sxs-lookup"><span data-stu-id="caaea-111">Step 2: Identify objects toomigrate tooIn-Memory OLTP</span></span>
<span data-ttu-id="caaea-112">SSMS içeren bir **işlem Performans Analizi genel bakış** etkin bir iş yükü olan bir veritabanına karşı çalıştırabilirsiniz rapor.</span><span class="sxs-lookup"><span data-stu-id="caaea-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="caaea-113">Merhaba raporu, tablolar ve geçiş adaylar saklı yordamlar tanımlar tooIn bellek içi OLTP.</span><span class="sxs-lookup"><span data-stu-id="caaea-113">hello report identifies tables and stored procedures that are candidates for migration tooIn-Memory OLTP.</span></span>

<span data-ttu-id="caaea-114">SSMS toogenerate hello raporu:</span><span class="sxs-lookup"><span data-stu-id="caaea-114">In SSMS, toogenerate hello report:</span></span>

* <span data-ttu-id="caaea-115">Merhaba, **Nesne Gezgini**, veritabanı düğümünü sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="caaea-115">In hello **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="caaea-116">Tıklatın **raporları** > **standart raporları** > **işlem Performans Analizi genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="caaea-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="caaea-117">Daha fazla bilgi için bkz: [belirleme bir tablo veya saklı yordam gereken olması bağlantı noktalı tooIn bellek içi OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="caaea-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="caaea-118">3. adım: karşılaştırılabilir test veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="caaea-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="caaea-119">Veritabanınızı Hello rapor gösterir varsayalım olmaktan için yararlı bir tablo tooa bellek için iyileştirilmiş tablo dönüştürülen.</span><span class="sxs-lookup"><span data-stu-id="caaea-119">Suppose hello report indicates your database has a table that would benefit from being converted tooa memory-optimized table.</span></span> <span data-ttu-id="caaea-120">Test ederek tooconfirm hello göstergesi ilk sınamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="caaea-120">We recommend that you first test tooconfirm hello indication by testing.</span></span>

<span data-ttu-id="caaea-121">Üretim veritabanınız test kopyasını gerekir.</span><span class="sxs-lookup"><span data-stu-id="caaea-121">You need a test copy of your production database.</span></span> <span data-ttu-id="caaea-122">Merhaba test veritabanı olmalıdır hello aynı katmanı düzeyini üretim veritabanınız olarak hizmet.</span><span class="sxs-lookup"><span data-stu-id="caaea-122">hello test database should be at hello same service tier level as your production database.</span></span>

<span data-ttu-id="caaea-123">Test, tooease test veritabanınızı gibi ince ayar:</span><span class="sxs-lookup"><span data-stu-id="caaea-123">tooease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="caaea-124">SSMS kullanarak toohello test veritabanı bağlanın.</span><span class="sxs-lookup"><span data-stu-id="caaea-124">Connect toohello test database by using SSMS.</span></span>
2. <span data-ttu-id="caaea-125">tooavoid gerek WITH (SNAPSHOT) seçeneği sorgularda Merhaba, hello veritabanı seçeneği T-SQL deyimi aşağıdaki hello gösterilen şekilde ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="caaea-125">tooavoid needing hello WITH (SNAPSHOT) option in queries, set hello database option as shown in hello following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="caaea-126">4. adım: tabloları geçirme</span><span class="sxs-lookup"><span data-stu-id="caaea-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="caaea-127">Oluşturmalı ve bellek için iyileştirilmiş kopyasını doldurmak Merhaba tablonun tootest istiyor.</span><span class="sxs-lookup"><span data-stu-id="caaea-127">You must create and populate a memory-optimized copy of hello table you want tootest.</span></span> <span data-ttu-id="caaea-128">Kullanarak oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="caaea-128">You can create it by using either:</span></span>

* <span data-ttu-id="caaea-129">Merhaba SSMS kullanışlı belleği en iyi duruma getirme sihirbazında.</span><span class="sxs-lookup"><span data-stu-id="caaea-129">hello handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="caaea-130">El ile T-SQL.</span><span class="sxs-lookup"><span data-stu-id="caaea-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="caaea-131">Belleği en iyi duruma getirme Sihirbazı'nda SSMS</span><span class="sxs-lookup"><span data-stu-id="caaea-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="caaea-132">toouse bu geçiş seçeneği:</span><span class="sxs-lookup"><span data-stu-id="caaea-132">toouse this migration option:</span></span>

1. <span data-ttu-id="caaea-133">Toohello test veritabanı SSMS ile bağlanma.</span><span class="sxs-lookup"><span data-stu-id="caaea-133">Connect toohello test database with SSMS.</span></span>
2. <span data-ttu-id="caaea-134">Merhaba, **Object Explorer**hello tabloyu sağ tıklatın ve ardından **belleği en iyi duruma getirme Danışmanı**.</span><span class="sxs-lookup"><span data-stu-id="caaea-134">In hello **Object Explorer**, right-click on hello table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="caaea-135">Merhaba **tablo bellek iyileştirici Danışmanı** Sihirbazı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="caaea-135">hello **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="caaea-136">Başlangıç Sihirbazı'nda tıklatın **geçiş doğrulama** (veya hello **sonraki** düğmesi) Merhaba tablonun herhangi varsa toosee desteklenmeyen bellek için iyileştirilmiş tablolarda desteklenmeyen özellikler.</span><span class="sxs-lookup"><span data-stu-id="caaea-136">In hello wizard, click **Migration validation** (or hello **Next** button) toosee if hello table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="caaea-137">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="caaea-137">For more information, see:</span></span>
   
   * <span data-ttu-id="caaea-138">Merhaba *belleği en iyi duruma getirme denetim listesi* içinde [belleği en iyi duruma getirme Danışmanı](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="caaea-138">hello *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="caaea-139">[Bellek içi OLTP tarafından desteklenmeyen transact-SQL yapıları](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="caaea-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="caaea-140">[Geçirme tooIn bellek içi OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="caaea-140">[Migrating tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="caaea-141">Merhaba tablonun desteklenmeyen özellikleri yok varsa hello Danışmanı hello gerçek şema ve veri geçişi sizin için gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="caaea-141">If hello table has no unsupported features, hello advisor can perform hello actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="caaea-142">El ile T-SQL</span><span class="sxs-lookup"><span data-stu-id="caaea-142">Manual T-SQL</span></span>
<span data-ttu-id="caaea-143">toouse bu geçiş seçeneği:</span><span class="sxs-lookup"><span data-stu-id="caaea-143">toouse this migration option:</span></span>

1. <span data-ttu-id="caaea-144">Tooyour test veritabanı SSMS (veya benzer bir yardımcı programını) kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="caaea-144">Connect tooyour test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="caaea-145">Merhaba tam T-SQL komut dosyası, tablo ve dizinlerini edinin.</span><span class="sxs-lookup"><span data-stu-id="caaea-145">Obtain hello complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="caaea-146">SSMS, tablo düğümünü sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="caaea-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="caaea-147">Tıklatın **komut tablo olarak** > **için oluşturun** > **yeni sorgu penceresinde**.</span><span class="sxs-lookup"><span data-stu-id="caaea-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="caaea-148">WITH Hello komut penceresinde ekleyin (memory_optımızed = ON) toohello CREATE TABLE deyimi.</span><span class="sxs-lookup"><span data-stu-id="caaea-148">In hello script window, add WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE statement.</span></span>
4. <span data-ttu-id="caaea-149">Bir kümelenmiş dizin ise tooNONCLUSTERED değiştirin.</span><span class="sxs-lookup"><span data-stu-id="caaea-149">If there is a CLUSTERED index, change it tooNONCLUSTERED.</span></span>
5. <span data-ttu-id="caaea-150">Merhaba var olan tablo SP_RENAME kullanarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="caaea-150">Rename hello existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="caaea-151">Düzenlenen CREATE TABLE kodunuzu çalıştırarak Hello yeni bellek için iyileştirilmiş Merhaba tablonun kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="caaea-151">Create hello new memory-optimized copy of hello table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="caaea-152">Merhaba veri tooyour bellek için iyileştirilmiş Tablo Ekle kullanarak Kopyala... SEÇİN * İÇİNE:</span><span class="sxs-lookup"><span data-stu-id="caaea-152">Copy hello data tooyour memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="caaea-153">(İsteğe bağlı) 5. adım: saklı yordamları geçirme</span><span class="sxs-lookup"><span data-stu-id="caaea-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="caaea-154">Merhaba bellek içi özelliği, Gelişmiş performans için bir saklı yordam de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="caaea-154">hello In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="caaea-155">Yerel koda derlenmiş saklı yordamlar ile ilgili önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="caaea-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="caaea-156">Yerel koda derlenmiş bir saklı yordam aşağıdaki seçenekler, T-SQL WITH yan tümcesi'hello olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="caaea-156">A natively compiled stored procedure must have hello following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="caaea-157">NATIVE_COMPILATION ÖĞESİNİ</span><span class="sxs-lookup"><span data-stu-id="caaea-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="caaea-158">Şemaya Bağlama: saklı yordam hello anlamı tabloların sütun tanımlarını hello saklı yordamı bırakma sürece hello saklı yordamı etkileyecek herhangi bir şekilde değiştirilmiş sahip olamaz.</span><span class="sxs-lookup"><span data-stu-id="caaea-158">SCHEMABINDING: meaning tables that hello stored procedure cannot have their column definitions changed in any way that would affect hello stored procedure, unless you drop hello stored procedure.</span></span>

<span data-ttu-id="caaea-159">Yerel bir modül biri büyük kullanmalısınız [ATOMİK bloklar](http://msdn.microsoft.com/library/dn452281.aspx) işlem yönetimi.</span><span class="sxs-lookup"><span data-stu-id="caaea-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="caaea-160">Herhangi bir rol veya geri alma işlemi için açık BEGIN TRANSACTION yok.</span><span class="sxs-lookup"><span data-stu-id="caaea-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="caaea-161">Kodunuzu bir iş kuralı ihlal algılarsa, hello atomik blok sonlandırabilir bir [THROW](http://msdn.microsoft.com/library/ee677615.aspx) deyimi.</span><span class="sxs-lookup"><span data-stu-id="caaea-161">If your code detects a violation of a business rule, it can terminate hello atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="caaea-162">İçin tipik CREATE PROCEDURE yerel koda derlenmiş</span><span class="sxs-lookup"><span data-stu-id="caaea-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="caaea-163">Genellikle hello T-SQL toocreate yerel koda derlenmiş bir saklı yordam benzer toohello şablonu aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="caaea-163">Typically hello T-SQL toocreate a natively compiled stored procedure is similar toohello following template:</span></span>

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* <span data-ttu-id="caaea-164">Merhaba TRANSACTION_ISOLATION_LEVEL hello en yaygın değeri hello yerel koda derlenmiş saklı yordamı anlık görüntüsüdür.</span><span class="sxs-lookup"><span data-stu-id="caaea-164">For hello TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is hello most common value for hello natively compiled stored procedure.</span></span> <span data-ttu-id="caaea-165">Ancak, bir alt kümesini hello diğer değerleri de desteklenir:</span><span class="sxs-lookup"><span data-stu-id="caaea-165">However,  a subset of hello other values are also supported:</span></span>
  
  * <span data-ttu-id="caaea-166">YİNELENEBİLİR OKUMA</span><span class="sxs-lookup"><span data-stu-id="caaea-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="caaea-167">SERİ HALE GETİRİLEBİLİR</span><span class="sxs-lookup"><span data-stu-id="caaea-167">SERIALIZABLE</span></span>
* <span data-ttu-id="caaea-168">Merhaba dil değerini hello sys.languages görünümünde mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="caaea-168">hello LANGUAGE value must be present in hello sys.languages view.</span></span>

### <a name="how-toomigrate-a-stored-procedure"></a><span data-ttu-id="caaea-169">Nasıl toomigrate bir saklı yordam</span><span class="sxs-lookup"><span data-stu-id="caaea-169">How toomigrate a stored procedure</span></span>
<span data-ttu-id="caaea-170">Merhaba geçiş adımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="caaea-170">hello migration steps are:</span></span>

1. <span data-ttu-id="caaea-171">Merhaba CREATE PROCEDURE betik toohello normal yorumlanan saklı yordam edinin.</span><span class="sxs-lookup"><span data-stu-id="caaea-171">Obtain hello CREATE PROCEDURE script toohello regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="caaea-172">Kendi üstbilgi toomatch hello önceki şablonu yeniden yazın.</span><span class="sxs-lookup"><span data-stu-id="caaea-172">Rewrite its header toomatch hello previous template.</span></span>
3. <span data-ttu-id="caaea-173">Merhaba saklı yordamı T-SQL kodunu yerel koda derlenmiş saklı yordamlar için desteklenmeyen herhangi bir özellik kullanıp kullanmadığını onaylaması.</span><span class="sxs-lookup"><span data-stu-id="caaea-173">Ascertain whether hello stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="caaea-174">Geçici Çözümler gerekirse uygulayın.</span><span class="sxs-lookup"><span data-stu-id="caaea-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="caaea-175">Ayrıntılar için bkz: [yerel olarak depolanan yordamlar derlenmiş geçiş sorunları](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="caaea-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="caaea-176">Merhaba eski saklı yordam SP_RENAME kullanarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="caaea-176">Rename hello old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="caaea-177">Veya yalnızca BIRAKILAMIYOR.</span><span class="sxs-lookup"><span data-stu-id="caaea-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="caaea-178">Düzenlenen oluşturma yordamı T-SQL betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="caaea-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="caaea-179">6. adım: İş yükünüzün testi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="caaea-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="caaea-180">Test veritabanınızdaki üretim veritabanınız çalıştıran benzer toohello iş yükü olan bir iş yükü çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="caaea-180">Run a workload in your test database that is similar toohello workload that runs in your production database.</span></span> <span data-ttu-id="caaea-181">Bu, tabloları ve saklı yordamlar için hello bellek içi özelliği kullanımınız tarafından elde hello performans kazancı ortaya çıkarır.</span><span class="sxs-lookup"><span data-stu-id="caaea-181">This should reveal hello performance gain achieved by your use of hello In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="caaea-182">Merhaba iş yükünün önemli öznitelikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="caaea-182">Major attributes of hello workload are:</span></span>

* <span data-ttu-id="caaea-183">Eşzamanlı bağlantı sayısı.</span><span class="sxs-lookup"><span data-stu-id="caaea-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="caaea-184">Okuma/yazma oranı.</span><span class="sxs-lookup"><span data-stu-id="caaea-184">Read/write ratio.</span></span>

<span data-ttu-id="caaea-185">tootailor ve çalışma hello test iş yükü, göz önünde bulundurun gösterilen hello kullanışlı ostress.exe aracını kullanarak [burada](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="caaea-185">tootailor and run hello test workload, consider using hello handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="caaea-186">hello testinizi çalıştırmak toominimize ağ gecikmesini hello veritabanının bulunduğu aynı Azure coğrafi bölge.</span><span class="sxs-lookup"><span data-stu-id="caaea-186">toominimize network latency, run your test in hello same Azure geographic region where hello database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="caaea-187">7. adım: Uygulama sonrası izleme</span><span class="sxs-lookup"><span data-stu-id="caaea-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="caaea-188">Bellek içi uygulamalarınızda üretim Hello performans etkisini izleme göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="caaea-188">Consider monitoring hello performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="caaea-189">[Bellek içi depolama izleme](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="caaea-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="caaea-190">Dinamik yönetim görünümlerini kullanarak Azure SQL Database’i izleme</span><span class="sxs-lookup"><span data-stu-id="caaea-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="caaea-191">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="caaea-191">Related links</span></span>
* [<span data-ttu-id="caaea-192">Bellek içi OLTP (bellek içi iyileştirme)</span><span class="sxs-lookup"><span data-stu-id="caaea-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="caaea-193">Giriş tooNatively derlenmiş saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="caaea-193">Introduction tooNatively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="caaea-194">Belleği en iyi duruma getirme Danışmanı</span><span class="sxs-lookup"><span data-stu-id="caaea-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

