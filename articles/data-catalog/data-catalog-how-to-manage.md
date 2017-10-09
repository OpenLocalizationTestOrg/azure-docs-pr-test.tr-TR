---
title: "Azure veri Kataloğu aaaManage veri varlıklarını | Microsoft Docs"
description: "Merhaba makale nasıl toocontrol görünürlük ve veri varlıklarının sahipliğini Azure veri Kataloğu'nda kayıtlı vurgular."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="7c7db-103">Azure veri Kataloğu'nda veri varlıklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="7c7db-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="7c7db-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="7c7db-104">Introduction</span></span>
<span data-ttu-id="7c7db-105">Böylece kolayca bulmak ve tooperform analiz gerekir ve kararları hello veri kaynaklarını anlamasına azure veri Kataloğu veri kaynağı bulma için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7c7db-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand hello data sources you need tooperform analysis and make decisions.</span></span> <span data-ttu-id="7c7db-106">Sizin ve diğer kullanıcıların bulmak ve kullanılabilir veri kaynaklarını çok çeşitli hello anlamak bulma yeteneklere hello büyük etkisi olun.</span><span class="sxs-lookup"><span data-stu-id="7c7db-106">These discovery capabilities make hello biggest impact when you and other users can find and understand hello broadest range of available data sources.</span></span> <span data-ttu-id="7c7db-107">Bu öğeleri aklınızda tüm kayıtlı veri kaynaklarının toobe görünür tooand bulunabilirlik tüm katalog kullanıcıları tarafından veri Kataloğu'nun hello varsayılan davranışı içindir.</span><span class="sxs-lookup"><span data-stu-id="7c7db-107">With these elements in mind, hello default behavior of Data Catalog is for all registered data sources toobe visible tooand discoverable by all catalog users.</span></span>

<span data-ttu-id="7c7db-108">Veri Kataloğu verme, erişim toohello verileri kendisi.</span><span class="sxs-lookup"><span data-stu-id="7c7db-108">Data Catalog does not give you access toohello data itself.</span></span> <span data-ttu-id="7c7db-109">Veri erişimi hello veri kaynağı hello sahibi tarafından denetlenir.</span><span class="sxs-lookup"><span data-stu-id="7c7db-109">Data access is controlled by hello owner of hello data source.</span></span> <span data-ttu-id="7c7db-110">Veri Kataloğu ile veri kaynaklarını bulmasına ve hello kataloğa kayıtlı bir ilgili toohello kaynak hello meta verileri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c7db-110">With Data Catalog, you can discover data sources and view hello metadata that's related toohello sources that are registered in hello catalog.</span></span>

<span data-ttu-id="7c7db-111">Burada veri kaynakları yalnızca görünür toospecific kullanıcılar veya belirli grupların toomembers olmalıdır durumlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="7c7db-111">There might be situations, however, where data sources should only be visible toospecific users, or toomembers of specific groups.</span></span> <span data-ttu-id="7c7db-112">Bu senaryolarda, kullanıcılar hello katalog içindeki kayıtlı veri kaynaklarının sahipliğini almak ve hello oldukları hello kaynakların güvenilirliğini denetlemek.</span><span class="sxs-lookup"><span data-stu-id="7c7db-112">In such scenarios, users can take ownership of registered data assets within hello catalog and then control hello visibility of hello assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="7c7db-113">Bu makalede açıklanan hello işlevi yalnızca hello, Azure veri Kataloğu standart sürümü kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7c7db-113">hello functionality described in this article is available only in hello Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="7c7db-114">Merhaba ücretsiz sürüm sahipliği ve veri varlık görünürlüğü kısıtlamak için özellikleri sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="7c7db-114">hello Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="7c7db-115">Veri varlıklarının sahipliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="7c7db-115">Manage ownership of data assets</span></span>
<span data-ttu-id="7c7db-116">Varsayılan olarak, veri Kataloğu'nda kayıtlı veri varlıklarını sahipsiz.</span><span class="sxs-lookup"><span data-stu-id="7c7db-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="7c7db-117">Herhangi bir kullanıcı izni tooaccess hello Kataloğu ile bulabilir ve bu varlıklarına açıklama.</span><span class="sxs-lookup"><span data-stu-id="7c7db-117">Any user with permission tooaccess hello catalog can discover and annotate these assets.</span></span> <span data-ttu-id="7c7db-118">Kullanıcılar, sahipsiz veri varlıklarının sahipliğini ve hello oldukları hello varlıklarının görünürlüğünü sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="7c7db-118">Users can take ownership of unowned data assets and then limit hello visibility of hello assets they own.</span></span>

