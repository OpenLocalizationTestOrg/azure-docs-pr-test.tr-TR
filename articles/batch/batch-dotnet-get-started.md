---
title: "aaaTutorial - .NET için kullanım hello Azure Batch istemci kitaplığı | Microsoft Docs"
description: "Azure Batch temel kavramlarını Hello öğrenin ve .NET kullanarak basit bir çözüm oluşturun."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a>.NET için hello toplu istemci kitaplığı ile çözümler derleme kullanmaya başlama

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Merhaba temel bilgileri öğrenmek [Azure Batch] [ azure_batch] ve hello [Batch .NET] [ net_api] kitaplığı bu makalede bir C# örnek uygulama adımı tarafından aşağıdakiler ele gibi adım. Biz Merhaba örnek uygulaması hello Batch hizmeti tooprocess nasıl geliştirdiğini de paralel iş yükünü hello Bulut ve onu ile nasıl etkileşim kurduğu bakın [Azure Storage](../storage/common/storage-introduction.md) dosya hazırlığı ve alımı için. Ortak Batch uygulama iş akışı öğrenin ve hello başlıca Batch bileşenleri işler, görevler, havuzlar gibi temel bir anlayış edinmek ve işlem düğümleri.

![Batch çözümü iş akışı (temel)][11]<br/>

## <a name="prerequisites"></a>Ön koşullar
Bu makalede, C# ve Visual Studio deneyimine sahip olduğunuz varsayılmaktadır. Aşağıda Azure ve hello toplu işlem ve depolama hizmetleri için belirtilen mümkün toosatisfy hello hesap oluşturma gerekliliklerini olduğunuzu varsayar.

### <a name="accounts"></a>Hesaplar
* **Azure hesabı**: Henüz bir Azure aboneliğiniz yoksa, [ücretsiz Azure hesabı oluşturun][azure_free_account].
* **Batch hesabı**: Azure aboneliğiniz olduktan sonra, [Azure Batch hesabı oluşturun](batch-account-create-portal.md).
* **Storage hesabı**: Bkz. [Azure Storage hesapları hakkında](../storage/common/storage-create-storage-account.md) sayfası, [Storage hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) bölümü.

> [!IMPORTANT]
> Batch şu anda destekler *yalnızca* hello **genel amaçlı** #5. adımda açıklandığı gibi depolama hesabı türü, [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) içinde [Azure hakkında Depolama hesapları](../storage/common/storage-create-storage-account.md).
>
>

### <a name="visual-studio"></a>Visual Studio
Bilmeniz gereken **Visual Studio 2015 veya daha yeni** toobuild hello örnek proje. Visual Studio'nun Ücretsiz ve deneme sürümlerini hello bulabilirsiniz [Visual Studio ürün genel bakış][visual_studio].

### <a name="dotnettutorial-code-sample"></a>*DotNetTutorial* kodu örneği
Merhaba [DotNetTutorial] [ github_dotnettutorial] örnek birçok Batch kod örnekleri bulunan hello hello biridir [azure-batch-samples] [ github_samples] havuzda GitHub. Tüm hello örnekleri tıklayarak indirebileceğiniz **Kopyala veya indir > ZIP'i indir** hello depo giriş sayfasındaki veya hello tıklatarak [azure-batch-samples-master.zip] [ github_samples_zip]doğrudan indirme bağlantısına. Merhaba hello ZIP dosyasının içeriğini ayıkladıktan sonra klasör aşağıdaki hello hello çözüm bulabilirsiniz:

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a>Azure Batch Gezgini (isteğe bağlı)
Merhaba [Azure Batch Gezgini] [ github_batchexplorer] hello dahil ücretsiz bir yardımcı programdır [azure-batch-samples] [ github_samples] github'daki. Gerekli değil toocomplete sırasında Bu öğretici, geliştirirken ve Batch çözümlerinizi hatalarını ayıklarken yararlı olabilir.

## <a name="dotnettutorial-sample-project-overview"></a>DotNetTutorial örnek projesine genel bakış
Merhaba *DotNetTutorial* kod örneği buradaki iki projeden oluşan bir Visual Studio çözümü: **DotNetTutorial** ve **TaskApplication**.

