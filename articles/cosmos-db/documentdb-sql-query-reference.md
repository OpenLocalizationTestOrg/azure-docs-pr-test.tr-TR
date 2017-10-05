---
title: "Azure DB Cosmos DocumentDB API: SQL söz dizimi | Microsoft Docs"
description: "Azure Cosmos DB DocumentDB API SQL sorgu dili için başvuru belgeleri."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 06/13/2017
ms.author: mimig
ms.openlocfilehash: 63b2d20c74df4fd6173994ee1a727594ba8afba3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="ff6e3-103">Azure DB Cosmos DocumentDB API: SQL söz dizimi başvurusu</span><span class="sxs-lookup"><span data-stu-id="ff6e3-103">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="ff6e3-104">Azure Cosmos DB DocumentDB API tanıdık SQL (yapılandırılmış sorgu dili) kullanarak belgelerin sorgulanmasını dilbilgisi gibi hiyerarşik JSON belgelerini gerektirmeden açık şema veya ikincil dizinlerin oluşturulmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-104">The Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="ff6e3-105">Bu konu, başvuru belgeleri DocumentDB API SQL sorgu dili için sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-105">This topic provides reference documentation for the DocumentDB API SQL query language.</span></span>

<span data-ttu-id="ff6e3-106">DocumentDB API SQL sorgu dili için bkz [SQL sorgularını Azure Cosmos DB DocumentDB API için](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="ff6e3-106">For a walkthrough of the DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="ff6e3-107">Ayrıca ziyaret etmek için davet ediyoruz [Query Playground](http://www.documentdb.com/sql/demo) burada Azure Cosmos DB deneyin ve SQL sorgularını kümemize karşı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-107">We also invite you to visit the [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="ff6e3-108">SEÇME sorgusu</span><span class="sxs-lookup"><span data-stu-id="ff6e3-108">SELECT query</span></span>  
<span data-ttu-id="ff6e3-109">JSON belgeleri veritabanından alır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-109">Retrieves JSON documents from the database.</span></span> <span data-ttu-id="ff6e3-110">İfade değerlendirme, filtreleme tahminleri destekler ve birleştirir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-110">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="ff6e3-111">Seçim deyimleri tanımlamak için kullanılan kuralları sözdizimi kuralları bölümünde tabloda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-111">The conventions used for describing the SELECT statements are tabulated in the Syntax conventions section.</span></span>  
  
<span data-ttu-id="ff6e3-112">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-112">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="ff6e3-113">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-113">**Remarks**</span></span>  
  
 <span data-ttu-id="ff6e3-114">Ayrıntılar için bölümlere her yan tümcesi aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-114">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="ff6e3-115">SELECT yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-115">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="ff6e3-116">FROM yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-116">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="ff6e3-117">WHERE yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-117">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="ff6e3-118">ORDER BY yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-118">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="ff6e3-119">SELECT deyiminde yan tümceleri, yukarıda gösterildiği gibi sıralanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-119">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="ff6e3-120">İsteğe bağlı bir yan tümceleri herhangi biri atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-120">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="ff6e3-121">Ancak isteğe bağlı bir yan tümceleri kullanıldığında, doğru sırayla görünmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-121">But when optional clauses are used, they must appear in the right order.</span></span>  
  
<span data-ttu-id="ff6e3-122">**SELECT deyimi mantıksal işleme sırası**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-122">**Logical Processing Order of the SELECT statement**</span></span>  
  
<span data-ttu-id="ff6e3-123">Yan tümceleri işlenme sırası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-123">The order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="ff6e3-124">FROM yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-124">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="ff6e3-125">WHERE yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-125">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="ff6e3-126">ORDER BY yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-126">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="ff6e3-127">SELECT yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-127">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="ff6e3-128">Bu sözdiziminde görünme sırasını farklı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-128">Note that this is different from the order in which they appear in the syntax.</span></span> <span data-ttu-id="ff6e3-129">İşlenen yan tümcesi ile sunulan tüm yeni sembolleri görünür ve daha sonra işlenen yan tümcelerinde kullanılabilir gibi sıralama olmamasıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-129">The ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="ff6e3-130">Örneğin, bir FROM yan tümcesinde bildirilen diğer adlar WHERE erişilebilir ve SELECT yan tümceleri.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-130">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="ff6e3-131">**Boşluk karakterleri ve açıklamaları**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-131">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="ff6e3-132">Tırnak içine alınan bir dizeyi bir parçası olmayan veya tanımlayıcı tırnak içine alınmış tüm boşluk karakterleri dil dilbilgisi parçası olmayan ve ayrıştırma sırasında yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-132">All white space characters which are not part of a quoted string or quoted identifier are not part of the language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="ff6e3-133">T-SQL stili yorumlar gibi sorgu dili destekler</span><span class="sxs-lookup"><span data-stu-id="ff6e3-133">The query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="ff6e3-134">SQL deyimi`-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-134">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="ff6e3-135">Boşluk karakterleri ve açıklamalar herhangi anlamlı dilbilgisi değil olsa da, belirteçlerin ayırmak için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-135">While whitespace characters and comments do not have any significance in the grammar, they must be used to separate tokens.</span></span> <span data-ttu-id="ff6e3-136">Örneğin: `-1e5` bir tek sayı belirteç süre olan`: – 1 e5` eksi bir belirteç numarası 1 ve tanımlayıcı e5 tarafından izlenir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-136">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="ff6e3-137"><a name="bk_select_query"></a>SELECT yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-137"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="ff6e3-138">SELECT deyiminde yan tümceleri, yukarıda gösterildiği gibi sıralanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-138">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="ff6e3-139">İsteğe bağlı bir yan tümceleri herhangi biri atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-139">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="ff6e3-140">Ancak isteğe bağlı bir yan tümceleri kullanıldığında, doğru sırayla görünmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-140">But when optional clauses are used, they must appear in the right order.</span></span>  

<span data-ttu-id="ff6e3-141">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-141">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="ff6e3-142">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-142">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="ff6e3-143">Özellikler veya sonuç kümesi için seçilecek değeri.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-143">Properties or value to be selected for the result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="ff6e3-144">Değer herhangi bir değişiklik yapmadan alınması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-144">Specifies that the value should be retrieved without making any changes.</span></span> <span data-ttu-id="ff6e3-145">İşlenen değer bir nesne ise, özellikle, tüm özellikler alınır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-145">Specifically if the processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="ff6e3-146">Alınacak özellikler listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-146">Specifies the list of properties to be retrieved.</span></span> <span data-ttu-id="ff6e3-147">Her döndürülen değeri, belirtilen özellikleri olan bir nesne olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-147">Each returned value will be an object with the properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="ff6e3-148">JSON değeri yerine tam JSON nesnesi alınması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-148">Specifies that the JSON value should be retrieved instead of the complete JSON object.</span></span> <span data-ttu-id="ff6e3-149">Bu, aksine `<property_list>` Öngörülen Değer bir nesne içinde kaymasını değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-149">This, unlike `<property_list>` does not wrap the projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="ff6e3-150">Hesaplanacak değerin temsil eden ifadesi.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-150">Expression representing the value to be computed.</span></span> <span data-ttu-id="ff6e3-151">Bkz: [skaler ifadelerin](#bk_scalar_expressions) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-151">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="ff6e3-152">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-152">**Remarks**</span></span>  
  
<span data-ttu-id="ff6e3-153">`SELECT *` Sözdizimi geçerli yalnızca tam olarak bir diğer ad belirtmiş FROM yan tümcesi varsa.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-153">The `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="ff6e3-154">`SELECT *`projeksiyon gerektiğinde yararlı olabilecek bir kimlik projeksiyon sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-154">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="ff6e3-155">SEÇİN * yalnızca FROM yan tümcesi belirtilirse geçerlidir ve yalnızca tek bir giriş kaynağı sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-155">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="ff6e3-156">Unutmayın `SELECT <select_list>` ve `SELECT *` "söz dizimi sugar" olduğunu ve bunun yerine aşağıda gösterildiği gibi basit SELECT deyimi kullanılarak belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-156">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="ff6e3-157">eşdeğerdir:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-157">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="ff6e3-158">eşdeğerdir:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-158">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="ff6e3-159">**Ayrıca bkz.**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-159">**See Also**</span></span>  
  
[<span data-ttu-id="ff6e3-160">Skaler ifade</span><span class="sxs-lookup"><span data-stu-id="ff6e3-160">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="ff6e3-161">SELECT yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-161">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="ff6e3-162"><a name="bk_from_clause"></a>FROM yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-162"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="ff6e3-163">Kaynak veya birleştirilmiş kaynakları belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-163">Specifies the source or joined sources.</span></span> <span data-ttu-id="ff6e3-164">FROM yan tümcesi isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-164">The FROM clause is optional.</span></span> <span data-ttu-id="ff6e3-165">Aksi durumda belirtilen, diğer yan tümceleri hala FROM yan tümcesi tek bir belgenin sağladıysanız olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-165">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="ff6e3-166">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-166">**Syntax**</span></span>  
  
```  
FROM <from_specification>  
  
<from_specification> ::=   
        <from_source> {[ JOIN <from_source>][,...n]}  
  
<from_source> ::=   
          <collection_expression> [[AS] input_alias]  
        | input_alias IN <collection_expression>  
  
<collection_expression> ::=   
        ROOT   
     | collection_name  
     | input_alias  
     | <collection_expression> '.' property_name  
     | <collection_expression> '[' "property_name" | array_index ']'  
```  
  
<span data-ttu-id="ff6e3-167">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-167">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="ff6e3-168">Bir veri kaynağı olan veya olmayan bir diğer ad belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-168">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="ff6e3-169">Diğer ad belirtilmezse, gelen çıkarılabilir olacaktır `<collection_expression>` kuralları kullanarak:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-169">If alias is not specified, it will be inferred from the `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="ff6e3-170">İfade bir toplama_adı ise, toplama_adı bir diğer ad olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-170">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="ff6e3-171">İfade ise `<collection_expression>`, property_name sonra property_name bir diğer ad olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-171">If the expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="ff6e3-172">İfade bir toplama_adı ise, toplama_adı bir diğer ad olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-172">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="ff6e3-173">OLARAK`input_alias`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-173">AS `input_alias`</span></span>  
  
<span data-ttu-id="ff6e3-174">Belirleyen `input_alias` temel Toplama ifadesi tarafından döndürülen değerler kümesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-174">Specifies that the `input_alias` is a set of values returned by the underlying collection expression.</span></span>  
 
<span data-ttu-id="ff6e3-175">`input_alias`IN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-175">`input_alias` IN</span></span>  
  
<span data-ttu-id="ff6e3-176">Belirleyen `input_alias` temel Toplama ifadesi tarafından döndürülen her dizinin tüm dizi öğeleri üzerinde yineleme tarafından elde edilen değerleri kümesi temsil etmelidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-176">Specifies that the `input_alias` should represent the set of values obtained by iterating over all array elements of each array returned by the underlying collection expression.</span></span> <span data-ttu-id="ff6e3-177">Dizi olmayan temel Toplama ifadesi tarafından döndürülen herhangi bir değer yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-177">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="ff6e3-178">Belge almak için kullanılacak Toplama ifadesi belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-178">Specifies the collection expression to be used to retrieve the documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="ff6e3-179">Bu belge varsayılan olarak şu anda bağlı koleksiyonu alınması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-179">Specifies that document should be retrieved from the default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="ff6e3-180">Bu belgede sağlanan koleksiyondan alınması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-180">Specifies that document should be retrieved from the provided collection.</span></span> <span data-ttu-id="ff6e3-181">Koleksiyon adı şu anda bağlı koleksiyonunun adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-181">The name of the collection must match the name of the collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="ff6e3-182">Bu belgede sağlanan diğer adı tarafından tanımlanan diğer kaynaktan alınması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-182">Specifies that document should be retrieved from the other source defined by the provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="ff6e3-183">Bu belge erişerek alınabilir belirtir `property_name` özelliği veya dizi_dizini dizi öğesi tarafından alınan tüm belgeler için belirtilen toplama ifadesi.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-183">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="ff6e3-184">Bu belge erişerek alınabilir belirtir `property_name` özelliği veya dizi_dizini dizi öğesi tarafından alınan tüm belgeler için belirtilen toplama ifadesi.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-184">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="ff6e3-185">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-185">**Remarks**</span></span>  
  
<span data-ttu-id="ff6e3-186">Tüm diğer adlar sağlanan veya içinde çıkarımı yapılan `<from_source>(`s) benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-186">All aliases provided or inferred in the `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="ff6e3-187">Sözdizimi `<collection_expression>.`property_name aynı olup `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-187">The Syntax `<collection_expression>.`property_name is the same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="ff6e3-188">Ancak, bir özellik adı tanımlayıcı olmayan karakterleri içeriyorsa, ikinci sözdizimi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-188">However, the latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="ff6e3-189">**Dizi öğeleri eksik özellikleri eksik değerleri işleme tanımlanmamış**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-189">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="ff6e3-190">Bir toplama ifadesi özellikleri veya dizi öğeleri ve değer yok erişirse, bu değeri göz ardı ve daha fazla işlenmedi.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-190">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="ff6e3-191">**Toplama ifadesi içerik kapsamı**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-191">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="ff6e3-192">Bir toplama ifadesi koleksiyonu kapsamlı veya belge kapsamlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-192">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="ff6e3-193">Temel alınan kaynak koleksiyonu ifadesinin ya da kök ise koleksiyonu kapsamlı, ifade olan veya `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-193">An expression is collection-scoped, if the underlying source of the collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="ff6e3-194">Bu tür bir ifade koleksiyondan doğrudan alınan belgeleri kümesini temsil eder ve diğer toplama ifadeleri işlenmesini bağımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-194">Such an expression represents a set of documents retrieved from the collection directly, and is not dependent on the processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="ff6e3-195">Belge temel alınan kaynak koleksiyonu ifadesinin ise kapsamlı, ifade olan `input_alias` sorgu sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-195">An expression is document-scoped, if the underlying source of the collection expression is `input_alias` introduced earlier in the query.</span></span> <span data-ttu-id="ff6e3-196">Bu tür bir ifade diğer koleksiyonla ilişkili kümesine ait her bir belgenin kapsamında toplama ifadesinin hesaplanmasıyla elde belgeleri kümesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-196">Such an expression represents a set of documents obtained by evaluating the collection expression in the scope of each document belonging to the set associated with the aliased collection.</span></span>  <span data-ttu-id="ff6e3-197">Sonuç kümesi her temel kümesindeki belgelerin toplama ifadesinin hesaplanmasıyla elde edilen kümeleri birleşim olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-197">The resulting set will be a union of sets obtained by evaluating the collection expression for each of the documents in the underlying set.</span></span>  
  
<span data-ttu-id="ff6e3-198">**Birleşimler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-198">**Joins**</span></span>  
  
<span data-ttu-id="ff6e3-199">Geçerli sürümde Azure Cosmos DB iç birleştirmeler destekler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-199">In the current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="ff6e3-200">Ek birleştirme özellikleri yeni çıkacak.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-200">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="ff6e3-201">İç birleşimler birleştirme katılan kümelerinin eksiksiz bir çapraz ürün sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-201">Inner joins result in a complete cross product of the sets participating in the join.</span></span> <span data-ttu-id="ff6e3-202">Burada yer alan tanımlama grubu içindeki her değerin katılmasını birleştirme ayarlamak diğer adı ile ilişkili ve söz konusu diğer ad diğer yan tümcelerinde başvurarak erişilen N-öğe başlık kümesi bir N yönlü birleştirme sonucudur.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-202">The result of an N-way join is a set of N-element tuples, where each value in the tuple is associated with the aliased set participating in the join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="ff6e3-203">Değerlendirme katılma katılımcı ayarlar bağlamı kapsamına bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-203">The evaluation of the join depends on the context scope of the participating sets:</span></span>  
  
-  <span data-ttu-id="ff6e3-204">Bir birleştirme arasında koleksiyon kümesi A ve koleksiyon kapsamlı B, A ve b kümelerindeki tüm öğelerin çapraz ürün sonuçları ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ff6e3-204">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="ff6e3-205">Tüm ayarlar her belge için B A. belge kapsamlı ayarlama değerlendirerek elde birleşimi sonuçlanıyor kümesi belge kapsamlı kümesi B arasındaki bir birleştirme</span><span class="sxs-lookup"><span data-stu-id="ff6e3-205">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="ff6e3-206">Geçerli sürümde, bir koleksiyon kapsamlı ifade maksimum Sorgu işlemcisi tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-206">In the current release, a maximum of one collection-scoped expression is supported by the query processor.</span></span>  
  
<span data-ttu-id="ff6e3-207">**Birleştirme örnekleri:**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-207">**Examples of joins:**</span></span>  
  
<span data-ttu-id="ff6e3-208">Aşağıdaki FROM yan tümcesi bakalım:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-208">Let's look at the following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="ff6e3-209">Tanımlamak her kaynak izin `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-209">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="ff6e3-210">Bu FROM yan tümcesi N-diziler (tuple N değerlerle) kümesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-210">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="ff6e3-211">Her tanımlama grubu tüm koleksiyon diğer adları kendi ilgili ayarlar yineleme tarafından üretilen değerler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-211">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="ff6e3-212">*Örnek 1, 2 kaynaklarıyla KATIL:*</span><span class="sxs-lookup"><span data-stu-id="ff6e3-212">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="ff6e3-213">Let `<from_source1>` koleksiyonu kapsamlı ve kümesi {A, B, C} temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-213">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="ff6e3-214">Let `<from_source2>` input_alias1 başvuran belge kapsamlı ve ayarlar temsil eder:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-214">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="ff6e3-215">{1, 2} için`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-215">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="ff6e3-216">için {3}`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-216">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="ff6e3-217">{4, 5} için`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-217">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="ff6e3-218">FROM yan tümcesi `<from_source1> JOIN <from_source2>` aşağıdaki başlıklar neden olur:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-218">The FROM clause `<from_source1> JOIN <from_source2>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="ff6e3-219">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="ff6e3-219">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="ff6e3-220">*Örnek 2, 3 kaynaklarıyla KATIL:*</span><span class="sxs-lookup"><span data-stu-id="ff6e3-220">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="ff6e3-221">Let `<from_source1>` koleksiyonu kapsamlı ve kümesi {A, B, C} temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-221">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="ff6e3-222">Let `<from_source2>` belge kapsamlı başvuran olması `input_alias1` ve ayarlar temsil eder:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-222">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="ff6e3-223">{1, 2} için`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-223">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="ff6e3-224">için {3}`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-224">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="ff6e3-225">{4, 5} için`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-225">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="ff6e3-226">Let `<from_source3>` belge kapsamlı başvuran olması `input_alias2` ve ayarlar temsil eder:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-226">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="ff6e3-227">{100, 200} için`input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-227">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="ff6e3-228">{300} için`input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-228">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="ff6e3-229">FROM yan tümcesi `<from_source1> JOIN <from_source2> JOIN <from_source3>` aşağıdaki başlıklar neden olur:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-229">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="ff6e3-230">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="ff6e3-230">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="ff6e3-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="ff6e3-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ff6e3-232">Diğer değerler için diziler eksikliği `input_alias1`, `input_alias2`, kendisi için `<from_source3>` hiçbir değer döndürmedi.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-232">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which the `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="ff6e3-233">*Örnek 3, 3 kaynaklarıyla KATIL:*</span><span class="sxs-lookup"><span data-stu-id="ff6e3-233">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="ff6e3-234">< Koleksiyon kapsamlı ve {A, B, C} kümesini temsil eden from_source1 > olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-234">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="ff6e3-235">Let `<from_source1>` koleksiyonu kapsamlı ve kümesi {A, B, C} temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-235">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="ff6e3-236">< Belge kapsamlı başvuru input_alias1 olması ve ayarlar temsil from_source2 > sağlar:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-236">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="ff6e3-237">{1, 2} için`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-237">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="ff6e3-238">için {3}`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-238">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="ff6e3-239">{4, 5} için`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-239">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="ff6e3-240">Let `<from_source3>` kapsamlı `input_alias1` ve ayarlar temsil eder:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-240">Let `<from_source3>` be scoped to `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="ff6e3-241">{100, 200} için`input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-241">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="ff6e3-242">{300} için`input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="ff6e3-242">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="ff6e3-243">FROM yan tümcesi `<from_source1> JOIN <from_source2> JOIN <from_source3>` aşağıdaki başlıklar neden olur:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-243">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="ff6e3-244">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="ff6e3-244">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="ff6e3-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), (C, 4, 300) (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="ff6e3-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="ff6e3-246">Bu arasında çapraz ürün ile sonuçlandı `<from_source2>` ve `<from_source3>` her ikisi de aynı kapsamındaki çünkü `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-246">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped to the same `<from_source1>`.</span></span>  <span data-ttu-id="ff6e3-247">Bu 4 (2 x 2) sonuçlandı diziler değerini 0 diziler B (1 x 0) değeri sahip olması ve 2 (2 x 1) değeri C. diziler</span><span class="sxs-lookup"><span data-stu-id="ff6e3-247">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="ff6e3-248">**Ayrıca bkz.**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-248">**See also**</span></span>  
  
 [<span data-ttu-id="ff6e3-249">SELECT yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-249">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="ff6e3-250"><a name="bk_where_clause"></a>WHERE yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-250"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="ff6e3-251">Sorgu tarafından döndürülen belgeler için arama koşulu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-251">Specifies the search condition for the documents returned by the query.</span></span>  
  
 <span data-ttu-id="ff6e3-252">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-252">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="ff6e3-253">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-253">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="ff6e3-254">Döndürülecek belgeler için karşılanması gereken koşulu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-254">Specifies the condition to be met for the documents to be returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="ff6e3-255">Hesaplanacak değerin temsil eden ifadesi.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-255">Expression representing the value to be computed.</span></span> <span data-ttu-id="ff6e3-256">Bkz: [skaler ifadelerin](#bk_scalar_expressions) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-256">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="ff6e3-257">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-257">**Remarks**</span></span>  
  
 <span data-ttu-id="ff6e3-258">Filtre olarak belirtilen bir ifade döndürülecek belge için sırayla koşulunu true olarak değerlendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-258">In order for the document to be returned an expression specified as filter condition must evaluate to true.</span></span> <span data-ttu-id="ff6e3-259">Boole değeri true koşulu, başka bir değer yerine getirecek yalnızca: tanımlanmamış, null, false, sayı, dizi veya nesne uygun olmadığı koşul.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-259">Only Boolean value true will satisfy the condition, any other value: undefined, null, false, Number, Array or Object will not satisfy the condition.</span></span>  
  
##  <span data-ttu-id="ff6e3-260"><a name="bk_orderby_clause"></a>ORDER BY yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-260"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="ff6e3-261">Sorgu tarafından döndürülen sonuçları sıralama düzenini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-261">Specifies the sorting order for results returned by the query.</span></span>  
  
 <span data-ttu-id="ff6e3-262">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-262">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="ff6e3-263">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-263">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="ff6e3-264">Bir özellik veya sorgu sonucu kümesi sıralama yapılacak ifade belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-264">Specifies a property or expression on which to sort the query result set.</span></span> <span data-ttu-id="ff6e3-265">Sıralama sütunu adı veya sütun diğer adı belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-265">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="ff6e3-266">Birden çok sütunları sıralama belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-266">Multiple sort columns can be specified.</span></span> <span data-ttu-id="ff6e3-267">Sütun adları benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-267">Column names must be unique.</span></span> <span data-ttu-id="ff6e3-268">ORDER BY yan tümcesinde sütunları sıralama sırasını sıralanmış sonuç kümesi organizasyonu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-268">The sequence of the sort columns in the ORDER BY clause defines the organization of the sorted result set.</span></span> <span data-ttu-id="ff6e3-269">Diğer bir deyişle, sonuç kümesi ilk özelliği tarafından sıralanır ve ardından bu sıralı liste ikinci özelliği vb. göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-269">That is, the result set is sorted by the first property and then that ordered list is sorted by the second property, and so on.</span></span>  
  
     <span data-ttu-id="ff6e3-270">ORDER BY yan tümcesinde başvurulan sütun adları seçim listesindeki bir sütun veya herhangi belirsizlikleri olmadan FROM yan tümcesinde belirtilen bir tablodaki tanımlanmış bir sütuna karşılık gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-270">The column names referenced in the ORDER BY clause must correspond to either a column in the select list or to a column defined in a table specified in the FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="ff6e3-271">Tek bir özellik veya sorgu sonucu kümesi sıralama yapılacak ifade belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-271">Specifies a single property or expression on which to sort the query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="ff6e3-272">Bkz: [skaler ifadelerin](#bk_scalar_expressions) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-272">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="ff6e3-273">Belirtilen sütunundaki değerler artan veya azalan sırada sıralanması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-273">Specifies that the values in the specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="ff6e3-274">ASC en düşük değerden yüksek değere sıralar.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-274">ASC sorts from the lowest value to highest value.</span></span> <span data-ttu-id="ff6e3-275">DESC en yüksek değerden düşük değere sıralar.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-275">DESC sorts from highest value to lowest value.</span></span> <span data-ttu-id="ff6e3-276">ASC varsayılan sıralama düzeni ' dir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-276">ASC is the default sort order.</span></span> <span data-ttu-id="ff6e3-277">Null değerler en düşük olası değerler kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-277">Null values are treated as the lowest possible values.</span></span>  
  
 <span data-ttu-id="ff6e3-278">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-278">**Remarks**</span></span>  
  
 <span data-ttu-id="ff6e3-279">Sorgu dilbilgisi özellikleri tarafından birden çok sipariş desteklerken, yalnızca tek bir özellik, yalnızca adlarla ve özellik adları, yani, hesaplanan özellikleri karşı sıralama Azure Cosmos DB sorgu çalışma zamanı destekler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-279">While the query grammar supports multiple order by properties, the Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="ff6e3-280">Sıralama, ayrıca dizin oluşturma ilkesi özelliği ve en yüksek duyarlık ile belirtilen tür için bir aralığı dizini içerir gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-280">Sorting also requires that the indexing policy includes a range index for the property and the specified type, with the maximum precision.</span></span> <span data-ttu-id="ff6e3-281">Daha fazla ayrıntı için dizin oluşturma ilkesi belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-281">Refer to the indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="ff6e3-282"><a name="bk_scalar_expressions"></a>Skaler ifade</span><span class="sxs-lookup"><span data-stu-id="ff6e3-282"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="ff6e3-283">Skaler bir ifade, simgeler ve tek bir değer almak için değerlendirilen işleçleri birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-283">A scalar expression is a combination of symbols and operators that can be evaluated to obtain a single value.</span></span> <span data-ttu-id="ff6e3-284">Basit ifadeler sabitler, özellik başvuruları, dizi öğesi başvuruları, diğer başvurular veya işlev çağrılarını olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-284">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="ff6e3-285">Basit ifadeler işleçleri kullanarak karmaşık ifadelere birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-285">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="ff6e3-286">Hangi skaler ifade olabilir değerleri hakkında daha fazla bilgi için bkz: [sabitleri](#bk_constants) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-286">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="ff6e3-287">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-287">**Syntax**</span></span>  
  
```  
<scalar_expression> ::=  
       <constant>   
     | input_alias   
     | parameter_name  
     | <scalar_expression>.property_name  
     | <scalar_expression>'['"property_name"|array_index']'  
     | unary_operator <scalar_expression>  
     | <scalar_expression> binary_operator <scalar_expression>    
     | <scalar_expression> ? <scalar_expression> : <scalar_expression>  
     | <scalar_function_expression>  
     | <create_object_expression>   
     | <create_array_expression>  
     | (<scalar_expression>)   
  
<scalar_function_expression> ::=  
        'udf.' Udf_scalar_function([<scalar_expression>][,…n])  
        | builtin_scalar_function([<scalar_expression>][,…n])  
  
<create_object_expression> ::=  
   '{' [{property_name | "property_name"} : <scalar_expression>][,…n] '}'  
  
<create_array_expression> ::=  
   '[' [<scalar_expression>][,…n] ']'  
  
```  
  
 <span data-ttu-id="ff6e3-288">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-288">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="ff6e3-289">Sabit bir değeri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-289">Represents a constant value.</span></span> <span data-ttu-id="ff6e3-290">Bkz: [sabitleri](#bk_constants) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-290">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="ff6e3-291">Tarafından tanımlanan bir değeri temsil `input_alias` sunulan `FROM` yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-291">Represents a value defined by the `input_alias` introduced in the `FROM` clause.</span></span>  
    <span data-ttu-id="ff6e3-292">Bu değer olmayan olması garanti **tanımsız** –**tanımsız** giriş değerleri atlanır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-292">This value is guaranteed to not be **undefined** –**undefined** values in the input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="ff6e3-293">Bir nesnenin özellik değerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-293">Represents a value of the property of an object.</span></span> <span data-ttu-id="ff6e3-294">Özelliği mevcut değil veya özellik bir nesne olmayan bir değer başvurulan durumunda için ifadeyi hesaplar **tanımsız** değeri.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-294">If the property does not exist or property is referenced on a value which is not an object, then the expression evaluates to **undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="ff6e3-295">Ada sahip özelliğin değerini temsil eden `property_name` veya dizi öğesi dizine sahip `array_index` nesne/dizisi.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-295">Represents a value of the property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="ff6e3-296">Özellik/dizi dizini yok veya nesne/dizi olmayan bir değer özelliği/dizi dizini başvurulan, ifade için Tanımsız değer değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-296">If the property/array index does not exist or the property/array index is referenced on a value which is not an object/array, then the expression evaluates to undefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="ff6e3-297">Tek bir değer uygulanan bir işleç temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-297">Represents an operator that is applied to a single value.</span></span> <span data-ttu-id="ff6e3-298">Bkz: [işleçleri](#bk_operators) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-298">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="ff6e3-299">İki değer için uygulanan bir işleç temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-299">Represents an operator that is applied to two values.</span></span> <span data-ttu-id="ff6e3-300">Bkz: [işleçleri](#bk_operators) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-300">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="ff6e3-301">İşlev çağrısının sonucunu tarafından tanımlanan bir değeri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-301">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="ff6e3-302">Kullanıcının adını skaler işlev tanımlı.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-302">Name of the user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="ff6e3-303">Yerleşik skaler işlev adı.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-303">Name of the built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="ff6e3-304">Belirtilen özelliklere sahip yeni bir nesne oluşturarak alınan bir değer ve bunların değerleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-304">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="ff6e3-305">Öğeleri olarak belirtilen değerlerle yeni bir dizi oluşturarak elde bir değeri temsil eder</span><span class="sxs-lookup"><span data-stu-id="ff6e3-305">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="ff6e3-306">Belirtilen parametre adı değerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-306">Represents a value of the specified parameter name.</span></span> <span data-ttu-id="ff6e3-307">Parametre adları @ tek bir ilk karakter olarak olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-307">Parameter names must have a single @ as the first character.</span></span>  
  
 <span data-ttu-id="ff6e3-308">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-308">**Remarks**</span></span>  
  
 <span data-ttu-id="ff6e3-309">Bir yerleşik veya kullanıcı çağırma skaler işlev tanımlandığında tüm bağımsız değişkenler tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-309">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="ff6e3-310">Bağımsız değişkenlerden biri ise tanımlanmamış, işlev çağrılmaz ve sonucu tanımsız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-310">If any of the arguments is undefined, the function will not be called and the result will be undefined.</span></span>  
  
 <span data-ttu-id="ff6e3-311">Bir nesne oluştururken Tanımsız değer atanmış herhangi bir özelliği atlandı ve oluşturulan nesnesinde yer almayan.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-311">When creating an object, any property that is assigned undefined value will be skipped and not included in the created object.</span></span>  
  
 <span data-ttu-id="ff6e3-312">Ne zaman herhangi bir öğeyi değer bir dizi oluşturma atanmış **tanımsız** değeri atlandı ve oluşturulan nesnesinde dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-312">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in the created object.</span></span> <span data-ttu-id="ff6e3-313">Bu, oluşturulan dizi dizinleri atlandı değil, şekilde yerini alacak sonraki tanımlanan öğe neden olur.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-313">This will cause the next defined element to take its place in such a way that the created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="ff6e3-314"><a name="bk_operators"></a>İşleçler</span><span class="sxs-lookup"><span data-stu-id="ff6e3-314"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="ff6e3-315">Bu bölümde desteklenen işleçleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-315">This section describes the supported operators.</span></span> <span data-ttu-id="ff6e3-316">Her işleci tam olarak bir kategoriye atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-316">Each operator can be assigned to exactly one category.</span></span>  
  
 <span data-ttu-id="ff6e3-317">Bkz: **işleci kategorileri** Ayrıntılar için aşağıdaki tabloya işlenmesi ile ilgili **tanımsız** değerleri, giriş değerleri ve işleme türlerini eşleşmeyen ile değerlerin türü gereksinimleri.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-317">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="ff6e3-318">**İşleç kategoriler:**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-318">**Operator categories:**</span></span>  
  
|<span data-ttu-id="ff6e3-319">**Kategori**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-319">**Category**</span></span>|<span data-ttu-id="ff6e3-320">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-320">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="ff6e3-321">**aritmetik**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-321">**arithmetic**</span></span>|<span data-ttu-id="ff6e3-322">İşleç input(s) istendiğiniz olmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-322">Operator expects input(s) to be Number(s).</span></span> <span data-ttu-id="ff6e3-323">Çıktı ayrıca bir sayıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-323">Output is also a Number.</span></span> <span data-ttu-id="ff6e3-324">Herhangi biri ise **tanımsız** veya numarası sonra sonuç dışında türüdür **tanımsız**.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-324">If any of the inputs is **undefined** or type other than Number then the result is **undefined**.</span></span>|  
|<span data-ttu-id="ff6e3-325">**bit tabanlı**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-325">**bitwise**</span></span>|<span data-ttu-id="ff6e3-326">İşleç input(s) 32-bit işaretli tamsayıyı istendiğiniz olmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-326">Operator expects input(s) to be 32-bit signed integer Number(s).</span></span> <span data-ttu-id="ff6e3-327">Çıktı da 32 bit imzalı numarası tamsayıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-327">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="ff6e3-328">Herhangi bir tamsayı olmayan değer yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-328">Any non-integer value will be rounded.</span></span> <span data-ttu-id="ff6e3-329">Pozitif bir değer yuvarlanacağı, negatif değerleri yuvarlanan.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-329">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="ff6e3-330">32 bit tamsayı aralığın dışında herhangi bir değer, son 32 bitlik, iki kişinin tamamlama gösterimi gerçekleştirerek dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-330">Any value that is outside of the 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="ff6e3-331">Herhangi biri ise **tanımsız** sonuç sonra diğer, sayıdan yazın veya **tanımsız**.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-331">If any of the inputs is **undefined** or type other than Number, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="ff6e3-332">**Not:** yukarıdaki davranışı JavaScript bit düzeyinde işleci davranışı ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-332">**Note:** The above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="ff6e3-333">**mantıksal**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-333">**logical**</span></span>|<span data-ttu-id="ff6e3-334">İşleç input(s) Boolean(s) olmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-334">Operator expects input(s) to be Boolean(s).</span></span> <span data-ttu-id="ff6e3-335">Çıktı de bir Boole değeri olur.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-335">Output is also a Boolean.</span></span><br /><span data-ttu-id="ff6e3-336">Herhangi biri ise **tanımsız** sonucu olacaktır sonra Boolean, diğerinden yazın veya **tanımsız**.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-336">If any of the inputs is **undefined** or type other than Boolean, then the result will be **undefined**.</span></span>|  
|<span data-ttu-id="ff6e3-337">**Karşılaştırma**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-337">**comparison**</span></span>|<span data-ttu-id="ff6e3-338">İşleci, aynı türe sahip ve tanımsız olmaması için input(s) bekliyor.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-338">Operator expects input(s) to have the same type and not be undefined.</span></span> <span data-ttu-id="ff6e3-339">Çıktı bir Boole değeri değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-339">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="ff6e3-340">Herhangi biri ise **tanımsız** veya girişleri farklı türlerine sahip sonra sonuç **tanımsız**.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-340">If any of the inputs is **undefined** or the inputs have different types, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="ff6e3-341">Bkz: **karşılaştırma için değerlerin sıralama** ayrıntıları sıralama değeri için tablo.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-341">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="ff6e3-342">**dize**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-342">**string**</span></span>|<span data-ttu-id="ff6e3-343">İşleç input(s) dizelerini olmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-343">Operator expects input(s) to be String(s).</span></span> <span data-ttu-id="ff6e3-344">Çıktı ayrıca bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-344">Output is also a String.</span></span><br /><span data-ttu-id="ff6e3-345">Herhangi biri ise **tanımsız** sonuç sonra dize dışında yazın veya **tanımsız**.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-345">If any of the inputs is **undefined** or type other than String then the result is **undefined**.</span></span>|  
  
 <span data-ttu-id="ff6e3-346">**Birli işleçleri:**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-346">**Unary operators:**</span></span>  
  
|<span data-ttu-id="ff6e3-347">**Ad**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-347">**Name**</span></span>|<span data-ttu-id="ff6e3-348">**İşleci**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-348">**Operator**</span></span>|<span data-ttu-id="ff6e3-349">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-349">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="ff6e3-350">**aritmetik**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-350">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="ff6e3-351">Sayı değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-351">Returns the number value.</span></span><br /><br /> <span data-ttu-id="ff6e3-352">Bit tabanlı değil işlecini.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-352">Bitwise negation.</span></span> <span data-ttu-id="ff6e3-353">Sayı değeri tasarruflarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-353">Returns negated number value.</span></span>|  
|<span data-ttu-id="ff6e3-354">**bit tabanlı**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-354">**bitwise**</span></span>|~|<span data-ttu-id="ff6e3-355">Olanları tamamlama.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-355">Ones' complement.</span></span> <span data-ttu-id="ff6e3-356">Tamamlama sayı değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-356">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="ff6e3-357">**Mantıksal**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-357">**Logical**</span></span>|<span data-ttu-id="ff6e3-358">**DEĞİL**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-358">**NOT**</span></span>|<span data-ttu-id="ff6e3-359">Değilleme.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-359">Negation.</span></span> <span data-ttu-id="ff6e3-360">Boole değeri döndürür tasarruflarını.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-360">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="ff6e3-361">**İkili işleçler:**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-361">**Binary operators:**</span></span>  
  
|<span data-ttu-id="ff6e3-362">**Ad**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-362">**Name**</span></span>|<span data-ttu-id="ff6e3-363">**İşleci**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-363">**Operator**</span></span>|<span data-ttu-id="ff6e3-364">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-364">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="ff6e3-365">**aritmetik**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-365">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="ff6e3-366">Ayrıca.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-366">Addition.</span></span><br /><br /> <span data-ttu-id="ff6e3-367">Çıkarma.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-367">Subtraction.</span></span><br /><br /> <span data-ttu-id="ff6e3-368">Çarpma.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-368">Multiplication.</span></span><br /><br /> <span data-ttu-id="ff6e3-369">Bölme.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-369">Division.</span></span><br /><br /> <span data-ttu-id="ff6e3-370">Modülasyon.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-370">Modulation.</span></span>|  
|<span data-ttu-id="ff6e3-371">**bit tabanlı**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-371">**bitwise**</span></span>|<span data-ttu-id="ff6e3-372">&#124;</span><span class="sxs-lookup"><span data-stu-id="ff6e3-372">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="ff6e3-373">Bit düzeyinde OR.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-373">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="ff6e3-374">Bit düzeyinde and</span><span class="sxs-lookup"><span data-stu-id="ff6e3-374">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="ff6e3-375">Bit düzeyinde XOR.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-375">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="ff6e3-376">Sola kaydırma.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-376">Left Shift.</span></span><br /><br /> <span data-ttu-id="ff6e3-377">Sağa kaydırma.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-377">Right Shift.</span></span><br /><br /> <span data-ttu-id="ff6e3-378">Sıfır dolgu sağa kaydırma.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-378">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="ff6e3-379">**mantıksal**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-379">**logical**</span></span>|<span data-ttu-id="ff6e3-380">**VE**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-380">**AND**</span></span><br /><br /> <span data-ttu-id="ff6e3-381">**VEYA**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-381">**OR**</span></span>|<span data-ttu-id="ff6e3-382">Mantıksal ve işlecini.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-382">Logical conjunction.</span></span> <span data-ttu-id="ff6e3-383">Döndürür **true** iki bağımsız değişkenler ise **true**, döndürür **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-383">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="ff6e3-384">Mantıksal ve işlecini.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-384">Logical conjunction.</span></span> <span data-ttu-id="ff6e3-385">Döndürür **true** iki bağımsız değişkenler ise **true**, döndürür **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-385">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="ff6e3-386">**Karşılaştırma**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-386">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="ff6e3-387">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-387">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="ff6e3-388">**??**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-388">**??**</span></span>|<span data-ttu-id="ff6e3-389">Eşittir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-389">Equals.</span></span> <span data-ttu-id="ff6e3-390">Döndürür **true** bağımsız değişkenleri eşit olup olmadığını döndürür **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-390">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="ff6e3-391">Eşit değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-391">Not equal to.</span></span> <span data-ttu-id="ff6e3-392">Döndürür **true** bağımsız değişkenleri eşit değilse döndürür **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-392">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="ff6e3-393">Büyüktür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-393">Greater Than.</span></span> <span data-ttu-id="ff6e3-394">Döndürür **true** ilk bağımsız değişken ikinci sürümden daha büyükse, dönüş **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-394">Returns **true** if first argument is greater than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="ff6e3-395">Büyüktür veya eşittir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-395">Greater Than or Equal To.</span></span> <span data-ttu-id="ff6e3-396">Döndürür **true** ilk bağımsız değişkeni sıfırdan büyük veya eşit ikincisi ise, döndürür **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-396">Returns **true** if first argument is greater than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="ff6e3-397">Küçüktür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-397">Less Than.</span></span> <span data-ttu-id="ff6e3-398">Döndürür **true** ilk bağımsız değişken düşükse ikinci bir dönüş daha **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-398">Returns **true** if first argument is less than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="ff6e3-399">Küçük veya eşittir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-399">Less Than or Equal To.</span></span> <span data-ttu-id="ff6e3-400">Döndürür **true** ilk bağımsız değişken ikinci eşit veya daha az ise, döndürür **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-400">Returns **true** if first argument is less than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="ff6e3-401">Birleşim.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-401">Coalesce.</span></span> <span data-ttu-id="ff6e3-402">İlk bağımsız değişkeni ise, ikinci bağımsız değişkeni döndürür bir **tanımsız** değeri.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-402">Returns the second argument if the first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="ff6e3-403">**Dize**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-403">**String**</span></span>|<span data-ttu-id="ff6e3-404">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-404">**&#124;&#124;**</span></span>|<span data-ttu-id="ff6e3-405">Birleştirme.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-405">Concatenation.</span></span> <span data-ttu-id="ff6e3-406">Her iki değişken birleşimini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-406">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="ff6e3-407">**Üçlü işleçler:**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-407">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="ff6e3-408">Üçlü işleci</span><span class="sxs-lookup"><span data-stu-id="ff6e3-408">Ternary operator</span></span>|<span data-ttu-id="ff6e3-409">?</span><span class="sxs-lookup"><span data-stu-id="ff6e3-409">?</span></span>|<span data-ttu-id="ff6e3-410">İlk bağımsız değişken değerlendirilirse ikinci bağımsız değişkeni döndürür **true**; üçüncü bağımsız değişken yoksa döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-410">Returns the second argument if the first argument evaluates to **true**; return the third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="ff6e3-411">**Karşılaştırma için değerlerin sıralama**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-411">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="ff6e3-412">**Tür**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-412">**Type**</span></span>|<span data-ttu-id="ff6e3-413">**Değerleri sırası**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-413">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="ff6e3-414">**Tanımlanmamış**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-414">**Undefined**</span></span>|<span data-ttu-id="ff6e3-415">Karşılaştırılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-415">Not comparable.</span></span>|  
|<span data-ttu-id="ff6e3-416">**Null**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-416">**Null**</span></span>|<span data-ttu-id="ff6e3-417">Tek değer: **null**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-417">Single value: **null**</span></span>|  
|<span data-ttu-id="ff6e3-418">**Sayı**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-418">**Number**</span></span>|<span data-ttu-id="ff6e3-419">Doğal bir gerçek sayı.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-419">Natural real number.</span></span><br /><br /> <span data-ttu-id="ff6e3-420">Negatif sonsuz değerle diğer sayı değeri küçüktür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-420">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="ff6e3-421">Pozitif sonsuz değerle diğer numara değerden daha büyük. **NaN** değeri karşılaştırılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-421">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="ff6e3-422">İle karşılaştırma **NaN** sonuçlanır **tanımsız** değeri.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-422">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="ff6e3-423">**Dize**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-423">**String**</span></span>|<span data-ttu-id="ff6e3-424">Lexicographical sırası.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-424">Lexicographical order.</span></span>|  
|<span data-ttu-id="ff6e3-425">**Dizi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-425">**Array**</span></span>|<span data-ttu-id="ff6e3-426">Yoktur, ancak Tarafsız sıralaması.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-426">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="ff6e3-427">**Nesne**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-427">**Object**</span></span>|<span data-ttu-id="ff6e3-428">Yoktur, ancak Tarafsız sıralaması.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-428">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="ff6e3-429">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-429">**Remarks**</span></span>  
  
 <span data-ttu-id="ff6e3-430">Veritabanından alınan gerçekte kadar Azure Cosmos DB'de değerlerin türleri bilinen genellikle değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-430">In Azure Cosmos DB, the types of values are often not known until they are actually retrieved from the database.</span></span> <span data-ttu-id="ff6e3-431">Sorguları verimli yürütülmesini desteklemek için işleçler çoğunu sıkı tür gereksinimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-431">In order to support efficient execution of queries, most of the operators have strict type requirements.</span></span> <span data-ttu-id="ff6e3-432">Ayrıca kendilerini işleçleriyle örtük dönüşümler gerçekleştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-432">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="ff6e3-433">Bu sorguda ister anlamına gelir: seçin * gelen kök r WHERE r.Age = 21 yalnızca döndürecektir özelliği geçerlilik süresi ile belgeleri sayısına eşit 21.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-433">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal to the number 21.</span></span> <span data-ttu-id="ff6e3-434">Belgeleri özelliği geçerlilik süresi dizesi "21" veya "0021" dizesi eşit ile eşleşmez, "21" ifadesi olarak = 21 çok tanımsız değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-434">Documents with property Age equal to the string "21" or the string "0021" will not match, as the expression "21" = 21 evaluates to undefined.</span></span> <span data-ttu-id="ff6e3-435">Dizinlerin, daha iyi kullanımı için çünkü böylece belirli bir değer arama (yani 21 sayı) (yani numarası 21 veya dizeler "21", "021", "21.0"...) olası eşleşmeler sonsuz sayıda ara daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-435">This allows for a better use of indexes, because the lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="ff6e3-436">Bu, JavaScript farklı türlerde değerler işleçlerini nasıl değerlendirir alanından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-436">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="ff6e3-437">**Diziler ve nesneleri eşitlik ve karşılaştırma**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-437">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="ff6e3-438">Aralık işleçleri kullanarak dizi veya nesne değerleri karşılaştırma (>, > =, <, < =) üzerinde nesne ya da dizi değerleri tanımlanan sırasını değil olarak tanımlanmamış sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-438">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="ff6e3-439">Ancak eşitlik/eşitsizlik işleçlerini kullanma (=,! =, <>) desteklenir ve değerleri karşılaştırılabilir yapısal olarak.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-439">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="ff6e3-440">Diziler, her iki diziler aynı sayıda öğe varsa ve konumlarını eşleşen adresindeki öğeleri de eşit eşit.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-440">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="ff6e3-441">Tüm öğeleri sonuçlarında çiftinin karşılaştırma tanımlanmamış, dizi karşılaştırma sonucu tanımlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-441">If comparing any pair of elements results in undefined, the result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="ff6e3-442">Her iki nesne tanımlanan aynı özelliklere sahipse ve Özellikler eşleşen değerleri de aynıysa eşit nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-442">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="ff6e3-443">Nesne karşılaştırma sonucunu, herhangi bir özellik değerleri sonuçlarında çifti karşılaştırma tanımlanmamış, tanımlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-443">If comparing any pair of property values results in undefined, the result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="ff6e3-444"><a name="bk_constants"></a>Sabitleri</span><span class="sxs-lookup"><span data-stu-id="ff6e3-444"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="ff6e3-445">Bir sabit olarak da bilinen bir hazır değer veya bir skaler değere belirli veri değeri temsil eden bir simge ' dir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-445">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="ff6e3-446">Bir sabit biçimi temsil ettiği değer veri türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-446">The format of a constant depends on the data type of the value it represents.</span></span>  
  
 <span data-ttu-id="ff6e3-447">**Skaler veri türleri desteklenir:**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-447">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="ff6e3-448">**Tür**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-448">**Type**</span></span>|<span data-ttu-id="ff6e3-449">**Değerleri sırası**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-449">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="ff6e3-450">**Tanımlanmamış**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-450">**Undefined**</span></span>|<span data-ttu-id="ff6e3-451">Tek değer: **tanımlanmamış**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-451">Single value: **undefined**</span></span>|  
|<span data-ttu-id="ff6e3-452">**Null**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-452">**Null**</span></span>|<span data-ttu-id="ff6e3-453">Tek değer: **null**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-453">Single value: **null**</span></span>|  
|<span data-ttu-id="ff6e3-454">**Boole değeri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-454">**Boolean**</span></span>|<span data-ttu-id="ff6e3-455">Değerler: **false**, **doğru**.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-455">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="ff6e3-456">**Sayı**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-456">**Number**</span></span>|<span data-ttu-id="ff6e3-457">Çift duyarlıklı kayan noktalı sayı, standart IEEE 754.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-457">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="ff6e3-458">**Dize**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-458">**String**</span></span>|<span data-ttu-id="ff6e3-459">Sıfır veya daha fazla Unicode karakter dizisi.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-459">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="ff6e3-460">Dizeleri tek veya çift tırnak içine alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-460">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="ff6e3-461">**Dizi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-461">**Array**</span></span>|<span data-ttu-id="ff6e3-462">Sıfır veya daha fazla öğeleri dizisi.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-462">A sequence of zero or more elements.</span></span> <span data-ttu-id="ff6e3-463">Her öğe tanımlanmamış dışında herhangi bir skaler veri türü değeri olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-463">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="ff6e3-464">**Nesne**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-464">**Object**</span></span>|<span data-ttu-id="ff6e3-465">Sırasız bir sıfır veya daha fazla ad/değer çiftleri kümesi.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-465">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="ff6e3-466">Adı bir UNICODE dizesi, değeri dışında herhangi bir skaler veri türde olabilir **tanımlanmamış**.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-466">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="ff6e3-467">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-467">**Syntax**</span></span>  
  
```  
<constant> ::=  
   <undefined_constant>  
     | <null_constant>   
     | <boolean_constant>   
     | <number_constant>   
     | <string_constant>   
     | <array_constant>   
     | <object_constant>   
  
<undefined_constant> ::= undefined  
  
<null_constant> ::= null  
  
<boolean_constant> ::= false | true  
  
<number_constant> ::= decimal_literal | hexadecimal_literal  
  
<string_constant> ::= string_literal  
  
<array_constant> ::=  
    '[' [<constant>][,...n] ']'  
  
<object_constant> ::=   
   '{' [{property_name | "property_name"} : <constant>][,...n] '}'  
  
```  
  
 <span data-ttu-id="ff6e3-468">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-468">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="ff6e3-469">Türü tanımlanmamış değeri tanımsız temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-469">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="ff6e3-470">Temsil eden **null** türü değeri **Null**.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-470">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="ff6e3-471">Boolean türünde sabiti temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-471">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="ff6e3-472">Temsil eden **yanlış** türü Boolean değeri.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-472">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="ff6e3-473">Temsil eden **true** türü Boolean değeri.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-473">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="ff6e3-474">Bir sabiti temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-474">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="ff6e3-475">Ondalık değişmez değerleri ondalık sayı veya bilimsel gösterim kullanılarak temsil numaralarıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-475">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="ff6e3-476">Onaltılık değişmez değerler, önek '0 x bir veya daha fazla onaltılık basamak ile izlenen' kullanılarak temsil numaralarıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-476">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="ff6e3-477">Dize türünde bir sabiti temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-477">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="ff6e3-478">Dize değişmez değerleri, sıfır veya daha fazla Unicode karakter dizisi veya kaçış sıraları tarafından temsil edilen Unicode dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-478">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="ff6e3-479">Dize değişmez değerleri tek tırnak içine alınmış (kesme işareti: ') veya çift tırnak (tırnak işareti: ").</span><span class="sxs-lookup"><span data-stu-id="ff6e3-479">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="ff6e3-480">Aşağıdaki kaçış sıralarına izin vermesi:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-480">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="ff6e3-481">**Kaçış sırası**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-481">**Escape sequence**</span></span>|<span data-ttu-id="ff6e3-482">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-482">**Description**</span></span>|<span data-ttu-id="ff6e3-483">**Unicode karakter**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-483">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="ff6e3-484">\\'</span><span class="sxs-lookup"><span data-stu-id="ff6e3-484">\\'</span></span>|<span data-ttu-id="ff6e3-485">kesme işareti (')</span><span class="sxs-lookup"><span data-stu-id="ff6e3-485">apostrophe (')</span></span>|<span data-ttu-id="ff6e3-486">U + 0027</span><span class="sxs-lookup"><span data-stu-id="ff6e3-486">U+0027</span></span>|  
|<span data-ttu-id="ff6e3-487">\\"</span><span class="sxs-lookup"><span data-stu-id="ff6e3-487">\\"</span></span>|<span data-ttu-id="ff6e3-488">tırnak işareti (")</span><span class="sxs-lookup"><span data-stu-id="ff6e3-488">quotation mark (")</span></span>|<span data-ttu-id="ff6e3-489">U + 0022</span><span class="sxs-lookup"><span data-stu-id="ff6e3-489">U+0022</span></span>|  
|\\\|<span data-ttu-id="ff6e3-490">Ters solidus (\\)</span><span class="sxs-lookup"><span data-stu-id="ff6e3-490">reverse solidus (\\)</span></span>|<span data-ttu-id="ff6e3-491">U + 005C</span><span class="sxs-lookup"><span data-stu-id="ff6e3-491">U+005C</span></span>|  
|\\/|<span data-ttu-id="ff6e3-492">solidus (/)</span><span class="sxs-lookup"><span data-stu-id="ff6e3-492">solidus (/)</span></span>|<span data-ttu-id="ff6e3-493">U + 002F</span><span class="sxs-lookup"><span data-stu-id="ff6e3-493">U+002F</span></span>|  
|<span data-ttu-id="ff6e3-494">\b</span><span class="sxs-lookup"><span data-stu-id="ff6e3-494">\b</span></span>|<span data-ttu-id="ff6e3-495">Geri Al</span><span class="sxs-lookup"><span data-stu-id="ff6e3-495">backspace</span></span>|<span data-ttu-id="ff6e3-496">U + 0008</span><span class="sxs-lookup"><span data-stu-id="ff6e3-496">U+0008</span></span>|  
|<span data-ttu-id="ff6e3-497">\f</span><span class="sxs-lookup"><span data-stu-id="ff6e3-497">\f</span></span>|<span data-ttu-id="ff6e3-498">sonraki sayfaya geçme</span><span class="sxs-lookup"><span data-stu-id="ff6e3-498">form feed</span></span>|<span data-ttu-id="ff6e3-499">U + 000C</span><span class="sxs-lookup"><span data-stu-id="ff6e3-499">U+000C</span></span>|  
|\n|<span data-ttu-id="ff6e3-500">satır besleme</span><span class="sxs-lookup"><span data-stu-id="ff6e3-500">line feed</span></span>|<span data-ttu-id="ff6e3-501">U + 000A</span><span class="sxs-lookup"><span data-stu-id="ff6e3-501">U+000A</span></span>|  
|<span data-ttu-id="ff6e3-502">\r</span><span class="sxs-lookup"><span data-stu-id="ff6e3-502">\r</span></span>|<span data-ttu-id="ff6e3-503">satır başı</span><span class="sxs-lookup"><span data-stu-id="ff6e3-503">carriage return</span></span>|<span data-ttu-id="ff6e3-504">U + 000D</span><span class="sxs-lookup"><span data-stu-id="ff6e3-504">U+000D</span></span>|  
|<span data-ttu-id="ff6e3-505">\t</span><span class="sxs-lookup"><span data-stu-id="ff6e3-505">\t</span></span>|<span data-ttu-id="ff6e3-506">Sekmesi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-506">tab</span></span>|<span data-ttu-id="ff6e3-507">U + 0009</span><span class="sxs-lookup"><span data-stu-id="ff6e3-507">U+0009</span></span>|  
|<span data-ttu-id="ff6e3-508">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="ff6e3-508">\uXXXX</span></span>|<span data-ttu-id="ff6e3-509">4 onaltılık basamak tarafından tanımlanan bir Unicode karakter.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-509">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="ff6e3-510">U + XXXX</span><span class="sxs-lookup"><span data-stu-id="ff6e3-510">U+XXXX</span></span>|  
  
##  <span data-ttu-id="ff6e3-511"><a name="bk_query_perf_guidelines"></a>Sorgu performans kuralları</span><span class="sxs-lookup"><span data-stu-id="ff6e3-511"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="ff6e3-512">Büyük bir koleksiyon için verimli bir şekilde yürütülmek üzere bir sorgu için sırasıyla bir veya daha fazla dizinleri sunulan filtreleri kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-512">In order for a query to be executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="ff6e3-513">Aşağıdaki filtreler için dizin arama olarak kabul edilir:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-513">The following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="ff6e3-514">Eşitlik işleci (=), bir belge yol ifadesi ve bir sabit ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-514">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="ff6e3-515">Aralık işleçleri kullanın (<, \<=, >, > =) bir belge yol ifadesi ve sayı sabitleri.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-515">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="ff6e3-516">Belge yol ifadesi sabit bir yol başvurulan veritabanı koleksiyonundan belgelerdeki tanımlayan herhangi bir ifade gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-516">Document path expression stands for any expression which identifies a constant path in the documents from the referenced database collection.</span></span>  
  
 <span data-ttu-id="ff6e3-517">**Belge yol ifadesi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-517">**Document path expression**</span></span>  
  
 <span data-ttu-id="ff6e3-518">Belge yol ifadelerini ifadeleri, özelliği veya dizi dizin oluşturucu assessors veritabanı koleksiyon belgelerden gelen bir belge üzerinden yolu.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-518">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="ff6e3-519">Bu yol, doğrudan veritabanı koleksiyonundaki belgelerde bir filtrede başvurulan değerleri konumunu tanımlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-519">This path can be used to identify the location of values referenced in a filter directly within the documents in the database collection.</span></span>  
  
 <span data-ttu-id="ff6e3-520">Bir ifadenin bir belge yol ifadesi olarak kabul edilmesi bunu yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="ff6e3-520">For an expression to be considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="ff6e3-521">Koleksiyon kök doğrudan başvurun.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-521">Reference the collection root directly.</span></span>  
  
2.  <span data-ttu-id="ff6e3-522">Bazı belge yol ifadesi başvuru özelliği ya da sabiti dizi Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="ff6e3-522">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="ff6e3-523">Bazı belge yol ifadesi temsil eden bir diğer ad başvuru.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-523">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="ff6e3-524">**Sözdizimi kuralları**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-524">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="ff6e3-525">Aşağıdaki tabloda, DocumentDB API sorgu dili başvurusu sözdizimi tanımlamak için kullanılan kuralları açıklar.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-525">The following table describes the conventions used to describe syntax in the DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="ff6e3-526">**Kuralı**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-526">**Convention**</span></span>|<span data-ttu-id="ff6e3-527">**İçin kullanılır**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-527">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="ff6e3-528">BÜYÜK HARF</span><span class="sxs-lookup"><span data-stu-id="ff6e3-528">UPPERCASE</span></span>|<span data-ttu-id="ff6e3-529">Büyük küçük harf duyarlı anahtar sözcükler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-529">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="ff6e3-530">küçük harf</span><span class="sxs-lookup"><span data-stu-id="ff6e3-530">lowercase</span></span>|<span data-ttu-id="ff6e3-531">Büyük küçük harfe duyarlı anahtar sözcükler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-531">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="ff6e3-532">\<nonterminal ></span><span class="sxs-lookup"><span data-stu-id="ff6e3-532">\<nonterminal></span></span>|<span data-ttu-id="ff6e3-533">Terminal dışı, ayrı olarak tanımlı.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-533">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="ff6e3-534">\<nonterminal >:: =</span><span class="sxs-lookup"><span data-stu-id="ff6e3-534">\<nonterminal> ::=</span></span>|<span data-ttu-id="ff6e3-535">Nonterminal sözdizimi tanımı.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-535">Syntax definition of the nonterminal.</span></span>|  
    |<span data-ttu-id="ff6e3-536">other_terminal</span><span class="sxs-lookup"><span data-stu-id="ff6e3-536">other_terminal</span></span>|<span data-ttu-id="ff6e3-537">Sözcük içindeki ayrıntısı açıklanan Terminal (belirteç).</span><span class="sxs-lookup"><span data-stu-id="ff6e3-537">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="ff6e3-538">Tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="ff6e3-538">identifier</span></span>|<span data-ttu-id="ff6e3-539">Tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-539">Identifier.</span></span> <span data-ttu-id="ff6e3-540">Aşağıdaki karakterleri yalnızca sağlar: a-z A-Z 0-9 _First karakter, bir sayı olamaz.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-540">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="ff6e3-541">"dize"</span><span class="sxs-lookup"><span data-stu-id="ff6e3-541">"string"</span></span>|<span data-ttu-id="ff6e3-542">Tırnak işaretli dizesi.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-542">Quoted string.</span></span> <span data-ttu-id="ff6e3-543">Geçerli bir dize verir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-543">Allows any valid string.</span></span> <span data-ttu-id="ff6e3-544">Bir string_literal açıklamasına bakın.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-544">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="ff6e3-545">'simgesi'</span><span class="sxs-lookup"><span data-stu-id="ff6e3-545">'symbol'</span></span>|<span data-ttu-id="ff6e3-546">Sözdizimi parçası olan değişmez değer simge.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-546">Literal symbol which is part of the syntax.</span></span>|  
    |<span data-ttu-id="ff6e3-547">&#124; (dikey çubuk)</span><span class="sxs-lookup"><span data-stu-id="ff6e3-547">&#124; (vertical bar)</span></span>|<span data-ttu-id="ff6e3-548">Alternatifleri sözdizimi öğeleri için.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-548">Alternatives for syntax items.</span></span> <span data-ttu-id="ff6e3-549">Belirtilen öğeleri yalnızca birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-549">You can use only one of the items specified.</span></span>|  
    |<span data-ttu-id="ff6e3-550">[] /(brackets)</span><span class="sxs-lookup"><span data-stu-id="ff6e3-550">[ ] /(brackets)</span></span>|<span data-ttu-id="ff6e3-551">Köşeli bir veya daha fazla isteğe bağlı öğeleri kapatın.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-551">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="ff6e3-552">[,.. .n]</span><span class="sxs-lookup"><span data-stu-id="ff6e3-552">[ ,...n ]</span></span>|<span data-ttu-id="ff6e3-553">Önündeki öğeyi yinelenen n kaç kez uygulanıp uygulanamayacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-553">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="ff6e3-554">Yineleme virgülle ayrılır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-554">The occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="ff6e3-555">[.. .n]</span><span class="sxs-lookup"><span data-stu-id="ff6e3-555">[ ...n ]</span></span>|<span data-ttu-id="ff6e3-556">Önündeki öğeyi yinelenen n kaç kez uygulanıp uygulanamayacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-556">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="ff6e3-557">Yineleme boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-557">The occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="ff6e3-558"><a name="bk_built_in_functions"></a>Yerleşik işlevler</span><span class="sxs-lookup"><span data-stu-id="ff6e3-558"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="ff6e3-559">Azure Cosmos DB birçok yerleşik SQL işlevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-559">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="ff6e3-560">Yerleşik işlevler kategorilerini aşağıda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-560">The categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="ff6e3-561">İşlevi</span><span class="sxs-lookup"><span data-stu-id="ff6e3-561">Function</span></span>|<span data-ttu-id="ff6e3-562">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff6e3-562">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="ff6e3-563">Matematik işlevleri</span><span class="sxs-lookup"><span data-stu-id="ff6e3-563">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="ff6e3-564">Matematik işlevleri her genellikle, bağımsız değişken olarak sağlanır ve sayısal bir değeri döndürme giriş değerlerine göre bir hesaplama gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-564">The mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="ff6e3-565">Denetimi işlevleri yazın</span><span class="sxs-lookup"><span data-stu-id="ff6e3-565">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="ff6e3-566">Tür denetleme işlevleri SQL sorguları içinde bir ifade türünü kontrol olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-566">The type checking functions allow you to check the type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="ff6e3-567">Dize işlevleri</span><span class="sxs-lookup"><span data-stu-id="ff6e3-567">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="ff6e3-568">Dize işlevleri dizesi giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir dize, sayısal ya da Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-568">The string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="ff6e3-569">Dizi işlevleri</span><span class="sxs-lookup"><span data-stu-id="ff6e3-569">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="ff6e3-570">Dizi işlevleri bir Boole değeri veya dizi değeri, bir dizi giriş değeri ve return sayısal işlem gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-570">The array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="ff6e3-571">Uzamsal işlevleri</span><span class="sxs-lookup"><span data-stu-id="ff6e3-571">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="ff6e3-572">Uzamsal işlevleri uzamsal nesne giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir sayısal ya da Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-572">The spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="ff6e3-573"><a name="bk_mathematical_functions"></a>Matematik işlevleri</span><span class="sxs-lookup"><span data-stu-id="ff6e3-573"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="ff6e3-574">Aşağıdaki işlevleri her genellikle, bağımsız değişken olarak sağlanır ve sayısal bir değeri döndürme giriş değerlerine göre bir hesaplama gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-574">The following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="ff6e3-575">ABS</span><span class="sxs-lookup"><span data-stu-id="ff6e3-575">ABS</span></span>](#bk_abs)|[<span data-ttu-id="ff6e3-576">ACOS</span><span class="sxs-lookup"><span data-stu-id="ff6e3-576">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="ff6e3-577">ASIN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-577">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="ff6e3-578">ATAN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-578">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="ff6e3-579">ATN2</span><span class="sxs-lookup"><span data-stu-id="ff6e3-579">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="ff6e3-580">TAVAN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-580">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="ff6e3-581">COS</span><span class="sxs-lookup"><span data-stu-id="ff6e3-581">COS</span></span>](#bk_cos)|[<span data-ttu-id="ff6e3-582">COT</span><span class="sxs-lookup"><span data-stu-id="ff6e3-582">COT</span></span>](#bk_cot)|[<span data-ttu-id="ff6e3-583">DERECE</span><span class="sxs-lookup"><span data-stu-id="ff6e3-583">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="ff6e3-584">EXP</span><span class="sxs-lookup"><span data-stu-id="ff6e3-584">EXP</span></span>](#bk_exp)|[<span data-ttu-id="ff6e3-585">KAT</span><span class="sxs-lookup"><span data-stu-id="ff6e3-585">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="ff6e3-586">GÜNLÜK</span><span class="sxs-lookup"><span data-stu-id="ff6e3-586">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="ff6e3-587">LOG10</span><span class="sxs-lookup"><span data-stu-id="ff6e3-587">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="ff6e3-588">PI</span><span class="sxs-lookup"><span data-stu-id="ff6e3-588">PI</span></span>](#bk_pi)|[<span data-ttu-id="ff6e3-589">GÜÇ</span><span class="sxs-lookup"><span data-stu-id="ff6e3-589">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="ff6e3-590">RADYAN CİNSİNDEN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-590">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="ff6e3-591">YUVARLAK</span><span class="sxs-lookup"><span data-stu-id="ff6e3-591">ROUND</span></span>](#bk_round)|[<span data-ttu-id="ff6e3-592">SIN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-592">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="ff6e3-593">SQRT</span><span class="sxs-lookup"><span data-stu-id="ff6e3-593">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="ff6e3-594">KARE</span><span class="sxs-lookup"><span data-stu-id="ff6e3-594">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="ff6e3-595">OTURUM</span><span class="sxs-lookup"><span data-stu-id="ff6e3-595">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="ff6e3-596">TAN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-596">TAN</span></span>](#bk_tan)|[<span data-ttu-id="ff6e3-597">TRUNC</span><span class="sxs-lookup"><span data-stu-id="ff6e3-597">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="ff6e3-598"><a name="bk_abs"></a>ABS</span><span class="sxs-lookup"><span data-stu-id="ff6e3-598"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="ff6e3-599">Belirtilen sayısal ifade (pozitif) mutlak değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-599">Returns the absolute (positive) value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-600">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-600">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-601">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-601">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-602">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-602">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-603">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-603">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-604">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-604">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-605">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-605">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-606">Aşağıdaki örnekte, üç farklı numaralarında ABS işlevi kullanarak sonuçlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-606">The following example shows the results of using the ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="ff6e3-607">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-607">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="ff6e3-608"><a name="bk_acos"></a>ACOS</span><span class="sxs-lookup"><span data-stu-id="ff6e3-608"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="ff6e3-609">Açının kosinüsü belirtilen sayısal ifadesidir radyan cinsinden döndürür; arccosine olarak da bilinir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-609">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="ff6e3-610">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-610">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-611">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-611">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-612">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-612">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-613">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-613">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-614">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-614">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-615">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-615">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-616">Aşağıdaki örnek ACOS-1 döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-616">The following example returns the ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="ff6e3-617">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-617">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="ff6e3-618"><a name="bk_asin"></a>ASIN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-618"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="ff6e3-619">Açının sinüsü belirtilen sayısal ifadesidir radyan cinsinden döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-619">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="ff6e3-620">Bu arksinüsünü olarak da adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-620">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="ff6e3-621">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-621">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-622">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-622">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-623">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-623">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-624">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-624">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-625">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-625">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-626">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-626">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-627">Aşağıdaki örnek ASIN-1 döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-627">The following example returns the ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="ff6e3-628">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-628">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="ff6e3-629"><a name="bk_atan"></a>ATAN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-629"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="ff6e3-630">Açının tanjantı belirtilen sayısal ifadesidir radyan cinsinden döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-630">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="ff6e3-631">Bu arktanjantını olarak da adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-631">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="ff6e3-632">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-632">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-633">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-633">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-634">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-634">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-635">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-635">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-636">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-636">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-637">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-637">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-638">Aşağıdaki örnek, belirtilen değer ATAN döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-638">The following example returns the ATAN of the specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="ff6e3-639">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-639">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="ff6e3-640"><a name="bk_atn2"></a>ATN2</span><span class="sxs-lookup"><span data-stu-id="ff6e3-640"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="ff6e3-641">Radyan cinsinden ifade edilen y / x, ark tanjantını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-641">Returns the principal value of the arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="ff6e3-642">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-642">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-643">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-643">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-644">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-644">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-645">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-645">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-646">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-646">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-647">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-647">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-648">Aşağıdaki örnek için belirtilen ATN2 hesaplar x ve y bileşenleri.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-648">The following example calculates the ATN2 for the specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="ff6e3-649">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-649">Here is the result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="ff6e3-650"><a name="bk_ceiling"></a>TAVAN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-650"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="ff6e3-651">Büyüktür veya eşittir, belirtilen sayısal ifadenin en küçük tamsayı değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-651">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-652">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-652">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-653">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-653">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-654">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-654">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-655">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-655">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-656">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-656">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-657">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-657">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-658">Aşağıdaki örnek, pozitif sayısal, negatif ve TAVAN işlevi ile sıfır değerleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-658">The following example shows positive numeric, negative, and zero values with the CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="ff6e3-659">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-659">Here is the result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="ff6e3-660"><a name="bk_cos"></a>COS</span><span class="sxs-lookup"><span data-stu-id="ff6e3-660"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="ff6e3-661">Radyan cinsinden belirtilen ifade trigonometrik belirtilen açının kosinüsünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-661">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="ff6e3-662">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-662">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-663">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-663">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-664">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-664">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-665">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-665">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-666">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-666">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-667">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-667">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-668">Aşağıdaki örnek, belirtilen açının COS hesaplar.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-668">The following example calculates the COS of the specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="ff6e3-669">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-669">Here is the result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="ff6e3-670"><a name="bk_cot"></a>COT</span><span class="sxs-lookup"><span data-stu-id="ff6e3-670"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="ff6e3-671">Belirtilen açının trigonometrik kotanjantını radyan cinsinden belirtilen sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-671">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-672">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-672">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-673">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-673">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-674">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-674">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-675">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-675">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-676">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-676">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-677">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-677">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-678">Aşağıdaki örnek, belirtilen açının COT hesaplar.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-678">The following example calculates the COT of the specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="ff6e3-679">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-679">Here is the result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="ff6e3-680"><a name="bk_degrees"></a>DERECE</span><span class="sxs-lookup"><span data-stu-id="ff6e3-680"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="ff6e3-681">Radyan cinsinden Açı derece cinsinden karşılık gelen açıyı döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-681">Returns the corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="ff6e3-682">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-682">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-683">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-683">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-684">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-684">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-685">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-685">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-686">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-686">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-687">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-687">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-688">Aşağıdaki örnek, PI/2 radyan cinsinden Açı derece sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-688">The following example returns the number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="ff6e3-689">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-689">Here is the result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="ff6e3-690"><a name="bk_floor"></a>KAT</span><span class="sxs-lookup"><span data-stu-id="ff6e3-690"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="ff6e3-691">Belirtilen sayısal ifade küçük veya eşit en büyük tamsayıyı döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-691">Returns the largest integer less than or equal to the specified numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-692">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-692">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-693">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-693">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-694">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-694">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-695">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-695">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-696">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-696">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-697">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-697">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-698">Aşağıdaki örnek, pozitif sayısal, negatif ve FLOOR işlevi sıfır değerleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-698">The following example shows positive numeric, negative, and zero values with the FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="ff6e3-699">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-699">Here is the result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="ff6e3-700"><a name="bk_exp"></a>EXP</span><span class="sxs-lookup"><span data-stu-id="ff6e3-700"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="ff6e3-701">Üstel belirtilen sayısal ifadenin değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-701">Returns the exponential value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-702">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-702">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-703">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-703">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-704">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-704">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-705">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-705">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-706">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-706">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-707">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-707">**Remarks**</span></span>  
  
 <span data-ttu-id="ff6e3-708">Sabit **e** (2.718281...) Doğal logaritmanın tabanıdır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-708">The constant **e** (2.718281…), is the base of natural logarithms.</span></span>  
  
 <span data-ttu-id="ff6e3-709">Bir sayının üs. sabit olduğunda **e** sayının üssünün.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-709">The exponent of a number is the constant **e** raised to the power of the number.</span></span> <span data-ttu-id="ff6e3-710">Örneğin EXP(1.0) e = ^ 1.0 = 2.71828182845905 ve EXP(10) e = ^ 10 = 22026.4657948067.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-710">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="ff6e3-711">Bir sayının doğal logaritmasını üstel sayıdır kendisini: EXP (günlüğü (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-711">The exponential of the natural logarithm of a number is the number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="ff6e3-712">Ve üstel bir sayının doğal logaritmasını sayı kendisini: günlük (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-712">And the natural logarithm of the exponential of a number is the number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="ff6e3-713">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-713">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-714">Aşağıdaki örnek, bir değişken bildirir ve belirtilen değişkeni (10) üstel değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-714">The following example declares a variable and returns the exponential value of the specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="ff6e3-715">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-715">Here is the result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="ff6e3-716">Aşağıdaki örnek üstel değeri 20 natural logarithm ve üstel 20 doğal logaritmasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-716">The following example returns the exponential value of the natural logarithm of 20 and the natural logarithm of the exponential of 20.</span></span> <span data-ttu-id="ff6e3-717">Bu işlevler inverse işlevleri birbirinden olduğundan, dönüş değeri için her iki durumda da kayan nokta matematik yuvarlama ile 20'dir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-717">Because these functions are inverse functions of one another, the return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="ff6e3-718">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-718">Here is the result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="ff6e3-719"><a name="bk_log"></a>GÜNLÜK</span><span class="sxs-lookup"><span data-stu-id="ff6e3-719"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="ff6e3-720">Belirtilen sayısal ifade doğal logaritmasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-720">Returns the natural logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-721">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-721">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="ff6e3-722">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-722">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-723">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-723">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="ff6e3-724">Logaritmanın tabanı ayarlar isteğe bağlı sayısal değişkeni.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-724">Optional numeric argument that sets the base for the logarithm.</span></span>  
  
 <span data-ttu-id="ff6e3-725">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-725">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-726">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-726">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-727">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-727">**Remarks**</span></span>  
  
 <span data-ttu-id="ff6e3-728">Varsayılan olarak, LOG() doğal logaritmasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-728">By default, LOG() returns the natural logarithm.</span></span> <span data-ttu-id="ff6e3-729">İsteğe bağlı temel parametresini kullanarak başka bir değere logaritmanın tabanı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-729">You can change the base of the logarithm to another value by using the optional base parameter.</span></span>  
  
 <span data-ttu-id="ff6e3-730">Logaritmanın tabanı için doğal logaritmasını olan **e**, burada **e** Irrational sabiti 2.718281828 için yaklaşık eşittir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-730">The natural logarithm is the logarithm to the base **e**, where **e** is an irrational constant approximately equal to 2.718281828.</span></span>  
  
 <span data-ttu-id="ff6e3-731">Üstel bir sayının doğal logaritmasını sayıdır kendisini: günlük (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-731">The natural logarithm of the exponential of a number is the number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="ff6e3-732">Ve sayının doğal logaritmasını Üstel sayı kendisini: EXP (günlüğü (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-732">And the exponential of the natural logarithm of a number is the number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="ff6e3-733">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-733">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-734">Aşağıdaki örnek, bir değişken bildirir ve belirtilen değişkeni (10) logaritmasını değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-734">The following example declares a variable and returns the logarithm value of the specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="ff6e3-735">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-735">Here is the result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="ff6e3-736">Aşağıdaki örnek, bir sayı üs için günlük hesaplar.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-736">The following example calculates the LOG for the exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="ff6e3-737">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-737">Here is the result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="ff6e3-738"><a name="bk_log10"></a>LOG10</span><span class="sxs-lookup"><span data-stu-id="ff6e3-738"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="ff6e3-739">Belirtilen sayısal ifade 10 tabanında logaritmasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-739">Returns the base-10 logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-740">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-740">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-741">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-741">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-742">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-742">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-743">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-743">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-744">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-744">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-745">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-745">**Remarks**</span></span>  
  
 <span data-ttu-id="ff6e3-746">LOG10 ve güç işlevleri inversely birbirleriyle ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-746">The LOG10 and POWER functions are inversely related to one another.</span></span> <span data-ttu-id="ff6e3-747">Örneğin, 10 ^ LOG10(n) = n.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-747">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="ff6e3-748">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-748">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-749">Aşağıdaki örnek, bir değişken bildirir ve belirtilen değişkeni (100) LOG10 değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-749">The following example declares a variable and returns the LOG10 value of the specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="ff6e3-750">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-750">Here is the result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="ff6e3-751"><a name="bk_pi"></a>PI</span><span class="sxs-lookup"><span data-stu-id="ff6e3-751"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="ff6e3-752">PI sayısının sabit değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-752">Returns the constant value of PI.</span></span>  
  
 <span data-ttu-id="ff6e3-753">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-753">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="ff6e3-754">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-754">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-755">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-755">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-756">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-756">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-757">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-757">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-758">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-758">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-759">Aşağıdaki örnek PI değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-759">The following example returns the value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="ff6e3-760">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-760">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="ff6e3-761"><a name="bk_power"></a>GÜÇ</span><span class="sxs-lookup"><span data-stu-id="ff6e3-761"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="ff6e3-762">Belirtilen güç belirtilen ifadenin değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-762">Returns the value of the specified expression to the specified power.</span></span>  
  
 <span data-ttu-id="ff6e3-763">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-763">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="ff6e3-764">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-764">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-765">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-765">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="ff6e3-766">Hangi yükseltmek güç `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-766">Is the power to which to raise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="ff6e3-767">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-767">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-768">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-768">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-769">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-769">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-770">Aşağıdaki örnek, bir sayı (sayının küp) 3 üssüne yükseltme gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-770">The following example demonstrates raising a number to the power of 3 (the cube of the number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="ff6e3-771">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-771">Here is the result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="ff6e3-772"><a name="bk_radians"></a>RADYAN CİNSİNDEN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-772"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="ff6e3-773">Derece sayısal bir ifadenin girildiğinde radyan cinsinden döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-773">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="ff6e3-774">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-774">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-775">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-775">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-776">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-776">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-777">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-777">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-778">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-778">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-779">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-779">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-780">Aşağıdaki örnek, birkaç açıları girdi olarak alır ve bunlara karşılık gelen radian değerler döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-780">The following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="ff6e3-781">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-781">Here is the result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="ff6e3-782"><a name="bk_round"></a>YUVARLAK</span><span class="sxs-lookup"><span data-stu-id="ff6e3-782"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="ff6e3-783">En yakın tamsayı değerine yuvarlanan sayısal bir değer döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-783">Returns a numeric value, rounded to the closest integer value.</span></span>  
  
 <span data-ttu-id="ff6e3-784">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-784">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-785">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-785">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-786">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-786">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-787">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-787">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-788">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-788">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-789">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-789">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-790">Aşağıdaki örnek şu pozitif ve negatif sayıları en yakın tamsayıya yuvarlar.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-790">The following example rounds the following positive and negative numbers to the nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="ff6e3-791">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-791">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="ff6e3-792"><a name="bk_sign"></a>OTURUM</span><span class="sxs-lookup"><span data-stu-id="ff6e3-792"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="ff6e3-793">Artı (+ 1), sıfır (0) veya belirtilen sayısal ifadenin eksi (-1) işareti döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-793">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-794">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-794">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-795">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-795">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-796">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-796">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-797">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-797">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-798">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-798">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-799">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-799">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-800">Aşağıdaki örnek, 2 -2 ' sayıların oturum değerleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-800">The following example returns the SIGN values of numbers from -2 to 2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="ff6e3-801">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-801">Here is the result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="ff6e3-802"><a name="bk_sin"></a>SIN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-802"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="ff6e3-803">Radyan cinsinden belirtilen ifade trigonometrik belirtilen açının sinüsünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-803">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="ff6e3-804">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-804">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-805">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-805">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-806">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-806">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-807">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-807">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-808">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-808">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-809">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-809">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-810">Aşağıdaki örnek, belirtilen açının SIN hesaplar.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-810">The following example calculates the SIN of the specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="ff6e3-811">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-811">Here is the result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="ff6e3-812"><a name="bk_sqrt"></a>SQRT</span><span class="sxs-lookup"><span data-stu-id="ff6e3-812"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="ff6e3-813">Belirtilen sayısal değer kare kökünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-813">Returns the square root of the specified numeric value.</span></span>  
  
 <span data-ttu-id="ff6e3-814">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-814">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-815">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-815">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-816">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-816">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-817">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-817">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-818">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-818">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-819">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-819">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-820">Aşağıdaki örnek, 1-3 sayının kare kökleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-820">The following example returns the square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="ff6e3-821">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-821">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="ff6e3-822"><a name="bk_square"></a>KARE</span><span class="sxs-lookup"><span data-stu-id="ff6e3-822"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="ff6e3-823">Kare belirtilen sayısal değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-823">Returns the square of the specified numeric value.</span></span>  
  
 <span data-ttu-id="ff6e3-824">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-824">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-825">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-825">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-826">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-826">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-827">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-827">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-828">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-828">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-829">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-829">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-830">Aşağıdaki örnek numaraları 1-3 kareleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-830">The following example returns the squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="ff6e3-831">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-831">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="ff6e3-832"><a name="bk_tan"></a>TAN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-832"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="ff6e3-833">Belirtilen ifadedeki radyan cinsinden belirtilen açının tanjantını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-833">Returns the tangent of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="ff6e3-834">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-834">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-835">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-835">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-836">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-836">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-837">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-837">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-838">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-838">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-839">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-839">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-840">Aşağıdaki örnek PI () tanjantını hesaplar / 2.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-840">The following example calculates the tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="ff6e3-841">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-841">Here is the result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="ff6e3-842"><a name="bk_trunc"></a>TRUNC</span><span class="sxs-lookup"><span data-stu-id="ff6e3-842"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="ff6e3-843">En yakın tamsayı değerine kesilmiş sayısal bir değer döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-843">Returns a numeric value, truncated to the closest integer value.</span></span>  
  
 <span data-ttu-id="ff6e3-844">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-844">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="ff6e3-845">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-845">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="ff6e3-846">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-846">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-847">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-847">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-848">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-848">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-849">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-849">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-850">Aşağıdaki örnek şu pozitif ve negatif sayıları yakın tamsayı değeri tamsayıya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-850">The following example truncates the following positive and negative numbers to the nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="ff6e3-851">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-851">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="ff6e3-852"><a name="bk_type_checking_functions"></a>Denetimi işlevleri yazın</span><span class="sxs-lookup"><span data-stu-id="ff6e3-852"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="ff6e3-853">Aşağıdaki işlevleri karşı giriş değerleri denetleme türünü destekleyen ve her bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-853">The following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="ff6e3-854">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="ff6e3-854">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="ff6e3-855">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="ff6e3-855">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="ff6e3-856">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="ff6e3-856">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="ff6e3-857">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="ff6e3-857">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="ff6e3-858">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="ff6e3-858">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="ff6e3-859">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="ff6e3-859">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="ff6e3-860">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="ff6e3-860">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="ff6e3-861">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="ff6e3-861">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="ff6e3-862"><a name="bk_is_array"></a>IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="ff6e3-862"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="ff6e3-863">Belirtilen ifade türü bir dizi olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-863">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span>  
  
 <span data-ttu-id="ff6e3-864">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-864">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="ff6e3-865">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-865">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ff6e3-866">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-866">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ff6e3-867">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-867">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-868">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-868">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ff6e3-869">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-869">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-870">Aşağıdaki örnek, JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve IS_ARRAY işlevini kullanarak tanımsız türleri denetler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-870">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_ARRAY function.</span></span>  
  
```  
SELECT   
 IS_ARRAY(true),   
 IS_ARRAY(1),  
 IS_ARRAY("value"),  
 IS_ARRAY(null),  
 IS_ARRAY({prop: "value"}),   
 IS_ARRAY([1, 2, 3]),  
 IS_ARRAY({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="ff6e3-871">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-871">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="ff6e3-872"><a name="bk_is_bool"></a>IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="ff6e3-872"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="ff6e3-873">Belirtilen ifade türü bir Boole değeri olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-873">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="ff6e3-874">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-874">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="ff6e3-875">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-875">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ff6e3-876">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-876">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ff6e3-877">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-877">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-878">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-878">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ff6e3-879">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-879">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-880">Aşağıdaki örnek, JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve IS_BOOL işlevini kullanarak tanımsız türleri denetler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-880">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_BOOL function.</span></span>  
  
```  
SELECT   
    IS_BOOL(true),   
    IS_BOOL(1),  
    IS_BOOL("value"),   
    IS_BOOL(null),  
    IS_BOOL({prop: "value"}),   
    IS_BOOL([1, 2, 3]),  
    IS_BOOL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="ff6e3-881">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-881">Here is the result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="ff6e3-882"><a name="bk_is_defined"></a>IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="ff6e3-882"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="ff6e3-883">Özellik değeri atanmış olan gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-883">Returns a Boolean indicating if the property has been assigned a value.</span></span>  
  
 <span data-ttu-id="ff6e3-884">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-884">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="ff6e3-885">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-885">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ff6e3-886">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-886">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ff6e3-887">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-887">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-888">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-888">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ff6e3-889">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-889">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-890">Aşağıdaki örnek belirtilen JSON belgesi içinde bir özellik varlığını denetler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-890">The following example checks for the presence of a property within the specified JSON document.</span></span> <span data-ttu-id="ff6e3-891">İlk, "a" var, ancak "b" mevcut olduğundan ikinci false döndürür beri true değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-891">The first returns true since "a" is present, but the second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="ff6e3-892">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-892">Here is the result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="ff6e3-893"><a name="bk_is_null"></a>IS_NULL</span><span class="sxs-lookup"><span data-stu-id="ff6e3-893"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="ff6e3-894">Belirtilen ifade türü null olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-894">Returns a Boolean value indicating if the type of the specified expression is null.</span></span>  
  
 <span data-ttu-id="ff6e3-895">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-895">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="ff6e3-896">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-896">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ff6e3-897">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-897">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ff6e3-898">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-898">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-899">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-899">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ff6e3-900">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-900">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-901">Aşağıdaki örnek, JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve IS_NULL işlevini kullanarak tanımsız türleri denetler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-901">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NULL(true),   
    IS_NULL(1),  
    IS_NULL("value"),   
    IS_NULL(null),  
    IS_NULL({prop: "value"}),   
    IS_NULL([1, 2, 3]),  
    IS_NULL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="ff6e3-902">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-902">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="ff6e3-903"><a name="bk_is_number"></a>IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="ff6e3-903"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="ff6e3-904">Belirtilen ifade türü bir sayı olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-904">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span>  
  
 <span data-ttu-id="ff6e3-905">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-905">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="ff6e3-906">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-906">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ff6e3-907">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-907">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ff6e3-908">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-908">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-909">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-909">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ff6e3-910">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-910">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-911">Aşağıdaki örnek, JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve IS_NULL işlevini kullanarak tanımsız türleri denetler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-911">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NUMBER(true),   
    IS_NUMBER(1),  
    IS_NUMBER("value"),   
    IS_NUMBER(null),  
    IS_NUMBER({prop: "value"}),   
    IS_NUMBER([1, 2, 3]),  
    IS_NUMBER({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="ff6e3-912">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-912">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="ff6e3-913"><a name="bk_is_object"></a>IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="ff6e3-913"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="ff6e3-914">Belirtilen ifade türü bir JSON nesnesi olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-914">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="ff6e3-915">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-915">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="ff6e3-916">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-916">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ff6e3-917">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-917">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ff6e3-918">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-918">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-919">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-919">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ff6e3-920">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-920">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-921">Aşağıdaki örnek, JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve IS_OBJECT işlevini kullanarak tanımsız türleri denetler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-921">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_OBJECT function.</span></span>  
  
```  
SELECT   
    IS_OBJECT(true),   
    IS_OBJECT(1),  
    IS_OBJECT("value"),   
    IS_OBJECT(null),  
    IS_OBJECT({prop: "value"}),   
    IS_OBJECT([1, 2, 3]),  
    IS_OBJECT({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="ff6e3-922">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-922">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="ff6e3-923"><a name="bk_is_primitive"></a>IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="ff6e3-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="ff6e3-924">Belirtilen ifade türü bir basit tür olup olmadığını gösteren bir Boole değeri döndürür (dize, Boolean, sayısal veya null).</span><span class="sxs-lookup"><span data-stu-id="ff6e3-924">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="ff6e3-925">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-925">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="ff6e3-926">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-926">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ff6e3-927">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-927">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ff6e3-928">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-928">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-929">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-929">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ff6e3-930">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-930">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-931">Aşağıdaki örnek, JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve IS_PRIMITIVE işlevini kullanarak tanımsız türleri denetler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-931">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_PRIMITIVE function.</span></span>  
  
```  
SELECT   
           IS_PRIMITIVE(true),   
           IS_PRIMITIVE(1),  
           IS_PRIMITIVE("value"),   
           IS_PRIMITIVE(null),  
           IS_PRIMITIVE({prop: "value"}),   
           IS_PRIMITIVE([1, 2, 3]),  
           IS_PRIMITIVE({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="ff6e3-932">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-932">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="ff6e3-933"><a name="bk_is_string"></a>IS_STRING</span><span class="sxs-lookup"><span data-stu-id="ff6e3-933"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="ff6e3-934">Belirtilen ifade türü bir dize olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-934">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span>  
  
 <span data-ttu-id="ff6e3-935">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-935">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="ff6e3-936">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-936">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="ff6e3-937">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-937">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ff6e3-938">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-938">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-939">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-939">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ff6e3-940">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-940">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-941">Aşağıdaki örnek, JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve IS_STRING işlevini kullanarak tanımsız türleri denetler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-941">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_STRING function.</span></span>  
  
```  
SELECT   
       IS_STRING(true),   
       IS_STRING(1),  
       IS_STRING("value"),   
       IS_STRING(null),  
       IS_STRING({prop: "value"}),   
       IS_STRING([1, 2, 3]),  
       IS_STRING({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="ff6e3-942">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-942">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="ff6e3-943"><a name="bk_string_functions"></a>Dize işlevleri</span><span class="sxs-lookup"><span data-stu-id="ff6e3-943"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="ff6e3-944">Aşağıdaki skaler işlevler dize giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir dize, sayısal ya da Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-944">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="ff6e3-945">CONCAT</span><span class="sxs-lookup"><span data-stu-id="ff6e3-945">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="ff6e3-946">İÇERİR</span><span class="sxs-lookup"><span data-stu-id="ff6e3-946">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="ff6e3-947">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="ff6e3-947">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="ff6e3-948">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="ff6e3-948">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="ff6e3-949">SOL</span><span class="sxs-lookup"><span data-stu-id="ff6e3-949">LEFT</span></span>](#bk_left)|[<span data-ttu-id="ff6e3-950">UZUNLUĞU</span><span class="sxs-lookup"><span data-stu-id="ff6e3-950">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="ff6e3-951">DAHA DÜŞÜK</span><span class="sxs-lookup"><span data-stu-id="ff6e3-951">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="ff6e3-952">LTRIM</span><span class="sxs-lookup"><span data-stu-id="ff6e3-952">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="ff6e3-953">DEĞİŞTİR</span><span class="sxs-lookup"><span data-stu-id="ff6e3-953">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="ff6e3-954">ÇOĞALTILAN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-954">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="ff6e3-955">TERS ÇEVİR</span><span class="sxs-lookup"><span data-stu-id="ff6e3-955">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="ff6e3-956">SAĞ</span><span class="sxs-lookup"><span data-stu-id="ff6e3-956">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="ff6e3-957">RTRIM</span><span class="sxs-lookup"><span data-stu-id="ff6e3-957">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="ff6e3-958">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="ff6e3-958">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="ff6e3-959">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="ff6e3-959">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="ff6e3-960">ÜST</span><span class="sxs-lookup"><span data-stu-id="ff6e3-960">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="ff6e3-961"><a name="bk_concat"></a>CONCAT</span><span class="sxs-lookup"><span data-stu-id="ff6e3-961"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="ff6e3-962">İki veya daha fazla dize değerlerini birleştirme sonucu olan bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-962">Returns a string that is the result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="ff6e3-963">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-963">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="ff6e3-964">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-964">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-965">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-965">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-966">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-966">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-967">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-967">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-968">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-968">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-969">Aşağıdaki örnek, belirtilen değerler birleştirilmiş dizeyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-969">The following example returns the concatenated string of the specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="ff6e3-970">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-970">Here is the result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="ff6e3-971"><a name="bk_contains"></a>İÇERİR</span><span class="sxs-lookup"><span data-stu-id="ff6e3-971"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="ff6e3-972">Döndüren bir Boolean belirten ikinci ilk ifade dize olup olmadığını içerir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-972">Returns a Boolean indicating whether the first string expression contains the second.</span></span>  
  
 <span data-ttu-id="ff6e3-973">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-973">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="ff6e3-974">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-974">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-975">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-975">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-976">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-976">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-977">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-977">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ff6e3-978">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-978">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-979">Aşağıdaki örnekte, "abc" "ab" ve "d" içerir olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-979">The following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="ff6e3-980">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-980">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="ff6e3-981"><a name="bk_endswith"></a>ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="ff6e3-981"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="ff6e3-982">Döndürür Boolean belirten bir ilk ifade dize olup olmadığını ve ikinci sona erer.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-982">Returns a Boolean indicating whether the first string expression ends with the second.</span></span>  
  
 <span data-ttu-id="ff6e3-983">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-983">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="ff6e3-984">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-984">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-985">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-985">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-986">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-986">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-987">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-987">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ff6e3-988">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-988">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-989">Aşağıdaki örnekte, "abc", "b" ve "bc" ile biten döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-989">The following example returns the "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="ff6e3-990">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-990">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="ff6e3-991"><a name="bk_index_of"></a>INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="ff6e3-991"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="ff6e3-992">İkinci ilk örneğinin başlangıç konumunu döndürür dizesi ifade ilk belirtilen dize ifadesi veya -1 içinde dizesi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-992">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>  
  
 <span data-ttu-id="ff6e3-993">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-993">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="ff6e3-994">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-994">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-995">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-995">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-996">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-996">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-997">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-997">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-998">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-998">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-999">Aşağıdaki örnekte, "abc" içinde çeşitli alt dizeler dizinini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-999">The following example returns the index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="ff6e3-1000">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1000">Here is the result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="ff6e3-1001"><a name="bk_left"></a>SOL</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1001"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="ff6e3-1002">Sol bölümü belirtilen sayıda karakteri içeren bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1002">Returns the left part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="ff6e3-1003">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1003">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1004">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1004">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-1005">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1005">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="ff6e3-1006">Geçerli herhangi bir sayısal ifadeye ' dir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1006">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1007">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1007">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1008">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1008">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1009">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1009">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1010">Aşağıdaki örnekte "abc" sol bölümü için çeşitli uzunluk değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1010">The following example returns the left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="ff6e3-1011">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1011">Here is the result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="ff6e3-1012"><a name="bk_length"></a>UZUNLUĞU</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1012"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="ff6e3-1013">Belirtilen dize ifadesinin karakterlerin sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1013">Returns the number of characters of the specified string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1014">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1014">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1015">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1015">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-1016">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1016">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1017">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1017">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1018">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1018">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1019">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1019">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1020">Aşağıdaki örnek, bir dize uzunluğunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1020">The following example returns the length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="ff6e3-1021">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1021">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="ff6e3-1022"><a name="bk_lower"></a>DAHA DÜŞÜK</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1022"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="ff6e3-1023">Büyük harf karakter verileri küçük harfe dönüştürmek sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1023">Returns a string expression after converting uppercase character data to lowercase.</span></span>  
  
 <span data-ttu-id="ff6e3-1024">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1024">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1025">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1025">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-1026">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1026">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1027">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1027">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1028">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1028">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1029">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1029">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1030">Aşağıdaki örnek sorguda düşük kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1030">The following example shows how to use LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="ff6e3-1031">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1031">Here is the result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="ff6e3-1032"><a name="bk_ltrim"></a>LTRIM</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1032"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="ff6e3-1033">Öndeki boşlukları kaldırır sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1033">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="ff6e3-1034">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1034">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1035">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1035">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-1036">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1036">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1037">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1037">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1038">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1038">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1039">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1039">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1040">Aşağıdaki örnek bir sorgu içinde LTRIM kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1040">The following example shows how to use LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="ff6e3-1041">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1041">Here is the result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="ff6e3-1042"><a name="bk_replace"></a>DEĞİŞTİR</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1042"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="ff6e3-1043">Belirtilen dize değeri tüm oluşumlarını başka bir dize değeri ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1043">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="ff6e3-1044">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1044">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1045">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1045">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-1046">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1046">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1047">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1047">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1048">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1048">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1049">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1049">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1050">Aşağıdaki örnek sorguda Değiştir kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1050">The following example shows how to use REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="ff6e3-1051">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1051">Here is the result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="ff6e3-1052"><a name="bk_replicate"></a>ÇOĞALTMA</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1052"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="ff6e3-1053">Bir dize değeri, belirtilen sayıda yineler.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1053">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="ff6e3-1054">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1054">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1055">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1055">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-1056">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1056">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="ff6e3-1057">Geçerli herhangi bir sayısal ifadeye ' dir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1057">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1058">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1058">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1059">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1059">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1060">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1060">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1061">Aşağıdaki örnek sorguda REPLICATE kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1061">The following example shows how to use REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="ff6e3-1062">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1062">Here is the result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="ff6e3-1063"><a name="bk_reverse"></a>TERS ÇEVİR</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1063"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="ff6e3-1064">Ters sırada bir dize değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1064">Returns the reverse order of a string value.</span></span>  
  
 <span data-ttu-id="ff6e3-1065">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1065">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1066">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1066">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-1067">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1067">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1068">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1068">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1069">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1069">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1070">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1070">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1071">Aşağıdaki örnek sorguda ters kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1071">The following example shows how to use REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="ff6e3-1072">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1072">Here is the result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="ff6e3-1073"><a name="bk_right"></a>SAĞ</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1073"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="ff6e3-1074">Belirtilen sayıda karakteri içeren bir dize sağ bölümünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1074">Returns the right part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="ff6e3-1075">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1075">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1076">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1076">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-1077">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1077">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="ff6e3-1078">Geçerli herhangi bir sayısal ifadeye ' dir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1078">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1079">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1079">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1080">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1080">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1081">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1081">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1082">Aşağıdaki örnekte, "abc" sağ parçası için çeşitli uzunluk değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1082">The following example returns the right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="ff6e3-1083">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1083">Here is the result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="ff6e3-1084"><a name="bk_rtrim"></a>RTRIM</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1084"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="ff6e3-1085">Sondaki boşlukları kaldırır sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1085">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="ff6e3-1086">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1086">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1087">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1087">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-1088">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1088">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1089">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1089">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1090">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1090">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1091">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1091">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1092">Aşağıdaki örnek bir sorgu içinde RTRIM kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1092">The following example shows how to use RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="ff6e3-1093">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1093">Here is the result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="ff6e3-1094"><a name="bk_startswith"></a>STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1094"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="ff6e3-1095">Döndüren bir Boolean belirten ilk ifade dize olup olmadığını ve ikinci başlatır.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1095">Returns a Boolean indicating whether the first string expression starts with the second.</span></span>  
  
 <span data-ttu-id="ff6e3-1096">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1096">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1097">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1097">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-1098">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1098">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1099">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1099">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1100">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1100">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1101">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1101">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1102">Aşağıdaki örnekte "abc" dize "b" ile başlayıp başlamadığını denetler ve "a".</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1102">The following example checks if the string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="ff6e3-1103">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1103">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="ff6e3-1104"><a name="bk_substring"></a>SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1104"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="ff6e3-1105">Belirtilen karakter sıfır tabanlı konumdan başlayarak bir dize ifadesi bölümünü döndürür ve belirtilen uzunlukta veya dize sonu devam eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1105">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span>  
  
 <span data-ttu-id="ff6e3-1106">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1106">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="ff6e3-1107">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1107">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-1108">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1108">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="ff6e3-1109">Geçerli herhangi bir sayısal ifadeye ' dir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1109">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1110">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1110">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1111">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1111">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1112">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1112">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1113">Aşağıdaki örnek, 1 ve 1 karakter uzunluğu için başlangıç "abc" alt dizeyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1113">The following example returns the substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="ff6e3-1114">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1114">Here is the result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="ff6e3-1115"><a name="bk_upper"></a>ÜST</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1115"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="ff6e3-1116">Küçük harf karakter verileri büyük harfe dönüştürme sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1116">Returns a string expression after converting lowercase character data to uppercase.</span></span>  
  
 <span data-ttu-id="ff6e3-1117">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1117">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1118">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1118">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="ff6e3-1119">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1119">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1120">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1120">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1121">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1121">Returns a string expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1122">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1122">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1123">Aşağıdaki örnek sorguda üst kullanmayı gösterir</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1123">The following example shows how to use UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="ff6e3-1124">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1124">Here is the result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="ff6e3-1125"><a name="bk_array_functions"></a>Dizi işlevleri</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1125"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="ff6e3-1126">Aşağıdaki skaler işlevler bir dizi giriş değeri ve return sayısal, Boole veya dizi değer üzerinde bir işlemi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1126">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="ff6e3-1127">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1127">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="ff6e3-1128">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1128">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="ff6e3-1129">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1129">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="ff6e3-1130">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1130">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="ff6e3-1131"><a name="bk_array_concat"></a>ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="ff6e3-1132">İki veya daha fazla dizi değerlerini birleştirme sonucu olan bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1132">Returns an array that is the result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="ff6e3-1133">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1133">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="ff6e3-1134">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1134">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="ff6e3-1135">Tüm geçerli dizi ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1135">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1136">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1136">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1137">Bir dizi ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1137">Returns an array expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1138">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1138">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1139">Aşağıdaki örnek dizilerinin birleştirmek nasıl.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1139">The following example how to concatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="ff6e3-1140">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1140">Here is the result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="ff6e3-1141"><a name="bk_array_contains"></a>ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="ff6e3-1142">Dizi belirtilen değeri içerip içermediğini gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1142">Returns a Boolean indicating whether the array contains the specified value.</span></span>  
  
 <span data-ttu-id="ff6e3-1143">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1143">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="ff6e3-1144">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1144">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="ff6e3-1145">Tüm geçerli dizi ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1145">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="ff6e3-1146">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1146">Is any valid expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1147">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1147">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1148">Bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1148">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="ff6e3-1149">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1149">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1150">Aşağıdaki örnekte nasıl ARRAY_CONTAINS kullanarak bir dizi üyeliği denetlenir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1150">The following example how to check for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="ff6e3-1151">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1151">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="ff6e3-1152"><a name="bk_array_length"></a>ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="ff6e3-1153">Belirtilen dizi ifadesi öğe sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1153">Returns the number of elements of the specified array expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1154">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1154">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1155">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1155">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="ff6e3-1156">Tüm geçerli dizi ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1156">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1157">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1157">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1158">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1158">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1159">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1159">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1160">Aşağıdaki örnek ARRAY_LENGTH kullanarak bir dizi uzunluğu alma.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1160">The following example how to get the length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="ff6e3-1161">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1161">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="ff6e3-1162"><a name="bk_array_slice"></a>ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="ff6e3-1163">Bir dizi ifadesi bölümünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1163">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="ff6e3-1164">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1164">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="ff6e3-1165">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1165">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="ff6e3-1166">Tüm geçerli dizi ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1166">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="ff6e3-1167">Geçerli herhangi bir sayısal ifadeye ' dir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1167">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1168">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1168">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1169">Bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1169">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="ff6e3-1170">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1170">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1171">Aşağıdaki örnek ARRAY_SLICE kullanarak bir dizi parçası alma.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1171">The following example how to get a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="ff6e3-1172">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1172">Here is the result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="ff6e3-1173"><a name="bk_spatial_functions"></a>Uzamsal işlevleri</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1173"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="ff6e3-1174">Aşağıdaki skaler işlevler uzamsal nesne giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir sayısal ya da Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1174">The following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="ff6e3-1175">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1175">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="ff6e3-1176">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1176">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="ff6e3-1177">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1177">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="ff6e3-1178">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1178">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="ff6e3-1179">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1179">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="ff6e3-1180"><a name="bk_st_distance"></a>ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="ff6e3-1181">İki GeoJSON noktası, çokgen veya LineString ifadeleri uzaklığı döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1181">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="ff6e3-1182">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1182">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1183">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1183">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="ff6e3-1184">Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1184">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1185">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1185">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1186">Uzaklığı içeren sayısal bir ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1186">Returns a numeric expression containing the distance.</span></span> <span data-ttu-id="ff6e3-1187">Bu varsayılan başvuru sistemi metre cinsinden ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1187">This is expressed in meters for the default reference system.</span></span>  
  
 <span data-ttu-id="ff6e3-1188">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1188">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1189">Aşağıdaki örnek, içinde 30 km st_dıstance yerleşik işlevini kullanarak belirtilen konumun olan tüm ailesi belgeleri döndürülecek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1189">The following example shows how to return all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> <span data-ttu-id="ff6e3-1190">.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1190">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="ff6e3-1191">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1191">Here is the result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="ff6e3-1192"><a name="bk_st_within"></a>ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1192"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="ff6e3-1193">İlk bağımsız değişkeninde belirtilen GeoJSON nesne (noktası, çokgen veya LineString) ikinci bağımsız GeoJSON (noktası, çokgen veya LineString) içinde olup olmadığını gösteren bir Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1193">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument is within the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="ff6e3-1194">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1194">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1195">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1195">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="ff6e3-1196">Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1196">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="ff6e3-1197">Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1198">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1198">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1199">Bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1199">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="ff6e3-1200">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1200">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1201">Aşağıdaki örnek, ST_WITHIN kullanarak bir Çokgen içindeki tüm ailesi belgeleri bulmak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1201">The following example shows how to find all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="ff6e3-1202">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1202">Here is the result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="ff6e3-1203"><a name="bk_st_intersects"></a>ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="ff6e3-1204">İlk bağımsız değişkeninde belirtilen GeoJSON nesne (noktası, çokgen veya LineString) ikinci bağımsız GeoJSON (noktası, çokgen veya LineString) kesiştiğinden olup olmadığını gösteren bir Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1204">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument intersects the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="ff6e3-1205">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1205">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1206">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1206">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="ff6e3-1207">Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1207">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="ff6e3-1208">Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1209">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1209">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1210">Bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1210">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="ff6e3-1211">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1211">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1212">Aşağıdaki örnek ile belirtilen Çokgen kesiştiğinden tüm alanlar bulmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1212">The following example shows how to find all areas that intersects with the given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="ff6e3-1213">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1213">Here is the result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="ff6e3-1214"><a name="bk_st_isvalid"></a>ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="ff6e3-1215">Belirtilen GeoJSON noktası, çokgen veya LineString ifade geçerli olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1215">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="ff6e3-1216">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1216">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1217">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1217">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="ff6e3-1218">Tüm geçerli GeoJSON noktası, çokgen veya LineString ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1218">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1219">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1219">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1220">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1220">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1221">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1221">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1222">Aşağıdaki örnek, bir nokta ST_VALID kullanarak geçerli olup olmadığını denetlemek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1222">The following example shows how to check if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="ff6e3-1223">Örneğin, bu nokta değerleri [-90, 90], geçerli aralıkta şekilde sorgu döndürür false değil bir enlem değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1223">For example, this point has a latitude value that's not in the valid range of values [-90, 90], so the query returns false.</span></span>  
  
 <span data-ttu-id="ff6e3-1224">Çokgenler için sağlanan son koordinat çifti kapalı bir şekil oluşturmak için ilk olarak, aynı olmalıdır GeoJSON belirtilmesini gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1224">For polygons, the GeoJSON specification requires that the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span> <span data-ttu-id="ff6e3-1225">Çokgen içindeki noktaları yönünün sırayla belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1225">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="ff6e3-1226">Belirtilen saat yönünde sırayla Çokgen bölge içindeki tersini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1226">A polygon specified in clockwise order represents the inverse of the region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="ff6e3-1227">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1227">Here is the result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="ff6e3-1228"><a name="bk_st_isvaliddetailed"></a>ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="ff6e3-1229">Belirtilen GeoJSON noktası, çokgen veya LineString ifade geçerli olup olmadığını ve geçersiz bir Boole değeri içeren bir JSON değeri değeri döndürür, ayrıca bir dize değeri olarak nedeni.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1229">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="ff6e3-1230">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1230">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="ff6e3-1231">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1231">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="ff6e3-1232">Tüm geçerli GeoJSON noktası veya Çokgen ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1232">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="ff6e3-1233">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1233">**Return Types**</span></span>  
  
 <span data-ttu-id="ff6e3-1234">Belirtilen GeoJSON noktası veya Çokgen ifade geçerli olup olmadığını ve geçersiz bir Boole değeri içeren bir JSON değeri değeri döndürür, ayrıca bir dize değeri olarak nedeni.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1234">Returns a JSON value containing a Boolean value if the specified GeoJSON point or polygon expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="ff6e3-1235">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1235">**Examples**</span></span>  
  
 <span data-ttu-id="ff6e3-1236">Aşağıdaki örnekte nasıl ST_ISVALIDDETAILED kullanarak geçerlilik (ayrıntılarla gibi) denetlenir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1236">The following example how to check validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="ff6e3-1237">Sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1237">Here is the result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a polygon must have the same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="ff6e3-1238">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1238">Next steps</span></span>  
 <span data-ttu-id="ff6e3-1239">[SQL söz dizimi ve Azure Cosmos DB SQL sorgusu](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="ff6e3-1239">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="ff6e3-1240">Azure Cosmos DB belgeleri</span><span class="sxs-lookup"><span data-stu-id="ff6e3-1240">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
