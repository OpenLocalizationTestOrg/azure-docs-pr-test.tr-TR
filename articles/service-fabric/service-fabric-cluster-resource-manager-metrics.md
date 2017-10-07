---
title: "Ölçümleri kullanarak aaaManage Azure mikro hizmet yük | Microsoft Docs"
description: "Service Fabric toomanage tooconfigure ve kullanım ölçümlerini kaynak tüketimini nasıl hizmet hakkında bilgi edinin."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 0d622ea6-a7c7-4bef-886b-06e6b85a97fb
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 592dc749ce30683a1e439a702b7d0dc0a638276f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-resource-consumption-and-load-in-service-fabric-with-metrics"></a>Kaynak tüketimini ve Service Fabric yük ölçümlerle yönetme
*Ölçümleri* , hizmetleri çok değer verdiğiniz ve hangi hello kümedeki hello düğümler tarafından sağlanan hello kaynaklardır. Bir sipariş performansını tooimprove veya İzleyicisi Merhaba hizmetlerinizi toomanage istediğiniz herhangi bir şey ölçümüdür. Örneğin, hizmetiniz aşırı yüklüyse bellek tüketimi tooknow izlemek. Başka bir hello hizmeti bellek az sipariş tooget daha iyi performans kısıtlı olduğu başka bir yerde olup taşıma çıkışı toofigure kullanılır.

Bellek, Disk ve CPU kullanımı gibi şeyleri ölçümler gösterilebilir. Bu ölçümler fiziksel, yönetilen toobe gereken hello düğümde toophysical kaynakları karşılık kaynakları ölçümleridir. Ölçümleri de olabilir (ve genellikle olan) mantıksal ölçümleri. Mantıksal ölçümleri "MyWorkQueueDepth" veya "MessagesToProcess" veya "TotalRecords" gibi noktalardır. Mantıksal ölçümleri uygulama tanımlı ve dolaylı olarak toosome fiziksel kaynak tüketimini karşılık gelir. Sabit toomeasure ve rapor hizmeti başına temelinde fiziksel kaynakları tüketiminin olabileceğinden mantıksal ölçümleri yaygındır. Merhaba karmaşıklığını ölçme ve fiziksel ölçümlerinizi raporlama ayrıca neden Service Fabric bazı varsayılan ölçümleri sağlar olur.

## <a name="default-metrics"></a>Varsayılan ölçümleri
Yazma ve hizmet dağıtımı başladı tooget istediğinizi düşünelim. Bu noktada içereceği tükettiği hangi fiziksel veya mantıksal kaynakları bilinmiyor. Uygundur! diğer bir ölçümleri belirtildiğinde hello Service Fabric kümesi Kaynak Yöneticisi bazı varsayılan ölçümleri kullanır. Bunlar:

  - PrimaryCount - hello düğümde birincil çoğaltmalara sayısı 
  - ReplicaCount - hello düğümde toplam durum bilgisi olan çoğaltmaların sayısı
  - Sayısı - tüm hizmet nesnelerde (durum bilgisiz ve durum bilgisi olan) hello düğüm sayısı

| Ölçüm | Durum bilgisiz örneği yükleme | Durum bilgisi olan ikincil yükleme | Durum bilgisi olan birincil yükleme |
| --- | --- | --- | --- |
| PrimaryCount |0 |0 |1 |
| ReplicaCount |0 |1 |1 |
| Sayı |1 |1 |1 |

Temel iş yükleri için makul bir dağıtım hello küme iş hello varsayılan ölçümleri sağlar. Aşağıdaki örneğine hello iki hizmetleri oluşturmak ve Dengeleme hello varsayılan ölçümleri Bel ne olur görelim. Merhaba ilk üç bölümleri olan bir durum bilgisi olan hizmet hizmetidir ve bir hedef çoğaltma üç boyutunu ayarlayın. Merhaba ikinci hizmeti, bir bölüm ve bir örnek sayısını üç ile durumsuz bir hizmettir.

İşte, alırsınız:

<center>
![Varsayılan ölçümlerle küme düzeni][Image1]
</center>

