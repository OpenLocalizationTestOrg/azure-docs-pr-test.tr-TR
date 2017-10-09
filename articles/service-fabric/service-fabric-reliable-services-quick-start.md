---
title: "aaaCreate ilk Service Fabric uygulamanızı C# | Microsoft Docs"
description: "Giriş toocreating durum bilgisiz ve durum bilgisi olan hizmetler ile Microsoft Azure Service Fabric uygulaması."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Reliable Services özelliğini kullanmaya başlayın
> [!div class="op_single_selector"]
> * [Windows üzerinde C#](service-fabric-reliable-services-quick-start.md)
> * [Linux üzerinde Java](service-fabric-reliable-services-quick-start-java.md)
> 
> 

Azure Service Fabric uygulaması kodunuzu çalıştırmak bir veya daha fazla hizmet içeriyor. Bu kılavuz size nasıl gösterir toocreate durum bilgisiz ve durum bilgisi olan Service Fabric uygulamaları ile [Reliable Services](service-fabric-reliable-services-introduction.md).  Bu Microsoft Virtual Academy video de nasıl gösterir toocreate durum bilgisiz güvenilir hizmet:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965">  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a>Temel kavramlar
Reliable Services ile size yalnızca çalışmaya tooget birkaç temel kavramları toounderstand gerekir:

* **Hizmet türü**: hizmet uygulamanızın budur. Genişleten yazma hello sınıf tarafından tanımlanan `StatelessService` ve diğer kod veya bağımlılıkları, bir ad ve sürüm numarası ile birlikte kullanılır.
* **Hizmet örneği adlı**: toorun sınıf türü nesne örneklerini oluşturmak gibi hizmetiniz, adlandırılmış örnekleri, hizmet türüne ilişkin çok oluşturmak. Bir hizmet örneği hello kullanarak bir URI hello biçiminde olan bir ada sahip "fabric: /" gibi Düzen "fabric: / MyApp/MyService".
* **Hizmet ana bilgisayarı**: hizmet örneklerinin ihtiyacı toorun barındırma işlemi içinde oluşturduğunuz adlı hello. Merhaba hizmet ana bilgisayarı hizmet örneklerini çalıştırdığı yalnızca bir işlemdir.
* **Hizmet kayıt**: kayıt getirir her şeyi birlikte. Merhaba hizmet türü kaydedilmelidir Service Fabric hello ile bir hizmeti çalışma zamanı ana bilgisayar tooallow Service Fabric toocreate örnekleri toorun.  

## <a name="create-a-stateless-service"></a>Durum bilgisi olmayan bir hizmet oluşturma
Durum bilgisiz Hizmet şu anda hello norm bulut uygulamalarında hizmet türüdür. Merhaba hizmetin kendisini güvenilir bir şekilde depolanır veya yüksek oranda kullanılabilir hale toobe gereken veri içermediğinden durum bilgisiz olarak değerlendirilir. Durum bilgisiz Hizmeti'nin bir örneğini kapanırsa, iç durumu kaybolur. Bu tür hizmet, Azure tablo veya bir SQL veritabanı gibi dış depolama kalıcı tooan durumu olmalıdır için toobe yapılan yüksek oranda kullanılabilir ve güvenilir.

Visual Studio 2015 veya Visual Studio 2017 yönetici olarak başlatın ve adlı yeni bir Service Fabric uygulaması projesi oluşturduğunuzda *HelloWorld*:

![Merhaba yeni proje iletişim kutusu toocreate yeni bir Service Fabric uygulaması kullanın](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

Adlı bir durum bilgisiz hizmet projesi oluşturma *HelloWorldStateless*:

![Hello ikinci iletişim kutusunda, durum bilgisiz hizmet projesi oluşturma](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

Çözümünüzü şimdi iki proje içerir:

* *HelloWorld*. Merhaba budur *uygulama* içeren projesi, *Hizmetleri*. Ayrıca, uygulamanızı Merhaba uygulaması gibi bir dizi toodeploy Yardım PowerShell Betiği açıklar hello uygulama bildirimi içerir.
* *HelloWorldStateless*. Merhaba hizmet projesi budur. Merhaba durum bilgisiz hizmet uygulaması içerir.

## <a name="implement-hello-service"></a>Merhaba hizmet ekleme
Açık hello **HelloWorldStateless.cs** hello hizmet proje dosyasında. Service Fabric içinde bir hizmet iş mantığı çalıştırabilirsiniz. Merhaba hizmeti API'si kodunuz için iki giriş noktaları sağlar:

* Adlı bir uçlu giriş noktası yöntemi *RunAsync*, burada uzun süre çalışan işlem iş yükleri de dahil olmak üzere tüm iş yükleri yürütme başlayabilirsiniz.

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* Burada, iletişim yığınında ASP.NET Core gibi tercih ettiğiniz ekleyebilirsiniz iletişimi giriş noktası. Kullanıcılar ve diğer hizmetler isteklerini almak başlayabileceğiniz budur.

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

Bu öğreticide, biz hello odaklanacaktır `RunAsync()` giriş noktası yöntemi. Hemen kodunuzu çalıştırmaya başlayabileceğiniz budur.
Merhaba proje şablonu içeren bir örnek uygulaması `RunAsync()` , çalışırken sayısını artırır.

> [!NOTE]
> Nasıl bir iletişimle toowork yığın hakkında daha fazla bilgi için bkz [OWIN kendi kendine barındırma ile Service Fabric Web API Hizmetleri](service-fabric-reliable-services-communication-webapi.md)
> 
> 

### <a name="runasync"></a>RunAsync
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

bir hizmet örneği yerleştirilen ve hazır tooexecute olduğunda hello platform bu yöntemi çağırır. Merhaba hizmet örneği açıldığında durumsuz bir hizmet için basitçe anlamına gelir. Hizmet örneğinizi kapalı toobe gerektiğinde bir iptal belirteci toocoordinate sağlanır. Service Fabric bu hizmet örneği Aç/Kapat döngüsünü hello hizmetinin birçok kez hello ömrü boyunca bir bütün olarak ortaya çıkabilir. Bu da dahil olmak üzere çeşitli nedenlerden kaynaklanabilir:

* Merhaba sistem, hizmet örneği için kaynak Dengeleme taşır.
* Kodunuzdaki hataları oluşur.
* Merhaba uygulama veya sistem yükseltilir.
* Merhaba temel alınan donanım kesinti karşılaşır.

Bu düzenlemesi hello sistem tookeep tarafından yönetilen hizmetinizi yüksek oranda kullanılabilir ve düzgün şekilde dengeli.

`RunAsync()`zaman uyumlu olarak bloğu değil. Uygulamanıza RunAsync, bir görev döndürür veya herhangi uzun süre çalışan veya engelleme işlemleri tooallow hello çalışma zamanı toocontinue bekler. Merhaba notta `while(true)` hello önceki örnekte, bir görev döndüren bir döngüde `await Task.Delay()` kullanılır. İş yükünüzün zaman uyumlu olarak engellemelidir, yeni bir görev ile zamanlamalısınız `Task.Run()` içinde `RunAsync` uygulaması.

İş yükünüzün iptaline iptal belirteci sağlanan hello tarafından düzenlenmiş işbirlikçi çaba ' dir. Merhaba sistem (başarılı bir şekilde tamamlandığında, iptal veya hataya göre) için görev tooend bekleyecek taşır önce. Herhangi bir iş ve çıkış önemli toohonor hello iptal belirteci, bitiş olduğu `RunAsync()` hello sistem iptal istediğinde mümkün olan en kısa sürede.

Bu durum bilgisiz hizmet örnekte hello sayısı yerel bir değişkende depolanır. Ancak bu durum bilgisi olmayan bir hizmet olduğundan, yalnızca hello geçerli yaşam döngüsünü kendi hizmet örneği için depolanan hello değeri yok. Merhaba hizmet taşır veya yeniden hello değeri kayıp olur.

## <a name="create-a-stateful-service"></a>Durum bilgisi olan bir hizmet oluşturma
Service Fabric hizmetinin durum bilgisi olan yeni bir tür tanıtır. Durum bilgisi olan hizmet tarafından kullanıldığı hello kod ile birlikte bulunan güvenilir bir şekilde hello hizmetin kendisini içinde durumu koruyabilirsiniz. Durum Service Fabric tarafından hello gerek toopersist durum tooan dış depolama yüksek oranda kullanılabilir hale getirilir.

Merhaba hizmet taşır veya yeniden başlatır, olsa bile tooconvert durum bilgisiz toohighly kullanılabilir ve kalıcı bir sayaç değeri, bir durum bilgisi olan hizmet gerekir.

İçinde aynı hello *HelloWorld* uygulama hello Hizmetleri başvurularında hello uygulama projesi ve seçerek üzerinde sağ tıklayarak yeni bir hizmet ekleyebilirsiniz **Ekle -> Yeni yapı hizmeti**.

![Hizmet tooyour Service Fabric uygulaması ekleyin](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

Seçin **durum bilgisi olan hizmet** ve adlandırın *HelloWorldStateful*. **Tamam** düğmesine tıklayın.

![Merhaba yeni proje iletişim kutusu toocreate yeni bir Service Fabric durum bilgisi olan hizmet kullanın](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

Uygulamanızı şimdi iki Hizmetleri olmalıdır: Merhaba durum bilgisiz hizmet *HelloWorldStateless* ve hello durum bilgisi olan hizmet *HelloWorldStateful*.

Durum bilgisi olan bir hizmet hello sahiptir ve durum bilgisi olmayan hizmet olarak aynı giriş noktaları. Merhaba ana farktır hello kullanılabilirliğini bir *durum sağlayıcısı* , saklayabilir durumu güvenilir. Service Fabric adlı durum sağlayıcısı bir uygulama ile birlikte gelen [güvenilir koleksiyonları](service-fabric-reliable-services-reliable-collections.md), olanak sağlayan güvenilir durum Yöneticisi hello yoluyla çoğaltılan veri yapılarını oluşturmanıza. Durum bilgisi olan güvenilir hizmet varsayılan olarak bu durum sağlayıcısı kullanır.

Açık **HelloWorldStateful.cs** içinde *HelloWorldStateful*, RunAsync yöntemi aşağıdaki hello içerir:

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a>RunAsync
`RunAsync()`durum bilgisi olan ve durum bilgisiz Hizmetleri'nde benzer şekilde çalışır. Yürütülmeden önce ancak, bir durum bilgisi olan hizmeti hello platform ek çalışma sizin adınıza gerçekleştirir `RunAsync()`. Bu iş o hello güvenilir durum Yöneticisi sağlama içerebilir ve hazır toouse güvenilir koleksiyonlarıdır.

### <a name="reliable-collections-and-hello-reliable-state-manager"></a>Güvenilir koleksiyonları ve hello güvenilir durum Yöneticisi
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) tooreliably deposu durumu hello hizmetindeki kullanabilirsiniz bir sözlük uygulamasıdır. Service Fabric ve güvenilir koleksiyonlarla, hizmetiniz için bir dış kalıcı depoya hello gerek kalmadan doğrudan veri depolayabilirsiniz. Güvenilir koleksiyonları verilerinizin yüksek oranda kullanılabilir yap. Service Fabric gerçekleştirir, bu, oluşturma ve birden çok yönetme *çoğaltmaları* hizmetinizin sizin için. Ayrıca, bu çoğaltmaların ve bunların durumu geçişleri yönetme koyma hello karmaşıklık soyutlar bir API sağlar.

Güvenilir koleksiyonları birkaç uyarılar, özel türleri dahil olmak üzere, herhangi bir .NET türü depolayabilirsiniz:

* Service Fabric durumunuza tarafından yüksek oranda kullanılabilir kılar *çoğaltma* durumunu düğümler ve güvenilir koleksiyonları arasında her kopyada veri toolocal diski depolamak. Bu güvenilir koleksiyonu içinde depolanan her şey olması gerektiği anlamına gelir *seri hale getirilebilir*. Varsayılan olarak, güvenilir koleksiyonları kullanmaya [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) seri hale getirme için bu nedenle olduğu önemli toomake türlerinizi olduğundan emin [hello veri sözleşmesi seri hale getirici tarafından desteklenen](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) hello varsayılan kullandığınızda Serileştirici.
* Güvenilir derlemeler işlemleri yaparsanız nesneleri yüksek kullanılabilirlik için çoğaltılır. Güvenilir koleksiyonu içinde depolanan nesneleri hizmetinizi yerel bellekte tutulur. Bu, yerel başvuru toohello nesnesi olduğu anlamına gelir.
  
   Bu nesne yerel örnekleri işlemde hello güvenilir koleksiyonu bir güncelleştirme işlemi gerçekleştirilirken olmadan mutate değil, önemlidir. Değişiklikleri toolocal nesnelerinin örneklerini otomatik olarak çoğaltılmayacak olmasıdır. Merhaba nesneyi geri hello sözlükteki yeniden eklemek veya hello birini kullanın *güncelleştirme* hello sözlük yöntemleri.

Merhaba güvenilir durum Yöneticisi güvenilir koleksiyonları tarafından yönetilir. Yalnızca hello güvenilir durum Yöneticisi için güvenilir bir koleksiyon adıyla herhangi bir zamanda ve herhangi bir yerde hizmetinizi sorabilirsiniz. bir başvuru ulaşırsınız Hello güvenilir durum Yöneticisi sağlar. Verme önerilir, başvuruları tooreliable koleksiyonu örnekleri sınıf üyesi değişkenleri veya özellikleri kaydetmeniz. Merhaba başvuru ayarlandığını tooensure önemi gerçekleştirilecek tooan örneği hello hizmet çevriminin her zaman. Merhaba güvenilir durum Yöneticisi bu iş, işler ve yineleme ziyaretleriniz için optimize edilmiştir.

### <a name="transactional-and-asynchronous-operations"></a>İşlem ve zaman uyumsuz işlemler
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

Merhaba çoğunu sahip güvenilir koleksiyonların aynı işlemleri, kendi `System.Collections.Generic` ve `System.Collections.Concurrent` ortaklarınıza LINQ hariç. Güvenilir derlemeler işlemleri zaman uyumsuzdur. Yazma işlemleri güvenilir koleksiyonlarıyla g/ç işlemleri tooreplicate gerçekleştirmek ve veri toodisk kalır olmasıdır.

Güvenilir toplama işlemleri *işlem*, böylece, durumu tutarlı birden çok güvenilir koleksiyonları ve işlemler arasında tutabilirsiniz. Örneğin, bir iş öğesi güvenilir bir kuyruktan dequeue bir işlem gerçekleştirmek ve sözlükteki güvenilir, tümü tek bir işlem içinde hello sonucu kaydetmek. Bu atomik bir işlem olarak kabul edilir ve hello tüm işlemi başarılı olur veya hello tüm işlemi geri alma güvence altına alır. Merhaba öğesi dequeue sonra bir hata oluşursa, ancak hello sonuç kaydetmeden önce hello tüm işlem geri alındı ve işleme hello sırasındaki hello öğesi kalır.

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın
Şimdi toohello döndürürüz *HelloWorld* uygulama. Artık, yapı ve hizmetlerinizi dağıtabilirsiniz. Bastığınızda **F5**, uygulamanızı oluşturulan ve dağıtılan tooyour yerel küme olacaktır.

Merhaba çalışmaya başlamak Hizmetleri sonra oluşturulan hello olay Windows için izleme (ETW) olayları görüntüleyebilirsiniz bir **tanılama olayları** penceresi. Görüntülenen hello olaylar hello durum bilgisi olmayan hizmet ve durum bilgisi olan hizmeti hello uygulamasında hello olduğuna dikkat edin. Merhaba tıklayarak hello akış duraklatabilirsiniz **duraklatma** düğmesi. Bu iletiyi genişleterek sonra bir ileti hello ayrıntılarını inceleyebilirsiniz.

> [!NOTE]
> Merhaba uygulamayı çalıştırmadan önce çalıştıran bir yerel geliştirme kümesine sahip olduğunuzdan emin olun. Merhaba denetleyin [Başlangıç Kılavuzu](service-fabric-get-started.md) yerel ortamınızı ayarlama hakkında bilgi için.
> 
> 

![Visual Studio tanılama olaylarını görüntüle](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a>Sonraki adımlar
[Service Fabric uygulamanızı Visual Studio'da hata ayıklama](service-fabric-debugging-your-application.md)

[Kullanmaya başlama: OWIN kendi kendine barındırma ile Service Fabric Web API Hizmetleri](service-fabric-reliable-services-communication-webapi.md)

[Güvenilir Koleksiyonlar hakkında daha fazla bilgi edinin](service-fabric-reliable-services-reliable-collections.md)

[Bir uygulamayı dağıtma](service-fabric-deploy-remove-applications.md)

[Uygulama yükseltme](service-fabric-application-upgrade.md)

[Güvenilir hizmetler için Geliştirici Başvurusu](https://msdn.microsoft.com/library/azure/dn706529.aspx)

