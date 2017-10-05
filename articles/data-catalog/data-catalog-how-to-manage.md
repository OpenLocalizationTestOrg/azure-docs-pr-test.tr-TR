---
title: "Azure veri Kataloğu'nda veri varlıklarını yönetme | Microsoft Docs"
description: "Makaleyi görünürlük ve Azure veri Kataloğu'nda kayıtlı veri varlıklarının sahipliğini denetleme vurgular."
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
ms.openlocfilehash: 8b9159b7bc4f7b2dac12d9012c6c903e75a6ac16
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a><span data-ttu-id="2915c-103">Azure veri Kataloğu'nda veri varlıklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="2915c-103">Manage data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="2915c-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="2915c-104">Introduction</span></span>
<span data-ttu-id="2915c-105">Böylece kolayca bulmak ve analiz gerçekleştirmek ve kararlar için gereken veri kaynaklarını anlamasına azure veri Kataloğu veri kaynağı bulma için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2915c-105">Azure Data Catalog is designed for data-source discovery, so that you can easily discover and understand the data sources you need to perform analysis and make decisions.</span></span> <span data-ttu-id="2915c-106">Sizin ve diğer kullanıcıların bulmak ve kullanılabilir veri kaynakları çok çeşitli anlamak bulma yeteneklere büyük etkisi olun.</span><span class="sxs-lookup"><span data-stu-id="2915c-106">These discovery capabilities make the biggest impact when you and other users can find and understand the broadest range of available data sources.</span></span> <span data-ttu-id="2915c-107">Aklınızda bu öğeler ile görünür ve tüm katalog kullanıcıları tarafından bulunabilir olması için tüm kayıtlı veri kaynakları veri Kataloğu varsayılan davranışını içindir.</span><span class="sxs-lookup"><span data-stu-id="2915c-107">With these elements in mind, the default behavior of Data Catalog is for all registered data sources to be visible to and discoverable by all catalog users.</span></span>

<span data-ttu-id="2915c-108">Veri Kataloğu, veri erişim sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="2915c-108">Data Catalog does not give you access to the data itself.</span></span> <span data-ttu-id="2915c-109">Veri erişimini veri kaynağının sahibi tarafından denetlenir.</span><span class="sxs-lookup"><span data-stu-id="2915c-109">Data access is controlled by the owner of the data source.</span></span> <span data-ttu-id="2915c-110">Veri Kataloğu ile veri kaynaklarını bulmasına ve kataloğa kayıtlı kaynaklarla ilgili meta verileri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2915c-110">With Data Catalog, you can discover data sources and view the metadata that's related to the sources that are registered in the catalog.</span></span>

<span data-ttu-id="2915c-111">Burada veri kaynaklarının yalnızca belirli kullanıcılara veya belirli grupların üyelerine görünmesi gereken durumlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="2915c-111">There might be situations, however, where data sources should only be visible to specific users, or to members of specific groups.</span></span> <span data-ttu-id="2915c-112">Kullanıcılar bu senaryolarda katalog içindeki kayıtlı veri varlıklarının sahipliğini ve sahip olduğunuz kaynakların güvenilirliğini denetlemek.</span><span class="sxs-lookup"><span data-stu-id="2915c-112">In such scenarios, users can take ownership of registered data assets within the catalog and then control the visibility of the assets they own.</span></span>

> [!NOTE]
> <span data-ttu-id="2915c-113">Bu makalede açıklanan işlevselliği, yalnızca, Azure veri Kataloğu standart sürümü kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2915c-113">The functionality described in this article is available only in the Standard Edition of Azure Data Catalog.</span></span> <span data-ttu-id="2915c-114">Ücretsiz sürüm sahipliği ve kısıtlama veri varlığına görünürlük yeteneklerini sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="2915c-114">The Free Edition does not provide capabilities for ownership and restricting data-asset visibility.</span></span>
>
>

