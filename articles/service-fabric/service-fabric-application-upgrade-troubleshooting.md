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
# <a name="troubleshoot-application-upgrades"></a>Uygulama yükseltme ile ilgili sorunları giderme
Bu makalede bazı Azure Service Fabric uygulama yükseltme geçici hello yaygın sorunların çoğunu kapsar ve nasıl tooresolve bunları.

## <a name="troubleshoot-a-failed-application-upgrade"></a>Başarısız uygulama yükseltme sorunlarını giderme
Yükseltme başarısız olduğunda, hello hello çıktısını **Get-ServiceFabricApplicationUpgrade** komutu hello hata ayıklama için ek bilgiler içerir.  Merhaba aşağıdaki listede hello ek bilgiler nasıl kullanılabileceğini belirtir:

1. Merhaba hatası türünü tanımlayın.
2. Merhaba hatanın nedenini belirleyin.
3. Daha fazla araştırma için bir veya daha fazla başarısız olan bileşenleri yalıtma.

Service Fabric hello hatası bağımsız olarak, hello olup olmadığını algıladığında, bu bilgiler kullanılabilir **FailureAction** tooroll geri veya hello yükseltme askıya alın.

### <a name="identify-hello-failure-type"></a>Merhaba hatası türünü tanımlayın
Merhaba çıktısını içinde **Get-ServiceFabricApplicationUpgrade**, **FailureTimestampUtc** , bir yükseltme hatasına Service Fabric tarafından algılandı hello zaman damgası (UTC) olarak tanımlar ve  **FailureAction** tetiklendi. **FailureReason** hello hatanın olası üç üst düzey nedenlerden biri tanımlar:

1. UpgradeDomainTimeout - gösteren belirli bir yükseltme etki alanı toocomplete çok uzun sürdü ve **UpgradeDomainTimeout** süresi doldu.
2. OverallUpgradeTimeout - gösterir genel yükseltme Bu hello toocomplete çok uzun sürdü ve **UpgradeTimeout** süresi doldu.
3. Durum denetimi - belirten bir güncelleştirme etki alanını yükselttikten sonra Merhaba uygulaması sağlıksız kalan olduğunu toohello according belirtilen sistem durumu ilkeleri ve **HealthCheckRetryTimeout** süresi doldu.

Hello yükseltme başarısız olur ve geri alma başladığında bu girişler yalnızca hello çıkışında görünür. Daha fazla bilgi hello hatası hello türüne bağlı olarak görüntülenir.

### <a name="investigate-upgrade-timeouts"></a>Yükseltme zaman aşımı araştırın
Zaman aşımı hataları tarafından hizmet kullanılabilirliği sorunlarını yaygın hatalardır yükseltin. Bu paragraf aşağıdaki hello çıkış nerede hizmet çoğaltmaları veya örnekleri toostart hello yeni kod sürümünde başarısız yükseltme normaldir. Merhaba **UpgradeDomainProgressAtFailure** alan tüm bekleyen yükseltme çalışmanın hatanın hello zamanında anlık görüntüsünü yakalar.

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

Bu örnekte, hello yükseltme başarısız yükseltme etki alanında *MYUD1* ve iki bölüm (*744c8d9f-1d26-417e-a60e-cd48f5c098f0* ve *4b43f4d8-b26b-424e-9307-7a7a62e79750*) takılmış. Merhaba bölümleri takılmış hello çalışma zamanı yüklenemiyor tooplace birincil çoğaltma olduğundan (*WaitForPrimaryPlacement*) hedef düğümleri üzerinde *Düğüm1* ve *Düğüm4*.

