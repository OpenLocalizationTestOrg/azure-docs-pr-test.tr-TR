---
title: "Service Fabric aaaAzure modelleri ve senaryoları | Microsoft Docs"
description: "En iyi yöntemleri öğrenin ve, yeniden kullanılabilir desenleri toodesign kanıtlanmış geliştirmek ve, mikro Service Fabric üzerinde çalışır."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 3811420eb53d9a49e490dd2e2e5319d8dea5629c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="1a4f8-103">Service Fabric modelleri ve senaryoları</span><span class="sxs-lookup"><span data-stu-id="1a4f8-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="1a4f8-104">Azure Service Fabric kullanarak büyük ölçekli mikro derlemeye arıyorsanız, kimin tasarlanmış ve bu platform (PaaS) hizmet olarak yerleşik hello uzmanlarından öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from hello experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="1a4f8-105">Uygun mimarisi ile başlayın ve ardından öğrenin nasıl uygulamanız için toooptimize kaynakları.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-105">Get started with proper architecture, and then learn how toooptimize resources for your application.</span></span> <span data-ttu-id="1a4f8-106">Merhaba [Service Fabric desenleri ve uygulamalar](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) indirmelere gerçek müşteriler tarafından Service Fabric senaryoları ve uygulama alanları hakkında sık sorulan hello soruları yanıtlar.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-106">hello [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers hello questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="1a4f8-107">Toodesign, geliştirmek ve nasıl, mikro hizmet en iyi yöntemler ve kanıtlanmış, yeniden kullanılabilir desenler kullanılarak doku üzerinde çalışması öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-107">Find out how toodesign, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="1a4f8-108">Service Fabric özetini almak ve derin küme en iyi duruma getirme ve eski uygulamalar geçirme güvenlik, IOT ve oyun motorları barındırma ölçekte kapsayan konularını içine yakından inceleyin.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="1a4f8-109">Çeşitli iş yükleri için kesintisiz teslim bakın ve hatta Linux desteği ve kapsayıcıları hello ayrıntılı bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-109">Look at continuous delivery for various workloads, and even get hello details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="1a4f8-110">Giriş</span><span class="sxs-lookup"><span data-stu-id="1a4f8-110">Introduction</span></span>
<span data-ttu-id="1a4f8-111">En iyi uygulamaları inceleyin ve platform (PaaS) hizmet olarak altyapı üzerinden bir hizmet (Iaas) olarak seçme hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="1a4f8-112">Merhaba, aşağıdaki kanıtlanmış uygulama tasarım kurallara göre ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-112">Get hello details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="1a4f8-113">Video</span><span class="sxs-lookup"><span data-stu-id="1a4f8-113">Video</span></span></th><th><span data-ttu-id="1a4f8-114">PowerPoint deste</span><span class="sxs-lookup"><span data-stu-id="1a4f8-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="1a4f8-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Giriş tooService yapı</a></span><span class="sxs-lookup"><span data-stu-id="1a4f8-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction tooService Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="1a4f8-116">Küme planlama ve Yönetimi</span><span class="sxs-lookup"><span data-stu-id="1a4f8-116">Cluster planning and management</span></span>
<span data-ttu-id="1a4f8-117">Kapasite planlaması, küme en iyi duruma getirme ve bu göz Azure Service Fabric kümesi güvenliği hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="1a4f8-118">Video</span><span class="sxs-lookup"><span data-stu-id="1a4f8-118">Video</span></span></th><th><span data-ttu-id="1a4f8-119">PowerPoint deste</span><span class="sxs-lookup"><span data-stu-id="1a4f8-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="1a4f8-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Küme planlama ve Yönetimi</a></span><span class="sxs-lookup"><span data-stu-id="1a4f8-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="1a4f8-121">Hiper ölçekli web</span><span class="sxs-lookup"><span data-stu-id="1a4f8-121">Hyper-scale web</span></span>
<span data-ttu-id="1a4f8-122">Kullanılabilirlik ve güvenilirlik, Hiper ölçekli ve durum yönetimi dahil olmak üzere hiper ölçekli web geçici kavramlarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="1a4f8-123">Video</span><span class="sxs-lookup"><span data-stu-id="1a4f8-123">Video</span></span></th><th><span data-ttu-id="1a4f8-124">PowerPoint deste</span><span class="sxs-lookup"><span data-stu-id="1a4f8-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="1a4f8-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hiper ölçekli web</a></span><span class="sxs-lookup"><span data-stu-id="1a4f8-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="1a4f8-126">IoT</span><span class="sxs-lookup"><span data-stu-id="1a4f8-126">IoT</span></span>
<span data-ttu-id="1a4f8-127">Azure Service Fabric hello Azure IOT ardışık düzen, çok kiracılı ve IOT ölçekte da dahil olmak üzere, hello bağlamında Hello nesnelerin interneti (IOT) keşfedin.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-127">Explore hello Internet of Things (IoT) in hello context of Azure Service Fabric, including hello Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="1a4f8-128">Video</span><span class="sxs-lookup"><span data-stu-id="1a4f8-128">Video</span></span></th><th><span data-ttu-id="1a4f8-129">PowerPoint deste</span><span class="sxs-lookup"><span data-stu-id="1a4f8-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="1a4f8-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="1a4f8-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="1a4f8-131">Oyun</span><span class="sxs-lookup"><span data-stu-id="1a4f8-131">Gaming</span></span>
<span data-ttu-id="1a4f8-132">Bırakma tabanlı oyunlar, etkileşimli oyunlar ve varolan oyun altyapıları barındırma arayın.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="1a4f8-133">Video</span><span class="sxs-lookup"><span data-stu-id="1a4f8-133">Video</span></span></th><th><span data-ttu-id="1a4f8-134">PowerPoint deste</span><span class="sxs-lookup"><span data-stu-id="1a4f8-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="1a4f8-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Oyun</a></span><span class="sxs-lookup"><span data-stu-id="1a4f8-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="1a4f8-136">Sürekli teslim</span><span class="sxs-lookup"><span data-stu-id="1a4f8-136">Continuous delivery</span></span>
<span data-ttu-id="1a4f8-137">Visual Studio Team Services, iş akışı derleme/paket/yayımlama, çoklu ortam kurulumu ve hizmet paketi/paylaşımı sürekli tümleştirme/kesintisiz teslim de dahil olmak üzere kavramları keşfedin.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="1a4f8-138">Video</span><span class="sxs-lookup"><span data-stu-id="1a4f8-138">Video</span></span></th><th><span data-ttu-id="1a4f8-139">PowerPoint deste</span><span class="sxs-lookup"><span data-stu-id="1a4f8-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="1a4f8-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Kesintisiz teslim</a></span><span class="sxs-lookup"><span data-stu-id="1a4f8-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="1a4f8-141">Geçiş</span><span class="sxs-lookup"><span data-stu-id="1a4f8-141">Migration</span></span>
<span data-ttu-id="1a4f8-142">Bir bulut hizmetinden ayrıca eski uygulamaların toomigration geçiş hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-142">Learn about migrating from a cloud service, in addition toomigration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="1a4f8-143">Video</span><span class="sxs-lookup"><span data-stu-id="1a4f8-143">Video</span></span></th><th><span data-ttu-id="1a4f8-144">PowerPoint deste</span><span class="sxs-lookup"><span data-stu-id="1a4f8-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="1a4f8-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Geçiş</a></span><span class="sxs-lookup"><span data-stu-id="1a4f8-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="1a4f8-146">Kapsayıcılar ve Linux desteği</span><span class="sxs-lookup"><span data-stu-id="1a4f8-146">Containers and Linux support</span></span>
<span data-ttu-id="1a4f8-147">Merhaba yanıt toohello soru Al "neden kapsayıcıları?"</span><span class="sxs-lookup"><span data-stu-id="1a4f8-147">Get hello answer toohello question, "Why containers?"</span></span> <span data-ttu-id="1a4f8-148">Windows kapsayıcıları, Linux destekler ve Linux kapsayıcıları düzenleme için hello önizleme hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-148">Learn about hello preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="1a4f8-149">Ayrıca, öğrenin toomigrate .NET Core uygulamaları tooLinux.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-149">Plus, find out how toomigrate .NET Core apps tooLinux.</span></span>

<table><tr><th><span data-ttu-id="1a4f8-150">Video</span><span class="sxs-lookup"><span data-stu-id="1a4f8-150">Video</span></span></th><th><span data-ttu-id="1a4f8-151">PowerPoint deste</span><span class="sxs-lookup"><span data-stu-id="1a4f8-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="1a4f8-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Kapsayıcılar ve Linux desteği</a></span><span class="sxs-lookup"><span data-stu-id="1a4f8-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="1a4f8-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1a4f8-153">Next steps</span></span>
<span data-ttu-id="1a4f8-154">Service Fabric modelleri ve senaryoları hakkında öğrendiğinize göre daha fazla nasıl çok bilgiyi[oluşturun ve kümelerini Yönet](service-fabric-deploy-anywhere.md), [bulut Hizmetleri uygulamaları tooService doku geçirmek](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [ayarlama Kesintisiz teslim](service-fabric-set-up-continuous-integration.md), ve [kapsayıcıları dağıtın](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1a4f8-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how too[create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps tooService Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
