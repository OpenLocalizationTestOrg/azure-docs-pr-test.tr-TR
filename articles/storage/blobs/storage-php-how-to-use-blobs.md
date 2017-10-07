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
ms.openlocfilehash: 2e77415519b38007652e3ea372da531b3a97c5d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a><span data-ttu-id="04429-103">Nasıl toouse blob depolama biriminden PHP</span><span class="sxs-lookup"><span data-stu-id="04429-103">How toouse blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="04429-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="04429-104">Overview</span></span>
<span data-ttu-id="04429-105">Azure Blob Depolama hello bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="04429-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="04429-106">Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="04429-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="04429-107">BLOB Depolama başvurulan tooas nesne depolama de olabilir.</span><span class="sxs-lookup"><span data-stu-id="04429-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="04429-108">Bu kılavuz size nasıl tooperform yaygın senaryolar hello Azure'ı kullanarak blob hizmeti gösterir.</span><span class="sxs-lookup"><span data-stu-id="04429-108">This guide shows you how tooperform common scenarios using hello Azure blob service.</span></span> <span data-ttu-id="04429-109">Merhaba örnekler PHP ile yazılmıştır ve hello kullan [PHP için Azure SDK][download].</span><span class="sxs-lookup"><span data-stu-id="04429-109">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="04429-110">Merhaba kapsanan senaryolar dahil **karşıya**, **listeleme**, **indirme**, ve **silme** BLOB'lar.</span><span class="sxs-lookup"><span data-stu-id="04429-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="04429-111">BLOB'ları hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="04429-111">For more information on blobs, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="04429-112">PHP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="04429-112">Create a PHP application</span></span>
<span data-ttu-id="04429-113">Merhaba hello Azure blob hizmete erişen bir PHP uygulaması oluşturmaya yönelik gereksinim, yalnızca hello hello Azure SDK sınıfları, PHP'nin için kodunuzu içinde başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="04429-113">hello only requirement for creating a PHP application that accesses hello Azure blob service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="04429-114">Uygulamanızın, Not Defteri dahil olmak üzere tüm geliştirme araçları toocreate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04429-114">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="04429-115">Bu kılavuzda, bir PHP uygulamasının içinde yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir hizmet özelliklerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="04429-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="04429-116">Hello Azure istemci kitaplıkları Al</span><span class="sxs-lookup"><span data-stu-id="04429-116">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a><span data-ttu-id="04429-117">Uygulama tooaccess hello blob hizmeti yapılandırın</span><span class="sxs-lookup"><span data-stu-id="04429-117">Configure your application tooaccess hello blob service</span></span>
<span data-ttu-id="04429-118">toouse hello Azure blob hizmeti API'leri, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="04429-118">toouse hello Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="04429-119">Hello kullanarak başvuru hello otomatik yükleyici dosyasını [require_once] deyimi, ve</span><span class="sxs-lookup"><span data-stu-id="04429-119">Reference hello autoloader file using hello [require_once] statement, and</span></span>
2. <span data-ttu-id="04429-120">Kullanabileceğinize sınıfları başvuru.</span><span class="sxs-lookup"><span data-stu-id="04429-120">Reference any classes you might use.</span></span>

<span data-ttu-id="04429-121">Merhaba aşağıdaki örnekte nasıl tooinclude hello otomatik Yükleyiciden dosya ve başvuru hello gösterir **ServicesBuilder** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="04429-121">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="04429-122">Bu makalede Hello örnekler hello oluşturucu aracılığıyla Azure için PHP istemci kitaplıkları yüklü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="04429-122">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="04429-123">Merhaba kitaplıklarını el ile yüklediyseniz tooreference hello gerekir `WindowsAzure.php` otomatik yükleyici dosyası.</span><span class="sxs-lookup"><span data-stu-id="04429-123">If you installed hello libraries manually, you need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="04429-124">Merhaba aşağıdaki örnekte, hello `require_once` deyimi her zaman gösterilecek, ancak yalnızca hello sınıfları hello örnek tooexecute için gereken başvuru.</span><span class="sxs-lookup"><span data-stu-id="04429-124">In hello examples below, hello `require_once` statement will be shown always, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="04429-125">Bir Azure depolama bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="04429-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="04429-126">tooinstantiate bir Azure blob hizmeti istemcisi, öncelikle geçerli bir bağlantı dizesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="04429-126">tooinstantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="04429-127">Merhaba blob hizmeti bağlantı dizesini Hello biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="04429-127">hello format for hello blob service connection string is:</span></span>

