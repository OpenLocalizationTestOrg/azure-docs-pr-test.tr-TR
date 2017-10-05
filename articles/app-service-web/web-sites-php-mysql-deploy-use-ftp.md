---
title: "Azure App Service’ta bir PHP-MySQL web uygulaması oluşturma ve uygulamayı FTP kullanarak dağıtma"
description: "Azure için MySQL ve kullanım FTP dağıtımında verilerini depolayan bir PHP web uygulamasının nasıl oluşturulacağını gösteren bir öğretici."
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
ms.openlocfilehash: d428dffc6b810a692be0ec39a5f9cca05f5439e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="7f2db-103">Azure App Service’ta bir PHP-MySQL web uygulaması oluşturma ve uygulamayı FTP kullanarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="7f2db-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="7f2db-104">Bu öğretici, bir PHP MySQL web uygulamasının nasıl oluşturulacağını ve FTP kullanarak dağıtma gösterir.</span><span class="sxs-lookup"><span data-stu-id="7f2db-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it using FTP.</span></span> <span data-ttu-id="7f2db-105">Bu öğretici, varsayar [PHP][install-php], [MySQL][install-mysql], bir web sunucusu ve bilgisayarınızda yüklü bir FTP istemcisi.</span><span class="sxs-lookup"><span data-stu-id="7f2db-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="7f2db-106">Bu öğreticideki yönergeler işletim Windows, Mac ve Linux dahil olmak üzere tüm sisteminizde izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="7f2db-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="7f2db-107">Bu kılavuzu tamamladıktan sonra Azure'da çalışan bir PHP/MySQL web uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f2db-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="7f2db-108">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="7f2db-108">You will learn:</span></span>

* <span data-ttu-id="7f2db-109">Bir web uygulaması ve Azure Portalı'nı kullanarak bir MySQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f2db-109">How to create a web app and a MySQL database using the Azure Portal.</span></span> <span data-ttu-id="7f2db-110">PHP Web uygulamaları varsayılan olarak etkinleştirilmiş olduğundan, özel bir şey PHP kodunuzu çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7f2db-110">Because PHP is enabled in Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="7f2db-111">FTP kullanarak Azure uygulamanızı yayımlamak nasıl.</span><span class="sxs-lookup"><span data-stu-id="7f2db-111">How to publish your application to Azure using FTP.</span></span>

<span data-ttu-id="7f2db-112">Bu öğreticiyi izleyerek, PHP bir basit kayıt web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7f2db-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="7f2db-113">Uygulama bir Web uygulamasını barındırılan.</span><span class="sxs-lookup"><span data-stu-id="7f2db-113">The application will be hosted in a Web App.</span></span> <span data-ttu-id="7f2db-114">Tamamlanmış uygulamanın bir ekran görüntüsü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7f2db-114">A screenshot of the completed application is below:</span></span>

![Azure PHP Web sitesi][running-app]

> [!NOTE]
> <span data-ttu-id="7f2db-116">Bir hesabı için kaydolmadan önce Azure App Service'i kullanmaya başlamak istiyorsanız, Git [App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f2db-116">If you want to get started with Azure App Service before signing up for an account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7f2db-117">Kredi kartı veya taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7f2db-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="7f2db-118">Bir web uygulaması oluşturun ve FTP Yayımlama Ayarla</span><span class="sxs-lookup"><span data-stu-id="7f2db-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="7f2db-119">Bir web uygulaması ve bir MySQL veritabanı oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7f2db-119">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="7f2db-120">Oturum açma [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="7f2db-120">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="7f2db-121">Tıklatın **+ yeni** üst simgesine sol Azure Portal'ın.</span><span class="sxs-lookup"><span data-stu-id="7f2db-121">Click the **+ New** icon on the top left of the Azure Portal.</span></span>
   
    ![Yeni Azure Web sitesi oluştur][new-website]
3. <span data-ttu-id="7f2db-123">Arama türündeki **Web uygulaması + MySQL** ve tıklayın **Web uygulaması + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="7f2db-123">In the search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Yeni Web sitesi özel oluştur][custom-create]
4. <span data-ttu-id="7f2db-125">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f2db-125">Click **Create**.</span></span> <span data-ttu-id="7f2db-126">Benzersiz bir uygulama hizmeti adına, kaynak grubu ve yeni bir hizmet planı için geçerli bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="7f2db-126">Enter a unique app service name, a valid name for the resource group and a new service plan.</span></span>
   
    ![Küme kaynak grubu adı][resource-group]
