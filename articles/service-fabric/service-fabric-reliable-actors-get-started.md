---
title: "aaaCreate, ilk aktör tabanlı Azure mikro hizmet C# | Microsoft Docs"
description: "Bu öğretici oluşturma, hata ayıklama ve Service Fabric Reliable Actors kullanarak basit bir aktör tabanlı hizmet dağıtma hello adımlarda size yol gösterir."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="e4e7a-103">Reliable Actors ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e4e7a-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4e7a-104">Windows üzerinde C#</span><span class="sxs-lookup"><span data-stu-id="e4e7a-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="e4e7a-105">Linux üzerinde Java</span><span class="sxs-lookup"><span data-stu-id="e4e7a-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="e4e7a-106">Bu makalede, Azure Service Fabric Reliable Actors hello temelleri açıklanır ve oluşturma, hata ayıklama ve Visual Studio basit bir güvenilir aktör uygulama dağıtma size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="e4e7a-107">Yükleme ve Kurulum</span><span class="sxs-lookup"><span data-stu-id="e4e7a-107">Installation and setup</span></span>
<span data-ttu-id="e4e7a-108">Başlamadan önce makinenizde ayarlanan hello Service Fabric geliştirme ortamı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-108">Before you start, ensure that you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="e4e7a-109">Tooset gerekiyorsa, görmek ayrıntılı yönergeler üzerinde [nasıl hello geliştirme ortamını ayarlama tooset](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e4e7a-109">If you need tooset it up, see detailed instructions on [how tooset up hello development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="e4e7a-110">Temel kavramlar</span><span class="sxs-lookup"><span data-stu-id="e4e7a-110">Basic concepts</span></span>
<span data-ttu-id="e4e7a-111">Reliable Actors ile yalnızca, başlatılan tooget birkaç temel kavramları toounderstand gerekir:</span><span class="sxs-lookup"><span data-stu-id="e4e7a-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="e4e7a-112">**Aktör hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-112">**Actor service**.</span></span> <span data-ttu-id="e4e7a-113">Güvenilir aktörler hello Service Fabric altyapısında dağıtılabilir Reliable Services paketlenir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="e4e7a-114">Aktör örnekleri adlı hizmet örneği içinde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="e4e7a-115">**Aktör kayıt**.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-115">**Actor registration**.</span></span> <span data-ttu-id="e4e7a-116">Olarak Reliable Services ile güvenilir aktör hizmeti ile Merhaba Service Fabric çalışma zamanı kayıtlı toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="e4e7a-117">Ayrıca, hello aktör türü hello aktör çalışma zamanı ile kayıtlı toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="e4e7a-118">**Aktör arabirimi**.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-118">**Actor interface**.</span></span> <span data-ttu-id="e4e7a-119">Merhaba aktör kullanılan toodefine bir aktör kesin türü belirtilmiş bir ortak arabiriminin bir arabirimdir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="e4e7a-120">Hello güvenilir aktör modeli terminolojisi, aktör Merhaba ileti türlerini anlamak ve işleyebilirsiniz hello hello aktör arabirimi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="e4e7a-121">Merhaba aktör arabirimi diğer aktörler tarafından kullanılır ve istemci uygulamaları çok "(uyumsuz) iletileri toohello aktör Gönder".</span><span class="sxs-lookup"><span data-stu-id="e4e7a-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="e4e7a-122">Güvenilir aktörler birden çok arabirimi uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="e4e7a-123">**ActorProxy sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-123">**ActorProxy class**.</span></span> <span data-ttu-id="e4e7a-124">Merhaba ActorProxy sınıfı istemci uygulamaları tooinvoke tarafından kullanılan hello hello aktör arabirimi aracılığıyla kullanıma sunulan yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="e4e7a-125">Merhaba ActorProxy sınıfı iki önemli işlevleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="e4e7a-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="e4e7a-126">Ad çözümlemesi: mümkün toolocate hello aktör (bunu barındırıldığı hello kümesinin Bul hello düğümü) hello kümedeki olduğu.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="e4e7a-127">Hata işleme: Bu yöntem çağrılarına yeniden deneyin ve sonra hello aktör konumu yeniden çözümlemek, örneğin, hello aktör toobe gerektiren bir hata hello kümedeki tooanother düğümde yeniden konumlandırılmasını.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="e4e7a-128">tooactor arabirimleri ilgilidir kuralları aşağıdaki hello tümleştirilmediği şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e4e7a-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="e4e7a-129">Aktör arabirim yöntemleri aşırı yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="e4e7a-130">Aktör arabirimi yöntemlerini çıkışı olmamalıdır, ref veya isteğe bağlı parametreler.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="e4e7a-131">Genel arabirimler desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="e4e7a-132">Visual Studio'da yeni proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="e4e7a-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="e4e7a-133">Visual Studio 2015 veya Visual Studio 2017 yönetici olarak başlatın ve yeni bir Service Fabric uygulaması projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="e4e7a-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Visual Studio - yeni proje için Service Fabric araçları][1]

<span data-ttu-id="e4e7a-135">Merhaba sonraki iletişim kutusunda toocreate istediğiniz proje hello türünü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-135">In hello next dialog box, you can choose hello type of project that you want toocreate.</span></span>

![Service Fabric proje şablonları][5]

<span data-ttu-id="e4e7a-137">Merhaba HelloWorld projesi için hello Service Fabric Reliable Actors hizmet kullanalım.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-137">For hello HelloWorld project, let's use hello Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="e4e7a-138">Merhaba çözüm oluşturduktan sonra yapı izlenerek hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="e4e7a-138">After you have created hello solution, you should see hello following structure:</span></span>

![Service Fabric Proje yapısı][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="e4e7a-140">Güvenilir aktörler temel yapı taşları</span><span class="sxs-lookup"><span data-stu-id="e4e7a-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="e4e7a-141">Tipik bir Reliable Actors çözümü üç projeyi oluşur:</span><span class="sxs-lookup"><span data-stu-id="e4e7a-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="e4e7a-142">**Merhaba uygulama projesi (MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-142">**hello application project (MyActorApplication)**.</span></span> <span data-ttu-id="e4e7a-143">Bu, tüm hello Hizmetleri birlikte dağıtım paketleri hello projesidir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-143">This is hello project that packages all of hello services together for deployment.</span></span> <span data-ttu-id="e4e7a-144">Merhaba içerdiği *ApplicationManifest.xml* ve Merhaba uygulaması yönetmek için PowerShell komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-144">It contains hello *ApplicationManifest.xml* and PowerShell scripts for managing hello application.</span></span>
* <span data-ttu-id="e4e7a-145">**Merhaba arabirimi proje (MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-145">**hello interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="e4e7a-146">Bu arabirim tanımı hello aktör hello içeren hello projesidir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-146">This is hello project that contains hello interface definition for hello actor.</span></span> <span data-ttu-id="e4e7a-147">Merhaba MyActor.Interfaces projesinde hello aktör hello çözümde tarafından kullanılan hello arabirimleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-147">In hello MyActor.Interfaces project, you can define hello interfaces that will be used by hello actors in hello solution.</span></span> <span data-ttu-id="e4e7a-148">Merhaba arabirimi hello aktör uygulama ve genellikle algılama toodefine kolaylaştırır şekilde hello aktör çağırma hello istemcileri tarafından paylaşılan hello aktör sözleşmesini tanımlayan ancak aktör arabirimlerinizi herhangi bir ad ile herhangi bir projeye tanımlanabilir, derleme içinde Merhaba aktör uygulamasından ayırın ve birden çok diğer projeler tarafından paylaşılabilir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-148">Your actor interfaces can be defined in any project with any name, however hello interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in an assembly that is separate from hello actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="e4e7a-149">**Merhaba aktör hizmeti projesi (MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-149">**hello actor service project (MyActor)**.</span></span> <span data-ttu-id="e4e7a-150">Bu, devam eden toohost hello aktör olan hello kullanılan proje toodefine hello Service Fabric hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-150">This is hello project used toodefine hello Service Fabric service that is going toohost hello actor.</span></span> <span data-ttu-id="e4e7a-151">Merhaba aktör hello uygulamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-151">It contains hello implementation of hello actor.</span></span> <span data-ttu-id="e4e7a-152">Aktör hello taban türünden türeyen bir sınıf uygulamasıdır `Actor` ve Implements hello hello MyActor.Interfaces projesinde tanımlanan arabirimi.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-152">An actor implementation is a class that derives from hello base type `Actor` and implements hello interface(s) that are defined in hello MyActor.Interfaces project.</span></span> <span data-ttu-id="e4e7a-153">Aktör sınıfı da kabul eden bir oluşturucu uygulamalıdır bir `ActorService` örneği ve bir `ActorId` ve bunları toohello temel geçirir `Actor` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them toohello base `Actor` class.</span></span> <span data-ttu-id="e4e7a-154">Bu oluşturucu bağımlılık ekleme platform bağımlılıklar için sağlar.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-154">This allows for constructor dependency injection of platform dependencies.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

<span data-ttu-id="e4e7a-155">Merhaba aktör hizmeti hello Service Fabric çalışma zamanında bir hizmet türü ile kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-155">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="e4e7a-156">Merhaba, aktör örneklerinizi aktör hizmeti toorun sipariş, aktör türünüz hello aktör hizmeti ile da kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-156">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="e4e7a-157">Merhaba `ActorRuntime` kayıt yöntemi, bu iş aktörleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-157">hello `ActorRuntime` registration method performs this work for actors.</span></span>

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="e4e7a-158">Visual Studio'da yeni bir proje başlangıç ve yalnızca bir aktör tanımı varsa hello kayıt Visual Studio'nun oluşturduğu hello kodda varsayılan olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-158">If you start from a new project in Visual Studio and you have only one actor definition, hello registration is included by default in hello code that Visual Studio generates.</span></span> <span data-ttu-id="e4e7a-159">Merhaba hizmetinde diğer aktörler tanımlarsanız kullanarak tooadd hello aktör kayıt gerekir:</span><span class="sxs-lookup"><span data-stu-id="e4e7a-159">If you define other actors in hello service, you need tooadd hello actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="e4e7a-160">Merhaba Service Fabric aktör çalışma zamanı bazı yayar [olaylar ve performans sayaçları ilgili tooactor yöntemler](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="e4e7a-160">hello Service Fabric Actors runtime emits some [events and performance counters related tooactor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="e4e7a-161">Bunlar, tanılama ve performans izlemesi kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="e4e7a-162">Hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="e4e7a-162">Debugging</span></span>
<span data-ttu-id="e4e7a-163">Visual Studio için Hello Service Fabric araçları yerel makinenizde hata ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-163">hello Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="e4e7a-164">Hata ayıklama oturumu basarsa hello tarafından F5 tuşuna başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-164">You can start a debugging session by hitting hello F5 key.</span></span> <span data-ttu-id="e4e7a-165">Derlemeler (gerekirse) Visual Studio paketler.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="e4e7a-166">Ayrıca hello yerel Service Fabric kümesi hello uygulama dağıtır ve hello hata ayıklayıcı ekler.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-166">It also deploys hello application on hello local Service Fabric cluster and attaches hello debugger.</span></span>

<span data-ttu-id="e4e7a-167">Merhaba dağıtım işlemi sırasında hello hello ediyor görebilirsiniz **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e4e7a-167">During hello deployment process, you can see hello progress in hello **Output** window.</span></span>

![Service Fabric hata ayıklama çıktı penceresi][3]

## <a name="next-steps"></a><span data-ttu-id="e4e7a-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e4e7a-169">Next steps</span></span>
<span data-ttu-id="e4e7a-170">Daha fazla bilgi edinmek [Reliable Actors hello Service Fabric platformundan kullanma](service-fabric-reliable-actors-platform.md).</span><span class="sxs-lookup"><span data-stu-id="e4e7a-170">Learn more about [how Reliable Actors use hello Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
