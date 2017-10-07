---
title: "Medya kullanarak işlemci aaaHow tooCreate .NET için Azure Media Services SDK'sı hello | Microsoft Docs"
description: "Nasıl toocreate medya işlemci bileşeni tooencode biçimine dönüştürmek, şifrelemek veya medya içeriği şifresini çözmek için Azure Media Services öğrenin. Kod örnekleri C# dilinde yazılmıştır ve .NET için Media Services SDK'sı hello kullanın."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="676b2-104">Nasıl yapılır: bir medya işlemci örneği Al</span><span class="sxs-lookup"><span data-stu-id="676b2-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="676b2-105">.NET</span><span class="sxs-lookup"><span data-stu-id="676b2-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="676b2-106">REST</span><span class="sxs-lookup"><span data-stu-id="676b2-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="676b2-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="676b2-107">Overview</span></span>
<span data-ttu-id="676b2-108">Medya işlemcisi kodlama gibi kodlama, ek olarak, belirli işleme görevi işleyen bir bileşenidir Media Services'de şifreleme veya medya içeriği çözme dönüştürme biçimi.</span><span class="sxs-lookup"><span data-stu-id="676b2-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="676b2-109">Genellikle bir görev tooencode oluşturulurken medya işlemcisi oluşturma, şifrelemek veya medya içeriği hello biçimine dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="676b2-109">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="676b2-110">Azure medya işlemcileri</span><span class="sxs-lookup"><span data-stu-id="676b2-110">Azure media processors</span></span> 

<span data-ttu-id="676b2-111">konu aşağıdaki hello medya işlemcileri listesi sağlar:</span><span class="sxs-lookup"><span data-stu-id="676b2-111">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="676b2-112">Kodlama medya işlemcileri</span><span class="sxs-lookup"><span data-stu-id="676b2-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="676b2-113">Analizi medya işlemcileri</span><span class="sxs-lookup"><span data-stu-id="676b2-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="676b2-114">Medya işlemcisi Al</span><span class="sxs-lookup"><span data-stu-id="676b2-114">Get Media Processor</span></span>

<span data-ttu-id="676b2-115">yöntem gösterir nasıl aşağıdaki hello tooget medya işlemci örneği.</span><span class="sxs-lookup"><span data-stu-id="676b2-115">hello following method shows how tooget a media processor instance.</span></span> <span data-ttu-id="676b2-116">Merhaba kod örneği varsayar adlı bir modül düzeyi değişkeni hello kullanımını **_bağlamı** hello bölümde açıklandığı gibi tooreference hello sunucu bağlamı [nasıl yapılır: Hizmetleri programlamayla tooMedia bağlanmak](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="676b2-116">hello code example assumes hello use of a module-level variable named **_context** tooreference hello server context as described in hello section [How to: Connect tooMedia Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="676b2-117">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="676b2-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="676b2-118">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="676b2-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="676b2-119">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="676b2-119">Next Steps</span></span>
<span data-ttu-id="676b2-120">Artık bildiğinize göre nasıl tooget medya işlemci örneği Git toohello [nasıl tooEncode bir varlık](media-services-dotnet-encode-with-media-encoder-standard.md) nasıl toouse hello Medya Kodlayıcısı standart tooencode bir varlık gösterecektir konu.</span><span class="sxs-lookup"><span data-stu-id="676b2-120">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

