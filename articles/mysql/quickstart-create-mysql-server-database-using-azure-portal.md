---
title: "Hızlı Başlangıç: MySQL için Azure Veritabanı sunucusu Oluşturma - Azure portalı | Microsoft Docs"
description: "Bu makale adımları kullanarak size Azure portal tooquickly hello yaklaşık beş dakika içinde MySQL sunucusu için bir örnek Azure veritabanı oluşturun."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 08/15/2017
ms.openlocfilehash: d5754fe7a6f0f0f4b3fa19d456c4e15e64ca396c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-portal"></a>Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma
Azure veritabanı için MySQL toorun sağlayan yönetilen bir hizmettir, yönetmek ve yüksek oranda kullanılabilir MySQL veritabanları hello bulutta ölçeklendirin. Bu hızlı başlangıç toocreate Azure nasıl veritabanı için MySQL sunucusu yaklaşık beş dakika içinde hello Azure portal kullanarak gösterir. 

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum
Web tarayıcınızı açın ve toohello gidin [Microsoft Azure portal](https://portal.azure.com/). Kimlik bilgileri toosign toohello Portalı'nda girin. Hizmet panonuz Hello varsayılan görünümüdür.

## <a name="create-azure-database-for-mysql-server"></a>MySQL için Azure Veritabanı sunucusu oluşturma
MySQL için Azure Veritabanı sunucusu, tanımlı bir dizi [işlem ve depolama kaynağı](./concepts-compute-unit-and-storage.md) ile oluşturulur. Merhaba server içinde oluşturulur bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md).

Bu adımları toocreate MySQL sunucusu için bir Azure veritabanı izleyin:

1. Merhaba tıklatın **yeni** hello sol üst köşesinin hello Azure portalı üzerinde bulunan düğmesini (+).

2. Seçin **veritabanları** hello gelen **yeni** sayfasında ve seçin **Azure veritabanı için MySQL** hello gelen **veritabanları** sayfası. Ayrıca yazabilirsiniz **MySQL** hello yeni sayfa arama kutusu toofind hello hizmetinin içinde.
![Azure portalı - yeni - veritabanı - MySQL](./media/quickstart-create-mysql-server-database-using-azure-portal/2_navigate-to-mysql.png)

