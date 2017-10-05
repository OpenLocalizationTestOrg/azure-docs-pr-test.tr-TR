---
title: Php'den Table storage kullanma | Microsoft Docs
description: "PHP tablo hizmetinden oluşturmak ve bir tablo silmek için nasıl kullanılacağını öğrenin ve ekleme, silme ve tablo sorgu."
services: cosmos-db
documentationcenter: php
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7a48446a11c5c6db0c9f4fdd8872b1e3c12e85c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-table-storage-from-php"></a><span data-ttu-id="849fa-103">Php'den Table storage kullanma</span><span class="sxs-lookup"><span data-stu-id="849fa-103">How to use table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="849fa-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="849fa-104">Overview</span></span>
<span data-ttu-id="849fa-105">Bu kılavuz Azure Table hizmetini kullanarak yaygın senaryolar gerçekleştirme gösterir.</span><span class="sxs-lookup"><span data-stu-id="849fa-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="849fa-106">PHP ve kullanım örnekleri yazılır [PHP için Azure SDK][download].</span><span class="sxs-lookup"><span data-stu-id="849fa-106">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="849fa-107">Kapsamdaki senaryolar dahil **oluşturma ve bir tablo silme ve ekleme, silme ve bir tablo varlıkları sorgulama**.</span><span class="sxs-lookup"><span data-stu-id="849fa-107">The scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="849fa-108">Azure tablo hizmeti hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="849fa-108">For more information on the Azure Table service, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="849fa-109">PHP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="849fa-109">Create a PHP application</span></span>
<span data-ttu-id="849fa-110">Azure Table hizmete erişen bir PHP uygulaması oluşturmak için yalnızca Azure SDK'sındaki sınıfların PHP'nin için kodunuzu içinde başvuran gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="849fa-110">The only requirement for creating a PHP application that accesses the Azure Table service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="849fa-111">Not Defteri dahil olmak üzere uygulamanızı oluşturmak için tüm geliştirme araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="849fa-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="849fa-112">Bu kılavuzda, bir PHP uygulamanızda yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir tablo hizmet özelliklerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="849fa-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="849fa-113">Azure istemci kitaplıkları Al</span><span class="sxs-lookup"><span data-stu-id="849fa-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-table-service"></a><span data-ttu-id="849fa-114">Tablo hizmete erişmek için uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="849fa-114">Configure your application to access the Table service</span></span>
<span data-ttu-id="849fa-115">Azure tablo hizmeti API'ları kullanmak için aktarmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="849fa-115">To use the Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="849fa-116">Otomatik Yükleyiciden kullanarak dosya başvuru [require_once] [ require_once] deyimi, ve</span><span class="sxs-lookup"><span data-stu-id="849fa-116">Reference the autoloader file using the [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="849fa-117">Kullanabileceğinize sınıfları başvuru.</span><span class="sxs-lookup"><span data-stu-id="849fa-117">Reference any classes you might use.</span></span>

<span data-ttu-id="849fa-118">Aşağıdaki örnek otomatik Yükleyiciden dosya ve başvuru dahil gösterilmektedir **ServicesBuilder** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="849fa-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="849fa-119">Bu makaledeki örneklerde oluşturucu aracılığıyla Azure için PHP istemci kitaplıkları yüklü olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="849fa-119">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="849fa-120">Başvuruda bulunmanız kitaplıklarını el ile yüklediyseniz, <code>WindowsAzure.php</code> otomatik yükleyici dosyası.</span><span class="sxs-lookup"><span data-stu-id="849fa-120">If you installed the libraries manually, you need to reference the <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="849fa-121">Aşağıdaki örneklerde `require_once` deyimi her zaman gösterilir, ancak yalnızca örnek yürütmek gerekli sınıfları başvurulur.</span><span class="sxs-lookup"><span data-stu-id="849fa-121">In the examples below, the `require_once` statement is always shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="849fa-122">Bir Azure depolama bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="849fa-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="849fa-123">Azure tablo hizmeti istemcisi örneği oluşturmak için öncelikle geçerli bir bağlantı dizesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="849fa-123">To instantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="849fa-124">Tablo hizmeti bağlantı dizesini biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="849fa-124">The format for the Table service connection string is:</span></span>

