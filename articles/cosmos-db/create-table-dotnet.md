---
title: "bir Azure Cosmos DB .NET uygulaması kullanarak aaaBuild hello tablo API | Microsoft Docs"
description: ".NET kullanarak Azure Cosmos DB'nin Tablo API’si ile çalışmaya başlama"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 66327041-4d5e-4ce6-a394-fee107c18e59
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/22/2017
ms.author: arramac
ms.openlocfilehash: bdd4f8ec45407962b3d2cb26aa814a20cfc62173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-table-api"></a>Azure Cosmos DB: hello tablo API kullanarak bir .NET uygulaması oluşturma

Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz. 

Bu hızlı başlangıç gösteren nasıl toocreate bir Azure Cosmos DB hesap ve hello Azure portal kullanarak bu hesap içinde bir tablo oluşturun. Ardından kod tooinsert, güncelleştirme ve silme varlıkları yazma ve hello kullanarak yeni bazı sorgular çalıştırın [Windows Azure depolama Premium tablosu](https://aka.ms/premiumtablenuget) NuGet paketinden (Önizleme). Bu kitaplık hello sahip aynı sınıfları ve yöntem imzaları hello genel olarak [Windows Azure depolama SDK](https://www.nuget.org/packages/WindowsAzure.Storage), ancak aynı zamanda hello kullanarak hello özelliği tooconnect tooAzure Cosmos DB hesaplarına sahip [tablo API](table-introduction.md) (Önizleme). 

## <a name="prerequisites"></a>Ön koşullar

Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve hello kullan **ücretsiz** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Etkinleştirdiğinizden emin olun **Azure geliştirme** hello Visual Studio Kurulumu sırasında.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Veritabanı hesabı oluşturma

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a>Tablo ekleme

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a>Örnek verileri ekleme

Veri Gezgini (Önizleme) kullanarak veri tooyour yeni tablosu artık ekleyebilirsiniz.

1. Veri Gezgini'nde **sample-table** seçeneğini genişletin, **Varlıklar**'a ve ardından **Varlık Ekle**'ye tıklayın.

   ![Yeni varlıklar veri Gezgini'nde hello Azure portal oluşturun.](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. Şimdi veri toohello PartitionKey değeri ve RowKey değeri kutularının ekleyin ve **varlık Ekle**.

   ![Ayarlama bölüm anahtarı ve yeni bir varlık için satır anahtarını hello](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    Artık daha fazla varlık tooyour tablo eklemek, varlıklarınızı düzenleme veya verilerinizi Veri Gezgini sorgu. Veri Gezgini Ayrıca, üretilen iş ölçekleme ve saklı yordamlar, kullanıcı tanımlı işlevler ve Tetikleyicileri tooyour tabloyu eklemek yerdir.

## <a name="clone-hello-sample-application"></a>Merhaba örnek uygulaması kopyalama

Şimdi şimdi kopyalama tablo uygulama github'dan hello bağlantı dizesini ayarlamak ve çalıştırın. Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz. 

1. Git bash gibi bir git terminal penceresi açın ve `cd` tooa çalışma dizini.  

2. Çalışma hello aşağıdaki tooclone hello örnek depo komutu. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. Ardından Visual Studio'da hello çözüm dosyasını açın. 

## <a name="review-hello-code"></a>Merhaba kod gözden geçirme

Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım. Bu kod satırları hello Azure Cosmos DB kaynakları oluşturun, açık hello Program.cs dosyasının ve bulabilirsiniz. 

* Merhaba CloudTableClient başlatılır.

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* Henüz yoksa yeni bir tablo oluşturulur.

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* Yeni bir Tablo kapsayıcısı oluşturulur. Bu kod çok benzer tooregular Azure Table depolama SDK'sı fark edeceksiniz. 

    ```csharp
    CustomerEntity item = new CustomerEntity()
                {
                    PartitionKey = Guid.NewGuid().ToString(),
                    RowKey = Guid.NewGuid().ToString(),
                    Email = $"{GetRandomString(6)}@contoso.com",
                    PhoneNumber = "425-555-0102",
                    Bio = GetRandomString(1000)
                };
    ```

## <a name="update-your-connection-string"></a>Bağlantı dizenizi güncelleştirme

Artık uygulamanızı tooAzure Cosmos DB iletişim kurabilirsiniz böylece biz hello bağlantı dizesi bilgilerini güncelleştireceksiniz. 

1. Visual Studio'da hello app.config dosyasını açın. 

2. Merhaba, [Azure portal](http://portal.azure.com/)hello Azure Cosmos DB Gezinti Menüsü sol, tıklatın **bağlantı dizesi**. Ardından yeni hello Bölmesi'nde hello bağlantı dizesi için hello Kopyala düğmesini tıklatın. 

    ![Görüntüleme ve hello bağlantı dizesi Bölmesi'nde hello uç noktasını ve hesap anahtarını kopyalama](./media/create-table-dotnet/keys.png)

3. Merhaba değeri hello PremiumStorageConnectionString hello değeri olarak hello app.config dosyasına yapıştırın. 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    Merhaba StandardStorageConnectionString olduğu gibi bırakabilirsiniz.

Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip. 

## <a name="run-hello-web-app"></a>Merhaba web uygulaması çalıştırın

1. Visual Studio'da hello üzerinde sağ **PremiumTableGetStarted** proje **Çözüm Gezgini** ve ardından **NuGet paketlerini Yönet**. 

2. Merhaba NuGet içinde **Gözat** kutusuna *WindowsAzure.Storage PremiumTable*.

3. Merhaba denetleyin **dahil et** kutusu. 

4. Merhaba sonuçlarından hello yüklemek **WindowsAzure.Storage PremiumTable** kitaplığı. Bu, tüm bağımlılıkları yanı sıra hello Önizleme Azure Cosmos DB tablo API paketi yükler. Bu Azure Table Depolama tarafından kullanılan hello Windows Azure depolama paket daha farklı bir NuGet paketi olduğuna dikkat edin. 

5. CTRL + F5'e tıklayın toorun Merhaba uygulaması.

    Merhaba konsol penceresi eklenmesini, alınan, sorgulanan, değiştirilen ve hello tablosundan silinen hello verilerini görüntüler. Merhaba betik tamamlandığında, herhangi bir anahtar tooclose hello konsol penceresi tuşuna basın. 
    
    ![Merhaba quickstart konsol çıktısı](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. Veri Gezgini'nde, bunlar silinmez şekilde program.cs 188 208 satırlarında çıkışı yalnızca açıklama toosee hello yeni varlıklar istiyorsanız hello örnek yeniden çalıştırın. 

    Şimdi tooData Gezgini geri dönebilirsiniz tıklatın **yenileme**, hello genişletin **kişiler** tablosu ve'ı tıklatın **varlıklar**ve ardından bu yeni verilerle çalışmak. 

    ![Veri Gezgini'ndeki yeni varlıklar](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a>Gözden geçirme SLA'hello Azure portalı

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Kaynakları temizleme

Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin: 

1. Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın. 
2. Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıç toocreate bir Azure Cosmos DB hesap hello Veri Gezgini'ni kullanarak bir tablo oluşturma ve bir uygulama çalıştırmasına öğrendiniz.  Şimdi verilerinizi hello tablo API kullanarak sorgulama yapabilirsiniz.  

> [!div class="nextstepaction"]
> [Merhaba tablo API kullanarak sorgu](tutorial-query-table.md)

