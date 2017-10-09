---
title: "SQL veritabanı için olay dosyası kodu aaaXEvent | Microsoft Docs"
description: "PowerShell ve Transact-SQL hello olay dosyası hedef Azure SQL veritabanı genişletilmiş bir olay oluşturulduğunu gösteren bir iki aşamalı kod örnek sağlar. Azure depolama, bu senaryo, gerekli bir parçasıdır."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: bbb10ecc-739f-4159-b844-12b4be161231
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: genemi
ms.openlocfilehash: 4457bd3250f4644b54da2f7daddb9da12070e93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a>SQL veritabanı genişletilmiş olaylar için olay dosya hedef kodu

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Tam bir kod örneği, genişletilmiş bir olay için sağlam şekilde toocapture ve rapor bilgi istiyor.

Microsoft SQL Server'da hello [olay dosyası hedef](http://msdn.microsoft.com/library/ff878115.aspx) kullanılan toostore olay çıkışları bir yerel sabit sürücüye dosyasına değil. Ancak bu tür dosyaları kullanılabilir tooAzure SQL veritabanı değil. Bunun yerine hello Azure depolama hizmeti toosupport hello olay dosyası hedef kullanın.

Bu konuda iki aşamalı kod örneği gösterir:

* PowerShell, toocreate hello buluttaki bir Azure depolama kapsayıcısı.
* Transact-SQL:
  
  * tooassign hello Azure Storage kapsayıcısı tooan olay dosyası hedefi.
  * toocreate ve başlangıç hello olay oturumu ve benzeri.

## <a name="prerequisites"></a>Ön koşullar

