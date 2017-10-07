---
title: php'den aaaHow toouse blob storage (nesne depolama) | Microsoft Docs
description: "Azure Blob storage (nesne depolama) ile Merhaba bulutta yapılandırılmamış veri depolayın."
documentationcenter: php
services: storage
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1af56b59-b3f0-4b46-8441-aab463ae088e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 331405e583c17c4f71acacdc0078b2bc71efbef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a>Nasıl toouse blob depolama biriminden PHP
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Genel Bakış
Azure Blob Depolama hello bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir. Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir. BLOB Depolama başvurulan tooas nesne depolama de olabilir.

Bu kılavuz size nasıl tooperform yaygın senaryolar hello Azure'ı kullanarak blob hizmeti gösterir. Merhaba örnekler PHP ile yazılmıştır ve hello kullan [PHP için Azure SDK][download]. Merhaba kapsanan senaryolar dahil **karşıya**, **listeleme**, **indirme**, ve **silme** BLOB'lar. BLOB'ları hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next-steps) bölümü.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>PHP uygulaması oluşturma
Merhaba hello Azure blob hizmete erişen bir PHP uygulaması oluşturmaya yönelik gereksinim, yalnızca hello hello Azure SDK sınıfları, PHP'nin için kodunuzu içinde başvuruyor. Uygulamanızın, Not Defteri dahil olmak üzere tüm geliştirme araçları toocreate kullanabilirsiniz.

Bu kılavuzda, bir PHP uygulamasının içinde yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir hizmet özelliklerini kullanın.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure istemci kitaplıkları Al
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a>Uygulama tooaccess hello blob hizmeti yapılandırın
toouse hello Azure blob hizmeti API'leri, şunları yapmanız gerekir:

1. Hello kullanarak başvuru hello otomatik yükleyici dosyasını [require_once] deyimi, ve
2. Kullanabileceğinize sınıfları başvuru.

Merhaba aşağıdaki örnekte nasıl tooinclude hello otomatik Yükleyiciden dosya ve başvuru hello gösterir **ServicesBuilder** sınıfı.

> [!NOTE]
> Bu makalede Hello örnekler hello oluşturucu aracılığıyla Azure için PHP istemci kitaplıkları yüklü olduğunu varsayar. Merhaba kitaplıklarını el ile yüklediyseniz tooreference hello gerekir `WindowsAzure.php` otomatik yükleyici dosyası.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Merhaba aşağıdaki örnekte, hello `require_once` deyimi her zaman gösterilecek, ancak yalnızca hello sınıfları hello örnek tooexecute için gereken başvuru.

## <a name="set-up-an-azure-storage-connection"></a>Bir Azure depolama bağlantı kurma
tooinstantiate bir Azure blob hizmeti istemcisi, öncelikle geçerli bir bağlantı dizesi olması gerekir. Merhaba blob hizmeti bağlantı dizesini Hello biçimdedir:

Canlı hizmetine erişmek için:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Merhaba depolama öykünücüsü erişmek için:

```php
UseDevelopmentStorage=true
```

toocreate herhangi bir Azure hizmeti istemci toouse hello gereksinim **ServicesBuilder** sınıfı. Şunları yapabilirsiniz:

* Merhaba bağlantı geçirmek doğrudan tooit dize veya
* Kullanım hello **CloudConfigurationManager (CCM)** toocheck birden çok dış kaynaklardan hello bağlantı dizesi:
  * Varsayılan olarak, bir dış kaynak - ortam değişkenleri için destek ile gelir.
  * Merhaba genişleterek yeni kaynakları ekleyebilirsiniz **ConnectionStringSource** sınıfı.

Burada özetlenen hello örnekler için başlangıç bağlantı dizesi doğrudan geçirilir.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a>Bir kapsayıcı oluşturma
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

A **BlobRestProxy** nesnesi ile Merhaba bir blob kapsayıcı oluşturun olanak tanır **createContainer** yöntemi. Bir kapsayıcı oluştururken hello kapsayıcı seçeneklerini ayarlayabilirsiniz, ancak bunun nedenle gerekli değildir. (aşağıdaki hello örnek tooset hello kapsayıcı nasıl erişim denetimi listesi (ACL) ve kapsayıcı meta verilerini gösterir.)

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Blob\Models\CreateContainerOptions;
use MicrosoftAzure\Storage\Blob\Models\PublicAccessType;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


// OPTIONAL: Set public access policy and metadata.
// Create container options object.
$createContainerOptions = new CreateContainerOptions();