Bazı şeyleri toonote:
  - Merhaba durum bilgisi olan hizmet için birincil çoğaltmalara birkaç düğümleri arasında dağıtılır
  - Aynı bölüm olan farklı düğümlerde hello çoğaltmaları
  - ana ve ikincil toplam sayısı Hello hello kümede dağıtılır.
  - Hizmet nesnelerinin toplam sayısı Hello her düğümde eşit olarak ayrılır

İyi!

Merhaba varsayılan ölçümleri harika bir başlangıç çalışır. Ancak, hello varsayılan ölçümleri yalnızca, o ana kadarki yürütecek. Örneğin: sonuçları mükemmel bile kullanımı tüm bölümleri tarafından çekilen hello bölümlendirme, Düzen olduğunu hello olasılığını nedir? Belirli bir hizmeti için yük hello hello fırsat nedir zamanla sabittir ya da hatta yalnızca aynı arasında birden çok bölüm şu anda hello?

Yalnızca hello varsayılan Ölçümleriyle çalıştırabilir. Ancak, genellikle böylece küme kullanımınızı alt ve istediğiniz daha fazla düzensiz anlamına gelir. Merhaba varsayılan ölçümleri Uyarlamalı değil ve her şeyi eşdeğer olduğunu varsayın olmasıdır. Örneğin, "1" toohello PrimaryCount ölçüm meşgul bir birincil ve iki olmayan bir katkıda. Merhaba kötü durumda yalnızca hello varsayılan ölçümleri kullanarak da performans sorunları kaynaklanan overscheduled düğümleri neden olabilir. Merhaba kümenizi dışında çoğu alma ve performans sorunlarını önleme düşünüyorsanız toouse özel ölçümleri ve dinamik yük raporlama gerekir.

## <a name="custom-metrics"></a>Özel ölçümleri
Merhaba hizmet oluşturulurken ölçümleri adlı-service-örnek başına temelinde yapılandırılır.

Herhangi bir ölçümü açıkladığı bazı özelliklere sahiptir: bir ad, bir ağırlık ve varsayılan yükleme.

* Ölçüm adı: Merhaba ölçüm hello adı. Hello ölçüm adı hello Resource Manager'ın açısından hello kümedeki hello ölçüm için benzersiz bir tanımlayıcı değil.
* Ağırlık: Bu ölçüm göreli toohello ne kadar önemli olduğunu ölçüm ağırlığı tanımlar bu hizmet için diğer ölçümleri.
* Varsayılan yükleme: hello varsayılan yük hello hizmet durum bilgisiz veya durum bilgisi olan bağlı olarak farklı şekilde gösterilir.
  * Durum bilgisi olmayan hizmetler için her ölçümü DefaultLoad adlı tek bir özelliğe sahip.
  * Durum bilgisi olan hizmetler için tanımladığınız:
    * PrimaryDefaultLoad: Bu ölçüm birincil olduğunda bu hizmet tüketir hello varsayılan süre
    * SecondaryDefaultLoad: Bu ölçüm ikincil olduğunda bu hizmet tüketir hello varsayılan süre

> [!NOTE]
> Özel ölçümlerini tanımlayın ve too_also_ kullanım hello varsayılan ölçümleri istiyorsanız too_explicitly_ gereksinim hello varsayılan ölçümleri geri ve ağırlıklarını ve değerleri tanımlamak için ekleyin. Bu durum, hello ilişkisi hello varsayılan ölçümleri ve özel ölçümlerinizi tanımlamanız gerekir çünkü. Örneğin, belki de birincil dağıtım'den fazla ConnectionCount veya WorkQueueDepth ilgilendiğiniz. Tooreduce istediğiniz varsayılan hello ağırlığını hello PrimaryCount tarafından ölçüm yüksek olduğundan, bunlar önceliklidir, ölçümleri tooensure eklediğinizde tooMedium.
>

