---
title: "aaaTroubleshooting uygulama yükseltmelerini | Microsoft Docs"
description: "Bu makalede bir Service Fabric uygulama yükseltme geçici bazı yaygın sorunları ele alır ve nasıl tooresolve bunları."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 19ad152e-ec50-4327-9f19-065c875c003c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 0f56fa61db9b4e32824623f162dc1bfe7fda0f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="08187-103">Uygulama yükseltme ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="08187-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="08187-104">Bu makalede bazı Azure Service Fabric uygulama yükseltme geçici hello yaygın sorunların çoğunu kapsar ve nasıl tooresolve bunları.</span><span class="sxs-lookup"><span data-stu-id="08187-104">This article covers some of hello common issues around upgrading an Azure Service Fabric application and how tooresolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="08187-105">Başarısız uygulama yükseltme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="08187-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="08187-106">Yükseltme başarısız olduğunda, hello hello çıktısını **Get-ServiceFabricApplicationUpgrade** komutu hello hata ayıklama için ek bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="08187-106">When an upgrade fails, hello output of hello **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging hello failure.</span></span>  <span data-ttu-id="08187-107">Merhaba aşağıdaki listede hello ek bilgiler nasıl kullanılabileceğini belirtir:</span><span class="sxs-lookup"><span data-stu-id="08187-107">hello following list specifies how hello additional information can be used:</span></span>

1. <span data-ttu-id="08187-108">Merhaba hatası türünü tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="08187-108">Identify hello failure type.</span></span>
2. <span data-ttu-id="08187-109">Merhaba hatanın nedenini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="08187-109">Identify hello failure reason.</span></span>
3. <span data-ttu-id="08187-110">Daha fazla araştırma için bir veya daha fazla başarısız olan bileşenleri yalıtma.</span><span class="sxs-lookup"><span data-stu-id="08187-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="08187-111">Service Fabric hello hatası bağımsız olarak, hello olup olmadığını algıladığında, bu bilgiler kullanılabilir **FailureAction** tooroll geri veya hello yükseltme askıya alın.</span><span class="sxs-lookup"><span data-stu-id="08187-111">This information is available when Service Fabric detects hello failure regardless of whether hello **FailureAction** is tooroll back or suspend hello upgrade.</span></span>

### <a name="identify-hello-failure-type"></a><span data-ttu-id="08187-112">Merhaba hatası türünü tanımlayın</span><span class="sxs-lookup"><span data-stu-id="08187-112">Identify hello failure type</span></span>
<span data-ttu-id="08187-113">Merhaba çıktısını içinde **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** , bir yükseltme hatasına Service Fabric tarafından algılandı hello zaman damgası (UTC) olarak tanımlar ve  **FailureAction** tetiklendi.</span><span class="sxs-lookup"><span data-stu-id="08187-113">In hello output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies hello timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="08187-114">**FailureReason** hello hatanın olası üç üst düzey nedenlerden biri tanımlar:</span><span class="sxs-lookup"><span data-stu-id="08187-114">**FailureReason** identifies one of three potential high-level causes of hello failure:</span></span>

