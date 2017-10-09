---
title: "Güvenilir hizmetler aaaAdvanced kullanımını | Microsoft Docs"
description: "Service Fabric'ın Reliable Services hizmetlerinizi eklenen esneklik için Gelişmiş kullanımı hakkında bilgi edinin."
services: Service-Fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: masnider
ms.assetid: f2942871-863d-47c3-b14a-7cdad9a742c7
ms.service: Service-Fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: e6d6310a4deae9edcfcd76551e1337f0e39e9e5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-usage-of-hello-reliable-services-programming-model"></a>Merhaba güvenilir programlama modeli hizmetler kullanımını Gelişmiş
Azure Service Fabric, yazma ve durum bilgisiz ve durum bilgisi olan güvenilir hizmetler yönetme basitleştirir. Bu kılavuz, hizmetlerinizi Reliable Services toogain Gelişmiş kullanımlar hakkında daha fazla denetim ve esneklik alınmaktadır. Önceki tooreading bu kılavuz, ile öğrenmeniz [hello Reliable Services programlama modeli](service-fabric-reliable-services-introduction.md).

Durum bilgisi olan ve durum bilgisi olmayan hizmetler için kullanıcı kodu iki birincil giriş noktası vardır:

* `RunAsync(C#) / runAsync(Java)`Hizmet kodunuz için genel amaçlı giriş noktası niteliğindedir.
* `CreateServiceReplicaListeners(C#)`ve `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` istemci istekleri için iletişim dinleyicileri açmak içindir.

Çoğu hizmetler için bu iki giriş noktaları yeterlidir. Nadir durumlarda bir hizmetin yaşam döngüsü hakkında daha fazla denetime gerektiğinde ek yaşam döngüsü olayları kullanılabilir.

## <a name="stateless-service-instance-lifecycle"></a>Durum bilgisiz hizmet örneği yaşam döngüsü
Bir durum bilgisi olmayan hizmetin yaşam döngüsü, çok basit bir işlemdir. Durum bilgisiz hizmeti yalnızca açık, kapalı, durduruldu veya kaldırılabilir. `RunAsync`bir hizmet örneği açılır ve bir hizmet örneği durduruldu veya kapatıldığında iptal durum bilgisi olmayan bir hizmet olarak yürütülür.

Ancak `RunAsync` neredeyse tüm durumlarda, hello açık kapatın ve durum bilgisiz hizmet durdurma olayları kullanılabilir ayrıca içinde yeterli olması gerekir:

* `Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java`Merhaba durum bilgisiz hizmet örneği hakkında kullanılan toobe olduğunda OnOpenAsync adı verilir. Genişletilmiş hizmeti başlatma görevleri şu anda başlatılabilir.
* `Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java`Merhaba durum bilgisiz hizmet örneği toobe geçerken OnCloseAsync adlı düzgün biçimde kapatma. Bu hello hizmetin kod yükseltilmesi, tooload Dengeleme nedeniyle hello hizmet örneği taşındığı ya da geçici bir hata algılandığında ortaya çıkabilir. OnCloseAsync Kapat kullanılan toosafely herhangi bir kaynağa olması, herhangi bir arka plan işlem durdurmak, dış durumu kaydetmeyi bitirmek veya var olan bağlantıları kapatın.
* `void OnAbort() - C# / void onAbort() - Java`Merhaba durum bilgisiz hizmet örneği zorla kapatılıyor OnAbort denir. Bu genellikle hello düğümde kalıcı bir hata algılandığında veya Service Fabric güvenilir bir şekilde hello hizmet örneğinin yaşam döngüsü toointernal hataları nedeniyle yönetemediğinde olarak adlandırılır.

## <a name="stateful-service-replica-lifecycle"></a>Durum bilgisi olan hizmet çoğaltma yaşam döngüsü

> [!NOTE]
> Durum bilgisi olan güvenilir hizmetler Java'da henüz desteklenmiyor.
>
>

Bir durum bilgisi olan hizmet yinelemenin yaşam döngüsü, bir durum bilgisiz hizmet örneği çok daha karmaşıktır. Ayrıca tooopen, kapatın ve olayları abort, bir durum bilgisi olan hizmet çoğaltma rolü değişiklikleri yaşam süresi boyunca uğradığında. Bir durum bilgisi olan hizmet çoğaltma rolü değiştiğinde hello `OnChangeRoleAsync` olay tetiklenir:

* `Task OnChangeRoleAsync(ReplicaRole, CancellationToken)`Merhaba durum bilgisi olan hizmet çoğaltma rolü, örneğin tooprimary veya ikincil değiştirirken OnChangeRoleAsync adı verilir. Birincil çoğaltmalara yazma durumu verilmiştir (toocreate izin verilir ve tooReliable koleksiyonları yazma). İkincil çoğaltmaları (yalnızca var olan güvenilir koleksiyonlarından okuyabilir) okuma durumu atanır. Durum bilgisi olan hizmet çoğu iş hello birincil kopyada gerçekleştirilir. İkincil çoğaltmaların salt okunur doğrulama, rapor oluşturma, veri araştırma veya diğer salt okunur işleri gerçekleştirebilirsiniz.

Durum bilgisi olan bir hizmette yalnızca hello birincil çoğaltma yazma erişimi toostate vardır ve bu nedenle hello hizmet asıl işi gerçekleştirirken genellikle olur. Merhaba `RunAsync` durum bilgisi olan hizmet yönteminde yalnızca hello durum bilgisi olan hizmet çoğaltma birincil olduğunda gerçekleştirilir. Merhaba `RunAsync` birincil kopyanın rol değişiklikleri birincil çıktığınızda yanı sıra hello sırasında kapatıp olayları abort yöntemi iptal edilir.

Hello kullanarak `OnChangeRoleAsync` olay tooperform iş çoğaltma rolü de olduğu gibi yanıt toorole değişiklik bağlı olarak verir.

Durum bilgisi olan hizmet ayrıca hello aynı dört yaşam döngüsü olayları durumsuz bir hizmet olarak sağlar hello aynı semantiği ve kullanım örnekleri:

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a>Sonraki adımlar
Daha gelişmiş konular ilgili tooService için doku, makaleler hello bakın:

* [Durum bilgisi olan güvenilir hizmetler yapılandırma](service-fabric-reliable-services-configuration.md)
* [Service Fabric sistem durumu giriş](service-fabric-health-introduction.md)
* [Sorun giderme için sistem durumu raporlarını kullanma](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Yapılandırma Hizmetleri hello Service Fabric kümesi Resource Manager ile](service-fabric-cluster-resource-manager-configure-services.md)
