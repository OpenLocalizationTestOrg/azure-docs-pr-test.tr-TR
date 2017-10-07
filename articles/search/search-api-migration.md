---
title: "Azure Search Hizmeti REST API sürümü 2016-09-01 aaaUpgrading toohello | Microsoft Docs"
description: "Azure Search Hizmeti REST API sürümü 2016-09-01 toohello yükseltme"
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
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="72635-103">Azure Search Hizmeti REST API sürümü 2016-09-01 toohello yükseltme</span><span class="sxs-lookup"><span data-stu-id="72635-103">Upgrading toohello Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="72635-104">Sürüm 2015-02-28 veya 2015-02-28-Önizleme hello birini kullanıyorsanız, [Azure Search Hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx), bu makalede, uygulama toouse hello sonraki genel olarak kullanılabilir API sürümü, 2016-09-01 yükseltmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="72635-104">If you're using version 2015-02-28 or 2015-02-28-Preview of hello [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application toouse hello next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="72635-105">Sürüm 2016-09-01 hello REST API, önceki sürümlerinden bazı değişiklikler içerir.</span><span class="sxs-lookup"><span data-stu-id="72635-105">Version 2016-09-01 of hello REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="72635-106">Kodunuzu değiştirmeden önce kullandığınız bağlı olarak hangi sürümün yalnızca en az çaba istemeniz gerekir böylece bunlar çoğunlukla geriye dönük uyumludur.</span><span class="sxs-lookup"><span data-stu-id="72635-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="72635-107">Bkz: [adımları tooupgrade](#UpgradeSteps) yönelik yönergeler toochange, kod toouse hello yeni API sürümü.</span><span class="sxs-lookup"><span data-stu-id="72635-107">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="72635-108">Azure Search Hizmeti örneğinizi hello en son dahil olmak üzere birkaç REST API sürümlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="72635-108">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="72635-109">En son Merhaba, ancak, kod toouse hello en yeni sürüme geçirmek öneririz artık olduğunda toouse bir sürüm devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72635-109">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="72635-110">Sürüm 2016-09-01 yenilikler</span><span class="sxs-lookup"><span data-stu-id="72635-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="72635-111">Sürüm 2016-09-01 hello ikinci genel olarak kullanılabilir hello Azure Search Hizmeti REST API'si sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="72635-111">Version 2016-09-01 is hello second generally available release of hello Azure Search Service REST API.</span></span> <span data-ttu-id="72635-112">Bu API sürümündeki yeni özellikler içerir:</span><span class="sxs-lookup"><span data-stu-id="72635-112">New features in this API version include:</span></span>