* **DotNetTutorial** (sanal makineler) işlem düğümlerinde paralel iş yükünü hello toplu işlem ve depolama hizmetleri tooexecute ile etkileşim kuran hello istemci uygulamasıdır. DotNetTutorial yerel iş istasyonunuzda çalışır.
* **TaskApplication** Azure tooperform hello asıl işi işlem düğümlerinde çalışan hello programdır. Merhaba örnekteki `TaskApplication.exe` hello metni (girdi dosyası hello) Azure Storage'dan indirilen dosyada ayrıştırıyor. Bir metin dosyası oluşturur sonra (Merhaba çıktı dosyası) hello giriş dosyasında görünen hello ilk üç sözcük listesini içerir. Merhaba çıktı dosyasını oluşturduktan sonra TaskApplication hello dosya tooAzure depolama yükler. Bu yükleme için kullanılabilir toohello istemci uygulaması hale getirir. TaskApplication hello Batch hizmeti birden çok işlem düğümünde paralel olarak çalışır.

Merhaba Aşağıdaki diyagramda gösterilmektedir hello istemci uygulaması tarafından gerçekleştirilen birincil işlemleri hello *DotNetTutorial*ve hello görevler tarafından yürütülen hello uygulama *TaskApplication*. Bu temel iş akışı, Batch’le oluşturulan çok sayıda işlem çözümünün tipik halidir. Bu her özelliğe hello Batch hizmeti uygun olmadığı belirtilirken, neredeyse her Batch senaryosu iş akışının bölümlerini içerir.

![Batch örnek iş akışı][8]<br/>

