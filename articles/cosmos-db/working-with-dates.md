---
title: "Azure Cosmos veritabanı tarihlerle aaaWorking | Microsoft Docs"
description: "Toowork ile Azure Cosmos DB'de nasıl tarihleri hakkında bilgi edinin."
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: e587772f-ce9f-498c-a017-a51e7265bb23
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 27ec170e4bef72c0b5b456738f1275ef02543024
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a>Azure Cosmos DB tarihleri ile çalışma
Azure Cosmos DB sunar şema esnekliği ve zengin bir yerel dizin oluşturma [JSON](http://www.json.org) veri modeli. Veritabanları, koleksiyonlar, belgeler ve saklı yordamları da dahil olmak üzere tüm Azure Cosmos DB kaynakları modellenir ve JSON belgeleri olarak depolanır. Olma taşınabilir bir zorunluluk, JSON (ve Azure Cosmos DB) temel türleri, yalnızca küçük bir kümesini destekler: dize, sayı, Boole değeri, dizi, nesne ve Null. Ancak, JSON esnektir ve geliştiriciler ve çerçeveleri toorepresent nesne veya dizi oluşturma ve bu temelleri kullanarak daha karmaşık türleri izin verir. 

Toplama toohello temel türleri, birçok uygulama hello gereksinim [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) toorepresent tarihleri ve tarih damgası yazın. Bu makalede nasıl geliştiriciler depolamak, alabilir ve tarihleri hello .NET SDK kullanarak Azure Cosmos veritabanı sorgu açıklanmaktadır.

## <a name="storing-datetimes"></a>Tarih/saat depolanması
Varsayılan olarak, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) DateTime değerleri olarak serileştiren [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) dizeleri. Çoğu uygulama hello varsayılan dize gösterimi nedeni aşağıdaki Merhaba DateTime için kullanabilirsiniz:

* Dizeleri karşılaştırma ve dönüştürülen toostrings olduklarında hello hello DateTime değerleri sıralama göreli korunur. 
* Bu yaklaşım, JSON dönüştürme için herhangi bir özel kod veya öznitelikleri gerektirmez.
* JSON içinde depolanan gibi hello tarihleri İnsan okunabilir.
* Bu yaklaşım hızlı sorgu performansı için Azure Cosmos veritabanı dizin yararlanabilir.

Örneğin, kod parçacığında depoları hello bir `Order` içeren iki DateTime özellikleri - nesne `ShipDate` ve `OrderDate` bir belge olarak .NET SDK'sı hello kullanarak:

    public class Order
    {
        [JsonProperty(PropertyName="id")]
        public string Id { get; set; }
        public DateTime OrderDate { get; set; }
        public DateTime ShipDate { get; set; }
        public double Total { get; set; }
    }

    await client.CreateDocumentAsync("/dbs/orderdb/colls/orders", 
        new Order 
        { 
            Id = "09152014101",
            OrderDate = DateTime.UtcNow.AddDays(-30),
            ShipDate = DateTime.UtcNow.AddDays(-14), 
            Total = 113.39
        });

Bu belgede Azure Cosmos DB'de şekilde depolanır:

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

Alternatif olarak, tarih/saat olarak UNIX zaman damgaları, diğer bir deyişle, hello 1 Ocak 1970'ten beri geçen saniyelerin sayısını gösteren bir sayı olarak saklayabilirsiniz. Azure Cosmos DB'ın iç zaman damgası (`_ts`) özelliği, bu yaklaşım izler. Merhaba kullanabilirsiniz [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) tooserialize sayı olarak tarih/saat sınıfı. 

## <a name="indexing-datetimes-for-range-queries"></a>Tarih/saat aralığı sorgular için dizin oluşturma
Aralık sorguları içeren DateTime değerleri yaygındır. Örneğin, toofind dünden bu yana oluşturulan tüm siparişleri gerekir ya da son beş dakika hello gönderilen tüm siparişleri bulmak, tooperform aralığı sorguları gerekir. Bu sorgular verimli bir şekilde tooexecute, koleksiyonunuzu aralığı dizeleri dizin oluşturma için yapılandırmanız gerekir.

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

Hakkında daha fazla bilgi ilkeler dizin tooconfigure [Azure Cosmos DB dizin oluşturma ilkeleri](indexing-policies.md).

## <a name="querying-datetimes-in-linq"></a>Tarih/saat LINQ sorgulama
LINQ aracılığıyla Azure Cosmos veritabanında depolanan verileri Sorgulama Hello DocumentDB .NET SDK'yı otomatik olarak destekler. Örneğin, hello aşağıdaki kod parçacığında bir LINQ Sorgu hello son üç gün sevk edilen bu filtreler siparişleri gösterir.

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

Azure Cosmos veritabanı SQL sorgu dili ve hello LINQ sağlayıcısındaki hakkında daha fazla bilgiyi [sorgulama Cosmos DB](documentdb-sql-query.md).

Bu makalede, nasıl toostore, dizin ve tarih/saat Azure Cosmos veritabanı sorgu inceledik.

## <a name="next-steps"></a>Sonraki Adımlar
* İndirme ve çalıştırma hello [github'daki kod örnekleri](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)
* Daha fazla bilgi edinmek [DocumentDB API sorgusu](documentdb-sql-query.md)
* Daha fazla bilgi edinmek [Azure Cosmos DB dizin oluşturma ilkeleri](indexing-policies.md)
