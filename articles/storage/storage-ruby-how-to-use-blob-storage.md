---
title: aaaHow toouse ruby'den Blob storage (nesne depolama) | Microsoft Docs
description: "Azure Blob storage (nesne depolama) ile Merhaba bulutta yapılandırılmamış veri depolayın."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 638826777f5a7ae8330fd67cdbb51d5eee1736a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a>Nasıl toouse ruby'den Blob storage
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Genel Bakış
Azure Blob Depolama hello bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir. Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir. BLOB Depolama başvurulan tooas nesne depolama de olabilir.

Bu kılavuz size nasıl gösterir Blob storage kullanarak tooperform senaryoları. Merhaba örnekleri hello Ruby API kullanılarak yazılır. Merhaba kapsanan senaryolar dahil **karşıya yükleme, listeleme, indirme,** ve **silme** BLOB'lar.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Ruby uygulaması oluşturma
Bir Ruby uygulaması oluşturun. Yönergeler için bkz: [Azure VM'de rayları Web uygulaması üzerinde Söyleniş](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)

## <a name="configure-your-application-tooaccess-storage"></a>Uygulama tooaccess depolama yapılandırma
Azure Storage toouse, toodownload ve kullanım hello hello storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içeren Söyleniş azure paketi gerekir.

### <a name="use-rubygems-tooobtain-hello-package"></a>RubyGems tooobtain hello paketini kullanın
1. Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (UNIX).
2. "Gem yükle azure" Merhaba komut penceresinde tooinstall hello gem ve bağımlılıkları yazın.

### <a name="import-hello-package"></a>Merhaba paketi İçeri Aktar
Sık kullandığınız metin Düzenleyicisi'ni kullanarak hello toouse depolama burada düşündüğünüz Söyleniş dosya toohello üstündeki aşağıdaki hello ekleyin:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Bir Azure depolama bağlantı kurma
Hello azure modülü hello ortam değişkenleri okuma **AZURE\_depolama\_hesap** ve **AZURE\_depolama\_ACCESS_KEY** için bilgi tooconnect tooyour Azure depolama hesabı gerekiyor. Bu ortam değişkenleri ayarlanmamışsa, kullanmadan önce hello hesap bilgileri belirtmelisiniz **Azure::Blob::BlobService** koddan hello ile:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain hello Azure portal bu değerleri Klasik veya Resource Manager depolama hesabı:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Toouse istediğiniz toohello depolama hesabının gidin.
3. Merhaba sağ üzerinde Hello ayarları dikey penceresinde tıklayın **erişim tuşları**.
4. Görüntülenen hello erişim anahtarları dikey penceresinde hello erişim tuşu 1 ve 2 erişim anahtarı görürsünüz. Bunlardan kullanabilirsiniz.
5. Merhaba Kopyala simgesi toocopy hello anahtar toohello Pano'ı tıklatın.

tooobtain hello Klasik Azure Portalı'nda bu değerleri Klasik depolama hesabı:

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Toouse istediğiniz toohello depolama hesabının gidin.
3. Tıklatın **erişim ANAHTARLARINI Yönet** hello Gezinti bölmesinin hello altındaki.
4. Merhaba açılan iletişim kutusunda hello depolama hesabı adı, birincil erişim anahtarını ve ikincil erişim anahtarını görürsünüz. Erişim anahtarı hello birincil veya ikincil bir hello kullanabilirsiniz.
5. Merhaba Kopyala simgesi toocopy hello anahtar toohello Pano'ı tıklatın.

## <a name="create-a-container"></a>Bir kapsayıcı oluşturma
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Merhaba **Azure::Blob::BlobService** nesne kapsayıcıları ve blob'larla çalışmanıza olanak sağlar. toocreate bir kapsayıcı kullanmak hello **oluşturma\_container()** yöntemi.

Merhaba aşağıdaki kod örneğinde bir kapsayıcı oluşturur veya varsa hello hata yazdırır.

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

Toomake hello hello kapsayıcı dosyalarında ortak istiyorsanız hello kapsayıcının izinlerini ayarlayabilirsiniz.

Merhaba yalnızca değiştirebileceğiniz <strong>oluşturma\_container()</strong> çağrısı toopass hello **: ortak\_erişim\_düzeyi** seçeneği:

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

Hello için geçerli değerler **: ortak\_erişim\_düzeyi** seçeneği şunlardır:

* **BLOB:** BLOB'lar için herkese okuma erişimi belirtir. Bu kapsayıcı içindeki BLOB verilerini anonim istek okunabilir ancak kapsayıcı verileri mevcut değil. İstemcilerin anonim istek aracılığıyla hello kapsayıcıdaki blobları numaralandırılamıyor.
* **kapsayıcı:** tam ortak okuma erişimi için kapsayıcı ve blob verilerini belirtir. İstemcilerin anonim istek aracılığıyla hello kapsayıcıdaki blobları sıralayabilirsiniz, ancak depolama hesabı Merhaba kapsayıcılara numaralandırılamıyor.

Alternatif olarak, bir kapsayıcı hello genel erişim düzeyini kullanarak değiştirebileceğiniz **ayarlamak\_kapsayıcı\_acl()** yöntemi toospecify hello genel erişim düzeyi.

Aşağıdaki kod örneğine değişiklikleri hello genel erişim düzeyi çok hello**kapsayıcı**:

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a>Bir kapsayıcıya bir blob yükleme
tooupload içerik tooa blob, kullanım hello **oluşturma\_blok\_blob()** yöntemi toocreate hello blob, bir dosya kullanın veya dize hello BLOB Merhaba içeriğine.

Merhaba aşağıdaki kodu hello dosya yüklemeleri **test.png** "görüntü-blob'u" Merhaba kapsayıcısında adlı yeni bir blob olarak.

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a>Liste hello BLOB'ları bir kapsayıcıda
toolist hello kapsayıcılar kullanma **list_containers()** yöntemi.
bir kapsayıcıdaki toolist hello BLOB'ları kullanmak **listesi\_blobs()** yöntemi.

Bu, tüm Merhaba kapsayıcılara hello hesabı için tüm hello blobları hello URL'lerini çıkarır.

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a>Blob’ları indirme
toodownload BLOB'ları kullanmak hello **almak\_blob()** yöntemi tooretrieve hello içeriği.

Merhaba aşağıdaki kod örneğinde kullanarak gösterilmektedir **almak\_blob()** toodownload hello "görüntü blob'u" içeriğini ve tooa yerel dosya yazma.

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a>Bir Blob Sil
Son olarak, bir blob toodelete kullanmak hello **silmek\_blob()** yöntemi. Merhaba aşağıdaki kod örneğinde gösterilmektedir nasıl toodelete blob.

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a>Sonraki adımlar
daha karmaşık depolama görevleri hakkında toolearn bu bağlantıları izleyin:

* [Azure Depolama Ekibi Blog’u](http://blogs.msdn.com/b/windowsazurestorage/)
* [Ruby için Azure SDK](https://github.com/WindowsAzure/azure-sdk-for-ruby) github'daki
* [Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı](storage-use-azcopy.md)

