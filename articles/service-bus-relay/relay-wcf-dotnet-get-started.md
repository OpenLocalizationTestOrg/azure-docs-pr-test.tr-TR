---
title: ".NET Azure geçiş WCF geçişlerine aaaGet Başlarken | Microsoft Docs"
description: "Toouse Azure geçiş WCF farklı konumlarda barındırılan tooconnect iki uygulamaları nasıl geçişleri öğrenin."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: a652617fc2e9b7c8d62d39fa914f77df6e3a1771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a>Nasıl toouse Azure geçiş WCF geçişleri .NET ile
Bu makalede nasıl toouse hello Azure geçiş hizmeti açıklanmaktadır. Hello örnekler C# dilinde yazılmıştır ve Service Bus derlemesine hello bulundurulan uzantıları ile hello Windows Communication Foundation (WCF) API'sini kullanır. Hello Azure geçişi hakkında daha fazla bilgi için bkz: [Azure geçişine genel bakış](relay-what-is-it.md).

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a>WCF geçişi nedir?

Hello Azure [ *WCF geçiş* ](relay-what-is-it.md) hizmet, hem Azure veri merkezinde hem de kendi şirket içi Kurumsal ortamınızda çalışan karma uygulamalar toobuild sağlar. Merhaba geçiş hizmeti kolaylaştıran bu sağlayarak toosecurely tooopen bir güvenlik duvarı bağlantı olması veya gerekliliği olmadan bir kurumsal ağ toohello genel bulut içinde bulunan Windows Communication Foundation (WCF) hizmetlerini kullanıma sunma tooa kurumsal ağ altyapısına müdahale eden değişiklikler.

