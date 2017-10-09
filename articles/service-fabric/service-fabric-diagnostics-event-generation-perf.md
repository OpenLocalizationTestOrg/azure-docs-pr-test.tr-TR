---
title: "aaaAzure Service Fabric performansını izleme | Microsoft Docs"
description: "İzleme ve tanılama Azure Service Fabric kümeleri için performans sayaçları hakkında bilgi edinin."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a>Performans ölçümleri

Ölçümleri toplanan toounderstand hello performans kümenizin yanı sıra içinde çalışan hello uygulamaları gerekir. Service Fabric kümeleri için performans sayaçlarını izleyerek hello toplama öneririz.

## <a name="nodes"></a>Düğümler

Kümenizdeki Hello makineler için aşağıdaki performans sayaçları toobetter anlamak her makinede yük hello ve kararları ölçeklendirme uygun küme olun hello toplama göz önünde bulundurun.

| Sayacı kategorisi | Sayaç adı |
| --- | --- |
| PhysicalDisk (her Disk için) | Ort. Disk okuma sırası uzunluğu |
| PhysicalDisk (her Disk için) | Ort. Disk yazma sırası uzunluğu |
| PhysicalDisk (her Disk için) | Ort. Disk sn/Okuma |
| PhysicalDisk (her Disk için) | Ort. Disk sn/yazma |
| PhysicalDisk (her Disk için) | Disk Okuma/sn |
| PhysicalDisk (her Disk için) | Disk okuma bayt/sn |
| PhysicalDisk (her Disk için) | Disk Yazma/sn |
| PhysicalDisk (her Disk için) | Disk Yazma Bayt/sn |
| Bellek | Kullanılabilir MBayt |
| PagingFile | % Kullanım |
| Process(Total) | % İşlemci zamanı |
| İşlem (her hizmeti) | % İşlemci zamanı |
| İşlem (her hizmeti) | İşlem kimliği |
| İşlem (her hizmeti) | Özel bayt sayısı |
| İşlem (her hizmeti) | İş parçacığı sayısı |
| İşlem (her hizmeti) | Sanal bayt sayısı |
| İşlem (her hizmeti) | Çalışma kümesi |
| İşlem (her hizmeti) | Çalışma kümesi - özel |

## <a name="net-applications-and-services"></a>.NET uygulamaları ve Hizmetleri

.NET Hizmetleri tooyour küme dağıtıyorsanız sayaçları aşağıdaki hello toplayın. 

| Sayacı kategorisi | Sayaç adı |
| --- | --- |
| .NET CLR bellek (her hizmeti) | İşlem kimliği |
| .NET CLR bellek (her hizmeti) | # Toplam kaydedilmiş bayt |
| .NET CLR bellek (her hizmeti) | # Toplam bayt ayrılmış |
| .NET CLR bellek (her hizmeti) | # Tüm yığınlardaki bayt |
| .NET CLR bellek (her hizmeti) | # Gen 0 koleksiyonları |
| .NET CLR bellek (her hizmeti) | # Gen 1 koleksiyonları |
| .NET CLR bellek (her hizmeti) | # Gen 2 koleksiyonları |
| .NET CLR bellek (her hizmeti) | GC % zaman |

### <a name="service-fabrics-custom-performance-counters"></a>Service Fabric'ın özel performans sayaçları

Service Fabric özel performans sayaçları önemli miktarda oluşturur. Merhaba yüklü SDK varsa, Performans İzleyicisi uygulamanızda hello kapsamlı listesi Windows makinenizde görebilirsiniz (Başlat > Performans İzleyicisi). 

Merhaba uygulamalarda tooyour küme dağıtıyorsanız, Reliable Actors kullanıyorsanız, gelen countes ekleyin `Service Fabric Actor` ve `Service Fabric Actor Method` kategorileri (bkz [Service Fabric güvenilir aktörler tanılama](service-fabric-reliable-actors-diagnostics.md)).

Güvenilir hizmetlerini kullanıyorsanız, benzer şekilde sahibiz `Service Fabric Service` ve `Service Fabric Service Method` toplamanız gerekir sayacı kategorileri sayaçları. 

Güvenilir koleksiyonları kullanırsanız, hello eklemenizi öneririz `Avg. Transaction ms/Commit` hello gelen `Service Fabric Transactional Replicator` toocollect hello ortalama yürütme gecikmesi işlem ölçüm başına.


## <a name="next-steps"></a>Sonraki adımlar

* Daha fazla bilgi edinmek [olay oluşturma hello platform düzeyinde](service-fabric-diagnostics-event-generation-infra.md) Service Fabric içinde
* Aracılığıyla performans ölçümlerini derleme [Azure tanılama](service-fabric-diagnostics-event-aggregation-wad.md)
