---
title: "Azure Cosmos DB aaaExpire verileri toolive süresiyle | Microsoft Docs"
description: "TTL ile Microsoft Azure Cosmos DB hello sistemden bir süre sonra otomatik olarak temizlenir hello özelliği toohave belgeleri sağlar."
services: cosmos-db
documentationcenter: 
keywords: zaman toolive
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a>Zaman toolive ile otomatik olarak Azure Cosmos DB koleksiyonlarda verileri süresi dolacak
Uygulamalar oluşturmak ve çok büyük miktarda veri depolayın. Bu veriler, bazı bilgiler yalnızca sınırlı bir süre için yararlıdır oluşturulan makine olay verileri, günlükler ve kullanıcı oturumu ister. Merhaba uygulaması fazlalık toohello ihtiyaçlarını Hello veri olduktan sonra bu verileri güvenli toopurge olduğundan ve bir uygulamanın hello depolama gereksinimlerini azaltmak.

"Zaman toolive" veya TTL ile Microsoft Azure Cosmos DB hello veritabanından bir süre sonra otomatik olarak temizlenir hello özelliği toohave belgeler sağlar. Merhaba varsayılan süre toolive hello koleksiyon düzeyinde ayarlamak ve bir belge başına temelinde geçersiz kılındı. Bir koleksiyonu varsayılan olarak veya bir belge düzeyinde TTL ayarlandıktan sonra Cosmos DB son değiştirildiği olduğundan, bu süre, saniye sonra mevcut belgeleri otomatik olarak kaldırır.

Hello belgenin en son değiştirildiği zamanı Cosmos DB'de toolive karşı bir uzaklık kullanır. toodo bu hello kullanan `_ts` her belge üzerinde var olan alan. Merhaba _ts UNIX stili dönem zaman damgası temsil eden hello tarih ve saat alanıdır. Merhaba `_ts` alanı her zaman bir belge değiştirildiğinde güncelleştirilir. 

## <a name="ttl-behavior"></a>TTL davranışı
Merhaba TTL özelliği, iki düzeyde - hello koleksiyon düzeyinde ve hello belge düzeyinde TTL özellikleri tarafından denetlenir. Hello değerleri saniye olarak ayarlamak ve hello delta olarak davranılır `_ts` hello belge en son değiştirildiği.

1. DefaultTTL hello koleksiyon için
   
   * Eksik (veya set toonull), belgeler, otomatik olarak silinmez.
   * Varsa ve hello değerdir "-1" = sonsuz – belgeleri varsayılan olarak süresi yok
   * Varsa ve hello değerdir bir numara ("n") – belgelerin süresi dolsun "n" saniye son değişikliğinden sonra
2. TTL hello belgeler için: 
   
   * Özelliği, yalnızca DefaultTTL hello üst koleksiyonu için mevcut olduğunda geçerlidir.
   * Merhaba üst koleksiyon için Hello DefaultTTL değerini geçersiz kılar.

Merhaba belge süresi doldu hemen (`ttl`  +  `_ts` > geçerli sunucu zamanı =), "süresi dolmuş olarak" Merhaba belge olarak işaretlendi. Bu tarihten sonra bu belgeler üzerinde hiçbir işlem izin verilecek ve hello gerçekleştirilen herhangi bir sorgu sonuçlarından bırakılır. Merhaba belgeleri hello sistemde fiziksel olarak silinir ve hello arka planda mümkün daha sonra silinir. Bu kullanılmasına neden değil [istek birimlerine (RUs)](request-units.md) hello koleksiyonu bütçesi.

Merhaba mantığı yukarıda matris aşağıdaki hello gösterilebilir:

|  | DefaultTTL eksik değil hello koleksiyonunda ayarlayın. | DefaultTTL = -1 koleksiyonu | DefaultTTL koleksiyonunda "n" = |
| --- |:--- |:--- |:--- |
| TTL eksik belgesi |Hiçbir şey hello belge ve koleksiyon TTL kavramına sahip olduğundan belge düzeyinde toooverride. |Bu koleksiyonun hiç belgelerde sona erecek. |Bu koleksiyonda hello belgeleri aralığı n sona erdiğinde sona erecek. |
| TTL belgesinde -1 = |Hiçbir şey toooverride hello koleksiyonu tanımlamıyor beri hello belge düzeyinde hello belge kılabilirsiniz DefaultTTL özelliği. TTL belgesinde hello sistem tarafından yorumlanan atanmamış. |Bu koleksiyonun hiç belgelerde sona erecek. |TTL =-1'de bu koleksiyonun Hello belgeyle asla sona erecek. Diğer tüm belgeler "n" aralığından sonra sona erecek. |
| TTL belgesinde n = |Hiçbir şey hello belge düzeyinde toooverride. Bir belge üzerinde TTL hello sistem tarafından yorumlanan kaydetmeyin. |TTL Hello belgeyle = n saniye cinsinden aralık n sonra dolacak. Diğer belgeleri -1 aralığı devralır ve süresi dolmayacak. |TTL Hello belgeyle = n saniye cinsinden aralık n sonra dolacak. Diğer belgeler "n" aralığı hello koleksiyonundan devralır. |

## <a name="configuring-ttl"></a>TTL yapılandırma
Varsayılan olarak, varsayılan olarak tüm Cosmos DB koleksiyonlarında ve tüm belgeleri zaman toolive devre dışıdır.

