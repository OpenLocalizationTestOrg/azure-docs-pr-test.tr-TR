---
title: aaaHow toouse PHP'den table storage ' | Microsoft Docs
description: "Nasıl toouse PHP toocreate tablo hizmetinden hello ve tablo ve ekleme, silme ve sorgu hello tablosu silmek öğrenin."
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
ms.openlocfilehash: 5b7c92221069d1c2a6ca951c06ae8eea8bb8478c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-php"></a>Nasıl toouse tablo php'den depolama
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure Table hizmet hello gösterir. Merhaba örnekler PHP ile yazılmıştır ve hello kullan [PHP için Azure SDK][download]. Merhaba kapsanan senaryolar dahil **oluşturma ve bir tablo silme ve ekleme, silme ve bir tablo varlıkları sorgulama**. Merhaba hello Azure tablo hizmeti hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>PHP uygulaması oluşturma
Merhaba hello Azure Table hizmete erişen bir PHP uygulaması oluşturmaya yönelik gereksinim, yalnızca hello hello Azure SDK sınıfları, PHP'nin için kodunuzu içinde başvuruyor. Uygulamanızın, Not Defteri dahil olmak üzere tüm geliştirme araçları toocreate kullanabilirsiniz.

Bu kılavuzda, bir PHP uygulamanızda yerel olarak veya bir Azure web rolü, çalışan rolü veya Web sitesi içinde çalışan kodu çağrılabilir tablo hizmet özelliklerini kullanın.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure istemci kitaplıkları Al
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a>Uygulama tooaccess hello tablo hizmetini yapılandırma
toouse hello Azure tablo hizmeti API'leri, şunları yapmanız gerekir:

1. Hello kullanarak başvuru hello otomatik yükleyici dosyasını [require_once] [ require_once] deyimi, ve
2. Kullanabileceğinize sınıfları başvuru.

Merhaba aşağıdaki örnekte nasıl tooinclude hello otomatik Yükleyiciden dosya ve başvuru hello gösterir **ServicesBuilder** sınıfı.

> [!NOTE]
> Bu makalede Hello örnekler hello oluşturucu aracılığıyla Azure için PHP istemci kitaplıkları yüklü olduğunu varsayar. Merhaba kitaplıklarını el ile yüklediyseniz tooreference hello gerekir <code>WindowsAzure.php</code> otomatik yükleyici dosyası.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Merhaba aşağıdaki örnekte, hello `require_once` deyimi her zaman gösterilir, ancak yalnızca hello sınıfları hello örnek tooexecute için gereken başvuru.

## <a name="set-up-an-azure-storage-connection"></a>Bir Azure depolama bağlantı kurma
tooinstantiate Azure tablo hizmeti istemcisi, öncelikle geçerli bir bağlantı dizesi olması gerekir. Merhaba tablo hizmeti bağlantı dizesini Hello biçimdedir:

Canlı hizmetine erişmek için:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Merhaba öykünücüsü depolama erişmek için:

```php
UseDevelopmentStorage=true
```

toocreate herhangi bir Azure hizmeti istemci toouse hello gereksinim **ServicesBuilder** sınıfı. Şunları yapabilirsiniz:

* Merhaba bağlantı geçirmek doğrudan tooit dize veya
* Kullanım hello **CloudConfigurationManager (CCM)** toocheck birden çok dış kaynaklardan hello bağlantı dizesi:
  * bir dış kaynak - ortam değişkenleri için destek ile birlikte varsayılan olarak,
  * Merhaba genişleterek yeni kaynakları ekleyebilirsiniz **ConnectionStringSource** sınıfı

Burada özetlenen hello örnekler için başlangıç bağlantı dizesi doğrudan geçirilir.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a>Bir tablo oluşturma
A **TableRestProxy** nesnesi ile Merhaba tablosu oluşturma olanak tanır **createTable** yöntemi. Bir tablo oluştururken hello tablo hizmeti zaman aşımı ayarlayabilirsiniz. (Merhaba tablo hizmeti zaman aşımı hakkında daha fazla bilgi için bkz: [ayarı zaman aşımları tablo hizmeti işlemleri için][table-service-timeouts].)

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

