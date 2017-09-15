## <a name="next-steps"></a><span data-ttu-id="d089f-101">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d089f-101">Next steps</span></span>

<span data-ttu-id="d089f-102">Azure anahtar kasası tümleştirmeyi etkinleştirdikten sonra SQL VM üzerinde SQL Server şifrelemeyi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d089f-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="d089f-103">İlk olarak, anahtar kasanızı içinde bir asimetrik anahtar ve SQL Server içinde bir simetrik anahtar kendi VM'nizi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d089f-103">First, you will need to create an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="d089f-104">Ardından, veritabanları ve yedeklemeleri şifrelemeyi etkinleştirmek için T-SQL deyimlerini yürütmek mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d089f-104">Then, you will be able to execute T-SQL statements to enable encryption for your databases and backups.</span></span>

<span data-ttu-id="d089f-105">Birkaç forms özelliklerden yararlanabilirsiniz şifreleme vardır:</span><span class="sxs-lookup"><span data-stu-id="d089f-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="d089f-106">Saydam veri şifreleme (TDE)</span><span class="sxs-lookup"><span data-stu-id="d089f-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="d089f-107">Şifreli yedekleme</span><span class="sxs-lookup"><span data-stu-id="d089f-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="d089f-108">Sütun düzeyinde şifreleme (Temizle)</span><span class="sxs-lookup"><span data-stu-id="d089f-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="d089f-109">Bu alanların her biri için aşağıdaki Transact-SQL betikleri örnekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="d089f-109">The following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="d089f-110">Örnekler için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d089f-110">Prerequisites for examples</span></span>

<span data-ttu-id="d089f-111">Bulunan iki önkoşul tabanlı her örnek: bir asimetrik anahtar, anahtar Kasası'ndan adlı **CONTOSO_KEY** AKV tümleştirme özelliği tarafından oluşturulan bir kimlik bilgisi adı verilen ve **Azure_EKM_TDE_cred**.</span><span class="sxs-lookup"><span data-stu-id="d089f-111">Each example is based on the two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by the AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="d089f-112">Aşağıdaki Transact-SQL komutlarıyla örnekleri çalıştırmak için bu Önkoşullar ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d089f-112">The following Transact-SQL commands setup these prerequisites for running the examples.</span></span>

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

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="d089f-113">Saydam veri şifreleme (TDE)</span><span class="sxs-lookup"><span data-stu-id="d089f-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="d089f-114">TDE için veritabanı altyapısı tarafından kullanılacak bir SQL Server oturumu oluşturun, sonra kimlik bilgisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d089f-114">Create a SQL Server login to be used by the Database Engine for TDE, then add the credential to it.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with the asymmetric key
   -- for the Database engine to use when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the TDE Login to add the credential for use by the
   -- Database Engine to access the key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. <span data-ttu-id="d089f-115">TDE için kullanılacak veritabanı şifreleme anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d089f-115">Create the database encryption key that will be used for TDE.</span></span>

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the database to enable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a><span data-ttu-id="d089f-116">Şifreli yedekleme</span><span class="sxs-lookup"><span data-stu-id="d089f-116">Encrypted backups</span></span>

1. <span data-ttu-id="d089f-117">Yedeklemeleri şifrelemek için veritabanı motoru tarafından kullanılmak üzere bir SQL Server oturumu oluşturun ve kimlik bilgisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d089f-117">Create a SQL Server login to be used by the Database Engine for encrypting backups, and add the credential to it.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with the asymmetric key
   -- for the Database engine to use when it is encrypting the backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the Encrypted Backup Login to add the credential for use by
   -- the Database Engine to access the key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. <span data-ttu-id="d089f-118">Yedekleme veritabanı belirtme şifreleme anahtar kasasında depolanan asimetrik anahtarla.</span><span class="sxs-lookup"><span data-stu-id="d089f-118">Backup the database specifying encryption with the asymmetric key stored in the key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   TO DISK = N'[PATH TO BACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="d089f-119">Sütun düzeyinde şifreleme (Temizle)</span><span class="sxs-lookup"><span data-stu-id="d089f-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="d089f-120">Bu komut dosyası anahtar kasasında asimetrik anahtar tarafından korunan bir simetrik anahtar oluşturur ve veritabanındaki verileri şifrelemek için simetrik anahtar kullanır.</span><span class="sxs-lookup"><span data-stu-id="d089f-120">This script creates a symmetric key protected by the asymmetric key in the key vault, and then uses the symmetric key to encrypt data in the database.</span></span>

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open the symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close the symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a><span data-ttu-id="d089f-121">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d089f-121">Additional resources</span></span>

<span data-ttu-id="d089f-122">Bu şifreleme özelliklerinin nasıl kullanılacağı hakkında daha fazla bilgi için bkz: [kullanarak EKM SQL Server şifreleme özellikleriyle](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span><span class="sxs-lookup"><span data-stu-id="d089f-122">For more information on how to use these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="d089f-123">Bu makaledeki adımları zaten bir Azure sanal makinede çalışan SQL Server olduğunu varsayalım unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d089f-123">Note that the steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="d089f-124">Aksi takdirde bkz [bir SQL Server sanal makinesi sağlama](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="d089f-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="d089f-125">Azure Vm'lerinde SQL Server çalıştıran diğer yönergeler için bkz: [Azure sanal makinelere genel bakış SQL Server'da](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d089f-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>