### <a name="defining-metrics-for-your-service---an-example"></a>Ölçümleri hizmetinizin - örneği tanımlama
Yapılandırma aşağıdaki hello istediğiniz varsayalım:

  - "ConnectionCount" adlı bir ölçüm hizmetinizi raporları
  - Ayrıca toouse hello varsayılan ölçümleri istediğiniz 
  - Bazı ölçüler yaptıktan ve normal olarak bu hizmet birincil çoğaltmasını "ConnectionCount" 20 birimler aldığını biliyorsanız
  - İkincil kopya "ConnectionCount" 5 birimleri kullanın
  - "ConnectionCount" Merhaba bu belirli bir hizmet performansını yönetme bakımından en önemli ölçüm hello olduğunu biliyor
  - Hala dengeli birincil çoğaltmalara istiyor. Birincil çoğaltmalara Dengeleme genellikle iyi bir fikir ne olursa olsun içindir. Bu, birlikte birincil çoğaltmalara çoğunu etkileyen bazı düğüm veya hata etki alanı hello kaybı önlemeye yardımcı olur. 
  - Aksi takdirde hello varsayılan ölçümleri ince

Bu ölçüm yapılandırma hizmetiyle toocreate yazarsınız hello kod aşağıdadır:

Kod:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
StatefulServiceLoadMetricDescription connectionMetric = new StatefulServiceLoadMetricDescription();
connectionMetric.Name = "ConnectionCount";
connectionMetric.PrimaryDefaultLoad = 20;
connectionMetric.SecondaryDefaultLoad = 5;
connectionMetric.Weight = ServiceLoadMetricWeight.High;

StatefulServiceLoadMetricDescription primaryCountMetric = new StatefulServiceLoadMetricDescription();
primaryCountMetric.Name = "PrimaryCount";
primaryCountMetric.PrimaryDefaultLoad = 1;
primaryCountMetric.SecondaryDefaultLoad = 0;
primaryCountMetric.Weight = ServiceLoadMetricWeight.Medium;

StatefulServiceLoadMetricDescription replicaCountMetric = new StatefulServiceLoadMetricDescription();
replicaCountMetric.Name = "ReplicaCount";
replicaCountMetric.PrimaryDefaultLoad = 1;
replicaCountMetric.SecondaryDefaultLoad = 1;
replicaCountMetric.Weight = ServiceLoadMetricWeight.Low;

StatefulServiceLoadMetricDescription totalCountMetric = new StatefulServiceLoadMetricDescription();
totalCountMetric.Name = "Count";
totalCountMetric.PrimaryDefaultLoad = 1;
totalCountMetric.SecondaryDefaultLoad = 1;
totalCountMetric.Weight = ServiceLoadMetricWeight.Low;

serviceDescription.Metrics.Add(connectionMetric);
serviceDescription.Metrics.Add(primaryCountMetric);
serviceDescription.Metrics.Add(replicaCountMetric);
serviceDescription.Metrics.Add(totalCountMetric);

await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ConnectionCount,High,20,5”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

> [!NOTE]
> örneklerde hello hello bu belgenin kalan tanımlamak ve yönetme ölçümleri başına adlı-hizmet temelinde. Olası toodefine ölçümleri hello hizmetine hizmetleriniz için aynı zamanda olan _türü_ düzeyi. Bu hizmet bildirimlerinizi belirterek gerçekleştirilir. Türü düzeyindeki ölçümlerini tanımlayan çeşitli nedenlerle önerilmez. Merhaba ilk ölçüm adları sık ortama özgü nedenidir. Yerinde kesin bir sözleşme sürece, bir ortamda, hello ölçüm "Çekirdek" "MiliCores" veya "Çekirdek" bazılarında olmadığından emin olamaz. Ölçümlerinizi, bildiriminde tanımlanmışsa, ortam başına toocreate yeni bildirimleri gerekir. Bu, genellikle farklı bildirimleri tooa artışı sağlamakta toomanagement zorluklar yalnızca küçük farklılıklar sağlar.  
>
> Ölçüm yükleri adlı-service-örnek başına temelinde yaygın olarak atanır. Örneğin, hello bir örneğini oluşturmak düşünelim toouse planları CustomerA buna yalnızca hafifçe hizmet. Ayrıca daha büyük bir iş yükü olan CustomerB için oluşturduğunuz başka varsayalım. Bu durumda, bu hizmetleri tootweak hello varsayılan yükler büyük olasılıkla istersiniz. Ölçümleri varsa ve bu senaryo toosupport bildirimleri ve tanımlanan yükleri istediğiniz her müşteri için farklı uygulama ve hizmet türleri gerektirir. hizmet oluşturma sırasında tanımlanan hello değerleri bu tooset hello belirli Varsayılanları kullanabileceğinizi şekilde hello bildiriminde tanımlanan geçersiz kılar. Ancak, bunu hello bildirimleri toonot eşleşme ile gerçekte bu hello Hizmeti'ni çalıştıran bildirilen hello değerleri neden olur. Bu tooconfusion yol açabilir. 
>