Merhaba **Get-ServiceFabricNode** komutu, bu iki düğüm yükseltme etki alanında olduğundan kullanılan tooverify olabilir *MYUD1*. Merhaba *UpgradePhase* diyor *PostUpgradeSafetyCheck*, hello yükseltme etki alanındaki tüm düğümleri yükseltme işlemi tamamlandıktan sonra bu güvenlik denetimleri yaşanan anlamına gelir. Bu bilgiler hello uygulama kodunun hello yeni sürümüyle tooa olası sorunu işaret eder. Merhaba en sık karşılaşılan sorunları hello açık veya promosyon tooprimary kod yollarının hizmet hatalardır.

Bir *UpgradePhase* , *PreUpgradeSafetyCheck* gerçekleştirilip gerçekleştirilmediğine önce hello yükseltme etki alanını hazırlama sorunları vardı anlamına gelir. Merhaba en sık karşılaşılan sorunları bu durumda hizmet hello kapatın veya birincil kod yollarından indirgeme hatalardır.

Merhaba geçerli **UpgradeState** olan *RollingBackCompleted*, hello özgün yükseltmeyi geri alma ile gerçekleştirilen gerekir böylece **FailureAction**, hangi otomatik olarak hata sonrasında hello yükseltme geri alındı. Merhaba özgün yükseltme el ile gerçekleştirdiyseniz **FailureAction**, sonra da hello yükseltme yerine bir hello uygulamasının hata ayıklama Canlı askıya alınma durumundaysa tooallow olacaktır.

### <a name="investigate-health-check-failures"></a>Sistem durumu denetimi hatalarını Araştır
Sistem durumu denetimi hataları bir yükseltme etki alanındaki tüm düğümleri yükseltme ve tüm güvenlik denetimleri geçirme işlemini tamamladıktan sonra oluşabilecek çeşitli sorunları tarafından tetiklenebilir. Bu paragraf aşağıdaki hello çıktı toofailed durumu denetimleri nedeniyle yükseltme bir hatanın normaldir. Merhaba **UnhealthyEvaluations** alan belirtilen toohello göre hello yükseltme hello aynı anda başarısız durumu denetimleri görüntüsünü yakalar [sistem durumu ilkesi](service-fabric-health-introduction.md).

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

Sistem durumu denetimi hataları araştırılıyor ilk hello Service Fabric sistem durumu modeli bilinmesini gerektirir. Ancak bile bu tür bir ayrıntılı anlama olmadan, iki hizmet sağlıksız olduğunu görebiliriz: *fabric: / DemoApp/Svc3* ve *fabric: / DemoApp/Svc2*, hello hata durum raporu ("InjectedFault birlikte "Bu durumda). Bu örnekte, iki dışı dört Hizmetleri %0 sağlıksız hello varsayılan hedef olduğu sağlıksız, (*MaxPercentUnhealthyServices*).

Merhaba yükseltme sırasında başarısız olan belirterek askıya alındı bir **FailureAction** el ile olduğunda yükseltme hello başlatılıyor. Bu mod, başka bir eylem gerçekleştirmeden önce bize tooinvestigate hello Canlı sistem hello başarısız durumda sağlar.

### <a name="recover-from-a-suspended-upgrade"></a>Askıya alınmış bir yükseltmeyi kurtarmak
Bir geri alma ile **FailureAction**, hello yükseltme otomatik olarak geri başarısız olan temel alındığında olmadığından gerekli hiçbir kurtarma yok. El ile **FailureAction**, çeşitli kurtarma seçenekler vardır:

1.  Tetikleyici bir geri alma
2. Merhaba yükseltme Hello kalanı el ile devam edin
3. Yükseltme devam hello izlenen

Merhaba **başlangıç ServiceFabricApplicationRollback** Merhaba uygulaması geri hiçbir zaman toostart komutu kullanılabilir. Merhaba komutu başarıyla döndüğünde hello geri alma isteği hello sistemde kayıtlı ve kısa süre içinde bundan sonra başlar.

