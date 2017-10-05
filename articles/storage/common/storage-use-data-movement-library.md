---
title: "Microsoft Azure Storage veri hareketi kitaplığı ile veri aktarımı | Microsoft Docs"
description: "Veri hareketi kitaplığı taşımak veya için veya blob ve dosya içeriğinden veri kopyalamak için kullanın. Verileri Azure depolama birimine yerel dosyalarından kopyalamak veya içinde veya depolama hesapları arasında veri kopyalama. Kolayca verilerinizi Azure depolama alanına geçiş."
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
ms.openlocfilehash: 7db1761a9a3b8a74a39b2d441849fb89d44cd42b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-data-with-the-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="dbb93-105">Microsoft Azure Storage veri hareketi kitaplığı ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="dbb93-105">Transfer Data with the Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="dbb93-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="dbb93-106">Overview</span></span>
<span data-ttu-id="dbb93-107">Microsoft Azure Storage veri hareketi kitaplığı karşıya yükleme, indirme ve Azure Storage Bloblarında ve dosyaları kopyalama yüksek performans için tasarlanmış bir platformlar arası açık kaynak kitaplıktır.</span><span class="sxs-lookup"><span data-stu-id="dbb93-107">The Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="dbb93-108">' In temelini oluşturan çekirdek veri hareketi altyapısını bu kitaplığıdır [AzCopy](../storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="dbb93-108">This library is the core data movement framework that powers [AzCopy](../storage-use-azcopy.md).</span></span> <span data-ttu-id="dbb93-109">Veri hareketi kitaplığı bizim geleneksel kullanılamaz kullanışlı yöntemler sağlar [.NET Azure Storage istemci Kitaplığı](../blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="dbb93-109">The Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](../blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="dbb93-110">Bu paralel işlem sayısını ayarlayın, aktarma işleminin ilerleme durumunu izlemek, iptal edilen bir aktarımı ve çok daha fazlasını kolayca sürdürme yeteneğini içerir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-110">This includes the ability to set the number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="dbb93-111">Bu kitaplık ayrıca .NET uygulamaları için Windows, Linux ve macOS oluştururken kullanabileceğiniz anlamına gelir .NET Core kullanır.</span><span class="sxs-lookup"><span data-stu-id="dbb93-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="dbb93-112">.NET Core hakkında daha fazla bilgi için bkz [.NET Core belgeleri](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="dbb93-112">To learn more about .NET Core, refer to the [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="dbb93-113">Bu kitaplık, geleneksel .NET Framework uygulamaları için Windows için de çalışır.</span><span class="sxs-lookup"><span data-stu-id="dbb93-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="dbb93-114">Bu belge, Windows, Linux ve macOS üzerinde çalışır ve aşağıdaki senaryolarda gerçekleştiren bir .NET Core konsol uygulaması oluşturmak nasıl gösterir:</span><span class="sxs-lookup"><span data-stu-id="dbb93-114">This document demonstrates how to create a .NET Core console application that that runs on Windows, Linux, and macOS and performs the following scenarios:</span></span>

- <span data-ttu-id="dbb93-115">Dosyalar ve dizinler Blob depolama alanına karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="dbb93-115">Upload files and directories to Blob Storage.</span></span>
- <span data-ttu-id="dbb93-116">Paralel işlem sayısı, veri aktarırken tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="dbb93-116">Define the number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="dbb93-117">Veri aktarımı gelişimi izleme.</span><span class="sxs-lookup"><span data-stu-id="dbb93-117">Track data transfer progress.</span></span>
- <span data-ttu-id="dbb93-118">İptal edilen veri aktarımını devam edin.</span><span class="sxs-lookup"><span data-stu-id="dbb93-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="dbb93-119">Dosya URL'den Blob depolama alanına kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="dbb93-119">Copy file from URL to Blob Storage.</span></span> 
- <span data-ttu-id="dbb93-120">BLOB depolama alanından Blob depolama alanına kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="dbb93-120">Copy from Blob Storage to Blob Storage.</span></span>

