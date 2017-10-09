---
title: "Sistem durumu raporlarını ile aaaTroubleshoot | Microsoft Docs"
description: "Sorun giderme küme veya uygulama sorunları için Azure Service Fabric bileşenleri ve bunların kullanım tarafından gönderilen hello sistem durumu raporları açıklar."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a><span data-ttu-id="94d63-103">Sistem durumu raporları tootroubleshoot kullanın</span><span class="sxs-lookup"><span data-stu-id="94d63-103">Use system health reports tootroubleshoot</span></span>
<span data-ttu-id="94d63-104">Azure Service Fabric bileşenleri raporda hello kutusu dışında hello kümedeki tüm varlıklar.</span><span class="sxs-lookup"><span data-stu-id="94d63-104">Azure Service Fabric components report out of hello box on all entities in hello cluster.</span></span> <span data-ttu-id="94d63-105">Merhaba [sistem durumu deposu](service-fabric-health-introduction.md#health-store) oluşturur ve hello sistem raporlarına dayalı varlıklar siler.</span><span class="sxs-lookup"><span data-stu-id="94d63-105">hello [health store](service-fabric-health-introduction.md#health-store) creates and deletes entities based on hello system reports.</span></span> <span data-ttu-id="94d63-106">Bu da onları varlık etkileşimleri yakalayan bir hiyerarşide düzenler.</span><span class="sxs-lookup"><span data-stu-id="94d63-106">It also organizes them in a hierarchy that captures entity interactions.</span></span>

> [!NOTE]
> <span data-ttu-id="94d63-107">Sistem durumu ile ilgili toounderstand kavramları hakkında daha fazla okuma [Service Fabric sistem durumu modeli](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="94d63-107">toounderstand health-related concepts, read more at [Service Fabric health model](service-fabric-health-introduction.md).</span></span>
> 
> 

<span data-ttu-id="94d63-108">Sistem durumu raporlarını küme ve uygulama işlevselliğini ve sistem durumu üzerinden bayrağı sorunların görünürlük sağlar.</span><span class="sxs-lookup"><span data-stu-id="94d63-108">System health reports provide visibility into cluster and application functionality and flag issues through health.</span></span> <span data-ttu-id="94d63-109">Uygulamalar ve hizmetler için sistem durumu raporlarını varlıkları uygulanır ve Service Fabric perspektif hello doğru davranmakta olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="94d63-109">For applications and services, system health reports verify that entities are implemented and are behaving correctly from hello Service Fabric perspective.</span></span> <span data-ttu-id="94d63-110">Merhaba raporları tüm sistem durumu hello iş mantığı hello hizmetinin veya askıdaki işlemleri algılamak izleme sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="94d63-110">hello reports do not provide any health monitoring of hello business logic of hello service or detection of hung processes.</span></span> <span data-ttu-id="94d63-111">Kullanıcı Hizmetleri hello sistem durumu bilgileri belirli tootheir mantığı verilerle zenginleştirmek.</span><span class="sxs-lookup"><span data-stu-id="94d63-111">User services can enrich hello health data with information specific tootheir logic.</span></span>

> [!NOTE]
> <span data-ttu-id="94d63-112">Watchdogs durum raporları görünür yalnızca *sonra* hello sistem bileşenleri bir varlık oluşturun.</span><span class="sxs-lookup"><span data-stu-id="94d63-112">Watchdogs health reports are visible only *after* hello system components create an entity.</span></span> <span data-ttu-id="94d63-113">Bir varlık silindiğinde, hello sistem durumu deposu ile ilişkili tüm sistem durumu raporları otomatik olarak siler.</span><span class="sxs-lookup"><span data-stu-id="94d63-113">When an entity is deleted, hello health store automatically deletes all health reports associated with it.</span></span> <span data-ttu-id="94d63-114">Merhaba varlık yeni bir örneğini oluştururken hello aynı durum geçerlidir (örneğin, yeni bir durum bilgisi olan kalıcı hizmet çoğaltma örneği oluşturulur).</span><span class="sxs-lookup"><span data-stu-id="94d63-114">hello same is true when a new instance of hello entity is created (for example, a new stateful persisted service replica instance is created).</span></span> <span data-ttu-id="94d63-115">Merhaba eski örneği ile ilişkili tüm raporlar silinir ve hello deposundan temizlendi.</span><span class="sxs-lookup"><span data-stu-id="94d63-115">All reports associated with hello old instance are deleted and cleaned up from hello store.</span></span>
> 
> 

<span data-ttu-id="94d63-116">Merhaba sistem bileşeni raporları hello ile başlayan hello kaynağa göre tanımlanır "**sistem.**"</span><span class="sxs-lookup"><span data-stu-id="94d63-116">hello system component reports are identified by hello source, which starts with hello "**System.**"</span></span> <span data-ttu-id="94d63-117">önek.</span><span class="sxs-lookup"><span data-stu-id="94d63-117">prefix.</span></span> <span data-ttu-id="94d63-118">Geçersiz parametreler raporlarla reddedildi olarak watchdogs için kaynakları, aynı önek hello kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="94d63-118">Watchdogs can't use hello same prefix for their sources, as reports with invalid parameters are rejected.</span></span>
<span data-ttu-id="94d63-119">Şimdi ne tetikler toounderstand bazı sistem bakma raporları ve toocorrect hello nasıl olası sorunları bunlar temsil eder.</span><span class="sxs-lookup"><span data-stu-id="94d63-119">Let's look at some system reports toounderstand what triggers them and how toocorrect hello possible issues they represent.</span></span>

> [!NOTE]
> <span data-ttu-id="94d63-120">Service Fabric hello küme ve uygulama olanlar içine görünürlüğünü artırmak koşullar ilgi tooadd raporlarda devam eder.</span><span class="sxs-lookup"><span data-stu-id="94d63-120">Service Fabric continues tooadd reports on conditions of interest that improve visibility into what is happening in hello cluster and application.</span></span> <span data-ttu-id="94d63-121">Varolan raporları de Gelişmiş ile daha fazla ayrıntı toohelp sorun giderme hello sorunu daha hızlı.</span><span class="sxs-lookup"><span data-stu-id="94d63-121">Existing reports can also be enhanced with more details toohelp troubleshoot hello problem faster.</span></span>
> 
> 

## <a name="cluster-system-health-reports"></a><span data-ttu-id="94d63-122">Sistem durumu raporlarını küme</span><span class="sxs-lookup"><span data-stu-id="94d63-122">Cluster system health reports</span></span>
<span data-ttu-id="94d63-123">Merhaba küme durumu varlık hello health store içinde otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="94d63-123">hello cluster health entity is created automatically in hello health store.</span></span> <span data-ttu-id="94d63-124">Her şeyi düzgün çalışmıyorsa, sistemi raporu yok.</span><span class="sxs-lookup"><span data-stu-id="94d63-124">If everything works properly, it doesn't have a system report.</span></span>

### <a name="neighborhood-loss"></a><span data-ttu-id="94d63-125">Komşuları kaybı</span><span class="sxs-lookup"><span data-stu-id="94d63-125">Neighborhood loss</span></span>
<span data-ttu-id="94d63-126">**System.Federation** Komşuları kaybı algıladığında bir hata bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-126">**System.Federation** reports an error when it detects a neighborhood loss.</span></span> <span data-ttu-id="94d63-127">tek tek düğümlerden Hello rapordur ve hello düğüm kimliği hello özellik adı dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="94d63-127">hello report is from individual nodes, and hello node ID is included in hello property name.</span></span> <span data-ttu-id="94d63-128">İki olay (Merhaba boşluk rapor her iki tarafında) genellikle bir Komşuları hello tüm Service Fabric halka kaybederseniz bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94d63-128">If one neighborhood is lost in hello entire Service Fabric ring, you can typically expect two events (both sides of hello gap report).</span></span> <span data-ttu-id="94d63-129">Daha fazla Semt kaybolursa, daha fazla olay vardır.</span><span class="sxs-lookup"><span data-stu-id="94d63-129">If more neighborhoods are lost, there are more events.</span></span>

<span data-ttu-id="94d63-130">Merhaba rapor hello genel kira zaman aşımı toolive hello zaman olarak belirtir.</span><span class="sxs-lookup"><span data-stu-id="94d63-130">hello report specifies hello global lease timeout as hello time toolive.</span></span> <span data-ttu-id="94d63-131">Merhaba koşul etkin kaldığı sürece hello rapor hello TTL süresince her yarısı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="94d63-131">hello report is resent every half of hello TTL duration for as long as hello condition remains active.</span></span> <span data-ttu-id="94d63-132">Merhaba olay süresi dolduğunda, otomatik olarak kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="94d63-132">hello event is automatically removed when it expires.</span></span> <span data-ttu-id="94d63-133">Merhaba raporlama düğümü çalışmıyor olsa bile hello rapor hello health Store'dan doğru temizlenir, süresi dolan davranış sağlar kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="94d63-133">Remove when expired behavior ensures that hello report is cleaned up from hello health store correctly, even if hello reporting node is down.</span></span>

* <span data-ttu-id="94d63-134">**SourceId**: System.Federation</span><span class="sxs-lookup"><span data-stu-id="94d63-134">**SourceId**: System.Federation</span></span>
* <span data-ttu-id="94d63-135">**Özellik**: ile başlayan **Komşuları** ve düğüm bilgiler yer almaktadır</span><span class="sxs-lookup"><span data-stu-id="94d63-135">**Property**: Starts with **Neighborhood** and includes node information</span></span>
* <span data-ttu-id="94d63-136">**Sonraki adımlar**: neden hello Komşuları (örneğin, küme düğümleri arasındaki onay hello iletişimi) kaybolur araştırın.</span><span class="sxs-lookup"><span data-stu-id="94d63-136">**Next steps**: Investigate why hello neighborhood is lost (for example, check hello communication between cluster nodes).</span></span>

## <a name="node-system-health-reports"></a><span data-ttu-id="94d63-137">Düğüm sistem durumu raporları</span><span class="sxs-lookup"><span data-stu-id="94d63-137">Node system health reports</span></span>
<span data-ttu-id="94d63-138">**System.FM**, hello Yük Devretme Yöneticisi hizmetini temsil eder, küme düğümleri hakkında bilgi yönetir hello yetkilisi.</span><span class="sxs-lookup"><span data-stu-id="94d63-138">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about cluster nodes.</span></span> <span data-ttu-id="94d63-139">Her düğüm System.FM durumunu gösteren bir raporu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="94d63-139">Each node should have one report from System.FM showing its state.</span></span> <span data-ttu-id="94d63-140">Merhaba düğümü varlıklar hello düğüm durumu kaldırıldığında kaldırılır (bkz [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span><span class="sxs-lookup"><span data-stu-id="94d63-140">hello node entities are removed when hello node state is removed (see [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).</span></span>

### <a name="node-updown"></a><span data-ttu-id="94d63-141">Düğüm yukarı/aşağı</span><span class="sxs-lookup"><span data-stu-id="94d63-141">Node up/down</span></span>
<span data-ttu-id="94d63-142">Merhaba düğümü (Bu da çalışır durumda) hello halkası katıldığında System.FM Tamam bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-142">System.FM reports as OK when hello node joins hello ring (it's up and running).</span></span> <span data-ttu-id="94d63-143">Merhaba halkası Hello düğümü departs zaman bir hata bildiriyor (aşağı, yükseltme ya da yalnızca bozulmuş başarısız oldu çünkü).</span><span class="sxs-lookup"><span data-stu-id="94d63-143">It reports an error when hello node departs hello ring (it's down, either for upgrading or simply because it has failed).</span></span> <span data-ttu-id="94d63-144">Merhaba sistem durumu mağaza tarafından oluşturulmuş hello sistem durumu hiyerarşi bağıntı System.FM düğüm raporları ile birlikte dağıtılan varlıklarda eylemi alır.</span><span class="sxs-lookup"><span data-stu-id="94d63-144">hello health hierarchy built by hello health store takes action on deployed entities in correlation with System.FM node reports.</span></span> <span data-ttu-id="94d63-145">Merhaba düğüm tüm dağıtılan varlıkların sanal üst dikkate alır.</span><span class="sxs-lookup"><span data-stu-id="94d63-145">It considers hello node a virtual parent of all deployed entities.</span></span> <span data-ttu-id="94d63-146">Yukarı System.FM tarafından hello ile aynı hello varlıkla ilişkili hello örneği olarak örnek olarak hello düğümü bildirilirse bu düğümde dağıtılan hello varlıklar sorguları sunulur.</span><span class="sxs-lookup"><span data-stu-id="94d63-146">hello deployed entities on that node are exposed through queries if hello node is reported as up by System.FM, with hello same instance as hello instance associated with hello entities.</span></span> <span data-ttu-id="94d63-147">System.FM o hello düğümü kapalı veya (yeni bir örneği) yeniden bildirdiğinde hello sistem durumu depolama yalnızca düğüm aşağı hello veya hello düğümünün hello önceki örneğinde bulunabilir dağıtılan hello varlıklar otomatik olarak temizler.</span><span class="sxs-lookup"><span data-stu-id="94d63-147">When System.FM reports that hello node is down or restarted (a new instance), hello health store automatically cleans up hello deployed entities that can exist only on hello down node or on hello previous instance of hello node.</span></span>

* <span data-ttu-id="94d63-148">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="94d63-148">**SourceId**: System.FM</span></span>
* <span data-ttu-id="94d63-149">**Özellik**: durumu</span><span class="sxs-lookup"><span data-stu-id="94d63-149">**Property**: State</span></span>
* <span data-ttu-id="94d63-150">**Sonraki adımlar**: hello düğümü için bir yükseltme çalışmıyorsa, onu yükseltildikten sonra geri gelmesi.</span><span class="sxs-lookup"><span data-stu-id="94d63-150">**Next steps**: If hello node is down for an upgrade, it should come back up once it has been upgraded.</span></span> <span data-ttu-id="94d63-151">Bu durumda, hello sistem durumu geri tooOK geçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="94d63-151">In this case, hello health state should switch back tooOK.</span></span> <span data-ttu-id="94d63-152">Merhaba düğümü geri gelmez veya bu başarısız olursa hello sorunu daha fazla araştırma gerekir.</span><span class="sxs-lookup"><span data-stu-id="94d63-152">If hello node doesn't come back or it fails, hello problem needs more investigation.</span></span>

<span data-ttu-id="94d63-153">Merhaba aşağıdaki örnek hello System.FM olay Tamam düğümü için bir sistem durumu ile görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="94d63-153">hello following example shows hello System.FM event with a health state of OK for node up:</span></span>

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a><span data-ttu-id="94d63-154">Sertifika süre sonu</span><span class="sxs-lookup"><span data-stu-id="94d63-154">Certificate expiration</span></span>
<span data-ttu-id="94d63-155">**System.FabricNode** hello düğüm tarafından kullanılan sertifika sona erme olduğunda bir uyarı bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-155">**System.FabricNode** reports a warning when certificates used by hello node are near expiration.</span></span> <span data-ttu-id="94d63-156">Düğüm başına üç sertifika vardır: **Certificate_cluster**, **Certificate_server**, ve **Certificate_default_client**.</span><span class="sxs-lookup"><span data-stu-id="94d63-156">There are three certificates per node: **Certificate_cluster**, **Certificate_server**, and **Certificate_default_client**.</span></span> <span data-ttu-id="94d63-157">Merhaba geçerlilik süresi en az iki hafta sonra hello rapor sistem durumu Tamam olur.</span><span class="sxs-lookup"><span data-stu-id="94d63-157">When hello expiration is at least two weeks away, hello report health state is OK.</span></span> <span data-ttu-id="94d63-158">Merhaba sona erme iki hafta içinde hello rapor türü bir uyarı olur.</span><span class="sxs-lookup"><span data-stu-id="94d63-158">When hello expiration is within two weeks, hello report type is a warning.</span></span> <span data-ttu-id="94d63-159">Bu olayların TTL sonsuzdur ve bir düğüm hello küme ayrıldığında bunlar kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="94d63-159">TTL of these events is infinite, and they are removed when a node leaves hello cluster.</span></span>

* <span data-ttu-id="94d63-160">**SourceId**: System.FabricNode</span><span class="sxs-lookup"><span data-stu-id="94d63-160">**SourceId**: System.FabricNode</span></span>
* <span data-ttu-id="94d63-161">**Özellik**: ile başlayan **sertifika** ve hello sertifika türü hakkında daha fazla bilgi içerir</span><span class="sxs-lookup"><span data-stu-id="94d63-161">**Property**: Starts with **Certificate** and contains more information about hello certificate type</span></span>
* <span data-ttu-id="94d63-162">**Sonraki adımlar**: sona erme olmaları durumunda hello sertifikaları güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="94d63-162">**Next steps**: Update hello certificates if they are near expiration.</span></span>

### <a name="load-capacity-violation"></a><span data-ttu-id="94d63-163">Yük kapasite ihlali</span><span class="sxs-lookup"><span data-stu-id="94d63-163">Load capacity violation</span></span>
<span data-ttu-id="94d63-164">düğüm kapasitesi ihlaline neden algıladığında bir uyarı hello Service Fabric yük dengeleyici bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-164">hello Service Fabric Load Balancer reports a warning when it detects a node capacity violation.</span></span>

* <span data-ttu-id="94d63-165">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="94d63-165">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="94d63-166">**Özellik**: ile başlayan **kapasitesi**</span><span class="sxs-lookup"><span data-stu-id="94d63-166">**Property**: Starts with **Capacity**</span></span>
* <span data-ttu-id="94d63-167">**Sonraki adımlar**: onay sağlanan Ölçümler ve görünüm hello geçerli kapasite hello düğümde.</span><span class="sxs-lookup"><span data-stu-id="94d63-167">**Next steps**: Check provided metrics and view hello current capacity on hello node.</span></span>

## <a name="application-system-health-reports"></a><span data-ttu-id="94d63-168">Uygulama sistem durumu raporları</span><span class="sxs-lookup"><span data-stu-id="94d63-168">Application system health reports</span></span>
<span data-ttu-id="94d63-169">**System.CM**, hello Küme Yöneticisi hizmetini temsil eder, bir uygulamayla ilgili bilgileri yönetir hello yetkilisi.</span><span class="sxs-lookup"><span data-stu-id="94d63-169">**System.CM**, which represents hello Cluster Manager service, is hello authority that manages information about an application.</span></span>

### <a name="state"></a><span data-ttu-id="94d63-170">Durum</span><span class="sxs-lookup"><span data-stu-id="94d63-170">State</span></span>
<span data-ttu-id="94d63-171">Merhaba uygulaması oluşturulduğunda veya güncelleştirilmiş System.CM olarak Tamam bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-171">System.CM reports as OK when hello application has been created or updated.</span></span> <span data-ttu-id="94d63-172">Merhaba uygulaması silindiğinde deposundan kaldırılabilir böylece hello sistem durumu deposu bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-172">It informs hello health store when hello application has been deleted, so that it can be removed from store.</span></span>

* <span data-ttu-id="94d63-173">**SourceId**: System.CM</span><span class="sxs-lookup"><span data-stu-id="94d63-173">**SourceId**: System.CM</span></span>
* <span data-ttu-id="94d63-174">**Özellik**: durumu</span><span class="sxs-lookup"><span data-stu-id="94d63-174">**Property**: State</span></span>
* <span data-ttu-id="94d63-175">**Sonraki adımlar**: Merhaba uygulaması oluşturduysanız veya güncelleştirilmiş hello Küme Yöneticisi sistem durumu raporu içermelidir.</span><span class="sxs-lookup"><span data-stu-id="94d63-175">**Next steps**: If hello application has been created or updated, it should include hello Cluster Manager health report.</span></span> <span data-ttu-id="94d63-176">Aksi takdirde, sorgu vererek Merhaba uygulaması hello durumunu denetleyin (örneğin, PowerShell cmdlet'ini hello **Get-ServiceFabricApplication - ApplicationName *applicationName***).</span><span class="sxs-lookup"><span data-stu-id="94d63-176">Otherwise, check hello state of hello application by issuing a query (for example, hello PowerShell cmdlet **Get-ServiceFabricApplication -ApplicationName *applicationName***).</span></span>

<span data-ttu-id="94d63-177">Merhaba aşağıdaki örnek hello durum olayı üzerinde hello gösterir **fabric: / WordCount** uygulama:</span><span class="sxs-lookup"><span data-stu-id="94d63-177">hello following example shows hello state event on hello **fabric:/WordCount** application:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a><span data-ttu-id="94d63-178">Hizmet sistem durumu raporları</span><span class="sxs-lookup"><span data-stu-id="94d63-178">Service system health reports</span></span>
<span data-ttu-id="94d63-179">**System.FM**, hello Yük Devretme Yöneticisi hizmetini temsil eder, hizmetler hakkında bilgi yönetir hello yetkilisi.</span><span class="sxs-lookup"><span data-stu-id="94d63-179">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about services.</span></span>

### <a name="state"></a><span data-ttu-id="94d63-180">Durum</span><span class="sxs-lookup"><span data-stu-id="94d63-180">State</span></span>
<span data-ttu-id="94d63-181">Merhaba hizmet oluşturduğunuzda System.FM olarak Tamam bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-181">System.FM reports as OK when hello service has been created.</span></span> <span data-ttu-id="94d63-182">Merhaba hizmet silindiğinde hello health Store'dan hello varlık siler.</span><span class="sxs-lookup"><span data-stu-id="94d63-182">It deletes hello entity from hello health store when hello service has been deleted.</span></span>

* <span data-ttu-id="94d63-183">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="94d63-183">**SourceId**: System.FM</span></span>
* <span data-ttu-id="94d63-184">**Özellik**: durumu</span><span class="sxs-lookup"><span data-stu-id="94d63-184">**Property**: State</span></span>

<span data-ttu-id="94d63-185">Merhaba aşağıdaki örnek hello durum olayı hello hizmette gösterir **fabric: / WordCount/WordCountWebService**:</span><span class="sxs-lookup"><span data-stu-id="94d63-185">hello following example shows hello state event on hello service **fabric:/WordCount/WordCountWebService**:</span></span>

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a><span data-ttu-id="94d63-186">Hizmet bağıntı hatası</span><span class="sxs-lookup"><span data-stu-id="94d63-186">Service correlation error</span></span>
<span data-ttu-id="94d63-187">**System.PLB** başka bir hizmetle ilişkili hizmet toobe güncelleştirme bir benzeşim zinciri oluşturur algıladığında bir hata bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-187">**System.PLB** reports an error when it detects that updating a service toobe correlated with another service creates an affinity chain.</span></span> <span data-ttu-id="94d63-188">başarılı güncelleştirme gerçekleştiğinde hello rapor temizlenir.</span><span class="sxs-lookup"><span data-stu-id="94d63-188">hello report is cleared when successful update happens.</span></span>

* <span data-ttu-id="94d63-189">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="94d63-189">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="94d63-190">**Özellik**: ServiceDescription</span><span class="sxs-lookup"><span data-stu-id="94d63-190">**Property**: ServiceDescription</span></span>
* <span data-ttu-id="94d63-191">**Sonraki adımlar**: onay hello bağıntılı hizmeti açıklamaları.</span><span class="sxs-lookup"><span data-stu-id="94d63-191">**Next steps**: Check hello correlated service descriptions.</span></span>

## <a name="partition-system-health-reports"></a><span data-ttu-id="94d63-192">Bölüm sistem durumu raporları</span><span class="sxs-lookup"><span data-stu-id="94d63-192">Partition system health reports</span></span>
<span data-ttu-id="94d63-193">**System.FM**, hello Yük Devretme Yöneticisi hizmetini temsil eder, hizmet bölümleri hakkında bilgi yönetir hello yetkilisi.</span><span class="sxs-lookup"><span data-stu-id="94d63-193">**System.FM**, which represents hello Failover Manager service, is hello authority that manages information about service partitions.</span></span>

### <a name="state"></a><span data-ttu-id="94d63-194">Durum</span><span class="sxs-lookup"><span data-stu-id="94d63-194">State</span></span>
<span data-ttu-id="94d63-195">Merhaba bölümü oluşturulup oluşturulmadığını ve iyi durumda olduğunda System.FM olarak Tamam bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-195">System.FM reports as OK when hello partition has been created and is healthy.</span></span> <span data-ttu-id="94d63-196">Merhaba Bölüm silindiğinde hello health Store'dan hello varlık siler.</span><span class="sxs-lookup"><span data-stu-id="94d63-196">It deletes hello entity from hello health store when hello partition is deleted.</span></span>

<span data-ttu-id="94d63-197">Merhaba bölüm hello minimum yineleme sayısı ise, bir hata bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-197">If hello partition is below hello minimum replica count, it reports an error.</span></span> <span data-ttu-id="94d63-198">Merhaba bölümü hello minimum yineleme sayısı değil, ancak hello hedef çoğaltma sayısı olan, bir uyarı bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-198">If hello partition is not below hello minimum replica count, but it is below hello target replica count, it reports a warning.</span></span> <span data-ttu-id="94d63-199">Merhaba bölüm çekirdek kaybında System.FM bir hata bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-199">If hello partition is in quorum loss, System.FM reports an error.</span></span>

<span data-ttu-id="94d63-200">Diğer önemli olayları Hello yeniden yapılandırma beklenenden ve hello yapı beklenenden daha uzun sürerse uzun sürerse bir uyarı içerir.</span><span class="sxs-lookup"><span data-stu-id="94d63-200">Other important events include a warning when hello reconfiguration takes longer than expected and when hello build takes longer than expected.</span></span> <span data-ttu-id="94d63-201">Beklenen hello kez hello derleme ve yeniden yapılandırma için hizmet senaryolarını temel alarak yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="94d63-201">hello expected times for hello build and reconfiguration are configurable based on service scenarios.</span></span> <span data-ttu-id="94d63-202">Örneğin, bir hizmet durumunun SQL veritabanı gibi bir terabayt varsa hello yapı durumu küçük miktarda bir hizmet için daha uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="94d63-202">For example, if a service has a terabyte of state, such as SQL Database, hello build takes longer than for a service with a small amount of state.</span></span>

* <span data-ttu-id="94d63-203">**SourceId**: System.FM</span><span class="sxs-lookup"><span data-stu-id="94d63-203">**SourceId**: System.FM</span></span>
* <span data-ttu-id="94d63-204">**Özellik**: durumu</span><span class="sxs-lookup"><span data-stu-id="94d63-204">**Property**: State</span></span>
* <span data-ttu-id="94d63-205">**Sonraki adımlar**: hello sistem durumu iyi değil, bazı çoğaltmaları oluşturulan, açılan ya da yükseltilen tooprimary veya ikincil doğru şekilde yapıldığını değil mümkündür.</span><span class="sxs-lookup"><span data-stu-id="94d63-205">**Next steps**: If hello health state is not OK, it's possible that some replicas have not been created, opened, or promoted tooprimary or secondary correctly.</span></span> <span data-ttu-id="94d63-206">Çoğu durumda, bir hizmet hata hello açık veya rolü Değiştir uygulamasında hello temel nedeni oluşturur.</span><span class="sxs-lookup"><span data-stu-id="94d63-206">In many instances, hello root cause is a service bug in hello open or change-role implementation.</span></span>

<span data-ttu-id="94d63-207">Aşağıdaki örnek hello sağlıklı bir bölüm gösterir:</span><span class="sxs-lookup"><span data-stu-id="94d63-207">hello following example shows a healthy partition:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="94d63-208">Merhaba aşağıdaki örnek hedef yineleme sayısı: bir bölüm hello durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="94d63-208">hello following example shows hello health of a partition that is below target replica count.</span></span> <span data-ttu-id="94d63-209">Merhaba sonraki adımdır nasıl yapılandırıldığını gösterir tooget hello bölüm açıklaması: **MinReplicaSetSize** üç ve **TargetReplicaSetSize** yedi değil.</span><span class="sxs-lookup"><span data-stu-id="94d63-209">hello next step is tooget hello partition description, which shows how it is configured: **MinReplicaSetSize** is three and **TargetReplicaSetSize** is seven.</span></span> <span data-ttu-id="94d63-210">Ardından hello kümedeki düğüm sayısını hello alırken: beş.</span><span class="sxs-lookup"><span data-stu-id="94d63-210">Then get hello number of nodes in hello cluster: five.</span></span> <span data-ttu-id="94d63-211">Merhaba hedef çoğaltmaların sayısı hello kullanılabilir düğüm sayısından daha yüksek olduğu için bu nedenle bu durumda, iki çoğaltma yerleştirilemez.</span><span class="sxs-lookup"><span data-stu-id="94d63-211">So in this case, two replicas can't be placed because hello target number of replicas is higher than hello number of nodes available.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
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
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a><span data-ttu-id="94d63-212">Çoğaltma kısıtlama ihlali</span><span class="sxs-lookup"><span data-stu-id="94d63-212">Replica constraint violation</span></span>
<span data-ttu-id="94d63-213">**System.PLB** çoğaltma kısıtlama ihlali algılar ve tüm çoğaltmalarını yerleştirilemiyor varsa bir uyarı bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-213">**System.PLB** reports a warning if it detects a replica constraint violation and can't place all partition replicas.</span></span> <span data-ttu-id="94d63-214">Hello rapor ayrıntılarının hangi kısıtlamaları ve hello çoğaltma yerleştirme özellikleri engelliyor.</span><span class="sxs-lookup"><span data-stu-id="94d63-214">hello report details show which constraints and properties prevent hello replica placement.</span></span>

* <span data-ttu-id="94d63-215">**SourceId**: System.PLB</span><span class="sxs-lookup"><span data-stu-id="94d63-215">**SourceId**: System.PLB</span></span>
* <span data-ttu-id="94d63-216">**Özellik**: ile başlayan **ReplicaConstraintViolation**</span><span class="sxs-lookup"><span data-stu-id="94d63-216">**Property**: Starts with **ReplicaConstraintViolation**</span></span>

## <a name="replica-system-health-reports"></a><span data-ttu-id="94d63-217">Çoğaltma sistem durumu raporları</span><span class="sxs-lookup"><span data-stu-id="94d63-217">Replica system health reports</span></span>
<span data-ttu-id="94d63-218">**System.RA**, hello yeniden yapılandırma aracı bileşeni temsil eden durumda hello çoğaltma durumu için hello yetkilidir.</span><span class="sxs-lookup"><span data-stu-id="94d63-218">**System.RA**, which represents hello reconfiguration agent component, is hello authority for hello replica state.</span></span>

### <a name="state"></a><span data-ttu-id="94d63-219">Durum</span><span class="sxs-lookup"><span data-stu-id="94d63-219">State</span></span>
<span data-ttu-id="94d63-220">**System.RA** hello çoğaltma oluşturduğunuzda Tamam bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-220">**System.RA** reports OK when hello replica has been created.</span></span>

* <span data-ttu-id="94d63-221">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="94d63-221">**SourceId**: System.RA</span></span>
* <span data-ttu-id="94d63-222">**Özellik**: durumu</span><span class="sxs-lookup"><span data-stu-id="94d63-222">**Property**: State</span></span>

<span data-ttu-id="94d63-223">Aşağıdaki örnek hello sağlıklı bir çoğaltma gösterir:</span><span class="sxs-lookup"><span data-stu-id="94d63-223">hello following example shows a healthy replica:</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a><span data-ttu-id="94d63-224">Çoğaltma açma durumu</span><span class="sxs-lookup"><span data-stu-id="94d63-224">Replica open status</span></span>
<span data-ttu-id="94d63-225">Merhaba API çağrısı çağrıldığında bu sistem durumu raporu hello açıklamasını hello başlangıç zamanı (Eşgüdümlü Evrensel Saat) içerir.</span><span class="sxs-lookup"><span data-stu-id="94d63-225">hello description of this health report contains hello start time (Coordinated Universal Time) when hello API call was invoked.</span></span>

<span data-ttu-id="94d63-226">**System.RA** hello çoğaltma açık yapılandırılmış hello süresinden daha uzun sürerse bir uyarı raporları (varsayılan: 30 dakika).</span><span class="sxs-lookup"><span data-stu-id="94d63-226">**System.RA** reports a warning if hello replica open takes longer than hello configured period (default: 30 minutes).</span></span> <span data-ttu-id="94d63-227">Hizmet kullanılabilirliği Hello API etkiler, hello rapor çok daha hızlı (bir yapılandırılabilir aralığıyla, varsayılan değer 30 saniyedir) verilir.</span><span class="sxs-lookup"><span data-stu-id="94d63-227">If hello API impacts service availability, hello report is issued much faster (a configurable interval, with a default of 30 seconds).</span></span> <span data-ttu-id="94d63-228">ölçülen hello zaman hello çoğaltıcı açın ve açık hello hizmeti için harcanan hello süre içerir.</span><span class="sxs-lookup"><span data-stu-id="94d63-228">hello time measured includes hello time taken for hello replicator open and hello service open.</span></span> <span data-ttu-id="94d63-229">Merhaba açarsanız hello özelliği değişiklikleri tooOK tamamlar.</span><span class="sxs-lookup"><span data-stu-id="94d63-229">hello property changes tooOK if hello open completes.</span></span>

* <span data-ttu-id="94d63-230">**SourceId**: System.RA</span><span class="sxs-lookup"><span data-stu-id="94d63-230">**SourceId**: System.RA</span></span>
* <span data-ttu-id="94d63-231">**Özellik**: **ReplicaOpenStatus**</span><span class="sxs-lookup"><span data-stu-id="94d63-231">**Property**: **ReplicaOpenStatus**</span></span>
* <span data-ttu-id="94d63-232">**Sonraki adımlar**: hello sistem durumu iyi değil, neden hello çoğaltma açık beklenenden uzun sürüyor araştırın.</span><span class="sxs-lookup"><span data-stu-id="94d63-232">**Next steps**: If hello health state is not OK, investigate why hello replica open takes longer than expected.</span></span>

### <a name="slow-service-api-call"></a><span data-ttu-id="94d63-233">Yavaş hizmeti API çağrısı</span><span class="sxs-lookup"><span data-stu-id="94d63-233">Slow service API call</span></span>
<span data-ttu-id="94d63-234">**System.RAP** ve **System.Replicator** çağrısı toohello kullanıcı hizmet kodu yapılandırılmış hello süreden uzun sürerse bir uyarı rapor.</span><span class="sxs-lookup"><span data-stu-id="94d63-234">**System.RAP** and **System.Replicator** report a warning if a call toohello user service code takes longer than hello configured time.</span></span> <span data-ttu-id="94d63-235">Merhaba çağrısı tamamlandığında hello uyarı temizlenir.</span><span class="sxs-lookup"><span data-stu-id="94d63-235">hello warning is cleared when hello call completes.</span></span>

* <span data-ttu-id="94d63-236">**SourceId**: System.RAP veya System.Replicator</span><span class="sxs-lookup"><span data-stu-id="94d63-236">**SourceId**: System.RAP or System.Replicator</span></span>
* <span data-ttu-id="94d63-237">**Özellik**: hello yavaş API hello adı.</span><span class="sxs-lookup"><span data-stu-id="94d63-237">**Property**: hello name of hello slow API.</span></span> <span data-ttu-id="94d63-238">Merhaba açıklama hello zaman hello API'si hakkında daha fazla ayrıntı bekleyen açıldı sağlar.</span><span class="sxs-lookup"><span data-stu-id="94d63-238">hello description provides more details about hello time hello API has been pending.</span></span>
* <span data-ttu-id="94d63-239">**Sonraki adımlar**: hello çağrısı neden beklenenden uzun sürüyor araştırın.</span><span class="sxs-lookup"><span data-stu-id="94d63-239">**Next steps**: Investigate why hello call takes longer than expected.</span></span>

<span data-ttu-id="94d63-240">Aşağıdaki örneğine hello bir bölüm çekirdek kaybına ve hello araştırma bitti adımları toofigure neden çıkışı gösterir.</span><span class="sxs-lookup"><span data-stu-id="94d63-240">hello following example shows a partition in quorum loss, and hello investigation steps done toofigure out why.</span></span> <span data-ttu-id="94d63-241">Durumunu almak için hello çoğaltmaları biri bir uyarı sistem durumu sahip.</span><span class="sxs-lookup"><span data-stu-id="94d63-241">One of hello replicas has a warning health state, so you get its health.</span></span> <span data-ttu-id="94d63-242">Bunu hello hizmet işlemi System.RAP tarafından bildirilen bir olayı beklenenden daha uzun sürer gösterir.</span><span class="sxs-lookup"><span data-stu-id="94d63-242">It shows that hello service operation takes longer than expected, an event reported by System.RAP.</span></span> <span data-ttu-id="94d63-243">Bu bilgileri alındıktan sonra hello sonraki adıma hello hizmet koduna toolook olduğu ve var. araştırın.</span><span class="sxs-lookup"><span data-stu-id="94d63-243">After this information is received, hello next step is toolook at hello service code and investigate there.</span></span> <span data-ttu-id="94d63-244">Bu durumda, hello **RunAsync** hello durum bilgisi olan hizmet uygulaması işlenmeyen bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="94d63-244">For this case, hello **RunAsync** implementation of hello stateful service throws an unhandled exception.</span></span> <span data-ttu-id="94d63-245">Merhaba çoğaltmaları geri dönüştürülmesi tüm yinelemeleri hello uyarı durumunda göremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94d63-245">hello replicas are recycling, so you may not see any replicas in hello warning state.</span></span> <span data-ttu-id="94d63-246">Alma hello sistem durumu yeniden deneyin ve farklılıklarını hello çoğaltma kimliği arayın</span><span class="sxs-lookup"><span data-stu-id="94d63-246">You can retry getting hello health state and look for any differences in hello replica ID.</span></span> <span data-ttu-id="94d63-247">Bazı durumlarda, hello deneme ipuçları verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94d63-247">In certain cases, hello retries can give you clues.</span></span>

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

<span data-ttu-id="94d63-248">Hatalı bir uygulama hello hello hata ayıklayıcı altında başlattığınızda hello Tanılama Olayları windows hello durum RunAsync göster:</span><span class="sxs-lookup"><span data-stu-id="94d63-248">When you start hello faulty application under hello debugger, hello diagnostic events windows show hello exception thrown from RunAsync:</span></span>

![Visual Studio 2015 Tanılama Olayları: RunAsync hatası fabric: / HelloWorldStatefulApplication.][1]

<span data-ttu-id="94d63-250">Visual Studio 2015 Tanılama Olayları: RunAsync hatası **fabric: / HelloWorldStatefulApplication**.</span><span class="sxs-lookup"><span data-stu-id="94d63-250">Visual Studio 2015 diagnostic events: RunAsync failure in **fabric:/HelloWorldStatefulApplication**.</span></span>

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a><span data-ttu-id="94d63-251">Çoğaltma kuyruğu dolu</span><span class="sxs-lookup"><span data-stu-id="94d63-251">Replication queue full</span></span>
<span data-ttu-id="94d63-252">**System.Replicator** hello çoğaltma sırası dolu olduğunda bir uyarı bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-252">**System.Replicator** reports a warning when hello replication queue is full.</span></span> <span data-ttu-id="94d63-253">Bir veya daha fazla ikincil çoğaltmaları yavaş tooacknowledge işlemler olduğundan hello üzerinde birincil, çoğaltma sırası genellikle tam haline gelir.</span><span class="sxs-lookup"><span data-stu-id="94d63-253">On hello primary, replication queue usually becomes full because one or more secondary replicas are slow tooacknowledge operations.</span></span> <span data-ttu-id="94d63-254">Merhaba hizmeti yavaş tooapply hello işlemleri olduğunda ikincil hello üzerinde bu genellikle gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="94d63-254">On hello secondary, this usually happens when hello service is slow tooapply hello operations.</span></span> <span data-ttu-id="94d63-255">Merhaba sırası dolu olduğunda hello uyarı temizlenir.</span><span class="sxs-lookup"><span data-stu-id="94d63-255">hello warning is cleared when hello queue is no longer full.</span></span>

* <span data-ttu-id="94d63-256">**SourceId**: System.Replicator</span><span class="sxs-lookup"><span data-stu-id="94d63-256">**SourceId**: System.Replicator</span></span>
* <span data-ttu-id="94d63-257">**Özellik**: **PrimaryReplicationQueueStatus** veya **SecondaryReplicationQueueStatus**hello çoğaltma rolü bağlı olarak</span><span class="sxs-lookup"><span data-stu-id="94d63-257">**Property**: **PrimaryReplicationQueueStatus** or **SecondaryReplicationQueueStatus**, depending on hello replica role</span></span>

### <a name="slow-naming-operations"></a><span data-ttu-id="94d63-258">Yavaş adlandırma işlemleri</span><span class="sxs-lookup"><span data-stu-id="94d63-258">Slow Naming operations</span></span>
<span data-ttu-id="94d63-259">**System.NamingService** adlandırma işlemi kabul edilebilir daha uzun sürerse, birincil Çoğaltmada durumu raporları.</span><span class="sxs-lookup"><span data-stu-id="94d63-259">**System.NamingService** reports health on its primary replica when a Naming operation takes longer than acceptable.</span></span> <span data-ttu-id="94d63-260">Adlandırma işlemleri örnekleri [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) veya [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span><span class="sxs-lookup"><span data-stu-id="94d63-260">Examples of Naming operations are [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) or [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span></span> <span data-ttu-id="94d63-261">Daha fazla yöntem FabricClient altında örneğin altında bulunabilir [hizmet yönetimi yöntemleri](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) veya [özellik yönetimi yöntemleri](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span><span class="sxs-lookup"><span data-stu-id="94d63-261">More methods can be found under FabricClient, for example under [service management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) or [property management methods](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).</span></span>

> [!NOTE]
> <span data-ttu-id="94d63-262">Merhaba adlandırma hizmeti hello Küme hizmeti adları tooa konumunda çözümler ve kullanıcıların toomanage hizmet adları ve özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="94d63-262">hello Naming service resolves service names tooa location in hello cluster and enables users toomanage service names and properties.</span></span> <span data-ttu-id="94d63-263">Bu hizmet bölümlenmiş bir Service Fabric kalıcı olur.</span><span class="sxs-lookup"><span data-stu-id="94d63-263">It is a Service Fabric partitioned persisted service.</span></span> <span data-ttu-id="94d63-264">Merhaba bölümden biri hello tüm Service Fabric adları ve Hizmetleri hakkında meta veriler içeren Authority Owner temsil eder.</span><span class="sxs-lookup"><span data-stu-id="94d63-264">One of hello partitions represents hello Authority Owner, which contains metadata about all Service Fabric names and services.</span></span> <span data-ttu-id="94d63-265">Merhaba Service Fabric adları hello hizmet Genişletilebilir olacak şekilde Name Owner bölümleri adlı eşlenen toodifferent bölümlerdir.</span><span class="sxs-lookup"><span data-stu-id="94d63-265">hello Service Fabric names are mapped toodifferent partitions, called Name Owner partitions, so hello service is extensible.</span></span> <span data-ttu-id="94d63-266">Daha fazla bilgi edinin [hizmet adlandırma](service-fabric-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="94d63-266">Read more about [Naming service](service-fabric-architecture.md).</span></span>
> 
> 

<span data-ttu-id="94d63-267">Bir adlandırma işlemi beklenenden daha uzun sürerse, hello işlemi hello uyarı raporda ile işaretlenir *hizmet bölüm adlandırma hello birincil çoğaltmasını hizmet hello işlemi*.</span><span class="sxs-lookup"><span data-stu-id="94d63-267">When a Naming operation takes longer than expected, hello operation is flagged with a Warning report on hello *primary replica of hello Naming service partition that serves hello operation*.</span></span> <span data-ttu-id="94d63-268">Merhaba işlem başarıyla tamamlanırsa hello uyarı temizlenir.</span><span class="sxs-lookup"><span data-stu-id="94d63-268">If hello operation completes successfully, hello Warning is cleared.</span></span> <span data-ttu-id="94d63-269">Merhaba işlemi bir hata ile tamamlarsa, hello sistem durumu raporu hello hatayla ilgili ayrıntılar içerir.</span><span class="sxs-lookup"><span data-stu-id="94d63-269">If hello operation completes with an error, hello health report includes details about hello error.</span></span>

* <span data-ttu-id="94d63-270">**SourceId**: System.NamingService</span><span class="sxs-lookup"><span data-stu-id="94d63-270">**SourceId**: System.NamingService</span></span>
* <span data-ttu-id="94d63-271">**Özellik**: önek ile başlayan **Duration_** ve hello yavaş işlemi ve hangi hello üzerinde işlem uygulanır hello Service Fabric adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="94d63-271">**Property**: Starts with prefix **Duration_** and identifies hello slow operation and hello Service Fabric name on which hello operation is applied.</span></span> <span data-ttu-id="94d63-272">Örneğin, hizmet adı doku oluşturma: / MyApp/MyService gereken çok uzun, hello özelliği Duration_AOCreateService.fabric:/MyApp/MyService.</span><span class="sxs-lookup"><span data-stu-id="94d63-272">For example, if create service at name fabric:/MyApp/MyService takes too long, hello property is Duration_AOCreateService.fabric:/MyApp/MyService.</span></span> <span data-ttu-id="94d63-273">AO noktaları toohello rolü hello adlandırma bölüm bu adı ve işlem için.</span><span class="sxs-lookup"><span data-stu-id="94d63-273">AO points toohello role of hello Naming partition for this name and operation.</span></span>
* <span data-ttu-id="94d63-274">**Sonraki adımlar**: onay neden hello adlandırma işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="94d63-274">**Next steps**: Check why hello Naming operation fails.</span></span> <span data-ttu-id="94d63-275">Her bir işlemin farklı kök neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="94d63-275">Each operation can have different root causes.</span></span> <span data-ttu-id="94d63-276">Örneğin, silme hizmet takılmış bir düğümde hello uygulama ana bilgisayarı hello servis kodu tooa kullanıcı hata nedeniyle bir düğümde kilitlenen tutar olduğundan.</span><span class="sxs-lookup"><span data-stu-id="94d63-276">For example, delete service may be stuck on a node because hello application host keeps crashing on a node due tooa user bug in hello service code.</span></span>

<span data-ttu-id="94d63-277">Aşağıdaki örneğine hello oluşturma hizmeti işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="94d63-277">hello following example shows a create service operation.</span></span> <span data-ttu-id="94d63-278">Merhaba işlemi yapılandırılan hello süreden daha uzun sürdü.</span><span class="sxs-lookup"><span data-stu-id="94d63-278">hello operation took longer than hello configured duration.</span></span> <span data-ttu-id="94d63-279">AO yeniden deneme sayısı ve iş tooNO gönderir.</span><span class="sxs-lookup"><span data-stu-id="94d63-279">AO retries and sends work tooNO.</span></span> <span data-ttu-id="94d63-280">HİÇBİR tamamlanmış hello son işlem zaman aşımı ile.</span><span class="sxs-lookup"><span data-stu-id="94d63-280">NO completed hello last operation with Timeout.</span></span> <span data-ttu-id="94d63-281">Bu durumda, hello aynı çoğaltma hello AO ve rol için birincil özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="94d63-281">In this case, hello same replica is primary for both hello AO and NO roles.</span></span>

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a><span data-ttu-id="94d63-282">DeployedApplication sistem durumu raporları</span><span class="sxs-lookup"><span data-stu-id="94d63-282">DeployedApplication system health reports</span></span>
<span data-ttu-id="94d63-283">**System.Hosting** hello yetkilisi dağıtılan varlıklar üzerinde.</span><span class="sxs-lookup"><span data-stu-id="94d63-283">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="activation"></a><span data-ttu-id="94d63-284">Etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="94d63-284">Activation</span></span>
<span data-ttu-id="94d63-285">Bir uygulama hello düğümde başarıyla etkinleştirildi System.Hosting olarak Tamam bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-285">System.Hosting reports as OK when an application has been successfully activated on hello node.</span></span> <span data-ttu-id="94d63-286">Aksi takdirde bir hata bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-286">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="94d63-287">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="94d63-287">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="94d63-288">**Özellik**: hello ürün sürümüne dahil olmak üzere etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="94d63-288">**Property**: Activation, including hello rollout version</span></span>
* <span data-ttu-id="94d63-289">**Sonraki adımlar**: neden hello etkinleştirme başarısız hello uygulamanın sağlıksız olduğunu gerekiyorsa araştırın.</span><span class="sxs-lookup"><span data-stu-id="94d63-289">**Next steps**: If hello application is unhealthy, investigate why hello activation failed.</span></span>

<span data-ttu-id="94d63-290">Merhaba aşağıdaki örnek başarılı etkinleştirme gösterir:</span><span class="sxs-lookup"><span data-stu-id="94d63-290">hello following example shows successful activation:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="94d63-291">İndir</span><span class="sxs-lookup"><span data-stu-id="94d63-291">Download</span></span>
<span data-ttu-id="94d63-292">**System.Hosting** hello uygulama paketin indirmesi başarısız olursa bir hata bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-292">**System.Hosting** reports an error if hello application package download fails.</span></span>

* <span data-ttu-id="94d63-293">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="94d63-293">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="94d63-294">**Özellik**:  **indirin:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="94d63-294">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="94d63-295">**Sonraki adımlar**: hello indirme hello düğümde neden başarısız araştırın.</span><span class="sxs-lookup"><span data-stu-id="94d63-295">**Next steps**: Investigate why hello download failed on hello node.</span></span>

## <a name="deployedservicepackage-system-health-reports"></a><span data-ttu-id="94d63-296">DeployedServicePackage sistem durumu raporları</span><span class="sxs-lookup"><span data-stu-id="94d63-296">DeployedServicePackage system health reports</span></span>
<span data-ttu-id="94d63-297">**System.Hosting** hello yetkilisi dağıtılan varlıklar üzerinde.</span><span class="sxs-lookup"><span data-stu-id="94d63-297">**System.Hosting** is hello authority on deployed entities.</span></span>

### <a name="service-package-activation"></a><span data-ttu-id="94d63-298">Hizmet paketi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="94d63-298">Service package activation</span></span>
<span data-ttu-id="94d63-299">System.Hosting Tamam hello hizmet paketi etkinleştirme hello düğümde başarılı olup olmadığını bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-299">System.Hosting reports as OK if hello service package activation on hello node is successful.</span></span> <span data-ttu-id="94d63-300">Aksi takdirde bir hata bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-300">Otherwise, it reports an error.</span></span>

* <span data-ttu-id="94d63-301">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="94d63-301">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="94d63-302">**Özellik**: etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="94d63-302">**Property**: Activation</span></span>
* <span data-ttu-id="94d63-303">**Sonraki adımlar**: neden hello etkinleştirme başarısız araştırın.</span><span class="sxs-lookup"><span data-stu-id="94d63-303">**Next steps**: Investigate why hello activation failed.</span></span>

### <a name="code-package-activation"></a><span data-ttu-id="94d63-304">Kod paketi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="94d63-304">Code package activation</span></span>
<span data-ttu-id="94d63-305">**System.Hosting** hello etkinleştirme başarılı olduğunda Tamam her kod paketi için raporlar.</span><span class="sxs-lookup"><span data-stu-id="94d63-305">**System.Hosting** reports as OK for each code package if hello activation is successful.</span></span> <span data-ttu-id="94d63-306">Merhaba etkinleştirme başarısız olursa, yapılandırılan bir uyarı bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-306">If hello activation fails, it reports a warning as configured.</span></span> <span data-ttu-id="94d63-307">Varsa **CodePackage** tooactivate başarısız olduğunda veya yapılandırılmış hello büyük bir hata ile sona erer **CodePackageHealthErrorThreshold**, barındırma bir hata bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-307">If **CodePackage** fails tooactivate or terminates with an error greater than hello configured **CodePackageHealthErrorThreshold**, hosting reports an error.</span></span> <span data-ttu-id="94d63-308">Bir hizmet paketi birden çok kod paketler içeriyorsa, bir etkinleştirme raporu her biri için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="94d63-308">If a service package contains multiple code packages, an activation report is generated for each one.</span></span>

* <span data-ttu-id="94d63-309">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="94d63-309">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="94d63-310">**Özellik**: kullanır hello önek **CodePackageActivation** ve hello kod paketi ve hello giriş noktası olarak hello adını içeren  **CodePackageActivation:* CodePackageName*:*SetupEntryPoint/EntryPoint*** (örneğin, **CodePackageActivation:Code:SetupEntryPoint**)</span><span class="sxs-lookup"><span data-stu-id="94d63-310">**Property**: Uses hello prefix **CodePackageActivation** and contains hello name of hello code package and hello entry point as **CodePackageActivation:*CodePackageName*:*SetupEntryPoint/EntryPoint*** (for example, **CodePackageActivation:Code:SetupEntryPoint**)</span></span>

### <a name="service-type-registration"></a><span data-ttu-id="94d63-311">Hizmet türü kayıt</span><span class="sxs-lookup"><span data-stu-id="94d63-311">Service type registration</span></span>
<span data-ttu-id="94d63-312">**System.Hosting** hello hizmet türü başarıyla kaydedilmişse Tamam bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-312">**System.Hosting** reports as OK if hello service type has been registered successfully.</span></span> <span data-ttu-id="94d63-313">Merhaba kayıt zamanında yapıldığında değildi hata raporları (kullanılarak yapılandırılan **ServiceTypeRegistrationTimeout**).</span><span class="sxs-lookup"><span data-stu-id="94d63-313">It reports an error if hello registration wasn't done in time (as configured by using **ServiceTypeRegistrationTimeout**).</span></span> <span data-ttu-id="94d63-314">Merhaba çalışma zamanı kapattıysanız, hello hizmet türü hello düğümden kaydı ve barındırma bir uyarı bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-314">If hello runtime is closed, hello service type is unregistered from hello node and Hosting reports a warning.</span></span>

* <span data-ttu-id="94d63-315">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="94d63-315">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="94d63-316">**Özellik**: kullanır hello önek **ServiceTypeRegistration** ve hello hizmet türü adı içerir (örneğin, **ServiceTypeRegistration:FileStoreServiceType**)</span><span class="sxs-lookup"><span data-stu-id="94d63-316">**Property**: Uses hello prefix **ServiceTypeRegistration** and contains hello service type name (for example, **ServiceTypeRegistration:FileStoreServiceType**)</span></span>

<span data-ttu-id="94d63-317">Aşağıdaki örnek hello sağlıklı dağıtılmış hizmet paketi gösterir:</span><span class="sxs-lookup"><span data-stu-id="94d63-317">hello following example shows a healthy deployed service package:</span></span>

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a><span data-ttu-id="94d63-318">İndir</span><span class="sxs-lookup"><span data-stu-id="94d63-318">Download</span></span>
<span data-ttu-id="94d63-319">**System.Hosting** hello hizmet paketin indirmesi başarısız olursa bir hata bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-319">**System.Hosting** reports an error if hello service package download fails.</span></span>

* <span data-ttu-id="94d63-320">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="94d63-320">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="94d63-321">**Özellik**:  **indirin:*RolloutVersion***</span><span class="sxs-lookup"><span data-stu-id="94d63-321">**Property**: **Download:*RolloutVersion***</span></span>
* <span data-ttu-id="94d63-322">**Sonraki adımlar**: hello indirme hello düğümde neden başarısız araştırın.</span><span class="sxs-lookup"><span data-stu-id="94d63-322">**Next steps**: Investigate why hello download failed on hello node.</span></span>

### <a name="upgrade-validation"></a><span data-ttu-id="94d63-323">Yükseltme doğrulaması</span><span class="sxs-lookup"><span data-stu-id="94d63-323">Upgrade validation</span></span>
<span data-ttu-id="94d63-324">**System.Hosting** hello yükseltme sırasında doğrulama başarısız veya hello varsa hello düğümde yükseltme başarısız olursa bir hata bildirir.</span><span class="sxs-lookup"><span data-stu-id="94d63-324">**System.Hosting** reports an error if validation during hello upgrade fails or if hello upgrade fails on hello node.</span></span>

* <span data-ttu-id="94d63-325">**SourceId**: System.Hosting</span><span class="sxs-lookup"><span data-stu-id="94d63-325">**SourceId**: System.Hosting</span></span>
* <span data-ttu-id="94d63-326">**Özellik**: kullanır hello önek **FabricUpgradeValidation** ve hello yükseltme sürümünü içerir</span><span class="sxs-lookup"><span data-stu-id="94d63-326">**Property**: Uses hello prefix **FabricUpgradeValidation** and contains hello upgrade version</span></span>
* <span data-ttu-id="94d63-327">**Açıklama**: işaret toohello hata ile karşılaşıldı</span><span class="sxs-lookup"><span data-stu-id="94d63-327">**Description**: Points toohello error encountered</span></span>

## <a name="next-steps"></a><span data-ttu-id="94d63-328">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="94d63-328">Next steps</span></span>
[<span data-ttu-id="94d63-329">Service Fabric sistem durumu raporlarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="94d63-329">View Service Fabric health reports</span></span>](service-fabric-view-entities-aggregated-health.md)

[<span data-ttu-id="94d63-330">Nasıl tooreport ve onay sistem durumu hizmeti</span><span class="sxs-lookup"><span data-stu-id="94d63-330">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="94d63-331">İzleme ve Hizmetleri yerel olarak tanılama</span><span class="sxs-lookup"><span data-stu-id="94d63-331">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="94d63-332">Service Fabric uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="94d63-332">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

