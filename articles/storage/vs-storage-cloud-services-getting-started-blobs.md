---
title: "BLOB ile çalışmaya başlama depolama ve Visual Studio bağlı Hizmetleri (bulut Hizmetleri) | Microsoft Docs"
description: "Visual Studio kullanarak bir depolama hesabına bağlanma Hizmetleri bağlandıktan sonra bir bulut hizmeti projesini Visual Studio'da Azure Blob storage kullanarak nereden başlayacaksınız"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: e154c81ef3765a3c006b3c27a979be881f14d0ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="cfe7e-103">Azure Blob Storage ve Visual Studio ile çalışmaya başlama bağlı Hizmetleri (bulut hizmeti projeleri)</span><span class="sxs-lookup"><span data-stu-id="cfe7e-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="cfe7e-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cfe7e-104">Overview</span></span>
<span data-ttu-id="cfe7e-105">Bu makalede oluşturulan ya da Visual Studio kullanarak bir Azure Storage hesabı başvurulan sonra Azure Blob Storage'ı kullanmaya başlamak nasıl **bağlı Hizmetleri Ekle** iletişim kutusunda bir Visual Studio bulut Hizmetleri projesi.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-105">This article describes how to get started with Azure Blob Storage after you created or referenced an Azure Storage account by using the Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="cfe7e-106">Erişme ve blob kapsayıcıları oluşturma ve karşıya yükleme, listeleme ve BLOB'ları indirme gibi genel görevleri gerçekleştirmek nasıl göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-106">We'll show you how to access and create blob containers, and how to perform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="cfe7e-107">Örnekler C yazılır\# ve [.NET için Microsoft Azure Storage istemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfe7e-107">The samples are written in C\# and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="cfe7e-108">Azure Blob Storage, büyük miktarlarda herhangi bir yere HTTP veya HTTPS aracılığıyla erişilebilir yapılandırılmamış verileri depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="cfe7e-109">Tek bir blob herhangi bir boyutta olabilir.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-109">A single blob can be any size.</span></span> <span data-ttu-id="cfe7e-110">BLOB'ları görüntüleri, ses ve video dosyaları, ham verileri ve belge dosyaları gibi olabilir.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="cfe7e-111">Dosyaları klasörlerde yalnızca dinamik olarak kapsayıcılarında depolama BLOB'ları dinamik.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="cfe7e-112">Bir depolama oluşturduktan sonra depolama alanında bir veya daha fazla kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-112">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="cfe7e-113">Örneğin, "Koleksiyon defteri" adlı bir depolama resimleri depolamak için "görüntüleri" adlı depolama kapsayıcıları oluşturabilirsiniz ve başka bir "ses dosyalarını depolamak için ses" olarak adlandırılan.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-113">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="cfe7e-114">Kapsayıcılar oluşturduktan sonra bunları tek tek blob dosyaları karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-114">After you create the containers, you can upload individual blob files to them.</span></span>

