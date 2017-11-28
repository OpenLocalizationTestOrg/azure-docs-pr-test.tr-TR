---
title: "Java, ilk aktör tabanlı Azure mikro hizmet oluşturma | Microsoft Docs"
description: "Bu öğretici oluşturma, hata ayıklama ve Service Fabric Reliable Actors kullanarak basit bir aktör tabanlı hizmet dağıtma adımları açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 288f1ed1016f50031065e66444d2562427194dc7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="bc8b3-103">Reliable Actors ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="bc8b3-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc8b3-104">Windows üzerinde C#</span><span class="sxs-lookup"><span data-stu-id="bc8b3-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="bc8b3-105">Linux üzerinde Java</span><span class="sxs-lookup"><span data-stu-id="bc8b3-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="bc8b3-106">Bu makalede, Azure Service Fabric Reliable Actors temelleri açıklanır ve oluşturma ve Java basit bir güvenilir aktör uygulama dağıtma size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="bc8b3-107">Yükleme ve Kurulum</span><span class="sxs-lookup"><span data-stu-id="bc8b3-107">Installation and setup</span></span>
<span data-ttu-id="bc8b3-108">Başlamadan önce makinenizde ayarlanan Service Fabric geliştirme ortamı sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-108">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="bc8b3-109">Bunu ayarlamak gerekiyorsa, Git [Mac Başlarken](service-fabric-get-started-mac.md) veya [Linux'ta Başlarken](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="bc8b3-109">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="bc8b3-110">Temel kavramlar</span><span class="sxs-lookup"><span data-stu-id="bc8b3-110">Basic concepts</span></span>
<span data-ttu-id="bc8b3-111">Reliable Actors ile çalışmaya başlamak için yalnızca birkaç temel kavramları anlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="bc8b3-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="bc8b3-112">**Aktör hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-112">**Actor service**.</span></span> <span data-ttu-id="bc8b3-113">Güvenilir aktörler Service Fabric altyapısında dağıtılabilir Reliable Services paketlenir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="bc8b3-114">Aktör örnekleri adlı hizmet örneği içinde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="bc8b3-115">**Aktör kayıt**.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-115">**Actor registration**.</span></span> <span data-ttu-id="bc8b3-116">Olarak Reliable Services ile güvenilir aktör hizmeti Service Fabric çalışma zamanı ile kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="bc8b3-117">Ayrıca, aktör türü aktör çalışma zamanı ile kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-117">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="bc8b3-118">**Aktör arabirimi**.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-118">**Actor interface**.</span></span> <span data-ttu-id="bc8b3-119">Aktör arabirimi bir aktör, türü kesin belirlenmiş bir ortak arabirimi tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-119">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="bc8b3-120">Güvenilir aktör modeli terminolojisinde aktör arabirimi aktör anlayabileceği iletileri ve işlem türlerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="bc8b3-121">Aktör arabirimi "(uyumsuz) aktör göndermek için" diğer aktörler ve istemci uygulamalar tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="bc8b3-122">Güvenilir aktörler birden çok arabirimi uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="bc8b3-123">**ActorProxy sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-123">**ActorProxy class**.</span></span> <span data-ttu-id="bc8b3-124">ActorProxy sınıfı aktör arabirimi aracılığıyla kullanıma sunulan yöntemleri çağırmak için istemci uygulamaları tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="bc8b3-125">ActorProxy sınıfı iki önemli işlevleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="bc8b3-125">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="bc8b3-126">Ad çözümlemesi: küme (Bul onu barındırıldığı küme düğümünün) aktör bulabilir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="bc8b3-127">Hata işleme: yöntem çağrılarına yeniden deneyin ve yeniden aktör konumu, örneğin, kümedeki başka bir düğüme yeniden konumlandırılmasını aktör gerektiren bir hatadan sonra çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="bc8b3-128">Aktör arabirimlerine ilgilidir aşağıdaki kurallar tümleştirilmediği şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bc8b3-128">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="bc8b3-129">Aktör arabirim yöntemleri aşırı yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="bc8b3-130">Aktör arabirimi yöntemlerini çıkışı olmamalıdır, ref veya isteğe bağlı parametreler.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="bc8b3-131">Genel arabirimler desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="bc8b3-132">Aktör hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc8b3-132">Create an actor service</span></span>
<span data-ttu-id="bc8b3-133">Yeni bir Service Fabric uygulaması oluşturmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="bc8b3-134">Linux için Service Fabric SDK'sı bir Yeoman içeren bir durum bilgisiz Service Service Fabric uygulaması için askılamayı sağlamak için oluşturucu.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-134">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="bc8b3-135">Aşağıdaki Yeoman çalıştırarak komutu:</span><span class="sxs-lookup"><span data-stu-id="bc8b3-135">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="bc8b3-136">Oluşturmak için yönergeleri izleyin bir **güvenilir aktör hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-136">Follow the instructions to create a **Reliable Actor Service**.</span></span> <span data-ttu-id="bc8b3-137">Bu öğretici için "HelloWorldActorApplication" uygulama adı ve aktör "HelloWorldActor."</span><span class="sxs-lookup"><span data-stu-id="bc8b3-137">For this tutorial, name the application "HelloWorldActorApplication" and the actor "HelloWorldActor."</span></span> <span data-ttu-id="bc8b3-138">Aşağıdaki yapı iskelesi oluşturulacak:</span><span class="sxs-lookup"><span data-stu-id="bc8b3-138">The following scaffolding will be created:</span></span>

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="bc8b3-139">Güvenilir aktörler temel yapı taşları</span><span class="sxs-lookup"><span data-stu-id="bc8b3-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="bc8b3-140">Daha önce açıklanan temel kavramları güvenilir aktör hizmetinin temel yapı taşlarının çevir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-140">The basic concepts described earlier translate into the basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="bc8b3-141">Aktör arabirimi</span><span class="sxs-lookup"><span data-stu-id="bc8b3-141">Actor interface</span></span>
<span data-ttu-id="bc8b3-142">Aktör arabirimi tanımını içerir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-142">This contains the interface definition for the actor.</span></span> <span data-ttu-id="bc8b3-143">Bu arabirim aktör uygulama ve böylece genellikle aktör uygulamasından ayrı bir yerde tanımlamak için mantıklı ve birden çok diğer hizmetlerin veya istemci uygulamaları tarafından paylaşılan aktör çağırma istemcileri tarafından paylaşılan aktör sözleşme tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-143">This interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in a place that is separate from the actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="bc8b3-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="bc8b3-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="bc8b3-145">Aktör hizmeti</span><span class="sxs-lookup"><span data-stu-id="bc8b3-145">Actor service</span></span>
<span data-ttu-id="bc8b3-146">Bu, aktör uygulama ve aktör kayıt kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="bc8b3-147">Aktör sınıfı aktör arabirimini uygular.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-147">The actor class implements the actor interface.</span></span> <span data-ttu-id="bc8b3-148">Burada, aktör çalıştığını budur.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-148">This is where your actor does its work.</span></span>