Tablo adları kısıtlamaları hakkında bilgi için bkz: [anlama hello tablo hizmeti veri modelini][table-data-model].

## <a name="add-an-entity-tooa-table"></a>Bir varlık tooa tablo ekleme
tooadd bir varlık tooa tablo oluşturma yeni bir **varlık** nesne ve çok geçirin**TableRestProxy -> insertEntity**. Bir varlık oluşturduğunuzda, belirtmeniz gerektiğini unutmayın bir `PartitionKey` ve `RowKey`. Bunlar hello bir varlık için benzersiz tanımlayıcı ve çok diğer varlık özellikleri daha hızlı sorgulanabilir değerlerdir. Merhaba sistemini kullanan `PartitionKey` tooautomatically çok sayıda depolama düğümleri Merhaba tablonun varlıklar dağıtın. Varlıklarla aynı hello `PartitionKey` hello üzerinde depolanan aynı düğüm. (Birden çok varlık aynı düğüm gerçekleştirmek hello üzerinde depolanan işlemleri farklı düğümlere saklanan varlıkları üzerinde daha iyi.) Merhaba `RowKey` bölüm içindeki bir varlığın hello benzersiz kimliğidir.

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

Tablo özellikleri ve türleri hakkında daha fazla bilgi için bkz: [anlama hello tablo hizmeti veri modelini][table-data-model].

Merhaba **TableRestProxy** sınıfı varlıkları eklemek için iki alternatif yöntem sunar: **insertOrMergeEntity** ve **insertOrReplaceEntity**. toouse bu yöntemleri oluşturma yeni bir **varlık** ve parametre tooeither yöntemi olarak geçirin. Henüz yoksa her yöntem hello varlık ekler. Merhaba varlık zaten varsa, **insertOrMergeEntity** hello özellikleri zaten mevcutsa özellik değerlerini güncelleştirir ve yeni özellikleri ekler Bunlar yoksa while **insertOrReplaceEntity** tamamen var olan bir varlığı değiştirir. örnekte gösterildiği nasıl aşağıdaki hello toouse **insertOrMergeEntity**. Varsa hello varlıkla `PartitionKey` "tasksSeattle" ve `RowKey` "1" zaten mevcut değil, bu eklenir. (Merhaba yukarıdaki örnekte gösterildiği gibi) daha önce eklendiği, ancak hello `DueDate` özelliği güncelleştirilir ve hello `Status` özellik eklenir. Merhaba `Description` ve `Location` özellikleri de güncelleştirilmiş değerlerle, etkili bir şekilde bırakmak ancak bunları değişmeden. İkinci bu iki özellik olmayan eklenen hello örnekte gösterildiği gibi ancak hello hedef varlık üzerinde var, mevcut değerlerine değişmeden kalır.

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

## <a name="retrieve-a-single-entity"></a>Tek bir varlık alma
Merhaba **TableRestProxy -> getEntity** yöntemi tooretrieve verir sorgulanırken tarafından tek bir varlık kendi `PartitionKey` ve `RowKey`. Bölüm anahtarı Hello aşağıdaki örnekte, hello `tasksSeattle` ve satır anahtarını `1` toohello geçirilen **getEntity** yöntemi.

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

## <a name="retrieve-all-entities-in-a-partition"></a>Tüm varlıkları bir bölüme alma
Varlık sorguları filtreleri kullanarak oluşturulur (daha fazla bilgi için bkz: [sorgulama tabloları ve varlıkları][filters]). tooretrieve, bölümdeki tüm varlıklar kullanmak hello filtre "PartitionKey eq *bölüm_adı*". örnekte gösterildiği nasıl aşağıdaki hello tooretrieve hello alanındaki tüm varlıklara `tasksSeattle` filtre toohello geçirerek bölüm **queryEntities** yöntemi.

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a>Bir alt kümesini varlıkları bir bölüme alma
Merhaba hello önceki örnekte kullanılan aynı düzeni kullanılan tooretrieve tüm varlıkları bir bölüme kısmı olabilir. Merhaba alt aldığınız varlıkların kullandığınız hello Filtresi tarafından belirlenir (daha fazla bilgi için bkz: [sorgulama tabloları ve varlıkları][filters]) örnekteki nasıl aşağıdaki .hello toouse filtre tooretrieve belirli bir sahip tüm varlık `Location` ve `DueDate` belirtilen bir tarih küçüktür.

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

