---
title: "aaaHow tooview ilgili Azure veri Kataloğu veri varlıklarını | Microsoft Docs"
description: "Bu makalede tooview seçilen veri varlığını Azure veri Kataloğu'nda, veri varlıklarını nasıl ilişkilendirileceğini açıklar."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="cc332-103">Azure veri Kataloğu veri varlıklarını tooview ilişkisini?</span><span class="sxs-lookup"><span data-stu-id="cc332-103">How tooview related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="cc332-104">Azure veri Kataloğu tooview veri varlıklarını Seçili ilgili tooa veri varlık ve görünüm aralarındaki ilişkilerin sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc332-104">Azure Data Catalog allows you tooview data assets related tooa selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="cc332-105">Desteklenen veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="cc332-105">Supported data sources</span></span> 
<span data-ttu-id="cc332-106">Veri kaynakları aşağıdaki hello veri varlıklarından kaydolduğunuzda, Azure veri Kataloğu seçili hello veri varlıklarını birleştirme ilişkilerini hakkındaki meta verileri otomatik olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="cc332-106">When you register data assets from hello following data sources, Azure Data Catalog automatically registers metadata about join relationships between hello selected data assets.</span></span> 

- <span data-ttu-id="cc332-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="cc332-107">SQL Server</span></span>
- <span data-ttu-id="cc332-108">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="cc332-108">Azure SQL Database</span></span>
- <span data-ttu-id="cc332-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="cc332-109">MySQL</span></span>
- <span data-ttu-id="cc332-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="cc332-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="cc332-111">İlgili veri varlıklarını görüntülemek</span><span class="sxs-lookup"><span data-stu-id="cc332-111">View related data assets</span></span>
<span data-ttu-id="cc332-112">Seçili ilgili tooa dataset olan tooview veri varlıklarını kullanmak hello **ilişkileri** sekmesinde hello görüntü aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="cc332-112">tooview data assets that are related tooa selected dataset, use hello **Relationships** tab as shown in hello following image:</span></span> 

![Azure veri Kataloğu - veri varlıklarını ilgili görüntüleyin](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="cc332-114">Bu örnekte, seçili Merhaba için iki ilişkisi vardır **ProductSubcategory** veri varlığına:</span><span class="sxs-lookup"><span data-stu-id="cc332-114">In this example, there are two relationships for hello selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="cc332-115">Merhaba ürün tablosunun ProductSubcategoryID sütunu seçili hello ProductSubcategory tablosunun ProductSubcategoryID sütunla yabancı anahtar ilişkisi vardır.</span><span class="sxs-lookup"><span data-stu-id="cc332-115">ProductSubcategoryID column of hello Product table has a foreign key relationship with ProductSubcategoryID column of hello selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="cc332-116">Merhaba ProductSubCategory tablosunun ProductCategoryID sütunu seçili hello ProductCategory tablosunun ProductCategoryID sütunla yabancı anahtar ilişkisi vardır.</span><span class="sxs-lookup"><span data-stu-id="cc332-116">ProductCategoryID column of hello ProductSubCategory table has a foreign key relationship with ProductCategoryID column of hello selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="cc332-117">Merhaba ok hello ilişkileri ağaç görünümünde Hello yönünü dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="cc332-117">Notice hello direction of hello arrow in hello relationships tree view.</span></span>  

<span data-ttu-id="cc332-118">toosee hello sütunun hello tam adı gibi daha fazla ayrıntı hello fare üzerine getirin ve görüntü aşağıdaki açılan benzer toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="cc332-118">toosee more details such as hello fully qualified name of hello column, move hello mouse over and you see a popup similar toohello following image:</span></span> 

![Azure veri Kataloğu - ilişki açılan](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="cc332-120">önceden kaydedilmiş olan varlıklar arasındaki ilişkiler tooinclude, bu varlıkları yeniden kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cc332-120">tooinclude relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc332-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cc332-121">Next steps</span></span>
- [<span data-ttu-id="cc332-122">Nasıl toomanage veri varlıklarını</span><span class="sxs-lookup"><span data-stu-id="cc332-122">How toomanage data assets</span></span>](data-catalog-how-to-manage.md)
