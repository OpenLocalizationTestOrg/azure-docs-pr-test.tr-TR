---
title: "Azure Media Services .NET SDK'sı ile aaaCreating filtreleri"
description: "Bu konuda, istemci bir akış belirli bölümlerine toostream kullanabilmeniz için nasıl toocreate filtreler açıklanmaktadır. Media Services, dinamik bildirimleri tooachieve Bu seçmeli akış oluşturur."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2f6894ca-fb43-43c0-9151-ddbb2833cafd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 16d9497d48ab1d3f841dd97efb0f66016a2435c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="330c8-104">Azure Media Services .NET SDK ile Filtre Oluşturma</span><span class="sxs-lookup"><span data-stu-id="330c8-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="330c8-105">.NET</span><span class="sxs-lookup"><span data-stu-id="330c8-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="330c8-106">REST</span><span class="sxs-lookup"><span data-stu-id="330c8-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="330c8-107">2.11 sürümünden başlayarak, Media Services, varlıklarınızı için toodefine filtreler sağlar.</span><span class="sxs-lookup"><span data-stu-id="330c8-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="330c8-108">Bu filtreler müşterilerinizin gibi toochoose toodo şeyleri izin veren sunucu tarafı kurallardır: kayıttan yürütme (yerine hello tüm video oynatma), bir video yalnızca bir bölümünü veya yalnızca bir alt kümesini, müşterinizin aygıt işleyebileceğini (ses ve video yorumlama belirtin Tüm hello yorumlama yerine hello varlık ile ilişkili olan).</span><span class="sxs-lookup"><span data-stu-id="330c8-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="330c8-109">Bu varlıklarınızı filtreleme aracılığıyla elde edilen **dinamik bildirim**müşterinizin isteği toostream bir video oluşturulan s tabanlı üzerinde belirtilen filtreler.</span><span class="sxs-lookup"><span data-stu-id="330c8-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="330c8-110">Daha ayrıntılı bilgi için bkz: ilgili toofilters ve dinamik bildirimini [dinamik bildirimleri genel bakış](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="330c8-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="330c8-111">Bu konu, nasıl toouse Media Services .NET SDK'sı toocreate, güncelleştirme ve filtreleri silmek gösterir.</span><span class="sxs-lookup"><span data-stu-id="330c8-111">This topic shows how toouse Media Services .NET SDK toocreate, update, and delete filters.</span></span> 

<span data-ttu-id="330c8-112">Bir filtre güncelleştirirseniz, Yukarı Akış uç noktası toorefresh hello kuralları too2 dakika sürebilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="330c8-112">Note if you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="330c8-113">Hello içerik bu filtre kullanarak sunulduğu (ve proxy'ler ve CDN önbellekleri önbelleğe alınmış), bu filtre güncelleştiriliyor player hatalarına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="330c8-113">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="330c8-114">Bu tooclear hello önbellek hello filtre güncelleştirdikten sonra önerilir.</span><span class="sxs-lookup"><span data-stu-id="330c8-114">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="330c8-115">Bu seçenek yoksa, başka bir filtre kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="330c8-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="330c8-116">Toocreate filtreleri türleri kullanılır</span><span class="sxs-lookup"><span data-stu-id="330c8-116">Types used toocreate filters</span></span>
<span data-ttu-id="330c8-117">Merhaba aşağıdaki türleri filtreleri oluşturulurken kullanılır:</span><span class="sxs-lookup"><span data-stu-id="330c8-117">hello following types are used when creating filters:</span></span> 

* <span data-ttu-id="330c8-118">**IStreamingFilter**.</span><span class="sxs-lookup"><span data-stu-id="330c8-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="330c8-119">Bu tür REST API aşağıdaki hello üzerinde temel [filtresi](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="330c8-119">This type is based on hello following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="330c8-120">**IStreamingAssetFilter**.</span><span class="sxs-lookup"><span data-stu-id="330c8-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="330c8-121">Bu tür REST API aşağıdaki hello üzerinde temel [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="330c8-121">This type is based on hello following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="330c8-122">**PresentationTimeRange**.</span><span class="sxs-lookup"><span data-stu-id="330c8-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="330c8-123">Bu tür REST API aşağıdaki hello üzerinde temel [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="330c8-123">This type is based on hello following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="330c8-124">**FilterTrackSelectStatement** ve **IFilterTrackPropertyCondition**.</span><span class="sxs-lookup"><span data-stu-id="330c8-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="330c8-125">REST API'leri aşağıdaki hello üzerinde temel alarak bu tür [FilterTrackSelect ve FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="330c8-125">These types are based on hello following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="330c8-126">Genel filtrelerin oluşturma/güncelleştirme/okuma/silme</span><span class="sxs-lookup"><span data-stu-id="330c8-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="330c8-127">Merhaba aşağıdaki kod nasıl toouse .NET toocreate güncelleştirmek için okuma ve varlık filtreleri silmek gösterir.</span><span class="sxs-lookup"><span data-stu-id="330c8-127">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

    string filterName = "GlobalFilter_" + Guid.NewGuid().ToString();

    List<FilterTrackSelectStatement> filterTrackSelectStatements = new List<FilterTrackSelectStatement>();

    FilterTrackSelectStatement filterTrackSelectStatement = new FilterTrackSelectStatement();
    filterTrackSelectStatement.PropertyConditions = new List<IFilterTrackPropertyCondition>();
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackNameCondition("Track Name", FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackBitrateRangeCondition(new FilterTrackBitrateRange(0, 1), FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackTypeCondition(FilterTrackType.Audio, FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatements.Add(filterTrackSelectStatement);

    // Create
    IStreamingFilter filter = _context.Filters.Create(filterName, new PresentationTimeRange(), filterTrackSelectStatements);

    // Update
    filter.PresentationTimeRange = new PresentationTimeRange(timescale: 500);
    filter.Update();

    // Read
    var filterUpdated = _context.Filters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filter.Delete();


## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="330c8-128">Oluşturma/güncelleştirme/okuma/silme varlık filtreleri</span><span class="sxs-lookup"><span data-stu-id="330c8-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="330c8-129">Merhaba aşağıdaki kod nasıl toouse .NET toocreate güncelleştirmek için okuma ve varlık filtreleri silmek gösterir.</span><span class="sxs-lookup"><span data-stu-id="330c8-129">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

    string assetName = "AssetFilter_" + Guid.NewGuid().ToString();
    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

    string filterName = "AssetFilter_" + Guid.NewGuid().ToString();


    // Create
    IStreamingAssetFilter filter = asset.AssetFilters.Create(filterName,
                                        new PresentationTimeRange(), 
                                        new List<FilterTrackSelectStatement>());

    // Update
    filter.PresentationTimeRange = 
            new PresentationTimeRange(start: 6000000000, end: 72000000000);

    filter.Update();

    // Read
    asset = _context.Assets.Where(c => c.Id == asset.Id).FirstOrDefault();
    var filterUpdated = asset.AssetFilters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filterUpdated.Delete();




## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="330c8-130">Akış filtreleri kullanın URL'lerini derleme</span><span class="sxs-lookup"><span data-stu-id="330c8-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="330c8-131">Nasıl toopublish ve teslim varlıklarınızı, bkz. bilgi [teslim içerik tooCustomers genel bakış](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="330c8-131">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="330c8-132">Merhaba Aşağıdaki örnekler nasıl tooadd akış URL'lerini tooyour filtreleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="330c8-132">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="330c8-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="330c8-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="330c8-134">**Apple HTTP canlı akış (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="330c8-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="330c8-135">**Apple HTTP canlı akış (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="330c8-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="330c8-136">**Kesintisiz akış**</span><span class="sxs-lookup"><span data-stu-id="330c8-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="330c8-137">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="330c8-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="330c8-138">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="330c8-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="330c8-139">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="330c8-139">See Also</span></span>
[<span data-ttu-id="330c8-140">Dinamik bildirimleri genel bakış</span><span class="sxs-lookup"><span data-stu-id="330c8-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

