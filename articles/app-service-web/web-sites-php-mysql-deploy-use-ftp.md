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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>Azure App Service’ta bir PHP-MySQL web uygulaması oluşturma ve uygulamayı FTP kullanarak dağıtma
Bu öğretici, bir PHP MySQL web uygulamasının nasıl oluşturulacağını ve FTP kullanarak dağıtma gösterir. Bu öğretici, varsayar [PHP][install-php], [MySQL][install-mysql], bir web sunucusu ve bilgisayarınızda yüklü bir FTP istemcisi. Bu öğreticideki yönergeler işletim Windows, Mac ve Linux dahil olmak üzere tüm sisteminizde izlenebilir. Bu kılavuzu tamamladıktan sonra Azure'da çalışan bir PHP/MySQL web uygulaması gerekir.

Şunları öğreneceksiniz:

* Bir web uygulaması ve Azure Portalı'nı kullanarak bir MySQL veritabanı oluşturma PHP Web uygulamaları varsayılan olarak etkinleştirilmiş olduğundan, özel bir şey PHP kodunuzu çalıştırmak için gereklidir.
* FTP kullanarak Azure uygulamanızı yayımlamak nasıl.

Bu öğreticiyi izleyerek, PHP bir basit kayıt web uygulaması oluşturacaksınız. Uygulama bir Web uygulamasını barındırılan. Tamamlanmış uygulamanın bir ekran görüntüsü aşağıda verilmiştir:

![Azure PHP Web sitesi][running-app]

> [!NOTE]
> Bir hesabı için kaydolmadan önce Azure App Service'i kullanmaya başlamak istiyorsanız, Git [App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı veya taahhüt gerekmez. 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>Bir web uygulaması oluşturun ve FTP Yayımlama Ayarla
Bir web uygulaması ve bir MySQL veritabanı oluşturmak için aşağıdaki adımları izleyin:

1. Oturum açma [Azure Portal][management-portal].
2. Tıklatın **+ yeni** üst simgesine sol Azure Portal'ın.
   
    ![Yeni Azure Web sitesi oluştur][new-website]
3. Arama türündeki **Web uygulaması + MySQL** ve tıklayın **Web uygulaması + MySQL**.
   
    ![Yeni Web sitesi özel oluştur][custom-create]
4. **Oluştur**'a tıklayın. Benzersiz bir uygulama hizmeti adına, kaynak grubu ve yeni bir hizmet planı için geçerli bir ad girin.
   
    ![Küme kaynak grubu adı][resource-group]
5. Yasal koşulları kabul ettiğinizi belirten dahil olmak üzere, yeni bir veritabanı için değerler girin.
   
    ![Yeni MySQL veritabanı oluştur][new-mysql-db]
6. Web uygulaması oluşturduğunuzda, yeni uygulama hizmeti dikey penceresini görürsünüz.
7. Tıklayın **ayarları** > **dağıtım kimlik bilgileri**. 
   
    ![Dağıtım kimlik bilgilerini ayarlama][set-deployment-credentials]
