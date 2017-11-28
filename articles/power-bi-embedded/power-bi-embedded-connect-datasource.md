---
title: "aaaMicrosoft Power BI Embedded - bağlanan tooa veri kaynağı"
description: "Power BI Embedded, toodata kaynaklarına bağlanın"
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
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a><span data-ttu-id="c7884-103">Tooa veri kaynağına bağlanma</span><span class="sxs-lookup"><span data-stu-id="c7884-103">Connect tooa data source</span></span>
<span data-ttu-id="c7884-104">İle **Power BI Embedded**, raporlar, kendi uygulamanıza eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="c7884-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="c7884-105">Power BI raporu uygulamanıza bulunmadığında, arka plandaki tarafından veri toohello hello rapor bağlanır **alma** hello veri ya da bir kopyasını **doğrudan bağlanma** toohello veri kaynağını kullanan  **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="c7884-105">When you embed a Power BI report into your app, hello report connects toohello underlying data by **importing** a copy of hello data or by **connecting directly** toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="c7884-106">Kullanarak arasındaki farklar hello işte **alma** ve **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="c7884-106">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="c7884-107">İçeri Aktarma</span><span class="sxs-lookup"><span data-stu-id="c7884-107">Import</span></span> | <span data-ttu-id="c7884-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="c7884-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="c7884-109">Tablolar, sütunlar *ve veri* içeri aktarılan veya hello raporun kümesine kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c7884-109">Tables, columns, *and data* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="c7884-110">toosee bu oluştu toohello temel alınan veriler değiştiğinde, yenileme veya alma, bir tam, güncel veri kümesini yeniden.</span><span class="sxs-lookup"><span data-stu-id="c7884-110">toosee changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="c7884-111">Yalnızca *tablolar ve sütunlar* içeri aktarılan veya hello raporun kümesine kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c7884-111">Only *tables and columns* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="c7884-112">Her zaman hello en güncel verileri görüntülediğiniz.</span><span class="sxs-lookup"><span data-stu-id="c7884-112">You always view hello most current data.</span></span> |

<span data-ttu-id="c7884-113">Power BI Embedded ile DirectQuery bulut veri kaynaklarıyla kullanabilirsiniz, ancak veri kaynakları şu anda şirket içi değil.</span><span class="sxs-lookup"><span data-stu-id="c7884-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="c7884-114">Merhaba şirket içi veri ağ geçidi Power BI Embedded ile şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="c7884-114">hello On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="c7884-115">Bu, şirket içi veri kaynakları ile DirectQuery kullanamayacağınız anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c7884-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="c7884-116">Desteklenen veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="c7884-116">Supported data sources</span></span>

<span data-ttu-id="c7884-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="c7884-117">**DirectQuery**</span></span>
* <span data-ttu-id="c7884-118">Azure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="c7884-118">Azure SQL database</span></span>
* <span data-ttu-id="c7884-119">Azure SQL Veri Ambarı</span><span class="sxs-lookup"><span data-stu-id="c7884-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="c7884-120">**İçeri Aktarma**</span><span class="sxs-lookup"><span data-stu-id="c7884-120">**Import**</span></span>

<span data-ttu-id="c7884-121">Tüm hello kullanılabilir veri kaynaklarını Power BI Desktop içinde kullanarak içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7884-121">You can import using all of hello available data sources within Power BI Desktop.</span></span> <span data-ttu-id="c7884-122">Şunları yapacaksınız **değil** mümkün toorefresh Power BI Embedded içinde bu verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="c7884-122">You will **not** be able toorefresh that data within Power BI Embedded.</span></span> <span data-ttu-id="c7884-123">Tooupload değişiklikleri olacaktır tooyour PBIX dosyası tooPower BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="c7884-123">You will have tooupload changes tooyour PBIX file tooPower BI Embedded.</span></span> <span data-ttu-id="c7884-124">Bu toono kullanılabilir ağ geçididir.</span><span class="sxs-lookup"><span data-stu-id="c7884-124">This is due toono available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="c7884-125">DirectQuery kullanmanın yararları</span><span class="sxs-lookup"><span data-stu-id="c7884-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="c7884-126">İki birincil avantajları vardır kullanırken **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="c7884-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="c7884-127">**DirectQuery** sağlar, yapı görselleştirmeleri Burada, aksi takdirde olacaktır unfeasible toofirst alma çok büyük veri kümeleri üzerinde tüm veri hello.</span><span class="sxs-lookup"><span data-stu-id="c7884-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible toofirst import all of hello data.</span></span>
* <span data-ttu-id="c7884-128">Veri değişikliklerini temel alınan veri yenileme gerektirebilir ve bazı raporlar için hello toodisplay geçerli verileri büyük veri aktarımları, yeniden içeri aktarılmasını verilerin unfeasible sağlama gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="c7884-128">Underlying data changes can require a refresh of data, and for some reports, hello need toodisplay current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="c7884-129">Bunun aksine, **DirectQuery** raporları her zaman güncel verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7884-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="c7884-130">DirectQuery sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="c7884-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="c7884-131">Bazı sınırlamalar toousing vardır **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="c7884-131">There are a few limitations toousing **DirectQuery**:</span></span>

