---
title: "Merhaba .NET arka uç sunucusu için Mobile Apps SDK'sı ile aaaHow toowork | Microsoft Docs"
description: "Nasıl toowork ile Merhaba .NET arka uç sunucusu SDK Azure App Service Mobile Apps için öğrenin."
keywords: "uygulama hizmeti, azure uygulama hizmeti, mobil uygulama, mobil hizmet, Ölçek, ölçeklenebilir, uygulama dağıtımı, azure uygulama dağıtımı"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a>Azure Mobile Apps için Hello .NET arka uç sunucusu SDK ile çalışma
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

Bu konu nasıl toouse hello anahtar Azure App Service Mobile Apps senaryolarda .NET arka uç sunucusu SDK gösterir. Hello Azure Mobile Apps SDK'sı, ASP.NET uygulamanız mobil istemcilerden çalışmanıza yardımcı olur.

> [!TIP]
> Merhaba [.NET server için Azure Mobile Apps SDK] [ 2] github'da açık bir kaynaktır. Merhaba depo hello tüm sunucu SDK birim test paketi ve bazı örnek projeler de dahil olmak üzere tüm kaynak kodunu içerir.
>
>

## <a name="reference-documentation"></a>Başvuru belgeleri
Merhaba sunucusu SDK Hello başvuru belgelerine bulunduğu burada: [Azure Mobile Apps .NET başvurusu][1].

## <a name="create-app"></a>Nasıl yapılır: bir .NET Mobil uygulama arka ucu oluşturma
Yeni bir proje başlıyorsanız, her iki hello kullanarak bir uygulama hizmeti uygulaması oluşturabilir [Azure portalı] veya Visual Studio. Merhaba App Service uygulama yerel olarak çalıştırmak veya hello proje tooyour bulut tabanlı uygulama hizmeti mobil uygulama yayımlayın.