8. FTP yayımlamayı etkinleştirmek için bir kullanıcı adı ve parolasını sağlamanız gerekir. Kimlik bilgileri kaydedin ve oluşturduğunuz parola ve kullanıcı adını not edin.
   
    ![Yayımlama kimlik bilgileri oluşturma][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>Derleme ve uygulamanızı yerel olarak test etme
Kayıt uygulama kaydetmek bir olay için ad ve e-posta adresinizi sağlayarak sağlayan basit bir PHP uygulamasıdır. Önceki şahıslar hakkında bilgi bir tabloda görüntülenir. Kayıt bilgileri bir MySQL veritabanında depolanır. Uygulama iki dosyadan oluşur:

* **PHP için index.php'dir**: kaydı ve registrant bilgi içeren bir tablo için bir form görüntüler.
* **CreateTable.php**: uygulama için MySQL tablosu oluşturur. Bu dosya yalnızca bir kez kullanılır.

Derleme ve uygulamayı yerel olarak çalıştırmak için aşağıdaki adımları izleyin. Bu adımları PHP, MySQL ve yerel makinenizde ayarlanan bir web sunucusu, olduğunu varsayın Not ve etkinleştirdiğiniz [PDO uzantısı MySQL için][pdo-mysql].

1. Adlı bir MySQL veritabanı oluşturma `registration`. Bu komutla MySQL komut isteminden bunu yapabilirsiniz:
   
        mysql> create database registration;
2. Web sunucunuzun kök dizininde adlı bir klasör oluşturun `registration` ve iki dosya içinde - adlı oluşturun `createtable.php` ve adlı `index.php`.
3. Açık `createtable.php` dosyasını bir metin düzenleyicisi veya IDE ve aşağıdaki kodu ekleyin. Bu kodu oluşturmak için kullanılan `registration_tbl` tablosundaki `registration` veritabanı.
   
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
   > Değerleri güncelleştirmeniz gerekecektir <code>$user</code> ve <code>$pwd</code> yerel MySQL kullanıcı adı ve parola.
   > 
   > 
4. Bir web tarayıcısı açın ve [http://localhost/registration/createtable.php][localhost-createtable]. Bu oluşturacak `registration_tbl` veritabanındaki tablo.
5. Açık **php için index.php'dir** dosyasını bir metin düzenleyicisi veya IDE ve (PHP kodunun, sonraki adımlarda de eklenir) sayfanın temel HTML ve CSS kodunu ekleyin.
   
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
6. PHP etiketleri içinde veritabanına bağlanmak için PHP kodu ekleyin.
   
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
   > Yeniden değerleri güncelleştirmeniz gerekecektir <code>$user</code> ve <code>$pwd</code> yerel MySQL kullanıcı adı ve parola.
   > 
   > 
7. Veritabanı bağlantı kodu kayıt defteri bilgilerini veritabanına eklemek için kodu ekleyin.
   
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
8. Son olarak, yukarıdaki kod veritabanından veri almak için kodu ekleyin.
   
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

Şimdi gözatabilirsiniz [http://localhost/registration/index.php] [ localhost-index] uygulamayı test etmek için.

## <a name="get-mysql-and-ftp-connection-information"></a>MySQL ve FTP bağlantı bilgileri alma
Web uygulamaları, profilinizde çalıştıran MySQL veritabanına bağlanmak için bağlantı bilgilerini gerekir. MySQL bağlantı bilgilerini almak için şu adımları izleyin:

1. Web uygulaması dikey uygulama hizmetinden kaynak grubu bağlantıyı tıklatın:
   
    ![Kaynak Grup Seç][select-resourcegroup]
2. Veritabanını, kaynak grubundan tıklatın:
   
    ![Veritabanını seçin][select-database]
3. Özet veritabanından seçin **ayarları** > **özellikleri**.
   
    ![Özellikleri seçme][select-properties]
4. Değerlerini Not `Database`, `Host`, `User Id`, ve `Password`.
   
    ![Not özellikleri][note-properties]
5. Web uygulamanızdan tıklatın **yayım profili indirin** sayfanın sağ alt köşesindeki bağlantıda:
   
    ![Yayım profili indirin][download-publish-profile]
6. Açık `.publishsettings` dosyasını bir XML düzenleyicisinde. 
7. Bul `<publishProfile >` öğeyle `publishMethod="FTP"` , aşağıdakine benzer görünür:
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

Not `publishUrl`, `userName`, ve `userPWD` öznitelikleri.

## <a name="publish-your-app"></a>Uygulamanızı yayımlama
Uygulamanızı yerel olarak test ettikten sonra web uygulamanıza FTP kullanarak yayımlayabilirsiniz. Ancak, ilk uygulamasında veritabanı bağlantısı bilgilerini güncelleştirmek gerekir. Daha önce aldığınız veritabanı bağlantı bilgilerini kullanarak (içinde **MySQL almak ve FTP bağlantı bilgileri** bölüm), aşağıdaki bilgileri güncelleştirin **her ikisi de** `createdatabase.php` ve `index.php` uygun değerlerle dosyaları:

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

Şimdi FTP kullanarak uygulamanızı yayımlamak hazırsınız.

1. Tercih, FTP İstemcisi'ni açın.
2. Girin *ana bilgisayar adı bölümü* gelen `publishUrl` ettiğiniz yukarıda FTP istemciniz özniteliği.
3. Girin `userName` ve `userPWD` yukarıda belirtilen öznitelikler, FTP istemcisi değişmeden.
4. Bağlantı kurun.

Bağlantıyı oluşturduktan sonra karşıya yükleme ve gerektiğinde dosyaları indirme mümkün olacaktır. Olduğu kök dizinine dosyaları karşıya mutlaka `/site/wwwroot`.

Her ikisi de karşıya sonra `index.php` ve `createtable.php`, Gözat **http://[site name].azurewebsites.net/createtable.php** uygulama için MySQL tablo oluşturmak için göz **http://[site adı]. azurewebsites.NET/index.php** uygulamayı kullanmaya başlamak için.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: [PHP Geliştirici Merkezi](/develop/php/).

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

