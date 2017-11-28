---
title: "Azure SQL Data Warehouse aaaUsing T-SQL görünümleri | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse'da Transact-SQL görünümlerini kullanma ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="7949e-103">SQL veri ambarı görünümlerde</span><span class="sxs-lookup"><span data-stu-id="7949e-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="7949e-104">Görünümleri SQL veri ambarı'nda özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="7949e-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="7949e-105">Çözümünüzü farklı şekillerde tooimprove hello kalitesini sayısında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7949e-105">They can be used in a number of different ways tooimprove hello quality of your solution.</span></span>  <span data-ttu-id="7949e-106">Bu makalede birkaç örnekleri nasıl tooenrich toobe gereksinim hello sınırlamaları yanı sıra görünümleri çözümünüzle kabul vurgular.</span><span class="sxs-lookup"><span data-stu-id="7949e-106">This article highlights a few examples of how tooenrich your solution with views, as well as hello limitations that need toobe considered.</span></span>

> [!NOTE]
> <span data-ttu-id="7949e-107">Sözdizimi `CREATE VIEW` bu makalede ele alınmamıştır.</span><span class="sxs-lookup"><span data-stu-id="7949e-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="7949e-108">Lütfen toohello bakın [CREATE VIEW] [ CREATE VIEW] MSDN makalesinde bu başvuru bilgileri için.</span><span class="sxs-lookup"><span data-stu-id="7949e-108">Please refer toohello [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="7949e-109">Mimari Özet</span><span class="sxs-lookup"><span data-stu-id="7949e-109">Architectural abstraction</span></span>
<span data-ttu-id="7949e-110">Yaygın bir uygulama düzeni toore olduğu-tablolar oluşturma tablo AS seçin (desen veri yükleme yaparken yeniden adlandırma nesne tarafından izlenen CTAS) kullanarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7949e-110">A very common application pattern is toore-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="7949e-111">Aşağıdaki örnek Hello yeni tarihi kayıtları tooa tarih boyutu ekler.</span><span class="sxs-lookup"><span data-stu-id="7949e-111">hello example below adds new date records tooa date dimension.</span></span> <span data-ttu-id="7949e-112">Nasıl DimDate_New, yeni bir tabble ilk oluşturulduğunda ve tooreplace hello özgün sürümü Merhaba tablonun yeniden adlandırılmış unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7949e-112">Note how a new tabble, DimDate_New, is first created and then renamed tooreplace hello original version of hello table.</span></span>

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

<span data-ttu-id="7949e-113">Ancak, bu yaklaşım görünmesini ve "tablo yok" hata iletileri yanı sıra bir kullanıcının görünüm kayboluyor tabloları neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="7949e-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="7949e-114">Merhaba arka plandaki nesneleri yeniden adlandırıldıktan adımında görünümleri tutarlı sunu katmanı kullanılan tooprovide kullanıcılarla olabilir.</span><span class="sxs-lookup"><span data-stu-id="7949e-114">Views can be used tooprovide users with a consistent presentation layer whilst hello underlying objects are renamed.</span></span> <span data-ttu-id="7949e-115">Kullanıcılara erişim sağlayarak toohello verileri bir görünümler yoluyla anlamına gelir kullanıcılar hello temel tabloları toohave görünürlüğünü gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="7949e-115">By providing users access toohello data through a views, means users don't need toohave visibility of hello underlying tables.</span></span> <span data-ttu-id="7949e-116">Merhaba veri ambarı tasarımcıları hello veri modeli gelişmesi ve hello veri yükleme işlemi sırasında CTAS kullanarak performansı en üst düzeye çıkarmak sağlarken tutarlı bir kullanıcı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7949e-116">This provides a consistent user experience while ensuring that hello data warehouse designers can evolve hello data model and maximize performance by using CTAS during hello data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="7949e-117">Performansı iyileştirme</span><span class="sxs-lookup"><span data-stu-id="7949e-117">Performance optimization</span></span>
<span data-ttu-id="7949e-118">Görünümleri de kullanılan tooenforce en iyi duruma getirilmiş performans birleştirmeler tablolar arasında olabilir.</span><span class="sxs-lookup"><span data-stu-id="7949e-118">Views can also be utilized tooenforce performance optimized joins between tables.</span></span> <span data-ttu-id="7949e-119">Örneğin, bir görünüm olarak yedekli dağıtım anahtarı ölçütleri toominimize veri taşıma birleştirme hello bir parçası olarak dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7949e-119">For example, a view can incorporate a redundant distribution key as part of hello joining criteria toominimize data movement.</span></span>  <span data-ttu-id="7949e-120">Bir görünüm başka bir yararı tooforce belirli bir sorgu veya birleşme ipucu olabilir.</span><span class="sxs-lookup"><span data-stu-id="7949e-120">Another benefit of a view could be tooforce a specific query or joining hint.</span></span> <span data-ttu-id="7949e-121">Bu şekilde görünümleri birleştirmeler kullanıcılar tooremember hello doğru yapı kendi birleştirmelerde hello gereksinimini önleme bir en iyi şekilde her zaman gerçekleştirildiğinden emin güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="7949e-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding hello need for users tooremember hello correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="7949e-122">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="7949e-122">Limitations</span></span>
<span data-ttu-id="7949e-123">SQL veri ambarı görünümlerinde yalnızca meta verilerdir.</span><span class="sxs-lookup"><span data-stu-id="7949e-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="7949e-124">Sonuç olarak aşağıdaki seçenekleri şu hello kullanılabilir değil:</span><span class="sxs-lookup"><span data-stu-id="7949e-124">Consequently hello following options are not available:</span></span>

* <span data-ttu-id="7949e-125">Şema bağlama seçeneği yoktur</span><span class="sxs-lookup"><span data-stu-id="7949e-125">There is no schema binding option</span></span>
* <span data-ttu-id="7949e-126">Temel tabloyu hello görünüm üzerinden güncelleştirilemiyor</span><span class="sxs-lookup"><span data-stu-id="7949e-126">Base tables cannot be updated through hello view</span></span>
* <span data-ttu-id="7949e-127">Geçici tablolar üzerindeki görünüm oluşturulamıyor</span><span class="sxs-lookup"><span data-stu-id="7949e-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="7949e-128">Merhaba genişletme için destek yok / NOEXPAND ipuçları</span><span class="sxs-lookup"><span data-stu-id="7949e-128">There is no support for hello EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="7949e-129">SQL veri ambarı'nda hiç dizini oluşturulmuş görünüm yok</span><span class="sxs-lookup"><span data-stu-id="7949e-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="7949e-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7949e-130">Next steps</span></span>
<span data-ttu-id="7949e-131">Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="7949e-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="7949e-132">İçin `CREATE VIEW` sözdizimi başvurun çok[CREATE VIEW][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="7949e-132">For `CREATE VIEW` syntax please refer too[CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
