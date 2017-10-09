---
title: "aaaReliable üzerinde Service Fabric aktör | Microsoft Docs"
description: "Reliable Actors Reliable Services üzerinde katmanlanmış ve hello Service Fabric platformundan hello özellikleriyle nasıl açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: ecffb54139f1171c7839b77fed0be60950881198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a>Reliable Actors hello Service Fabric platformundan kullanma
Bu makalede, Reliable Actors hello Azure Service Fabric platformda nasıl çalıştığı açıklanmıştır. Güvenilir aktörler Çalıştır hello olarak adlandırılan bir durum bilgisi olan güvenilir hizmet uygulaması içinde barındırılan bir çerçeve *aktör hizmeti*. Merhaba aktör hizmeti tüm hello bileşenleri gerekli toomanage hello yaşam döngüsü ve ileti, aktörleri göndermeyi içerir:

* Merhaba aktör çalışma zamanı yaşam döngüsü, atık toplama yönetir ve tek iş parçacıklı erişimini zorunlu kılar.
* Aktör hizmeti remoting dinleyicisi uzaktan erişim çağrıları tooactors kabul eder ve bunları tooa dağıtıcısı tooroute toohello uygun aktör örneği gönderir.
* Merhaba aktör durumu sağlayıcısı (gibi hello güvenilir koleksiyonları durumu sağlayıcısı) durumu sağlayıcıları sarmalar ve aktör durum yönetimi için bir bağdaştırıcı sağlar.

Bu bileşenleri birlikte form hello güvenilir aktör çerçevesi.

## <a name="service-layering"></a>Hizmet katmanlarını
Merhaba aktör hizmeti kendisini güvenilir bir hizmet olduğundan, tüm hello [uygulama modeli](service-fabric-application-model.md), yaşam döngüsü, [paketleme](service-fabric-package-apps.md), [dağıtım](service-fabric-deploy-remove-applications.md), yükseltme ve kavramlarını ölçeklendirme Güvenilir hizmetler uygulamak hello aynı şekilde tooactor Hizmetleri. 

![Aktör hizmeti katmanlama][1]

Merhaba önceki diyagramda hello hello Service Fabric uygulama çerçeveleri ve kullanıcı kodu arasındaki ilişkiyi gösterir. Mavi öğeleri hello Reliable Services uygulama çerçevesi temsil eder, turuncu hello güvenilir aktör framework ve yeşil kullanıcı kodu temsil eder.

Güvenilir Hizmetleri'nde hizmetinizi hello devralır `StatefulService` sınıfı. Bu sınıf kendisini türetilmiş, `StatefulServiceBase` (veya `StatelessService` durum bilgisi olmayan hizmetler için). Reliable Actors içinde hello aktör hizmeti kullanın. Merhaba aktör hizmetidir hello farklı bir uygulama `StatefulServiceBase` , aktörler çalıştırdığı bu Implements hello aktör düzeni sınıfı. Merhaba aktör hizmeti kendisi yalnızca uygulaması olduğundan `StatefulServiceBase`, türetilen kendi hizmet yazabilirsiniz `ActorService` ve uygulama servis düzeyi özellikleri aynı hello devralırken yaptığınız şekilde `StatefulService`, gibi:

* Hizmet yedekleme ve geri yükleme.
* İşlevselliği tüm aktörler, örneğin, bir devre kesici paylaşılan.
* Uzak yordam çağrıları hello aktör hizmetin kendisi ve tek tek her aktör.

> [!NOTE]
> Durum bilgisi olan hizmetler Java/Linux şu anda desteklenmemektedir.

### <a name="using-hello-actor-service"></a>Merhaba aktör hizmeti kullanma
Aktör örnekleri bunlar çalıştırdığınız erişim toohello aktör hizmeti vardır. Merhaba aktör hizmeti aracılığıyla aktör örnekleri program aracılığıyla hello Hizmet bağlamı elde edebilirsiniz. Merhaba Hizmet bağlamı hello bölüm kimliği, hizmet adı, uygulama adı ve diğer Service Fabric platforma özgü bilgileri vardır:

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