Bir anımsatıcı olarak: toouse hello varsayılan ölçümleri yalnızca istiyorsanız, tootouch hello ölçümleri toplama hiç gerek yoktur veya hizmetinizi oluşturulurken özel bir şey yapmanız. hiçbir başkalarının tanımlandığında hello varsayılan ölçümleri otomatik olarak kullanılan. 

Artık daha ayrıntılı bu ayarların her biri aracılığıyla edelim ve onu etkilediğini hello davranışı hakkında konuşun.

## <a name="load"></a>Yükleme
Merhaba ölçümleri tanımlamanın tüm noktası toorepresent bazı yüktür. *Yük* belirli bir metrik ne kadarının bazı hizmet örneği veya belirtilen bir düğüm üzerindeki çoğaltma tarafından kullanılan olduğu. Yük neredeyse herhangi bir noktada yapılandırılabilir. Örneğin:

  - Bir hizmet oluşturduğunuzda yük tanımlanabilir. Bu adlı _varsayılan yük_.
  - bir hizmet güncelleştirilmiş için hello hizmeti oluşturulduktan sonra varsayılan gibi hello Ölçüm bilgilerini yükler. Bu adlı _bir hizmeti güncelleştirme_. 
  - Merhaba yükler belli bir bölüm için bu hizmet için sıfırlama toohello varsayılan değerleri olabilir. Bu adlı _bölüm yükünü sıfırlama_.
  - Yükleme bildirilen üzerinde bir çalışma zamanı sırasında dinamik olarak hizmet nesnesi temelinde. Bu adlı _yük raporlama_. 
  
Bu stratejileri tümünün aynı yaşam süresi boyunca hizmeti hello içinde kullanılabilir. 

## <a name="default-load"></a>Varsayılan yükleme
*Varsayılan yükleme* bu hizmetin her bir hizmet nesnesi (durum bilgisiz örneği veya durum bilgisi olan çoğaltma) tüketen hello ölçüsü ne kadarının. dinamik yük raporu gibi diğer bilgileri alıncaya kadar hello küme Resource Manager hello hizmet nesnesi hello yük için bu sayıyı kullanır. Daha basit hizmetlerde hello varsayılan yükleme statik bir tanımıdır. Hello varsayılan yükü hiçbir zaman güncelleştirilir ve hello hizmet hello ömrü boyunca kullanılır. Varsayılan basit kapasite planlama burada belirli miktarda kaynağı ayrılmış toodifferent iş yüklerinin ve değiştirme senaryoları works harika yükler.

