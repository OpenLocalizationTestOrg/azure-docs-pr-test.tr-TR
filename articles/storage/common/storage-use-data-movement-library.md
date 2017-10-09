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
ms.openlocfilehash: 9aec6cb171f794cc6ca432938ce499079e7dfdec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="4e6fd-105">Microsoft Azure Storage veri hareketi kitaplığı hello ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="4e6fd-105">Transfer Data with hello Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="4e6fd-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4e6fd-106">Overview</span></span>
<span data-ttu-id="4e6fd-107">Microsoft Azure Storage veri hareketi kitaplığı Hello karşıya yükleme, indirme ve Azure Storage Bloblarında ve dosyaları kopyalama yüksek performans için tasarlanmış bir platformlar arası açık kaynak kitaplıktır.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-107">hello Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="4e6fd-108">' In temelini oluşturan hello çekirdek veri hareketi altyapısını bu kitaplığıdır [AzCopy](../storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="4e6fd-108">This library is hello core data movement framework that powers [AzCopy](../storage-use-azcopy.md).</span></span> <span data-ttu-id="4e6fd-109">Merhaba veri hareketi kitaplığı bizim geleneksel kullanılamaz kullanışlı yöntemler sağlar [.NET Azure Storage istemci Kitaplığı](../blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="4e6fd-109">hello Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](../blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="4e6fd-110">İptal edilen bir aktarımı ve daha fazlasını kolayca sürdürmek, bu hello özelliği tooset hello paralel işlem, izleme aktarma işleminin ilerleme durumunu sayısını içerir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-110">This includes hello ability tooset hello number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="4e6fd-111">Bu kitaplık ayrıca .NET uygulamaları için Windows, Linux ve macOS oluştururken kullanabileceğiniz anlamına gelir .NET Core kullanır.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="4e6fd-112">.NET Core hakkında daha fazla toolearn başvuran toohello [.NET Core belgeleri](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="4e6fd-112">toolearn more about .NET Core, refer toohello [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="4e6fd-113">Bu kitaplık, geleneksel .NET Framework uygulamaları için Windows için de çalışır.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="4e6fd-114">Bu belge nasıl toocreate .NET Core konsol uygulaması, Windows, Linux ve macOS çalışır ve senaryoları aşağıdaki hello gerçekleştirir gösterir:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-114">This document demonstrates how toocreate a .NET Core console application that that runs on Windows, Linux, and macOS and performs hello following scenarios:</span></span>

- <span data-ttu-id="4e6fd-115">Dosyalar ve dizinler tooBlob depolama karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-115">Upload files and directories tooBlob Storage.</span></span>
- <span data-ttu-id="4e6fd-116">Veri aktarırken Hello paralel işlem sayısını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-116">Define hello number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="4e6fd-117">Veri aktarımı gelişimi izleme.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-117">Track data transfer progress.</span></span>
- <span data-ttu-id="4e6fd-118">İptal edilen veri aktarımını devam edin.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="4e6fd-119">URL tooBlob depolama dosya kopyala.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-119">Copy file from URL tooBlob Storage.</span></span> 
- <span data-ttu-id="4e6fd-120">BLOB Storage tooBlob depolama kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-120">Copy from Blob Storage tooBlob Storage.</span></span>

<span data-ttu-id="4e6fd-121">**Gerekenler:**</span><span class="sxs-lookup"><span data-stu-id="4e6fd-121">**What you need:**</span></span>

* [<span data-ttu-id="4e6fd-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="4e6fd-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="4e6fd-123">Bir [Azure Storage hesabı](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="4e6fd-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="4e6fd-124">Bu kılavuz, zaten aşina olduğunuzu varsayar [Azure Storage](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="4e6fd-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="4e6fd-125">Merhaba okuma değil, ise [giriş tooAzure depolama](storage-introduction.md) belgelerine yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-125">If not, reading hello [Introduction tooAzure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="4e6fd-126">En önemlisi, çok ihtiyacınız[depolama hesabı oluşturma](storage-create-storage-account.md#create-a-storage-account) toostart kullanarak hello veri hareketi kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-126">Most importantly, you need too[create a Storage account](storage-create-storage-account.md#create-a-storage-account) toostart using hello Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="4e6fd-127">Kurulum</span><span class="sxs-lookup"><span data-stu-id="4e6fd-127">Setup</span></span>  

1. <span data-ttu-id="4e6fd-128">Merhaba ziyaret [.NET Core Yükleme Kılavuzu](https://www.microsoft.com/net/core) tooinstall .NET Core.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-128">Visit hello [.NET Core Installation Guide](https://www.microsoft.com/net/core) tooinstall .NET Core.</span></span> <span data-ttu-id="4e6fd-129">Ortamınızı seçerken, hello komut satırı seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-129">When selecting your environment, choose hello command-line option.</span></span> 
2. <span data-ttu-id="4e6fd-130">Merhaba komut satırından projeniz için bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-130">From hello command line, create a directory for your project.</span></span> <span data-ttu-id="4e6fd-131">Gidin bu dizine yazın `dotnet new` toocreate C# konsol projesi.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-131">Navigate into this directory, then type `dotnet new` toocreate a C# console project.</span></span>
3. <span data-ttu-id="4e6fd-132">Bu dizin Visual Studio Code açın.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="4e6fd-133">Bu adım hızlı bir şekilde hello komut satırı yazarak yapılabilir `code .`.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-133">This step can be quickly done via hello command line by typing `code .`.</span></span>  
4. <span data-ttu-id="4e6fd-134">Merhaba yüklemek [C# uzantısı](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) hello Visual Studio kod Market gelen.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-134">Install hello [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from hello Visual Studio Code Marketplace.</span></span> <span data-ttu-id="4e6fd-135">Visual Studio Code'u yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="4e6fd-136">Bu noktada, iki istem görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="4e6fd-137">"Gerekli varlıklar toobuild ve hata ayıklama" eklemek için biridir</span><span class="sxs-lookup"><span data-stu-id="4e6fd-137">One is for adding "required assets toobuild and debug."</span></span> <span data-ttu-id="4e6fd-138">"Evet" i tıklatın</span><span class="sxs-lookup"><span data-stu-id="4e6fd-138">Click "yes."</span></span> <span data-ttu-id="4e6fd-139">Çözümlenmemiş bağımlılıkları geri yüklemek için başka bir uyarı içindir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="4e6fd-140">"Geri yükleme".</span><span class="sxs-lookup"><span data-stu-id="4e6fd-140">Click "restore."</span></span>
6. <span data-ttu-id="4e6fd-141">Uygulamanızı şimdi içermelidir bir `launch.json` dosyasını hello altında `.vscode` dizin.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-141">Your application should now contain a `launch.json` file under hello `.vscode` directory.</span></span> <span data-ttu-id="4e6fd-142">Bu dosyada hello değiştirme `externalConsole` çok değer`true`.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-142">In this file, change hello `externalConsole` value too`true`.</span></span>
7. <span data-ttu-id="4e6fd-143">Visual Studio Code toodebug .NET Core uygulamaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-143">Visual Studio Code allows you toodebug .NET Core applications.</span></span> <span data-ttu-id="4e6fd-144">İsabet `F5` toorun uygulamanız ve kurulumunuzu çalışır durumda olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-144">Hit `F5` toorun your application and verify that your setup is working.</span></span> <span data-ttu-id="4e6fd-145">"Hello World!" görmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="4e6fd-145">You should see "Hello World!"</span></span> <span data-ttu-id="4e6fd-146">Yazdırılan toohello Konsolu.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-146">printed toohello console.</span></span> 

## <a name="add-data-movement-library-tooyour-project"></a><span data-ttu-id="4e6fd-147">Veri hareketi kitaplığı tooyour proje ekleyin</span><span class="sxs-lookup"><span data-stu-id="4e6fd-147">Add Data Movement Library tooyour project</span></span>

1. <span data-ttu-id="4e6fd-148">Merhaba veri hareketi kitaplığı toohello en son sürümünü Hello eklemek `dependencies` bölümü, `project.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-148">Add hello latest version of hello Data Movement Library toohello `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="4e6fd-149">Merhaba yazıldığı sırada, bu sürüm olacaktır`"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="4e6fd-149">At hello time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="4e6fd-150">Ekleme `"portable-net45+win8"` toohello `imports` bölümü.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-150">Add `"portable-net45+win8"` toohello `imports` section.</span></span> 
3. <span data-ttu-id="4e6fd-151">Bir istem toorestore projenizi görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-151">A prompt should display toorestore your project.</span></span> <span data-ttu-id="4e6fd-152">Merhaba "geri yükle" düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-152">Click hello "restore" button.</span></span> <span data-ttu-id="4e6fd-153">Ayrıca, projenizin hello komut satırından hello komutu yazarak geri yükleyebilirsiniz `dotnet restore` hello kök proje dizininizin.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-153">You can also restore your project from hello command line by typing hello command `dotnet restore` in hello root of your project directory.</span></span>

<span data-ttu-id="4e6fd-154">Değiştirme `project.json`:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-154">Modify `project.json`:</span></span>

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

## <a name="set-up-hello-skeleton-of-your-application"></a><span data-ttu-id="4e6fd-155">Uygulamanızı Hello çatıyı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="4e6fd-155">Set up hello skeleton of your application</span></span>
<span data-ttu-id="4e6fd-156">Merhaba bunu yapmadan ilk şey uygulamamız hello "çatıyı" kodunu ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-156">hello first thing we do is set up hello "skeleton" code of our application.</span></span> <span data-ttu-id="4e6fd-157">Bu kod bize için bir depolama hesabı adı ve hesap anahtarı ister ve bu kimlik bilgileri toocreate kullanan bir `CloudStorageAccount` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-157">This code prompts us for a Storage account name and account key and uses those credentials toocreate a `CloudStorageAccount` object.</span></span> <span data-ttu-id="4e6fd-158">Tüm aktarımı senaryolarda bizim depolama hesabı ile kullanılan toointeract nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-158">This object is used toointeract with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="4e6fd-159">Merhaba kod ayrıca biz gibi aktarım işlemi toochoose hello türü bize ister tooexecute.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-159">hello code also prompts us toochoose hello type of transfer operation we would like tooexecute.</span></span> 

<span data-ttu-id="4e6fd-160">Değiştirme `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-160">Modify `Program.cs`:</span></span>

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

## <a name="transfer-local-file-tooazure-blob"></a><span data-ttu-id="4e6fd-161">Yerel dosya tooAzure Blob Aktarım</span><span class="sxs-lookup"><span data-stu-id="4e6fd-161">Transfer local file tooAzure Blob</span></span>
<span data-ttu-id="4e6fd-162">Merhaba yöntemleri ekleyin `GetSourcePath` ve `GetBlob` çok`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-162">Add hello methods `GetSourcePath` and `GetBlob` too`Program.cs`:</span></span>

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

<span data-ttu-id="4e6fd-163">Merhaba değiştirme `TransferLocalFileToAzureBlob` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-163">Modify hello `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="4e6fd-164">Bu kod bize hello yol tooa yerel dosya, yeni veya mevcut bir kapsayıcı hello adını ve yeni blob hello adını ister.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-164">This code prompts us for hello path tooa local file, hello name of a new or existing container, and hello name of a new blob.</span></span> <span data-ttu-id="4e6fd-165">Merhaba `TransferManager.UploadAsync` yöntemi bu bilgileri kullanarak hello karşıya yükleme gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-165">hello `TransferManager.UploadAsync` method performs hello upload using this information.</span></span> 

<span data-ttu-id="4e6fd-166">İsabet `F5` toorun uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-166">Hit `F5` toorun your application.</span></span> <span data-ttu-id="4e6fd-167">Bu hello karşıya oluştu depolama hesabınızla hello görüntüleyerek doğrulayabilirsiniz [Microsoft Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="4e6fd-167">You can verify that hello upload occurred by viewing your Storage account with hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="4e6fd-168">Paralel işlem sayısını ayarlama</span><span class="sxs-lookup"><span data-stu-id="4e6fd-168">Set number of parallel operations</span></span>
<span data-ttu-id="4e6fd-169">Harika bir özellik tarafından hello veri hareketi kitaplığı hello özelliği tooset hello paralel işlemleri tooincrease hello veri aktarımı verimi sayısı sunulur.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-169">A great feature offered by hello Data Movement Library is hello ability tooset hello number of parallel operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="4e6fd-170">Varsayılan olarak, hello veri hareketi kitaplığı kümesi paralel işlemleri too8 hello sayısı * hello makinenizde çekirdek sayısı.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-170">By default, hello Data Movement Library sets hello number of parallel operations too8 * hello number of cores on your machine.</span></span> 

<span data-ttu-id="4e6fd-171">Düşük bant genişlikli ortamında çok sayıda paralel işlemleri hello ağ bağlantısı doldurmaya ve gerçekte tam olarak tamamlanmasını işlemlerini önlemek aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm hello network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="4e6fd-172">Bu ayar toodetermine ile tooexperiment neler çalışır en iyi tabanlı kullanılabilir ağ bant genişliğinizi ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-172">You'll need tooexperiment with this setting toodetermine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="4e6fd-173">Bize tooset hello paralel işlem sayısını verir biraz kod ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-173">Let's add some code that allows us tooset hello number of parallel operations.</span></span> <span data-ttu-id="4e6fd-174">Ayrıca hello aktarımı toocomplete için gereken süreyi zaman kod ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-174">Let's also add code that times how long it takes for hello transfer toocomplete.</span></span>

<span data-ttu-id="4e6fd-175">Ekleme bir `SetNumberOfParallelOperations` yöntemi çok`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-175">Add a `SetNumberOfParallelOperations` method too`Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="4e6fd-176">Merhaba değiştirme `ExecuteChoice` yöntemi toouse `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-176">Modify hello `ExecuteChoice` method toouse `SetNumberOfParallelOperations`:</span></span>

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

<span data-ttu-id="4e6fd-177">Merhaba değiştirme `TransferLocalFileToAzureBlob` yöntemi toouse süreölçer:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-177">Modify hello `TransferLocalFileToAzureBlob` method toouse a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="4e6fd-178">Aktarım gelişimi izleme</span><span class="sxs-lookup"><span data-stu-id="4e6fd-178">Track transfer progress</span></span>
<span data-ttu-id="4e6fd-179">Bizim veri tootransfer için sürdü ne kadar süreyle bilerek mükemmeldir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-179">Knowing how long it took for our data tootransfer is great.</span></span> <span data-ttu-id="4e6fd-180">Ancak, mümkün toosee hello bizim aktarımı ilerlemesini olan *sırasında* hello aktarım işlemi daha da iyi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-180">However, being able toosee hello progress of our transfer *during* hello transfer operation would be even better.</span></span> <span data-ttu-id="4e6fd-181">tooachieve bu senaryo, toocreate ihtiyacımız bir `TransferContext` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-181">tooachieve this scenario, we need toocreate a `TransferContext` object.</span></span> <span data-ttu-id="4e6fd-182">Merhaba `TransferContext` nesnesi iki biçimde gelir: `SingleTransferContext` ve `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-182">hello `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="4e6fd-183">Merhaba eski bir tek (ne biz şimdi yaptığınız) dosyasını aktarmak için ve hello ikinci bir dizin (daha sonra ekliyoruz) dosyaları aktarmak için.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-183">hello former is for transferring a single file (which is what we're doing now) and hello latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="4e6fd-184">Merhaba yöntemleri ekleyin `GetSingleTransferContext` ve `GetDirectoryTransferContext` çok`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-184">Add hello methods `GetSingleTransferContext` and `GetDirectoryTransferContext` too`Program.cs`:</span></span> 

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

<span data-ttu-id="4e6fd-185">Merhaba değiştirme `TransferLocalFileToAzureBlob` yöntemi toouse `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-185">Modify hello `TransferLocalFileToAzureBlob` method toouse `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="4e6fd-186">İptal edilen bir aktarımı Sürdür</span><span class="sxs-lookup"><span data-stu-id="4e6fd-186">Resume a canceled transfer</span></span>
<span data-ttu-id="4e6fd-187">Veri hareketi kitaplığı Hello tarafından sunulan başka bir uygun hello özelliği tooresume iptal edilmiş bir aktarımı özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-187">Another convenient feature offered by hello Data Movement Library is hello ability tooresume a canceled transfer.</span></span> <span data-ttu-id="4e6fd-188">Bize yazarak tootemporarily iptal hello aktarımı sağlar biraz kod ekleyelim `c`ve sonra hello aktarımı 3 saniye sonra sürdürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-188">Let's add some code that allows us tootemporarily cancel hello transfer by typing `c`, and then resume hello transfer 3 seconds later.</span></span>

<span data-ttu-id="4e6fd-189">Değiştirme `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

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

<span data-ttu-id="4e6fd-190">Şimdiye kadar bizim `checkpoint` değeri her zaman ayarlanmış çok`null`.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-190">Up until now, our `checkpoint` value has always been set too`null`.</span></span> <span data-ttu-id="4e6fd-191">Şimdi, biz hello aktarımı iptal ederseniz, biz hello bizim Aktarım son denetim noktası almak ve sonra bu yeni bir kontrol noktası bizim aktarımı bağlamda kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-191">Now, if we cancel hello transfer, we retrieve hello last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-tooazure-blob-directory"></a><span data-ttu-id="4e6fd-192">Yerel tooAzure Blob dizin Aktarım</span><span class="sxs-lookup"><span data-stu-id="4e6fd-192">Transfer local directory tooAzure Blob directory</span></span>
<span data-ttu-id="4e6fd-193">Merhaba veri hareketi kitaplığı aynı anda yalnızca bir dosya aktarımı istendiği olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-193">It would be disappointing if hello Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="4e6fd-194">Bu hello durumda değil.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-194">Luckily, this is not hello case.</span></span> <span data-ttu-id="4e6fd-195">Merhaba veri hareketi kitaplığı hello özelliği tootransfer dosyaları ve tüm alt dizinlerinin dizininin sağlar.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-195">hello Data Movement Library provides hello ability tootransfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="4e6fd-196">Bize toodo sağlayan bazı kodu tam olarak bunu ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-196">Let's add some code that allows us toodo just that.</span></span>

<span data-ttu-id="4e6fd-197">İlk olarak, hello yöntemi ekleyin `GetBlobDirectory` çok`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-197">First, add hello method `GetBlobDirectory` too`Program.cs`:</span></span>

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

<span data-ttu-id="4e6fd-198">Ardından, değiştirin `TransferLocalDirectoryToAzureBlobDirectory`:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

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

<span data-ttu-id="4e6fd-199">Bu yöntem ve tek bir dosyayı karşıya yükleme için hello yöntemi arasındaki bazı farklar vardır.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-199">There are a few differences between this method and hello method for uploading a single file.</span></span> <span data-ttu-id="4e6fd-200">Şu anda kullanmakta olduğunuz `TransferManager.UploadDirectoryAsync` ve hello `getDirectoryTransferContext` daha önce oluşturduğumuz yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-200">We're now using `TransferManager.UploadDirectoryAsync` and hello `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="4e6fd-201">Ayrıca, artık sağlıyoruz bir `options` değer bize tooinclude alt dizinleri bizim karşıya istediğimizi tooindicate sağlayan tooour karşıya yükleme işlemi.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-201">In addition, we now provide an `options` value tooour upload operation, which allows us tooindicate that we want tooinclude subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-tooazure-blob"></a><span data-ttu-id="4e6fd-202">URL tooAzure Blob dosya Kopyala</span><span class="sxs-lookup"><span data-stu-id="4e6fd-202">Copy file from URL tooAzure Blob</span></span>
<span data-ttu-id="4e6fd-203">Şimdi, bize toocopy URL tooan Azure Blob dosyasından veren kod ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-203">Now, let's add code that allows us toocopy a file from a URL tooan Azure Blob.</span></span> 

<span data-ttu-id="4e6fd-204">Değiştirme `TransferUrlToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-204">Modify `TransferUrlToAzureBlob`:</span></span>

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

<span data-ttu-id="4e6fd-205">Başka bir bulut hizmeti (örneğin, AWS) tooAzure toomove verileri gerektiğinde bir önemli kullanım bu özellik için bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-205">One important use case for this feature is when you need toomove data from another cloud service (e.g. AWS) tooAzure.</span></span> <span data-ttu-id="4e6fd-206">Veren bir URL'ye sahip olduğu sürece toohello kaynağa erişim, hello kullanarak bu kaynağa Azure BLOB'ları kolayca taşıyabilirsiniz `TransferManager.CopyAsync` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-206">As long as you have a URL that gives you access toohello resource, you can easily move that resource into Azure Blobs by using hello `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="4e6fd-207">Bu yöntem aynı zamanda yeni bir boolean parametresiyle sunar.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="4e6fd-208">Bu parametre çok ayarı`true` toodo zaman uyumsuz bir sunucu-tarafı kopyalama istiyoruz gösterir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-208">Setting this parameter too`true` indicates that we want toodo an asynchronous server-side copy.</span></span> <span data-ttu-id="4e6fd-209">Bu parametre çok ayarı`false` hello kaynaktır indirilen tooour yerel makine ilk olarak, yani bir zaman uyumlu kopyası - sonra tooAzure Blob karşıya gösterir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-209">Setting this parameter too`false` indicates a synchronous copy - meaning hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="4e6fd-210">Ancak, zaman uyumlu kopyası şu anda yalnızca bir Azure depolama kaynak tooanother kopyalamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-210">However, synchronous copy is currently only available for copying from one Azure Storage resource tooanother.</span></span> 

## <a name="transfer-azure-blob-tooazure-blob"></a><span data-ttu-id="4e6fd-211">Azure Blob tooAzure Blob Aktarım</span><span class="sxs-lookup"><span data-stu-id="4e6fd-211">Transfer Azure Blob tooAzure Blob</span></span>
<span data-ttu-id="4e6fd-212">Benzersiz şekilde hello veri hareketi kitaplığı tarafından sağlanan başka bir hello özelliği toocopy bir Azure depolama kaynak tooanother gelen özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-212">Another feature that's uniquely provided by hello Data Movement Library is hello ability toocopy from one Azure Storage resource tooanother.</span></span> 

<span data-ttu-id="4e6fd-213">Değiştirme `TransferAzureBlobToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="4e6fd-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

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

<span data-ttu-id="4e6fd-214">Bu örnekte, biz hello Boole parametresi kümesinde `TransferManager.CopyAsync` çok`false` tooindicate toodo zaman uyumlu kopyası istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-214">In this example, we set hello boolean parameter in `TransferManager.CopyAsync` too`false` tooindicate that we want toodo a synchronous copy.</span></span> <span data-ttu-id="4e6fd-215">Bu hello kaynak indirilen tooour yerel makine ilk olan, ardından tooAzure Blob karşıya anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-215">This means that hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="4e6fd-216">kopyalama işlemi tutarlı bir hızda olduğunu mükemmel şekilde tooensure Hello zaman uyumlu kopyası seçenektir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-216">hello synchronous copy option is a great way tooensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="4e6fd-217">Buna karşılık, zaman uyumsuz bir sunucu tarafı kopyası hello hızına hello kullanılabilir ağ bant genişliği dalgalanma hello sunucuda bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-217">In contrast, hello speed of an asynchronous server-side copy is dependent on hello available network bandwidth on hello server, which can fluctuate.</span></span> <span data-ttu-id="4e6fd-218">Ancak, zaman uyumlu kopyası ek çıkış karşılaştırıldığında maliyet tooasynchronous kopya oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-218">However, synchronous copy may generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="4e6fd-219">Merhaba önerilen yaklaşımdır toouse zaman uyumlu kopyası hello bir Azure VM'de aynı bölgede kaynak depolama hesabı tooavoid çıkışı maliyeti.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-219">hello recommended approach is toouse synchronous copy in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="4e6fd-220">Sonuç</span><span class="sxs-lookup"><span data-stu-id="4e6fd-220">Conclusion</span></span>
<span data-ttu-id="4e6fd-221">Veri taşıma uygulamamız tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-221">Our data movement application is now complete.</span></span> <span data-ttu-id="4e6fd-222">[Merhaba tam kod örneği Github'da kullanılabilir](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="4e6fd-222">[hello full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4e6fd-223">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4e6fd-223">Next steps</span></span>
<span data-ttu-id="4e6fd-224">Bu Başlarken'de, Azure Storage ile etkileşim kurar ve Windows, Linux ve macOS üzerinde çalışan bir uygulama oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="4e6fd-225">Bu Başlarken Blob depolamaya odaklı.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="4e6fd-226">Ancak, bu aynı bilgi uygulanan tooFile depolama olabilir.</span><span class="sxs-lookup"><span data-stu-id="4e6fd-226">However, this same knowledge can be applied tooFile Storage.</span></span> <span data-ttu-id="4e6fd-227">daha fazlasını toolearn kullanıma [Azure Storage veri hareketi kitaplığı başvuru belgeleri](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="4e6fd-227">toolearn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]




