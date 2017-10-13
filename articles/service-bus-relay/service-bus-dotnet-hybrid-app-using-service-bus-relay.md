---
title: "Azure WCF Geçişi karma şirket içi uygulama/bulut uygulaması (.NET) | Microsoft Belgeleri"
description: "Azure WCF Geçişini kullanarak karma .NET şirket içi uygulama/bulut uygulaması oluşturmayı öğrenin."
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
ms.openlocfilehash: d15c30dad9fb4bbe9082d6a3c72cd20ed42bbc3e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a>Azure WCF Geçişini kullanan karma .NET şirket içi uygulama/bulut uygulaması
## <a name="introduction"></a>Giriş

Bu makale, Microsoft Azure ve Visual Studio ile nasıl karma bulut uygulaması derleyeceğinizi gösterir. Öğretici Azure kullanımına ilişkin deneyim sahibi olmadığınızı varsayar. 30 dakikadan kısa sürede, birden çok Azure kaynağını kullanan ve bulutta çalışan bir uygulamaya sahip olacaksınız.

Şunları öğreneceksiniz:

* Bir web çözümünde kullanılması amacıyla web hizmeti oluşturma veya var olan bir web hizmetini uyarlama.
* Azure uygulaması ve başka bir yerde barındırılan web hizmeti arasında veri paylaşımı için Azure WCF Geçişi hizmetini kullanma.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a>Azure Relay geçişinin karma çözümlere yönelik yardımları

İşletme çözümleri, genel olarak yeni ve benzersiz işletme gereksinimlerini karşılamak için yazılan özel bir kodun ve kullanılan çözüm ve sistemler tarafından sağlanan var olan işlevselliğin bir birleşiminden oluşur.

Çözüm mimarları, ölçek gereksinimlerini daha kolay bir şekilde karşılamak ve işlem maliyetlerini düşürmek için bulutu kullanmaya başlıyor. Bunu yaparken de çözümleri için yapı taşı olarak kullanmak istedikleri var olan hizmet varlıklarının kurumsal güvenlik duvarının içinde ve bulut çözümüyle kolayca erişilemeyecek konumda olduklarını fark ettiler. Birçok dahili hizmet, kurumsal ağ ucunda kolayca kullanıma sunulabilecek şekilde derlenmez veya barındırılmaz.

