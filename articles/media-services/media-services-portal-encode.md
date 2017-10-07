---
title: "aaaEncode Medya Kodlayıcısı standart ile hello Azure portal kullanarak bir varlık | Microsoft Docs"
description: "Bu öğreticide, Medya Kodlayıcısı standart ile hello Azure portal kullanarak bir varlık kodlama hello adımları açıklanmaktadır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a><span data-ttu-id="3bca6-103">Medya Kodlayıcısı standart ile hello Azure portal kullanarak bir varlık kodlama</span><span class="sxs-lookup"><span data-stu-id="3bca6-103">Encode an asset using Media Encoder Standard with hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="3bca6-104">toocomplete Bu öğretici bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bca6-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="3bca6-105">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3bca6-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="3bca6-106">Merhaba en sık karşılaşılan senaryolardan biri, bit hızı Uyarlamalı akış tooyour istemcileri iletmektir Azure Media Services ile çalışırken.</span><span class="sxs-lookup"><span data-stu-id="3bca6-106">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="3bca6-107">Media Services şu bit hızı Uyarlamalı akış teknolojilerini hello destekler: HTTP canlı akışı (HLS), kesintisiz akış, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="3bca6-107">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="3bca6-108">tooprepare videolarınızı bit hızı Uyarlamalı akış için tooencode kaynağınız video Çoklu bit hızlı dosyalarıyla gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bca6-108">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="3bca6-109">Merhaba kullanması gereken **Medya Kodlayıcısı standart** Kodlayıcı tooencode videolarınızı.</span><span class="sxs-lookup"><span data-stu-id="3bca6-109">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="3bca6-110">Media Services, Çoklu bit hızlı MP4s akış biçimlerine aşağıdaki hello içinde de toodeliver sağlayan dinamik paketleme sağlar: MPEG DASH, HLS, kesintisiz akış, bu akış biçimlerine toore paket kalmadan olmadan.</span><span class="sxs-lookup"><span data-stu-id="3bca6-110">Media Services also provides dynamic packaging which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toore-package into these streaming formats.</span></span> <span data-ttu-id="3bca6-111">Dinamik paketleme ile toostore yeterlidir ve tek bir depolama biçiminde ve Media Services hello dosyaları ödeme hello istemciden gelen isteklere göre uygun yanıtı derler ve.</span><span class="sxs-lookup"><span data-stu-id="3bca6-111">With dynamic packaging you only need toostore and pay for hello files in single storage format and Media Services will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="3bca6-112">tootake avantajı dinamik paketleme, tooencode kaynak dosyanızı Çoklu bit hızlı MP4 dosyaları (kodlama adımları hello gösterilmektedir daha sonra bu bölümde) kümesine ihtiyacınız.</span><span class="sxs-lookup"><span data-stu-id="3bca6-112">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="3bca6-113">işlem tooscale medya bkz [bu](media-services-portal-scale-media-processing.md) konu.</span><span class="sxs-lookup"><span data-stu-id="3bca6-113">tooscale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-hello-azure-portal"></a><span data-ttu-id="3bca6-114">Hello Azure portal ile kodlayın</span><span class="sxs-lookup"><span data-stu-id="3bca6-114">Encode with hello Azure portal</span></span>
<span data-ttu-id="3bca6-115">Bu bölüm, içeriğinizi Medya Kodlayıcısı standart ile tooencode uygulayabileceğiniz hello adımları açıklar.</span><span class="sxs-lookup"><span data-stu-id="3bca6-115">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="3bca6-116">Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="3bca6-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="3bca6-117">Merhaba, **ayarları** penceresinde, seçin **varlıklar**.</span><span class="sxs-lookup"><span data-stu-id="3bca6-117">In hello **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="3bca6-118">Merhaba, **varlıklar** penceresinde, select hello varlık tooencode istersiniz.</span><span class="sxs-lookup"><span data-stu-id="3bca6-118">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
4. <span data-ttu-id="3bca6-119">Tuşuna hello **kodla** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3bca6-119">Press hello **Encode** button.</span></span>
5. <span data-ttu-id="3bca6-120">Merhaba, **bir varlık kodla** penceresi, select hello "Medya Kodlayıcısı standart" işlemcisini ve bir hazır.</span><span class="sxs-lookup"><span data-stu-id="3bca6-120">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="3bca6-121">Hazır ayarlar hakkında daha fazla bilgi için bkz. [Bit hızı merdivenini otomatik oluşturma](media-services-autogen-bitrate-ladder-with-mes.md) ve [MES Görev Ön Ayarları](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3bca6-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="3bca6-122">Hangi kodlama hazır kullanılır toocontrol planlıyorsanız, bunu göz önünde bulundurun: tooselect hello giriş videonuzun için en uygun olan Önayar önemlidir.</span><span class="sxs-lookup"><span data-stu-id="3bca6-122">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="3bca6-123">Giriş videonuzun 1920 x 1080 piksel çözünürlüğü sahip biliyorsanız, örneğin, hello kullanabilirsiniz "H264 Çoklu bit hızı 1080p" hazır.</span><span class="sxs-lookup"><span data-stu-id="3bca6-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="3bca6-124">Düşük çözünürlüklü (640 x 360) bir videonuz olması durumunda "H264 Çoklu Bit hızı 1080p" ön ayarını kullanmamalısınız.</span><span class="sxs-lookup"><span data-stu-id="3bca6-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="3bca6-125">Daha kolay yönetim için hello hello çıkış varlık adını düzenleme ve hello işinin hello adı bir seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="3bca6-125">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Varlıkları kodlama](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="3bca6-127">**Oluştur**’a basın.</span><span class="sxs-lookup"><span data-stu-id="3bca6-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="3bca6-128">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="3bca6-128">Next step</span></span>
<span data-ttu-id="3bca6-129">Bölümünde açıklandığı gibi hello Azure portal ile kodlama işi ilerleme durumunu izleyebilirsiniz [bu](media-services-portal-check-job-progress.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3bca6-129">You can monitor encoding job progress with hello Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="3bca6-130">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="3bca6-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3bca6-131">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="3bca6-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

