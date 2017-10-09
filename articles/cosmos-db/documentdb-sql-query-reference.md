---
<span data-ttu-id="3db21-101">Başlık: aaa "Azure Cosmos DB DocumentDB API'si: SQL söz dizimi | Microsoft Docs"Açıklama: başvuru belgelerini hello Azure Cosmos DB DocumentDB API SQL sorgu dili için.</span><span class="sxs-lookup"><span data-stu-id="3db21-101">title: aaa"Azure Cosmos DB DocumentDB API: SQL syntax | Microsoft Docs" description: Reference documentation for hello Azure Cosmos DB DocumentDB API SQL query language.</span></span>
<span data-ttu-id="3db21-102">Hizmetleri: cosmos db Yazar: mimig1 Yöneticisi: jhubbard Düzenleyicisi: mimig documentationcenter: ''</span><span class="sxs-lookup"><span data-stu-id="3db21-102">services: cosmos-db author: mimig1 manager: jhubbard editor: mimig documentationcenter: ''</span></span>

<span data-ttu-id="3db21-103">MS.assetid: ms.service: cosmos db ms.workload: Veri Hizmetleri ms.tgt_pltfrm: na ms.devlang: na ms.topic: ms.date başvuru: 13/06/2017 ms.author: mimig</span><span class="sxs-lookup"><span data-stu-id="3db21-103">ms.assetid: ms.service: cosmos-db ms.workload: data-services ms.tgt_pltfrm: na ms.devlang: na ms.topic: reference ms.date: 06/13/2017 ms.author: mimig</span></span>

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="3db21-104">Azure DB Cosmos DocumentDB API: SQL söz dizimi başvurusu</span><span class="sxs-lookup"><span data-stu-id="3db21-104">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="3db21-105">Hello Azure Cosmos DB DocumentDB API tanıdık SQL (yapılandırılmış sorgu dili) kullanarak belgelerin sorgulanmasını dilbilgisi gibi hiyerarşik JSON belgelerini gerektirmeden açık şema veya ikincil dizinlerin oluşturulmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="3db21-105">hello Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="3db21-106">Bu konu, başvuru belgeleri hello DocumentDB API SQL sorgu dili için sağlar.</span><span class="sxs-lookup"><span data-stu-id="3db21-106">This topic provides reference documentation for hello DocumentDB API SQL query language.</span></span>

