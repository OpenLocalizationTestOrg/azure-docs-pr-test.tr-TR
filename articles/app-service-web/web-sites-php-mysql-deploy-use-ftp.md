---
title: "aaaCreate PHP MySQL uygulamasını Azure App Service'te web ve FTP kullanarak dağıtın"
description: "Nasıl toocreate bir PHP web, FTP dağıtım tooAzure MySQL ve kullanım verilerini depolayan gösteren bir öğretici."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6d9d1de5-5868-48fd-8bad-decb4979cd65
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4d3b56a8ac63d0eba0dc0aec1b62e6d12f601bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="a5183-103">Azure App Service’ta bir PHP-MySQL web uygulaması oluşturma ve uygulamayı FTP kullanarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="a5183-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="a5183-104">Bu öğretici, toocreate PHP MySQL web nasıl uygulama ve nasıl gösterir toodeploy FTP kullanarak.</span><span class="sxs-lookup"><span data-stu-id="a5183-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it using FTP.</span></span> <span data-ttu-id="a5183-105">Bu öğretici, varsayar [PHP][install-php], [MySQL][install-mysql], bir web sunucusu ve bilgisayarınızda yüklü bir FTP istemcisi.</span><span class="sxs-lookup"><span data-stu-id="a5183-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="a5183-106">Bu öğreticideki yönergeler Hello işletim Windows, Mac ve Linux dahil olmak üzere tüm sisteminizde izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="a5183-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="a5183-107">Bu kılavuzu tamamladıktan sonra Azure'da çalışan bir PHP/MySQL web uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5183-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="a5183-108">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="a5183-108">You will learn:</span></span>

* <span data-ttu-id="a5183-109">Nasıl toocreate bir web uygulaması ve bir MySQL hello Azure Portal kullanarak veritabanı.</span><span class="sxs-lookup"><span data-stu-id="a5183-109">How toocreate a web app and a MySQL database using hello Azure Portal.</span></span> <span data-ttu-id="a5183-110">PHP Web uygulamaları varsayılan olarak etkindir, özel bir şey gerekli toorun çünkü PHP kodunuzu.</span><span class="sxs-lookup"><span data-stu-id="a5183-110">Because PHP is enabled in Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="a5183-111">Nasıl toopublish kullanarak uygulamanızı tooAzure FTP.</span><span class="sxs-lookup"><span data-stu-id="a5183-111">How toopublish your application tooAzure using FTP.</span></span>

<span data-ttu-id="a5183-112">Bu öğreticiyi izleyerek, PHP bir basit kayıt web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a5183-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="a5183-113">Merhaba uygulaması, bir Web uygulamasında barındırılan.</span><span class="sxs-lookup"><span data-stu-id="a5183-113">hello application will be hosted in a Web App.</span></span> <span data-ttu-id="a5183-114">Tamamlanan hello uygulamasının ekran görüntüsü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a5183-114">A screenshot of hello completed application is below:</span></span>

![Azure PHP Web sitesi][running-app]

> [!NOTE]
> <span data-ttu-id="a5183-116">Bir hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5183-116">If you want tooget started with Azure App Service before signing up for an account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a5183-117">Kredi kartı veya taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a5183-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="a5183-118">Bir web uygulaması oluşturun ve FTP Yayımlama Ayarla</span><span class="sxs-lookup"><span data-stu-id="a5183-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="a5183-119">Bu adımları toocreate bir web uygulaması ve bir MySQL veritabanı izleyin:</span><span class="sxs-lookup"><span data-stu-id="a5183-119">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="a5183-120">Oturum açma toohello [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="a5183-120">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="a5183-121">Merhaba tıklatın **+ yeni** hello üst simgesine sol hello Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a5183-121">Click hello **+ New** icon on hello top left of hello Azure Portal.</span></span>
   
    ![Yeni Azure Web sitesi oluştur][new-website]
