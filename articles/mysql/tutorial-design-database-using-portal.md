---
title: "İlk Azure veritabanı için MySQL veritabanı - Azure Portal aaaDesign | Microsoft Docs"
description: "Bu öğretici açıklar nasıl toocreate Azure veritabanı için MySQL sunucusunu yönetmek ve Azure portalını kullanarak veritabanı."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>İlk Azure veritabanınızı MySQL veritabanı için tasarlama
Azure veritabanı için MySQL toorun sağlayan yönetilen bir hizmettir, yönetmek ve yüksek oranda kullanılabilir MySQL veritabanları hello bulutta ölçeklendirin. Hello Azure portal kullanarak kolayca sunucunuzu yönetin ve bir veritabanı tasarlayın.

Bu öğreticide, Azure portal toolearn hello nasıl kullanmak için:

> [!div class="checklist"]
> * MySQL için Azure bir veritabanı oluşturun
> * Merhaba sunucu Güvenlik Duvarı'nı yapılandırma
> * MySQL komut satırı aracı toocreate bir veritabanını kullanın
> * Örnek verileri yükleme
> * Verileri sorgulama
> * Verileri güncelleştirme
> * Verileri geri yükleme

## <a name="sign-in-toohello-azure-portal"></a>Toohello Azure portalında oturum açın
Sık kullanılan web tarayıcınızı açın ve hello ziyaret [Microsoft Azure portal](https://portal.azure.com/). Kimlik bilgileri toosign toohello Portalı'nda girin. Hizmet panonuz Hello varsayılan görünümüdür.

## <a name="create-an-azure-database-for-mysql-server"></a>MySQL için Azure Veritabanı sunucusu oluşturma
MySQL için Azure Veritabanı sunucusu, tanımlı bir dizi [işlem ve depolama kaynağı](./concepts-compute-unit-and-storage.md) ile oluşturulur. Merhaba server içinde oluşturulur bir [Azure kaynak grubu](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).

1. Çok gidin**veritabanları** > **Azure veritabanı için MySQL**. MySQL sunucusu altında bulamazsa **veritabanları** kategorisi, tıklatın **tümünü görmek** tooshow kullanılabilir tüm Hizmetleri veritabanı. Ayrıca yazabilirsiniz **Azure veritabanı için MySQL** hello arama kutusu tooquickly hello hizmeti bulamadı.
![2-1 Bul tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)

2. Tıklatın **Azure veritabanı için MySQL** kutucuğuna ve ardından **oluşturma**.

Bizim örneğimizde, hello Azure veritabanı MySQL form için aşağıdaki bilgilerle hello ile doldurun:

| **Ayar** | **Önerilen değer** | **Alan Açıklaması** |
|---|---|---|
| *Sunucu adı* | myserver4demo  | Sunucu adı toobe genel benzersiz sahiptir. |
| *Abonelik* | mysubscription | Aboneliğinizi hello açılan listeden seçin. |
| *Kaynak grubu* | myresourcegroup | Bir kaynak grubu oluşturun veya mevcut olanlardan birini kullanın. |
| *Sunucu yöneticisi oturum açma bilgileri* | myadmin | Kurulum Yönetici hesap adı. |
| *Parola* |  | Güçlü bir yönetici hesabı parolası belirleyin. |
| *Parolayı onayla* |  | Merhaba yönetici hesabı parolasını onaylayın. |
| *Konum* |  | Kullanılabilir bir bölge seçin. |
| *Sürüm* | 5.7 | Merhaba en son sürümünü seçin. |
| *Performansı yapılandır* | Temel, 50 birimleri, 50 GB işlem  | **Fiyatlandırma katmanı**, **İşlem Birimleri**, **Depolama (GB)** öğelerini seçip **Tamam**’a tıklayın. |
| *PIN tooDashboard* | İşaretli | Toocheck, bu kutu önerilir, böylece hello sunucu üzerinde kolayca daha sonra bulabilirsiniz |
Sonra, **Oluştur**’a tıklayın. Bir veya iki dakika içinde MySQL sunucusu için yeni bir Azure veritabanı hello bulutta çalışmaktadır. Tıklayabilirsiniz **bildirimleri** hello araç toomonitor hello dağıtım işlemi düğmesinde.

## <a name="configure-firewall"></a>Güvenlik duvarını yapılandırma
Azure veritabanları MySQL için bir güvenlik duvarı tarafından korunur. Varsayılan olarak, tüm bağlantılar toohello sunucusu ve hello veritabanları hello Sunucusu'ndaki reddedilir. TooAzure veritabanı için MySQL hello için ilk kez bağlanmadan önce hello güvenlik duvarı tooadd hello istemci makinenin ortak ağ IP adresi (veya IP adresi aralığı) yapılandırın.

1. Yeni oluşturulan sunucunuz tıklayın ve ardından **bağlantı güvenliği**.
   ![3 1 bağlantı güvenliği](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)
2. Yapabilecekleriniz **eklemek IP**, veya güvenlik duvarı kurallarını yapılandırın. Tooclick unutmayın **kaydetmek** hello kuralları oluşturduktan sonra.
Şimdi, mysql komut satırı aracını veya MySQL çalışma ekranı GUI aracını kullanarak toohello sunucusuna bağlanabilir.

> [!TIP]
> MySQL sunucusu için Azure veritabanı 3306 bağlantı noktası üzerinden iletişim kurar. Bir şirket ağından gelen tooconnect çalışıyorsanız, bağlantı noktası 3306 üzerinden giden trafik, ağınızın güvenlik duvarı tarafından izin verilmiyor. BT departmanınız 3306 bir bağlantı noktası açar sürece bu durumda, tooAzure MySQL server bağlanamıyor.

## <a name="get-connection-information"></a>Bağlantı bilgilerini alma
Tam alma hello **sunucu adı** ve **sunucu yönetici oturum açma adı** hello Azure portal MySQL sunucudan için Azure veritabanınızın. Mysql komut satırı aracını kullanarak hello tam adı tooconnect tooyour sunucusu kullanın. 

1. İçinde [Azure portal](https://portal.azure.com/), tıklatın **tüm kaynakları** hello sol taraftaki menüyü, hello adını yazın ve arama MySQL server için Azure veritabanınızın. Merhaba sunucu adı tooview hello Ayrıntılar'ı seçin.

2. Hello ayarları altında başlığını tıklatın **özellikleri**. Aşağı Not **sunucu adı** ve **sunucu yönetici oturum açma adı**. Hello Kopyala düğmesine bir sonraki tooeach alan toocopy toohello Pano tıklatabilirsiniz.
   ![4-2 sunucu özellikleri](./media/tutorial-design-database-using-portal/4_2-server-properties.png)

Bu örnekte, hello sunucu adıdır *myserver4demo.mysql.database.azure.com*, ve hello Sunucu Yöneticisi oturum açma  *myadmin@myserver4demo* .

## <a name="connect-toohello-server-using-mysql"></a>MySQL kullanarak toohello sunucusuna bağlan
Kullanım [mysql komut satırı aracı](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish MySQL sunucusu için bağlantı tooyour Azure veritabanı. Hello Azure bulut Kabuk hello tarayıcıda veya mysql araçlarının yüklü kullanarak yerel olarak kendi makineden hello mysql komut satırı aracını çalıştırabilirsiniz. toolaunch hello Azure bulut Kabuk tıklatın hello `Try It` bu makaledeki kod bloğu düğmesine veya hello Azure portalını ziyaret edin ve hello tıklatın `>_` hello üst sağ araç çubuğunda simge. 

Merhaba komutu tooconnect yazın:
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a>Boş veritabanı oluşturma
Bağlı toohello sunucu olduğunuzda, bir boş veritabanı toowork ile oluşturun.
```sql
CREATE DATABASE mysampledb;
```

Merhaba isteminde komut tooswitch bağlantı toothis yeni oluşturulan veritabanı aşağıdaki hello çalıştırın:
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Merhaba veritabanında tabloları oluşturma
Nasıl tooconnect toohello Azure veritabanı MySQL veritabanı için biz nasıl gidebilirsiniz bildiğinize göre toocomplete temel bazı görevler.

İlk olarak, size bir tablo oluşturun ve bazı verilerle yükleyin. Envanter bilgilerini depolayan bir tablo oluşturalım.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Merhaba tablolara veri yükleme
Bir tablo sahibiz, biz bazı veri içine ekleyebilirsiniz. Merhaba açık komut istemi penceresinde, sorgu tooinsert aşağıdaki hello bazı satırlar alt kümesini çalıştırın.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Şimdi örnek verilerin daha önce oluşturduğunuz hello tabloya iki satır var.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Sorgulamak ve hello hello tablolarındaki verileri güncelleyin
Sorgu tooretrieve bilgisinden hello veritabanı tablosundan hello yürütün.
```sql
SELECT * FROM inventory;
```

Ayrıca hello tablolardaki hello verileri güncelleştirebilirsiniz.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

veri aldığınızda hello satır buna göre güncelleştirilir.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Zaman içinde veritabanı tooa önceki bir noktaya geri
Önemli veritabanı tablosu yanlışlıkla sildiyseniz ve hello verileri kolayca kurtaramazsınız düşünün. Azure veritabanı için MySQL yeni sunucuyu hello veritabanları bir kopyası oluşturuluyor, zaman içindeki toorestore hello sunucusu tooa noktası sağlar. Bu yeni sunucu toorecover silinmiş verilerinizi kullanabilirsiniz. Merhaba Hello tablo eklenmeden önce aşağıdaki adımları geri yükleme hello örnek sunucu tooa noktası.

1. Hello Azure portal, Azure veritabanı için MySQL bulun. Merhaba üzerinde **genel bakış** sayfasında, **geri** hello araç. Merhaba geri yükleme sayfası açılır.

   ![10-1, bir veritabanını geri yükleyin](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. Merhaba doldurun **geri** hello gerekli bilgilerle formu.
   
   ![10-2 geri yükleme formu](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - **Geri yükleme noktası**: bir noktası listelenen hello zaman çerçevesi içinde toorestore için istediğiniz zaman seçin. Yerel saat dilimi tooUTC tooconvert emin olun.
   - **Toonew sunucuyu geri**: toorestore için istediğiniz yeni bir sunucu adı sağlayın.
   - **Konum**: hello bölge hello kaynak sunucu ile aynı olması ve değiştirilemez.
   - **Fiyatlandırma katmanı**: fiyatlandırma katmanı hello olduğu hello hello aynı kaynak sunucu ve değiştirilemez.
   
3. Tıklatın **Tamam** toorestore hello sunucu çok[tooa noktası zaman içinde geri](./howto-restore-server-portal.md) hello tablo silinmeden önce. Bir sunucuyu geri belirttiğiniz hello noktaya itibariyle hello sunucu yeni bir kopyasını oluşturur. 

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, Azure portal toolearned hello nasıl kullanmak için:

> [!div class="checklist"]
> * MySQL için Azure bir veritabanı oluşturun
> * Merhaba sunucu Güvenlik Duvarı'nı yapılandırma
> * MySQL komut satırı aracı toocreate bir veritabanını kullanın
> * Örnek verileri yükleme
> * Verileri sorgulama
> * Verileri güncelleştirme
> * Verileri geri yükleme

> [!div class="nextstepaction"]
> [Nasıl tooconnect uygulamaları tooAzure veritabanı için MySQL](./howto-connection-string.md)
