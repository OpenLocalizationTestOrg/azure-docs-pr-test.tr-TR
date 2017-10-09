---
title: "Akış uç noktaları hello Azure portal ile aaaScale | Microsoft Docs"
description: "Bu öğreticide hello Azure portal ile akış uç noktalarını ölçeklendirme hello adımları açıklanmaktadır."
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
ms.openlocfilehash: e466edf9232558b9e270f54ee2849cd9b22ad121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="f52d2-103">Hello Azure portal ile akış uç noktalarını ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="f52d2-103">Scale streaming endpoints with hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="f52d2-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f52d2-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="f52d2-105">toocomplete Bu öğretici bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f52d2-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="f52d2-106">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f52d2-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="f52d2-107">**Premium** akış uç noktaları, adanmış ve ölçeklenebilir bant genişliği kapasitesi sağlar; dolayısıyla gelişmiş iş yükleri için uygundur.</span><span class="sxs-lookup"><span data-stu-id="f52d2-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="f52d2-108">**Premium** akış uç noktası olan müşteriler, varsayılan olarak bir akış birimi (SU) alır.</span><span class="sxs-lookup"><span data-stu-id="f52d2-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="f52d2-109">Akış uç noktası hello SUs eklenerek genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="f52d2-109">hello streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="f52d2-110">Her SU ek bant genişliği kapasitesi toohello uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="f52d2-110">Each SU provides additional bandwidth capacity toohello application.</span></span> <span data-ttu-id="f52d2-111">Akış uç nokta türleri ve CDN yapılandırma hakkında daha fazla bilgi için bkz: Merhaba [akış uç noktası genel bakış](media-services-portal-manage-streaming-endpoints.md) konu.</span><span class="sxs-lookup"><span data-stu-id="f52d2-111">For more information about streaming endpoint types and CDN configuration, see hello [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="f52d2-112">Bu konuda gösterilmektedir nasıl tooscale akış uç noktası.</span><span class="sxs-lookup"><span data-stu-id="f52d2-112">This topic shows how tooscale a streaming endpoint.</span></span>

<span data-ttu-id="f52d2-113">Fiyatlandırma ayrıntıları hakkında daha fazla bilgi için bkz. [Media Services Fiyatlandırma Ayrıntıları](http://go.microsoft.com/fwlink/?LinkId=275107).</span><span class="sxs-lookup"><span data-stu-id="f52d2-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="f52d2-114">Akış uç noktalarını ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="f52d2-114">Scale streaming endpoints</span></span>

<span data-ttu-id="f52d2-115">toochange hello akış birim sayısını hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="f52d2-115">toochange hello number of streaming units, do hello following:</span></span>

1. <span data-ttu-id="f52d2-116">Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="f52d2-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="f52d2-117">Merhaba, **ayarları** penceresinde, seçin **akış uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="f52d2-117">In hello **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="f52d2-118">Merhaba akış uç noktasında tooscale istediğiniz'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f52d2-118">Click on hello streaming endpoint that you want tooscale.</span></span> 

    [!NOTE] <span data-ttu-id="f52d2-119">Yalnızca ölçeklendirebilirsiniz **Premium** akış uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="f52d2-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="f52d2-120">Merhaba kaydırıcı toospecify hello akış birim sayısını taşıyın.</span><span class="sxs-lookup"><span data-stu-id="f52d2-120">Move hello slider toospecify hello number of streaming units.</span></span>

    ![Akış uç noktası](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="f52d2-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f52d2-122">Next steps</span></span>
<span data-ttu-id="f52d2-123">Media Services öğrenme yollarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="f52d2-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f52d2-124">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="f52d2-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

