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
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a><span data-ttu-id="4baaf-103">Reliable Actors hello Service Fabric platformundan kullanma</span><span class="sxs-lookup"><span data-stu-id="4baaf-103">How Reliable Actors use hello Service Fabric platform</span></span>
<span data-ttu-id="4baaf-104">Bu makalede, Reliable Actors hello Azure Service Fabric platformda nasıl çalıştığı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4baaf-104">This article explains how Reliable Actors work on hello Azure Service Fabric platform.</span></span> <span data-ttu-id="4baaf-105">Güvenilir aktörler Çalıştır hello olarak adlandırılan bir durum bilgisi olan güvenilir hizmet uygulaması içinde barındırılan bir çerçeve *aktör hizmeti*.</span><span class="sxs-lookup"><span data-stu-id="4baaf-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called hello *actor service*.</span></span> <span data-ttu-id="4baaf-106">Merhaba aktör hizmeti tüm hello bileşenleri gerekli toomanage hello yaşam döngüsü ve ileti, aktörleri göndermeyi içerir:</span><span class="sxs-lookup"><span data-stu-id="4baaf-106">hello actor service contains all hello components necessary toomanage hello lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="4baaf-107">Merhaba aktör çalışma zamanı yaşam döngüsü, atık toplama yönetir ve tek iş parçacıklı erişimini zorunlu kılar.</span><span class="sxs-lookup"><span data-stu-id="4baaf-107">hello Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="4baaf-108">Aktör hizmeti remoting dinleyicisi uzaktan erişim çağrıları tooactors kabul eder ve bunları tooa dağıtıcısı tooroute toohello uygun aktör örneği gönderir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-108">An actor service remoting listener accepts remote access calls tooactors and sends them tooa dispatcher tooroute toohello appropriate actor instance.</span></span>
* <span data-ttu-id="4baaf-109">Merhaba aktör durumu sağlayıcısı (gibi hello güvenilir koleksiyonları durumu sağlayıcısı) durumu sağlayıcıları sarmalar ve aktör durum yönetimi için bir bağdaştırıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="4baaf-109">hello Actor State Provider wraps state providers (such as hello Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="4baaf-110">Bu bileşenleri birlikte form hello güvenilir aktör çerçevesi.</span><span class="sxs-lookup"><span data-stu-id="4baaf-110">These components together form hello Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="4baaf-111">Hizmet katmanlarını</span><span class="sxs-lookup"><span data-stu-id="4baaf-111">Service layering</span></span>
<span data-ttu-id="4baaf-112">Merhaba aktör hizmeti kendisini güvenilir bir hizmet olduğundan, tüm hello [uygulama modeli](service-fabric-application-model.md), yaşam döngüsü, [paketleme](service-fabric-package-apps.md), [dağıtım](service-fabric-deploy-remove-applications.md), yükseltme ve kavramlarını ölçeklendirme Güvenilir hizmetler uygulamak hello aynı şekilde tooactor Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="4baaf-112">Because hello actor service itself is a reliable service, all hello [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply hello same way tooactor services.</span></span> 

![Aktör hizmeti katmanlama][1]

<span data-ttu-id="4baaf-114">Merhaba önceki diyagramda hello hello Service Fabric uygulama çerçeveleri ve kullanıcı kodu arasındaki ilişkiyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-114">hello preceding diagram shows hello relationship between hello Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="4baaf-115">Mavi öğeleri hello Reliable Services uygulama çerçevesi temsil eder, turuncu hello güvenilir aktör framework ve yeşil kullanıcı kodu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="4baaf-115">Blue elements represent hello Reliable Services application framework, orange represents hello Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="4baaf-116">Güvenilir Hizmetleri'nde hizmetinizi hello devralır `StatefulService` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4baaf-116">In Reliable Services, your service inherits hello `StatefulService` class.</span></span> <span data-ttu-id="4baaf-117">Bu sınıf kendisini türetilmiş, `StatefulServiceBase` (veya `StatelessService` durum bilgisi olmayan hizmetler için).</span><span class="sxs-lookup"><span data-stu-id="4baaf-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="4baaf-118">Reliable Actors içinde hello aktör hizmeti kullanın.</span><span class="sxs-lookup"><span data-stu-id="4baaf-118">In Reliable Actors, you use hello actor service.</span></span> <span data-ttu-id="4baaf-119">Merhaba aktör hizmetidir hello farklı bir uygulama `StatefulServiceBase` , aktörler çalıştırdığı bu Implements hello aktör düzeni sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4baaf-119">hello actor service is a different implementation of hello `StatefulServiceBase` class that implements hello actor pattern where your actors run.</span></span> <span data-ttu-id="4baaf-120">Merhaba aktör hizmeti kendisi yalnızca uygulaması olduğundan `StatefulServiceBase`, türetilen kendi hizmet yazabilirsiniz `ActorService` ve uygulama servis düzeyi özellikleri aynı hello devralırken yaptığınız şekilde `StatefulService`, gibi:</span><span class="sxs-lookup"><span data-stu-id="4baaf-120">Because hello actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features hello same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="4baaf-121">Hizmet yedekleme ve geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="4baaf-121">Service backup and restore.</span></span>
* <span data-ttu-id="4baaf-122">İşlevselliği tüm aktörler, örneğin, bir devre kesici paylaşılan.</span><span class="sxs-lookup"><span data-stu-id="4baaf-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="4baaf-123">Uzak yordam çağrıları hello aktör hizmetin kendisi ve tek tek her aktör.</span><span class="sxs-lookup"><span data-stu-id="4baaf-123">Remote procedure calls on hello actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="4baaf-124">Durum bilgisi olan hizmetler Java/Linux şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-hello-actor-service"></a><span data-ttu-id="4baaf-125">Merhaba aktör hizmeti kullanma</span><span class="sxs-lookup"><span data-stu-id="4baaf-125">Using hello actor service</span></span>
<span data-ttu-id="4baaf-126">Aktör örnekleri bunlar çalıştırdığınız erişim toohello aktör hizmeti vardır.</span><span class="sxs-lookup"><span data-stu-id="4baaf-126">Actor instances have access toohello actor service in which they are running.</span></span> <span data-ttu-id="4baaf-127">Merhaba aktör hizmeti aracılığıyla aktör örnekleri program aracılığıyla hello Hizmet bağlamı elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4baaf-127">Through hello actor service, actor instances can programmatically obtain hello service context.</span></span> <span data-ttu-id="4baaf-128">Merhaba Hizmet bağlamı hello bölüm kimliği, hizmet adı, uygulama adı ve diğer Service Fabric platforma özgü bilgileri vardır:</span><span class="sxs-lookup"><span data-stu-id="4baaf-128">hello service context has hello partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

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


<span data-ttu-id="4baaf-129">Bir hizmet türünün hello Service Fabric çalışma zamanında ile tüm güvenilir hizmetler gibi hello aktör hizmeti kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-129">Like all Reliable Services, hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="4baaf-130">Aktör örneklerinizi toorun Hello aktör hizmeti için aktör türünüz ayrıca hello aktör hizmetiyle kaydedilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-130">For hello actor service toorun your actor instances, your actor type must also be registered with hello actor service.</span></span> <span data-ttu-id="4baaf-131">Merhaba `ActorRuntime` kayıt yöntemi, bu iş aktörleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-131">hello `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="4baaf-132">Merhaba en basit durumda, yalnızca aktör türünüz kaydedebilirsiniz ve varsayılan ayarlarla hello aktör hizmeti örtük olarak kullanılacak:</span><span class="sxs-lookup"><span data-stu-id="4baaf-132">In hello simplest case, you can just register your actor type, and hello actor service with default settings will implicitly be used:</span></span>

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

<span data-ttu-id="4baaf-133">Alternatif olarak, kendiniz hello kayıt yöntemi tooconstruct hello aktör hizmeti tarafından sağlanan bir lambda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4baaf-133">Alternatively, you can use a lambda provided by hello registration method tooconstruct hello actor service yourself.</span></span> <span data-ttu-id="4baaf-134">Merhaba aktör hizmetini yapılandırın ve açıkça bağımlılıkları tooyour aktör kurucusu aracılığıyla burada Ekle aktör örneklerinizi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4baaf-134">You can then configure hello actor service and explicitly construct your actor instances, where you can inject dependencies tooyour actor through its constructor:</span></span>

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

### <a name="actor-service-methods"></a><span data-ttu-id="4baaf-135">Aktör hizmeti yöntemleri</span><span class="sxs-lookup"><span data-stu-id="4baaf-135">Actor service methods</span></span>
<span data-ttu-id="4baaf-136">Aktör hizmeti uygulayan hello `IActorService` (C#) veya `ActorService` (Java) sırayla uygulayan `IService` (C#) veya `Service` (Java).</span><span class="sxs-lookup"><span data-stu-id="4baaf-136">hello Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="4baaf-137">Bu uzaktan yordam çağrısı hizmeti yöntemleri sağlayan Reliable Services remoting tarafından kullanılan hello arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-137">This is hello interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="4baaf-138">Hizmet remoting uzaktan çağrılabilir hizmet düzeyi yöntemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="4baaf-139">Aktör numaralandırma</span><span class="sxs-lookup"><span data-stu-id="4baaf-139">Enumerating actors</span></span>
<span data-ttu-id="4baaf-140">Merhaba aktör hizmeti bir istemcinin hello hizmetini barındıran hello aktörler hakkında tooenumerate meta veriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="4baaf-140">hello actor service allows a client tooenumerate metadata about hello actors that hello service is hosting.</span></span> <span data-ttu-id="4baaf-141">Merhaba aktör hizmeti bölümlenmiş bir durum bilgisi olan hizmet olduğundan, numaralandırma bölüm başına gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-141">Because hello actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="4baaf-142">Her bölüm birçok aktörler içerebileceğinden hello sabit disk belleğine alınmış sonuçlar kümesi olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="4baaf-142">Because each partition might contain many actors, hello enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="4baaf-143">tüm sayfaları oku kadar üzerinden hello sayfaları döngüye.</span><span class="sxs-lookup"><span data-stu-id="4baaf-143">hello pages are looped over until all pages are read.</span></span> <span data-ttu-id="4baaf-144">örnekte gösterildiği nasıl aşağıdaki hello toocreate aktör hizmetinin bir bölümdeki tüm etkin aktörler listesi:</span><span class="sxs-lookup"><span data-stu-id="4baaf-144">hello following example shows how toocreate a list of all active actors in one partition of an actor service:</span></span>

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

#### <a name="deleting-actors"></a><span data-ttu-id="4baaf-145">Aktör silme</span><span class="sxs-lookup"><span data-stu-id="4baaf-145">Deleting actors</span></span>
<span data-ttu-id="4baaf-146">Merhaba aktör hizmeti aktörler silmek için bir işlevi de sağlar:</span><span class="sxs-lookup"><span data-stu-id="4baaf-146">hello actor service also provides a function for deleting actors:</span></span>

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

<span data-ttu-id="4baaf-147">Merhaba aktörler ve durumlarına silme hakkında daha fazla bilgi için bkz: [aktör yaşam döngüsü belgelerine](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="4baaf-147">For more information on deleting actors and their state, see hello [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="4baaf-148">Özel aktör hizmeti</span><span class="sxs-lookup"><span data-stu-id="4baaf-148">Custom actor service</span></span>
<span data-ttu-id="4baaf-149">Merhaba aktör kayıt lambda kullanarak türetilen kendi özel aktör hizmeti kaydedebilirsiniz `ActorService` (C#) ve `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="4baaf-149">By using hello actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="4baaf-150">Bu özel aktör hizmeti, kendi hizmet düzeyi işlevselliği devralan bir hizmet sınıfı yazarak uygulayabileceğiniz `ActorService` (C#) veya `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="4baaf-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="4baaf-151">Bir özel aktör hizmeti tüm hello aktör çalışma zamanı işlevsellik devralır `ActorService` (C#) veya `FabricActorService` (Java) ve kullanılan tooimplement kendi hizmet yöntemleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-151">A custom actor service inherits all hello actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used tooimplement your own service methods.</span></span>

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

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="4baaf-152">Uygulama aktör yedekleme ve geri yükleme</span><span class="sxs-lookup"><span data-stu-id="4baaf-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="4baaf-153">Aşağıdaki örneğine hello hello özel aktör hizmetini yöntemi tooback aktör verileri hello remoting dinleyici zaten mevcut yararlanarak gösteren `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="4baaf-153">In hello following example, hello custom actor service exposes a method tooback up actor data by taking advantage of hello remoting listener already present in `ActorService`:</span></span>

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


<span data-ttu-id="4baaf-154">Bu örnekte, `IMyActorService` uygulayan bir remoting sözleşme `IService` (C#) ve `Service` (Java) ve ardından tarafından uygulanan `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="4baaf-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="4baaf-155">Üzerinde bu remoting sözleşme yöntemleri ekleyerek `IMyActorService` de kullanılabilir tooa istemci remoting proxy aracılığıyla oluşturarak sunulmuştur `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="4baaf-155">By adding this remoting contract, methods on `IMyActorService` are now also available tooa client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

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

## <a name="application-model"></a><span data-ttu-id="4baaf-156">Uygulama modeli</span><span class="sxs-lookup"><span data-stu-id="4baaf-156">Application model</span></span>
<span data-ttu-id="4baaf-157">Merhaba uygulama modeli olan hello şekilde aynı aktör Reliable Services hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-157">Actor services are Reliable Services, so hello application model is hello same.</span></span> <span data-ttu-id="4baaf-158">Ancak, hello aktör framework derleme araçları hello uygulama modeli dosyaların bazıları sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4baaf-158">However, hello actor framework build tools generate some of hello application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="4baaf-159">Hizmet bildirimi</span><span class="sxs-lookup"><span data-stu-id="4baaf-159">Service manifest</span></span>
<span data-ttu-id="4baaf-160">Merhaba aktör framework derleme araçları aktör hizmetinizin ServiceManifest.xml dosyasının Merhaba içeriğine otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4baaf-160">hello actor framework build tools automatically generate hello contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="4baaf-161">Bu dosya içerir:</span><span class="sxs-lookup"><span data-stu-id="4baaf-161">This file includes:</span></span>

* <span data-ttu-id="4baaf-162">Aktör hizmeti türü.</span><span class="sxs-lookup"><span data-stu-id="4baaf-162">Actor service type.</span></span> <span data-ttu-id="4baaf-163">Merhaba türü adı aktör'ın Proje adına göre oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4baaf-163">hello type name is generated based on your actor's project name.</span></span> <span data-ttu-id="4baaf-164">Merhaba Kalıcılık özniteliği, aktör bağlı olarak, hello HasPersistedState bayrağı da buna uygun olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="4baaf-164">Based on hello persistence attribute on your actor, hello HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="4baaf-165">Kod paketi.</span><span class="sxs-lookup"><span data-stu-id="4baaf-165">Code package.</span></span>
* <span data-ttu-id="4baaf-166">Yapılandırma paketi.</span><span class="sxs-lookup"><span data-stu-id="4baaf-166">Config package.</span></span>
* <span data-ttu-id="4baaf-167">Kaynaklar ve uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="4baaf-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="4baaf-168">Uygulama bildirimi</span><span class="sxs-lookup"><span data-stu-id="4baaf-168">Application manifest</span></span>
<span data-ttu-id="4baaf-169">Merhaba aktör framework derleme araçları varsayılan hizmet tanımı aktör hizmetiniz için otomatik olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4baaf-169">hello actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="4baaf-170">Merhaba derleme araçları hello varsayılan hizmet özelliklerini doldurun:</span><span class="sxs-lookup"><span data-stu-id="4baaf-170">hello build tools populate hello default service properties:</span></span>

* <span data-ttu-id="4baaf-171">Çoğaltma kümesi sayısı, aktör hello Kalıcılık özniteliği tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-171">Replica set count is determined by hello persistence attribute on your actor.</span></span> <span data-ttu-id="4baaf-172">Her zaman hello Kalıcılık özniteliği, aktör değiştirildiğinde, hello çoğaltma kümesi sayısı hello varsayılan hizmet tanımında buna uygun olarak sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="4baaf-172">Each time hello persistence attribute on your actor is changed, hello replica set count in hello default service definition is reset accordingly.</span></span>
* <span data-ttu-id="4baaf-173">Bölüm düzeni ve aralığı tooUniform Int64 hello tam Int64 anahtar aralığı ile ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="4baaf-173">Partition scheme and range are set tooUniform Int64 with hello full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="4baaf-174">Aktörler için Service Fabric bölümü kavramlar</span><span class="sxs-lookup"><span data-stu-id="4baaf-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="4baaf-175">Aktör Hizmetleri bölümlenmiş durum bilgisi olan hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="4baaf-176">Aktör hizmeti her bölüm aktörler kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="4baaf-177">Hizmet bölümlerini Service Fabric birden çok düğümler üzerinden otomatik olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="4baaf-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="4baaf-178">Aktör örnekleri sonuç olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="4baaf-178">Actor instances are distributed as a result.</span></span>

![Bölümleme aktör ve dağıtım][5]

<span data-ttu-id="4baaf-180">Güvenilir hizmetler farklı bir bölüm düzeni ve bölüm anahtarı aralıkları ile oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="4baaf-181">Merhaba aktör hizmeti hello tam Int64 anahtar aralığı toomap aktörler toopartitions ile Merhaba Int64 bölümleme düzenini kullanır.</span><span class="sxs-lookup"><span data-stu-id="4baaf-181">hello actor service uses hello Int64 partitioning scheme with hello full Int64 key range toomap actors toopartitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="4baaf-182">Aktör kimliği</span><span class="sxs-lookup"><span data-stu-id="4baaf-182">Actor ID</span></span>
<span data-ttu-id="4baaf-183">Merhaba hizmetinde oluşturulan her aktör hello tarafından temsil edilen ilişkili benzersiz bir Kimliğe sahip `ActorId` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4baaf-183">Each actor that's created in hello service has a unique ID associated with it, represented by hello `ActorId` class.</span></span> <span data-ttu-id="4baaf-184">`ActorId`rastgele kimlikleri oluşturarak hello hizmeti bölümleri arasında Tekdüzen aktörler dağıtım için kullanılabilecek bir donuk kimliği değeridir:</span><span class="sxs-lookup"><span data-stu-id="4baaf-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across hello service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="4baaf-185">Her `ActorId` karma tooan Int64 değil.</span><span class="sxs-lookup"><span data-stu-id="4baaf-185">Every `ActorId` is hashed tooan Int64.</span></span> <span data-ttu-id="4baaf-186">Merhaba aktör hizmeti bir Int64 bölümleme düzeni hello tam Int64 anahtar aralığı ile kullanmanız gerekir nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="4baaf-186">This is why hello actor service must use an Int64 partitioning scheme with hello full Int64 key range.</span></span> <span data-ttu-id="4baaf-187">Ancak, özel kimlik değerleri için kullanılabilecek bir `ActorID`GUID/UUID, dizeleri ve Int64s dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="4baaf-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

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

<span data-ttu-id="4baaf-188">GUID/UUID ve dizeleri kullanırken hello karma tooan Int64 değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="4baaf-188">When you're using GUIDs/UUIDs and strings, hello values are hashed tooan Int64.</span></span> <span data-ttu-id="4baaf-189">Ancak, ne zaman, açıkça sağlayan bir Int64 tooan `ActorId`, hello Int64 eşleme doğrudan tooa bölüm daha fazla karma olmadan.</span><span class="sxs-lookup"><span data-stu-id="4baaf-189">However, when you're explicitly providing an Int64 tooan `ActorId`, hello Int64 will map directly tooa partition without further hashing.</span></span> <span data-ttu-id="4baaf-190">Bölüm hello aktörler yerleştirildiği Bu teknik toocontrol kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4baaf-190">You can use this technique toocontrol which partition hello actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4baaf-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4baaf-191">Next steps</span></span>
* [<span data-ttu-id="4baaf-192">Aktör durum yönetimi</span><span class="sxs-lookup"><span data-stu-id="4baaf-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="4baaf-193">Aktör yaşam döngüsü ve çöp toplama</span><span class="sxs-lookup"><span data-stu-id="4baaf-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="4baaf-194">Aktör API başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="4baaf-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="4baaf-195">.NET örnek kod</span><span class="sxs-lookup"><span data-stu-id="4baaf-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="4baaf-196">Java örnek kod</span><span class="sxs-lookup"><span data-stu-id="4baaf-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
