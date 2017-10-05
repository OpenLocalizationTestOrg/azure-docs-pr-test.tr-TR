---
title: "Azure Cosmos DB: .NET Core ile DocumentDB API’si başlangıç öğreticisi | Microsoft Docs"
description: "Azure Cosmos DB DocumentDB API’si .NET Core SDK'sını kullanarak çevrimiçi bir veritabanı ve C# konsol uygulaması oluşturan öğretici."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 7536978bbb1e41b6484b66fd1b51c900fc3e545d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-getting-started-with-the-documentdb-api-and-net-core"></a><span data-ttu-id="0922e-103">Azure Cosmos DB: DocumentDB API’si ve .NET Core ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0922e-103">Azure Cosmos DB: Getting started with the DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0922e-104">.NET</span><span class="sxs-lookup"><span data-stu-id="0922e-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="0922e-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="0922e-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="0922e-106">MongoDB için Node.js</span><span class="sxs-lookup"><span data-stu-id="0922e-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="0922e-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="0922e-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="0922e-108">Java</span><span class="sxs-lookup"><span data-stu-id="0922e-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="0922e-109">C++</span><span class="sxs-lookup"><span data-stu-id="0922e-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="0922e-110">DocumentDB API'sine Azure Cosmos .NET Core eğitici Başlarken DB için Hoş Geldiniz!</span><span class="sxs-lookup"><span data-stu-id="0922e-110">Welcome to the DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="0922e-111">Bu öğreticiyi uyguladıktan sonra, Azure Cosmos DB kaynaklarını oluşturan ve sorgulayan bir konsol uygulamasına sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0922e-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="0922e-112">Şu konulara değineceğiz:</span><span class="sxs-lookup"><span data-stu-id="0922e-112">We'll cover:</span></span>

* <span data-ttu-id="0922e-113">Azure Cosmos DB hesabı oluşturma ve hesaba bağlanma</span><span class="sxs-lookup"><span data-stu-id="0922e-113">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="0922e-114">Visual Studio Çözümünüzü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0922e-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="0922e-115">Çevrimiçi bir veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0922e-115">Creating an online database</span></span>
* <span data-ttu-id="0922e-116">Koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="0922e-116">Creating a collection</span></span>
* <span data-ttu-id="0922e-117">JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="0922e-117">Creating JSON documents</span></span>
* <span data-ttu-id="0922e-118">Koleksiyonu sorgulama</span><span class="sxs-lookup"><span data-stu-id="0922e-118">Querying the collection</span></span>
* <span data-ttu-id="0922e-119">Bir belgeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="0922e-119">Replacing a document</span></span>
* <span data-ttu-id="0922e-120">Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="0922e-120">Deleting a document</span></span>
* <span data-ttu-id="0922e-121">Veritabanını silme</span><span class="sxs-lookup"><span data-stu-id="0922e-121">Deleting the database</span></span>

<span data-ttu-id="0922e-122">Zamanınız yok mu?</span><span class="sxs-lookup"><span data-stu-id="0922e-122">Don't have time?</span></span> <span data-ttu-id="0922e-123">Endişelenmeyin!</span><span class="sxs-lookup"><span data-stu-id="0922e-123">Don't worry!</span></span> <span data-ttu-id="0922e-124">Eksiksiz çözümü [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started)'da bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0922e-124">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="0922e-125">Hızlı yönergeler için [Tam çözümü edinme bölümüne](#GetSolution) atlayın.</span><span class="sxs-lookup"><span data-stu-id="0922e-125">Jump to the [Get the complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="0922e-126">Xamarin iOS, Android veya formlar oluşturmak istediğiniz DocumentDB API ve .NET Core SDK kullanarak uygulama?</span><span class="sxs-lookup"><span data-stu-id="0922e-126">Want to build a Xamarin iOS, Android, or Forms application using the DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="0922e-127">Bkz: [yapı Xamarin ve Azure Cosmos DB mobil uygulamalar](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="0922e-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0922e-128">Azure Cosmos DB .NET Core Bu öğreticide kullanılan SDK henüz Evrensel Windows Platformu (UWP) uygulamaları ile uyumlu değil.</span><span class="sxs-lookup"><span data-stu-id="0922e-128">The Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="0922e-129">.NET Core SDK'sının UWP uygulamalarını destekleyen bir önizleme sürümü için [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) adresine e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="0922e-129">For a preview version of the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="0922e-130">Şimdi başlayalım!</span><span class="sxs-lookup"><span data-stu-id="0922e-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0922e-131">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0922e-131">Prerequisites</span></span>
<span data-ttu-id="0922e-132">Lütfen aşağıdakilere sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="0922e-132">Please make sure you have the following:</span></span>

