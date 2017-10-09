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
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="e9f23-104">SQL veritabanı genişletilmiş olaylar için olay dosya hedef kodu</span><span class="sxs-lookup"><span data-stu-id="e9f23-104">Event File target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="e9f23-105">Tam bir kod örneği, genişletilmiş bir olay için sağlam şekilde toocapture ve rapor bilgi istiyor.</span><span class="sxs-lookup"><span data-stu-id="e9f23-105">You want a complete code sample for a robust way toocapture and report information for an extended event.</span></span>

<span data-ttu-id="e9f23-106">Microsoft SQL Server'da hello [olay dosyası hedef](http://msdn.microsoft.com/library/ff878115.aspx) kullanılan toostore olay çıkışları bir yerel sabit sürücüye dosyasına değil.</span><span class="sxs-lookup"><span data-stu-id="e9f23-106">In Microsoft SQL Server, hello [Event File target](http://msdn.microsoft.com/library/ff878115.aspx) is used toostore event outputs into a local hard drive file.</span></span> <span data-ttu-id="e9f23-107">Ancak bu tür dosyaları kullanılabilir tooAzure SQL veritabanı değil.</span><span class="sxs-lookup"><span data-stu-id="e9f23-107">But such files are not available tooAzure SQL Database.</span></span> <span data-ttu-id="e9f23-108">Bunun yerine hello Azure depolama hizmeti toosupport hello olay dosyası hedef kullanın.</span><span class="sxs-lookup"><span data-stu-id="e9f23-108">Instead we use hello Azure Storage service toosupport hello Event File target.</span></span>

<span data-ttu-id="e9f23-109">Bu konuda iki aşamalı kod örneği gösterir:</span><span class="sxs-lookup"><span data-stu-id="e9f23-109">This topic presents a two-phase code sample:</span></span>

* <span data-ttu-id="e9f23-110">PowerShell, toocreate hello buluttaki bir Azure depolama kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="e9f23-110">PowerShell, toocreate an Azure Storage container in hello cloud.</span></span>
* <span data-ttu-id="e9f23-111">Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="e9f23-111">Transact-SQL:</span></span>
  
  * <span data-ttu-id="e9f23-112">tooassign hello Azure Storage kapsayıcısı tooan olay dosyası hedefi.</span><span class="sxs-lookup"><span data-stu-id="e9f23-112">tooassign hello Azure Storage container tooan Event File target.</span></span>
  * <span data-ttu-id="e9f23-113">toocreate ve başlangıç hello olay oturumu ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="e9f23-113">toocreate and start hello event session, and so on.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9f23-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e9f23-114">Prerequisites</span></span>