* <span data-ttu-id="c7884-132">Tüm tablolar tek bir veritabanından gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="c7884-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="c7884-133">Merhaba sorgu fazla karmaşık olması durumunda bir hata ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="c7884-133">If hello query is overly complex, an error will occur.</span></span> <span data-ttu-id="c7884-134">en az karmaşık olacak şekilde tooremedy hello hata, hello sorgu yeniden düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7884-134">tooremedy hello error you must refactor hello query so it is less complex.</span></span> <span data-ttu-id="c7884-135">Merhaba sorgu karmaşık olması gerekiyorsa kullanmak yerine tooimport hello verilere ihtiyaç duyarsınız **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="c7884-135">If hello query must be complex, you will need tooimport hello data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="c7884-136">İlişki filtreleme, her iki yönde yerine sınırlı tooa tek yön olur.</span><span class="sxs-lookup"><span data-stu-id="c7884-136">Relationship filtering is limited tooa single direction, rather than both directions.</span></span>
* <span data-ttu-id="c7884-137">Merhaba bir sütunun veri türünü değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7884-137">You cannot change hello data type of a column.</span></span>
* <span data-ttu-id="c7884-138">Varsayılan olarak, sınırlamalar ölçüler izin DAX ifadeleri yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c7884-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="c7884-139">Bkz: [DirectQuery ve ölçüleri](#measures).</span><span class="sxs-lookup"><span data-stu-id="c7884-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="c7884-140">DirectQuery ve ölçüleri</span><span class="sxs-lookup"><span data-stu-id="c7884-140">DirectQuery and measures</span></span>
<span data-ttu-id="c7884-141">kabul edilebilir performans toohello veri kaynağındaki gönderilen tooensure sorguların vardır, sınırlamalar ölçüler üzerinde uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="c7884-141">tooensure queries sent toohello underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="c7884-142">Kullanırken **Power BI Desktop**, Gelişmiş kullanıcılar seçebilirsiniz toobypass bu sınırlamaya seçerek **Dosya > Seçenekler ve Ayarlar > Seçenekler**.</span><span class="sxs-lookup"><span data-stu-id="c7884-142">When using **Power BI Desktop**, advanced users can choose toobypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="c7884-143">Merhaba, **seçenekleri** iletişim kutusunda, seçin **DirectQuery**ve hello seçeneğini belirleyin **DirectQuery modunda Kısıtlanmamış ölçümlere izin**.</span><span class="sxs-lookup"><span data-stu-id="c7884-143">In hello **Options** dialog, choose **DirectQuery**, and select hello option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="c7884-144">Bu seçenek belirlendiğinde, bir ölçü için geçerli olan herhangi bir DAX ifade kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c7884-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="c7884-145">Kullanıcıların farkında olması gerekir; Ancak, hello verileri içe aktarıldığında bazı ifadeleri, çok iyi gerçekleştireceğini çok yavaş sorguları toohello arka neden olabilir, kaynağı **DirectQuery** modu.</span><span class="sxs-lookup"><span data-stu-id="c7884-145">Users must be aware; however, that some expressions that perform very well when hello data is imported may result in very slow queries toohello backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="c7884-146">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="c7884-146">See Also</span></span>
* [<span data-ttu-id="c7884-147">Microsoft Power BI Embedded ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c7884-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="c7884-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="c7884-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="c7884-149">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="c7884-149">More questions?</span></span> [<span data-ttu-id="c7884-150">Merhaba Power BI topluluk deneyin</span><span class="sxs-lookup"><span data-stu-id="c7884-150">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

