---
title: "Azure App Service’te WordPress web uygulaması oluşturma | Microsoft Belgeleri"
description: "Azure Portal'ı kullanarak WordPress blogu için yeni bir Azure web uygulaması oluşturmayı öğrenin."
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
ms.openlocfilehash: 460afdabed947fb4018a9ea8a7a5bc7dc5bc89c7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="af0e6-103">Azure App Service’te bir WordPress web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="af0e6-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="af0e6-104">Bu öğreticide Azure Market’ten bir WordPress blog sitesinin nasıl dağıtılacağı gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="af0e6-104">This tutorial shows how to deploy a WordPress blog site from the Azure Marketplace.</span></span>

<span data-ttu-id="af0e6-105">Bu öğreticiyi tamamladığınızda, bulutta bulunan ve çalışan kendi WordPress blog sitenize sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="af0e6-105">When you're done with the tutorial you'll have your own WordPress blog site up and running in the cloud.</span></span>

![WordPress sitesi](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="af0e6-107">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="af0e6-107">You'll learn:</span></span>

* <span data-ttu-id="af0e6-108">Azure Marketi'nde bir uygulama şablonunu bulma.</span><span class="sxs-lookup"><span data-stu-id="af0e6-108">How to find an application template in the Azure Marketplace.</span></span>
* <span data-ttu-id="af0e6-109">Azure App Service'te şablon temelli bir web uygulaması oluşturma.</span><span class="sxs-lookup"><span data-stu-id="af0e6-109">How to create a web app in Azure App Service that is based on the template.</span></span>
* <span data-ttu-id="af0e6-110">Yeni web uygulaması ve veritabanı için Azure App Service ayarlarını yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="af0e6-110">How to configure Azure App Service settings for the new web app and database.</span></span>

<span data-ttu-id="af0e6-111">Azure Marketi, Microsoft, üçüncü taraf şirketler ve açık kaynak yazılım girişimleri tarafından geliştirilen çok çeşitli popüler web uygulamalarını kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="af0e6-111">The Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="af0e6-112">Web uygulamaları birçok popüler uygulamayı temel alarak oluşturulur, bu WordPress örneğinde [PHP](/develop/nodejs/), [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/) ve [Python](/develop/python/) bunlardan yalnızca birkaçıdır.</span><span class="sxs-lookup"><span data-stu-id="af0e6-112">The web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), to name a few.</span></span> <span data-ttu-id="af0e6-113">Azure Marketi'nde bir web uygulaması oluşturmak için ihtiyacınız olan tek yazılım [Azure Portal](https://portal.azure.com/) için kullandığınız tarayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="af0e6-113">To create a web app from the Azure Marketplace the only software you need is the browser that you use for the [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="af0e6-114">Bu öğreticide dağıttığınız WordPress sitesi veritabanı için MySQL kullanır.</span><span class="sxs-lookup"><span data-stu-id="af0e6-114">The WordPress site that you deploy in this tutorial uses MySQL for the database.</span></span> <span data-ttu-id="af0e6-115">Bunun yerine veritabanı için SQL Database’i kullanmak istiyorsanız, bkz: [Project Nami](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="af0e6-115">If you wish to instead use SQL Database for the database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="af0e6-116">**Project Nami** Market üzerinden de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="af0e6-116">**Project Nami** is also available through the Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="af0e6-117">Bu öğreticiyi tamamlamak için Microsoft Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="af0e6-117">To complete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="af0e6-118">Bir hesabınız yoksa, [Visual Studio abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) veya [ücretsiz deneme için kaydolabilirsiniz](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="af0e6-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="af0e6-119">Bir Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak istiyorsanız [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/)’e gidin.</span><span class="sxs-lookup"><span data-stu-id="af0e6-119">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="af0e6-120">Burada, App Service'te hemen bir kısa süreli başlangıç web uygulaması oluşturabilirsiniz; kredi kartı gerekmez ve hiçbir taahhüt yoktur.</span><span class="sxs-lookup"><span data-stu-id="af0e6-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="af0e6-121">WordPress’i seçme ve Azure App Service için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="af0e6-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="af0e6-122">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="af0e6-122">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="af0e6-123">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af0e6-123">Click **New**.</span></span>
   
    ![Yeni Oluştur][5]
