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
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="38811-104">Azure Mobile Apps için Hello .NET arka uç sunucusu SDK ile çalışma</span><span class="sxs-lookup"><span data-stu-id="38811-104">Work with hello .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="38811-105">Bu konu nasıl toouse hello anahtar Azure App Service Mobile Apps senaryolarda .NET arka uç sunucusu SDK gösterir.</span><span class="sxs-lookup"><span data-stu-id="38811-105">This topic shows you how toouse hello .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="38811-106">Hello Azure Mobile Apps SDK'sı, ASP.NET uygulamanız mobil istemcilerden çalışmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="38811-106">hello Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="38811-107">Merhaba [.NET server için Azure Mobile Apps SDK] [ 2] github'da açık bir kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="38811-107">hello [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="38811-108">Merhaba depo hello tüm sunucu SDK birim test paketi ve bazı örnek projeler de dahil olmak üzere tüm kaynak kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="38811-108">hello repository contains all source code including hello entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="38811-109">Başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="38811-109">Reference documentation</span></span>
<span data-ttu-id="38811-110">Merhaba sunucusu SDK Hello başvuru belgelerine bulunduğu burada: [Azure Mobile Apps .NET başvurusu][1].</span><span class="sxs-lookup"><span data-stu-id="38811-110">hello reference documentation for hello server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="38811-111"><a name="create-app"></a>Nasıl yapılır: bir .NET Mobil uygulama arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="38811-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="38811-112">Yeni bir proje başlıyorsanız, her iki hello kullanarak bir uygulama hizmeti uygulaması oluşturabilir [Azure portalı] veya Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38811-112">If you are starting a new project, you can create an App Service application using either hello [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="38811-113">Merhaba App Service uygulama yerel olarak çalıştırmak veya hello proje tooyour bulut tabanlı uygulama hizmeti mobil uygulama yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="38811-113">You can run hello App Service application locally or publish hello project tooyour cloud-based App Service mobile app.</span></span>

<span data-ttu-id="38811-114">Mobil özelliklerini tooan mevcut proje ekliyorsanız, hello bkz [indirin ve hello SDK başlatma](#install-sdk) bölümü.</span><span class="sxs-lookup"><span data-stu-id="38811-114">If you are adding mobile capabilities tooan existing project, see hello [Download and initialize hello SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-hello-azure-portal"></a><span data-ttu-id="38811-115">Hello Azure portal kullanarak bir .NET arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="38811-115">Create a .NET backend using hello Azure portal</span></span>
<span data-ttu-id="38811-116">bir uygulama hizmeti mobil arka uç toocreate, ya da izleyin hello [hızlı başlangıç Öğreticisi] [ 3] veya şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="38811-116">toocreate an App Service mobile backend, either follow hello [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="38811-117">Merhaba edilene *başlama* dikey altında **tablo API Oluştur**, seçin **C#** olarak, **arka uç dilinizi**.</span><span class="sxs-lookup"><span data-stu-id="38811-117">Back in hello *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="38811-118">Tıklatın **karşıdan**sıkıştırılmış proje dosyalarını tooyour yerel bilgisayar ayıklayın ve hello çözümü Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="38811-118">Click **Download**, extract the compressed project files tooyour local computer, and open hello solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="38811-119">Visual Studio 2013 ve Visual Studio 2015 kullanarak bir .NET arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="38811-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="38811-120">Merhaba yüklemek [.NET için Azure SDK] [ 4] (sürüm 2.9.0 veya sonrası) toocreate Visual Studio'da bir Azure Mobile Apps projesi.</span><span class="sxs-lookup"><span data-stu-id="38811-120">Install hello [Azure SDK for .NET][4] (version 2.9.0 or later) toocreate an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="38811-121">Merhaba SDK yükledikten sonra aşağıdaki adımları hello kullanarak bir ASP.NET uygulamasını oluşturun:</span><span class="sxs-lookup"><span data-stu-id="38811-121">Once you have installed hello SDK, create an ASP.NET application using hello following steps:</span></span>

1. <span data-ttu-id="38811-122">Açık hello **yeni proje** iletişim (gelen *dosya* > **yeni** > **proje...** ).</span><span class="sxs-lookup"><span data-stu-id="38811-122">Open hello **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="38811-123">Genişletme **şablonları** > **Visual C#**seçip **Web**.</span><span class="sxs-lookup"><span data-stu-id="38811-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="38811-124">Seçin **ASP.NET Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="38811-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="38811-125">Merhaba proje adı girin.</span><span class="sxs-lookup"><span data-stu-id="38811-125">Fill in hello project name.</span></span> <span data-ttu-id="38811-126">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38811-126">Then click **OK**.</span></span>
5. <span data-ttu-id="38811-127">Altında *ASP.NET 4.5.2 şablonları*seçin **Azure mobil uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="38811-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="38811-128">Denetleyin **hello buluttaki konağa** toocreate hello içinde mobil arka uç bulut toowhich bu proje yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38811-128">Check **Host in hello cloud** toocreate a mobile backend in hello cloud toowhich you can publish this project.</span></span>
6. <span data-ttu-id="38811-129">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38811-129">Click **OK**.</span></span>

## <span data-ttu-id="38811-130"><a name="install-sdk"></a>Nasıl yapılır: karşıdan yükle ve hello SDK başlatma</span><span class="sxs-lookup"><span data-stu-id="38811-130"><a name="install-sdk"></a>How to: Download and initialize hello SDK</span></span>
<span data-ttu-id="38811-131">Merhaba SDK kullanılabilir [NuGet.org]. Bu paket hello SDK kullanmaya hello gerekli temel işlevselliği tooget içerir.</span><span class="sxs-lookup"><span data-stu-id="38811-131">hello SDK is available on [NuGet.org]. This package includes hello base functionality required tooget started using hello SDK.</span></span> <span data-ttu-id="38811-132">tooinitialize SDK Merhaba, hello tooperform eylemleri gereksinim **HttpConfiguration** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="38811-132">tooinitialize hello SDK, you need tooperform actions on hello **HttpConfiguration** object.</span></span>

### <a name="install-hello-sdk"></a><span data-ttu-id="38811-133">Merhaba SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="38811-133">Install hello SDK</span></span>
<span data-ttu-id="38811-134">tooinstall hello SDK, Visual Studio'da hello sunucu projesi sağ tıklatın seçin **NuGet paketlerini Yönet**, hello Ara [Microsoft.Azure.Mobile.Server] paketini ve ardından  **Yükleme**.</span><span class="sxs-lookup"><span data-stu-id="38811-134">tooinstall hello SDK, right-click on hello server project in Visual Studio, select **Manage NuGet Packages**, search for hello [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="38811-135"><a name="server-project-setup"></a>Merhaba sunucu projesi başlatma</span><span class="sxs-lookup"><span data-stu-id="38811-135"><a name="server-project-setup"></a> Initialize hello server project</span></span>
<span data-ttu-id="38811-136">OWIN başlangıç sınıfı dahil ederek başlatılmış benzer tooother ASP.NET projeleri, .NET arka uç sunucu projesi var.</span><span class="sxs-lookup"><span data-stu-id="38811-136">A .NET backend server project is initialized similar tooother ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="38811-137">Merhaba NuGet paketi başvurulan olun `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="38811-137">Ensure that you have referenced hello NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="38811-138">tooadd Visual Studio'da bu sınıf sağ tıklayın, sunucu projesi ve select **Ekle** >
**yeni öğe**, ardından **Web**  >  ** Genel** > **OWIN başlangıç sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="38811-138">tooadd this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="38811-139">Bir sınıf özniteliği aşağıdaki hello ile oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="38811-139">A class is generated with hello following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="38811-140">Merhaba, `Configuration()` yöntemi, OWIN başlangıç sınıfı, kullanım, bir **HttpConfiguration** nesne tooconfigure hello Azure Mobile Apps ortamı.</span><span class="sxs-lookup"><span data-stu-id="38811-140">In hello `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object tooconfigure hello Azure Mobile Apps environment.</span></span>
<span data-ttu-id="38811-141">Aşağıdaki örnek hello hello sunucu projesi hiçbir ek özellikler içeren başlatır:</span><span class="sxs-lookup"><span data-stu-id="38811-141">hello following example initializes hello server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="38811-142">tooenable tek tek özellikleri, üzerinde hello genişletme yöntemlerini çağırmalıdır **MobileAppConfiguration** nesne çağırmadan önce **ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="38811-142">tooenable individual features, you must call extension methods on hello **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="38811-143">Örneğin, kod aşağıdaki hello hello varsayılan yolları hello özniteliğine sahip tooall API denetleyicilerinin ekler `[MobileAppController]` başlatma sırasında:</span><span class="sxs-lookup"><span data-stu-id="38811-143">For example, hello following code adds hello default routes tooall API controllers that have hello attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="38811-144">Merhaba server hızlı başlangıçtan hello Azure portal çağrıları **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="38811-144">hello server quickstart from hello Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="38811-145">Kurulum aşağıdaki bu eşdeğer toohello:</span><span class="sxs-lookup"><span data-stu-id="38811-145">This equivalent toohello following setup:</span></span>

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

<span data-ttu-id="38811-146">kullanılan hello uzantı yöntemleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="38811-146">hello extension methods used are:</span></span>

* <span data-ttu-id="38811-147">`AddMobileAppHomeController()`Merhaba varsayılan Azure Mobile Apps giriş sayfası sağlar.</span><span class="sxs-lookup"><span data-stu-id="38811-147">`AddMobileAppHomeController()` provides hello default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="38811-148">`MapApiControllers()`Merhaba ile donatılmış Webapı denetleyicileri için özel API olanakları sağlayan `[MobileAppController]` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="38811-148">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with hello `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="38811-149">`AddTables()`Merhaba eşlenmesini sağlar `/tables` uç noktaları tootable denetleyicileri.</span><span class="sxs-lookup"><span data-stu-id="38811-149">`AddTables()` provides a mapping of hello `/tables` endpoints tootable controllers.</span></span>
* <span data-ttu-id="38811-150">`AddTablesWithEntityFramework()`bir kısaltılmış eşleme hello için olan `/tables` Entity Framework kullanarak uç noktaları alarak denetleyicileri.</span><span class="sxs-lookup"><span data-stu-id="38811-150">`AddTablesWithEntityFramework()` is a short-hand for mapping hello `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="38811-151">`AddPushNotifications()`Bildirim hub'ları için cihazları kaydetme, basit bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="38811-151">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="38811-152">`MapLegacyCrossDomainController()`Standart CORS üstbilgilerini yerel geliştirme için sağlar.</span><span class="sxs-lookup"><span data-stu-id="38811-152">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="38811-153">SDK uzantıları</span><span class="sxs-lookup"><span data-stu-id="38811-153">SDK extensions</span></span>
<span data-ttu-id="38811-154">NuGet tabanlı uzantı paketleri aşağıdaki hello uygulamanız tarafından kullanılan çeşitli mobil özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="38811-154">hello following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="38811-155">Hello kullanarak başlatma sırasında uzantılarını etkinleştirme **MobileAppConfiguration** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="38811-155">You enable extensions during initialization by using hello **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="38811-156">[Microsoft.Azure.Mobile.Server.Quickstart] destekler hello temel Mobile Apps kurulumu.</span><span class="sxs-lookup"><span data-stu-id="38811-156">[Microsoft.Azure.Mobile.Server.Quickstart] Supports hello basic Mobile Apps setup.</span></span> <span data-ttu-id="38811-157">Arama hello tarafından eklenen toohello yapılandırma **UseDefaultConfiguration** başlatma sırasında genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="38811-157">Added toohello configuration by calling hello **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="38811-158">Bu uzantı uzantıları aşağıdaki içerir: bildirimleri, kimlik doğrulama, varlık, tablolar, etki alanları arası ve giriş paketleri.</span><span class="sxs-lookup"><span data-stu-id="38811-158">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="38811-159">Bu paket, hello Mobile Apps hızlı başlangıç hello Azure portalı üzerinde kullanılabilir tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="38811-159">This package is used by hello Mobile Apps Quickstart available on hello Azure portal.</span></span>
* <span data-ttu-id="38811-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) uygulayan hello varsayılan *bu mobil uygulamayı çalışır durumda olduğundan sayfa* hello web sitesinin kök.</span><span class="sxs-lookup"><span data-stu-id="38811-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements hello default *this mobile app is up and running page* for hello web site root.</span></span> <span data-ttu-id="38811-161">Çağırarak toohello yapılandırması eklemek **AddMobileAppHomeController** genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="38811-161">Add toohello configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="38811-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) veriler ve ayarlar yukarı hello veri ardışık ile çalışmaya yönelik sınıflar içerir.</span><span class="sxs-lookup"><span data-stu-id="38811-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up hello data pipeline.</span></span> <span data-ttu-id="38811-163">Toohello yapılandırması tarafından arama hello eklemek **AddTables** genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="38811-163">Add toohello configuration by calling hello **AddTables** extension method.</span></span>
* <span data-ttu-id="38811-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) hello Entity Framework tooaccess verileri hello SQL veritabanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="38811-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables hello Entity Framework tooaccess data in hello SQL Database.</span></span> <span data-ttu-id="38811-165">Toohello yapılandırması tarafından arama hello eklemek **AddTablesWithEntityFramework** genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="38811-165">Add toohello configuration by calling hello **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="38811-166">[Microsoft.Azure.Mobile.Server.Authentication] etkinleştirir kimlik doğrulama ve ayarlar yukarı hello OWIN ara yazılımı toovalidate belirteçleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="38811-166">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up hello OWIN middleware used toovalidate tokens.</span></span> <span data-ttu-id="38811-167">Toohello yapılandırması tarafından arama hello eklemek **AddAppServiceAuthentication** ve **Iappbuilder**. **UseAppServiceAuthentication** genişletme yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="38811-167">Add toohello configuration by calling hello **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="38811-168">[Microsoft.Azure.Mobile.Server.Notifications] anında iletme bildirimleri ve anında iletme kayıt uç noktasını tanımlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="38811-168">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="38811-169">Toohello yapılandırması tarafından arama hello eklemek **AddPushNotifications** genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="38811-169">Add toohello configuration by calling hello **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="38811-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) veri toolegacy mobil uygulamanızın web tarayıcılarından hizmet veren bir denetleyiciyi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="38811-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data toolegacy web browsers from your Mobile App.</span></span> <span data-ttu-id="38811-171">Çağırarak toohello yapılandırması eklemek **MapLegacyCrossDomainController** genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="38811-171">Add toohello configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="38811-172">[Microsoft.Azure.Mobile.Server.Login] özel kimlik doğrulama senaryoları sırasında kullanılan bir statik yöntem hello AppServiceLoginHandler.CreateToken() yöntemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="38811-172">[Microsoft.Azure.Mobile.Server.Login] Provides hello AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="38811-173"><a name="publish-server-project"></a>Nasıl yapılır: yayımlama hello sunucu projesi</span><span class="sxs-lookup"><span data-stu-id="38811-173"><a name="publish-server-project"></a>How to: Publish hello server project</span></span>
<span data-ttu-id="38811-174">Bu bölümde, nasıl toopublish .NET arka ucu proje Visual Studio'dan gösterir.</span><span class="sxs-lookup"><span data-stu-id="38811-174">This section shows you how toopublish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="38811-175">Arka uç projeniz Git kullanarak da dağıtabilir veya herhangi bir hello hello kapsamdaki diğer yöntemleri [Azure uygulama hizmeti dağıtım belgeleri](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="38811-175">You can also deploy your backend project using Git or any of hello other methods covered in hello [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="38811-176">Visual Studio'da hello proje toorestore NuGet paketlerini yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38811-176">In Visual Studio, rebuild hello project toorestore NuGet packages.</span></span>
2. <span data-ttu-id="38811-177">Çözüm Gezgini'nde, sağ hello proje tıklatın **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="38811-177">In Solution Explorer, right-click hello project, click **Publish**.</span></span> <span data-ttu-id="38811-178">Merhaba, yayımladığınız ilk kez, toodefine bir yayımlama profili gerekir.</span><span class="sxs-lookup"><span data-stu-id="38811-178">hello first time you publish, you need toodefine a publishing profile.</span></span> <span data-ttu-id="38811-179">Önceden tanımlı bir profili varsa, seçin ve tıklatın **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="38811-179">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="38811-180">Tooselect yayımlama hedefi sorulursa tıklatın **Microsoft Azure App Service** > **sonraki**, sonra (gerekirse) ile Azure kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="38811-180">If asked tooselect a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="38811-181">Visual Studio indirmeleri ve güvenli bir şekilde depolar, doğrudan Azure ayarlarını yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="38811-181">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="38811-182">Seçin, **abonelik**seçin **kaynak türü** gelen **Görünüm**, genişletin **mobil uygulama**ve mobil uygulama arka tıklayın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="38811-182">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="38811-183">Merhaba doğrulayın profil bilgilerini yayımlamak ve tıklatın **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="38811-183">Verify hello publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="38811-184">Mobil uygulama arka başarıyla yayımladı, başarıyı gösteren bir giriş sayfasına bakın.</span><span class="sxs-lookup"><span data-stu-id="38811-184">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="38811-185"><a name="define-table-controller"></a>Nasıl yapılır: bir tablo denetleyicisi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="38811-185"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="38811-186">Bir tablo denetleyicisi tooexpose SQL tablosu toomobile istemcileri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="38811-186">Define a Table Controller tooexpose a SQL table toomobile clients.</span></span>  <span data-ttu-id="38811-187">Bir tablo denetleyicisi yapılandırma üç adımı gerektirir:</span><span class="sxs-lookup"><span data-stu-id="38811-187">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="38811-188">Bir veri aktarım nesnesini (DTO) sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38811-188">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="38811-189">Bir tablo başvurusu hello mobil DbContext sınıfı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="38811-189">Configure a table reference in hello Mobile DbContext class.</span></span>
3. <span data-ttu-id="38811-190">Bir tablo denetleyicisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38811-190">Create a table controller.</span></span>

<span data-ttu-id="38811-191">Bir veri aktarım nesnesini (DTO) öğesinden devralınan bir düz C# nesnesidir `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="38811-191">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="38811-192">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="38811-192">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="38811-193">Merhaba DTO hello SQL veritabanı içinde kullanılan toodefine hello tablosu değil.</span><span class="sxs-lookup"><span data-stu-id="38811-193">hello DTO is used toodefine hello table within hello SQL database.</span></span>  <span data-ttu-id="38811-194">toocreate hello veritabanı girişi, ekleme bir `DbSet<>` hello kullanmakta olduğunuz DbContext özelliğine.</span><span class="sxs-lookup"><span data-stu-id="38811-194">toocreate hello database entry, add a `DbSet<>` property to hello DbContext you are using.</span></span>  <span data-ttu-id="38811-195">Merhaba varsayılan proje şablonu Azure mobil uygulamalar için hello DbContext çağrılır `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="38811-195">In hello default project template for Azure Mobile Apps, hello DbContext is called `Models\MobileServiceContext.cs`:</span></span>

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

<span data-ttu-id="38811-196">Azure SDK'sı yüklü hello varsa, aşağıdaki gibi bir şablon tablo denetleyicisi artık oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="38811-196">If you have hello Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="38811-197">Merhaba denetleyicileri klasörü sağ tıklatın ve seçin **Ekle** > **denetleyicisi...** .</span><span class="sxs-lookup"><span data-stu-id="38811-197">Right-click on hello Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="38811-198">Select hello **Azure Mobile Apps tablo denetleyicisi** seçeneğini ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="38811-198">Select hello **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="38811-199">Merhaba, **denetleyici Ekle** iletişim:</span><span class="sxs-lookup"><span data-stu-id="38811-199">In hello **Add Controller** dialog:</span></span>
   * <span data-ttu-id="38811-200">Merhaba, **Model sınıfı** açılan listesinde, yeni DTO seçin.</span><span class="sxs-lookup"><span data-stu-id="38811-200">In hello **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="38811-201">Merhaba, **DbContext** açılan listesinde, select hello mobil hizmet DbContext sınıfı.</span><span class="sxs-lookup"><span data-stu-id="38811-201">In hello **DbContext** dropdown, select hello Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="38811-202">Merhaba Denetleyici adı sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="38811-202">hello Controller name is created for you.</span></span>
4. <span data-ttu-id="38811-203">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="38811-203">Click **Add**.</span></span>

<span data-ttu-id="38811-204">Hello hızlı başlangıç sunucu projesi içeren basit bir örneğin **TodoItemController**.</span><span class="sxs-lookup"><span data-stu-id="38811-204">hello quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="38811-205"><a name="adjust-pagesize"></a>Nasıl yapılır: hello tablo disk belleği boyutunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="38811-205"><a name="adjust-pagesize"></a>How to: Adjust hello table paging size</span></span>
<span data-ttu-id="38811-206">Varsayılan olarak, Azure Mobile Apps istek başına 50 kayıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="38811-206">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="38811-207">Disk belleği hello istemci kendi kullanıcı Arabirimi iş parçacığı veya hello sunucusu çok uzun bir süre için iyi bir kullanıcı deneyimi sağlayarak tie değil sağlar.</span><span class="sxs-lookup"><span data-stu-id="38811-207">Paging ensures that hello client does not tie up their UI thread nor hello server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="38811-208">toochange hello tablo disk belleği boyutu artışı hello sunucu tarafı "izin verilen sorgu boyutu" ve hello istemci-tarafı sayfa boyutu hello sunucu tarafı "izin verilen sorgu boyutu" Merhaba kullanarak ayarlanır `EnableQuery` özniteliği:</span><span class="sxs-lookup"><span data-stu-id="38811-208">toochange hello table paging size, increase hello server side "allowed query size" and hello client-side page size hello server side "allowed query size" is adjusted using hello `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="38811-209">Merhaba PageSize hello aynı ya da hello istemci tarafından istenilen hello boyutundan büyük olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="38811-209">Ensure hello PageSize is hello same or larger than hello size requested by hello client.</span></span>  <span data-ttu-id="38811-210">Merhaba istemci sayfa boyutunu değiştirme hakkında ayrıntılar için toohello belirli istemci nasıl yapılır belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="38811-210">Refer toohello specific client HOWTO documentation for details on changing hello client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="38811-211">Nasıl yapılır: özel bir API denetleyicisi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="38811-211">How to: Define a custom API controller</span></span>
<span data-ttu-id="38811-212">Merhaba özel API denetleyicisi hello en temel işlevleri tooyour mobil uygulama arka uç nokta göstererek sağlar.</span><span class="sxs-lookup"><span data-stu-id="38811-212">hello custom API controller provides hello most basic functionality tooyour Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="38811-213">Merhaba [MobileAppController] özniteliği kullanılarak mobile özgü API denetleyicisi kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38811-213">You can register a mobile-specific API controller using hello [MobileAppController] attribute.</span></span> <span data-ttu-id="38811-214">Merhaba `MobileAppController` özniteliği hello rota kaydeder, hello Mobile Apps JSON serileştirici ayarlar ve açar [istemci sürüm denetimi](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="38811-214">hello `MobileAppController` attribute registers hello route, sets up hello Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="38811-215">Visual Studio'da hello denetleyicileri klasörü sağ tıklatın, ardından **Ekle** > **denetleyicisi**seçin **Web API 2 denetleyicisi&mdash;boş** ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="38811-215">In Visual Studio, right-click hello Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="38811-216">Tedarik bir **Denetleyici adı**, gibi `CustomController`, tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="38811-216">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="38811-217">Merhaba yeni denetleyici sınıfı dosyasında hello aşağıdakileri ekleyin deyimi kullanarak:</span><span class="sxs-lookup"><span data-stu-id="38811-217">In hello new controller class file, add hello following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="38811-218">Merhaba uygulamak **[MobileAppController]** özniteliği aşağıdaki örneğine hello olduğu gibi toohello API denetleyicisi sınıfı tanımı:</span><span class="sxs-lookup"><span data-stu-id="38811-218">Apply hello **[MobileAppController]** attribute toohello API controller class definition, as in hello following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="38811-219">Çağrı toohello App_Start/Startup.MobileApp.cs dosyasında ekleyin **MapApiControllers** uzantısı yönteminizdeki aşağıdaki örneğine hello:</span><span class="sxs-lookup"><span data-stu-id="38811-219">In App_Start/Startup.MobileApp.cs file, add a call toohello **MapApiControllers** extension method, as in hello following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="38811-220">Merhaba de kullanabilirsiniz `UseDefaultConfiguration()` genişletme yöntemi yerine `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="38811-220">You can also use hello `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="38811-221">Sahip olmadığı herhangi bir denetleyicisi **MobileAppControllerAttribute** uygulanan hala istemcileri tarafından erişilebilen, ancak bunu doğru şekilde herhangi bir mobil uygulama istemci SDK kullanan istemciler tarafından tüketilmeyen.</span><span class="sxs-lookup"><span data-stu-id="38811-221">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="38811-222">Nasıl yapılır: kimlik doğrulaması ile çalışma</span><span class="sxs-lookup"><span data-stu-id="38811-222">How to: Work with authentication</span></span>
<span data-ttu-id="38811-223">Azure Mobile Apps kullanan App Service kimlik doğrulama / yetkilendirme toosecure mobil arka.</span><span class="sxs-lookup"><span data-stu-id="38811-223">Azure Mobile Apps uses App Service Authentication / Authorization toosecure your mobile backend.</span></span>  <span data-ttu-id="38811-224">Bu bölümde, nasıl gösterilir .NET arka uç sunucu projenizi kimlik doğrulaması ile ilgili görevleri aşağıdaki tooperform hello:</span><span class="sxs-lookup"><span data-stu-id="38811-224">This section shows you how tooperform hello following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="38811-225">Nasıl yapılır: kimlik doğrulaması tooa sunucu projesi ekleme</span><span class="sxs-lookup"><span data-stu-id="38811-225">How to: Add authentication tooa server project</span></span>](#add-auth)
* [<span data-ttu-id="38811-226">Nasıl yapılır: uygulamanız için özel kimlik doğrulamasını kullan</span><span class="sxs-lookup"><span data-stu-id="38811-226">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="38811-227">Nasıl yapılır: alma kimliği doğrulanmış kullanıcı bilgileri</span><span class="sxs-lookup"><span data-stu-id="38811-227">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="38811-228">Nasıl yapılır: yetkili kullanıcıların veri erişimini kısıtlamak</span><span class="sxs-lookup"><span data-stu-id="38811-228">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="38811-229"><a name="add-auth"></a>Nasıl yapılır: kimlik doğrulaması tooa sunucu projesi ekleme</span><span class="sxs-lookup"><span data-stu-id="38811-229"><a name="add-auth"></a>How to: Add authentication tooa server project</span></span>
<span data-ttu-id="38811-230">Kimlik doğrulama tooyour sunucu projesi hello genişleterek ekleyebileceğiniz **MobileAppConfiguration** nesne ve OWIN ara yazılımı yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="38811-230">You can add authentication tooyour server project by extending hello **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="38811-231">Merhaba yüklediğinizde [Microsoft.Azure.Mobile.Server.Quickstart] paket ve çağrı hello **UseDefaultConfiguration** genişletme yöntemi, toostep 3 atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38811-231">When you install hello [Microsoft.Azure.Mobile.Server.Quickstart] package and call hello **UseDefaultConfiguration** extension method, you can skip toostep 3.</span></span>

1. <span data-ttu-id="38811-232">Visual Studio'da hello yüklemek [Microsoft.Azure.Mobile.Server.Authentication] paket.</span><span class="sxs-lookup"><span data-stu-id="38811-232">In Visual Studio, install hello [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="38811-233">Aşağıdaki kod hello hello başında hello Hello haline proje dosyasında eklemek **yapılandırma** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="38811-233">In hello Startup.cs project file, add hello following line of code at hello beginning of hello **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="38811-234">Bu OWIN ara yazılım bileşeni ilişkili hello uygulama hizmeti gateway tarafından yayınlanan belirteçleri doğrular.</span><span class="sxs-lookup"><span data-stu-id="38811-234">This OWIN middleware component validates tokens issued by hello associated App Service gateway.</span></span>
3. <span data-ttu-id="38811-235">Merhaba eklemek `[Authorize]` özniteliği tooany denetleyicisi veya kimlik doğrulama gerektiren yöntemi.</span><span class="sxs-lookup"><span data-stu-id="38811-235">Add hello `[Authorize]` attribute tooany controller or method that requires authentication.</span></span>

<span data-ttu-id="38811-236">toolearn konusunda tooauthenticate istemcileri tooyour Mobile Apps arka bkz [Ekle kimlik doğrulama tooyour uygulama](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="38811-236">toolearn about how tooauthenticate clients tooyour Mobile Apps backend, see [Add authentication tooyour app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="38811-237"><a name="custom-auth"></a>Nasıl yapılır: uygulamanız için özel kimlik doğrulamasını kullan</span><span class="sxs-lookup"><span data-stu-id="38811-237"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="38811-238">Toouse hello App Service kimlik doğrulama/yetkilendirme sağlayıcılardan biri istemiyorsanız, kendi oturum açma sistem uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38811-238">If you do not wish toouse one of hello App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="38811-239">Merhaba yüklemek [Microsoft.Azure.Mobile.Server.Login] tooassist kimlik doğrulama belirteci oluşturma ile paket.</span><span class="sxs-lookup"><span data-stu-id="38811-239">Install hello [Microsoft.Azure.Mobile.Server.Login] package tooassist with authentication token generation.</span></span>  <span data-ttu-id="38811-240">Kullanıcı kimlik bilgilerini doğrulamak için kendi kodunuzu girin.</span><span class="sxs-lookup"><span data-stu-id="38811-240">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="38811-241">Örneğin, güvenlik ve karma parolaları bir veritabanında karşı denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38811-241">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="38811-242">Merhaba aşağıdaki örnekte, hello `isValidAssertion()` yöntemi (başka bir yerde tanımlanır) için bu denetimleri sorumlu.</span><span class="sxs-lookup"><span data-stu-id="38811-242">In hello example below, hello `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="38811-243">bir ApiController oluşturma ve gösterme Hello özel kimlik doğrulama açığa `register` ve `login` eylemler.</span><span class="sxs-lookup"><span data-stu-id="38811-243">hello custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="38811-244">Merhaba istemci hello kullanıcıdan özel kullanıcı Arabirimi toocollect hello bilgilerini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="38811-244">hello client should use a custom UI toocollect hello information from hello user.</span></span>  <span data-ttu-id="38811-245">Standart bir HTTP POST ile birlikte gönderilen toohello API çağrısı sonra hello bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="38811-245">hello information is then submitted toohello API with a standard HTTP POST call.</span></span> <span data-ttu-id="38811-246">Merhaba onaylama Hello sunucuyu doğrular sonra bir belirteç hello kullanarak verilen `AppServiceLoginHandler.CreateToken()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="38811-246">Once hello server validates hello assertion, a token is issued using hello `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="38811-247">Merhaba ApiController **vermemelisiniz** hello kullan `[MobileAppController]` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="38811-247">hello ApiController **should not** use hello `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="38811-248">Örnek `login` eylem:</span><span class="sxs-lookup"><span data-stu-id="38811-248">An example `login` action:</span></span>

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

<span data-ttu-id="38811-249">Örnek önceki hello LoginResult ve LoginResultUser gerekli özellikleri gösterme seri hale getirilebilir nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="38811-249">In hello preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="38811-250">Merhaba istemci oturum açma yanıtları toobe hello form JSON nesneler olarak döndürülen bekler:</span><span class="sxs-lookup"><span data-stu-id="38811-250">hello client expects login responses toobe returned as JSON objects of hello form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="38811-251">Merhaba `AppServiceLoginHandler.CreateToken()` yöntemi içeren bir *İzleyici* ve bir *veren* parametresi.</span><span class="sxs-lookup"><span data-stu-id="38811-251">hello `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="38811-252">Bu parametrelerin her ikisini de toohello URL'sini hello HTTPS şeması kullanarak, uygulamanızın kök ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="38811-252">Both of these parameters are set toohello URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="38811-253">Benzer şekilde ayarlamalısınız *secretKey* toobe hello değeri, uygulamanızın imzalama anahtarı.</span><span class="sxs-lookup"><span data-stu-id="38811-253">Similarly you should set *secretKey* toobe hello value of your application's signing key.</span></span> <span data-ttu-id="38811-254">Bir istemci anahtarı olarak kullanılan toomint anahtarlarının olması ve kullanıcıların kimliğine imzalama hello dağıtmayın.</span><span class="sxs-lookup"><span data-stu-id="38811-254">Do not distribute hello signing key in a client as it can be used toomint keys and impersonate users.</span></span> <span data-ttu-id="38811-255">Merhaba başvurarak App Service içinde barındırılan tutarak imzalama hello edinebilirsiniz *Web sitesi\_AUTH\_imzalama\_anahtar* ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="38811-255">You can obtain hello signing key while hosted in App Service by referencing hello *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="38811-256">Yerel hata ayıklama bağlamda gerekirse hello hello yönergeleri izleyin [yerel kimlik doğrulaması ile hata ayıklama](#local-debug) bölümünde tooretrieve hello anahtarı ve bir uygulama ayarı olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="38811-256">If needed in a local debugging context, follow hello instructions in hello [Local debugging with authentication](#local-debug) section tooretrieve hello key and store it as an application setting.</span></span>

<span data-ttu-id="38811-257">verilen hello belirteci ayrıca diğer talepleri ve sona erme tarihi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="38811-257">hello issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="38811-258">En düşük düzeyde, verilen hello belirteci bir konu içermelidir (**alt**) talep.</span><span class="sxs-lookup"><span data-stu-id="38811-258">Minimally, hello issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="38811-259">Merhaba standart istemci destekleyebilir `loginAsync()` hello kimlik doğrulaması rota aşırı yüklemesi tarafından yöntemi.</span><span class="sxs-lookup"><span data-stu-id="38811-259">You can support hello standard client `loginAsync()` method by overloading hello authentication route.</span></span>  <span data-ttu-id="38811-260">Merhaba istemci çağırırsa `client.loginAsync('custom');` toolog içinde rota olmalıdır `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="38811-260">If hello client calls `client.loginAsync('custom');` toolog in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="38811-261">Merhaba denetleyicisi özel kimlik doğrulama kullanarak hello yol ayarlayabilirsiniz `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="38811-261">You can set hello route for hello custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="38811-262">Hello kullanarak `loginAsync()` yaklaşım sağlar hello kimlik doğrulama belirtecini bağlı tooevery sonraki çağrı toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="38811-262">Using hello `loginAsync()` approach ensures that hello authentication token is attached tooevery subsequent call toohello service.</span></span>
>
>

### <span data-ttu-id="38811-263"><a name="user-info"></a>Nasıl yapılır: alma kimliği doğrulanmış kullanıcı bilgileri</span><span class="sxs-lookup"><span data-stu-id="38811-263"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="38811-264">Bir kullanıcı tarafından uygulama hizmeti doğrulandığında, kullanıcı kimliği ve diğer bilgileri .NET arka uç kodunuzun atanan hello erişebilir.</span><span class="sxs-lookup"><span data-stu-id="38811-264">When a user is authenticated by App Service, you can access hello assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="38811-265">Merhaba kullanıcı bilgilerini hello arka yetkilendirme kararları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="38811-265">hello user information can be used for making authorization decisions in hello backend.</span></span> <span data-ttu-id="38811-266">Merhaba aşağıdaki kod bir istekle ilişkili hello kullanıcı Kimliğini alır:</span><span class="sxs-lookup"><span data-stu-id="38811-266">hello following code obtains hello user ID associated with a request:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="38811-267">Merhaba SID hello sağlayıcıya özgü kullanıcı ID'den türetilmiş ve verilen kullanıcı ve oturum açma sağlayıcısı için statiktir.</span><span class="sxs-lookup"><span data-stu-id="38811-267">hello SID is derived from hello provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="38811-268">Merhaba SID için geçersiz kimlik doğrulama belirteçleri null şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="38811-268">hello SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="38811-269">Uygulama Hizmeti ayrıca oturum açma sağlayıcınızdan belirli talep istemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="38811-269">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="38811-270">Her bir kimlik sağlayıcısı kimlik sağlayıcısı SDK kullanarak daha fazla bilgi sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="38811-270">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="38811-271">Örneğin, arkadaş bilgilerini hello Facebook grafik API'sini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38811-271">For example, you can use hello Facebook Graph API for friends information.</span></span>  <span data-ttu-id="38811-272">İstenen taleplerin hello sağlayıcısı dikey penceresinde hello Azure portal belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38811-272">You can specify claims that are requested in hello provider blade in hello Azure portal.</span></span> <span data-ttu-id="38811-273">Bazı talep hello kimlik sağlayıcısı ile ek yapılandırma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="38811-273">Some claims require additional configuration with hello identity provider.</span></span>

<span data-ttu-id="38811-274">Merhaba aşağıdaki kod çağrıları hello **GetAppServiceIdentityAsync** hello erişim belirteci gerekli toomake hello Facebook grafik API'si istekler dahil uzantısı yöntemi tooget hello oturum açma kimlik bilgileri:</span><span class="sxs-lookup"><span data-stu-id="38811-274">hello following code calls hello **GetAppServiceIdentityAsync** extension method tooget hello login credentials, which include hello access token needed toomake requests against hello Facebook Graph API:</span></span>

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

<span data-ttu-id="38811-275">Kullanarak bir ekleme deyimi için `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="38811-275">Add a using statement for `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="38811-276"><a name="authorize"></a>Nasıl yapılır: yetkili kullanıcıların veri erişimini kısıtlamak</span><span class="sxs-lookup"><span data-stu-id="38811-276"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="38811-277">Merhaba önceki bölümde nasıl tooretrieve hello kimliği doğrulanmış bir kullanıcı kullanıcı Kimliğini gösterdi.</span><span class="sxs-lookup"><span data-stu-id="38811-277">In hello previous section, we showed how tooretrieve hello user ID of an authenticated user.</span></span> <span data-ttu-id="38811-278">Erişim toodata ve diğer kaynaklar bu değere göre kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38811-278">You can restrict access toodata and other resources based on this value.</span></span> <span data-ttu-id="38811-279">Örneğin, bir kullanıcı kimliği sütunu tootables ekleme ve hello sorgu sonuçları hello kullanıcı Kimliğine göre filtreleme verileri yalnızca tooauthorized kullanıcılar döndürülen basit yol toolimit olur.</span><span class="sxs-lookup"><span data-stu-id="38811-279">For example, adding a userId column tootables and filtering hello query results by hello user ID is a simple way toolimit returned data only tooauthorized users.</span></span> <span data-ttu-id="38811-280">yalnızca hello SID hello Todoıtem tablosu üzerinde hello UserID sütunundaki değeri eşleştiğinde hello aşağıdaki kod veri satırlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="38811-280">hello following code returns data rows only when hello SID matches the value in hello UserId column on hello TodoItem table:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="38811-281">Merhaba `Query()` yöntemi döndürür bir `IQueryable` , yönetilebilir toohandle LINQ filtreleyerek.</span><span class="sxs-lookup"><span data-stu-id="38811-281">hello `Query()` method returns an `IQueryable` that can be manipulated by LINQ toohandle filtering.</span></span>

## <a name="how-to-add-push-notifications-tooa-server-project"></a><span data-ttu-id="38811-282">Nasıl yapılır: anında iletme bildirimleri tooa sunucu projesi ekleme</span><span class="sxs-lookup"><span data-stu-id="38811-282">How to: Add push notifications tooa server project</span></span>
<span data-ttu-id="38811-283">Merhaba genişleterek anında iletme bildirimleri tooyour sunucu projesi eklemek **MobileAppConfiguration** nesne ve bildirim hub'ları istemci oluşturma.</span><span class="sxs-lookup"><span data-stu-id="38811-283">Add push notifications tooyour server project by extending hello **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="38811-284">Visual Studio'da hello sunucu projesi sağ tıklatın ve **NuGet paketlerini Yönet**, arama `Microsoft.Azure.Mobile.Server.Notifications`, ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="38811-284">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="38811-285">Bu adım tooinstall hello yineleyin `Microsoft.Azure.NotificationHubs` hello bildirim hub'ları istemci kitaplığı içeren paket.</span><span class="sxs-lookup"><span data-stu-id="38811-285">Repeat this step tooinstall hello `Microsoft.Azure.NotificationHubs` package, which includes hello Notification Hubs client library.</span></span>
3. <span data-ttu-id="38811-286">App_Start/Startup.MobileApp.cs içinde arama toohello ekleyin **AddPushNotifications()** genişletme yöntemi başlatma sırasında:</span><span class="sxs-lookup"><span data-stu-id="38811-286">In App_Start/Startup.MobileApp.cs, and add a call toohello **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="38811-287">Bildirim hub'ları istemci oluşturur koddan hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="38811-287">Add hello following code that creates a Notification Hubs client:</span></span>

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

<span data-ttu-id="38811-288">Merhaba bildirim hub'ları istemci toosend anında iletme bildirimleri tooregistered cihazlar artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38811-288">You can now use hello Notification Hubs client toosend push notifications tooregistered devices.</span></span> <span data-ttu-id="38811-289">Daha fazla bilgi için bkz: [Ekle anında iletme bildirimleri tooyour uygulama](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="38811-289">For more information, see [Add push notifications tooyour app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="38811-290">Bildirim hub'ları hakkında daha fazla toolearn bkz [Notification Hubs'a genel bakış](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="38811-290">toolearn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="38811-291"><a name="tags"></a>Nasıl yapılır: etkinleştir hedeflenen etiketleri kullanarak anında iletme</span><span class="sxs-lookup"><span data-stu-id="38811-291"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="38811-292">Bildirim hub'ları etiketleri kullanarak toospecific kayıtlar hedeflenen bildirimleri göndermenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="38811-292">Notification Hubs lets you send targeted notifications toospecific registrations by using tags.</span></span> <span data-ttu-id="38811-293">Birkaç etiket otomatik olarak oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="38811-293">Several tags are created automatically:</span></span>

* <span data-ttu-id="38811-294">belirli bir aygıt Hello yükleme kimliği tanımlar.</span><span class="sxs-lookup"><span data-stu-id="38811-294">hello Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="38811-295">Merhaba kullanıcı kimliği temel kimlik doğrulaması hello üzerinde SID belirli bir kullanıcı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="38811-295">hello User Id based on hello authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="38811-296">Merhaba hello kimliği erişilebilir yükleme **InstallationID** hello özellikte **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="38811-296">hello installation ID can be accessed from hello **installationId** property on hello **MobileServiceClient**.</span></span>  <span data-ttu-id="38811-297">Hello aşağıdaki örnekte bir yükleme kimliği tooadd nasıl kullanılacağını etiket tooa belirli yükleme bildirim hub'ları gösterir:</span><span class="sxs-lookup"><span data-stu-id="38811-297">hello following example shows how to use an installation ID tooadd a tag tooa specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="38811-298">Anında iletme bildirimi kaydı sırasında Hello istemci tarafından sağlanan herhangi bir etiket hello arka ucu tarafından hello yükleme oluştururken göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="38811-298">Any tags supplied by hello client during push notification registration are ignored by hello backend when creating hello installation.</span></span> <span data-ttu-id="38811-299">toohello yükleme tooenable istemci tooadd etiketleri, düzeni önceki hello kullanarak etiketleri ekler özel bir API oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="38811-299">tooenable a client tooadd tags toohello installation, you must create a custom API that adds tags using hello preceding pattern.</span></span>

<span data-ttu-id="38811-300">Bkz: [istemci eklenen anında iletme bildirimi etiketleri] [ 5] hello App Service Mobile Apps tamamlanmış hızlı başlangıç örnek bir örnek.</span><span class="sxs-lookup"><span data-stu-id="38811-300">See [Client-added push notification tags][5] in hello App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="38811-301"><a name="push-user"></a>Nasıl yapılır: gönderme anında iletme bildirimleri tooan kimliği doğrulanmış kullanıcı</span><span class="sxs-lookup"><span data-stu-id="38811-301"><a name="push-user"></a>How to: Send push notifications tooan authenticated user</span></span>
<span data-ttu-id="38811-302">Kimliği doğrulanmış bir kullanıcı için anında iletme bildirimleri kaydolduğunda, bir kullanıcı kimliği etiketi toohello kayıt otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="38811-302">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="38811-303">Bu etiketi kullanarak anında iletme bildirimleri tooall cihazlar söz konusu kişi tarafından kayıtlı gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38811-303">By using this tag, you can send push notifications tooall devices registered by that person.</span></span> <span data-ttu-id="38811-304">Merhaba aşağıdaki kod hello isteği yapan kullanıcı SID'si alır ve bu kişi için bir şablon anında iletme bildirimi tooevery aygıt kaydı gönderir:</span><span class="sxs-lookup"><span data-stu-id="38811-304">hello following code gets hello SID of user making the request and sends a template push notification tooevery device registration for that person:</span></span>

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="38811-305">Kimliği doğrulanmış bir istemci anında iletme bildirimleri için kaydolurken kayıt denemeden önce kimlik doğrulamasının tam olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="38811-305">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="38811-306">Daha fazla bilgi için bkz: [anında toousers] [ 6] hello App Service Mobile Apps tamamlanmış hızlı başlangıç örnek .NET arka ucu için.</span><span class="sxs-lookup"><span data-stu-id="38811-306">For more information, see [Push toousers][6] in hello App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a><span data-ttu-id="38811-307">Nasıl yapılır: hata ayıklama ve sorun giderme hello .NET sunucusu SDK</span><span class="sxs-lookup"><span data-stu-id="38811-307">How to: Debug and troubleshoot hello .NET Server SDK</span></span>
<span data-ttu-id="38811-308">Azure uygulama hizmeti birkaç hata ayıklama ve sorun giderme teknikleri ASP.NET uygulamaları için sağlar:</span><span class="sxs-lookup"><span data-stu-id="38811-308">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="38811-309">Bir Azure uygulama hizmeti izleme</span><span class="sxs-lookup"><span data-stu-id="38811-309">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="38811-310">Azure uygulama hizmetinde tanılama günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="38811-310">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="38811-311">Visual Studio'da bir Azure uygulama hizmeti sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="38811-311">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="38811-312">Günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="38811-312">Logging</span></span>
<span data-ttu-id="38811-313">Merhaba standart ASP.NET izleme yazma kullanarak hizmet tanılama günlükleri tooApp yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38811-313">You can write tooApp Service diagnostic logs by using hello standard ASP.NET trace writing.</span></span> <span data-ttu-id="38811-314">Toohello günlükleri yazmadan önce mobil uygulama arka ucunuzu tanılama etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="38811-314">Before you can write toohello logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="38811-315">tooenable tanılama ve yazma toohello günlükleri:</span><span class="sxs-lookup"><span data-stu-id="38811-315">tooenable diagnostics and write toohello logs:</span></span>

1. <span data-ttu-id="38811-316">Merhaba adımları [nasıl tooenable tanılama](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="38811-316">Follow hello steps in [How tooenable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="38811-317">Merhaba aşağıdakileri ekleyin, kod dosyanızda deyimiyle:</span><span class="sxs-lookup"><span data-stu-id="38811-317">Add hello following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="38811-318">İzleme yazıcısı toowrite hello .NET arka uç toohello tanılama günlükleri, aşağıdaki gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="38811-318">Create a trace writer toowrite from hello .NET backend toohello diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="38811-319">Sunucu projenizi yeniden yayımlamanız ve hello mobil uygulama arka uç tooexecute hello kod yolu hello günlük ile erişim.</span><span class="sxs-lookup"><span data-stu-id="38811-319">Republish your server project, and access hello Mobile App backend tooexecute hello code path with hello logging.</span></span>
5. <span data-ttu-id="38811-320">Karşıdan yükle ve açıklandığı gibi hello günlükleri, değerlendirme [nasıl yapılır: indirme günlükleri](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="38811-320">Download and evaluate hello logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="38811-321"><a name="local-debug"></a>Yerel kimlik doğrulaması ile hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="38811-321"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="38811-322">Uygulamanızı çalıştırabilirsiniz tootest yerel olarak değiştirir toohello bulut yayımlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="38811-322">You can run your application locally tootest changes before publishing them toohello cloud.</span></span> <span data-ttu-id="38811-323">Çoğu Azure Mobile Apps arka uçlarını için basın *F5* while Visual Studio'da.</span><span class="sxs-lookup"><span data-stu-id="38811-323">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="38811-324">Ancak, kimlik doğrulaması kullanılırken ek bazı noktalar vardır.</span><span class="sxs-lookup"><span data-stu-id="38811-324">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="38811-325">Bir bulut tabanlı mobil uygulama ile App Service kimlik doğrulama/yapılandırılmış yetkilendirme olmalıdır ve istemci hello alternatif oturum açma konağı olarak belirtilen hello bulut uç noktası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="38811-325">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have hello cloud endpoint specified as hello alternate login host.</span></span> <span data-ttu-id="38811-326">İstemci platformunuzu gerekli hello belirli adımlar için Hello belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="38811-326">See hello documentation for your client platform for hello specific steps required.</span></span>

<span data-ttu-id="38811-327">Mobil arka sahip olduğundan emin olun [Microsoft.Azure.Mobile.Server.Authentication] yüklü.</span><span class="sxs-lookup"><span data-stu-id="38811-327">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="38811-328">Ardından, sonra hello aşağıdaki uygulamanızın OWIN başlangıç sınıfı ekleyin `MobileAppConfiguration` uygulanan tooyour bırakıldı `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="38811-328">Then, in your application's OWIN startup class, add hello following, after `MobileAppConfiguration` has been applied tooyour `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="38811-329">Örnek önceki hello hello yapılandırmalısınız *authAudience* ve *authIssuer* olması hello HTTPS kullanarak, uygulamanızın kök URL'si tooeach dosya Web.config içindeki uygulama ayarları düzeni.</span><span class="sxs-lookup"><span data-stu-id="38811-329">In hello preceding example, you should configure hello *authAudience* and *authIssuer* application settings within your Web.config file tooeach be the URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="38811-330">Benzer şekilde ayarlamalısınız *authSigningKey* toobe hello değeri, uygulamanızın imzalama anahtarı.</span><span class="sxs-lookup"><span data-stu-id="38811-330">Similarly you should set *authSigningKey* toobe hello value of your application's signing key.</span></span>
<span data-ttu-id="38811-331">tooobtain hello imzalama anahtarı:</span><span class="sxs-lookup"><span data-stu-id="38811-331">tooobtain hello signing key:</span></span>

1. <span data-ttu-id="38811-332">Merhaba içinde tooyour uygulamasına gidin [Azure portalı]</span><span class="sxs-lookup"><span data-stu-id="38811-332">Navigate tooyour app within hello [Azure portal]</span></span>
2. <span data-ttu-id="38811-333">Tıklatın **Araçları**, **Kudu**, **Git**.</span><span class="sxs-lookup"><span data-stu-id="38811-333">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="38811-334">Merhaba Kudu Yönetim sitesini'ı tıklatın **ortam**.</span><span class="sxs-lookup"><span data-stu-id="38811-334">In hello Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="38811-335">Merhaba değeri Bul *Web sitesi\_AUTH\_imzalama\_anahtar*.</span><span class="sxs-lookup"><span data-stu-id="38811-335">Find hello value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="38811-336">İmzalama anahtarı hello için kullanım hello *authSigningKey* , yerel uygulama yapılandırma parametresi.  Mobil arka hangi hello istemci hello belirteci hello bulut tabanlı uç noktasından alacağı yerel olarak çalıştırırken donanımlı toovalidate belirteçleri sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="38811-336">Use hello signing key for hello *authSigningKey* parameter in your local application config.  Your mobile backend is now equipped toovalidate tokens when running locally, which hello client obtains hello token from hello cloud-based endpoint.</span></span>

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
