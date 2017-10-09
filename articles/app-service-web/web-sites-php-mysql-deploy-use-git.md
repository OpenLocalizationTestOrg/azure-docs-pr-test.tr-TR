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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a>Azure App Service’ta bir PHP-MySQL web uygulaması oluşturma ve uygulamayı Git kullanarak dağıtma
Bu öğretici, toocreate PHP MySQL web nasıl uygulama ve nasıl gösterir toodeploy, çok[uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) Git kullanarak. Kullanacağınız [PHP][install-php], MySQL komut satırı aracı hello (parçası [MySQL][install-mysql]), ve [Git] [ install-git] bilgisayarınızda yüklü. Bu öğreticideki yönergeler Hello işletim Windows, Mac ve Linux dahil olmak üzere tüm sisteminizde izlenebilir. Bu kılavuzu tamamladıktan sonra Azure'da çalışan bir PHP/MySQL web uygulaması gerekir.

Şunları öğreneceksiniz:

* Nasıl hello kullanarak toocreate bir web uygulaması ve bir MySQL veritabanı [Azure Portal][management-portal]. PHP etkin olduğundan [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) varsayılan olarak, özel bir şey gerekli toorun olan PHP kodunuzu.
* Nasıl toopublish ve Git kullanarak, uygulama tooAzure yeniden yayımlayın.
* Nasıl adresindeki tooenable hello Composer uzantısını tooautomate Oluşturucu görevleri her `git push`.

Bu öğreticiyi izleyerek, PHP bir basit kayıt web uygulaması oluşturacaksınız. Merhaba uygulaması, Web uygulamalarında barındırılan. Tamamlanan hello uygulamasının ekran görüntüsü aşağıda verilmiştir:

![Azure PHP web sitesi][running-app]

## <a name="set-up-hello-development-environment"></a>Merhaba geliştirme ortamını ayarlama
Bu öğretici, varsayar [PHP][install-php], MySQL komut satırı aracı hello (parçası [MySQL][install-mysql]), ve [Git] [ install-git] bilgisayarınızda yüklü.

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a>Bir web uygulaması oluşturma ve Git yayımlama Ayarla
Bu adımları toocreate bir web uygulaması ve bir MySQL veritabanı izleyin:

1. Oturum açma toohello [Azure Portal][management-portal].
2. Merhaba tıklatın **yeni** simgesi.
3. Tıklatın **bkz tüm** sonraki çok**Market**. 
4. Tıklatın **Web + mobil**, ardından **Web uygulaması + MySQL**. Sonra, **Oluştur**’a tıklayın.
5. Kaynak grubunuz için geçerli bir ad girin.
   
    ![Küme kaynak grubu adı][resource-group]
6. Yeni web uygulamanız için değerler girin.
   
    ![Web uygulaması oluşturma][new-web-app]
7. Kabul ettiğinizi belirten dahil olmak üzere yeni veritabanınız için değerleri girin toohello yasal koşulları.
   
    ![Yeni MySQL veritabanı oluştur][new-mysql-db]
8. Merhaba web uygulaması oluşturduğunuzda hello yeni web uygulaması dikey görürsünüz.
9. İçinde **ayarları** tıklayın **sürekli dağıtım**, tıklayın *gerekli ayarları Yapılandır*.
   
    ![Git yayımlama Ayarla][setup-publishing]
10. Seçin **yerel Git deposu** hello kaynağı için.
    
     ![Git deposu ayarlama][setup-repository]
11. tooenable yayımlama Git, kullanıcı adı ve parola sağlamalısınız. Merhaba kullanıcı adı ve parola oluşturduğunuz not edin. (Önce bir Git deposu ayarladıysanız, bu adım atlanır.)
    
     ![Yayımlama kimlik bilgileri oluşturma][credentials]

## <a name="get-remote-mysql-connection-information"></a>Uzak MySQL bağlantı bilgilerini alma
Web uygulamaları, profilinizde çalıştıran tooconnect toohello MySQL veritabanı bağlantı bilgilerini hello. tooget MySQL bağlantı bilgilerini, şu adımları izleyin:

1. Kaynak grubundan hello veritabanı'nı tıklatın:
   
    ![Veritabanını seçin][select-database]
2. Merhaba veritabanından **ayarları**seçin **özellikleri**.
   
    ![Özellikleri seçme][select-properties]
3. Merhaba değerlerini Not `Database`, `Host`, `User Id`, ve `Password`.
   
    ![Not özellikleri][note-properties]

## <a name="build-and-test-your-app-locally"></a>Derleme ve uygulamanızı yerel olarak test etme
Bir web uygulaması oluşturduğunuza göre uygulamanızı yerel olarak geliştirme ve ardından test sonra dağıtın.

Merhaba kayıt uygulama adı ve e-posta adresinizi sağlayarak bir olay için tooregister sağlayan basit bir PHP uygulamasıdır. Önceki şahıslar hakkında bilgi bir tabloda görüntülenir. Kayıt bilgileri bir MySQL veritabanında depolanır. Merhaba uygulama bir dosya (kopyala/yapıştır kodu aşağıda kullanılabilir) oluşur:

