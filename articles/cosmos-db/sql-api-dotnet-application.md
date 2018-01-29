---
title: "Azure Cosmos DB için ASP.NET MVC öğreticisi: Web Uygulaması Geliştirme | Microsoft Docs"
description: "Azure Cosmos DB'yi kullanarak bir MVC web uygulaması oluşturmak için hazırlanan ASP.NET MVC öğreticisi. Azure Web Siteleri'nde barındırılan bir yapılacaklar uygulamasında JSON ve erişim verilerini depolayacaksınız - adım adım ASP.NET MVC öğreticisi."
keywords: "asp.net mvc öğreticisi, web uygulaması dağıtımı, mvc web uygulaması, asp net mvc adım adım öğreticisi"
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.custom: devcenter
ms.openlocfilehash: a403af0f31823f89cdc79d6769dff61aeaefc4ad
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/18/2017
---
# <a name="_Toc395809351"></a>ASP.NET MVC Öğreticisi: Azure Cosmos DB ile Web uygulaması geliştirme
> [!div class="op_single_selector"]
> * [.NET](sql-api-dotnet-application.md)
> * [Node.js](sql-api-nodejs-application.md)
> * [Java](sql-api-java-application.md)
> * [Python](sql-api-python-application.md)
> 
> 

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

Bu makale, JSON belgelerini depolama ve sorgulama amacıyla Azure Cosmos DB'yi nasıl verimli bir şekilde kullanabileceğinizi vurgulamak için, Azure Cosmos DB kullanarak bir yapılacaklar uygulamasının nasıl oluşturulacağını gösteren uçtan uca bir kılavuz sağlar. Görevler, JSON belgeleri olarak Azure Cosmos DB'de depolanır.

![Bu öğreticiyle oluşturulan yapılacaklar listesi MVC web uygulamasının ekran görüntüsü - adım adım ASP.NET MVC öğreticisi](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-image01.png)

Bu kılavuz, Azure Cosmos DB hizmet depolamak için nasıl kullanılacağı ve erişim verilerini Azure üzerinde barındırılan bir ASP.NET MVC web uygulamasından gösterir. ASP.NET MVC bileşenleri yerine yalnızca Azure Cosmos DB'ye odaklanan bir öğretici arıyorsanız bkz. [Azure Cosmos DB C# konsol uygulaması oluşturma](sql-api-get-started.md).

> [!TIP]
> Bu öğretici, ASP.NET MVC ve Azure Web Siteleri'ni kullanma konusunda deneyim sahibi olduğunuzu varsayar. ASP.NET veya [önkoşul araçlarında](#_Toc395637760) yeniyseniz [GitHub][GitHub] konumundan örnek projenin tamamını indirmenizi ve bu örnekteki yönergeleri uygulamanızı öneririz. Oluşturduktan sonra, proje bağlamında kodu daha iyi kavramak için bu makaleyi inceleyebilirsiniz.
> 
> 

## <a name="_Toc395637760"></a>Bu veritabanı öğreticisi için önkoşullar
Bu makaledeki yönergeleri uygulamadan önce aşağıdakilere sahip olduğunuzdan emin olmanız gerekir:

* Etkin bir Azure hesabı.  Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun. 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* [!INCLUDE [cosmos-db-emulator-vs](../../includes/cosmos-db-emulator-vs.md)]  
* Visual Studio 2017, Visual Studio yükleyicisi kullanılabilen .NET için Microsoft Azure SDK.

Bu makaledeki tüm ekran görüntüleri Microsoft Visual Studio Community 2017 kullanılarak alınmıştır. Sisteminiz farklı bir sürüme sahip yapılandırılmışsa ekranlarınızın ve seçeneklerinizin tamamen eşleşmeme olasılığı, ancak yukarıdaki önkoşulları karşılarsanız bu çözümün çalışması gerekir mümkündür.

