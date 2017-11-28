---
title: "aaaAzure Media Services sık sorulan sorular | Microsoft Docs"
description: "Sık sorulan sorular (SSS)"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="91236-103">Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="91236-103">Frequently asked questions</span></span>

<span data-ttu-id="91236-104">Bu makalede hello Azure Media Services (AMS) kullanıcı topluluğu tarafından gerçekleştirilen sık sorulan sorular giderir.</span><span class="sxs-lookup"><span data-stu-id="91236-104">This article addresses frequently asked questions raised by hello Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="91236-105">Genel AMS SSS</span><span class="sxs-lookup"><span data-stu-id="91236-105">General AMS FAQs</span></span>
<span data-ttu-id="91236-106">S: nasıl dizin ölçeklendirme?</span><span class="sxs-lookup"><span data-stu-id="91236-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="91236-107">Aşağıdakilere ayrılmış hello birimleri olan hello aynı kodlama ve görevleri dizin oluşturma için.</span><span class="sxs-lookup"><span data-stu-id="91236-107">A: hello reserved units are hello same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="91236-108">Yönergeleri izleyerek [nasıl tooScale kodlamaya ayrılan birimler](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="91236-108">Follow instructions on [How tooScale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="91236-109">**Not** dizin oluşturucu performans ayrılmış birim türü tarafından etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="91236-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="91236-110">S: karşıya kodlanmış ve video yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="91236-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="91236-111">Toostream çalıştığınızda hello neden hello video ne olacağını oynamaz onu?</span><span class="sxs-lookup"><span data-stu-id="91236-111">What would be hello reason hello video does not play when I try toostream it?</span></span>

<span data-ttu-id="91236-112">Y: birini en yaygın nedenlerinden olan akış uç noktası hello tooplayback içinden çalıştığınız hello sahip olmadığınız hello **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="91236-112">A: One of hello most common reasons is you do not have hello streaming endpoint from which you are trying tooplayback in hello **Running** state.</span></span>  

<span data-ttu-id="91236-113">S: bir canlı akış üzerinde birleştirme yapabilirim?</span><span class="sxs-lookup"><span data-stu-id="91236-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="91236-114">Y: birleştirme Canlı akışlar üzerinde şu anda değil sunulur Azure Media Services'de toopre gerekir böylece-bilgisayarınızda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="91236-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need toopre-compose on your computer.</span></span>

<span data-ttu-id="91236-115">S: Azure CDN canlı akış ile kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="91236-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="91236-116">Y: Media Services, Azure CDN ile tümleştirmeyi destekler (daha fazla bilgi için bkz: [nasıl tooManage akış uç noktalarını Media Services hesabı](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="91236-116">A: Media Services supports integration with Azure CDN (for more information, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="91236-117">Canlı akış CDN ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91236-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="91236-118">Azure Media Services, kesintisiz akış, HLS ve MPEG-DASH çıkışları sağlar.</span><span class="sxs-lookup"><span data-stu-id="91236-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="91236-119">Bu biçimler verileri aktarmak için HTTP kullanmasına ve HTTP önbelleğe alma avantajlarını elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="91236-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="91236-120">Bölünmüş toofragments gerçek video/ses veri akışı dinamik olarak ve bu tek tek parçaları CDN'de önbelleğe.</span><span class="sxs-lookup"><span data-stu-id="91236-120">In live streaming actual video/audio data is divided toofragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="91236-121">Yalnızca veri gereksinimlerini toobe yenilendi hello bildirim verilerdir.</span><span class="sxs-lookup"><span data-stu-id="91236-121">Only data needs toobe refreshed is hello manifest data.</span></span> <span data-ttu-id="91236-122">CDN bildirim verileri düzenli aralıklarla yeniler.</span><span class="sxs-lookup"><span data-stu-id="91236-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="91236-123">S: mu Azure Media services depolanmasını görüntüleri destekliyor?</span><span class="sxs-lookup"><span data-stu-id="91236-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="91236-124">A:, yalnızca toostore JPEG veya PNG görüntüleri arıyorsanız, Azure Blob Storage de tutmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="91236-124">A: If you are just looking toostore JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="91236-125">Video veya ses varlıklar ile ilişkili tookeep istemediğiniz sürece bunları Media Services hesap hiçbir avantajı tooputting yoktur.</span><span class="sxs-lookup"><span data-stu-id="91236-125">There is no benefit tooputting them in your Media Services account unless you want tookeep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="91236-126">Veya hello video Kodlayıcısı içindeki yer paylaşımları olarak gerek toouse hello görüntüleri olabilir. Medya Kodlayıcısı standart destekler videolar en üstünde yer paylaşımı görüntüler ve hangi JPEG ve desteklenen gibi PNG listeler olan giriş biçimleri.</span><span class="sxs-lookup"><span data-stu-id="91236-126">Or if you might have a need toouse hello images as overlays in hello video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="91236-127">Daha fazla bilgi için bkz: [oluşturma yer paylaşımları](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="91236-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="91236-128">S: nasıl miyim bir Media Services hesabı tooanother varlıklarını kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91236-128">Q: How can I copy assets from one Media Services account tooanother.</span></span>

