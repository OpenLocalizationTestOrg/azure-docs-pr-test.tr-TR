---
title: "Uygulama yükseltme sorunlarını giderme | Microsoft Docs"
description: "Bu makale, Service Fabric uygulaması ve bunların nasıl çözüleceği yükseltme geçici bazı yaygın sorunları ele alır."
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
ms.openlocfilehash: f7f6bc0c29e2b43fbc8e451c5a4a50110b78349e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-application-upgrades"></a><span data-ttu-id="8da27-103">Uygulama yükseltme ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="8da27-103">Troubleshoot application upgrades</span></span>
<span data-ttu-id="8da27-104">Bu makalede bazı Azure Service Fabric uygulama ve bunların nasıl çözüleceği yükseltme geçici yaygın sorunların çoğunu kapsar.</span><span class="sxs-lookup"><span data-stu-id="8da27-104">This article covers some of the common issues around upgrading an Azure Service Fabric application and how to resolve them.</span></span>

## <a name="troubleshoot-a-failed-application-upgrade"></a><span data-ttu-id="8da27-105">Başarısız uygulama yükseltme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="8da27-105">Troubleshoot a failed application upgrade</span></span>
<span data-ttu-id="8da27-106">Yükseltme başarısız olduğunda, çıktısını **Get-ServiceFabricApplicationUpgrade** komutu hata ayıklama için ek bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="8da27-106">When an upgrade fails, the output of the **Get-ServiceFabricApplicationUpgrade** command contains additional information for debugging the failure.</span></span>  <span data-ttu-id="8da27-107">Aşağıdaki listede, ek bilgiler nasıl kullanılabileceğini belirtir:</span><span class="sxs-lookup"><span data-stu-id="8da27-107">The following list specifies how the additional information can be used:</span></span>

1. <span data-ttu-id="8da27-108">Hata türünü tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8da27-108">Identify the failure type.</span></span>
2. <span data-ttu-id="8da27-109">Hatanın nedenini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="8da27-109">Identify the failure reason.</span></span>
3. <span data-ttu-id="8da27-110">Daha fazla araştırma için bir veya daha fazla başarısız olan bileşenleri yalıtma.</span><span class="sxs-lookup"><span data-stu-id="8da27-110">Isolate one or more failing components for further investigation.</span></span>

<span data-ttu-id="8da27-111">Service Fabric mi bakılmaksızın hatası algıladığında, bu bilgiler kullanılabilir **FailureAction** geri alma veya yükseltme askıya alma.</span><span class="sxs-lookup"><span data-stu-id="8da27-111">This information is available when Service Fabric detects the failure regardless of whether the **FailureAction** is to roll back or suspend the upgrade.</span></span>

### <a name="identify-the-failure-type"></a><span data-ttu-id="8da27-112">Hata türünü tanımlayın</span><span class="sxs-lookup"><span data-stu-id="8da27-112">Identify the failure type</span></span>
<span data-ttu-id="8da27-113">Çıktısı olarak **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** , bir yükseltme hatasına Service Fabric tarafından algılandı zaman damgası (UTC) olarak tanımlar ve  **FailureAction** tetiklendi.</span><span class="sxs-lookup"><span data-stu-id="8da27-113">In the output of **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** identifies the timestamp (in UTC) at which an upgrade failure was detected by Service Fabric and **FailureAction** was triggered.</span></span> <span data-ttu-id="8da27-114">**FailureReason** hatanın olası üç üst düzey nedenlerden biri tanımlar:</span><span class="sxs-lookup"><span data-stu-id="8da27-114">**FailureReason** identifies one of three potential high-level causes of the failure:</span></span>

