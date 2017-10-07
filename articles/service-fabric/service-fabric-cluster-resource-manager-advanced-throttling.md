---
title: "Merhaba Service Fabric kümesi Kaynak Yöneticisi'nde aaaThrottling | Microsoft Docs"
description: "Merhaba Service Fabric kümesi kaynak yöneticisi tarafından sağlanan tooconfigure hello kısıtlamaları öğrenin."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4a44678b-a5aa-4d30-958f-dc4332ebfb63
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f418536911d3e3814e78a4d9f057dfb867ca7c63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-hello-service-fabric-cluster-resource-manager"></a>Azaltma hello Service Fabric kümesi Kaynak Yöneticisi
Merhaba Küme Kaynak Yöneticisi'ni düzgün yapılandırdıktan olsa bile hello küme kesintiye. Örneğin, yükseltme sırasında oluştu neler olacağını eşzamanlı düğüm ve hata etki alanı hataları - olabilir? Merhaba küme Resource Manager toofix tooreorganize ve düzeltme hello küme çalışarak hello küme kaynaklarını kullanan her şeyi her zaman çalışır. Kısıtlamaları yardımcı bir backstop sağlamak hello küme kaynakları toostabilize kullanma - hello düğümleri gelen geri, böylece hello ağ bölümleri onarma, düzeltilmiş BITS dağıtılmış.

toohelp durumlarda bu tür ile Merhaba Service Fabric kümesi Kaynak Yöneticisi birkaç kısıtlamaları içerir. Bu kısıtlamaları tüm oldukça büyük hammers ' dir. Genellikle, dikkatli planlama ve sınama yapılmadan değiştirilmesi gerekir.

Merhaba küme kaynak yöneticisinin kısıtlamaları değiştirirseniz, tooyour beklenen gerçek yük ayarlamak. Bazı durumlarda daha uzun toostabilize hello küme alır anlamına gelir olsa bile bazı kısıtlar yerinde toohave gereksinim belirleyebilir. Test gerekli toodetermine hello doğru değerleri kısıtlamaları etmektir. Düşük yeterli tooactually önlemek çok fazla kaynak tüketimini ve kısıtlamaları makul bir sürede toobe yeterince tooallow hello küme toorespond toochanges gerekir. 

Müşteriler gördük hello zamanının çoğunu zaten bir kaynak kısıtlanmış ortamında olduğundan bırakıldı kısıtlamaları kullanın. Bazı örnekler tek düğümler ya da çok sayıda durum bilgisi olan yinelemede mümkün toobuild olmayan diskleri için sınırlı ağ bant genişliği olacaktır toothroughput sınırlamaları nedeniyle paralel. Kısıtlamaları, işlemleri işlemleri toofail neden bu kaynakları doldurmaya veya yavaş. Bu gibi durumlarda müşteriler kısıtlamaları kullanılan ve kararlı bir duruma hello küme tooreach geçen süre miktarı hello genişletme biliyorduk. Müşterileri de bunlar kısıtlanan sırada düşük genel güvenilirlik çalışan sonlandırmak anladım.


## <a name="configuring-hello-throttles"></a>Yapılandırma hello kısıtlar

Service Fabric çoğaltma hareketleri hello sayısını azaltma için iki mekanizma vardır. Merhaba varsayılan Service Fabric 5.7 önce var olan bir mekanizma, bir izin verilen taşır mutlak sayı olarak azaltma temsil eder. Bu, tüm boyutları kümeleri için çalışmaz. Özellikle büyük kümeleri hello varsayılan değer, daha küçük kümelerde hiçbir etkisi yaparken gerekli olduğunda bile Dengeleme aşağı önemli ölçüde yavaşlamasının çok küçük olabilir. Bu önceki mekanizması yüzde tabanlı denetimi tarafından hangi hangi hizmetlerin hello sayısı dinamik kümeleriyle iyi ölçeklenir yerini yenisi aldı ve düğümler düzenli olarak değiştirin.

Merhaba kısıtlamaları hello kümelerinde çoğaltmaları hello sayısı yüzdesi dayanır. Temel Percetage kısıtlamaları ifade hello Kuralı etkinleştirmek: "hareket çoğaltmaları % 10'dan fazla 10 dakikalık bir zaman aralığı içinde", örneğin.

