---
title: "aaaMigrate, veri ambarı çözüm tooSQL | Microsoft Docs"
description: "Çözüm tooAzure SQL Data Warehouse platformunuz getiren Geçiş Kılavuzu."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a><span data-ttu-id="86cfd-103">SQL Data Warehouse, çözüm tooAzure geçirme</span><span class="sxs-lookup"><span data-stu-id="86cfd-103">Migrate your solution tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="86cfd-104">Ne var olan bir veritabanı çözümü tooAzure SQL veri ambarı geçiş konusuysa bakın.</span><span class="sxs-lookup"><span data-stu-id="86cfd-104">See what's involved in migrating an existing database solution tooAzure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="86cfd-105">İş yükünüzün profil</span><span class="sxs-lookup"><span data-stu-id="86cfd-105">Profile your workload</span></span>
<span data-ttu-id="86cfd-106">Geçirmeden önce SQL Data Warehouse hello doğru iş yükü çözümdür belirli toobe istiyor.</span><span class="sxs-lookup"><span data-stu-id="86cfd-106">Before migrating, you want toobe certain SQL Data Warehouse is hello right solution for your workload.</span></span> <span data-ttu-id="86cfd-107">SQL veri ambarı büyük veri tasarlanmış Dağıtılmış Sistem tooperform analytics ' dir.</span><span class="sxs-lookup"><span data-stu-id="86cfd-107">SQL Data Warehouse is a distributed system designed tooperform analytics on large data.</span></span>  <span data-ttu-id="86cfd-108">Geçirme tooSQL veri ambarı çok sabit toounderstand değildir ancak bazı zaman tooimplement sürebilir bazı tasarım değişiklikleri gerektirir.</span><span class="sxs-lookup"><span data-stu-id="86cfd-108">Migrating tooSQL Data Warehouse requires some design changes that are not too hard toounderstand but might take some time tooimplement.</span></span> <span data-ttu-id="86cfd-109">Bir kurumsal sınıf veri ambarı, İşletmenizde hello avantajları hello çabalara demektir.</span><span class="sxs-lookup"><span data-stu-id="86cfd-109">If your business requires an enterprise-class data warehouse, hello benefits are worth hello effort.</span></span> <span data-ttu-id="86cfd-110">Ancak, SQL Data Warehouse hello gücünü gerek duymuyorsanız, daha fazla uygun maliyetli toouse SQL Server veya Azure SQL veritabanı değil.</span><span class="sxs-lookup"><span data-stu-id="86cfd-110">However, if you don't need hello power of SQL Data Warehouse, it is more cost-effective toouse SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="86cfd-111">SQL veri ambarı kullanmayı olduğunda:</span><span class="sxs-lookup"><span data-stu-id="86cfd-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="86cfd-112">Bir veya daha fazla terabayt veri sahip</span><span class="sxs-lookup"><span data-stu-id="86cfd-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="86cfd-113">Büyük miktarlarda verinin toorun analytics planlama</span><span class="sxs-lookup"><span data-stu-id="86cfd-113">Plan toorun analytics on large amounts of data</span></span>
- <span data-ttu-id="86cfd-114">Merhaba özelliği tooscale işlem ve depolama gerekir</span><span class="sxs-lookup"><span data-stu-id="86cfd-114">Need hello ability tooscale compute and storage</span></span> 
- <span data-ttu-id="86cfd-115">Bunları gerekmediğinde duraklatma tarafından toosave maliyetleri işlem kaynaklarını istiyor.</span><span class="sxs-lookup"><span data-stu-id="86cfd-115">Want toosave costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="86cfd-116">SQL veri ambarı sahip işlem (gerçekleştirme OLTP) iş yükleri için kullanmayın:</span><span class="sxs-lookup"><span data-stu-id="86cfd-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="86cfd-117">Yüksek yoğunlukta okuma ve yazma işlemleri</span><span class="sxs-lookup"><span data-stu-id="86cfd-117">High frequency reads and writes</span></span>
- <span data-ttu-id="86cfd-118">Singleton çok sayıda seçer</span><span class="sxs-lookup"><span data-stu-id="86cfd-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="86cfd-119">Yüksek hacimli tek bir satır ekler</span><span class="sxs-lookup"><span data-stu-id="86cfd-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="86cfd-120">Satır satır işleme tarafından gerekiyor</span><span class="sxs-lookup"><span data-stu-id="86cfd-120">Row by row processing needs</span></span>
- <span data-ttu-id="86cfd-121">Uyumsuz biçimleri (JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="86cfd-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-hello-migration"></a><span data-ttu-id="86cfd-122">Merhaba geçişi planlama</span><span class="sxs-lookup"><span data-stu-id="86cfd-122">Plan hello migration</span></span>

<span data-ttu-id="86cfd-123">Var olan bir çözümü tooSQL veri ambarı toomigrate karar verdikten sonra başlarken önce önemli tooplan hello geçiş değil.</span><span class="sxs-lookup"><span data-stu-id="86cfd-123">Once you have decided toomigrate an existing solution tooSQL Data Warehouse, it is important tooplan hello migration before getting started.</span></span> 

<span data-ttu-id="86cfd-124">Planlama tek amacı, tablo şemalarını verilerinizi tooensure olduğunu ve kodunuzu SQL Data Warehouse ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="86cfd-124">One goal of planning is tooensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="86cfd-125">Bazı uyumluluk farklar toowork geçici geçerli sistem ve SQL Data Warehouse arasında vardır.</span><span class="sxs-lookup"><span data-stu-id="86cfd-125">There are some compatibility differences toowork around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="86cfd-126">Ayrıca, büyük miktarlarda veri tooAzure alır süresini geçirme.</span><span class="sxs-lookup"><span data-stu-id="86cfd-126">Plus, migrating large amounts of data tooAzure takes time.</span></span> <span data-ttu-id="86cfd-127">Dikkatli planlama veri tooAzure alma hızlandırır.</span><span class="sxs-lookup"><span data-stu-id="86cfd-127">Careful planning expedites getting your data tooAzure.</span></span> 

<span data-ttu-id="86cfd-128">Planlama, başka bir hedef çözümünüzü SQL veri ambarı hello yüksek sorgu performansı yararlanır ayarlamalar tooensure tooprovide tasarlanmış toomake tasarımdır.</span><span class="sxs-lookup"><span data-stu-id="86cfd-128">Another goal of planning is toomake design adjustments tooensure your solution takes advantage of hello high query performance SQL Data Warehouse is designed tooprovide.</span></span> <span data-ttu-id="86cfd-129">Veri ambarları ölçek tasarlama farklı tasarım desenleri tanıtır ve bu nedenle geleneksel yaklaşım her zaman hello en iyi değil.</span><span class="sxs-lookup"><span data-stu-id="86cfd-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always hello best.</span></span> <span data-ttu-id="86cfd-130">Geçişten sonra bazı tasarım ayarlamalar yapabilmenize rağmen daha erken hello işleminde değişiklik daha sonra zaman kaydeder.</span><span class="sxs-lookup"><span data-stu-id="86cfd-130">Although you can make some design adjustments after migration, making changes sooner in hello process will save time later.</span></span>

<span data-ttu-id="86cfd-131">tooperform başarılı bir geçiş, gereksinim duyduğunuz toomigrate, tablo şemalarını, kodunuz ve verileriniz.</span><span class="sxs-lookup"><span data-stu-id="86cfd-131">tooperform a successful migration, you need toomigrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="86cfd-132">Bu geçiş konuları hakkında yönergeler için bkz:</span><span class="sxs-lookup"><span data-stu-id="86cfd-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="86cfd-133">Şemalar geçirme</span><span class="sxs-lookup"><span data-stu-id="86cfd-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="86cfd-134">Kodunuzu geçirme</span><span class="sxs-lookup"><span data-stu-id="86cfd-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="86cfd-135">[Verilerinizi geçirme](sql-data-warehouse-migrate-data.md).</span><span class="sxs-lookup"><span data-stu-id="86cfd-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a><span data-ttu-id="86cfd-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="86cfd-136">Next steps</span></span>
<span data-ttu-id="86cfd-137">Hello kat (Müşteri danışma ekibi) blog yayımlama bazı harika SQL Data Warehouse yönergeler de vardır.</span><span class="sxs-lookup"><span data-stu-id="86cfd-137">hello CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="86cfd-138">Kendi makale bakalım [uygulamada geçiş veri tooAzure SQL Data Warehouse] [ Migrating data tooAzure SQL Data Warehouse in practice] geçiş hakkında ek yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="86cfd-138">Take a look at their article, [Migrating data tooAzure SQL Data Warehouse in practice][Migrating data tooAzure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
