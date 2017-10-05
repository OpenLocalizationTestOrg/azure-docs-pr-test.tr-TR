---
title: "Microsoft Power BI Embedded - bir veri kaynağına bağlanma"
description: "Power BI Embedded, veri kaynaklarına bağlanmak"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 9f614bbc63eae788aa52132c8f0e42ad8963559a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-a-data-source"></a><span data-ttu-id="e3d7b-103">Bir veri kaynağına bağlanma</span><span class="sxs-lookup"><span data-stu-id="e3d7b-103">Connect to a data source</span></span>
<span data-ttu-id="e3d7b-104">İle **Power BI Embedded**, raporlar, kendi uygulamanıza eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="e3d7b-105">Uygulamanıza bir Power BI raporu, rapor tarafından temel alınan veri bağlanır **alma** yapılandırarak veya verilerin bir kopyasını **doğrudan bağlanma** kullanarak veri kaynağı için **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-105">When you embed a Power BI report into your app, the report connects to the underlying data by **importing** a copy of the data or by **connecting directly** to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="e3d7b-106">**İçeri Aktarma** ve **DirectQuery**.arasındaki farklar burada yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-106">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="e3d7b-107">İçeri Aktarma</span><span class="sxs-lookup"><span data-stu-id="e3d7b-107">Import</span></span> | <span data-ttu-id="e3d7b-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="e3d7b-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="e3d7b-109">Tablolar, sütunlar *ve veri* içeri aktarılan veya raporun veri kümesine kopyalar.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-109">Tables, columns, *and data* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="e3d7b-110">Temel alınan verilerde meydana değişiklikleri görmek için yenileme veya alma, bir tam, güncel veri kümesini yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-110">To see changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="e3d7b-111">Yalnızca *tablolar ve sütunlar* içeri aktarılan veya raporun veri kümesine kopyalar.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-111">Only *tables and columns* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="e3d7b-112">Her zaman en güncel verileri görüntülediğiniz.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-112">You always view the most current data.</span></span> |

<span data-ttu-id="e3d7b-113">Power BI Embedded ile DirectQuery bulut veri kaynaklarıyla kullanabilirsiniz, ancak veri kaynakları şu anda şirket içi değil.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="e3d7b-114">Şirket içi veri ağ geçidi, şu anda Power BI Embedded ile desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-114">The On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="e3d7b-115">Bu, şirket içi veri kaynakları ile DirectQuery kullanamayacağınız anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="e3d7b-116">Desteklenen veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="e3d7b-116">Supported data sources</span></span>

<span data-ttu-id="e3d7b-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="e3d7b-117">**DirectQuery**</span></span>
* <span data-ttu-id="e3d7b-118">Azure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="e3d7b-118">Azure SQL database</span></span>
* <span data-ttu-id="e3d7b-119">Azure SQL Veri Ambarı</span><span class="sxs-lookup"><span data-stu-id="e3d7b-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="e3d7b-120">**İçeri Aktarma**</span><span class="sxs-lookup"><span data-stu-id="e3d7b-120">**Import**</span></span>

<span data-ttu-id="e3d7b-121">Tüm Power BI Desktop içinde kullanılabilir veri kaynakları kullanarak içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-121">You can import using all of the available data sources within Power BI Desktop.</span></span> <span data-ttu-id="e3d7b-122">Şunları yapacaksınız **değil** Power BI Embedded içinde bu verileri yenileyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-122">You will **not** be able to refresh that data within Power BI Embedded.</span></span> <span data-ttu-id="e3d7b-123">Değişiklikleri Power BI Embedded, PBIX dosyanızı karşıya yüklemek gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-123">You will have to upload changes to your PBIX file to Power BI Embedded.</span></span> <span data-ttu-id="e3d7b-124">Ağ geçidi nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-124">This is due to no available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="e3d7b-125">DirectQuery kullanmanın yararları</span><span class="sxs-lookup"><span data-stu-id="e3d7b-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="e3d7b-126">İki birincil avantajları vardır kullanırken **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="e3d7b-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="e3d7b-127">**DirectQuery** tüm verileri çok büyük veri kümeleri, burada, aksi takdirde olacaktır ilk alınacak unfeasible üzerinden görselleştirmeleri oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible to first import all of the data.</span></span>
* <span data-ttu-id="e3d7b-128">Veri değişikliklerini temel alınan veri yenileme gerektirebilir ve bazı raporlar için geçerli verileri görüntülemek için gereken büyük veri aktarımları, yeniden içeri aktarılmasını verilerin unfeasible sağlama gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-128">Underlying data changes can require a refresh of data, and for some reports, the need to display current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="e3d7b-129">Bunun aksine, **DirectQuery** raporları her zaman güncel verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="e3d7b-130">DirectQuery sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="e3d7b-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="e3d7b-131">Kullanımıyla ilgili birkaç sınırlama vardır **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="e3d7b-131">There are a few limitations to using **DirectQuery**:</span></span>

