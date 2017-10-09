---
title: "aaaDeploy hello beş dakikada Azure portalında WordPress uygulamasında | Microsoft Docs"
description: "Ne kadar kolay toorun web uygulamaları App Service'te bir WordPress uygulaması dağıtarak olduğunu öğrenin. Sonuçları anında görün."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="73b09-104">Hello Azure portal WordPress uygulamasında beş dakika içinde dağıtma</span><span class="sxs-lookup"><span data-stu-id="73b09-104">Deploy a WordPress app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="73b09-105">Bu öğretici şunların nasıl yapıldığını gösterir toodeploy ilk [WordPress](https://wordpress.org/) çok web uygulaması[Azure App Service](../app-service/app-service-value-prop-what-is.md) dakika.</span><span class="sxs-lookup"><span data-stu-id="73b09-105">This tutorial shows you how toodeploy your first [WordPress](https://wordpress.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![WordPress sitesi](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="73b09-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="73b09-107">Prerequisites</span></span>
<span data-ttu-id="73b09-108">Bir Microsoft Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="73b09-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="73b09-109">Bir hesabınız yoksa, [ücretsiz deneme için kaydolabilir](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone avantajlarınızı etkinleştirebilirsiniz.](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="73b09-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="73b09-110">Azure hesabınız olmadan [App Service'i Deneyebilirsiniz](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="73b09-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="73b09-111">Bir başlangıç uygulaması oluşturun ve tooan saat--beraberinde, gerekli herhangi bir kredi kartı veya bir taahhüt yürütebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73b09-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-wordpress-app"></a><span data-ttu-id="73b09-112">Merhaba WordPress uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="73b09-112">Deploy hello WordPress app</span></span>
1. <span data-ttu-id="73b09-113">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="73b09-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="73b09-114">[https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress) adresini açın.</span><span class="sxs-lookup"><span data-stu-id="73b09-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="73b09-115">Bu bir kısayol tooimmediately hello Azure portalında yeni bir WordPress uygulaması yapılandırma bağlantıdır.</span><span class="sxs-lookup"><span data-stu-id="73b09-115">This link is a shortcut tooimmediately configure a new WordPress app in hello Azure portal.</span></span>

3. <span data-ttu-id="73b09-116">**Uygulama adı** bölümünde bir web uygulaması adı girin.</span><span class="sxs-lookup"><span data-stu-id="73b09-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="73b09-117">Merhaba adı hello benzersiz ise hello kutusunda yeşil bir onay işareti görürsünüz `azurewebsites.net` etki alanı.</span><span class="sxs-lookup"><span data-stu-id="73b09-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="73b09-118">İçinde **kaynak grubu**, tıklatın **Yeni Oluştur** yeni bir toocreate [kaynak grubu](../azure-resource-manager/resource-group-overview.md), bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="73b09-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="73b09-119">**Veritabanı Sağlayıcısı**'nda **CleaDB**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="73b09-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="73b09-120">**App Service planı/Konum** > **Yeni Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73b09-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="73b09-121">Merhaba yapılandırma [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="73b09-121">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="73b09-122">İçinde **uygulama hizmeti planı**, türü hello istenen adı.</span><span class="sxs-lookup"><span data-stu-id="73b09-122">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="73b09-123">İçinde **konumu**, bir konum toohost planınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="73b09-123">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="73b09-124">**Fiyatlandırma katmanı**'na tıklayıp **F1 Ücretsiz** veya uygun bulduğunuz başka bir katmanı seçin ve **Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73b09-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="73b09-125">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73b09-125">Click **OK**.</span></span>

8. <span data-ttu-id="73b09-126">**Veritabanı** > **Yeni Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73b09-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="73b09-127">SQL veritabanı Hello gösterildiği gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="73b09-127">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="73b09-128">**Veritabanı Adı** alanına bir veritabanı adı yazın.</span><span class="sxs-lookup"><span data-stu-id="73b09-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="73b09-129">İçinde **konumu**, seçin hello hello uygulama hizmeti planı aynı konumda.</span><span class="sxs-lookup"><span data-stu-id="73b09-129">In **Location**, choose hello same location as hello App Service plan.</span></span>
    - <span data-ttu-id="73b09-130">**Fiyatlandırma katmanı**'na tıklayıp **Mercury** veya uygun bulduğunuz başka bir katmanı seçin ve **Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73b09-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="73b09-131">**Yasal Koşullar**'a ve **Satın Al**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73b09-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="73b09-132">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73b09-132">Click **OK**.</span></span>

9. <span data-ttu-id="73b09-133">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73b09-133">Click **Create**.</span></span>

    <span data-ttu-id="73b09-134">Azure şimdi yapılandırmanızı temel alarak WordPress uygulamanızı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="73b09-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="73b09-135">**Dağıtım başlatıldı...** bildirimini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="73b09-135">You should see a **Deployment started...** notification.</span></span>

    ![Dağıtım başladı - Azure App Service’teki ilk WordPress uygulaması](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="73b09-137">WordPress web uygulamanızı başlatma ve yönetme</span><span class="sxs-lookup"><span data-stu-id="73b09-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="73b09-138">Azure uygulama dağıtımını tamamladığında başka bir bildirim daha göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="73b09-138">When Azure completes app deployment you see another notification.</span></span>

![Dağıtım başarılı - Azure App Service’teki ilk WordPress uygulaması](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="73b09-140">Merhaba bildirime tıklayın.</span><span class="sxs-lookup"><span data-stu-id="73b09-140">Click hello notification.</span></span> <span data-ttu-id="73b09-141">Bu eksik, her zaman hello bildirim zil tıklayarak erişebildiğinizi (![bildirim aşağıdaki - Azure App Service'te ilk WordPress](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="73b09-141">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="73b09-142">Şimdi web uygulamasının yönetim [dikey penceresini](../azure-resource-manager/resource-group-portal.md#manage-resources) (*dikey pencere*: dikey olarak açılan portal sayfası) görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="73b09-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="73b09-143">Merhaba genel bakış sayfası Hello üst tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="73b09-143">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Göz at - Azure App Service’teki ilk WordPress](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="73b09-145">Merhaba WordPress gördüğünüz artık **Hoş Geldiniz** sayfası.</span><span class="sxs-lookup"><span data-stu-id="73b09-145">Now you see hello WordPress **Welcome** page.</span></span> <span data-ttu-id="73b09-146">Merhaba WordPress yüklemesini yapılandırmak ve onunla yürütmeye başlayın!</span><span class="sxs-lookup"><span data-stu-id="73b09-146">Configure hello WordPress installation and start playing with it!</span></span>

    ![WordPress yapılandırması - Azure App Service’teki ilk WordPress](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="73b09-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="73b09-148">Next steps</span></span>
* <span data-ttu-id="73b09-149">[Oluşturma, yapılandırma ve Laravel web uygulama tooAzure dağıtma](app-service-web-php-get-started.md) -ihtiyacınız toorun Azure, herhangi bir PHP web uygulamasına gibi hello temel becerileri öğrenin:</span><span class="sxs-lookup"><span data-stu-id="73b09-149">[Create, configure, and deploy a Laravel web app tooAzure](app-service-web-php-get-started.md) - Learn hello basic skills you need toorun any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="73b09-150">Azure’da PowerShell/Bash uygulamaları oluşturma ve yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="73b09-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="73b09-151">PHP sürümünü ayarlama.</span><span class="sxs-lookup"><span data-stu-id="73b09-151">Set PHP version.</span></span>
    * <span data-ttu-id="73b09-152">Merhaba kök uygulama dizininde değil bir başlangıç dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="73b09-152">Use a start file that is not in hello root application directory.</span></span>
    * <span data-ttu-id="73b09-153">Composer otomasyonunu etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="73b09-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="73b09-154">Ortama özel değişkenlere erişme.</span><span class="sxs-lookup"><span data-stu-id="73b09-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="73b09-155">Sık karşılaşılan hataları giderme.</span><span class="sxs-lookup"><span data-stu-id="73b09-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="73b09-156">[Kod tooAzure uygulama hizmeti dağıtmak](web-sites-deploy.md)-toodeploy FTP ya da kaynak havuzları nasıl kontrol öğrenin.</span><span class="sxs-lookup"><span data-stu-id="73b09-156">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="73b09-157">[İşlevselliği tooyour ilk web uygulamanız eklemek](app-service-web-get-started-2.md) -Azure uygulaması toohello sonraki düzeye taşıyın.</span><span class="sxs-lookup"><span data-stu-id="73b09-157">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="73b09-158">Kullanıcılarınızın kimliklerini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="73b09-158">Authenticate your users.</span></span> <span data-ttu-id="73b09-159">Talebe göre ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="73b09-159">Scale it based on demand.</span></span> <span data-ttu-id="73b09-160">Performans uyarıları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="73b09-160">Set up some performance alerts.</span></span> <span data-ttu-id="73b09-161">Tümünü birkaç tıklamayla gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="73b09-161">All with a few clicks.</span></span>
