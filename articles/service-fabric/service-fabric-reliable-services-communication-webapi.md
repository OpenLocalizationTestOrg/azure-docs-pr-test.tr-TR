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
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a>Kullanmaya başlama: OWIN kendi kendine barındırma ile Service Fabric Web API Hizmetleri
Kullanıcılarla ve birbirleriyle Hizmetleri toocommunicate nasıl istediğinize karar zaman azure Service Fabric hello güç sizin elinizde koyar. Bu öğreticide, .NET (OWIN) Service Fabric'ın güvenilir hizmetler API kendi kendine barındırma için açık Web arabirimi ile ASP.NET Web API kullanarak hizmet iletişimi uygulanmasına odaklanmaktadır. Biz derine hello Reliable Services takılabilir iletişim API inceleyin. Ayrıca Web API'sini bir adım adım örnek tooshow kullanacağız, nasıl özel iletişim dinleyici yukarı tooset.

## <a name="introduction-tooweb-api-in-service-fabric"></a>Service Fabric içinde giriş tooWeb API
ASP.NET Web API, .NET Framework hello üstünde HTTP API'leri oluşturmaya yönelik yaygın olarak kullanılan ve güçlü bir çerçevedir. Zaten hello çerçevesiyle bilmiyorsanız, bkz: [ASP.NET Web API 2 ile çalışmaya başlama](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn daha fazla.

Service Fabric Web API aynı ASP.NET Web tanıyor ve ona memnuniyet API hello. Merhaba nasıl farktır, *konak* bir Web API uygulaması. Microsoft Internet Information Services (IIS) kullanarak olmaz. toobetter hello farkı anlamak, şimdi iki bölüme ayırın:

1. Merhaba Web API uygulaması (denetleyicileri ve modelleri dahil)
2. Merhaba ana bilgisayar (Merhaba IIS web sunucusu, genellikle)

Bir Web API uygulaması değiştirmez. Merhaba son yazılmış Web API uygulamalardan farklı değildir ve uygulama kodunuz çoğunu mümkün toosimply taşıma olması gerekir. Ancak burada hello uygulamayı barındıran IIS üzerinde barındırma varsa ne alışık olduğunuz öğesinden biraz farklı olabilir. Biz bölümü barındırma toohello ulaşmadan önce bir şey daha fazla bilmiyorsanız başlayalım: hello Web API uygulaması.

## <a name="create-hello-application"></a>Merhaba uygulaması oluşturma
Visual Studio 2015'te tek bir durum bilgisiz hizmetle yeni bir Service Fabric uygulaması oluşturmaya başlayın.

Web API kullanarak durumsuz bir hizmet için bir Visual Studio şablonu kullanılabilir tooyou ' dir. Bu öğreticide, biz bu şablonu seçtiyseniz ne elde edebileceğiniz sonuçları sıfırdan bir Web API projesi derleme.

Nasıl toobuild sıfırdan veya bir Web API projesinde hello durum bilgisiz hizmeti Web API'sini şablonu ile başlatın ve yalnızca izleyin boş bir durum bilgisi olmayan proje toolearn seçin.  

Merhaba ilk adımı Web API için bazı NuGet paketleri toopull oluşturur. toouse istiyoruz hello Microsoft.AspNet.WebApi.OwinSelfHost paketidir. Bu paket, tüm hello gerekli Web API paketleri ve hello içerir *konak* paketler. Bu daha sonra önemli olacaktır.

Merhaba paketleri yüklendikten sonra hello temel Web API projesi yapısı oluşturmaya başlayabilirsiniz. Web API kullandıysanız, hello proje yapısını tanıdık gelecektir. Başlangıç ekleyerek bir `Controllers` dizin ve basit değerleri denetleyicisi:

**ValuesController.cs**

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

Ardından, bir başlangıç sınıfı hello proje kök tooregister hello yönlendirme, biçimlendiricileri ve herhangi bir yapılandırma ayarı ekleyin. Bu aynı zamanda Web API toohello içinde nerede takılan olup *konak*, hangi tekrar ziyaret daha sonra yeniden. 

**Haline**

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

Bu hello uygulama için bir parçasıdır. Bu noktada, biz yalnızca hello temel Web API projesi düzeni kurma ayarladınız. Şu ana kadar Web API projeleri hello son yazılmış veya hello temel Web API şablonunu çok farklı görüneceğini döndürmemelidir. İş mantığınızın hello denetleyicileri ve modellerinde her zamanki gibi gider.

Şimdi biz biz gerçekte çalışabilmesi barındırma hakkında ne yapacaksınız?