// Set public access policy. Possible values are
// PublicAccessType::CONTAINER_AND_BLOBS and PublicAccessType::BLOBS_ONLY.
// CONTAINER_AND_BLOBS:
// Specifies full public read access for container and blob data.
// proxys can enumerate blobs within hello container via anonymous
// request, but cannot enumerate containers within hello storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within hello container via
// anonymous request.
// If this value is not specified in hello request, container data is
// private toohello account owner.
$createContainerOptions->setPublicAccess(PublicAccessType::CONTAINER_AND_BLOBS);

// Set container metadata.
$createContainerOptions->addMetaData("key1", "value1");
$createContainerOptions->addMetaData("key2", "value2");

try    {
    // Create container.
    $blobRestProxy->createContainer("mycontainer", $createContainerOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Çağırma **setPublicAccess (PublicAccessType::CONTAINER\_ve\_BLOB'lar)** yapar hello kapsayıcı ve blob verilerini anonim istekler erişilebilir. Çağırma **setPublicAccess(PublicAccessType::BLOBS_ONLY)** yalnızca blob veri anonim istekler erişilebilir hale getirir. Kapsayıcı ACL'ler hakkında daha fazla bilgi için bkz: [kümesi kapsayıcı ACL (REST API'si)][container-acl].

Blob hizmeti hata kodları hakkında daha fazla bilgi için bkz: [Blob hizmeti hata kodları][error-codes].

## <a name="upload-a-blob-into-a-container"></a>Bir kapsayıcıya bir blob yükleme
bir dosya bir BLOB kullanım hello tooupload **BlobRestProxy -> createBlockBlob** yöntemi. Bu işlem mevcut değil veya varsa üzerine yazar hello blob oluşturur. Merhaba aşağıdaki kod örneği, hello kapsayıcısı zaten oluşturulmuş kullanır varsayar ve [fopen] [ fopen] tooopen hello dosyasını bir akış olarak.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


$content = fopen("c:\myfile.txt", "r");
$blob_name = "myblob";

try    {
    //Upload blob
    $blobRestProxy->createBlockBlob("mycontainer", $blob_name, $content);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Önceki örnek hello Not blob bir akış olarak yükler. Ancak, bir blob de, örneğin, hello kullanarak bir dize olarak yüklenebilen [dosya\_almak\_içeriği] [ file_get_contents] işlevi. toodo bu değişiklik hello önceki örnek kullanma, `$content = fopen("c:\myfile.txt", "r");` çok`$content = file_get_contents("c:\myfile.txt");`.

## <a name="list-hello-blobs-in-a-container"></a>Liste hello BLOB'ları bir kapsayıcıda
toolist hello BLOB'ları bir kapsayıcıda kullanmak hello **BlobRestProxy -> listBlobs** yöntemi ile bir **foreach** tooloop hello sonucundan döngü. Merhaba aşağıdaki kod bir kapsayıcıda çıktı olarak her bir blob hello adını görüntüler ve kendi URI toohello tarayıcı görüntüler.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // List blobs.
    $blob_list = $blobRestProxy->listBlobs("mycontainer");
    $blobs = $blob_list->getBlobs();

    foreach($blobs as $blob)
    {
        echo $blob->getName().": ".$blob->getUrl()."<br />";
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="download-a-blob"></a>Blob indirme
toodownload bir blob çağrısı hello **BlobRestProxy -> getBlob** yöntemi sonra çağrı hello **getContentStream** hello kaynaklanan yöntemi **GetBlobResult** nesnesi.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Get blob.
    $blob = $blobRestProxy->getBlob("mycontainer", "myblob");
    fpassthru($blob->getContentStream());
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Yukarıdaki bu hello örnek bir akış kaynağı (Merhaba, varsayılan davranıştır) olarak bir blob alır unutmayın. Ancak, hello kullanabilirsiniz [akış\_almak\_içeriği] [ stream-get-contents] işlevi tooconvert hello akış tooa dizesi döndürdü.

## <a name="delete-a-blob"></a>Blob silme
toodelete bir blob geçirmek hello kapsayıcı adı hem de blob adı çok**BlobRestProxy -> deleteBlob**.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Delete blob.
    $blobRestProxy->deleteBlob("mycontainer", "myblob");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-a-blob-container"></a>Bir blob kapsayıcısından silin
Son olarak, bir blob kapsayıcısını toodelete geçirmek hello kapsayıcı adı çok**BlobRestProxy -> deleteContainer**.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);

try    {
    // Delete container.
    $blobRestProxy->deleteContainer("mycontainer");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>Sonraki adımlar
Hello Azure blob hizmeti hello temellerini öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin.

* Merhaba ziyaret [Azure depolama ekibi blogu](http://blogs.msdn.com/b/windowsazurestorage/)
* Merhaba bkz [PHP blok blobu örnek](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).
* Merhaba bkz [PHP sayfa blob örnek](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).
* [Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı](storage-use-azcopy.md)

Daha fazla bilgi için hello Ayrıca bkz. [PHP Geliştirici Merkezi](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
