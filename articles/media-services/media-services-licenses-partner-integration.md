---
title: "aaaUsing ortakları toodeliver Widevine lisansları tooAzure Media Services | Microsoft Docs"
description: "Bu makalede, Azure Media Services (AMS) toodeliver, PlayReady ve Widevine DRMs AMS tarafından dinamik olarak şifrelenmiş bir akış nasıl kullanabileceğinizi açıklar. Medya Hizmetleri PlayReady lisans sunucusundan Hello PlayReady lisans gelir ve castLabs lisans sunucusu tarafından Widevine lisans teslim edilir."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5bcad5a4-c0bb-4871-9cce-808a913c53e6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 3c18a8a22ced239931dea5385020194bd6d83f28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-partners-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="7460b-104">İş ortakları toodeliver Widevine lisansları tooAzure Media Services'i kullanma</span><span class="sxs-lookup"><span data-stu-id="7460b-104">Using partners toodeliver Widevine licenses tooAzure Media Services</span></span>
## <a name="overview"></a><span data-ttu-id="7460b-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7460b-105">Overview</span></span>
<span data-ttu-id="7460b-106">Microsoft Azure Media Services MPEG-DASH ortak şifreleme (CENC) belirtimi hello şifrelenmiş Widevine DRM ile korunan toodeliver sağlar.</span><span class="sxs-lookup"><span data-stu-id="7460b-106">Microsoft Azure Media Services enables you toodeliver MPEG-DASH protected with Widevine DRM, which is encrypted per hello Common Encryption (CENC) specification.</span></span>

<span data-ttu-id="7460b-107">Media Services .NET SDK'sı sürüm 3.5.2'de Hello ile başlayarak, Media Services, tooconfigure Widevine lisans şablonu sağlar ve Widevine lisansları alın.</span><span class="sxs-lookup"><span data-stu-id="7460b-107">Starting with hello Media Services .NET SDK version 3.5.2, Media Services enables you tooconfigure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="7460b-108">Widevine lisansları teslim AMS ortaklarını toohelp aşağıdaki hello de kullanabilirsiniz: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="7460b-108">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

## <a name="castlabs"></a><span data-ttu-id="7460b-109">castLabs</span><span class="sxs-lookup"><span data-stu-id="7460b-109">castLabs</span></span>
<span data-ttu-id="7460b-110">Kullanabileceğiniz [castLabs](http://castlabs.com/company/partners/azure/) toodeliver Widevine lisansları.</span><span class="sxs-lookup"><span data-stu-id="7460b-110">You can use [castLabs](http://castlabs.com/company/partners/azure/) toodeliver Widevine licenses.</span></span> <span data-ttu-id="7460b-111">Daha fazla bilgi için bkz: [castLabs kullanarak tooAzure Media Services toodeliver DRM lisansları](media-services-castlabs-integration.md)</span><span class="sxs-lookup"><span data-stu-id="7460b-111">For more information, see [Using castLabs toodeliver DRM licenses tooAzure Media Services](media-services-castlabs-integration.md)</span></span>

## <a name="axinom"></a><span data-ttu-id="7460b-112">Axinom</span><span class="sxs-lookup"><span data-stu-id="7460b-112">Axinom</span></span>
<span data-ttu-id="7460b-113">Kullanabileceğiniz [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) toodeliver Widevine lisansları.</span><span class="sxs-lookup"><span data-stu-id="7460b-113">You can use [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) toodeliver Widevine licenses.</span></span> <span data-ttu-id="7460b-114">Daha fazla bilgi için bkz: [kullanarak Axinom toodeliver DRM lisansları tooAzure medya Hizmetleri](media-services-axinom-integration.md)</span><span class="sxs-lookup"><span data-stu-id="7460b-114">For more information, see [Using Axinom toodeliver DRM licenses tooAzure Media Services](media-services-axinom-integration.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="7460b-115">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="7460b-115">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7460b-116">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="7460b-116">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="7460b-117">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="7460b-117">See also</span></span>
[<span data-ttu-id="7460b-118">PlayReady ve/ya Widevine dinamik ortak şifreleme işlemini kullanma</span><span class="sxs-lookup"><span data-stu-id="7460b-118">Using PlayReady and/or Widevine dynamic common encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="7460b-119">Mingfei'nın blogu</span><span class="sxs-lookup"><span data-stu-id="7460b-119">Mingfei’s blog</span></span>](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)

