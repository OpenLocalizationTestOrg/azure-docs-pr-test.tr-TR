---
title: "Azure portalı: SQL veritabanı oluşturma | Microsoft Docs"
description: "Azure portalında SQL Veritabanı mantıksal sunucusu, sunucu düzeyi güvenlik duvarı kuralı ve veritabanı oluşturun ve sorgulayın."
keywords: "sql veritabanı öğreticisi, sql veritabanı oluşturma"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: Active
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: quickstart
ms.date: 01/10/2018
ms.author: ninarn
ms.openlocfilehash: e438613e3913eb88232c7b2a4b5280f6890f478e
ms.sourcegitcommit: 562a537ed9b96c9116c504738414e5d8c0fd53b1
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/12/2018
---
# <a name="create-an-azure-sql-database-in-the-azure-portal"></a>Azure portalında Azure SQL veritabanı oluşturma

Bu hızlı başlangıç öğreticisinde, Azure’da SQL veritabanı oluşturma adımlar gösterilmektedir. Azure SQL Veritabanı, bulutta yüksek oranda kullanılabilir SQL Server veritabanlarını çalıştırıp ölçeklendirmenize olanak tanıyan bir “Hizmet Olarak Veritabanı” teklifidir. Bu hızlı başlangıç, Azure portalını kullanarak bir SQL veritabanı oluşturma işlemini göstermektedir.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz](https://azure.microsoft.com/free/) bir hesap oluşturun.

## <a name="log-in-to-the-azure-portal"></a>Azure portalında oturum açma

[Azure Portal](https://portal.azure.com/)’da oturum açın.

## <a name="create-a-sql-database"></a>SQL veritabanı oluşturma

Azure SQL veritabanı bir dizi [işlem ve depolama kaynağı](sql-database-service-tiers.md) ile oluşturulur. Veritabanı bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) ve bir [Azure SQL Veritabanı mantıksal sunucusu](sql-database-features.md) içinde oluşturulur.

Adventure Works LT örnek verilerini içeren bir SQL veritabanı oluşturmak için bu adımları izleyin.

1. Azure portalının sol üst köşesinde bulunan **Yeni** düğmesine tıklayın.

2. **Yeni** penceresinden **Veritabanları**’nı seçin ve **Yeni** sayfasında **SQL Veritabanı** altından **Oluştur**’u seçin.

   ![create database-1](./media/sql-database-get-started-portal/create-database-1.png)

3. SQL Veritabanı formunu, önceki görüntüde gösterildiği gibi aşağıdaki bilgilerle doldurun:   

   | Ayar       | Önerilen değer | Açıklama |
   | ------------ | ------------------ | ------------------------------------------------- |
   | **Veritabanı adı** | mySampleDatabase | Geçerli veritabanı adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers). |
   | **Abonelik** | Aboneliğiniz  | Abonelikleriniz hakkında daha ayrıntılı bilgi için bkz. [Abonelikler](https://account.windowsazure.com/Subscriptions). |
   | **Kaynak grubu**  | myResourceGroup | Geçerli kaynak grubu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). |
   | **Kaynak seçme** | Örnek (AdventureWorksLT) | AdventureWorksLT şemasını ve verilerini yeni veritabanınıza yükler |

   > [!IMPORTANT]
   > Bu hızlı başlangıcın geri kalanında kullanılacağı için bu formdaki örnek veritabanını seçmeniz gerekir.
   >

