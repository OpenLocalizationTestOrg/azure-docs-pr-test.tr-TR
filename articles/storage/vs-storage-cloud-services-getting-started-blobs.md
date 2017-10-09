---
title: "aaaGet, bağlı hizmetler (bulut Hizmetleri) blob depolama ve Visual Studio ile çalışmaya | Microsoft Docs"
description: "Visual Studio kullanarak tooa depolama hesabı bağlanma Hizmetleri bağlandıktan sonra bir bulut hizmeti projesini Visual Studio'da Azure Blob storage kullanarak tooget nasıl başlatılacağını"
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
ms.openlocfilehash: 62fb7fcff0a90008859ebe23755f13ef0555e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="97dcb-103">Azure Blob Storage ve Visual Studio ile çalışmaya başlama bağlı Hizmetleri (bulut hizmeti projeleri)</span><span class="sxs-lookup"><span data-stu-id="97dcb-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="97dcb-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="97dcb-104">Overview</span></span>
<span data-ttu-id="97dcb-105">Oluşturulan veya hello Visual Studio kullanarak bir Azure Storage hesabı başvurulan sonra tooget Azure Blob Storage ile çalışmaya nasıl bu makalede **bağlı Hizmetleri Ekle** iletişim kutusunda bir Visual Studio bulut Hizmetleri projesi.</span><span class="sxs-lookup"><span data-stu-id="97dcb-105">This article describes how tooget started with Azure Blob Storage after you created or referenced an Azure Storage account by using hello Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="97dcb-106">Nasıl göstereceğiz tooaccess blob kapsayıcıları ve nasıl tooperform ortak görevleri karşıya yükleme, listeleme ve BLOB'ları indirme gibi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97dcb-106">We'll show you how tooaccess and create blob containers, and how tooperform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="97dcb-107">Merhaba örnekleri C'de yazılmış\# ve hello [.NET için Microsoft Azure Storage istemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="97dcb-107">hello samples are written in C\# and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="97dcb-108">Azure Blob Storage, büyük miktarda gelen herhangi bir yere Merhaba Dünya HTTP veya HTTPS aracılığıyla erişilebilir yapılandırılmamış veriyi depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="97dcb-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="97dcb-109">Tek bir blob herhangi bir boyutta olabilir.</span><span class="sxs-lookup"><span data-stu-id="97dcb-109">A single blob can be any size.</span></span> <span data-ttu-id="97dcb-110">BLOB'ları görüntüleri, ses ve video dosyaları, ham verileri ve belge dosyaları gibi olabilir.</span><span class="sxs-lookup"><span data-stu-id="97dcb-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="97dcb-111">Dosyaları klasörlerde yalnızca dinamik olarak kapsayıcılarında depolama BLOB'ları dinamik.</span><span class="sxs-lookup"><span data-stu-id="97dcb-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="97dcb-112">Bir depolama oluşturduktan sonra hello depolama alanında bir veya daha fazla kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="97dcb-112">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="97dcb-113">Örneğin, "Koleksiyon defteri" adlı bir depolama "görüntüleri" toostore resimleri adlı hello storage'da kapsayıcı oluşturma ve ses dosyaları başka bir "ses" toostore çağrılır.</span><span class="sxs-lookup"><span data-stu-id="97dcb-113">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="97dcb-114">Merhaba kapsayıcılara oluşturduktan sonra tek tek blob dosyaları toothem karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97dcb-114">After you create hello containers, you can upload individual blob files toothem.</span></span>