<span data-ttu-id="849fa-125">Canlı hizmetine erişmek için:</span><span class="sxs-lookup"><span data-stu-id="849fa-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="849fa-126">Öykünücü depolama erişmek için:</span><span class="sxs-lookup"><span data-stu-id="849fa-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="849fa-127">Herhangi bir Azure hizmeti istemcisi oluşturmak için kullanmanız gerekir **ServicesBuilder** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="849fa-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="849fa-128">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="849fa-128">You can:</span></span>

* <span data-ttu-id="849fa-129">doğrudan bağlantı dizesi geçirin veya</span><span class="sxs-lookup"><span data-stu-id="849fa-129">pass the connection string directly to it or</span></span>
* <span data-ttu-id="849fa-130">kullanmak **CloudConfigurationManager (CCM)** bağlantı dizesi için dış kaynaklardan denetlemek için:</span><span class="sxs-lookup"><span data-stu-id="849fa-130">use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="849fa-131">bir dış kaynak - ortam değişkenleri için destek ile birlikte varsayılan olarak,</span><span class="sxs-lookup"><span data-stu-id="849fa-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="849fa-132">genişleterek yeni kaynakları ekleyebilirsiniz **ConnectionStringSource** sınıfı</span><span class="sxs-lookup"><span data-stu-id="849fa-132">you can add new sources by extending the **ConnectionStringSource** class</span></span>

