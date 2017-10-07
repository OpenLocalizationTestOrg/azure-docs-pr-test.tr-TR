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
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="325d0-103">Esnek veritabanı işlerine Başlarken</span><span class="sxs-lookup"><span data-stu-id="325d0-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="325d0-104">Esnek veritabanı iş (Önizleme) tooreliability sağlayan Azure SQL veritabanı için birden fazla veritabanı otomatik olarak yeniden denenmeden sırasında span T-SQL betiklerini yürütmek ve nihai tamamlama sağlama güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="325d0-104">Elastic Database jobs (preview) for Azure SQL Database allows you tooreliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="325d0-105">Merhaba hello esnek veritabanı iş özelliği hakkında daha fazla bilgi için lütfen bkz [özelliği genel bakış sayfasında](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="325d0-105">For more information about hello Elastic Database job feature, please see hello [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="325d0-106">Bu konuda bulunan hello örnek genişletir [esnek veritabanı araçlarını kullanmaya başlama](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="325d0-106">This topic extends hello sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="325d0-107">Tamamlandığında, şunları yapacaksınız: öğrenin nasıl toocreate ve ilgili veritabanları grubunu yönetme işlerini yönetin.</span><span class="sxs-lookup"><span data-stu-id="325d0-107">When completed, you will: learn how toocreate and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="325d0-108">Gerekli toouse hello esnek ölçek sipariş tootake esnek iş hello yararları avantajlarından araçlarında olmadığı.</span><span class="sxs-lookup"><span data-stu-id="325d0-108">It is not required toouse hello Elastic Scale tools in order tootake advantage of hello benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="325d0-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="325d0-109">Prerequisites</span></span>
<span data-ttu-id="325d0-110">İndirme ve çalıştırma hello [esnek veritabanı araçlarını örneği ile çalışmaya başlama](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="325d0-110">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="325d0-111">Merhaba örnek uygulaması kullanarak Yöneticisi bir parça eşlemesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="325d0-111">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="325d0-112">Burada Yöneticisi birlikte hello parça veri ekleme tarafından izlenen birkaç parça parça eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="325d0-112">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="325d0-113">Parçalı verileri ile ayarlanması parça zaten varsa, hello aşağıdaki adımları atlayın ve sonraki bölümde toohello taşıyın.</span><span class="sxs-lookup"><span data-stu-id="325d0-113">If you already have shards set up with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="325d0-114">Derleme ve çalıştırma hello **esnek veritabanı araçlarını kullanmaya başlama** örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="325d0-114">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="325d0-115">Adım 7 hello bölümünde kadar Hello adımları [hello örnek uygulamasını indirme ve çalıştırma](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="325d0-115">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="325d0-116">Adım 7 Hello sonunda, komut istemine aşağıdaki hello görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="325d0-116">At hello end of Step 7, you will see hello following command prompt:</span></span>

   ![Komut İstemi](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="325d0-118">Merhaba komut penceresinde "1" yazın ve tuşuna basın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="325d0-118">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="325d0-119">Bu hello parça eşleme Yöneticisi oluşturur ve iki parça toohello sunucu ekler.</span><span class="sxs-lookup"><span data-stu-id="325d0-119">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="325d0-120">Daha sonra "3" yazın ve basın **Enter**; Bu eylem dört kez yineler.</span><span class="sxs-lookup"><span data-stu-id="325d0-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="325d0-121">Bu örnek verileri satır, parça ekler.</span><span class="sxs-lookup"><span data-stu-id="325d0-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="325d0-122">Merhaba [Azure Portal](https://portal.azure.com) üç yeni veritabanları göstermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="325d0-122">hello [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Visual Studio onayı](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="325d0-124">Bu noktada, tüm hello veritabanları hello parça eşlemesindeki yansıtan özel veritabanını koleksiyonu oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="325d0-124">At this point, we will create a custom database collection that reflects all hello databases in hello shard map.</span></span> <span data-ttu-id="325d0-125">Bu, bize toocreate izin ve yeni bir tablo arasında parça eklemek bir işi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="325d0-125">This will allow us toocreate and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="325d0-126">Burada size genellikle bir parça eşleme hedef hello kullanarak oluşturacak **yeni AzureSqlJobTarget** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="325d0-126">Here we would usually create a shard map target, using hello **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="325d0-127">Hello parça eşleme manager veritabanının veritabanı hedef olarak ayarlanmış olması gerekir ve ardından hello belirli parça eşleme hedef olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="325d0-127">hello shard map manager database must be set as a database target and then hello specific shard map is specified as a target.</span></span> <span data-ttu-id="325d0-128">Bunun yerine, biz giderek tooenumerate tüm hello hello Server'daki veritabanlarıdır ve hello veritabanları toohello yeni özel koleksiyon ana veritabanı hello durumla ekleyin.</span><span class="sxs-lookup"><span data-stu-id="325d0-128">Instead, we are going tooenumerate all hello databases in hello server and add hello databases toohello new custom collection with hello exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a><span data-ttu-id="325d0-129">Özel bir koleksiyon oluşturur ve tüm veritabanları hello sunucusu toohello özel koleksiyon hedef ana hello durumla ekleyin.</span><span class="sxs-lookup"><span data-stu-id="325d0-129">Creates a custom collection and add all databases in hello server toohello custom collection target with hello exception of master.</span></span>
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
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="325d0-130">Veritabanları arasında yürütme için T-SQL komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="325d0-130">Create a T-SQL Script for execution across databases</span></span>
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

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a><span data-ttu-id="325d0-131">Merhaba iş tooexecute bir komut dosyası hello özel grubu veritabanları arasında oluştur</span><span class="sxs-lookup"><span data-stu-id="325d0-131">Create hello job tooexecute a script across hello custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a><span data-ttu-id="325d0-132">Merhaba iş yürütme</span><span class="sxs-lookup"><span data-stu-id="325d0-132">Execute hello job</span></span>
<span data-ttu-id="325d0-133">PowerShell Betiği aşağıdaki hello kullanılan tooexecute var olan bir iş olabilir:</span><span class="sxs-lookup"><span data-stu-id="325d0-133">hello following PowerShell script can be used tooexecute an existing job:</span></span>

<span data-ttu-id="325d0-134">Değişken tooreflect istenen hello iş adı toohave yürütülen aşağıdaki hello güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="325d0-134">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="325d0-135">Tek iş yürütme Hello durumunu alır</span><span class="sxs-lookup"><span data-stu-id="325d0-135">Retrieve hello state of a single job execution</span></span>
<span data-ttu-id="325d0-136">Kullanım hello aynı **Get-AzureSqlJobExecution** hello cmdlet'iyle **ıncludechildren'ın** parametresi tooview hello alt iş yürütmeleri durumunu öğesine hello her karşı her iş yürütme için belirli bir durumda Merhaba işi tarafından hedef veritabanı.</span><span class="sxs-lookup"><span data-stu-id="325d0-136">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a><span data-ttu-id="325d0-137">Birden çok iş yürütmeleri arasında hello durumunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="325d0-137">View hello state across multiple job executions</span></span>
<span data-ttu-id="325d0-138">Merhaba **Get-AzureSqlJobExecution** cmdlet'i aracılığıyla sağlanan hello parametreleri filtre birden çok iş yürütmeleri kullanılan toodisplay olabilir birden fazla isteğe bağlı parametreler vardır.</span><span class="sxs-lookup"><span data-stu-id="325d0-138">hello **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="325d0-139">Merhaba aşağıdaki hello olası yolları toouse Get-AzureSqlJobExecution bazılarını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="325d0-139">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="325d0-140">Tüm etkin üst düzey iş yürütmeleri Al:</span><span class="sxs-lookup"><span data-stu-id="325d0-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="325d0-141">Etkin olmayan iş yürütmeleri dahil olmak üzere tüm üst düzey iş yürütmeleri Al:</span><span class="sxs-lookup"><span data-stu-id="325d0-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="325d0-142">Etkin olmayan iş yürütmeleri dahil olmak üzere sağlanan iş yürütme kimliği, tüm alt iş yürütmeleri Al:</span><span class="sxs-lookup"><span data-stu-id="325d0-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="325d0-143">Bir zamanlama kullanılarak oluşturulan tüm iş yürütmeleri almak / birleşimi etkin olmayan işler de dahil olmak üzere, iş:</span><span class="sxs-lookup"><span data-stu-id="325d0-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="325d0-144">Etkin olmayan işler de dahil olmak üzere bir belirtilen parça eşleme hedefleme tüm işleri Al:</span><span class="sxs-lookup"><span data-stu-id="325d0-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="325d0-145">Etkin olmayan işler de dahil olmak üzere belirtilen özel bir koleksiyonu hedefleyen tüm işleri Al:</span><span class="sxs-lookup"><span data-stu-id="325d0-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="325d0-146">Belirli iş yürütme içinde iş görev yürütmeleri Hello listesini al:</span><span class="sxs-lookup"><span data-stu-id="325d0-146">Retrieve hello list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="325d0-147">İş görev yürütme ayrıntıları alın:</span><span class="sxs-lookup"><span data-stu-id="325d0-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="325d0-148">PowerShell Betiği aşağıdaki hello kullanılan tooview hello yürütme hatalarını ayıklama özellikle yararlıdır iş görevi yürütmede ayrıntılarını olabilir.</span><span class="sxs-lookup"><span data-stu-id="325d0-148">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="325d0-149">İş görevi yürütmeleri içinde hataları alma</span><span class="sxs-lookup"><span data-stu-id="325d0-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="325d0-150">Merhaba JobTaskExecution nesnesi hello yaşam döngüsü boyunca bir ileti özelliği birlikte hello görev için bir özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="325d0-150">hello JobTaskExecution object includes a property for hello Lifecycle of hello task along with a Message property.</span></span> <span data-ttu-id="325d0-151">Bir iş görevi yürütmede başarısız olursa hello yaşam döngüsü özelliği çok ayarlanacak*başarısız* ve toohello elde edilen özel durum iletisi ve kendi yığını hello ileti özelliği ayarlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="325d0-151">If a job task execution failed, hello Lifecycle property will be set too*Failed* and hello Message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="325d0-152">Bir işi başarılı olmadı önemli tooview hello için belirli bir işi başarılı olmadı iş görevleri ayrıntılarını olur.</span><span class="sxs-lookup"><span data-stu-id="325d0-152">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

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

## <a name="waiting-for-a-job-execution-toocomplete"></a><span data-ttu-id="325d0-153">İş yürütme toocomplete için bekleniyor</span><span class="sxs-lookup"><span data-stu-id="325d0-153">Waiting for a job execution toocomplete</span></span>
<span data-ttu-id="325d0-154">PowerShell Betiği aşağıdaki hello iş görev toocomplete için kullanılan toowait olabilir:</span><span class="sxs-lookup"><span data-stu-id="325d0-154">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="325d0-155">Özel yürütme ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="325d0-155">Create a custom execution policy</span></span>
<span data-ttu-id="325d0-156">Esnek veritabanı iş destekler işleri başlatırken uygulanan özel yürütme ilkelerini oluşturma.</span><span class="sxs-lookup"><span data-stu-id="325d0-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="325d0-157">Yürütme ilkelerini tanımlamak için şu anda izin ver:</span><span class="sxs-lookup"><span data-stu-id="325d0-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="325d0-158">Adı: Merhaba yürütme İlkesi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="325d0-158">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="325d0-159">İş zaman aşımı: bir iş tarafından esnek veritabanı işi iptal edilecek önce toplam süre.</span><span class="sxs-lookup"><span data-stu-id="325d0-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="325d0-160">İlk yeniden deneme aralığı: Aralığı toowait ilk yeniden denemeden önce.</span><span class="sxs-lookup"><span data-stu-id="325d0-160">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="325d0-161">En fazla yeniden deneme aralığı: Yeniden deneme aralıkları toouse Cap.</span><span class="sxs-lookup"><span data-stu-id="325d0-161">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="325d0-162">Yeniden deneme aralığı geri Çekilme katsayısı: Katsayısı toocalculate hello sonraki aralıkta yeniden denemeler arasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="325d0-162">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="325d0-163">Merhaba aşağıdaki formül kullanılır: (ilk yeniden deneme aralığı) * Math.pow ((aralığı geri Çekilme katsayısı) (yeniden deneme sayısı) - 2).</span><span class="sxs-lookup"><span data-stu-id="325d0-163">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="325d0-164">En fazla deneme: hello sayısının işindeki yeniden deneme girişimleri tooperform.</span><span class="sxs-lookup"><span data-stu-id="325d0-164">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="325d0-165">Merhaba varsayılan yürütme İlkesi hello aşağıdaki değerleri kullanır:</span><span class="sxs-lookup"><span data-stu-id="325d0-165">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="325d0-166">Ad: Varsayılan yürütme İlkesi</span><span class="sxs-lookup"><span data-stu-id="325d0-166">Name: Default execution policy</span></span>
* <span data-ttu-id="325d0-167">İş zaman aşımı: 1 hafta</span><span class="sxs-lookup"><span data-stu-id="325d0-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="325d0-168">İlk yeniden deneme aralığı: 100 milisaniyede</span><span class="sxs-lookup"><span data-stu-id="325d0-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="325d0-169">En fazla yeniden deneme aralığı: 30 dakika</span><span class="sxs-lookup"><span data-stu-id="325d0-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="325d0-170">Yeniden deneme aralığı katsayısı: 2</span><span class="sxs-lookup"><span data-stu-id="325d0-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="325d0-171">En fazla deneme: 2.147.483.647</span><span class="sxs-lookup"><span data-stu-id="325d0-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="325d0-172">İstenen hello yürütme ilkesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="325d0-172">Create hello desired execution policy:</span></span>

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

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="325d0-173">Özel yürütme ilkesini güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="325d0-173">Update a custom execution policy</span></span>
<span data-ttu-id="325d0-174">İstenen hello yürütme İlkesi tooupdate güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="325d0-174">Update hello desired execution policy tooupdate:</span></span>

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

## <a name="cancel-a-job"></a><span data-ttu-id="325d0-175">Bir işi iptal etme</span><span class="sxs-lookup"><span data-stu-id="325d0-175">Cancel a job</span></span>
<span data-ttu-id="325d0-176">Esnek veritabanı iş işleri iptal isteklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="325d0-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="325d0-177">Esnek veritabanı iş şu anda yürütülmekte olan bir işi iptal isteği algılarsa, toostop hello iş deneyecek.</span><span class="sxs-lookup"><span data-stu-id="325d0-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="325d0-178">Esnek veritabanı iş iptal gerçekleştirebilirsiniz iki farklı yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="325d0-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="325d0-179">Şu anda yürütülmekte olan iptal etme görevleri: bir görevi şu anda çalışırken iptal algılanırsa, şu anda yürütülmekte olan hello görev yönünü hello içinde iptal denenecek.</span><span class="sxs-lookup"><span data-stu-id="325d0-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="325d0-180">Örneğin: iptal çalışırken şu anda gerçekleştirilen uzun süre çalışan bir sorgusu ise, bir deneme toocancel hello sorgu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="325d0-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="325d0-181">İptal etme görev yeniden deneme: iptal hello denetimi iş parçacığı tarafından algılanırsa, bir görev için yürütme başlatılmadan önce hello denetimi iş parçacığı hello görev başlatma önlemek ve hello isteği iptal edildi olarak bildirin.</span><span class="sxs-lookup"><span data-stu-id="325d0-181">Canceling Task Retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="325d0-182">İş iptali için üst iş istediyseniz hello iptal isteği hello üst iş ve tüm alt işlerini uyulacaktır.</span><span class="sxs-lookup"><span data-stu-id="325d0-182">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="325d0-183">toosubmit iptal isteği kullanmak hello **Stop-AzureSqlJobExecution** cmdlet'i ve kümesi hello **JobExecutionId** parametresi.</span><span class="sxs-lookup"><span data-stu-id="325d0-183">toosubmit a cancellation request, use hello **Stop-AzureSqlJobExecution** cmdlet and set hello **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a><span data-ttu-id="325d0-184">Bir iş adı ve hello işin geçmişini sil</span><span class="sxs-lookup"><span data-stu-id="325d0-184">Delete a job by name and hello job's history</span></span>
<span data-ttu-id="325d0-185">Esnek veritabanı iş işleri zaman uyumsuz silinmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="325d0-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="325d0-186">Bir işi silinmek üzere işaretlenmiş ve tüm iş yürütmeleri için hello işini tamamladıktan sonra hello sistem hello iş ve tüm iş geçmişini siler.</span><span class="sxs-lookup"><span data-stu-id="325d0-186">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="325d0-187">Merhaba sistem etkin iş yürütmeleri otomatik olarak iptal etmek değil.</span><span class="sxs-lookup"><span data-stu-id="325d0-187">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="325d0-188">Bunun yerine, Dur AzureSqlJobExecution çağrılan toocancel etkin iş yürütmeleri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="325d0-188">Instead, Stop-AzureSqlJobExecution must be invoked toocancel active job executions.</span></span>

<span data-ttu-id="325d0-189">tootrigger iş silme, kullanım hello **Kaldır AzureSqlJob** cmdlet'i ve kümesi hello **JobName** parametresi.</span><span class="sxs-lookup"><span data-stu-id="325d0-189">tootrigger job deletion, use hello **Remove-AzureSqlJob** cmdlet and set hello **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="325d0-190">Özel veritabanını hedef oluşturma</span><span class="sxs-lookup"><span data-stu-id="325d0-190">Create a custom database target</span></span>
<span data-ttu-id="325d0-191">Özel veritabanı hedefleri yürütme doğrudan veya bir özel veritabanı grubundaki eklemek için kullanılabilen esnek veritabanı işlerinde tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="325d0-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="325d0-192">Bu yana **esnek havuzlar** henüz doğrudan desteklenmeyen hello PowerShell API'leri, yalnızca bir özel veritabanı hedef ve hello havuzundaki tüm hello veritabanları kapsayan özel veritabanı koleksiyon hedef oluşturun.</span><span class="sxs-lookup"><span data-stu-id="325d0-192">Since **elastic pools** are not yet directly supported via hello PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="325d0-193">Aşağıdaki değişkenleri tooreflect istenen hello veritabanı bilgilerle hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="325d0-193">Set hello following variables tooreflect hello desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="325d0-194">Özel veritabanı koleksiyon hedef oluşturma</span><span class="sxs-lookup"><span data-stu-id="325d0-194">Create a custom database collection target</span></span>
<span data-ttu-id="325d0-195">Özel veritabanı koleksiyon hedefi tanımlı tooenable yürütme arasında birden çok tanımlanmış veritabanı hedefi olabilir.</span><span class="sxs-lookup"><span data-stu-id="325d0-195">A custom database collection target can be defined tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="325d0-196">Bir veritabanı grubu oluşturulduktan sonra veritabanları ilişkili toohello özel koleksiyon hedef olabilir.</span><span class="sxs-lookup"><span data-stu-id="325d0-196">After a database group is created, databases can be associated toohello custom collection target.</span></span>

<span data-ttu-id="325d0-197">Değişkenleri tooreflect hello istenen özel koleksiyon hedef yapılandırması aşağıdaki hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="325d0-197">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="325d0-198">Veritabanlarını tooa özel veritabanı koleksiyon hedefi ekleyin</span><span class="sxs-lookup"><span data-stu-id="325d0-198">Add databases tooa custom database collection target</span></span>
<span data-ttu-id="325d0-199">Veritabanı hedefleri özel veritabanı koleksiyon hedefleri toocreate grubu ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="325d0-199">Database targets can be associated with custom database collection targets toocreate a group of databases.</span></span> <span data-ttu-id="325d0-200">Özel veritabanı koleksiyon hedef hedefleyen bir iş oluşturulduğunda, yürütme hello aynı anda genişletilmiş tootarget hello veritabanları ilişkili toohello grubu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="325d0-200">Whenever a job is created that targets a custom database collection target, it will be expanded tootarget hello databases associated toohello group at hello time of execution.</span></span>

<span data-ttu-id="325d0-201">İstenen hello veritabanı tooa belirli özel koleksiyon ekleyin:</span><span class="sxs-lookup"><span data-stu-id="325d0-201">Add hello desired database tooa specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="325d0-202">Özel veritabanı koleksiyon hedef içinde Hello veritabanları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="325d0-202">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="325d0-203">Kullanım hello **Get-AzureSqlJobTarget** cmdlet tooretrieve hello alt veritabanları özel veritabanı koleksiyon hedef içinde.</span><span class="sxs-lookup"><span data-stu-id="325d0-203">Use hello **Get-AzureSqlJobTarget** cmdlet tooretrieve hello child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="325d0-204">Bir iş tooexecute özel veritabanı koleksiyon hedef arasında bir komut dosyası oluşturun</span><span class="sxs-lookup"><span data-stu-id="325d0-204">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="325d0-205">Kullanım hello **yeni AzureSqlJob** cmdlet toocreate özel veritabanı koleksiyon hedef tarafından tanımlanan veritabanlarının bir gruba göre bir işi.</span><span class="sxs-lookup"><span data-stu-id="325d0-205">Use hello **New-AzureSqlJob** cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="325d0-206">Esnek veritabanı iş karşılık gelen her tooa veritabanı hello özel veritabanı koleksiyon hedefle ilişkili ve hello betik her veritabanına karşı yürütüldüğünden emin olmayı birden çok alt işlere hello iş genişletin.</span><span class="sxs-lookup"><span data-stu-id="325d0-206">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="325d0-207">Yeniden ıdempotent toobe dayanıklı tooretries betiklerdir önemlidir.</span><span class="sxs-lookup"><span data-stu-id="325d0-207">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="325d0-208">Veritabanları arasında veri toplama</span><span class="sxs-lookup"><span data-stu-id="325d0-208">Data collection across databases</span></span>
<span data-ttu-id="325d0-209">**Esnek veritabanı iş** grubu bir sorgu yürütülürken destekler ve hello sonuçları tooa belirtilen veritabanının tablo gönderir.</span><span class="sxs-lookup"><span data-stu-id="325d0-209">**Elastic Database jobs** supports executing a query across a group of databases and sends hello results tooa specified database’s table.</span></span> <span data-ttu-id="325d0-210">Merhaba tablo, her veritabanı hello olgu toosee hello sorgunun sonuçlarını sonra sorgulanabilir.</span><span class="sxs-lookup"><span data-stu-id="325d0-210">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="325d0-211">Bu zaman uyumsuz mekanizması tooexecute birçok veritabanı arasında bir sorgu sağlar.</span><span class="sxs-lookup"><span data-stu-id="325d0-211">This provides an asynchronous mechanism tooexecute a query across many databases.</span></span> <span data-ttu-id="325d0-212">Geçici olarak devre dışı bırakılıyor hello veritabanlarından birini gibi hata durumları otomatik olarak yeniden deneme işlenir.</span><span class="sxs-lookup"><span data-stu-id="325d0-212">Failure cases such as one of hello databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="325d0-213">henüz yoksa, hello belirtilen hedef tablo otomatik olarak oluşturulur, hello eşleşen hello şeması sonuç kümesi döndürdü.</span><span class="sxs-lookup"><span data-stu-id="325d0-213">hello specified destination table will be automatically created if it does not yet exist, matching hello schema of hello returned result set.</span></span> <span data-ttu-id="325d0-214">Bir komut dosyası yürütme birden çok sonuç kümesi döndürürse, esnek veritabanı işlerini yalnızca hello ilk sağlanan bir toohello hedef tablo gönderir.</span><span class="sxs-lookup"><span data-stu-id="325d0-214">If a script execution returns multiple result sets, Elastic Database jobs will only send hello first one toohello provided destination table.</span></span>

<span data-ttu-id="325d0-215">PowerShell Betiği aşağıdaki hello kullanılan tooexecute sonuçlarını belirtilen tabloya toplama bir komut dosyası olabilir.</span><span class="sxs-lookup"><span data-stu-id="325d0-215">hello following PowerShell script can be used tooexecute a script collecting its results into a specified table.</span></span> <span data-ttu-id="325d0-216">Bu komut dosyasını bir T-SQL betiği, tek bir sonuç kümesi çıkarır oluşturulup oluşturulmadığını ve bir özel veritabanı koleksiyon hedef oluşturulan varsayar.</span><span class="sxs-lookup"><span data-stu-id="325d0-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="325d0-217">Tooreflect hello istenen komut, kimlik bilgileri ve yürütme hedef aşağıdaki hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="325d0-217">Set hello following tooreflect hello desired script, credentials, and execution target:</span></span>

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="325d0-218">Oluşturma ve veri toplama senaryoları için bir işi başlatma</span><span class="sxs-lookup"><span data-stu-id="325d0-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="325d0-219">Bir iş tetikleyici kullanarak iş yürütme için bir zamanlama oluşturmak</span><span class="sxs-lookup"><span data-stu-id="325d0-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="325d0-220">PowerShell Betiği aşağıdaki hello kullanılan toocreate yeniden zamanlama olabilir.</span><span class="sxs-lookup"><span data-stu-id="325d0-220">hello following PowerShell script can be used toocreate a reoccurring schedule.</span></span> <span data-ttu-id="325d0-221">Bu komut dosyasını bir dakikalık bir zaman aralığı kullanır, ancak yeni AzureSqlJobSchedule - DayInterval, - HourInterval, - MonthInterval ve - WeekInterval parametreleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="325d0-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="325d0-222">Yalnızca bir kez yürütme zamanlamaları oluşturulabilir göre geçirme - kez.</span><span class="sxs-lookup"><span data-stu-id="325d0-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="325d0-223">Yeni bir zamanlama oluşturun:</span><span class="sxs-lookup"><span data-stu-id="325d0-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="325d0-224">Bir iş tetikleyici toohave zaman zamanlamaya göre çalıştırılan bir iş oluşturun</span><span class="sxs-lookup"><span data-stu-id="325d0-224">Create a job trigger toohave a job executed on a time schedule</span></span>
<span data-ttu-id="325d0-225">Bir iş Tetikleyici tanımlı toohave yürütülen iş according tooa saat zamanlama olabilir.</span><span class="sxs-lookup"><span data-stu-id="325d0-225">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="325d0-226">PowerShell Betiği aşağıdaki hello kullanılan toocreate iş tetikleyici olabilir.</span><span class="sxs-lookup"><span data-stu-id="325d0-226">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="325d0-227">Değişkenleri toocorrespond toohello istenen iş aşağıdaki hello ayarlayabilir ve zamanlayın:</span><span class="sxs-lookup"><span data-stu-id="325d0-227">Set hello following variables toocorrespond toohello desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="325d0-228">Zamanlamaya göre yürütülmesini zamanlanmış ilişkilendirme toostop işi kaldırma</span><span class="sxs-lookup"><span data-stu-id="325d0-228">Remove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="325d0-229">iş yürütme iş tetikleyici, hello iş tetikleyici aracılığıyla yinelenmeye toodiscontinue kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="325d0-229">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span>
<span data-ttu-id="325d0-230">Yürütülmekte olan iş tetikleyici toostop bir işi kaldırma hello kullanarak according tooa zamanlaması **Kaldır AzureSqlJobTrigger** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="325d0-230">Remove a job trigger toostop a job from being executed according tooa schedule using hello **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="325d0-231">Esnek veritabanı sorgu sonuçları tooExcel alma</span><span class="sxs-lookup"><span data-stu-id="325d0-231">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="325d0-232">Merhaba sonuçlarını bir sorgu tooan Excel dosyasını içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="325d0-232">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="325d0-233">Excel 2013'ü başlatın.</span><span class="sxs-lookup"><span data-stu-id="325d0-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="325d0-234">Toohello gidin **veri** Şerit.</span><span class="sxs-lookup"><span data-stu-id="325d0-234">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="325d0-235">Tıklatın **diğer kaynaklardan** tıklatıp **SQL Server'dan**.</span><span class="sxs-lookup"><span data-stu-id="325d0-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Excel Import diğer kaynaklardan](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="325d0-237">Merhaba, **Veri Bağlantı Sihirbazı** hello sunucu adını ve oturum açma kimlik bilgilerini yazın.</span><span class="sxs-lookup"><span data-stu-id="325d0-237">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="325d0-238">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="325d0-238">Then click **Next**.</span></span>
5. <span data-ttu-id="325d0-239">Merhaba iletişim kutusunda **hello verileri içeren Select hello veritabanı**seçin hello **ElasticDBQuery** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="325d0-239">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="325d0-240">Select hello **müşteriler** tablo hello liste görünümünde ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="325d0-240">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="325d0-241">Ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="325d0-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="325d0-242">Merhaba, **veri içeri aktarma** formunda, altında **nasıl bu verileri tooview çalışma kitabınızı istediğinizi seçin**seçin **tablo** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="325d0-242">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="325d0-243">Tüm satırları hello **müşteriler** tablo, farklı parça içinde depolanan doldurmak hello Excel sayfası.</span><span class="sxs-lookup"><span data-stu-id="325d0-243">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="325d0-244">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="325d0-244">Next steps</span></span>
<span data-ttu-id="325d0-245">Artık, Excel'in veri işlevleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="325d0-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="325d0-246">Veritabanı adı, sunucu adıyla Hello bağlantı dizesi kullanın ve tooconnect BI ve veri tümleştirme araçları toohello esnek sorgu veritabanınızı kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="325d0-246">Use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="325d0-247">SQL Server, aracı için bir veri kaynağı olarak desteklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="325d0-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="325d0-248">Toohello esnek sorgu veritabanını ve herhangi bir SQL Server veritabanı gibi dış tablolara ve SQL Server tablolarını aracınızı toowith bağlamak bakın.</span><span class="sxs-lookup"><span data-stu-id="325d0-248">Refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="325d0-249">Maliyet</span><span class="sxs-lookup"><span data-stu-id="325d0-249">Cost</span></span>
<span data-ttu-id="325d0-250">Merhaba esnek veritabanı sorgu özelliğini kullanmak için ek ücret yoktur.</span><span class="sxs-lookup"><span data-stu-id="325d0-250">There is no additional charge for using hello Elastic Database query feature.</span></span> <span data-ttu-id="325d0-251">Ancak, şu anda bu özellik bir uç noktası olarak yalnızca premium veritabanlarında kullanılabilir, ancak hello parça herhangi bir hizmet katmanı olabilir.</span><span class="sxs-lookup"><span data-stu-id="325d0-251">However, at this time this feature is available only on premium databases as an end point, but hello shards can be of any service tier.</span></span>

<span data-ttu-id="325d0-252">Fiyatlandırma bilgileri için bkz: [SQL veritabanı fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="325d0-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
