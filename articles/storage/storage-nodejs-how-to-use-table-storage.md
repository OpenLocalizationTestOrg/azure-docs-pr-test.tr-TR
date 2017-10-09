---
title: "aaaHow toouse Node.js Azure tablo depolamasından | Microsoft Docs"
description: "Bir NoSQL veri deposu olan Azure Table storage kullanılarak hello bulutta yapılandırılmış veri depolayın."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 990a71337b806d759d0277a7691712346db7b355
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a>Nasıl toouse Node.js Azure tablo depolamasından
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Genel Bakış
Bu konu, nasıl tooperform yaygın senaryolar hello Azure Table kullanarak bir Node.js uygulamasında hizmet gösterir.

Bu konudaki Hello kod örnekleri, bir Node.js uygulaması zaten olduğunu varsayın. Hakkında bilgi için toocreate Azure, bir Node.js uygulamasında aşağıdaki konulardan birini bakın:

* [Azure App Service'te bir Node.js web uygulaması oluşturma](../app-service-web/app-service-web-get-started-nodejs.md)
* [Derleme ve Webmatrix'i kullanarak bir Node.js web uygulaması tooAzure dağıtma](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* [Derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (Windows PowerShell kullanarak)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a>Uygulama tooaccess Azure Storage yapılandırın
toouse Azure Storage, hello storage REST Hizmetleri ile iletişim kuran bir dizi kolaylık içerir Node.js için Azure depolama SDK'sını hello gerekir.

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a>Düğüm paketi Yöneticisi (NPM) tooinstall hello paketini kullanın
1. Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows) **Terminal** (Mac) veya **Bash** (UNIX) ve uygulamanızı oluşturulduğu toohello klasörüne gidin.
2. Tür **npm yükleme azure depolama** hello komut penceresinde. Merhaba komut çıktısı aşağıdaki örneğine benzer toohello ' dir.

       azure-storage@0.5.0 node_modules\azure-storage
       +-- extend@1.2.1
       +-- xmlbuilder@0.4.3
       +-- mime@1.2.11
       +-- node-uuid@1.4.3
       +-- validator@3.22.2
       +-- underscore@1.4.4
       +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
       +-- xml2js@0.2.7 (sax@0.5.2)
       +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. Merhaba el ile çalıştırabilirsiniz **ls** komutu tooverify, bir **düğümü\_modülleri** klasörü oluşturuldu. Bu klasöre hello bulacaksınız **azure depolama** tooaccess depolama ihtiyacınız hello kitaplıklarını içeren paket.

### <a name="import-hello-package"></a>Merhaba paketi İçeri Aktar
Kod toohello hello üstündeki aşağıdaki hello eklemek **server.js** uygulamanızı dosyasında:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Bir Azure depolama bağlantı kurma
Hello azure modülü hello ortam değişkenleri AZURE okuma\_depolama\_HESABINI ve AZURE\_depolama\_erişim\_anahtar ya da AZURE\_depolama\_bağlantı \_Gerekli bilgileri tooconnect tooyour Azure depolama hesabı için dize. Bu ortam değişkenleri ayarlanmamışsa çağrılırken hello hesap bilgileri belirtmelisiniz **TableService**.

Hello hello ortam değişkenlerini ayarlama örneği için [Azure portal](https://portal.azure.com) bir Azure Web sitesi için bkz: [Node.js web app kullanarak hello Azure tablo hizmeti](../app-service-web/storage-nodejs-use-table-storage-web-site.md).

## <a name="create-a-table"></a>Bir tablo oluşturma
Merhaba aşağıdaki kod oluşturur bir **TableService** nesne ve toocreate yeni bir tablo kullanır. Merhaba üstündeki yakın Hello aşağıdakileri ekleyin **server.js**.

```nodejs
var tableSvc = azure.createTableService();
```

Çağrı çok hello**createTableIfNotExists** zaten yoksa, hello belirtilen adla yeni bir tablo oluşturur. Merhaba aşağıdaki örnekte zaten yoksa, 'mytable' adlı yeni bir tablo oluşturur:

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

Merhaba `result.created` olacaktır `true` yeni bir tablo oluşturduysanız ve `false` hello tablo zaten varsa. Merhaba `response` hello isteğiyle ilgili bilgileri içerir.

### <a name="filters"></a>Filtreler
İsteğe bağlı filtreleme operations kullanılarak gerçekleştirilen uygulanan toooperations olabilir **TableService**. İşlemleri filtreleme içerebilir günlüğe kaydetme, otomatik olarak yeniden deneniyor, vs. Filtreleri hello imza yöntemiyle uygulayan nesneler şunlardır:

```nodejs
function handle (requestOptions, next)
```

Kendi hello isteği seçenekleri ön işleme yaptıktan sonra hello yöntemi toocall "İleri", bir geri çağırma imza aşağıdaki hello ile geçirme gerekir:

```nodejs
function (returnObject, finalCallback, next)
```

Bu geri çağırma ve hello returnObject (Merhaba isteği toohello sunucusundan hello yanıt) işlemden sonra hello geri çağırma tooeither gereken diğer filtreleri işleme toocontinue varsa sonraki çağırma veya yalnızca finalCallback çağırma aksi tooend hello Hizmet başlatma.

Yeniden deneme mantığını uygulaması iki filtre hello Node.js için Azure SDK ile birlikte **ExponentialRetryPolicyFilter** ve **LinearRetryPolicyFilter**. Merhaba aşağıdaki oluşturur bir **TableService** hello kullanan nesneyi **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a>Bir varlık tooa tablo ekleme
bir varlık tooadd ilk varlık özelliklerinizi tanımlayan bir nesne oluşturun. Tüm varlıklar içermesi gereken bir **PartitionKey** ve **RowKey**, hello varlık için benzersiz tanımlayıcı olduğu.

* **PartitionKey** -hello varlık depolanan hello bölüm belirler
* **RowKey** - benzersiz şekilde hello varlığın hello bölüm içinde tanımlar

Her ikisi de **PartitionKey** ve **RowKey** dize değerleri olmalıdır. Daha fazla bilgi için bkz: [anlama hello tablo hizmeti veri modelini](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Merhaba, bir varlığın tanımlama örneği aşağıdadır. Unutmayın **vade tarihi** bir türü olarak tanımlanmış **Edm.DateTime**. Belirten hello türü isteğe bağlıdır ve türleri çıkarımı yapılan belirtilen yoksa.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> Ayrıca bir **zaman damgası** bir varlık eklendiğinde veya, Azure tarafından ayarlanan her kayıt için alan.
>
>

Merhaba de kullanabilirsiniz **entityGenerator** toocreate varlıklar. Merhaba aşağıdaki örnekte oluşturur hello hello kullanarak aynı görev varlık **entityGenerator**.

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

bir varlık tooyour tablosu tooadd geçirmek hello varlık nesnesi toohello **insertEntity** yöntemi.

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

Merhaba işlemi başarılı olursa `result` hello içerecek [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) kayda Merhaba eklenen ve `response` hello işlemiyle ilgili bilgi içerir.

Örnek yanıt:

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> Varsayılan olarak, **insertEntity** hello bir parçası olarak eklenen hello varlık döndürmüyor `response` bilgi. Planı bu varlık üzerinde başka işlemler gerçekleştirmek ya da toocache hello bilgi istiyor hello bir parçası olarak döndürdüğü yararlı toohave olabilir `result`. Etkinleştirerek bunu yapabilirsiniz **echoContent** gibi:
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a>Bir varlığı güncelleştirir
Var olan bir varlığı birden çok yöntemleri kullanılabilir tooupdate vardır:

* **replaceEntity** -değiştirme tarafından var olan bir varlığı güncelleştirir
* **mergeEntity** -hello varolan varlık kümesine yeni özellik değerlerinin birleştirerek var olan bir varlığı güncelleştirir
* **insertOrReplaceEntity** -değiştirme tarafından var olan bir varlığı güncelleştirir. Hiçbir varlık varsa, yeni bir tane eklenir
* **insertOrMergeEntity** -hello varolan içine yeni özellik değerlerinin birleştirerek var olan bir varlığı güncelleştirir. Hiçbir varlık varsa, yeni bir tane eklenir

Merhaba aşağıdaki örneği kullanarak bir varlık güncelleştirme gösterir **replaceEntity**:

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> Güncelleştirilmekte hello veri daha önce başka bir işlem tarafından değiştirilmiş, varsayılan olarak, bir varlık güncelleştirme toosee denetlemez. toosupport eşzamanlı güncelleştirmeleri:
>
> 1. Merhaba güncelleştirilmekte hello nesnesinin ETag alın. Bu hello bir parçası olarak döndürülür `response` tüm ilgili varlık işlemi için ve alınabilir `response['.metadata'].etag`.
> 2. Bir varlık, bir güncelleştirme işlemi gerçekleştirilirken eklediğinizde hello ETag bilgi toohello yeni varlık daha önce alındı. Örneğin:
>
>       entity2 ['.metadata'] .etag currentEtag; =
> 3. Merhaba güncelleştirme işlemini gerçekleştirin. Uygulamanızın, başka bir örneği gibi hello ETag değeri, alınan bu yana hello varlık güncellendiyse bir `error` hello istekte belirtilen hello güncelleştirme koşulu karşılanmadı belirten döndürülür.
>
>

İle **replaceEntity** ve **mergeEntity**, güncelleştirilen hello varlık yoksa hello güncelleştirme işlemi başarısız olur. Bu nedenle olup zaten var. bakılmaksızın bir varlık toostore istiyorsanız, kullanmak **insertOrReplaceEntity** veya **insertOrMergeEntity**.

Merhaba `result` başarılı güncelleştirmesi işlemleri hello içerecek **Etag** Merhaba varlık güncelleştirildi.

## <a name="work-with-groups-of-entities"></a>Varlıkları gruplarıyla çalışma
Bazen algılama toosubmit birden çok operations birlikte bir toplu tooensure atomik hello sunucusu tarafından işleme kolaylaştırır. kullanan, hello tooaccomplish **TableBatch** sınıf toocreate toplu ve sonra hello **executeBatch** yöntemi **TableService** tooperform hello toplu işlemler.

 bir toplu işte iki varlık gönderme aşağıdaki örneğine hello gösterir:

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

Başarılı toplu işlemler için `result` hello toplu her işlem için bilgiler içerir.

### <a name="work-with-batched-operations"></a>Toplu işlemleri ile çalışma
Operations eklenen tooa toplu hello görüntüleyerek sahip denetlenir `operations` özelliği. İşlemlerle yöntemleri toowork aşağıdaki hello de kullanabilirsiniz:

* **Clear** -tüm işlemler bir batch temizler
* **getOperations** -hello toplu işlemindeki bir işlem alır
* **hasOperations** -hello toplu işlemler varsa true değerini döndürür
* **removeOperations** -bir işlem kaldırır
* **boyutu** -döndürür hello hello toplu işlemi sayısı

## <a name="retrieve-an-entity-by-key"></a>Anahtara göre bir varlık alma
belirli bir varlık üzerinde hello dayalı tooreturn **PartitionKey** ve **RowKey**, hello kullan **retrieveEntity** yöntemi.

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

Bu işlem tamamlandıktan sonra `result` hello varlık içerir.

## <a name="query-a-set-of-entities"></a>Varlık kümesi sorgulama
tooquery bir tablo kullanmak hello **TableQuery** toobuild yan tümceleri aşağıdaki hello kullanarak bir sorgu ifadesi yukarı nesnesi:

* **seçin** -hello alanları toobe hello sorgudan döndürülen
* **Burada** - hello nerede yan tümcesi

  * **ve** - bir `and` koşul
  * **veya** - bir `or` koşul
* **üst** -hello öğeleri toofetch sayısı

Merhaba aşağıdaki örnek ilk beş öğelerinin bir PartitionKey ile 'hometasks' hello döndürülecek bir sorgu oluşturur.

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

Bu yana **seçin** , tüm alanları döndürülecek kullanılmaz. Tablo, kullanım tooperform hello sorgusu **queryEntities**. Merhaba aşağıdaki örnekte bu 'mytable' sorgu tooreturn varlıklardan kullanır.

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

Başarılı olursa, `result.entries` hello sorguyla eşleşen varlıkları dizisi içerir. Merhaba sorgu oluşturulamıyor tooreturn ise tüm varlıkları `result.continuationToken` olmayan olacaktır*null* ve üçüncü parametresi, hello olarak kullanılan **queryEntities** tooretrieve daha fazla sonuç. Merhaba ilk sorguyu *null* hello üçüncü parametre için.

### <a name="query-a-subset-of-entity-properties"></a>Giriş özellikleri alt kümesi sorgulama
Bir sorgu tooa tablosu yalnızca birkaç alanları bir varlıktan alabilir.
Bu, bant genişliğini azaltır ve özellikle büyük varlıklar için sorgu performansını iyileştirebilir. Kullanım hello **seçin** hello alanları toobe yan tümcesi ve geçişi hello adlarını döndürdü. Örneğin, hello aşağıdaki sorguyu yalnızca hello döndürülecek **açıklama** ve **vade tarihi** alanları.

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a>Bir varlığı silme
Bir varlığın bölüm ve satır anahtarını kullanarak silebilirsiniz. Bu örnekte, hello **task1** nesnesini içeren hello **RowKey** ve **PartitionKey** silinmiş hello varlık toobe değerleri. Merhaba nesne toohello geçirilen sonra **deleteEntity** yöntemi.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> Öğe, öğe hello tooensure silme başka bir işlem tarafından değiştirilip değiştirilmediğini Etag'ler kullanmayı göz önünde bulundurun. Bkz: [bir varlığı güncelleştirmek](#update-an-entity) Etag'ler kullanma hakkında bilgi için.
>
>

## <a name="delete-a-table"></a>Bir tablo silme
koddan hello bir depolama hesabından bir tablo siler.

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

Merhaba tablo var olup olmadığından emin değilseniz kullanmak **deleteTableIfExists**.

## <a name="use-continuation-tokens"></a>Devamlılık belirteçleri kullanın
İçin devamlılık belirteci tablolar için sonuçları büyük miktarlarda sorgulanırken arayın. Sorgunuz için bir devamlılık belirteci mevcut olduğunda, toorecognize derleme değil, farkına varmazsınız olduğunu kullanılabilir büyük miktarlarda verinin olabilir.

Merhaba sonuçları nesne döndürülen varlık kümeleri sorgulama sırasında bir `continuationToken` böyle bir belirteç bulunduğunda özelliği. Bu işlemi daha sonra bir sorgu toocontinue toomove hello bölüm ve tablo varlıkları arasında gerçekleştirirken da kullanabilirsiniz.

Sorgularken, continuationToken parametresi hello sorgu nesne örneği ile Merhaba geri çağırma işlevi arasında sağlanabilir:

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

Merhaba inceleyin, `continuationToken` nesnesi bulacaksınız özellikler gibi `nextPartitionKey`, `nextRowKey` ve `targetLocation`, tüm hello sonuçları aracılığıyla kullanılan tooiterate olabilir.

Devamlılık örnek hello Azure depolama Node.js bağlantıların github'da içinde yok. Ara `examples/samples/continuationsample.js`.

## <a name="work-with-shared-access-signatures"></a>Paylaşılan erişim imzaları ile çalışma
Paylaşılan erişim imzaları (SAS) depolama hesabı adı veya anahtarları sağlamadan güvenli şekilde tooprovide ayrıntılı erişim tootables ' dir. SAS genellikle bir mobil uygulama tooquery kayıtları izin verme gibi sınırlı kullanılan tooprovide erişim tooyour, verilerdir.

Bir bulut tabanlı hizmeti gibi güvenilir bir uygulama hello kullanarak bir SAS oluşturur **generateSharedAccessSignature** Merhaba, **TableService**, tooan sağlar ve güvenilmeyen veya yarı güvenilir uygulama Mobil uygulama gibi. Hello SAS hello başlangıç tanımlayan bir ilke ve bitiş tarihleri sırasında hangi hello SAS geçerlidir kullanılarak oluşturulan, aynı zamanda erişim düzeyi verilen toohello SAS sahibi hello.

Merhaba aşağıdaki örnek hello SAS sahibi tooquery ('r') hello tablo izin veren yeni bir paylaşılan erişim ilkesi oluşturur ve 100 dakika hello zaman oluşturulduktan sonra süresi dolar.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

Gerekli olduğu gibi aynı zamanda, hello SAS sahibi tooaccess hello tablo çalıştığında sağlanan hello ana bilgisayar bilgilerini olması gerektiğini unutmayın.

ile SAS kullanır hello sonra istemci uygulaması Hello **TableServiceWithSAS** hello tabloda tooperform işlemleri. Aşağıdaki örnek hello toohello tablo bağlanır ve bir sorgu gerçekleştirir.

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

Güncelleştirme veya silme varlıklar tooinsert girişiminde yapılmışsa hello SAS yalnızca sorgu erişimle oluşturulmasının üzerinden, bir hata döndürülür.

### <a name="access-control-lists"></a>Erişim denetim listeleri
Erişim denetimi listesi (ACL) tooset hello erişim ilkesi için bir SAS de kullanabilirsiniz. Birden çok istemcileri tooaccess hello tablo tooallow istiyor, ancak her istemci için farklı erişim ilkeleri sağlar, bu yararlı olur.

Bir ACL her ilkesiyle ilişkili bir Kimliğe sahip bir dizi erişim ilkeleri kullanılarak uygulanır. iki ilke, 'User1' diğeri için 'kullanıcı2' hello aşağıdaki örneğine tanımlar:

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Örnek alır aşağıdaki hello hello hello geçerli ACL'si **hometasks** tablo ve hello yeni ilkeleri kullanılarak ekler **setTableAcl**. Bu yaklaşım sağlar:

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Bir kez hello ACL ayarlayın, hello Kimliği İlkesi için temel bir SAS sonra oluşturabilirsiniz. Aşağıdaki örnek hello 'kullanıcı2' için yeni bir SAS oluşturur:

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için kaynakları aşağıdaki hello bakın.

* [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.
* [Azure depolama SDK'sı düğüm için](https://github.com/Azure/azure-storage-node) github'daki.
* [Node.js Geliştirici Merkezi](/develop/nodejs/)
* [Oluşturma ve bir Node.js uygulaması tooan Azure Web sitesi dağıtma](../app-service-web/app-service-web-get-started-nodejs.md)
