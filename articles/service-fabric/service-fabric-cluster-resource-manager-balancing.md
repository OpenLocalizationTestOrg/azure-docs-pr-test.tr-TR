---
title: "aaaBalance Azure Service Fabric kümesi | Microsoft Docs"
description: "Bir giriş toobalancing kümenizle hello Service Fabric kümesi Resource Manager."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a>Service fabric kümesi Dengeleme
Merhaba Service Fabric kümesi Kaynak Yöneticisi, dinamik yük değişiklikleri, tanımlandığında tooadditions veya düğümler veya hizmetleri kaldırma işlemleri destekler. Bir kısıtlama ihlali de otomatik olarak düzeltir ve önceden hello küme yeniden dengeler. Ancak bu eylemler ne sıklıkta alınır ve bunları tetikleyen?

Küme Kaynak Yöneticisi'ni gerçekleştirir bu hello iş üç farklı kategorisi vardır. Bunlar:

1. Yerleştirme – bu aşamada herhangi bir durum bilgisi olan çoğaltmaları veya eksik olan durum bilgisiz örnekleri yerleştirme ile ilgilidir. Yerleştirme, hem yeni hizmetleri hem de işleme durum bilgisi olan çoğaltmaları veya başarısız olan durum bilgisiz örnekleri içerir. Silme ve çoğaltmalar veya örnekleri bırakma burada ele alınır.
2. Kısıtlama denetler – Bu aşama olup olmadığını denetler ve hello farklı yerleştirme kısıtlamaları (kurallar) hello sistem içinde ihlalleri düzeltir. Düğümler kapasite değildir ve bir hizmetin kısıtlamalarından karşılandığından emin olduktan gibi şeyler kuralları örnekleridir.
3. Dengeleme – bu aşama dengelenmesi üzerinde yapılandırılmış hello dayalı gerekliyse toosee istenen farklı ölçümleri bakiyesini düzeyini denetler. Öyleyse hello bir düzende küme diğer bir deyişle daha dengeli toofind çalışır.

## <a name="configuring-cluster-resource-manager-timers"></a>Küme Kaynak Yöneticisi zamanlayıcıları yapılandırma
Merhaba ilk Dengeleme geçici denetimleri kümesini zamanlayıcılar kümesidir. Bu zamanlayıcılar ne sıklıkta hello küme Resource Manager hello küme inceler ve düzeltici eylemleri gerçekleştirir yönetir.

Küme Kaynak Yöneticisi yapabilir düzeltmeleri hello farklı bu türlerinin her biri kendi sıklığı yöneten farklı bir Zamanlayıcı tarafından denetlenir. Her Zamanlayıcı başlatıldığında başlangıç görevi zamanlandı. Varsayılan olarak, Resource Manager hello:

* durumu tarar ve güncelleştirmeleri (örneğin, bir düğümü çalışmıyor kayıt) uygular her 1/saniyede 10
* Merhaba yerleştirme onay bayrağını ayarlar 
* saniyede Hello kısıtlaması onay bayrağını ayarlar
* beş saniyede bayrağı Dengeleme hello ayarlar.

Aşağıda bu zamanlayıcılar yöneten hello yapılandırma örnekleri şunlardır:

ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

Bugün hello küme kaynak yöneticisi yalnızca bu eylemlerden biri, aynı anda sırayla gerçekleştirir. "En düşük aralıkları" olarak toothese zamanlayıcılar bakın ve hello zamanlayıcılar "ayarı bayrakları" devre dışı olduğunda gerçekleştirilecek eylemleri hello nedeni budur. Örneğin, küme Resource Manager, bekleyen mvc'deki hello hello küme Dengeleme önce toocreate Hizmetleri ister. Belirtilen hello varsayılan zaman aralıklarıyla görebileceğiniz gibi hello küme kaynak yöneticisi için herhangi bir şey bu gereksinimlerini toodo sık tarar. Normalde bu her adımı sırasında yapılan değişiklikler hello kümesi küçük anlamına gelir. Şeyler hello kümede gerçekleştiğinde sık olarak küçük değişiklikler hello küme Resource Manager toobe yanıt verir. Merhaba varsayılan zamanlayıcılar bazı birçok hello itibaren aynı toplu işleme sağlamak olay türleri toooccur aynı anda eğilimi gösterir. 

Örneğin, başarısız olduğunda düğümleri aynı anda kadar tüm hata etki alanlarını yapabilirsiniz. Tüm bu hatalar hello sonraki durum sırasında yakalanan güncelleştirme hello sonra *PLBRefreshGap*. Merhaba düzeltmeleri yerleştirme, kısıtlama denetimi aşağıdaki ve çalıştırmalarını Dengeleme hello sırasında belirlenir. Varsayılan hello tarafından küme Resource Manager değil hello kümesindeki değişiklikleri saatlik aracılığıyla tarama ve tooaddress tüm değişiklikleri aynı anda çalışıyor. Bunun yapılması karmaşası toobursts sunulmasını sağlar.