* Bir Azure hesabı ve aboneliği [Ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.
* Herhangi bir veritabanı, bir tablodaki oluşturabilirsiniz.
  
  * İsteğe bağlı olarak yapabileceğiniz [oluşturma bir **AdventureWorksLT** demo veritabanı](sql-database-get-started.md) dakika.
* SQL Server Management Studio (ssms.exe), ideal olarak en son aylık güncelleştirme sürümü. 
  Merhaba son ssms.exe öğesinden yükleyebilirsiniz:
  
  * Başlıklı konuda [SQL Server Management Studio'yu indirme](http://msdn.microsoft.com/library/mt238290.aspx).
  * [Doğrudan bağlantı toohello indirme.](http://go.microsoft.com/fwlink/?linkid=616025)
* Merhaba olmalıdır [Azure PowerShell modülleri](http://go.microsoft.com/?linkid=9811175) yüklü.
  
  * Merhaba modülleri sağlar komutları gibi - **yeni AzureStorageAccount**.

## <a name="phase-1-powershell-code-for-azure-storage-container"></a>1. Aşama: Azure depolama kapsayıcısı PowerShell kodu

Bu PowerShell hello iki aşamalı kod örneği Aşama 1 ' dir.

Önceki olası çalıştırın ve rerunnable sonra hello betik komutları tooclean ile başlatılır.

1. Merhaba PowerShell Betiği Notepad.exe gibi basit bir metin düzenleyicisine yapıştırın ve hello uzantılı bir dosya olarak hello komut dosyasını kaydederseniz **.ps1**.
2. PowerShell ISE yönetici olarak başlatın.
3. Merhaba istemine yazın<br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/>ve ardından Enter tuşuna basın.
4. PowerShell ISE'yi açın, **.ps1** dosya. Merhaba komut dosyasını çalıştırın.
5. Merhaba komut dosyası ilk tooAzure içinde oturum yeni bir pencere başlatır.
   
   * Oturumunuz kesintiye uğratmadan hello komut dosyasını yeniden, hello yorum hello uygun seçeneğiniz **Add-AzureAccount** komutu.

![Azure Modülü yüklü hazır toorun betik ile PowerShell ISE.][30_powershell_ise]


### <a name="powershell-code"></a>PowerShell kodu

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after hello first run.
# Current PowerShell environment retains hello successful outcome.

'Expect a pop-up window in which you log in tooAzure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit hello values assigned toothese variables, especially hello first few!
'

# Ensure hello current date is between
# hello Expiry and Start time values that you edit here.

$subscriptionName    = 'YOUR_SUBSCRIPTION_NAME'
$policySasExpiryTime = '2016-01-28T23:44:56Z'
$policySasStartTime  = '2015-08-01'


$storageAccountName     = 'gmstorageaccountxevent'
$storageAccountLocation = 'West US'
$contextName            = 'gmcontext'
$containerName          = 'gmcontainerxevent'
$policySasToken         = 'gmpolicysastoken'


# Leave this value alone, as 'rwl'.
$policySasPermission = 'rwl'

#--------------- 3 -----------------------


# hello ending display lists your Azure subscriptions.
# One should match hello $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for hello current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up hello old Azure Storage Account after any previous run, 
before continuing this new run.'


If ($storageAccountName)
{
    Remove-AzureStorageAccount -StorageAccountName $storageAccountName
}

#--------------- 5 -----------------------

[System.DateTime]::Now.ToString()

'
Create a storage account. 
This might take several minutes, will beep when ready.
  ...PLEASE WAIT...'

New-AzureStorageAccount `
    -StorageAccountName $storageAccountName `
    -Location           $storageAccountLocation

[System.DateTime]::Now.ToString()

[System.Media.SystemSounds]::Beep.Play()


'
Get hello primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# hello context will be needed toocreate a container within hello storage account.

'Create a context object from hello storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within hello storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy toobe applied toohello SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for hello container.
'
Try
{
    $sasTokenWithPolicy = New-AzureStorageContainerSASToken `
        -Name    $containerName `
        -Context $context `
        -Policy  $policySasToken
}
Catch 
{
    $Error[0].Exception.ToString()
}

#-------------- 7 ------------------------


'Display hello values that YOU must edit into hello Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here toodelete your Azure Storage account. See hello preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift toohello Transact-SQL portion of hello two-part code sample!'

# EOFile
```


Sona erdiğinde, hello PowerShell Betiği yazdıran birkaç adlandırılmış değerler hello not edin. Bu değerleri hello Aşama 2 aşağıdaki Transact-SQL komut dosyası içine düzenlemeniz gerekir.

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a>2. Aşama: Azure Storage kapsayıcısını kullanan Transact-SQL kodu

* Aşamasında bu kod örneği, 1, bir Azure depolama kapsayıcısının bir PowerShell komut dosyası toocreate verdi.
* Sonraki aşama 2 hello aşağıdaki Transact-SQL betiği hello kapsayıcı kullanmanız gerekir.

Önceki olası çalıştırın ve rerunnable sonra hello betik komutları tooclean ile başlatılır.

Merhaba PowerShell Betiği birkaç adlandırılmış değerler yazdırıldığında bunu sona erdi. Bu değerleri hello Transact-SQL komut dosyası toouse düzenlemeniz gerekir. Bul **Yapılacaklar** hello Transact-SQL komut dosyası toolocate hello noktaları düzenleyin.

1. SQL Server Management Studio'yu (ssms.exe) açın.
2. Tooyour Azure SQL veritabanı veritabanına bağlanın.
3. Tooopen yeni bir sorgu bölmesine tıklayın.
4. Transact-SQL betiği hello sorgu bölmesine aşağıdaki hello yapıştırın.
5. Bulma her **Yapılacaklar** hello komut dosyası ve hello uygun düzenlemeleri yapın.
6. Kaydedin ve ardından hello komut dosyasını çalıştırın.


> [!WARNING]
> Merhaba PowerShell Betiği önceki hello tarafından oluşturulan SAS anahtarı değeri ile başlar bir '?' (soru işareti). T-SQL betiği aşağıdaki hello hello SAS anahtarı kullandığınızda, şunları yapmalısınız *hello başında Kaldır '?'* . Aksi takdirde çabalarınız güvenliği tarafından engellenmiş olabilir.


### <a name="transact-sql-code"></a>Transact-SQL kodunu

```sql
---- TODO: First, run hello PowerShell portion of this two-part code sample.
---- TODO: Second, find every 'TODO' in this Transact-SQL file, and edit each.

---- Transact-SQL code for Event File target on Azure SQL Database.


SET NOCOUNT ON;
GO


----  Step 1.  Establish one little table, and  ---------
----  insert one row of data.


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'gmTabEmployee')
BEGIN
    DROP TABLE gmTabEmployee;
END
GO


CREATE TABLE gmTabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO gmTabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO


------  Step 2.  Create key, and  ------------
------  Create credential (your Azure Storage container must already exist).


IF NOT EXISTS
    (SELECT * FROM sys.symmetric_keys
        WHERE symmetric_key_id = 101)
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '0C34C960-6621-4682-A123-C7EA08E3FC46' -- Or any newid().
END
GO


IF EXISTS
    (SELECT * FROM sys.database_scoped_credentials
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in hello long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  hello event session has an event with an action,
------  and a has a target.

IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'gmeventsessionname240b')
BEGIN
    DROP
        EVENT SESSION
            gmeventsessionname240b
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE

    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE 'UPDATE gmTabEmployee%'
            )
    ADD TARGET
        package0.event_file
            (
            -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
            -- Also, tweak hello .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start hello event session.  ----------------
------  Issue hello SQL Update statements that will be traced.
------  Then stop hello session.

------  Note: If hello target fails tooattach,
------  hello session must be stopped and restarted.

ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = START;
GO


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
GO


ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = STOP;
GO


-------------- Step 5.  Select hello results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and hello associated Container name.
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b',
                null, null, null
            );
GO


-------------- Step 6.  Clean up. ----------

DROP
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE;
GO

DROP DATABASE SCOPED CREDENTIAL
    -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount toodelete your Azure Storage account!';
GO
```


Çalıştırdığınızda hello hedef tooattach başarısız olursa, durdurmak ve hello olay oturumu yeniden başlatın:

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a>Çıktı

Merhaba Transact-SQL betiği tamamlandığında hello altında bir hücreyi tıklatın **event_data_XML** sütun başlığı. Bir  **<event>**  öğesi bir güncelleştirme deyim gösteren görüntülenir.

Bir işte  **<event>**  test sırasında oluşturulan öğe:


```xml
<event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T19:18:45.420Z">
  <data name="state">
    <value>0</value>
    <text>Normal</text>
  </data>
  <data name="line_number">
    <value>5</value>
  </data>
  <data name="offset">
    <value>148</value>
  </data>
  <data name="offset_end">
    <value>368</value>
  </data>
  <data name="statement">
    <value>UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe'</value>
  </data>
  <action name="sql_text" package="sqlserver">
    <value>

SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
</value>
  </action>
</event>
```


Sistem işlevi tooread hello event_file aşağıdaki Transact-SQL komut dosyası kullanılan hello önceki hello:

* [sys.fn_xe_file_target_read_file (Transact-SQL)](http://msdn.microsoft.com/library/cc280743.aspx)

Genişletilmiş olay verilerini hello görüntülemek için Gelişmiş Seçenekleri açıklaması şu adresten edinilebilir:

* [Gelişmiş genişletilmiş olaylar hedef verilerini görüntüleme](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a>SQL Server'da Hello kod örnek toorun dönüştürme

Microsoft SQL Server Transact-SQL örneği önceki toorun hello istediğinizi varsayın.

* Kolaylık olması için toocompletely Değiştir kullanmak hello Azure Storage kapsayıcısının basit bir dosyayla gibi istediğiniz **C:\myeventdata.xel**. Merhaba dosya toohello yerel bilgisayarın sabit sürücüsü SQL Server barındıran hello yazılacaktır.
* Transact-SQL deyimi için herhangi bir tür ihtiyaç duymaz **CREATE MASTER KEY** ve **kimlik bilgisi Oluştur**.
* Merhaba, **oluşturma olay OTURUMU** deyimi içinde kendi **hedef Ekle** yan tümcesi, atanan hello Http değerini değiştirmek çok yapılan**filename =** gibibirtamyoldizesini **C:\myfile.xel**.
  
  * Azure depolama hesabı söz konusu.

## <a name="more-information"></a>Daha fazla bilgi

Hesapları ve Azure Storage hizmeti Merhaba kapsayıcılara hakkında daha fazla bilgi için bkz:

* [Nasıl toouse Blob depolama alanından .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [Adlandırma ve kapsayıcıları, Blobları ve meta verileri başvurma](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [Kök kapsayıcı Hello ile çalışma](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [Ders 1: bir Azure kapsayıcısı üzerinde depolanan erişim ilkesi ve bir paylaşılan erişim imzası oluşturma](http://msdn.microsoft.com/library/dn466430.aspx)
  * [Ders 2: paylaşılan erişim imzası kullanarak bir SQL Server kimlik bilgisi oluşturma](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

