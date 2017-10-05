---
title: Php'den BLOB storage (nesne depolama) kullanma | Microsoft Docs
description: "Azure Blob Storage (nesne depolama) ile bulutta yapılandırılmamış veri depolayın."
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
ms.openlocfilehash: 2c356d7faafa8ef4591087b5b1f949b9374732be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-php"></a><span data-ttu-id="a6432-103">Php'den BLOB storage kullanma</span><span class="sxs-lookup"><span data-stu-id="a6432-103">How to use blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="a6432-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a6432-104">Overview</span></span>
<span data-ttu-id="a6432-105">Azure Blob Storage, bulutta nesne/blob olarak yapılandırılmamış veri depolayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="a6432-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="a6432-106">Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="a6432-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="a6432-107">Blob Storage aynı zamanda nesne depolama olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="a6432-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="a6432-108">Bu kılavuz Azure blob hizmeti kullanılarak yaygın senaryolar gerçekleştirme gösterir.</span><span class="sxs-lookup"><span data-stu-id="a6432-108">This guide shows you how to perform common scenarios using the Azure blob service.</span></span> <span data-ttu-id="a6432-109">PHP ve kullanım örnekleri yazılır [PHP için Azure SDK][download].</span><span class="sxs-lookup"><span data-stu-id="a6432-109">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="a6432-110">Kapsamdaki senaryolar dahil **karşıya**, **listeleme**, **indirme**, ve **silme** BLOB'lar.</span><span class="sxs-lookup"><span data-stu-id="a6432-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="a6432-111">BLOB'ları hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="a6432-111">For more information on blobs, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="a6432-112">PHP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a6432-112">Create a PHP application</span></span>
<span data-ttu-id="a6432-113">Azure blob hizmete erişen bir PHP uygulaması oluşturmak için yalnızca Azure SDK'sındaki sınıfların PHP'nin için kodunuzu içinde başvuran gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="a6432-113">The only requirement for creating a PHP application that accesses the Azure blob service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="a6432-114">Not Defteri dahil olmak üzere uygulamanızı oluşturmak için tüm geliştirme araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a6432-114">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="a6432-115">Bu kılavuzda, bir PHP uygulamasının içinde yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir hizmet özelliklerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6432-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="a6432-116">Azure istemci kitaplıkları Al</span><span class="sxs-lookup"><span data-stu-id="a6432-116">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-blob-service"></a><span data-ttu-id="a6432-117">Blob hizmetine erişmek için uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a6432-117">Configure your application to access the blob service</span></span>
<span data-ttu-id="a6432-118">Azure blob hizmeti API'ları kullanmak için aktarmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a6432-118">To use the Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="a6432-119">Otomatik Yükleyiciden kullanarak dosya başvuru [require_once] deyimi, ve</span><span class="sxs-lookup"><span data-stu-id="a6432-119">Reference the autoloader file using the [require_once] statement, and</span></span>
2. <span data-ttu-id="a6432-120">Kullanabileceğinize sınıfları başvuru.</span><span class="sxs-lookup"><span data-stu-id="a6432-120">Reference any classes you might use.</span></span>

