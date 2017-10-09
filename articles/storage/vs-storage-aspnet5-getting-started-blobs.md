---
title: "aaaGet, bağlı hizmetler (ASP.NET Core) blob depolama ve Visual Studio ile çalışmaya | Microsoft Docs"
description: "Visual Studio kullanarak bir depolama hesabı oluşturduktan sonra Visual Studio ASP.NET Core projede Azure Blob storage kullanarak tooget nasıl başlatılacağını bağlı Hizmetleri"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: a4c31c08c38d99eb9c66fe2af72ca42fa3804688
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a>Azure Blob ile çalışmaya başlama depolama ve Visual Studio bağlı Hizmetleri (ASP.NET çekirdek)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Genel Bakış
Bu makalede, oluşturduğunuz veya hello Visual Studio bağlı Hizmetleri Ekle iletişim kutusunu kullanarak bir ASP.NET Core projesini bir Azure depolama hesabında başvurulan sonra Visual Studio'da Azure Blob storage kullanarak tooget nasıl başlatılacağını açıklar.

Azure Blob Depolama büyük miktarda gelen herhangi bir yere Merhaba Dünya HTTP veya HTTPS aracılığıyla erişilebilir yapılandırılmamış veriyi depolamak için bir hizmettir. Tek bir blob herhangi bir boyutta olabilir. BLOB'ları görüntüleri, ses ve video dosyaları, ham verileri ve belge dosyaları gibi olabilir. Bu makalede hello Visual Studio kullanarak Azure storage hesabı oluşturduktan sonra tooget blob storage'ı nasıl başlatılacağını açıklar **bağlı Hizmetleri Ekle** ASP.NET Core projesinde iletişim.

Dosyaları klasörlerde yalnızca dinamik olarak kapsayıcılarında depolama BLOB'ları dinamik. Bir depolama oluşturduktan sonra hello depolama alanında bir veya daha fazla kapsayıcı oluşturun. Örneğin, "Koleksiyon defteri" adlı bir depolama "görüntüleri" toostore resimleri adlı hello storage'da kapsayıcı oluşturma ve ses dosyaları başka bir "ses" toostore çağrılır. Merhaba kapsayıcılara oluşturduktan sonra tek tek blob dosyaları toothem karşıya yükleyebilirsiniz. Bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](storage-dotnet-how-to-use-blobs.md) program aracılığıyla BLOB'lar düzenleme hakkında daha fazla bilgi.

## <a name="access-blob-containers-in-code"></a>Kod erişim blob kapsayıcıları
zaten mevcut değillerse tooprogrammatically erişim BLOB'lar ASP.NET Core projelerinde öğeleri aşağıdaki tooadd hello gerekir.

1. Aşağıdaki kod ad alanı bildirimleri toohello dosyasının üst kısmında tooprogrammatically erişim Azure depolama istediğiniz tüm C# hello ekleyin.
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kod tooget aşağıdaki hello depolama bağlantı dizesi ve hello Azure hizmet yapılandırma depolama hesabı bilgileri kullanın.
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    **Not:** hello hello kod önünde kodu yukarıdaki tüm bölümleri aşağıdaki hello kullanın.
3. Kullanım bir **CloudBlobClient** tooget nesne bir **CloudBlobContainer** başvuru tooan var olan bir kapsayıcı depolama hesabınızdaki.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a>Kod içinde bir kapsayıcı oluşturma
Merhaba de kullanabilirsiniz **CloudBlobClient** toocreate depolama hesabınızdaki bir kapsayıcı. Tek toodo ihtiyacınız olan tooadd bir çağrı çok**CreateIfNotExistsAsync** koddan hello olduğu gibi:

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


**Not:** hello çağrıları tooAzure depolama ASP.NET Core gerçekleştirmek API'leri zaman uyumsuz. Bkz: [uyumsuz ve bekleme ile zaman uyumsuz programlama](http://msdn.microsoft.com/library/hh191443.aspx) daha fazla bilgi için. Aşağıdaki Hello kodu zaman uyumsuz programlama yöntemleri kullanıldığı varsayılmaktadır.

toomake hello dosyaları hello kapsayıcı kullanılabilir tooeveryone içinde hello kapsayıcı toobe ortak koddan hello kullanarak ayarlayabilirsiniz.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a>Bir kapsayıcıya bir blob yükleme
bir kapsayıcı halinde bir blob dosya tooupload bir kapsayıcı başvurusu alın ve tooget bir blob başvurusu kullanın. Bir blob başvurusu aldıktan sonra herhangi bir veri tooit akışıdır tarafından arama hello yükleyebilirsiniz **UploadFromStreamAsync** yöntemi. Bu işlem henüz veya mevcut değilse bu raporun üzerine hello blob oluşturur. örnekte gösterildiği nasıl aşağıdaki hello tooupload blob bir kapsayıcı halinde ve o hello kapsayıcısı zaten oluşturulduğu varsayılmaktadır.

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Liste hello BLOB'ları bir kapsayıcıda
toolist hello BLOB'ları bir kapsayıcıda, ilk olarak bir kapsayıcı başvurusu alın. Ardından hello kapsayıcının çağırabilirsiniz **ListBlobsSegmentedAsync** yöntemi tooretrieve hello blobları ve/veya dizinleri içindeki. tooaccess hello zengin özellik ve yöntem **Ilistblobıtem**, tooa atamalısınız **CloudBlockBlob**, **CloudPageBlob**, veya  **CloudBlobDirectory** nesnesi. Varsa yazın hello blob bilmiyorsanız, hangi toocast türü onay toodetermine kullanabileceğiniz şekilde. koddan hello tooretrieve ve çıkış URI bir kapsayıcıdaki her öğesinin nasıl hello gösterir.

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

Vardır diğer yolları toolist hello bir blob kapsayıcı içeriğini. Bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) daha fazla bilgi için.

## <a name="download-a-blob"></a>Blob indirme
toodownload bir blob başvurusu toohello blob ilk alın ve hello çağrısı **DownloadToStreamAsync** yöntemi. Merhaba aşağıdaki örnek kullanır hello **DownloadToStreamAsync** sonra yerel bir dosya olarak kaydedin yöntemi tootransfer hello blob içeriği tooa akış nesnesi.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

Dosyaları olarak toosave BLOB'ları diğer yolları vardır. Bkz: [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](storage-dotnet-how-to-use-blobs.md#download-blobs) daha fazla bilgi için.

## <a name="delete-a-blob"></a>Blob silme
toodelete bir blob başvurusu toohello blob ilk alın ve hello çağrısı **DeleteAsync** yöntemini.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

