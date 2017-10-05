---
title: "BLOB ile çalışmaya başlama depolama ve Visual Studio bağlı Hizmetleri (ASP.NET Core) | Microsoft Docs"
description: "Visual Studio kullanarak bir depolama hesabı oluşturduktan sonra Azure Blob Depolama Visual Studio ASP.NET Core projede kullanmaya başlamak nasıl bağlı Hizmetleri"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 2e8060b44c395ad7c24e7778c0ef65148a3a45de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="7d212-103">Azure Blob ile çalışmaya başlama depolama ve Visual Studio bağlı Hizmetleri (ASP.NET çekirdek)</span><span class="sxs-lookup"><span data-stu-id="7d212-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="7d212-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7d212-104">Overview</span></span>
<span data-ttu-id="7d212-105">Bu makalede, oluşturduğunuz veya Visual Studio bağlı Hizmetleri Ekle iletişim kutusunu kullanarak bir ASP.NET Core projesini bir Azure depolama hesabında başvurulan sonra Visual Studio'da Azure Blob storage ile çalışmaya başlamak açıklar.</span><span class="sxs-lookup"><span data-stu-id="7d212-105">This article describes how to get started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="7d212-106">Azure Blob Depolama büyük miktarda gelen yerden HTTP veya HTTPS aracılığıyla erişilebilir yapılandırılmamış veriyi depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="7d212-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="7d212-107">Tek bir blob herhangi bir boyutta olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d212-107">A single blob can be any size.</span></span> <span data-ttu-id="7d212-108">BLOB'ları görüntüleri, ses ve video dosyaları, ham verileri ve belge dosyaları gibi olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d212-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="7d212-109">Bu makalede, Visual Studio kullanarak Azure storage hesabı oluşturduktan sonra blob storage'ı kullanmaya başlamak açıklar **bağlı Hizmetleri Ekle** ASP.NET Core projesinde iletişim.</span><span class="sxs-lookup"><span data-stu-id="7d212-109">This article describes how to get started with blob storage after you create an Azure storage account by using the Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="7d212-110">Dosyaları klasörlerde yalnızca dinamik olarak kapsayıcılarında depolama BLOB'ları dinamik.</span><span class="sxs-lookup"><span data-stu-id="7d212-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="7d212-111">Bir depolama oluşturduktan sonra depolama alanında bir veya daha fazla kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7d212-111">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="7d212-112">Örneğin, "Koleksiyon defteri" adlı bir depolama resimleri depolamak için "görüntüleri" adlı depolama kapsayıcıları oluşturabilirsiniz ve başka bir "ses dosyalarını depolamak için ses" olarak adlandırılan.</span><span class="sxs-lookup"><span data-stu-id="7d212-112">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="7d212-113">Kapsayıcılar oluşturduktan sonra bunları tek tek blob dosyaları karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="7d212-113">After you create the containers, you can upload individual blob files to them.</span></span> <span data-ttu-id="7d212-114">Bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md) program aracılığıyla BLOB'lar düzenleme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="7d212-114">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="7d212-115">Kod erişim blob kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="7d212-115">Access blob containers in code</span></span>
<span data-ttu-id="7d212-116">Zaten mevcut değillerse ASP.NET Core projelerinde BLOB'lar programlı olarak erişmek için aşağıdaki öğeleri eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d212-116">To programmatically access blobs in ASP.NET Core projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="7d212-117">Aşağıdaki kod ad alanı bildirimleri Azure depolama programlı olarak erişmek istediğiniz tüm C# dosyasının üstüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7d212-117">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="7d212-118">Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="7d212-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="7d212-119">Azure hizmet yapılandırmasından depolama bağlantı dizesi ve depolama hesabı bilgilerini almak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d212-119">Use the following code to get your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="7d212-120">**Not:** tüm kod önünde Yukarıdaki kod aşağıdaki bölümleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d212-120">**NOTE:** Use all of the above code in front of the code in the following sections.</span></span>
3. <span data-ttu-id="7d212-121">Kullanım bir **CloudBlobClient** nesnesi bir **CloudBlobContainer** depolama hesabınızdaki var olan bir kapsayıcı başvurusu.</span><span class="sxs-lookup"><span data-stu-id="7d212-121">Use a **CloudBlobClient** object to get a **CloudBlobContainer** reference to an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="7d212-122">Kod içinde bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d212-122">Create a container in code</span></span>
<span data-ttu-id="7d212-123">Aynı zamanda **CloudBlobClient** depolama hesabınızdaki bir kapsayıcı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="7d212-123">You can also use the **CloudBlobClient** to create a container in your storage account.</span></span> <span data-ttu-id="7d212-124">Tüm yapmanız gereken bir çağrı ekleyin etmektir **CreateIfNotExistsAsync** aşağıdaki kodu olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="7d212-124">All you need to do is to add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference to a container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="7d212-125">**Not:** ASP.NET Core Azure depolama çağrıları gerçekleştirdiğinizde API'leri zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="7d212-125">**NOTE:** The APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="7d212-126">Bkz: [uyumsuz ve bekleme ile zaman uyumsuz programlama](http://msdn.microsoft.com/library/hh191443.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="7d212-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="7d212-127">Aşağıdaki kodu, zaman uyumsuz programlama yöntemleri kullanıldığı varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7d212-127">The code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="7d212-128">Kapsayıcı içindeki dosyaların herkese kullanılabilmesi için genel olarak aşağıdaki kodu kullanarak kapsayıcıyı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d212-128">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="7d212-129">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="7d212-129">Upload a blob into a container</span></span>
<span data-ttu-id="7d212-130">Bir kapsayıcıya bir blob dosya karşıya yükleme için bir kapsayıcı başvurusu alın ve bir blob başvurusu almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d212-130">To upload a blob file into a container, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="7d212-131">Bir blob başvurusu aldıktan sonra veri kendisine çağırarak karşıya yükleyebilirsiniz **UploadFromStreamAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7d212-131">After you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="7d212-132">Bu işlem henüz veya mevcut değilse bu raporun üzerine blob oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7d212-132">This operation creates the blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="7d212-133">Aşağıdaki örnek kapsayıcının önceden oluşturulduğunu varsayarak bir blobun bir kapsayıcıya nasıl yükleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d212-133">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Get a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with the contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="7d212-134">Blob’ları bir kapsayıcıda listeleme</span><span class="sxs-lookup"><span data-stu-id="7d212-134">List the blobs in a container</span></span>
<span data-ttu-id="7d212-135">Blob’ları bir kapsayıcıda listelemek için ilk olarak bir kapsayıcı başvurusu edinin.</span><span class="sxs-lookup"><span data-stu-id="7d212-135">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="7d212-136">Ardından kapsayıcının çağırabilirsiniz **ListBlobsSegmentedAsync** blobları ve/veya dizinleri içindeki alma yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7d212-136">You can then call the container's **ListBlobsSegmentedAsync** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="7d212-137">Dönen **IListBlobItem** için zengin özellik ve yöntem kümesine erişmek için **CloudBlockBlob**, **CloudPageBlob** veya **CloudBlobDirectory** nesnesine yayınlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d212-137">To access the rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="7d212-138">Blob türü bilmiyorsanız, hangisine yayınlayacağınızı belirlemek için bir tür denetimi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d212-138">If you don't know the blob type, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="7d212-139">Aşağıdaki kod, almak ve her bir kapsayıcı öğe URI'sini çıkış gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7d212-139">The following code demonstrates how to retrieve and output the URI of each item in a container.</span></span>

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
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
    } while (token != null);

