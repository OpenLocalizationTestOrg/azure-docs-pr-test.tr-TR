---
title: "Service Fabric üzerinde Reliable Actors | Microsoft Docs"
description: "Reliable Actors Reliable Services üzerinde katmanlanmış ve Service Fabric platformundan özellikleriyle nasıl açıklanmaktadır."
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
ms.openlocfilehash: 0a12da52b6e74c721cd25f89e7cde3c07153a396
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-reliable-actors-use-the-service-fabric-platform"></a><span data-ttu-id="851c2-103">Reliable Actors hizmeti tarafından Service Fabric platformunun kullanımı</span><span class="sxs-lookup"><span data-stu-id="851c2-103">How Reliable Actors use the Service Fabric platform</span></span>
<span data-ttu-id="851c2-104">Bu makalede, Azure Service Fabric platformda Reliable Actors nasıl çalıştığı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="851c2-104">This article explains how Reliable Actors work on the Azure Service Fabric platform.</span></span> <span data-ttu-id="851c2-105">Durum bilgisi olan güvenilir bir hizmet uygulaması içinde barındırılan bir çerçeve çalıştırmanız reliable Actors adlı *aktör hizmeti*.</span><span class="sxs-lookup"><span data-stu-id="851c2-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called the *actor service*.</span></span> <span data-ttu-id="851c2-106">Aktör hizmeti yaşam döngüsü ve ileti gönderme, aktörleri yönetmek gerekli tüm bileşenleri içerir:</span><span class="sxs-lookup"><span data-stu-id="851c2-106">The actor service contains all the components necessary to manage the lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="851c2-107">Aktör çalışma zamanı yaşam döngüsü, atık toplama yönetir ve tek iş parçacıklı erişimini zorunlu kılar.</span><span class="sxs-lookup"><span data-stu-id="851c2-107">The Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="851c2-108">Aktör hizmeti remoting dinleyicisi aktörler için uzaktan erişim çağrılarını kabul eder ve bunları uygun aktör örneğine yönlendirmek için bir dağıtıcı gönderir.</span><span class="sxs-lookup"><span data-stu-id="851c2-108">An actor service remoting listener accepts remote access calls to actors and sends them to a dispatcher to route to the appropriate actor instance.</span></span>
* <span data-ttu-id="851c2-109">Aktör durumu sağlayıcısı (örneğin, güvenilir koleksiyonları durumu sağlayıcısı) durum sağlayıcılarının sarmalar ve aktör durum yönetimi için bir bağdaştırıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="851c2-109">The Actor State Provider wraps state providers (such as the Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="851c2-110">Bu bileşenlerin birlikte güvenilir aktör framework oluştururlar.</span><span class="sxs-lookup"><span data-stu-id="851c2-110">These components together form the Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="851c2-111">Hizmet katmanlarını</span><span class="sxs-lookup"><span data-stu-id="851c2-111">Service layering</span></span>
<span data-ttu-id="851c2-112">Aktör hizmeti güvenilir bir hizmet olduğundan tüm [uygulama modeli](service-fabric-application-model.md), yaşam döngüsü, [paketleme](service-fabric-package-apps.md), [dağıtım](service-fabric-deploy-remove-applications.md), yükseltme ve ölçeklendirme Reliable Services kavramlarını aktör Hizmetleri aynı şekilde geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="851c2-112">Because the actor service itself is a reliable service, all the [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply the same way to actor services.</span></span> 

![Aktör hizmeti katmanlama][1]

<span data-ttu-id="851c2-114">Önceki diyagramda Service Fabric uygulama çerçeveleri ve kullanıcı kodu arasındaki ilişkiyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="851c2-114">The preceding diagram shows the relationship between the Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="851c2-115">Mavi öğeleri Reliable Services uygulama çerçevesi temsil eder, turuncu güvenilir aktör framework ve yeşil kullanıcı kodu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="851c2-115">Blue elements represent the Reliable Services application framework, orange represents the Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="851c2-116">Güvenilir Hizmetleri'nde hizmetinizi devralır `StatefulService` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="851c2-116">In Reliable Services, your service inherits the `StatefulService` class.</span></span> <span data-ttu-id="851c2-117">Bu sınıf kendisini türetilmiş, `StatefulServiceBase` (veya `StatelessService` durum bilgisi olmayan hizmetler için).</span><span class="sxs-lookup"><span data-stu-id="851c2-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="851c2-118">Reliable Actors içinde aktör hizmeti kullanın.</span><span class="sxs-lookup"><span data-stu-id="851c2-118">In Reliable Actors, you use the actor service.</span></span> <span data-ttu-id="851c2-119">Aktör hizmeti farklı bir uygulamasıdır `StatefulServiceBase` , aktörler çalıştırdığı aktör deseni uygulayan sınıf.</span><span class="sxs-lookup"><span data-stu-id="851c2-119">The actor service is a different implementation of the `StatefulServiceBase` class that implements the actor pattern where your actors run.</span></span> <span data-ttu-id="851c2-120">Aktör hizmeti uygulaması yalnızca olduğundan `StatefulServiceBase`, türetilen kendi hizmet yazabilirsiniz `ActorService` ve hizmet düzeyi özellikleri devralırken yaptığınız şekilde uygulamak `StatefulService`, gibi:</span><span class="sxs-lookup"><span data-stu-id="851c2-120">Because the actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features the same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="851c2-121">Hizmet yedekleme ve geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="851c2-121">Service backup and restore.</span></span>
* <span data-ttu-id="851c2-122">İşlevselliği tüm aktörler, örneğin, bir devre kesici paylaşılan.</span><span class="sxs-lookup"><span data-stu-id="851c2-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="851c2-123">Aktör hizmeti ve tek tek her aktör uzak yordam çağrıları.</span><span class="sxs-lookup"><span data-stu-id="851c2-123">Remote procedure calls on the actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="851c2-124">Durum bilgisi olan hizmetler Java/Linux şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="851c2-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-the-actor-service"></a><span data-ttu-id="851c2-125">Aktör hizmeti kullanma</span><span class="sxs-lookup"><span data-stu-id="851c2-125">Using the actor service</span></span>
<span data-ttu-id="851c2-126">Aktör örnekleri bunlar çalıştırdığınız aktör hizmetine erişimi vardır.</span><span class="sxs-lookup"><span data-stu-id="851c2-126">Actor instances have access to the actor service in which they are running.</span></span> <span data-ttu-id="851c2-127">Aktör hizmeti aracılığıyla aktör örnekleri program aracılığıyla hizmet bağlamı elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="851c2-127">Through the actor service, actor instances can programmatically obtain the service context.</span></span> <span data-ttu-id="851c2-128">Hizmet bağlamı, bölüm kimliği, hizmet adı, uygulama adı ve diğer Service Fabric platforma özgü bilgileri vardır:</span><span class="sxs-lookup"><span data-stu-id="851c2-128">The service context has the partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

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


<span data-ttu-id="851c2-129">Service Fabric çalışma zamanında bir hizmet türü ile tüm güvenilir hizmetler gibi aktör hizmeti kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="851c2-129">Like all Reliable Services, the actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="851c2-130">Aktör hizmeti aktör örneklerinizi çalıştırmak aktör türünüz aktör hizmeti ile kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="851c2-130">For the actor service to run your actor instances, your actor type must also be registered with the actor service.</span></span> <span data-ttu-id="851c2-131">`ActorRuntime` Kayıt yöntemi, bu iş aktörleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="851c2-131">The `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="851c2-132">En basit durumda, yalnızca aktör türünüz kaydedebilirsiniz ve varsayılan ayarlarla aktör hizmeti örtük olarak kullanılacak:</span><span class="sxs-lookup"><span data-stu-id="851c2-132">In the simplest case, you can just register your actor type, and the actor service with default settings will implicitly be used:</span></span>

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

<span data-ttu-id="851c2-133">Alternatif olarak, kayıt yöntemi tarafından sağlanan bir lambda aktör hizmeti kendiniz oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="851c2-133">Alternatively, you can use a lambda provided by the registration method to construct the actor service yourself.</span></span> <span data-ttu-id="851c2-134">Aktör hizmeti yapılandırmak ve burada kurucusu aracılığıyla, aktör bağımlılıkları ekleyemezsiniz aktör örneklerinizi açıkça oluşturun:</span><span class="sxs-lookup"><span data-stu-id="851c2-134">You can then configure the actor service and explicitly construct your actor instances, where you can inject dependencies to your actor through its constructor:</span></span>

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

### <a name="actor-service-methods"></a><span data-ttu-id="851c2-135">Aktör hizmeti yöntemleri</span><span class="sxs-lookup"><span data-stu-id="851c2-135">Actor service methods</span></span>
<span data-ttu-id="851c2-136">Aktör hizmeti uygulayan `IActorService` (C#) veya `ActorService` (Java) sırayla uygulayan `IService` (C#) veya `Service` (Java).</span><span class="sxs-lookup"><span data-stu-id="851c2-136">The Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="851c2-137">Bu uzaktan yordam çağrısı hizmeti yöntemleri sağlayan Reliable Services remoting tarafından kullanılan arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="851c2-137">This is the interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="851c2-138">Hizmet remoting uzaktan çağrılabilir hizmet düzeyi yöntemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="851c2-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="851c2-139">Aktör numaralandırma</span><span class="sxs-lookup"><span data-stu-id="851c2-139">Enumerating actors</span></span>
<span data-ttu-id="851c2-140">Aktör hizmeti meta veri hizmeti barındırma aktörler hakkında numaralandırılamadı bir istemcinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="851c2-140">The actor service allows a client to enumerate metadata about the actors that the service is hosting.</span></span> <span data-ttu-id="851c2-141">Aktör hizmeti bölümlenmiş bir durum bilgisi olan hizmet olduğundan, numaralandırma bölüm başına gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="851c2-141">Because the actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="851c2-142">Her bölüm birçok aktörler içerebileceğinden sabit disk belleğine alınmış sonuçlar kümesi olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="851c2-142">Because each partition might contain many actors, the enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="851c2-143">Tüm sayfaları oku kadar üzerinden sayfaları döngüye.</span><span class="sxs-lookup"><span data-stu-id="851c2-143">The pages are looped over until all pages are read.</span></span> <span data-ttu-id="851c2-144">Aşağıdaki örnekte bir aktör hizmeti bir bölümünü tüm etkin aktörler listesini oluşturulacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="851c2-144">The following example shows how to create a list of all active actors in one partition of an actor service:</span></span>

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

#### <a name="deleting-actors"></a><span data-ttu-id="851c2-145">Aktör silme</span><span class="sxs-lookup"><span data-stu-id="851c2-145">Deleting actors</span></span>
<span data-ttu-id="851c2-146">Aktör hizmeti aktörler silmek için bir işlevi de sağlar:</span><span class="sxs-lookup"><span data-stu-id="851c2-146">The actor service also provides a function for deleting actors:</span></span>

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

<span data-ttu-id="851c2-147">Aktörlerin ve durumlarına silme hakkında daha fazla bilgi için bkz: [aktör yaşam döngüsü belgelerine](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="851c2-147">For more information on deleting actors and their state, see the [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="851c2-148">Özel aktör hizmeti</span><span class="sxs-lookup"><span data-stu-id="851c2-148">Custom actor service</span></span>
<span data-ttu-id="851c2-149">Aktör kayıt lambda kullanarak türetilen kendi özel aktör hizmeti kaydedebilirsiniz `ActorService` (C#) ve `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="851c2-149">By using the actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="851c2-150">Bu özel aktör hizmeti, kendi hizmet düzeyi işlevselliği devralan bir hizmet sınıfı yazarak uygulayabileceğiniz `ActorService` (C#) veya `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="851c2-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="851c2-151">Bir özel aktör hizmeti tüm aktör çalışma zamanı işlevsellik devralır `ActorService` (C#) veya `FabricActorService` (Java) ve kendi hizmet yöntemleri uygulamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="851c2-151">A custom actor service inherits all the actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used to implement your own service methods.</span></span>

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

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="851c2-152">Uygulama aktör yedekleme ve geri yükleme</span><span class="sxs-lookup"><span data-stu-id="851c2-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="851c2-153">Aşağıdaki örnekte, özel aktör hizmeti zaten mevcut remoting dinleyicisi yararlanarak aktör verileri yedeklemek için bir yöntem sunar. `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="851c2-153">In the following example, the custom actor service exposes a method to back up actor data by taking advantage of the remoting listener already present in `ActorService`:</span></span>

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
           // store the contents of backupInfo.Directory
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
           // store the contents of backupInfo.Directory
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


<span data-ttu-id="851c2-154">Bu örnekte, `IMyActorService` uygulayan bir remoting sözleşme `IService` (C#) ve `Service` (Java) ve ardından tarafından uygulanan `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="851c2-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="851c2-155">Üzerinde bu remoting sözleşme yöntemleri ekleyerek `IMyActorService` şimdi de remoting proxy aracılığıyla oluşturarak istemciye kullanılabilir `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="851c2-155">By adding this remoting contract, methods on `IMyActorService` are now also available to a client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

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

## <a name="application-model"></a><span data-ttu-id="851c2-156">Uygulama modeli</span><span class="sxs-lookup"><span data-stu-id="851c2-156">Application model</span></span>
<span data-ttu-id="851c2-157">Uygulama modeli aynı olacak şekilde aktör Reliable Services hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="851c2-157">Actor services are Reliable Services, so the application model is the same.</span></span> <span data-ttu-id="851c2-158">Ancak, aktör framework derleme araçları uygulama modeli dosyaların bazıları sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="851c2-158">However, the actor framework build tools generate some of the application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="851c2-159">Hizmet bildirimi</span><span class="sxs-lookup"><span data-stu-id="851c2-159">Service manifest</span></span>
<span data-ttu-id="851c2-160">Aktör framework derleme araçları aktör hizmetinizin ServiceManifest.xml dosyasının içeriği otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="851c2-160">The actor framework build tools automatically generate the contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="851c2-161">Bu dosya içerir:</span><span class="sxs-lookup"><span data-stu-id="851c2-161">This file includes:</span></span>

* <span data-ttu-id="851c2-162">Aktör hizmeti türü.</span><span class="sxs-lookup"><span data-stu-id="851c2-162">Actor service type.</span></span> <span data-ttu-id="851c2-163">Tür adı aktör'ın Proje adına göre oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="851c2-163">The type name is generated based on your actor's project name.</span></span> <span data-ttu-id="851c2-164">Aktör Kalıcılık öznitelikte bağlı olarak, HasPersistedState bayrağı da buna uygun olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="851c2-164">Based on the persistence attribute on your actor, the HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="851c2-165">Kod paketi.</span><span class="sxs-lookup"><span data-stu-id="851c2-165">Code package.</span></span>
* <span data-ttu-id="851c2-166">Yapılandırma paketi.</span><span class="sxs-lookup"><span data-stu-id="851c2-166">Config package.</span></span>
* <span data-ttu-id="851c2-167">Kaynaklar ve uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="851c2-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="851c2-168">Uygulama bildirimi</span><span class="sxs-lookup"><span data-stu-id="851c2-168">Application manifest</span></span>
<span data-ttu-id="851c2-169">Aktör framework derleme araçları varsayılan hizmet tanımı aktör hizmetiniz için otomatik olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="851c2-169">The actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="851c2-170">Derleme araçları varsayılan hizmet özelliklerini doldurun:</span><span class="sxs-lookup"><span data-stu-id="851c2-170">The build tools populate the default service properties:</span></span>

* <span data-ttu-id="851c2-171">Çoğaltma kümesi sayısı, aktör Kalıcılık özniteliği tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="851c2-171">Replica set count is determined by the persistence attribute on your actor.</span></span> <span data-ttu-id="851c2-172">Aktör Kalıcılık öznitelikte her değiştiğinde çoğaltma kümesi sayısı varsayılan hizmet tanımında buna uygun olarak sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="851c2-172">Each time the persistence attribute on your actor is changed, the replica set count in the default service definition is reset accordingly.</span></span>
* <span data-ttu-id="851c2-173">Bölüm düzeni ve aralığı Tekdüzen Int64 tam Int64 anahtar aralığıyla ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="851c2-173">Partition scheme and range are set to Uniform Int64 with the full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="851c2-174">Aktörler için Service Fabric bölümü kavramlar</span><span class="sxs-lookup"><span data-stu-id="851c2-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="851c2-175">Aktör Hizmetleri bölümlenmiş durum bilgisi olan hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="851c2-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="851c2-176">Aktör hizmeti her bölüm aktörler kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="851c2-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="851c2-177">Hizmet bölümlerini Service Fabric birden çok düğümler üzerinden otomatik olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="851c2-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="851c2-178">Aktör örnekleri sonuç olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="851c2-178">Actor instances are distributed as a result.</span></span>

![Bölümleme aktör ve dağıtım][5]

<span data-ttu-id="851c2-180">Güvenilir hizmetler farklı bir bölüm düzeni ve bölüm anahtarı aralıkları ile oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="851c2-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="851c2-181">Aktör hizmeti aktörler bölümlere eşlemek için tam Int64 anahtar aralığıyla Int64 bölümleme düzenini kullanır.</span><span class="sxs-lookup"><span data-stu-id="851c2-181">The actor service uses the Int64 partitioning scheme with the full Int64 key range to map actors to partitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="851c2-182">Aktör kimliği</span><span class="sxs-lookup"><span data-stu-id="851c2-182">Actor ID</span></span>
<span data-ttu-id="851c2-183">Hizmetinde oluşturulan her aktör tarafından temsil edilen ilişkili benzersiz bir Kimliğe sahip `ActorId` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="851c2-183">Each actor that's created in the service has a unique ID associated with it, represented by the `ActorId` class.</span></span> <span data-ttu-id="851c2-184">`ActorId`rastgele kimlikleri oluşturarak service bölümler aktörler Tekdüzen dağıtım için kullanılabilecek bir donuk kimliği değeridir:</span><span class="sxs-lookup"><span data-stu-id="851c2-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across the service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="851c2-185">Her `ActorId` bir Int64 karma haline getirilir.</span><span class="sxs-lookup"><span data-stu-id="851c2-185">Every `ActorId` is hashed to an Int64.</span></span> <span data-ttu-id="851c2-186">Aktör hizmeti bir Int64 bölümleme düzeni tam Int64 anahtar aralığıyla kullanmalısınız nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="851c2-186">This is why the actor service must use an Int64 partitioning scheme with the full Int64 key range.</span></span> <span data-ttu-id="851c2-187">Ancak, özel kimlik değerleri için kullanılabilecek bir `ActorID`GUID/UUID, dizeleri ve Int64s dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="851c2-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

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

<span data-ttu-id="851c2-188">GUID/UUID ve dizeleri kullanırken, değerlerin bir Int64 karma hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="851c2-188">When you're using GUIDs/UUIDs and strings, the values are hashed to an Int64.</span></span> <span data-ttu-id="851c2-189">Ancak, ne zaman, açıkça sağlayan bir Int64 bir `ActorId`, Int64 daha fazla karma olmadan doğrudan bir bölüm eşler.</span><span class="sxs-lookup"><span data-stu-id="851c2-189">However, when you're explicitly providing an Int64 to an `ActorId`, the Int64 will map directly to a partition without further hashing.</span></span> <span data-ttu-id="851c2-190">Aktör yerleştirilir hangi bölümünü denetlemek için bu tekniği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="851c2-190">You can use this technique to control which partition the actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="851c2-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="851c2-191">Next steps</span></span>
* [<span data-ttu-id="851c2-192">Aktör durum yönetimi</span><span class="sxs-lookup"><span data-stu-id="851c2-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="851c2-193">Aktör yaşam döngüsü ve çöp toplama</span><span class="sxs-lookup"><span data-stu-id="851c2-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="851c2-194">Aktör API başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="851c2-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="851c2-195">.NET örnek kod</span><span class="sxs-lookup"><span data-stu-id="851c2-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="851c2-196">Java örnek kod</span><span class="sxs-lookup"><span data-stu-id="851c2-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
