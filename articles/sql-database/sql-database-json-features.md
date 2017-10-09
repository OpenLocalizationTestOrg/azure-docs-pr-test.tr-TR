---
title: "aaaAzure SQL veritabanı JSON özellikleri | Microsoft Docs"
description: "Azure SQL veritabanı tooparse, sorgu ve JavaScript nesne gösterimi (JSON) gösteriminde biçim verileri sağlar."
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 55860105-2f5f-4b10-87a0-99faa32b5653
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.date: 11/15/2016
ms.author: jovanpop
ms.workload: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 30a31a1b01482ec276646b6fd6ca0c1f581168d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a>Azure SQL veritabanında JSON özellikleri ile çalışmaya başlama
Ayrıştırma ve sorgu JavaScript nesne gösterimi gösterilen veriler azure SQL veritabanı sağlar [(JSON)](http://www.json.org/) biçimlendirmek ve ilişkisel verilerinizi JSON metni olarak verin.

JSON, modern web ve mobil uygulamalarda veri değişimi için kullanılan bir popüler veri biçimidir. JSON, günlük dosyalarında veya NoSQL veritabanları gibi yarı yapılandırılmış verileri depolamak için de kullanılır [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/). Dönüş sonuçları JSON metin olarak biçimlendirilmiş veya verileri kabul birçok REST web hizmeti JSON olarak biçimlendirilmiş. Çoğu Azure Hizmetleri gibi [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), ve [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) dönün veya JSON tüketen REST uç noktalar vardır.

Azure SQL veritabanı, JSON verileriyle kolayca çalışmanızı ve veritabanınızı modern Hizmetleri ile tümleştirme sağlar.

## <a name="overview"></a>Genel Bakış
Azure SQL veritabanı işlevleri JSON verilerle çalışmak için aşağıdaki hello sağlar:

![JSON işlevleri](./media/sql-database-json-features/image_1.png)

JSON metni varsa, verileri JSON öğesinden çıkarın veya hello yerleşik işlevlerini kullanarak JSON doğru şekilde yapılandırıldığını doğrulayın [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), ve [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) . Merhaba [json_modıfy](https://msdn.microsoft.com/library/dn921892.aspx) işlevi JSON metni içindeki değeri güncelleştirmenize olanak sağlar. Daha gelişmiş sorgulama ve analiz, için [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) işlevi bir dizi satır JSON nesnelerinin bir dizisi dönüştürme. Herhangi bir SQL sorgu sonuç kümesi döndürdü hello üzerinde çalıştırılabilir. Son olarak, var olan bir [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) olanak sağlayan yan tümcesi biçimlendirmek ilişkisel tabloları JSON metni olarak depolanan veriler.

## <a name="formatting-relational-data-in-json-format"></a>JSON biçiminde ilişkisel veri biçimlendirme
JSON içinde bir yanıt sağlar ve katman hello veritabanından veri alır biçimlendirin veya istemci tarafı JavaScript çerçeveler veya verileri kabul kitaplıkları JSON olarak biçimlendirilmiş bir web hizmeti varsa, doğrudan SQL sorgusunda JSON olarak veritabanı içeriğinizi biçimlendirebilirsiniz. Artık sonuçları Azure SQL veritabanından JSON, olarak biçimlendirir toowrite uygulama koduna sahip veya bazı JSON seri hale getirme kitaplığı tooconvert Tablo sorgusu sonuçları dahil edin ve nesneleri tooJSON biçimi serileştirme. Bunun yerine, Azure SQL veritabanında JSON olarak JSON yan tümcesi tooformat SQL sorgu sonuçları için hello kullanmak ve doğrudan uygulamanızda kullanın.

Aşağıdaki örneğine hello hello Sales.Customer tablodaki hello FOR JSON yan tümcesi kullanılarak JSON olarak biçimlendirilir:

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

Merhaba FOR JSON PATH'i yan tümcesi hello hello sorgunun sonuçlarını JSON metin olarak biçimlendirir. Merhaba hücre değerlerini JSON değerleri olarak oluşsa sütun adları anahtarlar kullanılır:

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

Merhaba sonuç kümesi, burada her satır ayrı bir JSON nesnesi olarak biçimlendirilmiş bir JSON dizisi olarak biçimlendirilir.

Sütun diğer adları noktalı gösterim kullanılarak JSON Sonuç kümenizi hello çıkış biçimini özelleştirebilirsiniz YOLUNU gösterir. Sorgu aşağıdaki hello hello "CustomerName" anahtarı hello çıkış JSON biçiminde hello adını değiştirir ve telefon ve Faks numaraları hello "Başvurun" alt nesnesinde yerleştirir:

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

Bu sorgunun Hello çıktı şu şekildedir:

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

Bu örnekte, biz dizi yerine tek bir JSON nesnesi hello belirterek döndürülen [wıthout_array_wrapper](https://msdn.microsoft.com/library/mt631354.aspx) seçeneği. Sorgu sonucu olarak tek bir nesne döndürme biliyorsanız, bu seçeneği kullanabilirsiniz.

Merhaba ana hello FOR JSON yan tümcesi, iç içe geçmiş JSON nesnelerinin veya dizi olarak biçimlendirilmiş veritabanınızı karmaşık hiyerarşik veri döndürmek sağlar değeridir. iç içe geçmiş bir sipariş dizisi olarak toohello müşteri ait nasıl tooinclude siparişleri örnekte gösterildiği aşağıdaki hello:

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

Ayrı sorgulara tooget müşteri verileri ve toofetch ilgili siparişleri bir liste göndermek yerine, tüm hello gerekli verileri tek bir sorgu ile hello örnek çıktı aşağıdaki gösterildiği gibi alabilirsiniz:

```
{
  "Name":"Nada Jovanovic",
  "Phone":"(215) 555-0100",
  "Fax":"(215) 555-0101",
  "Orders":[
    {"OrderID":382,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":395,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":1657,"OrderDate":"2013-01-31","ExpectedDeliveryDate":"2013-02-01"}
]
}
```

## <a name="working-with-json-data"></a>JSON verileriyle çalışma
Karmaşık alt nesneler, dizileri veya hiyerarşik veri varsa, kesinlikle yapılandırılmış veri yoksa veya zaman içinde veri yapılarını gelişmesi, hello JSON biçiminde herhangi bir karmaşık veri yapısını, toorepresent yardımcı olabilir.

JSON herhangi bir dize türü Azure SQL veritabanında gibi kullanılabilecek bir metinsel biçimidir. Standart NVARCHAR JSON verilerini depolamak ya da gönder:

```
CREATE TABLE Products (
  Id int identity primary key,
  Title nvarchar(200),
  Data nvarchar(max)
)
go
CREATE PROCEDURE InsertProduct(@title nvarchar(200), @json nvarchar(max))
AS BEGIN
    insert into Products(Title, Data)
    values(@title, @json)
END
```

Bu örnekte kullanılan JSON verilerini Hello hello NVARCHAR(MAX) türü kullanılarak temsil edilir. JSON bu tabloya eklenen veya hello aşağıdaki örnekte gösterildiği gibi standart Transact-SQL söz dizimini kullanarak hello saklı yordamının bağımsız değişken olarak sağlanan:

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

Ayrıca herhangi bir istemci tarafı dili veya Azure SQL veritabanında dize verilerle çalışır kitaplığı JSON verilerle çalışır. JSON, bellek için iyileştirilmiş bir tablo veya bir sistem sürümü tutulan tablo gibi hello NVARCHAR türü destekleyen herhangi bir tabloda depolanabilir. JSON herhangi bir kısıtlama hello istemci tarafı kodlar veya hello veritabanı katmanı sunmaz.

## <a name="querying-json-data"></a>JSON veri sorgulama
Azure SQL tablolarda depolanan JSON olarak biçimlendirilmiş verileri varsa, JSON işlevler içinde herhangi bir SQL sorgu bu verileri kullanmanıza olanak tanır.

Azure SQL veritabanı let kullanılabilir JSON işlevleri başka bir SQL veri türü olarak JSON olarak biçimlendirilmiş verileri kabul eder. Kolayca değerleri JSON metni hello ayıklamak ve herhangi bir sorgu JSON verilerini kullanın:

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

Merhaba JSON_VALUE işlevi bir değer hello veri sütununda depolanan JSON metinden ayıklar. Bu işlev bir JavaScript benzeri yolu tooreference bir değeri JSON metni tooextract kullanır. Ayıklanan hello değeri herhangi bir kısmını SQL sorgusu kullanılabilir.

Merhaba JSON_QUERY işlevi benzer tooJSON_VALUE ' dir. JSON_VALUE farklı olarak, bu işlev dizileri veya JSON metninde yerleştirilir nesneleri gibi karmaşık alt nesne ayıklar.

Merhaba json_modıfy işlevi hello değerinin hello yolunu güncelleştirilmelidir hello JSON metnini, aynı zamanda hello eskisinin üzerine yeni bir değer belirtmenize olanak sağlar. Bu şekilde hello tüm yapısını yeniden ayrıştırmayı olmadan kolayca JSON metnini güncelleştirebilirsiniz.

JSON standart metin olarak kaydedildiği metin sütunlarında depolanan hello değerleri düzgün biçimlendirilmiş garanti vardır. Standart Azure SQL veritabanı denetimi kısıtlamaları ve hello ISJSON işlevi kullanarak, JSON sütunda depolanan metin düzgün biçimlendirildiğinden doğrulayabilirsiniz:

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

Merhaba giriş metni düzgün biçimlendirildiğinden, JSON, hello ISJSON işlevi hello değeri 1 döndürür. Her INSERT veya update JSON sütunun üzerinde bu kısıtlamayı yeni metin değeri hatalı biçimlendirilmiş JSON olmadığından emin olun.

## <a name="transforming-json-into-tabular-format"></a>JSON tablo biçimine dönüştürme
Azure SQL veritabanı, tablo biçiminde ve yükleme veya sorgu JSON veri JSON koleksiyonlara dönüştürme sağlar.

OPENJSON JSON metni ayrıştırır, JSON nesnelerinin bir dizisi bulur, hello dizi hello öğelerini aracılığıyla tekrarlanan ve hello elde edilen sonucu hello dizinin her bir öğe için bir satır döndürür tablo değerli bir işlevdir.

![JSON tablo](./media/sql-database-json-features/image_2.png)

Merhaba yukarıdaki örnekte, biz nerede toolocate hello açılması gerekir (Merhaba $expand. JSON dizisi belirtebilirsiniz Siparişleri yolu), hangi sütunların sonucu olarak döndürülmelidir ve toofind hello burada döndürülecek JSON değerleri olarak hücreleri.

Biz hello JSON dizisinde dönüştürebilirsiniz @orders değişkenine bir dizi satır, bu sonuç kümesi çözümlemek veya standart bir tabloya satır ekleme:

```
CREATE PROCEDURE InsertOrders(@orders nvarchar(max))
AS BEGIN

    insert into Orders(Number, Date, Customer, Quantity)
    select Number, Date, Customer, Quantity
    OPENJSON (@orders)
     WITH (
            Number varchar(200),
            Date datetime,
            Customer varchar(200),
            Quantity int
     )

END
```
bir JSON dizisi olarak biçimlendirilmiş ve bir parametre toohello depolanan yordamı ayrıştırılır ve hello siparişleri tabloya eklenen olarak sağlanan siparişleri Hello topluluğu.

## <a name="next-steps"></a>Sonraki adımlar
toolearn toointegrate uygulamanıza bağlı olarak, JSON denetleyin nasıl bu kaynakları:

* [TechNet blogu](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [MSDN belgelerine](https://msdn.microsoft.com/library/dn921897.aspx)
* [Kanal 9 video](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

JSON, uygulamanıza tümleştirmek için çeşitli senaryoları hakkında toolearn bkz hello gösterileri bu [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) veya kullanım örneğinde eşleşen bir senaryo Bul [JSON Blog yazılarını](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).

