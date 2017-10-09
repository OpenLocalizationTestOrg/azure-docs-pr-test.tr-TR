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
ms.openlocfilehash: 3df0cf14b69d85cdc2f62cc3c8b901be102fa026
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a>.NET kullanarak Azure Blob Storage’ı kullanmaya başlayın

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

Azure Blob Depolama hello bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir. Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir. BLOB Depolama başvurulan tooas nesne depolama de olabilir.

### <a name="about-this-tutorial"></a>Bu öğretici hakkında
Bu öğretici, Azure Blob storage kullanarak bazı genel senaryolar için .NET toowrite kodu nasıl gösterir. Kapsanan senaryolar arasında blob yükleme, listeleme, indirme ve silme yer alır.

**Ön koşullar:**

* [Microsoft Visual Studio](https://www.visualstudio.com/)
* [.NET için Azure Depolama İstemcisi](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [.NET için Azure Yapılandırma Yöneticisi](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* Bir [Azure Storage hesabı](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Daha fazla örnek
Blob depolama kullanan diğer örnekler için [.NET’te Azure Blob Depolama Kullanmaya Başlama](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/). Merhaba örnek uygulamayı indirin ve çalıştırın veya hello kodu github'da göz atın.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Using yönergeleri ekleme
Merhaba aşağıdakileri ekleyin **kullanarak** hello yönergeleri toohello üst `Program.cs` dosyası:

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a>Merhaba bağlantı dizesini ayrıştırma
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a>Merhaba Blob hizmeti istemcisi oluşturma
Merhaba **CloudBlobClient** sınıfı sağlar, size, tooretrieve kapsayıcılar ve bloblar Blob depolama alanına depolanır. Tek yönlü toocreate hello hizmeti istemcisi şöyledir:

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
Artık veri okuyan ve yazan veri tooBlob depolama hazır toowrite kodu bulunur.

## <a name="create-a-container"></a>Bir kapsayıcı oluşturma
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Bu örnekte gösterilir nasıl toocreate zaten yoksa, bir kapsayıcı:

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

Varsayılan olarak, hello yeni kapsayıcı depolama erişim anahtarı toodownload bloblarınızın bu kapsayıcısından belirlemeniz gerektiği anlamına gelir. Merhaba kapsayıcı kullanılabilir tooeveryone içindeki toomake hello dosyaları istiyorsanız hello kapsayıcı toobe ortak koddan hello kullanarak ayarlayabilirsiniz:

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

Merhaba Internet üzerinden herkes ortak bir kapsayıcıdaki blobları görebilir. Ancak, değiştirme veya yalnızca hello uygun hesap erişim tuşu veya paylaşılan erişim imzası varsa silin.

## <a name="upload-a-blob-into-a-container"></a>Bir kapsayıcıya bir blob yükleme
Azure Blob Storage blok blobları ve sayfa bloblarını destekler.  Çoğu durumda, blok blob türü toouse önerilen hello ' dir.

tooupload dosya tooa blok blob bir kapsayıcı başvurusu alın ve blok blob başvurusu tooget kullanın. Bir blob başvurusu edindiğinizde arama hello tarafından herhangi bir veri tooit akışıdır yükleyebilirsiniz **UploadFromStream** yöntemi. Bu işlem daha önce bulunamadı veya mevcut değilse bu raporun üzerine hello blob oluşturur.

örnekte gösterildiği nasıl aşağıdaki hello tooupload blob bir kapsayıcı halinde ve o hello kapsayıcısı zaten oluşturulduğu varsayılmaktadır.

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

## <a name="list-hello-blobs-in-a-container"></a>Liste hello BLOB'ları bir kapsayıcıda
toolist hello BLOB'ları bir kapsayıcıda, ilk olarak bir kapsayıcı başvurusu alın. Merhaba kapsayıcının sonra kullanabileceğiniz **ListBlobs** yöntemi tooretrieve hello blobları ve/veya dizinleri içindeki. tooaccess hello zengin özellik ve yöntem **Ilistblobıtem**, tooa atamalısınız **CloudBlockBlob**, **CloudPageBlob**, veya  **CloudBlobDirectory** nesnesi. Merhaba türü bilinmiyor, hangi toocast türü onay toodetermine kullanabilirsiniz için. Merhaba aşağıdaki kodu nasıl tooretrieve ve çıktı hello her öğe URI'sini hello gösterir _fotoğraf_ kapsayıcı:

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

Blob adlarına yol bilgilerini ekleyerek, geleneksel bir dosya sisteminde olduğu gibi düzenleme ve geçiş yapabileceğiniz sanal bir dizin yapısı oluşturabilirsiniz. Merhaba dizin yapısını sanal Blob depolama alanına kullanılabilir kaynakları kapsayıcılar ve bloblar yalnızca yalnızca--hello. Ancak, hello depolama istemci kitaplığı sunar bir **CloudBlobDirectory** nesne toorefer tooa sanal dizini ve bu şekilde düzenlenen BLOB'ları ile çalışmanın hello işlemini basitleştirir.

Örneğin, adlandırılmış bir kapsayıcıda blok blobları kümesine aşağıdaki hello göz önünde bulundurun *fotoğraf*:

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

Çağırdığınızda **ListBlobs** hello üzerinde *fotoğraf* kapsayıcı (önceki kod parçacığını hello olduğu gibi), hiyerarşik bir listeleme döner. Her ikisi de içeren **CloudBlobDirectory** ve **CloudBlockBlob** hello dizinleri ve blobları hello kapsayıcıda sırasıyla temsil eden nesne. Merhaba sonuçta çıktı şuna benzer:

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

İsteğe bağlı olarak, hello ayarlayabilirsiniz **Listblobs** hello parametresinin **ListBlobs** yönteme **doğru**. Bu durumda, hello kapsayıcıdaki her blob olarak döndürülür bir **CloudBlockBlob** nesnesi. Çağrı çok hello**ListBlobs** tooreturn düz listeleme şu şekilde görünür:

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

ve hello sonuçlar şöyle görünür:

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

## <a name="download-blobs"></a>Blob’ları indirme
toodownload BLOB'lar, ilk olarak bir blob başvurusu alın ve ardından hello çağırın **DownloadToStream** yöntemi. Merhaba aşağıdaki örnek kullanır hello **DownloadToStream** yöntemi tootransfer hello blob içeriği tooa stream nesnesi tooa yerel dosya daha sonra devam edebilir.

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

Merhaba de kullanabilirsiniz **DownloadToStream** yöntemi toodownload hello içeriği blob olarak bir metin dizesi.

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

## <a name="delete-blobs"></a>Blob’ları silme
toodelete bir blob önce bir blob başvurusu alın ve ardından arama **silmek** yöntemini.

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

## <a name="list-blobs-in-pages-asynchronously"></a>Blob’ları sayfalarda zaman uyumsuz olarak listeleme
Çok sayıda BLOB listeliyorsanız veya toocontrol hello bir listeleme işlemi ile dönen sonuç sayısını isterseniz sonuç sayfalarında blobları listeleyebilirsiniz. Böylece yürütme tooreturn büyük bir sonuç kümesi beklenirken engellenmeyen Bu örnek nasıl tooreturn sayfalarında zaman uyumsuz olarak sonuçları gösterir.

Bu örnek düz bir blob listesi gösterir, ancak ayarı hello tarafından da hiyerarşik bir listeleme gerçekleştirebilirsiniz _Listblobs_ hello parametresinin **ListBlobsSegmentedAsync** yöntemi too_false_.

Merhaba örnek yöntemi zaman uyumsuz bir yöntem çağırdığı için onu hello ile dönmelidir _zaman uyumsuz_ anahtar sözcüğü ve döndürmelidir bir **görev** nesnesi. Merhaba await hello için belirtilen anahtar sözcüğü **ListBlobsSegmentedAsync** yöntemi hello listeleme görevi tamamlanana kadar hello örnek yönteminin yürütülmesi askıya alır.

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

## <a name="writing-tooan-append-blob"></a>Yazma tooan blob ekleme
Ek blob, günlük tutma gibi ekleme işlemleri için en iyi duruma getirilmiştir. Bir blok blobu gibi bir ek blobu bloklardan oluşur, ancak yeni bir blok tooan ek blob eklediğinizde, bu her zaman eklenmiş toohello hello blob sonudur. Bir ek blobdaki mevcut bloğu güncelleştiremezsiniz veya silemezsiniz. bir blok blobu olduğu gibi bir ek blobu Hello blok kimliği gösterilmez.

Her bir ek blobu bloğunda tooa en fazla 4 MB yukarı farklı bir boyutta olabilir ve bir ek blobu en fazla 50.000 blok içerebilir. Merhaba en fazla bir ek blobu bu nedenle biraz 195 GB'tan (4 MB X 50.000 blok) boyutudur.

Aşağıdaki Hello örnek yeni bir ek blob oluşturur ve basit günlük yazma işlemini benzeterek bazı veri tooit ekler.

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

Bkz: [anlama blok Blobları, sayfa Blobları ve ek Bloblarını](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) hello hello üç türde BLOB arasındaki farklar hakkında daha fazla bilgi.

## <a name="managing-security-for-blobs"></a>Blobların güvenliğini sağlama
Varsayılan olarak, Azure depolama, verilerinizi hello hesabı erişim anahtarlarını elinde olan erişim toohello hesabına sahip sınırlayarak güvende tutar. Depolama hesabınızı tooshare blob verilerini gerektiğinde, önemli toodo olduğundan bunu hesap erişim tuşlarınızı hello güvenliğini tehlikeye olmadan. Ayrıca, Azure storage'da ve hello kablo üzerinden giderek güvenlidir blob veri tooensure şifreleyebilirsiniz.

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a>Erişim tooblob veri denetleme
Varsayılan olarak, depolama hesabınızda blob verileri hello erişilebilir yalnızca toostorage hesap sahibi değil. Blob Storage'a karşı istek kimlik doğrulaması varsayılan olarak hello hesap erişim tuşu gerektirir. Ancak, toomake isteyebilir belirli blob veri kullanılabilir tooother kullanıcıları. İki seçeneğiniz vardır:

* **Anonim erişim:** Bir kapsayıcıyı veya bloblarını anonim erişim için genel erişime açabilirsiniz. Bkz: [anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](storage-manage-access-to-resources.md) daha fazla bilgi için.
* **Paylaşılan erişim imzası:** istemcileri belirlediğiniz izinlerle ve belirttiğiniz bir aralığında depolama hesabınızdaki atanmış erişim tooa kaynak sağlayan bir paylaşılan erişim imzası (SAS) sağlayabilirsiniz. Daha fazla bilgi edinmek için bkz. [Paylaşılan Erişim İmzaları (SAS) kullanma](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

### <a name="encrypting-blob-data"></a>Blob verilerini şifreleme
Azure depolama hello istemcide hem hello sunucuda blob verisi şifreleme özelliği destekler.

* **İstemci tarafı şifreleme:** tooAzure depolama karşıya yükleme ve toohello istemci indirilirken verilerin şifresini çözmek önce istemci uygulamalar içinde şifrelenen verilerin .NET desteklediği için depolama istemci kitaplığı hello. Merhaba kitaplık ayrıca depolama hesabı anahtarı yönetimi için Azure anahtar kasası ile tümleştirmeyi destekler. Daha fazla bilgi için bkz. [Microsoft Azure Storage için .NET içinde İstemci Tarafı Şifreleme](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json). Ayrıca bkz. [Öğretici: Azure Anahtar Kasası kullanılarak Microsoft Azure Storage’daki blobları şifreleme ve şifresini çözme](storage-encrypt-decrypt-blobs-key-vault.md).
* **Sunucu tarafı şifreleme**: Azure Storage artık sunucu tarafı şifreleme desteklemektedir. Bkz. [Bekleyen Veri için Azure Storage Hizmeti Şifreleme (Önizleme)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

## <a name="next-steps"></a>Sonraki adımlar
Blob storage'nın hello temel bilgileri öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.

### <a name="microsoft-azure-storage-explorer"></a>Microsoft Azure Depolama Gezgini
* [Microsoft Azure Depolama Gezgini (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.

### <a name="blob-storage-samples"></a>Blob depolama örnekleri
* [.NET’te Azure Blob Depolama Kullanmaya Başlama](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a>Blob Storage başvurusu
* [.NET başvurusu için Depolama İstemci Kitaplığı](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [REST API başvurusu](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a>Kavramsal kılavuzlar
* [Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [.NET için Dosya depolamayı kullanmaya başlama](../files/storage-dotnet-how-to-use-files.md)
* [Nasıl toouse Azure blob depolama hello WebJobs SDK ile](../../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