<span data-ttu-id="7d212-140">Diğer bir blob kapsayıcı içeriğini listele yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="7d212-140">There are others ways to list the contents of a blob container.</span></span> <span data-ttu-id="7d212-141">Bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="7d212-141">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="7d212-142">Blob indirme</span><span class="sxs-lookup"><span data-stu-id="7d212-142">Download a blob</span></span>
<span data-ttu-id="7d212-143">Bir blob indirmek için ilk blob başvurusu alın ve ardından arama **DownloadToStreamAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7d212-143">To download a blob, first get a reference to the blob, and then call the **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="7d212-144">Aşağıdaki örnek kullanır **DownloadToStreamAsync** blob içeriklerini sonra yerel bir dosya olarak kaydedin bir akış nesnesine aktarmak için yöntem.</span><span class="sxs-lookup"><span data-stu-id="7d212-144">The following example uses the **DownloadToStreamAsync** method to transfer the blob contents to a stream object that you can then save as a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save the blob contents to a file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="7d212-145">Blobları dosya olarak kaydetmek için başka yolları vardır.</span><span class="sxs-lookup"><span data-stu-id="7d212-145">There are other ways to save blobs as files.</span></span> <span data-ttu-id="7d212-146">Bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="7d212-146">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="7d212-147">Blob silme</span><span class="sxs-lookup"><span data-stu-id="7d212-147">Delete a blob</span></span>
<span data-ttu-id="7d212-148">Bir blobu silmek için önce bir blob başvurusu alın ve ardından çağırın **DeleteAsync** yöntemini.</span><span class="sxs-lookup"><span data-stu-id="7d212-148">To delete a blob, first get a reference to the blob, and then call the **DeleteAsync** method on it.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="7d212-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7d212-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

