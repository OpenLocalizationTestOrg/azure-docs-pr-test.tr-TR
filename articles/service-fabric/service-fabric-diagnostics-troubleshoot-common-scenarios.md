---
title: Olay izleme ile aaaTroubleshooting | Microsoft Docs
description: "Microsoft Azure Service Fabric Services'de dağıtırken karşılaşılan en yaygın sorunları hello."
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
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="449f8-103">Azure Service Fabric Services'de dağıttığınızda sık rastlanan sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="449f8-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="449f8-104">Geliştirici bilgisayarınızda Hizmetleri çalıştırırken kolay toouse olan [hata ayıklama Visual Studio Araçları](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="449f8-104">When you're running services on your developer computer, it is easy toouse [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="449f8-105">Uzak kümeleri için [sistem durumu raporlarının](service-fabric-view-entities-aggregated-health.md) her zaman iyi toostart olur.</span><span class="sxs-lookup"><span data-stu-id="449f8-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place toostart.</span></span> <span data-ttu-id="449f8-106">Bu raporlar içindir PowerShell aracılığıyla en kolay yolu tooaccess hello veya [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="449f8-106">hello easiest ways tooaccess these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="449f8-107">Bu makalede, uzak bir küme hata ayıklama ve nasıl ilgili temel bilgilere sahipsiniz varsayar bunlardan araçları toouse.</span><span class="sxs-lookup"><span data-stu-id="449f8-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how toouse either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="449f8-108">Uygulama kilitlenme</span><span class="sxs-lookup"><span data-stu-id="449f8-108">Application crash</span></span>
<span data-ttu-id="449f8-109">Merhaba "bölümdür aşağıda hedef çoğaltma veya örnek sayısının" rapordur hizmetinizi kilitlenen bir göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="449f8-109">hello "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="449f8-110">Burada hizmetinizi kilitlenen çıkışı toofind biraz daha fazla araştırma alır.</span><span class="sxs-lookup"><span data-stu-id="449f8-110">toofind out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="449f8-111">Hizmetinizi ölçekte çalışırken en iyi arkadaşınızın iyi planlanmış genişletme izlemeleri kümesi olur.</span><span class="sxs-lookup"><span data-stu-id="449f8-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="449f8-112">Denemeden önerin [Azure tanılama](service-fabric-diagnostics-how-to-setup-wad.md) bu izlemeleri toplamak ve bir çözüm gibi kullanılarak [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) görüntüleme ve arama hello izlemeleri için.</span><span class="sxs-lookup"><span data-stu-id="449f8-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching hello traces.</span></span>

![SFX bölüm sistem durumu](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="449f8-114">Hizmet veya aktör başlatma sırasında</span><span class="sxs-lookup"><span data-stu-id="449f8-114">During service or actor initialization</span></span>
<span data-ttu-id="449f8-115">Merhaba hizmet türü başlatılmadan önce tüm özel durumlar hello işlem toocrash neden olur.</span><span class="sxs-lookup"><span data-stu-id="449f8-115">Any exceptions before hello service type is initialized will cause hello process toocrash.</span></span> <span data-ttu-id="449f8-116">Bu kilitlenme türlerinde hello uygulama olay günlüğü hizmetinizden hello hata gösterir.</span><span class="sxs-lookup"><span data-stu-id="449f8-116">For these types of crashes, hello application event log will show hello error from your service.</span></span>
<span data-ttu-id="449f8-117">Merhaba hizmet başlatılmadan önce hello en yaygın özel durumları toosee bunlar.</span><span class="sxs-lookup"><span data-stu-id="449f8-117">These are hello most common exceptions toosee before hello service is initialized.</span></span>

<span data-ttu-id="449f8-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="449f8-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="449f8-119">Bu hata genellikle toomissing derleme bağımlılıkları olur.</span><span class="sxs-lookup"><span data-stu-id="449f8-119">This error is often due toomissing assembly dependencies.</span></span> <span data-ttu-id="449f8-120">Visual Studio veya hello Genel Derleme Önbelleği hello düğüm için Hello CopyLocal özelliği denetleyin.</span><span class="sxs-lookup"><span data-stu-id="449f8-120">Check hello CopyLocal property in Visual Studio or hello global assembly cache for hello node.</span></span>

<span data-ttu-id="449f8-121">***System.Runtime.InteropServices.COMException*** *adresindeki System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="449f8-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="449f8-122">Bu, hello kayıtlı hizmet türü adının hello hizmet bildirimi eşleşmiyor gösterir.</span><span class="sxs-lookup"><span data-stu-id="449f8-122">This indicates that hello registered service type name does not match hello service manifest.</span></span>

<span data-ttu-id="449f8-123">[Azure tanılama](service-fabric-diagnostics-how-to-setup-wad.md) yapılandırılmış tooupload hello uygulama olay günlüğü, tüm düğümler için otomatik olarak olabilir.</span><span class="sxs-lookup"><span data-stu-id="449f8-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured tooupload hello application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="449f8-124">RunAsync() veya OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="449f8-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="449f8-125">Merhaba kilitlenme hello başlatma veya kayıtlı hizmet türü veya aktör çalıştırılması sırasında oluşursa, Azure Service Fabric tarafından hello özel durum yakalandı.</span><span class="sxs-lookup"><span data-stu-id="449f8-125">If hello crash happens during hello initialization or running of your registered service type or actor, hello exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="449f8-126">Bunlar hello "Sonraki adımlar" bölümüne ayrıntılı hello EventSource sağlayıcılardan görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="449f8-126">You can view these from hello EventSource providers detailed in hello "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="449f8-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="449f8-127">Next steps</span></span>
<span data-ttu-id="449f8-128">Service Fabric tarafından sağlanan mevcut Tanılama hakkında daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="449f8-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="449f8-129">Güvenilir aktörler tanılama</span><span class="sxs-lookup"><span data-stu-id="449f8-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="449f8-130">Güvenilir hizmetler tanılama</span><span class="sxs-lookup"><span data-stu-id="449f8-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

