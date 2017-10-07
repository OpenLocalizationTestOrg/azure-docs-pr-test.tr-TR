---
title: "AAA Yönet hızı ve Azure Media Services ile kodlama eşzamanlılık | Microsoft Docs"
description: "Bu makalede hızı ve Azure Media Services ile kodlama işleri/görevleri eşzamanlılığı nasıl yönetebilmeniz için kısa bir genel bakış sunulmaktadır."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="07485-103">Hız ve, kodlama eşzamanlılık yönetme</span><span class="sxs-lookup"><span data-stu-id="07485-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="07485-104">Bu makalede hızı ve kodlama işleri/görevlerinizi eşzamanlılığı nasıl yönetebilmeniz için kısa bir genel bakış sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="07485-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="07485-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="07485-105">Overview</span></span>

<span data-ttu-id="07485-106">Media Services, bir **ayrılmış birim türü** ile görevleri işleme medyanızı işlenir hello hızını belirler.</span><span class="sxs-lookup"><span data-stu-id="07485-106">In Media Services, a **Reserved Unit Type** determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="07485-107">Merhaba aşağıdaki arasında seçim yapabilirsiniz ayrılmış birim türleri: **S1**, **S2**, veya **S3**.</span><span class="sxs-lookup"><span data-stu-id="07485-107">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="07485-108">Örneğin, aynı kodlama işi çalıştıktan daha hızlı hello kullandığınızda hello **S2** ayrılmış birim türü karşılaştırma toohello **S1** türü.</span><span class="sxs-lookup"><span data-stu-id="07485-108">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span> <span data-ttu-id="07485-109">Merhaba [kodlama birimleri ölçeklendirme](media-services-scale-media-processing-overview.md) konu arasında farklı kodlama hızları seçerken karar vermenize yardımcı olan bir tablo gösterir.</span><span class="sxs-lookup"><span data-stu-id="07485-109">hello [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="07485-110">Ayrıca toospecifying hello ayrılmış birim türü, hesabınızla tooprovision belirtebilirsiniz **ayrılan birimler**.</span><span class="sxs-lookup"><span data-stu-id="07485-110">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units**.</span></span> <span data-ttu-id="07485-111">sağlanan ayrılmış birim Hello sayısı belirli bir hesap eşzamanlı olarak işlenebilecek ortam görevleri hello sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="07485-111">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="07485-112">Örneğin, beş medya görevler eşzamanlı olarak kadar uzun çalışıyor olacak beş ayrılmış birimler, hesabınız varsa, olarak vardır görevleri toobe işlenir.</span><span class="sxs-lookup"><span data-stu-id="07485-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks toobe processed.</span></span> <span data-ttu-id="07485-113">Merhaba Kalan görevler hello kuyrukta bekler ve sıralı olarak çalışan bir görev tamamlandığında işlemek için toplanmış.</span><span class="sxs-lookup"><span data-stu-id="07485-113">hello remaining tasks will wait in hello queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="07485-114">Bir hesap sağlanan tüm ayrılan birimler yoksa, ardından görevleri sırayla çekilir.</span><span class="sxs-lookup"><span data-stu-id="07485-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="07485-115">Bu durumda, hello bir görev tamamlama arasındaki süre bekleyin ve hello sonraki bir başlangıç kaynakları hello kullanılabilirliğini hello sistemde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="07485-115">In this case, hello wait time between one task finishing and hello next one starting will depend on hello availability of resources in hello system.</span></span>

<span data-ttu-id="07485-116">Ayrıntılı bilgi ve örnekler için nasıl tooscale kodlama birimlerini görmek gösteren [bu](media-services-scale-media-processing-overview.md) konu.</span><span class="sxs-lookup"><span data-stu-id="07485-116">For detailed information and examples that show how tooscale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="07485-117">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="07485-117">Next step</span></span>

[<span data-ttu-id="07485-118">Kodlama ölçek birimleri</span><span class="sxs-lookup"><span data-stu-id="07485-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="07485-119">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="07485-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="07485-120">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="07485-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

