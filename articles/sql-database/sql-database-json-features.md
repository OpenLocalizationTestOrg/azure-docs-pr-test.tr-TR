---
title: "Azure SQL veritabanı JSON özellikleri | Microsoft Docs"
description: "Azure SQL veritabanı ayrıştırma, sorgu ve JavaScript nesne gösterimi (JSON) gösteriminde biçim verileri sağlar."
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
ms.openlocfilehash: 883e661107dd838f5c381cdef2c7f891b9a9389c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="6970b-103">Azure SQL veritabanında JSON özellikleri ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6970b-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="6970b-104">Ayrıştırma ve sorgu JavaScript nesne gösterimi gösterilen veriler azure SQL veritabanı sağlar [(JSON)](http://www.json.org/) biçimlendirmek ve ilişkisel verilerinizi JSON metni olarak verin.</span><span class="sxs-lookup"><span data-stu-id="6970b-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="6970b-105">JSON, modern web ve mobil uygulamalarda veri değişimi için kullanılan bir popüler veri biçimidir.</span><span class="sxs-lookup"><span data-stu-id="6970b-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="6970b-106">JSON, günlük dosyalarında veya NoSQL veritabanları gibi yarı yapılandırılmış verileri depolamak için de kullanılır [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="6970b-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="6970b-107">Dönüş sonuçları JSON metin olarak biçimlendirilmiş veya verileri kabul birçok REST web hizmeti JSON olarak biçimlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="6970b-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="6970b-108">Çoğu Azure Hizmetleri gibi [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), ve [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) dönün veya JSON tüketen REST uç noktalar vardır.</span><span class="sxs-lookup"><span data-stu-id="6970b-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="6970b-109">Azure SQL veritabanı, JSON verileriyle kolayca çalışmanızı ve veritabanınızı modern Hizmetleri ile tümleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="6970b-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="6970b-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6970b-110">Overview</span></span>
<span data-ttu-id="6970b-111">Azure SQL veritabanı, JSON verilerle çalışmak için aşağıdaki işlevleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="6970b-111">Azure SQL Database provides the following functions for working with JSON data:</span></span>

![JSON işlevleri](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="6970b-113">JSON metni varsa, verileri JSON öğesinden çıkarın veya yerleşik işlevlerini kullanarak JSON doğru şekilde yapılandırıldığını doğrulayın [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), ve [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span><span class="sxs-lookup"><span data-stu-id="6970b-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using the built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="6970b-114">[Json_modıfy](https://msdn.microsoft.com/library/dn921892.aspx) işlevi JSON metni içindeki değeri güncelleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6970b-114">The [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="6970b-115">Daha gelişmiş sorgulama ve analiz, için [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) işlevi bir dizi satır JSON nesnelerinin bir dizisi dönüştürme.</span><span class="sxs-lookup"><span data-stu-id="6970b-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="6970b-116">Herhangi bir SQL sorgu döndürülen sonuç kümesi üzerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="6970b-116">Any SQL query can be executed on the returned result set.</span></span> <span data-ttu-id="6970b-117">Son olarak, var olan bir [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) olanak sağlayan yan tümcesi biçimlendirmek ilişkisel tabloları JSON metni olarak depolanan veriler.</span><span class="sxs-lookup"><span data-stu-id="6970b-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="6970b-118">JSON biçiminde ilişkisel veri biçimlendirme</span><span class="sxs-lookup"><span data-stu-id="6970b-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="6970b-119">JSON içinde bir yanıt sağlar ve katman veritabanından veri alır biçimlendirin veya istemci tarafı JavaScript çerçeveler veya verileri kabul kitaplıkları JSON olarak biçimlendirilmiş bir web hizmeti varsa, doğrudan SQL sorgusunda JSON olarak veritabanı içeriğinizi biçimlendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6970b-119">If you have a web service that takes data from the database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="6970b-120">Artık sonuçları JSON olarak Azure SQL veritabanından biçimler uygulama kod yazmak zorunda veya Tablo sorgusu sonuçları dönüştürmek ve JSON biçimine nesneleri seri hale getirmek için bazı JSON seri hale getirme kitaplığı içerir.</span><span class="sxs-lookup"><span data-stu-id="6970b-120">You no longer have to write application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library to convert tabular query results and then serialize objects to JSON format.</span></span> <span data-ttu-id="6970b-121">Bunun yerine, FOR JSON yan tümcesi SQL sorgu sonuçları Azure SQL veritabanında JSON olarak biçimlendirmek ve doğrudan, uygulamanızda kullanmak üzere kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6970b-121">Instead, you can use the FOR JSON clause to format SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="6970b-122">Aşağıdaki örnekte, Sales.Customer tablodaki FOR JSON yan tümcesi kullanılarak JSON olarak biçimlendirilir:</span><span class="sxs-lookup"><span data-stu-id="6970b-122">In the following example, rows from the Sales.Customer table are formatted as JSON by using the FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="6970b-123">FOR JSON PATH'i yan tümcesi sorgunun sonuçları JSON metin olarak biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="6970b-123">The FOR JSON PATH clause formats the results of the query as JSON text.</span></span> <span data-ttu-id="6970b-124">Hücre değerlerini JSON değerleri olarak oluşsa sütun adları anahtarlar kullanılır:</span><span class="sxs-lookup"><span data-stu-id="6970b-124">Column names are used as keys, while the cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="6970b-125">Sonuç kümesi, burada her satır ayrı bir JSON nesnesi olarak biçimlendirilmiş bir JSON dizisi olarak biçimlendirilir.</span><span class="sxs-lookup"><span data-stu-id="6970b-125">The result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="6970b-126">Sütun diğer adları noktalı gösterim kullanılarak JSON Sonuç kümenizi çıkış biçimini özelleştirebilirsiniz YOLUNU gösterir.</span><span class="sxs-lookup"><span data-stu-id="6970b-126">PATH indicates that you can customize the output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="6970b-127">Aşağıdaki sorgu çıkış JSON biçiminde "CustomerName" anahtar adını değiştirir ve telefon ve Faks numaraları "Başvurun" alt nesnesinde yerleştirir:</span><span class="sxs-lookup"><span data-stu-id="6970b-127">The following query changes the name of the "CustomerName" key in the output JSON format, and puts phone and fax numbers in the "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="6970b-128">Bu sorgu çıktısı şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="6970b-128">The output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="6970b-129">Bu örnekte, biz dizi yerine tek bir JSON nesnesi belirterek döndürülen [wıthout_array_wrapper](https://msdn.microsoft.com/library/mt631354.aspx) seçeneği.</span><span class="sxs-lookup"><span data-stu-id="6970b-129">In this example we returned a single JSON object instead of an array by specifying the [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="6970b-130">Sorgu sonucu olarak tek bir nesne döndürme biliyorsanız, bu seçeneği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6970b-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="6970b-131">Ana FOR JSON yan tümcesi, iç içe geçmiş JSON nesnelerinin veya dizi olarak biçimlendirilmiş veritabanınızı karmaşık hiyerarşik veri döndürmek sağlar değeri.</span><span class="sxs-lookup"><span data-stu-id="6970b-131">The main value of the FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="6970b-132">Aşağıdaki örnek, iç içe geçmiş bir sipariş dizisi olarak müşteriye ait siparişleri dahil et gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="6970b-132">The following example shows how to include Orders that belong to the Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="6970b-133">Müşteri verilerini almak için sorguları ayırın ve ardından ilgili siparişleri listesini getirmek için gerekli tüm verileri tek bir sorgu ile alabilirsiniz aşağıdaki örnek çıktıda görüldüğü gibi göndermek yerine:</span><span class="sxs-lookup"><span data-stu-id="6970b-133">Instead of sending separate queries to get Customer data and then to fetch a list of related Orders, you can get all the necessary data with a single query, as shown in the following sample output:</span></span>

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

## <a name="working-with-json-data"></a><span data-ttu-id="6970b-134">JSON verileriyle çalışma</span><span class="sxs-lookup"><span data-stu-id="6970b-134">Working with JSON data</span></span>
<span data-ttu-id="6970b-135">Karmaşık alt nesneler, dizileri veya hiyerarşik veri varsa, kesinlikle yapılandırılmış veri yoksa veya zaman içinde veri yapılarını gelişmesi, JSON biçimi, herhangi bir karmaşık veri yapısını temsil etmek için yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6970b-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, the JSON format can help you to represent any complex data structure.</span></span>

<span data-ttu-id="6970b-136">JSON herhangi bir dize türü Azure SQL veritabanında gibi kullanılabilecek bir metinsel biçimidir.</span><span class="sxs-lookup"><span data-stu-id="6970b-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="6970b-137">Standart NVARCHAR JSON verilerini depolamak ya da gönder:</span><span class="sxs-lookup"><span data-stu-id="6970b-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

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

<span data-ttu-id="6970b-138">Bu örnekte kullanılan JSON verilerini NVARCHAR(MAX) türü kullanılarak temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="6970b-138">The JSON data used in this example is represented by using the NVARCHAR(MAX) type.</span></span> <span data-ttu-id="6970b-139">JSON bu tabloya eklenen veya aşağıdaki örnekte gösterildiği gibi standart Transact-SQL söz dizimini kullanarak saklı yordam bağımsız değişken olarak sağlanan:</span><span class="sxs-lookup"><span data-stu-id="6970b-139">JSON can be inserted into this table or provided as an argument of the stored procedure using standard Transact-SQL syntax as shown in the following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="6970b-140">Ayrıca herhangi bir istemci tarafı dili veya Azure SQL veritabanında dize verilerle çalışır kitaplığı JSON verilerle çalışır.</span><span class="sxs-lookup"><span data-stu-id="6970b-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="6970b-141">JSON, bellek için iyileştirilmiş bir tablo veya bir sistem sürümü tutulan tablo gibi NVARCHAR türü destekleyen herhangi bir tabloda depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="6970b-141">JSON can be stored in any table that supports the NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="6970b-142">JSON herhangi bir kısıtlama istemci-tarafı koduna veya veritabanı katmanı sunmaz.</span><span class="sxs-lookup"><span data-stu-id="6970b-142">JSON does not introduce any constraint either in the client-side code or in the database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="6970b-143">JSON veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="6970b-143">Querying JSON data</span></span>
<span data-ttu-id="6970b-144">Azure SQL tablolarda depolanan JSON olarak biçimlendirilmiş verileri varsa, JSON işlevler içinde herhangi bir SQL sorgu bu verileri kullanmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="6970b-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="6970b-145">Azure SQL veritabanı let kullanılabilir JSON işlevleri başka bir SQL veri türü olarak JSON olarak biçimlendirilmiş verileri kabul eder.</span><span class="sxs-lookup"><span data-stu-id="6970b-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="6970b-146">Kolayca değerleri JSON Metinden ayıklamak ve herhangi bir sorgu JSON verilerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="6970b-146">You can easily extract values from the JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="6970b-147">JSON_VALUE işlevi bir değer veri sütununda depolanan JSON metinden ayıklar.</span><span class="sxs-lookup"><span data-stu-id="6970b-147">The JSON_VALUE function extracts a value from JSON text stored in the Data column.</span></span> <span data-ttu-id="6970b-148">Bu işlev bir JavaScript benzeri yolu ayıklamak için JSON metin değerinde başvurmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="6970b-148">This function uses a JavaScript-like path to reference a value in JSON text to extract.</span></span> <span data-ttu-id="6970b-149">Ayıklanan değerin herhangi bir kısmını SQL sorgusu kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6970b-149">The extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="6970b-150">JSON_QUERY işlevi için JSON_VALUE benzer.</span><span class="sxs-lookup"><span data-stu-id="6970b-150">The JSON_QUERY function is similar to JSON_VALUE.</span></span> <span data-ttu-id="6970b-151">JSON_VALUE farklı olarak, bu işlev dizileri veya JSON metninde yerleştirilir nesneleri gibi karmaşık alt nesne ayıklar.</span><span class="sxs-lookup"><span data-stu-id="6970b-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="6970b-152">Json_modıfy işlevi değerinin yolunu güncelleştirilmelidir JSON metnini, aynı zamanda eskisinin üzerine yeni bir değer belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6970b-152">The JSON_MODIFY function lets you specify the path of the value in the JSON text that should be updated, as well as a new value that will overwrite the old one.</span></span> <span data-ttu-id="6970b-153">Bu şekilde tüm yapısını yeniden ayrıştırmayı olmadan kolayca JSON metnini güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6970b-153">This way you can easily update JSON text without reparsing the entire structure.</span></span>

<span data-ttu-id="6970b-154">JSON standart metin olarak kaydedildiği metin sütunlarında depolanan değerleri düzgün biçimlendirilmiş garanti vardır.</span><span class="sxs-lookup"><span data-stu-id="6970b-154">Since JSON is stored in a standard text, there are no guarantees that the values stored in text columns are properly formatted.</span></span> <span data-ttu-id="6970b-155">Standart Azure SQL veritabanı denetimi kısıtlamaları ve ISJSON işlevi kullanarak, JSON sütunda depolanan metin düzgün biçimlendirildiğinden doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6970b-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and the ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="6970b-156">Giriş metni düzgün biçimlendirildiğinden, JSON, ISJSON işlevi, 1 değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="6970b-156">If the input text is properly formatted JSON, the ISJSON function returns the value 1.</span></span> <span data-ttu-id="6970b-157">Her INSERT veya update JSON sütunun üzerinde bu kısıtlamayı yeni metin değeri hatalı biçimlendirilmiş JSON olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="6970b-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="6970b-158">JSON tablo biçimine dönüştürme</span><span class="sxs-lookup"><span data-stu-id="6970b-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="6970b-159">Azure SQL veritabanı, tablo biçiminde ve yükleme veya sorgu JSON veri JSON koleksiyonlara dönüştürme sağlar.</span><span class="sxs-lookup"><span data-stu-id="6970b-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="6970b-160">OPENJSON JSON metni ayrıştırır, JSON nesnelerinin bir dizisi bulur, dizinin öğeleri tekrarlanan ve elde edilen sonucu dizideki her öğe için bir satır döndürür tablo değerli bir işlevdir.</span><span class="sxs-lookup"><span data-stu-id="6970b-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through the elements of the array, and returns one row in the output result for each element of the array.</span></span>

![JSON tablo](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="6970b-162">Yukarıdaki örnekte, biz açılması gerekir ($expand. JSON dizisi bulmanın nerede depolanacağını belirtebilirsiniz Siparişleri yolu), hangi sütunların sonuç ve hücreler olarak döndürülecek JSON değerlerin nereden olarak döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="6970b-162">In the example above, we can specify where to locate the JSON array that should be opened (in the $.Orders path), what columns should be returned as result, and where to find the JSON values that will be returned as cells.</span></span>

<span data-ttu-id="6970b-163">Biz bir JSON dizisi dönüştürebilirsiniz @orders değişkenine bir dizi satır, bu sonuç kümesi çözümlemek veya standart bir tabloya satır ekleme:</span><span class="sxs-lookup"><span data-stu-id="6970b-163">We can transform a JSON array in the @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

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
<span data-ttu-id="6970b-164">Bir JSON dizisi olarak biçimlendirilmiş ve saklı yordama parametre ayrıştırılır ve siparişleri tabloya eklenen verilen siparişler topluluğu.</span><span class="sxs-lookup"><span data-stu-id="6970b-164">The collection of orders formatted as a JSON array and provided as a parameter to the stored procedure can be parsed and inserted into the Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6970b-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6970b-165">Next steps</span></span>
<span data-ttu-id="6970b-166">JSON uygulamanıza tümleştirmek öğrenmek için aşağıdaki kaynaklara gözatın:</span><span class="sxs-lookup"><span data-stu-id="6970b-166">To learn how to integrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="6970b-167">TechNet blogu</span><span class="sxs-lookup"><span data-stu-id="6970b-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="6970b-168">MSDN belgelerine</span><span class="sxs-lookup"><span data-stu-id="6970b-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="6970b-169">Kanal 9 video</span><span class="sxs-lookup"><span data-stu-id="6970b-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="6970b-170">JSON uygulamanıza tümleştirmek için çeşitli senaryoları hakkında bilgi edinmek için bu demo görmek [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) veya kullanım örneğinde eşleşen bir senaryo Bul [JSON Blog yazılarını](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span><span class="sxs-lookup"><span data-stu-id="6970b-170">To learn about various scenarios for integrating JSON into your application, see the demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