1. <span data-ttu-id="8da27-115">UpgradeDomainTimeout - gösteren belirli bir yükseltme etki alanı tamamlanması çok uzun sürdü ve **UpgradeDomainTimeout** süresi doldu.</span><span class="sxs-lookup"><span data-stu-id="8da27-115">UpgradeDomainTimeout - Indicates that a particular upgrade domain took too long to complete and **UpgradeDomainTimeout** expired.</span></span>
2. <span data-ttu-id="8da27-116">OverallUpgradeTimeout - gösterir genel yükseltmenin tamamlanması çok uzun sürdü ve **UpgradeTimeout** süresi doldu.</span><span class="sxs-lookup"><span data-stu-id="8da27-116">OverallUpgradeTimeout - Indicates that the overall upgrade took too long to complete and **UpgradeTimeout** expired.</span></span>
3. <span data-ttu-id="8da27-117">Durum denetimi - bir güncelleştirme etki alanını yükselttikten sonra uygulamaya göre belirtilen sistem durumu ilkeleri sağlıksız kalan olduğunu gösterir ve **HealthCheckRetryTimeout** süresi doldu.</span><span class="sxs-lookup"><span data-stu-id="8da27-117">HealthCheck - Indicates that after upgrading an update domain, the application remained unhealthy according to the specified health policies and **HealthCheckRetryTimeout** expired.</span></span>

<span data-ttu-id="8da27-118">Yükseltme başarısız olur ve geri alma başladığında bu girişler yalnızca çıktıda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="8da27-118">These entries only show up in the output when the upgrade fails and starts rolling back.</span></span> <span data-ttu-id="8da27-119">Daha fazla bilgi hata türüne bağlı olarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8da27-119">Further information is displayed depending on the type of the failure.</span></span>

### <a name="investigate-upgrade-timeouts"></a><span data-ttu-id="8da27-120">Yükseltme zaman aşımı araştırın</span><span class="sxs-lookup"><span data-stu-id="8da27-120">Investigate upgrade timeouts</span></span>
<span data-ttu-id="8da27-121">Zaman aşımı hataları tarafından hizmet kullanılabilirliği sorunlarını yaygın hatalardır yükseltin.</span><span class="sxs-lookup"><span data-stu-id="8da27-121">Upgrade timeout failures are most commonly caused by service availability issues.</span></span> <span data-ttu-id="8da27-122">Bu paragraf aşağıdaki çıktı burada yeni kod sürümü başlatmak hizmet çoğaltmaları veya örnekleri başarısız yükseltme normaldir.</span><span class="sxs-lookup"><span data-stu-id="8da27-122">The output following this paragraph is typical of upgrades where service replicas or instances fail to start in the new code version.</span></span> <span data-ttu-id="8da27-123">**UpgradeDomainProgressAtFailure** alan tüm bekleyen yükseltme çalışmanın hatanın zamanında anlık görüntüsünü yakalar.</span><span class="sxs-lookup"><span data-stu-id="8da27-123">The **UpgradeDomainProgressAtFailure** field captures a snapshot of any pending upgrade work at the time of failure.</span></span>

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

<span data-ttu-id="8da27-124">Bu örnekte, yükseltme başarısız yükseltme etki alanında *MYUD1* ve iki bölüm (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* ve *4b43f4d8-b26b-424e-9307-7a7a62e79750*) takılmış.</span><span class="sxs-lookup"><span data-stu-id="8da27-124">In this example, the upgrade failed at upgrade domain *MYUD1* and two partitions (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* and *4b43f4d8-b26b-424e-9307-7a7a62e79750*) were stuck.</span></span> <span data-ttu-id="8da27-125">Çalışma zamanı birincil çoğaltmalara yerleştiremedi çünkü bölümleri takılmış (*WaitForPrimaryPlacement*) hedef düğümleri üzerinde *Düğüm1* ve *Düğüm4*.</span><span class="sxs-lookup"><span data-stu-id="8da27-125">The partitions were stuck because the runtime was unable to place primary replicas (*WaitForPrimaryPlacement*) on target nodes *Node1* and *Node4*.</span></span>