* <span data-ttu-id="e9f23-115">Bir Azure hesabı ve aboneliği</span><span class="sxs-lookup"><span data-stu-id="e9f23-115">An Azure account and subscription.</span></span> <span data-ttu-id="e9f23-116">[Ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9f23-116">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e9f23-117">Herhangi bir veritabanı, bir tablodaki oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9f23-117">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="e9f23-118">İsteğe bağlı olarak yapabileceğiniz [oluşturma bir **AdventureWorksLT** demo veritabanı](sql-database-get-started.md) dakika.</span><span class="sxs-lookup"><span data-stu-id="e9f23-118">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="e9f23-119">SQL Server Management Studio (ssms.exe), ideal olarak en son aylık güncelleştirme sürümü.</span><span class="sxs-lookup"><span data-stu-id="e9f23-119">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="e9f23-120">Merhaba son ssms.exe öğesinden yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e9f23-120">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="e9f23-121">Başlıklı konuda [SQL Server Management Studio'yu indirme](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9f23-121">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="e9f23-122">Doğrudan bağlantı toohello indirme.</span><span class="sxs-lookup"><span data-stu-id="e9f23-122">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)
* <span data-ttu-id="e9f23-123">Merhaba olmalıdır [Azure PowerShell modülleri](http://go.microsoft.com/?linkid=9811175) yüklü.</span><span class="sxs-lookup"><span data-stu-id="e9f23-123">You must have hello [Azure PowerShell modules](http://go.microsoft.com/?linkid=9811175) installed.</span></span>
  
  * <span data-ttu-id="e9f23-124">Merhaba modülleri sağlar komutları gibi - **yeni AzureStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="e9f23-124">hello modules provide commands such as - **New-AzureStorageAccount**.</span></span>

## <a name="phase-1-powershell-code-for-azure-storage-container"></a><span data-ttu-id="e9f23-125">1. Aşama: Azure depolama kapsayıcısı PowerShell kodu</span><span class="sxs-lookup"><span data-stu-id="e9f23-125">Phase 1: PowerShell code for Azure Storage container</span></span>

<span data-ttu-id="e9f23-126">Bu PowerShell hello iki aşamalı kod örneği Aşama 1 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e9f23-126">This PowerShell is phase 1 of hello two-phase code sample.</span></span>

<span data-ttu-id="e9f23-127">Önceki olası çalıştırın ve rerunnable sonra hello betik komutları tooclean ile başlatılır.</span><span class="sxs-lookup"><span data-stu-id="e9f23-127">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

1. <span data-ttu-id="e9f23-128">Merhaba PowerShell Betiği Notepad.exe gibi basit bir metin düzenleyicisine yapıştırın ve hello uzantılı bir dosya olarak hello komut dosyasını kaydederseniz **.ps1**.</span><span class="sxs-lookup"><span data-stu-id="e9f23-128">Paste hello PowerShell script into a simple text editor such as Notepad.exe, and save hello script as a file with hello extension **.ps1**.</span></span>
2. <span data-ttu-id="e9f23-129">PowerShell ISE yönetici olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="e9f23-129">Start PowerShell ISE as an Administrator.</span></span>
3. <span data-ttu-id="e9f23-130">Merhaba istemine yazın</span><span class="sxs-lookup"><span data-stu-id="e9f23-130">At hello prompt, type</span></span><br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/><span data-ttu-id="e9f23-131">ve ardından Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="e9f23-131">and then press Enter.</span></span>
4. <span data-ttu-id="e9f23-132">PowerShell ISE'yi açın, **.ps1** dosya.</span><span class="sxs-lookup"><span data-stu-id="e9f23-132">In PowerShell ISE, open your **.ps1** file.</span></span> <span data-ttu-id="e9f23-133">Merhaba komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9f23-133">Run hello script.</span></span>
5. <span data-ttu-id="e9f23-134">Merhaba komut dosyası ilk tooAzure içinde oturum yeni bir pencere başlatır.</span><span class="sxs-lookup"><span data-stu-id="e9f23-134">hello script first starts a new window in which you log in tooAzure.</span></span>
   
   * <span data-ttu-id="e9f23-135">Oturumunuz kesintiye uğratmadan hello komut dosyasını yeniden, hello yorum hello uygun seçeneğiniz **Add-AzureAccount** komutu.</span><span class="sxs-lookup"><span data-stu-id="e9f23-135">If you rerun hello script without disrupting your session, you have hello convenient option of commenting out hello **Add-AzureAccount** command.</span></span>

![Azure Modülü yüklü hazır toorun betik ile PowerShell ISE.][30_powershell_ise]


### <a name="powershell-code"></a><span data-ttu-id="e9f23-137">PowerShell kodu</span><span class="sxs-lookup"><span data-stu-id="e9f23-137">PowerShell code</span></span>

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


<span data-ttu-id="e9f23-138">Sona erdiğinde, hello PowerShell Betiği yazdıran birkaç adlandırılmış değerler hello not edin.</span><span class="sxs-lookup"><span data-stu-id="e9f23-138">Take note of hello few named values that hello PowerShell script prints when it ends.</span></span> <span data-ttu-id="e9f23-139">Bu değerleri hello Aşama 2 aşağıdaki Transact-SQL komut dosyası içine düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9f23-139">You must edit those values into hello Transact-SQL script that follows as phase 2.</span></span>

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a><span data-ttu-id="e9f23-140">2. Aşama: Azure Storage kapsayıcısını kullanan Transact-SQL kodu</span><span class="sxs-lookup"><span data-stu-id="e9f23-140">Phase 2: Transact-SQL code that uses Azure Storage container</span></span>

* <span data-ttu-id="e9f23-141">Aşamasında bu kod örneği, 1, bir Azure depolama kapsayıcısının bir PowerShell komut dosyası toocreate verdi.</span><span class="sxs-lookup"><span data-stu-id="e9f23-141">In phase 1 of this code sample, you ran a PowerShell script toocreate an Azure Storage container.</span></span>
* <span data-ttu-id="e9f23-142">Sonraki aşama 2 hello aşağıdaki Transact-SQL betiği hello kapsayıcı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9f23-142">Next in phase 2, hello following Transact-SQL script must use hello container.</span></span>

<span data-ttu-id="e9f23-143">Önceki olası çalıştırın ve rerunnable sonra hello betik komutları tooclean ile başlatılır.</span><span class="sxs-lookup"><span data-stu-id="e9f23-143">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

<span data-ttu-id="e9f23-144">Merhaba PowerShell Betiği birkaç adlandırılmış değerler yazdırıldığında bunu sona erdi.</span><span class="sxs-lookup"><span data-stu-id="e9f23-144">hello PowerShell script printed a few named values when it ended.</span></span> <span data-ttu-id="e9f23-145">Bu değerleri hello Transact-SQL komut dosyası toouse düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9f23-145">You must edit hello Transact-SQL script toouse those values.</span></span> <span data-ttu-id="e9f23-146">Bul **Yapılacaklar** hello Transact-SQL komut dosyası toolocate hello noktaları düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="e9f23-146">Find **TODO** in hello Transact-SQL script toolocate hello edit points.</span></span>

1. <span data-ttu-id="e9f23-147">SQL Server Management Studio'yu (ssms.exe) açın.</span><span class="sxs-lookup"><span data-stu-id="e9f23-147">Open SQL Server Management Studio (ssms.exe).</span></span>
2. <span data-ttu-id="e9f23-148">Tooyour Azure SQL veritabanı veritabanına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="e9f23-148">Connect tooyour Azure SQL Database database.</span></span>
3. <span data-ttu-id="e9f23-149">Tooopen yeni bir sorgu bölmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9f23-149">Click tooopen a new query pane.</span></span>
4. <span data-ttu-id="e9f23-150">Transact-SQL betiği hello sorgu bölmesine aşağıdaki hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9f23-150">Paste hello following Transact-SQL script into hello query pane.</span></span>
5. <span data-ttu-id="e9f23-151">Bulma her **Yapılacaklar** hello komut dosyası ve hello uygun düzenlemeleri yapın.</span><span class="sxs-lookup"><span data-stu-id="e9f23-151">Find every **TODO** in hello script and make hello appropriate edits.</span></span>
6. <span data-ttu-id="e9f23-152">Kaydedin ve ardından hello komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9f23-152">Save, and then run hello script.</span></span>


> [!WARNING]
> <span data-ttu-id="e9f23-153">Merhaba PowerShell Betiği önceki hello tarafından oluşturulan SAS anahtarı değeri ile başlar bir '?' (soru işareti).</span><span class="sxs-lookup"><span data-stu-id="e9f23-153">hello SAS key value generated by hello preceding PowerShell script might begin with a '?' (question mark).</span></span> <span data-ttu-id="e9f23-154">T-SQL betiği aşağıdaki hello hello SAS anahtarı kullandığınızda, şunları yapmalısınız *hello başında Kaldır '?'* .</span><span class="sxs-lookup"><span data-stu-id="e9f23-154">When you use hello SAS key in hello following T-SQL script, you must *remove hello leading '?'*.</span></span> <span data-ttu-id="e9f23-155">Aksi takdirde çabalarınız güvenliği tarafından engellenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="e9f23-155">Otherwise your efforts might be blocked by security.</span></span>


### <a name="transact-sql-code"></a><span data-ttu-id="e9f23-156">Transact-SQL kodunu</span><span class="sxs-lookup"><span data-stu-id="e9f23-156">Transact-SQL code</span></span>

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


<span data-ttu-id="e9f23-157">Çalıştırdığınızda hello hedef tooattach başarısız olursa, durdurmak ve hello olay oturumu yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="e9f23-157">If hello target fails tooattach when you run, you must stop and restart hello event session:</span></span>

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a><span data-ttu-id="e9f23-158">Çıktı</span><span class="sxs-lookup"><span data-stu-id="e9f23-158">Output</span></span>

<span data-ttu-id="e9f23-159">Merhaba Transact-SQL betiği tamamlandığında hello altında bir hücreyi tıklatın **event_data_XML** sütun başlığı.</span><span class="sxs-lookup"><span data-stu-id="e9f23-159">When hello Transact-SQL script completes, click a cell under hello **event_data_XML** column header.</span></span> <span data-ttu-id="e9f23-160">Bir  **<event>**  öğesi bir güncelleştirme deyim gösteren görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e9f23-160">One **<event>** element is displayed which shows one UPDATE statement.</span></span>

<span data-ttu-id="e9f23-161">Bir işte  **<event>**  test sırasında oluşturulan öğe:</span><span class="sxs-lookup"><span data-stu-id="e9f23-161">Here is one **<event>** element that was generated during testing:</span></span>


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


<span data-ttu-id="e9f23-162">Sistem işlevi tooread hello event_file aşağıdaki Transact-SQL komut dosyası kullanılan hello önceki hello:</span><span class="sxs-lookup"><span data-stu-id="e9f23-162">hello preceding Transact-SQL script used hello following system function tooread hello event_file:</span></span>

* [<span data-ttu-id="e9f23-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="e9f23-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/cc280743.aspx)

<span data-ttu-id="e9f23-164">Genişletilmiş olay verilerini hello görüntülemek için Gelişmiş Seçenekleri açıklaması şu adresten edinilebilir:</span><span class="sxs-lookup"><span data-stu-id="e9f23-164">An explanation of advanced options for hello viewing of data from extended events is available at:</span></span>

* [<span data-ttu-id="e9f23-165">Gelişmiş genişletilmiş olaylar hedef verilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e9f23-165">Advanced Viewing of Target Data from Extended Events</span></span>](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a><span data-ttu-id="e9f23-166">SQL Server'da Hello kod örnek toorun dönüştürme</span><span class="sxs-lookup"><span data-stu-id="e9f23-166">Converting hello code sample toorun on SQL Server</span></span>

<span data-ttu-id="e9f23-167">Microsoft SQL Server Transact-SQL örneği önceki toorun hello istediğinizi varsayın.</span><span class="sxs-lookup"><span data-stu-id="e9f23-167">Suppose you wanted toorun hello preceding Transact-SQL sample on Microsoft SQL Server.</span></span>

* <span data-ttu-id="e9f23-168">Kolaylık olması için toocompletely Değiştir kullanmak hello Azure Storage kapsayıcısının basit bir dosyayla gibi istediğiniz **C:\myeventdata.xel**.</span><span class="sxs-lookup"><span data-stu-id="e9f23-168">For simplicity, you would want toocompletely replace use of hello Azure Storage container with a simple file such as **C:\myeventdata.xel**.</span></span> <span data-ttu-id="e9f23-169">Merhaba dosya toohello yerel bilgisayarın sabit sürücüsü SQL Server barındıran hello yazılacaktır.</span><span class="sxs-lookup"><span data-stu-id="e9f23-169">hello file would be written toohello local hard drive of hello computer that hosts SQL Server.</span></span>
* <span data-ttu-id="e9f23-170">Transact-SQL deyimi için herhangi bir tür ihtiyaç duymaz **CREATE MASTER KEY** ve **kimlik bilgisi Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="e9f23-170">You would not need any kind of Transact-SQL statements for **CREATE MASTER KEY** and **CREATE CREDENTIAL**.</span></span>
* <span data-ttu-id="e9f23-171">Merhaba, **oluşturma olay OTURUMU** deyimi içinde kendi **hedef Ekle** yan tümcesi, atanan hello Http değerini değiştirmek çok yapılan**filename =** gibibirtamyoldizesini **C:\myfile.xel**.</span><span class="sxs-lookup"><span data-stu-id="e9f23-171">In hello **CREATE EVENT SESSION** statement, in its **ADD TARGET** clause, you would replace hello Http value assigned made too**filename=** with a full path string like **C:\myfile.xel**.</span></span>
  
  * <span data-ttu-id="e9f23-172">Azure depolama hesabı söz konusu.</span><span class="sxs-lookup"><span data-stu-id="e9f23-172">No Azure Storage account need be involved.</span></span>

## <a name="more-information"></a><span data-ttu-id="e9f23-173">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="e9f23-173">More information</span></span>

<span data-ttu-id="e9f23-174">Hesapları ve Azure Storage hizmeti Merhaba kapsayıcılara hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="e9f23-174">For more info about accounts and containers in hello Azure Storage service, see:</span></span>

* [<span data-ttu-id="e9f23-175">Nasıl toouse Blob depolama alanından .NET</span><span class="sxs-lookup"><span data-stu-id="e9f23-175">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="e9f23-176">Adlandırma ve kapsayıcıları, Blobları ve meta verileri başvurma</span><span class="sxs-lookup"><span data-stu-id="e9f23-176">Naming and Referencing Containers, Blobs, and Metadata</span></span>](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [<span data-ttu-id="e9f23-177">Kök kapsayıcı Hello ile çalışma</span><span class="sxs-lookup"><span data-stu-id="e9f23-177">Working with hello Root Container</span></span>](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [<span data-ttu-id="e9f23-178">Ders 1: bir Azure kapsayıcısı üzerinde depolanan erişim ilkesi ve bir paylaşılan erişim imzası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e9f23-178">Lesson 1: Create a stored access policy and a shared access signature on an Azure container</span></span>](http://msdn.microsoft.com/library/dn466430.aspx)
  * [<span data-ttu-id="e9f23-179">Ders 2: paylaşılan erişim imzası kullanarak bir SQL Server kimlik bilgisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e9f23-179">Lesson 2: Create a SQL Server credential using a shared access signature</span></span>](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

