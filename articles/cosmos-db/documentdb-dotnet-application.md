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
ms.openlocfilehash: 3f2950fe25feb8f3ee81cc0a79bf624f0ee33bd5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <span data-ttu-id="f3a7d-105"><a name="_Toc395809351"></a>ASP.NET MVC Öğreticisi: Azure Cosmos DB ile Web uygulaması geliştirme</span><span class="sxs-lookup"><span data-stu-id="f3a7d-105"><a name="_Toc395809351"></a>ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3a7d-106">.NET</span><span class="sxs-lookup"><span data-stu-id="f3a7d-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="f3a7d-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="f3a7d-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="f3a7d-108">Java</span><span class="sxs-lookup"><span data-stu-id="f3a7d-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="f3a7d-109">Python</span><span class="sxs-lookup"><span data-stu-id="f3a7d-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="f3a7d-110">Bu makale, JSON belgelerini depolama ve sorgulama amacıyla Azure Cosmos DB'yi nasıl verimli bir şekilde kullanabileceğinizi vurgulamak için, Azure Cosmos DB kullanarak bir yapılacaklar uygulamasının nasıl oluşturulacağını gösteren uçtan uca bir kılavuz sağlar.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-110">To highlight how you can efficiently leverage Azure Cosmos DB to store and query JSON documents, this article provides an end-to-end walk-through showing you how to build a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="f3a7d-111">Görevler, JSON belgeleri olarak Azure Cosmos DB'de depolanır.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-111">The tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Bu öğreticiyle oluşturulan yapılacaklar listesi MVC web uygulamasının ekran görüntüsü - adım adım ASP.NET MVC öğreticisi](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="f3a7d-113">Bu kılavuz, Azure Cosmos DB hizmet depolamak için nasıl kullanılacağı ve erişim verilerini Azure üzerinde barındırılan bir ASP.NET MVC web uygulamasından gösterir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-113">This walk-through shows you how to use the Azure Cosmos DB service to store and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="f3a7d-114">ASP.NET MVC bileşenleri yerine yalnızca Azure Cosmos DB'ye odaklanan bir öğretici arıyorsanız bkz. [Azure Cosmos DB C# konsol uygulaması oluşturma](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f3a7d-114">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not the ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> <span data-ttu-id="f3a7d-115">Bu öğretici, ASP.NET MVC ve Azure Web Siteleri'ni kullanma konusunda deneyim sahibi olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-115">This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites.</span></span> <span data-ttu-id="f3a7d-116">ASP.NET veya [önkoşul araçlarında](#_Toc395637760) yeniyseniz [GitHub][GitHub] konumundan örnek projenin tamamını indirmenizi ve bu örnekteki yönergeleri uygulamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-116">If you are new to ASP.NET or the [prerequisite tools](#_Toc395637760), we recommend downloading the complete sample project from [GitHub][GitHub] and following the instructions in this sample.</span></span> <span data-ttu-id="f3a7d-117">Oluşturduktan sonra, proje bağlamında kodu daha iyi kavramak için bu makaleyi inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-117">Once you have it built, you can review this article to gain insight on the code in the context of the project.</span></span>
> 
> 

## <span data-ttu-id="f3a7d-118"><a name="_Toc395637760"></a>Bu veritabanı öğreticisi için önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f3a7d-118"><a name="_Toc395637760"></a>Prerequisites for this database tutorial</span></span>
<span data-ttu-id="f3a7d-119">Bu makaledeki yönergeleri uygulamadan önce aşağıdakilere sahip olduğunuzdan emin olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f3a7d-119">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="f3a7d-120">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-120">An active Azure account.</span></span> <span data-ttu-id="f3a7d-121">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f3a7d-122">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f3a7d-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

    <span data-ttu-id="f3a7d-123">OR</span><span class="sxs-lookup"><span data-stu-id="f3a7d-123">OR</span></span>

    <span data-ttu-id="f3a7d-124">Yerel bir [Azure Cosmos DB Öykünücüsü](local-emulator.md) yüklemesi.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="f3a7d-125">[Visual Studio 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="f3a7d-125">[Visual Studio 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="f3a7d-126">Visual Studio 2017, Visual Studio yükleyicisi kullanılabilen .NET için Microsoft Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-126">Microsoft Azure SDK for .NET for Visual Studio 2017, available through the Visual Studio Installer.</span></span>

<span data-ttu-id="f3a7d-127">Bu makaledeki tüm ekran görüntüleri Microsoft Visual Studio Community 2017 kullanılarak alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-127">All the screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="f3a7d-128">Sisteminiz farklı bir sürüme sahip yapılandırılmışsa ekranlarınızın ve seçeneklerinizin tamamen eşleşmeme olasılığı, ancak yukarıdaki önkoşulları karşılarsanız bu çözümün çalışması gerekir mümkündür.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-128">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet the above prerequisites this solution should work.</span></span>

## <span data-ttu-id="f3a7d-129"><a name="_Toc395637761"></a>1. Adım: Azure Cosmos DB veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f3a7d-129"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="f3a7d-130">İlk olarak bir Azure Cosmos DB hesabı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-130">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="f3a7d-131">Zaten bir SQL (DocumentDB) hesabı için Azure Cosmos DB varsa veya Bu öğretici için Azure Cosmos DB öykünücüsü kullanıyorsanız, adımına atlayabilirsiniz [yeni bir ASP.NET MVC uygulaması oluşturma](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="f3a7d-131">If you already have a SQL (DocumentDB) account for Azure Cosmos DB or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="f3a7d-132">Şimdi yeni bir ASP.NET MVC uygulamasının nasıl oluşturulacağını en başından başlayarak inceleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-132">We will now walk through how to create a new ASP.NET MVC application from the ground-up.</span></span> 

## <span data-ttu-id="f3a7d-133"><a name="_Toc395637762"></a>2. Adım: Yeni bir ASP.NET MVC uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f3a7d-133"><a name="_Toc395637762"></a>Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="f3a7d-134">Visual Studio'da, **Dosya** menüsündeki **Yeni** seçeneğine gidin ve ardından **Proje**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-134">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span> <span data-ttu-id="f3a7d-135">**Yeni Proje** iletişim kutusu görünür.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-135">The **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="f3a7d-136">**Proje türleri** bölmesinde **Şablonlar**, **Visual C#**, **Web**'i genişletin ve ardından **ASP.NET Web Uygulaması**'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-136">In the **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![ASP.NET Web Uygulaması proje türü vurgulanmış şekilde Yeni Proje iletişim kutusunun ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="f3a7d-138">**Ad** kutusunda projenin adını yazın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-138">In the **Name** box, type the name of the project.</span></span> <span data-ttu-id="f3a7d-139">Bu öğretici "todo" adını kullanır.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-139">This tutorial uses the name "todo".</span></span> <span data-ttu-id="f3a7d-140">Bunun dışında bir şey kullanmayı seçerseniz bu öğreticinin todo ad alanından söz ettiği her yerde sağlanan kod örneklerini uygulamanıza verdiğiniz ada göre ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-140">If you choose to use something other than this, then wherever this tutorial talks about the todo namespace, you need to adjust the provided code samples to use whatever you named your application.</span></span> 
4. <span data-ttu-id="f3a7d-141">Projeyi oluşturmak istediğiniz klasöre gitmek için **Gözat**'a tıklayın ve ardından **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-141">Click **Browse** to navigate to the folder where you would like to create the project, and then click **OK**.</span></span>
   
      <span data-ttu-id="f3a7d-142">**Yeni ASP.NET Web uygulaması** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-142">The **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![MVC uygulama şablonu vurgulanmış ile yeni bir ASP.NET Web uygulaması iletişim kutusunun ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="f3a7d-144">Şablonlar bölmesinde **MVC**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-144">In the templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="f3a7d-145">**Tamam**'a tıklayarak Visual Studio'nun boş ASP.NET MVC şablonu çevresinde iskele oluşturmasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-145">Click **OK** and let Visual Studio do its thing around scaffolding the empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="f3a7d-146">Visual Studio demirbaş MVC uygulamasını oluşturmayı tamamlandıktan sonra, yerel olarak çalıştırabileceğiniz boş bir ASP.NET uygulamasına sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-146">Once Visual Studio has finished creating the boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="f3a7d-147">Hepimizin ASP.NET "Hello World" uygulamasını gördüğünden emin olduğum için, projeyi yerel olarak çalıştırmayı atlayacağız.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-147">We'll skip running the project locally because I'm sure we've all seen the ASP.NET "Hello World" application.</span></span> <span data-ttu-id="f3a7d-148">Şimdi doğrudan bu projeye Azure Cosmos DB eklemeye ve uygulamamızı oluşturmaya geçelim.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-148">Let's go straight to adding Azure Cosmos DB to this project and building our application.</span></span>

## <span data-ttu-id="f3a7d-149"><a name="_Toc395637767"></a>3. Adım: MVC web uygulaması projenize Azure Cosmos DB ekleme</span><span class="sxs-lookup"><span data-stu-id="f3a7d-149"><a name="_Toc395637767"></a>Step 3: Add Azure Cosmos DB to your MVC web application project</span></span>
<span data-ttu-id="f3a7d-150">Bu çözüm için gereken ASP.NET MVC altyapısının çoğunu elde ettiğimize göre, bu öğreticinin asıl amacı olan MVC web uygulamamıza Azure Cosmos DB'yi eklemeye geçelim.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-150">Now that we have most of the ASP.NET MVC plumbing that we need for this solution, let's get to the real purpose of this tutorial, adding Azure Cosmos DB to our MVC web application.</span></span>

1. <span data-ttu-id="f3a7d-151">Azure Cosmos DB .NET SDK'sı paketlenir ve bir NuGet paketi olarak dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-151">The Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="f3a7d-152">NuGet paketini Visual Studio'da almak için, **Çözüm Gezgini**'nde projeye sağ tıklayarak ve ardından **NuGet Paketlerini Yönet**'e tıklayarak Visual Studio'daki NuGet paket yöneticisini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-152">To get the NuGet package in Visual Studio, use the NuGet package manager in Visual Studio by right-clicking on the project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![NuGet Paketlerini Yönet vurgulanmış şekilde, Çözüm Gezgini'nde web uygulaması projesi için sağ tıklama seçeneklerinin ekran görüntüsü.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="f3a7d-154">**NuGet Paketlerini Yönet** iletişim kutusu görünür.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-154">The **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="f3a7d-155">NuGet **Gözat** kutusunda ***Azure DocumentDB*** yazın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-155">In the NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="f3a7d-156">(Paket adı için Azure Cosmos DB güncelleştirilmemiş.)</span><span class="sxs-lookup"><span data-stu-id="f3a7d-156">(The package name has not been updated to Azure Cosmos DB.)</span></span>
   
    <span data-ttu-id="f3a7d-157">Sonuçlardan yüklemek **Microsoft.Azure.DocumentDB Microsoft tarafından** paket.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-157">From the results, install the **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="f3a7d-158">Bu, indirin ve Newtonsoft.Json gibi tüm bağımlılıkları yanı sıra Azure Cosmos DB paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-158">This will download and install the Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="f3a7d-159">**Önizleme** penceresinde **Tamam**'a tıklayıp **Lisans Kabulü** penceresinde **Kabul Ediyorum**'a tıklayarak yüklemeyi tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-159">Click **OK** in the **Preview** window, and **I Accept** in the **License Acceptance** window to complete the install.</span></span>
   
    ![Microsoft Azure DocumentDB İstemci Kitaplığı vurgulanmış şekilde NuGet Paketlerini Yönet penceresinin ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="f3a7d-161">Alternatif olarak, paketi yüklemek için Paket Yöneticisi Konsolu'nu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-161">Alternatively you can use the Package Manager Console to install the package.</span></span> <span data-ttu-id="f3a7d-162">Bunu yapmak için, **Araçlar** menüsünde **NuGet Paket Yöneticisi**'ne tıklayın ve ardından **Paket Yöneticisi Konsolu**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-162">To do so, on the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="f3a7d-163">İstendiğinde aşağıdakileri yazın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-163">At the prompt, type the following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="f3a7d-164">Paket yüklendikten sonra, Visual Studio çözümünüz Microsoft.Azure.Documents.Client ve Newtonsoft.Json olmak üzere iki yeni başvuru eklenmiş şekilde aşağıdakine benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-164">Once the package is installed, your Visual Studio solution should resemble the following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Çözüm Gezgini'nde JSON veri projesine eklenen iki başvurunun ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <span data-ttu-id="f3a7d-166"><a name="_Toc395637763"></a>4. Adım: ASP.NET MVC uygulamasını ayarlama</span><span class="sxs-lookup"><span data-stu-id="f3a7d-166"><a name="_Toc395637763"></a>Step 4: Set up the ASP.NET MVC application</span></span>
<span data-ttu-id="f3a7d-167">Şimdi bu MVC uygulamasına modeller, görünümler ve denetleyiciler ekleyelim:</span><span class="sxs-lookup"><span data-stu-id="f3a7d-167">Now let's add the models, views, and controllers to this MVC application:</span></span>

* <span data-ttu-id="f3a7d-168">[Model ekleme](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="f3a7d-168">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="f3a7d-169">[Denetleyici ekleme](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="f3a7d-169">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="f3a7d-170">[Görünümler ekleme](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="f3a7d-170">[Add views](#_Toc395637766).</span></span>

### <span data-ttu-id="f3a7d-171"><a name="_Toc395637764"></a>JSON veri modeli ekleme</span><span class="sxs-lookup"><span data-stu-id="f3a7d-171"><a name="_Toc395637764"></a>Add a JSON data model</span></span>
<span data-ttu-id="f3a7d-172">MVC'de **M** olan modeli oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-172">Let's begin by creating the **M** in MVC, the model.</span></span> 

1. <span data-ttu-id="f3a7d-173">**Çözüm Gezgini**'nde **Modeller** klasörüne sağ tıklayın, **Ekle**'ye tıklayın ve ardından **Sınıf**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-173">In **Solution Explorer**, right-click the **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="f3a7d-174">**Yeni Öğe Ekle** iletişim kutusu görünür.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-174">The **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="f3a7d-175">Yeni sınıfınıza **Item.cs** adını verin ve **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-175">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="f3a7d-176">Bu yeni **Item.cs** dosyasında, son *using deyiminden* sonra aşağıdakini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-176">In this new **Item.cs** file, add the following after the last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="f3a7d-177">Şimdi de bu kodu</span><span class="sxs-lookup"><span data-stu-id="f3a7d-177">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="f3a7d-178">aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-178">with the following code.</span></span>
   
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
   
    <span data-ttu-id="f3a7d-179">Azure Cosmos DB'deki tüm veriler kablo üzerinden geçer ve JSON olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-179">All data in Azure Cosmos DB is passed over the wire and stored as JSON.</span></span> <span data-ttu-id="f3a7d-180">JSON.NET tarafından nesnelerinizin seri hale getirilme/seri durumundan çıkarılma yolunu denetlemek için, yeni oluşturduğumuz **Item** sınıfında gösterildiği şekilde **JsonProperty** özniteliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-180">To control the way your objects are serialized/deserialized by JSON.NET you can use the **JsonProperty** attribute as demonstrated in the **Item** class we just created.</span></span> <span data-ttu-id="f3a7d-181">Bunu yapmak **zorunda** değilsiniz ancak özelliklerimin JSON camelCase adlandırma kurallarına uyduğundan emin olmak istiyorum.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-181">You don't **have** to do this but I want to ensure that my properties follow the JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="f3a7d-182">Özellik adının biçimini JSON'a gittiği zaman denetlemenin yanı sıra, **Açıklama** özelliğinde yaptığım gibi .NET özelliklerinizi tamamen yeniden adlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-182">Not only can you control the format of the property name when it goes into JSON, but you can entirely rename your .NET properties like I did with the **Description** property.</span></span> 

### <span data-ttu-id="f3a7d-183"><a name="_Toc395637765"></a>Denetleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="f3a7d-183"><a name="_Toc395637765"></a>Add a controller</span></span>
<span data-ttu-id="f3a7d-184">**M** ile işimiz bitti; şimdi de MVC'deki **C**'yi, yani denetleyici sınıfını oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-184">That takes care of the **M**, now let's create the **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="f3a7d-185">**Çözüm Gezgini**'nde **Denetleyiciler** klasörüne sağ tıklayın, **Ekle**'ye tıklayın ve ardından **Denetleyici**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-185">In **Solution Explorer**, right-click the **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="f3a7d-186">**İskele Ekle** iletişim kutusu görünür.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-186">The **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="f3a7d-187">**MVC 5 Denetleyici - Boş**'u seçin ve ardından **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-187">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![MVC 5 Denetleyici - Boş seçeneği vurgulanmış şekilde İskele Ekle iletişim kutusunun ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="f3a7d-189">Yeni Denetleyicinize **ItemController** adını verin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-189">Name your new Controller, **ItemController.**</span></span>
   
    ![Denetleyici Ekle iletişim kutusunun ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="f3a7d-191">Dosya oluşturulduktan sonra, Visual Studio çözümünüz **Çözüm Gezgini**'nde yeni ItemController.cs dosyasıyla aşağıdakine benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-191">Once the file is created, your Visual Studio solution should resemble the following with the new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="f3a7d-192">Daha önce oluşturduğunuz yeni Item.cs dosyası da gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-192">The new Item.cs file created earlier is also shown.</span></span>
   
    ![Yeni ItemController.cs dosyası ve Item.cs dosyası vurgulanmış şekilde Visual Studio çözümü - Çözüm Gezgini'nin ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="f3a7d-194">ItemController.cs'yi kapatabilirsiniz, buna daha sonra geri döneceğiz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-194">You can close ItemController.cs, we'll come back to it later.</span></span> 

### <span data-ttu-id="f3a7d-195"><a name="_Toc395637766"></a>Görünümler ekleme</span><span class="sxs-lookup"><span data-stu-id="f3a7d-195"><a name="_Toc395637766"></a>Add views</span></span>
<span data-ttu-id="f3a7d-196">Şimdi MVC'deki **V**'yi, yani görünümleri oluşturalım:</span><span class="sxs-lookup"><span data-stu-id="f3a7d-196">Now, let's create the **V** in MVC, the views:</span></span>

* <span data-ttu-id="f3a7d-197">[Öğe Dizini görünümü ekleme](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="f3a7d-197">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="f3a7d-198">[Yeni Öğe görünümü ekleme](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="f3a7d-198">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="f3a7d-199">[Düzenleme Öğesi görünümü ekleme](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="f3a7d-199">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <span data-ttu-id="f3a7d-200"><a name="AddItemIndexView"></a>Öğe Dizini görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="f3a7d-200"><a name="AddItemIndexView"></a>Add an Item Index view</span></span>
1. <span data-ttu-id="f3a7d-201">**Çözüm Gezgini**'nde **Görünümler** klasörünü genişletin, daha önce **ItemController**'ı eklediğinizde Visual Studio'nun sizin için oluşturduğu boş **Öğe** klasörüne sağ tıklayın, **Ekle**'ye tıklayın ve ardından **Görünüm**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-201">In **Solution Explorer**, expand the **Views**  folder, right-click the empty **Item** folder that Visual Studio created for you when you added the **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Görünüm Ekle komutları vurgulanmış şekilde Visual Studio'nun oluşturduğu Öğe klasörünü gösteren Çözüm Gezgini'nin ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="f3a7d-203">**Görünüm Ekle** iletişim kutusunda aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="f3a7d-203">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="f3a7d-204">**Görünüm adı** kutusunda ***Index*** yazın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-204">In the **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="f3a7d-205">**Şablon** kutusunda ***Liste***'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-205">In the **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="f3a7d-206">**Model sınıfı** kutusunda ***Öğe (todo.Models)*** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-206">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="f3a7d-207">Düzen sayfası kutusunda ***~/Views/Shared/_Layout.cshtml*** yazın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-207">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Görünüm Ekle iletişim kutusunu gösteren ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="f3a7d-209">Bu değerlerin tümü ayarlandıktan sonra, **Ekle**'ye tıklayın ve Visual Studio'nun yeni bir şablon görünümü oluşturmasına izin verin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-209">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="f3a7d-210">Tamamlandığında, oluşturulan cshtml dosyasını açar.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-210">Once it is done, it will open the cshtml file  that was created.</span></span> <span data-ttu-id="f3a7d-211">Daha sonra geri döneceğimiz için Visual Studio'daki bu dosyayı kapatabiliriz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-211">We can close that file in Visual Studio as we will come back to it later.</span></span>

#### <span data-ttu-id="f3a7d-212"><a name="AddNewIndexView"></a>Yeni Öğe görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="f3a7d-212"><a name="AddNewIndexView"></a>Add a New Item view</span></span>
<span data-ttu-id="f3a7d-213">**Öğe Dizini** görünümü oluşturmamıza benzer şekilde, şimdi de yeni **Öğeler** oluşturmak için yeni bir görünüm oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-213">Similar to how we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="f3a7d-214">**Çözüm Gezgini**'nde **Öğe** klasörüne tekrar sağ tıklayın, **Ekle**'ye tıklayın ve ardından **Görünüm**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-214">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="f3a7d-215">**Görünüm Ekle** iletişim kutusunda aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="f3a7d-215">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="f3a7d-216">**Görünüm adı** kutusunda ***Create*** yazın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-216">In the **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="f3a7d-217">**Şablon** kutusunda ***Oluştur***'u seçin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-217">In the **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="f3a7d-218">**Model sınıfı** kutusunda ***Öğe (todo.Models)*** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-218">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="f3a7d-219">Düzen sayfası kutusunda ***~/Views/Shared/_Layout.cshtml*** yazın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-219">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="f3a7d-220">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-220">Click **Add**.</span></span>
   
#### <span data-ttu-id="f3a7d-221"><a name="_Toc395888515"></a>Düzenleme Öğesi görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="f3a7d-221"><a name="_Toc395888515"></a>Add an Edit Item view</span></span>
<span data-ttu-id="f3a7d-222">Son olarak, bir **Öğe**'yi düzenlemek için daha önce kullandığımız yolu tekrarlayarak son bir görünüm ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-222">And finally, add one last view for editing an **Item** in the same way as before.</span></span>

1. <span data-ttu-id="f3a7d-223">**Çözüm Gezgini**'nde **Öğe** klasörüne tekrar sağ tıklayın, **Ekle**'ye tıklayın ve ardından **Görünüm**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-223">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="f3a7d-224">**Görünüm Ekle** iletişim kutusunda aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="f3a7d-224">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="f3a7d-225">**Görünüm adı** kutusunda ***Edit*** yazın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-225">In the **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="f3a7d-226">**Şablon** kutusunda ***Düzenle***'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-226">In the **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="f3a7d-227">**Model sınıfı** kutusunda ***Öğe (todo.Models)*** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-227">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="f3a7d-228">Düzen sayfası kutusunda ***~/Views/Shared/_Layout.cshtml*** yazın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-228">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="f3a7d-229">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-229">Click **Add**.</span></span>

<span data-ttu-id="f3a7d-230">Bunu yaptıktan sonra, bu görünümlere daha sonra geri döneceğimiz için Visual Studio'daki tüm cshtml belgelerini kapatın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-230">Once this is done, close all the cshtml documents in Visual Studio as we will return to these views later.</span></span>

## <span data-ttu-id="f3a7d-231"><a name="_Toc395637769"></a>5. Adım: Azure Cosmos DB’yi bağlama</span><span class="sxs-lookup"><span data-stu-id="f3a7d-231"><a name="_Toc395637769"></a>Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="f3a7d-232">Standart MVC işleri hallolduğuna göre, Azure Cosmos DB için kod eklemeye dönelim.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-232">Now that the standard MVC stuff is taken care of, let's turn to adding the code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="f3a7d-233">Bu bölümde, aşağıdakileri işlemek için kod ekleyeceğiz:</span><span class="sxs-lookup"><span data-stu-id="f3a7d-233">In this section, we'll add code to handle the following:</span></span>

* <span data-ttu-id="f3a7d-234">[Tamamlanmamış Öğeleri listeleme](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="f3a7d-234">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="f3a7d-235">[Öğeler ekleme](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="f3a7d-235">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="f3a7d-236">[Öğeleri düzenleme](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="f3a7d-236">[Editing Items](#_Toc395637772).</span></span>

### <span data-ttu-id="f3a7d-237"><a name="_Toc395637770"></a>MVC web uygulamanızda tamamlanmamış Öğeleri listeleme</span><span class="sxs-lookup"><span data-stu-id="f3a7d-237"><a name="_Toc395637770"></a>Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="f3a7d-238">Burada yapılacak ilk şey, Azure Cosmos DB'ye bağlanmayı ve kullanmayı sağlayan tüm mantığı içeren bir sınıf eklemektir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-238">The first thing to do here is add a class that contains all the logic to connect to and use Azure Cosmos DB.</span></span> <span data-ttu-id="f3a7d-239">Bu öğretici için tüm bu mantığı DocumentDBRepository adlı bir depo sınıfına kapsülleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-239">For this tutorial we'll encapsulate all this logic in to a repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="f3a7d-240">**Çözüm Gezgini**'nde projeye sağ tıklayın, **Ekle**'ye tıklayın ve ardından **Sınıf**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-240">In **Solution Explorer**, right-click on the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="f3a7d-241">Yeni sınıfa **DocumentDBRepository** adını verin ve **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-241">Name the new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="f3a7d-242">Yeni oluşturulan **DocumentDBRepository** sınıfında *ad alanı* bildiriminin üstüne aşağıdaki *using deyimlerini* ekleyin</span><span class="sxs-lookup"><span data-stu-id="f3a7d-242">In the newly created **DocumentDBRepository** class and add the following *using statements* above the *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    <span data-ttu-id="f3a7d-243">Şimdi de bu kodu</span><span class="sxs-lookup"><span data-stu-id="f3a7d-243">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="f3a7d-244">aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-244">with the following code.</span></span>
   
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
   
    
3. <span data-ttu-id="f3a7d-245">Bazı değerleri yapılandırmadan okuyoruz, bu nedenle uygulamanızın **Web.config** dosyasını açın ve `<AppSettings>` bölümünün altına aşağıdaki satırları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-245">We're reading some values from configuration, so open the **Web.config** file of your application and add the following lines under the `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter the URI from the Keys blade of the Azure Portal"/>
        <add key="authKey" value="enter the PRIMARY KEY, or the SECONDARY KEY, from the Keys blade of the Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="f3a7d-246">Şimdi de Azure Portal'ın Anahtarlar dikey penceresini kullanarak *endpoint* ve *authKey* değerlerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-246">Now, update the values for *endpoint* and *authKey* using the Keys blade of the Azure Portal.</span></span> <span data-ttu-id="f3a7d-247">Uç nokta ayarının değeri olarak Anahtarlar dikey penceresinden **URI**'yi kullanın ve authKey ayarının değeri olarak Anahtarlar dikey penceresinden **BİRİNCİL ANAHTAR** veya **İKİNCİL ANAHTAR**'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-247">Use the **URI** from the Keys blade as the value of the endpoint setting, and use the **PRIMARY KEY**, or **SECONDARY KEY** from the Keys blade as the value of the authKey setting.</span></span>

    <span data-ttu-id="f3a7d-248">Azure Cosmos DB depoyu şimdi bağlamayı, alır dikkatli uygulama mantığımızı ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-248">That takes care of wiring up the Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="f3a7d-249">Bir yapılacaklar listesi uygulamasıyla yapabilmeyi istediğimiz ilk şey, tamamlanmamış öğeleri görüntülemektir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-249">The first thing we want to be able to do with a todo list application is to display the incomplete items.</span></span>  <span data-ttu-id="f3a7d-250">**DocumentDBRepository** sınıfının içinde herhangi bir yere aşağıdaki kod parçacığını kopyalayıp yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-250">Copy and paste the following code snippet anywhere within the **DocumentDBRepository** class.</span></span>
   
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
2. <span data-ttu-id="f3a7d-251">Daha önce eklediğimiz **ItemController**'ı açın ve ad alanı bildiriminin üstüne aşağıdaki *using deyimlerini* ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-251">Open the **ItemController** we added earlier and add the following *using statements* above the namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="f3a7d-252">Projeniz "todo" olarak adlandırılmamışsa using "todo.Models" deyimini projenizin adını yansıtacak şekilde güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-252">If your project is not named "todo", then you need to update using "todo.Models"; to reflect the name of your project.</span></span>
   
    <span data-ttu-id="f3a7d-253">Şimdi de bu kodu</span><span class="sxs-lookup"><span data-stu-id="f3a7d-253">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="f3a7d-254">aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-254">with the following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="f3a7d-255">**Global.asax.cs**'yi açın ve **Application_Start** yöntemine aşağıdaki satırı ekleyin</span><span class="sxs-lookup"><span data-stu-id="f3a7d-255">Open **Global.asax.cs** and add the following line to the **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="f3a7d-256">Bu noktada çözümünüzün herhangi bir hata olmadan oluşturulabiliyor olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-256">At this point your solution should be able to build without any errors.</span></span>

<span data-ttu-id="f3a7d-257">Uygulamayı şimdi çalıştırırsanız **HomeController**'a ve söz konusu denetleyicinin **Dizin** görünümüne gidersiniz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-257">If you ran the application now, you would go to the **HomeController** and the **Index** view of that controller.</span></span> <span data-ttu-id="f3a7d-258">Başta seçtiğimiz MVC şablonu projesinin varsayılan davranışı budur ancak biz bunu istemiyoruz!</span><span class="sxs-lookup"><span data-stu-id="f3a7d-258">This is the default behavior for the MVC template project we chose at the start but we don't want that!</span></span> <span data-ttu-id="f3a7d-259">Bu davranışı değiştirmek için bu MVC uygulamasındaki yönlendirmeyi değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-259">Let's change the routing on this MVC application to alter this behavior.</span></span>

<span data-ttu-id="f3a7d-260">***App\_Start\RouteConfig.cs***'yi açın, "defaults:" ile başlayan satırı bulun ve aşağıdakine benzeyecek şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-260">Open ***App\_Start\RouteConfig.cs*** and locate the line starting with "defaults:" and change it to resemble the following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="f3a7d-261">Bu, yönlendirme davranışını denetlemek için URL'de bir değer belirtmemeniz durumunda, denetleyici olarak **Giriş** yerine **Öğe**'yi ve görünüm olarak **Dizin**'i kullanmasını ASP.NET MVC'ye söyler.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-261">This now tells ASP.NET MVC that if you have not specified a value in the URL to control the routing behavior that instead of **Home**, use **Item** as the controller and user **Index** as the view.</span></span>

<span data-ttu-id="f3a7d-262">Uygulamayı şimdi çalıştırırsanız uygulama depo sınıfını çağıran ve tamamlanmamış tüm öğeleri **Görünümler**\\**Öğe**\\**Dizin** görünümüne getiren GetItems yöntemini kullanan **ItemController**'ınızı çağırır.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-262">Now if you run the application, it will call into your **ItemController** which will call in to the repository class and use the GetItems method to return all the incomplete items to the **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="f3a7d-263">Bu projeyi şimdi oluşturur ve çalıştırırsanız buna benzeyen bir şey görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-263">If you build and run this project now, you should now see something that looks this.</span></span>    

![Bu veritabanı öğreticisi tarafından oluşturulan yapılacaklar listesi web uygulamasının ekran görüntüsü](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <span data-ttu-id="f3a7d-265"><a name="_Toc395637771"></a>Öğeler ekleme</span><span class="sxs-lookup"><span data-stu-id="f3a7d-265"><a name="_Toc395637771"></a>Adding Items</span></span>
<span data-ttu-id="f3a7d-266">Boş bir kılavuzdan başka şeyler görmek için veritabanımıza biraz öğe ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-266">Let's put some items into our database so we have something more than an empty grid to look at.</span></span>

<span data-ttu-id="f3a7d-267">Azure Cosmos DB'deki kaydı kalıcı hale getirmek için Azure Cosmos DBRepository ve ItemController'a biraz kod ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-267">Let's add some code to  Azure Cosmos DBRepository and ItemController to persist the record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="f3a7d-268">**DocumentDBRepository** sınıfınıza aşağıdaki yöntemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-268">Add the following method to your **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="f3a7d-269">Bu yöntem yalnızca kendisine geçirilen nesneyi alır ve Azure Cosmos DB'de devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-269">This method simply takes an object passed to it and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="f3a7d-270">ItemController.cs dosyasını açın ve sınıfın içine aşağıdaki kod parçacığını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-270">Open the ItemController.cs file and add the following code snippet within the class.</span></span> <span data-ttu-id="f3a7d-271">ASP.NET MVC **Oluştur** eylemi için ne yapacağını bu şekilde bilir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-271">This is how ASP.NET MVC knows what to do for the **Create** action.</span></span> <span data-ttu-id="f3a7d-272">Bu durumda yalnızca daha önce oluşturulan ilişkili Create.cshtml görünümünü işler.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-272">In this case just render the associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="f3a7d-273">Şimdi bu denetleyicide **Oluştur** görünümünden gönderim kabul edecek biraz daha koda ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-273">We now need some more code in this controller that will accept the submission from the **Create** view.</span></span>
3. <span data-ttu-id="f3a7d-274">Bu denetleyici için bir POST formuyla ASP.NET MVC'ye ne yapacağını söyleyen ItemController.cs sınıfına bir sonraki kod blokunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-274">Add the next block of code to the ItemController.cs class that tells ASP.NET MVC what to do with a form POST for this controller.</span></span>
   
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
   
    <span data-ttu-id="f3a7d-275">Bu kod DocumentDBRepository'ye çağrı yapar ve yeni todo öğesini veritabanında kalıcı hale getirmek için CreateItemAsync yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-275">This code calls in to the DocumentDBRepository and uses the CreateItemAsync method to persist the new todo item to the database.</span></span> 
   
    <span data-ttu-id="f3a7d-276">**Güvenlik Notu**: **ValidateAntiForgeryToken** özniteliği burada bu uygulamayı siteler arası istek sahteciliği saldırılarına karşı korunmaya yardımcı olmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-276">**Security Note**: The **ValidateAntiForgeryToken** attribute is used here to help protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="f3a7d-277">Bu özniteliği eklemek tek başına yeterli değildir, görünümlerinizin de bu sahteciliği karşı önleme belirteci ile çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-277">There is more to it than just adding this attribute, your views need to work with this anti-forgery token as well.</span></span> <span data-ttu-id="f3a7d-278">Bu konu hakkında daha fazla bilgi ve bunu doğru uygulamaya yönelik örnekler için lütfen bkz. [Siteler Arası İstek Sahteciliğini Önleme][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="f3a7d-278">For more on the subject, and examples of how to implement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="f3a7d-279">[GitHub][GitHub]'da sağlanan kaynak kodu tam uygulamayı içerir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-279">The source code provided on [GitHub][GitHub] has the full implementation in place.</span></span>
   
    <span data-ttu-id="f3a7d-280">**Güvenlik Notu**: Aşırı gönderim saldırılarına karşı korunmaya yardımcı olmak için yöntem parametresinde **Bind** özniteliğini de kullanırız.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-280">**Security Note**: We also use the **Bind** attribute on the method parameter to help protect against over-posting attacks.</span></span> <span data-ttu-id="f3a7d-281">Daha ayrıntılı bilgi için lütfen bkz. [ASP.NET MVC'de Temel CRUD İşlemleri][Basic CRUD Operations in ASP.NET MVC].</span><span class="sxs-lookup"><span data-stu-id="f3a7d-281">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="f3a7d-282">Veritabanımıza yeni Öğeler eklemek için gereken kod burada son bulur.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-282">This concludes the code required to add new Items to our database.</span></span>

### <span data-ttu-id="f3a7d-283"><a name="_Toc395637772"></a>Öğeleri Düzenleme</span><span class="sxs-lookup"><span data-stu-id="f3a7d-283"><a name="_Toc395637772"></a>Editing Items</span></span>
<span data-ttu-id="f3a7d-284">Yapacağımız son bir şey kaldı, bu da veritabanında **Öğeler**'i düzenleme ve bunları tamamlanmış olarak işaretleme özelliğini eklemektir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-284">There is one last thing for us to do, and that is to add the ability to edit **Items** in the database and to mark them as complete.</span></span> <span data-ttu-id="f3a7d-285">Düzenleme görünümü projeye zaten eklenmişti, bu nedenle yalnızca denetleyicimize ve **DocumentDBRepository** sınıfına biraz kod eklememiz gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-285">The view for editing was already added to the project, so we just need to add some code to our controller and to the **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="f3a7d-286">**DocumentDBRepository** sınıfına aşağıdakileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-286">Add the following to the **DocumentDBRepository** class.</span></span>
   
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
   
    <span data-ttu-id="f3a7d-287">Bu yöntemlerin ilki olan **GetItem**, Azure Cosmos DB'den bir Öğe getirir ve bu öğe **ItemController**'a ve sonra **Düzenle** görünümüne geçirilir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-287">The first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back to the **ItemController** and then on to the **Edit** view.</span></span>
   
    <span data-ttu-id="f3a7d-288">Yeni eklediğimiz yöntemlerin ikincisi, Azure Cosmos DB'deki **Belge**'yi, **ItemController**'dan geçirilen **Belge**'nin sürümüyle değiştirir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-288">The second of the methods we just added replaces the **Document** in Azure Cosmos DB with the version of the **Document** passed in from the **ItemController**.</span></span>
2. <span data-ttu-id="f3a7d-289">Aşağıdakileri **ItemController** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-289">Add the following to the **ItemController** class.</span></span>
   
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
   
    <span data-ttu-id="f3a7d-290">İlk yöntem, kullanıcı **Dizin** görünümünden **Düzenle** bağlantısına tıkladığında meydana gelen Http GET'ini işler.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-290">The first method handles the Http GET that happens when the user clicks on the **Edit** link from the **Index** view.</span></span> <span data-ttu-id="f3a7d-291">Bu yöntem Azure Cosmos DB'den bir [**Belge**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) getirir ve bunu **Düzenle** görünümüne geçirir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-291">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it to the **Edit** view.</span></span>
   
    <span data-ttu-id="f3a7d-292">Ardından, **Düzenle** görünümü **IndexController**'a bir Http POST yapar.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-292">The **Edit** view will then do an Http POST to the **IndexController**.</span></span> 
   
    <span data-ttu-id="f3a7d-293">Eklediğimiz ikinci yöntem, güncelleştirilmiş nesneyi veritabanında kalıcı hale getirmek üzere Azure Cosmos DB'ye geçirir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-293">The second method we added handles passing the updated object to Azure Cosmos DB to be persisted in the database.</span></span>

<span data-ttu-id="f3a7d-294">Hepsi bu; uygulamamızı çalıştırmak, tamamlanmamış **Öğeleri** listelemek, yeni **Öğeler** eklemek ve **Öğeleri** düzenlemek için ihtiyacımız olan her şey bu kadar.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-294">That's it, that is everything we need to run our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <span data-ttu-id="f3a7d-295"><a name="_Toc395637773"></a>6. Adım: Uygulamayı yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f3a7d-295"><a name="_Toc395637773"></a>Step 6: Run the application locally</span></span>
<span data-ttu-id="f3a7d-296">Yerel makinenizde uygulamayı test etmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="f3a7d-296">To test the application on your local machine, do the following:</span></span>

1. <span data-ttu-id="f3a7d-297">Uygulamayı hata ayıklama modunda oluşturmak için Visual Studio'da F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-297">Hit F5 in Visual Studio to build the application in debug mode.</span></span> <span data-ttu-id="f3a7d-298">Bu işlemin uygulamayı oluşturması ve bir tarayıcıyı daha önce gördüğümüz boş kılavuz sayfasıyla başlatması gerekir:</span><span class="sxs-lookup"><span data-stu-id="f3a7d-298">It should build the application and launch a browser with the empty grid page we saw before:</span></span>
   
    ![Bu veritabanı öğreticisi tarafından oluşturulan yapılacaklar listesi web uygulamasının ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="f3a7d-300">**Yeni Oluştur** bağlantısına tıklayın ve **Ad** ve **Açıklama** alanlarına değerler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-300">Click the **Create New** link and add values to the **Name** and **Description** fields.</span></span> <span data-ttu-id="f3a7d-301">**Tamamlandı** onay kutusunu seçmeden bırakın, aksi halde yeni **Öğe** tamamlanmış durumda eklenir ve ilk listede görünmez.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-301">Leave the **Completed** check box unselected otherwise the new **Item** will be added in a completed state and will not appear on the initial list.</span></span>
   
    ![Oluştur görünümünün ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="f3a7d-303">**Oluştur**'a tıklayın, böylece **Dizin** görünümüne geri yönlendirilirsiniz ve **Öğeniz** listede görünür.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-303">Click **Create** and you are redirected back to the **Index** view and your **Item** appears in the list.</span></span>
   
    ![Dizin görünümünün ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="f3a7d-305">Yapılacaklar listenize birkaç **Öğe** daha ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-305">Feel free to add a few more **Items** to your todo list.</span></span>
    
4. <span data-ttu-id="f3a7d-306">Listedeki bir **Öğe**'nin yanındaki **Düzenle**'ye tıklayın, böylece **Tamamlandı** bayrağı dahil olmak üzere nesnenizin herhangi bir özelliğini güncelleştirebileceğiniz **Düzenle** görünümüne gidersiniz.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-306">Click **Edit** next to an **Item** on the list and you are taken to the **Edit** view where you can update any property of your object, including the **Completed** flag.</span></span> <span data-ttu-id="f3a7d-307">**Tamamlandı** bayrağını işaretler ve **Kaydet**'e tıklarsanız **Öğe** tamamlanmamış görevler listesinden kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-307">If you mark the **Complete** flag and click **Save**, the **Item** is removed from the list of incomplete tasks.</span></span>
   
    ![Tamamlandı kutusu işaretlenmiş şekilde Dizin görünümünün ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="f3a7d-309">Uygulamayı test ettikten sonra, uygulamanın hata ayıklamasını durdurmak için Ctrl+F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-309">Once you've tested the app, press Ctrl+F5 to stop debugging the app.</span></span> <span data-ttu-id="f3a7d-310">Dağıtıma hazırsınız!</span><span class="sxs-lookup"><span data-stu-id="f3a7d-310">You're ready to deploy!</span></span>

## <span data-ttu-id="f3a7d-311"><a name="_Toc395637774"></a>7. adım: Azure uygulama hizmeti uygulamaya dağıtma</span><span class="sxs-lookup"><span data-stu-id="f3a7d-311"><a name="_Toc395637774"></a>Step 7: Deploy the application to Azure App Service</span></span> 
<span data-ttu-id="f3a7d-312">Azure Cosmos DB ile düzgün çalışmasını tam uygulama sahip olduğunuza göre bu web uygulamasını Azure App Service'e dağıtmak için yapacağız.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-312">Now that you have the complete application working correctly with Azure Cosmos DB we're going to deploy this web app to Azure App Service.</span></span>  

1. <span data-ttu-id="f3a7d-313">Bu uygulamayı yayımlamak için yapmanız gereken tek şey, **Çözüm Gezgini**'nde projeye sağ tıklamak ve **Yayımla**'ya tıklamaktır.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-313">To publish this application all you need to do is right-click on the project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Çözüm Gezgini'nde Yayımla seçeneğinin ekran görüntüsü](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="f3a7d-315">İçinde **Yayımla** iletişim kutusu, tıklatın **Microsoft Azure App Service**seçeneğini belirleyip **Yeni Oluştur** tıklayın veya bir uygulama hizmeti profili oluşturma **var olanı Seç**  varolan profili kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-315">In the **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** to create an App Service profile, or click **Select Existing** to use an existing profile.</span></span>

    ![Visual Studio'da Yayımla iletişim kutusu](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="f3a7d-317">Var olan bir Azure uygulama hizmeti profiliniz varsa, abonelik adınızı girin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-317">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="f3a7d-318">Kullanım **Görünüm** kaynak grubu veya kaynak türü göre sıralamak için filtre sonra Azure uygulama hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-318">Use the **View** filter to sort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![Visual Studio'da uygulama hizmeti iletişim kutusu](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="f3a7d-320">Yeni bir Azure uygulama hizmeti profili oluşturmak için tıklatın **Yeni Oluştur** içinde **Yayımla** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-320">To create a new Azure App Service profile, click **Create New** in the **Publish** dialog box.</span></span> <span data-ttu-id="f3a7d-321">İçinde **App Service Oluştur** iletişim kutusunda, Web uygulaması adı ve uygun abonelik, kaynak grubu ve uygulama hizmeti planı girin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-321">In the **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Visual Studio'da uygulama hizmeti iletişim kutusu oluşturma](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="f3a7d-323">Visual Studio birkaç saniye içinde web uygulamanızı yayımlamayı bitirecek ve Azure'da çalışan, handiwork görebileceğiniz bir tarayıcıyı başlatacak!</span><span class="sxs-lookup"><span data-stu-id="f3a7d-323">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <span data-ttu-id="f3a7d-324"><a name="_Toc395637775"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f3a7d-324"><a name="_Toc395637775"></a>Next steps</span></span>
<span data-ttu-id="f3a7d-325">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="f3a7d-325">Congratulations!</span></span> <span data-ttu-id="f3a7d-326">Yalnızca ilk ASP.NET MVC Azure Cosmos DB kullanarak web uygulaması oluşturdunuz ve bunu Azure yayımladınız.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-326">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it to Azure.</span></span> <span data-ttu-id="f3a7d-327">Bu öğreticide bulunmayan ayrıntı ve silme işlevleri dahil olmak üzere, tüm uygulamanın kaynak kodu [GitHub][GitHub]'dan indirilebilir veya kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-327">The source code for the complete application, including the detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="f3a7d-328">Uygulamanıza bunları eklemek isterseniz kodu alın ve bu uygulamaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a7d-328">So if you're interested in adding that to your app, grab the code and add it to this app.</span></span>

<span data-ttu-id="f3a7d-329">Uygulamanıza ek işlevsellik eklemek için kullanılabilen API'leri inceleyin [Azure Cosmos DB .NET kitaplığı](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) ve Azure Cosmos DB .NET Kitaplığı'na katkıda bulunmaktan çekinmeyin [GitHub] [GitHub].</span><span class="sxs-lookup"><span data-stu-id="f3a7d-329">To add additional functionality to your application, review the APIs available in the [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free to contribute to the Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
