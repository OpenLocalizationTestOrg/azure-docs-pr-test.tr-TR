---
title: "Merhaba ASP.NET Web API ile aaaService iletişim | Microsoft Docs"
description: "Nasıl tooimplement hizmet iletişimi kullanarak adım adım hello ASP.NET Web API OWIN hello güvenilir Hizmetleri API kendi kendine barındırma ile bilgi edinin."
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
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="f451a-103">Kullanmaya başlama: OWIN kendi kendine barındırma ile Service Fabric Web API Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="f451a-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="f451a-104">Kullanıcılarla ve birbirleriyle Hizmetleri toocommunicate nasıl istediğinize karar zaman azure Service Fabric hello güç sizin elinizde koyar.</span><span class="sxs-lookup"><span data-stu-id="f451a-104">Azure Service Fabric puts hello power in your hands when you're deciding how you want your services toocommunicate with users and with each other.</span></span> <span data-ttu-id="f451a-105">Bu öğreticide, .NET (OWIN) Service Fabric'ın güvenilir hizmetler API kendi kendine barındırma için açık Web arabirimi ile ASP.NET Web API kullanarak hizmet iletişimi uygulanmasına odaklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f451a-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="f451a-106">Biz derine hello Reliable Services takılabilir iletişim API inceleyin.</span><span class="sxs-lookup"><span data-stu-id="f451a-106">We'll delve deeply into hello Reliable Services pluggable communication API.</span></span> <span data-ttu-id="f451a-107">Ayrıca Web API'sini bir adım adım örnek tooshow kullanacağız, nasıl özel iletişim dinleyici yukarı tooset.</span><span class="sxs-lookup"><span data-stu-id="f451a-107">We'll also use Web API in a step-by-step example tooshow you how tooset up a custom communication listener.</span></span>

## <a name="introduction-tooweb-api-in-service-fabric"></a><span data-ttu-id="f451a-108">Service Fabric içinde giriş tooWeb API</span><span class="sxs-lookup"><span data-stu-id="f451a-108">Introduction tooWeb API in Service Fabric</span></span>
<span data-ttu-id="f451a-109">ASP.NET Web API, .NET Framework hello üstünde HTTP API'leri oluşturmaya yönelik yaygın olarak kullanılan ve güçlü bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="f451a-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of hello .NET Framework.</span></span> <span data-ttu-id="f451a-110">Zaten hello çerçevesiyle bilmiyorsanız, bkz: [ASP.NET Web API 2 ile çalışmaya başlama](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn daha fazla.</span><span class="sxs-lookup"><span data-stu-id="f451a-110">If you're not already familiar with hello framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn more.</span></span>

<span data-ttu-id="f451a-111">Service Fabric Web API aynı ASP.NET Web tanıyor ve ona memnuniyet API hello.</span><span class="sxs-lookup"><span data-stu-id="f451a-111">Web API in Service Fabric is hello same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="f451a-112">Merhaba nasıl farktır, *konak* bir Web API uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f451a-112">hello difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="f451a-113">Microsoft Internet Information Services (IIS) kullanarak olmaz.</span><span class="sxs-lookup"><span data-stu-id="f451a-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="f451a-114">toobetter hello farkı anlamak, şimdi iki bölüme ayırın:</span><span class="sxs-lookup"><span data-stu-id="f451a-114">toobetter understand hello difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="f451a-115">Merhaba Web API uygulaması (denetleyicileri ve modelleri dahil)</span><span class="sxs-lookup"><span data-stu-id="f451a-115">hello Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="f451a-116">Merhaba ana bilgisayar (Merhaba IIS web sunucusu, genellikle)</span><span class="sxs-lookup"><span data-stu-id="f451a-116">hello host (hello web server, usually IIS)</span></span>

