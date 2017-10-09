---
title: aaaHow toouse python'dan Azure Blob storage (nesne depolama) | Microsoft Docs
description: "Azure Blob storage (nesne depolama) ile Merhaba bulutta yapılandırılmamış veri depolayın."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 6efc61aa89e6d2544b7a18c80ce3546640f90462
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a>Nasıl toouse python'dan Azure Blob Depolama
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Genel Bakış
Azure Blob Depolama hello bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir. Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir. BLOB Depolama başvurulan tooas nesne depolama de olabilir.

Bu makale size nasıl gösterir Blob storage kullanarak tooperform senaryoları. Merhaba örnekleri Python içinde yazılmış ve hello kullan [Python için Microsoft Azure depolama SDK]. karşıya yükleme, listeleme, indirme ve BLOB'ları silme kapsamdaki hello senaryolar içerir.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a>Bir kapsayıcı oluşturma
Merhaba blob türüne göre toouse, istediğiniz oluşturma bir **BlockBlobService**, **AppendBlobService**, veya **PageBlobService** nesnesi. Merhaba aşağıdaki kod kullanan bir **BlockBlobService** nesnesi. Tooprogrammatically erişim Azure blok Blob Depolama istediğiniz herhangi bir Python dosyasının kaydedileceği hello üstüne yakın Hello aşağıdakileri ekleyin.

```python
from azure.storage.blob import BlockBlobService
```

Merhaba aşağıdaki kod oluşturur bir **BlockBlobService** Merhaba, depolama hesabı adı ve hesap anahtarını kullanarak nesnesi.  'Myaccount' ve 'mykey' hesap adı ve anahtarı ile değiştirin.

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Aşağıdaki kod örneğine hello kullanabileceğiniz bir **BlockBlobService** yoksa nesne toocreate hello kapsayıcısı.

```python
block_blob_service.create_container('mycontainer')
```

(Daha önce yaptığınız gibi), depolama erişim anahtarınızı belirtmeniz gerekir böylece varsayılan olarak, hello yeni kapsayıcı özel, bu kapsayıcı toodownload bloblarından. Merhaba kapsayıcı kullanılabilir tooeveryone içinde toomake hello BLOB'lar istiyorsanız, hello kapsayıcı oluşturmak ve koddan hello kullanarak hello genel erişim düzeyini geçirin.

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

Alternatif olarak, aşağıdaki kodu hello oluşturduktan sonra bir kapsayıcı değiştirebilirsiniz.

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

Bu değişiklikten sonra hello Internet üzerinden herkes ortak bir kapsayıcıdaki blobları görebilir ancak yalnızca değiştirebilir veya silebilirsiniz.

## <a name="upload-a-blob-into-a-container"></a>Bir kapsayıcıya bir blob yükleme
toocreate blok blobu ve karşıya yükleme verileri kullanmak hello **oluşturma\_blob\_gelen\_yolu**, **oluşturma\_blob\_gelen\_akış**, **oluşturma\_blob\_gelen\_bayt** veya **oluşturma\_blob\_gelen\_metin** yöntemleri. Bunlar hello verilerin hello boyutu 64 MB aştığında hello gerekli Öbekleme gerçekleştiren üst düzey yöntemleridir.

**oluşturma\_blob\_gelen\_yolu** karşıya hello hello belirtilen yol, bir dosyanın içeriğini ve **oluşturma\_blob\_gelen\_akış** karşıya hello zaten açılmış bir dosya/akışı içeriği. **oluşturma\_blob\_gelen\_bayt** bayt dizisi yükler ve **oluşturma\_blob\_gelen\_metin** belirtilen hello yükler Belirtilen kodlama (Varsayılanları tooUTF-8) Hello kullanarak metin değeri.

Merhaba aşağıdaki örnek yükler hello Merhaba içeriğine **sunset.png** hello dosyasına **myblob** blob.

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a>Liste hello BLOB'ları bir kapsayıcıda
toolist hello BLOB'ları bir kapsayıcıda kullanmak hello **listesi\_BLOB'lar** yöntemi. Bu yöntem bir oluşturucuyu döndürür. Merhaba aşağıdaki kodu çıkarır hello **adı** her BLOB bir kapsayıcı toohello konsolunda.

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a>Blob’ları indirme
bir blob toodownload verileri kullan **almak\_blob\_için\_yolu**, **almak\_blob\_için\_akış**, **alma\_blob\_için\_bayt**, veya **almak\_blob\_için\_metin**. Bunlar hello verilerin hello boyutu 64 MB aştığında hello gerekli Öbekleme gerçekleştiren üst düzey yöntemleridir.

Merhaba aşağıdaki örneği kullanarak gösterir **almak\_blob\_için\_yolu** toodownload Merhaba içeriğine hello **myblob** toohello depolamakveblob**çıkış sunset.png** dosya.

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a>Blob silme
Son olarak, bir blob toodelete çağrısı **delete_blob**.

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a>Yazma tooan blob ekleme
Ek blob, günlük tutma gibi ekleme işlemleri için en iyi duruma getirilmiştir. Bir blok blobu gibi bir ek blobu bloklardan oluşur, ancak yeni bir blok tooan ek blob eklediğinizde, bu her zaman eklenmiş toohello hello blob sonudur. Bir ek blobdaki mevcut bloğu güncelleştiremezsiniz veya silemezsiniz. bir blok blobu olduğu gibi bir ek blobu Hello blok kimliği gösterilmez.

Her bir ek blobu bloğunda tooa en fazla 4 MB yukarı farklı bir boyutta olabilir ve bir ek blobu en fazla 50.000 blok içerebilir. Merhaba en fazla bir ek blobu bu nedenle biraz 195 GB'tan (4 MB X 50.000 blok) boyutudur.

Aşağıdaki Hello örnek yeni bir ek blob oluşturur ve basit günlük yazma işlemini benzeterek bazı veri tooit ekler.

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a>Sonraki adımlar
Blob storage'nın hello temel bilgileri öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.

* [Python Geliştirici Merkezi](https://azure.microsoft.com/develop/python/)
* [Azure Depolama Hizmetleri REST API'si](http://msdn.microsoft.com/library/azure/dd179355)
* [Azure Depolama Ekibi Blog’u]
* [Python için Microsoft Azure depolama SDK]

[Azure Depolama Ekibi Blog’u]: http://blogs.msdn.com/b/windowsazurestorage/
[Python için Microsoft Azure depolama SDK]: https://github.com/Azure/azure-storage-python