Bir hizmet türünün hello Service Fabric çalışma zamanında ile tüm güvenilir hizmetler gibi hello aktör hizmeti kayıtlı olması gerekir. Aktör örneklerinizi toorun Hello aktör hizmeti için aktör türünüz ayrıca hello aktör hizmetiyle kaydedilmesi gerekir. Merhaba `ActorRuntime` kayıt yöntemi, bu iş aktörleri gerçekleştirir. Merhaba en basit durumda, yalnızca aktör türünüz kaydedebilirsiniz ve varsayılan ayarlarla hello aktör hizmeti örtük olarak kullanılacak:

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

Alternatif olarak, kendiniz hello kayıt yöntemi tooconstruct hello aktör hizmeti tarafından sağlanan bir lambda kullanabilirsiniz. Merhaba aktör hizmetini yapılandırın ve açıkça bağımlılıkları tooyour aktör kurucusu aracılığıyla burada Ekle aktör örneklerinizi oluşturun:

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a>Aktör hizmeti yöntemleri
Aktör hizmeti uygulayan hello `IActorService` (C#) veya `ActorService` (Java) sırayla uygulayan `IService` (C#) veya `Service` (Java). Bu uzaktan yordam çağrısı hizmeti yöntemleri sağlayan Reliable Services remoting tarafından kullanılan hello arabirimidir. Hizmet remoting uzaktan çağrılabilir hizmet düzeyi yöntemleri içerir.

#### <a name="enumerating-actors"></a>Aktör numaralandırma
Merhaba aktör hizmeti bir istemcinin hello hizmetini barındıran hello aktörler hakkında tooenumerate meta veriler sağlar. Merhaba aktör hizmeti bölümlenmiş bir durum bilgisi olan hizmet olduğundan, numaralandırma bölüm başına gerçekleştirilir. Her bölüm birçok aktörler içerebileceğinden hello sabit disk belleğine alınmış sonuçlar kümesi olarak döndürülür. tüm sayfaları oku kadar üzerinden hello sayfaları döngüye. örnekte gösterildiği nasıl aşağıdaki hello toocreate aktör hizmetinin bir bölümdeki tüm etkin aktörler listesi:

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a>Aktör silme
Merhaba aktör hizmeti aktörler silmek için bir işlevi de sağlar:

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

Merhaba aktörler ve durumlarına silme hakkında daha fazla bilgi için bkz: [aktör yaşam döngüsü belgelerine](service-fabric-reliable-actors-lifecycle.md).

### <a name="custom-actor-service"></a>Özel aktör hizmeti
Merhaba aktör kayıt lambda kullanarak türetilen kendi özel aktör hizmeti kaydedebilirsiniz `ActorService` (C#) ve `FabricActorService` (Java). Bu özel aktör hizmeti, kendi hizmet düzeyi işlevselliği devralan bir hizmet sınıfı yazarak uygulayabileceğiniz `ActorService` (C#) veya `FabricActorService` (Java). Bir özel aktör hizmeti tüm hello aktör çalışma zamanı işlevsellik devralır `ActorService` (C#) veya `FabricActorService` (Java) ve kullanılan tooimplement kendi hizmet yöntemleri olabilir.

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a>Uygulama aktör yedekleme ve geri yükleme
 Aşağıdaki örneğine hello hello özel aktör hizmetini yöntemi tooback aktör verileri hello remoting dinleyici zaten mevcut yararlanarak gösteren `ActorService`:

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


Bu örnekte, `IMyActorService` uygulayan bir remoting sözleşme `IService` (C#) ve `Service` (Java) ve ardından tarafından uygulanan `MyActorService`. Üzerinde bu remoting sözleşme yöntemleri ekleyerek `IMyActorService` de kullanılabilir tooa istemci remoting proxy aracılığıyla oluşturarak sunulmuştur `ActorServiceProxy`:

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a>Uygulama modeli
Merhaba uygulama modeli olan hello şekilde aynı aktör Reliable Services hizmetleridir. Ancak, hello aktör framework derleme araçları hello uygulama modeli dosyaların bazıları sizin için oluşturur.

### <a name="service-manifest"></a>Hizmet bildirimi
Merhaba aktör framework derleme araçları aktör hizmetinizin ServiceManifest.xml dosyasının Merhaba içeriğine otomatik olarak oluşturur. Bu dosya içerir:

* Aktör hizmeti türü. Merhaba türü adı aktör'ın Proje adına göre oluşturulur. Merhaba Kalıcılık özniteliği, aktör bağlı olarak, hello HasPersistedState bayrağı da buna uygun olarak ayarlanır.
* Kod paketi.
* Yapılandırma paketi.
* Kaynaklar ve uç noktaları.

### <a name="application-manifest"></a>Uygulama bildirimi
Merhaba aktör framework derleme araçları varsayılan hizmet tanımı aktör hizmetiniz için otomatik olarak oluşturun. Merhaba derleme araçları hello varsayılan hizmet özelliklerini doldurun:

* Çoğaltma kümesi sayısı, aktör hello Kalıcılık özniteliği tarafından belirlenir. Her zaman hello Kalıcılık özniteliği, aktör değiştirildiğinde, hello çoğaltma kümesi sayısı hello varsayılan hizmet tanımında buna uygun olarak sıfırlanır.
* Bölüm düzeni ve aralığı tooUniform Int64 hello tam Int64 anahtar aralığı ile ayarlanır.

## <a name="service-fabric-partition-concepts-for-actors"></a>Aktörler için Service Fabric bölümü kavramlar
Aktör Hizmetleri bölümlenmiş durum bilgisi olan hizmetleridir. Aktör hizmeti her bölüm aktörler kümesini içerir. Hizmet bölümlerini Service Fabric birden çok düğümler üzerinden otomatik olarak dağıtılır. Aktör örnekleri sonuç olarak dağıtılır.

![Bölümleme aktör ve dağıtım][5]

Güvenilir hizmetler farklı bir bölüm düzeni ve bölüm anahtarı aralıkları ile oluşturulabilir. Merhaba aktör hizmeti hello tam Int64 anahtar aralığı toomap aktörler toopartitions ile Merhaba Int64 bölümleme düzenini kullanır.

### <a name="actor-id"></a>Aktör kimliği
Merhaba hizmetinde oluşturulan her aktör hello tarafından temsil edilen ilişkili benzersiz bir Kimliğe sahip `ActorId` sınıfı. `ActorId`rastgele kimlikleri oluşturarak hello hizmeti bölümleri arasında Tekdüzen aktörler dağıtım için kullanılabilecek bir donuk kimliği değeridir:

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


Her `ActorId` karma tooan Int64 değil. Merhaba aktör hizmeti bir Int64 bölümleme düzeni hello tam Int64 anahtar aralığı ile kullanmanız gerekir nedeni budur. Ancak, özel kimlik değerleri için kullanılabilecek bir `ActorID`GUID/UUID, dizeleri ve Int64s dahil olmak üzere.

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

GUID/UUID ve dizeleri kullanırken hello karma tooan Int64 değerlerdir. Ancak, ne zaman, açıkça sağlayan bir Int64 tooan `ActorId`, hello Int64 eşleme doğrudan tooa bölüm daha fazla karma olmadan. Bölüm hello aktörler yerleştirildiği Bu teknik toocontrol kullanabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* [Aktör durum yönetimi](service-fabric-reliable-actors-state-management.md)
* [Aktör yaşam döngüsü ve çöp toplama](service-fabric-reliable-actors-lifecycle.md)
* [Aktör API başvuru belgeleri](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [.NET örnek kod](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Java örnek kod](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