## <a name="retrieve-a-subset-of-entity-properties"></a>Varlık özellikleri kümesini Al
Varlık özelliklerinin bir alt sorgu alabilirsiniz. Adlı bu teknik *projeksiyon*, bant genişliğini azaltır ve özellikle büyük varlıklar için sorgu performansını iyileştirebilir. bir özellik toobe toospecify alınan, hello özelliği toohello hello adını geçirmek **sorgu addSelectField ->** yöntemi. Bu yöntem birden çok kez tooadd daha fazla özellik çağırabilirsiniz. Yürütme sonrasında **TableRestProxy -> queryEntities**, hello döndürülen varlıkları yalnızca seçili hello özellikleri vardır. (Tooreturn bir alt tablo varlıkların istiyorsanız, bir filtre sorguları hello yukarıda gösterildiği gibi kullanın.)

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

## <a name="update-an-entity"></a>Bir varlığı güncelleştirir
Var olan bir varlığı hello kullanarak güncelleştirilebilir **varlık setProperty ->** ve **varlık addProperty ->** hello varlık ve ardından arama yöntemlere **TableRestProxy updateEntity ->** . Merhaba aşağıdaki örnekte bir varlığı alır, bir özellik değiştirir, başka bir özellik kaldırır ve yeni bir özellik ekler. Bir özellik değeri çok ayarlayarak kaldırabilirsiniz Not**null**.

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

## <a name="delete-an-entity"></a>Bir varlığı silme
bir varlık toodelete geçirmek hello tablo adı ve hello varlığın `PartitionKey` ve `RowKey` toohello **TableRestProxy -> deleteEntity** yöntemi.

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

Not eşzamanlılık denetleyeceğini hello kullanarak silinmiş bir varlık toobe Merhaba Etag ayarlayabilirsiniz **DeleteEntityOptions -> setEtag** yöntemi ve geçirerek hello **DeleteEntityOptions** çok nesne**deleteEntity** dördüncü bir parametre olarak.

## <a name="batch-table-operations"></a>Toplu tablo işlemleri
Merhaba **TableRestProxy -> Toplu** yöntemi tooexecute sağlayan birden çok işlem tek bir istek. Merhaba burada desen işlemleri çok ekleme içerir**BatchRequest** nesne ve hello geçirme **BatchRequest** toohello nesne **TableRestProxy -> Toplu** yöntemi. tooadd işlemi tooa **BatchRequest** nesnesi, birden çok kez yöntemler aşağıdaki hello hiçbirini çağırabilirsiniz:

* **addInsertEntity** (bir insertEntity işlem ekler)
* **addUpdateEntity** (bir updateEntity işlem ekler)
* **addMergeEntity** (mergeEntity işlemi ekler)
* **addInsertOrReplaceEntity** (bir insertOrReplaceEntity işlem ekler)
* **addInsertOrMergeEntity** (bir insertOrMergeEntity işlem ekler)
* **addDeleteEntity** (deleteEntity işlemi ekler)

örnekte gösterildiği nasıl aşağıdaki hello tooexecute **insertEntity** ve **deleteEntity** tek bir istek işlemleri:

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

Toplu tablo işlemleri hakkında daha fazla bilgi için bkz: [varlık Grup işlemleri gerçekleştirme][entity-group-transactions].

## <a name="delete-a-table"></a>Bir tablo silme
Son olarak, bir tablo toodelete geçirmek hello tablo adı toohello **TableRestProxy -> deleteTable** yöntemi.

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

## <a name="next-steps"></a>Sonraki adımlar
Hello Azure tablo hizmeti hello temellerini öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin.

* [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.

* [PHP Geliştirici Merkezi](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
