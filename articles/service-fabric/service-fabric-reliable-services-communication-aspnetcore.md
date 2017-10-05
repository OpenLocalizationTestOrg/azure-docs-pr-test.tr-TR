---
title: "Hizmet ASP.NET Core ile iletişim | Microsoft Docs"
description: "Durum bilgisiz ve durum bilgisi olan güvenilir hizmetler ASP.NET Core kullanmayı öğrenin."
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
ms.openlocfilehash: 8ac4d409f7363e8b4ae98be659a627ac8db8d787
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="a637f-103">ASP.NET çekirdek Service Fabric güvenilir hizmetler</span><span class="sxs-lookup"><span data-stu-id="a637f-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="a637f-104">ASP.NET Core modern bulut tabanlı Internet'e bağlı uygulamaları, web uygulamaları, IOT uygulamaları ve mobil arka uçlarını gibi oluşturmak için yeni bir açık kaynaklı ve çapraz platform framework kümesidir.</span><span class="sxs-lookup"><span data-stu-id="a637f-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="a637f-105">Bu makalede hizmet doku güvenilir hizmetler kullanarak ASP.NET Core hizmetlerini barındıran bir ayrıntılı kılavuzdur **Microsoft.ServiceFabric.AspNetCore.** * NuGet paketlerini kümesi.</span><span class="sxs-lookup"><span data-stu-id="a637f-105">This article is an in-depth guide to hosting ASP.NET Core services in Service Fabric Reliable Services using the **Microsoft.ServiceFabric.AspNetCore.*** set of NuGet packages.</span></span>

<span data-ttu-id="a637f-106">Service Fabric ASP.NET çekirdek tanıtım bir öğretici ve geliştirme ortamınızı ayarlayın alma hakkında yönergeler için bkz: [bir web uygulamanız için ASP.NET Core kullanarak ön derleme](service-fabric-add-a-web-frontend.md).</span><span class="sxs-lookup"><span data-stu-id="a637f-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment set up, see [Building a web front-end for your application using ASP.NET Core](service-fabric-add-a-web-frontend.md).</span></span>

