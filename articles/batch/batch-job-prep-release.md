---
title: "aaaCreate görevleri tooprepare işler ve işlem düğümlerinde - Azure Batch tam işleri | Microsoft Docs"
description: "Kullanım iş düzeyinde hazırlık görevleri toominimize verileri tooAzure toplu işlem düğümleri aktarım ve düğüm temizleme iş tamamlanma görevlerde bırakın."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="5a9b8-103">İş hazırlama ve iş sürüm görevleri toplu işlem düğümleri</span><span class="sxs-lookup"><span data-stu-id="5a9b8-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="5a9b8-104">Bir Azure toplu işlem, genellikle görevlerinin yürütülür ve Bakım görevlerinin tamamlandığında sonrası iş önce kurulum çeşit gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="5a9b8-105">Toodownload ortak görev giriş verisi tooyour işlem düğümleri gerekir ya da hello işi tamamlandıktan sonra görev çıktı verileri tooAzure depolama karşıya.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-105">You might need toodownload common task input data tooyour compute nodes, or upload task output data tooAzure Storage after hello job completes.</span></span> <span data-ttu-id="5a9b8-106">Kullanabileceğiniz **iş hazırlama** ve **iş yayın** tooperform bu işlemlerin görevler.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-106">You can use **job preparation** and **job release** tasks tooperform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="5a9b8-107">Hangi iş hazırlama ve görevleri?</span><span class="sxs-lookup"><span data-stu-id="5a9b8-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="5a9b8-108">Bir iş görevlerinin çalıştırmadan önce hello iş hazırlama görevi tüm işlem düğümleri zamanlanmış toorun üzerinde en az bir görev çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-108">Before a job's tasks run, hello job preparation task runs on all compute nodes scheduled toorun at least one task.</span></span> <span data-ttu-id="5a9b8-109">Hello işi tamamlandığında, hello iş bırakma görevi hello havuzun en az bir görev yürütmüş her düğümünde çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-109">Once hello job is completed, hello job release task runs on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="5a9b8-110">Normal toplu görevler gibi iş hazırlama değiştiğinde çağrılan bir komut satırı toobe belirtebilirsiniz veya bırakma görevini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-110">As with normal Batch tasks, you can specify a command line toobe invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="5a9b8-111">İş hazırlama ve bırakma görevleri dosya indirme gibi bilinen toplu görev özellikler sunar ([kaynak dosyaları][net_job_prep_resourcefiles]), yükseltilmiş yürütme, özel ortam değişkenleri, maksimum yürütme süresi, yeniden deneme sayısı ve dosyayı elde tutma süresi.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="5a9b8-112">Aşağıdaki bölümlerde hello bilgi edineceksiniz nasıl toouse hello [JobPreparationTask] [ net_job_prep] ve [JobReleaseTask] [ net_job_release] sınıfları hello bulundu [Batch .NET] [ api_net] kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-112">In hello following sections, you'll learn how toouse hello [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in hello [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="5a9b8-113">İş hazırlama ve bırakma görevleri "havuzu paylaşılan" ortamlarda, işlem düğümleri havuzu iş çalıştırmaları arasında devam ederse ve birçok iş tarafından kullanılan özellikle yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a><span data-ttu-id="5a9b8-114">Ne zaman toouse iş hazırlama ve görevleri bırakın</span><span class="sxs-lookup"><span data-stu-id="5a9b8-114">When toouse job preparation and release tasks</span></span>
<span data-ttu-id="5a9b8-115">İş hazırlama ve iş sürüm görevleri aşağıdaki durumlarda hello için iyi bir tercihtir şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5a9b8-115">Job preparation and job release tasks are a good fit for hello following situations:</span></span>

<span data-ttu-id="5a9b8-116">**Ortak görev verileri indirin**</span><span class="sxs-lookup"><span data-stu-id="5a9b8-116">**Download common task data**</span></span>

