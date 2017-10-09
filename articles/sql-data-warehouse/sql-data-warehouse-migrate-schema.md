---
title: "aaaMigrate, şema tooSQL veri ambarı | Microsoft Docs"
description: "Çözümleri geliştirmek için şema tooAzure SQL Data Warehouse geçirmek için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a><span data-ttu-id="e640d-103">Şemalar tooSQL veri ambarına geçirme</span><span class="sxs-lookup"><span data-stu-id="e640d-103">Migrate your schemas tooSQL Data Warehouse</span></span>
<span data-ttu-id="e640d-104">SQL şemaları tooSQL veri ambarı geçirmek için yönergeler.</span><span class="sxs-lookup"><span data-stu-id="e640d-104">Guidance for migrating your SQL schemas tooSQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="e640d-105">Şema geçişinizi planlayın</span><span class="sxs-lookup"><span data-stu-id="e640d-105">Plan your schema migration</span></span>

<span data-ttu-id="e640d-106">Geçiş planlıyorsanız hello görmeniz [tablo genel bakışı] [ table overview] toobecome istatistikleri, dağıtım, bölümlendirme ve dizin oluşturma gibi tablo tasarım konuları hakkında bilgi sahibi.</span><span class="sxs-lookup"><span data-stu-id="e640d-106">As you plan a migration, see hello [table overview][table overview] toobecome familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="e640d-107">Ayrıca bazı listeler [desteklenmeyen tablo özellikleri] [ unsupported table features] ve bunların geçici çözümleri.</span><span class="sxs-lookup"><span data-stu-id="e640d-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a><span data-ttu-id="e640d-108">Kullanıcı tanımlı şemaları tooconsolidate veritabanları kullanın</span><span class="sxs-lookup"><span data-stu-id="e640d-108">Use user-defined schemas tooconsolidate databases</span></span>

<span data-ttu-id="e640d-109">Var olan İş yükünüzün büyük olasılıkla birden fazla veritabanı var.</span><span class="sxs-lookup"><span data-stu-id="e640d-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="e640d-110">Örneğin, bir SQL Server veri ambarı Hazırlama veritabanı, veri ambarı veritabanı ve bazı veri reyonu veritabanı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="e640d-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="e640d-111">Bu topolojide, her veritabanı ayrı bir iş yükü ayrı güvenlik ilkeleriyle birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="e640d-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="e640d-112">Bunun aksine, SQL Data Warehouse hello tüm veri ambarı iş yükü bir veritabanı içinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="e640d-112">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="e640d-113">Veritabanı birleştirmeler izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="e640d-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="e640d-114">Bu nedenle, SQL Data Warehouse hello bir veritabanı içinde depolanan hello veri ambarı toobe tarafından kullanılan bütün tablolar bekliyor.</span><span class="sxs-lookup"><span data-stu-id="e640d-114">Therefore, SQL Data Warehouse expects all tables used by hello data warehouse toobe stored within hello one database.</span></span>

<span data-ttu-id="e640d-115">Kullanıcı tanımlı şemaları tooconsolidate kullanarak mevcut İş yükünüzün bir veritabanına öneririz.</span><span class="sxs-lookup"><span data-stu-id="e640d-115">We recommend using user-defined schemas tooconsolidate your existing workload into one database.</span></span> <span data-ttu-id="e640d-116">Örnekler için bkz: [kullanıcı tanımlı şemaları](sql-data-warehouse-develop-user-defined-schemas.md)</span><span class="sxs-lookup"><span data-stu-id="e640d-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="e640d-117">Uyumlu veri türleri kullanın</span><span class="sxs-lookup"><span data-stu-id="e640d-117">Use compatible data types</span></span>
<span data-ttu-id="e640d-118">SQL Data Warehouse ile uyumlu olan veri türleri toobe değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e640d-118">Modify your data types toobe compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="e640d-119">Desteklenen ve desteklenmeyen veri türlerinin listesi için bkz: [veri türleri][data types].</span><span class="sxs-lookup"><span data-stu-id="e640d-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="e640d-120">Bu konuda desteklenmeyen hello türleri için geçici çözümler sunar.</span><span class="sxs-lookup"><span data-stu-id="e640d-120">That topic gives workarounds for hello unsupported types.</span></span> <span data-ttu-id="e640d-121">Ayrıca bir sorgu SQL veri ambarı'nda desteklenmeyen tooidentify varolan türler sağlar.</span><span class="sxs-lookup"><span data-stu-id="e640d-121">It also provides a query tooidentify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="e640d-122">Satır boyutu en aza indir</span><span class="sxs-lookup"><span data-stu-id="e640d-122">Minimize row size</span></span>
<span data-ttu-id="e640d-123">En iyi performans için tablolarınızı hello satır uzunluğu en aza indirin.</span><span class="sxs-lookup"><span data-stu-id="e640d-123">For best performance, minimize hello row length of your tables.</span></span> <span data-ttu-id="e640d-124">Daha kısa satır uzunlukları toobetter performans neden olduğundan, çalışan hello en küçük veri türleri, verileriniz için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e640d-124">Since shorter row lengths lead toobetter performance, use hello smallest data types that work for your data.</span></span> 