<span data-ttu-id="a637f-107">Bu makalede geri kalanı ile ASP.NET Core bilginiz varsayar.</span><span class="sxs-lookup"><span data-stu-id="a637f-107">The rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="a637f-108">Okuma öneririz, varsa [ASP.NET Core Temelleri](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span><span class="sxs-lookup"><span data-stu-id="a637f-108">If not, we recommend reading through the [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-the-service-fabric-environment"></a><span data-ttu-id="a637f-109">Service Fabric ortamında ASP.NET Çekirdeği</span><span class="sxs-lookup"><span data-stu-id="a637f-109">ASP.NET Core in the Service Fabric environment</span></span>

<span data-ttu-id="a637f-110">Tam .NET Framework veya .NET Core üzerinde ASP.NET Core uygulamaları çalıştırabilirsiniz olsa da, Service Fabric Hizmetleri şu anda tam .NET Framework üzerinde yalnızca çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a637f-110">While ASP.NET Core apps can run on .NET Core or on the full .NET Framework, Service Fabric services currently can only run on the full .NET Framework.</span></span> <span data-ttu-id="a637f-111">Bunun anlamı, bir ASP.NET Core Service Fabric hizmet oluşturma sırasında tam .NET Framework hala hedeflemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a637f-111">This means when you build an ASP.NET  Core Service Fabric service, you must still target the full .NET Framework.</span></span>

<span data-ttu-id="a637f-112">ASP.NET Core Service Fabric iki farklı şekillerde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="a637f-112">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="a637f-113">**Bir konuk yürütülebilir dosya barındırılan**.</span><span class="sxs-lookup"><span data-stu-id="a637f-113">**Hosted as a guest executable**.</span></span> <span data-ttu-id="a637f-114">Bu, öncelikle hiçbir kod değişikliklerle Service Fabric mevcut ASP.NET Core uygulamaları çalıştırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a637f-114">This is primarily used to run existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="a637f-115">**İçinde güvenilir bir hizmet Farklı Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="a637f-115">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="a637f-116">Bu, Service Fabric çalışma zamanı ile daha iyi tümleştirme sağlar ve durum bilgisi olan ASP.NET Core hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="a637f-116">This allows better integration with the Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="a637f-117">Bu makalenin geri kalanında, ASP.NET Core güvenilir bir Service Fabric SDK ile birlikte gelen ASP.NET Core tümleştirme bileşenlerini kullanarak hizmet içinde kullanımı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a637f-117">The rest of this article explains how to use ASP.NET Core inside a Reliable Service using the ASP.NET Core integration components that ship with the Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="a637f-118">Service Fabric hizmeti barındırma</span><span class="sxs-lookup"><span data-stu-id="a637f-118">Service Fabric service hosting</span></span>

<span data-ttu-id="a637f-119">Service Fabric içinde bir veya daha fazla örnekleri ve/veya hizmetinizin çoğaltmaları çalıştırmak bir *hizmet ana bilgisayar işlemi*, hizmet kodunuzun çalıştığı bir yürütülebilir dosya.</span><span class="sxs-lookup"><span data-stu-id="a637f-119">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="a637f-120">Kendi hizmet yazar olarak, hizmet ana bilgisayar işlemi ve Service Fabric etkinleştirir ve sizin için izler.</span><span class="sxs-lookup"><span data-stu-id="a637f-120">You, as a service author, own the service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="a637f-121">(En fazla MVC 5) geleneksel ASP.NET IIS System.Web.dll aracılığıyla sıkı şekilde bağlı.</span><span class="sxs-lookup"><span data-stu-id="a637f-121">Traditional ASP.NET (up to MVC 5) is tightly coupled to IIS through System.Web.dll.</span></span> <span data-ttu-id="a637f-122">ASP.NET çekirdek web sunucusu ve web uygulamanızı arasında ayrım sağlar.</span><span class="sxs-lookup"><span data-stu-id="a637f-122">ASP.NET Core provides a separation between the web server and your web application.</span></span> <span data-ttu-id="a637f-123">Bu web uygulamaları farklı web sunucuları arasında taşınabilir olmasını sağlar ve ayrıca web sunucularının sağlar *kendi kendini barındıran*, ayrılmış IIS gibi web sunucusu yazılımı anlamına gelir, bir web sunucusu tarafından sahip olunan bir işlem aksine, kendi işleminde başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a637f-123">This allows web applications to be portable between different web servers and also allows web servers to be *self-hosted*, which means you can start a web server in your own process, as opposed to a process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="a637f-124">Service Fabric hizmeti ve ASP.NET, bir konuk yürütülebilir dosya veya güvenilir bir hizmette birleştirmek için hizmet ana bilgisayar işlemi içinde ASP.NET başlatılamaz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a637f-124">In order to combine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able to start ASP.NET inside your service host process.</span></span> <span data-ttu-id="a637f-125">Kendi kendine barındırma ASP.NET Core, bunu yapmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a637f-125">ASP.NET Core self-hosting allows you to do this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="a637f-126">ASP.NET Core güvenilir hizmetinde barındırma</span><span class="sxs-lookup"><span data-stu-id="a637f-126">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="a637f-127">Genellikle, kendi kendini barındıran ASP.NET Core uygulamaları bir WebHost uygulamanın giriş noktası gibi oluşturmasına `static void Main()` yönteminde `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="a637f-127">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as the `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="a637f-128">Bu durumda, WebHost yaşam döngüsü işlemi yaşam döngüsü için bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a637f-128">In this case, the lifecycle of the WebHost is bound to the lifecycle of the process.</span></span>

![Bir işlemde ASP.NET Core barındırma][0]

<span data-ttu-id="a637f-130">Bu hizmet türünün örneklerini oluşturabilir böylece uygulama giriş noktası yalnızca bir hizmet türünün Service Fabric çalışma zamanı ile kaydetmek için kullanıldığından ancak, uygulama giriş noktası bir WebHost güvenilir bir hizmet oluşturmak için doğru yerde değil.</span><span class="sxs-lookup"><span data-stu-id="a637f-130">However, the application entry point is not the right place to create a WebHost in a Reliable Service, because the application entry point is only used to register a service type with the Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="a637f-131">WebHost kendisini güvenilir bir hizmet olarak oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a637f-131">The WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="a637f-132">Hizmet barındırma işlemi içinde birden çok yaşam döngüleri hizmet örneği ve/veya çoğaltmaları gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a637f-132">Within the service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="a637f-133">Bir güvenilir hizmet örneği türetme, hizmet sınıfı tarafından temsil edilen `StatelessService` veya `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="a637f-133">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="a637f-134">Bir hizmet için iletişim yığını bulunan bir `ICommunicationListener` hizmet sınıfınızı uygulamasında.</span><span class="sxs-lookup"><span data-stu-id="a637f-134">The communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="a637f-135">`Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet paketlerini içeren uygulamaları `ICommunicationListener` başlatın ve ASP.NET Core WebHost Kestrel ya da güvenilir bir hizmette WebListener yönetin.</span><span class="sxs-lookup"><span data-stu-id="a637f-135">The `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage the ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![ASP.NET Core güvenilir hizmetinde barındırma][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="a637f-137">ASP.NET Core ICommunicationListeners</span><span class="sxs-lookup"><span data-stu-id="a637f-137">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="a637f-138">`ICommunicationListener` Kestrel ve WebListener içinde için uygulamaları `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet paketlerini benzer kullanım desenlerini sahip ancak her web sunucusuna belirli biraz farklı eylemleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="a637f-138">The `ICommunicationListener` implementations for Kestrel and WebListener in the  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific to each web server.</span></span> 

<span data-ttu-id="a637f-139">Her iki iletişim dinleyicileri şu bağımsız değişkenleri alan bir oluşturucu sağlar:</span><span class="sxs-lookup"><span data-stu-id="a637f-139">Both communication listeners provide a constructor that takes the following arguments:</span></span>
 - <span data-ttu-id="a637f-140">**`ServiceContext serviceContext`**`ServiceContext` Çalışan hizmeti hakkında bilgi içeren nesne.</span><span class="sxs-lookup"><span data-stu-id="a637f-140">**`ServiceContext serviceContext`**: The `ServiceContext` object that contains information about the running service.</span></span>
 - <span data-ttu-id="a637f-141">**`string endpointName`**: adını bir `Endpoint` ServiceManifest.xml yapılandırmasında.</span><span class="sxs-lookup"><span data-stu-id="a637f-141">**`string endpointName`**: the name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="a637f-142">Burada iki iletişim dinleyicileri farklı budur öncelikle: WebListener **gerektirir** bir `Endpoint` Kestrel çalışmazken yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="a637f-142">This is primarily where the two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="a637f-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**:, oluşturduğunuz ve dönüş uygulayan bir lambda bir `IWebHost`.</span><span class="sxs-lookup"><span data-stu-id="a637f-143">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="a637f-144">Bu sayede yapılandırmak `IWebHost` ASP.NET Core uygulamada normalde olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="a637f-144">This allows you to configure `IWebHost` the way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="a637f-145">Service Fabric tümleştirme bağlı olarak, seçeneklerini için oluşturulan bir URL kullanın lambda sağlar ve `Endpoint` sağladığınız yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="a637f-145">The lambda provides a URL which is generated for you depending on the Service Fabric integration options you use and the `Endpoint` configuration you provide.</span></span> <span data-ttu-id="a637f-146">URL sonra değiştirilebilir veya olarak kullanılan olduğunu-web sunucusu başlatmaktır.</span><span class="sxs-lookup"><span data-stu-id="a637f-146">That URL can then be modified or used as-is to start the web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="a637f-147">Service Fabric tümleştirme Ara</span><span class="sxs-lookup"><span data-stu-id="a637f-147">Service Fabric integration middleware</span></span>
<span data-ttu-id="a637f-148">`Microsoft.ServiceFabric.Services.AspNetCore` NuGet paketini içeren `UseServiceFabricIntegration` genişletme yöntemi `IWebHostBuilder` , Service Fabric algılayan ara yazılımı ekler.</span><span class="sxs-lookup"><span data-stu-id="a637f-148">The `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes the `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="a637f-149">Bu ara yazılımın Kestrel veya WebListener yapılandırır `ICommunicationListener` Service Fabric adlandırma hizmeti benzersiz bir hizmet URL'si için ve istemciler doğru hizmete bağlanırken emin olmak için istemci istekleri doğrular.</span><span class="sxs-lookup"><span data-stu-id="a637f-149">This middleware configures the Kestrel or WebListener `ICommunicationListener` to register a unique service URL with the Service Fabric Naming Service and then validates client requests to ensure clients are connecting to the right service.</span></span> <span data-ttu-id="a637f-150">Bu, Service Fabric, birden çok web uygulamaları burada aynı fiziksel veya sanal makine üzerinde çalıştırabilirsiniz ancak istemciler yanlışlıkla yanlış hizmete bağlanmasını önlemek için benzersiz bir ana bilgisayar adları kullanmayın gibi paylaşılan konak ortamında gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a637f-150">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on the same physical or virtual machine but do not use unique host names, to prevent clients from mistakenly connecting to the wrong service.</span></span> <span data-ttu-id="a637f-151">Bu senaryo, sonraki bölümde daha ayrıntılı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a637f-151">This scenario is described in more detail in the next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="a637f-152">Hatalı kimlik durumunun</span><span class="sxs-lookup"><span data-stu-id="a637f-152">A case of mistaken identity</span></span>
<span data-ttu-id="a637f-153">Hizmet çoğaltmalar, protokol, bakılmaksızın benzersiz IP: BağlantıNoktası birleşimi üzerinde dinler.</span><span class="sxs-lookup"><span data-stu-id="a637f-153">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="a637f-154">Bir IP: BağlantıNoktası uç noktada dinleme hizmeti çoğaltma başladıktan sonra o uç noktası adresi Service Fabric adlandırma Burada, istemciler veya diğer hizmetler tarafından keşfedilmesini hizmeti bildirir.</span><span class="sxs-lookup"><span data-stu-id="a637f-154">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address to the Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="a637f-155">Hizmet uygulaması dinamik olarak atanan bağlantı noktası kullanıyorsanız, bir hizmet çoğaltma tesadüfen aynı fiziksel veya sanal makine üzerinde öncekinden başka bir hizmet aynı IP: BağlantıNoktası uç noktası kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="a637f-155">If services use dynamically-assigned application ports, a service replica may coincidentally use the same IP:port endpoint of another service that was previously on the same physical or virtual machine.</span></span> <span data-ttu-id="a637f-156">Bu bir istemciye mistakely neden yanlış hizmetine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="a637f-156">This can cause a client to mistakely connect to the wrong service.</span></span> <span data-ttu-id="a637f-157">Aşağıdaki olaylar dizisi oluşursa bu durum oluşabilir:</span><span class="sxs-lookup"><span data-stu-id="a637f-157">This can happen if the following sequence of events occur:</span></span>

 1. <span data-ttu-id="a637f-158">Hizmeti bir HTTP üzerinden 10.0.0.1:30000 üzerinde dinler.</span><span class="sxs-lookup"><span data-stu-id="a637f-158">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="a637f-159">İstemci Hizmeti A çözümler ve adres 10.0.0.1:30000 alır</span><span class="sxs-lookup"><span data-stu-id="a637f-159">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="a637f-160">Bir hizmet farklı bir düğüme taşır.</span><span class="sxs-lookup"><span data-stu-id="a637f-160">Service A moves to a different node.</span></span>
 4. <span data-ttu-id="a637f-161">Hizmet B üzerinde 10.0.0.1 yerleştirilir ve tesadüfen 30000 aynı bağlantı noktasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="a637f-161">Service B is placed on 10.0.0.1 and coincidentally uses the same port 30000.</span></span>
 5. <span data-ttu-id="a637f-162">İstemci, hizmet bir önbelleğe alınan adresi 10.0.0.1:30000 ile bağlanmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="a637f-162">Client attempts to connect to service A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="a637f-163">İstemci şimdi kullanıldıklarını değil B yanlış hizmete bağlı hizmetine başarıyla bağlandı.</span><span class="sxs-lookup"><span data-stu-id="a637f-163">Client is now successfully connected to service B not realizing it is connected to the wrong service.</span></span>

<span data-ttu-id="a637f-164">Bu hataları tanılamak zor olabilir rastgele zamanlarda neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="a637f-164">This can cause bugs at random times that can be difficult to diagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="a637f-165">Benzersiz bir hizmet URL'leri kullanma</span><span class="sxs-lookup"><span data-stu-id="a637f-165">Using unique service URLs</span></span>
<span data-ttu-id="a637f-166">Bunu önlemek için hizmetleri benzersiz bir tanımlayıcı adlandırma hizmeti için bir uç nokta sonrası ve ardından istemci istekleri sırasında bu benzersiz tanımlayıcı doğrulamak.</span><span class="sxs-lookup"><span data-stu-id="a637f-166">To prevent this, services can post an endpoint to the Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="a637f-167">Bu, güvenilir bir saldırgan-Kiracı olmayan ortamda hizmetleri arasında İşbirlikçi bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="a637f-167">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="a637f-168">Bu, bir kiracı tehlikeli ortamda güvenli hizmetinin kimlik doğrulaması sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="a637f-168">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="a637f-169">Ara yazılım tarafından eklenen güvenilir bir ortamda `UseServiceFabricIntegration` yöntemi otomatik olarak ekler benzersiz bir tanımlayıcı adlandırma hizmete gönderilen ve bu tanımlayıcı her istekte doğrular adresine.</span><span class="sxs-lookup"><span data-stu-id="a637f-169">In a trusted environment, the middleware that's added by the `UseServiceFabricIntegration` method automatically appends a unique identifier to the address that is posted to the Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="a637f-170">Tanımlayıcı eşleşmiyorsa, ara yazılım hemen bir HTTP 410 kaybedildi yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="a637f-170">If the identifier does not match, the middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="a637f-171">Dinamik olarak atanan bir bağlantı noktası olmalısınız kullanan Hizmetleri bu ara yazılımı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a637f-171">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="a637f-172">Sabit benzersiz bağlantı noktası kullanan hizmetler işbirlikçi ortamında bu sorun yok.</span><span class="sxs-lookup"><span data-stu-id="a637f-172">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="a637f-173">Sabit benzersiz bağlantı noktası tipik olarak bilinen bir bağlantı noktasına bağlanmak istemci uygulamaları için gereken dışarıya yönelik hizmetler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a637f-173">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications to connect to.</span></span> <span data-ttu-id="a637f-174">Örneğin, çoğu Internet'e yönelik web uygulamaları, web tarayıcısı bağlantıları için bağlantı noktası 80 veya 443 kullanır.</span><span class="sxs-lookup"><span data-stu-id="a637f-174">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="a637f-175">Bu durumda, benzersiz tanımlayıcı etkinleştirilmemelidir.</span><span class="sxs-lookup"><span data-stu-id="a637f-175">In this case, the unique identifier should not be enabled.</span></span>

<span data-ttu-id="a637f-176">Aşağıdaki diyagramda istek akışı etkin Ara yazılımla gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="a637f-176">The following diagram shows the request flow with the middleware enabled:</span></span>

![Service Fabric ASP.NET Core tümleştirme][2]

<span data-ttu-id="a637f-178">Kestrel ve WebListener `ICommunicationListener` uygulamaları tam olarak aynı şekilde bu mekanizması kullanır.</span><span class="sxs-lookup"><span data-stu-id="a637f-178">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly the same way.</span></span> <span data-ttu-id="a637f-179">WebListener dahili arka plandaki kullanarak benzersiz URL yollarına bağlı istekleri ayırt edebilir ancak *http.sys* işlevselliği özelliği, bağlantı noktası *değil* WebListener tarafından kullanılan `ICommunicationListener` uygulama, daha önce açıklanan senaryo HTTP 503 ve HTTP 404 hata durum kodları neden.</span><span class="sxs-lookup"><span data-stu-id="a637f-179">Although WebListener can internally differentiate requests based on unique URL paths using the underlying *http.sys* port sharing feature, that functionality is *not* used by the WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in the scenario described earlier.</span></span> <span data-ttu-id="a637f-180">HTTP 503 ve HTTP 404 zaten genellikle diğer hataları belirtmek için kullanılan gibi sırayla çok hata amacı belirlemek istemcileri zorlaştırır.</span><span class="sxs-lookup"><span data-stu-id="a637f-180">That in turn makes it very difficult for clients to determine the intent of the error, as HTTP 503 and HTTP 404 are already commonly used to indicate other errors.</span></span> <span data-ttu-id="a637f-181">Bu nedenle, hem Kestrel ve WebListener `ICommunicationListener` uygulamaları standartlaştırmak tarafından sağlanan ara yazılım üzerinde `UseServiceFabricIntegration` genişletme yöntemi istemcileri yalnızca gerçekleştirmeniz gerekir böylece hizmet uç noktası yeniden çözümlemek HTTP 410 yanıtları eylem.</span><span class="sxs-lookup"><span data-stu-id="a637f-181">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on the middleware provided by the `UseServiceFabricIntegration` extension method so that clients only need to perform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="a637f-182">Güvenilir hizmetler WebListener</span><span class="sxs-lookup"><span data-stu-id="a637f-182">WebListener in Reliable Services</span></span>
<span data-ttu-id="a637f-183">WebListener kullanılabilir güvenilir hizmetinde içeri aktararak **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="a637f-183">WebListener can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="a637f-184">Bu pakette `WebListenerCommunicationListener`, uygulaması `ICommunicationListener`, sağlayan bir ASP.NET Core WebHost içinde güvenilir bir hizmet oluşturmak web sunucusu olarak WebListener kullanarak.</span><span class="sxs-lookup"><span data-stu-id="a637f-184">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using WebListener as the web server.</span></span>

<span data-ttu-id="a637f-185">WebListener üzerinde oluşturulan [Windows HTTP sunucu API'sini](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="a637f-185">WebListener is built on the [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="a637f-186">Bu kullanır *http.sys* HTTP isteklerini işleyen ve web uygulamaları çalışan işlemler için yönlendirmek için IIS tarafından kullanılan çekirdek sürücüsü.</span><span class="sxs-lookup"><span data-stu-id="a637f-186">This uses the *http.sys* kernel driver used by IIS to process HTTP requests and route them to processes running web applications.</span></span> <span data-ttu-id="a637f-187">Bu, aynı fiziksel veya sanal makinenize benzersiz URL yolu veya ana bilgisayar adı tarafından disambiguated web uygulamalarını barındırmasını aynı bağlantı noktasında birden çok işlem sağlar.</span><span class="sxs-lookup"><span data-stu-id="a637f-187">This allows multiple processes on the same physical or virtual machine to host web applications on the same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="a637f-188">Bu özellikler aynı kümedeki birden çok Web sitesini barındırmak için Service Fabric yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="a637f-188">These features are useful in Service Fabric for hosting multiple websites in the same cluster.</span></span>

<span data-ttu-id="a637f-189">Aşağıdaki diyagram WebListener nasıl kullandığını gösterir *http.sys* bağlantı noktası paylaşımı için Windows çekirdek sürücüsü:</span><span class="sxs-lookup"><span data-stu-id="a637f-189">The following diagram illustrates how WebListener uses the *http.sys* kernel driver on Windows for port sharing:</span></span>

![HTTP.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="a637f-191">Durum bilgisiz hizmetindeki WebListener</span><span class="sxs-lookup"><span data-stu-id="a637f-191">WebListener in a stateless service</span></span>
<span data-ttu-id="a637f-192">Kullanılacak `WebListener` durum bilgisiz hizmetinde, geçersiz kılma `CreateServiceInstanceListeners` yöntemi ve return bir `WebListenerCommunicationListener` örneği:</span><span class="sxs-lookup"><span data-stu-id="a637f-192">To use `WebListener` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

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

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="a637f-193">Durum bilgisi olan hizmet WebListener</span><span class="sxs-lookup"><span data-stu-id="a637f-193">WebListener in a stateful service</span></span>

<span data-ttu-id="a637f-194">`WebListenerCommunicationListener`şu anda arka plandaki ile zorluklar nedeniyle durum bilgisi olan hizmetler kullanmak için tasarlanmamıştır *http.sys* bağlantı noktası özelliği paylaşma.</span><span class="sxs-lookup"><span data-stu-id="a637f-194">`WebListenerCommunicationListener` is currently not designed for use in stateful services due to complications with the underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="a637f-195">Daha fazla bilgi için aşağıdaki bölümde WebListener ile dinamik bağlantı noktası ayırma bakın.</span><span class="sxs-lookup"><span data-stu-id="a637f-195">For more information, see the following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="a637f-196">Durum bilgisi olan hizmetler için Kestrel önerilen web sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="a637f-196">For stateful services, Kestrel is the recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="a637f-197">Uç nokta yapılandırması</span><span class="sxs-lookup"><span data-stu-id="a637f-197">Endpoint configuration</span></span>

<span data-ttu-id="a637f-198">Bir `Endpoint` Windows HTTP sunucu WebListener dahil olmak üzere API kullanan web sunucuları için yapılandırma gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a637f-198">An `Endpoint` configuration is required for web servers that use the Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="a637f-199">Windows HTTP sunucu API'si kullanan web sunucularının URL'LERİNİ ile ilk yedek gerekir *http.sys* (Bu normalde ile gerçekleştirilir [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) aracı).</span><span class="sxs-lookup"><span data-stu-id="a637f-199">Web servers that use the Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with the [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="a637f-200">Bu eylem, Hizmetleri varsayılan olmayan yükseltilmiş ayrıcalıklar gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="a637f-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="a637f-201">"Http" veya "https" seçeneklerini `Protocol` özelliği `Endpoint` yapılandırmasında *ServiceManifest.xml* özellikle bir URL ile kaydetmek için Service Fabric çalışma zamanını istemek için kullanılan *http.sys* adına kullanma [ *güçlü joker* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL öneki.</span><span class="sxs-lookup"><span data-stu-id="a637f-201">The "http" or "https" options for the `Protocol` property of the `Endpoint` configuration in *ServiceManifest.xml* are used specifically to instruct the Service Fabric runtime to register a URL with *http.sys* on your behalf using the [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="a637f-202">Örneğin, ayırmak için `http://+:80` bir hizmet için aşağıdaki yapılandırma içinde ServiceManifest.xml kullanılmalıdır:</span><span class="sxs-lookup"><span data-stu-id="a637f-202">For example, to reserve `http://+:80` for a service, the following configuration should be used in ServiceManifest.xml:</span></span>

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

<span data-ttu-id="a637f-203">Ve uç nokta adı için geçirilmelidir `WebListenerCommunicationListener` Oluşturucusu:</span><span class="sxs-lookup"><span data-stu-id="a637f-203">And the endpoint name must be passed to the `WebListenerCommunicationListener` constructor:</span></span>

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

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="a637f-204">Statik bir bağlantı noktası ile WebListener kullanın</span><span class="sxs-lookup"><span data-stu-id="a637f-204">Use WebListener with a static port</span></span>
<span data-ttu-id="a637f-205">Statik bağlantı noktası WebListener ile kullanmak için bağlantı noktası numarası sağlayın `Endpoint` yapılandırma:</span><span class="sxs-lookup"><span data-stu-id="a637f-205">To use a static port with WebListener, provide the port number in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="a637f-206">Dinamik bir bağlantı noktası ile WebListener kullanın</span><span class="sxs-lookup"><span data-stu-id="a637f-206">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="a637f-207">Dinamik olarak atanan bir bağlantı noktasının WebListener ile kullanmak için atlayın `Port` özelliğinde `Endpoint` yapılandırma:</span><span class="sxs-lookup"><span data-stu-id="a637f-207">To use a dynamically assigned port with WebListener, omit the `Port` property in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="a637f-208">Dinamik bir bağlantı noktası tarafından ayrılmış Not bir `Endpoint` yapılandırma, yalnızca bir bağlantı noktası sağlar *ana bilgisayar işlemi başına*.</span><span class="sxs-lookup"><span data-stu-id="a637f-208">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="a637f-209">Geçerli Service Fabric barındırma modeli birden fazla hizmet örneği ve/veya çoğaltmaların her biri aracılığıyla ayrılmış aynı bağlantı noktasını paylaşmak anlamına gelir aynı işlemde barındırılan verir `Endpoint` yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="a637f-209">The current Service Fabric hosting model allows multiple service instances and/or replicas to be hosted in the same process, meaning that each one will share the same port when allocated through the `Endpoint` configuration.</span></span> <span data-ttu-id="a637f-210">Birden çok WebListener örneği arka plandaki kullanarak bir bağlantı noktası paylaşabilirsiniz *http.sys* özellik, ancak, bağlantı noktası tarafından desteklenmiyor `WebListenerCommunicationListener` istemci isteklerini tanıttığı zorluklar nedeniyle.</span><span class="sxs-lookup"><span data-stu-id="a637f-210">Multiple WebListener instances can share a port using the underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due to the complications it introduces for client requests.</span></span> <span data-ttu-id="a637f-211">Dinamik bağlantı noktası kullanım için Kestrel önerilen web sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="a637f-211">For dynamic port usage, Kestrel is the recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="a637f-212">Güvenilir hizmetler kestrel</span><span class="sxs-lookup"><span data-stu-id="a637f-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="a637f-213">Kestrel kullanılabilir güvenilir hizmetinde içeri aktararak **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="a637f-213">Kestrel can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="a637f-214">Bu pakette `KestrelCommunicationListener`, uygulaması `ICommunicationListener`, sağlayan bir ASP.NET Core WebHost içinde güvenilir bir hizmet oluşturmak web sunucusu olarak Kestrel kullanarak.</span><span class="sxs-lookup"><span data-stu-id="a637f-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using Kestrel as the web server.</span></span>

<span data-ttu-id="a637f-215">Kestrel ASP.NET Core için platformlar arası web sunucusu libuv, platformlar arası zaman uyumsuz g/ç kitaplığı dayalıdır.</span><span class="sxs-lookup"><span data-stu-id="a637f-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="a637f-216">WebListener Kestrel merkezi endpoint Yöneticisi gibi kullanmaz *http.sys*.</span><span class="sxs-lookup"><span data-stu-id="a637f-216">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="a637f-217">Ve WebListener farklı olarak, birden çok işlemler arasında bağlantı noktası paylaşımı Kestrel desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="a637f-217">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="a637f-218">Kestrel her örneğini benzersiz bir bağlantı noktası kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a637f-218">Each instance of Kestrel must use a unique port.</span></span>

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="a637f-220">Durum bilgisiz hizmetindeki kestrel</span><span class="sxs-lookup"><span data-stu-id="a637f-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="a637f-221">Kullanılacak `Kestrel` durum bilgisiz hizmetinde, geçersiz kılma `CreateServiceInstanceListeners` yöntemi ve return bir `KestrelCommunicationListener` örneği:</span><span class="sxs-lookup"><span data-stu-id="a637f-221">To use `Kestrel` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

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

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="a637f-222">Durum bilgisi olan hizmet kestrel</span><span class="sxs-lookup"><span data-stu-id="a637f-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="a637f-223">Kullanılacak `Kestrel` durum bilgisi olan bir hizmeti geçersiz kılma `CreateServiceReplicaListeners` yöntemi ve return bir `KestrelCommunicationListener` örneği:</span><span class="sxs-lookup"><span data-stu-id="a637f-223">To use `Kestrel` in a stateful service, override the `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

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

<span data-ttu-id="a637f-224">Bu örnekte, bir tek örneğini `IReliableStateManager` WebHost bağımlılık ekleme kapsayıcısına sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a637f-224">In this example, a singleton instance of `IReliableStateManager` is provided to the WebHost dependency injection container.</span></span> <span data-ttu-id="a637f-225">Bu kesinlikle gerekli değildir, ancak kullanmanıza olanak tanır `IReliableStateManager` ve güvenilir koleksiyonlarda MVC denetleyici eylem yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="a637f-225">This is not strictly necessary, but it allows you to use `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="a637f-226">Unutmayın bir `Endpoint` yapılandırma adı **değil** için sağlanan `KestrelCommunicationListener` durum bilgisi olan bir hizmette.</span><span class="sxs-lookup"><span data-stu-id="a637f-226">Note that an `Endpoint` configuration name is **not** provided to `KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="a637f-227">Bu aşağıdaki bölümünde daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a637f-227">This is explained in more detail in the following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="a637f-228">Uç nokta yapılandırması</span><span class="sxs-lookup"><span data-stu-id="a637f-228">Endpoint configuration</span></span>
<span data-ttu-id="a637f-229">Bir `Endpoint` yapılandırma Kestrel kullanmak için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="a637f-229">An `Endpoint` configuration is not required to use Kestrel.</span></span> 

<span data-ttu-id="a637f-230">Kestrel basit tek başına web sunucusunun adıdır; WebListener (veya HttpListener) aksine, onu ihtiyaç duymadığı bir `Endpoint` yapılandırmasında *ServiceManifest.xml* başlatmadan önce URL kayıt gerektirmediğinden.</span><span class="sxs-lookup"><span data-stu-id="a637f-230">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior to starting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="a637f-231">Statik bir bağlantı noktası ile Kestrel kullanın</span><span class="sxs-lookup"><span data-stu-id="a637f-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="a637f-232">Statik bağlantı noktası yapılandırılabilir `Endpoint` ServiceManifest.xml yapılandırma Kestrel ile kullanım için.</span><span class="sxs-lookup"><span data-stu-id="a637f-232">A static port can be configured in the `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="a637f-233">Bu kesinlikle gerekli olmamakla birlikte, iki olası faydaları sağlar:</span><span class="sxs-lookup"><span data-stu-id="a637f-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="a637f-234">Bağlantı noktası uygulama bağlantı noktası aralığı içinde uymazsa, işletim sistemi güvenlik duvarı üzerinden Service Fabric tarafından açılmış.</span><span class="sxs-lookup"><span data-stu-id="a637f-234">If the port does not fall in the application port range, it is opened through the OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="a637f-235">Size sağlanan URL `KestrelCommunicationListener` Bu bağlantı noktasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="a637f-235">The URL provided to you through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="a637f-236">Varsa bir `Endpoint` olan yapılandırılmış, adını içine geçirilmelidir `KestrelCommunicationListener` Oluşturucusu:</span><span class="sxs-lookup"><span data-stu-id="a637f-236">If an `Endpoint` is configured, its name must be passed into the `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="a637f-237">Varsa bir `Endpoint` yapılandırması kullanılmaz, adını atla `KestrelCommunicationListener` Oluşturucusu.</span><span class="sxs-lookup"><span data-stu-id="a637f-237">If an `Endpoint` configuration is not used, omit the name in the `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="a637f-238">Bu durumda, dinamik bir bağlantı noktası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a637f-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="a637f-239">Daha fazla bilgi için sonraki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="a637f-239">See the next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="a637f-240">Dinamik bir bağlantı noktası ile Kestrel kullanın</span><span class="sxs-lookup"><span data-stu-id="a637f-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="a637f-241">Kestrel gelen otomatik olarak bağlantı noktası atamasını kullanamaz `Endpoint` ServiceManifest.xml, yapılandırmada olduğundan otomatik olarak bağlantı noktası atama bir `Endpoint` yapılandırması atar benzersiz bir bağlantı noktası başına *ana bilgisayar işlemi*, ve tek ana bilgisayar işlemi birden çok Kestrel örnekleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a637f-241">Kestrel cannot use the automatic port assignment from the `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="a637f-242">Bağlantı noktası paylaşımı Kestrel desteklemediğinden, her Kestrel örneğini benzersiz bir bağlantı noktasında açılmalıdır gibi bu çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="a637f-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="a637f-243">Dinamik bağlantı noktası atama Kestrel ile kullanmak için yalnızca atlayın `Endpoint` ServiceManifest.xml yapılandırmasında tamamen ve bir uç nokta adı geçmeyin `KestrelCommunicationListener` Oluşturucusu:</span><span class="sxs-lookup"><span data-stu-id="a637f-243">To use dynamic port assignment with Kestrel, simply omit the `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name to the `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="a637f-244">Bu yapılandırmada, `KestrelCommunicationListener` kullanılmayan bir bağlantı noktası uygulama bağlantı noktası aralığından otomatik olarak seçer.</span><span class="sxs-lookup"><span data-stu-id="a637f-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from the application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="a637f-245">Senaryolar ve yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="a637f-245">Scenarios and configurations</span></span>
<span data-ttu-id="a637f-246">Bu bölümde aşağıdaki senaryoları açıklar ve web sunucusu, bağlantı noktası yapılandırmasını, Service Fabric tümleştirme seçeneklerini ve çeşitli ayarları düzgün çalışan bir hizmet elde etmek için önerilen birleşimi sağlar:</span><span class="sxs-lookup"><span data-stu-id="a637f-246">This section describes the following scenarios and provides the recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings to achieve a properly functioning service:</span></span>
 - <span data-ttu-id="a637f-247">ASP.NET Core durum bilgisiz hizmetini dışarıdan kullanıma</span><span class="sxs-lookup"><span data-stu-id="a637f-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="a637f-248">Yalnızca dahili ASP.NET Core durum bilgisiz hizmeti</span><span class="sxs-lookup"><span data-stu-id="a637f-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="a637f-249">Yalnızca dahili ASP.NET Core durum bilgisi olan hizmet</span><span class="sxs-lookup"><span data-stu-id="a637f-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="a637f-250">Bir **dışarıdan kullanıma sunulan** hizmetidir, genellikle bir yük dengeleyici üzerinden küme dışında erişilebilir bir uç noktasını kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="a637f-250">An **externally exposed** service is one that exposes an endpoint reachable from outside the cluster, usually through a load balancer.</span></span>

<span data-ttu-id="a637f-251">Bir **yalnızca iç** hizmetidir biri, uç nokta yalnızca küme içinde erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="a637f-251">An **internal-only** service is one whose endpoint is only reachable from within the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="a637f-252">Durum bilgisi olan hizmet uç noktaları genellikle Internet'e açık olmamalıdır değil.</span><span class="sxs-lookup"><span data-stu-id="a637f-252">Stateful service endpoints generally should not be exposed to the Internet.</span></span> <span data-ttu-id="a637f-253">Yük Dengeleyici bulun ve uygun durum bilgisi olan hizmet çoğaltma trafiği yönlendirmek mümkün olmayacağından durum bilgisi olan hizmetler kullanıma sunmak Service Fabric hizmeti çözümleme, Azure yük dengeleyici gibi algılamadan yük dengeleyici arkasında kümelerinin yükleyemez.</span><span class="sxs-lookup"><span data-stu-id="a637f-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as the Azure Load Balancer, will be unable to expose stateful services because the load balancer will not be able to locate and route traffic to the appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="a637f-254">ASP.NET Core durum bilgisi olmayan hizmetler dışarıdan kullanıma</span><span class="sxs-lookup"><span data-stu-id="a637f-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="a637f-255">WebListener dış, Internet'e HTTP uç noktaları Windows kullanıma ön uç Hizmetleri için önerilen web sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="a637f-255">WebListener is the recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="a637f-256">Saldırılara karşı daha iyi koruma sağlar ve Windows kimlik doğrulaması ve bağlantı noktası paylaşımı gibi Kestrel desteklemez özelliklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="a637f-256">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="a637f-257">Kestrel bir kenarı (Internet'e yönelik) sunucusu olarak şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="a637f-257">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="a637f-258">IIS veya Nginx gibi bir ters proxy sunucusu, ortak Internet'ten trafiğini işlemek için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a637f-258">A reverse proxy server such as IIS or Nginx must be used to handle traffic from the public Internet.</span></span>
 
<span data-ttu-id="a637f-259">Internet'e açık olduğunda bir durum bilgisi olmayan hizmetin bir yük dengeleyici üzerinden erişilebilen bir iyi bilinen ve kararlı uç noktası kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a637f-259">When exposed to the Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="a637f-260">Bu, uygulamanızın kullanıcılara sağlayacak URL'dir.</span><span class="sxs-lookup"><span data-stu-id="a637f-260">This is the URL you will provide to users of your application.</span></span> <span data-ttu-id="a637f-261">Aşağıdaki yapılandırma önerilir:</span><span class="sxs-lookup"><span data-stu-id="a637f-261">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="a637f-262">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="a637f-262">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a637f-263">Web sunucusu</span><span class="sxs-lookup"><span data-stu-id="a637f-263">Web server</span></span> | <span data-ttu-id="a637f-264">WebListener</span><span class="sxs-lookup"><span data-stu-id="a637f-264">WebListener</span></span> | <span data-ttu-id="a637f-265">Hizmet yalnızca güvenilir bir ağ, bu tür bir intranet açılırsa Kestrel kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a637f-265">If the service is only exposed to a trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="a637f-266">Aksi takdirde, WebListener tercih edilen bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="a637f-266">Otherwise, WebListener is the preferred option.</span></span> |
| <span data-ttu-id="a637f-267">Bağlantı noktası yapılandırması</span><span class="sxs-lookup"><span data-stu-id="a637f-267">Port configuration</span></span> | <span data-ttu-id="a637f-268">Statik</span><span class="sxs-lookup"><span data-stu-id="a637f-268">static</span></span> | <span data-ttu-id="a637f-269">İyi bilinen statik bağlantı noktası olarak yapılandırılmalıdır `Endpoints` ServiceManifest.xml, yapılandırmayı 80 HTTP veya HTTPS için 443 gibi.</span><span class="sxs-lookup"><span data-stu-id="a637f-269">A well-known static port should be configured in the `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="a637f-270">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="a637f-270">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="a637f-271">None</span><span class="sxs-lookup"><span data-stu-id="a637f-271">None</span></span> | <span data-ttu-id="a637f-272">`ServiceFabricIntegrationOptions.None` Hizmeti, gelen istekler için benzersiz bir kimlik doğrulama girişiminde değil böylece Service Fabric tümleştirme Ara yapılandırırken seçeneği kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a637f-272">The `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that the service does not attempt to validate incoming requests for a unique identifier.</span></span> <span data-ttu-id="a637f-273">Dış kullanıcılar, uygulamanızın ara yazılım tarafından kullanılan benzersiz tanımlayıcı bilgiler bilmez.</span><span class="sxs-lookup"><span data-stu-id="a637f-273">External users of your application will not know the unique identifying information used by the middleware.</span></span> |
| <span data-ttu-id="a637f-274">Örnek sayısı</span><span class="sxs-lookup"><span data-stu-id="a637f-274">Instance Count</span></span> | <span data-ttu-id="a637f-275">-1</span><span class="sxs-lookup"><span data-stu-id="a637f-275">-1</span></span> | <span data-ttu-id="a637f-276">Bir örnek, bir yük dengeleyici trafiği almak tüm düğümlere kullanılabilir olmasını sağlamak, ayarı örnek sayısı tipik kullanım durumlarında, "-"1 olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a637f-276">In typical use cases, the instance count setting should be set to "-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="a637f-277">Birden çok dışarıdan kullanıma sunulan hizmetler düğümleri aynı kümesi paylaşıyorsanız, benzersiz ancak kararlı bir URL yolu kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a637f-277">If multiple externally exposed services share the same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="a637f-278">Bu, IWebHost yapılandırırken sağlanan URL değiştirerek gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a637f-278">This can be accomplished by modifying the URL provided when configuring IWebHost.</span></span> <span data-ttu-id="a637f-279">Bu, yalnızca WebListener için geçerlidir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a637f-279">Note this applies to WebListener only.</span></span>

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

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="a637f-280">Yalnızca dahili durum bilgisiz ASP.NET Core hizmeti</span><span class="sxs-lookup"><span data-stu-id="a637f-280">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="a637f-281">Yalnızca küme içinde çağrılır durum bilgisi olmayan hizmetler benzersiz URL'leri kullanmanız gerekir ve birden çok hizmetleri arasında işbirliği emin olmak için bağlantı noktalarını dinamik olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="a637f-281">Stateless services that are only called from within the cluster should use unique URLs and dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="a637f-282">Aşağıdaki yapılandırma önerilir:</span><span class="sxs-lookup"><span data-stu-id="a637f-282">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="a637f-283">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="a637f-283">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a637f-284">Web sunucusu</span><span class="sxs-lookup"><span data-stu-id="a637f-284">Web server</span></span> | <span data-ttu-id="a637f-285">kestrel</span><span class="sxs-lookup"><span data-stu-id="a637f-285">Kestrel</span></span> | <span data-ttu-id="a637f-286">WebListener iç durum bilgisi olmayan hizmetler için kullanılabilir ancak Kestrel bir ana bilgisayar paylaşmak birden fazla hizmet örneği izin vermek için önerilen sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="a637f-286">Although WebListener may be used for internal stateless services, Kestrel is the recommended server to allow multiple service instances to share a host.</span></span>  |
| <span data-ttu-id="a637f-287">Bağlantı noktası yapılandırması</span><span class="sxs-lookup"><span data-stu-id="a637f-287">Port configuration</span></span> | <span data-ttu-id="a637f-288">dinamik olarak atanan</span><span class="sxs-lookup"><span data-stu-id="a637f-288">dynamically assigned</span></span> | <span data-ttu-id="a637f-289">Bir durum bilgisi olan hizmetin birden fazla çoğaltma bir ana bilgisayar işlemi veya ana bilgisayar işletim sistemi paylaşabilir ve bu nedenle benzersiz bağlantı noktaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a637f-289">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="a637f-290">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="a637f-290">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="a637f-291">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="a637f-291">UseUniqueServiceUrl</span></span> | <span data-ttu-id="a637f-292">Dinamik bağlantı noktası atama ile bu ayar daha önce açıklanan hatalı kimlik sorunu önler.</span><span class="sxs-lookup"><span data-stu-id="a637f-292">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="a637f-293">Instancecount</span><span class="sxs-lookup"><span data-stu-id="a637f-293">InstanceCount</span></span> | <span data-ttu-id="a637f-294">tüm</span><span class="sxs-lookup"><span data-stu-id="a637f-294">any</span></span> | <span data-ttu-id="a637f-295">Ayarlama örnek sayısı hizmeti çalıştırmak gerekli olarak herhangi bir değere ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a637f-295">The instance count setting can be set to any value necessary to operate the service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="a637f-296">Yalnızca dahili durum bilgisi olan ASP.NET Core hizmeti</span><span class="sxs-lookup"><span data-stu-id="a637f-296">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="a637f-297">Yalnızca küme içinde çağrılır durum bilgisi olan hizmetler dinamik olarak atanan bağlantı noktaları, birden çok hizmetleri arasında işbirliği sağlamak için kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="a637f-297">Stateful services that are only called from within the cluster should use dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="a637f-298">Aşağıdaki yapılandırma önerilir:</span><span class="sxs-lookup"><span data-stu-id="a637f-298">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="a637f-299">**Notlar**</span><span class="sxs-lookup"><span data-stu-id="a637f-299">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a637f-300">Web sunucusu</span><span class="sxs-lookup"><span data-stu-id="a637f-300">Web server</span></span> | <span data-ttu-id="a637f-301">kestrel</span><span class="sxs-lookup"><span data-stu-id="a637f-301">Kestrel</span></span> | <span data-ttu-id="a637f-302">`WebListenerCommunicationListener` Çoğaltmaları bir ana bilgisayar işlemi paylaşmak durum bilgisi olan hizmet tarafından kullanılmak üzere tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="a637f-302">The `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="a637f-303">Bağlantı noktası yapılandırması</span><span class="sxs-lookup"><span data-stu-id="a637f-303">Port configuration</span></span> | <span data-ttu-id="a637f-304">dinamik olarak atanan</span><span class="sxs-lookup"><span data-stu-id="a637f-304">dynamically assigned</span></span> | <span data-ttu-id="a637f-305">Bir durum bilgisi olan hizmetin birden fazla çoğaltma bir ana bilgisayar işlemi veya ana bilgisayar işletim sistemi paylaşabilir ve bu nedenle benzersiz bağlantı noktaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a637f-305">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="a637f-306">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="a637f-306">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="a637f-307">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="a637f-307">UseUniqueServiceUrl</span></span> | <span data-ttu-id="a637f-308">Dinamik bağlantı noktası atama ile bu ayar daha önce açıklanan hatalı kimlik sorunu önler.</span><span class="sxs-lookup"><span data-stu-id="a637f-308">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a637f-309">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a637f-309">Next steps</span></span>
[<span data-ttu-id="a637f-310">Service Fabric uygulamanızı Visual Studio kullanarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="a637f-310">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
