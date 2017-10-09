---
title: "aaaCreate PHP MySQL web uygulaması Azure App Service'te ve Git kullanarak dağıtın"
description: "Nasıl toocreate bir PHP MySQL verilerini depolayan web ve Git dağıtım tooAzure kullanmak gösteren bir öğretici."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
tags: mysql
ms.assetid: 7454475f-e275-4bc7-9f09-1ef07382e5da
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 9c22946777598cc973cd9dfc8d2a258bd08cc39a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="d7023-103">Azure App Service’ta bir PHP-MySQL web uygulaması oluşturma ve uygulamayı Git kullanarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="d7023-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="d7023-104">Bu öğretici, toocreate PHP MySQL web nasıl uygulama ve nasıl gösterir toodeploy, çok[uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) Git kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d7023-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="d7023-105">Kullanacağınız [PHP][install-php], MySQL komut satırı aracı hello (parçası [MySQL][install-mysql]), ve [Git] [ install-git] bilgisayarınızda yüklü.</span><span class="sxs-lookup"><span data-stu-id="d7023-105">You will use [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="d7023-106">Bu öğreticideki yönergeler Hello işletim Windows, Mac ve Linux dahil olmak üzere tüm sisteminizde izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="d7023-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="d7023-107">Bu kılavuzu tamamladıktan sonra Azure'da çalışan bir PHP/MySQL web uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7023-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="d7023-108">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="d7023-108">You will learn:</span></span>

