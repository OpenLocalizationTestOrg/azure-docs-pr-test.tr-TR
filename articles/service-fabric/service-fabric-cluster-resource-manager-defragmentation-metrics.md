---
title: "Azure Service Fabric ölçümlerini aaaDefragmentation | Microsoft Docs"
description: "Birleştirme kullanarak veya Service Fabric ölçümlerini için bir strateji olarak sevk bir genel bakış"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: d09045a6cf196d2771f1a0794637f4579d3eb96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a>Ölçümleri ve Service Fabric yük birleştirme
Yük ölçüm hello kümedeki yönetmek için hello Service Fabric kümesi kaynak yöneticisinin varsayılan toodistribute hello yük stratejidir. Düğümleri eşit olarak kullanıldığını sağlama tooboth Çekişme ve harcanan kaynakları sağlama sıcak ve soğuk noktalar önler. Merhaba küme iş yüklerini dağıtma hello hata belirli bir iş yükü büyük bir yüzdesini almaz sağlar beri hataları sürdüren açısından güvenli olur. 

Merhaba Service Fabric kümesi Kaynak Yöneticisi, birleştirme olan yük yönetmek için farklı bir strateji desteklemiyor. Birleştirme toodistribute hello kullanım ölçüm Merhaba kümede çalışırken yerine onu birleştirilir olduğunu anlamına gelir. Birleştirme yalnızca bir ters çevirmeyi hello ortalama standart sapmasını ölçüm yükü en aza yerine stratejisi – Dengeleme hello varsayılan, hello Küme Kaynak Yöneticisi'ni çalışır tooincrease onu.

## <a name="when-toouse-defragmentation"></a>Zaman toouse birleştirme
Merhaba kümedeki yük dağıtma, bazı hello kaynaklara her düğümde tüketir. Bazı iş yükleri olağanüstü büyük ve çoğu veya hepsi bir düğümün tüketen Hizmetleri oluşturun. Bu durumda olduğunda büyük yeterli hiç oluşturulan iş yükleri bunları herhangi düğümü toorun boşluk mümkündür. Büyük iş yüklerini Service Fabric bir sorun değildir; Bu durumlarda hello tooreorganize hello küme toomake yer büyük bu iş yükü için ihtiyaç duyduğu Küme Kaynak Yöneticisi'ni belirler. Ancak, hello hello kümede zamanlanmış toowait toobe sırada iş yükü vardır.

Daha sonra birçok Hizmetleri ve geçici bir çözüm durumu toomove varsa hello kümede yerleştirilen hello büyük iş yükü toobe uzun bir süredir ele geçirebilir. Merhaba kümedeki diğer iş yükleri de büyük varsa ve bu nedenle uzun tooreorganize ele daha yüksektir. Merhaba Service Fabric ekip oluşturma zamanları ile bu senaryonun benzetimleri ölçülür. %30 ve % 50 arasında yukarıdaki Küme kullanımı var hemen büyük hizmetleri oluşturma çok uzun sürdüğü bulduk. toohandle bu senaryo, biz birleştirme karşı bir strateji olarak sunulmuştur. Büyük iş yükleri için özellikle olanları oluşturulma zamanı birleştirme gerçekten bu yeni iş yüklerine Yardım önemli olduğu hello kümede zamanlanmış bulduk.

Daha az düğümlerin içine birleştirme ölçümleri toohave hello küme Resource Manager tooproactively try toocondense hello yük hello Hizmetleri yapılandırabilirsiniz. Bu, olduğunu neredeyse her zaman hello küme yeniden düzenleme olmadan büyük Hizmetleri için yeriniz sağlamaya yardımcı olur. Tooreorganize hello küme olmamasından büyük iş yüklerini hızlı oluşturma sağlar.

Çoğu kişi birleştirme gerek yoktur. Hizmetleri olan genellikle küçük, sabit toofind odada onlar için hello küme olmadığı için. Düzenlenmesi mümkün olduğunda, çünkü çoğu Hizmetleri küçük ve hızlı bir şekilde ve paralel taşınabilir öğeyi hızlı bir şekilde, yeniden başlatılır. Hizmetleri, büyük ve bunları hızlı bir şekilde oluşturulan gereksinim ardından hello ancak birleştirme stratejisi sizin için olur. Biz birleştirme sonraki kullanmanın hello bileşim ele alacağız. 

