---
title: "Merhaba ASP.NET Core ile aaaService iletişim | Microsoft Docs"
description: "Bilgi toouse ASP.NET Core nasıl durum bilgisiz ve durum bilgisi olan güvenilir hizmetler."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 6e6a83ab04390150292f63de5d9b51d290284e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="ed43e-103">ASP.NET çekirdek Service Fabric güvenilir hizmetler</span><span class="sxs-lookup"><span data-stu-id="ed43e-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="ed43e-104">ASP.NET Core modern bulut tabanlı Internet'e bağlı uygulamaları, web uygulamaları, IOT uygulamaları ve mobil arka uçlarını gibi oluşturmak için yeni bir açık kaynaklı ve çapraz platform framework kümesidir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="ed43e-105">Bu makalede ASP.NET Core services Service Fabric güvenilir hello kullanarak Hizmetleri'nde bir ayrıntılı kılavuz toohosting olan **Microsoft.ServiceFabric.AspNetCore.** * NuGet paketlerini kümesi.</span><span class="sxs-lookup"><span data-stu-id="ed43e-105">This article is an in-depth guide toohosting ASP.NET Core services in Service Fabric Reliable Services using hello **Microsoft.ServiceFabric.AspNetCore.*** set of NuGet packages.</span></span>

<span data-ttu-id="ed43e-106">Service Fabric ASP.NET çekirdek tanıtım bir öğretici ve geliştirme ortamınızı ayarlayın alma hakkında yönergeler için bkz: [bir web uygulamanız için ASP.NET Core kullanarak ön derleme](service-fabric-add-a-web-frontend.md).</span><span class="sxs-lookup"><span data-stu-id="ed43e-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment set up, see [Building a web front-end for your application using ASP.NET Core](service-fabric-add-a-web-frontend.md).</span></span>