Merhaba **Resume-ServiceFabricApplicationUpgrade** komutu kullanılabilir hello hello kalanı aracılığıyla tooproceed yükseltme el ile bir seferde bir yükseltme etki alanı. Bu modda, yalnızca güvenlik denetimleri hello sistem tarafından gerçekleştirilir. Daha fazla sistem durumu denetimleri yapılır. Bu komut yalnızca hello kullanılabilir *UpgradeState* gösterir *RollingForwardPending*, o hello geçerli yükseltme etki alanı başka bir deyişle, yükseltmeyi tamamladı. ancak hello sonraki bir (Bekleyen) başlatılmadı.

Merhaba **güncelleştirme ServiceFabricApplicationUpgrade** kullanılan tooresume izlenen hello güvenlik ve sistem durumu denetimleri yükseltmeye olan yapılabilir komutu.

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

Burada son askıya alındı hello yükseltme etki alanı ve aynı parametreleri ve önce sistem durumu ilkeleri olarak yükseltme kullanım hello Hello yükseltme devam eder. Gerekirse, tüm hello yükseltme parametreleri ve sistem durumu ilkeleri çıkış önceki hello gösterilen hello yükseltme devam ettiğinde aynı komut hello değiştirilebilir. Bu örnekte, hello parametreleri ve değişmeden hello sistem durumu ilkeleri ile izlenen modda hello yükseltme devam ediyor.

## <a name="further-troubleshooting"></a>Daha fazla sorun giderme
### <a name="service-fabric-is-not-following-hello-specified-health-policies"></a>Service Fabric belirtilen hello değil aşağıdaki sistem durumu ilkeleri
Olası neden 1:

Service Fabric tüm yüzdeleri varlıkların (örneğin, çoğaltmalar, bölümler ve Hizmetler) gerçek sayılara için sistem durumu değerlendirmesi dönüşür ve her zaman toowhole varlıklar yuvarlar. Örneğin, Merhaba, en fazla *MaxPercentUnhealthyReplicasPerPartition* % 21 olduğunu ve beş çoğaltmalar, Service Fabric tootwo sağlıksız çoğaltmaları yedeklemek sağlar (diğer bir deyişle,`Math.Ceiling (5*0.21)`). Bu nedenle, sistem durumu ilkeleri uygun şekilde ayarlamanız gerekir.

Olası neden 2:

Sistem durumu ilkeleri toplam Hizmetleri ve özgü olmayan hizmet örnekleri yüzdelerini bakımından belirtilir. Örneğin, bir uygulama dört varsa, yükseltme önce hizmeti D sağlıksız olduğu ancak çok az etkisi toohello uygulamayla örnekleri A, B, C ve D, hizmet. Yükseltme ve ayarlanmış hello parametre sırasında sağlıksız Hizmeti D bilinen tooignore hello istiyoruz *MaxPercentUnhealthyServices* toobe yalnızca A, B ve C varsayılarak % 25 toobe sağlıklı gerekir.

C bozulur sırada ancak, hello yükseltme sırasında D sağlıklı duruma gelebilir. yalnızca % 25'ini hello Hizmetleri sağlıklı olduğundan hello yükseltme yine de başarılı. Ancak, tooC olması nedeniyle beklenmeyen hataları yerine D. beklenmedik bir şekilde sağlıksız neden Bu durumda, D, A'dan farklı hizmet türü olarak modellenmesi gerekir B ve c Sistem durumu ilkeleri hizmet türü belirtilmiş olduğundan, farklı sağlıksız yüzde eşikleri uygulanan toodifferent Hizmetleri olabilir. 

