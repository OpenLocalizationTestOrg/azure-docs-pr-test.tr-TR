---
title: "aaaDesign ilk Azure SQL veritabanınızı | Microsoft Docs"
description: "İlk Azure SQL veritabanınızı toodesign öğrenin."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/03/2017
ms.author: carlrab
ms.openlocfilehash: 65f0a1594cbdda7480abf32a847266a073e7560d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-sql-database"></a>İlk Azure SQL veritabanınızı tasarlama

Azure SQL veritabanı bir ilişkisel veritabanı-olarak-a (DBaaS) hello Microsoft Cloud ("Azure") hizmetidir. Bu öğreticide, nasıl toouse hello Azure portal öğrenin ve [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) için: 

> [!div class="checklist"]
> * Hello Azure portalında bir veritabanı oluşturun
> * Hello Azure portal sunucu düzeyinde güvenlik duvarı kuralında ayarlama
> * SSMS ile toohello veritabanına bağlanın
> * SSMS ile tabloları oluşturma
> * Yığın BCP ile veri yükleme
> * SSMS ile bu verileri Sorgulama
> * Merhaba veritabanı tooa önceki geri [geri yükleme noktası](sql-database-recovery-using-backups.md#point-in-time-restore) hello Azure portal'ın

Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici, yapma emin yüklediğiniz:
- Merhaba en yeni sürümünü [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).
- Merhaba en yeni sürümünü [BCP ve SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).

## <a name="log-in-toohello-azure-portal"></a>Toohello Azure portalında oturum açın

İçinde toohello oturum [Azure portal](https://portal.azure.com/).

## <a name="create-a-blank-sql-database"></a>Boş bir SQL veritabanı oluşturma

Azure SQL veritabanı bir dizi [işlem ve depolama kaynağı](sql-database-service-tiers.md) ile oluşturulur. Merhaba veritabanı içinde oluşturulur bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) ve bir [Azure SQL Database mantıksal sunucusu](sql-database-features.md). 

Bu adımları toocreate boş bir SQL veritabanı izleyin. 

1. Merhaba tıklatın **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.

2. Seçin **veritabanları** hello gelen **yeni** sayfasında ve seçin **SQL veritabanı** hello gelen **veritabanları** sayfası. 

   ![Boş veritabanı oluşturma](./media/sql-database-design-first-database/create-empty-database.png)

3. Hello SQL veritabanı formu görüntü önceki hello üzerinde gösterildiği gibi bilgileri, aşağıdaki hello ile doldurun:   

   | Ayar       | Önerilen değer | Açıklama | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Veritabanı adı** | mySampleDatabase | Geçerli veritabanı adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers). | 
   | **Abonelik** | Aboneliğiniz  | Abonelikleriniz hakkında daha ayrıntılı bilgi için bkz. [Abonelikler](https://account.windowsazure.com/Subscriptions). |
   | **Kaynak grubu** | myResourceGroup | Geçerli kaynak grubu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). |
   | **Kaynak seçin** | Boş veritabanı | Boş bir veritabanı oluşturulması gerektiğini belirtir. |