yüzde tabanlı azaltma için hello yapılandırma ayarları şunlardır:

  - GlobalMovementThrottleThresholdPercentage - kümedeki herhangi bir zamanda izin hareketlerinin sayısı üst sınırı çoğaltmaları hello kümedeki toplam sayısı yüzdesi olarak ifade edilen. 0 sınır gösterir. Merhaba varsayılan değer 0'dır. Bu ayar ve GlobalMovementThrottleThreshold belirtilirse, ardından hello daha pasif sınırı kullanılır.
  - GlobalMovementThrottleThresholdPercentageForPlacement - çoğaltmaları hello kümedeki toplam sayısı yüzdesi olarak ifade edilen hello yerleştirme aşamasında, izin verilen hareketlerinin sayısı üst sınırı. 0 sınır gösterir. Merhaba varsayılan değer 0'dır. Bu ayar ve GlobalMovementThrottleThresholdForPlacement belirtilirse, ardından hello daha pasif sınırı kullanılır.
  - GlobalMovementThrottleThresholdPercentageForBalancing - aşaması, çoğaltmaları hello kümedeki toplam sayısı yüzdesi olarak ifade edilen Dengeleme hello sırasında izin verilen hareketlerinin sayısı üst sınırı. 0 sınır gösterir. Merhaba varsayılan değer 0'dır. Bu ayar ve GlobalMovementThrottleThresholdForBalancing belirtilirse, ardından hello daha pasif sınırı kullanılır.

Merhaba azaltma yüzdesi belirtirken, %5 0,05 belirtmeniz gerekir. Bu kısıtlamaları yönetilen hello hello saniye cinsinden belirtilen GlobalMovementThrottleCountingInterval aralığıdır.


``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThresholdPercentage" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForPlacement" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForBalancing" Value="0" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
</Section>
```

tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "GlobalMovementThrottleThresholdPercentage",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForPlacement",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForBalancing",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleCountingInterval",
          "value": "600"
      }
    ]
  }
]
```

### <a name="default-count-based-throttles"></a>Varsayılan dayalı sayısı kısıtlamaları
Eski kümede vardır veya bu yapılandırmalar beri yükseltildi kümelerinde hala korur durumunda bu bilgiler sağlanır. Genel olarak, bunlar hello yüzde tabanlı kısıtlamaları ile yukarıdaki değiştirilir önerilir. Yüzde tabanlı azaltma varsayılan olarak devre dışı bırakıldığından bu kısıtlamaları devre dışı ve hello kısıtlamaları yüzde tabanlı yerini kadar hello varsayılan kısıtlamaları bir küme için kalır. 

  - GlobalMovementThrottleThreshold – Bu ayar bazı zamanla hello hareketleri hello kümedeki toplam sayısını denetler. Merhaba süreyi saniye cinsinden hello GlobalMovementThrottleCountingInterval olarak belirtilir. Merhaba hello GlobalMovementThrottleThreshold için varsayılan değer 1000'dir ve hello varsayılan değer hello GlobalMovementThrottleCountingInterval için 600'dür.
  - MovementPerPartitionThrottleThreshold – Bu ayar bazı zaman içinde hello hareketleri herhangi bir hizmet bölümü için toplam sayısını denetler. Merhaba süreyi saniye cinsinden hello MovementPerPartitionThrottleCountingInterval olarak belirtilir. Merhaba hello MovementPerPartitionThrottleThreshold için varsayılan değer 50'dir ve hello varsayılan değer hello MovementPerPartitionThrottleCountingInterval için 600'dür.

Bu kısıtlamaları için başlangıç yapılandırmasını hello aynı yüzde tabanlı hello azaltma olarak desen izler.

## <a name="next-steps"></a>Sonraki adımlar
- toofind hello Küme Kaynak Yöneticisi yönetir ve dengeleyen hello kümedeki yük hakkında hello makalesine üzerinde kullanıma [Yük Dengeleme](service-fabric-cluster-resource-manager-balancing.md)
- Merhaba küme Resource Manager hello küme açıklamak için birçok seçeneğiniz vardır. toofind bunlarla ilgili daha fazla bilgi, bu makalede denetleyin [açıklayan bir Service Fabric kümesi](service-fabric-cluster-resource-manager-cluster-description.md)
