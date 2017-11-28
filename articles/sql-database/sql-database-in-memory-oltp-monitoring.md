---
title: "aaaMonitor XTP bellek içi depolama | Microsoft Docs"
description: "Tahmin ve İzleyici XTP bellek içi depolama, kapasite kullanın; Kapasite hatayı 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="58519-103">Bellek içi OLTP Depolama Alanını izleme</span><span class="sxs-lookup"><span data-stu-id="58519-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="58519-104">Kullanırken [bellek içi OLTP](sql-database-in-memory.md), bellek için iyileştirilmiş tablolar ve Tablo değişkenlerinin verileri bellek içi OLTP depolamada yer alıyor.</span><span class="sxs-lookup"><span data-stu-id="58519-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="58519-105">Her Premium Hizmet katmanını hello belgelenen en fazla bir bellek içi OLTP depolama boyutuna sahip [SQL Database hizmet katmanları makale](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="58519-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="58519-106">Bu sınır aşılırsa sonra ekleme ve güncelleştirme işlemleri (hatası 41823 ile) başarısız olan başlayabilir.</span><span class="sxs-lookup"><span data-stu-id="58519-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="58519-107">Bu noktada tooeither delete veri tooreclaim belleğe ihtiyacınız veya hello performans katmanı veritabanınızın yükseltin.</span><span class="sxs-lookup"><span data-stu-id="58519-107">At that point you will need tooeither delete data tooreclaim memory, or upgrade hello performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a><span data-ttu-id="58519-108">Veri hello bellek içi depolama cap içinde uygun olup olmadığını belirleme</span><span class="sxs-lookup"><span data-stu-id="58519-108">Determine whether data will fit within hello in-memory storage cap</span></span>
<span data-ttu-id="58519-109">Merhaba depolama cap belirlemek: hello başvurun [SQL Database hizmet katmanları makale](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) hello depolama caps hello farklı Premium hizmet katmanı için.</span><span class="sxs-lookup"><span data-stu-id="58519-109">Determine hello storage cap: consult hello [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for hello storage caps of hello different Premium service tiers.</span></span>

<span data-ttu-id="58519-110">Bellek için iyileştirilmiş bir tablo çalışır için gereksinimleri aynı hello bellek tahmin şekilde SQL Server için Azure SQL veritabanı'nda yapar.</span><span class="sxs-lookup"><span data-stu-id="58519-110">Estimating memory requirements for a memory-optimized table works hello same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="58519-111">Birkaç dakika tooreview bu konuda ele [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="58519-111">Take a few minutes tooreview that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="58519-112">Merhaba tablosu ve tablo değişkeni satırları yanı sıra, dizinler, hello en fazla kullanıcı veri boyutu doğru saymak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="58519-112">Note that hello table and table variable rows, as well as indexes, count toward hello max user data size.</span></span> <span data-ttu-id="58519-113">Ayrıca, ALTER TABLE yeterli yer toocreate hello tüm tablo ve dizinlerini yeni bir sürümü gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="58519-113">In addition, ALTER TABLE needs enough room toocreate a new version of hello entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="58519-114">İzleme ve uyarı</span><span class="sxs-lookup"><span data-stu-id="58519-114">Monitoring and alerting</span></span>
<span data-ttu-id="58519-115">Bellek içi depolama kullanımı hello yüzdesi olarak izleyebilirsiniz [depolama cap performans katmanı için](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) hello Azure'nın [portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="58519-115">You can monitor in-memory storage use as a percentage of hello [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in hello Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="58519-116">Merhaba veritabanı dikey penceresinde hello kaynak kullanımı kutusunu bulun ve Düzenle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="58519-116">On hello Database blade, locate hello Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="58519-117">Merhaba ölçümü seçebilmeniz `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="58519-117">Then select hello metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="58519-118">tooadd bir uyarı hello kaynak kullanımı kutusunu tooopen hello ölçüm dikey penceresinde'ı tıklatın, sonra Ekle uyarıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="58519-118">tooadd an alert, click on hello Resource Utilization box tooopen hello Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="58519-119">Veya sorgu tooshow hello bellek içi depolama kullanımını izleyen hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="58519-119">Or use hello following query tooshow hello in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="58519-120">Bellek durum - hata 41823 düzeltin</span><span class="sxs-lookup"><span data-stu-id="58519-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="58519-121">Bellek sonuçlarını 41823 hata iletisiyle başarısız INSERT, UPDATE ve oluşturma işlemleri çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="58519-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="58519-122">Hata iletisi 41823 hello bellek için iyileştirilmiş tablolar ve Tablo değişkenlerinin hello sınırını aştınız gösterir.</span><span class="sxs-lookup"><span data-stu-id="58519-122">Error message 41823 indicates that hello memory-optimized tables and table variables have exceeded hello maximum size.</span></span>

<span data-ttu-id="58519-123">tooresolve bu hata ya da:</span><span class="sxs-lookup"><span data-stu-id="58519-123">tooresolve this error, either:</span></span>

* <span data-ttu-id="58519-124">Veri hello bellek için iyileştirilmiş tablolar, potansiyel olarak yük boşaltma hello veri tootraditional, disk tabanlı tabloları silin; veya,</span><span class="sxs-lookup"><span data-stu-id="58519-124">Delete data from hello memory-optimized tables, potentially offloading hello data tootraditional, disk-based tables; or,</span></span>
* <span data-ttu-id="58519-125">Merhaba hizmet katmanı tooone yükseltme hello verileri için yeterli bellek içi depolama ile bellek için iyileştirilmiş tablolardaki tookeep gerekir.</span><span class="sxs-lookup"><span data-stu-id="58519-125">Upgrade hello service tier tooone with enough in-memory storage for hello data you need tookeep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58519-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="58519-126">Next steps</span></span>
<span data-ttu-id="58519-127">Kılavuzu izleme için bkz: [Azure SQL Dinamik Yönetim görünümlerini kullanarak veritabanı izleme](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="58519-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
