---
title: "MySQL çalışma ekranı MySQL'den için tooAzure veritabanına bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç hello adımları toouse MySQL çalışma ekranı MySQL için Azure veritabanındaki tooconnect ve sorgu verileri sağlar."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a>Azure veritabanı için MySQL: kullanım MySQL çalışma ekranı tooconnect ve sorgu verileri
Bu hızlı başlangıç gösteren nasıl MySQL kullanma tooconnect tooan Azure veritabanı hello MySQL çalışma ekranı uygulama. 

## <a name="prerequisites"></a>Ön koşullar
Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:
- [Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a>MySQL çalışma ekranı yükleyin
Karşıdan yükleyip MySQL çalışma ekranı bilgisayarınıza [hello MySQL Web sitesi](https://dev.mysql.com/downloads/workbench/).

## <a name="get-connection-information"></a>Bağlantı bilgilerini alma
Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için MySQL alın. Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).

2. Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve oluşturduğunuz, gibi hello sunucu araması **myserver4demo**.

3. Merhaba sunucu adına tıklayın.

4. Select hello sunucunun **özellikleri** sayfası. Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.

 ![Azure veritabanı için MySQL sunucu adı](./media/connect-workbench/1-server-properties-name-login.png)
 
5. Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.

## <a name="connect-toohello-server-using-mysql-workbench"></a>MySQL çalışma ekranı kullanarak toohello sunucusuna bağlan 
tooconnect tooAzure MySQL server: Hello GUI aracıyla MySQL çalışma ekranı

1.  Merhaba, bilgisayarınızdaki MySQL çalışma ekranı uygulama başlatın. 

2.  İçinde **yeni bağlantı kurma** iletişim kutusunda, üzerinde hello bilgisinden hello girin **parametreleri** sekmesi:

    ![yeni bağlantı oluştur](./media/connect-workbench/2-setup-new-connection.png)

    | **Ayar** | **Önerilen değer** | **Alan açıklaması** |
    |---|---|---|
    |   Bağlantı Adı | Tanıtım Bağlantısı | Bu bağlantı için bir etiket belirtin. |
    | Bağlantı Yöntemi | Standart (TCP/IP) | Standart (TCP/IP) yeterlidir. |
    | Ana Bilgisayar Adı | *sunucu adı* | Hello Azure veritabanı için MySQL daha önce oluşturduğunuz zaman, kullanılan hello sunucu adı değeri belirtin. Gösterilen örnek sunucumuz: myserver4demo.mysql.database.azure.com. Merhaba tam etki alanı adını kullan (\*. mysql.database.azure.com) hello örnekte gösterildiği gibi. Sunucu adınız anımsamıyorsanız hello önceki bölümde tooget hello bağlantı bilgilerini hello adımları izleyin.  |
    | Bağlantı noktası | 3306 | Her zaman bağlantı noktası tooAzure veritabanı için MySQL bağlanırken 3306 kullanın. |
    | Kullanıcı adı |  *sunucu yöneticisi oturum açma adı* | İçinde hello sunucu yönetici oturum açma kullanıcı hello Azure veritabanı için MySQL daha önce oluşturduğunuz zaman sağlanan yazın. Bizim örnek kullanıcı adımız myadmin@myserver4demo. Merhaba kullanıcıadı anımsamıyorsanız hello önceki bölümde tooget hello bağlantı bilgilerini hello adımları izleyin. Merhaba biçimi  *username@servername* .
    | Parola | parolanız | Tıklatın **kasası deposunda...**  düğmesi toosave hello parola. |

3.   Tıklatın **Bağlantıyı Sına** tüm parametrelerin doğru yapılandırılmışsa tootest. 

4.   Tıklatın **Tamam** toosave hello bağlantı. 

5.   Merhaba listesi içinde **MySQL bağlantısı**hello döşeme karşılık gelen tooyour server'ı tıklatın ve kurulan hello bağlantı toobe için bekleyin.

6.   Yeni bir SQL sekmesi sorgularınızı yazabileceğiniz için boş bir Düzenleyicisi açılır.

    > [!NOTE]
    > Varsayılan olarak, SSL bağlantı güvenliği gereklidir ve Azure veritabanınızı MySQL sunucusu için zorunlu tutulur. Genellikle SSL sertifikalarıyla ek yapılandırma MySQL çalışma ekranı tooconnect tooyour sunucusu için gereklidir. SSL hakkında daha fazla bilgi için bkz: [yapılandırma SSL bağlantısı'nda uygulama toosecurely bağlanmak tooAzure veritabanı için MySQL](./howto-configure-ssl.md).  Toodisable SSL gerekiyorsa, hello Azure portalını ziyaret edin ve hello bağlantı güvenlik sayfası toodisable hello Zorla SSL bağlantısı Değiştir düğmesini tıklatın.

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a>Bir tablo oluşturma, veri eklemek, veri okuma, verileri güncelleştirmek, verilerini sil
1. Merhaba örnek SQL kodu kopyalayıp boş bir SQL sekmesi tooillustrate bazı örnek veriler yapıştırın.

    Bu kod quickstartdb adlı boş bir veritabanı oluşturur ve stok adlandırılmış bir örnek tablo oluşturur. Bazı satırlar ekler ve ardından hello satırları okur. Bir güncelleştirme deyimi hello verilerle değiştirir ve okuma satırları yeniden Merhaba. Son olarak, bir satırı siler ve hello satırları yeniden okur.
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    çalışması bittikten sonra hello ekran SQL çalışma ekranı ve hello çıktısında hello SQL kodu örneği gösterilmektedir.
    
    ![MySQL çalışma ekranı SQL sekmesi toorun örnek SQL kodu](media/connect-workbench/3-workbench-sql-tab.png)

2. toorun hello örnek SQL kodu tıklatın hello hello araç Cıvata simgesine gölge hello **SQL dosyası** sekmesi.
3. Merhaba üç sekmeli sonuçlarında hello fark **sonuç kılavuz** hello orta bölümünde hello sayfasının. 
4. Bildirim hello **çıkış** hello sayfanın hello sonundaki listesi. Her komut Hello durumu gösterilir. 

Şimdi, tooAzure veritabanı için MySQL MySQL çalışma ekranı kullanarak bağlı ve hello SQL dilini kullanarak veri sorguladınız.

## <a name="next-steps"></a>Sonraki adımlar
> [!div class="nextstepaction"]
> [Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme](./concepts-migrate-import-export.md)
