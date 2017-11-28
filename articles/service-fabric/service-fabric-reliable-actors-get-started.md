---
title: "İlk aktör tabanlı Azure mikro hizmet C# ' ta oluşturma | Microsoft Docs"
description: "Bu öğretici oluşturma, hata ayıklama ve Service Fabric Reliable Actors kullanarak basit bir aktör tabanlı hizmet dağıtma adımları açıklanmaktadır."
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
ms.openlocfilehash: 3f447e049ccd33c77f422e8aa703ad6646f9ffa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="481c7-103">Reliable Actors ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="481c7-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="481c7-104">Windows üzerinde C#</span><span class="sxs-lookup"><span data-stu-id="481c7-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="481c7-105">Linux üzerinde Java</span><span class="sxs-lookup"><span data-stu-id="481c7-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="481c7-106">Bu makalede, Azure Service Fabric Reliable Actors temelleri açıklanır ve oluşturma, hata ayıklama ve Visual Studio basit bir güvenilir aktör uygulama dağıtma size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="481c7-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="481c7-107">Yükleme ve Kurulum</span><span class="sxs-lookup"><span data-stu-id="481c7-107">Installation and setup</span></span>
<span data-ttu-id="481c7-108">Başlamadan önce makinenizde ayarlanan Service Fabric geliştirme ortamı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="481c7-108">Before you start, ensure that you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="481c7-109">Ayrıntılı yönergeler ayarlamanız gerekiyorsa, bakın [geliştirme ortamını ayarlama konusunda](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="481c7-109">If you need to set it up, see detailed instructions on [how to set up the development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="481c7-110">Temel kavramlar</span><span class="sxs-lookup"><span data-stu-id="481c7-110">Basic concepts</span></span>
<span data-ttu-id="481c7-111">Reliable Actors ile çalışmaya başlamak için yalnızca birkaç temel kavramları anlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="481c7-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="481c7-112">**Aktör hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="481c7-112">**Actor service**.</span></span> <span data-ttu-id="481c7-113">Güvenilir aktörler Service Fabric altyapısında dağıtılabilir Reliable Services paketlenir.</span><span class="sxs-lookup"><span data-stu-id="481c7-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="481c7-114">Aktör örnekleri adlı hizmet örneği içinde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="481c7-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="481c7-115">**Aktör kayıt**.</span><span class="sxs-lookup"><span data-stu-id="481c7-115">**Actor registration**.</span></span> <span data-ttu-id="481c7-116">Olarak Reliable Services ile güvenilir aktör hizmeti Service Fabric çalışma zamanı ile kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="481c7-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="481c7-117">Ayrıca, aktör türü aktör çalışma zamanı ile kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="481c7-117">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="481c7-118">**Aktör arabirimi**.</span><span class="sxs-lookup"><span data-stu-id="481c7-118">**Actor interface**.</span></span> <span data-ttu-id="481c7-119">Aktör arabirimi bir aktör, türü kesin belirlenmiş bir ortak arabirimi tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="481c7-119">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="481c7-120">Güvenilir aktör modeli terminolojisinde aktör arabirimi aktör anlayabileceği iletileri ve işlem türlerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="481c7-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="481c7-121">Aktör arabirimi "(uyumsuz) aktör göndermek için" diğer aktörler ve istemci uygulamalar tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="481c7-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="481c7-122">Güvenilir aktörler birden çok arabirimi uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="481c7-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="481c7-123">**ActorProxy sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="481c7-123">**ActorProxy class**.</span></span> <span data-ttu-id="481c7-124">ActorProxy sınıfı aktör arabirimi aracılığıyla kullanıma sunulan yöntemleri çağırmak için istemci uygulamaları tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="481c7-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="481c7-125">ActorProxy sınıfı iki önemli işlevleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="481c7-125">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="481c7-126">Ad çözümlemesi: küme (Bul onu barındırıldığı küme düğümünün) aktör bulabilir.</span><span class="sxs-lookup"><span data-stu-id="481c7-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="481c7-127">Hata işleme: yöntem çağrılarına yeniden deneyin ve yeniden aktör konumu, örneğin, kümedeki başka bir düğüme yeniden konumlandırılmasını aktör gerektiren bir hatadan sonra çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="481c7-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="481c7-128">Aktör arabirimlerine ilgilidir aşağıdaki kurallar tümleştirilmediği şunlardır:</span><span class="sxs-lookup"><span data-stu-id="481c7-128">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="481c7-129">Aktör arabirim yöntemleri aşırı yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="481c7-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="481c7-130">Aktör arabirimi yöntemlerini çıkışı olmamalıdır, ref veya isteğe bağlı parametreler.</span><span class="sxs-lookup"><span data-stu-id="481c7-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="481c7-131">Genel arabirimler desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="481c7-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="481c7-132">Visual Studio'da yeni proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="481c7-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="481c7-133">Visual Studio 2015 veya Visual Studio 2017 yönetici olarak başlatın ve yeni bir Service Fabric uygulaması projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="481c7-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Visual Studio - yeni proje için Service Fabric araçları][1]

<span data-ttu-id="481c7-135">Sonraki iletişim kutusunda, oluşturmak istediğiniz proje türünü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="481c7-135">In the next dialog box, you can choose the type of project that you want to create.</span></span>

![Service Fabric proje şablonları][5]

<span data-ttu-id="481c7-137">HelloWorld projesi için Service Fabric Reliable Actors hizmet kullanalım.</span><span class="sxs-lookup"><span data-stu-id="481c7-137">For the HelloWorld project, let's use the Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="481c7-138">Çözüm oluşturduktan sonra aşağıdaki yapısını görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="481c7-138">After you have created the solution, you should see the following structure:</span></span>

![Service Fabric Proje yapısı][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="481c7-140">Güvenilir aktörler temel yapı taşları</span><span class="sxs-lookup"><span data-stu-id="481c7-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="481c7-141">Tipik bir Reliable Actors çözümü üç projeyi oluşur:</span><span class="sxs-lookup"><span data-stu-id="481c7-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="481c7-142">**Uygulama projesi (MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="481c7-142">**The application project (MyActorApplication)**.</span></span> <span data-ttu-id="481c7-143">Bu, tüm hizmetlerin birlikte dağıtım paketleri projesidir.</span><span class="sxs-lookup"><span data-stu-id="481c7-143">This is the project that packages all of the services together for deployment.</span></span> <span data-ttu-id="481c7-144">İçerdiği *ApplicationManifest.xml* ve uygulama yönetmek için PowerShell komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="481c7-144">It contains the *ApplicationManifest.xml* and PowerShell scripts for managing the application.</span></span>
* <span data-ttu-id="481c7-145">**Arabirim proje (MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="481c7-145">**The interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="481c7-146">Aktör arabirim tanımı içeren projeye budur.</span><span class="sxs-lookup"><span data-stu-id="481c7-146">This is the project that contains the interface definition for the actor.</span></span> <span data-ttu-id="481c7-147">MyActor.Interfaces projesinde çözümdeki aktör tarafından kullanılacak olan arabirimler tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="481c7-147">In the MyActor.Interfaces project, you can define the interfaces that will be used by the actors in the solution.</span></span> <span data-ttu-id="481c7-148">Aktör uygulaması tarafından paylaşılan aktör sözleşme arabirimi tanımlar ancak aktör arabirimlerinizi herhangi bir ad ile herhangi bir projeye tanımlanabilir ve aktör çağırma istemcileri, bu nedenle genellikle aktör uygulamasından ayrıdır ve diğer birden çok proje tarafından paylaşılan bir bütünleştirilmiş tanımlamak için mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="481c7-148">Your actor interfaces can be defined in any project with any name, however the interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in an assembly that is separate from the actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="481c7-149">**Aktör hizmeti projesi (MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="481c7-149">**The actor service project (MyActor)**.</span></span> <span data-ttu-id="481c7-150">Aktör barındırmak için giderek Service Fabric hizmeti tanımlamak için kullanılan proje budur.</span><span class="sxs-lookup"><span data-stu-id="481c7-150">This is the project used to define the Service Fabric service that is going to host the actor.</span></span> <span data-ttu-id="481c7-151">Aktör uygulamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="481c7-151">It contains the implementation of the actor.</span></span> <span data-ttu-id="481c7-152">Taban türünden türeyen bir sınıf bir aktör uygulamasıdır `Actor` ve MyActor.Interfaces projesinde tanımlanan arabirimlere uygulanır.</span><span class="sxs-lookup"><span data-stu-id="481c7-152">An actor implementation is a class that derives from the base type `Actor` and implements the interface(s) that are defined in the MyActor.Interfaces project.</span></span> <span data-ttu-id="481c7-153">Aktör sınıfı da kabul eden bir oluşturucu uygulamalıdır bir `ActorService` örneği ve bir `ActorId` ve tabanına geçirir `Actor` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="481c7-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them to the base `Actor` class.</span></span> <span data-ttu-id="481c7-154">Bu oluşturucu bağımlılık ekleme platform bağımlılıklar için sağlar.</span><span class="sxs-lookup"><span data-stu-id="481c7-154">This allows for constructor dependency injection of platform dependencies.</span></span>

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

<span data-ttu-id="481c7-155">Aktör hizmeti Service Fabric çalışma zamanında bir hizmet türü ile kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="481c7-155">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="481c7-156">Aktör hizmetinin aktör örneklerinizi çalışması sırayla aktör türünüz aktör hizmeti ile kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="481c7-156">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="481c7-157">`ActorRuntime` Kayıt yöntemi, bu iş aktörleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="481c7-157">The `ActorRuntime` registration method performs this work for actors.</span></span>

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

<span data-ttu-id="481c7-158">Visual Studio'da yeni bir proje başlangıç ve yalnızca bir aktör tanımı varsa, kayıt Visual Studio'nun oluşturduğu kodu varsayılan olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="481c7-158">If you start from a new project in Visual Studio and you have only one actor definition, the registration is included by default in the code that Visual Studio generates.</span></span> <span data-ttu-id="481c7-159">Diğer aktörler hizmetinde tanımlarsanız kullanarak aktör kayıt eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="481c7-159">If you define other actors in the service, you need to add the actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="481c7-160">Service Fabric aktör çalışma zamanı bazı yayar [olaylar ve performans sayaçları ilgili aktör yöntemler](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="481c7-160">The Service Fabric Actors runtime emits some [events and performance counters related to actor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="481c7-161">Bunlar, tanılama ve performans izlemesi kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="481c7-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="481c7-162">Hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="481c7-162">Debugging</span></span>
<span data-ttu-id="481c7-163">Visual Studio için Service Fabric araçları yerel makinenizde hata ayıklama desteği.</span><span class="sxs-lookup"><span data-stu-id="481c7-163">The Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="481c7-164">F5 tuşuna basmak tarafından bir hata ayıklama oturumu başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="481c7-164">You can start a debugging session by hitting the F5 key.</span></span> <span data-ttu-id="481c7-165">Derlemeler (gerekirse) Visual Studio paketler.</span><span class="sxs-lookup"><span data-stu-id="481c7-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="481c7-166">Ayrıca, yerel Service Fabric kümesi uygulamayı dağıtır ve hata ayıklayıcı ekler.</span><span class="sxs-lookup"><span data-stu-id="481c7-166">It also deploys the application on the local Service Fabric cluster and attaches the debugger.</span></span>

<span data-ttu-id="481c7-167">Dağıtım işlemi sırasında devam eden görebilirsiniz **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="481c7-167">During the deployment process, you can see the progress in the **Output** window.</span></span>

![Service Fabric hata ayıklama çıktı penceresi][3]

## <a name="next-steps"></a><span data-ttu-id="481c7-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="481c7-169">Next steps</span></span>
<span data-ttu-id="481c7-170">Daha fazla bilgi edinmek [Reliable Actors Service Fabric platformundan kullanma](service-fabric-reliable-actors-platform.md).</span><span class="sxs-lookup"><span data-stu-id="481c7-170">Learn more about [how Reliable Actors use the Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
