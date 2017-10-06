---
title: "Azure SQL veritabanı ile ASP.NET uygulamasında aaaBuild | Microsoft Docs"
description: "Bilgi nasıl tooget bir ASP.NET bağlantı tooa SQL veritabanı ile Azure üzerinde çalışan uygulama."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a>Azure SQL veritabanı ile bir ASP.NET uygulaması oluşturma

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar. Bu öğretici nasıl toodeploy veri güdümlü bir ASP.NET web uygulamasına ve çok bağlanacağını gösterir[Azure SQL veritabanı](../sql-database/sql-database-technical-overview.md). İşiniz bittiğinde, çalışır durumda bir ASP.NET uygulamanız [Azure App Service](../app-service/app-service-value-prop-what-is.md) ve tooSQL veritabanına bağlı.

![Azure web uygulamasında yayımlanan ASP.NET uygulaması](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Azure SQL veritabanı oluşturma
> * Bir ASP.NET uygulaması tooSQL veritabanına bağlan
> * Merhaba uygulama tooAzure dağıtma
> * Merhaba veri modeli güncelleştirmek ve hello uygulama yeniden dağıtın
> * Azure tooyour terminal akış günlükleri
> * Merhaba uygulamada hello Azure portalı Yönet

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici:

* Yükleme [Visual Studio 2017](https://www.visualstudio.com/downloads/) iş yükleri aşağıdaki hello ile:
  - **ASP.NET ve web geliştirme**
  - **Azure geliştirme**

  ![ASP.NET ve web geliştirme ile Azure geliştirme (Web ve Bulut altında)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Merhaba örnek indirme

[Merhaba örnek projesini indirin](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).

Extract (sıkıştırmasını açın) hello *dotnet-sqldb-öğretici-master.zip* dosya.

Merhaba örnek projesini içeren temel bir [ASP.NET MVC](https://www.asp.net/mvc) CRUD (Oluştur-okunur-güncelleştirme-Sil) uygulamasını kullanarak [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="run-hello-app"></a>Merhaba uygulamayı çalıştırma

Açık hello *dotnet-sqldb-öğretici-ana/DotNetAppSqlDb.sln* dosyasını Visual Studio'da. 

Tür `Ctrl+F5` hata ayıklama olmadan toorun hello uygulama. Merhaba uygulama varsayılan tarayıcınızda görüntülenir. Select hello **Yeni Oluştur** bağlayın ve birkaç oluşturun *Yapılacaklar* öğeleri. 

![Yeni ASP.NET Projesi iletişim kutusu](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

Test hello **Düzenle**, **ayrıntıları**, ve **silmek** bağlantılar.

Merhaba uygulama bir veritabanı bağlamını tooconnect hello veritabanıyla kullanır. Bu örnekte, hello veritabanı bağlamını adlı bir bağlantı dizesi kullanır `MyDbConnection`. Merhaba bağlantı dizesi hello ayarlanmış *Web.config* dosya ve başvurulan hello *Models/MyDatabaseContext.cs* dosya. Merhaba bağlantı dizesi adı daha sonra hello öğretici tooconnect hello Azure web uygulaması tooan Azure SQL veritabanı kullanılır. 

## <a name="publish-tooazure-with-sql-database"></a>SQL veritabanı ile tooAzure yayımlama

Merhaba, **Çözüm Gezgini**, sağ tıklatın, **DotNetAppSqlDb** proje ve seçin **Yayımla**.

![Çözüm Gezgini'nden yayımlama](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

**Microsoft Azure App Service**’in seçili olduğundan emin olup **Yayımla**’ya tıklayın.

![Projeye genel bakış sayfasından yayımlama](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

Yayımlama hello açılır **App Service Oluştur** iletişim kutusunda, oluşturduğunuz tüm yardımcı olan hello Azure kaynaklarını azure'da ASP.NET web uygulamanız toorun gerekir.

### <a name="sign-in-tooazure"></a>İçinde tooAzure oturum

Merhaba, **App Service Oluştur** iletişim kutusunda, tıklatın **Hesap Ekle**ve tooyour Azure aboneliği oturum açın. Bir Microsoft hesabında zaten oturum açtıysanız hesabın Azure aboneliğinizi barındırdığından emin olun. Microsoft hesabı oturum açmış Hello Azure aboneliğiniz yoksa, tooadd hello doğru hesabını tıklatın.
   
![İçinde tooAzure oturum](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

Oturum açıldıktan sonra tüm Azure web uygulamanız bu iletişim için gereken kaynakları hello hazır toocreate demektir.

### <a name="configure-hello-web-app-name"></a>Merhaba web uygulaması adını yapılandırma

Oluşturulan başlangıç web uygulaması adı tutun veya tooanother benzersiz adını değiştirin (geçerli karakterler `a-z`, `0-9`, ve `-`). Merhaba web uygulaması adı, uygulamanız için hello varsayılan URL bir parçası olarak kullanılır (`<app_name>.azurewebsites.net`, burada `<app_name>` web uygulaması adınız). Merhaba web uygulaması adı toobe benzersiz azure'da tüm uygulamalarında gerekir. 

![App service Oluştur iletişim kutusu](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Sonraki çok**kaynak grubu**, tıklatın **yeni**.

![Sonraki tooResource grubu, yeni tıklayın.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

Ad hello kaynak grubu **myResourceGroup**.

> [!NOTE]
> ' A tıklamayın **oluşturma**. Önce bir SQL veritabanını sonraki adımda tooset gerekir.

### <a name="create-an-app-service-plan"></a>App Service planı oluşturma

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Sonraki çok**App Service planı**, tıklatın **yeni**. 

Merhaba, **uygulama hizmeti planı yapılandırmak** iletişim kutusunda, ayarları aşağıdaki hello ile Merhaba yeni uygulama hizmeti planını yapılandır:

![App Service planı oluşturma](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| Ayar  | Önerilen değer | Daha fazla bilgi için |
| ----------------- | ------------ | ----|
|**Uygulama hizmeti planı**| myAppServicePlan | [App Service planları](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|**Konum**| Batı Avrupa | [Azure bölgeleri](https://azure.microsoft.com/regions/) |
|**Boyut**| Ücretsiz | [Fiyatlandırma katmanları](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a>SQL Server örneği oluşturma

Bir veritabanı oluşturmadan önce gereken bir [Azure SQL Database mantıksal sunucusu](../sql-database/sql-database-features.md). Mantıksal sunucu, grup olarak yönetilen bir veritabanı grubu içerir.

Seçin **diğer Azure hizmetlerini keşfedin**.

![Web uygulaması adını yapılandırma](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

Merhaba, **Hizmetleri** sekmesini ve ardından hello  **+**  simgesi sonraki çok**SQL veritabanı**. 

![Merhaba Hizmetleri, sekmesini Merhaba + simgesi sonraki tooSQL veritabanı.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

Merhaba, **SQL veritabanını yapılandırma** iletişim kutusunda, tıklatın **yeni** sonraki çok**SQL Server**. 

Benzersiz sunucu adı oluşturulur. Bu ad hello varsayılan URL bir parçası olarak mantıksal sunucunuz için kullanılan `<server_name>.database.windows.net`. Bunu Azure tüm mantıksal sunucu örnekleri arasında benzersiz olması gerekir. Merhaba sunucu adını değiştirmek, ancak bu öğretici için oluşturulan hello değeri tutun.

Bir yönetici kullanıcı adı ve parolayı ekleyin ve ardından **Tamam**. Parola karmaşıklık gereksinimleri için bkz: [parola ilkesi](/sql/relational-databases/security/password-policy).

Bu kullanıcı adı ve parola unutmayın. Toomanage hello mantıksal sunucusuna gerek daha sonra örneği.

![SQL Server örneği oluşturma](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a>SQL Veritabanı oluşturma

Merhaba, **SQL veritabanını yapılandırma** iletişim: 

* Merhaba varsayılan olarak oluşturulan tutmak **veritabanı adı**.
* İçinde **bağlantı dizesi adı**, türü *MyDbConnection*. Bu ad başvuru hello bağlantı dizesi eşleşmelidir *Models/MyDatabaseContext.cs*.
* **Tamam**’ı seçin.

![SQL veritabanını Yapılandır](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

Merhaba **App Service Oluştur** iletişim oluşturduğunuz hello kaynakları gösterir. **Oluştur**'a tıklayın. 

![oluşturduğunuz hello kaynakları](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

Hello Azure kaynakları oluşturma Hello Sihirbazı tamamlandıktan sonra ASP.NET uygulama tooAzure yayımlar. Varsayılan tarayıcı hello URL dağıtılan toohello uygulamayla başlatılır. 

Birkaç Yapılacaklar öğelerini ekleyin.

![Azure web uygulamasında yayımlanan ASP.NET uygulaması](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

Tebrikler! Veri tabanlı ASP.NET uygulamanızı Azure App Service'te çalışıyor.

## <a name="access-hello-sql-database-locally"></a>Yerel olarak erişim hello SQL veritabanı

Visual Studio keşfedin ve yönetmenize olanak sağlar, yeni SQL veritabanınızı kolayca hello **SQL Server Nesne Gezgini**.

### <a name="create-a-database-connection"></a>Bir veritabanı bağlantısı oluşturma

Merhaba gelen **Görünüm** menüsünde, select **SQL Server Nesne Gezgini**.

Merhaba üst kısmındaki **SQL Server Nesne Gezgini**, hello tıklatın **SQL Server Ekle** düğmesi.

### <a name="configure-hello-database-connection"></a>Merhaba veritabanı bağlantısını yapılandır

Merhaba, **Bağlan** iletişim kutusunda, hello genişletin **Azure** düğümü. Tüm SQL veritabanı örnekleri Azure burada listelenir.

Select hello `DotNetAppSqlDb` SQL veritabanı. daha önce oluşturduğunuz hello bağlantı hello altındaki otomatik olarak doldurulur.

Daha önce oluşturduğunuz hello veritabanı yönetici parolasını yazıp tıklatın **Bağlan**.

![Visual Studio'dan veritabanı bağlantısını yapılandır](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a>İstemci bağlantısı bilgisayarınızdan izin ver

Merhaba **yeni bir güvenlik duvarı kuralı oluşturmak** iletişim kutusu açılır. Varsayılan olarak, SQL veritabanı örneğinde bağlantılar Azure web uygulamanızın gibi Azure hizmetlerinden yalnızca izin verir. tooconnect tooyour veritabanı, hello SQL veritabanı örneğinde bir güvenlik duvarı kuralı oluşturun. Merhaba güvenlik duvarı kuralı hello genel IP adresi, yerel bilgisayarınızın sağlar.

Merhaba iletişim zaten bilgisayarınızın ortak IP adresi ile doldurulur.

Olduğundan emin olun **my istemci IP'si Ekle** seçilir ve tıklatın **Tamam**. 

![SQL veritabanı örneği için güvenlik duvarını ayarlama](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

Visual Studio, SQL veritabanı örneğinizin hello güvenlik duvarı ayarı oluşturma tamamlandığında, bağlantınızı görünür **SQL Server Nesne Gezgini**.

Burada, gerçekleştirebileceğiniz hello en yaygın veritabanı gibi işlemleri çalıştırma sorguları, görünümler ve saklı yordamları ve daha fazla oluşturun. 

Merhaba üzerinde sağ `Todoes` tablo ve seçin **görünüm verilerini**. 

![SQL veritabanı nesneleri keşfedin](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a>Code First geçişleri uygulamayı güncelleştirme

Veritabanı ve web uygulamanızı Azure'da hello tanıdık araçlar Visual Studio tooupdate de kullanabilirsiniz. Bu adımda, Entity Framework toomake bir değişiklik tooyour veritabanı şeması Code First geçişleri kullanın ve tooAzure yayımlayın.

Entity Framework Code First Migrations kullanma hakkında daha fazla bilgi için bkz: [Entity Framework 6 kod MVC 5 kullanarak ilk ile çalışmaya başlama](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="update-your-data-model"></a>Veri modelinizi güncelleştir

Açık _Models\Todo.cs_ hello Kod düzenleyicisinde. Özellik toohello aşağıdaki hello eklemek `ToDo` sınıfı:

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a>Code First Migrations yerel olarak çalıştırma

Birkaç komutları toomake güncelleştirmeleri tooyour yerel veritabanı çalıştırın. 

Merhaba gelen **Araçları** menüsünde tıklatın **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**.

Hello Paket Yöneticisi konsolu penceresinde, Code First geçişleri etkinleştir:

```PowerShell
Enable-Migrations
```

Bir geçiş ekleyin:

```PowerShell
Add-Migration AddProperty
```

Merhaba yerel veritabanı güncelleştirin:

```PowerShell
Update-Database
```

Tür `Ctrl+F5` toorun hello uygulama. Test Merhaba, ayrıntıları düzenlemek ve bağlantıları oluşturun.

Merhaba uygulaması hatasız yüklerse, Code First Migrations başarılı oldu. Ancak, uygulama mantığınızın bu yeni özellik henüz kullanmadığından, sayfa hala görünüyor aynı hello. 

### <a name="use-hello-new-property"></a>Merhaba yeni özelliğini kullanın

Kod toouse hello bazı değişiklikler yapmak `Done` özelliği. Bu öğreticide kolaylık sağlamak için yalnızca toochange hello oluşturacağız `Index` ve `Create` toosee hello özellik eylemi görüntüler.

Açık _Controllers\TodosController.cs_.

Hello bulur `Create()` yöntemi ekleyin `Done` hello özelliklerinde toohello listesi `Bind` özniteliği. İşiniz bittiğinde, `Create()` yöntemi imza hello kod aşağıdaki gibi görünür:

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

Açık _Views\Todos\Create.cshtml_.

Hello Razor kodunun, görmelisiniz bir `<div class="form-group">` kullanan öğesi `model.Description`ve ardından başka bir `<div class="form-group">` kullanan öğesi `model.CreatedDate`. Bu iki öğenin hemen ardından, eklemek başka `<div class="form-group">` kullanan öğesi `model.Done`:

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

Açık _Views\Todos\Index.cshtml_.

Merhaba boş Ara `<th></th>` öğesi. Bu öğe yalnızca Razor kod aşağıdaki hello ekleyin:

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

Hello bulur `<td>` hello içeren öğeyi `Html.ActionLink()` yardımcı yöntemler. Bu öğe yalnızca Razor kod aşağıdaki hello ekleyin:

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

Tüm yapmanız gereken hello toosee hello değişiklikleri olan `Index` ve `Create` görünümleri. 

Tür `Ctrl+F5` toorun hello uygulama.

Şimdi Yapılacaklar öğesi ekleyin ve denetleme **Bitti**. Ardından, giriş sayfanız tamamlanmış bir öğe olarak gösterilmesi gerekir. Bu hello unutmayın `Edit` görünümü hello Göster değil `Done` alan hello değişmedi çünkü `Edit` görünümü.

### <a name="enable-code-first-migrations-in-azure"></a>Azure'da Code First geçişleri etkinleştir

Kodunuzu değiştirmek works veritabanı geçiş dahil olmak üzere, göre tooyour Azure web uygulaması yayımlama ve SQL veritabanınızı Code First Migrations ile çok güncelleştirin.

Tıpkı, projenize sağ tıklayın ve önce seçin **Yayımla**.

Tıklatın **ayarları** tooopen hello Yayımla Sihirbazı.

![Açık yayımlama ayarları](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

Başlangıç Sihirbazı'nda tıklatın **sonraki**.

SQL veritabanınız olarak doldurulur için hello bağlantı dizesini doğrulayın **MyDatabaseContext (MyDbConnection)**. Tooselect hello gerekebilir **myToDoAppDb** veritabanından hello açılır. 

Seçin **yürütme önce kod uygulamalı geçişler (uygulama başlatılırken çalışır)**, ardından **kaydetmek**.

![Azure web uygulamasında Code First geçişleri etkinleştir](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a>Yaptığınız değişiklikleri yayımlama

Azure web uygulamanızda Code First Migrations etkinleştirildi, kod değişikliklerinizin yayımlayın.

Merhaba, yayımlama sayfası, tıklatın **Yayımla**.

Yapılacaklar öğelerini yeniden eklemeyi deneyin ve seçin **Bitti**, ve bunlar sayfanız tamamlanmış bir öğe olarak içinde gösterilmesi gerekir.

![Kod ilk geçişten sonra Azure web uygulaması](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

Tüm mevcut Yapılacaklar öğelerini hala görüntülenir. ASP.NET uygulamanızı yayımladığınızda, SQL veritabanında var olan veri kaybı olmadığından. Ayrıca, Code First Migrations hello veri şeması yalnızca değiştirir ve varolan verilerinizi dokunmaz.


## <a name="stream-application-logs"></a>Akış uygulama günlükleri

İzleme iletileri doğrudan, Azure web uygulaması tooVisual Studio akışını sağlayabilirsiniz.

Açık _Controllers\TodosController.cs_.

Her eylem ile başlayan bir `Trace.WriteLine()` yöntemi. Bu kodu tooshow eklenir, nasıl tooyour Azure web uygulaması tooadd izleme iletileri.

### <a name="open-server-explorer"></a>Açık Sunucu Gezgini

Merhaba gelen **Görünüm** menüsünde, select **Sunucu Gezgini**. Azure web uygulamanız için günlük kaydını yapılandırmak **Sunucu Gezgini**. 

### <a name="enable-log-streaming"></a>Günlük akışı etkinleştir

İçinde **Sunucu Gezgini**, genişletin **Azure** > **uygulama hizmeti**.

Merhaba genişletin **myResourceGroup** kaynak grubu, oluşturduğunuz ilk hello Azure web uygulaması oluşturduğunuzda.

Azure web uygulamanızın sağ tıklatıp **akış günlüklerini görüntüle**.

![Günlük akışı etkinleştir](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

Merhaba günlükleri şimdi hello akışı **çıkış** penceresi. 

![Çıktı penceresinde akış günlük](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

Ancak, hello izleme iletilerini henüz görmüyorsanız. Bu ilk seçtiğinizde, çünkü **akış günlüklerini görüntüle**, Azure web uygulamanızın ayarlar hello izleme düzeyi çok`Error`, hangi yalnızca günlükleri hata olayları (Merhaba ile `Trace.TraceError()` yöntemi).

### <a name="change-trace-levels"></a>Değişiklik izleme düzeyi

toochange hello izleme düzeyleri toooutput gidin diğer izleme iletilerini geri çok**Sunucu Gezgini**.

Azure web uygulamanızı yeniden sağ tıklatıp **ayarları**.

Merhaba, **uygulama günlüğü (dosya sistemi)** açılan listesinde, select **ayrıntılı**. **Kaydet** düğmesine tıklayın.

![Değişiklik izleme düzeyi tooVerbose](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> Ne tür iletileri her düzeyi için görüntülenen farklı izleme düzeyleri toosee ile deneyebilirsiniz. Örneğin, hello **bilgi** düzeyi tarafından oluşturulan tüm günlükleri içeren `Trace.TraceInformation()`, `Trace.TraceWarning()`, ve `Trace.TraceError()`, ancak tarafından oluşturulan günlükleri `Trace.WriteLine()`.
>
>

Tarayıcınızda, azure'da hello Yapılacaklar listesi uygulaması geçici tıklatmayı deneyin. Merhaba izleme iletilerini şimdi toohello akışı **çıkış** Visual Studio'daki.

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a>Akış Günlüğü Durdur

toostop günlük akış hizmeti Merhaba, hello tıklatın **izlemeyi durdurmak** hello düğmesini **çıkış** penceresi.

![Akış Günlüğü Durdur](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a>Azure web uygulamanızı yönetme

Toohello Git [Azure portal](https://portal.azure.com) oluşturduğunuz toosee hello web uygulaması. 



Merhaba sol menüden **uygulama hizmeti**, Azure web uygulamanızın hello adını tıklatın.

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

Web uygulamanızın sayfasında indiniz. 

Varsayılan olarak, hello portal hello gösterir **genel bakış** sayfası. Bu sayfa, uygulamanızın nasıl çalıştığını gösterir. Buradan ayrıca göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz. Merhaba sekmeler hello sayfasının sol tarafında hello açabilirsiniz hello farklı yapılandırma sayfaları gösterir. 

![Azure portalında App Service sayfası](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]
> * Azure SQL veritabanı oluşturma
> * Bir ASP.NET uygulaması tooSQL veritabanına bağlan
> * Merhaba uygulama tooAzure dağıtma
> * Merhaba veri modeli güncelleştirmek ve hello uygulama yeniden dağıtın
> * Azure tooyour terminal akış günlükleri
> * Merhaba uygulamada hello Azure portalı Yönet

İlerlemek toohello sonraki öğretici toolearn nasıl toomap özel DNS ad toohello web uygulaması.

> [!div class="nextstepaction"]
> [Harita bir var olan özel DNS adı tooAzure Web uygulamaları](app-service-web-tutorial-custom-domain.md)
