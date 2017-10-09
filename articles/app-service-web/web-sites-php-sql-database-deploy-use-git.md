---
title: "aaaCreate PHP SQL web uygulaması ve tooAzure uygulama hizmeti dağıtma Git kullanma"
description: "Nasıl toocreate bir PHP web Azure SQL veritabanında veri depolayan uygulaması ve Git dağıtım tooAzure uygulama hizmeti kullanmak gösteren bir öğretici."
services: app-service\web, sql-database
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6b090bf6-31d8-4b74-81eb-050ef95929ca
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aaacb2fe0787bbcdafa72871912e8d08792be29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a><span data-ttu-id="c1928-103">Bir PHP SQL web uygulaması oluşturma ve tooAzure uygulama hizmeti dağıtma Git kullanma</span><span class="sxs-lookup"><span data-stu-id="c1928-103">Create a PHP-SQL web app and deploy tooAzure App Service using Git</span></span>
<span data-ttu-id="c1928-104">Bu öğretici nasıl toocreate bir PHP web uygulamasında gösterir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) tooAzure SQL veritabanına bağlanan ve nasıl toodeploy Git kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c1928-104">This tutorial shows you how toocreate a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects tooAzure SQL Database and how toodeploy it using Git.</span></span> <span data-ttu-id="c1928-105">Bu öğretici, varsayar [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [SQL Server için PHP için Microsoft Drivers ](http://www.microsoft.com/download/en/details.aspx?id=20098), ve [Git] [ install-git] bilgisayarınızda yüklü.</span><span class="sxs-lookup"><span data-stu-id="c1928-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="c1928-106">Bu kılavuzu tamamladıktan sonra Azure'da çalışan bir PHP SQL web uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1928-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="c1928-107">Yükleme ve PHP, SQL Server Express ve hello Microsoft Drivers hello kullanarak PHP için SQL Server için Yapılandır [Microsoft Web Platformu yükleyicisi](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1928-107">You can install and configure PHP, SQL Server Express, and hello Microsoft Drivers for SQL Server for PHP using hello [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="c1928-108">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="c1928-108">You will learn:</span></span>

