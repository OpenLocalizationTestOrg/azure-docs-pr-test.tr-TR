---
title: "aaaCreate, ilk aktör tabanlı Azure mikro hizmet Java | Microsoft Docs"
description: "Bu öğretici oluşturma, hata ayıklama ve Service Fabric Reliable Actors kullanarak basit bir aktör tabanlı hizmet dağıtma hello adımlarda size yol gösterir."
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
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="4c597-103">Reliable Actors ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="4c597-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c597-104">Windows üzerinde C#</span><span class="sxs-lookup"><span data-stu-id="4c597-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="4c597-105">Linux üzerinde Java</span><span class="sxs-lookup"><span data-stu-id="4c597-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="4c597-106">Bu makalede, Azure Service Fabric Reliable Actors hello temelleri açıklanır ve oluşturma ve Java basit bir güvenilir aktör uygulama dağıtma size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="4c597-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="4c597-107">Yükleme ve Kurulum</span><span class="sxs-lookup"><span data-stu-id="4c597-107">Installation and setup</span></span>
<span data-ttu-id="4c597-108">Başlamadan önce makinenizde ayarlanan hello Service Fabric geliştirme ortamı sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4c597-108">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="4c597-109">Tooset ihtiyacınız varsa bunun Git çok[Mac Başlarken](service-fabric-get-started-mac.md) veya [Linux'ta Başlarken](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4c597-109">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="4c597-110">Temel kavramlar</span><span class="sxs-lookup"><span data-stu-id="4c597-110">Basic concepts</span></span>
<span data-ttu-id="4c597-111">Reliable Actors ile yalnızca, başlatılan tooget birkaç temel kavramları toounderstand gerekir:</span><span class="sxs-lookup"><span data-stu-id="4c597-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="4c597-112">**Aktör hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="4c597-112">**Actor service**.</span></span> <span data-ttu-id="4c597-113">Güvenilir aktörler hello Service Fabric altyapısında dağıtılabilir Reliable Services paketlenir.</span><span class="sxs-lookup"><span data-stu-id="4c597-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="4c597-114">Aktör örnekleri adlı hizmet örneği içinde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4c597-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="4c597-115">**Aktör kayıt**.</span><span class="sxs-lookup"><span data-stu-id="4c597-115">**Actor registration**.</span></span> <span data-ttu-id="4c597-116">Olarak Reliable Services ile güvenilir aktör hizmeti ile Merhaba Service Fabric çalışma zamanı kayıtlı toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c597-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="4c597-117">Ayrıca, hello aktör türü hello aktör çalışma zamanı ile kayıtlı toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c597-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="4c597-118">**Aktör arabirimi**.</span><span class="sxs-lookup"><span data-stu-id="4c597-118">**Actor interface**.</span></span> <span data-ttu-id="4c597-119">Merhaba aktör kullanılan toodefine bir aktör kesin türü belirtilmiş bir ortak arabiriminin bir arabirimdir.</span><span class="sxs-lookup"><span data-stu-id="4c597-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="4c597-120">Hello güvenilir aktör modeli terminolojisi, aktör Merhaba ileti türlerini anlamak ve işleyebilirsiniz hello hello aktör arabirimi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="4c597-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="4c597-121">Merhaba aktör arabirimi diğer aktörler tarafından kullanılır ve istemci uygulamaları çok "(uyumsuz) iletileri toohello aktör Gönder".</span><span class="sxs-lookup"><span data-stu-id="4c597-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="4c597-122">Güvenilir aktörler birden çok arabirimi uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c597-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="4c597-123">**ActorProxy sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="4c597-123">**ActorProxy class**.</span></span> <span data-ttu-id="4c597-124">Merhaba ActorProxy sınıfı istemci uygulamaları tooinvoke tarafından kullanılan hello hello aktör arabirimi aracılığıyla kullanıma sunulan yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="4c597-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="4c597-125">Merhaba ActorProxy sınıfı iki önemli işlevleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="4c597-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="4c597-126">Ad çözümlemesi: mümkün toolocate hello aktör (bunu barındırıldığı hello kümesinin Bul hello düğümü) hello kümedeki olduğu.</span><span class="sxs-lookup"><span data-stu-id="4c597-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="4c597-127">Hata işleme: Bu yöntem çağrılarına yeniden deneyin ve sonra hello aktör konumu yeniden çözümlemek, örneğin, hello aktör toobe gerektiren bir hata hello kümedeki tooanother düğümde yeniden konumlandırılmasını.</span><span class="sxs-lookup"><span data-stu-id="4c597-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="4c597-128">tooactor arabirimleri ilgilidir kuralları aşağıdaki hello tümleştirilmediği şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4c597-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="4c597-129">Aktör arabirim yöntemleri aşırı yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="4c597-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="4c597-130">Aktör arabirimi yöntemlerini çıkışı olmamalıdır, ref veya isteğe bağlı parametreler.</span><span class="sxs-lookup"><span data-stu-id="4c597-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="4c597-131">Genel arabirimler desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="4c597-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="4c597-132">Aktör hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c597-132">Create an actor service</span></span>
<span data-ttu-id="4c597-133">Yeni bir Service Fabric uygulaması oluşturmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="4c597-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="4c597-134">Merhaba Linux için Service Fabric SDK içeren bir Yeoman durum bilgisiz hizmeti ile bir Service Fabric uygulaması için oluşturucu tooprovide hello askılamayı.</span><span class="sxs-lookup"><span data-stu-id="4c597-134">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="4c597-135">Merhaba çalıştırarak Yeoman komutu:</span><span class="sxs-lookup"><span data-stu-id="4c597-135">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="4c597-136">Merhaba yönergeleri toocreate izleyin bir **güvenilir aktör hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="4c597-136">Follow hello instructions toocreate a **Reliable Actor Service**.</span></span> <span data-ttu-id="4c597-137">Bu öğretici için ad hello uygulama "HelloWorldActorApplication" ve hello aktör "HelloWorldActor."</span><span class="sxs-lookup"><span data-stu-id="4c597-137">For this tutorial, name hello application "HelloWorldActorApplication" and hello actor "HelloWorldActor."</span></span> <span data-ttu-id="4c597-138">Yapı iskelesi aşağıdaki hello oluşturulacak:</span><span class="sxs-lookup"><span data-stu-id="4c597-138">hello following scaffolding will be created:</span></span>

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

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="4c597-139">Güvenilir aktörler temel yapı taşları</span><span class="sxs-lookup"><span data-stu-id="4c597-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="4c597-140">daha önce açıklanan hello temel kavramları hello temel yapı taşlarını bir güvenilir aktör hizmeti çevir.</span><span class="sxs-lookup"><span data-stu-id="4c597-140">hello basic concepts described earlier translate into hello basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="4c597-141">Aktör arabirimi</span><span class="sxs-lookup"><span data-stu-id="4c597-141">Actor interface</span></span>
<span data-ttu-id="4c597-142">Bu hello aktör hello arabirimi tanımını içerir.</span><span class="sxs-lookup"><span data-stu-id="4c597-142">This contains hello interface definition for hello actor.</span></span> <span data-ttu-id="4c597-143">Bu arabirim hello aktör uygulama ve genellikle bu olan bir yerde hello aktör uygulamasından ayırın ve birden çok diğer tarafından paylaşılan algılama toodefine kolaylaştırır şekilde hello aktör çağırma hello istemcileri tarafından paylaşılan hello aktör sözleşme tanımlar Hizmet veya istemci uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="4c597-143">This interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in a place that is separate from hello actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="4c597-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="4c597-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="4c597-145">Aktör hizmeti</span><span class="sxs-lookup"><span data-stu-id="4c597-145">Actor service</span></span>
<span data-ttu-id="4c597-146">Bu, aktör uygulama ve aktör kayıt kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="4c597-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="4c597-147">Merhaba Aktör sınıfı hello aktör arabirimini uygular.</span><span class="sxs-lookup"><span data-stu-id="4c597-147">hello actor class implements hello actor interface.</span></span> <span data-ttu-id="4c597-148">Burada, aktör çalıştığını budur.</span><span class="sxs-lookup"><span data-stu-id="4c597-148">This is where your actor does its work.</span></span>

