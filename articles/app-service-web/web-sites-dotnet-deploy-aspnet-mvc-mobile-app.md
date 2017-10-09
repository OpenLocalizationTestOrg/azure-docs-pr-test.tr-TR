---
title: "Azure App Service'te bir ASP.NET MVC 5 aaaDeploy mobil web uygulaması"
description: "Nasıl toodeploy bir web uygulaması tooAzure App Service mobile kullanarak ASP.NET MVC 5 web uygulaması özellikleri öğretilmektedir öğretici."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="4e347-103">Azure App Service'te bir ASP.NET MVC 5 mobil web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="4e347-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="4e347-104">Bu öğretici nasıl toobuild bir ASP.NET MVC 5 web, mobil dostu uygulamasını temellerini hello ve tooAzure uygulama hizmeti dağıtma öğretir.</span><span class="sxs-lookup"><span data-stu-id="4e347-104">This tutorial will teach you hello basics of how toobuild an ASP.NET MVC 5 web app that is mobile-friendly and deploy it tooAzure App Service.</span></span> <span data-ttu-id="4e347-105">Bu öğretici için gereksinim duyduğunuz [için Visual Studio Express 2013 Web] [ Visual Studio Express 2013] veya hello professional, zaten varsa, Visual Studio sürümü.</span><span class="sxs-lookup"><span data-stu-id="4e347-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or hello professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="4e347-106">Kullanabileceğiniz [Visual Studio 2015] ancak hello ekran görüntüleri farklı olacaktır ve hello ASP.NET 4.x şablonları kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e347-106">You can use [Visual Studio 2015] but hello screen shots will be different and you must use hello ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="4e347-107">Ne oluşturacağınız</span><span class="sxs-lookup"><span data-stu-id="4e347-107">What You'll Build</span></span>
<span data-ttu-id="4e347-108">Bu öğretici için sağlanan mobil özellikleri toohello basit konferans listeleme uygulama hello ekleyeceksiniz [başlangıç projesi][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="4e347-108">For this tutorial, you'll add mobile features toohello simple conference-listing application that's provided in hello [starter project][StarterProject].</span></span> <span data-ttu-id="4e347-109">Merhaba aşağıdaki ekran görüntüsü hello ASP.NET oturumları tamamlandı hello uygulamada, Internet Explorer 11 F12 geliştirici araçları hello tarayıcı öykünücüsünde görüldüğü gibi gösterir.</span><span class="sxs-lookup"><span data-stu-id="4e347-109">hello following screenshot shows hello ASP.NET sessions in hello completed application, as seen in hello browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="4e347-110">Internet Explorer 11 F12 hello geliştirici araçları ve hello kullanabilirsiniz [Fiddler aracı] [ Fiddler] toohelp uygulamanızın hatalarını ayıklama.</span><span class="sxs-lookup"><span data-stu-id="4e347-110">You can use hello Internet Explorer 11 F12 developer tools and hello [Fiddler tool][Fiddler] toohelp debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="4e347-111">Bilgi edineceksiniz yetenekleri</span><span class="sxs-lookup"><span data-stu-id="4e347-111">Skills You'll Learn</span></span>
<span data-ttu-id="4e347-112">Öğrenecekleriniz aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4e347-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="4e347-113">Nasıl toouse Visual Studio 2013 toopublish web uygulamanızı doğrudan Azure App Service'teki web uygulamasına tooa.</span><span class="sxs-lookup"><span data-stu-id="4e347-113">How toouse Visual Studio 2013 toopublish your web application directly tooa web app in Azure App Service.</span></span>
* <span data-ttu-id="4e347-114">Nasıl mobil cihazlarda görünen geliştirmek için hello CSS önyükleme framework hello ASP.NET MVC 5 şablonlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="4e347-114">How hello ASP.NET MVC 5 templates use hello CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="4e347-115">Nasıl hello iPhone ve Android gibi tootarget belirli mobil tarayıcılar toocreate mobile özgü görünümler</span><span class="sxs-lookup"><span data-stu-id="4e347-115">How toocreate mobile-specific views tootarget specific mobile browsers, such as hello iPhone and Android</span></span>
* <span data-ttu-id="4e347-116">Nasıl toocreate esnek görünümler (aygıtlarda toodifferent tarayıcılar yanıt görünümler)</span><span class="sxs-lookup"><span data-stu-id="4e347-116">How toocreate responsive views (views that respond toodifferent browsers across devices)</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="4e347-117">Merhaba geliştirme ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="4e347-117">Set up hello development environment</span></span>
<span data-ttu-id="4e347-118">2.5.1 .NET için Azure SDK'sı hello yükleyerek geliştirme ortamınızı ayarlayın veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="4e347-118">Set up your development environment by installing hello Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="4e347-119">.NET için Azure SDK tooinstall hello hello bağlantıyı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4e347-119">tooinstall hello Azure SDK for .NET, click hello link below.</span></span> <span data-ttu-id="4e347-120">Henüz yüklü Visual Studio 2013 yoksa, hello bağlantı tarafından yüklenir.</span><span class="sxs-lookup"><span data-stu-id="4e347-120">If you don't have Visual Studio 2013 installed yet, it will be installed by hello link.</span></span> <span data-ttu-id="4e347-121">Bu öğreticide Visual Studio 2013 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4e347-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="4e347-122">[Visual Studio 2013 için Azure SDK][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="4e347-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="4e347-123">Merhaba Web Platformu yükleyicisi penceresinde **yüklemek** ve hello yükleme işlemine devam edin.</span><span class="sxs-lookup"><span data-stu-id="4e347-123">In hello Web Platform Installer window, click **Install** and proceed with hello installation.</span></span>

<span data-ttu-id="4e347-124">Bir mobil tarayıcı öykünücüsü de gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e347-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="4e347-125">Merhaba aşağıdakilerden herhangi birini çalışır:</span><span class="sxs-lookup"><span data-stu-id="4e347-125">Any of hello following will work:</span></span>

* <span data-ttu-id="4e347-126">Tarayıcı öykünücüsünde [Internet Explorer 11 F12 Geliştirici Araçları] [ EmulatorIE11] (tüm mobil tarayıcı ekran görüntülerinde kullanılır).</span><span class="sxs-lookup"><span data-stu-id="4e347-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="4e347-127">Windows Phone 8, Windows Phone 7 ve Apple iPad için kullanıcı aracısı dizesi hazır sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4e347-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="4e347-128">Tarayıcı öykünücüsünde [Google Chrome DevTools][EmulatorChrome].</span><span class="sxs-lookup"><span data-stu-id="4e347-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="4e347-129">Çok sayıda Android aygıtların yanı sıra Apple iPhone, Apple iPad ve Amazon Kindle yangın için hazır ayarları içerir.</span><span class="sxs-lookup"><span data-stu-id="4e347-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="4e347-130">Ayrıca, dokunma olayları öykünür.</span><span class="sxs-lookup"><span data-stu-id="4e347-130">It also emulates touch events.</span></span>
* <span data-ttu-id="4e347-131">[Opera Mobile öykünücüsü][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="4e347-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="4e347-132">C ile Visual Studio projeleri\# kaynak kodu bu konuda kullanılabilir tooaccompany şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4e347-132">Visual Studio projects with C\# source code are available tooaccompany this topic:</span></span>

* <span data-ttu-id="4e347-133">[Başlangıç projesi indirme][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="4e347-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="4e347-134">[Proje indirme tamamlandı][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="4e347-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="4e347-135"><a name="bkmk_DeployStarterProject"></a>Merhaba başlangıç projesi tooan Azure web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="4e347-135"><a name="bkmk_DeployStarterProject"></a>Deploy hello starter project tooan Azure web app</span></span>
1. <span data-ttu-id="4e347-136">Merhaba konferans listeleme uygulamayı karşıdan [başlangıç projesi][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="4e347-136">Download hello conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="4e347-137">Ardından Windows Gezgini'nde, indirilen hello ZIP dosyasını sağ tıklatın ve seçin *özellikleri*.</span><span class="sxs-lookup"><span data-stu-id="4e347-137">Then in Windows Explorer, right-click hello downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="4e347-138">Merhaba, **özellikleri** iletişim kutusunda, hello seçin **Engellemeyi Kaldır** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="4e347-138">In hello **Properties** dialog box, choose hello **Unblock** button.</span></span> <span data-ttu-id="4e347-139">(Engellemelerini kaldırma toouse çalıştığınızda oluşan bir güvenlik uyarısı engelleyen bir *.zip* hello Web'den indirdiğiniz dosya.)</span><span class="sxs-lookup"><span data-stu-id="4e347-139">(Unblocking prevents a security warning that occurs when you try toouse a *.zip* file that you've downloaded from hello web.)</span></span>
4. <span data-ttu-id="4e347-140">Merhaba ZIP dosyasını sağ tıklatın ve seçin **tümünü Ayıkla** hello dosya sıkıştırmasını açmak için.</span><span class="sxs-lookup"><span data-stu-id="4e347-140">Right-click hello ZIP file and select **Extract All** to unzip hello file.</span></span> 
5. <span data-ttu-id="4e347-141">Visual Studio'da hello açın *C#\Mvc5Mobile.sln* dosya.</span><span class="sxs-lookup"><span data-stu-id="4e347-141">In Visual Studio, open hello *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="4e347-142">Çözüm Gezgini'nde, hello projesine sağ tıklayın ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="4e347-142">In Solution Explorer, right-click hello project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="4e347-143">Web'de yayımlama tıklatın **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="4e347-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="4e347-144">Azure'da oturum zaten yapmadıysanız, tıklatın **Hesap Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4e347-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="4e347-145">Merhaba istemleri toolog Azure hesabınızda izleyin.</span><span class="sxs-lookup"><span data-stu-id="4e347-145">Follow hello prompts toolog into your Azure account.</span></span>
10. <span data-ttu-id="4e347-146">Merhaba App Service iletişim şimdi oturum gibi göstermelidir.</span><span class="sxs-lookup"><span data-stu-id="4e347-146">hello App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="4e347-147">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4e347-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="4e347-148">Merhaba, **Web uygulaması adı** alanında, benzersiz uygulama adı ön ekini belirtin.</span><span class="sxs-lookup"><span data-stu-id="4e347-148">In hello **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="4e347-149">Tam web uygulaması adı olacaktır  *&lt;öneki >*. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="4e347-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="4e347-150">Ayrıca, seçin veya yeni bir kaynak grubu adı belirtin **kaynak grubu**.</span><span class="sxs-lookup"><span data-stu-id="4e347-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="4e347-151">Ardından **yeni** toocreate yeni bir uygulama hizmeti planı.</span><span class="sxs-lookup"><span data-stu-id="4e347-151">Then, click **New** toocreate a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="4e347-152">Merhaba yeni uygulama hizmeti planı yapılandırmak ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4e347-152">Configure hello new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="4e347-153">Geri hello App Service Oluştur iletişim kutusunda tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4e347-153">Back in hello Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="4e347-154">Hello Azure kaynaklarını oluşturulduktan sonra hello Web Yayımla iletişim yeni uygulamanızı hello ayarları ile doldurulur.</span><span class="sxs-lookup"><span data-stu-id="4e347-154">After hello Azure resources are created, hello Publish Web dialog will be filled with hello settings for your new app.</span></span> <span data-ttu-id="4e347-155">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4e347-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="4e347-156">Visual Studio yayımlama hello başlangıç projesi toohello Azure web uygulaması tamamlandığında toodisplay hello canlı web uygulaması hello Masaüstü tarayıcı penceresinde açar.</span><span class="sxs-lookup"><span data-stu-id="4e347-156">Once Visual Studio finishes publishing hello starter project toohello Azure web app, hello desktop browser opens toodisplay hello live web app.</span></span>
15. <span data-ttu-id="4e347-157">Mobil tarayıcı öykünücüsü'ı başlatın, Merhaba konferans uygulaması hello URL'sini kopyalayın (*<prefix>*. azurewebsites.net) hello öykünücüsü içine sağ üst düğmesini tıklatın ve seçin **etiketegöreGözat**.</span><span class="sxs-lookup"><span data-stu-id="4e347-157">Start your mobile browser emulator, copy hello URL for hello conference application (*<prefix>*.azurewebsites.net) into hello emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="4e347-158">Merhaba varsayılan tarayıcı olarak Internet Explorer 11 kullanıyorsanız, tootype yeterlidir `F12`, ardından `Ctrl+8`, hello tarayıcı profilini çok değiştirmek**Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="4e347-158">If you are using Internet Explorer 11 as hello default browser, you just need tootype `F12`, then `Ctrl+8`, and then change hello browser profile too**Windows Phone**.</span></span> <span data-ttu-id="4e347-159">Aşağıdaki görüntü hello gösterir *AllTags* dikey modunda görüntüle (seçme gelen **etikete göre Gözat**).</span><span class="sxs-lookup"><span data-stu-id="4e347-159">The image below shows hello *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="4e347-160">MVC 5 uygulamanızı Visual Studio'dan ayıklayabilirsiniz olsa da, web uygulaması tooAzure yayımlayabilirsiniz yeniden tooverify hello canlı web uygulamasından doğrudan mobil, tarayıcı veya tarayıcı öykünücüsü.</span><span class="sxs-lookup"><span data-stu-id="4e347-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app tooAzure again tooverify hello live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="4e347-161">Merhaba görünen bir mobil cihazda çok okunabilir durumdadır.</span><span class="sxs-lookup"><span data-stu-id="4e347-161">hello display is very readable on a mobile device.</span></span> <span data-ttu-id="4e347-162">Merhaba görsel efektler hello önyükleme CSS çerçevesi tarafından uygulanan bazıları da zaten görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e347-162">You can also already see some of hello visual effects applied by hello Bootstrap CSS framework.</span></span>
<span data-ttu-id="4e347-163">Merhaba tıklatın **ASP.NET** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="4e347-163">Click hello **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="4e347-164">Merhaba ASP.NET etiket görünümünü önyükleme sizin için otomatik olarak yapar yakınlaştırma donatılmıştır toohello ekrandır.</span><span class="sxs-lookup"><span data-stu-id="4e347-164">hello ASP.NET tag view is zoom-fitted toohello screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="4e347-165">Ancak, bu görünüm toobetter seri hello mobil tarayıcı artırabilir.</span><span class="sxs-lookup"><span data-stu-id="4e347-165">However, you can improve this view toobetter suit hello mobile browser.</span></span> <span data-ttu-id="4e347-166">Örneğin, hello **tarih** okumak sütun zordur.</span><span class="sxs-lookup"><span data-stu-id="4e347-166">For example, hello **Date** column is difficult to read.</span></span> <span data-ttu-id="4e347-167">Daha sonra hello öğreticide hello değiştireceğiz *AllTags* toomake görüntülemek, mobil dostu.</span><span class="sxs-lookup"><span data-stu-id="4e347-167">Later in hello tutorial you'll change hello *AllTags* view toomake it mobile-friendly.</span></span>

## <span data-ttu-id="4e347-168"><a name="bkmk_bootstrap"></a>Önyükleme CSS Framework</span><span class="sxs-lookup"><span data-stu-id="4e347-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="4e347-169">Yeni hello MVC 5 yerleşik önyükleme destek şablonudur.</span><span class="sxs-lookup"><span data-stu-id="4e347-169">New in hello MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="4e347-170">Nasıl hello farklı görünümleri, uygulamanızda hemen artırır zaten gördünüz.</span><span class="sxs-lookup"><span data-stu-id="4e347-170">You have already seen how it immediately improves hello different views in your application.</span></span> <span data-ttu-id="4e347-171">Örneğin, Hello tarayıcı genişliği daha küçük olduğunda hello gezinti çubuğu hello üstünde otomatik olarak daraltılabilir.</span><span class="sxs-lookup"><span data-stu-id="4e347-171">For example, hello navigation bar at hello top is automatically collapsible when hello browser width is smaller.</span></span> <span data-ttu-id="4e347-172">Hello Masaüstü tarayıcının hello tarayıcı penceresini yeniden boyutlandırmayı deneyin ve hello gezinti çubuğu kendi görünüm nasıl değiştiğini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e347-172">On hello desktop browser, try resizing hello browser window and see how hello navigation bar changes its look and feel.</span></span> <span data-ttu-id="4e347-173">Önyükleme yerleşik hello yanıt veren web tasarımı budur.</span><span class="sxs-lookup"><span data-stu-id="4e347-173">This is hello responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="4e347-174">Merhaba Web uygulaması önyükleme görünür nasıl toosee açmak *uygulama\_Başlat\\BundleConfig.cs* ve açıklamayı içeren hello satırları *bootstrap.js* ve *bootstrap.css*.</span><span class="sxs-lookup"><span data-stu-id="4e347-174">toosee how hello Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out hello lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="4e347-175">Merhaba aşağıdaki kod hello hello son iki bilgilerinin gösterir `RegisterBundles` yöntemi hello değişiklikten sonra:</span><span class="sxs-lookup"><span data-stu-id="4e347-175">hello following code shows hello last two statements of hello `RegisterBundles` method after hello change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="4e347-176">Tuşuna `Ctrl+F5` toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="4e347-176">Press `Ctrl+F5` toorun hello application.</span></span>

<span data-ttu-id="4e347-177">Bu hello daraltılabilir gezinti çubuğu sunulmuştur yalnızca normal sırasız bir listesini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="4e347-177">Observe that hello collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="4e347-178">Tıklatın **etikete göre Gözat** yeniden, ardından **ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="4e347-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="4e347-179">Merhaba mobil öykünücü görünümünde, artık yakınlaştırma donatılmıştır toohello ekran değildir ve sipariş toosee hello sağ tarafında Merhaba tablonun yana kaydırma gerekir göre görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e347-179">In hello mobile emulator view, you can see now that it is no longer zoom-fitted toohello screen, and you must scroll sideways in order toosee hello right side of hello table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="4e347-180">Yaptığınız değişiklikleri geri almak ve mobil dostu görünen hello yenileme hello mobil tarayıcı tooverify geri yüklendi.</span><span class="sxs-lookup"><span data-stu-id="4e347-180">Undo your changes and refresh hello mobile browser tooverify that hello mobile-friendly display has been restored.</span></span>

<span data-ttu-id="4e347-181">Önyükleme belirli tooASP.NET MVC 5 değildir ve herhangi bir web uygulamasında bu özelliklerden yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e347-181">Bootstrap is not specific tooASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="4e347-182">Ancak, MVC 5 Web uygulaması önyükleme varsayılan olarak yararlanabilir böylece artık ASP.NET MVC 5 proje şablonuna kuruludur.</span><span class="sxs-lookup"><span data-stu-id="4e347-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="4e347-183">Önyükleme hakkında daha fazla bilgi için toothe Git [önyükleme] [ BootstrapSite] site.</span><span class="sxs-lookup"><span data-stu-id="4e347-183">For more information about Bootstrap, go toothe [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="4e347-184">Merhaba sonraki bölümde göreceğiniz nasıl tooprovide mobil tarayıcı özel görünümler.</span><span class="sxs-lookup"><span data-stu-id="4e347-184">In hello next section you'll see how tooprovide mobile-browser specific views.</span></span>

## <span data-ttu-id="4e347-185"><a name="bkmk_overrideviews"></a>Merhaba görünümleri, düzenleri ve kısmi görünümler geçersiz kıl</span><span class="sxs-lookup"><span data-stu-id="4e347-185"><a name="bkmk_overrideviews"></a> Override hello Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="4e347-186">Genel olarak, tek bir mobil tarayıcı için veya belirli bir tarayıcı için mobil tarayıcılar için (düzenler ve kısmi görünümler dahil) herhangi bir görünüm geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e347-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="4e347-187">mobile özgü tooprovide görüntülemek için bir görünüm dosyasını kopyalayın ve ekleme *. Mobil* toohello dosya adı.</span><span class="sxs-lookup"><span data-stu-id="4e347-187">tooprovide a mobile-specific view, you can copy a view file and add *.Mobile* toohello file name.</span></span> <span data-ttu-id="4e347-188">Örneğin, bir mobil toocreate *dizin* görünümü kopyalayabilir *görünümleri\\giriş\\Index.cshtml* için *görünümleri\\giriş\\ Index.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="4e347-188">For example, toocreate a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="4e347-189">Bu bölümde, bir mobil özgü Düzen dosyası oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="4e347-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="4e347-190">toostart, kopya *görünümleri\\paylaşılan\\\_Layout.cshtml* için *görünümleri\\paylaşılan\\\_Layout.Mobile.cshtml* .</span><span class="sxs-lookup"><span data-stu-id="4e347-190">toostart, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="4e347-191">Açık  *\_Layout.Mobile.cshtml* hello başlığını değiştirip **MVC5 uygulama** çok**MVC5 uygulama (mobil)**.</span><span class="sxs-lookup"><span data-stu-id="4e347-191">Open *\_Layout.Mobile.cshtml* and change hello title from **MVC5 Application** too**MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="4e347-192">Her `Html.ActionLink` çağırmak için hello gezinti çubuğu, "her bağlantısını gözatma türü" kaldırmak *ActionLink*.</span><span class="sxs-lookup"><span data-stu-id="4e347-192">In each `Html.ActionLink` call for hello navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="4e347-193">Merhaba aşağıdaki kod gösterir tamamlandı hello `<ul class="nav navbar-nav">` hello mobil düzeni dosyasının etiketi.</span><span class="sxs-lookup"><span data-stu-id="4e347-193">hello following code shows hello completed `<ul class="nav navbar-nav">` tag of hello mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="4e347-194">Kopya hello *görünümleri\\giriş\\AllTags.cshtml* dosya *görünümleri\\giriş\\AllTags.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="4e347-194">Copy hello *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="4e347-195">Merhaba yeni dosyasını açın ve değişiklik `<h2>` "Etiketleri" öğesinden çok "etiketler (M)":</span><span class="sxs-lookup"><span data-stu-id="4e347-195">Open hello new file and change the `<h2>` element from "Tags" too"Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="4e347-196">Bir masaüstü tarayıcısı kullanarak ve mobil tarayıcı öykünücüsü kullanarak toohello etiketleri sayfasına göz atın.</span><span class="sxs-lookup"><span data-stu-id="4e347-196">Browse toohello tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="4e347-197">Merhaba mobil tarayıcı öykünücüsü iki değişiklik yaptığınız hello gösterir (Merhaba başlığını  *\_Layout.Mobile.cshtml* ve hello başlığını *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="4e347-197">hello mobile browser emulator shows hello two changes you made (hello title from *\_Layout.Mobile.cshtml* and hello title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="4e347-198">Buna karşılık, hello Masaüstü görüntü değişmediğini (başlıkları ile  *\_Layout.cshtml* ve *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="4e347-198">In contrast, hello desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="4e347-199"><a name="bkmk_browserviews"></a>Tarayıcı özel görünümlerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e347-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="4e347-200">Ayrıca toomobile ve Masaüstü özgü görünümler, tek bir tarayıcı için görünümler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e347-200">In addition toomobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="4e347-201">Örneğin, özellikle hello iPhone veya hello Android tarayıcı görünümler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e347-201">For example, you can create views that are specifically for hello iPhone or hello Android browser.</span></span> <span data-ttu-id="4e347-202">Bu bölümde, hello iPhone tarayıcı ve hello iPhone sürümü için bir düzen oluşturacaksınız *AllTags* görünümü.</span><span class="sxs-lookup"><span data-stu-id="4e347-202">In this section, you'll create a layout for hello iPhone browser and an iPhone version of hello *AllTags* view.</span></span>

<span data-ttu-id="4e347-203">Açık hello *Global.asax* dosyasını ve kod toohello altına aşağıdaki hello eklemek `Application_Start` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4e347-203">Open hello *Global.asax* file and add hello following code toohello bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="4e347-204">Bu kod, "her gelen istek karşı eşleşen iPhone" adlı yeni bir görüntü modu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="4e347-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="4e347-205">Merhaba gelen istek (diğer bir deyişle, hello kullanıcı aracısı hello dizesi "iPhone" içeriyorsa), tanımlanmış bir koşulu eşleşirse, ASP.NET MVC için görünümleri adında "iPhone" soneki içeren arar.</span><span class="sxs-lookup"><span data-stu-id="4e347-205">If hello incoming request matches the condition you defined (that is, if hello user agent contains hello string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="4e347-206">Mobil tarayıcı özgü ekleme görüntülediğinizde modları, gibi iPhone ve Android için olması emin tooset hello ilk bağımsız değişkeni çok`0` (Merhaba listenin hello Ekle) toomake bu hello tarayıcıya özgü modu hello mobil şablonu göre önceliklidir emin (*. Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="4e347-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure tooset hello first argument too`0` (insert at hello top of hello list) toomake sure that hello browser-specific mode takes precedence over hello mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="4e347-207">Merhaba mobil şablonu hello hello listesinin başında yerine ise, bu, hedeflenen görüntü modu seçilir (ilk eşleşme WINS hello ve eşleşen tüm mobil tarayıcılar hello mobil şablonu).</span><span class="sxs-lookup"><span data-stu-id="4e347-207">If hello mobile template is at hello top of hello list instead, it will be selected over your intended display mode (hello first match wins, and hello mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="4e347-208">Merhaba kodda sağ `DefaultDisplayMode`, seçin **gidermek**ve ardından `using System.Web.WebPages;`.</span><span class="sxs-lookup"><span data-stu-id="4e347-208">In hello code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="4e347-209">Bu başvuru toothe ekler `System.Web.WebPages` yerdir ad alanı `DisplayModeProvider` ve `DefaultDisplayMode` türleri tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4e347-209">This adds a reference toothe `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="4e347-210">Alternatif olarak, aşağıdaki satırı toothe hello yalnızca el ile ekleyebileceğiniz `using` hello dosyasının bölümü.</span><span class="sxs-lookup"><span data-stu-id="4e347-210">Alternatively, you can just manually add hello following line toothe `using` section of hello file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="4e347-211">Merhaba değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4e347-211">Save hello changes.</span></span> <span data-ttu-id="4e347-212">Kopya *görünümleri\\paylaşılan\\\_Layout.Mobile.cshtml* dosya *görünümleri\\paylaşılan\\\_Layout.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="4e347-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="4e347-213">Merhaba yeni dosyasını açın ve hello başlığını değiştirme `MVC5 Application (Mobile)` için `MVC5 Application (iPhone)`.</span><span class="sxs-lookup"><span data-stu-id="4e347-213">Open hello new file and then change hello title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="4e347-214">Kopya hello *görünümleri\\giriş\\AllTags.Mobile.cshtml* dosya *görünümleri\\giriş\\AllTags.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="4e347-214">Copy hello *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="4e347-215">Merhaba Hello yeni dosyasında değişiklik `<h2>` öğesi öğesinden "etiketler (M)" çok "etiketler (iPhone)".</span><span class="sxs-lookup"><span data-stu-id="4e347-215">In hello new file, change hello `<h2>` element from "Tags (M)" too"Tags (iPhone)".</span></span>

<span data-ttu-id="4e347-216">Merhaba uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4e347-216">Run hello application.</span></span> <span data-ttu-id="4e347-217">Bir mobil tarayıcı öykünücüsü çalıştırmak, kendi kullanıcı aracısı çok ayarlandığından emin olun "iPhone" ve toohello Gözat *AllTags* görünümü.</span><span class="sxs-lookup"><span data-stu-id="4e347-217">Run a mobile browser emulator, make sure its user agent is set too"iPhone", and browse toohello *AllTags* view.</span></span> <span data-ttu-id="4e347-218">Internet Explorer 11 F12 geliştirici araçları hello öykünücüsü kullanıyorsanız, öykünme toohello aşağıdakileri yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="4e347-218">If you are using hello emulator in Internet Explorer 11 F12 developer tools, configure emulation toohello following:</span></span>

* <span data-ttu-id="4e347-219">Tarayıcı profili = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="4e347-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="4e347-220">Kullanıcı aracısı dizesi = **özel**</span><span class="sxs-lookup"><span data-stu-id="4e347-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="4e347-221">Özel bir dize = **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="4e347-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="4e347-222">Merhaba aşağıdaki ekran gösterilir hello *AllTags* Internet Explorer 11 F12 geliştirici araçları hello özel kullanıcı aracısı dizesi ile öykünücüde işlenmiş Görünüm (Bu, bir iPhone 5 C kullanıcı aracısı dizesi).</span><span class="sxs-lookup"><span data-stu-id="4e347-222">hello following screenshot shows hello *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with hello custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="4e347-223">Merhaba mobil tarayıcıda hello seçin **konuşmacılar** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="4e347-223">In hello mobile browser, select hello **Speakers** link.</span></span> <span data-ttu-id="4e347-224">Mobil bir görünüm olduğundan (*AllSpeakers.Mobile.cshtml*), hello varsayılan konuşmacılar görüntülemek (*AllSpeakers.cshtml*) hello mobil düzeni görünümü kullanılarak oluşturulması ( *\_ Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="4e347-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), hello default speakers view (*AllSpeakers.cshtml*) is rendered using hello mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="4e347-225">Merhaba başlık aşağıda gösterildiği gibi **MVC5 uygulama (mobil)** tanımlanan  *\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="4e347-225">As shown below, hello title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="4e347-226">Ayarlayarak genel işleme mobil düzeni içinde varsayılan (mobil olmayan) görünümünden devre dışı bırakabilirsiniz `RequireConsistentDisplayMode` için `true` hello içinde *görünümleri\\\_ViewStart.cshtml* dosyası şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="4e347-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in hello *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="4e347-227">Zaman `RequireConsistentDisplayMode` çok ayarlanır`true`, hello mobil Düzen (*\_Layout.Mobile.cshtml*) yalnızca mobil görünümleri için kullanılır (yani görünüm dosyası hello biçiminde olduğunda  ***Görünümadı** . Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="4e347-227">When `RequireConsistentDisplayMode` is set too`true`, hello mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of hello form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="4e347-228">Tooset isteyebilirsiniz `RequireConsistentDisplayMode` çok`true` mobil düzeninizi iyi mobil olmayan görünümlerle işe yaramazsa.</span><span class="sxs-lookup"><span data-stu-id="4e347-228">You might want tooset `RequireConsistentDisplayMode` too`true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="4e347-229">Merhaba ekran görüntüsü aşağıda gösterilmiştir nasıl hello *konuşmacılar* sayfasını işler `RequireConsistentDisplayMode` çok ayarlanır`true` (olmadan hello dizesindeki "(mobil)" Merhaba hello üstünde gezinti çubuğu).</span><span class="sxs-lookup"><span data-stu-id="4e347-229">hello screenshot below shows how hello *Speakers* page renders when `RequireConsistentDisplayMode` is set too`true` (without hello string "(Mobile)" in hello navigational bar at hello top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="4e347-230">Ayarlayarak belirli bir görünümde tutarlı görüntü modu devre dışı bırakabilirsiniz `RequireConsistentDisplayMode` çok`false` hello görünüm dosyasında.</span><span class="sxs-lookup"><span data-stu-id="4e347-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` too`false` in hello view file.</span></span> <span data-ttu-id="4e347-231">Merhaba aşağıdaki biçimlendirmede *görünümleri\\giriş\\AllSpeakers.cshtml* dosya kümeleri `RequireConsistentDisplayMode` çok`false`:</span><span class="sxs-lookup"><span data-stu-id="4e347-231">The following markup in hello *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` too`false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="4e347-232">Bu bölümde gördük nasıl toocreate mobil düzenleri ve görünümler ve iPhone toocreate düzenleri ve görünümler gibi belirli cihazlar için nasıl hello.</span><span class="sxs-lookup"><span data-stu-id="4e347-232">In this section we've seen how toocreate mobile layouts and views and how toocreate layouts and views for specific devices such as hello iPhone.</span></span>
<span data-ttu-id="4e347-233">Ancak, tek bir stil Masaüstü, telefon ve tablet tarayıcılar toocreate tutarlı bir görünüm arasında uygulanabilir anlamına gelir esnek düzeni hello ana avantajı hello önyükleme CSS framework'ün olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="4e347-233">However, hello main advantage of hello Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers toocreate a consistent look and feel.</span></span> <span data-ttu-id="4e347-234">Merhaba sonraki bölümde nasıl tooleverage Bootstrap toocreate mobil dostu görürsünüz görünümleri.</span><span class="sxs-lookup"><span data-stu-id="4e347-234">In hello next section you'll see how tooleverage Bootstrap toocreate mobile-friendly views.</span></span>

## <span data-ttu-id="4e347-235"><a name="bkmk_Improvespeakerslist"></a>Merhaba konuşmacılar listesi geliştirmek</span><span class="sxs-lookup"><span data-stu-id="4e347-235"><a name="bkmk_Improvespeakerslist"></a> Improve hello Speakers List</span></span>
<span data-ttu-id="4e347-236">Yalnızca anlatıldığı gibi hello *konuşmacılar* görünümdür okunabilir ancak hello bağlantılar küçük olduğunda ve bir mobil cihazda zor tootap.</span><span class="sxs-lookup"><span data-stu-id="4e347-236">As you just saw, hello *Speakers* view is readable, but hello links are small and are difficult tootap on a mobile device.</span></span> <span data-ttu-id="4e347-237">Bu bölümde, hello yapacağız *AllSpeakers* büyük, dokunun kolay bağlantıları görüntüler ve arama kutusu tooquickly içeren görünümü mobil dostu konuşmacılar bulur.</span><span class="sxs-lookup"><span data-stu-id="4e347-237">In this section, you'll make hello *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box tooquickly find speakers.</span></span>

<span data-ttu-id="4e347-238">Merhaba önyükleme kullanabilirsiniz [bağlantılı listesi grubu] [ linked list group] hello artırmak için stil *konuşmacılar* görünümü.</span><span class="sxs-lookup"><span data-stu-id="4e347-238">You can use hello Bootstrap [linked list group][linked list group] styling to improve hello *Speakers* view.</span></span> <span data-ttu-id="4e347-239">İçinde *görünümleri\\giriş\\AllSpeakers.cshtml*, hello hello Razor dosyasının içeriğini aşağıdaki hello kod ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4e347-239">In *Views\\Home\\AllSpeakers.cshtml*, replace hello contents of hello Razor file with hello code below.</span></span>

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="4e347-240">Merhaba `class="list-group"` hello özniteliğinde `<div>` etiket uygular önyükleme listesi stil ve hello `class="input-group-item"` özniteliği önyükleme liste öğesi stil tooeach bağlantısını uygular.</span><span class="sxs-lookup"><span data-stu-id="4e347-240">hello `class="list-group"` attribute in hello `<div>` tag applies the Bootstrap list styling, and hello `class="input-group-item"` attribute applies Bootstrap list item styling tooeach link.</span></span>

<span data-ttu-id="4e347-241">Merhaba mobil tarayıcıyı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="4e347-241">Refresh hello mobile browser.</span></span> <span data-ttu-id="4e347-242">Bu görünüm görülüyor Hello güncelleştirildi:</span><span class="sxs-lookup"><span data-stu-id="4e347-242">hello updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="4e347-243">Merhaba önyükleme [bağlantılı listesi grubu] [ linked list group] stil kadar daha iyi bir kullanıcı deneyimi olan hello tüm kutusunu tıklanabilir, her bağlantı için yapar.</span><span class="sxs-lookup"><span data-stu-id="4e347-243">hello Bootstrap [linked list group][linked list group] styling makes hello entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="4e347-244">Toothe Masaüstü görünümüne geçin ve hello tutarlı bir görünüm gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="4e347-244">Switch toothe desktop view and observe hello consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="4e347-245">Merhaba mobil tarayıcı görünümü geliştirilmiştir rağmen hello uzun konuşmacılar listesi gidin zordur.</span><span class="sxs-lookup"><span data-stu-id="4e347-245">Although hello mobile browser view has improved, it's difficult to navigate hello long list of speakers.</span></span> <span data-ttu-id="4e347-246">Önyükleme bir arama filtresi işlevselliği out-of--box sağlamaz, ancak birkaç kod satırıyla, ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e347-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="4e347-247">İlk arama kutusu toohello görünümü ekleme sonra hello hello filtre işlevi için JavaScript kodu kanca.</span><span class="sxs-lookup"><span data-stu-id="4e347-247">You will first add a search box toohello view, then hook up with hello JavaScript code for hello filter function.</span></span> <span data-ttu-id="4e347-248">İçinde *görünümleri\\giriş\\AllSpeakers.cshtml*, ekleme bir \<form\> etiketi hello hemen sonra \<h2\> , aşağıda gösterildiği gibi etiketi:</span><span class="sxs-lookup"><span data-stu-id="4e347-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after hello \<h2\> tag, as shown below:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="4e347-249">Bu hello fark `<form>` ve `<input>` etiketlere hem de hello uygulanan önyükleme stilleri toothem sahip.</span><span class="sxs-lookup"><span data-stu-id="4e347-249">Notice that hello `<form>` and `<input>` tags both have hello Bootstrap styles applied toothem.</span></span> <span data-ttu-id="4e347-250">Merhaba `<span>` öğesi ekler bir önyükleme [glyphicon] [ glyphicon] toothe arama kutusu.</span><span class="sxs-lookup"><span data-stu-id="4e347-250">hello `<span>` element adds a Bootstrap [glyphicon][glyphicon] toothe search box.</span></span>

<span data-ttu-id="4e347-251">Merhaba, *betikleri* klasörü, adlandırılan bir JavaScript dosyası ekleme *filter.js*.</span><span class="sxs-lookup"><span data-stu-id="4e347-251">In hello *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="4e347-252">Merhaba dosyasını açın ve kod içine aşağıdaki hello yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="4e347-252">Open hello file and paste hello following code into it:</span></span>

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

<span data-ttu-id="4e347-253">Ayrıca, kayıtlı paketlerin tooinclude filter.js gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e347-253">You also need tooinclude filter.js in your registered bundles.</span></span> <span data-ttu-id="4e347-254">Açık *uygulama\_Başlat\\BundleConfig.cs* ve hello ilk paketleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4e347-254">Open *App\_Start\\BundleConfig.cs* and change hello first bundles.</span></span> <span data-ttu-id="4e347-255">İlk değiştirme `bundles.Add` deyimi (hello için **jquery** paket) tooinclude *betikleri\\filter.js*aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="4e347-255">Change the first `bundles.Add` statement (for hello **jquery** bundle) tooinclude *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="4e347-256">Merhaba **jquery** paket hello varsayılan olarak zaten işlenmiş  *\_düzeni* görünümü.</span><span class="sxs-lookup"><span data-stu-id="4e347-256">hello **jquery** bundle is already rendered by hello default *\_Layout* view.</span></span> <span data-ttu-id="4e347-257">Daha sonra hello kullanabilir aynı JavaScript kodu tooapply filtre işlevselliği tooother liste görünümleri.</span><span class="sxs-lookup"><span data-stu-id="4e347-257">Later, you can utilize hello same JavaScript code tooapply the filter functionality tooother list views.</span></span>

<span data-ttu-id="4e347-258">Merhaba mobil tarayıcıyı yenileyin ve Git toohello *AllSpeakers* görünümü.</span><span class="sxs-lookup"><span data-stu-id="4e347-258">Refresh hello mobile browser and go toohello *AllSpeakers* view.</span></span> <span data-ttu-id="4e347-259">Arama kutusuna "sc" yazın.</span><span class="sxs-lookup"><span data-stu-id="4e347-259">In the search box, type "sc".</span></span> <span data-ttu-id="4e347-260">Merhaba konuşmacılar listesi şimdi tooyour arama dizesi göre filtrelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="4e347-260">hello speakers list should now be filtered according tooyour search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="4e347-261"><a name="bkmk_improvetags"></a>Merhaba Etiketler listesi geliştirmek</span><span class="sxs-lookup"><span data-stu-id="4e347-261"><a name="bkmk_improvetags"></a> Improve hello Tags List</span></span>
<span data-ttu-id="4e347-262">Hello gibi *konuşmacılar* hello görünümü *etiketleri* görünümdür okunabilir ancak hello bağlantılardır mobil aygıttaki zor ve küçük tootap.</span><span class="sxs-lookup"><span data-stu-id="4e347-262">Like hello *Speakers* view, hello *Tags* view is readable, but hello links are small and difficult tootap on a mobile device.</span></span> <span data-ttu-id="4e347-263">Merhaba düzeltebilirsiniz *etiketleri* görünüm hello aynı şekilde hello düzeltme *konuşmacılar* daha önce ancak hello aşağıda açıklanan hello kod değişiklikleri kullanırsanız, görüntülemek `Html.ActionLink` yöntemi sözdiziminde  *Görünümler\\giriş\\AllTags.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="4e347-263">You can fix hello *Tags* view hello same way you fix hello *Speakers* view, if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="4e347-264">Merhaba Masaüstü tarayıcısı görünümler gibi yenilenir:</span><span class="sxs-lookup"><span data-stu-id="4e347-264">hello refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="4e347-265">Ve mobil tarayıcı görünümler gibi hello yenilenir:</span><span class="sxs-lookup"><span data-stu-id="4e347-265">And hello refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="4e347-266">Bu hello özgün liste biçimlendirmesini fark ederseniz yine de var. mobil tarayıcı hello ve ne oldu tooyour iyi önyükleme stil merak ediyor; Bu, önceki eylem toocreate mobil belirli görünüm bir yapı</span><span class="sxs-lookup"><span data-stu-id="4e347-266">If you notice that hello original list formatting is still there in hello mobile browser and wonder what happened tooyour nice Bootstrap styling, this is an artifact of your earlier action toocreate mobile specific views.</span></span> <span data-ttu-id="4e347-267">Ancak, hello önyükleme CSS framework toocreate yanıt veren web tasarımı kullanıyorsanız, head gidin ve bu mobile özgü görünümler ve hello mobile özgü Düzen görünümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="4e347-267">However, now that you are using hello Bootstrap CSS framework toocreate a responsive web design, go head and remove these mobile-specific views and hello mobile-specific layout views.</span></span> <span data-ttu-id="4e347-268">Bunu yaptıktan sonra hello yenilendi mobil tarayıcı hello önyükleme stil gösterir.</span><span class="sxs-lookup"><span data-stu-id="4e347-268">Once you have done so, hello refreshed mobile browser will show hello Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="4e347-269"><a name="bkmk_improvedates"></a>Merhaba tarihleri listesi geliştirmek</span><span class="sxs-lookup"><span data-stu-id="4e347-269"><a name="bkmk_improvedates"></a> Improve hello Dates List</span></span>
<span data-ttu-id="4e347-270">Merhaba artırabilir *tarihleri* hello geliştirilmiş gibi görüntülemek *konuşmacılar* ve *etiketleri* daha önce ancak aşağıdaki hello açıklanan hello kod değişiklikleri kullanırsanızgörünümleri`Html.ActionLink` yöntemi sözdiziminde *görünümleri\\giriş\\AllDates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="4e347-270">You can improve hello *Dates* view like you improved hello *Speakers* and *Tags* views if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="4e347-271">Böyle bir yenilenen mobil tarayıcı görünümü alırsınız:</span><span class="sxs-lookup"><span data-stu-id="4e347-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="4e347-272">Daha fazla hello artırabilir *tarihleri* tarihe göre hello tarih-saat değerlerini düzenleme görünümü.</span><span class="sxs-lookup"><span data-stu-id="4e347-272">You can further improve hello *Dates* view by organizing hello date-time values by date.</span></span> <span data-ttu-id="4e347-273">Bu önyükleme hello ile yapılabilir [paneller] [ panels] stil oluşturma.</span><span class="sxs-lookup"><span data-stu-id="4e347-273">This can be done with hello Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="4e347-274">Merhaba Hello içeriğini değiştirin *görünümleri\\giriş\\AllDates.cshtml* aşağıdaki kod ile dosya:</span><span class="sxs-lookup"><span data-stu-id="4e347-274">Replace hello contents of hello *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

<span data-ttu-id="4e347-275">Bu kod ayrı bir oluşturur `<div class="panel panel-primary">` her farklı tarih hello listesi ve kullandığı hello için etiket [bağlantılı listesi grubu] [ linked list group] ilgili için bağlantılar olarak önce.</span><span class="sxs-lookup"><span data-stu-id="4e347-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in hello list, and uses hello [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="4e347-276">Bu kod çalıştığında gibi görünüyor hangi hello mobil tarayıcı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="4e347-276">Here's what hello mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="4e347-277">Anahtar toohello Masaüstü tarayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4e347-277">Switch toohello desktop browser.</span></span> <span data-ttu-id="4e347-278">Yeniden hello tutarlı bir görünüm unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4e347-278">Again, note hello consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="4e347-279"><a name="bkmk_improvesessionstable"></a>Merhaba SessionsTable görünüm geliştirmek</span><span class="sxs-lookup"><span data-stu-id="4e347-279"><a name="bkmk_improvesessionstable"></a> Improve hello SessionsTable View</span></span>
<span data-ttu-id="4e347-280">Bu bölümde, hello yapacağız *SessionsTable* daha fazla mobil dostu görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="4e347-280">In this section, you'll make hello *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="4e347-281">Daha kapsamlı hello önceki değişiklikler değişikliktir.</span><span class="sxs-lookup"><span data-stu-id="4e347-281">This change is more extensive hello previous changes.</span></span>

<span data-ttu-id="4e347-282">Merhaba mobil tarayıcıda hello dokunun **etiketi** düğmesine ve ardından girin `asp` arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="4e347-282">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="4e347-283">Merhaba dokunun **ASP.NET** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="4e347-283">Tap hello **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="4e347-284">Gördüğünüz gibi hello görüntü şu anda tasarlanmış toobe hello Masaüstü tarayıcıda görüntülenen olan bir tablo olarak biçimlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4e347-284">As you can see, hello display is formatted as a table, which is currently designed toobe viewed in hello desktop browser.</span></span> <span data-ttu-id="4e347-285">Ancak, bir mobil tarayıcı üzerinde biraz zor tooread olur.</span><span class="sxs-lookup"><span data-stu-id="4e347-285">However, it's a little bit difficult tooread on a mobile browser.</span></span> <span data-ttu-id="4e347-286">toofix Bu, açık *görünümleri\\giriş\\SessionsTable.cshtml* ve ardından dosya Merhaba içeriğine koddan hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4e347-286">toofix this, open *Views\\Home\\SessionsTable.cshtml* and then replace hello contents of the file with hello following code:</span></span>

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

<span data-ttu-id="4e347-287">Merhaba kod 3 işlemi yapar:</span><span class="sxs-lookup"><span data-stu-id="4e347-287">hello code does 3 things:</span></span>

* <span data-ttu-id="4e347-288">kullandığı hello önyükleme [özel bağlantılı listesi grubu] [ custom linked list group] bu bilgileri (sınıflar gibi kullanarak bir mobil tarayıcı üzerinde okunabilir olmasını sağlamak tooformat oturum bilgilerini dikey olarak hello. Liste-Grup-öğesi-metin)</span><span class="sxs-lookup"><span data-stu-id="4e347-288">uses hello Bootstrap [custom linked list group][custom linked list group] tooformat hello session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="4e347-289">Merhaba geçerlidir [kılavuz sistem] [ grid system] toothe düzeni, bu nedenle bu hello oturum öğelerini akış yatay tarayıcıda hello Masaüstü ve dikey olarak hello mobil tarayıcıda (Merhaba sütun md 4 sınıfı kullanarak)</span><span class="sxs-lookup"><span data-stu-id="4e347-289">applies hello [grid system][grid system] toothe layout, so that hello session items flow horizontally in hello desktop browser and vertically in hello mobile browser (using hello col-md-4 class)</span></span>
* <span data-ttu-id="4e347-290">kullandığı hello [esnek yardımcı programları] [ responsive utilities] (Merhaba gizli xs sınıfı kullanarak) hello mobil tarayıcıda görüntülendiğinde hello oturum etiketlerini gizlemek için</span><span class="sxs-lookup"><span data-stu-id="4e347-290">uses hello [responsive utilities][responsive utilities] to hide hello session tags when viewed in hello mobile browser (using hello hidden-xs class)</span></span>

<span data-ttu-id="4e347-291">Ayrıca bir başlık bağlantı toogo toohello ilgili oturumu dokunabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e347-291">You can also tap a title link toogo toohello respective session.</span></span> <span data-ttu-id="4e347-292">Aşağıdaki Hello görüntü hello kod değişiklikleri yansıtır.</span><span class="sxs-lookup"><span data-stu-id="4e347-292">hello image below reflects hello code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="4e347-293">otomatik olarak uygulanan hello önyükleme kılavuz sistem hello mobil tarayıcı oturumlarında dikey düzenler.</span><span class="sxs-lookup"><span data-stu-id="4e347-293">hello Bootstrap grid system that you applied automatically arranges the sessions vertically in hello mobile browser.</span></span> <span data-ttu-id="4e347-294">Ayrıca, hello etiketleri gösterilmez dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="4e347-294">Also, notice that hello tags are not shown.</span></span> <span data-ttu-id="4e347-295">Anahtar toohello Masaüstü tarayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4e347-295">Switch toohello desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="4e347-296">Merhaba Masaüstü tarayıcıda hello etiketleri şimdi görüntülenen dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="4e347-296">In hello desktop browser, notice that hello tags are now displayed.</span></span> <span data-ttu-id="4e347-297">Ayrıca, uyguladığınız hello önyükleme kılavuz sistem hello oturum öğeleri iki sütunlardaki düzenler görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e347-297">Also, you can see that hello Bootstrap grid system you applied arranges hello session items in two columns.</span></span> <span data-ttu-id="4e347-298">Tarayıcı büyütmek, hello düzenleme toothree sütunları değiştiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4e347-298">If you enlarge the browser, you will see that hello arrangement changes toothree columns.</span></span>

## <span data-ttu-id="4e347-299"><a name="bkmk_improvesessionbycode"></a>Merhaba SessionByCode görünüm geliştirmek</span><span class="sxs-lookup"><span data-stu-id="4e347-299"><a name="bkmk_improvesessionbycode"></a> Improve hello SessionByCode View</span></span>
<span data-ttu-id="4e347-300">Son olarak, hello düzeltme *SessionByCode* toomake görüntülemek, mobil dostu.</span><span class="sxs-lookup"><span data-stu-id="4e347-300">Finally, you'll fix hello *SessionByCode* view toomake it mobile-friendly.</span></span>

<span data-ttu-id="4e347-301">Merhaba mobil tarayıcıda hello dokunun **etiketi** düğmesine ve ardından girin `asp` arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="4e347-301">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="4e347-302">Merhaba dokunun **ASP.NET** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="4e347-302">Tap hello **ASP.NET** link.</span></span> <span data-ttu-id="4e347-303">Merhaba ASP.NET etiketi oturumlar görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4e347-303">Sessions for hello ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="4e347-304">Merhaba seçin **ASP.NET ve AngularJS ile tek sayfa uygulaması oluşturma** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="4e347-304">Choose hello **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="4e347-305">Merhaba varsayılan masaüstü görünümünde sorun yoktur, ancak bazı önyükleme GUI bileşenlerini kullanarak hello görünüm kolayca artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e347-305">hello default desktop view is fine, but you can improve hello look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="4e347-306">Açık *görünümleri\\giriş\\SessionByCode.cshtml* ve hello içeriği biçimlendirme aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4e347-306">Open *Views\\Home\\SessionByCode.cshtml* and replace hello contents with hello following markup:</span></span>

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

<span data-ttu-id="4e347-307">Merhaba yeni markup tooimprove hello mobil görüntüle stil oluşturma önyükleme paneller kullanır.</span><span class="sxs-lookup"><span data-stu-id="4e347-307">hello new markup uses Bootstrap panels styling tooimprove hello mobile view.</span></span> 

<span data-ttu-id="4e347-308">Merhaba mobil tarayıcıyı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="4e347-308">Refresh hello mobile browser.</span></span> <span data-ttu-id="4e347-309">Merhaba aşağıdaki görüntüde yaptığınız hello kod değişiklikleri yansıtır:</span><span class="sxs-lookup"><span data-stu-id="4e347-309">hello following image reflects hello code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="4e347-310">Kaydırma ve gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="4e347-310">Wrap Up and Review</span></span>
<span data-ttu-id="4e347-311">Bu öğretici, nasıl göstermiştir toouse ASP.NET MVC 5 toodevelop mobil dostu Web uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="4e347-311">This tutorial has shown you how toouse ASP.NET MVC 5 toodevelop mobile-friendly Web applications.</span></span> <span data-ttu-id="4e347-312">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="4e347-312">These include:</span></span>

* <span data-ttu-id="4e347-313">Bir ASP.NET MVC 5 uygulama tooan App Service web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="4e347-313">Deploy an ASP.NET MVC 5 application tooan App Service web app</span></span>
* <span data-ttu-id="4e347-314">MVC 5 uygulamanızda önyükleme toocreate yanıt veren web düzenini kullanın</span><span class="sxs-lookup"><span data-stu-id="4e347-314">Use Bootstrap toocreate responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="4e347-315">Düzen, görünümleri ve kısmi görünümler, hem genel hem de tek bir görünümü için geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="4e347-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="4e347-316">Denetim düzenini ve kısmi geçersiz kılma zorlama kullanarak `RequireConsistentDisplayMode` özelliği</span><span class="sxs-lookup"><span data-stu-id="4e347-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="4e347-317">Merhaba iPhone tarayıcısı gibi belirli tarayıcılar hedef görünümlerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e347-317">Create views that target specific browsers, such as hello iPhone browser</span></span>
* <span data-ttu-id="4e347-318">Razor kodunda önyükleme Stil Uygula</span><span class="sxs-lookup"><span data-stu-id="4e347-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="4e347-319">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="4e347-319">See Also</span></span>
* [<span data-ttu-id="4e347-320">yanıt veren web tasarımı 9 temel ilkeleri</span><span class="sxs-lookup"><span data-stu-id="4e347-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="4e347-321">[Önyükleme][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="4e347-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="4e347-322">[Resmi önyükleme blogu][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="4e347-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="4e347-323">[Öğretici Cumhuriyeti gelen twitter Bootstrap Öğreticisi][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="4e347-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="4e347-324">[Merhaba önyükleme Playground][hello Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="4e347-324">[hello Bootstrap Playground][hello Bootstrap Playground]</span></span>
* <span data-ttu-id="4e347-325">[W3C öneri mobil Web uygulaması en iyi uygulamalar][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="4e347-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="4e347-326">[Medya sorgular için W3C adayı önerisi][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="4e347-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="4e347-327">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="4e347-327">What's changed</span></span>
* <span data-ttu-id="4e347-328">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="4e347-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

