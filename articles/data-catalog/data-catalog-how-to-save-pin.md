---
title: "Aramaları kaydetme ve Azure veri Kataloğu'nda veri varlıklarının Sabitle | Microsoft Docs"
description: "Nasıl yapılır makalesi veri kaynakları ve daha sonra kullanmak için veri varlıklarını kaydetme için Azure veri Kataloğu özellikleri vurgulama."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 8c319d0dcbe8b95af11b8be2368a9348b260446c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="86394-103">Azure veri Kataloğu'nda arama ve PIN veri varlıklarını kaydetme</span><span class="sxs-lookup"><span data-stu-id="86394-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="86394-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="86394-104">Introduction</span></span>
<span data-ttu-id="86394-105">Azure veri Kataloğu, veri kaynağı bulma için yetenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="86394-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="86394-106">Hızlı bir şekilde arayın ve veri kaynaklarını bulmak ve bunların amacı anlamak için katalog daha kolay elinizdeki iş için doğru verileri bulmak filtre.</span><span class="sxs-lookup"><span data-stu-id="86394-106">You can quickly search and filter the catalog to locate data sources and understand their intended purpose, making it easier to find the right data for the job at hand.</span></span>

<span data-ttu-id="86394-107">Ancak düzenli olarak aynı verilerle çalışmak ne gerekir?</span><span class="sxs-lookup"><span data-stu-id="86394-107">But what if you need to regularly work with the same data?</span></span> <span data-ttu-id="86394-108">Ve ne sizin ve diğer kullanıcıların düzenli olarak bilginiz kataloğunda aynı veri kaynaklarına katkıda?</span><span class="sxs-lookup"><span data-stu-id="86394-108">And what if you and other users regularly contribute your knowledge to the same data sources in the catalog?</span></span> <span data-ttu-id="86394-109">Bu durumlarda, art arda aynı aramaları vermek verimsiz olabilir.</span><span class="sxs-lookup"><span data-stu-id="86394-109">In these situations, having to repeatedly issue the same searches can be inefficient.</span></span> <span data-ttu-id="86394-110">Kayıtlı arama ve sabitlenmiş veri varlıkları olduğu yardımcı olabilir budur.</span><span class="sxs-lookup"><span data-stu-id="86394-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="86394-111">Kaydedilen aramalar</span><span class="sxs-lookup"><span data-stu-id="86394-111">Saved searches</span></span>
<span data-ttu-id="86394-112">Veri Kataloğu'nda kaydedilmiş bir aramayı bir yeniden kullanılabilir, kullanıcı başına arama tanımıdır.</span><span class="sxs-lookup"><span data-stu-id="86394-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="86394-113">Arama terimleri, etiketler ve diğer filtreleri gibi bir arama tanımlamak ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="86394-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="86394-114">Daha sonra kendi arama ölçütleriyle eşleşen hiçbir veri varlıklarını döndürmek için kayıtlı arama tanımı yeniden çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86394-114">You can re-run the saved search definition later to return any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="86394-115">Kaydedilmiş bir aramayı oluşturma</span><span class="sxs-lookup"><span data-stu-id="86394-115">Create a saved search</span></span>
<span data-ttu-id="86394-116">Kaydedilmiş bir aramayı oluşturmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="86394-116">To create a saved search, do the following:</span></span>
1. <span data-ttu-id="86394-117">Azure veri Kataloğu portalında içinde **geçerli aramayı** penceresinde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="86394-117">In the Azure Data Catalog portal, in the **Current Search** window, click **Save**.</span></span> 

    ![Geçerli arama ayarları Kaydet bağlantısı](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="86394-119">Yeniden kullanmak ve ardından istediğiniz arama ölçütlerini girin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="86394-119">Enter the search criteria that you want to reuse, and then click **Save**.</span></span>

    ![Kaydedilen arama adı geçerli arama ayarları](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="86394-121">İstendiğinde, kayıtlı arama için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="86394-121">When you are prompted, enter a name for the saved search.</span></span> <span data-ttu-id="86394-122">Anlamlı bir ad seçin ve araması tarafından döndürülen veri varlıklarını açıklar.</span><span class="sxs-lookup"><span data-stu-id="86394-122">Pick a name that is meaningful and that describes the data assets that will be returned by the search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="86394-123">Kaydedilmiş aramaları Yönet</span><span class="sxs-lookup"><span data-stu-id="86394-123">Manage saved searches</span></span>
<span data-ttu-id="86394-124">Bir veya daha fazla aramalar, kaydettiğiniz sonra bir **kayıtlı aramaları** seçeneği altında görüntülenir **geçerli aramayı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="86394-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath the **Current Search** box.</span></span> <span data-ttu-id="86394-125">Liste genişletildiğinde tüm kaydedilmiş aramaları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="86394-125">When the list is expanded, all saved searches are displayed.</span></span>

 ![Kaydedilmiş aramaları listesi](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="86394-127">Aşağıdakilerden birini yapın:</span><span class="sxs-lookup"><span data-stu-id="86394-127">Do any of the following:</span></span>

* <span data-ttu-id="86394-128">Bir arama yürütmek için kaydedilmiş bir aramayı listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="86394-128">To execute a search, select a saved search in the list.</span></span>

* <span data-ttu-id="86394-129">Kayıtlı bir aramaya Yönetimi seçeneklerinin bir listesini görüntülemek için arama adının yanındaki aşağı oka tıklayın.</span><span class="sxs-lookup"><span data-stu-id="86394-129">To view a list of management options for a saved search, click the down arrow next to the search name.</span></span>

    ![Kaydedilmiş aramaları yönetmek için Seçenekler](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="86394-131">Kayıtlı arama için yeni bir ad girmeyi seçin **yeniden adlandırma**.</span><span class="sxs-lookup"><span data-stu-id="86394-131">To enter a new name for the saved search, select **Rename**.</span></span> <span data-ttu-id="86394-132">Arama tanımı değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="86394-132">The search definition is not changed.</span></span>

* <span data-ttu-id="86394-133">Kayıtlı arama listenizden kaldırmayı seçin **silmek**ve silme işlemini onaylayın.</span><span class="sxs-lookup"><span data-stu-id="86394-133">To remove the saved search from your list, select **Delete**, and then confirm the deletion.</span></span>

* <span data-ttu-id="86394-134">Kayıtlı arama varsayılan aramanızı olarak işaretlemek için seçin **varsayılan olarak Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="86394-134">To mark the saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="86394-135">Azure veri Kataloğu giriş sayfasından bir "boş" araması gerçekleştirirseniz, varsayılan aramanızı yürütülür.</span><span class="sxs-lookup"><span data-stu-id="86394-135">If you perform an “empty” search from the Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="86394-136">Varsayılan arama olarak işaretlenmiş arama en üstünde ek olarak, görüntülenen **kayıtlı aramaları** listesi.</span><span class="sxs-lookup"><span data-stu-id="86394-136">In addition, the search that's marked as the default search is displayed at the top of the **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="86394-137">Kuruluş Kaydedilmiş aramaları</span><span class="sxs-lookup"><span data-stu-id="86394-137">Organizational saved searches</span></span>
<span data-ttu-id="86394-138">Kuruluşunuzdaki tüm kullanıcı kendi kullanmak için aramaları kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86394-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="86394-139">Veri Kataloğu yöneticileri kuruluş içindeki tüm kullanıcılar için aramaları da kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86394-139">Data Catalog administrators can also save searches for all users within the organization.</span></span> <span data-ttu-id="86394-140">Yöneticiler bir aramayı kaydettiğinizde, bunlar ile sunulan bir **paylaşımı şirket içinde** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="86394-140">When administrators save a search, they're presented with a **Share within the company** option.</span></span> <span data-ttu-id="86394-141">Bu seçeneğin belirlenmesi, kuruluşunuzdaki tüm kullanıcılar için kayıtlı arama paylaşır.</span><span class="sxs-lookup"><span data-stu-id="86394-141">Selecting this option shares the saved search for all users in the organization.</span></span>

 ![Kuruluş Kaydedilmiş aramaları](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="86394-143">Sabitlenmiş veri varlıklarını</span><span class="sxs-lookup"><span data-stu-id="86394-143">Pinned data assets</span></span>
<span data-ttu-id="86394-144">Kaydedilmiş aramaları ile kaydedebilir ve arama tanımları yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86394-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="86394-145">Aramaları tarafından döndürülen veri varlıklarını katalog değişiklik içeriğini olarak zaman içinde değişebilir.</span><span class="sxs-lookup"><span data-stu-id="86394-145">The data assets that are returned by the searches might change over time as the contents of the catalog change.</span></span> <span data-ttu-id="86394-146">Veri varlıklarını PIN zaman bir arama kullanmaya gerek kalmadan daha kolay erişim sağlamak için belirli veri varlıklarını açıkça tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86394-146">When you pin data assets, you can explicitly identify specific data assets to make them easier to access without needing to use a search.</span></span>

<span data-ttu-id="86394-147">Bir veri varlığına sabitleme basittir.</span><span class="sxs-lookup"><span data-stu-id="86394-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="86394-148">Veri varlığına sabitlenmiş listenize eklemek için tıklayın **PIN** simgesi.</span><span class="sxs-lookup"><span data-stu-id="86394-148">To add the data asset to your pinned list, you simply click the **pin** icon.</span></span> <span data-ttu-id="86394-149">Simge varlık döşemenin döşeme görünümünü ve Azure veri Kataloğu portalını liste görünümünde en sol sütununda köşesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="86394-149">The icon is displayed in the corner of the asset tile in the tile view, and in the left-most column in the list view in the Azure Data Catalog portal.</span></span>

![Veri varlığına PIN simgesi](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="86394-151">Bir veri varlığına kaldırıldığında eşit olarak açıktır.</span><span class="sxs-lookup"><span data-stu-id="86394-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="86394-152">Tıklamanız yeterlidir **sabitleme** simgesi seçili varlık ayarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="86394-152">Simply click the **unpin** icon to toggle the setting for the selected asset.</span></span>

![Veri varlığına sabitleme simgesi](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="the-my-assets-section"></a><span data-ttu-id="86394-154">My varlıklar bölümü</span><span class="sxs-lookup"><span data-stu-id="86394-154">The My Assets section</span></span>
<span data-ttu-id="86394-155">Veri Kataloğu portalı giriş sayfasına içeren bir **My varlıklar** ilgi varlıklar geçerli kullanıcı için görüntüler bölümü.</span><span class="sxs-lookup"><span data-stu-id="86394-155">The Data Catalog portal home page includes a **My Assets** section that displays assets of interest to the current user.</span></span> <span data-ttu-id="86394-156">Bu bölümde her iki sabitlenmiş varlıkları içerir ve kayıtlı aramalar.</span><span class="sxs-lookup"><span data-stu-id="86394-156">This section includes both pinned assets and saved searches.</span></span>

![Giriş sayfasında My varlıklar bölümü](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="86394-158">Özet</span><span class="sxs-lookup"><span data-stu-id="86394-158">Summary</span></span>
<span data-ttu-id="86394-159">Azure veri Kataloğu sizin ve diğer kuruluş üyelerinin verileri ve daha fazla süre ile çalışmak için arayan daha az zaman harcayabilir için gereksinim duyduğunuz, veri kaynaklarını bulmasına kolaylaştırmak yetenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="86394-159">Azure Data Catalog provides capabilities that make it easier to discover the data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="86394-160">Kayıtlı aramalar ve kullanıcılar ile art arda çalıştıkları veri kaynaklarını kolayca tanıyacak şekilde varlıklar bu çekirdek özellikler yapı veri sabitlenir.</span><span class="sxs-lookup"><span data-stu-id="86394-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