* <span data-ttu-id="cfe7e-115">Program aracılığıyla BLOB'lar düzenleme ile ilgili daha fazla bilgi için bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="cfe7e-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="cfe7e-116">Azure Storage hakkında genel bilgi için bkz: [Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="cfe7e-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="cfe7e-117">Azure bulut hizmetleri hakkında genel bilgi için bkz: [bulut Hizmetleri belgelerinde](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="cfe7e-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="cfe7e-118">ASP.NET uygulamalarını programlama hakkında daha fazla bilgi için bkz: [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="cfe7e-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="cfe7e-119">Kod erişim blob kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="cfe7e-119">Access blob containers in code</span></span>
<span data-ttu-id="cfe7e-120">Zaten mevcut değilse bulut hizmeti projelerinde BLOB'lar programlı olarak erişmek için aşağıdaki öğeleri eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-120">To programmatically access blobs in cloud service projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="cfe7e-121">Aşağıdaki kod ad alanı bildirimleri, Azure Storage programlı olarak erişmek istediğiniz tüm C# dosyasının üstüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-121">Add the following code namespace declarations to the top of any C# file in which you wish to programmatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="cfe7e-122">Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="cfe7e-123">Almak için aşağıdaki kodu kullanın depolama bağlantı dizesini ve Azure hizmet yapılandırma depolama hesabı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-123">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="cfe7e-124">Alma bir **CloudBlobClient** depolama hesabınızdaki var olan bir kapsayıcı başvurmak için.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-124">Get a **CloudBlobClient** object to reference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="cfe7e-125">Alma bir **CloudBlobContainer** belirli blob kapsayıcısı başvurmak için.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-125">Get a **CloudBlobContainer** object to reference a specific blob container.</span></span>
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="cfe7e-126">Aşağıdaki bölümlerde gösterilen kodu önüne önceki yordamda gösterilen tüm kodları kullanın.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-126">Use all of the code shown in the previous procedure in front of the code shown in the following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="cfe7e-127">Kod içinde bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cfe7e-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="cfe7e-128">Azure Storage giden çağrıları ASP.NET gerçekleştirmek bazı API'leri zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-128">Some APIs that perform calls out to Azure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="cfe7e-129">Bkz: [uyumsuz ve bekleme ile zaman uyumsuz programlama](http://msdn.microsoft.com/library/hh191443.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="cfe7e-130">Aşağıdaki örnek kodda, zaman uyumsuz programlama yöntemleri kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-130">The code in the following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="cfe7e-131">Depolama hesabınızdaki bir kapsayıcı oluşturmak için yapmanız gereken tek şey bir çağrı ekleyin **CreateIfNotExistsAsync** aşağıdaki kodu olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="cfe7e-131">To create a container in your storage account, all you need to do is add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="cfe7e-132">Kapsayıcı içindeki dosyaların herkese kullanılabilmesi için genel olarak aşağıdaki kodu kullanarak kapsayıcıyı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-132">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="cfe7e-133">Internet üzerinden herkes ortak bir kapsayıcıdaki blobları görebilir ancak değiştirdiğinizde ya da yalnızca uygun erişim anahtarı varsa, bunları silin.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-133">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="cfe7e-134">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="cfe7e-134">Upload a blob into a container</span></span>
<span data-ttu-id="cfe7e-135">Azure Storage blok blobları ve sayfa bloblarını destekler.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="cfe7e-136">Çoğu durumda kullanılması önerilen blob türü blok blobudur.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-136">In the majority of cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="cfe7e-137">Bir dosyayı bir blok blobuna yüklemek için bir kapsayıcı başvurusu alın ve blok blob başvurusu almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-137">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="cfe7e-138">Bir blob başvurusu edindiğinizde **UploadFromStream** yöntemini çağırarak istediğiniz veri akışını yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-138">Once you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStream** method.</span></span> <span data-ttu-id="cfe7e-139">Bu işlemle, eğer önceden oluşturulmadıysa bir blob oluşturulacaktır, aksi takdirde üzerine yazılacaktır.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-139">This operation creates the blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="cfe7e-140">Aşağıdaki örnek kapsayıcının önceden oluşturulduğunu varsayarak bir blobun bir kapsayıcıya nasıl yükleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-140">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Retrieve a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="cfe7e-141">Blob’ları bir kapsayıcıda listeleme</span><span class="sxs-lookup"><span data-stu-id="cfe7e-141">List the blobs in a container</span></span>
<span data-ttu-id="cfe7e-142">Blob’ları bir kapsayıcıda listelemek için ilk olarak bir kapsayıcı başvurusu edinin.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-142">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="cfe7e-143">Ardından içindeki blobları ve/veya dizinleri almak için kapsayıcının **ListBlobs** yöntemini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-143">You can then use the container's **ListBlobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="cfe7e-144">Zengin özellik ve yöntem erişmek için **Ilistblobıtem**, kendisine atamalısınız bir **CloudBlockBlob**, **CloudPageBlob**, veya **CloudBlobDirectory** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-144">To access the rich set of properties and methods for a  returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="cfe7e-145">Tür bilinmiyorsa, hangisine yayınlayacağınızı belirlemek için bir tür denetimi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-145">If the type is unknown, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="cfe7e-146">Aşağıdaki kod, **resimler** kapsayıcısındaki her nesnenin URI’sinin nasıl alınacağını ve çıkacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="cfe7e-146">The following code demonstrates how to retrieve and output the URI of each item in the **photos** container:</span></span>

    // Loop over items within the container and output the length and URI.
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

<span data-ttu-id="cfe7e-147">Önceki kod örneğinde gösterildiği gibi blob hizmetinde kapsayıcıları, de dizinleri kavramı vardır.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-147">As shown in the previous code sample, the blob service has the concept of directories within containers, as well.</span></span> <span data-ttu-id="cfe7e-148">Bu, böylelikle daha klasör benzeri bir yapı bloblarınızın düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="cfe7e-149">Örneğin bir kapsayıcıda yer alan ve **resimler** olarak adlandırılan aşağıdaki blok blobları kümesine göz atın:</span><span class="sxs-lookup"><span data-stu-id="cfe7e-149">For example, consider the following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="cfe7e-150">Çağırdığınızda **ListBlobs** (olduğu gibi önceki örnek) kapsayıcısı üzerinde döndürülen koleksiyonu içerir **CloudBlobDirectory** ve **CloudBlockBlob** dizinleri ve blobları en üst düzeyinde bulunan temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-150">When you call **ListBlobs** on the container (as in the previous sample), the collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="cfe7e-151">Sonuçta çıktı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="cfe7e-151">Here is the resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="cfe7e-152">İsteğe bağlı olarak **ListBlobs** yönteminin **UseFlatBlobListing** parametresini **true** olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-152">Optionally, you can set the **UseFlatBlobListing** parameter of of the **ListBlobs** method to **true**.</span></span> <span data-ttu-id="cfe7e-153">Bu olarak döndürülen her blob sonuçlanır bir **CloudBlockBlob**ne olursa olsun, dizin.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="cfe7e-154">İşte çağrısı **ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="cfe7e-154">Here is the call to **ListBlobs**:</span></span>

    // Loop over items within the container and output the length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="cfe7e-155">ve sonuçları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cfe7e-155">and here are the results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="cfe7e-156">Daha fazla bilgi için bkz: [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfe7e-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="cfe7e-157">Blob’ları indirme</span><span class="sxs-lookup"><span data-stu-id="cfe7e-157">Download blobs</span></span>
<span data-ttu-id="cfe7e-158">Blob’ları indirmek için ilk olarak bir blob başvurusu alın ve ardından **DownloadToStream** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-158">To download blobs, first retrieve a blob reference and then call the **DownloadToStream** method.</span></span> <span data-ttu-id="cfe7e-159">Aşağıdaki örnek, blob içeriklerini bir akış nesnesine aktarmak ve ardından yerel bir dosyaya kalıcı olarak almak için **DownloadToStream** yöntemini kullanır:</span><span class="sxs-lookup"><span data-stu-id="cfe7e-159">The following example uses the **DownloadToStream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents to a file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="cfe7e-160">Bunun yanında bir blobun içeriklerini metin dizesi olarak indirmek için **DownloadToStream** yöntemini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-160">You can also use the **DownloadToStream** method to download the contents of a blob as a text string.</span></span>

    // Get a reference to a blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="cfe7e-161">Blob’ları silme</span><span class="sxs-lookup"><span data-stu-id="cfe7e-161">Delete blobs</span></span>
<span data-ttu-id="cfe7e-162">Bir blobu silmek için önce bir blob başvurusu alın ve ardından çağıran **silmek** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-162">To delete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="cfe7e-163">Blob’ları sayfalarda zaman uyumsuz olarak listeleme</span><span class="sxs-lookup"><span data-stu-id="cfe7e-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="cfe7e-164">Çok sayıda blob listeliyorsanız veya bir listeleme işlemi ile dönen sonuç sayısını denetlemek isterseniz sonuç sayfalarında blobları listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-164">If you are listing a large number of blobs, or you want to control the number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="cfe7e-165">Bu örnek, geniş bir sonuç kümesinin dönmesini beklerken çalıştırmanın engellenmemesi için sayfalardaki sonuçların zaman uyumsuz olarak nasıl döneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-165">This example shows how to return results in pages asynchronously, so that execution is not blocked while waiting to return a large set of results.</span></span>

<span data-ttu-id="cfe7e-166">Bu örnek düz bir blob listesi gösterir, ancak **ListBlobsSegmentedAsync** metodunun **useFlatBlobListing** parametresini **false** olarak ayarlayarak hiyerarşik bir listeleme gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting the **useFlatBlobListing** parameter of the **ListBlobsSegmentedAsync** method to **false**.</span></span>

<span data-ttu-id="cfe7e-167">Örnek metot, zaman uyumsuz bir metot çağırdığı için **async** anahtar sözcüğüyle başlamalı ve bir **Görev** nesnesi döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-167">Because the sample method calls an asynchronous method, it must be prefaced with the **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="cfe7e-168">Belirtilen **ListBlobsSegmentedAsync** yöntemi için belirlenen bekleme anahtar kelimesi, listeleme görevi tamamlanana kadar örnek yöntemin çalıştırılmasını askıya alır.</span><span class="sxs-lookup"><span data-stu-id="cfe7e-168">The await keyword specified for the **ListBlobsSegmentedAsync** method suspends execution of the sample method until the listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs to the console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
        // When the continuation token is null, the last page has been returned and execution can exit the loop.
        do
        {
            // This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
            // or by calling a different overload.
            resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
            if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
            foreach (var blobItem in resultSegment.Results)
            {
                Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
            }
            Console.WriteLine();

            //Get the continuation token.
            continuationToken = resultSegment.ContinuationToken;
        }
        while (continuationToken != null);
    }

## <a name="next-steps"></a><span data-ttu-id="cfe7e-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cfe7e-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

