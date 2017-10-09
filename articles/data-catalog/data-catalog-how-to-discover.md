---
title: "Azure veri Kataloğu'ndaki aaaHow toodiscover veri kaynaklarında | Microsoft Docs"
description: "Bu makalede nasıl toodiscover aramayı ve filtrelemeyi de dahil olmak üzere Azure veri Kataloğu ile veri varlıklarını kayıtlı vurgular ve isabet vurgulama özelliklerini hello Azure veri Kataloğu portalını hello kullanarak."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: f72ae3a3-6573-4710-89a7-f13555e1968c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 624834b8895dd50c8931c9d3e6f8dc217927c617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodiscover-data-sources-in-azure-data-catalog"></a><span data-ttu-id="50c4d-103">Azure veri Kataloğu'nda nasıl toodiscover veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="50c4d-103">How toodiscover data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="50c4d-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="50c4d-104">Introduction</span></span>
<span data-ttu-id="50c4d-105">Azure veri Kataloğu kayıt ve bulma kurumsal veri kaynakları için bir sistem görevi gören bir tam olarak yönetilen bir bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="50c4d-105">Azure Data Catalog is a fully managed cloud service that serves as a system of registration and discovery for enterprise data sources.</span></span> <span data-ttu-id="50c4d-106">Diğer bir deyişle, Bul, anlamak ve veri kaynaklarını kullanan kişilerin veri Kataloğu yardımcı olur ve daha fazla değer, var olan verilerden alma kuruluşlar yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="50c4d-106">In other words, Data Catalog helps people discover, understand, and use data sources, and it helps organizations get more value from their existing data.</span></span> <span data-ttu-id="50c4d-107">Bir veri kaynağına veri Kataloğu ile kaydedildikten sonra böylece toodiscover hello verileri kolayca arayabilirsiniz meta verilerini hello hizmeti tarafından dizine alınır.</span><span class="sxs-lookup"><span data-stu-id="50c4d-107">After a data source is registered with Data Catalog, its metadata is indexed by hello service, so that you can easily search toodiscover hello data you need.</span></span>

## <a name="searching-and-filtering"></a><span data-ttu-id="50c4d-108">Arama ve filtreleme</span><span class="sxs-lookup"><span data-stu-id="50c4d-108">Searching and filtering</span></span>
<span data-ttu-id="50c4d-109">Veri Kataloğu bulma işlemi iki birincil mekanizmayı kullanır: arama ve filtreleme.</span><span class="sxs-lookup"><span data-stu-id="50c4d-109">Discovery in Data Catalog uses two primary mechanisms: searching and filtering.</span></span>

<span data-ttu-id="50c4d-110">Arama hem sezgisel hem de güçlü tasarlanmış toobe olur.</span><span class="sxs-lookup"><span data-stu-id="50c4d-110">Searching is designed toobe both intuitive and powerful.</span></span> <span data-ttu-id="50c4d-111">Varsayılan olarak, arama terimleri kullanıcı tarafından ek açıklamalar dahil olmak üzere hello kataloğunda herhangi bir özellikle eşleştirilir.</span><span class="sxs-lookup"><span data-stu-id="50c4d-111">By default, search terms are matched against any property in hello catalog, including user-provided annotations.</span></span>

<span data-ttu-id="50c4d-112">Filtreleme tasarlanmıştır toocomplement arama.</span><span class="sxs-lookup"><span data-stu-id="50c4d-112">Filtering is designed toocomplement searching.</span></span> <span data-ttu-id="50c4d-113">Uzmanlar, veri kaynağı türü, nesne türü ve etiketler gibi belirli özellikleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c4d-113">You can select specific characteristics such as experts, data source type, object type, and tags.</span></span> <span data-ttu-id="50c4d-114">Yalnızca eşleşen veri varlıklarını görüntülemek ve arama sonuçları toomatching varlıklar sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="50c4d-114">You can view only matching data assets, and constrain search results toomatching assets.</span></span>

<span data-ttu-id="50c4d-115">Arama ve filtreleme, bir birleşimini kullanarak, gereksinim duyduğunuz veri Kataloğu toodiscover hello veri kaynaklarıyla kayıtlı hello veri kaynaklarına hızlıca gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c4d-115">By using a combination of searching and filtering, you can quickly navigate hello data sources that have been registered with Data Catalog toodiscover hello data sources you need.</span></span>