<span data-ttu-id="7c7db-119">Veri Kataloğu'ndaki bir veri varlığına ait olduğunda, yalnızca hello sahipleri tarafından yetkilendirilmiş kullanıcılar hello varlık bulmak ve meta verilerini görüntülemek ve yalnızca hello sahipleri hello varlık hello Kataloğu'ndan silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c7db-119">When a data asset in Data Catalog is owned, only users who are authorized by hello owners can discover hello asset and view its metadata, and only hello owners can delete hello asset from hello catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="7c7db-120">Veri Kataloğu sahipliği hello kataloğunda depolanmış hello meta etkiler.</span><span class="sxs-lookup"><span data-stu-id="7c7db-120">Ownership in Data Catalog affects only hello metadata that's stored in hello catalog.</span></span> <span data-ttu-id="7c7db-121">Sahipliği hello temel alınan veri kaynağında tüm izinleri confer değil.</span><span class="sxs-lookup"><span data-stu-id="7c7db-121">Ownership does not confer any permissions on hello underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="7c7db-122">Sahipliği alın</span><span class="sxs-lookup"><span data-stu-id="7c7db-122">Take ownership</span></span>
<span data-ttu-id="7c7db-123">Kullanıcılar, hello seçerek veri varlıklarının sahipliğini alabilir **Sahipliği Al** hello veri Kataloğu portalında seçeneği.</span><span class="sxs-lookup"><span data-stu-id="7c7db-123">Users can take ownership of data assets by selecting hello **Take Ownership** option in hello Data Catalog portal.</span></span> <span data-ttu-id="7c7db-124">Özel izinler gerekli tootake sahipliğini sahipsiz veri varlığına ' dir.</span><span class="sxs-lookup"><span data-stu-id="7c7db-124">No special permissions are required tootake ownership of an unowned data asset.</span></span> <span data-ttu-id="7c7db-125">Herhangi bir kullanıcı bir sahipsiz veri varlığı sahipliğini alabilir.</span><span class="sxs-lookup"><span data-stu-id="7c7db-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="7c7db-126">Sahipleri ve ikincil sahipler ekleme</span><span class="sxs-lookup"><span data-stu-id="7c7db-126">Add owners and co-owners</span></span>
<span data-ttu-id="7c7db-127">Bir veri varlığına zaten sahip değilse, diğer kullanıcıların yalnızca Sahiplik alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="7c7db-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="7c7db-128">Bunlar birlikte sahipleri olarak var olan bir sahibi tarafından eklenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c7db-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="7c7db-129">Tüm sahibi ikincil sahip ek kullanıcı veya güvenlik grupları ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="7c7db-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="7c7db-130">Bu en iyi yöntem toohave herhangi bir veri varlığına ait sahipleri olarak en az iki kişiler aranır.</span><span class="sxs-lookup"><span data-stu-id="7c7db-130">It is a best practice toohave at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="7c7db-131">Sahipleri Kaldır</span><span class="sxs-lookup"><span data-stu-id="7c7db-131">Remove owners</span></span>
<span data-ttu-id="7c7db-132">Tüm varlık sahibi ikincil sahip eklemeniz yeterlidir gibi tüm varlık sahibi tüm ikincil sahip kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c7db-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="7c7db-133">Bir sahibi olarak kendisine veya kendisini kaldırır bir varlık sahibi artık hello varlık yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c7db-133">An asset owner who removes him or herself as an owner can no longer manage hello asset.</span></span> <span data-ttu-id="7c7db-134">Merhaba varlık sahibinin sahibi olarak kendisine veya kendisini kaldırır ve diğer ortak sahip yoktur, hello varlık durumu sahipsiz tooan döner.</span><span class="sxs-lookup"><span data-stu-id="7c7db-134">If hello asset owner removes him or herself as an owner and there are no other co-owners, hello asset reverts tooan unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="7c7db-135">Denetim görünürlüğü</span><span class="sxs-lookup"><span data-stu-id="7c7db-135">Control visibility</span></span>
<span data-ttu-id="7c7db-136">Veri varlığına sahipleri hello oldukları hello veri varlıklarının görünürlüğünü kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c7db-136">Data-asset owners can control hello visibility of hello data assets they own.</span></span> <span data-ttu-id="7c7db-137">toorestrict görünürlüğü hello varsayılan olarak, tüm veri Kataloğu kullanıcıları bulmak ve görünüm veri varlığına hello burada hello varlık sahibi değiştirmek hello görünürlük ayarından **herkesin** çok**sahipler ve bu kullanıcılar** hello özelliklerinde hello varlık.</span><span class="sxs-lookup"><span data-stu-id="7c7db-137">toorestrict visibility as hello default, where all Data Catalog users can discover and view hello data asset, hello asset owner can toggle hello visibility setting from **Everyone** too**Owners & These Users** in hello properties for hello asset.</span></span> <span data-ttu-id="7c7db-138">Sahipleri, belirli kullanıcılar ve güvenlik grupları daha sonra ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c7db-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="7c7db-139">Mümkün olduğunda, varlık sahipliği ve görünürlük izinleri toosecurity grupları ve tooindividual kullanıcıları değil atanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c7db-139">Whenever possible, asset ownership and visibility permissions should be assigned toosecurity groups and not tooindividual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="7c7db-140">Katalog yöneticileri</span><span class="sxs-lookup"><span data-stu-id="7c7db-140">Catalog administrators</span></span>
<span data-ttu-id="7c7db-141">Veri Kataloğu yöneticileri örtük olarak hello katalogdaki tüm varlıkları ikincil sahip olur.</span><span class="sxs-lookup"><span data-stu-id="7c7db-141">Data Catalog administrators are implicitly co-owners of all assets in hello catalog.</span></span> <span data-ttu-id="7c7db-142">Varlık sahipleri görünürlük yöneticileri kaldıramazsınız ve yöneticiler sahipliği ve tüm veri varlıklarını hello kataloğunda görünürlük yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="7c7db-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in hello catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="7c7db-143">Özet</span><span class="sxs-lookup"><span data-stu-id="7c7db-143">Summary</span></span>
<span data-ttu-id="7c7db-144">Merhaba veri Kataloğu kitle kaynak modeli toometadata ve veri varlık bulma tüm katalog kullanıcıları toocontribute sağlar ve keşfedin.</span><span class="sxs-lookup"><span data-stu-id="7c7db-144">hello Data Catalog crowdsourcing model toometadata and data asset discovery allows all catalog users toocontribute and discover.</span></span> <span data-ttu-id="7c7db-145">Merhaba, veri Kataloğu standart sürümü, sahipliği ve Yönetimi toolimit hello görünürlük ve belirli veri varlıklarını kullanımı için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7c7db-145">hello Standard Edition of Data Catalog is designed for ownership and management toolimit hello visibility and use of specific data assets.</span></span>