<span data-ttu-id="f451a-117">Bir Web API uygulaması değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="f451a-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="f451a-118">Merhaba son yazılmış Web API uygulamalardan farklı değildir ve uygulama kodunuz çoğunu mümkün toosimply taşıma olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f451a-118">It's no different from Web API applications you may have written in hello past, and you should be able toosimply move over most of your application code.</span></span> <span data-ttu-id="f451a-119">Ancak burada hello uygulamayı barındıran IIS üzerinde barındırma varsa ne alışık olduğunuz öğesinden biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f451a-119">But if you've been hosting on IIS, where you host hello application may be a little different from what you're used to.</span></span> <span data-ttu-id="f451a-120">Biz bölümü barındırma toohello ulaşmadan önce bir şey daha fazla bilmiyorsanız başlayalım: hello Web API uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f451a-120">Before we get toohello hosting part, let's start with something more familiar: hello Web API application.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="f451a-121">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f451a-121">Create hello application</span></span>
<span data-ttu-id="f451a-122">Visual Studio 2015'te tek bir durum bilgisiz hizmetle yeni bir Service Fabric uygulaması oluşturmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="f451a-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="f451a-123">Web API kullanarak durumsuz bir hizmet için bir Visual Studio şablonu kullanılabilir tooyou ' dir.</span><span class="sxs-lookup"><span data-stu-id="f451a-123">A Visual Studio template for a stateless service using Web API is available tooyou.</span></span> <span data-ttu-id="f451a-124">Bu öğreticide, biz bu şablonu seçtiyseniz ne elde edebileceğiniz sonuçları sıfırdan bir Web API projesi derleme.</span><span class="sxs-lookup"><span data-stu-id="f451a-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="f451a-125">Nasıl toobuild sıfırdan veya bir Web API projesinde hello durum bilgisiz hizmeti Web API'sini şablonu ile başlatın ve yalnızca izleyin boş bir durum bilgisi olmayan proje toolearn seçin.</span><span class="sxs-lookup"><span data-stu-id="f451a-125">Select a blank Stateless Service project toolearn how toobuild a Web API project from scratch, or you can start with hello stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="f451a-126">Merhaba ilk adımı Web API için bazı NuGet paketleri toopull oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f451a-126">hello first step is toopull in some NuGet packages for Web API.</span></span> <span data-ttu-id="f451a-127">toouse istiyoruz hello Microsoft.AspNet.WebApi.OwinSelfHost paketidir.</span><span class="sxs-lookup"><span data-stu-id="f451a-127">hello package we want toouse is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="f451a-128">Bu paket, tüm hello gerekli Web API paketleri ve hello içerir *konak* paketler.</span><span class="sxs-lookup"><span data-stu-id="f451a-128">This package includes all hello necessary Web API packages and hello *host* packages.</span></span> <span data-ttu-id="f451a-129">Bu daha sonra önemli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f451a-129">This will be important later.</span></span>

<span data-ttu-id="f451a-130">Merhaba paketleri yüklendikten sonra hello temel Web API projesi yapısı oluşturmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f451a-130">After hello packages have been installed, you can begin building out hello basic Web API project structure.</span></span> <span data-ttu-id="f451a-131">Web API kullandıysanız, hello proje yapısını tanıdık gelecektir.</span><span class="sxs-lookup"><span data-stu-id="f451a-131">If you've used Web API, hello project structure should look very familiar.</span></span> <span data-ttu-id="f451a-132">Başlangıç ekleyerek bir `Controllers` dizin ve basit değerleri denetleyicisi:</span><span class="sxs-lookup"><span data-stu-id="f451a-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="f451a-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="f451a-133">**ValuesController.cs**</span></span>

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

<span data-ttu-id="f451a-134">Ardından, bir başlangıç sınıfı hello proje kök tooregister hello yönlendirme, biçimlendiricileri ve herhangi bir yapılandırma ayarı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f451a-134">Next, add a Startup class at hello project root tooregister hello routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="f451a-135">Bu aynı zamanda Web API toohello içinde nerede takılan olup *konak*, hangi tekrar ziyaret daha sonra yeniden.</span><span class="sxs-lookup"><span data-stu-id="f451a-135">This is also where Web API plugs in toohello *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="f451a-136">**Haline**</span><span class="sxs-lookup"><span data-stu-id="f451a-136">**Startup.cs**</span></span>

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

<span data-ttu-id="f451a-137">Bu hello uygulama için bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="f451a-137">That's it for hello application part.</span></span> <span data-ttu-id="f451a-138">Bu noktada, biz yalnızca hello temel Web API projesi düzeni kurma ayarladınız.</span><span class="sxs-lookup"><span data-stu-id="f451a-138">At this point, we've set up just hello basic Web API project layout.</span></span> <span data-ttu-id="f451a-139">Şu ana kadar Web API projeleri hello son yazılmış veya hello temel Web API şablonunu çok farklı görüneceğini döndürmemelidir.</span><span class="sxs-lookup"><span data-stu-id="f451a-139">So far, it shouldn't look much different from Web API projects you may have written in hello past or from hello basic Web API template.</span></span> <span data-ttu-id="f451a-140">İş mantığınızın hello denetleyicileri ve modellerinde her zamanki gibi gider.</span><span class="sxs-lookup"><span data-stu-id="f451a-140">Your business logic goes in hello controllers and models as usual.</span></span>

