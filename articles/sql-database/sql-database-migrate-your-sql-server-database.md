---
title: "SQL Server DB Azure SQL veritabanına geçirme | Microsoft Docs"
description: "SQL Server veritabanını Azure SQL veritabanına geçirme öğrenin."
services: sql-database
documentationcenter: 
author: janeng
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/27/2017
ms.author: janeng
ms.openlocfilehash: 375d3ea0230e7d3fd0fc02ca7e0b8a7a76c24a27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-sql-server-database-to-azure-sql-database"></a>SQL Server veritabanını Azure SQL veritabanına geçirme

Azure SQL veritabanı, SQL Server veritabanınızın üç bölümden oluşan bir işlemdir - ilk hazırlama taşıma, ardından dışarı aktarın ve veritabanı içeri aktarın. Bu öğreticide, öğrenin:

> [!div class="checklist"]
> * Azure SQL veritabanı kullanarak geçiş için bir SQL Server veritabanında hazırlama [veri geçiş Yardımcısı](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)
> * Veritabanını bir BACPAC dosyasına dışarı aktarma
> * Bir Azure SQL veritabanına BACPAC dosyasını içeri aktar

Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticiyi tamamlamak için aşağıdaki ön koşulların karşılandığından emin olun:

- En son sürümü yüklü [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). SSMS yükleme SQLPackage, bir dizi veritabanı geliştirme görevlerini otomatikleştirmek için kullanılan bir komut satırı yardımcı programı en yeni sürümünü yükler. 
- Yüklü [veri geçiş Yardımcısı](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).
- Tanımladınız ve geçirmek için bir veritabanı erişimi. Bu öğretici kullanır [SQL Server 2008R2 AdventureWorks OLTP veritabanını](https://msftdbprodsamples.codeplex.com/releases/view/59211) örneğindeki SQL Server 2008R2 ya da daha yeni, ancak siz tercih ettiğiniz herhangi bir veritabanını kullanabilirsiniz. Uyumluluk sorunlarını gidermek için kullanmak [SQL Server veri araçları](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)

## <a name="prepare-for-migration"></a>Geçiş için hazırlama

Geçişe hazırlanmak hazır olursunuz. Kullanmak için aşağıdaki adımları izleyin  **[veri geçiş Yardımcısı](https://www.microsoft.com/download/details.aspx?id=53595)**  veritabanınız Azure SQL veritabanı geçiş için hazır olup olmadığını değerlendirmek için.

1. Açık **veri geçiş Yardımcısı**. Herhangi bir bilgisayarda, geçirmeyi planladığınız veritabanını içeren SQL Server örneği ile bağlantı DMA çalıştırabilir, SQL Server örneğini barındıran bilgisayara yüklemeniz gerekmez.

     ![açık veri geçiş Yardımcısı](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. Sol menüde tıklatın **+ yeni** oluşturmak için bir **değerlendirme** projesi. Formu doldurun bir **proje adı** (diğer tüm değerler varsayılan değerlerinde bırakılmalıdır) tıklatıp **oluşturma**. **Seçenekleri** sayfası açılır.

     ![Yeni veri geçiş Yardımcısı projesi](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. Üzerinde **seçenekleri** sayfasında, **sonraki**. **Seçin kaynakları** sayfası açılır.

     ![Yeni veri geçiş seçenekleri](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. Üzerinde **seçin kaynakları** sayfasında, geçirmeyi planladığınız sunucunun içeren SQL Server örneğinin adını girin. Bu sayfadaki diğer değerler, gerekirse değiştirin. **Bağlan**'a tıklayın.

     ![Yeni veri geçiş select kaynakları](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. İçinde **ekleme kaynakları** kısmı **seçin kaynakları** sayfasında, uyumluluk için sınanacak veritabanları için onay kutularını seçin. **Ekle**'ye tıklayın.

     ![Yeni veri geçiş select kaynakları](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. Tıklatın **Başlat değerlendirme**.

     ![Yeni veri geçiş başlangıç değerlendirme](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. Değerlendirme tamamlandığında veritabanı geçirmek için yeterince uyumlu olup olmadığını görmek için ilk bakın. Yeşil bir daire onay işaretine arayın.

     ![Yeni veri geçiş değerlendirme sonuçlarını uyumlu](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. Sonuçları gözden geçirin. **SQL Server özellik eşliği** gösterilen sonucu olan varsayılan sonuçlarını gözden geçirin. Özellikle desteklenmeyen ve kısmen desteklenen özellikler hakkında bilgi ve önerilen eylemler hakkında sağlanan bilgileri gözden geçirin. 

     ![Yeni veri geçiş değerlendirme eşlik](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. Gözden geçirme **uyumluluk sorunları** bu seçeneği sol üst köşedeki tıklatarak. Özellikle geçiş blockers, davranış değişiklikleri ve her uyumluluk düzeyi için kullanım dışı özellikler hakkındaki bilgileri gözden geçirin. AdventureWorks2008R2 veritabanı için SQL Server 2000'den itibaren SQL Server 2008 ve SERVERPROPERTY('LCID') değişiklikleri itibaren tam metin araması değişiklikleri gözden geçirin. Bu değişiklikler hakkında daha fazla bilgi için daha fazla bilgi için bağlantılar sağlanır. Birçok seçenekleri arayın ve tam metin araması için ayarları değiştirdiniz 

   > [!IMPORTANT] 
   > Azure SQL veritabanına veritabanınızı geçirdikten sonra veritabanını geçerli uyumluluk düzeyinde (düzey 100 AdventureWorks2008R2 veritabanı için) veya daha yüksek düzeyde çalışmaya seçebilirsiniz. Uygulamaları ve belirli bir uyumluluk düzeyinde bir veritabanı işletim seçenekleri hakkında daha fazla bilgi için bkz: [ALTER veritabanı uyumluluk düzeyi](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Ayrıca bkz. [ALTER veritabanı kapsamlı yapılandırma](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) Uyumluluk Düzeyleri ilgili ek veritabanı düzeyi ayarları hakkında bilgi için.
   >

10. İsteğe bağlı olarak, tıklayın **verme rapor** raporu bir JSON dosyası olarak kaydetmek için.
11. Veri geçiş Yardımcısı'nı kapatın.

## <a name="export-to-bacpac-file"></a>BACPAC dosyasına dışarı aktarma 

ZIP dosyası meta verileri ve SQL Server veritabanından veri içeren BACPAC uzantılı bir BACPAC dosyasıdır. Bir BACPAC dosyayı Azure blob depolama veya geçiş - veya arşivleme için yerel depolama gibi SQL Server'dan Azure SQL veritabanına depolanabilir. Bir verme işlemsel olarak tutarlı olmasını ya da hiçbir yazma emin olmalısınız etkinlik dışa aktarma sırasında gerçekleşen.

Yerel depolama alanına AdventureWorks2008R2 veritabanını dışarı aktarma SQLPackage komut satırı yardımcı programını kullanmak için aşağıdaki adımları izleyin.

1. Bir Windows komut istemi açın ve sahip olduğunuz bir klasöre dizininize değiştirin **130** sürüm SQLPackage, - gibi **C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin**.

2. Dışarı aktarmak için komut isteminde aşağıdaki SQLPackage komutu yürütün **AdventureWorks2008R2** veritabanını **localhost** için **AdventureWorks2008R2.bacpac**. Bu değerleri ortamınıza uygun şekilde değiştirin.

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![sqlpackage dışarı aktarma](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

Yürütme tamamlandıktan sonra oluşturulan BACPAC dosyası yürütülebilir sqlpackage bulunduğu dizinde depolanır. Bu örnekte, C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin. 

## <a name="log-in-to-the-azure-portal"></a>Azure portalında oturum açma

[Azure Portal](https://portal.azure.com/)’da oturum açın. SQLPackage komut satırı yardımcı programını çalıştırdığınız bilgisayarda oturum açma güvenlik duvarı kuralı oluşturma 5. adımda kolaylaştırır.

## <a name="create-a-sql-server-logical-server"></a>Bir SQL server mantıksal sunucusu oluşturma

A [SQL server mantıksal sunucu](sql-database-features.md) birden fazla veritabanı için merkezi bir yönetim noktası işlevi görür. Geçirilen Adventure Works OLTP SQL Server veritabanını içeren bir SQL server mantıksal sunucu oluşturmak için aşağıdaki adımları izleyin. 

1. Azure portalının sol üst köşesinde bulunan **Yeni** düğmesine tıklayın.

2. Tür **sql server** arama penceresinde **yeni** sayfasında ve seçin **SQL veritabanı (mantıksal sunucu)** filtre uygulanmış listeden.

    ![mantıksal sunucu seçme](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. Üzerinde **her şeyi** sayfasında, **SQL server (mantıksal sunucu)** ve ardından **oluşturma** üzerinde **SQL Server (mantıksal sunucu)** sayfası.

    ![mantıksal sunucusu oluşturma](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. SQL sunucusu (mantıksal sunucu) formunu, önceki görüntüde gösterildiği gibi aşağıdaki bilgilerle doldurun:     

   | Ayar       | Önerilen değer | Açıklama | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Sunucu adı** | Genel olarak benzersiz bir ad girin | Geçerli sunucu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). | 
   | **Sunucu yöneticisi oturum açma bilgileri** | Geçerli bir ad girin | Geçerli oturum açma adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers). |
   | **Parola** | Geçerli bir parola girin | Parolanız en az 8 karakter olmalı ve aşağıdaki kategoriden üçünden karakterler içermelidir: büyük harf karakterler, küçük harfler, sayılar ve alfasayısal olmayan karakter. |
   | **Abonelik** | Abonelik seçin | Abonelikleriniz hakkında daha ayrıntılı bilgi için bkz. [Abonelikler](https://account.windowsazure.com/Subscriptions). |
   | **Kaynak grubu** | Varolan bir kaynak grubu seçin veya yeni bir grup oluşturun **myResourceGroup** |  Geçerli kaynak grubu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). |
   | **Konum** | Yeni sunucu için geçerli bir konum girin | Bölgeler hakkında bilgi için bkz. [Azure Bölgeleri](https://azure.microsoft.com/regions/). |

   ![mantıksal sunucu tamamlandı formu oluşturma](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. Tıklatın **oluşturma** mantıksal sunucusu sağlamak için. Sağlama birkaç dakika sürer. 

> [!IMPORTANT]
> Sunucu adı, Sunucu Yöneticisi oturum açma adı ve parola unutmayın. Bu öğreticide daha sonra bu değerler gerekir.
>

## <a name="create-a-server-level-firewall-rule"></a>Sunucu düzeyinde bir güvenlik duvarı kuralı oluşturma

SQL veritabanı hizmetinin oluşturur bir [sunucu düzeyinde güvenlik duvarı](sql-database-firewall-configure.md) engelleyen harici uygulamalar ve araçlar için Güvenlik Duvarı'nı açmak için bir güvenlik duvarı kuralı yapılandırılmadığı sürece sunucu veya sunucu üzerindeki herhangi bir veritabanına bağlanmasını Belirli IP adresleri. SQLPackage komut satırı yardımcı programını çalıştırdığınız bilgisayarın IP adresi için bir SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı oluşturmak için aşağıdaki adımları izleyin. Bu, Azure SQL veritabanı güvenlik duvarı üzerinden SQL serverDatabase mantıksal sunucusuna bağlanmak SQLPackage sağlar. 

1. Tıklatın **tüm kaynakları** sol menüden ve yeni sunucunuzu tıklayın **tüm kaynakları** sayfa. Sunucunuz için genel bakış sayfası açılır ve ek yapılandırma seçeneklerini sağlar.

     ![mantıksal sunucusuna genel bakış](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Tıklatın **Güvenlik Duvarı** altında sol menüde **ayarları** genel bakış sayfasında. SQL Veritabanı sunucusu için **Güvenlik duvarı ayarları** sayfası açılır. 

3. Tıklatın **istemci IP'si Ekle** bilgisayarın IP adresi eklemek için araç çubuğundaki kullanmakta olduğunuz ve ardından **kaydetmek**. Bu IP adresi için bir sunucu düzeyinde güvenlik duvarı kuralı oluşturulur.

     ![sunucu güvenlik duvarı kuralı ayarla](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. **Tamam** düğmesine tıklayın.

SQL Server Management Studio veya önceden oluşturulmuş sunucu yönetici hesabı kullanarak bu IP adresinden tercih ettiğiniz başka bir araç kullanarak bu sunucudaki tüm veritabanları artık bağlanabilir.

> [!NOTE]
> SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar. Bir kurumsal ağ içerisinden bağlanmaya çalışıyorsanız, ağınızın güvenlik duvarı tarafından 1433 numaralı bağlantı noktası üzerinden giden trafiğe izin verilmiyor olabilir. Bu durumda BT departmanınız 1433 numaralı bağlantı noktasını açmadığı sürece Azure SQL Veritabanı sunucunuza bağlanamazsınız.
>

## <a name="import-a-bacpac-file-to-azure-sql-database"></a>Azure SQL veritabanı için bir BACPAC dosyasını içeri aktarın 

Azure SQL veritabanını belirtilen bir oluşturmak için en yeni sürümlerin SQLPackage komut satırı yardımcı programının desteği sağlamak [Hizmet katmanını ve performans düzeyini](sql-database-service-tiers.md). En iyi performans için içeri aktarma işlemi sırasında yüksek Hizmet katmanını ve performans düzeyini seçin ve Hizmet katmanını ve performans düzeyini hemen gerekenden daha yüksek olması durumunda içeri aktarma işleminden sonra ölçeklendirmeyi azaltın.

Bu adımları kullanma AdventureWorks2008R2 veritabanını Azure SQL veritabanı için içeri aktarma SQLPackage komut satırı yardımcı programını izleyin. Bu görev için SQL Server Management Studio'yu kullanabilirsiniz, ancak SQLPackage en fazla esneklik ve en iyi performans için birçok üretim ortamları için tercih edilen yöntemdir. Bkz: [BACPAC dosyalarını kullanarak Azure SQL veritabanı için SQL Server'dan geçirme](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

- İçeri aktarmak için komut isteminde aşağıdaki SQLPackage komutu yürütme **AdventureWorks2008R2** yerel depolama veritabanına yeni bir veritabanı, bir hizmet katmanı ,dahaönceoluşturduğunuzSQLservermantıksalsunucu **Premium**ve bir hizmet amacını **P6**. SQL server mantıksal sunucunuz için uygun değerlerle köşeli değerleri değiştirin ve yeni veritabanı için bir ad belirtin (Ayrıca köşeli değiştirin). Veritabanı sürümü ve hizmet objectgive ortamınıza uygun şekilde değerlerini değiştirmek seçebilirsiniz. Bu öğreticinin amaçları doğrultusunda, yükseltilen veritabanının adı **myMigratedDatabase**.

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![sqlpackage alma](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Bir SQL server mantıksal sunucusu 1433 bağlantı noktasını dinler. Bir SQL server mantıksal Sunucusu'ndan kurumsal bir güvenlik duvarı içinde bağlanmaya çalışıyorsanız, bu bağlantı noktası, başarılı bir şekilde bağlanmak Kurumsal Güvenlik Duvarı'nda açık olması gerekir.
>

## <a name="connect-using-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) kullanarak bağlan

Geçirilen adlı veritabanı, Azure SQL veritabanı sunucunuzun ve yeni bir bağlantı kurmak için SQL Server Management Studio kullanın **myMigratedDatabase** bu öğreticideki. SQL Server Management Studio SQLPackage çalıştırıldığı farklı bir bilgisayarda çalıştırıyorsanız, önceki yordamdaki adımları kullanarak bu bilgisayar için bir güvenlik duvarı kuralı oluşturun.

1. SQL Server Management Studio’yu açın.

2. **Sunucuya Bağlan** iletişim kutusuna şu bilgileri girin:
   - **Sunucu türü**: Veritabanı altyapısını belirtin
   - **Sunucu adı**: tam sunucu adınızı girin **mynewserver20170403.database.windows.net**
   - **Kimlik doğrulama**: SQL Server Kimlik Doğrulaması belirtin
   - **Kullanıcı adı**: Sunucu yöneticisi hesabınızı girin
   - **Parola**: Sunucu yöneticisi hesabınızın parolasını girin
 
    ![SSMS ile bağlanma](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. **Bağlan**'a tıklayın. Nesne Gezgini penceresi açılır. 

4. Nesne Gezgini'nde genişletin **veritabanları** genişletin ve ardından **myMigratedDatabase** örnek veritabanında nesneleri görüntülemek için.

## <a name="change-database-properties"></a>Veritabanı özelliklerini değiştir

Hizmet katmanı, performans düzeyi ve SQL Server Management Studio'yu kullanarak uyumluluk düzeyini değiştirebilirsiniz. İçeri aktarma aşaması sırasında en iyi performans için daha yüksek bir performans katmanı veritabanına aktarmak, ancak içeri aktarılan veritabanını etkin olarak kullanmaya hazır olana kadar tasarruf için alma işlemi tamamlandıktan sonra ölçeklendirmenizi öneririz. Uyumluluk düzeyinin değiştirilmesi, daha iyi performans ve Azure SQL veritabanı hizmetinin en yeni özelliklere erişim elde etmek. Eski bir veritabanını geçirdiğinizde, veritabanı uyumluluk düzeyi düzeyinde içeri aktarılmakta olan veritabanı ile uyumlu olan en düşük desteklenen korunur. Daha fazla bilgi için bkz: [iyileştirilmiş sorgu performansı ile Azure SQL veritabanı uyumluluk düzeyi 130](sql-database-compatibility-level-query-performance-130.md).

1. Nesne Gezgini'nde sağ **myMigratedDatabase** tıklatıp **yeni sorgu**. Veritabanına bağlı bir sorgu penceresi açılır.

2. Hizmet katmanı ayarlamak için aşağıdaki komutu yürütün **standart** ve performans düzeyine **S1**.

    ```
    ALTER DATABASE myMigratedDatabase 
    MODIFY 
        (
        EDITION = 'Standard'
        , MAXSIZE = 250 GB
        , SERVICE_OBJECTIVE = 'S1'
    );
    ```

    ![Hizmet katmanını değiştirebilirsiniz](./media/sql-database-migrate-your-sql-server-database/service-tier.png)

3. Veritabanı uyumluluk düzeyini değiştirmek için aşağıdaki komutu yürütün **130**.

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![uyumluluk düzeyini değiştirme](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a>Sonraki adımlar 
Bu öğreticide dışarı ve veritabanınızı içe hazır. İçin öğrenilen:

> [!div class="checklist"]
> * Bir SQL Server veritabanında Azure SQL veritabanı geçiş için hazırlama
> * Veritabanını bir BACPAC dosyasına dışarı aktarma
> * Bir Azure SQL veritabanına BACPAC dosyasını içeri aktar

Veritabanınızın güvenliğini sağlamak öğrenmek için sonraki öğretici ilerleyin.

> [!div class="nextstepaction"]
> [Azure SQL veritabanınızı güvenli](sql-database-security-tutorial.md).


