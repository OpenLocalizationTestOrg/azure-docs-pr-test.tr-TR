
1. tooescalate ayrıcalıklar, türü:
   
        sudo -s
   
    Parolanızı girin.
2. MySQL Community Server edition tooinstall yazın:
   
        zypper install mysql-community-server
   
    MySQL indirilir ve yüklenir bekleyin.
3. Merhaba sistem önyüklendiğinde tooset MySQL toostart, türü:
   
        insserv mysql
4. Merhaba MySQL arka plan programı (mysqld), bu komutla el ile başlatın:
   
        rcmysql start
   
    Merhaba MySQL arka plan programı, türü toocheck hello durumu:
   
        rcmysql status
   
    toostop hello MySQL arka plan programı, yazın:
   
        rcmysql stop
   
   > [!IMPORTANT]
   > Yükleme sonrasında, hello MySQL kök parola varsayılan olarak boştur. Çalıştırmanızı öneririz **mysql\_güvenli\_yükleme**, güvenli MySQL yardımcı olan bir komut dosyası. Hello betik toochange hello MySQL kök parola ister, anonim kullanıcı hesaplarını kaldırın, uzak kök oturum açmalar devre dışı bırakmak, test veritabanları kaldırın ve hello ayrıcalıkları tablo yeniden yükleyin. Bu seçeneklerin Evet tooall yanıtlayın ve hello kök parolasını değiştirme önerilir.
   > 
   > 
5. Bu toorun hello betiği MySQL yükleme komut dosyası yazın:
   
        mysql_secure_installation
6. İçinde tooMySQL oturum:
   
        mysql -u root -p
   
    (Hangi hello önceki adımda değiştirdiğiniz) hello MySQL kök parola girin ve bir istemiyle, sunulur burada hello veritabanıyla SQL deyimleri toointeract verebilir.
7. hello Hello aşağıdakini çalıştırın toocreate yeni bir MySQL kullanıcı **mysql >** istemi:
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Not, hello noktalı virgül (;) hello hello sonunda satırları hello komutları bitiş için önemli.
8. toocreate bir veritabanı ve grant hello `mysqluser` üzerindeki komutları aşağıdaki sorunu hello kullanıcının izinleri:
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Veritabanı kullanıcı adları ve parolalar toohello veritabanına bağlanma komut dosyaları tarafından yalnızca kullanıldığını unutmayın.  Veritabanı kullanıcı hesabı adları mutlaka hello sistem gerçek kullanıcı hesaplarında temsil etmiyor.
9. başka bir bilgisayardan türü toolog içinde:
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    Burada `ip-address` içinden, bağlanan tooMySQL hello bilgisayar hello IP adresidir.
10. MySQL veritabanı yönetim yardımcı programı, tooexit hello yazın:
    
        quit

## <a name="add-an-endpoint"></a>Bir uç nokta ekleme
1. MySQL yüklendikten sonra tooconfigure bir uç nokta tooaccess MySQL uzaktan gerekir. İçinde toohello oturum [Klasik Azure portalı][AzurePortal]. Tıklatın **sanal makineleri**, yeni bir sanal makine hello adına tıklayın ve ardından **uç noktaları**.
2. Tıklatın **Ekle** hello sayfanın hello sonundaki.
3. Protokolüyle "MySQL" adlı bir uç nokta ekleyin **TCP**, ve **ortak** ve **özel** bağlantı noktaları kümesi çok "3306".
4. tooremotely bilgisayarınızdan türü toohello sanal makineye bağlanın:
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    Örneğin, bu öğreticide oluşturduğumuz hello sanal makine kullanarak, bu komutu yazın:
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