[**1. Adım.**](#step-1-create-storage-containers) Azure Blob Storage’da **kapsayıcılar** oluşturun.<br/>
[**2. Adım.**](#step-2-upload-task-application-and-data-files) Karşıya yükleme görev uygulaması dosyalarını ve girdi dosyalarını toocontainers.<br/>
[**3. Adım.**](#step-3-create-batch-pool) Batch **havuzu** oluşturun.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Merhaba havuzu **StartTask** yüklemeleri hello görev ikili dosyalarını (TaskApplication) toonodes hello havuzuna Katıl gibi.<br/>
[**4. Adım.**](#step-4-create-batch-job) Batch **işi** oluşturun.<br/>
[**5. Adım**](#step-5-add-tasks-to-job) Ekleme **görevleri** toohello işi.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** Merhaba, düğümlerde zamanlanmış tooexecute görevlerdir.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Her görev kendi girdi verilerini Azure Storage’dan indirip yürütmeye başlar.<br/>
[**6. Adım**](#step-6-monitor-tasks) Görevleri izleyin.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Görevlerin tamamlanmasıyla, kendi çıktı veri tooAzure depolama karşıya yükleyin.<br/>
[**7. Adım**](#step-7-download-task-output) Storage’dan görev çıktısını indirin.

Belirtildiği gibi her Batch çözümü tam adımları gerçekleştirir ve çok daha fazlasını içerir, ancak hello *DotNetTutorial* örnek uygulaması Batch çözümde bulunan ortak işlemleri göstermektedir.

## <a name="build-hello-dotnettutorial-sample-project"></a>Merhaba yapı *DotNetTutorial* örnek proje
Merhaba örnek başarıyla çalıştırabilmeniz için önce Batch ve Storage hesabı kimlik bilgileri hello belirtmelisiniz *DotNetTutorial* projenin `Program.cs` dosya. Henüz yapmadıysanız, hello çözümü Visual Studio'da hello çift tıklatarak açın `DotNetTutorial.sln` çözüm dosyası. Veya ondan hello kullanarak Visual Studio'da açın **Dosya > Aç > Proje/çözüm** menüsü.

Açık `Program.cs` hello içinde *DotNetTutorial* projesi. Daha sonra kimlik bilgilerinizi belirtildiği gibi hello dosyasının hello üstüne yakın ekleyin:

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> Şu anda yukarıda belirtildiği gibi hello kimlik bilgilerini belirtmelisiniz bir **genel amaçlı** Azure depolama hesabında depolama. Toplu iş uygulamalarınız hello içinde blob storage kullanma **genel amaçlı** depolama hesabı. Merhaba seçerek oluşturulmuş bir depolama hesabı için Hello kimlik bilgilerini belirtmeyin *Blob storage* hesap türü.
>
>

Batch ve Storage hesabı kimlik bilgilerinizi her hizmetin hesap dikey hello hello bulabilirsiniz [Azure portal][azure_portal]:

![Merhaba portalda batch kimlik bilgileri][9]
![hello portalda Storage kimlik bilgileri][10]<br/>

Kimlik bilgilerinizle hello proje güncelleştirildi, Çözüm Gezgini'ndeki hello çözüme sağ tıklatın ve **yapı çözümü**. İstenirse, herhangi bir NuGet paketinin geri yüklenmesi hello onaylayın.

> [!TIP]
> Merhaba NuGet paketleri otomatik olarak geri yüklenmez veya bir hata toorestore hello paketlerle ilgili hatalar görürseniz, hello sahip olduğundan emin olun [NuGet Paket Yöneticisi] [ nuget_packagemgr] yüklü. Sonra da eksik paketleri hello indirilmesini etkinleştirin. Bkz: [etkinleştirme paket geri yükleme sırasında yapı] [ nuget_restore] tooenable paket yükleme.
>
>

Merhaba, aşağıdaki bölümlerde, biz Merhaba örnek uygulaması tooprocess gerçekleştirir hello adımları hello Batch hizmeti iş yükünü bölme ve bu adımlar üzerine ayrıntılı tartıştık. Her hello örnek kod satırı ele alınan bu yana yolunuzu bu makalenin hello rest aracılığıyla çalışırken toorefer toohello açık çözümü Visual Studio'da öneririz.

Merhaba toohello üstündeki gidin `MainAsync` hello yönteminde *DotNetTutorial* projenin `Program.cs` toostart 1. adım ile dosya. Her adım aşağıda kabaca yöntemini aşağıdaki şekilde hello ilerleyişini çağrıları sonra `MainAsync`.

## <a name="step-1-create-storage-containers"></a>1. Adım: Storage kapsayıcıları oluşturma
![Azure Depolama'da kapsayıcı oluşturma][1]
<br/>

Azure Storage ilet etkileşimde bulunmak için Batch’te yerleşik destek bulunur. Storage hesabınızdaki kapsayıcılar, Batch hesabınızda çalışan hello görevler için gerekli hello dosyaları sağlar. Merhaba kapsayıcılara hello görevlerin oluşturduğu bir yerde toostore hello çıktı verilerini de sağlar. ilk şey hello hello *DotNetTutorial* istemci uygulamasının yapacağı üç kapsayıcı oluşturmaktır [Azure Blob Storage](../storage/common/storage-introduction.md):

* **Uygulama**: Bu kapsayıcı hello görevlerin yanı sıra DLL'ler gibi birçok bağlantının tarafından çalıştırılan hello uygulamayı da depolar.
* **Giriş**: görevler hello hello veri dosyaları tooprocess yükleyecek *giriş* kapsayıcı.
* **Çıktı**: görevler girdi dosyası işlemeyi tamamladıklarında hello sonuçları toohello karşıya yükleyecek *çıkış* kapsayıcı.

Sipariş toointeract bir depolama hesabı ve kapsayıcı, oluşturma hello kullanırız [.NET için Azure Storage istemci Kitaplığı][net_api_storage]. Bir başvuru toohello hesabıyla oluşturuyoruz [CloudStorageAccount][net_cloudstorageaccount]ve oluşturan bir [CloudBlobClient][net_cloudblobclient]:

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

Merhaba kullanırız `blobClient` başvuru hello uygulama genelinde ve tooseveral yöntemleri parametre olarak geçirin. Bu, burada diyoruz hello yukarıdaki hemen izleyen hello kod bloğunda örneğidir `CreateContainerIfNotExistAsync` tooactually Merhaba kapsayıcılara oluşturun.

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

Merhaba kapsayıcılara oluşturduktan sonra Merhaba uygulaması artık hello görevler tarafından kullanılacak hello dosyaları karşıya yükleyebilir.

> [!TIP]
> [Nasıl toouse Blob depolama alanından .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) Azure Storage kapsayıcıları ve blob'larla çalışma hakkında kapsamlı bilgi sağlar. Batch ile çalışmaya başladığınızda okuma listenizin hello yukarıya yakın olması gerekir.
>
>

## <a name="step-2-upload-task-application-and-data-files"></a>2. Adım: Görev uygulamasını ve veri dosyalarını karşıya yükleme
![Karşıya yükleme görev uygulamasını ve girdi (veri) toocontainers dosyaları][2]
<br/>

Merhaba dosyayı karşıya yükleme işlemi, *DotNetTutorial* ilk tanımlar **uygulama** ve **giriş** hello yerel makinede oldukları gibi dosya yolları. Sonra hello önceki adımda oluşturduğunuz bu dosyaları toohello kapsayıcıları yükler.

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

İçinde iki yöntem vardır `Program.cs` hello karşıya yükleme işlemini oluşturan:

* `UploadFilesToContainerAsync`: Bu yöntem koleksiyonu döndürür [ResourceFile] [ net_resourcefile] (aşağıda açıklanmıştır) nesneleri ve dahili olarak çağrıları `UploadFileToContainerAsync` dosya almak için diğer bir deyişle, her tooupload geçirilen hello *filePaths* parametresi.
* `UploadFileToContainerAsync`: Bu, aslında hello dosyayı karşıya yüklemeyi gerçekleştiren ve hello oluşturan hello yöntemdir [ResourceFile] [ net_resourcefile] nesneleri. Merhaba dosyayı karşıya yükledikten sonra bu hello dosya için paylaşılan erişim imzası (SAS) alır ve temsil ettiği bir ResourceFile nesnesini döndürür. Paylaşılan erişim imzaları aşağıda da açıklanmıştır.

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a>ResourceFiles
A [ResourceFile] [ net_resourcefile] hello URL tooa indirilen tooa Azure depolama alanı dosyasında toplu görevlerle işlem düğümü, görev çalıştırılmadan önce sağlar. Merhaba [ResourceFile.BlobSource] [ net_resourcefile_blobsource] özelliği, Azure Storage'da yer aldığından hello hello dosyanın tam URL'sini belirtir. Merhaba URL ayrıca güvenli erişim toohello dosya sağlayan bir paylaşılan erişim imzası (SAS) içerebilir. Batch .NET’teki çoğu görev türünde *ResourceFiles* özelliği vardır; bu özellikte şunlar bulunur:

* [CloudTask][net_task]
* [StartTask][net_pool_starttask]
* [JobPreparationTask][net_jobpreptask]
* [JobReleaseTask][net_jobreltask]

DotNetTutorial örnek uygulaması Hello hello JobPreparationTask veya JobReleaseTask görev türlerini kullanmaz, ancak daha fazla bilgiyi ilgili [iş hazırlama ve tamamlama görevlerini çalıştırma Azure Batch işlem düğümlerinde](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Paylaşılan erişim imzası (SAS)
Paylaşılan erişim imzalar dizelerdir — bir URL bir parçası olarak dahil olduğunda — güvenli erişim toocontainers ve Azure Storage blobları sağlar. Merhaba DotNetTutorial uygulaması hem blob kullanır ve kapsayıcı paylaşılan erişim imzası URL'lerini ve nasıl tooobtain bu paylaşılan erişim imzası dizeleri depolama hizmeti hello gösterir.

* **Blob paylaşılan erişim imzaları**: DotNetTutorial hello havuza ait StartTask, Storage'dan hello uygulama ikililerini ve girdi veri dosyalarını indirdiğinde blob paylaşılan erişim imzalarını kullanır (3. adım aşağıya bakın). Merhaba `UploadFileToContainerAsync` Dotnettutorial'in yönteminde `Program.cs` her blob'un paylaşılan erişim imzasını alan hello kodunu içerir. Bu işlemi [CloudBlob.GetSharedAccessSignature][net_sas_blob] çağırarak gerçekleştirir.
* **Kapsayıcı paylaşılan erişim imzaları**: her görev hello işlem düğümü işini bitirdiğinde, kendi çıktı dosyasını toohello yükler *çıkış* Azure storage'da kapsayıcı. toodo, TaskApplication hello dosyayı karşıya yüklediğinde hello yolu bir parçası olarak yazma erişimi toohello kapsayıcı sağlayan kapsayıcı paylaşılan erişim imzasını kullanır. Alma hello kapsayıcı paylaşılan erişim imzası zaman erişim imzası alma hello blob paylaşılan olarak benzer bir şekilde gerçekleştirilir. DotNetTutorial ' Bu hello bulacaksınız `GetContainerSasUrl` yardımcı yöntem çağrılarını [CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo şekilde. Okuyacaksınız TaskApplication hello kapsayıcı nasıl kullandığı hakkında daha fazla paylaşılan erişim imzasını "6. adım: izleme görevleri."

> [!TIP]
> Hello iki parçalı seriyi kullanıma paylaşılan erişim imzalarındaki [Kısım 1: paylaşılan erişim imzası (SAS) modelini anlama hello](../storage/common/storage-dotnet-shared-access-signature-part-1.md) ve [2. parça: oluşturma ve paylaşılan erişim imzası (SAS) ileBlobstoragekullanma](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn depolama hesabınızdaki toodata güvenli erişim sağlama hakkında daha fazla.
>
>

## <a name="step-3-create-batch-pool"></a>3. Adım: Batch havuzu oluşturma
![Batch havuzu oluşturma][3]
<br/>

Batch **havuzu**, Batch’in işe ait görevleri yürüttüğü işlem düğümlerinin (sanal makineler) koleksiyonudur.

Merhaba uygulama ve veri dosyalarını toohello depolama hesabı Azure depolama API'leri ile karşıya yüklenmesini sonra *DotNetTutorial* hello Batch .NET kitaplığı tarafından sağlanan API'leri ile çağrıları toohello Batch hizmeti yapmadan başlar. Merhaba kod ilk oluşturur bir [BatchClient][net_batchclient]:

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

Ardından, hello örnek bir işlem düğümü havuzu oluşturacak çağrısıyla hello Batch hesabında çok oluşturur`CreatePoolIfNotExistsAsync`. `CreatePoolIfNotExistsAsync`kullandığı hello [BatchClient.PoolOperations.CreatePool] [ net_pool_create] yöntemi toocreate hello toplu işlem hizmeti yeni bir havuzda:

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

Bir havuzu oluştururken [CreatePool][net_pool_create], işlem düğümleri hello sayısı gibi çeşitli parametreleri hello belirttiğiniz [hello düğümlerin boyutu](../cloud-services/cloud-services-sizes-specs.md), ve düğümlerin işletim hello Sistem. İçinde *DotNetTutorial*, kullandığımız [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2'den [bulut Hizmetleri](../cloud-services/cloud-services-guestos-update-matrix.md). 

Azure sanal makineleri (VM'ler) işlem düğümleri havuzlarının hello belirterek oluşturabilirsiniz [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] havuzunuz için. VM işlem düğümü havuzlarını Windows veya [Linux görüntülerinden](batch-linux-nodes.md) oluşturabilirsiniz. VM görüntüleri için Hello kaynağı ya da olabilir:

- Merhaba [Azure Virtual Machines Marketi][vm_marketplace], kullanıma hazır hem Windows hem de Linux görüntüleri sağlar. 
- Hazırlayıp sağlayacağınız bir özel görüntü. Özel görüntüler hakkında daha fazla ayrıntı için bkz. [Batch ile büyük ölçekli paralel işlem çözümleri geliştirme](batch-api-basics.md#pool).

> [!IMPORTANT]
> Batch’teki işlem kaynakları ücretlidir. toominimize maliyetleri alt `targetDedicatedComputeNodes` hello örneği çalıştırmadan önce too1.
>
>

Bu fiziksel düğüm özellikleriyle birlikte, de belirtebilir bir [StartTask] [ net_pool_starttask] hello havuzu için. Bu düğüme hello havuzuna katılır ve her bir düğümü yeniden Hello StartTask her düğümde yürütür. Merhaba StartTask Itanium tabanlı sistemler için işlem düğümleri önceki toohello yürütme görevlerin üzerinde uygulamaları yüklemek için özellikle yararlıdır. Örneğin, görevleriniz verileri Python betiklerini kullanarak işlemek, StartTask tooinstall Python hello işlem düğümlerinde kullanabilirsiniz.

Bu örnek uygulamasında hello StartTask, Storage'dan indirilen hello dosyaları kopyalar (hangi belirtilen hello kullanarak [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] özelliği) dizininden hello StartTask çalışma dizini toohello paylaşılan, *tüm* hello düğümde çalışan görevler erişebilir. Esas olarak, bu kopyalar `TaskApplication.exe` ve onun bağımlılıklarını toohello paylaşılan her düğüme hello düğümü hello havuza katılmış olduğundan hello düğümü üzerinde çalışacak herhangi bir görevi erişebilmesi.

> [!TIP]
> Merhaba **uygulama paketleri** Azure batch özelliği, uygulamanızı bir havuzdaki işlem düğümleri hello üzerine başka bir şekilde tooget sağlar. Bkz: [Batch uygulama paketleriyle uygulama toocompute düğümlerini dağıtmak](batch-application-packages.md) Ayrıntılar için.
>
>

Ayrıca içinde yukarıdaki hello kod parçacığında dikkat çeken bir şey hello hello iki ortam değişkenleri kullanımıdır *CommandLine* hello StartTask özelliğinin: `%AZ_BATCH_TASK_WORKING_DIR%` ve `%AZ_BATCH_NODE_SHARED_DIR%`. Batch havuzundaki her işlem düğümü belirli tooBatch olan birkaç ortam değişkenlerini otomatik olarak yapılandırılır. Bir görev tarafından yürütülen herhangi bir işlem toothese ortam değişkenlerine erişim vardır.

> [!TIP]
> bir Batch havuzu ve görev çalışma dizinleri hakkında bilgilerin işlem düğümlerinde bulunan hello ortam değişkenleri hakkında daha fazla toofind bkz hello [görevler için ortam ayarları](batch-api-basics.md#environment-settings-for-tasks) ve [dosyalar ve dizinler ](batch-api-basics.md#files-and-directories) hello bölümlerde [geliştiriciler için Batch özelliklerine genel bakış](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>4. Adım: Batch işi oluşturma
![Batch işi oluşturma][4]<br/>

Batch **işi**, görevler koleksiyonudur ve işlem düğümlerinin bir havuzuyla ilişkilidir. Merhaba görevleri bir işlemle ilişkili hello havuzun işlem düğümleri üzerinde yürütün.

Bir işi yalnızca ilgili iş yüklerinde görevlerin düzenlenmesi ve, ancak aynı zamanda yanı sıra, ilişkisi tooother işlerini hello toplu olarak iş önceliği hello en fazla çalışma hello işin (ve uzantılarının, görevleri) gibi bazı kısıtlamalar etkileyici kullanabilirsiniz hesabı. Bu örnekte, ancak hello iş #3. adımda oluşturulan hello havuzu ile ilişkilidir. Yapılandırılmış başka ek özellik yoktur.

Tüm Batch işleri belirli bir havuzla ilişkilidir. Bu ilişkilendirme hello işin görevlerinin hangi düğümleri gösterir. Bu hello kullanarak belirttiğiniz [Cloudjob.poolınformation] [ net_job_poolinfo] hello aşağıdaki kod parçacığında gösterildiği gibi özelliği.

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

Bir işi oluşturuldu, görevler tooperform hello iş eklenir.

## <a name="step-5-add-tasks-toojob"></a>5. adım: görevleri toojob ekleme
![Görevleri toojob Ekle][5]<br/>
*(1) görevler toohello iş eklenir, düğümlerde zamanlanmış toorun (2) hello görevlerdir ve (3) hello görevleri hello veri dosyaları tooprocess indirme*

Toplu **görevleri** hello üzerinde yürütülen hello tek tek iş birimleri işlem düğümlerini şunlardır. Bir görev, bir komut satırı ve hello komut dosyaları veya bu komut satırında belirttiğiniz yürütülebilir dosyaları çalıştırır.

tooactually gerçekleştirmek iş, görevleri tooa iş eklenmesi gerekir. Her [CloudTask] [ net_task] bir komut satırı özelliği kullanılarak yapılandırılır ve [ResourceFiles] [ net_task_resourcefiles] (Merhaba havuza ait startTask gibi), komut satırı otomatik olarak yürütülmeden önce hello görev toohello düğümü indirir. Merhaba, *DotNetTutorial* örnek projesinde her görev yalnızca bir dosya işler. Bu nedenle, kendi ResourceFiles koleksiyonunda tek bir öğe bulunmaktadır.

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> Ortam değişkenlerine eriştiklerinde gibi `%AZ_BATCH_NODE_SHARED_DIR%` veya hello düğümün bulunmayan bir uygulama yürüttüklerinde `PATH`, görev komut satırları öneki, ile `cmd /c`. Bu açıkça hello komut yorumlayıcı yürütecek ve komutunuzu uyguladıktan sonra tooterminate isteyin. Bu gereksinim, görevlerinizin hello düğümün bir uygulama yürütüyorsa gereksizdir `PATH` (gibi *robocopy.exe* veya *powershell.exe*) ve hiç ortam değişkeni kullanılır.
>
>

Merhaba içinde `foreach` Yukarıdaki kod parçacığında hello döngüde, üç komut satırı bağımsız değişkenleri çok geçirilen şekilde hello komut satırı hello görev için oluşturulan görebilirsiniz*TaskApplication.exe*:

1. Merhaba **ilk bağımsız değişken** hello dosya tooprocess hello yoludur. Merhaba düğümde yer aldığından bu hello yerel yol toohello dosyasıdır. ResourceFile nesnesi'ne zaman hello `UploadFileToContainerAsync` ilk oluşturulduğunda yukarıdaki hello dosya adı bu özellik için (bir parametre toohello ResourceFile oluşturucuda) kullanılır. Bu, hello dosya bulunabilir hello aynı gösterir olarak dizin *TaskApplication.exe*.
2. Merhaba **ikinci bağımsız değişken** bu hello üst belirtir *N* sözcükler toohello çıktı dosyasına yazılması gerekir. Merhaba örnekte bu hello ilk üç sözcük toohello çıktı dosyasına yazılır böylece kodlanmış.
3. Merhaba **üçüncü bağımsız değişken** yazma erişimi toohello sağlayan hello paylaşılan erişim imzası (SAS) **çıkış** Azure storage'da kapsayıcı. *TaskApplication.exe* hello çıktı dosyası tooAzure depolama yüklediğinde erişim imzası URL'sini bu paylaşılan kullanır. Bunun için hello kod hello bulabilirsiniz `UploadFileToContainer` hello TaskApplication projesinin yönteminde `Program.cs` dosyası:

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a>6. Adım: Görevleri izleme
![Görevleri izleme][6]<br/>
*Merhaba istemci uygulaması (1) izleyiciler tamamlama ve başarı durumu için görevleri hello ve (2) görevler karşıya yükleme sonuç veri tooAzure depolama hello*

Görevleri tooa iş eklendiğinde bunlar otomatik olarak kuyruğa ve hello işle ilişkili hello havuzundaki işlem düğümlerinde yürütülmesi için zamanlanan. Belirttiğiniz hello ayarlarına bağlı olarak, Batch tüm kuyruğa alınan, zamanlama, yeniden deneniyor ve diğer görev yönetimi görevlerini işler.

Toomonitoring görev yürütme birçok yaklaşım vardır. DotNetTutorial, yalnızca tamamlama, görev başarılı veya başarısız durumlarını raporlayan basit bir örnek gösterilmektedir. Merhaba içinde `MonitorTasks` Dotnettutorial'in yönteminde `Program.cs`, tartışmayı destekleyen üç Batch .NET kavramı vardır. Görüntülenme sırasıyla aşağıda listelenmişlerdir:

1. **ODATADetailLevel**: Liste işlemlerinde [ODATADetailLevel][net_odatadetaillevel] belirtilmesi (iş görevlerinin listesini almak gibi) Batch uygulaması performansını sağlamak için önemlidir. Ekleme [hello Azure Batch hizmetinin verimli bir şekilde sorgu](batch-efficient-list-queries.md) toplu iş uygulamalarınız içinde durum izlemenin herhangi sıralama yapmayı planlıyorsanız, liste okuma tooyour.
2. **TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor], görev durumlarının izlenmesi için yardımcı programlara sahip Batch .NET uygulamalarını sağlar. İçinde `MonitorTasks`, *DotNetTutorial* için tüm görevleri tooreach bekler [TaskState.Completed] [ net_taskstate] zaman sınırı içinde. Ardından hello işi sonlandırır.
3. **TerminateJobAsync**: bir işlemle sonlandırma [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (veya hello engelleme JobOperations.TerminateJob) bu işin tamamlandı olarak işaretler. Temel toodo olduğundan bunu Batch çözümünüzü kullanıyorsa, bir [JobReleaseTask][net_jobreltask]. [İş hazırlama ve tamamlama görevleri](batch-job-prep-release.md)’nde açıklanan özel tür bir görevdir.

Merhaba `MonitorTasks` yönteminden *DotNetTutorial*'s `Program.cs` aşağıda yer almaktadır:

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a>7. Adım: Görev çıktısı indirme
![Storage'dan görev çıktısını indirme][7]<br/>

Merhaba iş tamamlandığında, hello görevleri hello çıktısını Azure Storage'dan indirilebilir. Bu çağrı çok yapılır`DownloadBlobsFromContainerAsync` içinde *DotNetTutorial*'s `Program.cs`:

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> Çağrı çok hello`DownloadBlobsFromContainerAsync` hello içinde *DotNetTutorial* uygulama belirtir hello dosyaları indirilen tooyour olmalıdır `%TEMP%` klasör. Ücretsiz toomodify düşünüyorsanız bu konumu çıktı.
>
>

## <a name="step-8-delete-containers"></a>8. Adım: Sil kapsayıcıları
Azure Storage'da yer alan veriler için ücretlendirildiğinizden, Batch işleriniz için artık gerekli olmayan bir fikir tooremove BLOB her zaman sayısıdır. Dotnettutorial'ın `Program.cs`, bu üç çağrı toohello yardımcı yöntemi ile yapılır `DeleteContainerAsync`:

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

Merhaba yöntemin kendisi yalnızca başvuru toohello kapsayıcı edinir ve ardından çağırır [Cloudblobcontainer.deleteıfexistsasync][net_container_delete]:

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>9. adım: hello işi ve hello havuzu silme
Merhaba son adımda Merhaba DotNetTutorial uygulaması tarafından oluşturulan istendiğinde toodelete hello iş ve hello havuzu demektir. İşlerin ve görevlerin kendileri için sizden ücret alınmasa da işlem düğümleri için *ücret alınır*. Bu nedenle, düğümleri yalnızca gerektiğinde ayırmanız önerilir. Kullanılmayan havuzların silinmesi bakım işleminizin bir parçası olabilir.

Merhaba BatchClient's [JobOperations] [ net_joboperations] ve [PoolOperations] [ net_pooloperations] her ikisi de varsa adlı ilgili silme yöntemleri vardır Merhaba kullanıcı silme onaylar:

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> İşlem kaynaklarının ücretli olduğunu unutmayın; kullanılmayan havuzların silinmesi masrafları azaltacaktır. Ayrıca, bir havuzun silinmesinin Bu havuz içindeki tüm işlem düğümlerini siler ve hello havuz silindikten sonra hello düğümlerinde tüm veriler kurtarılamaz olacağını unutmayın.
>
>

## <a name="run-hello-dotnettutorial-sample"></a>Merhaba çalıştırmak *DotNetTutorial* örnek
Merhaba örnek uygulamayı çalıştırdığınızda, hello konsol çıktısı benzer toohello aşağıdaki olacaktır. Yürütme sırasında bir öğesiyle karşılaşacaksınız `Awaiting task completion, timeout in 00:30:00...` hello havuzun işlem düğümleri başlatıldığı sırada. Kullanım hello [Azure portal] [ azure_portal] toomonitor havuzu, işlem düğümleri, işi ve görevleri yürütme sırasında ve sonrasında. Kullanım hello [Azure portal] [ azure_portal] veya hello [Azure Storage Gezgini] [ storage_explorers] olan tooview hello depolama kaynaklarını (kapsayıcılar ve bloblar) Merhaba uygulama tarafından oluşturulur.

Tipik yürütme süresi **yaklaşık 5 dakika** varsayılan yapılandırmasında hello uygulama çalıştırıldığında.

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a>Sonraki adımlar
Ücretsiz toomake değişiklikleri çok eşitleyerek*DotNetTutorial* ve *TaskApplication* tooexperiment farklı olan işlem senaryoları. Örneğin, bir yürütme gecikmesi çok eklemeyi deneyin*TaskApplication*gibi bir durumda olduğu gibi [Thread.Sleep][net_thread_sleep], uzun süre çalışan toosimulate görevler ve bunları hello Portalı'nda izleyebilirsiniz. Deneyin daha fazla görev eklemeye veya işlem düğümleri hello sayısını ayarlama. İçin mantığı toocheck eklemek ve varolan bir havuzu toospeed yürütme saati hello kullanılmasına izin verin (*İpucu*: kullanıma `ArticleHelpers.cs` hello içinde [öğesini kullanıma alın] [ github_samples_common] proje [azure-batch-samples][github_samples]).

Merhaba temel iş akışı Batch çözümünün ile tanıdık, zaman toodig hello Batch hizmetinin ek özelliklerinin toohello içinde olduğu.

* Gözden geçirme hello [genel bakış Azure Batch özelliklerine](batch-api-basics.md) yeni toohello hizmeti olup olmadığınızı öneririz makalesi.
* Başlat'hello altında diğer Batch geliştirmesi makalelerine **geliştirme ayrıntılı** hello içinde [Batch öğrenme yolu][batch_learning_path].
* Hello toplu kullanarak hello "ilk N sözcük" iş yükünü işlemenin farklı bir uygulama kullanıma [TopNWords] [ github_topnwords] örnek.
* Gözden geçirme hello Batch .NET [sürüm notları](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) hello en son değişiklikleri hello Kitaplığı'nda.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Azure Depolama’da kapsayıcı oluşturma"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Karşıya yükleme görev uygulamasını ve girdi (veri) toocontainers dosyaları"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Batch havuzu oluşturma"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Batch işi oluşturma"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Görevleri toojob Ekle"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Görevleri izleme"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Depolama’dan görev çıkışını indirme"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Batch çözümü iş akışı (tam diyagram)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Portalda Batch kimlik bilgileri"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Portalda Depolama kimlik bilgileri"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Batch çözümü iş akışı (minimal diyagram)"
