---
title: Azure Media Services REST API aaaCreating filtrelerle | Microsoft Docs
description: "Bu konuda, istemci bir akış belirli bölümlerine toostream kullanabilmeniz için nasıl toocreate filtreler açıklanmaktadır. Media Services, dinamik bildirimleri tooachieve Bu seçmeli akış oluşturur."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f7d23daf-7cd2-49c7-a195-ab902912ab3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: d0b5af3b193b35f22ac70887963c2f0a06b60bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="9d0e5-104">İle Azure Media Services REST API filtreleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d0e5-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9d0e5-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9d0e5-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="9d0e5-106">REST</span><span class="sxs-lookup"><span data-stu-id="9d0e5-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="9d0e5-107">2.11 sürümünden başlayarak, Media Services, varlıklarınızı için toodefine filtreler sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d0e5-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="9d0e5-108">Bu filtreler müşterilerinizin gibi toochoose toodo şeyleri izin veren sunucu tarafı kurallardır: kayıttan yürütme (yerine hello tüm video oynatma), bir video yalnızca bir bölümünü veya yalnızca bir alt kümesini, müşterinizin aygıt işleyebileceğini (ses ve video yorumlama belirtin Tüm hello yorumlama yerine hello varlık ile ilişkili olan).</span><span class="sxs-lookup"><span data-stu-id="9d0e5-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="9d0e5-109">Bu varlıklarınızı filtreleme aracılığıyla arşivlenmiş **dinamik bildirim**müşterinizin isteği toostream bir video oluşturulan s tabanlı üzerinde belirtilen filtreler.</span><span class="sxs-lookup"><span data-stu-id="9d0e5-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="9d0e5-110">Daha ayrıntılı bilgi için bkz: ilgili toofilters ve dinamik bildirimini [dinamik bildirimleri genel bakış](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9d0e5-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="9d0e5-111">Bu konu, nasıl toouse REST API'leri toocreate, güncelleştirme ve filtreleri silmek gösterir.</span><span class="sxs-lookup"><span data-stu-id="9d0e5-111">This topic shows how toouse REST APIs toocreate, update, and delete filters.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="9d0e5-112">Toocreate filtreleri türleri kullanılır</span><span class="sxs-lookup"><span data-stu-id="9d0e5-112">Types used toocreate filters</span></span>
<span data-ttu-id="9d0e5-113">Merhaba aşağıdaki türleri filtreleri oluşturulurken kullanılır:</span><span class="sxs-lookup"><span data-stu-id="9d0e5-113">hello following types are used when creating filters:</span></span>  