Merhaba küme hello Küme Kaynak Yöneticisi ayrıca bazı ek bilgiler toodetermine imbalanced gerekir. İçin sahip olduğumuz iki parça yapılandırma: *BalancingThresholds* ve *ActivityThresholds*.

## <a name="balancing-thresholds"></a>Dengeleme eşikleri
Dengeleme eşik dengelenmesi tetiklemek hello ana denetimdir. Merhaba Dengeleme eşik bir ölçüm için ise bir _oranı_. Merhaba üzerinde bir ölçüm için Hello yükü en hello yük miktarı az yüklenen hello bölü düğümü yüklerse Bu ölçüm 's düğümü aşıyor *BalancingThreshold*, hello küme imbalanced olur. Sonuç olarak Dengeleme küme Resource Manager denetler tetiklenen hello sonraki zaman hello olur. Merhaba *MinLoadBalancingInterval* Zamanlayıcı tanımlar dengelenmesi gerekliyse, ne sıklıkta hello küme Resource Manager denetlemeniz gerekir. Denetimi, herhangi bir şey olur anlamına gelmez. 

Dengeleme eşikleri hello küme tanımının bir parçası olarak ölçüm başına temelinde tanımlanır. Ölçümler hakkında daha fazla bilgi için kullanıma [bu makalede](service-fabric-cluster-resource-manager-metrics.md).

ClusterManifest.xml

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<center>
![Eşik örnek Dengeleme][Image1]
</center>

Bu örnekte, her hizmetin bazı ölçüsünün bir birimi kullanıyor. Merhaba üst örnekte, bir düğümde en fazla yük hello beş ve hello en az iki. Bu ölçüm eşiği Dengeleme bu hello üç olduğunu düşünelim. Merhaba oranı hello kümedeki 5/2 olduğundan 2.5 ve bu, üç, hello küme eşiğinin dengeleme dengeli hello belirtilenden azdır =. Merhaba küme Resource Manager denetlediğinde dengelemesiz tetiklenir.

Merhaba en az iki oranı beş içinde kaynaklanan ederken hello altındaki örnekte, bir düğümde en fazla yük hello 10 ' dur. Beş hello belirlenen karşı eşiğinin Bu ölçüm için üç değerinden daha büyük. Sonuç olarak, yeniden dengelenemiyor Çalıştır sonraki zamanlanan saat hello Zamanlayıcı ateşlenir Dengeleme olacaktır. Böyle bir durumda bazı genellikle dağıtılmış tooNode3 yüktür. Merhaba Service Fabric kümesi Kaynak Yöneticisi doyumsuz bir yaklaşım kullanmadığı için bazı yükleme dağıtılmış tooNode2 de olabilir. 

<center>
![Eşik örnek Eylemler Dengeleme][Image2]
</center>

> [!NOTE]
> "Dengeleme" Yük kümenizdeki yönetmek için iki farklı stratejileri işler. Küme Kaynak Yöneticisi'ni kullanır hello hello varsayılan stratejisi toodistribute hello kümedeki hello düğümler arasında yüktür. Merhaba diğer stratejidir [birleştirme](service-fabric-cluster-resource-manager-defragmentation-metrics.md). Birleştirme sırasında hello gerçekleştirilen Dengeleme aynı çalıştırın. Merhaba Dengeleme ve birleştirme stratejilerini hello içinde farklı ölçümleri kullanılabilir aynı küme. Bir hizmetin Dengeleme ve birleştirme ölçümleri olabilir. Birleştirme ölçümlerini hello hello oranını yükler olduğunda dengelenmesi hello küme Tetikleyicileri _aşağıda_ eşik Dengeleme hello. 
>

Eşik Dengeleme hello alma, açık bir hedef değil. Dengeleme eşikleri olan yalnızca bir *tetikleyici*. Çalıştırır Dengeleme olduğunda hello küme Resource Manager bunu yapabilirsiniz, hangi iyileştirmeleri varsa belirler. Karşı arama yalnızca koparılan devre dışı olduğundan, hiçbir şey taşır anlamına gelmez. Bazen hello imbalanced ancak çok kısıtlanmış toocorrect kümedir. Alternatif olarak, çok hareketleri hello geliştirmeleri gerektiren [pahalı](service-fabric-cluster-resource-manager-movement-cost.md)).

## <a name="activity-thresholds"></a>Etkinlik eşikleri
Düğümleri görece imbalanced olsa da, bazı durumlarda, hello *toplam* hello kümedeki yük miktarı düşük. Yük Hello eksikliği geçici DIP olabilir veya hello kümesi yeni ve yalnızca alma olduğundan önyükleme içinde. Her iki durumda da, elde edilen az toobe olduğundan Dengeleme hello kümesi toospend zaman istemeyebilirsiniz. Dengeleme Hello küme yapılan, ağ harcamanız ve her büyük yapmadan kaynakları toomove şeyler geçici işlem *mutlak* fark. gereksiz tooavoid taşır, etkinlik eşikleri bilinen başka bir denetim yoktur. Etkinlik eşikleri etkinliği için bazı mutlak alt sınır toospecify sağlar. Hiçbir düğümü bu eşiğin üstünde ise, hello Dengeleme eşiğine olsa bile Dengeleme tetiklenen değil.

