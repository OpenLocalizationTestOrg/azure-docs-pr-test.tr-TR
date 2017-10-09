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
# <a name="how-toocreate-a-web-app-with-redis-cache"></a>Nasıl toocreate Redis önbelleği ile Web uygulaması
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Bu öğreticide gösterilmiştir nasıl toocreate ve ASP.NET web uygulaması tooa web uygulamasını Azure App Service'de Visual Studio 2017 kullanarak dağıtın. Hello örnek uygulama bir veritabanındaki ekip istatistiklerinin listesini görüntüler ve farklı şekillerde toouse Azure Redis önbelleği toostore gösterir ve hello önbellekten veri alın. Merhaba öğreticiyi tamamladığınızda okur ve Azure Redis önbelleği ile en iyi duruma getirilmiş ve barındırılan tooa veritabanı, Azure'da yazan çalışan bir web uygulamasına sahip olacaksınız.

Şunları öğreneceksiniz:

* Nasıl toocreate bir ASP.NET MVC 5 web uygulamasını Visual Studio'da.
* Nasıl Entity Framework kullanarak bir veritabanındaki tooaccess verileri.
* Nasıl tooimprove veri işleme ve depolama ve Azure Redis önbelleği kullanılarak veri alma veritabanı yükünü azaltma.
* Nasıl toouse bir Redis kümesi tooretrieve hello en iyi 5 ekibi sıralanır.
* Nasıl tooprovision Resource Manager şablonu kullanarak Merhaba uygulaması için Azure kaynaklarını hello.
* Nasıl toopublish, Visual Studio kullanarak uygulama tooAzure hello.

## <a name="prerequisites"></a>Ön koşullar
toocomplete hello Öğreticisi önkoşulları aşağıdaki hello olması gerekir.

