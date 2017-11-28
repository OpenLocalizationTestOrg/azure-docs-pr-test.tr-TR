---
title: aaaHow toouse PHP'den table storage ' | Microsoft Docs
description: "Nasıl toouse PHP toocreate tablo hizmetinden hello ve tablo ve ekleme, silme ve sorgu hello tablosu silmek öğrenin."
services: storage
documentationcenter: php
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 1e1036118e208280b4c205da7d7eea61e79359c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-php"></a><span data-ttu-id="9307c-103">Nasıl toouse tablo php'den depolama</span><span class="sxs-lookup"><span data-stu-id="9307c-103">How toouse table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="9307c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9307c-104">Overview</span></span>
<span data-ttu-id="9307c-105">Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure Table hizmet hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="9307c-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="9307c-106">Merhaba örnekler PHP ile yazılmıştır ve hello kullan [PHP için Azure SDK][download].</span><span class="sxs-lookup"><span data-stu-id="9307c-106">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="9307c-107">Merhaba kapsanan senaryolar dahil **oluşturma ve bir tablo silme ve ekleme, silme ve bir tablo varlıkları sorgulama**.</span><span class="sxs-lookup"><span data-stu-id="9307c-107">hello scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="9307c-108">Merhaba hello Azure tablo hizmeti hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="9307c-108">For more information on hello Azure Table service, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="9307c-109">PHP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="9307c-109">Create a PHP application</span></span>
<span data-ttu-id="9307c-110">Merhaba hello Azure Table hizmete erişen bir PHP uygulaması oluşturmaya yönelik gereksinim, yalnızca hello hello Azure SDK sınıfları, PHP'nin için kodunuzu içinde başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="9307c-110">hello only requirement for creating a PHP application that accesses hello Azure Table service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="9307c-111">Uygulamanızın, Not Defteri dahil olmak üzere tüm geliştirme araçları toocreate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9307c-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="9307c-112">Bu kılavuzda, bir PHP uygulamanızda yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir tablo hizmet özelliklerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9307c-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="9307c-113">Hello Azure istemci kitaplıkları Al</span><span class="sxs-lookup"><span data-stu-id="9307c-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a><span data-ttu-id="9307c-114">Uygulama tooaccess hello tablo hizmetini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9307c-114">Configure your application tooaccess hello Table service</span></span>
<span data-ttu-id="9307c-115">toouse hello Azure tablo hizmeti API'leri, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9307c-115">toouse hello Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="9307c-116">Hello kullanarak başvuru hello otomatik yükleyici dosyasını [require_once] [ require_once] deyimi, ve</span><span class="sxs-lookup"><span data-stu-id="9307c-116">Reference hello autoloader file using hello [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="9307c-117">Kullanabileceğinize sınıfları başvuru.</span><span class="sxs-lookup"><span data-stu-id="9307c-117">Reference any classes you might use.</span></span>

<span data-ttu-id="9307c-118">Merhaba aşağıdaki örnekte nasıl tooinclude hello otomatik Yükleyiciden dosya ve başvuru hello gösterir **ServicesBuilder** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9307c-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="9307c-119">Bu makalede Hello örnekler hello oluşturucu aracılığıyla Azure için PHP istemci kitaplıkları yüklü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="9307c-119">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="9307c-120">Merhaba kitaplıklarını el ile yüklediyseniz tooreference hello gerekir <code>WindowsAzure.php</code> otomatik yükleyici dosyası.</span><span class="sxs-lookup"><span data-stu-id="9307c-120">If you installed hello libraries manually, you need tooreference hello <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="9307c-121">Merhaba aşağıdaki örnekte, hello `require_once` deyimi her zaman gösterilir, ancak yalnızca hello sınıfları hello örnek tooexecute için gereken başvuru.</span><span class="sxs-lookup"><span data-stu-id="9307c-121">In hello examples below, hello `require_once` statement is always shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="9307c-122">Bir Azure depolama bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="9307c-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="9307c-123">tooinstantiate Azure tablo hizmeti istemcisi, öncelikle geçerli bir bağlantı dizesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9307c-123">tooinstantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="9307c-124">Merhaba tablo hizmeti bağlantı dizesini Hello biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="9307c-124">hello format for hello Table service connection string is:</span></span>

<span data-ttu-id="9307c-125">Canlı hizmetine erişmek için:</span><span class="sxs-lookup"><span data-stu-id="9307c-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="9307c-126">Merhaba öykünücüsü depolama erişmek için:</span><span class="sxs-lookup"><span data-stu-id="9307c-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="9307c-127">toocreate herhangi bir Azure hizmeti istemci toouse hello gereksinim **ServicesBuilder** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9307c-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="9307c-128">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9307c-128">You can:</span></span>