* <span data-ttu-id="72635-113">[Özel çözümleyiciler](https://aka.ms/customanalyzers), hangi izin dizine ve aranabilir belirteçlere metin dönüştürme işleminin hello üzerinde tootake denetim.</span><span class="sxs-lookup"><span data-stu-id="72635-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you tootake control over hello process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="72635-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) ve [Azure Table Storage](search-howto-indexing-azure-tables.md) tooeasily izin dizin oluşturucular içeri aktarma verileri Azure depolama alanından Azure Search bir zamanlama veya isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="72635-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you tooeasily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="72635-115">[Alan eşlemeleri](search-indexer-field-mappings.md), hangi izin toocustomize nasıl dizin oluşturucular verileri Azure Search alın.</span><span class="sxs-lookup"><span data-stu-id="72635-115">[Field mappings](search-indexer-field-mappings.md), which allow you toocustomize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="72635-116">Etag'ler bir eşzamanlılık güvenli şekilde tooupdate hello tanımları dizinler, dizin oluşturucular ve veri kaynaklarını izin verir.</span><span class="sxs-lookup"><span data-stu-id="72635-116">ETags, which allow you tooupdate hello definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="72635-117">Adımları tooupgrade</span><span class="sxs-lookup"><span data-stu-id="72635-117">Steps tooupgrade</span></span>
<span data-ttu-id="72635-118">2015-02-28 sürümünden yükseltme yapıyorsanız, büyük olasılıkla toochange hello sürüm numarası dışındaki tüm değişiklikleri tooyour kod toomake olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="72635-118">If you are upgrading from version 2015-02-28, you probably won't have toomake any changes tooyour code, other than toochange hello version number.</span></span> <span data-ttu-id="72635-119">Merhaba yalnızca durumlar toochange kod gerekebilir ne zaman şunlardır:</span><span class="sxs-lookup"><span data-stu-id="72635-119">hello only situations in which you may need toochange code are when:</span></span>

* <span data-ttu-id="72635-120">Tanınmayan özellikleri bir API yanıt döndürüldüğünde kod başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="72635-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="72635-121">Varsayılan olarak, uygulamanızın anlamadığı özellikleri yok saymanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="72635-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="72635-122">Kodunuzu API istekleri devam ederse ve tooresend çalışır bunları toohello yeni API sürümü.</span><span class="sxs-lookup"><span data-stu-id="72635-122">Your code persists API requests and tries tooresend them toohello new API version.</span></span> <span data-ttu-id="72635-123">Uygulamanızı hello arama API döndürülen devamlılık belirteçleri devam ederse, örneğin, bu durum oluşabilir (daha fazla bilgi için Ara `@search.nextPageParameters` hello içinde [arama API Başvurusu](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="72635-123">For example, this might happen if your application persists continuation tokens returned from hello Search API (for more information, look for `@search.nextPageParameters` in hello [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="72635-124">Ardından bu durumlardan birini tooyou uygularsanız, toochange uygun şekilde kodunuzu gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="72635-124">If either of these situations apply tooyou, then you may need toochange your code accordingly.</span></span> <span data-ttu-id="72635-125">Hello kullanarak toostart istemediğiniz sürece Aksi halde, hiçbir değişiklik gerekli olmalıdır [yeni özellikler](#WhatsNew) 2016-09-01 sürümü.</span><span class="sxs-lookup"><span data-stu-id="72635-125">Otherwise, no changes should be necessary unless you want toostart using hello [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="72635-126">Sürüm 2015-02-28-Önizlemesi'nden yükseltiyorsanız, yukarıdaki hello için de geçerlidir, ancak bazı Önizleme özellikleri 2016-09-01 sürümünde mevcut olmayan farkında olmanız da gerekir:</span><span class="sxs-lookup"><span data-stu-id="72635-126">If you are upgrading from version 2015-02-28-Preview, hello above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="72635-127">CSV dosyaları ve JSON dizileri içeren BLOB'lar için Azure Blob Storage dizin oluşturucu desteği.</span><span class="sxs-lookup"><span data-stu-id="72635-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="72635-128">Eş anlamlıları</span><span class="sxs-lookup"><span data-stu-id="72635-128">Synonyms</span></span>
* <span data-ttu-id="72635-129">"Bu gibi daha fazla" sorguları</span><span class="sxs-lookup"><span data-stu-id="72635-129">"More like this" queries</span></span>

<span data-ttu-id="72635-130">Kodunuzu bu özellikleri kullanıyorsa, mümkün tooupgrade too2016-09-bunları kullanımınızı kaldırma olmadan 01 olmaz.</span><span class="sxs-lookup"><span data-stu-id="72635-130">If your code uses these features, you will not be able tooupgrade too2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72635-131">Lütfen unutmayın, Önizleme API'leri sınama ve değerlendirme için tasarlanmıştır ve üretim ortamlarında kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="72635-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="72635-132">Sonuç</span><span class="sxs-lookup"><span data-stu-id="72635-132">Conclusion</span></span>
<span data-ttu-id="72635-133">Hello Azure Search Hizmeti REST API kullanma hakkında daha fazla ayrıntı ihtiyacınız varsa, en son güncelleştirilen hello bkz [API Başvurusu](https://msdn.microsoft.com/library/azure/dn798935.aspx) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="72635-133">If you need more details on using hello Azure Search Service REST API, see hello recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="72635-134">Azure Search'te bildiriminiz bizim.</span><span class="sxs-lookup"><span data-stu-id="72635-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="72635-135">Sorunlarla karşılaşırsanız, ücretsiz tooask bize hello hakkında Yardım için eşitleyerek [Azure arama MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) veya [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="72635-135">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="72635-136">Azure hakkında soru soran StackOverflow, yapma emin tootag ile arama `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="72635-136">If you're asking a question about Azure Search on StackOverflow, make sure tootag it with `azure-search`.</span></span>

<span data-ttu-id="72635-137">Azure Search kullandığınız için teşekkür ederiz!</span><span class="sxs-lookup"><span data-stu-id="72635-137">Thank you for using Azure Search!</span></span>

