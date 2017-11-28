---
title: "Sık kullanılan otomatik ölçeklendirme desenlerini aaaOverview | Microsoft Docs"
description: "Azure'da hello ortak desenler tooauto bazıları kaynağınız ölçeklendirmek öğrenin."
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
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="423a4-103">Sık kullanılan otomatik ölçeklendirme desenlerini genel bakış</span><span class="sxs-lookup"><span data-stu-id="423a4-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="423a4-104">Bu makalede, Azure kaynak hello ortak desenler tooscale bazıları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="423a4-104">This article describes some of hello common patterns tooscale your resource in Azure.</span></span>

<span data-ttu-id="423a4-105">Azure İzleyici otomatik ölçek tooVirtual makine ölçek kümeleri (VMSS), bulut Hizmetleri, uygulama hizmeti planları ve uygulama hizmeti ortamları yalnızca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="423a4-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="423a4-106">Sağlar kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="423a4-106">Lets get started</span></span>

<span data-ttu-id="423a4-107">Bu makalede, otomatik ölçekli bilgi sahibi olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="423a4-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="423a4-108">Yapabilecekleriniz [başlatılan burada tooscale, kaynak alma][1].</span><span class="sxs-lookup"><span data-stu-id="423a4-108">You can [get started here tooscale your resource][1].</span></span> <span data-ttu-id="423a4-109">Merhaba hello ortak ölçek desenler bazıları verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="423a4-109">hello following are some of hello common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="423a4-110">CPU üzerinde göre ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="423a4-110">Scale based on CPU</span></span>

<span data-ttu-id="423a4-111">Bir web uygulaması (/ VMSS/bulut hizmeti rolü) sahip ve</span><span class="sxs-lookup"><span data-stu-id="423a4-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="423a4-112">Tooscale istediğiniz çıkış/dayalı olarak CPU ölçek.</span><span class="sxs-lookup"><span data-stu-id="423a4-112">You want tooscale out/scale in based on CPU.</span></span>
- <span data-ttu-id="423a4-113">Ayrıca, tooensure istediğiniz en az bir örnek sayısı yoktur.</span><span class="sxs-lookup"><span data-stu-id="423a4-113">Additionally, you want tooensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="423a4-114">Ayrıca, bir şekilde ölçeklendirebilirsiniz örnekleri sınırı toohello sayısını ayarlayın tooensure istiyor.</span><span class="sxs-lookup"><span data-stu-id="423a4-114">Also, you want tooensure that you set a maximum limit toohello number of instances you can scale to.</span></span>

![CPU üzerinde göre ölçeklendirin][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="423a4-116">Haftanın günü vs hafta sonu farklı ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="423a4-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="423a4-117">Bir web uygulaması (/ VMSS/bulut hizmeti rolü) sahip ve</span><span class="sxs-lookup"><span data-stu-id="423a4-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="423a4-118">Varsayılan olarak (günlerinde) 3 örneklerinin istediğiniz</span><span class="sxs-lookup"><span data-stu-id="423a4-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="423a4-119">Hafta sonu trafiği beklemeyen ve bu nedenle hafta sonu too1 örneği aşağı tooscale istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="423a4-119">You don't expect traffic on weekends and hence you want tooscale down too1 instance on weekends.</span></span>

![Haftanın günü vs hafta sonu farklı ölçeklendirme][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="423a4-121">Farklı tatilleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="423a4-121">Scale differently during holidays</span></span>

<span data-ttu-id="423a4-122">Bir web uygulaması (/ VMSS/bulut hizmeti rolü) sahip ve</span><span class="sxs-lookup"><span data-stu-id="423a4-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="423a4-123">Yukarı/Aşağı CPU kullanımında varsayılan olarak temel tooscale istediğiniz</span><span class="sxs-lookup"><span data-stu-id="423a4-123">You want tooscale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="423a4-124">Ancak, tatilde (veya işletmeniz için önemli olan belirli gün) sırasında toooverride hello Varsayılanları istediğiniz ve elinizin daha fazla kapasiteye sahip.</span><span class="sxs-lookup"><span data-stu-id="423a4-124">However, during holiday season (or specific days that are important for your business) you want toooverride hello defaults and have more capacity at your disposal.</span></span>

![Ölçek farklı üzerinde tatiller][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="423a4-126">Özel bir ölçü göre ölçeklendirin</span><span class="sxs-lookup"><span data-stu-id="423a4-126">Scale based on custom metric</span></span>

<span data-ttu-id="423a4-127">Bir web ön uç ve hello arka ucuyla iletişim kuran bir API katmanı vardır.</span><span class="sxs-lookup"><span data-stu-id="423a4-127">You have a web front end and a API tier that communicates with hello backend.</span></span> 

- <span data-ttu-id="423a4-128">Özel olaylar hello ön uçtaki göre tooscale hello API katmanı istediğiniz (örnek: Merhaba alışveriş sepeti hello öğelerin sayısı temel kullanıma alma işleminizi tooscale istediğiniz)</span><span class="sxs-lookup"><span data-stu-id="423a4-128">You want tooscale hello API tier based on custom events in hello front end (example: You want tooscale your checkout process based on hello number of items in hello shopping cart)</span></span>

![Özel bir ölçü göre ölçeklendirin][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png