## <a name="service-hosting"></a>Barındırma hizmeti
Hizmetinizi Service Fabric içinde çalışan bir *hizmet ana bilgisayar işlemi*, hizmet kodunuzun çalıştığı bir yürütülebilir dosya. Merhaba güvenilir Hizmetleri API kullanarak bir hizmet yazdığınızda, hizmet projenizi yalnızca, hizmet türü kaydeder ve kodunuzun çalıştığı tooan yürütülebilir dosyasını derler. Service Fabric .NET içinde bir hizmet yazarken bu çoğu durumda geçerlidir. Program.cs içinde hello durum bilgisiz hizmet projeyi açtığınızda, görmeniz gerekir:

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

Gecikmeleri anormal biçimde hello giriş noktası tooa konsol uygulaması gibi görünüyorsa, çünkü olmasıdır.

Hizmet ana bilgisayar işlemi hakkında daha ayrıntılı bilgi hello ve hizmet kayıt olan bu makalenin hello kapsamı dışındadır. Ancak için önemli tooknow artık *kendi işleminde service kodunuzun çalıştığı*.

## <a name="self-host-web-api-with-an-owin-host"></a>Bir OWIN ana bilgisayar ile Web API kendini barındırma
Web API uygulama kodunuz kendi işleminde barındırılan koşuluyla, nasıl, onu tooa web sunucunuzu kurmak kanca? Girin [OWIN](http://owin.org/). OWIN yalnızca bir .NET web uygulamaları ve web sunucuları arasında sözleşmedir. ASP.NET (yukarı tooMVC 5) kullanıldığında, geleneksel hello web System.Web aracılığıyla sıkı şekilde bağlı tooIIS uygulamasıdır. Ancak, onu barındıran hello web sunucusundan ayrılmış bir web uygulaması yazma için Web API OWIN, uygular. Bu nedenle, kullanabileceğiniz bir *kendi kendini barındıran* kendi işleminde başlatabilirsiniz OWIN web sunucusu. Bu, biz yalnızca açıklanan hello Service Fabric barındırma modeli ile mükemmel sığar.

Bu makalede, Katana hello OWIN konağı olarak hello Web API uygulaması için kullanacağız. Katana uygulamasıdır üzerinde oluşturulan bir açık kaynak OWIN konak [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) ve Windows hello [HTTP sunucu API'sini](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).

> [!NOTE]
> toolearn Katana, Git toohello hakkında daha fazla [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana). Nasıl hızlı bir genel bakış için bkz toouse Katana tooself ana Web API [kullanım OWIN tooSelf konak ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).
> 
> 

## <a name="set-up-hello-web-server"></a>Merhaba web sunucusunu ayarlama
Merhaba güvenilir Hizmetleri API kullanıcılar ve istemcilerin tooconnect toohello hizmet izin ver iletişim yığınlarda burada takın iletişimi giriş noktası sağlar:

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

Merhaba web sunucusu (ve gelecekteki WebSockets gibi hello kullandığınız diğer iletişim yığını) hello ICommunicationListener arabirimi toointegrate doğru hello sistemiyle kullanmanız gerekir. Merhaba nedeniyle bu adımları izleyerek hello daha belirgin hale gelir.

İlk olarak, ICommunicationListener uygulayan OwinCommunicationListener adlı bir sınıf oluşturun:

**OwinCommunicationListener.cs**

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

Merhaba ICommunicationListener arabirim üç yöntem toomanage hizmetiniz için iletişimi dinleyici sağlar:

* *OpenAsync*. İsteklerini dinlemeye başlatın.
* *CloseAsync*. İsteklerini dinlemeye durdurmak, tüm yürütülen istekler bitiş ve düzgün biçimde kapatılamadı.
* *Abort*. Her şeyi iptal edin ve hemen durdurmak.

tooget, ekleme işlemi başlatıldı özel sınıf üyeleri şeyler hello dinleyici toofunction gerekir. Bunlar hello oluşturucu kullanılarak başlatılmalı ve URL dinleme hello ayarladığınızda, daha sonra kullanılır.

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

## <a name="implement-openasync"></a>Uygulama OpenAsync
tooset hello web sunucusu, iki parça bilgi gerekir:

* *Bir URL yolu öneki*. Bu isteğe bağlı olsa da, siz tooset için yararlı olan bu yukarı şimdi böylece uygulamanızda güvenli bir şekilde birden çok web hizmetleri barındırabilir.
* *Bir bağlantı noktası*.

Bir bağlantı noktası hello web sunucusuna ulaşmadan önce Service Fabric uygulaması ile Merhaba temel işletim sisteminin, üzerinde çalıştığı arasında bir tampon görevi gördüğünden bir uygulama katmanı sağladığını anlamak önemlidir. Bu nedenle, Service Fabric şekilde tooconfigure sağlar *uç noktaları* hizmetleriniz için. Service Fabric uç noktaları, hizmet toouse için kullanılabilir olmasını sağlar. Bu yolu tooconfigure yoksa bunları kendiniz işletim sistemi ortamı temel hello. Service Fabric uygulamanızı farklı ortamlarda herhangi bir değişiklik tooyour uygulama toomake gerek kalmadan kolaylıkla barındırabilir. (Örneğin, konak hello aynı uygulamayı Azure veya kendi veri merkezinizin.)

Bir HTTP uç noktası PackageRoot\ServiceManifest.xml yapılandırın:

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

Kısıtlı kimlik bilgilerini (ağ hizmeti Windows) Hello hizmet ana bilgisayar işlemi çalıştığı çünkü bu önemli bir adımdır. Bu, hizmet erişim tooset bir HTTP uç noktası yukarı, kendi olmaz anlamına gelir. Service Fabric Hello uç nokta Yapılandırması kullanılarak hizmet hello URL üzerinde dinler hello için hello doğru erişim denetim listesine (ACL) tooset bilir. Service Fabric, tooconfigure uç noktaları ayrıca standart bir yer sağlar.

Geri OwinCommunicationListener.cs içinde OpenAsync uygulama başlatabilirsiniz. Merhaba web sunucusu başladığınız budur. İlk olarak, hello uç nokta bilgileri alın ve hello hizmet üzerinde dinler hello URL oluşturun. Merhaba URL hello dinleyicisi durumsuz bir hizmeti veya bir durum bilgisi olan hizmet kullanılan bağlı olarak farklı olacaktır. Durum bilgisi olan bir hizmet için benzersiz bir adres her durum bilgisi olan hizmet çoğaltma için bunu dinlediği üzerinde toocreate hello dinleyicisi gerekir. Durum bilgisi olmayan hizmetler için başlangıç adresi daha kolay olabilir. 

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

"Http://+" Buraya kullanıldığını unutmayın. Bu toomake hello web sunucusu localhost, FQDN ve hello Makine IP de dahil olmak üzere tüm kullanılabilir adresleri, dinliyor emin olur.

Merhaba OpenAsync neden hello web sunucusu (veya tüm iletişim yığını) doğrudan yalnızca sahip olmak yerine bir ICommunicationListener açmak gibi gerçekleştirilir hello en önemli nedenlerinden biri uygulamasıdır `RunAsync()` hello hizmetindeki. Merhaba dönüş OpenAsync web sunucusu hello hello adresi dinlediği değerdir. Bu adres toohello sistem döndürüldüğünde, hello adresi hello hizmetine kaydeder. Service Fabric, istemciler ve diğer hizmetleri toothen izin veren bir API isteyin bu adres için hizmet adına göre sağlar. Merhaba hizmeti adresi statik olmadığı için bu önemlidir. Hizmetleri kaynak Dengeleme ve kullanılabilirlik amacıyla hello kümedeki taşındı. Bu adresi bir hizmet için dinleme tooresolve hello istemcilerinin veren hello mekanizmadır.

İle aklınızda OpenAsync hello web sunucusu başlatır ve dinlemede hello adresini döndürür. "Http://+" üzerinde dinler unutmayın, ancak OpenAsync hello adresi döndürmeden önce Merhaba "+" Merhaba IP veya FQDN şu anda açıktır hello düğümünün ile değiştirilir. Bu yöntem tarafından döndürülen hello adresi hello sistemiyle kayıtlı değil. Ayrıca, istemciler ve diğer hizmetler için bir hizmetin adresi söylediğinizde gördükleri olur. İstemcileri toocorrectly tooit bağlanmak, hello adresi gerçek bir IP veya FQDN gerekir.

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

Bu toohello OwinCommunicationListener hello oluşturucuda geçirildi hello başlangıç sınıfı başvuran unutmayın. Bu başlangıç örnek hello web sunucusu toobootstrap hello Web API uygulama tarafından kullanılır.

Merhaba `ServiceEventSource.Current.Message()` satır hello Tanılama Olayları penceresinde daha sonra görünür hello web sunucusu hello uygulama tooconfirm çalıştırdığınızda başarıyla başlattı.

## <a name="implement-closeasync-and-abort"></a>Uygulama CloseAsync ve durdurma
Son olarak, CloseAsync ve Abort uygulamak toostop hello web sunucusu. Merhaba web sunucusu OpenAsync sırasında oluşturulan hello sunucu tanıtıcısı atma tarafından durdurulabilir.

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

Bu uygulama örnekte CloseAsync ve Abort yalnızca hello web sunucusunu durdurun. Tooperform CloseAsync hello web sunucusunun daha düzgün bir şekilde koordine kapatma tercih edebilirler. Örneğin, hello kapatma hello döndürmeden önce tamamlandı yürütülen istekleri toobe için bekleyin.

## <a name="start-hello-web-server"></a>Başlangıç hello web sunucusu
Şimdi hazır toocreate olduğunuz ve OwinCommunicationListener toostart hello web sunucusu örneğini döndürür. Merhaba geri hizmet sınıfı (WebService.cs) hello, geçersiz kılma `CreateServiceInstanceListeners()` yöntemi:

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

Bu olduğu yere hello Web API *uygulama* ve OWIN hello *konak* son karşılamak. Merhaba ana bilgisayar (OwinCommunicationListener) hello örneği verilen *uygulama* (Web API) aracılığıyla hello başlangıç sınıfı. Service Fabric sonra kendi ömrü yönetir. Bu aynı düzeni genellikle tüm iletişim yığını ile izlenebilir.

## <a name="put-it-all-together"></a>Hepsini bir araya getirin
Bu örnekte, toodo hello içinde herhangi bir şey gerekmez `RunAsync()` bu geçersiz kılma yalnızca kaldırılabilmesi için yöntem.

Merhaba son hizmet uygulaması çok basit olmalıdır. Yalnızca, toocreate hello iletişimi dinleyicisi gerekir:

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

Merhaba tam `OwinCommunicationListener` sınıfı:

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

Tüm hello parçaları yerinde yerleştirdiğiniz, projenizin güvenilir Hizmetleri API giriş noktaları ve OWIN ana bilgisayar ile tipik bir Web API uygulaması gibi görünmelidir.

## <a name="run-and-connect-through-a-web-browser"></a>Çalıştırın ve bir web tarayıcısı üzerinden Bağlan
Bunu yapmadıysanız [geliştirme ortamınızı ayarlama](service-fabric-get-started.md).

Şimdi, yapı ve hizmetinize dağıtın. Tuşuna **F5** Visual Studio toobuild içinde hello uygulama ve dağıtın. Hello Tanılama Olayları penceresinde hello web sunucusu üzerinde http://localhost:8281 açılan belirten bir ileti görürsünüz /.

> [!NOTE]
> Başlangıç bağlantı noktası zaten makinenizde başka bir işlem tarafından açılıp açılmadığını, burada bir hata görebilirsiniz. Bu, o hello dinleyicisi açılamadı gösterir. Merhaba durum söz konusuysa ServiceManifest.xml hello uç nokta yapılandırması için farklı bir bağlantı noktası kullanmayı deneyin.
> 
> 

Merhaba hizmeti çalışmaya başladıktan sonra bir tarayıcı açın ve çok gidin[API/http://localhost:8281/değerleri](http://localhost:8281/api/values) tootest onu.

## <a name="scale-it-out"></a>Out ölçeklendirme
Durum bilgisiz web uygulamalarını genellikle ölçeklendirme, daha fazla makine ekleme ve bunları hello web uygulamalarında dönmesini anlamına gelir. Her yeni düğümler tooa küme eklendiklerinde Service Fabric'ın düzenleme altyapısı sizin için bunu yapabilirsiniz. Durum bilgisiz hizmet örneklerini oluşturduğunuzda, hello numarasını belirtebilirsiniz örneklerini toocreate istiyor. Service Fabric bu örneklerinin sayısını hello kümedeki düğümlere yerleştirir. Ve emin olur değil toocreate, birden fazla örneği herhangi bir düğümde. Service Fabric tooalways oluşturma örneği her düğümde belirterek söyleyebilirsiniz **-1** hello örnek sayısı için. Bu düğümler tooscale kümenizin eklediğinizde, durum bilgisiz hizmetinizi örneği hello yeni düğümler üzerinde oluşturulacak güvence altına alır. Bir hizmet örneği oluşturduğunuzda ayarlamak için bu değeri hello hizmet örneği, özelliğidir. PowerShell aracılığıyla bunu yapabilirsiniz:

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

Visual Studio durum bilgisiz hizmet projede varsayılan hizmet tanımlarken de bunu yapabilirsiniz:

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

Toocreate uygulama ve hizmet örneği, nasıl görürüm hakkında daha fazla bilgi için [bir uygulamayı dağıtmak](service-fabric-deploy-remove-applications.md).

## <a name="next-steps"></a>Sonraki adımlar
[Service Fabric uygulamanızı Visual Studio kullanarak hata ayıklama](service-fabric-debugging-your-application.md)