* <span data-ttu-id="97dcb-115">Program aracılığıyla BLOB'lar düzenleme ile ilgili daha fazla bilgi için bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="97dcb-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="97dcb-116">Azure Storage hakkında genel bilgi için bkz: [Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="97dcb-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="97dcb-117">Azure bulut hizmetleri hakkında genel bilgi için bkz: [bulut Hizmetleri belgelerinde](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="97dcb-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="97dcb-118">ASP.NET uygulamalarını programlama hakkında daha fazla bilgi için bkz: [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="97dcb-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="97dcb-119">Kod erişim blob kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="97dcb-119">Access blob containers in code</span></span>
<span data-ttu-id="97dcb-120">tooprogrammatically erişim blobları bulut hizmeti projelerinde zaten mevcut değillerse öğeleri aşağıdaki tooadd hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="97dcb-120">tooprogrammatically access blobs in cloud service projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="97dcb-121">Aşağıdaki kod ad alanı bildirimleri toohello dosyasının üst kısmında tooprogrammatically erişim Azure Storage istediğiniz tüm C# hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="97dcb-121">Add hello following code namespace declarations toohello top of any C# file in which you wish tooprogrammatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="97dcb-122">Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="97dcb-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="97dcb-123">Kod tooget aşağıdaki kullanım hello depolama bağlantı dizesi ve depolama hesabı bilgilerini hello Azure hizmet yapılandırmasından hello.</span><span class="sxs-lookup"><span data-stu-id="97dcb-123">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="97dcb-124">Alma bir **CloudBlobClient** tooreference depolama hesabınızdaki var olan bir kapsayıcı nesne.</span><span class="sxs-lookup"><span data-stu-id="97dcb-124">Get a **CloudBlobClient** object tooreference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="97dcb-125">Alma bir **CloudBlobContainer** tooreference belirli blob kapsayıcı nesne.</span><span class="sxs-lookup"><span data-stu-id="97dcb-125">Get a **CloudBlobContainer** object tooreference a specific blob container.</span></span>
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="97dcb-126">Tüm bölümler aşağıdaki hello gösterilen hello kod önünde hello önceki yordamda gösterilen hello kodunun kullanın.</span><span class="sxs-lookup"><span data-stu-id="97dcb-126">Use all of hello code shown in hello previous procedure in front of hello code shown in hello following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="97dcb-127">Kod içinde bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="97dcb-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="97dcb-128">ASP.NET tooAzure depolama giden çağrıları gerçekleştirdiğinizde bazı API'leri zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="97dcb-128">Some APIs that perform calls out tooAzure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="97dcb-129">Bkz: [uyumsuz ve bekleme ile zaman uyumsuz programlama](http://msdn.microsoft.com/library/hh191443.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="97dcb-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="97dcb-130">Aşağıdaki örneğine hello Hello kodda zaman uyumsuz programlama yöntemleri kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="97dcb-130">hello code in hello following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="97dcb-131">Depolama hesabınızdaki bir kapsayıcı toocreate, tüm yapmanız gereken toodo ekleyin bir çağrı çok**CreateIfNotExistsAsync** koddan hello olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="97dcb-131">toocreate a container in your storage account, all you need toodo is add a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="97dcb-132">toomake hello dosyaları hello kapsayıcı kullanılabilir tooeveryone içinde hello kapsayıcı toobe ortak koddan hello kullanarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97dcb-132">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="97dcb-133">Merhaba Internet üzerinden herkes ortak bir kapsayıcıdaki blobları görebilir ancak değiştirdiğinizde ya da yalnızca hello uygun erişim anahtarı varsa, bunları silin.</span><span class="sxs-lookup"><span data-stu-id="97dcb-133">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="97dcb-134">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="97dcb-134">Upload a blob into a container</span></span>
<span data-ttu-id="97dcb-135">Azure Storage blok blobları ve sayfa bloblarını destekler.</span><span class="sxs-lookup"><span data-stu-id="97dcb-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="97dcb-136">Merhaba çoğu durumda, blok blob türü toouse önerilen hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="97dcb-136">In hello majority of cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="97dcb-137">tooupload dosya tooa blok blob bir kapsayıcı başvurusu alın ve blok blob başvurusu tooget kullanın.</span><span class="sxs-lookup"><span data-stu-id="97dcb-137">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="97dcb-138">Bir blob başvurusu edindiğinizde arama hello tarafından herhangi bir veri tooit akışıdır yükleyebilirsiniz **UploadFromStream** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="97dcb-138">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="97dcb-139">Bu işlem daha önce bulunamadı veya mevcut değilse bu raporun üzerine hello blob oluşturur.</span><span class="sxs-lookup"><span data-stu-id="97dcb-139">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="97dcb-140">örnekte gösterildiği nasıl aşağıdaki hello tooupload blob bir kapsayıcı halinde ve o hello kapsayıcısı zaten oluşturulduğu varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="97dcb-140">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="97dcb-141">Liste hello BLOB'ları bir kapsayıcıda</span><span class="sxs-lookup"><span data-stu-id="97dcb-141">List hello blobs in a container</span></span>
<span data-ttu-id="97dcb-142">toolist hello BLOB'ları bir kapsayıcıda, ilk olarak bir kapsayıcı başvurusu alın.</span><span class="sxs-lookup"><span data-stu-id="97dcb-142">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="97dcb-143">Merhaba kapsayıcının sonra kullanabileceğiniz **ListBlobs** yöntemi tooretrieve hello blobları ve/veya dizinleri içindeki.</span><span class="sxs-lookup"><span data-stu-id="97dcb-143">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="97dcb-144">tooaccess hello zengin özellik ve yöntem **Ilistblobıtem**, tooa atamalısınız **CloudBlockBlob**, **CloudPageBlob**, veya  **CloudBlobDirectory** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="97dcb-144">tooaccess hello rich set of properties and methods for a  returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="97dcb-145">Merhaba türü bilinmiyor, hangi toocast türü onay toodetermine kullanabilirsiniz için.</span><span class="sxs-lookup"><span data-stu-id="97dcb-145">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="97dcb-146">Merhaba aşağıdaki kodu nasıl tooretrieve ve çıktı hello her öğe URI'sini hello gösterir **fotoğraf** kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="97dcb-146">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **photos** container:</span></span>

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

