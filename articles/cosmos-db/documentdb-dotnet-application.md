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
# <span data-ttu-id="20cdb-105"><a name="_Toc395809351"></a>ASP.NET MVC Öğreticisi: Azure Cosmos DB ile Web uygulaması geliştirme</span><span class="sxs-lookup"><span data-stu-id="20cdb-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="20cdb-106">.NET</span><span class="sxs-lookup"><span data-stu-id="20cdb-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="20cdb-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="20cdb-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="20cdb-108">Java</span><span class="sxs-lookup"><span data-stu-id="20cdb-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="20cdb-109">Python</span><span class="sxs-lookup"><span data-stu-id="20cdb-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="20cdb-110">toohighlight nasıl verimli bir şekilde Azure Cosmos DB toostore yararlanır ve JSON belgelerini sorgulamak bu makalede nasıl gösteren bir uçtan uca kılavuz sağlar toobuild Azure Cosmos DB kullanarak bir Yapılacaklar uygulamasının.</span><span class="sxs-lookup"><span data-stu-id="20cdb-110">toohighlight how you can efficiently leverage Azure Cosmos DB toostore and query JSON documents, this article provides an end-to-end walk-through showing you how toobuild a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="20cdb-111">Merhaba görevleri Azure Cosmos DB JSON belgeleri olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="20cdb-111">hello tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Merhaba Yapılacaklar listesi MVC web uygulaması Bu öğretici - adım adım Asp.net MVC Öğreticisi tarafından oluşturulan ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="20cdb-113">Bu kılavuz size nasıl toouse hello Azure Cosmos DB hizmeti toostore ve erişim verilerini Azure üzerinde barındırılan bir ASP.NET MVC web uygulamasından gösterir.</span><span class="sxs-lookup"><span data-stu-id="20cdb-113">This walk-through shows you how toouse hello Azure Cosmos DB service toostore and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="20cdb-114">Yalnızca Azure Cosmos DB odaklanan bir öğretici arıyorsanız ve hello ASP.NET MVC bileşenleri görmezsiniz [bir Azure Cosmos DB C# konsol uygulaması oluşturma](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="20cdb-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not hello ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="20cdb-115">Bu öğretici, ASP.NET MVC ve Azure Web Siteleri'ni kullanma konusunda deneyim sahibi olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="20cdb-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="20cdb-116">Yeni tooASP.NET veya hello ise [önkoşul araçlarında](#_Toc395637760), hello konumundan örnek projenin tamamını indirme öneririz [GitHub] [ GitHub] hello yönergeleri izleyerek Bu örnek.</span><span class="sxs-lookup"><span data-stu-id="20cdb-116">If you are new tooASP.NET or hello [prerequisite tools](#_Toc395637760), we recommend downloading hello complete sample project from [GitHub][GitHub] and following hello instructions in this sample.</span></span> <span data-ttu-id="20cdb-117">Oluşturduktan sonra bu makale toogain Insight hello proje hello bağlamında hello kodu gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20cdb-117">Once you have it built, you can review this article toogain insight on hello code in hello context of hello project.</span></span>
> 
> 

