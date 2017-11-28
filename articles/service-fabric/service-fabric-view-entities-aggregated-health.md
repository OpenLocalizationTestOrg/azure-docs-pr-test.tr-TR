---
title: "aaaHow tooview Azure Service Fabric varlıkları toplanan sistem durumu | Microsoft Docs"
description: "Nasıl tooquery, görüntülemek ve sistem durumu sorgularının ve genel sorgular aracılığıyla Azure Service Fabric varlıkları toplanan Sistem Değerlendirme açıklar."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="0860c-103">Service Fabric sistem durumu raporlarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="0860c-103">View Service Fabric health reports</span></span>
<span data-ttu-id="0860c-104">Azure Service Fabric tanıtır bir [sistem durumu modeli](service-fabric-health-introduction.md) hangi sistem bileşenleri ve watchdogs yerel koşulları rapor için sistem durumu varlıkları ile bunların izlemekte olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="0860c-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="0860c-105">Merhaba [sistem durumu deposu](service-fabric-health-introduction.md#health-store) varlıklar sağlıklı olup tüm sistem durumu verileri toodetermine toplar.</span><span class="sxs-lookup"><span data-stu-id="0860c-105">hello [health store](service-fabric-health-introduction.md#health-store) aggregates all health data toodetermine whether entities are healthy.</span></span>

