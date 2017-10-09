---
Başlık: aaa "Azure Cosmos DB DocumentDB API'si: SQL söz dizimi | Microsoft Docs"Açıklama: başvuru belgelerini hello Azure Cosmos DB DocumentDB API SQL sorgu dili için.
Hizmetleri: cosmos db Yazar: mimig1 Yöneticisi: jhubbard Düzenleyicisi: mimig documentationcenter: ''

MS.assetid: ms.service: cosmos db ms.workload: Veri Hizmetleri ms.tgt_pltfrm: na ms.devlang: na ms.topic: ms.date başvuru: 13/06/2017 ms.author: mimig

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a>Azure DB Cosmos DocumentDB API: SQL söz dizimi başvurusu

Hello Azure Cosmos DB DocumentDB API tanıdık SQL (yapılandırılmış sorgu dili) kullanarak belgelerin sorgulanmasını dilbilgisi gibi hiyerarşik JSON belgelerini gerektirmeden açık şema veya ikincil dizinlerin oluşturulmasını destekler. Bu konu, başvuru belgeleri hello DocumentDB API SQL sorgu dili için sağlar.

Merhaba DocumentDB API SQL sorgu dili bir anlatım için bkz: [SQL sorgularını Azure Cosmos DB DocumentDB API için](documentdb-sql-query.md).  
  
