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
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="fa111-104">Azure Cosmos DB: DocumentDB API başlangıç öğreticisi</span><span class="sxs-lookup"><span data-stu-id="fa111-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa111-105">.NET</span><span class="sxs-lookup"><span data-stu-id="fa111-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="fa111-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="fa111-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="fa111-107">MongoDB için Node.js</span><span class="sxs-lookup"><span data-stu-id="fa111-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="fa111-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="fa111-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="fa111-109">Java</span><span class="sxs-lookup"><span data-stu-id="fa111-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="fa111-110">C++</span><span class="sxs-lookup"><span data-stu-id="fa111-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="fa111-111">Hoş Geldiniz toohello Azure Cosmos DB DocumentDB API başlangıç Öğreticisi!</span><span class="sxs-lookup"><span data-stu-id="fa111-111">Welcome toohello Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="fa111-112">Bu öğreticiyi uyguladıktan sonra, Azure Cosmos DB kaynaklarını oluşturan ve sorgulayan bir konsol uygulamasına sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fa111-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="fa111-113">Şu konulara değineceğiz:</span><span class="sxs-lookup"><span data-stu-id="fa111-113">We'll cover:</span></span>

* <span data-ttu-id="fa111-114">Oluşturma ve tooan Azure Cosmos DB hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="fa111-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="fa111-115">Visual Studio Çözümünüzü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fa111-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="fa111-116">Çevrimiçi bir veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa111-116">Creating an online database</span></span>
* <span data-ttu-id="fa111-117">Koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa111-117">Creating a collection</span></span>
* <span data-ttu-id="fa111-118">JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa111-118">Creating JSON documents</span></span>
* <span data-ttu-id="fa111-119">Merhaba koleksiyonu sorgulama</span><span class="sxs-lookup"><span data-stu-id="fa111-119">Querying hello collection</span></span>
* <span data-ttu-id="fa111-120">Bir belgeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="fa111-120">Replacing a document</span></span>
* <span data-ttu-id="fa111-121">Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="fa111-121">Deleting a document</span></span>
* <span data-ttu-id="fa111-122">Merhaba veritabanını silme</span><span class="sxs-lookup"><span data-stu-id="fa111-122">Deleting hello database</span></span>

