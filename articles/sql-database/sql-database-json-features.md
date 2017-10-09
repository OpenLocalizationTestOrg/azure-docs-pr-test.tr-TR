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
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="e303f-103">Azure SQL veritabanında JSON özellikleri ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e303f-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="e303f-104">Ayrıştırma ve sorgu JavaScript nesne gösterimi gösterilen veriler azure SQL veritabanı sağlar [(JSON)](http://www.json.org/) biçimlendirmek ve ilişkisel verilerinizi JSON metni olarak verin.</span><span class="sxs-lookup"><span data-stu-id="e303f-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="e303f-105">JSON, modern web ve mobil uygulamalarda veri değişimi için kullanılan bir popüler veri biçimidir.</span><span class="sxs-lookup"><span data-stu-id="e303f-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="e303f-106">JSON, günlük dosyalarında veya NoSQL veritabanları gibi yarı yapılandırılmış verileri depolamak için de kullanılır [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="e303f-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="e303f-107">Dönüş sonuçları JSON metin olarak biçimlendirilmiş veya verileri kabul birçok REST web hizmeti JSON olarak biçimlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="e303f-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="e303f-108">Çoğu Azure Hizmetleri gibi [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), ve [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) dönün veya JSON tüketen REST uç noktalar vardır.</span><span class="sxs-lookup"><span data-stu-id="e303f-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="e303f-109">Azure SQL veritabanı, JSON verileriyle kolayca çalışmanızı ve veritabanınızı modern Hizmetleri ile tümleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="e303f-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="e303f-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e303f-110">Overview</span></span>
<span data-ttu-id="e303f-111">Azure SQL veritabanı işlevleri JSON verilerle çalışmak için aşağıdaki hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="e303f-111">Azure SQL Database provides hello following functions for working with JSON data:</span></span>

![JSON işlevleri](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="e303f-113">JSON metni varsa, verileri JSON öğesinden çıkarın veya hello yerleşik işlevlerini kullanarak JSON doğru şekilde yapılandırıldığını doğrulayın [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), ve [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e303f-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using hello built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="e303f-114">Merhaba [json_modıfy](https://msdn.microsoft.com/library/dn921892.aspx) işlevi JSON metni içindeki değeri güncelleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e303f-114">hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="e303f-115">Daha gelişmiş sorgulama ve analiz, için [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) işlevi bir dizi satır JSON nesnelerinin bir dizisi dönüştürme.</span><span class="sxs-lookup"><span data-stu-id="e303f-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="e303f-116">Herhangi bir SQL sorgu sonuç kümesi döndürdü hello üzerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e303f-116">Any SQL query can be executed on hello returned result set.</span></span> <span data-ttu-id="e303f-117">Son olarak, var olan bir [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) olanak sağlayan yan tümcesi biçimlendirmek ilişkisel tabloları JSON metni olarak depolanan veriler.</span><span class="sxs-lookup"><span data-stu-id="e303f-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="e303f-118">JSON biçiminde ilişkisel veri biçimlendirme</span><span class="sxs-lookup"><span data-stu-id="e303f-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="e303f-119">JSON içinde bir yanıt sağlar ve katman hello veritabanından veri alır biçimlendirin veya istemci tarafı JavaScript çerçeveler veya verileri kabul kitaplıkları JSON olarak biçimlendirilmiş bir web hizmeti varsa, doğrudan SQL sorgusunda JSON olarak veritabanı içeriğinizi biçimlendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e303f-119">If you have a web service that takes data from hello database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="e303f-120">Artık sonuçları Azure SQL veritabanından JSON, olarak biçimlendirir toowrite uygulama koduna sahip veya bazı JSON seri hale getirme kitaplığı tooconvert Tablo sorgusu sonuçları dahil edin ve nesneleri tooJSON biçimi serileştirme.</span><span class="sxs-lookup"><span data-stu-id="e303f-120">You no longer have toowrite application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library tooconvert tabular query results and then serialize objects tooJSON format.</span></span> <span data-ttu-id="e303f-121">Bunun yerine, Azure SQL veritabanında JSON olarak JSON yan tümcesi tooformat SQL sorgu sonuçları için hello kullanmak ve doğrudan uygulamanızda kullanın.</span><span class="sxs-lookup"><span data-stu-id="e303f-121">Instead, you can use hello FOR JSON clause tooformat SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="e303f-122">Aşağıdaki örneğine hello hello Sales.Customer tablodaki hello FOR JSON yan tümcesi kullanılarak JSON olarak biçimlendirilir:</span><span class="sxs-lookup"><span data-stu-id="e303f-122">In hello following example, rows from hello Sales.Customer table are formatted as JSON by using hello FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="e303f-123">Merhaba FOR JSON PATH'i yan tümcesi hello hello sorgunun sonuçlarını JSON metin olarak biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="e303f-123">hello FOR JSON PATH clause formats hello results of hello query as JSON text.</span></span> <span data-ttu-id="e303f-124">Merhaba hücre değerlerini JSON değerleri olarak oluşsa sütun adları anahtarlar kullanılır:</span><span class="sxs-lookup"><span data-stu-id="e303f-124">Column names are used as keys, while hello cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="e303f-125">Merhaba sonuç kümesi, burada her satır ayrı bir JSON nesnesi olarak biçimlendirilmiş bir JSON dizisi olarak biçimlendirilir.</span><span class="sxs-lookup"><span data-stu-id="e303f-125">hello result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="e303f-126">Sütun diğer adları noktalı gösterim kullanılarak JSON Sonuç kümenizi hello çıkış biçimini özelleştirebilirsiniz YOLUNU gösterir.</span><span class="sxs-lookup"><span data-stu-id="e303f-126">PATH indicates that you can customize hello output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="e303f-127">Sorgu aşağıdaki hello hello "CustomerName" anahtarı hello çıkış JSON biçiminde hello adını değiştirir ve telefon ve Faks numaraları hello "Başvurun" alt nesnesinde yerleştirir:</span><span class="sxs-lookup"><span data-stu-id="e303f-127">hello following query changes hello name of hello "CustomerName" key in hello output JSON format, and puts phone and fax numbers in hello "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="e303f-128">Bu sorgunun Hello çıktı şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="e303f-128">hello output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="e303f-129">Bu örnekte, biz dizi yerine tek bir JSON nesnesi hello belirterek döndürülen [wıthout_array_wrapper](https://msdn.microsoft.com/library/mt631354.aspx) seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e303f-129">In this example we returned a single JSON object instead of an array by specifying hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="e303f-130">Sorgu sonucu olarak tek bir nesne döndürme biliyorsanız, bu seçeneği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e303f-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="e303f-131">Merhaba ana hello FOR JSON yan tümcesi, iç içe geçmiş JSON nesnelerinin veya dizi olarak biçimlendirilmiş veritabanınızı karmaşık hiyerarşik veri döndürmek sağlar değeridir.</span><span class="sxs-lookup"><span data-stu-id="e303f-131">hello main value of hello FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="e303f-132">iç içe geçmiş bir sipariş dizisi olarak toohello müşteri ait nasıl tooinclude siparişleri örnekte gösterildiği aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="e303f-132">hello following example shows how tooinclude Orders that belong toohello Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="e303f-133">Ayrı sorgulara tooget müşteri verileri ve toofetch ilgili siparişleri bir liste göndermek yerine, tüm hello gerekli verileri tek bir sorgu ile hello örnek çıktı aşağıdaki gösterildiği gibi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e303f-133">Instead of sending separate queries tooget Customer data and then toofetch a list of related Orders, you can get all hello necessary data with a single query, as shown in hello following sample output:</span></span>

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

## <a name="working-with-json-data"></a><span data-ttu-id="e303f-134">JSON verileriyle çalışma</span><span class="sxs-lookup"><span data-stu-id="e303f-134">Working with JSON data</span></span>
<span data-ttu-id="e303f-135">Karmaşık alt nesneler, dizileri veya hiyerarşik veri varsa, kesinlikle yapılandırılmış veri yoksa veya zaman içinde veri yapılarını gelişmesi, hello JSON biçiminde herhangi bir karmaşık veri yapısını, toorepresent yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e303f-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, hello JSON format can help you toorepresent any complex data structure.</span></span>

<span data-ttu-id="e303f-136">JSON herhangi bir dize türü Azure SQL veritabanında gibi kullanılabilecek bir metinsel biçimidir.</span><span class="sxs-lookup"><span data-stu-id="e303f-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="e303f-137">Standart NVARCHAR JSON verilerini depolamak ya da gönder:</span><span class="sxs-lookup"><span data-stu-id="e303f-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

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

<span data-ttu-id="e303f-138">Bu örnekte kullanılan JSON verilerini Hello hello NVARCHAR(MAX) türü kullanılarak temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="e303f-138">hello JSON data used in this example is represented by using hello NVARCHAR(MAX) type.</span></span> <span data-ttu-id="e303f-139">JSON bu tabloya eklenen veya hello aşağıdaki örnekte gösterildiği gibi standart Transact-SQL söz dizimini kullanarak hello saklı yordamının bağımsız değişken olarak sağlanan:</span><span class="sxs-lookup"><span data-stu-id="e303f-139">JSON can be inserted into this table or provided as an argument of hello stored procedure using standard Transact-SQL syntax as shown in hello following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="e303f-140">Ayrıca herhangi bir istemci tarafı dili veya Azure SQL veritabanında dize verilerle çalışır kitaplığı JSON verilerle çalışır.</span><span class="sxs-lookup"><span data-stu-id="e303f-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="e303f-141">JSON, bellek için iyileştirilmiş bir tablo veya bir sistem sürümü tutulan tablo gibi hello NVARCHAR türü destekleyen herhangi bir tabloda depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="e303f-141">JSON can be stored in any table that supports hello NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="e303f-142">JSON herhangi bir kısıtlama hello istemci tarafı kodlar veya hello veritabanı katmanı sunmaz.</span><span class="sxs-lookup"><span data-stu-id="e303f-142">JSON does not introduce any constraint either in hello client-side code or in hello database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="e303f-143">JSON veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="e303f-143">Querying JSON data</span></span>
<span data-ttu-id="e303f-144">Azure SQL tablolarda depolanan JSON olarak biçimlendirilmiş verileri varsa, JSON işlevler içinde herhangi bir SQL sorgu bu verileri kullanmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e303f-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="e303f-145">Azure SQL veritabanı let kullanılabilir JSON işlevleri başka bir SQL veri türü olarak JSON olarak biçimlendirilmiş verileri kabul eder.</span><span class="sxs-lookup"><span data-stu-id="e303f-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="e303f-146">Kolayca değerleri JSON metni hello ayıklamak ve herhangi bir sorgu JSON verilerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="e303f-146">You can easily extract values from hello JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="e303f-147">Merhaba JSON_VALUE işlevi bir değer hello veri sütununda depolanan JSON metinden ayıklar.</span><span class="sxs-lookup"><span data-stu-id="e303f-147">hello JSON_VALUE function extracts a value from JSON text stored in hello Data column.</span></span> <span data-ttu-id="e303f-148">Bu işlev bir JavaScript benzeri yolu tooreference bir değeri JSON metni tooextract kullanır.</span><span class="sxs-lookup"><span data-stu-id="e303f-148">This function uses a JavaScript-like path tooreference a value in JSON text tooextract.</span></span> <span data-ttu-id="e303f-149">Ayıklanan hello değeri herhangi bir kısmını SQL sorgusu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e303f-149">hello extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="e303f-150">Merhaba JSON_QUERY işlevi benzer tooJSON_VALUE ' dir.</span><span class="sxs-lookup"><span data-stu-id="e303f-150">hello JSON_QUERY function is similar tooJSON_VALUE.</span></span> <span data-ttu-id="e303f-151">JSON_VALUE farklı olarak, bu işlev dizileri veya JSON metninde yerleştirilir nesneleri gibi karmaşık alt nesne ayıklar.</span><span class="sxs-lookup"><span data-stu-id="e303f-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="e303f-152">Merhaba json_modıfy işlevi hello değerinin hello yolunu güncelleştirilmelidir hello JSON metnini, aynı zamanda hello eskisinin üzerine yeni bir değer belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e303f-152">hello JSON_MODIFY function lets you specify hello path of hello value in hello JSON text that should be updated, as well as a new value that will overwrite hello old one.</span></span> <span data-ttu-id="e303f-153">Bu şekilde hello tüm yapısını yeniden ayrıştırmayı olmadan kolayca JSON metnini güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e303f-153">This way you can easily update JSON text without reparsing hello entire structure.</span></span>

<span data-ttu-id="e303f-154">JSON standart metin olarak kaydedildiği metin sütunlarında depolanan hello değerleri düzgün biçimlendirilmiş garanti vardır.</span><span class="sxs-lookup"><span data-stu-id="e303f-154">Since JSON is stored in a standard text, there are no guarantees that hello values stored in text columns are properly formatted.</span></span> <span data-ttu-id="e303f-155">Standart Azure SQL veritabanı denetimi kısıtlamaları ve hello ISJSON işlevi kullanarak, JSON sütunda depolanan metin düzgün biçimlendirildiğinden doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e303f-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and hello ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="e303f-156">Merhaba giriş metni düzgün biçimlendirildiğinden, JSON, hello ISJSON işlevi hello değeri 1 döndürür.</span><span class="sxs-lookup"><span data-stu-id="e303f-156">If hello input text is properly formatted JSON, hello ISJSON function returns hello value 1.</span></span> <span data-ttu-id="e303f-157">Her INSERT veya update JSON sütunun üzerinde bu kısıtlamayı yeni metin değeri hatalı biçimlendirilmiş JSON olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="e303f-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="e303f-158">JSON tablo biçimine dönüştürme</span><span class="sxs-lookup"><span data-stu-id="e303f-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="e303f-159">Azure SQL veritabanı, tablo biçiminde ve yükleme veya sorgu JSON veri JSON koleksiyonlara dönüştürme sağlar.</span><span class="sxs-lookup"><span data-stu-id="e303f-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="e303f-160">OPENJSON JSON metni ayrıştırır, JSON nesnelerinin bir dizisi bulur, hello dizi hello öğelerini aracılığıyla tekrarlanan ve hello elde edilen sonucu hello dizinin her bir öğe için bir satır döndürür tablo değerli bir işlevdir.</span><span class="sxs-lookup"><span data-stu-id="e303f-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through hello elements of hello array, and returns one row in hello output result for each element of hello array.</span></span>

![JSON tablo](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="e303f-162">Merhaba yukarıdaki örnekte, biz nerede toolocate hello açılması gerekir (Merhaba $expand. JSON dizisi belirtebilirsiniz Siparişleri yolu), hangi sütunların sonucu olarak döndürülmelidir ve toofind hello burada döndürülecek JSON değerleri olarak hücreleri.</span><span class="sxs-lookup"><span data-stu-id="e303f-162">In hello example above, we can specify where toolocate hello JSON array that should be opened (in hello $.Orders path), what columns should be returned as result, and where toofind hello JSON values that will be returned as cells.</span></span>

<span data-ttu-id="e303f-163">Biz hello JSON dizisinde dönüştürebilirsiniz @orders değişkenine bir dizi satır, bu sonuç kümesi çözümlemek veya standart bir tabloya satır ekleme:</span><span class="sxs-lookup"><span data-stu-id="e303f-163">We can transform a JSON array in hello @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

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
<span data-ttu-id="e303f-164">bir JSON dizisi olarak biçimlendirilmiş ve bir parametre toohello depolanan yordamı ayrıştırılır ve hello siparişleri tabloya eklenen olarak sağlanan siparişleri Hello topluluğu.</span><span class="sxs-lookup"><span data-stu-id="e303f-164">hello collection of orders formatted as a JSON array and provided as a parameter toohello stored procedure can be parsed and inserted into hello Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e303f-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e303f-165">Next steps</span></span>
<span data-ttu-id="e303f-166">toolearn toointegrate uygulamanıza bağlı olarak, JSON denetleyin nasıl bu kaynakları:</span><span class="sxs-lookup"><span data-stu-id="e303f-166">toolearn how toointegrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="e303f-167">TechNet blogu</span><span class="sxs-lookup"><span data-stu-id="e303f-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="e303f-168">MSDN belgelerine</span><span class="sxs-lookup"><span data-stu-id="e303f-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="e303f-169">Kanal 9 video</span><span class="sxs-lookup"><span data-stu-id="e303f-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="e303f-170">JSON, uygulamanıza tümleştirmek için çeşitli senaryoları hakkında toolearn bkz hello gösterileri bu [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) veya kullanım örneğinde eşleşen bir senaryo Bul [JSON Blog yazılarını](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span><span class="sxs-lookup"><span data-stu-id="e303f-170">toolearn about various scenarios for integrating JSON into your application, see hello demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