## <a name="enabling-ttl"></a>TTL etkinleştirme
TTL tooenable bir koleksiyon ya da bir koleksiyon içinde hello belgelerine koleksiyonu tooeither -1 veya sıfır olmayan pozitif bir sayı tooset hello DefaultTTL özelliği gerekir. Varsayılan olarak hello koleksiyonundaki tüm belgeleri sonsuza kadar Canlı ancak hello Cosmos DB hizmeti bu koleksiyon, bu varsayılanı geçersiz belgeler için izlemelidir hello DefaultTTL çok 1 anlamına gelir ayarlama.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a>Bir koleksiyonda varsayılan TTL yapılandırma
Bir koleksiyon düzeyinde toolive bir varsayılan saati mümkün tooconfigure arasındadır. tooset hello TTL hello zaman damgası hello belgenin son değiştirilme sonra bir koleksiyon üzerinde tooprovide hello süre, saniye cinsinden tooexpire gösteren sıfır olmayan pozitif bir sayı hello koleksiyonundaki tüm belgeleri gereken (`_ts`). Veya hello varsayılan çok-toohello koleksiyonunda eklenen tüm belgeleri süresiz olarak varsayılan olarak dinamik gelir 1 ayarlayabilirsiniz.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a>Bir belge TTL ayarı
Ayrıca toosetting varsayılan TTL bir koleksiyonda belirli TTL belge düzeyinde ayarlayabilirsiniz. Bunun yapılması hello varsayılan hello koleksiyonunun geçersiz kılar.

* tooset hello TTL bir belge üzerinde gösteren sıfır olmayan pozitif bir sayı hello dönem hello zaman damgası hello belgenin son değiştirilme sonra tooexpire hello belge saniye cinsinden tooprovide gerekir (`_ts`).
* Bir belgenin hello koleksiyonunun varsayılan hello hiçbir TTL alan varsa uygulanır.
* TTL hello koleksiyon düzeyinde devre dışıysa, TTL hello koleksiyonunda yeniden etkinleştirilene kadar hello belgesindeki hello TTL alanında yoksayılacak.

Nasıl tooset hello belge TTL bitiş tarihini gösteren bir parçacığı aşağıda verilmiştir:

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a>Var olan bir belgeyi TTL genişletme
Merhaba belge üzerinde herhangi bir yazma işlemi yaparak hello TTL belgesinde sıfırlayabilirsiniz. Bunun yapılması hello ayarlayacak `_ts` toohello geçerli saati ve hello geri sayım toohello hello tarafından belirlenen süre sonu, belge `ttl`, yeniden başlar. Toochange hello istiyorsanız `ttl` bir belgenin diğer ayarlanabilir alan yaptığınız gibi hello alanı güncelleştirebilirsiniz.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a>Bir belgeden TTL kaldırma
TTL bir belgeyi ayarlama ve artık bu belgeyi tooexpire istiyorsanız, ardından hello belge alabilir, hello TTL alanı kaldırmak ve hello sunucusundaki hello belgeden değiştirin. Merhaba TTL alanı hello belgeden kaldırıldığında, hello varsayılan hello koleksiyonunun uygulanır. toostop bir belgeden süresinin dolmasını ve hello koleksiyonundan devralmayan tooset hello TTL değeri çok-1 yüklemeniz gerekir.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a>TTL devre dışı bırakma
toodisable TTL tamamen, bir koleksiyon ve durdurma hello arka plan işleme hello DefaultTTL özelliği hello koleksiyonunda silinmeli süresi dolan belgeleri için aranıyor. Bu özellik silme çok 1 ayarından farklıdır. Yeni belgeleri çok 1 anlamına gelir ayarlama toohello koleksiyonu sonsuza kadar Canlı ancak, bu belirli belgeleri hello koleksiyonundaki kılabilirsiniz eklendi. Önceki bir varsayılan açıkça silmiş belgeleri olsa bile bu özellik tamamen hello koleksiyonundan kaldırılması hiçbir belge dolacağını anlamına gelir.

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a>SSS
**Ne TTL bana maliyeti ne olacak?**

Hiçbir ek maliyet toosetting TTL belgesinde yoktur.

**Ne kadar süreyle Hello TTL yukarı olduğunda, my belge toodelete sürer?**

hemen hello TTL çalışır durumda ve CRUD veya sorgu API'leri yoluyla erişilemeyecek hello belgeleri süresi dolmuş. 

**TTL belgesinde herhangi RU giderler etkileyecek?**

Hayır, hiçbir etkisi olacaktır RU masrafları Cosmos DB'de TTL aracılığıyla süresi dolan belgelerin silme işlemleri için.

**Hello TTL özelliği yalnızca tooentire belgeleri geçerli veya bireysel belge özellik değerlerini süresinin dolmasını sağlayabilir mi?**

TTL toohello belgenin tamamına uygulanır. Tooexpire isterseniz yeni bir belge ve ardından bir kısmı tooa ayrı "bağlı" belgedeki hello ana belgeden hello bölümü ayıklayın ve ardından TTL ayıklanan belge kullanmak önerilir.

**Merhaba TTL özellik belirli bir dizin oluşturma gereksinimleri var mı?**

Evet. Merhaba koleksiyonu olmalıdır [ilke kümesi dizin](indexing-policies.md) tooeither CONSISTENT veya Lazy. Önceden ayarlanmış bir DefaultTTL sahip bir koleksiyonun üzerinde dizin oluşturmayı devre dışı çalışırken tooturn olarak tooset DefaultTTL kümesi tooNone dizin ile bir koleksiyon üzerinde çalışırken bir hatayla sonuçlanır.

## <a name="next-steps"></a>Sonraki adımlar
Azure Cosmos DB hakkında daha fazla toolearn başvuran toohello hizmet [ *belgelerine* ](https://azure.microsoft.com/documentation/services/cosmos-db/) sayfası.

