---
title: "aaaPersist iş ve görev çıktısını tooAzure depolama hello Azure Batch hizmeti API'si ile | Microsoft Docs"
description: "Nasıl tooAzure depolama toouse Batch hizmeti API'si toopersist toplu görevi ve iş çıktısını öğrenin."
services: batch
author: tamram
manager: timlt
editor: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.openlocfilehash: 71b3f7c0dda2d2a9d8eb3eef83229873c70ca22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-task-data-tooazure-storage-with-hello-batch-service-api"></a>Görev veri tooAzure depolama hello Batch hizmeti API'si Sürdür

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Merhaba Batch hizmeti API'si 2017-05-01 sürümünden başlayarak, görevler ve havuzları hello sanal makine yapılandırması ile çalışan iş yöneticisi görevleri için kalıcı çıkış veri tooAzure depolama destekler. Bir görev eklediğinizde, hello görevin çıkış hello hedefi olarak Azure Storage'da kapsayıcı belirtebilirsiniz. Batch hizmeti hello sonra hello görev tamamlandığında, herhangi bir çıktı veri toothat kapsayıcısına yazar.

Bir avantajı toousing hello Batch hizmeti API toopersist görev çıktısını görev hello toomodify Merhaba uygulaması gerekiyor mu olduğunu çalışıyor. Bunun yerine, birkaç basit değişiklikler tooyour istemci uygulaması ile Merhaba görevin çıktısı hello görev oluşturur hello kod devam edebilir.   

## <a name="when-do-i-use-hello-batch-service-api-toopersist-task-output"></a>Merhaba Batch hizmeti API'si toopersist görev çıktısını kullandığınızda?

Azure Batch birden fazla tek yönlü toopersist görev çıktısını sağlar. Merhaba Batch hizmeti API'si kullanılarak en iyi uygun toothese senaryolar kullanışlı bir yaklaşım şöyledir:

