---
title: "C++ ile Azure File storage için aaaDevelop | Microsoft Docs"
description: "Nasıl toodevelop C++ uygulamaları ve Azure File storage toostore kullanan hizmetler dosya verileri öğrenin."
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: 40c3aac94214a91121913e2ded315031aeed1c30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a>C++ ile Azure File storage için geliştirme
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Bu öğretici hakkında

Bu öğreticide şunları öğreneceksiniz nasıl tooperform Azure File storage üzerinde temel işlemler. Aracılığıyla örnekleri, C++ ile yazılmış nasıl toocreate paylaşır öğreneceksiniz ve dizinleri, karşıya yükleme, liste ve dosyaları silin. Yeni tooAzure dosya depolama varsa, hello kavramları izleyin hello bölümlerde aracılığıyla hello örnekleri anlaşılmasına yardımcı olur.


* Oluşturma ve Azure dosya paylaşımları silme
* Oluşturma ve dizinleri silme
* Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme
* Karşıya yükleyin, indirin ve dosya silme
* Bir Azure dosya paylaşımı için Hello kota (en fazla boyut) ayarlama
* Merhaba paylaşımında tanımlı bir paylaşılan erişim ilkesi kullanan bir dosya için paylaşılan erişim imzası (SAS anahtarı) oluşturun.