## <a name="_Toc395637761"></a>1. Adım: Azure Cosmos DB veritabanı hesabı oluşturma
İlk olarak bir Azure Cosmos DB hesabı oluşturalım. SQL hesabı için Azure Cosmos DB zaten varsa veya Bu öğretici için Azure Cosmos DB öykünücüsü kullanıyorsanız, adımına atlayabilirsiniz [yeni bir ASP.NET MVC uygulaması oluşturma](#_Toc395637762).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
Şimdi yeni bir ASP.NET MVC uygulamasının nasıl oluşturulacağını en başından başlayarak inceleyeceğiz. 

## <a name="_Toc395637762"></a>2. Adım: Yeni bir ASP.NET MVC uygulaması oluşturma

1. Visual Studio'da, **Dosya** menüsündeki **Yeni** seçeneğine gidin ve ardından **Proje**'ye tıklayın. **Yeni Proje** iletişim kutusu görünür.

2. **Proje türleri** bölmesinde **Şablonlar**, **Visual C#**, **Web**'i genişletin ve ardından **ASP.NET Web Uygulaması**'nı seçin.

      ![ASP.NET Web Uygulaması proje türü vurgulanmış şekilde Yeni Proje iletişim kutusunun ekran görüntüsü](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. **Ad** kutusunda projenin adını yazın. Bu öğretici "todo" adını kullanır. Bunun dışında bir şey kullanmayı seçerseniz bu öğreticinin todo ad alanından söz ettiği her yerde sağlanan kod örneklerini uygulamanıza verdiğiniz ada göre ayarlamanız gerekir. 
4. Projeyi oluşturmak istediğiniz klasöre gitmek için **Gözat**'a tıklayın ve ardından **Tamam**'a tıklayın.
   
      **Yeni ASP.NET Web uygulaması** iletişim kutusu görüntülenir.
   
    ![MVC uygulama şablonu vurgulanmış ile yeni bir ASP.NET Web uygulaması iletişim kutusunun ekran görüntüsü](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. Şablonlar bölmesinde **MVC**'yi seçin.

6. **Tamam**'a tıklayarak Visual Studio'nun boş ASP.NET MVC şablonu çevresinde iskele oluşturmasını sağlayın. 

          
7. Visual Studio demirbaş MVC uygulamasını oluşturmayı tamamlandıktan sonra, yerel olarak çalıştırabileceğiniz boş bir ASP.NET uygulamasına sahip olursunuz.
   
    Hepimizin ASP.NET "Hello World" uygulamasını gördüğünden emin olduğum için, projeyi yerel olarak çalıştırmayı atlayacağız. Şimdi doğrudan bu projeye Azure Cosmos DB eklemeye ve uygulamamızı oluşturmaya geçelim.

## <a name="_Toc395637767"></a>3. Adım: MVC web uygulaması projenize Azure Cosmos DB ekleme
Bu çözüm için gereken ASP.NET MVC altyapısının çoğunu elde ettiğimize göre, bu öğreticinin asıl amacı olan MVC web uygulamamıza Azure Cosmos DB'yi eklemeye geçelim.

1. Azure Cosmos DB .NET SDK'sı paketlenir ve bir NuGet paketi olarak dağıtılmış. NuGet paketini Visual Studio'da almak için, **Çözüm Gezgini**'nde projeye sağ tıklayarak ve ardından **NuGet Paketlerini Yönet**'e tıklayarak Visual Studio'daki NuGet paket yöneticisini kullanın.
   
    ![NuGet Paketlerini Yönet vurgulanmış şekilde, Çözüm Gezgini'nde web uygulaması projesi için sağ tıklama seçeneklerinin ekran görüntüsü.](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    **NuGet Paketlerini Yönet** iletişim kutusu görünür.
2. NuGet **Gözat** kutusunda ***Azure DocumentDB*** yazın. (Paket adı için Azure Cosmos DB güncelleştirilmemiş.)
   
    Sonuçlardan yüklemek **Microsoft.Azure.DocumentDB Microsoft tarafından** paket. Bu, indirin ve Newtonsoft.Json gibi tüm bağımlılıkları yanı sıra Azure Cosmos DB paketini yükleyin. **Önizleme** penceresinde **Tamam**'a tıklayıp **Lisans Kabulü** penceresinde **Kabul Ediyorum**'a tıklayarak yüklemeyi tamamlayın.
   
    ![Microsoft Azure Cosmos DB istemci kitaplığı vurgulanmış ile NuGet paketlerini Yönet penceresinin ekran görüntüsü](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      Alternatif olarak, paketi yüklemek için Paket Yöneticisi Konsolu'nu kullanabilirsiniz. Bunu yapmak için, **Araçlar** menüsünde **NuGet Paket Yöneticisi**'ne tıklayın ve ardından **Paket Yöneticisi Konsolu**'na tıklayın. İstendiğinde aşağıdakileri yazın.
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. Paket yüklendikten sonra, Visual Studio çözümünüz Microsoft.Azure.Documents.Client ve Newtonsoft.Json olmak üzere iki yeni başvuru eklenmiş şekilde aşağıdakine benzemelidir.
   
    ![Çözüm Gezgini'nde JSON veri projesine eklenen iki başvurunun ekran görüntüsü](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <a name="_Toc395637763"></a>4. Adım: ASP.NET MVC uygulamasını ayarlama
Şimdi bu MVC uygulamasına modeller, görünümler ve denetleyiciler ekleyelim:

* [Model ekleme](#_Toc395637764).
* [Denetleyici ekleme](#_Toc395637765).
* [Görünümler ekleme](#_Toc395637766).

### <a name="_Toc395637764"></a>JSON veri modeli ekleme
MVC'de **M** olan modeli oluşturarak başlayalım. 

1. **Çözüm Gezgini**'nde **Modeller** klasörüne sağ tıklayın, **Ekle**'ye tıklayın ve ardından **Sınıf**'a tıklayın.
   
      **Yeni Öğe Ekle** iletişim kutusu görünür.
2. Yeni sınıfınıza **Item.cs** adını verin ve **Ekle**'ye tıklayın. 
3. Bu yeni **Item.cs** dosyasında, son *using deyiminden* sonra aşağıdakini ekleyin.
   
        using Newtonsoft.Json;
4. Şimdi de bu kodu 
   
        public class Item
        {
        }
   
    aşağıdaki kodla değiştirin.
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    Azure Cosmos DB'deki tüm veriler kablo üzerinden geçer ve JSON olarak depolanır. JSON.NET tarafından nesnelerinizin seri hale getirilme/seri durumundan çıkarılma yolunu denetlemek için, yeni oluşturduğumuz **Item** sınıfında gösterildiği şekilde **JsonProperty** özniteliğini kullanabilirsiniz. Bunu yapmak **zorunda** değilsiniz ancak özelliklerimin JSON camelCase adlandırma kurallarına uyduğundan emin olmak istiyorum. 
   
    Özellik adının biçimini JSON'a gittiği zaman denetlemenin yanı sıra, **Açıklama** özelliğinde yaptığım gibi .NET özelliklerinizi tamamen yeniden adlandırabilirsiniz. 

### <a name="_Toc395637765"></a>Denetleyici ekleme
**M** ile işimiz bitti; şimdi de MVC'deki **C**'yi, yani denetleyici sınıfını oluşturalım.

1. **Çözüm Gezgini**'nde **Denetleyiciler** klasörüne sağ tıklayın, **Ekle**'ye tıklayın ve ardından **Denetleyici**'ye tıklayın.
   
    **İskele Ekle** iletişim kutusu görünür.
2. **MVC 5 Denetleyici - Boş**'u seçin ve ardından **Ekle**'ye tıklayın.
   
    ![MVC 5 Denetleyici - Boş seçeneği vurgulanmış şekilde İskele Ekle iletişim kutusunun ekran görüntüsü](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. Yeni Denetleyicinize **ItemController** adını verin.
   
    ![Denetleyici Ekle iletişim kutusunun ekran görüntüsü](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    Dosya oluşturulduktan sonra, Visual Studio çözümünüz **Çözüm Gezgini**'nde yeni ItemController.cs dosyasıyla aşağıdakine benzemelidir. Daha önce oluşturduğunuz yeni Item.cs dosyası da gösterilmektedir.
   
    ![Yeni ItemController.cs dosyası ve Item.cs dosyası vurgulanmış şekilde Visual Studio çözümü - Çözüm Gezgini'nin ekran görüntüsü](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    ItemController.cs'yi kapatabilirsiniz, buna daha sonra geri döneceğiz. 

### <a name="_Toc395637766"></a>Görünümler ekleme
Şimdi MVC'deki **V**'yi, yani görünümleri oluşturalım:

* [Öğe Dizini görünümü ekleme](#AddItemIndexView).
* [Yeni Öğe görünümü ekleme](#AddNewIndexView).
* [Düzenleme Öğesi görünümü ekleme](#_Toc395888515).

#### <a name="AddItemIndexView"></a>Öğe Dizini görünümü ekleme
1. **Çözüm Gezgini**'nde **Görünümler** klasörünü genişletin, daha önce **ItemController**'ı eklediğinizde Visual Studio'nun sizin için oluşturduğu boş **Öğe** klasörüne sağ tıklayın, **Ekle**'ye tıklayın ve ardından **Görünüm**'e tıklayın.
   
    ![Görünüm Ekle komutları vurgulanmış şekilde Visual Studio'nun oluşturduğu Öğe klasörünü gösteren Çözüm Gezgini'nin ekran görüntüsü](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. **Görünüm Ekle** iletişim kutusunda aşağıdakileri yapın:
   
   * **Görünüm adı** kutusunda ***Index*** yazın.
   * **Şablon** kutusunda ***Liste***'yi seçin.
   * **Model sınıfı** kutusunda ***Öğe (todo.Models)*** seçeneğini belirleyin.
   * Düzen sayfası kutusunda ***~/Views/Shared/_Layout.cshtml*** yazın.
     
   ![Görünüm Ekle iletişim kutusunu gösteren ekran görüntüsü](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. Bu değerlerin tümü ayarlandıktan sonra, **Ekle**'ye tıklayın ve Visual Studio'nun yeni bir şablon görünümü oluşturmasına izin verin. Tamamlandığında, oluşturulan cshtml dosyasını açar. Daha sonra geri döneceğimiz için Visual Studio'daki bu dosyayı kapatabiliriz.

#### <a name="AddNewIndexView"></a>Yeni Öğe görünümü ekleme
**Öğe Dizini** görünümü oluşturmamıza benzer şekilde, şimdi de yeni **Öğeler** oluşturmak için yeni bir görünüm oluşturacağız.

1. **Çözüm Gezgini**'nde **Öğe** klasörüne tekrar sağ tıklayın, **Ekle**'ye tıklayın ve ardından **Görünüm**'e tıklayın.
2. **Görünüm Ekle** iletişim kutusunda aşağıdakileri yapın:
   
   * **Görünüm adı** kutusunda ***Create*** yazın.
   * **Şablon** kutusunda ***Oluştur***'u seçin.
   * **Model sınıfı** kutusunda ***Öğe (todo.Models)*** seçeneğini belirleyin.
   * Düzen sayfası kutusunda ***~/Views/Shared/_Layout.cshtml*** yazın.
   * **Ekle**'ye tıklayın.
   
#### <a name="_Toc395888515"></a>Düzenleme Öğesi görünümü ekleme
Son olarak, bir **Öğe**'yi düzenlemek için daha önce kullandığımız yolu tekrarlayarak son bir görünüm ekleyin.

1. **Çözüm Gezgini**'nde **Öğe** klasörüne tekrar sağ tıklayın, **Ekle**'ye tıklayın ve ardından **Görünüm**'e tıklayın.
2. **Görünüm Ekle** iletişim kutusunda aşağıdakileri yapın:
   
   * **Görünüm adı** kutusunda ***Edit*** yazın.
   * **Şablon** kutusunda ***Düzenle***'yi seçin.
   * **Model sınıfı** kutusunda ***Öğe (todo.Models)*** seçeneğini belirleyin.
   * Düzen sayfası kutusunda ***~/Views/Shared/_Layout.cshtml*** yazın.
   * **Ekle**'ye tıklayın.

Bunu yaptıktan sonra, bu görünümlere daha sonra geri döneceğimiz için Visual Studio'daki tüm cshtml belgelerini kapatın.

## <a name="_Toc395637769"></a>5. Adım: Azure Cosmos DB’yi bağlama
Standart MVC işleri hallolduğuna göre, Azure Cosmos DB için kod eklemeye dönelim. 

Bu bölümde, aşağıdakileri işlemek için kod ekleyeceğiz:

* [Tamamlanmamış Öğeleri listeleme](#_Toc395637770).
* [Öğeler ekleme](#_Toc395637771).
* [Öğeleri düzenleme](#_Toc395637772).

### <a name="_Toc395637770"></a>MVC web uygulamanızda tamamlanmamış Öğeleri listeleme
Burada yapılacak ilk şey, Azure Cosmos DB'ye bağlanmayı ve kullanmayı sağlayan tüm mantığı içeren bir sınıf eklemektir. Bu öğretici için tüm bu mantığı DocumentDBRepository adlı bir depo sınıfına kapsülleyeceğiz. 

1. **Çözüm Gezgini**'nde projeye sağ tıklayın, **Ekle**'ye tıklayın ve ardından **Sınıf**'a tıklayın. Yeni sınıfa **DocumentDBRepository** adını verin ve **Ekle**'ye tıklayın.
2. Yeni oluşturulan **DocumentDBRepository** sınıfında *ad alanı* bildiriminin üstüne aşağıdaki *using deyimlerini* ekleyin
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    Şimdi de bu kodu 
   
        public class DocumentDBRepository
        {
        }
   
    aşağıdaki kodla değiştirin.
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. Bazı değerleri yapılandırmadan okuyoruz, bu nedenle uygulamanızın **Web.config** dosyasını açın ve `<AppSettings>` bölümünün altına aşağıdaki satırları ekleyin.
   
        <add key="endpoint" value="enter the URI from the Keys blade of the Azure Portal"/>
        <add key="authKey" value="enter the PRIMARY KEY, or the SECONDARY KEY, from the Keys blade of the Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. Şimdi de Azure Portal'ın Anahtarlar dikey penceresini kullanarak *endpoint* ve *authKey* değerlerini güncelleştirin. Uç nokta ayarının değeri olarak Anahtarlar dikey penceresinden **URI**'yi kullanın ve authKey ayarının değeri olarak Anahtarlar dikey penceresinden **BİRİNCİL ANAHTAR** veya **İKİNCİL ANAHTAR**'ı kullanın.

    Azure Cosmos DB depoyu şimdi bağlamayı, alır dikkatli uygulama mantığımızı ekleyelim.

1. Bir yapılacaklar listesi uygulamasıyla yapabilmeyi istediğimiz ilk şey, tamamlanmamış öğeleri görüntülemektir.  **DocumentDBRepository** sınıfının içinde herhangi bir yere aşağıdaki kod parçacığını kopyalayıp yapıştırın.
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. Daha önce eklediğimiz **ItemController**'ı açın ve ad alanı bildiriminin üstüne aşağıdaki *using deyimlerini* ekleyin.
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    Projeniz "todo" olarak adlandırılmamışsa using "todo.Models" deyimini projenizin adını yansıtacak şekilde güncelleştirmeniz gerekir.
   
    Şimdi de bu kodu
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    aşağıdaki kodla değiştirin.
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. **Global.asax.cs**'yi açın ve **Application_Start** yöntemine aşağıdaki satırı ekleyin 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

Bu noktada çözümünüzün herhangi bir hata olmadan oluşturulabiliyor olması gerekir.

Uygulamayı şimdi çalıştırırsanız **HomeController**'a ve söz konusu denetleyicinin **Dizin** görünümüne gidersiniz. Başta seçtiğimiz MVC şablonu projesinin varsayılan davranışı budur ancak biz bunu istemiyoruz! Bu davranışı değiştirmek için bu MVC uygulamasındaki yönlendirmeyi değiştirelim.

***App\_Start\RouteConfig.cs***'yi açın, "defaults:" ile başlayan satırı bulun ve aşağıdakine benzeyecek şekilde değiştirin.

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

Bu, yönlendirme davranışını denetlemek için URL'de bir değer belirtmemeniz durumunda, denetleyici olarak **Giriş** yerine **Öğe**'yi ve görünüm olarak **Dizin**'i kullanmasını ASP.NET MVC'ye söyler.

Uygulamayı şimdi çalıştırırsanız uygulama depo sınıfını çağıran ve tamamlanmamış tüm öğeleri **Görünümler**\\**Öğe**\\**Dizin** görünümüne getiren GetItems yöntemini kullanan **ItemController**'ınızı çağırır. 

Bu projeyi şimdi oluşturur ve çalıştırırsanız buna benzeyen bir şey görürsünüz.    

![Bu veritabanı öğreticisi tarafından oluşturulan yapılacaklar listesi web uygulamasının ekran görüntüsü](./media/sql-api-dotnet-application/build-and-run-the-project-now.png)

### <a name="_Toc395637771"></a>Öğeler ekleme
Boş bir kılavuzdan başka şeyler görmek için veritabanımıza biraz öğe ekleyelim.

Azure Cosmos DB'deki kaydı kalıcı hale getirmek için Azure Cosmos DBRepository ve ItemController'a biraz kod ekleyelim.

1. **DocumentDBRepository** sınıfınıza aşağıdaki yöntemi ekleyin.
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   Bu yöntem yalnızca kendisine geçirilen nesneyi alır ve Azure Cosmos DB'de devam ettirir.
2. ItemController.cs dosyasını açın ve sınıfın içine aşağıdaki kod parçacığını ekleyin. ASP.NET MVC **Oluştur** eylemi için ne yapacağını bu şekilde bilir. Bu durumda yalnızca daha önce oluşturulan ilişkili Create.cshtml görünümünü işler.
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    Şimdi bu denetleyicide **Oluştur** görünümünden gönderim kabul edecek biraz daha koda ihtiyacımız var.
3. Bu denetleyici için bir POST formuyla ASP.NET MVC'ye ne yapacağını söyleyen ItemController.cs sınıfına bir sonraki kod blokunu ekleyin.
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    Bu kod DocumentDBRepository'ye çağrı yapar ve yeni todo öğesini veritabanında kalıcı hale getirmek için CreateItemAsync yöntemini kullanır. 
   
    **Güvenlik Notu**: **ValidateAntiForgeryToken** özniteliği burada bu uygulamayı siteler arası istek sahteciliği saldırılarına karşı korunmaya yardımcı olmak için kullanılır. Bu özniteliği eklemek tek başına yeterli değildir, görünümlerinizin de bu sahteciliği karşı önleme belirteci ile çalışması gerekir. Bu konu hakkında daha fazla bilgi ve bunu doğru uygulamaya yönelik örnekler için lütfen bkz. [Siteler Arası İstek Sahteciliğini Önleme][Preventing Cross-Site Request Forgery]. [GitHub][GitHub]'da sağlanan kaynak kodu tam uygulamayı içerir.
   
    **Güvenlik Notu**: Aşırı gönderim saldırılarına karşı korunmaya yardımcı olmak için yöntem parametresinde **Bind** özniteliğini de kullanırız. Daha ayrıntılı bilgi için lütfen bkz. [ASP.NET MVC'de Temel CRUD İşlemleri][Basic CRUD Operations in ASP.NET MVC].

Veritabanımıza yeni Öğeler eklemek için gereken kod burada son bulur.

### <a name="_Toc395637772"></a>Öğeleri Düzenleme
Yapacağımız son bir şey kaldı, bu da veritabanında **Öğeler**'i düzenleme ve bunları tamamlanmış olarak işaretleme özelliğini eklemektir. Düzenleme görünümü projeye zaten eklenmişti, bu nedenle yalnızca denetleyicimize ve **DocumentDBRepository** sınıfına biraz kod eklememiz gereklidir.

1. **DocumentDBRepository** sınıfına aşağıdakileri ekleyin.
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    Bu yöntemlerin ilki olan **GetItem**, Azure Cosmos DB'den bir Öğe getirir ve bu öğe **ItemController**'a ve sonra **Düzenle** görünümüne geçirilir.
   
    Yeni eklediğimiz yöntemlerin ikincisi, Azure Cosmos DB'deki **Belge**'yi, **ItemController**'dan geçirilen **Belge**'nin sürümüyle değiştirir.
2. Aşağıdakileri **ItemController** sınıfına ekleyin.
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    İlk yöntem, kullanıcı **Dizin** görünümünden **Düzenle** bağlantısına tıkladığında meydana gelen Http GET'ini işler. Bu yöntem Azure Cosmos DB'den bir [**Belge**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) getirir ve bunu **Düzenle** görünümüne geçirir.
   
    Ardından, **Düzenle** görünümü **IndexController**'a bir Http POST yapar. 
   
    Eklediğimiz ikinci yöntem, güncelleştirilmiş nesneyi veritabanında kalıcı hale getirmek üzere Azure Cosmos DB'ye geçirir.

Hepsi bu; uygulamamızı çalıştırmak, tamamlanmamış **Öğeleri** listelemek, yeni **Öğeler** eklemek ve **Öğeleri** düzenlemek için ihtiyacımız olan her şey bu kadar.

## <a name="_Toc395637773"></a>6. Adım: Uygulamayı yerel olarak çalıştırma
Yerel makinenizde uygulamayı test etmek için aşağıdakileri yapın:

1. Uygulamayı hata ayıklama modunda oluşturmak için Visual Studio'da F5'e basın. Bu işlemin uygulamayı oluşturması ve bir tarayıcıyı daha önce gördüğümüz boş kılavuz sayfasıyla başlatması gerekir:
   
    ![Bu veritabanı öğreticisi tarafından oluşturulan yapılacaklar listesi web uygulamasının ekran görüntüsü](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. **Yeni Oluştur** bağlantısına tıklayın ve **Ad** ve **Açıklama** alanlarına değerler ekleyin. **Tamamlandı** onay kutusunu seçmeden bırakın, aksi halde yeni **Öğe** tamamlanmış durumda eklenir ve ilk listede görünmez.
   
    ![Oluştur görünümünün ekran görüntüsü](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. **Oluştur**'a tıklayın, böylece **Dizin** görünümüne geri yönlendirilirsiniz ve **Öğeniz** listede görünür.
   
    ![Dizin görünümünün ekran görüntüsü](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    Yapılacaklar listenize birkaç **Öğe** daha ekleyebilirsiniz.
    
4. Listedeki bir **Öğe**'nin yanındaki **Düzenle**'ye tıklayın, böylece **Tamamlandı** bayrağı dahil olmak üzere nesnenizin herhangi bir özelliğini güncelleştirebileceğiniz **Düzenle** görünümüne gidersiniz. **Tamamlandı** bayrağını işaretler ve **Kaydet**'e tıklarsanız **Öğe** tamamlanmamış görevler listesinden kaldırılır.
   
    ![Tamamlandı kutusu işaretlenmiş şekilde Dizin görünümünün ekran görüntüsü](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. Uygulamayı test ettikten sonra, uygulamanın hata ayıklamasını durdurmak için Ctrl+F5'e basın. Dağıtıma hazırsınız!

## <a name="_Toc395637774"></a>7. adım: Azure uygulama hizmeti uygulamaya dağıtma 
Azure Cosmos DB ile düzgün çalışmasını tam uygulama sahip olduğunuza göre bu web uygulamasını Azure App Service'e dağıtmak için yapacağız.  

1. Bu uygulamayı yayımlamak için yapmanız gereken tek şey, **Çözüm Gezgini**'nde projeye sağ tıklamak ve **Yayımla**'ya tıklamaktır.
   
    ![Çözüm Gezgini'nde Yayımla seçeneğinin ekran görüntüsü](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. İçinde **Yayımla** iletişim kutusu, tıklatın **Microsoft Azure App Service**seçeneğini belirleyip **Yeni Oluştur** tıklayın veya bir uygulama hizmeti profili oluşturma **var olanı Seç**  varolan profili kullanmak için.

    ![Visual Studio'da Yayımla iletişim kutusu](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. Var olan bir Azure uygulama hizmeti profiliniz varsa, abonelik adınızı girin. Kullanım **Görünüm** kaynak grubu veya kaynak türü göre sıralamak için filtre sonra Azure uygulama hizmeti seçin. 
   
    ![Visual Studio'da uygulama hizmeti iletişim kutusu](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. Yeni bir Azure uygulama hizmeti profili oluşturmak için tıklatın **Yeni Oluştur** içinde **Yayımla** iletişim kutusu. İçinde **App Service Oluştur** iletişim kutusunda, Web uygulaması adı ve uygun abonelik, kaynak grubu ve uygulama hizmeti planı girin ve ardından **oluşturma**.

    ![Visual Studio'da uygulama hizmeti iletişim kutusu oluşturma](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

Visual Studio birkaç saniye içinde web uygulamanızı yayımlamayı bitirecek ve Azure'da çalışan, handiwork görebileceğiniz bir tarayıcıyı başlatacak!



## <a name="_Toc395637775"></a>Sonraki adımlar
Tebrikler! Yalnızca ilk ASP.NET MVC Azure Cosmos DB kullanarak web uygulaması oluşturdunuz ve bunu Azure yayımladınız. Bu öğreticide bulunmayan ayrıntı ve silme işlevleri dahil olmak üzere, tüm uygulamanın kaynak kodu [GitHub][GitHub]'dan indirilebilir veya kopyalanabilir. Uygulamanıza bunları eklemek isterseniz kodu alın ve bu uygulamaya ekleyin.

Uygulamanıza ek işlevsellik eklemek için kullanılabilen API'leri inceleyin [Azure Cosmos DB .NET kitaplığı](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) ve Azure Cosmos DB .NET Kitaplığı'na katkıda bulunmaktan çekinmeyin [GitHub] [GitHub]. 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