- İstemci uygulamanızı içinde görevin çalıştığı Merhaba uygulaması değiştirmeden toowrite kod toopersist görev çıktısını istiyorsunuz.
- Toplu iş görevleri ve iş yöneticisi görevleri hello sanal makine yapılandırması ile oluşturulan havuzlarında toopersist çıkışı istiyor.
- Toopersist çıkış tooan Azure depolama kapsayıcısının rasgele bir ada sahip istiyor.
- Toopersist çıkış tooan Azure depolama kapsayıcısının according toohello adlı istediğiniz [toplu iş dosyası kuralları standart](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

Senaryonuz Yukarıda listelenenler farklıysa, farklı bir yaklaşım tooconsider gerekebilir. Örneğin, Hello Görev yürütülürken hello Batch hizmeti API'si akış çıkışı tooAzure depolama şu anda desteklemiyor. toostream çıkışı, hello toplu iş dosyası kuralları kitaplığı, .NET için kullanılabilir kullanmayı düşünün. Diğer diller için kendi çözüm tooimplement gerekir. Kalıcı görev çıktısı için diğer seçenekleri hakkında daha fazla bilgi için bkz: [kalan iş ve görev çıktısını tooAzure depolama](batch-task-output.md). 

## <a name="create-a-container-in-azure-storage"></a>Azure Storage'da kapsayıcı oluşturma

tooAzure depolama toopersist görev çıktısı, toocreate çıkış dosyalarınızı hello hedefi olarak hizmet veren bir kapsayıcı gerekir. İşinizi göndermeden önce göreviniz, tercihen çalıştırmadan önce hello kapsayıcı oluşturun. toocreate hello kapsayıcı, kullanım hello uygun Azure Storage istemci kitaplığı veya SDK. Azure depolama API'leri hakkında daha fazla bilgi için bkz: Merhaba [Azure Storage belgeleri](https://docs.microsoft.com/azure/storage/).

Uygulamanızı C# dilinde yazıyorsanız, örneğin, hello kullan [.NET için Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/). örnekte gösterildiği nasıl aşağıdaki hello toocreate bir kapsayıcı:

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-hello-container"></a>Merhaba kapsayıcı için bir paylaşılan erişim imzası Al

Merhaba kapsayıcısı oluşturduktan sonra yazma erişimi toohello kapsayıcısı ile paylaşılan erişim imzası (SAS) alın. Bir SAS atanmış erişim toohello kapsayıcı sağlar. Merhaba SAS izinleri ve belirli bir zaman aralığı içinde belirtilen bir kümesiyle erişim verir. Merhaba Batch hizmeti bir SAS yazma izinleri toowrite Görev çıkış toohello kapsayıcısı ile gerekir. SAS hakkında daha fazla bilgi için bkz: [kullanarak paylaşılan erişim imzaları \(SAS\) Azure storage'da](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

Hello Azure depolama API'leri kullanılarak bir SAS aldığınızda, hello API bir SAS belirteci dize döndürür. Bu belirteç dizesini hello SAS hello izinleri ve hangi hello SAS geçerli hello aralıkta dahil olmak üzere, tüm parametrelerinin içerir. toouse hello SAS tooaccess Azure storage'da kapsayıcı, tooappend hello SAS belirteci dize toohello kaynak URI'si gerekir. Merhaba birlikte Hello kaynak URI'si, SAS belirteci eklenmiş, kimliği doğrulanmış erişim tooAzure depolama sağlar.

Merhaba aşağıdaki örnekte nasıl tooget salt yazılır SAS belirteci hello kapsayıcısı için dize gösterir, ardından hello SAS toohello kapsayıcı URI ekler:

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a>Görev çıktısı için çıktı dosyaları belirtin

bir görev için toospecify çıktı dosyaları bir koleksiyonunu oluşturmak [ÇıktıDosyası](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) nesneleri ve toohello atayın [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) hello görev oluşturduğunuzda özelliği. 

Merhaba aşağıdaki .NET kod örneğinde adlı rastgele sayılar tooa dosyası yazan bir görev oluşturur `output.txt`. Merhaba örnek bir çıktı dosyası oluşturur `output.txt` toobe toohello kapsayıcı yazılır. Merhaba örneği hello dosya desenle eşleşen tüm günlük dosyalarını için çıktı dosyaları da oluşturur `std*.txt` (_örneğin_, `stdout.txt` ve `stderr.txt`). Merhaba kapsayıcı URL'si hello oluşturulduğu SAS önceden hello kapsayıcısı gerektirir. Merhaba Batch hizmeti hello SAS tooauthenticate erişim toohello kapsayıcı kullanır: 

```csharp
new CloudTask(taskId, "cmd /v:ON /c \"echo off && set && (FOR /L %i IN (1,1,100000) DO (ECHO !RANDOM!)) > output.txt\"")
{
    OutputFiles = new List<OutputFile>
    {
        new OutputFile(
            filePattern: @"..\std*.txt",
            destination: new OutputFileDestination(
         new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId)),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
        new OutputFile(
            filePattern: @"output.txt",
            destination: 
         new OutputFileDestination(new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId + @"\output.txt")),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
}
```

### <a name="specify-a-file-pattern-for-matching"></a>Eşleşen bir dosya düzeni belirtme

Bir çıkış dosyası belirttiğinizde, hello kullanabilirsiniz [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) özelliği toospecify eşleşen bir dosya deseni. Merhaba dosya deseni sıfır dosyaları, tek bir dosya veya bir başlangıç görevi tarafından oluşturulan dosyaları kümesini eşleşmiyor olabilir.

Merhaba **FilePattern** özelliğini destekleyen standart dosya sistemi joker karakterler gibi `*` (özyinelemeli olmayan eşleşen için) ve `**` (özyinelemeli eşleşen için). Örneğin, hello Yukarıdaki örnek kod hello dosya düzeni toomatch belirtir `std*.txt` yinelemeli olmayan: 

`filePattern: @"..\std*.txt"`

tooupload tek bir dosya ile joker dosya düzeni belirtin. Örneğin, hello Yukarıdaki örnek kod hello dosya düzeni toomatch belirtir `output.txt`:

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a>Bir karşıya yükleme koşulu belirtin

Merhaba [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) özelliği verir koşullu çıktı dosyaları karşıya yükleme. Başarısız olursa yaygın bir senaryo tooupload bir hello görev başarılı olursa dosyaları kümesini ve farklı bir dosya kümesi ' dir. Örneğin, yalnızca hello görev başarısız olur ve sıfır olmayan çıkış kodu ile çıkar tooupload ayrıntılı günlük dosyalarını isteyebilirsiniz. Benzer şekilde, yalnızca hello görev başarılı olursa, bu dosyaları veya hello görev başarısız olursa eksik olabileceğinden tooupload sonuç dosyalarını isteyebilirsiniz.

Merhaba Yukarıdaki kod örneğini ayarlar hello **UploadCondition** özelliği çok**Net_offline_option**. Bu ayar, başlangıç görevleri tamamlandıktan sonra bağımsız olarak hello hello çıkış kodu değerini karşıya toobe o hello dosyadır belirtir. 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

Diğer ayarlar için bkz: hello [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) enum.

### <a name="disambiguate-files-with-hello-same-name"></a>Merhaba dosyalarıyla belirsizliğini ortadan kaldırmak aynı adı

bir İşte Hello görevleri hello sahip dosyalar oluşturabilir aynı adı. Örneğin, `stdout.txt` ve `stderr.txt` bir işlemde çalışan her görev için oluşturulur. Her görev kendi içeriğinde çalıştığından, bu dosyaları hello düğümün dosya sisteminde çakışmadığından. Ancak, birden çok görevleri tooa paylaşılan kapsayıcı dosyalarından karşıya yüklediğinizde, hello toodisambiguate dosyalarıyla gerekir aynı adı.

Merhaba [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) özelliği, hello hedef blob veya sanal dizinde çıktı dosyalarını belirtir. Merhaba kullanabilirsiniz **yolu** özelliği tooname hello blob veya sanal dizin çıktı ile aynı adı benzersiz olarak Azure Storage'da adlı hello dosyaları şekilde. Merhaba yolunda Hello görev kimliği'ni kullanarak bir en iyi yolu tooensure benzersiz adlar olduğu ve kolayca dosyaları tanımlayın.

Merhaba, **FilePattern** özelliğini tooa joker karakter ifadesini ayarlayın, sonra hello desenle eşleşen tüm dosyaları hello tarafından belirtilen karşıya yüklenen toohello sanal dizini olan **yolu** özelliği. Örneğin, hello kapsayıcı ise `mycontainer`, hello görev kimliği `mytask`, ve hello dosya deseni `..\std*.txt`, mutlak URI toohello çıktı dosyalarını Azure storage'da benzer olacaktır hello:

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

Merhaba, **FilePattern** özellik kümesi toomatch tek bir dosya adı, joker karakterler içermediğinden anlamına gelir, sonra hello değerini hello **yolu** özelliği hello tam blob adını belirtir . Adlandırma çakışmaları birden fazla görevden tek bir dosya ile öngörüyorsanız, hello hello sanal dizin adını hello dosya adı toodisambiguate bir parçası olarak bu dosyaları içerir. Örneğin, kümesi hello **yolu** özellik tooinclude hello görev kimliği, hello sınırlayıcı karakter (genellikle bir eğik çizgi) ve hello dosya adı:

`path: taskId + @"/output.txt"`

Merhaba mutlak URI toohello çıkış dosyaları için bir dizi görevi şuna benzeyecektir:

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

Azure depolama alanında sanal dizinleri hakkında daha fazla bilgi için bkz: [hello BLOB'ları bir kapsayıcıda listelemek](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).


## <a name="diagnose-file-upload-errors"></a>Dosya karşıya yükleme hatalarını tanılama

Çıktı karşıya yükleme dosyaları tooAzure depolama başarısız olduysa hello görev toohello taşır **tamamlandı** durumu ve hello [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) özelliği ayarlanmış. Merhaba inceleyin **FailureInformation** özelliği toodetermine hangi hata oluştu. Örneğin, dosya karşıya yükleme sırasında hello kapsayıcı bulunamazsa oluşan bir hata şöyledir: 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of hello specified Azure container(s) was not found while attempting tooupload an output file
```

İki günlük dosyaları toohello işlem düğümü, her dosya karşıya yükleme toplu Yazar `fileuploadout.txt` ve `fileuploaderr.txt`. Bu günlük dosyaları toolearn belirli hata hakkında daha fazla inceleyebilirsiniz. Merhaba görev kendisini çalıştırılamadı çünkü burada hello dosya karşıya yükleme hiçbir zaman, örneğin denendi durumlarda, sonra bu günlük dosyaları mevcut olmaz.

## <a name="diagnose-file-upload-performance"></a>Dosya karşıya yükleme performansı tanılama

Merhaba `fileuploadout.txt` dosya karşıya yükleme ilerleme durumu günlüğe kaydeder. Bu dosya toolearn ne kadar süreyle dosyanızı karşıya yükleme hakkında daha fazla sürüyor inceleyebilirsiniz. Tooupload performans, hello hedef kapsayıcı hello olup hello düğümün, diğer hello düğümünde etkinliği hello karşıya yükleme, başlangıç zamanında hello boyutu da dahil olmak üzere birçok faktörlere olduğunu aklınızda bulundurun hello Batch havuzu aynı bölgede, kaç tane düğümleri olan Depolama hesabı aynı saat ve benzeri hello toohello yükleniyor.

## <a name="use-hello-batch-service-api-with-hello-batch-file-conventions-standard"></a>Toplu iş dosyası kuralları standart hello ile Merhaba Batch hizmeti API'si kullanın

Görev çıktısı hello Batch hizmeti API'si ile kalıcı, hedef kapsayıcı adı verebilirsiniz ve istediğiniz ancak blobları. Tooname de seçebilirsiniz bunları toohello göre [toplu iş dosyası kuralları standart](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). Merhaba dosyası kuralları standart hello Hedef kapsayıcıyı ve Azure storage'da bir blob hello iş ve görev hello adlarına göre verilen çıktı dosyası hello adları belirler. Merhaba dosyası kuralları standart çıktı dosyalarını adlandırma için kullandığınız sonra çıktı dosyalarınızı hello görüntülenmek için kullanılabilir [Azure portal](https://portal.azure.com).

C# ' ta geliştiriyorsanız hello yerleşik hello yöntemlerini kullanabilirsiniz [.NET için toplu iş dosyası kuralları Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files). Bu kitaplık sizin için doğru kapsayıcıları ve blob yolları adlı hello oluşturur. Örneğin, hello API tooget hello için doğru bir adı hello iş adına göre hello kapsayıcı çağırabilirsiniz:

```csharp
string containerName = job.OutputStorageContainerName();
```

Merhaba kullanabilirsiniz [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) yöntemi tooreturn kullanılan toowrite toohello kapsayıcı paylaşılan erişim imzası (SAS) URL. Ardından bu SAS toohello geçirebilirsiniz [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) Oluşturucusu.

C# dışındaki bir dilde geliştiriyorsanız tooimplement hello dosyası kuralları standart kendiniz gerekir.

## <a name="code-sample"></a>Kod örneği

Merhaba [PersistOutputs] [ github_persistoutputs] örnek proje hello biridir [Azure Batch kod örnekleri] [ github_samples] github'da. Bu Visual Studio çözümü nasıl toodurable depolama toouse hello toplu istemci kitaplığı için .NET toopersist görev çıktısını gösterir. toorun hello örnek, şu adımları izleyin:

1. Açık hello projesinde **Visual Studio 2015 veya daha yeni**.
2. Batch ve Storage eklemek **hesabının kimlik bilgilerini** çok**AccountSettings.settings** hello öğesini kullanıma alın projesinde.
3. **Yapı** (ancak çalışmaz) hello çözümü. İstenirse herhangi bir NuGet paketinin geri yükleyin.
4. Kullanım hello Azure portal tooupload bir [uygulama paketi](batch-application-packages.md) için **PersistOutputsTask**. Merhaba dahil `PersistOutputsTask.exe` ve bağımlı derlemeleri hello .zip paketindeki kümesi hello uygulama kimliği çok "PersistOutputsTask" ve hello uygulama Paket sürümü "1.0" çok.
5. **Başlat** (Çalıştır) hello **PersistOutputs** projesi.
6. İstendiğinde toochoose hello Kalıcılık teknolojisi toouse çalışan hello örnek girdiğinizde **2** hello Batch hizmeti API'si toopersist görev çıktısını kullanarak toorun hello örnek.
7. İsterseniz, girme hello örnek yeniden çalıştırmak **3** toopersist çıktı hello Batch hizmeti API'si ve toohello standart dosya kurallarına göre tooname hello hedef kapsayıcı ve blob yolu.

## <a name="next-steps"></a>Sonraki adımlar

- .NET için kalıcı görev çıktısını hello dosyası kuralları Kitaplığı hakkında daha fazla bilgi için bkz: [iş ve görev veri tooAzure depolama hello toplu iş dosyası kuralları kitaplığı için .NET toopersist kalıcı ](batch-task-output-file-conventions.md).
- Azure Batch kalıcı çıktı verileri için diğer yaklaşımlar hakkında daha fazla bilgi için bkz: [kalan iş ve görev çıktısını tooAzure depolama](batch-task-output.md).

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