<span data-ttu-id="3db21-107">Merhaba DocumentDB API SQL sorgu dili bir anlatım için bkz: [SQL sorgularını Azure Cosmos DB DocumentDB API için](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="3db21-107">For a walkthrough of hello DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="3db21-108">Ayrıca toovisit hello davet ediyoruz [Query Playground](http://www.documentdb.com/sql/demo) burada Azure Cosmos DB deneyin ve SQL sorgularını kümemize karşı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3db21-108">We also invite you toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="3db21-109">SEÇME sorgusu</span><span class="sxs-lookup"><span data-stu-id="3db21-109">SELECT query</span></span>  
<span data-ttu-id="3db21-110">JSON belgeleri hello veritabanından alır.</span><span class="sxs-lookup"><span data-stu-id="3db21-110">Retrieves JSON documents from hello database.</span></span> <span data-ttu-id="3db21-111">İfade değerlendirme, filtreleme tahminleri destekler ve birleştirir.</span><span class="sxs-lookup"><span data-stu-id="3db21-111">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="3db21-112">Merhaba SELECT deyimi tanımlamak için kullanılan hello kuralları hello sözdizimi kuralları bölümünde tabloda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-112">hello conventions used for describing hello SELECT statements are tabulated in hello Syntax conventions section.</span></span>  
  
<span data-ttu-id="3db21-113">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-113">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="3db21-114">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="3db21-114">**Remarks**</span></span>  
  
 <span data-ttu-id="3db21-115">Ayrıntılar için bölümlere her yan tümcesi aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="3db21-115">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="3db21-116">SELECT yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="3db21-116">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="3db21-117">FROM yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="3db21-117">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="3db21-118">WHERE yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="3db21-118">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="3db21-119">ORDER BY yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="3db21-119">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="3db21-120">Merhaba yan tümceleri hello SELECT deyimi içinde yukarıda gösterildiği gibi sıralanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3db21-120">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="3db21-121">Merhaba isteğe bağlı yan tümceleri herhangi biri atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="3db21-121">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="3db21-122">Ancak isteğe bağlı bir yan tümceleri kullanıldığında, hello doğru sırada görünmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3db21-122">But when optional clauses are used, they must appear in hello right order.</span></span>  
  
<span data-ttu-id="3db21-123">**Merhaba SELECT deyimi mantıksal işleme sırası**</span><span class="sxs-lookup"><span data-stu-id="3db21-123">**Logical Processing Order of hello SELECT statement**</span></span>  
  
<span data-ttu-id="3db21-124">yan tümceleri işlenme hello sırası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="3db21-124">hello order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="3db21-125">FROM yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="3db21-125">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="3db21-126">WHERE yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="3db21-126">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="3db21-127">ORDER BY yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="3db21-127">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="3db21-128">SELECT yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="3db21-128">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="3db21-129">Bu hello sözdiziminde görüntüleneceği hello sipariş farklı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3db21-129">Note that this is different from hello order in which they appear in hello syntax.</span></span> <span data-ttu-id="3db21-130">işlenen yan tümcesi ile sunulan tüm yeni sembolleri görünür ve daha sonra işlenen yan tümcelerinde kullanılabilir gibi hello sıralama olmamasıdır.</span><span class="sxs-lookup"><span data-stu-id="3db21-130">hello ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="3db21-131">Örneğin, bir FROM yan tümcesinde bildirilen diğer adlar WHERE erişilebilir ve SELECT yan tümceleri.</span><span class="sxs-lookup"><span data-stu-id="3db21-131">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="3db21-132">**Boşluk karakterleri ve açıklamaları**</span><span class="sxs-lookup"><span data-stu-id="3db21-132">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="3db21-133">Tırnak içine alınan bir dizeyi bir parçası olmayan veya tanımlayıcı tırnak içine alınmış tüm boşluk karakterleri hello dil dilbilgisi parçası olmayan ve ayrıştırma sırasında yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="3db21-133">All white space characters which are not part of a quoted string or quoted identifier are not part of hello language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="3db21-134">T-SQL stili yorumlar gibi Hello sorgu dili destekler</span><span class="sxs-lookup"><span data-stu-id="3db21-134">hello query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="3db21-135">SQL deyimi`-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="3db21-135">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="3db21-136">Boşluk karakterleri ve açıklamalar herhangi anlamlı hello dilbilgisi değil olmakla birlikte, kullanılan tooseparate belirteçleri olmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="3db21-136">While whitespace characters and comments do not have any significance in hello grammar, they must be used tooseparate tokens.</span></span> <span data-ttu-id="3db21-137">Örneğin: `-1e5` bir tek sayı belirteç süre olan`: – 1 e5` eksi bir belirteç numarası 1 ve tanımlayıcı e5 tarafından izlenir.</span><span class="sxs-lookup"><span data-stu-id="3db21-137">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="3db21-138"><a name="bk_select_query"></a>SELECT yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="3db21-138"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="3db21-139">Merhaba yan tümceleri hello SELECT deyimi içinde yukarıda gösterildiği gibi sıralanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3db21-139">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="3db21-140">Merhaba isteğe bağlı yan tümceleri herhangi biri atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="3db21-140">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="3db21-141">Ancak isteğe bağlı bir yan tümceleri kullanıldığında, hello doğru sırada görünmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3db21-141">But when optional clauses are used, they must appear in hello right order.</span></span>  

<span data-ttu-id="3db21-142">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-142">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="3db21-143">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-143">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="3db21-144">Merhaba sonuç için seçilen özellikler veya değer toobe ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3db21-144">Properties or value toobe selected for hello result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="3db21-145">Merhaba değeri hiçbir değişiklik yapmadan alınması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3db21-145">Specifies that hello value should be retrieved without making any changes.</span></span> <span data-ttu-id="3db21-146">İşlenen hello değer bir nesne ise, özellikle, tüm özellikler alınır.</span><span class="sxs-lookup"><span data-stu-id="3db21-146">Specifically if hello processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="3db21-147">Alınan özellikleri toobe Hello listesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3db21-147">Specifies hello list of properties toobe retrieved.</span></span> <span data-ttu-id="3db21-148">Her döndürülen değeri, belirtilen hello özellikleri olan bir nesne olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3db21-148">Each returned value will be an object with hello properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="3db21-149">Merhaba JSON değeri hello tam JSON nesne yerine alınması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3db21-149">Specifies that hello JSON value should be retrieved instead of hello complete JSON object.</span></span> <span data-ttu-id="3db21-150">Bu, aksine `<property_list>` öngörülen hello değer bir nesne içinde kaymasını değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-150">This, unlike `<property_list>` does not wrap hello projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="3db21-151">Merhaba değeri toobe temsil eden ifadesi hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="3db21-151">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="3db21-152">Bkz: [skaler ifadelerin](#bk_scalar_expressions) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="3db21-152">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="3db21-153">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="3db21-153">**Remarks**</span></span>  
  
<span data-ttu-id="3db21-154">Merhaba `SELECT *` sözdizimi geçerli yalnızca tam olarak bir diğer ad belirtmiş FROM yan tümcesi varsa.</span><span class="sxs-lookup"><span data-stu-id="3db21-154">hello `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="3db21-155">`SELECT *`projeksiyon gerektiğinde yararlı olabilecek bir kimlik projeksiyon sağlar.</span><span class="sxs-lookup"><span data-stu-id="3db21-155">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="3db21-156">SEÇİN * yalnızca FROM yan tümcesi belirtilirse geçerlidir ve yalnızca tek bir giriş kaynağı sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="3db21-156">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="3db21-157">Unutmayın `SELECT <select_list>` ve `SELECT *` "söz dizimi sugar" olduğunu ve bunun yerine aşağıda gösterildiği gibi basit SELECT deyimi kullanılarak belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="3db21-157">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="3db21-158">eşdeğerdir:</span><span class="sxs-lookup"><span data-stu-id="3db21-158">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="3db21-159">eşdeğerdir:</span><span class="sxs-lookup"><span data-stu-id="3db21-159">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="3db21-160">**Ayrıca bkz.**</span><span class="sxs-lookup"><span data-stu-id="3db21-160">**See Also**</span></span>  
  
[<span data-ttu-id="3db21-161">Skaler ifade</span><span class="sxs-lookup"><span data-stu-id="3db21-161">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="3db21-162">SELECT yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="3db21-162">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="3db21-163"><a name="bk_from_clause"></a>FROM yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="3db21-163"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="3db21-164">Merhaba kaynak veya birleştirilmiş kaynakları belirtir.</span><span class="sxs-lookup"><span data-stu-id="3db21-164">Specifies hello source or joined sources.</span></span> <span data-ttu-id="3db21-165">Merhaba FROM yan tümcesi isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="3db21-165">hello FROM clause is optional.</span></span> <span data-ttu-id="3db21-166">Aksi durumda belirtilen, diğer yan tümceleri hala FROM yan tümcesi tek bir belgenin sağladıysanız olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="3db21-166">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="3db21-167">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-167">**Syntax**</span></span>  
  
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
  
<span data-ttu-id="3db21-168">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-168">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="3db21-169">Bir veri kaynağı olan veya olmayan bir diğer ad belirtir.</span><span class="sxs-lookup"><span data-stu-id="3db21-169">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="3db21-170">Diğer ad belirtilmezse, onu hello olayla `<collection_expression>` kuralları kullanarak:</span><span class="sxs-lookup"><span data-stu-id="3db21-170">If alias is not specified, it will be inferred from hello `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="3db21-171">Merhaba deyim bir toplama_adı ise toplama_adı bir diğer ad olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3db21-171">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="3db21-172">Merhaba ifade ise `<collection_expression>`, property_name sonra property_name bir diğer ad olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3db21-172">If hello expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="3db21-173">Merhaba deyim bir toplama_adı ise toplama_adı bir diğer ad olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3db21-173">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="3db21-174">OLARAK`input_alias`</span><span class="sxs-lookup"><span data-stu-id="3db21-174">AS `input_alias`</span></span>  
  
<span data-ttu-id="3db21-175">Bu hello belirtir `input_alias` Toplama ifadesi temel hello tarafından döndürülen değerler kümesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-175">Specifies that hello `input_alias` is a set of values returned by hello underlying collection expression.</span></span>  
 
<span data-ttu-id="3db21-176">`input_alias`IN</span><span class="sxs-lookup"><span data-stu-id="3db21-176">`input_alias` IN</span></span>  
  
<span data-ttu-id="3db21-177">Bu hello belirtir `input_alias` Toplama ifadesi temel hello tarafından döndürülen her dizinin tüm dizi öğeleri üzerinde yineleme tarafından elde edilen değerleri hello kümesini temsil etmelidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-177">Specifies that hello `input_alias` should represent hello set of values obtained by iterating over all array elements of each array returned by hello underlying collection expression.</span></span> <span data-ttu-id="3db21-178">Dizi olmayan temel Toplama ifadesi tarafından döndürülen herhangi bir değer yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="3db21-178">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="3db21-179">Merhaba Toplama ifadesi toobe kullanılan tooretrieve hello belgeler belirtir.</span><span class="sxs-lookup"><span data-stu-id="3db21-179">Specifies hello collection expression toobe used tooretrieve hello documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="3db21-180">Bu belge hello varsayılan, bağlı durumda koleksiyonu alınması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3db21-180">Specifies that document should be retrieved from hello default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="3db21-181">Bu belgede sağlanan hello koleksiyonundan alınması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3db21-181">Specifies that document should be retrieved from hello provided collection.</span></span> <span data-ttu-id="3db21-182">Merhaba koleksiyonunun Hello adı şu anda bağlı hello koleksiyonunun hello adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-182">hello name of hello collection must match hello name of hello collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="3db21-183">Bu belge hello alınan belirtir sağlanan hello diğer adı tarafından tanımlanan diğer kaynak.</span><span class="sxs-lookup"><span data-stu-id="3db21-183">Specifies that document should be retrieved from hello other source defined by hello provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="3db21-184">Bu belge hello erişerek alınabilir belirtir `property_name` özelliği veya dizi_dizini dizi öğesi tarafından alınan tüm belgeler için belirtilen toplama ifadesi.</span><span class="sxs-lookup"><span data-stu-id="3db21-184">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="3db21-185">Bu belge hello erişerek alınabilir belirtir `property_name` özelliği veya dizi_dizini dizi öğesi tarafından alınan tüm belgeler için belirtilen toplama ifadesi.</span><span class="sxs-lookup"><span data-stu-id="3db21-185">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="3db21-186">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="3db21-186">**Remarks**</span></span>  
  
<span data-ttu-id="3db21-187">Tüm diğer adlar sağlanan veya hello çıkarımı yapılan `<from_source>(`s) benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3db21-187">All aliases provided or inferred in hello `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="3db21-188">Merhaba sözdizimi `<collection_expression>.`property_name aynı hello olduğu `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="3db21-188">hello Syntax `<collection_expression>.`property_name is hello same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="3db21-189">Ancak, bir özellik adı tanımlayıcısı dışı karakterler içeriyorsa hello ikinci sözdizimi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3db21-189">However, hello latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="3db21-190">**Dizi öğeleri eksik özellikleri eksik değerleri işleme tanımlanmamış**</span><span class="sxs-lookup"><span data-stu-id="3db21-190">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="3db21-191">Bir toplama ifadesi özellikleri veya dizi öğeleri ve değer yok erişirse, bu değeri göz ardı ve daha fazla işlenmedi.</span><span class="sxs-lookup"><span data-stu-id="3db21-191">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="3db21-192">**Toplama ifadesi içerik kapsamı**</span><span class="sxs-lookup"><span data-stu-id="3db21-192">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="3db21-193">Bir toplama ifadesi koleksiyonu kapsamlı veya belge kapsamlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="3db21-193">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="3db21-194">Koleksiyon kapsamlı bir ifade, hello hello toplama ifadesinin temel alınan kaynak ya da kök ise veya `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="3db21-194">An expression is collection-scoped, if hello underlying source of hello collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="3db21-195">Bu tür bir ifade hello koleksiyonundan doğrudan alınan belgeleri kümesini temsil eder ve diğer toplama ifadeleri hello işlenmesini bağımlı değildir.</span><span class="sxs-lookup"><span data-stu-id="3db21-195">Such an expression represents a set of documents retrieved from hello collection directly, and is not dependent on hello processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="3db21-196">Belge kapsamlı bir ifade, hello hello toplama ifadesinin temel alınan kaynak `input_alias` önceki hello sorguda sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="3db21-196">An expression is document-scoped, if hello underlying source of hello collection expression is `input_alias` introduced earlier in hello query.</span></span> <span data-ttu-id="3db21-197">Bu tür bir ifade hello diğer koleksiyonuyla ilişkilendirilen toohello kümesi ait her bir belgenin hello kapsamında hello toplama ifadesinin hesaplanmasıyla elde belgeleri kümesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-197">Such an expression represents a set of documents obtained by evaluating hello collection expression in hello scope of each document belonging toohello set associated with hello aliased collection.</span></span>  <span data-ttu-id="3db21-198">Merhaba sonuç kümesi her kümesi temel hello hello belgelerde hello toplama ifadesinin hesaplanmasıyla elde edilen kümeleri birleşim olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3db21-198">hello resulting set will be a union of sets obtained by evaluating hello collection expression for each of hello documents in hello underlying set.</span></span>  
  
<span data-ttu-id="3db21-199">**Birleşimler**</span><span class="sxs-lookup"><span data-stu-id="3db21-199">**Joins**</span></span>  
  
<span data-ttu-id="3db21-200">Merhaba geçerli sürümde, Azure Cosmos DB iç birleştirmeler destekler.</span><span class="sxs-lookup"><span data-stu-id="3db21-200">In hello current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="3db21-201">Ek birleştirme özellikleri yeni çıkacak.</span><span class="sxs-lookup"><span data-stu-id="3db21-201">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="3db21-202">İç birleşimler sonuçlanır eksiksiz bir çapraz ürün hello hello birleştirme katılan ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3db21-202">Inner joins result in a complete cross product of hello sets participating in hello join.</span></span> <span data-ttu-id="3db21-203">Merhaba bir N yönlü birleştirme burada hello tanımlama grubu içindeki her değerin katılan hello birleştirme ayarlamak hello diğer adı ile ilişkili ve söz konusu diğer ad diğer yan tümcelerinde başvurarak erişilen N-öğe başlık kümesi sonucudur.</span><span class="sxs-lookup"><span data-stu-id="3db21-203">hello result of an N-way join is a set of N-element tuples, where each value in hello tuple is associated with hello aliased set participating in hello join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="3db21-204">Merhaba değerlendirme hello birleştirme hello bağlam kapsamına kümeleri katılan hello bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="3db21-204">hello evaluation of hello join depends on hello context scope of hello participating sets:</span></span>  
  
-  <span data-ttu-id="3db21-205">Bir birleştirme arasında koleksiyon kümesi A ve koleksiyon kapsamlı B, A ve b kümelerindeki tüm öğelerin çapraz ürün sonuçları ayarlayın</span><span class="sxs-lookup"><span data-stu-id="3db21-205">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="3db21-206">Tüm ayarlar her belge için B A. belge kapsamlı ayarlama değerlendirerek elde birleşimi sonuçlanıyor kümesi belge kapsamlı kümesi B arasındaki bir birleştirme</span><span class="sxs-lookup"><span data-stu-id="3db21-206">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="3db21-207">Merhaba geçerli sürümde, en fazla bir koleksiyon kapsamlı ifade hello Sorgu işlemcisi tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3db21-207">In hello current release, a maximum of one collection-scoped expression is supported by hello query processor.</span></span>  
  
<span data-ttu-id="3db21-208">**Birleştirme örnekleri:**</span><span class="sxs-lookup"><span data-stu-id="3db21-208">**Examples of joins:**</span></span>  
  
<span data-ttu-id="3db21-209">FROM yan tümcesi aşağıdaki hello bakalım:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="3db21-209">Let's look at hello following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="3db21-210">Tanımlamak her kaynak izin `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="3db21-210">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="3db21-211">Bu FROM yan tümcesi N-diziler (tuple N değerlerle) kümesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-211">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="3db21-212">Her tanımlama grubu tüm koleksiyon diğer adları kendi ilgili ayarlar yineleme tarafından üretilen değerler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="3db21-212">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="3db21-213">*Örnek 1, 2 kaynaklarıyla KATIL:*</span><span class="sxs-lookup"><span data-stu-id="3db21-213">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="3db21-214">Let `<from_source1>` koleksiyonu kapsamlı ve kümesi {A, B, C} temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-214">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="3db21-215">Let `<from_source2>` input_alias1 başvuran belge kapsamlı ve ayarlar temsil eder:</span><span class="sxs-lookup"><span data-stu-id="3db21-215">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="3db21-216">{1, 2} için`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="3db21-216">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="3db21-217">için {3}`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="3db21-217">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="3db21-218">{4, 5} için`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="3db21-218">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="3db21-219">Merhaba FROM yan tümcesi `<from_source1> JOIN <from_source2>` diziler aşağıdaki hello neden olur:</span><span class="sxs-lookup"><span data-stu-id="3db21-219">hello FROM clause `<from_source1> JOIN <from_source2>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="3db21-220">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="3db21-220">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="3db21-221">*Örnek 2, 3 kaynaklarıyla KATIL:*</span><span class="sxs-lookup"><span data-stu-id="3db21-221">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="3db21-222">Let `<from_source1>` koleksiyonu kapsamlı ve kümesi {A, B, C} temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-222">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="3db21-223">Let `<from_source2>` belge kapsamlı başvuran olması `input_alias1` ve ayarlar temsil eder:</span><span class="sxs-lookup"><span data-stu-id="3db21-223">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="3db21-224">{1, 2} için`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="3db21-224">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="3db21-225">için {3}`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="3db21-225">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="3db21-226">{4, 5} için`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="3db21-226">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="3db21-227">Let `<from_source3>` belge kapsamlı başvuran olması `input_alias2` ve ayarlar temsil eder:</span><span class="sxs-lookup"><span data-stu-id="3db21-227">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="3db21-228">{100, 200} için`input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="3db21-228">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="3db21-229">{300} için`input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="3db21-229">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="3db21-230">Merhaba FROM yan tümcesi `<from_source1> JOIN <from_source2> JOIN <from_source3>` diziler aşağıdaki hello neden olur:</span><span class="sxs-lookup"><span data-stu-id="3db21-230">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="3db21-231">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="3db21-231">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="3db21-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="3db21-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="3db21-233">Diğer değerler için diziler eksikliği `input_alias1`, `input_alias2`, hangi hello için `<from_source3>` hiçbir değer döndürmedi.</span><span class="sxs-lookup"><span data-stu-id="3db21-233">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which hello `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="3db21-234">*Örnek 3, 3 kaynaklarıyla KATIL:*</span><span class="sxs-lookup"><span data-stu-id="3db21-234">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="3db21-235">< Koleksiyon kapsamlı ve {A, B, C} kümesini temsil eden from_source1 > olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="3db21-235">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="3db21-236">Let `<from_source1>` koleksiyonu kapsamlı ve kümesi {A, B, C} temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-236">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="3db21-237">< Belge kapsamlı başvuru input_alias1 olması ve ayarlar temsil from_source2 > sağlar:</span><span class="sxs-lookup"><span data-stu-id="3db21-237">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="3db21-238">{1, 2} için`input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="3db21-238">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="3db21-239">için {3}`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="3db21-239">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="3db21-240">{4, 5} için`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="3db21-240">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="3db21-241">Let `<from_source3>` kapsamlı çok`input_alias1` ve ayarlar temsil eder:</span><span class="sxs-lookup"><span data-stu-id="3db21-241">Let `<from_source3>` be scoped too`input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="3db21-242">{100, 200} için`input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="3db21-242">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="3db21-243">{300} için`input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="3db21-243">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="3db21-244">Merhaba FROM yan tümcesi `<from_source1> JOIN <from_source2> JOIN <from_source3>` diziler aşağıdaki hello neden olur:</span><span class="sxs-lookup"><span data-stu-id="3db21-244">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="3db21-245">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="3db21-245">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="3db21-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), (C, 4, 300) (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="3db21-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="3db21-247">Bu arasında çapraz ürün ile sonuçlandı `<from_source2>` ve `<from_source3>` her ikisi de kapsamlı toohello olduğundan aynı `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="3db21-247">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped toohello same `<from_source1>`.</span></span>  <span data-ttu-id="3db21-248">Bu 4 (2 x 2) sonuçlandı diziler değerini 0 diziler B (1 x 0) değeri sahip olması ve 2 (2 x 1) değeri C. diziler</span><span class="sxs-lookup"><span data-stu-id="3db21-248">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="3db21-249">**Ayrıca bkz.**</span><span class="sxs-lookup"><span data-stu-id="3db21-249">**See also**</span></span>  
  
 [<span data-ttu-id="3db21-250">SELECT yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="3db21-250">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="3db21-251"><a name="bk_where_clause"></a>WHERE yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="3db21-251"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="3db21-252">Merhaba sorgu tarafından döndürülen hello belgeler için Hello arama koşulu belirtir.</span><span class="sxs-lookup"><span data-stu-id="3db21-252">Specifies hello search condition for hello documents returned by hello query.</span></span>  
  
 <span data-ttu-id="3db21-253">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-253">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="3db21-254">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-254">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="3db21-255">Döndürülen hello belgeleri toobe için karşılanıp hello koşulu toobe belirtir.</span><span class="sxs-lookup"><span data-stu-id="3db21-255">Specifies hello condition toobe met for hello documents toobe returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="3db21-256">Merhaba değeri toobe temsil eden ifadesi hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="3db21-256">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="3db21-257">Merhaba bkz [skaler ifadelerin](#bk_scalar_expressions) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="3db21-257">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="3db21-258">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="3db21-258">**Remarks**</span></span>  
  
 <span data-ttu-id="3db21-259">Merhaba sırayla filtre koşulu tootrue değerlendirilmelidir olarak belirtilen bir ifade belge toobe döndürdü.</span><span class="sxs-lookup"><span data-stu-id="3db21-259">In order for hello document toobe returned an expression specified as filter condition must evaluate tootrue.</span></span> <span data-ttu-id="3db21-260">Boole değeri true hello koşul, başka bir değer yerine getirecek yalnızca: tanımlanmamış, null, false, sayı, dizi veya nesne uygun olmadığı hello koşulu.</span><span class="sxs-lookup"><span data-stu-id="3db21-260">Only Boolean value true will satisfy hello condition, any other value: undefined, null, false, Number, Array or Object will not satisfy hello condition.</span></span>  
  
##  <span data-ttu-id="3db21-261"><a name="bk_orderby_clause"></a>ORDER BY yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="3db21-261"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="3db21-262">Merhaba sorgu tarafından döndürülen sonuçları için sıralama hello belirtir.</span><span class="sxs-lookup"><span data-stu-id="3db21-262">Specifies hello sorting order for results returned by hello query.</span></span>  
  
 <span data-ttu-id="3db21-263">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-263">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="3db21-264">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-264">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="3db21-265">Bir özellik veya üzerinde toosort hello sorgu sonuç kümesini ifade belirtir.</span><span class="sxs-lookup"><span data-stu-id="3db21-265">Specifies a property or expression on which toosort hello query result set.</span></span> <span data-ttu-id="3db21-266">Sıralama sütunu adı veya sütun diğer adı belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="3db21-266">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="3db21-267">Birden çok sütunları sıralama belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="3db21-267">Multiple sort columns can be specified.</span></span> <span data-ttu-id="3db21-268">Sütun adları benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3db21-268">Column names must be unique.</span></span> <span data-ttu-id="3db21-269">Merhaba hello ORDER BY yan tümcesinde sütunları sıralama Hello sırasını hello kuruluş sıralanmış hello sonuç kümesinin tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3db21-269">hello sequence of hello sort columns in hello ORDER BY clause defines hello organization of hello sorted result set.</span></span> <span data-ttu-id="3db21-270">Diğer bir deyişle, hello sonuç kümesi hello ilk özelliği tarafından sıralanır ve o sıralı liste hello ikinci özelliği ve benzeri sonra sıralanır.</span><span class="sxs-lookup"><span data-stu-id="3db21-270">That is, hello result set is sorted by hello first property and then that ordered list is sorted by hello second property, and so on.</span></span>  
  
     <span data-ttu-id="3db21-271">Merhaba ORDER BY yan tümcesinde başvurulan hello sütun adları hello bir sütunda herhangi belirsizlikleri olmadan hello FROM yan tümcesinde belirtilen bir tabloda tanımlanan liste veya tooa sütun seçin tooeither karşılık gelmelidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-271">hello column names referenced in hello ORDER BY clause must correspond tooeither a column in hello select list or tooa column defined in a table specified in hello FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="3db21-272">Hangi toosort hello sorgu sonuç kümesinde tek bir özellik veya ifadeyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="3db21-272">Specifies a single property or expression on which toosort hello query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="3db21-273">Merhaba bkz [skaler ifadelerin](#bk_scalar_expressions) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="3db21-273">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="3db21-274">Merhaba Belirtilen sütundaki Hello değerleri artan veya azalan sırada sıralanması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3db21-274">Specifies that hello values in hello specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="3db21-275">ASC hello en düşük değer toohighest değerinden sıralar.</span><span class="sxs-lookup"><span data-stu-id="3db21-275">ASC sorts from hello lowest value toohighest value.</span></span> <span data-ttu-id="3db21-276">DESC en yüksek değer toolowest değerinden sıralar.</span><span class="sxs-lookup"><span data-stu-id="3db21-276">DESC sorts from highest value toolowest value.</span></span> <span data-ttu-id="3db21-277">ASC hello varsayılan sıralama düzeni ' dir.</span><span class="sxs-lookup"><span data-stu-id="3db21-277">ASC is hello default sort order.</span></span> <span data-ttu-id="3db21-278">Null değerler hello düşük olası değerler kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="3db21-278">Null values are treated as hello lowest possible values.</span></span>  
  
 <span data-ttu-id="3db21-279">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="3db21-279">**Remarks**</span></span>  
  
 <span data-ttu-id="3db21-280">Merhaba sorgu dilbilgisi özellikleri tarafından birden çok sipariş desteklerken, yalnızca tek bir özellik, yalnızca adlarla ve özellik adları, yani, hesaplanan özellikleri karşı sıralama hello Azure Cosmos DB sorgu çalışma zamanı destekler.</span><span class="sxs-lookup"><span data-stu-id="3db21-280">While hello query grammar supports multiple order by properties, hello Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="3db21-281">Sıralama de gerektirir dizin oluşturma ilkesi o hello içerir hello özelliği ve belirtilen hello için bir aralığı dizin türüyle hello en yüksek duyarlık.</span><span class="sxs-lookup"><span data-stu-id="3db21-281">Sorting also requires that hello indexing policy includes a range index for hello property and hello specified type, with hello maximum precision.</span></span> <span data-ttu-id="3db21-282">Dizin oluşturma ilkesi belgeleri daha fazla ayrıntı için toohello bakın.</span><span class="sxs-lookup"><span data-stu-id="3db21-282">Refer toohello indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="3db21-283"><a name="bk_scalar_expressions"></a>Skaler ifade</span><span class="sxs-lookup"><span data-stu-id="3db21-283"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="3db21-284">Skaler bir ifade simge birleşiminden oluşur ve tooobtain tek bir değer olabilir işleçleri değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="3db21-284">A scalar expression is a combination of symbols and operators that can be evaluated tooobtain a single value.</span></span> <span data-ttu-id="3db21-285">Basit ifadeler sabitler, özellik başvuruları, dizi öğesi başvuruları, diğer başvurular veya işlev çağrılarını olabilir.</span><span class="sxs-lookup"><span data-stu-id="3db21-285">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="3db21-286">Basit ifadeler işleçleri kullanarak karmaşık ifadelere birleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="3db21-286">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="3db21-287">Hangi skaler ifade olabilir değerleri hakkında daha fazla bilgi için bkz: [sabitleri](#bk_constants) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3db21-287">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="3db21-288">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-288">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="3db21-289">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-289">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="3db21-290">Sabit bir değeri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-290">Represents a constant value.</span></span> <span data-ttu-id="3db21-291">Bkz: [sabitleri](#bk_constants) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="3db21-291">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="3db21-292">Merhaba tarafından tanımlanan bir değeri temsil `input_alias` hello sunulan `FROM` yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="3db21-292">Represents a value defined by hello `input_alias` introduced in hello `FROM` clause.</span></span>  
    <span data-ttu-id="3db21-293">Bu değer toonot garanti olması **tanımsız** –**tanımsız** hello giriş değerleri atlanır.</span><span class="sxs-lookup"><span data-stu-id="3db21-293">This value is guaranteed toonot be **undefined** –**undefined** values in hello input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="3db21-294">Bir nesnenin hello özelliğinin değerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-294">Represents a value of hello property of an object.</span></span> <span data-ttu-id="3db21-295">Merhaba özelliği mevcut değil veya özellik bir nesne olmayan bir değer başvurulan durumunda hello ifadeyi hesaplar çok**tanımsız** değeri.</span><span class="sxs-lookup"><span data-stu-id="3db21-295">If hello property does not exist or property is referenced on a value which is not an object, then hello expression evaluates too**undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="3db21-296">Adında hello özellik değerini temsil eder `property_name` veya dizi öğesi dizine sahip `array_index` nesne/dizisi.</span><span class="sxs-lookup"><span data-stu-id="3db21-296">Represents a value of hello property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="3db21-297">Merhaba özelliği/dizi dizini yok veya hello özelliği/dizi dizini bir nesne/dizisi olmayan bir değer başvuruluyor, hello ifadeyi tooundefined değeri hesaplar.</span><span class="sxs-lookup"><span data-stu-id="3db21-297">If hello property/array index does not exist or hello property/array index is referenced on a value which is not an object/array, then hello expression evaluates tooundefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="3db21-298">Tek değere uygulanan tooa olan işleç bir temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-298">Represents an operator that is applied tooa single value.</span></span> <span data-ttu-id="3db21-299">Bkz: [işleçleri](#bk_operators) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="3db21-299">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="3db21-300">Uygulanan tootwo değerleri bir işleç temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-300">Represents an operator that is applied tootwo values.</span></span> <span data-ttu-id="3db21-301">Bkz: [işleçleri](#bk_operators) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="3db21-301">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="3db21-302">İşlev çağrısının sonucunu tarafından tanımlanan bir değeri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-302">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="3db21-303">Merhaba kullanıcının adını skaler işlev tanımlı.</span><span class="sxs-lookup"><span data-stu-id="3db21-303">Name of hello user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="3db21-304">Merhaba yerleşik skaler işlev adı.</span><span class="sxs-lookup"><span data-stu-id="3db21-304">Name of hello built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="3db21-305">Belirtilen özelliklere sahip yeni bir nesne oluşturarak alınan bir değer ve bunların değerleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-305">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="3db21-306">Öğeleri olarak belirtilen değerlerle yeni bir dizi oluşturarak elde bir değeri temsil eder</span><span class="sxs-lookup"><span data-stu-id="3db21-306">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="3db21-307">Merhaba belirtilen parametre adı değerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-307">Represents a value of hello specified parameter name.</span></span> <span data-ttu-id="3db21-308">Parametre adları @ tek bir hello ilk karakteri olarak olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3db21-308">Parameter names must have a single @ as hello first character.</span></span>  
  
 <span data-ttu-id="3db21-309">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="3db21-309">**Remarks**</span></span>  
  
 <span data-ttu-id="3db21-310">Bir yerleşik veya kullanıcı çağırma skaler işlev tanımlandığında tüm bağımsız değişkenler tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3db21-310">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="3db21-311">Hello bağımsız değişkenlerden biri tanımsız hello işlev çağrılmaz ve hello sonucu tanımsız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3db21-311">If any of hello arguments is undefined, hello function will not be called and hello result will be undefined.</span></span>  
  
 <span data-ttu-id="3db21-312">Bir nesne oluştururken, Tanımsız değer atanmış herhangi bir özelliği atlandı ve nesne oluşturulan hello dahil değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-312">When creating an object, any property that is assigned undefined value will be skipped and not included in hello created object.</span></span>  
  
 <span data-ttu-id="3db21-313">Ne zaman herhangi bir öğeyi değer bir dizi oluşturma atanmış **tanımsız** değeri atlandı ve oluşturulan hello nesnesinde dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="3db21-313">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in hello created object.</span></span> <span data-ttu-id="3db21-314">Bu sonraki tanımlanan hello öğesi tootake onun yerine neden olacak şekilde, oluşturulan hello dizi dizinleri atlandı değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-314">This will cause hello next defined element tootake its place in such a way that hello created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="3db21-315"><a name="bk_operators"></a>İşleçler</span><span class="sxs-lookup"><span data-stu-id="3db21-315"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="3db21-316">Bu bölümde desteklenen hello işleçleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3db21-316">This section describes hello supported operators.</span></span> <span data-ttu-id="3db21-317">Her işleç atanan tooexactly bir kategori olabilir.</span><span class="sxs-lookup"><span data-stu-id="3db21-317">Each operator can be assigned tooexactly one category.</span></span>  
  
 <span data-ttu-id="3db21-318">Bkz: **işleci kategorileri** Ayrıntılar için aşağıdaki tabloya işlenmesi ile ilgili **tanımsız** değerleri, giriş değerleri ve işleme türlerini eşleşmeyen ile değerlerin türü gereksinimleri.</span><span class="sxs-lookup"><span data-stu-id="3db21-318">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="3db21-319">**İşleç kategoriler:**</span><span class="sxs-lookup"><span data-stu-id="3db21-319">**Operator categories:**</span></span>  
  
|<span data-ttu-id="3db21-320">**Kategori**</span><span class="sxs-lookup"><span data-stu-id="3db21-320">**Category**</span></span>|<span data-ttu-id="3db21-321">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="3db21-321">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="3db21-322">**aritmetik**</span><span class="sxs-lookup"><span data-stu-id="3db21-322">**arithmetic**</span></span>|<span data-ttu-id="3db21-323">İşleç bekliyor input(s) toobe numaraları.</span><span class="sxs-lookup"><span data-stu-id="3db21-323">Operator expects input(s) toobe Number(s).</span></span> <span data-ttu-id="3db21-324">Çıktı ayrıca bir sayıdır.</span><span class="sxs-lookup"><span data-stu-id="3db21-324">Output is also a Number.</span></span> <span data-ttu-id="3db21-325">Merhaba girdi ise **tanımsız** veya numarası sonra hello sonuç dışında türüdür **tanımsız**.</span><span class="sxs-lookup"><span data-stu-id="3db21-325">If any of hello inputs is **undefined** or type other than Number then hello result is **undefined**.</span></span>|  
|<span data-ttu-id="3db21-326">**bit tabanlı**</span><span class="sxs-lookup"><span data-stu-id="3db21-326">**bitwise**</span></span>|<span data-ttu-id="3db21-327">İşleç bekliyor input(s) toobe 32-bit işaretli tamsayıyı numaraları.</span><span class="sxs-lookup"><span data-stu-id="3db21-327">Operator expects input(s) toobe 32-bit signed integer Number(s).</span></span> <span data-ttu-id="3db21-328">Çıktı da 32 bit imzalı numarası tamsayıdır.</span><span class="sxs-lookup"><span data-stu-id="3db21-328">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="3db21-329">Herhangi bir tamsayı olmayan değer yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="3db21-329">Any non-integer value will be rounded.</span></span> <span data-ttu-id="3db21-330">Pozitif bir değer yuvarlanacağı, negatif değerleri yuvarlanan.</span><span class="sxs-lookup"><span data-stu-id="3db21-330">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="3db21-331">Merhaba 32 bit tamsayı aralığın dışında herhangi bir değer, son 32 bitlik, iki kişinin tamamlama gösterimi gerçekleştirerek dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="3db21-331">Any value that is outside of hello 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="3db21-332">Merhaba girdi ise **tanımsız** hello sonuç ise diğer, sayıdan yazın veya **tanımsız**.</span><span class="sxs-lookup"><span data-stu-id="3db21-332">If any of hello inputs is **undefined** or type other than Number, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="3db21-333">**Not:** hello davranışı üzerinde JavaScript bit düzeyinde işleci davranışı ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="3db21-333">**Note:** hello above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="3db21-334">**mantıksal**</span><span class="sxs-lookup"><span data-stu-id="3db21-334">**logical**</span></span>|<span data-ttu-id="3db21-335">İşleç bekliyor input(s) toobe Boolean(s).</span><span class="sxs-lookup"><span data-stu-id="3db21-335">Operator expects input(s) toobe Boolean(s).</span></span> <span data-ttu-id="3db21-336">Çıktı de bir Boole değeri olur.</span><span class="sxs-lookup"><span data-stu-id="3db21-336">Output is also a Boolean.</span></span><br /><span data-ttu-id="3db21-337">Merhaba girdi ise **tanımsız** hello sonucu olacaktır sonra Boolean, diğerinden yazın veya **tanımsız**.</span><span class="sxs-lookup"><span data-stu-id="3db21-337">If any of hello inputs is **undefined** or type other than Boolean, then hello result will be **undefined**.</span></span>|  
|<span data-ttu-id="3db21-338">**Karşılaştırma**</span><span class="sxs-lookup"><span data-stu-id="3db21-338">**comparison**</span></span>|<span data-ttu-id="3db21-339">İşleç bekliyor input(s) aynı yazın ve tanımsız olmaması toohave hello.</span><span class="sxs-lookup"><span data-stu-id="3db21-339">Operator expects input(s) toohave hello same type and not be undefined.</span></span> <span data-ttu-id="3db21-340">Çıktı bir Boole değeri değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-340">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="3db21-341">Merhaba girdi ise **tanımsız** veya hello girişleri farklı türlerine sahip ardından hello sonuç **tanımsız**.</span><span class="sxs-lookup"><span data-stu-id="3db21-341">If any of hello inputs is **undefined** or hello inputs have different types, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="3db21-342">Bkz: **karşılaştırma için değerlerin sıralama** ayrıntıları sıralama değeri için tablo.</span><span class="sxs-lookup"><span data-stu-id="3db21-342">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="3db21-343">**dize**</span><span class="sxs-lookup"><span data-stu-id="3db21-343">**string**</span></span>|<span data-ttu-id="3db21-344">İşleç bekliyor input(s) toobe dizelerini.</span><span class="sxs-lookup"><span data-stu-id="3db21-344">Operator expects input(s) toobe String(s).</span></span> <span data-ttu-id="3db21-345">Çıktı ayrıca bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-345">Output is also a String.</span></span><br /><span data-ttu-id="3db21-346">Merhaba girdi ise **tanımsız** veya dize sonra hello sonuç dışında türüdür **tanımsız**.</span><span class="sxs-lookup"><span data-stu-id="3db21-346">If any of hello inputs is **undefined** or type other than String then hello result is **undefined**.</span></span>|  
  
 <span data-ttu-id="3db21-347">**Birli işleçleri:**</span><span class="sxs-lookup"><span data-stu-id="3db21-347">**Unary operators:**</span></span>  
  
|<span data-ttu-id="3db21-348">**Ad**</span><span class="sxs-lookup"><span data-stu-id="3db21-348">**Name**</span></span>|<span data-ttu-id="3db21-349">**İşleci**</span><span class="sxs-lookup"><span data-stu-id="3db21-349">**Operator**</span></span>|<span data-ttu-id="3db21-350">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="3db21-350">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="3db21-351">**aritmetik**</span><span class="sxs-lookup"><span data-stu-id="3db21-351">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="3db21-352">Merhaba sayı değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-352">Returns hello number value.</span></span><br /><br /> <span data-ttu-id="3db21-353">Bit tabanlı değil işlecini.</span><span class="sxs-lookup"><span data-stu-id="3db21-353">Bitwise negation.</span></span> <span data-ttu-id="3db21-354">Sayı değeri tasarruflarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-354">Returns negated number value.</span></span>|  
|<span data-ttu-id="3db21-355">**bit tabanlı**</span><span class="sxs-lookup"><span data-stu-id="3db21-355">**bitwise**</span></span>|~|<span data-ttu-id="3db21-356">Olanları tamamlama.</span><span class="sxs-lookup"><span data-stu-id="3db21-356">Ones' complement.</span></span> <span data-ttu-id="3db21-357">Tamamlama sayı değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-357">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="3db21-358">**Mantıksal**</span><span class="sxs-lookup"><span data-stu-id="3db21-358">**Logical**</span></span>|<span data-ttu-id="3db21-359">**DEĞİL**</span><span class="sxs-lookup"><span data-stu-id="3db21-359">**NOT**</span></span>|<span data-ttu-id="3db21-360">Değilleme.</span><span class="sxs-lookup"><span data-stu-id="3db21-360">Negation.</span></span> <span data-ttu-id="3db21-361">Boole değeri döndürür tasarruflarını.</span><span class="sxs-lookup"><span data-stu-id="3db21-361">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="3db21-362">**İkili işleçler:**</span><span class="sxs-lookup"><span data-stu-id="3db21-362">**Binary operators:**</span></span>  
  
|<span data-ttu-id="3db21-363">**Ad**</span><span class="sxs-lookup"><span data-stu-id="3db21-363">**Name**</span></span>|<span data-ttu-id="3db21-364">**İşleci**</span><span class="sxs-lookup"><span data-stu-id="3db21-364">**Operator**</span></span>|<span data-ttu-id="3db21-365">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="3db21-365">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="3db21-366">**aritmetik**</span><span class="sxs-lookup"><span data-stu-id="3db21-366">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="3db21-367">Ayrıca.</span><span class="sxs-lookup"><span data-stu-id="3db21-367">Addition.</span></span><br /><br /> <span data-ttu-id="3db21-368">Çıkarma.</span><span class="sxs-lookup"><span data-stu-id="3db21-368">Subtraction.</span></span><br /><br /> <span data-ttu-id="3db21-369">Çarpma.</span><span class="sxs-lookup"><span data-stu-id="3db21-369">Multiplication.</span></span><br /><br /> <span data-ttu-id="3db21-370">Bölme.</span><span class="sxs-lookup"><span data-stu-id="3db21-370">Division.</span></span><br /><br /> <span data-ttu-id="3db21-371">Modülasyon.</span><span class="sxs-lookup"><span data-stu-id="3db21-371">Modulation.</span></span>|  
|<span data-ttu-id="3db21-372">**bit tabanlı**</span><span class="sxs-lookup"><span data-stu-id="3db21-372">**bitwise**</span></span>|<span data-ttu-id="3db21-373">&#124;</span><span class="sxs-lookup"><span data-stu-id="3db21-373">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="3db21-374">Bit düzeyinde OR.</span><span class="sxs-lookup"><span data-stu-id="3db21-374">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="3db21-375">Bit düzeyinde and</span><span class="sxs-lookup"><span data-stu-id="3db21-375">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="3db21-376">Bit düzeyinde XOR.</span><span class="sxs-lookup"><span data-stu-id="3db21-376">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="3db21-377">Sola kaydırma.</span><span class="sxs-lookup"><span data-stu-id="3db21-377">Left Shift.</span></span><br /><br /> <span data-ttu-id="3db21-378">Sağa kaydırma.</span><span class="sxs-lookup"><span data-stu-id="3db21-378">Right Shift.</span></span><br /><br /> <span data-ttu-id="3db21-379">Sıfır dolgu sağa kaydırma.</span><span class="sxs-lookup"><span data-stu-id="3db21-379">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="3db21-380">**mantıksal**</span><span class="sxs-lookup"><span data-stu-id="3db21-380">**logical**</span></span>|<span data-ttu-id="3db21-381">**VE**</span><span class="sxs-lookup"><span data-stu-id="3db21-381">**AND**</span></span><br /><br /> <span data-ttu-id="3db21-382">**VEYA**</span><span class="sxs-lookup"><span data-stu-id="3db21-382">**OR**</span></span>|<span data-ttu-id="3db21-383">Mantıksal ve işlecini.</span><span class="sxs-lookup"><span data-stu-id="3db21-383">Logical conjunction.</span></span> <span data-ttu-id="3db21-384">Döndürür **true** iki bağımsız değişkenler ise **true**, döndürür **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="3db21-384">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="3db21-385">Mantıksal ve işlecini.</span><span class="sxs-lookup"><span data-stu-id="3db21-385">Logical conjunction.</span></span> <span data-ttu-id="3db21-386">Döndürür **true** iki bağımsız değişkenler ise **true**, döndürür **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="3db21-386">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="3db21-387">**Karşılaştırma**</span><span class="sxs-lookup"><span data-stu-id="3db21-387">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="3db21-388">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="3db21-388">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="3db21-389">**??**</span><span class="sxs-lookup"><span data-stu-id="3db21-389">**??**</span></span>|<span data-ttu-id="3db21-390">Eşittir.</span><span class="sxs-lookup"><span data-stu-id="3db21-390">Equals.</span></span> <span data-ttu-id="3db21-391">Döndürür **true** bağımsız değişkenleri eşit olup olmadığını döndürür **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="3db21-391">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="3db21-392">Eşit değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-392">Not equal to.</span></span> <span data-ttu-id="3db21-393">Döndürür **true** bağımsız değişkenleri eşit değilse döndürür **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="3db21-393">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="3db21-394">Büyüktür.</span><span class="sxs-lookup"><span data-stu-id="3db21-394">Greater Than.</span></span> <span data-ttu-id="3db21-395">Döndürür **true** ilk bağımsız değişken ikinci bir hello büyükse, dönüş **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="3db21-395">Returns **true** if first argument is greater than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="3db21-396">Büyüktür veya eşittir.</span><span class="sxs-lookup"><span data-stu-id="3db21-396">Greater Than or Equal To.</span></span> <span data-ttu-id="3db21-397">Döndürür **true** ilk bağımsız değişken ikinci toohello eşit veya değerinden daha büyük olursa döndürür **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="3db21-397">Returns **true** if first argument is greater than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="3db21-398">Küçüktür.</span><span class="sxs-lookup"><span data-stu-id="3db21-398">Less Than.</span></span> <span data-ttu-id="3db21-399">Döndürür **true** ilk bağımsız değişken ikinci bir hello daha az ise, döndürür **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="3db21-399">Returns **true** if first argument is less than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="3db21-400">Küçük veya eşittir.</span><span class="sxs-lookup"><span data-stu-id="3db21-400">Less Than or Equal To.</span></span> <span data-ttu-id="3db21-401">Döndürür **true** ilk bağımsız değişken küçük veya buna eşit olması durumunda toohello ikinci bir dönüş **false** Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="3db21-401">Returns **true** if first argument is less than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="3db21-402">Birleşim.</span><span class="sxs-lookup"><span data-stu-id="3db21-402">Coalesce.</span></span> <span data-ttu-id="3db21-403">Merhaba ilk bağımsız değişkeni ise döndürür hello ikinci bağımsız değişkeni bir **tanımsız** değeri.</span><span class="sxs-lookup"><span data-stu-id="3db21-403">Returns hello second argument if hello first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="3db21-404">**Dize**</span><span class="sxs-lookup"><span data-stu-id="3db21-404">**String**</span></span>|<span data-ttu-id="3db21-405">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="3db21-405">**&#124;&#124;**</span></span>|<span data-ttu-id="3db21-406">Birleştirme.</span><span class="sxs-lookup"><span data-stu-id="3db21-406">Concatenation.</span></span> <span data-ttu-id="3db21-407">Her iki değişken birleşimini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-407">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="3db21-408">**Üçlü işleçler:**</span><span class="sxs-lookup"><span data-stu-id="3db21-408">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="3db21-409">Üçlü işleci</span><span class="sxs-lookup"><span data-stu-id="3db21-409">Ternary operator</span></span>|<span data-ttu-id="3db21-410">?</span><span class="sxs-lookup"><span data-stu-id="3db21-410">?</span></span>|<span data-ttu-id="3db21-411">Merhaba ilk bağımsız değişkeni çok değerlendirilirse döndürür hello ikinci bağımsız değişken**true**; hello üçüncü bağımsız değişken yoksa döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-411">Returns hello second argument if hello first argument evaluates too**true**; return hello third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="3db21-412">**Karşılaştırma için değerlerin sıralama**</span><span class="sxs-lookup"><span data-stu-id="3db21-412">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="3db21-413">**Tür**</span><span class="sxs-lookup"><span data-stu-id="3db21-413">**Type**</span></span>|<span data-ttu-id="3db21-414">**Değerleri sırası**</span><span class="sxs-lookup"><span data-stu-id="3db21-414">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="3db21-415">**Tanımlanmamış**</span><span class="sxs-lookup"><span data-stu-id="3db21-415">**Undefined**</span></span>|<span data-ttu-id="3db21-416">Karşılaştırılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-416">Not comparable.</span></span>|  
|<span data-ttu-id="3db21-417">**Null**</span><span class="sxs-lookup"><span data-stu-id="3db21-417">**Null**</span></span>|<span data-ttu-id="3db21-418">Tek değer: **null**</span><span class="sxs-lookup"><span data-stu-id="3db21-418">Single value: **null**</span></span>|  
|<span data-ttu-id="3db21-419">**Sayı**</span><span class="sxs-lookup"><span data-stu-id="3db21-419">**Number**</span></span>|<span data-ttu-id="3db21-420">Doğal bir gerçek sayı.</span><span class="sxs-lookup"><span data-stu-id="3db21-420">Natural real number.</span></span><br /><br /> <span data-ttu-id="3db21-421">Negatif sonsuz değerle diğer sayı değeri küçüktür.</span><span class="sxs-lookup"><span data-stu-id="3db21-421">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="3db21-422">Pozitif sonsuz değerle diğer numara değerden daha büyük. **NaN** değeri karşılaştırılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-422">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="3db21-423">İle karşılaştırma **NaN** sonuçlanır **tanımsız** değeri.</span><span class="sxs-lookup"><span data-stu-id="3db21-423">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="3db21-424">**Dize**</span><span class="sxs-lookup"><span data-stu-id="3db21-424">**String**</span></span>|<span data-ttu-id="3db21-425">Lexicographical sırası.</span><span class="sxs-lookup"><span data-stu-id="3db21-425">Lexicographical order.</span></span>|  
|<span data-ttu-id="3db21-426">**Dizi**</span><span class="sxs-lookup"><span data-stu-id="3db21-426">**Array**</span></span>|<span data-ttu-id="3db21-427">Yoktur, ancak Tarafsız sıralaması.</span><span class="sxs-lookup"><span data-stu-id="3db21-427">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="3db21-428">**Nesne**</span><span class="sxs-lookup"><span data-stu-id="3db21-428">**Object**</span></span>|<span data-ttu-id="3db21-429">Yoktur, ancak Tarafsız sıralaması.</span><span class="sxs-lookup"><span data-stu-id="3db21-429">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="3db21-430">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="3db21-430">**Remarks**</span></span>  
  
 <span data-ttu-id="3db21-431">Gerçekte hello veritabanından alınan kadar Azure Cosmos DB'de değerlerin hello türleri bilinen genellikle değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-431">In Azure Cosmos DB, hello types of values are often not known until they are actually retrieved from hello database.</span></span> <span data-ttu-id="3db21-432">Sipariş toosupport verimli yürütme sorgularının, hello işleçleri çoğunu sıkı tür gereksinimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="3db21-432">In order toosupport efficient execution of queries, most of hello operators have strict type requirements.</span></span> <span data-ttu-id="3db21-433">Ayrıca kendilerini işleçleriyle örtük dönüşümler gerçekleştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="3db21-433">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="3db21-434">Bu sorguda ister anlamına gelir: seçin * gelen kök r WHERE r.Age = 21 yalnızca özelliği geçerlilik süresi eşit toohello sayı 21 belgelerle döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-434">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal toohello number 21.</span></span> <span data-ttu-id="3db21-435">Belgeleri özelliği geçerlilik süresi eşit toohello "21" veya hello dize "0021" ile eşleşmez, "21" Merhaba ifade olarak = 21 tooundefined değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="3db21-435">Documents with property Age equal toohello string "21" or hello string "0021" will not match, as hello expression "21" = 21 evaluates tooundefined.</span></span> <span data-ttu-id="3db21-436">Bu dizinleri, daha iyi kullanımı için çünkü sağlar hello arama belirli bir değerin (yani 21 sayı) (yani numarası 21 veya dizeler "21", "021", "21.0"...) olası eşleşmeler sonsuz sayıda ara daha hızlıdır.</span><span class="sxs-lookup"><span data-stu-id="3db21-436">This allows for a better use of indexes, because hello lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="3db21-437">Bu, JavaScript farklı türlerde değerler işleçlerini nasıl değerlendirir alanından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="3db21-437">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="3db21-438">**Diziler ve nesneleri eşitlik ve karşılaştırma**</span><span class="sxs-lookup"><span data-stu-id="3db21-438">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="3db21-439">Aralık işleçleri kullanarak dizi veya nesne değerleri karşılaştırma (>, > =, <, < =) üzerinde nesne ya da dizi değerleri tanımlanan sırasını değil olarak tanımlanmamış sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="3db21-439">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="3db21-440">Ancak eşitlik/eşitsizlik işleçlerini kullanma (=,! =, <>) desteklenir ve değerleri karşılaştırılabilir yapısal olarak.</span><span class="sxs-lookup"><span data-stu-id="3db21-440">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="3db21-441">Diziler, her iki diziler aynı sayıda öğe varsa ve konumlarını eşleşen adresindeki öğeleri de eşit eşit.</span><span class="sxs-lookup"><span data-stu-id="3db21-441">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="3db21-442">Öğe çiftleri karşılaştırma dizi karşılaştırma tanımlanmamış, hello sonucunda sonuçlanırsa tanımlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="3db21-442">If comparing any pair of elements results in undefined, hello result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="3db21-443">Her iki nesne tanımlanan aynı özelliklere sahipse ve Özellikler eşleşen değerleri de aynıysa eşit nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="3db21-443">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="3db21-444">Özellik değerlerinin herhangi bir çifti karşılaştırma nesne karşılaştırma tanımlanmamış, hello sonucunda sonuçlanırsa tanımlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="3db21-444">If comparing any pair of property values results in undefined, hello result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="3db21-445"><a name="bk_constants"></a>Sabitleri</span><span class="sxs-lookup"><span data-stu-id="3db21-445"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="3db21-446">Bir sabit olarak da bilinen bir hazır değer veya bir skaler değere belirli veri değeri temsil eden bir simge ' dir.</span><span class="sxs-lookup"><span data-stu-id="3db21-446">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="3db21-447">bir sabit Hello biçimi temsil ettiği hello değerinin veri türüne hello bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="3db21-447">hello format of a constant depends on hello data type of hello value it represents.</span></span>  
  
 <span data-ttu-id="3db21-448">**Skaler veri türleri desteklenir:**</span><span class="sxs-lookup"><span data-stu-id="3db21-448">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="3db21-449">**Tür**</span><span class="sxs-lookup"><span data-stu-id="3db21-449">**Type**</span></span>|<span data-ttu-id="3db21-450">**Değerleri sırası**</span><span class="sxs-lookup"><span data-stu-id="3db21-450">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="3db21-451">**Tanımlanmamış**</span><span class="sxs-lookup"><span data-stu-id="3db21-451">**Undefined**</span></span>|<span data-ttu-id="3db21-452">Tek değer: **tanımlanmamış**</span><span class="sxs-lookup"><span data-stu-id="3db21-452">Single value: **undefined**</span></span>|  
|<span data-ttu-id="3db21-453">**Null**</span><span class="sxs-lookup"><span data-stu-id="3db21-453">**Null**</span></span>|<span data-ttu-id="3db21-454">Tek değer: **null**</span><span class="sxs-lookup"><span data-stu-id="3db21-454">Single value: **null**</span></span>|  
|<span data-ttu-id="3db21-455">**Boole değeri**</span><span class="sxs-lookup"><span data-stu-id="3db21-455">**Boolean**</span></span>|<span data-ttu-id="3db21-456">Değerler: **false**, **doğru**.</span><span class="sxs-lookup"><span data-stu-id="3db21-456">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="3db21-457">**Sayı**</span><span class="sxs-lookup"><span data-stu-id="3db21-457">**Number**</span></span>|<span data-ttu-id="3db21-458">Çift duyarlıklı kayan noktalı sayı, standart IEEE 754.</span><span class="sxs-lookup"><span data-stu-id="3db21-458">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="3db21-459">**Dize**</span><span class="sxs-lookup"><span data-stu-id="3db21-459">**String**</span></span>|<span data-ttu-id="3db21-460">Sıfır veya daha fazla Unicode karakter dizisi.</span><span class="sxs-lookup"><span data-stu-id="3db21-460">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="3db21-461">Dizeleri tek veya çift tırnak içine alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3db21-461">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="3db21-462">**Dizi**</span><span class="sxs-lookup"><span data-stu-id="3db21-462">**Array**</span></span>|<span data-ttu-id="3db21-463">Sıfır veya daha fazla öğeleri dizisi.</span><span class="sxs-lookup"><span data-stu-id="3db21-463">A sequence of zero or more elements.</span></span> <span data-ttu-id="3db21-464">Her öğe tanımlanmamış dışında herhangi bir skaler veri türü değeri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3db21-464">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="3db21-465">**Nesne**</span><span class="sxs-lookup"><span data-stu-id="3db21-465">**Object**</span></span>|<span data-ttu-id="3db21-466">Sırasız bir sıfır veya daha fazla ad/değer çiftleri kümesi.</span><span class="sxs-lookup"><span data-stu-id="3db21-466">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="3db21-467">Adı bir UNICODE dizesi, değeri dışında herhangi bir skaler veri türde olabilir **tanımlanmamış**.</span><span class="sxs-lookup"><span data-stu-id="3db21-467">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="3db21-468">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-468">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="3db21-469">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-469">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="3db21-470">Türü tanımlanmamış değeri tanımsız temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-470">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="3db21-471">Temsil eden **null** türü değeri **Null**.</span><span class="sxs-lookup"><span data-stu-id="3db21-471">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="3db21-472">Boolean türünde sabiti temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-472">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="3db21-473">Temsil eden **yanlış** türü Boolean değeri.</span><span class="sxs-lookup"><span data-stu-id="3db21-473">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="3db21-474">Temsil eden **true** türü Boolean değeri.</span><span class="sxs-lookup"><span data-stu-id="3db21-474">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="3db21-475">Bir sabiti temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-475">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="3db21-476">Ondalık değişmez değerleri ondalık sayı veya bilimsel gösterim kullanılarak temsil numaralarıdır.</span><span class="sxs-lookup"><span data-stu-id="3db21-476">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="3db21-477">Onaltılık değişmez değerler, önek '0 x bir veya daha fazla onaltılık basamak ile izlenen' kullanılarak temsil numaralarıdır.</span><span class="sxs-lookup"><span data-stu-id="3db21-477">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="3db21-478">Dize türünde bir sabiti temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-478">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="3db21-479">Dize değişmez değerleri, sıfır veya daha fazla Unicode karakter dizisi veya kaçış sıraları tarafından temsil edilen Unicode dizelerdir.</span><span class="sxs-lookup"><span data-stu-id="3db21-479">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="3db21-480">Dize değişmez değerleri tek tırnak içine alınmış (kesme işareti: ') veya çift tırnak (tırnak işareti: ").</span><span class="sxs-lookup"><span data-stu-id="3db21-480">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="3db21-481">Aşağıdaki kaçış sıralarına izin vermesi:</span><span class="sxs-lookup"><span data-stu-id="3db21-481">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="3db21-482">**Kaçış sırası**</span><span class="sxs-lookup"><span data-stu-id="3db21-482">**Escape sequence**</span></span>|<span data-ttu-id="3db21-483">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="3db21-483">**Description**</span></span>|<span data-ttu-id="3db21-484">**Unicode karakter**</span><span class="sxs-lookup"><span data-stu-id="3db21-484">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="3db21-485">\\'</span><span class="sxs-lookup"><span data-stu-id="3db21-485">\\'</span></span>|<span data-ttu-id="3db21-486">kesme işareti (')</span><span class="sxs-lookup"><span data-stu-id="3db21-486">apostrophe (')</span></span>|<span data-ttu-id="3db21-487">U + 0027</span><span class="sxs-lookup"><span data-stu-id="3db21-487">U+0027</span></span>|  
|<span data-ttu-id="3db21-488">\\"</span><span class="sxs-lookup"><span data-stu-id="3db21-488">\\"</span></span>|<span data-ttu-id="3db21-489">tırnak işareti (")</span><span class="sxs-lookup"><span data-stu-id="3db21-489">quotation mark (")</span></span>|<span data-ttu-id="3db21-490">U + 0022</span><span class="sxs-lookup"><span data-stu-id="3db21-490">U+0022</span></span>|  
|\\\|<span data-ttu-id="3db21-491">Ters solidus (\\)</span><span class="sxs-lookup"><span data-stu-id="3db21-491">reverse solidus (\\)</span></span>|<span data-ttu-id="3db21-492">U + 005C</span><span class="sxs-lookup"><span data-stu-id="3db21-492">U+005C</span></span>|  
|\\/|<span data-ttu-id="3db21-493">solidus (/)</span><span class="sxs-lookup"><span data-stu-id="3db21-493">solidus (/)</span></span>|<span data-ttu-id="3db21-494">U + 002F</span><span class="sxs-lookup"><span data-stu-id="3db21-494">U+002F</span></span>|  
|<span data-ttu-id="3db21-495">\b</span><span class="sxs-lookup"><span data-stu-id="3db21-495">\b</span></span>|<span data-ttu-id="3db21-496">Geri Al</span><span class="sxs-lookup"><span data-stu-id="3db21-496">backspace</span></span>|<span data-ttu-id="3db21-497">U + 0008</span><span class="sxs-lookup"><span data-stu-id="3db21-497">U+0008</span></span>|  
|<span data-ttu-id="3db21-498">\f</span><span class="sxs-lookup"><span data-stu-id="3db21-498">\f</span></span>|<span data-ttu-id="3db21-499">sonraki sayfaya geçme</span><span class="sxs-lookup"><span data-stu-id="3db21-499">form feed</span></span>|<span data-ttu-id="3db21-500">U + 000C</span><span class="sxs-lookup"><span data-stu-id="3db21-500">U+000C</span></span>|  
|\n|<span data-ttu-id="3db21-501">satır besleme</span><span class="sxs-lookup"><span data-stu-id="3db21-501">line feed</span></span>|<span data-ttu-id="3db21-502">U + 000A</span><span class="sxs-lookup"><span data-stu-id="3db21-502">U+000A</span></span>|  
|<span data-ttu-id="3db21-503">\r</span><span class="sxs-lookup"><span data-stu-id="3db21-503">\r</span></span>|<span data-ttu-id="3db21-504">satır başı</span><span class="sxs-lookup"><span data-stu-id="3db21-504">carriage return</span></span>|<span data-ttu-id="3db21-505">U + 000D</span><span class="sxs-lookup"><span data-stu-id="3db21-505">U+000D</span></span>|  
|<span data-ttu-id="3db21-506">\t</span><span class="sxs-lookup"><span data-stu-id="3db21-506">\t</span></span>|<span data-ttu-id="3db21-507">Sekmesi</span><span class="sxs-lookup"><span data-stu-id="3db21-507">tab</span></span>|<span data-ttu-id="3db21-508">U + 0009</span><span class="sxs-lookup"><span data-stu-id="3db21-508">U+0009</span></span>|  
|<span data-ttu-id="3db21-509">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="3db21-509">\uXXXX</span></span>|<span data-ttu-id="3db21-510">4 onaltılık basamak tarafından tanımlanan bir Unicode karakter.</span><span class="sxs-lookup"><span data-stu-id="3db21-510">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="3db21-511">U + XXXX</span><span class="sxs-lookup"><span data-stu-id="3db21-511">U+XXXX</span></span>|  
  
##  <span data-ttu-id="3db21-512"><a name="bk_query_perf_guidelines"></a>Sorgu performans kuralları</span><span class="sxs-lookup"><span data-stu-id="3db21-512"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="3db21-513">Verimli bir şekilde büyük bir koleksiyon için yürütülen bir sorgu toobe için sırayla bir veya daha fazla dizinleri sunulan filtreleri kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3db21-513">In order for a query toobe executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="3db21-514">Dizin arama için filtreleri aşağıdaki hello kabul edilir:</span><span class="sxs-lookup"><span data-stu-id="3db21-514">hello following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="3db21-515">Eşitlik işleci (=), bir belge yol ifadesi ve bir sabit ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="3db21-515">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="3db21-516">Aralık işleçleri kullanın (<, \<=, >, > =) bir belge yol ifadesi ve sayı sabitleri.</span><span class="sxs-lookup"><span data-stu-id="3db21-516">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="3db21-517">Belge yol ifadesi sabit bir yol başvurulan hello veritabanı koleksiyonundan hello belgelerdeki tanımlayan herhangi bir ifade gösterir.</span><span class="sxs-lookup"><span data-stu-id="3db21-517">Document path expression stands for any expression which identifies a constant path in hello documents from hello referenced database collection.</span></span>  
  
 <span data-ttu-id="3db21-518">**Belge yol ifadesi**</span><span class="sxs-lookup"><span data-stu-id="3db21-518">**Document path expression**</span></span>  
  
 <span data-ttu-id="3db21-519">Belge yol ifadelerini ifadeleri, özelliği veya dizi dizin oluşturucu assessors veritabanı koleksiyon belgelerden gelen bir belge üzerinden yolu.</span><span class="sxs-lookup"><span data-stu-id="3db21-519">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="3db21-520">Bu yol hello veritabanı koleksiyonundaki hello belgelerde doğrudan bir filtrede başvurulan değerleri kullanılan tooidentify hello konumu olabilir.</span><span class="sxs-lookup"><span data-stu-id="3db21-520">This path can be used tooidentify hello location of values referenced in a filter directly within hello documents in hello database collection.</span></span>  
  
 <span data-ttu-id="3db21-521">Bir ifade toobe için bir belge yol ifadesi olarak kabul edilmelidir:</span><span class="sxs-lookup"><span data-stu-id="3db21-521">For an expression toobe considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="3db21-522">Başvuru hello koleksiyonu kök doğrudan.</span><span class="sxs-lookup"><span data-stu-id="3db21-522">Reference hello collection root directly.</span></span>  
  
2.  <span data-ttu-id="3db21-523">Bazı belge yol ifadesi başvuru özelliği ya da sabiti dizi Oluşturucusu</span><span class="sxs-lookup"><span data-stu-id="3db21-523">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="3db21-524">Bazı belge yol ifadesi temsil eden bir diğer ad başvuru.</span><span class="sxs-lookup"><span data-stu-id="3db21-524">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="3db21-525">**Sözdizimi kuralları**</span><span class="sxs-lookup"><span data-stu-id="3db21-525">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="3db21-526">Aşağıdaki tablonun hello hello kullanılan kuralları toodescribe sözdizimi hello DocumentDB API sorgu dili başvurusu açıklar.</span><span class="sxs-lookup"><span data-stu-id="3db21-526">hello following table describes hello conventions used toodescribe syntax in hello DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="3db21-527">**Kuralı**</span><span class="sxs-lookup"><span data-stu-id="3db21-527">**Convention**</span></span>|<span data-ttu-id="3db21-528">**İçin kullanılır**</span><span class="sxs-lookup"><span data-stu-id="3db21-528">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="3db21-529">BÜYÜK HARF</span><span class="sxs-lookup"><span data-stu-id="3db21-529">UPPERCASE</span></span>|<span data-ttu-id="3db21-530">Büyük küçük harf duyarlı anahtar sözcükler.</span><span class="sxs-lookup"><span data-stu-id="3db21-530">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="3db21-531">küçük harf</span><span class="sxs-lookup"><span data-stu-id="3db21-531">lowercase</span></span>|<span data-ttu-id="3db21-532">Büyük küçük harfe duyarlı anahtar sözcükler.</span><span class="sxs-lookup"><span data-stu-id="3db21-532">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="3db21-533">\<nonterminal ></span><span class="sxs-lookup"><span data-stu-id="3db21-533">\<nonterminal></span></span>|<span data-ttu-id="3db21-534">Terminal dışı, ayrı olarak tanımlı.</span><span class="sxs-lookup"><span data-stu-id="3db21-534">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="3db21-535">\<nonterminal >:: =</span><span class="sxs-lookup"><span data-stu-id="3db21-535">\<nonterminal> ::=</span></span>|<span data-ttu-id="3db21-536">Merhaba nonterminal sözdizimi tanımı.</span><span class="sxs-lookup"><span data-stu-id="3db21-536">Syntax definition of hello nonterminal.</span></span>|  
    |<span data-ttu-id="3db21-537">other_terminal</span><span class="sxs-lookup"><span data-stu-id="3db21-537">other_terminal</span></span>|<span data-ttu-id="3db21-538">Sözcük içindeki ayrıntısı açıklanan Terminal (belirteç).</span><span class="sxs-lookup"><span data-stu-id="3db21-538">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="3db21-539">Tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="3db21-539">identifier</span></span>|<span data-ttu-id="3db21-540">Tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="3db21-540">Identifier.</span></span> <span data-ttu-id="3db21-541">Aşağıdaki karakterleri yalnızca sağlar: a-z A-Z 0-9 _First karakter, bir sayı olamaz.</span><span class="sxs-lookup"><span data-stu-id="3db21-541">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="3db21-542">"dize"</span><span class="sxs-lookup"><span data-stu-id="3db21-542">"string"</span></span>|<span data-ttu-id="3db21-543">Tırnak işaretli dizesi.</span><span class="sxs-lookup"><span data-stu-id="3db21-543">Quoted string.</span></span> <span data-ttu-id="3db21-544">Geçerli bir dize verir.</span><span class="sxs-lookup"><span data-stu-id="3db21-544">Allows any valid string.</span></span> <span data-ttu-id="3db21-545">Bir string_literal açıklamasına bakın.</span><span class="sxs-lookup"><span data-stu-id="3db21-545">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="3db21-546">'simgesi'</span><span class="sxs-lookup"><span data-stu-id="3db21-546">'symbol'</span></span>|<span data-ttu-id="3db21-547">Merhaba sözdizimi parçası olan değişmez değer simge.</span><span class="sxs-lookup"><span data-stu-id="3db21-547">Literal symbol which is part of hello syntax.</span></span>|  
    |<span data-ttu-id="3db21-548">&#124; (dikey çubuk)</span><span class="sxs-lookup"><span data-stu-id="3db21-548">&#124; (vertical bar)</span></span>|<span data-ttu-id="3db21-549">Alternatifleri sözdizimi öğeleri için.</span><span class="sxs-lookup"><span data-stu-id="3db21-549">Alternatives for syntax items.</span></span> <span data-ttu-id="3db21-550">Belirtilen hello öğeleri yalnızca birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3db21-550">You can use only one of hello items specified.</span></span>|  
    |<span data-ttu-id="3db21-551">[] /(brackets)</span><span class="sxs-lookup"><span data-stu-id="3db21-551">[ ] /(brackets)</span></span>|<span data-ttu-id="3db21-552">Köşeli bir veya daha fazla isteğe bağlı öğeleri kapatın.</span><span class="sxs-lookup"><span data-stu-id="3db21-552">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="3db21-553">[,.. .n]</span><span class="sxs-lookup"><span data-stu-id="3db21-553">[ ,...n ]</span></span>|<span data-ttu-id="3db21-554">Öğesini önceki hello yinelenen n kaç kez uygulanıp uygulanamayacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3db21-554">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="3db21-555">Merhaba oluşum virgülle ayrılır.</span><span class="sxs-lookup"><span data-stu-id="3db21-555">hello occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="3db21-556">[.. .n]</span><span class="sxs-lookup"><span data-stu-id="3db21-556">[ ...n ]</span></span>|<span data-ttu-id="3db21-557">Öğesini önceki hello yinelenen n kaç kez uygulanıp uygulanamayacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3db21-557">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="3db21-558">Merhaba oluşum boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="3db21-558">hello occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="3db21-559"><a name="bk_built_in_functions"></a>Yerleşik işlevler</span><span class="sxs-lookup"><span data-stu-id="3db21-559"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="3db21-560">Azure Cosmos DB birçok yerleşik SQL işlevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="3db21-560">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="3db21-561">Yerleşik işlev Hello kategorileri aşağıda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-561">hello categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="3db21-562">İşlevi</span><span class="sxs-lookup"><span data-stu-id="3db21-562">Function</span></span>|<span data-ttu-id="3db21-563">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3db21-563">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="3db21-564">Matematik işlevleri</span><span class="sxs-lookup"><span data-stu-id="3db21-564">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="3db21-565">Merhaba matematik işlevleri her genellikle, bağımsız değişken olarak sağlanır ve sayısal bir değeri döndürme giriş değerlerine göre bir hesaplama gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="3db21-565">hello mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="3db21-566">Denetimi işlevleri yazın</span><span class="sxs-lookup"><span data-stu-id="3db21-566">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="3db21-567">Merhaba tür denetimi işlevleri içinde SQL sorguları ifade toocheck hello türü izin verin.</span><span class="sxs-lookup"><span data-stu-id="3db21-567">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="3db21-568">Dize işlevleri</span><span class="sxs-lookup"><span data-stu-id="3db21-568">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="3db21-569">Merhaba dize işlevleri dizesi giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir dize, sayısal ya da Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-569">hello string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="3db21-570">Dizi işlevleri</span><span class="sxs-lookup"><span data-stu-id="3db21-570">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="3db21-571">Merhaba dizi işlevleri bir Boole değeri veya dizi değeri, bir dizi giriş değeri ve return sayısal işlem gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="3db21-571">hello array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="3db21-572">Uzamsal işlevleri</span><span class="sxs-lookup"><span data-stu-id="3db21-572">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="3db21-573">Merhaba uzamsal işlevleri uzamsal nesne giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir sayısal ya da Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-573">hello spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="3db21-574"><a name="bk_mathematical_functions"></a>Matematik işlevleri</span><span class="sxs-lookup"><span data-stu-id="3db21-574"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="3db21-575">Merhaba aşağıdaki işlevleri genellikle, bağımsız değişken olarak sağlanır ve sayısal bir değeri döndürme giriş değerlerine göre bir hesaplama gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="3db21-575">hello following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="3db21-576">ABS</span><span class="sxs-lookup"><span data-stu-id="3db21-576">ABS</span></span>](#bk_abs)|[<span data-ttu-id="3db21-577">ACOS</span><span class="sxs-lookup"><span data-stu-id="3db21-577">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="3db21-578">ASIN</span><span class="sxs-lookup"><span data-stu-id="3db21-578">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="3db21-579">ATAN</span><span class="sxs-lookup"><span data-stu-id="3db21-579">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="3db21-580">ATN2</span><span class="sxs-lookup"><span data-stu-id="3db21-580">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="3db21-581">TAVAN</span><span class="sxs-lookup"><span data-stu-id="3db21-581">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="3db21-582">COS</span><span class="sxs-lookup"><span data-stu-id="3db21-582">COS</span></span>](#bk_cos)|[<span data-ttu-id="3db21-583">COT</span><span class="sxs-lookup"><span data-stu-id="3db21-583">COT</span></span>](#bk_cot)|[<span data-ttu-id="3db21-584">DERECE</span><span class="sxs-lookup"><span data-stu-id="3db21-584">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="3db21-585">EXP</span><span class="sxs-lookup"><span data-stu-id="3db21-585">EXP</span></span>](#bk_exp)|[<span data-ttu-id="3db21-586">KAT</span><span class="sxs-lookup"><span data-stu-id="3db21-586">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="3db21-587">GÜNLÜK</span><span class="sxs-lookup"><span data-stu-id="3db21-587">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="3db21-588">LOG10</span><span class="sxs-lookup"><span data-stu-id="3db21-588">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="3db21-589">PI</span><span class="sxs-lookup"><span data-stu-id="3db21-589">PI</span></span>](#bk_pi)|[<span data-ttu-id="3db21-590">GÜÇ</span><span class="sxs-lookup"><span data-stu-id="3db21-590">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="3db21-591">RADYAN CİNSİNDEN</span><span class="sxs-lookup"><span data-stu-id="3db21-591">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="3db21-592">YUVARLAK</span><span class="sxs-lookup"><span data-stu-id="3db21-592">ROUND</span></span>](#bk_round)|[<span data-ttu-id="3db21-593">SIN</span><span class="sxs-lookup"><span data-stu-id="3db21-593">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="3db21-594">SQRT</span><span class="sxs-lookup"><span data-stu-id="3db21-594">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="3db21-595">KARE</span><span class="sxs-lookup"><span data-stu-id="3db21-595">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="3db21-596">OTURUM</span><span class="sxs-lookup"><span data-stu-id="3db21-596">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="3db21-597">TAN</span><span class="sxs-lookup"><span data-stu-id="3db21-597">TAN</span></span>](#bk_tan)|[<span data-ttu-id="3db21-598">TRUNC</span><span class="sxs-lookup"><span data-stu-id="3db21-598">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="3db21-599"><a name="bk_abs"></a>ABS</span><span class="sxs-lookup"><span data-stu-id="3db21-599"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="3db21-600">Sayısal ifade döndürür hello mutlak (pozitif) değerini hello belirtildi.</span><span class="sxs-lookup"><span data-stu-id="3db21-600">Returns hello absolute (positive) value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-601">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-601">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-602">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-602">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-603">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-603">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-604">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-604">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-605">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-605">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-606">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-606">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-607">Merhaba aşağıdaki örnek üç farklı numaralarında hello ABS işlevi kullanılarak hello sonuçlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3db21-607">hello following example shows hello results of using hello ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="3db21-608">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-608">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="3db21-609"><a name="bk_acos"></a>ACOS</span><span class="sxs-lookup"><span data-stu-id="3db21-609"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="3db21-610">Kosinüsü belirtilen sayısal ifade hello radyan cinsinden döndürür hello açı; arccosine olarak da bilinir.</span><span class="sxs-lookup"><span data-stu-id="3db21-610">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="3db21-611">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-611">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-612">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-612">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-613">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-613">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-614">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-614">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-615">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-615">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-616">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-616">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-617">Merhaba aşağıdaki örnek hello ACOS-1 döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-617">hello following example returns hello ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="3db21-618">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-618">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="3db21-619"><a name="bk_asin"></a>ASIN</span><span class="sxs-lookup"><span data-stu-id="3db21-619"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="3db21-620">Döndürür hello açının sinüsü hello olduğundan, sayısal ifade radyan cinsinden.</span><span class="sxs-lookup"><span data-stu-id="3db21-620">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="3db21-621">Bu arksinüsünü olarak da adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="3db21-621">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="3db21-622">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-622">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-623">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-623">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-624">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-624">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-625">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-625">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-626">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-626">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-627">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-627">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-628">Merhaba aşağıdaki örnek hello ASIN-1 döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-628">hello following example returns hello ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="3db21-629">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-629">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="3db21-630"><a name="bk_atan"></a>ATAN</span><span class="sxs-lookup"><span data-stu-id="3db21-630"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="3db21-631">Döndürür hello açının tanjantı hello olduğundan, sayısal ifade radyan cinsinden.</span><span class="sxs-lookup"><span data-stu-id="3db21-631">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="3db21-632">Bu arktanjantını olarak da adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="3db21-632">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="3db21-633">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-633">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-634">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-634">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-635">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-635">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-636">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-636">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-637">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-637">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-638">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-638">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-639">Aşağıdaki döndürür hello ATAN hello örneğine hello değer belirtildi.</span><span class="sxs-lookup"><span data-stu-id="3db21-639">hello following example returns hello ATAN of hello specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="3db21-640">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-640">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="3db21-641"><a name="bk_atn2"></a>ATN2</span><span class="sxs-lookup"><span data-stu-id="3db21-641"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="3db21-642">Merhaba asıl hello Ark radyan cinsinden ifade edilen tanjantı y / x değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-642">Returns hello principal value of hello arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="3db21-643">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-643">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-644">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-644">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-645">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-645">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-646">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-646">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-647">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-647">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-648">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-648">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-649">Merhaba aşağıdaki örnek hesaplar hello ATN2 belirtilen hello için x ve y bileşenleri.</span><span class="sxs-lookup"><span data-stu-id="3db21-649">hello following example calculates hello ATN2 for hello specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="3db21-650">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-650">Here is hello result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="3db21-651"><a name="bk_ceiling"></a>TAVAN</span><span class="sxs-lookup"><span data-stu-id="3db21-651"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="3db21-652">En küçük tamsayı değeri büyük hello veya belirtilen sayısal ifade hello eşit verir.</span><span class="sxs-lookup"><span data-stu-id="3db21-652">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-653">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-653">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-654">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-654">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-655">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-655">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-656">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-656">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-657">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-657">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-658">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-658">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-659">TAVAN işlevi sıfır değerleri ile Merhaba ve pozitif sayısal, negatif aşağıdaki örneğine hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="3db21-659">hello following example shows positive numeric, negative, and zero values with hello CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="3db21-660">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-660">Here is hello result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="3db21-661"><a name="bk_cos"></a>COS</span><span class="sxs-lookup"><span data-stu-id="3db21-661"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="3db21-662">Döndürür hello trigonometrik kosinüsünü hello radyan cinsinden açı, hello ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="3db21-662">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="3db21-663">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-663">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-664">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-664">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-665">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-665">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-666">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-666">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-667">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-667">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-668">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-668">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-669">Aşağıdaki örnek hello hello Merhaba açı belirtilen COS hesaplar.</span><span class="sxs-lookup"><span data-stu-id="3db21-669">hello following example calculates hello COS of hello specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="3db21-670">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-670">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="3db21-671"><a name="bk_cot"></a>COT</span><span class="sxs-lookup"><span data-stu-id="3db21-671"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="3db21-672">Döndürür hello trigonometrik kotanjantını hello radyan cinsinden açı, hello sayısal ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="3db21-672">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-673">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-673">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-674">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-674">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-675">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-675">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-676">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-676">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-677">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-677">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-678">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-678">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-679">Aşağıdaki örnek hello hello hello belirtilen açının COT hesaplar.</span><span class="sxs-lookup"><span data-stu-id="3db21-679">hello following example calculates hello COT of hello specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="3db21-680">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-680">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="3db21-681"><a name="bk_degrees"></a>DERECE</span><span class="sxs-lookup"><span data-stu-id="3db21-681"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="3db21-682">Karşılık gelen açıyı radyan cinsinden açı için derece cinsinden döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="3db21-682">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="3db21-683">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-683">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-684">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-684">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-685">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-685">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-686">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-686">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-687">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-687">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-688">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-688">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-689">Merhaba aşağıdaki örnek hello sayısını derece, PI/2 radyan cinsinden açı döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-689">hello following example returns hello number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="3db21-690">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-690">Here is hello result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="3db21-691"><a name="bk_floor"></a>KAT</span><span class="sxs-lookup"><span data-stu-id="3db21-691"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="3db21-692">Daha az Hello en büyük tamsayıyı döndürür veya bu değere eşit toohello sayısal ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="3db21-692">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-693">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-693">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-694">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-694">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-695">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-695">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-696">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-696">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-697">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-697">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-698">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-698">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-699">FLOOR işlevi sıfır değerleri ile Merhaba ve pozitif sayısal, negatif aşağıdaki örneğine hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="3db21-699">hello following example shows positive numeric, negative, and zero values with hello FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="3db21-700">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-700">Here is hello result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="3db21-701"><a name="bk_exp"></a>EXP</span><span class="sxs-lookup"><span data-stu-id="3db21-701"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="3db21-702">Merhaba, hello üstel değer döndüren sayısal ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="3db21-702">Returns hello exponential value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-703">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-703">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-704">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-704">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-705">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-705">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-706">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-706">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-707">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-707">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-708">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="3db21-708">**Remarks**</span></span>  
  
 <span data-ttu-id="3db21-709">Merhaba sabiti **e** (2.718281...) olan hello doğal logaritma temel.</span><span class="sxs-lookup"><span data-stu-id="3db21-709">hello constant **e** (2.718281…), is hello base of natural logarithms.</span></span>  
  
 <span data-ttu-id="3db21-710">Merhaba sayısının üssü hello sabiti olduğunda **e** toohello hello sayının üssünün.</span><span class="sxs-lookup"><span data-stu-id="3db21-710">hello exponent of a number is hello constant **e** raised toohello power of hello number.</span></span> <span data-ttu-id="3db21-711">Örneğin EXP(1.0) e = ^ 1.0 = 2.71828182845905 ve EXP(10) e = ^ 10 = 22026.4657948067.</span><span class="sxs-lookup"><span data-stu-id="3db21-711">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="3db21-712">bir sayının hello doğal logaritmasını üstel Hello numarasıdır hello kendisini: EXP (günlüğü (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="3db21-712">hello exponential of hello natural logarithm of a number is hello number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="3db21-713">Ve bir dizi üstel hello hello doğal logaritmasını hello numarasıdır kendisini: günlük (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="3db21-713">And hello natural logarithm of hello exponential of a number is hello number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="3db21-714">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-714">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-715">Merhaba aşağıdaki örnekte değişken bildirir ve hello üstel hello belirtilen değişkeni (10) değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-715">hello following example declares a variable and returns hello exponential value of hello specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="3db21-716">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-716">Here is hello result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="3db21-717">Merhaba aşağıdaki örnek hello üstel değerini 20 hello doğal logaritmasını ve hello hello doğal logaritmasını 20 üstel döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-717">hello following example returns hello exponential value of hello natural logarithm of 20 and hello natural logarithm of hello exponential of 20.</span></span> <span data-ttu-id="3db21-718">Bu işlevler inverse işlevleri, bir başka hello dönüş değeri kayan nokta 20 matematik her iki durumda olduğu için yuvarlama ile olduğundan.</span><span class="sxs-lookup"><span data-stu-id="3db21-718">Because these functions are inverse functions of one another, hello return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="3db21-719">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-719">Here is hello result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="3db21-720"><a name="bk_log"></a>GÜNLÜK</span><span class="sxs-lookup"><span data-stu-id="3db21-720"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="3db21-721">Merhaba hello doğal logaritmasını döndürür sayısal ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="3db21-721">Returns hello natural logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-722">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-722">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="3db21-723">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-723">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-724">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-724">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="3db21-725">Merhaba hello logaritmanın tabanı ayarlar isteğe bağlı sayısal değişkeni.</span><span class="sxs-lookup"><span data-stu-id="3db21-725">Optional numeric argument that sets hello base for hello logarithm.</span></span>  
  
 <span data-ttu-id="3db21-726">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-726">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-727">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-727">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-728">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="3db21-728">**Remarks**</span></span>  
  
 <span data-ttu-id="3db21-729">Varsayılan olarak, LOG() hello doğal logaritmasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-729">By default, LOG() returns hello natural logarithm.</span></span> <span data-ttu-id="3db21-730">Merhaba temel hello logaritmasını tooanother değerinin hello isteğe bağlı temel parametresini kullanarak değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3db21-730">You can change hello base of hello logarithm tooanother value by using hello optional base parameter.</span></span>  
  
 <span data-ttu-id="3db21-731">Hello doğal logaritmasını olduğu hello logaritmasını toohello temel **e**, burada **e** Irrational bir sabit yaklaşık olarak eşit too2.718281828 değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-731">hello natural logarithm is hello logarithm toohello base **e**, where **e** is an irrational constant approximately equal too2.718281828.</span></span>  
  
 <span data-ttu-id="3db21-732">Merhaba bir dizi üstel Hello doğal logaritmasını numarasıdır hello kendisini: günlük (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="3db21-732">hello natural logarithm of hello exponential of a number is hello number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="3db21-733">Ve sayının hello doğal logaritmasını üstel hello hello numarasıdır kendisini: EXP (günlüğü (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="3db21-733">And hello exponential of hello natural logarithm of a number is hello number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="3db21-734">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-734">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-735">Merhaba aşağıdaki örnekte değişken bildirir ve hello logaritmasını hello belirtilen değişkeni (10) değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-735">hello following example declares a variable and returns hello logarithm value of hello specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="3db21-736">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-736">Here is hello result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="3db21-737">Merhaba aşağıdaki örnek bir sayının hello üs Merhaba günlük hesaplar.</span><span class="sxs-lookup"><span data-stu-id="3db21-737">hello following example calculates hello LOG for hello exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="3db21-738">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-738">Here is hello result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="3db21-739"><a name="bk_log10"></a>LOG10</span><span class="sxs-lookup"><span data-stu-id="3db21-739"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="3db21-740">Merhaba döndürür hello 10 tabanında logaritmasını sayısal ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="3db21-740">Returns hello base-10 logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-741">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-741">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-742">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-742">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-743">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-743">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-744">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-744">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-745">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-745">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-746">**Açıklamalar**</span><span class="sxs-lookup"><span data-stu-id="3db21-746">**Remarks**</span></span>  
  
 <span data-ttu-id="3db21-747">Merhaba LOG10 ve güç işlevleri inversely ilgili tooone olan başka bir.</span><span class="sxs-lookup"><span data-stu-id="3db21-747">hello LOG10 and POWER functions are inversely related tooone another.</span></span> <span data-ttu-id="3db21-748">Örneğin, 10 ^ LOG10(n) = n.</span><span class="sxs-lookup"><span data-stu-id="3db21-748">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="3db21-749">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-749">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-750">Merhaba aşağıdaki örnekte değişken bildirir ve hello LOG10 hello belirtilen değişkeni (100) değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-750">hello following example declares a variable and returns hello LOG10 value of hello specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="3db21-751">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-751">Here is hello result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="3db21-752"><a name="bk_pi"></a>PI</span><span class="sxs-lookup"><span data-stu-id="3db21-752"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="3db21-753">PI sayısının sabit bir değer döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="3db21-753">Returns hello constant value of PI.</span></span>  
  
 <span data-ttu-id="3db21-754">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-754">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="3db21-755">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-755">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-756">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-756">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-757">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-757">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-758">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-758">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-759">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-759">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-760">Merhaba aşağıdaki örnek hello PI değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-760">hello following example returns hello value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="3db21-761">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-761">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="3db21-762"><a name="bk_power"></a>GÜÇ</span><span class="sxs-lookup"><span data-stu-id="3db21-762"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="3db21-763">Döndürür hello belirtilen başlangıç değeri ifadesi toohello belirtilen güç.</span><span class="sxs-lookup"><span data-stu-id="3db21-763">Returns hello value of hello specified expression toohello specified power.</span></span>  
  
 <span data-ttu-id="3db21-764">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-764">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="3db21-765">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-765">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-766">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-766">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="3db21-767">Merhaba güç toowhich tooraise olan `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="3db21-767">Is hello power toowhich tooraise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="3db21-768">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-768">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-769">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-769">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-770">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-770">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-771">Aşağıdaki örneğine hello 3 (Merhaba küp hello sayının) numara toohello gücünü oluşturma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-771">hello following example demonstrates raising a number toohello power of 3 (hello cube of hello number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="3db21-772">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-772">Here is hello result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="3db21-773"><a name="bk_radians"></a>RADYAN CİNSİNDEN</span><span class="sxs-lookup"><span data-stu-id="3db21-773"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="3db21-774">Derece sayısal bir ifadenin girildiğinde radyan cinsinden döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-774">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="3db21-775">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-775">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-776">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-776">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-777">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-777">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-778">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-778">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-779">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-779">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-780">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-780">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-781">Merhaba aşağıdaki örnekte birkaç açıları girdi olarak alır ve bunlara karşılık gelen radian değerler döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-781">hello following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="3db21-782">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-782">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="3db21-783"><a name="bk_round"></a>YUVARLAK</span><span class="sxs-lookup"><span data-stu-id="3db21-783"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="3db21-784">Yuvarlak toohello en yakın tamsayı değeri sayısal bir değer döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-784">Returns a numeric value, rounded toohello closest integer value.</span></span>  
  
 <span data-ttu-id="3db21-785">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-785">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-786">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-786">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-787">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-787">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-788">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-788">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-789">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-789">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-790">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-790">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-791">Merhaba aşağıdaki örnek pozitif ve negatif sayıları toohello tamsayı en yakın aşağıdaki hello yuvarlar.</span><span class="sxs-lookup"><span data-stu-id="3db21-791">hello following example rounds hello following positive and negative numbers toohello nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="3db21-792">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-792">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="3db21-793"><a name="bk_sign"></a>OTURUM</span><span class="sxs-lookup"><span data-stu-id="3db21-793"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="3db21-794">Artı (+ 1), sıfır (0), döndürür hello veya sayısal ifade hello eksi (-1) belirtisi belirtildi.</span><span class="sxs-lookup"><span data-stu-id="3db21-794">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-795">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-795">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-796">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-796">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-797">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-797">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-798">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-798">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-799">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-799">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-800">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-800">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-801">Merhaba aşağıdaki örnek hello oturum değerleri sayıların-2 too2 döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-801">hello following example returns hello SIGN values of numbers from -2 too2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="3db21-802">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-802">Here is hello result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="3db21-803"><a name="bk_sin"></a>SIN</span><span class="sxs-lookup"><span data-stu-id="3db21-803"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="3db21-804">Döndürür hello trigonometrik sinüsünü hello radyan cinsinden açı, hello ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="3db21-804">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="3db21-805">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-805">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-806">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-806">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-807">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-807">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-808">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-808">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-809">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-809">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-810">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-810">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-811">Aşağıdaki örnek hello hello SIN hello belirtilen açının hesaplar.</span><span class="sxs-lookup"><span data-stu-id="3db21-811">hello following example calculates hello SIN of hello specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="3db21-812">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-812">Here is hello result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="3db21-813"><a name="bk_sqrt"></a>SQRT</span><span class="sxs-lookup"><span data-stu-id="3db21-813"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="3db21-814">Belirtilen sayısal değer hello hello kare kökünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-814">Returns hello square root of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="3db21-815">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-815">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-816">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-816">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-817">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-817">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-818">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-818">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-819">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-819">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-820">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-820">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-821">Merhaba aşağıdaki örnek 1-3 sayıların hello kare kökleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-821">hello following example returns hello square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="3db21-822">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-822">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="3db21-823"><a name="bk_square"></a>KARE</span><span class="sxs-lookup"><span data-stu-id="3db21-823"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="3db21-824">Merhaba kare döndürür hello sayısal değer belirtildi.</span><span class="sxs-lookup"><span data-stu-id="3db21-824">Returns hello square of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="3db21-825">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-825">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-826">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-826">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-827">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-827">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-828">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-828">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-829">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-829">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-830">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-830">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-831">Merhaba aşağıdaki örnek numaraları 1-3 hello kareleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-831">hello following example returns hello squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="3db21-832">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-832">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="3db21-833"><a name="bk_tan"></a>TAN</span><span class="sxs-lookup"><span data-stu-id="3db21-833"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="3db21-834">Merhaba hello tanjantını döndürür radyan cinsinden açı, hello ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="3db21-834">Returns hello tangent of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="3db21-835">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-835">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-836">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-836">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-837">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-837">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-838">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-838">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-839">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-839">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-840">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-840">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-841">Merhaba aşağıdaki örnek hesaplar PI () hello tanjantını / 2.</span><span class="sxs-lookup"><span data-stu-id="3db21-841">hello following example calculates hello tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="3db21-842">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-842">Here is hello result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="3db21-843"><a name="bk_trunc"></a>TRUNC</span><span class="sxs-lookup"><span data-stu-id="3db21-843"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="3db21-844">Kesilmiş toohello en yakın tamsayı değeri sayısal bir değer döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-844">Returns a numeric value, truncated toohello closest integer value.</span></span>  
  
 <span data-ttu-id="3db21-845">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-845">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="3db21-846">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-846">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="3db21-847">Sayısal bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="3db21-847">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-848">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-848">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-849">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-849">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-850">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-850">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-851">Aşağıdaki örnek hello pozitif ve negatif sayıları toohello tamsayı değeri en yakın aşağıdaki hello tamsayıya dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-851">hello following example truncates hello following positive and negative numbers toohello nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="3db21-852">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-852">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="3db21-853"><a name="bk_type_checking_functions"></a>Denetimi işlevleri yazın</span><span class="sxs-lookup"><span data-stu-id="3db21-853"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="3db21-854">Merhaba aşağıdaki işlevleri karşı giriş değerleri denetleme türünü destekleyen ve her bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-854">hello following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="3db21-855">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="3db21-855">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="3db21-856">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="3db21-856">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="3db21-857">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="3db21-857">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="3db21-858">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="3db21-858">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="3db21-859">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="3db21-859">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="3db21-860">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="3db21-860">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="3db21-861">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="3db21-861">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="3db21-862">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="3db21-862">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="3db21-863"><a name="bk_is_array"></a>IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="3db21-863"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="3db21-864">Bir dizidir hello Hello türü ifade belirttiyseniz gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-864">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span>  
  
 <span data-ttu-id="3db21-865">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-865">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="3db21-866">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-866">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="3db21-867">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-867">Is any valid expression.</span></span>  
  
 <span data-ttu-id="3db21-868">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-868">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-869">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-869">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="3db21-870">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-870">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-871">Merhaba aşağıdaki örnek JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve hello IS_ARRAY işlevi kullanarak tanımsız türleri denetler.</span><span class="sxs-lookup"><span data-stu-id="3db21-871">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_ARRAY function.</span></span>  
  
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
  
 <span data-ttu-id="3db21-872">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-872">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="3db21-873"><a name="bk_is_bool"></a>IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="3db21-873"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="3db21-874">Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri olan bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-874">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="3db21-875">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-875">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="3db21-876">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-876">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="3db21-877">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-877">Is any valid expression.</span></span>  
  
 <span data-ttu-id="3db21-878">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-878">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-879">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-879">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="3db21-880">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-880">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-881">Merhaba aşağıdaki örnek JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve hello IS_BOOL işlevi kullanarak tanımsız türleri denetler.</span><span class="sxs-lookup"><span data-stu-id="3db21-881">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_BOOL function.</span></span>  
  
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
  
 <span data-ttu-id="3db21-882">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-882">Here is hello result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="3db21-883"><a name="bk_is_defined"></a>IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="3db21-883"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="3db21-884">Başlangıç özellik değeri atanmış olan gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-884">Returns a Boolean indicating if hello property has been assigned a value.</span></span>  
  
 <span data-ttu-id="3db21-885">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-885">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="3db21-886">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-886">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="3db21-887">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-887">Is any valid expression.</span></span>  
  
 <span data-ttu-id="3db21-888">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-888">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-889">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-889">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="3db21-890">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-890">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-891">Örnek denetimleri hello varlığını hello içinde bir özellik için aşağıdaki hello JSON belgesi belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="3db21-891">hello following example checks for hello presence of a property within hello specified JSON document.</span></span> <span data-ttu-id="3db21-892">Merhaba önce "a" var, ancak hello ikinci "b" mevcut olduğundan false döndürür. bu yana true değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-892">hello first returns true since "a" is present, but hello second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="3db21-893">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-893">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="3db21-894"><a name="bk_is_null"></a>IS_NULL</span><span class="sxs-lookup"><span data-stu-id="3db21-894"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="3db21-895">Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri null döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-895">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span>  
  
 <span data-ttu-id="3db21-896">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-896">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="3db21-897">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-897">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="3db21-898">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-898">Is any valid expression.</span></span>  
  
 <span data-ttu-id="3db21-899">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-899">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-900">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-900">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="3db21-901">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-901">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-902">Merhaba aşağıdaki örnek JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve hello IS_NULL işlevi kullanarak tanımsız türleri denetler.</span><span class="sxs-lookup"><span data-stu-id="3db21-902">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="3db21-903">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-903">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="3db21-904"><a name="bk_is_number"></a>IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="3db21-904"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="3db21-905">Bir sayıdır hello Hello türü ifade belirttiyseniz gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-905">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span>  
  
 <span data-ttu-id="3db21-906">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-906">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="3db21-907">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-907">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="3db21-908">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-908">Is any valid expression.</span></span>  
  
 <span data-ttu-id="3db21-909">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-909">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-910">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-910">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="3db21-911">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-911">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-912">Merhaba aşağıdaki örnek JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve hello IS_NULL işlevi kullanarak tanımsız türleri denetler.</span><span class="sxs-lookup"><span data-stu-id="3db21-912">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="3db21-913">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-913">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="3db21-914"><a name="bk_is_object"></a>IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="3db21-914"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="3db21-915">Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri olan bir JSON nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-915">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="3db21-916">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-916">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="3db21-917">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-917">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="3db21-918">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-918">Is any valid expression.</span></span>  
  
 <span data-ttu-id="3db21-919">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-919">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-920">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-920">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="3db21-921">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-921">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-922">Merhaba aşağıdaki örnek JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve hello IS_OBJECT işlevi kullanarak tanımsız türleri denetler.</span><span class="sxs-lookup"><span data-stu-id="3db21-922">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_OBJECT function.</span></span>  
  
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
  
 <span data-ttu-id="3db21-923">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-923">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="3db21-924"><a name="bk_is_primitive"></a>IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="3db21-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="3db21-925">Merhaba Hello türü ifade ilkel belirtilirse, gösteren bir Boole değeri döndürür (dize, Boolean, sayısal veya null).</span><span class="sxs-lookup"><span data-stu-id="3db21-925">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="3db21-926">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-926">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="3db21-927">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-927">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="3db21-928">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-928">Is any valid expression.</span></span>  
  
 <span data-ttu-id="3db21-929">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-929">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-930">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-930">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="3db21-931">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-931">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-932">Merhaba aşağıdaki örnek JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve hello IS_PRIMITIVE işlevi kullanarak tanımsız türleri denetler.</span><span class="sxs-lookup"><span data-stu-id="3db21-932">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_PRIMITIVE function.</span></span>  
  
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
  
 <span data-ttu-id="3db21-933">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-933">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="3db21-934"><a name="bk_is_string"></a>IS_STRING</span><span class="sxs-lookup"><span data-stu-id="3db21-934"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="3db21-935">Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri bir dize verir.</span><span class="sxs-lookup"><span data-stu-id="3db21-935">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span>  
  
 <span data-ttu-id="3db21-936">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-936">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="3db21-937">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-937">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="3db21-938">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-938">Is any valid expression.</span></span>  
  
 <span data-ttu-id="3db21-939">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-939">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-940">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-940">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="3db21-941">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-941">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-942">Merhaba aşağıdaki örnek JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve hello IS_STRING işlevi kullanarak tanımsız türleri denetler.</span><span class="sxs-lookup"><span data-stu-id="3db21-942">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_STRING function.</span></span>  
  
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
  
 <span data-ttu-id="3db21-943">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-943">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="3db21-944"><a name="bk_string_functions"></a>Dize işlevleri</span><span class="sxs-lookup"><span data-stu-id="3db21-944"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="3db21-945">Merhaba aşağıdaki skaler işlevler dize giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir dize, sayısal ya da Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-945">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="3db21-946">CONCAT</span><span class="sxs-lookup"><span data-stu-id="3db21-946">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="3db21-947">İÇERİR</span><span class="sxs-lookup"><span data-stu-id="3db21-947">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="3db21-948">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="3db21-948">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="3db21-949">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="3db21-949">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="3db21-950">SOL</span><span class="sxs-lookup"><span data-stu-id="3db21-950">LEFT</span></span>](#bk_left)|[<span data-ttu-id="3db21-951">UZUNLUĞU</span><span class="sxs-lookup"><span data-stu-id="3db21-951">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="3db21-952">DAHA DÜŞÜK</span><span class="sxs-lookup"><span data-stu-id="3db21-952">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="3db21-953">LTRIM</span><span class="sxs-lookup"><span data-stu-id="3db21-953">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="3db21-954">DEĞİŞTİR</span><span class="sxs-lookup"><span data-stu-id="3db21-954">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="3db21-955">ÇOĞALTILAN</span><span class="sxs-lookup"><span data-stu-id="3db21-955">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="3db21-956">TERS ÇEVİR</span><span class="sxs-lookup"><span data-stu-id="3db21-956">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="3db21-957">SAĞ</span><span class="sxs-lookup"><span data-stu-id="3db21-957">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="3db21-958">RTRIM</span><span class="sxs-lookup"><span data-stu-id="3db21-958">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="3db21-959">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="3db21-959">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="3db21-960">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="3db21-960">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="3db21-961">ÜST</span><span class="sxs-lookup"><span data-stu-id="3db21-961">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="3db21-962"><a name="bk_concat"></a>CONCAT</span><span class="sxs-lookup"><span data-stu-id="3db21-962"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="3db21-963">İki veya daha fazla dize değerlerini birleştirme hello sonucu olan bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-963">Returns a string that is hello result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="3db21-964">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-964">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="3db21-965">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-965">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-966">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-966">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="3db21-967">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-967">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-968">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-968">Returns a string expression.</span></span>  
  
 <span data-ttu-id="3db21-969">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-969">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-970">Örnek döndürür birleştirilmiş hello hello dizisi aşağıdaki hello değerleri belirtti.</span><span class="sxs-lookup"><span data-stu-id="3db21-970">hello following example returns hello concatenated string of hello specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="3db21-971">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-971">Here is hello result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="3db21-972"><a name="bk_contains"></a>İÇERİR</span><span class="sxs-lookup"><span data-stu-id="3db21-972"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="3db21-973">Merhaba ilk dize ifadesi hello ikinci içerip içermediğini gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-973">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span>  
  
 <span data-ttu-id="3db21-974">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-974">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="3db21-975">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-975">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-976">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-976">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="3db21-977">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-977">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-978">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-978">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="3db21-979">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-979">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-980">Merhaba aşağıdaki örnekte "abc" "ab" ve "d" içerir olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="3db21-980">hello following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="3db21-981">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-981">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="3db21-982"><a name="bk_endswith"></a>ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="3db21-982"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="3db21-983">Merhaba ilk dize ifadesi ile Merhaba ikinci bitip olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-983">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span>  
  
 <span data-ttu-id="3db21-984">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-984">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="3db21-985">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-985">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-986">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-986">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="3db21-987">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-987">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-988">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-988">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="3db21-989">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-989">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-990">Merhaba aşağıdaki örnekte "abc", "b" ve "bc" ile biten hello döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-990">hello following example returns hello "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="3db21-991">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-991">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="3db21-992"><a name="bk_index_of"></a>INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="3db21-992"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="3db21-993">Merhaba dize bulunmazsa hello ikinci dize ifadesi hello ilk belirtilen dize ifadesi veya -1 içinde hello ilk oluşum konumunu başlangıç hello döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-993">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>  
  
 <span data-ttu-id="3db21-994">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-994">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="3db21-995">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-995">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-996">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-996">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="3db21-997">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-997">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-998">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-998">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-999">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-999">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1000">Merhaba aşağıdaki örnekte "abc" içinde çeşitli alt dizeler hello dizinini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1000">hello following example returns hello index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="3db21-1001">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1001">Here is hello result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="3db21-1002"><a name="bk_left"></a>SOL</span><span class="sxs-lookup"><span data-stu-id="3db21-1002"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="3db21-1003">Döndürür hello sol bölümü bir dizenin belirtilen hello ile karakter sayısı.</span><span class="sxs-lookup"><span data-stu-id="3db21-1003">Returns hello left part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="3db21-1004">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1004">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="3db21-1005">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1005">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-1006">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1006">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="3db21-1007">Geçerli herhangi bir sayısal ifadeye ' dir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1007">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-1008">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1008">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1009">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1009">Returns a string expression.</span></span>  
  
 <span data-ttu-id="3db21-1010">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1010">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1011">Merhaba aşağıdaki örnekte "abc" bölümü çeşitli uzunluk değeri için sol hello döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1011">hello following example returns hello left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="3db21-1012">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1012">Here is hello result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="3db21-1013"><a name="bk_length"></a>UZUNLUĞU</span><span class="sxs-lookup"><span data-stu-id="3db21-1013"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="3db21-1014">Dize ifadesi belirtilen döndürür hello hello karakter sayısı.</span><span class="sxs-lookup"><span data-stu-id="3db21-1014">Returns hello number of characters of hello specified string expression.</span></span>  
  
 <span data-ttu-id="3db21-1015">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1015">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="3db21-1016">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1016">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-1017">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1017">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="3db21-1018">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1018">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1019">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1019">Returns a string expression.</span></span>  
  
 <span data-ttu-id="3db21-1020">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1020">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1021">Merhaba aşağıdaki örnek hello uzunlukta bir dize döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1021">hello following example returns hello length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="3db21-1022">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1022">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="3db21-1023"><a name="bk_lower"></a>DAHA DÜŞÜK</span><span class="sxs-lookup"><span data-stu-id="3db21-1023"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="3db21-1024">Büyük harf karakter veri toolowercase dönüştürmeden sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1024">Returns a string expression after converting uppercase character data toolowercase.</span></span>  
  
 <span data-ttu-id="3db21-1025">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1025">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="3db21-1026">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1026">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-1027">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1027">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="3db21-1028">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1028">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1029">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1029">Returns a string expression.</span></span>  
  
 <span data-ttu-id="3db21-1030">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1030">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1031">örnekte gösterildiği nasıl aşağıdaki hello toouse alt sorgu.</span><span class="sxs-lookup"><span data-stu-id="3db21-1031">hello following example shows how toouse LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="3db21-1032">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1032">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="3db21-1033"><a name="bk_ltrim"></a>LTRIM</span><span class="sxs-lookup"><span data-stu-id="3db21-1033"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="3db21-1034">Öndeki boşlukları kaldırır sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1034">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="3db21-1035">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1035">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="3db21-1036">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1036">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-1037">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1037">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="3db21-1038">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1038">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1039">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1039">Returns a string expression.</span></span>  
  
 <span data-ttu-id="3db21-1040">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1040">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1041">örnekte gösterildiği nasıl aşağıdaki hello toouse LTRIM bir sorgu içinde.</span><span class="sxs-lookup"><span data-stu-id="3db21-1041">hello following example shows how toouse LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="3db21-1042">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1042">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="3db21-1043"><a name="bk_replace"></a>DEĞİŞTİR</span><span class="sxs-lookup"><span data-stu-id="3db21-1043"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="3db21-1044">Belirtilen dize değeri tüm oluşumlarını başka bir dize değeri ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1044">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="3db21-1045">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1045">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="3db21-1046">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1046">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-1047">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1047">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="3db21-1048">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1048">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1049">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1049">Returns a string expression.</span></span>  
  
 <span data-ttu-id="3db21-1050">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1050">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1051">Aşağıdaki örneğine hello toouse bir sorguda nasıl YERİNİ gösterir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1051">hello following example shows how toouse REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="3db21-1052">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1052">Here is hello result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="3db21-1053"><a name="bk_replicate"></a>ÇOĞALTMA</span><span class="sxs-lookup"><span data-stu-id="3db21-1053"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="3db21-1054">Bir dize değeri, belirtilen sayıda yineler.</span><span class="sxs-lookup"><span data-stu-id="3db21-1054">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="3db21-1055">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1055">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="3db21-1056">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1056">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-1057">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1057">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="3db21-1058">Geçerli herhangi bir sayısal ifadeye ' dir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1058">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-1059">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1059">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1060">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1060">Returns a string expression.</span></span>  
  
 <span data-ttu-id="3db21-1061">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1061">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1062">Aşağıdaki örneğine hello nasıl toouse ÇOĞALTMAK sorguda gösterir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1062">hello following example shows how toouse REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="3db21-1063">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1063">Here is hello result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="3db21-1064"><a name="bk_reverse"></a>TERS ÇEVİR</span><span class="sxs-lookup"><span data-stu-id="3db21-1064"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="3db21-1065">Merhaba ters sırada bir dize değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1065">Returns hello reverse order of a string value.</span></span>  
  
 <span data-ttu-id="3db21-1066">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1066">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="3db21-1067">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1067">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-1068">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1068">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="3db21-1069">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1069">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1070">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1070">Returns a string expression.</span></span>  
  
 <span data-ttu-id="3db21-1071">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1071">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1072">Aşağıdaki örneğine hello nasıl toouse ters sorguda gösterir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1072">hello following example shows how toouse REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="3db21-1073">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1073">Here is hello result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="3db21-1074"><a name="bk_right"></a>SAĞ</span><span class="sxs-lookup"><span data-stu-id="3db21-1074"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="3db21-1075">Karakter sayısını döndürür hello dizesi sağ parçası hello ile belirtilen.</span><span class="sxs-lookup"><span data-stu-id="3db21-1075">Returns hello right part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="3db21-1076">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1076">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="3db21-1077">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1077">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-1078">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1078">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="3db21-1079">Geçerli herhangi bir sayısal ifadeye ' dir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1079">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-1080">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1080">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1081">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1081">Returns a string expression.</span></span>  
  
 <span data-ttu-id="3db21-1082">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1082">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1083">Merhaba aşağıdaki örnek hello sağ bölümünü "abc" için çeşitli uzunluk değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1083">hello following example returns hello right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="3db21-1084">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1084">Here is hello result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="3db21-1085"><a name="bk_rtrim"></a>RTRIM</span><span class="sxs-lookup"><span data-stu-id="3db21-1085"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="3db21-1086">Sondaki boşlukları kaldırır sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1086">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="3db21-1087">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1087">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="3db21-1088">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1088">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-1089">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1089">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="3db21-1090">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1090">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1091">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1091">Returns a string expression.</span></span>  
  
 <span data-ttu-id="3db21-1092">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1092">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1093">örnekte gösterildiği nasıl aşağıdaki hello toouse RTRIM bir sorgu içinde.</span><span class="sxs-lookup"><span data-stu-id="3db21-1093">hello following example shows how toouse RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="3db21-1094">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1094">Here is hello result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="3db21-1095"><a name="bk_startswith"></a>STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="3db21-1095"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="3db21-1096">Merhaba ilk dize ifadesi ile Merhaba ikinci başlayıp başlamadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1096">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span>  
  
 <span data-ttu-id="3db21-1097">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1097">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="3db21-1098">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1098">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-1099">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1099">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="3db21-1100">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1100">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1101">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1101">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="3db21-1102">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1102">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1103">Merhaba denetimleri Merhaba, dize "abc" aşağıdaki örnekte başlar "b" ve "a".</span><span class="sxs-lookup"><span data-stu-id="3db21-1103">hello following example checks if hello string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="3db21-1104">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1104">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="3db21-1105"><a name="bk_substring"></a>SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="3db21-1105"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="3db21-1106">Merhaba başlayan bir dize ifadesi döndürür parçası karakter sıfır tabanlı konumu belirtilen ve uzunluk veya hello dize toohello sonu toohello belirtilen devam eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-1106">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span>  
  
 <span data-ttu-id="3db21-1107">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1107">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="3db21-1108">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1108">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-1109">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1109">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="3db21-1110">Geçerli herhangi bir sayısal ifadeye ' dir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1110">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-1111">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1111">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1112">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1112">Returns a string expression.</span></span>  
  
 <span data-ttu-id="3db21-1113">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1113">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1114">Merhaba aşağıdaki örnekte "abc" Merhaba dizenin 1 ve 1 karakter uzunluğu için başlangıç döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1114">hello following example returns hello substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="3db21-1115">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1115">Here is hello result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="3db21-1116"><a name="bk_upper"></a>ÜST</span><span class="sxs-lookup"><span data-stu-id="3db21-1116"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="3db21-1117">Küçük harf karakter veri toouppercase dönüştürmeden sonra bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1117">Returns a string expression after converting lowercase character data toouppercase.</span></span>  
  
 <span data-ttu-id="3db21-1118">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1118">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="3db21-1119">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1119">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="3db21-1120">Tüm geçerli bir dize ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1120">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="3db21-1121">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1121">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1122">Bir dize ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1122">Returns a string expression.</span></span>  
  
 <span data-ttu-id="3db21-1123">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1123">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1124">örnekte gösterildiği nasıl aşağıdaki hello toouse üst sorgu</span><span class="sxs-lookup"><span data-stu-id="3db21-1124">hello following example shows how toouse UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="3db21-1125">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1125">Here is hello result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="3db21-1126"><a name="bk_array_functions"></a>Dizi işlevleri</span><span class="sxs-lookup"><span data-stu-id="3db21-1126"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="3db21-1127">skaler işlevler aşağıdaki hello bir dizi giriş değeri ve return sayısal, Boole veya dizi değer üzerinde bir işlemi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="3db21-1127">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="3db21-1128">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="3db21-1128">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="3db21-1129">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="3db21-1129">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="3db21-1130">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="3db21-1130">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="3db21-1131">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="3db21-1131">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="3db21-1132"><a name="bk_array_concat"></a>ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="3db21-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="3db21-1133">İki veya daha fazla dizi değerlerini birleştirme hello sonucu olan bir dizi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1133">Returns an array that is hello result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="3db21-1134">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1134">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="3db21-1135">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1135">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="3db21-1136">Tüm geçerli dizi ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1136">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="3db21-1137">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1137">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1138">Bir dizi ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1138">Returns an array expression.</span></span>  
  
 <span data-ttu-id="3db21-1139">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1139">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1140">örnekte nasıl tooconcatenate iki dizi hello.</span><span class="sxs-lookup"><span data-stu-id="3db21-1140">hello following example how tooconcatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="3db21-1141">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1141">Here is hello result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="3db21-1142"><a name="bk_array_contains"></a>ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="3db21-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="3db21-1143">Belirtilen değer hello dizi hello içerip içermediğini gösteren Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1143">Returns a Boolean indicating whether hello array contains hello specified value.</span></span>  
  
 <span data-ttu-id="3db21-1144">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1144">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="3db21-1145">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1145">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="3db21-1146">Tüm geçerli dizi ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1146">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="3db21-1147">Geçerli bir ifade değil.</span><span class="sxs-lookup"><span data-stu-id="3db21-1147">Is any valid expression.</span></span>  
  
 <span data-ttu-id="3db21-1148">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1148">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1149">Bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1149">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="3db21-1150">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1150">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1151">Aşağıdaki örneğine nasıl hello toocheck ARRAY_CONTAINS kullanarak bir dizi üyelik için.</span><span class="sxs-lookup"><span data-stu-id="3db21-1151">hello following example how toocheck for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="3db21-1152">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1152">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="3db21-1153"><a name="bk_array_length"></a>ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="3db21-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="3db21-1154">Dizi ifadesi belirtilen döndürür hello hello öğelerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="3db21-1154">Returns hello number of elements of hello specified array expression.</span></span>  
  
 <span data-ttu-id="3db21-1155">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1155">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="3db21-1156">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1156">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="3db21-1157">Tüm geçerli dizi ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1157">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="3db21-1158">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1158">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1159">Sayısal ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1159">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-1160">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1160">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1161">örnek, nasıl tooget hello ARRAY_LENGTH kullanarak bir dizi uzunluğu hello.</span><span class="sxs-lookup"><span data-stu-id="3db21-1161">hello following example how tooget hello length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="3db21-1162">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1162">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="3db21-1163"><a name="bk_array_slice"></a>ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="3db21-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="3db21-1164">Bir dizi ifadesi bölümünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1164">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="3db21-1165">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1165">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="3db21-1166">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1166">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="3db21-1167">Tüm geçerli dizi ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1167">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="3db21-1168">Geçerli herhangi bir sayısal ifadeye ' dir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1168">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="3db21-1169">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1169">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1170">Bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1170">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="3db21-1171">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1171">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1172">Aşağıdaki örneğine nasıl hello tooget ARRAY_SLICE kullanarak bir dizi bir parçası.</span><span class="sxs-lookup"><span data-stu-id="3db21-1172">hello following example how tooget a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="3db21-1173">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1173">Here is hello result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="3db21-1174"><a name="bk_spatial_functions"></a>Uzamsal işlevleri</span><span class="sxs-lookup"><span data-stu-id="3db21-1174"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="3db21-1175">Merhaba aşağıdaki skaler işlevler uzamsal nesne giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir sayısal ya da Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1175">hello following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="3db21-1176">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="3db21-1176">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="3db21-1177">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="3db21-1177">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="3db21-1178">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="3db21-1178">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="3db21-1179">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="3db21-1179">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="3db21-1180">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="3db21-1180">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="3db21-1181"><a name="bk_st_distance"></a>ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="3db21-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="3db21-1182">Merhaba iki GeoJSON noktası, çokgen veya LineString ifadeleri arasında Hello uzaklığını döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1182">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="3db21-1183">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1183">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="3db21-1184">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1184">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="3db21-1185">Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1185">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="3db21-1186">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1186">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1187">Başlangıç uzaklığı içeren sayısal bir ifade döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1187">Returns a numeric expression containing hello distance.</span></span> <span data-ttu-id="3db21-1188">Bu ölçümler hello varsayılan başvuru sistemi için ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1188">This is expressed in meters for hello default reference system.</span></span>  
  
 <span data-ttu-id="3db21-1189">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1189">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1190">örnekte gösterildiği nasıl aşağıdaki hello tooreturn içinde 30 km hello biri olan tüm ailesi belgeleri belirtilen hello st_dıstance yerleşik işlevi kullanarak konumu.</span><span class="sxs-lookup"><span data-stu-id="3db21-1190">hello following example shows how tooreturn all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> <span data-ttu-id="3db21-1191">.</span><span class="sxs-lookup"><span data-stu-id="3db21-1191">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="3db21-1192">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1192">Here is hello result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="3db21-1193"><a name="bk_st_within"></a>ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="3db21-1193"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="3db21-1194">Merhaba ilk bağımsız değişkeninde belirtilen hello GeoJSON nesne (noktası, çokgen veya LineString) hello ikinci bağımsız değişkeni hello GeoJSON (noktası, çokgen veya LineString) içinde olup olmadığını gösteren bir Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1194">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument is within hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="3db21-1195">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1195">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="3db21-1196">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1196">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="3db21-1197">Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="3db21-1198">Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1198">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="3db21-1199">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1199">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1200">Bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1200">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="3db21-1201">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1201">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1202">Aşağıdaki örnek hello nasıl toofind ST_WITHIN kullanarak bir Çokgen tüm ailesi belgeleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1202">hello following example shows how toofind all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="3db21-1203">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1203">Here is hello result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="3db21-1204"><a name="bk_st_intersects"></a>ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="3db21-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="3db21-1205">Merhaba ilk bağımsız değişkeninde belirtilen hello GeoJSON nesne (noktası, çokgen veya LineString) hello ikinci bağımsız değişken hello GeoJSON (noktası, çokgen veya LineString) kesiştiğinden olup olmadığını gösteren bir Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1205">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument intersects hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="3db21-1206">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1206">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="3db21-1207">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1207">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="3db21-1208">Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="3db21-1209">Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1209">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="3db21-1210">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1210">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1211">Bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1211">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="3db21-1212">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1212">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1213">örnekte gösterildiği nasıl aşağıdaki hello ile kesiştiğinden tüm alanları hello Çokgen toofind.</span><span class="sxs-lookup"><span data-stu-id="3db21-1213">hello following example shows how toofind all areas that intersects with hello given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="3db21-1214">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1214">Here is hello result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="3db21-1215"><a name="bk_st_isvalid"></a>ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="3db21-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="3db21-1216">Merhaba GeoJSON noktası, çokgen veya LineString ifadesi geçerli belirtilen olup olmadığını gösteren bir Boole değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1216">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="3db21-1217">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1217">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="3db21-1218">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1218">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="3db21-1219">Tüm geçerli GeoJSON noktası, çokgen veya LineString ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1219">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="3db21-1220">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1220">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1221">Boole ifadesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1221">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="3db21-1222">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1222">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1223">örnekte gösterildiği nasıl aşağıdaki hello bir noktası geçerliyse ST_VALID kullanarak toocheck.</span><span class="sxs-lookup"><span data-stu-id="3db21-1223">hello following example shows how toocheck if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="3db21-1224">Örneğin, bu nokta hello geçerli değerler [-90, 90] aralığında değil enlem değer içeriyor, bu nedenle hello sorgu yanlış değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1224">For example, this point has a latitude value that's not in hello valid range of values [-90, 90], so hello query returns false.</span></span>  
  
 <span data-ttu-id="3db21-1225">Çokgenler için hello hello son koordinat çifti sağlanan olması gerektiğini belirtilmesini gerektiriyor GeoJSON hello aynı hello ilk toocreate kapalı şekli.</span><span class="sxs-lookup"><span data-stu-id="3db21-1225">For polygons, hello GeoJSON specification requires that hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span> <span data-ttu-id="3db21-1226">Çokgen içindeki noktaları yönünün sırayla belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1226">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="3db21-1227">Belirtilen saat yönünde sırayla Çokgen hello bölgesinde hello tersini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3db21-1227">A polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="3db21-1228">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1228">Here is hello result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="3db21-1229"><a name="bk_st_isvaliddetailed"></a>ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="3db21-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="3db21-1230">Merhaba GeoJSON noktası, çokgen veya LineString ifade belirtilmişse bir Boole değeri içeren bir JSON değeri geçerli değil ve geçersiz, ayrıca bir dize değeri olarak neden hello döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1230">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="3db21-1231">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="3db21-1231">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="3db21-1232">**Bağımsız değişkenler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1232">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="3db21-1233">Tüm geçerli GeoJSON noktası veya Çokgen ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1233">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="3db21-1234">**Dönüş türleri**</span><span class="sxs-lookup"><span data-stu-id="3db21-1234">**Return Types**</span></span>  
  
 <span data-ttu-id="3db21-1235">Merhaba GeoJSON noktası belirtilen veya Çokgen ifadesi geçerli değil ve geçersiz, ayrıca bir dize değeri olarak neden hello bir Boole değeri içeren bir JSON değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3db21-1235">Returns a JSON value containing a Boolean value if hello specified GeoJSON point or polygon expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="3db21-1236">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="3db21-1236">**Examples**</span></span>  
  
 <span data-ttu-id="3db21-1237">Aşağıdaki örneğine nasıl hello ST_ISVALIDDETAILED kullanarak toocheck geçerlilik (ayrıntılarla ile).</span><span class="sxs-lookup"><span data-stu-id="3db21-1237">hello following example how toocheck validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="3db21-1238">Merhaba sonuç kümesini burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3db21-1238">Here is hello result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="3db21-1239">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3db21-1239">Next steps</span></span>  
 <span data-ttu-id="3db21-1240">[SQL söz dizimi ve Azure Cosmos DB SQL sorgusu](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="3db21-1240">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="3db21-1241">Azure Cosmos DB belgeleri</span><span class="sxs-lookup"><span data-stu-id="3db21-1241">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