* <span data-ttu-id="9307c-129">Merhaba bağlantı geçirmek doğrudan tooit dize veya</span><span class="sxs-lookup"><span data-stu-id="9307c-129">pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="9307c-130">Kullanım hello **CloudConfigurationManager (CCM)** toocheck birden çok dış kaynaklardan hello bağlantı dizesi:</span><span class="sxs-lookup"><span data-stu-id="9307c-130">use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="9307c-131">bir dış kaynak - ortam değişkenleri için destek ile birlikte varsayılan olarak,</span><span class="sxs-lookup"><span data-stu-id="9307c-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="9307c-132">Merhaba genişleterek yeni kaynakları ekleyebilirsiniz **ConnectionStringSource** sınıfı</span><span class="sxs-lookup"><span data-stu-id="9307c-132">you can add new sources by extending hello **ConnectionStringSource** class</span></span>

<span data-ttu-id="9307c-133">Burada özetlenen hello örnekler için başlangıç bağlantı dizesi doğrudan geçirilir.</span><span class="sxs-lookup"><span data-stu-id="9307c-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="9307c-134">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="9307c-134">Create a table</span></span>
<span data-ttu-id="9307c-135">A **TableRestProxy** nesnesi ile Merhaba tablosu oluşturma olanak tanır **createTable** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9307c-135">A **TableRestProxy** object lets you create a table with hello **createTable** method.</span></span> <span data-ttu-id="9307c-136">Bir tablo oluştururken hello tablo hizmeti zaman aşımı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9307c-136">When creating a table, you can set hello Table service timeout.</span></span> <span data-ttu-id="9307c-137">(Merhaba tablo hizmeti zaman aşımı hakkında daha fazla bilgi için bkz: [ayarı zaman aşımları tablo hizmeti işlemleri için][table-service-timeouts].)</span><span class="sxs-lookup"><span data-stu-id="9307c-137">(For more information about hello Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Create table.
    $tableRestProxy->createTable("mytable");
}
catch(ServiceException $e){
    $code = $e->getCode();
    $error_message = $e->getMessage();
    // Handle exception based on error codes and messages.
    // Error codes and messages can be found here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
}
```

<span data-ttu-id="9307c-138">Tablo adları kısıtlamaları hakkında bilgi için bkz: [anlama hello tablo hizmeti veri modelini][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="9307c-138">For information about restrictions on table names, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="9307c-139">Bir varlık tooa tablo ekleme</span><span class="sxs-lookup"><span data-stu-id="9307c-139">Add an entity tooa table</span></span>
<span data-ttu-id="9307c-140">tooadd bir varlık tooa tablo oluşturma yeni bir **varlık** nesne ve çok geçirin**TableRestProxy -> insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="9307c-140">tooadd an entity tooa table, create a new **Entity** object and pass it too**TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="9307c-141">Bir varlık oluşturduğunuzda, belirtmeniz gerektiğini unutmayın bir `PartitionKey` ve `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="9307c-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="9307c-142">Bunlar hello bir varlık için benzersiz tanımlayıcı ve çok diğer varlık özellikleri daha hızlı sorgulanabilir değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="9307c-142">These are hello unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="9307c-143">Merhaba sistemini kullanan `PartitionKey` tooautomatically çok sayıda depolama düğümleri Merhaba tablonun varlıklar dağıtın.</span><span class="sxs-lookup"><span data-stu-id="9307c-143">hello system uses `PartitionKey` tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="9307c-144">Varlıklarla aynı hello `PartitionKey` hello üzerinde depolanan aynı düğüm.</span><span class="sxs-lookup"><span data-stu-id="9307c-144">Entities with hello same `PartitionKey` are stored on hello same node.</span></span> <span data-ttu-id="9307c-145">(Birden çok varlık aynı düğüm gerçekleştirmek hello üzerinde depolanan işlemleri farklı düğümlere saklanan varlıkları üzerinde daha iyi.) Merhaba `RowKey` bölüm içindeki bir varlığın hello benzersiz kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="9307c-145">(Operations on multiple entities stored on hello same node perform better than on entities stored across different nodes.) hello `RowKey` is hello unique ID of an entity within a partition.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$entity = new Entity();
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity->addProperty("Location", EdmType::STRING, "Home");

