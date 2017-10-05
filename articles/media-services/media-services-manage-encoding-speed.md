---
title: "Hız ve Azure Media Services ile kodlama eşzamanlılık yönetme | Microsoft Docs"
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
ms.openlocfilehash: 0463904fd9bf1138587d0d214e572ddd38cc2184
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="ad05a-103">Hız ve, kodlama eşzamanlılık yönetme</span><span class="sxs-lookup"><span data-stu-id="ad05a-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="ad05a-104">Bu makalede hızı ve kodlama işleri/görevlerinizi eşzamanlılığı nasıl yönetebilmeniz için kısa bir genel bakış sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ad05a-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="ad05a-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ad05a-105">Overview</span></span>

<span data-ttu-id="ad05a-106">Media Services, bir **ayrılmış birim türü** ile görevleri işleme medyanızı işlenir hızını belirler.</span><span class="sxs-lookup"><span data-stu-id="ad05a-106">In Media Services, a **Reserved Unit Type** determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="ad05a-107">Şu ayrılmış birim türlerinden birini seçebilirsiniz: **S1**, **S2** veya **S3**.</span><span class="sxs-lookup"><span data-stu-id="ad05a-107">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="ad05a-108">Örneğin, aynı kodlama işi **S2** ayrılmış birim türünü kullandığınızda **S1** türüne göre daha hızlı çalışır.</span><span class="sxs-lookup"><span data-stu-id="ad05a-108">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span> <span data-ttu-id="ad05a-109">[Kodlama birimleri ölçeklendirme](media-services-scale-media-processing-overview.md) konu arasında farklı kodlama hızları seçerken karar vermenize yardımcı olan bir tablo gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad05a-109">The [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="ad05a-110">Ayrılmış birim türü belirtmeye ek olarak, hesabınızla sağlayacak belirtebilirsiniz **ayrılan birimler**.</span><span class="sxs-lookup"><span data-stu-id="ad05a-110">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units**.</span></span> <span data-ttu-id="ad05a-111">Sağlanan ayrılmış birim sayısı, verili bir hesapta eşzamanlı olarak işlenebilecek medya görevlerinin sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="ad05a-111">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="ad05a-112">Örneğin, beş medya görevler eşzamanlı olarak kadar uzun çalışıyor olacak beş ayrılmış birimler, hesabınız varsa, olarak işlenecek görevler vardır.</span><span class="sxs-lookup"><span data-stu-id="ad05a-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks to be processed.</span></span> <span data-ttu-id="ad05a-113">Kalan görevler sıraya bekler ve sıralı olarak çalışan bir görev tamamlandığında işlemek için toplanmış.</span><span class="sxs-lookup"><span data-stu-id="ad05a-113">The remaining tasks will wait in the queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="ad05a-114">Bir hesap sağlanan tüm ayrılan birimler yoksa, ardından görevleri sırayla çekilir.</span><span class="sxs-lookup"><span data-stu-id="ad05a-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="ad05a-115">Bu durumda, sonraki bir başlangıç ve bitiş görev arasındaki bekleme süresine sistemde kaynakları kullanılabilirliğine bağlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ad05a-115">In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.</span></span>

<span data-ttu-id="ad05a-116">Ayrıntılı bilgi ve kodlama birimleri ölçeklendirme gösteren örnekler için bkz: [bu](media-services-scale-media-processing-overview.md) konu.</span><span class="sxs-lookup"><span data-stu-id="ad05a-116">For detailed information and examples that show how to scale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="ad05a-117">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="ad05a-117">Next step</span></span>

[<span data-ttu-id="ad05a-118">Kodlama ölçek birimleri</span><span class="sxs-lookup"><span data-stu-id="ad05a-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="ad05a-119">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="ad05a-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ad05a-120">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="ad05a-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