<span data-ttu-id="f451a-141">Şimdi biz biz gerçekte çalışabilmesi barındırma hakkında ne yapacaksınız?</span><span class="sxs-lookup"><span data-stu-id="f451a-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="f451a-142">Barındırma hizmeti</span><span class="sxs-lookup"><span data-stu-id="f451a-142">Service hosting</span></span>
<span data-ttu-id="f451a-143">Hizmetinizi Service Fabric içinde çalışan bir *hizmet ana bilgisayar işlemi*, hizmet kodunuzun çalıştığı bir yürütülebilir dosya.</span><span class="sxs-lookup"><span data-stu-id="f451a-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="f451a-144">Merhaba güvenilir Hizmetleri API kullanarak bir hizmet yazdığınızda, hizmet projenizi yalnızca, hizmet türü kaydeder ve kodunuzun çalıştığı tooan yürütülebilir dosyasını derler.</span><span class="sxs-lookup"><span data-stu-id="f451a-144">When you write a service by using hello Reliable Services API, your service project just compiles tooan executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="f451a-145">Service Fabric .NET içinde bir hizmet yazarken bu çoğu durumda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f451a-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="f451a-146">Program.cs içinde hello durum bilgisiz hizmet projeyi açtığınızda, görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f451a-146">When you open Program.cs in hello stateless service project, you should see:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="f451a-147">Gecikmeleri anormal biçimde hello giriş noktası tooa konsol uygulaması gibi görünüyorsa, çünkü olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="f451a-147">If that looks suspiciously like hello entry point tooa console application, that's because it is.</span></span>