* <span data-ttu-id="c1928-109">Nasıl toocreate bir Azure web app ve hello kullanarak bir SQL veritabanı [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="c1928-109">How toocreate an Azure web app and a SQL Database using hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="c1928-110">PHP App Service Web Apps içinde varsayılan olarak etkindir, özel bir şey gerekli toorun çünkü PHP kodunuzu.</span><span class="sxs-lookup"><span data-stu-id="c1928-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="c1928-111">Nasıl toopublish ve Git kullanarak, uygulama tooAzure yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="c1928-111">How toopublish and re-publish your application tooAzure using Git.</span></span>

<span data-ttu-id="c1928-112">Bu öğreticiyi izleyerek, PHP bir basit kayıt web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c1928-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="c1928-113">Merhaba uygulaması bir Azure Web Sitesi'nde barındırılan.</span><span class="sxs-lookup"><span data-stu-id="c1928-113">hello application will be hosted in an Azure Website.</span></span> <span data-ttu-id="c1928-114">Tamamlanan hello uygulamasının ekran görüntüsü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c1928-114">A screenshot of hello completed application is below:</span></span>

![Azure PHP Web sitesi](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="c1928-116">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1928-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c1928-117">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c1928-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="c1928-118">Bir Azure web uygulaması oluşturma ve Git yayımlama Ayarla</span><span class="sxs-lookup"><span data-stu-id="c1928-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="c1928-119">Bu adımları toocreate Azure web uygulaması ve SQL veritabanı izleyin:</span><span class="sxs-lookup"><span data-stu-id="c1928-119">Follow these steps toocreate an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="c1928-120">İçinde toohello oturum [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c1928-120">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c1928-121">Merhaba tıklatarak açık hello Azure Marketi **yeni** hello üst simgesine sol hello panosunu, tıklayın **Tümünü Seç** sonraki tooMarketplace ve seçerek **Web + mobil**.</span><span class="sxs-lookup"><span data-stu-id="c1928-121">Open hello Azure Marketplace by clicking hello **New** icon on hello top left of hello dashboard, click on **Select All** next tooMarketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="c1928-122">Hello Market, seçin **Web + mobil**.</span><span class="sxs-lookup"><span data-stu-id="c1928-122">In hello Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="c1928-123">Merhaba tıklatın **Web uygulaması + SQL** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c1928-123">Click hello **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="c1928-124">Hello Web uygulaması + SQL uygulama Hello açıklamasını okuduktan sonra Seç **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c1928-124">After reading hello description of hello Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="c1928-125">Her bölüm üzerinde'i tıklatın (**kaynak grubu**, **Web uygulaması**, **veritabanı**, ve **abonelik**) girin ve gerekli hello için değerleri seçin alanlar:</span><span class="sxs-lookup"><span data-stu-id="c1928-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for hello required fields:</span></span>
   
   * <span data-ttu-id="c1928-126">Tercih ettiğiniz bir URL adı girin</span><span class="sxs-lookup"><span data-stu-id="c1928-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="c1928-127">Veritabanı sunucusu kimlik bilgilerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c1928-127">Configure database server credentials</span></span>
   * <span data-ttu-id="c1928-128">Merhaba bölgeye en yakın tooyou seçin</span><span class="sxs-lookup"><span data-stu-id="c1928-128">Select hello region closest tooyou</span></span>
     
     ![uygulamanızı yapılandırma](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="c1928-130">Merhaba web uygulaması tanımlama bittiğinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c1928-130">When finished defining hello web app, click **Create**.</span></span>
   
    <span data-ttu-id="c1928-131">Merhaba web uygulaması oluşturduğunuzda hello **bildirimleri** düğmesi yeşil flash **başarı** ve kaynak grubu dikey penceresi açık tooshow hem hello web app ve hello SQL veritabanında hello Grup hello.</span><span class="sxs-lookup"><span data-stu-id="c1928-131">When hello web app has been created, hello **Notifications** button will flash a green **SUCCESS** and hello resource group blade open tooshow both hello web app and hello SQL database in hello group.</span></span>
8. <span data-ttu-id="c1928-132">Merhaba kaynak grubu dikey tooopen hello web uygulamanızın dikey penceresinde Hello web uygulamanızın simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c1928-132">Click hello web app's icon in hello resource group blade tooopen hello web app's blade.</span></span>
   
    ![web uygulamanızın kaynak grubu](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="c1928-134">İçinde **ayarları** tıklatın **sürekli dağıtım** > **gerekli ayarları Yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="c1928-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="c1928-135">Seçin **yerel Git deposu** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c1928-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![kaynak kodunuz nerede](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="c1928-137">Önce bir Git deposu ayarlama ayarlamadıysanız, bir kullanıcı adı ve parolasını sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1928-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="c1928-138">toodo bunu, **ayarları** > **dağıtım kimlik bilgileri** hello web uygulamanızın dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="c1928-138">toodo this, click **Settings** > **Deployment credentials** in hello web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="c1928-139">İçinde **ayarları** tıklayın **özellikleri** toosee hello Git uzak URL ihtiyacınız toouse toodeploy PHP uygulamanızı daha sonra.</span><span class="sxs-lookup"><span data-stu-id="c1928-139">In **Settings** click on **Properties** toosee hello Git remote URL you need toouse toodeploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="c1928-140">SQL veritabanı bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="c1928-140">Get SQL Database connection information</span></span>
<span data-ttu-id="c1928-141">bağlı olan tooconnect toohello SQL veritabanı örneği tooyour web uygulaması, profilinizde hello veritabanı oluşturduğunuzda belirttiğiniz bağlantı bilgilerini hello.</span><span class="sxs-lookup"><span data-stu-id="c1928-141">tooconnect toohello SQL Database instance that is linked tooyour web app, your will need hello connection information, which you specified when you created hello database.</span></span> <span data-ttu-id="c1928-142">tooget hello SQL veritabanı bağlantı bilgilerini, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c1928-142">tooget hello SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="c1928-143">Geri hello kaynak grubu dikey penceresinde hello SQL Database'in simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c1928-143">Back in hello resource group's blade, click hello SQL database's icon.</span></span>
2. <span data-ttu-id="c1928-144">Merhaba SQL Database'in dikey penceresinde tıklayın **ayarları** > **özellikleri**, ardından **veritabanı bağlantı dizelerini Göster**.</span><span class="sxs-lookup"><span data-stu-id="c1928-144">In hello SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![Veritabanı özellikleri görüntüle](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="c1928-146">Merhaba gelen **PHP** bölüm hello ortaya çıkan iletişim, hello değerlerini Not `Server`, `SQL Database`, ve `User Name`.</span><span class="sxs-lookup"><span data-stu-id="c1928-146">From hello **PHP** section of hello resulting dialog, make note of hello values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="c1928-147">Daha sonra PHP web uygulaması tooAzure uygulama hizmeti zaman yayımlama bu değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="c1928-147">You will use these values later when publishing your PHP web app tooAzure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="c1928-148">Uygulamanızı yerel olarak oluşturma ve test etme</span><span class="sxs-lookup"><span data-stu-id="c1928-148">Build and test your application locally</span></span>
<span data-ttu-id="c1928-149">Merhaba kayıt uygulama adı ve e-posta adresinizi sağlayarak bir olay için tooregister sağlayan basit bir PHP uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="c1928-149">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="c1928-150">Önceki şahıslar hakkında bilgi bir tabloda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c1928-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="c1928-151">Kayıt defteri bilgilerini bir SQL veritabanı örneğinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="c1928-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="c1928-152">Merhaba uygulaması iki dosyaları (kopyala/yapıştır kodu aşağıda kullanılabilir) oluşur:</span><span class="sxs-lookup"><span data-stu-id="c1928-152">hello application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="c1928-153">**PHP için index.php'dir**: kaydı ve registrant bilgi içeren bir tablo için bir form görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c1928-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="c1928-154">**CreateTable.php**: Merhaba uygulaması için hello SQL veritabanı tablosu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c1928-154">**createtable.php**: Creates hello SQL Database table for hello application.</span></span> <span data-ttu-id="c1928-155">Bu dosya yalnızca bir kez kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c1928-155">This file will only be used once.</span></span>

<span data-ttu-id="c1928-156">yerel olarak toorun Merhaba uygulaması hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="c1928-156">toorun hello application locally, follow hello steps below.</span></span> <span data-ttu-id="c1928-157">PHP sahip ve SQL Server Express ayarlanan yerel makinenizde ve etkinleştirdiğinizden emin hello adımları varsayılır Not [PDO uzantısı için SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="c1928-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled hello [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="c1928-158">Adlı bir SQL Server veritabanı oluşturma `registration`.</span><span class="sxs-lookup"><span data-stu-id="c1928-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="c1928-159">Hello bunu yapabilirsiniz `sqlcmd` komut istemi Bu komutlar:</span><span class="sxs-lookup"><span data-stu-id="c1928-159">You can do this from hello `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="c1928-160">Uygulama kök dizininde iki dosya - adlı oluşturma `createtable.php` ve adlı `index.php`.</span><span class="sxs-lookup"><span data-stu-id="c1928-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="c1928-161">Açık hello `createtable.php` dosyasını bir metin düzenleyicisi veya IDE ve hello aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c1928-161">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="c1928-162">Bu kod kullanılan toocreate hello olacaktır `registration_tbl` hello tabloda `registration` veritabanı.</span><span class="sxs-lookup"><span data-stu-id="c1928-162">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
            id INT NOT NULL IDENTITY(1,1) 
            PRIMARY KEY(id),
            name VARCHAR(30),
            email VARCHAR(30),
            date DATE)";
            $conn->query($sql);
        }
        catch(Exception $e){
            die(print_r($e));
        }
        echo "<h3>Table created.</h3>";
        ?>
   
    <span data-ttu-id="c1928-163">Tooupdate hello değerlerini gerektiğine dikkat edin <code>$user</code> ve <code>$pwd</code> yerel SQL Server kullanıcı adı ve parola.</span><span class="sxs-lookup"><span data-stu-id="c1928-163">Note that you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="c1928-164">Merhaba kök dizininde komutu aşağıdaki hello uygulama türü Merhaba, bir terminal içinde:</span><span class="sxs-lookup"><span data-stu-id="c1928-164">In a terminal at hello root directory of hello application type hello following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="c1928-165">Bir web tarayıcısı açın ve çok Gözat**http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="c1928-165">Open a web browser and browse too**http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="c1928-166">Bu hello oluşturacak `registration_tbl` hello veritabanındaki tablo.</span><span class="sxs-lookup"><span data-stu-id="c1928-166">This will create hello `registration_tbl` table in hello database.</span></span>
6. <span data-ttu-id="c1928-167">Açık hello **php için index.php'dir** dosyasını bir metin düzenleyicisi veya IDE ve hello başlangıç sayfası için temel HTML ve CSS kodunu ekleyin (Merhaba PHP kodunun, sonraki adımlarda de eklenir).</span><span class="sxs-lookup"><span data-stu-id="c1928-167">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
        <html>
        <head>
        <Title>Registration Form</Title>
        <style type="text/css">
            body { background-color: #fff; border-top: solid 10px #000;
                color: #333; font-size: .85em; margin: 20; padding: 20;
                font-family: "Segoe UI", Verdana, Helvetica, Sans-Serif;
            }
            h1, h2, h3,{ color: #000; margin-bottom: 0; padding-bottom: 0; }
            h1 { font-size: 2em; }
            h2 { font-size: 1.75em; }
            h3 { font-size: 1.2em; }
            table { margin-top: 0.75em; }
            th { font-size: 1.2em; text-align: left; border: none; padding-left: 0; }
            td { padding: 0.25em 2em 0.25em 0em; border: 0 none; }
        </style>
        </head>
        <body>
        <h1>Register here!</h1>
        <p>Fill in your name and email address, then click <strong>Submit</strong> tooregister.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. <span data-ttu-id="c1928-168">Merhaba PHP etiketlere toohello veritabanına bağlanmak için PHP kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c1928-168">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="c1928-169">Yeniden tooupdate hello değerlerini gerekir <code>$user</code> ve <code>$pwd</code> yerel MySQL kullanıcı adı ve parola.</span><span class="sxs-lookup"><span data-stu-id="c1928-169">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="c1928-170">Merhaba veritabanı bağlantı kodu kayıt defteri bilgilerini hello veritabanına yerleştirilmesi için kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c1928-170">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
        if(!empty($_POST)) {
        try {
            $name = $_POST['name'];
            $email = $_POST['email'];
            $date = date("Y-m-d");
            // Insert data
            $sql_insert = "INSERT INTO registration_tbl (name, email, date) 
                           VALUES (?,?,?)";
            $stmt = $conn->prepare($sql_insert);
            $stmt->bindValue(1, $name);
            $stmt->bindValue(2, $email);
            $stmt->bindValue(3, $date);
            $stmt->execute();
        }
        catch(Exception $e) {
            die(var_dump($e));
        }
        echo "<h3>Your're registered!</h3>";
        }
9. <span data-ttu-id="c1928-171">Son olarak, yukarıdaki hello kod hello veritabanından veri almak için kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c1928-171">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
        $sql_select = "SELECT * FROM registration_tbl";
        $stmt = $conn->query($sql_select);
        $registrants = $stmt->fetchAll(); 
        if(count($registrants) > 0) {
            echo "<h2>People who are registered:</h2>";
            echo "<table>";
            echo "<tr><th>Name</th>";
            echo "<th>Email</th>";
            echo "<th>Date</th></tr>";
            foreach($registrants as $registrant) {
                echo "<tr><td>".$registrant['name']."</td>";
                echo "<td>".$registrant['email']."</td>";
                echo "<td>".$registrant['date']."</td></tr>";
            }
             echo "</table>";
        } else {
            echo "<h3>No one is currently registered.</h3>";
        }

<span data-ttu-id="c1928-172">Artık çok gözatabilirsiniz**http://localhost:8000/index.php** tootest Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="c1928-172">You can now browse too**http://localhost:8000/index.php** tootest hello application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="c1928-173">Uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="c1928-173">Publish your application</span></span>
<span data-ttu-id="c1928-174">Uygulamanızı yerel olarak test ettikten sonra tooApp Service Web Apps Git kullanarak yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1928-174">After you have tested your application locally, you can publish it tooApp Service Web Apps using Git.</span></span> <span data-ttu-id="c1928-175">Ancak, ilk hello uygulamasında tooupdate hello veritabanı bağlantısı bilgilerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1928-175">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="c1928-176">Daha önce aldığınız hello veritabanı bağlantı bilgilerini kullanarak (Merhaba içinde **alma SQL veritabanı bağlantı bilgilerini** bölüm), bilgileri aşağıdaki güncelleştirme hello **her ikisi de** hello `createdatabase.php` ve `index.php` hello dosyalarıyla uygun değerler:</span><span class="sxs-lookup"><span data-stu-id="c1928-176">Using hello database connection information you obtained earlier (in hello **Get SQL Database connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="c1928-177">Merhaba, <code>$host</code>, sunucu hello değerini $a, ile <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="c1928-177">In hello <code>$host</code>, hello value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="c1928-178">Şimdi, Git yayımlamayı hazır tooset olan ve hello uygulamayı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="c1928-178">Now, you are ready tooset up Git publishing and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="c1928-179">Merhaba aynı adımları not ettiğiniz hello hello sonunda bunlar **Azure web uygulaması oluşturun ve Git yayımlamayı ayarlayın** yukarıdaki bölümde.</span><span class="sxs-lookup"><span data-stu-id="c1928-179">These are hello same steps noted at hello end of hello **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="c1928-180">Bash'i açın (veya Git ise bir terminal, `PATH`), uygulamanızın dizinleri toohello kök dizini değiştirin (Merhaba **kayıt** dizin), ve çalışma hello aşağıdaki komutlar:</span><span class="sxs-lookup"><span data-stu-id="c1928-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application (hello **registration** directory), and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="c1928-181">Daha önce oluşturduğunuz hello parola istenir.</span><span class="sxs-lookup"><span data-stu-id="c1928-181">You will be prompted for hello password you created earlier.</span></span>
2. <span data-ttu-id="c1928-182">Çok Gözat**http://[web uygulama name].azurewebsites.net/createtable.php** toocreate hello SQL veritabanı tablosunda Merhaba uygulaması için.</span><span class="sxs-lookup"><span data-stu-id="c1928-182">Browse too**http://[web app name].azurewebsites.net/createtable.php** toocreate hello SQL database table for hello application.</span></span>
3. <span data-ttu-id="c1928-183">Çok Gözat**http://[web uygulama name].azurewebsites.net/index.php** Merhaba uygulaması kullanarak toobegin.</span><span class="sxs-lookup"><span data-stu-id="c1928-183">Browse too**http://[web app name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

<span data-ttu-id="c1928-184">Uygulamanızı yayımladıktan sonra değişiklikler tooit yapmaya başlamak ve Git toopublish kullanmanızı bunları.</span><span class="sxs-lookup"><span data-stu-id="c1928-184">After you have published your application, you can begin making changes tooit and use Git toopublish them.</span></span> 

## <a name="publish-changes-tooyour-application"></a><span data-ttu-id="c1928-185">Değişiklikleri tooyour uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="c1928-185">Publish changes tooyour application</span></span>
<span data-ttu-id="c1928-186">toopublish değişiklikleri tooapplication, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c1928-186">toopublish changes tooapplication, follow these steps:</span></span>

1. <span data-ttu-id="c1928-187">Değişiklik tooyour uygulamayı yerel olarak belirler.</span><span class="sxs-lookup"><span data-stu-id="c1928-187">Make changes tooyour application locally.</span></span>
2. <span data-ttu-id="c1928-188">Bash'i açın (ya da bir terminal Git olan BT, `PATH`), uygulamanızın dizinleri toohello kök dizini değiştirin ve hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c1928-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="c1928-189">Daha önce oluşturduğunuz hello parola istenir.</span><span class="sxs-lookup"><span data-stu-id="c1928-189">You will be prompted for hello password you created earlier.</span></span>
3. <span data-ttu-id="c1928-190">Çok Gözat**http://[web uygulama name].azurewebsites.net/index.php** toosee değişikliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="c1928-190">Browse too**http://[web app name].azurewebsites.net/index.php** toosee your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="c1928-191">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="c1928-191">What's changed</span></span>
* <span data-ttu-id="c1928-192">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c1928-192">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

