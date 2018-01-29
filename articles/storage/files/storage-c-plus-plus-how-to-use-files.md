---
title: "C++ ile Azure dosyaları için geliştirme | Microsoft Docs"
description: "C++ uygulamaları ve dosya verilerini depolamak için Azure dosyaları kullanan hizmetleri geliştirmeyi öğrenin."
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
ms.date: 09/19/2017
ms.author: renashahmsft
ms.openlocfilehash: d2f55b5ca6348ba8e190c65ec9a72c6f730d869e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="develop-for-azure-files-with-c"></a>C++ ile Azure dosyaları için geliştirme
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Bu öğretici hakkında

Bu öğreticide, Azure dosyalarda temel işlemleri gerçekleştirmeyi öğreneceksiniz. C++'da yazılmış örnekleri sayesinde, paylaşımları ve dizinler oluşturma, karşıya yükleme, liste ve dosyaları silin öğreneceksiniz. Azure dosyaları yeniyseniz, aşağıdaki bölümlerde açıklanan kavramlar aracılığıyla örnekleri anlaşılmasına yardımcı olur.


* Oluşturma ve Azure dosya paylaşımları silme
* Oluşturma ve dizinleri silme
* Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme
* Karşıya yükleyin, indirin ve dosya silme
* Bir Azure dosya paylaşımı için kota (en fazla boyut) ayarlama
* Paylaşımda tanımlı bir paylaşılan erişim ilkesi kullanan bir dosya için paylaşılan erişim imzası (SAS anahtarı) oluşturma.

> [!Note]  
> Azure dosyaları SMB üzerinden erişilebileceği için standart C++ g/ç sınıfları ve işlevleri kullanarak Azure dosya paylaşımına erişmek basit uygulamaları yazmak mümkündür. Bu makalede Azure depolama C++ kullanan SDK'ın, uygulamaların nasıl yazılacağını anlatmaktadır [dosya REST API'si](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) Azure dosyaları anlaşmak için.

## <a name="create-a-c-application"></a>C++ uygulaması oluşturma
Örnekleri oluşturmak için Azure Storage istemci Kitaplığı'nı 2.4.0 C++ için yüklemeniz gerekir. Ayrıca bir Azure depolama hesabı oluşturduğunuz.

C++ için Azure Storage istemcisi 2.4.0 yüklemek için aşağıdaki yöntemlerden birini kullanabilirsiniz:

* **Linux:** verilen yönergeleri izleyerek [C++ Benioku için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) sayfası.
* **Windows:** Visual Studio'da sırasıyla **Araçları &gt; NuGet Paket Yöneticisi &gt; Paket Yöneticisi Konsolu**. Aşağıdaki komutu yazın [NuGet Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) ve basın **ENTER**.
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-to-use-azure-files"></a>Azure dosyaları kullanmak için uygulamanızı ayarlama
Azure dosyaları yönetmek istediğiniz C++ kaynak dosyanın en üstüne deyimleri şunlar ekleyin:

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Bir Azure depolama bağlantı dizesi ayarlama
Dosya depolama kullanmak için Azure depolama hesabınıza bağlanmanız gerekir. İlk adım, depolama hesabınıza bağlanmak için kullanacağız bir bağlantı dizesini yapılandırmak için olacaktır. Şimdi bunun için statik bir değişken tanımlayın.

```cpp
// Define the connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-to-an-azure-storage-account"></a>Bir Azure depolama hesabına bağlanma
Kullanabileceğiniz **cloud_storage_account** depolama hesabı bilgileri temsil eden sınıf. Depolama bağlantı dizesi, depolama hesabı bilgilerini almak için kullanabileceğiniz **ayrıştırma** yöntemi.

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a>Bir Azure dosya paylaşımı oluşturma
Tüm dosya ve dizinlerin bir Azure dosya paylaşımı adı verilen bir kapsayıcıda yer bir **paylaşmak**. Depolama hesabınız hesap kapasitenizi verdiğinden sayıda paylaşımları olabilir. Bir paylaşımı ve içeriklerini erişim elde etmek için bir Azure dosyaları istemci kullanmanız gerekir.

```cpp
// Create the Azure Files client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

Azure dosyaları İstemcisi'ni kullanarak bir paylaşım için bir başvuru edinebilirsiniz.

```cpp
// Get a reference to the file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

Paylaşımı oluşturmak için kullanın **create_if_not_exists** yöntemi **cloud_file_share** nesnesi.

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

Bu noktada, **paylaşmak** adlı bir paylaşım için bir başvuru tutan **örnek paylaşımı my**.

## <a name="delete-an-azure-file-share"></a>Bir Azure Dosya Paylaşımı Sil
Bir paylaşım silme yapılır çağırarak **delete_if_exists** cloud_file_share nesnesi üzerinde yöntemi. Yapan örnek kod aşağıda verilmiştir.

```cpp
// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete the share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a>Dizin oluşturma
Depolama kök dizininde yerine bunların tümünün alt dizinleri içindeki dosyaları koyarak düzenleyebilirsiniz. Azure dosyaları hesabınızı izin verdiği sayıda dizinleri oluşturmanıza olanak sağlar. Aşağıdaki kodu adlı bir dizin oluşturacak **örnek dizin my** adlı bir alt yanı sıra kök dizini altında **örnek alt my**.

