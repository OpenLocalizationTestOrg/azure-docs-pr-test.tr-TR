---
title: "aaaAzure Media Services dinamik paketleme genel bakış | Microsoft Docs"
description: "Merhaba konu sağlar ve dinamik paketleme genel bakış."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="3e6d8-103">Dinamik paketleme</span><span class="sxs-lookup"><span data-stu-id="3e6d8-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="3e6d8-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3e6d8-104">Overview</span></span>
<span data-ttu-id="3e6d8-105">Microsoft Azure Media Services, kullanılan toodeliver olabilir birçok medya kaynak dosya biçimleri, medya akış biçimlerine ve içerik koruma biçimleri tooa istemci teknolojileri çeşitli (örneğin, iOS, XBOX, Silverlight, Windows 8).</span><span class="sxs-lookup"><span data-stu-id="3e6d8-105">Microsoft Azure Media Services can be used toodeliver many media source file formats, media streaming formats, and content protection formats tooa variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="3e6d8-106">Bu istemciler farklı protokollere anlamanıza, örneğin bir HTTP canlı akışı (HLS) V4 biçiminde iOS gerektirir ve Silverlight ve Xbox kesintisiz akış gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3e6d8-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="3e6d8-107">Uyarlamalı bit hızlı (Çoklu bit hızı) kümesi varsa MP4 (ISO temel medya 14496-12) dosyaları veya uyarlamalı bit hızlı kesintisiz akış dosyalarının MPEG DASH, HLS veya kesintisiz akış anlamak tooserve tooclients istediğiniz kümesi, medya avantajlarından almalıdır Dinamik paketleme Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="3e6d8-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want tooserve tooclients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="3e6d8-108">Dinamik tüm yapmanız gereken paketleme ile toocreate Uyarlamalı bit hızlı MP4 veya uyarlamalı bit hızlı kesintisiz akış dosyaları kümesi içeren bir varlıktır.</span><span class="sxs-lookup"><span data-stu-id="3e6d8-108">With dynamic packaging all you need is toocreate an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="3e6d8-109">Merhaba hello bildiriminde belirtilen biçime bağlı olarak veya istek parçalara, hello isteğe bağlı Akış sunucusu, hello akış seçmiş olduğunuz hello protokolde almanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="3e6d8-109">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="3e6d8-110">Sonuç olarak, yalnızca toostore gerekir ve tek bir depolama biçiminde ve Media Services hizmeti hello dosyaları ödeme hello istemciden gelen isteklere göre uygun yanıtı derler ve.</span><span class="sxs-lookup"><span data-stu-id="3e6d8-110">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="3e6d8-111">Merhaba Aşağıdaki diyagramda hello geleneksel kodlama ve statik paketleme iş akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3e6d8-111">hello following diagram shows hello traditional encoding and static packaging workflow.</span></span>

![Statik kodlama](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="3e6d8-113">Merhaba Aşağıdaki diyagramda hello dinamik paketleme iş akışı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3e6d8-113">hello following diagram shows hello dynamic packaging workflow.</span></span>

![Dinamik kodlama](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="3e6d8-115">Yaygın bir senaryo</span><span class="sxs-lookup"><span data-stu-id="3e6d8-115">Common scenario</span></span>
1. <span data-ttu-id="3e6d8-116">(Bir ara dosyayı olarak adlandırılır) bir giriş dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3e6d8-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="3e6d8-117">Örneğin, H.264, MP4 veya WMV (desteklenen biçimler hello listesi için bkz [hello Medya Kodlayıcısı standart tarafından desteklenen biçimleri](media-services-media-encoder-standard-formats.md).</span><span class="sxs-lookup"><span data-stu-id="3e6d8-117">For example, H.264, MP4, or WMV (for hello list of supported formats see [Formats Supported by hello Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="3e6d8-118">Mezzanine dosya tooH.264 MP4 bit hızı Uyarlamalı kümelerinizi kodlayın.</span><span class="sxs-lookup"><span data-stu-id="3e6d8-118">Encode your mezzanine file tooH.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="3e6d8-119">Merhaba isteğe bağlı Bulucu oluşturarak hello Uyarlamalı bit hızı MP4 kümesine içeren hello varlığı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="3e6d8-119">Publish hello asset that contains hello adaptive bitrate MP4 set by creating hello On-Demand Locator.</span></span>
4. <span data-ttu-id="3e6d8-120">URL'leri tooaccess akış hello oluşturun ve, içerik akışı sağlama.</span><span class="sxs-lookup"><span data-stu-id="3e6d8-120">Build hello streaming URLs tooaccess and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="3e6d8-121">Varlıklar dinamik akış için hazırlama</span><span class="sxs-lookup"><span data-stu-id="3e6d8-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="3e6d8-122">tooprepare varlığınız, akış dinamik için iki seçenek vardır:</span><span class="sxs-lookup"><span data-stu-id="3e6d8-122">tooprepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="3e6d8-123">[Ana dosya karşıya yükleme](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="3e6d8-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="3e6d8-124">[Merhaba Medya Kodlayıcısı standart Kodlayıcı tooproduce H.264 MP4 bit hızı Uyarlamalı kümeleri kullanan](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="3e6d8-124">[Use hello Media Encoder Standard encoder tooproduce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="3e6d8-125">[Kullanıcınıza içeriğinizin akışını](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3e6d8-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="3e6d8-126"><a id="unsupported_formats"></a>Dinamik paketleme tarafından desteklenmeyen biçimleri</span><span class="sxs-lookup"><span data-stu-id="3e6d8-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="3e6d8-127">Merhaba aşağıdaki kaynak dosya biçimlerini dinamik paketleme tarafından desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="3e6d8-127">hello following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="3e6d8-128">Dolby dijital mp4 dosyaları.</span><span class="sxs-lookup"><span data-stu-id="3e6d8-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="3e6d8-129">Dolby dijital kesintisiz dosyalar.</span><span class="sxs-lookup"><span data-stu-id="3e6d8-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="3e6d8-130">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="3e6d8-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3e6d8-131">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="3e6d8-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

