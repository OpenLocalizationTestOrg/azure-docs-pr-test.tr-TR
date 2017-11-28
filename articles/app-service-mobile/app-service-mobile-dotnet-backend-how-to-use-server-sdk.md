---
title: "Mobil uygulamalar için .NET arka uç sunucusu SDK ile çalışmaya nasıl | Microsoft Docs"
description: "Azure App Service Mobile Apps için .NET arka uç sunucusu SDK ile çalışmayı öğrenin."
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
ms.openlocfilehash: 657fea16e47c15efd262c86d6a150a721476134a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="work-with-the-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="7f410-104">Azure Mobile Apps için .NET arka uç sunucu SDK’sı ile çalışma</span><span class="sxs-lookup"><span data-stu-id="7f410-104">Work with the .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="7f410-105">Bu konuda anahtar Azure App Service Mobile Apps senaryolarda .NET arka uç sunucusu SDK kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="7f410-105">This topic shows you how to use the .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="7f410-106">Azure Mobile Apps SDK'sı, ASP.NET uygulamanız mobil istemcilerden çalışmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7f410-106">The Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="7f410-107">[.NET server için Azure Mobile Apps SDK] [ 2] github'da açık bir kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="7f410-107">The [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="7f410-108">Depo tüm sunucu SDK birim test paketi ve bazı örnek projeler de dahil olmak üzere tüm kaynak kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="7f410-108">The repository contains all source code including the entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="7f410-109">Başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="7f410-109">Reference documentation</span></span>
<span data-ttu-id="7f410-110">SDK sunucusu için başvuru belgeleri burada bulunur: [Azure Mobile Apps .NET başvurusu][1].</span><span class="sxs-lookup"><span data-stu-id="7f410-110">The reference documentation for the server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="7f410-111"><a name="create-app"></a>Nasıl yapılır: bir .NET Mobil uygulama arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f410-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="7f410-112">Yeni bir proje başlıyorsanız, kullanarak bir uygulama hizmeti uygulaması oluşturabilir [Azure portalı] veya Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7f410-112">If you are starting a new project, you can create an App Service application using either the [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="7f410-113">Uygulama hizmeti uygulamayı yerel olarak çalıştırın veya bulut tabanlı uygulama hizmeti mobil uygulamanıza proje yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="7f410-113">You can run the App Service application locally or publish the project to your cloud-based App Service mobile app.</span></span>