<span data-ttu-id="0860c-106">Merhaba küme hello sistem bileşenleri tarafından gönderilen sistem durumu raporları ile birlikte otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="0860c-106">hello cluster is automatically populated with health reports sent by hello system components.</span></span> <span data-ttu-id="0860c-107">Ayrıntılı bilgi için [kullanım sistem durumu raporları tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="0860c-107">Read more at [Use system health reports tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="0860c-108">Service Fabric birden çok yol tooget toplanan hello durumunu hello varlıklar sağlar:</span><span class="sxs-lookup"><span data-stu-id="0860c-108">Service Fabric provides multiple ways tooget hello aggregated health of hello entities:</span></span>

* <span data-ttu-id="0860c-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) veya diğer görsel Araçlar</span><span class="sxs-lookup"><span data-stu-id="0860c-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="0860c-110">Sistem durumu sorgularının (aracılığıyla, PowerShell, API veya REST)</span><span class="sxs-lookup"><span data-stu-id="0860c-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="0860c-111">Genel sistem durumu (aracılığıyla, PowerShell, API veya REST) hello özelliklerinden biri olarak varlıklar, bu dönüş listesini sorgular</span><span class="sxs-lookup"><span data-stu-id="0860c-111">General queries that return a list of entities that have health as one of hello properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="0860c-112">Şimdi bu seçenekleri toodemonstrate beş düğümler ve hello yerel bir küme kullanın [fabric: / WordCount uygulamasını](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="0860c-112">toodemonstrate these options, let's use a local cluster with five nodes and hello [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="0860c-113">Merhaba **fabric: / WordCount** iki varsayılan hizmet, bir durum bilgisi olan hizmet türü içeren uygulama `WordCountServiceType`ve durum bilgisiz hizmet türü `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="0860c-113">hello **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="0860c-114">Merhaba değiştirilen `ApplicationManifest.xml` toorequire yedi hedef çoğaltmaları hello durum bilgisi olan hizmet ve bir bölüm.</span><span class="sxs-lookup"><span data-stu-id="0860c-114">I changed hello `ApplicationManifest.xml` toorequire seven target replicas for hello stateful service and one partition.</span></span> <span data-ttu-id="0860c-115">Merhaba kümede yalnızca beş düğüm olduğundan hello sistem bileşenleri hello hizmet bölüme bir uyarı hello hedef sayısı olduğundan bildirin.</span><span class="sxs-lookup"><span data-stu-id="0860c-115">Because there are only five nodes in hello cluster, hello system components report a warning on hello service partition because it is below hello target count.</span></span>

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="0860c-116">Service Fabric Explorer'da sistem durumu</span><span class="sxs-lookup"><span data-stu-id="0860c-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="0860c-117">Service Fabric Explorer hello küme görsel görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="0860c-117">Service Fabric Explorer provides a visual view of hello cluster.</span></span> <span data-ttu-id="0860c-118">Merhaba resimde, görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0860c-118">In hello image below, you can see that:</span></span>

* <span data-ttu-id="0860c-119">Merhaba uygulama **fabric: / WordCount** tarafından raporlanan bir hata olayı olduğundan (hata) kırmızıdır **MyWatchdog** hello özelliği için **kullanılabilirlik**.</span><span class="sxs-lookup"><span data-stu-id="0860c-119">hello application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for hello property **Availability**.</span></span>
* <span data-ttu-id="0860c-120">Kendi hizmetlerden biri **fabric: / WordCount/WordCountService** sarı (uyarı).</span><span class="sxs-lookup"><span data-stu-id="0860c-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="0860c-121">Merhaba hizmet yedi yinelemelerle yapılandırılır ve iki repicas yerleştirilemez şekilde hello kümesinin beş düğümü vardır.</span><span class="sxs-lookup"><span data-stu-id="0860c-121">hello service is configured with seven replicas and hello cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="0860c-122">Burada gösterilmese hello hizmeti sistem rapordan nedeniyle sarı bölümdür `System.FM` olduğunu belirten `Partition is below target replica or instance count`.</span><span class="sxs-lookup"><span data-stu-id="0860c-122">Although it's not shown here, hello service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="0860c-123">Merhaba sarı bölüm Tetikleyicileri sarı hizmet hello.</span><span class="sxs-lookup"><span data-stu-id="0860c-123">hello yellow partition triggers hello yellow service.</span></span>
* <span data-ttu-id="0860c-124">Merhaba küme hello kırmızı nedeniyle kırmızı uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="0860c-124">hello cluster is red because of hello red application.</span></span>

<span data-ttu-id="0860c-125">Merhaba değerlendirme varsayılan ilkelerden hello küme bildirimi ve uygulama bildirimi kullanır.</span><span class="sxs-lookup"><span data-stu-id="0860c-125">hello evaluation uses default policies from hello cluster manifest and application manifest.</span></span> <span data-ttu-id="0860c-126">Bunlar, katı ilkeleri ve herhangi bir hata tolerans değil.</span><span class="sxs-lookup"><span data-stu-id="0860c-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="0860c-127">Service Fabric Explorer ile Merhaba küme görünümü:</span><span class="sxs-lookup"><span data-stu-id="0860c-127">View of hello cluster with Service Fabric Explorer:</span></span>

![Service Fabric Explorer ile Merhaba küme görüntüleyin.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="0860c-129">Daha fazla bilgi edinin [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="0860c-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="0860c-130">Sistem durumu sorgularının sayısı</span><span class="sxs-lookup"><span data-stu-id="0860c-130">Health queries</span></span>
<span data-ttu-id="0860c-131">Service Fabric her desteklenen hello için sistem durumu sorgularının sunan [varlık türleri](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="0860c-131">Service Fabric exposes health queries for each of hello supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="0860c-132">Merhaba yöntemleri kullanarak API aracılığıyla erişilebilir [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlet'leri ve REST.</span><span class="sxs-lookup"><span data-stu-id="0860c-132">They can be accessed through hello API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="0860c-133">Bu sorguları hello varlık tüm sistem bilgilerini döndürür: hello toplanan sistem durumu, varlık sistem durumu olayları, alt sistem durumlarını (varsa), (Merhaba varlık sağlıklı olmadığında) sağlıksız değerlendirmeleri ve alt sistem durumu istatistikleri (zaman uygulanabilir).</span><span class="sxs-lookup"><span data-stu-id="0860c-133">These queries return complete health information about hello entity: hello aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when hello entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="0860c-134">Merhaba health store içinde tam olarak doldurulan bir sistem durumu varlık döndürülür.</span><span class="sxs-lookup"><span data-stu-id="0860c-134">A health entity is returned when it is fully populated in hello health store.</span></span> <span data-ttu-id="0860c-135">Merhaba varlık (silinmez) etkin ve sistem raporu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0860c-135">hello entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="0860c-136">Merhaba hiyerarşi zinciri kendi üst varlıklarını ayrıca sistem raporları sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0860c-136">Its parent entities on hello hierarchy chain must also have system reports.</span></span> <span data-ttu-id="0860c-137">Bu koşulların herhangi biri değil sağlanırsa, hello durumu return sorgular bir [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) ile [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` gösterir neden hello varlık alınmadı.</span><span class="sxs-lookup"><span data-stu-id="0860c-137">If any of these conditions are not satisfied, hello health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why hello entity is not returned.</span></span>
>
>

<span data-ttu-id="0860c-138">Merhaba sistem durumu sorgularının hello varlık türüne bağlıdır hello varlık tanımlayıcısı geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0860c-138">hello health queries must pass in hello entity identifier, which depends on hello entity type.</span></span> <span data-ttu-id="0860c-139">Merhaba sorguları isteğe bağlı sistem durumu ilkesi parametreleri kabul eder.</span><span class="sxs-lookup"><span data-stu-id="0860c-139">hello queries accept optional health policy parameters.</span></span> <span data-ttu-id="0860c-140">Sistem durumu ilkeleri belirtilirse, hello [sistem durumu ilkeleri](service-fabric-health-introduction.md#health-policies) hello küme veya uygulama bildirimden değerlendirmesi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0860c-140">If no health policies are specified, hello [health policies](service-fabric-health-introduction.md#health-policies) from hello cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="0860c-141">Sistem durumu ilkeleri için bir tanım Hello bildirimleri içermiyorsa, hello varsayılan sistem durumu ilkeleri değerlendirme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0860c-141">If hello manifests don't contain a definition for health policies, hello default health policies are used for evaluation.</span></span> <span data-ttu-id="0860c-142">Merhaba varsayılan sistem durumu ilkeleri hataları tolerans değil.</span><span class="sxs-lookup"><span data-stu-id="0860c-142">hello default health policies do not tolerate any failures.</span></span> <span data-ttu-id="0860c-143">Merhaba sorgular yalnızca kısmi alt döndürmek için filtreler de kabul veya belirtilen filtreler saygı olayları--hello olanları hello.</span><span class="sxs-lookup"><span data-stu-id="0860c-143">hello queries also accept filters for returning only partial children or events--hello ones that respect hello specified filters.</span></span> <span data-ttu-id="0860c-144">Başka bir filtre hello alt istatistikleri hariç izin verir.</span><span class="sxs-lookup"><span data-stu-id="0860c-144">Another filter allows excluding hello children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="0860c-145">Merhaba ileti yanıt boyutu azaltılmış şekilde hello çıkış filtreleri hello sunucu tarafında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="0860c-145">hello output filters are applied on hello server side, so hello message reply size is reduced.</span></span> <span data-ttu-id="0860c-146">Toolimit hello veri döndürülen yerine filtreleri hello istemci tarafında uygulama hello çıkış filtreleri kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="0860c-146">We recommended that you use hello output filters toolimit hello data returned, rather than apply filters on hello client side.</span></span>
>
>

<span data-ttu-id="0860c-147">Bir varlığın durumu içerir:</span><span class="sxs-lookup"><span data-stu-id="0860c-147">An entity's health contains:</span></span>

* <span data-ttu-id="0860c-148">Merhaba hello varlık sistem durumu birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="0860c-148">hello aggregated health state of hello entity.</span></span> <span data-ttu-id="0860c-149">Varlık sistem durumu raporları, alt sistem durumlarını (varsa) ve sistem durumu ilkeleri göre hello sistem durumu depoya göre hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="0860c-149">Computed by hello health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="0860c-150">Daha fazla bilgi edinin [varlık sistem durumu değerlendirmesi](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="0860c-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="0860c-151">Sistem durumu olayları hello varlıkta hello.</span><span class="sxs-lookup"><span data-stu-id="0860c-151">hello health events on hello entity.</span></span>
* <span data-ttu-id="0860c-152">alt bulunabilir hello varlıklar için tüm alt sistem durumlarının Hello koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="0860c-152">hello collection of health states of all children for hello entities that can have children.</span></span> <span data-ttu-id="0860c-153">Merhaba sistem durumlarını ve toplanan sistem durumu hello varlık tanımlayıcıları içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-153">hello health states contain entity identifiers and hello aggregated health state.</span></span> <span data-ttu-id="0860c-154">tooget tüm sistem için bir alt hello sorgu durumu hello alt varlık türü için çağırın ve hello alt tanımlayıcıda geçirin.</span><span class="sxs-lookup"><span data-stu-id="0860c-154">tooget complete health for a child, call hello query health for hello child entity type and pass in hello child identifier.</span></span>
* <span data-ttu-id="0860c-155">Hello varlık sağlam değilse bu noktası toohello rapor hello sağlıksız değerlendirmeleri hello varlığın hello durum tetikledi.</span><span class="sxs-lookup"><span data-stu-id="0860c-155">hello unhealthy evaluations that point toohello report that triggered hello state of hello entity, if hello entity is not healthy.</span></span> <span data-ttu-id="0860c-156">Merhaba değerlendirmeleri özyinelemeli, geçerli sistem durumu tetiklenen hello alt sistem durumu değerlendirmesini içeren ' dir.</span><span class="sxs-lookup"><span data-stu-id="0860c-156">hello evaluations are recursive, containing hello children health evaluations that triggered current health state.</span></span> <span data-ttu-id="0860c-157">Örneğin, bir izleme bir çoğaltma karşı bir hata bildirdi.</span><span class="sxs-lookup"><span data-stu-id="0860c-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="0860c-158">Merhaba uygulama sistem tooan sağlıksız hizmet nedeniyle sağlıksız bir değerlendirme gösterir; Merhaba hizmettir tooa bölümünde hata nedeniyle sağlıksız; Merhaba bölümdür tooa çoğaltma hatası nedeniyle sağlıksız; Merhaba çoğaltma toohello izleme hata sistem durumu raporu sağlam değil.</span><span class="sxs-lookup"><span data-stu-id="0860c-158">hello application health shows an unhealthy evaluation due tooan unhealthy service; hello service is unhealthy due tooa partition in error; hello partition is unhealthy due tooa replica in error; hello replica is unhealthy due toohello watchdog error health report.</span></span>
* <span data-ttu-id="0860c-159">alt hello varlıklar tüm alt türleri için Hello sistem durumu istatistikleri.</span><span class="sxs-lookup"><span data-stu-id="0860c-159">hello health statistics for all children types of hello entities that have children.</span></span> <span data-ttu-id="0860c-160">Örneğin, küme durumu uygulamalar, hizmetler, bölümler, çoğaltmaları toplam sayısını hello gösterir ve varlıkları hello kümedeki dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="0860c-160">For example, cluster health shows hello total number of applications, services, partitions, replicas, and deployed entities in hello cluster.</span></span> <span data-ttu-id="0860c-161">Hizmet çoğaltmaları hello altında belirtilen ve hello toplam bölüm sayısı hizmetin sistem durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="0860c-161">Service health shows hello total number of partitions and replicas under hello specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="0860c-162">Küme durumu Al</span><span class="sxs-lookup"><span data-stu-id="0860c-162">Get cluster health</span></span>
<span data-ttu-id="0860c-163">Döndürür hello küme varlık durumunu hello ve uygulamaların ve düğümler (Merhaba Küme alt) hello sistem durumlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-163">Returns hello health of hello cluster entity and contains hello health states of applications and nodes (children of hello cluster).</span></span> <span data-ttu-id="0860c-164">Giriş:</span><span class="sxs-lookup"><span data-stu-id="0860c-164">Input:</span></span>

* <span data-ttu-id="0860c-165">[İsteğe bağlı] hello küme sistem durumu ilkesi tooevaluate hello düğümler ve hello küme olayları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0860c-165">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="0860c-166">[İsteğe bağlı] hello uygulama sistem durumu ilkesi Eşlem ' hello sistem durumu ilkeleri ile toooverride hello uygulama bildirim ilkeleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0860c-166">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="0860c-167">[İsteğe bağlı] Olaylar, düğümleri ve hangi girişlerin belirtin uygulamaları filtreler ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="0860c-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="0860c-168">Tüm olayları, düğümleri ve uygulamaları hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="0860c-168">All events, nodes, and applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="0860c-169">[İsteğe bağlı] Tooexclude sağlık istatistikleri filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="0860c-169">[Optional] Filter tooexclude health statistics.</span></span>
* <span data-ttu-id="0860c-170">[İsteğe bağlı] Filtre tooinclude fabric: / sistem durumu istatistiklerine hello sağlık istatistikleri.</span><span class="sxs-lookup"><span data-stu-id="0860c-170">[Optional] Filter tooinclude fabric:/System health statistics in hello health statistics.</span></span> <span data-ttu-id="0860c-171">Yalnızca hello sağlık istatistikleri değil çıkarıldığında geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0860c-171">Only applicable when hello health statistics are not excluded.</span></span> <span data-ttu-id="0860c-172">Varsayılan olarak, hello sistem durumu İstatistikler yalnızca kullanıcı uygulamaları ve hello sistem uygulaması için istatistikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-172">By default, hello health statistics include only statistics for user applications and not hello System application.</span></span>

### <a name="api"></a><span data-ttu-id="0860c-173">API</span><span class="sxs-lookup"><span data-stu-id="0860c-173">API</span></span>
<span data-ttu-id="0860c-174">tooget küme sistem durumu, oluşturma bir `FabricClient` ve çağrı hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) yöntemi kendi **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="0860c-174">tooget cluster health, create a `FabricClient` and call hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="0860c-175">Merhaba aşağıdaki çağrıyı hello küme durumu alır:</span><span class="sxs-lookup"><span data-stu-id="0860c-175">hello following call gets hello cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="0860c-176">Merhaba aşağıdaki kodu hello küme durumu bir özel küme sistem durumu ilkesi kullanarak alır ve düğümler ve uygulamalar için filtreler.</span><span class="sxs-lookup"><span data-stu-id="0860c-176">hello following code gets hello cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="0860c-177">Merhaba sağlık istatistikleri hello doku içerdiğini belirtir: / Sistem istatistikleri.</span><span class="sxs-lookup"><span data-stu-id="0860c-177">It specifies that hello health statistics include hello fabric:/System statistics.</span></span> <span data-ttu-id="0860c-178">Oluşturduğu [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), hello giriş bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains hello input information.</span></span>

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="0860c-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0860c-179">PowerShell</span></span>
<span data-ttu-id="0860c-180">Merhaba cmdlet tooget hello küme durumu [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="0860c-180">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="0860c-181">İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0860c-181">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="0860c-182">Merhaba hello küme beş düğümü, hello sistem uygulaması ve doku durumda: / WordCount açıklandığı şekilde yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="0860c-182">hello state of hello cluster is five nodes, hello system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="0860c-183">cmdlet aşağıdaki Merhaba, varsayılan sistem durumu ilkeleri kullanarak küme durumu alır.</span><span class="sxs-lookup"><span data-stu-id="0860c-183">hello following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="0860c-184">Merhaba toplanmış uyarı sistem durumu, çünkü hello fabric: / WordCount uygulamasını uyarı.</span><span class="sxs-lookup"><span data-stu-id="0860c-184">hello aggregated health state is warning, because hello fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="0860c-185">Merhaba sağlıksız değerlendirmeleri Ayrıntıları toplanan hello durumu tetikleyen hello koşullara nasıl sağladığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0860c-185">Note how hello unhealthy evaluations provide details on hello conditions that triggered hello aggregated health.</span></span>

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

<span data-ttu-id="0860c-186">Merhaba aşağıdaki PowerShell cmdlet'ini hello küme hello durumunu özel uygulama İlkesi kullanarak alır.</span><span class="sxs-lookup"><span data-stu-id="0860c-186">hello following PowerShell cmdlet gets hello health of hello cluster by using a custom application policy.</span></span> <span data-ttu-id="0860c-187">Sonuçları tooget yalnızca uygulamalar ve hata veya uyarı düğümler filtreler.</span><span class="sxs-lookup"><span data-stu-id="0860c-187">It filters results tooget only applications and nodes in error or warning.</span></span> <span data-ttu-id="0860c-188">Tüm sağlıklı olarak sonuç olarak, düğüm, döndürülür.</span><span class="sxs-lookup"><span data-stu-id="0860c-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="0860c-189">Yalnızca doku hello: / WordCount uygulamasını hello uygulamaları filtre dikkate alır.</span><span class="sxs-lookup"><span data-stu-id="0860c-189">Only hello fabric:/WordCount application respects hello applications filter.</span></span> <span data-ttu-id="0860c-190">Merhaba özel ilke hello doku için hata olarak tooconsider uyarıları belirttiğinden: / WordCount uygulama hello hata olduğu gibi değerlendirilir ve bu nedenle hello kümedir.</span><span class="sxs-lookup"><span data-stu-id="0860c-190">Because hello custom policy specifies tooconsider warnings as errors for hello fabric:/WordCount application, hello application is evaluated as in error, and so is hello cluster.</span></span>

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a><span data-ttu-id="0860c-191">REST</span><span class="sxs-lookup"><span data-stu-id="0860c-191">REST</span></span>
<span data-ttu-id="0860c-192">Küme durumu ile alabilirsiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) veya [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="0860c-193">Düğüm durumu Al</span><span class="sxs-lookup"><span data-stu-id="0860c-193">Get node health</span></span>
<span data-ttu-id="0860c-194">Döndürür, bir düğüm varlık durumunu hello ve hello düğümde bildirilen hello sistem durumu olayları içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-194">Returns hello health of a node entity and contains hello health events reported on hello node.</span></span> <span data-ttu-id="0860c-195">Giriş:</span><span class="sxs-lookup"><span data-stu-id="0860c-195">Input:</span></span>

* <span data-ttu-id="0860c-196">Merhaba düğümü tanımlar [gerekli] hello düğüm adı.</span><span class="sxs-lookup"><span data-stu-id="0860c-196">[Required] hello node name that identifies hello node.</span></span>
* <span data-ttu-id="0860c-197">[İsteğe bağlı] hello küme sistem durumu ilkesi ayarlarını tooevaluate sistem durumu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0860c-197">[Optional] hello cluster health policy settings used tooevaluate health.</span></span>
* <span data-ttu-id="0860c-198">[İsteğe bağlı] Hangi girişlerin belirten olaylar için filtreleri ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="0860c-198">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="0860c-199">Tüm olaylar hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0860c-199">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="0860c-200">API</span><span class="sxs-lookup"><span data-stu-id="0860c-200">API</span></span>
<span data-ttu-id="0860c-201">tooget düğüm durumu hello API aracılığıyla oluşturma bir `FabricClient` ve çağrı hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) kendi HealthManager yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0860c-201">tooget node health through hello API, create a `FabricClient` and call hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="0860c-202">Merhaba aşağıdaki kodu hello düğüm durumu hello belirtilen düğüm adı alır:</span><span class="sxs-lookup"><span data-stu-id="0860c-202">hello following code gets hello node health for hello specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="0860c-203">Merhaba olayları filtresi ve özel İlkesi aracılığıyla düğüm adı ve geçişleri belirtilen için hello aşağıdaki kodu hello düğüm durumu alır [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="0860c-203">hello following code gets hello node health for hello specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="0860c-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0860c-204">PowerShell</span></span>
<span data-ttu-id="0860c-205">Merhaba cmdlet tooget hello düğüm durumu [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="0860c-205">hello cmdlet tooget hello node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="0860c-206">İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0860c-206">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="0860c-207">cmdlet aşağıdaki Merhaba, varsayılan sistem durumu ilkeleri kullanarak hello düğüm durumu alır:</span><span class="sxs-lookup"><span data-stu-id="0860c-207">hello following cmdlet gets hello node health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="0860c-208">Merhaba aşağıdaki cmdlet'i hello tüm düğümlerinin sistem durumunu hello kümede alır:</span><span class="sxs-lookup"><span data-stu-id="0860c-208">hello following cmdlet gets hello health of all nodes in hello cluster:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a><span data-ttu-id="0860c-209">REST</span><span class="sxs-lookup"><span data-stu-id="0860c-209">REST</span></span>
<span data-ttu-id="0860c-210">Düğüm durumu ile alabileceğiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) veya bir [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="0860c-211">Uygulama durumunu Al</span><span class="sxs-lookup"><span data-stu-id="0860c-211">Get application health</span></span>
<span data-ttu-id="0860c-212">Bir uygulama varlığı hello durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-212">Returns hello health of an application entity.</span></span> <span data-ttu-id="0860c-213">Dağıtılan hello uygulama ve hizmet öğelerini hello sistem durumlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-213">It contains hello health states of hello deployed application and service children.</span></span> <span data-ttu-id="0860c-214">Giriş:</span><span class="sxs-lookup"><span data-stu-id="0860c-214">Input:</span></span>

* <span data-ttu-id="0860c-215">Merhaba uygulaması tanımlayan [gerekli] hello uygulama adı (URI).</span><span class="sxs-lookup"><span data-stu-id="0860c-215">[Required] hello application name (URI) that identifies hello application.</span></span>
* <span data-ttu-id="0860c-216">[İsteğe bağlı] hello uygulama durumu ilkesi toooverride hello uygulama bildirim ilkeleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0860c-216">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="0860c-217">[İsteğe bağlı] Olaylar, hizmetler ve hangi girişlerin belirtin dağıtılan uygulamalar için filtreleri ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="0860c-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="0860c-218">Tüm olaylar, hizmetler ve dağıtılan uygulamalar hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu var.</span><span class="sxs-lookup"><span data-stu-id="0860c-218">All events, services, and deployed applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="0860c-219">[İsteğe bağlı] Tooexclude hello sağlık istatistikleri filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="0860c-219">[Optional] Filter tooexclude hello health statistics.</span></span> <span data-ttu-id="0860c-220">Belirtilmezse, hello sistem durumu istatistikleri hello Tamam, uyarı ve hata sayısı için tüm uygulama alt öğeleri içerir: Hizmetler, bölümler, çoğaltmalar, dağıtılan uygulamalar ve hizmet paketleri dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="0860c-220">If not specified, hello health statistics include hello ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="0860c-221">API</span><span class="sxs-lookup"><span data-stu-id="0860c-221">API</span></span>
<span data-ttu-id="0860c-222">tooget uygulama sistem oluşturma bir `FabricClient` ve çağrı hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) kendi HealthManager yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0860c-222">tooget application health, create a `FabricClient` and call hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="0860c-223">Merhaba aşağıdaki kodu hello uygulama sağlığını hello belirtilen uygulama adı (URI) alır:</span><span class="sxs-lookup"><span data-stu-id="0860c-223">hello following code gets hello application health for hello specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="0860c-224">Merhaba aşağıdaki kodu hello uygulama sağlığını hello belirtilen uygulama adı (URI) için filtrelerle alır ve özel ilkelerinde belirtilen aracılığıyla [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="0860c-224">hello following code gets hello application health for hello specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="0860c-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0860c-225">PowerShell</span></span>
<span data-ttu-id="0860c-226">Merhaba cmdlet tooget hello uygulama durumu [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="0860c-226">hello cmdlet tooget hello application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="0860c-227">İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0860c-227">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="0860c-228">Merhaba aşağıdaki cmdlet'i döndürür hello hello durumunu **fabric: / WordCount** uygulama:</span><span class="sxs-lookup"><span data-stu-id="0860c-228">hello following cmdlet returns hello health of hello **fabric:/WordCount** application:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

<span data-ttu-id="0860c-229">PowerShell cmdlet özel ilkeler geçişte aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="0860c-229">hello following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="0860c-230">Ayrıca, alt ve olayları filtreler.</span><span class="sxs-lookup"><span data-stu-id="0860c-230">It also filters children and events.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a><span data-ttu-id="0860c-231">REST</span><span class="sxs-lookup"><span data-stu-id="0860c-231">REST</span></span>
<span data-ttu-id="0860c-232">Uygulama health ile alabilirsiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) veya [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="0860c-233">Hizmet durumunu Al</span><span class="sxs-lookup"><span data-stu-id="0860c-233">Get service health</span></span>
<span data-ttu-id="0860c-234">Bir hizmet varlığı hello durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-234">Returns hello health of a service entity.</span></span> <span data-ttu-id="0860c-235">Merhaba bölüm sistem durumlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-235">It contains hello partition health states.</span></span> <span data-ttu-id="0860c-236">Giriş:</span><span class="sxs-lookup"><span data-stu-id="0860c-236">Input:</span></span>

* <span data-ttu-id="0860c-237">Merhaba hizmet tanımlayan [gerekli] hello hizmet adı (URI).</span><span class="sxs-lookup"><span data-stu-id="0860c-237">[Required] hello service name (URI) that identifies hello service.</span></span>
* <span data-ttu-id="0860c-238">[İsteğe bağlı] hello uygulama durumu ilkesi toooverride hello uygulama bildirim İlkesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0860c-238">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="0860c-239">[İsteğe bağlı] Olayları ve hangi girişlerin belirtmek bölümleri için filtreleri ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="0860c-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="0860c-240">Tüm olayları ve bölümleri hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="0860c-240">All events and partitions are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="0860c-241">[İsteğe bağlı] Tooexclude sağlık istatistikleri filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="0860c-241">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="0860c-242">Belirtilmezse, sistem durumu istatistikleri göster hello Tamam Merhaba, tüm bölümler ve çoğaltmalar Merhaba hizmetinin uyarı ve hata sayısı.</span><span class="sxs-lookup"><span data-stu-id="0860c-242">If not specified, hello health statistics show hello ok, warning, and error count for all partitions and replicas of hello service.</span></span>

### <a name="api"></a><span data-ttu-id="0860c-243">API</span><span class="sxs-lookup"><span data-stu-id="0860c-243">API</span></span>
<span data-ttu-id="0860c-244">tooget hizmet durumu hello API aracılığıyla oluşturma bir `FabricClient` ve çağrı hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) kendi HealthManager yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0860c-244">tooget service health through hello API, create a `FabricClient` and call hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="0860c-245">Merhaba aşağıda belirtilen hizmet adı (URI) hizmetiyle hello durumunu alır:</span><span class="sxs-lookup"><span data-stu-id="0860c-245">hello following example gets hello health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="0860c-246">Merhaba aşağıdaki kodu alır hello hizmet durumu hello belirtilen hizmet adı (URI), filtreleri ve özel ilke aracılığıyla belirtme [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="0860c-246">hello following code gets hello service health for hello specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="0860c-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0860c-247">PowerShell</span></span>
<span data-ttu-id="0860c-248">Merhaba cmdlet tooget hello hizmet durumu [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="0860c-248">hello cmdlet tooget hello service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="0860c-249">İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0860c-249">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="0860c-250">cmdlet aşağıdaki Merhaba, varsayılan sistem durumu ilkeleri kullanarak hello hizmet durumu alır:</span><span class="sxs-lookup"><span data-stu-id="0860c-250">hello following cmdlet gets hello service health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="0860c-251">REST</span><span class="sxs-lookup"><span data-stu-id="0860c-251">REST</span></span>
<span data-ttu-id="0860c-252">Hizmet durumu ile alabileceğiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) veya bir [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="0860c-253">Bölüm durumu Al</span><span class="sxs-lookup"><span data-stu-id="0860c-253">Get partition health</span></span>
<span data-ttu-id="0860c-254">Bir bölüm varlık hello durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-254">Returns hello health of a partition entity.</span></span> <span data-ttu-id="0860c-255">Merhaba çoğaltma sistem durumlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-255">It contains hello replica health states.</span></span> <span data-ttu-id="0860c-256">Giriş:</span><span class="sxs-lookup"><span data-stu-id="0860c-256">Input:</span></span>

* <span data-ttu-id="0860c-257">[Gerekli] hello bölüm hello bölüm tanımlayan kimlik (GUID).</span><span class="sxs-lookup"><span data-stu-id="0860c-257">[Required] hello partition ID (GUID) that identifies hello partition.</span></span>
* <span data-ttu-id="0860c-258">[İsteğe bağlı] hello uygulama durumu ilkesi toooverride hello uygulama bildirim İlkesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0860c-258">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="0860c-259">[İsteğe bağlı] Olayları ve hangi girişlerin belirtin çoğaltmaları için filtreleri ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="0860c-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="0860c-260">Tüm olayları ve çoğaltmaları hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="0860c-260">All events and replicas are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="0860c-261">[İsteğe bağlı] Tooexclude sağlık istatistikleri filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="0860c-261">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="0860c-262">Belirtilmezse, kaç tane çoğaltmaları Tamam, uyarı ve hata durumlarıdır hello sistem durumu istatistiklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="0860c-262">If not specified, hello health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="0860c-263">API</span><span class="sxs-lookup"><span data-stu-id="0860c-263">API</span></span>
<span data-ttu-id="0860c-264">tooget bölüm durumu hello API aracılığıyla oluşturma bir `FabricClient` ve çağrı hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) kendi HealthManager yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0860c-264">tooget partition health through hello API, create a `FabricClient` and call hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="0860c-265">toospecify isteğe bağlı parametreleri, [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="0860c-265">toospecify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="0860c-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0860c-266">PowerShell</span></span>
<span data-ttu-id="0860c-267">Merhaba cmdlet tooget hello bölüm durumu [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="0860c-267">hello cmdlet tooget hello partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="0860c-268">İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0860c-268">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="0860c-269">Hello aşağıdaki cmdlet'i alır hello tüm bölümleri için hello sistem durumu **fabric: / WordCount/WordCountService** hizmeti ve filtreleri çoğaltma sistem durumlarını çıkışı:</span><span class="sxs-lookup"><span data-stu-id="0860c-269">hello following cmdlet gets hello health for all partitions of hello **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="0860c-270">REST</span><span class="sxs-lookup"><span data-stu-id="0860c-270">REST</span></span>
<span data-ttu-id="0860c-271">Bölüm health ile alabileceğiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) veya bir [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="0860c-272">Çoğaltma durumu Al</span><span class="sxs-lookup"><span data-stu-id="0860c-272">Get replica health</span></span>
<span data-ttu-id="0860c-273">Bir durum bilgisi olan hizmet çoğaltmayı veya bir durum bilgisiz hizmet örneği Hello durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-273">Returns hello health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="0860c-274">Giriş:</span><span class="sxs-lookup"><span data-stu-id="0860c-274">Input:</span></span>

* <span data-ttu-id="0860c-275">Merhaba çoğaltma tanımlayan [gerekli] hello bölüm kimlik (GUID) ve çoğaltma kimliği.</span><span class="sxs-lookup"><span data-stu-id="0860c-275">[Required] hello partition ID (GUID) and replica ID that identifies hello replica.</span></span>
* <span data-ttu-id="0860c-276">[İsteğe bağlı] hello uygulama sistem durumu ilkesi parametreleri toooverride hello uygulama bildirim ilkeleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0860c-276">[Optional] hello application health policy parameters used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="0860c-277">[İsteğe bağlı] Hangi girişlerin belirten olaylar için filtreleri ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="0860c-277">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="0860c-278">Tüm olaylar hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0860c-278">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="0860c-279">API</span><span class="sxs-lookup"><span data-stu-id="0860c-279">API</span></span>
<span data-ttu-id="0860c-280">tooget hello çoğaltma durumu hello API aracılığıyla oluşturma bir `FabricClient` ve çağrı hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) kendi HealthManager yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0860c-280">tooget hello replica health through hello API, create a `FabricClient` and call hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="0860c-281">Gelişmiş parametrelerini, kullanım toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="0860c-281">toospecify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="0860c-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0860c-282">PowerShell</span></span>
<span data-ttu-id="0860c-283">Merhaba cmdlet tooget hello çoğaltma durumu [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="0860c-283">hello cmdlet tooget hello replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="0860c-284">İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0860c-284">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="0860c-285">Merhaba aşağıdaki cmdlet'i hello birincil çoğaltma hello hizmetinin tüm bölümler için başlangıç durumunu alır:</span><span class="sxs-lookup"><span data-stu-id="0860c-285">hello following cmdlet gets hello health of hello primary replica for all partitions of hello service:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="0860c-286">REST</span><span class="sxs-lookup"><span data-stu-id="0860c-286">REST</span></span>
<span data-ttu-id="0860c-287">Çoğaltma sistem durumu ile alabileceğiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) veya bir [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="0860c-288">Dağıtılmış uygulama durumunu Al</span><span class="sxs-lookup"><span data-stu-id="0860c-288">Get deployed application health</span></span>
<span data-ttu-id="0860c-289">Düğümün varlık üzerinde dağıtılmış bir uygulaması hello durumunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-289">Returns hello health of an application deployed on a node entity.</span></span> <span data-ttu-id="0860c-290">Dağıtılan hello hizmet paketi sistem durumlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-290">It contains hello deployed service package health states.</span></span> <span data-ttu-id="0860c-291">Giriş:</span><span class="sxs-lookup"><span data-stu-id="0860c-291">Input:</span></span>

* <span data-ttu-id="0860c-292">Merhaba tanımlamak [gerekli] hello uygulama adı (URI) ve düğüm adı (dize) uygulama dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="0860c-292">[Required] hello application name (URI) and node name (string) that identify hello deployed application.</span></span>
* <span data-ttu-id="0860c-293">[İsteğe bağlı] hello uygulama durumu ilkesi toooverride hello uygulama bildirim ilkeleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0860c-293">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="0860c-294">[İsteğe bağlı] Olayları ve hangi girişlerin belirtin dağıtılmış hizmet paketleri için filtreleri ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="0860c-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="0860c-295">Tüm olayları ve dağıtılmış hizmet paketleri hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="0860c-295">All events and deployed service packages are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="0860c-296">[İsteğe bağlı] Tooexclude sağlık istatistikleri filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="0860c-296">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="0860c-297">Belirtilmezse, hello sağlık istatistikleri Tamam, uyarı ve hata sistem durumlarının dağıtılmış hizmet paketleri hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="0860c-297">If not specified, hello health statistics show hello number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="0860c-298">API</span><span class="sxs-lookup"><span data-stu-id="0860c-298">API</span></span>
<span data-ttu-id="0860c-299">tooget hello durumunu hello API aracılığıyla bir düğümde dağıtılan bir uygulama oluşturmak bir `FabricClient` ve çağrı hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) kendi HealthManager yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0860c-299">tooget hello health of an application deployed on a node through hello API, create a `FabricClient` and call hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="0860c-300">toospecify isteğe bağlı parametreleri, [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="0860c-300">toospecify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="0860c-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0860c-301">PowerShell</span></span>
<span data-ttu-id="0860c-302">Merhaba cmdlet tooget dağıtılan hello uygulama sağlığını olan [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="0860c-302">hello cmdlet tooget hello deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="0860c-303">İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0860c-303">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="0860c-304">uygulamanın dağıtıldığı çıkışı toofind çalıştırmak [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) ve hello bakma dağıtılan uygulama alt.</span><span class="sxs-lookup"><span data-stu-id="0860c-304">toofind out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed application children.</span></span>

<span data-ttu-id="0860c-305">Merhaba aşağıdaki cmdlet'i alır hello hello durumunu **fabric: / WordCount** dağıtılan uygulama **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="0860c-305">hello following cmdlet gets hello health of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="0860c-306">REST</span><span class="sxs-lookup"><span data-stu-id="0860c-306">REST</span></span>
<span data-ttu-id="0860c-307">Dağıtılmış uygulama sistem durumu ile alabilirsiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) veya [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="0860c-308">Dağıtılan hizmet paketi durumu Al</span><span class="sxs-lookup"><span data-stu-id="0860c-308">Get deployed service package health</span></span>
<span data-ttu-id="0860c-309">Dağıtılan hizmet paketi varlık durumunu döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="0860c-309">Returns hello health of a deployed service package entity.</span></span> <span data-ttu-id="0860c-310">Giriş:</span><span class="sxs-lookup"><span data-stu-id="0860c-310">Input:</span></span>

* <span data-ttu-id="0860c-311">[Gerekli] hello uygulama adı (URI), düğüm adı (dize) ve hizmet bildirim adı (dize) hello tanımlayan hizmet paketi dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="0860c-311">[Required] hello application name (URI), node name (string), and service manifest name (string) that identify hello deployed service package.</span></span>
* <span data-ttu-id="0860c-312">[İsteğe bağlı] hello uygulama durumu ilkesi toooverride hello uygulama bildirim İlkesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0860c-312">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="0860c-313">[İsteğe bağlı] Hangi girişlerin belirten olaylar için filtreleri ilgilendiğiniz ve hello sonucu (örneğin, yalnızca, hatalar veya uyarılar ve hatalar) döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="0860c-313">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="0860c-314">Tüm olaylar hello filtre bağımsız olarak kullanılan tooevaluate hello toplanan varlık durumu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0860c-314">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="0860c-315">API</span><span class="sxs-lookup"><span data-stu-id="0860c-315">API</span></span>
<span data-ttu-id="0860c-316">Merhaba API aracılığıyla dağıtılan hizmet paketi tooget hello durumunu oluşturmak bir `FabricClient` ve çağrı hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) kendi HealthManager yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0860c-316">tooget hello health of a deployed service package through hello API, create a `FabricClient` and call hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="0860c-317">toospecify isteğe bağlı parametreleri, [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="0860c-317">toospecify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="0860c-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0860c-318">PowerShell</span></span>
<span data-ttu-id="0860c-319">Merhaba cmdlet tooget dağıtılan hello hizmet paketi durumu olan [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="0860c-319">hello cmdlet tooget hello deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="0860c-320">İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0860c-320">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="0860c-321">uygulamanın dağıtıldığı, toosee çalıştırmak [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) ve dağıtılan hello uygulamaları arayın.</span><span class="sxs-lookup"><span data-stu-id="0860c-321">toosee where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed applications.</span></span> <span data-ttu-id="0860c-322">olan hizmet paketleri bir uygulamada arama sırasında hello toosee dağıtılan hizmet paketi alt hello içinde [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) çıktı.</span><span class="sxs-lookup"><span data-stu-id="0860c-322">toosee which service packages are in an application, look at hello deployed service package children in hello [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="0860c-323">Merhaba aşağıdaki cmdlet'i alır hello hello durumunu **WordCountServicePkg** hello hizmet paketi **fabric: / WordCount** dağıtılan uygulama **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="0860c-323">hello following cmdlet gets hello health of hello **WordCountServicePkg** service package of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="0860c-324">Merhaba varlık **System.Hosting** başarılı hizmet paketi ve giriş noktası etkinleştirme ve başarılı hizmet türü kaydı için raporları.</span><span class="sxs-lookup"><span data-stu-id="0860c-324">hello entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="0860c-325">REST</span><span class="sxs-lookup"><span data-stu-id="0860c-325">REST</span></span>
<span data-ttu-id="0860c-326">Dağıtılan hizmet paketi durumu ile alabileceğiniz bir [GET isteğini](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) veya bir [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) hello gövdesinde açıklanan sistem durumu ilkeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="0860c-327">Sistem durumu öbek sorguları</span><span class="sxs-lookup"><span data-stu-id="0860c-327">Health chunk queries</span></span>
<span data-ttu-id="0860c-328">Merhaba sistem durumu öbek sorgular giriş filtreleri başına (yinelemeli olarak), çok düzeyli Küme alt döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="0860c-328">hello health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="0860c-329">Büyük bir esnekliğe hello alt seçerken izin Gelişmiş Filtreler destekleyen toobe döndürdü.</span><span class="sxs-lookup"><span data-stu-id="0860c-329">It supports advanced filters that allow a lot of flexibility in choosing hello children toobe returned.</span></span> <span data-ttu-id="0860c-330">Merhaba filtreler alt hello benzersiz tanımlayıcı veya diğer grup kimlikleri ve/veya sistem durumlarını tarafından belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0860c-330">hello filters can specify children by hello unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="0860c-331">Varsayılan olarak, hiç alt öğe, her zaman birinci düzeydeki alt öğeleri dahil karşılıklı toohealth komutları dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="0860c-331">By default, no children are included, as opposed toohealth commands that always include first-level children.</span></span>

<span data-ttu-id="0860c-332">Merhaba [sistem durumu sorgularının](service-fabric-view-entities-aggregated-health.md#health-queries) hello dönüş yalnızca ilk düzeyi alt belirtilen gerekli filtreleri her varlık.</span><span class="sxs-lookup"><span data-stu-id="0860c-332">hello [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of hello specified entity per required filters.</span></span> <span data-ttu-id="0860c-333">tooget hello alt hello alt ilgi her bir varlık için ek sistem durumu API'leri çağırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0860c-333">tooget hello children of hello children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="0860c-334">Benzer şekilde, belirli varlıkları tooget hello durumunu, istenen her varlık için bir sistem durumu API çağırmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0860c-334">Similarly, tooget hello health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="0860c-335">Merhaba filtreleme Gelişmiş öbek sorgu toorequest sağlar hello ileti boyutu ve iletileri hello sayısını en aza bir sorgu ilgi birden çok öğe.</span><span class="sxs-lookup"><span data-stu-id="0860c-335">hello chunk query advanced filtering allows you toorequest multiple items of interest in one query, minimizing hello message size and hello number of messages.</span></span>

<span data-ttu-id="0860c-336">Merhaba hello öbek sorgu, sistem durumu daha fazla küme varlıklar (gerekli kök dizininde başlayan olası tüm küme varlıklar) için tek çağrıda alabilirsiniz olduğunu değeridir.</span><span class="sxs-lookup"><span data-stu-id="0860c-336">hello value of hello chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="0860c-337">Karmaşık sistem durumu sorgusu gibi ifade edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0860c-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="0860c-338">Dönüş yalnızca uygulamalar hata ve bu uygulamalar için uyarı veya hata tüm hizmetleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="0860c-339">Döndürülen hizmetler için tüm bölümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="0860c-340">Yalnızca hello durumunu adlarıyla belirtilen dört uygulamaları döndür.</span><span class="sxs-lookup"><span data-stu-id="0860c-340">Return only hello health of four applications, specified by their names.</span></span>
* <span data-ttu-id="0860c-341">Yalnızca hello durumunu uygulamaları istenen uygulama türü döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-341">Return only hello health of applications of a desired application type.</span></span>
* <span data-ttu-id="0860c-342">Tüm dağıtılan varlık, bir düğümde döndür.</span><span class="sxs-lookup"><span data-stu-id="0860c-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="0860c-343">Tüm uygulamalar, hello belirtilen düğümdeki tüm dağıtılan uygulamaları ve bu düğümdeki tüm dağıtılan hello hizmet paketleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-343">Returns all applications, all deployed applications on hello specified node and all hello deployed service packages on that node.</span></span>
* <span data-ttu-id="0860c-344">Tüm çoğaltmaları hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-344">Return all replicas in error.</span></span> <span data-ttu-id="0860c-345">Tüm uygulamalar, hizmetler, bölümler ve yalnızca çoğaltmalar hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="0860c-346">Tüm uygulamaları döndür.</span><span class="sxs-lookup"><span data-stu-id="0860c-346">Return all applications.</span></span> <span data-ttu-id="0860c-347">Belirtilen bir hizmeti için tüm bölümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="0860c-348">Şu anda hello sistem durumu öbek sorgu yalnızca hello küme varlık için açıktır.</span><span class="sxs-lookup"><span data-stu-id="0860c-348">Currently, hello health chunk query is exposed only for hello cluster entity.</span></span> <span data-ttu-id="0860c-349">İçeren bir küme durumu öbek döndürür:</span><span class="sxs-lookup"><span data-stu-id="0860c-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="0860c-350">Merhaba küme durumu birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="0860c-350">hello cluster aggregated health state.</span></span>
* <span data-ttu-id="0860c-351">Hello sağlık durumu öbek listesi giriş filtreleri saygı düğümleri.</span><span class="sxs-lookup"><span data-stu-id="0860c-351">hello health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="0860c-352">Hello sağlık durumu öbek giriş filtreleri saygı uygulamaların listesi.</span><span class="sxs-lookup"><span data-stu-id="0860c-352">hello health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="0860c-353">Her uygulama sistem durumu öbek giriş filtreleri ve hello filtreleri saygı tüm dağıtılmış uygulamaları öbek listesiyle saygı tüm hizmetleri ile öbek listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect hello filters.</span></span> <span data-ttu-id="0860c-354">Merhaba alt hizmetler ve dağıtılan uygulamalar için aynı.</span><span class="sxs-lookup"><span data-stu-id="0860c-354">Same for hello children of services and deployed applications.</span></span> <span data-ttu-id="0860c-355">Bu şekilde hello kümedeki tüm varlıklar olası istediyseniz, hiyerarşik bir biçimde döndürülebilir.</span><span class="sxs-lookup"><span data-stu-id="0860c-355">This way, all entities in hello cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="0860c-356">Küme durumu öbek sorgu</span><span class="sxs-lookup"><span data-stu-id="0860c-356">Cluster health chunk query</span></span>
<span data-ttu-id="0860c-357">Döndürür hello küme varlık durumunu hello ve hello hiyerarşik sağlık durumu öbekleri gerekli alt içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-357">Returns hello health of hello cluster entity and contains hello hierarchical health state chunks of required children.</span></span> <span data-ttu-id="0860c-358">Giriş:</span><span class="sxs-lookup"><span data-stu-id="0860c-358">Input:</span></span>

* <span data-ttu-id="0860c-359">[İsteğe bağlı] hello küme sistem durumu ilkesi tooevaluate hello düğümler ve hello küme olayları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0860c-359">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="0860c-360">[İsteğe bağlı] hello uygulama sistem durumu ilkesi Eşlem ' hello sistem durumu ilkeleri ile toooverride hello uygulama bildirim ilkeleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0860c-360">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="0860c-361">[İsteğe bağlı] Düğümler ve hangi girişlerin belirtin uygulamalar için filtreleri ilgilendiğiniz ve hello sonucunda döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="0860c-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in hello result.</span></span> <span data-ttu-id="0860c-362">Merhaba filtreleri belirli tooan varlık/Grup varlıkların veya o düzeyde uygulanabilir tooall varlıklardır.</span><span class="sxs-lookup"><span data-stu-id="0860c-362">hello filters are specific tooan entity/group of entities or are applicable tooall entities at that level.</span></span> <span data-ttu-id="0860c-363">filtrelerin listesi Hello bir genel filtre ve/veya hello sorgu tarafından döndürülen belirli tanımlayıcıları toofine çizgisi varlıklar için filtreleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="0860c-363">hello list of filters can contain one general filter and/or filters for specific identifiers toofine-grain entities returned by hello query.</span></span> <span data-ttu-id="0860c-364">Merhaba alt öğe boş ise, varsayılan olarak döndürülmez.</span><span class="sxs-lookup"><span data-stu-id="0860c-364">If empty, hello children are not returned by default.</span></span>
  <span data-ttu-id="0860c-365">Merhaba filtreler hakkında daha fazla bilgiyi [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) ve [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="0860c-365">Read more about hello filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="0860c-366">Merhaba uygulama filtreleri can yinelemeli çocuklar için Gelişmiş filtreler belirtin.</span><span class="sxs-lookup"><span data-stu-id="0860c-366">hello application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="0860c-367">Merhaba öbek sonuç hello filtreleri saygı hello alt öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-367">hello chunk result includes hello children that respect hello filters.</span></span>

<span data-ttu-id="0860c-368">Şu anda hello öbek sorgu sağlıksız değerlendirmeleri veya varlık olaylarını döndürmüyor.</span><span class="sxs-lookup"><span data-stu-id="0860c-368">Currently, hello chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="0860c-369">Bu ek bilgileri hello var olan küme sistem durumu sorgusu kullanılarak edinilebilir.</span><span class="sxs-lookup"><span data-stu-id="0860c-369">That extra information can be obtained using hello existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="0860c-370">API</span><span class="sxs-lookup"><span data-stu-id="0860c-370">API</span></span>
<span data-ttu-id="0860c-371">tooget küme durumu öbek, oluşturma bir `FabricClient` ve çağrı hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) yöntemi kendi **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="0860c-371">tooget cluster health chunk, create a `FabricClient` and call hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="0860c-372">İçinde geçirebilirsiniz [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe sistem durumu ilkeleri ve Gelişmiş filtreleri.</span><span class="sxs-lookup"><span data-stu-id="0860c-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe health policies and advanced filters.</span></span>

<span data-ttu-id="0860c-373">Merhaba aşağıdaki kodu küme durumu Öbek ile Gelişmiş filtreleri alır.</span><span class="sxs-lookup"><span data-stu-id="0860c-373">hello following code gets cluster health chunk with advanced filters.</span></span>

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="0860c-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0860c-374">PowerShell</span></span>
<span data-ttu-id="0860c-375">Merhaba cmdlet tooget hello küme durumu [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="0860c-375">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="0860c-376">İlk olarak, hello kullanarak toohello kümesine bağlanın [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0860c-376">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="0860c-377">Hata dışında her zaman döndürülmesi gereken belirli bir düğüm, yalnızca olmaları durumunda hello aşağıdaki kodu düğümleri alır.</span><span class="sxs-lookup"><span data-stu-id="0860c-377">hello following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

<span data-ttu-id="0860c-378">cmdlet aşağıdaki hello küme Öbek ile uygulama filtrelerini alır.</span><span class="sxs-lookup"><span data-stu-id="0860c-378">hello following cmdlet gets cluster chunk with application filters.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

<span data-ttu-id="0860c-379">Merhaba aşağıdaki cmdlet'i tüm dağıtılan varlıklar bir düğümde döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-379">hello following cmdlet returns all deployed entities on a node.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a><span data-ttu-id="0860c-380">REST</span><span class="sxs-lookup"><span data-stu-id="0860c-380">REST</span></span>
<span data-ttu-id="0860c-381">Küme durumu Öbek ile alabileceğiniz bir [GET isteği](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) veya [POST isteği](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) sistem durumu ilkeleri ve Gelişmiş filtreleri hello gövdesinde açıklanan içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in hello body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="0860c-382">Genel sorgular</span><span class="sxs-lookup"><span data-stu-id="0860c-382">General queries</span></span>
<span data-ttu-id="0860c-383">Genel sorguları belirtilen bir türün Service Fabric varlıkların listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="0860c-384">Merhaba API sunulur (Merhaba yöntemleri aracılığıyla **FabricClient.QueryManager**), PowerShell cmdlet'leri ve REST.</span><span class="sxs-lookup"><span data-stu-id="0860c-384">They are exposed through hello API (via hello methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="0860c-385">Bu sorgular, alt sorgular birden çok bileşenlerini toplama.</span><span class="sxs-lookup"><span data-stu-id="0860c-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="0860c-386">Bunlardan biri olan hello [sistem durumu deposu](service-fabric-health-introduction.md#health-store), toplanan her sorgu sonucu için sistem durumu, hello doldurur.</span><span class="sxs-lookup"><span data-stu-id="0860c-386">One of them is hello [health store](service-fabric-health-introduction.md#health-store), which populates hello aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="0860c-387">Genel sorgular hello toplanan sistem durumu hello varlığın dönün ve zengin sistem durumu verileri içermez.</span><span class="sxs-lookup"><span data-stu-id="0860c-387">General queries return hello aggregated health state of hello entity and do not contain rich health data.</span></span> <span data-ttu-id="0860c-388">Bir varlık sağlam değilse, sistem durumu sorguları tooget ile olayları, alt sistem durumlarını ve sağlıksız değerlendirmeleri gibi tüm sistem durumu bilgilerini, izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0860c-388">If an entity is not healthy, you can follow up with health queries tooget all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="0860c-389">Genel sorgular bir varlık için bir bilinmeyen sistem durumu döndürürse, bu hello sistem durumu depoyu hello varlık hakkında tam veri yok mümkündür.</span><span class="sxs-lookup"><span data-stu-id="0860c-389">If general queries return an unknown health state for an entity, it's possible that hello health store doesn't have complete data about hello entity.</span></span> <span data-ttu-id="0860c-390">Ayrıca bir alt sorgu toohello sistem durumu deposu başarılı değildi mümkündür (örneğin, bir iletişim hatası oluştu veya hello sistem durumu deposu kısıtlanan).</span><span class="sxs-lookup"><span data-stu-id="0860c-390">It's also possible that a subquery toohello health store wasn't successful (for example, there was a communication error, or hello health store was throttled).</span></span> <span data-ttu-id="0860c-391">Merhaba varlık için bir sistem durumu sorgusu ile izle.</span><span class="sxs-lookup"><span data-stu-id="0860c-391">Follow up with a health query for hello entity.</span></span> <span data-ttu-id="0860c-392">Merhaba alt sorgu ağ sorunları gibi geçici bir hatayla karşılaştı, bu izleme sorgu başarılı olabilir.</span><span class="sxs-lookup"><span data-stu-id="0860c-392">If hello subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="0860c-393">Bu aynı zamanda, daha fazla ayrıntı neden hello varlık sunulmaz hakkında hello health Store'dan verebilir.</span><span class="sxs-lookup"><span data-stu-id="0860c-393">It may also give you more details from hello health store about why hello entity is not exposed.</span></span>

<span data-ttu-id="0860c-394">Merhaba içeren sorgular **HealthState** varlıklar için:</span><span class="sxs-lookup"><span data-stu-id="0860c-394">hello queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="0860c-395">Düğüm listesi: (disk belleği) hello kümede hello liste düğümlerine döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-395">Node list: Returns hello list nodes in hello cluster (paged).</span></span>
  * <span data-ttu-id="0860c-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="0860c-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="0860c-397">PowerShell: Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="0860c-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="0860c-398">Uygulama listesi: döndürür hello (disk belleği) hello kümedeki uygulamaların listesi.</span><span class="sxs-lookup"><span data-stu-id="0860c-398">Application list: Returns hello list of applications in hello cluster (paged).</span></span>
  * <span data-ttu-id="0860c-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="0860c-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="0860c-400">PowerShell: Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="0860c-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="0860c-401">Hizmet listesi: (disk belleği) bir uygulamanın hizmet hello listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-401">Service list: Returns hello list of services in an application (paged).</span></span>
  * <span data-ttu-id="0860c-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="0860c-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="0860c-403">PowerShell: Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="0860c-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="0860c-404">Bölüm listesi: (disk belleği) bir hizmet bölümlerinde hello listesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-404">Partition list: Returns hello list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="0860c-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="0860c-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="0860c-406">PowerShell: Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="0860c-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="0860c-407">Çoğaltma Listesi: (disk belleği) bir bölüm kopyalarını hello listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-407">Replica list: Returns hello list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="0860c-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="0860c-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="0860c-409">PowerShell: Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="0860c-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="0860c-410">Uygulama listesi dağıtılan: bir düğümde dağıtılan uygulamalar hello listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-410">Deployed application list: Returns hello list of deployed applications on a node.</span></span>
  * <span data-ttu-id="0860c-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="0860c-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="0860c-412">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="0860c-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="0860c-413">Hizmet paketi listesi dağıtılan: dağıtılan bir uygulama, hizmet paketleri hello listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-413">Deployed service package list: Returns hello list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="0860c-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="0860c-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="0860c-415">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="0860c-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="0860c-416">Bazı hello sorguları, disk belleğine alınan sonuçları döndürür.</span><span class="sxs-lookup"><span data-stu-id="0860c-416">Some of hello queries return paged results.</span></span> <span data-ttu-id="0860c-417">Merhaba bu sorguların return türetilmiş bir listedir [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="0860c-417">hello return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="0860c-418">Merhaba sonuçları bir ileti uymuyorsa yalnızca bir sayfa döndürülür ve bir ContinuationToken, numaralandırma durduğu izler.</span><span class="sxs-lookup"><span data-stu-id="0860c-418">If hello results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="0860c-419">Aynı sorgu ve hello devamlılık belirteci hello önceki sorgu tooget sonraki sonuçlarından geçirin toocall hello devam edin.</span><span class="sxs-lookup"><span data-stu-id="0860c-419">Continue toocall hello same query and pass in hello continuation token from hello previous query tooget next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="0860c-420">Örnekler</span><span class="sxs-lookup"><span data-stu-id="0860c-420">Examples</span></span>
<span data-ttu-id="0860c-421">Merhaba aşağıdaki kodu hello sağlıksız uygulamaları hello kümede alır:</span><span class="sxs-lookup"><span data-stu-id="0860c-421">hello following code gets hello unhealthy applications in hello cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="0860c-422">Merhaba aşağıdaki cmdlet'i alır hello doku hello uygulama ayrıntılarını: / WordCount uygulamasını.</span><span class="sxs-lookup"><span data-stu-id="0860c-422">hello following cmdlet gets hello application details for hello fabric:/WordCount application.</span></span> <span data-ttu-id="0860c-423">Sistem durumu uyarı konumunda olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="0860c-423">Notice that health state is at warning.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

<span data-ttu-id="0860c-424">Merhaba aşağıdaki cmdlet'i hello hata sistem durumu hizmetleriyle alır:</span><span class="sxs-lookup"><span data-stu-id="0860c-424">hello following cmdlet gets hello services with a health state of error:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="0860c-425">Küme ve uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="0860c-425">Cluster and application upgrades</span></span>
<span data-ttu-id="0860c-426">Merhaba küme ve uygulama izlenen bir yükseltme sırasında Service Fabric sistem durumu tooensure her şeyi sağlıklı kalmasını denetler.</span><span class="sxs-lookup"><span data-stu-id="0860c-426">During a monitored upgrade of hello cluster and application, Service Fabric checks health tooensure that everything remains healthy.</span></span> <span data-ttu-id="0860c-427">Bir varlık olarak yapılandırılmış sistem durumu ilkeleri kullanılarak hesaplanan sağlıksız ise hello yükseltme yükseltme özgü ilkeler toodetermine hello bir sonraki eylem geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0860c-427">If an entity is unhealthy as evaluated by using configured health policies, hello upgrade applies upgrade-specific policies toodetermine hello next action.</span></span> <span data-ttu-id="0860c-428">Merhaba yükseltme (örneğin, hata koşullarını düzelttikten veya ilkelerini değiştirme) duraklatılmış tooallow kullanıcı etkileşimi olabilir veya bu otomatik olarak toohello önceki iyi sürümüne geri.</span><span class="sxs-lookup"><span data-stu-id="0860c-428">hello upgrade may be paused tooallow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back toohello previous good version.</span></span>

<span data-ttu-id="0860c-429">Sırasında bir *küme* yükseltme, hello Küme Yükseltme durumu alma.</span><span class="sxs-lookup"><span data-stu-id="0860c-429">During a *cluster* upgrade, you can get hello cluster upgrade status.</span></span> <span data-ttu-id="0860c-430">Merhaba yükseltme Durumu sağlıksız değerlendirmeleri, hangi noktası toowhat hello kümede sağlıksız olduğunu içerir.</span><span class="sxs-lookup"><span data-stu-id="0860c-430">hello upgrade status includes unhealthy evaluations, which point toowhat is unhealthy in hello cluster.</span></span> <span data-ttu-id="0860c-431">Toohealth sorunları Hello yükseltme geri alınması durumunda, hello yükseltme durumu hello son sağlıksız nedenleri hatırlıyor.</span><span class="sxs-lookup"><span data-stu-id="0860c-431">If hello upgrade is rolled back due toohealth issues, hello upgrade status remembers hello last unhealthy reasons.</span></span> <span data-ttu-id="0860c-432">Bu bilgileri yöneticilerin hello yükseltme geri alındı veya durduruldu sonra nelerin yanlış gittiğini araştırmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="0860c-432">This information can help administrators investigate what went wrong after hello upgrade rolled back or stopped.</span></span>

<span data-ttu-id="0860c-433">Benzer şekilde, sırasında bir *uygulama* yükseltme, tüm sağlıksız değerlendirmeleri hello uygulama yükseltme durumunu da bulunur.</span><span class="sxs-lookup"><span data-stu-id="0860c-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in hello application upgrade status.</span></span>

<span data-ttu-id="0860c-434">Merhaba aşağıdaki hello uygulama yükseltme durumu değiştirilmiş bir yapı için gösterir: / WordCount uygulamasını.</span><span class="sxs-lookup"><span data-stu-id="0860c-434">hello following shows hello application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="0860c-435">Bir izleme çoğaltmalarını birinde bir hata bildirdi.</span><span class="sxs-lookup"><span data-stu-id="0860c-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="0860c-436">Merhaba durumu denetimleri değil geri dikkate alır çünkü hello yükseltme alınıyor.</span><span class="sxs-lookup"><span data-stu-id="0860c-436">hello upgrade is rolling back because hello health checks are not respected.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

<span data-ttu-id="0860c-437">Merhaba hakkında daha fazla bilgiyi [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="0860c-437">Read more about hello [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-tootroubleshoot"></a><span data-ttu-id="0860c-438">Sistem durumu değerlendirmesini tootroubleshoot kullanın</span><span class="sxs-lookup"><span data-stu-id="0860c-438">Use health evaluations tootroubleshoot</span></span>
<span data-ttu-id="0860c-439">Merhaba küme ya da bir uygulama ile ilgili bir sorun olduğunda hello küme veya uygulama sistem durumu toopinpoint sorunun ne olduğunu arayın.</span><span class="sxs-lookup"><span data-stu-id="0860c-439">Whenever there is an issue with hello cluster or an application, look at hello cluster or application health toopinpoint what is wrong.</span></span> <span data-ttu-id="0860c-440">Merhaba sağlıksız değerlendirmeleri hangi tetiklenen hello geçerli iyi olmayan sistem durumu hakkında ayrıntılar verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0860c-440">hello unhealthy evaluations provide details about what triggered hello current unhealthy state.</span></span> <span data-ttu-id="0860c-441">Gerekiyorsa, sağlam olmayan alt varlıkları tooidentify hello kök nedeni ayrıntıya girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0860c-441">If you need to, you can drill down into unhealthy child entities tooidentify hello root cause.</span></span>

<span data-ttu-id="0860c-442">Örneğin, bir hata raporu çoğaltmalarını birinde olduğundan bir uygulama sağlıksız düşünün.</span><span class="sxs-lookup"><span data-stu-id="0860c-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="0860c-443">Merhaba aşağıdaki Powershell cmdlet'ini hello sağlıksız değerlendirmeleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="0860c-443">hello following Powershell cmdlet shows hello unhealthy evaluations:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

<span data-ttu-id="0860c-444">Daha fazla bilgi hello çoğaltma tooget arayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0860c-444">You can look at hello replica tooget more information:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="0860c-445">Merhaba sağlıksız değerlendirmeleri göster hello ilk neden hello varlık toocurrent sistem durumu değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="0860c-445">hello unhealthy evaluations show hello first reason hello entity is evaluated toocurrent health state.</span></span> <span data-ttu-id="0860c-446">Bu durum tetiklemek birden çok olay olabilir, ancak bunlar değil olması yansıtılır hello değerlendirmeleri.</span><span class="sxs-lookup"><span data-stu-id="0860c-446">There may be multiple other events that trigger this state, but they are not be reflected in hello evaluations.</span></span> <span data-ttu-id="0860c-447">tooget hello sistem durumu varlıkları toofigure hello kümedeki tüm hello sağlıksız raporların aşağı ayrıntıya hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="0860c-447">tooget more information, drill down into hello health entities toofigure out all hello unhealthy reports in hello cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="0860c-448">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0860c-448">Next steps</span></span>
[<span data-ttu-id="0860c-449">Sistem durumu raporları tootroubleshoot kullanın</span><span class="sxs-lookup"><span data-stu-id="0860c-449">Use system health reports tootroubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="0860c-450">Özel Service Fabric sistem durumu rapor ekleme</span><span class="sxs-lookup"><span data-stu-id="0860c-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="0860c-451">Nasıl tooreport ve onay sistem durumu hizmeti</span><span class="sxs-lookup"><span data-stu-id="0860c-451">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="0860c-452">İzleme ve Hizmetleri yerel olarak tanılama</span><span class="sxs-lookup"><span data-stu-id="0860c-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="0860c-453">Service Fabric uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="0860c-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