<span data-ttu-id="fa111-123">Zamanınız yok mu?</span><span class="sxs-lookup"><span data-stu-id="fa111-123">Don't have time?</span></span> <span data-ttu-id="fa111-124">Endişelenmeyin!</span><span class="sxs-lookup"><span data-stu-id="fa111-124">Don't worry!</span></span> <span data-ttu-id="fa111-125">Merhaba eksiksiz bir çözüm edinilebilir [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="fa111-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="fa111-126">Toohello atlama [hello tam NoSQL Öğreticisi çözümü edinme bölümüne](#GetSolution) hızlı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="fa111-126">Jump toohello [Get hello complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="fa111-127">Daha sonra lütfen hello kullan oylama hello üstüne veya altına bu sayfa toogive, bize geri bildirim düğmeler.</span><span class="sxs-lookup"><span data-stu-id="fa111-127">Afterwards, please use hello voting buttons at hello top or bottom of this page toogive us feedback.</span></span> <span data-ttu-id="fa111-128">Bize istiyorsanız toocontact doğrudan düşündüğünüz e-posta adresi serbest tooinclude yorumlarınızı içinde.</span><span class="sxs-lookup"><span data-stu-id="fa111-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="fa111-129">Şimdi başlayalım!</span><span class="sxs-lookup"><span data-stu-id="fa111-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa111-130">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fa111-130">Prerequisites</span></span>
<span data-ttu-id="fa111-131">Merhaba aşağıdaki sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="fa111-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="fa111-132">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="fa111-132">An active Azure account.</span></span> <span data-ttu-id="fa111-133">Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa111-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="fa111-134">Alternatif olarak, hello kullanabilirsiniz [Azure Cosmos DB öykünücüsü](local-emulator.md) Bu öğretici için.</span><span class="sxs-lookup"><span data-stu-id="fa111-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="fa111-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="fa111-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="fa111-136">1. Adım: Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa111-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="fa111-137">Bir Azure Cosmos DB hesabı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="fa111-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="fa111-138">Toouse istediğiniz bir hesap zaten varsa, şimdi çok atlayabilirsiniz[Visual Studio çözümünüzü kurma](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="fa111-138">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="fa111-139">Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) toosetup öykünücüsü hello ve İleri çok atlayabilirsiniz[Visual Studio çözümünüzü kurma](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="fa111-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="fa111-140"><a id="SetupVS"></a>2. Adım: Visual Studio çözümünüzü kurma</span><span class="sxs-lookup"><span data-stu-id="fa111-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="fa111-141">Bilgisayarınızda **Visual Studio 2017**'yi açın.</span><span class="sxs-lookup"><span data-stu-id="fa111-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="fa111-142">Merhaba üzerinde **dosya** menüsünde, select **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="fa111-142">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="fa111-143">Merhaba, **yeni proje** iletişim kutusunda **şablonları** / **Visual C#** / **konsol uygulaması**, adı Proje ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fa111-143">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="fa111-144">![Merhaba yeni proje penceresinin ekran görüntüsü](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="fa111-144">![Screen shot of hello New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="fa111-145">Merhaba, **Çözüm Gezgini**, Visual Studio çözümünüzün yeni konsol uygulamanızın üzerinde sağ tıklayın ve ardından **NuGet paketlerini Yönet...**</span><span class="sxs-lookup"><span data-stu-id="fa111-145">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Merhaba sağ tıklama menüsünün hello proje için ekran görüntüsü](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="fa111-147">Merhaba, **Nuget** sekmesini tıklatın, **Gözat**ve türü **azure documentdb** hello arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="fa111-147">In hello **Nuget** tab, click **Browse**, and type **azure documentdb** in hello search box.</span></span>
6. <span data-ttu-id="fa111-148">Merhaba sonuçları içinde bulmak **Microsoft.Azure.DocumentDB** tıklatıp **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="fa111-148">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="fa111-149">Merhaba hello Azure Cosmos DB DocumentDB API'si istemci kitaplığı için paket kimliği [Microsoft Azure DocumentDB istemci Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="fa111-149">hello package ID for hello Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="fa111-150">![Azure Cosmos DB istemci SDK'sını bulmak için Nuget menüsünün hello ekran görüntüsü](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="fa111-150">![Screen shot of hello Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="fa111-151">Değişiklikleri toohello çözümü gözden geçirme hakkında bir ileti alırsanız tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fa111-151">If you get a messages about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="fa111-152">Lisans kabulü hakkında bir ileti alırsanız **Kabul ediyorum**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fa111-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="fa111-153">Harika!</span><span class="sxs-lookup"><span data-stu-id="fa111-153">Great!</span></span> <span data-ttu-id="fa111-154">Biz hello Kurulumu tamamladığımıza göre biraz kod yazmaya başlayalım.</span><span class="sxs-lookup"><span data-stu-id="fa111-154">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="fa111-155">Bu öğreticinin tamamlanmış kod projesini [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs)'da bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa111-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="fa111-156"><a id="Connect"></a>3. adım: tooan Azure Cosmos DB hesap bağlanma</span><span class="sxs-lookup"><span data-stu-id="fa111-156"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="fa111-157">İlk olarak, bunlar ekleyin başvuran C# uygulamanız, hello Program.cs dosyasındaki toohello başlangıcı:</span><span class="sxs-lookup"><span data-stu-id="fa111-157">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="fa111-158">Sipariş toocomplete hello öğreticide hello yukarıdaki bağımlılıkları eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="fa111-158">In order toocomplete hello tutorial, make sure you add hello dependencies above.</span></span>
> 
> 

<span data-ttu-id="fa111-159">Şimdi bu iki sabiti ve *client* değişkeninizi *Program* ortak sınıfının altına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa111-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="fa111-160">Ardından, head geri toohello [Azure Portal](https://portal.azure.com) tooretrieve uç noktasının URL'sini ve birincil anahtar.</span><span class="sxs-lookup"><span data-stu-id="fa111-160">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="fa111-161">Merhaba uç noktasının URL'sini ve birincil anahtar, uygulama toounderstand için gerekli olan nerede tooconnect ve Azure Cosmos DB tootrust için uygulamanızın bağlantı.</span><span class="sxs-lookup"><span data-stu-id="fa111-161">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="fa111-162">İçinde Azure Portal Merhaba, tooyour Azure Cosmos DB hesap gidin ve ardından **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="fa111-162">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="fa111-163">Merhaba URI hello Portal'dan kopyalayın ve yapıştırın `<your endpoint URL>` hello program.cs dosyasındaki.</span><span class="sxs-lookup"><span data-stu-id="fa111-163">Copy hello URI from hello portal and paste it into `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="fa111-164">BİRİNCİL anahtar hello portalından hello kopyalayıp yapıştırın sonra `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="fa111-164">Then copy hello PRIMARY KEY from hello portal and paste it into `<your primary key>`.</span></span>

![Merhaba hello NoSQL Öğreticisi toocreate C# konsol uygulaması tarafından kullanılan Azure Portal ekran görüntüsü.][keys]

<span data-ttu-id="fa111-167">Ardından, Merhaba uygulaması hello yeni bir örneğini oluşturarak başlayacağız **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="fa111-167">Next, we'll start hello application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="fa111-168">Merhaba aşağıda **ana** yöntemi adlı bu zaman uyumsuz yeni görevi ekleyin **GetStartedDemo**, örneğini oluşturacak, yeni **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="fa111-168">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="fa111-169">Zaman uyumsuz görevinizi Hello aşağıdaki kod toorun eklemek, **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fa111-169">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="fa111-170">Merhaba **ana** yöntemi özel durumları yakalar ve bunları toohello konsol yazar.</span><span class="sxs-lookup"><span data-stu-id="fa111-170">hello **Main** method will catch exceptions and write them toohello console.</span></span>

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

<span data-ttu-id="fa111-171">Tuşuna **F5** toorun uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="fa111-171">Press **F5** toorun your application.</span></span> <span data-ttu-id="fa111-172">Merhaba konsol penceresi çıktısı görüntüler selamlama iletisine `End of demo, press any key tooexit.` hello bağlantısı kuruldu onaylama.</span><span class="sxs-lookup"><span data-stu-id="fa111-172">hello console window output displays hello message `End of demo, press any key tooexit.` confirming that hello connection was made.</span></span>  <span data-ttu-id="fa111-173">Daha sonra hello konsol penceresi kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa111-173">You can then close hello console window.</span></span> 

<span data-ttu-id="fa111-174">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="fa111-174">Congratulations!</span></span> <span data-ttu-id="fa111-175">Başarılı bir şekilde bağlı tooan Azure Cosmos DB hesap, artık Azure Cosmos DB kaynaklarla çalışmak bir bakalım.</span><span class="sxs-lookup"><span data-stu-id="fa111-175">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="fa111-176">4. Adım: Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa111-176">Step 4: Create a database</span></span>
<span data-ttu-id="fa111-177">Bir veritabanı oluşturmak için hello kodu eklemeden önce toohello konsol yazmak için bir yardımcı yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fa111-177">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="fa111-178">Kopyalama ve yapıştırma hello **WriteToConsoleAndPromptToContinue** yöntemi hello sonra **GetStartedDemo** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fa111-178">Copy and paste hello **WriteToConsoleAndPromptToContinue** method after hello **GetStartedDemo** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

<span data-ttu-id="fa111-179">Azure Cosmos DB [veritabanı](documentdb-resources.md#databases) hello kullanarak oluşturulan [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) hello yöntemi **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fa111-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="fa111-180">Bir veritabanı hello mantıksal, koleksiyonlar genelinde bölümlenmiş JSON belgesi depolama kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="fa111-180">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="fa111-181">Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello istemci oluşturulduktan sonra yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fa111-181">Copy and paste hello following code tooyour **GetStartedDemo** method after hello client creation.</span></span> <span data-ttu-id="fa111-182">Bu, *FamilyDB* adlı bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fa111-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="fa111-183">Tuşuna **F5** toorun uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="fa111-183">Press **F5** toorun your application.</span></span>

<span data-ttu-id="fa111-184">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="fa111-184">Congratulations!</span></span> <span data-ttu-id="fa111-185">Başarılı bir şekilde bir Azure Cosmos DB veritabanı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="fa111-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="fa111-186"><a id="CreateColl"></a>5. Adım: Koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa111-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="fa111-187">**CreateDocumentCollectionIfNotExistsAsync**, ayrılmış işleme ile yeni bir koleksiyon oluşturur, bu da ücret ödenmesini gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="fa111-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="fa111-188">Daha ayrıntılı bilgi için lütfen [fiyatlandırma sayfamızı](https://azure.microsoft.com/pricing/details/cosmos-db/) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="fa111-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="fa111-189">A [koleksiyonu](documentdb-resources.md#collections) hello kullanarak oluşturulan [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) hello yöntemi **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fa111-189">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="fa111-190">Koleksiyon, JSON belgelerinin ve ilişkili JavaScript uygulama mantığının bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="fa111-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="fa111-191">Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello veritabanı oluşturulduktan sonra yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fa111-191">Copy and paste hello following code tooyour **GetStartedDemo** method after hello database creation.</span></span> <span data-ttu-id="fa111-192">Bu, *FamilyCollection* adlı bir belge koleksiyonu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fa111-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="fa111-193">Tuşuna **F5** toorun uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="fa111-193">Press **F5** toorun your application.</span></span>

<span data-ttu-id="fa111-194">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="fa111-194">Congratulations!</span></span> <span data-ttu-id="fa111-195">Başarılı bir şekilde bir Azure Cosmos DB belge koleksiyonu oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="fa111-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="fa111-196"><a id="CreateDoc"></a>6. Adım: JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa111-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="fa111-197">A [belge](documentdb-resources.md#documents) hello kullanarak oluşturulan [Documentclient](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) hello yöntemi **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fa111-197">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="fa111-198">Belgeler, kullanıcı tanımlı (rastgele) JSON içeriğidir.</span><span class="sxs-lookup"><span data-stu-id="fa111-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="fa111-199">Şimdi bir veya daha fazla belge ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="fa111-199">We can now insert one or more documents.</span></span> <span data-ttu-id="fa111-200">İstediğiniz toostore veritabanınızda veriler zaten varsa, hello Azure Cosmos DB kullanabilirsiniz [veri geçiş aracı](import-data.md) tooimport hello verileri bir veritabanına.</span><span class="sxs-lookup"><span data-stu-id="fa111-200">If you already have data you'd like toostore in your database, you can use hello Azure Cosmos DB [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

<span data-ttu-id="fa111-201">İlk olarak, toocreate ihtiyacımız bir **ailesi** Bu örnekte Azure Cosmos DB içinde depolanan nesneleri temsil edecek sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fa111-201">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="fa111-202">**Family**'nin içinde kullanılan **Parent**, **Child**, **Pet**, **Address** alt sınıflarını da oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="fa111-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="fa111-203">Belgelerin, JSON'da **id** olarak seri hale getirilmiş bir **Id** özelliğine sahip olmaları gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fa111-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="fa111-204">İç alt sınıfları hello sonra aşağıdaki hello ekleyerek bu sınıfları oluşturmak **GetStartedDemo** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fa111-204">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="fa111-205">Kopyalama ve yapıştırma hello **ailesi**, **üst**, **alt**, **evcil hayvan**, ve **adresi** hello sonra sınıfları **WriteToConsoleAndPromptToContinue** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fa111-205">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after hello **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="fa111-206">Kopyalama ve yapıştırma hello **Createfamilydocumentıfnotexists** yöntemini, **adresi** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fa111-206">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

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

<span data-ttu-id="fa111-207">Ve iki belge, her biri için hello Andersen ailesi ve Wakefield ailesi hello ekleme.</span><span class="sxs-lookup"><span data-stu-id="fa111-207">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="fa111-208">Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello belge koleksiyonu oluşturulduktan sonra yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fa111-208">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document collection creation.</span></span>

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

<span data-ttu-id="fa111-209">Tuşuna **F5** toorun uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="fa111-209">Press **F5** toorun your application.</span></span>

<span data-ttu-id="fa111-210">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="fa111-210">Congratulations!</span></span> <span data-ttu-id="fa111-211">Başarılı bir şekilde iki Azure Cosmos DB belgesi oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="fa111-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Gösteren hello hello hesabı, hello çevrimiçi veritabanı, hello koleksiyon arasındaki hiyerarşik ilişkiyi Diyagram ve C# konsol uygulaması hello NoSQL Öğreticisi toocreate tarafından kullanılan hello belgeler](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="fa111-213"><a id="Query"></a>7. Adım: Azure Cosmos DB kaynaklarını sorgulama</span><span class="sxs-lookup"><span data-stu-id="fa111-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="fa111-214">Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için [zengin sorguların](documentdb-sql-query.md) gerçekleştirilmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="fa111-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="fa111-215">Merhaba aşağıdaki örnek kod çeşitli sorgularını gösterir - hem Azure Cosmos DB SQL kullanarak, sözdizimi ve bunun yanı sıra karşı çalıştırabilirsiniz LINQ - biz hello önceki adımda eklenen belgelerde hello.</span><span class="sxs-lookup"><span data-stu-id="fa111-215">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="fa111-216">Kopyalama ve yapıştırma hello **ExecuteSimpleQuery** sonra yöntemi, **Createfamilydocumentıfnotexists** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fa111-216">Copy and paste hello **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="fa111-217">Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello ikinci belge oluşturmanın sonra yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fa111-217">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="fa111-218">Tuşuna **F5** toorun uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="fa111-218">Press **F5** toorun your application.</span></span>

<span data-ttu-id="fa111-219">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="fa111-219">Congratulations!</span></span> <span data-ttu-id="fa111-220">Bir Azure Cosmos DB koleksiyonunu başarıyla sorguladınız.</span><span class="sxs-lookup"><span data-stu-id="fa111-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="fa111-221">Merhaba Aşağıdaki diyagram hello Azure Cosmos DB SQL sorgusu söz dizimi karşı hello koleksiyonu olarak adlandırılır, nasıl oluşturulacağını gösterir ve hello aynı mantığı uygular de toohello LINQ sorgusu.</span><span class="sxs-lookup"><span data-stu-id="fa111-221">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Merhaba kapsamını ve hello sorgunun anlamını diyagramı bir C# konsol uygulaması hello NoSQL Öğreticisi toocreate tarafından kullanılan](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="fa111-223">Merhaba [FROM](documentdb-sql-query.md#FromClause) Azure Cosmos DB sorguları kapsamlı tooa tek koleksiyon zaten olduğu için anahtar sözcüğü hello sorguda isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fa111-223">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="fa111-224">Bu nedenle, "FROM Families f", "FROM root r" veya seçtiğiniz herhangi bir başka değişken adıyla değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="fa111-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="fa111-225">Azure Cosmos DB aileleri, kök veya hello değişken adı, seçtiğiniz, başvuru hello geçerli koleksiyonu varsayılan olarak Infer.</span><span class="sxs-lookup"><span data-stu-id="fa111-225">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="fa111-226"><a id="ReplaceDocument"></a>8. Adım: JSON belgesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="fa111-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="fa111-227">Azure Cosmos DB, JSON belgelerini değiştirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="fa111-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="fa111-228">Kopyalama ve yapıştırma hello **ReplaceFamilyDocument** sonra yöntemi, **ExecuteSimpleQuery** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fa111-228">Copy and paste hello **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="fa111-229">Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello yöntemi hello sonunda hello sorgu yürütme sonrasında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fa111-229">Copy and paste hello following code tooyour **GetStartedDemo** method after hello query execution, at hello end of hello method.</span></span> <span data-ttu-id="fa111-230">Merhaba belgeyi değiştirdikten sonra bu hello çalıştıracaktır aynı tooview değiştirilen hello belgeyi yeniden sorgula.</span><span class="sxs-lookup"><span data-stu-id="fa111-230">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="fa111-231">Tuşuna **F5** toorun uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="fa111-231">Press **F5** toorun your application.</span></span>

<span data-ttu-id="fa111-232">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="fa111-232">Congratulations!</span></span> <span data-ttu-id="fa111-233">Başarılı bir şekilde bir Azure Cosmos DB belgesini değiştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="fa111-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="fa111-234"><a id="DeleteDocument"></a>9. Adım: JSON belgesini silme</span><span class="sxs-lookup"><span data-stu-id="fa111-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="fa111-235">Azure Cosmos DB, JSON belgelerini silmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="fa111-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="fa111-236">Kopyalama ve yapıştırma hello **DeleteFamilyDocument** sonra yöntemi, **ReplaceFamilyDocument** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fa111-236">Copy and paste hello **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="fa111-237">Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello ikinci sorguyu yürütmenin, hello yöntemi hello sonunda sonra yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fa111-237">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second query execution, at hello end of hello method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="fa111-238">Tuşuna **F5** toorun uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="fa111-238">Press **F5** toorun your application.</span></span>

<span data-ttu-id="fa111-239">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="fa111-239">Congratulations!</span></span> <span data-ttu-id="fa111-240">Başarılı bir şekilde bir Azure Cosmos DB belgesini sildiniz.</span><span class="sxs-lookup"><span data-stu-id="fa111-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="fa111-241"><a id="DeleteDatabase"></a>10. adım: hello veritabanını silme</span><span class="sxs-lookup"><span data-stu-id="fa111-241"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="fa111-242">Veritabanı oluşturulan silme hello hello veritabanı ve tüm alt kaynaklar (koleksiyonlar, belgeler, vb.) kaldırır.</span><span class="sxs-lookup"><span data-stu-id="fa111-242">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="fa111-243">Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** yöntemini hello belge sonra toodelete hello tüm veritabanını ve tüm alt kaynaklarını silin.</span><span class="sxs-lookup"><span data-stu-id="fa111-243">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document delete toodelete hello entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="fa111-244">Tuşuna **F5** toorun uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="fa111-244">Press **F5** toorun your application.</span></span>

<span data-ttu-id="fa111-245">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="fa111-245">Congratulations!</span></span> <span data-ttu-id="fa111-246">Başarılı bir şekilde bir Azure Cosmos DB veritabanını sildiniz.</span><span class="sxs-lookup"><span data-stu-id="fa111-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="fa111-247"><a id="Run"></a>11. Adım: C# konsol uygulamanızı hep birlikte çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="fa111-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="fa111-248">Visual Studio toobuild hello uygulamasında hata ayıklama modunda F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="fa111-248">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="fa111-249">Başlarken uygulamanızın bir konsol penceresinde hello çıktısını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa111-249">You should see hello output of your get started app in a console window.</span></span> <span data-ttu-id="fa111-250">Merhaba çıktı hello hello sonuçlarını gösterir eklenir ve hello örnek metinle eşleşmelidir sorgular.</span><span class="sxs-lookup"><span data-stu-id="fa111-250">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

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

<span data-ttu-id="fa111-251">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="fa111-251">Congratulations!</span></span> <span data-ttu-id="fa111-252">Merhaba öğreticisini tamamladınız ve çalışma C# konsol uygulaması sahip!</span><span class="sxs-lookup"><span data-stu-id="fa111-252">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="fa111-253"><a id="GetSolution"></a>Merhaba tam Öğreticisi çözümünü edinme</span><span class="sxs-lookup"><span data-stu-id="fa111-253"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="fa111-254">Toocomplete hello adımları Bu öğreticinin veya yalnızca istediğiniz toodownload hello kod örnekleri saati yoksa alamadık, buradan edinebilirsiniz [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="fa111-254">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="fa111-255">toobuild hello GetStarted çözümünü hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="fa111-255">toobuild hello GetStarted solution, you will need hello following:</span></span>

* <span data-ttu-id="fa111-256">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="fa111-256">An active Azure account.</span></span> <span data-ttu-id="fa111-257">Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa111-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="fa111-258">Bir [Azure Cosmos DB hesabı][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="fa111-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="fa111-259">Merhaba [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) çözüm Github'da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fa111-259">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="fa111-260">toorestore hello başvuruları toohello Azure Cosmos DB .NET SDK Visual Studio'da sağ hello **GetStarted** Çözüm Gezgini ve ardından çözüm **NuGet paketi geri yüklemeyi etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="fa111-260">toorestore hello references toohello Azure Cosmos DB .NET SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="fa111-261">Ardından, hello App.config dosyasında açıklandığı gibi hello EndpointUrl ve AuthorizationKey değerlerini güncelleştirin [tooan Azure Cosmos DB hesabını bağlaması](#Connect).</span><span class="sxs-lookup"><span data-stu-id="fa111-261">Next, in hello App.config file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="fa111-262">Hepsi bu kadar, derleyin ve devam edin!</span><span class="sxs-lookup"><span data-stu-id="fa111-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="fa111-263">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fa111-263">Next steps</span></span>
* <span data-ttu-id="fa111-264">Daha karmaşık bir ASP.NET MVC öğreticisi mi istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="fa111-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="fa111-265">Bkz: [ASP.NET MVC Öğreticisi: Web uygulaması geliştirme Azure Cosmos DB ile](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="fa111-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="fa111-266">Tooperform ölçek ve performans ile Azure Cosmos DB istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="fa111-266">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="fa111-267">Bkz: [performansı ve ölçeği Azure Cosmos DB ile test etme](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="fa111-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="fa111-268">Nasıl çok öğrenin[Azure Cosmos DB istekleri, kullanım ve depolama izleme](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="fa111-268">Learn how too[monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="fa111-269">Merhaba, örnek veri kümelerimizde sorgular çalıştırın [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="fa111-269">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="fa111-270">toolearn Azure Cosmos DB hakkında daha fazla bilgi görmek [tooAzure Cosmos DB Hoş Geldiniz](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="fa111-270">toolearn more about Azure Cosmos DB, see [Welcome tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
