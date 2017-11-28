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
# <a name="azure-cosmos-db-build-a-net-application-using-hello-table-api"></a><span data-ttu-id="16939-103">Azure Cosmos DB: hello tablo API kullanarak bir .NET uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="16939-103">Azure Cosmos DB: Build a .NET application using hello Table API</span></span>

<span data-ttu-id="16939-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="16939-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="16939-105">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16939-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="16939-106">Bu hızlı başlangıç gösteren nasıl toocreate bir Azure Cosmos DB hesap ve hello Azure portal kullanarak bu hesap içinde bir tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="16939-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, and create a table within that account using hello Azure portal.</span></span> <span data-ttu-id="16939-107">Ardından kod tooinsert, güncelleştirme ve silme varlıkları yazma ve hello kullanarak yeni bazı sorgular çalıştırın [Windows Azure depolama Premium tablosu](https://aka.ms/premiumtablenuget) NuGet paketinden (Önizleme).</span><span class="sxs-lookup"><span data-stu-id="16939-107">You'll then write code tooinsert, update, and delete entities, and run some queries using hello new [Windows Azure Storage Premium Table](https://aka.ms/premiumtablenuget) (preview) package from NuGet.</span></span> <span data-ttu-id="16939-108">Bu kitaplık hello sahip aynı sınıfları ve yöntem imzaları hello genel olarak [Windows Azure depolama SDK](https://www.nuget.org/packages/WindowsAzure.Storage), ancak aynı zamanda hello kullanarak hello özelliği tooconnect tooAzure Cosmos DB hesaplarına sahip [tablo API](table-introduction.md) (Önizleme).</span><span class="sxs-lookup"><span data-stu-id="16939-108">This library has hello same classes and method signatures as hello public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has hello ability tooconnect tooAzure Cosmos DB accounts using hello [Table API](table-introduction.md) (preview).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="16939-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="16939-109">Prerequisites</span></span>

<span data-ttu-id="16939-110">Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve hello kullan **ücretsiz** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="16939-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="16939-111">Etkinleştirdiğinizden emin olun **Azure geliştirme** hello Visual Studio Kurulumu sırasında.</span><span class="sxs-lookup"><span data-stu-id="16939-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="16939-112">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="16939-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="16939-113">Tablo ekleme</span><span class="sxs-lookup"><span data-stu-id="16939-113">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="16939-114">Örnek verileri ekleme</span><span class="sxs-lookup"><span data-stu-id="16939-114">Add sample data</span></span>

<span data-ttu-id="16939-115">Veri Gezgini (Önizleme) kullanarak veri tooyour yeni tablosu artık ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16939-115">You can now add data tooyour new table using Data Explorer (Preview).</span></span>

