---
title: "aaaGetting başlatılan esnek veritabanı işleriyle | Microsoft Docs"
description: "nasıl toouse esnek veritabanı işleri"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 2540de0e-2235-4cdd-9b6a-b841adba00e5
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: bc5894d2df4235738ab961db4f69c11cdf786cc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a>Esnek veritabanı işlerine Başlarken
Esnek veritabanı iş (Önizleme) tooreliability sağlayan Azure SQL veritabanı için birden fazla veritabanı otomatik olarak yeniden denenmeden sırasında span T-SQL betiklerini yürütmek ve nihai tamamlama sağlama güvence altına alır. Merhaba hello esnek veritabanı iş özelliği hakkında daha fazla bilgi için lütfen bkz [özelliği genel bakış sayfasında](sql-database-elastic-jobs-overview.md).

Bu konuda bulunan hello örnek genişletir [esnek veritabanı araçlarını kullanmaya başlama](sql-database-elastic-scale-get-started.md). Tamamlandığında, şunları yapacaksınız: öğrenin nasıl toocreate ve ilgili veritabanları grubunu yönetme işlerini yönetin. Gerekli toouse hello esnek ölçek sipariş tootake esnek iş hello yararları avantajlarından araçlarında olmadığı.

## <a name="prerequisites"></a>Ön koşullar
İndirme ve çalıştırma hello [esnek veritabanı araçlarını örneği ile çalışmaya başlama](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Merhaba örnek uygulaması kullanarak Yöneticisi bir parça eşlemesi oluşturma
Burada Yöneticisi birlikte hello parça veri ekleme tarafından izlenen birkaç parça parça eşleme oluşturur. Parçalı verileri ile ayarlanması parça zaten varsa, hello aşağıdaki adımları atlayın ve sonraki bölümde toohello taşıyın.

1. Derleme ve çalıştırma hello **esnek veritabanı araçlarını kullanmaya başlama** örnek uygulama. Adım 7 hello bölümünde kadar Hello adımları [hello örnek uygulamasını indirme ve çalıştırma](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). Adım 7 Hello sonunda, komut istemine aşağıdaki hello görürsünüz:

   ![Komut İstemi](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. Merhaba komut penceresinde "1" yazın ve tuşuna basın **Enter**. Bu hello parça eşleme Yöneticisi oluşturur ve iki parça toohello sunucu ekler. Daha sonra "3" yazın ve basın **Enter**; Bu eylem dört kez yineler. Bu örnek verileri satır, parça ekler.
3. Merhaba [Azure Portal](https://portal.azure.com) üç yeni veritabanları göstermesi gerekir:

   ![Visual Studio onayı](./media/sql-database-elastic-query-getting-started/portal.png)

   Bu noktada, tüm hello veritabanları hello parça eşlemesindeki yansıtan özel veritabanını koleksiyonu oluşturacağız. Bu, bize toocreate izin ve yeni bir tablo arasında parça eklemek bir işi çalıştırın.

Burada size genellikle bir parça eşleme hedef hello kullanarak oluşturacak **yeni AzureSqlJobTarget** cmdlet'i. Hello parça eşleme manager veritabanının veritabanı hedef olarak ayarlanmış olması gerekir ve ardından hello belirli parça eşleme hedef olarak belirtilir. Bunun yerine, biz giderek tooenumerate tüm hello hello Server'daki veritabanlarıdır ve hello veritabanları toohello yeni özel koleksiyon ana veritabanı hello durumla ekleyin.

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a>Özel bir koleksiyon oluşturur ve tüm veritabanları hello sunucusu toohello özel koleksiyon hedef ana hello durumla ekleyin.
   ```
    $customCollectionName = "dbs_in_server"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $ResourceGroupName = "ddove_samples"
    $ServerName = "samples"
    $dbsinserver = Get-AzureRMSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName
    $dbsinserver | %{
    $currentdb = $_.DatabaseName
    $ErrorActionPreference = "Stop"
    Write-Output ""

    Try
    {
       New-AzureSqlJobTarget -ServerName $ServerName -DatabaseName $currentdb | Write-Output
    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already a database target."
        }

        else
        {
            throw $_
        }

    }

    Try
    {
        if ($currentdb -eq "master")
        {
            Write-Host $currentdb "will not be added custom collection target" $CustomCollectionName "."
        }

        else
        {
            Add-AzureSqlJobChildTarget -CustomCollectionName $CustomCollectionName -ServerName $ServerName -DatabaseName $currentdb
            Write-Host $currentdb "was added to" $CustomCollectionName "."
        }

    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already in hello custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Veritabanları arasında yürütme için T-SQL komut dosyası oluşturma
   ```
    $scriptName = "NewTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'Test')
    BEGIN
        CREATE TABLE Test(
            TestId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO Test(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script
   ```

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a>Merhaba iş tooexecute bir komut dosyası hello özel grubu veritabanları arasında oluştur

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a>Merhaba iş yürütme
PowerShell Betiği aşağıdaki hello kullanılan tooexecute var olan bir iş olabilir:

Değişken tooreflect istenen hello iş adı toohave yürütülen aşağıdaki hello güncelleştirin:

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a>Tek iş yürütme Hello durumunu alır
Kullanım hello aynı **Get-AzureSqlJobExecution** hello cmdlet'iyle **ıncludechildren'ın** parametresi tooview hello alt iş yürütmeleri durumunu öğesine hello her karşı her iş yürütme için belirli bir durumda Merhaba işi tarafından hedef veritabanı.

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a>Birden çok iş yürütmeleri arasında hello durumunu görüntüle
Merhaba **Get-AzureSqlJobExecution** cmdlet'i aracılığıyla sağlanan hello parametreleri filtre birden çok iş yürütmeleri kullanılan toodisplay olabilir birden fazla isteğe bağlı parametreler vardır. Merhaba aşağıdaki hello olası yolları toouse Get-AzureSqlJobExecution bazılarını göstermektedir:

Tüm etkin üst düzey iş yürütmeleri Al:

   ```
    Get-AzureSqlJobExecution
   ```

Etkin olmayan iş yürütmeleri dahil olmak üzere tüm üst düzey iş yürütmeleri Al:

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

Etkin olmayan iş yürütmeleri dahil olmak üzere sağlanan iş yürütme kimliği, tüm alt iş yürütmeleri Al:

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

Bir zamanlama kullanılarak oluşturulan tüm iş yürütmeleri almak / birleşimi etkin olmayan işler de dahil olmak üzere, iş:

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

Etkin olmayan işler de dahil olmak üzere bir belirtilen parça eşleme hedefleme tüm işleri Al:

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

Etkin olmayan işler de dahil olmak üzere belirtilen özel bir koleksiyonu hedefleyen tüm işleri Al:

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

Belirli iş yürütme içinde iş görev yürütmeleri Hello listesini al:

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

İş görev yürütme ayrıntıları alın:

PowerShell Betiği aşağıdaki hello kullanılan tooview hello yürütme hatalarını ayıklama özellikle yararlıdır iş görevi yürütmede ayrıntılarını olabilir.
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a>İş görevi yürütmeleri içinde hataları alma
Merhaba JobTaskExecution nesnesi hello yaşam döngüsü boyunca bir ileti özelliği birlikte hello görev için bir özellik içerir. Bir iş görevi yürütmede başarısız olursa hello yaşam döngüsü özelliği çok ayarlanacak*başarısız* ve toohello elde edilen özel durum iletisi ve kendi yığını hello ileti özelliği ayarlanacaktır. Bir işi başarılı olmadı önemli tooview hello için belirli bir işi başarılı olmadı iş görevleri ayrıntılarını olur.

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions)
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }
   ```

## <a name="waiting-for-a-job-execution-toocomplete"></a>İş yürütme toocomplete için bekleniyor
PowerShell Betiği aşağıdaki hello iş görev toocomplete için kullanılan toowait olabilir:

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

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

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy
   ```

### <a name="update-a-custom-execution-policy"></a>Özel yürütme ilkesini güncelleştirin
İstenen hello yürütme İlkesi tooupdate güncelleştirin:

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy
   ```

## <a name="cancel-a-job"></a>Bir işi iptal etme
Esnek veritabanı iş işleri iptal isteklerini destekler.  Esnek veritabanı iş şu anda yürütülmekte olan bir işi iptal isteği algılarsa, toostop hello iş deneyecek.

Esnek veritabanı iş iptal gerçekleştirebilirsiniz iki farklı yolu vardır:

1. Şu anda yürütülmekte olan iptal etme görevleri: bir görevi şu anda çalışırken iptal algılanırsa, şu anda yürütülmekte olan hello görev yönünü hello içinde iptal denenecek.  Örneğin: iptal çalışırken şu anda gerçekleştirilen uzun süre çalışan bir sorgusu ise, bir deneme toocancel hello sorgu olacaktır.
2. İptal etme görev yeniden deneme: iptal hello denetimi iş parçacığı tarafından algılanırsa, bir görev için yürütme başlatılmadan önce hello denetimi iş parçacığı hello görev başlatma önlemek ve hello isteği iptal edildi olarak bildirin.

İş iptali için üst iş istediyseniz hello iptal isteği hello üst iş ve tüm alt işlerini uyulacaktır.

toosubmit iptal isteği kullanmak hello **Stop-AzureSqlJobExecution** cmdlet'i ve kümesi hello **JobExecutionId** parametresi.

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a>Bir iş adı ve hello işin geçmişini sil
Esnek veritabanı iş işleri zaman uyumsuz silinmesini destekler. Bir işi silinmek üzere işaretlenmiş ve tüm iş yürütmeleri için hello işini tamamladıktan sonra hello sistem hello iş ve tüm iş geçmişini siler. Merhaba sistem etkin iş yürütmeleri otomatik olarak iptal etmek değil.  

Bunun yerine, Dur AzureSqlJobExecution çağrılan toocancel etkin iş yürütmeleri olması gerekir.

tootrigger iş silme, kullanım hello **Kaldır AzureSqlJob** cmdlet'i ve kümesi hello **JobName** parametresi.

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a>Özel veritabanını hedef oluşturma
Özel veritabanı hedefleri yürütme doğrudan veya bir özel veritabanı grubundaki eklemek için kullanılabilen esnek veritabanı işlerinde tanımlanabilir. Bu yana **esnek havuzlar** henüz doğrudan desteklenmeyen hello PowerShell API'leri, yalnızca bir özel veritabanı hedef ve hello havuzundaki tüm hello veritabanları kapsayan özel veritabanı koleksiyon hedef oluşturun.

Aşağıdaki değişkenleri tooreflect istenen hello veritabanı bilgilerle hello ayarlayın:

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a>Özel veritabanı koleksiyon hedef oluşturma
Özel veritabanı koleksiyon hedefi tanımlı tooenable yürütme arasında birden çok tanımlanmış veritabanı hedefi olabilir. Bir veritabanı grubu oluşturulduktan sonra veritabanları ilişkili toohello özel koleksiyon hedef olabilir.

Değişkenleri tooreflect hello istenen özel koleksiyon hedef yapılandırması aşağıdaki hello ayarlayın:

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a>Veritabanlarını tooa özel veritabanı koleksiyon hedefi ekleyin
Veritabanı hedefleri özel veritabanı koleksiyon hedefleri toocreate grubu ile ilişkili olabilir. Özel veritabanı koleksiyon hedef hedefleyen bir iş oluşturulduğunda, yürütme hello aynı anda genişletilmiş tootarget hello veritabanları ilişkili toohello grubu olacaktır.

İstenen hello veritabanı tooa belirli özel koleksiyon ekleyin:

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Özel veritabanı koleksiyon hedef içinde Hello veritabanları gözden geçirin
Kullanım hello **Get-AzureSqlJobTarget** cmdlet tooretrieve hello alt veritabanları özel veritabanı koleksiyon hedef içinde.

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Bir iş tooexecute özel veritabanı koleksiyon hedef arasında bir komut dosyası oluşturun
Kullanım hello **yeni AzureSqlJob** cmdlet toocreate özel veritabanı koleksiyon hedef tarafından tanımlanan veritabanlarının bir gruba göre bir işi. Esnek veritabanı iş karşılık gelen her tooa veritabanı hello özel veritabanı koleksiyon hedefle ilişkili ve hello betik her veritabanına karşı yürütüldüğünden emin olmayı birden çok alt işlere hello iş genişletin. Yeniden ıdempotent toobe dayanıklı tooretries betiklerdir önemlidir.

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a>Veritabanları arasında veri toplama
**Esnek veritabanı iş** grubu bir sorgu yürütülürken destekler ve hello sonuçları tooa belirtilen veritabanının tablo gönderir. Merhaba tablo, her veritabanı hello olgu toosee hello sorgunun sonuçlarını sonra sorgulanabilir. Bu zaman uyumsuz mekanizması tooexecute birçok veritabanı arasında bir sorgu sağlar. Geçici olarak devre dışı bırakılıyor hello veritabanlarından birini gibi hata durumları otomatik olarak yeniden deneme işlenir.

henüz yoksa, hello belirtilen hedef tablo otomatik olarak oluşturulur, hello eşleşen hello şeması sonuç kümesi döndürdü. Bir komut dosyası yürütme birden çok sonuç kümesi döndürürse, esnek veritabanı işlerini yalnızca hello ilk sağlanan bir toohello hedef tablo gönderir.

PowerShell Betiği aşağıdaki hello kullanılan tooexecute sonuçlarını belirtilen tabloya toplama bir komut dosyası olabilir. Bu komut dosyasını bir T-SQL betiği, tek bir sonuç kümesi çıkarır oluşturulup oluşturulmadığını ve bir özel veritabanı koleksiyon hedef oluşturulan varsayar.

Tooreflect hello istenen komut, kimlik bilgileri ve yürütme hedef aşağıdaki hello ayarlayın:

   ```
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
   ```

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a>Oluşturma ve veri toplama senaryoları için bir işi başlatma
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a>Bir iş tetikleyici kullanarak iş yürütme için bir zamanlama oluşturmak
PowerShell Betiği aşağıdaki hello kullanılan toocreate yeniden zamanlama olabilir. Bu komut dosyasını bir dakikalık bir zaman aralığı kullanır, ancak yeni AzureSqlJobSchedule - DayInterval, - HourInterval, - MonthInterval ve - WeekInterval parametreleri de destekler. Yalnızca bir kez yürütme zamanlamaları oluşturulabilir göre geçirme - kez.

Yeni bir zamanlama oluşturun:
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a>Bir iş tetikleyici toohave zaman zamanlamaya göre çalıştırılan bir iş oluşturun
Bir iş Tetikleyici tanımlı toohave yürütülen iş according tooa saat zamanlama olabilir. PowerShell Betiği aşağıdaki hello kullanılan toocreate iş tetikleyici olabilir.

Değişkenleri toocorrespond toohello istenen iş aşağıdaki hello ayarlayabilir ve zamanlayın:

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>Zamanlamaya göre yürütülmesini zamanlanmış ilişkilendirme toostop işi kaldırma
iş yürütme iş tetikleyici, hello iş tetikleyici aracılığıyla yinelenmeye toodiscontinue kaldırılabilir.
Yürütülmekte olan iş tetikleyici toostop bir işi kaldırma hello kullanarak according tooa zamanlaması **Kaldır AzureSqlJobTrigger** cmdlet'i.

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a>Esnek veritabanı sorgu sonuçları tooExcel alma
 Merhaba sonuçlarını bir sorgu tooan Excel dosyasını içeri aktarabilirsiniz.

1. Excel 2013'ü başlatın.
2. Toohello gidin **veri** Şerit.
3. Tıklatın **diğer kaynaklardan** tıklatıp **SQL Server'dan**.

   ![Excel Import diğer kaynaklardan](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. Merhaba, **Veri Bağlantı Sihirbazı** hello sunucu adını ve oturum açma kimlik bilgilerini yazın. Ardından **İleri**'ye tıklayın.
5. Merhaba iletişim kutusunda **hello verileri içeren Select hello veritabanı**seçin hello **ElasticDBQuery** veritabanı.
6. Select hello **müşteriler** tablo hello liste görünümünde ve tıklayın **sonraki**. Ardından **son**.
7. Merhaba, **veri içeri aktarma** formunda, altında **nasıl bu verileri tooview çalışma kitabınızı istediğinizi seçin**seçin **tablo** tıklatıp **Tamam**.

Tüm satırları hello **müşteriler** tablo, farklı parça içinde depolanan doldurmak hello Excel sayfası.

## <a name="next-steps"></a>Sonraki adımlar
Artık, Excel'in veri işlevleri de kullanabilirsiniz. Veritabanı adı, sunucu adıyla Hello bağlantı dizesi kullanın ve tooconnect BI ve veri tümleştirme araçları toohello esnek sorgu veritabanınızı kimlik bilgileri. SQL Server, aracı için bir veri kaynağı olarak desteklendiğinden emin olun. Toohello esnek sorgu veritabanını ve herhangi bir SQL Server veritabanı gibi dış tablolara ve SQL Server tablolarını aracınızı toowith bağlamak bakın.

### <a name="cost"></a>Maliyet
Merhaba esnek veritabanı sorgu özelliğini kullanmak için ek ücret yoktur. Ancak, şu anda bu özellik bir uç noktası olarak yalnızca premium veritabanlarında kullanılabilir, ancak hello parça herhangi bir hizmet katmanı olabilir.

Fiyatlandırma bilgileri için bkz: [SQL veritabanı fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/sql-database/).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