<span data-ttu-id="7f410-114">Varolan bir projeye mobil özelliklerini ekliyorsanız, bkz: [indirin ve SDK'sını başlatma](#install-sdk) bölümü.</span><span class="sxs-lookup"><span data-stu-id="7f410-114">If you are adding mobile capabilities to an existing project, see the [Download and initialize the SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-the-azure-portal"></a><span data-ttu-id="7f410-115">Azure Portalı'nı kullanarak bir .NET arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f410-115">Create a .NET backend using the Azure portal</span></span>
<span data-ttu-id="7f410-116">Bir uygulama hizmeti mobil arka uç oluşturmak için aşağıdakilerden birini izleyin [hızlı başlangıç Öğreticisi] [ 3] veya şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7f410-116">To create an App Service mobile backend, either follow the [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="7f410-117">Geri *başlama* dikey altında **tablo API Oluştur**, seçin **C#** olarak, **arka uç dilinizi**.</span><span class="sxs-lookup"><span data-stu-id="7f410-117">Back in the *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="7f410-118">Tıklatın **karşıdan**sıkıştırılmış proje dosyalarını yerel bilgisayarınıza ayıklayın ve Visual Studio çözümü açın.</span><span class="sxs-lookup"><span data-stu-id="7f410-118">Click **Download**, extract the compressed project files to your local computer, and open the solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="7f410-119">Visual Studio 2013 ve Visual Studio 2015 kullanarak bir .NET arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f410-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="7f410-120">Yükleme [.NET için Azure SDK] [ 4] (sürüm 2.9.0 veya sonrası) Visual Studio'da bir Azure Mobile Apps projesi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="7f410-120">Install the [Azure SDK for .NET][4] (version 2.9.0 or later) to create an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="7f410-121">SDK'yı yükledikten sonra aşağıdaki adımları kullanarak bir ASP.NET uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7f410-121">Once you have installed the SDK, create an ASP.NET application using the following steps:</span></span>

1. <span data-ttu-id="7f410-122">Açık **yeni proje** iletişim (gelen *dosya* > **yeni** > **proje...** ).</span><span class="sxs-lookup"><span data-stu-id="7f410-122">Open the **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="7f410-123">Genişletme **şablonları** > **Visual C#**seçip **Web**.</span><span class="sxs-lookup"><span data-stu-id="7f410-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="7f410-124">Seçin **ASP.NET Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="7f410-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="7f410-125">Proje adı girin.</span><span class="sxs-lookup"><span data-stu-id="7f410-125">Fill in the project name.</span></span> <span data-ttu-id="7f410-126">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f410-126">Then click **OK**.</span></span>
5. <span data-ttu-id="7f410-127">Altında *ASP.NET 4.5.2 şablonları*seçin **Azure mobil uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="7f410-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="7f410-128">Denetleme **bulutta Barındır** mobil arka uç bu proje yayımlamak bulutta oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="7f410-128">Check **Host in the cloud** to create a mobile backend in the cloud to which you can publish this project.</span></span>
6. <span data-ttu-id="7f410-129">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f410-129">Click **OK**.</span></span>

## <span data-ttu-id="7f410-130"><a name="install-sdk"></a>Nasıl yapılır: indirme ve SDK'sını başlatma</span><span class="sxs-lookup"><span data-stu-id="7f410-130"><a name="install-sdk"></a>How to: Download and initialize the SDK</span></span>
<span data-ttu-id="7f410-131">SDK kullanılabilir [NuGet.org].</span><span class="sxs-lookup"><span data-stu-id="7f410-131">The SDK is available on [NuGet.org].</span></span> <span data-ttu-id="7f410-132">Bu paket için SDK'sını kullanmaya başlamak için gerekli temel işlevselliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="7f410-132">This package includes the base functionality required to get started using the SDK.</span></span> <span data-ttu-id="7f410-133">SDK'yı başlatmak için üzerinde eylemler gerçekleştirmek gerekir **HttpConfiguration** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7f410-133">To initialize the SDK, you need to perform actions on the **HttpConfiguration** object.</span></span>

### <a name="install-the-sdk"></a><span data-ttu-id="7f410-134">SDK yükle</span><span class="sxs-lookup"><span data-stu-id="7f410-134">Install the SDK</span></span>
<span data-ttu-id="7f410-135">SDK yüklemek için sunucu projesi Visual Studio'da seçin sağ tıklayın **NuGet paketlerini Yönet**, arama [Microsoft.Azure.Mobile.Server] paketini ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="7f410-135">To install the SDK, right-click on the server project in Visual Studio, select **Manage NuGet Packages**, search for the [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="7f410-136"><a name="server-project-setup"></a>Sunucu projesi başlatma</span><span class="sxs-lookup"><span data-stu-id="7f410-136"><a name="server-project-setup"></a> Initialize the server project</span></span>
<span data-ttu-id="7f410-137">Bir .NET arka uç sunucu projesi benzer diğer ASP.NET projeleri için OWIN başlangıç sınıfı dahil ederek başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="7f410-137">A .NET backend server project is initialized similar to other ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="7f410-138">NuGet paketi başvurulan olun `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="7f410-138">Ensure that you have referenced the NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="7f410-139">Visual Studio'da bu sınıf eklemek için sunucu projenize sağ tıklayın ve seçin **Ekle** >
**yeni öğe**, ardından **Web** > **genel** > **OWIN başlangıç sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="7f410-139">To add this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="7f410-140">Bir sınıf aşağıdaki öznitelik oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="7f410-140">A class is generated with the following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="7f410-141">İçinde `Configuration()` yöntemi, OWIN başlangıç sınıfı, kullanım, bir **HttpConfiguration** Azure Mobile Apps ortamını yapılandırma nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7f410-141">In the `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object to configure the Azure Mobile Apps environment.</span></span>
<span data-ttu-id="7f410-142">Aşağıdaki örnek, hiçbir ek özellikler içeren sunucu projesi başlatır:</span><span class="sxs-lookup"><span data-stu-id="7f410-142">The following example initializes the server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="7f410-143">Tek tek özellikleri etkinleştirmek için genişletme yöntemleri üzerinde çağırmalısınız **MobileAppConfiguration** nesne çağırmadan önce **ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="7f410-143">To enable individual features, you must call extension methods on the **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="7f410-144">Örneğin, aşağıdaki kod özniteliğine sahip tüm API denetleyicilerinin varsayılan yolların ekler `[MobileAppController]` başlatma sırasında:</span><span class="sxs-lookup"><span data-stu-id="7f410-144">For example, the following code adds the default routes to all API controllers that have the attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="7f410-145">Azure portal aramalardan server Hızlı Başlangıç **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="7f410-145">The server quickstart from the Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="7f410-146">Aşağıdaki Kurulum bu eşdeğerdir:</span><span class="sxs-lookup"><span data-stu-id="7f410-146">This equivalent to the following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from the Home package
            .MapApiControllers()
            .AddTables(                               // from the Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from the Entity package
                )
            .AddPushNotifications()                   // from the Notifications package
            .MapLegacyCrossDomainController()         // from the CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="7f410-147">Kullanılan genişletme yöntemleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7f410-147">The extension methods used are:</span></span>

* <span data-ttu-id="7f410-148">`AddMobileAppHomeController()`Varsayılan Azure Mobile Apps giriş sayfası sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f410-148">`AddMobileAppHomeController()` provides the default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="7f410-149">`MapApiControllers()`Webapı denetleyicileri ile donatılmış özel API yetenekleri sağlar `[MobileAppController]` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="7f410-149">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with the `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="7f410-150">`AddTables()`bir eşlenmesini sağlar `/tables` tablo denetleyicilerine uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="7f410-150">`AddTables()` provides a mapping of the `/tables` endpoints to table controllers.</span></span>
* <span data-ttu-id="7f410-151">`AddTablesWithEntityFramework()`bir kısaltılmış eşlemesi için olan `/tables` Entity Framework kullanarak uç noktaları alarak denetleyicileri.</span><span class="sxs-lookup"><span data-stu-id="7f410-151">`AddTablesWithEntityFramework()` is a short-hand for mapping the `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="7f410-152">`AddPushNotifications()`Bildirim hub'ları için cihazları kaydetme, basit bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f410-152">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="7f410-153">`MapLegacyCrossDomainController()`Standart CORS üstbilgilerini yerel geliştirme için sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f410-153">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="7f410-154">SDK uzantıları</span><span class="sxs-lookup"><span data-stu-id="7f410-154">SDK extensions</span></span>
<span data-ttu-id="7f410-155">Aşağıdaki NuGet tabanlı uzantısı paketleri, uygulamanız tarafından kullanılabilen çeşitli mobil özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f410-155">The following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="7f410-156">Kullanarak başlatma sırasında uzantılarını etkinleştirme **MobileAppConfiguration** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7f410-156">You enable extensions during initialization by using the **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="7f410-157">[Microsoft.Azure.Mobile.Server.Quickstart] temel Mobile Apps Kurulumu destekler.</span><span class="sxs-lookup"><span data-stu-id="7f410-157">[Microsoft.Azure.Mobile.Server.Quickstart] Supports the basic Mobile Apps setup.</span></span> <span data-ttu-id="7f410-158">Çağırarak yapılandırmaya eklenmiş **UseDefaultConfiguration** başlatma sırasında genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7f410-158">Added to the configuration by calling the **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="7f410-159">Bu uzantı uzantıları aşağıdaki içerir: bildirimleri, kimlik doğrulama, varlık, tablolar, etki alanları arası ve giriş paketleri.</span><span class="sxs-lookup"><span data-stu-id="7f410-159">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="7f410-160">Bu paket, Azure portalında kullanılabilir Mobile Apps Quickstart tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7f410-160">This package is used by the Mobile Apps Quickstart available on the Azure portal.</span></span>
* <span data-ttu-id="7f410-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) varsayılan uygulayan *bu mobil uygulamayı çalışır durumda olduğundan sayfa* bir web sitesi kök.</span><span class="sxs-lookup"><span data-stu-id="7f410-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements the default *this mobile app is up and running page* for the web site root.</span></span> <span data-ttu-id="7f410-162">Yapılandırmaya çağırarak eklemek **AddMobileAppHomeController** genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7f410-162">Add to the configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="7f410-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) verilerle çalışmak için sınıflar içerir ve veri ardışık kümeleri yukarı.</span><span class="sxs-lookup"><span data-stu-id="7f410-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up the data pipeline.</span></span> <span data-ttu-id="7f410-164">Yapılandırmaya çağırarak eklemek **AddTables** genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7f410-164">Add to the configuration by calling the **AddTables** extension method.</span></span>
* <span data-ttu-id="7f410-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) SQL veritabanındaki verilere erişmek Entity Framework sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f410-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables the Entity Framework to access data in the SQL Database.</span></span> <span data-ttu-id="7f410-166">Yapılandırmaya çağırarak eklemek **AddTablesWithEntityFramework** genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7f410-166">Add to the configuration by calling the **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="7f410-167">[Microsoft.Azure.Mobile.Server.Authentication] kimlik doğrulaması sağlar ve ayarlar yukarı belirteçleri doğrulamak için kullanılan OWIN ara yazılımı.</span><span class="sxs-lookup"><span data-stu-id="7f410-167">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up the OWIN middleware used to validate tokens.</span></span> <span data-ttu-id="7f410-168">Yapılandırmaya çağırarak eklemek **AddAppServiceAuthentication** ve **Iappbuilder**. **UseAppServiceAuthentication** genişletme yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="7f410-168">Add to the configuration by calling the **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="7f410-169">[Microsoft.Azure.Mobile.Server.Notifications] anında iletme bildirimleri ve anında iletme kayıt uç noktasını tanımlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f410-169">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="7f410-170">Yapılandırmaya çağırarak eklemek **AddPushNotifications** genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7f410-170">Add to the configuration by calling the **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="7f410-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) verilerini mobil uygulamanızdan eski tarayıcılar için hizmet veren bir denetleyiciyi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7f410-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data to legacy web browsers from your Mobile App.</span></span> <span data-ttu-id="7f410-172">Yapılandırmaya çağırarak eklemek **MapLegacyCrossDomainController** genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7f410-172">Add to the configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="7f410-173">[Microsoft.Azure.Mobile.Server.Login] özel kimlik doğrulama senaryoları sırasında kullanılan bir statik yöntem AppServiceLoginHandler.CreateToken() yöntemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f410-173">[Microsoft.Azure.Mobile.Server.Login] Provides the AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="7f410-174"><a name="publish-server-project"></a>Nasıl yapılır: Sunucu projesi yayımlama</span><span class="sxs-lookup"><span data-stu-id="7f410-174"><a name="publish-server-project"></a>How to: Publish the server project</span></span>
<span data-ttu-id="7f410-175">Bu bölümde, .NET arka uç projeniz Visual Studio'dan yayımlamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="7f410-175">This section shows you how to publish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="7f410-176">Arka uç projeniz Git kullanarak da dağıtabilir veya diğer yöntemlerden herhangi birini ele [Azure uygulama hizmeti dağıtım belgeleri](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7f410-176">You can also deploy your backend project using Git or any of the other methods covered in the [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="7f410-177">Visual Studio'da NuGet paketlerini geri yüklemek için projeyi yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f410-177">In Visual Studio, rebuild the project to restore NuGet packages.</span></span>
2. <span data-ttu-id="7f410-178">Çözüm Gezgini'nde projeye sağ tıklayın, **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="7f410-178">In Solution Explorer, right-click the project, click **Publish**.</span></span> <span data-ttu-id="7f410-179">İlk yayımladığınızda, yayımlama profili tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f410-179">The first time you publish, you need to define a publishing profile.</span></span> <span data-ttu-id="7f410-180">Önceden tanımlı bir profili varsa, seçin ve tıklatın **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="7f410-180">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="7f410-181">Yayımlama hedefi seçmek için sorulursa tıklatın **Microsoft Azure App Service** > **sonraki**, sonra (gerekirse) ile Azure kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7f410-181">If asked to select a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="7f410-182">Visual Studio indirmeleri ve güvenli bir şekilde depolar, doğrudan Azure ayarlarını yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="7f410-182">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="7f410-183">Seçin, **abonelik**seçin **kaynak türü** gelen **Görünüm**, genişletin **mobil uygulama**ve mobil uygulama arka tıklayın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7f410-183">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="7f410-184">Yayımlama profili bilgilerini doğrulayın ve tıklatın **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="7f410-184">Verify the publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="7f410-185">Mobil uygulama arka başarıyla yayımladı, başarıyı gösteren bir giriş sayfasına bakın.</span><span class="sxs-lookup"><span data-stu-id="7f410-185">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="7f410-186"><a name="define-table-controller"></a>Nasıl yapılır: bir tablo denetleyicisi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="7f410-186"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="7f410-187">Mobil istemcilerin bir SQL tablosuna kullanıma sunmak için bir tablo denetleyicisi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="7f410-187">Define a Table Controller to expose a SQL table to mobile clients.</span></span>  <span data-ttu-id="7f410-188">Bir tablo denetleyicisi yapılandırma üç adımı gerektirir:</span><span class="sxs-lookup"><span data-stu-id="7f410-188">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="7f410-189">Bir veri aktarım nesnesini (DTO) sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f410-189">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="7f410-190">Bir tablo başvurusu mobil DbContext sınıfında yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7f410-190">Configure a table reference in the Mobile DbContext class.</span></span>
3. <span data-ttu-id="7f410-191">Bir tablo denetleyicisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f410-191">Create a table controller.</span></span>

<span data-ttu-id="7f410-192">Bir veri aktarım nesnesini (DTO) öğesinden devralınan bir düz C# nesnesidir `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="7f410-192">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="7f410-193">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7f410-193">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="7f410-194">DTO tablo SQL veritabanı içinde tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7f410-194">The DTO is used to define the table within the SQL database.</span></span>  <span data-ttu-id="7f410-195">Veritabanı girişi oluşturmak için Ekle bir `DbSet<>` kullanmakta olduğunuz DbContext özelliğine.</span><span class="sxs-lookup"><span data-stu-id="7f410-195">To create the database entry, add a `DbSet<>` property to the DbContext you are using.</span></span>  <span data-ttu-id="7f410-196">Azure Mobile Apps için varsayılan proje şablonu DbContext adlı `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="7f410-196">In the default project template for Azure Mobile Apps, the DbContext is called `Models\MobileServiceContext.cs`:</span></span>

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

<span data-ttu-id="7f410-197">Azure SDK'sı yüklü varsa, artık bir şablon tablo denetleyicisi aşağıdaki gibi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7f410-197">If you have the Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="7f410-198">Denetleyicileri klasörü sağ tıklatın ve seçin **Ekle** > **denetleyicisi...** .</span><span class="sxs-lookup"><span data-stu-id="7f410-198">Right-click on the Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="7f410-199">Seçin **Azure Mobile Apps tablo denetleyicisi** seçeneğini ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="7f410-199">Select the **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="7f410-200">İçinde **denetleyici Ekle** iletişim:</span><span class="sxs-lookup"><span data-stu-id="7f410-200">In the **Add Controller** dialog:</span></span>
   * <span data-ttu-id="7f410-201">İçinde **Model sınıfı** açılan listesinde, yeni DTO seçin.</span><span class="sxs-lookup"><span data-stu-id="7f410-201">In the **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="7f410-202">İçinde **DbContext** açılan listesinde, mobil hizmet DbContext sınıfı seçin.</span><span class="sxs-lookup"><span data-stu-id="7f410-202">In the **DbContext** dropdown, select the Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="7f410-203">Denetleyici adı sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7f410-203">The Controller name is created for you.</span></span>
4. <span data-ttu-id="7f410-204">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f410-204">Click **Add**.</span></span>

<span data-ttu-id="7f410-205">Basit bir örneğin hızlı başlangıç sunucu projesi içeren **TodoItemController**.</span><span class="sxs-lookup"><span data-stu-id="7f410-205">The quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="7f410-206"><a name="adjust-pagesize"></a>Nasıl yapılır: Tablo disk belleği boyutunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="7f410-206"><a name="adjust-pagesize"></a>How to: Adjust the table paging size</span></span>
<span data-ttu-id="7f410-207">Varsayılan olarak, Azure Mobile Apps istek başına 50 kayıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="7f410-207">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="7f410-208">Disk belleği, istemci kendi kullanıcı Arabirimi iş parçacığı veya çok uzun bir süre için sunucunun yukarı iyi bir kullanıcı deneyimi sağlayarak tie değil, sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f410-208">Paging ensures that the client does not tie up their UI thread nor the server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="7f410-209">Tablo disk belleği boyutunu değiştirmek için "izin verilen sorgu boyutu" sunucu tarafı artırmak ve istemci tarafı sayfa boyutu sunucu tarafı "sorgu boyutu izin verilen" olarak ayarlandı kullanarak `EnableQuery` özniteliği:</span><span class="sxs-lookup"><span data-stu-id="7f410-209">To change the table paging size, increase the server side "allowed query size" and the client-side page size The server side "allowed query size" is adjusted using the `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="7f410-210">PageSize aynı olduğundan emin olun veya istemci tarafından istenilen boyuttan büyük.</span><span class="sxs-lookup"><span data-stu-id="7f410-210">Ensure the PageSize is the same or larger than the size requested by the client.</span></span>  <span data-ttu-id="7f410-211">Belirli istemci istemci sayfa boyutunu değiştirme hakkında ayrıntılar için nasıl yapılır belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="7f410-211">Refer to the specific client HOWTO documentation for details on changing the client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="7f410-212">Nasıl yapılır: özel bir API denetleyicisi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="7f410-212">How to: Define a custom API controller</span></span>
<span data-ttu-id="7f410-213">Özel API denetleyicisi bir uç nokta göstererek, mobil uygulamanızın arka ucuna en temel işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f410-213">The custom API controller provides the most basic functionality to your Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="7f410-214">[MobileAppController] özniteliği kullanılarak mobile özgü API denetleyicisi kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f410-214">You can register a mobile-specific API controller using the [MobileAppController] attribute.</span></span> <span data-ttu-id="7f410-215">`MobileAppController` Özniteliği rota kaydeder, Mobile Apps JSON seri hale getirici ayarlar ve açar [istemci sürüm denetimi](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="7f410-215">The `MobileAppController` attribute registers the route, sets up the Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="7f410-216">Visual Studio'da denetleyicileri klasörüne sağ tıklayın ve ardından **Ekle** > **denetleyicisi**seçin **Web API 2 denetleyicisi&mdash;boş** tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="7f410-216">In Visual Studio, right-click the Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="7f410-217">Tedarik bir **Denetleyici adı**, gibi `CustomController`, tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="7f410-217">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="7f410-218">Yeni denetleyici sınıf dosyasında, aşağıdaki ekleme deyimini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="7f410-218">In the new controller class file, add the following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="7f410-219">Uygulama **[MobileAppController]** özniteliği aşağıdaki örnekte olduğu gibi API denetleyicisi sınıfı tanımı:</span><span class="sxs-lookup"><span data-stu-id="7f410-219">Apply the **[MobileAppController]** attribute to the API controller class definition, as in the following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="7f410-220">App_Start/Startup.MobileApp.cs dosyasında bir çağrı ekleyin **MapApiControllers** genişletme yöntemi, aşağıdaki örnekteki gibi:</span><span class="sxs-lookup"><span data-stu-id="7f410-220">In App_Start/Startup.MobileApp.cs file, add a call to the **MapApiControllers** extension method, as in the following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="7f410-221">Aynı zamanda `UseDefaultConfiguration()` genişletme yöntemi yerine `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="7f410-221">You can also use the `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="7f410-222">Sahip olmadığı herhangi bir denetleyicisi **MobileAppControllerAttribute** uygulanan hala istemcileri tarafından erişilebilen, ancak bunu doğru şekilde herhangi bir mobil uygulama istemci SDK kullanan istemciler tarafından tüketilmeyen.</span><span class="sxs-lookup"><span data-stu-id="7f410-222">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="7f410-223">Nasıl yapılır: kimlik doğrulaması ile çalışma</span><span class="sxs-lookup"><span data-stu-id="7f410-223">How to: Work with authentication</span></span>
<span data-ttu-id="7f410-224">Azure Mobile Apps kullanan App Service kimlik doğrulama / yetkilendirme, mobil arka uç güvenli hale getirmek için.</span><span class="sxs-lookup"><span data-stu-id="7f410-224">Azure Mobile Apps uses App Service Authentication / Authorization to secure your mobile backend.</span></span>  <span data-ttu-id="7f410-225">Bu bölümde aşağıdaki kimlik doğrulama ile ilgili görevlerin .NET arka uç sunucu projenizi nasıl gerçekleştirileceğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="7f410-225">This section shows you how to perform the following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="7f410-226">Nasıl yapılır: bir sunucu projesi için kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="7f410-226">How to: Add authentication to a server project</span></span>](#add-auth)
* [<span data-ttu-id="7f410-227">Nasıl yapılır: uygulamanız için özel kimlik doğrulamasını kullan</span><span class="sxs-lookup"><span data-stu-id="7f410-227">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="7f410-228">Nasıl yapılır: alma kimliği doğrulanmış kullanıcı bilgileri</span><span class="sxs-lookup"><span data-stu-id="7f410-228">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="7f410-229">Nasıl yapılır: yetkili kullanıcıların veri erişimini kısıtlamak</span><span class="sxs-lookup"><span data-stu-id="7f410-229">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="7f410-230"><a name="add-auth"></a>Nasıl yapılır: bir sunucu projesi için kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="7f410-230"><a name="add-auth"></a>How to: Add authentication to a server project</span></span>
<span data-ttu-id="7f410-231">Kimlik doğrulama sunucu projenizi genişleterek ekleyebileceğiniz **MobileAppConfiguration** nesne ve OWIN ara yazılımı yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="7f410-231">You can add authentication to your server project by extending the **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="7f410-232">Yüklediğinizde [Microsoft.Azure.Mobile.Server.Quickstart] paket ve çağrısı **UseDefaultConfiguration** genişletme yöntemi, 3. adıma atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f410-232">When you install the [Microsoft.Azure.Mobile.Server.Quickstart] package and call the **UseDefaultConfiguration** extension method, you can skip to step 3.</span></span>

1. <span data-ttu-id="7f410-233">Visual Studio'da yükleme [Microsoft.Azure.Mobile.Server.Authentication] paket.</span><span class="sxs-lookup"><span data-stu-id="7f410-233">In Visual Studio, install the [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="7f410-234">Haline proje dosyasında başında aşağıdaki kod satırını ekleyin **yapılandırma** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7f410-234">In the Startup.cs project file, add the following line of code at the beginning of the **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="7f410-235">Bu OWIN ara yazılım bileşeni ilişkili uygulama hizmeti ağ geçidi tarafından yayınlanan belirteçleri doğrular.</span><span class="sxs-lookup"><span data-stu-id="7f410-235">This OWIN middleware component validates tokens issued by the associated App Service gateway.</span></span>
3. <span data-ttu-id="7f410-236">Ekleme `[Authorize]` özniteliği herhangi bir denetleyici veya kimlik doğrulama gerektiren yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7f410-236">Add the `[Authorize]` attribute to any controller or method that requires authentication.</span></span>

<span data-ttu-id="7f410-237">Mobile Apps arka istemcilerin kimliğini doğrulamak nasıl hakkında bilgi edinmek için [uygulamanıza kimlik doğrulaması ekleme](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="7f410-237">To learn about how to authenticate clients to your Mobile Apps backend, see [Add authentication to your app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="7f410-238"><a name="custom-auth"></a>Nasıl yapılır: uygulamanız için özel kimlik doğrulamasını kullan</span><span class="sxs-lookup"><span data-stu-id="7f410-238"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="7f410-239">App Service kimlik doğrulama/yetkilendirme sağlayıcılardan biri kullanmak istemiyorsanız, kendi oturum açma sistem uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f410-239">If you do not wish to use one of the App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="7f410-240">Yükleme [Microsoft.Azure.Mobile.Server.Login] ile kimlik doğrulama belirteci oluşturma yardımcı olmak üzere paket.</span><span class="sxs-lookup"><span data-stu-id="7f410-240">Install the [Microsoft.Azure.Mobile.Server.Login] package to assist with authentication token generation.</span></span>  <span data-ttu-id="7f410-241">Kullanıcı kimlik bilgilerini doğrulamak için kendi kodunuzu girin.</span><span class="sxs-lookup"><span data-stu-id="7f410-241">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="7f410-242">Örneğin, güvenlik ve karma parolaları bir veritabanında karşı denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f410-242">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="7f410-243">Aşağıdaki örnekte `isValidAssertion()` yöntemi (başka bir yerde tanımlanır) için bu denetimleri sorumlu.</span><span class="sxs-lookup"><span data-stu-id="7f410-243">In the example below, the `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="7f410-244">Özel kimlik doğrulama bir ApiController oluşturma ve gösterme sunulan `register` ve `login` eylemler.</span><span class="sxs-lookup"><span data-stu-id="7f410-244">The custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="7f410-245">İstemci, kullanıcıdan bilgi toplamak için özel bir kullanıcı Arabirimi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f410-245">The client should use a custom UI to collect the information from the user.</span></span>  <span data-ttu-id="7f410-246">Bilgi, standart HTTP POST çağrısıyla API sonra gönderilir.</span><span class="sxs-lookup"><span data-stu-id="7f410-246">The information is then submitted to the API with a standard HTTP POST call.</span></span> <span data-ttu-id="7f410-247">Onaylama işlemi sunucuyu doğrular sonra bir belirteç kullanarak verilen `AppServiceLoginHandler.CreateToken()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7f410-247">Once the server validates the assertion, a token is issued using the `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="7f410-248">ApiController **vermemelisiniz** kullanmak `[MobileAppController]` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="7f410-248">The ApiController **should not** use the `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="7f410-249">Örnek `login` eylem:</span><span class="sxs-lookup"><span data-stu-id="7f410-249">An example `login` action:</span></span>

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

<span data-ttu-id="7f410-250">Önceki örnekte LoginResult ve LoginResultUser gerekli özellikleri gösterme seri hale getirilebilir nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="7f410-250">In the preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="7f410-251">İstemci oturum açma yanıt biçiminde JSON nesneler olarak döndürülecek bekler:</span><span class="sxs-lookup"><span data-stu-id="7f410-251">The client expects login responses to be returned as JSON objects of the form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="7f410-252">`AppServiceLoginHandler.CreateToken()` Yöntemi içeren bir *İzleyici* ve bir *veren* parametresi.</span><span class="sxs-lookup"><span data-stu-id="7f410-252">The `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="7f410-253">Bu parametrelerin her ikisini de HTTPS şeması kullanarak URL'ye, uygulamanızın kök ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="7f410-253">Both of these parameters are set to the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="7f410-254">Benzer şekilde ayarlamalısınız *secretKey* uygulamanızı değerini anahtar imzalama kullanıcının olması.</span><span class="sxs-lookup"><span data-stu-id="7f410-254">Similarly you should set *secretKey* to be the value of your application's signing key.</span></span> <span data-ttu-id="7f410-255">Anahtarları Naneli ve kullanıcıları taklit etmek için kullanılabilir olarak bir istemci imzalama anahtarı dağıtmayın.</span><span class="sxs-lookup"><span data-stu-id="7f410-255">Do not distribute the signing key in a client as it can be used to mint keys and impersonate users.</span></span> <span data-ttu-id="7f410-256">App Service içinde başvurarak barındırılan sırada imzalama anahtarı edinebilirsiniz *Web sitesi\_AUTH\_imzalama\_anahtar* ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="7f410-256">You can obtain the signing key while hosted in App Service by referencing the *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="7f410-257">Yerel hata ayıklama bağlamda gerekirse'ndaki yönergeleri izleyin [yerel kimlik doğrulaması ile hata ayıklama](#local-debug) anahtarı almak ve bir uygulama ayarı olarak depolamak için bölüm.</span><span class="sxs-lookup"><span data-stu-id="7f410-257">If needed in a local debugging context, follow the instructions in the [Local debugging with authentication](#local-debug) section to retrieve the key and store it as an application setting.</span></span>

<span data-ttu-id="7f410-258">Verilen belirteç, ayrıca diğer talepleri ve sona erme tarihi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="7f410-258">The issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="7f410-259">Verilen belirteç en azından bir konu içermelidir (**alt**) talep.</span><span class="sxs-lookup"><span data-stu-id="7f410-259">Minimally, the issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="7f410-260">Standart istemci destekleyebilir `loginAsync()` tarafından kimlik doğrulaması rota aşırı yükleme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7f410-260">You can support the standard client `loginAsync()` method by overloading the authentication route.</span></span>  <span data-ttu-id="7f410-261">İstemci çağırırsa `client.loginAsync('custom');` oturum açmak için yönlendirme olmalı `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="7f410-261">If the client calls `client.loginAsync('custom');` to log in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="7f410-262">Özel kimlik doğrulama kullanarak denetleyici için rota ayarlayabilirsiniz `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="7f410-262">You can set the route for the custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="7f410-263">Kullanarak `loginAsync()` yaklaşım sağlar sonraki her çağrı için hizmet kimlik doğrulama belirteci eklenir.</span><span class="sxs-lookup"><span data-stu-id="7f410-263">Using the `loginAsync()` approach ensures that the authentication token is attached to every subsequent call to the service.</span></span>
>
>

### <span data-ttu-id="7f410-264"><a name="user-info"></a>Nasıl yapılır: alma kimliği doğrulanmış kullanıcı bilgileri</span><span class="sxs-lookup"><span data-stu-id="7f410-264"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="7f410-265">App Service tarafından bir kullanıcı kimlik doğrulaması yapıldığında .NET arka uç kodunuzun atanan kullanıcı Kimliğini ve diğer bilgilere erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f410-265">When a user is authenticated by App Service, you can access the assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="7f410-266">Kullanıcı bilgilerini arka yetkilendirme kararları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7f410-266">The user information can be used for making authorization decisions in the backend.</span></span> <span data-ttu-id="7f410-267">Aşağıdaki kod, bir istekle ilişkili kullanıcı kimliği alır:</span><span class="sxs-lookup"><span data-stu-id="7f410-267">The following code obtains the user ID associated with a request:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="7f410-268">SID, sağlayıcıya özgü kullanıcı ID'den türetilmiş ve verilen kullanıcı ve oturum açma sağlayıcısı için statiktir.</span><span class="sxs-lookup"><span data-stu-id="7f410-268">The SID is derived from the provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="7f410-269">SID için geçersiz kimlik doğrulama belirteçleri null şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="7f410-269">The SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="7f410-270">Uygulama Hizmeti ayrıca oturum açma sağlayıcınızdan belirli talep istemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="7f410-270">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="7f410-271">Her bir kimlik sağlayıcısı kimlik sağlayıcısı SDK kullanarak daha fazla bilgi sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="7f410-271">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="7f410-272">Örneğin, Facebook grafik API'si arkadaş bilgilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f410-272">For example, you can use the Facebook Graph API for friends information.</span></span>  <span data-ttu-id="7f410-273">Azure portalında sağlayıcısı dikey penceresinde istenen taleplerin belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f410-273">You can specify claims that are requested in the provider blade in the Azure portal.</span></span> <span data-ttu-id="7f410-274">Bazı talep kimlik sağlayıcısı ile ek yapılandırma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7f410-274">Some claims require additional configuration with the identity provider.</span></span>

<span data-ttu-id="7f410-275">Aşağıdaki kod çağrıları **GetAppServiceIdentityAsync** erişim dahil oturum açma kimlik bilgileri belirteci almak için genişletme yöntemi gerekli Facebook grafik API'si istekler yapmak:</span><span class="sxs-lookup"><span data-stu-id="7f410-275">The following code calls the **GetAppServiceIdentityAsync** extension method to get the login credentials, which include the access token needed to make requests against the Facebook Graph API:</span></span>

    // Get the credentials for the logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with the Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request the current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with the Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="7f410-276">Kullanarak bir ekleme deyimi için `System.Security.Principal` sağlamak için **GetAppServiceIdentityAsync** genişletme yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7f410-276">Add a using statement for `System.Security.Principal` to provide the **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="7f410-277"><a name="authorize"></a>Nasıl yapılır: yetkili kullanıcıların veri erişimini kısıtlamak</span><span class="sxs-lookup"><span data-stu-id="7f410-277"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="7f410-278">Önceki bölümde biz kimliği doğrulanmış bir kullanıcı kullanıcı Kimliğini almak nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7f410-278">In the previous section, we showed how to retrieve the user ID of an authenticated user.</span></span> <span data-ttu-id="7f410-279">Veri ve bu değere göre diğer kaynaklara erişimi kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f410-279">You can restrict access to data and other resources based on this value.</span></span> <span data-ttu-id="7f410-280">Örneğin, bir kullanıcı kimliği sütunu tablolarına ekleme ve kullanıcı Kimliğine göre sorgu sonuçlarını filtreleme döndürülen verilerin yalnızca yetkili kullanıcılara sınırlamak için bir basit yoludur.</span><span class="sxs-lookup"><span data-stu-id="7f410-280">For example, adding a userId column to tables and filtering the query results by the user ID is a simple way to limit returned data only to authorized users.</span></span> <span data-ttu-id="7f410-281">Yalnızca SID Todoıtem tablosu üzerinde UserID sütunundaki değeri eşleştiğinde aşağıdaki kod veri satırlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="7f410-281">The following code returns data rows only when the SID matches the value in the UserId column on the TodoItem table:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong to the current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="7f410-282">`Query()` Yöntemi döndürür bir `IQueryable` filtreleme işlemek için LINQ tarafından yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="7f410-282">The `Query()` method returns an `IQueryable` that can be manipulated by LINQ to handle filtering.</span></span>

## <a name="how-to-add-push-notifications-to-a-server-project"></a><span data-ttu-id="7f410-283">Nasıl yapılır: anında iletme eklemek sunucu projesi bildirimleri</span><span class="sxs-lookup"><span data-stu-id="7f410-283">How to: Add push notifications to a server project</span></span>
<span data-ttu-id="7f410-284">Genişleterek sunucu projenizi anında iletme bildirimleri ekleme **MobileAppConfiguration** nesne ve bildirim hub'ları istemci oluşturma.</span><span class="sxs-lookup"><span data-stu-id="7f410-284">Add push notifications to your server project by extending the **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="7f410-285">Visual Studio'da sunucu projesi sağ tıklatın ve **NuGet paketlerini Yönet**, arama `Microsoft.Azure.Mobile.Server.Notifications`, ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="7f410-285">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="7f410-286">Yüklemek için bu adımı yineleyin `Microsoft.Azure.NotificationHubs` bildirim hub'ları istemci kitaplığı içeren paket.</span><span class="sxs-lookup"><span data-stu-id="7f410-286">Repeat this step to install the `Microsoft.Azure.NotificationHubs` package, which includes the Notification Hubs client library.</span></span>
3. <span data-ttu-id="7f410-287">App_Start/Startup.MobileApp.cs içinde ve bir çağrı ekleyin **AddPushNotifications()** genişletme yöntemi başlatma sırasında:</span><span class="sxs-lookup"><span data-stu-id="7f410-287">In App_Start/Startup.MobileApp.cs, and add a call to the **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="7f410-288">Bildirim hub'ları istemci oluşturur aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7f410-288">Add the following code that creates a Notification Hubs client:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="7f410-289">Kayıtlı cihazlara anında iletme bildirimleri göndermek için Notification Hubs istemci artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f410-289">You can now use the Notification Hubs client to send push notifications to registered devices.</span></span> <span data-ttu-id="7f410-290">Daha fazla bilgi için bkz: [uygulamanıza anında iletme bildirimleri ekleme](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="7f410-290">For more information, see [Add push notifications to your app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="7f410-291">Notification Hubs hakkında daha fazla bilgi için bkz: [Notification Hubs'a genel bakış](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7f410-291">To learn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="7f410-292"><a name="tags"></a>Nasıl yapılır: etkinleştir hedeflenen etiketleri kullanarak anında iletme</span><span class="sxs-lookup"><span data-stu-id="7f410-292"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="7f410-293">Bildirim hub'ları etiketleri kullanarak belirli kayıtlar için hedeflenen bildirimleri göndermenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="7f410-293">Notification Hubs lets you send targeted notifications to specific registrations by using tags.</span></span> <span data-ttu-id="7f410-294">Birkaç etiket otomatik olarak oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="7f410-294">Several tags are created automatically:</span></span>

* <span data-ttu-id="7f410-295">Belirli bir aygıt yükleme kimliği tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7f410-295">The Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="7f410-296">Belirli bir kullanıcı kimliği doğrulanmış SID tabanlı kullanıcı kimliği tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7f410-296">The User Id based on the authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="7f410-297">Kimliği erişilebilir gelen yükleme **InstallationID** özelliği **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="7f410-297">The installation ID can be accessed from the **installationId** property on the **MobileServiceClient**.</span></span>  <span data-ttu-id="7f410-298">Aşağıdaki örnek, bildirim hub'ları belirli bir yüklemede bir etiket eklemek için bir yükleme kimliği kullanmayı gösterir:</span><span class="sxs-lookup"><span data-stu-id="7f410-298">The following example shows how to use an installation ID to add a tag to a specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="7f410-299">Anında iletme bildirimi kaydı sırasında istemci tarafından sağlanan herhangi bir etiket arka ucu tarafından yükleme oluştururken göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="7f410-299">Any tags supplied by the client during push notification registration are ignored by the backend when creating the installation.</span></span> <span data-ttu-id="7f410-300">Etiketler yüklemesine eklemek bir istemci etkinleştirmek için önceki desenini kullanarak etiketleri ekler özel bir API oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f410-300">To enable a client to add tags to the installation, you must create a custom API that adds tags using the preceding pattern.</span></span>

<span data-ttu-id="7f410-301">Bkz: [istemci eklenen anında iletme bildirimi etiketleri] [ 5] App Service Mobile Apps tamamlanmış hızlı başlangıç örnek bir örnek.</span><span class="sxs-lookup"><span data-stu-id="7f410-301">See [Client-added push notification tags][5] in the App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="7f410-302"><a name="push-user"></a>Nasıl yapılır: kimliği doğrulanmış bir kullanıcı için anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="7f410-302"><a name="push-user"></a>How to: Send push notifications to an authenticated user</span></span>
<span data-ttu-id="7f410-303">Kimliği doğrulanmış bir kullanıcı için anında iletme bildirimleri kaydolduğunda, bir kullanıcı kimliği etiketi kayıt için otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="7f410-303">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="7f410-304">Bu etiket kullanarak, söz konusu kişi tarafından kaydedilen tüm cihazlara anında iletme bildirimleri gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f410-304">By using this tag, you can send push notifications to all devices registered by that person.</span></span> <span data-ttu-id="7f410-305">Aşağıdaki kod, isteği yapan kullanıcı SID'si alır ve bu kişi için her aygıt kaydı için bir şablon anında iletme bildirimi gönderir:</span><span class="sxs-lookup"><span data-stu-id="7f410-305">The following code gets the SID of user making the request and sends a template push notification to every device registration for that person:</span></span>

    // Get the current user SID and create a tag for the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for the template with the item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification to the user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="7f410-306">Kimliği doğrulanmış bir istemci anında iletme bildirimleri için kaydolurken kayıt denemeden önce kimlik doğrulamasının tam olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7f410-306">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="7f410-307">Daha fazla bilgi için bkz: [kullanıcılara anında iletme] [ 6] .NET arka ucu App Service Mobile Apps tamamlanmış hızlı başlangıç örnek.</span><span class="sxs-lookup"><span data-stu-id="7f410-307">For more information, see [Push to users][6] in the App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-the-net-server-sdk"></a><span data-ttu-id="7f410-308">Nasıl yapılır: hata ayıklama ve .NET sunucusu SDK'sı sorun giderme</span><span class="sxs-lookup"><span data-stu-id="7f410-308">How to: Debug and troubleshoot the .NET Server SDK</span></span>
<span data-ttu-id="7f410-309">Azure uygulama hizmeti birkaç hata ayıklama ve sorun giderme teknikleri ASP.NET uygulamaları için sağlar:</span><span class="sxs-lookup"><span data-stu-id="7f410-309">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="7f410-310">Bir Azure uygulama hizmeti izleme</span><span class="sxs-lookup"><span data-stu-id="7f410-310">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="7f410-311">Azure uygulama hizmetinde tanılama günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="7f410-311">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="7f410-312">Visual Studio'da bir Azure uygulama hizmeti sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="7f410-312">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="7f410-313">Günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="7f410-313">Logging</span></span>
<span data-ttu-id="7f410-314">Uygulama hizmeti tanılama günlükleri için standart ASP.NET izleme yazma kullanarak yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f410-314">You can write to App Service diagnostic logs by using the standard ASP.NET trace writing.</span></span> <span data-ttu-id="7f410-315">Günlüklere yazılır önce mobil uygulama arka ucunuzu tanılama etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f410-315">Before you can write to the logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="7f410-316">Tanılamayı etkinleştirin ve günlüklere yazılır için:</span><span class="sxs-lookup"><span data-stu-id="7f410-316">To enable diagnostics and write to the logs:</span></span>

1. <span data-ttu-id="7f410-317">Adımları [tanılama etkinleştirme](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="7f410-317">Follow the steps in [How to enable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="7f410-318">Aşağıdaki kod dosyanızda deyimiyle:</span><span class="sxs-lookup"><span data-stu-id="7f410-318">Add the following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="7f410-319">.NET arka ucundan için tanılama günlükleri, aşağıdaki gibi yazmak için bir izleme yazıcısı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7f410-319">Create a trace writer to write from the .NET backend to the diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="7f410-320">Sunucu projenizi yeniden yayımlamanız ve günlük ile kod yolu yürütmek için mobil uygulama arka ucu erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f410-320">Republish your server project, and access the Mobile App backend to execute the code path with the logging.</span></span>
5. <span data-ttu-id="7f410-321">Karşıdan yükle ve günlükleri açıklandığı gibi değerlendirme [nasıl yapılır: günlükleri indirmek](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="7f410-321">Download and evaluate the logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="7f410-322"><a name="local-debug"></a>Yerel kimlik doğrulaması ile hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="7f410-322"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="7f410-323">Uygulamanızı yerel olarak değişikliklerini buluta yayımlamadan önce test etmek için çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f410-323">You can run your application locally to test changes before publishing them to the cloud.</span></span> <span data-ttu-id="7f410-324">Çoğu Azure Mobile Apps arka uçlarını için basın *F5* while Visual Studio'da.</span><span class="sxs-lookup"><span data-stu-id="7f410-324">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="7f410-325">Ancak, kimlik doğrulaması kullanılırken ek bazı noktalar vardır.</span><span class="sxs-lookup"><span data-stu-id="7f410-325">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="7f410-326">Bir bulut tabanlı mobil uygulama ile App Service kimlik doğrulama/yapılandırılmış yetkilendirme olmalıdır ve istemci alternatif oturum açma ana bilgisayar belirtilen bulut uç noktası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7f410-326">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have the cloud endpoint specified as the alternate login host.</span></span> <span data-ttu-id="7f410-327">İstemci platformunuz için gerekli adımlarla belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="7f410-327">See the documentation for your client platform for the specific steps required.</span></span>

<span data-ttu-id="7f410-328">Mobil arka sahip olduğundan emin olun [Microsoft.Azure.Mobile.Server.Authentication] yüklü.</span><span class="sxs-lookup"><span data-stu-id="7f410-328">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="7f410-329">Ardından, sonra aşağıdaki uygulamanızın OWIN başlangıç sınıfı ekleyin `MobileAppConfiguration` uygulandıktan, `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="7f410-329">Then, in your application's OWIN startup class, add the following, after `MobileAppConfiguration` has been applied to your `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="7f410-330">Önceki örnekte, yapılandırmanız *authAudience* ve *authIssuer* uygulama Web.config içinde dosya ayarları için her HTTPS şeması kullanarak, uygulamanızın kök URL'si olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7f410-330">In the preceding example, you should configure the *authAudience* and *authIssuer* application settings within your Web.config file to each be the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="7f410-331">Benzer şekilde ayarlamalısınız *authSigningKey* uygulamanızı değerini anahtar imzalama kullanıcının olması.</span><span class="sxs-lookup"><span data-stu-id="7f410-331">Similarly you should set *authSigningKey* to be the value of your application's signing key.</span></span>
<span data-ttu-id="7f410-332">İmzalama anahtarı edinmek için:</span><span class="sxs-lookup"><span data-stu-id="7f410-332">To obtain the signing key:</span></span>

1. <span data-ttu-id="7f410-333">Uygulamanızda gidin [Azure portalı]</span><span class="sxs-lookup"><span data-stu-id="7f410-333">Navigate to your app within the [Azure portal]</span></span>
2. <span data-ttu-id="7f410-334">Tıklatın **Araçları**, **Kudu**, **Git**.</span><span class="sxs-lookup"><span data-stu-id="7f410-334">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="7f410-335">Kudu Yönetim sitesini'ı tıklatın **ortam**.</span><span class="sxs-lookup"><span data-stu-id="7f410-335">In the Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="7f410-336">Değeri Bul *Web sitesi\_AUTH\_imzalama\_anahtar*.</span><span class="sxs-lookup"><span data-stu-id="7f410-336">Find the value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="7f410-337">İmzalama anahtarı kullanmak *authSigningKey* , yerel uygulama yapılandırma parametresi.</span><span class="sxs-lookup"><span data-stu-id="7f410-337">Use the signing key for the *authSigningKey* parameter in your local application config.</span></span>  <span data-ttu-id="7f410-338">Mobil arka istemci bulut tabanlı uç noktasından belirteç alan yerel olarak çalıştırırken belirteçleri doğrulamak için şimdi bulunur.</span><span class="sxs-lookup"><span data-stu-id="7f410-338">Your mobile backend is now equipped to validate tokens when running locally, which the client obtains the token from the cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
<span data-ttu-id="7f410-339">[Azure portalı]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="7f410-339">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="7f410-340">[NuGet.org]: http://www.nuget.org/</span><span class="sxs-lookup"><span data-stu-id="7f410-340">[NuGet.org]: http://www.nuget.org/</span></span>
<span data-ttu-id="7f410-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span><span class="sxs-lookup"><span data-stu-id="7f410-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span></span>
<span data-ttu-id="7f410-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span><span class="sxs-lookup"><span data-stu-id="7f410-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span></span>
<span data-ttu-id="7f410-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span><span class="sxs-lookup"><span data-stu-id="7f410-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span></span>
<span data-ttu-id="7f410-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span><span class="sxs-lookup"><span data-stu-id="7f410-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span></span>
<span data-ttu-id="7f410-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span><span class="sxs-lookup"><span data-stu-id="7f410-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span></span>
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
