---
title: "Azure’da MySQL veritabanı oluşturma ve ona bağlanma"
description: "Bir MySQL veritabanı oluşturun ve bir PHP web uygulamasını Azure buna bağlanmak için Azure portalını kullanmayı öğrenin."
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: 
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;cephalin
ms.openlocfilehash: 66f4b7a5f8eb3f6f125c9420b40caffca3d43dd6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-connect-to-a-mysql-database-in-azure"></a><span data-ttu-id="15fec-103">Azure’da MySQL veritabanı oluşturma ve ona bağlanma</span><span class="sxs-lookup"><span data-stu-id="15fec-103">Create and connect to a MySQL database in Azure</span></span>
<span data-ttu-id="15fec-104">Bu öğretici bir MySQL veritabanının oluşturulacağı gösterilmektedir [Azure portal](https://portal.azure.com) (sağlayıcısı [ClearDB](http://www.cleardb.com/)) ve çalışır durumda bir PHP web uygulamasından bağlanmak nasıl [Azure App Service](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="15fec-104">This tutorial shows you how to create a MySQL database in the [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how to connect to it from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="15fec-105">Ayrıca bir MySQL veritabanı parçası olarak oluşturabileceğiniz bir [Market uygulaması şablonu](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="15fec-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="15fec-106">Azure portalında bir MySQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="15fec-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="15fec-107">Azure portalında bir MySQL veritabanı oluşturmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="15fec-107">To create a MySQL database in the Azure portal, do the following:</span></span>

1. <span data-ttu-id="15fec-108">[Azure Portal](https://portal.azure.com)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="15fec-108">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="15fec-109">Sol menüden **yeni** > **veri + depolama** > **MySQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="15fec-109">From the left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Azure - başlangıç MySQL veritabanı oluşturma](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="15fec-111">Yeni MySQL veritabanı [dikey](azure-portal-overview.md), yeni MySQL veritabanınız şu şekilde yapılandırın (*dikey*: yatay açılır bir portal sayfası):</span><span class="sxs-lookup"><span data-stu-id="15fec-111">In the New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="15fec-112">**Veritabanı adı**: benzersiz olarak tanımlanabilen bir ad yazın</span><span class="sxs-lookup"><span data-stu-id="15fec-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="15fec-113">**Abonelik**: kullanılacak aboneliği seçin</span><span class="sxs-lookup"><span data-stu-id="15fec-113">**Subscription**: Choose the subscription to use</span></span>
   * <span data-ttu-id="15fec-114">**Veritabanı türü**: seçin **paylaşılan** için düşük maliyetli veya ücretsiz katman veya **adanmış** özel kaynakları alınamadı.</span><span class="sxs-lookup"><span data-stu-id="15fec-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** to get dedicated resources.</span></span>
   * <span data-ttu-id="15fec-115">**Kaynak grubu**: mevcut bir MySQL veritabanı Ekle [kaynak grubu](azure-resource-manager/resource-group-overview.md) veya yeni bir yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="15fec-115">**Resource group**: Add the MySQL database to an existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="15fec-116">Aynı gruptaki kaynakların birlikte kolayca yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="15fec-116">Resources in the same group can be easily managed together.</span></span>
   * <span data-ttu-id="15fec-117">**Konum**: yakın bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="15fec-117">**Location**: Select a location close to you.</span></span> <span data-ttu-id="15fec-118">Varolan bir kaynak grubuna eklerken, kaynak grubunun konuma kilitli.</span><span class="sxs-lookup"><span data-stu-id="15fec-118">When adding to an existing resource group, you're locked to the resource group's location.</span></span>
   * <span data-ttu-id="15fec-119">**Fiyatlandırma katmanı**: tıklatın **fiyatlandırma katmanı**, ardından fiyatlandırma seçeneğini belirleyin (**Mercury** katman ücretsiz) ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="15fec-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="15fec-120">**Yasal koşullar**: tıklatın **yasal koşulları**, satın alma ayrıntılarını gözden geçirin ve'ı tıklatın **satın**.</span><span class="sxs-lookup"><span data-stu-id="15fec-120">**Legal Terms**: Click **Legal Terms**, review the purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="15fec-121">**Panoya Sabitle**: doğrudan panodan erişim isteyip istemediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="15fec-121">**Pin to dashboard**: Select if you want to access it directly from the dashboard.</span></span> <span data-ttu-id="15fec-122">Henüz portal gezinme alışık değilseniz bu özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="15fec-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="15fec-123">Aşağıdaki ekran görüntüsünde, MySQL veritabanınızı nasıl yapılandırabileceğiniz yalnızca bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="15fec-123">The following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Azure üzerinde MySQL veritabanı oluşturma - yapılandırma](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="15fec-125">Bitirdiğinizde yapılandırma, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="15fec-125">When you're done configuring, click **Create**.</span></span>

    ![Azure üzerinde MySQL veritabanı oluşturma - oluşturma](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="15fec-127">Dağıtım başladı bildiğiniz bir açılır bildirim veren görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="15fec-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Bir MySQL veritabanı - ediyor oluşturma](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="15fec-129">Dağıtım başarılı olduktan sonra başka bir açılır alırsınız.</span><span class="sxs-lookup"><span data-stu-id="15fec-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="15fec-130">Portal, MySQL veritabanı dikey aynı zamanda otomatik olarak açar.</span><span class="sxs-lookup"><span data-stu-id="15fec-130">The portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-to-your-mysql-database"></a><span data-ttu-id="15fec-131">MySQL veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="15fec-131">Connect to your MySQL database</span></span>
<span data-ttu-id="15fec-132">Yeni MySQL veritabanınız için bağlantı bilgilerini görmek için tıklatmanız **özellikleri** web uygulamanızın dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="15fec-132">To see the connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Azure - MySQL veritabanı dikey bir MySQL veritabanı oluşturma](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="15fec-134">Bu gibi durumlarda, bu bağlantı bilgisini artık herhangi bir web uygulamasına kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15fec-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="15fec-135">Basit bir PHP uygulaması'ndan bağlantı bilgisinin nasıl kullanılacağını gösteren bir örnek kullanılabilir [burada](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span><span class="sxs-lookup"><span data-stu-id="15fec-135">A sample that shows how to use the connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-the-php-get-started-tutorial"></a><span data-ttu-id="15fec-136">Bir Laravel web uygulamasından (PHP get Başlarken Öğreticisi) bağlanma</span><span class="sxs-lookup"><span data-stu-id="15fec-136">Connect a Laravel web app (from the PHP get started tutorial)</span></span>
<span data-ttu-id="15fec-137">Öğretici yalnızca tamamlandı varsayalım [oluşturma, yapılandırma ve Azure'a bir PHP web uygulaması dağıtma](app-service-web/app-service-web-php-get-started.md) ve bir [Laravel](https://www.laravel.com/) Azure'da çalışan web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="15fec-137">Suppose you just finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="15fec-138">Veritabanı özellikleri Laravel uygulamanıza kolayca ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15fec-138">You can easily add database capabilities to your Laravel app.</span></span> <span data-ttu-id="15fec-139">Yalnızca aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="15fec-139">Just follow the steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="15fec-140">Aşağıdaki adımlarda öğreticiyi bitirdikten varsayılmaktadır [oluşturma, yapılandırma ve Azure'a bir PHP web uygulaması dağıtma](app-service-web/app-service-web-php-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="15fec-140">The following steps assume that you have finished the tutorial [Create, configure, and deploy a PHP web app to Azure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="15fec-141">Laravel uygulama yerel geliştirme ortamınızı MySQL veritabanına işaret edecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="15fec-141">Configure the Laravel app in your local development environment to point to the MySQL database.</span></span> <span data-ttu-id="15fec-142">Bunu yapmak için açın `.env` Laravel uygulamanızın kök dizini ve MySQL veritabanı seçeneklerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="15fec-142">To do this, open `.env` from your Laravel app's root directory and configure the MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="15fec-143">İçinde **özellikleri** dikey penceresinde, MySQL veritabanınızın adını olabilir veya bir içinde görüntülenmeyebilir **veritabanı adı** alan.</span><span class="sxs-lookup"><span data-stu-id="15fec-143">In the **Properties** blade, the name of your MySQL database may or may not be the one shown in the **DATABASE NAME** field.</span></span> <span data-ttu-id="15fec-144">Veritabanı parametresi iade daha iyidir **bağlantı DİZESİ** alan.</span><span class="sxs-lookup"><span data-stu-id="15fec-144">It's better to check the Database parameter in the **CONNECTION STRING** field.</span></span>    
   >
   > ![Bir MySQL veritabanı - ediyor oluşturma](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="15fec-146">MySQL erişim artık yüklü olduğunu doğrulamak için en hızlı yoludur kullanmaktır [Laravel'ın varsayılan kimlik doğrulama iskele](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="15fec-146">The quickest way to verify that you have MySQL access now is to use [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="15fec-147">Komut satırı terminale Laravel uygulamanızın kök dizininden aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="15fec-147">In the command-line terminal, run the following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="15fec-148">İlk komut, önceden tanımlanmış geçişleri temel Azure tabloları oluşturur `database/migrations` dizin ve ikinci komut scaffolds temel görünümleri ve kullanıcı kaydı ve kimlik doğrulaması için rota.</span><span class="sxs-lookup"><span data-stu-id="15fec-148">The first command creates the tables in Azure based on predefined migrations in the `database/migrations` directory, and the second  command scaffolds the basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="15fec-149">Geliştirme Sunucusu şimdi çalıştır:</span><span class="sxs-lookup"><span data-stu-id="15fec-149">Run the development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="15fec-150">Tarayıcı için 8000 gidin ve gösterildiği gibi yeni bir kullanıcı kaydı:</span><span class="sxs-lookup"><span data-stu-id="15fec-150">In the browser, navigate to http://localhost:8000 and register a new user as shown:</span></span>

    ![Azure'da MySQL veritabanına bağlanma - kullanıcı kaydı](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="15fec-152">Tam UI istemi kayıt izleyin.</span><span class="sxs-lookup"><span data-stu-id="15fec-152">Follow the UI prompt complete the registration.</span></span> <span data-ttu-id="15fec-153">Kayıt işlemi tamamlandıktan sonra oturum açmanız.</span><span class="sxs-lookup"><span data-stu-id="15fec-153">Once registration completes, you will be logged in.</span></span>

    ![Azure'da MySQL veritabanına bağlanma - kullanıcı kaydı](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="15fec-155">Artık uygulamanızı Azure MySQL veritabanında karşı geliştirmektedir.</span><span class="sxs-lookup"><span data-stu-id="15fec-155">You are now developing your app against the MySQL database in Azure.</span></span>
5. <span data-ttu-id="15fec-156">Şimdi, çoğaltmak yeterlidir, `.env` Azure web uygulamanızın ayarlar.</span><span class="sxs-lookup"><span data-stu-id="15fec-156">Now, you just need to replicate your `.env` settings to your Azure web app.</span></span> <span data-ttu-id="15fec-157">Aşağıdaki Azure CLI komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="15fec-157">Run the following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="15fec-158">Ardından, kaydetmek ve daha önce çalıştırılırken yapılan yerel değişiklikleri Azure'a gönderin `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="15fec-158">Next, commit and push to Azure the local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="15fec-159">Azure web uygulaması'na göz atın.</span><span class="sxs-lookup"><span data-stu-id="15fec-159">Browse to the Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="15fec-160">Daha önce oluşturduğunuz kullanıcı kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="15fec-160">Log in using the user credentials you created earlier.</span></span>

    ![Connect Azure - MySQL veritabanında Azure web uygulaması'na göz atın](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="15fec-162">Oturum açtıktan sonra kolay sonrası oturum açma ekranı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="15fec-162">After you log in, you should see the friendly post-login screen.</span></span>

    ![Oturum açmış Azure - MySQL veritabanına bağlan](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="15fec-164">Tebrikler, azure'da PHP web uygulamanız şimdi MySQL veritabanından veri erişiyor.</span><span class="sxs-lookup"><span data-stu-id="15fec-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15fec-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="15fec-165">Next steps</span></span>
<span data-ttu-id="15fec-166">Daha fazla bilgi için bkz: [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="15fec-166">For more information, see the [PHP Developer Center](/develop/php/).</span></span>
