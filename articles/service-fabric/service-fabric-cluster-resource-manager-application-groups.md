---
title: "aaaService doku Küme Kaynak Yöneticisi - uygulama grupları | Microsoft Docs"
description: "Hello uygulama grubu işlevindeki hello Service Fabric kümesi Kaynak Yöneticisi'ne genel bakış"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a>Giriş tooApplication grupları
Service Fabric'ın Küme Kaynağı Yöneticisi genellikle hello yük dengelemesini yaparak küme kaynaklarını yönetir (aracılığıyla temsil [ölçümleri](service-fabric-cluster-resource-manager-metrics.md)) hello kümesi boyunca eşit. Service Fabric yönetir hello ve hello kümede hello düğümler hello kapasitesini bir bütün olarak [kapasite](service-fabric-cluster-resource-manager-cluster-description.md). Ölçümleri ve kapasite birçok iş yükü, ancak bazen ek gereksinimleri Getir yoğun olarak kullanılır farklı hizmet doku uygulama örnekleri desenleri harika çalışır. Örneğin, isteyebilirsiniz:

- Yedek hello kümedeki hello düğümlere bazı kapasite bazı Adlandırılmış uygulama örneği içindeki hello hizmetler için
- (Bunları hello tüm küme yaymak) yerine adlandırılmış uygulama örneği içinde hello hizmetleri üzerinde çalışan düğümleri Hello toplam sayısını sınırla
- Kapasiteleri hello adlandırılmış Uygulama örneğinin kendisinde toolimit hello hello Hizmetleri içindeki hizmetler veya toplam kaynak tüketimini sayısını tanımlayın.

Bu gereksinimleri hello Service Fabric kümesi Kaynak Yöneticisi toomeet uygulama grupları adlı bir özelliği destekler.

## <a name="limiting-hello-maximum-number-of-nodes"></a>Merhaba en fazla düğüm sayısını sınırlandırma
Uygulama örneğini gerektiğinde Merhaba basit kullanım uygulama kapasitesi toobe tooa belirli maksimum düğüm sayısı sınırlı bir durumdur. Bu uygulama örneği makine kümesi sayısı üzerine içindeki tüm hizmetler birleştirir. Birleştirme toopredict çalıştığınız ya da bu adlandırılmış uygulama örneği içindeki hello hizmetler tarafından fiziksel kaynak kullanımını cap faydalıdır. 

Merhaba aşağıdaki resimde bir uygulama örneği ile ve tanımlanan düğüm sayısı üst sınırı olmadan gösterilmektedir:

<center>
![Uygulama örneği en fazla düğüm sayısını tanımlama][Image1]
</center>

Merhaba sol örnekte hello uygulama tanımlı düğüm sayısı üst sınırı yok ve üç hizmeti vardır. Hello küme Resource Manager altı kullanılabilir düğümler tooachieve hello iyi dengeyi hello kümedeki (Merhaba, varsayılan davranıştır) üzerinden tüm çoğaltmaları yayılır. Merhaba sağ örnekte, biz hello bkz aynı uygulama sınırlı toothree düğümleri.

Bu davranışı denetler hello parametre en fazla düğüm adı verilir. Bu parametre uygulama oluşturma sırasında ayarlayın veya zaten çalışan bir uygulama örneği için güncelleştirilmiştir.

PowerShell

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

C#

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

Düğümleri Hello kümesinde hello Küme Kaynak Yöneticisi'ni hangi hizmet nesnelerin araya yerleştirilen veya hangi düğümlerin alışmanız garanti etmez.

## <a name="application-metrics-load-and-capacity"></a>Uygulama ölçümleri, yükü ve kapasite
Uygulama grupları ayrıca belirli adlandırılmış uygulama örneği ve bu ölçümleri için o uygulama örneğinin kapasitesi ile ilişkili toodefine ölçümleri sağlar. Uygulama ölçümleri tootrack, ayrılmış ve o uygulama örneğinin içine hello Hizmetleri sınırı hello kaynak tüketimini izin verir.

Her uygulama ölçümü için ayarlanabilir iki değer vardır:

- **Toplam uygulama kapasitesinin** – Bu ayar hello hello uygulama belirli bir ölçüm için toplam kapasitesini temsil eder. Merhaba Küme Kaynak Yöneticisi'ni yeni hizmetlerin toplam yük tooexceed bu değer neden olacağından bu uygulama örneği içinde hello oluşturulmasına izin vermez. Örneğin, hello uygulama örneği 10 kapasitesine sahip ve beş yükünü zaten varsayalım. 10 toplam varsayılan yükü olan bir hizmeti Hello oluşturulması izin verilmeyen.
- **En fazla düğüm kapasitesi** – Bu ayar, tek bir düğümde hello uygulama için en fazla toplam yükleme hello belirtir. Yük bu kapasite kalırsa, hello küme Resource Manager hello yükü azaldıktan çoğaltmaları tooother düğümleri taşır.


