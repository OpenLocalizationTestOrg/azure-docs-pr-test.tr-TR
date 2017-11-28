---
title: "aaaDeploy hello beş dakikada Azure portalında bir Umbraco web uygulamasında | Microsoft Docs"
description: "Ne kadar kolay toorun App Service'te web uygulamalarını örnek bir ASP.NET uygulaması dağıtarak olduğunu öğrenin. Sonuçları anında görün."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="f990f-104">Beş dakika içinde bir hello Azure portal Umbraco web uygulamasında dağıtma</span><span class="sxs-lookup"><span data-stu-id="f990f-104">Deploy an Umbraco web app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="f990f-105">Bu öğretici n dağıtmanıza yardımcı olan [Umbraco](https://our.umbraco.org/) çok web uygulaması[Azure App Service](../app-service/app-service-value-prop-what-is.md) dakika.</span><span class="sxs-lookup"><span data-stu-id="f990f-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Umbraco uygulaması](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="f990f-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f990f-107">Prerequisites</span></span>
<span data-ttu-id="f990f-108">Bir Microsoft Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f990f-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="f990f-109">Bir hesabınız yoksa, [ücretsiz deneme için kaydolabilir](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone avantajlarınızı etkinleştirebilirsiniz.](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="f990f-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="f990f-110">Azure hesabınız olmadan [App Service'i Deneyebilirsiniz](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="f990f-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="f990f-111">Bir başlangıç uygulaması oluşturun ve tooan saat--beraberinde, gerekli herhangi bir kredi kartı veya bir taahhüt yürütebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f990f-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-aspnet-app"></a><span data-ttu-id="f990f-112">Merhaba ASP.NET uygulamasını dağıtma</span><span class="sxs-lookup"><span data-stu-id="f990f-112">Deploy hello ASP.NET app</span></span>
1. <span data-ttu-id="f990f-113">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f990f-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f990f-114">[https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS) adresini açın.</span><span class="sxs-lookup"><span data-stu-id="f990f-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="f990f-115">Bu bir kısayol tooimmediately hello Azure portalında yeni bir Umbraco uygulaması yapılandırma bağlantıdır.</span><span class="sxs-lookup"><span data-stu-id="f990f-115">This link is a shortcut tooimmediately configure a new Umbraco app in hello Azure portal.</span></span>

3. <span data-ttu-id="f990f-116">**Uygulama adı** bölümünde bir web uygulaması adı girin.</span><span class="sxs-lookup"><span data-stu-id="f990f-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="f990f-117">Merhaba adı hello benzersiz ise hello kutusunda yeşil bir onay işareti görürsünüz `azurewebsites.net` etki alanı.</span><span class="sxs-lookup"><span data-stu-id="f990f-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="f990f-118">İçinde **kaynak grubu**, tıklatın **Yeni Oluştur** yeni bir toocreate [kaynak grubu](../azure-resource-manager/resource-group-overview.md), bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="f990f-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="f990f-119">**App Service planı/Konum** > **Yeni Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f990f-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="f990f-120">Merhaba yapılandırma [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="f990f-120">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="f990f-121">İçinde **uygulama hizmeti planı**, türü hello istenen adı.</span><span class="sxs-lookup"><span data-stu-id="f990f-121">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="f990f-122">İçinde **konumu**, bir konum toohost planınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="f990f-122">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="f990f-123">**Fiyatlandırma katmanı**'na tıklayıp **F1 Ücretsiz** veya uygun bulduğunuz başka bir katmanı seçin ve **Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f990f-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="f990f-124">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f990f-124">Click **OK**.</span></span>

    <span data-ttu-id="f990f-125">Umbraco CMS yapılandırmanızı hello ekran aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="f990f-125">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Yapılandırma devam ediyor - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="f990f-127">**SQL Veritabanı** > **Yeni veritabanı oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f990f-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="f990f-128">SQL veritabanı Hello gösterildiği gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f990f-128">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="f990f-129">**Ad** alanına **myDB** gibi bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="f990f-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="f990f-130">**Fiyatlandırma katmanı**'na tıklayıp **F Ücretsiz** veya uygun bulduğunuz başka bir katmanı seçin ve **Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f990f-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="f990f-131">**Hedef sunucu** > **Yeni sunucu oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f990f-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="f990f-132">Merhaba veritabanı sunucusu gösterildiği gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f990f-132">Configure hello database server as shown:</span></span>

        - <span data-ttu-id="f990f-133">**Sunucu adı** alanına bir sunucu adı yazın.</span><span class="sxs-lookup"><span data-stu-id="f990f-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="f990f-134">Merhaba adı hello benzersiz ise hello kutusunda yeşil bir onay işareti görürsünüz `.database.windows.net` etki alanı.</span><span class="sxs-lookup"><span data-stu-id="f990f-134">You will see a green checkmark in hello box if hello name is unique in hello `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="f990f-135">İçinde **Sunucu Yöneticisi oturum açma**, türü hello istenen yöneticinin kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="f990f-135">In **Server admin login**, type hello desired admininistrator username.</span></span>
        - <span data-ttu-id="f990f-136">İçinde **parola** ve **parolayı onayla**, hello istediğiniz parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="f990f-136">In **Password** and **Confirm password**, type hello desired password.</span></span>
        - <span data-ttu-id="f990f-137">Konumunda, select hello web uygulaması için kullandığınız aynı konuma hello.</span><span class="sxs-lookup"><span data-stu-id="f990f-137">In Location, select hello same location you use for hello web app.</span></span>
        - <span data-ttu-id="f990f-138">Emin olun **izin azure Hizmetleri tooaccess sunucusu** seçilir.</span><span class="sxs-lookup"><span data-stu-id="f990f-138">Make sure **Allow azure services tooaccess server** is selected.</span></span>
        - <span data-ttu-id="f990f-139">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f990f-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="f990f-140">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f990f-140">Click **Select**.</span></span>

13. <span data-ttu-id="f990f-141">Tıklatın **Web uygulaması ayarları**hello veritabanı kullanıcı adı ve parola belirtin ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f990f-141">Click **Web app settings**, specify hello database username and password, and click **OK**.</span></span>

    <span data-ttu-id="f990f-142">Umbraco CMS yapılandırmanızı hello ekran aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="f990f-142">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Yapılandırma tamamlandı - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="f990f-144">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f990f-144">Click **Create**.</span></span>
    
    <span data-ttu-id="f990f-145">Azure şimdi yapılandırmanızı temel alarak Umbraco uygulamanızı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f990f-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="f990f-146">**Dağıtım başlatıldı...** bildirimini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f990f-146">You should see a **Deployment started...** notification.</span></span>

    ![Dağıtım başarılı - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="f990f-148">Umrbaco web uygulamanızı başlatma ve yönetme</span><span class="sxs-lookup"><span data-stu-id="f990f-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="f990f-149">Azure uygulama dağıtımını tamamladığında başka bir bildirim daha göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="f990f-149">When Azure completes app deployment you see another notification.</span></span>

![Dağıtım başarılı - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="f990f-151">Merhaba bildirime tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f990f-151">Click hello notification.</span></span> <span data-ttu-id="f990f-152">Bu eksik, her zaman hello bildirim zil tıklayarak erişebildiğinizi (![bildirim aşağıdaki - Azure App Service'te ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="f990f-152">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="f990f-153">Şimdi web uygulamasının yönetim [dikey penceresini](../azure-resource-manager/resource-group-portal.md#manage-resources) (*dikey pencere*: dikey olarak açılan portal sayfası) görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f990f-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="f990f-154">Merhaba genel bakış sayfası Hello üst tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="f990f-154">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Göz at - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="f990f-156">Merhaba Umbraco gördüğünüz artık **Hoş Geldiniz** sayfası.</span><span class="sxs-lookup"><span data-stu-id="f990f-156">Now you see hello Umbraco **Welcome** page.</span></span> <span data-ttu-id="f990f-157">Merhaba Umbraco yükleme yapılandırmak ve onunla yürütmeye başlayın!</span><span class="sxs-lookup"><span data-stu-id="f990f-157">Configure hello Umbraco installation and start playing with it!</span></span>

    ![Umbraco yapılandırması - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="f990f-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f990f-159">Next steps</span></span>
* <span data-ttu-id="f990f-160">[Bir ASP.NET web uygulaması tooAzure App Service, Visual Studio kullanarak dağıtmak](app-service-web-get-started-dotnet.md) -toocreate hello herhangi birini kullanarak Visual Studio'da yeni bir Azure web uygulaması uygulama şablonları nasıl dahil öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f990f-160">[Deploy an ASP.NET web app tooAzure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how toocreate a new Azure web app from Visual Studio, using any one of hello included application templates.</span></span>
* <span data-ttu-id="f990f-161">[Kod tooAzure uygulama hizmeti dağıtmak](web-sites-deploy.md)-toodeploy FTP ya da kaynak havuzları nasıl kontrol öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f990f-161">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="f990f-162">[İşlevselliği tooyour ilk web uygulamanız eklemek](app-service-web-get-started-2.md) -Azure uygulaması toohello sonraki düzeye taşıyın.</span><span class="sxs-lookup"><span data-stu-id="f990f-162">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="f990f-163">Kullanıcılarınızın kimliklerini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f990f-163">Authenticate your users.</span></span> <span data-ttu-id="f990f-164">Talebe göre ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="f990f-164">Scale it based on demand.</span></span> <span data-ttu-id="f990f-165">Performans uyarıları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f990f-165">Set up some performance alerts.</span></span> <span data-ttu-id="f990f-166">Tümünü birkaç tıklamayla gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="f990f-166">All with a few clicks.</span></span>
