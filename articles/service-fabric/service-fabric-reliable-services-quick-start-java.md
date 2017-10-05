---
title: "Java'da ilk, güvenilir Azure mikro hizmet oluşturma | Microsoft Docs"
description: "Durum bilgisiz ve durum bilgisi olan Hizmetleri ile Microsoft Azure Service Fabric uygulaması oluşturma giriş."
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
ms.openlocfilehash: 1ebabe4844732412e04bab8c277f7ebbc4a5737c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="65b7b-103">Reliable Services özelliğini kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="65b7b-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="65b7b-104">Windows üzerinde C#</span><span class="sxs-lookup"><span data-stu-id="65b7b-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="65b7b-105">Linux üzerinde Java</span><span class="sxs-lookup"><span data-stu-id="65b7b-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="65b7b-106">Bu makalede, Azure Service Fabric Reliable Services temelleri açıklanır ve oluşturma ve Java'da yazılmış basit bir güvenilir hizmet uygulaması dağıtma size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="65b7b-106">This article explains the basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="65b7b-107">Bu Microsoft Virtual Academy video ayrıca durum bilgisiz güvenilir bir hizmetin nasıl oluşturulacağını gösterir:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="65b7b-107">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="65b7b-108">Yükleme ve Kurulum</span><span class="sxs-lookup"><span data-stu-id="65b7b-108">Installation and setup</span></span>
<span data-ttu-id="65b7b-109">Başlamadan önce makinenizde ayarlanan Service Fabric geliştirme ortamı sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="65b7b-109">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="65b7b-110">Bunu ayarlamak gerekiyorsa, Git [Mac Başlarken](service-fabric-get-started-mac.md) veya [Linux'ta Başlarken](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="65b7b-110">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="65b7b-111">Temel kavramlar</span><span class="sxs-lookup"><span data-stu-id="65b7b-111">Basic concepts</span></span>
<span data-ttu-id="65b7b-112">Reliable Services ile çalışmaya başlamak için yalnızca birkaç temel kavramları anlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="65b7b-112">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="65b7b-113">**Hizmet türü**: hizmet uygulamanızın budur.</span><span class="sxs-lookup"><span data-stu-id="65b7b-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="65b7b-114">Genişleten yazma sınıf tarafından tanımlanan `StatelessService` ve diğer kod veya bağımlılıkları, bir ad ve sürüm numarası ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="65b7b-114">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="65b7b-115">**Hizmet örneği adlı**: sınıf türü nesne örneklerini oluşturmak gibi hizmetinizi çalıştırmak için adlandırılmış örnekleri, hizmet türüne ilişkin çok oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="65b7b-115">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="65b7b-116">Hizmeti aslında, yazma, bir hizmet sınıfında nesne örneklemesi örnekleridir.</span><span class="sxs-lookup"><span data-stu-id="65b7b-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="65b7b-117">**Hizmet ana bilgisayarı**: oluşturduğunuz adlandırılmış hizmet örneklerinin bir konak içinde çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="65b7b-117">**Service host**: The named service instances you create need to run inside a host.</span></span> <span data-ttu-id="65b7b-118">Hizmet ana bilgisayarı hizmet örneklerini çalıştırdığı yalnızca bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="65b7b-118">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="65b7b-119">**Hizmet kayıt**: kayıt getirir her şeyi birlikte.</span><span class="sxs-lookup"><span data-stu-id="65b7b-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="65b7b-120">Hizmet türü çalıştırmak için Service Fabric çalışma zamanı ile örnekleri oluşturmak Service Fabric izin vermek için bir hizmet ana bilgisayarı kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="65b7b-120">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="65b7b-121">Durum bilgisi olmayan bir hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="65b7b-121">Create a stateless service</span></span>
<span data-ttu-id="65b7b-122">Service Fabric uygulaması oluşturmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="65b7b-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="65b7b-123">Linux için Service Fabric SDK'sı bir Yeoman içeren bir durum bilgisiz Service Service Fabric uygulaması için askılamayı sağlamak için oluşturucu.</span><span class="sxs-lookup"><span data-stu-id="65b7b-123">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="65b7b-124">Aşağıdaki Yeoman çalıştırarak komutu:</span><span class="sxs-lookup"><span data-stu-id="65b7b-124">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="65b7b-125">Oluşturmak için yönergeleri izleyin bir **güvenilir durum bilgisiz hizmet**.</span><span class="sxs-lookup"><span data-stu-id="65b7b-125">Follow the instructions to create a **Reliable Stateless Service**.</span></span> <span data-ttu-id="65b7b-126">Bu öğretici için "HelloWorldApplication" uygulama adı ve "HelloWorld" hizmet.</span><span class="sxs-lookup"><span data-stu-id="65b7b-126">For this tutorial, name the application "HelloWorldApplication" and the service "HelloWorld".</span></span> <span data-ttu-id="65b7b-127">Dizinler için sonuç içerir `HelloWorldApplication` ve `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="65b7b-127">The result includes directories for the `HelloWorldApplication` and `HelloWorld`.</span></span>

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

## <a name="implement-the-service"></a><span data-ttu-id="65b7b-128">Uygulama hizmeti</span><span class="sxs-lookup"><span data-stu-id="65b7b-128">Implement the service</span></span>
<span data-ttu-id="65b7b-129">Açık **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="65b7b-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="65b7b-130">Bu sınıf, hizmet türünü tanımlar ve herhangi bir kod çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65b7b-130">This class defines the service type, and can run any code.</span></span> <span data-ttu-id="65b7b-131">Hizmeti API'si kodunuz için iki giriş noktaları sağlar:</span><span class="sxs-lookup"><span data-stu-id="65b7b-131">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="65b7b-132">Adlı bir uçlu giriş noktası yöntemi `runAsync()`, burada uzun süre çalışan işlem iş yükleri de dahil olmak üzere tüm iş yükleri yürütme başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65b7b-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="65b7b-133">Seçim içinde iletişim yığını burada takın iletişimi giriş noktası.</span><span class="sxs-lookup"><span data-stu-id="65b7b-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="65b7b-134">Kullanıcılar ve diğer hizmetler isteklerini almak başlayabileceğiniz budur.</span><span class="sxs-lookup"><span data-stu-id="65b7b-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="65b7b-135">Bu öğreticide, biz odaklanmak `runAsync()` giriş noktası yöntemi.</span><span class="sxs-lookup"><span data-stu-id="65b7b-135">In this tutorial, we focus on the `runAsync()` entry point method.</span></span> <span data-ttu-id="65b7b-136">Hemen kodunuzu çalıştırmaya başlayabileceğiniz budur.</span><span class="sxs-lookup"><span data-stu-id="65b7b-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="65b7b-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="65b7b-137">RunAsync</span></span>
<span data-ttu-id="65b7b-138">Bir hizmet örneği yerleştirilen ve çalıştırılmaya hazır olduğunda platform bu yöntemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="65b7b-138">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="65b7b-139">Hizmet örneği açıldığında durumsuz bir hizmet için basitçe anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="65b7b-139">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="65b7b-140">Hizmet örneğinizi kapatılması gerektiğinde koordine etmek için bir iptal belirteci sağlanır.</span><span class="sxs-lookup"><span data-stu-id="65b7b-140">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="65b7b-141">Service Fabric bu hizmet örneği Aç/Kapat döngüsünü birçok kez ömrü hizmeti bir bütün olarak ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="65b7b-141">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="65b7b-142">Bu da dahil olmak üzere çeşitli nedenlerden kaynaklanabilir:</span><span class="sxs-lookup"><span data-stu-id="65b7b-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="65b7b-143">Sistem, hizmet örneği için kaynak Dengeleme taşır.</span><span class="sxs-lookup"><span data-stu-id="65b7b-143">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="65b7b-144">Kodunuzdaki hataları oluşur.</span><span class="sxs-lookup"><span data-stu-id="65b7b-144">Faults occur in your code.</span></span>
* <span data-ttu-id="65b7b-145">Uygulama veya sistem yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="65b7b-145">The application or system is upgraded.</span></span>
* <span data-ttu-id="65b7b-146">Temel alınan donanım kesinti karşılaşır.</span><span class="sxs-lookup"><span data-stu-id="65b7b-146">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="65b7b-147">Bu düzenlemesi yönetilen hizmetinizi yüksek oranda kullanılabilir ve düzgün şekilde dengeli tutmak için Service Fabric tarafından.</span><span class="sxs-lookup"><span data-stu-id="65b7b-147">This orchestration is managed by Service Fabric to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="65b7b-148">`runAsync()`zaman uyumlu olarak bloğu değil.</span><span class="sxs-lookup"><span data-stu-id="65b7b-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="65b7b-149">Uygulamanıza runAsync devam etmek çalışma zamanı izin vermek için bir CompletableFuture döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="65b7b-149">Your implementation of runAsync should return a CompletableFuture to allow the runtime to continue.</span></span> <span data-ttu-id="65b7b-150">İş yükünüzün içinde CompletableFuture yapılmalıdır uzun süre çalışan bir görev uygulamak gerekip gerekmediğini.</span><span class="sxs-lookup"><span data-stu-id="65b7b-150">If your workload needs to implement a long running task that should be done inside the CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="65b7b-151">İptal etme</span><span class="sxs-lookup"><span data-stu-id="65b7b-151">Cancellation</span></span>
<span data-ttu-id="65b7b-152">İş yükünüzün iptaline tarafından sağlanan iptal belirteci bağımsızlıklar işbirlikçi çaba ' dir.</span><span class="sxs-lookup"><span data-stu-id="65b7b-152">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="65b7b-153">Sistem göreviniz (başarılı bir şekilde tamamlandığında, iptal veya hataya göre) taşır önce sona erdirmek bekler.</span><span class="sxs-lookup"><span data-stu-id="65b7b-153">The system waits for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="65b7b-154">İptal belirteci dikkate için herhangi bir iş bitirip çıkmak önemlidir `runAsync()` sistem iptal istediğinde mümkün olan en kısa sürede.</span><span class="sxs-lookup"><span data-stu-id="65b7b-154">It is important to honor the cancellation token, finish any work, and exit `runAsync()` as quickly as possible when the system requests cancellation.</span></span> <span data-ttu-id="65b7b-155">Aşağıdaki örnek, bir iptal olayını işlemek gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="65b7b-155">The following example demonstrates how to handle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace the following sample code with your own logic
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

### <a name="service-registration"></a><span data-ttu-id="65b7b-156">Hizmet kayıt</span><span class="sxs-lookup"><span data-stu-id="65b7b-156">Service registration</span></span>
<span data-ttu-id="65b7b-157">Hizmet türlerini Service Fabric çalışma zamanı ile kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="65b7b-157">Service types must be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="65b7b-158">Hizmet türü tanımlanan `ServiceManifest.xml` ve uygulayan hizmet sınıfınızı `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="65b7b-158">The service type is defined in the `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="65b7b-159">Hizmet kayıt işlemi ana giriş noktası gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="65b7b-159">Service registration is performed in the process main entry point.</span></span> <span data-ttu-id="65b7b-160">Bu örnekte işlem ana giriş noktasıdır `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="65b7b-160">In this example, the process main entry point is `HelloWorldServiceHost.java`:</span></span>

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

## <a name="run-the-application"></a><span data-ttu-id="65b7b-161">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="65b7b-161">Run the application</span></span>

<span data-ttu-id="65b7b-162">Yeoman yapı iskelesi uygulama oluşturup dağıtın ve uygulamayı kaldırmak için komut dosyaları bash bir gradle komut dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="65b7b-162">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span></span> <span data-ttu-id="65b7b-163">Uygulamayı çalıştırmak için ilk uygulama gradle ile oluşturun:</span><span class="sxs-lookup"><span data-stu-id="65b7b-163">To run the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="65b7b-164">Bu, Service Fabric CLI kullanarak dağıtılan bir Service Fabric uygulama paketi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="65b7b-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="65b7b-165">Service Fabric CLI ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="65b7b-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="65b7b-166">Uygulama paketi dağıtmak için gerekli Service Fabric CLI komutları install.sh komut dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="65b7b-166">The install.sh script contains the necessary Service Fabric CLI commands to deploy the application package.</span></span> <span data-ttu-id="65b7b-167">Uygulamayı dağıtmak için install.sh komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="65b7b-167">Run the install.sh script to deploy the application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="65b7b-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65b7b-168">Next steps</span></span>

* [<span data-ttu-id="65b7b-169">Service Fabric CLI ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="65b7b-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