3. Yeni Sunucu ayrıntıları form Hello görüntü önceki hello üzerinde gösterildiği gibi bilgileri, aşağıdaki hello ile doldurmak:

    **Ayar** | **Önerilen değer** | **Alan Açıklaması** 
    ---|---|---
    Sunucu adı | myserver4demo | Azure veritabanınızı MySQL sunucusuna tanıtan benzersiz bir ad seçin. Merhaba etki alanı adı *mysql.database.azure.com* eklenmiş toohello sunucu adı için uygulamalar tooconnect sağlar. Merhaba sunucu adı yalnızca küçük harf, sayı ve hello tire (-) karakterini içerebilir ve 3-63 karakter içermelidir.
    Abonelik | Aboneliğiniz | Merhaba toouse sunucunuz için istediğiniz Azure aboneliği. Birden çok aboneliğiniz varsa, hangi hello kaynak için faturalandırılır hello uygun abonelik seçin.
    Kaynak grubu | myresourcegroup | Yeni bir kaynak grubu adı oluşturabilir veya mevcut bir aboneliğinizi kullanabilirsiniz.
    Sunucu yöneticisi oturum açma | myadmin | Kendi oturum açma hesabı toouse toohello sunucusu bağlanırken olun. Hello Yöneticisi oturum açma adı, 'azure_superuser', 'admin', 'Yönetici', 'root', 'Konuk' veya 'genel' olamaz.
    Parola | *Tercih ettiğiniz* | Merhaba server yönetici hesabı için yeni bir parola oluşturun. 8 too128 karakterler içermelidir. Parolanız kategorileri aşağıdaki hello üçünden karakterler içermelidir – İngilizce büyük harfler, küçük harfler, sayılar (0-9) ve alfasayısal olmayan karakterler (!, $, #, %, vs.).
    Parolayı onayla | *Tercih ettiğiniz*| Merhaba yönetici hesabı parolasını onaylayın.
    Konum | *Merhaba bölgeye en yakın tooyour kullanıcılar*| En yakın tooyour kullanıcılar ya da diğer Azure uygulamalarını hello konumu seçin.
    Sürüm | *Merhaba en son sürümünü seçin*| Belirli gereksinimlere sahip sürece hello en son sürümünü seçin.
    Fiyatlandırma Katmanı | **Temel**, **50 İşlem Birimi** **50 GB** | Tıklatın **fiyatlandırma katmanı** toospecify hello hizmeti katmanını ve performans düzeyini yeni veritabanı. Seçin **temel katmana** hello sekmesinde hello üstünde. Merhaba Hello solundaki tıklatın **işlem birimleri** kaydırıcı tooadjust hello değeri toohello az tutar kullanılabilir Bu Hızlı Başlangıç için. Tıklatın **Tamam** toosave hello fiyatlandırma katmanı seçimi. Aşağıdaki ekran görüntüsü hello bakın.
    PIN toodashboard | İşaretli | Merhaba denetleyin **PIN toodashboard** seçeneği tooallow kolay izleme sunucunuzun hello ön panosu sayfasında Azure portalı.

    > [!IMPORTANT]
    > Merhaba Sunucu Yöneticisi oturum açma ve burada belirttiğiniz parola toohello Server'daki gerekli toolog ve veritabanlarını Bu hızlı başlangıç devamındaki kümesidir. Bu bilgileri daha sonra kullanmak üzere aklınızda tutun veya kaydedin.
    > 

    ![Azure portal - gerekli hello form girişi sağlayarak MySQL oluşturma](./media/quickstart-create-mysql-server-database-using-azure-portal/3_create-server.png)

4.  Tıklatın **oluşturma** tooprovision hello sunucu. Sağlama too20 dakika yukarı birkaç dakika en fazla sürer.
   
5.  Merhaba araç çubuğundan, **bildirimleri** (zil simgesine) toomonitor hello dağıtım işlemi.

## <a name="configure-a-server-level-firewall-rule"></a>Sunucu düzeyinde güvenlik duvarı kuralı oluşturma

MySQL hizmeti için Azure veritabanı Hello hello sunucu düzeyinde güvenlik duvarı oluşturur. Bu Güvenlik Duvarı'nı bir güvenlik duvarı kuralı tooopen hello Güvenlik Duvarı'nı belirli IP adresleri için yapılandırılmadığı sürece dış uygulamaları ve Araçları'nın toohello sunucusu ve hello sunucudaki tüm veritabanları bağlanmasını önler. 

1.  Merhaba dağıtım tamamlandıktan sonra sunucunuzun bulun. Gerekirse arama yapabilirsiniz. Örneğin, **tüm kaynakları** hello sol menüsünden ve hello sunucu adı yazın (Merhaba örneği gibi *myserver4demo*) toosearch yeni oluşturulan sunucunuz için. Merhaba arama sonucunda listelenen sunucunuzun adını tıklatın. Merhaba **genel bakış** sayfası sunucunuz açar ve ek yapılandırma seçeneklerini sağlar.

2. Merhaba sunucu sayfasında seçin **bağlantı güvenliği**.

3.  Merhaba altında **güvenlik duvarı kuralları** hello hello boş bir metin kutusunda başlığını tıklatın **kural adı** sütun toobegin hello güvenlik duvarı kuralı oluşturma. 

    Bu Hızlı Başlangıç için şimdi tüm IP adresleri hello Server'a hello metin kutusunda her sütun değerleri aşağıdaki hello ile doldurarak izin ver:

    Kural Adı | Başlangıç IP’si | Bitiş IP’si 
    ---|---|---
    AllowAllIps |  0.0.0.0 | 255.255.255.255

4. Merhaba, hello üst araç çubuğunda **bağlantı güvenliği** sayfasında, **kaydetmek**. Birkaç dakika sonra ve bağlantı güvenliği güncelleştirme başarıyla devam etmeden önce tamamlandığını gösteren bildirim hello bildirim bekleyin.

    > [!NOTE]
    > MySQL veritabanı bağlantılarını tooAzure 3306 bağlantı noktası üzerinden iletişim kurar. Bir şirket ağından gelen tooconnect çalışıyorsanız, bağlantı noktası 3306 üzerinden giden trafik, ağınızın güvenlik duvarı tarafından izin verilmiyor. BT departmanınız 3306 bir bağlantı noktası açar sürece bu durumda, mümkün tooconnect tooyour sunucu olmaz.
    > 

## <a name="get-hello-connection-information"></a>Merhaba bağlantı bilgilerini alma
tooconnect tooyour veritabanı sunucusu, tooremember hello tam sunucu adı ve yönetici oturum açma kimlik bilgileri gerekir. Bu değerleri hello hızlı başlangıç makaledeki daha önce not ettiğiniz. Yaptığınız olmayan olasılığına hello sunucu adını ve oturum açma bilgilerini hello sunucusundan kolayca bulabilirsiniz **genel bakış** sayfa veya hello **özellikleri** hello Azure portal sayfasında.

1. Sunucunuzun **Genel Bakış** sayfasını açın. Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**. 
    İmleç her bir alan getirin ve toohello sağ hello metnin hello Kopyala simgesi görünür. Gerekli toocopy hello değerleri olarak Hello Kopyala simgesine tıklayın.

    Bu örnekte, hello sunucu adıdır *myserver4demo.mysql.database.azure.com*, ve hello Sunucu Yöneticisi oturum açma  *myadmin@myserver4demo* .

## <a name="connect-toomysql-using-mysql-command-line-tool"></a>MySQL komut satırı aracını kullanarak tooMySQL Bağlan
Bazı uygulamaları tooconnect tooyour Azure veritabanı MySQL sunucusu için kullanabilirsiniz. İlk hello kullanalım [mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) komut satırı tooillustrate nasıl aracı tooconnect toohello sunucu.  Bir web tarayıcısı kullanabilirsiniz ve hello Azure bulut hello burada açıklandığı gibi Kabuk ek yazılım tooinstall gerekir. Merhaba mysql yardımcı programını yerel olarak kendi makinede yüklü varsa, buradan da bağlanabilirsiniz.

1. Hello terminal simgesi aracılığıyla Hello Azure bulut Kabuğu'nu başlatın (> _) hello üzerinde hello Azure portal web sayfasının sağ üst.

2. Hello Azure bulut Kabuk tootype bash Kabuk komutları etkinleştirme tarayıcınızda açar.

    ![Komut istemi - mysql komut satırı örneği](./media/quickstart-create-mysql-server-database-using-azure-portal/7_connect-to-server.png)

3. Merhaba bulut Kabuk isteminde hello yeşil isteminde hello mysql komut satırı yazarak tooyour Azure veritabanı MySQL sunucusu için bağlayın.

    Biçim aşağıdaki hello hello mysql yardımcı programı ile MySQL sunucusu için kullanılan tooconnect tooan Azure veritabanı şöyledir:
    ```bash
    mysql --host <yourserver> --user <server admin login> --password
    ```

    Örneğin, komutu aşağıdaki hello tooour örnek sunucu bağlanır:
    ```azurecli-interactive
    mysql --host myserver4demo.mysql.database.azure.com --user myadmin@myserver4demo --password
    ```

    mysql parametresi |Önerilen değer|Açıklama
    ---|---|---
    --host | *sunucu adı* | Hello Azure veritabanı için MySQL daha önce oluşturduğunuz zaman, kullanılan hello sunucu adı değeri belirtin. Gösterilen örnek sunucumuz: myserver4demo.mysql.database.azure.com. Merhaba tam etki alanı adını kullan (\*. mysql.database.azure.com) hello örnekte gösterildiği gibi. Sunucu adınız anımsamıyorsanız hello önceki bölümde tooget hello bağlantı bilgilerini hello adımları izleyin. 
    --kullanıcı | *sunucu yöneticisi oturum açma adı* |İçinde hello sunucu yönetici oturum açma kullanıcı hello Azure veritabanı için MySQL daha önce oluşturduğunuz zaman sağlanan yazın. Merhaba kullanıcıadı anımsamıyorsanız hello önceki bölümde tooget hello bağlantı bilgilerini hello adımları izleyin.  Merhaba biçimi  *username@servername* .
    --parola | *istenene kadar bekleyin* | İstenir çok "Parola gir" çalıştırdıktan sonra hello komutu girin. İstendiğinde, hello aynı tür hello sunucu oluştururken sağladığınız parolayı.  Not hello yazdığınız karakterler hello bash üzerinde komut istemi gösterilmez parola belirtilmiş. Tüm hello karakter tooauthenticate yazmış bağlanmak sonra enter tuşuna basın.

   Bağlantı kurulduktan sonra hello mysql yardımcı programı görüntüler bir `mysql>` , tootype komutları sor. 

    Örnek mysql çıktısı:
    ```bash
    Welcome toohello MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 65505
    Server version: 5.6.26.0 MySQL Community Server (GPL)
    
    Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.
    
    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.
    
    mysql>
    ```
    > [!TIP]
    > Merhaba güvenlik duvarı değilse hello aşağıdaki hata oluşuyor tooallow hello IP adresini hello Azure bulut Kabuk yapılandırılmış:
    >
    > HATA 2003 (28000): İstemci IP adresi 123.456.789.0 tooaccess hello sunucu izin verilmiyor.
    >
    > tooresolve hello hata yapma emin hello sunucu yapılandırması eşleşme hello adımları hello *bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırın* hello makalenin bölümüne.

4. Görünüm sunucu durumu tooensure hello bağlantısı çalışır durumdadır. Türü `status` hello mysql adresindeki > bunu bağlandıktan sonra ister.
    ```sql
    status
    ```

   > [!TIP]
   > Ek komutlar için bkz. [MySQL 5.7 Başvuru Kılavuzu - Bölüm 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).

5.  Merhaba mysql boş bir veritabanı oluşturun > merhaba aşağıdaki komutu yazarak istem:
    ```sql
    CREATE DATABASE quickstartdb;
    ```
    Merhaba komutu birkaç dakika sonra toocomplete sürebilir. 

    MySQL sunucusu için Azure Veritabanı içinde bir veya birden fazla veritabanı oluşturabilirsiniz. Tüm hello kaynakları toocreate sunucu tooutilize başına tek bir veritabanı opt veya birden çok veritabanları tooshare hello kaynakları oluşturun. Hiçbir toohello sayısı sınırı oluşturulabilir veritabanları yoktur, ancak birden çok veritabanı hello paylaşmak aynı sunucu kaynakları. 

6. Liste hello mysql hello veritabanlarındaki > merhaba aşağıdaki komutu yazarak istem:

    ```sql
    SHOW DATABASES;
    ```

7.  Tür `\q` ve tooquit hello mysql aracı ENTER tuşuna basın. Tamamladıktan sonra hello Azure bulut Kabuk kapatabilirsiniz.

Şimdi toohello Azure veritabanı için MySQL bağlı sahip ve boş kullanıcı veritabanı oluşturuldu. Toohello sonraki bölümde toorepeat benzer bir alıştırma tooconnect toohello devam başka bir ortak aracı, MySQL çalışma ekranı kullanarak aynı sunucu.

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Merhaba MySQL çalışma ekranı GUI aracını kullanarak toohello sunucuya bağlanın
tooconnect tooAzure MySQL server: Hello GUI aracıyla MySQL çalışma ekranı

1.  Merhaba, istemci bilgisayardaki MySQL çalışma ekranı uygulaması başlatın. MySQL Workbench uygulamasını [buradan](https://dev.mysql.com/downloads/workbench/) indirip yükleyebilirsiniz.

2.  İçinde **yeni bağlantı kurma** iletişim kutusunda, aşağıdaki bilgilerle hello girin **parametreleri** sekmesi:

    ![yeni bağlantı oluştur](./media/quickstart-create-mysql-server-database-using-azure-portal/setup-new-connection.png)

    | **Ayar** | **Önerilen değer** | **Alan Açıklaması** |
    |---|---|---|
    |   Bağlantı Adı | Tanıtım Bağlantısı | Bu bağlantı için bir etiket belirtin. |
    | Bağlantı Yöntemi | Standart (TCP/IP) | Standart (TCP/IP) yeterlidir. |
    | Ana Bilgisayar Adı | *sunucu adı* | Hello Azure veritabanı için MySQL daha önce oluşturduğunuz zaman, kullanılan hello sunucu adı değeri belirtin. Gösterilen örnek sunucumuz: myserver4demo.mysql.database.azure.com. Merhaba tam etki alanı adını kullan (\*. mysql.database.azure.com) hello örnekte gösterildiği gibi. Sunucu adınız anımsamıyorsanız hello önceki bölümde tooget hello bağlantı bilgilerini hello adımları izleyin.  |
    | Bağlantı noktası | 3306 | Her zaman bağlantı noktası tooAzure veritabanı için MySQL bağlanırken 3306 kullanın. |
    | Kullanıcı adı |  *sunucu yöneticisi oturum açma adı* | İçinde hello sunucu yönetici oturum açma kullanıcı hello Azure veritabanı için MySQL daha önce oluşturduğunuz zaman sağlanan yazın. Bizim örnek kullanıcı adımız myadmin@myserver4demo. Merhaba kullanıcıadı anımsamıyorsanız hello önceki bölümde tooget hello bağlantı bilgilerini hello adımları izleyin. Merhaba biçimi  *username@servername* .
    | Parola | parolanız | Tıklatın depolama kasasına... düğmesine toosave hello parola. |

    Tıklatın **Bağlantıyı Sına** tüm parametrelerin doğru yapılandırılmışsa tootest. Tamam toosave hello bağlantısını tıklatın. 

    > [!NOTE]
    > SSL varsayılan olarak, sunucunuzdaki zorunlu ve başarıyla sipariş tooconnect ek yapılandırma gerektirir. Bkz: [yapılandırma SSL bağlantısı'nda uygulama toosecurely bağlanmak tooAzure veritabanı için MySQL](./howto-configure-ssl.md).  Bu Hızlı Başlangıç için toodisable SSL istiyorsanız hello Azure portalını ziyaret edin ve hello bağlantı güvenlik sayfası toodisable hello Zorla SSL bağlantısı Değiştir düğmesini tıklatın.

## <a name="clean-up-resources"></a>Kaynakları temizleme
Temiz hello hızlı başlangıcı oluşturduğunuz hello kaynakları silerek hello [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md)hello kaynak grubundaki tüm hello kaynakları içerir veya varsa hello bir sunucu kaynağı silerek tookeep hello istiyor olduğu gibi diğer kaynaklar.

> [!TIP]
> Bu koleksiyondaki diğer Hızlı Başlangıçlar, bu Hızlı Başlangıcı temel alır. Sonraki ile toowork toocontinue planlıyorsanız bu quickstart oluşturulan kaynakları quickstarts, değil temizleme hello. Toocontinue düşünmüyorsanız bu hızlı başlangıcı hello Azure portal tarafından oluşturulan tüm kaynakları adımları toodelete aşağıdaki hello kullanın.
>

Yeni oluşturulan hello server dahil olmak üzere toodelete hello tüm kaynak grubu:
1.  Kaynak grubunuzun hello Azure portalı bulun. Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve hello örneğimizde gibi kaynak grubunuzun adını ardından **myresourcegroup**.
2.  Kaynak grubunuzun sayfasında **Sil**’e tıklayın. Ardından türü hello kaynak grubunuzun adını, Örneğimizdeki gibi **myresourcegroup**, buna hello metin kutusu tooconfirm silme ve ardından **silmek**.

Veya bunun yerine, toodelete hello sunucu yeni oluşturulan:
1.  Açık yoksa sunucunuz hello Azure portalı bulun. Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları**ve oluşturduğunuz hello sunucusu için arama yapın.
2.  Merhaba üzerinde **genel bakış** hello sayfasında, **silmek** hello üst bölmesindeki düğmesi.
![MySQL için Azure Veritabanı - Sunucuyu silme](./media/quickstart-create-mysql-server-database-using-azure-portal/delete-server.png)
3.  Toodelete istediğiniz ve etkilenen altındaki hello veritabanlarını Göster hello sunucu adını doğrulayın. Bizim örneğimizde gibi hello metin kutusuna sunucunuzun adını yazın **myserver4demo**ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

> [!div class="nextstepaction"]
> [İlk MySQL için Azure Veritabanınızı tasarlama](./tutorial-design-database-using-portal.md)

