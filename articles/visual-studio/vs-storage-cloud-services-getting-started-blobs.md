---
title: "aaaGet, bağlı hizmetler (bulut Hizmetleri) blob depolama ve Visual Studio ile çalışmaya | Microsoft Docs"
description: "Visual Studio kullanarak tooa depolama hesabı bağlanma Hizmetleri bağlandıktan sonra bir bulut hizmeti projesini Visual Studio'da Azure Blob storage kullanarak tooget nasıl başlatılacağını"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 158197a9d49bc4f26841d689405529192c52f529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Azure Blob Storage ve Visual Studio ile çalışmaya başlama bağlı Hizmetleri (bulut hizmeti projeleri)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Genel Bakış
Oluşturulan veya hello Visual Studio kullanarak bir Azure Storage hesabı başvurulan sonra tooget Azure Blob Storage ile çalışmaya nasıl bu makalede **bağlı Hizmetleri Ekle** iletişim kutusunda bir Visual Studio bulut Hizmetleri projesi. Nasıl göstereceğiz tooaccess blob kapsayıcıları ve nasıl tooperform ortak görevleri karşıya yükleme, listeleme ve BLOB'ları indirme gibi oluşturabilirsiniz. Merhaba örnekleri C'de yazılmış\# ve hello [.NET için Microsoft Azure Storage istemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Azure Blob Storage, büyük miktarda gelen herhangi bir yere Merhaba Dünya HTTP veya HTTPS aracılığıyla erişilebilir yapılandırılmamış veriyi depolamak için bir hizmettir. Tek bir blob herhangi bir boyutta olabilir. BLOB'ları görüntüleri, ses ve video dosyaları, ham verileri ve belge dosyaları gibi olabilir.

Dosyaları klasörlerde yalnızca dinamik olarak kapsayıcılarında depolama BLOB'ları dinamik. Bir depolama oluşturduktan sonra hello depolama alanında bir veya daha fazla kapsayıcı oluşturun. Örneğin, "Koleksiyon defteri" adlı bir depolama "görüntüleri" toostore resimleri adlı hello storage'da kapsayıcı oluşturma ve ses dosyaları başka bir "ses" toostore çağrılır. Merhaba kapsayıcılara oluşturduktan sonra tek tek blob dosyaları toothem karşıya yükleyebilirsiniz.