## <a name="manage-ownership-of-data-assets"></a><span data-ttu-id="2915c-115">Veri varlıklarının sahipliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="2915c-115">Manage ownership of data assets</span></span>
<span data-ttu-id="2915c-116">Varsayılan olarak, veri Kataloğu'nda kayıtlı veri varlıklarını sahipsiz.</span><span class="sxs-lookup"><span data-stu-id="2915c-116">By default, data assets that are registered in Data Catalog are unowned.</span></span> <span data-ttu-id="2915c-117">Kataloğu'na erişmek için izne sahip herhangi bir kullanıcı bulmak ve bu varlıklarına açıklama.</span><span class="sxs-lookup"><span data-stu-id="2915c-117">Any user with permission to access the catalog can discover and annotate these assets.</span></span> <span data-ttu-id="2915c-118">Kullanıcılar, sahipsiz veri varlıklarının sahipliğini ve sahip olduğunuz kaynakların güvenilirliğini sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="2915c-118">Users can take ownership of unowned data assets and then limit the visibility of the assets they own.</span></span>

<span data-ttu-id="2915c-119">Veri Kataloğu'ndaki bir veri varlığına ait olduğunda, yalnızca sahipleri tarafından yetkilendirilmiş kullanıcılar varlık bulmak ve meta verilerini görüntülemek ve yalnızca sahiplerinin varlık Kataloğu'ndan silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2915c-119">When a data asset in Data Catalog is owned, only users who are authorized by the owners can discover the asset and view its metadata, and only the owners can delete the asset from the catalog.</span></span>

> [!NOTE]
> <span data-ttu-id="2915c-120">Veri Kataloğu sahipliği kataloğunda depolanan meta veriler etkiler.</span><span class="sxs-lookup"><span data-stu-id="2915c-120">Ownership in Data Catalog affects only the metadata that's stored in the catalog.</span></span> <span data-ttu-id="2915c-121">Sahipliği temel alınan veri kaynağında tüm izinleri confer değil.</span><span class="sxs-lookup"><span data-stu-id="2915c-121">Ownership does not confer any permissions on the underlying data source.</span></span>
>
>

### <a name="take-ownership"></a><span data-ttu-id="2915c-122">Sahipliği alın</span><span class="sxs-lookup"><span data-stu-id="2915c-122">Take ownership</span></span>
<span data-ttu-id="2915c-123">Kullanıcılar, seçerek veri varlıklarının sahipliğini alabilir **Sahipliği Al** veri Kataloğu portalında seçeneği.</span><span class="sxs-lookup"><span data-stu-id="2915c-123">Users can take ownership of data assets by selecting the **Take Ownership** option in the Data Catalog portal.</span></span> <span data-ttu-id="2915c-124">Özel izinler sahipsiz veri varlığına sahipliğini almak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2915c-124">No special permissions are required to take ownership of an unowned data asset.</span></span> <span data-ttu-id="2915c-125">Herhangi bir kullanıcı bir sahipsiz veri varlığı sahipliğini alabilir.</span><span class="sxs-lookup"><span data-stu-id="2915c-125">Any user can take ownership of an unowned data asset.</span></span>

### <a name="add-owners-and-co-owners"></a><span data-ttu-id="2915c-126">Sahipleri ve ikincil sahipler ekleme</span><span class="sxs-lookup"><span data-stu-id="2915c-126">Add owners and co-owners</span></span>
<span data-ttu-id="2915c-127">Bir veri varlığına zaten sahip değilse, diğer kullanıcıların yalnızca Sahiplik alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="2915c-127">If a data asset is already owned, other users cannot simply take ownership.</span></span> <span data-ttu-id="2915c-128">Bunlar birlikte sahipleri olarak var olan bir sahibi tarafından eklenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2915c-128">They must be added as co-owners by an existing owner.</span></span> <span data-ttu-id="2915c-129">Tüm sahibi ikincil sahip ek kullanıcı veya güvenlik grupları ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="2915c-129">Any owner can add additional users or security groups as co-owners.</span></span>

> [!NOTE]
> <span data-ttu-id="2915c-130">Herhangi bir ait veri varlığını sahiplerini olarak en az iki kişiler için iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="2915c-130">It is a best practice to have at least two individuals as owners for any owned data asset.</span></span>
>
>