3. <span data-ttu-id="af0e6-125">**WordPress**’i arayın ve ardından **WordPress**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af0e6-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="af0e6-126">(MySQL yerine SQL Database kullanmak isterseniz, **Project Nami** için arama yapın.)</span><span class="sxs-lookup"><span data-stu-id="af0e6-126">If you wish to use SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![Listede WordPress][7]
4. <span data-ttu-id="af0e6-128">WordPress uygulaması açıklamasını okuduktan sonra, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af0e6-128">After reading the description of the WordPress app, click **Create**.</span></span>
   
    ![Oluştur](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="af0e6-130">Web uygulaması için **Web uygulaması** kutusuna bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="af0e6-130">Enter a name for the web app in the **Web app** box.</span></span>
   
    <span data-ttu-id="af0e6-131">Web uygulamasının URL’si {ad}.azurewebsites.net şeklinde olacağından, bu ad azurewebsites.net etki alanında benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="af0e6-131">This name must be unique in the azurewebsites.net domain because the URL of the web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="af0e6-132">Girdiğiniz ad benzersiz değilse, metin kutusunda kırmızı bir ünlem işareti gösterilir.</span><span class="sxs-lookup"><span data-stu-id="af0e6-132">If the name you enter isn't unique, a red exclamation mark appears in the text box.</span></span>
6. <span data-ttu-id="af0e6-133">Birden fazla aboneliğiniz varsa, kullanmak istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="af0e6-133">If you have more than one subscription, choose the one you want to use.</span></span> 
7. <span data-ttu-id="af0e6-134">Bir **Kaynak Grubu** seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="af0e6-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="af0e6-135">Kaynak grupları hakkında daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="af0e6-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="af0e6-136">Bir **App Service planı/Konum** seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="af0e6-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="af0e6-137">App Service planları hakkında daha fazla bilgi için bkz. [Azure App Service planlarına genel bakış](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="af0e6-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="af0e6-138">**Veritabanı**’na tıklayın ve ardından **Yeni MySQL Veritabanı** dikey penceresinde, MySQL veritabanınızı yapılandırmak için gereken değerleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="af0e6-138">Click **Database**, and then in the **New MySQL Database** blade provide the required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="af0e6-139">a.</span><span class="sxs-lookup"><span data-stu-id="af0e6-139">a.</span></span> <span data-ttu-id="af0e6-140">Yeni bir ad girin veya varsayılan adı bırakın.</span><span class="sxs-lookup"><span data-stu-id="af0e6-140">Enter a new name or leave the default name.</span></span>
   
    <span data-ttu-id="af0e6-141">b.</span><span class="sxs-lookup"><span data-stu-id="af0e6-141">b.</span></span> <span data-ttu-id="af0e6-142">**Veritabanı Türü**’nü **Paylaşılan** olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="af0e6-142">Leave the **Database Type** set to **Shared**.</span></span>
   
    <span data-ttu-id="af0e6-143">c.</span><span class="sxs-lookup"><span data-stu-id="af0e6-143">c.</span></span> <span data-ttu-id="af0e6-144">Web uygulaması için seçtiğinizle aynı konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="af0e6-144">Choose the same location as the one you chose for the web app.</span></span>
   
    <span data-ttu-id="af0e6-145">d.</span><span class="sxs-lookup"><span data-stu-id="af0e6-145">d.</span></span> <span data-ttu-id="af0e6-146">Bir fiyatlandırma katmanı seçin.</span><span class="sxs-lookup"><span data-stu-id="af0e6-146">Choose a pricing tier.</span></span> <span data-ttu-id="af0e6-147">Minimum izin verilen bağlantı ve disk alanıyla ücretsiz olan Mercury bu öğretici için uygundur.</span><span class="sxs-lookup"><span data-stu-id="af0e6-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="af0e6-148">**Yeni MySQL veritabanı** dikey penceresinde **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af0e6-148">In the **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="af0e6-149">**WordPress** dikey penceresinde, yasal koşulları kabul edin ve ardından **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af0e6-149">In the **WordPress** blade, accept the legal terms, and then click **Create**.</span></span> 
    
     ![Web uygulaması yapılandırma](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="af0e6-151">Azure App Service web uygulamasını, genellikle bir dakikadan az süre içinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="af0e6-151">Azure App Service creates the web app, typically in less than a minute.</span></span> <span data-ttu-id="af0e6-152">Portal sayfasının üst kısmındaki zil simgesine tıklayarak ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af0e6-152">You can watch the progress by clicking the bell icon at the top of the portal page.</span></span>
    
     ![İlerleme göstergesi](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="af0e6-154">WordPress web uygulamanızı başlatma ve yönetme</span><span class="sxs-lookup"><span data-stu-id="af0e6-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="af0e6-155">Web uygulaması oluşturma tamamlandığında, Azure Portal’da uygulamayı oluşturduğunuz kaynak grubuna gidin, burada web uygulamasını ve veritabanını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af0e6-155">When the web app creation is finished, navigate in the Azure Portal to the resource group in which you created the application, and you can see the web app and the database.</span></span>
   
    <span data-ttu-id="af0e6-156">Ampul simgeli ek kaynak, web hizmetiniz için izleme hizmetleri sağlayan [Application Insights](/services/application-insights/)’dır.</span><span class="sxs-lookup"><span data-stu-id="af0e6-156">The extra resource with the light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="af0e6-157">**Kaynak grubu** dikey penceresinde, web uygulaması satırına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af0e6-157">In the **Resource group** blade, click the web app line.</span></span>
   
    ![Web uygulaması yapılandırma](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="af0e6-159">Web uygulaması dikey penceresinde, **Gözat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af0e6-159">In the Web app blade, click **Browse**.</span></span>
   
    ![site URL][browse]
4. <span data-ttu-id="af0e6-161">WordPress **Karşılama** sayfasında, WordPress için gereken yapılandırma bilgilerini girin ve ardından **WordPress’i Yükle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="af0e6-161">In the WordPress **Welcome** page, enter the configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![WordPress’i yapılandırma](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="af0e6-163">**Karşılama** sayfasında oluşturduğunuz kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="af0e6-163">Log in using the credentials you created on the **Welcome** page.</span></span>  
6. <span data-ttu-id="af0e6-164">Sitenizin Pano sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="af0e6-164">Your site Dashboard page opens.</span></span>    
   
    ![WordPress sitesi](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="af0e6-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="af0e6-166">Next steps</span></span>
<span data-ttu-id="af0e6-167">Galeriden bir PHP web uygulamasını nasıl oluşturup dağıtacağınızı gördünüz.</span><span class="sxs-lookup"><span data-stu-id="af0e6-167">You've seen how to create and deploy a PHP web app from the gallery.</span></span> <span data-ttu-id="af0e6-168">Azure’da PHP kullanma hakkında daha fazla bilgi için bkz. [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="af0e6-168">For more information about using PHP in Azure, see the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="af0e6-169">App Service Web Apps ile çalışma hakkında daha fazla bilgi için sayfanın sol tarafındaki (geniş tarayıcı pencereleri için) veya sayfanın üst kısmındaki (dar tarayıcı pencereleri için) bağlantılara bakın.</span><span class="sxs-lookup"><span data-stu-id="af0e6-169">For more information about how to work with App Service Web Apps, see the links on the left side of the page (for wide browser windows) or at the top of the page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="af0e6-170">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="af0e6-170">What's changed</span></span>
* <span data-ttu-id="af0e6-171">Web Sitelerinden App Service’e değiştirme kılavuzu için bkz. [Azure App Service ve mevcut Azure Hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="af0e6-171">For a guide to the change from Websites to App Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
