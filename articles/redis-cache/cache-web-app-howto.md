---
title: "aaaHow toocreate Redis önbelleği ile Web uygulaması | Microsoft Docs"
description: "Bilgi nasıl toocreate Redis önbelleği ile Web uygulaması"
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
ms.openlocfilehash: d3e6df97b06fdf9032570dc360944be4bd7715de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-web-app-with-redis-cache"></a><span data-ttu-id="21fa6-103">Nasıl toocreate Redis önbelleği ile Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="21fa6-103">How toocreate a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="21fa6-104">.NET</span><span class="sxs-lookup"><span data-stu-id="21fa6-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="21fa6-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="21fa6-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="21fa6-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="21fa6-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="21fa6-107">Java</span><span class="sxs-lookup"><span data-stu-id="21fa6-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="21fa6-108">Python</span><span class="sxs-lookup"><span data-stu-id="21fa6-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="21fa6-109">Bu öğreticide gösterilmiştir nasıl toocreate ve ASP.NET web uygulaması tooa web uygulamasını Azure App Service'de Visual Studio 2017 kullanarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-109">This tutorial shows how toocreate and deploy an ASP.NET web application tooa web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="21fa6-110">Hello örnek uygulama bir veritabanındaki ekip istatistiklerinin listesini görüntüler ve farklı şekillerde toouse Azure Redis önbelleği toostore gösterir ve hello önbellekten veri alın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-110">hello sample application displays a list of team statistics from a database and shows different ways toouse Azure Redis Cache toostore and retrieve data from hello cache.</span></span> <span data-ttu-id="21fa6-111">Merhaba öğreticiyi tamamladığınızda okur ve Azure Redis önbelleği ile en iyi duruma getirilmiş ve barındırılan tooa veritabanı, Azure'da yazan çalışan bir web uygulamasına sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="21fa6-111">When you complete hello tutorial you'll have a running web app that reads and writes tooa database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="21fa6-112">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="21fa6-112">You'll learn:</span></span>

* <span data-ttu-id="21fa6-113">Nasıl toocreate bir ASP.NET MVC 5 web uygulamasını Visual Studio'da.</span><span class="sxs-lookup"><span data-stu-id="21fa6-113">How toocreate an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="21fa6-114">Nasıl Entity Framework kullanarak bir veritabanındaki tooaccess verileri.</span><span class="sxs-lookup"><span data-stu-id="21fa6-114">How tooaccess data from a database using Entity Framework.</span></span>
* <span data-ttu-id="21fa6-115">Nasıl tooimprove veri işleme ve depolama ve Azure Redis önbelleği kullanılarak veri alma veritabanı yükünü azaltma.</span><span class="sxs-lookup"><span data-stu-id="21fa6-115">How tooimprove data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="21fa6-116">Nasıl toouse bir Redis kümesi tooretrieve hello en iyi 5 ekibi sıralanır.</span><span class="sxs-lookup"><span data-stu-id="21fa6-116">How toouse a Redis sorted set tooretrieve hello top 5 teams.</span></span>
* <span data-ttu-id="21fa6-117">Nasıl tooprovision Resource Manager şablonu kullanarak Merhaba uygulaması için Azure kaynaklarını hello.</span><span class="sxs-lookup"><span data-stu-id="21fa6-117">How tooprovision hello Azure resources for hello application using a Resource Manager template.</span></span>
* <span data-ttu-id="21fa6-118">Nasıl toopublish, Visual Studio kullanarak uygulama tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="21fa6-118">How toopublish hello application tooAzure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21fa6-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="21fa6-119">Prerequisites</span></span>
<span data-ttu-id="21fa6-120">toocomplete hello Öğreticisi önkoşulları aşağıdaki hello olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="21fa6-120">toocomplete hello tutorial, you must have hello following prerequisites.</span></span>

