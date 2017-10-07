---
title: "aaaScale medya kodlama birimleri - Azure ekleyerek işleme |  Microsoft Docs"
description: "Bilgi nasıl toohow tooadd kodlama birimleri .NET"
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
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a><span data-ttu-id="0c611-103">Nasıl tooscale .NET SDK'sı ile kodlama</span><span class="sxs-lookup"><span data-stu-id="0c611-103">How tooscale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0c611-104">Portal</span><span class="sxs-lookup"><span data-stu-id="0c611-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="0c611-105">.NET</span><span class="sxs-lookup"><span data-stu-id="0c611-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="0c611-106">REST</span><span class="sxs-lookup"><span data-stu-id="0c611-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="0c611-107">Java</span><span class="sxs-lookup"><span data-stu-id="0c611-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="0c611-108">PHP</span><span class="sxs-lookup"><span data-stu-id="0c611-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="0c611-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0c611-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0c611-110">Tooreview hello emin olun [genel bakış](media-services-scale-media-processing-overview.md) konu tooget konu işleme medya ölçeklendirme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="0c611-110">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="0c611-111">.NET SDK kullanarak ayrılan birimler kodlama toochange hello ayrılmış birim türü ve hello sayısı hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="0c611-111">toochange hello reserved unit type and hello number of encoding reserved units using .NET SDK, do hello following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="0c611-112">Bir destek bileti açmadan</span><span class="sxs-lookup"><span data-stu-id="0c611-112">Opening a Support Ticket</span></span>
<span data-ttu-id="0c611-113">Varsayılan olarak her Media Services hesabı tooup too25 ölçeklendirebilirsiniz kodlama ve 5 isteğe bağlı akışa ayrılan birimler.</span><span class="sxs-lookup"><span data-stu-id="0c611-113">By default every Media Services account can scale tooup too25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="0c611-114">Bir destek bileti açılarak daha yüksek bir sınır isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="0c611-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="0c611-115">Bir destek bileti açın</span><span class="sxs-lookup"><span data-stu-id="0c611-115">Open a support ticket</span></span>
<span data-ttu-id="0c611-116">tooopen bir destek bileti hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="0c611-116">tooopen a support ticket do hello following:</span></span>

1. <span data-ttu-id="0c611-117">Tıklatın [alma desteği](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="0c611-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="0c611-118">Açmadınız ederseniz kimlik bilgileriniz istendiğinde tooenter olabilir.</span><span class="sxs-lookup"><span data-stu-id="0c611-118">If you are not logged in, you will be prompted tooenter your credentials.</span></span>
2. <span data-ttu-id="0c611-119">Aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="0c611-119">Select your subscription.</span></span>
3. <span data-ttu-id="0c611-120">Destek türü'nün altında "Teknik" seçin.</span><span class="sxs-lookup"><span data-stu-id="0c611-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="0c611-121">"Bilet oluştur" seçeneğini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0c611-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="0c611-122">"Azure medya hello sonraki sayfada sunulan hizmetler" Merhaba ürün listesinde seçin.</span><span class="sxs-lookup"><span data-stu-id="0c611-122">Select "Azure Media Services" in hello product list presented on hello next page.</span></span>
6. <span data-ttu-id="0c611-123">"Sorun türü" seçin sorununuz için uygun olan.</span><span class="sxs-lookup"><span data-stu-id="0c611-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="0c611-124">Devam Et'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0c611-124">Click Continue.</span></span>
8. <span data-ttu-id="0c611-125">Sonraki sayfasındaki yönergeleri izleyin ve sorunu ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="0c611-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="0c611-126">Tooopen hello bilet Gönder'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0c611-126">Click submit tooopen hello ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="0c611-127">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="0c611-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0c611-128">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="0c611-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

