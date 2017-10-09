## <a name="next-steps"></a>Sonraki adımlar

Azure anahtar kasası tümleştirmeyi etkinleştirdikten sonra SQL VM üzerinde SQL Server şifrelemeyi etkinleştirebilirsiniz. İlk olarak, toocreate bir asimetrik anahtar anahtar kasanızı ve SQL Server içinde bir simetrik anahtar içinde VM gerekir. Ardından, veritabanları ve yedeklemeler için mümkün tooexecute T-SQL deyimleri tooenable şifreleme olacaktır.

Birkaç forms özelliklerden yararlanabilirsiniz şifreleme vardır:

* [Saydam veri şifreleme (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)
* [Şifreli yedekleme](https://msdn.microsoft.com/library/dn449489.aspx)
* [Sütun düzeyinde şifreleme (Temizle)](https://msdn.microsoft.com/library/ms173744.aspx)

Merhaba aşağıdaki Transact-SQL betikleri örnekleri bu alanların her biri için sağlar.

### <a name="prerequisites-for-examples"></a>Örnekler için Önkoşullar

Bulunan hello iki önkoşul tabanlı her örnek: bir asimetrik anahtar, anahtar Kasası'ndan adlı **CONTOSO_KEY** ve adlı hello AKV tümleştirme özelliği tarafından oluşturulan bir kimlik bilgisi **Azure_EKM_TDE_cred**. Merhaba aşağıdaki Transact-SQL komutlarıyla hello örnekleri çalıştırmak için bu Önkoşullar ayarlayın.

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

### <a name="transparent-data-encryption-tde"></a>Saydam veri şifreleme (TDE)

1. TDE için Hello veritabanı motoru tarafından kullanılan SQL Server oturum açma toobe oluşturun, sonra hello kimlik bilgisi tooit ekleyin.

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

1. TDE için kullanılacak hello veritabanı şifreleme anahtarı oluşturun.

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

### <a name="encrypted-backups"></a>Şifreli yedekleme

1. Merhaba yedeklemeleri şifrelemek için veritabanı motoru tarafından kullanılan SQL Server oturum açma toobe oluşturun ve hello kimlik bilgisi tooit ekleyin.

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

1. Yedekleme hello veritabanı hello asimetrik anahtarla hello anahtar kasasında depolanan şifreleme belirtme.

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a>Sütun düzeyinde şifreleme (Temizle)

Bu komut dosyası hello anahtar kasasında hello asimetrik anahtar tarafından korunan bir simetrik anahtar oluşturur ve ardından hello simetrik anahtar tooencrypt veri hello veritabanında kullanır.

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

## <a name="additional-resources"></a>Ek kaynaklar

Toouse bu şifreleme özellikleri nasıl görürüm hakkında daha fazla bilgi için [kullanarak EKM SQL Server şifreleme özellikleriyle](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).

Bu makaledeki adımları Hello bir Azure sanal makinede çalışan SQL Server zaten sahip olduğunuzu varsaymaktadır unutmayın. Aksi takdirde bkz [bir SQL Server sanal makinesi sağlama](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md). Azure Vm'lerinde SQL Server çalıştıran diğer yönergeler için bkz: [Azure sanal makinelere genel bakış SQL Server'da](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).