Ayrıca toovisit hello davet ediyoruz [Query Playground](http://www.documentdb.com/sql/demo) burada Azure Cosmos DB deneyin ve SQL sorgularını kümemize karşı çalıştırabilirsiniz.  
  
## <a name="select-query"></a>SEÇME sorgusu  
JSON belgeleri hello veritabanından alır. İfade değerlendirme, filtreleme tahminleri destekler ve birleştirir.  Merhaba SELECT deyimi tanımlamak için kullanılan hello kuralları hello sözdizimi kuralları bölümünde tabloda verilmiştir.  
  
**Sözdizimi**  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 **Açıklamalar**  
  
 Ayrıntılar için bölümlere her yan tümcesi aşağıdaki bakın:  
  
-   [SELECT yan tümcesi](#bk_select_query)  
  
-   [FROM yan tümcesi](#bk_from_clause)  
  
-   [WHERE yan tümcesi](#bk_where_clause)  
  
-   [ORDER BY yan tümcesi](#bk_orderby_clause)  
  
Merhaba yan tümceleri hello SELECT deyimi içinde yukarıda gösterildiği gibi sıralanmalıdır. Merhaba isteğe bağlı yan tümceleri herhangi biri atlanabilir. Ancak isteğe bağlı bir yan tümceleri kullanıldığında, hello doğru sırada görünmesi gerekir.  
  
**Merhaba SELECT deyimi mantıksal işleme sırası**  
  
yan tümceleri işlenme hello sırası şöyledir:  

1.  [FROM yan tümcesi](#bk_from_clause)  
2.  [WHERE yan tümcesi](#bk_where_clause)  
3.  [ORDER BY yan tümcesi](#bk_orderby_clause)  
4.  [SELECT yan tümcesi](#bk_select_query)  

Bu hello sözdiziminde görüntüleneceği hello sipariş farklı olduğunu unutmayın. işlenen yan tümcesi ile sunulan tüm yeni sembolleri görünür ve daha sonra işlenen yan tümcelerinde kullanılabilir gibi hello sıralama olmamasıdır. Örneğin, bir FROM yan tümcesinde bildirilen diğer adlar WHERE erişilebilir ve SELECT yan tümceleri.  

**Boşluk karakterleri ve açıklamaları**  

Tırnak içine alınan bir dizeyi bir parçası olmayan veya tanımlayıcı tırnak içine alınmış tüm boşluk karakterleri hello dil dilbilgisi parçası olmayan ve ayrıştırma sırasında yok sayılır.  

T-SQL stili yorumlar gibi Hello sorgu dili destekler  

-   SQL deyimi`-- comment text [newline]`  

Boşluk karakterleri ve açıklamalar herhangi anlamlı hello dilbilgisi değil olmakla birlikte, kullanılan tooseparate belirteçleri olmaları gerekir. Örneğin: `-1e5` bir tek sayı belirteç süre olan`: – 1 e5` eksi bir belirteç numarası 1 ve tanımlayıcı e5 tarafından izlenir.  

##  <a name="bk_select_query"></a>SELECT yan tümcesi  
Merhaba yan tümceleri hello SELECT deyimi içinde yukarıda gösterildiği gibi sıralanmalıdır. Merhaba isteğe bağlı yan tümceleri herhangi biri atlanabilir. Ancak isteğe bağlı bir yan tümceleri kullanıldığında, hello doğru sırada görünmesi gerekir.  

**Sözdizimi**  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 **Bağımsız değişkenler**  
  
 `<select_specification>`  
  
 Merhaba sonuç için seçilen özellikler veya değer toobe ayarlayın.  
  
 `'*'`  
  
Merhaba değeri hiçbir değişiklik yapmadan alınması gerektiğini belirtir. İşlenen hello değer bir nesne ise, özellikle, tüm özellikler alınır.  
  
 `<object_property_list>`  
  
Alınan özellikleri toobe Hello listesini belirtir. Her döndürülen değeri, belirtilen hello özellikleri olan bir nesne olacaktır.  
  
`VALUE`  
  
Merhaba JSON değeri hello tam JSON nesne yerine alınması gerektiğini belirtir. Bu, aksine `<property_list>` öngörülen hello değer bir nesne içinde kaymasını değil.  
  
`<scalar_expression>`  
  
Merhaba değeri toobe temsil eden ifadesi hesaplanır. Bkz: [skaler ifadelerin](#bk_scalar_expressions) ayrıntıları bölümü.  
  
**Açıklamalar**  
  
Merhaba `SELECT *` sözdizimi geçerli yalnızca tam olarak bir diğer ad belirtmiş FROM yan tümcesi varsa. `SELECT *`projeksiyon gerektiğinde yararlı olabilecek bir kimlik projeksiyon sağlar. SEÇİN * yalnızca FROM yan tümcesi belirtilirse geçerlidir ve yalnızca tek bir giriş kaynağı sunmuştur.  
  
Unutmayın `SELECT <select_list>` ve `SELECT *` "söz dizimi sugar" olduğunu ve bunun yerine aşağıda gösterildiği gibi basit SELECT deyimi kullanılarak belirtilebilir.  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     eşdeğerdir:  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     eşdeğerdir:  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
**Ayrıca bkz.**  
  
[Skaler ifade](#bk_scalar_expressions)  
[SELECT yan tümcesi](#bk_select_query)  
  
##  <a name="bk_from_clause"></a>FROM yan tümcesi  
Merhaba kaynak veya birleştirilmiş kaynakları belirtir. Merhaba FROM yan tümcesi isteğe bağlıdır. Aksi durumda belirtilen, diğer yan tümceleri hala FROM yan tümcesi tek bir belgenin sağladıysanız olarak yürütülür.  
  
**Sözdizimi**  
  
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
  
**Bağımsız değişkenler**  
  
`<from_source>`  
  
Bir veri kaynağı olan veya olmayan bir diğer ad belirtir. Diğer ad belirtilmezse, onu hello olayla `<collection_expression>` kuralları kullanarak:  
  
-   Merhaba deyim bir toplama_adı ise toplama_adı bir diğer ad olarak kullanılır.  
  
-   Merhaba ifade ise `<collection_expression>`, property_name sonra property_name bir diğer ad olarak kullanılır. Merhaba deyim bir toplama_adı ise toplama_adı bir diğer ad olarak kullanılır.  
  
OLARAK`input_alias`  
  
Bu hello belirtir `input_alias` Toplama ifadesi temel hello tarafından döndürülen değerler kümesidir.  
 
`input_alias`IN  
  
Bu hello belirtir `input_alias` Toplama ifadesi temel hello tarafından döndürülen her dizinin tüm dizi öğeleri üzerinde yineleme tarafından elde edilen değerleri hello kümesini temsil etmelidir. Dizi olmayan temel Toplama ifadesi tarafından döndürülen herhangi bir değer yok sayılır.  
  
`<collection_expression>`  
  
Merhaba Toplama ifadesi toobe kullanılan tooretrieve hello belgeler belirtir.  
  
`ROOT`  
  
Bu belge hello varsayılan, bağlı durumda koleksiyonu alınması gerektiğini belirtir.  
  
`collection_name`  
  
Bu belgede sağlanan hello koleksiyonundan alınması gerektiğini belirtir. Merhaba koleksiyonunun Hello adı şu anda bağlı hello koleksiyonunun hello adı eşleşmelidir.  
  
`input_alias`  
  
Bu belge hello alınan belirtir sağlanan hello diğer adı tarafından tanımlanan diğer kaynak.  
  
`<collection_expression> '.' property_`  
  
Bu belge hello erişerek alınabilir belirtir `property_name` özelliği veya dizi_dizini dizi öğesi tarafından alınan tüm belgeler için belirtilen toplama ifadesi.  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
Bu belge hello erişerek alınabilir belirtir `property_name` özelliği veya dizi_dizini dizi öğesi tarafından alınan tüm belgeler için belirtilen toplama ifadesi.  
  
**Açıklamalar**  
  
Tüm diğer adlar sağlanan veya hello çıkarımı yapılan `<from_source>(`s) benzersiz olması gerekir. Merhaba sözdizimi `<collection_expression>.`property_name aynı hello olduğu `<collection_expression>' ['"property_name"']'`. Ancak, bir özellik adı tanımlayıcısı dışı karakterler içeriyorsa hello ikinci sözdizimi kullanılabilir.  
  
**Dizi öğeleri eksik özellikleri eksik değerleri işleme tanımlanmamış**  
  
Bir toplama ifadesi özellikleri veya dizi öğeleri ve değer yok erişirse, bu değeri göz ardı ve daha fazla işlenmedi.  
  
**Toplama ifadesi içerik kapsamı**  
  
Bir toplama ifadesi koleksiyonu kapsamlı veya belge kapsamlı olabilir:  
  
-   Koleksiyon kapsamlı bir ifade, hello hello toplama ifadesinin temel alınan kaynak ya da kök ise veya `collection_name`. Bu tür bir ifade hello koleksiyonundan doğrudan alınan belgeleri kümesini temsil eder ve diğer toplama ifadeleri hello işlenmesini bağımlı değildir.  
  
-   Belge kapsamlı bir ifade, hello hello toplama ifadesinin temel alınan kaynak `input_alias` önceki hello sorguda sunmuştur. Bu tür bir ifade hello diğer koleksiyonuyla ilişkilendirilen toohello kümesi ait her bir belgenin hello kapsamında hello toplama ifadesinin hesaplanmasıyla elde belgeleri kümesini temsil eder.  Merhaba sonuç kümesi her kümesi temel hello hello belgelerde hello toplama ifadesinin hesaplanmasıyla elde edilen kümeleri birleşim olacaktır.  
  
**Birleşimler**  
  
Merhaba geçerli sürümde, Azure Cosmos DB iç birleştirmeler destekler. Ek birleştirme özellikleri yeni çıkacak.

İç birleşimler sonuçlanır eksiksiz bir çapraz ürün hello hello birleştirme katılan ayarlar. Merhaba bir N yönlü birleştirme burada hello tanımlama grubu içindeki her değerin katılan hello birleştirme ayarlamak hello diğer adı ile ilişkili ve söz konusu diğer ad diğer yan tümcelerinde başvurarak erişilen N-öğe başlık kümesi sonucudur.  
  
Merhaba değerlendirme hello birleştirme hello bağlam kapsamına kümeleri katılan hello bağlıdır:  
  
-  Bir birleştirme arasında koleksiyon kümesi A ve koleksiyon kapsamlı B, A ve b kümelerindeki tüm öğelerin çapraz ürün sonuçları ayarlayın
  
-   Tüm ayarlar her belge için B A. belge kapsamlı ayarlama değerlendirerek elde birleşimi sonuçlanıyor kümesi belge kapsamlı kümesi B arasındaki bir birleştirme  
  
 Merhaba geçerli sürümde, en fazla bir koleksiyon kapsamlı ifade hello Sorgu işlemcisi tarafından desteklenir.  
  
**Birleştirme örnekleri:**  
  
FROM yan tümcesi aşağıdaki hello bakalım:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`  
  
 Tanımlamak her kaynak izin `input_alias1, input_alias2, …, input_aliasN`. Bu FROM yan tümcesi N-diziler (tuple N değerlerle) kümesini döndürür. Her tanımlama grubu tüm koleksiyon diğer adları kendi ilgili ayarlar yineleme tarafından üretilen değerler içeriyor.  
  
*Örnek 1, 2 kaynaklarıyla KATIL:*  
  
- Let `<from_source1>` koleksiyonu kapsamlı ve kümesi {A, B, C} temsil eder.  
  
- Let `<from_source2>` input_alias1 başvuran belge kapsamlı ve ayarlar temsil eder:  
  
    {1, 2} için`input_alias1 = A,`  
  
    için {3}`input_alias1 = B,`  
  
    {4, 5} için`input_alias1 = C,`  
  
- Merhaba FROM yan tümcesi `<from_source1> JOIN <from_source2>` diziler aşağıdaki hello neden olur:  
  
    (`input_alias1, input_alias2`):  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
*Örnek 2, 3 kaynaklarıyla KATIL:*  
  
- Let `<from_source1>` koleksiyonu kapsamlı ve kümesi {A, B, C} temsil eder.  
  
- Let `<from_source2>` belge kapsamlı başvuran olması `input_alias1` ve ayarlar temsil eder:  
  
    {1, 2} için`input_alias1 = A,`  
  
    için {3}`input_alias1 = B,`  
  
    {4, 5} için`input_alias1 = C,`  
  
- Let `<from_source3>` belge kapsamlı başvuran olması `input_alias2` ve ayarlar temsil eder:  
  
    {100, 200} için`input_alias2 = 1,`  
  
    {300} için`input_alias2 = 3,`  
  
- Merhaba FROM yan tümcesi `<from_source1> JOIN <from_source2> JOIN <from_source3>` diziler aşağıdaki hello neden olur:  
  
    (input_alias1, input_alias2, input_alias3):  
  
    (A, 1, 100), (A, 1, 200), (B, 3, 300)  
  
> [!NOTE]
> Diğer değerler için diziler eksikliği `input_alias1`, `input_alias2`, hangi hello için `<from_source3>` hiçbir değer döndürmedi.  
  
*Örnek 3, 3 kaynaklarıyla KATIL:*  
  
- < Koleksiyon kapsamlı ve {A, B, C} kümesini temsil eden from_source1 > olanak tanır.  
  
- Let `<from_source1>` koleksiyonu kapsamlı ve kümesi {A, B, C} temsil eder.  
  
- < Belge kapsamlı başvuru input_alias1 olması ve ayarlar temsil from_source2 > sağlar:  
  
    {1, 2} için`input_alias1 = A,`  
  
    için {3}`input_alias1 = B,`  
  
    {4, 5} için`input_alias1 = C,`  
  
- Let `<from_source3>` kapsamlı çok`input_alias1` ve ayarlar temsil eder:  
  
    {100, 200} için`input_alias2 = A,`  
  
    {300} için`input_alias2 = C,`  
  
- Merhaba FROM yan tümcesi `<from_source1> JOIN <from_source2> JOIN <from_source3>` diziler aşağıdaki hello neden olur:  
  
    (`input_alias1, input_alias2, input_alias3`):  
  
    (A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200), (C, 4, 300) (C, 5, 300)  
  
> [!NOTE]
> Bu arasında çapraz ürün ile sonuçlandı `<from_source2>` ve `<from_source3>` her ikisi de kapsamlı toohello olduğundan aynı `<from_source1>`.  Bu 4 (2 x 2) sonuçlandı diziler değerini 0 diziler B (1 x 0) değeri sahip olması ve 2 (2 x 1) değeri C. diziler  
  
**Ayrıca bkz.**  
  
 [SELECT yan tümcesi](#bk_select_query)  
  
##  <a name="bk_where_clause"></a>WHERE yan tümcesi  
 Merhaba sorgu tarafından döndürülen hello belgeler için Hello arama koşulu belirtir.  
  
 **Sözdizimi**  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 **Bağımsız değişkenler**  
  
-   `<filter_condition>`  
  
     Döndürülen hello belgeleri toobe için karşılanıp hello koşulu toobe belirtir.  
  
-   `<scalar_expression>`  
  
     Merhaba değeri toobe temsil eden ifadesi hesaplanır. Merhaba bkz [skaler ifadelerin](#bk_scalar_expressions) ayrıntıları bölümü.  
  
 **Açıklamalar**  
  
 Merhaba sırayla filtre koşulu tootrue değerlendirilmelidir olarak belirtilen bir ifade belge toobe döndürdü. Boole değeri true hello koşul, başka bir değer yerine getirecek yalnızca: tanımlanmamış, null, false, sayı, dizi veya nesne uygun olmadığı hello koşulu.  
  
##  <a name="bk_orderby_clause"></a>ORDER BY yan tümcesi  
 Merhaba sorgu tarafından döndürülen sonuçları için sıralama hello belirtir.  
  
 **Sözdizimi**  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 **Bağımsız değişkenler**  
  
-   `<sort_specification>`  
  
     Bir özellik veya üzerinde toosort hello sorgu sonuç kümesini ifade belirtir. Sıralama sütunu adı veya sütun diğer adı belirtilebilir.  
  
     Birden çok sütunları sıralama belirtilebilir. Sütun adları benzersiz olmalıdır. Merhaba hello ORDER BY yan tümcesinde sütunları sıralama Hello sırasını hello kuruluş sıralanmış hello sonuç kümesinin tanımlar. Diğer bir deyişle, hello sonuç kümesi hello ilk özelliği tarafından sıralanır ve o sıralı liste hello ikinci özelliği ve benzeri sonra sıralanır.  
  
     Merhaba ORDER BY yan tümcesinde başvurulan hello sütun adları hello bir sütunda herhangi belirsizlikleri olmadan hello FROM yan tümcesinde belirtilen bir tabloda tanımlanan liste veya tooa sütun seçin tooeither karşılık gelmelidir.  
  
-   `<sort_expression>`  
  
     Hangi toosort hello sorgu sonuç kümesinde tek bir özellik veya ifadeyi belirtir.  
  
-   `<scalar_expression>`  
  
     Merhaba bkz [skaler ifadelerin](#bk_scalar_expressions) ayrıntıları bölümü.  
  
-   `ASC | DESC`  
  
     Merhaba Belirtilen sütundaki Hello değerleri artan veya azalan sırada sıralanması gerektiğini belirtir. ASC hello en düşük değer toohighest değerinden sıralar. DESC en yüksek değer toolowest değerinden sıralar. ASC hello varsayılan sıralama düzeni ' dir. Null değerler hello düşük olası değerler kabul edilir.  
  
 **Açıklamalar**  
  
 Merhaba sorgu dilbilgisi özellikleri tarafından birden çok sipariş desteklerken, yalnızca tek bir özellik, yalnızca adlarla ve özellik adları, yani, hesaplanan özellikleri karşı sıralama hello Azure Cosmos DB sorgu çalışma zamanı destekler. Sıralama de gerektirir dizin oluşturma ilkesi o hello içerir hello özelliği ve belirtilen hello için bir aralığı dizin türüyle hello en yüksek duyarlık. Dizin oluşturma ilkesi belgeleri daha fazla ayrıntı için toohello bakın.  
  
##  <a name="bk_scalar_expressions"></a>Skaler ifade  
 Skaler bir ifade simge birleşiminden oluşur ve tooobtain tek bir değer olabilir işleçleri değerlendirilir. Basit ifadeler sabitler, özellik başvuruları, dizi öğesi başvuruları, diğer başvurular veya işlev çağrılarını olabilir. Basit ifadeler işleçleri kullanarak karmaşık ifadelere birleştirilebilir.  
  
 Hangi skaler ifade olabilir değerleri hakkında daha fazla bilgi için bkz: [sabitleri](#bk_constants) bölümü.  
  
 **Sözdizimi**  
  
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
  
 **Bağımsız değişkenler**  
  
-   `<constant>`  
  
     Sabit bir değeri temsil eder. Bkz: [sabitleri](#bk_constants) ayrıntıları bölümü.  
  
-   `input_alias`  
  
     Merhaba tarafından tanımlanan bir değeri temsil `input_alias` hello sunulan `FROM` yan tümcesi.  
    Bu değer toonot garanti olması **tanımsız** –**tanımsız** hello giriş değerleri atlanır.  
  
-   `<scalar_expression>.property_name`  
  
     Bir nesnenin hello özelliğinin değerini temsil eder. Merhaba özelliği mevcut değil veya özellik bir nesne olmayan bir değer başvurulan durumunda hello ifadeyi hesaplar çok**tanımsız** değeri.  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     Adında hello özellik değerini temsil eder `property_name` veya dizi öğesi dizine sahip `array_index` nesne/dizisi. Merhaba özelliği/dizi dizini yok veya hello özelliği/dizi dizini bir nesne/dizisi olmayan bir değer başvuruluyor, hello ifadeyi tooundefined değeri hesaplar.  
  
-   `unary_operator <scalar_expression>`  
  
     Tek değere uygulanan tooa olan işleç bir temsil eder. Bkz: [işleçleri](#bk_operators) ayrıntıları bölümü.  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     Uygulanan tootwo değerleri bir işleç temsil eder. Bkz: [işleçleri](#bk_operators) ayrıntıları bölümü.  
  
-   `<scalar_function_expression>`  
  
     İşlev çağrısının sonucunu tarafından tanımlanan bir değeri temsil eder.  
  
-   `udf_scalar_function`  
  
     Merhaba kullanıcının adını skaler işlev tanımlı.  
  
-   `builtin_scalar_function`  
  
     Merhaba yerleşik skaler işlev adı.  
  
-   `<create_object_expression>`  
  
     Belirtilen özelliklere sahip yeni bir nesne oluşturarak alınan bir değer ve bunların değerleri temsil eder.  
  
-   `<create_array_expression>`  
  
     Öğeleri olarak belirtilen değerlerle yeni bir dizi oluşturarak elde bir değeri temsil eder  
  
-   `parameter_name`  
  
     Merhaba belirtilen parametre adı değerini temsil eder. Parametre adları @ tek bir hello ilk karakteri olarak olması gerekir.  
  
 **Açıklamalar**  
  
 Bir yerleşik veya kullanıcı çağırma skaler işlev tanımlandığında tüm bağımsız değişkenler tanımlanması gerekir. Hello bağımsız değişkenlerden biri tanımsız hello işlev çağrılmaz ve hello sonucu tanımsız olacaktır.  
  
 Bir nesne oluştururken, Tanımsız değer atanmış herhangi bir özelliği atlandı ve nesne oluşturulan hello dahil değil.  
  
 Ne zaman herhangi bir öğeyi değer bir dizi oluşturma atanmış **tanımsız** değeri atlandı ve oluşturulan hello nesnesinde dahil değildir. Bu sonraki tanımlanan hello öğesi tootake onun yerine neden olacak şekilde, oluşturulan hello dizi dizinleri atlandı değil.  
  
##  <a name="bk_operators"></a>İşleçler  
 Bu bölümde desteklenen hello işleçleri açıklanmaktadır. Her işleç atanan tooexactly bir kategori olabilir.  
  
 Bkz: **işleci kategorileri** Ayrıntılar için aşağıdaki tabloya işlenmesi ile ilgili **tanımsız** değerleri, giriş değerleri ve işleme türlerini eşleşmeyen ile değerlerin türü gereksinimleri.  
  
 **İşleç kategoriler:**  
  
|**Kategori**|**Ayrıntılar**|  
|-|-|  
|**aritmetik**|İşleç bekliyor input(s) toobe numaraları. Çıktı ayrıca bir sayıdır. Merhaba girdi ise **tanımsız** veya numarası sonra hello sonuç dışında türüdür **tanımsız**.|  
|**bit tabanlı**|İşleç bekliyor input(s) toobe 32-bit işaretli tamsayıyı numaraları. Çıktı da 32 bit imzalı numarası tamsayıdır.<br /><br /> Herhangi bir tamsayı olmayan değer yuvarlanır. Pozitif bir değer yuvarlanacağı, negatif değerleri yuvarlanan.<br /><br /> Merhaba 32 bit tamsayı aralığın dışında herhangi bir değer, son 32 bitlik, iki kişinin tamamlama gösterimi gerçekleştirerek dönüştürülür.<br /><br /> Merhaba girdi ise **tanımsız** hello sonuç ise diğer, sayıdan yazın veya **tanımsız**.<br /><br /> **Not:** hello davranışı üzerinde JavaScript bit düzeyinde işleci davranışı ile uyumludur.|  
|**mantıksal**|İşleç bekliyor input(s) toobe Boolean(s). Çıktı de bir Boole değeri olur.<br />Merhaba girdi ise **tanımsız** hello sonucu olacaktır sonra Boolean, diğerinden yazın veya **tanımsız**.|  
|**Karşılaştırma**|İşleç bekliyor input(s) aynı yazın ve tanımsız olmaması toohave hello. Çıktı bir Boole değeri değil.<br /><br /> Merhaba girdi ise **tanımsız** veya hello girişleri farklı türlerine sahip ardından hello sonuç **tanımsız**.<br /><br /> Bkz: **karşılaştırma için değerlerin sıralama** ayrıntıları sıralama değeri için tablo.|  
|**dize**|İşleç bekliyor input(s) toobe dizelerini. Çıktı ayrıca bir dizedir.<br />Merhaba girdi ise **tanımsız** veya dize sonra hello sonuç dışında türüdür **tanımsız**.|  
  
 **Birli işleçleri:**  
  
|**Ad**|**İşleci**|**Ayrıntılar**|  
|-|-|-|  
|**aritmetik**|+<br /><br /> -|Merhaba sayı değeri döndürür.<br /><br /> Bit tabanlı değil işlecini. Sayı değeri tasarruflarını döndürür.|  
|**bit tabanlı**|~|Olanları tamamlama. Tamamlama sayı değeri döndürür.|  
|**Mantıksal**|**DEĞİL**|Değilleme. Boole değeri döndürür tasarruflarını.|  
  
 **İkili işleçler:**  
  
|**Ad**|**İşleci**|**Ayrıntılar**|  
|-|-|-|  
|**aritmetik**|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|Ayrıca.<br /><br /> Çıkarma.<br /><br /> Çarpma.<br /><br /> Bölme.<br /><br /> Modülasyon.|  
|**bit tabanlı**|&#124;<br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|Bit düzeyinde OR.<br /><br /> Bit düzeyinde and<br /><br /> Bit düzeyinde XOR.<br /><br /> Sola kaydırma.<br /><br /> Sağa kaydırma.<br /><br /> Sıfır dolgu sağa kaydırma.|  
|**mantıksal**|**VE**<br /><br /> **VEYA**|Mantıksal ve işlecini. Döndürür **true** iki bağımsız değişkenler ise **true**, döndürür **false** Aksi takdirde.<br /><br /> Mantıksal ve işlecini. Döndürür **true** iki bağımsız değişkenler ise **true**, döndürür **false** Aksi takdirde.|  
|**Karşılaştırma**|**=**<br /><br /> **!=, <>**<br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> **??**|Eşittir. Döndürür **true** bağımsız değişkenleri eşit olup olmadığını döndürür **false** Aksi takdirde.<br /><br /> Eşit değil. Döndürür **true** bağımsız değişkenleri eşit değilse döndürür **false** Aksi takdirde.<br /><br /> Büyüktür. Döndürür **true** ilk bağımsız değişken ikinci bir hello büyükse, dönüş **false** Aksi takdirde.<br /><br /> Büyüktür veya eşittir. Döndürür **true** ilk bağımsız değişken ikinci toohello eşit veya değerinden daha büyük olursa döndürür **false** Aksi takdirde.<br /><br /> Küçüktür. Döndürür **true** ilk bağımsız değişken ikinci bir hello daha az ise, döndürür **false** Aksi takdirde.<br /><br /> Küçük veya eşittir. Döndürür **true** ilk bağımsız değişken küçük veya buna eşit olması durumunda toohello ikinci bir dönüş **false** Aksi takdirde.<br /><br /> Birleşim. Merhaba ilk bağımsız değişkeni ise döndürür hello ikinci bağımsız değişkeni bir **tanımsız** değeri.|  
|**Dize**|**&#124;&#124;**|Birleştirme. Her iki değişken birleşimini döndürür.|  
  
 **Üçlü işleçler:**  
  
|Üçlü işleci|?|Merhaba ilk bağımsız değişkeni çok değerlendirilirse döndürür hello ikinci bağımsız değişken**true**; hello üçüncü bağımsız değişken yoksa döndürür.|  
|-|-|-|  
  
 **Karşılaştırma için değerlerin sıralama**  
  
|**Tür**|**Değerleri sırası**|  
|-|-|  
|**Tanımlanmamış**|Karşılaştırılabilir değil.|  
|**Null**|Tek değer: **null**|  
|**Sayı**|Doğal bir gerçek sayı.<br /><br /> Negatif sonsuz değerle diğer sayı değeri küçüktür.<br /><br /> Pozitif sonsuz değerle diğer numara değerden daha büyük. **NaN** değeri karşılaştırılabilir değil. İle karşılaştırma **NaN** sonuçlanır **tanımsız** değeri.|  
|**Dize**|Lexicographical sırası.|  
|**Dizi**|Yoktur, ancak Tarafsız sıralaması.|  
|**Nesne**|Yoktur, ancak Tarafsız sıralaması.|  
  
 **Açıklamalar**  
  
 Gerçekte hello veritabanından alınan kadar Azure Cosmos DB'de değerlerin hello türleri bilinen genellikle değil. Sipariş toosupport verimli yürütme sorgularının, hello işleçleri çoğunu sıkı tür gereksinimleri vardır. Ayrıca kendilerini işleçleriyle örtük dönüşümler gerçekleştirmeyin.  
  
 Bu sorguda ister anlamına gelir: seçin * gelen kök r WHERE r.Age = 21 yalnızca özelliği geçerlilik süresi eşit toohello sayı 21 belgelerle döndürür. Belgeleri özelliği geçerlilik süresi eşit toohello "21" veya hello dize "0021" ile eşleşmez, "21" Merhaba ifade olarak = 21 tooundefined değerlendirir. Bu dizinleri, daha iyi kullanımı için çünkü sağlar hello arama belirli bir değerin (yani 21 sayı) (yani numarası 21 veya dizeler "21", "021", "21.0"...) olası eşleşmeler sonsuz sayıda ara daha hızlıdır. Bu, JavaScript farklı türlerde değerler işleçlerini nasıl değerlendirir alanından farklıdır.  
  
 **Diziler ve nesneleri eşitlik ve karşılaştırma**  
  
 Aralık işleçleri kullanarak dizi veya nesne değerleri karşılaştırma (>, > =, <, < =) üzerinde nesne ya da dizi değerleri tanımlanan sırasını değil olarak tanımlanmamış sonuçlanır. Ancak eşitlik/eşitsizlik işleçlerini kullanma (=,! =, <>) desteklenir ve değerleri karşılaştırılabilir yapısal olarak.  
  
 Diziler, her iki diziler aynı sayıda öğe varsa ve konumlarını eşleşen adresindeki öğeleri de eşit eşit. Öğe çiftleri karşılaştırma dizi karşılaştırma tanımlanmamış, hello sonucunda sonuçlanırsa tanımlanmamıştır.  
  
 Her iki nesne tanımlanan aynı özelliklere sahipse ve Özellikler eşleşen değerleri de aynıysa eşit nesneleridir. Özellik değerlerinin herhangi bir çifti karşılaştırma nesne karşılaştırma tanımlanmamış, hello sonucunda sonuçlanırsa tanımlanmamıştır.  
  
##  <a name="bk_constants"></a>Sabitleri  
 Bir sabit olarak da bilinen bir hazır değer veya bir skaler değere belirli veri değeri temsil eden bir simge ' dir. bir sabit Hello biçimi temsil ettiği hello değerinin veri türüne hello bağlıdır.  
  
 **Skaler veri türleri desteklenir:**  
  
|**Tür**|**Değerleri sırası**|  
|-|-|  
|**Tanımlanmamış**|Tek değer: **tanımlanmamış**|  
|**Null**|Tek değer: **null**|  
|**Boole değeri**|Değerler: **false**, **doğru**.|  
|**Sayı**|Çift duyarlıklı kayan noktalı sayı, standart IEEE 754.|  
|**Dize**|Sıfır veya daha fazla Unicode karakter dizisi. Dizeleri tek veya çift tırnak içine alınmalıdır.|  
|**Dizi**|Sıfır veya daha fazla öğeleri dizisi. Her öğe tanımlanmamış dışında herhangi bir skaler veri türü değeri olabilir.|  
|**Nesne**|Sırasız bir sıfır veya daha fazla ad/değer çiftleri kümesi. Adı bir UNICODE dizesi, değeri dışında herhangi bir skaler veri türde olabilir **tanımlanmamış**.|  
  
 **Sözdizimi**  
  
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
  
 **Bağımsız değişkenler**  
  
1.  `<undefined_constant>; undefined`  
  
     Türü tanımlanmamış değeri tanımsız temsil eder.  
  
2.  `<null_constant>; null`  
  
     Temsil eden **null** türü değeri **Null**.  
  
3.  `<boolean_constant>`  
  
     Boolean türünde sabiti temsil eder.  
  
4.  `false`  
  
     Temsil eden **yanlış** türü Boolean değeri.  
  
5.  `true`  
  
     Temsil eden **true** türü Boolean değeri.  
  
6.  `<number_constant>`  
  
     Bir sabiti temsil eder.  
  
7.  `decimal_literal`  
  
     Ondalık değişmez değerleri ondalık sayı veya bilimsel gösterim kullanılarak temsil numaralarıdır.  
  
8.  `hexadecimal_literal`  
  
     Onaltılık değişmez değerler, önek '0 x bir veya daha fazla onaltılık basamak ile izlenen' kullanılarak temsil numaralarıdır.  
  
9. `<string_constant>`  
  
     Dize türünde bir sabiti temsil eder.  
  
10. `string _literal`  
  
     Dize değişmez değerleri, sıfır veya daha fazla Unicode karakter dizisi veya kaçış sıraları tarafından temsil edilen Unicode dizelerdir. Dize değişmez değerleri tek tırnak içine alınmış (kesme işareti: ') veya çift tırnak (tırnak işareti: ").  
  
 Aşağıdaki kaçış sıralarına izin vermesi:  
  
|**Kaçış sırası**|**Açıklama**|**Unicode karakter**|  
|-|-|-|  
|\\'|kesme işareti (')|U + 0027|  
|\\"|tırnak işareti (")|U + 0022|  
|\\\|Ters solidus (\\)|U + 005C|  
|\\/|solidus (/)|U + 002F|  
|\b|Geri Al|U + 0008|  
|\f|sonraki sayfaya geçme|U + 000C|  
|\n|satır besleme|U + 000A|  
|\r|satır başı|U + 000D|  
|\t|Sekmesi|U + 0009|  
|\uXXXX|4 onaltılık basamak tarafından tanımlanan bir Unicode karakter.|U + XXXX|  
  
##  <a name="bk_query_perf_guidelines"></a>Sorgu performans kuralları  
 Verimli bir şekilde büyük bir koleksiyon için yürütülen bir sorgu toobe için sırayla bir veya daha fazla dizinleri sunulan filtreleri kullanmanız gerekir.  
  
 Dizin arama için filtreleri aşağıdaki hello kabul edilir:  
  
-   Eşitlik işleci (=), bir belge yol ifadesi ve bir sabit ile kullanın.  
  
-   Aralık işleçleri kullanın (<, \<=, >, > =) bir belge yol ifadesi ve sayı sabitleri.  
  
-   Belge yol ifadesi sabit bir yol başvurulan hello veritabanı koleksiyonundan hello belgelerdeki tanımlayan herhangi bir ifade gösterir.  
  
 **Belge yol ifadesi**  
  
 Belge yol ifadelerini ifadeleri, özelliği veya dizi dizin oluşturucu assessors veritabanı koleksiyon belgelerden gelen bir belge üzerinden yolu. Bu yol hello veritabanı koleksiyonundaki hello belgelerde doğrudan bir filtrede başvurulan değerleri kullanılan tooidentify hello konumu olabilir.  
  
 Bir ifade toobe için bir belge yol ifadesi olarak kabul edilmelidir:  
  
1.  Başvuru hello koleksiyonu kök doğrudan.  
  
2.  Bazı belge yol ifadesi başvuru özelliği ya da sabiti dizi Oluşturucusu  
  
3.  Bazı belge yol ifadesi temsil eden bir diğer ad başvuru.  
  
     **Sözdizimi kuralları**  
  
     Aşağıdaki tablonun hello hello kullanılan kuralları toodescribe sözdizimi hello DocumentDB API sorgu dili başvurusu açıklar.  
  
    |**Kuralı**|**İçin kullanılır**|  
    |-|-|    
    |BÜYÜK HARF|Büyük küçük harf duyarlı anahtar sözcükler.|  
    |küçük harf|Büyük küçük harfe duyarlı anahtar sözcükler.|  
    |\<nonterminal >|Terminal dışı, ayrı olarak tanımlı.|  
    |\<nonterminal >:: =|Merhaba nonterminal sözdizimi tanımı.|  
    |other_terminal|Sözcük içindeki ayrıntısı açıklanan Terminal (belirteç).|  
    |Tanımlayıcı|Tanımlayıcı. Aşağıdaki karakterleri yalnızca sağlar: a-z A-Z 0-9 _First karakter, bir sayı olamaz.|  
    |"dize"|Tırnak işaretli dizesi. Geçerli bir dize verir. Bir string_literal açıklamasına bakın.|  
    |'simgesi'|Merhaba sözdizimi parçası olan değişmez değer simge.|  
    |&#124; (dikey çubuk)|Alternatifleri sözdizimi öğeleri için. Belirtilen hello öğeleri yalnızca birini kullanabilirsiniz.|  
    |[] /(brackets)|Köşeli bir veya daha fazla isteğe bağlı öğeleri kapatın.|  
    |[,.. .n]|Öğesini önceki hello yinelenen n kaç kez uygulanıp uygulanamayacağını gösterir. Merhaba oluşum virgülle ayrılır.|  
    |[.. .n]|Öğesini önceki hello yinelenen n kaç kez uygulanıp uygulanamayacağını gösterir. Merhaba oluşum boşlukla ayrılır.|  
  
##  <a name="bk_built_in_functions"></a>Yerleşik işlevler  
 Azure Cosmos DB birçok yerleşik SQL işlevleri sağlar. Yerleşik işlev Hello kategorileri aşağıda listelenmiştir.  
  
|İşlevi|Açıklama|  
|--------------|-----------------|  
|[Matematik işlevleri](#bk_mathematical_functions)|Merhaba matematik işlevleri her genellikle, bağımsız değişken olarak sağlanır ve sayısal bir değeri döndürme giriş değerlerine göre bir hesaplama gerçekleştirir.|  
|[Denetimi işlevleri yazın](#bk_type_checking_functions)|Merhaba tür denetimi işlevleri içinde SQL sorguları ifade toocheck hello türü izin verin.|  
|[Dize işlevleri](#bk_string_functions)|Merhaba dize işlevleri dizesi giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir dize, sayısal ya da Boole değeri döndürür.|  
|[Dizi işlevleri](#bk_array_functions)|Merhaba dizi işlevleri bir Boole değeri veya dizi değeri, bir dizi giriş değeri ve return sayısal işlem gerçekleştirir.|  
|[Uzamsal işlevleri](#bk_spatial_functions)|Merhaba uzamsal işlevleri uzamsal nesne giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir sayısal ya da Boole değeri döndürür.|  
  
###  <a name="bk_mathematical_functions"></a>Matematik işlevleri  
 Merhaba aşağıdaki işlevleri genellikle, bağımsız değişken olarak sağlanır ve sayısal bir değeri döndürme giriş değerlerine göre bir hesaplama gerçekleştirir.  
  
||||  
|-|-|-|  
|[ABS](#bk_abs)|[ACOS](#bk_acos)|[ASIN](#bk_asin)|  
|[ATAN](#bk_atan)|[ATN2](#bk_atn2)|[TAVAN](#bk_ceiling)|  
|[COS](#bk_cos)|[COT](#bk_cot)|[DERECE](#bk_degrees)|  
|[EXP](#bk_exp)|[KAT](#bk_floor)|[GÜNLÜK](#bk_log)|  
|[LOG10](#bk_log10)|[PI](#bk_pi)|[GÜÇ](#bk_power)|  
|[RADYAN CİNSİNDEN](#bk_radians)|[YUVARLAK](#bk_round)|[SIN](#bk_sin)|  
|[SQRT](#bk_sqrt)|[KARE](#bk_square)|[OTURUM](#bk_sign)|  
|[TAN](#bk_tan)|[TRUNC](#bk_trunc)||  
  
####  <a name="bk_abs"></a>ABS  
 Sayısal ifade döndürür hello mutlak (pozitif) değerini hello belirtildi.  
  
 **Sözdizimi**  
  
```  
ABS (<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek üç farklı numaralarında hello ABS işlevi kullanılarak hello sonuçlarını gösterir.  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <a name="bk_acos"></a>ACOS  
 Kosinüsü belirtilen sayısal ifade hello radyan cinsinden döndürür hello açı; arccosine olarak da bilinir.  
  
 **Sözdizimi**  
  
```  
ACOS(<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek hello ACOS-1 döndürür.  
  
```  
SELECT ACOS(-1)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_asin"></a>ASIN  
 Döndürür hello açının sinüsü hello olduğundan, sayısal ifade radyan cinsinden. Bu arksinüsünü olarak da adlandırılır.  
  
 **Sözdizimi**  
  
```  
ASIN(<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek hello ASIN-1 döndürür.  
  
```  
SELECT ASIN(-1)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <a name="bk_atan"></a>ATAN  
 Döndürür hello açının tanjantı hello olduğundan, sayısal ifade radyan cinsinden. Bu arktanjantını olarak da adlandırılır.  
  
 **Sözdizimi**  
  
```  
ATAN(<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Aşağıdaki döndürür hello ATAN hello örneğine hello değer belirtildi.  
  
```  
SELECT ATAN(-45.01)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <a name="bk_atn2"></a>ATN2  
 Merhaba asıl hello Ark radyan cinsinden ifade edilen tanjantı y / x değerini döndürür.  
  
 **Sözdizimi**  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek hesaplar hello ATN2 belirtilen hello için x ve y bileşenleri.  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <a name="bk_ceiling"></a>TAVAN  
 En küçük tamsayı değeri büyük hello veya belirtilen sayısal ifade hello eşit verir.  
  
 **Sözdizimi**  
  
```  
CEILING (<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 TAVAN işlevi sıfır değerleri ile Merhaba ve pozitif sayısal, negatif aşağıdaki örneğine hello gösterir.  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <a name="bk_cos"></a>COS  
 Döndürür hello trigonometrik kosinüsünü hello radyan cinsinden açı, hello ifade belirtildi.  
  
 **Sözdizimi**  
  
```  
COS(<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Aşağıdaki örnek hello hello Merhaba açı belirtilen COS hesaplar.  
  
```  
SELECT COS(14.78)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <a name="bk_cot"></a>COT  
 Döndürür hello trigonometrik kotanjantını hello radyan cinsinden açı, hello sayısal ifade belirtildi.  
  
 **Sözdizimi**  
  
```  
COT(<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Aşağıdaki örnek hello hello hello belirtilen açının COT hesaplar.  
  
```  
SELECT COT(124.1332)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <a name="bk_degrees"></a>DERECE  
 Karşılık gelen açıyı radyan cinsinden açı için derece cinsinden döndürür hello.  
  
 **Sözdizimi**  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek hello sayısını derece, PI/2 radyan cinsinden açı döndürür.  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": 90}]  
```  
  
####  <a name="bk_floor"></a>KAT  
 Daha az Hello en büyük tamsayıyı döndürür veya bu değere eşit toohello sayısal ifade belirtildi.  
  
 **Sözdizimi**  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 FLOOR işlevi sıfır değerleri ile Merhaba ve pozitif sayısal, negatif aşağıdaki örneğine hello gösterir.  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <a name="bk_exp"></a>EXP  
 Merhaba, hello üstel değer döndüren sayısal ifade belirtildi.  
  
 **Sözdizimi**  
  
```  
EXP (<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Açıklamalar**  
  
 Merhaba sabiti **e** (2.718281...) olan hello doğal logaritma temel.  
  
 Merhaba sayısının üssü hello sabiti olduğunda **e** toohello hello sayının üssünün. Örneğin EXP(1.0) e = ^ 1.0 = 2.71828182845905 ve EXP(10) e = ^ 10 = 22026.4657948067.  
  
 bir sayının hello doğal logaritmasını üstel Hello numarasıdır hello kendisini: EXP (günlüğü (n)) = n. Ve bir dizi üstel hello hello doğal logaritmasını hello numarasıdır kendisini: günlük (EXP (n)) = n.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnekte değişken bildirir ve hello üstel hello belirtilen değişkeni (10) değerini döndürür.  
  
```  
SELECT EXP(10)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 Merhaba aşağıdaki örnek hello üstel değerini 20 hello doğal logaritmasını ve hello hello doğal logaritmasını 20 üstel döndürür. Bu işlevler inverse işlevleri, bir başka hello dönüş değeri kayan nokta 20 matematik her iki durumda olduğu için yuvarlama ile olduğundan.  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <a name="bk_log"></a>GÜNLÜK  
 Merhaba hello doğal logaritmasını döndürür sayısal ifade belirtildi.  
  
 **Sözdizimi**  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
-   `base`  
  
     Merhaba hello logaritmanın tabanı ayarlar isteğe bağlı sayısal değişkeni.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Açıklamalar**  
  
 Varsayılan olarak, LOG() hello doğal logaritmasını döndürür. Merhaba temel hello logaritmasını tooanother değerinin hello isteğe bağlı temel parametresini kullanarak değiştirebilirsiniz.  
  
 Hello doğal logaritmasını olduğu hello logaritmasını toohello temel **e**, burada **e** Irrational bir sabit yaklaşık olarak eşit too2.718281828 değil.  
  
 Merhaba bir dizi üstel Hello doğal logaritmasını numarasıdır hello kendisini: günlük (EXP (n)) = n. Ve sayının hello doğal logaritmasını üstel hello hello numarasıdır kendisini: EXP (günlüğü (n)) = n.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnekte değişken bildirir ve hello logaritmasını hello belirtilen değişkeni (10) değerini döndürür.  
  
```  
SELECT LOG(10)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 Merhaba aşağıdaki örnek bir sayının hello üs Merhaba günlük hesaplar.  
  
```  
SELECT EXP(LOG(10))  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <a name="bk_log10"></a>LOG10  
 Merhaba döndürür hello 10 tabanında logaritmasını sayısal ifade belirtildi.  
  
 **Sözdizimi**  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Açıklamalar**  
  
 Merhaba LOG10 ve güç işlevleri inversely ilgili tooone olan başka bir. Örneğin, 10 ^ LOG10(n) = n.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnekte değişken bildirir ve hello LOG10 hello belirtilen değişkeni (100) değerini döndürür.  
  
```  
SELECT LOG10(100)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: 2}]  
```  
  
####  <a name="bk_pi"></a>PI  
 PI sayısının sabit bir değer döndürür hello.  
  
 **Sözdizimi**  
  
```  
PI ()  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek hello PI değerini döndürür.  
  
```  
SELECT PI()  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_power"></a>GÜÇ  
 Döndürür hello belirtilen başlangıç değeri ifadesi toohello belirtilen güç.  
  
 **Sözdizimi**  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
-   `y`  
  
     Merhaba güç toowhich tooraise olan `numeric_expression`.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Aşağıdaki örneğine hello 3 (Merhaba küp hello sayının) numara toohello gücünü oluşturma işlemi gösterilmektedir.  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <a name="bk_radians"></a>RADYAN CİNSİNDEN  
 Derece sayısal bir ifadenin girildiğinde radyan cinsinden döndürür.  
  
 **Sözdizimi**  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnekte birkaç açıları girdi olarak alır ve bunlara karşılık gelen radian değerler döndürür.  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <a name="bk_round"></a>YUVARLAK  
 Yuvarlak toohello en yakın tamsayı değeri sayısal bir değer döndürür.  
  
 **Sözdizimi**  
  
```  
ROUND(<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek pozitif ve negatif sayıları toohello tamsayı en yakın aşağıdaki hello yuvarlar.  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <a name="bk_sign"></a>OTURUM  
 Artı (+ 1), sıfır (0), döndürür hello veya sayısal ifade hello eksi (-1) belirtisi belirtildi.  
  
 **Sözdizimi**  
  
```  
SIGN(<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek hello oturum değerleri sayıların-2 too2 döndürür.  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <a name="bk_sin"></a>SIN  
 Döndürür hello trigonometrik sinüsünü hello radyan cinsinden açı, hello ifade belirtildi.  
  
 **Sözdizimi**  
  
```  
SIN(<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Aşağıdaki örnek hello hello SIN hello belirtilen açının hesaplar.  
  
```  
SELECT SIN(45.175643)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <a name="bk_sqrt"></a>SQRT  
 Belirtilen sayısal değer hello hello kare kökünü döndürür.  
  
 **Sözdizimi**  
  
```  
SQRT(<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek 1-3 sayıların hello kare kökleri döndürür.  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <a name="bk_square"></a>KARE  
 Merhaba kare döndürür hello sayısal değer belirtildi.  
  
 **Sözdizimi**  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek numaraları 1-3 hello kareleri döndürür.  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <a name="bk_tan"></a>TAN  
 Merhaba hello tanjantını döndürür radyan cinsinden açı, hello ifade belirtildi.  
  
 **Sözdizimi**  
  
```  
TAN (<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek hesaplar PI () hello tanjantını / 2.  
  
```  
SELECT TAN(PI()/2);  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <a name="bk_trunc"></a>TRUNC  
 Kesilmiş toohello en yakın tamsayı değeri sayısal bir değer döndürür.  
  
 **Sözdizimi**  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `numeric_expression`  
  
     Sayısal bir ifadedir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Aşağıdaki örnek hello pozitif ve negatif sayıları toohello tamsayı değeri en yakın aşağıdaki hello tamsayıya dönüştürür.  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <a name="bk_type_checking_functions"></a>Denetimi işlevleri yazın  
 Merhaba aşağıdaki işlevleri karşı giriş değerleri denetleme türünü destekleyen ve her bir Boole değeri döndürür.  
  
||||  
|-|-|-|  
|[IS_ARRAY](#bk_is_array)|[IS_BOOL](#bk_is_bool)|[IS_DEFINED](#bk_is_defined)|  
|[IS_NULL](#bk_is_null)|[IS_NUMBER](#bk_is_number)|[IS_OBJECT](#bk_is_object)|  
|[IS_PRIMITIVE](#bk_is_primitive)|[IS_STRING](#bk_is_string)||  
  
####  <a name="bk_is_array"></a>IS_ARRAY  
 Bir dizidir hello Hello türü ifade belirttiyseniz gösteren bir Boole değeri döndürür.  
  
 **Sözdizimi**  
  
```  
IS_ARRAY(<expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `expression`  
  
     Geçerli bir ifade değil.  
  
 **Dönüş türleri**  
  
 Boole ifadesi döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve hello IS_ARRAY işlevi kullanarak tanımsız türleri denetler.  
  
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
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <a name="bk_is_bool"></a>IS_BOOL  
 Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri olan bir Boole değeri döndürür.  
  
 **Sözdizimi**  
  
```  
IS_BOOL(<expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `expression`  
  
     Geçerli bir ifade değil.  
  
 **Dönüş türleri**  
  
 Boole ifadesi döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve hello IS_BOOL işlevi kullanarak tanımsız türleri denetler.  
  
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
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_defined"></a>IS_DEFINED  
 Başlangıç özellik değeri atanmış olan gösteren bir Boole değeri döndürür.  
  
 **Sözdizimi**  
  
```  
IS_DEFINED(<expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `expression`  
  
     Geçerli bir ifade değil.  
  
 **Dönüş türleri**  
  
 Boole ifadesi döndürür.  
  
 **Örnekler**  
  
 Örnek denetimleri hello varlığını hello içinde bir özellik için aşağıdaki hello JSON belgesi belirtilmiş. Merhaba önce "a" var, ancak hello ikinci "b" mevcut olduğundan false döndürür. bu yana true değerini döndürür.  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <a name="bk_is_null"></a>IS_NULL  
 Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri null döndürür.  
  
 **Sözdizimi**  
  
```  
IS_NULL(<expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `expression`  
  
     Geçerli bir ifade değil.  
  
 **Dönüş türleri**  
  
 Boole ifadesi döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve hello IS_NULL işlevi kullanarak tanımsız türleri denetler.  
  
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
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_number"></a>IS_NUMBER  
 Bir sayıdır hello Hello türü ifade belirttiyseniz gösteren bir Boole değeri döndürür.  
  
 **Sözdizimi**  
  
```  
IS_NUMBER(<expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `expression`  
  
     Geçerli bir ifade değil.  
  
 **Dönüş türleri**  
  
 Boole ifadesi döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve hello IS_NULL işlevi kullanarak tanımsız türleri denetler.  
  
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
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_object"></a>IS_OBJECT  
 Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri olan bir JSON nesnesi döndürür.  
  
 **Sözdizimi**  
  
```  
IS_OBJECT(<expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `expression`  
  
     Geçerli bir ifade değil.  
  
 **Dönüş türleri**  
  
 Boole ifadesi döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve hello IS_OBJECT işlevi kullanarak tanımsız türleri denetler.  
  
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
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <a name="bk_is_primitive"></a>IS_PRIMITIVE  
 Merhaba Hello türü ifade ilkel belirtilirse, gösteren bir Boole değeri döndürür (dize, Boolean, sayısal veya null).  
  
 **Sözdizimi**  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `expression`  
  
     Geçerli bir ifade değil.  
  
 **Dönüş türleri**  
  
 Boole ifadesi döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve hello IS_PRIMITIVE işlevi kullanarak tanımsız türleri denetler.  
  
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
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <a name="bk_is_string"></a>IS_STRING  
 Merhaba Hello türü ifade belirttiyseniz gösteren bir Boole değeri bir dize verir.  
  
 **Sözdizimi**  
  
```  
IS_STRING(<expression>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `expression`  
  
     Geçerli bir ifade değil.  
  
 **Dönüş türleri**  
  
 Boole ifadesi döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek JSON Boolean, sayı, dize, null nesneleri, nesne, dizi ve hello IS_STRING işlevi kullanarak tanımsız türleri denetler.  
  
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
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <a name="bk_string_functions"></a>Dize işlevleri  
 Merhaba aşağıdaki skaler işlevler dize giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir dize, sayısal ya da Boole değeri döndürür.  
  
||||  
|-|-|-|  
|[CONCAT](#bk_concat)|[İÇERİR](#bk_contains)|[ENDSWITH](#bk_endswith)|  
|[INDEX_OF](#bk_index_of)|[SOL](#bk_left)|[UZUNLUĞU](#bk_length)|  
|[DAHA DÜŞÜK](#bk_lower)|[LTRIM](#bk_ltrim)|[DEĞİŞTİR](#bk_replace)|  
|[ÇOĞALTILAN](#bk_replicate)|[TERS ÇEVİR](#bk_reverse)|[SAĞ](#bk_right)|  
|[RTRIM](#bk_rtrim)|[STARTSWITH](#bk_startswith)|[SUBSTRING](#bk_substring)|  
|[ÜST](#bk_upper)|||  
  
####  <a name="bk_concat"></a>CONCAT  
 İki veya daha fazla dize değerlerini birleştirme hello sonucu olan bir dize döndürür.  
  
 **Sözdizimi**  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
 **Dönüş türleri**  
  
 Bir dize ifadesi döndürür.  
  
 **Örnekler**  
  
 Örnek döndürür birleştirilmiş hello hello dizisi aşağıdaki hello değerleri belirtti.  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <a name="bk_contains"></a>İÇERİR  
 Merhaba ilk dize ifadesi hello ikinci içerip içermediğini gösteren bir Boole değeri döndürür.  
  
 **Sözdizimi**  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
 **Dönüş türleri**  
  
 Boole ifadesi döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnekte "abc" "ab" ve "d" içerir olmadığını denetler.  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_endswith"></a>ENDSWITH  
 Merhaba ilk dize ifadesi ile Merhaba ikinci bitip olup olmadığını gösteren bir Boole değeri döndürür.  
  
 **Sözdizimi**  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
 **Dönüş türleri**  
  
 Boole ifadesi döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnekte "abc", "b" ve "bc" ile biten hello döndürür.  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_index_of"></a>INDEX_OF  
 Merhaba dize bulunmazsa hello ikinci dize ifadesi hello ilk belirtilen dize ifadesi veya -1 içinde hello ilk oluşum konumunu başlangıç hello döndürür.  
  
 **Sözdizimi**  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnekte "abc" içinde çeşitli alt dizeler hello dizinini döndürür.  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <a name="bk_left"></a>SOL  
 Döndürür hello sol bölümü bir dizenin belirtilen hello ile karakter sayısı.  
  
 **Sözdizimi**  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
-   `num_expr`  
  
     Geçerli herhangi bir sayısal ifadeye ' dir.  
  
 **Dönüş türleri**  
  
 Bir dize ifadesi döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnekte "abc" bölümü çeşitli uzunluk değeri için sol hello döndürür.  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <a name="bk_length"></a>UZUNLUĞU  
 Dize ifadesi belirtilen döndürür hello hello karakter sayısı.  
  
 **Sözdizimi**  
  
```  
LENGTH(<str_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
 **Dönüş türleri**  
  
 Bir dize ifadesi döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek hello uzunlukta bir dize döndürür.  
  
```  
SELECT LENGTH("abc")  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_lower"></a>DAHA DÜŞÜK  
 Büyük harf karakter veri toolowercase dönüştürmeden sonra bir dize ifadesi döndürür.  
  
 **Sözdizimi**  
  
```  
LOWER(<str_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
 **Dönüş türleri**  
  
 Bir dize ifadesi döndürür.  
  
 **Örnekler**  
  
 örnekte gösterildiği nasıl aşağıdaki hello toouse alt sorgu.  
  
```  
SELECT LOWER("Abc")  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <a name="bk_ltrim"></a>LTRIM  
 Öndeki boşlukları kaldırır sonra bir dize ifadesi döndürür.  
  
 **Sözdizimi**  
  
```  
LTRIM(<str_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
 **Dönüş türleri**  
  
 Bir dize ifadesi döndürür.  
  
 **Örnekler**  
  
 örnekte gösterildiği nasıl aşağıdaki hello toouse LTRIM bir sorgu içinde.  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <a name="bk_replace"></a>DEĞİŞTİR  
 Belirtilen dize değeri tüm oluşumlarını başka bir dize değeri ile değiştirir.  
  
 **Sözdizimi**  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
 **Dönüş türleri**  
  
 Bir dize ifadesi döndürür.  
  
 **Örnekler**  
  
 Aşağıdaki örneğine hello toouse bir sorguda nasıl YERİNİ gösterir.  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <a name="bk_replicate"></a>ÇOĞALTMA  
 Bir dize değeri, belirtilen sayıda yineler.  
  
 **Sözdizimi**  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
-   `num_expr`  
  
     Geçerli herhangi bir sayısal ifadeye ' dir.  
  
 **Dönüş türleri**  
  
 Bir dize ifadesi döndürür.  
  
 **Örnekler**  
  
 Aşağıdaki örneğine hello nasıl toouse ÇOĞALTMAK sorguda gösterir.  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <a name="bk_reverse"></a>TERS ÇEVİR  
 Merhaba ters sırada bir dize değerini döndürür.  
  
 **Sözdizimi**  
  
```  
REVERSE(<str_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
 **Dönüş türleri**  
  
 Bir dize ifadesi döndürür.  
  
 **Örnekler**  
  
 Aşağıdaki örneğine hello nasıl toouse ters sorguda gösterir.  
  
```  
SELECT REVERSE("Abc")  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <a name="bk_right"></a>SAĞ  
 Karakter sayısını döndürür hello dizesi sağ parçası hello ile belirtilen.  
  
 **Sözdizimi**  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
-   `num_expr`  
  
     Geçerli herhangi bir sayısal ifadeye ' dir.  
  
 **Dönüş türleri**  
  
 Bir dize ifadesi döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnek hello sağ bölümünü "abc" için çeşitli uzunluk değeri döndürür.  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <a name="bk_rtrim"></a>RTRIM  
 Sondaki boşlukları kaldırır sonra bir dize ifadesi döndürür.  
  
 **Sözdizimi**  
  
```  
RTRIM(<str_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
 **Dönüş türleri**  
  
 Bir dize ifadesi döndürür.  
  
 **Örnekler**  
  
 örnekte gösterildiği nasıl aşağıdaki hello toouse RTRIM bir sorgu içinde.  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <a name="bk_startswith"></a>STARTSWITH  
 Merhaba ilk dize ifadesi ile Merhaba ikinci başlayıp başlamadığını gösteren bir Boole değeri döndürür.  
  
 **Sözdizimi**  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
 **Dönüş türleri**  
  
 Boole ifadesi döndürür.  
  
 **Örnekler**  
  
 Merhaba denetimleri Merhaba, dize "abc" aşağıdaki örnekte başlar "b" ve "a".  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_substring"></a>SUBSTRING  
 Merhaba başlayan bir dize ifadesi döndürür parçası karakter sıfır tabanlı konumu belirtilen ve uzunluk veya hello dize toohello sonu toohello belirtilen devam eder.  
  
 **Sözdizimi**  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
-   `num_expr`  
  
     Geçerli herhangi bir sayısal ifadeye ' dir.  
  
 **Dönüş türleri**  
  
 Bir dize ifadesi döndürür.  
  
 **Örnekler**  
  
 Merhaba aşağıdaki örnekte "abc" Merhaba dizenin 1 ve 1 karakter uzunluğu için başlangıç döndürür.  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": "b"}]  
```  
  
####  <a name="bk_upper"></a>ÜST  
 Küçük harf karakter veri toouppercase dönüştürmeden sonra bir dize ifadesi döndürür.  
  
 **Sözdizimi**  
  
```  
UPPER(<str_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `str_expr`  
  
     Tüm geçerli bir dize ifadesidir.  
  
 **Dönüş türleri**  
  
 Bir dize ifadesi döndürür.  
  
 **Örnekler**  
  
 örnekte gösterildiği nasıl aşağıdaki hello toouse üst sorgu  
  
```  
SELECT UPPER("Abc")  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <a name="bk_array_functions"></a>Dizi işlevleri  
 skaler işlevler aşağıdaki hello bir dizi giriş değeri ve return sayısal, Boole veya dizi değer üzerinde bir işlemi gerçekleştirme  
  
||||  
|-|-|-|  
|[ARRAY_CONCAT](#bk_array_concat)|[ARRAY_CONTAINS](#bk_array_contains)|[ARRAY_LENGTH](#bk_array_length)|  
|[ARRAY_SLICE](#bk_array_slice)|||  
  
####  <a name="bk_array_concat"></a>ARRAY_CONCAT  
 İki veya daha fazla dizi değerlerini birleştirme hello sonucu olan bir dizi döndürür.  
  
 **Sözdizimi**  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 **Bağımsız değişkenler**  
  
-   `arr_expr`  
  
     Tüm geçerli dizi ifadesidir.  
  
 **Dönüş türleri**  
  
 Bir dizi ifadesi döndürür.  
  
 **Örnekler**  
  
 örnekte nasıl tooconcatenate iki dizi hello.  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <a name="bk_array_contains"></a>ARRAY_CONTAINS  
 Belirtilen değer hello dizi hello içerip içermediğini gösteren Boole değeri döndürür.  
  
 **Sözdizimi**  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `arr_expr`  
  
     Tüm geçerli dizi ifadesidir.  
  
-   `expr`  
  
     Geçerli bir ifade değil.  
  
 **Dönüş türleri**  
  
 Bir Boole değeri döndürür.  
  
 **Örnekler**  
  
 Aşağıdaki örneğine nasıl hello toocheck ARRAY_CONTAINS kullanarak bir dizi üyelik için.  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_array_length"></a>ARRAY_LENGTH  
 Dizi ifadesi belirtilen döndürür hello hello öğelerinin sayısı.  
  
 **Sözdizimi**  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `arr_expr`  
  
     Tüm geçerli dizi ifadesidir.  
  
 **Dönüş türleri**  
  
 Sayısal ifade döndürür.  
  
 **Örnekler**  
  
 örnek, nasıl tooget hello ARRAY_LENGTH kullanarak bir dizi uzunluğu hello.  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_array_slice"></a>ARRAY_SLICE  
 Bir dizi ifadesi bölümünü döndürür.
  
 **Sözdizimi**  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 **Bağımsız değişkenler**  
  
-   `arr_expr`  
  
     Tüm geçerli dizi ifadesidir.  
  
-   `num_expr`  
  
     Geçerli herhangi bir sayısal ifadeye ' dir.  
  
 **Dönüş türleri**  
  
 Bir Boole değeri döndürür.  
  
 **Örnekler**  
  
 Aşağıdaki örneğine nasıl hello tooget ARRAY_SLICE kullanarak bir dizi bir parçası.  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <a name="bk_spatial_functions"></a>Uzamsal işlevleri  
 Merhaba aşağıdaki skaler işlevler uzamsal nesne giriş değeri üzerinde bir işlemi gerçekleştirmek ve bir sayısal ya da Boole değeri döndürür.  
  
||||  
|-|-|-|  
|[ST_DISTANCE](#bk_st_distance)|[ST_WITHIN](#bk_st_within)|[ST_INTERSECTS](#bk_st_intersects)|[ST_ISVALID](#bk_st_isvalid)|  
|[ST_ISVALIDDETAILED](#bk_st_isvaliddetailed)|||  
  
####  <a name="bk_st_distance"></a>ST_DISTANCE  
 Merhaba iki GeoJSON noktası, çokgen veya LineString ifadeleri arasında Hello uzaklığını döndürür.  
  
 **Sözdizimi**  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `spatial_expr`  
  
     Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.  
  
 **Dönüş türleri**  
  
 Başlangıç uzaklığı içeren sayısal bir ifade döndürür. Bu ölçümler hello varsayılan başvuru sistemi için ifade edilir.  
  
 **Örnekler**  
  
 örnekte gösterildiği nasıl aşağıdaki hello tooreturn içinde 30 km hello biri olan tüm ailesi belgeleri belirtilen hello st_dıstance yerleşik işlevi kullanarak konumu. .  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <a name="bk_st_within"></a>ST_WITHIN  
 Merhaba ilk bağımsız değişkeninde belirtilen hello GeoJSON nesne (noktası, çokgen veya LineString) hello ikinci bağımsız değişkeni hello GeoJSON (noktası, çokgen veya LineString) içinde olup olmadığını gösteren bir Boole ifadesi döndürür.  
  
 **Sözdizimi**  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `spatial_expr`  
  
     Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.  
 
-   `spatial_expr`  
  
     Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.  
  
 **Dönüş türleri**  
  
 Bir Boole değeri döndürür.  
  
 **Örnekler**  
  
 Aşağıdaki örnek hello nasıl toofind ST_WITHIN kullanarak bir Çokgen tüm ailesi belgeleri gösterir.  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <a name="bk_st_intersects"></a>ST_INTERSECTS  
 Merhaba ilk bağımsız değişkeninde belirtilen hello GeoJSON nesne (noktası, çokgen veya LineString) hello ikinci bağımsız değişken hello GeoJSON (noktası, çokgen veya LineString) kesiştiğinden olup olmadığını gösteren bir Boole ifadesi döndürür.  
  
 **Sözdizimi**  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `spatial_expr`  
  
     Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.  
 
-   `spatial_expr`  
  
     Tüm geçerli GeoJSON noktası, çokgen veya LineString nesne ifadesidir.  
  
 **Dönüş türleri**  
  
 Bir Boole değeri döndürür.  
  
 **Örnekler**  
  
 örnekte gösterildiği nasıl aşağıdaki hello ile kesiştiğinden tüm alanları hello Çokgen toofind.  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <a name="bk_st_isvalid"></a>ST_ISVALID  
 Merhaba GeoJSON noktası, çokgen veya LineString ifadesi geçerli belirtilen olup olmadığını gösteren bir Boole değeri döndürür.  
  
 **Sözdizimi**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `spatial_expr`  
  
     Tüm geçerli GeoJSON noktası, çokgen veya LineString ifadesidir.  
  
 **Dönüş türleri**  
  
 Boole ifadesi döndürür.  
  
 **Örnekler**  
  
 örnekte gösterildiği nasıl aşağıdaki hello bir noktası geçerliyse ST_VALID kullanarak toocheck.  
  
 Örneğin, bu nokta hello geçerli değerler [-90, 90] aralığında değil enlem değer içeriyor, bu nedenle hello sorgu yanlış değerini döndürür.  
  
 Çokgenler için hello hello son koordinat çifti sağlanan olması gerektiğini belirtilmesini gerektiriyor GeoJSON hello aynı hello ilk toocreate kapalı şekli. Çokgen içindeki noktaları yönünün sırayla belirtilmelidir. Belirtilen saat yönünde sırayla Çokgen hello bölgesinde hello tersini temsil eder.  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{ "$1": false }]  
```  
  
####  <a name="bk_st_isvaliddetailed"></a>ST_ISVALIDDETAILED  
 Merhaba GeoJSON noktası, çokgen veya LineString ifade belirtilmişse bir Boole değeri içeren bir JSON değeri geçerli değil ve geçersiz, ayrıca bir dize değeri olarak neden hello döndürür.  
  
 **Sözdizimi**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **Bağımsız değişkenler**  
  
-   `spatial_expr`  
  
     Tüm geçerli GeoJSON noktası veya Çokgen ifadesidir.  
  
 **Dönüş türleri**  
  
 Merhaba GeoJSON noktası belirtilen veya Çokgen ifadesi geçerli değil ve geçersiz, ayrıca bir dize değeri olarak neden hello bir Boole değeri içeren bir JSON değeri döndürür.  
  
 **Örnekler**  
  
 Aşağıdaki örneğine nasıl hello ST_ISVALIDDETAILED kullanarak toocheck geçerlilik (ayrıntılarla ile).  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 Merhaba sonuç kümesini burada verilmiştir.  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a>Sonraki adımlar  
 [SQL söz dizimi ve Azure Cosmos DB SQL sorgusu](documentdb-sql-query.md)   
 [Azure Cosmos DB belgeleri](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
