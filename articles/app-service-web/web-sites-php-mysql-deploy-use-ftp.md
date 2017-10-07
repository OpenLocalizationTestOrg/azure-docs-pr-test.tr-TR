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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>Azure App Service’ta bir PHP-MySQL web uygulaması oluşturma ve uygulamayı FTP kullanarak dağıtma
Bu öğretici, toocreate PHP MySQL web nasıl uygulama ve nasıl gösterir toodeploy FTP kullanarak. Bu öğretici, varsayar [PHP][install-php], [MySQL][install-mysql], bir web sunucusu ve bilgisayarınızda yüklü bir FTP istemcisi. Bu öğreticideki yönergeler Hello işletim Windows, Mac ve Linux dahil olmak üzere tüm sisteminizde izlenebilir. Bu kılavuzu tamamladıktan sonra Azure'da çalışan bir PHP/MySQL web uygulaması gerekir.

Şunları öğreneceksiniz:

* Nasıl toocreate bir web uygulaması ve bir MySQL hello Azure Portal kullanarak veritabanı. PHP Web uygulamaları varsayılan olarak etkindir, özel bir şey gerekli toorun çünkü PHP kodunuzu.
* Nasıl toopublish kullanarak uygulamanızı tooAzure FTP.

Bu öğreticiyi izleyerek, PHP bir basit kayıt web uygulaması oluşturacaksınız. Merhaba uygulaması, bir Web uygulamasında barındırılan. Tamamlanan hello uygulamasının ekran görüntüsü aşağıda verilmiştir:

![Azure PHP Web sitesi][running-app]

> [!NOTE]
> Bir hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı veya taahhüt gerekmez. 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>Bir web uygulaması oluşturun ve FTP Yayımlama Ayarla
Bu adımları toocreate bir web uygulaması ve bir MySQL veritabanı izleyin:

1. Oturum açma toohello [Azure Portal][management-portal].
2. Merhaba tıklatın **+ yeni** hello üst simgesine sol hello Azure Portal.
   
    ![Yeni Azure Web sitesi oluştur][new-website]
3. Merhaba arama türündeki **Web uygulaması + MySQL** ve tıklayın **Web uygulaması + MySQL**.
   
    ![Yeni Web sitesi özel oluştur][custom-create]
4. **Oluştur**'a tıklayın. Benzersiz bir uygulama hizmeti adına, hello kaynak grubu için geçerli bir ad ve yeni bir hizmet planı girin.
   
    ![Küme kaynak grubu adı][resource-group]
5. Kabul ettiğinizi belirten dahil olmak üzere yeni veritabanınız için değerleri girin toohello yasal koşulları.
   
    ![Yeni MySQL veritabanı oluştur][new-mysql-db]
6. Merhaba web uygulaması oluşturduğunuzda hello yeni uygulama hizmeti dikey görürsünüz.
7. Tıklayın **ayarları** > **dağıtım kimlik bilgileri**. 
   
    ![Dağıtım kimlik bilgilerini ayarlama][set-deployment-credentials]
