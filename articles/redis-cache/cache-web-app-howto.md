---
title: "Redis Cache ile Web Uygulamaları oluşturma | Microsoft Docs"
description: "Redis Cache ile Web Uygulaması oluşturmayı öğrenin"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: hero-article
ms.date: 05/09/2017
ms.author: sdanie
ms.openlocfilehash: f23f71cc01eccf17d36885f786de9a7517606803
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-web-app-with-redis-cache"></a><span data-ttu-id="0dc61-103">Redis Cache ile Web Uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="0dc61-103">How to create a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0dc61-104">.NET</span><span class="sxs-lookup"><span data-stu-id="0dc61-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="0dc61-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0dc61-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="0dc61-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="0dc61-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="0dc61-107">Java</span><span class="sxs-lookup"><span data-stu-id="0dc61-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="0dc61-108">Python</span><span class="sxs-lookup"><span data-stu-id="0dc61-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="0dc61-109">Bu öğreticide, ASP.NET web uygulamasının nasıl oluşturulacağını ve Visual Studio 2017 kullanılarak Azure Uygulama Hizmeti’ndeki bir web uygulamasına nasıl dağıtılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-109">This tutorial shows how to create and deploy an ASP.NET web application to a web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="0dc61-110">Örnek uygulama bir veritabanındaki ekip istatistiklerinin listesini görüntüler ve önbellekten veri depolama ve almaya yönelik Azure Redis Cache’i kullanmak için farklı yollar gösterir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-110">The sample application displays a list of team statistics from a database and shows different ways to use Azure Redis Cache to store and retrieve data from the cache.</span></span> <span data-ttu-id="0dc61-111">Öğreticiyi tamamladığınızda, Azure Redis Cache ile en iyi hale getirilmiş ve Azure’da barındırılan, bir veritabanını okuyan ve yazan çalışan bir web uygulamasına sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0dc61-111">When you complete the tutorial you'll have a running web app that reads and writes to a database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="0dc61-112">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="0dc61-112">You'll learn:</span></span>

* <span data-ttu-id="0dc61-113">Visual Studio’da ASP.NET MVC 5 web uygulaması oluşturma.</span><span class="sxs-lookup"><span data-stu-id="0dc61-113">How to create an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="0dc61-114">Entity Framework’ü kullanarak bir veritabanındaki verilere erişme.</span><span class="sxs-lookup"><span data-stu-id="0dc61-114">How to access data from a database using Entity Framework.</span></span>
* <span data-ttu-id="0dc61-115">Azure Redis Cache’i kullanarak veri depolayarak ve alarak veri işlemeyi iyileştirme ve veritabanı yükünü azaltma.</span><span class="sxs-lookup"><span data-stu-id="0dc61-115">How to improve data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="0dc61-116">En iyi 5 ekibi almak için bir Redis sıralanmış kümesi kullanma.</span><span class="sxs-lookup"><span data-stu-id="0dc61-116">How to use a Redis sorted set to retrieve the top 5 teams.</span></span>
* <span data-ttu-id="0dc61-117">Resource Manager şablonunu kullanarak uygulama için Azure kaynakları sağlama.</span><span class="sxs-lookup"><span data-stu-id="0dc61-117">How to provision the Azure resources for the application using a Resource Manager template.</span></span>
* <span data-ttu-id="0dc61-118">Visual Studio kullanarak uygulamayı yayımlama.</span><span class="sxs-lookup"><span data-stu-id="0dc61-118">How to publish the application to Azure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dc61-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0dc61-119">Prerequisites</span></span>
<span data-ttu-id="0dc61-120">Bu öğreticiyi tamamlamak için aşağıdaki ön koşullara sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-120">To complete the tutorial, you must have the following prerequisites.</span></span>

