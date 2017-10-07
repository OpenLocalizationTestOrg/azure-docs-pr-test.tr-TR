---
title: "aaaReliable Hizmetleri iletişimi genel bakış | Microsoft Docs"
description: "Açılış dinleyicileri Hizmetleri dahil olmak üzere, uç noktaları çözme ve hizmetleri arasında iletişim kurarken hello Reliable Services iletişim modeline genel bakış."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a>Nasıl toouse hello Reliable Services iletişim API'leri
Bir platform olarak Azure Service Fabric Hizmetleri arasındaki iletişim hakkında tamamen bağımsızdır. Tüm protokoller ve yığınları UDP tooHTTP kabul edilir. Bu hizmetleri nasıl iletişim kurmanız gerekir toohello Hizmet Geliştirici toochoose olur. yerleşik iletişim toobuild kullanabileceğiniz API'leri yanı sıra, özel iletişim bileşenlerinizin yığınlar Hello Reliable Services uygulama çerçevesi sağlar.

## <a name="set-up-service-communication"></a>Hizmet iletişim kurma ayarlayın
Merhaba güvenilir Hizmetleri API hizmeti iletişimi için basit bir arabirim kullanır. tooopen hizmetiniz için bir uç nokta yalnızca bu arabirimi uygular:

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

Hizmet tabanlı sınıfı yöntemi geçersiz kılma seçeneğinde döndürerek iletişimi dinleyicisi uygulamanızı daha sonra ekleyebilirsiniz.

Durum bilgisi olmayan hizmetler için:

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

Durum bilgisi olan hizmetler için:

> [!NOTE]
> Durum bilgisi olan güvenilir hizmetler Java'da henüz desteklenmiyor.
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

Her iki durumda da dinleyicileri koleksiyonunu döndürür. Bu, büyük olasılıkla birden çok dinleyici kullanarak farklı protokoller kullanarak birden çok uç noktalarda hizmet toolisten sağlar. Örneğin, bir HTTP dinleyicisi ve ayrı bir Web yuvası dinleyicisi olabilir. Her dinleyicisi adı ve hello elde edilen koleksiyonunu alır *ad: adresi* bir istemci bir hizmet örneği veya bir bölüm için dinleme adresleri hello istediğinde, çiftleri bir JSON nesnesi olarak temsil.

Bir durum bilgisiz hizmetinde hello geçersiz kılma ServiceInstanceListeners koleksiyonunu döndürür. A `ServiceInstanceListener` işlevi toocreate içeren bir `ICommunicationListener(C#) / CommunicationListener(Java)` ve bir ad sağlar. Durum bilgisi olan hizmetler için hello geçersiz kılma ServiceReplicaListeners koleksiyonunu döndürür. Bu durum bilgisiz kendisine karşılık gelen biraz farklı değildir çünkü bir `ServiceReplicaListener` seçeneği tooopen sahip bir `ICommunicationListener` ikincil çoğaltmalar üzerinde. Yalnızca bir hizmet birden çok iletişim dinleyicileri kullanabilirsiniz, ancak aynı zamanda hangi dinleyicileri ikincil çoğaltmalar üzerinde isteklerini kabul etmek ve hangilerinin yalnızca birincil çoğaltmalar üzerinde dinleme belirtebilirsiniz.

Örneğin, yalnızca birincil çoğaltmalar RPC çağrılarını alan bir ServiceRemotingListener sahip olabilir ve okuma geçen ikinci, özel bir dinleyici ikincil çoğaltmaların üzerine HTTP üzerinden ister:

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> Hizmet için her dinleyicisi birden çok dinleyici oluştururken **gerekir** benzersiz bir ad verilmelidir.
>
>

Son olarak, hello hello hizmeti için gerekli olan hello uç noktaları açıklayan [hizmet bildirimi](service-fabric-application-model.md) uç noktalarda hello bölümünde.

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

Merhaba iletişimi dinleyici tooit hello ayrılan hello uç nokta kaynaklara erişebilir `CodePackageActivationContext` hello içinde `ServiceContext`. Merhaba dinleyicisi açıldığında isteklerini dinlemeye başlatabilirsiniz.

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> Uç nokta kaynaklardır ortak toohello tüm hizmet paketi ve hello hizmet paketi etkinleştirildiğinde Service Fabric tarafından ayrılır. Aynı aynı ServiceHost paylaşmak hello barındırılan birden çok hizmet çoğaltmalar Merhaba bağlantı noktası. Başka bir deyişle, bu hello iletişimi dinleyicisi bağlantı noktası paylaşımı desteklemelidir. Merhaba hello dinleme adresi oluşturduğunda bunu yapmanın yolu hello iletişimi dinleyici toouse hello için bölüm kimliği ve çoğaltma/örnek kimliği önerilir.
>
>

