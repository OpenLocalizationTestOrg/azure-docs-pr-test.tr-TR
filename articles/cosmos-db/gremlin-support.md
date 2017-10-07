---
title: aaaAzure Cosmos DB Gremlin destek | Microsoft Docs
description: "Merhaba, özellikleri ve adımları Apache TinkerPop Gremlin dili hakkında bilgi edinin ve Azure Cosmos veritabanı kullanılabilir"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 6016ccba-0fb9-4218-892e-8f32a1bcc590
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/10/2017
ms.author: denlee
ms.openlocfilehash: f8c2ce50c6946e971f56fe1f3838b0899cb2ad8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-gremlin-graph-support"></a>Azure Cosmos DB Gremlin grafik desteği
Azure Cosmos DB destekleyen [Apache Tinkerpop'ın](http://tinkerpop.apache.org) grafik geçişi dil [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), grafik varlıkları oluşturma ve grafik sorgu işlemleri gerçekleştirmek için bir grafik API'si olan. Hello Gremlin dil toocreate grafik varlıkları (köşeleri ve kenarları) kullanın, bu varlıkların içinde özelliklerini değiştirmek, sorgular ve çapraz geçişlerine gerçekleştirmek ve varlıkları silin. 

Azure Cosmos DB Kurumsal kullanıma hazır özellikler toograph veritabanları getirir. Bu, genel dağıtım, depolama ve işleme, tahmin edilebilir tek basamaklı milisaniyelik gecikme, otomatik dizin oluşturma ve % 99,99 SLA ölçeklendirme bağımsız içerir. Azure Cosmos DB TinkerPop/Gremlin desteklediğinden, başka bir grafik veritabanı toomake kod değişiklikleri olmadan kullanılarak yazılmış uygulamaları kolayca geçirebilirsiniz. Ayrıca, Gremlin desteği sayesinde, Azure Cosmos DB sorunsuz bir şekilde TinkerPop etkin analitik çerçeveler gibi bütünleşir [Apache Spark GraphX](http://spark.apache.org/graphx/). 

Bu makalede, biz Gremlin hızlı bir kılavuz sağlar ve hello Gremlin özellikleri ve grafik API'si destek hello Önizleme'de desteklenen adımları numaralandırır.

## <a name="gremlin-by-example"></a>Örneğe göre gremlin
Bir örnek grafik toounderstand nasıl sorguları Gremlin ifade edilebilir kullanalım. Merhaba aşağıdaki şekilde kullanıcıların, ilgi alanları ve aygıtların bir grafik hello formunda ilgili verileri yöneten bir iş uygulaması gösterilmiştir.  

![Kişilerin, cihazların ve ilgi gösteren örnek veritabanı](./media/gremlin-support/sample-graph.png) 

Bu grafik şu (Gremlin içinde "etiket" olarak adlandırılır) köşe türlerini hello sahiptir:

- Kişiler: hello grafiği bir kez deneme, Thomas ve Ben üç kişilerin vardır.
- İlgi: Bu örnekte, kendi ilgi alanlarına futbol oyunu hello
- Aygıtlar: kişiler kullanan hello cihazları
- İşletim sistemleri: hello işletim sistemlerini çalıştıran hello cihazlar

Biz kenarı türleri/etiketleri aşağıdaki hello aracılığıyla bu varlıkları arasındaki ilişkileri hello temsil eder:

- Bilir: Örneğin, "Thomas deneme bilir"
- İlginizi: bizim grafikte hello kişilerin Örneğin, "Ben içinde futbol ilgilenmektedir" toorepresent hello ilgi
- RunsOS: Dizüstü hello Windows işletim sistemi çalıştırır.
- Kullanır: toorepresent hangi cihaz kişi bir kullanır. Örneğin, bir kez deneme 77 seri numarasıyla Motorola telefon kullanır.

Bazı işlemler hello kullanarak bu grafik karşı Şimdi Çalıştır [Gremlin konsol](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console). Tercih ettiğiniz (Java, Node.js, Python veya .NET) hello platformunda Gremlin sürücüleri kullanarak bu işlemler gerçekleştirebilir.  Azure Cosmos DB'de desteklenen adresindeki Ara önce birkaç örnek tooget hello sözdizimi hakkında bilginiz bakalım.

İlk CRUD bakalım. Merhaba aşağıdaki Gremlin deyimi hello "Thomas" köşe hello grafik ekler:

```
:> g.addV('person').property('id', 'thomas.1').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44)
```

Ardından, bir "bilir" kenar Thomas ve bir kez deneme arasındaki Gremlin deyiminden hello ekler.

```
:> g.V('thomas.1').addE('knows').to(g.V('robin.1'))
```

Merhaba aşağıdaki sorguyu hello "kişi" köşeleri ilk adlarının azalan sırada döndürür:
```
:> g.V().hasLabel('person').order().by('firstName', decr)
```

Burada, gerektiğinde grafikleri bekliyoruz tooanswer "hangi işletim sistemleri Thomas arkadaşların kullanıyor musunuz?" gibi soruları. Bu basit Gremlin geçişi tooget bu bilgileri hello grafikten çalıştırabilirsiniz:

```
:> g.V('thomas.1').out('knows').out('uses').out('runsos').group().by('name').by(count())
```
Şimdi ne Azure Cosmos DB Gremlin geliştiricileri için sağladığı konumundaki bakalım.

## <a name="gremlin-features"></a>Gremlin özellikleri
TinkerPop grafik teknolojileri çeşitli kapsayan bir standarttır. Bu nedenle, hangi özelliklerin bir grafik sağlayıcısı tarafından sağlanan standart terminolojisi toodescribe sahiptir. Azure Cosmos DB kalıcı, yüksek eşzamanlılık, birden çok sunuculara veya kümelere bölümlenebilir yazılabilir grafik veritabanı sağlar. 

Merhaba aşağıdaki tabloda Azure Cosmos DB tarafından uygulanan hello TinkerPop özellikler listelenmektedir: 

| Kategori | Azure Cosmos DB uygulama |  Notlar | 
| --- | --- | --- |
| Grafik özellikleri | Kalıcılığı ve ConcurrentAccess Önizleme'de sağlar. Tasarlanmış toosupport işlemleri | Bilgisayar yöntemlerini hello Spark bağlayıcısı aracılığıyla uygulanabilir. |
| Değişken özellikleri | Boolean, tamsayı, bayt destekler çift, tamsayı, uzun, dize Float | İlkel türler destekler, veri modeli aracılığıyla karmaşık türler ile uyumlu |
| Köşe özellikleri | RemoveVertices, MetaProperties, AddVertices, MultiProperties, StringIds, UserSuppliedIds, AddProperty, RemoveProperty destekler  | Oluşturma, değiştirme ve silme köşeleri destekler |
| Köşe özellik özellikleri | StringIds, UserSuppliedIds, AddProperty, RemoveProperty, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | Oluşturma, değiştirme ve silme köşe özelliklerini destekler |
| Edge özellikleri | AddEges, RemoveEdges, StringIds, UserSuppliedIds, AddProperty, RemoveProperty | Oluşturma, değiştirme ve silme kenarları destekler |
| Özellik özellikleri | Özellikler, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | Oluşturma, değiştirme ve silme kenar özellikleri destekler |

## <a name="gremlin-wire-format-graphson"></a>Gremlin kablo biçimi: GraphSON

Azure Cosmos DB kullanır hello [GraphSON biçimi](https://github.com/thinkaurelius/faunus/wiki/GraphSON-Format) sonuçları Gremlin işlemlerinden döndürülürken. GraphSON köşeleri, kenarları ve JSON kullanarak özelliklerini (tek ve birden çok değerli) temsil eden hello Gremlin standart biçimidir. 

Örneğin, hello aşağıdaki kod parçacığında köşe GraphSON gösterimini gösterir *toohello istemci döndürülen* Azure Cosmos DB'den. 

```json
  {
    "id": "a7111ba7-0ea1-43c9-b6b2-efc5e3aea4c0",
    "label": "person",
    "type": "vertex",
    "outE": {
      "knows": [
        {
          "id": "3ee53a60-c561-4c5e-9a9f-9c7924bc9aef",
          "inV": "04779300-1c8e-489d-9493-50fd1325a658"
        },
        {
          "id": "21984248-ee9e-43a8-a7f6-30642bc14609",
          "inV": "a8e3e741-2ef7-4c01-b7c8-199f8e43e3bc"
        }
      ]
    },
    "properties": {
      "firstName": [
        {
          "value": "Thomas"
        }
      ],
      "lastName": [
        {
          "value": "Andersen"
        }
      ],
      "age": [
        {
          "value": 45
        }
      ]
    }
  }
```

Köşe için GraphSON tarafından kullanılan hello özellikleri hello şunlardır:

| Özellik | Açıklama |
| --- | --- |
| id | Merhaba köşe Hello kimliği. (Birleşimi _partition varsa hello değerle) benzersiz olmalıdır |
| Etiket | Merhaba köşesinin Hello etiketi. Bu isteğe bağlıdır ve kullanılan toodescribe hello varlık türüdür. |
| type | Grafik olmayan belgelerden kullanılan toodistinguish köşeleri |
| properties | Merhaba köşe ile ilişkili kullanıcı tanımlı özellikleri paketi. Her bir özellik, birden çok değerlere sahip olabilir. |
| _partition (yapılandırılabilir) | Merhaba köşe Hello bölüm anahtarı. Grafikleri çıkışı kullanılan tooscale toomultiple sunucular olabilir |
| outE | Bu, bir köşe kenarlarından çıkışı bir listesini içerir. Köşe ile Merhaba bitişik bilgilerini depolamak için çapraz geçişlerine Hızlı yürütme sağlar. Kenarları etiketlerine göre gruplandırılır. |

Ve bilgi toohelp hello grafiğinin Gezinti tooother bölümleriyle aşağıdaki hello hello kenar içerir.

| Özellik | Açıklama |
| --- | --- |
| id | Merhaba kenar Hello kimliği. (Birleşimi _partition varsa hello değerle) benzersiz olmalıdır |
| Etiket | Merhaba ucunun Hello etiketi. Bu özellik isteğe bağlıdır ve kullanılan toodescribe hello ilişki türüdür. |
| Stok | Bu bir kenar için köşeleri listesi içerir. Merhaba edge Hello bitişik bilgilerini depolamak çapraz geçişlerine hızlı yürütülmesini sağlar. Köşeleri etiketlerine göre gruplandırılır. |
| properties | Merhaba edge ile ilişkili kullanıcı tanımlı özellikleri paketi. Her bir özellik, birden çok değerlere sahip olabilir. |

Her bir özellik, bir dizi birden çok değer depolayabilirsiniz. 

| Özellik | Açıklama |
| --- | --- |
| değer | Merhaba özelliğinin Hello değeri

## <a name="gremlin-partitioning"></a>Gremlin bölümlendirme

Azure Cosmos DB'de grafikleri ölçeklendirebilirsiniz kapsayıcılara depolanan bağımsız olarak bakımından depolama üretilen işi (normalleştirilmiş istekleri / saniye cinsinden). Her kapsayıcı isteğe bağlı bir tanımlamanız gerekir, ancak ilgili veriler için bir mantıksal bölüm sınır belirler bölüm anahtar özelliği önerilir. Her köşe/kenar olmalıdır bir `id` Bu bölüm anahtarı değerini varlıkları için benzersizdir özelliği. Merhaba ayrıntıları ele alınmıştır [Azure Cosmos DB'de bölümleme](partition-data.md).

Gremlin işlemleri Azure Cosmos DB birden çok bölüm span grafik verileri arasında sorunsuz çalışır. Ancak, sorguları, filtre olarak yaygın olarak kullanılan, grafikleri sahip birçok farklı değerleri ve benzer sıklığını bu değerleri erişmek için bir bölüm anahtarı toochoose önerilir. 

## <a name="gremlin-steps"></a>Gremlin adımları
Şimdi hello Azure Cosmos DB tarafından desteklenen Gremlin adımları bakalım. Gremlin üzerinde tam bir başvuru için bkz: [TinkerPop başvuru](http://tinkerpop.apache.org/docs/current/reference).

| Adım | Açıklama | TinkerPop 3.2 belgeleri | Notlar |
| --- | --- | --- | --- |
| `addE` | İki köşeleri arasında kenar ekler | [addE adım](http://tinkerpop.apache.org/docs/current/reference/#addedge-step) | |
| `addV` | Bir köşe toohello grafik ekler | [addV adım](http://tinkerpop.apache.org/docs/current/reference/#addvertex-step) | |
| `and` | Ensurest tüm hello çapraz geçişlerine değer döndürme | [ve adım](http://tinkerpop.apache.org/docs/current/reference/#and-step) | |
| `as` | Bir adım modülatörü tooassign bir adım bir değişken toohello çıktısı | [adım olarak](http://tinkerpop.apache.org/docs/current/reference/#as-step) | |
| `by` | İle kullanılan bir adım modülatörü `group` ve`order` | [Adım](http://tinkerpop.apache.org/docs/current/reference/#by-step) | |
| `coalesce` | Bir sonuç döndürür hello ilk geçişi döndürür | [Adım birleşim](http://tinkerpop.apache.org/docs/current/reference/#coalesce-step) | |
| `constant` | Sabit bir değer döndürür. İle kullanılan`coalesce`| [Sabit adım](http://tinkerpop.apache.org/docs/current/reference/#constant-step) | |
| `count` | Merhaba geçişi Merhaba sayımını döndürür | [Count adım](http://tinkerpop.apache.org/docs/current/reference/#count-step) | |
| `dedup` | Merhaba yinelenen değerleri kaldırılmış değerleri döndürür hello | [Yinelenenleri kaldırma adım](http://tinkerpop.apache.org/docs/current/reference/#dedup-step) | |
| `drop` | Değerleri (köşe/kenar) düşme hello | [bırakma adımı](http://tinkerpop.apache.org/docs/current/reference/#drop-step) | |
| `fold` | Merhaba toplama sonuçları hesaplar bir engel görür| [Katlama adım](http://tinkerpop.apache.org/docs/current/reference/#fold-step) | |
| `group` | Belirtilen hello etiketlerini esas alan değerleri grupları hello| [Grup adımı](http://tinkerpop.apache.org/docs/current/reference/#group-step) | |
| `has` | Toofilter özellikleri, köşe ve kenarları kullanılır. Destekler `hasLabel`, `hasId`, `hasNot`, ve `has` çeşitleri. | [adım vardır](http://tinkerpop.apache.org/docs/current/reference/#has-step) | |
| `inject` | Değerleri bir akışa ekleme| [Adım ekleme](http://tinkerpop.apache.org/docs/current/reference/#inject-step) | |
| `is` | Boole ifadesi kullanarak bir filtre tooperform kullanılan | [Adım](http://tinkerpop.apache.org/docs/current/reference/#is-step) | |
| `limit` | Öğe sayısı toolimit hello geçişi kullanılan| [sınır adım](http://tinkerpop.apache.org/docs/current/reference/#limit-step) | |
| `local` | Yerel bir çapraz geçiş, benzer tooa alt sorgu bölümünü sarmalar | [Yerel adım](http://tinkerpop.apache.org/docs/current/reference/#local-step) | |
| `not` | Bir filtre tooproduce hello değilleme kullanılan | [Adım değil](http://tinkerpop.apache.org/docs/current/reference/#not-step) | |
| `optional` | Belirtilen hello sonucunu döndürür hello döndürdüğü sonuç başka döndürürse geçişi hello arama öğesi | [İsteğe bağlı adım](http://tinkerpop.apache.org/docs/current/reference/#optional-step) | |
| `or` | Merhaba çapraz geçişlerine en az biri bir değer döndürür sağlar | [veya adımı](http://tinkerpop.apache.org/docs/current/reference/#or-step) | |
| `order` | Merhaba döndürür sonuçlarında belirtilen sıralama düzeni | [Sipariş adım](http://tinkerpop.apache.org/docs/current/reference/#order-step) | |
| `path` | Döndürür hello tam yolunu hello geçişi | [yol adım](http://tinkerpop.apache.org/docs/current/reference/#path-step) | |
| `project` | Bir harita olarak projeleri hello özellikleri | [Proje adım](http://tinkerpop.apache.org/docs/current/reference/#project-step) | |
| `properties` | Etiketleri döndürür hello özellikleri hello için belirtilen | [özellikleri adım](http://tinkerpop.apache.org/docs/current/reference/#properties-step) | |
| `range` | Filtreler toohello değerlerin belirtilen| [Aralık adım](http://tinkerpop.apache.org/docs/current/reference/#range-step) | |
| `repeat` | Hello için tekrarlanıyor hello adım sayısı belirtildi. Döngü için kullanılan | [adımı yineleyin](http://tinkerpop.apache.org/docs/current/reference/#repeat-step) | |
| `sample` | Merhaba geçişi toosample sonuçlarından kullanılan | [Örnek adım](http://tinkerpop.apache.org/docs/current/reference/#sample-step) | |
| `select` | Merhaba geçişi tooproject sonuçlarından kullanılan |  [adım seçin](http://tinkerpop.apache.org/docs/current/reference/#select-step) | |
| `store` | Engelleyici olmayan toplamalar hello geçişi gelen için kullanılır | [Mağaza adım](http://tinkerpop.apache.org/docs/current/reference/#store-step) | |
| `tree` | Bir ağaç içine köşe toplama yolları | [Ağaç adım](http://tinkerpop.apache.org/docs/current/reference/#tree-step) | |
| `unfold` | Yineleyici bir adım olarak unroll| [Adım unfold](http://tinkerpop.apache.org/docs/current/reference/#unfold-step) | |
| `union` | Birden çok çapraz geçişlerine sonuçlarından birleştirme| [birleşim adım](http://tinkerpop.apache.org/docs/current/reference/#union-step) | |
| `V` | Köşeleri ve kenarları arasında çapraz geçişlerine için gerekli Hello adımları içerir `V`, `E`, `out`, `in`, `both`, `outE`, `inE`, `bothE`, `outV`, `inV`, `bothV`, ve `otherV` için | [Köşe adımları](http://tinkerpop.apache.org/docs/current/reference/#vertex-steps) | |
| `where` | Merhaba geçişi toofilter sonuçlarından kullanılır. Destekler `eq`, `neq`, `lt`, `lte`, `gt`, `gte`, ve `between` işleçleri  | [Burada adım](http://tinkerpop.apache.org/docs/current/reference/#where-step) | |

Azure Cosmos veritabanı altyapısı yazma için iyileştirilmiş otomatik köşeleri ve kenarları içindeki tüm özelliklerinin varsayılan dizin oluşturmayı destekler. Bu nedenle, sorgular filtreleriyle, sorguları, sıralama, aralık veya herhangi bir özellikte toplamalar hello dizinden işlenir ve verimli bir şekilde hizmet. Üzerinde şu incelemeyi Azure Cosmos veritabanı dizin oluşturma nasıl çalıştığıyla ilgili daha fazla bilgi için bkz [şema belirsiz dizin](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf).

## <a name="next-steps"></a>Sonraki Adımlar
* Graph uygulaması oluşturmaya başlamak [bizim SDK'ları kullanma](create-graph-dotnet.md) 
* Daha fazla bilgi edinmek [Azure Cosmos DB'ın grafik desteği](graph-introduction.md)
