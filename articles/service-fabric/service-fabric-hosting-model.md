---
title: "Service Fabric barındırma modeli aaaAzure | Microsoft Docs"
description: "Dağıtılan bildirimleri yapı hizmeti ve hizmet ana bilgisayar işlemi çoğaltmaları (veya örnekleri) arasındaki ilişkiyi açıklar."
services: service-fabric
documentationcenter: .net
author: harahma
manager: timlt
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/15/2017
ms.author: harahma
ms.openlocfilehash: 30e0ba19cd672a722f76477a311ecef7c213b055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-hosting-model"></a>Service Fabric barındırma modeli
Bu makale, Service Fabric tarafından sağlanan modelleri barındıran uygulama genel bir bakış sağlar ve hello hello farklılıkları açıklar **paylaşılan işlem** ve **özel işlem** modeller. Dağıtılan bir uygulama, bir Service Fabric düğümü ve hello hizmeti ve hello hizmet ana bilgisayar işlemi çoğaltmaları (veya örnekleri) arasındaki ilişkiyi nasıl göründüğünü açıklayan.

Devam etmeden önce aşina olduğundan emin olun [Service Fabric uygulama modeli] [ a1] ve çeşitli kavramlar ve aralarındaki ilişkisi anladığınızdan emin olun. 

> [!NOTE]
> Basitlik için bu makalede, açıkça belirtilmediği sürece:
>
> - Word'ün tüm kullanır *çoğaltma* tooboth durum bilgisi olan bir hizmet veya statless hizmet örneğini bir çoğaltma başvuruyor.
> - *CodePackage* kabul çok eşdeğerdir*ServiceHost* kaydeder işlem bir *ServiceType* ve hizmetlerin, konaklar çoğaltmaları *ServiceType*.
>

toounderstand barındırma modeli Merhaba, bize bir örnek yol. Bize söyleyin, sahip olduğumuz bir *ApplicationType* 'olan MyAppType' bir *ServiceType* 'tarafından sağlanan MyServiceType' *ServicePackage* 'olan MyServicePackage' bir *CodePackage* 'hangi kaydeder MyCodePackage' *ServiceType* 'çalıştırıldığında MyServiceType'.

Diyelim ki 3 düğümlü bir kümeniz olduğuna ve oluşturuyoruz bir *uygulama* **fabric: / App1** 'MyAppType' türünde. Bu içinde *uygulama* **fabric: / App1** hizmet oluşturuyoruz **doku: / App1/ServiceA** '2 bölümleri olan MyServiceType' türünde (söyleyin **P1**  &  **P2**) ve bölüm başına 3 çoğaltmaları. Merhaba Aşağıdaki diyagramda bu uygulamayı şekilde hello görünümünü sona eriyor dağıtılan bir düğümde gösterilmektedir.

<center>
![Dağıtılmış uygulama düğümü görünümü][node-view-one]
</center>

Service Fabric etkinleştirilmiş '', her iki hello bölümleri çoğaltmalardan yani barındırma MyCodePackage' başlatılan MyServicePackage' **P1** & **P2**. Merhaba kümedeki düğümlerin eşit toonumber bölüm başına çoğaltmaların sayısı Seçtiğimiz hello kümedeki tüm hello düğümler aynı görünümü sahip gerektiğini unutmayın. Başka bir hizmet oluşturalım **doku: / App1/ServiceB** uygulamada **fabric: / App1** 1 bölümü olan (söyleyin **P3**) ve bölüm başına 3 çoğaltmaları. Aşağıdaki diyagramda, yeni bir görünüm hello hello düğümünde gösterilmektedir:

<center>
![Dağıtılmış uygulama düğümü görünümü][node-view-two]
</center>

Service Fabric bölümü için yeni çoğaltma hello yerleştirilen görebiliriz gibi **P3** hizmetinin **fabric: / App1/ServiceB** 'MyServicePackage' ın hello varolan etkinleştirme. Şimdi sağlar başka oluşturmak *uygulama* **fabric: / App2** 'MyAppType' türünde ve içinde **doku: / App2** hizmet oluşturma **doku: / App2/ServiceA** 2 bölümleri olan (söyleyin **P4** & **P5**) ve bölüm başına 3 çoğaltmaları. Diyagramları aşağıdaki hello yeni düğümü görünüm gösterir:

