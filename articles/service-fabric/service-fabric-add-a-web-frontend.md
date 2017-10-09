---
title: "aaaCreate ASP.NET Core kullanarak Azure Service Fabric uygulamanızı bir web ön uç | Microsoft Docs"
description: "Service Fabric uygulaması toohello web bir ASP.NET Core proje ve hizmet Remoting aracılığıyla hizmet içi iletişim kullanarak kullanıma sunar."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a>Web hizmeti ön uç için ASP.NET Core kullanarak uygulamanızı oluşturun
Varsayılan olarak, Azure Service Fabric Hizmetleri ortak arabirimi toohello web sağlamaz. tooexpose uygulamanızın işlevselliği tooHTTP istemciler, bir web tooact giriş noktası olarak proje ve orada tooyour iletişim toocreate sahip tek tek Hizmetleri.

Bu öğreticide, biz ayrılacağı yeri biz hello seçmek [Visual Studio'da ilk uygulamanızı oluşturma](service-fabric-create-your-first-application-in-visual-studio.md) öğretici ve ASP.NET Core web hizmetini hello durum bilgisi olan sayacı hizmetini önüne ekleyin. Zaten yapmadıysanız, geri dönün ve Bu öğreticide ilk adım gerekir.

## <a name="set-up-your-environment-for-aspnet-core"></a>ASP.NET Core için ortamınızı ayarlayın

Bu öğretici yanı sıra Visual Studio 2017 toofollow gerekir. Herhangi bir sürümünü yapın. 

 - [Visual Studio 2017 yükleyin](https://www.visualstudio.com/)

toodevelop ASP.NET Core Service Fabric uygulamaları yüklü iş yükleri aşağıdaki hello olmalıdır:
 - **Azure geliştirme** (altında *Web ve bulut*)
 - **ASP.NET ve web geliştirme** (altında *Web ve bulut*)
 - **.NET core platformlar arası geliştirme** (altında *diğer Toolsets*)

>[!Note] 
>Visual Studio 2015 kullanmaya devam ediyorsanız toohave gerekiyor ancak hello .NET Core araçları Visual Studio 2015 için artık, güncelleştirilmekte olan [.NET Core VS 2015 Tooling Önizleme 2](https://www.microsoft.com/net/download/core) yüklü.

## <a name="add-an-aspnet-core-service-tooyour-application"></a>ASP.NET Core hizmet tooyour uygulama ekleme
ASP.NET Core toocreate modern web kullanıcı arabirimini kullanın ve API web bir basit, platformlar arası web geliştirme altyapısıdır. 

Bir ASP.NET Web API projesi tooour mevcut uygulamayı ekleyelim.

1. Çözüm Gezgini'nde sağ **Hizmetleri** içinde hello uygulama projesi ve seçin **Ekle > Yeni yapı hizmeti**.
   
    ![Yeni bir hizmet tooan varolan uygulama ekleme][vs-add-new-service]
2. Merhaba üzerinde **bir hizmet oluşturma** sayfasında, **ASP.NET Core** ve bir ad verin.
   
    ![ASP.NET web hizmeti hello yeni hizmet iletişim kutusunda seçme][vs-new-service-dialog]

3. Merhaba sonraki sayfaya ASP.NET Core birtakım proje şablonları sağlar. Bunlar olan Merhaba, aynı Not ASP.NET Core projesinde bir Service Fabric uygulaması dışında bir miktarda ek kod tooregister oluşturduysanız görür seçimler hello hizmeti ile Merhaba Service Fabric çalışma zamanı. Bu öğretici için seçin **Web API**. Ancak, uygulayabilirsiniz hello aynı kavramları toobuilding tam web uygulaması.
   
    ![ASP.NET proje türü seçme][vs-new-aspnet-project-dialog]
   
    Web API projeniz oluşturulduktan sonra iki hizmet uygulamanızda olmalıdır. Uygulamanızı toobuild devam ederken, daha fazla hizmet tam olarak hello ekleyebilirsiniz aynı şekilde. Her bağımsız olarak sürümlü hem de yükseltilmiş olabilir.

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın
tooget ne biz, şimdi yaptığınız bir fikir hello yeni uygulama ve ASP.NET Core Web API şablon hello hello varsayılan davranışı göz sağlar Al dağıtın.

1. Visual Studio toodebug hello uygulamasında F5 tuşuna basın.
2. Dağıtım tamamlandığında, Visual Studio tarayıcı toohello kökündeki hello ASP.NET Web API hizmetini başlatır. 404 hatası hello tarayıcıda görmeniz gerekir böylece hello ASP.NET çekirdek Web API şablon hello kökü için varsayılan davranış sağlamaz.
3. Ekleme `/api/values` hello tarayıcıda toohello konumu. Bu hello çağırır `Get` hello ValuesController hello Web API şablonunda yöntemi. Merhaba şablon--iki dizeyi içeren bir JSON dizisi tarafından sağlanan hello varsayılan yanıt verir:
   
    ![ASP.NET Core Web API şablondan döndürülen varsayılan değerler][browser-aspnet-template-values]
   
    Merhaba öğretici Hello sonuna bu sayfayı varsayılan dizeleri hello durum bilgisi olan hizmetimizi hello yerine en son sayaç değerini gösterir.

## <a name="connect-hello-services"></a>Merhaba Hizmetleri'ne Bağlama
Service Fabric reliable services ile nasıl iletişim kuracağını tam esneklik sağlar. Tek bir uygulama içinde TCP, bir HTTP REST API üzerinden erişilebilen diğer hizmetler ve hala web yuvalarını erişilebilir diğer hizmetler aracılığıyla erişilebilen hizmetler olabilir. Merhaba seçenekleri ve hello bileşim ilgili arka plan için bkz: [hizmetleriyle iletişim kurmasını](service-fabric-connect-and-communicate-with-services.md). Bu öğreticide, kullandığımız [Service Fabric hizmeti Remoting](service-fabric-reliable-services-communication-remoting.md), hello SDK'te sağlanan.

Hello (uzaktan yordam çağrısı veya RPC'ler Modellenen) hizmeti Remoting yaklaşım, hello ortak sözleşme hello hizmeti için bir arabirim tooact tanımlayın. Ardından, bu arabirimi toogenerate proxy sınıfı hello hizmetiyle etkileşim için kullanın.

### <a name="create-hello-remoting-interface"></a>Merhaba remoting arabirimi oluşturma
Merhaba durum bilgisi olan hizmet ve diğer hizmetleri, bu örneği hello ASP.NET Core web projesi arasında hello sözleşme olarak hello arabirimi tooact oluşturarak başlayalım. Bu arabirim, kendi sınıf kitaplığı proje oluşturacağız şekilde toomake RPC çağrısı, kullanan tüm hizmetleri tarafından paylaşılan gerekir.

1. Çözüm Gezgini'nde Çözümünüze sağ tıklayın ve seçin **Ekle** > **yeni proje**.

2. Merhaba seçin **Visual C#** sol gezinti bölmesi ve ardından hello hello girişi **sınıf kitaplığı** şablonu. Bu hello .NET Framework sürümü olarak ayarlanmış çok olun**4.5.2**.
   
    ![Durum bilgisi olan hizmetiniz için bir arabirim projesi oluşturma][vs-add-class-library-project]

3. Merhaba yüklemek **Microsoft.ServiceFabric.Services.Remoting** NuGet paketi. Arama **Microsoft.ServiceFabric.Services.Remoting** hello NuGet Paket Yöneticisi ve hizmet Remoting kullanan tüm projelerde hello çözümde yükleme de dahil olmak üzere:
   - Merhaba hizmet arabirimi içeren hello sınıf kitaplığı proje
   - Merhaba durum bilgisi olan hizmet projesi
   - Merhaba ASP.NET Core web hizmeti projesi
   
    ![Merhaba Hizmetleri NuGet paketi ekleme][vs-services-nuget-package]

4. Merhaba Sınıf Kitaplığı'nda tek bir yönteme bir arabirim oluşturmak `GetCountAsync`, ve hello arabiriminden genişletmek `Microsoft.ServiceFabric.Services.Remoting.IService`. Hello remoting arabirimi hizmet Remoting arabirimi olduğunu bu arabirimi tooindicate türetilmelidir.
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a>Durum bilgisi olan hizmet hello arabirimi uygulama
Merhaba arabirimi tanımlamış olduğunuz, tooimplement ihtiyacımız hello durum bilgisi olan hizmet içinde.

1. Durum bilgisi olan hizmetinizi hello arabirimi içeren bir başvuru toohello sınıf kitaplığı proje ekleyin.
   
    ![Bir başvuru toohello sınıf kitaplığı proje hello durum bilgisi olan hizmet ekleme][vs-add-class-library-reference]
2. Öğesinden devralınan hello sınıfını bulun `StatefulService`, gibi `MyStatefulService`ve tooimplement hello genişletmek `ICounter` arabirimi.
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. Şimdi hello tanımlanan tek bir yöntem hello uygulamak `ICounter` arabirimi, `GetCountAsync`.
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a>Bir hizmet remoting dinleyici kullanarak hello durum bilgisi olan hizmet kullanıma sunma
Merhaba ile `ICounter` uygulanan hello son adım arabirimidir tooopen hello hizmet Remoting iletişim kanalı. Durum bilgisi olan hizmetler için Service Fabric adlı geçersiz kılınabilir bir yöntem sağlar. `CreateServiceReplicaListeners`. Bu yöntemle tooenable hizmetiniz için istediğiniz iletişim hello türüne göre bir veya daha fazla iletişim dinleyicileri belirtebilirsiniz.

> [!NOTE]
> bir iletişim kanalı toostateless Hizmetleri açmak için hello eşdeğer yöntemi çağrıldığında `CreateServiceInstanceListeners`.

Bu durumda, biz hello varolan `CreateServiceReplicaListeners` yöntemi ve örneği sağlayan `ServiceRemotingListener`, istemcilerden aranabilir, RPC bitiş noktası oluşturur `ServiceProxy`.  

Merhaba `CreateServiceRemotingListener` hello üzerinde genişletme yöntemi `IService` arabirimi tooeasily verir oluşturma bir `ServiceRemotingListener` tüm varsayılan ayarlarla. toouse bu genişletme yöntemi hello olduğundan emin olun `Microsoft.ServiceFabric.Services.Remoting.Runtime` içeri aktarılan ad alanı. 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a>Merhaba hizmeti ile Merhaba ServiceProxy sınıfı toointeract kullanın
Durum bilgisi olan hizmetimizi şimdi hazır tooreceive diğer hizmetlerden RPC üzerinden trafiğidir. Bu nedenle tüm kalır ekleme hello kod toocommunicate onunla hello ASP.NET web hizmeti.

1. ASP.NET projenizde hello içeren bir başvuru toohello sınıf kitaplığı eklemek `ICounter` arabirimi.

2. Merhaba daha önce eklediğiniz **Microsoft.ServiceFabric.Services.Remoting** NuGet paketi toohello ASP.NET projesi. Bu paket hello sağlar `ServiceProxy` kullanacağınız sınıfı toomake RPC toohello durum bilgisi olan hizmet çağırır. Bu NuGet paketi hello ASP.NET Core web hizmeti projesi yüklendiğinden emin olun.

4. Merhaba, **denetleyicileri** klasörü, açık hello `ValuesController` sınıfı. Bu hello Not `Get` yöntemi şu anda yalnızca "değer1" ve "önceki hello tarayıcıda ne gördüğümüz eşleşen değer2"--sabit kodlanmış bir dize dizisi döndürür. Bu uygulama, kod aşağıdaki hello ile değiştirin:
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    Kodun ilk satırı Hello hello bir anahtardır. toocreate hello ICounter proxy toohello durum bilgisi olan hizmet, tooprovide iki parça bilgi gerekir: bir bölüm kimliği ve hello hello hizmetin adını.
   
    Kendi durumunun farklı demet içine bir müşteri kimliği veya posta kodu gibi tanımlayan bir anahtara göre bölerek bölümleme tooscale durum bilgisi olan hizmetler kullanabilirsiniz. Önemsiz uygulamamız hello durum bilgisi olan hizmet yalnızca bir bölüm sahiptir, böylece Hello anahtar önemli değildir. Sağladığınız herhangi bir tuşa toohello götürür aynı bölüm. Hizmetleri, bölümleme hakkında daha fazla toolearn bkz [nasıl toopartition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).
   
    Merhaba hizmet adıdır hello form doku URI'sini: /&lt;Uygulama_adı&gt;/&lt;servıce_name&gt;.
   
    Bu iki parça bilgi ile Service Fabric istekleri gönderilmesi gereken hello makine benzersiz şekilde tanımlayabilir. Merhaba `ServiceProxy` sınıfı onun yerine aynı zamanda sorunsuz bir şekilde hello durum bilgisi olan hizmet bölüm barındırdığı hello makine başarısız olduğu ve başka bir makine yükseltilen tootake olmalıdır hello durumu işler. Bu soyutlama yazma yapar istemci kodu toodeal önemli ölçüde daha basit diğer hizmetlerle hello.
   
    Biz hello proxy olduktan sonra biz yalnızca hello çağırma `GetCountAsync` yöntemi ve sonucunu döndürür.

5. F5 tuşuna basın yeniden toorun hello uygulama değiştirdi. Olarak daha önce Visual Studio otomatik olarak hello tarayıcı toohello hello web projesi kökündeki başlatır. Merhaba "API/değerleri" yolu ekleyin ve döndürülen hello geçerli sayaç değeri görmeniz gerekir.
   
    ![Merhaba tarayıcıda görüntülenen hello durum bilgisi olan bir sayaç değeri][browser-aspnet-counter-value]
   
    Merhaba tarayıcıyı yenilemek düzenli aralıklarla toosee hello sayaç değeri güncelleştirme.

## <a name="kestrel-and-weblistener"></a>Kestrel ve WebListener

Merhaba Kestrel bilinen, varsayılan ASP.NET Core web sunucusu olduğundan [doğrudan Internet trafiğini işlemek için şu anda desteklenmeyen](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel). Sonuç olarak, hello Service Fabric için ASP.NET Core durum bilgisiz hizmet şablonu kullanan [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) varsayılan olarak. 

Service Fabric Hizmetleri'ndeki Kestrel ve WebListener hakkında daha fazla toolearn başvurun çok[Service Fabric Reliable Services ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).

## <a name="connecting-tooa-reliable-actor-service"></a>Tooa güvenilir aktör hizmeti bağlanma
Bu öğretici bir durum bilgisi olan hizmeti ile iletişim web ön ucu ekleme odaklanır. Ancak, çok benzer bir model tootalk tooactors izleyebilirsiniz. Bir güvenilir aktör projesi oluşturduğunuzda, Visual Studio, sizin için otomatik olarak bir arabirim projesi oluşturur. Bu arabirim toogenerate aktör proxy ile Merhaba aktör hello web projesi toocommunicate kullanabilirsiniz. Merhaba iletişim kanalı otomatik olarak sağlanır. Toodo herhangi bir şey gerekmez, olduğundan eşdeğer tooestablishing bir `ServiceRemotingListener` Bu öğreticide hello durum bilgisi olan hizmeti için yaptığınız gibi.

## <a name="how-web-services-work-on-your-local-cluster"></a>Web hizmetleri yerel kümenizde nasıl çalışır
Genel olarak, tam olarak aynı Service Fabric uygulaması tooa çok makineli, dağıtılan yerel kümenizde küme ve beklendiği gibi çalıştığını yüksek oranda emin hello dağıtabilirsiniz. Yerel kümenizdeki tooa tek makine yalnızca bir beş düğümlü yapılandırmasını daraltılmış olmasıdır.

Tooweb Hizmetleri gelir ancak olduğunda bir anahtar ayrıntı. Azure'da yaptığı gibi bir yük dengeleyicinin arkasına kümenizi bulunur, web hizmetlerinizi hello yük dengeleyici itibaren her makineye dağıtılan emin olmalısınız yalnızca hepsini-bir kez deneme trafik hello makinelerde. Bu ayarı hello tarafından yapabileceğiniz `InstanceCount` hello hizmet toohello özel bir değer için "-"1.

Bunun aksine, bir web hizmeti yerel olarak çalıştırdığınızda, tooensure gerekir hello hizmet, yalnızca bir örneği çalışıyor. Aksi takdirde, çakışmaları hello üzerinde aynı dinleyen birden çok işlemlerini çalıştırmak yolu ve bağlantı noktası. Sonuç olarak, hello web hizmeti örnek sayısı çok ayarlanmalıdır yerel dağıtımlar için "1".

Farklı ortam için farklı değerler tooconfigure nasıl görürüm toolearn [birden çok ortamlar için uygulama parametreleri yönetme](service-fabric-manage-multiple-environment-app-configuration.md).

## <a name="next-steps"></a>Sonraki adımlar
ASP.NET Core uygulamanızla için kümesi sonlandırmak için daha fazla bilgi edinmek için bir web ön sahip olduğunuza [Service Fabric Reliable Services ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) ASP.NET Core Service Fabric ile nasıl çalıştığı bir derinlemesine anlamak için.

Ardından, [hizmetleriyle iletişim kurmasını hakkında daha fazla bilgi](service-fabric-connect-and-communicate-with-services.md) genel tooget tam bir resim olarak nasıl hizmet iletişimi Service Fabric çalışır.

Hizmet iletişimi nasıl çalıştığını, iyi anlamış olmanız sonra [bir küme oluşturmak ve uygulama toohello bulut dağıtma](service-fabric-cluster-creation-via-portal.md).

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