<span data-ttu-id="8da27-126">**Get-ServiceFabricNode** komutu, bu iki düğüm yükseltme etki alanında olduğunu doğrulamak için kullanılabilir *MYUD1*.</span><span class="sxs-lookup"><span data-stu-id="8da27-126">The **Get-ServiceFabricNode** command can be used to verify that these two nodes are in upgrade domain *MYUD1*.</span></span> <span data-ttu-id="8da27-127">*UpgradePhase* diyor *PostUpgradeSafetyCheck*, yükseltme etki alanındaki tüm düğümleri yükseltme işlemi tamamlandıktan sonra bu güvenlik denetimleri yaşanan anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8da27-127">The *UpgradePhase* says *PostUpgradeSafetyCheck*, which means that these safety checks are occurring after all nodes in the upgrade domain have finished upgrading.</span></span> <span data-ttu-id="8da27-128">Bu bilgiler, uygulama kodu yeni sürümü ile olası bir sorunu işaret eder.</span><span class="sxs-lookup"><span data-stu-id="8da27-128">All this information points to a potential issue with the new version of the application code.</span></span> <span data-ttu-id="8da27-129">En yaygın sorunları, açın veya birincil kod yollarının yükseltmesine hizmet hatalardır.</span><span class="sxs-lookup"><span data-stu-id="8da27-129">The most common issues are service errors in the open or promotion to primary code paths.</span></span>

<span data-ttu-id="8da27-130">Bir *UpgradePhase* , *PreUpgradeSafetyCheck* gerçekleştirilip gerçekleştirilmediğine önce yükseltme etki alanını hazırlama sorunları vardı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8da27-130">An *UpgradePhase* of *PreUpgradeSafetyCheck* means there were issues preparing the upgrade domain before it was performed.</span></span> <span data-ttu-id="8da27-131">En yaygın sorunları bu durumda hizmet kapatma ya da birincil kod yollarından indirgeme hatalardır.</span><span class="sxs-lookup"><span data-stu-id="8da27-131">The most common issues in this case are service errors in the close or demotion from primary code paths.</span></span>

<span data-ttu-id="8da27-132">Geçerli **UpgradeState** olan *RollingBackCompleted*, özgün yükseltmeyi geri alma ile gerçekleştirilen gerekir böylece **FailureAction**, hangi otomatik olarak toplama hata sonrasında yükseltme yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="8da27-132">The current **UpgradeState** is *RollingBackCompleted*, so the original upgrade must have been performed with a rollback **FailureAction**, which automatically rolled back the upgrade upon failure.</span></span> <span data-ttu-id="8da27-133">Özgün yükseltme el ile gerçekleştirdiyseniz **FailureAction**, sonra da yükseltme yerine canlı izin vermek için askıya alınmış durumda uygulamayı hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="8da27-133">If the original upgrade was performed with a manual **FailureAction**, then the upgrade would instead be in a suspended state to allow live debugging of the application.</span></span>

