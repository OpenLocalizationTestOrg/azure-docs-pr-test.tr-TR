---
title: "aaaAzure Service Bus WCF geçişi Öğreticisi | Microsoft Docs"
description: "Service Bus istemci uygulaması ve hizmeti WCF geçiş kullanarak oluşturun."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a>Azure WCF geçiş Öğreticisi

Bu öğretici nasıl basit bir WCF toobuild geçiş açıklar istemci uygulaması ve Azure geçişi kullanarak hizmet. Kullanıldığı benzer bir öğretici [Service Bus Mesajlaşma hizmeti](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), bkz: [Service Bus kuyrukları ile çalışmaya başlama](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

Bu öğreticide, bir anlayış gerekli toocreate WCF geçiş istemcisi ve hizmet uygulaması hello adımları sağlar. Özgün WCF hizmetindeki benzerlerinde gibi bir hizmet her biri bir veya daha fazla hizmet işlemini kullanıma sunar, bir veya daha fazla uç noktaları, kullanıma sunan bir yapıdır. bir hizmetin Hello uç noktası hello hizmet bulunabileceği, bir adresi bir istemci hello hizmeti ve hello hizmet tooits istemciler tarafından sağlanan hello işlevselliği tanımlayan bir sözleşme ile iletişim kurması gereken hello bilgilerini içeren bir bağlama belirtir. WCF ve WCF geçiş arasındaki temel fark Hello bu hello uç bulutta hello yerine yerel olarak bilgisayarınızda kullanıma sunulan ' dir.

Bu öğreticideki konu başlıklarını hello sırasıyla çalıştıktan sonra çalışan bir hizmetiniz ve hello hizmet hello işlemlerini çağırabilen bir istemci sahip olacaktır. Merhaba ilk konu açıklar nasıl tooset bir hesap. Merhaba sonraki adımlar açıklanmaktadır nasıl toodefine bir hizmeti kullanan bir sözleşme, nasıl tooimplement hello hizmet ve nasıl tooconfigure hello kod hizmetinde. Ayrıca tanımladıkları nasıl toohost ve Çalıştır hello hizmeti. Merhaba oluşturan hizmet kendiliğinden barındırılır ve hello istemci ve hizmet çalışması üzerinde hello aynı bilgisayar. Merhaba hizmetini kodu veya bir yapılandırma dosyası kullanarak yapılandırabilirsiniz.

Hello son üç adımda toocreate bir istemci uygulaması hello istemci uygulamasını yapılandırma ve oluşturma ve hello işlevselliği hello konağının erişebileceği bir istemci kullanın açıklanmaktadır.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğreticiyi izleyerek hello gerekir:

* [Microsoft Visual Studio 2015 veya üzeri](http://visualstudio.com). Bu öğreticide Visual Studio 2017 kullanır.
* Etkin bir Azure hesabı. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir hesap oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/free/).

## <a name="create-a-service-namespace"></a>Hizmet ad alanı oluşturma

Merhaba ilk adımdır toocreate bir ad alanı ve tooobtain bir [paylaşılan erişim imzası (SAS)](../service-bus-messaging/service-bus-sas.md) anahtarı. Bir ad alanı aracılığıyla geçiş hizmetine hello kullanıma sunulan her uygulama için bir uygulama sınırı sağlar. Hizmet ad alanı oluşturulduğunda bir SAS anahtarı hello sistem tarafından otomatik olarak oluşturulur. Hizmet ad alanı ve SAS anahtarı birleşimi Hello Azure tooauthenticate erişim tooan uygulamanız için hello kimlik bilgileri sağlar. Merhaba izleyin [yönergeleri burada](relay-create-namespace-portal.md) toocreate geçiş ad alanı.

## <a name="define-a-wcf-service-contract"></a>WCF hizmet sözleşmesini tanımlama

Merhaba hizmet sözleşmesini hangi işlemleri (web hizmeti terminolojisi yöntemler ve işlevlere hello) hello hizmet destekler belirtir. Sözleşmeler; C++, C# veya Visual Basic arabirimi tanımlamasıyla oluşturulur. Merhaba arabirimdeki her yöntem tooa belirli hizmet işlemi karşılık gelir. Her bir arabirime hello olmalıdır [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) özniteliği uygulanan tooit ve her işlem hello olmalıdır [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) uygulanan öznitelik tooit. Bir yöntemi varsa hello içeren bir arabirimdeki [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) özniteliğinde hello yok [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) özniteliği, yöntem kullanıma sunulmaz. Bu görevler için Hello kodu aşağıdaki hello yordamın hello örnekte sağlanır. Sözleşmeler ve hizmetlere daha büyük bir tartışma için bkz: [Hizmetleri Tasarlama ve uygulama](https://msdn.microsoft.com/library/ms729746.aspx) hello WCF belgelerinde içinde.

### <a name="create-a-relay-contract-with-an-interface"></a>Geçiş sözleşme sahip bir arabirim oluşturma

1. Visual Studio Yönetici olarak açın hello hello programa sağ tıklayarak **Başlat** menü ve seçerek **yönetici olarak çalıştır**.
2. Yeni bir konsol uygulama projesi oluşturun. Merhaba tıklatın **dosya** menü ve seçin **yeni**, ardından **proje**. Merhaba, **yeni proje** iletişim kutusunda, tıklatın **Visual C#** (varsa **Visual C#** görüntülenmiyorsa, kısmına bakın **diğer diller**). Merhaba tıklatın **konsol uygulaması (.NET Framework)** şablonu ve adlandırın **EchoService**. Tıklatın **Tamam** toocreate hello projesi.

    ![][2]

3. Merhaba Service Bus NuGet paketini yükleyin. Bu paket otomatik olarak başvuruları toohello Service Bus kitaplıklarının yanı sıra hello WCF ekler **System.ServiceModel**. [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) tooprogrammatically erişim hello WCF'nin temel özelliklerine etkinleştirir hello ad alanıdır. Hizmet veri yolu hello nesnelerin çoğunu ve WCF toodefine Hizmet sözleşmeleri özniteliklerini kullanır.

    Çözüm Gezgini'nde, hello projesine sağ tıklayın ve ardından **NuGet paketlerini Yönet...** . Merhaba tıklatın **Gözat** sekmesini ve ardından arama `Microsoft Azure Service Bus`. Bu hello proje adı hello seçili olun **sürümler** kutusu. Tıklatın **yükleme**ve hello kullanım koşullarını kabul edin.

    ![][3]
4. Çözüm Gezgini'nde çift tıklayarak hello Program.cs dosyasının tooopen zaten değilse hello düzenleyicisinde açın.
5. Merhaba aşağıdakileri ekleyin hello hello dosya üstündeki deyimleri kullanarak:

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. Değişiklik hello ad alanı adı varsayılan **EchoService** çok**Microsoft.ServiceBus.Samples**.

   > [!IMPORTANT]
   > Bu öğretici hello C# ad alanı kullanır **Microsoft.ServiceBus.Samples**, yönetilen hello hello yapılandırma dosyasında kullanılan türü hello sözleşme tabanlı hello ad olduğu [hello WCF istemciyapılandırma](#configure-the-wcf-client) adım. Bu örneği derlemek istediğinizde herhangi bir ad alanı belirtebilirsiniz; Ancak, ardından hello sözleşme ve hizmet hello ad alanlarını uygun şekilde, hello uygulama yapılandırma dosyasında değiştirmediğiniz sürece hello öğretici çalışmaz. Merhaba App.config dosyası olmalıdır belirtilen hello ad hello aynı C# dosyalarınızda belirtilen hello ad alanı olarak.
   >
   >
7. Merhaba hemen sonra `Microsoft.ServiceBus.Samples` ad alanı bildirimi, ancak hello ad alanı içinde adlı yeni arabirimi tanımlayın `IEchoContract` ve hello geçerli `ServiceContractAttribute` ad alanı değerine sahip öznitelik toohello arabirimi `http://samples.microsoft.com/ServiceModel/Relay/`. Hello ad alanı değeri kodunuzu hello kapsam boyunca kullandığınız hello ad alanından farklıdır. Bunun yerine, başlangıç ad alanı değeri bu sözleşme için benzersiz bir tanımlayıcı olarak kullanılır. Hello ad alanını açıkça belirlemek hello varsayılan ad alanı değeri toohello sözleşme adına eklenmesini engeller. Koddan sonra hello ad alanı bildirimi hello yapıştırın:

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > Genellikle, hello hizmet sözleşmesi ad alanı sürüm bilgilerini içeren bir adlandırma şeması içerir. Hello hizmet sözleşmesi ad içinde sürüm bilgileri de dahil olmak üzere yeni bir ad alanı ile yeni bir hizmet sözleşmesi tanımlayarak ve yeni bir uç noktada kullanıma Hizmetleri tooisolate önemli değişiklikler sağlar. Bu şekilde, istemciler güncelleştirilmiş toobe gerek kalmadan toouse hello eski hizmet sözleşmelerini devam edebilirsiniz. Sürüm bilgileri, bir tarihten veya bir derleme numarasından oluşabilir. Daha fazla bilgi için bkz. [Hizmet Sürümü Oluşturma](http://go.microsoft.com/fwlink/?LinkID=180498). Bu öğreticinin Hello amaçları doğrultusunda, düzeni hello hizmet sözleşmesi ad alanının adlandırma hello sürüm bilgilerini içermiyor.
   >
   >
8. Merhaba içinde `IEchoContract` arabirim, hello tek bir işlem hello için bir yöntem bildirin `IEchoContract` sözleşme çıkarır hello içinde arabirim ve hello geçerli `OperationContractAttribute` parçası olarak tooexpose istediğiniz özniteliği toohello yöntemi hello ortak WCF geçiş , aşağıdaki gibi Sözleşme:

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. Merhaba hemen sonra `IEchoContract` arabirim tanımı, hem de devralan bir kanal bildirin `IEchoContract` ve ayrıca toohello `IClientChannel` arabirimi, aşağıda gösterildiği gibi:

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    Bir kanal üzerinden hello ana bilgisayar ve istemci bilgileri tooeach diğer kullandıkları hello WCF nesnesidir. Daha sonra hello kanal tooecho bilgileri hello iki uygulama arasındaki karşı kod yazacaksınız.
10. Hello gelen **yapı** menüsünde tıklatın **Çözümü Derle** veya basın **Ctrl + Shift + B** tooconfirm hello çalışmanızın o ana kadarki doğruluğunu.

### <a name="example"></a>Örnek

koddan hello WCF geçiş sözleşmesini tanımlayan temel bir arabirimi gösterir.

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Merhaba arabirimi oluşturulur, hello arabirimi uygulayabilirsiniz.

## <a name="implement-hello-wcf-contract"></a>Uygulama hello WCF Sözleşmesi

Bir Azure geçişi oluşturmak için öncelikle bir arabirim kullanılarak tanımlanan hello sözleşmeyi oluşturmanız gerekir. Merhaba arabirimi oluşturma hakkında daha fazla bilgi için hello önceki adıma bakın. Merhaba sonraki adıma tooimplement hello arabirimidir. Bu adlı bir sınıf oluşturursunuz `EchoService` hello kullanıcı tanımlı uygulayan `IEchoContract` arabirimi. Merhaba arabirimi uyguladıktan sonra bir App.config yapılandırma dosyası kullanarak hello arabirimi ardından yapılandırın. Merhaba yapılandırma dosyası hello hello hizmetin adını, hello adını hello sözleşme ve hello geçiş hizmeti ile kullanılan toocommunicate Protokolü hello türü gibi hello uygulama için gerekli bilgileri içerir. Bu görevler için kullanılan hello kod aşağıdaki hello yordamın hello örnekte sağlanır. Nasıl tooimplement hizmet sözleşme hakkında daha fazla genel bilgi için bkz: [hizmet sözleşmelerini uygulama](https://msdn.microsoft.com/library/ms733764.aspx) hello WCF belgelerinde içinde.

1. Adlı yeni bir sınıf oluşturun `EchoService` hello hello tanımını hemen sonra `IEchoContract` arabirimi. Merhaba `EchoService` sınıfı uygulayan hello `IEchoContract` arabirimi.

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    Benzer tooother arabirim uygulamaları, farklı bir dosyada hello tanımı uygulayabilirsiniz. Ancak, Bu öğretici için hello uygulama aynı dosya hello arabirim tanımı ve hello hello bulunan `Main` yöntemi.
2. Merhaba uygulamak [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) toohello özniteliği `IEchoContract` arabirimi. Merhaba özniteliği hello hizmet adı ve ad alanını belirtir. Bunu yaptıktan sonra hello `EchoService` sınıfı şu şekilde görünür:

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. Uygulama hello `Echo` hello tanımlanmış yöntemi `IEchoContract` hello arabiriminde `EchoService` sınıfı.

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. Tıklatın **yapı**, ardından **yapı çözümü** tooconfirm hello çalışmanızın doğruluğunu.

### <a name="define-hello-configuration-for-hello-service-host"></a>Hello hizmet ana bilgisayarı için başlangıç yapılandırmasını tanımlama

1. Merhaba yapılandırma dosyası çok benzer tooa WCF yapılandırma dosyasıdır. Merhaba hizmet adı, uç noktayı (istemcilerin ve ana bilgisayarların birbirleriyle toocommunicate için Azure geçiş gösteren başka bir deyişle, hello konum) içerir ve hello bağlama (kullanılan toocommunicate Protokolü hello türü). Merhaba ana bu yapılandırılan hizmet uç noktasının tooa başvuruyor farktır [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) hello .NET Framework parçası olmayan bağlama. [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) hello hizmeti tarafından tanımlanan hello bağlamaları biridir.
2. İçinde **Çözüm Gezgini**, hello App.config dosyası tooopen çift tıklayın, hello Visual Studio düzenleyicisinde.
3. Merhaba, `<appSettings>` öğesi hello yer tutucuları hizmet ad alanınızın hello adıyla değiştirin ve hello bir önceki adımda kopyaladığınız SAS anahtarı.
4. Merhaba içinde `<system.serviceModel>` etiketler eklemek bir `<services>` öğesi. Bir tek yapılandırma dosyasında birden çok geçiş uygulamaları tanımlayabilirsiniz. Ancak bu öğreticide yalnızca bir adet tanımlanır.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. Merhaba içinde `<services>` öğesi ekleme bir `<service>` öğesi toodefine hello hello hizmetin adını.

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. Merhaba içinde `<service>` öğesi hello uç nokta sözleşmesinin hello konumunu tanımlayın ve ayrıca hello endpoint yönelik bağlama türünü hello.

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    Hello endpoint hello istemci hello ana bilgisayar uygulamasını nerede arayacağını tanımlar. Daha sonra bu adım toocreate tam olarak hello konak Azure geçiş aracılığıyla kullanıma sunan bir URI hello öğretici kullanır. Merhaba bağlama TCP protokolü toocommunicate hello geçiş hizmeti ile Merhaba gibi kullanıyoruz olduğunu bildirir.
7. Merhaba gelen **yapı** menüsünde tıklatın **yapı çözümü** tooconfirm hello çalışmanızın doğruluğunu.

### <a name="example"></a>Örnek

Merhaba aşağıdaki kod hello hizmet sözleşmesini hello uyarlamasını gösterir.

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

Merhaba aşağıdaki kod hello hello hizmet ana bilgisayarı ile ilişkilendirilen hello App.config dosyasının temel biçimini gösterir.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a>Hizmet barındırma ve temel bir web hizmeti tooregister hello geçiş ile çalıştırma

Bu adım nasıl toorun Azure geçiş açıklar hizmet.

### <a name="create-hello-relay-credentials"></a>Merhaba geçiş kimlik bilgileri oluşturun

1. İçinde `Main()`, hangi toostore hello ad alanında iki değişkeni oluşturun ve hello hello konsol penceresinden okunan SAS anahtarı.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    Merhaba SAS anahtar projeniz kullanılan sonraki tooaccess olacaktır. Merhaba ad alanı bir parametre olarak geçirilen çok`CreateServiceUri` toocreate hizmet URI'si.
2. Kullanarak bir [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) nesne, hello kimlik bilgisi türü olarak bir SAS anahtarı kullanarak bildirin. Merhaba doğrudan hello son adımda eklediğiniz hello koddan sonra aşağıdaki kodu ekleyin.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a>Merhaba hizmeti için bir taban adresi oluşturma

Merhaba son adımda eklediğiniz hello koddan sonra oluşturma bir `Uri` hello hizmeti hello temel adres için örneği. Bu URI hello Service Bus şemasını, başlangıç ad alanı ve hello hizmet arabirimi hello yolunu belirtir.

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

"sb" ifadesinin kısaltmasıdır hello Service Bus şeması için ve biz hello protokol olarak TCP kullanıyoruz gösterir. Bu aynı zamanda daha önce hello yapılandırma dosyasında belirtilir zaman [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) olarak hello bağlama belirtildi.

Bu öğretici için hello URI'dir `sb://putServiceNamespaceHere.windows.net/EchoService`.

### <a name="create-and-configure-hello-service-host"></a>Oluşturma ve hello hizmet ana bilgisayarı yapılandırma

1. Merhaba bağlantı modunu çok ayarlamak`AutoDetect`.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    Merhaba Protokolü hello hizmeti kullanan toocommunicate hello geçiş hizmeti ile Merhaba bağlantı modunu açıklar; HTTP veya TCP. Merhaba varsayılan ayarı kullanarak `AutoDetect`, hello hizmeti çalışır tooconnect tooAzure geçiş kullanılabilir durumdaysa TCP ve HTTP üzerinden TCP kullanılabilir değilse. Bu hello Protokolü hello hizmetinden farklıdır Not istemci iletişimi için belirtir. Bu protokol, kullanılan hello bağlama tarafından belirlenir. Örneğin, bir hizmet hello kullanabilirsiniz [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) , uç noktasında istemcileriyle HTTP üzerinden iletişim kurduğu bağlama. Aynı hizmeti belirtebilirsiniz **ConnectivityMode.AutoDetect** hello hizmeti ile Azure geçişi TCP üzerinden iletişim kurar.
2. Bu bölümde daha önce oluşturulan URI hello kullanarak hello hizmet ana bilgisayarını oluşturun.

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    Merhaba hizmet konağı hello hizmeti başlatır hello WCF nesnesidir. Merhaba türü geçirdiğiniz burada toocreate istediğiniz hizmet (bir `EchoService` türü) ve ayrıca istediğiniz tooexpose hello hizmet toohello adresi.
3. Merhaba Program.cs dosyasının Hello üstünde çok başvurular ekleyin[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) ve [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. Geri `Main()`, hello uç nokta tooenable genel erişim yapılandırın.

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    Bu adımı uygulamanız genel olarak hello ATOM akışı projeniz için inceleyerek bulunabileceğini hello geçiş hizmeti bildirir. Ayarlarsanız **DiscoveryType** çok**özel**, bir istemci mümkün tooaccess hello hizmeti olması. Ancak, hello geçiş ad alanı aradığında hello hizmet görünmez. Bunun yerine, hello istemci tooknow hello bitiş noktası yolu oluşturmanız gerekir.
5. Uygulama hello hizmeti kimlik bilgileri hello App.config dosyasında tanımlanan toohello hizmet uç noktaları:

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    Merhaba önceki adımda belirtildiği gibi birden çok hizmet ve uç noktaları hello yapılandırma dosyasında bildirilen. Bildirirseniz Bu kod hello yapılandırma dosyasını ve arama çapraz her uç nokta toowhich için kimlik bilgilerinizi uygulamalıdır. Ancak, bu öğreticide, tek bir uç nokta hello yapılandırma dosyası vardır.

### <a name="open-hello-service-host"></a>Açık hello hizmet konağı

1. Merhaba hizmeti açın.

    ```csharp
    host.Open();
    ```
2. Hizmet hello hello kullanıcı çalıştıran ve açıklayan bilgilendirmek nasıl tooshut hello hizmeti kapalı.

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. Tamamlandığında, hello hizmet ana bilgisayarını kapatın.

    ```csharp
    host.Close();
    ```
4. Tuşuna **Ctrl + Shift + B** toobuild hello projesi.

### <a name="example"></a>Örnek

Tamamlanmış hizmet kodunuzun şu şekilde görünmelidir. ana bilgisayar hizmeti bir konsol uygulamasında hello ve Hello kod hello öğreticide hello hizmet sözleşmesini ve önceki adımları içerir.

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a>Merhaba hizmet sözleşmesi için bir WCF istemcisi oluşturma

Merhaba sonraki adımı toocreate bir istemci uygulaması ve daha sonraki adımlarda gerçekleştireceksiniz hello hizmet sözleşmesini tanımlama. Bu adımların hello adımlara benzer olduğunu unutmayın kullanılan toocreate hizmet: bir App.config düzenleme sözleşme tanımlama, kimlik bilgileri tooconnect toohello geçişi hizmetini kullanma vb.. Bu görevler için kullanılan hello kod aşağıdaki hello yordamın hello örnekte sağlanır.

1. Merhaba aşağıdakileri yaparak hello geçerli Visual Studio çözümüne hello istemci için yeni bir proje oluşturun:

   1. Çözüm Gezgini'nde, buna hello hello hizmeti içeren aynı çözüm, hello geçerli çözüme (Merhaba proje değil) sağ tıklayın ve **Ekle**. Ardından **Yeni Proje**'ye tıklayın.
   2. Merhaba, **Yeni Proje Ekle** iletişim kutusu, tıklatın **Visual C#** (varsa **Visual C#** görüntülenmiyorsa, kısmına bakın **diğer diller**) seçin hello **Konsol uygulaması (.NET Framework)** şablonu ve adlandırın **EchoClient**.
   3. **Tamam** düğmesine tıklayın.
      <br />
2. Çözüm Gezgini'nde hello hello Program.cs dosyasına çift tıklayarak **EchoClient** proje tooopen zaten değilse hello düzenleyicisinde açın.
3. Değişiklik hello ad alanı adı varsayılan `EchoClient` çok`Microsoft.ServiceBus.Samples`.
4. Merhaba yüklemek [Service Bus NuGet paketi](https://www.nuget.org/packages/WindowsAzure.ServiceBus): hello Çözüm Gezgini'nde sağ **EchoClient** proje ve ardından **NuGet paketlerini Yönet**. Merhaba tıklatın **Gözat** sekmesini ve ardından arama `Microsoft Azure Service Bus`. Tıklatın **yükleme**ve hello kullanım koşullarını kabul edin.

    ![][3]
5. Ekleme bir `using` hello bildirimi [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) hello Program.cs dosyasındaki ad alanı.

    ```csharp
    using System.ServiceModel;
    ```
6. Hello hizmet sözleşmesi tanımını toohello ad hello aşağıdaki örnekte gösterildiği gibi ekleyin. Bu tanım hello kullanılan aynı toohello tanımını olduğuna dikkat edin **hizmet** projesi. Bu kod hello hello üstünde eklemelisiniz `Microsoft.ServiceBus.Samples` ad alanı.

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. Tuşuna **Ctrl + Shift + B** toobuild hello istemci.

### <a name="example"></a>Örnek

Merhaba aşağıdaki kod hello Program.cs dosyasının geçerli durumunu hello hello gösterir **EchoClient** projesi.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a>Merhaba WCF istemcisini yapılandırma

Bu adımda, daha önce bu öğreticide oluşturduğunuz hello hizmete erişen temel istemci uygulamasına yönelik bir App.config dosyası oluşturun. Bu App.config dosyası hello sözleşme, bağlama ve hello uç noktanın adı tanımlar. Bu görevler için kullanılan hello kod aşağıdaki hello yordamın hello örnekte sağlanır.

1. Çözüm Gezgini'nde, hello **EchoClient** projesi, çift **App.config** tooopen hello dosyasını hello Visual Studio düzenleyicisinde.
2. Merhaba, `<appSettings>` öğesi hello yer tutucuları hizmet ad alanınızın hello adıyla değiştirin ve hello bir önceki adımda kopyaladığınız SAS anahtarı.
3. Add Hello system.serviceModel öğesi içinde bir `<client>` öğesi.

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    Bu adım ile WCF stilinde istemci uygulaması tanımladığınızı bildirirsiniz.
4. Merhaba içinde `client` öğesi hello adı, sözleşmeyi ve hello uç noktası için bağlama türünü tanımlayın.

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    Bu adım hello uç noktası, hello hizmeti ve Merhaba istemci uygulaması ile Azure geçişi TCP toocommunicate kullandığını hello olgu tanımlanan hello sözleşme hello adını tanımlar. Merhaba uç nokta adı kullanılan hello toolink Bu uç nokta yapılandırması hello hizmet URI'si ile sonraki adım.
5. Tıklatın **dosya**, ardından **Tümünü Kaydet**.

## <a name="example"></a>Örnek

Merhaba aşağıdaki kodu hello Echo istemciye için hello App.config dosyasını gösterir.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a>Uygulama hello WCF istemcisi
Bu adımda, bu öğreticide daha önce oluşturduğunuz hello hizmete erişen bir temel istemci uygulaması uygulayın. Benzer toohello hizmeti hello istemci hello çoğunu gerçekleştirir aynı işlemleri tooaccess Azure geçişi:

1. Merhaba bağlantı modunu ayarlar.
2. Merhaba hello ana bilgisayar hizmetinin yer URI oluşturur.
3. Merhaba güvenlik kimlik bilgilerini tanımlar.
4. Merhaba kimlik bilgilerini toohello bağlantı geçerlidir.
5. Merhaba bağlantı açar.
6. Merhaba uygulamaya özgü görevleri gerçekleştirir.
7. Merhaba bağlantıyı kapatır.

Merhaba hizmeti bir çağrı çok kullanır ancak bununla birlikte, hello temel farklar Merhaba istemci uygulaması bir kanal tooconnect toohello geçiş hizmetini kullanan biri**ServiceHost**. Bu görevler için kullanılan hello kod aşağıdaki hello yordamın hello örnekte sağlanır.

### <a name="implement-a-client-application"></a>Bir istemci uygulaması kullanma
1. Merhaba bağlantı modunu çok ayarlamak**otomatik algıla**. Merhaba içindeki kodu aşağıdaki hello eklemek `Main()` hello yöntemi **EchoClient** uygulama.

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. Merhaba konsoldan okunan değişkenleri toohold hello değerleri hello hizmet ad alanı ve SAS anahtarı tanımlayın.

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. Merhaba geçiş projenizde hello konak hello konumunu tanımlayan URI oluşturun.

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. Hizmet ad alanı uç noktanız için Hello kimlik bilgisi nesnesi oluşturun.

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. Merhaba App.config dosyasında açıklanan hello yapılandırmayı yükleyen hello kanal fabrikası oluşturun.

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    Kanal fabrikası üzerinden hello hizmet ve istemci uygulamaları iletişim kanalı oluşturan WCF nesnesidir.
6. Merhaba kimlik bilgileri geçerli.

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. Oluşturun ve hello kanal toohello hizmeti açın.

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. Merhaba temel kullanıcı arabirimini ve hello Yankı için işlevselliği yazma.

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    Merhaba kod bir proxy olarak hello hello kanal nesnesinin örneğini hello hizmeti için kullandığını unutmayın.
9. Merhaba kanal ve Kapat hello Fabrika kapatın.

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a>Örnek

Tamamlanan kodu aşağıdaki gibi görünmelidir nasıl toocreate bir istemci uygulaması, nasıl toocall hello hello hizmet işlemlerini ve nasıl tooclose hello istemci hello işleminden sonra çağrı gösteren tamamlandı.

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a>Merhaba uygulamaları çalıştırma

1. Tuşuna **Ctrl + Shift + B** toobuild hello çözümü. Bu, hello istemci projesi ve hello önceki adımlarda oluşturduğunuz hello hizmet projesi oluşturur.
2. Önce çalışan hello istemci uygulama, hello hizmet uygulamasının çalıştığından emin olmanız gerekir. Visual Studio'da Çözüm Gezgini'nde hello sağ **EchoService** çözüm, ardından **özellikleri**.
3. Merhaba çözüm Özellikleri iletişim kutusunda, tıklatın **başlangıç projesi**, hello ardından **birden fazla başlangıç projesi** düğmesi. Emin olun **EchoService** hello listede ilk olarak görünür.
4. Set hello **eylem** hem hello kutusunu **EchoService** ve **EchoClient** çok projeleri**Başlat**.

    ![][5]
5. **Proje Bağımlılıkları**'na tıklayın. Merhaba, **projeleri** kutusunda **EchoClient**. Merhaba, **bağlıdır** kutusunda, emin olun **EchoService** denetlenir.

    ![][6]
6. Tıklatın **Tamam** toodismiss hello **özellikleri** iletişim.
7. Tuşuna **F5** toorun her iki proje.
8. Her iki konsol penceresi açın ve hello ad alanı adı ister. Merhaba hizmeti ilk olarak, bunu hello içinde çalıştırılmalıdır **EchoService** konsol penceresinde, hello ad girin ve ardından basın **Enter**.
9. Ardından SAS anahtarınız istenir. Merhaba SAS anahtarını girin ve ENTER tuşuna basın.

    Burada, hello konsol penceresinden örnek çıktı verilmiştir. Örneğin yalnızca amaçları şunlardır Hello değerleri sağlanan unutmayın.

    `Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`

    Merhaba hizmet uygulaması toohello konsol penceresinde hello adresi üzerinde dinleme yaptığı, aşağıdaki örneğine hello görülen yazdırır.

    `Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`
10. Merhaba, **EchoClient** konsol penceresinde, girin hello hello hizmet uygulaması için daha önce girdiğiniz aynı bilgileri. Merhaba önceki adımları tooenter hello izleyin aynı hizmet ad alanı ve SAS anahtarı Merhaba istemci uygulaması için değerler.
11. Bu değerleri girdikten sonra hello istemci kanal toohello hizmet açar ve hello aşağıdaki konsol çıktısı örneğinde görüldüğü şekilde bazı metinler, tooenter ister.

    `Enter text tooecho (or [Enter] tooexit):`

    Bazı metin toosend toohello hizmet uygulaması girin ve Enter tuşuna basın. Bu metin toohello hizmeti hello Echo hizmet işlemi aracılığıyla gönderilir ve hello hizmet konsol penceresinde hello örnek çıktı aşağıdaki gibi görünür.

    `Echoing: My sample text`

    Merhaba istemci uygulaması hello hello dönüş değerini alan `Echo` hello orijinal metni alır ve bunu yazdıran işlemi tooits konsol penceresinde. Merhaba, hello istemci konsol penceresinden örnek çıktı verilmiştir.

    `Server echoed: My sample text`
12. Bu şekilde hello istemci toohello hizmetinden metin iletileri göndermeye devam edebilirsiniz. İşiniz bittiğinde, içinde hello istemci ve hizmet Konsolu windows tooend her iki uygulamayı basın.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğretici, Service Bus WCF geçiş yeteneklerine toobuild Azure geçiş istemci uygulaması ve hizmeti kullanılarak nasıl hello gösterdi. Kullanıldığı benzer bir öğretici [Service Bus Mesajlaşma hizmeti](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), bkz: [Service Bus kuyrukları ile çalışmaya başlama](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).

toolearn Azure geçişi hakkında daha fazla bilgi aşağıdaki konularda hello bakın.

* [Azure Service Bus mimarisine genel bakış](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [Azure Geçiş’e genel bakış](relay-what-is-it.md)
* [Toouse hello WCF hizmeti .NET ile nasıl geçiş](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