Mobil özelliklerini tooan mevcut proje ekliyorsanız, hello bkz [indirin ve hello SDK başlatma](#install-sdk) bölümü.

### <a name="create-a-net-backend-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir .NET arka ucu oluşturma
bir uygulama hizmeti mobil arka uç toocreate, ya da izleyin hello [hızlı başlangıç Öğreticisi] [ 3] veya şu adımları izleyin:

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

Merhaba edilene *başlama* dikey altında **tablo API Oluştur**, seçin **C#** olarak, **arka uç dilinizi**. Tıklatın **karşıdan**sıkıştırılmış proje dosyalarını tooyour yerel bilgisayar ayıklayın ve hello çözümü Visual Studio'da açın.

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a>Visual Studio 2013 ve Visual Studio 2015 kullanarak bir .NET arka ucu oluşturma
Merhaba yüklemek [.NET için Azure SDK] [ 4] (sürüm 2.9.0 veya sonrası) toocreate Visual Studio'da bir Azure Mobile Apps projesi. Merhaba SDK yükledikten sonra aşağıdaki adımları hello kullanarak bir ASP.NET uygulamasını oluşturun:

1. Açık hello **yeni proje** iletişim (gelen *dosya* > **yeni** > **proje...** ).
2. Genişletme **şablonları** > **Visual C#**seçip **Web**.
3. Seçin **ASP.NET Web uygulaması**.
4. Merhaba proje adı girin. Daha sonra, **Tamam**'a tıklayın.
5. Altında *ASP.NET 4.5.2 şablonları*seçin **Azure mobil uygulaması**. Denetleyin **hello buluttaki konağa** toocreate hello içinde mobil arka uç bulut toowhich bu proje yayımlayabilirsiniz.
6. **Tamam** düğmesine tıklayın.

## <a name="install-sdk"></a>Nasıl yapılır: karşıdan yükle ve hello SDK başlatma
Merhaba SDK kullanılabilir [NuGet.org]. Bu paket hello SDK kullanmaya hello gerekli temel işlevselliği tooget içerir. tooinitialize SDK Merhaba, hello tooperform eylemleri gereksinim **HttpConfiguration** nesnesi.

### <a name="install-hello-sdk"></a>Merhaba SDK yükleme
tooinstall hello SDK, Visual Studio'da hello sunucu projesi sağ tıklatın seçin **NuGet paketlerini Yönet**, hello Ara [Microsoft.Azure.Mobile.Server] paketini ve ardından  **Yükleme**.

### <a name="server-project-setup"></a>Merhaba sunucu projesi başlatma
OWIN başlangıç sınıfı dahil ederek başlatılmış benzer tooother ASP.NET projeleri, .NET arka uç sunucu projesi var. Merhaba NuGet paketi başvurulan olun `Microsoft.Owin.Host.SystemWeb`. tooadd Visual Studio'da bu sınıf sağ tıklayın, sunucu projesi ve select **Ekle** >
**yeni öğe**, ardından **Web**  >  ** Genel** > **OWIN başlangıç sınıfı**.  Bir sınıf özniteliği aşağıdaki hello ile oluşturulur:

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

Merhaba, `Configuration()` yöntemi, OWIN başlangıç sınıfı, kullanım, bir **HttpConfiguration** nesne tooconfigure hello Azure Mobile Apps ortamı.
Aşağıdaki örnek hello hello sunucu projesi hiçbir ek özellikler içeren başlatır:

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

tooenable tek tek özellikleri, üzerinde hello genişletme yöntemlerini çağırmalıdır **MobileAppConfiguration** nesne çağırmadan önce **ApplyTo**. Örneğin, kod aşağıdaki hello hello varsayılan yolları hello özniteliğine sahip tooall API denetleyicilerinin ekler `[MobileAppController]` başlatma sırasında:

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

Merhaba server hızlı başlangıçtan hello Azure portal çağrıları **UseDefaultConfiguration()**. Kurulum aşağıdaki bu eşdeğer toohello:

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

kullanılan hello uzantı yöntemleri şunlardır:

* `AddMobileAppHomeController()`Merhaba varsayılan Azure Mobile Apps giriş sayfası sağlar.
* `MapApiControllers()`Merhaba ile donatılmış Webapı denetleyicileri için özel API olanakları sağlayan `[MobileAppController]` özniteliği.
* `AddTables()`Merhaba eşlenmesini sağlar `/tables` uç noktaları tootable denetleyicileri.
* `AddTablesWithEntityFramework()`bir kısaltılmış eşleme hello için olan `/tables` Entity Framework kullanarak uç noktaları alarak denetleyicileri.
* `AddPushNotifications()`Bildirim hub'ları için cihazları kaydetme, basit bir yöntem sağlar.
* `MapLegacyCrossDomainController()`Standart CORS üstbilgilerini yerel geliştirme için sağlar.

### <a name="sdk-extensions"></a>SDK uzantıları
NuGet tabanlı uzantı paketleri aşağıdaki hello uygulamanız tarafından kullanılan çeşitli mobil özellikleri sağlar. Hello kullanarak başlatma sırasında uzantılarını etkinleştirme **MobileAppConfiguration** nesnesi.

* [Microsoft.Azure.Mobile.Server.Quickstart] destekler hello temel Mobile Apps kurulumu. Arama hello tarafından eklenen toohello yapılandırma **UseDefaultConfiguration** başlatma sırasında genişletme yöntemi. Bu uzantı uzantıları aşağıdaki içerir: bildirimleri, kimlik doğrulama, varlık, tablolar, etki alanları arası ve giriş paketleri. Bu paket, hello Mobile Apps hızlı başlangıç hello Azure portalı üzerinde kullanılabilir tarafından kullanılır.
* [Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) uygulayan hello varsayılan *bu mobil uygulamayı çalışır durumda olduğundan sayfa* hello web sitesinin kök. Çağırarak toohello yapılandırması eklemek **AddMobileAppHomeController** genişletme yöntemi.
* [Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) veriler ve ayarlar yukarı hello veri ardışık ile çalışmaya yönelik sınıflar içerir. Toohello yapılandırması tarafından arama hello eklemek **AddTables** genişletme yöntemi.
* [Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) hello Entity Framework tooaccess verileri hello SQL veritabanı sağlar. Toohello yapılandırması tarafından arama hello eklemek **AddTablesWithEntityFramework** genişletme yöntemi.
* [Microsoft.Azure.Mobile.Server.Authentication] etkinleştirir kimlik doğrulama ve ayarlar yukarı hello OWIN ara yazılımı toovalidate belirteçleri kullanılır. Toohello yapılandırması tarafından arama hello eklemek **AddAppServiceAuthentication** ve **Iappbuilder**. **UseAppServiceAuthentication** genişletme yöntemleri.
* [Microsoft.Azure.Mobile.Server.Notifications] anında iletme bildirimleri ve anında iletme kayıt uç noktasını tanımlar sağlar. Toohello yapılandırması tarafından arama hello eklemek **AddPushNotifications** genişletme yöntemi.
* [Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) veri toolegacy mobil uygulamanızın web tarayıcılarından hizmet veren bir denetleyiciyi oluşturur. Çağırarak toohello yapılandırması eklemek **MapLegacyCrossDomainController** genişletme yöntemi.
* [Microsoft.Azure.Mobile.Server.Login] özel kimlik doğrulama senaryoları sırasında kullanılan bir statik yöntem hello AppServiceLoginHandler.CreateToken() yöntemi sağlar.

## <a name="publish-server-project"></a>Nasıl yapılır: yayımlama hello sunucu projesi
Bu bölümde, nasıl toopublish .NET arka ucu proje Visual Studio'dan gösterir. Arka uç projeniz Git kullanarak da dağıtabilir veya herhangi bir hello hello kapsamdaki diğer yöntemleri [Azure uygulama hizmeti dağıtım belgeleri](../app-service-web/web-sites-deploy.md).

1. Visual Studio'da hello proje toorestore NuGet paketlerini yeniden oluşturun.
2. Çözüm Gezgini'nde, sağ hello proje tıklatın **Yayımla**. Merhaba, yayımladığınız ilk kez, toodefine bir yayımlama profili gerekir. Önceden tanımlı bir profili varsa, seçin ve tıklatın **Yayımla**.
3. Tooselect yayımlama hedefi sorulursa tıklatın **Microsoft Azure App Service** > **sonraki**, sonra (gerekirse) ile Azure kimlik bilgilerinizle oturum açın.
   Visual Studio indirmeleri ve güvenli bir şekilde depolar, doğrudan Azure ayarlarını yayımlayın.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. Seçin, **abonelik**seçin **kaynak türü** gelen **Görünüm**, genişletin **mobil uygulama**ve mobil uygulama arka tıklayın ve ardından **Tamam**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. Merhaba doğrulayın profil bilgilerini yayımlamak ve tıklatın **Yayımla**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    Mobil uygulama arka başarıyla yayımladı, başarıyı gösteren bir giriş sayfasına bakın.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <a name="define-table-controller"></a>Nasıl yapılır: bir tablo denetleyicisi tanımlayın
Bir tablo denetleyicisi tooexpose SQL tablosu toomobile istemcileri tanımlayın.  Bir tablo denetleyicisi yapılandırma üç adımı gerektirir:

1. Bir veri aktarım nesnesini (DTO) sınıf oluşturun.
2. Bir tablo başvurusu hello mobil DbContext sınıfı yapılandırın.
3. Bir tablo denetleyicisi oluşturun.

Bir veri aktarım nesnesini (DTO) öğesinden devralınan bir düz C# nesnesidir `EntityData`.  Örneğin:

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

Merhaba DTO hello SQL veritabanı içinde kullanılan toodefine hello tablosu değil.  toocreate hello veritabanı girişi, ekleme bir `DbSet<>` hello kullanmakta olduğunuz DbContext özelliğine.  Merhaba varsayılan proje şablonu Azure mobil uygulamalar için hello DbContext çağrılır `Models\MobileServiceContext.cs`:

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

Azure SDK'sı yüklü hello varsa, aşağıdaki gibi bir şablon tablo denetleyicisi artık oluşturabilirsiniz:

1. Merhaba denetleyicileri klasörü sağ tıklatın ve seçin **Ekle** > **denetleyicisi...** .
2. Select hello **Azure Mobile Apps tablo denetleyicisi** seçeneğini ve ardından **Ekle**.
3. Merhaba, **denetleyici Ekle** iletişim:
   * Merhaba, **Model sınıfı** açılan listesinde, yeni DTO seçin.
   * Merhaba, **DbContext** açılan listesinde, select hello mobil hizmet DbContext sınıfı.
   * Merhaba Denetleyici adı sizin için oluşturulur.
4. **Ekle**'ye tıklayın.

Hello hızlı başlangıç sunucu projesi içeren basit bir örneğin **TodoItemController**.

### <a name="adjust-pagesize"></a>Nasıl yapılır: hello tablo disk belleği boyutunu ayarlama
Varsayılan olarak, Azure Mobile Apps istek başına 50 kayıt döndürür.  Disk belleği hello istemci kendi kullanıcı Arabirimi iş parçacığı veya hello sunucusu çok uzun bir süre için iyi bir kullanıcı deneyimi sağlayarak tie değil sağlar. toochange hello tablo disk belleği boyutu artışı hello sunucu tarafı "izin verilen sorgu boyutu" ve hello istemci-tarafı sayfa boyutu hello sunucu tarafı "izin verilen sorgu boyutu" Merhaba kullanarak ayarlanır `EnableQuery` özniteliği:

    [EnableQuery(PageSize = 500)]

Merhaba PageSize hello aynı ya da hello istemci tarafından istenilen hello boyutundan büyük olduğundan emin olun.  Merhaba istemci sayfa boyutunu değiştirme hakkında ayrıntılar için toohello belirli istemci nasıl yapılır belgelerine başvurun.

## <a name="how-to-define-a-custom-api-controller"></a>Nasıl yapılır: özel bir API denetleyicisi tanımlayın
Merhaba özel API denetleyicisi hello en temel işlevleri tooyour mobil uygulama arka uç nokta göstererek sağlar. Merhaba [MobileAppController] özniteliği kullanılarak mobile özgü API denetleyicisi kaydedebilirsiniz. Merhaba `MobileAppController` özniteliği hello rota kaydeder, hello Mobile Apps JSON serileştirici ayarlar ve açar [istemci sürüm denetimi](app-service-mobile-client-and-server-versioning.md).

1. Visual Studio'da hello denetleyicileri klasörü sağ tıklatın, ardından **Ekle** > **denetleyicisi**seçin **Web API 2 denetleyicisi&mdash;boş** ve tıklatın **Ekle**.
2. Tedarik bir **Denetleyici adı**, gibi `CustomController`, tıklatıp **Ekle**.
3. Merhaba yeni denetleyici sınıfı dosyasında hello aşağıdakileri ekleyin deyimi kullanarak:

        using Microsoft.Azure.Mobile.Server.Config;
4. Merhaba uygulamak **[MobileAppController]** özniteliği aşağıdaki örneğine hello olduğu gibi toohello API denetleyicisi sınıfı tanımı:

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. Çağrı toohello App_Start/Startup.MobileApp.cs dosyasında ekleyin **MapApiControllers** uzantısı yönteminizdeki aşağıdaki örneğine hello:

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

Merhaba de kullanabilirsiniz `UseDefaultConfiguration()` genişletme yöntemi yerine `MapApiControllers()`. Sahip olmadığı herhangi bir denetleyicisi **MobileAppControllerAttribute** uygulanan hala istemcileri tarafından erişilebilen, ancak bunu doğru şekilde herhangi bir mobil uygulama istemci SDK kullanan istemciler tarafından tüketilmeyen.

## <a name="how-to-work-with-authentication"></a>Nasıl yapılır: kimlik doğrulaması ile çalışma
Azure Mobile Apps kullanan App Service kimlik doğrulama / yetkilendirme toosecure mobil arka.  Bu bölümde, nasıl gösterilir .NET arka uç sunucu projenizi kimlik doğrulaması ile ilgili görevleri aşağıdaki tooperform hello:

* [Nasıl yapılır: kimlik doğrulaması tooa sunucu projesi ekleme](#add-auth)
* [Nasıl yapılır: uygulamanız için özel kimlik doğrulamasını kullan](#custom-auth)
* [Nasıl yapılır: alma kimliği doğrulanmış kullanıcı bilgileri](#user-info)
* [Nasıl yapılır: yetkili kullanıcıların veri erişimini kısıtlamak](#authorize)

### <a name="add-auth"></a>Nasıl yapılır: kimlik doğrulaması tooa sunucu projesi ekleme
Kimlik doğrulama tooyour sunucu projesi hello genişleterek ekleyebileceğiniz **MobileAppConfiguration** nesne ve OWIN ara yazılımı yapılandırma. Merhaba yüklediğinizde [Microsoft.Azure.Mobile.Server.Quickstart] paket ve çağrı hello **UseDefaultConfiguration** genişletme yöntemi, toostep 3 atlayabilirsiniz.

1. Visual Studio'da hello yüklemek [Microsoft.Azure.Mobile.Server.Authentication] paket.
2. Aşağıdaki kod hello hello başında hello Hello haline proje dosyasında eklemek **yapılandırma** yöntemi:

        app.UseAppServiceAuthentication(config);

    Bu OWIN ara yazılım bileşeni ilişkili hello uygulama hizmeti gateway tarafından yayınlanan belirteçleri doğrular.
3. Merhaba eklemek `[Authorize]` özniteliği tooany denetleyicisi veya kimlik doğrulama gerektiren yöntemi.

toolearn konusunda tooauthenticate istemcileri tooyour Mobile Apps arka bkz [Ekle kimlik doğrulama tooyour uygulama](app-service-mobile-ios-get-started-users.md).

### <a name="custom-auth"></a>Nasıl yapılır: uygulamanız için özel kimlik doğrulamasını kullan
Toouse hello App Service kimlik doğrulama/yetkilendirme sağlayıcılardan biri istemiyorsanız, kendi oturum açma sistem uygulayabilirsiniz. Merhaba yüklemek [Microsoft.Azure.Mobile.Server.Login] tooassist kimlik doğrulama belirteci oluşturma ile paket.  Kullanıcı kimlik bilgilerini doğrulamak için kendi kodunuzu girin. Örneğin, güvenlik ve karma parolaları bir veritabanında karşı denetleyebilirsiniz. Merhaba aşağıdaki örnekte, hello `isValidAssertion()` yöntemi (başka bir yerde tanımlanır) için bu denetimleri sorumlu.

bir ApiController oluşturma ve gösterme Hello özel kimlik doğrulama açığa `register` ve `login` eylemler. Merhaba istemci hello kullanıcıdan özel kullanıcı Arabirimi toocollect hello bilgilerini kullanmanız gerekir.  Standart bir HTTP POST ile birlikte gönderilen toohello API çağrısı sonra hello bilgilerdir. Merhaba onaylama Hello sunucuyu doğrular sonra bir belirteç hello kullanarak verilen `AppServiceLoginHandler.CreateToken()` yöntemi.  Merhaba ApiController **vermemelisiniz** hello kullan `[MobileAppController]` özniteliği.

Örnek `login` eylem:

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

Örnek önceki hello LoginResult ve LoginResultUser gerekli özellikleri gösterme seri hale getirilebilir nesneleridir. Merhaba istemci oturum açma yanıtları toobe hello form JSON nesneler olarak döndürülen bekler:

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

Merhaba `AppServiceLoginHandler.CreateToken()` yöntemi içeren bir *İzleyici* ve bir *veren* parametresi. Bu parametrelerin her ikisini de toohello URL'sini hello HTTPS şeması kullanarak, uygulamanızın kök ayarlanır. Benzer şekilde ayarlamalısınız *secretKey* toobe hello değeri, uygulamanızın imzalama anahtarı. Bir istemci anahtarı olarak kullanılan toomint anahtarlarının olması ve kullanıcıların kimliğine imzalama hello dağıtmayın. Merhaba başvurarak App Service içinde barındırılan tutarak imzalama hello edinebilirsiniz *Web sitesi\_AUTH\_imzalama\_anahtar* ortam değişkeni. Yerel hata ayıklama bağlamda gerekirse hello hello yönergeleri izleyin [yerel kimlik doğrulaması ile hata ayıklama](#local-debug) bölümünde tooretrieve hello anahtarı ve bir uygulama ayarı olarak depolar.

verilen hello belirteci ayrıca diğer talepleri ve sona erme tarihi içerebilir.  En düşük düzeyde, verilen hello belirteci bir konu içermelidir (**alt**) talep.

Merhaba standart istemci destekleyebilir `loginAsync()` hello kimlik doğrulaması rota aşırı yüklemesi tarafından yöntemi.  Merhaba istemci çağırırsa `client.loginAsync('custom');` toolog içinde rota olmalıdır `/.auth/login/custom`.  Merhaba denetleyicisi özel kimlik doğrulama kullanarak hello yol ayarlayabilirsiniz `MapHttpRoute()`:

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> Hello kullanarak `loginAsync()` yaklaşım sağlar hello kimlik doğrulama belirtecini bağlı tooevery sonraki çağrı toohello hizmet.
>
>

### <a name="user-info"></a>Nasıl yapılır: alma kimliği doğrulanmış kullanıcı bilgileri
Bir kullanıcı tarafından uygulama hizmeti doğrulandığında, kullanıcı kimliği ve diğer bilgileri .NET arka uç kodunuzun atanan hello erişebilir. Merhaba kullanıcı bilgilerini hello arka yetkilendirme kararları kullanılabilir. Merhaba aşağıdaki kod bir istekle ilişkili hello kullanıcı Kimliğini alır:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

Merhaba SID hello sağlayıcıya özgü kullanıcı ID'den türetilmiş ve verilen kullanıcı ve oturum açma sağlayıcısı için statiktir.  Merhaba SID için geçersiz kimlik doğrulama belirteçleri null şeklindedir.

Uygulama Hizmeti ayrıca oturum açma sağlayıcınızdan belirli talep istemenize olanak tanır. Her bir kimlik sağlayıcısı kimlik sağlayıcısı SDK kullanarak daha fazla bilgi sağlayabilir.  Örneğin, arkadaş bilgilerini hello Facebook grafik API'sini kullanabilirsiniz.  İstenen taleplerin hello sağlayıcısı dikey penceresinde hello Azure portal belirtebilirsiniz. Bazı talep hello kimlik sağlayıcısı ile ek yapılandırma gerektirir.

Merhaba aşağıdaki kod çağrıları hello **GetAppServiceIdentityAsync** hello erişim belirteci gerekli toomake hello Facebook grafik API'si istekler dahil uzantısı yöntemi tooget hello oturum açma kimlik bilgileri:

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

Kullanarak bir ekleme deyimi için `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** genişletme yöntemi.

### <a name="authorize"></a>Nasıl yapılır: yetkili kullanıcıların veri erişimini kısıtlamak
Merhaba önceki bölümde nasıl tooretrieve hello kimliği doğrulanmış bir kullanıcı kullanıcı Kimliğini gösterdi. Erişim toodata ve diğer kaynaklar bu değere göre kısıtlayabilirsiniz. Örneğin, bir kullanıcı kimliği sütunu tootables ekleme ve hello sorgu sonuçları hello kullanıcı Kimliğine göre filtreleme verileri yalnızca tooauthorized kullanıcılar döndürülen basit yol toolimit olur. yalnızca hello SID hello Todoıtem tablosu üzerinde hello UserID sütunundaki değeri eşleştiğinde hello aşağıdaki kod veri satırlarını döndürür:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

Merhaba `Query()` yöntemi döndürür bir `IQueryable` , yönetilebilir toohandle LINQ filtreleyerek.

## <a name="how-to-add-push-notifications-tooa-server-project"></a>Nasıl yapılır: anında iletme bildirimleri tooa sunucu projesi ekleme
Merhaba genişleterek anında iletme bildirimleri tooyour sunucu projesi eklemek **MobileAppConfiguration** nesne ve bildirim hub'ları istemci oluşturma.

1. Visual Studio'da hello sunucu projesi sağ tıklatın ve **NuGet paketlerini Yönet**, arama `Microsoft.Azure.Mobile.Server.Notifications`, ardından **yükleme**.
2. Bu adım tooinstall hello yineleyin `Microsoft.Azure.NotificationHubs` hello bildirim hub'ları istemci kitaplığı içeren paket.
3. App_Start/Startup.MobileApp.cs içinde arama toohello ekleyin **AddPushNotifications()** genişletme yöntemi başlatma sırasında:

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. Bildirim hub'ları istemci oluşturur koddan hello ekleyin:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

Merhaba bildirim hub'ları istemci toosend anında iletme bildirimleri tooregistered cihazlar artık kullanabilirsiniz. Daha fazla bilgi için bkz: [Ekle anında iletme bildirimleri tooyour uygulama](app-service-mobile-ios-get-started-push.md). Bildirim hub'ları hakkında daha fazla toolearn bkz [Notification Hubs'a genel bakış](../notification-hubs/notification-hubs-push-notification-overview.md).

## <a name="tags"></a>Nasıl yapılır: etkinleştir hedeflenen etiketleri kullanarak anında iletme
Bildirim hub'ları etiketleri kullanarak toospecific kayıtlar hedeflenen bildirimleri göndermenize olanak sağlar. Birkaç etiket otomatik olarak oluşturulur:

* belirli bir aygıt Hello yükleme kimliği tanımlar.
* Merhaba kullanıcı kimliği temel kimlik doğrulaması hello üzerinde SID belirli bir kullanıcı tanımlar.

Merhaba hello kimliği erişilebilir yükleme **InstallationID** hello özellikte **MobileServiceClient**.  Hello aşağıdaki örnekte bir yükleme kimliği tooadd nasıl kullanılacağını etiket tooa belirli yükleme bildirim hub'ları gösterir:

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

Anında iletme bildirimi kaydı sırasında Hello istemci tarafından sağlanan herhangi bir etiket hello arka ucu tarafından hello yükleme oluştururken göz ardı edilir. toohello yükleme tooenable istemci tooadd etiketleri, düzeni önceki hello kullanarak etiketleri ekler özel bir API oluşturmanız gerekir.

Bkz: [istemci eklenen anında iletme bildirimi etiketleri] [ 5] hello App Service Mobile Apps tamamlanmış hızlı başlangıç örnek bir örnek.

## <a name="push-user"></a>Nasıl yapılır: gönderme anında iletme bildirimleri tooan kimliği doğrulanmış kullanıcı
Kimliği doğrulanmış bir kullanıcı için anında iletme bildirimleri kaydolduğunda, bir kullanıcı kimliği etiketi toohello kayıt otomatik olarak eklenir. Bu etiketi kullanarak anında iletme bildirimleri tooall cihazlar söz konusu kişi tarafından kayıtlı gönderebilirsiniz. Merhaba aşağıdaki kod hello isteği yapan kullanıcı SID'si alır ve bu kişi için bir şablon anında iletme bildirimi tooevery aygıt kaydı gönderir:

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

Kimliği doğrulanmış bir istemci anında iletme bildirimleri için kaydolurken kayıt denemeden önce kimlik doğrulamasının tam olduğundan emin olun. Daha fazla bilgi için bkz: [anında toousers] [ 6] hello App Service Mobile Apps tamamlanmış hızlı başlangıç örnek .NET arka ucu için.

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a>Nasıl yapılır: hata ayıklama ve sorun giderme hello .NET sunucusu SDK
Azure uygulama hizmeti birkaç hata ayıklama ve sorun giderme teknikleri ASP.NET uygulamaları için sağlar:

* [Bir Azure uygulama hizmeti izleme](../app-service-web/web-sites-monitor.md)
* [Azure uygulama hizmetinde tanılama günlük kaydını etkinleştir](../app-service-web/web-sites-enable-diagnostic-log.md)
* [Visual Studio'da bir Azure uygulama hizmeti sorunlarını giderme](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a>Günlüğe kaydetme
Merhaba standart ASP.NET izleme yazma kullanarak hizmet tanılama günlükleri tooApp yazabilirsiniz. Toohello günlükleri yazmadan önce mobil uygulama arka ucunuzu tanılama etkinleştirmeniz gerekir.

tooenable tanılama ve yazma toohello günlükleri:

1. Merhaba adımları [nasıl tooenable tanılama](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).
2. Merhaba aşağıdakileri ekleyin, kod dosyanızda deyimiyle:

        using System.Web.Http.Tracing;
3. İzleme yazıcısı toowrite hello .NET arka uç toohello tanılama günlükleri, aşağıdaki gibi oluşturun:

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. Sunucu projenizi yeniden yayımlamanız ve hello mobil uygulama arka uç tooexecute hello kod yolu hello günlük ile erişim.
5. Karşıdan yükle ve açıklandığı gibi hello günlükleri, değerlendirme [nasıl yapılır: indirme günlükleri](../app-service-web/web-sites-enable-diagnostic-log.md#download).

### <a name="local-debug"></a>Yerel kimlik doğrulaması ile hata ayıklama
Uygulamanızı çalıştırabilirsiniz tootest yerel olarak değiştirir toohello bulut yayımlamadan önce. Çoğu Azure Mobile Apps arka uçlarını için basın *F5* while Visual Studio'da. Ancak, kimlik doğrulaması kullanılırken ek bazı noktalar vardır.

Bir bulut tabanlı mobil uygulama ile App Service kimlik doğrulama/yapılandırılmış yetkilendirme olmalıdır ve istemci hello alternatif oturum açma konağı olarak belirtilen hello bulut uç noktası olmalıdır. İstemci platformunuzu gerekli hello belirli adımlar için Hello belgelerine bakın.

Mobil arka sahip olduğundan emin olun [Microsoft.Azure.Mobile.Server.Authentication] yüklü. Ardından, sonra hello aşağıdaki uygulamanızın OWIN başlangıç sınıfı ekleyin `MobileAppConfiguration` uygulanan tooyour bırakıldı `HttpConfiguration`:

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

Örnek önceki hello hello yapılandırmalısınız *authAudience* ve *authIssuer* olması hello HTTPS kullanarak, uygulamanızın kök URL'si tooeach dosya Web.config içindeki uygulama ayarları düzeni. Benzer şekilde ayarlamalısınız *authSigningKey* toobe hello değeri, uygulamanızın imzalama anahtarı.
tooobtain hello imzalama anahtarı:

1. Merhaba içinde tooyour uygulamasına gidin [Azure portalı]
2. Tıklatın **Araçları**, **Kudu**, **Git**.
3. Merhaba Kudu Yönetim sitesini'ı tıklatın **ortam**.
4. Merhaba değeri Bul *Web sitesi\_AUTH\_imzalama\_anahtar*.

İmzalama anahtarı hello için kullanım hello *authSigningKey* , yerel uygulama yapılandırma parametresi.  Mobil arka hangi hello istemci hello belirteci hello bulut tabanlı uç noktasından alacağı yerel olarak çalıştırırken donanımlı toovalidate belirteçleri sunulmuştur.

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[Azure portalı]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