## <span data-ttu-id="20cdb-118"><a name="_Toc395637760"></a>Bu veritabanı öğreticisi için önkoşullar</span><span class="sxs-lookup"><span data-stu-id="20cdb-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="20cdb-119">Bu makaledeki Hello yönergeleri izlemeden önce hello aşağıdaki sahip olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="20cdb-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="20cdb-120">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="20cdb-120">An active Azure account.</span></span> <span data-ttu-id="20cdb-121">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20cdb-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="20cdb-122">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="20cdb-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="20cdb-123">OR</span><span class="sxs-lookup"><span data-stu-id="20cdb-123">OR</span></span>

    <span data-ttu-id="20cdb-124">Merhaba yerel yüklemesi [Azure Cosmos DB öykünücüsü](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="20cdb-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="20cdb-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="20cdb-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="20cdb-126">Visual Studio 2017, Visual Studio yükleyicisi hello kullanılabilen .NET için Microsoft Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="20cdb-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through hello Visual Studio Installer.</span></span>

<span data-ttu-id="20cdb-127">Tüm hello ekran görüntüleri bu makalede Microsoft Visual Studio Community 2017 kullanılarak alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="20cdb-127">All hello screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="20cdb-128">Sisteminiz farklı bir sürüme sahip yapılandırılmışsa ekranlarınızın ve seçeneklerinizin tamamen eşleşmeme olasılığı, ancak hello yukarıdaki Önkoşullar karşılıyorsa bu çözümün çalışması gerekir mümkündür.</span><span class="sxs-lookup"><span data-stu-id="20cdb-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet hello above prerequisites this solution should work.</span></span>

## <span data-ttu-id="20cdb-129"><a name="_Toc395637761"></a>1. Adım: Azure Cosmos DB veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="20cdb-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="20cdb-130">İlk olarak bir Azure Cosmos DB hesabı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="20cdb-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="20cdb-131">Zaten bir SQL (DocumentDB) hesabı için Azure Cosmos DB veya kullanıyorsanız bu öğretici için Azure Cosmos DB öykünücüsü Merhaba, çok atlayabilirsiniz[yeni bir ASP.NET MVC uygulaması oluşturma](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="20cdb-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="20cdb-132">Biz şimdi nasıl toocreate hello yeni bir ASP.NET MVC uygulamasından başından başlayarak yukarı aracılığıyla yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="20cdb-132">We will now walk through how toocreate a new ASP.NET MVC application from hello ground-up.</span></span> 

## <span data-ttu-id="20cdb-133"><a name="_Toc395637762"></a>2. Adım: Yeni bir ASP.NET MVC uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="20cdb-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="20cdb-134">Visual Studio'da, hello **dosya** menüsünde çok noktası**yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-134">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span> <span data-ttu-id="20cdb-135">Merhaba **yeni proje** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="20cdb-135">hello **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="20cdb-136">Merhaba, **proje türleri** bölmesini genişletin **şablonları**, **Visual C#**, **Web**ve ardından **ASP.NET Web uygulaması** .</span><span class="sxs-lookup"><span data-stu-id="20cdb-136">In hello **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Merhaba yeni proje iletişim kutusu ile Merhaba ASP.NET Web uygulaması proje türü vurgulanmış ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="20cdb-138">Merhaba, **adı** kutusu, hello projesinin türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="20cdb-138">In hello **Name** box, type hello name of hello project.</span></span> <span data-ttu-id="20cdb-139">Bu öğretici "todo" Merhaba adını kullanır.</span><span class="sxs-lookup"><span data-stu-id="20cdb-139">This tutorial uses hello name "todo".</span></span> <span data-ttu-id="20cdb-140">Bunun dışında bir şey toouse seçerseniz, Bu öğretici hello todo ad alanıyla ilgili ettiği her yerde sonra tooadjust hello sağlanan kod örnekleri toouse uygulamanızı adlı yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="20cdb-140">If you choose toouse something other than this, then wherever this tutorial talks about hello todo namespace, you need tooadjust hello provided code samples toouse whatever you named your application.</span></span> 
4. <span data-ttu-id="20cdb-141">Tıklatın **Gözat** Burada, gibi toocreate hello proje ve ardından toonavigate toohello klasörü **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-141">Click **Browse** toonavigate toohello folder where you would like toocreate hello project, and then click **OK**.</span></span>
   
      <span data-ttu-id="20cdb-142">Merhaba **yeni ASP.NET Web uygulaması** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="20cdb-142">hello **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Merhaba MVC uygulama şablonu vurgulanmış ile Merhaba yeni ASP.NET Web uygulaması iletişim kutusu ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="20cdb-144">Merhaba Şablonlar bölmesinde seçin **MVC**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-144">In hello templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="20cdb-145">Tıklatın **Tamam** ve Visual Studio yapı iskelesi hello boş ASP.NET MVC şablonu çevresinde oluşturmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20cdb-145">Click **OK** and let Visual Studio do its thing around scaffolding hello empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="20cdb-146">Visual Studio hello Demirbaş MVC uygulamasını oluşturmayı tamamlandıktan sonra yerel olarak çalıştırabileceğiniz boş bir ASP.NET uygulamasına sahip.</span><span class="sxs-lookup"><span data-stu-id="20cdb-146">Once Visual Studio has finished creating hello boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="20cdb-147">Yerel olarak biz olduğunuz tüm görülen hello ASP.NET "Hello World" emin olduğum için çalışan hello proje atlayın uygulama.</span><span class="sxs-lookup"><span data-stu-id="20cdb-147">We'll skip running hello project locally because I'm sure we've all seen hello ASP.NET "Hello World" application.</span></span> <span data-ttu-id="20cdb-148">Düz tooadding Azure Cosmos DB toothis proje ve uygulamamızı oluşturmaya edelim.</span><span class="sxs-lookup"><span data-stu-id="20cdb-148">Let's go straight tooadding Azure Cosmos DB toothis project and building our application.</span></span>

## <span data-ttu-id="20cdb-149"><a name="_Toc395637767"></a>3. adım: Azure Cosmos DB tooyour MVC web uygulaması projesi ekleme</span><span class="sxs-lookup"><span data-stu-id="20cdb-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB tooyour MVC web application project</span></span>
<span data-ttu-id="20cdb-150">Biz bu çözüm için ihtiyacımız hello ASP.NET MVC tesisat çoğunu sahip olduğunuza göre şimdi Azure Cosmos DB tooour MVC web uygulaması ekleme, bu öğreticinin asıl amacı toohello alın.</span><span class="sxs-lookup"><span data-stu-id="20cdb-150">Now that we have most of hello ASP.NET MVC plumbing that we need for this solution, let's get toohello real purpose of this tutorial, adding Azure Cosmos DB tooour MVC web application.</span></span>

1. <span data-ttu-id="20cdb-151">Hello Azure Cosmos DB .NET SDK'sını paketlenir ve bir NuGet paketi olarak dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="20cdb-151">hello Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="20cdb-152">tooget Visual Studio'da NuGet paketi Merhaba, hello projeye sağ tıklayarak Visual Studio'daki hello NuGet paket yöneticisini kullanın **Çözüm Gezgini** ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-152">tooget hello NuGet package in Visual Studio, use hello NuGet package manager in Visual Studio by right-clicking on hello project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Merhaba ekran görüntüsü seçenekler NuGet paketlerini Yönet vurgulanmış ile Çözüm Gezgini'nde başlangıç web uygulaması projesi için sağ tıklatın.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="20cdb-154">Merhaba **NuGet paketlerini Yönet** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="20cdb-154">hello **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="20cdb-155">Merhaba NuGet içinde **Gözat** kutusuna ***Azure DocumentDB***.</span><span class="sxs-lookup"><span data-stu-id="20cdb-155">In hello NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="20cdb-156">(Merhaba paket adı güncelleştirilmiş tooAzure Cosmos DB yedeklenmedi.)</span><span class="sxs-lookup"><span data-stu-id="20cdb-156">(hello package name has not been updated tooAzure Cosmos DB.)</span></span>
   
    <span data-ttu-id="20cdb-157">Merhaba sonuçlarından hello yüklemek **Microsoft.Azure.DocumentDB Microsoft tarafından** paket.</span><span class="sxs-lookup"><span data-stu-id="20cdb-157">From hello results, install hello **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="20cdb-158">Bu, indirin ve Newtonsoft.Json gibi tüm bağımlılıkları yanı sıra hello Azure Cosmos DB paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="20cdb-158">This will download and install hello Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="20cdb-159">' I tıklatın **Tamam** hello içinde **Önizleme** penceresinde ve **kabul ediyorum** hello içinde **lisans kabulünü** penceresi toocomplete hello yükleme.</span><span class="sxs-lookup"><span data-stu-id="20cdb-159">Click **OK** in hello **Preview** window, and **I Accept** in hello **License Acceptance** window toocomplete hello install.</span></span>
   
    ![Microsoft Azure DocumentDB istemci kitaplığı vurgulanmış hello ile Merhaba NuGet paketlerini Yönet penceresinin ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="20cdb-161">Alternatif olarak, Paket Yöneticisi konsolu tooinstall hello paket hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20cdb-161">Alternatively you can use hello Package Manager Console tooinstall hello package.</span></span> <span data-ttu-id="20cdb-162">toodo şekilde, hello **Araçları** menüsünde tıklatın **NuGet Paket Yöneticisi**ve ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-162">toodo so, on hello **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="20cdb-163">Merhaba isteminde hello aşağıdakini yazın.</span><span class="sxs-lookup"><span data-stu-id="20cdb-163">At hello prompt, type hello following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="20cdb-164">Merhaba paket yüklendikten sonra Visual Studio çözümünüzü eklenen, iki yeni başvuru Microsoft.Azure.Documents.Client ve Newtonsoft.Json hello aşağıdakilerle benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="20cdb-164">Once hello package is installed, your Visual Studio solution should resemble hello following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Merhaba iki başvurunun ekran görüntüsü, Çözüm Gezgini'nde toohello JSON veri projesine eklendi](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="20cdb-166"><a name="_Toc395637763"></a>4. adım: ASP.NET MVC uygulaması hello ayarlama</span><span class="sxs-lookup"><span data-stu-id="20cdb-166"><a name="_Toc395637763"></a>Step 4: Set up hello ASP.NET MVC application</span></span>
<span data-ttu-id="20cdb-167">Şimdi Merhaba modeller, görünümler ve denetleyiciler toothis MVC uygulaması ekleyelim:</span><span class="sxs-lookup"><span data-stu-id="20cdb-167">Now let's add hello models, views, and controllers toothis MVC application:</span></span>

* <span data-ttu-id="20cdb-168">[Model ekleme](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="20cdb-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="20cdb-169">[Denetleyici ekleme](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="20cdb-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="20cdb-170">[Görünümler ekleme](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="20cdb-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="20cdb-171"><a name="_Toc395637764"></a>JSON veri modeli ekleme</span><span class="sxs-lookup"><span data-stu-id="20cdb-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="20cdb-172">Merhaba oluşturarak başlayalım **M** MVC'de, model hello.</span><span class="sxs-lookup"><span data-stu-id="20cdb-172">Let's begin by creating hello **M** in MVC, hello model.</span></span> 

1. <span data-ttu-id="20cdb-173">İçinde **Çözüm Gezgini**, sağ hello **modelleri** klasörünü tıklatın **Ekle**ve ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-173">In **Solution Explorer**, right-click hello **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="20cdb-174">Merhaba **Yeni Öğe Ekle** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="20cdb-174">hello **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="20cdb-175">Yeni sınıfınıza **Item.cs** adını verin ve **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20cdb-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="20cdb-176">Bu yeni **Item.cs** dosya, hello aşağıdakileri hello sonra son ekleyin *deyimiyle*.</span><span class="sxs-lookup"><span data-stu-id="20cdb-176">In this new **Item.cs** file, add hello following after hello last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="20cdb-177">Şimdi de bu kodu</span><span class="sxs-lookup"><span data-stu-id="20cdb-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="20cdb-178">koddan hello ile.</span><span class="sxs-lookup"><span data-stu-id="20cdb-178">with hello following code.</span></span>
   
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
   
    <span data-ttu-id="20cdb-179">Tüm veriler Azure Cosmos veritabanı hello kablo üzerinden geçer ve JSON olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="20cdb-179">All data in Azure Cosmos DB is passed over hello wire and stored as JSON.</span></span> <span data-ttu-id="20cdb-180">nesnelerinizin seri/seri kullanabileceğiniz JSON.NET tarafından toocontrol hello şekilde hello **Item** özniteliği hello gösterildiği gibi **öğesi** yeni oluşturduğumuz sınıfı.</span><span class="sxs-lookup"><span data-stu-id="20cdb-180">toocontrol hello way your objects are serialized/deserialized by JSON.NET you can use hello **JsonProperty** attribute as demonstrated in hello **Item** class we just created.</span></span> <span data-ttu-id="20cdb-181">Sizin **sahip** toodo bu ancak sorun istediğiniz tooensure özelliklerimin hello JSON camelCase adlandırma kuralları izleyin.</span><span class="sxs-lookup"><span data-stu-id="20cdb-181">You don't **have** toodo this but I want tooensure that my properties follow hello JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="20cdb-182">JSON'a gittiği ancak hello ile olduğu gibi .NET özelliklerinizi tamamen adlandırabilirsiniz hello özellik adının hello biçimi yalnızca denetleyebilirsiniz **açıklama** özelliği.</span><span class="sxs-lookup"><span data-stu-id="20cdb-182">Not only can you control hello format of hello property name when it goes into JSON, but you can entirely rename your .NET properties like I did with hello **Description** property.</span></span> 

### <span data-ttu-id="20cdb-183"><a name="_Toc395637765"></a>Denetleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="20cdb-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="20cdb-184">Merhaba mvc'deki **M**, şimdi hello oluşturalım **C** ' yi, yani denetleyici sınıfını.</span><span class="sxs-lookup"><span data-stu-id="20cdb-184">That takes care of hello **M**, now let's create hello **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="20cdb-185">İçinde **Çözüm Gezgini**, sağ hello **denetleyicileri** klasörünü tıklatın **Ekle**ve ardından **denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-185">In **Solution Explorer**, right-click hello **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="20cdb-186">Merhaba **İskele Ekle** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="20cdb-186">hello **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="20cdb-187">**MVC 5 Denetleyici - Boş**'u seçin ve ardından **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20cdb-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![MVC 5 denetleyici - boş seçeneği vurgulanmış hello ile Merhaba İskele Ekle iletişim kutusunun ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="20cdb-189">Yeni Denetleyicinize **ItemController** adını verin.</span><span class="sxs-lookup"><span data-stu-id="20cdb-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Merhaba denetleyici Ekle iletişim kutusunun ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="20cdb-191">Merhaba dosya oluşturulduktan sonra Visual Studio çözümünüzü hello aşağıdaki hello yeni Itemcontroller.cs dosyasıyla benzemelidir **Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-191">Once hello file is created, your Visual Studio solution should resemble hello following with hello new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="20cdb-192">Merhaba daha önce oluşturduğunuz yeni Item.cs dosyası da gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="20cdb-192">hello new Item.cs file created earlier is also shown.</span></span>
   
    ![Merhaba Visual Studio çözümü - hello yeni Itemcontroller.cs dosyası ve Item.cs dosyası vurgulanmış şekilde çözüm Gezgini'nin ekran](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="20cdb-194">Itemcontroller.cs'yi kapatabilirsiniz, biz tooit daha sonra yine gelmenizi.</span><span class="sxs-lookup"><span data-stu-id="20cdb-194">You can close ItemController.cs, we'll come back tooit later.</span></span> 

### <span data-ttu-id="20cdb-195"><a name="_Toc395637766"></a>Görünümler ekleme</span><span class="sxs-lookup"><span data-stu-id="20cdb-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="20cdb-196">Şimdi, hello oluşturalım **V** MVC uygulamasında hello görünümleri:</span><span class="sxs-lookup"><span data-stu-id="20cdb-196">Now, let's create hello **V** in MVC, hello views:</span></span>

* <span data-ttu-id="20cdb-197">[Öğe Dizini görünümü ekleme](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="20cdb-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="20cdb-198">[Yeni Öğe görünümü ekleme](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="20cdb-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="20cdb-199">[Düzenleme Öğesi görünümü ekleme](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="20cdb-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="20cdb-200"><a name="AddItemIndexView"></a>Öğe Dizini görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="20cdb-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="20cdb-201">İçinde **Çözüm Gezgini**, hello genişletin **görünümleri** klasörü, sağ hello boş **öğesi** hello eklediğinizde Visual Studio için oluşturduğunuz klasöre  **Itemcontroller** daha önce tıklatın **Ekle**ve ardından **Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-201">In **Solution Explorer**, expand hello **Views**  folder, right-click hello empty **Item** folder that Visual Studio created for you when you added hello **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Visual Studio hello Görünüm Ekle komutları vurgulanmış oluşturulan hello öğe klasörünü gösteren Çözüm Gezgini ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="20cdb-203">Merhaba, **Görünüm Ekle** iletişim kutusunda, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="20cdb-203">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="20cdb-204">Merhaba, **Görünüm adı** kutusuna ***dizin***.</span><span class="sxs-lookup"><span data-stu-id="20cdb-204">In hello **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="20cdb-205">Merhaba, **şablonu** kutusunda ***listesi***.</span><span class="sxs-lookup"><span data-stu-id="20cdb-205">In hello **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="20cdb-206">Merhaba, **Model sınıfı** kutusunda ***öğesi (Yapılacaklar. Modeller)***.</span><span class="sxs-lookup"><span data-stu-id="20cdb-206">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="20cdb-207">Merhaba düzen sayfası kutusunda yazın ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="20cdb-207">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Ekran görüntüsü gösteren hello Görünüm Ekle iletişim kutusu](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="20cdb-209">Bu değerlerin tümü ayarlandıktan sonra, **Ekle**'ye tıklayın ve Visual Studio'nun yeni bir şablon görünümü oluşturmasına izin verin.</span><span class="sxs-lookup"><span data-stu-id="20cdb-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="20cdb-210">Bunu yaptıktan sonra oluşturulan hello cshtml dosyasını açar.</span><span class="sxs-lookup"><span data-stu-id="20cdb-210">Once it is done, it will open hello cshtml file  that was created.</span></span> <span data-ttu-id="20cdb-211">Biz tooit daha sonra yine gelmenizi şekilde Biz bu dosyayı Visual Studio kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20cdb-211">We can close that file in Visual Studio as we will come back tooit later.</span></span>

#### <span data-ttu-id="20cdb-212"><a name="AddNewIndexView"></a>Yeni Öğe görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="20cdb-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="20cdb-213">Oluşturduğumuz benzer toohow bir **öğe dizini** görünümü, biz şimdi oluşturacak yeni oluşturmak için yeni bir görünüm **öğeleri**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-213">Similar toohow we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="20cdb-214">İçinde **Çözüm Gezgini**, sağ hello **öğesi** klasörü yeniden tıklatın **Ekle**ve ardından **Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-214">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="20cdb-215">Merhaba, **Görünüm Ekle** iletişim kutusunda, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="20cdb-215">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="20cdb-216">Merhaba, **Görünüm adı** kutusuna ***oluşturma***.</span><span class="sxs-lookup"><span data-stu-id="20cdb-216">In hello **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="20cdb-217">Merhaba, **şablonu** kutusunda ***oluşturma***.</span><span class="sxs-lookup"><span data-stu-id="20cdb-217">In hello **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="20cdb-218">Merhaba, **Model sınıfı** kutusunda ***öğesi (Yapılacaklar. Modeller)***.</span><span class="sxs-lookup"><span data-stu-id="20cdb-218">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="20cdb-219">Merhaba düzen sayfası kutusunda yazın ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="20cdb-219">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="20cdb-220">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20cdb-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="20cdb-221"><a name="_Toc395888515"></a>Düzenleme Öğesi görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="20cdb-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="20cdb-222">Ve son olarak, düzenleme için son bir görünüm ekleyin bir **öğesi** hello içinde öncekiyle aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="20cdb-222">And finally, add one last view for editing an **Item** in hello same way as before.</span></span>

1. <span data-ttu-id="20cdb-223">İçinde **Çözüm Gezgini**, sağ hello **öğesi** klasörü yeniden tıklatın **Ekle**ve ardından **Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-223">In **Solution Explorer**, right-click hello **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="20cdb-224">Merhaba, **Görünüm Ekle** iletişim kutusunda, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="20cdb-224">In hello **Add View** dialog box, do hello following:</span></span>
   
   * <span data-ttu-id="20cdb-225">Merhaba, **Görünüm adı** kutusuna ***Düzenle***.</span><span class="sxs-lookup"><span data-stu-id="20cdb-225">In hello **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="20cdb-226">Merhaba, **şablonu** kutusunda ***Düzenle***.</span><span class="sxs-lookup"><span data-stu-id="20cdb-226">In hello **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="20cdb-227">Merhaba, **Model sınıfı** kutusunda ***öğesi (Yapılacaklar. Modeller)***.</span><span class="sxs-lookup"><span data-stu-id="20cdb-227">In hello **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="20cdb-228">Merhaba düzen sayfası kutusunda yazın ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="20cdb-228">In hello layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="20cdb-229">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20cdb-229">Click **Add**.</span></span>

<span data-ttu-id="20cdb-230">Bunu yaptıktan sonra toothese görünümleri daha sonra geri döneceksiniz olarak Visual Studio tüm hello cshtml belgelerini kapatın.</span><span class="sxs-lookup"><span data-stu-id="20cdb-230">Once this is done, close all hello cshtml documents in Visual Studio as we will return toothese views later.</span></span>

## <span data-ttu-id="20cdb-231"><a name="_Toc395637769"></a>5. Adım: Azure Cosmos DB’yi bağlama</span><span class="sxs-lookup"><span data-stu-id="20cdb-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="20cdb-232">Merhaba standart MVC işleri hallolduğuna göre tooadding hello kodu Azure Cosmos DB dönelim.</span><span class="sxs-lookup"><span data-stu-id="20cdb-232">Now that hello standard MVC stuff is taken care of, let's turn tooadding hello code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="20cdb-233">Bu bölümde, kod toohandle hello aşağıdaki ekleyeceğiz:</span><span class="sxs-lookup"><span data-stu-id="20cdb-233">In this section, we'll add code toohandle hello following:</span></span>

* <span data-ttu-id="20cdb-234">[Tamamlanmamış Öğeleri listeleme](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="20cdb-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="20cdb-235">[Öğeler ekleme](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="20cdb-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="20cdb-236">[Öğeleri düzenleme](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="20cdb-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="20cdb-237"><a name="_Toc395637770"></a>MVC web uygulamanızda tamamlanmamış Öğeleri listeleme</span><span class="sxs-lookup"><span data-stu-id="20cdb-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="20cdb-238">Merhaba ilk şey toodo burada olan tüm hello mantığı tooconnect tooand kullanım Azure Cosmos DB içeren bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="20cdb-238">hello first thing toodo here is add a class that contains all hello logic tooconnect tooand use Azure Cosmos DB.</span></span> <span data-ttu-id="20cdb-239">Bu öğretici için size tüm bu mantığı DocumentDBRepository adlı tooa depo sınıfına kapsülleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="20cdb-239">For this tutorial we'll encapsulate all this logic in tooa repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="20cdb-240">İçinde **Çözüm Gezgini**, hello projeye sağ tıklayın, **Ekle**ve ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-240">In **Solution Explorer**, right-click on hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="20cdb-241">Ad hello yeni sınıf **DocumentDBRepository** tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-241">Name hello new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="20cdb-242">Yeni oluşturulan hello içinde **DocumentDBRepository** sınıfı ve hello aşağıdakileri ekleyin *using deyimleri* hello yukarıda *ad alanı* bildirimi</span><span class="sxs-lookup"><span data-stu-id="20cdb-242">In hello newly created **DocumentDBRepository** class and add hello following *using statements* above hello *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="20cdb-243">Şimdi de bu kodu</span><span class="sxs-lookup"><span data-stu-id="20cdb-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="20cdb-244">koddan hello ile.</span><span class="sxs-lookup"><span data-stu-id="20cdb-244">with hello following code.</span></span>
   
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
   
    
3. <span data-ttu-id="20cdb-245">Bazı değerler yapılandırmasından okuduğunuz, bu nedenle hello Aç **Web.config** uygulamanızın dosyasını ve satırlar hello altında aşağıdaki hello ekleyin `<AppSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="20cdb-245">We're reading some values from configuration, so open hello **Web.config** file of your application and add hello following lines under hello `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="20cdb-246">Şimdi, hello değerlerini güncelleştirin *endpoint* ve *authKey* hello anahtarlar dikey penceresinde hello Azure Portal kullanarak.</span><span class="sxs-lookup"><span data-stu-id="20cdb-246">Now, update hello values for *endpoint* and *authKey* using hello Keys blade of hello Azure Portal.</span></span> <span data-ttu-id="20cdb-247">Merhaba kullanmak **URI** hello hello uç noktası ayarı ve kullanım hello hello değeri olarak anahtarlar dikey penceresinden **birincil anahtar**, veya **ikincil anahtar** hello hello hello değeri olarak anahtarlar dikey penceresinden authKey ayarının.</span><span class="sxs-lookup"><span data-stu-id="20cdb-247">Use hello **URI** from hello Keys blade as hello value of hello endpoint setting, and use hello **PRIMARY KEY**, or **SECONDARY KEY** from hello Keys blade as hello value of hello authKey setting.</span></span>

    <span data-ttu-id="20cdb-248">Alır dikkatli'hello Azure Cosmos DB depoyu şimdi bağlamayı, uygulama mantığımızı ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="20cdb-248">That takes care of wiring up hello Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="20cdb-249">Merhaba ilk şey toodisplay hello tamamlanmamış öğeleri toobe mümkün toodo bir Yapılacaklar listesi uygulaması ile olan istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="20cdb-249">hello first thing we want toobe able toodo with a todo list application is toodisplay hello incomplete items.</span></span>  <span data-ttu-id="20cdb-250">Aşağıdaki kod parçacığını hello içinde istediğiniz yere hello kopyalayıp **DocumentDBRepository** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="20cdb-250">Copy and paste hello following code snippet anywhere within hello **DocumentDBRepository** class.</span></span>
   
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
2. <span data-ttu-id="20cdb-251">Açık hello **Itemcontroller** daha önce eklenen ve hello aşağıdakileri ekleyin *using deyimleri* hello ad alanı bildiriminin üstüne.</span><span class="sxs-lookup"><span data-stu-id="20cdb-251">Open hello **ItemController** we added earlier and add hello following *using statements* above hello namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="20cdb-252">Projeniz "todo" adlı değil, ardından "todo. kullanarak tooupdate gerekir Modelleri"; projeniz tooreflect hello adı.</span><span class="sxs-lookup"><span data-stu-id="20cdb-252">If your project is not named "todo", then you need tooupdate using "todo.Models"; tooreflect hello name of your project.</span></span>
   
    <span data-ttu-id="20cdb-253">Şimdi de bu kodu</span><span class="sxs-lookup"><span data-stu-id="20cdb-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="20cdb-254">koddan hello ile.</span><span class="sxs-lookup"><span data-stu-id="20cdb-254">with hello following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="20cdb-255">Açık **Global.asax.cs** ve satır toohello aşağıdaki hello ekleyin **Application_Start** yöntemi</span><span class="sxs-lookup"><span data-stu-id="20cdb-255">Open **Global.asax.cs** and add hello following line toohello **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="20cdb-256">Bu noktada çözümünüzün hatasız mümkün toobuild olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="20cdb-256">At this point your solution should be able toobuild without any errors.</span></span>

<span data-ttu-id="20cdb-257">Merhaba uygulamayı şimdi çalıştırırsanız toohello geçecek **HomeController** ve hello **dizin** söz konusu denetleyicinin görünümü.</span><span class="sxs-lookup"><span data-stu-id="20cdb-257">If you ran hello application now, you would go toohello **HomeController** and hello **Index** view of that controller.</span></span> <span data-ttu-id="20cdb-258">Merhaba başlangıcında seçtik hello MVC şablonu projesinin hello varsayılan davranışı budur ancak biz bunu istemiyoruz!</span><span class="sxs-lookup"><span data-stu-id="20cdb-258">This is hello default behavior for hello MVC template project we chose at hello start but we don't want that!</span></span> <span data-ttu-id="20cdb-259">Bu davranış bu MVC uygulama tooalter yönlendirme hello değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="20cdb-259">Let's change hello routing on this MVC application tooalter this behavior.</span></span>

<span data-ttu-id="20cdb-260">Açık ***uygulama\_Start\RouteConfig.cs*** ve başlayarak hello satırı bulun "Varsayılanları:" ve aşağıdaki tooresemble hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="20cdb-260">Open ***App\_Start\RouteConfig.cs*** and locate hello line starting with "defaults:" and change it tooresemble hello following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="20cdb-261">Bu şimdi hello URL toocontrol bir değer belirtmediyseniz, yönlendirme davranışını yerine hello ASP.NET MVC söyler **giriş**, kullanın **öğesi** hello denetleyici ve kullanıcı olarak **dizin** hello görünüm olarak.</span><span class="sxs-lookup"><span data-stu-id="20cdb-261">This now tells ASP.NET MVC that if you have not specified a value in hello URL toocontrol hello routing behavior that instead of **Home**, use **Item** as hello controller and user **Index** as hello view.</span></span>

<span data-ttu-id="20cdb-262">Merhaba uygulaması çalıştırırsanız, bunu şimdi, **Itemcontroller** hangi toohello depo sınıfında çağırın ve tüm hello tamamlanmamış öğeleri toohello hello Getıtems yöntemini tooreturn kullanmak **görünümleri** \\ **Öğesi**\\**dizin** görünümü.</span><span class="sxs-lookup"><span data-stu-id="20cdb-262">Now if you run hello application, it will call into your **ItemController** which will call in toohello repository class and use hello GetItems method tooreturn all hello incomplete items toohello **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="20cdb-263">Bu projeyi şimdi oluşturur ve çalıştırırsanız buna benzeyen bir şey görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="20cdb-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Bu veritabanı Öğreticisi tarafından oluşturulan hello Yapılacaklar listesi web uygulamasının ekran görüntüsü](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="20cdb-265"><a name="_Toc395637771"></a>Öğeler ekleme</span><span class="sxs-lookup"><span data-stu-id="20cdb-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="20cdb-266">Şimdi bir boş kılavuz toolook başka şeyler sahibiz şekilde bazı öğeler Veritabanımıza yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="20cdb-266">Let's put some items into our database so we have something more than an empty grid toolook at.</span></span>

<span data-ttu-id="20cdb-267">Bazı kodlar çok ekleyelim Azure Cosmos DBRepository ve Itemcontroller'a toopersist hello kayıt Azure Cosmos veritabanı.</span><span class="sxs-lookup"><span data-stu-id="20cdb-267">Let's add some code too Azure Cosmos DBRepository and ItemController toopersist hello record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="20cdb-268">Yöntem tooyour aşağıdaki hello eklemek **DocumentDBRepository** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="20cdb-268">Add hello following method tooyour **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="20cdb-269">Bu yöntem yalnızca tooit geçirilen nesneyi alır ve Azure Cosmos DB'de devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="20cdb-269">This method simply takes an object passed tooit and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="20cdb-270">Merhaba Itemcontroller.cs dosyasını açın ve aşağıdaki kod parçacığını hello sınıfı içinde hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="20cdb-270">Open hello ItemController.cs file and add hello following code snippet within hello class.</span></span> <span data-ttu-id="20cdb-271">ASP.NET MVC hello için hangi toodo nasıl bilir budur **oluşturma** eylem.</span><span class="sxs-lookup"><span data-stu-id="20cdb-271">This is how ASP.NET MVC knows what toodo for hello **Create** action.</span></span> <span data-ttu-id="20cdb-272">Bu durumda yalnızca işleme hello Create.cshtml görünümünü daha önce oluşturulan ilişkili.</span><span class="sxs-lookup"><span data-stu-id="20cdb-272">In this case just render hello associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="20cdb-273">Şimdi bu denetleyici hello hello gönderim kabul edecek biraz daha koda ihtiyacımız **oluşturma** görünümü.</span><span class="sxs-lookup"><span data-stu-id="20cdb-273">We now need some more code in this controller that will accept hello submission from hello **Create** view.</span></span>
3. <span data-ttu-id="20cdb-274">Merhaba sonraki bloğu kod toohello hangi toodo Bu denetleyici için POST formuyla ASP.NET MVC söyleyen Itemcontroller.cs sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="20cdb-274">Add hello next block of code toohello ItemController.cs class that tells ASP.NET MVC what toodo with a form POST for this controller.</span></span>
   
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
   
    <span data-ttu-id="20cdb-275">Bu kod toohello DocumentDBRepository çağırır ve hello Createıtemasync yöntemini toopersist hello yeni Yapılacaklar öğesi toohello bir veritabanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="20cdb-275">This code calls in toohello DocumentDBRepository and uses hello CreateItemAsync method toopersist hello new todo item toohello database.</span></span> 
   
    <span data-ttu-id="20cdb-276">**Güvenlik Notu**: Merhaba **ValidateAntiForgeryToken** özniteliği kullanılır burada toohelp bu uygulamayı siteler arası istek sahteciliği saldırılarına karşı koruyun.</span><span class="sxs-lookup"><span data-stu-id="20cdb-276">**Security Note**: hello **ValidateAntiForgeryToken** attribute is used here toohelp protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="20cdb-277">Bu öznitelik yalnızca eklemekten daha fazla tooit, kendi görünümlerinizi de bu sahteciliğe karşı koruma belirteci ile toowork gerekir.</span><span class="sxs-lookup"><span data-stu-id="20cdb-277">There is more tooit than just adding this attribute, your views need toowork with this anti-forgery token as well.</span></span> <span data-ttu-id="20cdb-278">Merhaba konu ve nasıl tooimplement bunu doğru şekilde, lütfen görmek örnekleri hakkında daha fazla bilgi için [siteler arası istek sahteciliğini önleme][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="20cdb-278">For more on hello subject, and examples of how tooimplement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="20cdb-279">Sağlanan kaynak kodu Hello [GitHub] [ GitHub] hello tam uygulamayı içerir.</span><span class="sxs-lookup"><span data-stu-id="20cdb-279">hello source code provided on [GitHub][GitHub] has hello full implementation in place.</span></span>
   
    <span data-ttu-id="20cdb-280">**Güvenlik Notu**: hello de kullanırız **bağlamak** hello yöntemi parametresi toohelp öznitelikte aşırı gönderim saldırılarına karşı koruyun.</span><span class="sxs-lookup"><span data-stu-id="20cdb-280">**Security Note**: We also use hello **Bind** attribute on hello method parameter toohelp protect against over-posting attacks.</span></span> <span data-ttu-id="20cdb-281">Daha ayrıntılı bilgi için lütfen bkz. [ASP.NET MVC'de Temel CRUD İşlemleri][Basic CRUD Operations in ASP.NET MVC].</span><span class="sxs-lookup"><span data-stu-id="20cdb-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="20cdb-282">Merhaba gerekli kod tooadd yeni öğeleri tooour veritabanı sonlanır.</span><span class="sxs-lookup"><span data-stu-id="20cdb-282">This concludes hello code required tooadd new Items tooour database.</span></span>

### <span data-ttu-id="20cdb-283"><a name="_Toc395637772"></a>Öğeleri Düzenleme</span><span class="sxs-lookup"><span data-stu-id="20cdb-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="20cdb-284">Toodo bize için son bir şey yoktur ve tooadd hello özelliği tooedit **öğeleri** hello veritabanı ve toomark olarak tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="20cdb-284">There is one last thing for us toodo, and that is tooadd hello ability tooedit **Items** in hello database and toomark them as complete.</span></span> <span data-ttu-id="20cdb-285">Merhaba düzenleme görünümü zaten toohello proje eklenmiş, yalnızca tooadd ihtiyacımız şekilde tooour denetleyici ve toohello bazı kodu **DocumentDBRepository** yeniden sınıf.</span><span class="sxs-lookup"><span data-stu-id="20cdb-285">hello view for editing was already added toohello project, so we just need tooadd some code tooour controller and toohello **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="20cdb-286">Toohello aşağıdaki hello eklemek **DocumentDBRepository** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="20cdb-286">Add hello following toohello **DocumentDBRepository** class.</span></span>
   
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
   
    <span data-ttu-id="20cdb-287">Bu yöntemlerin ilki olan Hello **GetItem** Azure Cosmos DB'den geri toohello geçirilen bir öğe getirir **Itemcontroller** ve ardından toohello **Düzenle** görünümü.</span><span class="sxs-lookup"><span data-stu-id="20cdb-287">hello first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back toohello **ItemController** and then on toohello **Edit** view.</span></span>
   
    <span data-ttu-id="20cdb-288">Merhaba hello yöntemlerinin ikinci yalnızca değiştirir hello eklediğimiz **belge** Azure Cosmos veritabanı hello hello sürümüyle **belge** hello geçirilen **Itemcontroller**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-288">hello second of hello methods we just added replaces hello **Document** in Azure Cosmos DB with hello version of hello **Document** passed in from hello **ItemController**.</span></span>
2. <span data-ttu-id="20cdb-289">Toohello aşağıdaki hello eklemek **Itemcontroller** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="20cdb-289">Add hello following toohello **ItemController** class.</span></span>
   
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
   
    <span data-ttu-id="20cdb-290">Merhaba ilk yöntemi tanıtıcıları hello kullanıcı tıkladığında, üzerinde hello olur Http GET hello **Düzenle** hello bağlantısından **dizin** görünümü.</span><span class="sxs-lookup"><span data-stu-id="20cdb-290">hello first method handles hello Http GET that happens when hello user clicks on hello **Edit** link from hello **Index** view.</span></span> <span data-ttu-id="20cdb-291">Bu yöntem getirir bir [ **belge** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) Azure Cosmos DB'den ve toohello geçirir **Düzenle** görünümü.</span><span class="sxs-lookup"><span data-stu-id="20cdb-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it toohello **Edit** view.</span></span>
   
    <span data-ttu-id="20cdb-292">Merhaba **Düzenle** görünüm sonra bir Http POST toohello yapın **Indexcontroller**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-292">hello **Edit** view will then do an Http POST toohello **IndexController**.</span></span> 
   
    <span data-ttu-id="20cdb-293">güncelleştirilmiş hello nesne tooAzure Cosmos DB toobe geçirme tanıtıcıları eklediğimiz ikinci yöntem hello hello veritabanında kalıcı.</span><span class="sxs-lookup"><span data-stu-id="20cdb-293">hello second method we added handles passing hello updated object tooAzure Cosmos DB toobe persisted in hello database.</span></span>

<span data-ttu-id="20cdb-294">Bunu ihtiyacımız olan her şey toorun uygulamamız olan olan, tamamlanmamış listesi **öğeleri**, yeni Ekle **öğeleri**ve düzenleme **öğeleri**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-294">That's it, that is everything we need toorun our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="20cdb-295"><a name="_Toc395637773"></a>6. adım: hello uygulama yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="20cdb-295"><a name="_Toc395637773"></a>Step 6: Run hello application locally</span></span>
<span data-ttu-id="20cdb-296">yerel makinenizde tootest Merhaba uygulaması hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="20cdb-296">tootest hello application on your local machine, do hello following:</span></span>

1. <span data-ttu-id="20cdb-297">Visual Studio toobuild hello uygulamasında hata ayıklama modunda F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="20cdb-297">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span> <span data-ttu-id="20cdb-298">Merhaba uygulaması derleme ve önce gördüğümüz hello boş kılavuz sayfasıyla bir tarayıcıyı başlatacak:</span><span class="sxs-lookup"><span data-stu-id="20cdb-298">It should build hello application and launch a browser with hello empty grid page we saw before:</span></span>
   
    ![Bu veritabanı Öğreticisi tarafından oluşturulan hello Yapılacaklar listesi web uygulamasının ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="20cdb-300">Merhaba tıklatın **Yeni Oluştur** değerleri toohello ekleyin ve bağlama **adı** ve **açıklama** alanları.</span><span class="sxs-lookup"><span data-stu-id="20cdb-300">Click hello **Create New** link and add values toohello **Name** and **Description** fields.</span></span> <span data-ttu-id="20cdb-301">Merhaba bırakın **tamamlandı** onay kutusu seçili değilse hello yeni **öğesi** tamamlanmış durumda eklenir ve hello ilk listede görünmez.</span><span class="sxs-lookup"><span data-stu-id="20cdb-301">Leave hello **Completed** check box unselected otherwise hello new **Item** will be added in a completed state and will not appear on hello initial list.</span></span>
   
    ![Merhaba Oluştur görünümünün ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="20cdb-303">Tıklatın **oluşturma** ve yeniden yönlendirilen geri toohello **dizin** Görünüm ve **öğesi** hello listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="20cdb-303">Click **Create** and you are redirected back toohello **Index** view and your **Item** appears in hello list.</span></span>
   
    ![Merhaba dizin görünümünün ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="20cdb-305">Ücretsiz tooadd birkaç daha eşitleyerek **öğeleri** tooyour Yapılacaklar listesi.</span><span class="sxs-lookup"><span data-stu-id="20cdb-305">Feel free tooadd a few more **Items** tooyour todo list.</span></span>
    
4. <span data-ttu-id="20cdb-306">Tıklatın **Düzenle** sonraki tooan **öğesi** hello listedeki toohello alınır **Düzenle** hello dahil olmak üzere nesnenizin herhangi bir özelliği güncelleştirme Görünüm  **Tamamlanan** bayrağı.</span><span class="sxs-lookup"><span data-stu-id="20cdb-306">Click **Edit** next tooan **Item** on hello list and you are taken toohello **Edit** view where you can update any property of your object, including hello **Completed** flag.</span></span> <span data-ttu-id="20cdb-307">Merhaba işaretlerseniz **tam** bayrak ve tıklatın **kaydetmek**, hello **öğesi** hello tamamlanmamış görevler listesinden kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="20cdb-307">If you mark hello **Complete** flag and click **Save**, hello **Item** is removed from hello list of incomplete tasks.</span></span>
   
    ![Merhaba hello tamamlandı kutusu işaretli şekilde dizin görünümünün ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="20cdb-309">Merhaba uygulamayı test ettikten sonra Ctrl + F5 toostop hello uygulama hata ayıklama tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="20cdb-309">Once you've tested hello app, press Ctrl+F5 toostop debugging hello app.</span></span> <span data-ttu-id="20cdb-310">Hazır toodeploy olduğunuz!</span><span class="sxs-lookup"><span data-stu-id="20cdb-310">You're ready toodeploy!</span></span>

## <span data-ttu-id="20cdb-311"><a name="_Toc395637774"></a>7. adım: hello uygulama tooAzure uygulama hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="20cdb-311"><a name="_Toc395637774"></a>Step 7: Deploy hello application tooAzure App Service</span></span> 
<span data-ttu-id="20cdb-312">Merhaba tam uygulamaya sahip olduğunuza Azure Cosmos DB ile düzgün çalışmasını toodeploy bu web uygulaması tooAzure uygulama hizmeti yapacağız.</span><span class="sxs-lookup"><span data-stu-id="20cdb-312">Now that you have hello complete application working correctly with Azure Cosmos DB we're going toodeploy this web app tooAzure App Service.</span></span>  

1. <span data-ttu-id="20cdb-313">toopublish toodo ihtiyacınız bu uygulamanın tüm olduğunu hello projeye sağ tıklayın **Çözüm Gezgini** tıklatıp **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-313">toopublish this application all you need toodo is right-click on hello project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Merhaba Çözüm Gezgini'nde Yayımla seçeneğinin ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="20cdb-315">Merhaba, **Yayımla** iletişim kutusu, tıklatın **Microsoft Azure App Service**seçeneğini belirleyip **Yeni Oluştur** toocreate bir uygulama hizmeti profil ya da'ı tıklatın **seçin Varolan** toouse bir profil.</span><span class="sxs-lookup"><span data-stu-id="20cdb-315">In hello **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** toocreate an App Service profile, or click **Select Existing** toouse an existing profile.</span></span>

    ![Visual Studio'da Yayımla iletişim kutusu](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="20cdb-317">Var olan bir Azure uygulama hizmeti profiliniz varsa, abonelik adınızı girin.</span><span class="sxs-lookup"><span data-stu-id="20cdb-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="20cdb-318">Kullanım hello **Görünüm** toosort kaynak grubu veya kaynak türü tarafından filtre sonra Azure uygulama hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="20cdb-318">Use hello **View** filter toosort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Visual Studio'da uygulama hizmeti iletişim kutusu](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="20cdb-320">Yeni bir Azure uygulama hizmeti profili toocreate tıklatın **Yeni Oluştur** hello içinde **Yayımla** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="20cdb-320">toocreate a new Azure App Service profile, click **Create New** in hello **Publish** dialog box.</span></span> <span data-ttu-id="20cdb-321">Merhaba, **App Service Oluştur** iletişim kutusunda, Web uygulaması adı ve uygun abonelik, kaynak grubu ve uygulama hizmeti planı girin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="20cdb-321">In hello **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Visual Studio'da uygulama hizmeti iletişim kutusu oluşturma](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="20cdb-323">Visual Studio birkaç saniye içinde web uygulamanızı yayımlamayı bitirecek ve Azure'da çalışan, handiwork görebileceğiniz bir tarayıcıyı başlatacak!</span><span class="sxs-lookup"><span data-stu-id="20cdb-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="20cdb-324"><a name="_Toc395637775"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20cdb-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="20cdb-325">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="20cdb-325">Congratulations!</span></span> <span data-ttu-id="20cdb-326">Yalnızca ilk ASP.NET MVC Azure Cosmos DB kullanarak web uygulaması oluşturdunuz ve bunu tooAzure yayımladınız.</span><span class="sxs-lookup"><span data-stu-id="20cdb-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it tooAzure.</span></span> <span data-ttu-id="20cdb-327">Merhaba hello ayrıntı dahil olmak üzere Merhaba tam uygulaması için kaynak kodu ve silme bu dahil edilmemiş işlevlerinin öğretici indirilebilir veya kopyalamanın [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="20cdb-327">hello source code for hello complete application, including hello detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="20cdb-328">Bu nedenle bu tooyour uygulama eklemek isterseniz hello kodu alın ve toothis uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="20cdb-328">So if you're interested in adding that tooyour app, grab hello code and add it toothis app.</span></span>

<span data-ttu-id="20cdb-329">tooadd ek işlevler tooyour uygulama, gözden geçirme hello API'leri hello kullanılabilir [Azure Cosmos DB .NET kitaplığı](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) üzerinde boş toocontribute toohello Azure Cosmos DB .NET kitaplığı eşitleyerek [GitHub] [GitHub].</span><span class="sxs-lookup"><span data-stu-id="20cdb-329">tooadd additional functionality tooyour application, review hello APIs available in hello [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free toocontribute toohello Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