> [!Note]  
> SMB üzerinden Azure File storage erişilebileceği için hello standart C++ g/ç sınıfları ve işlevleri kullanarak hello Azure dosya paylaşımına erişim olası toowrite basit uygulamalar var. Bu makalede nasıl kullanan toowrite uygulamaları hello kullanan Azure depolama C++ SDK hello anlatmaktadır [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure dosya depolama.

## <a name="create-a-c-application"></a>C++ uygulaması oluşturma
toobuild hello örnekleri, C++ için tooinstall hello Azure Storage istemci kitaplığı 2.4.0 gerekir. Ayrıca bir Azure depolama hesabı oluşturduğunuz.

tooinstall hello Azure Storage istemcisi 2.4.0 C++ için yöntemler aşağıdaki hello birini kullanabilirsiniz:

* **Linux:** hello verilen hello yönergeleri izleyerek [C++ Benioku için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) sayfası.
* **Windows:** Visual Studio'da sırasıyla **Araçları &gt; NuGet Paket Yöneticisi &gt; Paket Yöneticisi Konsolu**. Türü hello şu komutu hello [NuGet Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) ve basın **ENTER**.
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a>Uygulama toouse Azure File storage ayarlayın
Deyimleri toohello üst toomanipulate Azure File storage istediğiniz hello C++ kaynak dosyasının Hello şunlar ekleyin:

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Bir Azure depolama bağlantı dizesi ayarlama
Dosya depolama toouse tooconnect tooyour Azure depolama hesabınızın olması gerekir. Merhaba ilk adımı tooconfigure kullanacağız bir bağlantı dizesi olacaktır tooconnect tooyour depolama hesabı. Şimdi bir statik değişken toodo tanımlamak.

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a>Tooan Azure depolama hesabı bağlanma
Merhaba kullanabilirsiniz **cloud_storage_account** toorepresent depolama hesabı bilgilerinizi sınıfı. tooretrieve depolama hesap bilgileri hello depolama bağlantı dizesinden, hello kullanabilirsiniz **ayrıştırma** yöntemi.

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a>Bir Azure dosya paylaşımı oluşturma
Tüm dosyaları ve dizinleri Azure dosya depolama olarak adlandırılan bir kapsayıcıda yer bir **paylaşımı**. Depolama hesabınız hesap kapasitenizi verdiğinden sayıda paylaşımları olabilir. tooobtain erişim tooa paylaşımı ve içeriklerini, toouse Azure dosya depolama istemcisi gerekir.

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

Hello Azure File storage İstemcisi'ni kullanarak bir başvuru tooa paylaşımı edinebilirsiniz.

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

toocreate hello paylaşımı, kullanım hello **create_if_not_exists** hello yöntemi **cloud_file_share** nesnesi.

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

Bu noktada, **paylaşmak** adlı bir başvuru tooa paylaşımı tutan **örnek paylaşımı my**.

## <a name="delete-an-azure-file-share"></a>Bir Azure Dosya Paylaşımı Sil
Bir paylaşım silme arama hello tarafından yapılır **delete_if_exists** cloud_file_share nesnesi üzerinde yöntemi. Yapan örnek kod aşağıda verilmiştir.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a>Dizin oluşturma
Bunların tümünün hello kök dizinine sahip olmak yerine alt dizinleri içindeki dosyaları koyarak depolama düzenleyebilirsiniz. Azure File storage hesabı olacak olarak birden çok dizini izin toocreate sağlar. Aşağıdaki Hello kodu adlı bir dizin oluşturur **örnek dizin my** adlı bir alt yanı sıra hello kök dizini altında **örnek alt my**.

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a>Bir dizini silme
Hala dosyaları içeren bir dizin veya diğer dizinleri silemezsiniz unutulmamalıdır rağmen bir dizin silinmesi basit bir görev olduğundan.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme
Dosya ve dizinlerin bir paylaşımı içinde listesini alma kolayca yapılır çağırarak **list_files_and_directories** üzerinde bir **cloud_file_directory** başvuru. tooaccess hello zengin özellik ve yöntem **list_file_and_directory_item**, hello çağırmalısınız **list_file_and_directory_item.as_file** yöntemi tooget bir **cloud_ Dosya** nesne veya hello **list_file_and_directory_item.as_directory** yöntemi tooget bir **cloud_file_directory** nesnesi.

koddan hello tooretrieve ve çıkış URI hello paylaşımının hello kök dizininde her öğesinin nasıl hello gösterir.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a>Dosyayı karşıya yükleme
Merhaba çok, bir Azure dosya paylaşımı dosyalarının bulunduğu bir kök dizin içeriyor. Bu bölümde, nasıl tooupload hello üzerine yerel depolama biriminden bir dosya kök dizini bir paylaşımın öğreneceksiniz.

bir dosyayı karşıya yüklemeyi hello ilk adımı tooobtain bulunduğu bir başvuru toohello dizin oluşturur. Arama hello tarafından bunu **get_root_directory_reference** hello Paylaşım nesnesinin yöntemi.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

Bir başvuru toohello kök dizin hello paylaşımının sahip olduğunuza göre üzerine bir dosyayı karşıya yükleyebilirsiniz. Bu örnek, bir dosya, metin ve bir akış yükler.

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a>Dosya indirme
toodownload dosyaları, önce dosya başvurusu alın ve ardından hello çağırın **download_to_stream** sonra sürdürebilirsiniz yöntemi tootransfer hello dosya içeriği tooa akış nesne tooa yerel dosya. Alternatif olarak, hello kullanabilirsiniz **download_to_file** yöntemi toodownload hello bir dosya tooa yerel dosyanın içeriğini. Merhaba kullanabilirsiniz **download_text** yöntemi toodownload hello bir metin dizesi olarak bir dosyanın içeriğini.

Merhaba aşağıdaki örnek kullanır hello **download_to_stream** ve **download_text** yöntemleri toodemonstrate önceki kısımlarında oluşturulan hello dosyaları indirme.

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a>Dosya silme
Başka bir ortak Azure File storage dosya silme işlemdir. Merhaba aşağıdaki kod my-örnek-dosya-hello kök dizini altında depolanan 3 adlı bir dosyayı siler.

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a>Bir Azure dosya paylaşımı için Hello kota (en fazla boyut) ayarlama
Gigabayt cinsinden bir dosya paylaşımı için hello kota (veya üst sınırı) ayarlayabilirsiniz. Ayrıca, ne kadar veri şu anda hello paylaşımında depolanan toosee kontrol edebilirsiniz.

Ayarı hello tarafından paylaşımı için kota bir, hello paylaşımında depolanan hello dosyaların toplam boyutu hello sınırlayabilirsiniz. Hello hello paylaşımdaki dosyaların toplam boyutu aşarsa hello kota hello paylaşımında ayarlayın, sonra istemcileri oluşturulamıyor tooincrease hello mevcut dosyaların boyutunu olabilir veya bu dosyaları boş olmadığı sürece, yeni dosyalar oluşturma.

Aşağıdaki örnek Hello nasıl toocheck hello bir paylaşım için geçerli kullanım ve nasıl tooset hello hello paylaşımı için kota gösterir.

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Dosya veya dosya paylaşımı için paylaşılan erişim imzası oluşturma
Paylaşılan erişim imzası (SAS) tek bir dosyayı veya dosya paylaşımı için oluşturabilirsiniz. Ayrıca, bir dosya paylaşımı toomanage paylaşılan erişim imzaları bir paylaşılan erişim ilkesi oluşturabilirsiniz. Tehlikeye girdiği durumlarda hello SAS iptal etme yolu sağladığı gibi bir paylaşılan erişim ilkesi oluşturmanız önerilir.

Aşağıdaki örneğine hello bir paylaşılan erişim ilkesi oluşturulur ve Itanium tabanlı sistemler için ilke tooprovide hello kısıtlamaları SAS için hello bir dosyada paylaşıma kullanır.

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a>Sonraki adımlar
Azure Storage hakkında daha fazla toolearn bu kaynakları araştırın:

* [C++ için Depolama İstemcisi Kitaplığı](https://github.com/Azure/azure-storage-cpp)
* [Azure depolama dosya hizmeti örnekleri c++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)
* [Azure Depolama Gezgini](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [Azure Depolama Belgeleri](https://azure.microsoft.com/documentation/services/storage/)