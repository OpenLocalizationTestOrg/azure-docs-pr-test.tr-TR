---
title: "aaaMigrate SQL Server DB tooAzure SQL veritabanı | Microsoft Docs"
description: "SQL Server veritabanı tooAzure SQL veritabanı toomigrate öğrenin."
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
ms.openlocfilehash: d10ad1d26576194f1dd6858bae5c3e7c1ec4fb91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-server-database-tooazure-sql-database"></a>SQL Server veritabanı tooAzure SQL veritabanına geçirme

SQL Server'ınızdaki taşıma veritabanı tooAzure SQL veritabanı üç bölümden oluşan bir işlemdir - önce hazırlayın, sonra dışarı aktarma ve hello veritabanı içeri aktarın. Bu öğreticide, öğrenin:

> [!div class="checklist"]
> * Geçiş tooAzure SQL veritabanı için SQL Server veritabanında hazırlama hello kullanarak [veri geçiş Yardımcısı](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)
> * Merhaba veritabanı tooa BACPAC dosyası dışarı aktarma
> * Bir Azure SQL veritabanına Hello BACPAC dosyası

Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.

## <a name="prerequisites"></a>Ön koşullar

Bu öğretici, Önkoşullar aşağıdaki yapma emin hello tamamlanır toocomplete:

