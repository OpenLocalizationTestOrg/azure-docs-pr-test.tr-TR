---
title: "Merhaba Microsoft Azure Storage veri hareketi kitaplığı ile verileri aaaTransfer | Microsoft Docs"
description: "Blob ve dosya içerikten Hello veri hareketi kitaplığı toomove veya kopya veri tooor kullanın. Yerel dosyalarından veri tooAzure depolama kopyalayın veya içinde veya depolama hesapları arasında veri kopyalayın. Kolayca, veri tooAzure depolama geçirin."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/22/2017
ms.author: seguler
ms.openlocfilehash: 5de902d132565a8eafdc672f7a1a18e1a2db3a06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a>Microsoft Azure Storage veri hareketi kitaplığı hello ile veri aktarımı

## <a name="overview"></a>Genel Bakış
Microsoft Azure Storage veri hareketi kitaplığı Hello karşıya yükleme, indirme ve Azure Storage Bloblarında ve dosyaları kopyalama yüksek performans için tasarlanmış bir platformlar arası açık kaynak kitaplıktır. ' In temelini oluşturan hello çekirdek veri hareketi altyapısını bu kitaplığıdır [AzCopy](storage-use-azcopy.md). Merhaba veri hareketi kitaplığı bizim geleneksel kullanılamaz kullanışlı yöntemler sağlar [.NET Azure Storage istemci Kitaplığı](storage-dotnet-how-to-use-blobs.md). İptal edilen bir aktarımı ve daha fazlasını kolayca sürdürmek, bu hello özelliği tooset hello paralel işlem, izleme aktarma işleminin ilerleme durumunu sayısını içerir.  

