---
title: "aaa\"Merhaba Azure portal ile içerik yayımlama | Microsoft Docs\""
description: "Bu öğreticide, içeriğinizi hello Azure portal ile yayımlama hello adımları açıklanmaktadır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a><span data-ttu-id="98a9e-103">İçerik hello Azure portal ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="98a9e-103">Publish content with hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="98a9e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="98a9e-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="98a9e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="98a9e-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="98a9e-106">REST</span><span class="sxs-lookup"><span data-stu-id="98a9e-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="98a9e-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="98a9e-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="98a9e-108">toocomplete Bu öğretici bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="98a9e-108">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="98a9e-109">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="98a9e-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="98a9e-110">tooprovide kullanılan toostream ya da içeriğinizi indirme URL'si, kullanıcı, önce çok "varlığınız bir Bulucu oluşturarak yayımlamanız".</span><span class="sxs-lookup"><span data-stu-id="98a9e-110">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="98a9e-111">Bulucular hello varlıkta bulunan erişim toofiles sağlar.</span><span class="sxs-lookup"><span data-stu-id="98a9e-111">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="98a9e-112">Media Services iki tür bulucuyu destekler:</span><span class="sxs-lookup"><span data-stu-id="98a9e-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="98a9e-113">Akış (OnDemandOrigin) bulucuları, (örneğin, toostream MPEG DASH, HLS veya kesintisiz akış) Uyarlamalı akış için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="98a9e-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="98a9e-114">toocreate akış Bulucusu varlığınız bir .ism dosyası içermelidir.</span><span class="sxs-lookup"><span data-stu-id="98a9e-114">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="98a9e-115">Aşamalı indirme aracılığıyla video teslimi için kullanılan aşamalı (SAS) bulucular.</span><span class="sxs-lookup"><span data-stu-id="98a9e-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="98a9e-116">Bir akış URL'si biçimi aşağıdaki hello sahiptir ve tooplay kesintisiz akış varlıklarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="98a9e-116">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="98a9e-117">HLS akış URL'si, bir toobuild ekleme (format = m3u8-aapl) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="98a9e-117">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="98a9e-118">bir akış URL'si, MPEG DASH toobuild ekleme (biçim mpd zaman csf =) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="98a9e-118">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="98a9e-119">Bir SAS URL'si biçimi aşağıdaki hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="98a9e-119">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="98a9e-120">Daha fazla bilgi için bkz: [içerik genel bakış sunan](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98a9e-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="98a9e-121">Mart 2015 öncesinde hello portal toocreate bulucular kullandıysanız, iki yıl sona erme tarihi olan bulucular oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="98a9e-121">If you used hello portal toocreate locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="98a9e-122">Kullanım Bulucunun sona erme tarihi bir tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) veya [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API'leri.</span><span class="sxs-lookup"><span data-stu-id="98a9e-122">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="98a9e-123">Bir SAS Bulucu hello sona erme tarihini güncelleştirdiğinizde hello URL'nin değiştiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="98a9e-123">Note that when you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="98a9e-124">toouse hello portal toopublish bir varlığı</span><span class="sxs-lookup"><span data-stu-id="98a9e-124">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="98a9e-125">toouse hello portal toopublish bir varlık hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="98a9e-125">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="98a9e-126">Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="98a9e-126">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="98a9e-127">**Ayarlar** > **Varlıklar**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="98a9e-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="98a9e-128">Merhaba varlık toopublish istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="98a9e-128">Select hello asset that you want toopublish.</span></span>
4. <span data-ttu-id="98a9e-129">Merhaba tıklatın **Yayımla** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="98a9e-129">Click hello **Publish** button.</span></span>
5. <span data-ttu-id="98a9e-130">Merhaba Bulucu türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="98a9e-130">Select hello locator type.</span></span>
6. <span data-ttu-id="98a9e-131">**Ekle**’ye basın.</span><span class="sxs-lookup"><span data-stu-id="98a9e-131">Press **Add**.</span></span>
   
    ![Yayımlama](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="98a9e-133">Merhaba URL toohello listesi eklenecek **yayımlanan URL'ler**.</span><span class="sxs-lookup"><span data-stu-id="98a9e-133">hello URL will be added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="98a9e-134">Merhaba portaldan içerik oynatma</span><span class="sxs-lookup"><span data-stu-id="98a9e-134">Play content from hello portal</span></span>
<span data-ttu-id="98a9e-135">Hello Azure portalı bir içerik oynatıcı sağlar videonuzu tootest kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98a9e-135">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="98a9e-136">İstenen hello videoya tıklayın ve hello ardından **Yürüt** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="98a9e-136">Click hello desired video and then click hello **Play** button.</span></span>

![Yayımlama](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="98a9e-138">Bazı dikkate alınması gereken noktalar vardır:</span><span class="sxs-lookup"><span data-stu-id="98a9e-138">Some considerations apply:</span></span>

* <span data-ttu-id="98a9e-139">Merhaba video yayımlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="98a9e-139">Make sure hello video has been published.</span></span>
* <span data-ttu-id="98a9e-140">Bu **Media player** hello varsayılan akış uç noktasından oynatır.</span><span class="sxs-lookup"><span data-stu-id="98a9e-140">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="98a9e-141">Varsayılan olmayan tooplay istiyorsanız akış uç noktası, toocopy hello URL'yi tıklatın ve başka bir oynatıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="98a9e-141">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="98a9e-142">Örneğin, [Azure Media Services Oynatıcı](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="98a9e-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="98a9e-143">Akış uç noktası akış hello çalıştırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="98a9e-143">hello streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="98a9e-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98a9e-144">Next steps</span></span>
<span data-ttu-id="98a9e-145">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="98a9e-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="98a9e-146">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="98a9e-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