<span data-ttu-id="97dcb-147">Hello önceki kod örneğinde gösterildiği şekilde hello blob hizmeti kapsayıcıları, de dizinleri hello kavramı vardır.</span><span class="sxs-lookup"><span data-stu-id="97dcb-147">As shown in hello previous code sample, hello blob service has hello concept of directories within containers, as well.</span></span> <span data-ttu-id="97dcb-148">Bu, böylelikle daha klasör benzeri bir yapı bloblarınızın düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97dcb-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="97dcb-149">Örneğin, adlandırılmış bir kapsayıcıda blok blobları kümesine aşağıdaki hello göz önünde bulundurun **fotoğraf**:</span><span class="sxs-lookup"><span data-stu-id="97dcb-149">For example, consider hello following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="97dcb-150">Çağırdığınızda **ListBlobs** (olduğu gibi hello önceki örnek) hello kapsayıcısı üzerinde döndürülen hello koleksiyonu içerir **CloudBlobDirectory** ve **CloudBlockBlob** nesneleri Merhaba dizinleri ve blobları hello en üst düzeyinde bulunan temsil eden.</span><span class="sxs-lookup"><span data-stu-id="97dcb-150">When you call **ListBlobs** on hello container (as in hello previous sample), hello collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="97dcb-151">Merhaba sonuçta çıktı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="97dcb-151">Here is hello resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="97dcb-152">İsteğe bağlı olarak, hello ayarlayabilirsiniz **Listblobs** hello parametresini **ListBlobs** yönteme **doğru**.</span><span class="sxs-lookup"><span data-stu-id="97dcb-152">Optionally, you can set hello **UseFlatBlobListing** parameter of of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="97dcb-153">Bu olarak döndürülen her blob sonuçlanır bir **CloudBlockBlob**ne olursa olsun, dizin.</span><span class="sxs-lookup"><span data-stu-id="97dcb-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="97dcb-154">İşte hello çağrısı çok**ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="97dcb-154">Here is hello call too**ListBlobs**:</span></span>

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="97dcb-155">ve hello sonuçları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="97dcb-155">and here are hello results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="97dcb-156">Daha fazla bilgi için bkz: [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="97dcb-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="97dcb-157">Blob’ları indirme</span><span class="sxs-lookup"><span data-stu-id="97dcb-157">Download blobs</span></span>
<span data-ttu-id="97dcb-158">toodownload BLOB'lar, ilk olarak bir blob başvurusu alın ve ardından hello çağırın **DownloadToStream** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="97dcb-158">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="97dcb-159">Merhaba aşağıdaki örnek kullanır hello **DownloadToStream** yöntemi tootransfer hello blob içeriği tooa stream nesnesi tooa yerel dosya daha sonra devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="97dcb-159">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="97dcb-160">Merhaba de kullanabilirsiniz **DownloadToStream** yöntemi toodownload hello içeriği blob olarak bir metin dizesi.</span><span class="sxs-lookup"><span data-stu-id="97dcb-160">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="97dcb-161">Blob’ları silme</span><span class="sxs-lookup"><span data-stu-id="97dcb-161">Delete blobs</span></span>
<span data-ttu-id="97dcb-162">toodelete bir blob önce bir blob başvurusu alın ve ardından arama **silmek** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="97dcb-162">toodelete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="97dcb-163">Blob’ları sayfalarda zaman uyumsuz olarak listeleme</span><span class="sxs-lookup"><span data-stu-id="97dcb-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="97dcb-164">Çok sayıda BLOB listeliyorsanız veya toocontrol hello bir listeleme işlemi ile dönen sonuç sayısını isterseniz sonuç sayfalarında blobları listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97dcb-164">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="97dcb-165">Böylece yürütme tooreturn büyük bir sonuç kümesi beklenirken engellenmeyen Bu örnek nasıl tooreturn sayfalarında zaman uyumsuz olarak sonuçları gösterir.</span><span class="sxs-lookup"><span data-stu-id="97dcb-165">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="97dcb-166">Bu örnek düz bir blob listesi gösterir, ancak ayarı hello tarafından da hiyerarşik bir listeleme gerçekleştirebilirsiniz **Listblobs** hello parametresinin **ListBlobsSegmentedAsync** yöntemi çok **yanlış**.</span><span class="sxs-lookup"><span data-stu-id="97dcb-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello **useFlatBlobListing** parameter of hello **ListBlobsSegmentedAsync** method too**false**.</span></span>

<span data-ttu-id="97dcb-167">Merhaba örnek yöntemi zaman uyumsuz bir yöntem çağırdığı için onu hello ile dönmelidir **zaman uyumsuz** anahtar sözcüğü ve döndürmelidir bir **görev** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="97dcb-167">Because hello sample method calls an asynchronous method, it must be prefaced with hello **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="97dcb-168">Merhaba await hello için belirtilen anahtar sözcüğü **ListBlobsSegmentedAsync** yöntemi hello listeleme görevi tamamlanana kadar hello örnek yönteminin yürütülmesi askıya alır.</span><span class="sxs-lookup"><span data-stu-id="97dcb-168">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
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

## <a name="next-steps"></a><span data-ttu-id="97dcb-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="97dcb-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