### <a name="remove-owners"></a><span data-ttu-id="2915c-131">Sahipleri Kaldır</span><span class="sxs-lookup"><span data-stu-id="2915c-131">Remove owners</span></span>
<span data-ttu-id="2915c-132">Tüm varlık sahibi ikincil sahip eklemeniz yeterlidir gibi tüm varlık sahibi tüm ikincil sahip kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2915c-132">Just as any asset owner can add co-owners, any asset owner can remove any co-owner.</span></span>

<span data-ttu-id="2915c-133">Bir sahibi olarak kendisine veya kendisini kaldırır bir varlık sahibi artık varlık yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2915c-133">An asset owner who removes him or herself as an owner can no longer manage the asset.</span></span> <span data-ttu-id="2915c-134">Varlık sahibinin sahibi olarak kendisine veya kendisini kaldırır ve diğer ortak sahip yoktur, varlık sahipsiz durumuna geri döner.</span><span class="sxs-lookup"><span data-stu-id="2915c-134">If the asset owner removes him or herself as an owner and there are no other co-owners, the asset reverts to an unowned state.</span></span>

## <a name="control-visibility"></a><span data-ttu-id="2915c-135">Denetim görünürlüğü</span><span class="sxs-lookup"><span data-stu-id="2915c-135">Control visibility</span></span>
<span data-ttu-id="2915c-136">Veri varlığına sahip oldukları veri varlıklarının görünürlüğünü kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2915c-136">Data-asset owners can control the visibility of the data assets they own.</span></span> <span data-ttu-id="2915c-137">Burada tüm veri Kataloğu kullanıcıları bulmak ve veri varlığına görüntülemek, varsayılan olarak görünürlüğü kısıtlamak için varlık sahibinin görünürlük ayarından geçiş yapabilirsiniz **herkesin** için **sahipler ve bu kullanıcılar** içinde Varlık özellikleri.</span><span class="sxs-lookup"><span data-stu-id="2915c-137">To restrict visibility as the default, where all Data Catalog users can discover and view the data asset, the asset owner can toggle the visibility setting from **Everyone** to **Owners & These Users** in the properties for the asset.</span></span> <span data-ttu-id="2915c-138">Sahipleri, belirli kullanıcılar ve güvenlik grupları daha sonra ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2915c-138">Owners can then add specific users and security groups.</span></span>

> [!NOTE]
> <span data-ttu-id="2915c-139">Mümkün olduğunda, varlık sahipliği ve görünürlük izinleri güvenlik gruplarına bireysel kullanıcılara atanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2915c-139">Whenever possible, asset ownership and visibility permissions should be assigned to security groups and not to individual users.</span></span>
>
>

## <a name="catalog-administrators"></a><span data-ttu-id="2915c-140">Katalog yöneticileri</span><span class="sxs-lookup"><span data-stu-id="2915c-140">Catalog administrators</span></span>
<span data-ttu-id="2915c-141">Veri Kataloğu yöneticileri örtük olarak katalogdaki tüm varlıkları ikincil sahip olur.</span><span class="sxs-lookup"><span data-stu-id="2915c-141">Data Catalog administrators are implicitly co-owners of all assets in the catalog.</span></span> <span data-ttu-id="2915c-142">Varlık sahipleri görünürlük yöneticileri kaldıramazsınız ve yöneticiler sahipliği ve tüm veri varlıklarını kataloğunda görünürlük yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="2915c-142">Asset owners cannot remove visibility from administrators, and administrators can manage ownership and visibility for all data assets in the catalog.</span></span>

## <a name="summary"></a><span data-ttu-id="2915c-143">Özet</span><span class="sxs-lookup"><span data-stu-id="2915c-143">Summary</span></span>
<span data-ttu-id="2915c-144">Meta veri ve veri varlık bulma için veri Kataloğu kitle kaynak modeli katkıda ve bulmak tüm katalog kullanıcıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="2915c-144">The Data Catalog crowdsourcing model to metadata and data asset discovery allows all catalog users to contribute and discover.</span></span> <span data-ttu-id="2915c-145">, Veri Kataloğu standart sürümü, görünürlük ve belirli veri varlıklarını kullanımını sınırlamak için sahipliği ve yönetimi için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2915c-145">The Standard Edition of Data Catalog is designed for ownership and management to limit the visibility and use of specific data assets.</span></span>
