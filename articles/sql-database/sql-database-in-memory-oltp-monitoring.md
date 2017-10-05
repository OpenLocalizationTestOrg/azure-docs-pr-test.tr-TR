---
title: "İzleme XTP bellek içi depolama | Microsoft Docs"
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
ms.openlocfilehash: 5afb2209f18b1ba2aa0a916a439509b01afd80da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-in-memory-oltp-storage"></a><span data-ttu-id="ef718-103">Bellek içi OLTP Depolama Alanını izleme</span><span class="sxs-lookup"><span data-stu-id="ef718-103">Monitor In-Memory OLTP Storage</span></span>
<span data-ttu-id="ef718-104">Kullanırken [bellek içi OLTP](sql-database-in-memory.md), bellek için iyileştirilmiş tablolar ve Tablo değişkenlerinin verileri bellek içi OLTP depolamada yer alıyor.</span><span class="sxs-lookup"><span data-stu-id="ef718-104">When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage.</span></span> <span data-ttu-id="ef718-105">Her Premium Hizmet katmanını belgelenen en fazla bir bellek içi OLTP depolama boyutuna sahip [SQL Database hizmet katmanları makale](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span><span class="sxs-lookup"><span data-stu-id="ef718-105">Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels).</span></span> <span data-ttu-id="ef718-106">Bu sınır aşılırsa sonra ekleme ve güncelleştirme işlemleri (hatası 41823 ile) başarısız olan başlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ef718-106">Once this limit is exceeded, insert and update operations may start failing (with error 41823).</span></span> <span data-ttu-id="ef718-107">Bu noktada, ya da belleği geri almasını verileri silmek veya veritabanınızın performans katmanı yükseltin.</span><span class="sxs-lookup"><span data-stu-id="ef718-107">At that point you will need to either delete data to reclaim memory, or upgrade the performance tier of your database.</span></span>

## <a name="determine-whether-data-will-fit-within-the-in-memory-storage-cap"></a><span data-ttu-id="ef718-108">Veri içinde bellek içi depolama ucun uygun olup olmadığını belirleme</span><span class="sxs-lookup"><span data-stu-id="ef718-108">Determine whether data will fit within the in-memory storage cap</span></span>
<span data-ttu-id="ef718-109">Depolama ucun belirlemek: başvurun [SQL Database hizmet katmanları makale](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) farklı Premium hizmet katmanları, depolama caps için.</span><span class="sxs-lookup"><span data-stu-id="ef718-109">Determine the storage cap: consult the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for the storage caps of the different Premium service tiers.</span></span>

<span data-ttu-id="ef718-110">Bellek için iyileştirilmiş tablo works onu aynı şekilde SQL Server için Azure SQL veritabanı'nda mu bellek gereksinimlerini tahmin etme.</span><span class="sxs-lookup"><span data-stu-id="ef718-110">Estimating memory requirements for a memory-optimized table works the same way for SQL Server as it does in Azure SQL Database.</span></span> <span data-ttu-id="ef718-111">Bu konuda üzerinde gözden geçirmek için birkaç dakika sürebilir [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef718-111">Take a few minutes to review that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).</span></span>

<span data-ttu-id="ef718-112">Tablosu ve tablo değişkeni satırları yanı dizinler, en fazla kullanıcı veri boyutu doğru saymak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ef718-112">Note that the table and table variable rows, as well as indexes, count toward the max user data size.</span></span> <span data-ttu-id="ef718-113">Buna ek olarak, ALTER TABLE tablonun tamamını ve dizinlerini yeni bir sürümünü oluşturmak için yeterli alan gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef718-113">In addition, ALTER TABLE needs enough room to create a new version of the entire table and its indexes.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="ef718-114">İzleme ve uyarı</span><span class="sxs-lookup"><span data-stu-id="ef718-114">Monitoring and alerting</span></span>
<span data-ttu-id="ef718-115">Bellek içi depolama kullanımı yüzdesi olarak izleyebilirsiniz [depolama cap performans katmanı için](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) azure'da [portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="ef718-115">You can monitor in-memory storage use as a percentage of the [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in the Azure [portal](https://portal.azure.com/):</span></span> 

* <span data-ttu-id="ef718-116">Veritabanı dikey penceresinde kaynak kullanımı kutusunu bulun ve Düzenle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef718-116">On the Database blade, locate the Resource utilization box and click on Edit.</span></span>
* <span data-ttu-id="ef718-117">Ölçümü seçin `In-Memory OLTP Storage percentage`.</span><span class="sxs-lookup"><span data-stu-id="ef718-117">Then select the metric `In-Memory OLTP Storage percentage`.</span></span>
* <span data-ttu-id="ef718-118">Bir uyarı eklemek için ölçüm dikey penceresi açmak için kaynak kullanımı kutusuna tıklayın, sonra Ekle uyarıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef718-118">To add an alert, click on the Resource Utilization box to open the Metric blade, then click on Add alert.</span></span>

<span data-ttu-id="ef718-119">Veya bellek içi depolama kullanımını göstermek için aşağıdaki sorguyu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ef718-119">Or use the following query to show the in-memory storage utilization:</span></span>

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a><span data-ttu-id="ef718-120">Bellek durum - hata 41823 düzeltin</span><span class="sxs-lookup"><span data-stu-id="ef718-120">Correct out-of-memory situations - Error 41823</span></span>
<span data-ttu-id="ef718-121">Bellek sonuçlarını 41823 hata iletisiyle başarısız INSERT, UPDATE ve oluşturma işlemleri çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="ef718-121">Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.</span></span>

<span data-ttu-id="ef718-122">Hata iletisi 41823 bellek için iyileştirilmiş tablolar ve Tablo değişkenlerinin boyutu üst sınırı aştınız gösterir.</span><span class="sxs-lookup"><span data-stu-id="ef718-122">Error message 41823 indicates that the memory-optimized tables and table variables have exceeded the maximum size.</span></span>

<span data-ttu-id="ef718-123">Ya da bu hatayı gidermek için:</span><span class="sxs-lookup"><span data-stu-id="ef718-123">To resolve this error, either:</span></span>

* <span data-ttu-id="ef718-124">Potansiyel olarak Geleneksel, disk tabanlı tablolara veri boşaltma bellek için iyileştirilmiş tablolardaki verileri silmek; veya,</span><span class="sxs-lookup"><span data-stu-id="ef718-124">Delete data from the memory-optimized tables, potentially offloading the data to traditional, disk-based tables; or,</span></span>
* <span data-ttu-id="ef718-125">Bellek için iyileştirilmiş tablolarda tutmak için gereken verileri için yeterli bellek içi depolama sahip bir hizmet katmanına yükseltin.</span><span class="sxs-lookup"><span data-stu-id="ef718-125">Upgrade the service tier to one with enough in-memory storage for the data you need to keep in memory-optimized tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef718-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ef718-126">Next steps</span></span>
<span data-ttu-id="ef718-127">Kılavuzu izleme için bkz: [Azure SQL Dinamik Yönetim görünümlerini kullanarak veritabanı izleme](sql-database-monitoring-with-dmvs.md).</span><span class="sxs-lookup"><span data-stu-id="ef718-127">For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).</span></span>
