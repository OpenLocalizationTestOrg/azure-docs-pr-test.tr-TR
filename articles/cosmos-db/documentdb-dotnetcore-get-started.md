---
title: "Azure Cosmos DB: .NET Core ile DocumentDB API’si başlangıç öğreticisi | Microsoft Docs"
description: "Çevrimiçi bir veritabanı ve hello Azure Cosmos DB DocumentDB API .NET Core SDK'sını kullanarak C# konsol uygulaması oluşturan bir Öğreticisi."
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
ms.openlocfilehash: 5e7efb327252e9e73e9b2a340820eeecc6937fa5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a><span data-ttu-id="215dd-103">Azure Cosmos DB: Merhaba DocumentDB API ve .NET Core ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="215dd-103">Azure Cosmos DB: Getting started with hello DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="215dd-104">.NET</span><span class="sxs-lookup"><span data-stu-id="215dd-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="215dd-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="215dd-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="215dd-106">MongoDB için Node.js</span><span class="sxs-lookup"><span data-stu-id="215dd-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="215dd-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="215dd-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="215dd-108">Java</span><span class="sxs-lookup"><span data-stu-id="215dd-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="215dd-109">C++</span><span class="sxs-lookup"><span data-stu-id="215dd-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="215dd-110">Toohello DocumentDB API Azure Cosmos .NET Core eğitici Başlarken DB için Hoş Geldiniz!</span><span class="sxs-lookup"><span data-stu-id="215dd-110">Welcome toohello DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="215dd-111">Bu öğreticiyi uyguladıktan sonra, Azure Cosmos DB kaynaklarını oluşturan ve sorgulayan bir konsol uygulamasına sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="215dd-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="215dd-112">Şu konulara değineceğiz:</span><span class="sxs-lookup"><span data-stu-id="215dd-112">We'll cover:</span></span>

* <span data-ttu-id="215dd-113">Oluşturma ve tooan Azure Cosmos DB hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="215dd-113">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="215dd-114">Visual Studio Çözümünüzü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="215dd-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="215dd-115">Çevrimiçi bir veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="215dd-115">Creating an online database</span></span>
* <span data-ttu-id="215dd-116">Koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="215dd-116">Creating a collection</span></span>
* <span data-ttu-id="215dd-117">JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="215dd-117">Creating JSON documents</span></span>
* <span data-ttu-id="215dd-118">Merhaba koleksiyonu sorgulama</span><span class="sxs-lookup"><span data-stu-id="215dd-118">Querying hello collection</span></span>
* <span data-ttu-id="215dd-119">Bir belgeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="215dd-119">Replacing a document</span></span>
* <span data-ttu-id="215dd-120">Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="215dd-120">Deleting a document</span></span>
* <span data-ttu-id="215dd-121">Merhaba veritabanını silme</span><span class="sxs-lookup"><span data-stu-id="215dd-121">Deleting hello database</span></span>

