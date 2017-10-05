---
title: "Azure veritabanı için MySQL MySQL çalışma ekranından bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç bağlanmak ve MySQL için Azure veritabanındaki verileri sorgulamak için MySQL çalışma ekranı kullanmak için adımları sağlar."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: 20a1f31ce42abb924504c4008f85420fc49aec89
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-to-connect-and-query-data"></a>Azure veritabanı için MySQL: kullanım MySQL çalışma ekranı bağlanmak ve verileri sorgulamak için
Bu Hızlı Başlangıç, MySQL çalışma ekranı uygulamayı kullanarak MySQL için bir Azure veritabanına bağlanmak gösterilmiştir. 

## <a name="prerequisites"></a>Ön koşullar
Bu hızlı başlangıçta, başlangıç noktası olarak şu kılavuzlardan birinde oluşturulan kaynaklar kullanılmaktadır:
- [Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a>MySQL çalışma ekranı yükleyin
Karşıdan yükleyip MySQL çalışma ekranı bilgisayarınıza [MySQL Web sitesi](https://dev.mysql.com/downloads/workbench/).

## <a name="get-connection-information"></a>Bağlantı bilgilerini alma
MySQL için Azure Veritabanı'na bağlanmak üzere gereken bağlantı bilgilerini alın. Tam sunucu adına ve oturum açma kimlik bilgilerine ihtiyacınız vardır.

1. [Azure Portal](https://portal.azure.com/)’da oturum açın.

2. Azure portalında sol taraftaki menüden **Tüm kaynaklar**'a tıklayın ve oluşturduğunuz sunucuyu (örneğin, **myserver4demo**) arayın.

3. Sunucunun adına tıklayın.

4. Sunucunun **Özellikler** sayfasını seçin. **Sunucu adını** ve **Sunucu yöneticisi oturum açma adını** not edin.

 ![Azure veritabanı için MySQL sunucu adı](./media/connect-workbench/1-server-properties-name-login.png)
 
5. Sunucunuzun oturum açma bilgilerini unuttuysanız **Genel Bakış** sayfasına giderek Sunucu yöneticisi oturum açma adını görüntüleyin ve gerekirse parolayı sıfırlayın.

## <a name="connect-to-the-server-using-mysql-workbench"></a>MySQL çalışma ekranı kullanarak sunucuya bağlanın 
MySQL Workbench GUI aracını kullanarak Azure MySQL sunucusuna bağlanmak için:

1.  Bilgisayarınızda MySQL çalışma ekranı uygulamayı başlatın. 

2.  İçinde **yeni bağlantı kurma** iletişim kutusunda, aşağıdaki bilgileri girin **parametreleri** sekmesi:

    ![yeni bağlantı oluştur](./media/connect-workbench/2-setup-new-connection.png)

    | **Ayar** | **Önerilen değer** | **Alan açıklaması** |
    |---|---|---|
    |   Bağlantı Adı | Tanıtım Bağlantısı | Bu bağlantı için bir etiket belirtin. |
    | Bağlantı Yöntemi | Standart (TCP/IP) | Standart (TCP/IP) yeterlidir. |
    | Ana Bilgisayar Adı | *sunucu adı* | MySQL için Azure Veritabanını oluştururken kullandığınız sunucu adı değerini belirtin. Gösterilen örnek sunucumuz: myserver4demo.mysql.database.azure.com. Örnekte gösterildiği gibi tam etki alanı adını (\*.mysql.database.azure.com) kullanın. Sunucu adınızı anımsamıyorsanız bağlantı bilgilerini almak için bir önceki bölümdeki adımları izleyin.  |
    | Bağlantı noktası | 3306 | MySQL Azure veritabanına bağlanırken her zaman bağlantı noktası olarak 3306 kullanın. |
    | Kullanıcı adı |  *sunucu yöneticisi oturum açma adı* | MySQL için Azure Veritabanını oluştururken girdiğiniz sunucu yöneticisi oturum açma kullanıcı adını yazın. Bizim örnek kullanıcı adımız myadmin@myserver4demo. Kullanıcı adını anımsamıyorsanız bağlantı bilgilerini almak için bir önceki bölümdeki adımları izleyin. Biçim şöyledir: *username@servername*.
    | Parola | parolanız | Tıklatın **kasası deposunda...**  Parolayı Kaydet düğmesi. |

3.   Tüm parametrelerin doğru yapılandırılıp yapılandırılmadığını test etmek için **Bağlantıyı Sına**’ya tıklayın. 

4.   Tıklatın **Tamam** bağlantıyı kaydetmek için. 

5.   Listesini içinde **MySQL bağlantısı**, sunucunuza karşılık gelen kutucuğa tıklayın ve bağlantının sağlanabilmesi için bekleyin.

6.   Yeni bir SQL sekmesi sorgularınızı yazabileceğiniz için boş bir Düzenleyicisi açılır.

    > [!NOTE]
    > Varsayılan olarak, SSL bağlantı güvenliği gereklidir ve Azure veritabanınızı MySQL sunucusu için zorunlu tutulur. Genellikle SSL sertifikalarıyla ek yapılandırma MySQL sunucunuza bağlanmak çalışma ekranı için gereklidir. SSL hakkında daha fazla bilgi için bkz: [uygulamanızda güvenli bir şekilde MySQL için Azure veritabanına bağlanmak için SSL yapılandırma bağlantısı](./howto-configure-ssl.md).  SSL devre dışı bırakmanız gerekirse Azure portalını ziyaret edin ve zorunlu SSL bağlantısı iki durumlu düğme devre dışı bırakmak için bağlantı güvenliği Sayfası'ı tıklatın.

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a>Bir tablo oluşturma, veri eklemek, veri okuma, verileri güncelleştirmek, verilerini sil
1. Örnek SQL kodu kopyalayıp bazı örnek veriler göstermek için boş bir SQL sekmesi yapıştırın.

    Bu kod quickstartdb adlı boş bir veritabanı oluşturur ve stok adlandırılmış bir örnek tablo oluşturur. Bazı satırlar ekler satırları daha sonra okur. Bir güncelleştirme deyimi verilerle değiştirir ve satırları yeniden okur. Son olarak, bir satır siler ve satırları yeniden okur.
    
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

    Çalışması bittikten sonra ekran SQL çalışma ekranı hem de çıkış SQL kod örneğini gösterir.
    
    ![Örnek SQL kodu çalıştırmak için MySQL çalışma ekranı SQL sekmesi](media/connect-workbench/3-workbench-sql-tab.png)

2. SQL kodu örneği çalıştırmak için araç çubuğunda açıklaştırıcı Cıvata simgesini tıklatın **SQL dosyası** sekmesi.
3. Üç sekmeli sonuçlarında fark **sonuç kılavuz** sayfasının ortasında bölümü. 
4. Bildirim **çıkış** sayfanın sonundaki listesi. Her komut durumu gösterilir. 

Şimdi, Azure veritabanı için MySQL çalışma ekranı kullanarak MySQL için bağlı ve SQL dilini kullanarak veri sorguladınız.

## <a name="next-steps"></a>Sonraki adımlar
> [!div class="nextstepaction"]
> [Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme](./concepts-migrate-import-export.md)
