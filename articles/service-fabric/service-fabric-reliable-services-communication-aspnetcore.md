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
# <a name="aspnet-core-in-service-fabric-reliable-services"></a>ASP.NET çekirdek Service Fabric güvenilir hizmetler

ASP.NET Core modern bulut tabanlı Internet'e bağlı uygulamaları, web uygulamaları, IOT uygulamaları ve mobil arka uçlarını gibi oluşturmak için yeni bir açık kaynaklı ve çapraz platform framework kümesidir. 

Bu makalede ASP.NET Core services Service Fabric güvenilir hello kullanarak Hizmetleri'nde bir ayrıntılı kılavuz toohosting olan **Microsoft.ServiceFabric.AspNetCore.** * NuGet paketlerini kümesi.

Service Fabric ASP.NET çekirdek tanıtım bir öğretici ve geliştirme ortamınızı ayarlayın alma hakkında yönergeler için bkz: [bir web uygulamanız için ASP.NET Core kullanarak ön derleme](service-fabric-add-a-web-frontend.md).

Merhaba, bu makalenin kalanında ile ASP.NET Core bilginiz varsayar. Merhaba okuma öneririz, varsa [ASP.NET Core Temelleri](https://docs.microsoft.com/aspnet/core/fundamentals/index).

## <a name="aspnet-core-in-hello-service-fabric-environment"></a>ASP.NET Core hello Service Fabric ortamında

ASP.NET Core uygulamaları hello tam .NET Framework, Service Fabric Hizmetleri şu anda yalnızca çalıştırabilirsiniz veya .NET Core üzerinde çalıştırmasına rağmen tam .NET Framework hello. Bir ASP.NET Core Service Fabric hizmeti yapılandırdığınızda Bunun anlamı, hala hedeflemelidir tam .NET Framework hello.

ASP.NET Core Service Fabric iki farklı şekillerde kullanılabilir:
 - **Bir konuk yürütülebilir dosya barındırılan**. Birincil olarak kullanılan toorun mevcut ASP.NET Core uygulamaları Service Fabric kod değişikliğine budur.
 - **İçinde güvenilir bir hizmet Farklı Çalıştır**. Bu, hello Service Fabric çalışma zamanı ile daha iyi tümleştirme sağlar ve durum bilgisi olan ASP.NET Core hizmetleri sağlar.

Merhaba, bu makalenin kalanında nasıl kullanarak güvenilir hizmet içinde ASP.NET Core toouse hello sevk ASP.NET Core Tümleştirme Bileşenleri hello Service Fabric SDK ile açıklanmaktadır. 

## <a name="service-fabric-service-hosting"></a>Service Fabric hizmeti barındırma

Service Fabric içinde bir veya daha fazla örnekleri ve/veya hizmetinizin çoğaltmaları çalıştırmak bir *hizmet ana bilgisayar işlemi*, hizmet kodunuzun çalıştığı bir yürütülebilir dosya. Kendi hizmet yazarı olarak hello hizmet ana bilgisayar işlemi ve Service Fabric etkinleştirir ve sizin için izler.

Geleneksel ASP.NET (yukarı tooMVC 5), sıkı şekilde bağlı tooIIS System.Web.dll aracılığıyla teknolojidir. ASP.NET Core hello web sunucusu ve web uygulamanızı arasında ayrım sağlar. Bu web uygulamaları toobe farklı web sunucuları arasında taşınabilir verir ve ayrıca web sunucuları toobe sağlar *kendi kendini barındıran*, anlamına gelir bir web sunucusu kendi işleminde adanmış web tarafından sahip olunan karşılıklı tooa işlem olarak başlatmak için IIS gibi sunucu yazılımı. 

Sipariş toocombine bir Service Fabric hizmeti ve ASP.NET, Konuk yürütülebilir dosya veya güvenilir bir hizmet, hizmet ana bilgisayar işlemi içinde mümkün toostart ASP.NET olması gerekir. Kendi kendine barındırma ASP.NET Core toodo verir bu.

## <a name="hosting-aspnet-core-in-a-reliable-service"></a>ASP.NET Core güvenilir hizmetinde barındırma
Genellikle, kendi kendini barındıran ASP.NET Core uygulamaları bir WebHost hello gibi bir uygulamanın giriş noktası oluşturmak `static void Main()` yönteminde `Program.cs`. Bu durumda, hello WebHost hello yaşam döngüsü hello işleminin ilişkili toohello yaşam döngüsü ' dir.

![Bir işlemde ASP.NET Core barındırma][0]

Ancak, hello uygulama giriş noktası hello doğru yerde toocreate WebHost güvenilir bir hizmet olarak değil, hello uygulama giriş noktası yalnızca kullanıldığından tooregister hizmet böylece hizmet örneklerini oluşturabilir, hello Service Fabric çalışma zamanı ile yazın yazın. Merhaba WebHost kendisini güvenilir bir hizmet olarak oluşturulmalıdır. Merhaba hizmet barındırma işlemi içinde birden çok yaşam döngüleri hizmet örneği ve/veya çoğaltmaları gidebilirsiniz. 

Bir güvenilir hizmet örneği türetme, hizmet sınıfı tarafından temsil edilen `StatelessService` veya `StatefulService`. bir hizmet için Hello iletişim yığını bulunduğu bir `ICommunicationListener` hizmet sınıfınızı uygulamasında. Merhaba `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet paketlerini içeren uygulamaları `ICommunicationListener` başlatmak ve Kestrel ya da güvenilir bir hizmette WebListener hello ASP.NET Core WebHost yönetin.

![ASP.NET Core güvenilir hizmetinde barındırma][1]

## <a name="aspnet-core-icommunicationlisteners"></a>ASP.NET Core ICommunicationListeners
Merhaba `ICommunicationListener` hello Kestrel ve WebListener uygulamalarında `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet paketlerini benzer kullanım desenlerini sahip ancak biraz farklı eylemler belirli tooeach web sunucu gerçekleştirin. 

Her iki iletişim dinleyicileri şu bağımsız hello alan bir oluşturucu sağlar:
 - **`ServiceContext serviceContext`**: Merhaba `ServiceContext` hizmetini çalıştıran hello hakkında bilgi içeren nesne.
 - **`string endpointName`**: hello adını bir `Endpoint` ServiceManifest.xml yapılandırmasında. Öncelikle burada hello iki iletişim dinleyicileri farklı budur: WebListener **gerektirir** bir `Endpoint` Kestrel çalışmazken yapılandırma.
 - **`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**:, oluşturduğunuz ve dönüş uygulayan bir lambda bir `IWebHost`. Tooconfigure bu sayede `IWebHost` normalde bir ASP.NET Core uygulamada hello yolu. Merhaba lambda sağlar, hello Service Fabric tümleştirme bağlı olarak, kullanım ve hello seçenekleri için oluşturulan bir URL `Endpoint` sağladığınız yapılandırma. URL sonra değiştirilebilir veya olarak kullanılan,-toostart hello web sunucusudur.

## <a name="service-fabric-integration-middleware"></a>Service Fabric tümleştirme Ara
Merhaba `Microsoft.ServiceFabric.Services.AspNetCore` NuGet paketi içeren hello `UseServiceFabricIntegration` genişletme yöntemi `IWebHostBuilder` , Service Fabric algılayan ara yazılımı ekler. Bu ara yazılımın hello Kestrel veya WebListener yapılandırır `ICommunicationListener` benzersiz bir hizmet URL'si ile Service Fabric adlandırma hizmeti hello ve ardından doğrular tooregister istemci istekleri tooensure istemcileri toohello doğru hizmet bağlama. Bu, Service Fabric, burada birden çok web uygulamaları üzerinde hello aynı fiziksel veya sanal makine çalıştırabilirsiniz ancak benzersiz ana bilgisayar adları, yanlışlıkla toohello yanlış hizmeti bağlanmasını tooprevent istemcileri kullanmayın gibi paylaşılan konak ortamında gereklidir. Bu senaryo hello sonraki bölümünde daha ayrıntılı olarak açıklanmıştır.

### <a name="a-case-of-mistaken-identity"></a>Hatalı kimlik durumunun
Hizmet çoğaltmalar, protokol, bakılmaksızın benzersiz IP: BağlantıNoktası birleşimi üzerinde dinler. Bir IP: BağlantıNoktası uç noktada dinleme hizmeti çoğaltma başladıktan sonra o uç noktası adresi toohello Service Fabric adlandırma hizmeti Burada, istemciler veya diğer hizmetler tarafından keşfedilmesini bildirir. Aynı IP: BağlantıNoktası uç noktasını, daha önce başka bir hizmet uygulaması dinamik olarak atanan bağlantı noktaları, bir hizmet çoğaltma tesadüfen hizmetleri kullanması Merhaba, aynı fiziksel veya sanal makine hello. Bu istemci neden toomistakely connect toohello yanlış hizmeti. Aşağıdaki olaylar dizisi hello oluşursa bu durum oluşabilir:

 1. Hizmeti bir HTTP üzerinden 10.0.0.1:30000 üzerinde dinler. 
 2. İstemci Hizmeti A çözümler ve adres 10.0.0.1:30000 alır
 3. Hizmet bir tooa farklı bir düğüme taşır.
 4. Hizmet B üzerinde 10.0.0.1 yerleştirilir ve tesadüfen kullandığı aynı bağlantı noktasını 30000 hello.
 5. İstemci tooconnect tooservice bir önbelleğe alınan adresi 10.0.0.1:30000 ile çalışır.
 6. İstemcidir başarıyla bağlı tooservice kullanıldıklarını değil B bağlı artık toohello yanlış hizmeti.

Bu hatalar zor toodiagnose olabilir rastgele zamanlarda neden olabilir. 

### <a name="using-unique-service-urls"></a>Benzersiz bir hizmet URL'leri kullanma
Bu, tooprevent Hizmetleri bir uç nokta toohello benzersiz bir tanımlayıcı adlandırma hizmeti gönderin ve ardından istemci istekleri sırasında bu benzersiz tanımlayıcı doğrulamak. Bu, güvenilir bir saldırgan-Kiracı olmayan ortamda hizmetleri arasında İşbirlikçi bir işlemdir. Bu, bir kiracı tehlikeli ortamda güvenli hizmetinin kimlik doğrulaması sağlamaz.

Güvenilen bir ortamda hello tarafından eklenen Ara hello `UseServiceFabricIntegration` yöntemi toohello adlandırma hizmeti gönderilen ve bu tanımlayıcı her istekte doğrular bir benzersiz tanımlayıcı toohello adresi otomatik olarak ekler. Hello tanımlayıcı eşleşmiyorsa hello ara yazılımı hemen bir HTTP 410 kaybedildi yanıtı döndürür.

Dinamik olarak atanan bir bağlantı noktası olmalısınız kullanan Hizmetleri bu ara yazılımı kullanın.

Sabit benzersiz bağlantı noktası kullanan hizmetler işbirlikçi ortamında bu sorun yok. Sabit benzersiz bağlantı noktası genellikle istemci uygulamaları tooconnect için bilinen bir bağlantı noktasına ihtiyacınız dışarıya yönelik hizmetler için kullanılır. Örneğin, çoğu Internet'e yönelik web uygulamaları, web tarayıcısı bağlantıları için bağlantı noktası 80 veya 443 kullanır. Bu durumda, hello benzersiz tanımlayıcı etkinleştirilmemelidir.

Merhaba Aşağıdaki diyagramda hello istek akışı etkin hello Ara yazılımla gösterilmektedir:

![Service Fabric ASP.NET Core tümleştirme][2]

Kestrel ve WebListener `ICommunicationListener` uygulamaları tam olarak hello bu mekanizması kullanır aynı şekilde. WebListener dahili hello temel kullanarak benzersiz URL yollarına bağlı istekleri ayırt edebilir ancak *http.sys* işlevselliği özelliği, bağlantı noktası *değil* WebListener hellotarafındankullanılan`ICommunicationListener` uygulama, daha önce açıklanan hello senaryoda HTTP 503 ve HTTP 404 hata durum kodları neden. HTTP 503 ve HTTP 404 yaygın olarak kullanılan tooindicate zaten olduğu gibi sırayla çok hello hatası istemciler toodetermine hello amacı diğer hataları zorlaştırır. Bu nedenle, hem Kestrel ve WebListener `ICommunicationListener` uygulamaları standartlaştırmak hello tarafından sağlanan hello ara yazılım üzerinde `UseServiceFabricIntegration` genişletme yöntemi istemcileri yalnızca tooperform hizmet uç noktası gerekir böylece yeniden çözümlemek HTTP 410 yanıtları eylem.

## <a name="weblistener-in-reliable-services"></a>Güvenilir hizmetler WebListener
WebListener kullanılabilir güvenilir bir hizmet olarak hello içeri aktararak **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet paketi. Bu pakette `WebListenerCommunicationListener`, uygulaması `ICommunicationListener`, sağlayan toocreate bir ASP.NET Core WebHost güvenilir bir hizmet içinde WebListener hello web sunucusu olarak kullanma.

WebListener hello üzerinde oluşturulmuş [Windows HTTP sunucu API'sini](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx). Bu hello kullanır *http.sys* IIS tooprocess HTTP tarafından kullanılan çekirdek sürücüsü ister ve bunları tooprocesses çalışan web uygulamalarını rota. Merhaba birden çok işlemi aynı fiziksel veya sanal makine toohost web uygulamaları üzerinde hello böylece benzersiz URL yolu veya ana bilgisayar adı tarafından disambiguated aynı bağlantı noktası. Bu özellikler hello içinde birden çok Web sitesini barındırmak için Service Fabric yararlıdır aynı küme.

Merhaba Aşağıdaki diyagramda WebListener hello nasıl kullandığı gösterilmiştir *http.sys* bağlantı noktası paylaşımı için Windows çekirdek sürücüsü:

![HTTP.sys][3]

### <a name="weblistener-in-a-stateless-service"></a>Durum bilgisiz hizmetindeki WebListener
toouse `WebListener` bir durum bilgisiz hizmetinde hello geçersiz kılma `CreateServiceInstanceListeners` yöntemi ve return bir `WebListenerCommunicationListener` örneği:

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

### <a name="weblistener-in-a-stateful-service"></a>Durum bilgisi olan hizmet WebListener

`WebListenerCommunicationListener`şu anda durum bilgisi olan hizmetler kullanmak için tasarlanmamıştır hello temel ile son toocomplications *http.sys* bağlantı noktası özelliği paylaşma. Daha fazla bilgi için dinamik bağlantı noktası ayırma ile WebListener bölümüne aşağıdaki hello bakın. Durum bilgisi olan hizmetler için web sunucusu önerilen hello Kestrel olur.

### <a name="endpoint-configuration"></a>Uç nokta yapılandırması

Bir `Endpoint` hello WebListener dahil olmak üzere Windows HTTP sunucu API'sini kullanan web sunucuları için yapılandırma gereklidir. Hello Windows HTTP sunucu API'sini kullanan web sunucularının URL'LERİNİ ile ilk yedek gerekir *http.sys* (Bu normalde hello ile gerçekleştirilir [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) aracı). Bu eylem, Hizmetleri varsayılan olmayan yükseltilmiş ayrıcalıklar gerektiriyor. Merhaba hello "http" veya "https" seçeneklerini `Protocol` hello özelliğinin `Endpoint` yapılandırmasında *ServiceManifest.xml* kullanılan özellikle tooinstruct hello Service Fabric çalışma zamanı tooregister URL ile*http.sys* hello kullanarak sizin adınıza [ *güçlü joker* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL öneki.

Örneğin, tooreserve `http://+:80` bir hizmet için hello aşağıdaki yapılandırma içinde ServiceManifest.xml kullanılmalıdır:

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

Ve toohello hello uç nokta adı geçirilen `WebListenerCommunicationListener` Oluşturucusu:

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

#### <a name="use-weblistener-with-a-static-port"></a>Statik bir bağlantı noktası ile WebListener kullanın
toouse WebListener, statik bir bağlantı noktası başlangıç bağlantı noktası numarası hello sağlamak `Endpoint` yapılandırma:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a>Dinamik bir bağlantı noktası ile WebListener kullanın
toouse WebListener, dinamik olarak atanmış bir bağlantı noktası atlayın hello `Port` hello özelliğinde `Endpoint` yapılandırma:

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

Dinamik bir bağlantı noktası tarafından ayrılmış Not bir `Endpoint` yapılandırma, yalnızca bir bağlantı noktası sağlar *ana bilgisayar işlemi başına*. Merhaba barındırma modeli sağlar hello barındırılan birden çok hizmet örnekleri ve/veya çoğaltmaları toobe geçerli Service Fabric aynı, her biri aynı bağlantı noktası hello ayrılmış hello paylaşacak anlamı işlemi `Endpoint` yapılandırma. Birden çok WebListener örnekleri hello temel kullanarak bir bağlantı noktası paylaşabilirsiniz *http.sys* özellik, ancak, bağlantı noktası tarafından desteklenmiyor `WebListenerCommunicationListener` istemci isteklerini tanıttığı toohello zorluklar son. Dinamik bağlantı noktası için Kestrel web sunucusu önerilen hello kullanımdır.

## <a name="kestrel-in-reliable-services"></a>Güvenilir hizmetler kestrel
Kestrel kullanılabilir güvenilir bir hizmet olarak hello içeri aktararak **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet paketi. Bu pakette `KestrelCommunicationListener`, uygulaması `ICommunicationListener`, sağlayan toocreate bir ASP.NET Core WebHost güvenilir bir hizmet içinde Kestrel hello web sunucusu olarak kullanma.

Kestrel ASP.NET Core için platformlar arası web sunucusu libuv, platformlar arası zaman uyumsuz g/ç kitaplığı dayalıdır. WebListener Kestrel merkezi endpoint Yöneticisi gibi kullanmaz *http.sys*. Ve WebListener farklı olarak, birden çok işlemler arasında bağlantı noktası paylaşımı Kestrel desteklemiyor. Kestrel her örneğini benzersiz bir bağlantı noktası kullanmanız gerekir.

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a>Durum bilgisiz hizmetindeki kestrel
toouse `Kestrel` bir durum bilgisiz hizmetinde hello geçersiz kılma `CreateServiceInstanceListeners` yöntemi ve return bir `KestrelCommunicationListener` örneği:

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

### <a name="kestrel-in-a-stateful-service"></a>Durum bilgisi olan hizmet kestrel
toouse `Kestrel` durum bilgisi olan bir hizmeti hello geçersiz kılma `CreateServiceReplicaListeners` yöntemi ve return bir `KestrelCommunicationListener` örneği:

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

Bu örnekte, bir tek örneğini `IReliableStateManager` toohello WebHost bağımlılık ekleme kapsayıcısını sağlanır. Bu kesinlikle gerekli değildir, ancak toouse tanır `IReliableStateManager` ve güvenilir koleksiyonlarda MVC denetleyici eylem yöntemleri.

Unutmayın bir `Endpoint` yapılandırma adı **değil** çok sağlanan`KestrelCommunicationListener` durum bilgisi olan bir hizmette. Bu bölüm aşağıdaki hello daha ayrıntılı açıklanmıştır.

### <a name="endpoint-configuration"></a>Uç nokta yapılandırması
Bir `Endpoint` yapılandırması gerekli toouse Kestrel değil. 

Kestrel basit tek başına web sunucusunun adıdır; WebListener (veya HttpListener) aksine, onu ihtiyaç duymadığı bir `Endpoint` yapılandırmasında *ServiceManifest.xml* URL kayıt önceki toostarting gerektirmediğinden. 

#### <a name="use-kestrel-with-a-static-port"></a>Statik bir bağlantı noktası ile Kestrel kullanın
Statik bağlantı noktası hello yapılandırılabilir `Endpoint` ServiceManifest.xml yapılandırma Kestrel ile kullanım için. Bu kesinlikle gerekli olmamakla birlikte, iki olası faydaları sağlar:
 1. Başlangıç bağlantı noktası hello uygulama bağlantı noktası aralığında uymazsa hello işletim sistemi güvenlik duvarı üzerinden Service Fabric tarafından açılmış.
 2. Sağlanan URL tooyou aracılığıyla hello `KestrelCommunicationListener` Bu bağlantı noktasını kullanır.

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

Varsa bir `Endpoint` olan yapılandırılmış, adını hello geçirilmelidir `KestrelCommunicationListener` Oluşturucusu: 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

Varsa bir `Endpoint` yapılandırması kullanılmaz, hello hello adlarında atlayın `KestrelCommunicationListener` Oluşturucusu. Bu durumda, dinamik bir bağlantı noktası kullanılır. Daha fazla bilgi için Hello sonraki bölüme bakın.

#### <a name="use-kestrel-with-a-dynamic-port"></a>Dinamik bir bağlantı noktası ile Kestrel kullanın
Kestrel hello bir hello otomatik olarak bağlantı noktası atama kullanamaz `Endpoint` ServiceManifest.xml, yapılandırmada olduğundan otomatik olarak bağlantı noktası atama bir `Endpoint` yapılandırması atar benzersiz bir bağlantı noktası başına *ana bilgisayar işlemi* , ve tek ana bilgisayar işlemi birden çok Kestrel örnekleri içerebilir. Bağlantı noktası paylaşımı Kestrel desteklemediğinden, her Kestrel örneğini benzersiz bir bağlantı noktasında açılmalıdır gibi bu çalışmaz.

toouse dinamik bağlantı noktası atama Kestrel ile yalnızca hello atlayın `Endpoint` ServiceManifest.xml yapılandırmasında tamamen ve bir uç nokta adı toohello geçmeyin `KestrelCommunicationListener` Oluşturucusu:

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

Bu yapılandırmada, `KestrelCommunicationListener` kullanılmayan bir bağlantı noktası hello uygulama bağlantı noktası aralığından otomatik olarak seçer.

## <a name="scenarios-and-configurations"></a>Senaryolar ve yapılandırmaları
Bu bölümde senaryo aşağıdaki hello açıklar ve hello düzgün çalıştığını hizmeti web sunucusu, bağlantı noktası yapılandırmasını, Service Fabric tümleştirme seçeneklerini ve çeşitli ayarları tooachieve önerilen sağlar:
 - ASP.NET Core durum bilgisiz hizmetini dışarıdan kullanıma
 - Yalnızca dahili ASP.NET Core durum bilgisiz hizmeti
 - Yalnızca dahili ASP.NET Core durum bilgisi olan hizmet

Bir **dışarıdan kullanıma sunulan** hizmetidir, genellikle bir yük dengeleyici üzerinden hello küme dışında erişilebilir bir uç noktasını kullanıma sunar.

Bir **yalnızca iç** hizmetidir biri, uç nokta yalnızca hello küme içinde erişilebilir.

> [!NOTE]
> Durum bilgisi olan hizmet uç noktaları genellikle olmamalıdır toohello Internet açık. Merhaba yük dengeleyici değil mümkün toolocate olması ve trafik toohello rota hello Azure yük dengeleyici gibi Service Fabric hizmeti çözümleme algılamadan yük dengeleyici arkasında kümelerinin oluşturulamıyor tooexpose durum bilgisi olan hizmetler olur uygun durum bilgisi olan hizmet çoğaltma. 

### <a name="externally-exposed-aspnet-core-stateless-services"></a>ASP.NET Core durum bilgisi olmayan hizmetler dışarıdan kullanıma
WebListener web sunucusu dış, Internet'e HTTP uç noktaları Windows kullanıma ön uç Hizmetleri için önerilen hello ' dir. Saldırılara karşı daha iyi koruma sağlar ve Windows kimlik doğrulaması ve bağlantı noktası paylaşımı gibi Kestrel desteklemez özelliklerini destekler. 

Kestrel bir kenarı (Internet'e yönelik) sunucusu olarak şu anda desteklenmiyor. IIS veya Nginx gibi bir ters proxy sunucusu kullanılmalıdır toohandle trafiği genel Internet hello.
 
Ne zaman gösterilen toohello Internet, durum bilgisiz hizmeti yük dengeleyici üzerinden erişilebilen bir iyi bilinen ve kararlı uç noktası kullanmanız gerekir. Bu, uygulamanızın toousers sağlayacak hello URL'dir. yapılandırma aşağıdaki hello önerilir:

|  |  | **Notlar** |
| --- | --- | --- |
| Web sunucusu | WebListener | Merhaba service yalnızca gösterilen tooa güvenilir ağ, bu tür bir intranet ise Kestrel kullanılabilir. Aksi takdirde, WebListener tercih edilen hello seçenektir. |
| Bağlantı noktası yapılandırması | Statik | İyi bilinen statik bağlantı noktası hello yapılandırılmalıdır `Endpoints` ServiceManifest.xml, yapılandırmayı 80 HTTP veya HTTPS için 443 gibi. |
| ServiceFabricIntegrationOptions | None | Merhaba `ServiceFabricIntegrationOptions.None` hello hizmeti toovalidate gelen istekler için benzersiz bir tanımlayıcı denemez böylece Service Fabric tümleştirme Ara yapılandırırken seçeneği kullanılmalıdır. Dış kullanıcılar, uygulamanızın hello benzersiz tanımlayıcı bilgiler hello ara yazılımı tarafından kullanılan bilmez. |
| Örnek sayısı | -1 | Tipik kullanım durumlarında ayarı hello örnek sayısı çok ayarlanmalıdır-"1" bir örnek, bir yük dengeleyici trafiği almak tüm düğümlere kullanılabilir olmasını sağlamak. |

Birden çok dışarıdan kullanıma sunulan hizmetler aynı düğümlerinin ayarlamak hello paylaşıyorsanız, benzersiz ancak kararlı bir URL yolu kullanılmalıdır. Bu, IWebHost yapılandırırken sağlanan hello URL değiştirerek gerçekleştirilebilir. Bu yalnızca tooWebListener geçerlidir unutmayın.

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

### <a name="internal-only-stateless-aspnet-core-service"></a>Yalnızca dahili durum bilgisiz ASP.NET Core hizmeti
Yalnızca gelen hello küme içinde denir durum bilgisi olmayan hizmetler ve bağlantı noktaları tooensure işbirliği birden çok hizmetleri arasında dinamik olarak atanan benzersiz URL'leri kullanmalısınız. yapılandırma aşağıdaki hello önerilir:

|  |  | **Notlar** |
| --- | --- | --- |
| Web sunucusu | kestrel | WebListener iç durum bilgisi olmayan hizmetler için kullanılabilir Kestrel hello birden çok hizmet örnekleri tooshare bir ana bilgisayar sunucusu tooallow önerilen olsa da.  |
| Bağlantı noktası yapılandırması | dinamik olarak atanan | Bir durum bilgisi olan hizmetin birden fazla çoğaltma bir ana bilgisayar işlemi veya ana bilgisayar işletim sistemi paylaşabilir ve bu nedenle benzersiz bağlantı noktaları gerekir. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Dinamik bağlantı noktası atama ile bu ayar daha önce açıklanan mistaken hello kimlik sorunu önler. |
| Instancecount | tüm | Merhaba örnek sayısı ayarını tooany değeri gerekli toooperate hello hizmet ayarlayabilirsiniz. |

### <a name="internal-only-stateful-aspnet-core-service"></a>Yalnızca dahili durum bilgisi olan ASP.NET Core hizmeti
Yalnızca gelen hello küme içinde denir durum bilgisi olan hizmetler birden çok hizmetleri arasında dinamik olarak atanan bağlantı noktaları tooensure işbirliği kullanmanız gerekir. yapılandırma aşağıdaki hello önerilir:

|  |  | **Notlar** |
| --- | --- | --- |
| Web sunucusu | kestrel | Merhaba `WebListenerCommunicationListener` çoğaltmaları bir ana bilgisayar işlemi paylaşmak durum bilgisi olan hizmet tarafından kullanılmak üzere tasarlanmamıştır. |
| Bağlantı noktası yapılandırması | dinamik olarak atanan | Bir durum bilgisi olan hizmetin birden fazla çoğaltma bir ana bilgisayar işlemi veya ana bilgisayar işletim sistemi paylaşabilir ve bu nedenle benzersiz bağlantı noktaları gerekir. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Dinamik bağlantı noktası atama ile bu ayar daha önce açıklanan mistaken hello kimlik sorunu önler. |

## <a name="next-steps"></a>Sonraki adımlar
[Service Fabric uygulamanızı Visual Studio kullanarak hata ayıklama](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
