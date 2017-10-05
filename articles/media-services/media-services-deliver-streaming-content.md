---
title: ".NET kullanarak Azure Media Services içerik yayımlama | Microsoft Docs"
description: "Bir akış URL'si oluşturmak için kullanılan bir Bulucu oluşturmayı öğrenin. Kod örnekleri, C# dilinde yazılmıştır ve .NET için Media Services SDK'sını kullanın."
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
ms.openlocfilehash: 2bcb012eef84faa7c1e13ed22e88e45e4300ed54
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-azure-media-services-content-using-net"></a><span data-ttu-id="5371d-104">.NET kullanarak Azure Media Services içerik yayımlama</span><span class="sxs-lookup"><span data-stu-id="5371d-104">Publish Azure Media Services content using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5371d-105">REST</span><span class="sxs-lookup"><span data-stu-id="5371d-105">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="5371d-106">.NET</span><span class="sxs-lookup"><span data-stu-id="5371d-106">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="5371d-107">Portal</span><span class="sxs-lookup"><span data-stu-id="5371d-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="5371d-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5371d-108">Overview</span></span>
<span data-ttu-id="5371d-109">Bir OnDemand akış Bulucusu oluşturma ve akış URL'si oluşturma MP4 kümesine bir bit hızı Uyarlamalı akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5371d-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="5371d-110">[Bir varlık kodlama](media-services-encode-asset.md) konu nasıl kodlanacağını Uyarlamalı bit hızlı MP4 kümesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="5371d-110">The [encoding an asset](media-services-encode-asset.md) topic shows how to encode into an adaptive bitrate MP4 set.</span></span> 

> [!NOTE]
> <span data-ttu-id="5371d-111">İçeriğinizi şifrelenmişse, varlık teslim ilkesini yapılandırın (açıklandığı gibi [bu](media-services-dotnet-configure-asset-delivery-policy.md) konu) bir Bulucu oluşturmadan önce.</span><span class="sxs-lookup"><span data-stu-id="5371d-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-dotnet-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 
> 
> 

<span data-ttu-id="5371d-112">Bir OnDemand Bulucu akış, aşamalı olarak indirilebilir MP4 dosyaları işaret URL'ler oluşturmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5371d-112">You can also use an OnDemand streaming locator to build URLs that point to MP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="5371d-113">Bu konuda bir OnDemand Bulucu, varlığı yayımlayın ve kesintisiz, MPEG DASH ve HLS akış URL'lerini oluşturmak için akış oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5371d-113">This topic shows how to create an OnDemand streaming locator to publish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="5371d-114">Aşamalı indirme URL'leri oluşturmak için etkin gösterir.</span><span class="sxs-lookup"><span data-stu-id="5371d-114">It also shows hot to build progressive download URLs.</span></span> 

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="5371d-115">Bir OnDemand akış Bulucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="5371d-115">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="5371d-116">OnDemand akış Bulucusu oluşturmak ve URL'leri almak için şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="5371d-116">To create the OnDemand streaming locator and get URLs, you need to do the following things:</span></span>

1. <span data-ttu-id="5371d-117">İçerik şifrelenmişse, bir erişim ilkesi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="5371d-117">If the content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="5371d-118">Bir OnDemand Bulucu akış oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5371d-118">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="5371d-119">Akış yapmayı planlıyorsanız, varlık içindeki akış bildirim dosyası (.ism) alın.</span><span class="sxs-lookup"><span data-stu-id="5371d-119">If you plan to stream, get the streaming manifest file (.ism) in the asset.</span></span> 
   
   <span data-ttu-id="5371d-120">Aşamalı indirmeyi planlıyorsanız, varlık MP4 dosyaları adlarını alır.</span><span class="sxs-lookup"><span data-stu-id="5371d-120">If you plan to progressively download, get the names of MP4 files in the asset.</span></span>  