try{
    $tableRestProxy->insertEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
}
```

<span data-ttu-id="9307c-146">Tablo özellikleri ve türleri hakkında daha fazla bilgi için bkz: [anlama hello tablo hizmeti veri modelini][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="9307c-146">For information about Table properties and types, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="9307c-147">Merhaba **TableRestProxy** sınıfı varlıkları eklemek için iki alternatif yöntem sunar: **insertOrMergeEntity** ve **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="9307c-147">hello **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="9307c-148">toouse bu yöntemleri oluşturma yeni bir **varlık** ve parametre tooeither yöntemi olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="9307c-148">toouse these methods, create a new **Entity** and pass it as a parameter tooeither method.</span></span> <span data-ttu-id="9307c-149">Henüz yoksa her yöntem hello varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="9307c-149">Each method will insert hello entity if it does not exist.</span></span> <span data-ttu-id="9307c-150">Merhaba varlık zaten varsa, **insertOrMergeEntity** hello özellikleri zaten mevcutsa özellik değerlerini güncelleştirir ve yeni özellikleri ekler Bunlar yoksa while **insertOrReplaceEntity** tamamen var olan bir varlığı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="9307c-150">If hello entity already exists, **insertOrMergeEntity** updates property values if hello properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="9307c-151">örnekte gösterildiği nasıl aşağıdaki hello toouse **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="9307c-151">hello following example shows how toouse **insertOrMergeEntity**.</span></span> <span data-ttu-id="9307c-152">Varsa hello varlıkla `PartitionKey` "tasksSeattle" ve `RowKey` "1" zaten mevcut değil, bu eklenir.</span><span class="sxs-lookup"><span data-stu-id="9307c-152">If hello entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="9307c-153">(Merhaba yukarıdaki örnekte gösterildiği gibi) daha önce eklendiği, ancak hello `DueDate` özelliği güncelleştirilir ve hello `Status` özellik eklenir.</span><span class="sxs-lookup"><span data-stu-id="9307c-153">However, if it has previously been inserted (as shown in hello example above), hello `DueDate` property will be updated, and hello `Status` property will be added.</span></span> <span data-ttu-id="9307c-154">Merhaba `Description` ve `Location` özellikleri de güncelleştirilmiş değerlerle, etkili bir şekilde bırakmak ancak bunları değişmeden.</span><span class="sxs-lookup"><span data-stu-id="9307c-154">hello `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="9307c-155">İkinci bu iki özellik olmayan eklenen hello örnekte gösterildiği gibi ancak hello hedef varlık üzerinde var, mevcut değerlerine değişmeden kalır.</span><span class="sxs-lookup"><span data-stu-id="9307c-155">If these latter two properties were not added as shown in hello example, but existed on hello target entity, their existing values would remain unchanged.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

//Create new entity.
$entity = new Entity();

// PartitionKey and RowKey are required.
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");

// If entity exists, existing properties are updated with new values and
// new properties are added. Missing properties are unchanged.
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified hello DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace hello entity with PartitionKey "tasksSeattle" and RowKey "1".
    $tableRestProxy->insertOrMergeEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="9307c-156">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="9307c-156">Retrieve a single entity</span></span>
