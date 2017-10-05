---
title: "Esnek veritabanı işlerine Başlarken | Microsoft Docs"
description: "Esnek veritabanı işleri kullanma"
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
ms.openlocfilehash: 05c20e880d4eb1eacdecc0c4c7e7491dfe1e6a89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="40379-103">Esnek veritabanı işlerine Başlarken</span><span class="sxs-lookup"><span data-stu-id="40379-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="40379-104">Azure SQL Database esnek veritabanı işleri (Önizleme) sağlar, güvenilirlik için birden fazla veritabanı otomatik olarak yeniden deneniyor ve nihai tamamlama garanti sağlama sırasında span T-SQL komut dosyalarını çalıştır.</span><span class="sxs-lookup"><span data-stu-id="40379-104">Elastic Database jobs (preview) for Azure SQL Database allows you to reliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="40379-105">Esnek veritabanı iş özelliği hakkında daha fazla bilgi için lütfen bkz [özelliği genel bakış sayfasında](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40379-105">For more information about the Elastic Database job feature, please see the [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="40379-106">Bu konuda bulunan örnek genişletir [esnek veritabanı araçlarını kullanmaya başlama](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="40379-106">This topic extends the sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="40379-107">Tamamlandığında, şunları yapacaksınız: bir grup ilişkili veritabanlarını yönetmek işleri oluşturmak ve yönetmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="40379-107">When completed, you will: learn how to create and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="40379-108">Esnek iş avantajlarından yararlanmak için esnek ölçek araçlarını kullanmak için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="40379-108">It is not required to use the Elastic Scale tools in order to take advantage of the benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40379-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="40379-109">Prerequisites</span></span>
<span data-ttu-id="40379-110">İndirme ve çalıştırma [esnek veritabanı araçlarını örneği ile çalışmaya başlama](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="40379-110">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="40379-111">Harita manager örnek uygulamasını kullanarak bir parça oluşturma</span><span class="sxs-lookup"><span data-stu-id="40379-111">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="40379-112">Burada birkaç parça parça veri ekleme tarafından izlenen, birlikte Yöneticisi bir parça eşleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="40379-112">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="40379-113">Parçalı veriler bunlara ayarlayın parça zaten varsa, aşağıdaki adımları atlayın ve sonraki bölüme taşıyın.</span><span class="sxs-lookup"><span data-stu-id="40379-113">If you already have shards set up with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="40379-114">Derleme ve çalıştırma **esnek veritabanı araçlarını kullanmaya başlama** örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="40379-114">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="40379-115">Adım 7 bölümünde kadar adımları [örnek uygulamasını indirme ve çalıştırma](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="40379-115">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="40379-116">Adım 7 sonunda, aşağıdaki komut istemi görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="40379-116">At the end of Step 7, you will see the following command prompt:</span></span>

   ![Komut İstemi](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="40379-118">Komut penceresinde "1" yazın ve tuşuna basın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="40379-118">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="40379-119">Bu parça eşleme Yöneticisi oluşturur ve iki parça sunucusuna ekler.</span><span class="sxs-lookup"><span data-stu-id="40379-119">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="40379-120">Daha sonra "3" yazın ve basın **Enter**; Bu eylem dört kez yineler.</span><span class="sxs-lookup"><span data-stu-id="40379-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="40379-121">Bu örnek verileri satır, parça ekler.</span><span class="sxs-lookup"><span data-stu-id="40379-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="40379-122">[Azure Portal](https://portal.azure.com) üç yeni veritabanları göstermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="40379-122">The [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Visual Studio onayı](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="40379-124">Bu noktada, parça eşlemindeki tüm veritabanları yansıtan bir özel veritabanı koleksiyon oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="40379-124">At this point, we will create a custom database collection that reflects all the databases in the shard map.</span></span> <span data-ttu-id="40379-125">Bu, bize oluşturmak ve yeni bir tablo arasında parça ekleme işlemi yürütmek izin verir.</span><span class="sxs-lookup"><span data-stu-id="40379-125">This will allow us to create and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="40379-126">Burada size genellikle bir parça eşleme oluşturacak kullanarak hedef **yeni AzureSqlJobTarget** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="40379-126">Here we would usually create a shard map target, using the **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="40379-127">Parça eşleme manager veritabanı, veritabanı hedefi olarak ayarlamanız gerekir ve ardından belirli parça eşleme hedef olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="40379-127">The shard map manager database must be set as a database target and then the specific shard map is specified as a target.</span></span> <span data-ttu-id="40379-128">Bunun yerine, biz sunucudaki tüm veritabanları numaralandırır ve veritabanlarını yeni özel koleksiyon ana veritabanı dışında eklemek adımıdır.</span><span class="sxs-lookup"><span data-stu-id="40379-128">Instead, we are going to enumerate all the databases in the server and add the databases to the new custom collection with the exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-the-server-to-the-custom-collection-target-with-the-exception-of-master"></a><span data-ttu-id="40379-129">Özel bir koleksiyon oluşturur ve tüm veritabanları ana hariç olmak üzere özel koleksiyon hedef sunucu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="40379-129">Creates a custom collection and add all databases in the server to the custom collection target with the exception of master.</span></span>
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
             Write-Host $currentdb "is already in the custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="40379-130">Veritabanları arasında yürütme için T-SQL komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="40379-130">Create a T-SQL Script for execution across databases</span></span>
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

## <a name="create-the-job-to-execute-a-script-across-the-custom-group-of-databases"></a><span data-ttu-id="40379-131">Veritabanları özel grup arasında bir betik yürütmek için proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="40379-131">Create the job to execute a script across the custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-the-job"></a><span data-ttu-id="40379-132">İş yürütme</span><span class="sxs-lookup"><span data-stu-id="40379-132">Execute the job</span></span>
<span data-ttu-id="40379-133">Aşağıdaki PowerShell betiğini, varolan bir projeyi yürütmek için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="40379-133">The following PowerShell script can be used to execute an existing job:</span></span>

<span data-ttu-id="40379-134">Aşağıdaki değişkeni istenen iş yürütülmesini yansıtacak şekilde güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="40379-134">Update the following variable to reflect the desired job name to have executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="40379-135">Tek iş yürütme durumunu alır</span><span class="sxs-lookup"><span data-stu-id="40379-135">Retrieve the state of a single job execution</span></span>
<span data-ttu-id="40379-136">Aynı **Get-AzureSqlJobExecution** cmdlet'iyle **ıncludechildren'ın** öğesine her iş yürütme iş tarafından hedeflenen her bir veritabanına karşı özel durumu olan alt iş yürütmeleri durumunu görüntülemek için parametre.</span><span class="sxs-lookup"><span data-stu-id="40379-136">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-the-state-across-multiple-job-executions"></a><span data-ttu-id="40379-137">Birden çok iş yürütmeleri arasında durumunu görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="40379-137">View the state across multiple job executions</span></span>
<span data-ttu-id="40379-138">**Get-AzureSqlJobExecution** cmdlet'i aracılığıyla sağlanan parametreleri filtre birden çok iş yürütmeleri görüntülemek için kullanılan birden fazla isteğe bağlı parametreler vardır.</span><span class="sxs-lookup"><span data-stu-id="40379-138">The **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="40379-139">Get-AzureSqlJobExecution kullanmak için olası yollardan bazılarını şunlar gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="40379-139">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="40379-140">Tüm etkin üst düzey iş yürütmeleri Al:</span><span class="sxs-lookup"><span data-stu-id="40379-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="40379-141">Etkin olmayan iş yürütmeleri dahil olmak üzere tüm üst düzey iş yürütmeleri Al:</span><span class="sxs-lookup"><span data-stu-id="40379-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="40379-142">Etkin olmayan iş yürütmeleri dahil olmak üzere sağlanan iş yürütme kimliği, tüm alt iş yürütmeleri Al:</span><span class="sxs-lookup"><span data-stu-id="40379-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="40379-143">Bir zamanlama kullanılarak oluşturulan tüm iş yürütmeleri almak / birleşimi etkin olmayan işler de dahil olmak üzere, iş:</span><span class="sxs-lookup"><span data-stu-id="40379-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="40379-144">Etkin olmayan işler de dahil olmak üzere bir belirtilen parça eşleme hedefleme tüm işleri Al:</span><span class="sxs-lookup"><span data-stu-id="40379-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="40379-145">Etkin olmayan işler de dahil olmak üzere belirtilen özel bir koleksiyonu hedefleyen tüm işleri Al:</span><span class="sxs-lookup"><span data-stu-id="40379-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="40379-146">Belirli iş yürütme içinde iş görev yürütmeleri listesini al:</span><span class="sxs-lookup"><span data-stu-id="40379-146">Retrieve the list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="40379-147">İş görev yürütme ayrıntıları alın:</span><span class="sxs-lookup"><span data-stu-id="40379-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="40379-148">Aşağıdaki PowerShell betiğini yürütme hatalarını ayıklama özellikle yararlıdır iş görevi yürütmede ayrıntılarını görüntülemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="40379-148">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="40379-149">İş görevi yürütmeleri içinde hataları alma</span><span class="sxs-lookup"><span data-stu-id="40379-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="40379-150">JobTaskExecution nesnesi, görev bir ileti özelliği birlikte yaşam döngüsü için bir özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="40379-150">The JobTaskExecution object includes a property for the Lifecycle of the task along with a Message property.</span></span> <span data-ttu-id="40379-151">Bir iş görevi yürütmede başarısız olduysa, yaşam döngüsü özelliği olarak ayarlanacaktır *başarısız* ve sonuçta elde edilen özel durum iletisi ve kendi yığını ileti özelliği ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="40379-151">If a job task execution failed, the Lifecycle property will be set to *Failed* and the Message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="40379-152">Bir işi başarısız oldu, belirli bir iş için başarılı olmadı iş görevleri ayrıntılarını görüntülemek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="40379-152">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

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

## <a name="waiting-for-a-job-execution-to-complete"></a><span data-ttu-id="40379-153">Bir iş yürütmenin tamamlanması bekleniyor</span><span class="sxs-lookup"><span data-stu-id="40379-153">Waiting for a job execution to complete</span></span>
<span data-ttu-id="40379-154">Aşağıdaki PowerShell betiğini bir iş görevinin tamamlanmasını beklemek için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="40379-154">The following PowerShell script can be used to wait for a job task to complete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="40379-155">Özel yürütme ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="40379-155">Create a custom execution policy</span></span>
<span data-ttu-id="40379-156">Esnek veritabanı iş destekler işleri başlatırken uygulanan özel yürütme ilkelerini oluşturma.</span><span class="sxs-lookup"><span data-stu-id="40379-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="40379-157">Yürütme ilkelerini tanımlamak için şu anda izin ver:</span><span class="sxs-lookup"><span data-stu-id="40379-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="40379-158">Adı: Yürütme İlkesi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="40379-158">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="40379-159">İş zaman aşımı: bir iş tarafından esnek veritabanı işi iptal edilecek önce toplam süre.</span><span class="sxs-lookup"><span data-stu-id="40379-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="40379-160">İlk yeniden deneme aralığı: ilk yeniden denemeden önce beklenecek aralığı.</span><span class="sxs-lookup"><span data-stu-id="40379-160">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="40379-161">En fazla yeniden deneme aralığı: kullanılacak Cap yeniden deneme aralıkları.</span><span class="sxs-lookup"><span data-stu-id="40379-161">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="40379-162">Aralık geri Çekilme katsayısı yeniden deneme: Katsayısı sonraki yeniden deneme aralığını hesaplamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="40379-162">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="40379-163">Aşağıdaki formül kullanılır: (ilk yeniden deneme aralığı) * Math.pow ((aralığı geri Çekilme katsayısı) (yeniden deneme sayısı) - 2).</span><span class="sxs-lookup"><span data-stu-id="40379-163">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="40379-164">En fazla deneme: En fazla yeniden deneme sayısını içinde bir işi gerçekleştirmek çalışır.</span><span class="sxs-lookup"><span data-stu-id="40379-164">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="40379-165">Varsayılan yürütme ilkesi aşağıdaki değerleri kullanır:</span><span class="sxs-lookup"><span data-stu-id="40379-165">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="40379-166">Ad: Varsayılan yürütme İlkesi</span><span class="sxs-lookup"><span data-stu-id="40379-166">Name: Default execution policy</span></span>
* <span data-ttu-id="40379-167">İş zaman aşımı: 1 hafta</span><span class="sxs-lookup"><span data-stu-id="40379-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="40379-168">İlk yeniden deneme aralığı: 100 milisaniyede</span><span class="sxs-lookup"><span data-stu-id="40379-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="40379-169">En fazla yeniden deneme aralığı: 30 dakika</span><span class="sxs-lookup"><span data-stu-id="40379-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="40379-170">Yeniden deneme aralığı katsayısı: 2</span><span class="sxs-lookup"><span data-stu-id="40379-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="40379-171">En fazla deneme: 2.147.483.647</span><span class="sxs-lookup"><span data-stu-id="40379-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="40379-172">İstenen yürütme ilkesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="40379-172">Create the desired execution policy:</span></span>

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

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="40379-173">Özel yürütme ilkesini güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="40379-173">Update a custom execution policy</span></span>
<span data-ttu-id="40379-174">Güncelleştirmek için istenen yürütme İlkesi güncelleştirmesi:</span><span class="sxs-lookup"><span data-stu-id="40379-174">Update the desired execution policy to update:</span></span>

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

## <a name="cancel-a-job"></a><span data-ttu-id="40379-175">Bir işi iptal etme</span><span class="sxs-lookup"><span data-stu-id="40379-175">Cancel a job</span></span>
<span data-ttu-id="40379-176">Esnek veritabanı iş işleri iptal isteklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="40379-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="40379-177">Esnek veritabanı iş şu anda yürütülmekte olan bir işi iptal isteği algılarsa, işi durdurmayı deneyecek.</span><span class="sxs-lookup"><span data-stu-id="40379-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="40379-178">Esnek veritabanı iş iptal gerçekleştirebilirsiniz iki farklı yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="40379-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="40379-179">Şu anda yürütülmekte olan iptal etme görevleri: bir görevi şu anda çalışırken iptal algılanırsa, görevi şu anda yürütülen en boy içinde iptal denenir.</span><span class="sxs-lookup"><span data-stu-id="40379-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="40379-180">Örneğin: iptal çalışırken şu anda gerçekleştirilen uzun süre çalışan bir sorgusu ise, sorguyu iptal etme girişimi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="40379-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="40379-181">İptal etme görev yeniden deneme: iptal denetimi iş parçacığı tarafından algılanırsa, bir görev için yürütme başlatılmadan önce denetimi iş parçacığı görev başlatma önlemek ve istek iptal edildi olarak bildirin.</span><span class="sxs-lookup"><span data-stu-id="40379-181">Canceling Task Retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="40379-182">İş iptali için üst iş istediyseniz üst iş ve tüm alt işlerini iptal isteğini uyulacaktır.</span><span class="sxs-lookup"><span data-stu-id="40379-182">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="40379-183">İptal isteği göndermek için kullanmak **Stop-AzureSqlJobExecution** cmdlet'i ve **JobExecutionId** parametresi.</span><span class="sxs-lookup"><span data-stu-id="40379-183">To submit a cancellation request, use the **Stop-AzureSqlJobExecution** cmdlet and set the **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-the-jobs-history"></a><span data-ttu-id="40379-184">İş adı ve iş geçmişini sil</span><span class="sxs-lookup"><span data-stu-id="40379-184">Delete a job by name and the job's history</span></span>
<span data-ttu-id="40379-185">Esnek veritabanı iş işleri zaman uyumsuz silinmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="40379-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="40379-186">Bir işi silinmek üzere işaretlenmiş ve tüm iş yürütmeleri işi tamamlandıktan sonra sistem iş ve tüm iş geçmişi silinir.</span><span class="sxs-lookup"><span data-stu-id="40379-186">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="40379-187">Sistem etkin iş yürütmeleri otomatik olarak iptal etmek değil.</span><span class="sxs-lookup"><span data-stu-id="40379-187">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="40379-188">Bunun yerine, Dur AzureSqlJobExecution etkin iş yürütmeleri iptal etmek için çağrılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="40379-188">Instead, Stop-AzureSqlJobExecution must be invoked to cancel active job executions.</span></span>

<span data-ttu-id="40379-189">İş silme tetiklemek için kullanabileceğiniz **Kaldır AzureSqlJob** cmdlet'i ve ayarlayın **JobName** parametresi.</span><span class="sxs-lookup"><span data-stu-id="40379-189">To trigger job deletion, use the **Remove-AzureSqlJob** cmdlet and set the **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="40379-190">Özel veritabanını hedef oluşturma</span><span class="sxs-lookup"><span data-stu-id="40379-190">Create a custom database target</span></span>
<span data-ttu-id="40379-191">Özel veritabanı hedefleri yürütme doğrudan veya bir özel veritabanı grubundaki eklemek için kullanılabilen esnek veritabanı işlerinde tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="40379-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="40379-192">Bu yana **esnek havuzlar** henüz doğrudan desteklenmeyen PowerShell API'leri, yalnızca bir özel veritabanı hedef ve havuzdaki tüm veritabanları kapsayan özel veritabanı koleksiyon hedef oluşturun.</span><span class="sxs-lookup"><span data-stu-id="40379-192">Since **elastic pools** are not yet directly supported via the PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="40379-193">İstenen veritabanı bilgilerini yansıtmak için aşağıdaki değişkenleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="40379-193">Set the following variables to reflect the desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="40379-194">Özel veritabanı koleksiyon hedef oluşturma</span><span class="sxs-lookup"><span data-stu-id="40379-194">Create a custom database collection target</span></span>
<span data-ttu-id="40379-195">Özel veritabanı koleksiyon hedef yürütme arasında birden çok tanımlanmış veritabanı hedefleri etkinleştirmek için tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="40379-195">A custom database collection target can be defined to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="40379-196">Bir veritabanı grubu oluşturulduktan sonra özel toplama hedef veritabanları ilişkilendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="40379-196">After a database group is created, databases can be associated to the custom collection target.</span></span>

<span data-ttu-id="40379-197">İstenen özel koleksiyon hedef yapılandırmayı yansıtacak şekilde aşağıdaki değişkenleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="40379-197">Set the following variables to reflect the desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="40379-198">Özel veritabanını koleksiyonu hedefe veritabanları ekleme</span><span class="sxs-lookup"><span data-stu-id="40379-198">Add databases to a custom database collection target</span></span>
<span data-ttu-id="40379-199">Veritabanı hedefleri veritabanlarının bir grup oluşturmak için özel veritabanı koleksiyon hedefleri ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="40379-199">Database targets can be associated with custom database collection targets to create a group of databases.</span></span> <span data-ttu-id="40379-200">Özel veritabanı koleksiyon hedef hedefleyen bir iş oluşturulduğunda, yürütme sırasında grubu için ilişkili veritabanlarını hedeflemek için genişletilir.</span><span class="sxs-lookup"><span data-stu-id="40379-200">Whenever a job is created that targets a custom database collection target, it will be expanded to target the databases associated to the group at the time of execution.</span></span>

<span data-ttu-id="40379-201">İstenen veritabanı belirli özel bir koleksiyona ekleyin:</span><span class="sxs-lookup"><span data-stu-id="40379-201">Add the desired database to a specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="40379-202">Özel veritabanı koleksiyon hedef içinde veritabanları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="40379-202">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="40379-203">Kullanım **Get-AzureSqlJobTarget** özel veritabanı koleksiyon hedef içinde alt veritabanları almak üzere.</span><span class="sxs-lookup"><span data-stu-id="40379-203">Use the **Get-AzureSqlJobTarget** cmdlet to retrieve the child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="40379-204">Özel veritabanı koleksiyon hedef arasında bir betik yürütmek için bir proje oluşturun</span><span class="sxs-lookup"><span data-stu-id="40379-204">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="40379-205">Kullanım **yeni AzureSqlJob** özel veritabanı koleksiyon hedef tarafından tanımlanan veritabanlarının bir gruba göre bir iş oluşturmak için cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="40379-205">Use the **New-AzureSqlJob** cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="40379-206">Esnek veritabanı iş her bir veritabanına karşılık gelen özel veritabanı koleksiyon hedefle ilişkili birden çok alt işlere işi'ni genişletin ve komut dosyası her veritabanına karşı yürütülür emin olun.</span><span class="sxs-lookup"><span data-stu-id="40379-206">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="40379-207">Yeniden, komut dosyaları, deneme dayanıklı olmasını ıdempotent olduğunu önemlidir.</span><span class="sxs-lookup"><span data-stu-id="40379-207">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="40379-208">Veritabanları arasında veri toplama</span><span class="sxs-lookup"><span data-stu-id="40379-208">Data collection across databases</span></span>
<span data-ttu-id="40379-209">**Esnek veritabanı iş** grubu bir sorgu yürütülürken destekler ve sonuçları belirtilen veritabanının tabloya gönderir.</span><span class="sxs-lookup"><span data-stu-id="40379-209">**Elastic Database jobs** supports executing a query across a group of databases and sends the results to a specified database’s table.</span></span> <span data-ttu-id="40379-210">Tablonun her veritabanından sorgunun sonuçlarını görmek için Olgu sonra sorgulanabilir.</span><span class="sxs-lookup"><span data-stu-id="40379-210">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="40379-211">Bu, birçok veritabanı arasında bir sorguyu yürütmek için zaman uyumsuz bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="40379-211">This provides an asynchronous mechanism to execute a query across many databases.</span></span> <span data-ttu-id="40379-212">Geçici olarak devre dışı bırakılıyor veritabanlarından birini gibi hata durumları otomatik olarak yeniden deneme işlenir.</span><span class="sxs-lookup"><span data-stu-id="40379-212">Failure cases such as one of the databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="40379-213">Bunu henüz, döndürülen sonuç kümesi şemasını eşleştirme yoksa, belirtilen hedef tablonun otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="40379-213">The specified destination table will be automatically created if it does not yet exist, matching the schema of the returned result set.</span></span> <span data-ttu-id="40379-214">Bir komut dosyası yürütme birden çok sonuç kümesi döndürürse, esnek veritabanı işlerini yalnızca birinci sağlanan hedef tabloyla gönderir.</span><span class="sxs-lookup"><span data-stu-id="40379-214">If a script execution returns multiple result sets, Elastic Database jobs will only send the first one to the provided destination table.</span></span>

<span data-ttu-id="40379-215">Aşağıdaki PowerShell komut dosyası sonuçlarını belirtilen tabloya toplama bir betik yürütmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="40379-215">The following PowerShell script can be used to execute a script collecting its results into a specified table.</span></span> <span data-ttu-id="40379-216">Bu komut dosyasını bir T-SQL betiği, tek bir sonuç kümesi çıkarır oluşturulup oluşturulmadığını ve bir özel veritabanı koleksiyon hedef oluşturulan varsayar.</span><span class="sxs-lookup"><span data-stu-id="40379-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="40379-217">İstenen komut, kimlik bilgileri ve yürütme hedef yansıtmak için aşağıdakileri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="40379-217">Set the following to reflect the desired script, credentials, and execution target:</span></span>

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="40379-218">Oluşturma ve veri toplama senaryoları için bir işi başlatma</span><span class="sxs-lookup"><span data-stu-id="40379-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="40379-219">Bir iş tetikleyici kullanarak iş yürütme için bir zamanlama oluşturmak</span><span class="sxs-lookup"><span data-stu-id="40379-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="40379-220">Aşağıdaki PowerShell betiğini yeniden bir zamanlama oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="40379-220">The following PowerShell script can be used to create a reoccurring schedule.</span></span> <span data-ttu-id="40379-221">Bu komut dosyasını bir dakikalık bir zaman aralığı kullanır, ancak yeni AzureSqlJobSchedule - DayInterval, - HourInterval, - MonthInterval ve - WeekInterval parametreleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="40379-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="40379-222">Yalnızca bir kez yürütme zamanlamaları oluşturulabilir göre geçirme - kez.</span><span class="sxs-lookup"><span data-stu-id="40379-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="40379-223">Yeni bir zamanlama oluşturun:</span><span class="sxs-lookup"><span data-stu-id="40379-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-to-have-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="40379-224">Bir zaman zamanlamaya göre çalıştırılan bir iş için bir iş Tetikleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="40379-224">Create a job trigger to have a job executed on a time schedule</span></span>
<span data-ttu-id="40379-225">Bir iş tetikleyici bir saat zamanlamaya göre çalıştırılan bir iş için tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="40379-225">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="40379-226">Aşağıdaki PowerShell betiğini bir işi tetikleyici oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="40379-226">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="40379-227">İstenen iş ve zamanlama karşılık gelen için aşağıdaki değişkenleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="40379-227">Set the following variables to correspond to the desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="40379-228">Zamanlamaya göre yürütülmesini işini durdurmak için zamanlanmış bir ilişkilendirmesini Kaldır</span><span class="sxs-lookup"><span data-stu-id="40379-228">Remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="40379-229">Bir iş tetikleyici aracılığıyla yeniden iş yürütme kesmek için iş tetikleyici kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="40379-229">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span>
<span data-ttu-id="40379-230">Bir zamanlamaya göre çalıştırılmasını bir işi durdurmak için bir iş tetikleyiciyi kaldırmak **Kaldır AzureSqlJobTrigger** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="40379-230">Remove a job trigger to stop a job from being executed according to a schedule using the **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="40379-231">Esnek veritabanı sorgu sonuçları Excel'e Al</span><span class="sxs-lookup"><span data-stu-id="40379-231">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="40379-232">Gelen bir sorgunun sonuçlarını bir Excel dosyasını içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40379-232">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="40379-233">Excel 2013'ü başlatın.</span><span class="sxs-lookup"><span data-stu-id="40379-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="40379-234">Gidin **veri** Şerit.</span><span class="sxs-lookup"><span data-stu-id="40379-234">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="40379-235">Tıklatın **diğer kaynaklardan** tıklatıp **SQL Server'dan**.</span><span class="sxs-lookup"><span data-stu-id="40379-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Excel Import diğer kaynaklardan](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="40379-237">İçinde **Veri Bağlantı Sihirbazı** sunucu adını ve oturum açma kimlik bilgilerini yazın.</span><span class="sxs-lookup"><span data-stu-id="40379-237">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="40379-238">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="40379-238">Then click **Next**.</span></span>
5. <span data-ttu-id="40379-239">İletişim kutusunda **istediğiniz verileri içeren bir veritabanı seçin**seçin **ElasticDBQuery** veritabanı.</span><span class="sxs-lookup"><span data-stu-id="40379-239">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="40379-240">Seçin **müşteriler** Tablo liste görünümünde ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="40379-240">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="40379-241">Ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="40379-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="40379-242">İçinde **veri içeri aktarma** formunda, altında **nasıl çalışma kitabınızı bu verileri görüntülemek istediğinizi seçin**seçin **tablo** tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="40379-242">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="40379-243">Tüm satırların **müşteriler** tablo, farklı parça içinde depolanan doldurmak Excel sayfası.</span><span class="sxs-lookup"><span data-stu-id="40379-243">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40379-244">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="40379-244">Next steps</span></span>
<span data-ttu-id="40379-245">Artık, Excel'in veri işlevleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40379-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="40379-246">Bağlantı dizesi, BI ve veri tümleştirme araçları esnek sorgu veritabanına bağlanmak için sunucu adı, veritabanı adının ve kimlik bilgilerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="40379-246">Use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="40379-247">SQL Server, aracı için bir veri kaynağı olarak desteklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="40379-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="40379-248">Herhangi bir SQL Server veritabanı gibi dış tablolar ve aracı ile bağlanacağı SQL Server tablolarını ve esnek sorgu veritabanı bakın.</span><span class="sxs-lookup"><span data-stu-id="40379-248">Refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="40379-249">Maliyet</span><span class="sxs-lookup"><span data-stu-id="40379-249">Cost</span></span>
<span data-ttu-id="40379-250">Esnek veritabanı sorgu özelliğini kullanmak için ek ücret yoktur.</span><span class="sxs-lookup"><span data-stu-id="40379-250">There is no additional charge for using the Elastic Database query feature.</span></span> <span data-ttu-id="40379-251">Ancak, şu anda bu özellik bir uç noktası olarak yalnızca premium veritabanlarında kullanılabilir, ancak parça herhangi bir hizmet katmanı olabilir.</span><span class="sxs-lookup"><span data-stu-id="40379-251">However, at this time this feature is available only on premium databases as an end point, but the shards can be of any service tier.</span></span>

<span data-ttu-id="40379-252">Fiyatlandırma bilgileri için bkz: [SQL veritabanı fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="40379-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