<span data-ttu-id="bc8b3-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="bc8b3-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a><span data-ttu-id="bc8b3-150">Aktör kayıt</span><span class="sxs-lookup"><span data-stu-id="bc8b3-150">Actor registration</span></span>
<span data-ttu-id="bc8b3-151">Aktör hizmeti Service Fabric çalışma zamanında bir hizmet türü ile kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-151">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="bc8b3-152">Aktör hizmetinin aktör örneklerinizi çalışması sırayla aktör türünüz aktör hizmeti ile kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-152">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="bc8b3-153">`ActorRuntime` Kayıt yöntemi, bu iş aktörleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-153">The `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="bc8b3-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="bc8b3-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a><span data-ttu-id="bc8b3-155">Test İstemcisi</span><span class="sxs-lookup"><span data-stu-id="bc8b3-155">Test client</span></span>
<span data-ttu-id="bc8b3-156">Bu basit bir sınama istemci uygulaması olan aktör hizmetinizi test etmek için Service Fabric uygulamadan ayrı olarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-156">This is a simple test client application you can run separately from the Service Fabric application to test your actor service.</span></span> <span data-ttu-id="bc8b3-157">Bir örnek, burada ActorProxy etkinleştirmek ve aktör örnekleri ile iletişim kurmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-157">This is an example of where the ActorProxy can be used to activate and communicate with actor instances.</span></span> <span data-ttu-id="bc8b3-158">Hizmetiniz ile dağıtılan.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-158">It does not get deployed with your service.</span></span>

### <a name="the-application"></a><span data-ttu-id="bc8b3-159">Uygulama</span><span class="sxs-lookup"><span data-stu-id="bc8b3-159">The application</span></span>
<span data-ttu-id="bc8b3-160">Son olarak, uygulama aktör hizmeti ve gelecekte birlikte dağıtım için eklemiş olabileceğiniz diğer hizmetler paketler.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-160">Finally, the application packages the actor service and any other services you might add in the future together for deployment.</span></span> <span data-ttu-id="bc8b3-161">İçerdiği *ApplicationManifest.xml* ve aktör hizmet paketi için yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-161">It contains the *ApplicationManifest.xml* and place holders for the actor service package.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="bc8b3-162">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="bc8b3-162">Run the application</span></span>

<span data-ttu-id="bc8b3-163">Yeoman yapı iskelesi uygulama oluşturup dağıtın ve uygulamayı kaldırmak için komut dosyaları bash bir gradle komut dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-163">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span></span> <span data-ttu-id="bc8b3-164">Uygulamayı dağıtmak için ilk uygulama gradle ile oluşturun:</span><span class="sxs-lookup"><span data-stu-id="bc8b3-164">To deploy the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="bc8b3-165">Bu Service Fabric CLI araçlarını kullanarak dağıtılan bir Service Fabric uygulama paketi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="bc8b3-166">Service Fabric CLI dağıtma</span><span class="sxs-lookup"><span data-stu-id="bc8b3-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="bc8b3-167">İnstall.sh betik uygulama paketi dağıtmak için gerekli Service Fabric CLI (sfctl) komutlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-167">The install.sh script contains the necessary Service Fabric CLI (sfctl) commands to deploy the application package.</span></span>
<span data-ttu-id="bc8b3-168">Uygulamayı dağıtmak için install.sh komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bc8b3-168">Run the install.sh script to deploy the application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="bc8b3-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc8b3-169">Next steps</span></span>

* [<span data-ttu-id="bc8b3-170">Service Fabric CLI ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="bc8b3-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
