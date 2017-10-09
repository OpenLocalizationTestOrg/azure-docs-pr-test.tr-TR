---
title: "C++ içinden aaaHow toouse blob storage (nesne depolama) | Microsoft Docs"
description: "Azure Blob storage (nesne depolama) ile Merhaba bulutta yapılandırılmamış veri depolayın."
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: e63df4683e5c10c9f8fbe4106c655df61be0e1a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a>Nasıl toouse Blob depolama alanından C++
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Genel Bakış
Azure Blob Depolama hello bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir. Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir. BLOB Depolama başvurulan tooas nesne depolama de olabilir.

Bu kılavuzu kullanarak tooperform genel senaryolar Azure Blob Depolama hizmetinin nasıl hello gösterilmektedir. Merhaba örnekleri C++ ile yazılmış ve hello kullan [C++ için Azure Storage istemci Kitaplığı](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Merhaba kapsanan senaryolar dahil **karşıya**, **listeleme**, **indirme**, ve **silme** BLOB'lar.  

> [!NOTE]
> Bu kılavuzu hedefleri c++ sürümü 1.0.0 ve yukarıda Azure Storage istemci kitaplığı hello. Merhaba önerilir sürümü aracılığıyla kullanılabilir olan depolama istemci kitaplığı 2.2.0, [NuGet](http://www.nuget.org/packages/wastorage) veya [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>C++ uygulaması oluşturma
Bu kılavuzda, C++ uygulamasında çalıştırabileceğiniz depolama özelliklerini kullanır.  

toodo tooinstall ihtiyacınız olacak şekilde, C++ için Azure Storage istemci kitaplığı hello ve Azure aboneliğinizde bir Azure depolama hesabı oluşturun.   

tooinstall hello Azure Storage istemci kitaplığı C++ için hello aşağıdaki yöntemleri kullanabilirsiniz:

* **Linux:** hello verilen hello yönergeleri izleyerek [C++ Benioku için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) sayfası.  
* **Windows:** Visual Studio'da sırasıyla **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**. Türü hello şu komutu hello [NuGet Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) ve basın **ENTER**.  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-blob-storage"></a>Uygulama tooaccess Blob Storage yapılandırın
Deyimleri toohello dosyasının üst kısmında toouse hello Azure depolama API'leri tooaccess BLOB'lar istediğiniz hello C++ Hello şunlar ekleyin:  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a>Bir Azure depolama bağlantı dizesini ayarlayın
Bir Azure storage istemcisi bir depolama bağlantı dizesi toostore uç kullanır ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgileri. Bir istemci uygulamasında çalıştırırken hello depolama bağlantı dizesi biçimi aşağıdaki, hello listelenen hello depolama hesabı için depolama hesabı ve hello depolama erişim anahtarınızı hello adını kullanarak hello olarak sağlamalısınız [Azure Portal](https://portal.azure.com)hello için *AccountName* ve *AccountKey* değerleri. Depolama hesapları ve erişim anahtarları hakkında daha fazla bilgi için bkz: [Azure Storage hesapları hakkında](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json). Bu örnek, bir statik alan toohold hello bağlantı dizesini nasıl bildirebilir gösterir:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest uygulamanızı yerel Windows bilgisayarınızda, Microsoft Azure hello kullanabilirsiniz [depolama öykünücüsü](../storage-use-emulator.md) ile Merhaba yüklü [Azure SDK'sı](https://azure.microsoft.com/downloads/). Merhaba depolama öykünücüsü hello Blob, kuyruk ve Tablo Hizmetleri, yerel geliştirme makinenizde Azure'da kullanılabilir benzetim yapan bir yardımcı programdır. Merhaba aşağıdaki örnek bir statik alan toohold hello bağlantı dizesi tooyour yerel depolama öykünücüsü nasıl bildirebilir gösterir:

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart hello Azure storage öykünücüsü, Select hello **Başlat** düğmesini veya tuşuna hello **Windows** anahtarı. Yazmaya başlayın **Azure Storage öykünücüsü**seçip **Microsoft Azure Storage öykünücüsü** uygulamaları hello listesinden.  

Merhaba aşağıdaki örnekleri bu iki yöntem tooget hello depolama bağlantı dizesi birini kullandığınızı varsayar.  

## <a name="retrieve-your-connection-string"></a>Bağlantı dizesi alma
Merhaba kullanabilirsiniz **cloud_storage_account** toorepresent depolama hesabı bilgilerinizi sınıfı. tooretrieve depolama hesap bilgileri hello depolama bağlantı dizesinden, hello kullanabilirsiniz **ayrıştırma** yöntemi.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

Ardından, bir başvuru tooa almak **cloud_blob_client** kapsayıcılar ve bloblar Blob Depolama hizmetinin hello içinde depolanan temsil eden tooretrieve nesnelerini izin verdiği ölçüde sınıfı. Merhaba aşağıdaki kod oluşturur bir **cloud_blob_client** biz alınan yukarıda hello depolama hesabı nesnesini kullanarak nesnesi:  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a>Nasıl yapılır: bir kapsayıcı oluşturma
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Bu örnekte gösterilir nasıl toocreate zaten yoksa, bir kapsayıcı:  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

Varsayılan olarak, hello yeni kapsayıcı özeldir ve bu kapsayıcı, depolama erişim anahtarı toodownload bloblarından belirtmeniz gerekir. Merhaba kapsayıcı kullanılabilir tooeveryone içinde toomake hello dosyaları (BLOB) istiyorsanız hello kapsayıcı toobe ortak koddan hello kullanarak ayarlayabilirsiniz:  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

Merhaba Internet üzerinden herkes ortak bir kapsayıcıdaki blobları görebilir ancak değiştirdiğinizde ya da yalnızca hello uygun erişim anahtarı varsa, bunları silin.  

## <a name="how-to-upload-a-blob-into-a-container"></a>Nasıl yapılır: bir kapsayıcıya bir blob karşıya yükleme
Azure Blob Storage blok blobları ve sayfa bloblarını destekler. Merhaba çoğu durumda, blok blob türü toouse önerilen hello ' dir.  

tooupload dosya tooa blok blob bir kapsayıcı başvurusu alın ve blok blob başvurusu tooget kullanın. Bir blob başvurusu edindiğinizde arama hello tarafından herhangi bir veri tooit akışıdır yükleyebilirsiniz **upload_from_stream** yöntemi. Bu işlem daha önce mevcut alamadık veya mevcut değilse üzerine hello blob oluşturur. örnekte gösterildiği nasıl aşağıdaki hello tooupload blob bir kapsayıcı halinde ve o hello kapsayıcısı zaten oluşturulduğu varsayılmaktadır.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

Alternatif olarak, hello kullanabilirsiniz **upload_from_file** yöntemi tooupload dosya tooa blok blobu.

## <a name="how-to-list-hello-blobs-in-a-container"></a>Nasıl yapılır: hello BLOB'ları bir kapsayıcıda listelemek
toolist hello BLOB'ları bir kapsayıcıda, ilk olarak bir kapsayıcı başvurusu alın. Merhaba kapsayıcının sonra kullanabileceğiniz **list_blobs** yöntemi tooretrieve hello blobları ve/veya dizinleri içindeki. tooaccess hello zengin özellik ve yöntem **list_blob_item**, hello çağırmalısınız **list_blob_item.as_blob** yöntemi tooget bir **cloud_blob** nesnesi veya hello **list_blob.as_directory** yöntemi tooget cloud_blob_directory nesnesi. Merhaba aşağıdaki kodu nasıl tooretrieve ve çıktı hello her öğe URI'sini hello gösterir **örnek kapsayıcı my** kapsayıcı:

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

İşlem listeleme konusunda daha fazla ayrıntı için bkz: [listesi Azure depolama kaynaklarını c++](../storage-c-plus-plus-enumeration.md).

## <a name="how-to-download-blobs"></a>Nasıl yapılır: BLOB'ları indirme
toodownload BLOB'lar, ilk olarak bir blob başvurusu alın ve ardından hello çağırın **download_to_stream** yöntemi. Merhaba aşağıdaki örnek kullanır hello **download_to_stream** yöntemi tootransfer hello blob içeriği tooa stream nesnesi tooa yerel dosya daha sonra devam edebilir.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

Alternatif olarak, hello kullanabilirsiniz **download_to_file** yöntemi toodownload hello blob tooa dosyasının içeriğini.
Ayrıca, aynı zamanda hello kullanabilirsiniz **download_text** yöntemi toodownload hello içeriği blob olarak bir metin dizesi.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a>Nasıl yapılır: BLOB'ları silme
bir blob toodelete önce bir blob başvurusu alın ve ardından hello çağırın **delete_blob** yöntemini.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a>Sonraki adımlar
Blob storage'nın hello temel bilgileri öğrendiğinize göre Azure Storage hakkında daha fazla bu bağlantılar toolearn izleyin.  

* [Nasıl toouse C++ içinden kuyruk depolama](../storage-c-plus-plus-how-to-use-queues.md)
* [Nasıl toouse C++ tablo depolamasından](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [C++'ta listesi Azure Storage kaynakları](../storage-c-plus-plus-enumeration.md)
* [C++ başvurusu için depolama istemci kitaplığı](http://azure.github.io/azure-storage-cpp)
* [Azure Depolama Belgeleri](https://azure.microsoft.com/documentation/services/storage/)
* [Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı](../storage-use-azcopy.md)