<span data-ttu-id="f451a-148">Hizmet ana bilgisayar işlemi hakkında daha ayrıntılı bilgi hello ve hizmet kayıt olan bu makalenin hello kapsamı dışındadır.</span><span class="sxs-lookup"><span data-stu-id="f451a-148">Further details about hello service host process and service registration are beyond hello scope of this article.</span></span> <span data-ttu-id="f451a-149">Ancak için önemli tooknow artık *kendi işleminde service kodunuzun çalıştığı*.</span><span class="sxs-lookup"><span data-stu-id="f451a-149">But it's important tooknow for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="f451a-150">Bir OWIN ana bilgisayar ile Web API kendini barındırma</span><span class="sxs-lookup"><span data-stu-id="f451a-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="f451a-151">Web API uygulama kodunuz kendi işleminde barındırılan koşuluyla, nasıl, onu tooa web sunucunuzu kurmak kanca?</span><span class="sxs-lookup"><span data-stu-id="f451a-151">Given that your Web API application code is hosted in its own process, how do you hook it up tooa web server?</span></span> <span data-ttu-id="f451a-152">Girin [OWIN](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="f451a-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="f451a-153">OWIN yalnızca bir .NET web uygulamaları ve web sunucuları arasında sözleşmedir.</span><span class="sxs-lookup"><span data-stu-id="f451a-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="f451a-154">ASP.NET (yukarı tooMVC 5) kullanıldığında, geleneksel hello web System.Web aracılığıyla sıkı şekilde bağlı tooIIS uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="f451a-154">Traditionally when ASP.NET (up tooMVC 5) is used, hello web application is tightly coupled tooIIS through System.Web.</span></span> <span data-ttu-id="f451a-155">Ancak, onu barındıran hello web sunucusundan ayrılmış bir web uygulaması yazma için Web API OWIN, uygular.</span><span class="sxs-lookup"><span data-stu-id="f451a-155">However, Web API implements OWIN, so you can write a web application that is decoupled from hello web server that hosts it.</span></span> <span data-ttu-id="f451a-156">Bu nedenle, kullanabileceğiniz bir *kendi kendini barındıran* kendi işleminde başlatabilirsiniz OWIN web sunucusu.</span><span class="sxs-lookup"><span data-stu-id="f451a-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="f451a-157">Bu, biz yalnızca açıklanan hello Service Fabric barındırma modeli ile mükemmel sığar.</span><span class="sxs-lookup"><span data-stu-id="f451a-157">This fits perfectly with hello Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="f451a-158">Bu makalede, Katana hello OWIN konağı olarak hello Web API uygulaması için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="f451a-158">In this article, we'll use Katana as hello OWIN host for hello Web API application.</span></span> <span data-ttu-id="f451a-159">Katana uygulamasıdır üzerinde oluşturulan bir açık kaynak OWIN konak [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) ve Windows hello [HTTP sunucu API'sini](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span><span class="sxs-lookup"><span data-stu-id="f451a-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and hello Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="f451a-160">toolearn Katana, Git toohello hakkında daha fazla [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span><span class="sxs-lookup"><span data-stu-id="f451a-160">toolearn more about Katana, go toohello [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="f451a-161">Nasıl hızlı bir genel bakış için bkz toouse Katana tooself ana Web API [kullanım OWIN tooSelf konak ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span><span class="sxs-lookup"><span data-stu-id="f451a-161">For a quick overview of how toouse Katana tooself-host Web API, see [Use OWIN tooSelf-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-hello-web-server"></a><span data-ttu-id="f451a-162">Merhaba web sunucusunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="f451a-162">Set up hello web server</span></span>
<span data-ttu-id="f451a-163">Merhaba güvenilir Hizmetleri API kullanıcılar ve istemcilerin tooconnect toohello hizmet izin ver iletişim yığınlarda burada takın iletişimi giriş noktası sağlar:</span><span class="sxs-lookup"><span data-stu-id="f451a-163">hello Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients tooconnect toohello service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="f451a-164">Merhaba web sunucusu (ve gelecekteki WebSockets gibi hello kullandığınız diğer iletişim yığını) hello ICommunicationListener arabirimi toointegrate doğru hello sistemiyle kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f451a-164">hello web server (and any other communication stack you use in hello future, such as WebSockets) should use hello ICommunicationListener interface toointegrate correctly with hello system.</span></span> <span data-ttu-id="f451a-165">Merhaba nedeniyle bu adımları izleyerek hello daha belirgin hale gelir.</span><span class="sxs-lookup"><span data-stu-id="f451a-165">hello reasons for this will become more apparent in hello following steps.</span></span>

<span data-ttu-id="f451a-166">İlk olarak, ICommunicationListener uygulayan OwinCommunicationListener adlı bir sınıf oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f451a-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="f451a-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="f451a-167">**OwinCommunicationListener.cs**</span></span>

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

<span data-ttu-id="f451a-168">Merhaba ICommunicationListener arabirim üç yöntem toomanage hizmetiniz için iletişimi dinleyici sağlar:</span><span class="sxs-lookup"><span data-stu-id="f451a-168">hello ICommunicationListener interface provides three methods toomanage a communication listener for your service:</span></span>

* <span data-ttu-id="f451a-169">*OpenAsync*.</span><span class="sxs-lookup"><span data-stu-id="f451a-169">*OpenAsync*.</span></span> <span data-ttu-id="f451a-170">İsteklerini dinlemeye başlatın.</span><span class="sxs-lookup"><span data-stu-id="f451a-170">Start listening for requests.</span></span>
* <span data-ttu-id="f451a-171">*CloseAsync*.</span><span class="sxs-lookup"><span data-stu-id="f451a-171">*CloseAsync*.</span></span> <span data-ttu-id="f451a-172">İsteklerini dinlemeye durdurmak, tüm yürütülen istekler bitiş ve düzgün biçimde kapatılamadı.</span><span class="sxs-lookup"><span data-stu-id="f451a-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="f451a-173">*Abort*.</span><span class="sxs-lookup"><span data-stu-id="f451a-173">*Abort*.</span></span> <span data-ttu-id="f451a-174">Her şeyi iptal edin ve hemen durdurmak.</span><span class="sxs-lookup"><span data-stu-id="f451a-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="f451a-175">tooget, ekleme işlemi başlatıldı özel sınıf üyeleri şeyler hello dinleyici toofunction gerekir.</span><span class="sxs-lookup"><span data-stu-id="f451a-175">tooget started, add private class members for things hello listener will need toofunction.</span></span> <span data-ttu-id="f451a-176">Bunlar hello oluşturucu kullanılarak başlatılmalı ve URL dinleme hello ayarladığınızda, daha sonra kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f451a-176">These will be initialized through hello constructor and used later when you set up hello listening URL.</span></span>

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a><span data-ttu-id="f451a-177">Uygulama OpenAsync</span><span class="sxs-lookup"><span data-stu-id="f451a-177">Implement OpenAsync</span></span>
<span data-ttu-id="f451a-178">tooset hello web sunucusu, iki parça bilgi gerekir:</span><span class="sxs-lookup"><span data-stu-id="f451a-178">tooset up hello web server, you need two pieces of information:</span></span>

* <span data-ttu-id="f451a-179">*Bir URL yolu öneki*.</span><span class="sxs-lookup"><span data-stu-id="f451a-179">*A URL path prefix*.</span></span> <span data-ttu-id="f451a-180">Bu isteğe bağlı olsa da, siz tooset için yararlı olan bu yukarı şimdi böylece uygulamanızda güvenli bir şekilde birden çok web hizmetleri barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="f451a-180">Although this is optional, it's good for you tooset this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="f451a-181">*Bir bağlantı noktası*.</span><span class="sxs-lookup"><span data-stu-id="f451a-181">*A port*.</span></span>

<span data-ttu-id="f451a-182">Bir bağlantı noktası hello web sunucusuna ulaşmadan önce Service Fabric uygulaması ile Merhaba temel işletim sisteminin, üzerinde çalıştığı arasında bir tampon görevi gördüğünden bir uygulama katmanı sağladığını anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="f451a-182">Before you get a port for hello web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and hello underlying operating system that it runs on.</span></span> <span data-ttu-id="f451a-183">Bu nedenle, Service Fabric şekilde tooconfigure sağlar *uç noktaları* hizmetleriniz için.</span><span class="sxs-lookup"><span data-stu-id="f451a-183">As such, Service Fabric provides a way tooconfigure *endpoints* for your services.</span></span> <span data-ttu-id="f451a-184">Service Fabric uç noktaları, hizmet toouse için kullanılabilir olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="f451a-184">Service Fabric ensures that endpoints are available for your service toouse.</span></span> <span data-ttu-id="f451a-185">Bu yolu tooconfigure yoksa bunları kendiniz işletim sistemi ortamı temel hello.</span><span class="sxs-lookup"><span data-stu-id="f451a-185">This way, you don't have tooconfigure them yourself in hello underlying OS environment.</span></span> <span data-ttu-id="f451a-186">Service Fabric uygulamanızı farklı ortamlarda herhangi bir değişiklik tooyour uygulama toomake gerek kalmadan kolaylıkla barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="f451a-186">You can easily host your Service Fabric application in different environments without having toomake any changes tooyour application.</span></span> <span data-ttu-id="f451a-187">(Örneğin, konak hello aynı uygulamayı Azure veya kendi veri merkezinizin.)</span><span class="sxs-lookup"><span data-stu-id="f451a-187">(For example, you can host hello same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="f451a-188">Bir HTTP uç noktası PackageRoot\ServiceManifest.xml yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f451a-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="f451a-189">Kısıtlı kimlik bilgilerini (ağ hizmeti Windows) Hello hizmet ana bilgisayar işlemi çalıştığı çünkü bu önemli bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="f451a-189">This step is important because hello service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="f451a-190">Bu, hizmet erişim tooset bir HTTP uç noktası yukarı, kendi olmaz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f451a-190">This means that your service won't have access tooset up an HTTP endpoint on its own.</span></span> <span data-ttu-id="f451a-191">Service Fabric Hello uç nokta Yapılandırması kullanılarak hizmet hello URL üzerinde dinler hello için hello doğru erişim denetim listesine (ACL) tooset bilir.</span><span class="sxs-lookup"><span data-stu-id="f451a-191">By using hello endpoint configuration, Service Fabric knows tooset up hello proper access control list (ACL) for hello URL that hello service will listen on.</span></span> <span data-ttu-id="f451a-192">Service Fabric, tooconfigure uç noktaları ayrıca standart bir yer sağlar.</span><span class="sxs-lookup"><span data-stu-id="f451a-192">Service Fabric also provides a standard place tooconfigure endpoints.</span></span>

<span data-ttu-id="f451a-193">Geri OwinCommunicationListener.cs içinde OpenAsync uygulama başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f451a-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="f451a-194">Merhaba web sunucusu başladığınız budur.</span><span class="sxs-lookup"><span data-stu-id="f451a-194">This is where you start hello web server.</span></span> <span data-ttu-id="f451a-195">İlk olarak, hello uç nokta bilgileri alın ve hello hizmet üzerinde dinler hello URL oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f451a-195">First, get hello endpoint information and create hello URL that hello service will listen on.</span></span> <span data-ttu-id="f451a-196">Merhaba URL hello dinleyicisi durumsuz bir hizmeti veya bir durum bilgisi olan hizmet kullanılan bağlı olarak farklı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f451a-196">hello URL will be different depending on whether hello listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="f451a-197">Durum bilgisi olan bir hizmet için benzersiz bir adres her durum bilgisi olan hizmet çoğaltma için bunu dinlediği üzerinde toocreate hello dinleyicisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f451a-197">For a stateful service, hello listener needs toocreate a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="f451a-198">Durum bilgisi olmayan hizmetler için başlangıç adresi daha kolay olabilir.</span><span class="sxs-lookup"><span data-stu-id="f451a-198">For stateless services, hello address can be much simpler.</span></span> 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

<span data-ttu-id="f451a-199">"Http://+" Buraya kullanıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f451a-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="f451a-200">Bu toomake hello web sunucusu localhost, FQDN ve hello Makine IP de dahil olmak üzere tüm kullanılabilir adresleri, dinliyor emin olur.</span><span class="sxs-lookup"><span data-stu-id="f451a-200">This is toomake sure that hello web server is listening on all available addresses, including localhost, FQDN, and hello machine IP.</span></span>

<span data-ttu-id="f451a-201">Merhaba OpenAsync neden hello web sunucusu (veya tüm iletişim yığını) doğrudan yalnızca sahip olmak yerine bir ICommunicationListener açmak gibi gerçekleştirilir hello en önemli nedenlerinden biri uygulamasıdır `RunAsync()` hello hizmetindeki.</span><span class="sxs-lookup"><span data-stu-id="f451a-201">hello OpenAsync implementation is one of hello most important reasons why hello web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in hello service.</span></span> <span data-ttu-id="f451a-202">Merhaba dönüş OpenAsync web sunucusu hello hello adresi dinlediği değerdir.</span><span class="sxs-lookup"><span data-stu-id="f451a-202">hello return value from OpenAsync is hello address that hello web server is listening on.</span></span> <span data-ttu-id="f451a-203">Bu adres toohello sistem döndürüldüğünde, hello adresi hello hizmetine kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f451a-203">When this address is returned toohello system, it registers hello address with hello service.</span></span> <span data-ttu-id="f451a-204">Service Fabric, istemciler ve diğer hizmetleri toothen izin veren bir API isteyin bu adres için hizmet adına göre sağlar.</span><span class="sxs-lookup"><span data-stu-id="f451a-204">Service Fabric provides an API that allows clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="f451a-205">Merhaba hizmeti adresi statik olmadığı için bu önemlidir.</span><span class="sxs-lookup"><span data-stu-id="f451a-205">This is important because hello service address is not static.</span></span> <span data-ttu-id="f451a-206">Hizmetleri kaynak Dengeleme ve kullanılabilirlik amacıyla hello kümedeki taşındı.</span><span class="sxs-lookup"><span data-stu-id="f451a-206">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="f451a-207">Bu adresi bir hizmet için dinleme tooresolve hello istemcilerinin veren hello mekanizmadır.</span><span class="sxs-lookup"><span data-stu-id="f451a-207">This is hello mechanism that allows clients tooresolve hello listening address for a service.</span></span>

<span data-ttu-id="f451a-208">İle aklınızda OpenAsync hello web sunucusu başlatır ve dinlemede hello adresini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f451a-208">With that in mind, OpenAsync starts hello web server and returns hello address that it's listening on.</span></span> <span data-ttu-id="f451a-209">"Http://+" üzerinde dinler unutmayın, ancak OpenAsync hello adresi döndürmeden önce Merhaba "+" Merhaba IP veya FQDN şu anda açıktır hello düğümünün ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="f451a-209">Note that it listens on "http://+", but before OpenAsync returns hello address, hello "+" is replaced with hello IP or FQDN of hello node it is currently on.</span></span> <span data-ttu-id="f451a-210">Bu yöntem tarafından döndürülen hello adresi hello sistemiyle kayıtlı değil.</span><span class="sxs-lookup"><span data-stu-id="f451a-210">hello address that is returned by this method is what's registered with hello system.</span></span> <span data-ttu-id="f451a-211">Ayrıca, istemciler ve diğer hizmetler için bir hizmetin adresi söylediğinizde gördükleri olur.</span><span class="sxs-lookup"><span data-stu-id="f451a-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="f451a-212">İstemcileri toocorrectly tooit bağlanmak, hello adresi gerçek bir IP veya FQDN gerekir.</span><span class="sxs-lookup"><span data-stu-id="f451a-212">For clients toocorrectly connect tooit, they need an actual IP or FQDN in hello address.</span></span>

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="f451a-213">Bu toohello OwinCommunicationListener hello oluşturucuda geçirildi hello başlangıç sınıfı başvuran unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f451a-213">Note that this references hello Startup class that was passed in toohello OwinCommunicationListener in hello constructor.</span></span> <span data-ttu-id="f451a-214">Bu başlangıç örnek hello web sunucusu toobootstrap hello Web API uygulama tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f451a-214">This startup instance is used by hello web server toobootstrap hello Web API application.</span></span>

<span data-ttu-id="f451a-215">Merhaba `ServiceEventSource.Current.Message()` satır hello Tanılama Olayları penceresinde daha sonra görünür hello web sunucusu hello uygulama tooconfirm çalıştırdığınızda başarıyla başlattı.</span><span class="sxs-lookup"><span data-stu-id="f451a-215">hello `ServiceEventSource.Current.Message()` line will appear in hello Diagnostic Events window later, when you run hello application tooconfirm that hello web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="f451a-216">Uygulama CloseAsync ve durdurma</span><span class="sxs-lookup"><span data-stu-id="f451a-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="f451a-217">Son olarak, CloseAsync ve Abort uygulamak toostop hello web sunucusu.</span><span class="sxs-lookup"><span data-stu-id="f451a-217">Finally, implement both CloseAsync and Abort toostop hello web server.</span></span> <span data-ttu-id="f451a-218">Merhaba web sunucusu OpenAsync sırasında oluşturulan hello sunucu tanıtıcısı atma tarafından durdurulabilir.</span><span class="sxs-lookup"><span data-stu-id="f451a-218">hello web server can be stopped by disposing hello server handle that was created during OpenAsync.</span></span>

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

<span data-ttu-id="f451a-219">Bu uygulama örnekte CloseAsync ve Abort yalnızca hello web sunucusunu durdurun.</span><span class="sxs-lookup"><span data-stu-id="f451a-219">In this implementation example, both CloseAsync and Abort simply stop hello web server.</span></span> <span data-ttu-id="f451a-220">Tooperform CloseAsync hello web sunucusunun daha düzgün bir şekilde koordine kapatma tercih edebilirler.</span><span class="sxs-lookup"><span data-stu-id="f451a-220">You may opt tooperform a more gracefully coordinated shutdown of hello web server in CloseAsync.</span></span> <span data-ttu-id="f451a-221">Örneğin, hello kapatma hello döndürmeden önce tamamlandı yürütülen istekleri toobe için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="f451a-221">For example, hello shutdown could wait for in-flight requests toobe completed before hello return.</span></span>

## <a name="start-hello-web-server"></a><span data-ttu-id="f451a-222">Başlangıç hello web sunucusu</span><span class="sxs-lookup"><span data-stu-id="f451a-222">Start hello web server</span></span>
<span data-ttu-id="f451a-223">Şimdi hazır toocreate olduğunuz ve OwinCommunicationListener toostart hello web sunucusu örneğini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f451a-223">You're now ready toocreate and return an instance of OwinCommunicationListener toostart hello web server.</span></span> <span data-ttu-id="f451a-224">Merhaba geri hizmet sınıfı (WebService.cs) hello, geçersiz kılma `CreateServiceInstanceListeners()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="f451a-224">Back in hello Service class (WebService.cs), override hello `CreateServiceInstanceListeners()` method:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

<span data-ttu-id="f451a-225">Bu olduğu yere hello Web API *uygulama* ve OWIN hello *konak* son karşılamak.</span><span class="sxs-lookup"><span data-stu-id="f451a-225">This is where hello Web API *application* and hello OWIN *host* finally meet.</span></span> <span data-ttu-id="f451a-226">Merhaba ana bilgisayar (OwinCommunicationListener) hello örneği verilen *uygulama* (Web API) aracılığıyla hello başlangıç sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f451a-226">hello host (OwinCommunicationListener) is given an instance of hello *application* (Web API) via hello Startup class.</span></span> <span data-ttu-id="f451a-227">Service Fabric sonra kendi ömrü yönetir.</span><span class="sxs-lookup"><span data-stu-id="f451a-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="f451a-228">Bu aynı düzeni genellikle tüm iletişim yığını ile izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="f451a-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="f451a-229">Hepsini bir araya getirin</span><span class="sxs-lookup"><span data-stu-id="f451a-229">Put it all together</span></span>
<span data-ttu-id="f451a-230">Bu örnekte, toodo hello içinde herhangi bir şey gerekmez `RunAsync()` bu geçersiz kılma yalnızca kaldırılabilmesi için yöntem.</span><span class="sxs-lookup"><span data-stu-id="f451a-230">In this example, you don't need toodo anything in hello `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="f451a-231">Merhaba son hizmet uygulaması çok basit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f451a-231">hello final service implementation should be very simple.</span></span> <span data-ttu-id="f451a-232">Yalnızca, toocreate hello iletişimi dinleyicisi gerekir:</span><span class="sxs-lookup"><span data-stu-id="f451a-232">It only needs toocreate hello communication listener:</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

<span data-ttu-id="f451a-233">Merhaba tam `OwinCommunicationListener` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="f451a-233">hello complete `OwinCommunicationListener` class:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

<span data-ttu-id="f451a-234">Tüm hello parçaları yerinde yerleştirdiğiniz, projenizin güvenilir Hizmetleri API giriş noktaları ve OWIN ana bilgisayar ile tipik bir Web API uygulaması gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="f451a-234">Now that you have put all hello pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="f451a-235">Çalıştırın ve bir web tarayıcısı üzerinden Bağlan</span><span class="sxs-lookup"><span data-stu-id="f451a-235">Run and connect through a web browser</span></span>
<span data-ttu-id="f451a-236">Bunu yapmadıysanız [geliştirme ortamınızı ayarlama](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f451a-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="f451a-237">Şimdi, yapı ve hizmetinize dağıtın.</span><span class="sxs-lookup"><span data-stu-id="f451a-237">You can now build and deploy your service.</span></span> <span data-ttu-id="f451a-238">Tuşuna **F5** Visual Studio toobuild içinde hello uygulama ve dağıtın.</span><span class="sxs-lookup"><span data-stu-id="f451a-238">Press **F5** in Visual Studio toobuild and deploy hello application.</span></span> <span data-ttu-id="f451a-239">Hello Tanılama Olayları penceresinde hello web sunucusu üzerinde http://localhost:8281 açılan belirten bir ileti görürsünüz /.</span><span class="sxs-lookup"><span data-stu-id="f451a-239">In hello Diagnostic Events window, you should see a message that indicates that hello web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="f451a-240">Başlangıç bağlantı noktası zaten makinenizde başka bir işlem tarafından açılıp açılmadığını, burada bir hata görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f451a-240">If hello port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="f451a-241">Bu, o hello dinleyicisi açılamadı gösterir.</span><span class="sxs-lookup"><span data-stu-id="f451a-241">This indicates that hello listener couldn't be opened.</span></span> <span data-ttu-id="f451a-242">Merhaba durum söz konusuysa ServiceManifest.xml hello uç nokta yapılandırması için farklı bir bağlantı noktası kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="f451a-242">If that's hello case, try using a different port for hello endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="f451a-243">Merhaba hizmeti çalışmaya başladıktan sonra bir tarayıcı açın ve çok gidin[API/http://localhost:8281/değerleri](http://localhost:8281/api/values) tootest onu.</span><span class="sxs-lookup"><span data-stu-id="f451a-243">Once hello service is running, open a browser and navigate too[http://localhost:8281/api/values](http://localhost:8281/api/values) tootest it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="f451a-244">Out ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="f451a-244">Scale it out</span></span>
<span data-ttu-id="f451a-245">Durum bilgisiz web uygulamalarını genellikle ölçeklendirme, daha fazla makine ekleme ve bunları hello web uygulamalarında dönmesini anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f451a-245">Scaling out stateless web apps typically means adding more machines and spinning up hello web apps on them.</span></span> <span data-ttu-id="f451a-246">Her yeni düğümler tooa küme eklendiklerinde Service Fabric'ın düzenleme altyapısı sizin için bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f451a-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added tooa cluster.</span></span> <span data-ttu-id="f451a-247">Durum bilgisiz hizmet örneklerini oluşturduğunuzda, hello numarasını belirtebilirsiniz örneklerini toocreate istiyor.</span><span class="sxs-lookup"><span data-stu-id="f451a-247">When you create instances of a stateless service, you can specify hello number of instances you want toocreate.</span></span> <span data-ttu-id="f451a-248">Service Fabric bu örneklerinin sayısını hello kümedeki düğümlere yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="f451a-248">Service Fabric places that number of instances on nodes in hello cluster.</span></span> <span data-ttu-id="f451a-249">Ve emin olur değil toocreate, birden fazla örneği herhangi bir düğümde.</span><span class="sxs-lookup"><span data-stu-id="f451a-249">And it makes sure not toocreate more than one instance on any one node.</span></span> <span data-ttu-id="f451a-250">Service Fabric tooalways oluşturma örneği her düğümde belirterek söyleyebilirsiniz **-1** hello örnek sayısı için.</span><span class="sxs-lookup"><span data-stu-id="f451a-250">You can also instruct Service Fabric tooalways create an instance on every node by specifying **-1** for hello instance count.</span></span> <span data-ttu-id="f451a-251">Bu düğümler tooscale kümenizin eklediğinizde, durum bilgisiz hizmetinizi örneği hello yeni düğümler üzerinde oluşturulacak güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="f451a-251">This guarantees that whenever you add nodes tooscale out your cluster, an instance of your stateless service will be created on hello new nodes.</span></span> <span data-ttu-id="f451a-252">Bir hizmet örneği oluşturduğunuzda ayarlamak için bu değeri hello hizmet örneği, özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="f451a-252">This value is a property of hello service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="f451a-253">PowerShell aracılığıyla bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f451a-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="f451a-254">Visual Studio durum bilgisiz hizmet projede varsayılan hizmet tanımlarken de bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f451a-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="f451a-255">Toocreate uygulama ve hizmet örneği, nasıl görürüm hakkında daha fazla bilgi için [bir uygulamayı dağıtmak](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="f451a-255">For more information on how toocreate application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f451a-256">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f451a-256">Next steps</span></span>
[<span data-ttu-id="f451a-257">Service Fabric uygulamanızı Visual Studio kullanarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="f451a-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