<span data-ttu-id="a6432-121">Aşağıdaki örnek otomatik Yükleyiciden dosya ve başvuru dahil gösterilmektedir **ServicesBuilder** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="a6432-121">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="a6432-122">Bu makaledeki örneklerde oluşturucu aracılığıyla Azure için PHP istemci kitaplıkları yüklü olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="a6432-122">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="a6432-123">Başvuruda bulunmanız kitaplıklarını el ile yüklediyseniz, `WindowsAzure.php` otomatik yükleyici dosyası.</span><span class="sxs-lookup"><span data-stu-id="a6432-123">If you installed the libraries manually, you need to reference the `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="a6432-124">Aşağıdaki örneklerde `require_once` deyimi her zaman gösterilecek, ancak yalnızca örnek yürütmek gerekli sınıfları başvurulur.</span><span class="sxs-lookup"><span data-stu-id="a6432-124">In the examples below, the `require_once` statement will be shown always, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="a6432-125">Bir Azure depolama bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="a6432-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="a6432-126">Bir Azure blob hizmeti istemcisi örneği oluşturmak için öncelikle geçerli bir bağlantı dizesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6432-126">To instantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="a6432-127">Blob hizmeti bağlantı dizesini biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="a6432-127">The format for the blob service connection string is:</span></span>

<span data-ttu-id="a6432-128">Canlı hizmetine erişmek için:</span><span class="sxs-lookup"><span data-stu-id="a6432-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="a6432-129">Depolama öykünücüsü erişmek için:</span><span class="sxs-lookup"><span data-stu-id="a6432-129">For accessing the storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="a6432-130">Herhangi bir Azure hizmeti istemcisi oluşturmak için kullanmanız gerekir **ServicesBuilder** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="a6432-130">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="a6432-131">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a6432-131">You can:</span></span>

* <span data-ttu-id="a6432-132">doğrudan bağlantı dizesi geçirin veya</span><span class="sxs-lookup"><span data-stu-id="a6432-132">Pass the connection string directly to it or</span></span>
* <span data-ttu-id="a6432-133">kullanmak **CloudConfigurationManager (CCM)** bağlantı dizesi için dış kaynaklardan denetlemek için:</span><span class="sxs-lookup"><span data-stu-id="a6432-133">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="a6432-134">Varsayılan olarak, bir dış kaynak - ortam değişkenleri için destek ile gelir.</span><span class="sxs-lookup"><span data-stu-id="a6432-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="a6432-135">Genişleterek yeni kaynakları ekleyebilirsiniz **ConnectionStringSource** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="a6432-135">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="a6432-136">Burada özetlenen örnekler için bağlantı dizesi doğrudan geçirilir.</span><span class="sxs-lookup"><span data-stu-id="a6432-136">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="a6432-137">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a6432-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="a6432-138">A **BlobRestProxy** nesnesi ile bir blob kapsayıcı oluşturun olanak tanır **createContainer** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a6432-138">A **BlobRestProxy** object lets you create a blob container with the **createContainer** method.</span></span> <span data-ttu-id="a6432-139">Bir kapsayıcı oluştururken, kapsayıcı seçeneklerini ayarlayabilirsiniz, ancak bunun nedenle gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="a6432-139">When creating a container, you can set options on the container, but doing so is not required.</span></span> <span data-ttu-id="a6432-140">(Aşağıdaki örnek kapsayıcı erişim denetim listesi (ACL) ve kapsayıcı meta verileri nasıl ayarlanacağını gösterir.)</span><span class="sxs-lookup"><span data-stu-id="a6432-140">(The example below shows how to set the container access control list (ACL) and container metadata.)</span></span>

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
// proxys can enumerate blobs within the container via anonymous
// request, but cannot enumerate containers within the storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within the container via
// anonymous request.
// If this value is not specified in the request, container data is
// private to the account owner.
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

<span data-ttu-id="a6432-141">Çağırma **setPublicAccess (PublicAccessType::CONTAINER\_ve\_BLOB'lar)** kapsayıcı ve blob verilerini anonim istekler aracılığıyla erişilebilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="a6432-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes the container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="a6432-142">Çağırma **setPublicAccess(PublicAccessType::BLOBS_ONLY)** yalnızca blob veri anonim istekler erişilebilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="a6432-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="a6432-143">Kapsayıcı ACL'ler hakkında daha fazla bilgi için bkz: [kümesi kapsayıcı ACL (REST API'si)][container-acl].</span><span class="sxs-lookup"><span data-stu-id="a6432-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="a6432-144">Blob hizmeti hata kodları hakkında daha fazla bilgi için bkz: [Blob hizmeti hata kodları][error-codes].</span><span class="sxs-lookup"><span data-stu-id="a6432-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="a6432-145">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="a6432-145">Upload a blob into a container</span></span>
<span data-ttu-id="a6432-146">Bir BLOB dosya karşıya yüklemek için kullanmak **BlobRestProxy -> createBlockBlob** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a6432-146">To upload a file as a blob, use the **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="a6432-147">Bu işlem mevcut değil veya varsa üzerine yazar blob oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a6432-147">This operation creates the blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="a6432-148">Aşağıdaki kod örneği kapsayıcısı zaten oluşturulmuş ve kullandığı varsayar [fopen] [ fopen] dosyasını bir akış olarak açın.</span><span class="sxs-lookup"><span data-stu-id="a6432-148">The code example below assumes that the container has already been created and uses [fopen][fopen] to open the file as a stream.</span></span>

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

<span data-ttu-id="a6432-149">Önceki örnek bir akış olarak bir blob'u karşıya unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a6432-149">Note that the previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="a6432-150">Ancak, bir blob ayrıca bir dize kullanmak, örneğin, yüklenebilir [dosya\_almak\_içeriği] [ file_get_contents] işlevi.</span><span class="sxs-lookup"><span data-stu-id="a6432-150">However, a blob can also be uploaded as a string using, for example, the [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="a6432-151">Önceki örneği kullanarak bunu değiştirmek `$content = fopen("c:\myfile.txt", "r");` için `$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="a6432-151">To do this using the previous sample, change `$content = fopen("c:\myfile.txt", "r");` to `$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="a6432-152">Blob’ları bir kapsayıcıda listeleme</span><span class="sxs-lookup"><span data-stu-id="a6432-152">List the blobs in a container</span></span>
<span data-ttu-id="a6432-153">BLOB'ları bir kapsayıcıda listelemek için kullanın **BlobRestProxy -> listBlobs** yöntemi ile bir **foreach** döngü için döngü sonucu.</span><span class="sxs-lookup"><span data-stu-id="a6432-153">To list the blobs in a container, use the **BlobRestProxy->listBlobs** method with a **foreach** loop to loop through the result.</span></span> <span data-ttu-id="a6432-154">Aşağıdaki kod bir kapsayıcıda çıktı olarak her bir blob adını görüntüler ve tarayıcıya URI'sini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a6432-154">The following code displays the name of each blob as output in a container and displays its URI to the browser.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="a6432-155">Blob indirme</span><span class="sxs-lookup"><span data-stu-id="a6432-155">Download a blob</span></span>
<span data-ttu-id="a6432-156">Bir blob indirmek için arama **BlobRestProxy -> getBlob** yöntemi,'ı çağırın **getContentStream** elde edilen yöntemi **GetBlobResult** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="a6432-156">To download a blob, call the **BlobRestProxy->getBlob** method, then call the **getContentStream** method on the resulting **GetBlobResult** object.</span></span>

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

<span data-ttu-id="a6432-157">Yukarıdaki örnekte bir akış kaynağı (varsayılan davranış) olarak bir blob alır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a6432-157">Note that the example above gets a blob as a stream resource (the default behavior).</span></span> <span data-ttu-id="a6432-158">Ancak, kullanabileceğiniz [akış\_almak\_içeriği] [ stream-get-contents] döndürülen akışa bir dizeye dönüştürmek için işlevi.</span><span class="sxs-lookup"><span data-stu-id="a6432-158">However, you can use the [stream\_get\_contents][stream-get-contents] function to convert the returned stream to a string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="a6432-159">Blob silme</span><span class="sxs-lookup"><span data-stu-id="a6432-159">Delete a blob</span></span>
<span data-ttu-id="a6432-160">Bir blobu silmek için blob adını ve kapsayıcı adı geçirmek **BlobRestProxy -> deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="a6432-160">To delete a blob, pass the container name and blob name to **BlobRestProxy->deleteBlob**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="a6432-161">Bir blob kapsayıcısından silin</span><span class="sxs-lookup"><span data-stu-id="a6432-161">Delete a blob container</span></span>
<span data-ttu-id="a6432-162">Son olarak, bir blob kapsayıcısını silmek için kapsayıcı adına geçirmek **BlobRestProxy -> deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="a6432-162">Finally, to delete a blob container, pass the container name to **BlobRestProxy->deleteContainer**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a6432-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a6432-163">Next steps</span></span>
<span data-ttu-id="a6432-164">Artık Azure blob hizmeti temel bilgileri öğrendiğinize göre daha karmaşık depolama görevleri hakkında bilgi edinmek için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="a6432-164">Now that you've learned the basics of the Azure blob service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="a6432-165">Ziyaret [Azure depolama ekibi blogu](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="a6432-165">Visit the [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="a6432-166">Bkz: [PHP blok blobu örnek](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="a6432-166">See the [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="a6432-167">Bkz: [PHP sayfa blob örnek](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="a6432-167">See the [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="a6432-168">AzCopy Komut Satırı Yardımcı Programı ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="a6432-168">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

<span data-ttu-id="a6432-169">Daha fazla bilgi için Ayrıca bkz. [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="a6432-169">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
<span data-ttu-id="a6432-170">[require_once]: http://php.net/require_once</span><span class="sxs-lookup"><span data-stu-id="a6432-170">[require_once]: http://php.net/require_once</span></span>
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
