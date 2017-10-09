---
title: "aaaService doku Küme Kaynak Yöneticisi - benzeşim | Microsoft Docs"
description: "Benzeşim hizmet doku hizmetler için yapılandırma genel bakış"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 678073e1-d08d-46c4-a811-826e70aba6c4
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 7dc9b6d9c18d9d615d39cff7de9d7cba1c040474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-service-affinity-in-service-fabric"></a>Yapılandırma ve Service Fabric hizmeti benzeşimini kullanma
Benzeşim çoğunlukla toohelp kolaylığı hello geçişin Bulut ve mikro Merhaba Dünya daha büyük tek yapılı uygulamalara sağlanan bir denetimdir. Bunu yapmak, böylece yan etkileri sahip olabilirsiniz, ancak Hizmetleri hello performansını iyileştirmek için bir iyileştirme da kullanılır.

Daha büyük bir uygulama veya bir yalnızca unutmayın, tooService doku (veya dağıtılmış bir ortama) mikro tasarlanan değildi getiren varsayalım. Bu geçiş türünü yaygındır. Merhaba ortamına hello tüm uygulama kaldırma, paketleme ve düzgün çalıştığından emin olmak başlatın. Daha sonra tüm tooeach diğer konuşun farklı küçük Hizmetleri içine çiğnemekten başlatın.

Sonunda Merhaba uygulaması bazı sorunlar yaşıyor bulabilirsiniz. Merhaba sorunları genellikle bu kategoriden ayrılır:

1. Bazı bileşeni X hello tek yapılı uygulama bileşeni Y belgelenmemiş bir bağımlılık vardı ve yalnızca bu bileşenleri ayrı hizmetlerine açık. Bu hizmetleri artık hello kümedeki farklı düğümlerde çalışan olduğundan, bunlar bozuk.
2. Bu bileşenlerin üzerinden iletişim kurmasına (adlandırılmış kanallar yerel | bellek paylaşılan | diskteki dosyaları) ve gerçekten toobe mümkün toowrite paylaşılan tooa yerel kaynak Performans nedeniyle şu anda gerekir. Bu sabit bağımlılık daha sonra belki de kaldırılır.
3. Her şeyi sorun yoktur, ancak bu iki bileşenin gerçekten chatty/performans hassas olduğunu öyle. Bunlar ayrı hizmetlerine taşındıklarında genel tanked uygulama performansı veya gecikme artar. Sonuç olarak, hello genel uygulama beklentilerini karşılayıp değil.

Bu durumda, biz toolose bizim düzenleme iş istemediğiniz ve toogo geri toohello monolith istemiyorum. Merhaba son koşul bile düz bir iyileştirme istenebilir. Ancak, biz hello bileşenleri toowork Hizmetleri olarak doğal olarak tasarlayabilirsiniz kadar (veya biz hello performans beklentilerini başka bir yolla çözebilir kadar) tooneed yere göre bazı duygusu yapacağız.

Hangi toodo? İyi üzerinde benzeşim kapatma çalışabilir.

## <a name="how-tooconfigure-affinity"></a>Nasıl tooconfigure benzeşimi
tooset benzeşim yukarı iki farklı hizmetler arasında bir benzeşim ilişkisi tanımlayın. "Bir hizmet başka bir işaret" ve "Bu hizmet yalnızca burada hizmetinin çalıştığını çalıştırabilirsiniz." belirten olarak benzeşim düşünebilirsiniz Bazen biz (burada hello üst hello alt işaretleyin) bir üst/alt ilişkisi tooaffinity bakın. Benzeşimi sağlar hello çoğaltmaları veya bir hizmet örnekleri üzerinde hello aynı sıraya alınma düğümleri olanlar başka bir hizmet olarak.