* <span data-ttu-id="d7023-109">Nasıl hello kullanarak toocreate bir web uygulaması ve bir MySQL veritabanı [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="d7023-109">How toocreate a web app and a MySQL database using hello [Azure Portal][management-portal].</span></span> <span data-ttu-id="d7023-110">PHP etkin olduğundan [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) varsayılan olarak, özel bir şey gerekli toorun olan PHP kodunuzu.</span><span class="sxs-lookup"><span data-stu-id="d7023-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="d7023-111">Nasıl toopublish ve Git kullanarak, uygulama tooAzure yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="d7023-111">How toopublish and re-publish your application tooAzure using Git.</span></span>
* <span data-ttu-id="d7023-112">Nasıl adresindeki tooenable hello Composer uzantısını tooautomate Oluşturucu görevleri her `git push`.</span><span class="sxs-lookup"><span data-stu-id="d7023-112">How tooenable hello Composer extension tooautomate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="d7023-113">Bu öğreticiyi izleyerek, PHP bir basit kayıt web uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d7023-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="d7023-114">Merhaba uygulaması, Web uygulamalarında barındırılan.</span><span class="sxs-lookup"><span data-stu-id="d7023-114">hello application will be hosted in Web Apps.</span></span> <span data-ttu-id="d7023-115">Tamamlanan hello uygulamasının ekran görüntüsü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d7023-115">A screenshot of hello completed application is below:</span></span>

![Azure PHP web sitesi][running-app]

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="d7023-117">Merhaba geliştirme ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="d7023-117">Set up hello development environment</span></span>
<span data-ttu-id="d7023-118">Bu öğretici, varsayar [PHP][install-php], MySQL komut satırı aracı hello (parçası [MySQL][install-mysql]), ve [Git] [ install-git] bilgisayarınızda yüklü.</span><span class="sxs-lookup"><span data-stu-id="d7023-118">This tutorial assumes you have [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="d7023-119">Bir web uygulaması oluşturma ve Git yayımlama Ayarla</span><span class="sxs-lookup"><span data-stu-id="d7023-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="d7023-120">Bu adımları toocreate bir web uygulaması ve bir MySQL veritabanı izleyin:</span><span class="sxs-lookup"><span data-stu-id="d7023-120">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="d7023-121">Oturum açma toohello [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="d7023-121">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="d7023-122">Merhaba tıklatın **yeni** simgesi.</span><span class="sxs-lookup"><span data-stu-id="d7023-122">Click hello **New** icon.</span></span>
3. <span data-ttu-id="d7023-123">Tıklatın **bkz tüm** sonraki çok**Market**.</span><span class="sxs-lookup"><span data-stu-id="d7023-123">Click **See All** next too**Marketplace**.</span></span> 
4. <span data-ttu-id="d7023-124">Tıklatın **Web + mobil**, ardından **Web uygulaması + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="d7023-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="d7023-125">Sonra, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d7023-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="d7023-126">Kaynak grubunuz için geçerli bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="d7023-126">Enter a valid name for your resource group.</span></span>
   
    ![Küme kaynak grubu adı][resource-group]
6. <span data-ttu-id="d7023-128">Yeni web uygulamanız için değerler girin.</span><span class="sxs-lookup"><span data-stu-id="d7023-128">Enter values for your new web app.</span></span>
   
    ![Web uygulaması oluşturma][new-web-app]
7. <span data-ttu-id="d7023-130">Kabul ettiğinizi belirten dahil olmak üzere yeni veritabanınız için değerleri girin toohello yasal koşulları.</span><span class="sxs-lookup"><span data-stu-id="d7023-130">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Yeni MySQL veritabanı oluştur][new-mysql-db]
8. <span data-ttu-id="d7023-132">Merhaba web uygulaması oluşturduğunuzda hello yeni web uygulaması dikey görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d7023-132">When hello web app has been created, you will see hello new web app blade.</span></span>
9. <span data-ttu-id="d7023-133">İçinde **ayarları** tıklayın **sürekli dağıtım**, tıklayın *gerekli ayarları Yapılandır*.</span><span class="sxs-lookup"><span data-stu-id="d7023-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Git yayımlama Ayarla][setup-publishing]
10. <span data-ttu-id="d7023-135">Seçin **yerel Git deposu** hello kaynağı için.</span><span class="sxs-lookup"><span data-stu-id="d7023-135">Select **Local Git Repository** for hello source.</span></span>
    
     ![Git deposu ayarlama][setup-repository]
11. <span data-ttu-id="d7023-137">tooenable yayımlama Git, kullanıcı adı ve parola sağlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="d7023-137">tooenable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="d7023-138">Merhaba kullanıcı adı ve parola oluşturduğunuz not edin.</span><span class="sxs-lookup"><span data-stu-id="d7023-138">Make a note of hello user name and password you create.</span></span> <span data-ttu-id="d7023-139">(Önce bir Git deposu ayarladıysanız, bu adım atlanır.)</span><span class="sxs-lookup"><span data-stu-id="d7023-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Yayımlama kimlik bilgileri oluşturma][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="d7023-141">Uzak MySQL bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="d7023-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="d7023-142">Web uygulamaları, profilinizde çalıştıran tooconnect toohello MySQL veritabanı bağlantı bilgilerini hello.</span><span class="sxs-lookup"><span data-stu-id="d7023-142">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="d7023-143">tooget MySQL bağlantı bilgilerini, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d7023-143">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="d7023-144">Kaynak grubundan hello veritabanı'nı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="d7023-144">From your resource group, click hello database:</span></span>
   
    ![Veritabanını seçin][select-database]
2. <span data-ttu-id="d7023-146">Merhaba veritabanından **ayarları**seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="d7023-146">From hello database **Settings**, select **Properties**.</span></span>
   
    ![Özellikleri seçme][select-properties]
3. <span data-ttu-id="d7023-148">Merhaba değerlerini Not `Database`, `Host`, `User Id`, ve `Password`.</span><span class="sxs-lookup"><span data-stu-id="d7023-148">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Not özellikleri][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="d7023-150">Derleme ve uygulamanızı yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="d7023-150">Build and test your app locally</span></span>
<span data-ttu-id="d7023-151">Bir web uygulaması oluşturduğunuza göre uygulamanızı yerel olarak geliştirme ve ardından test sonra dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d7023-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="d7023-152">Merhaba kayıt uygulama adı ve e-posta adresinizi sağlayarak bir olay için tooregister sağlayan basit bir PHP uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="d7023-152">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="d7023-153">Önceki şahıslar hakkında bilgi bir tabloda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d7023-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="d7023-154">Kayıt bilgileri bir MySQL veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="d7023-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="d7023-155">Merhaba uygulama bir dosya (kopyala/yapıştır kodu aşağıda kullanılabilir) oluşur:</span><span class="sxs-lookup"><span data-stu-id="d7023-155">hello application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="d7023-156">**PHP için index.php'dir**: kaydı ve registrant bilgi içeren bir tablo için bir form görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d7023-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="d7023-157">toobuild ve yerel olarak çalıştırma Merhaba uygulaması hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="d7023-157">toobuild and run hello application locally, follow hello steps below.</span></span> <span data-ttu-id="d7023-158">Bu adımları hello PHP ve MySQL komut satırı aracı (MySQL parçası) yerel makinenizde ayarlanmış olması ve hello etkinleştirdiğiniz varsayılır unutmayın [PDO uzantısı MySQL için][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="d7023-158">Note that these steps assume you have hello PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="d7023-159">Merhaba değerini kullanarak toohello uzak MySQL, sunucuya `Data Source`, `User Id`, `Password`, ve `Database` daha önce aldığınız:</span><span class="sxs-lookup"><span data-stu-id="d7023-159">Connect toohello remote MySQL server, using hello value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="d7023-160">Merhaba MySQL komut istemi görünür:</span><span class="sxs-lookup"><span data-stu-id="d7023-160">hello MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="d7023-161">Merhaba aşağıdaki Yapıştır `CREATE TABLE` komutu toocreate hello `registration_tbl` veritabanınızı tabloda:</span><span class="sxs-lookup"><span data-stu-id="d7023-161">Paste in hello following `CREATE TABLE` command toocreate hello `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="d7023-162">Yerel uygulama klasörüne Hello kök dizininde oluşturmak **php için index.php'dir** dosya.</span><span class="sxs-lookup"><span data-stu-id="d7023-162">In hello root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="d7023-163">Açık hello **php için index.php'dir** dosyasını bir metin düzenleyicisi veya IDE ve koddan hello ve tam hello gerekli değişiklikleri işaretlenmiş ekleyin `//TODO:` açıklamaları.</span><span class="sxs-lookup"><span data-stu-id="d7023-163">Open hello **index.php** file in a text editor or IDE and add hello following code, and complete hello necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update hello values for $host, $user, $pwd, and $db
            //using hello values you retrieved earlier from hello Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect toodatabase.
            try {
                $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
                $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            }
            catch(Exception $e){
                die(var_dump($e));
            }
            // Insert registration info
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
            // Retrieve data
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
        ?>
        </body>
        </html>

1. <span data-ttu-id="d7023-164">Aşağıdaki komutu bir terminal gidin tooyour uygulama klasörü ve türü hello:</span><span class="sxs-lookup"><span data-stu-id="d7023-164">In a terminal go tooyour application folder and type hello following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="d7023-165">Artık çok gözatabilirsiniz**8000 /** tootest Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d7023-165">You can now browse too**http://localhost:8000/** tootest hello application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="d7023-166">Uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="d7023-166">Publish your app</span></span>
<span data-ttu-id="d7023-167">Uygulamanızı yerel olarak test ettikten sonra Git kullanarak tooWeb uygulamaları yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7023-167">After you have tested your app locally, you can publish it tooWeb Apps using Git.</span></span> <span data-ttu-id="d7023-168">Yerel Git deponuzu başlatmak ve yayımlama hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="d7023-168">You will initialize your local Git repository and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="d7023-169">Bunlar olan hello aynı hello Azure Portalı'hello sonunda hello bir web uygulaması oluşturma ve ayarlama Git yayımlama bölümüne yukarıdaki yukarı gösterilen adımları.</span><span class="sxs-lookup"><span data-stu-id="d7023-169">These are hello same steps shown in hello Azure Portal at hello end of hello Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="d7023-170">(İsteğe bağlı)  Unutulan veya Git uzak repostitory URL'nizi yanlış toohello web uygulama özellikleri hello Azure Portal gidin.</span><span class="sxs-lookup"><span data-stu-id="d7023-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate toohello web app properties on hello Azure Portal.</span></span>
2. <span data-ttu-id="d7023-171">Bash'i açın (ya da bir terminal Git ise, `PATH`), uygulamanızın dizinleri toohello kök dizini değiştirin ve hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d7023-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="d7023-172">Daha önce oluşturduğunuz hello parola istenir.</span><span class="sxs-lookup"><span data-stu-id="d7023-172">You will be prompted for hello password you created earlier.</span></span>
   
    ![İlk anında iletme tooAzure Git aracılığıyla][git-initial-push]
3. <span data-ttu-id="d7023-174">Çok Gözat**http://[site name].azurewebsites.net/index.php** toobegin (Bu bilgiler, hesap Panonuzda de depolanacağı) hello uygulamasını kullanarak:</span><span class="sxs-lookup"><span data-stu-id="d7023-174">Browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application (this information will be stored on your account dashboard):</span></span>
   
    ![Azure PHP web sitesi][running-app]

<span data-ttu-id="d7023-176">Uygulamanızı yayımladıktan sonra değişiklikler tooit yapmaya başlamak ve Git toopublish kullanmanızı bunları.</span><span class="sxs-lookup"><span data-stu-id="d7023-176">After you have published your app, you can begin making changes tooit and use Git toopublish them.</span></span>

## <a name="publish-changes-tooyour-app"></a><span data-ttu-id="d7023-177">Değişiklikleri tooyour uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="d7023-177">Publish changes tooyour app</span></span>
<span data-ttu-id="d7023-178">toopublish değişiklikleri tooyour uygulama, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d7023-178">toopublish changes tooyour app, follow these steps:</span></span>

1. <span data-ttu-id="d7023-179">Değişiklikleri tooyour uygulamasını yerel olarak olun.</span><span class="sxs-lookup"><span data-stu-id="d7023-179">Make changes tooyour app locally.</span></span>
2. <span data-ttu-id="d7023-180">Bash'i açın (ya da bir terminal Git olan BT, `PATH`), uygulamanızın dizinleri toohello kök dizini değiştirin ve hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d7023-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your app, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="d7023-181">Daha önce oluşturduğunuz hello parola istenir.</span><span class="sxs-lookup"><span data-stu-id="d7023-181">You will be prompted for hello password you created earlier.</span></span>
   
    ![Site Ftp'den Git aracılığıyla tooAzure değiştirir][git-change-push]
3. <span data-ttu-id="d7023-183">Çok Gözat**http://[site name].azurewebsites.net/index.php** toosee uygulamanızı ve yapılan değişiklikler:</span><span class="sxs-lookup"><span data-stu-id="d7023-183">Browse too**http://[site name].azurewebsites.net/index.php** toosee your app and any changes you may have made:</span></span>
   
    ![Azure PHP web sitesi][running-app]

> [!NOTE]
> <span data-ttu-id="d7023-185">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7023-185">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d7023-186">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d7023-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a><span data-ttu-id="d7023-187">Oluşturucu otomasyon ile Merhaba Composer uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d7023-187">Enable Composer automation with hello Composer extension</span></span>
<span data-ttu-id="d7023-188">PHP projeniz varsa varsayılan olarak, App Service'te hello git dağıtım işlemi ile composer.json, hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="d7023-188">By default, hello git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="d7023-189">İşleme sırasında composer.json etkinleştirebilirsiniz `git push` hello Composer uzantısını etkinleştirerek.</span><span class="sxs-lookup"><span data-stu-id="d7023-189">You can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

1. <span data-ttu-id="d7023-190">PHP ile web uygulamanızın dikey penceresinde hello [Azure portal][management-portal], tıklatın **Araçları** > **uzantıları**.</span><span class="sxs-lookup"><span data-stu-id="d7023-190">In your PHP web app's blade in hello [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Oluşturucu uzantı ayarları][composer-extension-settings]
2. <span data-ttu-id="d7023-192">Tıklatın **Ekle**, ardından **Oluşturucu**.</span><span class="sxs-lookup"><span data-stu-id="d7023-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Composer uzantısını Ekle][composer-extension-add]
3. <span data-ttu-id="d7023-194">Tıklatın **Tamam** tooaccept yasal koşulları.</span><span class="sxs-lookup"><span data-stu-id="d7023-194">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="d7023-195">Tıklatın **Tamam** yeniden tooadd hello uzantısı.</span><span class="sxs-lookup"><span data-stu-id="d7023-195">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="d7023-196">Merhaba **yüklü uzantıları** dikey şimdi hello Composer uzantısını göster.</span><span class="sxs-lookup"><span data-stu-id="d7023-196">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="d7023-197">![Composer uzantısını görünümü][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="d7023-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="d7023-198">Şimdi, gerçekleştirmek `git add`, `git commit`, ve `git push` hello önceki bölümde ister.</span><span class="sxs-lookup"><span data-stu-id="d7023-198">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="d7023-199">Oluşturucu composer.json içinde tanımlanan bağımlılıklar yüklüyor şimdi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d7023-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Composer uzantısını başarılı][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="d7023-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d7023-201">Next steps</span></span>
<span data-ttu-id="d7023-202">Daha fazla bilgi için bkz: Merhaba [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="d7023-202">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

<!-- URL List -->

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[install-mysql]: http://dev.mysql.com/downloads/mysql/
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[management-portal]: https://portal.azure.com
[sql-database-editions]: http://msdn.microsoft.com/library/windowsazure/ee621788.aspx

<!-- IMG List -->

[running-app]: ./media/web-sites-php-mysql-deploy-use-git/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-git/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-git/create_web_mysql.png
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-git/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-git/select_webapp.png
[setup-git-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_git_publishing.png
[credentials]: ./media/web-sites-php-mysql-deploy-use-git/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-git/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-git/create_wa.png
[setup-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_deploy.png
[setup-repository]: ./media/web-sites-php-mysql-deploy-use-git/select_local_git.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-git/select_database.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-git/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-git/note-properties.png

[git-instructions]: ./media/web-sites-php-mysql-deploy-use-git/git-instructions.png
[git-change-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-change-push.png
[git-initial-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-initial-push.png

[composer-extension-settings]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-settings.png
[composer-extension-add]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-add.png
[composer-extension-view]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-view.png
[composer-extension-success]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-success.png
