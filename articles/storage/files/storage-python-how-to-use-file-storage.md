---
title: "Python ile Azure File storage için geliştirme | Microsoft Docs"
description: "Python uygulamaları ve dosya verilerini depolamak için Azure File storage'ı kullanma hizmetleri geliştirmeyi öğrenin."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 3dd14e8d3ea7d1e50f41633a7920a6d36becf789
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a>Python ile Azure File storage için geliştirme
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Bu öğretici hakkında
Bu öğretici, temel uygulamaları veya dosya verilerini depolamak için Azure dosya depolama kullanan hizmetler geliştirmek için Python kullanımını gösterilmektedir. Bu öğreticide, basit bir konsol uygulaması oluşturur ve Python ve Azure File storage ile temel eylemleri gerçekleştirme göster:

* Azure dosya paylaşımları oluşturma
* Dizinler oluşturma
* Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme
* Karşıya yükleyin, indirin ve dosya silme

> [!Note]  
> SMB üzerinden Azure File storage erişilebileceği için standart Python g/ç sınıfları ve işlevleri kullanarak Azure dosya paylaşımına erişim basit uygulamaları yazmak mümkündür. Bu makalede Azure depolama Python kullanan SDK'ın, uygulamaların nasıl yazılacağını anlatmaktadır [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) Azure dosya depolama alanına anlaşmak için.

### <a name="set-up-your-application-to-use-azure-file-storage"></a>Uygulamanızı Azure File storage kullanacak şekilde ayarlama
Azure Storage programlı olarak erişmek istediğiniz tüm Python kaynak dosyanın en üstüne yakın aşağıdakileri ekleyin.

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a>Azure File storage için bir bağlantı ayarlayın 
`FileService` Nesne paylaşımları, dizinleri ve dosyaları ile çalışmanıza olanak sağlar. Aşağıdaki kod oluşturur bir `FileService` depolama hesabı adı ve hesap anahtarını kullanarak nesne. Değiştir `<myaccount>` ve `<mykey>` , hesap adı ve anahtarınız ile.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Bir Azure dosya paylaşımı oluşturma
Aşağıdaki kod örneğinde kullanabileceğiniz bir `FileService` yoksa paylaşımı oluşturmak için nesne.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>Dizin oluşturma
Depolama kök dizininde yerine bunların tümünün alt dizinleri içindeki dosyaları yerleştirerek de düzenleyebilirsiniz. Azure File storage hesabınıza izin verdiği sayıda dizinleri oluşturmanıza olanak sağlar. Aşağıdaki kodu adlı bir alt dizinin oluşturacak **sampledir** kök dizininin altında.

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme
Dosyaların ve dizinlerin bir paylaşımda listelemek için kullanın **listesi\_dizinleri\_ve\_dosyaları** yöntemi. Bu yöntem bir oluşturucuyu döndürür. Aşağıdaki kod çıktıları **adı** her bir dosya ve dizin konsoluna bir paylaşımda.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>Dosyayı karşıya yükleme 
Azure dosya paylaşımı en azından içerir, bir kök dizin dosyalarının bulunduğu. Bu bölümde, bir paylaşım kök dizini üzerine yerel depolama biriminden bir dosya karşıya nasıl yükleneceğini öğreneceksiniz.

Bir dosya oluşturun ve verileri yüklemek için kullanmak `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` veya `create_file_from_text` yöntemleri. Bunlar veri boyutu 64 MB aştığında gerekli Öbekleme gerçekleştiren üst düzey yöntemleridir.

`create_file_from_path`Belirtilen yol bir dosyanın içeriğini yükler ve `create_file_from_stream` zaten açılmış bir dosya/akışı içeriğini yükler. `create_file_from_bytes`bayt dizisi yükler ve `create_file_from_text` belirtilen (varsayılan UTF-8) kodlaması kullanarak belirli bir metin değeri yükler.

Aşağıdaki örnek içeriğini yükler **sunset.png** içine dosya **myfile** dosya.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>Dosya indirme
Bir dosyadan veri indirmek için kullanacağınız `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, veya `get_file_to_text`. Bunlar veri boyutu 64 MB aştığında gerekli Öbekleme gerçekleştiren üst düzey yöntemleridir.

Aşağıdaki örnek, kullanma gösterir `get_file_to_path` içeriğini indirmek için **myfile** dosya ve onun için depolamak **çıkış sunset.png** dosya.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>Dosya silme
Son olarak, bir dosyayı silmek için çağrı `delete_file`.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>Sonraki adımlar
Python ile Azure File storage işlemek nasıl öğrendiğinize göre daha fazla bilgi için aşağıdaki bağlantıları izleyin.

* [Python Geliştirici Merkezi](/develop/python/)
* [Azure Depolama Hizmetleri REST API'si](http://msdn.microsoft.com/library/azure/dd179355)
* [Microsoft Azure depolama için Python SDK'sı](https://github.com/Azure/azure-storage-python)