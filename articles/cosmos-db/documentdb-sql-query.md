---
title: "Azure Cosmos DB DocumentDB API aaaSQL sorgularında | Microsoft Docs"
description: "Azure Cosmos DB SQL söz dizimi, veritabanı kavramlarını ve SQL sorguları hakkında bilgi edinin. SQL Azure Cosmos veritabanı bir JSON sorgu dili olarak kullanabilir."
keywords: "SQL söz dizimi, sql sorgusu, sql sorguları, json sorgu dili, veritabanı kavramlarını ve sql sorguları, toplama işlevleri"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a>SQL sorguları Azure Cosmos DB DocumentDB API'si
Microsoft Azure Cosmos DB bir JSON sorgu dili SQL (yapılandırılmış sorgu dili) kullanarak belgelerin sorgulanmasını destekler. Cosmos DB gerçekten şemasız. Kendi taahhüt toohello JSON veri modeli, doğrudan hello veritabanı altyapısı içinde otomatik JSON belgelerinin dizinini gerektirmeden açık şema veya ikincil dizinlerin oluşturulmasını sağlar. 

Cosmos DB Hello sorgu dili tasarlarken size iki hedefleri düşünerek vardı:

* Yeni bir JSON sorgu dili inventing yerine, biz toosupport SQL istedik. SQL hello en tanıdık ve popüler sorgu dilleri biridir. Cosmos veritabanı SQL, JSON belgelerini zengin sorgular için resmi bir programlama modeli sağlar.
* Bir JSON belgesi veritabanı JavaScript doğrudan hello Veritabanı Altyapısı'nda yürütülebilir, biz toouse JavaScript'in programlama modeli hello temel olarak bizim sorgu dili için istedik. Merhaba DocumentDB API SQL JavaScript'in tür sistemi, ifade değerlendirmesi ve işlev çağrısını kökü belirtilmiş. Bu içinde dönüş JSON belgeleri, kendi kendine birleşimler, uzamsal sorguları ve kullanıcı tanımlı işlevler (UDF'ler) diğer özellikler arasında JavaScript tamamen yazılmış çalıştırılışı arasında ilişkisel projeksiyonları, hiyerarşik gezinti için doğal bir programlama modeli sağlar. 

Bu özellikler anahtar tooreducing hello uyuşmazlık Merhaba uygulaması ile Merhaba veritabanı arasında ve geliştirici üretkenliği için önemli olduğundan inanıyoruz.

Burada Aravind Ramachandran Cosmos veritabanı sorgulama özelliklerini gösterir, video, aşağıdaki hello izlemeye ve ziyaret tarafından Başlarken öneririz bizim [Query Playground](http://www.documentdb.com/sql/demo), burada Cosmos DB deneyin ve SQL sorguları çalıştırma Veri kümemizde.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

Ardından, burada size bazı basit JSON belgeleri ve SQL komutları anlatan bir SQL sorgusu öğretici başlayın toothis makale döndür.

## <a id="GettingStarted"></a>Cosmos DB SQL komutları ile çalışmaya başlama
toosee Cosmos DB SQL adresindeki iş, şimdi birkaç basit JSON belgeleri ile başlar ve bazı basit sorgular size yol. Bu iki JSON belgeleri iki ailesi hakkında göz önünde bulundurun. Cosmos DB ile biz toocreate herhangi bir şemaları ya da ikincil dizinlerin açıkça gerekmez. Biz tooinsert hello JSON belgeleri tooa Cosmos DB koleksiyonu yeterlidir ve daha sonra sorgulayabilirsiniz. Basit bir JSON burada sahibiz belge hello Andersen ailesi, hello üst, alt öğelerini (ve bunların Evcil Hayvanlar), adresinizi ve kayıt bilgileri. Merhaba belge dizeler, sayılar, Boole değerlerini, dizileri ve iç içe özellikler vardır. 

**Belge**  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

Bir fark – sahip ikinci bir belge işte `givenName` ve `familyName` yerine kullanılan `firstName` ve `lastName`.

**Belge**  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

Şimdi birkaç sorgu deneyelim bu veri toounderstand karşı hello bazıları DocumentDB API SQL yönlerini anahtar. Örneğin, hello aşağıdaki hello Kimliği alanı eşleştiği döndürür hello belgeleri sorgu `AndersenFamily`. Olduğundan bir `SELECT *`, hello hello sorgu çıkışıdır hello tam JSON belgesi:

**Sorgu**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Sonuçları**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


Şimdi tooreformat hello farklı bir şekli JSON çıkışında burada ihtiyacımız hello durumu göz önünde bulundurun. Bu sorgu Hello Adres Şehir hello durumu olarak aynı ad hello olduğunda iki seçili alanları ile adı ve şehir projeleri yeni bir JSON nesnesi. Bu durumda, "NY, NY" eşleşir.

**Sorgu**    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

**Sonuçları**

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


Merhaba sonraki sorgunun döndürdüğü tüm hello verilen adları alt kimliğine eşleşen hello ailesinde `WakefieldFamily` hello Şehir ikamet ettiğiniz sıralanan.

**Sorgu**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

**Sonuçları**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


Merhaba Cosmos DB birkaç önemli yönleri sorgu dili kadarki gördük hello örnekler üzerinden toodraw dikkat tooa isteriz:  

* DocumentDB API SQL JSON değerler üzerinde çalışır olduğundan, satır ve sütunların yerine varlıklar şeklinde ağaç ile ilgilidir. Bu nedenle, hello dili, herhangi bir rastgele derinliğe hello ağacını toonodes gibi bakın sağlar `Node1.Node2.Node3…..Nodem`, benzer toorelational SQL başvuran toohello iki bölümü başvurusu `<table>.<column>`.   
* Merhaba sorgu dili works şema daha az veri ile yapılandırılmış. Bu nedenle, hello türü sistem gereksinimlerini toobe bağlı dinamik olarak. Merhaba aynı ifade farklı belgelere farklı türlerde üretebilir. bir sorgunun sonucu Hello geçerli bir JSON değer olmakla birlikte, sabit bir şema toobe garanti edilmez.  
* Cosmos DB yalnızca Katı JSON belgelerini destekler. Bu, yalnızca JSON türleriyle sınırlı toodeal hello tür sistemi ve ifadeler olduğu anlamına gelir. Toohello başvuran [JSON belirtimi](http://www.json.org/) daha fazla ayrıntı için.  
* Cosmos DB koleksiyon JSON belgeleri, şemasız bir kapsayıcısıdır. Merhaba ilişkileri veri varlıklarında içinde ve bir koleksiyondaki belgeler arasında örtük olarak kapsama ve birincil anahtar ve yabancı anahtar ilişkileri tarafından yakalanır. Bu makalenin sonraki bölümlerinde ele alınan hello içi belge birleştirmeler etkinliğinin düzenleyicileri gösteren değer önemli bir yönü budur.

## <a id="Indexing"></a>Cosmos DB dizin oluşturma
Biz DocumentDB API SQL söz dizimi hello ulaşmadan Cosmos DB tasarımında dizin hello incelenmesi yararlı olan. 

Veritabanı dizinlerini Hello amacı, iyi performans ve düşük gecikme süresi sağlarken kendi çeşitli formlar ve şekiller (örneğin, CPU ve giriş/çıkış) en düşük kaynak kullanımına sahip tooserve sorguları budur. Genellikle, bir veritabanını sorgulamak için doğru dizin hello hello seçimine kadar planlama ve deneme gerektirir. Bu yaklaşım, burada hello veri tooa kesin şema uygun değil ve hızlı bir şekilde dönüşmesi şema daha az veritabanları için bir zorluk oluşturur. 

Bu nedenle, biz hello Cosmos DB dizin alt sistemi tasarlarken, biz hedeflerini izleyerek hello ayarlayın:

* Dizin belgeleri şema gerek kalmadan: alt dizin hello herhangi bir şema bilgi gerektirmez veya şeması hakkında tüm varsayımlarda hello belgelerin. 
* Verimli, zengin hiyerarşik ve ilişkisel sorguları için destek: hello dizinini destekleyen hello Cosmos DB sorgu dili verimli bir şekilde, hiyerarşik ve ilişkisel tahminleri desteği dahil olmak üzere.
* Yazma sürekli bir birim in face of tutarlı sorgular için destek: yüksek yazma işleme iş yükleri için tutarlı sorgularla hello dizin artımlı olarak, verimli ve çevrimiçi yazma sürekli bir birimin hello karşılaştıkları güncelleştirilir. önemli tooserve hello sorguları hangi hello yapılandırılan kullanıcı hello belge hizmetindeki hello tutarlılık düzeyinde Hello tutarlı dizin güncelleştirmesidir.
* Çoklu kiracı için destek: hello ayırmaya dayalı modeli için kaynak İdaresi kiracılar arasında verildiğinde, dizin güncelleştirmeleri hello bütçe çoğaltma ayrılan sistem kaynaklarını (İşlemci, bellek ve saniye başına girdi/çıktı işlemleri) içinde gerçekleştirilir. 
* Depolama verimliliği: maliyet verimliliği için hello disk üzerinde depolama ek yükü hello dizinin sınırlanmış ve tahmin edilebilir. Cosmos DB maliyet tabanlı Geliştirici toomake bileşim dizin yükü ilişkisi toohello sorgu performansı arasında hello sağladığından, bu önemlidir.  

Toohello başvuran [Azure Cosmos DB örnekleri](https://github.com/Azure/azure-documentdb-net) nasıl tooconfigure hello bir koleksiyon için dizin oluşturma ilkesini gösteren örnekler için MSDN'de. Şimdi şimdi hello Azure Cosmos DB SQL söz dizimi hello ayrıntılarını alın.

## <a id="Basics"></a>Bir Azure Cosmos DB SQL sorgusu temelleri
Her sorgu, bir SELECT yan tümcesi ve isteğe bağlı FROM oluşur ve WHERE yan tümcelerini ANSI SQL standartları başına. Genellikle, her sorgu için hello kaynak hello FROM yan tümcesinde numaralandırılır. Daha sonra hello filtre hello WHERE yan tümcesi hello kaynak tooretrieve üzerinde uygulanır, JSON belgelerini bir kısmı. Son olarak, hello SELECT yan tümcesinde kullanılan tooproject hello istenen hello JSON değerleri listesi seçin.

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <a id="FromClause"></a>FROM yan tümcesi
Merhaba `FROM <from_specification>` hello kaynak filtre ya da daha sonra hello sorguda öngörülen sürece yan tümcesi isteğe bağlıdır. Bu yan tümce Hello amacı hangi hello sorgu çalışmalıdır toospecify hello veri kaynağıdır. Yaygın olarak hello tüm koleksiyon hello kaynağıdır, ancak bir hello koleksiyonunun bir alt bunun yerine belirtebilirsiniz. 

Bir sorgu ister `SELECT * FROM Families` hello tüm aileleri koleksiyon hangi tooenumerate hello kaynak olduğunu gösterir. Özel bir tanımlayıcısı kök hello koleksiyon adı kullanmak yerine kullanılan toorepresent hello koleksiyonu olabilir. Merhaba aşağıdaki listede sorgu zorlanan hello kurallarını içerir:

* Merhaba koleksiyonu olabilir, diğer gibi `SELECT f.id FROM Families AS f` ya da yalnızca `SELECT f.id FROM Families f`. Burada `f` hello eşdeğerdir `Families`. `AS`optional anahtar sözcüğü tooalias hello tanımlayıcısı değil.
* Bir kez diğer hello özgün kaynak bağlanamaz. Örneğin, `SELECT Families.id FROM Families f` hello tanımlayıcı "Aileleri" artık çözümlenemiyor beri sözdizimsel olarak geçersiz.
* Başvurulan toobe gereken tüm özellikleri tam olarak nitelenmiş olmalıdır. Merhaba kesin şema bağlılığı durumunda, bu zorlanan tooavoid bildirilmesidir belirsiz hiçbir bağlama. Bu nedenle, `SELECT id FROM Families f` hello özelliği bu yana sözdizimsel olarak geçersiz `id` bağlı değil.

### <a name="subdocuments"></a>Alt belgeleri
Merhaba kaynağı azaltılmış tooa daha küçük alt de olabilir. Örneği için yalnızca bir alt ağacı her belgedeki tooenumerating hello subroot sonra hello kaynak hello aşağıdaki örnekte gösterildiği gibi hale gelebilir:

**Sorgu**

    SELECT * 
    FROM Families.children

**Sonuçları**  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

Yukarıdaki örnek Hello hello kaynağı olarak bir dizi kullanılan olsa da, bir nesne de aşağıdaki örneğine hello gösterilen olduğu hello kaynağı olarak kullanılabilir: hello kaynağında bulunan (tanımsız değil) tüm geçerli JSON değer hello sonucunu eklenmek üzere olarak kabul edilir Merhaba sorgu. Bazı aileleri yoksa bir `address.state` değeri hello sorgu sonucu hariç tutulur.

**Sorgu**

    SELECT * 
    FROM Families.address.state

**Sonuçları**

    [
      "WA", 
      "NY"
    ]


## <a id="WhereClause"></a>WHERE yan tümcesi
WHERE yan tümcesi hello (**`WHERE <filter_condition>`**) isteğe bağlıdır. Merhaba hello kaynağı tarafından sağlanan hello JSON belgelerini hello sonuç bir parçası olarak dahil edilen sipariş toobe getirmelidir koşulları belirtir. Herhangi bir JSON belge değerlendirilmelidir hello belirtilen koşullar çok "true" Merhaba sonucu olarak kabul toobe. Merhaba yan tümcesi hello dizin katmanı sipariş toodetermine hello mutlak en küçük alt kümesini hello sonuç parçası olabilir kaynak belgeleri'tarafından kullanıldığı. 

Merhaba aşağıdaki sorguyu istekleri, değeri olan bir ad özelliği içeren belgeleri `AndersenFamily`. Name özelliği olmayan herhangi bir belge veya burada hello değeri eşleşmiyor `AndersenFamily` dışlandı. 

**Sorgu**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Sonuçları**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


Merhaba önceki örnekte basit eşitlik sorgu gösterdi. DocumentDB API SQL skaler ifadelerin çeşitli de destekler. İkili ve birli ifadeleri en yaygın olarak kullanılan hello var. Özellik başvuruları hello kaynak JSON nesnesinden de geçerli ifadeler oluyor. 

ikili işleçler aşağıdaki hello şu anda desteklenen ve örnek hello gösterildiği gibi sorgularında kullanılabilir:  

<table>
<tr>
<td>Aritmetik</td>    
<td>+,-,*,/,%</td>
</tr>
<tr>
<td>Bit düzeyinde</td>    
<td>|, &, ^, <<>>,, >>> (sıfır dolgu sağa kaydırma)</td>
</tr>
<tr>
<td>Mantıksal</td>
<td>VE VEYA DEĞİL</td>
</tr>
<tr>
<td>Karşılaştırma</td>    
<td>=, !=, &lt;, &gt;, &lt;=, &gt;=, <></td>
</tr>
<tr>
<td>Dize</td>    
<td>|| (birleştirme)</td>
</tr>
</table>  


İkili işleçler kullanarak bazı sorguları bir göz atalım.

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


birli işleçleri hello +,-, ~ değil de desteklenir ve sorgular içinde hello aşağıdaki örnekte gösterildiği gibi kullanılabilir:

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



Ayrıca toobinary ve birli işleçleri özelliği başvuruları de izin verilir. Örneğin, `SELECT * FROM Families f WHERE f.isRegistered` döndürür hello hello özelliği içeren JSON belgesi `isRegistered` hello özellik değerine eşit toohello JSON olduğu `true` değeri. Diğer tüm değerler (false, null, tanımlanmamış, `<number>`, `<string>`, `<object>`, `<array>`, vs.) toohello kaynak belge hello sonucundan dışlanan yol açar. 

### <a name="equality-and-comparison-operators"></a>Eşitlik ve Karşılaştırma işleçleri
Merhaba aşağıdaki tabloda eşitlik karşılaştırmaları hello sonucunu DocumentDB API SQL'de herhangi iki JSON türleri arasında gösterilmektedir.

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top">
            <strong>OP</strong>
         </td>
         <td valign="top">
            <strong>Tanımlanmamış</strong>
         </td>
         <td valign="top">
            <strong>Null</strong>
         </td>
         <td valign="top">
            <strong>Boole değeri</strong>
         </td>
         <td valign="top">
            <strong>Sayı</strong>
         </td>
         <td valign="top">
            <strong>Dize</strong>
         </td>
         <td valign="top">
            <strong>Nesne</strong>
         </td>
         <td valign="top">
            <strong>Dizi</strong>
         </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Tanımlanmamış<strong>
         </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Null<strong>
         </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
            <strong>TAMAM</strong>
         </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Boole değeri<strong>
         </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
            <strong>TAMAM</strong>
         </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Sayı<strong>
         </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
            <strong>TAMAM</strong>
         </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Dize<strong>
         </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
            <strong>TAMAM</strong>
         </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Nesne<strong>
         </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
            <strong>TAMAM</strong>
         </td>
         <td valign="top">
Tanımlanmamış </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Dizi<strong>
         </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
Tanımlanmamış </td>
         <td valign="top">
            <strong>TAMAM</strong>
         </td>
      </tr>
   </tbody>
</table>

Gibi diğer Karşılaştırma işleçleri için >, > =,! =, < ve <, hello = aşağıdaki kurallar geçerlidir:   

* Karşılaştırma türü üzerinden içinde tanımlanmamış sonuçlanır.
* İki nesne veya iki arasında karşılaştırma tanımlanmamış sonuçlarında dizi.   

Merhaba skaler ifade hello filtresi Hello sonucu olup olmadığını tanımlanmamış mantıksal olarak çok "true" eşitlemek değil bu yana tanımlanmamışsa, hello karşılık gelen belge hello sonucunda dahil edilir değil.

### <a name="between-keyword"></a>ARASINDA anahtar sözcüğü
ANSI SQL hello BETWEEN anahtar sözcüğü tooexpress sorguları aralıkları gibi değerlerin de kullanabilirsiniz. ARASINDA dizeyi veya sayı karşı kullanılabilir.

Örneğin, bu sorgu hangi hello ilk alt düzey 1-5 arasında (her ikisi de dahil) olan tüm ailesi belgeleri döndürür. 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

Farklı ANSI-SQL'de de hello BETWEEN yan tümcesi gibi hello FROM yan tümcesinde aşağıdaki örneğine hello kullanabilirsiniz.

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

Daha hızlı sorgu yürütme süreleri için toocreate tüm sayısal özellikleri/hello BETWEEN yan tümcesinde filtrelenen yolları karşı bir aralık dizin türünü kullanan bir dizin oluşturma ilkesi unutmayın. 

BETWEEN DocumentDB API ve ANSI SQL kullanarak arasında hello ana karma türlerinin özellikleri aralığı sorguları express – Örneğin, "bir sayı (5) düzeyde" olabilir bazı belgelerde ve diğerleri ("grade4") dizelerde farktır. Bu gibi durumlarda gibi JavaScript'te, iki farklı sonuçlarında "tanımsız" ve hello belge arasında bir karşılaştırma atlanacak.

### <a name="logical-and-or-and-not-operators"></a>Mantıksal (AND, OR ve NOT) işleçleri
Mantıksal işleçler Boole değerleri üzerinde çalışır. Bu işleçleri için mantıksal gerçekte tabloları Hello tabloları aşağıdaki hello gösterilir.

| OR | True | False | Tanımlanmamış |
| --- | --- | --- | --- |
| True |True |True |True |
| False |True |False |Tanımlanmamış |
| Tanımlanmamış |True |Tanımlanmamış |Tanımlanmamış |

| VE | True | False | Tanımlanmamış |
| --- | --- | --- | --- |
| True |True |False |Tanımlanmamış |
| False |False |False |False |
| Tanımlanmamış |Tanımlanmamış |False |Tanımlanmamış |

| DEĞİL |  |
| --- | --- |
| True |False |
| False |True |
| Tanımlanmamış |Tanımlanmamış |

### <a name="in-keyword"></a>Anahtar SÖZCÜĞÜ
Belirtilen bir değeri bir listedeki herhangi bir değer ile eşleşip eşleşmediğini hello IN anahtar sözcüğü kullanılan toocheck olabilir. Örneğin, bu sorgu, hello kimliği "WakefieldFamily" veya "AndersenFamily" biri olduğu tüm ailesi belgeleri döndürür. 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

Bu örnek hello durumu belirtilen hello hiçbirini olduğu tüm belgeleri döndüren değerleri.

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a>Üçlü (?) ve birleşim (?) işleçleri
Merhaba Üçlü ve birleşim işleçleri kullanılan toobuild koşullu ifadeler, C# ve JavaScript gibi programlama dillerinde benzer toopopular olabilir. 

Merhaba oluşturma yeni JSON özellikleri uçarak hello Üçlü (?) işleci çok kullanışlı olabilir. Örneğin, artık, sorguları tooclassify hello sınıfı düzeyleri başlangıç/Orta/aşağıda gösterildiği gibi gelişmiş gibi İnsan okunabilir bir form içine yazabilirsiniz.

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

Itanium tabanlı sistemler için hello çağrıları toohello operatör gibi aşağıdaki hello sorgusunda iç içe.

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

Olarak diğer sorgu işleçleri ile Merhaba hello koşullu ifade başvurulan özelliklerinde herhangi bir belgesinde eksikse veya karşılaştırılan hello türleri farklıysa, sonra bu belgeleri hello sorgu sonuçlarında hariç tutulur.

Merhaba birleşim (?) işleci olabilir tooefficiently onay hello bir özellik varlığını (paketini kullanılan tanımlanır) belgede. Yarı yapılandırılmış karşı sorgularken bu yararlıdır veya karma türlerinin veri. Örneğin, mevcut değilse bu sorguyu hello "Soyadı" varsa veya hello "Soyadı" döndürür.

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <a id="EscapingReservedKeywords"></a>Tırnak işaretli özelliği erişimcisi
Özellikler hello tırnak işaretli özelliği işlecini kullanarak da erişebilirsiniz `[]`. Örneğin, `SELECT c.grade` ve `SELECT c["grade"]` eşdeğerdir. Bu sözdiziminin tooescape alanları, özel karakterler içeriyor veya bir SQL anahtar sözcüğü ya da ayrılmış sözcük olarak aynı ad tooshare hello olur bir özellik gerektiğinde kullanışlıdır.

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <a id="SelectClause"></a>SELECT yan tümcesi
Merhaba SELECT yan tümcesi (**`SELECT <select_list>`**) zorunludur ve hangi değerlerin hello sorgudan tıpkı ANSI SQL'de alınır belirtir. Merhaba kaynak belgeleri üstünde filtre uygulanmış hello alt geçirilir hello projeksiyon aşaması hello JSON değerleri alınır ve yeni bir JSON nesnesi, bunun geçirilen her giriş için oluşturulan burada belirtilen. 

Aşağıdaki örnek hello tipik seçme sorgusu gösterir. 

**Sorgu**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Sonuçları**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a>İç içe Özellikler
Aşağıdaki örneğine hello biz iki iç içe özellikler yansıtma `f.address.state` ve `f.address.city`.

**Sorgu**

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Sonuçları**

    [{
      "state": "WA", 
      "city": "seattle"
    }]


Projeksiyon hello aşağıdaki örnekte gösterildiği gibi JSON ifadeler de destekler:

**Sorgu**

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Sonuçları**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


Merhaba role daha bakalım `$1` burada. Merhaba `SELECT` yan tümcesi toocreate bir JSON nesnesi gerekiyor ve hiçbir anahtar sağlanan beri örtük bağımsız değişken adları başlayarak kullanırız `$1`. Örneğin, etiketli iki örtük bağımsız değişkenlerini bu sorgunun döndürdüğü `$1` ve `$2`.

**Sorgu**

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Sonuçları**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a>Diğer ad
Şimdi şimdi hello Yukarıdaki örnek açık yumuşatma ile değerlerin genişletme. Diğer ad için kullanılan anahtar sözcük hello olduğu gibi. Planlanması hello ikinci değer çalışırken gösterildiği gibi isteğe bağlı `NameInfo`. 

Bir sorgu hello sahip iki özellik gerekmesi durumunda aynı adı yumuşatma birini veya her ikisini böylece bunlar öngörülen hello disambiguated özellikleri hello kullanılan toorename olmalı sonucu.

**Sorgu**

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Sonuçları**

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a>Skaler ifade
Ayrıca tooproperty başvuruyor, skaler ifadeler sabitler, aritmetik ifadeler, mantıksal ifadeler, vb. gibi hello SELECT yan tümcesi de destekler. Örneğin, basit bir "Hello World" sorgu aşağıdadır.

**Sorgu**

    SELECT "Hello World"

**Sonuçları**

    [{
      "$1": "Hello World"
    }]


Burada, skaler bir ifade kullanır daha karmaşık bir örnek verilmiştir.

**Sorgu**

    SELECT ((2 + 11 % 7)-2)/3    

**Sonuçları**

    [{
      "$1": 1.33333
    }]


Aşağıdaki örneğine hello hello hello skaler ifade Boolean sonucudur.

**Sorgu**

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

**Sonuçları**

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a>Nesne ve dizi oluşturma
Başka bir anahtar DocumentDB API SQL dizi/nesne oluşturma özelliğidir. Merhaba önceki örnekte yeni bir JSON nesnesi oluşturduğumuz dikkat edin. Benzer şekilde, bir de diziler hello örnekleri aşağıdaki gösterildiği gibi oluşturabilirsiniz:

**Sorgu**

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

**Sonuçları**  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <a id="ValueKeyword"></a>VALUE anahtar sözcüğü
Merhaba **değeri** anahtar sözcüğü bir şekilde tooreturn JSON değer sağlar. Örneğin, döndürür hello skaler gösterilen hello sorgu `"Hello World"` yerine `{$1: "Hello World"}`.

**Sorgu**

    SELECT VALUE "Hello World"

**Sonuçları**

    [
      "Hello World"
    ]


Merhaba aşağıdaki sorgunun döndürdüğü hello JSON değeri hello olmadan `"address"` hello sonuçlarında etiketi.

**Sorgu**

    SELECT VALUE f.address
    FROM Families f    

**Sonuçları**  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

Merhaba aşağıdaki örnekte bu tooshow nasıl genişlettiğini tooreturn JSON ilkel değerlerini (yaprak düzeyi hello JSON ağaç hello). 

**Sorgu**

    SELECT VALUE f.address.state
    FROM Families f    

**Sonuçları**

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a>* İşleci
Merhaba özel işleci (*) desteklenen tooproject hello olarak belgedir-değil. Kullanıldığında, hello yalnızca alan öngörülen olmalıdır. While gibi bir sorgu `SELECT * FROM Families f` geçerli olduğu `SELECT VALUE * FROM Families f ` ve `SELECT *, f.id FROM Families f ` geçerli değildir.

**Sorgu**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Sonuçları**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <a id="TopKeyword"></a>TOP işleci
Merhaba üst anahtar sözcüğü olabilir toolimit hello değerleri sorgudan sayısı kullanılır. ÜST hello ORDER BY yan tümcesi ile birlikte kullanıldığında, hello sonuç kümesi sınırlı toohello ilk N sıralı değerler sayısıdır; Aksi takdirde, tanımlanmamış bir sırada hello ilk N sonuç sayısını döndürür. En iyi uygulama, bir SELECT deyimi içinde ORDER BY yan tümcesi her zaman hello üst yan tümcesiyle birlikte kullanın. Bu toopredictably belirtmek hangi satırların üst tarafından etkilenen hello tek yoludur. 

**Sorgu**

    SELECT TOP 1 * 
    FROM Families f 

**Sonuçları**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

ÜST bir değişken değeri parametreli sorgular kullanmayı veya sabit bir değer (yukarıda gösterildiği gibi) ile kullanılabilir. Daha fazla ayrıntı için lütfen aşağıdaki parametreli sorgular bakın.

### <a id="Aggregates"></a>Toplama işlevleri
Toplamalar hello gerçekleştirebilirsiniz `SELECT` yan tümcesi. Toplama işlevleri, bir değerleri kümesi üzerinde bir hesaplama gerçekleştirmek ve tek bir değer döndürür. Örneğin, hello aşağıdaki sorguyu hello koleksiyonundaki ailesi belge hello sayısını döndürür.

**Sorgu**

    SELECT COUNT(1) 
    FROM Families f 

**Sonuçları**

    [{
        "$1": 2
    }]

Ayrıca hello skaler hello değerini toplama hello kullanarak dönebilirsiniz `VALUE` anahtar sözcüğü. Örneğin, hello aşağıdaki sorguyu Merhaba sayımını değerleri tek bir sayı döndürür:

**Sorgu**

    SELECT VALUE COUNT(1) 
    FROM Families f 

**Sonuçları**

    [ 2 ]

Filtrelerle birlikte toplamalar de gerçekleştirebilirsiniz. Örneğin, hello aşağıdaki sorguyu Merhaba sayımını hello adresi belgelerle hello Washington eyaleti yasalarına içinde döndürür.

**Sorgu**

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

**Sonuçları**

    [ 1 ]

Merhaba aşağıdaki tabloda hello listesini desteklenen toplama işlevleri DocumentDB API gösterir. `SUM`ve `AVG` ise sayısal değer üzerinde gerçekleştirilen `COUNT`, `MIN`, ve `MAX` numaraları, dizeleri, Boole değerlerini ve null değerlere gerçekleştirilebilir. 

| Kullanım | Açıklama |
|-------|-------------|
| SAYISI | Merhaba ifadesinde öğe sayısını döndürür hello. |
| TOPLA   | Merhaba ifadedeki tüm hello değerlerinin toplamını döndürür hello. |
| MIN   | Döndürür hello ifadedeki en küçük değer hello. |
| EN BÜYÜK   | Hello ifadedeki en büyük değeri döndürür hello. |
| ORTALAMA   | Merhaba ifadesinde hello değerlerin ortalamasını döndürür hello. |

Toplamalar, bir dizi yineleme hello sonuçlarını de gerçekleştirilebilir. Daha fazla bilgi için bkz: [dizi yineleme sorgularda](#Iteration).

> [!NOTE]
> Azure portal'ın sorgu Gezgini kullanarak hello zaman toplama sorguları sorgu sayfası kısmen toplanmış sonuçlar hello döndürebilir unutmayın. Hello SDK'ları, tek bir toplu değer tüm sayfalardaki üretir. 
> 
> Kod kullanarak tooperform toplama sorguları ihtiyacınız .NET SDK'sı 1.12.0, .NET Core SDK 1.1.0 veya Java SDK'sı 1.9.5 da sipariş veya üstü.    
>

## <a id="OrderByClause"></a>ORDER BY yan tümcesi
Gibi ANSI-SQL'de, isteğe bağlı bir Order By yan tümcesi sorgularken ekleyebilirsiniz. Merhaba yan tümcesi sonuçlar alınması gereken isteğe bağlı ASC/DESC bağımsız değişkeni toospecify hello sipariş içerebilir.

Örneğin, işte sorguda aileleri sırasına hello yerleşik Şehir kişinin adını alır.

**Sorgu**

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

**Sonuçları**

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

Burada da sorguda aileleri sayı temsil eden bir hello gibi dönem zamanı, yani, geçen süre 1 Ocak 1970'ten itibaren saniye cinsinden, depolanan oluşturma tarih sırasına göre alır.

**Sorgu**

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

**Sonuçları**

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <a id="Advanced"></a>Gelişmiş veritabanı kavramlarını ve SQL sorguları

### <a id="Iteration"></a>Yineleme
Yeni bir yapı hello eklenen **IN** DocumentDB API SQL tooprovide desteği, JSON diziler yineleme anahtar sözcük. Merhaba FROM kaynak yineleme için destek sağlar. Aşağıdaki örneğine hello ile başlayalım:

**Sorgu**

    SELECT * 
    FROM Families.children

**Sonuçları**  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

Şimdi hello koleksiyonundaki alt öğe üzerinden yineleme gerçekleştiren başka bir sorgu bakalım. Merhaba çıkış dizisi Hello fark unutmayın. Bu örnek böler `children` ve tek bir dizi hello sonuçları düzleştirir.  

**Sorgu**

    SELECT * 
    FROM c IN Families.children

**Sonuçları**  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

Bu, daha fazla hello aşağıdaki örnekte gösterildiği gibi hello dizinin her bir giriş üzerinde kullanılan toofilter olabilir:

**Sorgu**

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

**Sonuçları**  

    [{
      "givenName": "Lisa"
    }]

Dizi yineleme hello sonucunun üzerinde toplama de gerçekleştirebilirsiniz. Örneğin, hello aşağıdaki sorguyu hello tüm aileleri arasında alt sayar.

**Sorgu**

    SELECT COUNT(child) 
    FROM child IN Families.children

**Sonuçları**  

    [
      { 
        "$1": 3
      }
    ]

### <a id="Joins"></a>Birleşimler
İlişkisel bir veritabanında tablolar arasında hello gerek toojoin önemlidir. Merhaba normalleştirilmiş mantıksal corollary toodesigning şemaları kullanıcının. Bulmadýðýný toothis, DocumentDB API şemasız belgelerin hello Normalleştirilmemiş veri modeli ile ilgilidir. Bu hello mantıksal eşdeğerdir "Self Katıl" a.

Merhaba dili destekleyen hello sözdizimi < from_source1 > JOIN < from_source2 > birleştirme ediyor... < From_sourceN > katılın. Genel olarak, bu bir dizi döndürür **N**- diziler (ile tanımlama grubu **N** değerleri). Her tanımlama grubu tüm koleksiyon diğer adları kendi ilgili ayarlar yineleme tarafından üretilen değerler içeriyor. Diğer bir deyişle, tam bir çapraz ürün hello birleştirme katılan hello kümelerinin budur.

Merhaba aşağıdaki örneklerde hello JOIN yan tümcesi nasıl çalıştığı gösterilmektedir. Hello çapraz ürün kaynak ve boş her belge boş olduğundan aşağıdaki örneğine hello hello sonuç boş kalır.

**Sorgu**

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

**Sonuçları**  

    [{
    }]


Aşağıdaki örneğine hello hello birleştirme hello belge kökü hello arasında ise `children` subroot. Bu, iki JSON nesnesi arasındaki arası bir üründür. alt öğeleri olan bir dizi hello olgu biz hello alt öğeleri dizisi için tek bir kök çalışıyorsanız hello birleşim etkin değil. Bu nedenle Hello hello diziye sahip her bir belgenin vektörel çarpımını üretir tam olarak yalnızca bir belge beri hello sonucu yalnızca iki sonucu içerir.

**Sorgu**

    SELECT f.id
    FROM Families f
    JOIN f.children

**Sonuçları**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


Aşağıdaki örnek hello daha geleneksel bir birleştirme gösterir:

**Sorgu**

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

**Sonuçları**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



Merhaba ilk şey toonote bu hello olan `from_source` Merhaba, **katılma** yan tümcesi olan yineleyici. Bu nedenle, hello akışı bu durumda şu şekildedir:  

* Her alt öğesi genişletin **c** hello dizisindeki.
* Çapraz ürün hello belge hello kökü ile geçerli **f** her alt öğesi olan **c** hello ilk adımda düzleştirilmiş.
* Son olarak, hello kök nesnesi proje **f** name özelliği bırakır. 

Merhaba ilk belge (`AndersenFamily`) yalnızca tek bir nesnede karşılık gelen toothis belgesini hello sonuç kümesini içerecek şekilde yalnızca bir alt öğe içeriyor. Merhaba ikinci belge (`WakefieldFamily`) iki alt öğeleri içerir. Bu nedenle, hello çapraz ürün ayrı bir nesne için böylece her alt karşılık gelen toothis belge için iki nesne sonuçta her bir alt üretir. Her iki bu belgedeki alanlar hello kök hello aynı bir çapraz ürün beklendiği gibi.

Hello hello birleştirme gerçek yardımcı programı olan başka bir şekil hello cross-ürünün tooform diziler zor tooproject. Biz hello aşağıdaki örnekte gördüğünüz gibi Ayrıca, bir tanımlama grubu hello birleşimi olanak tanıyan hello filtre kullanıcı tarafından hello diziler genel memnun bir koşul seçti.

**Sorgu**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

**Sonuçları**

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



Bu örnek, örnek önceki hello doğal bir uzantıdır ve çift birleştirme gerçekleştirir. Bu nedenle, hello çapraz ürün sözde koddan hello görüntülenebilir:

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

`AndersenFamily`bir evcil hayvan sahip bir alt sahiptir. Bu nedenle, hello çapraz ürün bir satır verir (1\*1\*1) bu aile gelen. WakefieldFamily ancak iki alt öğe, ancak yalnızca bir alt "Jesse" Evcil Hayvanlar içeriyor. Jesse iki Evcil Hayvanlar yine de vardır. Bu nedenle hello çapraz ürün 1 verir\*1\*2 = 2 Bu ailesinden satırlar.

Merhaba sonraki örnekte olduğundan bir ek filtre `pet`. Merhaba Evcil adı "Gölge" olduğu tüm hello diziler dışlar. Biz mümkün toobuild diziler dizileri, herhangi bir hello tuple hello öğelerinin filtre gelen olan ve herhangi bir bileşimini hello öğeleri proje dikkat edin. 

**Sorgu**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

**Sonuçları**

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <a id="JavaScriptIntegration"></a>JavaScript tümleştirme
Azure Cosmos DB JavaScript tabanlı uygulama mantığını saklı yordamları ve Tetikleyicileri bakımından hello koleksiyonlar üzerinde doğrudan yürütmek için bir programlama modeli sağlar. Bu, her ikisi için sağlar:

* Özelliği toodo yüksek performanslı işlem CRUD işlemleri ve belgeleri hello doğrudan hello veritabanı altyapısının içinde JavaScript çalışma zamanı için derin tümleştirme, bir koleksiyondaki sorguları. 
* Denetim akışı, değişken kapsamı, atama ve özel durum işleme temelleri veritabanı işlemleri ile tümleştirilmesi doğal bir model. JavaScript tümleştirme için Azure Cosmos DB desteği hakkında daha fazla ayrıntı için lütfen toohello JavaScript sunucu tarafı programlama belgelerine bakın.

### <a id="UserDefinedFunctions"></a>Kullanıcı tanımlı işlevler (UDF'ler)
Bu makalede önceden tanımlanmış hello türleri ile birlikte DocumentDB API SQL kullanıcı tanımlı işlevler (UDF) için destek sağlar. Özellikle, skaler UDF'ler burada hello geliştiriciler sıfır veya daha çok değişkenlerinde geçirmek ve geri tek bağımsız değişken sonuç desteklenir. Bu değişkenin her biri geçerli JSON değerleri olmak için denetlenir.  

Merhaba DocumentDB API SQL söz dizimi, bu kullanıcı tanımlı işlevler kullanılarak toosupport özel uygulama mantığını genişletilir. UDF'ler DocumentDB API'si ile kayıtlı olması ve sonra bir SQL sorgusu bir parçası olarak başvurulan. Aslında, UDF'ler exquisitely olan hello sorgular tarafından çağrılan toobe tasarlanmıştır. Corollary toothis seçenek olarak, UDF'ler erişim toohello bağlam nesnesi, diğer JavaScript hello yoktur türleri (saklı yordamları ve Tetikleyicileri) sahip. Salt okunur olarak sorguları yürütmek olduğundan, birincil veya ikincil çoğaltmaları çalıştırabilirsiniz. Bu nedenle, UDF'ler diğer JavaScript türlerinin aksine ikincil çoğaltmalar üzerinde tasarlanmış toorun altındadır.

Aşağıda, özellikle bir belge koleksiyonu altında hello Cosmos DB veritabanı sırasında bir UDF nasıl kaydedilebilir bir örnektir.

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

Merhaba önceki örnekte oluşturur adı olan bir UDF `REGEX_MATCH`. İki JSON dizesi değerlerini kabul `input` ve `pattern` ve JavaScript'in string.match() işlevi kullanarak hello ilk eşleşmeleri hello düzeni belirtilen ikinci hello gerekmediğini denetler.

Bir yansıtma sorgu Biz bu UDF artık kullanabilirsiniz. UDF'ler hello büyük küçük harfe duyarlı önekiyle "udf." nitelenmiş olmalıdır gelen sorgulara çağrıldığında. 

> [!NOTE]
> Önceki too3/17/2015, Cosmos DB hello "udf." olmadan UDF çağrı desteklenir. önek seçin REGEX_MATCH() ister. Bu arama deseni kullanım dışı bırakıldı.  
> 
> 

**Sorgu**

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

**Sonuçları**

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

Merhaba UDF de bir filtre içinde de hello "udf ile." tam hello aşağıdaki örnekte, gösterildiği gibi kullanılabilir öneki:

**Sorgu**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

**Sonuçları**

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


Esas olarak, UDF'ler geçerli skaler ifadelerini ve tahminleri ve filtreleri kullanılabilir. 

tooexpand UDF'ler hello gücüyle başka bir örneğe koşullu mantığı ile bakalım:

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


Alıştırmaları UDF hello bir örnek aşağıda verilmiştir.

**Sorgu**

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

**Sonuçları**

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


Önceki örnekler gösterimi hello gibi UDF'ler JavaScript dil hello gücünü hello DocumentDB API SQL tooprovide ile bir zengin programlanabilir arabirimi toodo karmaşık yordam, koşullu mantık hello Yardım yerleşik JavaScript çalışma zamanı ile tümleştirme yetenekleri.

DocumentDB API SQL hello bağımsız değişkenleri toohello UDF'ler hello kaynağındaki her belge için hello geçerli aşamasında işleme hello UDF (WHERE yan tümcesi veya SELECT yan tümcesi) sağlar. Merhaba sonucu olarak dahil edilmiş genel yürütme ardışık düzeni sorunsuz bir şekilde hello. Başvurulan tooby hello UDF parametreleri hello parametre olarak kabul hello JSON değeri, kullanılabilir değil hello Özellikleri tanımlanmamış ve bu nedenle hello UDF çağırma tamamen atlanır. Benzer şekilde hello UDF Hello sonucu tanımsız ise hello sonucunda bulunmaz. 

Özet olarak, UDF'ler harika Araçlar toodo karmaşık iş mantığı hello sorgu kapsamında ' dir.

### <a name="operator-evaluation"></a>İşleç değerlendirme
Cosmos DB, bir JSON veritabanı olma hello virtue tarafından JavaScript işleçleri ve değerlendirme semantiği ile parallels çizer. Cosmos DB toopreserve JavaScript semantiği JSON desteği bakımından çalışır, ancak bazı durumlarda hello işlemi değerlendirme farklıdır.

Merhaba değerleri veritabanından kadar DocumentDB API SQL'de aksine geleneksel SQL değerlerin hello türleri bilinmez genellikle. Sipariş tooefficiently sorguları yürütün, hello işleçleri çoğunu sıkı tür gereksinimleri vardır. 

DocumentDB API SQL JavaScript aksine örtük dönüşümler gerçekleştirmez. Örneğin, bir sorgu ister `SELECT * FROM Person p WHERE p.Age = 21` eşleşen değeri olan 21 yaş özelliği içeren belgeleri. "021", "21.0", "0021", "00021" dize "21", veya diğer büyük olasılıkla sonsuz Çeşitlemeler, yaş özelliği eşleşen herhangi bir belge ister, vb. eşlenemiyor. Buna karşılık toohello hello dize değerlerini örtük olarak Integer toonumbers nerede JavaScript budur (örneğin, operatöre dayanan: ==). Bu seçenek, DocumentDB API SQL'de eşleşen verimli dizin için önemlidir. 

## <a name="parameterized-sql-queries"></a>Parametreli SQL sorguları
Cosmos DB hello @ gösterimi tanıdık ile ifade parametrelerle sorguları destekler. Parametreli SQL sağlam işleme ve kullanıcı girişi, SQL ekleme üzerinden veri yanlışlıkla açığa çıkmaya önleme, kaçış sağlar. 

Örneğin, Soyadı ve adres durumu kullandığı parametreler bir sorgu yazın ve son adı ve kullanıcı girişini temel alarak adresi durumunun çeşitli değerlerin yürütün.

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

Bu istek ardından aşağıda gösterildiği gibi tooCosmos DB parametreli bir JSON sorgu olarak gönderilebilir.

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

Merhaba bağımsız değişkeni tooTOP gibi parametreli sorgular kullanmayı aşağıda gösterilen ayarlanabilir.

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

Parametre değerleri geçerli bir JSON olabilir (dizeler, sayılar, Boole değerlerini, null, hatta dizileri veya JSON iç içe geçmiş). Ayrıca parametreleri Cosmos DB Şeması daha az olduğundan, karşı herhangi bir tür doğrulanmaz.

## <a id="BuiltinFunctions"></a>Yerleşik işlevler
Cosmos DB yerleşik işlevleri gibi kullanıcı tanımlı işlevler (UDF'ler) sorguları içinde kullanılan ortak işlemleri için de destekler.

| İşlev grubu          | İşlemler                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Matematik işlevleri  | ABS TAVAN, EXP, FLOOR, günlük, LOG10, güç, HEPSİNİ, oturum, SQRT, KARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, derece, PI, radyan, SIN ve TAN |
| Denetimi işlevleri yazın | IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED ve IS_PRIMITIVE                                                           |
| Dize işlevleri        | CONCAT, içerir, ENDSWITH, INDEX_OF, sol, uzunluk, alt, LTRIM, Değiştir, çoğaltılması, geriye doğru sağ, RTRIM, STARTSWITH, SUBSTRING ve üst       |
| Dizi işlevleri         | ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH ve ARRAY_SLICE                                                                                         |
| Uzamsal işlevleri       | St_dıstance, ST_WITHIN, ST_INTERSECTS, ST_ISVALID ve ST_ISVALIDDETAILED                                                                           | 

Şu anda yerleşik işlevi olduğu şimdi kullanılabilir bir kullanıcı tanımlı işlev (UDF) kullanıyorsanız, toobe daha hızlı toorun ve daha fazlasını geçiyor gibi hello karşılık gelen yerleşik işlevi kullanmalıdır verimli bir şekilde. 

### <a name="mathematical-functions"></a>Matematik işlevleri
Merhaba matematik işlevleri her bağımsız değişken olarak sağlanır ve sayısal bir değeri döndürme giriş değerlerine göre bir hesaplama gerçekleştirir. Burada, desteklenen yerleşik matematik işlevleri tablosu verilmiştir.


| Kullanım | Açıklama |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [[ABS (num_expr)](#bk_abs) | Sayısal ifade döndürür hello mutlak (pozitif) değerini hello belirtildi. |
| [Üst SINIRA (num_expr)](#bk_ceiling) | En küçük tamsayı değeri büyük hello veya belirtilen sayısal ifade hello eşit verir. |
| [FLOOR (num_expr)](#bk_floor) | Daha az Hello en büyük tamsayıyı döndürür veya bu değere eşit toohello sayısal ifade belirtildi. |
| [EXP (num_expr)](#bk_exp) | Merhaba, döndürür hello üs sayısal ifade belirtildi. |
| [Günlük (num_expr [, temel])](#bk_log) | Sayısal ifade hello hello doğal logaritmasını döndürür belirtilen veya hello kullanarak hello logaritmanın tabanı belirtilen |
| [Log10 (num_expr)](#bk_log10) | Merhaba, döndürür hello 10 tabanında Logaritmik değer sayısal ifade belirtildi. |
| [ROUND (num_expr)](#bk_round) | Yuvarlak toohello en yakın tamsayı değeri sayısal bir değer döndürür. |
| [TRUNC (num_expr)](#bk_trunc) | Kesilmiş toohello en yakın tamsayı değeri sayısal bir değer döndürür. |
| [SQRT (num_expr)](#bk_sqrt) | Merhaba hello kare kökünü döndürür sayısal ifade belirtildi. |
| [KARE (num_expr)](#bk_square) | Merhaba kare döndürür hello sayısal ifade belirtildi. |
| [GÜÇ (num_expr, num_expr)](#bk_power) | Sayısal ifade toohello değeri belirtilen döndürür hello hello gücünü belirtilmiş. |
| [OTURUM (num_expr)](#bk_sign) | Döndürür hello oturum değerini (-1, 0, 1) hello sayısal ifade belirtildi. |
| [ACOS (num_expr)](#bk_acos) | Kosinüsü belirtilen sayısal ifade hello radyan cinsinden döndürür hello açı; arccosine olarak da bilinir. |
| [ASIN (num_expr)](#bk_asin) | Döndürür hello açının sinüsü hello olduğundan, sayısal ifade radyan cinsinden. Bu arksinüsünü olarak da adlandırılır. |
| [ATAN (num_expr)](#bk_atan) | Döndürür hello açının tanjantı hello olduğundan, sayısal ifade radyan cinsinden. Bu arktanjantını olarak da adlandırılır. |
| [ATN2 (num_expr)](#bk_atn2) | Döndürür hello hello pozitif x ekseni ve hello ray hello kaynak toohello noktasından (y, x) arasında radyan cinsinden açı burada x ve y hello hello iki belirtilen float ifadeleri değerleri. |
| [COS (num_expr)](#bk_cos) | Döndürür hello trigonometrik kosinüsünü hello radyan cinsinden açı, hello ifade belirtildi. |
| [COT (num_expr)](#bk_cot) | Döndürür hello trigonometrik kotanjantını hello radyan cinsinden açı, hello sayısal ifade belirtildi. |
| [DERECE (num_expr)](#bk_degrees) | Karşılık gelen açıyı radyan cinsinden açı için derece cinsinden döndürür hello. |
| [PI)](#bk_pi) | PI sayısının sabit bir değer döndürür hello. |
| [Radyan CİNSİNDEN (num_expr)](#bk_radians) | Derece sayısal bir ifadenin girildiğinde radyan cinsinden döndürür. |
| [SIN (num_expr)](#bk_sin) | Döndürür hello trigonometrik sinüsünü hello radyan cinsinden açı, hello ifade belirtildi. |
| [TAN (num_expr)](#bk_tan) | Merhaba içinde hello giriş ifadesi döndürür hello tanjantını ifade belirtildi. |

Örneğin, şimdi sorguları hello aşağıdaki gibi çalıştırabilirsiniz:

**Sorgu**

    SELECT VALUE ABS(-4)

**Sonuçları**

    [4]

Cosmos veritabanı işlevleri karşılaştırıldığında tooANSI SQL arasındaki temel fark Hello bunlar iyi şema küçüktür ve karma şema verilerle tasarlanmış toowork olmasıdır. Örneğin, burada hello boyut özelliği eksik veya sahip bir belgeniz varsa "bilinmiyor" gibi bir sayısal olmayan değer sonra hello belge üzerinde bir hata döndürüyor yerine atlanır.

### <a name="type-checking-functions"></a>Denetimi işlevleri yazın
Merhaba tür denetimi işlevleri içinde SQL sorguları ifade toocheck hello türü izin verin. Denetimi işlevleri olabilir türü değişken veya bilinmeyen olduğunda toodetermine hello türü belgelerde özelliklerinin hello anında kullanılır. Burada, desteklenen yerleşik tür işlevleri denetlemesini tablosu verilmiştir.

<table>
<tr>
  <td><strong>Kullanım</strong></td>
  <td><strong>Açıklama</strong></td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (ifade)</a></td>
  <td>Merhaba değerin Hello türü bir dizi olup olmadığını gösteren bir Boole değeri döndürür.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (ifade)</a></td>
  <td>Hello türde bir hello değer bir Boole değeri olup olmadığını gösteren bir Boole değeri döndürür.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (ifade)</a></td>
  <td>Merhaba değerin Hello türü null olup olmadığını gösteren bir Boole değeri döndürür.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (ifade)</a></td>
  <td>Hello türde bir hello değer bir sayı olup olmadığını gösteren bir Boole değeri döndürür.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (ifade)</a></td>
  <td>Merhaba değerin Hello türü bir JSON nesnesi olup olmadığını gösteren bir Boole değeri döndürür.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (ifade)</a></td>
  <td>Merhaba değerin Hello türü bir dize olup olmadığını gösteren bir Boole değeri döndürür.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (ifade)</a></td>
  <td>Başlangıç özellik değeri atanmış olan gösteren bir Boole değeri döndürür.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (ifade)</a></td>
  <td>Merhaba değerin Hello türü bir dize, sayı, Boole veya null olup olmadığını gösteren bir Boole değeri döndürür.</td>
</tr>

</table>

Bu işlevler kullanılarak, şimdi sorguları hello aşağıdaki gibi çalıştırabilirsiniz:

**Sorgu**

    SELECT VALUE IS_NUMBER(-4)

**Sonuçları**

    [true]

### <a name="string-functions"></a>Dize işlevleri
Merhaba aşağıdaki skaler işlevler dize giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir dize, sayısal ya da Boole değeri döndürür. Yerleşik dize işlevleri tablosu aşağıdadır:

| Kullanım | Açıklama |
| --- | --- |
| [UZUNLUĞU (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |Dize ifadesi döndürür hello hello karakter sayısı belirtilen |
| [CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat) |İki veya daha fazla dize değerlerini birleştirme hello sonucu olan bir dize döndürür. |
| [SUBSTRING (str_expr, num_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |Bir dize ifadesi bölümünü döndürür. |
| [STARTSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |Merhaba ilk dize ifadesi ile Merhaba ikinci bitip olup olmadığını gösteren bir Boole değeri döndürür |
| [ENDSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |Merhaba ilk dize ifadesi ile Merhaba ikinci bitip olup olmadığını gösteren bir Boole değeri döndürür |
| [İÇERİR (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |Merhaba ilk dize ifadesi hello ikinci içerip içermediğini gösteren bir Boole değeri döndürür. |
| [INDEX_OF (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |Merhaba dize bulunmazsa hello ikinci dize ifadesi hello ilk belirtilen dize ifadesi veya -1 içinde hello ilk oluşum konumunu başlangıç hello döndürür. |
| [Sol (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |Döndürür hello sol bölümü bir dizenin belirtilen hello ile karakter sayısı. |
| [SAĞ (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |Karakter sayısını döndürür hello dizesi sağ parçası hello ile belirtilen. |
| [LTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |Öndeki boşlukları kaldırır sonra bir dize ifadesi döndürür. |
| [RTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |Tüm sondaki boşlukları kesilmesi sonrasında bir dize ifadesi döndürür. |
| [Alt (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |Büyük harf karakter veri toolowercase dönüştürmeden sonra bir dize ifadesi döndürür. |
| [ÜST (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |Küçük harf karakter veri toouppercase dönüştürmeden sonra bir dize ifadesi döndürür. |
| [REPLACE (str_expr, str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |Belirtilen dize değeri tüm oluşumlarını başka bir dize değeri ile değiştirir. |
| [REPLICATE (str_expr, num_expr)](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |Bir dize değeri, belirtilen sayıda yineler. |
| [Ters (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |Merhaba ters sırada bir dize değerini döndürür. |

Bu işlevleri kullanarak, artık hello aşağıdaki gibi sorguları çalıştırabilirsiniz. Örneğin, size hello aile adı büyük şu şekilde döndürebilirsiniz:

**Sorgu**

    SELECT VALUE UPPER(Families.id)
    FROM Families

**Sonuçları**

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

Veya bu örnekteki gibi dizeyi birleştirmek:

**Sorgu**

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

**Sonuçları**

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


Dize işlevleri, hello yan tümcesi toofilter sonuçları, aşağıdaki örneğine hello oluşturulacağı yeri de kullanılabilir:

**Sorgu**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

**Sonuçları**

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a>Dizi işlevleri
skaler işlevler aşağıdaki hello bir dizi giriş değeri ve return sayısal, Boole veya dizi değer üzerinde bir işlemi gerçekleştirin. Yerleşik dizi işlevleri tablosu aşağıdadır:

| Kullanım | Açıklama |
| --- | --- |
| [ARRAY_LENGTH (arr_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |Dizi ifadesi belirtilen döndürür hello hello öğelerinin sayısı. |
| [ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat) |İki veya daha fazla dizi değerlerini birleştirme hello sonucu olan bir dizi döndürür. |
| [ARRAY_CONTAINS (arr_expr, ifade [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains) |Belirtilen değer hello dizi hello içerip içermediğini gösteren Boole değeri döndürür. Merhaba eşleşme tam veya kısmi olup olmadığını belirtebilirsiniz. |
| [ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice) |Bir dizi ifadesi bölümünü döndürür. |

Dizi işlevleri JSON içinde kullanılan toomanipulate diziler olabilir. Örneğin, "Deneme Wakefield" olduğu bir hello üst tüm belgeleri döndüren bir sorgu aşağıdadır. 

**Sorgu**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

**Sonuçları**

    [{
      "id": "WakefieldFamily"
    }]

Merhaba dizi eşleşen öğeleri için kısmi bir parça belirtebilirsiniz. Merhaba aşağıdaki sorgu bulur hello ile tüm üst `givenName` , `Robin`.

**Sorgu**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

**Sonuçları**

    [{
      "id": "WakefieldFamily"
    }]


Burada, ARRAY_LENGTH tooget hello ailesi başına alt sayısını kullanan başka bir örnek verilmiştir.

**Sorgu**

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

**Sonuçları**

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a>Uzamsal işlevleri
Cosmos DB Jeo-uzamsal sorgulamak için yerleşik işlevler açık Jeo-uzamsal Konsorsiyumu (OGC) aşağıdaki hello destekler. 

<table>
<tr>
  <td><strong>Kullanım</strong></td>
  <td><strong>Açıklama</strong></td>
</tr>
<tr>
  <td>St_dıstance (point_expr, point_expr)</td>
  <td>Merhaba iki GeoJSON noktası, çokgen veya LineString ifadeleri arasında Hello uzaklığını döndürür.</td>
</tr>
<tr>
  <td>ST_WITHIN (point_expr, polygon_expr)</td>
  <td>Merhaba ilk GeoJSON nesne (noktası, çokgen veya LineString) hello ikinci GeoJSON nesne içinde (noktası, çokgen veya LineString) olup olmadığını gösteren bir Boole ifadesi döndürür.</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Merhaba iki belirtilen GeoJSON nesne (noktası, çokgen veya LineString) kesiştiği olup olmadığını gösteren bir Boole ifadesi döndürür.</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Merhaba GeoJSON noktası, çokgen veya LineString ifadesi geçerli belirtilen olup olmadığını gösteren bir Boole değeri döndürür.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Merhaba GeoJSON noktası, çokgen veya LineString ifade belirtilmişse bir Boole değeri içeren bir JSON değeri geçerli değil ve geçersiz, ayrıca bir dize değeri olarak neden hello döndürür.</td>
</tr>
</table>

Uzamsal işlevleri kullanılan tooperform yakınlık sorguları uzamsal veri olabilir. Örneğin, tüm ailesi hello st_dıstance yerleşik işlevi belirtilen konum içinde 30 km hello birini kullanarak belgeleri döndüren bir sorgu aşağıdadır. 

**Sorgu**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Sonuçları**

    [{
      "id": "WakefieldFamily"
    }]

Cosmos DB Jeo-uzamsal desteği hakkında daha fazla ayrıntı için lütfen bkz. [Azure Cosmos veritabanı Jeo-uzamsal verilerle çalışma](geospatial.md). Cosmos DB için uzamsal işlevleri ve hello SQL söz dizimi, sarmalar. Şimdi nasıl çalışır ve hello sözdizimi ile nasıl etkileşim kurduğu sorgulama LINQ kadarki gördük bir bakalım.

## <a id="Linq"></a>LINQ tooDocumentDB API SQL
LINQ, hesaplama nesnelerin akışları sorgular olarak ifade eder ve .NET çalışan bir programlama modelidir. JSON ve .NET nesneleri arasında dönüştürme kolaylaştırarak LINQ ile bir istemci-tarafı kitaplığı toointerface cosmos DB sağlar ve bir alt kümesini LINQ eşlemesinden tooCosmos DB sorguları. 

Merhaba resimde Cosmos DB kullanarak LINQ sorgularını destekleme hello mimari gösterilmektedir.  Merhaba Cosmos DB İstemcisi'ni kullanarak geliştiriciler oluşturabilir bir **Iqueryable** Cosmos DB sorgu sağlayıcısı sorguları hello doğrudan o hello LINQ sorgusu Cosmos DB sorguda çevirir, nesne. Merhaba sorgu daha sonra JSON biçiminde toohello Cosmos DB sunucusu tooretrieve sonuç kümesi geçirilir. Merhaba, sonuçları hello istemci tarafında .NET nesnelerin bir akışa seri durumdan çıkarılmış döndürdü.

![DocumentDB API - kullanarak LINQ sorgularını SQL söz dizimi, JSON sorgu dili, veritabanı kavramlarını ve SQL sorguları destekleyen mimarisi][1]

### <a name="net-and-json-mapping"></a>.NET ve JSON eşleme
.NET nesneleri ve JSON belgeleri arasında Hello eşleme doğal - her bir veri üyesi alanına eşlenen hello alan adı olduğu tooa JSON nesnesi eşlenen toohello "anahtarı" Merhaba nesnesinin bir parçası ve Başlangıç "değeri" parçasıdır eşlenen yinelemeli olarak toohello değeri hello nesnesinin bir parçası. Aşağıdaki örnek hello göz önünde bulundurun: oluşturulan hello ailesi nesnesidir eşlenen toohello JSON belgesi aşağıda gösterildiği gibi. Ve tersi yönde hello JSON belgesi eşlenen geri tooa .NET nesnedir.

**C# sınıfı**

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


**JSON**  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-toosql-translation"></a>LINQ tooSQL çevirisi
Merhaba Cosmos DB sorgu sağlayıcısı en iyi çaba eşleme Cosmos DB SQL sorgusu bir LINQ Sorgu gerçekleştirir. Açıklama aşağıdaki hello hello okuyucu LINQ temel bilgisi içeriyor varsayalım.

İlk olarak, hello tür sistemi için tüm JSON ilkel türler – sayısal türler, boolean, dize ve null destekliyoruz. Yalnızca bu JSON türleri desteklenir. skaler ifadelerin aşağıdaki hello desteklenir.

* Sabit değerler – bunlar hello sorgu değerlendirilir hello zamanında hello temel veri türlerinin sabit değerleri içerir.
* Özellik/dizi dizini ifadeleri – bu ifadeler toohello özelliğinin bir nesneyi veya bir dizi öğesine bakın.
  
     ailesi. Kimliği;    Family.Children[0].familyName;    Family.Children[0].grade;    Family.Children[n].grade; n bir int değişkenidir
* Aritmetik ifadeler - bunlar ortak aritmetik ifadeler sayısal ve Boole değerleri içerir. Merhaba tam listesi için toohello SQL belirtimine bakın.
  
     2 * family.children[0].grade;    x + y;
* Dize karşılaştırma ifadesi - bunlar bir dize değeri toosome sabit dize değeri karşılaştırma içerir.  
  
     mother.familyName == "Smith";    child.givenName s; == bir dize değişkeni s'dir
* Nesne/oluşturma ifadesi - dönüş Bu deyimler bileşik değer türü veya anonim tür bir nesneyi veya bir dizi tür nesneler dizisi. Bu değerleri iç içe.
  
     Yeni üst {familyName givenName "Smith" = "Can" =}; Yeni {ilk = 1, ikincisi 2 =}; iki alan sahip anonim bir tür              
     Yeni int [] {3, child.grade, 5};

### <a id="SupportedLinqOperators"></a>Desteklenen LINQ işleçlerin listesi
Merhaba LINQ sağlayıcısında hello DocumentDB .NET SDK'sı ile dahil desteklenen LINQ işleçlerin bir listesi aşağıda verilmiştir.

* **Seçin**: tahminleri Çevir toohello SQL nesne oluşturması dahil olmak üzere seçin
* **Burada**: filtreleri SQL WHERE toohello çevirin ve Destek arasında çeviri & &, || ve! toohello SQL işleçleri
* **SelectMany**: diziler toohello SQL JOIN yan tümcesinde geriye doğru izleme sağlar. Dizi öğeleri üzerinde kullanılan toochain/nest ifadeleri toofilter olabilir
* **OrderBy ve OrderByDescending**: tooORDER BY artan/azalan çevirir
* **Count**, **toplam**, **Min**, **Max**, ve **ortalama** toplama ve zaman uyumsuz eşdeğerlerine işleçleri **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, ve **AverageAsync**.
* **CompareTo**: toorange karşılaştırmaları çevirir. .NET ile karşılaştırılabilir değilseniz bu yana dizeleri için yaygın olarak kullanılan
* **Ele**: toohello SQL üst bir sorgunun sonuçlarına sınırlamak için çevirir.
* **Matematik işlevleri**: çevrilmesi destekler. NET'in Abs, Acos, Asin Cos tavan Atan Exp, Floor, günlük, Log10, Pow, hepsini, oturum, Sin, Sqrt, Tan, Truncate toohello eşdeğer SQL yerleşik işlevleri.
* **Dize işlevleri**: çevrilmesi destekler. NET'in Concat, içerir, EndsWith, IndexOf, Count, ToLower, TrimStart, Değiştir, tersine, TrimEnd, StartsWith, SubString, ToUpper toohello eşdeğer SQL yerleşik işlevler.
* **Dizi işlevleri**: çevrilmesi destekler. NET'in Concat, içerir ve sayısı toohello eşdeğer SQL yerleşik işlevler.
* **Jeo-uzamsal uzantı işlevleri**: saplama yöntemlerden içinde IsValid, uzaklığı çeviri destekler ve IsValidDetailed toohello eşdeğer SQL yerleşik işlevleri.
* **Kullanıcı tanımlı işlev uzantı işlevi**: hello destekler çevrilmesi saplama yöntemi UserDefinedFunctionProvider.Invoke toohello karşılık gelen kullanıcı tanımlı işlev.
* **Çeşitli**: koşullu işleçler ve hello çevrilmesi birleşim destekler. CONTAINS tooString çevirebilir içerir, ARRAY_CONTAINS veya hello SQL IN bağlamı bağlı olarak.

### <a name="sql-query-operators"></a>SQL sorgu işleçleri
Aşağıda, bazı hello standart LINQ Sorgu işleçleri tooCosmos DB sorguları nasıl dönüştürüleceğini gösteren bazı örnekler verilmiştir.

#### <a name="select-operator"></a>İşleç Seç
Merhaba sözdizimi `input.Select(x => f(x))`, burada `f` skaler bir ifade değil.

**LINQ lambda ifadesi**

    input.Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



**LINQ lambda ifadesi**

    input.Select(family => family.children[0].grade + c); // c is an int variable


**SQL** 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



**LINQ lambda ifadesi**

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


**SQL** 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a>SelectMany işleci
Merhaba sözdizimi `input.SelectMany(x => f(x))`, burada `f` koleksiyon türü döndüren bir skaler ifade.

**LINQ lambda ifadesi**

    input.SelectMany(family => family.children);

**SQL** 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a>Burada işleci
Merhaba sözdizimi `input.Where(x => f(x))`, burada `f` bir Boole değeri döndürür skaler bir ifade değil.

**LINQ lambda ifadesi**

    input.Where(family=> family.parents[0].familyName == "Smith");

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



**LINQ lambda ifadesi**

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a>Bileşik SQL sorguları
Hello işleçleri yukarıda oluşturulan tooform daha güçlü sorgular olabilir. Cosmos DB iç içe geçmiş koleksiyonları desteklediğinden hello birleşim birleştirilmiş iç içe geçmiş ya da.

#### <a name="concatenation"></a>Birleştirme
Merhaba sözdizimi `input(.|.SelectMany())(.Select()|.Where())*`. Birleştirilmiş bir sorgu ile isteğe bağlı başlatabilirsiniz `SelectMany` sorgu birden fazla ardından `Select` veya `Where` işleçler.

**LINQ lambda ifadesi**

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

**SQL**

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



**LINQ lambda ifadesi**

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



**LINQ lambda ifadesi**

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



**LINQ lambda ifadesi**

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

**SQL** 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a>İç içe geçme
Merhaba sözdizimi `input.SelectMany(x=>x.Q())` Q olduğu bir `Select`, `SelectMany`, veya `Where` işleci.

İç içe bir sorgu hello iç sorgu uygulanan tooeach hello dış toplama öğesidir. Bir önemli özelliği hello iç sorgu toohello alanları gibi hello dış koleksiyonundaki hello öğelerinin başvuruda bulunabilir kendi kendine birleştirir.

**LINQ lambda ifadesi**

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

**SQL** 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


**LINQ lambda ifadesi**

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



**LINQ lambda ifadesi**

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <a id="ExecutingSqlQueries"></a>SQL sorguları yürütme
Cosmos DB herhangi bir dil tarafından HTTP/HTTPS istekleri çağrılabilir bir REST API'si aracılığıyla kaynaklarını kullanıma sunar. Ayrıca, Cosmos DB .NET, Node.js, JavaScript ve Python gibi çeşitli popüler dilde programlama kitaplıkları sunar. Merhaba REST API ve hello tüm çeşitli kitaplıkları SQL sorgulama destekler. Merhaba .NET SDK ayrıca tooSQL sorgulama LINQ destekler.

örneklerde nasıl aşağıdaki hello toocreate bir sorgu ve Cosmos DB veritabanı hesabı karşı gönderin.

### <a id="RestAPI"></a>REST API'Sİ
Cosmos DB HTTP üzerinden açık bir RESTful programlama modeli sunar. Bir Azure aboneliği kullanarak veritabanı hesaplarını sağlanabilir. Merhaba Cosmos DB kaynak modeli kaynaklar her biri mantıksal ve kararlı bir URI kullanılarak adreslenebilir bir veritabanı hesabı altında bir dizi oluşur. Başvurulan tooas bu belgede bir akış kaynakları kümesidir. Veritabanı hesabı her birden çok koleksiyonu kapsayan bir veritabanları kümesi oluşur belgeleri, UDF'ler ve diğer kaynak türlerini her hangi içinde dönüş içerebilir.

Hello temel etkileşim bu kaynaklarla hello HTTP fiilleri GET, PUT, POST ve silme ile standart kullanıcıların yorumu modelidir. Merhaba POST fiil yeni bir kaynak oluşturulmasını, bir saklı yordamı yürütmek veya Cosmos DB sorgu verme için kullanılır. Sorguları her zaman salt okunur hiçbir yan etkileri olan işlemleridir.

Merhaba Aşağıdaki örnekler biz kadarki geçirdikten hello iki örnek belgeleri içeren bir koleksiyon karşı yapılan bir DocumentDB API sorgu için bir POST gösterir. Merhaba sorgu hello JSON name özelliğine göre basit bir filtre yok. Not hello hello `x-ms-documentdb-isquery` ve Content-Type: `application/query+json` işlemi hello üstbilgileri toodenote olan bir sorgu.

**İstek**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


**Sonuçları**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


Merhaba ikinci örneği birden çok sonuç hello birleştirme sonucu döndürür daha karmaşık bir sorgu gösterir.

**İstek**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


**Sonuçları**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


Bir sorgunun sonuçları sonuçlar tek sayfalık içinde sığamıyorsa sonra hello REST API aracılığıyla hello devamlılık belirteci döndürür `x-ms-continuation-token` yanıtı üstbilgisi. İstemcileri sonraki sonuçlarında hello üstbilgi dahil olmak üzere sonuçları sayfalara bölme. Sayfa başına sonuç Hello sayısı hello da denetlenebilir `x-ms-max-item-count` numara üstbilgi. Belirtilen sorgu Hello gibi bir toplama işlevi varsa `COUNT`, hello sorgu sayfası kısmen toplu değer sonuç hello sayfasını döndürebilir sonra. Merhaba istemcileri, bu sonuçları tooproduce hello son sonuçları, örneğin üzerinden ikinci düzey toplama gerçekleştirmek, hello tek tek sayfaları tooreturn hello toplam sayısı döndürülen hello sayıları üzerinden toplayın.

sorguları, kullanım hello için toomanage hello veri tutarlılığı İlkesi `x-ms-consistency-level` tüm REST API istekleri gibi üstbilgi. Oturum tutarlılığı için gerekli tooalso echo hello son olmasından `x-ms-session-token` hello sorgu isteği, tanımlama bilgisi üstbilgisi. Merhaba sorgulanan koleksiyonunun dizin oluşturma ilkesini de sorgu sonuçları hello tutarlılığını etkileyebilir. Merhaba varsayılan dizin oluşturma ilkesi ayarları, koleksiyonlar için hello her zaman geçerli hello belge içeriklerini ve sorgu sonuçları için veri seçilen hello tutarlılık eşleşen dizinidir. Dizin oluşturma ilkesi hello gevşek tooLazy ise, sorgular eski sonuçlar döndürebilir. Daha fazla bilgi için bkz: [Azure Cosmos DB tutarlılık düzeylerini][consistency-levels].

Yapılandırılmış hello dizin oluşturma ilkesini hello koleksiyonunda hello belirtilen sorgu destekleyemiyorsa, 400 "hatalı istek" Merhaba Azure Cosmos DB sunucusu döndürür. Bu karma (eşitlik) aramaları için ve dizine almasını açıkça yolları için yapılandırılmış yolları aralığı sorguları için döndürülür. Merhaba `x-ms-documentdb-query-enable-scan` bir dizini olmadığında belirtilen tooallow hello sorgu tooperform bir tarama üstbilgisi olabilir.

Ayrıntılı ölçümler ayarlayarak sorgu yürütme elde edebilirsiniz `x-ms-documentdb-populatequerymetrics` üstbilgisi çok`True`. Daha fazla bilgi için bkz: [SQL sorgu ölçümleri Azure Cosmos DB DocumentDB API'si](documentdb-sql-query-metrics.md).

### <a id="DotNetSdk"></a>C# (.NET) SDK
LINQ ve SQL Hello .NET SDK'yı destekleyen sorgulama. Merhaba aşağıdaki örnekte nasıl tooperform hello basit filtre sorgusu bu belgenin önceki bölümlerinde sunulan gösterilmektedir.

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


Bu örnek her belge içinde eşitlik için iki özellik karşılaştırır ve anonim tahminleri kullanır. 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


Merhaba sonraki örnek LINQ SelectMany ifade birleştirmeler gösterir.

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



Merhaba .NET istemci otomatik olarak yukarıda gösterildiği gibi hello foreach blokları sorgu sonuçlarında tüm hello sayfalarında dolaşır. Merhaba REST API bölümünde sunulan seçenekleri kullanılabilir ayrıca hello sorgu hello hello kullanarak .NET SDK'SININ `FeedOptions` ve `FeedResponse` hello CreateDocumentQuery yöntemi sınıflarda. Sayfa sayısı Hello hello kullanılarak denetlenebilir `MaxItemCount` ayarı. 

Disk belleği oluşturarak açıkça kontrol edebilirsiniz `IDocumentQueryable` hello kullanarak `IQueryable` okuyarak ardından nesne` ResponseContinuationToken` değerleri ve bunları geçirme geri olarak `RequestContinuationToken` içinde `FeedOptions`. `EnableScanInQuery`Merhaba sorgu yapılandırılmış hello dizin oluşturma ilkesi tarafından desteklendiğinde kümesi tooenable taramaları olabilir. Bölümlenmiş koleksiyonlar için kullandığınız `PartitionKey` toorun hello sorgusu tek bir bölüm (Cosmos DB otomatik olarak bu hello sorgu metinden ayıklayabilirsiniz rağmen), ve `EnableCrossPartitionQuery` toobe gerekebilir toorun sorgularını kullanarak birden çok bölüm karşı çalıştırabilirsiniz. 

Çok başvuran[Azure Cosmos DB .NET örnekleri](https://github.com/Azure/azure-documentdb-net) sorguları içeren daha fazla örnekleri için. 

### <a id="JavaScriptServerSideApi"></a>JavaScript sunucu tarafı API
Cosmos DB doğrudan saklı yordamları ve Tetikleyicileri kullanarak hello koleksiyonlar üzerinde temel JavaScript uygulama mantığının yürütmek için bir programlama modeli sağlar. bir koleksiyon düzeyinde kayıtlı hello JavaScript mantığı, ardından koleksiyonu verilen hello hello işlemlerini hello belgelerde veritabanı işlemlerini verebilir. Bu işlemler çevresel ACID işlemlerini sarılır.

Merhaba aşağıdaki örnek alanından toouse hello queryDocuments hello JavaScript sunucu API'sini toomake içinde nasıl sorgular gösterir iç saklı yordamları ve Tetikleyicileri.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <a id="References"></a>Başvuruları
1. [Giriş tooAzure Cosmos DB][introduction]
2. [Azure Cosmos veritabanı SQL belirtimi](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [Azure Cosmos DB .NET örnekleri](https://github.com/Azure/azure-documentdb-net)
4. [Azure Cosmos DB tutarlılık düzeyleri][consistency-levels]
5. ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)
6. JSON [http://json.org/](http://json.org/)
7. JavaScript belirtimi [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm) 
8. LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx) 
9. Sorgu büyük veritabanları için değerlendirme teknikleri [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)
10. Sorgu 1994 paralel ilişkisel veritabanı sistemleri, IEEE bilgisayar topluluğu basın, işleme
11. Lu, Ooi, Bronz, sorgu 1994 paralel ilişkisel veritabanı sistemleri, IEEE bilgisayar topluluğu basın, işleme.
12. Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Barış Tomkins: Pig Latin: veri işleme, SIGMOD 2008 için Not şekilde yabancı dil.
13. G. Graefe. sorgu iyileştirme için Hello basamaklar çerçevesi. IEEE veri Müh Bull., 18(3): 1995.

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md