* **PHP için index.php'dir**: kaydı ve registrant bilgi içeren bir tablo için bir form görüntüler.

toobuild ve yerel olarak çalıştırma Merhaba uygulaması hello adımları izleyin. Bu adımları hello PHP ve MySQL komut satırı aracı (MySQL parçası) yerel makinenizde ayarlanmış olması ve hello etkinleştirdiğiniz varsayılır unutmayın [PDO uzantısı MySQL için][pdo-mysql].

1. Merhaba değerini kullanarak toohello uzak MySQL, sunucuya `Data Source`, `User Id`, `Password`, ve `Database` daha önce aldığınız:
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. Merhaba MySQL komut istemi görünür:
   
        mysql>
3. Merhaba aşağıdaki Yapıştır `CREATE TABLE` komutu toocreate hello `registration_tbl` veritabanınızı tabloda:
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. Yerel uygulama klasörüne Hello kök dizininde oluşturmak **php için index.php'dir** dosya.
5. Açık hello **php için index.php'dir** dosyasını bir metin düzenleyicisi veya IDE ve koddan hello ve tam hello gerekli değişiklikleri işaretlenmiş ekleyin `//TODO:` açıklamaları.

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

1. Aşağıdaki komutu bir terminal gidin tooyour uygulama klasörü ve türü hello:
   
       php -S localhost:8000

Artık çok gözatabilirsiniz**8000 /** tootest Merhaba uygulaması.

## <a name="publish-your-app"></a>Uygulamanızı yayımlama
Uygulamanızı yerel olarak test ettikten sonra Git kullanarak tooWeb uygulamaları yayımlayabilirsiniz. Yerel Git deponuzu başlatmak ve yayımlama hello uygulama.

> [!NOTE]
> Bunlar olan hello aynı hello Azure Portalı'hello sonunda hello bir web uygulaması oluşturma ve ayarlama Git yayımlama bölümüne yukarıdaki yukarı gösterilen adımları.
> 
> 

1. (İsteğe bağlı)  Unutulan veya Git uzak repostitory URL'nizi yanlış toohello web uygulama özellikleri hello Azure Portal gidin.
2. Bash'i açın (ya da bir terminal Git ise, `PATH`), uygulamanızın dizinleri toohello kök dizini değiştirin ve hello aşağıdaki komutları çalıştırın:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Daha önce oluşturduğunuz hello parola istenir.
   
    ![İlk anında iletme tooAzure Git aracılığıyla][git-initial-push]
3. Çok Gözat**http://[site name].azurewebsites.net/index.php** toobegin (Bu bilgiler, hesap Panonuzda de depolanacağı) hello uygulamasını kullanarak:
   
    ![Azure PHP web sitesi][running-app]

Uygulamanızı yayımladıktan sonra değişiklikler tooit yapmaya başlamak ve Git toopublish kullanmanızı bunları.

## <a name="publish-changes-tooyour-app"></a>Değişiklikleri tooyour uygulama yayımlama
toopublish değişiklikleri tooyour uygulama, şu adımları izleyin:

1. Değişiklikleri tooyour uygulamasını yerel olarak olun.
2. Bash'i açın (ya da bir terminal Git olan BT, `PATH`), uygulamanızın dizinleri toohello kök dizini değiştirin ve hello aşağıdaki komutları çalıştırın:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Daha önce oluşturduğunuz hello parola istenir.
   
    ![Site Ftp'den Git aracılığıyla tooAzure değiştirir][git-change-push]
3. Çok Gözat**http://[site name].azurewebsites.net/index.php** toosee uygulamanızı ve yapılan değişiklikler:
   
    ![Azure PHP web sitesi][running-app]

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a>Oluşturucu otomasyon ile Merhaba Composer uzantısını etkinleştirme
PHP projeniz varsa varsayılan olarak, App Service'te hello git dağıtım işlemi ile composer.json, hiçbir şey yapmaz. İşleme sırasında composer.json etkinleştirebilirsiniz `git push` hello Composer uzantısını etkinleştirerek.

1. PHP ile web uygulamanızın dikey penceresinde hello [Azure portal][management-portal], tıklatın **Araçları** > **uzantıları**.
   
    ![Oluşturucu uzantı ayarları][composer-extension-settings]
2. Tıklatın **Ekle**, ardından **Oluşturucu**.
   
    ![Composer uzantısını Ekle][composer-extension-add]
3. Tıklatın **Tamam** tooaccept yasal koşulları. Tıklatın **Tamam** yeniden tooadd hello uzantısı.
   
    Merhaba **yüklü uzantıları** dikey şimdi hello Composer uzantısını göster.  
    ![Composer uzantısını görünümü][composer-extension-view]
4. Şimdi, gerçekleştirmek `git add`, `git commit`, ve `git push` hello önceki bölümde ister. Oluşturucu composer.json içinde tanımlanan bağımlılıklar yüklüyor şimdi görürsünüz.
   
    ![Composer uzantısını başarılı][composer-extension-success]

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: Merhaba [PHP Geliştirici Merkezi](/develop/php/).

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