<center>
![Dağıtılmış uygulama düğümü görünümü][node-view-three]
</center>

Bu süre Service Fabric etkinleştirilmiş 'hem de hizmet bölümlerden 'MyCodePackage' ve çoğaltmaları yeni bir kopyasını başlatan MyServicePackage' ın yeni bir kopyasını **fabric: / App2/ServiceA** (yani **P4**  &  **P5**) bu yeni kopya 'MyCodePackage' yerleştirilir.

## <a name="shared-process-model"></a>Paylaşılan işlem modeli
Ne yukarıda hello varsayılan barındırma modeli Service Fabric tarafından sağlanan ve gördüğümüz tooas başvurulan **paylaşılan işlem** modeli. Bu modelde için bir verilen *uygulama*, yalnızca bir kopya bir verilen *ServicePackage* üzerinde etkinleştirilmiş bir *düğümü* (tüm hello başladığı *CodePackages* içerdiği) ve tüm çoğaltmaları tüm hizmetlerin hello bir verilen *ServiceType* hello yerleştirilir *CodePackage* , kaydeder *ServiceType*. Diğer bir deyişle, tüm çoğaltmaları tüm hizmetlerin hello bir verilen *ServiceType* paylaşmak hello aynı işlemi.

## <a name="exclusive-process-model"></a>Özel işlem modeli
Merhaba Service Fabric tarafından sağlanan diğer barındırma modeldir **özel işlem** modeli. Bu modelde, üzerinde bir verilen *düğümü*, her çoğaltma yerleştirmek için Service Fabric yeni bir kopyasını etkinleştirir *ServicePackage* (tüm hello başladığı *CodePackages* içerdiği ) ve çoğaltma hello yerleştirilir *CodePackage* bu kayıtlı hello *ServiceType* hello hizmet toowhich çoğaltmanın ait. Diğer bir deyişle, her çoğaltma adanmış kendi işleminde yaşar. 

Bu model, sürüm Service Fabric 5.6 itibaren desteklenmektedir. **Özel işlem** modeli hello hizmet oluşturmaya hello aynı anda seçilen (kullanarak [PowerShell][p1], [REST] [ r1]veya [FabricClient][c1]) belirterek **ServicePackageActivationMode** 'ExclusiveProcess' olarak.

```powershell
PS C:\>New-ServiceFabricService -ApplicationName "fabric:/App1" -ServiceName "fabric:/App1/ServiceA" -ServiceTypeName "MyServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1 -ServicePackageActivationMode "ExclusiveProcess"
```

```csharp
var serviceDescription = new StatelessServiceDescription
{
    ApplicationName = new Uri("fabric:/App1"),
    ServiceName = new Uri("fabric:/App1/ServiceA"),
    ServiceTypeName = "MyServiceType",
    PartitionSchemeDescription = new SingletonPartitionSchemeDescription(),
    InstanceCount = -1,
    ServicePackageActivationMode = ServicePackageActivationMode.ExclusiveProcess
};

var fabricClient = new FabricClient(clusterEndpoints);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Varsayılan hizmet uygulama bildiriminizi varsa, seçebileceğiniz **özel işlem** belirterek model **ServicePackageActivationMode** özniteliği aşağıda gösterildiği gibi:

```xml
<DefaultServices>
  <Service Name="MyService" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
      <SingletonPartition/>
    </StatelessService>
  </Service>