1. <span data-ttu-id="08187-115">UpgradeDomainTimeout - gösteren belirli bir yükseltme etki alanı toocomplete çok uzun sürdü ve **UpgradeDomainTimeout** süresi doldu.</span><span class="sxs-lookup"><span data-stu-id="08187-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long toocomplete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="08187-116">OverallUpgradeTimeout - gösterir genel yükseltme Bu hello toocomplete çok uzun sürdü ve **UpgradeTimeout** süresi doldu.</span><span class="sxs-lookup"><span data-stu-id="08187-116">OverallUpgradeTimeout - Indicates that hello overall upgrade took too long toocomplete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="08187-117">Durum denetimi - belirten bir güncelleştirme etki alanını yükselttikten sonra Merhaba uygulaması sağlıksız kalan olduğunu toohello according belirtilen sistem durumu ilkeleri ve **HealthCheckRetryTimeout** süresi doldu.</span><span class="sxs-lookup"><span data-stu-id="08187-117">HealthCheck - Indicates that after upgrading an update domain, hello application remained unhealthy according toohello specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="08187-118">Hello yükseltme başarısız olur ve geri alma başladığında bu girişler yalnızca hello çıkışında görünür.</span><span class="sxs-lookup"><span data-stu-id="08187-118">These entries only show up in hello output when hello upgrade fails and starts rolling back.</span></span> <span data-ttu-id="08187-119">Daha fazla bilgi hello hatası hello türüne bağlı olarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="08187-119">Further information is displayed depending on hello type of hello failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="08187-120">Yükseltme zaman aşımı araştırın</span><span class="sxs-lookup"><span data-stu-id="08187-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="08187-121">Zaman aşımı hataları tarafından hizmet kullanılabilirliği sorunlarını yaygın hatalardır yükseltin.</span><span class="sxs-lookup"><span data-stu-id="08187-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="08187-122">Bu paragraf aşağıdaki hello çıkış nerede hizmet çoğaltmaları veya örnekleri toostart hello yeni kod sürümünde başarısız yükseltme normaldir.</span><span class="sxs-lookup"><span data-stu-id="08187-122">hello output following this paragraph is typical of upgrades where service replicas or instances fail toostart in hello new code version.</span></span> <span data-ttu-id="08187-123">Merhaba **UpgradeDomainProgressAtFailure** alan tüm bekleyen yükseltme çalışmanın hatanın hello zamanında anlık görüntüsünü yakalar.</span><span class="sxs-lookup"><span data-stu-id="08187-123">hello **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at hello time of failure.</span></span>

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                : fabric:/DemoApp
ApplicationTypeName            : DemoAppType
TargetApplicationTypeVersion   : v2
ApplicationParameters          : {}
StartTimestampUtc              : 4/14/2015 9:26:38 PM
FailureTimestampUtc            : 4/14/2015 9:27:05 PM
FailureReason                  : UpgradeDomainTimeout
UpgradeDomainProgressAtFailure : MYUD1

                                 NodeName            : Node4
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 744c8d9f-1d26-417e-a60e-cd48f5c098f0

                                 NodeName            : Node1
                                 UpgradePhase        : PostUpgradeSafetyCheck
                                 PendingSafetyChecks :
                                     WaitForPrimaryPlacement - PartitionId: 4b43f4d8-b26b-424e-9307-7a7a62e79750
UpgradeState                   : RollingBackCompleted
UpgradeDuration                : 00:00:46
CurrentUpgradeDomainDuration   : 00:00:00
NextUpgradeDomain              :
UpgradeDomainsStatus           : { "MYUD1" = "Completed";
                                 "MYUD2" = "Completed";
                                 "MYUD3" = "Completed" }
