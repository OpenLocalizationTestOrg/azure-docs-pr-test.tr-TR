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
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a>Bir PHP SQL web uygulaması oluşturma ve tooAzure uygulama hizmeti dağıtma Git kullanma
Bu öğretici nasıl toocreate bir PHP web uygulamasında gösterir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) tooAzure SQL veritabanına bağlanan ve nasıl toodeploy Git kullanarak. Bu öğretici, varsayar [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [SQL Server için PHP için Microsoft Drivers ](http://www.microsoft.com/download/en/details.aspx?id=20098), ve [Git] [ install-git] bilgisayarınızda yüklü. Bu kılavuzu tamamladıktan sonra Azure'da çalışan bir PHP SQL web uygulaması gerekir.

> [!NOTE]
> Yükleme ve PHP, SQL Server Express ve hello Microsoft Drivers hello kullanarak PHP için SQL Server için Yapılandır [Microsoft Web Platformu yükleyicisi](http://www.microsoft.com/web/downloads/platform.aspx).
> 
> 

Şunları öğreneceksiniz:

* Nasıl toocreate bir Azure web app ve hello kullanarak bir SQL veritabanı [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). PHP App Service Web Apps içinde varsayılan olarak etkindir, özel bir şey gerekli toorun çünkü PHP kodunuzu.
* Nasıl toopublish ve Git kullanarak, uygulama tooAzure yeniden yayımlayın.

Bu öğreticiyi izleyerek, PHP bir basit kayıt web uygulaması oluşturacaksınız. Merhaba uygulaması bir Azure Web Sitesi'nde barındırılan. Tamamlanan hello uygulamasının ekran görüntüsü aşağıda verilmiştir:

![Azure PHP Web sitesi](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a>Bir Azure web uygulaması oluşturma ve Git yayımlama Ayarla
Bu adımları toocreate Azure web uygulaması ve SQL veritabanı izleyin:

1. İçinde toohello oturum [Azure Portal](https://portal.azure.com/).
2. Merhaba tıklatarak açık hello Azure Marketi **yeni** hello üst simgesine sol hello panosunu, tıklayın **Tümünü Seç** sonraki tooMarketplace ve seçerek **Web + mobil**.
3. Hello Market, seçin **Web + mobil**.
4. Merhaba tıklatın **Web uygulaması + SQL** simgesi.
5. Hello Web uygulaması + SQL uygulama Hello açıklamasını okuduktan sonra Seç **oluşturma**.
6. Her bölüm üzerinde'i tıklatın (**kaynak grubu**, **Web uygulaması**, **veritabanı**, ve **abonelik**) girin ve gerekli hello için değerleri seçin alanlar:
   
   * Tercih ettiğiniz bir URL adı girin    
   * Veritabanı sunucusu kimlik bilgilerini yapılandırın
   * Merhaba bölgeye en yakın tooyou seçin
     
     ![uygulamanızı yapılandırma](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. Merhaba web uygulaması tanımlama bittiğinde tıklatın **oluşturma**.
   
    Merhaba web uygulaması oluşturduğunuzda hello **bildirimleri** düğmesi yeşil flash **başarı** ve kaynak grubu dikey penceresi açık tooshow hem hello web app ve hello SQL veritabanında hello Grup hello.
8. Merhaba kaynak grubu dikey tooopen hello web uygulamanızın dikey penceresinde Hello web uygulamanızın simgesine tıklayın.
   
    ![web uygulamanızın kaynak grubu](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. İçinde **ayarları** tıklatın **sürekli dağıtım** > **gerekli ayarları Yapılandır**. Seçin **yerel Git deposu** tıklatıp **Tamam**.
   
    ![kaynak kodunuz nerede](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    Önce bir Git deposu ayarlama ayarlamadıysanız, bir kullanıcı adı ve parolasını sağlamanız gerekir. toodo bunu, **ayarları** > **dağıtım kimlik bilgileri** hello web uygulamanızın dikey penceresinde.
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. İçinde **ayarları** tıklayın **özellikleri** toosee hello Git uzak URL ihtiyacınız toouse toodeploy PHP uygulamanızı daha sonra.

## <a name="get-sql-database-connection-information"></a>SQL veritabanı bağlantı bilgilerini alma
bağlı olan tooconnect toohello SQL veritabanı örneği tooyour web uygulaması, profilinizde hello veritabanı oluşturduğunuzda belirttiğiniz bağlantı bilgilerini hello. tooget hello SQL veritabanı bağlantı bilgilerini, şu adımları izleyin:

1. Geri hello kaynak grubu dikey penceresinde hello SQL Database'in simgesine tıklayın.
2. Merhaba SQL Database'in dikey penceresinde tıklayın **ayarları** > **özellikleri**, ardından **veritabanı bağlantı dizelerini Göster**. 
   
    ![Veritabanı özellikleri görüntüle](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. Merhaba gelen **PHP** bölüm hello ortaya çıkan iletişim, hello değerlerini Not `Server`, `SQL Database`, ve `User Name`. Daha sonra PHP web uygulaması tooAzure uygulama hizmeti zaman yayımlama bu değerleri kullanır.

## <a name="build-and-test-your-application-locally"></a>Uygulamanızı yerel olarak oluşturma ve test etme
Merhaba kayıt uygulama adı ve e-posta adresinizi sağlayarak bir olay için tooregister sağlayan basit bir PHP uygulamasıdır. Önceki şahıslar hakkında bilgi bir tabloda görüntülenir. Kayıt defteri bilgilerini bir SQL veritabanı örneğinde depolanır. Merhaba uygulaması iki dosyaları (kopyala/yapıştır kodu aşağıda kullanılabilir) oluşur:

* **PHP için index.php'dir**: kaydı ve registrant bilgi içeren bir tablo için bir form görüntüler.
* **CreateTable.php**: Merhaba uygulaması için hello SQL veritabanı tablosu oluşturur. Bu dosya yalnızca bir kez kullanılır.

yerel olarak toorun Merhaba uygulaması hello adımları izleyin. PHP sahip ve SQL Server Express ayarlanan yerel makinenizde ve etkinleştirdiğinizden emin hello adımları varsayılır Not [PDO uzantısı için SQL Server][pdo-sqlsrv].

1. Adlı bir SQL Server veritabanı oluşturma `registration`. Hello bunu yapabilirsiniz `sqlcmd` komut istemi Bu komutlar:
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. Uygulama kök dizininde iki dosya - adlı oluşturma `createtable.php` ve adlı `index.php`.
3. Açık hello `createtable.php` dosyasını bir metin düzenleyicisi veya IDE ve hello aşağıdaki kodu ekleyin. Bu kod kullanılan toocreate hello olacaktır `registration_tbl` hello tabloda `registration` veritabanı.
   
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
   
    Tooupdate hello değerlerini gerektiğine dikkat edin <code>$user</code> ve <code>$pwd</code> yerel SQL Server kullanıcı adı ve parola.
4. Merhaba kök dizininde komutu aşağıdaki hello uygulama türü Merhaba, bir terminal içinde:
   
        php -S localhost:8000
5. Bir web tarayıcısı açın ve çok Gözat**http://localhost:8000/createtable.php**. Bu hello oluşturacak `registration_tbl` hello veritabanındaki tablo.
6. Açık hello **php için index.php'dir** dosyasını bir metin düzenleyicisi veya IDE ve hello başlangıç sayfası için temel HTML ve CSS kodunu ekleyin (Merhaba PHP kodunun, sonraki adımlarda de eklenir).
   
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
7. Merhaba PHP etiketlere toohello veritabanına bağlanmak için PHP kodu ekleyin.
   
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
   
    Yeniden tooupdate hello değerlerini gerekir <code>$user</code> ve <code>$pwd</code> yerel MySQL kullanıcı adı ve parola.
8. Merhaba veritabanı bağlantı kodu kayıt defteri bilgilerini hello veritabanına yerleştirilmesi için kodu ekleyin.
   
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
9. Son olarak, yukarıdaki hello kod hello veritabanından veri almak için kodu ekleyin.
   
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

Artık çok gözatabilirsiniz**http://localhost:8000/index.php** tootest Merhaba uygulaması.

## <a name="publish-your-application"></a>Uygulamanızı yayımlama
Uygulamanızı yerel olarak test ettikten sonra tooApp Service Web Apps Git kullanarak yayımlayabilirsiniz. Ancak, ilk hello uygulamasında tooupdate hello veritabanı bağlantısı bilgilerini gerekir. Daha önce aldığınız hello veritabanı bağlantı bilgilerini kullanarak (Merhaba içinde **alma SQL veritabanı bağlantı bilgilerini** bölüm), bilgileri aşağıdaki güncelleştirme hello **her ikisi de** hello `createdatabase.php` ve `index.php` hello dosyalarıyla uygun değerler:

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> Merhaba, <code>$host</code>, sunucu hello değerini $a, ile <code>tcp:</code>.
> 
> 

Şimdi, Git yayımlamayı hazır tooset olan ve hello uygulamayı yayımlayın.

> [!NOTE]
> Merhaba aynı adımları not ettiğiniz hello hello sonunda bunlar **Azure web uygulaması oluşturun ve Git yayımlamayı ayarlayın** yukarıdaki bölümde.
> 
> 

1. Bash'i açın (veya Git ise bir terminal, `PATH`), uygulamanızın dizinleri toohello kök dizini değiştirin (Merhaba **kayıt** dizin), ve çalışma hello aşağıdaki komutlar:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Daha önce oluşturduğunuz hello parola istenir.
2. Çok Gözat**http://[web uygulama name].azurewebsites.net/createtable.php** toocreate hello SQL veritabanı tablosunda Merhaba uygulaması için.
3. Çok Gözat**http://[web uygulama name].azurewebsites.net/index.php** Merhaba uygulaması kullanarak toobegin.

Uygulamanızı yayımladıktan sonra değişiklikler tooit yapmaya başlamak ve Git toopublish kullanmanızı bunları. 

## <a name="publish-changes-tooyour-application"></a>Değişiklikleri tooyour uygulama yayımlama
toopublish değişiklikleri tooapplication, şu adımları izleyin:

1. Değişiklik tooyour uygulamayı yerel olarak belirler.
2. Bash'i açın (ya da bir terminal Git olan BT, `PATH`), uygulamanızın dizinleri toohello kök dizini değiştirin ve hello aşağıdaki komutları çalıştırın:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Daha önce oluşturduğunuz hello parola istenir.
3. Çok Gözat**http://[web uygulama name].azurewebsites.net/index.php** toosee değişikliklerinizi.

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