3. <span data-ttu-id="a5183-123">Merhaba arama türündeki **Web uygulaması + MySQL** ve tıklayın **Web uygulaması + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="a5183-123">In hello search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Yeni Web sitesi özel oluştur][custom-create]
4. <span data-ttu-id="a5183-125">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a5183-125">Click **Create**.</span></span> <span data-ttu-id="a5183-126">Benzersiz bir uygulama hizmeti adına, hello kaynak grubu için geçerli bir ad ve yeni bir hizmet planı girin.</span><span class="sxs-lookup"><span data-stu-id="a5183-126">Enter a unique app service name, a valid name for hello resource group and a new service plan.</span></span>
   
    ![Küme kaynak grubu adı][resource-group]
5. <span data-ttu-id="a5183-128">Kabul ettiğinizi belirten dahil olmak üzere yeni veritabanınız için değerleri girin toohello yasal koşulları.</span><span class="sxs-lookup"><span data-stu-id="a5183-128">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Yeni MySQL veritabanı oluştur][new-mysql-db]
6. <span data-ttu-id="a5183-130">Merhaba web uygulaması oluşturduğunuzda hello yeni uygulama hizmeti dikey görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a5183-130">When hello web app has been created, you will see hello new app service blade.</span></span>
7. <span data-ttu-id="a5183-131">Tıklayın **ayarları** > **dağıtım kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="a5183-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Dağıtım kimlik bilgilerini ayarlama][set-deployment-credentials]
8. <span data-ttu-id="a5183-133">tooenable FTP Yayımlama, bir kullanıcı adı ve parola sağlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="a5183-133">tooenable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="a5183-134">Merhaba kimlik bilgileri kaydedin ve hello kullanıcı adı ve parola oluşturduğunuz not edin.</span><span class="sxs-lookup"><span data-stu-id="a5183-134">Save hello credentials and make a note of hello user name and password you create.</span></span>
   
    ![Yayımlama kimlik bilgileri oluşturma][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="a5183-136">Derleme ve uygulamanızı yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="a5183-136">Build and test your app locally</span></span>
<span data-ttu-id="a5183-137">Merhaba kayıt uygulama adı ve e-posta adresinizi sağlayarak bir olay için tooregister sağlayan basit bir PHP uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="a5183-137">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="a5183-138">Önceki şahıslar hakkında bilgi bir tabloda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a5183-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="a5183-139">Kayıt bilgileri bir MySQL veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="a5183-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="a5183-140">Merhaba uygulama iki dosyadan oluşur:</span><span class="sxs-lookup"><span data-stu-id="a5183-140">hello app consists of two files:</span></span>

* <span data-ttu-id="a5183-141">**PHP için index.php'dir**: kaydı ve registrant bilgi içeren bir tablo için bir form görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a5183-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="a5183-142">**CreateTable.php**: Merhaba uygulaması için hello MySQL tablosu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a5183-142">**createtable.php**: Creates hello MySQL table for hello application.</span></span> <span data-ttu-id="a5183-143">Bu dosya yalnızca bir kez kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a5183-143">This file will only be used once.</span></span>

<span data-ttu-id="a5183-144">toobuild ve yerel olarak çalıştırma hello uygulama hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="a5183-144">toobuild and run hello app locally, follow hello steps below.</span></span> <span data-ttu-id="a5183-145">PHP, MySQL ve yerel makinenizde ayarlanan bir web sunucusu varsa ve etkinleştirdiğinizden emin hello adımları varsayın Not [PDO uzantısı MySQL için][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="a5183-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="a5183-146">Adlı bir MySQL veritabanı oluşturma `registration`.</span><span class="sxs-lookup"><span data-stu-id="a5183-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="a5183-147">Bu komutla hello MySQL komut satırından bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a5183-147">You can do this from hello MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="a5183-148">Web sunucunuzun kök dizininde adlı bir klasör oluşturun `registration` ve iki dosya içinde - adlı oluşturun `createtable.php` ve adlı `index.php`.</span><span class="sxs-lookup"><span data-stu-id="a5183-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="a5183-149">Açık hello `createtable.php` dosyasını bir metin düzenleyicisi veya IDE ve hello aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a5183-149">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="a5183-150">Bu kod kullanılan toocreate hello olacaktır `registration_tbl` hello tabloda `registration` veritabanı.</span><span class="sxs-lookup"><span data-stu-id="a5183-150">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
                        id INT NOT NULL AUTO_INCREMENT, 
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
   
   > [!NOTE]
   > <span data-ttu-id="a5183-151">Tooupdate hello değerlerini gerekir <code>$user</code> ve <code>$pwd</code> yerel MySQL kullanıcı adı ve parola.</span><span class="sxs-lookup"><span data-stu-id="a5183-151">You will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="a5183-152">Bir web tarayıcısı açın ve çok Gözat[http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="a5183-152">Open a web browser and browse too[http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="a5183-153">Bu hello oluşturacak `registration_tbl` hello veritabanındaki tablo.</span><span class="sxs-lookup"><span data-stu-id="a5183-153">This will create hello `registration_tbl` table in hello database.</span></span>
5. <span data-ttu-id="a5183-154">Açık hello **php için index.php'dir** dosyasını bir metin düzenleyicisi veya IDE ve hello başlangıç sayfası için temel HTML ve CSS kodunu ekleyin (Merhaba PHP kodunun, sonraki adımlarda de eklenir).</span><span class="sxs-lookup"><span data-stu-id="a5183-154">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
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
6. <span data-ttu-id="a5183-155">Merhaba PHP etiketlere toohello veritabanına bağlanmak için PHP kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a5183-155">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="a5183-156">Yeniden tooupdate hello değerlerini gerekir <code>$user</code> ve <code>$pwd</code> yerel MySQL kullanıcı adı ve parola.</span><span class="sxs-lookup"><span data-stu-id="a5183-156">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="a5183-157">Merhaba veritabanı bağlantı kodu kayıt defteri bilgilerini hello veritabanına yerleştirilmesi için kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a5183-157">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
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
8. <span data-ttu-id="a5183-158">Son olarak, yukarıdaki hello kod hello veritabanından veri almak için kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a5183-158">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
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

<span data-ttu-id="a5183-159">Artık çok gözatabilirsiniz[http://localhost/registration/index.php] [ localhost-index] tootest hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="a5183-159">You can now browse too[http://localhost/registration/index.php][localhost-index] tootest hello app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="a5183-160">MySQL ve FTP bağlantı bilgileri alma</span><span class="sxs-lookup"><span data-stu-id="a5183-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="a5183-161">Web uygulamaları, profilinizde çalıştıran tooconnect toohello MySQL veritabanı bağlantı bilgilerini hello.</span><span class="sxs-lookup"><span data-stu-id="a5183-161">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="a5183-162">tooget MySQL bağlantı bilgilerini, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="a5183-162">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="a5183-163">Web uygulaması dikey Hello uygulama hizmetinden hello kaynak grubu bağlantıyı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a5183-163">From hello app service web app blade click on hello resource group link:</span></span>
   
    ![Kaynak Grup Seç][select-resourcegroup]
2. <span data-ttu-id="a5183-165">Kaynak grubundan hello veritabanı'nı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a5183-165">From your resource group, click hello database:</span></span>
   
    ![Veritabanını seçin][select-database]
3. <span data-ttu-id="a5183-167">Özet Hello veritabanının seçileceği **ayarları** > **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="a5183-167">From hello database summary, select **Settings** > **Properties**.</span></span>
   
    ![Özellikleri seçme][select-properties]
4. <span data-ttu-id="a5183-169">Merhaba değerlerini Not `Database`, `Host`, `User Id`, ve `Password`.</span><span class="sxs-lookup"><span data-stu-id="a5183-169">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Not özellikleri][note-properties]
5. <span data-ttu-id="a5183-171">Web uygulamanızdan hello tıklatın **yayım profili indirin** hello hello sayfanın sağ alt köşesindeki bağlantıda:</span><span class="sxs-lookup"><span data-stu-id="a5183-171">From your web app, click hello **Download publish profile** link at hello bottom right corner of hello page:</span></span>
   
    ![Yayım profili indirin][download-publish-profile]
6. <span data-ttu-id="a5183-173">Açık hello `.publishsettings` dosyasını bir XML düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="a5183-173">Open hello `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="a5183-174">Hello bulur `<publishProfile >` öğeyle `publishMethod="FTP"` benzer toothis arar:</span><span class="sxs-lookup"><span data-stu-id="a5183-174">Find hello `<publishProfile >` element with `publishMethod="FTP"` that looks similar toothis:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="a5183-175">Merhaba Not `publishUrl`, `userName`, ve `userPWD` öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="a5183-175">Make note of hello `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="a5183-176">Uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="a5183-176">Publish your app</span></span>
<span data-ttu-id="a5183-177">Uygulamanızı yerel olarak test ettikten sonra FTP kullanarak tooyour web uygulaması yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5183-177">After you have tested your app locally, you can publish it tooyour web app using FTP.</span></span> <span data-ttu-id="a5183-178">Ancak, ilk hello uygulamasında tooupdate hello veritabanı bağlantısı bilgilerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5183-178">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="a5183-179">Daha önce aldığınız hello veritabanı bağlantı bilgilerini kullanarak (Merhaba içinde **MySQL almak ve FTP bağlantı bilgileri** bölüm), bilgileri aşağıdaki güncelleştirme hello **her ikisi de** hello `createdatabase.php` ve `index.php` hello dosyalarıyla uygun değerler:</span><span class="sxs-lookup"><span data-stu-id="a5183-179">Using hello database connection information you obtained earlier (in hello **Get MySQL and FTP connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="a5183-180">Artık toopublish FTP kullanarak uygulamanızı hazır.</span><span class="sxs-lookup"><span data-stu-id="a5183-180">Now you are ready toopublish your app using FTP.</span></span>

1. <span data-ttu-id="a5183-181">Tercih, FTP İstemcisi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="a5183-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="a5183-182">Merhaba girin *ana bilgisayar adı bölümü* hello gelen `publishUrl` ettiğiniz yukarıda FTP istemciniz özniteliği.</span><span class="sxs-lookup"><span data-stu-id="a5183-182">Enter hello *host name portion* from hello `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="a5183-183">Merhaba girin `userName` ve `userPWD` yukarıda belirtilen öznitelikler, FTP istemcisi değişmeden.</span><span class="sxs-lookup"><span data-stu-id="a5183-183">Enter hello `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="a5183-184">Bağlantı kurun.</span><span class="sxs-lookup"><span data-stu-id="a5183-184">Establish a connection.</span></span>

<span data-ttu-id="a5183-185">Bağlantıyı oluşturduktan sonra mümkün tooupload olması ve gerektiğinde dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="a5183-185">After you have connected you will be able tooupload and download files as needed.</span></span> <span data-ttu-id="a5183-186">Olan dosyaları toohello kök dizini yüklediğinizden emin olun `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="a5183-186">Be sure that you are uploading files toohello root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="a5183-187">Her ikisi de karşıya sonra `index.php` ve `createtable.php`, çok Gözat**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL tablo hello uygulama için sonra çok Gözat**http://[site adı ].azurewebsites.net/index.php** Merhaba uygulaması kullanarak toobegin.</span><span class="sxs-lookup"><span data-stu-id="a5183-187">After uploading both `index.php` and `createtable.php`, browse too**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL table for hello application, then browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5183-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a5183-188">Next steps</span></span>
<span data-ttu-id="a5183-189">Daha fazla bilgi için bkz: Merhaba [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="a5183-189">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-mysql]: http://dev.mysql.com/doc/refman/5.6/en/installing.html
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[localhost-createtable]: http://localhost/tasklist/createtable.php
[localhost-index]: http://localhost/tasklist/index.php
[running-app]: ./media/web-sites-php-mysql-deploy-use-ftp/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-ftp/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-ftp/create_web_mysql.png
[website-details]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/website_details.jpg
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-ftp/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-ftp/select_webapp.png
[set-deployment-credentials]: ./media/web-sites-php-mysql-deploy-use-ftp/set_credentials.png
[portal-ftp-username-password]: ./media/web-sites-php-mysql-deploy-use-ftp/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-ftp/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-ftp/create_wa.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-ftp/select_database.png
[select-resourcegroup]: ./media/web-sites-php-mysql-deploy-use-ftp/select_resourcegroup.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/note-properties.png

[connection-string-info]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/connection_string_info.png
[management-portal]: https://portal.azure.com
[download-publish-profile]: ./media/web-sites-php-mysql-deploy-use-ftp/download_publish_profile_3.png

