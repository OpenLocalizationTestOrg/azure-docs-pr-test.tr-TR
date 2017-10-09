---
title: "Azure App Service'te bir WordPress web uygulaması aaaCreate | Microsoft Docs"
description: "Nasıl toocreate yeni bir Azure web uygulaması hello Azure Portal'ı kullanarak WordPress blogu için öğrenin."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="9cdc8-103">Azure App Service’te bir WordPress web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cdc8-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="9cdc8-104">Bu öğretici nasıl toodeploy bir WordPress blog sitesi hello Azure Marketi gösterir.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-104">This tutorial shows how toodeploy a WordPress blog site from hello Azure Marketplace.</span></span>

<span data-ttu-id="9cdc8-105">Merhaba Bu öğreticiyi tamamladığınızda ve hello bulutta çalışan kendi WordPress blog sitenize sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-105">When you're done with hello tutorial you'll have your own WordPress blog site up and running in hello cloud.</span></span>

![WordPress sitesi](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="9cdc8-107">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="9cdc8-107">You'll learn:</span></span>

* <span data-ttu-id="9cdc8-108">Nasıl toofind hello Azure Marketi'nde bir uygulama şablonunda.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-108">How toofind an application template in hello Azure Marketplace.</span></span>
* <span data-ttu-id="9cdc8-109">Nasıl toocreate bir web uygulamasını Azure App Service, hello şablonunu temel alır.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-109">How toocreate a web app in Azure App Service that is based on hello template.</span></span>
* <span data-ttu-id="9cdc8-110">Nasıl tooconfigure Azure App Service ayarlarını hello yeni uygulama ve veritabanı web.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-110">How tooconfigure Azure App Service settings for hello new web app and database.</span></span>

<span data-ttu-id="9cdc8-111">Hello Azure Marketi çok çeşitli popüler web uygulamalarını Microsoft, üçüncü taraf şirketler ve açık kaynak yazılım girişimleri tarafından geliştirilen kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-111">hello Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="9cdc8-112">Merhaba web uygulamaları dahili çok çeşitli popüler uygulamayı üzerinde gibi [PHP](/develop/nodejs/) bu WordPress örneğinde [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), ve [Python](/develop/python/), az bir tooname.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-112">hello web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), tooname a few.</span></span> <span data-ttu-id="9cdc8-113">toocreate hello Azure Marketi hello Merhaba hello tarayıcının gereksinim duyduğunuz yazılım, yalnızca web uygulamasından [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9cdc8-113">toocreate a web app from hello Azure Marketplace hello only software you need is hello browser that you use for hello [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="9cdc8-114">Bu öğreticide dağıttığınız WordPress sitesi hello hello veritabanı için MySQL kullanır.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-114">hello WordPress site that you deploy in this tutorial uses MySQL for hello database.</span></span> <span data-ttu-id="9cdc8-115">Merhaba veritabanı için SQL veritabanı tooinstead kullanmak istiyorsanız, bkz: [proje Nami](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="9cdc8-115">If you wish tooinstead use SQL Database for hello database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="9cdc8-116">**Proje Nami** hello Market de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-116">**Project Nami** is also available through hello Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="9cdc8-117">toocomplete Bu öğreticide, bir Microsoft Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-117">toocomplete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="9cdc8-118">Bir hesabınız yoksa, [Visual Studio abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) veya [ücretsiz deneme için kaydolabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="9cdc8-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="9cdc8-119">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="9cdc8-119">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="9cdc8-120">Burada, App Service'te hemen bir kısa süreli başlangıç web uygulaması oluşturabilirsiniz; kredi kartı gerekmez ve hiçbir taahhüt yoktur.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="9cdc8-121">WordPress’i seçme ve Azure App Service için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9cdc8-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="9cdc8-122">İçinde toohello oturum [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9cdc8-122">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9cdc8-123">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-123">Click **New**.</span></span>
   
    ![Yeni Oluştur][5]
3. <span data-ttu-id="9cdc8-125">**WordPress**’i arayın ve ardından **WordPress**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="9cdc8-126">Toouse MySQL yerine SQL Database istiyorsanız, arama **proje Nami**.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-126">If you wish toouse SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![Listede WordPress][7]
4. <span data-ttu-id="9cdc8-128">Merhaba hello WordPress uygulaması açıklamasını okuduktan sonra tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-128">After reading hello description of hello WordPress app, click **Create**.</span></span>
   
    ![Oluştur](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="9cdc8-130">Hello hello web uygulaması için bir ad girin **Web uygulaması** kutusu.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-130">Enter a name for hello web app in hello **Web app** box.</span></span>
   
    <span data-ttu-id="9cdc8-131">Hello web uygulamasının Hello URL'si {ad} olacağı için bu ad hello azurewebsites.net etki alanında benzersiz olmalıdır. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-131">This name must be unique in hello azurewebsites.net domain because hello URL of hello web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="9cdc8-132">Girdiğiniz hello ad benzersiz değilse, hello metin kutusunda kırmızı bir ünlem işareti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-132">If hello name you enter isn't unique, a red exclamation mark appears in hello text box.</span></span>
6. <span data-ttu-id="9cdc8-133">Merhaba seçin, birden fazla aboneliğiniz varsa bir istediğiniz toouse.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-133">If you have more than one subscription, choose hello one you want toouse.</span></span> 
7. <span data-ttu-id="9cdc8-134">Bir **Kaynak Grubu** seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="9cdc8-135">Kaynak grupları hakkında daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9cdc8-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="9cdc8-136">Bir **App Service planı/Konum** seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="9cdc8-137">App Service planları hakkında daha fazla bilgi için bkz. [Azure App Service planlarına genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9cdc8-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="9cdc8-138">Tıklatın **veritabanı**ve ardından hello **yeni MySQL veritabanı** dikey penceresinde, MySQL veritabanınızı yapılandırmak için gerekli hello değerleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-138">Click **Database**, and then in hello **New MySQL Database** blade provide hello required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="9cdc8-139">a.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-139">a.</span></span> <span data-ttu-id="9cdc8-140">Yeni bir ad girin veya hello varsayılan adı bırakın.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-140">Enter a new name or leave hello default name.</span></span>
   
    <span data-ttu-id="9cdc8-141">b.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-141">b.</span></span> <span data-ttu-id="9cdc8-142">Merhaba bırakın **veritabanı türü** çok ayarlamak**paylaşılan**.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-142">Leave hello **Database Type** set too**Shared**.</span></span>
   
    <span data-ttu-id="9cdc8-143">c.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-143">c.</span></span> <span data-ttu-id="9cdc8-144">Hello gibi bir hello aynı konuma hello web uygulaması için seçtiğiniz seçin.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-144">Choose hello same location as hello one you chose for hello web app.</span></span>
   
    <span data-ttu-id="9cdc8-145">d.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-145">d.</span></span> <span data-ttu-id="9cdc8-146">Bir fiyatlandırma katmanı seçin.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-146">Choose a pricing tier.</span></span> <span data-ttu-id="9cdc8-147">Minimum izin verilen bağlantı ve disk alanıyla ücretsiz olan Mercury bu öğretici için uygundur.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="9cdc8-148">Merhaba, **yeni MySQL veritabanı** dikey penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-148">In hello **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="9cdc8-149">Merhaba, **WordPress** dikey penceresinde hello yasal koşulları kabul edin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-149">In hello **WordPress** blade, accept hello legal terms, and then click **Create**.</span></span> 
    
     ![Web uygulaması yapılandırma](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="9cdc8-151">Azure uygulama hizmeti hello web uygulamasını, genellikle bir dakikadan oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-151">Azure App Service creates hello web app, typically in less than a minute.</span></span> <span data-ttu-id="9cdc8-152">Merhaba sayfanın üst kısmındaki hello portal hello zil simgesine tıklayarak hello ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-152">You can watch hello progress by clicking hello bell icon at hello top of hello portal page.</span></span>
    
     ![İlerleme göstergesi](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="9cdc8-154">WordPress web uygulamanızı başlatma ve yönetme</span><span class="sxs-lookup"><span data-stu-id="9cdc8-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="9cdc8-155">Merhaba web uygulaması oluşturma tamamlandığında, hello uygulama oluşturulan ve hello web app ve hello veritabanı görebilirsiniz hello Azure Portal toohello kaynak grubuna gidin.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-155">When hello web app creation is finished, navigate in hello Azure Portal toohello resource group in which you created hello application, and you can see hello web app and hello database.</span></span>
   
    <span data-ttu-id="9cdc8-156">Merhaba hello ampul simgeli ek kaynak olan [Application Insights](/services/application-insights/), web uygulamanız için izleme hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-156">hello extra resource with hello light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="9cdc8-157">Merhaba, **kaynak grubu** dikey penceresinde hello web uygulaması satırına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-157">In hello **Resource group** blade, click hello web app line.</span></span>
   
    ![Web uygulaması yapılandırma](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="9cdc8-159">Merhaba Web uygulaması dikey penceresinde tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-159">In hello Web app blade, click **Browse**.</span></span>
   
    ![site URL][browse]
4. <span data-ttu-id="9cdc8-161">Merhaba WordPress içinde **Hoş Geldiniz** sayfasında, WordPress için gereken hello yapılandırma bilgilerini girin ve ardından **Wordpress'i Yükle**.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-161">In hello WordPress **Welcome** page, enter hello configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![WordPress’i yapılandırma](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="9cdc8-163">Merhaba üzerinde oluşturulan hello kimlik bilgilerini kullanarak oturum **Hoş Geldiniz** sayfası.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-163">Log in using hello credentials you created on hello **Welcome** page.</span></span>  
6. <span data-ttu-id="9cdc8-164">Sitenizin Pano sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-164">Your site Dashboard page opens.</span></span>    
   
    ![WordPress sitesi](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="9cdc8-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9cdc8-166">Next steps</span></span>
<span data-ttu-id="9cdc8-167">Gördüğünüz nasıl toocreate ve hello Galeriden bir PHP web uygulamasını dağıtın.</span><span class="sxs-lookup"><span data-stu-id="9cdc8-167">You've seen how toocreate and deploy a PHP web app from hello gallery.</span></span> <span data-ttu-id="9cdc8-168">Azure'da PHP kullanma hakkında daha fazla bilgi için bkz: Merhaba [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="9cdc8-168">For more information about using PHP in Azure, see hello [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="9cdc8-169">Hakkında daha fazla bilgi için App Service Web Apps ile toowork yan (geniş tarayıcı pencereleri için için) başlangıç sayfasının sol hello hello bağlantılar bakın veya hello sayfanın üst kısmındaki hello (için dar tarayıcı pencereleri için).</span><span class="sxs-lookup"><span data-stu-id="9cdc8-169">For more information about how toowork with App Service Web Apps, see hello links on hello left side of hello page (for wide browser windows) or at hello top of hello page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="9cdc8-170">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="9cdc8-170">What's changed</span></span>
* <span data-ttu-id="9cdc8-171">Web siteleri tooApp hizmet gelen bir kılavuzu toohello değişiklik için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="9cdc8-171">For a guide toohello change from Websites tooApp Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
