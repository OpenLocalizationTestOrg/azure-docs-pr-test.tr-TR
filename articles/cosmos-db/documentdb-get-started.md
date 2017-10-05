---
title: "Azure Cosmos DB: DocumentDB API başlangıç öğreticisi | Microsoft Docs"
description: "DocumentDB API'sini kullanarak çevrimiçi bir veritabanı ve C# konsol uygulaması oluşturan öğretici."
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
ms.openlocfilehash: 72f66081a6409f980ec6bca5188f585489245a36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="a56cb-104">Azure Cosmos DB: DocumentDB API başlangıç öğreticisi</span><span class="sxs-lookup"><span data-stu-id="a56cb-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a56cb-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a56cb-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="a56cb-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="a56cb-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="a56cb-107">MongoDB için Node.js</span><span class="sxs-lookup"><span data-stu-id="a56cb-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="a56cb-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="a56cb-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="a56cb-109">Java</span><span class="sxs-lookup"><span data-stu-id="a56cb-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="a56cb-110">C++</span><span class="sxs-lookup"><span data-stu-id="a56cb-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="a56cb-111">Azure Cosmos DB: DocumentDB API başlangıç öğreticisine hoş geldiniz!</span><span class="sxs-lookup"><span data-stu-id="a56cb-111">Welcome to the Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="a56cb-112">Bu öğreticiyi uyguladıktan sonra, Azure Cosmos DB kaynaklarını oluşturan ve sorgulayan bir konsol uygulamasına sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a56cb-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="a56cb-113">Şu konulara değineceğiz:</span><span class="sxs-lookup"><span data-stu-id="a56cb-113">We'll cover:</span></span>

* <span data-ttu-id="a56cb-114">Azure Cosmos DB hesabı oluşturma ve hesaba bağlanma</span><span class="sxs-lookup"><span data-stu-id="a56cb-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="a56cb-115">Visual Studio Çözümünüzü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a56cb-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="a56cb-116">Çevrimiçi bir veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a56cb-116">Creating an online database</span></span>
* <span data-ttu-id="a56cb-117">Koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="a56cb-117">Creating a collection</span></span>
* <span data-ttu-id="a56cb-118">JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="a56cb-118">Creating JSON documents</span></span>
* <span data-ttu-id="a56cb-119">Koleksiyonu sorgulama</span><span class="sxs-lookup"><span data-stu-id="a56cb-119">Querying the collection</span></span>
* <span data-ttu-id="a56cb-120">Bir belgeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="a56cb-120">Replacing a document</span></span>
* <span data-ttu-id="a56cb-121">Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="a56cb-121">Deleting a document</span></span>
* <span data-ttu-id="a56cb-122">Veritabanını silme</span><span class="sxs-lookup"><span data-stu-id="a56cb-122">Deleting the database</span></span>