## <a name="search-syntax"></a><span data-ttu-id="50c4d-116">Söz dizimi arama</span><span class="sxs-lookup"><span data-stu-id="50c4d-116">Search syntax</span></span>
<span data-ttu-id="50c4d-117">Merhaba varsayılan serbest metin arama basit ve sezgisel olsa da, veri kataloğu arama söz dizimi hello arama sonuçları üzerinde daha fazla denetim için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50c4d-117">Although hello default free text search is simple and intuitive, you can also use Data Catalog search syntax for greater control over hello search results.</span></span> <span data-ttu-id="50c4d-118">Teknikleri izleyerek veri kataloğu arama destekler hello:</span><span class="sxs-lookup"><span data-stu-id="50c4d-118">Data Catalog search supports hello following techniques:</span></span>

| <span data-ttu-id="50c4d-119">Teknik</span><span class="sxs-lookup"><span data-stu-id="50c4d-119">Technique</span></span> | <span data-ttu-id="50c4d-120">Kullanım</span><span class="sxs-lookup"><span data-stu-id="50c4d-120">Use</span></span> | <span data-ttu-id="50c4d-121">Örnek</span><span class="sxs-lookup"><span data-stu-id="50c4d-121">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50c4d-122">Basit Arama</span><span class="sxs-lookup"><span data-stu-id="50c4d-122">Basic search</span></span> |<span data-ttu-id="50c4d-123">Bir veya daha fazla arama terimi kullanan basit arama.</span><span class="sxs-lookup"><span data-stu-id="50c4d-123">Basic search that uses one or more search terms.</span></span> <span data-ttu-id="50c4d-124">Sonuçlar herhangi bir özelliği bir veya daha fazla belirtilen hello koşulları ile eşleşen tüm varlıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="50c4d-124">Results are any assets that match any property with one or more of hello terms specified.</span></span> |`sales data` |
| <span data-ttu-id="50c4d-125">Özellik kapsamı</span><span class="sxs-lookup"><span data-stu-id="50c4d-125">Property scoping</span></span> |<span data-ttu-id="50c4d-126">Belirtilen özelliği yalnızca dönüş veri kaynaklarının nerede hello arama terimi hello ile eşleştirilir.</span><span class="sxs-lookup"><span data-stu-id="50c4d-126">Return only data sources where hello search term is matched with hello specified property.</span></span> |`name:finance` |
| <span data-ttu-id="50c4d-127">Boole işleçleri</span><span class="sxs-lookup"><span data-stu-id="50c4d-127">Boolean operators</span></span> |<span data-ttu-id="50c4d-128">Genişletmek veya bir aramayı Boole işleçleri kullanarak daraltın.</span><span class="sxs-lookup"><span data-stu-id="50c4d-128">Broaden or narrow a search by using Boolean operations.</span></span> |`finance NOT corporate` |
| <span data-ttu-id="50c4d-129">Parantez ile gruplandırma</span><span class="sxs-lookup"><span data-stu-id="50c4d-129">Grouping with parenthesis</span></span> |<span data-ttu-id="50c4d-130">Parantez toogroup bölümleri hello sorgu tooachieve mantıksal ayırma, özellikle Boole işleçleri ile birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="50c4d-130">Use parentheses toogroup parts of hello query tooachieve logical isolation, especially in conjunction with Boolean operators.</span></span> |`name:finance AND (tags:Q1 OR tags:Q2)` |
| <span data-ttu-id="50c4d-131">Karşılaştırma işleçleri</span><span class="sxs-lookup"><span data-stu-id="50c4d-131">Comparison operators</span></span> |<span data-ttu-id="50c4d-132">Sayısal ve tarih veri türlerine sahip özellikler için eşitlik dışındaki karşılaştırmaları kullanın.</span><span class="sxs-lookup"><span data-stu-id="50c4d-132">Use comparisons other than equality for properties that have numeric and date data types.</span></span> |`modifiedTime > "11/05/2014"` |

