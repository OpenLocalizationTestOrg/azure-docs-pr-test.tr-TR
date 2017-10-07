---
title: "aaaGet, bağlı hizmetler (ASP.NET Core) blob depolama ve Visual Studio ile çalışmaya | Microsoft Docs"
description: "Visual Studio kullanarak bir depolama hesabı oluşturduktan sonra Visual Studio ASP.NET Core projede Azure Blob storage kullanarak tooget nasıl başlatılacağını bağlı Hizmetleri"
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
ms.openlocfilehash: 8eedf331896b21658c7b30a68a4391d8d60cd729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="b6c41-103">Azure Blob ile çalışmaya başlama depolama ve Visual Studio bağlı Hizmetleri (ASP.NET çekirdek)</span><span class="sxs-lookup"><span data-stu-id="b6c41-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="b6c41-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b6c41-104">Overview</span></span>
<span data-ttu-id="b6c41-105">Bu makalede, oluşturduğunuz veya hello Visual Studio bağlı Hizmetleri Ekle iletişim kutusunu kullanarak bir ASP.NET Core projesini bir Azure depolama hesabında başvurulan sonra Visual Studio'da Azure Blob storage kullanarak tooget nasıl başlatılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="b6c41-105">This article describes how tooget started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="b6c41-106">Azure Blob Depolama büyük miktarda gelen herhangi bir yere Merhaba Dünya HTTP veya HTTPS aracılığıyla erişilebilir yapılandırılmamış veriyi depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="b6c41-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="b6c41-107">Tek bir blob herhangi bir boyutta olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6c41-107">A single blob can be any size.</span></span> <span data-ttu-id="b6c41-108">BLOB'ları görüntüleri, ses ve video dosyaları, ham verileri ve belge dosyaları gibi olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6c41-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="b6c41-109">Bu makalede hello Visual Studio kullanarak Azure storage hesabı oluşturduktan sonra tooget blob storage'ı nasıl başlatılacağını açıklar **bağlı Hizmetleri Ekle** ASP.NET Core projesinde iletişim.</span><span class="sxs-lookup"><span data-stu-id="b6c41-109">This article describes how tooget started with blob storage after you create an Azure storage account by using hello Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="b6c41-110">Dosyaları klasörlerde yalnızca dinamik olarak kapsayıcılarında depolama BLOB'ları dinamik.</span><span class="sxs-lookup"><span data-stu-id="b6c41-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="b6c41-111">Bir depolama oluşturduktan sonra hello depolama alanında bir veya daha fazla kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b6c41-111">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="b6c41-112">Örneğin, "Koleksiyon defteri" adlı bir depolama "görüntüleri" toostore resimleri adlı hello storage'da kapsayıcı oluşturma ve ses dosyaları başka bir "ses" toostore çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b6c41-112">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="b6c41-113">Merhaba kapsayıcılara oluşturduktan sonra tek tek blob dosyaları toothem karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6c41-113">After you create hello containers, you can upload individual blob files toothem.</span></span> <span data-ttu-id="b6c41-114">Bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md) program aracılığıyla BLOB'lar düzenleme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="b6c41-114">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="b6c41-115">Kod erişim blob kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="b6c41-115">Access blob containers in code</span></span>
<span data-ttu-id="b6c41-116">zaten mevcut değillerse tooprogrammatically erişim BLOB'lar ASP.NET Core projelerinde öğeleri aşağıdaki tooadd hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6c41-116">tooprogrammatically access blobs in ASP.NET Core projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="b6c41-117">Aşağıdaki kod ad alanı bildirimleri toohello dosyasının üst kısmında tooprogrammatically erişim Azure depolama istediğiniz tüm C# hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b6c41-117">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="b6c41-118">Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="b6c41-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b6c41-119">Kod tooget aşağıdaki hello depolama bağlantı dizesi ve hello Azure hizmet yapılandırma depolama hesabı bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6c41-119">Use hello following code tooget your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="b6c41-120">**Not:** hello hello kod önünde kodu yukarıdaki tüm bölümleri aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6c41-120">**NOTE:** Use all of hello above code in front of hello code in hello following sections.</span></span>
3. <span data-ttu-id="b6c41-121">Kullanım bir **CloudBlobClient** tooget nesne bir **CloudBlobContainer** başvuru tooan var olan bir kapsayıcı depolama hesabınızdaki.</span><span class="sxs-lookup"><span data-stu-id="b6c41-121">Use a **CloudBlobClient** object tooget a **CloudBlobContainer** reference tooan existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="b6c41-122">Kod içinde bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6c41-122">Create a container in code</span></span>
<span data-ttu-id="b6c41-123">Merhaba de kullanabilirsiniz **CloudBlobClient** toocreate depolama hesabınızdaki bir kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="b6c41-123">You can also use hello **CloudBlobClient** toocreate a container in your storage account.</span></span> <span data-ttu-id="b6c41-124">Tek toodo ihtiyacınız olan tooadd bir çağrı çok**CreateIfNotExistsAsync** koddan hello olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="b6c41-124">All you need toodo is tooadd a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="b6c41-125">**Not:** hello çağrıları tooAzure depolama ASP.NET Core gerçekleştirmek API'leri zaman uyumsuz.</span><span class="sxs-lookup"><span data-stu-id="b6c41-125">**NOTE:** hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="b6c41-126">Bkz: [uyumsuz ve bekleme ile zaman uyumsuz programlama](http://msdn.microsoft.com/library/hh191443.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b6c41-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="b6c41-127">Aşağıdaki Hello kodu zaman uyumsuz programlama yöntemleri kullanıldığı varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b6c41-127">hello code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="b6c41-128">toomake hello dosyaları hello kapsayıcı kullanılabilir tooeveryone içinde hello kapsayıcı toobe ortak koddan hello kullanarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6c41-128">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="b6c41-129">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="b6c41-129">Upload a blob into a container</span></span>
<span data-ttu-id="b6c41-130">bir kapsayıcı halinde bir blob dosya tooupload bir kapsayıcı başvurusu alın ve tooget bir blob başvurusu kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6c41-130">tooupload a blob file into a container, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="b6c41-131">Bir blob başvurusu aldıktan sonra herhangi bir veri tooit akışıdır tarafından arama hello yükleyebilirsiniz **UploadFromStreamAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b6c41-131">After you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="b6c41-132">Bu işlem henüz veya mevcut değilse bu raporun üzerine hello blob oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b6c41-132">This operation creates hello blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="b6c41-133">örnekte gösterildiği nasıl aşağıdaki hello tooupload blob bir kapsayıcı halinde ve o hello kapsayıcısı zaten oluşturulduğu varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b6c41-133">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="b6c41-134">Liste hello BLOB'ları bir kapsayıcıda</span><span class="sxs-lookup"><span data-stu-id="b6c41-134">List hello blobs in a container</span></span>
<span data-ttu-id="b6c41-135">toolist hello BLOB'ları bir kapsayıcıda, ilk olarak bir kapsayıcı başvurusu alın.</span><span class="sxs-lookup"><span data-stu-id="b6c41-135">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="b6c41-136">Ardından hello kapsayıcının çağırabilirsiniz **ListBlobsSegmentedAsync** yöntemi tooretrieve hello blobları ve/veya dizinleri içindeki.</span><span class="sxs-lookup"><span data-stu-id="b6c41-136">You can then call hello container's **ListBlobsSegmentedAsync** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="b6c41-137">tooaccess hello zengin özellik ve yöntem **Ilistblobıtem**, tooa atamalısınız **CloudBlockBlob**, **CloudPageBlob**, veya  **CloudBlobDirectory** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="b6c41-137">tooaccess hello rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="b6c41-138">Varsa yazın hello blob bilmiyorsanız, hangi toocast türü onay toodetermine kullanabileceğiniz şekilde.</span><span class="sxs-lookup"><span data-stu-id="b6c41-138">If you don't know hello blob type, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="b6c41-139">koddan hello tooretrieve ve çıkış URI bir kapsayıcıdaki her öğesinin nasıl hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="b6c41-139">hello following code demonstrates how tooretrieve and output hello URI of each item in a container.</span></span>

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