* [Azure hesabı](#azure-account)
* [Merhaba .NET için Azure SDK ile Visual Studio 2017](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a>Azure hesabı
Bir Azure hesabı toocomplete hello öğretici gerekir. Şunları yapabilirsiniz:

* [Ücretsiz bir Azure hesabı açın](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). Out kullanılan tootry Ücretli Azure hizmetlerini olabilir krediler alırsınız. Hatta hello krediler bitmiş olsa, hello hesabı sürdürebilir ve ücretsiz Azure hizmetlerini ve özellikleri kullanın.
* [Visual Studio abone avantajları etkinleştirin](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). MSDN aboneliğiniz, ücretli Azure hizmetlerinizi kullanabildiğiniz her ay size kredi verir.

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a>Merhaba .NET için Azure SDK ile Visual Studio 2017
Başlangıç öğreticisi için Visual Studio 2017 hello ile yazılmış [.NET için Azure SDK](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools). Hello Azure SDK'sı 2.9.5 hello Visual Studio Yükleyicisi ile birlikte gelir.

Visual Studio 2015 varsa, hello hello öğreticiyi izleyebilirsiniz [.NET için Azure SDK](../dotnet-sdk.md) 2.8.2 veya sonraki bir sürümü. [Yükleme son Azure SDK'sını buradan Visual Studio 2015 için hello](http://go.microsoft.com/fwlink/?linkid=518003). Zaten yoksa, visual Studio SDK hello ile otomatik olarak yüklenir. Bazı ekranlar Bu öğreticide gösterilen hello çizimler farklı görünebilir.

Visual Studio 2013 varsa [indirme Visual Studio 2013 için en son Azure SDK'sını hello](http://go.microsoft.com/fwlink/?LinkID=324322). Bazı ekranlar Bu öğreticide gösterilen hello çizimler farklı görünebilir.

## <a name="create-hello-visual-studio-project"></a>Merhaba Visual Studio projesi oluşturma
1. Visual Studio’yu açın ve **Dosya**, **Yeni**, **Proje**’yi tıklayın.
2. Merhaba genişletin **Visual C#** hello düğümünde **şablonları** listesinde **bulut**, tıklatıp **ASP.NET Web uygulaması**. **.NET Framework 4.5.2** veya daha yüksek bir sürümün seçili olduğundan emin olun.  Tür **ContosoTeamStats** hello içine **adı** textbox tıklatıp **Tamam**.
   
    ![Proje oluşturma][cache-create-project]
3. Seçin **MVC** hello proje türü olarak. 

    Emin **doğrulaması yok** Merhaba belirtilen **kimlik doğrulaması** ayarlar. Visual Studio sürümüne bağlı olarak, hello varsayılan toosomething başka ayarlanabilir. toochange, tıklatın **kimlik doğrulamayı Değiştir** seçip **doğrulaması yok**.

    Visual Studio 2015 ile birlikte izliyorsanız, hello temizleyin **hello buluttaki konağa** onay kutusu. Artıracaksınız [sağlama Azure kaynaklarını hello](#provision-the-azure-resources) ve [yayımlama hello uygulama tooAzure](#publish-the-application-to-azure) hello öğreticide sonraki adımlarda. Bırakarak Visual Studio'dan bir App Service web uygulaması hazırlama örneği için **hello buluttaki konağa** işaretli bkz [ASP.NET ve Visual Studio kullanarak Azure App Service'te Web uygulamalarını kullanmaya başlama](../app-service-web/app-service-web-get-started-dotnet.md).
   
    ![Proje şablonu seçme][cache-select-template]
4. Tıklatın **Tamam** toocreate hello projesi.

## <a name="create-hello-aspnet-mvc-application"></a>Merhaba ASP.NET MVC uygulaması oluşturma
Merhaba öğreticinin bu bölümünde okur ve veritabanından ekip istatistiklerini görüntüleyen hello temel uygulamayı oluşturacaksınız.

* [Merhaba Entity Framework NuGet paketi ekleme](#add-the-entity-framework-nuget-package)
* [Merhaba modeli ekleme](#add-the-model)
* [Merhaba denetleyici ekleyin](#add-the-controller)
* [Merhaba görünümlerini yapılandırma](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a>Merhaba Entity Framework NuGet paketi ekleme

1. Tıklatın **NuGet Paket Yöneticisi**, **Paket Yöneticisi Konsolu** hello gelen **Araçları** menüsü.
2. Çalışma hello hello komuttan aşağıdaki **Paket Yöneticisi Konsolu** penceresi.
    
    ```
    Install-Package EntityFramework
    ```

Bu paketi hakkında daha fazla bilgi için bkz: Merhaba [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet sayfası.

### <a name="add-hello-model"></a>Merhaba modeli ekleme
1. **Çözüm Gezgini**’nde **Modeller**’e sağ tıklayın ve **Ekle**, **Sınıf**’ı seçin. 
   
    ![Model ekleme][cache-model-add-class]
2. Girin `Team` hello sınıfı adı ve tıklatın **Ekle**.
   
    ![Model sınıfı ekleme][cache-model-add-class-dialog]
3. Hello yerine `using` deyimleri hello hello üstündeki `Team.cs` hello aşağıdaki dosyasıyla `using` deyimleri.

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. Merhaba Hello tanımını değiştirin `Team` güncelleştirilmiş içeren kod parçacığını aşağıdaki hello sınıfıyla `Team` bazı diğer Entity Framework yardımcı sınıflarının yanı sıra tanımı sınıf. Merhaba kod ilk yaklaşım tooEntity Bu öğreticide kullanılan Framework hakkında daha fazla bilgi için bkz: [kod ilk tooa yeni veritabanı](https://msdn.microsoft.com/data/jj193542).

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


1. İçinde **Çözüm Gezgini**, çift **web.config** tooopen onu.
   
    ![Web.config][cache-web-config]
2. Merhaba aşağıdakileri ekleyin `connectionStrings` bölümü. Merhaba hello bağlantı dizesinin adını hello olan Entity Framework veritabanı bağlamı sınıfının hello adı eşleşmelidir `TeamContext`.

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Merhaba yeni ekleyebilirsiniz `connectionStrings` kendisini izleyen bölümüne `configSections`hello aşağıdaki örnekte gösterildiği gibi.

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
    > Bağlantı dizenizi Visual Studio hello sürümüne bağlı olarak farklı olabilir ve SQL Server Express edition toocomplete hello öğretici kullanılır. Merhaba web.config şablonu yapılandırılmış toomatch yüklemenizi olmalıdır ve içerebilir `Data Source` girişleri ister `(LocalDB)\v11.0` (gelen SQL Server Express 2012) veya `Data Source=(LocalDB)\MSSQLLocalDB` (SQL Server 2014'ün hızlı ve daha yeni). Bağlantı dizeleri ve SQL Express sürümleri hakkında daha fazla bilgi için bkz. [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .

### <a name="add-hello-controller"></a>Merhaba denetleyici ekleyin
1. Tuşuna **F6** toobuild hello projesi. 
2. İçinde **Çözüm Gezgini**, sağ hello **denetleyicileri** klasör ve **Ekle**, **denetleyicisi**.
   
    ![Denetleyici ekleme][cache-add-controller]
3. **Görünümlere sahip MVC 5 Denetleyici, Entity Framework kullanarak** öğesini seçin ve **Ekle**’ye tıklayın. ' I tıklattıktan sonra bir hata alırsanız **Ekle**, size hello önce projeyi oluşturduğunuzdan emin olun.
   
    ![Denetleyici sınıfı ekleme][cache-add-controller-class]
4. Seçin **ekip (ContosoTeamStats.Models)** hello gelen **Model sınıfı** aşağı açılan liste. Seçin **TeamContext (ContosoTeamStats.Models)** hello gelen **veri bağlamı sınıfı** aşağı açılan liste. Tür `TeamsController` hello içinde **denetleyicisi** (bunu otomatik olarak doldurulmamışsa) adı metin. Tıklatın **Ekle** toocreate hello denetleyici sınıfı ve hello varsayılan görünümler ekleyebilir.
   
    ![Denetleyici yapılandırma][cache-configure-controller]
5. İçinde **Çözüm Gezgini**, genişletin **Global.asax** çift tıklayın ve **Global.asax.cs** tooopen onu.
   
    ![Global.asax.cs][cache-global-asax]
6. İki aşağıdaki hello eklemek `using` deyimleri hello dosyanın üst kısmındaki hello hello diğer altında `using` deyimleri.

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. Aşağıdaki kod hello hello sonunda hello eklemek `Application_Start` yöntemi.

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. **Çözüm Gezgini**’nde, `App_Start` öğesini genişletin ve `RouteConfig.cs` öğesine çift tıklayın.
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. Değiştir `controller = "Home"` hello kodda aşağıdaki hello içinde `RegisterRoutes` yöntemiyle `controller = "Teams"` hello aşağıdaki örnekte gösterildiği gibi.

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a>Merhaba görünümlerini yapılandırma
1. İçinde **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü ve ardından hello **paylaşılan** klasörü ve çift **_Layout.cshtml**. 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. Değiştirme hello Merhaba içeriğine `title` öğesi ve Değiştir `My ASP.NET Application` ile `Contoso Team Stats` hello aşağıdaki örnekte gösterildiği gibi.

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. Merhaba, `body` bölümünde, ilk hello güncelleştirme `Html.ActionLink` deyimi ve Değiştir `Application name` ile `Contoso Team Stats` ve değiştirme `Home` ile `Teams`.
   
   * Önce: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`
   * Sonra: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`
     
     ![Kod değişiklikleri][cache-layout-cshtml-code]
2. Tuşuna **Ctrl + F5** toobuild ve Çalıştır Merhaba uygulaması. Merhaba uygulamasının bu sürümü hello sonuçları doğrudan hello veritabanından okur. Not hello **Yeni Oluştur**, **Düzenle**, **ayrıntıları**, ve **silmek** otomatik olarak olan eylemler tarafından hello toohello uygulama eklendi **Entity Framework kullanarak MVC 5 denetleyici, görünümleri olan** ayarlayın. Merhaba sonraki bölümde hello öğreticinin Redis önbelleği toooptimize hello veri erişimi ve toohello uygulamaya ek özellikler sağlamak ekleyeceksiniz.

![Başlangıç uygulaması][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a>Merhaba uygulama toouse Redis önbelleği yapılandırma
Merhaba öğreticinin bu bölümünde, hello örnek uygulama toostore yapılandırmak ve Başlangıç'ı kullanarak Azure Redis önbelleği örneği Contoso ekip istatistiklerini almak [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) önbellek istemcisi.

* [Merhaba uygulama toouse StackExchange.Redis yapılandırma](#configure-the-application-to-use-stackexchangeredis)
* [Hello TeamsController sınıfını tooreturn sonuçları hello önbellek veya hello veritabanından güncelleştir](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [Merhaba oluşturma, düzenleme, güncelleştirme ve yöntemleri toowork hello önbelleği ile silme](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [Merhaba ekipler dizini görünümünü toowork hello önbelleği ile güncelleştirme](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a>Merhaba uygulama toouse StackExchange.Redis yapılandırma
1. tooconfigure Visual Studio'da hello StackExchange.Redis NuGet paketi kullanarak bir istemci uygulaması tıklatın **NuGet Paket Yöneticisi**, **Paket Yöneticisi Konsolu** hello gelen **Araçları** menüsü.
2. Çalışma hello hello komuttan aşağıdaki `Package Manager Console` penceresi.
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    Merhaba paketi indirir ve hello ekler NuGet derleme başvurularını hello StackExchange.Redis önbellek istemcisi ile istemci uygulaması tooaccess Azure Redis önbelleği için gereklidir. Toouse hello tanımlayıcı adlı bir sürümünü tercih ederseniz `StackExchange.Redis` istemci kitaplığı, yükleme hello `StackExchange.Redis.StrongName` paket.
3. İçinde **Çözüm Gezgini**, hello genişletin **denetleyicileri** klasörü ve çift **TeamsController.cs** tooopen onu.
   
    ![Ekip denetleyicisi][cache-teamscontroller]
4. İki aşağıdaki hello eklemek `using` deyimleri çok**TeamsController.cs**.

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. İki özellikleri toohello aşağıdaki hello eklemek `TeamsController` sınıfı.

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

6. Bilgisayarınızda adlı bir dosya oluşturun `WebAppPlusCacheAppSecrets.config` ve karar toocheck örnek uygulamanızın hello kaynak kodu ile denetlenmeyecek bir konuma yerleştirin, başka bir yere içinde. Bu örnek hello içinde `AppSettingsSecrets.config` dosya adresindedir `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.
   
    Merhaba Düzenle `WebAppPlusCacheAppSecrets.config` dosya ve içeriği aşağıdaki hello ekleyin. Merhaba uygulama yerel olarak çalıştırırsanız bu bilgiler kullanılan tooconnect tooyour Azure Redis önbelleği örneği olur. Daha sonra hello öğreticide bir Azure Redis önbelleği örneği hazırlayacak ve hello önbellek adı ve parolasını güncelleştirin. Toorun Merhaba örnek uygulaması planlamıyorsanız hello oluşturma bu dosyanın yerel olarak atlayabilirsiniz ve tooAzure hello uygulama dağıttığınızda bulunduğundan hello dosya başvuru hello sonraki adımları hello uygulamadan hello önbellek bağlantı bilgilerini alır Merhaba Web uygulaması için ve bu dosyadan ayarlama. Merhaba itibaren `WebAppPlusCacheAppSecrets.config` dağıtılmadığı tooAzure uygulamanız ile yapmanıza gerek yoktur, toorun hello uygulamayı yerel olarak çalıştırmayacağınız sürece.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. İçinde **Çözüm Gezgini**, çift **web.config** tooopen onu.
   
    ![Web.config][cache-web-config]
2. Merhaba aşağıdakileri ekleyin `file` toohello özniteliği `appSettings` öğesi. Farklı bir dosya adı veya konumu kullandıysanız, bu değerleri hello hello örnekte gösterilen olanları değiştirin.
   
   * Önce: `<appSettings>`
   * Sonra: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`
     
   Merhaba ASP.NET çalışma zamanı hello hello hello biçimlendirme ile Merhaba harici dosyasının içeriğini birleştirir `<appSettings>` öğesi. Merhaba belirtilen dosya bulunamazsa hello çalışma zamanı hello dosya özniteliğini yok sayar. Gizli anahtarlarınız (Merhaba bağlantı dizesi tooyour önbellek) hello Merhaba uygulaması için kaynak kodu parçası olarak dahil edilmez. Web uygulaması tooAzure dağıttığınızda, hello `WebAppPlusCacheAppSecrests.config` (yani istediğinizi) dosyası dağıtılmaz. Azure'da bu Sırları birkaç yolu toospecify vardır ve Bu öğreticide bunlar otomatik olarak sizin için yapılandırılmış zaman, [sağlama Azure kaynaklarını hello](#provision-the-azure-resources) bir sonraki öğretici adımında. Azure'daki gizli anahtarlarla çalışma hakkında daha fazla bilgi için bkz: [en iyi uygulamalar parolalar ve diğer hassas verileri tooASP.NET ve Azure uygulama hizmeti dağıtmak için](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a>Hello TeamsController sınıfını tooreturn sonuçları hello önbellek veya hello veritabanından güncelleştir
Bu örnekte, ekip istatistikleri hello veritabanından veya hello önbellekten alınabilir. Ekip istatistiklerini seri hale getirilmiş bir hello önbelleğinde depolandığı `List<Team>`hem de Redis veri türleri kullanılarak sıralanmış bir küme olarak. Bir sıralanmış kümeden öğeleri alırken, belirli öğeler için bazı, tümü veya sorgu alabilirsiniz. Bu örnekte kazanma sayısına göre derece hello iyi 5 ekip için sıralanmış hello kümesi sorgulayacaksınız.

> [!NOTE]
> Gerekli toostore hello ekip istatistiklerini sipariş toouse Azure Redis önbelleği hello önbellekte çoklu biçimlerde olmadığı. Bu öğretici birden çok biçimleri toodemonstrate bazı kullanır hello farklı yolları ve farklı veri türleri toocache verileri kullanabilirsiniz.
> 
> 

1. Merhaba aşağıdakileri ekleyin `using` deyimleri toohello `TeamsController.cs` hello diğer ile Merhaba üstünde dosya `using` deyimleri.

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. Merhaba geçerli Değiştir `public ActionResult Index()` uygulama aşağıdaki hello uygulamasıyla yöntemi.

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


1. Aşağıdaki üç yöntem toohello hello eklemek `TeamsController` sınıfı tooimplement hello `playGames`, `clearCache`, ve `rebuildDB` eylemin hello türlerinden geçiş hello önceki kod parçacığında eklenen deyimi.
   
    Merhaba `PlayGames` yöntemi, oyun sezonunu taklit ederek hello ekip istatistiklerini güncelleştirir, kaydeder hello sonuçları toohello veritabanı ve temizler hello artık güncel olmayan hello önbelleğinden veri.

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

    Merhaba `RebuildDB` yöntemi yeniden başlatmak hello hello varsayılan ekip, kümesine veritabanıyla bunlar için İstatistikler oluşturur ve temizler hello artık güncel olmayan hello önbelleğinden veri.

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

    Merhaba `ClearCachedTeams` yöntemi önbellekteki ekip istatistiklerini hello önbellekten kaldırır.

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. Aşağıdaki dört yöntemleri toohello hello eklemek `TeamsController` sınıfı tooimplement hello hello önbellek ve hello veritabanı hello ekip istatistiklerini almanın çeşitli yollarını. Bu yöntemlerin her biri döndüren bir `List<Team>` sonra görüntülendiği göre hello görüntüleyin.
   
    Merhaba `GetFromDB` yöntemi hello veritabanından hello ekip istatistiklerini okur.
   
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

    Merhaba `GetFromList` yöntemi seri hale getirilmiş bir hello ekip istatistiklerini okur `List<Team>`. Önbellek isabetsizliği varsa, hello ekip istatistiklerini hello veritabanından okunur ve ardından gelecek sefer için hello önbellekte depolanır. Bu örnekte biz JSON.NET serileştirme tooserialize hello .NET nesneleri tooand hello önbellekten kullanıyorsunuz. Daha fazla bilgi için bkz: [nasıl toowork .NET ile Azure Redis Önbelleği'nde nesneleri](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

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

    Merhaba `GetFromSortedSet` yöntemi önbelleğe alınan bir sıralanmış kümeden hello ekip istatistiklerini okur. Önbellek isabetsizliği varsa, hello ekip istatistiklerini hello veritabanından okunur ve bir sıralanmış küme olarak hello önbelleğinde depolanır.

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

    Merhaba `GetFromSortedSetTop5` yöntemi hello üst 5 takımlara hello önbelleğe alınan sıralanmış kümesi okur. Merhaba hello varlığı hello önbelleği denetleyerek başlar `teamsSortedSet` anahtarı. Bu anahtar mevcut değilse hello `GetFromSortedSet` yöntemi tooread hello ekip istatistiklerini olarak adlandırılır ve hello önbelleğine depolayabilirsiniz. Ardından, hello önbelleğe alınan sıralanmış küme, döndürülen hello iyi 5 ekip için sorgulanır.

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

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a>Merhaba oluşturma, düzenleme, güncelleştirme ve yöntemleri toowork hello önbelleği ile silme
Bu örnek bölümü yöntemleri tooadd içerdiği gibi oluşturan hello iskele kurma kodu düzenleyebilir ve takımlar silebilirsiniz. Bir takım eklediyseniz, düzenlenebilir veya kaldırılan herhangi bir zamanda, hello önbelleğinde hello veriler güncel olmayan hale gelir. Değiştireceğiniz Bu bölümde, bu üç yöntem tooclear hello takımlar önbelleğe Hello önbellek hello veritabanı ile eşitlenmemiş olmayacaktır.

1. Toohello Gözat `Create(Team team)` hello yönteminde `TeamsController` sınıfı. Çağrı toohello ekleme `ClearCachedTeams` hello aşağıdaki örnekte gösterildiği gibi yöntemi.

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


1. Toohello Gözat `Edit(Team team)` hello yönteminde `TeamsController` sınıfı. Çağrı toohello ekleme `ClearCachedTeams` hello aşağıdaki örnekte gösterildiği gibi yöntemi.

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


1. Toohello Gözat `DeleteConfirmed(int id)` hello yönteminde `TeamsController` sınıfı. Çağrı toohello ekleme `ClearCachedTeams` hello aşağıdaki örnekte gösterildiği gibi yöntemi.

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


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a>Merhaba ekipler dizini görünümünü toowork hello önbelleği ile güncelleştirme
1. İçinde **Çözüm Gezgini**, hello genişletin **görünümleri** klasörünü seçip hello **takımlar** klasörü ve çift **Index.cshtml**.
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. Merhaba dosyasının üst kısmında hello, paragraf öğesini aşağıdaki Merhaba arayın.
   
    ![Eylem tablosu][cache-teams-index-table]
   
    Merhaba bağlantı toocreate yeni bir ekip budur. Merhaba paragraf öğesini aşağıdaki tablonun hello ile değiştirin. Bu tablo bir yeni bir oyun sezonu hello önbelleği temizleme, çalma yeni bir ekip oluşturmak için eylem bağlantıları vardır, hello takımlar hello önbelleğinden çeşitli biçimlerde alma, hello veritabanından hello ekipleri alma ve yeniden oluşturma yeni örnek veriler ile veritabanını hello.

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


1. Merhaba kaydırma toohello alt **Index.cshtml** dosya ve hello aşağıdakileri ekleyin `tr` öğesi hello son satırında hello olmasını sağlamak en son tablo hello dosyasında.
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    Bu satır hello değerini görüntüler `ViewBag.Msg` hello geçerli işlem hakkında bir durum raporu içerir. Merhaba `ViewBag.Msg` hello hello önceki adımdaki eylem bağlantılardan herhangi birine tıkladığınızda ayarlayın.   
   
    ![Durum iletisi][cache-status-message]
2. Tuşuna **F6** toobuild hello projesi.

## <a name="provision-hello-azure-resources"></a>Sağlama Azure kaynaklarını hello
toohost ilk hazırlamalısınız uygulamanızı azure'da uygulamanızın gerektirdiği Azure hizmetlerini hello. Merhaba örnek uygulaması Bu öğreticide Azure Hizmetleri aşağıdaki hello kullanır.

* Azure Redis Cache
* App Service Web Uygulaması
* SQL Database

toodeploy tercih ettiğiniz bu hizmetleri tooa yeni veya var olan kaynak grubunu tıklatın aşağıdaki hello **tooAzure dağıtmak** düğmesi.

[! [TooAzure dağıtım] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)

Bu **tooAzure dağıtmak** düğmesi kullanır hello [bir Web uygulaması artı Redis önbelleği artı SQL veritabanı oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Hızlı Başlangıç](https://github.com/Azure/azure-quickstart-templates) şablon tooprovision bu hizmetleri ve kümesi hello hello Azure Redis önbelleği bağlantı dizesi hello SQL Database ve hello uygulama ayarı için bağlantı dizesi.

> [!NOTE]
> Bir Azure hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir Azure hesabı oluşturabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).
> 
> 

Tıklatmak hello **tooAzure dağıtmak** düğmesini toohello Azure portal alır ve hello hello şablon tarafından açıklanan hello kaynakları oluşturma işlemini başlatır.

![TooAzure dağıtma][cache-deploy-to-azure-step-1]

1. Merhaba, **Temelleri** bölümünde hello Azure aboneliği toouse seçin ve varolan bir kaynak grubu seçin veya yeni bir tane oluşturun ve hello kaynak grubu konumu belirtin.
2. Merhaba, **ayarları** bölümünde, belirtin bir **yönetici oturum açma** (kullanmayan **yönetici**), **yönetici oturum açma parolası**ve  **Veritabanı adı**. Merhaba diğer parametreler boş bir uygulama hizmeti planı ve ücretsiz katman ile birlikte gelen yok hello SQL veritabanı ve Azure Redis önbelleği için daha düşük maliyetli seçenekler sunmak için yapılandırılır.

    ![TooAzure dağıtma][cache-deploy-to-azure-step-2]

3. İstenen hello ayarlarını yapılandırdıktan sonra Başlangıç sayfası, okuma hello hüküm ve koşullar toohello sonuna kaydırın ve hello denetleyin **toohello hüküm ve koşullar yukarıda belirtildiği kabul** onay kutusu.
4. toobegin sağlama hello kaynaklar'ı **satın alma**.

Merhaba bildirim simgesine tıklayın ve'ı tıklatın, dağıtımınızı tooview hello ilerleme **dağıtım başladı**.

![Dağıtım başladı][cache-deployment-started]

Merhaba üzerinde hello dağıtımınızın durumunu görüntüleyebilirsiniz **Microsoft.Template** dikey.

![TooAzure dağıtma][cache-deploy-to-azure-step-3]

Sağlama tamamlandıktan sonra uygulama tooAzure Visual Studio'dan yayımlayabilirsiniz.

> [!NOTE]
> Merhaba sağlama işlemi sırasında oluşabilecek hataları hello üzerinde görüntülenen **Microsoft.Template** dikey. Abonelik başına çok fazla SQL Server veya çok fazla Ücretsiz App Service barındırma planı yaygın hatalardır. Hataları çözümleyin ve tıklayarak hello işlemi yeniden **dağıtmanız** hello üzerinde **Microsoft.Template** dikey veya hello **tooAzure dağıtmak** bu öğreticideki düğmesi.
> 
> 

## <a name="publish-hello-application-tooazure"></a>Yayımlama Hello uygulama tooAzure
Merhaba öğreticinin bu adımında, yayımlama hello uygulama tooAzure ve hello bulutta çalıştırın.

1. Sağ hello **ContosoTeamStats** seçin ve Visual Studio Proje **Yayımla**.
   
    ![Yayımlama][cache-publish-app]
2. **Microsoft Azure App Service**’e tıklayın, **Var Olanı Seç**’i seçin ve **Yayımla**’ya tıklayın.
   
    ![Yayımlama][cache-publish-to-app-service]
3. Hello Azure kaynakları oluşturma hello kaynakları içeren hello kaynak grubunu genişletin ve Web uygulaması seçme hello istenen kullanılan hello aboneliği seçin. Merhaba kullandıysanız **tooAzure dağıtmak** , Web uygulaması adı ile başlayan düğmesi **Web sitesi** bazı ek karakterlerle devam eder.
   
    ![Web Uygulaması Seçme][cache-select-web-app]
4. Tıklatın **Tamam** toobegin hello işlem yayımlama. Birkaç dakika sonra işlem yayımlama hello tamamlanır ve örnek uygulama çalıştırılıyor hello ile bir tarayıcı başlatılır. Doğrularken veya yayımlarken bir DNS hatası alırsanız ve hello sağlama işlemi için hello Merhaba uygulaması için Azure kaynaklarını yalnızca yakın zamanda tamamlandı, kısa bir süre bekleyin ve yeniden deneyin.
   
    ![Önbellek eklendi][cache-added-to-application]

Merhaba aşağıdaki tabloda her eylem bağlantısını hello örnek uygulamadan açıklanmaktadır.

| Eylem | Açıklama |
| --- | --- |
| Yeni Oluştur |Yeni bir Ekip oluşturun. |
| Sezonu Oynat |Bir oyun sezonu, güncelleştirme hello ekip istatistiklerini, yürütmek ve temizleyin herhangi bir ekip verileri hello önbelleğinden eski. |
| Önbelleği Temizle |Hello önbellekten ekip istatistiklerini temizleyin hello. |
| Önbellekten Liste |Merhaba önbellekten Hello ekip istatistiklerini alın. Önbellek isabetsizliği varsa, hello veritabanından hello istatistikleri yükleyin ve bir sonraki seferde toohello önbellek kaydedin. |
| Önbellekten Sıralanmış Küme |Bir sıralanmış küme kullanarak hello önbellekten Hello ekip istatistiklerini alın. Önbellek isabetsizliği varsa, hello veritabanından hello istatistikleri yükleyin ve bir sıralanmış küme kullanarak toohello önbelleği kaydedin. |
| Önbellekteki En İyi 5 Ekip |Bir sıralanmış küme kullanarak hello önbellekten Hello en iyi 5 ekibi alın. Önbellek isabetsizliği varsa, hello veritabanından hello istatistikleri yükleyin ve bir sıralanmış küme kullanarak toohello önbelleği kaydedin. |
| DB’den yükleme |Merhaba veritabanından Hello ekip istatistiklerini alın. |
| DB Yeniden Oluşturma |Merhaba veritabanını yeniden oluşturun ve örnek ekip verileri ile yeniden yükleyin. |
| Düzenle / Ayrıntılar / Sil |Bir ekibi düzenleyin, ekibin ayrıntılarını görüntüleyin, ekibi silin. |

Merhaba eylemlerin bazıları tıklayın ve hello farklı kaynaklardan hello veri alma denemeleri yapın. Hello farklar toocomplete hello hello veritabanı ve hello önbellek hello veri almanın çeşitli yollarını hello süresi içinde değil.

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a>Merhaba uygulama ile işiniz bittiğinde hello kaynakları silin
Merhaba örnek öğretici uygulamasıyla işiniz bittiğinde, hello Azure silebilirsiniz maliyet sipariş tooconserve içinde kullanılan kaynakları ve kaynakları. Merhaba kullanırsanız **tooAzure dağıtmak** hello düğmesini [sağlama hello Azure kaynaklarını](#provision-the-azure-resources) bölümü ve tüm kaynaklarınız hello bulunur aynı kaynak grubunu silebilirsiniz bunları birlikte birinde Merhaba kaynak grubunu silerek işlemi.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) tıklatıp **kaynak grupları**.
2. Tür hello hello kutusuna kaynak grubunuzun adını **öğeleri Filtrele...**  metin kutusu.
3. Tıklatın **...**  kaynak grubunuzun sağındaki toohello.
4. **Sil**'e tıklayın.
   
    ![Sil][cache-delete-resource-group]
5. Tür hello adını tıklatın ve kaynak grubu **silmek**.
   
    ![Silmeyi onayla][cache-delete-confirm]

Sonra birkaç dakika sonra hello kaynak grubu ve içerdiği kaynakların tümü silinir.

> [!IMPORTANT]
> Bir kaynak grubunu silme işlemi geri alınamaz olduğunu ve hello kaynak grubunu ve tüm hello kaynaklar kalıcı olarak silindiğini unutmayın. Yanlışlıkla hello yanlış kaynak grubunu veya kaynakları silmediğinizden emin olun. Bu örnek varolan bir kaynak grubu içinde barındırmak için hello kaynaklar oluşturduysanız, her kaynağı kendi ilgili dikey penceresinden tek tek silebilirsiniz.
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a>Yerel makinenizde Hello örnek uygulamayı çalıştırın
toorun hello uygulamayı makinenizde yerel olarak Azure Redis Önbelleği'bir gereksinim, verilerinizi hangi toocache örneği. 

* Merhaba önceki bölümde açıklandığı gibi uygulama tooAzure yayımladıysanız, bu adım sırasında sağlanan hello Azure Redis önbelleği örneği kullanabilirsiniz.
* Başka bir var olan Azure Redis önbelleği örneği varsa, o toorun Bu örneği yerel olarak kullanabilirsiniz.
* Toocreate bir Azure Redis önbelleği örneğine ihtiyacınız varsa, hello adımları takip edebilirsiniz [bir önbellek oluşturma](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

Seçtikten veya hello önbellek toouse oluşturduktan sonra toohello Önbelleği'nde hello Azure portalına göz atın ve hello almak [ana bilgisayar adı](cache-configure.md#properties) ve [erişim anahtarları](cache-configure.md#access-keys) önbelleğiniz için. Yönergeler için bkz. [Redis önbelleği ayarlarını yapılandırma](cache-configure.md#configure-redis-cache-settings).

1. Açık hello `WebAppPlusCacheAppSecrets.config` hello sırasında oluşturulan dosyası [hello uygulama toouse Redis önbelleği yapılandırma](#configure-the-application-to-use-redis-cache) hello düzenleyiciyi kullanarak bu öğreticinin adımı.
2. Merhaba Düzenle `value` özniteliği ve değiştirme `MyCache.redis.cache.windows.net` hello ile [ana bilgisayar adı](cache-configure.md#properties) , önbellek ve her iki hello belirtin [birincil veya ikincil anahtarı](cache-configure.md#access-keys) hello parola olarak önbelleğinizin.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. Tuşuna **Ctrl + F5** toorun Merhaba uygulaması.

> [!NOTE]
> Merhaba uygulaması hello veritabanı dahil olmak üzere, yerel olarak çalıştığı ve hello Redis önbelleği, Azure'da barındırılan önbellek hello Not toounder görünebilir-hello veritabanı gerçekleştirin. En iyi performans için istemci uygulaması hello ve Azure Redis önbelleği örneği hello olmalıdır aynı konumu. 
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [ASP.NET MVC 5 ile çalışmaya başlama](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) hello üzerinde [ASP.NET](http://asp.net/) site.
* App Service'te bir ASP.NET Web uygulaması oluşturma daha fazla örnek için bkz: [oluşturma ve Azure App Service'te bir ASP.NET web uygulaması dağıtma](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) hello gelen [tanıtımında](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).
  * Merhaba tanıtımında demo öğesinden daha fazla quickstarts için bkz: [Azure geliştirici araçları hızlı başlangıç ipuçları](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).
* Merhaba hakkında daha fazla bilgi [kod ilk tooa yeni veritabanı](https://msdn.microsoft.com/data/jj193542) tooEntity Bu öğreticide kullanılan Framework yaklaşımını.
* [Azure App Service’deki web uygulamaları](../app-service-web/app-service-web-overview.md) hakkında daha fazla bilgi edinin.
* Nasıl çok öğrenin[İzleyici](cache-how-to-monitor.md) hello Azure portal, önbellekte.
* Azure Redis Cache premium özelliklerini keşfedin
  
  * [Nasıl tooconfigure kalıcılığını Premium Azure Redis önbelleği](cache-how-to-premium-persistence.md)
  * [Nasıl bir Premium Azure Redis önbelleği için kümeleri tooconfigure](cache-how-to-premium-clustering.md)
  * [Sanal ağ tooconfigure Premium Azure Redis önbelleği için nasıl destekler](cache-how-to-premium-vnet.md)
  * Merhaba bkz [Azure Redis önbelleği SSS](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) boyut, işleme ve premium önbelleklere sahip bant genişliği hakkında daha fazla ayrıntı için.

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

