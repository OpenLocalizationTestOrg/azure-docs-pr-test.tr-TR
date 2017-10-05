---
title: "Medya kodlama birimleri - Azure ekleyerek işleme ölçeğini |  Microsoft Docs"
description: "Bilgi nasıl .NET ile kodlama birimleri eklemek"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: 72a8729d22a9e76c8076d7a3347619a2163e4f09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-scale-encoding-with-net-sdk"></a><span data-ttu-id="b741f-103">.NET SDK ile kodlama ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="b741f-103">How to scale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b741f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="b741f-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="b741f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b741f-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="b741f-106">REST</span><span class="sxs-lookup"><span data-stu-id="b741f-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="b741f-107">Java</span><span class="sxs-lookup"><span data-stu-id="b741f-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="b741f-108">PHP</span><span class="sxs-lookup"><span data-stu-id="b741f-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="b741f-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b741f-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b741f-110">Gözden geçirdiğinizden emin olun [genel bakış](media-services-scale-media-processing-overview.md) konu işleme medya ölçeklendirme hakkında daha fazla bilgi için konu.</span><span class="sxs-lookup"><span data-stu-id="b741f-110">Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="b741f-111">Ayrılmış birim türü ve .NET SDK kullanarak ayrılan birimler kodlama sayısını değiştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="b741f-111">To change the reserved unit type and the number of encoding reserved units using .NET SDK, do the following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds to S1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="b741f-112">Bir destek bileti açmadan</span><span class="sxs-lookup"><span data-stu-id="b741f-112">Opening a Support Ticket</span></span>
<span data-ttu-id="b741f-113">Varsayılan olarak her Media Services hesabı kodlama ve 5 isteğe bağlı akışa ayrılan birimler en fazla 25 ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b741f-113">By default every Media Services account can scale to up to 25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="b741f-114">Bir destek bileti açılarak daha yüksek bir sınır isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="b741f-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="b741f-115">Bir destek bileti açın</span><span class="sxs-lookup"><span data-stu-id="b741f-115">Open a support ticket</span></span>
<span data-ttu-id="b741f-116">Bir destek açmak için bilet aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="b741f-116">To open a support ticket do the following:</span></span>

1. <span data-ttu-id="b741f-117">Tıklatın [alma desteği](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="b741f-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="b741f-118">Açmadıysanız, kimlik bilgilerinizi girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="b741f-118">If you are not logged in, you will be prompted to enter your credentials.</span></span>
2. <span data-ttu-id="b741f-119">Aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="b741f-119">Select your subscription.</span></span>
3. <span data-ttu-id="b741f-120">Destek türü'nün altında "Teknik" seçin.</span><span class="sxs-lookup"><span data-stu-id="b741f-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="b741f-121">"Bilet oluştur" seçeneğini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b741f-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="b741f-122">"Azure medya sonraki sayfada sunulan hizmetler" Ürün listesinde seçin.</span><span class="sxs-lookup"><span data-stu-id="b741f-122">Select "Azure Media Services" in the product list presented on the next page.</span></span>
6. <span data-ttu-id="b741f-123">"Sorun türü" seçin sorununuz için uygun olan.</span><span class="sxs-lookup"><span data-stu-id="b741f-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="b741f-124">Devam Et'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b741f-124">Click Continue.</span></span>
8. <span data-ttu-id="b741f-125">Sonraki sayfasındaki yönergeleri izleyin ve sorunu ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="b741f-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="b741f-126">Bilet için Gönder'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b741f-126">Click submit to open the ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="b741f-127">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="b741f-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b741f-128">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="b741f-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

