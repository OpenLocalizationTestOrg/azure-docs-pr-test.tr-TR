---
title: "Beş dakikada Azure portalında bir Umbraco web uygulaması dağıtma | Microsoft Docs"
description: "Örnek ASP.NET uygulamasını dağıtarak, App Service'te web uygulamaları çalıştırmanın ne kadar kolay olduğunu öğrenin. Sonuçları anında görün."
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
ms.openlocfilehash: 9e3e2130a66cdfe5f06eb3b366e53028c44e7e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-umbraco-web-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="8c7e1-104">Beş dakikada Azure portalında bir Umbraco web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="8c7e1-104">Deploy an Umbraco web app in the Azure portal in five minutes</span></span>

<span data-ttu-id="8c7e1-105">Bu öğretici, [Azure App Service](../app-service/app-service-value-prop-what-is.md)'te dakikalar içinde bir [Umbraco](https://our.umbraco.org/) web uygulaması dağıtmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Umbraco uygulaması](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="8c7e1-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8c7e1-107">Prerequisites</span></span>
<span data-ttu-id="8c7e1-108">Bir Microsoft Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="8c7e1-109">Bir hesabınız yoksa, [ücretsiz deneme için kaydolabilir](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone avantajlarınızı etkinleştirebilirsiniz.](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="8c7e1-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="8c7e1-110">Azure hesabınız olmadan [App Service'i Deneyebilirsiniz](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="8c7e1-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="8c7e1-111">Başlangıç uygulaması oluşturun ve bir saate kadar üzerinde çalışın; kredi kartı veya taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-aspnet-app"></a><span data-ttu-id="8c7e1-112">ASP.NET uygulamasını dağıtma</span><span class="sxs-lookup"><span data-stu-id="8c7e1-112">Deploy the ASP.NET app</span></span>
1. <span data-ttu-id="8c7e1-113">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="8c7e1-114">[https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS) adresini açın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="8c7e1-115">Bu bağlantı, Azure portalında yeni bir Umbraco uygulaması yapılandırma sayfasına hemen geçmenizi sağlayan bir kısayoldur.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-115">This link is a shortcut to immediately configure a new Umbraco app in the Azure portal.</span></span>

3. <span data-ttu-id="8c7e1-116">**Uygulama adı** bölümünde bir web uygulaması adı girin.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="8c7e1-117">Girdiğiniz ad `azurewebsites.net` etki alanında benzersizse kutuda yeşil renkli bir onay işareti göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="8c7e1-118">**Kaynak Grubu**'nda **Yeni oluştur**'a tıklayarak yeni bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) oluşturun ve ad verin.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="8c7e1-119">**App Service planı/Konum** > **Yeni Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="8c7e1-120">[App Service planını](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) gösterilen şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="8c7e1-120">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="8c7e1-121">**App Service planı** alanına istediğiniz adı girin.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-121">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="8c7e1-122">**Konum** alanında planınızın barındırılacağı konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-122">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="8c7e1-123">**Fiyatlandırma katmanı**'na tıklayıp **F1 Ücretsiz** veya uygun bulduğunuz başka bir katmanı seçin ve **Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="8c7e1-124">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-124">Click **OK**.</span></span>

    <span data-ttu-id="8c7e1-125">Umbraco CMS yapılandırmanız aşağıdaki ekran görüntüsündeki gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="8c7e1-125">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Yapılandırma devam ediyor - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="8c7e1-127">**SQL Veritabanı** > **Yeni veritabanı oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="8c7e1-128">SQL Veritabanını gösterilen şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="8c7e1-128">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="8c7e1-129">**Ad** alanına **myDB** gibi bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="8c7e1-130">**Fiyatlandırma katmanı**'na tıklayıp **F Ücretsiz** veya uygun bulduğunuz başka bir katmanı seçin ve **Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="8c7e1-131">**Hedef sunucu** > **Yeni sunucu oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="8c7e1-132">Veritabanı sunucusunu gösterilen şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="8c7e1-132">Configure the database server as shown:</span></span>

        - <span data-ttu-id="8c7e1-133">**Sunucu adı** alanına bir sunucu adı yazın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="8c7e1-134">Girdiğiniz ad `.database.windows.net` etki alanında benzersizse kutuda yeşil renkli bir onay işareti göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-134">You will see a green checkmark in the box if the name is unique in the `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="8c7e1-135">**Sunucu yöneticisi oturum açma** alanına istediğiniz yönetici kullanıcı adını girin.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-135">In **Server admin login**, type the desired admininistrator username.</span></span>
        - <span data-ttu-id="8c7e1-136">**Parola** ve **Parola onayı** alanlarına istediğiniz parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-136">In **Password** and **Confirm password**, type the desired password.</span></span>
        - <span data-ttu-id="8c7e1-137">Konum alanında web uygulaması için seçtiğiniz konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-137">In Location, select the same location you use for the web app.</span></span>
        - <span data-ttu-id="8c7e1-138">**Azure hizmetlerinin sunucuya erişmesine izin ver** seçeneğinin işaretlenmiş olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-138">Make sure **Allow azure services to access server** is selected.</span></span>
        - <span data-ttu-id="8c7e1-139">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="8c7e1-140">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-140">Click **Select**.</span></span>