* <span data-ttu-id="0922e-133">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="0922e-133">An active Azure account.</span></span> <span data-ttu-id="0922e-134">Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0922e-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="0922e-135">Alternatif olarak bu öğretici için [Azure Cosmos DB Öykünücüsü](local-emulator.md)’nü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0922e-135">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="0922e-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="0922e-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="0922e-137">MacOS veya Linux’ta çalışıyorsanız tercih ettiğiniz platforma yönelik [.NET Core SDK](https://www.microsoft.com/net/core#macos)’yı yükleyerek komut satırından .NET Core uygulamaları geliştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0922e-137">If you're working on MacOS or Linux, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#macos) for the platform of your choice.</span></span> 
    * <span data-ttu-id="0922e-138">Windows’da çalışıyorsanız [.NET Core SDK](https://www.microsoft.com/net/core#windows)’yı yükleyerek komut satırından .NET Core uygulamaları geliştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0922e-138">If you're working on Windows, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="0922e-139">Kendi düzenleyicinizi kullanabilir ya da ücretsiz olan ve Windows, Linux ve MacOS’de çalışan [Visual Studio Code](https://code.visualstudio.com/)’u indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0922e-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="0922e-140">1. Adım: Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0922e-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="0922e-141">Bir Azure Cosmos DB hesabı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="0922e-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="0922e-142">Kullanmak istediğiniz bir hesap zaten varsa [Visual Studio Çözümünüzü Kurma](#SetupVS)'ya atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0922e-142">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="0922e-143">Azure Cosmos DB Öykünücüsü’nü kullanıyorsanız öykünücünün kurulumunu gerçekleştirmek için lütfen [Azure Cosmos DB Öykünücüsü](local-emulator.md) konusundaki adımları izleyin ve [Visual Studio Çözümünüzü Ayarlama](#SetupVS) adımına atlayın.</span><span class="sxs-lookup"><span data-stu-id="0922e-143">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="0922e-144"><a id="SetupVS"></a>2. Adım: Visual Studio çözümünüzü kurma</span><span class="sxs-lookup"><span data-stu-id="0922e-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="0922e-145">Bilgisayarınızda **Visual Studio 2017**'yi açın.</span><span class="sxs-lookup"><span data-stu-id="0922e-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="0922e-146">**Dosya** menüsünde **Yeni**'yi seçin ve ardından **Proje**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="0922e-146">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="0922e-147">**Yeni Proje** iletişim kutusunda **Şablonlar** / **Visual C#** / **.NET Core**/**Konsol Uygulaması (.NET Core)** seçeneğini belirleyin, projenizi **DocumentDBGettingStarted** olarak adlandırın ve **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0922e-147">In the **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Yeni Proje penceresinin ekran görüntüsü](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="0922e-149">**Çözüm Gezgini** içinde, **DocumentDBGettingStarted**’a sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0922e-149">In the **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="0922e-150">Ardından, menüden çıkmadan **NuGet Paketlerini Yönet...** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0922e-150">Then without leaving the menu, click on **Manage NuGet Packages...**.</span></span>

   ![Proje için Sağ Tıklama Menüsünün ekran görüntüsü](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="0922e-152">**NuGet** sekmesinde, pencerenin üst kısmındaki **Gözat**'a tıklayın ve arama kutusuna **azure documentdb** yazın.</span><span class="sxs-lookup"><span data-stu-id="0922e-152">In the **NuGet** tab, click **Browse** at the top of the window, and type **azure documentdb** in the search box.</span></span>
7. <span data-ttu-id="0922e-153">Sonuçlardan **Microsoft.Azure.DocumentDB.Core** seçeneğini bulup **Yükle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0922e-153">Within the results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="0922e-154">.NET Core için DocumentDB İstemci Kitaplığı’nın paket kimliği [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)’dur.</span><span class="sxs-lookup"><span data-stu-id="0922e-154">The package ID for the DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="0922e-155">Bu .NET Core NuGet paketi tarafından desteklenmeyen bir .NET Framework sürümünü (net461 gibi) hedefliyorsanız, .NET Framework 4.5’ten itibaren tüm .NET Framework sürümlerini destekleyen [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB)’yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="0922e-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="0922e-156">Komut istemlerinde, NuGet paket yüklemelerini ve lisans sözleşmesini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="0922e-156">At the prompts, accept the NuGet package installations and the license agreement.</span></span>

<span data-ttu-id="0922e-157">Harika!</span><span class="sxs-lookup"><span data-stu-id="0922e-157">Great!</span></span> <span data-ttu-id="0922e-158">Kurulumu tamamladığımıza göre, biraz kod yazmaya başlayalım.</span><span class="sxs-lookup"><span data-stu-id="0922e-158">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="0922e-159">Bu öğreticinin tamamlanmış kod projesini [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started)'da bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0922e-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="0922e-160"><a id="Connect"></a>3. Adım: Azure Cosmos DB hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="0922e-160"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="0922e-161">İlk olarak, Program.cs dosyasında C# uygulamanızın başlangıcına bu başvuruları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0922e-161">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART TO YOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="0922e-162">Bu öğreticiyi tamamlamak için, yukarıdaki bağımlılıkları eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="0922e-162">In order to complete this tutorial, make sure you add the dependencies above.</span></span>

<span data-ttu-id="0922e-163">Şimdi bu iki sabiti ve *client* değişkeninizi *Program* ortak sınıfının altına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0922e-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART TO YOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="0922e-164">Ardından, URI ve birincil anahtarınızı almak için [Azure Portal](https://portal.azure.com)'a gidin.</span><span class="sxs-lookup"><span data-stu-id="0922e-164">Next, head to the [Azure Portal](https://portal.azure.com) to retrieve your URI and primary key.</span></span> <span data-ttu-id="0922e-165">Azure Cosmos DB URI ve birincil anahtar, uygulamanızın nereye bağlanacağını anlamak ve Azure Cosmos DB uygulamanızın bağlantısına güvenmesi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0922e-165">The Azure Cosmos DB URI and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="0922e-166">Azure Portal'da Azure Cosmos DB hesabınıza gidin ve ardından **Anahtarlar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0922e-166">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="0922e-167">Portaldaki URI’yi kopyalayın ve program.cs dosyasındaki `<your endpoint URI>` içine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-167">Copy the URI from the portal and paste it into `<your endpoint URI>` in the program.cs file.</span></span> <span data-ttu-id="0922e-168">Ardından portaldan BİRİNCİL ANAHTARI kopyalayın ve `<your key>` içine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-168">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span></span> <span data-ttu-id="0922e-169">Azure Cosmos DB Öykünücüsü’nü kullanıyorsanız uç nokta olarak `https://localhost:8081` değerini ve [Azure Cosmos DB Öykünücüsü’nü kullanarak geliştirme](local-emulator.md) bölümünden elde edilen iyi tanımlanmış yetkilendirme anahtarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="0922e-169">If you are using the Azure Cosmos DB Emulator, use `https://localhost:8081` as the endpoint, and the well-defined authorization key from [How to develop using the Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="0922e-170">< ve > işaretini kaldırdığınızdan, ancak uç noktası ve anahtarın başı ile sonundaki çift tırnağı bıraktığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0922e-170">Make sure to remove the < and > but leave the double quotes around your endpoint and key.</span></span>

![Bir C# konsol uygulaması oluşturmak için NoSQL öğreticisi tarafından kullanılan Azure Portal'ın ekran görüntüsü][keys]

<span data-ttu-id="0922e-173">**DocumentClient**'ın yeni bir örneğini oluşturarak başlarken uygulamasına başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="0922e-173">We'll start the getting started application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="0922e-174">**Main** yönteminin altına yeni **DocumentClient**'ımızın örneğini oluşturacak **GetStartedDemo** adlı bu zaman uyumsuz yeni görevi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0922e-174">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART TO YOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="0922e-175">Zaman uyumsuz görevinizi **Main** yönteminizden çalıştırmak için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0922e-175">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="0922e-176">**Main** yöntemi özel durumları yakalar ve bunları konsola yazar.</span><span class="sxs-lookup"><span data-stu-id="0922e-176">The **Main** method will catch exceptions and write them to the console.</span></span>

```csharp
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
```

<span data-ttu-id="0922e-177">Uygulamayı derlemek ve çalıştırmak için **DocumentDBGettingStarted** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="0922e-177">Press the **DocumentDBGettingStarted** button to build and run the application.</span></span>

<span data-ttu-id="0922e-178">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="0922e-178">Congratulations!</span></span> <span data-ttu-id="0922e-179">Bir Azure Cosmos DB hesabına başarıyla bağlandınız, şimdi Azure Cosmos DB kaynaklarıyla çalışmaya bakalım.</span><span class="sxs-lookup"><span data-stu-id="0922e-179">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="0922e-180">4. Adım: Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0922e-180">Step 4: Create a database</span></span>
<span data-ttu-id="0922e-181">Bir veritabanı oluşturmak için kodu eklemeden önce, konsola yazma için bir yardımcı yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0922e-181">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="0922e-182">**WriteToConsoleAndPromptToContinue** yöntemini kopyalayın ve **GetStartedDemo** yönteminin altına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-182">Copy and paste the **WriteToConsoleAndPromptToContinue** method underneath the **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="0922e-183">Azure Cosmos DB [veritabanı](documentdb-resources.md#databases) kullanılarak oluşturulan [Documentclient](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) yöntemi **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="0922e-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="0922e-184">Veritabanı, koleksiyonlar genelinde bölümlenmiş JSON belgesi depolama alanının mantıksal bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="0922e-184">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="0922e-185">Aşağıdaki kodu kopyalayın ve istemci oluşturmanın altında **GetStartedDemo** yönteminize yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-185">Copy and paste the following code to your **GetStartedDemo** method underneath the client creation.</span></span> <span data-ttu-id="0922e-186">Bu, *FamilyDB* adlı bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0922e-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="0922e-187">Uygulamanızı çalıştırmak için **DocumentDBGettingStarted** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="0922e-187">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="0922e-188">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="0922e-188">Congratulations!</span></span> <span data-ttu-id="0922e-189">Başarılı bir şekilde bir Azure Cosmos DB veritabanı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="0922e-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="0922e-190"><a id="CreateColl"></a>5. Adım: Koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="0922e-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="0922e-191">**CreateDocumentCollectionAsync**, ayrılmış işleme ile yeni bir koleksiyon oluşturur, bu da ücret ödenmesini gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="0922e-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="0922e-192">Daha ayrıntılı bilgi için lütfen [fiyatlandırma sayfamızı](https://azure.microsoft.com/pricing/details/cosmos-db/) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="0922e-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="0922e-193">Bir [koleksiyon](documentdb-resources.md#collections), **DocumentClient** sınıfının [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) yöntemi kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="0922e-193">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="0922e-194">Koleksiyon, JSON belgelerinin ve ilişkili JavaScript uygulama mantığının bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="0922e-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="0922e-195">Aşağıdaki kodu kopyalayın ve veritabanı oluşturmanın altında **GetStartedDemo** yönteminize yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-195">Copy and paste the following code to your **GetStartedDemo** method underneath the database creation.</span></span> <span data-ttu-id="0922e-196">Bunun yapılması *FamilyCollection_oa* adlı bir belge koleksiyonu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0922e-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="0922e-197">Uygulamanızı çalıştırmak için **DocumentDBGettingStarted** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="0922e-197">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="0922e-198">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="0922e-198">Congratulations!</span></span> <span data-ttu-id="0922e-199">Başarılı bir şekilde bir Azure Cosmos DB belge koleksiyonu oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="0922e-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="0922e-200"><a id="CreateDoc"></a>6. Adım: JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="0922e-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="0922e-201">Bir [belge](documentdb-resources.md#documents), **DocumentClient** sınıfının [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) yöntemi kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="0922e-201">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="0922e-202">Belgeler, kullanıcı tanımlı (rastgele) JSON içeriğidir.</span><span class="sxs-lookup"><span data-stu-id="0922e-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="0922e-203">Şimdi bir veya daha fazla belge ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="0922e-203">We can now insert one or more documents.</span></span> <span data-ttu-id="0922e-204">Veritabanınızda depolamak istediğiniz veriler zaten varsa, Azure Cosmos veritabanı kullanabilirsiniz [veri geçiş aracı](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="0922e-204">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="0922e-205">İlk olarak, bu örnekte Azure Cosmos DB içinde depolanan nesneleri temsil edecek bir **Family** sınıfı oluşturmamız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0922e-205">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="0922e-206">**Family**'nin içinde kullanılan **Parent**, **Child**, **Pet**, **Address** alt sınıflarını da oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="0922e-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="0922e-207">Belgelerin, JSON'da **id** olarak seri hale getirilmiş bir **Id** özelliğine sahip olmaları gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0922e-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="0922e-208">Bu sınıfları oluşturmak için **GetStartedDemo** yönteminden sonra aşağıdaki iç alt sınıfları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0922e-208">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="0922e-209">**Family**, **Parent**, **Child**, **Pet** ve **Address** sınıflarını kopyalayın ve **WriteToConsoleAndPromptToContinue** yönteminin altına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-209">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath the **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
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
```

<span data-ttu-id="0922e-210">**CreateFamilyDocumentIfNotExists** yöntemini kopyalayın ve **CreateDocumentCollectionIfNotExists** yönteminizin altına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-210">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="0922e-211">Andersen Ailesi ve Wakefield Ailesi için birer tane olmak üzere iki belge yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="0922e-211">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="0922e-212">`// ADD THIS PART TO YOUR CODE` öğesinden sonraki kodu kopyalayın ve belge koleksiyonu oluşturmanın altında **GetStartedDemo** yönteminize yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-212">Copy and paste the code that follows `// ADD THIS PART TO YOUR CODE` to your **GetStartedDemo** method underneath the document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

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

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

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

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

<span data-ttu-id="0922e-213">Uygulamanızı çalıştırmak için **DocumentDBGettingStarted** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="0922e-213">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="0922e-214">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="0922e-214">Congratulations!</span></span> <span data-ttu-id="0922e-215">Başarılı bir şekilde iki Azure Cosmos DB belgesi oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="0922e-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Bir C# konsol uygulaması oluşturmak için NoSQL öğreticisi tarafından kullanılan belgeler, hesap, çevrimiçi veritabanı ve koleksiyon arasındaki hiyerarşik ilişkiyi gösteren diyagram](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="0922e-217"><a id="Query"></a>7. Adım: Azure Cosmos DB kaynaklarını sorgulama</span><span class="sxs-lookup"><span data-stu-id="0922e-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="0922e-218">Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için [zengin sorguların](documentdb-sql-query.md) gerçekleştirilmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="0922e-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="0922e-219">Aşağıdaki örnek kod, önceki adımda yerleştirdiğimiz belgelerde hem Azure Cosmos DB SQL söz dizimi hem de LINQ kullanarak çalıştırabileceğimiz çeşitli sorguları gösterir.</span><span class="sxs-lookup"><span data-stu-id="0922e-219">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="0922e-220">**ExecuteSimpleQuery** yöntemini kopyalayın ve **CreateFamilyDocumentIfNotExists** yönteminizin altına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-220">Copy and paste the **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="0922e-221">Aşağıdaki kodu kopyalayın ve ikinci belge oluşturmanın altında **GetStartedDemo** yönteminize yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-221">Copy and paste the following code to your **GetStartedDemo** method underneath the second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART TO YOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="0922e-222">Uygulamanızı çalıştırmak için **DocumentDBGettingStarted** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="0922e-222">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="0922e-223">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="0922e-223">Congratulations!</span></span> <span data-ttu-id="0922e-224">Bir Azure Cosmos DB koleksiyonunu başarıyla sorguladınız.</span><span class="sxs-lookup"><span data-stu-id="0922e-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="0922e-225">Aşağıdaki diyagram oluşturduğunuz koleksiyonda Azure Cosmos DB SQL sorgusu söz diziminin nasıl çağrıldığını gösterir, aynı mantık LINQ sorgusu için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0922e-225">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Bir C# konsol uygulaması oluşturmak için NoSQL öğreticisi tarafından kullanılan sorgunun kapsamını ve anlamını gösteren diyagram](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="0922e-227">[FROM](documentdb-sql-query.md#FromClause) Azure Cosmos DB sorguları zaten tek bir koleksiyon kapsamında olduğundan anahtar sözcüğü sorguda isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0922e-227">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="0922e-228">Bu nedenle, "FROM Families f", "FROM root r" veya seçtiğiniz herhangi bir başka değişken adıyla değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="0922e-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="0922e-229">DocumentDB; Families, root veya seçtiğiniz değişken adının varsayılan olarak geçerli koleksiyona başvurduğu sonucuna varır.</span><span class="sxs-lookup"><span data-stu-id="0922e-229">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="0922e-230"><a id="ReplaceDocument"></a>8. Adım: JSON belgesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="0922e-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="0922e-231">Azure Cosmos DB, JSON belgelerini değiştirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="0922e-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="0922e-232">**ReplaceFamilyDocument** yöntemini kopyalayın ve **ExecuteSimpleQuery** yönteminizin altına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-232">Copy and paste the **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="0922e-233">Aşağıdaki kodu kopyalayın ve sorgu yürütmenin altında **GetStartedDemo** yönteminize yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-233">Copy and paste the following code to your **GetStartedDemo** method underneath the query execution.</span></span> <span data-ttu-id="0922e-234">Belgeyi değiştirdikten sonra, aynı sorgu tekrar çalıştırılarak değiştirilen belge görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0922e-234">After replacing the document, this will run the same query again to view the changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
// Update the Grade of the Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="0922e-235">Uygulamanızı çalıştırmak için **DocumentDBGettingStarted** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="0922e-235">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="0922e-236">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="0922e-236">Congratulations!</span></span> <span data-ttu-id="0922e-237">Başarılı bir şekilde bir Azure Cosmos DB belgesini değiştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="0922e-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="0922e-238"><a id="DeleteDocument"></a>9. Adım: JSON belgesini silme</span><span class="sxs-lookup"><span data-stu-id="0922e-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="0922e-239">Azure Cosmos DB, JSON belgelerini silmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="0922e-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="0922e-240">**DeleteFamilyDocument** yöntemini kopyalayın ve **ReplaceFamilyDocument** yönteminizin altına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-240">Copy and paste the **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="0922e-241">Aşağıdaki kodu kopyalayın ve ikinci sorguyu yürütmenin altında **GetStartedDemo** yönteminize yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-241">Copy and paste the following code to your **GetStartedDemo** method underneath the second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO CODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="0922e-242">Uygulamanızı çalıştırmak için **DocumentDBGettingStarted** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="0922e-242">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="0922e-243">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="0922e-243">Congratulations!</span></span> <span data-ttu-id="0922e-244">Başarılı bir şekilde bir Azure Cosmos DB belgesini sildiniz.</span><span class="sxs-lookup"><span data-stu-id="0922e-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="0922e-245"><a id="DeleteDatabase"></a>10. Adım: Veritabanını silme</span><span class="sxs-lookup"><span data-stu-id="0922e-245"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="0922e-246">Oluşturulan veritabanı silindiğinde, veritabanı ve tüm alt kaynaklar (koleksiyonlar, belgeler vb.) kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="0922e-246">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="0922e-247">Tüm veritabanını ve tüm alt kaynaklarını silmek için aşağıdaki kodu kopyalayın ve belge silmenin altında **GetStartedDemo** yönteminize yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-247">Copy and paste the following code to your **GetStartedDemo** method underneath the document delete to delete the entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART TO CODE
// Clean up/delete the database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="0922e-248">Uygulamanızı çalıştırmak için **DocumentDBGettingStarted** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="0922e-248">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="0922e-249">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="0922e-249">Congratulations!</span></span> <span data-ttu-id="0922e-250">Başarılı bir şekilde bir Azure Cosmos DB veritabanını sildiniz.</span><span class="sxs-lookup"><span data-stu-id="0922e-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="0922e-251"><a id="Run"></a>11. Adım: C# konsol uygulamanızı hep birlikte çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="0922e-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="0922e-252">Uygulamayı hata ayıklama modunda derlemek için, Visual Studio’da **DocumentDBGettingStarted** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="0922e-252">Press the **DocumentDBGettingStarted** button in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="0922e-253">Konsol penceresinde get Başlarken uygulamanızın çıktısını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0922e-253">You should see the output of your get started app in the console window.</span></span> <span data-ttu-id="0922e-254">Çıktı, eklediğimiz sorguların sonuçlarını gösterir ve aşağıdaki örnek metinle eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="0922e-254">The output will show the results of the queries we added and should match the example text below.</span></span>

```
Created FamilyDB_oa
Press any key to continue ...
Created FamilyCollection_oa
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
```

<span data-ttu-id="0922e-255">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="0922e-255">Congratulations!</span></span> <span data-ttu-id="0922e-256">Bu öğreticiyi tamamladınız ve çalışan bir C# konsol uygulamasına sahipsiniz!</span><span class="sxs-lookup"><span data-stu-id="0922e-256">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="0922e-257"><a id="GetSolution"></a> Tam öğretici çözümünü edinin</span><span class="sxs-lookup"><span data-stu-id="0922e-257"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="0922e-258">Bu makaledeki tüm örnekleri içeren GetStarted çözümünü derlemek için aşağıdakilere ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="0922e-258">To build the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="0922e-259">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="0922e-259">An active Azure account.</span></span> <span data-ttu-id="0922e-260">Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0922e-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="0922e-261">Bir [Azure Cosmos DB hesabı][create-documentdb-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="0922e-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="0922e-262">GitHub'da bulunan [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) çözümü.</span><span class="sxs-lookup"><span data-stu-id="0922e-262">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="0922e-263">DocumentDB API başvuruları Visual Studio'daki Azure Cosmos DB .NET Core SDK geri yüklemek için sağ **GetStarted** Çözüm Gezgini ve ardından çözüm **etkinleştirmek NuGet paketi geri yüklemesi**.</span><span class="sxs-lookup"><span data-stu-id="0922e-263">To restore the references to the DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="0922e-264">Bölümünde açıklandığı gibi Program.cs dosyasında EndpointUrl ve AuthorizationKey değerlerini sonraki, güncelleştirme [Azure Cosmos DB hesabına Bağlan](#Connect).</span><span class="sxs-lookup"><span data-stu-id="0922e-264">Next, in the Program.cs file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0922e-265">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0922e-265">Next steps</span></span>
* <span data-ttu-id="0922e-266">Daha karmaşık bir ASP.NET MVC öğreticisi mi istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="0922e-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="0922e-267">Bkz: [ASP.NET MVC Öğreticisi: Web uygulaması geliştirme Azure Cosmos DB ile](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="0922e-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="0922e-268">Xamarin iOS, Android veya formlar geliştirmek istediğiniz uygulama için Azure Cosmos DB .NET Core SDK DocumentDB API kullanarak?</span><span class="sxs-lookup"><span data-stu-id="0922e-268">Want to develop a Xamarin iOS, Android, or Forms application using the DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="0922e-269">Bkz: [yapı Xamarin ve Azure Cosmos DB mobil uygulamalar](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="0922e-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="0922e-270">Azure Cosmos DB ile ölçek ve performans testi mi yapmak istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="0922e-270">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="0922e-271">Bkz: [performansı ve ölçeği Azure Cosmos DB ile test etme](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="0922e-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="0922e-272">Bilgi edinmek için nasıl [İzleyici Azure Cosmos DB istekleri, kullanım ve depolama](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="0922e-272">Learn how to [Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="0922e-273">[Query Playground](https://www.documentdb.com/sql/demo)'daki örnek veri kümelerimizde sorgular çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0922e-273">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="0922e-274">Programlama modeli hakkında daha fazla bilgi için bkz: [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="0922e-274">To learn more about the programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