<span data-ttu-id="dbb93-121">**Gerekenler:**</span><span class="sxs-lookup"><span data-stu-id="dbb93-121">**What you need:**</span></span>

* [<span data-ttu-id="dbb93-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="dbb93-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="dbb93-123">Bir [Azure Storage hesabı](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="dbb93-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="dbb93-124">Bu kılavuz, zaten aşina olduğunuzu varsayar [Azure Storage](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="dbb93-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="dbb93-125">Değilse, okuma, [Azure Storage'a giriş](storage-introduction.md) belgelerine yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="dbb93-125">If not, reading the [Introduction to Azure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="dbb93-126">En önemlisi, gerek [depolama hesabı oluşturma](storage-create-storage-account.md#create-a-storage-account) veri hareketi kitaplığı kullanmaya başlamak için.</span><span class="sxs-lookup"><span data-stu-id="dbb93-126">Most importantly, you need to [create a Storage account](storage-create-storage-account.md#create-a-storage-account) to start using the Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="dbb93-127">Kurulum</span><span class="sxs-lookup"><span data-stu-id="dbb93-127">Setup</span></span>  

1. <span data-ttu-id="dbb93-128">Ziyaret [.NET Core Yükleme Kılavuzu](https://www.microsoft.com/net/core) .NET Core yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="dbb93-128">Visit the [.NET Core Installation Guide](https://www.microsoft.com/net/core) to install .NET Core.</span></span> <span data-ttu-id="dbb93-129">Ortamınızı seçerken, komut satırı seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="dbb93-129">When selecting your environment, choose the command-line option.</span></span> 
2. <span data-ttu-id="dbb93-130">Komut satırından projeniz için bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dbb93-130">From the command line, create a directory for your project.</span></span> <span data-ttu-id="dbb93-131">Gidin bu dizine yazın `dotnet new` bir C# konsol projesi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="dbb93-131">Navigate into this directory, then type `dotnet new` to create a C# console project.</span></span>
3. <span data-ttu-id="dbb93-132">Bu dizin Visual Studio Code açın.</span><span class="sxs-lookup"><span data-stu-id="dbb93-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="dbb93-133">Bu adım hızla komut satırı yazarak yapılabilir `code .`.</span><span class="sxs-lookup"><span data-stu-id="dbb93-133">This step can be quickly done via the command line by typing `code .`.</span></span>  
4. <span data-ttu-id="dbb93-134">Yükleme [C# uzantısı](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) Visual Studio kod marketten.</span><span class="sxs-lookup"><span data-stu-id="dbb93-134">Install the [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from the Visual Studio Code Marketplace.</span></span> <span data-ttu-id="dbb93-135">Visual Studio Code'u yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="dbb93-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="dbb93-136">Bu noktada, iki istem görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="dbb93-137">"Derleme ve hata ayıklamak için gerekli varlıklar." eklemek için biridir</span><span class="sxs-lookup"><span data-stu-id="dbb93-137">One is for adding "required assets to build and debug."</span></span> <span data-ttu-id="dbb93-138">"Evet" i tıklatın</span><span class="sxs-lookup"><span data-stu-id="dbb93-138">Click "yes."</span></span> <span data-ttu-id="dbb93-139">Çözümlenmemiş bağımlılıkları geri yüklemek için başka bir uyarı içindir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="dbb93-140">"Geri yükleme".</span><span class="sxs-lookup"><span data-stu-id="dbb93-140">Click "restore."</span></span>
6. <span data-ttu-id="dbb93-141">Uygulamanızı şimdi içermelidir bir `launch.json` altında dosya `.vscode` dizin.</span><span class="sxs-lookup"><span data-stu-id="dbb93-141">Your application should now contain a `launch.json` file under the `.vscode` directory.</span></span> <span data-ttu-id="dbb93-142">Bu dosyada değişiklik `externalConsole` değeri `true`.</span><span class="sxs-lookup"><span data-stu-id="dbb93-142">In this file, change the `externalConsole` value to `true`.</span></span>
7. <span data-ttu-id="dbb93-143">Visual Studio Code .NET Core uygulamaları ayıklamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="dbb93-143">Visual Studio Code allows you to debug .NET Core applications.</span></span> <span data-ttu-id="dbb93-144">İsabet `F5` uygulamanızı çalıştırın ve kurulumunuzu çalışır durumda olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="dbb93-144">Hit `F5` to run your application and verify that your setup is working.</span></span> <span data-ttu-id="dbb93-145">"Hello World!" görmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="dbb93-145">You should see "Hello World!"</span></span> <span data-ttu-id="dbb93-146">konsola yazdırılır.</span><span class="sxs-lookup"><span data-stu-id="dbb93-146">printed to the console.</span></span> 

## <a name="add-data-movement-library-to-your-project"></a><span data-ttu-id="dbb93-147">Veri hareketi kitaplığı projenize ekleyin</span><span class="sxs-lookup"><span data-stu-id="dbb93-147">Add Data Movement Library to your project</span></span>

1. <span data-ttu-id="dbb93-148">Veri hareketi kitaplığı için en son sürümünü eklemek `dependencies` bölümü, `project.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="dbb93-148">Add the latest version of the Data Movement Library to the `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="dbb93-149">Bu sürüm yazma zaman olacaktır`"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="dbb93-149">At the time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="dbb93-150">Ekleme `"portable-net45+win8"` için `imports` bölümü.</span><span class="sxs-lookup"><span data-stu-id="dbb93-150">Add `"portable-net45+win8"` to the `imports` section.</span></span> 
3. <span data-ttu-id="dbb93-151">Projenizi geri yüklemek için bir istem görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-151">A prompt should display to restore your project.</span></span> <span data-ttu-id="dbb93-152">"Geri yükleme" düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dbb93-152">Click the "restore" button.</span></span> <span data-ttu-id="dbb93-153">Ayrıca, projenizin komut satırından komutu yazarak geri yükleyebilirsiniz `dotnet restore` proje dizininiz kök.</span><span class="sxs-lookup"><span data-stu-id="dbb93-153">You can also restore your project from the command line by typing the command `dotnet restore` in the root of your project directory.</span></span>

<span data-ttu-id="dbb93-154">Değiştirme `project.json`:</span><span class="sxs-lookup"><span data-stu-id="dbb93-154">Modify `project.json`:</span></span>

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

## <a name="set-up-the-skeleton-of-your-application"></a><span data-ttu-id="dbb93-155">Uygulamanızı çatıyı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="dbb93-155">Set up the skeleton of your application</span></span>
<span data-ttu-id="dbb93-156">Bunu yapmadan ilk şey, uygulamamız "çatıyı" kod ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="dbb93-156">The first thing we do is set up the "skeleton" code of our application.</span></span> <span data-ttu-id="dbb93-157">Bu kod bize için bir depolama hesabı adı ve hesap anahtarı ister ve oluşturmak için bu kimlik bilgilerini kullanan bir `CloudStorageAccount` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="dbb93-157">This code prompts us for a Storage account name and account key and uses those credentials to create a `CloudStorageAccount` object.</span></span> <span data-ttu-id="dbb93-158">Bu nesnenin tüm aktarımı senaryolarda bizim depolama hesabı ile etkileşim kurmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dbb93-158">This object is used to interact with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="dbb93-159">Kod ayrıca bize aktarım işlemi yürütmek için isteriz türünü seçmek için istenir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-159">The code also prompts us to choose the type of transfer operation we would like to execute.</span></span> 

<span data-ttu-id="dbb93-160">Değiştirme `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="dbb93-160">Modify `Program.cs`:</span></span>

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
            Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

## <a name="transfer-local-file-to-azure-blob"></a><span data-ttu-id="dbb93-161">Azure Blob yerel dosya aktarımı</span><span class="sxs-lookup"><span data-stu-id="dbb93-161">Transfer local file to Azure Blob</span></span>
<span data-ttu-id="dbb93-162">Yöntemleri eklemek `GetSourcePath` ve `GetBlob` için `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="dbb93-162">Add the methods `GetSourcePath` and `GetBlob` to `Program.cs`:</span></span>

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

<span data-ttu-id="dbb93-163">Değiştirme `TransferLocalFileToAzureBlob` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="dbb93-163">Modify the `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="dbb93-164">Bu kod bize yolunu yerel bir dosya, yeni veya mevcut bir kapsayıcı adı ve yeni blob adını ister.</span><span class="sxs-lookup"><span data-stu-id="dbb93-164">This code prompts us for the path to a local file, the name of a new or existing container, and the name of a new blob.</span></span> <span data-ttu-id="dbb93-165">`TransferManager.UploadAsync` Yöntemi bu bilgileri kullanarak karşıya yükleme gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-165">The `TransferManager.UploadAsync` method performs the upload using this information.</span></span> 

<span data-ttu-id="dbb93-166">İsabet `F5` uygulamanızı çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="dbb93-166">Hit `F5` to run your application.</span></span> <span data-ttu-id="dbb93-167">Karşıya depolama hesabınızla görüntüleyerek oluştu doğrulayabilirsiniz [Microsoft Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="dbb93-167">You can verify that the upload occurred by viewing your Storage account with the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="dbb93-168">Paralel işlem sayısını ayarlama</span><span class="sxs-lookup"><span data-stu-id="dbb93-168">Set number of parallel operations</span></span>
<span data-ttu-id="dbb93-169">Veri hareketi kitaplığı tarafından sunulan bir büyük veri aktarımı verimliliğini artırmak için paralel işlem sayısını ayarlama özelliği özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-169">A great feature offered by the Data Movement Library is the ability to set the number of parallel operations to increase the data transfer throughput.</span></span> <span data-ttu-id="dbb93-170">Varsayılan olarak, veri hareketi kitaplığı paralel işlem sayısı 8'e ayarlar * makinenizde çekirdek sayısı.</span><span class="sxs-lookup"><span data-stu-id="dbb93-170">By default, the Data Movement Library sets the number of parallel operations to 8 * the number of cores on your machine.</span></span> 

<span data-ttu-id="dbb93-171">Düşük bant genişlikli ortamında çok sayıda paralel işlemleri ağ bağlantısı doldurmaya ve gerçekte tam olarak tamamlanmasını işlemlerini önlemek aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="dbb93-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm the network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="dbb93-172">Kullanılabilir ağ bant genişliğinizi neler en iyi tabanlı çalışır belirlemek için bu ayarı denemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-172">You'll need to experiment with this setting to determine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="dbb93-173">Bize paralel işlem sayısını ayarlamak sağlayan biraz kod ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="dbb93-173">Let's add some code that allows us to set the number of parallel operations.</span></span> <span data-ttu-id="dbb93-174">Ayrıca aktarımı tamamlamak gereken süreyi zaman kod ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="dbb93-174">Let's also add code that times how long it takes for the transfer to complete.</span></span>

<span data-ttu-id="dbb93-175">Ekleme bir `SetNumberOfParallelOperations` yönteme `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="dbb93-175">Add a `SetNumberOfParallelOperations` method to `Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like to use?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="dbb93-176">Değiştirme `ExecuteChoice` yöntemini kullanmak üzere `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="dbb93-176">Modify the `ExecuteChoice` method to use `SetNumberOfParallelOperations`:</span></span>

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

<span data-ttu-id="dbb93-177">Değiştirme `TransferLocalFileToAzureBlob` süreölçer kullanılacak yöntemi:</span><span class="sxs-lookup"><span data-stu-id="dbb93-177">Modify the `TransferLocalFileToAzureBlob` method to use a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="dbb93-178">Aktarım gelişimi izleme</span><span class="sxs-lookup"><span data-stu-id="dbb93-178">Track transfer progress</span></span>
<span data-ttu-id="dbb93-179">Bizim veri aktarmak sürdü ne kadar süreyle bilerek mükemmeldir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-179">Knowing how long it took for our data to transfer is great.</span></span> <span data-ttu-id="dbb93-180">Bizim aktarımı ilerlemesini ancak geçirebilmek *sırasında* aktarım işlemi daha iyi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="dbb93-180">However, being able to see the progress of our transfer *during* the transfer operation would be even better.</span></span> <span data-ttu-id="dbb93-181">Bu senaryo elde etmek için oluşturmamız gerekir bir `TransferContext` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="dbb93-181">To achieve this scenario, we need to create a `TransferContext` object.</span></span> <span data-ttu-id="dbb93-182">`TransferContext` Nesnesi iki biçimde gelir: `SingleTransferContext` ve `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="dbb93-182">The `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="dbb93-183">Eski (olan ne biz şimdi yaptığınız) tek dosya aktarmak için ve ikinci bir dizin (daha sonra ekliyoruz) dosyaları aktarmak için.</span><span class="sxs-lookup"><span data-stu-id="dbb93-183">The former is for transferring a single file (which is what we're doing now) and the latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="dbb93-184">Yöntemleri eklemek `GetSingleTransferContext` ve `GetDirectoryTransferContext` için `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="dbb93-184">Add the methods `GetSingleTransferContext` and `GetDirectoryTransferContext` to `Program.cs`:</span></span> 

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

<span data-ttu-id="dbb93-185">Değiştirme `TransferLocalFileToAzureBlob` yöntemini kullanmak üzere `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="dbb93-185">Modify the `TransferLocalFileToAzureBlob` method to use `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="dbb93-186">İptal edilen bir aktarımı Sürdür</span><span class="sxs-lookup"><span data-stu-id="dbb93-186">Resume a canceled transfer</span></span>
<span data-ttu-id="dbb93-187">Veri hareketi kitaplığı tarafından sunulan başka bir uygun iptal edilmiş bir aktarımı sürdürebilme özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-187">Another convenient feature offered by the Data Movement Library is the ability to resume a canceled transfer.</span></span> <span data-ttu-id="dbb93-188">Geçici olarak yazarak aktarımı iptal kurmamızı sağlayan biraz kod ekleyelim `c`ve ardından aktarımı 3 saniye sonra sürdürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbb93-188">Let's add some code that allows us to temporarily cancel the transfer by typing `c`, and then resume the transfer 3 seconds later.</span></span>

<span data-ttu-id="dbb93-189">Değiştirme `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="dbb93-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="dbb93-190">Şimdiye kadar bizim `checkpoint` değeri her zaman sınıflandırmalara ayarlandığı `null`.</span><span class="sxs-lookup"><span data-stu-id="dbb93-190">Up until now, our `checkpoint` value has always been set to `null`.</span></span> <span data-ttu-id="dbb93-191">Şimdi, biz aktarımı iptal ederseniz, biz bizim aktarımı son denetim noktası almak ve sonra bu yeni bir kontrol noktası bizim aktarımı bağlamda kullanın.</span><span class="sxs-lookup"><span data-stu-id="dbb93-191">Now, if we cancel the transfer, we retrieve the last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-to-azure-blob-directory"></a><span data-ttu-id="dbb93-192">Yerel dizin Azure Blob dizinine aktarma</span><span class="sxs-lookup"><span data-stu-id="dbb93-192">Transfer local directory to Azure Blob directory</span></span>
<span data-ttu-id="dbb93-193">Veri hareketi kitaplığı aynı anda yalnızca bir dosya aktarımı istendiği olacaktır.</span><span class="sxs-lookup"><span data-stu-id="dbb93-193">It would be disappointing if the Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="dbb93-194">Bu durumda değil.</span><span class="sxs-lookup"><span data-stu-id="dbb93-194">Luckily, this is not the case.</span></span> <span data-ttu-id="dbb93-195">Veri hareketi kitaplığı dosyaları ve tüm alt dizinlerinin dizini transfer olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="dbb93-195">The Data Movement Library provides the ability to transfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="dbb93-196">Bunu kurmamızı sağlayan biraz kod ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="dbb93-196">Let's add some code that allows us to do just that.</span></span>

<span data-ttu-id="dbb93-197">İlk olarak, yöntemi ekleyin `GetBlobDirectory` için `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="dbb93-197">First, add the method `GetBlobDirectory` to `Program.cs`:</span></span>

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

<span data-ttu-id="dbb93-198">Ardından, değiştirin `TransferLocalDirectoryToAzureBlobDirectory`:</span><span class="sxs-lookup"><span data-stu-id="dbb93-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="dbb93-199">Bu yöntem ve tek bir dosyayı karşıya yükleme için kullanılan yöntem arasındaki bazı farklar vardır.</span><span class="sxs-lookup"><span data-stu-id="dbb93-199">There are a few differences between this method and the method for uploading a single file.</span></span> <span data-ttu-id="dbb93-200">Şu anda kullanmakta olduğunuz `TransferManager.UploadDirectoryAsync` ve `getDirectoryTransferContext` daha önce oluşturduğumuz yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dbb93-200">We're now using `TransferManager.UploadDirectoryAsync` and the `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="dbb93-201">Ayrıca, artık sağlıyoruz bir `options` bizim karşıya alt dizinleri dahil etmek istiyoruz belirtmek kurmamızı sağlayan bizim karşıya yükleme işlemi için değer.</span><span class="sxs-lookup"><span data-stu-id="dbb93-201">In addition, we now provide an `options` value to our upload operation, which allows us to indicate that we want to include subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-to-azure-blob"></a><span data-ttu-id="dbb93-202">Dosyayı Azure Blob URL'den kopyalayın</span><span class="sxs-lookup"><span data-stu-id="dbb93-202">Copy file from URL to Azure Blob</span></span>
<span data-ttu-id="dbb93-203">Şimdi, bize bir dosyayı Azure Blob için bir URL'den kopyalamak veren kod ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="dbb93-203">Now, let's add code that allows us to copy a file from a URL to an Azure Blob.</span></span> 

<span data-ttu-id="dbb93-204">Değiştirme `TransferUrlToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="dbb93-204">Modify `TransferUrlToAzureBlob`:</span></span>

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="dbb93-205">Bu özellik için bir önemli kullanım örneği, verileri başka bir bulut hizmetinden (örneğin, AWS) Azure'a taşımak gereken zamandır.</span><span class="sxs-lookup"><span data-stu-id="dbb93-205">One important use case for this feature is when you need to move data from another cloud service (e.g. AWS) to Azure.</span></span> <span data-ttu-id="dbb93-206">Kaynağa erişim sağlayan bir URL'ye sahip olduğu sürece, kolayca bu kaynak Azure BLOB'ları kullanarak taşıyabilirsiniz `TransferManager.CopyAsync` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dbb93-206">As long as you have a URL that gives you access to the resource, you can easily move that resource into Azure Blobs by using the `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="dbb93-207">Bu yöntem aynı zamanda yeni bir boolean parametresiyle sunar.</span><span class="sxs-lookup"><span data-stu-id="dbb93-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="dbb93-208">Bu parametre ayarını `true` zaman uyumsuz bir sunucu tarafı kopya yapmak istiyoruz gösterir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-208">Setting this parameter to `true` indicates that we want to do an asynchronous server-side copy.</span></span> <span data-ttu-id="dbb93-209">Bu parametre ayarını `false` kaynak bizim yerel makineye ilk indirilir, sonra Azure Blob karşıya anlamı zaman uyumlu kopyası - gösterir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-209">Setting this parameter to `false` indicates a synchronous copy - meaning the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="dbb93-210">Ancak, zaman uyumlu kopyası şu anda yalnızca bir Azure depolama kaynağının diğerine kopyalamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-210">However, synchronous copy is currently only available for copying from one Azure Storage resource to another.</span></span> 

## <a name="transfer-azure-blob-to-azure-blob"></a><span data-ttu-id="dbb93-211">Azure Blob Azure Blob Aktarım</span><span class="sxs-lookup"><span data-stu-id="dbb93-211">Transfer Azure Blob to Azure Blob</span></span>
<span data-ttu-id="dbb93-212">Benzersiz olarak veri hareketi kitaplığı tarafından sağlanan başka bir Azure depolama kaynağının diğerine kopyalama becerisini özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-212">Another feature that's uniquely provided by the Data Movement Library is the ability to copy from one Azure Storage resource to another.</span></span> 

<span data-ttu-id="dbb93-213">Değiştirme `TransferAzureBlobToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="dbb93-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="dbb93-214">Bu örnekte, biz Boole parametresi kümesinde `TransferManager.CopyAsync` için `false` biz zaman uyumlu bir kopya yapmak istediğinizi belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="dbb93-214">In this example, we set the boolean parameter in `TransferManager.CopyAsync` to `false` to indicate that we want to do a synchronous copy.</span></span> <span data-ttu-id="dbb93-215">Bu kaynak bizim yerel makineye ilk indirilir, sonra Azure Blob karşıya olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-215">This means that the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="dbb93-216">Zaman uyumlu kopyası seçeneği, kopyalama işlemi tutarlı bir hızda olduğundan emin olmak için harika bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="dbb93-216">The synchronous copy option is a great way to ensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="dbb93-217">Buna karşılık, zaman uyumsuz bir sunucu tarafı kopyası hızına kullanılabilir ağ bant genişliği dalgalanma sunucuya bağlı.</span><span class="sxs-lookup"><span data-stu-id="dbb93-217">In contrast, the speed of an asynchronous server-side copy is dependent on the available network bandwidth on the server, which can fluctuate.</span></span> <span data-ttu-id="dbb93-218">Ancak, zaman uyumlu kopyası zaman uyumsuz kopyaya karşılaştırıldığında ek çıkışı maliyeti oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-218">However, synchronous copy may generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="dbb93-219">Önerilen yaklaşım çıkışı maliyeti önlemek için kaynak depolama hesabınız ile aynı bölgede olan Azure VM'deki zaman uyumlu kopyası kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="dbb93-219">The recommended approach is to use synchronous copy in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="dbb93-220">Sonuç</span><span class="sxs-lookup"><span data-stu-id="dbb93-220">Conclusion</span></span>
<span data-ttu-id="dbb93-221">Veri taşıma uygulamamız tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="dbb93-221">Our data movement application is now complete.</span></span> <span data-ttu-id="dbb93-222">[Tam kod örneği Github'da kullanılabilir](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="dbb93-222">[The full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dbb93-223">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dbb93-223">Next steps</span></span>
<span data-ttu-id="dbb93-224">Bu Başlarken'de, Azure Storage ile etkileşim kurar ve Windows, Linux ve macOS üzerinde çalışan bir uygulama oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="dbb93-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="dbb93-225">Bu Başlarken Blob depolamaya odaklı.</span><span class="sxs-lookup"><span data-stu-id="dbb93-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="dbb93-226">Ancak, aynı bu bilgiye dosya depolama birimine uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="dbb93-226">However, this same knowledge can be applied to File Storage.</span></span> <span data-ttu-id="dbb93-227">Daha fazla bilgi için kullanıma [Azure Storage veri hareketi kitaplığı başvuru belgeleri](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="dbb93-227">To learn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]