### <a name="service-address-registration"></a>Hizmeti adresi kaydı
Bir sistem hizmeti adlı hello *adlandırma hizmeti* Service Fabric kümelerinde çalışır. Merhaba adlandırma Hizmetleri ve her bir örneği veya çoğaltma hello hizmetinin dinlediği adresleri için bir kayıt hizmetidir. Ne zaman hello `OpenAsync(C#) / openAsync(Java)` yöntemi bir `ICommunicationListener(C#) / CommunicationListener(Java)` tamamlar, dönüş değeri hello Adlandırma Hizmeti kayıtlı. Bu adlandırma hizmeti olarak yayımlanan hello değeri herhangi bir şey hiç olabilir bir dize alır değeri döndürür. Merhaba hizmetinden hello adlandırma hizmeti için bir adres için söylediğinizde istemcileri gördükleri Bu dize değeridir.

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // hello string returned here will be published in hello Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

Service Fabric hizmet adına göre bu adres için istemcileri ve diğer hizmetleri toothen izin API'leri isteyin sağlar. Merhaba hizmeti adresi statik olmadığı için bu önemlidir. Hizmetleri kaynak Dengeleme ve kullanılabilirlik amacıyla hello kümedeki taşındı. Bu adresi bir hizmet için dinleme tooresolve hello ver hello mekanizmadır.

> [!NOTE]
> Nasıl bir iletişim dinleyici toowrite bakın, tam bir gözden geçirme [OWIN kendi kendine barındırma ile Service Fabric Web API Hizmetleri](service-fabric-reliable-services-communication-webapi.md) Java için kendi HTTP sunucusu uygulamasını yazabilirsiniz gelirken, C# ' ta EchoServer bakın https://github.com/Azure-Samples/service-fabric-java-getting-started örneğe.
>
>

## <a name="communicating-with-a-service"></a>Bir hizmet ile iletişim
Merhaba güvenilir Hizmetleri API Hizmetleri ile iletişim kitaplıkları toowrite istemcileri aşağıdaki hello sağlar.

### <a name="service-endpoint-resolution"></a>Hizmet uç noktası çözümleme
bir hizmeti ile Merhaba ilk adım toocommunication tooresolve bir uç nokta adresi hello bölüm veya tootalk için istediğiniz hello hizmet örneği, ' dir. Merhaba `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` yardımcı programının sınıfıdır hizmetin çalışma zamanında hello uç noktası belirlemek istemcileri yardımcı olan basit bir temel tür. Service Fabric terminolojisinde hizmetin hello uç noktası belirleme hello başvurulan tooas hello işlemidir *hizmet uç noktası çözümleme*.

Varsayılan ayarları kullanarak ServicePartitionResolver tooconnect tooservices bir küme içinde oluşturulabilir. Merhaba kullanım çoğu durum için önerilen şudur:

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

tooconnect tooservices farklı bir kümede bir küme ağ geçidi uç noktaları kümesiyle bir ServicePartitionResolver oluşturulabilir. Ağ geçidi uç noktaları toohello bağlanmak için yalnızca farklı uç noktalar olduğuna dikkat edin aynı küme. Örneğin:

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

Alternatif olarak, `ServicePartitionResolver` oluşturmak için bir işlev verilebilir bir `FabricClient` toouse dahili olarak:

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

`FabricClient`kullanılan toocommunicate hello kümede çeşitli yönetim işlemlerini için hello Service Fabric kümesi ile olan hello nesnesidir. Hizmet bölüm çözümleyici kümenizle nasıl etkileşim kurduğu üzerinde daha fazla denetim istediğinizde kullanışlıdır. `FabricClient`önemli tooreuse nedenle dahili olarak önbelleğe alma gerçekleştirir ve genellikle pahalı toocreate `FabricClient` mümkün olduğunca örnekleri.

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

Kullanılan tooretrieve hello sonra bir hizmet veya hizmet bölüm bölümlenmiş Hizmetleri için Adres Çözümleme yöntemidir.

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

Bir hizmet adresi kolayca bir ServicePartitionResolver kullanılarak çözülebilir, ancak daha fazla iş gereklidir tooensure hello çözülmüş adresi doğru şekilde kullanılabilir. Merhaba bağlantı denemesi geçici bir hata nedeniyle başarısız oldu ve yeniden denenebilir olup olmadığını istemciniz toodetect gerekir (örn., hizmet taşınmış veya geçici olarak kullanım dışı), ya da kalıcı bir hata (örneğin, hizmet silindi veya hello istenen kaynak artık yok). Hizmet örneği veya çoğaltmaları düğümü toonode birden çok nedeniyle herhangi bir zamanda taşıyabilirsiniz. hello hizmeti adresi ServicePartitionResolver çözümlendi, istemci kodunuzun tooconnect çalışır hello zamanına göre eski olabilir. Bu durumda yeniden hello istemci toore Çöz hello adresi gerekir. Merhaba önceki sağlama `ResolvedServicePartition` , çözümleyici gereksinimlerini tootry yeniden hello yerine yalnızca bir önbelleğe alınan adresi almak gösterir.