5. <span data-ttu-id="7f2db-128">Yasal koşulları kabul ettiğinizi belirten dahil olmak üzere, yeni bir veritabanı için değerler girin.</span><span class="sxs-lookup"><span data-stu-id="7f2db-128">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Yeni MySQL veritabanı oluştur][new-mysql-db]
6. <span data-ttu-id="7f2db-130">Web uygulaması oluşturduğunuzda, yeni uygulama hizmeti dikey penceresini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7f2db-130">When the web app has been created, you will see the new app service blade.</span></span>
7. <span data-ttu-id="7f2db-131">Tıklayın **ayarları** > **dağıtım kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="7f2db-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Dağıtım kimlik bilgilerini ayarlama][set-deployment-credentials]
8. <span data-ttu-id="7f2db-133">FTP yayımlamayı etkinleştirmek için bir kullanıcı adı ve parolasını sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f2db-133">To enable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="7f2db-134">Kimlik bilgileri kaydedin ve oluşturduğunuz parola ve kullanıcı adını not edin.</span><span class="sxs-lookup"><span data-stu-id="7f2db-134">Save the credentials and make a note of the user name and password you create.</span></span>
   
    ![Yayımlama kimlik bilgileri oluşturma][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="7f2db-136">Derleme ve uygulamanızı yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="7f2db-136">Build and test your app locally</span></span>
<span data-ttu-id="7f2db-137">Kayıt uygulama kaydetmek bir olay için ad ve e-posta adresinizi sağlayarak sağlayan basit bir PHP uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="7f2db-137">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="7f2db-138">Önceki şahıslar hakkında bilgi bir tabloda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7f2db-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="7f2db-139">Kayıt bilgileri bir MySQL veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="7f2db-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="7f2db-140">Uygulama iki dosyadan oluşur:</span><span class="sxs-lookup"><span data-stu-id="7f2db-140">The app consists of two files:</span></span>

* <span data-ttu-id="7f2db-141">**PHP için index.php'dir**: kaydı ve registrant bilgi içeren bir tablo için bir form görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7f2db-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="7f2db-142">**CreateTable.php**: uygulama için MySQL tablosu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7f2db-142">**createtable.php**: Creates the MySQL table for the application.</span></span> <span data-ttu-id="7f2db-143">Bu dosya yalnızca bir kez kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7f2db-143">This file will only be used once.</span></span>

<span data-ttu-id="7f2db-144">Derleme ve uygulamayı yerel olarak çalıştırmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="7f2db-144">To build and run the app locally, follow the steps below.</span></span> <span data-ttu-id="7f2db-145">Bu adımları PHP, MySQL ve yerel makinenizde ayarlanan bir web sunucusu, olduğunu varsayın Not ve etkinleştirdiğiniz [PDO uzantısı MySQL için][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="7f2db-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="7f2db-146">Adlı bir MySQL veritabanı oluşturma `registration`.</span><span class="sxs-lookup"><span data-stu-id="7f2db-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="7f2db-147">Bu komutla MySQL komut isteminden bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7f2db-147">You can do this from the MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="7f2db-148">Web sunucunuzun kök dizininde adlı bir klasör oluşturun `registration` ve iki dosya içinde - adlı oluşturun `createtable.php` ve adlı `index.php`.</span><span class="sxs-lookup"><span data-stu-id="7f2db-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="7f2db-149">Açık `createtable.php` dosyasını bir metin düzenleyicisi veya IDE ve aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f2db-149">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="7f2db-150">Bu kodu oluşturmak için kullanılan `registration_tbl` tablosundaki `registration` veritabanı.</span><span class="sxs-lookup"><span data-stu-id="7f2db-150">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
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
   > <span data-ttu-id="7f2db-151">Değerleri güncelleştirmeniz gerekecektir <code>$user</code> ve <code>$pwd</code> yerel MySQL kullanıcı adı ve parola.</span><span class="sxs-lookup"><span data-stu-id="7f2db-151">You will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="7f2db-152">Bir web tarayıcısı açın ve [http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="7f2db-152">Open a web browser and browse to [http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="7f2db-153">Bu oluşturacak `registration_tbl` veritabanındaki tablo.</span><span class="sxs-lookup"><span data-stu-id="7f2db-153">This will create the `registration_tbl` table in the database.</span></span>
5. <span data-ttu-id="7f2db-154">Açık **php için index.php'dir** dosyasını bir metin düzenleyicisi veya IDE ve (PHP kodunun, sonraki adımlarda de eklenir) sayfanın temel HTML ve CSS kodunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f2db-154">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
        <p>Fill in your name and email address, then click <strong>Submit</strong> to register.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
6. <span data-ttu-id="7f2db-155">PHP etiketleri içinde veritabanına bağlanmak için PHP kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f2db-155">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="7f2db-156">Yeniden değerleri güncelleştirmeniz gerekecektir <code>$user</code> ve <code>$pwd</code> yerel MySQL kullanıcı adı ve parola.</span><span class="sxs-lookup"><span data-stu-id="7f2db-156">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="7f2db-157">Veritabanı bağlantı kodu kayıt defteri bilgilerini veritabanına eklemek için kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f2db-157">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
8. <span data-ttu-id="7f2db-158">Son olarak, yukarıdaki kod veritabanından veri almak için kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f2db-158">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="7f2db-159">Şimdi gözatabilirsiniz [http://localhost/registration/index.php] [ localhost-index] uygulamayı test etmek için.</span><span class="sxs-lookup"><span data-stu-id="7f2db-159">You can now browse to [http://localhost/registration/index.php][localhost-index] to test the app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="7f2db-160">MySQL ve FTP bağlantı bilgileri alma</span><span class="sxs-lookup"><span data-stu-id="7f2db-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="7f2db-161">Web uygulamaları, profilinizde çalıştıran MySQL veritabanına bağlanmak için bağlantı bilgilerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f2db-161">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="7f2db-162">MySQL bağlantı bilgilerini almak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7f2db-162">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="7f2db-163">Web uygulaması dikey uygulama hizmetinden kaynak grubu bağlantıyı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="7f2db-163">From the app service web app blade click on the resource group link:</span></span>
   
    ![Kaynak Grup Seç][select-resourcegroup]
2. <span data-ttu-id="7f2db-165">Veritabanını, kaynak grubundan tıklatın:</span><span class="sxs-lookup"><span data-stu-id="7f2db-165">From your resource group, click the database:</span></span>
   
    ![Veritabanını seçin][select-database]
3. <span data-ttu-id="7f2db-167">Özet veritabanından seçin **ayarları** > **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="7f2db-167">From the database summary, select **Settings** > **Properties**.</span></span>
   
    ![Özellikleri seçme][select-properties]
4. <span data-ttu-id="7f2db-169">Değerlerini Not `Database`, `Host`, `User Id`, ve `Password`.</span><span class="sxs-lookup"><span data-stu-id="7f2db-169">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Not özellikleri][note-properties]
5. <span data-ttu-id="7f2db-171">Web uygulamanızdan tıklatın **yayım profili indirin** sayfanın sağ alt köşesindeki bağlantıda:</span><span class="sxs-lookup"><span data-stu-id="7f2db-171">From your web app, click the **Download publish profile** link at the bottom right corner of the page:</span></span>
   
    ![Yayım profili indirin][download-publish-profile]
6. <span data-ttu-id="7f2db-173">Açık `.publishsettings` dosyasını bir XML düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="7f2db-173">Open the `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="7f2db-174">Bul `<publishProfile >` öğeyle `publishMethod="FTP"` , aşağıdakine benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="7f2db-174">Find the `<publishProfile >` element with `publishMethod="FTP"` that looks similar to this:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="7f2db-175">Not `publishUrl`, `userName`, ve `userPWD` öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="7f2db-175">Make note of the `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="7f2db-176">Uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="7f2db-176">Publish your app</span></span>
<span data-ttu-id="7f2db-177">Uygulamanızı yerel olarak test ettikten sonra web uygulamanıza FTP kullanarak yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f2db-177">After you have tested your app locally, you can publish it to your web app using FTP.</span></span> <span data-ttu-id="7f2db-178">Ancak, ilk uygulamasında veritabanı bağlantısı bilgilerini güncelleştirmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f2db-178">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="7f2db-179">Daha önce aldığınız veritabanı bağlantı bilgilerini kullanarak (içinde **MySQL almak ve FTP bağlantı bilgileri** bölüm), aşağıdaki bilgileri güncelleştirin **her ikisi de** `createdatabase.php` ve `index.php` uygun değerlerle dosyaları:</span><span class="sxs-lookup"><span data-stu-id="7f2db-179">Using the database connection information you obtained earlier (in the **Get MySQL and FTP connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="7f2db-180">Şimdi FTP kullanarak uygulamanızı yayımlamak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="7f2db-180">Now you are ready to publish your app using FTP.</span></span>

1. <span data-ttu-id="7f2db-181">Tercih, FTP İstemcisi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="7f2db-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="7f2db-182">Girin *ana bilgisayar adı bölümü* gelen `publishUrl` ettiğiniz yukarıda FTP istemciniz özniteliği.</span><span class="sxs-lookup"><span data-stu-id="7f2db-182">Enter the *host name portion* from the `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="7f2db-183">Girin `userName` ve `userPWD` yukarıda belirtilen öznitelikler, FTP istemcisi değişmeden.</span><span class="sxs-lookup"><span data-stu-id="7f2db-183">Enter the `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="7f2db-184">Bağlantı kurun.</span><span class="sxs-lookup"><span data-stu-id="7f2db-184">Establish a connection.</span></span>

<span data-ttu-id="7f2db-185">Bağlantıyı oluşturduktan sonra karşıya yükleme ve gerektiğinde dosyaları indirme mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7f2db-185">After you have connected you will be able to upload and download files as needed.</span></span> <span data-ttu-id="7f2db-186">Olduğu kök dizinine dosyaları karşıya mutlaka `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="7f2db-186">Be sure that you are uploading files to the root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="7f2db-187">Her ikisi de karşıya sonra `index.php` ve `createtable.php`, Gözat **http://[site name].azurewebsites.net/createtable.php** uygulama için MySQL tablo oluşturmak için göz **http://[site adı]. azurewebsites.NET/index.php** uygulamayı kullanmaya başlamak için.</span><span class="sxs-lookup"><span data-stu-id="7f2db-187">After uploading both `index.php` and `createtable.php`, browse to **http://[site name].azurewebsites.net/createtable.php** to create the MySQL table for the application, then browse to **http://[site name].azurewebsites.net/index.php** to begin using the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f2db-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7f2db-188">Next steps</span></span>
<span data-ttu-id="7f2db-189">Daha fazla bilgi için bkz: [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="7f2db-189">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

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