## <a name="defragmentation-tradeoffs"></a>Birleştirme bileşim
Daha fazla hizmet başarısız düğümleri üzerinde çalışan bu yana birleştirme hataları, impactfulness artırabilir. Merhaba küme kaynaklarında büyük iş yüklerini hello oluşturulması için bekleyen ayırma tutulması gereken beri birleştirme maliyetleri de artırabilirsiniz.

Hello Aşağıdaki diyagramda iki küme görsel gösterimi, birleştirilmiş diğeri olmayan sağlar. 

<center>
![Karşılaştırma ve dengeli kümeleri birleştirilmiş][Image1]
</center>

Dengeli hello durumda gerekli tooplace hello en büyük hizmet nesnelerden biri olacak hareketleri hello sayısını göz önünde bulundurun. Merhaba birleştirilmiş kümede hello büyük iş yükü diğer hizmetler toomove toowait gerek kalmadan dört veya beş düğümlerinde yerleştirilemedi.

## <a name="defragmentation-pros-and-cons"></a>Birleştirme Artıları ve eksileri
Bu nedenle bu diğer kavramsal bileşim nelerdir? Hakkında hızlı bir şeyler toothink tablosu aşağıdadır:

| Birleştirme uzmanları | Birleştirme simgeler |
| --- | --- |
| Büyük Hizmetleri daha hızlı oluşturulmasını sağlar |Concentrates Çekişme artırma daha az düğümü yükleme |
| Etkinleştirir veri taşıma oluşturma sırasında düşürün. |Hataları daha fazla hizmet etkileyebilir ve daha fazla karmaşası neden |
| Alan geri kazanma ve gereksinimleri zengin açıklaması sağlar |Daha karmaşık genel kaynak yönetimi yapılandırma |

Birleştirilmiş karıştırabilirsiniz ve aynı küme normal ölçümlerini hello. Merhaba Küme Kaynak Yöneticisi'ni çalışır tooconsolidate hello birleştirme ölçümleri yaymak sırasında mümkün olduğunca başkalarının hello. Birleştirme karıştırma ve stratejileri Dengeleme hello sonuçları dahil olmak üzere çeşitli etkenlere bağlıdır:
  - Birleştirme ölçümleri hello sayısı ve ölçümleri Dengeleme hello sayısı
  - Herhangi bir hizmet ölçümleri her iki tür kullanıp kullanmadığını 
  - Merhaba ölçüm ağırlığı
  - Geçerli ölçüm yükler
  
Deneme gerekli toodetermine hello tam gerekli yapılandırmadır. Birleştirme ölçümleri üretimde etkinleştirmeden önce iş yüklerinin kapsamlı ölçüm öneririz. Bu birleştirme ve dengeli ölçümleri hello içinde karıştırılması durumlarda özellikle geçerlidir aynı hizmet. 

## <a name="configuring-defragmentation-metrics"></a>Birleştirme ölçümleri yapılandırma
Birleştirme ölçümleri yapılandırma bir genel hello kümedeki bir karardır ve tek tek ölçümleri birleştirme için seçilebilir. config parçacıkları aşağıdaki hello nasıl tooconfigure ölçümlerini birleştirme gösterir. Bu durumda, "Metric2" normalde dengeli toobe devam ederken "Metric1" bir birleştirme ölçü olarak yapılandırılır. 

ClusterManifest.xml:

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a>Sonraki adımlar
- Merhaba küme Resource Manager hello küme açıklamak için adam seçenekleri vardır. toofind bunlarla ilgili daha fazla bilgi, bu makalede denetleyin [açıklayan bir Service Fabric kümesi](service-fabric-cluster-resource-manager-cluster-description.md)
- Kullanım ve kapasite hello kümedeki hello Service Fabric kümesi kaynak yöneticisi nasıl yönettiğini ölçümleridir. Ölçümler hakkında daha fazla toolearn ve nasıl tooconfigure bunları kullanıma [bu makalede](service-fabric-cluster-resource-manager-metrics.md)

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
