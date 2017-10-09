---
title: "aaaGet başlatılan .NET kullanarak Azure Blob storage'ı (nesne depolama) | Microsoft Docs"
description: "Azure Blob storage (nesne depolama) ile Merhaba bulutta yapılandırılmamış veri depolayın."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 9b675ac073e7e901fe1afe54f7bfea12eefbf3ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="e5fa2-103">.NET kullanarak Azure Blob Storage’ı kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="e5fa2-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="e5fa2-104">Azure Blob Depolama hello bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-104">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="e5fa2-105">Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="e5fa2-106">BLOB Depolama başvurulan tooas nesne depolama de olabilir.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-106">Blob storage is also referred tooas object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="e5fa2-107">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="e5fa2-107">About this tutorial</span></span>
<span data-ttu-id="e5fa2-108">Bu öğretici, Azure Blob storage kullanarak bazı genel senaryolar için .NET toowrite kodu nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-108">This tutorial shows how toowrite .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="e5fa2-109">Kapsanan senaryolar arasında blob yükleme, listeleme, indirme ve silme yer alır.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="e5fa2-110">**Ön koşullar:**</span><span class="sxs-lookup"><span data-stu-id="e5fa2-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="e5fa2-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e5fa2-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="e5fa2-112">.NET için Azure Depolama İstemcisi</span><span class="sxs-lookup"><span data-stu-id="e5fa2-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="e5fa2-113">.NET için Azure Yapılandırma Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="e5fa2-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="e5fa2-114">Bir [Azure Storage hesabı](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="e5fa2-114">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="e5fa2-115">Daha fazla örnek</span><span class="sxs-lookup"><span data-stu-id="e5fa2-115">More samples</span></span>
<span data-ttu-id="e5fa2-116">Blob depolama kullanan diğer örnekler için [.NET’te Azure Blob Depolama Kullanmaya Başlama](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="e5fa2-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="e5fa2-117">Merhaba örnek uygulamayı indirin ve çalıştırın veya hello kodu github'da göz atın.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-117">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="e5fa2-118">Using yönergeleri ekleme</span><span class="sxs-lookup"><span data-stu-id="e5fa2-118">Add using directives</span></span>
<span data-ttu-id="e5fa2-119">Merhaba aşağıdakileri ekleyin **kullanarak** hello yönergeleri toohello üst `Program.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="e5fa2-119">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="e5fa2-120">Merhaba bağlantı dizesini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="e5fa2-120">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a><span data-ttu-id="e5fa2-121">Merhaba Blob hizmeti istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5fa2-121">Create hello Blob service client</span></span>
<span data-ttu-id="e5fa2-122">Merhaba **CloudBlobClient** sınıfı sağlar, size, tooretrieve kapsayıcılar ve bloblar Blob depolama alanına depolanır.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-122">hello **CloudBlobClient** class enables you tooretrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="e5fa2-123">Tek yönlü toocreate hello hizmeti istemcisi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e5fa2-123">Here's one way toocreate hello service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="e5fa2-124">Artık veri okuyan ve yazan veri tooBlob depolama hazır toowrite kodu bulunur.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-124">Now you are ready toowrite code that reads data from and writes data tooBlob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="e5fa2-125">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5fa2-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="e5fa2-126">Bu örnekte gösterilir nasıl toocreate zaten yoksa, bir kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="e5fa2-126">This example shows how toocreate a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="e5fa2-127">Varsayılan olarak, hello yeni kapsayıcı depolama erişim anahtarı toodownload bloblarınızın bu kapsayıcısından belirlemeniz gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-127">By default, hello new container is private, meaning that you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="e5fa2-128">Merhaba kapsayıcı kullanılabilir tooeveryone içindeki toomake hello dosyaları istiyorsanız hello kapsayıcı toobe ortak koddan hello kullanarak ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e5fa2-128">If you want toomake hello files within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="e5fa2-129">Merhaba Internet üzerinden herkes ortak bir kapsayıcıdaki blobları görebilir.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-129">Anyone on hello Internet can see blobs in a public container.</span></span> <span data-ttu-id="e5fa2-130">Ancak, değiştirme veya yalnızca hello uygun hesap erişim tuşu veya paylaşılan erişim imzası varsa silin.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-130">However, you can modify or delete them only if you have hello appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="e5fa2-131">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="e5fa2-131">Upload a blob into a container</span></span>
<span data-ttu-id="e5fa2-132">Azure Blob Storage blok blobları ve sayfa bloblarını destekler.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="e5fa2-133">Çoğu durumda, blok blob türü toouse önerilen hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-133">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="e5fa2-134">tooupload dosya tooa blok blob bir kapsayıcı başvurusu alın ve blok blob başvurusu tooget kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-134">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="e5fa2-135">Bir blob başvurusu edindiğinizde arama hello tarafından herhangi bir veri tooit akışıdır yükleyebilirsiniz **UploadFromStream** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-135">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="e5fa2-136">Bu işlem daha önce bulunamadı veya mevcut değilse bu raporun üzerine hello blob oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-136">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="e5fa2-137">örnekte gösterildiği nasıl aşağıdaki hello tooupload blob bir kapsayıcı halinde ve o hello kapsayıcısı zaten oluşturulduğu varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-137">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="e5fa2-138">Liste hello BLOB'ları bir kapsayıcıda</span><span class="sxs-lookup"><span data-stu-id="e5fa2-138">List hello blobs in a container</span></span>
<span data-ttu-id="e5fa2-139">toolist hello BLOB'ları bir kapsayıcıda, ilk olarak bir kapsayıcı başvurusu alın.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-139">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="e5fa2-140">Merhaba kapsayıcının sonra kullanabileceğiniz **ListBlobs** yöntemi tooretrieve hello blobları ve/veya dizinleri içindeki.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-140">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="e5fa2-141">tooaccess hello zengin özellik ve yöntem **Ilistblobıtem**, tooa atamalısınız **CloudBlockBlob**, **CloudPageBlob**, veya  **CloudBlobDirectory** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-141">tooaccess hello  rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="e5fa2-142">Merhaba türü bilinmiyor, hangi toocast türü onay toodetermine kullanabilirsiniz için.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-142">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="e5fa2-143">Merhaba aşağıdaki kodu nasıl tooretrieve ve çıktı hello her öğe URI'sini hello gösterir _fotoğraf_ kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="e5fa2-143">hello following code demonstrates how tooretrieve and output hello URI of each item in hello _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, false))
{
    if (item.GetType() == typeof(CloudBlockBlob))
    {
        CloudBlockBlob blob = (CloudBlockBlob)item;

        Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);

    }
    else if (item.GetType() == typeof(CloudPageBlob))
    {
        CloudPageBlob pageBlob = (CloudPageBlob)item;

        Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);

    }
    else if (item.GetType() == typeof(CloudBlobDirectory))
    {
        CloudBlobDirectory directory = (CloudBlobDirectory)item;

        Console.WriteLine("Directory: {0}", directory.Uri);
    }
}
```

<span data-ttu-id="e5fa2-144">Blob adlarına yol bilgilerini ekleyerek, geleneksel bir dosya sisteminde olduğu gibi düzenleme ve geçiş yapabileceğiniz sanal bir dizin yapısı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="e5fa2-145">Merhaba dizin yapısını sanal Blob depolama alanına kullanılabilir kaynakları kapsayıcılar ve bloblar yalnızca yalnızca--hello.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-145">hello directory structure is virtual only--hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="e5fa2-146">Ancak, hello depolama istemci kitaplığı sunar bir **CloudBlobDirectory** nesne toorefer tooa sanal dizini ve bu şekilde düzenlenen BLOB'ları ile çalışmanın hello işlemini basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-146">However, hello storage client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="e5fa2-147">Örneğin, adlandırılmış bir kapsayıcıda blok blobları kümesine aşağıdaki hello göz önünde bulundurun *fotoğraf*:</span><span class="sxs-lookup"><span data-stu-id="e5fa2-147">For example, consider hello following set of block blobs in a container named *photos*:</span></span>

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

<span data-ttu-id="e5fa2-148">Çağırdığınızda **ListBlobs** hello üzerinde *fotoğraf* kapsayıcı (önceki kod parçacığını hello olduğu gibi), hiyerarşik bir listeleme döner.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-148">When you call **ListBlobs** on hello *photos* container (as in hello preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="e5fa2-149">Her ikisi de içeren **CloudBlobDirectory** ve **CloudBlockBlob** hello dizinleri ve blobları hello kapsayıcıda sırasıyla temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing hello directories and blobs in hello container, respectively.</span></span> <span data-ttu-id="e5fa2-150">Merhaba sonuçta çıktı şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="e5fa2-150">hello resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="e5fa2-151">İsteğe bağlı olarak, hello ayarlayabilirsiniz **Listblobs** hello parametresinin **ListBlobs** yönteme **doğru**.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-151">Optionally, you can set hello **UseFlatBlobListing** parameter of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="e5fa2-152">Bu durumda, hello kapsayıcıdaki her blob olarak döndürülür bir **CloudBlockBlob** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-152">In this case, every blob in hello container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="e5fa2-153">Çağrı çok hello**ListBlobs** tooreturn düz listeleme şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="e5fa2-153">hello call too**ListBlobs** tooreturn a flat listing looks like this:</span></span>

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="e5fa2-154">ve hello sonuçlar şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="e5fa2-154">and hello results look like this:</span></span>

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a><span data-ttu-id="e5fa2-155">Blob’ları indirme</span><span class="sxs-lookup"><span data-stu-id="e5fa2-155">Download blobs</span></span>
<span data-ttu-id="e5fa2-156">toodownload BLOB'lar, ilk olarak bir blob başvurusu alın ve ardından hello çağırın **DownloadToStream** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-156">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="e5fa2-157">Merhaba aşağıdaki örnek kullanır hello **DownloadToStream** yöntemi tootransfer hello blob içeriği tooa stream nesnesi tooa yerel dosya daha sonra devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-157">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="e5fa2-158">Merhaba de kullanabilirsiniz **DownloadToStream** yöntemi toodownload hello içeriği blob olarak bir metin dizesi.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-158">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="e5fa2-159">Blob’ları silme</span><span class="sxs-lookup"><span data-stu-id="e5fa2-159">Delete blobs</span></span>
<span data-ttu-id="e5fa2-160">toodelete bir blob önce bir blob başvurusu alın ve ardından arama **silmek** yöntemini.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-160">toodelete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="e5fa2-161">Blob’ları sayfalarda zaman uyumsuz olarak listeleme</span><span class="sxs-lookup"><span data-stu-id="e5fa2-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="e5fa2-162">Çok sayıda BLOB listeliyorsanız veya toocontrol hello bir listeleme işlemi ile dönen sonuç sayısını isterseniz sonuç sayfalarında blobları listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-162">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="e5fa2-163">Böylece yürütme tooreturn büyük bir sonuç kümesi beklenirken engellenmeyen Bu örnek nasıl tooreturn sayfalarında zaman uyumsuz olarak sonuçları gösterir.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-163">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="e5fa2-164">Bu örnek düz bir blob listesi gösterir, ancak ayarı hello tarafından da hiyerarşik bir listeleme gerçekleştirebilirsiniz _Listblobs_ hello parametresinin **ListBlobsSegmentedAsync** yöntemi too_false_.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello _useFlatBlobListing_ parameter of hello **ListBlobsSegmentedAsync** method too_false_.</span></span>

<span data-ttu-id="e5fa2-165">Merhaba örnek yöntemi zaman uyumsuz bir yöntem çağırdığı için onu hello ile dönmelidir _zaman uyumsuz_ anahtar sözcüğü ve döndürmelidir bir **görev** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-165">Because hello sample method calls an asynchronous method, it must be prefaced with hello _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="e5fa2-166">Merhaba await hello için belirtilen anahtar sözcüğü **ListBlobsSegmentedAsync** yöntemi hello listeleme görevi tamamlanana kadar hello örnek yönteminin yürütülmesi askıya alır.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-166">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get hello continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="e5fa2-167">Yazma tooan blob ekleme</span><span class="sxs-lookup"><span data-stu-id="e5fa2-167">Writing tooan append blob</span></span>
<span data-ttu-id="e5fa2-168">Ek blob, günlük tutma gibi ekleme işlemleri için en iyi duruma getirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="e5fa2-169">Bir blok blobu gibi bir ek blobu bloklardan oluşur, ancak yeni bir blok tooan ek blob eklediğinizde, bu her zaman eklenmiş toohello hello blob sonudur.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="e5fa2-170">Bir ek blobdaki mevcut bloğu güncelleştiremezsiniz veya silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="e5fa2-171">bir blok blobu olduğu gibi bir ek blobu Hello blok kimliği gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-171">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="e5fa2-172">Her bir ek blobu bloğunda tooa en fazla 4 MB yukarı farklı bir boyutta olabilir ve bir ek blobu en fazla 50.000 blok içerebilir.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-172">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="e5fa2-173">Merhaba en fazla bir ek blobu bu nedenle biraz 195 GB'tan (4 MB X 50.000 blok) boyutudur.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-173">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="e5fa2-174">Aşağıdaki Hello örnek yeni bir ek blob oluşturur ve basit günlük yazma işlemini benzeterek bazı veri tooit ekler.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-174">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="e5fa2-175">Bkz: [anlama blok Blobları, sayfa Blobları ve ek Bloblarını](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) hello hello üç türde BLOB arasındaki farklar hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about hello differences between hello three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="e5fa2-176">Blobların güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="e5fa2-176">Managing security for blobs</span></span>
<span data-ttu-id="e5fa2-177">Varsayılan olarak, Azure depolama, verilerinizi hello hesabı erişim anahtarlarını elinde olan erişim toohello hesabına sahip sınırlayarak güvende tutar.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-177">By default, Azure Storage keeps your data secure by limiting access toohello account owner, who is in possession of hello account access keys.</span></span> <span data-ttu-id="e5fa2-178">Depolama hesabınızı tooshare blob verilerini gerektiğinde, önemli toodo olduğundan bunu hesap erişim tuşlarınızı hello güvenliğini tehlikeye olmadan.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-178">When you need tooshare blob data in your storage account, it is important toodo so without compromising hello security of your account access keys.</span></span> <span data-ttu-id="e5fa2-179">Ayrıca, Azure storage'da ve hello kablo üzerinden giderek güvenlidir blob veri tooensure şifreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-179">Additionally, you can encrypt blob data tooensure that it is secure going over hello wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a><span data-ttu-id="e5fa2-180">Erişim tooblob veri denetleme</span><span class="sxs-lookup"><span data-stu-id="e5fa2-180">Controlling access tooblob data</span></span>
<span data-ttu-id="e5fa2-181">Varsayılan olarak, depolama hesabınızda blob verileri hello erişilebilir yalnızca toostorage hesap sahibi değil.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-181">By default, hello blob data in your storage account is accessible only toostorage account owner.</span></span> <span data-ttu-id="e5fa2-182">Blob Storage'a karşı istek kimlik doğrulaması varsayılan olarak hello hesap erişim tuşu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-182">Authenticating requests against Blob storage requires hello account access key by default.</span></span> <span data-ttu-id="e5fa2-183">Ancak, toomake isteyebilir belirli blob veri kullanılabilir tooother kullanıcıları.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-183">However, you may wish toomake certain blob data available tooother users.</span></span> <span data-ttu-id="e5fa2-184">İki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="e5fa2-184">You have two options:</span></span>

* <span data-ttu-id="e5fa2-185">**Anonim erişim:** Bir kapsayıcıyı veya bloblarını anonim erişim için genel erişime açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="e5fa2-186">Bkz: [anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](storage-manage-access-to-resources.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-186">See [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="e5fa2-187">**Paylaşılan erişim imzası:** istemcileri belirlediğiniz izinlerle ve belirttiğiniz bir aralığında depolama hesabınızdaki atanmış erişim tooa kaynak sağlayan bir paylaşılan erişim imzası (SAS) sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access tooa resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="e5fa2-188">Daha fazla bilgi edinmek için bkz. [Paylaşılan Erişim İmzaları (SAS) kullanma](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="e5fa2-188">See [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="e5fa2-189">Blob verilerini şifreleme</span><span class="sxs-lookup"><span data-stu-id="e5fa2-189">Encrypting blob data</span></span>
<span data-ttu-id="e5fa2-190">Azure depolama hello istemcide hem hello sunucuda blob verisi şifreleme özelliği destekler.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-190">Azure Storage supports encrypting blob data both at hello client and on hello server:</span></span>

* <span data-ttu-id="e5fa2-191">**İstemci tarafı şifreleme:** tooAzure depolama karşıya yükleme ve toohello istemci indirilirken verilerin şifresini çözmek önce istemci uygulamalar içinde şifrelenen verilerin .NET desteklediği için depolama istemci kitaplığı hello.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-191">**Client-side encryption:** hello Storage Client Library for .NET supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span> <span data-ttu-id="e5fa2-192">Merhaba kitaplık ayrıca depolama hesabı anahtarı yönetimi için Azure anahtar kasası ile tümleştirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-192">hello library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="e5fa2-193">Daha fazla bilgi için bkz. [Microsoft Azure Storage için .NET içinde İstemci Tarafı Şifreleme](storage-client-side-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="e5fa2-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](storage-client-side-encryption.md) for more information.</span></span> <span data-ttu-id="e5fa2-194">Ayrıca bkz. [Öğretici: Azure Anahtar Kasası kullanılarak Microsoft Azure Storage’daki blobları şifreleme ve şifresini çözme](storage-encrypt-decrypt-blobs-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="e5fa2-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="e5fa2-195">**Sunucu tarafı şifreleme**: Azure Storage artık sunucu tarafı şifreleme desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="e5fa2-196">Bkz. [Bekleyen Veri için Azure Storage Hizmeti Şifreleme (Önizleme)](storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="e5fa2-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](storage-service-encryption.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5fa2-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e5fa2-197">Next steps</span></span>
<span data-ttu-id="e5fa2-198">Blob storage'nın hello temel bilgileri öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-198">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="e5fa2-199">Microsoft Azure Depolama Gezgini</span><span class="sxs-lookup"><span data-stu-id="e5fa2-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="e5fa2-200">[Microsoft Azure Depolama Gezgini (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="e5fa2-200">[Microsoft Azure Storage Explorer (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="e5fa2-201">Blob depolama örnekleri</span><span class="sxs-lookup"><span data-stu-id="e5fa2-201">Blob storage samples</span></span>
* [<span data-ttu-id="e5fa2-202">.NET’te Azure Blob Depolama Kullanmaya Başlama</span><span class="sxs-lookup"><span data-stu-id="e5fa2-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="e5fa2-203">Blob Storage başvurusu</span><span class="sxs-lookup"><span data-stu-id="e5fa2-203">Blob storage reference</span></span>
* [<span data-ttu-id="e5fa2-204">.NET başvurusu için Depolama İstemci Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="e5fa2-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="e5fa2-205">REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="e5fa2-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="e5fa2-206">Kavramsal kılavuzlar</span><span class="sxs-lookup"><span data-stu-id="e5fa2-206">Conceptual guides</span></span>
* [<span data-ttu-id="e5fa2-207">Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="e5fa2-207">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="e5fa2-208">.NET için Dosya depolamayı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e5fa2-208">Get started with File storage for .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="e5fa2-209">Nasıl toouse Azure blob depolama hello WebJobs SDK ile</span><span class="sxs-lookup"><span data-stu-id="e5fa2-209">How toouse Azure blob storage with hello WebJobs SDK</span></span>](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
