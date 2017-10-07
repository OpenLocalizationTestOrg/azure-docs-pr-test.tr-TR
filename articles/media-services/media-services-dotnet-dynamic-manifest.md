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
# <a name="creating-filters-with-azure-media-services-net-sdk"></a>Azure Media Services .NET SDK ile Filtre Oluşturma
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

2.11 sürümünden başlayarak, Media Services, varlıklarınızı için toodefine filtreler sağlar. Bu filtreler müşterilerinizin gibi toochoose toodo şeyleri izin veren sunucu tarafı kurallardır: kayıttan yürütme (yerine hello tüm video oynatma), bir video yalnızca bir bölümünü veya yalnızca bir alt kümesini, müşterinizin aygıt işleyebileceğini (ses ve video yorumlama belirtin Tüm hello yorumlama yerine hello varlık ile ilişkili olan). Bu varlıklarınızı filtreleme aracılığıyla elde edilen **dinamik bildirim**müşterinizin isteği toostream bir video oluşturulan s tabanlı üzerinde belirtilen filtreler.

Daha ayrıntılı bilgi için bkz: ilgili toofilters ve dinamik bildirimini [dinamik bildirimleri genel bakış](media-services-dynamic-manifest-overview.md).

Bu konu, nasıl toouse Media Services .NET SDK'sı toocreate, güncelleştirme ve filtreleri silmek gösterir. 

Bir filtre güncelleştirirseniz, Yukarı Akış uç noktası toorefresh hello kuralları too2 dakika sürebilir unutmayın. Hello içerik bu filtre kullanarak sunulduğu (ve proxy'ler ve CDN önbellekleri önbelleğe alınmış), bu filtre güncelleştiriliyor player hatalarına neden olabilir. Bu tooclear hello önbellek hello filtre güncelleştirdikten sonra önerilir. Bu seçenek yoksa, başka bir filtre kullanmayı düşünün. 

## <a name="types-used-toocreate-filters"></a>Toocreate filtreleri türleri kullanılır
Merhaba aşağıdaki türleri filtreleri oluşturulurken kullanılır: 

* **IStreamingFilter**.  Bu tür REST API aşağıdaki hello üzerinde temel [filtresi](https://docs.microsoft.com/rest/api/media/operations/filter)
* **IStreamingAssetFilter**. Bu tür REST API aşağıdaki hello üzerinde temel [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* **PresentationTimeRange**. Bu tür REST API aşağıdaki hello üzerinde temel [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* **FilterTrackSelectStatement** ve **IFilterTrackPropertyCondition**. REST API'leri aşağıdaki hello üzerinde temel alarak bu tür [FilterTrackSelect ve FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

## <a name="createupdatereaddelete-global-filters"></a>Genel filtrelerin oluşturma/güncelleştirme/okuma/silme
Merhaba aşağıdaki kod nasıl toouse .NET toocreate güncelleştirmek için okuma ve varlık filtreleri silmek gösterir.

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


## <a name="createupdatereaddelete-asset-filters"></a>Oluşturma/güncelleştirme/okuma/silme varlık filtreleri
Merhaba aşağıdaki kod nasıl toouse .NET toocreate güncelleştirmek için okuma ve varlık filtreleri silmek gösterir.

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




## <a name="build-streaming-urls-that-use-filters"></a>Akış filtreleri kullanın URL'lerini derleme
Nasıl toopublish ve teslim varlıklarınızı, bkz. bilgi [teslim içerik tooCustomers genel bakış](media-services-deliver-content-overview.md).

Merhaba Aşağıdaki örnekler nasıl tooadd akış URL'lerini tooyour filtreleri gösterir.

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HTTP canlı akış (HLS) V4**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HTTP canlı akış (HLS) V3**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**Kesintisiz akış**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Ayrıca Bkz.
[Dinamik bildirimleri genel bakış](media-services-dynamic-manifest-overview.md)