<span data-ttu-id="9307c-157">Merhaba **TableRestProxy -> getEntity** yöntemi tooretrieve verir sorgulanırken tarafından tek bir varlık kendi `PartitionKey` ve `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="9307c-157">hello **TableRestProxy->getEntity** method allows you tooretrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="9307c-158">Bölüm anahtarı Hello aşağıdaki örnekte, hello `tasksSeattle` ve satır anahtarını `1` toohello geçirilen **getEntity** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9307c-158">In hello example below, hello partition key `tasksSeattle` and row key `1` are passed toohello **getEntity** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    $result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entity = $result->getEntity();

echo $entity->getPartitionKey().":".$entity->getRowKey();
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="9307c-159">Tüm varlıkları bir bölüme alma</span><span class="sxs-lookup"><span data-stu-id="9307c-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="9307c-160">Varlık sorguları filtreleri kullanarak oluşturulur (daha fazla bilgi için bkz: [sorgulama tabloları ve varlıkları][filters]).</span><span class="sxs-lookup"><span data-stu-id="9307c-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="9307c-161">tooretrieve, bölümdeki tüm varlıklar kullanmak hello filtre "PartitionKey eq *bölüm_adı*".</span><span class="sxs-lookup"><span data-stu-id="9307c-161">tooretrieve all entities in partition, use hello filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="9307c-162">örnekte gösterildiği nasıl aşağıdaki hello tooretrieve hello alanındaki tüm varlıklara `tasksSeattle` filtre toohello geçirerek bölüm **queryEntities** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9307c-162">hello following example shows how tooretrieve all entities in hello `tasksSeattle` partition by passing a filter toohello **queryEntities** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "PartitionKey eq 'tasksSeattle'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="9307c-163">Bir alt kümesini varlıkları bir bölüme alma</span><span class="sxs-lookup"><span data-stu-id="9307c-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="9307c-164">Merhaba hello önceki örnekte kullanılan aynı düzeni kullanılan tooretrieve tüm varlıkları bir bölüme kısmı olabilir.</span><span class="sxs-lookup"><span data-stu-id="9307c-164">hello same pattern used in hello previous example can be used tooretrieve any subset of entities in a partition.</span></span> <span data-ttu-id="9307c-165">Merhaba alt aldığınız varlıkların kullandığınız hello Filtresi tarafından belirlenir (daha fazla bilgi için bkz: [sorgulama tabloları ve varlıkları][filters]) örnekteki nasıl aşağıdaki .hello toouse filtre tooretrieve belirli bir sahip tüm varlık `Location` ve `DueDate` belirtilen bir tarih küçüktür.</span><span class="sxs-lookup"><span data-stu-id="9307c-165">hello subset of entities you retrieve are determined by hello filter you use (for more information, see [Querying Tables and Entities][filters]).hello following example shows how toouse a filter tooretrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "Location eq 'Office' and DueDate lt '2012-11-5'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="9307c-166">Varlık özellikleri kümesini Al</span><span class="sxs-lookup"><span data-stu-id="9307c-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="9307c-167">Varlık özelliklerinin bir alt sorgu alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9307c-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="9307c-168">Adlı bu teknik *projeksiyon*, bant genişliğini azaltır ve özellikle büyük varlıklar için sorgu performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="9307c-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="9307c-169">bir özellik toobe toospecify alınan, hello özelliği toohello hello adını geçirmek **sorgu addSelectField ->** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9307c-169">toospecify a property toobe retrieved, pass hello name of hello property toohello **Query->addSelectField** method.</span></span> <span data-ttu-id="9307c-170">Bu yöntem birden çok kez tooadd daha fazla özellik çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9307c-170">You can call this method multiple times tooadd more properties.</span></span> <span data-ttu-id="9307c-171">Yürütme sonrasında **TableRestProxy -> queryEntities**, hello döndürülen varlıkları yalnızca seçili hello özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="9307c-171">After executing **TableRestProxy->queryEntities**, hello returned entities will only have hello selected properties.</span></span> <span data-ttu-id="9307c-172">(Tooreturn bir alt tablo varlıkların istiyorsanız, bir filtre sorguları hello yukarıda gösterildiği gibi kullanın.)</span><span class="sxs-lookup"><span data-stu-id="9307c-172">(If you want tooreturn a subset of Table entities, use a filter as shown in hello queries above.)</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\QueryEntitiesOptions;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$options = new QueryEntitiesOptions();
$options->addSelectField("Description");

try    {
    $result = $tableRestProxy->queryEntities("mytable", $options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

// All entities in hello table are returned, regardless of whether
// they have hello Description field.
// toolimit hello results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a><span data-ttu-id="9307c-173">Bir varlığı güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="9307c-173">Update an entity</span></span>
<span data-ttu-id="9307c-174">Var olan bir varlığı hello kullanarak güncelleştirilebilir **varlık setProperty ->** ve **varlık addProperty ->** hello varlık ve ardından arama yöntemlere **TableRestProxy updateEntity ->** .</span><span class="sxs-lookup"><span data-stu-id="9307c-174">An existing entity can be updated by using hello **Entity->setProperty** and **Entity->addProperty** methods on hello entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="9307c-175">Merhaba aşağıdaki örnekte bir varlığı alır, bir özellik değiştirir, başka bir özellik kaldırır ve yeni bir özellik ekler.</span><span class="sxs-lookup"><span data-stu-id="9307c-175">hello following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="9307c-176">Bir özellik değeri çok ayarlayarak kaldırabilirsiniz Not**null**.</span><span class="sxs-lookup"><span data-stu-id="9307c-176">Note that you can remove a property by setting its value too**null**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);

$entity = $result->getEntity();

$entity->setPropertyValue("DueDate", new DateTime()); //Modified DueDate.

$entity->setPropertyValue("Location", null); //Removed Location.

$entity->addProperty("Status", EdmType::STRING, "In progress"); //Added Status.

try    {
    $tableRestProxy->updateEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="9307c-177">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="9307c-177">Delete an entity</span></span>
<span data-ttu-id="9307c-178">bir varlık toodelete geçirmek hello tablo adı ve hello varlığın `PartitionKey` ve `RowKey` toohello **TableRestProxy -> deleteEntity** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9307c-178">toodelete an entity, pass hello table name, and hello entity's `PartitionKey` and `RowKey` toohello **TableRestProxy->deleteEntity** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete entity.
    $tableRestProxy->deleteEntity("mytable", "tasksSeattle", "2");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="9307c-179">Not eşzamanlılık denetleyeceğini hello kullanarak silinmiş bir varlık toobe Merhaba Etag ayarlayabilirsiniz **DeleteEntityOptions -> setEtag** yöntemi ve geçirerek hello **DeleteEntityOptions** çok nesne**deleteEntity** dördüncü bir parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="9307c-179">Note that for concurrency checks, you can set hello Etag for an entity toobe deleted by using hello **DeleteEntityOptions->setEtag** method and passing hello **DeleteEntityOptions** object too**deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="9307c-180">Toplu tablo işlemleri</span><span class="sxs-lookup"><span data-stu-id="9307c-180">Batch table operations</span></span>
<span data-ttu-id="9307c-181">Merhaba **TableRestProxy -> Toplu** yöntemi tooexecute sağlayan birden çok işlem tek bir istek.</span><span class="sxs-lookup"><span data-stu-id="9307c-181">hello **TableRestProxy->batch** method allows you tooexecute multiple operations in a single request.</span></span> <span data-ttu-id="9307c-182">Merhaba burada desen işlemleri çok ekleme içerir**BatchRequest** nesne ve hello geçirme **BatchRequest** toohello nesne **TableRestProxy -> Toplu** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9307c-182">hello pattern here involves adding operations too**BatchRequest** object and then passing hello **BatchRequest** object toohello **TableRestProxy->batch** method.</span></span> <span data-ttu-id="9307c-183">tooadd işlemi tooa **BatchRequest** nesnesi, birden çok kez yöntemler aşağıdaki hello hiçbirini çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9307c-183">tooadd an operation tooa **BatchRequest** object, you can call any of hello following methods multiple times:</span></span>

* <span data-ttu-id="9307c-184">**addInsertEntity** (bir insertEntity işlem ekler)</span><span class="sxs-lookup"><span data-stu-id="9307c-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="9307c-185">**addUpdateEntity** (bir updateEntity işlem ekler)</span><span class="sxs-lookup"><span data-stu-id="9307c-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="9307c-186">**addMergeEntity** (mergeEntity işlemi ekler)</span><span class="sxs-lookup"><span data-stu-id="9307c-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="9307c-187">**addInsertOrReplaceEntity** (bir insertOrReplaceEntity işlem ekler)</span><span class="sxs-lookup"><span data-stu-id="9307c-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="9307c-188">**addInsertOrMergeEntity** (bir insertOrMergeEntity işlem ekler)</span><span class="sxs-lookup"><span data-stu-id="9307c-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="9307c-189">**addDeleteEntity** (deleteEntity işlemi ekler)</span><span class="sxs-lookup"><span data-stu-id="9307c-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="9307c-190">örnekte gösterildiği nasıl aşağıdaki hello tooexecute **insertEntity** ve **deleteEntity** tek bir istek işlemleri:</span><span class="sxs-lookup"><span data-stu-id="9307c-190">hello following example shows how tooexecute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;
use MicrosoftAzure\Storage\Table\Models\BatchOperations;

    // Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

// Create list of batch operation.
$operations = new BatchOperations();

$entity1 = new Entity();
$entity1->setPartitionKey("tasksSeattle");
$entity1->setRowKey("2");
$entity1->addProperty("Description", null, "Clean roof gutters.");
$entity1->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity1->addProperty("Location", EdmType::STRING, "Home");

// Add operation toolist of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation toolist of batch operations.
$operations->addDeleteEntity("mytable", "tasksSeattle", "1");

try    {
    $tableRestProxy->batch($operations);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="9307c-191">Toplu tablo işlemleri hakkında daha fazla bilgi için bkz: [varlık Grup işlemleri gerçekleştirme][entity-group-transactions].</span><span class="sxs-lookup"><span data-stu-id="9307c-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="9307c-192">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="9307c-192">Delete a table</span></span>
<span data-ttu-id="9307c-193">Son olarak, bir tablo toodelete geçirmek hello tablo adı toohello **TableRestProxy -> deleteTable** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9307c-193">Finally, toodelete a table, pass hello table name toohello **TableRestProxy->deleteTable** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete table.
    $tableRestProxy->deleteTable("mytable");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="9307c-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9307c-194">Next steps</span></span>
<span data-ttu-id="9307c-195">Hello Azure tablo hizmeti hello temellerini öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin.</span><span class="sxs-lookup"><span data-stu-id="9307c-195">Now that you've learned hello basics of hello Azure Table service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="9307c-196">[Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="9307c-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="9307c-197">[PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="9307c-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