UpgradeKind                    : Rolling
RollingUpgradeMode             : UnmonitoredAuto
ForceRestart                   : False
UpgradeReplicaSetCheckTimeout  : 00:00:00
```

<span data-ttu-id="08187-124">Bu örnekte, hello yükseltme başarısız yükseltme etki alanında *MYUD1* ve iki bölüm (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* ve *4b43f4d8-b26b-424e-9307-7a7a62e79750*) takılmış.</span><span class="sxs-lookup"><span data-stu-id="08187-124">In this example, hello upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="08187-125">Merhaba bölümleri takılmış hello çalışma zamanı yüklenemiyor tooplace birincil çoğaltma olduğundan (*WaitForPrimaryPlacement*) hedef düğümleri üzerinde *Düğüm1* ve *Düğüm4*.</span><span class="sxs-lookup"><span data-stu-id="08187-125">hello partitions were stuck because hello runtime was unable tooplace primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="08187-126">Merhaba **Get-ServiceFabricNode** komutu, bu iki düğüm yükseltme etki alanında olduğundan kullanılan tooverify olabilir *MYUD1*.</span><span class="sxs-lookup"><span data-stu-id="08187-126">hello **Get-ServiceFabricNode** command can be used tooverify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="08187-127">Merhaba *UpgradePhase* diyor *PostUpgradeSafetyCheck*, hello yükseltme etki alanındaki tüm düğümleri yükseltme işlemi tamamlandıktan sonra bu güvenlik denetimleri yaşanan anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="08187-127">hello *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in hello upgrade domain have finished upgrading.</span></span> <span data-ttu-id="08187-128">Bu bilgiler hello uygulama kodunun hello yeni sürümüyle tooa olası sorunu işaret eder.</span><span class="sxs-lookup"><span data-stu-id="08187-128">All this information points tooa potential issue with hello new version of hello application code.</span></span> <span data-ttu-id="08187-129">Merhaba en sık karşılaşılan sorunları hello açık veya promosyon tooprimary kod yollarının hizmet hatalardır.</span><span class="sxs-lookup"><span data-stu-id="08187-129">hello most common issues are service errors in hello open or promotion tooprimary code paths.</span></span>

<span data-ttu-id="08187-130">Bir *UpgradePhase* , *PreUpgradeSafetyCheck* gerçekleştirilip gerçekleştirilmediğine önce hello yükseltme etki alanını hazırlama sorunları vardı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="08187-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing hello upgrade domain before it was performed.</span></span> <span data-ttu-id="08187-131">Merhaba en sık karşılaşılan sorunları bu durumda hizmet hello kapatın veya birincil kod yollarından indirgeme hatalardır.</span><span class="sxs-lookup"><span data-stu-id="08187-131">hello most common issues in this case are service errors in hello close or demotion from primary code paths.</span></span>

<span data-ttu-id="08187-132">Merhaba geçerli **UpgradeState** olan *RollingBackCompleted*, hello özgün yükseltmeyi geri alma ile gerçekleştirilen gerekir böylece **FailureAction**, hangi otomatik olarak hata sonrasında hello yükseltme geri alındı.</span><span class="sxs-lookup"><span data-stu-id="08187-132">hello current **UpgradeState** is *RollingBackCompleted*, so hello original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back hello upgrade upon failure.</span></span> <span data-ttu-id="08187-133">Merhaba özgün yükseltme el ile gerçekleştirdiyseniz **FailureAction**, sonra da hello yükseltme yerine bir hello uygulamasının hata ayıklama Canlı askıya alınma durumundaysa tooallow olacaktır.</span><span class="sxs-lookup"><span data-stu-id="08187-133">If hello original upgrade was performed with a manual **FailureAction**, then hello upgrade would instead be in a suspended state tooallow live debugging of hello application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="08187-134">Sistem durumu denetimi hatalarını Araştır</span><span class="sxs-lookup"><span data-stu-id="08187-134">Investigate health check failures</span></span>
<span data-ttu-id="08187-135">Sistem durumu denetimi hataları bir yükseltme etki alanındaki tüm düğümleri yükseltme ve tüm güvenlik denetimleri geçirme işlemini tamamladıktan sonra oluşabilecek çeşitli sorunları tarafından tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="08187-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="08187-136">Bu paragraf aşağıdaki hello çıktı toofailed durumu denetimleri nedeniyle yükseltme bir hatanın normaldir.</span><span class="sxs-lookup"><span data-stu-id="08187-136">hello output following this paragraph is typical of an upgrade failure due toofailed health checks.</span></span> <span data-ttu-id="08187-137">Merhaba **UnhealthyEvaluations** alan belirtilen toohello göre hello yükseltme hello aynı anda başarısız durumu denetimleri görüntüsünü yakalar [sistem durumu ilkesi](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="08187-137">hello **UnhealthyEvaluations** field captures a snapshot of health checks that failed at hello time of hello upgrade according toohello specified [health policy](service-fabric-health-introduction.md).</span></span>

```
PS D:\temp> Get-ServiceFabricApplicationUpgrade fabric:/DemoApp

ApplicationName                         : fabric:/DemoApp
ApplicationTypeName                     : DemoAppType
TargetApplicationTypeVersion            : v4
ApplicationParameters                   : {}
StartTimestampUtc                       : 4/24/2015 2:42:31 AM
UpgradeState                            : RollingForwardPending
UpgradeDuration                         : 00:00:27
CurrentUpgradeDomainDuration            : 00:00:27
NextUpgradeDomain                       : MYUD2
UpgradeDomainsStatus                    : { "MYUD1" = "Completed";
                                          "MYUD2" = "Pending";
                                          "MYUD3" = "Pending" }
UnhealthyEvaluations                    :
                                          Unhealthy services: 50% (2/4), ServiceType='PersistedServiceType', MaxPercentUnhealthyServices=0%.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc3', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='3a9911f6-a2e5-452d-89a8-09271e7e49a8', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

                                          Unhealthy service: ServiceName='fabric:/DemoApp/Svc2', AggregatedHealthState='Error'.

                                              Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                              Unhealthy partition: PartitionId='744c8d9f-1d26-417e-a60e-cd48f5c098f0', AggregatedHealthState='Error'.

                                                  Error event: SourceId='Replica', Property='InjectedFault'.