![WCF Geçişi Kavramları](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

Azure geçişi, var olan Kuruluş ortamınızda toohost WCF hizmetleri sağlar. Ardından, Azure'da çalışan gelen oturumları ve istekleri toothese WCF hizmetleri toohello geçiş hizmeti için dinleme devredebilirsiniz. Bu, Azure, veya toomobile çalışanlara veya extranet iş ortağı ortamlarına içinde çalışan bu hizmetleri tooapplication kodu, tooexpose sağlar. Geçiş hizmetlerin ayrıntılı erişebilen toosecurely denetimi sağlar. Mevcut Kurumsal çözümleri ve hello buluttan yararlanma bunu verilerini ve güçlü ve güvenli bir yöntem tooexpose uygulama işlevselliğini sağlar.

Bu makalede toouse Azure geçiş toocreate bir WCF web hizmeti nasıl gösterilen iki taraf arasında güvenli bir konuşma uygulayan bir TCP kanal bağlaması kullanılarak anlatılmaktadır.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a>Merhaba Service Bus NuGet paketi alma
Merhaba [Service Bus NuGet paketi](https://www.nuget.org/packages/WindowsAzure.ServiceBus) hello en kolay yolu tooget hello hizmet veri yolu API'sini ve tooconfigure tüm hello Service Bus bağımlılıklarıyla uygulamanızla olduğu. tooinstall hello NuGet paketini projenize, hello aşağıdaki:

1. Çözüm Gezgini'nde, **Başvurular**'a sağ tıklayın ve ardından **NuGet Paketlerini Yönet**'e tıklayın.
2. "Hizmet veri yolu" ve select hello arama **Microsoft Azure Service Bus** öğesi. Tıklatın **yükleme** toocomplete hello yükleme sonra Kapat iletişim kutusunda aşağıdaki hello:
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a>Kullanıma ve bir SOAP web hizmetini TCP ile kullanma
var olan WCF SOAP web hizmetini dış tüketim tooexpose, değişiklikleri toohello hizmet bağlamalarında ve adreslerinde olmanız gerekir. Bu değişiklikleri tooyour yapılandırma dosyası gerektirebilir veya nasıl, ayarladığınız ve WCF hizmetlerinizi yapılandırılmış bağlı olarak kod değişiklikleri gerektirebilir. WCF, toohave izin verildiğini unutmayın aynı hizmet üzerinden birden çok ağ uç nokta Merhaba, hello varolan koruyabileceğinizi dış geçiş uç noktaları ekleme çalışırken iç uç noktalar hello aynı erişim süresi.

Bu görevde, basit bir WCF hizmeti oluşturma ve aktarma dinleyici tooit ekleyin. Bu alıştırma Visual Studio aşina varsayar ve proje oluşturmanın tüm hello ayrıntılarını içermez. Bunun yerine, hello kodu odaklanır.

Bu adımları başlamadan önce ortamınızı yordamı tooset aşağıdaki hello tamamlayın:

1. Visual Studio içinde iki proje, "İstemci" ve "Hizmet" Merhaba çözümünde içeren bir konsol uygulaması oluşturun.
2. Merhaba Service Bus NuGet paketi tooboth projeleri ekleyin. Bu paket tüm hello gerekli derleme başvurularını tooyour projeleri ekler.

### <a name="how-toocreate-hello-service"></a>Nasıl toocreate hello hizmeti
İlk olarak hello hizmetin kendisini oluşturun. Tüm WCF hizmetleri en az üç farklı bölümden oluşur:

* Değiştirilen mesajları ve çağrılan toobe hangi işlemleridir açıklayan sözleşme tanımı.
* Bu sözleşmenin uygulaması.
* Merhaba WCF hizmetini barındıran ve birkaç uç noktalarını kullanıma sunar ana bilgisayar.

Bu bölümdeki Hello kod örnekleri bu bileşenlerin her birini adres.

Merhaba sözleşmesini tanımlayan tek bir işlem `AddNumbers`, iki sayı ekleyen ve hello sonucunu döndürür. Merhaba `IProblemSolverChannel` arabirimi etkinleştirir hello istemci toomore hello Ara sunucu ömrünü kolayca yönetin. Böyle bir arabirim oluşturmak en iyi uygulama olarak değerlendirilir. İyi bir fikir tooput olduğundan bu sözleşme tanımı ayrı bir dosyaya böylece bu dosyayı "İstemci" ve "Hizmet" projenizden başvurabilirsiniz ancak hello kodu her iki projeye de kopyalayabilirsiniz.

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

Merhaba sözleşme mevcutsa, hello uygulaması aşağıdaki gibidir:

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a>Hizmet ana bilgisayarını programlamayla yapılandırma
Merhaba sözleşme ve uygulama elverişli olduğunda, şimdi hello hizmeti barındırabilir. Barındırma oluşur içinde bir [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) nesnesi, hangi hello hizmet örneklerini yönetme mvc'deki ve ana hello iletiler için dinleme bitiş noktası. Merhaba aşağıdaki kodu hello hizmet normal yerel uç ve bir geçiş uç nokta tooillustrate hello görünümü, iç ve dış uç noktaların yan yana ile yapılandırır. Merhaba dizesini değiştirmek *ad alanı* ad alanındaki adla ve *yourKey* hello önceki Kurulum adımında elde hello SAS anahtarıyla.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();

sh.Close();
```

Merhaba üzerinde iki uç nokta oluşturma Hello örnekte, aynı sözleşme uygulama. Yerel biridir ve bir Azure geçiş aracılığıyla yansıtılır. Merhaba arasındaki temel farklılıklar hello bağlamaları değil; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) hello yerel için ve [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) hello geçiş uç nokta ve hello adresleri. Merhaba yerel uç nokta farklı bir bağlantı noktası ile yerel ağ adresine sahiptir. Merhaba geçiş endpoint sahip hello dizesi oluşan bir uç nokta adresi `sb`, ad alanı adı ve hello yolu "solver." Bu hello URI sonuçları `sb://[serviceNamespace].servicebus.windows.net/solver`, hello Hizmeti uç noktası (geçiş) Service Bus TCP uç noktası olarak tam bir dış DNS adı ile tanımlama. Merhaba yer tutucuları hello değiştirme hello kodu yerleştirin, `Main` hello işlevinin **hizmet** uygulama, işlevsel bir hizmet olacaktır. Merhaba geçiş üzerinde özel olarak, hizmet toolisten istiyorsanız hello yerel uç nokta bildirimini kaldırın.

### <a name="configure-a-service-host-in-hello-appconfig-file"></a>Merhaba App.config dosyasında bir hizmet ana bilgisayarı yapılandırma
Merhaba konak hello App.config dosyasını kullanarak da yapılandırabilirsiniz. kod bu durumda barındırma hello hizmet hello sonraki örnekte gösterilir.

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

Merhaba uç nokta tanımları hello App.config dosyasına taşınır. Merhaba NuGet paketi, Azure geçiş için gerekli hello yapılandırma uzantıları olan tanımları toohello App.config dosyasının bir aralık zaten eklemiştir. Merhaba hello tam örnek, hello önceki kod, denk doğrudan hello ögesinin altında görünmelidir **system.serviceModel** öğesi. Bu kod örneği, projenizin C# ad alanının **Hizmet** olarak adlandırıldığını varsayar.
Merhaba yer tutucuları, geçiş ad alanı adını ve SAS anahtarı ile değiştirin.

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

Bu değişiklikleri yaptıktan sonra hello hizmeti önce yaptığınız gibi ancak iki dinamik uç noktayla birlikte başlar: biri yerel ve bir hello bulutta dinleyen.

### <a name="create-hello-client"></a>Merhaba istemcisi oluşturma
#### <a name="configure-a-client-programmatically"></a>Programlama ile istemci yapılandırma
tooconsume hello hizmet kullanan bir WCF istemcisi oluşturmak bir [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) nesnesi. Service Bus, SAS kullanılarak uygulanan belirteç tabanlı bir güvenlik modeli kullanır. Merhaba [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) sınıfı, bazı iyi bilinen belirteç sağlayıcılarını döndüren, fabrikada yerleştirilen yöntemleri ile bir güvenlik belirteci sağlayıcısı gösterir. Merhaba aşağıdaki örnek kullanır hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) yöntemi toohandle hello hello uygun SAS belirteci alımını. Merhaba adı ve anahtarı hello önceki bölümde açıklandığı gibi hello portalından alınan dosyalardır.

İlk, başvuru veya kopyalama hello `IProblemSolver` istemci projenize hello hizmet kodundan sözleşme.

Merhaba hello kodda yerine `Main` hello istemci, geçiş ad alanı ve SAS anahtarı ile yeniden hello yer tutucu metin değiştirme yöntemi.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

Hello hizmet, bunları çalıştırmak ve hello istemci şimdi yapı (Merhaba hizmeti çalıştırın), ve hello istemci hello hizmetini çağırır ve yazdırır **9**. Merhaba istemci ve sunucu farklı makinelerde ağlarda bile çalıştırabilirsiniz ve hello iletişimi çalışmaya devam edecektir. Merhaba istemci kodu da hello Bulut veya yerel olarak çalıştırabilirsiniz.

#### <a name="configure-a-client-in-hello-appconfig-file"></a>Merhaba App.config dosyasında istemci yapılandırma
koddan hello nasıl tooconfigure hello istemcisini kullanarak hello App.config dosyasını gösterir.

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

Merhaba uç nokta tanımları hello App.config dosyasına taşınır. Merhaba hello kodu daha önce listelenen aynı hello olduğundan, aşağıdaki örnek, doğrudan hello altında görünmelidir `<system.serviceModel>` öğesi. Burada, önceki gibi hello yer tutucuları geçiş ad alanı ve SAS anahtarı ile değiştirin.

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a>Sonraki adımlar
Artık Azure geçiş hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.

* [Azure Geçiş nedir?](relay-what-is-it.md)
* [Azure Service Bus mimarisine genel bakış](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* Service Bus örneklerini indirin [Azure örneklerinden] [ Azure samples] veya hello bkz [Service Bus örneklerine genel bakış][overview of Service Bus samples].

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