<span data-ttu-id="5a9b8-117">Toplu işlerin ortak bir veri kümesi hello iş görevleri için giriş olarak genellikle gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-117">Batch jobs often require a common set of data as input for hello job's tasks.</span></span> <span data-ttu-id="5a9b8-118">Örneğin, günlük risk analizi hesaplamalarda Pazar hello işteki iş özgü henüz ortak tooall görevleri verilerdir.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-118">For example, in daily risk analysis calculations, market data is job-specific, yet common tooall tasks in hello job.</span></span> <span data-ttu-id="5a9b8-119">Hello düğümü üzerinde çalışan herhangi bir görev kullanabilmesi bu Pazar veriler, genellikle birkaç gigabayt cinsinden boyutu, yalnızca bir kez indirilen tooeach işlem düğümü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-119">This market data, often several gigabytes in size, should be downloaded tooeach compute node only once so that any task that runs on hello node can use it.</span></span> <span data-ttu-id="5a9b8-120">Kullanım bir **iş hazırlama görevi** toodownload hello hello işinin yürütülmesi diğer görevleri kullanıcının önce bu veri tooeach düğümü.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-120">Use a **job preparation task** toodownload this data tooeach node before hello execution of hello job's other tasks.</span></span>

<span data-ttu-id="5a9b8-121">**İş ve Görev çıkış Sil**</span><span class="sxs-lookup"><span data-stu-id="5a9b8-121">**Delete job and task output**</span></span>

<span data-ttu-id="5a9b8-122">Burada bir havuzun işlem düğümleri işleri arasında yetkisi olmayan, bir "havuzu paylaşılan" ortamında çalıştırmaları arasında toodelete işi veri gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need toodelete job data between runs.</span></span> <span data-ttu-id="5a9b8-123">Tooconserve gerekebilecek disk alanı hello düğümlerde ya da kuruluşunuzun güvenlik ilkeleri karşılar.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-123">You might need tooconserve disk space on hello nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="5a9b8-124">Kullanım bir **iş bırakma görevi** iş hazırlama görevi tarafından indirilen, veya sırasında oluşturulan toodelete verilerin görev yürütme.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-124">Use a **job release task** toodelete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="5a9b8-125">**Günlük tutma**</span><span class="sxs-lookup"><span data-stu-id="5a9b8-125">**Log retention**</span></span>