[Azure Geçişi](https://azure.microsoft.com/services/service-bus/) ise mevcut Windows Communication Foundation (WCF) web hizmetlerinin alınarak kurumsal ağ altyapısını bozan değişikliklere gerek kalmadan kurumsal çevre dışında bulunan çözümlere güvenli bir şekilde erişmesini sağlamaya yönelik kullanım senaryosu için tasarlanmıştır. Bu tür geçişi hizmetleri, var olan ortamlarında barındırılmaya devam eder ancak bu hizmetler gelen oturumları ve istekleri bulutta barındırılan geçiş hizmetine devreder. Ayrıca, Azure Geçişi [Paylaşılan Erişim İmzası (SAS)](../service-bus-messaging/service-bus-sas.md) kimlik doğrulaması kullanarak bu hizmetleri yetkilendirilmemiş erişime karşı korur.

## <a name="solution-scenario"></a>Çözüm senaryosu
Bu öğreticide, ürün stoğu sayfasındaki ürünlerin listesini görmenize olanak sağlayan bir ASP.NET web sitesi oluşturacaksınız.

![][0]

Öğretici, var olan şirket içi sistemde ürün bilgilerine sahip olduğunuzu varsayar ve bu sisteme erişmek için Azure Geçişini kullanır. Bu çözüm, basit bir konsol uygulamasında çalışan web hizmeti ile benzetilir ve bir bellek içi ürün kümesi ile desteklenir. Bu konsol uygulamasını kendi bilgisayarınızda çalıştırabilirsiniz ve web rolünü Azure'a dağıtabilirsiniz. Bu özellik sayesinde, bilgisayarınız en az bir güvenlik duvarının arkasında ve bir ağ adresi çevirisi (NAT) katmanında yer alsa bile Azure veri merkezinde çalışan web rolünün gerçekten bilgisayarınıza çağrı gönderebildiğini göreceksiniz.

## <a name="set-up-the-development-environment"></a>Geliştirme ortamını ayarlama

Azure uygulamalarını geliştirmeye başlamadan önce, araçları indirip geliştirme ortamınızı ayarlayın:

1. SDK [indirme sayfasından](https://azure.microsoft.com/downloads/) .NET için Azure SDK'sını yükleyin.
2. **.NET** sütununda, kullandığınız [Visual Studio](http://www.visualstudio.com) sürümüne tıklayın. Bu öğreticideki adımlar Visual Studio 2015 kullanır, ancak Visual Studio 2017 ile de çalışır.
3. Yükleyiciyi çalıştırmanız veya kaydetmeniz istendiğinde **Çalıştır**'a tıklayın.
4. **Web Platformu Yükleyicisi**'nde **Yükle**'ye tıklayın ve kuruluma devam edin.
5. Kurulum tamamlandığında uygulamayı geliştirmeye başlamak için gereken her şeye sahip olacaksınız. SDK, Visual Studio'da Azure uygulamalarını kolayca geliştirmenize olanak sağlayan araçları içerir.

## <a name="create-a-namespace"></a>Ad alanı oluşturma

Azure'da geçiş özelliklerini kullanmaya başlamak için öncelikle bir hizmet ad alanı oluşturmanız gerekir. Ad alanı, uygulamanızda bulunan Azure kaynaklarını adreslemek için içeriğin kapsamını belirleyen bir kapsayıcı sunar. [Buradaki yönergeleri](relay-create-namespace-portal.md) izleyerek bir Geçiş ad alanı oluşturun.

## <a name="create-an-on-premises-server"></a>Şirket içi sunucu oluşturma

Öncelikle, bir (sahte) şirket içi ürün kataloğu sistemi derleyeceksiniz. Bu oldukça kolay bir işlemdir. Bu çalışmanın, entegre etmeye çalıştığımız tüm hizmet yüzeyini içeren gerçek bir şirket içi ürün kataloğu sistemini temsil ettiğini düşünebilirsiniz.

Bu proje bir Visual Studio konsol uygulamasıdır ve Service Bus kitaplıkları ile yapılandırma ayarlarını dahil etmek için [Azure Service Bus NuGet paketini](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) kullanır.

### <a name="create-the-project"></a>Proje oluşturma

1. Yönetici ayrıcalıklarını kullanarak Microsoft Visual Studio'yu başlatın. Bunu yapmak için Visual Studio program simgesine sağ tıklayıp **Yönetici olarak çalıştır**’a tıklayın.
2. Visual Studio'da, **Dosya** menüsündeki **Yeni** seçeneğine ve ardından **Proje**'ye tıklayın.
3. **Yüklü Şablonlar**'daki **Visual C#** bölümünde **Konsol Uygulaması (.NET Framework)** seçeneğine tıklayın. **Ad** kutusuna **ProductsServer** adını yazın:

   ![][11]
4. **ProductsServer** projesini oluşturmak için **Tamam** seçeneğine tıklayın.
5. Visual Studio'ya yönelik NuGet paketi yöneticisini zaten yüklediyseniz bir sonraki adımı atlayın. Yükleme yapmadıysanız [NuGet][NuGet] bölümünü ziyaret edin ve [NuGet'i Yükle](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)'ye tıklayın. NuGet paketi yöneticisini yüklemek için gereken istemleri gerçekleştirin ve Visual Studio'yu yeniden başlatın.
6. Çözüm Gezgini'nde **ProductsServer** projesine sağ tıklayın ve ardından **NuGet Paketlerini Yönet**'e tıklayın.
7. **Gözat** sekmesine tıklayıp `Microsoft Azure Service Bus` için arama yapın. **WindowsAzure.ServiceBus** paketini seçin.
8. **Yükle**'ye tıklayın ve kullanım koşullarını kabul edin.

   ![][13]

   Artık gerekli istemci derlemelerine başvuru oluşturulduğunu unutmayın.
8. Ürün sözleşmeniz için yeni bir sınıf ekleyin. Çözüm Gezgini'nde **ProductsServer** projesine sağ tıklayın ve ardından **Ekle** ve **Sınıf** seçeneklerine tıklayın.
9. **Ad** kutusuna **ProductsContract.cs** adını yazın: Daha sonra **Ekle**'ye tıklayın.
10. **ProductsContract.cs** sınıfında, ad alanı tanımını hizmet sözleşmesini tanımlayan şu kod ile değiştirin:

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define the data contract for the service
        [DataContract]
        // Declare the serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define the service contract.
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
11. Program.cs sınıfında içinde, ad alanı tanımını profil hizmetini ve bu hizmete yönelik ana bilgisayarı ekleyen şu kod ile değiştirin:

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement the IProducts interface.
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

            // Display a message in the service console application
            // when the list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define the Main() function in the service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER to close");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. Çözüm Gezgini'nde, **App.config** dosyasına çift tıklayarak dosyayı Visual Studio düzenleyicisinde açın. `<system.ServiceModel>` öğesinin en altına (yine `<system.ServiceModel>` içinde kalacak şekilde) aşağıdaki XML kodunu ekleyin. *yourKey* alanını daha önce portaldan aldığınız SAS anahtarıyla ve *yourServiceNamespace* alanını da ad alanı adınızla değiştirdiğinizden emin olun:

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
13. App.config dosyasından çıkmadan, `<appSettings>` öğesinde bağlantı dizesi değerini portaldan daha önce edindiğiniz bağlantı dizesiyle değiştirin.

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. Uygulamayı derlemek ve o ana kadarki doğruluğunu onaylamak üzere **Derle** menüsünde **Çözümü Derle** seçeneğine tıklayın veya **Ctrl+Shift+B**'ye basın.

## <a name="create-an-aspnet-application"></a>ASP.NET uygulaması oluşturma

Bu bölümde, ürün hizmetinizden alınan verileri görüntüleyen basit bir ASP.NET uygulaması oluşturacaksınız.

### <a name="create-the-project"></a>Proje oluşturma

1. Visual Studio'nun yönetici ayrıcalıklarıyla çalıştığından emin olun.
2. Visual Studio'da, **Dosya** menüsündeki **Yeni** seçeneğine ve ardından **Proje**'ye tıklayın.
3. **Yüklü Şablonlar**'daki **Visual C#** bölümünde bulunan **ASP.NET Web Uygulaması (.NET Framework)** seçeneğine tıklayın. Projeyi **ProductsPortal** olarak adlandırın. Daha sonra, **Tamam**'a tıklayın.

   ![][15]

4. **New ASP.NET Web Uygulaması** iletişim kutusundaki **ASP.NET Şablonları** listesinde **MVC** seçeneğine tıklayın.

   ![][16]

6. **Kimlik Doğrulamayı Değiştir** düğmesine tıklayın. **Kimlik Doğrulamayı Değiştir** iletişim kutusunda **Kimlik Doğrulama Yok** seçeneğinin belirlendiğinden emin olun ve ardından **Tamam**'a tıklayın. Bu öğreticide, kullanıcının oturum açmasını gerektirmeyen bir uygulamayı dağıtacaksınız.

    ![][18]

7. MVC uygulamasını oluşturmak üzere **New ASP.NET Web Uygulaması** iletişim kutusunda **Tamam**'a tıklayın.
8. Şimdi yeni bir web uygulaması için Azure kaynaklarını yapılandırmanız gerekir. [Bu makalenin Azure'da Yayımlama bölümündeki](../app-service/app-service-web-get-started-dotnet.md) adımları uygulayın. Daha sonra, bu öğreticiye geri dönün ve sonraki adıma geçin.
10. Çözüm Gezgini'nde **Modeller**'e sağ tıklayıp **Ekle**’ye ve ardından **Sınıf**’a tıklayın. **Ad** kutusuna **Product.cs** yazın. Daha sonra **Ekle**'ye tıklayın.

    ![][17]

### <a name="modify-the-web-application"></a>Web uygulamasını değiştirme

1. Visual Studio'da Product.cs dosyasındaki var olan ad alanı tanımını şu kod ile değiştirin:

   ```csharp
    // Declare properties for the products inventory.
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
2. Çözüm Gezgini'nde **Denetleyiciler** klasörünü genişletin ve Visual Studio'da açmak için **HomeController.cs** dosyasına çift tıklayın.
3. **HomeController.cs** dosyasındaki var olan ad alanı tanımını aşağıdaki kod ile değiştirin.

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of the products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. Çözüm Gezgini'nde, Görünümler/Paylaşılan klasörünü genişletin ve ardından **_Layout.cshtml** öğesine tıklayarak Visual Studio düzenleyicisinde açın.
5. **My ASP.NET Application** uygulamasının tüm örneklerini **LITWARE's Products** olarak değiştirin.
6. **Home**, **About** ve **Contact** bağlantılarını kaldırın. Aşağıdaki örnekte vurgulanmış kodu silin.

    ![][41]

7. Çözüm Gezgini'nde, Görünümler/Giriş klasörünü genişletin ve ardından **Index.cshtml** öğesine tıklayarak Visual Studio düzenleyicisinde açın. Dosyanın tüm içeriğini aşağıdaki kodla değiştirin.

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
8. Çalışmanızın o ana kadarki doğruluğunu onaylamak üzere projeyi derlemek için **Ctrl+Shift+B**'ye basabilirsiniz.

### <a name="run-the-app-locally"></a>Uygulamayı yerel olarak çalıştırma

Çalışır durumda olduğunu doğrulamak için uygulamayı çalıştırın.

1. **ProductsPortal** projesinin, etkin olduğundan emin olun. Çözüm Gezgini'nde proje adına sağ tıklayıp **Başlangıç Projesi Olarak Ayarla**'yı seçin.
2. Visual Studio'da **F5** tuşuna basın.
3. Uygulamanız, bir tarayıcıda çalışıyor olarak görüntülenmelidir.

   ![][21]

## <a name="put-the-pieces-together"></a>Parçaları bir araya getirme

Sonraki adım, şirket içi ürünlerin sunucusu ile ASP.NET uygulamasını birleştirmektir.

1. Açık değilse [ASP.NET uygulaması oluşturma](#create-an-aspnet-application) bölümünde oluşturduğunuz **ProductsPortal** projesini Visual Studio'da yeniden açın.
2. "Şirket İçi Sunucu Oluşturma" bölümündeki adıma benzer şekilde proje başvurularına NuGet paketini ekleyin. Çözüm Gezgini'nde **ProductsPortal** projesine sağ tıklayın ve ardından **NuGet Paketlerini Yönet**'e tıklayın.
3. "Service Bus" için arama yapın ve **WindowsAzure.ServiceBus** öğesini seçin. Yüklemeyi tamamlayıp iletişim kutusunu kapatın.
4. Çözüm Gezgini'nde **ProductsPortal** projesine sağ tıklayın ve ardından **Ekle** ve **Var Olan Öğe** seçeneklerine tıklayın.
5. **ProductsServer** konsol projesinden **ProductsContract.cs** dosyasına gidin. ProductsContract.cs dosyasına tıklayarak dosyayı vurgulayın. **Ekle** seçeneğinin yanındaki aşağı oka ve ardından **Bağlantı Olarak Ekle** seçeneğine tıklayın.

   ![][24]

6. Şimdi, Visual Studio düzenleyicisinde **HomeController.cs** dosyasını açın ve ad alanı tanımını aşağıdaki kodla değiştirin. *yourServiceNamespace* alanını hizmet ad alanınızla ve *yourKey* alanını da SAS anahtarınızla değiştirdiğinizden emin olun. Bu işlem, çağrı sonucunu döndürerek istemcinin şirket içi hizmete çağrı yapmasına olanak sağlar.

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
           // Declare the channel factory.
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
                   // Return a view of the products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. Çözüm Gezgini’nde **ProductsPortal** çözümüne sağ tıklayın (projeye değil, çözüme sağ tıkladığınızdan emin olun). **Ekle**'ye ve ardından **Var Olan Proje**'ye tıklayın.
8. **ProductsServer** projesine gidip **ProductsServer.csproj** çözümüne çift tıklayarak ekleyin.
9. **ProductsPortal**'da veri görüntülemek için**ProductsServer** projesinin çalışıyor olması gerekir. Çözüm Gezgini'nde **ProductsPortal** çözümüne sağ tıklayın ve ardından **Özellikler** seçeneğine tıklayın. **Özellik Sayfaları** iletişim kutusu görüntülenir.
10. Sol taraftaki **Başlangıç Projesi**'ne tıklayın. Sağ taraftaki **Birden çok başlangıç projesine** tıklayın. **ProductsServer** ve **ProductsPortal** projelerinin belirtilen sırada göründüğünden ve her ikisi için de eylem olarak **Başlat** seçeneğinin ayarlandığından emin olun.

      ![][25]

11. Yine **Özellikler** iletişim kutusunda, sol tarafta bulunan **Proje Bağımlılıkları**'na tıklayın.
12. **Projeler** listesinde **ProductsServer** projesine tıklayın. **ProductsPortal**'ın seçilmediğinden emin olun.
13. **Projeler** listesinde **ProductsPortal** projesine tıklayın. **ProductsServer** projesinin seçili olduğundan emin olun.

    ![][26]

14. **Özellik Sayfaları** iletişim kutusunda **Tamam**'a tıklayın.

## <a name="run-the-project-locally"></a>Projeyi yerel olarak çalıştırma

Uygulamayı yerel olarak test etmek için Visual Studio'da **F5**'e basın. İlk olarak şirket içi sunucunun (**ProductsServer**) başlaması gerekir, ardından **ProductsPortal** uygulaması bir tarayıcı penceresinde başlamalıdır. Bu kez ürün stoğunun ürün hizmeti şirket içi sisteminden aldığı verileri listelediğini görürsünüz.

![][10]

**ProductsPortal** sayfasında **Yenile** düğmesine basın. Sayfayı her yenilediğinizde, **ProductsServer** uygulamasından `GetProducts()` çağrıldığında sunucu uygulamasının bir ileti gönderdiğini görürsünüz.

Sonraki adıma geçmeden önce her iki uygulamayı da kapatın.

## <a name="deploy-the-productsportal-project-to-an-azure-web-app"></a>ProductsPortal projesini bir Azure web uygulamasına dağıtma

Sonraki adımda, Azure Web uygulaması **ProductsPortal** ön ucunu yeniden yayımlayacaksınız. Şunları yapın:

1. Çözüm Gezgini'nde **ProductsPortal** projesine sağ tıklayın ve **Yayımla** seçeneğine tıklayın. Ardından **Yayımlama** sayfasında **Yayımla**'ya tıklayın.

  > [!NOTE]
  > Dağıtımdan sonra **ProductsPortal** web projesinin otomatik olarak başlatılması durumunda tarayıcıda bir hata iletisi görüntülenebilir. **ProductsServer** uygulaması henüz çalışmadığından bu durumun meydana gelmesi olasıdır.
>
>

2. Bir sonraki adımda ihtiyaç duyacağınız için, dağıtılan web uygulamasının URL'sini kopyalayın. Ayrıca, Visual Studio'daki Azure App Service Etkinliği penceresinden de bu URL'yi elde edebilirsiniz:

  ![][9]

3. Çalışan uygulamayı durdurmak için tarayıcı penceresini kapatın.

### <a name="set-productsportal-as-web-app"></a>ProductsPortal'ı web uygulaması olarak ayarlama

Uygulamayı bulutta çalıştırmadan önce **ProductsPortal** öğesinin Visual Studio'da bir web uygulaması olarak başlatıldığından emin olmanız gerekir.

1. Visual Studio'da **ProductsPortal** projesine sağ tıklayın ve ardından **Özellikler**'e tıklayın.
2. Sol sütunda, **Web**'e tıklayın.
3. **Eylemi Başlat** bölümünde, **URL'yi Başlat** düğmesine tıklayın ve daha önce dağıttınız web uygulamasının URL'sini metin kutusuna girin (örneğin, `http://productsportal1234567890.azurewebsites.net/`).

    ![][27]

4. Visual Studio'daki **Dosya** menüsünde **Tümünü Kaydet**'e tıklayın.
5. Visual Studio'da Derle menüsünde **Çözümü Yeniden Derle**'ye tıklayın.

## <a name="run-the-application"></a>Uygulamayı çalıştırma

1. Uygulamayı derleyip çalıştırmak için F5'e basın. Öncelikle şirket içi sunucu (**ProductsServer** konsol uygulaması) başlamalıdır, ardından aşağıdaki ekran görüntüsünde gösterildiği gibi **ProductsPortal** uygulaması bir tarayıcı penceresinde başlamalıdır. Ürün stoğunun ürün hizmeti şirket içi sisteminden aldığı verileri listelediğini ve bu verileri web uygulamasında gösterdiğini göz önünde bulundurun. **ProductsPortal**'ın bir Azure web uygulaması olarak bulutta çalıştığından emin olmak için URL'yi kontrol edin.

   ![][1]

   > [!IMPORTANT]
   > **ProductsServer** konsol uygulamasının çalışır ve **ProductsPortal** uygulamasına veri sunma işlemini gerçekleştirebilir durumda olması gerekir. Tarayıcı bir hata görüntülerse birkaç saniye daha **ProductsServer** uygulamasının yüklenmesini ve aşağıdaki iletiyi görüntülemesini bekleyin. Daha sonra, tarayıcıda **Yenile** seçeneğine basın.
   >
   >

   ![][37]
2. Tarayıcı yenilendikten sonra **ProductsPortal** sayfasında **Yenile**'ye basın. Sayfayı her yenilediğinizde, **ProductsServer** uygulamasından `GetProducts()` çağrıldığında sunucu uygulamasının bir ileti gönderdiğini görürsünüz.

    ![][38]

## <a name="next-steps"></a>Sonraki adımlar

Azure Geçiş hakkında daha fazla bilgi edinmek için şu kaynaklara bakın:  

* [Azure Geçiş nedir?](relay-what-is-it.md)  
* [Geçiş nasıl kullanılır?](service-bus-dotnet-how-to-use-relay.md)  

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