<span data-ttu-id="91236-129">A: .NET kullanarak bir Media Services hesabı tooanother toocopy varlıkları kullanmanızı [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) genişletme yöntemi hello kullanılabilir [Azure Media Services .NET SDK uzantıları](https://github.com/Azure/azure-sdk-for-media-services-extensions/) deposu.</span><span class="sxs-lookup"><span data-stu-id="91236-129">A: toocopy assets from one Media Services account tooanother using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="91236-130">Daha fazla bilgi için bkz: [bu](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) Forumu iş parçacığı.</span><span class="sxs-lookup"><span data-stu-id="91236-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="91236-131">S: ne hello karakter AMS ile çalışırken, dosya adlandırma için desteklenir?</span><span class="sxs-lookup"><span data-stu-id="91236-131">Q: What are hello supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="91236-132">A: URL'leri içeriği (örneğin, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) akış Merhaba oluştururken Media Services hello hello IAssetFile.Name özellik değerini kullanır Bu nedenle, yüzde kodlama izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="91236-132">A: Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="91236-133">Merhaba hello değerini **adı** özelliği hello aşağıdakilerden herhangi birini içeremez [yüzde kodlama-ayrılmış karakterleri](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="91236-133">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="91236-134">Ayrıca, yalnızca bir olabilir '.'</span><span class="sxs-lookup"><span data-stu-id="91236-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="91236-135">Merhaba dosya adı uzantısı.</span><span class="sxs-lookup"><span data-stu-id="91236-135">for hello file name extension.</span></span>

<span data-ttu-id="91236-136">S: nasıl tooconnect kullanarak REST?</span><span class="sxs-lookup"><span data-stu-id="91236-136">Q: How tooconnect using REST?</span></span>

<span data-ttu-id="91236-137">Y: nasıl tooconnect toohello AMS API, bkz. bilgi için [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="91236-137">A: For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="91236-138">Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="91236-138">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="91236-139">Sonraki çağrılar toohello yapmanız gereken yeni bir URI.</span><span class="sxs-lookup"><span data-stu-id="91236-139">You must make subsequent calls toohello new URI.</span></span> 

<span data-ttu-id="91236-140">S: nasıl ı işlem kodlama hello sırasında bir video döndürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91236-140">Q: How can I rotate a video during hello encoding process.</span></span>

<span data-ttu-id="91236-141">Y: hello [Medya Kodlayıcısı standart](media-services-dotnet-encode-with-media-encoder-standard.md) 180/90/270 açıları tarafından dönüşünü destekler.</span><span class="sxs-lookup"><span data-stu-id="91236-141">A: hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="91236-142">"Auto", burada toodetect hello döndürme meta verilerde hello gelen MP4/MOV dosyası çalışır ve için dengelemek Hello varsayılan davranıştır.</span><span class="sxs-lookup"><span data-stu-id="91236-142">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="91236-143">Merhaba şunlar **kaynakları** öğesi tooone tanımlanan hello json hazır [burada](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="91236-143">Include hello following **Sources** element tooone of hello json presets defined [here](media-services-mes-presets-overview.md):</span></span>

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a><span data-ttu-id="91236-144">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="91236-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="91236-145">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="91236-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