<span data-ttu-id="b6c41-140">Vardır diğer yolları toolist hello bir blob kapsayıcı içeriğini.</span><span class="sxs-lookup"><span data-stu-id="b6c41-140">There are others ways toolist hello contents of a blob container.</span></span> <span data-ttu-id="b6c41-141">Bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b6c41-141">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="b6c41-142">Blob indirme</span><span class="sxs-lookup"><span data-stu-id="b6c41-142">Download a blob</span></span>
<span data-ttu-id="b6c41-143">toodownload bir blob başvurusu toohello blob ilk alın ve hello çağrısı **DownloadToStreamAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b6c41-143">toodownload a blob, first get a reference toohello blob, and then call hello **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="b6c41-144">Merhaba aşağıdaki örnek kullanır hello **DownloadToStreamAsync** sonra yerel bir dosya olarak kaydedin yöntemi tootransfer hello blob içeriği tooa akış nesnesi.</span><span class="sxs-lookup"><span data-stu-id="b6c41-144">hello following example uses hello **DownloadToStreamAsync** method tootransfer hello blob contents tooa stream object that you can then save as a local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="b6c41-145">Dosyaları olarak toosave BLOB'ları diğer yolları vardır.</span><span class="sxs-lookup"><span data-stu-id="b6c41-145">There are other ways toosave blobs as files.</span></span> <span data-ttu-id="b6c41-146">Bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b6c41-146">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="b6c41-147">Blob silme</span><span class="sxs-lookup"><span data-stu-id="b6c41-147">Delete a blob</span></span>
<span data-ttu-id="b6c41-148">toodelete bir blob başvurusu toohello blob ilk alın ve hello çağrısı **DeleteAsync** yöntemini.</span><span class="sxs-lookup"><span data-stu-id="b6c41-148">toodelete a blob, first get a reference toohello blob, and then call hello **DeleteAsync** method on it.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="b6c41-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b6c41-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

