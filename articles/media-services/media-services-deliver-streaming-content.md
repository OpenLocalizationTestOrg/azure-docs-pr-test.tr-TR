---
title: ".NET kullanarak Azure Media Services içerik aaaPublish | Microsoft Docs"
description: "Bilgi nasıl toocreate kullanılan toobuild bir akış URL'si olan bir Bulucu. Kod örnekleri C# dilinde yazılmıştır ve .NET için Media Services SDK'sı hello kullanın."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: c53b1f83-4cb1-4b09-840f-9c145b7d6f8d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: c941cd93c252a96e66546cce2793bb426afac059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-net"></a><span data-ttu-id="d7933-104">.NET kullanarak Azure Media Services içerik yayımlama</span><span class="sxs-lookup"><span data-stu-id="d7933-104">Publish Azure Media Services content using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7933-105">REST</span><span class="sxs-lookup"><span data-stu-id="d7933-105">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="d7933-106">.NET</span><span class="sxs-lookup"><span data-stu-id="d7933-106">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="d7933-107">Portal</span><span class="sxs-lookup"><span data-stu-id="d7933-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="d7933-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d7933-108">Overview</span></span>
<span data-ttu-id="d7933-109">Bir OnDemand akış Bulucusu oluşturma ve akış URL'si oluşturma MP4 kümesine bir bit hızı Uyarlamalı akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7933-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="d7933-110">Merhaba [bir varlık kodlama](media-services-encode-asset.md) konu, bir bit hızı Uyarlamalı MP4 içine tooencode nasıl ayarlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d7933-110">hello [encoding an asset](media-services-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> 

> [!NOTE]
> <span data-ttu-id="d7933-111">İçeriğinizi şifrelenmişse, varlık teslim ilkesini yapılandırın (açıklandığı gibi [bu](media-services-dotnet-configure-asset-delivery-policy.md) konu) bir Bulucu oluşturmadan önce.</span><span class="sxs-lookup"><span data-stu-id="d7933-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-dotnet-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 
> 
> 

<span data-ttu-id="d7933-112">Bir OnDemand Bulucu toobuild URL'leri aşamalı olarak indirilebilir bu noktası tooMP4 dosyaları akış de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7933-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="d7933-113">Bu konuda gösterilmektedir nasıl toocreate bir OnDemand Bulucu toopublish varlık ve yapı düzgün, MPEG DASH ve akış URL'lerini HLS akış.</span><span class="sxs-lookup"><span data-stu-id="d7933-113">This topic shows how toocreate an OnDemand streaming locator toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="d7933-114">Ayrıca Dinamik toobuild aşamalı indirme URL'leri gösterir.</span><span class="sxs-lookup"><span data-stu-id="d7933-114">It also shows hot toobuild progressive download URLs.</span></span> 

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="d7933-115">Bir OnDemand akış Bulucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7933-115">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="d7933-116">toocreate OnDemand Bulucu akış hello ve URL'leri alma, şeyler aşağıdaki toodo hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="d7933-116">toocreate hello OnDemand streaming locator and get URLs, you need toodo hello following things:</span></span>

1. <span data-ttu-id="d7933-117">Merhaba içerik şifrelenmişse, bir erişim ilkesi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d7933-117">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="d7933-118">Bir OnDemand Bulucu akış oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d7933-118">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="d7933-119">Toostream planlıyorsanız, hello varlık bildirim dosyasında (.ism) akış hello alın.</span><span class="sxs-lookup"><span data-stu-id="d7933-119">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="d7933-120">Tooprogressively indirme planlıyorsanız, hello varlık MP4 dosyaları hello adlarını alır.</span><span class="sxs-lookup"><span data-stu-id="d7933-120">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span>  
4. <span data-ttu-id="d7933-121">URL'leri toohello bildirim dosyası veya MP4 dosyaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d7933-121">Build URLs toohello manifest file or MP4 files.</span></span> 


>[!NOTE]
><span data-ttu-id="d7933-122">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="d7933-122">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="d7933-123">Kullanım hello aynı her zaman kullanıyorsanız ilke kimliği hello aynı gün / erişim izinleri.</span><span class="sxs-lookup"><span data-stu-id="d7933-123">Use hello same policy ID if you are always using hello same days / access permissions.</span></span> <span data-ttu-id="d7933-124">Örneğin, uzun bir süre (karşıya yükleme olmayan ilkeleri) yerinde hedeflenen tooremain olan bulucular için ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="d7933-124">For example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="d7933-125">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="d7933-125">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

### <a name="use-media-services-net-sdk"></a><span data-ttu-id="d7933-126">Media Services .NET SDK'yı kullanın</span><span class="sxs-lookup"><span data-stu-id="d7933-126">Use Media Services .NET SDK</span></span>
<span data-ttu-id="d7933-127">Akış URL'leri derleme</span><span class="sxs-lookup"><span data-stu-id="d7933-127">Build Streaming URLs</span></span> 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator toohello streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference toohello streaming manifest file from hello  
        // collection of files in hello asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL toohello manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL toomanifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL toomanifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL toomanifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

<span data-ttu-id="d7933-128">Merhaba çıkarır:</span><span class="sxs-lookup"><span data-stu-id="d7933-128">hello outputs:</span></span>

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> <span data-ttu-id="d7933-129">Ayrıca, bir SSL bağlantısı üzerinden içeriğinizin akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7933-129">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="d7933-130">toodo bu yaklaşımını, HTTPS ile akış URL'leri başlatma emin olun.</span><span class="sxs-lookup"><span data-stu-id="d7933-130">toodo this approach, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="d7933-131">Şu anda AMS SSL ile özel etki alanlarını desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="d7933-131">Currently, AMS doesn’t support SSL with custom domains.</span></span>
> 
> 

<span data-ttu-id="d7933-132">Aşamalı indirme URL'leri derleme</span><span class="sxs-lookup"><span data-stu-id="d7933-132">Build progressive download URLs</span></span> 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator toohello asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL toohello MP4 files. Use this tooprogressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

<span data-ttu-id="d7933-133">Merhaba çıkarır:</span><span class="sxs-lookup"><span data-stu-id="d7933-133">hello outputs:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a><span data-ttu-id="d7933-134">Media Services .NET SDK uzantıları kullanma</span><span class="sxs-lookup"><span data-stu-id="d7933-134">Use Media Services .NET SDK Extensions</span></span>
<span data-ttu-id="d7933-135">Merhaba aşağıdaki kod bir Bulucu oluşturmanız ve Uyarlamalı akış için hello kesintisiz akış, HLS ve MPEG-DASH URL'ler oluşturmak .NET SDK uzantıları yöntemleri çağırır.</span><span class="sxs-lookup"><span data-stu-id="d7933-135">hello following code calls .NET SDK extensions methods that create a locator and generate hello Smooth Streaming, HLS, and MPEG-DASH URLs for adaptive streaming.</span></span>

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get hello streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a><span data-ttu-id="d7933-136">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="d7933-136">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d7933-137">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="d7933-137">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d7933-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d7933-138">Next steps</span></span>
* [<span data-ttu-id="d7933-139">Varlıklar indirin</span><span class="sxs-lookup"><span data-stu-id="d7933-139">Download assets</span></span>](media-services-deliver-asset-download.md)
* [<span data-ttu-id="d7933-140">Varlık teslim ilkesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d7933-140">Configure asset delivery policy</span></span>](media-services-dotnet-configure-asset-delivery-policy.md)