* [<span data-ttu-id="21fa6-121">Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="21fa6-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="21fa6-122">Merhaba .NET için Azure SDK ile Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="21fa6-122">Visual Studio 2017 with hello Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="21fa6-123">Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="21fa6-123">Azure account</span></span>
<span data-ttu-id="21fa6-124">Bir Azure hesabı toocomplete hello öğretici gerekir.</span><span class="sxs-lookup"><span data-stu-id="21fa6-124">You need an Azure account toocomplete hello tutorial.</span></span> <span data-ttu-id="21fa6-125">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="21fa6-125">You can:</span></span>

* <span data-ttu-id="21fa6-126">[Ücretsiz bir Azure hesabı açın](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="21fa6-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="21fa6-127">Out kullanılan tootry Ücretli Azure hizmetlerini olabilir krediler alırsınız.</span><span class="sxs-lookup"><span data-stu-id="21fa6-127">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="21fa6-128">Hatta hello krediler bitmiş olsa, hello hesabı sürdürebilir ve ücretsiz Azure hizmetlerini ve özellikleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-128">Even after hello credits are used up, you can keep hello account and use free Azure services and features.</span></span>
* <span data-ttu-id="21fa6-129">[Visual Studio abone avantajları etkinleştirin](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="21fa6-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="21fa6-130">MSDN aboneliğiniz, ücretli Azure hizmetlerinizi kullanabildiğiniz her ay size kredi verir.</span><span class="sxs-lookup"><span data-stu-id="21fa6-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a><span data-ttu-id="21fa6-131">Merhaba .NET için Azure SDK ile Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="21fa6-131">Visual Studio 2017 with hello Azure SDK for .NET</span></span>
<span data-ttu-id="21fa6-132">Başlangıç öğreticisi için Visual Studio 2017 hello ile yazılmış [.NET için Azure SDK](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span><span class="sxs-lookup"><span data-stu-id="21fa6-132">hello tutorial is written for Visual Studio 2017 with hello [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="21fa6-133">Hello Azure SDK'sı 2.9.5 hello Visual Studio Yükleyicisi ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="21fa6-133">hello Azure SDK 2.9.5 is included with hello Visual Studio installer.</span></span>

<span data-ttu-id="21fa6-134">Visual Studio 2015 varsa, hello hello öğreticiyi izleyebilirsiniz [.NET için Azure SDK](../dotnet-sdk.md) 2.8.2 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="21fa6-134">If you have Visual Studio 2015, you can follow hello tutorial with hello [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="21fa6-135">[Yükleme son Azure SDK'sını buradan Visual Studio 2015 için hello](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="21fa6-135">[Download hello latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="21fa6-136">Zaten yoksa, visual Studio SDK hello ile otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="21fa6-136">Visual Studio is automatically installed with hello SDK if you don't already have it.</span></span> <span data-ttu-id="21fa6-137">Bazı ekranlar Bu öğreticide gösterilen hello çizimler farklı görünebilir.</span><span class="sxs-lookup"><span data-stu-id="21fa6-137">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

<span data-ttu-id="21fa6-138">Visual Studio 2013 varsa [indirme Visual Studio 2013 için en son Azure SDK'sını hello](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="21fa6-138">If you have Visual Studio 2013, you can [download hello latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="21fa6-139">Bazı ekranlar Bu öğreticide gösterilen hello çizimler farklı görünebilir.</span><span class="sxs-lookup"><span data-stu-id="21fa6-139">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

## <a name="create-hello-visual-studio-project"></a><span data-ttu-id="21fa6-140">Merhaba Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="21fa6-140">Create hello Visual Studio project</span></span>
1. <span data-ttu-id="21fa6-141">Visual Studio’yu açın ve **Dosya**, **Yeni**, **Proje**’yi tıklayın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="21fa6-142">Merhaba genişletin **Visual C#** hello düğümünde **şablonları** listesinde **bulut**, tıklatıp **ASP.NET Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="21fa6-142">Expand hello **Visual C#** node in hello **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="21fa6-143">**.NET Framework 4.5.2** veya daha yüksek bir sürümün seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="21fa6-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="21fa6-144">Tür **ContosoTeamStats** hello içine **adı** textbox tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="21fa6-144">Type **ContosoTeamStats** into hello **Name** textbox and click **OK**.</span></span>
   
    ![Proje oluşturma][cache-create-project]
3. <span data-ttu-id="21fa6-146">Seçin **MVC** hello proje türü olarak.</span><span class="sxs-lookup"><span data-stu-id="21fa6-146">Select **MVC** as hello project type.</span></span> 

    <span data-ttu-id="21fa6-147">Emin **doğrulaması yok** Merhaba belirtilen **kimlik doğrulaması** ayarlar.</span><span class="sxs-lookup"><span data-stu-id="21fa6-147">Ensure that **No Authentication** is specified for hello **Authentication** settings.</span></span> <span data-ttu-id="21fa6-148">Visual Studio sürümüne bağlı olarak, hello varsayılan toosomething başka ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="21fa6-148">Depending on your version of Visual Studio, hello default may be set toosomething else.</span></span> <span data-ttu-id="21fa6-149">toochange, tıklatın **kimlik doğrulamayı Değiştir** seçip **doğrulaması yok**.</span><span class="sxs-lookup"><span data-stu-id="21fa6-149">toochange it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="21fa6-150">Visual Studio 2015 ile birlikte izliyorsanız, hello temizleyin **hello buluttaki konağa** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="21fa6-150">If you are following along with Visual Studio 2015, clear hello **Host in hello cloud** checkbox.</span></span> <span data-ttu-id="21fa6-151">Artıracaksınız [sağlama Azure kaynaklarını hello](#provision-the-azure-resources) ve [yayımlama hello uygulama tooAzure](#publish-the-application-to-azure) hello öğreticide sonraki adımlarda.</span><span class="sxs-lookup"><span data-stu-id="21fa6-151">You'll [provision hello Azure resources](#provision-the-azure-resources) and [publish hello application tooAzure](#publish-the-application-to-azure) in subsequent steps in hello tutorial.</span></span> <span data-ttu-id="21fa6-152">Bırakarak Visual Studio'dan bir App Service web uygulaması hazırlama örneği için **hello buluttaki konağa** işaretli bkz [ASP.NET ve Visual Studio kullanarak Azure App Service'te Web uygulamalarını kullanmaya başlama](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="21fa6-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in hello cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![Proje şablonu seçme][cache-select-template]
4. <span data-ttu-id="21fa6-154">Tıklatın **Tamam** toocreate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-154">Click **OK** toocreate hello project.</span></span>

## <a name="create-hello-aspnet-mvc-application"></a><span data-ttu-id="21fa6-155">Merhaba ASP.NET MVC uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="21fa6-155">Create hello ASP.NET MVC application</span></span>
<span data-ttu-id="21fa6-156">Merhaba öğreticinin bu bölümünde okur ve veritabanından ekip istatistiklerini görüntüleyen hello temel uygulamayı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="21fa6-156">In this section of hello tutorial, you'll create hello basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="21fa6-157">Merhaba Entity Framework NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="21fa6-157">Add hello Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="21fa6-158">Merhaba modeli ekleme</span><span class="sxs-lookup"><span data-stu-id="21fa6-158">Add hello model</span></span>](#add-the-model)
* [<span data-ttu-id="21fa6-159">Merhaba denetleyici ekleyin</span><span class="sxs-lookup"><span data-stu-id="21fa6-159">Add hello controller</span></span>](#add-the-controller)
* [<span data-ttu-id="21fa6-160">Merhaba görünümlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="21fa6-160">Configure hello views</span></span>](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a><span data-ttu-id="21fa6-161">Merhaba Entity Framework NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="21fa6-161">Add hello Entity Framework NuGet package</span></span>

1. <span data-ttu-id="21fa6-162">Tıklatın **NuGet Paket Yöneticisi**, **Paket Yöneticisi Konsolu** hello gelen **Araçları** menüsü.</span><span class="sxs-lookup"><span data-stu-id="21fa6-162">Click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="21fa6-163">Çalışma hello hello komuttan aşağıdaki **Paket Yöneticisi Konsolu** penceresi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-163">Run hello following command from hello **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="21fa6-164">Bu paketi hakkında daha fazla bilgi için bkz: Merhaba [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet sayfası.</span><span class="sxs-lookup"><span data-stu-id="21fa6-164">For more information about this package, see hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-hello-model"></a><span data-ttu-id="21fa6-165">Merhaba modeli ekleme</span><span class="sxs-lookup"><span data-stu-id="21fa6-165">Add hello model</span></span>
1. <span data-ttu-id="21fa6-166">**Çözüm Gezgini**’nde **Modeller**’e sağ tıklayın ve **Ekle**, **Sınıf**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Model ekleme][cache-model-add-class]
2. <span data-ttu-id="21fa6-168">Girin `Team` hello sınıfı adı ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="21fa6-168">Enter `Team` for hello class name and click **Add**.</span></span>
   
    ![Model sınıfı ekleme][cache-model-add-class-dialog]
3. <span data-ttu-id="21fa6-170">Hello yerine `using` deyimleri hello hello üstündeki `Team.cs` hello aşağıdaki dosyasıyla `using` deyimleri.</span><span class="sxs-lookup"><span data-stu-id="21fa6-170">Replace hello `using` statements at hello top of hello `Team.cs` file with hello following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="21fa6-171">Merhaba Hello tanımını değiştirin `Team` güncelleştirilmiş içeren kod parçacığını aşağıdaki hello sınıfıyla `Team` bazı diğer Entity Framework yardımcı sınıflarının yanı sıra tanımı sınıf.</span><span class="sxs-lookup"><span data-stu-id="21fa6-171">Replace hello definition of hello `Team` class with hello following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="21fa6-172">Merhaba kod ilk yaklaşım tooEntity Bu öğreticide kullanılan Framework hakkında daha fazla bilgi için bkz: [kod ilk tooa yeni veritabanı](https://msdn.microsoft.com/data/jj193542).</span><span class="sxs-lookup"><span data-stu-id="21fa6-172">For more information on hello code first approach tooEntity Framework that's used in this tutorial, see [Code first tooa new database](https://msdn.microsoft.com/data/jj193542).</span></span>

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


1. <span data-ttu-id="21fa6-173">İçinde **Çözüm Gezgini**, çift **web.config** tooopen onu.</span><span class="sxs-lookup"><span data-stu-id="21fa6-173">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="21fa6-175">Merhaba aşağıdakileri ekleyin `connectionStrings` bölümü.</span><span class="sxs-lookup"><span data-stu-id="21fa6-175">Add hello following `connectionStrings` section.</span></span> <span data-ttu-id="21fa6-176">Merhaba hello bağlantı dizesinin adını hello olan Entity Framework veritabanı bağlamı sınıfının hello adı eşleşmelidir `TeamContext`.</span><span class="sxs-lookup"><span data-stu-id="21fa6-176">hello name of hello connection string must match hello name of hello Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="21fa6-177">Merhaba yeni ekleyebilirsiniz `connectionStrings` kendisini izleyen bölümüne `configSections`hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-177">You can add hello new `connectionStrings` section so that it follows `configSections`, as shown in hello following example.</span></span>

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
    > <span data-ttu-id="21fa6-178">Bağlantı dizenizi Visual Studio hello sürümüne bağlı olarak farklı olabilir ve SQL Server Express edition toocomplete hello öğretici kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21fa6-178">Your connection string may be different depending on hello version of Visual Studio and SQL Server Express edition used toocomplete hello tutorial.</span></span> <span data-ttu-id="21fa6-179">Merhaba web.config şablonu yapılandırılmış toomatch yüklemenizi olmalıdır ve içerebilir `Data Source` girişleri ister `(LocalDB)\v11.0` (gelen SQL Server Express 2012) veya `Data Source=(LocalDB)\MSSQLLocalDB` (SQL Server 2014'ün hızlı ve daha yeni).</span><span class="sxs-lookup"><span data-stu-id="21fa6-179">hello web.config template should be configured toomatch your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="21fa6-180">Bağlantı dizeleri ve SQL Express sürümleri hakkında daha fazla bilgi için bkz. [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span><span class="sxs-lookup"><span data-stu-id="21fa6-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-hello-controller"></a><span data-ttu-id="21fa6-181">Merhaba denetleyici ekleyin</span><span class="sxs-lookup"><span data-stu-id="21fa6-181">Add hello controller</span></span>
1. <span data-ttu-id="21fa6-182">Tuşuna **F6** toobuild hello projesi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-182">Press **F6** toobuild hello project.</span></span> 
2. <span data-ttu-id="21fa6-183">İçinde **Çözüm Gezgini**, sağ hello **denetleyicileri** klasör ve **Ekle**, **denetleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="21fa6-183">In **Solution Explorer**, right-click hello **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Denetleyici ekleme][cache-add-controller]
3. <span data-ttu-id="21fa6-185">**Görünümlere sahip MVC 5 Denetleyici, Entity Framework kullanarak** öğesini seçin ve **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="21fa6-186">' I tıklattıktan sonra bir hata alırsanız **Ekle**, size hello önce projeyi oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="21fa6-186">If you get an error after clicking **Add**, ensure that you have built hello project first.</span></span>
   
    ![Denetleyici sınıfı ekleme][cache-add-controller-class]
4. <span data-ttu-id="21fa6-188">Seçin **ekip (ContosoTeamStats.Models)** hello gelen **Model sınıfı** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="21fa6-188">Select **Team (ContosoTeamStats.Models)** from hello **Model class** drop-down list.</span></span> <span data-ttu-id="21fa6-189">Seçin **TeamContext (ContosoTeamStats.Models)** hello gelen **veri bağlamı sınıfı** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="21fa6-189">Select **TeamContext (ContosoTeamStats.Models)** from hello **Data context class** drop-down list.</span></span> <span data-ttu-id="21fa6-190">Tür `TeamsController` hello içinde **denetleyicisi** (bunu otomatik olarak doldurulmamışsa) adı metin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-190">Type `TeamsController` in hello **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="21fa6-191">Tıklatın **Ekle** toocreate hello denetleyici sınıfı ve hello varsayılan görünümler ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="21fa6-191">Click **Add** toocreate hello controller class and add hello default views.</span></span>
   
    ![Denetleyici yapılandırma][cache-configure-controller]
5. <span data-ttu-id="21fa6-193">İçinde **Çözüm Gezgini**, genişletin **Global.asax** çift tıklayın ve **Global.asax.cs** tooopen onu.</span><span class="sxs-lookup"><span data-stu-id="21fa6-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** tooopen it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="21fa6-195">İki aşağıdaki hello eklemek `using` deyimleri hello dosyanın üst kısmındaki hello hello diğer altında `using` deyimleri.</span><span class="sxs-lookup"><span data-stu-id="21fa6-195">Add hello following two `using` statements at hello top of hello file under hello other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="21fa6-196">Aşağıdaki kod hello hello sonunda hello eklemek `Application_Start` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-196">Add hello following line of code at hello end of hello `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="21fa6-197">**Çözüm Gezgini**’nde, `App_Start` öğesini genişletin ve `RouteConfig.cs` öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="21fa6-199">Değiştir `controller = "Home"` hello kodda aşağıdaki hello içinde `RegisterRoutes` yöntemiyle `controller = "Teams"` hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-199">Replace `controller = "Home"` in hello following code in hello `RegisterRoutes` method with `controller = "Teams"` as shown in hello following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a><span data-ttu-id="21fa6-200">Merhaba görünümlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="21fa6-200">Configure hello views</span></span>
1. <span data-ttu-id="21fa6-201">İçinde **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü ve ardından hello **paylaşılan** klasörü ve çift **_Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="21fa6-201">In **Solution Explorer**, expand hello **Views** folder and then hello **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="21fa6-203">Değiştirme hello Merhaba içeriğine `title` öğesi ve Değiştir `My ASP.NET Application` ile `Contoso Team Stats` hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-203">Change hello contents of hello `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in hello following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="21fa6-204">Merhaba, `body` bölümünde, ilk hello güncelleştirme `Html.ActionLink` deyimi ve Değiştir `Application name` ile `Contoso Team Stats` ve değiştirme `Home` ile `Teams`.</span><span class="sxs-lookup"><span data-stu-id="21fa6-204">In hello `body` section, update hello first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="21fa6-205">Önce: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="21fa6-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="21fa6-206">Sonra: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="21fa6-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Kod değişiklikleri][cache-layout-cshtml-code]
2. <span data-ttu-id="21fa6-208">Tuşuna **Ctrl + F5** toobuild ve Çalıştır Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="21fa6-208">Press **Ctrl+F5** toobuild and run hello application.</span></span> <span data-ttu-id="21fa6-209">Merhaba uygulamasının bu sürümü hello sonuçları doğrudan hello veritabanından okur.</span><span class="sxs-lookup"><span data-stu-id="21fa6-209">This version of hello application reads hello results directly from hello database.</span></span> <span data-ttu-id="21fa6-210">Not hello **Yeni Oluştur**, **Düzenle**, **ayrıntıları**, ve **silmek** otomatik olarak olan eylemler tarafından hello toohello uygulama eklendi **Entity Framework kullanarak MVC 5 denetleyici, görünümleri olan** ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-210">Note hello **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added toohello application by hello **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="21fa6-211">Merhaba sonraki bölümde hello öğreticinin Redis önbelleği toooptimize hello veri erişimi ve toohello uygulamaya ek özellikler sağlamak ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="21fa6-211">In hello next section of hello tutorial you'll add Redis Cache toooptimize hello data access and provide additional features toohello application.</span></span>

![Başlangıç uygulaması][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a><span data-ttu-id="21fa6-213">Merhaba uygulama toouse Redis önbelleği yapılandırma</span><span class="sxs-lookup"><span data-stu-id="21fa6-213">Configure hello application toouse Redis Cache</span></span>
<span data-ttu-id="21fa6-214">Merhaba öğreticinin bu bölümünde, hello örnek uygulama toostore yapılandırmak ve Başlangıç'ı kullanarak Azure Redis önbelleği örneği Contoso ekip istatistiklerini almak [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) önbellek istemcisi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-214">In this section of hello tutorial, you'll configure hello sample application toostore and retrieve Contoso team statistics from an Azure Redis Cache instance by using hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="21fa6-215">Merhaba uygulama toouse StackExchange.Redis yapılandırma</span><span class="sxs-lookup"><span data-stu-id="21fa6-215">Configure hello application toouse StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="21fa6-216">Hello TeamsController sınıfını tooreturn sonuçları hello önbellek veya hello veritabanından güncelleştir</span><span class="sxs-lookup"><span data-stu-id="21fa6-216">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="21fa6-217">Merhaba oluşturma, düzenleme, güncelleştirme ve yöntemleri toowork hello önbelleği ile silme</span><span class="sxs-lookup"><span data-stu-id="21fa6-217">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="21fa6-218">Merhaba ekipler dizini görünümünü toowork hello önbelleği ile güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="21fa6-218">Update hello Teams Index view toowork with hello cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a><span data-ttu-id="21fa6-219">Merhaba uygulama toouse StackExchange.Redis yapılandırma</span><span class="sxs-lookup"><span data-stu-id="21fa6-219">Configure hello application toouse StackExchange.Redis</span></span>
1. <span data-ttu-id="21fa6-220">tooconfigure Visual Studio'da hello StackExchange.Redis NuGet paketi kullanarak bir istemci uygulaması tıklatın **NuGet Paket Yöneticisi**, **Paket Yöneticisi Konsolu** hello gelen **Araçları** menüsü.</span><span class="sxs-lookup"><span data-stu-id="21fa6-220">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="21fa6-221">Çalışma hello hello komuttan aşağıdaki `Package Manager Console` penceresi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-221">Run hello following command from hello `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="21fa6-222">Merhaba paketi indirir ve hello ekler NuGet derleme başvurularını hello StackExchange.Redis önbellek istemcisi ile istemci uygulaması tooaccess Azure Redis önbelleği için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="21fa6-222">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span> <span data-ttu-id="21fa6-223">Toouse hello tanımlayıcı adlı bir sürümünü tercih ederseniz `StackExchange.Redis` istemci kitaplığı, yükleme hello `StackExchange.Redis.StrongName` paket.</span><span class="sxs-lookup"><span data-stu-id="21fa6-223">If you prefer toouse a strong-named version of hello `StackExchange.Redis` client library, install hello `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="21fa6-224">İçinde **Çözüm Gezgini**, hello genişletin **denetleyicileri** klasörü ve çift **TeamsController.cs** tooopen onu.</span><span class="sxs-lookup"><span data-stu-id="21fa6-224">In **Solution Explorer**, expand hello **Controllers** folder and double-click **TeamsController.cs** tooopen it.</span></span>
   
    ![Ekip denetleyicisi][cache-teamscontroller]
4. <span data-ttu-id="21fa6-226">İki aşağıdaki hello eklemek `using` deyimleri çok**TeamsController.cs**.</span><span class="sxs-lookup"><span data-stu-id="21fa6-226">Add hello following two `using` statements too**TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="21fa6-227">İki özellikleri toohello aşağıdaki hello eklemek `TeamsController` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="21fa6-227">Add hello following two properties toohello `TeamsController` class.</span></span>

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

6. <span data-ttu-id="21fa6-228">Bilgisayarınızda adlı bir dosya oluşturun `WebAppPlusCacheAppSecrets.config` ve karar toocheck örnek uygulamanızın hello kaynak kodu ile denetlenmeyecek bir konuma yerleştirin, başka bir yere içinde.</span><span class="sxs-lookup"><span data-stu-id="21fa6-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with hello source code of your sample application, should you decide toocheck it in somewhere.</span></span> <span data-ttu-id="21fa6-229">Bu örnek hello içinde `AppSettingsSecrets.config` dosya adresindedir `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="21fa6-229">In this example hello `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="21fa6-230">Merhaba Düzenle `WebAppPlusCacheAppSecrets.config` dosya ve içeriği aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-230">Edit hello `WebAppPlusCacheAppSecrets.config` file and add hello following contents.</span></span> <span data-ttu-id="21fa6-231">Merhaba uygulama yerel olarak çalıştırırsanız bu bilgiler kullanılan tooconnect tooyour Azure Redis önbelleği örneği olur.</span><span class="sxs-lookup"><span data-stu-id="21fa6-231">If you run hello application locally this information is used tooconnect tooyour Azure Redis Cache instance.</span></span> <span data-ttu-id="21fa6-232">Daha sonra hello öğreticide bir Azure Redis önbelleği örneği hazırlayacak ve hello önbellek adı ve parolasını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-232">Later in hello tutorial you'll provision an Azure Redis Cache instance and update hello cache name and password.</span></span> <span data-ttu-id="21fa6-233">Toorun Merhaba örnek uygulaması planlamıyorsanız hello oluşturma bu dosyanın yerel olarak atlayabilirsiniz ve tooAzure hello uygulama dağıttığınızda bulunduğundan hello dosya başvuru hello sonraki adımları hello uygulamadan hello önbellek bağlantı bilgilerini alır Merhaba Web uygulaması için ve bu dosyadan ayarlama.</span><span class="sxs-lookup"><span data-stu-id="21fa6-233">If you don't plan toorun hello sample application locally you can skip hello creation of this file and hello subsequent steps that reference hello file, because when you deploy tooAzure hello application retrieves hello cache connection information from hello app setting for hello Web App and not from this file.</span></span> <span data-ttu-id="21fa6-234">Merhaba itibaren `WebAppPlusCacheAppSecrets.config` dağıtılmadığı tooAzure uygulamanız ile yapmanıza gerek yoktur, toorun hello uygulamayı yerel olarak çalıştırmayacağınız sürece.</span><span class="sxs-lookup"><span data-stu-id="21fa6-234">Since hello `WebAppPlusCacheAppSecrets.config` is not deployed tooAzure with your application, you don't need it unless you are going toorun hello application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="21fa6-235">İçinde **Çözüm Gezgini**, çift **web.config** tooopen onu.</span><span class="sxs-lookup"><span data-stu-id="21fa6-235">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="21fa6-237">Merhaba aşağıdakileri ekleyin `file` toohello özniteliği `appSettings` öğesi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-237">Add hello following `file` attribute toohello `appSettings` element.</span></span> <span data-ttu-id="21fa6-238">Farklı bir dosya adı veya konumu kullandıysanız, bu değerleri hello hello örnekte gösterilen olanları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-238">If you used a different file name or location, substitute those values for hello ones shown in hello example.</span></span>
   
   * <span data-ttu-id="21fa6-239">Önce: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="21fa6-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="21fa6-240">Sonra: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="21fa6-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="21fa6-241">Merhaba ASP.NET çalışma zamanı hello hello hello biçimlendirme ile Merhaba harici dosyasının içeriğini birleştirir `<appSettings>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-241">hello ASP.NET runtime merges hello contents of hello external file with hello markup in hello `<appSettings>` element.</span></span> <span data-ttu-id="21fa6-242">Merhaba belirtilen dosya bulunamazsa hello çalışma zamanı hello dosya özniteliğini yok sayar.</span><span class="sxs-lookup"><span data-stu-id="21fa6-242">hello runtime ignores hello file attribute if hello specified file cannot be found.</span></span> <span data-ttu-id="21fa6-243">Gizli anahtarlarınız (Merhaba bağlantı dizesi tooyour önbellek) hello Merhaba uygulaması için kaynak kodu parçası olarak dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="21fa6-243">Your secrets (hello connection string tooyour cache) are not included as part of hello source code for hello application.</span></span> <span data-ttu-id="21fa6-244">Web uygulaması tooAzure dağıttığınızda, hello `WebAppPlusCacheAppSecrests.config` (yani istediğinizi) dosyası dağıtılmaz.</span><span class="sxs-lookup"><span data-stu-id="21fa6-244">When you deploy your web app tooAzure, hello `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="21fa6-245">Azure'da bu Sırları birkaç yolu toospecify vardır ve Bu öğreticide bunlar otomatik olarak sizin için yapılandırılmış zaman, [sağlama Azure kaynaklarını hello](#provision-the-azure-resources) bir sonraki öğretici adımında.</span><span class="sxs-lookup"><span data-stu-id="21fa6-245">There are several ways toospecify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision hello Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="21fa6-246">Azure'daki gizli anahtarlarla çalışma hakkında daha fazla bilgi için bkz: [en iyi uygulamalar parolalar ve diğer hassas verileri tooASP.NET ve Azure uygulama hizmeti dağıtmak için](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span><span class="sxs-lookup"><span data-stu-id="21fa6-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data tooASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a><span data-ttu-id="21fa6-247">Hello TeamsController sınıfını tooreturn sonuçları hello önbellek veya hello veritabanından güncelleştir</span><span class="sxs-lookup"><span data-stu-id="21fa6-247">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>
<span data-ttu-id="21fa6-248">Bu örnekte, ekip istatistikleri hello veritabanından veya hello önbellekten alınabilir.</span><span class="sxs-lookup"><span data-stu-id="21fa6-248">In this sample, team statistics can be retrieved from hello database or from hello cache.</span></span> <span data-ttu-id="21fa6-249">Ekip istatistiklerini seri hale getirilmiş bir hello önbelleğinde depolandığı `List<Team>`hem de Redis veri türleri kullanılarak sıralanmış bir küme olarak.</span><span class="sxs-lookup"><span data-stu-id="21fa6-249">Team statistics are stored in hello cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="21fa6-250">Bir sıralanmış kümeden öğeleri alırken, belirli öğeler için bazı, tümü veya sorgu alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21fa6-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="21fa6-251">Bu örnekte kazanma sayısına göre derece hello iyi 5 ekip için sıralanmış hello kümesi sorgulayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="21fa6-251">In this sample you'll query hello sorted set for hello top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="21fa6-252">Gerekli toostore hello ekip istatistiklerini sipariş toouse Azure Redis önbelleği hello önbellekte çoklu biçimlerde olmadığı.</span><span class="sxs-lookup"><span data-stu-id="21fa6-252">It is not required toostore hello team statistics in multiple formats in hello cache in order toouse Azure Redis Cache.</span></span> <span data-ttu-id="21fa6-253">Bu öğretici birden çok biçimleri toodemonstrate bazı kullanır hello farklı yolları ve farklı veri türleri toocache verileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21fa6-253">This tutorial uses multiple formats toodemonstrate some of hello different ways and different data types you can use toocache data.</span></span>
> 
> 

1. <span data-ttu-id="21fa6-254">Merhaba aşağıdakileri ekleyin `using` deyimleri toohello `TeamsController.cs` hello diğer ile Merhaba üstünde dosya `using` deyimleri.</span><span class="sxs-lookup"><span data-stu-id="21fa6-254">Add hello following `using` statements toohello `TeamsController.cs` file at hello top with hello other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="21fa6-255">Merhaba geçerli Değiştir `public ActionResult Index()` uygulama aşağıdaki hello uygulamasıyla yöntemi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-255">Replace hello current `public ActionResult Index()` method implementation with hello following implementation.</span></span>

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

            case "clearCache": // Clear hello results from hello cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild hello database with sample data.
                RebuildDB();
                break;
        }

        // Measure hello time it takes tooretrieve hello results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve hello top 5 teams from hello sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from hello cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from hello database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add hello elapsed time of hello operation toohello ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="21fa6-256">Aşağıdaki üç yöntem toohello hello eklemek `TeamsController` sınıfı tooimplement hello `playGames`, `clearCache`, ve `rebuildDB` eylemin hello türlerinden geçiş hello önceki kod parçacığında eklenen deyimi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-256">Add hello following three methods toohello `TeamsController` class tooimplement hello `playGames`, `clearCache`, and `rebuildDB` action types from hello switch statement added in hello previous code snippet.</span></span>
   
    <span data-ttu-id="21fa6-257">Merhaba `PlayGames` yöntemi, oyun sezonunu taklit ederek hello ekip istatistiklerini güncelleştirir, kaydeder hello sonuçları toohello veritabanı ve temizler hello artık güncel olmayan hello önbelleğinden veri.</span><span class="sxs-lookup"><span data-stu-id="21fa6-257">hello `PlayGames` method updates hello team statistics by simulating a season of games, saves hello results toohello database, and clears hello now outdated data from hello cache.</span></span>

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

    <span data-ttu-id="21fa6-258">Merhaba `RebuildDB` yöntemi yeniden başlatmak hello hello varsayılan ekip, kümesine veritabanıyla bunlar için İstatistikler oluşturur ve temizler hello artık güncel olmayan hello önbelleğinden veri.</span><span class="sxs-lookup"><span data-stu-id="21fa6-258">hello `RebuildDB` method reinitializes hello database with hello default set of teams, generates statistics for them, and clears hello now outdated data from hello cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize hello database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="21fa6-259">Merhaba `ClearCachedTeams` yöntemi önbellekteki ekip istatistiklerini hello önbellekten kaldırır.</span><span class="sxs-lookup"><span data-stu-id="21fa6-259">hello `ClearCachedTeams` method removes any cached team statistics from hello cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="21fa6-260">Aşağıdaki dört yöntemleri toohello hello eklemek `TeamsController` sınıfı tooimplement hello hello önbellek ve hello veritabanı hello ekip istatistiklerini almanın çeşitli yollarını.</span><span class="sxs-lookup"><span data-stu-id="21fa6-260">Add hello following four methods toohello `TeamsController` class tooimplement hello various ways of retrieving hello team statistics from hello cache and hello database.</span></span> <span data-ttu-id="21fa6-261">Bu yöntemlerin her biri döndüren bir `List<Team>` sonra görüntülendiği göre hello görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-261">Each of these methods returns a `List<Team>` which is then displayed by hello view.</span></span>
   
    <span data-ttu-id="21fa6-262">Merhaba `GetFromDB` yöntemi hello veritabanından hello ekip istatistiklerini okur.</span><span class="sxs-lookup"><span data-stu-id="21fa6-262">hello `GetFromDB` method reads hello team statistics from hello database.</span></span>
   
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

    <span data-ttu-id="21fa6-263">Merhaba `GetFromList` yöntemi seri hale getirilmiş bir hello ekip istatistiklerini okur `List<Team>`.</span><span class="sxs-lookup"><span data-stu-id="21fa6-263">hello `GetFromList` method reads hello team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="21fa6-264">Önbellek isabetsizliği varsa, hello ekip istatistiklerini hello veritabanından okunur ve ardından gelecek sefer için hello önbellekte depolanır.</span><span class="sxs-lookup"><span data-stu-id="21fa6-264">If there is a cache miss, hello team statistics are read from hello database and then stored in hello cache for next time.</span></span> <span data-ttu-id="21fa6-265">Bu örnekte biz JSON.NET serileştirme tooserialize hello .NET nesneleri tooand hello önbellekten kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="21fa6-265">In this sample we're using JSON.NET serialization tooserialize hello .NET objects tooand from hello cache.</span></span> <span data-ttu-id="21fa6-266">Daha fazla bilgi için bkz: [nasıl toowork .NET ile Azure Redis Önbelleği'nde nesneleri](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span><span class="sxs-lookup"><span data-stu-id="21fa6-266">For more information, see [How toowork with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

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

            ViewBag.msg += "Storing results toocache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="21fa6-267">Merhaba `GetFromSortedSet` yöntemi önbelleğe alınan bir sıralanmış kümeden hello ekip istatistiklerini okur.</span><span class="sxs-lookup"><span data-stu-id="21fa6-267">hello `GetFromSortedSet` method reads hello team statistics from a cached sorted set.</span></span> <span data-ttu-id="21fa6-268">Önbellek isabetsizliği varsa, hello ekip istatistiklerini hello veritabanından okunur ve bir sıralanmış küme olarak hello önbelleğinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="21fa6-268">If there is a cache miss, hello team statistics are read from hello database and stored in hello cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
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

            ViewBag.msg += "Storing results toocache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding toosorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="21fa6-269">Merhaba `GetFromSortedSetTop5` yöntemi hello üst 5 takımlara hello önbelleğe alınan sıralanmış kümesi okur.</span><span class="sxs-lookup"><span data-stu-id="21fa6-269">hello `GetFromSortedSetTop5` method reads hello top 5 teams from hello cached sorted set.</span></span> <span data-ttu-id="21fa6-270">Merhaba hello varlığı hello önbelleği denetleyerek başlar `teamsSortedSet` anahtarı.</span><span class="sxs-lookup"><span data-stu-id="21fa6-270">It starts by checking hello cache for hello existence of hello `teamsSortedSet` key.</span></span> <span data-ttu-id="21fa6-271">Bu anahtar mevcut değilse hello `GetFromSortedSet` yöntemi tooread hello ekip istatistiklerini olarak adlandırılır ve hello önbelleğine depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21fa6-271">If this key is not present, hello `GetFromSortedSet` method is called tooread hello team statistics and store them in hello cache.</span></span> <span data-ttu-id="21fa6-272">Ardından, hello önbelleğe alınan sıralanmış küme, döndürülen hello iyi 5 ekip için sorgulanır.</span><span class="sxs-lookup"><span data-stu-id="21fa6-272">Next, hello cached sorted set is queried for hello top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load hello entire sorted set into hello cache.
            GetFromSortedSet();

            // Retrieve hello top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get hello top 5 teams from hello sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a><span data-ttu-id="21fa6-273">Merhaba oluşturma, düzenleme, güncelleştirme ve yöntemleri toowork hello önbelleği ile silme</span><span class="sxs-lookup"><span data-stu-id="21fa6-273">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>
<span data-ttu-id="21fa6-274">Bu örnek bölümü yöntemleri tooadd içerdiği gibi oluşturan hello iskele kurma kodu düzenleyebilir ve takımlar silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21fa6-274">hello scaffolding code that was generated as part of this sample includes methods tooadd, edit, and delete teams.</span></span> <span data-ttu-id="21fa6-275">Bir takım eklediyseniz, düzenlenebilir veya kaldırılan herhangi bir zamanda, hello önbelleğinde hello veriler güncel olmayan hale gelir.</span><span class="sxs-lookup"><span data-stu-id="21fa6-275">Anytime a team is added, edited, or removed, hello data in hello cache becomes outdated.</span></span> <span data-ttu-id="21fa6-276">Değiştireceğiniz Bu bölümde, bu üç yöntem tooclear hello takımlar önbelleğe Hello önbellek hello veritabanı ile eşitlenmemiş olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="21fa6-276">In this section you'll modify these three methods tooclear hello cached teams so that hello cache won't be out of sync with hello database.</span></span>

1. <span data-ttu-id="21fa6-277">Toohello Gözat `Create(Team team)` hello yönteminde `TeamsController` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="21fa6-277">Browse toohello `Create(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="21fa6-278">Çağrı toohello ekleme `ClearCachedTeams` hello aşağıdaki örnekte gösterildiği gibi yöntemi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-278">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Create
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="21fa6-279">Toohello Gözat `Edit(Team team)` hello yönteminde `TeamsController` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="21fa6-279">Browse toohello `Edit(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="21fa6-280">Çağrı toohello ekleme `ClearCachedTeams` hello aşağıdaki örnekte gösterildiği gibi yöntemi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-280">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="21fa6-281">Toohello Gözat `DeleteConfirmed(int id)` hello yönteminde `TeamsController` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="21fa6-281">Browse toohello `DeleteConfirmed(int id)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="21fa6-282">Çağrı toohello ekleme `ClearCachedTeams` hello aşağıdaki örnekte gösterildiği gibi yöntemi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-282">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, hello cache is out of date.
        // Clear hello cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a><span data-ttu-id="21fa6-283">Merhaba ekipler dizini görünümünü toowork hello önbelleği ile güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="21fa6-283">Update hello Teams Index view toowork with hello cache</span></span>
1. <span data-ttu-id="21fa6-284">İçinde **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü seçip hello **takımlar** klasörü ve çift **Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="21fa6-284">In **Solution Explorer**, expand hello **Views** folder, then hello **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="21fa6-286">Merhaba dosyasının üst kısmında hello, paragraf öğesini aşağıdaki Merhaba arayın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-286">Near hello top of hello file, look for hello following paragraph element.</span></span>
   
    ![Eylem tablosu][cache-teams-index-table]
   
    <span data-ttu-id="21fa6-288">Merhaba bağlantı toocreate yeni bir ekip budur.</span><span class="sxs-lookup"><span data-stu-id="21fa6-288">This is hello link toocreate a new team.</span></span> <span data-ttu-id="21fa6-289">Merhaba paragraf öğesini aşağıdaki tablonun hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-289">Replace hello paragraph element with hello following table.</span></span> <span data-ttu-id="21fa6-290">Bu tablo bir yeni bir oyun sezonu hello önbelleği temizleme, çalma yeni bir ekip oluşturmak için eylem bağlantıları vardır, hello takımlar hello önbelleğinden çeşitli biçimlerde alma, hello veritabanından hello ekipleri alma ve yeniden oluşturma yeni örnek veriler ile veritabanını hello.</span><span class="sxs-lookup"><span data-stu-id="21fa6-290">This table has action links for creating a new team, playing a new season of games, clearing hello cache, retrieving hello teams from hello cache in several formats, retrieving hello teams from hello database, and rebuilding hello database with fresh sample data.</span></span>

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


1. <span data-ttu-id="21fa6-291">Merhaba kaydırma toohello alt **Index.cshtml** dosya ve hello aşağıdakileri ekleyin `tr` öğesi hello son satırında hello olmasını sağlamak en son tablo hello dosyasında.</span><span class="sxs-lookup"><span data-stu-id="21fa6-291">Scroll toohello bottom of hello **Index.cshtml** file and add hello following `tr` element so that it is hello last row in hello last table in hello file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="21fa6-292">Bu satır hello değerini görüntüler `ViewBag.Msg` hello geçerli işlem hakkında bir durum raporu içerir.</span><span class="sxs-lookup"><span data-stu-id="21fa6-292">This row displays hello value of `ViewBag.Msg` which contains a status report about hello current operation.</span></span> <span data-ttu-id="21fa6-293">Merhaba `ViewBag.Msg` hello hello önceki adımdaki eylem bağlantılardan herhangi birine tıkladığınızda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-293">hello `ViewBag.Msg` is set when you click any of hello action links from hello previous step.</span></span>   
   
    ![Durum iletisi][cache-status-message]
2. <span data-ttu-id="21fa6-295">Tuşuna **F6** toobuild hello projesi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-295">Press **F6** toobuild hello project.</span></span>

## <a name="provision-hello-azure-resources"></a><span data-ttu-id="21fa6-296">Sağlama Azure kaynaklarını hello</span><span class="sxs-lookup"><span data-stu-id="21fa6-296">Provision hello Azure resources</span></span>
<span data-ttu-id="21fa6-297">toohost ilk hazırlamalısınız uygulamanızı azure'da uygulamanızın gerektirdiği Azure hizmetlerini hello.</span><span class="sxs-lookup"><span data-stu-id="21fa6-297">toohost your application in Azure, you must first provision hello Azure services that your application requires.</span></span> <span data-ttu-id="21fa6-298">Merhaba örnek uygulaması Bu öğreticide Azure Hizmetleri aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="21fa6-298">hello sample application in this tutorial uses hello following Azure services.</span></span>

* <span data-ttu-id="21fa6-299">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="21fa6-299">Azure Redis Cache</span></span>
* <span data-ttu-id="21fa6-300">App Service Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="21fa6-300">App Service Web App</span></span>
* <span data-ttu-id="21fa6-301">SQL Database</span><span class="sxs-lookup"><span data-stu-id="21fa6-301">SQL Database</span></span>

<span data-ttu-id="21fa6-302">toodeploy tercih ettiğiniz bu hizmetleri tooa yeni veya var olan kaynak grubunu tıklatın aşağıdaki hello **tooAzure dağıtmak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-302">toodeploy these services tooa new or existing resource group of your choice, click hello following **Deploy tooAzure** button.</span></span>

<span data-ttu-id="21fa6-303">[! [TooAzure dağıtım] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="21fa6-303">[![Deploy tooAzure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="21fa6-304">Bu **tooAzure dağıtmak** düğmesi kullanır hello [bir Web uygulaması artı Redis önbelleği artı SQL veritabanı oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Hızlı Başlangıç](https://github.com/Azure/azure-quickstart-templates) şablon tooprovision bu hizmetleri ve kümesi hello hello Azure Redis önbelleği bağlantı dizesi hello SQL Database ve hello uygulama ayarı için bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-304">This **Deploy tooAzure** button uses hello [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template tooprovision these services and set hello connection string for hello SQL Database and hello application setting for hello Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="21fa6-305">Bir Azure hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir Azure hesabı oluşturabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="21fa6-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="21fa6-306">Tıklatmak hello **tooAzure dağıtmak** düğmesini toohello Azure portal alır ve hello hello şablon tarafından açıklanan hello kaynakları oluşturma işlemini başlatır.</span><span class="sxs-lookup"><span data-stu-id="21fa6-306">Clicking hello **Deploy tooAzure** button takes you toohello Azure portal and initiates hello process of creating hello resources described by hello template.</span></span>

![TooAzure dağıtma][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="21fa6-308">Merhaba, **Temelleri** bölümünde hello Azure aboneliği toouse seçin ve varolan bir kaynak grubu seçin veya yeni bir tane oluşturun ve hello kaynak grubu konumu belirtin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-308">In hello **Basics** section, select hello Azure subscription toouse, and select an existing resource group or create a new one, and specify hello resource group location.</span></span>
2. <span data-ttu-id="21fa6-309">Merhaba, **ayarları** bölümünde, belirtin bir **yönetici oturum açma** (kullanmayan **yönetici**), **yönetici oturum açma parolası**ve  **Veritabanı adı**.</span><span class="sxs-lookup"><span data-stu-id="21fa6-309">In hello **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="21fa6-310">Merhaba diğer parametreler boş bir uygulama hizmeti planı ve ücretsiz katman ile birlikte gelen yok hello SQL veritabanı ve Azure Redis önbelleği için daha düşük maliyetli seçenekler sunmak için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="21fa6-310">hello other parameters are configured for a free App Service hosting plan, and lower-cost options for hello SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![TooAzure dağıtma][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="21fa6-312">İstenen hello ayarlarını yapılandırdıktan sonra Başlangıç sayfası, okuma hello hüküm ve koşullar toohello sonuna kaydırın ve hello denetleyin **toohello hüküm ve koşullar yukarıda belirtildiği kabul** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="21fa6-312">After configuring hello desired settings, scroll toohello end of hello page, read hello terms and conditions, and check hello **I agree toohello terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="21fa6-313">toobegin sağlama hello kaynaklar'ı **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="21fa6-313">toobegin provisioning hello resources, click **Purchase**.</span></span>

<span data-ttu-id="21fa6-314">Merhaba bildirim simgesine tıklayın ve'ı tıklatın, dağıtımınızı tooview hello ilerleme **dağıtım başladı**.</span><span class="sxs-lookup"><span data-stu-id="21fa6-314">tooview hello progress of your deployment, click hello notification icon and click **Deployment started**.</span></span>

![Dağıtım başladı][cache-deployment-started]

<span data-ttu-id="21fa6-316">Merhaba üzerinde hello dağıtımınızın durumunu görüntüleyebilirsiniz **Microsoft.Template** dikey.</span><span class="sxs-lookup"><span data-stu-id="21fa6-316">You can view hello status of your deployment on hello **Microsoft.Template** blade.</span></span>

![TooAzure dağıtma][cache-deploy-to-azure-step-3]

<span data-ttu-id="21fa6-318">Sağlama tamamlandıktan sonra uygulama tooAzure Visual Studio'dan yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21fa6-318">When provisioning is complete, you can publish your application tooAzure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="21fa6-319">Merhaba sağlama işlemi sırasında oluşabilecek hataları hello üzerinde görüntülenen **Microsoft.Template** dikey.</span><span class="sxs-lookup"><span data-stu-id="21fa6-319">Any errors that may occur during hello provisioning process are displayed on hello **Microsoft.Template** blade.</span></span> <span data-ttu-id="21fa6-320">Abonelik başına çok fazla SQL Server veya çok fazla Ücretsiz App Service barındırma planı yaygın hatalardır.</span><span class="sxs-lookup"><span data-stu-id="21fa6-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="21fa6-321">Hataları çözümleyin ve tıklayarak hello işlemi yeniden **dağıtmanız** hello üzerinde **Microsoft.Template** dikey veya hello **tooAzure dağıtmak** bu öğreticideki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-321">Resolve any errors and restart hello process by clicking **Redeploy** on hello **Microsoft.Template** blade or hello **Deploy tooAzure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-hello-application-tooazure"></a><span data-ttu-id="21fa6-322">Yayımlama Hello uygulama tooAzure</span><span class="sxs-lookup"><span data-stu-id="21fa6-322">Publish hello application tooAzure</span></span>
<span data-ttu-id="21fa6-323">Merhaba öğreticinin bu adımında, yayımlama hello uygulama tooAzure ve hello bulutta çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-323">In this step of hello tutorial, you'll publish hello application tooAzure and run it in hello cloud.</span></span>

1. <span data-ttu-id="21fa6-324">Sağ hello **ContosoTeamStats** seçin ve Visual Studio Proje **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="21fa6-324">Right-click hello **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Yayımlama][cache-publish-app]
2. <span data-ttu-id="21fa6-326">**Microsoft Azure App Service**’e tıklayın, **Var Olanı Seç**’i seçin ve **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Yayımlama][cache-publish-to-app-service]
3. <span data-ttu-id="21fa6-328">Hello Azure kaynakları oluşturma hello kaynakları içeren hello kaynak grubunu genişletin ve Web uygulaması seçme hello istenen kullanılan hello aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-328">Select hello subscription used when creating hello Azure resources, expand hello resource group containing hello resources, and select hello desired Web App.</span></span> <span data-ttu-id="21fa6-329">Merhaba kullandıysanız **tooAzure dağıtmak** , Web uygulaması adı ile başlayan düğmesi **Web sitesi** bazı ek karakterlerle devam eder.</span><span class="sxs-lookup"><span data-stu-id="21fa6-329">If you used hello **Deploy tooAzure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Web Uygulaması Seçme][cache-select-web-app]
4. <span data-ttu-id="21fa6-331">Tıklatın **Tamam** toobegin hello işlem yayımlama.</span><span class="sxs-lookup"><span data-stu-id="21fa6-331">Click **OK** toobegin hello publishing process.</span></span> <span data-ttu-id="21fa6-332">Birkaç dakika sonra işlem yayımlama hello tamamlanır ve örnek uygulama çalıştırılıyor hello ile bir tarayıcı başlatılır.</span><span class="sxs-lookup"><span data-stu-id="21fa6-332">After a few moments hello publishing process completes and a browser is launched with hello running sample application.</span></span> <span data-ttu-id="21fa6-333">Doğrularken veya yayımlarken bir DNS hatası alırsanız ve hello sağlama işlemi için hello Merhaba uygulaması için Azure kaynaklarını yalnızca yakın zamanda tamamlandı, kısa bir süre bekleyin ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-333">If you get a DNS error when validating or publishing, and hello provisioning process for hello Azure resources for hello application has just recently completed, wait a moment and try again.</span></span>
   
    ![Önbellek eklendi][cache-added-to-application]

<span data-ttu-id="21fa6-335">Merhaba aşağıdaki tabloda her eylem bağlantısını hello örnek uygulamadan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="21fa6-335">hello following table describes each action link from hello sample application.</span></span>

| <span data-ttu-id="21fa6-336">Eylem</span><span class="sxs-lookup"><span data-stu-id="21fa6-336">Action</span></span> | <span data-ttu-id="21fa6-337">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21fa6-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21fa6-338">Yeni Oluştur</span><span class="sxs-lookup"><span data-stu-id="21fa6-338">Create New</span></span> |<span data-ttu-id="21fa6-339">Yeni bir Ekip oluşturun.</span><span class="sxs-lookup"><span data-stu-id="21fa6-339">Create a new Team.</span></span> |
| <span data-ttu-id="21fa6-340">Sezonu Oynat</span><span class="sxs-lookup"><span data-stu-id="21fa6-340">Play Season</span></span> |<span data-ttu-id="21fa6-341">Bir oyun sezonu, güncelleştirme hello ekip istatistiklerini, yürütmek ve temizleyin herhangi bir ekip verileri hello önbelleğinden eski.</span><span class="sxs-lookup"><span data-stu-id="21fa6-341">Play a season of games, update hello team stats, and clear any outdated team data from hello cache.</span></span> |
| <span data-ttu-id="21fa6-342">Önbelleği Temizle</span><span class="sxs-lookup"><span data-stu-id="21fa6-342">Clear Cache</span></span> |<span data-ttu-id="21fa6-343">Hello önbellekten ekip istatistiklerini temizleyin hello.</span><span class="sxs-lookup"><span data-stu-id="21fa6-343">Clear hello team stats from hello cache.</span></span> |
| <span data-ttu-id="21fa6-344">Önbellekten Liste</span><span class="sxs-lookup"><span data-stu-id="21fa6-344">List from Cache</span></span> |<span data-ttu-id="21fa6-345">Merhaba önbellekten Hello ekip istatistiklerini alın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-345">Retrieve hello team stats from hello cache.</span></span> <span data-ttu-id="21fa6-346">Önbellek isabetsizliği varsa, hello veritabanından hello istatistikleri yükleyin ve bir sonraki seferde toohello önbellek kaydedin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-346">If there is a cache miss, load hello stats from hello database and save toohello cache for next time.</span></span> |
| <span data-ttu-id="21fa6-347">Önbellekten Sıralanmış Küme</span><span class="sxs-lookup"><span data-stu-id="21fa6-347">Sorted Set from Cache</span></span> |<span data-ttu-id="21fa6-348">Bir sıralanmış küme kullanarak hello önbellekten Hello ekip istatistiklerini alın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-348">Retrieve hello team stats from hello cache using a sorted set.</span></span> <span data-ttu-id="21fa6-349">Önbellek isabetsizliği varsa, hello veritabanından hello istatistikleri yükleyin ve bir sıralanmış küme kullanarak toohello önbelleği kaydedin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-349">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="21fa6-350">Önbellekteki En İyi 5 Ekip</span><span class="sxs-lookup"><span data-stu-id="21fa6-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="21fa6-351">Bir sıralanmış küme kullanarak hello önbellekten Hello en iyi 5 ekibi alın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-351">Retrieve hello top 5 teams from hello cache using a sorted set.</span></span> <span data-ttu-id="21fa6-352">Önbellek isabetsizliği varsa, hello veritabanından hello istatistikleri yükleyin ve bir sıralanmış küme kullanarak toohello önbelleği kaydedin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-352">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="21fa6-353">DB’den yükleme</span><span class="sxs-lookup"><span data-stu-id="21fa6-353">Load from DB</span></span> |<span data-ttu-id="21fa6-354">Merhaba veritabanından Hello ekip istatistiklerini alın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-354">Retrieve hello team stats from hello database.</span></span> |
| <span data-ttu-id="21fa6-355">DB Yeniden Oluşturma</span><span class="sxs-lookup"><span data-stu-id="21fa6-355">Rebuild DB</span></span> |<span data-ttu-id="21fa6-356">Merhaba veritabanını yeniden oluşturun ve örnek ekip verileri ile yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-356">Rebuild hello database and reload it with sample team data.</span></span> |
| <span data-ttu-id="21fa6-357">Düzenle / Ayrıntılar / Sil</span><span class="sxs-lookup"><span data-stu-id="21fa6-357">Edit / Details / Delete</span></span> |<span data-ttu-id="21fa6-358">Bir ekibi düzenleyin, ekibin ayrıntılarını görüntüleyin, ekibi silin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="21fa6-359">Merhaba eylemlerin bazıları tıklayın ve hello farklı kaynaklardan hello veri alma denemeleri yapın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-359">Click some of hello actions and experiment with retrieving hello data from hello different sources.</span></span> <span data-ttu-id="21fa6-360">Hello farklar toocomplete hello hello veritabanı ve hello önbellek hello veri almanın çeşitli yollarını hello süresi içinde değil.</span><span class="sxs-lookup"><span data-stu-id="21fa6-360">Not hello differences in hello time it takes toocomplete hello various ways of retrieving hello data from hello database and hello cache.</span></span>

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a><span data-ttu-id="21fa6-361">Merhaba uygulama ile işiniz bittiğinde hello kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="21fa6-361">Delete hello resources when you are finished with hello application</span></span>
<span data-ttu-id="21fa6-362">Merhaba örnek öğretici uygulamasıyla işiniz bittiğinde, hello Azure silebilirsiniz maliyet sipariş tooconserve içinde kullanılan kaynakları ve kaynakları.</span><span class="sxs-lookup"><span data-stu-id="21fa6-362">When you are finished with hello sample tutorial application, you can delete hello Azure resources used in order tooconserve cost and resources.</span></span> <span data-ttu-id="21fa6-363">Merhaba kullanırsanız **tooAzure dağıtmak** hello düğmesini [sağlama hello Azure kaynaklarını](#provision-the-azure-resources) bölümü ve tüm kaynaklarınız hello bulunur aynı kaynak grubunu silebilirsiniz bunları birlikte birinde Merhaba kaynak grubunu silerek işlemi.</span><span class="sxs-lookup"><span data-stu-id="21fa6-363">If you use hello **Deploy tooAzure** button in hello [Provision hello Azure resources](#provision-the-azure-resources) section and all of your resources are contained in hello same resource group, you can delete them together in one operation by deleting hello resource group.</span></span>

1. <span data-ttu-id="21fa6-364">İçinde toohello oturum [Azure portal](https://portal.azure.com) tıklatıp **kaynak grupları**.</span><span class="sxs-lookup"><span data-stu-id="21fa6-364">Sign in toohello [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="21fa6-365">Tür hello hello kutusuna kaynak grubunuzun adını **öğeleri Filtrele...**  metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="21fa6-365">Type hello name of your resource group into hello **Filter items...** textbox.</span></span>
3. <span data-ttu-id="21fa6-366">Tıklatın **...**  kaynak grubunuzun sağındaki toohello.</span><span class="sxs-lookup"><span data-stu-id="21fa6-366">Click **...** toohello right of your resource group.</span></span>
4. <span data-ttu-id="21fa6-367">**Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-367">Click **Delete**.</span></span>
   
    ![Sil][cache-delete-resource-group]
5. <span data-ttu-id="21fa6-369">Tür hello adını tıklatın ve kaynak grubu **silmek**.</span><span class="sxs-lookup"><span data-stu-id="21fa6-369">Type hello name of your resource group and click **Delete**.</span></span>
   
    ![Silmeyi onayla][cache-delete-confirm]

<span data-ttu-id="21fa6-371">Sonra birkaç dakika sonra hello kaynak grubu ve içerdiği kaynakların tümü silinir.</span><span class="sxs-lookup"><span data-stu-id="21fa6-371">After a few moments hello resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21fa6-372">Bir kaynak grubunu silme işlemi geri alınamaz olduğunu ve hello kaynak grubunu ve tüm hello kaynaklar kalıcı olarak silindiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="21fa6-372">Note that deleting a resource group is irreversible and that hello resource group and all hello resources in it are permanently deleted.</span></span> <span data-ttu-id="21fa6-373">Yanlışlıkla hello yanlış kaynak grubunu veya kaynakları silmediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="21fa6-373">Make sure that you do not accidentally delete hello wrong resource group or resources.</span></span> <span data-ttu-id="21fa6-374">Bu örnek varolan bir kaynak grubu içinde barındırmak için hello kaynaklar oluşturduysanız, her kaynağı kendi ilgili dikey penceresinden tek tek silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21fa6-374">If you created hello resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a><span data-ttu-id="21fa6-375">Yerel makinenizde Hello örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="21fa6-375">Run hello sample application on your local machine</span></span>
<span data-ttu-id="21fa6-376">toorun hello uygulamayı makinenizde yerel olarak Azure Redis Önbelleği'bir gereksinim, verilerinizi hangi toocache örneği.</span><span class="sxs-lookup"><span data-stu-id="21fa6-376">toorun hello application locally on your machine, you need an Azure Redis Cache instance in which toocache your data.</span></span> 

* <span data-ttu-id="21fa6-377">Merhaba önceki bölümde açıklandığı gibi uygulama tooAzure yayımladıysanız, bu adım sırasında sağlanan hello Azure Redis önbelleği örneği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21fa6-377">If you have published your application tooAzure as described in hello previous section, you can use hello Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="21fa6-378">Başka bir var olan Azure Redis önbelleği örneği varsa, o toorun Bu örneği yerel olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21fa6-378">If you have another existing Azure Redis Cache instance, you can use that toorun this sample locally.</span></span>
* <span data-ttu-id="21fa6-379">Toocreate bir Azure Redis önbelleği örneğine ihtiyacınız varsa, hello adımları takip edebilirsiniz [bir önbellek oluşturma](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="21fa6-379">If you need toocreate an Azure Redis Cache instance, you can follow hello steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="21fa6-380">Seçtikten veya hello önbellek toouse oluşturduktan sonra toohello Önbelleği'nde hello Azure portalına göz atın ve hello almak [ana bilgisayar adı](cache-configure.md#properties) ve [erişim anahtarları](cache-configure.md#access-keys) önbelleğiniz için.</span><span class="sxs-lookup"><span data-stu-id="21fa6-380">Once you have selected or created hello cache toouse, browse toohello cache in hello Azure portal and retrieve hello [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="21fa6-381">Yönergeler için bkz. [Redis önbelleği ayarlarını yapılandırma](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="21fa6-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="21fa6-382">Açık hello `WebAppPlusCacheAppSecrets.config` hello sırasında oluşturulan dosyası [hello uygulama toouse Redis önbelleği yapılandırma](#configure-the-application-to-use-redis-cache) hello düzenleyiciyi kullanarak bu öğreticinin adımı.</span><span class="sxs-lookup"><span data-stu-id="21fa6-382">Open hello `WebAppPlusCacheAppSecrets.config` file that you created during hello [Configure hello application toouse Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using hello editor of your choice.</span></span>
2. <span data-ttu-id="21fa6-383">Merhaba Düzenle `value` özniteliği ve değiştirme `MyCache.redis.cache.windows.net` hello ile [ana bilgisayar adı](cache-configure.md#properties) , önbellek ve her iki hello belirtin [birincil veya ikincil anahtarı](cache-configure.md#access-keys) hello parola olarak önbelleğinizin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-383">Edit hello `value` attribute and replace `MyCache.redis.cache.windows.net` with hello [host name](cache-configure.md#properties) of your cache, and specify either hello [primary or secondary key](cache-configure.md#access-keys) of your cache as hello password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="21fa6-384">Tuşuna **Ctrl + F5** toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="21fa6-384">Press **Ctrl+F5** toorun hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="21fa6-385">Merhaba uygulaması hello veritabanı dahil olmak üzere, yerel olarak çalıştığı ve hello Redis önbelleği, Azure'da barındırılan önbellek hello Not toounder görünebilir-hello veritabanı gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-385">Note that because hello application, including hello database, is running locally and hello Redis Cache is hosted in Azure, hello cache may appear toounder-perform hello database.</span></span> <span data-ttu-id="21fa6-386">En iyi performans için istemci uygulaması hello ve Azure Redis önbelleği örneği hello olmalıdır aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="21fa6-386">For best performance, hello client application and Azure Redis Cache instance should be in hello same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="21fa6-387">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21fa6-387">Next steps</span></span>
* <span data-ttu-id="21fa6-388">Daha fazla bilgi edinmek [ASP.NET MVC 5 ile çalışmaya başlama](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) hello üzerinde [ASP.NET](http://asp.net/) site.</span><span class="sxs-lookup"><span data-stu-id="21fa6-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on hello [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="21fa6-389">App Service'te bir ASP.NET Web uygulaması oluşturma daha fazla örnek için bkz: [oluşturma ve Azure App Service'te bir ASP.NET web uygulaması dağıtma](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) hello gelen [tanıtımında](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="21fa6-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="21fa6-390">Merhaba tanıtımında demo öğesinden daha fazla quickstarts için bkz: [Azure geliştirici araçları hızlı başlangıç ipuçları](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="21fa6-390">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="21fa6-391">Merhaba hakkında daha fazla bilgi [kod ilk tooa yeni veritabanı](https://msdn.microsoft.com/data/jj193542) tooEntity Bu öğreticide kullanılan Framework yaklaşımını.</span><span class="sxs-lookup"><span data-stu-id="21fa6-391">Learn more about hello [Code first tooa new database](https://msdn.microsoft.com/data/jj193542) approach tooEntity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="21fa6-392">[Azure App Service’deki web uygulamaları](../app-service-web/app-service-web-overview.md) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="21fa6-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="21fa6-393">Nasıl çok öğrenin[İzleyici](cache-how-to-monitor.md) hello Azure portal, önbellekte.</span><span class="sxs-lookup"><span data-stu-id="21fa6-393">Learn how too[monitor](cache-how-to-monitor.md) your cache in hello Azure portal.</span></span>
* <span data-ttu-id="21fa6-394">Azure Redis Cache premium özelliklerini keşfedin</span><span class="sxs-lookup"><span data-stu-id="21fa6-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="21fa6-395">Nasıl tooconfigure kalıcılığını Premium Azure Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="21fa6-395">How tooconfigure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="21fa6-396">Nasıl bir Premium Azure Redis önbelleği için kümeleri tooconfigure</span><span class="sxs-lookup"><span data-stu-id="21fa6-396">How tooconfigure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="21fa6-397">Sanal ağ tooconfigure Premium Azure Redis önbelleği için nasıl destekler</span><span class="sxs-lookup"><span data-stu-id="21fa6-397">How tooconfigure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="21fa6-398">Merhaba bkz [Azure Redis önbelleği SSS](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) boyut, işleme ve premium önbelleklere sahip bant genişliği hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="21fa6-398">See hello [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

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