</DefaultServices>
```
Yukarıdaki örnekle devam edersek, başka bir hizmet oluşturma sağlar **doku: / App1/ServiceC** uygulamada **fabric: / App1** 2 bölümleri olan (söyleyin **P6**  &  **7**) ve bölüm başına 3 çoğaltmaları **ServicePackageActivationMode** too'ExclusiveProcess ayarlayın. Aşağıdaki diyagramda hello düğümünde yeni bir görünüm gösterir:

<center>
![Dağıtılmış uygulama düğümü görünümü][node-view-four]
</center>

Gördüğünüz gibi iki yeni kopyasını 'MyServicePackage' Service Fabric etkinleştirilmiş (bölümünden her çoğaltma için bir tane **P6** & **7**) ve ayrılmış kopyasınıherçoğaltmayerleştirilmiş*CodePackage*. Başka bir şey toonote burada olduğundan, ne zaman **özel işlem** modeli kullanılır, için bir verilen *uygulama*, birden çok kopya bir verilen *ServicePackage* üzerindeetkinolabilir *Düğüm*. İçinde Yukarıdaki örnek, biz 'MyServicePackage' üç kopyasını için etkin olup olmadığını **fabric: / App1**. Her 'MyServicePackage' etkin bu kopyasını sahip bir **ServicePackageAtivationId** içinde bu kopyayı tanımlayan ilişkili *uygulama* **fabric: / App1**.

Sadece **paylaşılan işlem** modeli için kullanılan bir *uygulama*gibi **doku: / App2** , yukarıdaki örnek, yoktur, yalnızca bir etkin kopyanın *ServicePackage*  üzerinde bir *düğümü* ve **ServicePackageAtivationId** bu etkinleştirmesi için *ServicePackage* ' boş bir dize '.

> [!NOTE]
>- **İşlem paylaşılan** barındırma modeli karşılık gelen çok**ServicePackageAtivationMode** eşit **SharedProcess**. Bu barındırma modeli hello varsayılandır ve **ServicePackageAtivationMode** hello hizmet oluşturmaya hello zaman belirtilmesi gerekmez.
>
>- **Özel işlem** barındırma modeli karşılık gelen çok**ServicePackageAtivationMode** eşit **ExclusiveProcess** ve hello oluşturma hello zaman açıkça belirtilen toobe gerekiyor hizmet. 
>
>- Bir hizmet barındırma modeli bilinir hello sorgulayarak [hizmet açıklaması] [ p2] ve değeri **ServicePackageAtivationMode**.
>
>

## <a name="working-with-deployed-service-package"></a>Dağıtılan hizmet paketi ile birlikte çalışma
Etkin bir kopyasını bir *ServicePackage* bir düğüm olarak adlandırılır [hizmet paketi dağıtılan][p3]. Daha önce ne zaman yukarıdaki **özel işlem** modeli için hizmetleri oluşturmak için kullanılan bir verilen *uygulama*, olabilir birden fazla dağıtılmış hizmet paketleri Merhaba aynı  *ServicePackage*. İşlemleri gerçekleştirirken belirli toodeployed hizmet paketi ister [dağıtılmış hizmet paketi durumunu raporlama] [ p4] veya [dağıtılan hizmet paketikodpaketiyenidenbaşlatılıyor] [ p5] vb. **ServicePackageActivationId** gereksinimlerini toobe sağlanan tooidentify belirli dağıtılmış hizmet paketi.

 **ServicePackageActivationId** dağıtılan bir hizmet paketi hello listesi sorgulayarak elde edilebilir [hizmet paketleri dağıtılan] [ p3] bir düğüm üzerinde. Sorgulanırken [hizmet türleri dağıtılan][p6], [çoğaltmaları dağıtılan] [ p7] ve [kodu paketleridağıtılan] [ p8] bir düğümde hello sorgu sonucu hello de içeren **ServicePackageActivationId** üst dağıtılmış hizmet paketi.

> [!NOTE]
>- Altında **paylaşılan işlem** üzerinde barındırma modeli, bir verilen *düğümü*, için bir verilen *uygulama*, yalnızca bir kopya bir *ServicePackage* etkinleştirilir . Bunun **ServicePackageActivationId** çok eşit*boş dize* ve işlemleri gerçekleştirme dağıtılmış hizmet paketi ilişkili belirtilmesi gerekmez. 
>
> - Altında **özel işlem** üzerinde barındırma modeli, bir verilen *düğümü*, için bir verilen *uygulama*, bir veya daha fazla kopyasını içeren bir *ServicePackage* can etkin olması. Her etkinleştirme sahip bir *boş* **ServicePackageActivationId** ve işlemleri gerçekleştirme dağıtılmış hizmet paketi ilişkili belirtilen toobe gerekiyor. 
>
> - Varsa **ServicePackageActivationId** too'empty dize varsayılan olarak ommited olan '. Dağıtılan bir hizmet paketini, altında etkinleştirildi **paylaşılan işlem** modeli varsa, sonra işlemi gerçekleştirilmesi üzerinde Aksi takdirde hello işlemi başarısız olur.
>
> - Bir kez tooquery ve önbellek önerilmez **ServicePackageActivationId** dinamik olarak oluşturulur ve çeşitli nedenlerle değiştirebilirsiniz. Gerektiren bir işlem gerçekleştirmeden önce **ServicePackageActivationId**, önce hello listesi sorgu [hizmet paketleri dağıtılan] [ p3] düğümünü ve ardından kullanıma  *ServicePackageActivationId** sorgu sonucu tooperform hello özgün işlem.
>
>

## <a name="guest-executable-and-container-applications"></a>Konuk çalıştırılabilir ve kapsayıcı uygulamaları
Service Fabric değerlendirir [Konuk yürütülebilir] [ a2] ve [kapsayıcı] [ a3] , yani müstakil statless Hizmetleri olarak uygulamaları hiçbir Service Fabric çalışma zamanı yok *ServiceHost* (bir işlem veya kapsayıcı). Bu hizmetler kendi içinde bulunan olduğundan çoğaltmaların sayısı *ServiceHost* bu hizmetler için geçerli değildir. Merhaba hizmetlerle kullanılan en yaygın tek bölümlü yapılandırmadır ile [Instancecount] [ c2] eşit çok-1 (örn. bir kopyası her bir küme düğümünde hello servis kodu). 

Merhaba varsayılan **ServicePackageActivationMode** için bu hizmetleri **SharedProcess** Service Fabric yalnızca bir kopyasını etkinleştirir; bu durumda *ServicePackage* üzerinde bir *Düğümü* için bir verilen *uygulama* hizmeti kodunu yalnızca bir kopyasını başka bir deyişle, çalışacak bir *düğümü*. Hizmet kod toorun birden çok kopyasını istiyorsanız bir *düğümü* birden fazla hizmet oluşturduğunuzda (*Service1* çok*ServiceN*), *ServiceType* (belirtilen *ServiceManifest*) ya da hizmetiniz çoklu bölümlenmiş olduğunda belirtmelisiniz **ServicePackageActivationMode** olarak **ExclusiveProcess**hello hizmet oluşturmaya hello zaman.

## <a name="changing-hosting-model-of-an-existing-service"></a>Var olan bir hizmet barındırma modelini değiştirme
Varolan bir hizmetinden barındırma modelini değiştirme **paylaşılan işlem** çok**özel işlem** tersi yükseltme veya güncelleştirme mekanizması (veya varsayılan uygulama belirtiminde hizmet aracılığıyla bildirim) şu anda desteklenmiyor. Bu özellik için destek gelecek sürümlerde gelecektir.

## <a name="choosing-between-shared-process-and-exclusive-process-model"></a>Paylaşılan işlem ve özel işlem modeli arasında seçim yapma
Hem bu barındırma modellerini kendi Artıları ve eksileri sahip ve kullanıcı hangisinin gereksinimlerine en uygun tooevaluate gerekiyor. **İşlem paylaşılan** modeli sağlayan daha iyi kullanımı, işletim sistemi kaynaklarının daha az işlemleri kökenli olduğundan, birden çok yinelemede hello aynı işlemi, bağlantı noktaları, vb. paylaşabilir. Ancak, hello çoğaltmaları birini burada hello hizmet konağı aşağı toobring gereken bir hata değerse, diğer tüm çoğaltmaları aynı işlemde etkiler.

 **Özel işlem** modeli de kendi işleminde her çoğaltma ile daha iyi yalıtımı sağlar ve hatalı davranan çoğaltma diğer çoğaltmaları etkilemez. Bunu burada bağlantı noktası paylaşımı hello iletişim protokolü tarafından desteklenmeyen durumlarda kullanışlı devreye girer. Merhaba özelliği tooapply kaynak İdaresi çoğaltma düzeyinde kolaylaştırır. Üzerinde diğer yandan hello **özel işlem** hello düğüm üzerindeki her çoğaltma için bir işlem olarak çoğaltılır daha fazla işletim sistemi kaynağı tüketir.

## <a name="exclusive-process-model-and-application-model-considerations"></a>Özel işlem modelini ve uygulama konuları modeli
Service Fabric uygulamanızı Hello önerilen yolu toomodel tookeep biri olan *ServiceType* başına *ServicePackage* ve bu modeli de hello uygulamalarının çoğu için çalışır. 

Ancak, tooenable özel senaryolar bir yerde *ServiceType* başına *ServicePackage* işlevsel olarak, Service Fabric sağlayan bir birden çok toohave, istenebilir değil *ServiceType* başına *ServicePackage* (ve bir *CodePackage* birden fazla kaydedebilirsiniz *ServiceType*). Burada, bu yapılandırmalar yararlı olabilir hello senaryolardan bazıları şunlardır:

- Daha az işlemleri örnekten oluşturmak ve işlem başına daha yüksek yineleme yoğunluğu olan toooptimize işletim sistemi kaynak kullanımı istiyor.
- Farklı ServiceTypes çoğaltmalardan tooshare yüksek başlatma veya maliyet bellek varsa bazı ortak veri gerekir.
- Ücretsiz hizmet sunumu varsa ve aynı işlemde hello hizmetinin tüm çoğaltmaları koyarak tooput kaynak kullanımı bir sınırı istiyorsanız.

**Özel işlem** barındırma modeli değil tutarlı sahip birden çok uygulama modeliyle *ServiceTypes* başına *ServicePackage*. Bunun nedeni birden çok, *ServiceTypes* başına *ServicePackage* tasarlanmış tooachieve daha yüksek kaynak çoğaltmalar arasında paylaşımı ve işlem başına daha yüksek yineleme yoğunluğu sağlar. Bulmadýðýný toowhat budur **özel işlem** tasarlanmış tooachieve modelidir.

Birden çok Hello durumunu göz önünde bulundurun *ServiceTypes* başına *ServicePackage* farklı ile *CodePackage* her kaydetme *ServiceType*. Bizim düşünelim bir *ServicePackage* 'iki olan MultiTypeServicePackge' *CodePackages*:

- 'Da kaydeder MyCodePackageA' *ServiceType* 'MyServiceTypeA'.
- 'Da kaydeder MyCodePackageB' *ServiceType* 'MyServiceTypeB'.

Şimdi sağlar söyleyin oluşturuyoruz bir *uygulama* **fabric: / SpecialApp** ve iç **doku: / SpecialApp** iki Hizmetleri ile aşağıdaki oluşturmak **özel İşlem** modeli:

- Hizmet **fabric: / SpecialApp/ServiceA** iki bölüm 'MyServiceTypeA' türünde (söyleyin **P1** ve **P2**) ve bölüm başına 3 çoğaltmaları.
- Hizmet **fabric: / SpecialApp/ServiceB** iki bölüm 'MyServiceTypeB' türünde (söyleyin **P3** ve **P4**) ve bölüm başına 3 çoğaltmaları.

Belirli bir düğümde hem hello hizmetleri her iki çoğaltma sahip olur. Kullandık beri **özel işlem** modeli toocreate hello Hizmetleri, Service Fabric 'MyServicePackge' ın yeni bir kopyasını her çoğaltma için etkinleşir. Her etkinleştirme 'MultiTypeServicePackge', 'MyCodePackageA' ve 'MyCodePackageB' bir kopyasını başlar. Ancak, 'MyCodePackageA' veya 'MyCodePackageB' yalnızca biri 'MultiTypeServicePackge' etkinleştirildiği hello çoğaltmasını barındıracak. Aşağıdaki diyagramda hello düğümü görünümü gösterilmektedir:

<center>
![Dağıtılmış uygulama düğümü görünümü][node-view-five]
</center>

 'MultiTypeServicePackge' hello etkinleştirme bölümünün yinelemenin görebiliriz gibi **P1** hizmetinin **fabric: / SpecialApp/ServiceA**, 'MyCodePackageA' hello çoğaltma barındırma ve ' MyCodePackageB' yalnızca başlatıldı ve çalışıyor. Benzer şekilde, 'MultiTypeServicePackge' etkinleştirme bölümünün yinelemenin içinde **P3** hizmetinin **fabric: / SpecialApp/ServiceB**, 'MyCodePackageB' hello çoğaltma barındırma ve 'MyCodePackageA' ise Yalnızca hazır ve çalışır ve benzeri. Bu nedenle, daha fazla sayıda hello *CodePackages* (farklı kaydetme *ServiceTypes*) başına *ServicePackage*, yedekli kaynak kullanımı daha yüksek olur. 
 
 Üzerinde hello diğer yandan biz Hizmetleri oluşturursanız **doku: / SpecialApp/ServiceA** ve **fabric: / SpecialApp/ServiceB** ile **paylaşılan işlem** Service Fabric işlem modeli için 'MultiTypeServicePackge' yalnızca bir kopyasını etkinleştirmek *uygulama* **fabric: / SpecialApp** (daha önce gördüğümüz gibi). 'MyCodePackageA' ana bilgisayar hizmeti için tüm çoğaltmaları **fabric: / SpecialApp/ServiceA** (veya, herhangi bir hizmet türü 'MyServiceTypeA' toobe daha kesin) ve 'MyCodePackageB' ana bilgisayar hizmeti için tüm çoğaltmaları **fabric: / SpecialApp/ServiceB** (veya, herhangi bir hizmet türü 'MyServiceTypeB' toobe daha kesin). Aşağıdaki diyagramda bu ayarda hello düğümünü görüntüler: 

<center>
![Dağıtılmış uygulama düğümü görünümü][node-view-six]
</center>

Yukarıdaki örnek Hello 'MyCodePackageA', 'MyServiceTypeA' ve 'MyServiceTypeB' kaydeder ve hiçbir 'MyCodePackageB' yoktur durumunda Hayır yedekli da olacaktır düşünebilirsiniz *CodePackage* çalışıyor. Bu doğru ise, ancak, daha önce belirtildiği gibi bu uygulama modeli ile yeteri kadar uyuşmasa **özel işlem** barındırma modeli. Hedef tooput ise, her yinelemede kendi adanmış hem kaydetme işlemini *ServiceTypes* aynı gelen *CodePackage* gerekli değildir ve her koyma *ServiceType* içinde kendi *ServicePacakge* daha doğal bir seçimdir.

## <a name="next-steps"></a>Sonraki adımlar
[Bir uygulama paketi] [ a4] ve hazır toodeploy alın.

[Dağıtma ve uygulamaları kaldırma] [ a5] açıklar nasıl toouse PowerShell toomanage uygulama örnekleri.

<!--Image references-->
[node-view-one]: ./media/service-fabric-hosting-model/node-view-one.png
[node-view-two]: ./media/service-fabric-hosting-model/node-view-two.png
[node-view-three]: ./media/service-fabric-hosting-model/node-view-three.png
[node-view-four]: ./media/service-fabric-hosting-model/node-view-four.png
[node-view-five]: ./media/service-fabric-hosting-model/node-view-five.png
[node-view-six]: ./media/service-fabric-hosting-model/node-view-six.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[a1]: service-fabric-application-model.md
[a2]: service-fabric-deploy-existing-app.md
[a3]: service-fabric-containers-overview.md
[a4]: service-fabric-package-apps.md
[a5]: service-fabric-deploy-remove-applications.md

[r1]: https://docs.microsoft.com/rest/api/servicefabric/sfclient-api-createservice

[c1]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync
[c2]: https://docs.microsoft.com/dotnet/api/system.fabric.description.statelessservicedescription.instancecount

[p1]: https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice
[p2]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricservicedescription
[p3]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicePackage
[p4]: https://docs.microsoft.com/powershell/servicefabric/vlatest/send-servicefabricdeployedservicepackagehealthreport
[p5]: https://docs.microsoft.com/powershell/servicefabric/vlatest/restart-servicefabricdeployedcodepackage
[p6]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicetype
[p7]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedreplica
[p8]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedcodepackage