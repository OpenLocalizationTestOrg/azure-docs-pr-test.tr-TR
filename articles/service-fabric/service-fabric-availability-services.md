---
title: "Service Fabric hizmetlerin kullanılabilirliğini | Microsoft Docs"
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
ms.openlocfilehash: 41ff2c3129facb0eea9d896ce75d7343ae2a018e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="availability-of-service-fabric-services"></a>Service Fabric hizmetlerin kullanılabilirliğini
Bu makale, Service Fabric bir hizmetin kullanılabilirliğini nasıl korur genel bir bakış sağlar.

## <a name="availability-of-service-fabric-stateless-services"></a>Service Fabric durum bilgisi olmayan hizmetler kullanılabilirliği
Azure Service Fabric Hizmetleri durum bilgisi olan ya da durum bilgisiz olabilir. Durum bilgisiz hizmet içermediği bir uygulama hizmetidir [yerel durumu](service-fabric-concepts-state.md) , yüksek oranda kullanılabilir veya güvenilir olması gerekir.

Durum bilgisiz hizmet oluşturma gerektirir tanımlayan bir `InstanceCount`. Örnek sayısı, kümede çalışan bir durum bilgisi olmayan hizmetin uygulama mantığı örneklerinin sayısını tanımlar. Örneklerinin sayısını artırarak bir durum bilgisi olmayan hizmetin ölçeklendirme önerilen yoludur.

Bir durum bilgisiz adlı hizmetin örneği başarısız olduğunda, yeni bir örneğini uygun bazı küme düğümünde oluşturulur. Örneğin, bir durum bilgisiz hizmet örneği üzerinde Düğüm1 başarısız olabilir ve Düğüm5'yeniden oluşturulması.

## <a name="availability-of-service-fabric-stateful-services"></a>Service Fabric durum bilgisi olan hizmetler kullanılabilirliği
Durum bilgisi olan hizmet ilişkili bazı durumlar vardır. Service Fabric durum bilgisi olan hizmet çoğaltmaları kümesi olarak modellenir. Her çoğaltma Ayrıca hizmet durumu kopyasına sahip hizmet kod çalışan bir örneğidir. Okuma ve yazma işlemleri (birincil olarak adlandırılır) bir yinelemede gerçekleştirilir. Durumu değişiklikleri yazma işlemleri *çoğaltılan* (çağrılan etkin ikinciller) çoğaltma kümesindeki diğer yinelemelere ve uygulanır. 

Yalnızca bir birincil çoğaltmaya olabilir, ancak birden fazla etkin ikincil çoğaltma olabilir. Etkin ikincil çoğaltmaların sayısı yapılandırılabilir bir değerdir ve daha yüksek bir sayı çoğaltmalarının daha fazla sayıda eşzamanlı yazılım ve donanım hatalarına dayanabilir.

Birincil çoğaltma devre dışı kalırsa, Service Fabric etkin ikincil çoğaltmaları yeni birincil birini yapar çoğaltma. Bu etkin ikincil çoğaltma durumu güncelleştirilmiş sürümünü zaten (aracılığıyla *çoğaltma*), ve daha fazla okuma işlemeye devam et ve yazma işlemleri.

Bu kavramı bir birincil veya etkin ikincil olan bir çoğaltma, çoğaltma rolü olarak bilinir.

### <a name="replica-roles"></a>Çoğaltma rolleri
Bir çoğaltma rolü Bu çoğaltma tarafından yönetilen durumu ömrünü yönetmek için kullanılır. Birincil Hizmetleri rolünü olmayan bir çoğaltma istekleri okuyun. Birincil durumunu güncelleştirme ve değişiklikleri çoğaltmaya ayrıca tüm yazma isteklerini işler. Bu değişiklikleri etkin ikincil Kopya kümesindeki uygulanır. Birincil çoğaltma çoğaltıldığını durumu değişiklikleri alır ve kendi görünüm durumu güncelleştirmek için bir etkin İkincil iş ediyor.

> [!NOTE]
> Üst düzey programlama modelleri gibi [Reliable Actors](service-fabric-reliable-actors-introduction.md) ve [Reliable Services](service-fabric-reliable-services-introduction.md) çoğaltma rolü geliştiriciden kavramı gizle. Aktör içinde rol kavramı sırasında büyük ölçüde çoğu senaryoları için Basitleştirilmiş Hizmetleri'ndeki gereksizdir.
>

## <a name="next-steps"></a>Sonraki adımlar
Service Fabric kavramları hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

- [Service Fabric Hizmetleri ölçeklendirme](service-fabric-concepts-scalability.md)
- [Service Fabric Hizmetleri bölümlendirme](service-fabric-concepts-partitioning.md)
- [Tanımlama ve durumunu yönetme](service-fabric-concepts-state.md)
- [Reliable Services](service-fabric-reliable-services-introduction.md)
