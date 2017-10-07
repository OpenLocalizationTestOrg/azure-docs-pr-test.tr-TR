---
title: aaaHow toouse Table storage (C++) | Microsoft Docs
description: "Bir NoSQL veri deposu olan Azure Table storage kullanılarak hello bulutta yapılandırılmış veri depolayın."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 8096fe531427ba4858f7f4cb7f664f941892d1c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a>Nasıl toouse C++ tablo depolamasından
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure Table depolama hizmeti hello gösterir. Merhaba örnekleri C++ ile yazılmış ve hello kullan [C++ için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md). Merhaba kapsanan senaryolar dahil **oluşturma ve bir tablo silme** ve **tablo varlıklarla çalışmaya**.

> [!NOTE]
> Bu kılavuzu hedefleri c++ sürümü 1.0.0 ve yukarıda Azure Storage istemci kitaplığı hello. Merhaba önerilir sürümü aracılığıyla kullanılabilir olan depolama istemci kitaplığı 2.2.0, [NuGet](http://www.nuget.org/packages/wastorage) veya [GitHub](https://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>C++ uygulaması oluşturma
Bu kılavuzda, C++ uygulamasında çalıştırılabilir depolama özelliklerini kullanır. toodo tooinstall ihtiyacınız olacak şekilde, C++ için Azure Storage istemci kitaplığı hello ve Azure aboneliğinizde bir Azure depolama hesabı oluşturun.  

tooinstall hello Azure Storage istemci kitaplığı C++ için hello aşağıdaki yöntemleri kullanabilirsiniz:

* **Linux:** hello üzerinde verilen hello yönergeleri izleyerek [C++ Benioku için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) sayfası.  
* **Windows:** Visual Studio'da sırasıyla **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**. Türü hello şu komutu hello [NuGet Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) ve Enter tuşuna basın.  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-table-storage"></a>Uygulama tooaccess tablo depolama yapılandırma
Deyimleri toohello dosyasının üst kısmında toouse hello Azure depolama API'leri tooaccess tabloları istediğiniz hello C++ Hello şunlar ekleyin:  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Bir Azure depolama bağlantı dizesi ayarlama
Bir Azure storage istemcisi bir depolama bağlantı dizesi toostore uç kullanır ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgileri. Bir istemci uygulaması çalıştırırken hello depolama bağlantı dizesi biçimi aşağıdaki hello olarak sağlamanız gerekir. Depolama hesabı ve hello depolama erişim anahtarınızı hello depolama hesabı için kullanım hello adı listelenen hello [Azure Portal](https://portal.azure.com) hello için *AccountName* ve *AccountKey* değerler. Depolama hesapları ve erişim anahtarları hakkında daha fazla bilgi için bkz: [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md). Bu örnek, bir statik alan toohold hello bağlantı dizesini nasıl bildirebilir gösterir:  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest uygulamanız, yerel Windows tabanlı bilgisayarınızın içinde hello Azure kullanabilirsiniz [depolama öykünücüsü](../storage/common/storage-use-emulator.md) ile Merhaba yüklü [Azure SDK'sı](https://azure.microsoft.com/downloads/). Merhaba depolama öykünücüsü hello Azure Blob, kuyruk ve Tablo Hizmetleri, yerel geliştirme makinenizde kullanılabilir benzetim yapan bir yardımcı programdır. Merhaba aşağıdaki örnek bir statik alan toohold hello bağlantı dizesi tooyour yerel depolama öykünücüsü nasıl bildirebilir gösterir:  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart Azure storage öykünücüsü Merhaba, hello tıklatın **Başlat** düğmesini veya tuşuna hello Windows anahtarı. Yazmaya başlayın **Azure Storage öykünücüsü**ve ardından **Microsoft Azure Storage öykünücüsü** uygulamaları hello listesinden.  

Merhaba aşağıdaki örnekleri bu iki yöntem tooget hello depolama bağlantı dizesi birini kullandığınızı varsayar.  

## <a name="retrieve-your-connection-string"></a>Bağlantı dizesi alma
Merhaba kullanabilirsiniz **cloud_storage_account** toorepresent depolama hesap bilgilerinizi sınıfı. tooretrieve depolama hesap bilgileri hello depolama bağlantı dizesinden, hello parse yöntemi kullanabilirsiniz.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

Ardından, bir başvuru tooa almak **cloud_table_client** tablolar için başvuru nesneleri alabilmenizi sağlar ve varlıkları tablo depolama hizmeti hello içinde depolanan sınıfı. Merhaba aşağıdaki kod oluşturur bir **cloud_table_client** biz alınan yukarıda hello depolama hesabı nesnesini kullanarak nesnesi:  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a>Bir tablo oluşturma
A **cloud_table_client** nesne tabloları ve varlıkları için başvuru nesneleri almak olanak sağlar. Merhaba aşağıdaki kod oluşturur bir **cloud_table_client** nesne ve toocreate yeni bir tablo kullanır.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a>Bir varlık tooa tablo ekleme
tooadd bir varlık tooa tablo oluşturma yeni bir **table_entity** nesne ve çok geçirin**table_operation::insert_entity**. Merhaba aşağıdaki kod hello müşterinin adını hello satır anahtarını ve Soyadı hello bölüm anahtarı olarak kullanır. Birlikte, bir varlığın bölüm ve satır anahtarı benzersiz şekilde hello varlık hello tablosundaki tanımlar. Anahtarları aynı bölüm anahtarına farklı olanlar daha hızlı sorgulanabilir hello varlıklarıyla bölüm, ancak farklı bölüm anahtarlarının kullanılması daha fazla paralel işlem ölçeklenebilirlik sağlar. Daha fazla bilgi için bkz: [Microsoft Azure depolama performans ve ölçeklenebilirlik Yapılacaklar listesi](../storage/common/storage-performance-checklist.md).

Merhaba aşağıdaki kod oluşturur Yeni bir örneğini **table_entity** depolanan bazı müşteri verileri toobe ile. Merhaba kod sonraki çağrılar **table_operation::insert_entity** toocreate bir **table_operation** bir tabloya tooinsert bir varlık nesnesini ve ilişkilendirilmiş bir hello birlikte yeni bir tablo varlık. Son olarak, hello kod çağrıları Hello yürütme yöntemi hello üzerinde **cloud_table** nesnesi. Ve hello yeni **table_operation** hello "Kişiler" tablosuna isteği toohello tablo hizmeti tooinsert hello yeni müşteri varlık gönderir.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a>Toplu işlem varlık yerleştirme
Bir yazma işlemi varlıklar toohello tablo hizmeti toplu ekleyebilirsiniz. Merhaba aşağıdaki kod oluşturur bir **table_batch_operation** nesne ve üç ekleme işlemleri tooit ekler. Her ekleme işlemi, değerlerinin ayarı yeni bir varlık nesnesi oluşturarak eklenir ve hello çağırma hello yöntemi Ekle **table_batch_operation** sahip yeni bir nesne tooassociate hello varlık ekleme işlemi. Ardından, **cloud_table.execute** tooexecute hello işlem çağrılır.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

Toplu işlemler ile ilgili bazı şeyleri toonote:  

* Gerçekleştirebileceğiniz too100 ekleme, silme, birleştirme, Değiştir, tek bir toplu işteki herhangi bir birleşimini ekleme veya birleştirme ve ekleme veya değiştirme işlemleri.  
* Merhaba toplu işlemdeki tek işlem hello olması durumunda toplu işlem bir alma işlemi olabilir.  
* Tek bir toplu işlem tüm varlıkları hello olmalıdır aynı bölüm anahtarı.  
* Sınırlı tooa 4 MB veri yükü toplu işlemdir.  

## <a name="retrieve-all-entities-in-a-partition"></a>Tüm varlıkları bir bölüme alma
tooquery kullanımı bir bölümdeki tüm varlıklar için bir tablo bir **table_query** nesnesi. Merhaba aşağıdaki kod örneğinde 'Smith' hello bölüm anahtarı olduğu varlıklar için bir filtre belirtir. Bu örnekte her varlığın hello sorgu sonuçları toohello konsolunda hello alanlarını yazdırır.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

Bu örnekte Hello sorgu hello filtre ölçütüyle eşleşen tüm hello varlıklar getirir. Büyük tablolar ve toodownload hello tablo varlıkları genellikle ihtiyacınız varsa, verilerinizi Azure storage blobları bunun yerine saklamanızı öneririz.

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Bir bölüme bir grup varlık alma
Tüm hello varlıkları bir bölüme tooquery istemiyorsanız, hello bölüm anahtarı Filtresi ile bir satır anahtarı filtresini birleştirerek bir aralık belirtebilirsiniz. Merhaba aşağıdaki kod örneği iki filtreleri tooget tüm varlıklar 'hello satır anahtarı (ad) burada hello alfabede 'E' den önceki bir harfle başlayan ve hello sorgu sonuçlarını yazdırır Smith' bölümünde kullanır.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a>Tek bir varlık alma
Bir sorgu tooretrieve tek, belirli bir varlığı yazabilirsiniz. Merhaba aşağıdaki kod kullanır **table_operation::retrieve_entity** toospecify hello Müşteri 'Jeff Smith'. Bu yöntem bir koleksiyon yerine yalnızca bir varlık döndürür ve hello döndürülen değer olarak **table_result**. Bir sorguda hem Bölüm hem de satır anahtarını belirterek hello en hızlı yolu tooretrieve hello tablo hizmetinden tek bir varlık olur.  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a>Bir varlığı değiştirme
bir varlık tooreplace hello tablo hizmetinden alın, hello varlık nesnesini değiştirin ve ardından hello Değişiklikleri Kaydet toohello tablo hizmeti yeniden. Merhaba aşağıdaki kod mevcut bir müşterinin telefon numarası ve e-posta adresini değiştirir. Çağırmak yerine **table_operation::insert_entity**, bu kod **table_operation::replace_entity**. Bu, hello işlemi başarısız olur; bu durumda alındığından beri hello varlık hello sunucuda değiştirilmediği sürece bu tam olarak hello sunucuda yerini hello varlık toobe neden olur. Uygulamanızı bir değişikliğin yanlışlıkla üzerine yazılmasını arasında alma hello ve uygulamanızın başka bir bileşen tarafından güncelleştirme yapılan tooprevent hatasıdır. Merhaba bu hatanın uygun işleme tooretrieve hello yeniden varlıktır, (hala geçerli ise) değişiklikleri yapın ve ardından başka bir gerçekleştirin **table_operation::replace_entity** işlemi. Merhaba sonraki bölümde gösterir, nasıl toooverride bu davranışı.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a>Bir varlığı yerleştirme veya değiştirme
**table_operation::replace_entity** hello varlık hello sunucudan alındığından beri değiştirilmişse işlemleri başarısız olur. Ayrıca, ilk sırada hello sunucusundan hello varlık almanız gerekir **table_operation::replace_entity** toobe başarılı. Bazı durumlarda, ancak hello varlık hello sunucuda var ve depolanan hello geçerli değerler ilgisiz tanımadığınız — güncelleştirmeniz tümünün üzerine yazmalıdır. tooaccomplish Bu, kullanacağınız bir **table_operation::insert_or_replace_entity** işlemi. Bu işlem yok veya bu zaman hello yapılan son güncelleştirmeden bağımsız olarak, varsa yerini hello varlık ekler. Aşağıdaki kod örneğine hello hello Jeff Smith için müşteri varlığı hala alınabilir, ancak daha sonra geri toohello sunucu aracılığıyla kaydedilir **table_operation::insert_or_replace_entity**. Toohello varlık hello alma ve güncelleştirme işlemi arasında yapılan güncelleştirmeler üzerine yazılır.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a>Giriş özellikleri alt kümesi sorgulama
Sorgu tooa tabloya bir varlık birkaç özelliği alabilir. Merhaba koddan hello sorguda kullanan hello **table_query::set_select_columns** yöntemi tooreturn yalnızca hello e-posta adreslerini hello tablosundaki varlıklar.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> Bir varlıktaki birkaç özelliği sorgulama tüm özellikleri alınırken değerinden daha verimli bir işlemdir.
> 
> 

## <a name="delete-an-entity"></a>Bir varlığı silme
Bir varlık, onu aldıktan sonra kolayca silebilirsiniz. Merhaba varlık alındıktan sonra arama **table_operation::delete_entity** hello varlık toodelete ile. Merhaba çağrısı **cloud_table.execute** yöntemi. Merhaba aşağıdaki kodu alır ve bir varlık bir bölüm anahtarı "Smith" ve "Jeff" satır anahtarı ile siler.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a>Bir tablo silme
Son olarak, aşağıdaki kod örneğine hello bir depolama hesabından bir tablo siler. Silinmiş bir tablo bir süre hello silmeyi izleyen yeniden oluşturulacak kullanılamaz toobe olacaktır.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a>Sonraki adımlar
Table Storage hello temel bilgileri öğrendiğinize göre Azure Storage hakkında daha fazla bu bağlantılar toolearn izleyin:  

* [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.
* [Nasıl toouse Blob depolama alanından C++](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Nasıl toouse C++ içinden kuyruk depolama](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [C++'ta Azure Storage kaynakları listeler](../storage/common/storage-c-plus-plus-enumeration.md)
* [C++ başvurusu için depolama istemci kitaplığı](http://azure.github.io/azure-storage-cpp)
* [Azure Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/)