4. Tıklatın **Server** toocreate ve yeni veritabanı için yeni bir sunucu yapılandırabilirsiniz. Merhaba dolgu **yeni sunucu form** bilgisinden hello ile: 

   | Ayar       | Önerilen değer | Açıklama | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Sunucu adı** | Genel olarak benzersiz bir ad | Geçerli sunucu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). | 
   | **Sunucu yöneticisi oturum açma bilgileri** | Geçerli bir ad | Geçerli oturum açma adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).|
   | **Parola** | Geçerli bir parola | Parolanız en az 8 karakter olmalı ve kategorileri aşağıdaki hello üçünden karakterler içermelidir: büyük harf karakterler, küçük harfler, sayılar ve alfasayısal olmayan karakter. |
   | **Konum** | Geçerli bir konum | Bölgeler hakkında bilgi için bkz. [Azure Bölgeleri](https://azure.microsoft.com/regions/). |

   ![create database-server](./media//sql-database-design-first-database/create-database-server.png)

5. **Seç**'e tıklayın.

6. Tıklatın **fiyatlandırma katmanı** toospecify hello hizmeti katmanını ve performans düzeyini yeni veritabanı. Bu öğretici için seçin **20 Dtu'lar** ve **250** GB depolama alanı.

   ![create database-s1](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. **Uygula**'ya tıklayın.  

8. Seçin bir **harmanlama** hello boş veritabanı (Bu öğretici için kullanım hello varsayılan değer). Harmanlamaları hakkında daha fazla bilgi için bkz: [harmanlamaları](https://docs.microsoft.com/sql/t-sql/statements/collations)

9. Tıklatın **oluşturma** tooprovision hello veritabanı. Bir dakika ve bir yarı toocomplete hakkında alır sağlama. 

10. Merhaba araç çubuğundan, **bildirimleri** toomonitor hello dağıtım işlemi.

   ![bildirim](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a>Sunucu düzeyinde bir güvenlik duvarı kuralı oluşturma

Hello SQL veritabanı hizmetinin hello sunucusu düzeyinde-harici uygulamalar ve Araçlar tooopen hello Güvenlik Duvarı'nı belirli IP adresleri için bir güvenlik duvarı kuralı yapılandırılmadığı sürece toohello sunucu veya hello sunucudaki tüm veritabanları bağlanmasını engelleyen bir güvenlik duvarı oluşturur. Bu adımları toocreate izleyin bir [SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı](sql-database-firewall-configure.md) için istemcinin IP adresi ve IP adresiniz yalnızca hello SQL veritabanı güvenlik duvarı üzerinden dış bağlantısı etkinleştirin. 

> [!NOTE]
> SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar. Bir şirket ağından gelen tooconnect çalışıyorsanız, bağlantı noktası 1433 üzerinden giden trafik, ağınızın güvenlik duvarı tarafından izin verilmiyor. BT departmanınız 1433 numaralı bağlantı noktasını açar sürece bu durumda, tooyour Azure SQL veritabanı sunucusuna bağlanamıyor.
>

1. Merhaba dağıtım tamamlandıktan sonra **SQL veritabanları** hello sol menüsünden ve ardından **mySampleDatabase** hello üzerinde **SQL veritabanları** sayfası. Merhaba hello tam olarak gösteren, veritabanı açılır genel bakış sayfasında tam sunucu adını (gibi **mynewserver20170313.database.windows.net**) ve diğer yapılandırmalar için seçenekler sağlar. Daha sonra kullanmak üzere bu tam sunucu adını kopyalayın.

   > [!IMPORTANT]
   > Sonraki hızlı başlatır, veritabanlarını ve bu tam sunucu adı tooconnect tooyour sunucu gerekir.
   > 

   ![sunucu adı](./media/sql-database-connect-query-dotnet/server-name.png) 

2. Tıklatın **ayarlayın sunucu Güvenlik Duvarı** hello önceki görüntüde gösterildiği gibi hello araç. Merhaba **Güvenlik Duvarı ayarları** hello SQL veritabanı sunucusu sayfasını açar. 

   ![sunucu güvenlik duvarı kuralı](./media/sql-database-get-started-portal/server-firewall-rule.png) 


3. Tıklatın **istemci IP'si Ekle** hello araç tooadd üzerinde geçerli IP adresi tooa yeni güvenlik duvarı kuralı. Güvenlik duvarı kuralı, 1433 numaralı bağlantı noktasını tek bir IP adresi veya bir IP adresi aralığı için açabilir.

4. **Kaydet** düğmesine tıklayın. Geçerli IP adresiniz hello mantıksal sunucuda bağlantı noktası 1433'ü açmak için bir sunucu düzeyinde güvenlik duvarı kuralı oluşturulur.

   ![sunucu güvenlik duvarı kuralı ayarla](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Tıklatın **Tamam** ve hello kapatın **Güvenlik Duvarı ayarları** sayfası.

Şimdi toohello SQL veritabanı sunucusunu ve veritabanlarını SQL Server Management Studio veya bu IP adresinden daha önce oluşturulmuş hello server yönetici hesabı kullanarak tercih ettiğiniz başka bir araç kullanarak bağlanabilir.

> [!IMPORTANT]
> Varsayılan olarak, tüm Azure hizmetlerini hello SQL veritabanı güvenlik duvarı üzerinden erişim etkin. Tıklatın **OFF** tüm Azure Hizmetleri için bu sayfayı toodisable üzerinde.

## <a name="sql-server-connection-information"></a>SQL Server bağlantı bilgileri

Azure SQL veritabanı sunucunuz için Hello tam sunucu adını hello Azure portal alın. SQL Server Management Studio'yu kullanarak hello tam adı tooconnect tooyour sunucusu kullanın.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası. 
3. Merhaba, **Essentials** Merhaba, veritabanı için Azure portal sayfası bölmesinde bulun ve ardından hello kopyalayın **sunucu adı**.

   ![bağlantı bilgileri](./media/sql-database-connect-query-dotnet/server-name.png)

## <a name="connect-toohello-database-with-ssms"></a>SSMS ile toohello veritabanına bağlanın

Kullanım [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish bağlantı tooyour Azure SQL veritabanı sunucusu.

1. SQL Server Management Studio’yu açın.

2. Merhaba, **tooServer bağlanmak** iletişim kutusunda, aşağıdaki bilgilerle hello girin:

   | Ayar       | Önerilen değer | Açıklama | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | Sunucu türü | Veritabanı altyapısı | Bu değer gereklidir |
   | Sunucu adı | Merhaba tam sunucu adı | Merhaba adı şöyle olmalıdır: **mynewserver20170313.database.windows.net**. |
   | Kimlik Doğrulaması | SQL Server Kimlik Doğrulaması | SQL kimlik doğrulaması biz Bu öğreticide yapılandırdığınız hello yalnızca kimlik doğrulaması türüdür. |
   | Oturum Aç | Merhaba server yönetici hesabı | Bu hello sunucu oluşturduğunuzda, belirttiğiniz hello hesabıdır. |
   | Parola | Sunucu yönetici hesabınız için Hello parola | Bu hello sunucu oluşturduğunuzda, belirttiğiniz hello paroladır. |

   ![tooserver Bağlan](./media/sql-database-connect-query-ssms/connect.png)

3. Tıklatın **seçenekleri** hello içinde **tooserver bağlanmak** iletişim kutusu. Merhaba, **toodatabase bağlanmak** bölümünde, girin **mySampleDatabase** tooconnect toothis veritabanı.

   ![sunucuda toodb Bağlan](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. **Bağlan**'a tıklayın. SSMS Hello Nesne Gezgini penceresi açılır. 

5. Nesne Gezgini'nde genişletin **veritabanları** genişletin ve ardından **mySampleDatabase** hello örnek veritabanındaki tooview hello nesneleri.

   ![Veritabanı nesneleri](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-hello-database"></a>Merhaba veritabanında tabloları oluşturma 

Bir öğrenci yönetimi sistemi kullanarak üniversiteler için model dört tablolar ile bir veritabanı şeması oluşturma [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):

- Kişi
- İndirmelere
- Öğrenci
- Bu model bir öğrenci yönetim sistemi üniversiteler için kredi

Merhaba Aşağıdaki diyagramda nasıl bu tablolar diğer ilgili tooeach gösterir. Bu tablolar bazıları diğer tablolardaki sütunlara başvuru. Örneğin, hello hello Öğrenci tabloya başvuruyorsa **PersonId** hello sütunu **kişi** tablo. Olay İncelemesi hello diyagramı toounderstand nasıl hello tabloları Bu öğreticide ilgili tooone olan başka bir. Nasıl ilişkin ayrıntılı bir bakış için toocreate etkili veritabanı tabloları, bkz: [etkili veritabanı tabloları oluşturma](https://msdn.microsoft.com/library/cc505842.aspx). Veri türleri seçme hakkında daha fazla bilgi için bkz: [veri türleri](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).

> [!NOTE]
> Merhaba de kullanabilirsiniz [Tablo Tasarımcısı'nda SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) toocreate ve tabloları tasarlayın. 

![Tablo ilişkileri](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. Nesne Gezgini’nde **mySampleDatabase** öğesine sağ tıklayıp **Yeni Sorgu**’ya tıklayın. Boş sorgu penceresi bağlı tooyour veritabanını başka bir deyişle açar.

2. Merhaba sorgu penceresinde, veritabanınızda query toocreate dört tablonun aşağıdaki hello yürütün: 

   ```sql 
   -- Create Person table

   CREATE TABLE Person
   (
   PersonId   INT IDENTITY PRIMARY KEY,
   FirstName   NVARCHAR(128) NOT NULL,
   MiddelInitial NVARCHAR(10),
   LastName   NVARCHAR(128) NOT NULL,
   DateOfBirth   DATE NOT NULL
   )
   
   -- Create Student table
 
   CREATE TABLE Student
   (
   StudentId INT IDENTITY PRIMARY KEY,
   PersonId  INT REFERENCES Person (PersonId),
   Email   NVARCHAR(256)
   )
   
   -- Create Course table
 
   CREATE TABLE Course
   (
   CourseId  INT IDENTITY PRIMARY KEY,
   Name   NVARCHAR(50) NOT NULL,
   Teacher   NVARCHAR(256) NOT NULL
   ) 

   -- Create Credit table
 
   CREATE TABLE Credit
   (
   StudentId   INT REFERENCES Student (StudentId),
   CourseId   INT REFERENCES Course (CourseId),
   Grade   DECIMAL(5,2) CHECK (Grade <= 100.00),
   Attempt   TINYINT,
   CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
   (
   StudentId, CourseId, Grade, Attempt
   )
   )
   ```

   ![Tabloları oluşturma](./media/sql-database-design-first-database/create-tables.png)

3. Oluşturduğunuz hello SQL Server Management Studio Nesne Gezgini toosee hello tabloları Hello 'tablo' düğümünü genişletin.

   ![SSMS tablolarının oluşturulması](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-hello-tables"></a>Merhaba tablolara veri yükleme

1. Adlı bir klasör oluşturun **SampleTableData** indirmeler klasörüne toostore örnek verilerinizde veritabanınız için. 

2. Sağ hello aşağıdaki bağlar ve bunları hello kaydetmek **SampleTableData** klasör. 

   - [SampleCourseData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [SamplePersonData](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [SampleStudentData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [SampleCreditData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. Bir komut istemi penceresi açın ve toohello SampleTableData klasörüne gidin.

4. Merhaba değerlerini değiştirme hello tablolara komutları tooinsert örnek verileri aşağıdaki hello yürütme **ServerName**, **DatabaseName**, **kullanıcıadı**ve **Parola** ortamınız için hello değerlere sahip.
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

Ayrıca, daha önce oluşturduğunuz hello tablolara şimdi örnek veri yüklemiş olduğunuz.

## <a name="query-data"></a>Verileri sorgulama

Sorguları tooretrieve bilgisinden hello veritabanı tablolarından hello yürütün. Bkz: [SQL sorguları yazma](https://technet.microsoft.com/library/bb264565.aspx) toolearn SQL sorguları yazma hakkında daha fazla. Tüm hello Öğrenciler öğrettin tüm dört tablonun toofind tarafından ' Dominick kendi sınıfında 75 %'den daha yüksek bir düzeyde olan Pope' Hello ilk sorgu birleştirir. Merhaba ikinci sorgu dört tablonun tamamını birleştirir ve 'Barış Coleman' herhangi bir zamanda kaydolduğu tüm kursları bulur.

1. Bir SQL Server Management Studio sorgu penceresinde hello sorgu aşağıdaki yürütün:

   ```sql 
   -- Find hello students taught by Dominick Pope who have a grade higher than 75%

   SELECT  person.FirstName,
   person.LastName,
   course.Name,
   credit.Grade
   FROM  Person AS person
   INNER JOIN Student AS student ON person.PersonId = student.PersonId
   INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
   INNER JOIN Course AS course ON credit.CourseId = course.courseId
   WHERE course.Teacher = 'Dominick Pope' 
   AND Grade > 75
   ```

2. Bir SQL Server Management Studio sorgu penceresinde, sorguyu çalıştırın:

   ```sql
   -- Find all hello courses in which Noe Coleman has ever enrolled

   SELECT  course.Name,
   course.Teacher,
   credit.Grade
   FROM  Course AS course
   INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
   INNER JOIN Student AS student ON student.StudentId = credit.StudentId
   INNER JOIN Person AS person ON person.PersonId = student.PersonId
   WHERE person.FirstName = 'Noe'
   AND person.LastName = 'Coleman'
   ```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Zaman içinde veritabanı tooa önceki bir noktaya geri

Yanlışlıkla bir tabloyu sildiniz düşünün. Bu, kolayca kurtaramazsınız şeydir. Azure SQL veritabanı toogo geri tooany noktası hello zamanda son too35 günleri sağlar ve bu noktaya zaman tooa yeni veritabanı geri yükleme. Bu veritabanı toorecover silinmiş verilerinizi gerçekleştirebilirsiniz. Merhaba tabloları eklenmeden önce hello aşağıdaki adımları hello örnek veritabanı tooa geri yükleme noktası.

1. Merhaba SQL veritabanı sayfasında veritabanınız için tıklayın **geri** hello araç. Merhaba **geri** sayfası açılır.

   ![Geri yükleme](./media/sql-database-design-first-database/restore.png)

2. Merhaba dolgu **geri** form hello gerekli bilgilerle:
    * Veritabanı adı: Bir veritabanı adı sağlayın 
    * Noktası zamanında: Select hello **noktası zaman** hello geri yükleme formundaki sekmesi 
    * Geri yükleme noktası: hello veritabanı değiştirilmeden önce oluşan bir süre seçin
    * Hedef sunucu: bir veritabanı geri yüklenirken bu değeri değiştirilemiyor 
    * Esnek veritabanı havuzu: seçin **yok**  
    * Fiyatlandırma katmanı: seçin **20 Dtu'lar** ve **250 GB** depolama.

   ![geri yükleme noktası](./media/sql-database-design-first-database/restore-point.png)

3. Tıklatın **Tamam** toorestore hello veritabanı çok[tooa noktası zaman içinde geri](sql-database-recovery-using-backups.md#point-in-time-restore) hello tabloları eklenmeden önce. Veritabanı tooa farklı bir noktaya geri yükleme zamanında, hello yinelenen bir veritabanı oluşturur hello özgün veritabanı hello noktaya itibariyle aynı sunucuya belirttiğiniz hello saklama süresi içinde olduğu sürece, [hizmet katmanı](sql-database-service-tiers.md).

## <a name="next-steps"></a>Sonraki Adımlar 
Bu öğreticide temel veritabanı görevlerini gibi bir veritabanı ve tablo oluşturma hakkında bilgi edindiniz, yükleme ve verileri sorgulamak ve zaman içinde hello veritabanı tooa önceki noktası geri. Şunları öğrendiniz:
> [!div class="checklist"]
> * Veritabanı oluşturma
> * Bir güvenlik duvarı kuralı ayarlamak
> * Toohello veritabanı ile bağlantı [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)
> * Tabloları oluşturma
> * Yığın veri yükleme
> * Bu verileri Sorgulama
> * SQL veritabanı kullanarak zamanında Hello veritabanı tooa önceki noktası geri [geri yükleme noktası](sql-database-recovery-using-backups.md#point-in-time-restore) özellikleri

Visual Studio ve C# kullanarak veritabanı tasarlama hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
>[Bir Azure SQL veritabanı tasarlama ve C# ve ADO.NET bağlantı](sql-database-design-first-database-csharp.md)
