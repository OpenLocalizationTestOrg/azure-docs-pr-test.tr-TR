---
title: "aaaCreate ve azure'da tooa MySQL veritabanına bağlanın"
description: "Nasıl toouse Azure portal toocreate bir MySQL veritabanı hello ve Azure bir PHP web uygulamasından tooit bağlanmak öğrenin."
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
ms.openlocfilehash: 3abc02f8887432625666afd847e9dc0c0a4db2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a><span data-ttu-id="66e23-103">Oluştur ve Azure tooa MySQL veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="66e23-103">Create and connect tooa MySQL database in Azure</span></span>
<span data-ttu-id="66e23-104">Bu öğretici nasıl toocreate bir MySQL veritabanı hello gösterir [Azure portal](https://portal.azure.com) (sağlayıcısı [ClearDB](http://www.cleardb.com/)) ve nasıl tooconnect tooit bir php'den web uygulaması çalışır durumda [Azure App Service](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="66e23-104">This tutorial shows you how toocreate a MySQL database in hello [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how tooconnect tooit from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="66e23-105">Ayrıca bir MySQL veritabanı parçası olarak oluşturabileceğiniz bir [Market uygulaması şablonu](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="66e23-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="66e23-106">Azure portalında bir MySQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="66e23-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="66e23-107">toocreate hello Azure portal, MySQL veritabanında hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="66e23-107">toocreate a MySQL database in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="66e23-108">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="66e23-108">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="66e23-109">Merhaba sol menüden **yeni** > **veri + depolama** > **MySQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="66e23-109">From hello left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![Azure - başlangıç MySQL veritabanı oluşturma](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="66e23-111">Merhaba yeni MySQL veritabanı içinde [dikey](azure-portal-overview.md), yeni MySQL veritabanınız şu şekilde yapılandırın (*dikey*: yatay açılır bir portal sayfası):</span><span class="sxs-lookup"><span data-stu-id="66e23-111">In hello New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="66e23-112">**Veritabanı adı**: benzersiz olarak tanımlanabilen bir ad yazın</span><span class="sxs-lookup"><span data-stu-id="66e23-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="66e23-113">**Abonelik**: hello abonelik toouse seçin</span><span class="sxs-lookup"><span data-stu-id="66e23-113">**Subscription**: Choose hello subscription toouse</span></span>
   * <span data-ttu-id="66e23-114">**Veritabanı türü**: seçin **paylaşılan** için düşük maliyetli veya ücretsiz katman veya **adanmış** tooget ayrılmış kaynakları.</span><span class="sxs-lookup"><span data-stu-id="66e23-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** tooget dedicated resources.</span></span>
   * <span data-ttu-id="66e23-115">**Kaynak grubu**: hello MySQL veritabanı tooan varolan eklemek [kaynak grubu](azure-resource-manager/resource-group-overview.md) veya yeni bir yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="66e23-115">**Resource group**: Add hello MySQL database tooan existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="66e23-116">Aynı grup birlikte kolayca yönetilebilir hello kaynakları.</span><span class="sxs-lookup"><span data-stu-id="66e23-116">Resources in hello same group can be easily managed together.</span></span>
   * <span data-ttu-id="66e23-117">**Konum**: konum Kapat tooyou seçin.</span><span class="sxs-lookup"><span data-stu-id="66e23-117">**Location**: Select a location close tooyou.</span></span> <span data-ttu-id="66e23-118">Kaynak grubu mevcut tooan eklerken kilitli toohello kaynak grubu konumu demektir.</span><span class="sxs-lookup"><span data-stu-id="66e23-118">When adding tooan existing resource group, you're locked toohello resource group's location.</span></span>
   * <span data-ttu-id="66e23-119">**Fiyatlandırma katmanı**: tıklatın **fiyatlandırma katmanı**, ardından fiyatlandırma seçeneğini belirleyin (**Mercury** katman ücretsiz) ve ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="66e23-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="66e23-120">**Yasal koşullar**: tıklatın **yasal koşulları**hello satın alma ayrıntılarını gözden geçirin ve'ı tıklatın **satın**.</span><span class="sxs-lookup"><span data-stu-id="66e23-120">**Legal Terms**: Click **Legal Terms**, review hello purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="66e23-121">**PIN toodashboard**: tooaccess istiyorsanız seçin, doğrudan hello panosundan.</span><span class="sxs-lookup"><span data-stu-id="66e23-121">**Pin toodashboard**: Select if you want tooaccess it directly from hello dashboard.</span></span> <span data-ttu-id="66e23-122">Henüz portal gezinme alışık değilseniz bu özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="66e23-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="66e23-123">Aşağıdaki ekran görüntüsü hello MySQL veritabanınızı nasıl yapılandırabileceğiniz yalnızca bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="66e23-123">hello following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![Azure üzerinde MySQL veritabanı oluşturma - yapılandırma](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="66e23-125">Bitirdiğinizde yapılandırma, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="66e23-125">When you're done configuring, click **Create**.</span></span>

    ![Azure üzerinde MySQL veritabanı oluşturma - oluşturma](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="66e23-127">Dağıtım başladı bildiğiniz bir açılır bildirim veren görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="66e23-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![Bir MySQL veritabanı - ediyor oluşturma](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="66e23-129">Dağıtım başarılı olduktan sonra başka bir açılır alırsınız.</span><span class="sxs-lookup"><span data-stu-id="66e23-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="66e23-130">Merhaba portal MySQL veritabanı dikey pencerenizde aynı zamanda otomatik olarak açar.</span><span class="sxs-lookup"><span data-stu-id="66e23-130">hello portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a><span data-ttu-id="66e23-131">Bağlantı tooyour MySQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="66e23-131">Connect tooyour MySQL database</span></span>
<span data-ttu-id="66e23-132">Yeni MySQL veritabanınızı toosee hello bağlantı bilgilerini tıklatmanız **özellikleri** web uygulamanızın dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="66e23-132">toosee hello connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![Azure - MySQL veritabanı dikey bir MySQL veritabanı oluşturma](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="66e23-134">Bu gibi durumlarda, bu bağlantı bilgisini artık herhangi bir web uygulamasına kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66e23-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="66e23-135">Nasıl toouse hello bağlantı bilgilerini basit bir PHP uygulamasından ulaşılabilir gösteren bir örnek [burada](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span><span class="sxs-lookup"><span data-stu-id="66e23-135">A sample that shows how toouse hello connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a><span data-ttu-id="66e23-136">Bir Laravel web uygulamasından (Merhaba PHP get Başlarken Öğreticisi) bağlanma</span><span class="sxs-lookup"><span data-stu-id="66e23-136">Connect a Laravel web app (from hello PHP get started tutorial)</span></span>
<span data-ttu-id="66e23-137">Yalnızca tamamlanan hello öğretici varsayalım [oluşturma, yapılandırma ve PHP web uygulaması tooAzure dağıtma](app-service-web/app-service-web-php-get-started.md) ve bir [Laravel](https://www.laravel.com/) Azure'da çalışan web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="66e23-137">Suppose you just finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="66e23-138">Veritabanı özellikleri tooyour Laravel uygulama kolayca ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66e23-138">You can easily add database capabilities tooyour Laravel app.</span></span> <span data-ttu-id="66e23-139">Yalnızca hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="66e23-139">Just follow hello steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="66e23-140">Merhaba aşağıdaki adımlarda hello öğreticiyi bitirdikten varsayılmaktadır [oluşturma, yapılandırma ve PHP web uygulaması tooAzure dağıtma](app-service-web/app-service-web-php-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="66e23-140">hello following steps assume that you have finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="66e23-141">Merhaba Laravel uygulama, yerel geliştirme ortamı toopoint toohello MySQL veritabanınızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="66e23-141">Configure hello Laravel app in your local development environment toopoint toohello MySQL database.</span></span> <span data-ttu-id="66e23-142">toodo Bu, açık `.env` Laravel uygulamanızın kök dizini ve hello MySQL veritabanı seçeneklerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="66e23-142">toodo this, open `.env` from your Laravel app's root directory and configure hello MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="66e23-143">Merhaba, **özellikleri** dikey penceresinde, MySQL veritabanınızı hello adını olabilir veya bir hello hello görüntülenmeyebilir **veritabanı adı** alan.</span><span class="sxs-lookup"><span data-stu-id="66e23-143">In hello **Properties** blade, hello name of your MySQL database may or may not be hello one shown in hello **DATABASE NAME** field.</span></span> <span data-ttu-id="66e23-144">Daha iyi toocheck hello veritabanı parametresinde hello olan **bağlantı DİZESİ** alan.</span><span class="sxs-lookup"><span data-stu-id="66e23-144">It's better toocheck hello Database parameter in hello **CONNECTION STRING** field.</span></span>    
   >
   > ![Bir MySQL veritabanı - ediyor oluşturma](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="66e23-146">Merhaba hızlı şekilde tooverify MySQL erişim şimdi sahip olduğu toouse [Laravel'ın varsayılan kimlik doğrulama iskele](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span><span class="sxs-lookup"><span data-stu-id="66e23-146">hello quickest way tooverify that you have MySQL access now is toouse [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="66e23-147">Merhaba komut satırı terminale komutları Laravel uygulamanızın kök dizininden aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="66e23-147">In hello command-line terminal, run hello following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="66e23-148">Merhaba ilk komut hello önceden tanımlanmış geçişleri göre azure'da hello tablolar oluşturur `database/migrations` dizin ve iskelesini kurar hello temel görünümleri ve kullanıcı kaydı ve kimlik doğrulaması için rota hello ikinci komutu.</span><span class="sxs-lookup"><span data-stu-id="66e23-148">hello first command creates hello tables in Azure based on predefined migrations in hello `database/migrations` directory, and hello second  command scaffolds hello basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="66e23-149">Merhaba geliştirme sunucusu şimdi çalıştır:</span><span class="sxs-lookup"><span data-stu-id="66e23-149">Run hello development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="66e23-150">Merhaba tarayıcıda toohttp://localhost:8000 gidin ve gösterildiği gibi yeni bir kullanıcı kaydı:</span><span class="sxs-lookup"><span data-stu-id="66e23-150">In hello browser, navigate toohttp://localhost:8000 and register a new user as shown:</span></span>

    ![Azure tooMySQL veritabanında connect - kullanıcı kaydı](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="66e23-152">Merhaba UI komut istemi tam hello kayıt izleyin.</span><span class="sxs-lookup"><span data-stu-id="66e23-152">Follow hello UI prompt complete hello registration.</span></span> <span data-ttu-id="66e23-153">Kayıt işlemi tamamlandıktan sonra oturum açmanız.</span><span class="sxs-lookup"><span data-stu-id="66e23-153">Once registration completes, you will be logged in.</span></span>

    ![Azure tooMySQL veritabanında connect - kullanıcı kaydı](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="66e23-155">Uygulamanızı azure'da hello MySQL veritabanında şimdi geliştirmektedir.</span><span class="sxs-lookup"><span data-stu-id="66e23-155">You are now developing your app against hello MySQL database in Azure.</span></span>
5. <span data-ttu-id="66e23-156">Şimdi, tooreplicate yeterlidir, `.env` ayarları tooyour Azure web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="66e23-156">Now, you just need tooreplicate your `.env` settings tooyour Azure web app.</span></span> <span data-ttu-id="66e23-157">Azure CLI komutları aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="66e23-157">Run hello following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="66e23-158">Ardından, kaydetmek ve anında önceki çalıştırılırken tooAzure hello yerel değişikliklerinin `php artisan make:auth`.</span><span class="sxs-lookup"><span data-stu-id="66e23-158">Next, commit and push tooAzure hello local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="66e23-159">Toohello Azure web uygulaması göz atın.</span><span class="sxs-lookup"><span data-stu-id="66e23-159">Browse toohello Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="66e23-160">Daha önce oluşturduğunuz hello kullanıcı kimlik bilgilerini kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="66e23-160">Log in using hello user credentials you created earlier.</span></span>

    ![Azure tooMySQL veritabanında connect - tooAzure web uygulaması Gözat](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="66e23-162">Oturum açtıktan sonra hello kolay sonrası oturum açma ekranı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="66e23-162">After you log in, you should see hello friendly post-login screen.</span></span>

    ![Azure - oturum tooMySQL veritabanına bağlan](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="66e23-164">Tebrikler, azure'da PHP web uygulamanız şimdi MySQL veritabanından veri erişiyor.</span><span class="sxs-lookup"><span data-stu-id="66e23-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66e23-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="66e23-165">Next steps</span></span>
<span data-ttu-id="66e23-166">Daha fazla bilgi için bkz: Merhaba [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="66e23-166">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>
