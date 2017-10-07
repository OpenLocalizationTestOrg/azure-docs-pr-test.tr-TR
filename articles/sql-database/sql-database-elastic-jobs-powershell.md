---
title: "aaaCreate ve esnek işleri PowerShell kullanarak yönetme | Microsoft Docs"
description: "PowerShell toomanage Azure SQL Database havuzları kullanılan"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a>PowerShell (Önizleme) kullanarak SQL Database esnek işleri oluşturmak ve yönetmek

Merhaba PowerShell API'leri için **esnek veritabanı işleri** (Önizleme) içinde göre betikleri yürütülecek grubu tanımlamanıza olanak sağlar. Bu makalede gösterilmektedir nasıl toocreate ve yönetme **esnek veritabanı işleri** PowerShell cmdlet'lerini kullanarak. Bkz: [esnek iş genel bakış](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Ön koşullar
* Azure aboneliği. Ücretsiz deneme için bkz: [ücretsiz bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).
* Merhaba esnek veritabanı araçları ile oluşturulmuş bir veritabanları kümesi. Bkz: [esnek veritabanı araçlarını kullanmaya başlama](sql-database-elastic-scale-get-started.md).
* Azure PowerShell. Ayrıntılı bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](https://docs.microsoft.com/powershell/azure/overview).
* **Esnek veritabanı iş** PowerShell paketi: bkz [esnek veritabanı yükleme işleri](sql-database-elastic-jobs-service-installation.md)

### <a name="select-your-azure-subscription"></a>Azure aboneliğinizi seçin
tooselect hello abonelik, abonelik kimliği gerekir (**- Subscriptionıd**) veya abonelik adı (**varlığıyla - SubscriptionName**). Birden çok aboneliğiniz varsa hello çalıştırabilirsiniz **Get-AzureRmSubscription** cmdlet'i ve kopyalama hello istenen hello sonuç kümesinden abonelik bilgileri. Abonelik bilgilerinizi olduktan sonra komutunu tooset aşağıdaki hello hello varsayılan olarak bu abonelik çalıştırmak, yani işleri oluşturmaya ve yönetmeye için hedef hello:

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

Merhaba [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) kullanım toodevelop için önerilen ve PowerShell betikleri hello esnek veritabanı işleri karşı yürütün.

## <a name="elastic-database-jobs-objects"></a>Esnek veritabanı işleri nesneleri
Aşağıdaki tabloda tüm hello nesne türlerini Hello **esnek veritabanı işleri** açıklaması ve ilgili PowerShell API'lerinden birlikte.

<table style="width:100%">
  <tr>
    <th>Nesne türü</th>
    <th>Açıklama</th>
    <th>İlgili PowerShell API'leri</th>
  </tr>
  <tr>
    <td>Kimlik Bilgisi</td>
    <td>Toodatabases betiklerinin yürütülmesi veya DACPACs uygulamasının bağlanırken kullanıcı adı ve parola toouse. <p>Merhaba parola hello esnek veritabanı iş veritabanında saklamak tooand göndermeden önce şifrelenir.  Merhaba parola hello esnek veritabanı iş hizmeti ile oluşturulan ve hello yükleme betikten karşıya hello kimlik bilgisi tarafından şifresi çözülür.</td>
    <td><p>Get-AzureSqlJobCredential</p>
    <p>AzureSqlJobCredential yeni</p><p>Set-AzureSqlJobCredential</p></td></td>
  </tr>

  <tr>
    <td>Betik</td>
    <td>Transact-SQL komut dosyası toobe veritabanları arasında yürütme için kullanılır.  Merhaba hizmeti hataları bağlı hello betik yürütme işlemi yeniden deneyecek beri hello betik yazarı toobe ıdempotent olmalıdır.
    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>Get-AzureSqlJobContentDefinition</p>
    <p>AzureSqlJobContent yeni</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>

  <tr>
    <td>DACPAC</td>
    <td><a href="https://msdn.microsoft.com/library/ee210546.aspx">Veri katmanı uygulaması </a> veritabanları arasında uygulanan toobe paketi.

    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>AzureSqlJobContent yeni</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>
  <tr>
    <td>Veritabanı hedef</td>
    <td>Veritabanı ve sunucu işaret tooan Azure SQL veritabanı adı.

    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>AzureSqlJobTarget yeni</p>
    </td>
  </tr>
  <tr>
    <td>Parça eşleme hedef</td>
    <td>Bir veritabanı hedef ve bir kimlik bilgisi toobe birleşimi bir esnek veritabanı parça eşlemesi içinde depolanan toodetermine bilgileri kullanılır.
    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>AzureSqlJobTarget yeni</p>
    <p>Set-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Özel Toplama hedef</td>
    <td>Veritabanlarını toocollectively tanımlanan Grup yürütme için kullanın.</td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>AzureSqlJobTarget yeni</p>
    </td>
  </tr>
<tr>
    <td>Özel Toplama alt hedef</td>
    <td>Özel bir koleksiyondan başvurulan veritabanı hedefi.</td>
    <td>
    <p>Ekleme AzureSqlJobChildTarget</p>
    <p>Remove-AzureSqlJobChildTarget</p>
    </td>
  </tr>

<tr>
    <td>İş</td>
    <td>
    <p>Kullanılan tootrigger yürütme veya toofulfill bir zamanlama olabilir bir işin parametrelerini tanımı.</p>
    </td>
    <td>
    <p>Get-AzureSqlJob</p>
    <p>AzureSqlJob yeni</p>
    <p>Set-AzureSqlJob</p>
    </td>
  </tr>

<tr>
    <td>İş yürütme</td>
    <td>
    <p>Bir komut dosyası çalıştırma veya hataları olan veritabanı bağlantıları için kimlik bilgilerini kullanarak bir DACPAC tooa hedef uygulama görevleri gerekli toofulfill kapsayıcının uygun tooan yürütme İlkesi işlenir.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Bekleme AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>İş görevi yürütmede</td>
    <td>
    <p>İş toofulfill bir işi tek birimidir.</p>
    <p>Bir iş görevi mümkün toosuccessfully değilse yürütmek, hello ortaya çıkan özel durum iletisi oturum açmış olmanız ve yeni bir eşleşen iş görevi oluşturulur ve belirtilen belge toohello içinde yürütülen yürütme ilkesi.</p></p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Bekleme AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>İş yürütme İlkesi</td>
    <td>
    <p>Yürütme zaman aşımı, yeniden deneme sınırları ve aralıklarla yeniden denemeler arasında denetimleri işi.</p>
    <p>Esnek veritabanı iş denemeler arasındaki aralığı üstel geri alma ile temelde sonsuz yeniden deneme iş görevi başarısızlık neden varsayılan iş yürütme İlkesi içerir.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecutionPolicy</p>
    <p>AzureSqlJobExecutionPolicy yeni</p>
    <p>Set-AzureSqlJobExecutionPolicy</p>
    </td>
  </tr>

<tr>
    <td>Zamanlama</td>
    <td>
    <p>Zaman belirtimi yürütme tootake bağlantısı yeniden aralığı veya tek bir zaman için temel.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobSchedule</p>
    <p>AzureSqlJobSchedule yeni</p>
    <p>Set-AzureSqlJobSchedule</p>
    </td>
  </tr>

<tr>
    <td>İş Tetikleyicileri</td>
    <td>
    <p>Bir iş ve toohello zamanlamaya göre bir zamanlama tootrigger iş yürütme arasında bir eşleme.</p>
    </td>
    <td>
    <p>AzureSqlJobTrigger yeni</p>
    <p>Remove-AzureSqlJobTrigger</p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a>Desteklenen esnek veritabanı işleri türleri Grup
Merhaba iş Transact-SQL (T-SQL) komut dosyaları veya DACPACs uygulama grubu yürütür. Bir iş üzerinde yürütülen gönderilen toobe olduğunda veritabanlarının, hello iş "Merhaba burada her hello gerçekleştirir alt işlere genişletir" bir grup hello grubu tek bir veritabanında karşı yürütme istedi. 

İki tür oluşturabileceğiniz Grup vardır: 

* [Parça eşleme](sql-database-elastic-scale-shard-map-management.md) Grup: bir iş gönderilen tootarget parça eşleme olduğunda hello iş parça geçerli kümesini hello parça eşleme toodetermine sorgular ve ardından alt hello parça eşleminde her parça işleri oluşturur.
* Özel Toplama grubu: özel bir veritabanları kümesi tanımlı. Bir işi özel bir koleksiyona hedeflediğinde, alt işleri her veritabanı için şu anda hello özel koleksiyonunda oluşturur.

## <a name="tooset-hello-elastic-database-jobs-connection"></a>tooset hello esnek veritabanı iş bağlantısı
Bağlantı toobe kümesi toohello işleri gerekiyor *denetim veritabanı* önceki toousing hello API'leri işler. Bu cmdlet'ini çalıştırarak hello kullanıcı adı ve parola esnek veritabanı işleri yüklenirken oluşturulan isteyen oluşturan bir kimlik bilgisi penceresi toopop tetikler. Bu konu içinde sağlanan tüm örnekleri bu ilk adımı zaten gerçekleştirilen olduğunu varsayalım.

Bir bağlantı toohello esnek veritabanı işleri açın:

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a>Merhaba esnek veritabanı işleri içinde şifrelenmiş kimlik bilgileri
Veritabanı kimlik bilgileri hello işlere eklenebilir *denetim veritabanı* şifreli, parola ile. (İş zamanlamalarını kullanarak) daha sonraki bir zamanda yürütülen gerekli toostore kimlik bilgileri tooenable işleri toobe olur.

Şifreleme hello yükleme komut dosyasının bir parçası oluşturulan bir sertifika ile çalışır. Merhaba yükleme betiği oluşturur ve şifrelenmiş parolalar yüklemeleri hello sertifika hello verilerin şifresini çözmek için Azure bulut hizmeti hello içine depolanır. Daha sonra Azure bulut hizmeti Hello hello ortak anahtarı hello işleri içinde depolar *denetim veritabanı* hello sertifika gerektirmeden hello PowerShell API'si veya Klasik Azure portalı arabirimi tooencrypt sağlanan parola sağlar yerel olarak yüklenmiş toobe.

Merhaba kimlik bilgisi parolaları şifrelenmiş ve salt okunur erişim tooElastic veritabanı işleri nesneleri kullanıcılarla güvenli. Ancak kötü niyetli bir kullanıcının okuma-yazma erişimi tooElastic veritabanı işlerini nesneleri tooextract bir parola ile mümkündür. İş yürütmeleri arasında yeniden tasarlanmış toobe kimlik bilgileridir. Kimlik bilgileri tootarget veritabanları bağlantı kurulurken aktarılır. Şu anda hello hedef veritabanlarında her kimlik bilgisi için kullanılan bir kısıtlama yoktur, kötü amaçlı kullanıcı hello kötü niyetli bir kullanıcının denetimindeki bir veritabanı için veritabanı hedef ekleyebilirsiniz. Merhaba kullanıcı daha sonra bu veritabanını toogain hello kimlik bilgisi parola hedefleyen bir iş başlayamadı.

Esnek veritabanı işleri için en iyi yöntemler şunlardır:

* Merhaba API'leri tootrusted kişiler kullanımını sınırlayın.
* Kimlik bilgileri hello olmalıdır en az ayrıcalık gerekli tooperform hello iş görevi.  Daha fazla bilgi bu içinde görülebilir [yetkilendirme ve izinleri](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN makalesi.

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a>toocreate veritabanları arasında iş yürütme için şifrelenmiş bir kimlik bilgisi
Yeni bir şifrelenmiş toocreate kimlik bilgisi, hello [ **Get-Credential cmdlet** ](https://technet.microsoft.com/library/hh849815.aspx) ister bir kullanıcı adı ve toohello geçirilen parolası [ **yeni AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a>tooupdate kimlik bilgileri
Parolalar değiştirdiğinizde, hello kullan [ **Set-AzureSqlJobCredential cmdlet'i** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) ve kümesi hello **CredentialName** parametresi.

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a>toodefine bir esnek veritabanı parça eşleme hedefi
tooexecute parça kümesindeki tüm veritabanlarında bir işi (kullanılarak oluşturulan [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md)), bir parça eşleme hello veritabanı hedefi olarak kullanın. Bu örnek hello esnek veritabanı istemci kitaplığı kullanılarak oluşturulmuş bir parçalı uygulaması gerektirir. Bkz: [esnek veritabanı araçlarını örneği ile çalışmaya başlama](sql-database-elastic-scale-get-started.md).

Hello parça eşleme manager veritabanının veritabanı hedef olarak ayarlanmış olması gerekir ve hello belirli parça eşlemesi hedef olarak belirtildi.

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Veritabanları arasında yürütme için T-SQL komut dosyası oluşturma
Yürütme için T-SQL komut dosyalarını oluştururken, toobuild önerilir bunları toobe [ıdempotent](https://en.wikipedia.org/wiki/Idempotence) ve hatalarına karşı dayanıklı. Esnek veritabanı iş yürütme hello sınıflandırma hello hatanın bağımsız olarak bir hata karşılaştığında bir betik yürütme işlemi yeniden deneyecek.

Kullanım hello [ **yeni AzureSqlJobContent cmdlet** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate yürütme için bir komut dosyasını kaydedin ve ayarlama hello **- ContentName** ve **- CommandText**parametreleri.

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a>Bir dosyadan yeni bir komut dosyası oluşturma
Hello T-SQL komut dosyası içinde tanımlanmış olması durumunda, bu tooimport hello komut dosyasını kullanın:

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a>veritabanları arasında yürütme için tooupdate T-SQL komut dosyası
Bu PowerShell Betiği güncelleştirmeleri var olan bir komut dosyası için T-SQL komut metni hello.

Değişkenleri tooreflect hello aşağıdaki kümesi hello betik tanım toobe kümesini istenen:

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a>tooupdate hello tanımı tooan varolan komut dosyası
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a>toocreate iş tooexecute parça eşleme arasında bir komut dosyası
Bu PowerShell Betiği esnek ölçek parça eşlemesindeki her parça genelinde bir betik yürütme işlemi için bir iş başlatır.

Set hello değişkenleri tooreflect hello aşağıdaki komut dosyası ve hedef istenen:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a>tooexecute bir işi
Bu PowerShell komut dosyası var olan bir işi çalıştırır:

Değişken tooreflect istenen hello iş adı toohave yürütülen aşağıdaki hello güncelleştirin:

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a>tek iş yürütme tooretrieve hello durumu
Kullanım hello [ **Get-AzureSqlJobExecution cmdlet'i** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) ve kümesi hello **JobExecutionId** parametresi tooview hello iş yürütme durumu.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

Kullanım hello aynı **Get-AzureSqlJobExecution** hello cmdlet'iyle **ıncludechildren'ın** parametresi tooview hello alt iş yürütmeleri durumunu öğesine hello her karşı her iş yürütme için belirli bir durumda Merhaba işi tarafından hedef veritabanı.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a>birden çok iş yürütmeleri arasında tooview hello durumu
Merhaba [ **Get-AzureSqlJobExecution cmdlet'i** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) kullanılan toodisplay olabilecek birden çok isteğe bağlı sağlanan hello parametreleriyle filtre birden çok iş yürütmeleri sahiptir. Merhaba aşağıdaki hello olası yolları toouse Get-AzureSqlJobExecution bazılarını göstermektedir:

Tüm etkin üst düzey iş yürütmeleri Al:

    Get-AzureSqlJobExecution

Etkin olmayan iş yürütmeleri dahil olmak üzere tüm üst düzey iş yürütmeleri Al:

    Get-AzureSqlJobExecution -IncludeInactive

Etkin olmayan iş yürütmeleri dahil olmak üzere sağlanan iş yürütme kimliği, tüm alt iş yürütmeleri Al:

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

Bir zamanlama kullanılarak oluşturulan tüm iş yürütmeleri almak / birleşimi etkin olmayan işler de dahil olmak üzere, iş:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

Etkin olmayan işler de dahil olmak üzere bir belirtilen parça eşleme hedefleme tüm işleri Al:

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Etkin olmayan işler de dahil olmak üzere belirtilen özel bir koleksiyonu hedefleyen tüm işleri Al:

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Belirli iş yürütme içinde iş görev yürütmeleri Hello listesini al:

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

İş görev yürütme ayrıntıları alın:

PowerShell Betiği aşağıdaki hello kullanılan tooview hello yürütme hatalarını ayıklama özellikle yararlıdır iş görevi yürütmede ayrıntılarını olabilir.

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a>iş görevi yürütmeleri içinde tooretrieve hataları
Merhaba **JobTaskExecution nesne** bir ileti özelliği birlikte hello görevinin hello yaşam döngüsü için bir özellik içerir. Bir iş görevi yürütmede başarısız olursa hello yaşam döngüsü özelliği çok ayarlanacak*başarısız* ve toohello elde edilen özel durum iletisi ve kendi yığını hello ileti özelliği ayarlanacaktır. Bir işi başarılı olmadı önemli tooview hello için belirli bir işi başarılı olmadı iş görevleri ayrıntılarını olur.

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a>iş yürütme toocomplete toowait
PowerShell Betiği aşağıdaki hello iş görev toocomplete için kullanılan toowait olabilir:

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a>Özel yürütme ilkesi oluşturma
Esnek veritabanı iş destekler işleri başlatırken uygulanan özel yürütme ilkelerini oluşturma.

Yürütme ilkelerini tanımlamak için şu anda izin ver:

* Adı: Merhaba yürütme İlkesi tanımlayıcısı.
* İş zaman aşımı: bir iş tarafından esnek veritabanı işi iptal edilecek önce toplam süre.
* İlk yeniden deneme aralığı: Aralığı toowait ilk yeniden denemeden önce.
* En fazla yeniden deneme aralığı: Yeniden deneme aralıkları toouse Cap.
* Yeniden deneme aralığı geri Çekilme katsayısı: Katsayısı toocalculate hello sonraki aralıkta yeniden denemeler arasında kullanılır.  Merhaba aşağıdaki formül kullanılır: (ilk yeniden deneme aralığı) * Math.pow ((aralığı geri Çekilme katsayısı) (yeniden deneme sayısı) - 2). 
* En fazla deneme: hello sayısının işindeki yeniden deneme girişimleri tooperform.

Merhaba varsayılan yürütme İlkesi hello aşağıdaki değerleri kullanır:

* Ad: Varsayılan yürütme İlkesi
* İş zaman aşımı: 1 hafta
* İlk yeniden deneme aralığı: 100 milisaniyede
* En fazla yeniden deneme aralığı: 30 dakika
* Yeniden deneme aralığı katsayısı: 2
* En fazla deneme: 2.147.483.647

İstenen hello yürütme ilkesi oluşturun:

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a>Özel yürütme ilkesini güncelleştirin
İstenen hello yürütme İlkesi tooupdate güncelleştirin:

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a>Bir işi iptal etme
Esnek veritabanı iş işlerin iptal isteklerini destekler.  Esnek veritabanı iş şu anda yürütülmekte olan bir işi iptal isteği algılarsa, toostop hello iş deneyecek.

Esnek veritabanı iş iptal gerçekleştirebilirsiniz iki farklı yolu vardır:

1. Şu anda yürütülmekte olan görevleri iptal: bir görevi şu anda çalışırken iptal algılanırsa, şu anda yürütülmekte olan hello görev yönünü hello içinde iptal denenecek.  Örneğin: iptal çalışırken şu anda gerçekleştirilen uzun süre çalışan bir sorgusu ise, bir deneme toocancel hello sorgu olacaktır.
2. Görev yeniden deneme iptal etme: iptal hello denetimi iş parçacığı tarafından algılanırsa, bir görev için yürütme başlatılmadan önce hello denetimi iş parçacığı hello görev başlatma önlemek ve hello isteği iptal edildi olarak bildirin.

İş iptali için üst iş istediyseniz hello iptal isteği hello üst iş ve tüm alt işlerini uyulacaktır.

toosubmit iptal isteği kullanmak hello [ **Stop-AzureSqlJobExecution cmdlet'i** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) ve kümesi hello **JobExecutionId** parametresi.

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a>bir iş toodelete ve geçmiş zaman uyumsuz olarak iş
Esnek veritabanı iş işleri zaman uyumsuz silinmesini destekler. Bir işi silinmek üzere işaretlenmiş ve tüm iş yürütmeleri için hello işini tamamladıktan sonra hello sistem hello iş ve tüm iş geçmişini siler. Merhaba sistem etkin iş yürütmeleri otomatik olarak iptal etmek değil.  

Çağırma [ **Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel etkin iş yürütmeleri.

tootrigger iş silme, kullanım hello [ **Kaldır AzureSqlJob cmdlet** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) ve kümesi hello **JobName** parametresi.

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a>toocreate özel veritabanı hedef
Özel veritabanı hedefleri doğrudan yürütme veya eklenmek üzere bir özel veritabanı grubu içinde tanımlayabilirsiniz. Örneğin, çünkü **esnek havuzlar** olan henüz PowerShell API'lerini kullanarak doğrudan desteklenen, bir özel veritabanı hedef ve hello havuzundaki tüm hello veritabanları kapsayan özel veritabanı koleksiyon hedef oluşturabilirsiniz.

Aşağıdaki değişkenleri tooreflect istenen hello veritabanı bilgilerle hello ayarlayın:

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a>toocreate özel veritabanı koleksiyon hedef
Kullanım hello [ **yeni AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine özel veritabanı koleksiyon hedef tooenable yürütme arasında birden çok tanımlanmış veritabanı hedefi. Bir veritabanı grubu oluşturduktan sonra veritabanları hello özel koleksiyon hedefle ilişkili olabilir.

Değişkenleri tooreflect hello istenen özel koleksiyon hedef yapılandırması aşağıdaki hello ayarlayın:

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a>tooadd veritabanları tooa özel veritabanı koleksiyon hedef
tooadd veritabanı tooa belirli özel bir koleksiyona kullanmak hello [ **Ekle AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet'i.

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Özel veritabanı koleksiyon hedef içinde Hello veritabanları gözden geçirin
Kullanım hello [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello alt veritabanları özel veritabanı koleksiyon hedef içinde. 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Bir iş tooexecute özel veritabanı koleksiyon hedef arasında bir komut dosyası oluşturun
Kullanım hello [ **yeni AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate özel veritabanı koleksiyon hedef tarafından tanımlanan veritabanlarının bir gruba göre bir işi. Esnek veritabanı iş karşılık gelen her tooa veritabanı hello özel veritabanı koleksiyon hedefle ilişkili ve hello betik her veritabanına karşı yürütüldüğünden emin olmayı birden çok alt işlere hello iş genişletin. Yeniden ıdempotent toobe dayanıklı tooretries betiklerdir önemlidir.

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a>Veritabanları arasında veri toplama
İş tooexecute bir sorgu veritabanları arasında bir grup kullanın ve hello sonuçları tooa belirli tablo gönderin. Merhaba tablo, her veritabanı hello olgu toosee hello sorgunun sonuçlarını sonra sorgulanabilir. Bu zaman uyumsuz yöntem tooexecute birçok veritabanı arasında bir sorgu sağlar. Başarısız denemeleri otomatik yeniden denemeler işlenir.

henüz yoksa, hello belirtilen hedef tablo otomatik olarak oluşturulur. Merhaba yeni tablo sonuç kümesi döndürdü hello hello şeması eşleşir. Bir komut dosyası birden çok sonuç kümesi döndürürse, esnek veritabanı işlerini yalnızca hello ilk toohello hedef tablo gönderir.

Merhaba aşağıdaki PowerShell betiğini bir komut dosyası çalıştırır ve sonuçları belirtilen tabloya toplar. Bu komut dosyasını bir T-SQL betiği, tek bir sonuç kümesi çıkarır oluşturuldu ve bir özel veritabanı koleksiyon hedef oluşturulduğunu varsayar.

Bu komut dosyası hello kullanan [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet'i. Komut dosyası, kimlik bilgileri ve yürütme hedef Hello parametrelerini ayarlayın:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a>toocreate ve başlangıç bir işi veri toplama senaryoları
Bu komut dosyası hello kullanan [ **başlangıç AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet'i.

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a>tooschedule iş yürütme tetikleyici
PowerShell Betiği aşağıdaki hello kullanılan toocreate yinelenen bir zamanlama olabilir. Bu komut dosyasını bir dakika aralığı kullanır ancak [ **yeni AzureSqlJobSchedule** ](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) - DayInterval, - HourInterval, - MonthInterval ve - WeekInterval parametreleri de destekler. Yalnızca bir kez yürütme zamanlamaları oluşturulabilir göre geçirme - kez.

Yeni bir zamanlama oluşturun:

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a>tootrigger zaman zamanlamaya göre çalıştırılan bir iş
Bir iş Tetikleyici tanımlı toohave yürütülen iş according tooa saat zamanlama olabilir. PowerShell Betiği aşağıdaki hello kullanılan toocreate iş tetikleyici olabilir.

Kullanım [yeni AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) ve kümesi hello aşağıdaki değişkenleri toocorrespond toohello istenen iş ve zamanlaması:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>tooremove zamanlamaya göre yürütülmesini zamanlanmış ilişkilendirme toostop işi
iş yürütme iş tetikleyici, hello iş tetikleyici aracılığıyla yinelenmeye toodiscontinue kaldırılabilir. Yürütülmekte olan iş tetikleyici toostop bir işi kaldırma hello kullanarak according tooa zamanlaması [ **Kaldır AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a>İş Tetikleyicileri ilişkili tooa zamanlama alma
PowerShell Betiği aşağıdaki hello kullanılan tooobtain olması ve hello iş Tetikleyicileri kayıtlı tooa belirli zaman planı görüntüler.

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a>tooretrieve proje Tetikleyicileri ilişkili tooa işi
Kullanım [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) kayıtlı iş içeren tooobtain ve görüntü zamanlamaları.

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a>toocreate veritabanları arasında yürütme için veri katmanı uygulaması (DACPAC)
toocreate bir DACPAC bkz [veri katmanı uygulamaları](https://msdn.microsoft.com/library/ee210546.aspx). toodeploy bir DACPAC kullanmak hello [yeni AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent). Merhaba DACPAC erişilebilir toohello hizmeti olması gerekir. Bu oluşturmak ve oluşturulan DACPAC tooAzure depolama tooupload önerilen bir [paylaşılan erişim imzası](../storage/common/storage-dotnet-shared-access-signature-part-1.md) hello DACPAC için.

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a>tooupdate veritabanları arasında yürütme için veri katmanı uygulaması (DACPAC)
Esnek veritabanı iş içinde kayıtlı varolan DACPACs güncelleştirilmiş toopoint toonew URI'ler olabilir. Kullanım hello [ **Set-AzureSqlJobContentDefinition cmdlet'i** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) varolan üzerinde tooupdate hello DACPAC URI kayıtlı DACPAC:

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a>toocreate iş tooapply veritabanları arasında veri katmanı uygulaması (DACPAC)
Esnek veritabanı iş bir DACPAC oluşturulduktan sonra bir iş grubu tooapply hello DACPAC oluşturulabilir. PowerShell Betiği aşağıdaki hello kullanılan toocreate DACPAC iş özel koleksiyonu veritabanları arasında şunlar olabilir:

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
