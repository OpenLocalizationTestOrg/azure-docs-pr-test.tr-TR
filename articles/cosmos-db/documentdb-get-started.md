---
title: "Azure Cosmos DB: DocumentDB API başlangıç öğreticisi | Microsoft Docs"
description: "Çevrimiçi bir veritabanı ve hello DocumentDB API kullanarak C# konsol uygulaması oluşturan bir Öğreticisi."
keywords: "nosql öğreticisi, çevrimiçi veritabanı, c# konsol uygulaması"
services: cosmos-db
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2017
ms.author: anhoh
ms.openlocfilehash: 65a181f715a670987492ad7815ef2ec94498e84d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a>Azure Cosmos DB: DocumentDB API başlangıç öğreticisi
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [MongoDB için Node.js](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Hoş Geldiniz toohello Azure Cosmos DB DocumentDB API başlangıç Öğreticisi! Bu öğreticiyi uyguladıktan sonra, Azure Cosmos DB kaynaklarını oluşturan ve sorgulayan bir konsol uygulamasına sahip olacaksınız.

Şu konulara değineceğiz:

* Oluşturma ve tooan Azure Cosmos DB hesabına bağlanma
* Visual Studio Çözümünüzü yapılandırma
* Çevrimiçi bir veritabanı oluşturma
* Koleksiyon oluşturma
* JSON belgeleri oluşturma
* Merhaba koleksiyonu sorgulama
* Bir belgeyi değiştirme
* Bir belgeyi silme
* Merhaba veritabanını silme

Zamanınız yok mu? Endişelenmeyin! Merhaba eksiksiz bir çözüm edinilebilir [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). Toohello atlama [hello tam NoSQL Öğreticisi çözümü edinme bölümüne](#GetSolution) hızlı yönergeler için.

Daha sonra lütfen hello kullan oylama hello üstüne veya altına bu sayfa toogive, bize geri bildirim düğmeler. Bize istiyorsanız toocontact doğrudan düşündüğünüz e-posta adresi serbest tooinclude yorumlarınızı içinde.

Şimdi başlayalım!

## <a name="prerequisites"></a>Ön koşullar
Merhaba aşağıdaki sahip olduğunuzdan emin olun:

* Etkin bir Azure hesabı. Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz. 
    * Alternatif olarak, hello kullanabilirsiniz [Azure Cosmos DB öykünücüsü](local-emulator.md) Bu öğretici için.
* [Visual Studio Community 2017](http://www.visualstudio.com/).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>1. Adım: Azure Cosmos DB hesabı oluşturma
Bir Azure Cosmos DB hesabı oluşturalım. Toouse istediğiniz bir hesap zaten varsa, şimdi çok atlayabilirsiniz[Visual Studio çözümünüzü kurma](#SetupVS). Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) toosetup öykünücüsü hello ve İleri çok atlayabilirsiniz[Visual Studio çözümünüzü kurma](#SetupVS).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>2. Adım: Visual Studio çözümünüzü kurma
1. Bilgisayarınızda **Visual Studio 2017**'yi açın.
2. Merhaba üzerinde **dosya** menüsünde, select **yeni**ve ardından **proje**.
3. Merhaba, **yeni proje** iletişim kutusunda **şablonları** / **Visual C#** / **konsol uygulaması**, adı Proje ve ardından **Tamam**.
   ![Merhaba yeni proje penceresinin ekran görüntüsü](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)
4. Merhaba, **Çözüm Gezgini**, Visual Studio çözümünüzün yeni konsol uygulamanızın üzerinde sağ tıklayın ve ardından **NuGet paketlerini Yönet...**
    
    ![Merhaba sağ tıklama menüsünün hello proje için ekran görüntüsü](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. Merhaba, **Nuget** sekmesini tıklatın, **Gözat**ve türü **azure documentdb** hello arama kutusuna.
6. Merhaba sonuçları içinde bulmak **Microsoft.Azure.DocumentDB** tıklatıp **yükleme**.
   Merhaba hello Azure Cosmos DB DocumentDB API'si istemci kitaplığı için paket kimliği [Microsoft Azure DocumentDB istemci Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).
   ![Azure Cosmos DB istemci SDK'sını bulmak için Nuget menüsünün hello ekran görüntüsü](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)

    Değişiklikleri toohello çözümü gözden geçirme hakkında bir ileti alırsanız tıklatın **Tamam**. Lisans kabulü hakkında bir ileti alırsanız **Kabul ediyorum**'a tıklayın.

Harika! Biz hello Kurulumu tamamladığımıza göre biraz kod yazmaya başlayalım. Bu öğreticinin tamamlanmış kod projesini [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs)'da bulabilirsiniz.

## <a id="Connect"></a>3. adım: tooan Azure Cosmos DB hesap bağlanma
İlk olarak, bunlar ekleyin başvuran C# uygulamanız, hello Program.cs dosyasındaki toohello başlangıcı:

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> Sipariş toocomplete hello öğreticide hello yukarıdaki bağımlılıkları eklediğinizden emin olun.
> 
> 

Şimdi bu iki sabiti ve *client* değişkeninizi *Program* ortak sınıfının altına ekleyin.

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

Ardından, head geri toohello [Azure Portal](https://portal.azure.com) tooretrieve uç noktasının URL'sini ve birincil anahtar. Merhaba uç noktasının URL'sini ve birincil anahtar, uygulama toounderstand için gerekli olan nerede tooconnect ve Azure Cosmos DB tootrust için uygulamanızın bağlantı.

İçinde Azure Portal Merhaba, tooyour Azure Cosmos DB hesap gidin ve ardından **anahtarları**.

Merhaba URI hello Portal'dan kopyalayın ve yapıştırın `<your endpoint URL>` hello program.cs dosyasındaki. BİRİNCİL anahtar hello portalından hello kopyalayıp yapıştırın sonra `<your primary key>`.

![Merhaba hello NoSQL Öğreticisi toocreate C# konsol uygulaması tarafından kullanılan Azure Portal ekran görüntüsü. Hesap, hello etkin hub vurgulandığı ile Merhaba hello Azure Cosmos DB hesabı dikey penceresinde ANAHTARLAR düğmesi ve anahtarlar dikey penceresinde hello üzerinde hello URI, birincil anahtar ve ikincil anahtar değerleri vurgulanmış bir Azure Cosmos DB gösterir][keys]

Ardından, Merhaba uygulaması hello yeni bir örneğini oluşturarak başlayacağız **DocumentClient**.

Merhaba aşağıda **ana** yöntemi adlı bu zaman uyumsuz yeni görevi ekleyin **GetStartedDemo**, örneğini oluşturacak, yeni **DocumentClient**.

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

Zaman uyumsuz görevinizi Hello aşağıdaki kod toorun eklemek, **ana** yöntemi. Merhaba **ana** yöntemi özel durumları yakalar ve bunları toohello konsol yazar.

    static void Main(string[] args)
    {
            // ADD THIS PART tooYOUR CODE
            try
            {
                    Program p = new Program();
                    p.GetStartedDemo().Wait();
            }
            catch (DocumentClientException de)
            {
                    Exception baseException = de.GetBaseException();
                    Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
            }
            catch (Exception e)
            {
                    Exception baseException = e.GetBaseException();
                    Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
            }
            finally
            {
                    Console.WriteLine("End of demo, press any key tooexit.");
                    Console.ReadKey();
            }

Tuşuna **F5** toorun uygulamanızı. Merhaba konsol penceresi çıktısı görüntüler selamlama iletisine `End of demo, press any key tooexit.` hello bağlantısı kuruldu onaylama.  Daha sonra hello konsol penceresi kapatabilirsiniz. 

Tebrikler! Başarılı bir şekilde bağlı tooan Azure Cosmos DB hesap, artık Azure Cosmos DB kaynaklarla çalışmak bir bakalım.  

## <a name="step-4-create-a-database"></a>4. Adım: Veritabanı oluşturma
Bir veritabanı oluşturmak için hello kodu eklemeden önce toohello konsol yazmak için bir yardımcı yöntemi ekleyin.

Kopyalama ve yapıştırma hello **WriteToConsoleAndPromptToContinue** yöntemi hello sonra **GetStartedDemo** yöntemi.

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

Azure Cosmos DB [veritabanı](documentdb-resources.md#databases) hello kullanarak oluşturulan [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) hello yöntemi **DocumentClient** sınıfı. Bir veritabanı hello mantıksal, koleksiyonlar genelinde bölümlenmiş JSON belgesi depolama kapsayıcısıdır.

Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello istemci oluşturulduktan sonra yöntemi. Bu, *FamilyDB* adlı bir veritabanı oluşturur.

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

Tuşuna **F5** toorun uygulamanızı.

Tebrikler! Başarılı bir şekilde bir Azure Cosmos DB veritabanı oluşturdunuz.  

## <a id="CreateColl"></a>5. Adım: Koleksiyon oluşturma
> [!WARNING]
> **CreateDocumentCollectionIfNotExistsAsync**, ayrılmış işleme ile yeni bir koleksiyon oluşturur, bu da ücret ödenmesini gerektirebilir. Daha ayrıntılı bilgi için lütfen [fiyatlandırma sayfamızı](https://azure.microsoft.com/pricing/details/cosmos-db/) ziyaret edin.
> 
> 

A [koleksiyonu](documentdb-resources.md#collections) hello kullanarak oluşturulan [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) hello yöntemi **DocumentClient** sınıfı. Koleksiyon, JSON belgelerinin ve ilişkili JavaScript uygulama mantığının bir kapsayıcısıdır.

Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello veritabanı oluşturulduktan sonra yöntemi. Bu, *FamilyCollection* adlı bir belge koleksiyonu oluşturur.

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

Tuşuna **F5** toorun uygulamanızı.

Tebrikler! Başarılı bir şekilde bir Azure Cosmos DB belge koleksiyonu oluşturdunuz.  

## <a id="CreateDoc"></a>6. Adım: JSON belgeleri oluşturma
A [belge](documentdb-resources.md#documents) hello kullanarak oluşturulan [Documentclient](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) hello yöntemi **DocumentClient** sınıfı. Belgeler, kullanıcı tanımlı (rastgele) JSON içeriğidir. Şimdi bir veya daha fazla belge ekleyebiliriz. İstediğiniz toostore veritabanınızda veriler zaten varsa, hello Azure Cosmos DB kullanabilirsiniz [veri geçiş aracı](import-data.md) tooimport hello verileri bir veritabanına.

İlk olarak, toocreate ihtiyacımız bir **ailesi** Bu örnekte Azure Cosmos DB içinde depolanan nesneleri temsil edecek sınıfı. **Family**'nin içinde kullanılan **Parent**, **Child**, **Pet**, **Address** alt sınıflarını da oluşturacağız. Belgelerin, JSON'da **id** olarak seri hale getirilmiş bir **Id** özelliğine sahip olmaları gerektiğini unutmayın. İç alt sınıfları hello sonra aşağıdaki hello ekleyerek bu sınıfları oluşturmak **GetStartedDemo** yöntemi.

Kopyalama ve yapıştırma hello **ailesi**, **üst**, **alt**, **evcil hayvan**, ve **adresi** hello sonra sınıfları **WriteToConsoleAndPromptToContinue** yöntemi.

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
    }

    // ADD THIS PART tooYOUR CODE
    public class Family
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        public string LastName { get; set; }
        public Parent[] Parents { get; set; }
        public Child[] Children { get; set; }
        public Address Address { get; set; }
        public bool IsRegistered { get; set; }
        public override string ToString()
        {
            return JsonConvert.SerializeObject(this);
        }
    }

    public class Parent
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
    }

    public class Child
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
        public string Gender { get; set; }
        public int Grade { get; set; }
        public Pet[] Pets { get; set; }
    }

    public class Pet
    {
        public string GivenName { get; set; }
    }

    public class Address
    {
        public string State { get; set; }
        public string County { get; set; }
        public string City { get; set; }
    }

Kopyalama ve yapıştırma hello **Createfamilydocumentıfnotexists** yöntemini, **adresi** sınıfı.

    // ADD THIS PART tooYOUR CODE
    private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
            this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
                this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
            }
            else
            {
                throw;
            }
        }
    }

Ve iki belge, her biri için hello Andersen ailesi ve Wakefield ailesi hello ekleme.

Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello belge koleksiyonu oluşturulduktan sonra yöntemi.

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART tooYOUR CODE
    Family andersenFamily = new Family
    {
            Id = "Andersen.1",
            LastName = "Andersen",
            Parents = new Parent[]
            {
                    new Parent { FirstName = "Thomas" },
                    new Parent { FirstName = "Mary Kay" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FirstName = "Henriette Thaulow",
                            Gender = "female",
                            Grade = 5,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Fluffy" }
                            }
                    }
            },
            Address = new Address { State = "WA", County = "King", City = "Seattle" },
            IsRegistered = true
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

    Family wakefieldFamily = new Family
    {
            Id = "Wakefield.7",
            LastName = "Wakefield",
            Parents = new Parent[]
            {
                    new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                    new Parent { FamilyName = "Miller", FirstName = "Ben" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FamilyName = "Merriam",
                            FirstName = "Jesse",
                            Gender = "female",
                            Grade = 8,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Goofy" },
                                    new Pet { GivenName = "Shadow" }
                            }
                    },
                    new Child
                    {
                            FamilyName = "Miller",
                            FirstName = "Lisa",
                            Gender = "female",
                            Grade = 1
                    }
            },
            Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
            IsRegistered = false
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

Tuşuna **F5** toorun uygulamanızı.

Tebrikler! Başarılı bir şekilde iki Azure Cosmos DB belgesi oluşturdunuz.  

![Gösteren hello hello hesabı, hello çevrimiçi veritabanı, hello koleksiyon arasındaki hiyerarşik ilişkiyi Diyagram ve C# konsol uygulaması hello NoSQL Öğreticisi toocreate tarafından kullanılan hello belgeler](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>7. Adım: Azure Cosmos DB kaynaklarını sorgulama
Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için [zengin sorguların](documentdb-sql-query.md) gerçekleştirilmesini destekler.  Merhaba aşağıdaki örnek kod çeşitli sorgularını gösterir - hem Azure Cosmos DB SQL kullanarak, sözdizimi ve bunun yanı sıra karşı çalıştırabilirsiniz LINQ - biz hello önceki adımda eklenen belgelerde hello.

Kopyalama ve yapıştırma hello **ExecuteSimpleQuery** sonra yöntemi, **Createfamilydocumentıfnotexists** yöntemi.

    // ADD THIS PART tooYOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find hello Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute hello same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello ikinci belge oluşturmanın sonra yöntemi.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Tuşuna **F5** toorun uygulamanızı.

Tebrikler! Bir Azure Cosmos DB koleksiyonunu başarıyla sorguladınız.

Merhaba Aşağıdaki diyagram hello Azure Cosmos DB SQL sorgusu söz dizimi karşı hello koleksiyonu olarak adlandırılır, nasıl oluşturulacağını gösterir ve hello aynı mantığı uygular de toohello LINQ sorgusu.

![Merhaba kapsamını ve hello sorgunun anlamını diyagramı bir C# konsol uygulaması hello NoSQL Öğreticisi toocreate tarafından kullanılan](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

Merhaba [FROM](documentdb-sql-query.md#FromClause) Azure Cosmos DB sorguları kapsamlı tooa tek koleksiyon zaten olduğu için anahtar sözcüğü hello sorguda isteğe bağlıdır. Bu nedenle, "FROM Families f", "FROM root r" veya seçtiğiniz herhangi bir başka değişken adıyla değiştirilebilir. Azure Cosmos DB aileleri, kök veya hello değişken adı, seçtiğiniz, başvuru hello geçerli koleksiyonu varsayılan olarak Infer.

## <a id="ReplaceDocument"></a>8. Adım: JSON belgesini değiştirme
Azure Cosmos DB, JSON belgelerini değiştirmeyi destekler.  

Kopyalama ve yapıştırma hello **ReplaceFamilyDocument** sonra yöntemi, **ExecuteSimpleQuery** yöntemi.

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello yöntemi hello sonunda hello sorgu yürütme sonrasında yöntemi. Merhaba belgeyi değiştirdikten sonra bu hello çalıştıracaktır aynı tooview değiştirilen hello belgeyi yeniden sorgula.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Tuşuna **F5** toorun uygulamanızı.

Tebrikler! Başarılı bir şekilde bir Azure Cosmos DB belgesini değiştirdiniz.

## <a id="DeleteDocument"></a>9. Adım: JSON belgesini silme
Azure Cosmos DB, JSON belgelerini silmeyi destekler.  

Kopyalama ve yapıştırma hello **DeleteFamilyDocument** sonra yöntemi, **ReplaceFamilyDocument** yöntemi.

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello ikinci sorguyu yürütmenin, hello yöntemi hello sonunda sonra yöntemi.

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

Tuşuna **F5** toorun uygulamanızı.

Tebrikler! Başarılı bir şekilde bir Azure Cosmos DB belgesini sildiniz.

## <a id="DeleteDatabase"></a>10. adım: hello veritabanını silme
Veritabanı oluşturulan silme hello hello veritabanı ve tüm alt kaynaklar (koleksiyonlar, belgeler, vb.) kaldırır.

Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** yöntemini hello belge sonra toodelete hello tüm veritabanını ve tüm alt kaynaklarını silin.

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

Tuşuna **F5** toorun uygulamanızı.

Tebrikler! Başarılı bir şekilde bir Azure Cosmos DB veritabanını sildiniz.

## <a id="Run"></a>11. Adım: C# konsol uygulamanızı hep birlikte çalıştırın!
Visual Studio toobuild hello uygulamasında hata ayıklama modunda F5'e basın.

Başlarken uygulamanızın bir konsol penceresinde hello çıktısını görmeniz gerekir. Merhaba çıktı hello hello sonuçlarını gösterir eklenir ve hello örnek metinle eşleşmelidir sorgular.

    Created FamilyDB
    Press any key toocontinue ...
    Created FamilyCollection
    Press any key toocontinue ...
    Created Family Andersen.1
    Press any key toocontinue ...
    Created Family Wakefield.7
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key tooexit.

Tebrikler! Merhaba öğreticisini tamamladınız ve çalışma C# konsol uygulaması sahip!

## <a id="GetSolution"></a>Merhaba tam Öğreticisi çözümünü edinme
Toocomplete hello adımları Bu öğreticinin veya yalnızca istediğiniz toodownload hello kod örnekleri saati yoksa alamadık, buradan edinebilirsiniz [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). 

toobuild hello GetStarted çözümünü hello aşağıdaki gerekir:

* Etkin bir Azure hesabı. Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.
* Bir [Azure Cosmos DB hesabı][cosmos-db-create-account].
* Merhaba [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) çözüm Github'da kullanılabilir.

toorestore hello başvuruları toohello Azure Cosmos DB .NET SDK Visual Studio'da sağ hello **GetStarted** Çözüm Gezgini ve ardından çözüm **NuGet paketi geri yüklemeyi etkinleştir**. Ardından, hello App.config dosyasında açıklandığı gibi hello EndpointUrl ve AuthorizationKey değerlerini güncelleştirin [tooan Azure Cosmos DB hesabını bağlaması](#Connect).

Hepsi bu kadar, derleyin ve devam edin!


## <a name="next-steps"></a>Sonraki adımlar
* Daha karmaşık bir ASP.NET MVC öğreticisi mi istiyorsunuz? Bkz: [ASP.NET MVC Öğreticisi: Web uygulaması geliştirme Azure Cosmos DB ile](documentdb-dotnet-application.md).
* Tooperform ölçek ve performans ile Azure Cosmos DB istiyorsunuz? Bkz: [performansı ve ölçeği Azure Cosmos DB ile test etme](performance-testing.md)
* Nasıl çok öğrenin[Azure Cosmos DB istekleri, kullanım ve depolama izleme](monitor-accounts.md).
* Merhaba, örnek veri kümelerimizde sorgular çalıştırın [Query Playground](https://www.documentdb.com/sql/demo).
* toolearn Azure Cosmos DB hakkında daha fazla bilgi görmek [tooAzure Cosmos DB Hoş Geldiniz](https://docs.microsoft.com/azure/cosmos-db/introduction).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