<span data-ttu-id="04429-128">Canlı hizmetine erişmek için:</span><span class="sxs-lookup"><span data-stu-id="04429-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="04429-129">Merhaba depolama öykünücüsü erişmek için:</span><span class="sxs-lookup"><span data-stu-id="04429-129">For accessing hello storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="04429-130">toocreate herhangi bir Azure hizmeti istemci toouse hello gereksinim **ServicesBuilder** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="04429-130">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="04429-131">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="04429-131">You can:</span></span>

* <span data-ttu-id="04429-132">Merhaba bağlantı geçirmek doğrudan tooit dize veya</span><span class="sxs-lookup"><span data-stu-id="04429-132">Pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="04429-133">Kullanım hello **CloudConfigurationManager (CCM)** toocheck birden çok dış kaynaklardan hello bağlantı dizesi:</span><span class="sxs-lookup"><span data-stu-id="04429-133">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="04429-134">Varsayılan olarak, bir dış kaynak - ortam değişkenleri için destek ile gelir.</span><span class="sxs-lookup"><span data-stu-id="04429-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="04429-135">Merhaba genişleterek yeni kaynakları ekleyebilirsiniz **ConnectionStringSource** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="04429-135">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="04429-136">Burada özetlenen hello örnekler için başlangıç bağlantı dizesi doğrudan geçirilir.</span><span class="sxs-lookup"><span data-stu-id="04429-136">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="04429-137">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="04429-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="04429-138">A **BlobRestProxy** nesnesi ile Merhaba bir blob kapsayıcı oluşturun olanak tanır **createContainer** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="04429-138">A **BlobRestProxy** object lets you create a blob container with hello **createContainer** method.</span></span> <span data-ttu-id="04429-139">Bir kapsayıcı oluştururken hello kapsayıcı seçeneklerini ayarlayabilirsiniz, ancak bunun nedenle gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="04429-139">When creating a container, you can set options on hello container, but doing so is not required.</span></span> <span data-ttu-id="04429-140">(aşağıdaki hello örnek tooset hello kapsayıcı nasıl erişim denetimi listesi (ACL) ve kapsayıcı meta verilerini gösterir.)</span><span class="sxs-lookup"><span data-stu-id="04429-140">(hello example below shows how tooset hello container access control list (ACL) and container metadata.)</span></span>

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