8. tooenable FTP Yayımlama, bir kullanıcı adı ve parola sağlamalısınız. Merhaba kimlik bilgileri kaydedin ve hello kullanıcı adı ve parola oluşturduğunuz not edin.
   
    ![Yayımlama kimlik bilgileri oluşturma][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>Derleme ve uygulamanızı yerel olarak test etme
Merhaba kayıt uygulama adı ve e-posta adresinizi sağlayarak bir olay için tooregister sağlayan basit bir PHP uygulamasıdır. Önceki şahıslar hakkında bilgi bir tabloda görüntülenir. Kayıt bilgileri bir MySQL veritabanında depolanır. Merhaba uygulama iki dosyadan oluşur:

* **PHP için index.php'dir**: kaydı ve registrant bilgi içeren bir tablo için bir form görüntüler.
* **CreateTable.php**: Merhaba uygulaması için hello MySQL tablosu oluşturur. Bu dosya yalnızca bir kez kullanılır.

toobuild ve yerel olarak çalıştırma hello uygulama hello adımları izleyin. PHP, MySQL ve yerel makinenizde ayarlanan bir web sunucusu varsa ve etkinleştirdiğinizden emin hello adımları varsayın Not [PDO uzantısı MySQL için][pdo-mysql].

1. Adlı bir MySQL veritabanı oluşturma `registration`. Bu komutla hello MySQL komut satırından bunu yapabilirsiniz:
   
        mysql> create database registration;
2. Web sunucunuzun kök dizininde adlı bir klasör oluşturun `registration` ve iki dosya içinde - adlı oluşturun `createtable.php` ve adlı `index.php`.
3. Açık hello `createtable.php` dosyasını bir metin düzenleyicisi veya IDE ve hello aşağıdaki kodu ekleyin. Bu kod kullanılan toocreate hello olacaktır `registration_tbl` hello tabloda `registration` veritabanı.
   
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
   > Tooupdate hello değerlerini gerekir <code>$user</code> ve <code>$pwd</code> yerel MySQL kullanıcı adı ve parola.
   > 
   > 
4. Bir web tarayıcısı açın ve çok Gözat[http://localhost/registration/createtable.php][localhost-createtable]. Bu hello oluşturacak `registration_tbl` hello veritabanındaki tablo.
5. Açık hello **php için index.php'dir** dosyasını bir metin düzenleyicisi veya IDE ve hello başlangıç sayfası için temel HTML ve CSS kodunu ekleyin (Merhaba PHP kodunun, sonraki adımlarda de eklenir).
   
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
6. Merhaba PHP etiketlere toohello veritabanına bağlanmak için PHP kodu ekleyin.
   
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
   > Yeniden tooupdate hello değerlerini gerekir <code>$user</code> ve <code>$pwd</code> yerel MySQL kullanıcı adı ve parola.
   > 
   > 
7. Merhaba veritabanı bağlantı kodu kayıt defteri bilgilerini hello veritabanına yerleştirilmesi için kodu ekleyin.
   
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
8. Son olarak, yukarıdaki hello kod hello veritabanından veri almak için kodu ekleyin.
   
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

Artık çok gözatabilirsiniz[http://localhost/registration/index.php] [ localhost-index] tootest hello uygulama.

## <a name="get-mysql-and-ftp-connection-information"></a>MySQL ve FTP bağlantı bilgileri alma
Web uygulamaları, profilinizde çalıştıran tooconnect toohello MySQL veritabanı bağlantı bilgilerini hello. tooget MySQL bağlantı bilgilerini, şu adımları izleyin:

1. Web uygulaması dikey Hello uygulama hizmetinden hello kaynak grubu bağlantıyı tıklatın:
   
    ![Kaynak Grup Seç][select-resourcegroup]
2. Kaynak grubundan hello veritabanı'nı tıklatın:
   
    ![Veritabanını seçin][select-database]
3. Özet Hello veritabanının seçileceği **ayarları** > **özellikleri**.
   
    ![Özellikleri seçme][select-properties]
4. Merhaba değerlerini Not `Database`, `Host`, `User Id`, ve `Password`.
   
    ![Not özellikleri][note-properties]
5. Web uygulamanızdan hello tıklatın **yayım profili indirin** hello hello sayfanın sağ alt köşesindeki bağlantıda:
   
    ![Yayım profili indirin][download-publish-profile]
6. Açık hello `.publishsettings` dosyasını bir XML düzenleyicisinde. 
7. Hello bulur `<publishProfile >` öğeyle `publishMethod="FTP"` benzer toothis arar:
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

Merhaba Not `publishUrl`, `userName`, ve `userPWD` öznitelikleri.

## <a name="publish-your-app"></a>Uygulamanızı yayımlama
Uygulamanızı yerel olarak test ettikten sonra FTP kullanarak tooyour web uygulaması yayımlayabilirsiniz. Ancak, ilk hello uygulamasında tooupdate hello veritabanı bağlantısı bilgilerini gerekir. Daha önce aldığınız hello veritabanı bağlantı bilgilerini kullanarak (Merhaba içinde **MySQL almak ve FTP bağlantı bilgileri** bölüm), bilgileri aşağıdaki güncelleştirme hello **her ikisi de** hello `createdatabase.php` ve `index.php` hello dosyalarıyla uygun değerler:

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

Artık toopublish FTP kullanarak uygulamanızı hazır.

1. Tercih, FTP İstemcisi'ni açın.
2. Merhaba girin *ana bilgisayar adı bölümü* hello gelen `publishUrl` ettiğiniz yukarıda FTP istemciniz özniteliği.
3. Merhaba girin `userName` ve `userPWD` yukarıda belirtilen öznitelikler, FTP istemcisi değişmeden.
4. Bağlantı kurun.

Bağlantıyı oluşturduktan sonra mümkün tooupload olması ve gerektiğinde dosyalarını indirin. Olan dosyaları toohello kök dizini yüklediğinizden emin olun `/site/wwwroot`.

Her ikisi de karşıya sonra `index.php` ve `createtable.php`, çok Gözat**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL tablo hello uygulama için sonra çok Gözat**http://[site adı ].azurewebsites.net/index.php** Merhaba uygulaması kullanarak toobegin.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: Merhaba [PHP Geliştirici Merkezi](/develop/php/).

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