* <span data-ttu-id="e3d7b-132">Tüm tablolar tek bir veritabanından gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="e3d7b-133">Sorgu fazla karmaşık olması durumunda bir hata ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-133">If the query is overly complex, an error will occur.</span></span> <span data-ttu-id="e3d7b-134">Hatayı gidermek için en az karmaşık olacak şekilde sorguyu yeniden düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-134">To remedy the error you must refactor the query so it is less complex.</span></span> <span data-ttu-id="e3d7b-135">Sorgu karmaşık olması gerekiyorsa kullanmak yerine verileri içe aktarmanız gerekir **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-135">If the query must be complex, you will need to import the data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="e3d7b-136">İlişki filtreleme, her iki yönde yerine tek bir yön sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-136">Relationship filtering is limited to a single direction, rather than both directions.</span></span>
* <span data-ttu-id="e3d7b-137">Bir sütunun veri türünü değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-137">You cannot change the data type of a column.</span></span>
* <span data-ttu-id="e3d7b-138">Varsayılan olarak, sınırlamalar ölçüler izin DAX ifadeleri yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="e3d7b-139">Bkz: [DirectQuery ve ölçüleri](#measures).</span><span class="sxs-lookup"><span data-stu-id="e3d7b-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="e3d7b-140">DirectQuery ve ölçüleri</span><span class="sxs-lookup"><span data-stu-id="e3d7b-140">DirectQuery and measures</span></span>
<span data-ttu-id="e3d7b-141">Temel alınan veri kaynağına gönderilen sorguların kabul edilebilir performans sahip emin olmak için sınırlamalar ölçüler üzerinde kullanılan.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-141">To ensure queries sent to the underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="e3d7b-142">Kullanırken **Power BI Desktop**, Gelişmiş kullanıcılar seçerek bu sınırlamaya atlamak seçebilirsiniz **Dosya > Seçenekler ve Ayarlar > Seçenekler**.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-142">When using **Power BI Desktop**, advanced users can choose to bypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="e3d7b-143">İçinde **seçenekleri** iletişim kutusunda, seçin **DirectQuery**ve seçeneğini **DirectQuery modunda Kısıtlanmamış ölçümlere izin**.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-143">In the **Options** dialog, choose **DirectQuery**, and select the option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="e3d7b-144">Bu seçenek belirlendiğinde, bir ölçü için geçerli olan herhangi bir DAX ifade kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="e3d7b-145">Kullanıcıların farkında olması gerekir; Ancak, verileri içe aktarıldığında gerçekleştiren çok iyi bazı değerler çok yavaş neden olabileceğini arka ucuna sorgular zaman içinde kaynak **DirectQuery** modu.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-145">Users must be aware; however, that some expressions that perform very well when the data is imported may result in very slow queries to the backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="e3d7b-146">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="e3d7b-146">See Also</span></span>
* [<span data-ttu-id="e3d7b-147">Microsoft Power BI Embedded ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e3d7b-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="e3d7b-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="e3d7b-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="e3d7b-149">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="e3d7b-149">More questions?</span></span> [<span data-ttu-id="e3d7b-150">Power BI Topluluğu'nu deneyin</span><span class="sxs-lookup"><span data-stu-id="e3d7b-150">Try the Power BI Community</span></span>](http://community.powerbi.com/)

