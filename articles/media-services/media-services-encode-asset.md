---
title: "aaaOverview ve Azure üzerinde karşılaştırması isteğe bağlı medya kodlayıcılar | Microsoft Docs"
description: "Bu konuda, genel bir bakış ve Azure karşılaştırma isteğe bağlı medya kodlayıcılar üzerine sağlar."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="49291-103">Genel bakış ve isteğe bağlı medya kodlayıcılar üzerinde Azure karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="49291-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="49291-104">Kodlama genel bakış</span><span class="sxs-lookup"><span data-stu-id="49291-104">Encoding overview</span></span>
<span data-ttu-id="49291-105">Azure Media Services hello hello bulutta medya kodlama için birden fazla seçeneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="49291-105">Azure Media Services provides multiple options for hello encoding of media in hello cloud.</span></span>

<span data-ttu-id="49291-106">Media Services ile başlıyor codec bileşenleri ve dosya biçimlerini arasındaki önemli toounderstand hello fark olur.</span><span class="sxs-lookup"><span data-stu-id="49291-106">When starting out with Media Services, it is important toounderstand hello difference between codecs and file formats.</span></span>
<span data-ttu-id="49291-107">Codec bileşenleri hello sıkıştırma/açma algoritmaları dosya biçimleri sıkıştırılmış hello video tutan kapsayıcılar ise uygulayan hello yazılımlardır.</span><span class="sxs-lookup"><span data-stu-id="49291-107">Codecs are hello software that implements hello compression/decompression algorithms whereas file formats are containers that hold hello compressed video.</span></span>

<span data-ttu-id="49291-108">Media Services, toore-package bu kalmadan olmadan, bit hızı Uyarlamalı MP4 veya kesintisiz akış kodlanmış (MPEG DASH, HLS, kesintisiz akış) Media Services tarafından desteklenen akış biçimlerinde içeriği toodeliver sağlayan dinamik paketleme sağlar. Akış biçimlerine.</span><span class="sxs-lookup"><span data-stu-id="49291-108">Media Services provides dynamic packaging which allows you toodeliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having toore-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="49291-109">AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="49291-109">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="49291-110">İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="49291-110">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> <span data-ttu-id="49291-111">tootake avantajlarından [dinamik paketleme](media-services-dynamic-packaging-overview.md), toodo hello aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="49291-111">tootake advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need toodo hello following:</span></span>
>
><span data-ttu-id="49291-112">Ayrıca, kaynak dosyanızı Uyarlamalı bit hızlı MP4 dosyaları veya (Merhaba kodlama adımları Bu öğreticinin ilerleyen bölümlerinde gösterilmektedir) Uyarlamalı bit hızlı kesintisiz akış dosyaları kümesine kodlayın.</span><span class="sxs-lookup"><span data-stu-id="49291-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (hello encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="49291-113">Media Services, bu makalede açıklanan isteğe bağlı kodlayıcılar üzerinde hello aşağıdakileri destekler:</span><span class="sxs-lookup"><span data-stu-id="49291-113">Media Services supports hello following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="49291-114">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="49291-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="49291-115">Media Encoder Premium İş Akışı</span><span class="sxs-lookup"><span data-stu-id="49291-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="49291-116">Bu makalede, kısa bir genel bakış isteğe bağlı medya kodlayıcılar sağlar ve daha ayrıntılı bilgi vermek bağlantılar tooarticles sağlar.</span><span class="sxs-lookup"><span data-stu-id="49291-116">This article gives a brief overview of on demand media encoders and provides links tooarticles that give more detailed information.</span></span> <span data-ttu-id="49291-117">Merhaba konu aynı zamanda hello kodlayıcılar karşılaştırması sağlar.</span><span class="sxs-lookup"><span data-stu-id="49291-117">hello topic also provides comparison of hello encoders.</span></span>