> [!NOTE]
> Kapasite yönetimi ve hello düğümler için kapasiteler kümenizdeki tanımlama hakkında daha fazla bilgi için lütfen bkz [bu makalede](service-fabric-cluster-resource-manager-cluster-description.md#capacity).
> 

Merhaba Küme Kaynak Yöneticisi durum bilgisi olan hizmetler toospecify kendi ana ve ikincil farklı varsayılan yük olanak sağlar. Durum bilgisi olmayan hizmetler yalnızca tooall örnekleri geçerli bir değer belirtebilirsiniz. Durum bilgisi olan hizmetler için birincil ve ikincil çoğaltmalar için hello varsayılan Yük genellikle farklı çoğaltmaların her rol işlerinde farklı türde yapmak bu yana. Örneğin, ana genellikle okuma ve yazma işlemleri hizmet ve kullanırken ikinciller hello hesaplama yük çoğunu işleyecek. Genellikle bir birincil çoğaltma için hello varsayılan yük hello varsayılan yük ikincil çoğaltmalar için daha yüksektir. Merhaba gerçek sayılar, kendi ölçü bağımlı olmalıdır.

## <a name="dynamic-load"></a>Dinamik yük
Hizmetiniz bir süredir çalışıyor varsayalım. Bazı izleme ile, fark ettim:

1. Bazı bölümleri veya belirli bir hizmeti örnekleri diğerlerinden daha fazla kaynak tüketmesine
2. Bazı hizmetleri zaman içinde değişir yük sahiptir.

Birçok yük dalgalanmaları bu tür neden olabilecek bir şey yoktur. Örneğin, farklı hizmetler veya bölümleri farklı gereksinimlere sahip farklı müşteriler ile ilişkilendirilir. Merhaba tutar iş hello hizmetinin değiştiğinden hello hello gün süresince yükü de değişebilir. Merhaba nedenle bağımsız olarak, genellikle varsayılan kullanabilirsiniz ve tek bir sayı yoktur. Merhaba küme dışında çoğu kullanımı tooget hello istiyorsanız, bu özellikle doğrudur. Varsayılan yükleme için çekme herhangi bir değer hello zaman bazıları yanlış olur. Yanlış varsayılan hello Küme Kaynak Yöneticisi üzerinden veya kaynak ayırma altında sonucunda yükler. Sonuç olarak, hello küme dengeli hello küme Resource Manager düşündüğü olsa da, üzerinde veya altında kullanılan düğümlerin vardır. Varsayılan yükleri ilk yerleştirme için bazı bilgiler sağlar, ancak gerçek iş yükleri için tam bir öykü olmadıklarını beri hala iyidir. kaynak gereksinimleri, hello Küme Kaynak Yöneticisi'ni değiştirerek tooaccurately yakalama her hizmet nesnesi tooupdate çalışma zamanı sırasında kendi yük sağlar. Bu, dinamik yük raporlama çağrılır.

Dinamik yük raporları kendi ayırma ve bildirilen yük ölçümleri kendi ömürleri boyunca çoğaltmalar veya örnekleri tooadjust izin verir. Bir hizmet çoğaltma veya soğuk ve herhangi bir iş yapmamanın örneğini genellikle belirli bir metrik düşük miktarda tarafından kullanılan raporlar. Meşgul çoğaltma veya örnek daha kullandıkları raporlar.

Çoğaltma veya örnek başına yük raporlama hello küme Resource Manager tooreorganize hello kümede hello bireysel hizmet nesneleri sağlar. Merhaba hizmetleri yeniden düzenleme gereksinim duydukları hello kaynakları alma sağlamaya yardımcı olur. Meşgul Hizmetleri etkili bir şekilde çok "diğer çoğaltmaları veya şu anda soğuk veya daha az çalışarak olan örnekleri kaynaklarınızı geri" alın.

Güvenilir hizmetler içinde hello kod tooreport yük dinamik olarak şöyle:

Kod:

```csharp
this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("CurrentConnectionCount", 1234), new LoadMetric("metric1", 42) });
```

Bir hizmet oluşturma sırasında tanımlı hello ölçümleri hiçbirinde bildirebilirsiniz. Service Fabric olmayan bir ölçüm için bir hizmet raporları yükü toouse yapılandırdıysanız, bu raporu yok sayar. Varsa diğer ölçümleri hello aynı bildirilen bu raporları kabul edilir geçerli süre. Servis kodu ölçmek ve tüm hello bunu bilen ölçümleri rapor için nasıl ve işleçler toochange hello servis kodu gerek kalmadan hello ölçüm yapılandırma toouse belirtebilirsiniz. 

### <a name="updating-a-services-metric-configuration"></a>Bir hizmetin ölçüm yapılandırmasını güncelleştirme
Ölçüm Hello listesine hello hizmetiyle ilişkili ve bu ölçümleri hello özelliklerini, Canlı Merhaba hizmeti çalışırken dinamik olarak güncelleştirilebilir. Bu deneme ve esneklik sağlar. Bazı örnekler bu yararlı olduğunda şunlardır:

  - belirli bir hizmet için buggy rapora bir ölçüm devre dışı bırakma
  - İstenen davranışı temelinde ölçümleri Hello ağırlıkları yeniden yapılandırma
  - yalnızca hello kodu zaten dağıtıldığını ve diğer mekanizmalar doğrulanmış sonra yeni bir ölçümü etkinleştirme
  - Merhaba varsayılan yük gözlemlenen davranışı ve tüketim dayalı bir hizmet için değiştirme

Merhaba ölçüm yapılandırmasını değiştirmek için ana apı'leridir `FabricClient.ServiceManagementClient.UpdateServiceAsync` C# ve `Update-ServiceFabricService` PowerShell'de. Bu API'leri ile belirttiğiniz ne olursa olsun bilgileri hemen varolan Ölçüm bilgilerini hello hizmet hello yerine geçer. 

## <a name="mixing-default-load-values-and-dynamic-load-reports"></a>Varsayılan yükleme değerlerini ve dinamik yük raporları karıştırma
Varsayılan yükleme ve dinamik yükleri hello için kullanılan aynı hizmet. Varsayılan yükleme ve dinamik yük raporları bir hizmet kullanan, dinamik raporlar görünmesini kadar varsayılan yük tahmini olarak görür. Varsayılan yükleme iyi çünkü toowork ile Merhaba Küme Kaynak Yöneticisi'ni bir şey sağlar. oluşturuldukları sırada hello varsayılan yük hello küme Resource Manager tooplace iyi konumları hello hizmet nesneleri sağlar. Varsayılan yükleme bilgi sağlanırsa, hizmetleri yerleşimini etkili bir şekilde rastgele belirlenir. Yük raporları daha sonra geldiğinde hello ilk rastgele yerleştirme genellikle yanlış olup hello küme Resource Manager toomove hizmetleri içerir.

Şimdi önceki örneğimizde alın ve bazı özel ölçümleri ve dinamik yük raporlama eklediğimiz ne olur bakın. Bu örnekte, bir örnek ölçümü "MemoryInMb" kullanırız.

> [!NOTE]
> Bellek Service Fabric olabilir hello sistem ölçümleri biridir [kaynak yöneten](service-fabric-resource-governance.md), ve kendiniz raporlama genellikle zordur. Aslında, tooreport bellek tüketimi bekliyoruz yoktur; Kullanılan bellek burada yardımcı toolearning hello küme Resource Manager hello yetenekleriyle ilgili olarak.
>

Şimdi başlangıçta hello durum bilgisi olan hizmet komutu aşağıdaki hello ile oluşturduğumuz olduğunu varsayın:

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("MemoryInMb,High,21,11”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

Bir anımsatıcı bu söz dizimi ("MetricName MetricWeight, PrimaryDefaultLoad, SecondaryDefaultLoad") değil.

Hangi bir olası küme düzeni gibi görünebilir görelim:

<center>
![Küme dengeli hem varsayılan hem de özel ölçümlerle][Image2]
</center>

Belirtmeye değer olan bazı noktalar:

* Bölüm içindeki ikincil çoğaltmaları her kendi yük olabilir
* Genel hello ölçümleri dengeli arayın. Bellek için en fazla hello arasındaki oran hello ve en düşük yüktür 1.75 (Merhaba düğümü ile Merhaba çoğu yük N3, hello az N2 ve 28/16 1.75 =).

Biz yine tooexplain gereken bazı şeyler vardır:

* Ne 1.75 oranını makul olup olmadığını belirledi? Merhaba Küme Kaynak Yöneticisi'ni nasıl yeterince iyi veya daha fazla iş toodo ise biliyor?
* Ne zaman Dengeleme oluşuyor?
* Ne bellek "Yüksek" ağırlıklı olduğunu anlama geliyor?

## <a name="metric-weights"></a>Ölçüm ağırlığı
İzleme hello aynı ölçümleri farklı hizmetlerde önemlidir. Genel Görünüm ne hello kümedeki küme Resource Manager tootrack tüketim Merhaba, düğümlere tüketim dengelemek ve düğüm kapasitesi geçmez emin olun sağlar olduğunu. Bununla birlikte, farklı görünümleri hello toohello önem olarak Hizmetleri olabilir aynı Ölçüm. Ayrıca, birçok ölçümleri ve çok sayıda Hizmetleri ile bir kümede mükemmel dengeli çözümleri için tüm ölçümleri var olmayabilir. Merhaba küme kaynak yöneticisi bu gibi durumlarda nasıl yöneteceğini?

Ölçüm ağırlığı hello Küme Kaynak Yöneticisi'ni nasıl toobalance hello küme kusursuz yanıt olduğunda toodecide izin verir. Ölçüm ağırlığı da hello küme Resource Manager toobalance belirli hizmetleri farklı olanak sağlar. Ölçümleri dört farklı ağırlık düzeyine sahip olabilir: sıfır, düşük, Orta ve yüksek. Ölçüm ağırlık sıfır hiçbir şey veya dengeli değerlendirirken katkıda bulunur. Ancak, kendi yük hala toocapacity yönetim katkıda. Ölçümleri sıfır ağırlık ile hala faydalıdır ve sık hizmet davranışı ve performans izleme işleminin bir parçası olarak kullanılır. [Bu makalede](service-fabric-diagnostics-event-generation-infra.md) hello kullanım ölçümleri izleme ve Tanılama, hizmetlerin üzerinde daha fazla bilgi sağlar. 

Merhaba gerçek hello kümedeki farklı ölçüm ağırlığı küme Resource Manager'ı hello farklı çözümler oluşturur etkisidir. Ölçüm ağırlığı hello Küme Kaynak Yöneticisi'ni, belirli ölçümleri diğerlerinden daha önemli söyleyin. Hiçbir kusursuz çözüm hello olduğunda Küme Kaynak Yöneticisi'ni hello yüksek ağırlıklı ölçümleri daha iyi dengeleyen çözümleri tercih. Bir hizmeti belirli bir ölçüm düşündüğü varsa bu ölçümün kullanımlarını imbalanced bulabilirsiniz önemli değildir. Bu, başka bir hizmet tooget önemli tooit olan bazı ölçüm bile bir dağıtımını sağlar.

Bazı yük raporları ve nasıl farklı ölçümü bir örneğe bakalım hello kümedeki farklı ayırmaları sonuçlarında ağırlık verir. Bu örnekte, hello göreli ağırlık hello ölçümleri geçiş hello küme Resource Manager toocreate Hizmetleri farklı düzenlenişlerini neden olduğunu bakın.

<center>
![Ölçüm ağırlık örnek ve Dengeleme çözümlerini üzerindeki etkisini][Image3]
</center>

Bu örnekte, dört farklı hizmetler, MetricA ve MetricB olmak üzere iki farklı ölçümleri için tüm raporlama farklı değerler vardır. Bir durumda, tüm hello Hizmetleri MetricA tanımlamak hello en önemli sunucudur (ağırlık yüksek =) ve önemli olarak MetricB (ağırlık düşük =). Sonuç olarak, bu hello Küme Kaynak Yöneticisi, hello Hizmetleri yerleştirir, böylece MetricA daha iyi MetricB dengeli bakın. "Daha iyi dengelenmiş" anlamına gelir MetricA düşük olduğunu MetricB daha düşük bir standart sapma vardır. Merhaba ikinci durumda, biz hello ölçüm ağırlığı ters çevrilir. Sonuç olarak, hello küme kaynak yöneticisi hizmetleri A ve B toocome yukarı MetricB daha iyi MetricA dengeli olduğu bir ayırma ile değiştirir.

> [!NOTE]
> Ölçüm ağırlığı hello Küme Kaynak Yöneticisi'ni nasıl dengelemeniz, ancak değil zaman Dengeleme olacağını belirler. Dengeleme hakkında daha fazla bilgi için kullanıma [bu makalede](service-fabric-cluster-resource-manager-balancing.md)
>

### <a name="global-metric-weights"></a>Genel ölçüm ağırlığı
Diyelim ki ServiceA yüksek ağırlık olarak MetricA tanımlar ve ServiceB MetricA tooLow veya sıfır hello ağırlık ayarlar. Kullanılan alma sona eriyor hello gerçek ağırlık nedir?

Her ölçüm için izlenen birden çok ağırlıkları vardır. Merhaba ilk ağırlık hello hello hizmet oluşturulduğunda hello ölçüm için tanımlı tek ' dir. Merhaba başka ağırlığını otomatik olarak hesaplanır genel ağırlık olur. Bu iki ağırlıkları çözümleri Puanlama Hello Küme Kaynak Yöneticisi'ni kullanır. Her iki ağırlıkları dikkate alarak önemlidir. Bu hello küme Resource Manager toobalance according tooits önceliklere sahip ve bir bütün doğru ayrılmış olarak bu hello küme ayrıca olun her hizmeti sağlar.

Hello küme Resource Manager için hem genel hem de yerel Bakiye hakkında önemli alamadık neler olacağını? İyi, kolay tooconstruct çözümleri genel dengeli ancak, tek tek Hizmetleri için yetersiz kaynak dengesindeki neden olur. Merhaba, aşağıdaki örnek, şimdi yalnızca hello varsayılan ölçümleri ile yapılandırılmış bir hizmet bakın ve yalnızca genel Bakiye kabul ne olur bakın:

<center>
![Merhaba genel yalnızca çözüm etkisi][Image4]
</center>

Yalnızca genel bakiyesi dayalı hello üst örnekte, bir bütün olarak hello küme gerçekten dengelenir. Tüm düğümler aynı sayısı ana ve aynı hello hello sahip toplam çoğaltmaları sayı. Merhaba gerçek etkisini bu ayırma sırasında bakarsanız ancak, bu nedenle iyi değil: tüm kendi ana aldığından herhangi bir düğümün hello kaybı belirli bir iş yükünü orantısız, etkiler.. Merhaba üç farklı bölümlerini hello daire hizmeti için üç ana hello Hello ilk düğüm başarısız olursa Örneğin, tümü kaybolur. Buna karşılık, hello üçgen ve Altıgene Hizmetleri bir çoğaltma kaybetmek bölümlerinin sahiptir. Bu, çoğaltma aşağı toorecover hello olması dışında bir kesintiye neden olur.

Hello altındaki örnekte hello küme Resource Manager hem hello genel ve hizmet başına bakiyesi dayalı hello çoğaltmaları dağıtılmış. Merhaba çözüm Hello puanı hesaplanırken hello ağırlık toohello genel çözüm ve (yapılandırılabilir) bölümü tooindividual hizmetlerinin çoğunu sağlar. Ölçüm için genel bakiyesi hello ölçüm ağırlığı her hizmetinden hello ortalaması alınarak hesaplanır. Her hizmet according tooits kendi tanımlı ölçüm ağırlığı dengelenir. Bu, hello Hizmetleri kendilerini içinde tootheir kendi gereksinimlerine göre dengelendiğini sağlar. Sonuç olarak, tüm hizmetlerin tüm bölümler Hello aynı ilk düğüm başarısız hello başarısız olursa dağıtılır. Merhaba etkisi tooeach olan hello aynı.

## <a name="next-steps"></a>Sonraki adımlar
- Hizmetleri yapılandırma hakkında daha fazla bilgi için [hizmetleri yapılandırma hakkında bilgi edinin](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- Birleştirme ölçümleri tanımlama tek yönlü tooconsolidate yayılmak yerine düğümlerde yüktür. toolearn nasıl tooconfigure birleştirme, çok bakın[bu makalede](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
- toofind hello Küme Kaynak Yöneticisi yönetir ve dengeleyen hello kümedeki yük hakkında hello makalesine üzerinde kullanıma [Yük Dengeleme](service-fabric-cluster-resource-manager-balancing.md)
- Merhaba baştan başlatın ve [giriş toohello Service Fabric kümesi Kaynak Yöneticisi Al](service-fabric-cluster-resource-manager-introduction.md)
- Taşıma maliyeti belirli hizmetleri diğerlerinden daha pahalı toomove olduğunu toohello küme Resource Manager sinyal bir yoludur. Taşıma maliyeti hakkında daha fazla toolearn başvurmak çok[bu makalede](service-fabric-cluster-resource-manager-movement-cost.md)

[Image1]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-cluster-layout-with-default-metrics.png
[Image2]:./media/service-fabric-cluster-resource-manager-metrics/Service-Fabric-Resource-Manager-Dynamic-Load-Reports.png
[Image3]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-metric-weights-impact.png
[Image4]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-global-vs-local-balancing.png