### <a name="investigate-health-check-failures"></a><span data-ttu-id="8da27-134">Sistem durumu denetimi hatalarını Araştır</span><span class="sxs-lookup"><span data-stu-id="8da27-134">Investigate health check failures</span></span>
<span data-ttu-id="8da27-135">Sistem durumu denetimi hataları bir yükseltme etki alanındaki tüm düğümleri yükseltme ve tüm güvenlik denetimleri geçirme işlemini tamamladıktan sonra oluşabilecek çeşitli sorunları tarafından tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="8da27-135">Health check failures can be triggered by various issues that can happen after all nodes in an upgrade domain finish upgrading and passing all safety checks.</span></span> <span data-ttu-id="8da27-136">Bu paragraf aşağıdaki çıktı yükseltme bir hata nedeniyle başarısız durumu denetimleri normaldir.</span><span class="sxs-lookup"><span data-stu-id="8da27-136">The output following this paragraph is typical of an upgrade failure due to failed health checks.</span></span> <span data-ttu-id="8da27-137">**UnhealthyEvaluations** alan belirtilen göre yükseltme zamanda başarısız durumu denetimleri görüntüsünü yakalar [sistem durumu ilkesi](service-fabric-health-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8da27-137">The **UnhealthyEvaluations** field captures a snapshot of health checks that failed at the time of the upgrade according to the specified [health policy](service-fabric-health-introduction.md).</span></span>

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

<span data-ttu-id="8da27-138">Sistem durumu denetimi hataları araştırılıyor ilk Service Fabric sistem durumu modeli bilinmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8da27-138">Investigating health check failures first requires an understanding of the Service Fabric health model.</span></span> <span data-ttu-id="8da27-139">Ancak bile bu tür bir ayrıntılı anlama olmadan, iki hizmet sağlıksız olduğunu görebiliriz: *fabric: / DemoApp/Svc3* ve *fabric: / DemoApp/Svc2*, hata sistem durumu raporlarının ("InjectedFault" ile birlikte Bu durumda).</span><span class="sxs-lookup"><span data-stu-id="8da27-139">But even without such an in-depth understanding, we can see that two services are unhealthy: *fabric:/DemoApp/Svc3* and *fabric:/DemoApp/Svc2*, along with the error health reports ("InjectedFault" in this case).</span></span> <span data-ttu-id="8da27-140">Bu örnekte, iki dışı dört Hizmetleri %0 sağlıksız varsayılan hedef olduğu sağlıksız, (*MaxPercentUnhealthyServices*).</span><span class="sxs-lookup"><span data-stu-id="8da27-140">In this example, two out of four services are unhealthy, which is below the default target of 0% unhealthy (*MaxPercentUnhealthyServices*).</span></span>

<span data-ttu-id="8da27-141">Yükseltme sırasında başarısız olan belirterek askıya alındı bir **FailureAction** yükseltme başlatırken elle.</span><span class="sxs-lookup"><span data-stu-id="8da27-141">The upgrade was suspended upon failing by specifying a **FailureAction** of manual when starting the upgrade.</span></span> <span data-ttu-id="8da27-142">Bu mod başka eylemi gerçekleştirmeden önce başarısız durumda Canlı sistem araştırmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="8da27-142">This mode allows us to investigate the live system in the failed state before taking any further action.</span></span>

### <a name="recover-from-a-suspended-upgrade"></a><span data-ttu-id="8da27-143">Askıya alınmış bir yükseltmeyi kurtarmak</span><span class="sxs-lookup"><span data-stu-id="8da27-143">Recover from a suspended upgrade</span></span>
<span data-ttu-id="8da27-144">Bir geri alma ile **FailureAction**, yükseltme otomatik olarak geri başarısız olan temel alındığında olmadığından gerekli hiçbir kurtarma yok.</span><span class="sxs-lookup"><span data-stu-id="8da27-144">With a rollback **FailureAction**, there is no recovery needed since the upgrade automatically rolls back upon failing.</span></span> <span data-ttu-id="8da27-145">El ile **FailureAction**, çeşitli kurtarma seçenekler vardır:</span><span class="sxs-lookup"><span data-stu-id="8da27-145">With a manual **FailureAction**, there are several recovery options:</span></span>

1.  <span data-ttu-id="8da27-146">Tetikleyici bir geri alma</span><span class="sxs-lookup"><span data-stu-id="8da27-146">trigger a rollback</span></span>
2. <span data-ttu-id="8da27-147">Yükseltme geri kalanı el ile devam edin</span><span class="sxs-lookup"><span data-stu-id="8da27-147">Proceed through the remainder of the upgrade manually</span></span>
3. <span data-ttu-id="8da27-148">İzlenen yükseltmeyi sürdürün</span><span class="sxs-lookup"><span data-stu-id="8da27-148">Resume the monitored upgrade</span></span>

<span data-ttu-id="8da27-149">**Başlangıç ServiceFabricApplicationRollback** komutu uygulama geri başlatmak için herhangi bir zamanda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8da27-149">The **Start-ServiceFabricApplicationRollback** command can be used at any time to start rolling back the application.</span></span> <span data-ttu-id="8da27-150">Komut başarıyla döndüğünde, geri alma isteği sistemde kayıtlı ve kısa süre içinde bundan sonra başlatır.</span><span class="sxs-lookup"><span data-stu-id="8da27-150">Once the command returns successfully, the rollback request has been registered in the system and starts shortly thereafter.</span></span>

<span data-ttu-id="8da27-151">**Resume-ServiceFabricApplicationUpgrade** komutu, yükseltme geri kalanı el ile devam etmek için kullanılabilir bir seferde bir yükseltme etki alanı.</span><span class="sxs-lookup"><span data-stu-id="8da27-151">The **Resume-ServiceFabricApplicationUpgrade** command can be used to proceed through the remainder of the upgrade manually, one upgrade domain at a time.</span></span> <span data-ttu-id="8da27-152">Bu modda, yalnızca güvenlik denetimleri sistem tarafından gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8da27-152">In this mode, only safety checks are performed by the system.</span></span> <span data-ttu-id="8da27-153">Daha fazla sistem durumu denetimleri yapılır.</span><span class="sxs-lookup"><span data-stu-id="8da27-153">No more health checks are performed.</span></span> <span data-ttu-id="8da27-154">Bu komut yalnızca olabilir kullanılır *UpgradeState* gösterir *RollingForwardPending*, başka bir deyişle, geçerli yükseltme etki alanı yükseltmeyi tamamladı. ancak bir sonraki (Bekleyen) başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="8da27-154">This command can only be used when the *UpgradeState* shows *RollingForwardPending*, which means that the current upgrade domain has finished upgrading but the next one has not started (pending).</span></span>

<span data-ttu-id="8da27-155">**Güncelleştirme ServiceFabricApplicationUpgrade** komutu, her iki güvenlik izlenen yükseltmeye devam etmek için kullanılabilir ve sistem durumu gerçekleştirilen denetler.</span><span class="sxs-lookup"><span data-stu-id="8da27-155">The **Update-ServiceFabricApplicationUpgrade** command can be used to resume the monitored upgrade with both safety and health checks being performed.</span></span>

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

<span data-ttu-id="8da27-156">Yükseltme devam eder burada son askıya alındı yükseltme etki alanı ve aynı parametreleri ve önce sistem durumu ilkeleri olarak yükseltme kullanın.</span><span class="sxs-lookup"><span data-stu-id="8da27-156">The upgrade continues from the upgrade domain where it was last suspended and use the same upgrade parameters and health policies as before.</span></span> <span data-ttu-id="8da27-157">Yükseltme devam ettiğinde gerekirse, tüm yükseltme parametreleri ve yukarıdaki çıktıda gösterilen sistem durumu ilkeleri aynı komutta değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="8da27-157">If needed, any of the upgrade parameters and health policies shown in the preceding output can be changed in the same command when the upgrade resumes.</span></span> <span data-ttu-id="8da27-158">Bu örnekte, izlenen modunda, parametreleri ve değişmeden sistem durumu ilkeleri ile yükseltme devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="8da27-158">In this example, the upgrade was resumed in Monitored mode, with the parameters and the health policies unchanged.</span></span>

## <a name="further-troubleshooting"></a><span data-ttu-id="8da27-159">Daha fazla sorun giderme</span><span class="sxs-lookup"><span data-stu-id="8da27-159">Further troubleshooting</span></span>
### <a name="service-fabric-is-not-following-the-specified-health-policies"></a><span data-ttu-id="8da27-160">Service Fabric belirtilen sistem durumu ilkeleri aşağıdaki değil</span><span class="sxs-lookup"><span data-stu-id="8da27-160">Service Fabric is not following the specified health policies</span></span>
<span data-ttu-id="8da27-161">Olası neden 1:</span><span class="sxs-lookup"><span data-stu-id="8da27-161">Possible Cause 1:</span></span>

<span data-ttu-id="8da27-162">Service Fabric sistem durumu değerlendirmesi için (örneğin, çoğaltmalar, bölümler ve Hizmetler) varlıkların gerçek sayılar tüm yüzdeleri çevirir ve her zaman tüm varlıklara yukarı yuvarlar.</span><span class="sxs-lookup"><span data-stu-id="8da27-162">Service Fabric translates all percentages into actual numbers of entities (for example, replicas, partitions, and services) for health evaluation and always rounds up to whole entities.</span></span> <span data-ttu-id="8da27-163">Örneğin, maksimum *MaxPercentUnhealthyReplicasPerPartition* % 21 olduğunu ve beş çoğaltmalar, en fazla iki sağlıksız çoğaltmaları Service Fabric sağlar (diğer bir deyişle,`Math.Ceiling (5*0.21)`).</span><span class="sxs-lookup"><span data-stu-id="8da27-163">For example, if the maximum *MaxPercentUnhealthyReplicasPerPartition* is 21% and there are five replicas, then Service Fabric allows up to two unhealthy replicas (that is,`Math.Ceiling (5*0.21)`).</span></span> <span data-ttu-id="8da27-164">Bu nedenle, sistem durumu ilkeleri uygun şekilde ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8da27-164">Thus, health policies should be set accordingly.</span></span>

<span data-ttu-id="8da27-165">Olası neden 2:</span><span class="sxs-lookup"><span data-stu-id="8da27-165">Possible Cause 2:</span></span>

<span data-ttu-id="8da27-166">Sistem durumu ilkeleri toplam Hizmetleri ve özgü olmayan hizmet örnekleri yüzdelerini bakımından belirtilir.</span><span class="sxs-lookup"><span data-stu-id="8da27-166">Health policies are specified in terms of percentages of total services and not specific service instances.</span></span> <span data-ttu-id="8da27-167">Örneğin, bir uygulama dört varsa, yükseltme önce hizmeti D sağlıksız olduğu ancak uygulama için çok az etkisi olan hizmet örnekleri A, B, C ve D.</span><span class="sxs-lookup"><span data-stu-id="8da27-167">For example, before an upgrade, if an application has four service instances A, B, C, and D, where service D is unhealthy but with little impact to the application.</span></span> <span data-ttu-id="8da27-168">Yükseltme sırasında bilinen sağlıksız Hizmeti D yoksay ve parametre kümesini istiyoruz *MaxPercentUnhealthyServices* yalnızca A varsayılarak % 25 B ve C sağlıklı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8da27-168">We want to ignore the known unhealthy service D during upgrade and set the parameter *MaxPercentUnhealthyServices* to be 25%, assuming only A, B, and C need to be healthy.</span></span>

<span data-ttu-id="8da27-169">C bozulur sırada ancak, yükseltme sırasında D sağlıklı duruma gelebilir.</span><span class="sxs-lookup"><span data-stu-id="8da27-169">However, during the upgrade, D may become healthy while C becomes unhealthy.</span></span> <span data-ttu-id="8da27-170">Yalnızca %25 Hizmetleri sağlıklı olduğundan yükseltme yine de başarılı.</span><span class="sxs-lookup"><span data-stu-id="8da27-170">The upgrade would still succeed because only 25% of the services are unhealthy.</span></span> <span data-ttu-id="8da27-171">Ancak, beklenmedik bir şekilde yerine D. sağlıklı olmadığını C nedeniyle beklenmeyen hataları neden Bu durumda, D, A'dan farklı hizmet türü olarak modellenmesi gerekir B ve c Sistem durumu ilkeleri hizmet türü belirtilmiş olduğundan, farklı sağlıksız yüzde eşikleri farklı hizmetlerine uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="8da27-171">However, it might result in unanticipated errors due to C being unexpectedly unhealthy instead of D. In this situation, D should be modeled as a different service type from A, B, and C. Since health policies are specified per service type, different unhealthy percentage thresholds can be applied to different services.</span></span> 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-the-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a><span data-ttu-id="8da27-172">Uygulama yükseltme için bir sistem durumu ilkesi belirtmedi ancak yükseltme hala hiçbir zaman belirtilen bazı zaman aşımlarını başarısız</span><span class="sxs-lookup"><span data-stu-id="8da27-172">I did not specify a health policy for application upgrade, but the upgrade still fails for some time-outs that I never specified</span></span>
<span data-ttu-id="8da27-173">Sistem durumu ilkeleri zaman olmayan yükseltme isteği, bunlar gelen alınır sağlanan *ApplicationManifest.xml* geçerli uygulama sürümü.</span><span class="sxs-lookup"><span data-stu-id="8da27-173">When health policies aren't provided to the upgrade request, they are taken from the *ApplicationManifest.xml* of the current application version.</span></span> <span data-ttu-id="8da27-174">Örneğin, sürüm 1.0 sürüm 2.0, uygulama sistem durumu ilkeleri için sürüm 1.0 için belirtilen uygulama X yükseltiyorsanız kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8da27-174">For example, if you're upgrading Application X from version 1.0 to version 2.0, application health policies specified for in version 1.0 are used.</span></span> <span data-ttu-id="8da27-175">Farklı sistem durumu ilkesi yükseltme için kullanılıp kullanılmayacağını ilke, uygulama yükseltme API çağrısı bir parçası olarak belirtilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="8da27-175">If a different health policy should be used for the upgrade, then the policy needs to be specified as part of the application upgrade API call.</span></span> <span data-ttu-id="8da27-176">API çağrısı bir parçası olarak belirtilen ilkeleri, yalnızca yükseltme sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="8da27-176">The policies specified as part of the API call only apply during the upgrade.</span></span> <span data-ttu-id="8da27-177">Yükseltme tamamlandıktan sonra ilkeleri belirtilen *ApplicationManifest.xml* kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8da27-177">Once the upgrade is complete, the policies specified in the *ApplicationManifest.xml* are used.</span></span>

### <a name="incorrect-time-outs-are-specified"></a><span data-ttu-id="8da27-178">Hatalı zaman aşımlarını belirtilen</span><span class="sxs-lookup"><span data-stu-id="8da27-178">Incorrect time-outs are specified</span></span>
<span data-ttu-id="8da27-179">Zaman aşımlarını tutarsız ayarladığınızda ne olduğu hakkında hiç merak ettiniz.</span><span class="sxs-lookup"><span data-stu-id="8da27-179">You may have wondered about what happens when time-outs are set inconsistently.</span></span> <span data-ttu-id="8da27-180">Örneğin, olabilir bir *UpgradeTimeout* bu küçük *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="8da27-180">For example, you may have an *UpgradeTimeout* that's less than the *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="8da27-181">Yanıtı bir hata döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8da27-181">The answer is that an error is returned.</span></span> <span data-ttu-id="8da27-182">Hatalar varsa döndürülür *UpgradeDomainTimeout* toplamını'dan küçük *HealthCheckWaitDuration* ve *HealthCheckRetryTimeout*, veya  *UpgradeDomainTimeout* toplamını'dan küçük *HealthCheckWaitDuration* ve *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="8da27-182">Errors are returned if the *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckRetryTimeout*, or if *UpgradeDomainTimeout* is less than the sum of *HealthCheckWaitDuration* and *HealthCheckStableDuration*.</span></span>

### <a name="my-upgrades-are-taking-too-long"></a><span data-ttu-id="8da27-183">My yükseltmeler çok uzun sürüyor</span><span class="sxs-lookup"><span data-stu-id="8da27-183">My upgrades are taking too long</span></span>
<span data-ttu-id="8da27-184">Zaman tamamlamak bir yükseltme için sistem durumu denetimlerinin ve belirtilen zaman aşımlarını bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8da27-184">The time for an upgrade to complete depends on the health checks and time-outs specified.</span></span> <span data-ttu-id="8da27-185">Sistem durumu denetimlerinin ve zaman aşımlarını kopyalama, dağıtma ve uygulama Sabitle için gereken süreyi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8da27-185">Health checks and time-outs depend on how long it takes to copy, deploy, and stabilize the application.</span></span> <span data-ttu-id="8da27-186">Nedenle ölçülü uzun zaman aşımlarını başlangıç öneririz zaman aşımlarını çok agresif olan başarısız yükseltme anlamına gelebilir.</span><span class="sxs-lookup"><span data-stu-id="8da27-186">Being too aggressive with time-outs might mean more failed upgrades, so we recommend starting conservatively with longer time-outs.</span></span>

<span data-ttu-id="8da27-187">Zaman aşımları yükseltme süreleri ile nasıl etkileşim hızlı Yenileyici şöyledir:</span><span class="sxs-lookup"><span data-stu-id="8da27-187">Here's a quick refresher on how the time-outs interact with the upgrade times:</span></span>

<span data-ttu-id="8da27-188">Bir yükseltme etki alanına tamamlayamıyor için yükseltme daha hızlı bir şekilde *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span><span class="sxs-lookup"><span data-stu-id="8da27-188">Upgrades for an upgrade domain cannot complete faster than *HealthCheckWaitDuration* + *HealthCheckStableDuration*.</span></span>

<span data-ttu-id="8da27-189">Yükseltme hatası gerçekleşemez daha hızlı bir şekilde *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span><span class="sxs-lookup"><span data-stu-id="8da27-189">Upgrade failure cannot occur faster than *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.</span></span>

<span data-ttu-id="8da27-190">Yükseltme etki alanı için yükseltme süresi sınırlıdır *UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="8da27-190">The upgrade time for an upgrade domain is limited by *UpgradeDomainTimeout*.</span></span>  <span data-ttu-id="8da27-191">Varsa *HealthCheckRetryTimeout* ve *HealthCheckStableDuration* hem de sıfır olması ve yükseltme sonunda üzerindezamanaşımınauğruyorsonrauygulamadurumunugeriveİlerigeçiştutar*UpgradeDomainTimeout*.</span><span class="sxs-lookup"><span data-stu-id="8da27-191">If *HealthCheckRetryTimeout* and *HealthCheckStableDuration* are both non-zero and the health of the application keeps switching back and forth, then the upgrade eventually times out on *UpgradeDomainTimeout*.</span></span> <span data-ttu-id="8da27-192">*UpgradeDomainTimeout* geçerli yükseltme etki alanı başlar için bir kez yükseltme sayım başlatır.</span><span class="sxs-lookup"><span data-stu-id="8da27-192">*UpgradeDomainTimeout* starts counting down once the upgrade for the current upgrade domain begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8da27-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8da27-193">Next steps</span></span>
<span data-ttu-id="8da27-194">[Uygulama kullanarak Visual Studio yükseltme](service-fabric-application-upgrade-tutorial.md) Visual Studio kullanarak bir uygulama yükseltme yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="8da27-194">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="8da27-195">[Uygulama Powershell kullanarak yükseltme](service-fabric-application-upgrade-tutorial-powershell.md) PowerShell kullanarak bir uygulama yükseltme yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="8da27-195">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="8da27-196">Uygulamanızı kullanarak yükseltme nasıl kontrol [yükseltme parametreleri](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="8da27-196">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="8da27-197">Uygulama yükseltme nasıl kullanılacağını öğrenerek uyumlu hale getirmek [veri seri hale getirme](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="8da27-197">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="8da27-198">Gelişmiş işlevselliği başvurarak uygulamanızı yükseltirken kullanmayı öğrenin [Gelişmiş konular](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="8da27-198">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