<span data-ttu-id="5a9b8-126">Tookeep bir kopyasını, görevlerinizin oluşturduğu günlük dosyaları veya belki de başarısız uygulamalar tarafından oluşturulan kilitlenme bilgi döküm dosyaları isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-126">You might want tookeep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="5a9b8-127">Kullanım bir **iş bırakma görevi** bu gibi durumlarda toocompress içinde ve bu verileri tooan karşıya [Azure Storage] [ azure_storage] hesabı.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-127">Use a **job release task** in such cases toocompress and upload this data tooan [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="5a9b8-128">Başka bir şekilde toopersist günlükleri ve diğer iş ve Görev çıkış veri toouse hello [Azure toplu işlem dosyası kuralları](batch-task-output.md) kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-128">Another way toopersist logs and other job and task output data is toouse hello [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="5a9b8-129">İş hazırlama görevi</span><span class="sxs-lookup"><span data-stu-id="5a9b8-129">Job preparation task</span></span>
<span data-ttu-id="5a9b8-130">Bir iş görevlerinin çalışmaya başlamadan önce Batch zamanlanmış toorun bir görev olan her işlem düğümünde hello iş hazırlama görevi yürütür.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-130">Before execution of a job's tasks, Batch executes hello job preparation task on each compute node that is scheduled toorun a task.</span></span> <span data-ttu-id="5a9b8-131">Varsayılan olarak, Batch hizmeti hello hello iş hazırlama görevi toobe hello görevleri zamanlanmış tooexecute hello düğümde çalıştırılmadan önce tamamlanmasına bekler.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-131">By default, hello Batch service waits for hello job preparation task toobe completed before running hello tasks scheduled tooexecute on hello node.</span></span> <span data-ttu-id="5a9b8-132">Ancak, hello hizmetini değil toowait yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-132">However, you can configure hello service not toowait.</span></span> <span data-ttu-id="5a9b8-133">Merhaba düğümü yeniden başlatılırsa, hello iş hazırlama görevi yeniden çalışır, ancak aynı zamanda bu davranışı devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-133">If hello node restarts, hello job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="5a9b8-134">Merhaba iş hazırlama görevi, zamanlanmış bir görev toorun olan düğüm üzerinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-134">hello job preparation task is executed only on nodes that are scheduled toorun a task.</span></span> <span data-ttu-id="5a9b8-135">Bir düğüm görev atanmamış durumunda bu hello gereksiz hazırlık görevi yürütülmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-135">This prevents hello unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="5a9b8-136">Merhaba sayısı bir iş için görevleri bir havuzdaki düğümlerin hello sayısından daha az olduğunda bu durum oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-136">This can occur when hello number of tasks for a job is less than hello number of nodes in a pool.</span></span> <span data-ttu-id="5a9b8-137">Ne zaman da uygulanır [eşzamanlı görev yürütme](batch-parallel-node-tasks.md) etkin, hangi bırakır bazı düğümler boşta hello görev sayısı hello toplam olası eş zamanlı görevleri düşükse.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if hello task count is lower than hello total possible concurrent tasks.</span></span> <span data-ttu-id="5a9b8-138">Merhaba iş hazırlama görevi boşta düğümlerinde çalıştırarak değil, veri aktarımı ücretlerine üzerinde daha az para harcamanız.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-138">By not running hello job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="5a9b8-139">[JobPreparationTask] [ net_job_prep_cloudjob] farklıdır [CloudPool.StartTask] [ pool_starttask] JobPreparationTask ancak her bir iş hello başlangıcında yürütür, StartTask yalnızca zaman bir işlem düğümünde önce bir havuz birleştirir yürütür veya yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at hello start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="5a9b8-140">İş bırakma görevi</span><span class="sxs-lookup"><span data-stu-id="5a9b8-140">Job release task</span></span>
<span data-ttu-id="5a9b8-141">Bir işi tamamlandı olarak işaretlendikten sonra hello iş bırakma görevi hello havuzun en az bir görev yürütmüş her düğümünde çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-141">Once a job is marked as completed, hello job release task is executed on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="5a9b8-142">Bir iş, bir sonlandırma isteği vererek tamamlanan olarak işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="5a9b8-143">Batch hizmeti iş durumu çok kümeleri hello sonra hello*sonlandırma*hello işle ilişkili etkin ya da çalışan görevleri sonlandırır ve hello iş bırakma görevini çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-143">hello Batch service then sets hello job state too*terminating*, terminates any active or running tasks associated with hello job, and runs hello job release task.</span></span> <span data-ttu-id="5a9b8-144">Merhaba iş ardından taşır toohello *tamamlandı* durumu.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-144">hello job then moves toohello *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="5a9b8-145">İş silme de hello iş bırakma görevi yürütür.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-145">Job deletion also executes hello job release task.</span></span> <span data-ttu-id="5a9b8-146">Bir iş zaten sona erdi, hello işi daha sonra silinirse ancak hello bırakma görevi ikinci kez çalıştırılmaz.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-146">However, if a job has already been terminated, hello release task is not run a second time if hello job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="5a9b8-147">Hazırlığı işi ve görevleri Batch .NET ile bırakın</span><span class="sxs-lookup"><span data-stu-id="5a9b8-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="5a9b8-148">toouse iş hazırlama görevi, Ata bir [JobPreparationTask] [ net_job_prep] nesne tooyour işin [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] özelliği .</span><span class="sxs-lookup"><span data-stu-id="5a9b8-148">toouse a job preparation task, assign a [JobPreparationTask][net_job_prep] object tooyour job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="5a9b8-149">Benzer şekilde, başlatma bir [JobReleaseTask] [ net_job_release] ve tooyour işin atayın [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] özelliği tooset hello İş bırakma görevi.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it tooyour job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property tooset hello job's release task.</span></span>

<span data-ttu-id="5a9b8-150">Bu kod parçacığında bulunan `myBatchClient` örneği [BatchClient][net_batch_client], ve `myPool` hello toplu işlem hesabı içinde varolan bir havuzu.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within hello Batch account.</span></span>

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="5a9b8-151">Bir işi sona erdi veya silindiğinde daha önce belirtildiği gibi hello bırakma görevi yürütülür.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-151">As mentioned earlier, hello release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="5a9b8-152">Bir işin sonlandırmak [JobOperations.TerminateJobAsync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="5a9b8-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="5a9b8-153">Bir işin silme [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="5a9b8-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="5a9b8-154">Genellikle sonlandırma veya bir iş görevlerinin tamamlandığında veya tanımladığınız bir zaman aşımı erişildiğinde silin.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="5a9b8-155">Github'daki kod örneği</span><span class="sxs-lookup"><span data-stu-id="5a9b8-155">Code sample on GitHub</span></span>
<span data-ttu-id="5a9b8-156">Eylem toosee iş hazırlama ve bırakma görevleri denetleyin hello [JobPrepRelease] [ job_prep_release_sample] örnek proje github'da.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-156">toosee job preparation and release tasks in action, check out hello [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="5a9b8-157">Bu konsol uygulamasını aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="5a9b8-157">This console application does hello following:</span></span>

1. <span data-ttu-id="5a9b8-158">Bir havuz ile iki "küçük" düğümü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="5a9b8-159">Bir işi, iş hazırlama, sürüm ve standart görevler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="5a9b8-160">Önce bir düğümün "paylaşılan" dizininde hello düğüm kimliği tooa metin dosyasına yazar iş hazırlama görevi çalıştırır hello.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-160">Runs hello job preparation task, which first writes hello node ID tooa text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="5a9b8-161">Kendi görev kimliği toohello yazan her düğüme bir görevin çalıştığı aynı metin dosyası.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-161">Runs a task on each node that writes its task ID toohello same text file.</span></span>
5. <span data-ttu-id="5a9b8-162">Tüm görevler tamamlandığında (veya hello zaman aşımı ulaşıldıktan sonra), her düğümün metin dosyası toohello konsol Merhaba içeriğine yazdırır.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-162">Once all tasks are completed (or hello timeout is reached), prints hello contents of each node's text file toohello console.</span></span>
6. <span data-ttu-id="5a9b8-163">Merhaba iş tamamlandığında hello iş yayın görev toodelete hello dosya hello düğümden çalışır.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-163">When hello job is completed, runs hello job release task toodelete hello file from hello node.</span></span>
7. <span data-ttu-id="5a9b8-164">Baskı siparişi hello çıkış kodları, hello iş hazırlama ve görevler üzerinde yürütülen her düğüm için bırakın.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-164">Prints hello exit codes of hello job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="5a9b8-165">Duraklatır yürütme tooallow onayı işinin ve/veya havuzu silme.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-165">Pauses execution tooallow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="5a9b8-166">Merhaba örnek uygulamasının çıktısının benzer toohello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5a9b8-166">Output from hello sample application is similar toohello following:</span></span>

```
Attempting toocreate pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> <span data-ttu-id="5a9b8-167">Toohello değişken oluşturma ve başlangıç saatini (bazı düğümler diğerlerinden önce görevler için hazır) yeni bir havuzdaki düğümlerin, farklı çıkış görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-167">Due toohello variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="5a9b8-168">Özellikle, hızlı bir şekilde Hello görevleri tamamlamak için hello havuzdaki düğümlerin birinde tüm hello işin görevleri yürütür.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-168">Specifically, because hello tasks complete quickly, one of hello pool's nodes may execute all of hello job's tasks.</span></span> <span data-ttu-id="5a9b8-169">Bu meydana gelirse, iş hazırlığı ve yayın görevleri bu hello fark edeceksiniz hiçbir görev yürütülen hello düğüm yok.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-169">If this occurs, you will notice that hello job prep and release tasks do not exist for hello node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a><span data-ttu-id="5a9b8-170">İş hazırlama ve bırakma görevleri hello Azure portalı içinde inceleyin.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-170">Inspect job preparation and release tasks in hello Azure portal</span></span>
<span data-ttu-id="5a9b8-171">Merhaba örnek uygulamayı çalıştırdığınızda, hello kullanabilirsiniz [Azure portal] [ portal] tooview hello özelliklerini hello işi ve görevleri veya hatta hello işin görevleri tarafından değiştirilmiş hello paylaşılan metin dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-171">When you run hello sample application, you can use hello [Azure portal][portal] tooview hello properties of hello job and its tasks, or even download hello shared text file that is modified by hello job's tasks.</span></span>

<span data-ttu-id="5a9b8-172">Merhaba ekran görüntüsü aşağıda gösterilmiştir hello **hazırlama görevleri dikey** hello Merhaba örnek uygulaması yürütülmesi sonra Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-172">hello screenshot below shows hello **Preparation tasks blade** in hello Azure portal after a run of hello sample application.</span></span> <span data-ttu-id="5a9b8-173">Toohello gidin *JobPrepReleaseSampleJob* özellikleri görevleri tamamladıktan sonra (ancak işi ve havuzu silmeden önce) tıklatıp **hazırlama görevleri** veya **yayın görevleri** tooview özellikleri.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-173">Navigate toohello *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** tooview their properties.</span></span>

![İş hazırlama özelliklerini Azure portalında][1]

## <a name="next-steps"></a><span data-ttu-id="5a9b8-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5a9b8-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="5a9b8-176">Uygulama paketleri</span><span class="sxs-lookup"><span data-stu-id="5a9b8-176">Application packages</span></span>
<span data-ttu-id="5a9b8-177">Toplama toohello iş hazırlama görevi içinde hello de kullanabilirsiniz [uygulama paketleri](batch-application-packages.md) toplu tooprepare özelliğini işlem düğümleri için görev yürütme.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-177">In addition toohello job preparation task, you can also use hello [application packages](batch-application-packages.md) feature of Batch tooprepare compute nodes for task execution.</span></span> <span data-ttu-id="5a9b8-178">Bu özellik bir yükleyici, çok sayıda (100 +) dosyalar içeren uygulamalar veya katı sürüm denetimi gerektiren uygulamalar çalıştıran gerektirmeyen uygulamalarını dağıtmak için özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="5a9b8-179">Uygulama yükleme ve verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="5a9b8-179">Installing applications and staging data</span></span>
<span data-ttu-id="5a9b8-180">Bu MSDN Forumu gönderisi düğümleriniz hazırlama görevleri çalıştırmak için çeşitli yöntemler genel bir bakış sağlar:</span><span class="sxs-lookup"><span data-stu-id="5a9b8-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="5a9b8-181">[İşlem düğümlerine uygulamaların yüklenmesi ve toplu veri hazırlama][forum_post]</span><span class="sxs-lookup"><span data-stu-id="5a9b8-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="5a9b8-182">Hello Azure Batch ekip üyelerinin biri tarafından yazılmış, toodeploy uygulamaları ve verileri toocompute düğümleri kullanabileceğiniz çeşitli teknikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="5a9b8-182">Written by one of hello Azure Batch team members, it discusses several techniques that you can use toodeploy applications and data toocompute nodes.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png