Bu kitaplık ayrıca .NET uygulamaları için Windows, Linux ve macOS oluştururken kullanabileceğiniz anlamına gelir .NET Core kullanır. .NET Core hakkında daha fazla toolearn başvuran toohello [.NET Core belgeleri](https://dotnet.github.io/). Bu kitaplık, geleneksel .NET Framework uygulamaları için Windows için de çalışır. 

Bu belge nasıl toocreate .NET Core konsol uygulaması, Windows, Linux ve macOS çalışır ve senaryoları aşağıdaki hello gerçekleştirir gösterir:

- Dosyalar ve dizinler tooBlob depolama karşıya yükleyin.
- Veri aktarırken Hello paralel işlem sayısını tanımlayın.
- Veri aktarımı gelişimi izleme.
- İptal edilen veri aktarımını devam edin. 
- URL tooBlob depolama dosya kopyala. 
- BLOB Storage tooBlob depolama kopyalayın.

**Gerekenler:**

* [Visual Studio Code](https://code.visualstudio.com/)
* Bir [Azure Storage hesabı](storage-create-storage-account.md#create-a-storage-account)

> [!NOTE]
> Bu kılavuz, zaten aşina olduğunuzu varsayar [Azure Storage](https://azure.microsoft.com/services/storage/). Merhaba okuma değil, ise [giriş tooAzure depolama](storage-introduction.md) belgelerine yararlıdır. En önemlisi, çok ihtiyacınız[depolama hesabı oluşturma](storage-create-storage-account.md#create-a-storage-account) toostart kullanarak hello veri hareketi kitaplığı.
> 
> 

## <a name="setup"></a>Kurulum  

1. Merhaba ziyaret [.NET Core Yükleme Kılavuzu](https://www.microsoft.com/net/core) tooinstall .NET Core. Ortamınızı seçerken, hello komut satırı seçeneği belirleyin. 
2. Merhaba komut satırından projeniz için bir dizin oluşturun. Gidin bu dizine yazın `dotnet new` toocreate C# konsol projesi.
3. Bu dizin Visual Studio Code açın. Bu adım hızlı bir şekilde hello komut satırı yazarak yapılabilir `code .`.  
4. Merhaba yüklemek [C# uzantısı](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) hello Visual Studio kod Market gelen. Visual Studio Code'u yeniden başlatın. 
5. Bu noktada, iki istem görmeniz gerekir. "Gerekli varlıklar toobuild ve hata ayıklama" eklemek için biridir "Evet" i tıklatın Çözümlenmemiş bağımlılıkları geri yüklemek için başka bir uyarı içindir. "Geri yükleme".
6. Uygulamanızı şimdi içermelidir bir `launch.json` dosyasını hello altında `.vscode` dizin. Bu dosyada hello değiştirme `externalConsole` çok değer`true`.
7. Visual Studio Code toodebug .NET Core uygulamaları sağlar. İsabet `F5` toorun uygulamanız ve kurulumunuzu çalışır durumda olduğunu doğrulayın. "Hello World!" görmeniz gerekir Yazdırılan toohello Konsolu. 

## <a name="add-data-movement-library-tooyour-project"></a>Veri hareketi kitaplığı tooyour proje ekleyin

1. Merhaba veri hareketi kitaplığı toohello en son sürümünü Hello eklemek `dependencies` bölümü, `project.json` dosya. Merhaba yazıldığı sırada, bu sürüm olacaktır`"Microsoft.Azure.Storage.DataMovement": "0.5.0"` 
2. Ekleme `"portable-net45+win8"` toohello `imports` bölümü. 
3. Bir istem toorestore projenizi görüntülemelidir. Merhaba "geri yükle" düğmesini tıklatın. Ayrıca, projenizin hello komut satırından hello komutu yazarak geri yükleyebilirsiniz `dotnet restore` hello kök proje dizininizin.

Değiştirme `project.json`:

    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {
        "Microsoft.Azure.Storage.DataMovement": "0.5.0"
      },
      "frameworks": {
        "netcoreapp1.1": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "type": "platform",
              "version": "1.1.0"
            }
          },
          "imports": [
            "dnxcore50",
            "portable-net45+win8"
          ]
        }
      }
    }

## <a name="set-up-hello-skeleton-of-your-application"></a>Uygulamanızı Hello çatıyı ayarlayın
Merhaba bunu yapmadan ilk şey uygulamamız hello "çatıyı" kodunu ayarlanır. Bu kod bize için bir depolama hesabı adı ve hesap anahtarı ister ve bu kimlik bilgileri toocreate kullanan bir `CloudStorageAccount` nesnesi. Tüm aktarımı senaryolarda bizim depolama hesabı ile kullanılan toointeract nesnesidir. Merhaba kod ayrıca biz gibi aktarım işlemi toochoose hello türü bize ister tooexecute. 

Değiştirme `Program.cs`:

```csharp
using System;
using System.Threading;
using System.Diagnostics;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.WindowsAzure.Storage.DataMovement;

namespace DMLibSample
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine("Enter Storage account name:");           
            string accountName = Console.ReadLine();

            Console.WriteLine("\nEnter Storage account key:");           
            string accountKey = Console.ReadLine();

            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + accountName + ";AccountKey=" + accountKey;
            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);

            ExecuteChoice(account);
        }

        public static void ExecuteChoice(CloudStorageAccount account)
        {
            Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
            int choice = int.Parse(Console.ReadLine());

            if(choice == 1)
            {
                TransferLocalFileToAzureBlob(account).Wait();
            }
            else if(choice == 2)
            {
                TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
            }
            else if(choice == 3)
            {
                TransferUrlToAzureBlob(account).Wait();
            }
            else if(choice == 4)
            {
                TransferAzureBlobToAzureBlob(account).Wait();
            }
        }

        public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
        {

        }

        public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
        {

        }
    }
}
```

## <a name="transfer-local-file-tooazure-blob"></a>Yerel dosya tooAzure Blob Aktarım
Merhaba yöntemleri ekleyin `GetSourcePath` ve `GetBlob` çok`Program.cs`:

```csharp
public static string GetSourcePath()
{
    Console.WriteLine("\nProvide path for source:");
    string sourcePath = Console.ReadLine();

    return sourcePath;
}

public static CloudBlockBlob GetBlob(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    Console.WriteLine("\nProvide name of new Blob:");
    string blobName = Console.ReadLine();
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    return blob;
}
```

Merhaba değiştirme `TransferLocalFileToAzureBlob` yöntemi:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    await TransferManager.UploadAsync(localFilePath, blob);
    Console.WriteLine("\nTransfer operation complete.");
    ExecuteChoice(account);
}
```

Bu kod bize hello yol tooa yerel dosya, yeni veya mevcut bir kapsayıcı hello adını ve yeni blob hello adını ister. Merhaba `TransferManager.UploadAsync` yöntemi bu bilgileri kullanarak hello karşıya yükleme gerçekleştirir. 

İsabet `F5` toorun uygulamanızı. Bu hello karşıya oluştu depolama hesabınızla hello görüntüleyerek doğrulayabilirsiniz [Microsoft Azure Storage Gezgini](http://storageexplorer.com/).

## <a name="set-number-of-parallel-operations"></a>Paralel işlem sayısını ayarlama
Harika bir özellik tarafından hello veri hareketi kitaplığı hello özelliği tooset hello paralel işlemleri tooincrease hello veri aktarımı verimi sayısı sunulur. Varsayılan olarak, hello veri hareketi kitaplığı kümesi paralel işlemleri too8 hello sayısı * hello makinenizde çekirdek sayısı. 

Düşük bant genişlikli ortamında çok sayıda paralel işlemleri hello ağ bağlantısı doldurmaya ve gerçekte tam olarak tamamlanmasını işlemlerini önlemek aklınızda bulundurun. Bu ayar toodetermine ile tooexperiment neler çalışır en iyi tabanlı kullanılabilir ağ bant genişliğinizi ihtiyacınız vardır. 

Bize tooset hello paralel işlem sayısını verir biraz kod ekleyelim. Ayrıca hello aktarımı toocomplete için gereken süreyi zaman kod ekleyelim.

Ekleme bir `SetNumberOfParallelOperations` yöntemi çok`Program.cs`:

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

Merhaba değiştirme `ExecuteChoice` yöntemi toouse `SetNumberOfParallelOperations`:

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
    int choice = int.Parse(Console.ReadLine());

    SetNumberOfParallelOperations();

    if(choice == 1)
    {
        TransferLocalFileToAzureBlob(account).Wait();
    }
    else if(choice == 2)
    {
        TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
    }
    else if(choice == 3)
    {
        TransferUrlToAzureBlob(account).Wait();
    }
    else if(choice == 4)
    {
        TransferAzureBlobToAzureBlob(account).Wait();
    }
}
```

Merhaba değiştirme `TransferLocalFileToAzureBlob` yöntemi toouse süreölçer:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="track-transfer-progress"></a>Aktarım gelişimi izleme
Bizim veri tootransfer için sürdü ne kadar süreyle bilerek mükemmeldir. Ancak, mümkün toosee hello bizim aktarımı ilerlemesini olan *sırasında* hello aktarım işlemi daha da iyi olacaktır. tooachieve bu senaryo, toocreate ihtiyacımız bir `TransferContext` nesnesi. Merhaba `TransferContext` nesnesi iki biçimde gelir: `SingleTransferContext` ve `DirectoryTransferContext`. Merhaba eski bir tek (ne biz şimdi yaptığınız) dosyasını aktarmak için ve hello ikinci bir dizin (daha sonra ekliyoruz) dosyaları aktarmak için.

Merhaba yöntemleri ekleyin `GetSingleTransferContext` ve `GetDirectoryTransferContext` çok`Program.cs`: 

```csharp
public static SingleTransferContext GetSingleTransferContext(TransferCheckpoint checkpoint)
{
    SingleTransferContext context = new SingleTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}

public static DirectoryTransferContext GetDirectoryTransferContext(TransferCheckpoint checkpoint)
{
    DirectoryTransferContext context = new DirectoryTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}
```

Merhaba değiştirme `TransferLocalFileToAzureBlob` yöntemi toouse `GetSingleTransferContext`:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint);
    Console.WriteLine("\nTransfer started...\n");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob, null, context);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="resume-a-canceled-transfer"></a>İptal edilen bir aktarımı Sürdür