UpgradeKind                             : Rolling
RollingUpgradeMode                      : Monitored
FailureAction                           : Manual
ForceRestart                            : False
UpgradeReplicaSetCheckTimeout           : 49710.06:28:15
HealthCheckWaitDuration                 : 00:00:00
HealthCheckStableDuration               : 00:00:10
HealthCheckRetryTimeout                 : 00:00:10
UpgradeDomainTimeout                    : 10675199.02:48:05.4775807
UpgradeTimeout                          : 10675199.02:48:05.4775807
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :
```

<span data-ttu-id="08187-138">Sistem durumu denetimi hataları araştırılıyor ilk hello Service Fabric sistem durumu modeli bilinmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="08187-138">Investigating health check failures first requires an understanding of hello Service Fabric health model.</span></span> <span data-ttu-id="08187-139">Ancak bile bu tür bir ayrıntılı anlama olmadan, iki hizmet sağlıksız olduğunu görebiliriz: *fabric: / DemoApp/Svc3* ve *fabric: / DemoApp/Svc2*, hello hata durum raporu ("InjectedFault birlikte "Bu durumda).</span><span class="sxs-lookup"><span data-stu-id="08187-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with hello error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="08187-140">Bu örnekte, iki dışı dört Hizmetleri %0 sağlıksız hello varsayılan hedef olduğu sağlıksız, (*MaxPercentUnhealthyServices*).</span><span class="sxs-lookup"><span data-stu-id="08187-140">In this example, two out of four services are unhealthy, which is below hello default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="08187-141">Merhaba yükseltme sırasında başarısız olan belirterek askıya alındı bir **FailureAction** el ile olduğunda yükseltme hello başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="08187-141">hello upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting hello upgrade.</span></span> <span data-ttu-id="08187-142">Bu mod, başka bir eylem gerçekleştirmeden önce bize tooinvestigate hello Canlı sistem hello başarısız durumda sağlar.</span><span class="sxs-lookup"><span data-stu-id="08187-142">This mode allows us tooinvestigate hello live system in hello failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="08187-143">Askıya alınmış bir yükseltmeyi kurtarmak</span><span class="sxs-lookup"><span data-stu-id="08187-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="08187-144">Bir geri alma ile **FailureAction**, hello yükseltme otomatik olarak geri başarısız olan temel alındığında olmadığından gerekli hiçbir kurtarma yok.</span><span class="sxs-lookup"><span data-stu-id="08187-144">With a rollback **FailureAction**, there is no recovery needed since hello upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="08187-145">El ile **FailureAction**, çeşitli kurtarma seçenekler vardır:</span><span class="sxs-lookup"><span data-stu-id="08187-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="08187-146">Tetikleyici bir geri alma</span><span class="sxs-lookup"><span data-stu-id="08187-146">trigger a rollback</span></span>
2. <span data-ttu-id="08187-147">Merhaba yükseltme Hello kalanı el ile devam edin</span><span class="sxs-lookup"><span data-stu-id="08187-147">Proceed through hello remainder of hello upgrade manually</span></span>
3. <span data-ttu-id="08187-148">Yükseltme devam hello izlenen</span><span class="sxs-lookup"><span data-stu-id="08187-148">Resume hello monitored upgrade</span></span>

<span data-ttu-id="08187-149">Merhaba **başlangıç ServiceFabricApplicationRollback** Merhaba uygulaması geri hiçbir zaman toostart komutu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="08187-149">hello **Start-ServiceFabricApplicationRollback** command can be used at any time toostart rolling back hello application.</span></span> <span data-ttu-id="08187-150">Merhaba komutu başarıyla döndüğünde hello geri alma isteği hello sistemde kayıtlı ve kısa süre içinde bundan sonra başlar.</span><span class="sxs-lookup"><span data-stu-id="08187-150">Once hello command returns successfully, hello rollback request has been registered in hello system and starts shortly thereafter.</span></span>

<span data-ttu-id="08187-151">Merhaba **Resume-ServiceFabricApplicationUpgrade** komutu kullanılabilir hello hello kalanı aracılığıyla tooproceed yükseltme el ile bir seferde bir yükseltme etki alanı.</span><span class="sxs-lookup"><span data-stu-id="08187-151">hello **Resume-ServiceFabricApplicationUpgrade** command can be used tooproceed through hello remainder of hello upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="08187-152">Bu modda, yalnızca güvenlik denetimleri hello sistem tarafından gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="08187-152">In this mode, only safety checks are performed by hello system.</span></span> <span data-ttu-id="08187-153">Daha fazla sistem durumu denetimleri yapılır.</span><span class="sxs-lookup"><span data-stu-id="08187-153">No more health checks are performed.</span></span> <span data-ttu-id="08187-154">Bu komut yalnızca hello kullanılabilir *UpgradeState* gösterir *RollingForwardPending*, o hello geçerli yükseltme etki alanı başka bir deyişle, yükseltmeyi tamamladı. ancak hello sonraki bir (Bekleyen) başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="08187-154">This command can only be used when hello *UpgradeState* shows *RollingForwardPending*, which means that hello current upgrade domain has finished upgrading but hello next one has not started (pending).</span></span>

<span data-ttu-id="08187-155">Merhaba **güncelleştirme ServiceFabricApplicationUpgrade** kullanılan tooresume izlenen hello güvenlik ve sistem durumu denetimleri yükseltmeye olan yapılabilir komutu.</span><span class="sxs-lookup"><span data-stu-id="08187-155">hello **Update-ServiceFabricApplicationUpgrade** command can be used tooresume hello monitored upgrade with both safety and health checks being performed.</span></span>

```
PS D:\temp> Update-ServiceFabricApplicationUpgrade fabric:/DemoApp -UpgradeMode Monitored

