---
title: "Azure SQL veri ambarı oluşturma - Azure Portal | Microsoft Docs"
description: "Azure SQL Veri Ambarı için, bir SQL sunucusu, sunucu düzeyi güvenlik kuralı ve Azure portalında bir veri ambarı oluşturun. Ardından sorgulayın."
keywords: "sql veri ambarı öğreticisi, SQL veri ambarı oluşturma"
services: sql-database
documentationcenter: 
author: barbkess
manager: jhubbard
editor: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: Active
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: quickstart
ms.date: 11/20/2017
ms.author: barbkess
ms.openlocfilehash: 65c1344aa9d5a997e4917191978f5d12da5eb0db
ms.sourcegitcommit: 310748b6d66dc0445e682c8c904ae4c71352fef2
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2017
---
# <a name="create-and-query-an-azure-sql-data-warehouse-in-the-azure-portal"></a>Azure portalında Azure SQL veri ambarı oluşturma ve sorgulama

Azure portalını kullanarak hızla bir Azure SQL veri ambarı oluşturun ve sorgulayın.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.

## <a name="before-you-begin"></a>Başlamadan önce

[SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms.md)’nun (SSMS) en yeni sürümünü indirin ve yükleyin.

## <a name="sign-in-to-the-azure-portal"></a>Azure portalında oturum açın

[Azure Portal](https://portal.azure.com/) oturum açın.

## <a name="create-a-data-warehouse"></a>Veri ambarı oluşturma

Azure SQL veri ambarı bir dizi [işlem kaynağı](performance-tiers.md) ile oluşturulur. Veritabanı bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) ve bir [Azure SQL mantıksal sunucusu](../sql-database/sql-database-features.md) içinde oluşturulur. 

AdventureWorksDW örnek verileri içeren bir SQL veri ambarı oluşturmak için bu adımları izleyin. 

1. Azure portalının sol üst köşesinde bulunan **Yeni** düğmesine tıklayın.

2. **Yeni** sayfasından **Veritabanları**’nı seçin ve **Yeni** sayfasında **Öne Çıkan** altından **SQL Veri Ambarı**’nı seçin.

    ![boş veri ambarı oluşturma](media/load-data-from-azure-blob-storage-using-polybase/create-empty-data-warehouse.png)

3. SQL Veri Ambarı formunu aşağıdaki bilgilerle doldurun:   

    | Ayar | Önerilen değer | Açıklama | 
    | ------- | --------------- | ----------- | 
    | **Veritabanı adı** | mySampleDataWarehouse | Geçerli veritabanı adları için bkz. [Veritabanı Tanımlayıcıları](/sql/relational-databases/databases/database-identifiers). Veri ambarının bir veritabanı türü olduğuna dikkat edin.| 
    | **Abonelik** | Aboneliğiniz  | Abonelikleriniz hakkında daha ayrıntılı bilgi için bkz. [Abonelikler](https://account.windowsazure.com/Subscriptions). |
    | **Kaynak grubu** | myResourceGroup | Geçerli kaynak grubu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). |
    | **Kaynak seçme** | Örnek | Örnek bir veritabanı yüklemek için belirtir. Veri ambarının bir veritabanı türü olduğuna dikkat edin. |
    | **Örnek seçme** | AdventureWorksDW | AdventureWorksDW örnek veritabanını yüklemeyi belirtir.  |

    ![veri ambarı oluşturma](media/create-data-warehouse-portal/select-sample.png)