Biz bizim Dengeleme eşiğinin Bu ölçüm için üç korumak varsayalım. Ayrıca 1536 etkinlik eşiğinin sahibiz varsayalım. Hello ilk durumda, hello küme hello imbalanced olsa eşik Dengeleme var. hiçbir düğüm karşılıyor bu etkinlik eşik, böylece hiçbir şey olmaz. Merhaba altındaki örnekte Düğüm1 etkinlik eşik hello ' dir. Her ikisi de Dengeleme eşik hello hello ölçüm Merhaba etkinlik eşiği aşıldı yana Dengeleme zamanlanır. Örnek olarak, diyagram aşağıdaki hello bakalım: 

<center>
![Etkinlik eşik örneği][Image3]
</center>

Yalnızca Dengeleme eşikleri gibi etkinlik eşikleri tanımlı başına Metrik hello Küme tanımı aracılığıyla şunlardır:

ClusterManifest.xml

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

Yük Dengeleme ve etkinlik eşiklere hem bağlı tooa belirli ölçüm Dengeleme - yalnızca her ikisi de Dengeleme eşik hello ve etkinlik eşiği Merhaba aşıldı tetiklenir aynı Ölçüm.

## <a name="balancing-services-together"></a>Hizmetleri birlikte Dengeleme
Merhaba küme imbalanced olup olmadığını küme çapında bir karardır. Ancak, düzeltme hakkında Git hello şekilde bireysel hizmet çoğaltmaları ve geçici örnekleri taşımaktır. Bu doğru mantıklıdır? Bellek bir düğümde yığılmış, birden çok çoğaltmalar veya örnekleri tooit katılan. Giderilmesi hello dengesizliği herhangi hello durum bilgisi olan çoğaltmaları veya hello imbalanced ölçümün kullanmak durum bilgisiz örneklerinin hareketli gerektirebilir.

Bazen imbalanced kendisini değildi bir hizmet taşınmış ancak (yerel hello tartışma unutmayın ve daha önce genel ağırlık verir). Tüm bu hizmetin ölçümleri dengeli neden bir hizmet taşındığında? Bir örnek görelim:

- Dört Hizmetleri, Service1, Service2, Service3 ve Service4 varsayalım. 
- Service1 ölçümleri Metric1 ve Metric2 bildirir. 
- Service2 ölçümleri Metric2 ve Metric3 bildirir. 
- Service3 ölçümleri Metric3 ve Metric4 bildirir.
- Service4 ölçüm Metric99 bildirir. 

Burada burada yapacağız kötülerinden görebilirsiniz: bir zinciri! Biz gerçekten dört bağımsız Hizmetleri yoksa, ilişkili üç hizmeti ve kendi başına kapalıdır bir sunuyoruz.

<center>
![Hizmetleri birlikte Dengeleme][Image4]
</center>

Bu zincir nedeniyle bir dengesizliği ölçümleri 1-4, çoğaltmalar veya örnekleri tooservices ait geçici 1-3 toomove neden olabilir. Ölçümleri 1, 2 veya 3 içinde bir dengesizliği içinde Service4 hareketleri sebep olamaz biliyoruz. Merhaba çoğaltmaları taşıyarak bu yana hiçbir noktası olacaktır veya can geçici tooService4 ait örnekleri kesinlikle hiçbir şey yapmak tooimpact hello Bakiye ölçümleri 1-3.

Merhaba Küme Kaynak Yöneticisi'ni otomatik olarak hangi hizmetlerin ilgili rakamlar. Ekleme, kaldırma veya hizmetleri için değişen hello ölçümleri ilişkilerini etkileyebilir. Örneğin, güncelleştirilmiş tooremove Metric2 Service2 Dengeleme iki çalışmaları arasında olabilir. Service1 Service2 arasındaki hello zinciri keser. Şimdi yerine iki grup ilgili hizmetlerin vardır üç:

<center>
![Hizmetleri birlikte Dengeleme][Image5]
</center>

## <a name="next-steps"></a>Sonraki adımlar
* Kullanım ve kapasite hello kümedeki hello Service Fabric kümesi kaynak yöneticisi nasıl yönettiğini ölçümleridir. Ölçümler hakkında daha fazla toolearn ve nasıl tooconfigure bunları kullanıma [bu makalede](service-fabric-cluster-resource-manager-metrics.md)
* Taşıma maliyeti belirli hizmetleri diğerlerinden daha pahalı toomove olduğunu toohello küme Resource Manager sinyal bir yoludur. Taşıma maliyeti hakkında daha fazla bilgi için çok başvuran[bu makalede](service-fabric-cluster-resource-manager-movement-cost.md)
* Merhaba küme Resource Manager hello kümede karmaşası aşağı tooslow yapılandırabilirsiniz birkaç kısıtlamaları vardır. Bunlar normalde gerekli değildir, ancak bunlara ihtiyacınız varsa bunları hakkında bilgi edinebilirsiniz [burada](service-fabric-cluster-resource-manager-advanced-throttling.md)

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