>[!NOTE]
><span data-ttu-id="49291-118">Varsayılan olarak, aynı anda bir etkin kodlama görev her Media Services hesabına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="49291-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="49291-119">Eşzamanlı olarak, satın aldığınız her kodlama ayrılmış birim için bir tane çalışan birden çok kodlama görevleri toohave izin kodlama birimleri ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49291-119">You can reserve encoding units that allow you toohave multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="49291-120">Bilgi için bkz: [kodlama birimleri ölçeklendirme](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="49291-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="49291-121">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="49291-121">Media Encoder Standard</span></span>
### <a name="how-toouse"></a><span data-ttu-id="49291-122">Nasıl toouse</span><span class="sxs-lookup"><span data-stu-id="49291-122">How toouse</span></span>
[<span data-ttu-id="49291-123">Nasıl tooencode Medya Kodlayıcısı standart ile</span><span class="sxs-lookup"><span data-stu-id="49291-123">How tooencode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="49291-124">Biçimleri</span><span class="sxs-lookup"><span data-stu-id="49291-124">Formats</span></span>
[<span data-ttu-id="49291-125">Biçimleri ve codec bileşenleri</span><span class="sxs-lookup"><span data-stu-id="49291-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="49291-126">Hazır</span><span class="sxs-lookup"><span data-stu-id="49291-126">Presets</span></span>
<span data-ttu-id="49291-127">Medya Kodlayıcısı standart yapılandırılmış açıklanan hello Kodlayıcı hazır birini kullanarak [burada](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="49291-127">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="49291-128">Giriş ve çıkış meta verileri</span><span class="sxs-lookup"><span data-stu-id="49291-128">Input and output metadata</span></span>
<span data-ttu-id="49291-129">Merhaba kodlayıcılar giriş meta verileri açıklanan [burada](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="49291-129">hello encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="49291-130">Merhaba kodlayıcılar çıkış meta verileri açıklanan [burada](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="49291-130">hello encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="49291-131">Küçük resimler oluşturma</span><span class="sxs-lookup"><span data-stu-id="49291-131">Generate thumbnails</span></span>
<span data-ttu-id="49291-132">Bilgi için bkz: [nasıl medya Kodlayıcı standart kullanarak toogenerate küçük resimleri](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="49291-132">For information, see [How toogenerate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="49291-133">Videoları (kırpma) kırpma</span><span class="sxs-lookup"><span data-stu-id="49291-133">Trim videos (clipping)</span></span>
<span data-ttu-id="49291-134">Bilgi için bkz: [nasıl medya Kodlayıcı standart kullanarak tootrim videolar](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="49291-134">For information, see [How tootrim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="49291-135">Yer paylaşımları oluşturma</span><span class="sxs-lookup"><span data-stu-id="49291-135">Create overlays</span></span>
<span data-ttu-id="49291-136">Bilgi için bkz: [nasıl toocreate yer paylaşımları medya Kodlayıcı standart kullanarak](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="49291-136">For information, see [How toocreate overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="49291-137">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="49291-137">See also</span></span>
[<span data-ttu-id="49291-138">Merhaba Media Services blogu</span><span class="sxs-lookup"><span data-stu-id="49291-138">hello Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="49291-139">Media Encoder Premium İş Akışı</span><span class="sxs-lookup"><span data-stu-id="49291-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="49291-140">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="49291-140">Overview</span></span>
[<span data-ttu-id="49291-141">Premium Azure Media Services kodlama Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="49291-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a><span data-ttu-id="49291-142">Nasıl toouse</span><span class="sxs-lookup"><span data-stu-id="49291-142">How toouse</span></span>
<span data-ttu-id="49291-143">Medya Kodlayıcısı Premium iş akışı, karmaşık iş akışları kullanılarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="49291-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="49291-144">İş akışı dosyalarını oluşturulabilir ve hello kullanarak güncelleştirilen [iş akışı Tasarımcısı](media-services-workflow-designer.md) aracı.</span><span class="sxs-lookup"><span data-stu-id="49291-144">Workflow files could be created and updated using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="49291-145">Nasıl tooUse Premium Azure Media Services kodlama</span><span class="sxs-lookup"><span data-stu-id="49291-145">How tooUse Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="49291-146">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="49291-146">Known issues</span></span>
<span data-ttu-id="49291-147">Giriş videonuzun kapalı açıklamalı alt yazı içermiyorsa hello varlık hala boş bir TTML dosya içerecektir çıktı.</span><span class="sxs-lookup"><span data-stu-id="49291-147">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="49291-148">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="49291-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="49291-149">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="49291-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="49291-150">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="49291-150">Related articles</span></span>
* [<span data-ttu-id="49291-151">Medya Kodlayıcısı standart hazır özelleştirerek gelişmiş kodlama görevleri gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="49291-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="49291-152">Kotalar ve kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="49291-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