1. <span data-ttu-id="16939-116">Veri Gezgini'nde **sample-table** seçeneğini genişletin, **Varlıklar**'a ve ardından **Varlık Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="16939-116">In Data Explorer, expand **sample-table**, click **Entities**, and then click **Add Entity**.</span></span>

   ![Yeni varlıklar veri Gezgini'nde hello Azure portal oluşturun.](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. <span data-ttu-id="16939-118">Şimdi veri toohello PartitionKey değeri ve RowKey değeri kutularının ekleyin ve **varlık Ekle**.</span><span class="sxs-lookup"><span data-stu-id="16939-118">Now add data toohello PartitionKey value box and RowKey value box, and click **Add Entity**.</span></span>

   ![Ayarlama bölüm anahtarı ve yeni bir varlık için satır anahtarını hello](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    <span data-ttu-id="16939-120">Artık daha fazla varlık tooyour tablo eklemek, varlıklarınızı düzenleme veya verilerinizi Veri Gezgini sorgu.</span><span class="sxs-lookup"><span data-stu-id="16939-120">You can now add more entities tooyour table, edit your entities, or query your data in Data Explorer.</span></span> <span data-ttu-id="16939-121">Veri Gezgini Ayrıca, üretilen iş ölçekleme ve saklı yordamlar, kullanıcı tanımlı işlevler ve Tetikleyicileri tooyour tabloyu eklemek yerdir.</span><span class="sxs-lookup"><span data-stu-id="16939-121">Data Explorer is also where you can scale your throughput and add stored procedures, user defined functions, and triggers tooyour table.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="16939-122">Merhaba örnek uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="16939-122">Clone hello sample application</span></span>

<span data-ttu-id="16939-123">Şimdi şimdi kopyalama tablo uygulama github'dan hello bağlantı dizesini ayarlamak ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="16939-123">Now let's clone a Table app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="16939-124">Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="16939-124">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="16939-125">Git bash gibi bir git terminal penceresi açın ve `cd` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="16939-125">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="16939-126">Çalışma hello aşağıdaki tooclone hello örnek depo komutu.</span><span class="sxs-lookup"><span data-stu-id="16939-126">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. <span data-ttu-id="16939-127">Ardından Visual Studio'da hello çözüm dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="16939-127">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="16939-128">Merhaba kod gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="16939-128">Review hello code</span></span>

<span data-ttu-id="16939-129">Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım.</span><span class="sxs-lookup"><span data-stu-id="16939-129">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="16939-130">Bu kod satırları hello Azure Cosmos DB kaynakları oluşturun, açık hello Program.cs dosyasının ve bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16939-130">Open hello Program.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="16939-131">Merhaba CloudTableClient başlatılır.</span><span class="sxs-lookup"><span data-stu-id="16939-131">hello CloudTableClient is initialized.</span></span>

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* <span data-ttu-id="16939-132">Henüz yoksa yeni bir tablo oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="16939-132">A new table is created if it does not exist.</span></span>

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* <span data-ttu-id="16939-133">Yeni bir Tablo kapsayıcısı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="16939-133">A new Table container is created.</span></span> <span data-ttu-id="16939-134">Bu kod çok benzer tooregular Azure Table depolama SDK'sı fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="16939-134">You will notice this code very similar tooregular Azure Table storage SDK.</span></span> 

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

## <a name="update-your-connection-string"></a><span data-ttu-id="16939-135">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="16939-135">Update your connection string</span></span>

<span data-ttu-id="16939-136">Artık uygulamanızı tooAzure Cosmos DB iletişim kurabilirsiniz böylece biz hello bağlantı dizesi bilgilerini güncelleştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="16939-136">Now we'll update hello connection string information so your app can talk tooAzure Cosmos DB.</span></span> 

1. <span data-ttu-id="16939-137">Visual Studio'da hello app.config dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="16939-137">In Visual Studio, open hello app.config file.</span></span> 

2. <span data-ttu-id="16939-138">Merhaba, [Azure portal](http://portal.azure.com/)hello Azure Cosmos DB Gezinti Menüsü sol, tıklatın **bağlantı dizesi**.</span><span class="sxs-lookup"><span data-stu-id="16939-138">In hello [Azure portal](http://portal.azure.com/), in hello Azure Cosmos DB left navigation menu, click **Connection String**.</span></span> <span data-ttu-id="16939-139">Ardından yeni hello Bölmesi'nde hello bağlantı dizesi için hello Kopyala düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="16939-139">Then in hello new pane click hello copy button for hello connection string.</span></span> 

    ![Görüntüleme ve hello bağlantı dizesi Bölmesi'nde hello uç noktasını ve hesap anahtarını kopyalama](./media/create-table-dotnet/keys.png)

3. <span data-ttu-id="16939-141">Merhaba değeri hello PremiumStorageConnectionString hello değeri olarak hello app.config dosyasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="16939-141">Paste hello value into hello app.config file as hello value of hello PremiumStorageConnectionString.</span></span> 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    <span data-ttu-id="16939-142">Merhaba StandardStorageConnectionString olduğu gibi bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16939-142">You can leave hello StandardStorageConnectionString as is.</span></span>

<span data-ttu-id="16939-143">Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="16939-143">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="run-hello-web-app"></a><span data-ttu-id="16939-144">Merhaba web uygulaması çalıştırın</span><span class="sxs-lookup"><span data-stu-id="16939-144">Run hello web app</span></span>

1. <span data-ttu-id="16939-145">Visual Studio'da hello üzerinde sağ **PremiumTableGetStarted** proje **Çözüm Gezgini** ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="16939-145">In Visual Studio, right-click on hello **PremiumTableGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="16939-146">Merhaba NuGet içinde **Gözat** kutusuna *WindowsAzure.Storage PremiumTable*.</span><span class="sxs-lookup"><span data-stu-id="16939-146">In hello NuGet **Browse** box, type *WindowsAzure.Storage-PremiumTable*.</span></span>

3. <span data-ttu-id="16939-147">Merhaba denetleyin **dahil et** kutusu.</span><span class="sxs-lookup"><span data-stu-id="16939-147">Check hello **Include prerelease** box.</span></span> 

4. <span data-ttu-id="16939-148">Merhaba sonuçlarından hello yüklemek **WindowsAzure.Storage PremiumTable** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="16939-148">From hello results, install hello **WindowsAzure.Storage-PremiumTable** library.</span></span> <span data-ttu-id="16939-149">Bu, tüm bağımlılıkları yanı sıra hello Önizleme Azure Cosmos DB tablo API paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="16939-149">This installs hello preview Azure Cosmos DB Table API package as well as all dependencies.</span></span> <span data-ttu-id="16939-150">Bu Azure Table Depolama tarafından kullanılan hello Windows Azure depolama paket daha farklı bir NuGet paketi olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="16939-150">Note that this is a different NuGet package than hello Windows Azure Storage package used by Azure Table storage.</span></span> 

5. <span data-ttu-id="16939-151">CTRL + F5'e tıklayın toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="16939-151">Click CTRL + F5 toorun hello application.</span></span>

    <span data-ttu-id="16939-152">Merhaba konsol penceresi eklenmesini, alınan, sorgulanan, değiştirilen ve hello tablosundan silinen hello verilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="16939-152">hello console window displays hello data being added, retrieved, queried, replaced and deleted from hello table.</span></span> <span data-ttu-id="16939-153">Merhaba betik tamamlandığında, herhangi bir anahtar tooclose hello konsol penceresi tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="16939-153">When hello script completes, press any key tooclose hello console window.</span></span> 
    
    ![Merhaba quickstart konsol çıktısı](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. <span data-ttu-id="16939-155">Veri Gezgini'nde, bunlar silinmez şekilde program.cs 188 208 satırlarında çıkışı yalnızca açıklama toosee hello yeni varlıklar istiyorsanız hello örnek yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="16939-155">If you want toosee hello new entities in Data Explorer, just comment out lines 188-208 in program.cs so they aren't deleted, then run hello sample again.</span></span> 

    <span data-ttu-id="16939-156">Şimdi tooData Gezgini geri dönebilirsiniz tıklatın **yenileme**, hello genişletin **kişiler** tablosu ve'ı tıklatın **varlıklar**ve ardından bu yeni verilerle çalışmak.</span><span class="sxs-lookup"><span data-stu-id="16939-156">You can now go back tooData Explorer, click **Refresh**, expand hello **people** table and click **Entities**, and then work with this new data.</span></span> 

    ![Veri Gezgini'ndeki yeni varlıklar](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="16939-158">Gözden geçirme SLA'hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="16939-158">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="16939-159">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="16939-159">Clean up resources</span></span>

<span data-ttu-id="16939-160">Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="16939-160">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="16939-161">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="16939-161">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="16939-162">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="16939-162">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16939-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="16939-163">Next steps</span></span>

<span data-ttu-id="16939-164">Bu hızlı başlangıç toocreate bir Azure Cosmos DB hesap hello Veri Gezgini'ni kullanarak bir tablo oluşturma ve bir uygulama çalıştırmasına öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="16939-164">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a table using hello Data Explorer, and run an app.</span></span>  <span data-ttu-id="16939-165">Şimdi verilerinizi hello tablo API kullanarak sorgulama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16939-165">Now you can query your data using hello Table API.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="16939-166">Merhaba tablo API kullanarak sorgu</span><span class="sxs-lookup"><span data-stu-id="16939-166">Query using hello Table API</span></span>](tutorial-query-table.md)