4. <span data-ttu-id="5371d-121">URL'ler bildirim dosyası veya MP4 dosyaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5371d-121">Build URLs to the manifest file or MP4 files.</span></span> 


>[!NOTE]
><span data-ttu-id="5371d-122">Farklı AMS ilkeleri için sınır 1.000.000 ilkedir (örneğin, Bulucu ilkesi veya ContentKeyAuthorizationPolicy için).</span><span class="sxs-lookup"><span data-stu-id="5371d-122">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="5371d-123">Aynı gün / erişim izinleri her zaman aynı ilke kimliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="5371d-123">Use the same policy ID if you are always using the same days / access permissions.</span></span> <span data-ttu-id="5371d-124">Örneğin, ilkeleri kalmasına yerinde uzun bir süre (karşıya yükleme olmayan ilkeleri) yöneliktir bulucular için.</span><span class="sxs-lookup"><span data-stu-id="5371d-124">For example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="5371d-125">Daha fazla bilgi için [bu](media-services-dotnet-manage-entities.md#limit-access-policies) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="5371d-125">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

### <a name="use-media-services-net-sdk"></a><span data-ttu-id="5371d-126">Media Services .NET SDK'yı kullanın</span><span class="sxs-lookup"><span data-stu-id="5371d-126">Use Media Services .NET SDK</span></span>
<span data-ttu-id="5371d-127">Akış URL'leri derleme</span><span class="sxs-lookup"><span data-stu-id="5371d-127">Build Streaming URLs</span></span> 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator to the streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on the locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference to the streaming manifest file from the  
        // collection of files in the asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL to the manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL to manifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL to manifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL to manifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

<span data-ttu-id="5371d-128">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="5371d-128">The outputs:</span></span>

    URL to manifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL to manifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL to manifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> <span data-ttu-id="5371d-129">Ayrıca, bir SSL bağlantısı üzerinden içeriğinizin akışını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5371d-129">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="5371d-130">Bu yaklaşım yapmak için HTTPS ile akış URL'leri başlatma emin olun.</span><span class="sxs-lookup"><span data-stu-id="5371d-130">To do this approach, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="5371d-131">Şu anda AMS SSL ile özel etki alanlarını desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="5371d-131">Currently, AMS doesn’t support SSL with custom domains.</span></span>
> 
> 

<span data-ttu-id="5371d-132">Aşamalı indirme URL'leri derleme</span><span class="sxs-lookup"><span data-stu-id="5371d-132">Build progressive download URLs</span></span> 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator to the asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on the locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL to the MP4 files. Use this to progressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

<span data-ttu-id="5371d-133">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="5371d-133">The outputs:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a><span data-ttu-id="5371d-134">Media Services .NET SDK uzantıları kullanma</span><span class="sxs-lookup"><span data-stu-id="5371d-134">Use Media Services .NET SDK Extensions</span></span>
<span data-ttu-id="5371d-135">Aşağıdaki kod bir Bulucu oluşturmanız ve Uyarlamalı akış için kesintisiz akış, HLS ve MPEG-DASH URL'ler oluşturmak .NET SDK uzantıları yöntemleri çağırır.</span><span class="sxs-lookup"><span data-stu-id="5371d-135">The following code calls .NET SDK extensions methods that create a locator and generate the Smooth Streaming, HLS, and MPEG-DASH URLs for adaptive streaming.</span></span>

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get the streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a><span data-ttu-id="5371d-136">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="5371d-136">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5371d-137">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="5371d-137">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5371d-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5371d-138">Next steps</span></span>
* [<span data-ttu-id="5371d-139">Varlıklar indirin</span><span class="sxs-lookup"><span data-stu-id="5371d-139">Download assets</span></span>](media-services-deliver-asset-download.md)
* [<span data-ttu-id="5371d-140">Varlık teslim ilkesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5371d-140">Configure asset delivery policy</span></span>](media-services-dotnet-configure-asset-delivery-policy.md)