- Yüklü hello en yeni sürümünü [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). SSMS yükleme hello SQLPackage, kullanılan tooautomate veritabanı geliştirme görevleri bir dizi olabilecek bir komut satırı yardımcı programını en yeni sürümünü yükler. 
- Yüklü hello [veri geçiş Yardımcısı](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).
- Tanımladınız ve erişim tooa veritabanı toomigrate sahip. Bu öğretici hello kullanır [SQL Server 2008R2 AdventureWorks OLTP veritabanını](https://msftdbprodsamples.codeplex.com/releases/view/59211) örneğindeki SQL Server 2008R2 ya da daha yeni, ancak siz tercih ettiğiniz herhangi bir veritabanını kullanabilirsiniz. toofix uyumluluk sorunları kullanmak [SQL Server veri araçları](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)

## <a name="prepare-for-migration"></a>Geçiş için hazırlama

Geçiş için hazır tooprepare var. Bu adımları toouse hello izleyin  **[veri geçiş Yardımcısı](https://www.microsoft.com/download/details.aspx?id=53595)**  tooassess hello veritabanınız geçiş tooAzure SQL veritabanı için hazır olup olmadığı.

1. Açık hello **veri geçiş Yardımcısı**. DMA veritabanıyla bağlantı toohello SQL Server örneği içeren hello herhangi bir bilgisayarda çalıştırabilirsiniz toomigrate planlama, SQL Server örneği hello barındıran bilgisayar üzerinde hello tooinstall gerekmez.

     ![açık veri geçiş Yardımcısı](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. Merhaba sol menüde tıklatın **+ yeni** toocreate bir **değerlendirme** projesi. Merhaba formu doldurun bir **proje adı** (diğer tüm değerler varsayılan değerlerinde bırakılmalıdır) tıklatıp **oluşturma**. Merhaba **seçenekleri** sayfası açılır.

     ![Yeni veri geçiş Yardımcısı projesi](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. Merhaba üzerinde **seçenekleri** sayfasında, **sonraki**. Merhaba **seçin kaynakları** sayfası açılır.

     ![Yeni veri geçiş seçenekleri](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. Merhaba üzerinde **seçin kaynakları** sayfasında, hello toomigrate planladığınız hello sunucuyu içeren SQL Server örneğinin adını girin. Değişiklik gerekiyorsa bu sayfadaki diğer değerleri hello. **Bağlan**'a tıklayın.

     ![Yeni veri geçiş select kaynakları](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. Merhaba, **ekleme kaynakları** hello kısmı **kaynakları seçin** sayfasında, uyumluluk için test hello veritabanları toobe hello onay kutularını seçin. **Ekle**'ye tıklayın.

     ![Yeni veri geçiş select kaynakları](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. Tıklatın **Başlat değerlendirme**.

     ![Yeni veri geçiş başlangıç değerlendirme](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. İlk Hello değerlendirme tamamlandığında hello veritabanı yeterince uyumlu toomigrate ise toosee bakın. Yeşil bir daire hello onay işaretine arayın.

     ![Yeni veri geçiş değerlendirme sonuçlarını uyumlu](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. Merhaba sonuçlarını gözden geçirin. Merhaba **SQL Server özellik eşliği** gösterilen sonuçları hello varsayılan sonuçları tooreview olur. Özellikle hello desteklenmeyen ve kısmen desteklenen özellikler hakkında bilgi ve önerilen eylemler hakkındaki hello sağlanan bilgileri gözden geçirin. 

     ![Yeni veri geçiş değerlendirme eşlik](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. Gözden geçirme hello **uyumluluk sorunları** bu seçeneği hello üst sol tıklatarak. Özellikle gözden geçirme geçiş blockers, davranış değişiklikleri hakkında bilgi hello ve kullanım dışı özellikler her uyumluluk düzeyi. Merhaba AdventureWorks2008R2 veritabanı için hello yapılan değişiklikleri gözden geçirmeleri SQL Server 2008 ve hello itibaren tooFull metin araması, SQL Server 2000'den itibaren tooSERVERPROPERTY('LCID') değiştirir. Bu değişiklikler hakkında daha fazla bilgi için daha fazla bilgi için bağlantılar sağlanır. Birçok seçenekleri arayın ve tam metin araması için ayarları değiştirdiniz 

   > [!IMPORTANT] 
   > SQL veritabanı, veritabanı tooAzure geçirdikten sonra geçerli uyumluluk düzeyinde (düzey 100 hello AdventureWorks2008R2 veritabanı için) veya daha yüksek düzeyde toooperate hello veritabanı seçebilirsiniz. Merhaba etkileri ve belirli bir uyumluluk düzeyinde bir veritabanı işletim seçenekleri hakkında daha fazla bilgi için bkz: [ALTER veritabanı uyumluluk düzeyi](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Ayrıca bkz. [ALTER veritabanı kapsamlı yapılandırma](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) toocompatibility düzeyleri ek veritabanı düzeyi ayarları hakkında bilgi için ilgili.
   >

10. İsteğe bağlı olarak, tıklayın **verme rapor** toosave hello rapor bir JSON dosyası olarak.
11. Veri geçiş Yardımcısı'nı Kapat hello.

## <a name="export-toobacpac-file"></a>Dışarı aktarma tooBACPAC dosyası 

ZIP dosyası BACPAC hello meta verileri ve SQL Server veritabanından veri içeren bir uzantıya sahip bir BACPAC dosyasıdır. Bir BACPAC dosyayı Azure blob depolama veya geçiş - veya arşivleme için yerel depolama gibi SQL Server tooAzure SQL veritabanı ' depolanabilir. İşlemsel olarak tutarlı bir verme toobe için ya da hiçbir yazma emin olmalısınız etkinlik hello dışa aktarma sırasında gerçekleşen.

Bu adımları toouse hello SQLPackage komut satırı yardımcı programını tooexport hello AdventureWorks2008R2 veritabanı toolocal depolama izleyin.

1. Bir Windows komut istemi açın ve hello sahip dizin tooa klasörünüzü değiştirmek **130** sürüm SQLPackage, - gibi **C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin**.

2. Merhaba komut istemi tooexport hello SQLPackage komutunda aşağıdaki hello yürütme **AdventureWorks2008R2** veritabanını **localhost** çok**AdventureWorks2008R2.bacpac**. Bu değerleri uygun tooyour ortamı olarak değiştirin.

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![sqlpackage dışarı aktarma](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

Merhaba yürütme tamamlandıktan sonra oluşturulan hello BACPAC dosya hello sqlpackage yürütülebilir bulunduğu hello dizininde depolanır. Bu örnekte, C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin. 

## <a name="log-in-toohello-azure-portal"></a>Toohello Azure portalında oturum açın

İçinde toohello oturum [Azure portal](https://portal.azure.com/). Merhaba SQLPackage komut satırı yardımcı programını çalıştırdığınız hello bilgisayardan oturum 5. adımda hello güvenlik duvarı kuralı hello oluşturulmasını kolaylaştırır.

## <a name="create-a-sql-server-logical-server"></a>Bir SQL server mantıksal sunucusu oluşturma

A [SQL server mantıksal sunucu](sql-database-features.md) birden fazla veritabanı için merkezi bir yönetim noktası işlevi görür. Bu adımları toocreate bir SQL server mantıksal sunucu toocontain hello geçirilen Adventure Works OLTP SQL Server veritabanı. 

1. Merhaba tıklatın **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.

2. Tür **sql server** hello arama penceresinde hello **yeni** sayfasında ve seçin **SQL veritabanı (mantıksal sunucu)** hello listesi filtrelenir.

    ![mantıksal sunucu seçme](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. Merhaba üzerinde **her şeyi** sayfasında, **SQL server (mantıksal sunucu)** ve ardından **oluşturma** hello üzerinde **SQL Server (mantıksal sunucu)** sayfası .

    ![mantıksal sunucusu oluşturma](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. Merhaba SQL server (mantıksal sunucu) form görüntüsü önceki hello üzerinde gösterildiği gibi bilgileri, aşağıdaki hello ile doldurun:     

   | Ayar       | Önerilen değer | Açıklama | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Sunucu adı** | Genel olarak benzersiz bir ad girin | Geçerli sunucu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). | 
   | **Sunucu yöneticisi oturum açma bilgileri** | Geçerli bir ad girin | Geçerli oturum açma adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers). |
   | **Parola** | Geçerli bir parola girin | Parolanız en az 8 karakter olmalı ve kategorileri aşağıdaki hello üçünden karakterler içermelidir: büyük harf karakterler, küçük harfler, sayılar ve alfasayısal olmayan karakter. |
   | **Abonelik** | Abonelik seçin | Abonelikleriniz hakkında daha ayrıntılı bilgi için bkz. [Abonelikler](https://account.windowsazure.com/Subscriptions). |
   | **Kaynak grubu** | Varolan bir kaynak grubu seçin veya yeni bir grup oluşturun **myResourceGroup** |  Geçerli kaynak grubu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). |
   | **Konum** | Merhaba yeni sunucu için geçerli bir konum girin | Bölgeler hakkında bilgi için bkz. [Azure Bölgeleri](https://azure.microsoft.com/regions/). |

   ![mantıksal sunucu tamamlandı formu oluşturma](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. Tıklatın **oluşturma** tooprovision hello mantıksal sunucu. Sağlama birkaç dakika sürer. 

> [!IMPORTANT]
> Sunucu adı, Sunucu Yöneticisi oturum açma adı ve parola unutmayın. Bu öğreticide daha sonra bu değerler gerekir.
>

## <a name="create-a-server-level-firewall-rule"></a>Sunucu düzeyinde bir güvenlik duvarı kuralı oluşturma

SQL veritabanı hizmetinin Hello oluşturur bir [hello sunucu düzeyinde güvenlik duvarı](sql-database-firewall-configure.md) engelleyen harici uygulamalar ve Araçlar bir güvenlik duvarı kuralı tooopen hello yapılandırılmadığı sürece toohello sunucu veya hello sunucu üzerindeki herhangi bir veritabanına bağlanmanızı Belirli IP adresleri için güvenlik duvarı. Bu adımları toocreate hello SQLPackage komut satırı yardımcı programını çalıştırdığınız hello bilgisayarın hello IP adresi için bir SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı izleyin. Bu SQLPackage tooconnect toohello SQL serverDatabase mantıksal sunucunun hello Azure SQL veritabanı güvenlik duvarı üzerinden sağlar. 

1. ' I tıklatın **tüm kaynakları** hello sol menüden yeni hello sunucunuzda tıklatıp **tüm kaynakları** sayfası. Sunucunuz için Hello genel bakış sayfası açılır ve ek yapılandırma seçeneklerini sağlar.

     ![mantıksal sunucusuna genel bakış](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Tıklatın **Güvenlik Duvarı** altında hello sol menüde **ayarları** hello genel bakış sayfasında. Merhaba **Güvenlik Duvarı ayarları** hello SQL veritabanı sunucusu sayfasını açar. 

3. Tıklatın **istemci IP'si Ekle** hello bilgisayarın hello araç tooadd hello IP adresine kullanmakta olduğunuz ve ardından **kaydetmek**. Bu IP adresi için bir sunucu düzeyinde güvenlik duvarı kuralı oluşturulur.

     ![sunucu güvenlik duvarı kuralı ayarla](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. **Tamam** düğmesine tıklayın.

Şimdi tooall veritabanlarını SQL Server Management Studio veya bu IP adresinden daha önce oluşturulmuş hello server yönetici hesabı kullanarak tercih ettiğiniz başka bir araç kullanarak bu sunucuya bağlanabilirsiniz.

> [!NOTE]
> SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar. Bir şirket ağından gelen tooconnect çalışıyorsanız, bağlantı noktası 1433 üzerinden giden trafik, ağınızın güvenlik duvarı tarafından izin verilmiyor. BT departmanınız 1433 numaralı bağlantı noktasını açar sürece bu durumda, tooyour Azure SQL veritabanı sunucusuna bağlanamıyor.
>

## <a name="import-a-bacpac-file-tooazure-sql-database"></a>Bir BACPAC dosya tooAzure SQL veritabanı alma 

Merhaba SQLPackage komut satırı yardımcı programını en yeni sürümleri Hello Azure SQL veritabanını belirtilen bir oluşturmak için destek sağlar [Hizmet katmanını ve performans düzeyini](sql-database-service-tiers.md). En iyi performans için içeri aktarma işlemi sırasında yüksek Hizmet katmanını ve performans düzeyini seçin ve hello hizmeti katmanını ve performans düzeyini hemen gerekenden daha yüksek olması durumunda içeri aktarma işleminden sonra ölçeklendirmeyi azaltın.

Bu adımları kullanın hello SQLPackage komut satırı yardımcı programını tooimport hello AdventureWorks2008R2 veritabanı tooAzure SQL veritabanı izleyin. Bu görev için SQL Server Management Studio'yu kullanabilirsiniz, ancak SQLPackage hello tercih edilen en büyük esneklik ve en iyi performans için birçok üretim ortamları için yöntemidir. Bkz: [SQL BACPAC dosyalarını kullanarak veritabanını SQL Server tooAzure geçiş](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

- Merhaba komut istemi tooimport hello SQLPackage komutunda aşağıdaki hello yürütme **AdventureWorks2008R2** yerel depolama toohello SQL server mantıksal Sunucusu'ndan Bu, önceden oluşturulmuş tooa yeni veritabanı, bir hizmeti veritabanı katmanını **Premium**ve bir hizmet amacını **P6**. SQL server mantıksal sunucunuz için uygun değerlerle köşeli Hello değerleri değiştirin ve hello yeni veritabanı (da Değiştir hello açılı ayraçları) için bir ad belirtin. Bu gibi durumlarda, veritabanı sürümü ve hizmet objectgive toochange hello değerleri de uygun tooyour ortamı olarak seçebilirsiniz. Bu öğretici Hello amaçla hello geçirilen veritabanı olarak adlandırılan **myMigratedDatabase**.

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![sqlpackage alma](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Bir SQL server mantıksal sunucusu 1433 bağlantı noktasını dinler. Tooconnect tooa SQL server mantıksal Sunucusu'ndan kurumsal bir güvenlik duvarı içinde çalışıyorsanız, toosuccessfully bağlanmak için bu bağlantı noktası hello Kurumsal Güvenlik Duvarı'nda açık olması gerekir.
>

## <a name="connect-using-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) kullanarak bağlan

SQL Server Management Studio tooestablish bağlantı tooyour Azure SQL veritabanı sunucusu ve adlı yeni geçirilen veritabanı kullanmak **myMigratedDatabase** bu öğreticideki. SQL Server Management Studio SQLPackage çalıştırıldığı farklı bir bilgisayarda çalışıyorsa hello önceki yordamda hello adımları kullanarak bu bilgisayar için bir güvenlik duvarı kuralı oluşturun.

1. SQL Server Management Studio’yu açın.

2. Merhaba, **tooServer bağlanmak** iletişim kutusunda, aşağıdaki bilgilerle hello girin:
   - **Sunucu türü**: Veritabanı altyapısını belirtin
   - **Sunucu adı**: tam sunucu adınızı girin **mynewserver20170403.database.windows.net**
   - **Kimlik doğrulama**: SQL Server Kimlik Doğrulaması belirtin
   - **Kullanıcı adı**: Sunucu yöneticisi hesabınızı girin
   - **Parola**: sunucu yönetici hesabınız için hello parolayı girin
 
    ![SSMS ile bağlanma](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. **Bağlan**'a tıklayın. Merhaba Nesne Gezgini penceresi açılır. 

4. Nesne Gezgini'nde genişletin **veritabanları** genişletin ve ardından **myMigratedDatabase** hello örnek veritabanındaki tooview hello nesneleri.

## <a name="change-database-properties"></a>Veritabanı özelliklerini değiştir

Merhaba hizmet katmanı, performans düzeyi ve SQL Server Management Studio'yu kullanarak uyumluluk düzeyini değiştirebilirsiniz. Merhaba içeri aktarma aşaması sırasında tooa daha yüksek performans katmanı veritabanı en iyi performans için aktarmak, ancak içeri aktarılan veritabanını hello hazır tooactively kullan olana kadar toosave para hello alma işlemi tamamlandıktan sonra ölçeklendirmenizi öneririz. Merhaba uyumluluk düzeyinin değiştirilmesi, daha iyi performans ve erişim toohello yeni yetenekleri hello Azure SQL veritabanı hizmetinin verim. Eski bir veritabanını geçirdiğinizde, veritabanı uyumluluk düzeyi alınmakta hello veritabanıyla uyumlu olduğundan hello desteklenen en düşük düzeyde tutulur. Daha fazla bilgi için bkz: [iyileştirilmiş sorgu performansı ile Azure SQL veritabanı uyumluluk düzeyi 130](sql-database-compatibility-level-query-performance-130.md).

1. Nesne Gezgini'nde sağ **myMigratedDatabase** tıklatıp **yeni sorgu**. Bir sorgu penceresi bağlı tooyour veritabanı açar.

2. Komut tooset hello hizmet katmanı çok aşağıdaki hello yürütme**standart** ve performans düzeyi çok hello**S1**.

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

3. Komut toochange hello veritabanı uyumluluk düzeyi çok aşağıdaki hello yürütme**130**.

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![uyumluluk düzeyini değiştirme](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a>Sonraki adımlar 
Bu öğreticide dışarı ve veritabanınızı içe hazır. İçin öğrenilen:

> [!div class="checklist"]
> * Bir SQL Server veritabanında SQL veritabanı geçiş tooAzure için hazırlama
> * Merhaba veritabanı tooa BACPAC dosyası dışarı aktarma
> * Bir Azure SQL veritabanına Hello BACPAC dosyası

Toohello sonraki öğretici toolearn nasıl ilerlemek toosecure veritabanınızı.

> [!div class="nextstepaction"]
> [Azure SQL veritabanınızı güvenli](sql-database-security-tutorial.md).


