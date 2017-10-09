---
title: "Her zaman şifreli: SQL veritabanı - Azure anahtar kasası | Microsoft Docs"
description: "Bu makalede, veri şifreleme kullanarak bir SQL veritabanında toosecure hassas verileri her zaman şifreli Sihirbazı SQL Server Management Studio'da nasıl hello gösterir. Bunu nasıl yapacağınızı gösterir yönergeleri de içerir toostore Azure anahtar Kasası'nda her şifreleme anahtarı."
keywords: "veri şifreleme, şifreleme anahtarı, bulut şifreleme"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a>Her zaman şifreli: SQL veritabanındaki hassas verileri korumak ve Azure anahtar kasası, şifreleme anahtarlarını saklamak

Bu makalede nasıl hello kullanarak veri şifrelemesi ile toosecure hassas verileri bir SQL veritabanı gösterilmektedir [her zaman şifreli Sihirbazı](https://msdn.microsoft.com/library/mt459280.aspx) içinde [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). Bunu nasıl yapacağınızı gösterir yönergeleri de içerir toostore Azure anahtar Kasası'nda her şifreleme anahtarı.

Her zaman şifreli bir yeni veri şifreleme Azure SQL veritabanındaki bir teknolojidir ve yardımcı olan bir SQL Server ve istemci ve sunucu arasında hello veri kullanımdayken taşıma sırasında rest hello sunucusunda hassas verileri koruyun. Her zaman şifreli hassas verileri asla hello veritabanı sistem içinde düz metin olarak görünmesini sağlar. Veri şifreleme yapılandırdıktan sonra yalnızca istemci uygulamaları ya da erişim toohello anahtarlara sahip uygulama sunucuları düz metin verilere erişebilir. Ayrıntılı bilgi için bkz: [(veritabanı altyapısı)'her zaman şifreli](https://msdn.microsoft.com/library/mt163865.aspx).

Merhaba veritabanı toouse her zaman şifreli yapılandırdıktan sonra C# Visual Studio toowork hello şifrelenmiş verilerle birlikte bir istemci uygulaması oluşturur.

Bu makalede Hello adımları izleyin ve öğrenin nasıl bir Azure SQL veritabanı için her zaman şifreli yukarı tooset. Bu makalede nasıl tooperform hello aşağıdaki görevleri öğreneceksiniz:

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
* [Azure PowerShell](/powershell/azure/overview), sürüm 1.0 veya üstü. Tür **(Get-Module azure - listavailable birlikte). Sürüm** toosee PowerShell sürümünü çalıştırıyor.

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a>İstemci uygulama tooaccess hello SQL veritabanı hizmetini etkinleştirme
İstemci uygulaması tooaccess hello SQL veritabanı hizmetinin hello gerekli kimlik doğrulama ve alınırken hello ayarlayarak etkinleştirmelisiniz *ClientID* ve *gizli* tooauthenticate gerekir koddan hello uygulamanızda.

1. Açık hello [Klasik Azure portalı](http://manage.windowsazure.com).
2. Seçin **Active Directory** ve uygulamanız kullanacak hello Active Directory örneğine'ı tıklatın.
3. Tıklatın **uygulamaları**ve ardından **eklemek**.
4. Uygulamanız için bir ad yazın (örneğin: *myClientApp*), select **WEB uygulaması**ve hello ok toocontinue'ı tıklatın.
5. Hello için **oturum açma URL** ve **uygulama kimliği URI'si** geçerli bir URL yazın (örneğin, *http://myClientApp*) ve devam edin.
6. Tıklatın **yapılandırma**.
7. Kopyalama, **istemci kimliği**. (Bu değer, kodunuzda daha sonra gerekecektir.)
8. Merhaba, **anahtarları** bölümünde, select **1 yıl** hello gelen **seçin süresi** aşağı açılan liste. (Adım 13 kaydettikten sonra hello anahtar kopyalayacak.)
9. Aşağı kaydırın ve tıklatın **uygulama eklemek**.
10. Bırakın **Göster** çok ayarlamak**Microsoft Apps** seçip **Microsoft Azure Hizmet Yönetimi API'si**. Merhaba onay işareti toocontinue'ı tıklatın.
11. Seçin **erişim Azure hizmet yönetimi...**  hello gelen **izinlere temsilci** aşağı açılan liste.
12. **KAYDET**'e tıklayın.
13. Sonlandığında kaydetme Hello sonra hello anahtar değeri hello kopyalama **anahtarları** bölümü. (Bu değer, kodunuzda daha sonra gerekecektir.)

## <a name="create-a-key-vault-toostore-your-keys"></a>Bir anahtar kasası toostore anahtarlarınızı oluşturma
İstemci uygulamanızı yapılandırılmış ve istemci Kimliğiniz sahip olduğunuza zaman toocreate bir anahtar kasası olan ve hello Kasası'nın gizli anahtarları (Merhaba her zaman şifreli anahtarlar) ve uygulamanızı erişebilmesi için erişim ilkesi yapılandırın. Merhaba *oluşturma*, *almak*, *listesi*, *oturum*, *doğrulayın*, *wrapKey*, ve *unwrapKey* yeni bir sütun ana anahtar oluşturma ve şifreleme SQL Server Management Studio ile ayarlamak için gerekli izinleri.

Komut dosyası izleyen hello çalıştırarak, bir anahtar kasası hızlı bir şekilde oluşturabilirsiniz. Ayrıntılı bir açıklaması ve bu cmdlet'leri ve oluşturma ve bir anahtar kasası yapılandırma hakkında daha fazla bilgi için bkz: [Azure anahtar kasası ile çalışmaya başlama](../key-vault/key-vault-get-started.md).

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a>Boş bir SQL veritabanı oluşturma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Çok Git**yeni** > **veri + depolama** > **SQL veritabanı**.
3. Oluşturma bir **boş** adlı veritabanı **Clinic** yeni veya var olan bir sunucuda. Toocreate hello Azure portal, bir veritabanına nasıl görürüm hakkında ayrıntılı yönergeler için [ilk Azure SQL veritabanınızı](sql-database-get-started-portal.md).
   
    ![Boş veritabanı oluşturma](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

Bağlantı dizesi hello hello veritabanı oluşturduktan sonra daha sonra hello öğreticide toohello yeni Clinic veritabanı ve kopyalama hello bağlantı dizesi bu nedenle göz atın. Herhangi bir zamanda hello bağlantı dizesi elde edebilirsiniz, ancak bunu kolay toocopy hello Azure portalı içinde.

1. Çok Git**SQL veritabanları** > **Clinic** > **veritabanı bağlantı dizelerini Göster**.
2. Merhaba bağlantı dizesini kopyalayın **ADO.NET**.
   
    ![Merhaba bağlantı dizesini kopyalayın](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>SSMS ile toohello veritabanına bağlanın
SSMS açın ve toohello sunucu hello Clinic veritabanıyla ilişkilendirin.

1. SSMS açın. (Çok Git**Bağlan** > **veritabanı altyapısı** tooopen hello **tooServer bağlanmak** açık değilse, pencere.)
2. Sunucu adı ve kimlik bilgilerini girin. Merhaba sunucu adı hello SQL veritabanı dikey bulunabilir ve daha önce kopyaladığınız hello bağlantı dizesinde. Tür hello tam sunucu adını dahil olmak üzere *database.windows.net*.
   
    ![Merhaba bağlantı dizesini kopyalayın](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

Merhaba, **yeni güvenlik duvarı kuralı** penceresi açılır oturum içinde tooAzure ve let SSMS sizin için yeni bir güvenlik duvarı kuralı oluşturun.

## <a name="create-a-table"></a>Bir tablo oluşturma
Bu bölümde, bir tablo toohold Hasta verileri oluşturur. Başlangıçta değil şifrelenmiş--hello sonraki bölümde şifreleme yapılandıracaksınız.

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
SSMS kolayca ayarlayarak hello sütun ana anahtar, sütun şifreleme anahtarı ve şifrelenmiş sütunlar, her zaman şifreli yapılandırmanıza yardımcı olacak bir sihirbaz sağlar.

1. Genişletme **veritabanları** > **Clinic** > **tabloları**.
2. Sağ hello **hastalar** tablo ve seçin **şifrelemek sütunları** tooopen hello her zaman şifreli Sihirbazı:
   
    ![Sütunları şifrele](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

Merhaba her zaman şifreli Sihirbazı'nı içerir bölümleri aşağıdaki hello: **sütun seçimi**, **ana anahtar yapılandırma**, **doğrulama**, ve **özeti** .

### <a name="column-selection"></a>Sütun Seçimi
Tıklatın **sonraki** hello üzerinde **giriş** sayfa tooopen hello **sütun seçimi** sayfası. Bu sayfada, hangi sütunların seçecektir tooencrypt, istediğiniz [hello şifreleme türünü ve hangi sütun şifreleme anahtarı (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.

Şifreleme **SSN** ve **doğum tarihi** bilgi için her bir süre bekleyin. Merhaba SSN sütun eşitlik aramaları, birleştirmeler ve Grupla destekleyen belirleyici şifreleme kullanır. Merhaba doğum tarihi sütun işlemlerini desteklemeyen rastgele şifreleme kullanır.

Set hello **şifreleme türü** hello SSN sütun için çok**Deterministic** ve doğum tarihi sütun çok hello**Randomized**. **İleri**’ye tıklayın.

![Sütunları şifrele](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a>Ana anahtar yapılandırma
Merhaba **ana anahtar yapılandırma** sayfasıdır CMK ve select hello anahtar depolama sağlayıcısı hello CMK depolanacağı ayarladığınız. Şu anda bir CMK hello Windows sertifika deposu, Azure anahtar kasası veya bir donanım güvenlik modülü (HSM) depolayabilirsiniz.

Bu öğreticide gösterilmiştir nasıl toostore anahtarlarınızı Azure anahtar Kasası'nda.

1. Seçin **Azure anahtar kasası**.
2. Merhaba İstenen anahtar kasası hello aşağı açılan listeden seçin.
3. **İleri**’ye tıklayın.

![Ana anahtar yapılandırma](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a>Doğrulama
Merhaba sütunları şifrelemek veya bir PowerShell komut dosyası toorun daha sonra kaydedin. Bu öğretici için seçin **toofinish şimdi devam** tıklatıp **sonraki**.

### <a name="summary"></a>Özet
Hello ayarlarının doğru olduğunu tıklatın emin olun ve **son** toocomplete hello kurulumu için her zaman şifrelenir.

![Özet](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a>Merhaba sihirbazın Eylemler doğrulayın
Merhaba Sihirbaz tamamlandıktan sonra veritabanı her zaman şifreli için ayarlanır. Merhaba gerçekleştirilen Sihirbazı hello aşağıdaki eylemler:

* Bir sütun ana anahtar oluşturulur ve Azure anahtar Kasası ' depolanır.
* Bir sütun şifreleme anahtarı oluşturulur ve Azure anahtar Kasası ' depolanır.
* Seçili sütunları şifreleme için yapılandırılmış hello. Merhaba hastalar tablosu şu anda hiç veri içermiyor, ancak mevcut verileri hello seçili sütunlardaki şimdi şifrelenir.

SSMS hello anahtarlarında hello oluşturulmasını genişleterek doğrulayabilirsiniz **Clinic** > **güvenlik** > **her zaman şifreli anahtarları**.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Şifrelenmiş hello verilerle çalışan istemci uygulaması oluşturma
Her zaman şifreli ayarlamak, gerçekleştiren bir uygulama oluşturabilirsiniz *ekler* ve *seçer* sütunlar üzerinde hello şifrelenmiş.  

> [!IMPORTANT]
> Uygulamanızı kullanmalısınız [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) nesneleri düz metin veri toohello sunucusu her zaman şifreli sütunlarla geçirilirken. Değişmez değerler SqlParameter nesnelerini kullanmadan geçirme bir özel durum neden olur.
> 
> 

1. Visual Studio'yu açın ve yeni C# oluşturma **konsol uygulaması** (2015 ve daha önceki Visual Studio) veya **konsol uygulaması (.NET Framework)** (2017 ve daha sonra Visual Studio). Projenizi çok ayarlandığından emin olun**.NET Framework 4.6** veya sonraki bir sürümü.
2. Ad hello proje **AlwaysEncryptedConsoleAKVApp** tıklatıp **Tamam**.
3. NuGet paketlerini çok giderek aşağıdaki hello yüklemek**Araçları** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsolu**.

Bu iki kod satırı hello Paket Yöneticisi konsolu çalıştırın.

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>Bağlantı dizesi tooenable her zaman şifreli değiştirme
Bu bölümde nasıl tooenable veritabanı bağlantı dizenizi her zaman şifrelenir.

tooenable her zaman şifreli, gereksinim duyduğunuz tooadd hello **sütun şifreleme ayarı** anahtar sözcüğü tooyour bağlantı dizesi ve çok ayarlayın**etkin**.

Bu doğrudan hello bağlantı dizesinde ayarlayabilirsiniz veya kullanarak ayarlayabilirsiniz [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). Merhaba Hello örnek uygulama sonraki bölüm gösterir nasıl toouse **SqlConnectionStringBuilder**.

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Her zaman şifreli hello bağlantı dizesinde etkinleştir
Anahtar sözcüğü tooyour bağlantı dizesi aşağıdaki hello ekleyin.

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a>Her zaman SqlConnectionStringBuilder ile şifrelenmiş etkinleştir
kodun gösterdiği nasıl aşağıdaki hello ayarlayarak tooenable her zaman şifreli [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) çok[etkin](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a>Hello Azure anahtar kasası sağlayıcısını Kaydet
Merhaba aşağıdaki kodu nasıl tooregister hello Azure anahtar kasası sağlayıcı hello ADO.NET sürücüsü ile gösterilir.

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a>Her zaman şifreli örnek konsol uygulaması
Bu örnek gösterilmektedir nasıl yapılır:

* Bağlantı dizesi tooenable her zaman şifreli değiştirin.
* Azure anahtar kasası, uygulamanın anahtar depolama sağlayıcısı hello olarak kaydedin.  
* Veriler şifrelenmiş hello sütunlara ekleyin.
* Bir kayıt şifrelenmiş sütununda belirli bir değeri filtreleyerek seçin.

Merhaba Değiştir **Program.cs** koddan hello ile. Merhaba genel connectionString değişkeni doğrudan hello Main yönteminin hello Azure portal, geçerli bağlantı dizesi ile önündeki hello satırında Hello bağlantı dizesini değiştirin. Bu toomake toothis kodu gerekli hello yalnızca değişikliktir.

Merhaba uygulama toosee her zaman şifreli eylemini çalıştırın.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

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

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
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


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed tooobtain hello access token");
            return result.AccessToken;
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
SSMS ile Merhaba hastalar veri sorgulayarak hello sunucuda hello gerçek veri şifrelenir hızlı bir şekilde kontrol edebilirsiniz (geçerli bağlantınızı kullanarak nerede **sütun şifreleme ayarı** henüz etkin değil).

Sorgu hello Clinic veritabanında aşağıdaki hello çalıştırın.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

Herhangi bir düz metin veri içermemesi hello şifrelenmiş sütunlar görebilirsiniz.

   ![Yeni konsol uygulaması](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

toouse SSMS tooaccess düz metin veri Merhaba, hello ekleyebilirsiniz *sütun şifreleme ayarı = etkin* parametresi toohello bağlantı.

1. SSMS, sunucunuzun sağ **Nesne Gezgini** ve **Bağlantıyı Kes**.
2. Tıklatın **Bağlan** > **veritabanı altyapısı** tooopen hello **tooServer bağlanmak** penceresini açın ve **seçenekleri**.
3. Tıklatın **ek bağlantı parametrelerini** ve türü **sütun şifreleme ayarı = etkin**.
   
    ![Yeni konsol uygulaması](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. Sorgu hello Clinic veritabanında aşağıdaki hello çalıştırın.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     Şimdi şifrelenmiş hello sütunlardaki hello düz metin verileri görebilirsiniz.

    ![Yeni konsol uygulaması](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a>Sonraki adımlar
Her zaman şifreli kullanan bir veritabanı oluşturduktan sonra toodo hello aşağıdaki isteyebilirsiniz:

* [Döndürün ve anahtarlarınızı Temizleme](https://msdn.microsoft.com/library/mt607048.aspx).
* [Zaten her zaman şifreli ile şifrelenmiş veri geçişi](https://msdn.microsoft.com/library/mt621539.aspx).

## <a name="related-information"></a>İlgili bilgiler
* [Her zaman şifreli (istemci geliştirme)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Saydam veri şifrelemesi](https://msdn.microsoft.com/library/bb934049.aspx)
* [SQL Server şifrelemesi](https://msdn.microsoft.com/library/bb510663.aspx)
* [Her zaman şifreli Sihirbazı](https://msdn.microsoft.com/library/mt459280.aspx)
* [Her zaman şifreli blogu](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

