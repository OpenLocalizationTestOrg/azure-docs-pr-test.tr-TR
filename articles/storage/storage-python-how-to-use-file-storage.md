---
title: "Python ile Azure File storage için aaaDevelop | Microsoft Docs"
description: "Nasıl toodevelop Python uygulamalar ve Azure File storage toostore kullanan hizmetler dosya verileri öğrenin."
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
ms.openlocfilehash: 45623e6dbec6f140cedc4e58e56a93fb4af9054e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a>Python ile Azure File storage için geliştirme
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Bu öğretici hakkında
Bu öğretici Python toodevelop uygulamalar veya Azure File storage toostore dosya verilerini kullanan Hizmetleri kullanma temelleri hello gösterilmektedir. Bu öğreticide, basit bir konsol uygulaması oluşturur ve Göster nasıl tooperform temel eylemleri Python ve Azure File storage ile:

* Azure dosya paylaşımları oluşturma
* Dizinler oluşturma
* Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme
* Karşıya yükleyin, indirin ve dosya silme

> [!Note]  
> SMB üzerinden Azure File storage erişilebileceği için hello standart Python g/ç sınıfları ve işlevleri kullanarak hello Azure dosya paylaşımına erişim olası toowrite basit uygulamalar var. Bu makalede nasıl kullanan toowrite uygulamaları hello kullanan Azure depolama Python SDK hello anlatmaktadır [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure dosya depolama.

### <a name="set-up-your-application-toouse-azure-file-storage"></a>Uygulama toouse Azure File storage ayarlayın
Tooprogrammatically erişim Azure Storage istediğiniz herhangi bir Python kaynak dosyasının hello üstüne yakın Hello aşağıdakileri ekleyin.

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a>Bir bağlantı tooAzure dosya depolama ayarlayın 
Merhaba `FileService` nesne paylaşımları, dizinleri ve dosyaları ile çalışmanıza olanak sağlar. Merhaba aşağıdaki kod oluşturur bir `FileService` Merhaba, depolama hesabı adı ve hesap anahtarını kullanarak nesnesi. Değiştir `<myaccount>` ve `<mykey>` , hesap adı ve anahtarınız ile.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Bir Azure dosya paylaşımı oluşturma
Aşağıdaki kod örneğine hello kullanabileceğiniz bir `FileService` yoksa nesne toocreate hello paylaşımı.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>Dizin oluşturma
Ayrıca, bunların tümünün hello kök dizinine sahip olmak yerine alt dizinleri içindeki dosyaları koyarak depolama düzenleyebilirsiniz. Azure File storage hesabı olacak olarak birden çok dizini izin toocreate sağlar. Aşağıdaki Hello kodu adlı bir alt dizinin oluşturur **sampledir** hello kök dizininin altında.

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme
toolist hello dosyaları ve dizinleri bir paylaşımda kullanmak hello **listesi\_dizinleri\_ve\_dosyaları** yöntemi. Bu yöntem bir oluşturucuyu döndürür. Merhaba aşağıdaki kodu çıkarır hello **adı** her bir dosya ve dizin paylaşımı toohello konsolunda.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>Dosyayı karşıya yükleme 
Azure dosya paylaşımı hello çok az içerir, bir kök dizin dosyalarının bulunduğu. Bu bölümde, nasıl tooupload hello üzerine yerel depolama biriminden bir dosya kök dizini bir paylaşımın öğreneceksiniz.

bir dosya toocreate ve karşıya yükleme verileri kullanmak hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` veya `create_file_from_text` yöntemleri. Bunlar hello verilerin hello boyutu 64 MB aştığında hello gerekli Öbekleme gerçekleştiren üst düzey yöntemleridir.

`create_file_from_path`Karşıya hello hello belirtilen yoldan dosya içeriğini ve `create_file_from_stream` karşıya hello zaten açılmış bir dosya/akışı içeriği. `create_file_from_bytes`bayt dizisi yükler ve `create_file_from_text` karşıya hello belirtilen hello kullanarak metin değeri belirtilen kodlama (Varsayılanları tooUTF-8).

Merhaba aşağıdaki örnek yükler hello Merhaba içeriğine **sunset.png** hello dosyasına **myfile** dosya.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>Dosya indirme
bir dosya toodownload verileri kullan `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, veya `get_file_to_text`. Bunlar hello verilerin hello boyutu 64 MB aştığında hello gerekli Öbekleme gerçekleştiren üst düzey yöntemleridir.

Merhaba aşağıdaki örneği kullanarak gösterir `get_file_to_path` toodownload Merhaba içeriğine hello **myfile** toohello depolamak ve dosya **çıkış sunset.png** dosya.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>Dosya silme
Son olarak, bir dosya toodelete çağrı `delete_file`.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>Sonraki adımlar
Artık, öğrendiğinize göre nasıl toomanipulate Python, Azure File storage daha fazla bu bağlantılar toolearn izleyin.

* [Python Geliştirici Merkezi](/develop/python/)
* [Azure Depolama Hizmetleri REST API'si](http://msdn.microsoft.com/library/azure/dd179355)
* [Microsoft Azure depolama için Python SDK'sı](https://github.com/Azure/azure-storage-python)