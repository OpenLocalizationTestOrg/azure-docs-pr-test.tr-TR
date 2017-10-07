---
title: "aaaPersist iş ve görev çıktısını tooAzure depolama hello dosyası kuralları kitaplığı için .NET - Azure Batch | Microsoft Docs"
description: ".NET toopersist toplu görev için toouse Azure toplu işlem dosyası kuralları kitaplığı ve proje çıktı tooAzure depolama ve görünüm hello hello Azure portal çıktısında nasıl kalıcı öğrenin."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a>İşi Sürdür ve .NET toopersist için hello toplu iş dosyası kuralları kitaplığı ile verileri tooAzure depolama görev 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Tek yönlü toopersist görev verilerdir toouse hello [.NET için Azure toplu işlem dosyası kuralları Kitaplığı][nuget_package]. Merhaba dosyası kuralları Kitaplığı görev çıktısını depolamak hello işlemini basitleştirir veri tooAzure depolama ve onu alınıyor. Merhaba dosyası kuralları Kitaplığı'nda görev ve istemci kodu kullanabilirsiniz &mdash; görev kodu kalıcı dosyaları için ve istemci kodu toolist ve bunları almak. Görev kodunuzu da hello kitaplığı tooretrieve hello çıkış Yukarı Akış görevlerin gibi kullanabilirsiniz bir [görev bağımlılıkları](batch-task-dependencies.md) senaryo. 

tooretrieve çıkış dosyaları hello dosyası kuralları kitaplığı ile belirli iş ya da görev için hello dosyaları amacı ve kimliği listeleyerek bulabilirsiniz. Tooknow hello adlar veya konumlar hello dosyaların gerekmez. Örneğin, belirli bir görev için tüm ara dosyaları hello dosyası kuralları kitaplığı toolist kullanın veya belirli bir iş için Önizleme dosya almak.