### <a name="i-did-not-specify-a-health-policy-for-application-upgrade-but-hello-upgrade-still-fails-for-some-time-outs-that-i-never-specified"></a>Uygulama yükseltme için bir sistem durumu ilkesi belirtmedi, ancak hiçbir zaman belirtilen bazı zaman aşımlarını hello yükseltme yine başarısız
Sistem durumu ilkeleri toohello yükseltme isteği sağlanmayan, hello alınır *ApplicationManifest.xml* hello geçerli uygulama sürümü. Örneğin, uygulama X sürüm 1.0 tooversion 2.0 ' yükseltiyorsanız, sürüm 1.0 için belirtilen uygulama sistem durumu ilkeleri kullanılır. Farklı sistem durumu ilkesi hello yükseltme için kullanılması gereken hello İlkesi hello uygulama yükseltme API çağrısı bir parçası olarak belirtilen toobe gerekir. Merhaba hello API çağrısı bir parçası olarak belirtilen ilkeleri yalnızca hello yükseltme sırasında uygulanır. Merhaba yükseltme tamamlandıktan sonra hello ilkelerinde belirtilen hello *ApplicationManifest.xml* kullanılır.

### <a name="incorrect-time-outs-are-specified"></a>Hatalı zaman aşımlarını belirtilen
Zaman aşımlarını tutarsız ayarladığınızda ne olduğu hakkında hiç merak ettiniz. Örneğin, olabilir bir *UpgradeTimeout* başlangıç değerinden küçük *UpgradeDomainTimeout*. Merhaba yanıt bir hata döndürülür. Merhaba, hata döndürülür *UpgradeDomainTimeout* hello toplamını'dan küçük *HealthCheckWaitDuration* ve *HealthCheckRetryTimeout*, veya  *UpgradeDomainTimeout* hello toplamını'dan küçük *HealthCheckWaitDuration* ve *HealthCheckStableDuration*.

### <a name="my-upgrades-are-taking-too-long"></a>My yükseltmeler çok uzun sürüyor
bir yükseltme toocomplete Hello süredir hello sistem durumu denetimlerinin ve belirtilen zaman aşımlarını bağlıdır. Sistem durumu denetimlerinin ve zaman aşımlarını toocopy süreyi bağlıdır, dağıtmak ve Merhaba uygulaması Sabitle. Nedenle ölçülü uzun zaman aşımlarını başlangıç öneririz zaman aşımlarını çok agresif olan başarısız yükseltme anlamına gelebilir.

Merhaba zaman aşımlarını hello yükseltme süreleri ile nasıl etkileşim hızlı Yenileyici şöyledir:

Bir yükseltme etki alanına tamamlayamıyor için yükseltme daha hızlı bir şekilde *HealthCheckWaitDuration* + *HealthCheckStableDuration*.

Yükseltme hatası gerçekleşemez daha hızlı bir şekilde *HealthCheckWaitDuration* + *HealthCheckRetryTimeout*.

Merhaba yükseltme etki alanı için yükseltme süresi sınırlıdır *UpgradeDomainTimeout*.  Varsa *HealthCheckRetryTimeout* ve *HealthCheckStableDuration* her ikisi de sıfır olan ve hello uygulama hello durumunu tutar anahtarlama geri ve İleri hello yükseltme sonunda üzerindezamanaşımınauğruyorsonra *UpgradeDomainTimeout*. *UpgradeDomainTimeout* başlar hello geçerli yükseltme etki alanı için bir kez sayım başlatır hello yükseltme.

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama kullanarak Visual Studio yükseltme](service-fabric-application-upgrade-tutorial.md) Visual Studio kullanarak bir uygulama yükseltme yol gösterir.

[Uygulama Powershell kullanarak yükseltme](service-fabric-application-upgrade-tutorial-powershell.md) PowerShell kullanarak bir uygulama yükseltme yol gösterir.

Uygulamanızı kullanarak yükseltme nasıl kontrol [yükseltme parametreleri](service-fabric-application-upgrade-parameters.md).

Uygulama yükseltme öğrenme tarafından uyumlu hale getirmek nasıl toouse [veri seri hale getirme](service-fabric-application-upgrade-data-serialization.md).

Uygulamanız çok başvurarak yükseltirken toouse işlevselliği nasıl Gelişmiş öğrenin[Gelişmiş konular](service-fabric-application-upgrade-advanced.md).