Genellikle, hello istemci kodu ServicePartitionResolver hello ile doğrudan işe. Oluşturulan ve toocommunication istemci hello güvenilir Hizmetleri API factory'leri geçirildi. Merhaba oluşturucuları kullanma hello çözümleyici dahili olarak toogenerate Hizmetleri ile kullanılan toocommunicate olabilecek istemci nesnesi.

### <a name="communication-clients-and-factories"></a>İletişim istemcileri ve oluşturucuları
Merhaba iletişimi Fabrika kitaplığı yeniden deneniyor bağlantıları tooresolved hizmet uç noktaları kolaylaştırır tipik bir hata işleme yeniden deneme deseni uygular. Merhaba hata işleyicileri sunarken hello Fabrika kitaplığı hello yeniden deneme mekanizması sağlar.

`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`tooa Service Fabric hizmeti iletişim kurabilirsiniz istemcileri üreten bir iletişim istemci sınıf üreticisi tarafından uygulanan hello temel arabirimi tanımlar. Burada hello istemci toocommunicate istediği hello Service Fabric hizmeti tarafından kullanılan hello iletişimi yığında CommunicationClientFactory bağlıdır hello uyarlamasını hello. Merhaba güvenilir Hizmetleri API sağlayan bir `CommunicationClientFactoryBase<TCommunicationClient>`. Bu temel bir hello CommunicationClientFactory arabirimi uygulamasını sağlar ve ortak tooall hello iletişimi yığınları olan görevleri gerçekleştirir. (ServicePartitionResolver toodetermine hello hizmet uç noktası kullanarak bu görevleri dahil). İstemcileri genellikle belirli toohello iletişim yığını olan hello soyut CommunicationClientFactoryBase sınıfı toohandle mantığı uygular.

Merhaba iletişimi istemci yalnızca bir adresi alır ve tooconnect tooa hizmeti kullanır. Merhaba istemci istediği ne olursa olsun protokolünü kullanabilirsiniz.

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

Merhaba istemci Fabrika iletişimi istemcileri oluşturmak için öncelikle sorumludur. Bir HTTP istemcisi gibi kalıcı bir bağlantı korumak olmayan istemciler için hello Fabrika toocreate ve dönüş hello istemci yeterlidir. Merhaba bağlantı toobe yeniden oluşturulması gerekip gerekmediğini bazı ikili protokolleri gibi kalıcı bir bağlantı korumak diğer protokolleri de hello Fabrika toodetermine tarafından doğrulanmalıdır.  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

Son olarak, bir özel durum oluştuğunda hangi eylemini tootake belirlemek için bir özel durum işleyici sorumludur. Özel durumlar kategorilere içine **yeniden denenebilir** ve **denenemeyen**.

* **Denenemeyen** özel durumlar yalnızca geri toohello çağıran işlenemezse.
* **yeniden denenebilir** özel durumlar daha fazla kategorilere ayrılabilir içine **geçici** ve **geçici olmayan**.
  * **Geçici** istisnaları, yalnızca hello hizmet uç noktası adresi yeniden çözümlemeden yeniden denenebilir. Bu geçici ağ sorunları içerir veya hizmet hata yanıtları hello hizmet uç noktası adresi gösteren olanlar dışındaki mevcut değil.
  * **Geçici olmayan** istisnaları hello hizmet uç noktası adresi toobe yeniden çözülmüş gerektirenler. Bunlar hello Hizmeti uç noktası, hello hizmet tooa farklı bir düğüme taşındıktan belirten erişilemedi belirtmek özel durumları içerir.

Merhaba `TryHandleException` belirli bir özel durum hakkında karar verir. Varsa, **bilmediği** hangi bir özel durum hakkında kararlar toomake döndürme zorunluluğu **false**. Varsa, **bilen** hangi karar toomake, hello sonuç uygun şekilde ayarlama ve döndürme **doğru**.

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a>Tüm bir araya getirme
İle bir `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, ve `IExceptionHandler(C#) / ExceptionHandler(Java)` bir iletişim protokolü, yerleşik bir `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` hepsini bir araya sarmalar ve hello hata işleme ve hizmet bölümü adres çözünürlüğü döngü bu bileşenlerin çevresinde sağlar.

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a>Sonraki adımlar
* HTTP iletişimi Hizmetleri'nde arasında örneğine bakın bir [C# örnek proje github'da](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) veya [Java örnek proje github'da](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).
* [Güvenilir hizmetler remoting ile uzak yordam çağrıları](service-fabric-reliable-services-communication-remoting.md)
* [Web API OWIN güvenilir Hizmetleri'nde kullanır](service-fabric-reliable-services-communication-webapi.md)
* [Güvenilir hizmetler kullanarak WCF iletişimi](service-fabric-reliable-services-communication-wcf.md)
