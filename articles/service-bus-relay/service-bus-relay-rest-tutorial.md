---
title: "Azure geçişi kullanarak aaaService Bus REST Öğreticisi | Microsoft Docs"
description: "REST tabanlı bir arabirimi kullanıma sunan basit bir Azure Service Bus geçişi ana bilgisayar uygulaması derleyin."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a>Azure WCF geçişi REST Öğreticisi

Bu öğretici toobuild basit bir Azure geçişi REST tabanlı bir arabirimi kullanıma sunan uygulama nasıl ana bilgisayar açıklar. REST, HTTP üzerinden Service Bus API'lerine istekleri tooaccess hello bir web tarayıcısı gibi bir web istemcisi sağlar.

Merhaba öğretici, Service Bus hello Windows Communication Foundation (WCF) REST programlama modeli tooconstruct bir REST hizmeti kullanır. Daha fazla bilgi için bkz: [WCF REST programlama modeli](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) ve [Hizmetleri Tasarlama ve uygulama](/dotnet/framework/wcf/designing-and-implementing-services) hello WCF belgelerinde içinde.

## <a name="step-1-create-a-namespace"></a>1. Adım: Ad alanı oluşturma

Merhaba Azure geçiş özelliklerinde toobegin kullanarak, öncelikle bir hizmet ad alanı oluşturmanız gerekir. Ad alanı, uygulamanızda bulunan Azure kaynaklarını adreslemek için içeriğin kapsamını belirleyen bir kapsayıcı sunar. Merhaba izleyin [yönergeleri burada](relay-create-namespace-portal.md) toocreate geçiş ad alanı.

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a>2. adım: bir REST tabanlı WCF Hizmeti sözleşmesi toouse Azure geçiş ile tanımlama

WCF REST tarzı bir hizmete oluşturduğunuzda, hello sözleşme tanımlamanız gerekir. ana bilgisayar destekler ne gibi işlemler hello Hello sözleşme belirtir. Bir hizmet işlemi, web hizmeti yöntemi olarak düşünülebilir. Sözleşmeler; C++, C# veya Visual Basic arabirimi tanımlamasıyla oluşturulur. Merhaba arabirimdeki her yöntem tooa belirli hizmet işlemi karşılık gelir. Merhaba [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) özniteliği uygulanan tooeach arabirimi ve gerekir hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) özniteliği uygulanan tooeach işlemi olmalıdır. Bir yöntemi varsa hello içeren bir arabirimdeki [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) hello yok [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), yöntem kullanıma sunulmaz. Bu görevler için kullanılan hello kodu aşağıdaki hello yordamın hello örnekte gösterilir.