```cpp
// Retrieve a reference to a directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if the share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a>Bir dizini silme
Hala dosyaları içeren bir dizin veya diğer dizinleri silemezsiniz unutulmamalıdır rağmen bir dizin silinmesi basit bir görev olduğundan.

```cpp
// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference to the directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference to the subdirectory you want to delete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete the subdirectory and the sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme
Dosya ve dizinlerin bir paylaşımı içinde listesini alma kolayca yapılır çağırarak **list_files_and_directories** üzerinde bir **cloud_file_directory** başvuru. Zengin özellik ve yöntem erişmek için **list_file_and_directory_item**, çağırmalısınız **list_file_and_directory_item.as_file** almak için yöntemi bir **cloud_file**  nesnesi veya **list_file_and_directory_item.as_directory** almak için yöntemi bir **cloud_file_directory** nesnesi.

Aşağıdaki kod, almak ve paylaşımın kök dizininde bulunan her öğesinin URI çıkış gösterilmiştir.

```cpp
//Get a reference to the root directory for the share.
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
En azından bir Azure dosya paylaşımı dosyalarının bulunduğu kök dizini içerir. Bu bölümde, bir paylaşım kök dizini üzerine yerel depolama biriminden bir dosya karşıya nasıl yükleneceğini öğreneceksiniz.

Bir dosyayı karşıya yüklemeyi ilk adımı bulunduğu dizin başvuru elde edilir. Çağırarak bunu **get_root_directory_reference** Paylaşım nesnesinin yöntemi.

```cpp
//Get a reference to the root directory for the share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

Bir başvuru paylaşımının kök dizinine sahip olduğunuza göre üzerine bir dosyayı karşıya yükleyebilirsiniz. Bu örnek, bir dosya, metin ve bir akış yükler.

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
Dosyalarını indirmek için önce bir dosya başvurusu alın ve ardından arama **download_to_stream** dosya içeriğini sonra yerel bir dosyaya kalıcı bir akış nesnesine aktarmak için yöntem. Alternatif olarak, kullanabileceğiniz **download_to_file** yerel bir dosyaya bir dosyanın içeriğini indirmek için yöntem. Kullanabileceğiniz **download_text** bir metin dizesi olarak bir dosyanın içeriğini indirmek için yöntem.

Aşağıdaki örnek kullanır **download_to_stream** ve **download_text** önceki kısımlarında oluşturulan dosyaları indirme göstermek için yöntemleri.

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

## <a name="delete-a-file"></a>Dosyayı silme
Başka bir ortak Azure dosyaları dosya silme işlemdir. Aşağıdaki kod, my-örnek-dosya-kök dizini altında depolanan 3 adlı bir dosyayı siler.

```cpp
// Get a reference to the root directory for the share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-the-quota-maximum-size-for-an-azure-file-share"></a>Bir Azure dosya paylaşımı için kota (en fazla boyut) ayarlama
Gigabayt cinsinden bir dosya paylaşımı için kota (veya üst sınırı) ayarlayabilirsiniz. Paylaşımda halihazırda ne kadar verinin depolandığını da kontrol edebilirsiniz.

Paylaşım için kota ayarlayarak paylaşımda depolanan toplam dosya boyutunu kısıtlayabilirsiniz. Paylaşımdaki toplam dosya boyutu belirlediğiniz kotayı aşarsa, istemciler mevcut dosyaların boyutunu artıramaz veya boş olmamaları halinde yeni dosyalar oluşturamaz.

Aşağıdaki örnekte, paylaşımdaki mevcut kullanımını nasıl kontrol edileceği veya paylaşım için nasıl kota ayarlanacağı gösterilmiştir.

```cpp
// Parse the connection string for the storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference to the share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets the quota to 2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Dosya veya dosya paylaşımı için paylaşılan erişim imzası oluşturma
Paylaşılan erişim imzası (SAS) tek bir dosyayı veya dosya paylaşımı için oluşturabilirsiniz. Ayrıca, paylaşılan erişim imzalarını yönetmek için dosya paylaşımında bir paylaşılan erişim ilkesi oluşturabilirsiniz. Gizliliğinin tehlikeye girdiği durumlarda SAS’yi iptal etme aracı olarak kullanılabilmesi nedeniyle bir paylaşılan erişim ilkesi oluşturmanız önerilir.

Aşağıdaki örnekte, paylaşım için bir paylaşılan erişim ilkesi oluşturulur, daha sonra bu ilke paylaşımdaki bir dosyada bulunan SAS için sınırlamalar sağlamak amacıyla kullanılır.

```cpp
// Parse the connection string for the storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the file client and get a reference to the share
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

    //set permissions to expire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for the share
    azure::storage::file_share_permissions permissions;    

    //retrieve the current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add the new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save the updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve the root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in the share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from the SAS, and write some text to the file.        
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
Azure Storage hakkında daha fazla bilgi için şu kaynakları araştırın:

* [C++ için Depolama İstemcisi Kitaplığı](https://github.com/Azure/azure-storage-cpp)
* [Azure depolama dosya hizmeti örnekleri c++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)
* [Azure Depolama Gezgini](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [Azure Depolama Belgeleri](https://azure.microsoft.com/documentation/services/storage/)