<span data-ttu-id="a56cb-123">Zamanınız yok mu?</span><span class="sxs-lookup"><span data-stu-id="a56cb-123">Don't have time?</span></span> <span data-ttu-id="a56cb-124">Endişelenmeyin!</span><span class="sxs-lookup"><span data-stu-id="a56cb-124">Don't worry!</span></span> <span data-ttu-id="a56cb-125">Eksiksiz çözümü [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started)'da bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="a56cb-126">Hızlı yönergeler için [NoSQL öğreticisi tam çözümünü edinme](#GetSolution) bölümüne atlayın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-126">Jump to the [Get the complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="a56cb-127">Ardından bize geri bildirim sağlamak için lütfen bu sayfanın üst veya alt kısmındaki oylama düğmelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-127">Afterwards, please use the voting buttons at the top or bottom of this page to give us feedback.</span></span> <span data-ttu-id="a56cb-128">Doğrudan sizinle iletişim kurmamızı isterseniz yorumlarınıza e-posta adresinizi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a56cb-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="a56cb-129">Şimdi başlayalım!</span><span class="sxs-lookup"><span data-stu-id="a56cb-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a56cb-130">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a56cb-130">Prerequisites</span></span>
<span data-ttu-id="a56cb-131">Lütfen aşağıdakilere sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="a56cb-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="a56cb-132">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="a56cb-132">An active Azure account.</span></span> <span data-ttu-id="a56cb-133">Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="a56cb-134">Alternatif olarak bu öğretici için [Azure Cosmos DB Öykünücüsü](local-emulator.md)’nü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-134">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="a56cb-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="a56cb-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="a56cb-136">1. Adım: Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a56cb-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="a56cb-137">Bir Azure Cosmos DB hesabı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="a56cb-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="a56cb-138">Kullanmak istediğiniz bir hesap zaten varsa [Visual Studio Çözümünüzü Kurma](#SetupVS)'ya atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-138">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="a56cb-139">Azure Cosmos DB Öykünücüsü’nü kullanıyorsanız öykünücünün kurulumunu gerçekleştirmek için lütfen [Azure Cosmos DB Öykünücüsü](local-emulator.md) konusundaki adımları izleyin ve [Visual Studio Çözümünüzü Ayarlama](#SetupVS) adımına atlayın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-139">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="a56cb-140"><a id="SetupVS"></a>2. Adım: Visual Studio çözümünüzü kurma</span><span class="sxs-lookup"><span data-stu-id="a56cb-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="a56cb-141">Bilgisayarınızda **Visual Studio 2017**'yi açın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="a56cb-142">**Dosya** menüsünde **Yeni**'yi seçin ve ardından **Proje**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="a56cb-142">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="a56cb-143">**Yeni Proje** iletişim kutusunda, **Şablonlar** / **Visual C#** / **Konsol Uygulaması**'nı seçin, projenizi adlandırın ve ardından **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-143">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="a56cb-144">![Yeni Proje penceresinin ekran görüntüsü](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="a56cb-144">![Screen shot of the New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="a56cb-145">**Çözüm Gezgini**'nde Visual Studio çözümünüzün altındaki yeni konsol uygulamanıza sağ tıklayın ve **NuGet Paketlerini Yönet...** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-145">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Proje için Sağ Tıklama Menüsünün ekran görüntüsü](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="a56cb-147">**NuGet** sekmesinde **Gözat**'a tıklayın ve arama kutusuna **azure documentdb** yazın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-147">In the **Nuget** tab, click **Browse**, and type **azure documentdb** in the search box.</span></span>
6. <span data-ttu-id="a56cb-148">Sonuçlarda **Microsoft.Azure.DocumentDB**'yi bulun ve **Yükle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-148">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="a56cb-149">Azure Cosmos DB DocumentDB API'si istemci kitaplığı için paket kimliği [Microsoft Azure DocumentDB istemci Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="a56cb-149">The package ID for the Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="a56cb-150">![Azure Cosmos DB İstemci SDK'sını bulmak için Nuget Menüsünün ekran görüntüsü](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="a56cb-150">![Screen shot of the Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="a56cb-151">Çözümdeki değişiklikleri gözden geçirme hakkında bir ileti alırsanız **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-151">If you get a messages about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="a56cb-152">Lisans kabulü hakkında bir ileti alırsanız **Kabul ediyorum**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="a56cb-153">Harika!</span><span class="sxs-lookup"><span data-stu-id="a56cb-153">Great!</span></span> <span data-ttu-id="a56cb-154">Kurulumu tamamladığımıza göre, biraz kod yazmaya başlayalım.</span><span class="sxs-lookup"><span data-stu-id="a56cb-154">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="a56cb-155">Bu öğreticinin tamamlanmış kod projesini [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs)'da bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="a56cb-156"><a id="Connect"></a>3. Adım: Azure Cosmos DB hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="a56cb-156"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="a56cb-157">İlk olarak, Program.cs dosyasında C# uygulamanızın başlangıcına bu başvuruları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a56cb-157">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART TO YOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="a56cb-158">Bu öğreticiyi tamamlamak için, yukarıdaki bağımlılıkları eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="a56cb-158">In order to complete the tutorial, make sure you add the dependencies above.</span></span>
> 
> 

<span data-ttu-id="a56cb-159">Şimdi bu iki sabiti ve *client* değişkeninizi *Program* ortak sınıfının altına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a56cb-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="a56cb-160">Ardından, uç nokta URL’nizi ve birincil anahtarınızı almak için tekrar [Azure Portal](https://portal.azure.com)’a gidin.</span><span class="sxs-lookup"><span data-stu-id="a56cb-160">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="a56cb-161">Uç nokta URL’si ve birincil anahtar, uygulamanızın nereye bağlanacağını anlaması ve Azure Cosmos DB’nin uygulamanızın bağlantısına güvenmesi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a56cb-161">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="a56cb-162">Azure Portal'da Azure Cosmos DB hesabınıza gidin ve ardından **Anahtarlar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-162">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="a56cb-163">Portaldaki URI’yi kopyalayın ve program.cs dosyasındaki `<your endpoint URL>` içine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-163">Copy the URI from the portal and paste it into `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="a56cb-164">Ardından portaldan BİRİNCİL ANAHTARI kopyalayın ve `<your primary key>` içine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-164">Then copy the PRIMARY KEY from the portal and paste it into `<your primary key>`.</span></span>

![Bir C# konsol uygulaması oluşturmak için NoSQL öğreticisi tarafından kullanılan Azure Portal'ın ekran görüntüsü][keys]

<span data-ttu-id="a56cb-167">Ardından **DocumentClient**'ın yeni bir örneğini oluşturarak uygulamayı başlatacağız.</span><span class="sxs-lookup"><span data-stu-id="a56cb-167">Next, we'll start the application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="a56cb-168">**Main** yönteminin altına yeni **DocumentClient**'ımızın örneğini oluşturacak **GetStartedDemo** adlı bu zaman uyumsuz yeni görevi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a56cb-168">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART TO YOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="a56cb-169">Zaman uyumsuz görevinizi **Main** yönteminizden çalıştırmak için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a56cb-169">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="a56cb-170">**Main** yöntemi özel durumları yakalar ve bunları konsola yazar.</span><span class="sxs-lookup"><span data-stu-id="a56cb-170">The **Main** method will catch exceptions and write them to the console.</span></span>

    static void Main(string[] args)
    {
            // ADD THIS PART TO YOUR CODE
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
                    Console.WriteLine("End of demo, press any key to exit.");
                    Console.ReadKey();
            }

<span data-ttu-id="a56cb-171">Uygulamanızı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-171">Press **F5** to run your application.</span></span> <span data-ttu-id="a56cb-172">Konsol penceresi çıktısı, bağlantının kurulduğunu onaylayan `End of demo, press any key to exit.` iletisini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a56cb-172">The console window output displays the message `End of demo, press any key to exit.` confirming that the connection was made.</span></span>  <span data-ttu-id="a56cb-173">Ardından konsol penceresini kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-173">You can then close the console window.</span></span> 

<span data-ttu-id="a56cb-174">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="a56cb-174">Congratulations!</span></span> <span data-ttu-id="a56cb-175">Bir Azure Cosmos DB hesabına başarıyla bağlandınız, şimdi Azure Cosmos DB kaynaklarıyla çalışmaya bakalım.</span><span class="sxs-lookup"><span data-stu-id="a56cb-175">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="a56cb-176">4. Adım: Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a56cb-176">Step 4: Create a database</span></span>
<span data-ttu-id="a56cb-177">Bir veritabanı oluşturmak için kodu eklemeden önce, konsola yazma için bir yardımcı yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a56cb-177">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="a56cb-178">**WriteToConsoleAndPromptToContinue** yöntemini kopyalayın ve **GetStartedDemo** yönteminin sonrasında yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-178">Copy and paste the **WriteToConsoleAndPromptToContinue** method after the **GetStartedDemo** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="a56cb-179">Azure Cosmos DB [veritabanınız](documentdb-resources.md#databases), **DocumentClient** sınıfının [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) yöntemi kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="a56cb-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="a56cb-180">Veritabanı, koleksiyonlar genelinde bölümlenmiş JSON belgesi depolama alanının mantıksal bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="a56cb-180">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="a56cb-181">Aşağıdaki kodu kopyalayın ve istemci oluşturmanın sonrasında **GetStartedDemo** yönteminize yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-181">Copy and paste the following code to your **GetStartedDemo** method after the client creation.</span></span> <span data-ttu-id="a56cb-182">Bu, *FamilyDB* adlı bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a56cb-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART TO YOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="a56cb-183">Uygulamanızı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-183">Press **F5** to run your application.</span></span>

<span data-ttu-id="a56cb-184">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="a56cb-184">Congratulations!</span></span> <span data-ttu-id="a56cb-185">Başarılı bir şekilde bir Azure Cosmos DB veritabanı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="a56cb-186"><a id="CreateColl"></a>5. Adım: Koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="a56cb-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="a56cb-187">**CreateDocumentCollectionIfNotExistsAsync**, ayrılmış işleme ile yeni bir koleksiyon oluşturur, bu da ücret ödenmesini gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="a56cb-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="a56cb-188">Daha ayrıntılı bilgi için lütfen [fiyatlandırma sayfamızı](https://azure.microsoft.com/pricing/details/cosmos-db/) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="a56cb-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="a56cb-189">Bir [koleksiyon](documentdb-resources.md#collections), **DocumentClient** sınıfının [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) yöntemi kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="a56cb-189">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="a56cb-190">Koleksiyon, JSON belgelerinin ve ilişkili JavaScript uygulama mantığının bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="a56cb-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="a56cb-191">Aşağıdaki kodu kopyalayın ve veritabanı oluşturmanın sonrasında **GetStartedDemo** yönteminize yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-191">Copy and paste the following code to your **GetStartedDemo** method after the database creation.</span></span> <span data-ttu-id="a56cb-192">Bu, *FamilyCollection* adlı bir belge koleksiyonu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a56cb-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART TO YOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="a56cb-193">Uygulamanızı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-193">Press **F5** to run your application.</span></span>

<span data-ttu-id="a56cb-194">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="a56cb-194">Congratulations!</span></span> <span data-ttu-id="a56cb-195">Başarılı bir şekilde bir Azure Cosmos DB belge koleksiyonu oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="a56cb-196"><a id="CreateDoc"></a>6. Adım: JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="a56cb-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="a56cb-197">Bir [belge](documentdb-resources.md#documents), **DocumentClient** sınıfının [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) yöntemi kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="a56cb-197">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="a56cb-198">Belgeler, kullanıcı tanımlı (rastgele) JSON içeriğidir.</span><span class="sxs-lookup"><span data-stu-id="a56cb-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="a56cb-199">Şimdi bir veya daha fazla belge ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-199">We can now insert one or more documents.</span></span> <span data-ttu-id="a56cb-200">Veritabanınızda depolamak istediğiniz veriler zaten varsa, Azure Cosmos DB kullanabilirsiniz [veri geçiş aracı](import-data.md) verileri bir veritabanına aktarmak için.</span><span class="sxs-lookup"><span data-stu-id="a56cb-200">If you already have data you'd like to store in your database, you can use the Azure Cosmos DB [Data Migration tool](import-data.md) to import the data into a database.</span></span>

<span data-ttu-id="a56cb-201">İlk olarak, bu örnekte Azure Cosmos DB içinde depolanan nesneleri temsil edecek bir **Family** sınıfı oluşturmamız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a56cb-201">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="a56cb-202">**Family**'nin içinde kullanılan **Parent**, **Child**, **Pet**, **Address** alt sınıflarını da oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="a56cb-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="a56cb-203">Belgelerin, JSON'da **id** olarak seri hale getirilmiş bir **Id** özelliğine sahip olmaları gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="a56cb-204">Bu sınıfları oluşturmak için **GetStartedDemo** yönteminden sonra aşağıdaki iç alt sınıfları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a56cb-204">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="a56cb-205">**Family**, **Parent**, **Child**, **Pet** ve **Address** sınıflarını kopyalayın ve **WriteToConsoleAndPromptToContinue** yönteminin sonrasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-205">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after the **WriteToConsoleAndPromptToContinue** method.</span></span>

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="a56cb-206">**CreateFamilyDocumentIfNotExists** yöntemini kopyalayın ve **Address** sınıfınızın altına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-206">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="a56cb-207">Andersen Ailesi ve Wakefield Ailesi için birer tane olmak üzere iki belge yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="a56cb-207">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="a56cb-208">Aşağıdaki kodu kopyalayın ve belge koleksiyonu oluşturmanın sonrasında **GetStartedDemo** yönteminize yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-208">Copy and paste the following code to your **GetStartedDemo** method after the document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="a56cb-209">Uygulamanızı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-209">Press **F5** to run your application.</span></span>

<span data-ttu-id="a56cb-210">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="a56cb-210">Congratulations!</span></span> <span data-ttu-id="a56cb-211">Başarılı bir şekilde iki Azure Cosmos DB belgesi oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Bir C# konsol uygulaması oluşturmak için NoSQL öğreticisi tarafından kullanılan belgeler, hesap, çevrimiçi veritabanı ve koleksiyon arasındaki hiyerarşik ilişkiyi gösteren diyagram](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="a56cb-213"><a id="Query"></a>7. Adım: Azure Cosmos DB kaynaklarını sorgulama</span><span class="sxs-lookup"><span data-stu-id="a56cb-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="a56cb-214">Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için [zengin sorguların](documentdb-sql-query.md) gerçekleştirilmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="a56cb-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="a56cb-215">Aşağıdaki örnek kod, önceki adımda yerleştirdiğimiz belgelerde hem Azure Cosmos DB SQL söz dizimi hem de LINQ kullanarak çalıştırabileceğimiz çeşitli sorguları gösterir.</span><span class="sxs-lookup"><span data-stu-id="a56cb-215">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="a56cb-216">**ExecuteSimpleQuery** yöntemini kopyalayın ve **CreateFamilyDocumentIfNotExists** yönteminizin sonrasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-216">Copy and paste the **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find the Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute the same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="a56cb-217">Aşağıdaki kodu kopyalayın ve ikinci belge oluşturmanın sonrasında **GetStartedDemo** yönteminize yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-217">Copy and paste the following code to your **GetStartedDemo** method after the second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART TO YOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="a56cb-218">Uygulamanızı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-218">Press **F5** to run your application.</span></span>

<span data-ttu-id="a56cb-219">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="a56cb-219">Congratulations!</span></span> <span data-ttu-id="a56cb-220">Bir Azure Cosmos DB koleksiyonunu başarıyla sorguladınız.</span><span class="sxs-lookup"><span data-stu-id="a56cb-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="a56cb-221">Aşağıdaki diyagram oluşturduğunuz koleksiyonda Azure Cosmos DB SQL sorgusu söz diziminin nasıl çağrıldığını gösterir, aynı mantık LINQ sorgusu için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="a56cb-221">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Bir C# konsol uygulaması oluşturmak için NoSQL öğreticisi tarafından kullanılan sorgunun kapsamını ve anlamını gösteren diyagram](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="a56cb-223">[FROM](documentdb-sql-query.md#FromClause) Azure Cosmos DB sorguları zaten tek bir koleksiyon kapsamında olduğundan anahtar sözcüğü sorguda isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a56cb-223">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="a56cb-224">Bu nedenle, "FROM Families f", "FROM root r" veya seçtiğiniz herhangi bir başka değişken adıyla değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a56cb-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="a56cb-225">Azure Cosmos DB Families, root veya seçtiğiniz değişken adı olarak Infer, varsayılan olarak geçerli koleksiyonun başvuru.</span><span class="sxs-lookup"><span data-stu-id="a56cb-225">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="a56cb-226"><a id="ReplaceDocument"></a>8. Adım: JSON belgesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="a56cb-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="a56cb-227">Azure Cosmos DB, JSON belgelerini değiştirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="a56cb-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="a56cb-228">**ReplaceFamilyDocument** yöntemini kopyalayın ve **ExecuteSimpleQuery** yönteminizin sonrasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-228">Copy and paste the **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="a56cb-229">Aşağıdaki kodu kopyalayın ve sorgu yürütmenin sonrasına, **GetStartedDemo** yönteminizin sonuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-229">Copy and paste the following code to your **GetStartedDemo** method after the query execution, at the end of the method.</span></span> <span data-ttu-id="a56cb-230">Belgeyi değiştirdikten sonra, aynı sorgu tekrar çalıştırılarak değiştirilen belge görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a56cb-230">After replacing the document, this will run the same query again to view the changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART TO YOUR CODE
    // Update the Grade of the Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="a56cb-231">Uygulamanızı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-231">Press **F5** to run your application.</span></span>

<span data-ttu-id="a56cb-232">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="a56cb-232">Congratulations!</span></span> <span data-ttu-id="a56cb-233">Başarılı bir şekilde bir Azure Cosmos DB belgesini değiştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="a56cb-234"><a id="DeleteDocument"></a>9. Adım: JSON belgesini silme</span><span class="sxs-lookup"><span data-stu-id="a56cb-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="a56cb-235">Azure Cosmos DB, JSON belgelerini silmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="a56cb-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="a56cb-236">**DeleteFamilyDocument** yöntemini kopyalayın ve **ReplaceFamilyDocument** yönteminizin sonrasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-236">Copy and paste the **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="a56cb-237">Aşağıdaki kodu kopyalayın ve ikinci sorgu yürütmenin sonrasına, **GetStartedDemo** yönteminizin sonuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-237">Copy and paste the following code to your **GetStartedDemo** method after the second query execution, at the end of the method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART TO CODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="a56cb-238">Uygulamanızı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-238">Press **F5** to run your application.</span></span>

<span data-ttu-id="a56cb-239">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="a56cb-239">Congratulations!</span></span> <span data-ttu-id="a56cb-240">Başarılı bir şekilde bir Azure Cosmos DB belgesini sildiniz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="a56cb-241"><a id="DeleteDatabase"></a>10. Adım: Veritabanını silme</span><span class="sxs-lookup"><span data-stu-id="a56cb-241"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="a56cb-242">Oluşturulan veritabanı silindiğinde, veritabanı ve tüm alt kaynaklar (koleksiyonlar, belgeler vb.) kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="a56cb-242">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="a56cb-243">Tüm veritabanını ve tüm alt kaynaklarını silmek için aşağıdaki kodu kopyalayın ve belge silmenin sonrasında **GetStartedDemo** yönteminize yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-243">Copy and paste the following code to your **GetStartedDemo** method after the document delete to delete the entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART TO CODE
    // Clean up/delete the database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="a56cb-244">Uygulamanızı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-244">Press **F5** to run your application.</span></span>

<span data-ttu-id="a56cb-245">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="a56cb-245">Congratulations!</span></span> <span data-ttu-id="a56cb-246">Başarılı bir şekilde bir Azure Cosmos DB veritabanını sildiniz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="a56cb-247"><a id="Run"></a>11. Adım: C# konsol uygulamanızı hep birlikte çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="a56cb-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="a56cb-248">Uygulamayı hata ayıklama modunda oluşturmak için Visual Studio'da F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-248">Hit F5 in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="a56cb-249">Başlarken uygulamanızın bir konsol penceresinde çıktısını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a56cb-249">You should see the output of your get started app in a console window.</span></span> <span data-ttu-id="a56cb-250">Çıktı, eklediğimiz sorguların sonuçlarını gösterir ve aşağıdaki örnek metinle eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="a56cb-250">The output will show the results of the queries we added and should match the example text below.</span></span>

    Created FamilyDB
    Press any key to continue ...
    Created FamilyCollection
    Press any key to continue ...
    Created Family Andersen.1
    Press any key to continue ...
    Created Family Wakefield.7
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key to exit.

<span data-ttu-id="a56cb-251">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="a56cb-251">Congratulations!</span></span> <span data-ttu-id="a56cb-252">Bu öğreticiyi tamamladınız ve çalışan bir C# konsol uygulamasına sahipsiniz!</span><span class="sxs-lookup"><span data-stu-id="a56cb-252">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="a56cb-253"><a id="GetSolution"></a> Tam öğretici çözümünü edinin</span><span class="sxs-lookup"><span data-stu-id="a56cb-253"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="a56cb-254">Bu öğreticideki adımları tamamlama fırsatınız olmadıysa veya yalnızca kod örneklerini indirmek isterseniz [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started)'dan ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-254">If you didn't have time to complete the steps in this tutorial, or just want to download the code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="a56cb-255">GetStarted çözümünü oluşturmak için aşağıdakilere ihtiyacınız olacak:</span><span class="sxs-lookup"><span data-stu-id="a56cb-255">To build the GetStarted solution, you will need the following:</span></span>

* <span data-ttu-id="a56cb-256">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="a56cb-256">An active Azure account.</span></span> <span data-ttu-id="a56cb-257">Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a56cb-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="a56cb-258">Bir [Azure Cosmos DB hesabı][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="a56cb-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="a56cb-259">GitHub'da bulunan [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) çözümü.</span><span class="sxs-lookup"><span data-stu-id="a56cb-259">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="a56cb-260">Visual Studio'da Azure Cosmos DB .NET SDK başvuruları geri yüklemek için sağ **GetStarted** Çözüm Gezgini ve ardından çözüm **NuGet paketi geri yüklemeyi etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="a56cb-260">To restore the references to the Azure Cosmos DB .NET SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="a56cb-261">Ardından, App.config dosyasında EndpointUrl ve AuthorizationKey değerlerini [Azure Cosmos DB hesabına bağlanma](#Connect) bölümünde açıklandığı gibi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a56cb-261">Next, in the App.config file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="a56cb-262">Hepsi bu kadar, derleyin ve devam edin!</span><span class="sxs-lookup"><span data-stu-id="a56cb-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="a56cb-263">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a56cb-263">Next steps</span></span>
* <span data-ttu-id="a56cb-264">Daha karmaşık bir ASP.NET MVC öğreticisi mi istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="a56cb-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="a56cb-265">Bkz: [ASP.NET MVC Öğreticisi: Web uygulaması geliştirme Azure Cosmos DB ile](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="a56cb-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="a56cb-266">Azure Cosmos DB ile ölçek ve performans testi mi yapmak istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="a56cb-266">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="a56cb-267">Bkz: [performansı ve ölçeği Azure Cosmos DB ile test etme](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="a56cb-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="a56cb-268">Bilgi edinmek için nasıl [Azure Cosmos DB istekleri, kullanım ve depolama izleme](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="a56cb-268">Learn how to [monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="a56cb-269">[Query Playground](https://www.documentdb.com/sql/demo)'daki örnek veri kümelerimizde sorgular çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a56cb-269">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="a56cb-270">Azure Cosmos DB hakkında daha fazla bilgi için bkz: ['na Hoş Geldiniz Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="a56cb-270">To learn more about Azure Cosmos DB, see [Welcome to Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