<span data-ttu-id="04429-141">Çağırma **setPublicAccess (PublicAccessType::CONTAINER\_ve\_BLOB'lar)** yapar hello kapsayıcı ve blob verilerini anonim istekler erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="04429-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes hello container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="04429-142">Çağırma **setPublicAccess(PublicAccessType::BLOBS_ONLY)** yalnızca blob veri anonim istekler erişilebilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="04429-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="04429-143">Kapsayıcı ACL'ler hakkında daha fazla bilgi için bkz: [kümesi kapsayıcı ACL (REST API'si)][container-acl].</span><span class="sxs-lookup"><span data-stu-id="04429-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="04429-144">Blob hizmeti hata kodları hakkında daha fazla bilgi için bkz: [Blob hizmeti hata kodları][error-codes].</span><span class="sxs-lookup"><span data-stu-id="04429-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="04429-145">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="04429-145">Upload a blob into a container</span></span>
<span data-ttu-id="04429-146">bir dosya bir BLOB kullanım hello tooupload **BlobRestProxy -> createBlockBlob** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="04429-146">tooupload a file as a blob, use hello **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="04429-147">Bu işlem mevcut değil veya varsa üzerine yazar hello blob oluşturur.</span><span class="sxs-lookup"><span data-stu-id="04429-147">This operation creates hello blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="04429-148">Merhaba aşağıdaki kod örneği, hello kapsayıcısı zaten oluşturulmuş kullanır varsayar ve [fopen] [ fopen] tooopen hello dosyasını bir akış olarak.</span><span class="sxs-lookup"><span data-stu-id="04429-148">hello code example below assumes that hello container has already been created and uses [fopen][fopen] tooopen hello file as a stream.</span></span>

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

<span data-ttu-id="04429-149">Önceki örnek hello Not blob bir akış olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="04429-149">Note that hello previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="04429-150">Ancak, bir blob de, örneğin, hello kullanarak bir dize olarak yüklenebilen [dosya\_almak\_içeriği] [ file_get_contents] işlevi.</span><span class="sxs-lookup"><span data-stu-id="04429-150">However, a blob can also be uploaded as a string using, for example, hello [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="04429-151">toodo bu değişiklik hello önceki örnek kullanma, `$content = fopen("c:\myfile.txt", "r");` çok`$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="04429-151">toodo this using hello previous sample, change `$content = fopen("c:\myfile.txt", "r");` too`$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="04429-152">Liste hello BLOB'ları bir kapsayıcıda</span><span class="sxs-lookup"><span data-stu-id="04429-152">List hello blobs in a container</span></span>
<span data-ttu-id="04429-153">toolist hello BLOB'ları bir kapsayıcıda kullanmak hello **BlobRestProxy -> listBlobs** yöntemi ile bir **foreach** tooloop hello sonucundan döngü.</span><span class="sxs-lookup"><span data-stu-id="04429-153">toolist hello blobs in a container, use hello **BlobRestProxy->listBlobs** method with a **foreach** loop tooloop through hello result.</span></span> <span data-ttu-id="04429-154">Merhaba aşağıdaki kod bir kapsayıcıda çıktı olarak her bir blob hello adını görüntüler ve kendi URI toohello tarayıcı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="04429-154">hello following code displays hello name of each blob as output in a container and displays its URI toohello browser.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="04429-155">Blob indirme</span><span class="sxs-lookup"><span data-stu-id="04429-155">Download a blob</span></span>
<span data-ttu-id="04429-156">toodownload bir blob çağrısı hello **BlobRestProxy -> getBlob** yöntemi sonra çağrı hello **getContentStream** hello kaynaklanan yöntemi **GetBlobResult** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="04429-156">toodownload a blob, call hello **BlobRestProxy->getBlob** method, then call hello **getContentStream** method on hello resulting **GetBlobResult** object.</span></span>

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

<span data-ttu-id="04429-157">Yukarıdaki bu hello örnek bir akış kaynağı (Merhaba, varsayılan davranıştır) olarak bir blob alır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="04429-157">Note that hello example above gets a blob as a stream resource (hello default behavior).</span></span> <span data-ttu-id="04429-158">Ancak, hello kullanabilirsiniz [akış\_almak\_içeriği] [ stream-get-contents] işlevi tooconvert hello akış tooa dizesi döndürdü.</span><span class="sxs-lookup"><span data-stu-id="04429-158">However, you can use hello [stream\_get\_contents][stream-get-contents] function tooconvert hello returned stream tooa string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="04429-159">Blob silme</span><span class="sxs-lookup"><span data-stu-id="04429-159">Delete a blob</span></span>
<span data-ttu-id="04429-160">toodelete bir blob geçirmek hello kapsayıcı adı hem de blob adı çok**BlobRestProxy -> deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="04429-160">toodelete a blob, pass hello container name and blob name too**BlobRestProxy->deleteBlob**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="04429-161">Bir blob kapsayıcısından silin</span><span class="sxs-lookup"><span data-stu-id="04429-161">Delete a blob container</span></span>
<span data-ttu-id="04429-162">Son olarak, bir blob kapsayıcısını toodelete geçirmek hello kapsayıcı adı çok**BlobRestProxy -> deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="04429-162">Finally, toodelete a blob container, pass hello container name too**BlobRestProxy->deleteContainer**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="04429-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="04429-163">Next steps</span></span>
<span data-ttu-id="04429-164">Hello Azure blob hizmeti hello temellerini öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin.</span><span class="sxs-lookup"><span data-stu-id="04429-164">Now that you've learned hello basics of hello Azure blob service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="04429-165">Merhaba ziyaret [Azure depolama ekibi blogu](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="04429-165">Visit hello [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="04429-166">Merhaba bkz [PHP blok blobu örnek](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="04429-166">See hello [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="04429-167">Merhaba bkz [PHP sayfa blob örnek](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="04429-167">See hello [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="04429-168">Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="04429-168">Transfer data with hello AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

<span data-ttu-id="04429-169">Daha fazla bilgi için hello Ayrıca bkz. [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="04429-169">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