<span data-ttu-id="4c597-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="4c597-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

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

### <a name="actor-registration"></a><span data-ttu-id="4c597-150">Aktör kayıt</span><span class="sxs-lookup"><span data-stu-id="4c597-150">Actor registration</span></span>
<span data-ttu-id="4c597-151">Merhaba aktör hizmeti hello Service Fabric çalışma zamanında bir hizmet türü ile kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c597-151">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="4c597-152">Merhaba, aktör örneklerinizi aktör hizmeti toorun sipariş, aktör türünüz hello aktör hizmeti ile da kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c597-152">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="4c597-153">Merhaba `ActorRuntime` kayıt yöntemi, bu iş aktörleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="4c597-153">hello `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="4c597-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="4c597-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

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

### <a name="test-client"></a><span data-ttu-id="4c597-155">Test İstemcisi</span><span class="sxs-lookup"><span data-stu-id="4c597-155">Test client</span></span>
<span data-ttu-id="4c597-156">Bu basit bir sınama istemci uygulaması olan aktör hizmetinizi hello Service Fabric uygulaması tootest ayrı olarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c597-156">This is a simple test client application you can run separately from hello Service Fabric application tootest your actor service.</span></span> <span data-ttu-id="4c597-157">Bir örnek burada hello ActorProxy kullanılan tooactivate olması ve aktör örnekleriyle iletişim.</span><span class="sxs-lookup"><span data-stu-id="4c597-157">This is an example of where hello ActorProxy can be used tooactivate and communicate with actor instances.</span></span> <span data-ttu-id="4c597-158">Hizmetiniz ile dağıtılan.</span><span class="sxs-lookup"><span data-stu-id="4c597-158">It does not get deployed with your service.</span></span>

### <a name="hello-application"></a><span data-ttu-id="4c597-159">Merhaba uygulaması</span><span class="sxs-lookup"><span data-stu-id="4c597-159">hello application</span></span>
<span data-ttu-id="4c597-160">Son olarak, hello uygulama paketleri aktör hizmeti ve hello birlikte dağıtım için gelecekte ekleme olasılığınız diğer hizmetler hello.</span><span class="sxs-lookup"><span data-stu-id="4c597-160">Finally, hello application packages hello actor service and any other services you might add in hello future together for deployment.</span></span> <span data-ttu-id="4c597-161">Merhaba içerdiği *ApplicationManifest.xml* ve hello aktör hizmet paketi için yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="4c597-161">It contains hello *ApplicationManifest.xml* and place holders for hello actor service package.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="4c597-162">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="4c597-162">Run hello application</span></span>

<span data-ttu-id="4c597-163">Merhaba Yeoman yapı iskelesi, gradle betik toobuild hello uygulama ve bash betikleri toodeploy ve Kaldır uygulamayı içerir.</span><span class="sxs-lookup"><span data-stu-id="4c597-163">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="4c597-164">toodeploy hello uygulama ilk yapı hello gradle ile:</span><span class="sxs-lookup"><span data-stu-id="4c597-164">toodeploy hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="4c597-165">Bu Service Fabric CLI araçlarını kullanarak dağıtılan bir Service Fabric uygulama paketi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4c597-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="4c597-166">Service Fabric CLI dağıtma</span><span class="sxs-lookup"><span data-stu-id="4c597-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="4c597-167">Merhaba install.sh betik hello gerekli Service Fabric CLI (sfctl) komutları toodeploy hello uygulama paketi içerir.</span><span class="sxs-lookup"><span data-stu-id="4c597-167">hello install.sh script contains hello necessary Service Fabric CLI (sfctl) commands toodeploy hello application package.</span></span>
<span data-ttu-id="4c597-168">Merhaba install.sh betik toodeploy hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4c597-168">Run hello install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="4c597-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4c597-169">Next steps</span></span>

* [<span data-ttu-id="4c597-170">Service Fabric CLI ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="4c597-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