Merhaba WCF sözleşmesi ve REST stili sözleşmesi arasındaki birincil fark olan bir özellik toohello hello eklenmesi [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx). Bu özellik arabirimi tooa yönteminizi hello üzerinde yönteminde toomap diğer tarafını hello arabirimi sağlar. Bu durumda, kullanacağız [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink yöntemi tooHTTP alın. Bu hizmet tooaccurately almak ve toohello arabirimi gönderilen komutları yorumlama veri yolu sağlar.

### <a name="toocreate-a-contract-with-an-interface"></a>toocreate bir arabirim ile bir sözleşme

1. Visual Studio'yu yönetici olarak açın: hello sağ hello programında **Başlat** menüsüne ve ardından **yönetici olarak çalıştır**.
2. Yeni bir konsol uygulama projesi oluşturun. Hello tıklatın **dosya** menü ve select **yeni**seçeneğini belirleyip **proje**. Merhaba, **yeni proje** iletişim kutusu, tıklatın **Visual C#**seçin hello **konsol uygulaması** şablonu ve adlandırın **Imagelistener**. Merhaba varsayılan kullanmak **konumu**. Tıklatın **Tamam** toocreate hello projesi.
3. Visual Studio, bir C# projesi için `Program.cs` dosyası oluşturur. Bu sınıf, boş bir içerir `Main()` yöntemi, bir konsol uygulama projesi toobuild için doğru gerekli.
4. Başvuruları tooService veri yolu ekleyin ve **System.ServiceModel.dll** hello Service Bus NuGet paketini yükleyerek toohello projesi. Bu paket otomatik olarak başvuruları toohello Service Bus kitaplıklarının yanı sıra hello WCF ekler **System.ServiceModel**. Çözüm Gezgini'nde hello sağ **Imagelistener** proje ve ardından **NuGet paketlerini Yönet**. Merhaba tıklatın **Gözat** sekmesini ve ardından arama `Microsoft Azure Service Bus`. Tıklatın **yükleme**ve hello kullanım koşullarını kabul edin.
5. Bir başvuru çok açıkça eklemeniz gerekir**System.ServiceModel.Web.dll** toohello proje:
   
    a. Çözüm Gezgini'nde hello sağ **başvuruları** hello proje klasörünü ve ardından altında bir klasör **Başvuru Ekle**.
   
    b. Merhaba, **Başvuru Ekle** iletişim kutusunda, hello **Framework** sekmesinde hello sol taraftaki ve hello **arama** kutusuna **System.ServiceModel.Web** . Select hello **System.ServiceModel.Web** onay kutusunu işaretleyin ve ardından **Tamam**.
6. Merhaba aşağıdakileri ekleyin `using` deyimleri hello Program.cs dosyasının hello üstünde.
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) WCF programlı erişim toobasic özellikleri etkinleştirir hello ad alanıdır. WCF geçiş hello nesnelerin çoğunu ve WCF toodefine Hizmet sözleşmeleri özniteliklerini kullanır. Geçiş uygulamalarınızın çoğunda bu ad alanı kullanır. Benzer şekilde, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) yardımcı Azure geçişi ve hello istemci web tarayıcısı ile iletişim hello nesne hello kanal tanımlayın. Son olarak, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) toocreate web tabanlı uygulamalar sağlayan hello türler içerir.
7. Merhaba yeniden adlandırma `ImageListener` ad alanı çok**Microsoft.ServiceBus.Samples**.
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. Doğrudan hello ad alanı bildiriminin büyük ayracını açma hello sonra adlı yeni arabirimi tanımlayın **Iımagecontract** ve hello geçerli **ServiceContractAttribute** özniteliği toohello arabirimi ile bir değeri `http://samples.microsoft.com/ServiceModel/Relay/`. Hello ad alanı değeri kodunuzu hello kapsam boyunca kullandığınız hello ad alanından farklıdır. Merhaba ad alanı değeri bu sözleşme için benzersiz bir tanımlayıcı olarak kullanılır ve sürüm bilgisini içermelidir. Daha fazla bilgi için bkz. [Hizmet Sürümü Oluşturma](http://go.microsoft.com/fwlink/?LinkID=180498). Hello ad alanını açıkça belirlemek hello varsayılan ad alanı değeri toohello sözleşme adına eklenmesini engeller.
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. Merhaba içinde `IImageContract` arabirim, hello tek bir işlem hello için bir yöntem bildirin `IImageContract` sözleşme çıkarır hello içinde arabirim ve hello geçerli `OperationContractAttribute` özniteliği hello genel hizmet veri yolu bir parçası olarak tooexpose istediğiniz toohello yöntemi Sözleşme.
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. Merhaba, **OperationContract** özniteliği, hello eklemek **WebGet** değeri.
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    Geçiş hizmeti tooroute HTTP GET istekleri çok etkinleştirir hello bunları yapmak`GetImage`ve dönüş değerleri, tootranslate hello `GetImage` HTTP GETRESPONSE yanıtına içine. Daha sonra hello öğreticide, bir web tarayıcısı tooaccess bu yöntem ve toodisplay hello görüntü hello tarayıcıda kullanacaksınız.
11. Merhaba hemen sonra `IImageContract` tanımı, her iki hello devralan bir kanal bildirin `IImageContract` ve `IClientChannel` arabirimleri.
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    Bir kanal üzerinden hello hizmet ve istemci bilgileri tooeach diğer kullandıkları hello WCF nesnesidir. Daha sonra ana bilgisayar uygulamanızda hello kanalı oluşturur. Azure geçişi, ardından bu kanal toopass hello HTTP GET isteklerine hello tarayıcı tooyour kullanır **Getımage** uygulaması. Merhaba geçiş de hello kanal tootake hello kullanır **Getımage** dönüş değeri ve hello istemci tarayıcısı için HTTP GetResponse çevir.
12. Merhaba gelen **yapı** menüsünde tıklatın **yapı çözümü** tooconfirm hello çalışmanızın o ana kadarki doğruluğunu.

### <a name="example"></a>Örnek
koddan hello WCF geçiş sözleşmesini tanımlayan temel bir arabirimi gösterir.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a>Adım 3: REST tabanlı WCF Hizmeti sözleşmesi toouse Service Bus uygulayın
REST stilinde WCF geçiş hizmeti oluşturmak için öncelikle bir arabirim kullanılarak tanımlanan hello sözleşmeyi oluşturmanız gerekir. Merhaba sonraki adıma tooimplement hello arabirimidir. Bu adlı bir sınıf oluşturursunuz **Imageservice** hello kullanıcı tanımlı uygulayan **Iımagecontract** arabirimi. Merhaba sözleşmeyi uyguladıktan sonra bir App.config dosyası kullanarak hello arabirimi ardından yapılandırın. Merhaba yapılandırma dosyası hello hello hizmetin adını, hello adını hello sözleşme ve hello geçiş hizmeti ile kullanılan toocommunicate Protokolü hello türü gibi hello uygulama için gerekli bilgileri içerir. Bu görevler için kullanılan hello kod aşağıdaki hello yordamın hello örnekte sağlanır.

Olarak hello önceki adımlara REST stilinde sözleşme ve WCF geçiş sözleşmesi uygulama arasında çok az fark yoktur.

### <a name="tooimplement-a-rest-style-service-bus-contract"></a>tooimplement REST stilinde Service Bus Sözleşmesi
1. Adlı yeni bir sınıf oluşturun **Imageservice** hello hello tanımını hemen sonra **Iımagecontract** arabirimi. Merhaba **Imageservice** sınıfı uygulayan hello **Iımagecontract** arabirimi.
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    Benzer tooother arabirim uygulamaları, farklı bir dosyada hello tanımı uygulayabilirsiniz. Ancak, Bu öğretici için hello uygulama aynı dosya hello arabirim tanımı hello görünür ve `Main()` yöntemi.
2. Merhaba uygulamak [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) toohello özniteliği **ServiceBehaviorAttribute** sınıfı hello sınıfı tooindicate WCF sözleşmesinin bir uygulamasıdır.
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    Önceden belirtildiği gibi bu ad alanı, geleneksel bir ad alanı değildir. Bunun yerine, hello hello sözleşmeyi tanımlayan WCF mimarisinin bir parçasıdır. Daha fazla bilgi için bkz: Merhaba [veri sözleşmesi adları](https://msdn.microsoft.com/library/ms731045.aspx) hello WCF belgelerinde konuda.
3. Bir .jpg görüntüsü tooyour proje ekleyin.  
   
    Bu tarayıcı alma hello hello hizmet görüntüleyen bir resimdir. Projenize sağ tıklayın ve ardından **Ekle**'ye tıklayın. Ardından **Var Olan Öğe**'ye tıklayın. Kullanım hello **varolan öğeyi Ekle** iletişim kutusu toobrowse tooan .jpg uygun ve ardından **Ekle**.
   
    Merhaba dosya eklerken emin olun **tüm dosyaları** hello aşağı açılan liste sonraki toohello seçili **dosya adı:** alan. Bu öğreticinin geri kalanını Hello varsayar bu hello "image.jpg" Merhaba görüntü adıdır. Farklı bir dosya varsa, toorename hello görüntüsü olması veya kod toocompensate değiştirmek.
4. toomake hizmetini çalıştıran bu hello bulabilir hello resim dosyası olarak emin **Çözüm Gezgini** hello görüntü dosyasına sağ tıklayın ve ardından **özellikleri**. Merhaba, **özellikleri** kümesi bölmesi, **tooOutput dizin kopyalama** çok**yeniyse Kopyala**.
5. Bir başvuru toohello ekleme **System.Drawing.dll** derleme toohello proje ve ilişkili hello aşağıdaki eklemek `using` deyimleri.  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. Merhaba, **Imageservice** sınıfı, eklemek isteğe bağlı olarak yükleri hello bit eşlem ve toosend hazırlar Oluşturucusu toohello istemci tarayıcısına hello.
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. Merhaba önceki kod, hemen sonra hello aşağıdakileri ekleyin **Getımage** hello yönteminde **Imageservice** hello görüntüsünü içeren sınıf tooreturn bir HTTP iletisi.
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    Bu uygulama kullanan **MemoryStream** tooretrieve hello görüntü ve toohello tarayıcı akış için hazırlayın. Merhaba akış noktasını sıfırdan başlatır, hello akış içeriğini .JPEG olarak bildirir ve hello bilgileri akışa sunar.
8. Merhaba gelen **yapı** menüsünde tıklatın **yapı çözümü**.

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a>Service Bus hello web hizmetini çalıştırmak için toodefine hello yapılandırma
1. İçinde **Çözüm Gezgini**, çift **App.config** tooopen onu hello Visual Studio düzenleyicisinde.
   
    Merhaba **App.config** dosyası, hello hizmet adı, uç noktayı (Azure geçiş tarafından kullanıma sunulan birbirleriyle istemcilerin ve ana bilgisayarların toocommunicate diğer bir deyişle, hello konum) ve bağlama (kullanılan toocommunicate Protokolü hello türü) içerir. Merhaba ana burada bu hello yapılandırılan hizmet uç noktası başvuruyor tooa farktır [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) bağlama.
2. Merhaba `<system.serviceModel>` XML öğesi olan bir veya daha çok hizmeti tanımlayan WCF öğesidir. Aşağıda, kullanılan toodefine hello hizmet adını ve uç nokta verilmiştir. Merhaba hello sonundaki `<system.serviceModel>` öğesi (ancak hala içinde `<system.serviceModel>`), ekleme bir `<bindings>` içeriği aşağıdaki hello sahip öğe. Merhaba uygulamada kullanılan hello bağlamaları tanımlar. Birden çok bağlama tanımlayabilirsiniz ancak bu öğreticide yalnızca bir tane tanımlayacaksınız.
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    Merhaba önceki kod tanımlayan WCF geçiş [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) ile bağlama **öğesinin** çok ayarlamak**hiçbiri**. Bu ayar, yukarıdaki bağlamayı kullanan bir uç noktanın istemci kimlik bilgilerini gerektirmeyeceğini belirtir.
3. Merhaba sonra `<bindings>` öğesi ekleme bir `<services>` öğesi. Benzer toohello bağlamalarla tek yapılandırma dosyasında birden çok hizmet tanımlayabilirsiniz. Ancak bu öğreticide yalnızca bir tane tanımlayacaksınız.
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    Bu adım önceden tanımlanmış hello varsayılan kullanan bir hizmet yapılandırır **webHttpRelayBinding**. Ayrıca hello varsayılan kullanır **sbTokenProvider**, hello sonraki adımda tanımlanan.
4. Hello sonra `<services>` öğesini oluşturmak bir `<behaviors>` içeriği izleyerek, "SAS_KEY" hello ile değiştiriliyor hello bir öğesiyle *paylaşılan erişim imzası* hello daha önce edindiğiniz (SAS) anahtarı [Azure portalı ][Azure portal].
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. Merhaba, App.config yine de `<appSettings>` öğesi, hello Portalı'ndan daha önce edindiğiniz hello bağlantı dizesiyle değiştirin hello tüm bağlantı dize değeri. 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. Merhaba gelen **yapı** menüsünde tıklatın **Çözümü Derle** toobuild hello çözümün tamamı.

### <a name="example"></a>Örnek
Merhaba aşağıdaki kod gösterir hello sözleşme ve hizmet uygulaması hello kullanarak Service Bus üzerinde çalışan REST tabanlı bir hizmetine **WebHttpRelayBinding** bağlama.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

Merhaba aşağıdaki örnek hello hizmetiyle ilişkili hello App.config dosyasını gösterir.

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a>4. adım: Ana bilgisayar hello REST tabanlı WCF Hizmeti toouse Azure geçişi
Bu adım, nasıl toorun bir web hizmeti WCF geçiş ile bir konsol uygulaması kullanarak açıklar. Bu adımda yazılan hello kodu tam bir listesi aşağıdaki hello yordamın hello örnekte sağlanır.

### <a name="toocreate-a-base-address-for-hello-service"></a>toocreate hello hizmeti için bir taban adresi
1. Merhaba, `Main()` işlevi bildiriminde, projenizin bir değişken toostore hello ad alanı oluşturun. Emin tooreplace olun `yourNamespace` hello geçiş ad alanı daha önce oluşturduğunuz hello adı.
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    Service Bus, ad alanı toocreate benzersiz bir URI hello adını kullanır.
2. Oluşturma bir `Uri` hello ad alanını temel hello hizmeti hello temel adres için örneği.
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a>toocreate ve hello web hizmeti ana bilgisayarını yapılandırma
* Bu bölümde daha önce oluşturduğunuz hello URI adresini kullanarak hello web hizmeti ana bilgisayarını oluşturun.
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    Merhaba hizmet konağı hello ana bilgisayar uygulamasının örneğini oluşturan hello WCF nesnesidir. İsteğe bağlı olarak bu örnek hello türü geçirir toocreate istediğiniz ana bilgisayarın (bir **Imageservice**), ve ayrıca istediğiniz tooexpose Merhaba ana bilgisayar uygulaması adresi hello.

### <a name="toorun-hello-web-service-host"></a>toorun hello web hizmeti ana bilgisayarı
1. Merhaba hizmeti açın.
   
    ```csharp
    host.Open();
    ```
    Merhaba hizmet artık çalışır durumdadır.
2. Merhaba hizmetinin çalıştığını ve nasıl toostop hello hizmet belirten bir ileti görüntüler.
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. Tamamlandığında, hello hizmet ana bilgisayarını kapatın.
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a>Örnek
Aşağıdaki örneğine hello hello öğretici ve ana hello hizmeti bir konsol uygulamasında hello hizmet sözleşmesini ve önceki adımları içerir. ImageListener.exe adlı bir yürütülebilir koddan hello derleyin.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a>Merhaba kodu derleme
Merhaba çözümü derledikten sonra toorun Merhaba uygulaması hello:

1. Tuşuna **F5**, veya toohello yürütülebilir dosya konumu (ImageListener\bin\Debug\ImageListener.exe) toorun hello hizmet göz atın. Tooperform hello sonraki adıma istedi gibi hello uygulama çalışırken, tutun.
2. Hello adresini kopyalayıp hello komut isteminden bir tarayıcı toosee hello görüntüsüne yapıştırın.
3. İşiniz bittiğinde, basın **Enter** hello komut istemi penceresi tooclose hello uygulama.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba Service Bus geçişi hizmetini kullanan bir uygulama oluşturduğunuza göre Azure geçişi hakkında daha fazla makaleleri toolearn aşağıdaki hello bakın:

* [Azure Service Bus mimarisine genel bakış](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [Azure Geçiş’e genel bakış](relay-what-is-it.md)
* [Toouse hello WCF hizmeti .NET ile nasıl geçiş](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
