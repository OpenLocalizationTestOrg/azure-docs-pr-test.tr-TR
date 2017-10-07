---
title: "Service Fabric kümesi Kaynak Yöneticisi: taşıma maliyeti | Microsoft Docs"
description: "Taşıma maliyeti Service Fabric Hizmetleri için genel bakış"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a>Hizmet taşıma maliyeti
Service Fabric kümesi Kaynak Yöneticisi hello bir faktör toodetermine hangi değişiklikleri toomake tooa küme hello bu değişiklikleri maliyetidir çalışırken göz önünde bulundurur. "Maliyet" Merhaba kavramı kapalı ne kadar hello küme karşı geliştirilebilir ticareti. Maliyet Dengeleme, birleştirme ve diğer gereksinimler için hizmetler taşırken hesaba katıldığında. Merhaba hedeftir hello toomeet hello gereksinimleri en az kesintiye uğratan veya pahalı yolu. 

Hizmetleri maliyetleri CPU süresi taşıma ve ağ bant genişliği en az. Durum bilgisi olan hizmetler için ek bellek ve disk tüketen hizmetlerin hello durumunu kopyalama gerektiriyor. Azure Service Fabric kümesi Resource Manager ile gelir bu hello çözümleri Hello maliyetini en aza indirme hello kümenin kaynakları gereksiz yere harcanan olmayan sağlamaya yardımcı olur. Ancak, hello küme kaynaklarında hello ayrılması önemli ölçüde artırmak tooignore çözümleri istemezsiniz.

Merhaba küme Resource Manager maliyetleri bilgi işlem ve toomanage hello küme denediğinde bunları sınırlama iki yolu vardır. Merhaba ilk mekanizması yalnızca onu yapacağınız her taşıma sayım. İki çözümleri ile hello oluşturuluyorsa hello Küme Kaynak Yöneticisi'ni (taşır toplam sayısı) en düşük maliyeti hello ile hello birini tercih sonra aynı (puan) dengeleyin.

Bu strateji de çalışır. Ancak varsayılan veya statik yükleri'te olduğu gibi tüm taşır eşit herhangi karmaşık sisteminde tahmin edilemez. Büyük olasılıkla toobe çok daha pahalı bazılarıdır.

## <a name="setting-move-costs"></a>Ayar maliyetleri taşıyın 
Oluşturulduğunda hello varsayılan taşıma maliyeti bir hizmet için belirtebilirsiniz:

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

C# ' TA: 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Ayrıca, belirtin veya hello hizmeti oluşturulduktan sonra MoveCost bir hizmet için dinamik olarak güncelleştir: 

PowerShell: 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

C# ' TA:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a>Taşıma maliyeti yineleme başına temelinde dinamik olarak belirtme

Merhaba önceki kod parçacıkları tüm bir tüm hizmetine aynı anda dış hello hizmetin kendisini MoveCost belirtmek için. Ancak, maliyeti en yararlı olduğu zaman taşımak hello taşıma maliyeti belirli hizmeti nesnesi, kullanım ömrü değiştirir. Merhaba kendilerini büyük olasılıkla Hizmetleri bu yana nasıl maliyetli toomove belirli bir zaman oldukları hello en iyi fikir vardır, hizmetleri tooreport çalışma zamanı sırasında tek tek kendi taşıma maliyeti için bir API yoktur. 

C# ' TA:

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a>Taşıma maliyeti etkisi
MoveCost dört düzeyi vardır: sıfır, düşük, Orta ve yüksek. MoveCosts sıfır dışında diğer, göreli tooeach ' dir. Sıfır taşıma maliyeti hareket ücretsizdir ve hello çözüm hello puan karşı saymak değil anlamına gelir. TooHigh maliyet taşınma mu ayarı *değil* garanti bu hello çoğaltma tek bir yerde kalır.

<center>
![Taşıma için çoğaltmalar seçerek bir etmen olarak taşıma maliyeti][Image1]
</center>

MoveCost neden az kesintiye genel hello ve hala eşdeğer tarihe ulaşan sırasında kolay tooachieve olan hello çözümler bulmanıza yardımcı olur. Bir hizmetin maliyeti kavramı göreli toomany şey olabilir. Merhaba, taşıma maliyeti hesaplama en yaygın unsurlar şunlardır:

- Durum veya hello hizmet toomove gereken veri miktarı Hello.
- istemci bağlantısının kesilmesi Hello maliyeti. Birincil çoğaltma taşıma genellikle daha bir ikincil çoğaltma taşıma hello maliyeti daha pahalıdır.
- yürütülen bir işlem kesintiye hello maliyeti. Bazı işlemler hello veri düzeyini depolamak veya yanıt tooa istemci çağrısında gerçekleştirilen işlemler maliyetlidir. Toostop istemediğiniz belirli bir noktadan sonra bunları için yoksa. Bu nedenle Hello işlemi sürerken taşıdığında bu hizmet nesnesi tooreduce hello olasılığını hello taşıma maliyeti artırın. Merhaba işlemi yapıldığında hello maliyeti arka toonormal ayarlayın.

## <a name="enabling-move-cost-in-your-cluster"></a>Taşıma maliyeti kümenizdeki etkinleştirme
Sırayla hesaba daha ayrıntılı MoveCosts toobe Merhaba, MoveCost kümenizdeki etkinleştirilmesi gerekir. Bu ayar olmadan taşır sayım hello varsayılan mod MoveCost hesaplamak için kullanılır ve MoveCost raporları göz ardı edilir.


ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a>Sonraki adımlar
- Service Fabric kümesi Kaynak Yöneticisi ölçümleri toomanage kullanım ve kapasite hello kümede kullanır. Ölçümler hakkında daha fazla toolearn ve nasıl tooconfigure bunları kullanıma [yönetme kaynak tüketimini ve Service Fabric yük ölçümlerle](service-fabric-cluster-resource-manager-metrics.md).
- toolearn nasıl hello Küme Kaynak Yöneticisi yönetir ve dengeleyen hello kümedeki yük hakkında kullanıma [Dengeleme Service Fabric kümesi](service-fabric-cluster-resource-manager-balancing.md).

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