* [<span data-ttu-id="0dc61-121">Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="0dc61-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="0dc61-122">.NET için Azure SDK içeren Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="0dc61-122">Visual Studio 2017 with the Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="0dc61-123">Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="0dc61-123">Azure account</span></span>
<span data-ttu-id="0dc61-124">Öğreticiyi tamamlamak için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-124">You need an Azure account to complete the tutorial.</span></span> <span data-ttu-id="0dc61-125">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0dc61-125">You can:</span></span>

* <span data-ttu-id="0dc61-126">[Ücretsiz bir Azure hesabı açın](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="0dc61-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="0dc61-127">Ücretli Azure hizmetlerini denemek için kullanabileceğiniz krediler alırsınız.</span><span class="sxs-lookup"><span data-stu-id="0dc61-127">You get credits that can be used to try out paid Azure services.</span></span> <span data-ttu-id="0dc61-128">Krediler bitmiş olsa bile hesabı sürdürebilir ve ücretsiz Azure hizmet ve özelliklerinden faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-128">Even after the credits are used up, you can keep the account and use free Azure services and features.</span></span>
* <span data-ttu-id="0dc61-129">[Visual Studio abone avantajları etkinleştirin](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="0dc61-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="0dc61-130">MSDN aboneliğiniz, ücretli Azure hizmetlerinizi kullanabildiğiniz her ay size kredi verir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-the-azure-sdk-for-net"></a><span data-ttu-id="0dc61-131">.NET için Azure SDK içeren Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="0dc61-131">Visual Studio 2017 with the Azure SDK for .NET</span></span>
<span data-ttu-id="0dc61-132">Bu öğretici, [.NET için Azure SDK](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools) içeren Visual Studio 2017 için hazırlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-132">The tutorial is written for Visual Studio 2017 with the [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="0dc61-133">Visual Studio yükleyicisine Azure SDK 2.9.5 dahildir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-133">The Azure SDK 2.9.5 is included with the Visual Studio installer.</span></span>

<span data-ttu-id="0dc61-134">Visual Studio 2015’e sahipseniz, [.NET için Azure SDK](../dotnet-sdk.md) 2.8.2 ile öğreticiyi takip edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-134">If you have Visual Studio 2015, you can follow the tutorial with the [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="0dc61-135">[Visual Studio 2015 için en son Azure SDK’sını buradan indirin](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="0dc61-135">[Download the latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="0dc61-136">Visual Studio’nuz yoksa, SDK ile otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-136">Visual Studio is automatically installed with the SDK if you don't already have it.</span></span> <span data-ttu-id="0dc61-137">Bu öğreticideki bazı ekranlar gösterilenlerden farklı görünebilir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-137">Some screens may look different from the illustrations shown in this tutorial.</span></span>

<span data-ttu-id="0dc61-138">Visual Studio 2013’ünüz varsa, [Visual Studio 2013 için en son Azure SDK'sını indirebilirsiniz](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="0dc61-138">If you have Visual Studio 2013, you can [download the latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="0dc61-139">Bu öğreticideki bazı ekranlar gösterilenlerden farklı görünebilir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-139">Some screens may look different from the illustrations shown in this tutorial.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="0dc61-140">Visual Studio projesini oluşturma</span><span class="sxs-lookup"><span data-stu-id="0dc61-140">Create the Visual Studio project</span></span>
1. <span data-ttu-id="0dc61-141">Visual Studio’yu açın ve **Dosya**, **Yeni**, **Proje**’yi tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="0dc61-142">**Şablonlar** listesindeki **Visual C#** öğesini genişletin, **Bulut**’u seçin ve **ASP.NET Web Uygulaması**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-142">Expand the **Visual C#** node in the **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="0dc61-143">**.NET Framework 4.5.2** veya daha yüksek bir sürümün seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0dc61-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="0dc61-144">**Ad** metin kutusunda **ContosoTeamStats** yazın ve **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-144">Type **ContosoTeamStats** into the **Name** textbox and click **OK**.</span></span>
   
    ![Proje oluşturma][cache-create-project]
3. <span data-ttu-id="0dc61-146">Proje türü olarak **MVC**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-146">Select **MVC** as the project type.</span></span> 

    <span data-ttu-id="0dc61-147">**Kimlik Doğrulama** ayarları için **Kimlik Doğrulaması Yok** seçeneğinin belirtildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="0dc61-147">Ensure that **No Authentication** is specified for the **Authentication** settings.</span></span> <span data-ttu-id="0dc61-148">Visual Studio sürümünüze bağlı olarak, varsayılan değer başka bir şeye ayarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-148">Depending on your version of Visual Studio, the default may be set to something else.</span></span> <span data-ttu-id="0dc61-149">Değiştirmek için **Kimlik Doğrulamasını Değiştir**’e tıklayıp **Kimlik Doğrulaması Yok**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-149">To change it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="0dc61-150">Visual Studio 2015 ile takip ediyorsanız, **Bulutta barındır** onay kutusunun işaretini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-150">If you are following along with Visual Studio 2015, clear the **Host in the cloud** checkbox.</span></span> <span data-ttu-id="0dc61-151">Öğreticinin sonraki adımlarında [Azure kaynaklarını hazırlayacak](#provision-the-azure-resources) ve [uygulamayı Azure’a yayımlayacaksınız](#publish-the-application-to-azure).</span><span class="sxs-lookup"><span data-stu-id="0dc61-151">You'll [provision the Azure resources](#provision-the-azure-resources) and [publish the application to Azure](#publish-the-application-to-azure) in subsequent steps in the tutorial.</span></span> <span data-ttu-id="0dc61-152">**Buluttaki konak** öğesini işaretli bırakarak Visual Studio’dan bir App Service web uygulaması hazırlama örneği için, bkz. [ASP.NET ve Visual Studio kullanarak Azure App Service’deki Web Uygulamalarını kullanmaya başlama](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0dc61-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in the cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![Proje şablonu seçme][cache-select-template]
4. <span data-ttu-id="0dc61-154">Projeyi oluşturmak için **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-154">Click **OK** to create the project.</span></span>

## <a name="create-the-aspnet-mvc-application"></a><span data-ttu-id="0dc61-155">4. Adım: ASP.NET MVC uygulamasını oluşturma</span><span class="sxs-lookup"><span data-stu-id="0dc61-155">Create the ASP.NET MVC application</span></span>
<span data-ttu-id="0dc61-156">Öğreticinin bu bölümünde, bir veritabanındaki ekip istatistiklerini okuyan ve görüntüleyen temel uygulamayı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0dc61-156">In this section of the tutorial, you'll create the basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="0dc61-157">Entity Framework NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="0dc61-157">Add the Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="0dc61-158">Modeli ekleme</span><span class="sxs-lookup"><span data-stu-id="0dc61-158">Add the model</span></span>](#add-the-model)
* [<span data-ttu-id="0dc61-159">Denetleyiciyi ekleme</span><span class="sxs-lookup"><span data-stu-id="0dc61-159">Add the controller</span></span>](#add-the-controller)
* [<span data-ttu-id="0dc61-160">Görünümleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0dc61-160">Configure the views</span></span>](#configure-the-views)

### <a name="add-the-entity-framework-nuget-package"></a><span data-ttu-id="0dc61-161">Entity Framework NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="0dc61-161">Add the Entity Framework NuGet package</span></span>

1. <span data-ttu-id="0dc61-162">**Araçlar** menüsünden **NuGet Paket Yöneticisi**, **Paket Yöneticisi Konsolu**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-162">Click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="0dc61-163">**Paket Yöneticisi Konsolu** penceresinde aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-163">Run the following command from the **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="0dc61-164">Bu paket hakkında daha fazla bilgi için [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet sayfasına bakın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-164">For more information about this package, see the [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-the-model"></a><span data-ttu-id="0dc61-165">Modeli ekleme</span><span class="sxs-lookup"><span data-stu-id="0dc61-165">Add the model</span></span>
1. <span data-ttu-id="0dc61-166">**Çözüm Gezgini**’nde **Modeller**’e sağ tıklayın ve **Ekle**, **Sınıf**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Model ekleme][cache-model-add-class]
2. <span data-ttu-id="0dc61-168">Sınıf adı için `Team` girin ve **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-168">Enter `Team` for the class name and click **Add**.</span></span>
   
    ![Model sınıfı ekleme][cache-model-add-class-dialog]
3. <span data-ttu-id="0dc61-170">`Team.cs` dosyasının üst tarafındaki `using` deyimini aşağıdaki `using` deyimleriyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-170">Replace the `using` statements at the top of the `Team.cs` file with the following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="0dc61-171">`Team` sınıfının tanımını, bazı diğer Entity Framework yardımcı sınıflarının yanı sıra güncelleştirilmiş `Team` sınıf tanımını içeren aşağıdaki kod parçacığı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-171">Replace the definition of the `Team` class with the following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="0dc61-172">Bu öğreticide kullanılan Entity Framework için ilk kod yaklaşımı hakkında daha fazla bilgi için, bkz. [Yeni bir veritabanına ilk kod](https://msdn.microsoft.com/data/jj193542).</span><span class="sxs-lookup"><span data-stu-id="0dc61-172">For more information on the code first approach to Entity Framework that's used in this tutorial, see [Code first to a new database](https://msdn.microsoft.com/data/jj193542).</span></span>

    ```c#
    public class Team
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public int Wins { get; set; }
        public int Losses { get; set; }
        public int Ties { get; set; }
    
        static public void PlayGames(IEnumerable<Team> teams)
        {
            // Simple random generation of statistics.
            Random r = new Random();
    
            foreach (var t in teams)
            {
                t.Wins = r.Next(33);
                t.Losses = r.Next(33);
                t.Ties = r.Next(0, 5);
            }
        }
    }
    
    public class TeamContext : DbContext
    {
        public TeamContext()
            : base("TeamContext")
        {
        }
    
        public DbSet<Team> Teams { get; set; }
    }
    
    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
    {
        protected override void Seed(TeamContext context)
        {
            var teams = new List<Team>
            {
                new Team{Name="Adventure Works Cycles"},
                new Team{Name="Alpine Ski House"},
                new Team{Name="Blue Yonder Airlines"},
                new Team{Name="Coho Vineyard"},
                new Team{Name="Contoso, Ltd."},
                new Team{Name="Fabrikam, Inc."},
                new Team{Name="Lucerne Publishing"},
                new Team{Name="Northwind Traders"},
                new Team{Name="Consolidated Messenger"},
                new Team{Name="Fourth Coffee"},
                new Team{Name="Graphic Design Institute"},
                new Team{Name="Nod Publishers"}
            };
    
            Team.PlayGames(teams);
    
            teams.ForEach(t => context.Teams.Add(t));
            context.SaveChanges();
        }
    }
    
    public class TeamConfiguration : DbConfiguration
    {
        public TeamConfiguration()
        {
            SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
        }
    }
    ```


1. <span data-ttu-id="0dc61-173">**Çözüm Gezgini**’nde, **web.config**’i açmak için sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-173">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="0dc61-175">Aşağıdaki `connectionStrings` bölümünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-175">Add the following `connectionStrings` section.</span></span> <span data-ttu-id="0dc61-176">Bağlantı dizesinin adını Entity Framework veritabanı bağlamı sınıfının adı olan `TeamContext` ile eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-176">The name of the connection string must match the name of the Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="0dc61-177">Aşağıdaki örnekte gösterildiği gibi, yeni `connectionStrings` bölümünü `configSections` bölümünün sonuna ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-177">You can add the new `connectionStrings` section so that it follows `configSections`, as shown in the following example.</span></span>

    ```xml
    <configuration>
      <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
      </configSections>
      <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
      </connectionStrings>
      ...
      ```

    > [!NOTE]
    > <span data-ttu-id="0dc61-178">Bağlantı dizeniz, öğreticiyi tamamlamak için kullanılan Visual Studio ve SQL Server Express sürümüne bağlı olarak farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-178">Your connection string may be different depending on the version of Visual Studio and SQL Server Express edition used to complete the tutorial.</span></span> <span data-ttu-id="0dc61-179">Web.config şablonu, yüklemenizle eşleşecek şekilde yapılandırılmalıdır ve `(LocalDB)\v11.0` (SQL Server Express 2012’den) ya da `Data Source=(LocalDB)\MSSQLLocalDB` (SQL Server Express 2014 ve daha yeni sürümlerden) gibi `Data Source` girişleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-179">The web.config template should be configured to match your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="0dc61-180">Bağlantı dizeleri ve SQL Express sürümleri hakkında daha fazla bilgi için bkz. [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span><span class="sxs-lookup"><span data-stu-id="0dc61-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-the-controller"></a><span data-ttu-id="0dc61-181">Denetleyiciyi ekleme</span><span class="sxs-lookup"><span data-stu-id="0dc61-181">Add the controller</span></span>
1. <span data-ttu-id="0dc61-182">Projeyi derlemek için **F6**’ya basın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-182">Press **F6** to build the project.</span></span> 
2. <span data-ttu-id="0dc61-183">**Çözüm Gezgini**'nde **Denetleyiciler** klasörüne sağ tıklayın ve **Ekle**, **Denetleyici**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-183">In **Solution Explorer**, right-click the **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Denetleyici ekleme][cache-add-controller]
3. <span data-ttu-id="0dc61-185">**Görünümlere sahip MVC 5 Denetleyici, Entity Framework kullanarak** öğesini seçin ve **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="0dc61-186">**Ekle**’ye tıkladıktan sonra herhangi bir hata alırsanız, önce projeyi oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0dc61-186">If you get an error after clicking **Add**, ensure that you have built the project first.</span></span>
   
    ![Denetleyici sınıfı ekleme][cache-add-controller-class]
4. <span data-ttu-id="0dc61-188">**Model sınıfı** açılır listesinden **Ekip (ContosoTeamStats.Models)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-188">Select **Team (ContosoTeamStats.Models)** from the **Model class** drop-down list.</span></span> <span data-ttu-id="0dc61-189">**Veri bağlamı** açılır listesinden **TeamContext (ContosoTeamStats.Models)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-189">Select **TeamContext (ContosoTeamStats.Models)** from the **Data context class** drop-down list.</span></span> <span data-ttu-id="0dc61-190">**Denetleyici** adı metin kutusuna `TeamsController` yazın (otomatik olarak doldurulmamışsa).</span><span class="sxs-lookup"><span data-stu-id="0dc61-190">Type `TeamsController` in the **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="0dc61-191">Denetleyici sınıfını oluşturmak ve varsayılan görünümleri eklemek için **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-191">Click **Add** to create the controller class and add the default views.</span></span>
   
    ![Denetleyici yapılandırma][cache-configure-controller]
5. <span data-ttu-id="0dc61-193">**Çözüm Gezgini**’nde, **Global.asax** öğesini genişletin ve **Global.asax.cs**’yi açmak için çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** to open it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="0dc61-195">Aşağıdaki iki `using` deyimini dosyanın üst tarafındaki diğer `using` deyimlerinin altına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-195">Add the following two `using` statements at the top of the file under the other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="0dc61-196">`Application_Start` yönteminin sonuna aşağıdaki kod satırını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-196">Add the following line of code at the end of the `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="0dc61-197">**Çözüm Gezgini**’nde, `App_Start` öğesini genişletin ve `RouteConfig.cs` öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="0dc61-199">Aşağıdaki örnekte gösterildiği gibi `controller = "Home"` öğesini `RegisterRoutes` yöntemindeki kod `controller = "Teams"` ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-199">Replace `controller = "Home"` in the following code in the `RegisterRoutes` method with `controller = "Teams"` as shown in the following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-the-views"></a><span data-ttu-id="0dc61-200">Görünümleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0dc61-200">Configure the views</span></span>
1. <span data-ttu-id="0dc61-201">**Çözüm Gezgini**’nde, **Görünümler** klasörünü ve ardından **Paylaşılan** klasörünü genişletin ve **_Layout.cshtml** öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-201">In **Solution Explorer**, expand the **Views** folder and then the **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="0dc61-203">`title` öğesinin içeriğini değiştirin ve aşağıdaki örnekte gösterildiği gibi `My ASP.NET Application` öğesini `Contoso Team Stats` ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-203">Change the contents of the `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in the following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="0dc61-204">`body` bölümünde, ilk `Html.ActionLink` deyimini güncelleştirin ve `Application name` öğesini `Contoso Team Stats` ile ve `Home` öğesini `Teams` ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-204">In the `body` section, update the first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="0dc61-205">Önce: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="0dc61-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="0dc61-206">Sonra: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="0dc61-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Kod değişiklikleri][cache-layout-cshtml-code]
2. <span data-ttu-id="0dc61-208">Uygulamayı derleyip çalıştırmak için **Ctrl+F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-208">Press **Ctrl+F5** to build and run the application.</span></span> <span data-ttu-id="0dc61-209">Uygulamasının bu sürümü, sonuçları doğrudan veritabanından okur.</span><span class="sxs-lookup"><span data-stu-id="0dc61-209">This version of the application reads the results directly from the database.</span></span> <span data-ttu-id="0dc61-210">**Yeni Oluştur**, **Düzenle**, **Ayrıntılar** ve **Sil** eylemlerinin **Görünümlere sahip MVC 5 Denetleyici, Entity Framework kullanarak** iskelesi tarafından otomatik olarak uygulamaya eklendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-210">Note the **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added to the application by the **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="0dc61-211">Öğreticinin sonraki bölümünde, veri erişimini iyileştirmek ve uygulamaya ek özellikler sağlamak için Redis Cache ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-211">In the next section of the tutorial you'll add Redis Cache to optimize the data access and provide additional features to the application.</span></span>

![Başlangıç uygulaması][cache-starter-application]

## <a name="configure-the-application-to-use-redis-cache"></a><span data-ttu-id="0dc61-213">Redis Cache’i kullanmak için uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0dc61-213">Configure the application to use Redis Cache</span></span>
<span data-ttu-id="0dc61-214">Öğreticinin bu bölümünde, [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) önbellek istemcisini kullanarak bir Azure Redis Cache’ten Contoso ekip istatistiklerini depolamak ve almak için örnek uygulamayı yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="0dc61-214">In this section of the tutorial, you'll configure the sample application to store and retrieve Contoso team statistics from an Azure Redis Cache instance by using the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="0dc61-215">StackExchange.Redis kullanmak için uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0dc61-215">Configure the application to use StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="0dc61-216">Önbellek veya veritabanından sonuçları döndürmek için TeamsController sınıfını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="0dc61-216">Update the TeamsController class to return results from the cache or the database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="0dc61-217">Oluştur, Düzenle ve Sil metotlarını önbellek ile çalışacak şekilde güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="0dc61-217">Update the Create, Edit, and Delete methods to work with the cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="0dc61-218">Ekipler Dizini görünümünü önbellek ile çalışacak şekilde güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="0dc61-218">Update the Teams Index view to work with the cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-the-application-to-use-stackexchangeredis"></a><span data-ttu-id="0dc61-219">StackExchange.Redis kullanmak için uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0dc61-219">Configure the application to use StackExchange.Redis</span></span>
1. <span data-ttu-id="0dc61-220">Visual Studio’da StackExchange.Redis NuGet paketi kullanarak bir istemci uygulamasını yapılandırmak için, **Araçlar** menüsünden **NuGet Paket Yöneticisi**, **Paket Yöneticisi Konsolu**’nu seçin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-220">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="0dc61-221">`Package Manager Console` penceresinden aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-221">Run the following command from the `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="0dc61-222">NuGet paketi, StackExchange.Redis Cache istemcisiyle Azure Redis Cache’e erişmek üzere istemci uygulamanız için gerekli derleme başvurularını ekler.</span><span class="sxs-lookup"><span data-stu-id="0dc61-222">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span></span> <span data-ttu-id="0dc61-223">`StackExchange.Redis` istemci kitaplığının tanımlayıcı adlı bir sürümünü kullanmak istiyorsanız `StackExchange.Redis.StrongName` paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-223">If you prefer to use a strong-named version of the `StackExchange.Redis` client library, install the `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="0dc61-224">**Çözüm Gezgini**’nde, **Denetleyiciler** klasörünü genişletin ve **TeamsController.cs** öğesini açmak için çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-224">In **Solution Explorer**, expand the **Controllers** folder and double-click **TeamsController.cs** to open it.</span></span>
   
    ![Ekip denetleyicisi][cache-teamscontroller]
4. <span data-ttu-id="0dc61-226">**TeamsController.cs** deyimlerini kullanarak aşağıdaki iki `using` deyimini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-226">Add the following two `using` statements to **TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="0dc61-227">Aşağıdaki iki özelliği `TeamsController` sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-227">Add the following two properties to the `TeamsController` class.</span></span>

    ```c#   
    // Redis Connection string info
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

6. <span data-ttu-id="0dc61-228">Bilgisayarınızda `WebAppPlusCacheAppSecrets.config` adlı bir dosya oluşturun ve örnek karar içinde uygulamanızın kaynak kodu ile denetlenmeyecek bir konuma yerleştirin, başka bir yerde denetlemeyi seçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with the source code of your sample application, should you decide to check it in somewhere.</span></span> <span data-ttu-id="0dc61-229">Bu örnekte, `AppSettingsSecrets.config` dosyası `C:\AppSecrets\WebAppPlusCacheAppSecrets.config` konumunda bulunur.</span><span class="sxs-lookup"><span data-stu-id="0dc61-229">In this example the `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="0dc61-230">`WebAppPlusCacheAppSecrets.config` dosyasını düzenleyin ve aşağıdaki içerikleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-230">Edit the `WebAppPlusCacheAppSecrets.config` file and add the following contents.</span></span> <span data-ttu-id="0dc61-231">Uygulamayı yerel olarak çalıştırırsanız, Azure Redis Cache örneğinize bağlanmak için bu bilgiler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-231">If you run the application locally this information is used to connect to your Azure Redis Cache instance.</span></span> <span data-ttu-id="0dc61-232">Öğreticide daha sonra bir Azure Redis Cache örneği hazırlayacak ve önbellek adı ve parolasını güncelleştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-232">Later in the tutorial you'll provision an Azure Redis Cache instance and update the cache name and password.</span></span> <span data-ttu-id="0dc61-233">Örnek uygulamayı yerel olarak çalıştırmayı düşünmüyorsanız, Azure’a dağıtırken uygulama Web Uygulaması için önbellek bağlantı bilgilerini bu dosya yerine uygulama ayarlarından aldığı için bu dosyayı oluşturma ve sonraki adımları atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-233">If you don't plan to run the sample application locally you can skip the creation of this file and the subsequent steps that reference the file, because when you deploy to Azure the application retrieves the cache connection information from the app setting for the Web App and not from this file.</span></span> <span data-ttu-id="0dc61-234">`WebAppPlusCacheAppSecrets.config` öğesi uygulamanızla birlikte Azure’a dağıtılmadığı için, uygulamayı yerel olarak çalıştırmayacağınız sürece ihtiyacınız olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-234">Since the `WebAppPlusCacheAppSecrets.config` is not deployed to Azure with your application, you don't need it unless you are going to run the application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="0dc61-235">**Çözüm Gezgini**’nde, **web.config**’i açmak için sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-235">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="0dc61-237">Aşağıdaki `file` özniteliğini `appSettings` öğesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-237">Add the following `file` attribute to the `appSettings` element.</span></span> <span data-ttu-id="0dc61-238">Farklı bir dosya adı veya konumu kullandıysanız, örnekte gösterilenlerin yerine bu değerleri koyun.</span><span class="sxs-lookup"><span data-stu-id="0dc61-238">If you used a different file name or location, substitute those values for the ones shown in the example.</span></span>
   
   * <span data-ttu-id="0dc61-239">Önce: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="0dc61-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="0dc61-240">Sonra: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="0dc61-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="0dc61-241">ASP.NET çalışma zamanı, `<appSettings>` öğesindeki biçimlendirmeye sahip harici dosyasının içeriğini birleştirir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-241">The ASP.NET runtime merges the contents of the external file with the markup in the `<appSettings>` element.</span></span> <span data-ttu-id="0dc61-242">Belirtilen dosya bulunamazsa, çalışma zamanı dosya özniteliğini yok sayar.</span><span class="sxs-lookup"><span data-stu-id="0dc61-242">The runtime ignores the file attribute if the specified file cannot be found.</span></span> <span data-ttu-id="0dc61-243">Gizli anahtarlarınız (önbelleğinize bağlantı dizisi) uygulamanız için kaynak kodun bir parçası olarak dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="0dc61-243">Your secrets (the connection string to your cache) are not included as part of the source code for the application.</span></span> <span data-ttu-id="0dc61-244">Web uygulamanızı Azure’a dağıtırken, `WebAppPlusCacheAppSecrests.config` dosyası dağıtılmaz (istediğiniz gibi).</span><span class="sxs-lookup"><span data-stu-id="0dc61-244">When you deploy your web app to Azure, the `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="0dc61-245">Bu gizli anahtarları Azure’da belirtmenin birkaç yolu vardır ve bir sonraki öğretici adımında [Azure kaynaklarını hazırlarken](#provision-the-azure-resources) sizin için otomatik olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-245">There are several ways to specify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision the Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="0dc61-246">Azure'daki gizli anahtarlarla çalışma hakkında daha fazla bilgi için, bkz. [Parolaları ve diğer hassas verileri ASP.NET ve Azure App Service’e dağıtmak için en iyi yöntemler](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span><span class="sxs-lookup"><span data-stu-id="0dc61-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database"></a><span data-ttu-id="0dc61-247">Önbellek veya veritabanından sonuçları döndürmek için TeamsController sınıfını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="0dc61-247">Update the TeamsController class to return results from the cache or the database</span></span>
<span data-ttu-id="0dc61-248">Bu örnekte, ekip istatistikleri veritabanı veya önbellekten alınabilir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-248">In this sample, team statistics can be retrieved from the database or from the cache.</span></span> <span data-ttu-id="0dc61-249">Ekip istatistikleri seri hale getirilmiş bir `List<Team>` ve ayrıca, Redis veri türleri kullanılarak sıralanmış bir küme olarak veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-249">Team statistics are stored in the cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="0dc61-250">Bir sıralanmış kümeden öğeleri alırken, belirli öğeler için bazı, tümü veya sorgu alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="0dc61-251">Bu örnekte, kazanma sayısına göre sıralanan en iyi 5 ekip için sıralanmış kümeyi sorgulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0dc61-251">In this sample you'll query the sorted set for the top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="0dc61-252">Azure Redis Cache’i kullanabilmek için ekip istatistiklerini önbellekte çoklu biçimlerde depolamak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-252">It is not required to store the team statistics in multiple formats in the cache in order to use Azure Redis Cache.</span></span> <span data-ttu-id="0dc61-253">Bu öğretici, verileri önbelleğe almak için kullanabileceğiniz farklı yol ve farklı veri türlerinin bazılarını göstermek için birden çok biçim kullanır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-253">This tutorial uses multiple formats to demonstrate some of the different ways and different data types you can use to cache data.</span></span>
> 
> 

1. <span data-ttu-id="0dc61-254">Aşağıdaki `using` deyimlerini `TeamsController.cs` dosyasının üst tarafındaki diğer `using` deyimleri ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-254">Add the following `using` statements to the `TeamsController.cs` file at the top with the other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="0dc61-255">Geçerli `public ActionResult Index()` yöntemi uygulamasını aşağıdaki uygulama ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-255">Replace the current `public ActionResult Index()` method implementation with the following implementation.</span></span>

    ```c#
    // GET: Teams
    public ActionResult Index(string actionType, string resultType)
    {
        List<Team> teams = null;

        switch(actionType)
        {
            case "playGames": // Play a new season of games.
                PlayGames();
                break;

            case "clearCache": // Clear the results from the cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild the database with sample data.
                RebuildDB();
                break;
        }

        // Measure the time it takes to retrieve the results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve the top 5 teams from the sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from the cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from the database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add the elapsed time of the operation to the ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="0dc61-256">Önceki kod parçacığında eklenen switch deyiminden `playGames`, `clearCache` ve `rebuildDB` eylem türlerini uygulamak için aşağıdaki üç yöntemi `TeamsController` sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-256">Add the following three methods to the `TeamsController` class to implement the `playGames`, `clearCache`, and `rebuildDB` action types from the switch statement added in the previous code snippet.</span></span>
   
    <span data-ttu-id="0dc61-257">`PlayGames` yöntemi, oyun sezonunu taklit ederek ekip istatistiklerini güncelleştirir, sonuçları veritabanına kaydeder ve artık güncel olmayan verileri veritabanından temizler.</span><span class="sxs-lookup"><span data-stu-id="0dc61-257">The `PlayGames` method updates the team statistics by simulating a season of games, saves the results to the database, and clears the now outdated data from the cache.</span></span>

    ```c#
    void PlayGames()
    {
        ViewBag.msg += "Updating team statistics. ";
        // Play a "season" of games.
        var teams = from t in db.Teams
                    select t;

        Team.PlayGames(teams);

        db.SaveChanges();

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="0dc61-258">`RebuildDB` yöntemi, varsayılan ekip kümesine sahip veritabanını yeniden başlatır, bunlar için istatistikler oluşturur ve artık güncel olmayan verileri veritabanından temizler.</span><span class="sxs-lookup"><span data-stu-id="0dc61-258">The `RebuildDB` method reinitializes the database with the default set of teams, generates statistics for them, and clears the now outdated data from the cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize the database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="0dc61-259">`ClearCachedTeams` yöntemi önbelleğe alınan tüm ekip istatistiklerini önbellekten kaldırır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-259">The `ClearCachedTeams` method removes any cached team statistics from the cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="0dc61-260">Önbellek ve veritabanından ekip istatistiklerini almanın çeşitli yollarını uygulamak için aşağıdaki dört yöntemi `TeamsController` sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-260">Add the following four methods to the `TeamsController` class to implement the various ways of retrieving the team statistics from the cache and the database.</span></span> <span data-ttu-id="0dc61-261">Bu yöntemlerin her biri daha sonra görünüm tarafından görüntülenen bir `List<Team>` döndürür.</span><span class="sxs-lookup"><span data-stu-id="0dc61-261">Each of these methods returns a `List<Team>` which is then displayed by the view.</span></span>
   
    <span data-ttu-id="0dc61-262">`GetFromDB` yöntemi veritabanından ekip istatistiklerini okur.</span><span class="sxs-lookup"><span data-stu-id="0dc61-262">The `GetFromDB` method reads the team statistics from the database.</span></span>
   
    ```c#
    List<Team> GetFromDB()
    {
        ViewBag.msg += "Results read from DB. ";
        var results = from t in db.Teams
            orderby t.Wins descending
            select t; 

        return results.ToList<Team>();
    }
    ```

    <span data-ttu-id="0dc61-263">`GetFromList` yöntemi önbellekteki ekip istatistiklerini seri hale getirilmiş bir `List<Team>` olarak okur.</span><span class="sxs-lookup"><span data-stu-id="0dc61-263">The `GetFromList` method reads the team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="0dc61-264">Önbellek isabetsizliği varsa, ekip istatistikleri veritabanından okunur ve ardından gelecek sefer için önbellekte depolanır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-264">If there is a cache miss, the team statistics are read from the database and then stored in the cache for next time.</span></span> <span data-ttu-id="0dc61-265">Bu örnekte, önbelleğe veya önbellekten .NET nesnelerini seri hale getirmek için JSON.NEY serileştirmeyi kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-265">In this sample we're using JSON.NET serialization to serialize the .NET objects to and from the cache.</span></span> <span data-ttu-id="0dc61-266">Daha fazla bilgi için, bkz. [Azure Redis Cache’te .NET nesneleri ile çalışma](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span><span class="sxs-lookup"><span data-stu-id="0dc61-266">For more information, see [How to work with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

    ```c#
    List<Team> GetFromList()
    {
        List<Team> teams = null;

        IDatabase cache = Connection.GetDatabase();
        string serializedTeams = cache.StringGet("teamsList");
        if (!String.IsNullOrEmpty(serializedTeams))
        {
            teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

            ViewBag.msg += "List read from cache. ";
        }
        else
        {
            ViewBag.msg += "Teams list cache miss. ";
            // Get from database and store in cache
            teams = GetFromDB();

            ViewBag.msg += "Storing results to cache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="0dc61-267">`GetFromSortedSet` yöntemi önbelleğe alınan bir sıralanmış kümeden ekip istatistiklerini okur.</span><span class="sxs-lookup"><span data-stu-id="0dc61-267">The `GetFromSortedSet` method reads the team statistics from a cached sorted set.</span></span> <span data-ttu-id="0dc61-268">Önbellek isabetsizliği varsa, ekip istatistikleri veritabanından okunur ve ardından bir sıralanmış küme olarak önbellekte depolanır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-268">If there is a cache miss, the team statistics are read from the database and stored in the cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
        if (teamsSortedSet.Count() > 0)
        {
            ViewBag.msg += "Reading sorted set from cache. ";
            teams = new List<Team>();
            foreach (var t in teamsSortedSet)
            {
                Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                teams.Add(tt);
            }
        }
        else
        {
            ViewBag.msg += "Teams sorted set cache miss. ";

            // Read from DB
            teams = GetFromDB();

            ViewBag.msg += "Storing results to cache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding to sorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="0dc61-269">`GetFromSortedSetTop5` yöntemi önbelleğe alınan sıralanmış kümesinden en iyi 5 ekibi okur.</span><span class="sxs-lookup"><span data-stu-id="0dc61-269">The `GetFromSortedSetTop5` method reads the top 5 teams from the cached sorted set.</span></span> <span data-ttu-id="0dc61-270">Bu, `teamsSortedSet` anahtarının varlığı için önbelleği denetleyerek başlar.</span><span class="sxs-lookup"><span data-stu-id="0dc61-270">It starts by checking the cache for the existence of the `teamsSortedSet` key.</span></span> <span data-ttu-id="0dc61-271">Bu anahtar yoksa, ekip istatistikleri okumak ve bunları önbellekte depolamak için `GetFromSortedSet` yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-271">If this key is not present, the `GetFromSortedSet` method is called to read the team statistics and store them in the cache.</span></span> <span data-ttu-id="0dc61-272">Daha sonra önbelleğe alınan sıralanmış küme, döndürülen en iyi 5 takım için sorgulanır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-272">Next, the cached sorted set is queried for the top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load the entire sorted set into the cache.
            GetFromSortedSet();

            // Retrieve the top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get the top 5 teams from the sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-the-create-edit-and-delete-methods-to-work-with-the-cache"></a><span data-ttu-id="0dc61-273">Önbellek ile çalışacak şekilde Oluştur, Düzenle ve Sil yöntemlerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="0dc61-273">Update the Create, Edit, and Delete methods to work with the cache</span></span>
<span data-ttu-id="0dc61-274">Bu örneğin bir parçası olarak oluşturulan iskele kurma kodu ekip ekleme, düzenleme ve silme yöntemlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-274">The scaffolding code that was generated as part of this sample includes methods to add, edit, and delete teams.</span></span> <span data-ttu-id="0dc61-275">Bir ekip her eklendiğinde, düzenlendiğinde veya kaldırıldığında önbellekteki veriler güncel olmayan hale gelir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-275">Anytime a team is added, edited, or removed, the data in the cache becomes outdated.</span></span> <span data-ttu-id="0dc61-276">Bu bölümde, önbelleğin veritabanı ile eşitlenmemiş olmaması için önbelleğe alınan ekipleri temizlemek üzere bu üç yöntemi değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-276">In this section you'll modify these three methods to clear the cached teams so that the cache won't be out of sync with the database.</span></span>

1. <span data-ttu-id="0dc61-277">`TeamsController` sınıfındaki `Create(Team team)` yöntemine göz atın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-277">Browse to the `Create(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="0dc61-278">Aşağıdaki örnekte gösterildiği gibi `ClearCachedTeams` yöntemine bir çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-278">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Create
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="0dc61-279">`TeamsController` sınıfındaki `Edit(Team team)` yöntemine göz atın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-279">Browse to the `Edit(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="0dc61-280">Aşağıdaki örnekte gösterildiği gibi `ClearCachedTeams` yöntemine bir çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-280">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="0dc61-281">`TeamsController` sınıfındaki `DeleteConfirmed(int id)` yöntemine göz atın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-281">Browse to the `DeleteConfirmed(int id)` method in the `TeamsController` class.</span></span> <span data-ttu-id="0dc61-282">Aşağıdaki örnekte gösterildiği gibi `ClearCachedTeams` yöntemine bir çağrı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-282">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, the cache is out of date.
        // Clear the cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-the-teams-index-view-to-work-with-the-cache"></a><span data-ttu-id="0dc61-283">Önbellek ile çalışacak şekilde Ekipler Dizini görünümünü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="0dc61-283">Update the Teams Index view to work with the cache</span></span>
1. <span data-ttu-id="0dc61-284">**Çözüm Gezgini**’nde, **Görünümler** klasörünü ve ardından **Ekipler** klasörünü genişletin ve **Index.cshtml** öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-284">In **Solution Explorer**, expand the **Views** folder, then the **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="0dc61-286">Dosyanın en üstüne yakın bir yerde, aşağıdaki paragraf öğesini arayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-286">Near the top of the file, look for the following paragraph element.</span></span>
   
    ![Eylem tablosu][cache-teams-index-table]
   
    <span data-ttu-id="0dc61-288">Bu, yeni bir ekip oluşturma bağlantısıdır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-288">This is the link to create a new team.</span></span> <span data-ttu-id="0dc61-289">Paragraf öğesini aşağıdaki tablo ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-289">Replace the paragraph element with the following table.</span></span> <span data-ttu-id="0dc61-290">Bu tabloda yeni bir ekip oluşturmak, yeni bir oyun sezonu oynama, önbelleği temizleme, önbellekten ekipleri çeşitli biçimlerde alma, veritabanından ekipleri alma ve yeni örnek veriler ile veritabanını yeniden oluşturma eylemlerinin bağlantılarını içermektedir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-290">This table has action links for creating a new team, playing a new season of games, clearing the cache, retrieving the teams from the cache in several formats, retrieving the teams from the database, and rebuilding the database with fresh sample data.</span></span>

    ```html
    <table class="table">
        <tr>
            <td>
                @Html.ActionLink("Create New", "Create")
            </td>
            <td>
                @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
            </td>
            <td>
                @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
            </td>
            <td>
                @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
            </td>
            <td>
                @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
            </td>
            <td>
                @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
            </td>
            <td>
                @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
            </td>
            <td>
                @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
            </td>
        </tr>    
    </table>
    ```


1. <span data-ttu-id="0dc61-291">**Index.cshtml** dosyasının aşağısına kaydırın ve dosyada bulunan son tablodaki son satır olması için aşağıdaki `tr` öğesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-291">Scroll to the bottom of the **Index.cshtml** file and add the following `tr` element so that it is the last row in the last table in the file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="0dc61-292">Bu satırda, geçerli işlem hakkında durum raporu içeren `ViewBag.Msg` değerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-292">This row displays the value of `ViewBag.Msg` which contains a status report about the current operation.</span></span> <span data-ttu-id="0dc61-293">Önceki adımdan herhangi bir eylem bağlantısına tıkladığınızda `ViewBag.Msg` değeri ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-293">The `ViewBag.Msg` is set when you click any of the action links from the previous step.</span></span>   
   
    ![Durum iletisi][cache-status-message]
2. <span data-ttu-id="0dc61-295">Projeyi derlemek için **F6**’ya basın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-295">Press **F6** to build the project.</span></span>

## <a name="provision-the-azure-resources"></a><span data-ttu-id="0dc61-296">Azure kaynaklarını hazırlama</span><span class="sxs-lookup"><span data-stu-id="0dc61-296">Provision the Azure resources</span></span>
<span data-ttu-id="0dc61-297">Uygulamanızı Azure’da barındırmak için önce uygulamanızın gerektirdiği Azure hizmetlerini hazırlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-297">To host your application in Azure, you must first provision the Azure services that your application requires.</span></span> <span data-ttu-id="0dc61-298">Bu öğreticideki örnek uygulama aşağıdaki Azure hizmetlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-298">The sample application in this tutorial uses the following Azure services.</span></span>

* <span data-ttu-id="0dc61-299">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="0dc61-299">Azure Redis Cache</span></span>
* <span data-ttu-id="0dc61-300">App Service Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="0dc61-300">App Service Web App</span></span>
* <span data-ttu-id="0dc61-301">SQL Database</span><span class="sxs-lookup"><span data-stu-id="0dc61-301">SQL Database</span></span>

<span data-ttu-id="0dc61-302">Bu hizmetleri yeni veya seçtiğiniz mevcut bir kaynak grubuna dağıtmak için, aşağıdaki **Azure’a Dağıt** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-302">To deploy these services to a new or existing resource group of your choice, click the following **Deploy to Azure** button.</span></span>

<span data-ttu-id="0dc61-303">[![Azure’a Dağıt][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="0dc61-303">[![Deploy to Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="0dc61-304">Bu **Azure’a Dağıt** düğmesi, bu hizmetleri hazırlamak ve SQL Database için bağlantı dizesini ve Azure Redis Cache bağlantı dizesi için uygulama ayarlarını belirlemek için [Web Uygulaması oluşturma artı Redis Cache artı SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Hızlı Başlangıç](https://github.com/Azure/azure-quickstart-templates) şablonunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-304">This **Deploy to Azure** button uses the [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template to provision these services and set the connection string for the SQL Database and the application setting for the Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="0dc61-305">Bir Azure hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir Azure hesabı oluşturabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="0dc61-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="0dc61-306">**Azure’a Dağıt** düğmesine tıkladığınızda sizi Azure portalına götürür ve şablon tarafından açıklanan kaynakların oluşturma işlemini başlatır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-306">Clicking the **Deploy to Azure** button takes you to the Azure portal and initiates the process of creating the resources described by the template.</span></span>

![Azure’a Dağıt][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="0dc61-308">**Temel Bilgiler** bölümünde, kullanılacak Azure aboneliğini ve mevcut bir kaynak grubu seçin veya yeni bir tane oluşturun ve kaynak grubu konumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-308">In the **Basics** section, select the Azure subscription to use, and select an existing resource group or create a new one, and specify the resource group location.</span></span>
2. <span data-ttu-id="0dc61-309">**Ayarlar** bölümünde bir **Yönetici Kullanıcı Adı** (**admin** adını kullanmayın), **Yönetici Parolaları** ve **Veritabanı Adı** belirtin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-309">In the **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="0dc61-310">Diğer parametreler, ücretsiz bir App Service barındırma planı ve ücretsiz katmanı ile birlikte sunulmayan SQL Veritabanı ve Azure Redis Cache için daha düşük maliyetli seçenekler sunmak için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-310">The other parameters are configured for a free App Service hosting plan, and lower-cost options for the SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![Azure’a Dağıt][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="0dc61-312">Ayarları yapılandırdıktan sonra sayfanın en altına inin, hüküm ve koşulları okuyun ve **Yukarıda belirtilen hüküm ve koşulları kabul ediyorum** onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-312">After configuring the desired settings, scroll to the end of the page, read the terms and conditions, and check the **I agree to the terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="0dc61-313">Kaynakları sağlamaya başlamak için **Satın al**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-313">To begin provisioning the resources, click **Purchase**.</span></span>

<span data-ttu-id="0dc61-314">Dağıtımınızın ilerlemesini görüntülemek için bildirim simgesine ve **Dağıtım başladı** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-314">To view the progress of your deployment, click the notification icon and click **Deployment started**.</span></span>

![Dağıtım başladı][cache-deployment-started]

<span data-ttu-id="0dc61-316">**Microsoft.Template** dikey penceresinde dağıtımınızın durumunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-316">You can view the status of your deployment on the **Microsoft.Template** blade.</span></span>

![Azure’a Dağıt][cache-deploy-to-azure-step-3]

<span data-ttu-id="0dc61-318">Hazırlama işlemi tamamlandığında, uygulamanızı Visual Studio’dan Azure’a yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-318">When provisioning is complete, you can publish your application to Azure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="0dc61-319">Sağlama işlemi sırasında oluşabilecek tüm hatalar **Microsoft.Template** dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-319">Any errors that may occur during the provisioning process are displayed on the **Microsoft.Template** blade.</span></span> <span data-ttu-id="0dc61-320">Abonelik başına çok fazla SQL Server veya çok fazla Ücretsiz App Service barındırma planı yaygın hatalardır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="0dc61-321">Tüm sorunları çözümleyin ve **Microsoft.Template** dikey penceresinde **Yeniden Dağıt** veya bu öğreticideki **Azure’a Dağıt** düğmesine tıklayarak işlemi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-321">Resolve any errors and restart the process by clicking **Redeploy** on the **Microsoft.Template** blade or the **Deploy to Azure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-the-application-to-azure"></a><span data-ttu-id="0dc61-322">Uygulamayı Azure’a yayımlama</span><span class="sxs-lookup"><span data-stu-id="0dc61-322">Publish the application to Azure</span></span>
<span data-ttu-id="0dc61-323">Öğreticinin bu adımında, uygulamayı Azure’a yayımlayacak ve bulutta çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="0dc61-323">In this step of the tutorial, you'll publish the application to Azure and run it in the cloud.</span></span>

1. <span data-ttu-id="0dc61-324">Visual Studio’da **ContosoTeamStats** öğesine sağ tıklayın ve **Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-324">Right-click the **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Yayımlama][cache-publish-app]
2. <span data-ttu-id="0dc61-326">**Microsoft Azure App Service**’e tıklayın, **Var Olanı Seç**’i seçin ve **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Yayımlama][cache-publish-to-app-service]
3. <span data-ttu-id="0dc61-328">Azure kaynakları oluşturulurken kullanılan aboneliği seçin, kaynakları içeren kaynak grubunu genişletin ve istediğiniz Web Uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-328">Select the subscription used when creating the Azure resources, expand the resource group containing the resources, and select the desired Web App.</span></span> <span data-ttu-id="0dc61-329">**Azure’a Dağıt** düğmesini kullandıysanız Web Uygulaması adınız **webSite** ile başlar ve bazı ek karakterlerle devam eder.</span><span class="sxs-lookup"><span data-stu-id="0dc61-329">If you used the **Deploy to Azure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Web Uygulaması Seçme][cache-select-web-app]
4. <span data-ttu-id="0dc61-331">Yayımlama işlemine başlamak için **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-331">Click **OK** to begin the publishing process.</span></span> <span data-ttu-id="0dc61-332">Birkaç dakika sonra yayımlama işlemi tamamlanır ve örnek uygulama çalıştırılarak bir tarayıcı başlatılır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-332">After a few moments the publishing process completes and a browser is launched with the running sample application.</span></span> <span data-ttu-id="0dc61-333">Doğrularken veya yayımlarken ve henüz tamamlanan uygulama için Azure kaynakları için işlem hazırlarken bir DNS hatası alırsanız, birkaç dakika bekleyin ve tekrar deneyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-333">If you get a DNS error when validating or publishing, and the provisioning process for the Azure resources for the application has just recently completed, wait a moment and try again.</span></span>
   
    ![Önbellek eklendi][cache-added-to-application]

<span data-ttu-id="0dc61-335">Aşağıdaki tablo örnek uygulamadaki her eylem bağlantısını açıklar.</span><span class="sxs-lookup"><span data-stu-id="0dc61-335">The following table describes each action link from the sample application.</span></span>

| <span data-ttu-id="0dc61-336">Eylem</span><span class="sxs-lookup"><span data-stu-id="0dc61-336">Action</span></span> | <span data-ttu-id="0dc61-337">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0dc61-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0dc61-338">Yeni Oluştur</span><span class="sxs-lookup"><span data-stu-id="0dc61-338">Create New</span></span> |<span data-ttu-id="0dc61-339">Yeni bir Ekip oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0dc61-339">Create a new Team.</span></span> |
| <span data-ttu-id="0dc61-340">Sezonu Oynat</span><span class="sxs-lookup"><span data-stu-id="0dc61-340">Play Season</span></span> |<span data-ttu-id="0dc61-341">Oyun sezonunu oynatın, ekip istatistiklerini güncelleştirin ve veritabanından tüm güncel olmayan ekip verilerini temizleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-341">Play a season of games, update the team stats, and clear any outdated team data from the cache.</span></span> |
| <span data-ttu-id="0dc61-342">Önbelleği Temizle</span><span class="sxs-lookup"><span data-stu-id="0dc61-342">Clear Cache</span></span> |<span data-ttu-id="0dc61-343">Önbellekten ekip istatistiklerini temizleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-343">Clear the team stats from the cache.</span></span> |
| <span data-ttu-id="0dc61-344">Önbellekten Liste</span><span class="sxs-lookup"><span data-stu-id="0dc61-344">List from Cache</span></span> |<span data-ttu-id="0dc61-345">Önbellekten ekip istatistiklerini alın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-345">Retrieve the team stats from the cache.</span></span> <span data-ttu-id="0dc61-346">Önbellek isabetsizliği varsa, veritabanından istatistikleri yükleyin ve bir sonraki seferde önbelleğe kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-346">If there is a cache miss, load the stats from the database and save to the cache for next time.</span></span> |
| <span data-ttu-id="0dc61-347">Önbellekten Sıralanmış Küme</span><span class="sxs-lookup"><span data-stu-id="0dc61-347">Sorted Set from Cache</span></span> |<span data-ttu-id="0dc61-348">Bir sıralanmış küme kullanarak önbellekten en iyi istatistiklerini alın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-348">Retrieve the team stats from the cache using a sorted set.</span></span> <span data-ttu-id="0dc61-349">Önbellek isabetsizliği varsa, veritabanından istatistikleri yükleyin ve bir sıralanmış küme kullanarak önbelleğe kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-349">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="0dc61-350">Önbellekteki En İyi 5 Ekip</span><span class="sxs-lookup"><span data-stu-id="0dc61-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="0dc61-351">Bir sıralanmış küme kullanarak önbellekten en iyi 5 ekibi alın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-351">Retrieve the top 5 teams from the cache using a sorted set.</span></span> <span data-ttu-id="0dc61-352">Önbellek isabetsizliği varsa, veritabanından istatistikleri yükleyin ve bir sıralanmış küme kullanarak önbelleğe kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-352">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="0dc61-353">DB’den yükleme</span><span class="sxs-lookup"><span data-stu-id="0dc61-353">Load from DB</span></span> |<span data-ttu-id="0dc61-354">Veritabanından ekip istatistiklerini alın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-354">Retrieve the team stats from the database.</span></span> |
| <span data-ttu-id="0dc61-355">DB Yeniden Oluşturma</span><span class="sxs-lookup"><span data-stu-id="0dc61-355">Rebuild DB</span></span> |<span data-ttu-id="0dc61-356">Veritabanını yeniden oluşturun ve örnek ekip verileri ile yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-356">Rebuild the database and reload it with sample team data.</span></span> |
| <span data-ttu-id="0dc61-357">Düzenle / Ayrıntılar / Sil</span><span class="sxs-lookup"><span data-stu-id="0dc61-357">Edit / Details / Delete</span></span> |<span data-ttu-id="0dc61-358">Bir ekibi düzenleyin, ekibin ayrıntılarını görüntüleyin, ekibi silin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="0dc61-359">Eylemlerden bazılarına tıklayın ve farklı kaynaklardan veri alma denemeleri yapın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-359">Click some of the actions and experiment with retrieving the data from the different sources.</span></span> <span data-ttu-id="0dc61-360">Veritabanı veya önbellekten veri almanın çeşitli yollarını tamamlamak için gereken zaman içindeki farklılıklar değildir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-360">Not the differences in the time it takes to complete the various ways of retrieving the data from the database and the cache.</span></span>

## <a name="delete-the-resources-when-you-are-finished-with-the-application"></a><span data-ttu-id="0dc61-361">Uygulama ile işiniz bittiğinde kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="0dc61-361">Delete the resources when you are finished with the application</span></span>
<span data-ttu-id="0dc61-362">Örnek öğretici uygulamasıyla işiniz bittiğinde, maliyet ve kaynakları korumak için kullanılan Azure kaynaklarını silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-362">When you are finished with the sample tutorial application, you can delete the Azure resources used in order to conserve cost and resources.</span></span> <span data-ttu-id="0dc61-363">**Azure kaynaklarını hazırlama** bölümünde [Azure’a Dağıt](#provision-the-azure-resources) düğmesini kullanırsanız ve tüm kaynaklarınız aynı grupta bulunuyorsa, kaynak grubunu silerek bunları tek bir işlemde silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-363">If you use the **Deploy to Azure** button in the [Provision the Azure resources](#provision-the-azure-resources) section and all of your resources are contained in the same resource group, you can delete them together in one operation by deleting the resource group.</span></span>

1. <span data-ttu-id="0dc61-364">[Azure portalında](https://portal.azure.com) oturum açın ve **Kaynak grupları**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-364">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="0dc61-365">**Öğeleri filtrele...** metin kutusuna kaynak grubunuzun adını yazın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-365">Type the name of your resource group into the **Filter items...** textbox.</span></span>
3. <span data-ttu-id="0dc61-366">Kaynak grubunuzun sağındaki **...** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-366">Click **...** to the right of your resource group.</span></span>
4. <span data-ttu-id="0dc61-367">**Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-367">Click **Delete**.</span></span>
   
    ![Sil][cache-delete-resource-group]
5. <span data-ttu-id="0dc61-369">Kaynak grubunuzun adını yazın ve **Sil**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-369">Type the name of your resource group and click **Delete**.</span></span>
   
    ![Silmeyi onayla][cache-delete-confirm]

<span data-ttu-id="0dc61-371">Birkaç dakika sonra kaynak grubu ve içerdiği kaynakların tümü silinir.</span><span class="sxs-lookup"><span data-stu-id="0dc61-371">After a few moments the resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0dc61-372">Bir kaynak grubunu silme işleminin geri alınamaz olduğunu ve kaynak grubunun ve içindeki tüm kaynakların kalıcı olarak silindiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-372">Note that deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span></span> <span data-ttu-id="0dc61-373">Yanlış kaynak grubunu veya kaynakları yanlışlıkla silmediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="0dc61-373">Make sure that you do not accidentally delete the wrong resource group or resources.</span></span> <span data-ttu-id="0dc61-374">Bu örneği mevcut bir kaynak grubunda barındırmak için kaynaklar oluşturduysanız, her kaynağı kendi ilgili dikey penceresinden tek tek silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-374">If you created the resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-the-sample-application-on-your-local-machine"></a><span data-ttu-id="0dc61-375">Örnek uygulamayı yerel makinenizde çalıştırma</span><span class="sxs-lookup"><span data-stu-id="0dc61-375">Run the sample application on your local machine</span></span>
<span data-ttu-id="0dc61-376">Uygulamayı makinenizde yerel olarak çalıştırmak için, verilerinizi önbelleğe almak üzere bir Azure Redis Cache örneğine ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-376">To run the application locally on your machine, you need an Azure Redis Cache instance in which to cache your data.</span></span> 

* <span data-ttu-id="0dc61-377">Önceki bölümde açıklandığı gibi Azure uygulamanızı yayımladıysanız, bu adım sırasında sağlanan Azure Redis Cache örneğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-377">If you have published your application to Azure as described in the previous section, you can use the Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="0dc61-378">Mevcut başka bir Azure Redis Cache örneğiniz varsa, bu örneği yerel olarak çalıştırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-378">If you have another existing Azure Redis Cache instance, you can use that to run this sample locally.</span></span>
* <span data-ttu-id="0dc61-379">Bir Azure Redis Cache örneği oluşturmanız gerekiyorsa, [Önbellek oluşturma](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache) makalesindeki adımları uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dc61-379">If you need to create an Azure Redis Cache instance, you can follow the steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="0dc61-380">Kullanılacak önbelleği seçtikten veya oluşturduktan sonra, Azure portalında önbelleğe göz atın ve önbelleğiniz için [konak adı](cache-configure.md#properties) ve [erişim anahtarlarını](cache-configure.md#access-keys) alın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-380">Once you have selected or created the cache to use, browse to the cache in the Azure portal and retrieve the [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="0dc61-381">Yönergeler için bkz. [Redis önbelleği ayarlarını yapılandırma](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="0dc61-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="0dc61-382">İstediğiniz düzenleyiciyi kullanarak bu öğreticinin [Redis Cache’i kullanmak için uygulamayı yapılandırma](#configure-the-application-to-use-redis-cache) adımında oluşturduğunuz `WebAppPlusCacheAppSecrets.config` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-382">Open the `WebAppPlusCacheAppSecrets.config` file that you created during the [Configure the application to use Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using the editor of your choice.</span></span>
2. <span data-ttu-id="0dc61-383">`value` özniteliğini düzenleyin ve `MyCache.redis.cache.windows.net` öğesini önbelleğinizin [konak adı](cache-configure.md#properties) ile değiştirin ve parola olarak önbelleğinizin [birincil veya ikincil anahtarını](cache-configure.md#access-keys) belirtin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-383">Edit the `value` attribute and replace `MyCache.redis.cache.windows.net` with the [host name](cache-configure.md#properties) of your cache, and specify either the [primary or secondary key](cache-configure.md#access-keys) of your cache as the password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="0dc61-384">Uygulamayı çalıştırmak için **Ctrl+F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-384">Press **Ctrl+F5** to run the application.</span></span>

> [!NOTE]
> <span data-ttu-id="0dc61-385">Veritabanı da dahil olmak üzere uygulama yerel olarak çalıştığı ve Redis Cache’in Azure’da barındırıldığı için, önbellek veritabanı altında gerçekleştirmek için görünebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-385">Note that because the application, including the database, is running locally and the Redis Cache is hosted in Azure, the cache may appear to under-perform the database.</span></span> <span data-ttu-id="0dc61-386">En iyi performans için, istemci uygulaması ve Azure Redis Cache örneği aynı konumda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0dc61-386">For best performance, the client application and Azure Redis Cache instance should be in the same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0dc61-387">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0dc61-387">Next steps</span></span>
* <span data-ttu-id="0dc61-388">[ASP.NET](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) sitesinde [ASP.NET MVC 5 ile Çalışmaya Başlama](http://asp.net/) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on the [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="0dc61-389">App Service’te ASP.NET Web Uygulaması oluşturmaya yönelik daha fazla örnek için [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [tanıtımı](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/) içindeki [Azure Uygulama Hizmeti’nde ASP.NET web uygulaması oluşturma ve dağıtma](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="0dc61-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="0dc61-390">HealthClinic.biz tanıtımından daha fazla hızlı başlangıç ipuçları için bkz. [Azure Geliştirici Araçları Hızlı Başlangıç İpuçları](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="0dc61-390">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="0dc61-391">Bu öğreticide kullanılan Entity Framework için [Yeni bir veritabanına ilk kod](https://msdn.microsoft.com/data/jj193542) yaklaşımı hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-391">Learn more about the [Code first to a new database](https://msdn.microsoft.com/data/jj193542) approach to Entity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="0dc61-392">[Azure App Service’deki web uygulamaları](../app-service-web/app-service-web-overview.md) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="0dc61-393">Azure portalındaki önbelleğinizi nasıl [izleyeceğinizi](cache-how-to-monitor.md) öğrenin.</span><span class="sxs-lookup"><span data-stu-id="0dc61-393">Learn how to [monitor](cache-how-to-monitor.md) your cache in the Azure portal.</span></span>
* <span data-ttu-id="0dc61-394">Azure Redis Cache premium özelliklerini keşfedin</span><span class="sxs-lookup"><span data-stu-id="0dc61-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="0dc61-395">Premium Azure Redis Cache için kalıcılığı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0dc61-395">How to configure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="0dc61-396">Premium Azure Redis Cache için kümeleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0dc61-396">How to configure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="0dc61-397">Premium Azure Redis Cache için Sanal Ağ desteğini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0dc61-397">How to configure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="0dc61-398">Boyut, işleme ve premium önbelleklere sahip bant genişliği hakkında daha fazla bilgi için, bkz. [Azure Redis Cache SSS](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span><span class="sxs-lookup"><span data-stu-id="0dc61-398">See the [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

<!-- IMAGES -->
[cache-starter-application]: ./media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: ./media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: ./media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: ./media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: ./media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: ./media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: ./media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: ./media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: ./media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: ./media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: ./media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: ./media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: ./media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: ./media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: ./media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: ./media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: ./media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: ./media/cache-web-app-howto/cache-status-message.png
[deploybutton]: ./media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: ./media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: ./media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: ./media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: ./media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: ./media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: ./media/cache-web-app-howto/cache-delete-confirm.png

