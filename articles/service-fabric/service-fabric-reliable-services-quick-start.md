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
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="a8046-103">Reliable Services özelliğini kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="a8046-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a8046-104">Windows üzerinde C#</span><span class="sxs-lookup"><span data-stu-id="a8046-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="a8046-105">Linux üzerinde Java</span><span class="sxs-lookup"><span data-stu-id="a8046-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="a8046-106">Azure Service Fabric uygulaması kodunuzu çalıştırmak bir veya daha fazla hizmet içeriyor.</span><span class="sxs-lookup"><span data-stu-id="a8046-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="a8046-107">Bu kılavuz size nasıl gösterir toocreate durum bilgisiz ve durum bilgisi olan Service Fabric uygulamaları ile [Reliable Services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a8046-107">This guide shows you how toocreate both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="a8046-108">Bu Microsoft Virtual Academy video de nasıl gösterir toocreate durum bilgisiz güvenilir hizmet:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="a8046-108">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="a8046-109">Temel kavramlar</span><span class="sxs-lookup"><span data-stu-id="a8046-109">Basic concepts</span></span>
<span data-ttu-id="a8046-110">Reliable Services ile size yalnızca çalışmaya tooget birkaç temel kavramları toounderstand gerekir:</span><span class="sxs-lookup"><span data-stu-id="a8046-110">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="a8046-111">**Hizmet türü**: hizmet uygulamanızın budur.</span><span class="sxs-lookup"><span data-stu-id="a8046-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="a8046-112">Genişleten yazma hello sınıf tarafından tanımlanan `StatelessService` ve diğer kod veya bağımlılıkları, bir ad ve sürüm numarası ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a8046-112">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="a8046-113">**Hizmet örneği adlı**: toorun sınıf türü nesne örneklerini oluşturmak gibi hizmetiniz, adlandırılmış örnekleri, hizmet türüne ilişkin çok oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="a8046-113">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="a8046-114">Bir hizmet örneği hello kullanarak bir URI hello biçiminde olan bir ada sahip "fabric: /" gibi Düzen "fabric: / MyApp/MyService".</span><span class="sxs-lookup"><span data-stu-id="a8046-114">A service instance has a name in hello form of a URI using hello "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="a8046-115">**Hizmet ana bilgisayarı**: hizmet örneklerinin ihtiyacı toorun barındırma işlemi içinde oluşturduğunuz adlı hello.</span><span class="sxs-lookup"><span data-stu-id="a8046-115">**Service host**: hello named service instances you create need toorun inside a host process.</span></span> <span data-ttu-id="a8046-116">Merhaba hizmet ana bilgisayarı hizmet örneklerini çalıştırdığı yalnızca bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="a8046-116">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="a8046-117">**Hizmet kayıt**: kayıt getirir her şeyi birlikte.</span><span class="sxs-lookup"><span data-stu-id="a8046-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="a8046-118">Merhaba hizmet türü kaydedilmelidir Service Fabric hello ile bir hizmeti çalışma zamanı ana bilgisayar tooallow Service Fabric toocreate örnekleri toorun.</span><span class="sxs-lookup"><span data-stu-id="a8046-118">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="a8046-119">Durum bilgisi olmayan bir hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8046-119">Create a stateless service</span></span>
<span data-ttu-id="a8046-120">Durum bilgisiz Hizmet şu anda hello norm bulut uygulamalarında hizmet türüdür.</span><span class="sxs-lookup"><span data-stu-id="a8046-120">A stateless service is a type of service that is currently hello norm in cloud applications.</span></span> <span data-ttu-id="a8046-121">Merhaba hizmetin kendisini güvenilir bir şekilde depolanır veya yüksek oranda kullanılabilir hale toobe gereken veri içermediğinden durum bilgisiz olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="a8046-121">It is considered stateless because hello service itself does not contain data that needs toobe stored reliably or made highly available.</span></span> <span data-ttu-id="a8046-122">Durum bilgisiz Hizmeti'nin bir örneğini kapanırsa, iç durumu kaybolur.</span><span class="sxs-lookup"><span data-stu-id="a8046-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="a8046-123">Bu tür hizmet, Azure tablo veya bir SQL veritabanı gibi dış depolama kalıcı tooan durumu olmalıdır için toobe yapılan yüksek oranda kullanılabilir ve güvenilir.</span><span class="sxs-lookup"><span data-stu-id="a8046-123">In this type of service, state must be persisted tooan external store, such as Azure Tables or a SQL database, for it toobe made highly available and reliable.</span></span>