* Program aracılığıyla BLOB'lar düzenleme ile ilgili daha fazla bilgi için bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).
* Azure Storage hakkında genel bilgi için bkz: [Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/).
* Azure bulut hizmetleri hakkında genel bilgi için bkz: [bulut Hizmetleri belgelerinde](https://azure.microsoft.com/documentation/services/cloud-services/).
* ASP.NET uygulamalarını programlama hakkında daha fazla bilgi için bkz: [ASP.NET](http://www.asp.net).

## <a name="access-blob-containers-in-code"></a>Kod erişim blob kapsayıcıları
tooprogrammatically erişim blobları bulut hizmeti projelerinde zaten mevcut değillerse öğeleri aşağıdaki tooadd hello gerekir.

1. Aşağıdaki kod ad alanı bildirimleri toohello dosyasının üst kısmında tooprogrammatically erişim Azure Storage istediğiniz tüm C# hello ekleyin.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kod tooget aşağıdaki kullanım hello depolama bağlantı dizesi ve depolama hesabı bilgilerini hello Azure hizmet yapılandırmasından hello.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. Alma bir **CloudBlobClient** tooreference depolama hesabınızdaki var olan bir kapsayıcı nesne.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. Alma bir **CloudBlobContainer** tooreference belirli blob kapsayıcı nesne.
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> Tüm bölümler aşağıdaki hello gösterilen hello kod önünde hello önceki yordamda gösterilen hello kodunun kullanın.
> 
> 

## <a name="create-a-container-in-code"></a>Kod içinde bir kapsayıcı oluşturma
> [!NOTE]
> ASP.NET tooAzure depolama giden çağrıları gerçekleştirdiğinizde bazı API'leri zaman uyumsuzdur. Bkz: [uyumsuz ve bekleme ile zaman uyumsuz programlama](http://msdn.microsoft.com/library/hh191443.aspx) daha fazla bilgi için. Aşağıdaki örneğine hello Hello kodda zaman uyumsuz programlama yöntemleri kullandığınızı varsayar.
> 
> 

Depolama hesabınızdaki bir kapsayıcı toocreate, tüm yapmanız gereken toodo ekleyin bir çağrı çok**CreateIfNotExistsAsync** koddan hello olduğu gibi:

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


toomake hello dosyaları hello kapsayıcı kullanılabilir tooeveryone içinde hello kapsayıcı toobe ortak koddan hello kullanarak ayarlayabilirsiniz.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


Merhaba Internet üzerinden herkes ortak bir kapsayıcıdaki blobları görebilir ancak değiştirdiğinizde ya da yalnızca hello uygun erişim anahtarı varsa, bunları silin.

## <a name="upload-a-blob-into-a-container"></a>Bir kapsayıcıya bir blob yükleme
Azure Storage blok blobları ve sayfa bloblarını destekler. Merhaba çoğu durumda, blok blob türü toouse önerilen hello ' dir.

tooupload dosya tooa blok blob bir kapsayıcı başvurusu alın ve blok blob başvurusu tooget kullanın. Bir blob başvurusu edindiğinizde arama hello tarafından herhangi bir veri tooit akışıdır yükleyebilirsiniz **UploadFromStream** yöntemi. Bu işlem daha önce bulunamadı veya mevcut değilse bu raporun üzerine hello blob oluşturur. örnekte gösterildiği nasıl aşağıdaki hello tooupload blob bir kapsayıcı halinde ve o hello kapsayıcısı zaten oluşturulduğu varsayılmaktadır.

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Liste hello BLOB'ları bir kapsayıcıda
toolist hello BLOB'ları bir kapsayıcıda, ilk olarak bir kapsayıcı başvurusu alın. Merhaba kapsayıcının sonra kullanabileceğiniz **ListBlobs** yöntemi tooretrieve hello blobları ve/veya dizinleri içindeki. tooaccess hello zengin özellik ve yöntem **Ilistblobıtem**, tooa atamalısınız **CloudBlockBlob**, **CloudPageBlob**, veya  **CloudBlobDirectory** nesnesi. Merhaba türü bilinmiyor, hangi toocast türü onay toodetermine kullanabilirsiniz için. Merhaba aşağıdaki kodu nasıl tooretrieve ve çıktı hello her öğe URI'sini hello gösterir **fotoğraf** kapsayıcı:

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

Hello önceki kod örneğinde gösterildiği şekilde hello blob hizmeti kapsayıcıları, de dizinleri hello kavramı vardır. Bu, böylelikle daha klasör benzeri bir yapı bloblarınızın düzenleyebilirsiniz. Örneğin, adlandırılmış bir kapsayıcıda blok blobları kümesine aşağıdaki hello göz önünde bulundurun **fotoğraf**:

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

Çağırdığınızda **ListBlobs** (olduğu gibi hello önceki örnek) hello kapsayıcısı üzerinde döndürülen hello koleksiyonu içerir **CloudBlobDirectory** ve **CloudBlockBlob** nesneleri Merhaba dizinleri ve blobları hello en üst düzeyinde bulunan temsil eden. Merhaba sonuçta çıktı şöyledir:

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


İsteğe bağlı olarak, hello ayarlayabilirsiniz **Listblobs** hello parametresini **ListBlobs** yönteme **doğru**. Bu olarak döndürülen her blob sonuçlanır bir **CloudBlockBlob**ne olursa olsun, dizin. İşte hello çağrısı çok**ListBlobs**:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

ve hello sonuçları şunlardır:

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

Daha fazla bilgi için bkz: [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).

## <a name="download-blobs"></a>Blob’ları indirme
toodownload BLOB'lar, ilk olarak bir blob başvurusu alın ve ardından hello çağırın **DownloadToStream** yöntemi. Merhaba aşağıdaki örnek kullanır hello **DownloadToStream** yöntemi tootransfer hello blob içeriği tooa stream nesnesi tooa yerel dosya daha sonra devam edebilir.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

Merhaba de kullanabilirsiniz **DownloadToStream** yöntemi toodownload hello içeriği blob olarak bir metin dizesi.

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a>Blob’ları silme
toodelete bir blob önce bir blob başvurusu alın ve ardından arama **silmek** yöntemi.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a>Blob’ları sayfalarda zaman uyumsuz olarak listeleme
Çok sayıda BLOB listeliyorsanız veya toocontrol hello bir listeleme işlemi ile dönen sonuç sayısını isterseniz sonuç sayfalarında blobları listeleyebilirsiniz. Böylece yürütme tooreturn büyük bir sonuç kümesi beklenirken engellenmeyen Bu örnek nasıl tooreturn sayfalarında zaman uyumsuz olarak sonuçları gösterir.

Bu örnek düz bir blob listesi gösterir, ancak ayarı hello tarafından da hiyerarşik bir listeleme gerçekleştirebilirsiniz **Listblobs** hello parametresinin **ListBlobsSegmentedAsync** yöntemi çok **yanlış**.

Merhaba örnek yöntemi zaman uyumsuz bir yöntem çağırdığı için onu hello ile dönmelidir **zaman uyumsuz** anahtar sözcüğü ve döndürmelidir bir **görev** nesnesi. Merhaba await hello için belirtilen anahtar sözcüğü **ListBlobsSegmentedAsync** yöntemi hello listeleme görevi tamamlanana kadar hello örnek yönteminin yürütülmesi askıya alır.

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

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