<span data-ttu-id="849fa-133">Burada özetlenen örnekler için bağlantı dizesi doğrudan geçirilir.</span><span class="sxs-lookup"><span data-stu-id="849fa-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="849fa-134">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="849fa-134">Create a table</span></span>
<span data-ttu-id="849fa-135">A **TableRestProxy** nesne içeren bir tablo oluşturma olanak tanır **createTable** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="849fa-135">A **TableRestProxy** object lets you create a table with the **createTable** method.</span></span> <span data-ttu-id="849fa-136">Bir tablo oluştururken, tablo hizmeti zaman aşımı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="849fa-136">When creating a table, you can set the Table service timeout.</span></span> <span data-ttu-id="849fa-137">(Tablo hizmeti zaman aşımı hakkında daha fazla bilgi için bkz: [ayarı zaman aşımları tablo hizmeti işlemleri için][table-service-timeouts].)</span><span class="sxs-lookup"><span data-stu-id="849fa-137">(For more information about the Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

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

<span data-ttu-id="849fa-138">Tablo adları kısıtlamaları hakkında bilgi için bkz: [tablo hizmeti veri modelini anlama][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="849fa-138">For information about restrictions on table names, see [Understanding the Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="849fa-139">Tabloya bir varlık ekleme</span><span class="sxs-lookup"><span data-stu-id="849fa-139">Add an entity to a table</span></span>
<span data-ttu-id="849fa-140">Bir tabloya bir varlık eklemek için yeni bir oluşturma **varlık** nesne ve ona geçirin **TableRestProxy -> insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="849fa-140">To add an entity to a table, create a new **Entity** object and pass it to **TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="849fa-141">Bir varlık oluşturduğunuzda, belirtmeniz gerektiğini unutmayın bir `PartitionKey` ve `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="849fa-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="849fa-142">Bunlar bir varlık için benzersiz tanımlayıcı ve çok diğer varlık özellikleri daha hızlı sorgulanabilir değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="849fa-142">These are the unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="849fa-143">Sistem kullanır `PartitionKey` tablonun varlıklar birçok depolama düğümleri üzerinde otomatik olarak dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="849fa-143">The system uses `PartitionKey` to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="849fa-144">Aynı varlıkla `PartitionKey` aynı düğümde depolanır.</span><span class="sxs-lookup"><span data-stu-id="849fa-144">Entities with the same `PartitionKey` are stored on the same node.</span></span> <span data-ttu-id="849fa-145">(Birden çok varlık aynı düğümde depolanan işlemleri farklı düğümlere saklanan varlıkları üzerinde daha iyi.) `RowKey` Bir varlığın bölüm içinde benzersiz kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="849fa-145">(Operations on multiple entities stored on the same node perform better than on entities stored across different nodes.) The `RowKey` is the unique ID of an entity within a partition.</span></span>

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
$entity->addProperty("Description", null, "Take out the trash.");
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

<span data-ttu-id="849fa-146">Tablo özellikleri ve türleri hakkında daha fazla bilgi için bkz: [tablo hizmeti veri modelini anlama][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="849fa-146">For information about Table properties and types, see [Understanding the Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="849fa-147">**TableRestProxy** sınıfı varlıkları eklemek için iki alternatif yöntem sunar: **insertOrMergeEntity** ve **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="849fa-147">The **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="849fa-148">Bu yöntemleri kullanmak için yeni bir oluşturma **varlık** ve her iki yöntem için parametre olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="849fa-148">To use these methods, create a new **Entity** and pass it as a parameter to either method.</span></span> <span data-ttu-id="849fa-149">Henüz yoksa her yöntem varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="849fa-149">Each method will insert the entity if it does not exist.</span></span> <span data-ttu-id="849fa-150">Varlık zaten varsa, **insertOrMergeEntity** özellikleri zaten mevcutsa özellik değerlerini güncelleştirir ve yeni özellikleri ekler Bunlar yoksa while **insertOrReplaceEntity** tamamen var olan bir varlığı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="849fa-150">If the entity already exists, **insertOrMergeEntity** updates property values if the properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="849fa-151">Aşağıdaki örnekte nasıl kullanılacağını gösterir **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="849fa-151">The following example shows how to use **insertOrMergeEntity**.</span></span> <span data-ttu-id="849fa-152">Varsa varlıkla `PartitionKey` "tasksSeattle" ve `RowKey` "1" zaten mevcut değil, bu eklenir.</span><span class="sxs-lookup"><span data-stu-id="849fa-152">If the entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="849fa-153">Ancak, (yukarıdaki örnekte gösterildiği gibi) daha önce eklenmiş, `DueDate` özelliği güncelleştirilir ve `Status` özellik eklenir.</span><span class="sxs-lookup"><span data-stu-id="849fa-153">However, if it has previously been inserted (as shown in the example above), the `DueDate` property will be updated, and the `Status` property will be added.</span></span> <span data-ttu-id="849fa-154">`Description` Ve `Location` özellikleri de güncelleştirilmiş değerlerle, etkili bir şekilde bırakmak ancak bunları değişmeden.</span><span class="sxs-lookup"><span data-stu-id="849fa-154">The `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="849fa-155">Bu ikinci iki özellik olmayan eklenen örnekte gösterildiği gibi ancak hedef varlık üzerinde var, mevcut değerlerine değişmeden kalır.</span><span class="sxs-lookup"><span data-stu-id="849fa-155">If these latter two properties were not added as shown in the example, but existed on the target entity, their existing values would remain unchanged.</span></span>

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
$entity->addProperty("Description", null, "Take out the trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified the DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace the entity with PartitionKey "tasksSeattle" and RowKey "1".
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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="849fa-156">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="849fa-156">Retrieve a single entity</span></span>
<span data-ttu-id="849fa-157">**TableRestProxy -> getEntity** yöntemi tek bir varlık için sorgulayarak almanıza olanak tanır, `PartitionKey` ve `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="849fa-157">The **TableRestProxy->getEntity** method allows you to retrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="849fa-158">Bölüm anahtarı aşağıdaki örnekte `tasksSeattle` ve satır anahtarını `1` geçirilen **getEntity** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="849fa-158">In the example below, the partition key `tasksSeattle` and row key `1` are passed to the **getEntity** method.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="849fa-159">Tüm varlıkları bir bölüme alma</span><span class="sxs-lookup"><span data-stu-id="849fa-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="849fa-160">Varlık sorguları filtreleri kullanarak oluşturulur (daha fazla bilgi için bkz: [sorgulama tabloları ve varlıkları][filters]).</span><span class="sxs-lookup"><span data-stu-id="849fa-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="849fa-161">Bölümdeki tüm varlıkları almak için filtre kullanma "PartitionKey eq *bölüm_adı*".</span><span class="sxs-lookup"><span data-stu-id="849fa-161">To retrieve all entities in partition, use the filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="849fa-162">Aşağıdaki örnek, tüm varlıkları almak gösterilmiştir `tasksSeattle` filtre geçirerek bölüm **queryEntities** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="849fa-162">The following example shows how to retrieve all entities in the `tasksSeattle` partition by passing a filter to the **queryEntities** method.</span></span>

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="849fa-163">Bir alt kümesini varlıkları bir bölüme alma</span><span class="sxs-lookup"><span data-stu-id="849fa-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="849fa-164">Önceki örnekte kullanılan aynı düzeni, bunların bir alt kümesini varlıkları bir bölüme almak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="849fa-164">The same pattern used in the previous example can be used to retrieve any subset of entities in a partition.</span></span> <span data-ttu-id="849fa-165">Aldığınız varlıkların alt kullandığınız Filtresi tarafından belirlenir (daha fazla bilgi için bkz: [sorgulama tabloları ve varlıkları][filters]). Aşağıdaki örnekte belirli bir ile tüm varlıkları almak için bir filtre kullanmayı gösterir `Location` ve `DueDate` belirtilen bir tarih küçüktür.</span><span class="sxs-lookup"><span data-stu-id="849fa-165">The subset of entities you retrieve are determined by the filter you use (for more information, see [Querying Tables and Entities][filters]).The following example shows how to use a filter to retrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

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

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="849fa-166">Varlık özellikleri kümesini Al</span><span class="sxs-lookup"><span data-stu-id="849fa-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="849fa-167">Varlık özelliklerinin bir alt sorgu alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="849fa-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="849fa-168">Adlı bu teknik *projeksiyon*, bant genişliğini azaltır ve özellikle büyük varlıklar için sorgu performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="849fa-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="849fa-169">Alınacak bir özelliği belirtmek için özelliğin adını geçirmek **sorgu addSelectField ->** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="849fa-169">To specify a property to be retrieved, pass the name of the property to the **Query->addSelectField** method.</span></span> <span data-ttu-id="849fa-170">Daha fazla özellik eklemek için birden çok kez bu yöntemi çağırın.</span><span class="sxs-lookup"><span data-stu-id="849fa-170">You can call this method multiple times to add more properties.</span></span> <span data-ttu-id="849fa-171">Yürütme sonrasında **TableRestProxy -> queryEntities**, döndürülen varlıkları yalnızca seçilen özellikleri sahip olur.</span><span class="sxs-lookup"><span data-stu-id="849fa-171">After executing **TableRestProxy->queryEntities**, the returned entities will only have the selected properties.</span></span> <span data-ttu-id="849fa-172">(Bir alt tablo varlıkların dönmek istiyorsanız, bir filtre sorguları yukarıda gösterildiği gibi kullanın.)</span><span class="sxs-lookup"><span data-stu-id="849fa-172">(If you want to return a subset of Table entities, use a filter as shown in the queries above.)</span></span>

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

// All entities in the table are returned, regardless of whether
// they have the Description field.
// To limit the results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a><span data-ttu-id="849fa-173">Bir varlığı güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="849fa-173">Update an entity</span></span>
<span data-ttu-id="849fa-174">Var olan bir varlığı kullanarak güncelleştirilebilir **varlık setProperty ->** ve **varlık addProperty ->** varlık ve ardından arama yöntemleri **TableRestProxy -> updateEntity**.</span><span class="sxs-lookup"><span data-stu-id="849fa-174">An existing entity can be updated by using the **Entity->setProperty** and **Entity->addProperty** methods on the entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="849fa-175">Aşağıdaki örnekte bir varlığı alır, bir özelliğini değiştirir, başka bir özellik kaldırır ve yeni bir özellik ekler.</span><span class="sxs-lookup"><span data-stu-id="849fa-175">The following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="849fa-176">Bir özelliğin değerini ayarlayarak kaldırabileceğini unutmayın **null**.</span><span class="sxs-lookup"><span data-stu-id="849fa-176">Note that you can remove a property by setting its value to **null**.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="849fa-177">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="849fa-177">Delete an entity</span></span>
<span data-ttu-id="849fa-178">Bir varlığı silmek için tablo adı ve varlığın geçmesi `PartitionKey` ve `RowKey` için **TableRestProxy -> deleteEntity** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="849fa-178">To delete an entity, pass the table name, and the entity's `PartitionKey` and `RowKey` to the **TableRestProxy->deleteEntity** method.</span></span>

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

<span data-ttu-id="849fa-179">Not eşzamanlılık denetleyeceğini kullanarak silinecek bir varlık için Etag ayarlayabilirsiniz **DeleteEntityOptions -> setEtag** yöntemi ve geçirerek **DeleteEntityOptions** nesnesini **deleteEntity** dördüncü bir parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="849fa-179">Note that for concurrency checks, you can set the Etag for an entity to be deleted by using the **DeleteEntityOptions->setEtag** method and passing the **DeleteEntityOptions** object to **deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="849fa-180">Toplu tablo işlemleri</span><span class="sxs-lookup"><span data-stu-id="849fa-180">Batch table operations</span></span>
<span data-ttu-id="849fa-181">**TableRestProxy -> Toplu** yöntemi birden çok işlem tek bir istekte yürütmesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="849fa-181">The **TableRestProxy->batch** method allows you to execute multiple operations in a single request.</span></span> <span data-ttu-id="849fa-182">Ekleme işlemleri için desen burada içerir **BatchRequest** nesnesi ve ardından geçirme **BatchRequest** nesnesini **TableRestProxy -> Toplu** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="849fa-182">The pattern here involves adding operations to **BatchRequest** object and then passing the **BatchRequest** object to the **TableRestProxy->batch** method.</span></span> <span data-ttu-id="849fa-183">Bir işlem eklemek için bir **BatchRequest** nesne çağırabilirsiniz aşağıdaki yöntemlerden herhangi birini birden çok kez:</span><span class="sxs-lookup"><span data-stu-id="849fa-183">To add an operation to a **BatchRequest** object, you can call any of the following methods multiple times:</span></span>

* <span data-ttu-id="849fa-184">**addInsertEntity** (bir insertEntity işlem ekler)</span><span class="sxs-lookup"><span data-stu-id="849fa-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="849fa-185">**addUpdateEntity** (bir updateEntity işlem ekler)</span><span class="sxs-lookup"><span data-stu-id="849fa-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="849fa-186">**addMergeEntity** (mergeEntity işlemi ekler)</span><span class="sxs-lookup"><span data-stu-id="849fa-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="849fa-187">**addInsertOrReplaceEntity** (bir insertOrReplaceEntity işlem ekler)</span><span class="sxs-lookup"><span data-stu-id="849fa-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="849fa-188">**addInsertOrMergeEntity** (bir insertOrMergeEntity işlem ekler)</span><span class="sxs-lookup"><span data-stu-id="849fa-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="849fa-189">**addDeleteEntity** (deleteEntity işlemi ekler)</span><span class="sxs-lookup"><span data-stu-id="849fa-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="849fa-190">Aşağıdaki örnekte nasıl yürütüleceği gösterilmektedir **insertEntity** ve **deleteEntity** tek bir istek işlemleri:</span><span class="sxs-lookup"><span data-stu-id="849fa-190">The following example shows how to execute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

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

// Add operation to list of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation to list of batch operations.
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

<span data-ttu-id="849fa-191">Toplu tablo işlemleri hakkında daha fazla bilgi için bkz: [varlık Grup işlemleri gerçekleştirme][entity-group-transactions].</span><span class="sxs-lookup"><span data-stu-id="849fa-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="849fa-192">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="849fa-192">Delete a table</span></span>
<span data-ttu-id="849fa-193">Son olarak, bir tabloyu silmek için tablo adını geçirmek **TableRestProxy -> deleteTable** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="849fa-193">Finally, to delete a table, pass the table name to the **TableRestProxy->deleteTable** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="849fa-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="849fa-194">Next steps</span></span>
<span data-ttu-id="849fa-195">Azure tablo hizmetinin öğrendiğinize göre daha karmaşık depolama görevleri hakkında bilgi edinmek için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="849fa-195">Now that you've learned the basics of the Azure Table service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="849fa-196">[Microsoft Azure Depolama Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md), Microsoft’un Windows, macOS ve Linux üzerinde Azure Depolama verileriyle görsel olarak çalışmanızı sağlayan ücretsiz ve tek başına uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="849fa-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="849fa-197">[PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="849fa-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