```csharp
ServiceCorrelationDescription affinityDescription = new ServiceCorrelationDescription();
affinityDescription.Scheme = ServiceCorrelationScheme.Affinity;
affinityDescription.ServiceName = new Uri("fabric:/otherApplication/parentService");
serviceDescription.Correlations.Add(affinityDescription);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

> [!NOTE]
> Bir alt hizmeti yalnızca bir tek benzeşim ilişkisinde yer alabilir. Merhaba alt Benzetilen toobe tootwo üst Hizmetleri aynı anda istediyseniz, birkaç seçeneğiniz vardır:
> - Merhaba ilişkileri ters (parentService1 ve hello geçerli alt hizmeti noktası parentService2 varsa), veya
> - Kurala göre bir hello üst hub'ı olarak belirleyin ve tüm hizmetleri, bu hizmeti noktası. 
>
> yerleştirme davranışını hello kümedeki kaynaklanan hello olması hello aynı.
>

## <a name="different-affinity-options"></a>Farklı benzeşim seçenekleri
Benzeşim birkaç bağıntı düzenleri biri ile temsil edilir ve iki farklı mod vardır. Merhaba en yaygın benzeşim NonAlignedAffinity veririz modudur. Çoğaltmaları NonAlignedAffinity içinde hello veya hello farklı Hizmetleri örneği üzerinde hello aynı yerleştirilir düğümleri. Merhaba diğer AlignedAffinity moddur. Yalnızca durum bilgisi olan hizmetler ile hizalanmış benzeşim yararlıdır. Hizmetleri hizalı toohave benzeşimi sağlar, bu hizmetlerin hello ana üzerinde yerleştirilir iki durum bilgisi olan yapılandırma hello aynı düğümleri olarak her diğer. Bu hizmetleri toobe hello üzerinde aynı yerleştirilen için her çifti ikincil kopya da neden düğümleri. Da mümkündür (ancak daha az görülen) tooconfigure NonAlignedAffinity durum bilgisi olan hizmetler için. NonAlignedAffinity, aynı düğümlerine hello farklı iki durum bilgisi olan hizmet çalıştırılır hello çoğaltmalarını Merhaba, ancak kendi ana farklı düğümlerde şunun.

<center>
![Benzeşim modları ve bunların etkileri][Image1]
</center>

### <a name="best-effort-desired-state"></a>En iyi çaba istenen durumu
En iyi çaba bir benzeşim ilişkidir. Merhaba düzenleme veya yapan hello çalıştıran aynı yürütülebilir bir işlemi güvenilirliği aynı garanti sağlamaz. bir benzeşim ilişkisi Hello Hizmetleri'nde başarısız olabilir ve bağımsız olarak taşınmasına temelde farklı varlıklardır. Ancak bu sonlarını geçici bir benzeşim ilişkisi de kesebilir. Örneğin, kapasite sınırlamaları hello benzeşim ilişkisi hello hizmet nesneleri yalnızca bazılarını belirli bir düğümde uygun olduğu anlamına gelebilir. Yerinde bir benzeşim ilişkisi olsa bu durumlarda, son zorlanamaz toohello diğer kısıtlamaları. Bu nedenle olası toodo olması durumunda, hello ihlali daha sonra otomatik olarak düzeltilir.

### <a name="chains-vs-stars"></a>Zincirleri yıldız karşılaştırması
Bugün hello küme Resource Manager mümkün toomodel zincirleri benzeşim ilişkilerin değil. Bu, bir alt bir benzeşim ilişkisi olan bir hizmettir anlamı başka bir benzeşim ilişkisi içinde üst öğesi olamaz. Bu ilişki türünde toomodel istiyorsanız, toomodel etkin olan bir zincir yerine bir yıldız olarak. bir zincir tooa yıldız hello alttaki alt gelen toomove üst öğeye sahip toohello ilk çocuğun üst yerine olacaktır. Hizmetlerinizin düzenlenmesi Hello bağlı olarak, birden çok kez toodo olabilir. Doğal üst hizmet ise, bir yer tutucu olarak hizmet veren bir toocreate sahip olabilir. Gereksinimlerinize bağlı olarak, ayrıca toolook içine isteyebilir [uygulama grupları](service-fabric-cluster-resource-manager-application-groups.md).

<center>
![Zincirleri vs. Merhaba benzeşimi ilişkileri bağlam yıldızları][Image2]
</center>

Başka bir şey toonote benzeşimi ilişkileri hakkında bugün yön olduklarından emin olan. Başka bir deyişle, hello benzeşim kural yalnızca hello üst yerleştirilen bu hello alt zorlar. Bu hello üst hello çocuğunuzla bulunduğu olunmasını sağlamamasıdır. Farklı Hizmetleri ile farklı yaşam döngüleri vardır ve başarısız ve bağımsız olarak hareket beri benzeşim ilişkisi hello toonote mükemmel veya anında zorlanamaz önemlidir. Örneğin, bunu kilitlendi çünkü hello üst aniden tooanother düğüm üzerinde başarısız varsayalım. tutarlı ve kullanılabilir, Hello Hizmetleri tutma hello öncelik olduğundan hello Küme Kaynak Yöneticisi ve Yük Devretme Yöneticisi tanıtıcısı ilk olarak, yük devretme hello. Hello yük devretme işlemi tamamlandıktan sonra hello benzeşim ilişkisi bozuk, ancak Küme Kaynak Yöneticisi bu hello alt bildirimler kadar her şeyi ince taşıdığını düşündüğü hello hello üst bulunduğu değil. Bu tür denetimler düzenli olarak gerçekleştirilir. Hello küme Resource Manager kısıtlamaları nasıl hesaplar hakkında daha fazla bilgi kullanılabilir [bu makalede](service-fabric-cluster-resource-manager-management-integration.md#constraint-types), ve [bu](service-fabric-cluster-resource-manager-balancing.md) nasıl tooconfigure hello hakkında tempoyla bu kısıtlamaların olduğu daha fazla ettiği değerlendirilir.   


### <a name="partitioning-support"></a>Bölümleme desteği
Merhaba son bir şey toonotice benzeşimi ile ilgili benzeşimi ilişkileri hello üst burada bölümlenmiş desteklenmeyen ' dir. Bölümlenmiş üst Hizmetleri sonunda desteklenmiyor olabilir, ancak bugün verilmez.

## <a name="next-steps"></a>Sonraki adımlar
- Hizmetleri yapılandırma hakkında daha fazla bilgi için [hizmetleri yapılandırma hakkında bilgi edinin](service-fabric-cluster-resource-manager-configure-services.md)
- toolimit Hizmetleri tooa küçük makineler kümesi veya toplama hello yük Hizmetleri, kullanım [uygulama grupları](service-fabric-cluster-resource-manager-application-groups.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resrouce-manager-affinity-modes.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-affinity/cluster-resource-manager-chains-vs-stars.png