4. Yeni veritabanınız için yeni bir sunucu oluşturup yapılandırmak üzere **Sunucu**’ya tıklayın. **Yeni sunucu formu**’nu aşağıdaki bilgilerle doldurun: 

    | Ayar | Önerilen değer | Açıklama | 
    | ------------ | ------------------ | ------------------------------------------------- | 
    | **Sunucu adı** | Genel olarak benzersiz bir ad | Geçerli sunucu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). | 
    | **Sunucu yöneticisi oturum açma bilgileri** | Geçerli bir ad | Geçerli oturum açma adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).|
    | **Parola** | Geçerli bir parola | Parolanızda en az 8 karakter bulunmalı ve parolanız şu üç kategoriden karakterler içermelidir: büyük harf karakterler, küçük harf karakterler, sayılar ve alfasayısal olmayan karakterler. |
    | **Konum** | Geçerli bir konum | Bölgeler hakkında bilgi için bkz. [Azure Bölgeleri](https://azure.microsoft.com/regions/). |

    ![veritabanı oluşturma](media/load-data-from-azure-blob-storage-using-polybase/create-database-server.png)

5. **Seç**'e tıklayın.

6. Veri ambarı için performans yapılandırmasını belirtmek üzere **Performans katmanı**’na tıklayın.

7. Bu öğretici için, **Elastiklik için İyileştirilmiş** performans katmanını seçin. Kaydırıcı varsayılan olarak **DW400**’e ayarlanmıştır.  Nasıl çalıştığını görmek için yukarı ve aşağı taşımayı deneyin. 

    ![performansı yapılandırma](media/load-data-from-azure-blob-storage-using-polybase/configure-performance.png)

8. **Uygula**'ya tıklayın.

9. SQL Veritabanı formunu tamamladıktan sonra veritabanını sağlamak için **Oluştur**’a tıklayın. Sağlama birkaç dakika sürer. 

    ![oluştur’a tıklayın](media/load-data-from-azure-blob-storage-using-polybase/click-create.png)

10. Araç çubuğunda **Bildirimler**’e tıklayarak dağıtım işlemini izleyin.
    
     ![bildirim](media/load-data-from-azure-blob-storage-using-polybase/notification.png)

## <a name="create-a-server-level-firewall-rule"></a>Sunucu düzeyinde bir güvenlik duvarı kuralı oluşturma

SQL Veri Ambarı hizmeti, dış uygulama ve araçların sunucuya ya da sunucu üzerindeki herhangi bir veritabanına bağlanmasını engelleyen sunucu düzeyinde bir güvenlik duvarı kuralı oluşturur. Bağlantıyı etkinleştirmek için, belirli IP adresleri için bağlantıyı etkinleştiren güvenlik duvarı kuralları ekleyebilirsiniz.  İstemcinizin IP adresine yönelik bir [sunucu düzeyi güvenlik duvarı kuralı](../sql-database/sql-database-firewall-configure.md) oluşturmak için bu adımları izleyin. 

> [!NOTE]
> SQL Veri Ambarı 1433 numaralı bağlantı noktası üzerinden iletişim kurar. Kurumsal ağ içinden bağlanmaya çalışıyorsanız, ağınızın güvenlik duvarı tarafından 1433 numaralı bağlantı noktası üzerinden giden trafiğe izin verilmiyor olabilir. Bu durumda BT departmanınız 1433 numaralı bağlantı noktasını açmadığı sürece Azure SQL Veritabanı sunucunuza bağlanamazsınız.
>

1. Dağıtım tamamlandıktan sonra, soldaki menüden **SQL veritabanları**'na ve ardından **SQL veritabanları** sayfasında **mySampleDatabase** öğesine tıklayın. Veritabanınıza ilişkin genel bakış sayfası açılır ve tam sunucu adı (örneğin, **mynewserver-20171113.database.windows.net**) görüntülenerek daha fazla yapılandırma seçeneği sunulur. 

2. Sonraki hızlı başlangıçlarda sunucunuza ve veritabanlarına bağlanmak için bu tam sunucu adını kopyalayın. Sunucu ayarlarını açmak için sunucu adına tıklayın.

   ![sunucu adını bulma](media/load-data-from-azure-blob-storage-using-polybase/find-server-name.png) 

3. Sunucu ayarlarını açmak için, 
4. sunucu adına tıklayın.

   ![sunucu ayarları](media/load-data-from-azure-blob-storage-using-polybase/server-settings.png) 

5. **Güvenlik duvarı ayarlarını göster**’e tıklayın. SQL Veritabanı sunucusu için **Güvenlik duvarı ayarları** sayfası açılır. 

   ![sunucu güvenlik duvarı kuralı](media/load-data-from-azure-blob-storage-using-polybase/server-firewall-rule.png) 

4. Geçerli IP adresinizi yeni bir güvenlik duvarı kuralına eklemek için araç çubuğunda **İstemci IP’si Ekle** öğesine tıklayın. Güvenlik duvarı kuralı, 1433 numaralı bağlantı noktasını tek bir IP adresi veya bir IP adresi aralığı için açabilir.

5. **Kaydet** düğmesine tıklayın. Geçerli IP adresiniz için mantıksal sunucuda 1433 numaralı bağlantı noktası açılarak sunucu düzeyinde güvenlik duvarı kuralı oluşturulur.

6. **Tamam**’a tıklayın ve sonra **Güvenlik duvarı ayarları** sayfasını kapatın.

Şimdi bu IP adresini kullanarak SQL sunucusuna ve veri ambarlarına bağlanabilirsiniz. Bağlantı SQL Server Management Studio’dan veya seçtiğiniz diğer bir araçtan çalışır. Bağlandığınızda, daha önce oluşturduğunuz ServerAdmin hesabını kullanın.  

> [!IMPORTANT]
> Varsayılan olarak, SQL Veritabanı güvenlik duvarı üzerinden erişim tüm Azure hizmetleri için etkindir. Tüm Azure hizmetleri için güvenlik duvarını kapatmak üzere bu sayfada **KAPALI**’ya ve ardından **Kaydet**’e tıklayın.

## <a name="get-the-fully-qualified-server-name"></a>Tam sunucu adını alma

SQL sunucunuzun tam sunucu adını Azure portalından alabilirsiniz. Daha sonra sunucuya bağlanırken tam adı kullanırsınız.

1. [Azure Portal](https://portal.azure.com/) oturum açın.
2. Soldaki menüden **SQL Veritabanları**’nı seçin ve **SQL veritabanları** sayfasında veritabanınıza tıklayın. 
3. Veritabanınızın Azure portal sayfasındaki **Temel Bilgiler** bölmesinde, **Sunucu adını** bulup kopyalayın. Bu örnekte, tam ad mynewserver-20171113.database.windows.net. 

    ![bağlantı bilgileri](media/load-data-from-azure-blob-storage-using-polybase/find-server-name.png)  

## <a name="connect-to-the-server-as-server-admin"></a>Sunucu yöneticisi olarak sunucuya bağlanma

Bu bölümde Azure SQL sunucunuzla bağlantı kurmak için [SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms.md) (SSMS) kullanılmaktadır.

1. SQL Server Management Studio’yu açın.

2. **Sunucuya Bağlan** iletişim kutusuna şu bilgileri girin:

   | Ayar       | Önerilen değer | Açıklama | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | Sunucu türü | Veritabanı altyapısı | Bu değer gereklidir |
   | Sunucu adı | Tam sunucu adı | Örnek: **mynewserver-20171113.database.windows.net**. |
   | Kimlik Doğrulaması | SQL Server Kimlik Doğrulaması | Bu öğreticide yapılandırılan tek kimlik doğrulaması türü SQL Kimlik Doğrulamasıdır. |
   | Oturum Aç | Sunucu yöneticisi hesabı | Bu, sunucuyu oluştururken belirttiğiniz hesaptır. |
   | Parola | Sunucu yöneticisi hesabınızın parolası | Bu, sunucuyu oluştururken belirttiğiniz paroladır. |

    ![sunucuya bağlan](media/load-data-from-azure-blob-storage-using-polybase/connect-to-server.png)

4. **Bağlan**'a tıklayın. SSMS’te Nesne Gezgini penceresi açılır. 

5. Nesne Gezgini’nde, **Veritabanları**’nı genişletin. Daha sonra yeni veritabanınızdaki nesneleri görüntülemek için **mySampleDatabase**’i genişletin.

    ![veritabanı nesneleri](media/create-data-warehouse-portal/connected.png) 

## <a name="run-some-queries"></a>Sorgular çalıştırma

SQL Veri Ambarı sorgu dili olarak T-SQL kullanır. Bir sorgu penceresi açıp T-SQL sorguları çalıştırmak için, aşağıdaki adımları kullanın:

1. **mySampleDataWarehouse**’a sağ tıklayıp **Yeni Sorgu**’yu seçin.  Yeni bir sorgu penceresi açılır.
2. Sorgu penceresinde, veritabanlarının listesini görmek için aşağıdaki komutu girin.

    ```sql
    SELECT * FROM sys.databases
    ```

3. **Yürüt**’e tıklayın.  Sorgu sonuçları iki veritabanı gösterir: **master** ve **mySampleDataWarehouse**.

    ![Sorgu veritabanları](media/create-data-warehouse-portal/query-databases.png)

4. Verilere bakmak için, Adams soyadına sahip ve üç çocuğu olan müşteri sayısını görmek için aşağıdaki komutu kullanın. Sonuçlarda altı müşteri listelenir. 

    ```sql
    SELECT LastName, FirstName FROM dbo.dimCustomer
    WHERE LastName = 'Adams' AND NumberChildrenAtHome = 3;
    ```

    ![dbo.dimCustomer’ı sorgulama](media/create-data-warehouse-portal/query-customer.png)

## <a name="clean-up-resources"></a>Kaynakları temizleme

Veri ambarı birimleri ve veri ambarınızda depolanan veriler için ücretlendirilirsiniz. Bu işlem ve depolama alanı kaynakları ayrı ayrı faturalandırılır. 

- Verileri depoda tutmak istiyorsanız, veri ambarını kullanmadığınız zamanlarda işlemi duraklatabilirsiniz. İşlemi duraklatarak, yalnızca veri depolama için ücretlendirilirsiniz. Verilerle çalışmak için hazır olduğunuzda işlemi sürdürebilirsiniz.
- Gelecekteki ücretlendirmeleri kaldırmak istiyorsanız, veri ambarını silebilirsiniz. 

Kaynakları istediğiniz gibi temizlemek için bu adımları izleyin.

1. [Azure portalında](https://portal.azure.com) oturum açıp veri ambarınıza tıklayın.

    ![Kaynakları temizleme](media/load-data-from-azure-blob-storage-using-polybase/clean-up-resources.png)

1. İşlemi duraklatmak için, **Duraklat** düğmesine tıklayın. Veri ambarı duraklatıldığında, bir **Başlat** düğmesi görürsünüz.  İşlemi sürdürmek için **Başlat**’a tıklayın.

2. İşlem veya depolama için ücretlendirilmemek üzere veri ambarını kaldırmak için **Sil**’e tıklayın.

3. Oluşturduğunuz SQL sunucusunu kaldırmak için, önceki görüntüdeki **mynewserver-20171113.database.windows.net** öğesine tıklayıp **Sil**’e tıklayın.  Sunucuyu silmek sunucuyla ilişkili tüm veritabanlarını da sileceğinden bu silme işlemini gerçekleştirirken dikkatli olun.

4. Kaynak grubunu kaldırmak için, **myResourceGroup**’a tıklayıp daha sonra **Kaynak grubunu sil**’e tıklayın.


## <a name="next-steps"></a>Sonraki adımlar
Şimdi bir veri ambarı oluşturdunuz, bir güvenlik duvarı kuralı oluşturdunuz, veri ambarınıza bağlandınız ve birkaç sorgu çalıştırdınız. Azure SQL Veri Ambarı hakkında daha fazla bilgi edinmek için, veri yükleme öğreticisiyle devam edin.
> [!div class="nextstepaction"]
>[SQL veri ambarına veri yükleme](load-data-from-azure-blob-storage-using-polybase.md)