<span data-ttu-id="215dd-122">Zamanınız yok mu?</span><span class="sxs-lookup"><span data-stu-id="215dd-122">Don't have time?</span></span> <span data-ttu-id="215dd-123">Endişelenmeyin!</span><span class="sxs-lookup"><span data-stu-id="215dd-123">Don't worry!</span></span> <span data-ttu-id="215dd-124">Merhaba eksiksiz bir çözüm edinilebilir [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="215dd-124">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="215dd-125">Toohello atlama [alma hello eksiksiz bir çözüm bölüm](#GetSolution) hızlı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="215dd-125">Jump toohello [Get hello complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="215dd-126">Xamarin iOS, Android veya formlar toobuild istediğiniz uygulamayı kullanarak hello DocumentDB API ve .NET Core SDK?</span><span class="sxs-lookup"><span data-stu-id="215dd-126">Want toobuild a Xamarin iOS, Android, or Forms application using hello DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="215dd-127">Bkz: [yapı Xamarin ve Azure Cosmos DB mobil uygulamalar](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="215dd-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="215dd-128">Bu öğreticide kullanılan Azure Cosmos DB .NET Core SDK Hello henüz Evrensel Windows Platformu (UWP) uygulamaları ile uyumlu değil.</span><span class="sxs-lookup"><span data-stu-id="215dd-128">hello Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="215dd-129">Merhaba UWP uygulamaları destekleyen .NET Core SDK Önizleme sürümü için çok e-posta Gönder[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="215dd-129">For a preview version of hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="215dd-130">Şimdi başlayalım!</span><span class="sxs-lookup"><span data-stu-id="215dd-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="215dd-131">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="215dd-131">Prerequisites</span></span>
<span data-ttu-id="215dd-132">Merhaba aşağıdaki sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="215dd-132">Please make sure you have hello following:</span></span>

* <span data-ttu-id="215dd-133">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="215dd-133">An active Azure account.</span></span> <span data-ttu-id="215dd-134">Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="215dd-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="215dd-135">Alternatif olarak, hello kullanabilirsiniz [Azure Cosmos DB öykünücüsü](local-emulator.md) Bu öğretici için.</span><span class="sxs-lookup"><span data-stu-id="215dd-135">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="215dd-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="215dd-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="215dd-137">MacOS ya da Linux üzerinde çalışıyorsanız, hello yükleyerek hello komut satırı .NET Core uygulamalardan geliştirebilirsiniz [.NET Core SDK](https://www.microsoft.com/net/core#macos) tercih ettiğiniz hello platform için.</span><span class="sxs-lookup"><span data-stu-id="215dd-137">If you're working on MacOS or Linux, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) for hello platform of your choice.</span></span> 
    * <span data-ttu-id="215dd-138">Windows üzerinde çalışıyorsanız, hello yükleyerek hello komut satırı .NET Core uygulamalardan geliştirebilirsiniz [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="215dd-138">If you're working on Windows, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="215dd-139">Kendi düzenleyicinizi kullanabilir ya da ücretsiz olan ve Windows, Linux ve MacOS’de çalışan [Visual Studio Code](https://code.visualstudio.com/)’u indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="215dd-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="215dd-140">1. Adım: Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="215dd-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="215dd-141">Bir Azure Cosmos DB hesabı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="215dd-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="215dd-142">Toouse istediğiniz bir hesap zaten varsa, şimdi çok atlayabilirsiniz[Visual Studio çözümünüzü kurma](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="215dd-142">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="215dd-143">Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) toosetup öykünücüsü hello ve İleri çok atlayabilirsiniz[Visual Studio çözümünüzü kurma](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="215dd-143">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="215dd-144"><a id="SetupVS"></a>2. Adım: Visual Studio çözümünüzü kurma</span><span class="sxs-lookup"><span data-stu-id="215dd-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="215dd-145">Bilgisayarınızda **Visual Studio 2017**'yi açın.</span><span class="sxs-lookup"><span data-stu-id="215dd-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="215dd-146">Merhaba üzerinde **dosya** menüsünde, select **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="215dd-146">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="215dd-147">Merhaba, **yeni proje** iletişim kutusunda **şablonları** / **Visual C#** / **.NET Core** / **Konsol uygulaması (.NET Core)**, projenizin adı **DocumentDBGettingStarted**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="215dd-147">In hello **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Merhaba yeni proje penceresinin ekran görüntüsü](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="215dd-149">Merhaba, **Çözüm Gezgini**, sağ tıklayın **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="215dd-149">In hello **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="215dd-150">Merhaba menüden çıkmadan tıklayın **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="215dd-150">Then without leaving hello menu, click on **Manage NuGet Packages...**.</span></span>

   ![Merhaba sağ tıklama menüsünün hello proje için ekran görüntüsü](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="215dd-152">Merhaba, **NuGet** sekmesini tıklatın, **Gözat** hello penceresi ve tür hello üstünde **azure documentdb** hello arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="215dd-152">In hello **NuGet** tab, click **Browse** at hello top of hello window, and type **azure documentdb** in hello search box.</span></span>
7. <span data-ttu-id="215dd-153">Merhaba sonuçları içinde bulmak **Microsoft.Azure.DocumentDB.Core** tıklatıp **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="215dd-153">Within hello results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="215dd-154">Merhaba DocumentDB istemci kitaplığı için .NET Core Hello paket kimliği [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="215dd-154">hello package ID for hello DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="215dd-155">Bu .NET Core NuGet paketi tarafından desteklenmeyen bir .NET Framework sürümünü (net461 gibi) hedefliyorsanız, .NET Framework 4.5’ten itibaren tüm .NET Framework sürümlerini destekleyen [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB)’yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="215dd-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="215dd-156">Merhaba istemleri hello NuGet paket yüklemeleri ve hello Lisans Sözleşmesi'ni kabul edin.</span><span class="sxs-lookup"><span data-stu-id="215dd-156">At hello prompts, accept hello NuGet package installations and hello license agreement.</span></span>

<span data-ttu-id="215dd-157">Harika!</span><span class="sxs-lookup"><span data-stu-id="215dd-157">Great!</span></span> <span data-ttu-id="215dd-158">Biz hello Kurulumu tamamladığımıza göre biraz kod yazmaya başlayalım.</span><span class="sxs-lookup"><span data-stu-id="215dd-158">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="215dd-159">Bu öğreticinin tamamlanmış kod projesini [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started)'da bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="215dd-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="215dd-160"><a id="Connect"></a>3. adım: tooan Azure Cosmos DB hesap bağlanma</span><span class="sxs-lookup"><span data-stu-id="215dd-160"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="215dd-161">İlk olarak, bunlar ekleyin başvuran C# uygulamanız, hello Program.cs dosyasındaki toohello başlangıcı:</span><span class="sxs-lookup"><span data-stu-id="215dd-161">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART tooYOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="215dd-162">İçinde Bu öğretici toocomplete sipariş, yukarıdaki hello bağımlılıkları eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="215dd-162">In order toocomplete this tutorial, make sure you add hello dependencies above.</span></span>

<span data-ttu-id="215dd-163">Şimdi bu iki sabiti ve *client* değişkeninizi *Program* ortak sınıfının altına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="215dd-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="215dd-164">Ardından, toohello head [Azure Portal](https://portal.azure.com) tooretrieve URI ve birincil anahtar.</span><span class="sxs-lookup"><span data-stu-id="215dd-164">Next, head toohello [Azure Portal](https://portal.azure.com) tooretrieve your URI and primary key.</span></span> <span data-ttu-id="215dd-165">Hello Azure Cosmos DB URI ve birincil anahtar, uygulama toounderstand için gerekli olduğu tooconnect ve Azure Cosmos DB tootrust için uygulamanızın bağlantı.</span><span class="sxs-lookup"><span data-stu-id="215dd-165">hello Azure Cosmos DB URI and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="215dd-166">İçinde Azure Portal Merhaba, tooyour Azure Cosmos DB hesap gidin ve ardından **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="215dd-166">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="215dd-167">Merhaba URI hello Portal'dan kopyalayın ve yapıştırın `<your endpoint URI>` hello program.cs dosyasındaki.</span><span class="sxs-lookup"><span data-stu-id="215dd-167">Copy hello URI from hello portal and paste it into `<your endpoint URI>` in hello program.cs file.</span></span> <span data-ttu-id="215dd-168">BİRİNCİL anahtar hello portalından hello kopyalayıp yapıştırın sonra `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="215dd-168">Then copy hello PRIMARY KEY from hello portal and paste it into `<your key>`.</span></span> <span data-ttu-id="215dd-169">Hello Azure Cosmos DB öykünücüsü kullanıyorsanız `https://localhost:8081` hello uç noktası ve hello iyi tanımlanmış yetkilendirme anahtarından olarak [nasıl toodevelop kullanarak izin ver hello Azure Cosmos DB öykünücüsü](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="215dd-169">If you are using hello Azure Cosmos DB Emulator, use `https://localhost:8081` as hello endpoint, and hello well-defined authorization key from [How toodevelop using hello Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="215dd-170">Tooremove hello emin olun < ve > ancak uç noktasını ve anahtarı çift tırnak hello bırakın.</span><span class="sxs-lookup"><span data-stu-id="215dd-170">Make sure tooremove hello < and > but leave hello double quotes around your endpoint and key.</span></span>

![Merhaba hello NoSQL Öğreticisi toocreate C# konsol uygulaması tarafından kullanılan Azure Portal ekran görüntüsü.][keys]

<span data-ttu-id="215dd-173">Merhaba Başlarken uygulamasına hello yeni bir örneğini oluşturarak başlayacağız **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="215dd-173">We'll start hello getting started application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="215dd-174">Merhaba aşağıda **ana** yöntemi adlı bu zaman uyumsuz yeni görevi ekleyin **GetStartedDemo**, örneğini oluşturacak, yeni **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="215dd-174">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART tooYOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="215dd-175">Zaman uyumsuz görevinizi Hello aşağıdaki kod toorun eklemek, **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="215dd-175">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="215dd-176">Merhaba **ana** yöntemi özel durumları yakalar ve bunları toohello konsol yazar.</span><span class="sxs-lookup"><span data-stu-id="215dd-176">hello **Main** method will catch exceptions and write them toohello console.</span></span>

```csharp
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
```

<span data-ttu-id="215dd-177">Tuşuna hello **DocumentDBGettingStarted** düğmesini toobuild ve hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="215dd-177">Press hello **DocumentDBGettingStarted** button toobuild and run hello application.</span></span>

<span data-ttu-id="215dd-178">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="215dd-178">Congratulations!</span></span> <span data-ttu-id="215dd-179">Başarılı bir şekilde bağlı tooan Azure Cosmos DB hesap, artık Azure Cosmos DB kaynaklarla çalışmak bir bakalım.</span><span class="sxs-lookup"><span data-stu-id="215dd-179">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="215dd-180">4. Adım: Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="215dd-180">Step 4: Create a database</span></span>
<span data-ttu-id="215dd-181">Bir veritabanı oluşturmak için hello kodu eklemeden önce toohello konsol yazmak için bir yardımcı yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="215dd-181">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="215dd-182">Kopyalama ve yapıştırma hello **WriteToConsoleAndPromptToContinue** hello yöntemini **GetStartedDemo** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="215dd-182">Copy and paste hello **WriteToConsoleAndPromptToContinue** method underneath hello **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="215dd-183">Azure Cosmos DB [veritabanı](documentdb-resources.md#databases) hello kullanarak oluşturulan [Documentclient](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) hello yöntemi **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="215dd-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="215dd-184">Bir veritabanı hello mantıksal, koleksiyonlar genelinde bölümlenmiş JSON belgesi depolama kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="215dd-184">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="215dd-185">Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello istemci oluşturmanın altında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="215dd-185">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello client creation.</span></span> <span data-ttu-id="215dd-186">Bu, *FamilyDB* adlı bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="215dd-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="215dd-187">Tuşuna hello **DocumentDBGettingStarted** toorun uygulamanızı düğmesi.</span><span class="sxs-lookup"><span data-stu-id="215dd-187">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="215dd-188">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="215dd-188">Congratulations!</span></span> <span data-ttu-id="215dd-189">Başarılı bir şekilde bir Azure Cosmos DB veritabanı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="215dd-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="215dd-190"><a id="CreateColl"></a>5. Adım: Koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="215dd-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="215dd-191">**CreateDocumentCollectionAsync**, ayrılmış işleme ile yeni bir koleksiyon oluşturur, bu da ücret ödenmesini gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="215dd-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="215dd-192">Daha ayrıntılı bilgi için lütfen [fiyatlandırma sayfamızı](https://azure.microsoft.com/pricing/details/cosmos-db/) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="215dd-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="215dd-193">A [koleksiyonu](documentdb-resources.md#collections) hello kullanarak oluşturulan [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) hello yöntemi **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="215dd-193">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="215dd-194">Koleksiyon, JSON belgelerinin ve ilişkili JavaScript uygulama mantığının bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="215dd-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="215dd-195">Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello veritabanı oluşturmanın altında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="215dd-195">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello database creation.</span></span> <span data-ttu-id="215dd-196">Bunun yapılması *FamilyCollection_oa* adlı bir belge koleksiyonu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="215dd-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="215dd-197">Tuşuna hello **DocumentDBGettingStarted** toorun uygulamanızı düğmesi.</span><span class="sxs-lookup"><span data-stu-id="215dd-197">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="215dd-198">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="215dd-198">Congratulations!</span></span> <span data-ttu-id="215dd-199">Başarılı bir şekilde bir Azure Cosmos DB belge koleksiyonu oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="215dd-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="215dd-200"><a id="CreateDoc"></a>6. Adım: JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="215dd-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="215dd-201">A [belge](documentdb-resources.md#documents) hello kullanarak oluşturulan [Documentclient](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) hello yöntemi **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="215dd-201">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="215dd-202">Belgeler, kullanıcı tanımlı (rastgele) JSON içeriğidir.</span><span class="sxs-lookup"><span data-stu-id="215dd-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="215dd-203">Şimdi bir veya daha fazla belge ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="215dd-203">We can now insert one or more documents.</span></span> <span data-ttu-id="215dd-204">İstediğiniz toostore veritabanınızda veriler zaten varsa, Azure Cosmos veritabanı kullanabilirsiniz [veri geçiş aracı](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="215dd-204">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="215dd-205">İlk olarak, toocreate ihtiyacımız bir **ailesi** Bu örnekte Azure Cosmos DB içinde depolanan nesneleri temsil edecek sınıfı.</span><span class="sxs-lookup"><span data-stu-id="215dd-205">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="215dd-206">**Family**'nin içinde kullanılan **Parent**, **Child**, **Pet**, **Address** alt sınıflarını da oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="215dd-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="215dd-207">Belgelerin, JSON'da **id** olarak seri hale getirilmiş bir **Id** özelliğine sahip olmaları gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="215dd-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="215dd-208">İç alt sınıfları hello sonra aşağıdaki hello ekleyerek bu sınıfları oluşturmak **GetStartedDemo** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="215dd-208">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="215dd-209">Kopyalama ve yapıştırma hello **ailesi**, **üst**, **alt**, **evcil hayvan**, ve **adresi** sınıflarını Merhaba **WriteToConsoleAndPromptToContinue** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="215dd-209">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath hello **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
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
```

<span data-ttu-id="215dd-210">Kopyalama ve yapıştırma hello **Createfamilydocumentıfnotexists** yöntemini, **Createdocumentcollectionıfnotexists** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="215dd-210">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="215dd-211">Ve iki belge, her biri için hello Andersen ailesi ve Wakefield ailesi hello ekleme.</span><span class="sxs-lookup"><span data-stu-id="215dd-211">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="215dd-212">İzleyen hello kodu kopyalayıp yapıştırın `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** hello belge koleksiyonu oluşturmanın altında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="215dd-212">Copy and paste hello code that follows `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** method underneath hello document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

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

<span data-ttu-id="215dd-213">Tuşuna hello **DocumentDBGettingStarted** toorun uygulamanızı düğmesi.</span><span class="sxs-lookup"><span data-stu-id="215dd-213">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="215dd-214">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="215dd-214">Congratulations!</span></span> <span data-ttu-id="215dd-215">Başarılı bir şekilde iki Azure Cosmos DB belgesi oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="215dd-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Gösteren hello hello hesabı, hello çevrimiçi veritabanı, hello koleksiyon arasındaki hiyerarşik ilişkiyi Diyagram ve C# konsol uygulaması hello NoSQL Öğreticisi toocreate tarafından kullanılan hello belgeler](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="215dd-217"><a id="Query"></a>7. Adım: Azure Cosmos DB kaynaklarını sorgulama</span><span class="sxs-lookup"><span data-stu-id="215dd-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="215dd-218">Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için [zengin sorguların](documentdb-sql-query.md) gerçekleştirilmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="215dd-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="215dd-219">Merhaba aşağıdaki örnek kod çeşitli sorgularını gösterir - hem Azure Cosmos DB SQL kullanarak, sözdizimi ve bunun yanı sıra karşı çalıştırabilirsiniz LINQ - biz hello önceki adımda eklenen belgelerde hello.</span><span class="sxs-lookup"><span data-stu-id="215dd-219">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="215dd-220">Kopyalama ve yapıştırma hello **ExecuteSimpleQuery** yöntemini, **Createfamilydocumentıfnotexists** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="215dd-220">Copy and paste hello **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="215dd-221">Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello ikinci belge oluşturmanın altında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="215dd-221">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="215dd-222">Tuşuna hello **DocumentDBGettingStarted** toorun uygulamanızı düğmesi.</span><span class="sxs-lookup"><span data-stu-id="215dd-222">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="215dd-223">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="215dd-223">Congratulations!</span></span> <span data-ttu-id="215dd-224">Bir Azure Cosmos DB koleksiyonunu başarıyla sorguladınız.</span><span class="sxs-lookup"><span data-stu-id="215dd-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="215dd-225">Merhaba Aşağıdaki diyagram hello Azure Cosmos DB SQL sorgusu söz dizimi karşı hello koleksiyonu olarak adlandırılır, nasıl oluşturulacağını gösterir ve hello aynı mantığı uygular de toohello LINQ sorgusu.</span><span class="sxs-lookup"><span data-stu-id="215dd-225">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Merhaba kapsamını ve hello sorgunun anlamını diyagramı bir C# konsol uygulaması hello NoSQL Öğreticisi toocreate tarafından kullanılan](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="215dd-227">Merhaba [FROM](documentdb-sql-query.md#FromClause) Azure Cosmos DB sorguları kapsamlı tooa tek koleksiyon zaten olduğu için anahtar sözcüğü hello sorguda isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="215dd-227">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="215dd-228">Bu nedenle, "FROM Families f", "FROM root r" veya seçtiğiniz herhangi bir başka değişken adıyla değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="215dd-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="215dd-229">DocumentDB aileleri, kök veya hello değişken adı, seçtiğiniz, başvuru hello geçerli koleksiyonu varsayılan olarak Infer.</span><span class="sxs-lookup"><span data-stu-id="215dd-229">DocumentDB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="215dd-230"><a id="ReplaceDocument"></a>8. Adım: JSON belgesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="215dd-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="215dd-231">Azure Cosmos DB, JSON belgelerini değiştirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="215dd-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="215dd-232">Kopyalama ve yapıştırma hello **ReplaceFamilyDocument** yöntemini, **ExecuteSimpleQuery** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="215dd-232">Copy and paste hello **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="215dd-233">Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello sorgu yürütmenin altında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="215dd-233">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello query execution.</span></span> <span data-ttu-id="215dd-234">Merhaba belgeyi değiştirdikten sonra bu hello çalıştıracaktır aynı tooview değiştirilen hello belgeyi yeniden sorgula.</span><span class="sxs-lookup"><span data-stu-id="215dd-234">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="215dd-235">Tuşuna hello **DocumentDBGettingStarted** toorun uygulamanızı düğmesi.</span><span class="sxs-lookup"><span data-stu-id="215dd-235">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="215dd-236">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="215dd-236">Congratulations!</span></span> <span data-ttu-id="215dd-237">Başarılı bir şekilde bir Azure Cosmos DB belgesini değiştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="215dd-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="215dd-238"><a id="DeleteDocument"></a>9. Adım: JSON belgesini silme</span><span class="sxs-lookup"><span data-stu-id="215dd-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="215dd-239">Azure Cosmos DB, JSON belgelerini silmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="215dd-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="215dd-240">Kopyalama ve yapıştırma hello **DeleteFamilyDocument** yöntemini, **ReplaceFamilyDocument** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="215dd-240">Copy and paste hello **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="215dd-241">Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello ikinci sorguyu yürütmenin altında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="215dd-241">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="215dd-242">Tuşuna hello **DocumentDBGettingStarted** toorun uygulamanızı düğmesi.</span><span class="sxs-lookup"><span data-stu-id="215dd-242">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="215dd-243">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="215dd-243">Congratulations!</span></span> <span data-ttu-id="215dd-244">Başarılı bir şekilde bir Azure Cosmos DB belgesini sildiniz.</span><span class="sxs-lookup"><span data-stu-id="215dd-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="215dd-245"><a id="DeleteDatabase"></a>10. adım: hello veritabanını silme</span><span class="sxs-lookup"><span data-stu-id="215dd-245"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="215dd-246">Veritabanı oluşturulan silme hello hello veritabanı ve tüm alt kaynaklar (koleksiyonlar, belgeler, vb.) kaldırır.</span><span class="sxs-lookup"><span data-stu-id="215dd-246">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="215dd-247">Kopyala ve Yapıştır hello aşağıdaki kod tooyour **GetStartedDemo** hello belge yöntemini toodelete hello tüm veritabanını ve tüm alt kaynaklarını silin.</span><span class="sxs-lookup"><span data-stu-id="215dd-247">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello document delete toodelete hello entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="215dd-248">Tuşuna hello **DocumentDBGettingStarted** toorun uygulamanızı düğmesi.</span><span class="sxs-lookup"><span data-stu-id="215dd-248">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="215dd-249">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="215dd-249">Congratulations!</span></span> <span data-ttu-id="215dd-250">Başarılı bir şekilde bir Azure Cosmos DB veritabanını sildiniz.</span><span class="sxs-lookup"><span data-stu-id="215dd-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="215dd-251"><a id="Run"></a>11. Adım: C# konsol uygulamanızı hep birlikte çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="215dd-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="215dd-252">Tuşuna hello **DocumentDBGettingStarted** Visual Studio toobuild hello uygulamasında hata ayıklama modunda düğmesi.</span><span class="sxs-lookup"><span data-stu-id="215dd-252">Press hello **DocumentDBGettingStarted** button in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="215dd-253">Başlarken uygulamanızın hello konsol penceresinde hello çıktısını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="215dd-253">You should see hello output of your get started app in hello console window.</span></span> <span data-ttu-id="215dd-254">Merhaba çıktı hello hello sonuçlarını gösterir eklenir ve hello örnek metinle eşleşmelidir sorgular.</span><span class="sxs-lookup"><span data-stu-id="215dd-254">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

```
Created FamilyDB_oa
Press any key toocontinue ...
Created FamilyCollection_oa
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
```

<span data-ttu-id="215dd-255">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="215dd-255">Congratulations!</span></span> <span data-ttu-id="215dd-256">Merhaba öğreticisini tamamladınız ve çalışma C# konsol uygulaması sahip!</span><span class="sxs-lookup"><span data-stu-id="215dd-256">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="215dd-257"><a id="GetSolution"></a>Merhaba tam Öğreticisi çözümünü edinme</span><span class="sxs-lookup"><span data-stu-id="215dd-257"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="215dd-258">Bu makaledeki tüm hello örnekleri içeren toobuild hello GetStarted çözümünü hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="215dd-258">toobuild hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="215dd-259">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="215dd-259">An active Azure account.</span></span> <span data-ttu-id="215dd-260">Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="215dd-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="215dd-261">Bir [Azure Cosmos DB hesabı][create-documentdb-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="215dd-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="215dd-262">Merhaba [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) çözüm Github'da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="215dd-262">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="215dd-263">toorestore hello başvuruları toohello Visual Studio'da Azure Cosmos DB .NET Core SDK için DocumentDB API sağ hello **GetStarted** Çözüm Gezgini ve ardından çözüm **etkinleştirmek NuGet paketi geri yüklemesi**.</span><span class="sxs-lookup"><span data-stu-id="215dd-263">toorestore hello references toohello DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="215dd-264">Ardından, hello Program.cs dosyasında açıklandığı gibi hello EndpointUrl ve AuthorizationKey değerlerini güncelleştirin [tooan Azure Cosmos DB hesabını bağlaması](#Connect).</span><span class="sxs-lookup"><span data-stu-id="215dd-264">Next, in hello Program.cs file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="215dd-265">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="215dd-265">Next steps</span></span>
* <span data-ttu-id="215dd-266">Daha karmaşık bir ASP.NET MVC öğreticisi mi istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="215dd-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="215dd-267">Bkz: [ASP.NET MVC Öğreticisi: Web uygulaması geliştirme Azure Cosmos DB ile](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="215dd-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="215dd-268">Xamarin iOS, Android veya formlar toodevelop istediğiniz için Azure Cosmos DB .NET Core SDK hello DocumentDB API uygulaması kullanılarak?</span><span class="sxs-lookup"><span data-stu-id="215dd-268">Want toodevelop a Xamarin iOS, Android, or Forms application using hello DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="215dd-269">Bkz: [yapı Xamarin ve Azure Cosmos DB mobil uygulamalar](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="215dd-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="215dd-270">Tooperform ölçek ve performans ile Azure Cosmos DB istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="215dd-270">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="215dd-271">Bkz: [performansı ve ölçeği Azure Cosmos DB ile test etme](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="215dd-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="215dd-272">Nasıl çok öğrenin[İzleyici Azure Cosmos DB istekleri, kullanım ve depolama](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="215dd-272">Learn how too[Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="215dd-273">Merhaba, örnek veri kümelerimizde sorgular çalıştırın [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="215dd-273">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="215dd-274">toolearn hello programlama modeli hakkında daha fazla bilgi görmek [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="215dd-274">toolearn more about hello programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