4. **Sunucu** altında **Gerekli ayarları yapılandır**’a tıklayıp, aşağıdaki görüntüde gösterildiği gibi SQL sunucusu (mantıksal sunucu) formunu aşağıdaki bilgilerle doldurun:   

   | Ayar       | Önerilen değer | Açıklama |
   | ------------ | ------------------ | ------------------------------------------------- |
   | **Sunucu adı** | Genel olarak benzersiz bir ad | Geçerli sunucu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). |
   | **Sunucu yöneticisi oturum açma bilgileri** | Geçerli bir ad | Geçerli oturum açma adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers). |
   | **Parola** | Geçerli bir parola | Parolanızda en az 8 karakter bulunmalı ve parolanız şu üç kategoriden karakterler içermelidir: büyük harf karakterler, küçük harf karakterler, sayılar ve alfasayısal olmayan karakterler. |
   | **Abonelik** | Aboneliğiniz | Abonelikleriniz hakkında daha ayrıntılı bilgi için bkz. [Abonelikler](https://account.windowsazure.com/Subscriptions). |
   | **Kaynak grubu** | myResourceGroup | Geçerli kaynak grubu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). |
   | **Konum** | Geçerli bir konum | Bölgeler hakkında bilgi için bkz. [Azure Bölgeleri](https://azure.microsoft.com/regions/). |

   > [!IMPORTANT]
   > Burada belirttiğiniz sunucu yöneticisi kullanıcı adı ve parolası, bu hızlı başlangıcın sonraki bölümlerinde sunucuda ve veritabanlarında oturum açmak için gereklidir. Bu bilgileri daha sonra kullanmak üzere aklınızda tutun veya kaydedin.
   >  

   ![create database-server](./media/sql-database-get-started-portal/create-database-server.png)

5. Formu tamamladığınızda **Seç**’e tıklayın.

6. Hizmet katmanını, DTU'ların sayısını ve depolama alanı miktarını belirtmek için **Fiyatlandırma katmanı**’na tıklayın. Her hizmet katmanı için kullanılabilir DTU'lar ve depolama alanı miktarı seçeneklerini araştırın.

   > [!IMPORTANT]
   > \* Mevcut depolama alanından büyük depolama alanları önizleme aşamasındadır ve ek maliyetler uygulanır. Ayrıntılar için bkz. [SQL Veritabanı fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-database/).
   >
   >\* Premium katmanlarda 1 TB’den fazla depolama alanı şu bölgelerde sunulmaktadır: ABD Doğu2, Batı ABD, US Gov Virginia, Batı Avrupa, Almanya Orta, Güneydoğu Asya, Japonya Doğu, Avustralya Doğu, Kanada Orta ve Kanada Doğu. Bkz. [P11 P15 Geçerli Sınırlamalar](sql-database-resource-limits.md#single-database-limitations-of-p11-and-p15-when-the-maximum-size-greater-than-1-tb).  
   >

7. Bu hızlı başlangıç öğreticisi için **standart** hizmet katmanını seçip kaydırıcıyı kullanarak **100 DTU (S3)** ve **400** GB depolama alanını seçin.

   ![create database-s1](./media/sql-database-get-started-portal/create-database-s1.png)

8. **Ek Depolama** seçeneğini kullanmak için önizleme koşullarını kabul edin.

   > [!IMPORTANT]
   > \* Mevcut depolama alanından büyük depolama alanları önizleme aşamasındadır ve ek maliyetler uygulanır. Ayrıntılar için bkz. [SQL Veritabanı fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-database/).
   >
   >\* Premium katmanlarda 1 TB’den fazla depolama alanı şu bölgelerde sunulmaktadır: ABD Doğu2, Batı ABD, US Gov Virginia, Batı Avrupa, Almanya Orta, Güneydoğu Asya, Japonya Doğu, Avustralya Doğu, Kanada Orta ve Kanada Doğu. Bkz. [P11 P15 Geçerli Sınırlamalar](sql-database-resource-limits.md#single-database-limitations-of-p11-and-p15-when-the-maximum-size-greater-than-1-tb).  
   >

9. Sunucu katmanını, DTU'ların sayısını ve depolama alanı miktarını seçtikten sonra **Uygula**’ya tıklayın.  

10. SQL Veritabanı formunu tamamladıktan sonra veritabanını sağlamak için **Oluştur**’a tıklayın. Sağlama birkaç dakika sürer.

11. Araç çubuğunda **Bildirimler**’e tıklayarak dağıtım işlemini izleyin.

     ![bildirim](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a>Sunucu düzeyinde bir güvenlik duvarı kuralı oluşturma

SQL Veritabanı hizmeti, güvenlik duvarını belirli IP adreslerine açmaya yönelik bir güvenlik duvarı kuralı oluşturulmadıkça, dış uygulama ve araçların sunucuya ya da sunucu üzerindeki herhangi bir veritabanına bağlanmasını engelleyen sunucu düzeyinde bir güvenlik duvarı kuralı oluşturur. SQL Veritabanı güvenlik duvarı üzerinden yalnızca IP adresinize yönelik dış bağlantıları etkinleştirmek üzere istemcinizin IP adresi için bir [SQL Veritabanı sunucu düzeyi güvenlik duvarı kuralı](sql-database-firewall-configure.md) oluşturmak için bu adımları izleyin.

> [!NOTE]
> SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar. Bir kurumsal ağ içerisinden bağlanmaya çalışıyorsanız, ağınızın güvenlik duvarı tarafından 1433 numaralı bağlantı noktası üzerinden giden trafiğe izin verilmiyor olabilir. Bu durumda BT departmanınız 1433 numaralı bağlantı noktasını açmadığı sürece Azure SQL Veritabanı sunucunuza bağlanamazsınız.
>

1. Dağıtım tamamlandıktan sonra, soldaki menüden **SQL veritabanları**'na ve ardından **SQL veritabanları** sayfasında **mySampleDatabase** öğesine tıklayın. Veritabanınıza ilişkin genel bakış sayfası açılır ve tam sunucu adı (örneğin, **mynewserver-20170824.database.windows.net**) görüntülenerek daha fazla yapılandırma seçeneği sunulur.

2. Sonraki hızlı başlangıçlarda sunucunuza ve veritabanlarına bağlanmak için bu tam sunucu adını kopyalayın.

   ![sunucu adı](./media/sql-database-get-started-portal/server-name.png)

3. Önceki görüntüde gösterildiği gibi araç çubuğundaki **sunucu güvenlik duvarı ayarla** öğesine tıklayın. SQL Veritabanı sunucusu için **Güvenlik duvarı ayarları** sayfası açılır.

   ![sunucu güvenlik duvarı kuralı](./media/sql-database-get-started-portal/server-firewall-rule.png)

4. Geçerli IP adresinizi yeni bir güvenlik duvarı kuralına eklemek için araç çubuğunda **İstemci IP’si Ekle** öğesine tıklayın. Güvenlik duvarı kuralı, 1433 numaralı bağlantı noktasını tek bir IP adresi veya bir IP adresi aralığı için açabilir.

5. **Kaydet**’e tıklayın. Geçerli IP adresiniz için mantıksal sunucuda 1433 numaralı bağlantı noktası açılarak sunucu düzeyinde güvenlik duvarı kuralı oluşturulur.

6. **Tamam**’a tıklayın ve sonra **Güvenlik duvarı ayarları** sayfasını kapatın.

Artık SQL Server Management Studio’yu veya seçtiğiniz başka bir aracı kullanarak, daha önce oluşturduğunuz sunucu yöneticisi hesabıyla bu IP adresinden SQL Veritabanı sunucusuna ve sunucuya ait veritabanlarına bağlanabilirsiniz.

> [!IMPORTANT]
> Varsayılan olarak, SQL Veritabanı güvenlik duvarı üzerinden erişim tüm Azure hizmetleri için etkindir. Tüm Azure hizmetleri için devre dışı bırakmak isterseniz bu sayfadaki **KAPALI** öğesine tıklayın.
>

## <a name="query-the-sql-database"></a>SQL veritabanını sorgulama

Azure’da bir örnek veritabanı oluşturduktan sonra, veritabanına bağlanabildiğinizi ve verileri sorgulayabildiğinizi onaylamak üzere Azure portalındaki yerleşik sorgu aracını kullanın.

1. Veritabanınızın SQL Veritabanı sayfasında, soldaki menüden **Veri gezgini (önizleme)** öğesini bulup tıklayın

   ![sorgu düzenleyicisini bulma](./media/sql-database-get-started-portal/find-query-editor.PNG)

2. Sunucu yöneticisi oturum açma bilgileri ve daha önce oluşturduğunuz parola ile SQL server kimlik doğrulaması kullanarak oturum açmak için **Oturum aç**’a tıklayın, oturum açma bilgilerini gözden geçirin ve ardından **Tamam**’a tıklayın.

   ![oturum açma](./media/sql-database-get-started-portal/login-menu.png)

3. Oturum açmak için **Tamam**’a tıklayın.

4. **ServerAdmin** olarak kimlik doğrulaması yaptıktan sonra sorgu düzenleyici bölmesine aşağıdaki sorguyu yazın.

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

5. **Çalıştır**’a tıklayın ve **Sonuçlar** bölmesindeki sorgu sonuçlarını gözden geçirin.

   ![sorgu düzenleyicisi sonuçları](./media/sql-database-get-started-portal/query-editor-results.png)

6. **Veri gezgini** sayfasını kapatın, kaydedilmemiş düzenlemelerinizi iptal etmek için **Tamam**’a tıklayın.

## <a name="clean-up-resources"></a>Kaynakları temizleme

[Sonraki adımlar](#next-steps)’a geçip farklı yöntemler kullanarak veritabanını sorgulama hakkında bilgi edinmek istiyorsanız bu kaynakları kaydedin. Bu hızlı başlangıç bölümünde oluşturduğunuz kaynakları silmek isterseniz, aşağıdaki adımları kullanın.


1. Azure portalında sol taraftaki menüden, **Kaynak grupları**’na tıklayın ve ardından **myResourceGroup**’a tıklayın.
2. Kaynak grubu sayfanızda, **Sil**’e tıklayın, metin kutusuna **myResourceGroup** yazın ve ardından **Sil**’e tıklayın.

## <a name="next-steps"></a>Sonraki adımlar

Artık bir veritabanınız olduğuna göre, sık kullandığınız araçlarla bağlanabilir ve sorgulayabilirsiniz. Aşağıdan aracınızı seçerek daha fazla bilgi edinin:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)
