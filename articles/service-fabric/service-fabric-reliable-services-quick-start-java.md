---
title: "aaaCreate, ilk güvenilir Azure mikro hizmet Java | Microsoft Docs"
description: "Giriş toocreating durum bilgisiz ve durum bilgisi olan hizmetler ile Microsoft Azure Service Fabric uygulaması."
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="a60d7-103">Reliable Services özelliğini kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="a60d7-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a60d7-104">Windows üzerinde C#</span><span class="sxs-lookup"><span data-stu-id="a60d7-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="a60d7-105">Linux üzerinde Java</span><span class="sxs-lookup"><span data-stu-id="a60d7-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="a60d7-106">Bu makalede, Azure Service Fabric Reliable Services hello temelleri açıklanır ve oluşturma ve Java'da yazılmış basit bir güvenilir hizmet uygulaması dağıtma size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="a60d7-106">This article explains hello basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="a60d7-107">Bu Microsoft Virtual Academy video de nasıl gösterir toocreate durum bilgisiz güvenilir hizmet:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="a60d7-107">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="a60d7-108">Yükleme ve Kurulum</span><span class="sxs-lookup"><span data-stu-id="a60d7-108">Installation and setup</span></span>
<span data-ttu-id="a60d7-109">Başlamadan önce makinenizde ayarlanan hello Service Fabric geliştirme ortamı sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a60d7-109">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="a60d7-110">Tooset ihtiyacınız varsa bunun Git çok[Mac Başlarken](service-fabric-get-started-mac.md) veya [Linux'ta Başlarken](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a60d7-110">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="a60d7-111">Temel kavramlar</span><span class="sxs-lookup"><span data-stu-id="a60d7-111">Basic concepts</span></span>
<span data-ttu-id="a60d7-112">Reliable Services ile size yalnızca çalışmaya tooget birkaç temel kavramları toounderstand gerekir:</span><span class="sxs-lookup"><span data-stu-id="a60d7-112">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="a60d7-113">**Hizmet türü**: hizmet uygulamanızın budur.</span><span class="sxs-lookup"><span data-stu-id="a60d7-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="a60d7-114">Genişleten yazma hello sınıf tarafından tanımlanan `StatelessService` ve diğer kod veya bağımlılıkları, bir ad ve sürüm numarası ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a60d7-114">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="a60d7-115">**Hizmet örneği adlı**: toorun sınıf türü nesne örneklerini oluşturmak gibi hizmetiniz, adlandırılmış örnekleri, hizmet türüne ilişkin çok oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="a60d7-115">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="a60d7-116">Hizmeti aslında, yazma, bir hizmet sınıfında nesne örneklemesi örnekleridir.</span><span class="sxs-lookup"><span data-stu-id="a60d7-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="a60d7-117">**Hizmet ana bilgisayarı**: gerek toorun bir ana bilgisayar içinde oluşturduğunuz hizmet örnekleri adlı hello.</span><span class="sxs-lookup"><span data-stu-id="a60d7-117">**Service host**: hello named service instances you create need toorun inside a host.</span></span> <span data-ttu-id="a60d7-118">Merhaba hizmet ana bilgisayarı hizmet örneklerini çalıştırdığı yalnızca bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="a60d7-118">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="a60d7-119">**Hizmet kayıt**: kayıt getirir her şeyi birlikte.</span><span class="sxs-lookup"><span data-stu-id="a60d7-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="a60d7-120">Merhaba hizmet türü kaydedilmelidir Service Fabric hello ile bir hizmeti çalışma zamanı ana bilgisayar tooallow Service Fabric toocreate örnekleri toorun.</span><span class="sxs-lookup"><span data-stu-id="a60d7-120">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="a60d7-121">Durum bilgisi olmayan bir hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="a60d7-121">Create a stateless service</span></span>
<span data-ttu-id="a60d7-122">Service Fabric uygulaması oluşturmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="a60d7-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="a60d7-123">Merhaba Linux için Service Fabric SDK içeren bir Yeoman durum bilgisiz hizmeti ile bir Service Fabric uygulaması için oluşturucu tooprovide hello askılamayı.</span><span class="sxs-lookup"><span data-stu-id="a60d7-123">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="a60d7-124">Merhaba çalıştırarak Yeoman komutu:</span><span class="sxs-lookup"><span data-stu-id="a60d7-124">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="a60d7-125">Merhaba yönergeleri toocreate izleyin bir **güvenilir durum bilgisiz hizmet**.</span><span class="sxs-lookup"><span data-stu-id="a60d7-125">Follow hello instructions toocreate a **Reliable Stateless Service**.</span></span> <span data-ttu-id="a60d7-126">Bu öğretici için ad Merhaba uygulaması "HelloWorldApplication" Merhaba "HelloWorld" service ve.</span><span class="sxs-lookup"><span data-stu-id="a60d7-126">For this tutorial, name hello application "HelloWorldApplication" and hello service "HelloWorld".</span></span> <span data-ttu-id="a60d7-127">Merhaba sonuç içerir hello için dizinler `HelloWorldApplication` ve `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="a60d7-127">hello result includes directories for hello `HelloWorldApplication` and `HelloWorld`.</span></span>

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a><span data-ttu-id="a60d7-128">Merhaba hizmet ekleme</span><span class="sxs-lookup"><span data-stu-id="a60d7-128">Implement hello service</span></span>
<span data-ttu-id="a60d7-129">Açık **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="a60d7-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="a60d7-130">Bu sınıf hello hizmet türünü tanımlar ve herhangi bir kod çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a60d7-130">This class defines hello service type, and can run any code.</span></span> <span data-ttu-id="a60d7-131">Merhaba hizmeti API'si kodunuz için iki giriş noktaları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a60d7-131">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="a60d7-132">Adlı bir uçlu giriş noktası yöntemi `runAsync()`, burada uzun süre çalışan işlem iş yükleri de dahil olmak üzere tüm iş yükleri yürütme başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a60d7-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="a60d7-133">Seçim içinde iletişim yığını burada takın iletişimi giriş noktası.</span><span class="sxs-lookup"><span data-stu-id="a60d7-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="a60d7-134">Kullanıcılar ve diğer hizmetler isteklerini almak başlayabileceğiniz budur.</span><span class="sxs-lookup"><span data-stu-id="a60d7-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="a60d7-135">Bu öğreticide, biz hello üzerinde odaklanmak `runAsync()` giriş noktası yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a60d7-135">In this tutorial, we focus on hello `runAsync()` entry point method.</span></span> <span data-ttu-id="a60d7-136">Hemen kodunuzu çalıştırmaya başlayabileceğiniz budur.</span><span class="sxs-lookup"><span data-stu-id="a60d7-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="a60d7-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="a60d7-137">RunAsync</span></span>
<span data-ttu-id="a60d7-138">bir hizmet örneği yerleştirilen ve hazır tooexecute olduğunda hello platform bu yöntemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="a60d7-138">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="a60d7-139">Merhaba hizmet örneği açıldığında durumsuz bir hizmet için basitçe anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a60d7-139">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="a60d7-140">Hizmet örneğinizi kapalı toobe gerektiğinde bir iptal belirteci toocoordinate sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a60d7-140">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="a60d7-141">Service Fabric bu hizmet örneği Aç/Kapat döngüsünü hello hizmetinin birçok kez hello ömrü boyunca bir bütün olarak ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="a60d7-141">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="a60d7-142">Bu da dahil olmak üzere çeşitli nedenlerden kaynaklanabilir:</span><span class="sxs-lookup"><span data-stu-id="a60d7-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="a60d7-143">Merhaba sistem, hizmet örneği için kaynak Dengeleme taşır.</span><span class="sxs-lookup"><span data-stu-id="a60d7-143">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="a60d7-144">Kodunuzdaki hataları oluşur.</span><span class="sxs-lookup"><span data-stu-id="a60d7-144">Faults occur in your code.</span></span>
* <span data-ttu-id="a60d7-145">Merhaba uygulama veya sistem yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="a60d7-145">hello application or system is upgraded.</span></span>
* <span data-ttu-id="a60d7-146">Merhaba temel alınan donanım kesinti karşılaşır.</span><span class="sxs-lookup"><span data-stu-id="a60d7-146">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="a60d7-147">Bu düzenlemesi Service Fabric tookeep tarafından yönetilen hizmetinizi yüksek oranda kullanılabilir ve düzgün şekilde dengeli.</span><span class="sxs-lookup"><span data-stu-id="a60d7-147">This orchestration is managed by Service Fabric tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="a60d7-148">`runAsync()`zaman uyumlu olarak bloğu değil.</span><span class="sxs-lookup"><span data-stu-id="a60d7-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="a60d7-149">Uygulamanıza runAsync CompletableFuture tooallow hello çalışma zamanı toocontinue döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="a60d7-149">Your implementation of runAsync should return a CompletableFuture tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="a60d7-150">İş yükünüzün tooimplement içinde yapılmalıdır uzun süre çalışan bir görev gerekiyorsa CompletableFuture hello.</span><span class="sxs-lookup"><span data-stu-id="a60d7-150">If your workload needs tooimplement a long running task that should be done inside hello CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="a60d7-151">İptal etme</span><span class="sxs-lookup"><span data-stu-id="a60d7-151">Cancellation</span></span>
<span data-ttu-id="a60d7-152">İş yükünüzün iptaline iptal belirteci sağlanan hello tarafından düzenlenmiş işbirlikçi çaba ' dir.</span><span class="sxs-lookup"><span data-stu-id="a60d7-152">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="a60d7-153">Merhaba sistem bekler, görev tooend için (başarılı bir şekilde tamamlandığında, iptal veya hataya göre) taşır önce.</span><span class="sxs-lookup"><span data-stu-id="a60d7-153">hello system waits for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="a60d7-154">Herhangi bir iş ve çıkış önemli toohonor hello iptal belirteci, bitiş olduğu `runAsync()` hello sistem iptal istediğinde mümkün olan en kısa sürede.</span><span class="sxs-lookup"><span data-stu-id="a60d7-154">It is important toohonor hello cancellation token, finish any work, and exit `runAsync()` as quickly as possible when hello system requests cancellation.</span></span> <span data-ttu-id="a60d7-155">Merhaba aşağıdaki örnekte gösterilmiştir nasıl toohandle iptal olay:</span><span class="sxs-lookup"><span data-stu-id="a60d7-155">hello following example demonstrates how toohandle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a><span data-ttu-id="a60d7-156">Hizmet kayıt</span><span class="sxs-lookup"><span data-stu-id="a60d7-156">Service registration</span></span>
<span data-ttu-id="a60d7-157">Hizmet türlerini hello Service Fabric çalışma zamanı ile kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a60d7-157">Service types must be registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="a60d7-158">Merhaba hizmet türü hello tanımlanan `ServiceManifest.xml` ve uygulayan hizmet sınıfınızı `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="a60d7-158">hello service type is defined in hello `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="a60d7-159">Hizmet kayıt hello işlem ana giriş noktası gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a60d7-159">Service registration is performed in hello process main entry point.</span></span> <span data-ttu-id="a60d7-160">Bu örnekte, ana giriş noktası işlem hello `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="a60d7-160">In this example, hello process main entry point is `HelloWorldServiceHost.java`:</span></span>

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a><span data-ttu-id="a60d7-161">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="a60d7-161">Run hello application</span></span>

<span data-ttu-id="a60d7-162">Merhaba Yeoman yapı iskelesi, gradle betik toobuild hello uygulama ve bash betikleri toodeploy ve Kaldır uygulamayı içerir.</span><span class="sxs-lookup"><span data-stu-id="a60d7-162">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="a60d7-163">toorun hello uygulama ilk yapı hello gradle ile:</span><span class="sxs-lookup"><span data-stu-id="a60d7-163">toorun hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="a60d7-164">Bu, Service Fabric CLI kullanarak dağıtılan bir Service Fabric uygulama paketi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a60d7-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="a60d7-165">Service Fabric CLI ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="a60d7-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="a60d7-166">Merhaba install.sh betik hello gerekli Service Fabric CLI komutları toodeploy hello uygulama paketi içerir.</span><span class="sxs-lookup"><span data-stu-id="a60d7-166">hello install.sh script contains hello necessary Service Fabric CLI commands toodeploy hello application package.</span></span> <span data-ttu-id="a60d7-167">İnstall.sh betik toodeploy hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a60d7-167">Run the install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="a60d7-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a60d7-168">Next steps</span></span>

* [<span data-ttu-id="a60d7-169">Service Fabric CLI ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a60d7-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