<span data-ttu-id="50c4d-133">Veri kataloğu arama hakkında daha fazla bilgi için bkz: Merhaba [Azure veri Kataloğu](https://msdn.microsoft.com/library/azure/mt267594.aspx) makalesi.</span><span class="sxs-lookup"><span data-stu-id="50c4d-133">For more information about Data Catalog search, see hello [Azure Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) article.</span></span>

## <a name="hit-highlighting"></a><span data-ttu-id="50c4d-134">İsabet vurgulama</span><span class="sxs-lookup"><span data-stu-id="50c4d-134">Hit highlighting</span></span>
<span data-ttu-id="50c4d-135">Arama sonuçları görüntülediğinizde, herhangi bir belirtilen hello eşleşen özelliklere görüntülenen arama terimleri (örneğin, hello veri varlık adı, açıklama ve etiketleri) olan vurgulanan toomake, verilen veri varlık tarafından verilen bir arama döndürülen neden daha kolay tooidentify.</span><span class="sxs-lookup"><span data-stu-id="50c4d-135">When you view search results, any displayed properties that match hello specified search terms (such as hello data asset name, description, and tags) are highlighted toomake it easier tooidentify why a given data asset was returned by a given search.</span></span>

> [!NOTE]
> <span data-ttu-id="50c4d-136">isabet vurgulama, kullanım hello kapalı tooturn **vurgulayın** hello veri Kataloğu portalında geçin.</span><span class="sxs-lookup"><span data-stu-id="50c4d-136">tooturn off hit highlighting, use hello **Highlight** switch in hello Data Catalog portal.</span></span>
>
>

<span data-ttu-id="50c4d-137">Arama sonuçları görüntülediğinizde, bir veri varlığına bile isabet etkin vurgulama içindedir neden bu her zaman belirgin olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="50c4d-137">When you view search results, it might not always be obvious why a data asset is included, even with hit highlighting enabled.</span></span> <span data-ttu-id="50c4d-138">Tüm özellikleri varsayılan olarak aranır olduğundan, bir veri varlığına bir eşleşme nedeniyle bir sütun düzeyinde özellik döndürülmesi.</span><span class="sxs-lookup"><span data-stu-id="50c4d-138">Because all properties are searched by default, a data asset might be returned because of a match on a column-level property.</span></span> <span data-ttu-id="50c4d-139">Ve birden çok kullanıcı kendi etiketleri ve açıklamaları ile kayıtlı veri varlıklarına açıklama çünkü tüm meta veri hello arama sonuçları listesinde görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="50c4d-139">And because multiple users can annotate registered data assets with their own tags and descriptions, not all metadata might be displayed in hello list of search results.</span></span>

<span data-ttu-id="50c4d-140">Merhaba varsayılan döşeme görünümü'nde hello arama sonuçlarında görüntülenen her bölme içerir bir **görünüm arama terimini** simgesi istiyorsanız, hızlı bir şekilde hello sayısı eşleşiyor ve konum ve toojump toothem görüntüleyebilmesi için.</span><span class="sxs-lookup"><span data-stu-id="50c4d-140">In hello default tile view, each tile displayed in hello search results includes a **View search term matches** icon, so that you can quickly view hello number of matches and their location, and toojump toothem if you want.</span></span>

 ![İsabet vurgulama ve hello Azure veri Kataloğu Portalı'nda arama sonuçları](./media/data-catalog-how-to-discover/search-matches.png)

## <a name="summary"></a><span data-ttu-id="50c4d-142">Özet</span><span class="sxs-lookup"><span data-stu-id="50c4d-142">Summary</span></span>
<span data-ttu-id="50c4d-143">Veri Kataloğu kopyalarla yapısal ve açıklayıcı bir veri kaynağı kaydetme çünkü hello veri meta verilerini kaynak toohello katalog hizmeti, hello veri kaynağını daha kolay toodiscover haline gelir ve anlama.</span><span class="sxs-lookup"><span data-stu-id="50c4d-143">Because registering a data source with Data Catalog copies structural and descriptive metadata from hello data source toohello catalog service, hello data source becomes easier toodiscover and understand.</span></span> <span data-ttu-id="50c4d-144">Bir veri kaynağı kaydınız sonra filtreleme kullanarak bulmak ve gelen hello veri Kataloğu portalını arayın.</span><span class="sxs-lookup"><span data-stu-id="50c4d-144">After you've registered a data source, you can discover it by using filtering and search from within hello Data Catalog portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50c4d-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="50c4d-145">Next steps</span></span>
* <span data-ttu-id="50c4d-146">Hakkında adım adım ayrıntılar için toodiscover veri kaynaklarını görmek [Azure veri Kataloğu ile çalışmaya başlama](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="50c4d-146">For step-by-step details about how toodiscover data sources, see [Get Started with Azure Data Catalog](data-catalog-get-started.md).</span></span>