UpgradeMode                             : Monitored
ForceRestart                            :
UpgradeReplicaSetCheckTimeout           :
FailureAction                           :
HealthCheckWaitDuration                 :
HealthCheckStableDuration               :
HealthCheckRetryTimeout                 :
UpgradeTimeout                          :
UpgradeDomainTimeout                    :
ConsiderWarningAsError                  :
MaxPercentUnhealthyPartitionsPerService :
MaxPercentUnhealthyReplicasPerPartition :
MaxPercentUnhealthyServices             :
MaxPercentUnhealthyDeployedApplications :
ServiceTypeHealthPolicyMap              :

PS D:\temp>
```

<span data-ttu-id="08187-156">Burada son askıya alındı hello yükseltme etki alanı ve aynı parametreleri ve önce sistem durumu ilkeleri olarak yükseltme kullanım hello Hello yükseltme devam eder.</span><span class="sxs-lookup"><span data-stu-id="08187-156">hello upgrade continues from hello upgrade domain where it was last suspended and use hello same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="08187-157">Gerekirse, tüm hello yükseltme parametreleri ve sistem durumu ilkeleri çıkış önceki hello gösterilen hello yükseltme devam ettiğinde aynı komut hello değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="08187-157">If needed, any of hello upgrade parameters and health policies shown in hello preceding output can be changed in hello same command when hello upgrade resumes.</span></span> <span data-ttu-id="08187-158">Bu örnekte, hello parametreleri ve değişmeden hello sistem durumu ilkeleri ile izlenen modda hello yükseltme devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="08187-158">In this example, hello upgrade was resumed in Monitored mode, with hello parameters and hello health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="08187-159">Daha fazla sorun giderme</span><span class="sxs-lookup"><span data-stu-id="08187-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a><span data-ttu-id="08187-160">Service Fabric belirtilen hello değil aşağıdaki sistem durumu ilkeleri</span><span class="sxs-lookup"><span data-stu-id="08187-160">Service Fabric is not following hello specified health policies</span></span>
<span data-ttu-id="08187-161">Olası neden 1:</span><span class="sxs-lookup"><span data-stu-id="08187-161">Possible Cause 1:</span></span>

<span data-ttu-id="08187-162">Service Fabric tüm yüzdeleri varlıkların (örneğin, çoğaltmalar, bölümler ve Hizmetler) gerçek sayılara için sistem durumu değerlendirmesi dönüşür ve her zaman toowhole varlıklar yuvarlar.</span><span class="sxs-lookup"><span data-stu-id="08187-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up toowhole entities.</span></span> <span data-ttu-id="08187-163">Örneğin, Merhaba, en fazla *MaxPercentUnhealthyReplicasPerPartition* % 21 olduğunu ve beş çoğaltmalar, Service Fabric tootwo sağlıksız çoğaltmaları yedeklemek sağlar (diğer bir deyişle,`Math.Ceiling (5*0.21)`).</span><span class="sxs-lookup"><span data-stu-id="08187-163">For example, if hello maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up tootwo unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="08187-164">Bu nedenle, sistem durumu ilkeleri uygun şekilde ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="08187-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="08187-165">Olası neden 2:</span><span class="sxs-lookup"><span data-stu-id="08187-165">Possible Cause 2:</span></span>

<span data-ttu-id="08187-166">Sistem durumu ilkeleri toplam Hizmetleri ve özgü olmayan hizmet örnekleri yüzdelerini bakımından belirtilir.</span><span class="sxs-lookup"><span data-stu-id="08187-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="08187-167">Örneğin, bir uygulama dört varsa, yükseltme önce hizmeti D sağlıksız olduğu ancak çok az etkisi toohello uygulamayla örnekleri A, B, C ve D, hizmet.</span><span class="sxs-lookup"><span data-stu-id="08187-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact toohello application.</span></span> <span data-ttu-id="08187-168">Yükseltme ve ayarlanmış hello parametre sırasında sağlıksız Hizmeti D bilinen tooignore hello istiyoruz *MaxPercentUnhealthyServices* toobe yalnızca A, B ve C varsayılarak % 25 toobe sağlıklı gerekir.</span><span class="sxs-lookup"><span data-stu-id="08187-168">We want tooignore hello known unhealthy service D during upgrade and set hello parameter *MaxPercentUnhealthyServices* toobe 25%, assuming only A, B, and C need toobe healthy.</span></span>

<span data-ttu-id="08187-169">C bozulur sırada ancak, hello yükseltme sırasında D sağlıklı duruma gelebilir.</span><span class="sxs-lookup"><span data-stu-id="08187-169">However, during hello upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="08187-170">yalnızca % 25'ini hello Hizmetleri sağlıklı olduğundan hello yükseltme yine de başarılı.</span><span class="sxs-lookup"><span data-stu-id="08187-170">hello upgrade would still succeed because only 25% of hello services are unhealthy.</span></span> <span data-ttu-id="08187-171">Ancak, tooC olması nedeniyle beklenmeyen hataları yerine D. beklenmedik bir şekilde sağlıksız neden Bu durumda, D, A'dan farklı hizmet türü olarak modellenmesi gerekir B ve c Sistem durumu ilkeleri hizmet türü belirtilmiş olduğundan, farklı sağlıksız yüzde eşikleri uygulanan toodifferent Hizmetleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="08187-171">However, it might result in unanticipated errors due tooC being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied toodifferent services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="08187-172">Uygulama yükseltme için bir sistem durumu ilkesi belirtmedi, ancak hiçbir zaman belirtilen bazı zaman aşımlarını hello yükseltme yine başarısız</span><span class="sxs-lookup"><span data-stu-id="08187-172">I did not specify a health policy for application upgrade, but hello upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="08187-173">Sistem durumu ilkeleri toohello yükseltme isteği sağlanmayan, hello alınır *ApplicationManifest.xml* hello geçerli uygulama sürümü.</span><span class="sxs-lookup"><span data-stu-id="08187-173">When health policies aren't provided toohello upgrade request, they are taken from hello *ApplicationManifest.xml* of hello current application version.</span></span> <span data-ttu-id="08187-174">Örneğin, uygulama X sürüm 1.0 tooversion 2.0 ' yükseltiyorsanız, sürüm 1.0 için belirtilen uygulama sistem durumu ilkeleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="08187-174">For example, if you're upgrading Application X from version 1.0 tooversion 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="08187-175">Farklı sistem durumu ilkesi hello yükseltme için kullanılması gereken hello İlkesi hello uygulama yükseltme API çağrısı bir parçası olarak belirtilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="08187-175">If a different health policy should be used for hello upgrade, then hello policy needs toobe specified as part of hello application upgrade API call.</span></span> <span data-ttu-id="08187-176">Merhaba hello API çağrısı bir parçası olarak belirtilen ilkeleri yalnızca hello yükseltme sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="08187-176">hello policies specified as part of hello API call only apply during hello upgrade.</span></span> <span data-ttu-id="08187-177">Merhaba yükseltme tamamlandıktan sonra hello ilkelerinde belirtilen hello *ApplicationManifest.xml* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="08187-177">Once hello upgrade is complete, hello policies specified in hello *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="08187-178">Hatalı zaman aşımlarını belirtilen</span><span class="sxs-lookup"><span data-stu-id="08187-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="08187-179">Zaman aşımlarını tutarsız ayarladığınızda ne olduğu hakkında hiç merak ettiniz.</span><span class="sxs-lookup"><span data-stu-id="08187-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="08187-180">Örneğin, olabilir bir *UpgradeTimeout* başlangıç değerinden küçük *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="08187-180">For example, you may have an *UpgradeTimeout* that's less than hello *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="08187-181">Merhaba yanıt bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="08187-181">hello answer is that an error is returned.</span></span> <span data-ttu-id="08187-182">Merhaba, hata döndürülür *UpgradeDomainTimeout* hello toplamını'dan küçük *HealthCheckWaitDuration* ve *HealthCheckRetryTimeout*, veya  *UpgradeDomainTimeout* hello toplamını'dan küçük *HealthCheckWaitDuration* ve *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="08187-182">Errors are returned if hello *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than hello sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="08187-183">My yükseltmeler çok uzun sürüyor</span><span class="sxs-lookup"><span data-stu-id="08187-183">My upgrades are taking too long</span></span>
<span data-ttu-id="08187-184">bir yükseltme toocomplete Hello süredir hello sistem durumu denetimlerinin ve belirtilen zaman aşımlarını bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="08187-184">hello time for an upgrade toocomplete depends on hello health checks and time-outs specified.</span></span> <span data-ttu-id="08187-185">Sistem durumu denetimlerinin ve zaman aşımlarını toocopy süreyi bağlıdır, dağıtmak ve Merhaba uygulaması Sabitle.</span><span class="sxs-lookup"><span data-stu-id="08187-185">Health checks and time-outs depend on how long it takes toocopy, deploy, and stabilize hello application.</span></span> <span data-ttu-id="08187-186">Nedenle ölçülü uzun zaman aşımlarını başlangıç öneririz zaman aşımlarını çok agresif olan başarısız yükseltme anlamına gelebilir.</span><span class="sxs-lookup"><span data-stu-id="08187-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="08187-187">Merhaba zaman aşımlarını hello yükseltme süreleri ile nasıl etkileşim hızlı Yenileyici şöyledir:</span><span class="sxs-lookup"><span data-stu-id="08187-187">Here's a quick refresher on how hello time-outs interact with hello upgrade times:</span></span>

<span data-ttu-id="08187-188">Bir yükseltme etki alanına tamamlayamıyor için yükseltme daha hızlı bir şekilde *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="08187-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="08187-189">Yükseltme hatası gerçekleşemez daha hızlı bir şekilde *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span><span class="sxs-lookup"><span data-stu-id="08187-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="08187-190">Merhaba yükseltme etki alanı için yükseltme süresi sınırlıdır *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="08187-190">hello upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="08187-191">Varsa *HealthCheckRetryTimeout* ve *HealthCheckStableDuration* her ikisi de sıfır olan ve hello uygulama hello durumunu tutar anahtarlama geri ve İleri hello yükseltme sonunda üzerindezamanaşımınauğruyorsonra *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="08187-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and hello health of hello application keeps switching back and forth, then hello upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="08187-192">*UpgradeDomainTimeout* başlar hello geçerli yükseltme etki alanı için bir kez sayım başlatır hello yükseltme.</span><span class="sxs-lookup"><span data-stu-id="08187-192">*UpgradeDomainTimeout* starts counting down once hello upgrade for hello current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08187-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08187-193">Next steps</span></span>
<span data-ttu-id="08187-194">[Uygulama kullanarak Visual Studio yükseltme](service-fabric-application-upgrade-tutorial.md) Visual Studio kullanarak bir uygulama yükseltme yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="08187-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="08187-195">[Uygulama Powershell kullanarak yükseltme](service-fabric-application-upgrade-tutorial-powershell.md) PowerShell kullanarak bir uygulama yükseltme yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="08187-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="08187-196">Uygulamanızı kullanarak yükseltme nasıl kontrol [yükseltme parametreleri](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="08187-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="08187-197">Uygulama yükseltme öğrenme tarafından uyumlu hale getirmek nasıl toouse [veri seri hale getirme](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="08187-197">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="08187-198">Uygulamanız çok başvurarak yükseltirken toouse işlevselliği nasıl Gelişmiş öğrenin[Gelişmiş konular](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="08187-198">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