<span data-ttu-id="e640d-125">Tablo satır genişliğini için PolyBase 1 MB sınırı vardır.</span><span class="sxs-lookup"><span data-stu-id="e640d-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="e640d-126">PolyBase ile SQL veri ambarında tooload veri planlıyorsanız, 1 MB'tan az, tablolar toohave en fazla satır genişliğini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e640d-126">If you plan tooload data into SQL Data Warehouse with PolyBase, update your tables toohave maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a><span data-ttu-id="e640d-127">Merhaba dağıtım seçeneğini belirtin</span><span class="sxs-lookup"><span data-stu-id="e640d-127">Specify hello distribution option</span></span>
<span data-ttu-id="e640d-128">SQL veri ambarı dağıtılmış bir veritabanı sistemidir.</span><span class="sxs-lookup"><span data-stu-id="e640d-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="e640d-129">Her tablo dağıtılmış veya hello işlem düğümleri arasında çoğaltılan.</span><span class="sxs-lookup"><span data-stu-id="e640d-129">Each table is distributed or replicated across hello Compute nodes.</span></span> <span data-ttu-id="e640d-130">Nasıl toodistribute hello veri belirtmenize olanak sağlar. bir tablo seçeneği yoktur.</span><span class="sxs-lookup"><span data-stu-id="e640d-130">There's a table option that lets you specify how toodistribute hello data.</span></span> <span data-ttu-id="e640d-131">Merhaba çoğaltılan, hepsini, seçimlerdir veya karma dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="e640d-131">hello choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="e640d-132">Her Artıları ve eksileri vardır.</span><span class="sxs-lookup"><span data-stu-id="e640d-132">Each has pros and cons.</span></span> <span data-ttu-id="e640d-133">Merhaba dağıtım seçeneği belirtmezseniz, SQL Data Warehouse hepsini hello varsayılan olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="e640d-133">If you don't specify hello distribution option, SQL Data Warehouse will use round-robin as hello default.</span></span>

- <span data-ttu-id="e640d-134">Hepsini hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="e640d-134">Round-robin is hello default.</span></span> <span data-ttu-id="e640d-135">Merhaba basit toouse olan ve hello verileri kadar hızlı yükler, ancak sorgu performansını yavaşlatır veri taşıma birleştirmeler gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e640d-135">It is hello simplest toouse, and loads hello data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="e640d-136">Her işlem düğümünde Merhaba tablonun kopyasını bir çoğaltılmış depolar.</span><span class="sxs-lookup"><span data-stu-id="e640d-136">Replicated stores a copy of hello table on each Compute node.</span></span> <span data-ttu-id="e640d-137">Çoğaltılmış tablolar kullanıcı olduklarından, veri taşıma birleşimler ve Toplamalar için gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="e640d-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="e640d-138">Bunlar ek depolama alanı gerektirir ve bu nedenle daha küçük tablolar için en iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="e640d-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="e640d-139">Dağıtılmış karma hello satırları karma işlevi ile tüm hello düğümler arasında dağıtır.</span><span class="sxs-lookup"><span data-stu-id="e640d-139">Hash distributed distributes hello rows across all hello nodes via a hash function.</span></span> <span data-ttu-id="e640d-140">Tasarlanmış tooprovide yüksek sorgu performansı büyük tablolarda olduğundan dağıtılmış karma tabloları hello Kalp SQL veri ambarı ' dir.</span><span class="sxs-lookup"><span data-stu-id="e640d-140">Hash distributed tables are hello heart of SQL Data Warehouse since they are designed tooprovide high query performance on large tables.</span></span> <span data-ttu-id="e640d-141">Bu seçenek bazı planlama tooselect hello en iyi sütun hangi toodistribute hello verileri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e640d-141">This option requires some planning tooselect hello best column on which toodistribute hello data.</span></span> <span data-ttu-id="e640d-142">İlk kez hello en iyi sütun hello seçmezseniz, ancak, kolayca hello verileri farklı bir sütun üzerinde yeniden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e640d-142">However, if you don't choose hello best column hello first time, you can easily re-distribute hello data on a different column.</span></span> 

<span data-ttu-id="e640d-143">toochoose hello her tablo için en iyi dağıtım seçeneği bkz [dağıtılmış tabloları](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="e640d-143">toochoose hello best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="e640d-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e640d-144">Next steps</span></span>
<span data-ttu-id="e640d-145">Veritabanı şeması tooSQL veri ambarı başarıyla geçirdikten sonra aşağıdaki makaleler hello tooone devam edin:</span><span class="sxs-lookup"><span data-stu-id="e640d-145">Once you have successfully migrated your database schema tooSQL Data Warehouse, proceed tooone of hello following articles:</span></span>

* <span data-ttu-id="e640d-146">[Verilerinizi geçirme][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="e640d-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="e640d-147">[Kodunuzu geçirme][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="e640d-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="e640d-148">SQL veri ambarı en iyi uygulamalar hakkında daha fazla bilgi için bkz: Merhaba [en iyi uygulamalar] [ best practices] makalesi.</span><span class="sxs-lookup"><span data-stu-id="e640d-148">For more about SQL Data Warehouse best practices, see hello [best practices][best practices] article.</span></span>

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
