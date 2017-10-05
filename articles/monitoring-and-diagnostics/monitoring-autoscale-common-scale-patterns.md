---
title: "Sık kullanılan otomatik ölçeklendirme desenlerini genel bakış | Microsoft Docs"
description: "Bazı ölçeği otomatik olarak ortak desenler kaynağınız Azure öğrenin."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fce51546e041c8989d813c3935e058c52b38ba77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="84bbd-103">Sık kullanılan otomatik ölçeklendirme desenlerini genel bakış</span><span class="sxs-lookup"><span data-stu-id="84bbd-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="84bbd-104">Bu makalede Azure kaynağınız ölçeklendirmek için ortak desenler bazıları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="84bbd-104">This article describes some of the common patterns to scale your resource in Azure.</span></span>

<span data-ttu-id="84bbd-105">Azure İzleyici otomatik ölçek yalnızca sanal makine ölçek kümeleri (VMSS), bulut Hizmetleri, uygulama hizmeti planları ve app service ortamları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="84bbd-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="84bbd-106">Sağlar kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="84bbd-106">Lets get started</span></span>

<span data-ttu-id="84bbd-107">Bu makalede, otomatik ölçekli bilgi sahibi olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="84bbd-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="84bbd-108">Yapabilecekleriniz [kaynağınız ölçeklendirmek için buradan başlayın][1].</span><span class="sxs-lookup"><span data-stu-id="84bbd-108">You can [get started here to scale your resource][1].</span></span> <span data-ttu-id="84bbd-109">Ortak ölçek desenler bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="84bbd-109">The following are some of the common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="84bbd-110">CPU üzerinde göre ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="84bbd-110">Scale based on CPU</span></span>

<span data-ttu-id="84bbd-111">Bir web uygulaması (/ VMSS/bulut hizmeti rolü) sahip ve</span><span class="sxs-lookup"><span data-stu-id="84bbd-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="84bbd-112">İstediğiniz ölçek genişletme/ölçek dayalı olarak CPU.</span><span class="sxs-lookup"><span data-stu-id="84bbd-112">You want to scale out/scale in based on CPU.</span></span>
- <span data-ttu-id="84bbd-113">Ayrıca, en az bir örnek sayısı yoktur sağlamak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="84bbd-113">Additionally, you want to ensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="84bbd-114">Ayrıca, için ölçeklendirebilirsiniz örnek sayısı maksimum bir sınır koymak sağlamak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="84bbd-114">Also, you want to ensure that you set a maximum limit to the number of instances you can scale to.</span></span>

![CPU üzerinde göre ölçeklendirin][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="84bbd-116">Haftanın günü vs hafta sonu farklı ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="84bbd-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="84bbd-117">Bir web uygulaması (/ VMSS/bulut hizmeti rolü) sahip ve</span><span class="sxs-lookup"><span data-stu-id="84bbd-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="84bbd-118">Varsayılan olarak (günlerinde) 3 örneklerinin istediğiniz</span><span class="sxs-lookup"><span data-stu-id="84bbd-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="84bbd-119">Hafta sonu trafiği beklemeyen ve hafta sonu aşağıya doğru 1 örneği ölçeklendirmek istiyorsanız bu nedenle.</span><span class="sxs-lookup"><span data-stu-id="84bbd-119">You don't expect traffic on weekends and hence you want to scale down to 1 instance on weekends.</span></span>

![Haftanın günü vs hafta sonu farklı ölçeklendirme][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="84bbd-121">Farklı tatilleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="84bbd-121">Scale differently during holidays</span></span>

<span data-ttu-id="84bbd-122">Bir web uygulaması (/ VMSS/bulut hizmeti rolü) sahip ve</span><span class="sxs-lookup"><span data-stu-id="84bbd-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="84bbd-123">Varsayılan olarak CPU kullanımı dikkate alarak yukarı/aşağı ölçeklendirmek istediğiniz</span><span class="sxs-lookup"><span data-stu-id="84bbd-123">You want to scale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="84bbd-124">Ancak, tatilde (veya işletmeniz için önemli olan belirli gün) sırasında varsayılanlarını geçersiz kıl ve daha fazla kapasite elinizin ister.</span><span class="sxs-lookup"><span data-stu-id="84bbd-124">However, during holiday season (or specific days that are important for your business) you want to override the defaults and have more capacity at your disposal.</span></span>

![Ölçek farklı üzerinde tatiller][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="84bbd-126">Özel bir ölçü göre ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="84bbd-126">Scale based on custom metric</span></span>

<span data-ttu-id="84bbd-127">Bir web ön uç ve arka uç ile iletişim kuran bir API katmanı vardır.</span><span class="sxs-lookup"><span data-stu-id="84bbd-127">You have a web front end and a API tier that communicates with the backend.</span></span> 

- <span data-ttu-id="84bbd-128">Özel olaylar ön uçtaki temel API katmanı istediğiniz (örnek: alışveriş sepeti öğelerinin sayısına dayalı olarak kullanıma alma işleminizi ölçeklendirmek istediğiniz)</span><span class="sxs-lookup"><span data-stu-id="84bbd-128">You want to scale the API tier based on custom events in the front end (example: You want to scale your checkout process based on the number of items in the shopping cart)</span></span>

![Özel bir ölçü göre ölçeklendirin][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png