PowerShell:

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

C# ' TA:

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a>Kapasite ayırma
Başka bir ortak için uygulama grupları içindeki kaynaklara küme hello tooensure verilen uygulama örneği için ayrılmış kullanılmasıdır. Merhaba uygulama örneği oluşturulduğunda hello alanı her zaman ayrılır.

Bile Merhaba uygulaması hemen gerçekleşir hello küme alanı ayırma:
- Merhaba uygulama örneği oluşturulur ancak hizmetlerin içindeki henüz yok
- Merhaba uygulama örneği değişiklikleri her zaman içindeki Hizmetler Hello sayısı 
- Merhaba Hizmetleri var, ancak hello kaynakları tüketen değil 

İki ek parametreler belirtmek uygulama örneğini gerektirir kaynaklarını ayırma: *düğüm* ve *NodeReservationCapacity*

- **En az düğüm** -hello minimum sayısını tanımlar uygulaması hello düğümlerinin örneği çalıştırmanız gerekir.  
- **NodeReservationCapacity** -Merhaba uygulaması için ölçüm başına Bu ayar değildir. Merhaba, burada, hizmetleri çalıştırma Bu uygulamadaki hello herhangi bir düğümde Merhaba uygulaması için ayrılmış bu ölçüm, hello miktarını değerdir.

Birleştirme **düğüm** ve **NodeReservationCapacity** hello kümedeki hello uygulama için en düşük yük ayırma güvence altına alır. Daha az kalan varsa hello kapasite küme hello toplam rezervasyon gerekli, Merhaba uygulaması oluşturma başarısız olur. 

Kapasite ayırma bir örneğe bakalım:

<center>
![Uygulama örnekleri ayrılmış Kapasite tanımlama][Image2]
</center>

Merhaba sol örnekte, uygulamaları herhangi uygulama tanımlı kapasiteye sahip değil. Merhaba Küme Kaynağı Yöneticisi her şeyi toonormal kurallarına göre dengeler.

Merhaba sağ üzerinde Hello örnekte Application1 ayarları aşağıdaki hello ile oluşturulmuş varsayalım:

- En az düğüm kümesi tootwo
- Bir uygulama ile tanımlanmış ölçümü
  - 20 NodeReservationCapacity

PowerShell

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

C#

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

Service Fabric Application1 için iki düğüm üzerinde kapasite ayırır ve olsa bile herhangi bir yük Application1 içinde hello Hizmetleri tarafından hello zamanında kullanılan Uygulama2 dizinlerini tooconsume Hizmetleri'nden kapasiteyi izin vermez. Bu ayrılmış uygulama kapasite tüketilen ve kapasite o düğümde ve hello kümedeki kalan hello düşülür değerlendirilir.  Merhaba ayırma küme kapasite hemen kalan hello çıkarılır, hello ayrılmış ancak yalnızca en az bir hizmet nesnesi üzerinde yerleştirildiğinde tüketim belirli bir düğümün hello kapasiteden çıkarılır. Kaynaklar yalnızca gerekli olduğunda düğümlerinde ayrılmış bu daha sonra bu ayırma esneklik ve daha iyi kaynak kullanımı için sağlar.

## <a name="obtaining-hello-application-load-information"></a>Merhaba uygulama yükleme bilgilerini alma
Bir uygulama için bir veya daha fazla ölçümleri tanımlanan kapasiteye sahip her bir uygulama için hello hizmetlerinin çoğaltmaları tarafından bildirilen hello birleşik yükleme hakkında bilgi edinebilirsiniz.

PowerShell:

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

C#

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

Merhaba ApplicationLoad sorgu hello hello uygulama için belirtilen uygulama kapasitesi hakkında temel bilgiler döndürür. Bu bilgiler hello Minimum düğümleri ve en fazla düğüm bilgileri ve hello uygulama şu anda kullandığı hello numarasını içerir. Ayrıca her uygulamayı yük ölçüm hakkında bilgi içerir dahil olmak üzere:

* Ölçüm adı: Hello ölçüm adıdır.
* Ayırma kapasitesi: hello kümede bu uygulama için ayrılmış küme kapasitesi.
* Uygulama yük: Bu uygulamanın alt çoğaltmalarının toplam yük.
* Uygulama kapasitesi: İzin verilen en yüksek uygulama yük değeri.

## <a name="removing-application-capacity"></a>Uygulama kapasite kaldırma
Merhaba uygulama kapasite parametreleri için bir uygulama ayarlandıktan sonra güncelleştirme uygulama API'leri veya PowerShell cmdlet'leri kullanılarak kaldırılabilir. Örneğin:

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

Bu komut tüm uygulama kapasite yönetim parametreleri hello uygulama örneğinden kaldırır. Bu düğüm, en fazla düğüm ve hello uygulamanın ölçümleri varsa içerir. Merhaba komutu Hello etkisini hemen uygulanır. Bu komut tamamlandıktan sonra hello küme Resource Manager hello varsayılan davranışı uygulamaları yönetmek için kullanır. Uygulama kapasite parametreleri belirtilebilir yeniden aracılığıyla `Update-ServiceFabricApplication` / `System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.

### <a name="restrictions-on-application-capacity"></a>Uygulama kapasite kısıtlamalar
Dikkate alınması gereken uygulama kapasite parametreleri bazı kısıtlamalar vardır. Doğrulama hatası varsa herhangi bir değişiklik gerçekleşir.

- Tüm tamsayı parametreleri negatif olmayan sayı olması gerekir.
- En az düğüm asla en fazla düğüm büyük olmalıdır.
- Ardından bir yük ölçümü için kapasiteler tanımlanmışsa, bu kurallara uymalıdır:
  - Düğüm ayırma kapasitesi en fazla düğüm kapasitesi büyük olmamalıdır. Örneğin, hello düğümü tootwo birimlerdeki hello ölçüm "CPU" Merhaba kapasiteyi sınırlamak ve her düğümde tooreserve üç birimleri deneyin.
  - En fazla düğüm belirtilirse, en fazla düğüm ve en fazla düğüm kapasitesi hello ürün toplam uygulama kapasiteden büyük olmamalıdır. Örneğin, "CPU" tooeight ayarlanır yük ölçümü için en fazla düğüm kapasitesi hello varsayalım. Ayrıca hello en fazla düğüm too10 ayarladığınızı varsayalım. Bu durumda, toplam uygulama kapasitesinin Bu yük ölçüm için 80'den büyük olmalıdır.

Merhaba kısıtlamaları, hem uygulama oluşturma ve güncelleştirme sırasında zorlanır.

## <a name="how-not-toouse-application-capacity"></a>Değil toouse nasıl uygulama kapasite
- Toouse hello uygulama grubu özellikleri tooconstrain hello uygulama tooa çalışmayın _belirli_ alt düğümleri kümesi. Diğer bir deyişle, hello uygulamanın en fazla beş düğümlerinde çalıştığını belirtebilirsiniz, ancak hello kümedeki belirli hangi beş düğümü. Bir uygulama toospecific sınırlama düğümleri kısıtlamalarından Hizmetleri kullanarak elde edilebilir.
- Aynı uygulama üzerinde yerleştirilir hello iki Hizmetleri'nden aynı düğümlerine hello toouse hello uygulama kapasite tooensure çalışmayın. Bunun yerine kullanın [benzeşim](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) veya [kısıtlamalarından](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).

## <a name="next-steps"></a>Sonraki adımlar
- Hizmetleri yapılandırma hakkında daha fazla bilgi için [hizmetleri yapılandırma hakkında bilgi edinin](service-fabric-cluster-resource-manager-configure-services.md)
- toofind hello Küme Kaynak Yöneticisi yönetir ve dengeleyen hello kümedeki yük hakkında hello makalesine üzerinde kullanıma [Yük Dengeleme](service-fabric-cluster-resource-manager-balancing.md)
- Merhaba baştan başlatın ve [giriş toohello Service Fabric kümesi Kaynak Yöneticisi Al](service-fabric-cluster-resource-manager-introduction.md)
- Ölçümleri genellikle nasıl çalıştığı hakkında daha fazla bilgi için okumaya devam [Service Fabric yük ölçümleri](service-fabric-cluster-resource-manager-metrics.md)
- Merhaba küme Resource Manager hello küme açıklamak için birçok seçeneğiniz vardır. toofind bunlarla ilgili daha fazla bilgi, bu makalede denetleyin [açıklayan bir Service Fabric kümesi](service-fabric-cluster-resource-manager-cluster-description.md)

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
