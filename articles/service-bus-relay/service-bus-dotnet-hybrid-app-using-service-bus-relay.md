---
title: "aaaAzure WCF geçiş karma şirket içi/bulut uygulama (.NET) | Microsoft Docs"
description: "Bilgi nasıl Azure WCF geçiş kullanarak toocreate bir .NET şirket içi/bulut karma uygulama."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a>Azure WCF Geçişini kullanan karma .NET şirket içi uygulama/bulut uygulaması
## <a name="introduction"></a>Giriş

Bu makalede, Microsoft Azure ve Visual Studio ile uygulama toobuild karma bir bulut nasıl gösterilmektedir. Başlangıç Öğreticisi Azure kullanma konusunda deneyim sahibi varsayar. Az 30 dakika içerisinde birden çok Azure kaynağını kullanan bir uygulama ve hello bulutta çalışan sahip olacaktır.

Şunları öğreneceksiniz:

* Nasıl toocreate veya bir web çözümünde var olan bir web hizmetini uyarlama.
* Nasıl bir Azure uygulaması ve web hizmeti arasında toouse hello Azure WCF geçiş hizmeti tooshare verileri başka bir yerde barındırılan.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a>Azure Relay geçişinin karma çözümlere yönelik yardımları

İşletme Çözümleri tootackle yeni yazılmış özel kod ve benzersiz iş gereksinimlerine ve mevcut işlevselliğini çözümleri ve zaten kullanımdadır sistemler tarafından sağlanan birlikte genellikle oluşur.

Çözüm mimarları ölçek gereksinimlerine ve işletim maliyetlerini daha kolay işlenmesi için toouse hello bulut başlıyor. Bunu yaparken, bunların çözümleri için yapı taşları hello Kurumsal güvenlik duvarı içinde ve dışında kolay olduğundan tooleverage istediğiniz var olan hizmet varlıklarının hello bulut çözümü tarafından erişim için ulaşmak bulun. Birçok dahili Hizmet derlenmez veya bunlar kolayca hello kurumsal ağ ucunda kullanıma sunulabilecek şekilde şekilde barındırılan.