> [!TIP]
> Merhaba Batch hizmeti API'si 2017-05-01 sürümünden başlayarak, görevler ve hello sanal makine yapılandırması ile oluşturulan havuzu çalışan iş yöneticisi görevleri için kalıcı çıkış veri tooAzure depolama destekler. Merhaba Batch hizmeti API'si bir görev oluşturur ve bir alternatif toohello dosyası kuralları kitaplık olarak hizmet veren hello kodu ve çıkış basit yol toopersist sağlar. Görevinizi çalıştıran tooupdate Merhaba uygulaması gerek kalmadan, Batch istemci uygulamaları toopersist çıkış değiştirebilirsiniz. Daha fazla bilgi için bkz: [hello Batch hizmeti API'si ile görev veri tooAzure depolama kalıcı](batch-task-output-files.md).
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a>Merhaba dosyası kuralları kitaplığı toopersist görev çıktısını kullandığınızda?

Azure Batch birden fazla tek yönlü toopersist görev çıktısını sağlar. Merhaba dosyası kuralları en iyi uygun toothese senaryolar verilmiştir:

- Merhaba kod göreviniz hello dosyası kuralları kitaplığı kullanarak toopersist dosyaları çalıştığını Merhaba uygulaması için kolayca değiştirebilirsiniz.
- Merhaba görev çalışmaya devam ederken toostream veri tooAzure depolama istiyor.
- Merhaba bulut hizmet yapılandırması veya hello sanal makine yapılandırması ile oluşturulan havuzlarından toopersist veri istiyor.
- İstemci uygulamanız veya diğer görevler hello gereksinimlerini toolocate iş ve Görev çıkış dosyalarını Kimliğine göre veya amacına göre yükleyin. 
- Hello Azure portal tooview Görev çıkış istiyor.

Senaryonuz Yukarıda listelenenler farklıysa, farklı bir yaklaşım tooconsider gerekebilir. Kalıcı görev çıktısı için diğer seçenekleri hakkında daha fazla bilgi için bkz: [kalan iş ve görev çıktısını tooAzure depolama](batch-task-output.md). 

## <a name="what-is-hello-batch-file-conventions-standard"></a>Merhaba toplu iş dosyası kuralları standart nedir?

Merhaba [toplu iş dosyası kuralları standart](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) hello hedef kapsayıcılarını ve çıktı dosyalarınızı yazılır blob yolları toowhich bir adlandırma şeması sağlar. Dosyaları kalıcı tooAzure toohello standart dosya kurallarına uyması depolama hello Azure portalında görüntülenmek için otomatik olarak kullanılabilir. Hello portal hello adlandırma kuralı farkındadır ve bu nedenle tooit uyması dosyaları görüntüleyebilirsiniz.

Hello dosyası kuralları kitaplığı .NET için depolama kapsayıcıları ve Görev çıkış dosyalarını toohello standart dosya kurallarına göre otomatik olarak adlandırır. Merhaba dosyası kuralları kitaplığı toojob kimliği, görev kimliği veya amaca göre yöntemleri tooquery çıktı dosyalarını Azure storage'da de sağlar.   

.NET dışında bir dil ile geliştiriyorsanız, uygulamanızda kendiniz hello dosyası kuralları standart uygulayabilirsiniz. Daha fazla bilgi için bkz: [hello toplu iş dosyası kuralları standardı hakkında](batch-task-output.md#about-the-batch-file-conventions-standard).

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a>Bir Azure depolama hesabı tooyour toplu işlem hesabı Bağla

toopersist çıkış veri tooAzure Hello dosyası kuralları kitaplığı kullanarak depolama, ilk Azure Storage hesabı tooyour toplu işlem hesabı bağlamanız gerekir. Henüz yapmadıysanız, bir depolama hesabı tooyour toplu işlem hesabı hello kullanarak bağlantı [Azure portal](https://portal.azure.com):

1. Tooyour Batch hesabında hello Azure portalına gidin. 
2. Altında **ayarları**seçin **depolama hesabı**.
3. Batch hesabınızla ilişkili bir depolama hesabı zaten yoksa tıklatın **depolama hesabı (hiçbiri)**.
4. Aboneliğiniz için hello listesinden bir depolama hesabı seçin. En iyi performans için hello olan bir Azure depolama hesabı kullanmak aynı bölgede hello toplu işlem hesabı görevlerinizi çalıştırdığı.

## <a name="persist-output-data"></a>Çıktı verilerini Sürdür

toopersist iş ve görev çıktı verilerini hello dosyası kuralları kitaplığıyla, Azure Storage'da kapsayıcı oluşturma ve sonra hello çıktı toohello kapsayıcısını kaydedin. Kullanım hello [.NET için Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage) , görev kodu tooupload hello Görev çıkış toohello kapsayıcısında. 

Kapsayıcılar ve bloblar Azure depolama ile çalışma hakkında daha fazla bilgi için bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

> [!WARNING]
> Merhaba dosyası kitaplığı depolanır kuralları olan tüm iş ve görev çıktıları kalıcı hello aynı kapsayıcı. Çok sayıda görevleri çalışırsanız toopersist hello aynı dosyaları zaman [azaltma sınırları depolama](../storage/common/storage-performance-checklist.md#blobs) zorlanabilir.
> 
> 

### <a name="create-storage-container"></a>Depolama kapsayıcısı oluşturma

toopersist Görev çıkış tooAzure depolama, öncelikle çağırarak bir kapsayıcı oluşturmanız [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync]. Bu uzantı metodu geçen bir [CloudStorageAccount] [ net_cloudstorageaccount] nesnesini parametre olarak. Azure portal ve hello alma yöntemleri ilgili hello makalenin sonraki bölümlerinde ele alınan adlandırılmış according toohello dosyası kuralları içeriğinin tarafından keşfedilebilir; böylece standart hello bir kapsayıcı oluşturur.

İstemci uygulamanızı genellikle hello kod toocreate bir kapsayıcı yerleştirin &mdash; hello havuzlar, işler ve görevler oluşturan uygulamasıdır.

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a>Depolama görev çıkarır

Azure storage'da kapsayıcı hazırladığınıza göre görevleri çıktı toohello kapsayıcı hello kullanarak kaydedebilirsiniz [TaskOutputStorage] [ net_taskoutputstorage] sınıfı hello dosyası kuralları Kitaplığı'nda bulundu.

Görev kodunuzda ilk oluşturun bir [TaskOutputStorage] [ net_taskoutputstorage] nesne sonra hello görev kendi iş tamamlandığında, hello çağırın [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] yöntemi toosave kendi çıktı tooAzure depolama.

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

Merhaba `kind` hello parametresinin [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) yöntemi kategorilere ayıran hello dosyaları kalıcı. Dört önceden tanımlanmış vardır [TaskOutputKind] [ net_taskoutputkind] türleri: `TaskOutput`, `TaskPreview`, `TaskLog`, ve `TaskIntermediate.` çıktı özel kategoriler de tanımlayabilirsiniz.

Bu çıktı türü belirli bir görevi çıkışları ne tür bir toplu iş daha sonra Merhaba sorguladığınızda çıkışları toolist kalıcı toospecify izin verir. Diğer bir deyişle, bir görev hello çıktıların listelediğinizde hello çıkış türlerinden birini hello listede filtreleyebilirsiniz. Örneğin, "Merhaba ver *Önizleme* için görev çıktısını *109*." Listeleme ve çıkışları alma hakkında daha fazla görünür [almak çıktı](#retrieve-output) hello makalede daha sonra.

> [!TIP]
> Merhaba çıktı türü de hello Azure portal belirli bir dosya nerede görüneceğini belirler: *TaskOutput*-kategorilere ayrılmış dosyaları görünür altında **Görev çıkış dosyaları**, ve *TaskLog*dosyaları görünür altında **görev günlükleri**.
> 
> 

### <a name="store-job-outputs"></a>Mağaza iş çıkarır

Ayrıca toostoring görev çıktısını alır, tüm bir işle ilişkili hello çıkışları depolayabilirsiniz. Örneğin, hello birleştirme görevde bir filmi işleme işin, tam olarak işlenen hello film iş çıktısı kalıcı olamadı. İş tamamlandığında, istemci uygulamanız listelemek ve hello iş hello çıktıların almak ve tooquery tek tek görevler hello mu değil.

İş çıktısı tarafından arama hello depolamak [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] yöntemi ve hello belirtin [JobOutputKind] [ net_joboutputkind] ve dosya adı:

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

Merhaba olduğu gibi **TaskOutputKind** türü görev çıktıları için kullandığınız hello [JobOutputKind] [ net_joboutputkind] türü toocategorize bir iş dosyaları kalıcı. Bu parametre (listesi) belirli bir çıkış türü için toolater sorgu sağlar. Merhaba **JobOutputKind** türü çıkış ve önizleme kategorileri içerir ve özel kategoriler oluşturulmasını destekler.

### <a name="store-task-logs"></a>Depolama görev günlükleri

Ayrıca toopersisting dosya toodurable depolama bir görev veya iş tamamlandığında, bir görev hello yürütülmesi sırasında güncelleştirilir toopersist dosyalarına ihtiyaç duymayabilirsiniz &mdash; günlük dosyalarını veya `stdout.txt` ve `stderr.txt`, örneğin. Bu amaçla hello Azure toplu işlem dosyası kuralları kitaplığı hello sağlar [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] yöntemi. İle [SaveTrackedAsync][net_savetrackedasync], güncelleştirmeler tooa dosyasına (belirttiğiniz bir aralıkta) hello düğümde izlemek ve bu güncelleştirmeleri tooAzure depolama kalır.

Aşağıdaki kod parçacığını hello kullanırız [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` hello görev hello yürütülmesi sırasında 15 dakikada Azure storage'da:

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

Merhaba açıklamalı bölüm `Code tooprocess data and produce output file(s)` göreviniz normalde gerçekleştireceği hello kodu için bir yer tutucudur. Örneğin, veriler Azure depolama biriminden yükler ve dönüşüm ya da hesaplama üzerinde gerçekleştiren kodu olabilir. Merhaba önemli bu parçacığı parçası gösteren böyle kodda nasıl kayabilir bir `using` blok tooperiodically güncelleştirme dosyası ile [SaveTrackedAsync][net_savetrackedasync].

Merhaba düğümü aracı hello havuzdaki her düğüme çalışır ve hello düğümü hello Batch hizmeti arasında hello komut ve denetim arabirimi sağlayan bir programdır. Merhaba `Task.Delay` çağrıdır hello sonunda bu gerekli `using` düğümü aracı hello blok tooensure toohello stdout.txt dosya hello düğümde standart zaman tooflush Merhaba içeriğine sahip. Bu gecikme olmadan bu olası toomiss hello son birkaç saniye çıktısını gösterir. Bu gecikme tüm dosyaları için gerekli olmayabilir.

> [!NOTE]
> Dosya ile izleme etkinleştirdiğinizde **SaveTrackedAsync**, yalnızca *ekler* toohello izlenen dosya kalıcı tooAzure depolama şunlardır. Yalnızca günlük dosyaları döndürme izlemek için bu yöntemi kullanın veya toowith yazılır diğer dosyalar işlem toohello hello dosya sonuna.
> 
> 

## <a name="retrieve-output-data"></a>Çıktı verilerini alma

Hello Azure toplu işlem dosyası kuralları kitaplığı kullanarak, kalıcı çıktı aldığınızda, görev ve iş merkezli bir şekilde bunu. Hello için görev veya iş tooknow gerek kalmadan, Azure Storage veya bile dosya adıyla çıkış yolu isteyebilir. Bunun yerine, görev tarafından çıktı dosyaları istek veya iş kimliği

Hello aşağıdaki kod parçacığını işe ait görevleri tekrarlanan, hello görev için hello çıktı dosyaları hakkında bazı bilgiler yazdırır ve sonra depolama biriminden dosyalarını indirir.

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a>Hello Azure portal görünümü çıktı dosyaları

Hello Azure portal görüntüler görev çıktı dosyalarını ve kalıcı tooa olan günlükleri bağlı hello kullanarak Azure Storage hesabını [toplu iş dosyası kuralları standart](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). Bu kuralları hello tercih ettiğiniz bir dil kendiniz uygulayabilirsiniz veya .NET uygulamalarınızın hello dosyası kuralları kitaplığını kullanabilirsiniz.

tooenable hello görüntü çıkış dosyalarınızın hello Portalı'nda hello aşağıdaki gereksinimleri karşılaması gerekir:

1. [Bir Azure depolama hesabı bağlantı](#requirement-linked-storage-account) tooyour toplu işlem hesabı.
2. Önceden tanımlanmış toohello depolama kapsayıcıları ve dosyaları için adlandırma kuralları çıkışları kalıcı olduğunda uyar. Bu kuralları hello tanımını hello dosyası kuralları Kitaplığı'nda bulabilirsiniz [Benioku][github_file_conventions_readme]. Merhaba kullanırsanız [Azure toplu işlem dosyası kuralları] [ nuget_package] kitaplığı toopersist, output, dosyalarınızı toohello dosyası kuralları standart göre kalıcı.

tooview görev çıktısını dosyaları ve hello Azure portalında, toohello görev çıktısı ilgilendiğiniz, ardından da gidin **kayıtlı çıktı dosyaları** veya **Günlükleri kaydedilen**. Bu görüntü hello gösterir **kayıtlı çıktı dosyaları** "007" kimlikli hello görev için:

![Görev dikey penceresinde hello Azure portal çıkarır][2]

## <a name="code-sample"></a>Kod örneği

Merhaba [PersistOutputs] [ github_persistoutputs] örnek proje hello biridir [Azure Batch kod örnekleri] [ github_samples] github'da. Bu Visual Studio çözümü nasıl toodurable depolama toouse hello Azure toplu işlem dosyası kuralları kitaplığı toopersist görev çıktısını gösterir. toorun hello örnek, şu adımları izleyin:

1. Açık hello projesinde **Visual Studio 2015 veya daha yeni**.
2. Batch ve Storage eklemek **hesabının kimlik bilgilerini** çok**AccountSettings.settings** hello öğesini kullanıma alın projesinde.
3. **Yapı** (ancak çalışmaz) hello çözümü. İstenirse herhangi bir NuGet paketinin geri yükleyin.
4. Kullanım hello Azure portal tooupload bir [uygulama paketi](batch-application-packages.md) için **PersistOutputsTask**. Merhaba dahil `PersistOutputsTask.exe` ve bağımlı derlemeleri hello .zip paketindeki kümesi hello uygulama kimliği çok "PersistOutputsTask" ve hello uygulama Paket sürümü "1.0" çok.
5. **Başlat** (Çalıştır) hello **PersistOutputs** projesi.
6. İstendiğinde toochoose hello Kalıcılık teknolojisi toouse çalışan hello örnek girdiğinizde **1** hello dosyası kuralları kitaplığı toopersist görev çıktısını kullanarak toorun hello örnek. 

## <a name="next-steps"></a>Sonraki adımlar

### <a name="get-hello-batch-file-conventions-library-for-net"></a>Merhaba toplu iş dosyası kuralları kitaplığı için .NET Al

.NET için Hello toplu iş dosyası kuralları kitaplığı edinilebilir [NuGet][nuget_package]. Merhaba kitaplığı genişletir hello [CloudJob] [ net_cloudjob] ve [CloudTask] [ net_cloudtask] yeni yöntemleri sınıflarıyla. Ayrıca bkz. hello [başvuru belgelerini](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) hello dosyası kuralları kitaplığı.

Merhaba [kaynak kodu] [ github_file_conventions] Merhaba dosyası kuralları kitaplığı Github'da hello Microsoft Azure SDK'sı .NET havuz için kullanılabilir. 

### <a name="explore-other-approaches-for-persisting-output-data"></a>Diğer yaklaşımlar kalıcı çıkış verileri keşfedin

- Bkz: [kalan iş ve görev çıktısını tooAzure depolama](batch-task-output.md) kalıcı görevi ve iş verileri genel bakış.
- Bkz: [hello Batch hizmeti API'si ile görev veri tooAzure depolama kalıcı](batch-task-output-files.md) toolearn nasıl toouse hello Batch hizmeti API'si toopersist çıktı verilerini.

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "Kayıtlı çıktı dosyaları ve Portalı'nda kayıtlı günlükleri seçiciler"
[2]: ./media/batch-task-output/task-output-02.png "Görev dikey penceresinde hello Azure portal çıkarır"