<span data-ttu-id="a8046-124">Visual Studio 2015 veya Visual Studio 2017 yönetici olarak başlatın ve adlı yeni bir Service Fabric uygulaması projesi oluşturduğunuzda *HelloWorld*:</span><span class="sxs-lookup"><span data-stu-id="a8046-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![Merhaba yeni proje iletişim kutusu toocreate yeni bir Service Fabric uygulaması kullanın](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="a8046-126">Adlı bir durum bilgisiz hizmet projesi oluşturma *HelloWorldStateless*:</span><span class="sxs-lookup"><span data-stu-id="a8046-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![Hello ikinci iletişim kutusunda, durum bilgisiz hizmet projesi oluşturma](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="a8046-128">Çözümünüzü şimdi iki proje içerir:</span><span class="sxs-lookup"><span data-stu-id="a8046-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="a8046-129">*HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="a8046-129">*HelloWorld*.</span></span> <span data-ttu-id="a8046-130">Merhaba budur *uygulama* içeren projesi, *Hizmetleri*.</span><span class="sxs-lookup"><span data-stu-id="a8046-130">This is hello *application* project that contains your *services*.</span></span> <span data-ttu-id="a8046-131">Ayrıca, uygulamanızı Merhaba uygulaması gibi bir dizi toodeploy Yardım PowerShell Betiği açıklar hello uygulama bildirimi içerir.</span><span class="sxs-lookup"><span data-stu-id="a8046-131">It also contains hello application manifest that describes hello application, as well as a number of PowerShell scripts that help you toodeploy your application.</span></span>
* <span data-ttu-id="a8046-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="a8046-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="a8046-133">Merhaba hizmet projesi budur.</span><span class="sxs-lookup"><span data-stu-id="a8046-133">This is hello service project.</span></span> <span data-ttu-id="a8046-134">Merhaba durum bilgisiz hizmet uygulaması içerir.</span><span class="sxs-lookup"><span data-stu-id="a8046-134">It contains hello stateless service implementation.</span></span>

## <a name="implement-hello-service"></a><span data-ttu-id="a8046-135">Merhaba hizmet ekleme</span><span class="sxs-lookup"><span data-stu-id="a8046-135">Implement hello service</span></span>
<span data-ttu-id="a8046-136">Açık hello **HelloWorldStateless.cs** hello hizmet proje dosyasında.</span><span class="sxs-lookup"><span data-stu-id="a8046-136">Open hello **HelloWorldStateless.cs** file in hello service project.</span></span> <span data-ttu-id="a8046-137">Service Fabric içinde bir hizmet iş mantığı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8046-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="a8046-138">Merhaba hizmeti API'si kodunuz için iki giriş noktaları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a8046-138">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="a8046-139">Adlı bir uçlu giriş noktası yöntemi *RunAsync*, burada uzun süre çalışan işlem iş yükleri de dahil olmak üzere tüm iş yükleri yürütme başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8046-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="a8046-140">Burada, iletişim yığınında ASP.NET Core gibi tercih ettiğiniz ekleyebilirsiniz iletişimi giriş noktası.</span><span class="sxs-lookup"><span data-stu-id="a8046-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="a8046-141">Kullanıcılar ve diğer hizmetler isteklerini almak başlayabileceğiniz budur.</span><span class="sxs-lookup"><span data-stu-id="a8046-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="a8046-142">Bu öğreticide, biz hello odaklanacaktır `RunAsync()` giriş noktası yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a8046-142">In this tutorial, we will focus on hello `RunAsync()` entry point method.</span></span> <span data-ttu-id="a8046-143">Hemen kodunuzu çalıştırmaya başlayabileceğiniz budur.</span><span class="sxs-lookup"><span data-stu-id="a8046-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="a8046-144">Merhaba proje şablonu içeren bir örnek uygulaması `RunAsync()` , çalışırken sayısını artırır.</span><span class="sxs-lookup"><span data-stu-id="a8046-144">hello project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="a8046-145">Nasıl bir iletişimle toowork yığın hakkında daha fazla bilgi için bkz [OWIN kendi kendine barındırma ile Service Fabric Web API Hizmetleri](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="a8046-145">For details about how toowork with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="a8046-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="a8046-146">RunAsync</span></span>
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

<span data-ttu-id="a8046-147">bir hizmet örneği yerleştirilen ve hazır tooexecute olduğunda hello platform bu yöntemi çağırır.</span><span class="sxs-lookup"><span data-stu-id="a8046-147">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="a8046-148">Merhaba hizmet örneği açıldığında durumsuz bir hizmet için basitçe anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a8046-148">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="a8046-149">Hizmet örneğinizi kapalı toobe gerektiğinde bir iptal belirteci toocoordinate sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a8046-149">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="a8046-150">Service Fabric bu hizmet örneği Aç/Kapat döngüsünü hello hizmetinin birçok kez hello ömrü boyunca bir bütün olarak ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="a8046-150">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="a8046-151">Bu da dahil olmak üzere çeşitli nedenlerden kaynaklanabilir:</span><span class="sxs-lookup"><span data-stu-id="a8046-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="a8046-152">Merhaba sistem, hizmet örneği için kaynak Dengeleme taşır.</span><span class="sxs-lookup"><span data-stu-id="a8046-152">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="a8046-153">Kodunuzdaki hataları oluşur.</span><span class="sxs-lookup"><span data-stu-id="a8046-153">Faults occur in your code.</span></span>
* <span data-ttu-id="a8046-154">Merhaba uygulama veya sistem yükseltilir.</span><span class="sxs-lookup"><span data-stu-id="a8046-154">hello application or system is upgraded.</span></span>
* <span data-ttu-id="a8046-155">Merhaba temel alınan donanım kesinti karşılaşır.</span><span class="sxs-lookup"><span data-stu-id="a8046-155">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="a8046-156">Bu düzenlemesi hello sistem tookeep tarafından yönetilen hizmetinizi yüksek oranda kullanılabilir ve düzgün şekilde dengeli.</span><span class="sxs-lookup"><span data-stu-id="a8046-156">This orchestration is managed by hello system tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="a8046-157">`RunAsync()`zaman uyumlu olarak bloğu değil.</span><span class="sxs-lookup"><span data-stu-id="a8046-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="a8046-158">Uygulamanıza RunAsync, bir görev döndürür veya herhangi uzun süre çalışan veya engelleme işlemleri tooallow hello çalışma zamanı toocontinue bekler.</span><span class="sxs-lookup"><span data-stu-id="a8046-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="a8046-159">Merhaba notta `while(true)` hello önceki örnekte, bir görev döndüren bir döngüde `await Task.Delay()` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a8046-159">Note in hello `while(true)` loop in hello previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="a8046-160">İş yükünüzün zaman uyumlu olarak engellemelidir, yeni bir görev ile zamanlamalısınız `Task.Run()` içinde `RunAsync` uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a8046-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="a8046-161">İş yükünüzün iptaline iptal belirteci sağlanan hello tarafından düzenlenmiş işbirlikçi çaba ' dir.</span><span class="sxs-lookup"><span data-stu-id="a8046-161">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="a8046-162">Merhaba sistem (başarılı bir şekilde tamamlandığında, iptal veya hataya göre) için görev tooend bekleyecek taşır önce.</span><span class="sxs-lookup"><span data-stu-id="a8046-162">hello system will wait for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="a8046-163">Herhangi bir iş ve çıkış önemli toohonor hello iptal belirteci, bitiş olduğu `RunAsync()` hello sistem iptal istediğinde mümkün olan en kısa sürede.</span><span class="sxs-lookup"><span data-stu-id="a8046-163">It is important toohonor hello cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when hello system requests cancellation.</span></span>

<span data-ttu-id="a8046-164">Bu durum bilgisiz hizmet örnekte hello sayısı yerel bir değişkende depolanır.</span><span class="sxs-lookup"><span data-stu-id="a8046-164">In this stateless service example, hello count is stored in a local variable.</span></span> <span data-ttu-id="a8046-165">Ancak bu durum bilgisi olmayan bir hizmet olduğundan, yalnızca hello geçerli yaşam döngüsünü kendi hizmet örneği için depolanan hello değeri yok.</span><span class="sxs-lookup"><span data-stu-id="a8046-165">But because this is a stateless service, hello value that's stored exists only for hello current lifecycle of its service instance.</span></span> <span data-ttu-id="a8046-166">Merhaba hizmet taşır veya yeniden hello değeri kayıp olur.</span><span class="sxs-lookup"><span data-stu-id="a8046-166">When hello service moves or restarts, hello value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="a8046-167">Durum bilgisi olan bir hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8046-167">Create a stateful service</span></span>
<span data-ttu-id="a8046-168">Service Fabric hizmetinin durum bilgisi olan yeni bir tür tanıtır.</span><span class="sxs-lookup"><span data-stu-id="a8046-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="a8046-169">Durum bilgisi olan hizmet tarafından kullanıldığı hello kod ile birlikte bulunan güvenilir bir şekilde hello hizmetin kendisini içinde durumu koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8046-169">A stateful service can maintain state reliably within hello service itself, co-located with hello code that's using it.</span></span> <span data-ttu-id="a8046-170">Durum Service Fabric tarafından hello gerek toopersist durum tooan dış depolama yüksek oranda kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="a8046-170">State is made highly available by Service Fabric without hello need toopersist state tooan external store.</span></span>

<span data-ttu-id="a8046-171">Merhaba hizmet taşır veya yeniden başlatır, olsa bile tooconvert durum bilgisiz toohighly kullanılabilir ve kalıcı bir sayaç değeri, bir durum bilgisi olan hizmet gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8046-171">tooconvert a counter value from stateless toohighly available and persistent, even when hello service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="a8046-172">İçinde aynı hello *HelloWorld* uygulama hello Hizmetleri başvurularında hello uygulama projesi ve seçerek üzerinde sağ tıklayarak yeni bir hizmet ekleyebilirsiniz **Ekle -> Yeni yapı hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="a8046-172">In hello same *HelloWorld* application, you can add a new service by right-clicking on hello Services references in hello application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![Hizmet tooyour Service Fabric uygulaması ekleyin](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="a8046-174">Seçin **durum bilgisi olan hizmet** ve adlandırın *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="a8046-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="a8046-175">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a8046-175">Click **OK**.</span></span>

![Merhaba yeni proje iletişim kutusu toocreate yeni bir Service Fabric durum bilgisi olan hizmet kullanın](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="a8046-177">Uygulamanızı şimdi iki Hizmetleri olmalıdır: Merhaba durum bilgisiz hizmet *HelloWorldStateless* ve hello durum bilgisi olan hizmet *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="a8046-177">Your application should now have two services: hello stateless service *HelloWorldStateless* and hello stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="a8046-178">Durum bilgisi olan bir hizmet hello sahiptir ve durum bilgisi olmayan hizmet olarak aynı giriş noktaları.</span><span class="sxs-lookup"><span data-stu-id="a8046-178">A stateful service has hello same entry points as a stateless service.</span></span> <span data-ttu-id="a8046-179">Merhaba ana farktır hello kullanılabilirliğini bir *durum sağlayıcısı* , saklayabilir durumu güvenilir.</span><span class="sxs-lookup"><span data-stu-id="a8046-179">hello main difference is hello availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="a8046-180">Service Fabric adlı durum sağlayıcısı bir uygulama ile birlikte gelen [güvenilir koleksiyonları](service-fabric-reliable-services-reliable-collections.md), olanak sağlayan güvenilir durum Yöneticisi hello yoluyla çoğaltılan veri yapılarını oluşturmanıza.</span><span class="sxs-lookup"><span data-stu-id="a8046-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through hello Reliable State Manager.</span></span> <span data-ttu-id="a8046-181">Durum bilgisi olan güvenilir hizmet varsayılan olarak bu durum sağlayıcısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="a8046-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="a8046-182">Açık **HelloWorldStateful.cs** içinde *HelloWorldStateful*, RunAsync yöntemi aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="a8046-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains hello following RunAsync method:</span></span>

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

### <a name="runasync"></a><span data-ttu-id="a8046-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="a8046-183">RunAsync</span></span>
<span data-ttu-id="a8046-184">`RunAsync()`durum bilgisi olan ve durum bilgisiz Hizmetleri'nde benzer şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="a8046-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="a8046-185">Yürütülmeden önce ancak, bir durum bilgisi olan hizmeti hello platform ek çalışma sizin adınıza gerçekleştirir `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="a8046-185">However, in a stateful service, hello platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="a8046-186">Bu iş o hello güvenilir durum Yöneticisi sağlama içerebilir ve hazır toouse güvenilir koleksiyonlarıdır.</span><span class="sxs-lookup"><span data-stu-id="a8046-186">This work can include ensuring that hello Reliable State Manager and Reliable Collections are ready toouse.</span></span>

### <a name="reliable-collections-and-hello-reliable-state-manager"></a><span data-ttu-id="a8046-187">Güvenilir koleksiyonları ve hello güvenilir durum Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="a8046-187">Reliable Collections and hello Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="a8046-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) tooreliably deposu durumu hello hizmetindeki kullanabilirsiniz bir sözlük uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="a8046-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use tooreliably store state in hello service.</span></span> <span data-ttu-id="a8046-189">Service Fabric ve güvenilir koleksiyonlarla, hizmetiniz için bir dış kalıcı depoya hello gerek kalmadan doğrudan veri depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8046-189">With Service Fabric and Reliable Collections, you can store data directly in your service without hello need for an external persistent store.</span></span> <span data-ttu-id="a8046-190">Güvenilir koleksiyonları verilerinizin yüksek oranda kullanılabilir yap.</span><span class="sxs-lookup"><span data-stu-id="a8046-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="a8046-191">Service Fabric gerçekleştirir, bu, oluşturma ve birden çok yönetme *çoğaltmaları* hizmetinizin sizin için.</span><span class="sxs-lookup"><span data-stu-id="a8046-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="a8046-192">Ayrıca, bu çoğaltmaların ve bunların durumu geçişleri yönetme koyma hello karmaşıklık soyutlar bir API sağlar.</span><span class="sxs-lookup"><span data-stu-id="a8046-192">It also provides an API that abstracts away hello complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="a8046-193">Güvenilir koleksiyonları birkaç uyarılar, özel türleri dahil olmak üzere, herhangi bir .NET türü depolayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a8046-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="a8046-194">Service Fabric durumunuza tarafından yüksek oranda kullanılabilir kılar *çoğaltma* durumunu düğümler ve güvenilir koleksiyonları arasında her kopyada veri toolocal diski depolamak.</span><span class="sxs-lookup"><span data-stu-id="a8046-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data toolocal disk on each replica.</span></span> <span data-ttu-id="a8046-195">Bu güvenilir koleksiyonu içinde depolanan her şey olması gerektiği anlamına gelir *seri hale getirilebilir*.</span><span class="sxs-lookup"><span data-stu-id="a8046-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="a8046-196">Varsayılan olarak, güvenilir koleksiyonları kullanmaya [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) seri hale getirme için bu nedenle olduğu önemli toomake türlerinizi olduğundan emin [hello veri sözleşmesi seri hale getirici tarafından desteklenen](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) hello varsayılan kullandığınızda Serileştirici.</span><span class="sxs-lookup"><span data-stu-id="a8046-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important toomake sure that your types are [supported by hello Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use hello default serializer.</span></span>
* <span data-ttu-id="a8046-197">Güvenilir derlemeler işlemleri yaparsanız nesneleri yüksek kullanılabilirlik için çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="a8046-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="a8046-198">Güvenilir koleksiyonu içinde depolanan nesneleri hizmetinizi yerel bellekte tutulur.</span><span class="sxs-lookup"><span data-stu-id="a8046-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="a8046-199">Bu, yerel başvuru toohello nesnesi olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a8046-199">This means that you have a local reference toohello object.</span></span>
  
   <span data-ttu-id="a8046-200">Bu nesne yerel örnekleri işlemde hello güvenilir koleksiyonu bir güncelleştirme işlemi gerçekleştirilirken olmadan mutate değil, önemlidir.</span><span class="sxs-lookup"><span data-stu-id="a8046-200">It is important that you do not mutate local instances of those objects without performing an update operation on hello reliable collection in a transaction.</span></span> <span data-ttu-id="a8046-201">Değişiklikleri toolocal nesnelerinin örneklerini otomatik olarak çoğaltılmayacak olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="a8046-201">This is because changes toolocal instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="a8046-202">Merhaba nesneyi geri hello sözlükteki yeniden eklemek veya hello birini kullanın *güncelleştirme* hello sözlük yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="a8046-202">You must re-insert hello object back into hello dictionary or use one of hello *update* methods on hello dictionary.</span></span>

<span data-ttu-id="a8046-203">Merhaba güvenilir durum Yöneticisi güvenilir koleksiyonları tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="a8046-203">hello Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="a8046-204">Yalnızca hello güvenilir durum Yöneticisi için güvenilir bir koleksiyon adıyla herhangi bir zamanda ve herhangi bir yerde hizmetinizi sorabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8046-204">You can simply ask hello Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="a8046-205">bir başvuru ulaşırsınız Hello güvenilir durum Yöneticisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a8046-205">hello Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="a8046-206">Verme önerilir, başvuruları tooreliable koleksiyonu örnekleri sınıf üyesi değişkenleri veya özellikleri kaydetmeniz.</span><span class="sxs-lookup"><span data-stu-id="a8046-206">We don't recommended that you save references tooreliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="a8046-207">Merhaba başvuru ayarlandığını tooensure önemi gerçekleştirilecek tooan örneği hello hizmet çevriminin her zaman.</span><span class="sxs-lookup"><span data-stu-id="a8046-207">Special care must be taken tooensure that hello reference is set tooan instance at all times in hello service lifecycle.</span></span> <span data-ttu-id="a8046-208">Merhaba güvenilir durum Yöneticisi bu iş, işler ve yineleme ziyaretleriniz için optimize edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a8046-208">hello Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="a8046-209">İşlem ve zaman uyumsuz işlemler</span><span class="sxs-lookup"><span data-stu-id="a8046-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="a8046-210">Merhaba çoğunu sahip güvenilir koleksiyonların aynı işlemleri, kendi `System.Collections.Generic` ve `System.Collections.Concurrent` ortaklarınıza LINQ hariç.</span><span class="sxs-lookup"><span data-stu-id="a8046-210">Reliable Collections have many of hello same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="a8046-211">Güvenilir derlemeler işlemleri zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="a8046-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="a8046-212">Yazma işlemleri güvenilir koleksiyonlarıyla g/ç işlemleri tooreplicate gerçekleştirmek ve veri toodisk kalır olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="a8046-212">This is because write operations with Reliable Collections perform I/O operations tooreplicate and persist data toodisk.</span></span>

<span data-ttu-id="a8046-213">Güvenilir toplama işlemleri *işlem*, böylece, durumu tutarlı birden çok güvenilir koleksiyonları ve işlemler arasında tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8046-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="a8046-214">Örneğin, bir iş öğesi güvenilir bir kuyruktan dequeue bir işlem gerçekleştirmek ve sözlükteki güvenilir, tümü tek bir işlem içinde hello sonucu kaydetmek.</span><span class="sxs-lookup"><span data-stu-id="a8046-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save hello result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="a8046-215">Bu atomik bir işlem olarak kabul edilir ve hello tüm işlemi başarılı olur veya hello tüm işlemi geri alma güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="a8046-215">This is treated as an atomic operation, and it guarantees that either hello entire operation will succeed or hello entire operation will roll back.</span></span> <span data-ttu-id="a8046-216">Merhaba öğesi dequeue sonra bir hata oluşursa, ancak hello sonuç kaydetmeden önce hello tüm işlem geri alındı ve işleme hello sırasındaki hello öğesi kalır.</span><span class="sxs-lookup"><span data-stu-id="a8046-216">If an error occurs after you dequeue hello item but before you save hello result, hello entire transaction is rolled back and hello item remains in hello queue for processing.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="a8046-217">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="a8046-217">Run hello application</span></span>
<span data-ttu-id="a8046-218">Şimdi toohello döndürürüz *HelloWorld* uygulama.</span><span class="sxs-lookup"><span data-stu-id="a8046-218">We now return toohello *HelloWorld* application.</span></span> <span data-ttu-id="a8046-219">Artık, yapı ve hizmetlerinizi dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8046-219">You can now build and deploy your services.</span></span> <span data-ttu-id="a8046-220">Bastığınızda **F5**, uygulamanızı oluşturulan ve dağıtılan tooyour yerel küme olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8046-220">When you press **F5**, your application will be built and deployed tooyour local cluster.</span></span>

<span data-ttu-id="a8046-221">Merhaba çalışmaya başlamak Hizmetleri sonra oluşturulan hello olay Windows için izleme (ETW) olayları görüntüleyebilirsiniz bir **tanılama olayları** penceresi.</span><span class="sxs-lookup"><span data-stu-id="a8046-221">After hello services start running, you can view hello generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="a8046-222">Görüntülenen hello olaylar hello durum bilgisi olmayan hizmet ve durum bilgisi olan hizmeti hello uygulamasında hello olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a8046-222">Note that hello events displayed are from both hello stateless service and hello stateful service in hello application.</span></span> <span data-ttu-id="a8046-223">Merhaba tıklayarak hello akış duraklatabilirsiniz **duraklatma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a8046-223">You can pause hello stream by clicking hello **Pause** button.</span></span> <span data-ttu-id="a8046-224">Bu iletiyi genişleterek sonra bir ileti hello ayrıntılarını inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8046-224">You can then examine hello details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="a8046-225">Merhaba uygulamayı çalıştırmadan önce çalıştıran bir yerel geliştirme kümesine sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a8046-225">Before you run hello application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="a8046-226">Merhaba denetleyin [Başlangıç Kılavuzu](service-fabric-get-started.md) yerel ortamınızı ayarlama hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="a8046-226">Check out hello [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![Visual Studio tanılama olaylarını görüntüle](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="a8046-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a8046-228">Next steps</span></span>
[<span data-ttu-id="a8046-229">Service Fabric uygulamanızı Visual Studio'da hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="a8046-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="a8046-230">Kullanmaya başlama: OWIN kendi kendine barındırma ile Service Fabric Web API Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="a8046-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="a8046-231">Güvenilir Koleksiyonlar hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="a8046-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="a8046-232">Bir uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="a8046-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="a8046-233">Uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="a8046-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="a8046-234">Güvenilir hizmetler için Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="a8046-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

