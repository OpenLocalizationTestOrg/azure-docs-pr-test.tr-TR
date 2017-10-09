---
title: "Her zaman şifreli: Azure SQL veritabanı - Windows sertifika deposunda | Microsoft Docs"
description: "Bu makalede, her zaman şifreli Sihirbazı SQL Server Management Studio (SSMS) kullanarak veritabanı şifreleme ile bir SQL veritabanında toosecure hassas verileri nasıl hello gösterir. Ayrıca, nasıl toostore hello Windows sertifika, şifreleme anahtarlarını saklamak gösterir."
keywords: "her zaman şifreli verileri, sql şifrelemesi, veritabanı şifreleme, hassas verileri şifrelemek"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a>Her zaman şifreli: SQL veritabanındaki hassas verileri korumak ve şifreleme anahtarlarınızı hello Windows sertifika deposunda depola

Bu makalede nasıl hello kullanarak toosecure hassas verileri bir SQL veritabanı şifreleme ile veritabanı gösterilmektedir [her zaman şifreli Sihirbazı](https://msdn.microsoft.com/library/mt459280.aspx) içinde [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). Ayrıca, nasıl toostore hello Windows sertifika, şifreleme anahtarlarını saklamak gösterir.

Her zaman şifreli bir yeni veri şifreleme Azure SQL veritabanındaki bir teknolojidir ve yardımcı olan bir SQL Server istemci ve sunucu arasında hareket sırasında rest hello sunucusunda hassas verileri korumak ve hello veri kullanımdayken bu hassas verileri asla sağlayarak olarak görünür düz metin hello veritabanı sistem içinde. Veri şifrelemek sonra yalnızca istemci uygulamaları ya da erişim toohello anahtarlara sahip uygulama sunucuları düz metin verilere erişebilir. Ayrıntılı bilgi için bkz: [(veritabanı altyapısı)'her zaman şifreli](https://msdn.microsoft.com/library/mt163865.aspx).

Merhaba veritabanı toouse her zaman şifreli yapılandırdıktan sonra C# Visual Studio toowork hello şifrelenmiş verilerle birlikte bir istemci uygulaması oluşturacaksınız.

Bu makale toolearn Hello adımları nasıl izleyin bir Azure SQL veritabanı için her zaman şifreli yukarı tooset. Bu makalede, nasıl tooperform hello aşağıdaki görevleri öğreneceksiniz:

* Kullanım hello her zaman şifreli sihirbazında SSMS toocreate [her zaman şifreli anahtarları](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).
  * Oluşturma bir [sütun ana anahtar (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).
  * Oluşturma bir [sütun şifreleme anahtarı (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).
* Bir veritabanı tablosu oluşturmak ve sütunları şifreleyebilirsiniz.
* Ekler, seçer ve şifrelenmiş hello sütunları verileri görüntüleyen bir uygulama oluşturun.

## <a name="prerequisites"></a>Ön koşullar
Bu öğretici için ihtiyacınız vardır:

* Bir Azure hesabı ve aboneliği Yoksa, kaydolun bir [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).
* [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) sürüm 13.0.700.242 veya sonraki bir sürümü.
* [.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) veya üstünü (Merhaba istemci bilgisayarda).
* [Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).

## <a name="create-a-blank-sql-database"></a>Boş bir SQL veritabanı oluşturma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Tıklatın **yeni** > **veri + depolama** > **SQL veritabanı**.
3. Oluşturma bir **boş** adlı veritabanı **Clinic** yeni veya var olan bir sunucuda. Hello Azure portalında bir veritabanı oluşturma hakkında ayrıntılı yönergeler için bkz: [ilk Azure SQL veritabanınızı](sql-database-get-started-portal.md).
   
    ![Boş veritabanı oluşturma](./media/sql-database-always-encrypted/create-database.png)

Daha sonra hello öğreticide hello bağlantı dizesi gerekir. Merhaba veritabanı oluşturulduktan sonra toohello yeni Clinic veritabanı ve kopyalama hello bağlantı dizesi gidin. Herhangi bir zamanda hello bağlantı dizesi elde edebilirsiniz, ancak bunu kolay toocopy onu hello Azure portal olduğunuzda.

1. Tıklatın **SQL veritabanları** > **Clinic** > **veritabanı bağlantı dizelerini Göster**.
2. Merhaba bağlantı dizesini kopyalayın **ADO.NET**.
   
    ![Merhaba bağlantı dizesini kopyalayın](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>SSMS ile toohello veritabanına bağlanın
SSMS açın ve toohello sunucu hello Clinic veritabanıyla ilişkilendirin.

1. SSMS açın. (Tıklatın **Bağlan** > **veritabanı altyapısı** tooopen hello **tooServer bağlanmak** penceresi açık değilse).
2. Sunucu adı ve kimlik bilgilerini girin. Merhaba sunucu adı hello SQL veritabanı dikey bulunabilir ve daha önce kopyaladığınız hello bağlantı dizesinde. Türü hello tam sunucu adını içeren *database.windows.net*.
   
    ![Merhaba bağlantı dizesini kopyalayın](./media/sql-database-always-encrypted/ssms-connect.png)

Merhaba, **yeni güvenlik duvarı kuralı** penceresi açılır oturum içinde tooAzure ve let SSMS sizin için yeni bir güvenlik duvarı kuralı oluşturun.

## <a name="create-a-table"></a>Bir tablo oluşturma
Bu bölümde, bir tablo toohold Hasta verileri oluşturur. Bu normal bir tablo başlangıçta--olacaktır şifreleme hello sonraki bölümde yapılandıracak.

1. Genişletme **veritabanları**.
2. Sağ hello **Clinic** veritabanı ve tıklatın **yeni sorgu**.
3. Transact-SQL (T-SQL) hello yeni sorgu penceresine aşağıdaki Yapıştır hello ve **yürütme** onu.

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a>(Her zaman şifreli yapılandırma) sütunları şifrele
SSMS sağlayan bir sihirbaz tooeasily yapılandırma ayarlayarak hello CMK, CEK ve şifrelenmiş sütunlar, her zaman şifrelenir.

1. Genişletme **veritabanları** > **Clinic** > **tabloları**.
2. Sağ hello **hastalar** tablo ve seçin **şifrelemek sütunları** tooopen hello her zaman şifreli Sihirbazı:
   
    ![Sütunları şifrele](./media/sql-database-always-encrypted/encrypt-columns.png)

Merhaba her zaman şifreli Sihirbazı'nı içerir bölümleri aşağıdaki hello: **sütun seçimi**, **ana anahtar yapılandırma** (CMK) **doğrulama**, ve  **Özet**.

### <a name="column-selection"></a>Sütun Seçimi
Tıklatın **sonraki** hello üzerinde **giriş** sayfa tooopen hello **sütun seçimi** sayfası. Bu sayfada, hangi sütunların seçecektir tooencrypt, istediğiniz [hello şifreleme türünü ve hangi sütun şifreleme anahtarı (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.

Şifreleme **SSN** ve **doğum tarihi** bilgi için her bir süre bekleyin. Merhaba **SSN** sütun eşitlik aramaları, birleştirmeler ve Grupla destekleyen belirleyici şifreleme kullanır. Merhaba **doğum tarihi** sütun işlemlerini desteklemeyen rastgele şifreleme kullanır.

Set hello **şifreleme türü** hello için **SSN** sütun çok**Deterministic** ve hello **doğum tarihi** sütun çok **Rastgele**. **İleri**’ye tıklayın.

![Sütunları şifrele](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a>Ana anahtar yapılandırma
Merhaba **ana anahtar yapılandırma** sayfasıdır CMK ve select hello anahtar depolama sağlayıcısı hello CMK depolanacağı ayarladığınız. Şu anda bir CMK hello Windows sertifika deposu, Azure anahtar kasası veya bir donanım güvenlik modülü (HSM) depolayabilirsiniz. Bu öğretici nasıl toostore anahtarlarınızı hello Windows sertifika depolamak gösterir.

Doğrulayın **Windows sertifika deposunda** seçilir ve tıklatın **sonraki**.

![Ana anahtar yapılandırma](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a>Doğrulama
Merhaba sütunları şifrelemek veya bir PowerShell komut dosyası toorun daha sonra kaydedin. Bu öğretici için seçin **toofinish şimdi devam** tıklatıp **sonraki**.

### <a name="summary"></a>Özet
Hello ayarlarının doğru olduğunu tıklatın emin olun ve **son** toocomplete hello kurulumu için her zaman şifrelenir.

![Özet](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a>Merhaba sihirbazın Eylemler doğrulayın
Merhaba Sihirbaz tamamlandıktan sonra veritabanı her zaman şifreli için ayarlanır. Merhaba gerçekleştirilen Sihirbazı hello aşağıdaki eylemler:

* Bir CMK oluşturulur.
* Bir CEK oluşturulur.
* Seçili sütunları şifreleme için yapılandırılmış hello. **Hastalar** tablosunda şu anda hiçbir veri var, ancak mevcut verileri hello seçili sütunlardaki şimdi şifrelenir.

Çok giderek SSMS hello anahtarlarında hello oluşturulmasını doğrulayabilirsiniz**Clinic** > **güvenlik** > **her zaman şifreli anahtarları**. Sihirbaz sizin için oluşturulan hello hello yeni anahtarlar artık görebilirsiniz.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Şifrelenmiş hello verilerle çalışan istemci uygulaması oluşturma
Her zaman şifreli ayarlamak, gerçekleştiren bir uygulama oluşturabilirsiniz *ekler* ve *seçer* sütunlar üzerinde hello şifrelenmiş. Merhaba örnek uygulamayı çalıştırın toosuccessfully çalıştırılmalıdır üzerinde hello hello Sihirbazı'nı her zaman şifreli çalıştığı aynı bilgisayarda. toorun hello uygulama başka bir bilgisayarda hello istemci uygulamasını çalıştıran her zaman şifreli sertifikaları toohello bilgisayarınızın dağıtmanız gerekir.  

> [!IMPORTANT]
> Uygulamanızı kullanmalısınız [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) nesneleri düz metin veri toohello sunucusu her zaman şifreli sütunlarla geçirilirken. Değişmez değerler SqlParameter nesnelerini kullanmadan geçirme bir özel durum neden olur.
> 
> 

1. Visual Studio'yu açın ve yeni bir C# konsol uygulaması oluşturun. Projenizi çok ayarlandığından emin olun**.NET Framework 4.6** veya sonraki bir sürümü.
2. Ad hello proje **AlwaysEncryptedConsoleApp** tıklatıp **Tamam**.

![Yeni konsol uygulaması](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>Bağlantı dizesi tooenable her zaman şifreli değiştirme
Bu bölümde nasıl tooenable veritabanı bağlantı dizenizi her zaman şifrelenir. Merhaba konsol uygulaması "Örnek konsol uygulaması her zaman şifrelenir." Merhaba sonraki bölümde, az önce oluşturduğunuz değiştirir

tooenable her zaman şifreli, gereksinim duyduğunuz tooadd hello **sütun şifreleme ayarı** anahtar sözcüğü tooyour bağlantı dizesi ve çok ayarlayın**etkin**.

Bu doğrudan hello bağlantı dizesinde ayarlayabilirsiniz veya kullanarak ayarlayabilirsiniz bir [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). Merhaba Hello örnek uygulama sonraki bölüm gösterir nasıl toouse **SqlConnectionStringBuilder**.

> [!NOTE]
> Bu bir istemci uygulama belirli tooAlways içinde şifrelenmiş gerekli hello yalnızca değişikliktir. Harici olarak kendi bağlantı dizesi depolar var olan bir uygulamanız varsa, (diğer bir deyişle, bir yapılandırma dosyasında), herhangi bir kod değiştirmeden mümkün tooenable her zaman şifreli olabilir.
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Her zaman şifreli hello bağlantı dizesinde etkinleştir
Anahtar sözcüğü tooyour bağlantı dizesi aşağıdaki hello ekleyin:

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a>Her zaman bir SqlConnectionStringBuilder ile şifrelenmiş etkinleştir
Merhaba aşağıdaki kod nasıl ayarlayarak tooenable her zaman şifreli hello gösterir [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) çok[etkin](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a>Her zaman şifreli örnek konsol uygulaması
Bu örnek gösterilmektedir nasıl yapılır:

* Bağlantı dizesi tooenable her zaman şifreli değiştirin.
* Veriler şifrelenmiş hello sütunlara ekleyin.
* Bir kayıt şifrelenmiş sütununda belirli bir değeri filtreleyerek seçin.

Merhaba Değiştir **Program.cs** koddan hello ile. Hello bağlantı dizesi hello genel connectionString değişken hello satır hello Main yönteminin doğrudan üstü için hello Azure portal, geçerli bağlantı dizesi ile değiştirin. Bu toomake toothis kodu gerekli hello yalnızca değişikliktir.

Merhaba uygulama toosee her zaman şifreli eylemini çalıştırın.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
         VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }


## <a name="verify-that-hello-data-is-encrypted"></a>Merhaba verilerin şifrelendiğinden emin olun
Merhaba sorgulayarak hello sunucuda hello gerçek veri şifrelenir hızlı bir şekilde denetleyebilirsiniz **hastalar** SSMS ile verileri. (Burada hello sütun şifreleme ayarı henüz etkinleştirilmedi geçerli bağlantınızı kullanın.)

Sorgu hello Clinic veritabanında aşağıdaki hello çalıştırın.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

Herhangi bir düz metin veri içermemesi hello şifrelenmiş sütunlar görebilirsiniz.

   ![Yeni konsol uygulaması](./media/sql-database-always-encrypted/ssms-encrypted.png)

toouse SSMS tooaccess düz metin veri Merhaba, hello ekleyebilirsiniz **sütun şifreleme ayarı = etkin** parametresi toohello bağlantı.

1. SSMS, sunucunuzun sağ **Object Explorer**ve ardından **Bağlantıyı Kes**.
2. Tıklatın **Bağlan** > **veritabanı altyapısı** tooopen hello **tooServer bağlanmak** penceresi ve ardından **seçenekleri**.
3. Tıklatın **ek bağlantı parametrelerini** ve türü **sütun şifreleme ayarı = etkin**.
   
    ![Yeni konsol uygulaması](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. Çalışma hello hello bir sorguyu aşağıdaki **Clinic** veritabanı.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     Şimdi şifrelenmiş hello sütunlardaki hello düz metin verileri görebilirsiniz.

    ![Yeni konsol uygulaması](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> Farklı bir bilgisayardan SSMS (veya herhangi bir istemci) ile bağlanıyorsanız, erişim toohello şifreleme anahtarları olmaz ve mümkün toodecrypt hello veri olmaz.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Her zaman şifreli kullanan bir veritabanı oluşturduktan sonra toodo hello aşağıdaki isteyebilirsiniz:

* Bu örnek, farklı bir bilgisayardan çalıştırın. Böylece erişim toohello düz metin veri olmaz ve başarılı bir şekilde çalışmaz erişim toohello şifreleme anahtarları, olmayacaktır.
* [Döndürün ve anahtarlarınızı Temizleme](https://msdn.microsoft.com/library/mt607048.aspx).
* [Zaten her zaman şifreli ile şifrelenmiş veri geçişi](https://msdn.microsoft.com/library/mt621539.aspx).
* [Her zaman şifreli sertifikaları tooother istemci makineleri dağıtmak](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (Merhaba "sertifikalar kullanılabilir tooApplications ve kullanıcıların hale" bölümüne bakın).

## <a name="related-information"></a>İlgili bilgiler
* [Her zaman şifreli (istemci geliştirme)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Saydam veri şifreleme](https://msdn.microsoft.com/library/bb934049.aspx)
* [SQL Server şifrelemesi](https://msdn.microsoft.com/library/bb510663.aspx)
* [Her zaman şifreli Sihirbazı](https://msdn.microsoft.com/library/mt459280.aspx)
* [Her zaman şifreli blogu](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