<span data-ttu-id="ed43e-107">Merhaba, bu makalenin kalanında ile ASP.NET Core bilginiz varsayar.</span><span class="sxs-lookup"><span data-stu-id="ed43e-107">hello rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="ed43e-108">Merhaba okuma öneririz, varsa [ASP.NET Core Temelleri](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span><span class="sxs-lookup"><span data-stu-id="ed43e-108">If not, we recommend reading through hello [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-hello-service-fabric-environment"></a><span data-ttu-id="ed43e-109">ASP.NET Core hello Service Fabric ortamında</span><span class="sxs-lookup"><span data-stu-id="ed43e-109">ASP.NET Core in hello Service Fabric environment</span></span>

<span data-ttu-id="ed43e-110">ASP.NET Core uygulamaları hello tam .NET Framework, Service Fabric Hizmetleri şu anda yalnızca çalıştırabilirsiniz veya .NET Core üzerinde çalıştırmasına rağmen tam .NET Framework hello.</span><span class="sxs-lookup"><span data-stu-id="ed43e-110">While ASP.NET Core apps can run on .NET Core or on hello full .NET Framework, Service Fabric services currently can only run on hello full .NET Framework.</span></span> <span data-ttu-id="ed43e-111">Bir ASP.NET Core Service Fabric hizmeti yapılandırdığınızda Bunun anlamı, hala hedeflemelidir tam .NET Framework hello.</span><span class="sxs-lookup"><span data-stu-id="ed43e-111">This means when you build an ASP.NET  Core Service Fabric service, you must still target hello full .NET Framework.</span></span>

<span data-ttu-id="ed43e-112">ASP.NET Core Service Fabric iki farklı şekillerde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="ed43e-112">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="ed43e-113">**Bir konuk yürütülebilir dosya barındırılan**.</span><span class="sxs-lookup"><span data-stu-id="ed43e-113">**Hosted as a guest executable**.</span></span> <span data-ttu-id="ed43e-114">Birincil olarak kullanılan toorun mevcut ASP.NET Core uygulamaları Service Fabric kod değişikliğine budur.</span><span class="sxs-lookup"><span data-stu-id="ed43e-114">This is primarily used toorun existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="ed43e-115">**İçinde güvenilir bir hizmet Farklı Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="ed43e-115">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="ed43e-116">Bu, hello Service Fabric çalışma zamanı ile daha iyi tümleştirme sağlar ve durum bilgisi olan ASP.NET Core hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ed43e-116">This allows better integration with hello Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="ed43e-117">Merhaba, bu makalenin kalanında nasıl kullanarak güvenilir hizmet içinde ASP.NET Core toouse hello sevk ASP.NET Core Tümleştirme Bileşenleri hello Service Fabric SDK ile açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-117">hello rest of this article explains how toouse ASP.NET Core inside a Reliable Service using hello ASP.NET Core integration components that ship with hello Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="ed43e-118">Service Fabric hizmeti barındırma</span><span class="sxs-lookup"><span data-stu-id="ed43e-118">Service Fabric service hosting</span></span>

<span data-ttu-id="ed43e-119">Service Fabric içinde bir veya daha fazla örnekleri ve/veya hizmetinizin çoğaltmaları çalıştırmak bir *hizmet ana bilgisayar işlemi*, hizmet kodunuzun çalıştığı bir yürütülebilir dosya.</span><span class="sxs-lookup"><span data-stu-id="ed43e-119">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="ed43e-120">Kendi hizmet yazarı olarak hello hizmet ana bilgisayar işlemi ve Service Fabric etkinleştirir ve sizin için izler.</span><span class="sxs-lookup"><span data-stu-id="ed43e-120">You, as a service author, own hello service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="ed43e-121">Geleneksel ASP.NET (yukarı tooMVC 5), sıkı şekilde bağlı tooIIS System.Web.dll aracılığıyla teknolojidir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-121">Traditional ASP.NET (up tooMVC 5) is tightly coupled tooIIS through System.Web.dll.</span></span> <span data-ttu-id="ed43e-122">ASP.NET Core hello web sunucusu ve web uygulamanızı arasında ayrım sağlar.</span><span class="sxs-lookup"><span data-stu-id="ed43e-122">ASP.NET Core provides a separation between hello web server and your web application.</span></span> <span data-ttu-id="ed43e-123">Bu web uygulamaları toobe farklı web sunucuları arasında taşınabilir verir ve ayrıca web sunucuları toobe sağlar *kendi kendini barındıran*, anlamına gelir bir web sunucusu kendi işleminde adanmış web tarafından sahip olunan karşılıklı tooa işlem olarak başlatmak için IIS gibi sunucu yazılımı.</span><span class="sxs-lookup"><span data-stu-id="ed43e-123">This allows web applications toobe portable between different web servers and also allows web servers toobe *self-hosted*, which means you can start a web server in your own process, as opposed tooa process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="ed43e-124">Sipariş toocombine bir Service Fabric hizmeti ve ASP.NET, Konuk yürütülebilir dosya veya güvenilir bir hizmet, hizmet ana bilgisayar işlemi içinde mümkün toostart ASP.NET olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-124">In order toocombine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able toostart ASP.NET inside your service host process.</span></span> <span data-ttu-id="ed43e-125">Kendi kendine barındırma ASP.NET Core toodo verir bu.</span><span class="sxs-lookup"><span data-stu-id="ed43e-125">ASP.NET Core self-hosting allows you toodo this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="ed43e-126">ASP.NET Core güvenilir hizmetinde barındırma</span><span class="sxs-lookup"><span data-stu-id="ed43e-126">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="ed43e-127">Genellikle, kendi kendini barındıran ASP.NET Core uygulamaları bir WebHost hello gibi bir uygulamanın giriş noktası oluşturmak `static void Main()` yönteminde `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="ed43e-127">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as hello `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="ed43e-128">Bu durumda, hello WebHost hello yaşam döngüsü hello işleminin ilişkili toohello yaşam döngüsü ' dir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-128">In this case, hello lifecycle of hello WebHost is bound toohello lifecycle of hello process.</span></span>

![Bir işlemde ASP.NET Core barındırma][0]

<span data-ttu-id="ed43e-130">Ancak, hello uygulama giriş noktası hello doğru yerde toocreate WebHost güvenilir bir hizmet olarak değil, hello uygulama giriş noktası yalnızca kullanıldığından tooregister hizmet böylece hizmet örneklerini oluşturabilir, hello Service Fabric çalışma zamanı ile yazın yazın.</span><span class="sxs-lookup"><span data-stu-id="ed43e-130">However, hello application entry point is not hello right place toocreate a WebHost in a Reliable Service, because hello application entry point is only used tooregister a service type with hello Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="ed43e-131">Merhaba WebHost kendisini güvenilir bir hizmet olarak oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-131">hello WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="ed43e-132">Merhaba hizmet barındırma işlemi içinde birden çok yaşam döngüleri hizmet örneği ve/veya çoğaltmaları gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed43e-132">Within hello service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="ed43e-133">Bir güvenilir hizmet örneği türetme, hizmet sınıfı tarafından temsil edilen `StatelessService` veya `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="ed43e-133">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="ed43e-134">bir hizmet için Hello iletişim yığını bulunduğu bir `ICommunicationListener` hizmet sınıfınızı uygulamasında.</span><span class="sxs-lookup"><span data-stu-id="ed43e-134">hello communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="ed43e-135">Merhaba `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet paketlerini içeren uygulamaları `ICommunicationListener` başlatmak ve Kestrel ya da güvenilir bir hizmette WebListener hello ASP.NET Core WebHost yönetin.</span><span class="sxs-lookup"><span data-stu-id="ed43e-135">hello `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage hello ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![ASP.NET Core güvenilir hizmetinde barındırma][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="ed43e-137">ASP.NET Core ICommunicationListeners</span><span class="sxs-lookup"><span data-stu-id="ed43e-137">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="ed43e-138">Merhaba `ICommunicationListener` hello Kestrel ve WebListener uygulamalarında `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet paketlerini benzer kullanım desenlerini sahip ancak biraz farklı eylemler belirli tooeach web sunucu gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="ed43e-138">hello `ICommunicationListener` implementations for Kestrel and WebListener in hello  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific tooeach web server.</span></span> 

<span data-ttu-id="ed43e-139">Her iki iletişim dinleyicileri şu bağımsız hello alan bir oluşturucu sağlar:</span><span class="sxs-lookup"><span data-stu-id="ed43e-139">Both communication listeners provide a constructor that takes hello following arguments:</span></span>
 - <span data-ttu-id="ed43e-140">**`ServiceContext serviceContext`**: Merhaba `ServiceContext` hizmetini çalıştıran hello hakkında bilgi içeren nesne.</span><span class="sxs-lookup"><span data-stu-id="ed43e-140">**`ServiceContext serviceContext`**: hello `ServiceContext` object that contains information about hello running service.</span></span>
 - <span data-ttu-id="ed43e-141">**`string endpointName`**: hello adını bir `Endpoint` ServiceManifest.xml yapılandırmasında.</span><span class="sxs-lookup"><span data-stu-id="ed43e-141">**`string endpointName`**: hello name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="ed43e-142">Öncelikle burada hello iki iletişim dinleyicileri farklı budur: WebListener **gerektirir** bir `Endpoint` Kestrel çalışmazken yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="ed43e-142">This is primarily where hello two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="ed43e-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**:, oluşturduğunuz ve dönüş uygulayan bir lambda bir `IWebHost`.</span><span class="sxs-lookup"><span data-stu-id="ed43e-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="ed43e-144">Tooconfigure bu sayede `IWebHost` normalde bir ASP.NET Core uygulamada hello yolu.</span><span class="sxs-lookup"><span data-stu-id="ed43e-144">This allows you tooconfigure `IWebHost` hello way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="ed43e-145">Merhaba lambda sağlar, hello Service Fabric tümleştirme bağlı olarak, kullanım ve hello seçenekleri için oluşturulan bir URL `Endpoint` sağladığınız yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="ed43e-145">hello lambda provides a URL which is generated for you depending on hello Service Fabric integration options you use and hello `Endpoint` configuration you provide.</span></span> <span data-ttu-id="ed43e-146">URL sonra değiştirilebilir veya olarak kullanılan,-toostart hello web sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="ed43e-146">That URL can then be modified or used as-is toostart hello web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="ed43e-147">Service Fabric tümleştirme Ara</span><span class="sxs-lookup"><span data-stu-id="ed43e-147">Service Fabric integration middleware</span></span>
<span data-ttu-id="ed43e-148">Merhaba `Microsoft.ServiceFabric.Services.AspNetCore` NuGet paketi içeren hello `UseServiceFabricIntegration` genişletme yöntemi `IWebHostBuilder` , Service Fabric algılayan ara yazılımı ekler.</span><span class="sxs-lookup"><span data-stu-id="ed43e-148">hello `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes hello `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="ed43e-149">Bu ara yazılımın hello Kestrel veya WebListener yapılandırır `ICommunicationListener` benzersiz bir hizmet URL'si ile Service Fabric adlandırma hizmeti hello ve ardından doğrular tooregister istemci istekleri tooensure istemcileri toohello doğru hizmet bağlama.</span><span class="sxs-lookup"><span data-stu-id="ed43e-149">This middleware configures hello Kestrel or WebListener `ICommunicationListener` tooregister a unique service URL with hello Service Fabric Naming Service and then validates client requests tooensure clients are connecting toohello right service.</span></span> <span data-ttu-id="ed43e-150">Bu, Service Fabric, burada birden çok web uygulamaları üzerinde hello aynı fiziksel veya sanal makine çalıştırabilirsiniz ancak benzersiz ana bilgisayar adları, yanlışlıkla toohello yanlış hizmeti bağlanmasını tooprevent istemcileri kullanmayın gibi paylaşılan konak ortamında gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-150">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on hello same physical or virtual machine but do not use unique host names, tooprevent clients from mistakenly connecting toohello wrong service.</span></span> <span data-ttu-id="ed43e-151">Bu senaryo hello sonraki bölümünde daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-151">This scenario is described in more detail in hello next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="ed43e-152">Hatalı kimlik durumunun</span><span class="sxs-lookup"><span data-stu-id="ed43e-152">A case of mistaken identity</span></span>
<span data-ttu-id="ed43e-153">Hizmet çoğaltmalar, protokol, bakılmaksızın benzersiz IP: BağlantıNoktası birleşimi üzerinde dinler.</span><span class="sxs-lookup"><span data-stu-id="ed43e-153">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="ed43e-154">Bir IP: BağlantıNoktası uç noktada dinleme hizmeti çoğaltma başladıktan sonra o uç noktası adresi toohello Service Fabric adlandırma hizmeti Burada, istemciler veya diğer hizmetler tarafından keşfedilmesini bildirir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-154">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address toohello Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="ed43e-155">Aynı IP: BağlantıNoktası uç noktasını, daha önce başka bir hizmet uygulaması dinamik olarak atanan bağlantı noktaları, bir hizmet çoğaltma tesadüfen hizmetleri kullanması Merhaba, aynı fiziksel veya sanal makine hello.</span><span class="sxs-lookup"><span data-stu-id="ed43e-155">If services use dynamically-assigned application ports, a service replica may coincidentally use hello same IP:port endpoint of another service that was previously on hello same physical or virtual machine.</span></span> <span data-ttu-id="ed43e-156">Bu istemci neden toomistakely connect toohello yanlış hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ed43e-156">This can cause a client toomistakely connect toohello wrong service.</span></span> <span data-ttu-id="ed43e-157">Aşağıdaki olaylar dizisi hello oluşursa bu durum oluşabilir:</span><span class="sxs-lookup"><span data-stu-id="ed43e-157">This can happen if hello following sequence of events occur:</span></span>

 1. <span data-ttu-id="ed43e-158">Hizmeti bir HTTP üzerinden 10.0.0.1:30000 üzerinde dinler.</span><span class="sxs-lookup"><span data-stu-id="ed43e-158">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="ed43e-159">İstemci Hizmeti A çözümler ve adres 10.0.0.1:30000 alır</span><span class="sxs-lookup"><span data-stu-id="ed43e-159">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="ed43e-160">Hizmet bir tooa farklı bir düğüme taşır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-160">Service A moves tooa different node.</span></span>
 4. <span data-ttu-id="ed43e-161">Hizmet B üzerinde 10.0.0.1 yerleştirilir ve tesadüfen kullandığı aynı bağlantı noktasını 30000 hello.</span><span class="sxs-lookup"><span data-stu-id="ed43e-161">Service B is placed on 10.0.0.1 and coincidentally uses hello same port 30000.</span></span>
 5. <span data-ttu-id="ed43e-162">İstemci tooconnect tooservice bir önbelleğe alınan adresi 10.0.0.1:30000 ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-162">Client attempts tooconnect tooservice A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="ed43e-163">İstemcidir başarıyla bağlı tooservice kullanıldıklarını değil B bağlı artık toohello yanlış hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ed43e-163">Client is now successfully connected tooservice B not realizing it is connected toohello wrong service.</span></span>

<span data-ttu-id="ed43e-164">Bu hatalar zor toodiagnose olabilir rastgele zamanlarda neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-164">This can cause bugs at random times that can be difficult toodiagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="ed43e-165">Benzersiz bir hizmet URL'leri kullanma</span><span class="sxs-lookup"><span data-stu-id="ed43e-165">Using unique service URLs</span></span>
<span data-ttu-id="ed43e-166">Bu, tooprevent Hizmetleri bir uç nokta toohello benzersiz bir tanımlayıcı adlandırma hizmeti gönderin ve ardından istemci istekleri sırasında bu benzersiz tanımlayıcı doğrulamak.</span><span class="sxs-lookup"><span data-stu-id="ed43e-166">tooprevent this, services can post an endpoint toohello Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="ed43e-167">Bu, güvenilir bir saldırgan-Kiracı olmayan ortamda hizmetleri arasında İşbirlikçi bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-167">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="ed43e-168">Bu, bir kiracı tehlikeli ortamda güvenli hizmetinin kimlik doğrulaması sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="ed43e-168">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="ed43e-169">Güvenilen bir ortamda hello tarafından eklenen Ara hello `UseServiceFabricIntegration` yöntemi toohello adlandırma hizmeti gönderilen ve bu tanımlayıcı her istekte doğrular bir benzersiz tanımlayıcı toohello adresi otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="ed43e-169">In a trusted environment, hello middleware that's added by hello `UseServiceFabricIntegration` method automatically appends a unique identifier toohello address that is posted toohello Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="ed43e-170">Hello tanımlayıcı eşleşmiyorsa hello ara yazılımı hemen bir HTTP 410 kaybedildi yanıtı döndürür.</span><span class="sxs-lookup"><span data-stu-id="ed43e-170">If hello identifier does not match, hello middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="ed43e-171">Dinamik olarak atanan bir bağlantı noktası olmalısınız kullanan Hizmetleri bu ara yazılımı kullanın.</span><span class="sxs-lookup"><span data-stu-id="ed43e-171">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="ed43e-172">Sabit benzersiz bağlantı noktası kullanan hizmetler işbirlikçi ortamında bu sorun yok.</span><span class="sxs-lookup"><span data-stu-id="ed43e-172">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="ed43e-173">Sabit benzersiz bağlantı noktası genellikle istemci uygulamaları tooconnect için bilinen bir bağlantı noktasına ihtiyacınız dışarıya yönelik hizmetler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-173">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications tooconnect to.</span></span> <span data-ttu-id="ed43e-174">Örneğin, çoğu Internet'e yönelik web uygulamaları, web tarayıcısı bağlantıları için bağlantı noktası 80 veya 443 kullanır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-174">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="ed43e-175">Bu durumda, hello benzersiz tanımlayıcı etkinleştirilmemelidir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-175">In this case, hello unique identifier should not be enabled.</span></span>

<span data-ttu-id="ed43e-176">Merhaba Aşağıdaki diyagramda hello istek akışı etkin hello Ara yazılımla gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="ed43e-176">hello following diagram shows hello request flow with hello middleware enabled:</span></span>

![Service Fabric ASP.NET Core tümleştirme][2]

<span data-ttu-id="ed43e-178">Kestrel ve WebListener `ICommunicationListener` uygulamaları tam olarak hello bu mekanizması kullanır aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="ed43e-178">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly hello same way.</span></span> <span data-ttu-id="ed43e-179">WebListener dahili hello temel kullanarak benzersiz URL yollarına bağlı istekleri ayırt edebilir ancak *http.sys* işlevselliği özelliği, bağlantı noktası *değil* WebListener hellotarafındankullanılan`ICommunicationListener` uygulama, daha önce açıklanan hello senaryoda HTTP 503 ve HTTP 404 hata durum kodları neden.</span><span class="sxs-lookup"><span data-stu-id="ed43e-179">Although WebListener can internally differentiate requests based on unique URL paths using hello underlying *http.sys* port sharing feature, that functionality is *not* used by hello WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in hello scenario described earlier.</span></span> <span data-ttu-id="ed43e-180">HTTP 503 ve HTTP 404 yaygın olarak kullanılan tooindicate zaten olduğu gibi sırayla çok hello hatası istemciler toodetermine hello amacı diğer hataları zorlaştırır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-180">That in turn makes it very difficult for clients toodetermine hello intent of hello error, as HTTP 503 and HTTP 404 are already commonly used tooindicate other errors.</span></span> <span data-ttu-id="ed43e-181">Bu nedenle, hem Kestrel ve WebListener `ICommunicationListener` uygulamaları standartlaştırmak hello tarafından sağlanan hello ara yazılım üzerinde `UseServiceFabricIntegration` genişletme yöntemi istemcileri yalnızca tooperform hizmet uç noktası gerekir böylece yeniden çözümlemek HTTP 410 yanıtları eylem.</span><span class="sxs-lookup"><span data-stu-id="ed43e-181">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on hello middleware provided by hello `UseServiceFabricIntegration` extension method so that clients only need tooperform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="ed43e-182">Güvenilir hizmetler WebListener</span><span class="sxs-lookup"><span data-stu-id="ed43e-182">WebListener in Reliable Services</span></span>
<span data-ttu-id="ed43e-183">WebListener kullanılabilir güvenilir bir hizmet olarak hello içeri aktararak **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="ed43e-183">WebListener can be used in a Reliable Service by importing hello **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="ed43e-184">Bu pakette `WebListenerCommunicationListener`, uygulaması `ICommunicationListener`, sağlayan toocreate bir ASP.NET Core WebHost güvenilir bir hizmet içinde WebListener hello web sunucusu olarak kullanma.</span><span class="sxs-lookup"><span data-stu-id="ed43e-184">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you toocreate an ASP.NET Core WebHost inside a Reliable Service using WebListener as hello web server.</span></span>

<span data-ttu-id="ed43e-185">WebListener hello üzerinde oluşturulmuş [Windows HTTP sunucu API'sini](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="ed43e-185">WebListener is built on hello [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="ed43e-186">Bu hello kullanır *http.sys* IIS tooprocess HTTP tarafından kullanılan çekirdek sürücüsü ister ve bunları tooprocesses çalışan web uygulamalarını rota.</span><span class="sxs-lookup"><span data-stu-id="ed43e-186">This uses hello *http.sys* kernel driver used by IIS tooprocess HTTP requests and route them tooprocesses running web applications.</span></span> <span data-ttu-id="ed43e-187">Merhaba birden çok işlemi aynı fiziksel veya sanal makine toohost web uygulamaları üzerinde hello böylece benzersiz URL yolu veya ana bilgisayar adı tarafından disambiguated aynı bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="ed43e-187">This allows multiple processes on hello same physical or virtual machine toohost web applications on hello same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="ed43e-188">Bu özellikler hello içinde birden çok Web sitesini barındırmak için Service Fabric yararlıdır aynı küme.</span><span class="sxs-lookup"><span data-stu-id="ed43e-188">These features are useful in Service Fabric for hosting multiple websites in hello same cluster.</span></span>

<span data-ttu-id="ed43e-189">Merhaba Aşağıdaki diyagramda WebListener hello nasıl kullandığı gösterilmiştir *http.sys* bağlantı noktası paylaşımı için Windows çekirdek sürücüsü:</span><span class="sxs-lookup"><span data-stu-id="ed43e-189">hello following diagram illustrates how WebListener uses hello *http.sys* kernel driver on Windows for port sharing:</span></span>

![HTTP.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="ed43e-191">Durum bilgisiz hizmetindeki WebListener</span><span class="sxs-lookup"><span data-stu-id="ed43e-191">WebListener in a stateless service</span></span>
<span data-ttu-id="ed43e-192">toouse `WebListener` bir durum bilgisiz hizmetinde hello geçersiz kılma `CreateServiceInstanceListeners` yöntemi ve return bir `WebListenerCommunicationListener` örneği:</span><span class="sxs-lookup"><span data-stu-id="ed43e-192">toouse `WebListener` in a stateless service, override hello `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="ed43e-193">Durum bilgisi olan hizmet WebListener</span><span class="sxs-lookup"><span data-stu-id="ed43e-193">WebListener in a stateful service</span></span>

<span data-ttu-id="ed43e-194">`WebListenerCommunicationListener`şu anda durum bilgisi olan hizmetler kullanmak için tasarlanmamıştır hello temel ile son toocomplications *http.sys* bağlantı noktası özelliği paylaşma.</span><span class="sxs-lookup"><span data-stu-id="ed43e-194">`WebListenerCommunicationListener` is currently not designed for use in stateful services due toocomplications with hello underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="ed43e-195">Daha fazla bilgi için dinamik bağlantı noktası ayırma ile WebListener bölümüne aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="ed43e-195">For more information, see hello following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="ed43e-196">Durum bilgisi olan hizmetler için web sunucusu önerilen hello Kestrel olur.</span><span class="sxs-lookup"><span data-stu-id="ed43e-196">For stateful services, Kestrel is hello recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="ed43e-197">Uç nokta yapılandırması</span><span class="sxs-lookup"><span data-stu-id="ed43e-197">Endpoint configuration</span></span>

<span data-ttu-id="ed43e-198">Bir `Endpoint` hello WebListener dahil olmak üzere Windows HTTP sunucu API'sini kullanan web sunucuları için yapılandırma gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-198">An `Endpoint` configuration is required for web servers that use hello Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="ed43e-199">Hello Windows HTTP sunucu API'sini kullanan web sunucularının URL'LERİNİ ile ilk yedek gerekir *http.sys* (Bu normalde hello ile gerçekleştirilir [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) aracı).</span><span class="sxs-lookup"><span data-stu-id="ed43e-199">Web servers that use hello Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="ed43e-200">Bu eylem, Hizmetleri varsayılan olmayan yükseltilmiş ayrıcalıklar gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="ed43e-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="ed43e-201">Merhaba hello "http" veya "https" seçeneklerini `Protocol` hello özelliğinin `Endpoint` yapılandırmasında *ServiceManifest.xml* kullanılan özellikle tooinstruct hello Service Fabric çalışma zamanı tooregister URL ile*http.sys* hello kullanarak sizin adınıza [ *güçlü joker* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL öneki.</span><span class="sxs-lookup"><span data-stu-id="ed43e-201">hello "http" or "https" options for hello `Protocol` property of hello `Endpoint` configuration in *ServiceManifest.xml* are used specifically tooinstruct hello Service Fabric runtime tooregister a URL with *http.sys* on your behalf using hello [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="ed43e-202">Örneğin, tooreserve `http://+:80` bir hizmet için hello aşağıdaki yapılandırma içinde ServiceManifest.xml kullanılmalıdır:</span><span class="sxs-lookup"><span data-stu-id="ed43e-202">For example, tooreserve `http://+:80` for a service, hello following configuration should be used in ServiceManifest.xml:</span></span>

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

<span data-ttu-id="ed43e-203">Ve toohello hello uç nokta adı geçirilen `WebListenerCommunicationListener` Oluşturucusu:</span><span class="sxs-lookup"><span data-stu-id="ed43e-203">And hello endpoint name must be passed toohello `WebListenerCommunicationListener` constructor:</span></span>

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="ed43e-204">Statik bir bağlantı noktası ile WebListener kullanın</span><span class="sxs-lookup"><span data-stu-id="ed43e-204">Use WebListener with a static port</span></span>
<span data-ttu-id="ed43e-205">toouse WebListener, statik bir bağlantı noktası başlangıç bağlantı noktası numarası hello sağlamak `Endpoint` yapılandırma:</span><span class="sxs-lookup"><span data-stu-id="ed43e-205">toouse a static port with WebListener, provide hello port number in hello `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="ed43e-206">Dinamik bir bağlantı noktası ile WebListener kullanın</span><span class="sxs-lookup"><span data-stu-id="ed43e-206">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="ed43e-207">toouse WebListener, dinamik olarak atanmış bir bağlantı noktası atlayın hello `Port` hello özelliğinde `Endpoint` yapılandırma:</span><span class="sxs-lookup"><span data-stu-id="ed43e-207">toouse a dynamically assigned port with WebListener, omit hello `Port` property in hello `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="ed43e-208">Dinamik bir bağlantı noktası tarafından ayrılmış Not bir `Endpoint` yapılandırma, yalnızca bir bağlantı noktası sağlar *ana bilgisayar işlemi başına*.</span><span class="sxs-lookup"><span data-stu-id="ed43e-208">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="ed43e-209">Merhaba barındırma modeli sağlar hello barındırılan birden çok hizmet örnekleri ve/veya çoğaltmaları toobe geçerli Service Fabric aynı, her biri aynı bağlantı noktası hello ayrılmış hello paylaşacak anlamı işlemi `Endpoint` yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="ed43e-209">hello current Service Fabric hosting model allows multiple service instances and/or replicas toobe hosted in hello same process, meaning that each one will share hello same port when allocated through hello `Endpoint` configuration.</span></span> <span data-ttu-id="ed43e-210">Birden çok WebListener örnekleri hello temel kullanarak bir bağlantı noktası paylaşabilirsiniz *http.sys* özellik, ancak, bağlantı noktası tarafından desteklenmiyor `WebListenerCommunicationListener` istemci isteklerini tanıttığı toohello zorluklar son.</span><span class="sxs-lookup"><span data-stu-id="ed43e-210">Multiple WebListener instances can share a port using hello underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due toohello complications it introduces for client requests.</span></span> <span data-ttu-id="ed43e-211">Dinamik bağlantı noktası için Kestrel web sunucusu önerilen hello kullanımdır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-211">For dynamic port usage, Kestrel is hello recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="ed43e-212">Güvenilir hizmetler kestrel</span><span class="sxs-lookup"><span data-stu-id="ed43e-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="ed43e-213">Kestrel kullanılabilir güvenilir bir hizmet olarak hello içeri aktararak **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="ed43e-213">Kestrel can be used in a Reliable Service by importing hello **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="ed43e-214">Bu pakette `KestrelCommunicationListener`, uygulaması `ICommunicationListener`, sağlayan toocreate bir ASP.NET Core WebHost güvenilir bir hizmet içinde Kestrel hello web sunucusu olarak kullanma.</span><span class="sxs-lookup"><span data-stu-id="ed43e-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you toocreate an ASP.NET Core WebHost inside a Reliable Service using Kestrel as hello web server.</span></span>

<span data-ttu-id="ed43e-215">Kestrel ASP.NET Core için platformlar arası web sunucusu libuv, platformlar arası zaman uyumsuz g/ç kitaplığı dayalıdır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="ed43e-216">WebListener Kestrel merkezi endpoint Yöneticisi gibi kullanmaz *http.sys*.</span><span class="sxs-lookup"><span data-stu-id="ed43e-216">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="ed43e-217">Ve WebListener farklı olarak, birden çok işlemler arasında bağlantı noktası paylaşımı Kestrel desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="ed43e-217">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="ed43e-218">Kestrel her örneğini benzersiz bir bağlantı noktası kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-218">Each instance of Kestrel must use a unique port.</span></span>

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="ed43e-220">Durum bilgisiz hizmetindeki kestrel</span><span class="sxs-lookup"><span data-stu-id="ed43e-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="ed43e-221">toouse `Kestrel` bir durum bilgisiz hizmetinde hello geçersiz kılma `CreateServiceInstanceListeners` yöntemi ve return bir `KestrelCommunicationListener` örneği:</span><span class="sxs-lookup"><span data-stu-id="ed43e-221">toouse `Kestrel` in a stateless service, override hello `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="ed43e-222">Durum bilgisi olan hizmet kestrel</span><span class="sxs-lookup"><span data-stu-id="ed43e-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="ed43e-223">toouse `Kestrel` durum bilgisi olan bir hizmeti hello geçersiz kılma `CreateServiceReplicaListeners` yöntemi ve return bir `KestrelCommunicationListener` örneği:</span><span class="sxs-lookup"><span data-stu-id="ed43e-223">toouse `Kestrel` in a stateful service, override hello `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

<span data-ttu-id="ed43e-224">Bu örnekte, bir tek örneğini `IReliableStateManager` toohello WebHost bağımlılık ekleme kapsayıcısını sağlanır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-224">In this example, a singleton instance of `IReliableStateManager` is provided toohello WebHost dependency injection container.</span></span> <span data-ttu-id="ed43e-225">Bu kesinlikle gerekli değildir, ancak toouse tanır `IReliableStateManager` ve güvenilir koleksiyonlarda MVC denetleyici eylem yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="ed43e-225">This is not strictly necessary, but it allows you toouse `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="ed43e-226">Unutmayın bir `Endpoint` yapılandırma adı **değil** çok sağlanan`KestrelCommunicationListener` durum bilgisi olan bir hizmette.</span><span class="sxs-lookup"><span data-stu-id="ed43e-226">Note that an `Endpoint` configuration name is **not** provided too`KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="ed43e-227">Bu bölüm aşağıdaki hello daha ayrıntılı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-227">This is explained in more detail in hello following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="ed43e-228">Uç nokta yapılandırması</span><span class="sxs-lookup"><span data-stu-id="ed43e-228">Endpoint configuration</span></span>
<span data-ttu-id="ed43e-229">Bir `Endpoint` yapılandırması gerekli toouse Kestrel değil.</span><span class="sxs-lookup"><span data-stu-id="ed43e-229">An `Endpoint` configuration is not required toouse Kestrel.</span></span> 

<span data-ttu-id="ed43e-230">Kestrel basit tek başına web sunucusunun adıdır; WebListener (veya HttpListener) aksine, onu ihtiyaç duymadığı bir `Endpoint` yapılandırmasında *ServiceManifest.xml* URL kayıt önceki toostarting gerektirmediğinden.</span><span class="sxs-lookup"><span data-stu-id="ed43e-230">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior toostarting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="ed43e-231">Statik bir bağlantı noktası ile Kestrel kullanın</span><span class="sxs-lookup"><span data-stu-id="ed43e-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="ed43e-232">Statik bağlantı noktası hello yapılandırılabilir `Endpoint` ServiceManifest.xml yapılandırma Kestrel ile kullanım için.</span><span class="sxs-lookup"><span data-stu-id="ed43e-232">A static port can be configured in hello `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="ed43e-233">Bu kesinlikle gerekli olmamakla birlikte, iki olası faydaları sağlar:</span><span class="sxs-lookup"><span data-stu-id="ed43e-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="ed43e-234">Başlangıç bağlantı noktası hello uygulama bağlantı noktası aralığında uymazsa hello işletim sistemi güvenlik duvarı üzerinden Service Fabric tarafından açılmış.</span><span class="sxs-lookup"><span data-stu-id="ed43e-234">If hello port does not fall in hello application port range, it is opened through hello OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="ed43e-235">Sağlanan URL tooyou aracılığıyla hello `KestrelCommunicationListener` Bu bağlantı noktasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-235">hello URL provided tooyou through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="ed43e-236">Varsa bir `Endpoint` olan yapılandırılmış, adını hello geçirilmelidir `KestrelCommunicationListener` Oluşturucusu:</span><span class="sxs-lookup"><span data-stu-id="ed43e-236">If an `Endpoint` is configured, its name must be passed into hello `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="ed43e-237">Varsa bir `Endpoint` yapılandırması kullanılmaz, hello hello adlarında atlayın `KestrelCommunicationListener` Oluşturucusu.</span><span class="sxs-lookup"><span data-stu-id="ed43e-237">If an `Endpoint` configuration is not used, omit hello name in hello `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="ed43e-238">Bu durumda, dinamik bir bağlantı noktası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="ed43e-239">Daha fazla bilgi için Hello sonraki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="ed43e-239">See hello next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="ed43e-240">Dinamik bir bağlantı noktası ile Kestrel kullanın</span><span class="sxs-lookup"><span data-stu-id="ed43e-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="ed43e-241">Kestrel hello bir hello otomatik olarak bağlantı noktası atama kullanamaz `Endpoint` ServiceManifest.xml, yapılandırmada olduğundan otomatik olarak bağlantı noktası atama bir `Endpoint` yapılandırması atar benzersiz bir bağlantı noktası başına *ana bilgisayar işlemi* , ve tek ana bilgisayar işlemi birden çok Kestrel örnekleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-241">Kestrel cannot use hello automatic port assignment from hello `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="ed43e-242">Bağlantı noktası paylaşımı Kestrel desteklemediğinden, her Kestrel örneğini benzersiz bir bağlantı noktasında açılmalıdır gibi bu çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="ed43e-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="ed43e-243">toouse dinamik bağlantı noktası atama Kestrel ile yalnızca hello atlayın `Endpoint` ServiceManifest.xml yapılandırmasında tamamen ve bir uç nokta adı toohello geçmeyin `KestrelCommunicationListener` Oluşturucusu:</span><span class="sxs-lookup"><span data-stu-id="ed43e-243">toouse dynamic port assignment with Kestrel, simply omit hello `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name toohello `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="ed43e-244">Bu yapılandırmada, `KestrelCommunicationListener` kullanılmayan bir bağlantı noktası hello uygulama bağlantı noktası aralığından otomatik olarak seçer.</span><span class="sxs-lookup"><span data-stu-id="ed43e-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from hello application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="ed43e-245">Senaryolar ve yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="ed43e-245">Scenarios and configurations</span></span>
<span data-ttu-id="ed43e-246">Bu bölümde senaryo aşağıdaki hello açıklar ve hello düzgün çalıştığını hizmeti web sunucusu, bağlantı noktası yapılandırmasını, Service Fabric tümleştirme seçeneklerini ve çeşitli ayarları tooachieve önerilen sağlar:</span><span class="sxs-lookup"><span data-stu-id="ed43e-246">This section describes hello following scenarios and provides hello recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings tooachieve a properly functioning service:</span></span>
 - <span data-ttu-id="ed43e-247">ASP.NET Core durum bilgisiz hizmetini dışarıdan kullanıma</span><span class="sxs-lookup"><span data-stu-id="ed43e-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="ed43e-248">Yalnızca dahili ASP.NET Core durum bilgisiz hizmeti</span><span class="sxs-lookup"><span data-stu-id="ed43e-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="ed43e-249">Yalnızca dahili ASP.NET Core durum bilgisi olan hizmet</span><span class="sxs-lookup"><span data-stu-id="ed43e-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="ed43e-250">Bir **dışarıdan kullanıma sunulan** hizmetidir, genellikle bir yük dengeleyici üzerinden hello küme dışında erişilebilir bir uç noktasını kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="ed43e-250">An **externally exposed** service is one that exposes an endpoint reachable from outside hello cluster, usually through a load balancer.</span></span>

<span data-ttu-id="ed43e-251">Bir **yalnızca iç** hizmetidir biri, uç nokta yalnızca hello küme içinde erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-251">An **internal-only** service is one whose endpoint is only reachable from within hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="ed43e-252">Durum bilgisi olan hizmet uç noktaları genellikle olmamalıdır toohello Internet açık.</span><span class="sxs-lookup"><span data-stu-id="ed43e-252">Stateful service endpoints generally should not be exposed toohello Internet.</span></span> <span data-ttu-id="ed43e-253">Merhaba yük dengeleyici değil mümkün toolocate olması ve trafik toohello rota hello Azure yük dengeleyici gibi Service Fabric hizmeti çözümleme algılamadan yük dengeleyici arkasında kümelerinin oluşturulamıyor tooexpose durum bilgisi olan hizmetler olur uygun durum bilgisi olan hizmet çoğaltma.</span><span class="sxs-lookup"><span data-stu-id="ed43e-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as hello Azure Load Balancer, will be unable tooexpose stateful services because hello load balancer will not be able toolocate and route traffic toohello appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="ed43e-254">ASP.NET Core durum bilgisi olmayan hizmetler dışarıdan kullanıma</span><span class="sxs-lookup"><span data-stu-id="ed43e-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="ed43e-255">WebListener web sunucusu dış, Internet'e HTTP uç noktaları Windows kullanıma ön uç Hizmetleri için önerilen hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-255">WebListener is hello recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="ed43e-256">Saldırılara karşı daha iyi koruma sağlar ve Windows kimlik doğrulaması ve bağlantı noktası paylaşımı gibi Kestrel desteklemez özelliklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="ed43e-256">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="ed43e-257">Kestrel bir kenarı (Internet'e yönelik) sunucusu olarak şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="ed43e-257">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="ed43e-258">IIS veya Nginx gibi bir ters proxy sunucusu kullanılmalıdır toohandle trafiği genel Internet hello.</span><span class="sxs-lookup"><span data-stu-id="ed43e-258">A reverse proxy server such as IIS or Nginx must be used toohandle traffic from hello public Internet.</span></span>
 
<span data-ttu-id="ed43e-259">Ne zaman gösterilen toohello Internet, durum bilgisiz hizmeti yük dengeleyici üzerinden erişilebilen bir iyi bilinen ve kararlı uç noktası kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-259">When exposed toohello Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="ed43e-260">Bu, uygulamanızın toousers sağlayacak hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-260">This is hello URL you will provide toousers of your application.</span></span> <span data-ttu-id="ed43e-261">yapılandırma aşağıdaki hello önerilir:</span><span class="sxs-lookup"><span data-stu-id="ed43e-261">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="ed43e-262">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="ed43e-262">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed43e-263">Web sunucusu</span><span class="sxs-lookup"><span data-stu-id="ed43e-263">Web server</span></span> | <span data-ttu-id="ed43e-264">WebListener</span><span class="sxs-lookup"><span data-stu-id="ed43e-264">WebListener</span></span> | <span data-ttu-id="ed43e-265">Merhaba service yalnızca gösterilen tooa güvenilir ağ, bu tür bir intranet ise Kestrel kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-265">If hello service is only exposed tooa trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="ed43e-266">Aksi takdirde, WebListener tercih edilen hello seçenektir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-266">Otherwise, WebListener is hello preferred option.</span></span> |
| <span data-ttu-id="ed43e-267">Bağlantı noktası yapılandırması</span><span class="sxs-lookup"><span data-stu-id="ed43e-267">Port configuration</span></span> | <span data-ttu-id="ed43e-268">Statik</span><span class="sxs-lookup"><span data-stu-id="ed43e-268">static</span></span> | <span data-ttu-id="ed43e-269">İyi bilinen statik bağlantı noktası hello yapılandırılmalıdır `Endpoints` ServiceManifest.xml, yapılandırmayı 80 HTTP veya HTTPS için 443 gibi.</span><span class="sxs-lookup"><span data-stu-id="ed43e-269">A well-known static port should be configured in hello `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="ed43e-270">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="ed43e-270">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="ed43e-271">None</span><span class="sxs-lookup"><span data-stu-id="ed43e-271">None</span></span> | <span data-ttu-id="ed43e-272">Merhaba `ServiceFabricIntegrationOptions.None` hello hizmeti toovalidate gelen istekler için benzersiz bir tanımlayıcı denemez böylece Service Fabric tümleştirme Ara yapılandırırken seçeneği kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-272">hello `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that hello service does not attempt toovalidate incoming requests for a unique identifier.</span></span> <span data-ttu-id="ed43e-273">Dış kullanıcılar, uygulamanızın hello benzersiz tanımlayıcı bilgiler hello ara yazılımı tarafından kullanılan bilmez.</span><span class="sxs-lookup"><span data-stu-id="ed43e-273">External users of your application will not know hello unique identifying information used by hello middleware.</span></span> |
| <span data-ttu-id="ed43e-274">Örnek sayısı</span><span class="sxs-lookup"><span data-stu-id="ed43e-274">Instance Count</span></span> | <span data-ttu-id="ed43e-275">-1</span><span class="sxs-lookup"><span data-stu-id="ed43e-275">-1</span></span> | <span data-ttu-id="ed43e-276">Tipik kullanım durumlarında ayarı hello örnek sayısı çok ayarlanmalıdır-"1" bir örnek, bir yük dengeleyici trafiği almak tüm düğümlere kullanılabilir olmasını sağlamak.</span><span class="sxs-lookup"><span data-stu-id="ed43e-276">In typical use cases, hello instance count setting should be set too"-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="ed43e-277">Birden çok dışarıdan kullanıma sunulan hizmetler aynı düğümlerinin ayarlamak hello paylaşıyorsanız, benzersiz ancak kararlı bir URL yolu kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-277">If multiple externally exposed services share hello same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="ed43e-278">Bu, IWebHost yapılandırırken sağlanan hello URL değiştirerek gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-278">This can be accomplished by modifying hello URL provided when configuring IWebHost.</span></span> <span data-ttu-id="ed43e-279">Bu yalnızca tooWebListener geçerlidir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ed43e-279">Note this applies tooWebListener only.</span></span>

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="ed43e-280">Yalnızca dahili durum bilgisiz ASP.NET Core hizmeti</span><span class="sxs-lookup"><span data-stu-id="ed43e-280">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="ed43e-281">Yalnızca gelen hello küme içinde denir durum bilgisi olmayan hizmetler ve bağlantı noktaları tooensure işbirliği birden çok hizmetleri arasında dinamik olarak atanan benzersiz URL'leri kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="ed43e-281">Stateless services that are only called from within hello cluster should use unique URLs and dynamically assigned ports tooensure cooperation between multiple services.</span></span> <span data-ttu-id="ed43e-282">yapılandırma aşağıdaki hello önerilir:</span><span class="sxs-lookup"><span data-stu-id="ed43e-282">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="ed43e-283">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="ed43e-283">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed43e-284">Web sunucusu</span><span class="sxs-lookup"><span data-stu-id="ed43e-284">Web server</span></span> | <span data-ttu-id="ed43e-285">kestrel</span><span class="sxs-lookup"><span data-stu-id="ed43e-285">Kestrel</span></span> | <span data-ttu-id="ed43e-286">WebListener iç durum bilgisi olmayan hizmetler için kullanılabilir Kestrel hello birden çok hizmet örnekleri tooshare bir ana bilgisayar sunucusu tooallow önerilen olsa da.</span><span class="sxs-lookup"><span data-stu-id="ed43e-286">Although WebListener may be used for internal stateless services, Kestrel is hello recommended server tooallow multiple service instances tooshare a host.</span></span>  |
| <span data-ttu-id="ed43e-287">Bağlantı noktası yapılandırması</span><span class="sxs-lookup"><span data-stu-id="ed43e-287">Port configuration</span></span> | <span data-ttu-id="ed43e-288">dinamik olarak atanan</span><span class="sxs-lookup"><span data-stu-id="ed43e-288">dynamically assigned</span></span> | <span data-ttu-id="ed43e-289">Bir durum bilgisi olan hizmetin birden fazla çoğaltma bir ana bilgisayar işlemi veya ana bilgisayar işletim sistemi paylaşabilir ve bu nedenle benzersiz bağlantı noktaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-289">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="ed43e-290">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="ed43e-290">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="ed43e-291">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="ed43e-291">UseUniqueServiceUrl</span></span> | <span data-ttu-id="ed43e-292">Dinamik bağlantı noktası atama ile bu ayar daha önce açıklanan mistaken hello kimlik sorunu önler.</span><span class="sxs-lookup"><span data-stu-id="ed43e-292">With dynamic port assignment, this setting prevents hello mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="ed43e-293">Instancecount</span><span class="sxs-lookup"><span data-stu-id="ed43e-293">InstanceCount</span></span> | <span data-ttu-id="ed43e-294">tüm</span><span class="sxs-lookup"><span data-stu-id="ed43e-294">any</span></span> | <span data-ttu-id="ed43e-295">Merhaba örnek sayısı ayarını tooany değeri gerekli toooperate hello hizmet ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed43e-295">hello instance count setting can be set tooany value necessary toooperate hello service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="ed43e-296">Yalnızca dahili durum bilgisi olan ASP.NET Core hizmeti</span><span class="sxs-lookup"><span data-stu-id="ed43e-296">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="ed43e-297">Yalnızca gelen hello küme içinde denir durum bilgisi olan hizmetler birden çok hizmetleri arasında dinamik olarak atanan bağlantı noktaları tooensure işbirliği kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-297">Stateful services that are only called from within hello cluster should use dynamically assigned ports tooensure cooperation between multiple services.</span></span> <span data-ttu-id="ed43e-298">yapılandırma aşağıdaki hello önerilir:</span><span class="sxs-lookup"><span data-stu-id="ed43e-298">hello following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="ed43e-299">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="ed43e-299">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed43e-300">Web sunucusu</span><span class="sxs-lookup"><span data-stu-id="ed43e-300">Web server</span></span> | <span data-ttu-id="ed43e-301">kestrel</span><span class="sxs-lookup"><span data-stu-id="ed43e-301">Kestrel</span></span> | <span data-ttu-id="ed43e-302">Merhaba `WebListenerCommunicationListener` çoğaltmaları bir ana bilgisayar işlemi paylaşmak durum bilgisi olan hizmet tarafından kullanılmak üzere tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="ed43e-302">hello `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="ed43e-303">Bağlantı noktası yapılandırması</span><span class="sxs-lookup"><span data-stu-id="ed43e-303">Port configuration</span></span> | <span data-ttu-id="ed43e-304">dinamik olarak atanan</span><span class="sxs-lookup"><span data-stu-id="ed43e-304">dynamically assigned</span></span> | <span data-ttu-id="ed43e-305">Bir durum bilgisi olan hizmetin birden fazla çoğaltma bir ana bilgisayar işlemi veya ana bilgisayar işletim sistemi paylaşabilir ve bu nedenle benzersiz bağlantı noktaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="ed43e-305">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="ed43e-306">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="ed43e-306">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="ed43e-307">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="ed43e-307">UseUniqueServiceUrl</span></span> | <span data-ttu-id="ed43e-308">Dinamik bağlantı noktası atama ile bu ayar daha önce açıklanan mistaken hello kimlik sorunu önler.</span><span class="sxs-lookup"><span data-stu-id="ed43e-308">With dynamic port assignment, this setting prevents hello mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ed43e-309">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ed43e-309">Next steps</span></span>
[<span data-ttu-id="ed43e-310">Service Fabric uygulamanızı Visual Studio kullanarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="ed43e-310">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