13. <span data-ttu-id="8c7e1-141">**Web uygulaması ayarları**'na tıklayın, veritabanı kullanıcı adını ve parolasını belirtin ve **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-141">Click **Web app settings**, specify the database username and password, and click **OK**.</span></span>

    <span data-ttu-id="8c7e1-142">Umbraco CMS yapılandırmanız aşağıdaki ekran görüntüsündeki gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="8c7e1-142">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![Yapılandırma tamamlandı - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="8c7e1-144">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-144">Click **Create**.</span></span>
    
    <span data-ttu-id="8c7e1-145">Azure şimdi yapılandırmanızı temel alarak Umbraco uygulamanızı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="8c7e1-146">**Dağıtım başlatıldı...** bildirimini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-146">You should see a **Deployment started...** notification.</span></span>

    ![Dağıtım başarılı - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="8c7e1-148">Umrbaco web uygulamanızı başlatma ve yönetme</span><span class="sxs-lookup"><span data-stu-id="8c7e1-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="8c7e1-149">Azure uygulama dağıtımını tamamladığında başka bir bildirim daha göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-149">When Azure completes app deployment you see another notification.</span></span>

![Dağıtım başarılı - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="8c7e1-151">Bildirime tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-151">Click the notification.</span></span> <span data-ttu-id="8c7e1-152">Bildirimi kaçırırsanız çan simgesine tıklayarak erişebilirsiniz (![Bildirim - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="8c7e1-152">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="8c7e1-153">Şimdi web uygulamasının yönetim [dikey penceresini](../azure-resource-manager/resource-group-portal.md#manage-resources) (*dikey pencere*: dikey olarak açılan portal sayfası) görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="8c7e1-154">Genel bakış sayfasının en üstünde yer alan **Göz at**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-154">In the top of the Overview page, click **Browse**.</span></span>
   
    ![Göz at - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="8c7e1-156">Şimdi Umbraco **Karşılama** sayfasını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-156">Now you see the Umbraco **Welcome** page.</span></span> <span data-ttu-id="8c7e1-157">Umbraco yüklemesini yapılandırın ve kurcalamaya başlayın!</span><span class="sxs-lookup"><span data-stu-id="8c7e1-157">Configure the Umbraco installation and start playing with it!</span></span>

    ![Umbraco yapılandırması - Azure App Service’teki ilk Umbraco](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="8c7e1-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8c7e1-159">Next steps</span></span>
* <span data-ttu-id="8c7e1-160">[Visual Studio'yu kullanarak Azure App Service’e bir ASP.NET Web uygulaması dağıtma](app-service-web-get-started-dotnet.md) - Mevcut uygulama şablonlarından birini kullanarak Visual Studio'dan yeni bir Azure web uygulaması oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-160">[Deploy an ASP.NET web app to Azure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how to create a new Azure web app from Visual Studio, using any one of the included application templates.</span></span>
* <span data-ttu-id="8c7e1-161">[Kodunuzu Azure App Service’e dağıtma](web-sites-deploy.md): FTP veya kaynak denetim depolarından dağıtım yapmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-161">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="8c7e1-162">[İlk web uygulamanıza işlevsellik ekleme](app-service-web-get-started-2.md): Azure uygulamanızı bir sonraki seviyeye taşıyın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-162">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="8c7e1-163">Kullanıcılarınızın kimliklerini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-163">Authenticate your users.</span></span> <span data-ttu-id="8c7e1-164">Talebe göre ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-164">Scale it based on demand.</span></span> <span data-ttu-id="8c7e1-165">Performans uyarıları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-165">Set up some performance alerts.</span></span> <span data-ttu-id="8c7e1-166">Tümünü birkaç tıklamayla gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-166">All with a few clicks.</span></span>