* [<span data-ttu-id="9d0e5-114">Filtre</span><span class="sxs-lookup"><span data-stu-id="9d0e5-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="9d0e5-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="9d0e5-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="9d0e5-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="9d0e5-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="9d0e5-117">FilterTrackSelect ve FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="9d0e5-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="9d0e5-118">Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d0e5-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="9d0e5-119">Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="9d0e5-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="9d0e5-120">TooMedia Hizmetleri'ne Bağlama</span><span class="sxs-lookup"><span data-stu-id="9d0e5-120">Connect tooMedia Services</span></span>

<span data-ttu-id="9d0e5-121">Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="9d0e5-121">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="9d0e5-122">Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="9d0e5-122">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="9d0e5-123">Sonraki çağrılar toohello yapmanız gereken yeni bir URI.</span><span class="sxs-lookup"><span data-stu-id="9d0e5-123">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="9d0e5-124">Filtre oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d0e5-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="9d0e5-125">Genel filtrelerin oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d0e5-125">Create global Filters</span></span>
<span data-ttu-id="9d0e5-126">toocreate genel bir filtre HTTP isteklerini aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9d0e5-126">toocreate a global Filter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="9d0e5-127">HTTP isteği</span><span class="sxs-lookup"><span data-stu-id="9d0e5-127">HTTP Request</span></span>
<span data-ttu-id="9d0e5-128">İstek üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="9d0e5-128">Request Headers</span></span>

    POST https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host:media.windows.net 

<span data-ttu-id="9d0e5-129">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="9d0e5-129">Request body</span></span> 

    {  
       "Name":"GlobalFilter",
       "PresentationTimeRange":{  
          "StartTimestamp":"0",
          "EndTimestamp":"9223372036854775807",
          "PresentationWindowDuration":"12000000000",
          "LiveBackoffDuration":"0",
          "Timescale":"10000000"
       },
       "Tracks":[  
          {  
             "PropertyConditions":
                  [  
                {  
                   "Property":"Type",
                   "Value":"audio",
                   "Operator":"Equal"
                },
                {  
                   "Property":"Bitrate",
                   "Value":"0-2147483647",
                   "Operator":"Equal"
                }
             ]
          }
       ]
    }




#### <a name="http-response"></a><span data-ttu-id="9d0e5-130">HTTP yanıtı</span><span class="sxs-lookup"><span data-stu-id="9d0e5-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="9d0e5-131">Yerel AssetFilters oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d0e5-131">Create local AssetFilters</span></span>
<span data-ttu-id="9d0e5-132">toocreate yerel AssetFilter HTTP isteklerini aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9d0e5-132">toocreate a local AssetFilter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="9d0e5-133">HTTP isteği</span><span class="sxs-lookup"><span data-stu-id="9d0e5-133">HTTP Request</span></span>
<span data-ttu-id="9d0e5-134">İstek üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="9d0e5-134">Request Headers</span></span>

    POST https://media.windows.net/API/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net  

<span data-ttu-id="9d0e5-135">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="9d0e5-135">Request body</span></span> 

    {   
       "Name":"AssetFilter", 
       "ParentAssetId":"nb:cid:UUID:536e555d-1500-80c3-92dc-f1e4fdc6c592", 
       "PresentationTimeRange":{   
          "StartTimestamp":"0", 
          "EndTimestamp":"9223372036854775807", 
          "PresentationWindowDuration":"12000000000", 
          "LiveBackoffDuration":"0", 
          "Timescale":"10000000" 
       }, 
       "Tracks":[   
          {   
             "PropertyConditions": 
                  [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

#### <a name="http-response"></a><span data-ttu-id="9d0e5-136">HTTP yanıtı</span><span class="sxs-lookup"><span data-stu-id="9d0e5-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="9d0e5-137">Filtreleri Listele</span><span class="sxs-lookup"><span data-stu-id="9d0e5-137">List filters</span></span>
### <a name="get-all-global-filters-in-hello-ams-account"></a><span data-ttu-id="9d0e5-138">Tüm genel alma **filtre**hello AMS hesabının s</span><span class="sxs-lookup"><span data-stu-id="9d0e5-138">Get all global **Filter**s in hello AMS account</span></span>
<span data-ttu-id="9d0e5-139">toolist filtreleri, HTTP isteklerini aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9d0e5-139">toolist filters, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="9d0e5-140">HTTP isteği</span><span class="sxs-lookup"><span data-stu-id="9d0e5-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="9d0e5-141">Alma **AssetFilter**bir varlıkla ilişkilendirilen s</span><span class="sxs-lookup"><span data-stu-id="9d0e5-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="9d0e5-142">HTTP isteği</span><span class="sxs-lookup"><span data-stu-id="9d0e5-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="9d0e5-143">Alma bir **AssetFilter** kimliğine göre</span><span class="sxs-lookup"><span data-stu-id="9d0e5-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="9d0e5-144">HTTP isteği</span><span class="sxs-lookup"><span data-stu-id="9d0e5-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="9d0e5-145">Güncelleştirme filtreleri</span><span class="sxs-lookup"><span data-stu-id="9d0e5-145">Update filters</span></span>
<span data-ttu-id="9d0e5-146">Kullanım düzeltme eki, PUT veya birleştirme tooupdate yeni özellik değerlerinin sahip bir filtre.</span><span class="sxs-lookup"><span data-stu-id="9d0e5-146">Use PATCH, PUT or MERGE tooupdate a filter with new property values.</span></span>  <span data-ttu-id="9d0e5-147">Bu işlemler hakkında daha fazla bilgi için bkz: [düzeltme eki, YERLEŞTİRME, birleştirme](http://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d0e5-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="9d0e5-148">Bir filtre güncelleştirirseniz, Yukarı Akış uç noktası toorefresh hello kuralları too2 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="9d0e5-148">If you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="9d0e5-149">Hello içerik bu filtre kullanarak sunulduğu (ve proxy'ler ve CDN önbellekleri önbelleğe alınmış), bu filtre güncelleştiriliyor player hatalarına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="9d0e5-149">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="9d0e5-150">Bu tooclear hello önbellek hello filtre güncelleştirdikten sonra önerilir.</span><span class="sxs-lookup"><span data-stu-id="9d0e5-150">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="9d0e5-151">Bu seçenek yoksa, başka bir filtre kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="9d0e5-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="9d0e5-152">Genel filtrelerin güncelleştir</span><span class="sxs-lookup"><span data-stu-id="9d0e5-152">Update global Filters</span></span>
<span data-ttu-id="9d0e5-153">tooupdate genel bir filtre HTTP isteklerini aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9d0e5-153">tooupdate a global filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="9d0e5-154">HTTP isteği</span><span class="sxs-lookup"><span data-stu-id="9d0e5-154">HTTP Request</span></span>
<span data-ttu-id="9d0e5-155">İstek üstbilgilerini:</span><span class="sxs-lookup"><span data-stu-id="9d0e5-155">Request headers:</span></span> 

    MERGE https://media.windows.net/API/Filters('filterName') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 
    Content-Length: 384

<span data-ttu-id="9d0e5-156">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="9d0e5-156">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

### <a name="update-local-assetfilters"></a><span data-ttu-id="9d0e5-157">Yerel AssetFilters güncelleştir</span><span class="sxs-lookup"><span data-stu-id="9d0e5-157">Update local AssetFilters</span></span>
<span data-ttu-id="9d0e5-158">yerel bir filtre tooupdate HTTP isteklerini aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="9d0e5-158">tooupdate a local filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="9d0e5-159">HTTP isteği</span><span class="sxs-lookup"><span data-stu-id="9d0e5-159">HTTP Request</span></span>
<span data-ttu-id="9d0e5-160">İstek üstbilgilerini:</span><span class="sxs-lookup"><span data-stu-id="9d0e5-160">Request headers:</span></span> 

    MERGE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter')  HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

<span data-ttu-id="9d0e5-161">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="9d0e5-161">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 


## <a name="delete-filters"></a><span data-ttu-id="9d0e5-162">Filtreleri Sil</span><span class="sxs-lookup"><span data-stu-id="9d0e5-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="9d0e5-163">Genel filtrelerin Sil</span><span class="sxs-lookup"><span data-stu-id="9d0e5-163">Delete global Filters</span></span>
<span data-ttu-id="9d0e5-164">toodelete genel bir filtre HTTP isteklerini aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9d0e5-164">toodelete a global Filter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="9d0e5-165">HTTP isteği</span><span class="sxs-lookup"><span data-stu-id="9d0e5-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="9d0e5-166">Yerel AssetFilters Sil</span><span class="sxs-lookup"><span data-stu-id="9d0e5-166">Delete local AssetFilters</span></span>
<span data-ttu-id="9d0e5-167">toodelete yerel AssetFilter HTTP isteklerini aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9d0e5-167">toodelete a local AssetFilter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="9d0e5-168">HTTP isteği</span><span class="sxs-lookup"><span data-stu-id="9d0e5-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="9d0e5-169">Akış filtreleri kullanın URL'lerini derleme</span><span class="sxs-lookup"><span data-stu-id="9d0e5-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="9d0e5-170">Nasıl toopublish ve teslim varlıklarınızı, bkz. bilgi [teslim içerik tooCustomers genel bakış](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9d0e5-170">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="9d0e5-171">Merhaba Aşağıdaki örnekler nasıl tooadd akış URL'lerini tooyour filtreleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="9d0e5-171">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="9d0e5-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="9d0e5-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="9d0e5-173">**Apple HTTP canlı akış (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="9d0e5-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="9d0e5-174">**Apple HTTP canlı akış (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="9d0e5-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="9d0e5-175">**Kesintisiz akış**</span><span class="sxs-lookup"><span data-stu-id="9d0e5-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="9d0e5-176">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="9d0e5-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9d0e5-177">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="9d0e5-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="9d0e5-178">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9d0e5-178">See Also</span></span>
[<span data-ttu-id="9d0e5-179">Dinamik bildirimleri genel bakış</span><span class="sxs-lookup"><span data-stu-id="9d0e5-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