[Azure geçiş](https://azure.microsoft.com/services/service-bus/) için tasarlanmış var olan Windows Communication Foundation (WCF) web hizmetlerini almaya kullanım örneği hello ve Hizmetleri gerek kalmadan hello Kurumsal çevre dışında bulunan güvenli bir şekilde erişilebilir toosolutions olanlar yapma toohello kurumsal ağ altyapısına müdahale eden değişiklikler. Bu tür geçiş hizmetleri hala kendi mevcut ortamın içinde barındırılan, ancak gelen oturumları ve istekleri toohello geçiş bulutta barındırılan hizmeti için dinleme temsilci. Ayrıca, Azure Geçişi [Paylaşılan Erişim İmzası (SAS)](../service-bus-messaging/service-bus-sas.md) kimlik doğrulaması kullanarak bu hizmetleri yetkilendirilmemiş erişime karşı korur.

## <a name="solution-scenario"></a>Çözüm senaryosu
Bu öğreticide, hello ürün stoğu sayfasındaki ürünlerin listesini toosee sağlayan bir ASP.NET Web sitesi oluşturur.

![][0]

Başlangıç Öğreticisi, varolan bir şirket içi sistemde ürün bilgilerine sahip ve bu sisteme Azure geçiş tooreach kullanır varsayar. Bu çözüm, basit bir konsol uygulamasında çalışan web hizmeti ile benzetilir ve bir bellek içi ürün kümesi ile desteklenir. Siz mümkün toorun bu konsol uygulamasını kendi bilgisayarınızda yüklü olması ve hello web rolünü Azure'a dağıtabilirsiniz. Bilgisayarınızı, bilgisayarınız en az bir güvenlik duvarı ve ağ adresi çevirisi (NAT) katmanı arkasında yer alacağı olsa bile bunu yaparak, nasıl hello Azure veri merkezinde çalışan hello web rolü gerçekten bilgisayarınıza çağrı gönderebildiğini göreceksiniz.

## <a name="set-up-hello-development-environment"></a>Merhaba geliştirme ortamını ayarlama

Azure uygulamalarını geliştirmeye başlamadan önce hello Araçları'nı indirmek ve geliştirme ortamınızı ayarlayın:

1. .NET için SDK hello Hello Azure SDK'sını yüklemek [indirmeler sayfası](https://azure.microsoft.com/downloads/).
2. Merhaba, **.NET** sütun hello sürümünü [Visual Studio](http://www.visualstudio.com) kullanmakta olduğunuz. Bu öğretici kullanımda Visual Studio 2015 Hello adımlar, ancak bunlar da Visual Studio 2017 ile çalışır.
3. Toorun istenir veya hello yükleyici kaydettiğinizde tıklatın **çalıştırmak**.
4. Merhaba, **Web Platformu yükleyicisi**,'ı tıklatın **yüklemek** ve hello yükleme işlemine devam edin.
5. Merhaba yüklemesi tamamlandıktan sonra her şeyi olacaktır gerekli toostart toodevelop hello uygulama. Merhaba SDK, Visual Studio'da Azure uygulamalarını kolayca geliştirmenize olanak sağlayan araçları içerir.

## <a name="create-a-namespace"></a>Ad alanı oluşturma

Merhaba Azure geçiş özelliklerinde toobegin kullanarak, öncelikle bir hizmet ad alanı oluşturmanız gerekir. Ad alanı, uygulamanızda bulunan Azure kaynaklarını adreslemek için içeriğin kapsamını belirleyen bir kapsayıcı sunar. Merhaba izleyin [yönergeleri burada](relay-create-namespace-portal.md) toocreate geçiş ad alanı.

## <a name="create-an-on-premises-server"></a>Şirket içi sunucu oluşturma

Öncelikle, bir (sahte) şirket içi ürün kataloğu sistemi derleyeceksiniz. Bu, oldukça basit olacaktır; Bu bir toointegrate çalıştığınız tüm hizmet yüzeyini içeren gerçek şirket içi ürün kataloğu sistemini temsil eden olarak görebilirsiniz.

Bu proje bir Visual Studio konsol uygulamasıdır ve kullandığı hello [Azure Service Bus NuGet paketi](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello Service Bus kitaplıkları ile yapılandırma ayarları.

### <a name="create-hello-project"></a>Başlangıç projesi oluşturma

1. Yönetici ayrıcalıklarını kullanarak Microsoft Visual Studio'yu başlatın. toodo, bu nedenle, hello Visual Studio program simgesine sağ tıklayın ve ardından **yönetici olarak çalıştır**.
2. Visual Studio'da, hello **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.
3. **Yüklü Şablonlar**'daki **Visual C#** bölümünde **Konsol Uygulaması (.NET Framework)** seçeneğine tıklayın. Merhaba, **adı** kutusu, tür hello adı **ProductsServer**:

   ![][11]
4. Tıklatın **Tamam** toocreate hello **ProductsServer** projesi.
5. Visual Studio hello NuGet paketi yöneticisini zaten yüklediyseniz, toohello bir sonraki adımı atlayın. Yükleme yapmadıysanız [NuGet][NuGet] bölümünü ziyaret edin ve [NuGet'i Yükle](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)'ye tıklayın. Merhaba istemleri tooinstall hello NuGet Paket Yöneticisi izleyin ve ardından Visual Studio'yu yeniden başlatın.
6. Çözüm Gezgini'nde hello sağ **ProductsServer** proje ve ardından **NuGet paketlerini Yönet**.
7. Merhaba tıklatın **Gözat** sekmesini ve ardından arama `Microsoft Azure Service Bus`. Select hello **WindowsAzure.ServiceBus** paket.
8. Tıklatın **yükleme**ve hello kullanım koşullarını kabul edin.

   ![][13]

   Bu hello gerekli istemci derlemelerine başvuru oluşturulduğunu unutmayın.
8. Ürün sözleşmeniz için yeni bir sınıf ekleyin. Çözüm Gezgini'nde hello sağ **ProductsServer** proje ve tıklatın **Ekle**ve ardından **sınıfı**.
9. Merhaba, **adı** kutusu, tür hello adı **ProductsContract.cs**. Daha sonra **Ekle**'ye tıklayın.
10. İçinde **ProductsContract.cs**, hello hello hizmeti için hello sözleşmesini tanımlayan kodu aşağıdaki ile Merhaba ad alanı tanımını değiştirin.

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. Program.cs içinde hello ad alanı tanımını hello hello Profil Hizmeti ile Merhaba konağını ekler kodu aşağıdaki ile değiştirin.

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. Çözüm Gezgini'nde hello çift tıklayarak **App.config** tooopen dosya hello Visual Studio düzenleyicisinde içinde. Merhaba hello sonundaki `<system.ServiceModel>` öğesi (ancak hala içinde `<system.ServiceModel>`), aşağıdaki XML kodunu hello ekleyin. Emin tooreplace olması *yourServiceNamespace* ad alanınızın hello adla ve *yourKey* , alınan önceki hello portalından hello SAS anahtarıyla:

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. Merhaba, App.config yine de `<appSettings>` öğesi, hello Portalı'ndan daha önce edindiğiniz hello bağlantı dizesiyle değiştirin hello bağlantı dizesi değeri.

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. Tuşuna **Ctrl + Shift + B** veya hello **yapı** menüsünde tıklatın **yapı çözümü** toobuild hello uygulama ve hello çalışmanızın o ana kadarki doğruluğundan.

## <a name="create-an-aspnet-application"></a>ASP.NET uygulaması oluşturma

Bu bölümde, ürün hizmetinizden alınan verileri görüntüleyen basit bir ASP.NET uygulaması oluşturacaksınız.

### <a name="create-hello-project"></a>Başlangıç projesi oluşturma

1. Visual Studio'nun yönetici ayrıcalıklarıyla çalıştığından emin olun.
2. Visual Studio'da, hello **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.
3. **Yüklü Şablonlar**'daki **Visual C#** bölümünde bulunan **ASP.NET Web Uygulaması (.NET Framework)** seçeneğine tıklayın. Ad hello proje **ProductsPortal**. Daha sonra, **Tamam**'a tıklayın.

   ![][15]

4. Merhaba gelen **ASP.NET şablonları** hello listesinde **yeni ASP.NET Web uygulaması** iletişim kutusunda, tıklatın **MVC**.

   ![][16]

6. Merhaba tıklatın **kimlik doğrulamayı Değiştir** düğmesi. Merhaba, **kimlik doğrulamayı Değiştir** iletişim kutusunda **doğrulaması yok** seçilir ve ardından **Tamam**. Bu öğreticide, kullanıcının oturum açmasını gerektirmeyen bir uygulamayı dağıtacaksınız.

    ![][18]

7. Merhaba edilene **yeni ASP.NET Web uygulaması** iletişim kutusunda, tıklatın **Tamam** toocreate hello MVC uygulama.
8. Şimdi yeni bir web uygulaması için Azure kaynaklarını yapılandırmanız gerekir. Merhaba Hello adımları [tooAzure bu makalenin yayımlama](../app-service-web/app-service-web-get-started-dotnet.md). Ardından, toothis öğretici dönün ve toohello sonraki adıma geçin.
10. Çözüm Gezgini'nde **Modeller**'e sağ tıklayıp **Ekle**’ye ve ardından **Sınıf**’a tıklayın. Merhaba, **adı** kutusu, tür hello adı **Product.cs**. Daha sonra **Ekle**'ye tıklayın.

    ![][17]

### <a name="modify-hello-web-application"></a>Merhaba web uygulamasını değiştirme

1. Merhaba Product.cs dosyasında Visual Studio, hello var olan ad alanı tanımını koddan hello ile değiştirin.

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. Çözüm Gezgini'nde hello genişletin **denetleyicileri** klasörünü hello çift tıklatın **HomeController.cs** tooopen dosya Visual Studio içinde.
3. İçinde **HomeController.cs**, hello var olan ad alanı tanımını koddan hello ile değiştirin.

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. Çözüm Gezgini'nde hello görünümler/paylaşılan klasörünü genişletin ve ardından **_Layout.cshtml** tooopen onu hello Visual Studio düzenleyicisinde.
5. Tüm oluşumlarını değiştirme **My ASP.NET Application** çok**LITWARE's Products**.
6. Merhaba kaldırmak **giriş**, **hakkında**, ve **kişi** bağlantılar. Aşağıdaki örneğine hello hello vurgulanmış kodu silin.

    ![][41]

7. Çözüm Gezgini'nde hello görünümler/giriş klasörünü genişletin ve ardından **Index.cshtml** tooopen onu hello Visual Studio düzenleyicisinde. Merhaba dosyanın tüm içeriğini Hello koddan hello ile değiştirin.

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. tooverify hello doğruluğu çalışmanızın o ana kadarki basabilirsiniz **Ctrl + Shift + B** toobuild hello projesi.

### <a name="run-hello-app-locally"></a>Merhaba uygulamayı yerel olarak çalıştırma

Çalıştığını hello uygulama tooverify çalıştırın.

1. Emin **ProductsPortal** hello etkin projesidir. Merhaba Çözüm Gezgini'nde proje adına sağ tıklayıp **başlangıç projesi olarak ayarla**.
2. Visual Studio'da **F5** tuşuna basın.
3. Uygulamanız, bir tarayıcıda çalışıyor olarak görüntülenmelidir.

   ![][21]

## <a name="put-hello-pieces-together"></a>Merhaba parçaları bir araya getirme

Merhaba sonraki hello şirket içi ürünlerin sunucusu hello ASP.NET uygulaması ile toohook adımdır.

1. Visual Studio'da yeniden Aç'u hello zaten açık değilse, **ProductsPortal** hello oluşturulan proje [ASP.NET uygulaması oluşturma](#create-an-aspnet-application) bölümü.
2. Merhaba "Bir şirket içi sunucu oluşturma" bölümünde, benzer toohello adımı hello NuGet paketi toohello proje başvuruları ekleyin. Çözüm Gezgini'nde hello sağ **ProductsPortal** proje ve ardından **NuGet paketlerini Yönet**.
3. "Hizmet veri yolu" ve select hello arama **WindowsAzure.ServiceBus** öğesi. Ardından hello yüklemeyi tamamlamak ve bu iletişim kutusunu kapatın.
4. Çözüm Gezgini'nde hello sağ **ProductsPortal** proje ve ardından **Ekle**, ardından **varolan öğeyi**.
5. Toohello gidin **ProductsContract.cs** hello dosyasından **ProductsServer** konsol projesi. Toohighlight ProductsContract.cs'ı tıklatın. Aşağı ok Hello sonraki çok tıklatın**Ekle**, ardından **bağlantı olarak Ekle**.

   ![][24]

6. Şimdi hello açmak **HomeController.cs** dosya hello Visual Studio düzenleyicisinde ve hello ad alanı tanımını koddan hello ile değiştirin. Emin tooreplace olması *yourServiceNamespace* hizmet ad alanınızın hello adla ve *yourKey* da SAS anahtarınızla. Bu hello hello çağrı sonucunu döndürerek hello istemci toocall hello şirket içi hizmet, olanak tanır.

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. Çözüm Gezgini'nde hello sağ **ProductsPortal** çözüm (yapma emin tooright tıklatma hello çözüm, değil hello Proje). **Ekle**'ye ve ardından **Var Olan Proje**'ye tıklayın.
8. Toohello gidin **ProductsServer** proje ve ardından hello **ProductsServer.csproj** çözüm dosya tooadd onu.
9. **ProductsServer** sipariş toodisplay hello verilerde çalıştırmalıdır **ProductsPortal**. Çözüm Gezgini'nde hello sağ **ProductsPortal** çözümü ve tıklatın **özellikleri**. Merhaba **özellik sayfaları** iletişim kutusu görüntülenir.
10. Sol tarafında hello üzerinde tıklatın **başlangıç projesi**. Merhaba sağ tarafta tıklatın **birden fazla başlangıç projesi**. Emin **ProductsServer** ve **ProductsPortal** , o sırada göründüğünden **Başlat** ikisi için de hello eylem olarak ayarlayın.

      ![][25]

11. Merhaba yine de **özellikleri** iletişim kutusu, tıklatın **proje bağımlılıkları** yan sol hello üzerinde.
12. Merhaba, **projeleri** tıklatın **ProductsServer**. **ProductsPortal**'ın seçilmediğinden emin olun.
13. Merhaba, **projeleri** tıklatın **ProductsPortal**. **ProductsServer** projesinin seçili olduğundan emin olun.

    ![][26]

14. Tıklatın **Tamam** hello içinde **özellik sayfaları** iletişim kutusu.

## <a name="run-hello-project-locally"></a>Merhaba projeyi yerel olarak çalıştırma

Visual Studio'da yerel olarak tootest Merhaba uygulaması basın **F5**. Merhaba şirket içi sunucu (**ProductsServer**) ilk başlayın, ardından hello **ProductsPortal** uygulaması bir tarayıcı penceresinde başlamalıdır. Bu süre, hello ürün stoğunun hello ürün hizmeti şirket içi sisteminden aldığı verileri listelediğini görürsünüz.

![][10]

Tuşuna **yenileme** hello üzerinde **ProductsPortal** sayfası. Merhaba sayfayı yenileyin, her bir ileti görüntüler hello sunucu uygulama göreceğiniz zaman `GetProducts()` gelen **ProductsServer** olarak adlandırılır.

Her iki uygulamayı toohello sonraki adıma devam etmeden önce kapatın.

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a>Merhaba ProductsPortal proje tooan Azure web uygulaması dağıtma

Merhaba sonraki adımdır toorepublish hello Azure Web uygulaması **ProductsPortal** ön uç. Aşağıdaki hello:

1. Çözüm Gezgini'nde hello sağ **ProductsPortal** proje öğesini tıklatıp **Yayımla**. Ardından **Yayımla** hello üzerinde **Yayımla** sayfası.

  > [!NOTE]
  > Bir hata iletisi hello tarayıcı penceresinde hello zaman görebilirsiniz **ProductsPortal** web projesi hello dağıtım sonrasında otomatik olarak başlatılır. Bu beklenen bir durumdur ve oluşur hello **ProductsServer** uygulaması henüz çalışmadığından.
>
>

2. Merhaba URL hello sonraki adımda ihtiyaç duyacağınız kopyalama hello hello URL'sini web uygulaması dağıtılmış. Visual Studio'da hello Azure App Service etkinliği penceresinden de bu URL'yi elde edebilirsiniz:

  ![][9]

3. Uygulama çalıştıran hello tarayıcı penceresini toostop hello kapatın.

### <a name="set-productsportal-as-web-app"></a>ProductsPortal'ı web uygulaması olarak ayarlama

Merhaba bulutta çalışan hello uygulama önce emin olmanız gerekir **ProductsPortal** gelen Visual Studio'dan bir web uygulaması olarak başlatılır.

1. Visual Studio'da hello sağ **ProductsPortal** proje ve ardından **özellikleri**.
2. Merhaba sol sütunda, tıklatın **Web**.
3. Merhaba, **eylemi Başlat** bölümünde, hello tıklatın **Start URL** düğmesine tıklayın ve hello metin kutusuna, daha önce dağıttınız web uygulamanız için; hello URL'sini girin örneğin, `http://productsportal1234567890.azurewebsites.net/`.

    ![][27]

4. Merhaba gelen **dosya** Visual Studio'da menüsünü **Tümünü Kaydet**.
5. Merhaba yapı menüden Visual Studio'da, **çözümü yeniden derle**.

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın

1. F5 toobuild tuşuna basın ve hello uygulamayı çalıştırın. Merhaba şirket içi sunucu (Merhaba **ProductsServer** konsol uygulaması) ilk başlayın, ardından hello **ProductsPortal** uygulaması, bir tarayıcı penceresinde başlamalıdır, aşağıdaki ekran hello gösterildiği gibi görüntüsü. Yeniden, hello ürün stoğunun hello ürün hizmeti şirket içi sisteminden aldığı verileri listelediğini ve bu verileri hello web uygulamasında gösterdiğini dikkat edin. Merhaba URL toomake emin denetleyin, **ProductsPortal** hello bulut Azure web uygulaması olarak çalışıyor.

   ![][1]

   > [!IMPORTANT]
   > Merhaba **ProductsServer** çalışıp çalışmadığını ve konsol uygulaması olmalıdır tooserve hello veri toohello **ProductsPortal** uygulama. Merhaba tarayıcı bir hata görüntülerse birkaç saniye daha bekleyin **ProductsServer** tooload ve aşağıdaki görüntü hello iletisi gönderir. Tuşuna basarak **yenileme** hello tarayıcıda.
   >
   >

   ![][37]
2. Geri hello tarayıcıda basın **yenileme** hello üzerinde **ProductsPortal** sayfası. Merhaba sayfayı yenileyin, her bir ileti görüntüler hello sunucu uygulama göreceğiniz zaman `GetProducts()` gelen **ProductsServer** olarak adlandırılır.

    ![][38]

## <a name="next-steps"></a>Sonraki adımlar

Azure geçişi hakkında daha fazla toolearn kaynakları aşağıdaki hello bakın:  

* [Azure Geçiş nedir?](relay-what-is-it.md)  
* [Toouse nasıl geçiş](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
