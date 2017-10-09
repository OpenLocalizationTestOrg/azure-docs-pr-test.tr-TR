## <a name="next-steps"></a><span data-ttu-id="09737-101">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="09737-101">Next steps</span></span>

<span data-ttu-id="09737-102">Azure anahtar kasası tümleştirmeyi etkinleştirdikten sonra SQL VM üzerinde SQL Server şifrelemeyi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09737-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="09737-103">İlk olarak, toocreate bir asimetrik anahtar anahtar kasanızı ve SQL Server içinde bir simetrik anahtar içinde VM gerekir.</span><span class="sxs-lookup"><span data-stu-id="09737-103">First, you will need toocreate an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="09737-104">Ardından, veritabanları ve yedeklemeler için mümkün tooexecute T-SQL deyimleri tooenable şifreleme olacaktır.</span><span class="sxs-lookup"><span data-stu-id="09737-104">Then, you will be able tooexecute T-SQL statements tooenable encryption for your databases and backups.</span></span>

<span data-ttu-id="09737-105">Birkaç forms özelliklerden yararlanabilirsiniz şifreleme vardır:</span><span class="sxs-lookup"><span data-stu-id="09737-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="09737-106">Saydam veri şifreleme (TDE)</span><span class="sxs-lookup"><span data-stu-id="09737-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="09737-107">Şifreli yedekleme</span><span class="sxs-lookup"><span data-stu-id="09737-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="09737-108">Sütun düzeyinde şifreleme (Temizle)</span><span class="sxs-lookup"><span data-stu-id="09737-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="09737-109">Merhaba aşağıdaki Transact-SQL betikleri örnekleri bu alanların her biri için sağlar.</span><span class="sxs-lookup"><span data-stu-id="09737-109">hello following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="09737-110">Örnekler için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="09737-110">Prerequisites for examples</span></span>

<span data-ttu-id="09737-111">Bulunan hello iki önkoşul tabanlı her örnek: bir asimetrik anahtar, anahtar Kasası'ndan adlı **CONTOSO_KEY** ve adlı hello AKV tümleştirme özelliği tarafından oluşturulan bir kimlik bilgisi **Azure_EKM_TDE_cred**.</span><span class="sxs-lookup"><span data-stu-id="09737-111">Each example is based on hello two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by hello AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="09737-112">Merhaba aşağıdaki Transact-SQL komutlarıyla hello örnekleri çalıştırmak için bu Önkoşullar ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="09737-112">hello following Transact-SQL commands setup these prerequisites for running hello examples.</span></span>

``` sql
USE master;
GO

sp_configure [show advanced options], 1;
GO
RECONFIGURE;
GO

-- Enable EKM provider
sp_configure [EKM provider enabled], 1;
GO
RECONFIGURE;

--create provider
CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov
FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';
GO

--create credential
CREATE CREDENTIAL sysadmin_ekm_cred
    WITH IDENTITY = 'keytestvault', --keyvault
    SECRET = '<<SECRET>>'
FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;


--must have sysadmin
ALTER LOGIN [TDE_Login]
ADD CREDENTIAL sysadmin_ekm_cred;


CREATE ASYMMETRIC KEY CONTOSO_KEY
FROM PROVIDER [AzureKeyVault_EKM_Prov]
WITH PROVIDER_KEY_NAME = 'keytestvault',  --key name
CREATION_DISPOSITION = OPEN_EXISTING;
```

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="09737-113">Saydam veri şifreleme (TDE)</span><span class="sxs-lookup"><span data-stu-id="09737-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="09737-114">TDE için Hello veritabanı motoru tarafından kullanılan SQL Server oturum açma toobe oluşturun, sonra hello kimlik bilgisi tooit ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09737-114">Create a SQL Server login toobe used by hello Database Engine for TDE, then add hello credential tooit.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello TDE Login tooadd hello credential for use by the
   -- Database Engine tooaccess hello key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. <span data-ttu-id="09737-115">TDE için kullanılacak hello veritabanı şifreleme anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09737-115">Create hello database encryption key that will be used for TDE.</span></span>

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello database tooenable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a><span data-ttu-id="09737-116">Şifreli yedekleme</span><span class="sxs-lookup"><span data-stu-id="09737-116">Encrypted backups</span></span>

1. <span data-ttu-id="09737-117">Merhaba yedeklemeleri şifrelemek için veritabanı motoru tarafından kullanılan SQL Server oturum açma toobe oluşturun ve hello kimlik bilgisi tooit ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09737-117">Create a SQL Server login toobe used by hello Database Engine for encrypting backups, and add hello credential tooit.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it is encrypting hello backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello Encrypted Backup Login tooadd hello credential for use by
   -- hello Database Engine tooaccess hello key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. <span data-ttu-id="09737-118">Yedekleme hello veritabanı hello asimetrik anahtarla hello anahtar kasasında depolanan şifreleme belirtme.</span><span class="sxs-lookup"><span data-stu-id="09737-118">Backup hello database specifying encryption with hello asymmetric key stored in hello key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="09737-119">Sütun düzeyinde şifreleme (Temizle)</span><span class="sxs-lookup"><span data-stu-id="09737-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="09737-120">Bu komut dosyası hello anahtar kasasında hello asimetrik anahtar tarafından korunan bir simetrik anahtar oluşturur ve ardından hello simetrik anahtar tooencrypt veri hello veritabanında kullanır.</span><span class="sxs-lookup"><span data-stu-id="09737-120">This script creates a symmetric key protected by hello asymmetric key in hello key vault, and then uses hello symmetric key tooencrypt data in hello database.</span></span>

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open hello symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data tooencrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close hello symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a><span data-ttu-id="09737-121">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="09737-121">Additional resources</span></span>

<span data-ttu-id="09737-122">Toouse bu şifreleme özellikleri nasıl görürüm hakkında daha fazla bilgi için [kullanarak EKM SQL Server şifreleme özellikleriyle](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span><span class="sxs-lookup"><span data-stu-id="09737-122">For more information on how toouse these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="09737-123">Bu makaledeki adımları Hello bir Azure sanal makinede çalışan SQL Server zaten sahip olduğunuzu varsaymaktadır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="09737-123">Note that hello steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="09737-124">Aksi takdirde bkz [bir SQL Server sanal makinesi sağlama](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="09737-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="09737-125">Azure Vm'lerinde SQL Server çalıştıran diğer yönergeler için bkz: [Azure sanal makinelere genel bakış SQL Server'da](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="09737-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
