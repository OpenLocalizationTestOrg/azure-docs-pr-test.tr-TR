---
title: "aaaHow toouse Ruby Azure tablo depolamasından | Microsoft Docs"
description: "Bir NoSQL veri deposu olan Azure Table storage kullanılarak hello bulutta yapılandırılmış veri depolayın."
services: cosmos-db
documentationcenter: ruby
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 2f9eb5a9160b551d6d1d198869787070c402b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a>Nasıl toouse Ruby Azure tablo depolamasından
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure Table hizmet hello gösterir. Merhaba örnekleri hello Ruby API kullanılarak yazılır. Merhaba kapsanan senaryolar dahil **oluşturma ve bir tablo, ekleme ve bir tablo varlıkları sorgulama**.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Ruby uygulaması oluşturma
Yönergeler için nasıl toocreate Ruby uygulaması bkz [Azure VM'de rayları Web uygulaması üzerinde Söyleniş](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Uygulama tooaccess depolama yapılandırma
Azure Storage toouse, toodownload ve kullanım hello hello depolama REST Hizmetleri ile iletişim kuran bir dizi kolaylık içeren Söyleniş azure paketi gerekir.

### <a name="use-rubygems-tooobtain-hello-package"></a>RubyGems tooobtain hello paketini kullanın
1. Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (UNIX).
2. Tür **gem yükleme azure** hello komut penceresinde tooinstall hello gem ve bağımlılıkları.

### <a name="import-hello-package"></a>Merhaba paketi İçeri Aktar
Sık kullandığınız metin düzenleyiciyi kullanın, hello toouse depolama burada düşündüğünüz Söyleniş dosya toohello üstündeki aşağıdaki hello ekleyin:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Bir Azure depolama bağlantı kurma
Hello azure modülü hello ortam değişkenleri okur **AZURE\_depolama\_hesap** ve **AZURE\_depolama\_erişim\_anahtar**tooconnect tooyour Azure depolama hesabı için bilgi gerekiyor. Bu ortam değişkenleri ayarlanmamışsa, kullanmadan önce hello hesap bilgileri belirtmelisiniz **Azure::TableService** koddan hello ile:

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

## <a name="create-a-table"></a>Bir tablo oluşturma
Merhaba **Azure::TableService** nesnesi, tabloları ve varlıkları ile çalışmanıza olanak sağlar. toocreate bir tablo kullanmak hello **oluşturma\_table()** yöntemi. Merhaba aşağıdaki örnek bir tablo oluşturur veya varsa baskı siparişi hata hello.

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a>Bir varlık tooa tablo ekleme
bir varlık tooadd ilk varlık özelliklerinizi tanımlayan bir karma nesnesi oluşturun. Her varlık için belirtmelisiniz Not bir **PartitionKey** ve **RowKey**. Bunlar hello varlıklarınızı öğesinin benzersiz tanımlayıcıları ve çok diğer özelliklerinizi daha hızlı sorgulanabilir değerlerdir. Azure depolama kullanan **PartitionKey** tooautomatically çok sayıda depolama düğümleri Merhaba tablonun varlıklar dağıtın. Varlıklarla aynı hello **PartitionKey** hello üzerinde depolanan aynı düğüm. Merhaba **RowKey** ait hello bölüm içinde hello varlığın hello benzersiz kimliğidir.

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a>Bir varlığı güncelleştirir
Var olan bir varlığı birden çok yöntemleri kullanılabilir tooupdate vardır:

* **Güncelleştirme\_entity():** var olan bir varlığı değiştirme tarafından güncelleştirin.
* **birleştirme\_entity():** hello varolan varlık kümesine yeni özellik değerlerinin birleştirerek var olan bir varlığı güncelleştirir.
* **INSERT\_veya\_birleştirme\_entity():** değiştirme tarafından var olan bir varlığı güncelleştirir. Hiçbir varlık varsa, yeni bir tane eklenir:
* **INSERT\_veya\_Değiştir\_entity():** hello varolan varlık kümesine yeni özellik değerlerinin birleştirerek var olan bir varlığı güncelleştirir. Hiçbir varlık varsa, yeni bir tane eklenir.

Merhaba aşağıdaki örneği kullanarak bir varlık güncelleştirme gösterir **güncelleştirme\_entity()**:

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

İle **güncelleştirme\_entity()** ve **birleştirme\_entity()**, güncelleştirdiğiniz hello varlık yoksa hello güncelleştirme işlemi başarısız olur. Bu nedenle olup zaten var. bakılmaksızın bir varlık toostore istiyorsanız, bunun yerine kullanmalısınız **Ekle\_veya\_Değiştir\_entity()** veya **Ekle\_veya \_birleştirme\_entity()**.

## <a name="work-with-groups-of-entities"></a>Varlıkları gruplarıyla çalışma
Bazen algılama toosubmit birden çok operations birlikte bir toplu tooensure atomik hello sunucusu tarafından işleme kolaylaştırır. tooaccomplish önce oluşturmanız, bir **toplu** nesnesi ve ardından hello **yürütme\_batch()** yöntemi **TableService**. Merhaba aşağıdaki örneği iki varlık RowKey 2 ve 3 toplu gönderme gösterir. Aynı PartitionKey sahip varlıklar için Works hello yalnızca o BT dikkat edin.

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a>Bir varlık için sorgu
tooquery kullanım hello bir tablodaki bir varlık **almak\_entity()** hello tablo adı geçirerek yöntemi **PartitionKey** ve **RowKey**.

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a>Varlık kümesi sorgulama
tooquery varlıklar bir tabloda bir dizi sorgu karma nesne oluşturma ve hello kullanma **sorgu\_entities()** yöntemi. Merhaba aşağıdaki örnek hello sahip tüm hello varlık alma gösterir aynı **PartitionKey**:

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> Merhaba sonuç kümesi tek bir sorgu tooreturn için çok büyük ise, bir devamlılık belirteci kullanabileceğiniz döndürülecek tooretrieve sonraki sayfalar.
>
>

## <a name="query-a-subset-of-entity-properties"></a>Giriş özellikleri alt kümesi sorgulama
Sorgu tooa tabloya bir varlık birkaç özelliği alabilir. "Projeksiyon" olarak adlandırılan bu teknik bant genişliğini azaltır ve özellikle büyük varlıklar için sorgu performansını iyileştirebilir. Kullanım hello select yan tümcesi ve geçişi hello adlarını toohello istemci toobring istediğiniz özellikleri hello.

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a>Bir varlığı silme
bir varlık toodelete kullanmak hello **silmek\_entity()** yöntemi. Merhaba varlık, hello PartitionKey ve RowKey hello varlığın içeren Merhaba tablonun hello adı toopass gerekir.

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a>Bir tablo silme
toodelete bir tablo kullanmak hello **silmek\_table()** yöntemi ve hello adını geçişinde hello toodelete istediğiniz tablo.

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a>Sonraki adımlar

* [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.
* [Ruby için Azure SDK](http://github.com/WindowsAzure/azure-sdk-for-ruby) github'daki

