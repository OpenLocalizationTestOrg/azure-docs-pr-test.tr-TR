---
title: "Olay izleme ile sorunlarını giderme | Microsoft Docs"
description: "Microsoft Azure Service Fabric Services'de dağıtırken karşılaşılan en yaygın sorunları."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: e60bd4b9291cb2fc748921e42f11f54bb545984f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="a6563-103">Azure Service Fabric Services'de dağıttığınızda sık rastlanan sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="a6563-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="a6563-104">Geliştirici bilgisayarınızda Hizmetleri çalıştırırken, kullanımı kolay [hata ayıklama Visual Studio Araçları](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="a6563-104">When you're running services on your developer computer, it is easy to use [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="a6563-105">Uzak kümeleri için [sistem durumu raporlarının](service-fabric-view-entities-aggregated-health.md) her zaman başlatmak için iyi bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="a6563-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place to start.</span></span> <span data-ttu-id="a6563-106">Bu raporlara erişmek için en kolay yollarından PowerShell aracılığıyla olan veya [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a6563-106">The easiest ways to access these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="a6563-107">Bu makalede, uzak bir küme hata ayıklama ve bu araçlardan birini kullanımıyla ilgili temel bilgilere sahipsiniz varsayar.</span><span class="sxs-lookup"><span data-stu-id="a6563-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how to use either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="a6563-108">Uygulama kilitlenme</span><span class="sxs-lookup"><span data-stu-id="a6563-108">Application crash</span></span>
<span data-ttu-id="a6563-109">"Bölüm aşağıdadır hedef çoğaltma veya örnek sayısının" rapordur hizmetinizi kilitlenen bir göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="a6563-109">The "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="a6563-110">Bulmanın nerede hizmetinizi kilitlenen biraz daha fazla araştırma alır.</span><span class="sxs-lookup"><span data-stu-id="a6563-110">To find out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="a6563-111">Hizmetinizi ölçekte çalışırken en iyi arkadaşınızın iyi planlanmış genişletme izlemeleri kümesi olur.</span><span class="sxs-lookup"><span data-stu-id="a6563-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="a6563-112">Denemeden önerin [Azure tanılama](service-fabric-diagnostics-how-to-setup-wad.md) bu izlemeleri toplamak ve bir çözüm gibi kullanılarak [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) görüntüleme ve izlemeleri arama için.</span><span class="sxs-lookup"><span data-stu-id="a6563-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching the traces.</span></span>

![SFX bölüm sistem durumu](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="a6563-114">Hizmet veya aktör başlatma sırasında</span><span class="sxs-lookup"><span data-stu-id="a6563-114">During service or actor initialization</span></span>
<span data-ttu-id="a6563-115">Hizmet türü başlatılmadan önce tüm özel durumlar işleminin çökmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="a6563-115">Any exceptions before the service type is initialized will cause the process to crash.</span></span> <span data-ttu-id="a6563-116">Bu kilitlenme türleri için uygulama olay günlüğüne hizmetinizden hata gösterir.</span><span class="sxs-lookup"><span data-stu-id="a6563-116">For these types of crashes, the application event log will show the error from your service.</span></span>
<span data-ttu-id="a6563-117">Bu hizmet başlatılmadan önce görmek için en yaygın durumlardır.</span><span class="sxs-lookup"><span data-stu-id="a6563-117">These are the most common exceptions to see before the service is initialized.</span></span>

<span data-ttu-id="a6563-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="a6563-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="a6563-119">Bu hata genellikle derleme bağımlılıkları nedeniyle eksik.</span><span class="sxs-lookup"><span data-stu-id="a6563-119">This error is often due to missing assembly dependencies.</span></span> <span data-ttu-id="a6563-120">Visual Studio ya da düğümü için Genel Derleme Önbelleği CopyLocal özelliğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="a6563-120">Check the CopyLocal property in Visual Studio or the global assembly cache for the node.</span></span>

<span data-ttu-id="a6563-121">***System.Runtime.InteropServices.COMException*** *adresindeki System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="a6563-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="a6563-122">Bu, kayıtlı hizmet türü adı hizmet bildirimi eşleşmediğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a6563-122">This indicates that the registered service type name does not match the service manifest.</span></span>

<span data-ttu-id="a6563-123">[Azure tanılama](service-fabric-diagnostics-how-to-setup-wad.md) tüm düğümler için uygulama olay günlüğünü otomatik olarak karşıya yüklemek için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="a6563-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured to upload the application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="a6563-124">RunAsync() veya OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="a6563-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="a6563-125">Kilitlenme başlatma veya kayıtlı hizmet türü veya aktör çalıştırılması sırasında oluşursa, Azure Service Fabric tarafından özel durum yakalandı.</span><span class="sxs-lookup"><span data-stu-id="a6563-125">If the crash happens during the initialization or running of your registered service type or actor, the exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="a6563-126">Bu "Sonraki adımlar" bölümünde ayrıntılı EventSource sağlayıcılardan görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6563-126">You can view these from the EventSource providers detailed in the "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6563-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a6563-127">Next steps</span></span>
<span data-ttu-id="a6563-128">Service Fabric tarafından sağlanan mevcut Tanılama hakkında daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="a6563-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="a6563-129">Güvenilir aktörler tanılama</span><span class="sxs-lookup"><span data-stu-id="a6563-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="a6563-130">Güvenilir hizmetler tanılama</span><span class="sxs-lookup"><span data-stu-id="a6563-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