Veri hareketi kitaplığı Hello tarafından sunulan başka bir uygun hello özelliği tooresume iptal edilmiş bir aktarımı özelliğidir. Bize yazarak tootemporarily iptal hello aktarımı sağlar biraz kod ekleyelim `c`ve sonra hello aktarımı 3 saniye sonra sürdürebilirsiniz.

Değiştirme `TransferLocalFileToAzureBlob`:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.UploadAsync(localFilePath, blob, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadAsync(localFilePath, blob, null, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Şimdiye kadar bizim `checkpoint` değeri her zaman ayarlanmış çok`null`. Şimdi, biz hello aktarımı iptal ederseniz, biz hello bizim Aktarım son denetim noktası almak ve sonra bu yeni bir kontrol noktası bizim aktarımı bağlamda kullanın. 

## <a name="transfer-local-directory-tooazure-blob-directory"></a>Yerel tooAzure Blob dizin Aktarım
Merhaba veri hareketi kitaplığı aynı anda yalnızca bir dosya aktarımı istendiği olacaktır. Bu hello durumda değil. Merhaba veri hareketi kitaplığı hello özelliği tootransfer dosyaları ve tüm alt dizinlerinin dizininin sağlar. Bize toodo sağlayan bazı kodu tam olarak bunu ekleyelim.

İlk olarak, hello yöntemi ekleyin `GetBlobDirectory` çok`Program.cs`:

```csharp
public static CloudBlobDirectory GetBlobDirectory(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container. This can be a new or existing Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    CloudBlobDirectory blobDirectory = container.GetDirectoryReference("");

    return blobDirectory;
}
```

Ardından, değiştirin `TransferLocalDirectoryToAzureBlobDirectory`:

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    UploadDirectoryOptions options = new UploadDirectoryOptions()
    {
        Recursive = true
    };

    try
    {
        task = TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetDirectoryTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Bu yöntem ve tek bir dosyayı karşıya yükleme için hello yöntemi arasındaki bazı farklar vardır. Şu anda kullanmakta olduğunuz `TransferManager.UploadDirectoryAsync` ve hello `getDirectoryTransferContext` daha önce oluşturduğumuz yöntemi. Ayrıca, artık sağlıyoruz bir `options` değer bize tooinclude alt dizinleri bizim karşıya istediğimizi tooindicate sağlayan tooour karşıya yükleme işlemi. 

## <a name="copy-file-from-url-tooazure-blob"></a>URL tooAzure Blob dosya Kopyala
Şimdi, bize toocopy URL tooan Azure Blob dosyasından veren kod ekleyelim. 

Değiştirme `TransferUrlToAzureBlob`:

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Başka bir bulut hizmeti (örneğin, AWS) tooAzure toomove verileri gerektiğinde bir önemli kullanım bu özellik için bir durumdur. Veren bir URL'ye sahip olduğu sürece toohello kaynağa erişim, hello kullanarak bu kaynağa Azure BLOB'ları kolayca taşıyabilirsiniz `TransferManager.CopyAsync` yöntemi. Bu yöntem aynı zamanda yeni bir boolean parametresiyle sunar. Bu parametre çok ayarı`true` toodo zaman uyumsuz bir sunucu-tarafı kopyalama istiyoruz gösterir. Bu parametre çok ayarı`false` hello kaynaktır indirilen tooour yerel makine ilk olarak, yani bir zaman uyumlu kopyası - sonra tooAzure Blob karşıya gösterir. Ancak, zaman uyumlu kopyası şu anda yalnızca bir Azure depolama kaynak tooanother kopyalamak için kullanılabilir. 

## <a name="transfer-azure-blob-tooazure-blob"></a>Azure Blob tooAzure Blob Aktarım
Benzersiz şekilde hello veri hareketi kitaplığı tarafından sağlanan başka bir hello özelliği toocopy bir Azure depolama kaynak tooanother gelen özelliğidir. 

Değiştirme `TransferAzureBlobToAzureBlob`:

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(sourceBlob, destinationBlob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(sourceBlob, destinationBlob, false, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Bu örnekte, biz hello Boole parametresi kümesinde `TransferManager.CopyAsync` çok`false` tooindicate toodo zaman uyumlu kopyası istiyoruz. Bu hello kaynak indirilen tooour yerel makine ilk olan, ardından tooAzure Blob karşıya anlamına gelir. kopyalama işlemi tutarlı bir hızda olduğunu mükemmel şekilde tooensure Hello zaman uyumlu kopyası seçenektir. Buna karşılık, zaman uyumsuz bir sunucu tarafı kopyası hello hızına hello kullanılabilir ağ bant genişliği dalgalanma hello sunucuda bağımlıdır. Ancak, zaman uyumlu kopyası ek çıkış karşılaştırıldığında maliyet tooasynchronous kopya oluşturabilir. Merhaba önerilen yaklaşımdır toouse zaman uyumlu kopyası hello bir Azure VM'de aynı bölgede kaynak depolama hesabı tooavoid çıkışı maliyeti.

## <a name="conclusion"></a>Sonuç
Veri taşıma uygulamamız tamamlanmıştır. [Merhaba tam kod örneği Github'da kullanılabilir](https://github.com/azure-samples/storage-dotnet-data-movement-library-app). 

## <a name="next-steps"></a>Sonraki adımlar
Bu Başlarken'de, Azure Storage ile etkileşim kurar ve Windows, Linux ve macOS üzerinde çalışan bir uygulama oluşturduk. Bu Başlarken Blob depolamaya odaklı. Ancak, bu aynı bilgi uygulanan tooFile depolama olabilir. daha fazlasını toolearn kullanıma [Azure Storage veri hareketi kitaplığı başvuru belgeleri](https://azure.github.io/azure-storage-net-data-movement).

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




