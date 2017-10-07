---
title: Service Fabric Hizmetleri aaaScalability | Microsoft Docs
description: "Açıklar nasıl tooscale Service Fabric Hizmetleri"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ed324f23-242f-47b7-af1a-e55c839e7d5d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5af06f8f71ad5dee32ba115b922842684867e654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-in-service-fabric"></a>Service Fabric ölçeklendirme
Azure Service Fabric kolay toobuild ölçeklenebilir uygulamalar hello hizmetler, bölümler ve çoğaltmalar bir kümenin hello düğümlerinde yöneterek kolaylaştırır. Birçok iş yükleri üzerinde çalışan aynı donanım etkinleştirir en fazla kaynak kullanımı Merhaba, ancak aynı zamanda tooscale iş yüklerinizi nasıl seçtiğiniz açısından esneklik sağlar. 

Service Fabric ölçeklendirme birkaç farklı şekilde gerçekleştirilir:

1. Ölçek oluşturma veya durum bilgisiz hizmet örnekleri kaldırma
2. Hizmetleri adlı ölçek oluşturma veya yeni kaldırma
3. Uygulama örnekleri adlı ölçek oluşturma veya yeni kaldırma
4. Bölümlenmiş hizmetlerini kullanarak ölçeklendirme
5. Ekleyerek ve hello kümeden düğüm kaldırma ölçeklendirme 
6. Küme Kaynak Yöneticisi'ni ölçümleri kullanarak ölçeklendirme

## <a name="scaling-by-creating-or-removing-stateless-service-instances"></a>Ölçek oluşturma veya durum bilgisiz hizmet örnekleri kaldırma
Merhaba en basit yolu tooscale Service Fabric içinde birini durum bilgisiz Hizmetleri ile çalışır. Durum bilgisi olmayan bir hizmet oluşturduğunuzda, bir fırsat toodefine alma bir `InstanceCount`. `InstanceCount`Merhaba hizmeti başladığında hizmetin kod kaç tane çalışan kopyalarını oluşturulan tanımlar. Örneğin, hello kümede 100 düğümleri olduğunu düşünelim. Ayrıca bir hizmet ile oluşturduğunuz düşünelim bir `InstanceCount` 10. Çalışma zamanı sırasında bu 10 çalışan kopyaları hello kod tüm meşgul hale gelebilir (veya yetecek kadar meşgul bulunamadı). Tek yönlü tooscale iş yükü toochange hello örnekleri sayısıdır. Örneğin, bazı izleme veya yönetim kod parçası örnekleri too50 veya too5 varolan sayısını hello değiştirmek, hello iş yükü tooscale veya temel alınarak hello uzaklaştırma gereken bağlı olarak yük. 

C# ' TA:

```csharp
StatelessServiceUpdateDescription updateDescription = new StatelessServiceUpdateDescription(); 
updateDescription.InstanceCount = 50;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

PowerShell:

```posh
Update-ServiceFabricService -Stateless -ServiceName $serviceName -InstanceCount 50
```
### <a name="using-dynamic-instance-count"></a>Dinamik örnek sayısı kullanma
Özel durum bilgisi olmayan hizmetler için bir otomatik şekilde toochange hello örnek sayısı Service Fabric sunar. Bu hello hizmet tooscale hello kullanılabilir düğüm sayısı ile dinamik olarak sağlar. Bu davranış içine Hello yolu tooopt tooset hello örnek sayısı olan = -1. Instancecount = -1 olan bir yönerge tooService "Çalıştır bu durum bilgisi olmayan hizmetin her düğümde." diyor yapı Merhaba düğüm sayısı değişirse Service Fabric hello hizmetinin geçerli tüm düğümler üzerinde çalıştığından emin olduktan hello örnek sayısı toomatch, otomatik olarak değişir. 

C# ' TA:

```csharp
StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
//Set other service properties necessary for creation....
serviceDescription.InstanceCount = -1;
await fc.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName -Stateless -PartitionSchemeSingleton -InstanceCount "-1"
```

## <a name="scaling-by-creating-or-removing-new-named-services"></a>Hizmetleri adlı ölçek oluşturma veya yeni kaldırma
Bir adlandırılmış hizmet örneği bir hizmet türünün belirli bir örneği olduğunu (bkz [Service Fabric uygulama yaşam döngüsü](service-fabric-application-lifecycle.md)) hello kümedeki bazı Adlandırılmış uygulama örneği içinde. 

Yeni adlı hizmet örneği oluşturulan (daha az veya meşgul hale Hizmetleri olarak veya kaldırılabilir). Bu, genellikle yük üzerinde var olan hizmetleri toodecrease izin vererek, daha fazla hizmet örnekleri arasında yayılan istekleri toobe sağlar. Merhaba Service Fabric kümesi Kaynak Yöneticisi hello Hizmetleri Hizmetleri oluştururken, dağıtılmış bir şekilde hello kümedeki yerleştirir. Merhaba tam kararları hello tarafından yönetilir [ölçümleri](service-fabric-cluster-resource-manager-metrics.md) hello küme ve diğer yerleştirme kuralları. Hizmetleri birkaç farklı şekilde oluşturulabilir ancak hello en yaygın olan birisi çağırma gibi yönetim eylemleri yoluyla [ `New-ServiceFabricService` ](https://docs.microsoft.com/en-us/powershell/module/servicefabric/new-servicefabricservice?view=azureservicefabricps), veya kod arama [ `CreateServiceAsync` ](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync?view=azure-dotnet). `CreateServiceAsync`bile gelen hello kümede çalışan diğer hizmetler içinde çağrılabilir.

Oluşturma Hizmetleri dinamik olarak her türlü içinde kullanılabilir ve ortak bir deseni. Örneğin, belirli bir iş akışı temsil eden bir durum bilgisi olan hizmet göz önünde bulundurun. İş temsil eden çağrıları up toothis hizmeti tooshow giderek ve bu hizmeti iş akışı ve kayıt giderek tooexecute hello adımları toothat devam. 

Nasıl bu belirli bir hizmet ölçek yapmak? Merhaba hizmet bazı formunda, çok kiracılı çağrılarını kabul ve adımları hello birçok farklı örnekleri için devre dışı aynı kazandırın tümünü bir defada iş akışı. Ancak, yapabilir hello kod bu yana daha karmaşık tooworry hello birçok farklı örnekleri hakkında artık aynı iş akışı, tüm farklı aşamalar ve farklı müşterilere ait. Ayrıca, aynı anda değil çözmek hello adresindeki birden çok iş akışı işleme izin ver hello ölçek sorun. Belirli bir noktada bu hizmetin belirli bir makine üzerinde çok fazla kaynak toofit tüketir olmasıdır. Birçok Hizmetleri hello ilk yer bu modelinde oluşturulmuş değil de kendi kodunda son toosome yapısında performans sorunu veya yavaşlama zorluk karşılaşırsınız. Bu tür sorunları hello hizmet değil toowork de neden Hello sayısını izleme mı eş zamanlı iş akışları büyük alır.  

Toocreate örneği bir çözümdür hello iş akışı farklı her örneği için bu hizmetin tootrack istiyor. Bu harika bir desen ve durum bilgisiz veya durum bilgisi olan hello hizmeti olup olmadığını çalışır. Bu desen toowork için "İş yükü Yöneticisi hizmeti" davranır genellikle başka bir hizmet yok. Bu hizmetin Hello iş tooreceive istekleri ve tooroute bu istekleri tooother hizmetleridir. Hello Yöneticisi hello iletisi aldığında hello iş yükü Hizmeti'nin bir örneğini dinamik olarak oluşturabilir ve ardından istekleri toothose hizmetlerini geçirebilirsiniz. Belirtilen iş akışı hizmeti işini tamamladığında hello Yöneticisi hizmeti de geri aramalar alabilir. Hello Yöneticisi bu geri aramalar aldığında, hello iş akışı hizmeti örneğini silin veya daha fazla çağrıları beklenen, bırakın. 

Bu tür Yöneticisi'nin Gelişmiş sürümleri bile yönettiği hello Hizmetleri havuzları oluşturabilirsiniz. Merhaba havuzu yeni bir istek geldiğinde, hello hizmet toospin toowait olmadığını sağlamaya yardımcı olur. Bunun yerine, hello Yöneticisi yalnızca hello havuzundan şu anda kullanımda olmayan bir iş akışı hizmeti seçin veya rastgele rota. Daha az büyük olasılıkla bu hello istek çalışmaya başlar yeni bir hizmet toobe toowait sahip olduğundan kullanılabilir hizmetler havuzu tutma işleme yeni istekler daha hızlı hale getirir. Yeni hizmetler oluşturma, hızlı, ancak boş veya anlık bağlıdır. Merhaba havuzu hello hello isteği toowait hizmet önce süresini en aza indirmek yardımcı olur. Yanıt sürelerini hello en önemli olduğunda, genellikle bu Yöneticisi ve havuz deseni görürsünüz. Sıraya alma hello istek ve hello arka plan oluşturma hello hizmetinde ve _sonra_ geçirme olduğu de popüler Yöneticisi düzeni oluşturma ve bazı iş hello miktarını bu hizmet şu anda izleme üzerinde temel Hizmetleri silme gibi Bekleyen sahiptir. 

## <a name="scaling-by-creating-or-removing-new-named-application-instances"></a>Uygulama örnekleri adlı ölçek oluşturma veya yeni kaldırma
Oluşturma ve silme tüm uygulama örnekleri oluşturma ve Hizmetleri siliniyor benzer toohello Düzen yöneliktir. Bu model için gelen alma hello bilgi hello hello küme içindeki diğer hizmetler ve bunu görmesini hello isteklerini temel alan hello kararı vermeden bazı Yöneticisi hizmeti yoktur. 

Ne zaman yeni bir adlandırılmış uygulama örneği oluşturma yeni bir adlandırılmış hizmet örneği zaten mevcut olan bazı uygulamada oluşturmak yerine kullanılsın mı? Bazı durumlar vardır:

  * Merhaba yeni uygulama kodu toorun bazı belirli kimlik veya güvenlik ayarları altında gereken bir müşteri için örneğidir.
    * Service Fabric farklı kod paketleri toorun belirli kimlikleri altında tanımlanmasına olanak sağlar. Sipariş toolaunch hello farklı kimlikler, hello etkinleştirmeleri altında aynı kod paketi gerekir farklı uygulama durumlarda toooccur. Dağıtılan mevcut bir müşterinin iş yükleri sahip olduğu bir durum düşünün. İzleme ve uzak veritabanları veya diğer sistemler gibi kendi erişim tooother kaynakları denetlemek için bu belirli bir kimlik altında çalışıyor olabilir. Yeni bir müşteri kaydolduğunda, bu durumda, muhtemelen tooactivate hello kodlarını istemediğiniz aynı içerik (işlem alanı). Olabilir, ancak bu, belirli bir kimliğe Merhaba içeriğine içinde hizmet kod tooact zorlaştırır. Daha fazla güvenlik, yalıtım ve kimlik yönetimi kodu genellikle olması gerekir. Adlı hizmetin farklı kullanmak yerine örnekleri içinde hello aynı uygulama örneği ve bu nedenle aynı işlem alanı Merhaba, farklı adlı Service Fabric uygulaması örnekleri kullanabilirsiniz. Bu, daha kolay toodefine farklı kimlik bağlamları kolaylaştırır.
  * Merhaba yeni uygulama örneği aynı zamanda yapılandırmasının bir araç olarak görev yapar
    * Varsayılan olarak, tüm uygulama örneğini içinde belirli bir hizmet türünün hizmet örnekleri adlı hello hello belirli bir düğümde aynı işlemi çalıştırır. Ne bu her hizmet örneği farklı bir şekilde yapılandırabilirsiniz ancak, bunun kadar karmaşık olmasıdır anlamına gelir. Hizmetleri Yapılandırma paketi içinde kendi config yukarı toolook kullandıkları bazı belirteci olması gerekir. Genellikle bu yalnızca hello hizmetin adıdır. Bu düzgün çalışır, ancak bunu hello yapılandırma toohello adları, uygulama örneği içinde hello bireysel adlandırılmış hizmet örneklerinin tüm çiftler. Bu kafa karıştırıcı olabilir ve sabit toomanage yapılandırma bu yana uygulama örneği belirli değerleri içeren bir tasarım zamanı yapısı normalde olur. Böylece Hello yeni hizmetler kendi belirli bilgi aramak daha fazla hizmet her zaman oluşturmak daha fazla uygulama yükseltmelerini hello yapılandırma paketleri veya yenilerini toodeploy içindeki toochange hello bilgileri anlamına gelir. Genellikle, daha kolay toocreate yepyeni bir adlandırılmış uygulama örneği olur. Daha sonra ne olursa olsun hello Hizmetleri için gerekli yapılandırmadır hello uygulama parametreleri tooset kullanabilirsiniz. Bu şekilde tüm, içinde oluşturulan hello Hizmetleri adlandırılmış uygulama örneği belirli yapılandırma ayarları devralabilirsiniz. Örneğin, hello ayarları ve özelleştirmelerini sırlar ya da müşteri kaynak sınırları, başına her müşteri için tek yapılandırma dosyasıyla sahip olmak yerine yerine farklı uygulama örneği bu ayarlarla her müşteri için olurdu geçersiz kılındı. 
  * Merhaba yeni uygulama yükseltme sınır olarak görev yapar
    * Service Fabric içinde farklı adlandırılmış uygulama örnekleri yükseltme için sınır olarak hizmet. Bir adlandırılmış uygulama örneği yükseltmesini başka bir adlandırılmış uygulama örneğini çalıştıran hello kod etkilemez. Merhaba farklı uygulamalar üzerinde hello aynı kod hello farklı sürümlerini çalıştıran sona erer aynı düğüm. Merhaba yeni kod hello izlemeniz gereken olup olmadığını aynı olarak başka bir hizmet veya yükseltmeleri seçebileceğinden toomake ölçeklendirme karar gerektiğinde bu bir etken olabilir. Örneğin, bir çağrı oluşturma ve Hizmetleri dinamik olarak silme belirli bir müşterinin iş yükleri ölçekleme için sorumlu hello Yöneticisi hizmetine ulaşan söyleyin. Bu durumda ancak hello ile ilişkili bir iş yükü için çağrıdır bir _yeni_ müşteri. Müşterilerin çoğu birbirinden daha önce listelenen yalnızca hello güvenlik ve yapılandırma nedeniyle yalıtılmış gibi çalışır, ancak hello yazılım ve seçme belirli sürümlerini çalıştıran bakımından daha fazla esneklik sağladığından zaman yükseltmeden. Aynı zamanda yeni bir uygulama örneği oluşturabilir ve hello hizmet oluşturma var. yalnızca toofurther bölüm hello herhangi bir yükseltme touch hizmetlerinizi miktarı. Ayrı uygulama örnekleri uygulama yükseltme yaparken büyük ayrıntı düzeyi sağlamak ve ayrıca A etkinleştirin / B testi ve mavi/yeşil dağıtımları. 
  * Merhaba varolan uygulama örneği dolu
    * Service Fabric içinde [uygulama kapasite](service-fabric-cluster-resource-manager-application-groups.md) toocontrol hello miktarda kaynak kullanılabilir belirli uygulama örnekleri için kullanabileceğiniz bir kavramdır. Örneğin, belirli bir hizmeti sipariş tooscale oluşturulan başka bir örneği toohave gerektiğine karar. Ancak, bu uygulama örneği belirli bir ölçüm için kapasite dışındadır. Bu belirli müşteri ya da iş yükü daha fazla kaynak hala verilmelidir, ardından bu uygulama için hello varolan kapasitesini artırmak ya da yeni bir uygulama oluşturun. 

## <a name="scaling-at-hello-partition-level"></a>Merhaba bölüm düzeyde ölçekleme
Service Fabric bölümleme destekler. Bölümleme hizmet her biri bağımsız olarak çalışır birkaç mantıksal ve fiziksel bölümlere, ayırır. Bu durum bilgisi olan hizmetleriyle yararlıdır, hiç kimse çoğaltmalarının ayarlamak beri toohandle tüm hello çağrıları vardır ve tüm hello durumunun aynı anda işlemek. Merhaba [genel bakış bölümleme](service-fabric-concepts-partitioning.md) desteklenen bölümleme şeması hello tür bilgiler sağlar. Her bölüm kopyalarını Hello hizmetin yük dağıtımı ve bir bütün olarak hiçbiri hello hizmeti veya herhangi bir bölümü tek hata noktası olduğundan emin olduktan bir kümedeki hello düğümler arasında yayılır. 

Düşük anahtarı 0, 99 yüksek anahtarı ve 4 bölüm sayısı ile ranged bölümleme düzeni kullanan bir hizmet göz önünde bulundurun. Üç düğümlü bir küme içinde hello hizmeti aşağıda gösterildiği gibi her bir düğümde hello kaynakları paylaşmak dört yinelemelerle düzenlendiği:

<center>
![Üç düğümü olan bir bölüm düzeni](./media/service-fabric-concepts-scalability/layout-three-nodes.png)
</center>

Merhaba düğümlerin sayısını artırmak için Service Fabric hello mevcut çoğaltmaları bazıları var. taşınır. Örneğin, toofour hello düğüm sayısını artırır ve hello çoğaltmaları yeniden dağıtılabilir varsayalım. Merhaba hizmeti şimdi her düğüm üzerinde çalışan üç çoğaltmaları artık, her toodifferent bölümleri ait. Merhaba yeni düğüm soğuk değil beri bu daha iyi kaynak kullanımı sağlar. Genellikle, her hizmetin daha fazla kaynak kullanılabilir tooit taşıdığından da performansı artırır.

<center>
![Dört düğüm ile bir bölüm düzeni](./media/service-fabric-concepts-scalability/layout-four-nodes.png)
</center>

## <a name="scaling-by-using-hello-service-fabric-cluster-resource-manager-and-metrics"></a>Merhaba Service Fabric kümesi Kaynak Yöneticisi ve ölçümleri kullanarak ölçeklendirme
[Ölçümleri](service-fabric-cluster-resource-manager-metrics.md) nasıl Hizmetleri kendi kaynak tüketimi tooService doku express şunlardır. Ölçümleri kullanarak bir fırsat tooreorganize hello Küme Kaynak Yöneticisi'ni sağlar ve hello küme hello düzenini en iyi duruma getirme. Örneğin, olabilir hello küme kaynaklarında Eskinin, ancak bunlar şu anda iş yaptıklarını toohello Hizmetleri ayrılabilir değil. Merhaba küme tooensure Hizmetleri erişime sahip olmasını sağlar hello küme Resource Manager tooreorganize ölçümleri kullanarak toohello kullanılabilir kaynaklar. 


## <a name="scaling-by-adding-and-removing-nodes-from-hello-cluster"></a>Ekleyerek ve hello kümeden düğüm kaldırma ölçeklendirme 
Service Fabric ile ölçekleme için başka bir seçenek toochange hello hello küme boyutudur. Merhaba küme Hello boyutunu değiştirme, düğüm ekleme veya bir veya daha fazla hello düğüm türü için hello kümede kaldırma anlamına gelir. Örneğin, tüm hello düğümleri hello kümedeki etkin olduğu bir durum düşünün. Bu hello kümenin kaynakları neredeyse tüm tüketilen anlamına gelir. Bu durumda, daha fazla düğüm toohello ekleme hello en iyi şekilde tooscale kümedir. Merhaba yeni düğümler hello küme hello katılma sonra Service Fabric kümesi kaynak yöneticisi hizmetleri toothem hello varolan düğümleri üzerinde daha az toplam yük kaynaklanan taşır. Örnek sayısı ile durum bilgisi olmayan hizmetler için = -1, daha fazla hizmet örnekleri otomatik olarak oluşturulur. Bu, bazı çağrıları toomove hello varolan düğümleri toohello yeni düğümlerden sağlar. 

Ekleme ve kaldırma düğümleri toohello küme hello Service Fabric Azure Resource Manager PowerShell modülü yoluyla gerçekleştirilebilir.

```posh
Add-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName  -NumberOfNodesToAdd 5 
Remove-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName -NumberOfNodesToRemove 5
```

## <a name="putting-it-all-together"></a>Tüm bir araya getirme
Burada tartışılan ve bir örnek konuşun tüm hello fikirleri atalım. Hizmet aşağıdaki hello göz önünde bulundurun: toobuild bir adres defteri olarak davranan bir hizmeti üzerinde toonames ve ilgili kişi bilgileri bulunduran çalışıyorsunuz. 

Sağ Önden soruları ilgili tooscale bir grup vardır: kaç kullanıcının, devam eden toohave misiniz? Her kullanıcı kaç kişi depolayacak mı? Toofigure bu her şeyi çalışılırken zaman, hizmetiniz hello için yukarı ilk kez duran zordur. Belirli bir bölüm sayısı olan tek bir statik hizmetle toogo giderek varsayalım. bölüm sayısı toohave neden olabilecek hatalı hello çekme hello sonuçlarıyla sorunları daha sonra ölçeklendirin. Benzer şekilde, tüm hello bilgileri değil olabilir hello sağ sayısı çekme olsa bile, gerekir. Örneğin, ayrıca toodecide hello Önden, hello küme boyutunu hem hello düğüm sayısını ve boyutlarının bakımından vardır. Genellikle sabit toopredict tooconsume yaşam süresi boyunca hizmeti kaç kaynak geçiyor. Ayrıca, sabit tooknow hello hizmet gerçekte gördüğü zaman hello trafiği düzeni öncesinde de olabilir. Örneğin, olabilir kişileri ekleyin ve bunların yalnızca ilk şey hello sabah kaldırın veya belki de onu eşit olarak hello hello gün süresince dağıtılır. Tooscale ve dinamik olarak gerekebilir bunu temel alarak. Olabilir ve tooneed tooscale oluşturacağız, ancak her iki durumda da, büyük olasılıkla tooneed tooreact toochanging kaynak tüketimini hizmetiniz tarafından oluşturacağız toopredict öğrenebilirsiniz. Var olan kaynakların kullanımını yeniden düzenleme yeterli olmadığı durumlarda bu sipariş tooprovide hello kümede hello boyutunu değiştirme daha fazla kaynak içerebilir. 

Ancak neden toopick çıkışı tek bir bölüm düzeni tüm kullanıcılar için bile deneyin? Neden kendinizi tooone hizmeti ve bir statik küme sınırlamanıza? Merhaba gerçek genellikle daha dinamik bir durumdur. 

İçin ölçek oluştururken, dinamik desen aşağıdaki hello göz önünde bulundurun. Tooadapt gerekebilir, tooyour durum:

1. Toopick bölümleme düzeni Everyone grubu için önden çalışırken yerine, "Yöneticisi hizmeti" oluşturun.
2. Bunlar hizmetiniz için kaydolduğunuzda hello iş hello Yöneticisi hizmeti müşteri bilgilerine toolook ' dir. Hello Yöneticisi hizmeti bağlı olarak bu bilgileri oluşturun, sonra bir örneği, _gerçek_ kişi depolama hizmeti _yalnızca o müşteri için_. Belirli yapılandırma, yalıtım veya yükseltmeler ihtiyacınız varsa bu müşteri için uygulama örneğini yukarı toospin da karar verebilirsiniz. 

Bu dinamik oluşturma birçok avantaj Desen:

  - Önden tüm kullanıcılar için tooguess hello doğru bölüm sayısı çalıştığınız değil veya tüm kendi başına sonsuz ölçeklenebilir tek bir hizmet oluşturun. 
  - Farklı kullanıcılar aynı bölüm sayısı, çoğaltma sayısı, yerleşim kısıtlaması, ölçümleri, varsayılan yükleri, hizmet adlarını, dns ayarlarını veya herhangi birini hello hello hizmeti tarafından belirtilen diğer özellikleri toohave hello değilsiniz veya uygulama düzeyinde. 
  - Ek veri kesimleme kazanır. Her bir müşteri hello hizmeti, kendi kopyasına sahip
    - Her müşteri hizmeti farklı şekilde yapılandırılmış ve bölümleri veya çoğaltmaları gerekli kendi beklenen ölçekte dayalı olarak daha az veya daha fazla veya daha az kaynakları verildi.
      - Örneğin, hello müşteri Merhaba "Altın" katmanı Ücretli - daha fazla çoğaltmalar veya daha fazla bölüm sayısı alabilir ve potansiyel olarak tootheir Hizmetleri ölçümleri ve uygulama kapasiteleri aracılığıyla kaynakları ayrılmış söyleyin.
      - Veya söyleyin bunlar gereken kişileri hello sayısını belirten bilgi "Küçük" - yalnızca birkaç bölümleri elde etmesi veya hatta diğer müşteriler paylaşılan hizmet havuzuyla içine konmuş sağlanan.
  - Müşteriler tooshow için beklerken bir dizi hizmet örneği veya çoğaltmaları çalıştırdığınız değil
  - Bir müşteri hiç ayrılırsa, ardından hizmetinizden bilgilerini kaldırarak bu hizmeti veya oluşturulduğu uygulamayı silmek hello Yöneticisi sahip olarak kadar basittir.

## <a name="next-steps"></a>Sonraki adımlar
Service Fabric kavramlarla ilgili daha fazla bilgi için aşağıdaki makaleler hello bakın:

* [Service Fabric hizmetlerin kullanılabilirliğini](service-fabric-availability-services.md)
* [Service Fabric Hizmetleri bölümlendirme](service-fabric-concepts-partitioning.md)
