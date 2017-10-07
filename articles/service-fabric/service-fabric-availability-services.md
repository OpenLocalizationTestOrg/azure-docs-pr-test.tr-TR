---
title: Service Fabric Hizmetleri aaaAvailability | Microsoft Docs
description: "Hata algılama, yük devretme ve kurtarma Hizmetleri için açıklar"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c443aadfe31a1413359b08d34c4b7dd5db4edd16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-of-service-fabric-services"></a>Service Fabric hizmetlerin kullanılabilirliğini
Bu makale, Service Fabric bir hizmetin kullanılabilirliğini nasıl korur genel bir bakış sağlar.

## <a name="availability-of-service-fabric-stateless-services"></a>Service Fabric durum bilgisi olmayan hizmetler kullanılabilirliği
Azure Service Fabric Hizmetleri durum bilgisi olan ya da durum bilgisiz olabilir. Durum bilgisiz hizmet içermediği bir uygulama hizmetidir [yerel durumu](service-fabric-concepts-state.md) , yüksek oranda kullanılabilir veya güvenilir toobe gerekir.

Durum bilgisiz hizmet oluşturma gerektirir tanımlayan bir `InstanceCount`. Merhaba örnek sayısı hello hello kümede çalışan hello durum bilgisi olmayan hizmetin uygulama mantığını örneklerinin sayısını tanımlar. Merhaba örneklerinin sayısını artırarak bir durum bilgisi olmayan hizmetin ölçeklendirme şekilde önerilen hello olur.

Bir durum bilgisiz adlı hizmetin örneği başarısız olduğunda, yeni bir örneğini hello kümedeki bazı uygun düğümde oluşturulur. Örneğin, bir durum bilgisiz hizmet örneği üzerinde Düğüm1 başarısız olabilir ve Düğüm5'yeniden oluşturulması.

## <a name="availability-of-service-fabric-stateful-services"></a>Service Fabric durum bilgisi olan hizmetler kullanılabilirliği
Durum bilgisi olan hizmet ilişkili bazı durumlar vardır. Service Fabric durum bilgisi olan hizmet çoğaltmaları kümesi olarak modellenir. Her çoğaltma hello kod ayrıca hello durumu bu hizmet için bir kopyasına sahip hello hizmetinin çalışan bir örneğidir. Okuma ve yazma işlemleri (Merhaba birincil olarak adlandırılır) bir yinelemede gerçekleştirilir. Yazma işlemleri gelen değişiklikler toostate olan *çoğaltılan* toohello (etkin ikincil kopya olarak adlandırılır) hello çoğaltma kümesindeki diğer kopyalarla ve uygulanır. 

Yalnızca bir birincil çoğaltmaya olabilir, ancak birden fazla etkin ikincil çoğaltma olabilir. Etkin ikincil çoğaltmaları Hello sayısı yapılandırılabilir ve daha yüksek bir sayı çoğaltmalarının daha fazla sayıda eşzamanlı yazılım ve donanım hatalarına dayanabileceğinden.

Merhaba birincil çoğaltma devre dışı kalırsa, Service Fabric hello etkin ikincil çoğaltmaları hello yeni birincil çoğaltma birini hale getirir. Bu etkin ikincil çoğaltma zaten hello durumunun hello güncelleştirilmiş sürümüne sahip (aracılığıyla *çoğaltma*), ve daha fazla okuma işlemeye devam et ve yazma işlemleri.

Bu kavramı bir birincil veya etkin ikincil olan bir çoğaltma, çoğaltma rolü hello adlandırılıyor.

### <a name="replica-roles"></a>Çoğaltma rolleri
Merhaba bir çoğaltma, çoğaltma tarafından yönetilen hello durumunun kullanılan toomanage hello yaşam döngüsü rolüdür. Birincil Hizmetleri rolünü olmayan bir çoğaltma istekleri okuyun. Merhaba birincil durumunu güncelleştirme ve hello değişiklikleri çoğaltmaya ayrıca tüm yazma isteklerini işler. Bu değişiklikler uygulanan toohello hello yineleme kümesindeki etkin ikincil öğe olur. bir etkin ikincil Hello iş birincil çoğaltma hello tooreceive durum değişiklikleri çoğaltıldığını ve onun hello durum görünümünü güncelleştirme ediyor.

> [!NOTE]
> Üst düzey programlama modelleri gibi [Reliable Actors](service-fabric-reliable-actors-introduction.md) ve [Reliable Services](service-fabric-reliable-services-introduction.md) çoğaltma rolü hello geliştiriciden hello kavramı gizle. Aktör içinde rol hello kavramı sırasında büyük ölçüde çoğu senaryoları için Basitleştirilmiş Hizmetleri'ndeki gereksizdir.
>

## <a name="next-steps"></a>Sonraki adımlar
Service Fabric kavramlarla ilgili daha fazla bilgi için aşağıdaki makaleler hello bakın:

- [Service Fabric Hizmetleri ölçeklendirme](service-fabric-concepts-scalability.md)
- [Service Fabric Hizmetleri bölümlendirme](service-fabric-concepts-partitioning.md)
- [Tanımlama ve durumunu yönetme](service-fabric-concepts-state.md)
- [Reliable Services](service-fabric-reliable-services-introduction.md)
