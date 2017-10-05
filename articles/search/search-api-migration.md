---
title: "Azure Search Hizmeti REST API'si için sürüm 2016-09-01 yükseltme | Microsoft Docs"
description: "Azure Search Hizmeti REST API'si için sürüm 2016-09-01 yükseltme"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: f6a189c2e314b91c490583a86d8bacca8ec78a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="1a289-103">Azure Search Hizmeti REST API'si için sürüm 2016-09-01 yükseltme</span><span class="sxs-lookup"><span data-stu-id="1a289-103">Upgrading to the Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="1a289-104">Sürüm 2015-02-28 veya 2015-02-28-Önizleme birini kullanıyorsanız, [Azure Search Hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx), bu makalede 2016-09-01 sonraki genel olarak kullanılabilir API sürümü kullanmak için uygulamanızı yükseltmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1a289-104">If you're using version 2015-02-28 or 2015-02-28-Preview of the [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application to use the next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="1a289-105">REST API sürümü 2016-09-01 önceki sürümlerinden bazı değişiklikler içerir.</span><span class="sxs-lookup"><span data-stu-id="1a289-105">Version 2016-09-01 of the REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="1a289-106">Kodunuzu değiştirmeden önce kullandığınız bağlı olarak hangi sürümün yalnızca en az çaba istemeniz gerekir böylece bunlar çoğunlukla geriye dönük uyumludur.</span><span class="sxs-lookup"><span data-stu-id="1a289-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="1a289-107">Bkz: [yükseltme adımları](#UpgradeSteps) yönelik yeni bir API sürümü kullanmak yönergeler kodunuzu değiştirmek.</span><span class="sxs-lookup"><span data-stu-id="1a289-107">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="1a289-108">Azure Search Hizmeti örneğinizi son de dahil olmak üzere birkaç REST API sürümlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="1a289-108">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="1a289-109">En son artık değildir, ancak en yeni sürümü kullanmak için kodunuzu geçirmek öneririz bir sürümünü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a289-109">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="1a289-110">Sürüm 2016-09-01 yenilikler</span><span class="sxs-lookup"><span data-stu-id="1a289-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="1a289-111">Sürüm 2016-09-01 ikinci genel olarak kullanılabilir Azure Search Hizmeti REST API'si sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="1a289-111">Version 2016-09-01 is the second generally available release of the Azure Search Service REST API.</span></span> <span data-ttu-id="1a289-112">Bu API sürümündeki yeni özellikler içerir:</span><span class="sxs-lookup"><span data-stu-id="1a289-112">New features in this API version include:</span></span>

* <span data-ttu-id="1a289-113">[Özel çözümleyiciler](https://aka.ms/customanalyzers), denetimini ele dizine ve aranabilir belirteçlere metin dönüştürme işlemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1a289-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you to take control over the process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="1a289-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) ve [Azure Table Storage](search-howto-indexing-azure-tables.md) kolayca verileri Azure depolama alanından Azure Search bir zamanlama veya isteğe bağlı almak izin dizin oluşturucular.</span><span class="sxs-lookup"><span data-stu-id="1a289-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you to easily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="1a289-115">[Alan eşlemeleri](search-indexer-field-mappings.md), hangi dizin oluşturucular verileri Azure Search nasıl içeri özelleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="1a289-115">[Field mappings](search-indexer-field-mappings.md), which allow you to customize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="1a289-116">Etag'ler, dizinler, dizin oluşturucular ve veri kaynaklarını tanımlarını bir eşzamanlılık güvenli şekilde güncelleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="1a289-116">ETags, which allow you to update the definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="1a289-117">Yükseltme adımları</span><span class="sxs-lookup"><span data-stu-id="1a289-117">Steps to upgrade</span></span>
<span data-ttu-id="1a289-118">2015-02-28 sürümünden yükseltme yapıyorsanız, kodunuz için dışında sürüm numarasını değiştirmek için değişiklik gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1a289-118">If you are upgrading from version 2015-02-28, you probably won't have to make any changes to your code, other than to change the version number.</span></span> <span data-ttu-id="1a289-119">Kodu değiştirmeniz gerekebilir yalnızca durumlar ne zaman şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1a289-119">The only situations in which you may need to change code are when:</span></span>

* <span data-ttu-id="1a289-120">Tanınmayan özellikleri bir API yanıt döndürüldüğünde kod başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="1a289-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="1a289-121">Varsayılan olarak, uygulamanızın anlamadığı özellikleri yok saymanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1a289-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="1a289-122">Kodunuzu API istekleri devam ederse ve yeni API sürümü yeniden göndermeyi dener.</span><span class="sxs-lookup"><span data-stu-id="1a289-122">Your code persists API requests and tries to resend them to the new API version.</span></span> <span data-ttu-id="1a289-123">Uygulamanızın arama API'den döndürülen devamlılık belirteçleri devam ederse, örneğin, bu durum oluşabilir (daha fazla bilgi için Ara `@search.nextPageParameters` içinde [arama API Başvurusu](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="1a289-123">For example, this might happen if your application persists continuation tokens returned from the Search API (for more information, look for `@search.nextPageParameters` in the [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="1a289-124">Bu durumlarda ya da sizin için geçerli değilse, kodunuzu uygun şekilde değiştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1a289-124">If either of these situations apply to you, then you may need to change your code accordingly.</span></span> <span data-ttu-id="1a289-125">Kullanmaya başlamak istemediğiniz sürece Aksi halde, hiçbir değişiklik gerekli olmalıdır [yeni özellikler](#WhatsNew) 2016-09-01 sürümü.</span><span class="sxs-lookup"><span data-stu-id="1a289-125">Otherwise, no changes should be necessary unless you want to start using the [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="1a289-126">Sürüm 2015-02-28-Önizlemesi'nden yükseltiyorsanız, yukarıdaki de geçerlidir, ancak bazı Önizleme özellikleri 2016-09-01 sürümünde mevcut olmayan farkında olmanız da gerekir:</span><span class="sxs-lookup"><span data-stu-id="1a289-126">If you are upgrading from version 2015-02-28-Preview, the above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="1a289-127">CSV dosyaları ve JSON dizileri içeren BLOB'lar için Azure Blob Storage dizin oluşturucu desteği.</span><span class="sxs-lookup"><span data-stu-id="1a289-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="1a289-128">Eş anlamlıları</span><span class="sxs-lookup"><span data-stu-id="1a289-128">Synonyms</span></span>
* <span data-ttu-id="1a289-129">"Bu gibi daha fazla" sorguları</span><span class="sxs-lookup"><span data-stu-id="1a289-129">"More like this" queries</span></span>

<span data-ttu-id="1a289-130">Kodunuzu bu özellikleri kullanıyorsa, bunları kullanımınızı kaldırmadan 2016-09-01 yükseltmeniz mümkün olmaz.</span><span class="sxs-lookup"><span data-stu-id="1a289-130">If your code uses these features, you will not be able to upgrade to 2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a289-131">Lütfen unutmayın, Önizleme API'leri sınama ve değerlendirme için tasarlanmıştır ve üretim ortamlarında kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="1a289-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="1a289-132">Sonuç</span><span class="sxs-lookup"><span data-stu-id="1a289-132">Conclusion</span></span>
<span data-ttu-id="1a289-133">Azure Search Hizmeti REST API'sini kullanarak hakkında daha fazla ayrıntı ihtiyacınız varsa, yeni güncelleştirilen bkz [API Başvurusu](https://msdn.microsoft.com/library/azure/dn798935.aspx) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="1a289-133">If you need more details on using the Azure Search Service REST API, see the recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="1a289-134">Azure Search'te bildiriminiz bizim.</span><span class="sxs-lookup"><span data-stu-id="1a289-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="1a289-135">Sorunlarla karşılaşırsanız, bize yardım isteyin çekinmeyin [Azure arama MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) veya [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="1a289-135">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="1a289-136">Azure Search hakkında bir soru üzerinde StackOverflow soran, kendisiyle etiketlemek emin olun `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="1a289-136">If you're asking a question about Azure Search on StackOverflow, make sure to tag it with `azure-search`.</span></span>

<span data-ttu-id="1a289-137">Azure Search kullandığınız için teşekkür ederiz!</span><span class="sxs-lookup"><span data-stu-id="1a289-137">Thank you for using Azure Search!</span></span>

