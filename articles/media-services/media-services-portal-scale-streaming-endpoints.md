---
title: "Akış uç noktaları Azure portal ile ölçek | Microsoft Docs"
description: "Bu öğreticide Azure portal ile akış uç noktalarını ölçeklendirme adımları açıklanmaktadır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 4bb891371e3fc802fa667688a88878db18e32422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="scale-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="bd33c-103">Azure portal ile akış uç noktalarını ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="bd33c-103">Scale streaming endpoints with the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="bd33c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="bd33c-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="bd33c-105">Bu öğreticiyi tamamlamak için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd33c-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="bd33c-106">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bd33c-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="bd33c-107">**Premium** akış uç noktaları, adanmış ve ölçeklenebilir bant genişliği kapasitesi sağlar; dolayısıyla gelişmiş iş yükleri için uygundur.</span><span class="sxs-lookup"><span data-stu-id="bd33c-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="bd33c-108">**Premium** akış uç noktası olan müşteriler, varsayılan olarak bir akış birimi (SU) alır.</span><span class="sxs-lookup"><span data-stu-id="bd33c-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="bd33c-109">Akış uç noktası, SU’lar eklenerek ölçeklendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="bd33c-109">The streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="bd33c-110">Her SU, uygulamaya ek bant genişliği kapasitesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd33c-110">Each SU provides additional bandwidth capacity to the application.</span></span> <span data-ttu-id="bd33c-111">Akış uç nokta türleri ve CDN yapılandırma hakkında daha fazla bilgi için bkz: [akış uç noktası genel bakış](media-services-portal-manage-streaming-endpoints.md) konu.</span><span class="sxs-lookup"><span data-stu-id="bd33c-111">For more information about streaming endpoint types and CDN configuration, see the [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="bd33c-112">Bu konu bir akış uç ölçeklendirme gösterir.</span><span class="sxs-lookup"><span data-stu-id="bd33c-112">This topic shows how to scale a streaming endpoint.</span></span>

<span data-ttu-id="bd33c-113">Fiyatlandırma ayrıntıları hakkında daha fazla bilgi için bkz. [Media Services Fiyatlandırma Ayrıntıları](http://go.microsoft.com/fwlink/?LinkId=275107).</span><span class="sxs-lookup"><span data-stu-id="bd33c-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="bd33c-114">Akış uç noktalarını ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="bd33c-114">Scale streaming endpoints</span></span>

<span data-ttu-id="bd33c-115">Akış birim sayısını değiştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="bd33c-115">To change the number of streaming units, do the following:</span></span>

1. <span data-ttu-id="bd33c-116">[Azure portalında](https://portal.azure.com/) Azure Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="bd33c-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="bd33c-117">İçinde **ayarları** penceresinde, seçin **akış uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="bd33c-117">In the **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="bd33c-118">Ölçeklendirmek istediğiniz akış uç noktasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd33c-118">Click on the streaming endpoint that you want to scale.</span></span> 

    [!NOTE] <span data-ttu-id="bd33c-119">Yalnızca ölçeklendirebilirsiniz **Premium** akış uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="bd33c-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="bd33c-120">Akış birim sayısını belirtmek üzere kaydırıcıyı taşıyın.</span><span class="sxs-lookup"><span data-stu-id="bd33c-120">Move the slider to specify the number of streaming units.</span></span>

    ![Akış uç noktası](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="bd33c-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd33c-122">Next steps</span></span>
<span data-ttu-id="bd33c-123">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="bd33c-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bd33c-124">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="bd33c-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

