---
title: "Azure Cosmos DB için ASP.NET MVC öğreticisi: Web Uygulaması Geliştirme | Microsoft Docs"
description: "ASP.NET MVC Öğreticisi toocreate Azure Cosmos DB kullanarak bir MVC web uygulaması. Azure Web Siteleri'nde barındırılan bir yapılacaklar uygulamasında JSON ve erişim verilerini depolayacaksınız - adım adım ASP.NET MVC öğreticisi."
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
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395809351"></a>ASP.NET MVC Öğreticisi: Azure Cosmos DB ile Web uygulaması geliştirme
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

toohighlight nasıl verimli bir şekilde Azure Cosmos DB toostore yararlanır ve JSON belgelerini sorgulamak bu makalede nasıl gösteren bir uçtan uca kılavuz sağlar toobuild Azure Cosmos DB kullanarak bir Yapılacaklar uygulamasının. Merhaba görevleri Azure Cosmos DB JSON belgeleri olarak depolanır.

![Merhaba Yapılacaklar listesi MVC web uygulaması Bu öğretici - adım adım Asp.net MVC Öğreticisi tarafından oluşturulan ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

Bu kılavuz size nasıl toouse hello Azure Cosmos DB hizmeti toostore ve erişim verilerini Azure üzerinde barındırılan bir ASP.NET MVC web uygulamasından gösterir. Yalnızca Azure Cosmos DB odaklanan bir öğretici arıyorsanız ve hello ASP.NET MVC bileşenleri görmezsiniz [bir Azure Cosmos DB C# konsol uygulaması oluşturma](documentdb-get-started.md).

> [!TIP]
> Bu öğretici, ASP.NET MVC ve Azure Web Siteleri'ni kullanma konusunda deneyim sahibi olduğunuzu varsayar. Yeni tooASP.NET veya hello ise [önkoşul araçlarında](#_Toc395637760), hello konumundan örnek projenin tamamını indirme öneririz [GitHub] [ GitHub] hello yönergeleri izleyerek Bu örnek. Oluşturduktan sonra bu makale toogain Insight hello proje hello bağlamında hello kodu gözden geçirebilirsiniz.
> 
> 

## <a name="_Toc395637760"></a>Bu veritabanı öğreticisi için önkoşullar
Bu makaledeki Hello yönergeleri izlemeden önce hello aşağıdaki sahip olduğundan emin olun:

* Etkin bir Azure hesabı. Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/). 

    OR

    Merhaba yerel yüklemesi [Azure Cosmos DB öykünücüsü](local-emulator.md).
* [Visual Studio 2017](http://www.visualstudio.com/).  
* Visual Studio 2017, Visual Studio yükleyicisi hello kullanılabilen .NET için Microsoft Azure SDK.

Tüm hello ekran görüntüleri bu makalede Microsoft Visual Studio Community 2017 kullanılarak alınmıştır. Sisteminiz farklı bir sürüme sahip yapılandırılmışsa ekranlarınızın ve seçeneklerinizin tamamen eşleşmeme olasılığı, ancak hello yukarıdaki Önkoşullar karşılıyorsa bu çözümün çalışması gerekir mümkündür.

## <a name="_Toc395637761"></a>1. Adım: Azure Cosmos DB veritabanı hesabı oluşturma
İlk olarak bir Azure Cosmos DB hesabı oluşturalım. Zaten bir SQL (DocumentDB) hesabı için Azure Cosmos DB veya kullanıyorsanız bu öğretici için Azure Cosmos DB öykünücüsü Merhaba, çok atlayabilirsiniz[yeni bir ASP.NET MVC uygulaması oluşturma](#_Toc395637762).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
Biz şimdi nasıl toocreate hello yeni bir ASP.NET MVC uygulamasından başından başlayarak yukarı aracılığıyla yol gösterir. 

## <a name="_Toc395637762"></a>2. Adım: Yeni bir ASP.NET MVC uygulaması oluşturma

1. Visual Studio'da, hello **dosya** menüsünde çok noktası**yeni**ve ardından **proje**. Merhaba **yeni proje** iletişim kutusu görüntülenir.

2. Merhaba, **proje türleri** bölmesini genişletin **şablonları**, **Visual C#**, **Web**ve ardından **ASP.NET Web uygulaması** .

      ![Merhaba yeni proje iletişim kutusu ile Merhaba ASP.NET Web uygulaması proje türü vurgulanmış ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. Merhaba, **adı** kutusu, hello projesinin türü hello adı. Bu öğretici "todo" Merhaba adını kullanır. Bunun dışında bir şey toouse seçerseniz, Bu öğretici hello todo ad alanıyla ilgili ettiği her yerde sonra tooadjust hello sağlanan kod örnekleri toouse uygulamanızı adlı yeterlidir. 
4. Tıklatın **Gözat** Burada, gibi toocreate hello proje ve ardından toonavigate toohello klasörü **Tamam**.
   
      Merhaba **yeni ASP.NET Web uygulaması** iletişim kutusu görüntülenir.
   
    ![Merhaba MVC uygulama şablonu vurgulanmış ile Merhaba yeni ASP.NET Web uygulaması iletişim kutusu ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. Merhaba Şablonlar bölmesinde seçin **MVC**.

6. Tıklatın **Tamam** ve Visual Studio yapı iskelesi hello boş ASP.NET MVC şablonu çevresinde oluşturmasını sağlayabilirsiniz. 

          
7. Visual Studio hello Demirbaş MVC uygulamasını oluşturmayı tamamlandıktan sonra yerel olarak çalıştırabileceğiniz boş bir ASP.NET uygulamasına sahip.
   
    Yerel olarak biz olduğunuz tüm görülen hello ASP.NET "Hello World" emin olduğum için çalışan hello proje atlayın uygulama. Düz tooadding Azure Cosmos DB toothis proje ve uygulamamızı oluşturmaya edelim.

## <a name="_Toc395637767"></a>3. adım: Azure Cosmos DB tooyour MVC web uygulaması projesi ekleme
Biz bu çözüm için ihtiyacımız hello ASP.NET MVC tesisat çoğunu sahip olduğunuza göre şimdi Azure Cosmos DB tooour MVC web uygulaması ekleme, bu öğreticinin asıl amacı toohello alın.

1. Hello Azure Cosmos DB .NET SDK'sını paketlenir ve bir NuGet paketi olarak dağıtılmış. tooget Visual Studio'da NuGet paketi Merhaba, hello projeye sağ tıklayarak Visual Studio'daki hello NuGet paket yöneticisini kullanın **Çözüm Gezgini** ve ardından **NuGet paketlerini Yönet**.
   
    ![Merhaba ekran görüntüsü seçenekler NuGet paketlerini Yönet vurgulanmış ile Çözüm Gezgini'nde başlangıç web uygulaması projesi için sağ tıklatın.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    Merhaba **NuGet paketlerini Yönet** iletişim kutusu görüntülenir.
2. Merhaba NuGet içinde **Gözat** kutusuna ***Azure DocumentDB***. (Merhaba paket adı güncelleştirilmiş tooAzure Cosmos DB yedeklenmedi.)
   
    Merhaba sonuçlarından hello yüklemek **Microsoft.Azure.DocumentDB Microsoft tarafından** paket. Bu, indirin ve Newtonsoft.Json gibi tüm bağımlılıkları yanı sıra hello Azure Cosmos DB paketini yükleyin. ' I tıklatın **Tamam** hello içinde **Önizleme** penceresinde ve **kabul ediyorum** hello içinde **lisans kabulünü** penceresi toocomplete hello yükleme.
   
    ![Microsoft Azure DocumentDB istemci kitaplığı vurgulanmış hello ile Merhaba NuGet paketlerini Yönet penceresinin ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      Alternatif olarak, Paket Yöneticisi konsolu tooinstall hello paket hello kullanabilirsiniz. toodo şekilde, hello **Araçları** menüsünde tıklatın **NuGet Paket Yöneticisi**ve ardından **Paket Yöneticisi Konsolu**. Merhaba isteminde hello aşağıdakini yazın.
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. Merhaba paket yüklendikten sonra Visual Studio çözümünüzü eklenen, iki yeni başvuru Microsoft.Azure.Documents.Client ve Newtonsoft.Json hello aşağıdakilerle benzemelidir.
   
    ![Merhaba iki başvurunun ekran görüntüsü, Çözüm Gezgini'nde toohello JSON veri projesine eklendi](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <a name="_Toc395637763"></a>4. adım: ASP.NET MVC uygulaması hello ayarlama
Şimdi Merhaba modeller, görünümler ve denetleyiciler toothis MVC uygulaması ekleyelim:

* [Model ekleme](#_Toc395637764).
* [Denetleyici ekleme](#_Toc395637765).
* [Görünümler ekleme](#_Toc395637766).

### <a name="_Toc395637764"></a>JSON veri modeli ekleme
Merhaba oluşturarak başlayalım **M** MVC'de, model hello. 

1. İçinde **Çözüm Gezgini**, sağ hello **modelleri** klasörünü tıklatın **Ekle**ve ardından **sınıfı**.
   
      Merhaba **Yeni Öğe Ekle** iletişim kutusu görüntülenir.
2. Yeni sınıfınıza **Item.cs** adını verin ve **Ekle**'ye tıklayın. 
3. Bu yeni **Item.cs** dosya, hello aşağıdakileri hello sonra son ekleyin *deyimiyle*.
   
        using Newtonsoft.Json;
4. Şimdi de bu kodu 
   
        public class Item
        {
        }
   
    koddan hello ile.
   
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
   
    Tüm veriler Azure Cosmos veritabanı hello kablo üzerinden geçer ve JSON olarak depolanır. nesnelerinizin seri/seri kullanabileceğiniz JSON.NET tarafından toocontrol hello şekilde hello **Item** özniteliği hello gösterildiği gibi **öğesi** yeni oluşturduğumuz sınıfı. Sizin **sahip** toodo bu ancak sorun istediğiniz tooensure özelliklerimin hello JSON camelCase adlandırma kuralları izleyin. 
   
    JSON'a gittiği ancak hello ile olduğu gibi .NET özelliklerinizi tamamen adlandırabilirsiniz hello özellik adının hello biçimi yalnızca denetleyebilirsiniz **açıklama** özelliği. 

### <a name="_Toc395637765"></a>Denetleyici ekleme
Merhaba mvc'deki **M**, şimdi hello oluşturalım **C** ' yi, yani denetleyici sınıfını.

1. İçinde **Çözüm Gezgini**, sağ hello **denetleyicileri** klasörünü tıklatın **Ekle**ve ardından **denetleyicisi**.
   
    Merhaba **İskele Ekle** iletişim kutusu görüntülenir.
2. **MVC 5 Denetleyici - Boş**'u seçin ve ardından **Ekle**'ye tıklayın.
   
    ![MVC 5 denetleyici - boş seçeneği vurgulanmış hello ile Merhaba İskele Ekle iletişim kutusunun ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. Yeni Denetleyicinize **ItemController** adını verin.
   
    ![Merhaba denetleyici Ekle iletişim kutusunun ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    Merhaba dosya oluşturulduktan sonra Visual Studio çözümünüzü hello aşağıdaki hello yeni Itemcontroller.cs dosyasıyla benzemelidir **Çözüm Gezgini**. Merhaba daha önce oluşturduğunuz yeni Item.cs dosyası da gösterilmektedir.
   
    ![Merhaba Visual Studio çözümü - hello yeni Itemcontroller.cs dosyası ve Item.cs dosyası vurgulanmış şekilde çözüm Gezgini'nin ekran](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    Itemcontroller.cs'yi kapatabilirsiniz, biz tooit daha sonra yine gelmenizi. 

### <a name="_Toc395637766"></a>Görünümler ekleme
Şimdi, hello oluşturalım **V** MVC uygulamasında hello görünümleri:

* [Öğe Dizini görünümü ekleme](#AddItemIndexView).
* [Yeni Öğe görünümü ekleme](#AddNewIndexView).
* [Düzenleme Öğesi görünümü ekleme](#_Toc395888515).

#### <a name="AddItemIndexView"></a>Öğe Dizini görünümü ekleme
1. İçinde **Çözüm Gezgini**, hello genişletin **görünümleri** klasörü, sağ hello boş **öğesi** hello eklediğinizde Visual Studio için oluşturduğunuz klasöre  **Itemcontroller** daha önce tıklatın **Ekle**ve ardından **Görünüm**.
   
    ![Visual Studio hello Görünüm Ekle komutları vurgulanmış oluşturulan hello öğe klasörünü gösteren Çözüm Gezgini ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. Merhaba, **Görünüm Ekle** iletişim kutusunda, aşağıdaki hello:
   
   * Merhaba, **Görünüm adı** kutusuna ***dizin***.
   * Merhaba, **şablonu** kutusunda ***listesi***.
   * Merhaba, **Model sınıfı** kutusunda ***öğesi (Yapılacaklar. Modeller)***.
   * Merhaba düzen sayfası kutusunda yazın ***~/Views/Shared/_Layout.cshtml***.
     
   ![Ekran görüntüsü gösteren hello Görünüm Ekle iletişim kutusu](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. Bu değerlerin tümü ayarlandıktan sonra, **Ekle**'ye tıklayın ve Visual Studio'nun yeni bir şablon görünümü oluşturmasına izin verin. Bunu yaptıktan sonra oluşturulan hello cshtml dosyasını açar. Biz tooit daha sonra yine gelmenizi şekilde Biz bu dosyayı Visual Studio kapatabilirsiniz.

#### <a name="AddNewIndexView"></a>Yeni Öğe görünümü ekleme
Oluşturduğumuz benzer toohow bir **öğe dizini** görünümü, biz şimdi oluşturacak yeni oluşturmak için yeni bir görünüm **öğeleri**.

1. İçinde **Çözüm Gezgini**, sağ hello **öğesi** klasörü yeniden tıklatın **Ekle**ve ardından **Görünüm**.
2. Merhaba, **Görünüm Ekle** iletişim kutusunda, aşağıdaki hello:
   
   * Merhaba, **Görünüm adı** kutusuna ***oluşturma***.
   * Merhaba, **şablonu** kutusunda ***oluşturma***.
   * Merhaba, **Model sınıfı** kutusunda ***öğesi (Yapılacaklar. Modeller)***.
   * Merhaba düzen sayfası kutusunda yazın ***~/Views/Shared/_Layout.cshtml***.
   * **Ekle**'ye tıklayın.
   
#### <a name="_Toc395888515"></a>Düzenleme Öğesi görünümü ekleme
Ve son olarak, düzenleme için son bir görünüm ekleyin bir **öğesi** hello içinde öncekiyle aynı şekilde.

1. İçinde **Çözüm Gezgini**, sağ hello **öğesi** klasörü yeniden tıklatın **Ekle**ve ardından **Görünüm**.
2. Merhaba, **Görünüm Ekle** iletişim kutusunda, aşağıdaki hello:
   
   * Merhaba, **Görünüm adı** kutusuna ***Düzenle***.
   * Merhaba, **şablonu** kutusunda ***Düzenle***.
   * Merhaba, **Model sınıfı** kutusunda ***öğesi (Yapılacaklar. Modeller)***.
   * Merhaba düzen sayfası kutusunda yazın ***~/Views/Shared/_Layout.cshtml***.
   * **Ekle**'ye tıklayın.

Bunu yaptıktan sonra toothese görünümleri daha sonra geri döneceksiniz olarak Visual Studio tüm hello cshtml belgelerini kapatın.

## <a name="_Toc395637769"></a>5. Adım: Azure Cosmos DB’yi bağlama
Merhaba standart MVC işleri hallolduğuna göre tooadding hello kodu Azure Cosmos DB dönelim. 

Bu bölümde, kod toohandle hello aşağıdaki ekleyeceğiz:

* [Tamamlanmamış Öğeleri listeleme](#_Toc395637770).
* [Öğeler ekleme](#_Toc395637771).
* [Öğeleri düzenleme](#_Toc395637772).

### <a name="_Toc395637770"></a>MVC web uygulamanızda tamamlanmamış Öğeleri listeleme
Merhaba ilk şey toodo burada olan tüm hello mantığı tooconnect tooand kullanım Azure Cosmos DB içeren bir sınıf ekleyin. Bu öğretici için size tüm bu mantığı DocumentDBRepository adlı tooa depo sınıfına kapsülleyeceğiz. 

1. İçinde **Çözüm Gezgini**, hello projeye sağ tıklayın, **Ekle**ve ardından **sınıfı**. Ad hello yeni sınıf **DocumentDBRepository** tıklatıp **Ekle**.
2. Yeni oluşturulan hello içinde **DocumentDBRepository** sınıfı ve hello aşağıdakileri ekleyin *using deyimleri* hello yukarıda *ad alanı* bildirimi
   
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
   
    koddan hello ile.
   
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
   
    
3. Bazı değerler yapılandırmasından okuduğunuz, bu nedenle hello Aç **Web.config** uygulamanızın dosyasını ve satırlar hello altında aşağıdaki hello ekleyin `<AppSettings>` bölümü.
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. Şimdi, hello değerlerini güncelleştirin *endpoint* ve *authKey* hello anahtarlar dikey penceresinde hello Azure Portal kullanarak. Merhaba kullanmak **URI** hello hello uç noktası ayarı ve kullanım hello hello değeri olarak anahtarlar dikey penceresinden **birincil anahtar**, veya **ikincil anahtar** hello hello hello değeri olarak anahtarlar dikey penceresinden authKey ayarının.

    Alır dikkatli'hello Azure Cosmos DB depoyu şimdi bağlamayı, uygulama mantığımızı ekleyelim.

1. Merhaba ilk şey toodisplay hello tamamlanmamış öğeleri toobe mümkün toodo bir Yapılacaklar listesi uygulaması ile olan istiyoruz.  Aşağıdaki kod parçacığını hello içinde istediğiniz yere hello kopyalayıp **DocumentDBRepository** sınıfı.
   
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
2. Açık hello **Itemcontroller** daha önce eklenen ve hello aşağıdakileri ekleyin *using deyimleri* hello ad alanı bildiriminin üstüne.
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    Projeniz "todo" adlı değil, ardından "todo. kullanarak tooupdate gerekir Modelleri"; projeniz tooreflect hello adı.
   
    Şimdi de bu kodu
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    koddan hello ile.
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. Açık **Global.asax.cs** ve satır toohello aşağıdaki hello ekleyin **Application_Start** yöntemi 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

Bu noktada çözümünüzün hatasız mümkün toobuild olmalıdır.

Merhaba uygulamayı şimdi çalıştırırsanız toohello geçecek **HomeController** ve hello **dizin** söz konusu denetleyicinin görünümü. Merhaba başlangıcında seçtik hello MVC şablonu projesinin hello varsayılan davranışı budur ancak biz bunu istemiyoruz! Bu davranış bu MVC uygulama tooalter yönlendirme hello değiştirelim.

Açık ***uygulama\_Start\RouteConfig.cs*** ve başlayarak hello satırı bulun "Varsayılanları:" ve aşağıdaki tooresemble hello değiştirin.

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

Bu şimdi hello URL toocontrol bir değer belirtmediyseniz, yönlendirme davranışını yerine hello ASP.NET MVC söyler **giriş**, kullanın **öğesi** hello denetleyici ve kullanıcı olarak **dizin** hello görünüm olarak.

Merhaba uygulaması çalıştırırsanız, bunu şimdi, **Itemcontroller** hangi toohello depo sınıfında çağırın ve tüm hello tamamlanmamış öğeleri toohello hello Getıtems yöntemini tooreturn kullanmak **görünümleri** \\ **Öğesi**\\**dizin** görünümü. 

Bu projeyi şimdi oluşturur ve çalıştırırsanız buna benzeyen bir şey görürsünüz.    

![Bu veritabanı Öğreticisi tarafından oluşturulan hello Yapılacaklar listesi web uygulamasının ekran görüntüsü](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <a name="_Toc395637771"></a>Öğeler ekleme
Şimdi bir boş kılavuz toolook başka şeyler sahibiz şekilde bazı öğeler Veritabanımıza yerleştirin.

Bazı kodlar çok ekleyelim Azure Cosmos DBRepository ve Itemcontroller'a toopersist hello kayıt Azure Cosmos veritabanı.

1. Yöntem tooyour aşağıdaki hello eklemek **DocumentDBRepository** sınıfı.
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   Bu yöntem yalnızca tooit geçirilen nesneyi alır ve Azure Cosmos DB'de devam ettirir.
2. Merhaba Itemcontroller.cs dosyasını açın ve aşağıdaki kod parçacığını hello sınıfı içinde hello ekleyin. ASP.NET MVC hello için hangi toodo nasıl bilir budur **oluşturma** eylem. Bu durumda yalnızca işleme hello Create.cshtml görünümünü daha önce oluşturulan ilişkili.
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    Şimdi bu denetleyici hello hello gönderim kabul edecek biraz daha koda ihtiyacımız **oluşturma** görünümü.
3. Merhaba sonraki bloğu kod toohello hangi toodo Bu denetleyici için POST formuyla ASP.NET MVC söyleyen Itemcontroller.cs sınıfına ekleyin.
   
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
   
    Bu kod toohello DocumentDBRepository çağırır ve hello Createıtemasync yöntemini toopersist hello yeni Yapılacaklar öğesi toohello bir veritabanı kullanır. 
   
    **Güvenlik Notu**: Merhaba **ValidateAntiForgeryToken** özniteliği kullanılır burada toohelp bu uygulamayı siteler arası istek sahteciliği saldırılarına karşı koruyun. Bu öznitelik yalnızca eklemekten daha fazla tooit, kendi görünümlerinizi de bu sahteciliğe karşı koruma belirteci ile toowork gerekir. Merhaba konu ve nasıl tooimplement bunu doğru şekilde, lütfen görmek örnekleri hakkında daha fazla bilgi için [siteler arası istek sahteciliğini önleme][Preventing Cross-Site Request Forgery]. Sağlanan kaynak kodu Hello [GitHub] [ GitHub] hello tam uygulamayı içerir.
   
    **Güvenlik Notu**: hello de kullanırız **bağlamak** hello yöntemi parametresi toohelp öznitelikte aşırı gönderim saldırılarına karşı koruyun. Daha ayrıntılı bilgi için lütfen bkz. [ASP.NET MVC'de Temel CRUD İşlemleri][Basic CRUD Operations in ASP.NET MVC].

Merhaba gerekli kod tooadd yeni öğeleri tooour veritabanı sonlanır.

### <a name="_Toc395637772"></a>Öğeleri Düzenleme
Toodo bize için son bir şey yoktur ve tooadd hello özelliği tooedit **öğeleri** hello veritabanı ve toomark olarak tamamlandı. Merhaba düzenleme görünümü zaten toohello proje eklenmiş, yalnızca tooadd ihtiyacımız şekilde tooour denetleyici ve toohello bazı kodu **DocumentDBRepository** yeniden sınıf.

1. Toohello aşağıdaki hello eklemek **DocumentDBRepository** sınıfı.
   
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
   
    Bu yöntemlerin ilki olan Hello **GetItem** Azure Cosmos DB'den geri toohello geçirilen bir öğe getirir **Itemcontroller** ve ardından toohello **Düzenle** görünümü.
   
    Merhaba hello yöntemlerinin ikinci yalnızca değiştirir hello eklediğimiz **belge** Azure Cosmos veritabanı hello hello sürümüyle **belge** hello geçirilen **Itemcontroller**.
2. Toohello aşağıdaki hello eklemek **Itemcontroller** sınıfı.
   
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
   
    Merhaba ilk yöntemi tanıtıcıları hello kullanıcı tıkladığında, üzerinde hello olur Http GET hello **Düzenle** hello bağlantısından **dizin** görünümü. Bu yöntem getirir bir [ **belge** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) Azure Cosmos DB'den ve toohello geçirir **Düzenle** görünümü.
   
    Merhaba **Düzenle** görünüm sonra bir Http POST toohello yapın **Indexcontroller**. 
   
    güncelleştirilmiş hello nesne tooAzure Cosmos DB toobe geçirme tanıtıcıları eklediğimiz ikinci yöntem hello hello veritabanında kalıcı.

Bunu ihtiyacımız olan her şey toorun uygulamamız olan olan, tamamlanmamış listesi **öğeleri**, yeni Ekle **öğeleri**ve düzenleme **öğeleri**.

## <a name="_Toc395637773"></a>6. adım: hello uygulama yerel olarak çalıştırma
yerel makinenizde tootest Merhaba uygulaması hello aşağıdaki:

1. Visual Studio toobuild hello uygulamasında hata ayıklama modunda F5'e basın. Merhaba uygulaması derleme ve önce gördüğümüz hello boş kılavuz sayfasıyla bir tarayıcıyı başlatacak:
   
    ![Bu veritabanı Öğreticisi tarafından oluşturulan hello Yapılacaklar listesi web uygulamasının ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. Merhaba tıklatın **Yeni Oluştur** değerleri toohello ekleyin ve bağlama **adı** ve **açıklama** alanları. Merhaba bırakın **tamamlandı** onay kutusu seçili değilse hello yeni **öğesi** tamamlanmış durumda eklenir ve hello ilk listede görünmez.
   
    ![Merhaba Oluştur görünümünün ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. Tıklatın **oluşturma** ve yeniden yönlendirilen geri toohello **dizin** Görünüm ve **öğesi** hello listesinde görünür.
   
    ![Merhaba dizin görünümünün ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    Ücretsiz tooadd birkaç daha eşitleyerek **öğeleri** tooyour Yapılacaklar listesi.
    
4. Tıklatın **Düzenle** sonraki tooan **öğesi** hello listedeki toohello alınır **Düzenle** hello dahil olmak üzere nesnenizin herhangi bir özelliği güncelleştirme Görünüm  **Tamamlanan** bayrağı. Merhaba işaretlerseniz **tam** bayrak ve tıklatın **kaydetmek**, hello **öğesi** hello tamamlanmamış görevler listesinden kaldırılır.
   
    ![Merhaba hello tamamlandı kutusu işaretli şekilde dizin görünümünün ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. Merhaba uygulamayı test ettikten sonra Ctrl + F5 toostop hello uygulama hata ayıklama tuşuna basın. Hazır toodeploy olduğunuz!

## <a name="_Toc395637774"></a>7. adım: hello uygulama tooAzure uygulama hizmeti dağıtma 
Merhaba tam uygulamaya sahip olduğunuza Azure Cosmos DB ile düzgün çalışmasını toodeploy bu web uygulaması tooAzure uygulama hizmeti yapacağız.  

1. toopublish toodo ihtiyacınız bu uygulamanın tüm olduğunu hello projeye sağ tıklayın **Çözüm Gezgini** tıklatıp **Yayımla**.
   
    ![Merhaba Çözüm Gezgini'nde Yayımla seçeneğinin ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. Merhaba, **Yayımla** iletişim kutusu, tıklatın **Microsoft Azure App Service**seçeneğini belirleyip **Yeni Oluştur** toocreate bir uygulama hizmeti profil ya da'ı tıklatın **seçin Varolan** toouse bir profil.

    ![Visual Studio'da Yayımla iletişim kutusu](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. Var olan bir Azure uygulama hizmeti profiliniz varsa, abonelik adınızı girin. Kullanım hello **Görünüm** toosort kaynak grubu veya kaynak türü tarafından filtre sonra Azure uygulama hizmeti seçin. 
   
    ![Visual Studio'da uygulama hizmeti iletişim kutusu](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. Yeni bir Azure uygulama hizmeti profili toocreate tıklatın **Yeni Oluştur** hello içinde **Yayımla** iletişim kutusu. Merhaba, **App Service Oluştur** iletişim kutusunda, Web uygulaması adı ve uygun abonelik, kaynak grubu ve uygulama hizmeti planı girin ve ardından **oluşturma**.

    ![Visual Studio'da uygulama hizmeti iletişim kutusu oluşturma](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

Visual Studio birkaç saniye içinde web uygulamanızı yayımlamayı bitirecek ve Azure'da çalışan, handiwork görebileceğiniz bir tarayıcıyı başlatacak!



## <a name="_Toc395637775"></a>Sonraki adımlar
Tebrikler! Yalnızca ilk ASP.NET MVC Azure Cosmos DB kullanarak web uygulaması oluşturdunuz ve bunu tooAzure yayımladınız. Merhaba hello ayrıntı dahil olmak üzere Merhaba tam uygulaması için kaynak kodu ve silme bu dahil edilmemiş işlevlerinin öğretici indirilebilir veya kopyalamanın [GitHub][GitHub]. Bu nedenle bu tooyour uygulama eklemek isterseniz hello kodu alın ve toothis uygulama ekleyin.

tooadd ek işlevler tooyour uygulama, gözden geçirme hello API'leri hello kullanılabilir [Azure Cosmos DB .NET kitaplığı](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) üzerinde boş toocontribute toohello Azure Cosmos DB .NET kitaplığı eşitleyerek [GitHub] [GitHub]. 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
