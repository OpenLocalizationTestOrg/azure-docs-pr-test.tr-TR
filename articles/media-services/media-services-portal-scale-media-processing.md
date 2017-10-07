---
title: "aaaScale medya kullanarak işleme hello Azure portalı | Microsoft Docs"
description: "Bu öğretici hello Azure portal kullanarak işleme ölçeklendirme medya hello adımlarda size yol gösterir."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a><span data-ttu-id="cbda3-103">Merhaba ayrılmış birim türünü değiştir</span><span class="sxs-lookup"><span data-stu-id="cbda3-103">Change hello reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cbda3-104">.NET</span><span class="sxs-lookup"><span data-stu-id="cbda3-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="cbda3-105">Portal</span><span class="sxs-lookup"><span data-stu-id="cbda3-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="cbda3-106">REST</span><span class="sxs-lookup"><span data-stu-id="cbda3-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="cbda3-107">Java</span><span class="sxs-lookup"><span data-stu-id="cbda3-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="cbda3-108">PHP</span><span class="sxs-lookup"><span data-stu-id="cbda3-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="cbda3-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cbda3-109">Overview</span></span>

<span data-ttu-id="cbda3-110">Bir Media Services hesabı bir ayrılmış birim görevleri işleme medyanızı işlenme hello hızı belirleyen türü ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="cbda3-110">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="cbda3-111">Merhaba aşağıdaki arasında seçim yapabilirsiniz ayrılmış birim türleri: **S1**, **S2**, veya **S3**.</span><span class="sxs-lookup"><span data-stu-id="cbda3-111">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="cbda3-112">Örneğin, aynı kodlama işi çalıştıktan daha hızlı hello kullandığınızda hello **S2** ayrılmış birim türü karşılaştırma toohello **S1** türü.</span><span class="sxs-lookup"><span data-stu-id="cbda3-112">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span>

<span data-ttu-id="cbda3-113">Ayrıca toospecifying hello ayrılmış birim türü, hesabınızla tooprovision belirtebilirsiniz **ayrılan birimler** (RUs).</span><span class="sxs-lookup"><span data-stu-id="cbda3-113">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="cbda3-114">sağlanan RUs Hello sayısı belirli bir hesap eşzamanlı olarak işlenebilecek ortam görevleri hello sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="cbda3-114">hello number of provisioned RUs determines hello number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="cbda3-115">RU, tüm medya işlemesini paralel hale getirmek için çalışır ve Azure Media Indexer’ın kullanıldığı dizin oluşturma işleri de buna dahildir.</span><span class="sxs-lookup"><span data-stu-id="cbda3-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="cbda3-116">Bununla birlikte kodlamadan farklı olarak, dizin oluşturma işleri daha hızlı ayrılmış birimlerde daha hızlı işlenmez.</span><span class="sxs-lookup"><span data-stu-id="cbda3-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbda3-117">Tooreview hello emin olun [genel bakış](media-services-scale-media-processing-overview.md) konu tooget konu işleme medya ölçeklendirme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="cbda3-117">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="cbda3-118">Medya işlemeyi ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="cbda3-118">Scale media processing</span></span>
<span data-ttu-id="cbda3-119">toochange hello ayrılmış birim türü ve hello ayrılmış birim sayısı, hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="cbda3-119">toochange hello reserved unit type and hello number of reserved units, do hello following:</span></span>

1. <span data-ttu-id="cbda3-120">Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="cbda3-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="cbda3-121">Merhaba, **ayarları** penceresinde, seçin **medya ayrılmış birimleri**.</span><span class="sxs-lookup"><span data-stu-id="cbda3-121">In hello **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="cbda3-122">toochange hello hello için ayrılmış birim sayısı seçilen ayrılmış birim türü, hello kullan **medya sunulan birimleri** kaydırıcı.</span><span class="sxs-lookup"><span data-stu-id="cbda3-122">toochange hello number of reserved units for hello selected reserved unit type, use hello **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="cbda3-123">toochange hello **AYRILMIŞ birim türü**, S1, S2 ve S3 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="cbda3-123">toochange hello **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![İşlemci sayfası](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="cbda3-125">Tuşuna hello düğmesi toosave yaptığınız değişiklikleri KAYDEDİN.</span><span class="sxs-lookup"><span data-stu-id="cbda3-125">Press hello SAVE button toosave your changes.</span></span>
   
    <span data-ttu-id="cbda3-126">KAYDETME bastığınızda hello yeni ayrılan birimler ayrılır.</span><span class="sxs-lookup"><span data-stu-id="cbda3-126">hello new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbda3-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cbda3-127">Next steps</span></span>
<span data-ttu-id="cbda3-128">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="cbda3-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cbda3-129">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="cbda3-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

