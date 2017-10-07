---
title: "Azure Search'te aaaHow tooimplement çok yönlü gezinme | Microsoft Docs"
description: "Azure Search, Microsoft Azure üzerinde barındırılan bulut arama hizmeti ile tümleştirmek modellenmiş bir gezinmede tooapplications ekleyin."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: cdf98fd4-63fd-4b50-b0b0-835cb08ad4d3
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 3/10/2017
ms.author: heidist
ms.openlocfilehash: c1e6bf9dc55d0044525db79e37d35a50ded5a736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-faceted-navigation-in-azure-search"></a>Nasıl modellenmiş bir gezinmede tooimplement Azure Search'te
Modellenmiş bir gezinmede arama uygulamaları kendi kendine yönlendirilmiş ayrıntıya gitme gezinti sağlayan bir filtreleme mekanizması ' dir. Merhaba terim 'modellenmiş bir gezinmede' tanınmayan olabilir, ancak büyük olasılıkla daha önce kullanılmış. Aşağıdaki örnekte gösterildiği hello modellenmiş bir gezinmede hello kullanılan kategorileri toofilter sonuçları'den fazla bir şey değildir.

 ![Azure arama iş Portal Tanıtımı][1]

Modellenmiş bir gezinmede bir alternatif giriş noktası toosearch ' dir. El ile karmaşık arama ifadeleri uygun bir alternatif tootyping sunar. Modelleri için sıfır sonuçları almadım sağlarken aradığınızı bulmanıza yardımcı olabilir. Bir geliştirici olarak modelleri, arama gövde gezinme hello en yararlı arama ölçütlerini kullanıma olanak tanır. Çevrimiçi perakende uygulamalarda modellenmiş bir gezinmede genellikle markalar, Departmanlar (çocuk yerine), boyutu, fiyat, popülerliği ve derecelendirmeleri üzerinde oluşturulmuştur. 

Modellenmiş bir gezinmede uygulama arama teknolojileri arasında farklılık gösterir. Azure Search'te modellenmiş bir gezinmede sorgu zamanında, şemada daha önce öznitelikli alanları kullanılarak oluşturulur.

-   Bir sorgu göndermelidir uygulamanızı derlemeler hello sorgularda *modeli sorgu parametreleri* tooget hello kullanılabilir modeli filtre değerleri bu belge için sonuç.

-   tooactually kırpma hello belge sonuç kümesi, Merhaba uygulaması da uygulamalısınız bir `$filter` ifade.

Uygulama geliştirme hello toplu hello iş sorguları yapıları kod yazma meydana gelir. Birçok modellenmiş Gezinti bölmesinden beklediğiniz hello uygulama davranışları aralıkları tanımlama ve sayıları için model sonuçları alma için yerleşik destek dahil olmak üzere hello hizmeti tarafından sağlanır. Merhaba hizmeti de yardımcı duyarlı Varsayılanları içerir yönetilmeleri Gezinti yapıları kaçının. 

## <a name="sample-code-and-demo"></a>Örnek kod ve tanıtım
Bu makalede örnek olarak bir iş arama portal kullanır. Merhaba örnek bir ASP.NET MVC uygulaması uygulanır.

-   Bakın ve test hello çalışma demo çevrimiçi adresindeki [Azure arama proje portalı Demo](http://azjobsdemo.azurewebsites.net/).

-   Merhaba kodu hello indirme [Azure-Samples bağlantıların github'da](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).

## <a name="get-started"></a>başlarken
Yeni toosearch geliştirme yapıyorsanız, kendi kendine yönlendirilmiş arama hello olasılıklarını gösterir hello en iyi şekilde toothink modellenmiş Gezinti olur. Önceden tanımlanmış filtreleri, hızlı bir şekilde arama sonuçları noktası tıklatın eylemler arasında aşağı daraltmak için kullanılan temel alarak ayrıntıya arama deneyimi türüdür. 

### <a name="interaction-model"></a>Etkileşim modeli

Merhaba arama deneyimi modellenmiş gezinmesine sağlandığından yanıt toouser Eylemler unfold sorguları bir dizi olarak anlayarak Başlat yinelemelidir.

başlangıç noktası hello genellikle hello periphery yerleştirilen çok yönlü gezinmeyi sağlayan bir uygulama sayfasıdır. Modellenmiş Gezinti ağaç yapısı, her değeri veya tıklanabilir bir metin için onay kutularını ile görülür. 

1. TooAzure arama gönderilen bir sorgu hello modellenmiş gezinti yapısında bir veya daha fazla model sorgu parametreleri aracılığıyla belirtir. Merhaba sorgu örneği için içerebilir `facet=Rating`, belki de ile bir `:values` veya `:sort` seçeneği toofurther hello sunu daraltın.
2. Merhaba sunu katmanı hello istekte belirtilen hello modellerle kullanarak çok yönlü gezinmeyi sağlayan bir arama sayfasını işler.
3. Derecelendirme içeren modellenmiş gezinti yapısı verildiğinde, yalnızca 4 veya daha yüksek bir derecelendirme ürünleriyle gösterilmesi gereken "4" tooindicate'ı tıklatın. 
4. Yanıt olarak Merhaba uygulaması içeren bir sorgu gönderir.`$filter=Rating ge 4` 
5. Merhaba yeni ölçütlerini karşılayan yalnızca bu öğeleri içeren bir azaltılmış sonuç kümesi gösteren hello sunu katmanı güncelleştirmeleri hello sayfasında, (Bu durumda, ürün 4 derecelendirilmiş ve üstü).

Bir model için sorgu parametresi olsa da, sorgu girişi ile karıştırmayın. Sorguda seçim ölçütü olarak asla kullanılmaz. Bunun yerine, model Sorgu parametrelerinin hello yanıtta gelir girişleri toohello gezinti yapısında olarak düşünün. Sağladığınız her model için sorgu parametresi, Azure Search hello kısmi sonuçlarındaki her model değeri için kaç tane belgelerdir değerlendirir.

Bildirim hello `$filter` 4. adımda. Merhaba filtre modellenmiş bir gezinmede önemli bir yönüdür. Modelleri ve filtreleri hello API bağımsız olmakla birlikte, düşündüğünüz her iki toodeliver hello deneyimi gerekir. 

### <a name="app-design-pattern"></a>Uygulama tasarım deseni

Uygulama kodunda hello düzeni toouse modeli sorgu parametreleri tooreturn hello modellenmiş bir gezinmede modeli sonuçları yanı sıra, bir $filter ifadesi birlikte yapısıdır.  Merhaba filtre ifadesi tanıtıcıları hello hello model değeri olayına tıklayın. Merhaba düşünün `$filter` arama sonuçlarının ifade hello gerçek kırpma arkasındaki hello kod olarak toohello sunu katmanı döndürdü. Renkleri modeli verildiğinde, hello rengi kırmızı tıklatarak aracılığıyla uygulanır bir `$filter` kırmızı renk olan öğeleri seçer ifade. 

### <a name="query-basics"></a>Sorgu temelleri

Azure Search'te bir isteği aracılığıyla bir veya daha fazla sorgu parametreleri belirtilir (bkz [Search belgeleri](http://msdn.microsoft.com/library/azure/dn798927.aspx) her biri bir açıklaması için). Hello sorgu parametreleri hiçbiri gerekli değildir, ancak en az bir geçerli bir sorgu toobe sırada olmalıdır.

Duyarlık hello özelliği toofilter ilgisiz isabet çıkışı gerçekleştirilir gibi birine veya ikisine de bu ifadeleri anladım:

-   **Arama =**  
    Bu parametrenin değerini Hello hello arama ifadesi meydana gelir. Tek bir metin veya birden çok hüküm ve işleçleri içeren karmaşık arama ifadesi olması olabilir. Merhaba sunucuda arama ifadesi tam metin arama, sıralama sırayla sonuçları döndüren koşullarını eşleşen hello dizin aranabilir alanlara sorgulamak için kullanılır. Ayarlarsanız `search` toonull, sorgu yürütme dizinidir hello tüm (diğer bir deyişle, `search=*`). İn this Case, diğer öğeleri Merhaba, gibi sorgu bir `$filter` veya profili Puanlama, hello hangi belgeleri döndürülen etkileyen birincil faktörlerdir `($filter`) ve hangi sırayla (`scoringProfile` veya `$orderby`).

-   **$filter =**  
    Bir filtre, belirli bir belge öznitelikleri hello değerlerine göre arama sonuçları hello boyutunu sınırlamak için güçlü bir mekanizmadır. A `$filter` hello kullanılabilir değerler ve her bir değer için karşılık gelen sayıları oluşturur olduğunu mantığı arkasından önce değerlendirilir

Karmaşık arama ifadeleri hello hello sorgu performansını azaltın. Mümkünse, sorgu performansını artırmak ve iyi oluşturulmuş filtre ifadeleri tooincrease duyarlık kullanın.

toobetter nasıl daha hassas bir filtre ekler anlamak, bir filtre ifadesi içeren bir karmaşık arama ifade tooone karşılaştırın:

-   `GET /indexes/hotel/docs?search=lodging budget +Seattle –motel +parking`
-   `GET /indexes/hotel/docs?search=lodging&$filter=City eq ‘Seattle’ and Parking and Type ne ‘motel’`

Her iki sorguları geçerlidir, ancak hello ikinci motels olmayan Seattle'da park ile arıyorsanız üstündedir.
-   Merhaba ilk sorgu belirtilen veya dize alanları adını, açıklamasını ve aranabilir verileri içeren herhangi bir alan gibi geçmeyen belirli sözcükleri kullanır.
-   Merhaba ikinci sorgu kesin eşleşmeler yapılandırılmış verileri arar ve büyük olasılıkla toobe çok daha doğru olduğundan.

Modellenmiş bir gezinmede içeren uygulamalarda, arama sonuçlarını daraltarak modellenmiş bir gezinmede yapısı üzerinden her bir kullanıcı eylemi eşlik emin olun. toonarrow sonuçları, bir filtre ifadesi kullanın.

<a name="howtobuildit"></a>

## <a name="build-a-faceted-navigation-app"></a>Modellenmiş bir gezinmede uygulaması oluşturma
Azure Search modellenmiş bir gezinmede hello arama isteği oluşturur, uygulama kodunuzda uygulayın. önceden tanımlanmış şemanızı öğelerinde Hello modellenmiş bir gezinmede kullanır.

Arama dizininize önceden tanımlanmış olan hello `Facetable [true|false]` dizin özniteliği, seçili alanları tooenable üzerinde ayarlayın veya kullanımlarını modellenmiş gezinti yapısında devre dışı. Olmadan `"Facetable" = true`, model Gezinti bölmesinde bir alan kullanılamaz.

Hello sunu katmanı kodunuzda hello kullanıcı deneyimi sağlar. Merhaba bağlı hello label ve değerleri, onay kutularını ve hello sayısı gibi hello modellenmiş gezinmesine bölümlerini listelenmelidir. Hello Azure Search REST API'sini platform belirsiz, hangi dil ve platformu kullanın. Merhaba önemli her ek modeli seçtiğinizde artımlı destek tooinclude kullanıcı Arabirimi öğeleri, güncelleştirilmiş kullanıcı Arabirimi ile durumu şeydir. 

Sorgu zamanında uygulama kodunuz içeren bir istek oluşturur `facet=[string]`, hello alan toofacet tarafından sağlayan bir istek parametresi. Sorgu birden fazla modelleri gibi olabilir `&facet=color&facet=category&facet=rating`, her biri ayrılmış bir ampersan (&) karakteri tarafından.

Uygulama kodu gerekir de oluşturmak bir `$filter` ifade toohandle hello modellenmiş bir gezinmede olay'ı tıklatın. A `$filter` filtre ölçütü olarak hello model değeri kullanarak hello arama sonuçlarını azaltır.

Azure arama güncelleştirmeleri toohello modellenmiş bir gezinmede yapısı birlikte girin bir veya daha fazla şartları temel alınarak hello arama sonuçlarını döndürür. Azure Search'te modellenmiş bir gezinmede modeli değerleri içeren bir tek düzeyli yapım ve her biri için kaç tane sonuçlarını bulunan sayar.

Aşağıdaki bölümlerde hello biz yakın nasıl göz atın toobuild her bölümü.

<a name="buildindex"></a>

## <a name="build-hello-index"></a>Merhaba dizini oluşturun
Bu dizin özniteliği aracılığıyla hello dizinindeki alan alanını temelinde etkin olduğunu: `"Facetable": true`.  
Büyük olasılıkla modellenmiş bir gezinmede kullanılabilir tüm alan türleri `Facetable` varsayılan olarak. Bu tür alan türleri içerir `Edm.String`, `Edm.DateTimeOffset`, ve tüm sayısal alan türleri hello (esas olarak, tüm alan türleri modellenebilir dışında olan `Edm.GeographyPoint`, hangi kullanılamaz modellenmiş bir gezinmede). 

Dizin oluştururken, en iyi uygulama modellenmiş gezinmesine tooexplicitly Aç olduğunu hiçbir zaman bir model kullanılması gereken alanlar için kapalıdır.  Özellikle, dize alanları için bir kimlik veya ürün adı gibi singleton değerleri çok ayarlanmalıdır`"Facetable": false` tooprevent kendi yanlışlıkla (ve etkisiz) modellenmiş bir gezinmede kullanın. Burada gerekmeyen kapalı olduğunu kapatma hello dizin hello boyutunu küçük tutmaya yardımcı olur ve genellikle performansı artırır.

Aşağıdaki hello proje portalı Demo örnek uygulaması, bazı öznitelikler tooreduce hello boyutunu kırpılmış hello Şeması'nın bir parçasıdır:

```json
{
  ...
  "name": "nycjobs",
  "fields": [
    { “name”: "id",                 "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "job_id",             "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "agency",              "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "posting_type",        "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "num_of_positions",    "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "business_title",      "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "civil_service_title", "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "title_code_no",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "level",               "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_from",   "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_to",     "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_frequency",    "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "work_location",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
…
    { “name”: "geo_location",        "type": "Edm.GeographyPoint",     "searchable": false, "filterable": true, ...  "facetable": false, ... },
    { “name”: "tags",                "type": "Collection(Edm.String)", "searchable": true,  "filterable": true, ...  "facetable": true, ...  }
  ],
…
}
```

Merhaba örnek şemada gördüğünüz `Facetable` kimliği değerleri gibi modellerini olarak kullanılmaması dize alanları için devre dışı. Burada gerekmeyen kapalı olduğunu kapatma hello dizin hello boyutunu küçük tutmaya yardımcı olur ve genellikle performansı artırır.

> [!TIP]
> En iyi uygulama, her bir alan için dizin özniteliklerini hello kümesini içerir. Ancak `Facetable` kasıtlı olarak ayarlama, neredeyse tüm alanlar için varsayılan olarak her özniteliği, her bir şema kararı hello etkilerini düşündüğünüz yardımcı olabilir açıktır. 

<a name="checkdata"></a>

## <a name="check-hello-data"></a>Merhaba veri denetleyin
Merhaba, verilerinizin kalitesini beklediğiniz gibi hello modellenmiş bir gezinmede yapısı olup gerçeğe üzerinde doğrudan etkisi vardır. Ayrıca filtreleri tooreduce hello sonuç kümesi oluşturma kolaylığı hello de etkiler.

Marka veya fiyat toofacet istiyorsanız, her belge için değerler içermelidir *BrandName* ve *ProductPrice* geçerli, tutarlı ve üretken filtre seçeneği olarak.

Hangi tooscrub için birkaç anımsatıcı şunlardır:

* Tarafından toofacet istediğiniz her alan için kendiniz Self yönlendirilmiş aramada filtre olarak uygun değerleri içerip içermediğini isteyin. Merhaba değerleri kısa, açıklayıcı ve yeterince farklı toooffer rakip seçenekler arasında NET bir seçenek olmalıdır.
* Yazım hatası veya neredeyse eşleşen değerler. Varsa, model renk ve alan değerlerini içeren turuncu ve Ornage (bir yazım hatası), hello renk alanına dayalı bir modeli hem de çekme.
* Karışık büyük metin de turuncu ve iki farklı değerler olarak görünen turuncu modellenmiş bir gezinmede düzensizliğe benzer zararlar verecektir. 
* Tek ve çoğul aynı değeri her biri için ayrı bir modelinin neden hello sürümleri.

Hayal edebildiğiniz gibi hello verileri hazırlama içinde tespitlerini etkili modellenmiş bir gezinmede önemli bir yönüdür.

<a name="presentationlayer"></a>

## <a name="build-hello-ui"></a>Merhaba kullanıcı Arabirimi oluşturma
Geri hello sunu katmanı çalışma, aksi takdirde eksik ve gerekli toohello hangi özellikler anlamak gereksinimleri ortaya çıkarmaya Yardım deneyimi arayabilirsiniz.

Web ya da uygulama sayfanızı hello modellenmiş bir gezinmede yapısını görüntüler modellenmiş bir gezinmede bakımından hello sayfasında kullanıcı girişi algılar ve değiştirilen hello öğeleri ekler. 

Web uygulamaları için AJAX toorefresh artımlı değişiklikler izin verdiği için hello sunu katmanı yaygın olarak kullanılır. ASP.NET MVC veya tooan Azure Search Hizmeti HTTP üzerinden bağlanabilirsiniz herhangi bir görsel öğe platforma da kullanabilirsiniz. Merhaba örnek uygulaması başvurulan Bu makale--hello **Azure arama proje portalı Demo** – toobe bir ASP.NET MVC uygulaması olur.

Merhaba örnek modellenmiş bir gezinmede hello arama sonuçları sayfasına yerleşik olarak bulunur. Merhaba hello alınan örnekte, aşağıdaki `index.cshtml` dosya hello örnek uygulamasının modellenmiş bir gezinmede hello Search'te görüntüleme gösterir hello statik HTML yapısı sonuçları sayfası. modelleri Hello listesi yerleşik veya bir arama terimi göndermek ya da seçin veya bir model temizlediğinizde dinamik olarak yeniden.

```html
<div class="widget sidebar-widget jobs-filter-widget">
  <h5 class="widget-title">Filter Results</h5>
    <p id="filterReset"></p>
    <div class="widget-content">

      <h6 id="businessTitleFacetTitle">Business Title</h6>
      <ul class="filter-list" id="business_title_facets">
      </ul>

      <h6>Location</h6>
      <ul class="filter-list" id="posting_type_facets">
      </ul>

      <h6>Posting Type</h6>
      <ul class="filter-list" id="posting_type_facets"></ul>

      <h6>Minimum Salary</h6>
      <ul class="filter-list" id="salary_range_facets">
      </ul>

  </div>
</div>
```

Merhaba hello gelen kod parçacığını aşağıdaki `index.cshtml` sayfası hello HTML toodisplay hello ilk modeli, iş başlık dinamik olarak oluşturur. Benzer işlevler hello HTML hello için diğer yönleri dinamik olarak oluşturun. Bir etiket ve hello için model sonucunda ortaya çıkan bulunan öğelerin sayısını görüntüler bir sayısı her modeli vardır.

```js
function UpdateBusinessTitleFacets(data) {
  var facetResultsHTML = '';
  for (var i = 0; i < data.length; i++) {
    facetResultsHTML += '<li><a href="javascript:void(0)" onclick="ChooseBusinessTitleFacet(\'' + data[i].Value + '\');">' + data[i].Value + ' (' + data[i].Count + ')</span></a></li>';
  }

  $("#business_title_facets").html(facetResultsHTML);
}
```

> [!TIP]
> Merhaba arama sonuçları sayfasını tasarlarken, tooadd modelleri temizlemek için bir mekanizma unutmayın. Onay kutusu eklerseniz, nasıl tooclear hello filtreler kolayca görebilirsiniz. Diğer düzenleri için bir içerik haritası desen veya başka bir yaratıcı yaklaşım gerekebilir. Örneğin, hello iş arama Portal örnek uygulama, hello tıklayabilirsiniz `[X]` seçili modeli tooclear hello modeli sonra.

<a name="buildquery"></a>

## <a name="build-hello-query"></a>Merhaba sorgu oluşturma
sorgular oluşturmak için yazma hello kod, arama ifadeleri, modelleri, profilleri – herhangi bir şey Puanlama filtreleri de dahil olmak üzere geçerli bir sorgu tüm parçalarını tooformulate bir istek kullanılan belirtmeniz gerekir. Bu bölümde, biz modelleri bir sorgu ve filtreleri modelleri toodeliver ile nasıl kullanıldığı bir azaltılmış nerelerde keşfedin sonuç.

Modelleri Bu örnek uygulamasında tam sayı olduğuna dikkat edin. Merhaba proje portalı Demo Hello arama deneyimi modellenmiş bir gezinmede ve filtreleri tasarlanmıştır. Merhaba belirgin hello sayfasında modellenmiş bir gezinmede yerleşimini önem derecesini gösterir. 

Genellikle iyi toobegin örneğidir. Merhaba hello alınan örnekte, aşağıdaki `JobsSearch.cs` dosya, model Gezinti oluşturur isteğin tabanlı iş başlık, konum, nakil türü ve Minimum maaş derlemeleri. 

```cs
SearchParameters sp = new SearchParameters()
{
  ...
  // Add facets
  Facets = new List<String>() { "business_title", "posting_type", "level", "salary_range_from,interval:50000" },
};
```

Bir model sorgu parametresi tooa alanı ayarlanır ve içeren virgülle ayrılmış liste hello veri türüne bağlı olarak, daha fazla parametreli olabilir `count:<integer>`, `sort:<>`, `interval:<integer>`, ve `values:<list>`. Aralıkları ayarlarken değerler listesini sayısal veriler için desteklenir. Bkz: [Search belgeleri (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) kullanım ayrıntıları için.

Modelleri yanı sıra, uygulamanız tarafından şeklide hello isteği ayrıca filtreleri toonarrow model değeri seçime dayalı adayı belgeler hello kümesi aşağı oluşturması gerekir. Bir Bisiklet Mağazası için ipuçları tooquestions ister modellenmiş bir gezinmede sağlar *hangi renkler, üreticileri ve bisiklet türleri kullanılabilir?*. Filtreleme gibi sorulara yanıtlar *hangi tam bisiklet kırmızı, Sıradağlar bisiklet bu aralığı fiyat?*. Yalnızca kırmızı ürünlerini gösterilmesi gereken, "Red" tooindicate tıklattığınızda hello sonraki sorgu hello uygulaması gönderir içeren `$filter=Color eq ‘Red’`.

Merhaba hello gelen kod parçacığını aşağıdaki `JobsSearch.cs` sayfa eklerse seçili hello iş başlık toohello filtre hello iş başlık modeli bir değer seçin.

```cs
if (businessTitleFacet != "")
  filter = "business_title eq '" + businessTitleFacet + "'";
```

<a name="tips"></a> 

## <a name="tips-and-best-practices"></a>İpuçları ve en iyi yöntemler

### <a name="indexing-tips"></a>Dizin oluşturma ipuçları
**Bir arama kutusu kullanmazsanız dizin verimliliğini artırmak**

Uygulamanız çok yönlü gezinme özel olarak kullanıyorsa (diğer bir deyişle, hiçbir arama kutusu), hello alan olarak işaretleyebilirsiniz `searchable=false`, `facetable=true` tooproduce daha küçük bir dizin. Ayrıca, dizin oluşturma işlemi yalnızca tüm model değerlerle word kesme yok veya bir çok sözcüklü değerin bileşen bölümleri hello dizinini oluşur.

**Hangi alanların modelleri kullanılabileceğini belirtin**

Bu hello geri çağırma hello dizin şemasını belirleyen bir model olarak kullanılabilir toouse alanlardır. Bir alan modellenebilir olduğunu varsayarak, hello sorgu tarafından hangi alanların toofacet belirtir. Merhaba alan olduğunu olduğunuz altındaki hello etiketini görünür hello değerleri sağlar. 

her etiketin altında görünür hello değerleri hello dizinden alınır. Örneğin, hello modeli alan ise *renk*, hello ek filtreleme için kullanılabilir değerler hello bu alanın değerlerini - kırmızı, siyah ve benzeri.

Yalnızca sayısal ve tarih/saat değerleri için açıkça hello modeli alanında değerlerini ayarlayabilirsiniz (örneğin, `facet=Rating,values:1|2|3|4|5`). Değerler listesini Bu alan türleri toosimplify hello ayrılması modeli sonuçları bitişik aralıkları (sayısal değerleri veya dönemlere göre ya da aralıkları) içine izin verilir. 

**Varsayılan olarak yalnızca bir düzey modellenmiş bir gezinmede olabilir** 

Belirtildiği gibi bir hiyerarşideki modelleri iç içe geçme için doğrudan desteği yoktur. Varsayılan olarak, Azure Search'te modellenmiş bir gezinmede yalnızca bir düzey filtre destekler. Ancak, geçici çözümler mevcut. Hiyerarşik modeli yapısında kodlayabilir bir `Collection(Edm.String)` ile bir giriş noktası hiyerarşisi. Bu geçici çözüm uygulandığında, bu makalede hello kapsamında değildir. 

### <a name="querying-tips"></a>İpuçları sorgulama
**Alanları doğrula**

Dinamik olarak güvenilmeyen kullanıcı girişini temel alarak modelleri hello listesi yapılandırdıysanız, hello modellenmiş alanlarının hello adları geçerli olduğunu doğrulayın. Veya URL'leri kullanarak oluştururken hello adları kaçış `Uri.EscapeDataString()` .NET ya da hello platformunda seçim eşdeğer.

### <a name="filtering-tips"></a>Filtreleme ipuçları
**Arama duyarlık filtrelerle artırın**

Filtreleri kullanın. Üzerinde güveniyorsanız yalnızca arama ifadeleri başına kaynaklanan bir belge toobe neden olabilecek, hello kesin model değeri kendi alanların hiçbirini yok döndürdü.

**Filtrelerle arama performansı artırma**

Filtreler arama için aday belgeler hello kümesi daraltmak ve gelen sıralaması içermeyecek. Çok sayıda belgeleri varsa, detaya seçmeli modeli genellikle kullanarak, daha iyi performans sağlar.
  
**Filtre yalnızca hello modellenmiş alanları**

Modellenmiş ayrıntıya aşağı genellikle tooonly istediğiniz hello model değeri belirli (modellenmiş) alanında olmayan herhangi bir yere tüm aranabilir alanları olan belgeler dahildir. Bir filtre eklemeden hello hedef alan hello hizmet toosearch yalnızca alanındaki hello modellenmiş eşleşen değere yönlendirerek eklenir.

**Daha fazla filtrelerle modeli sonuçları kırpma**

Model sonuçları modeli terimiyle eşleşen hello arama sonuçlarında bulunan belgelerdir. Aşağıdaki örnek, arama sonuçlarında hello içinde *bulut bilgi işlem*, 254 öğeleri de *iç belirtimi* bir içerik türü. Öğeleri dışlayan olmak zorunda değildir. Bir öğe hem filtreleri hello ölçütlerini karşılıyorsa, her birinde sayılır. Bu çoğaltma mümkündür üzerinde olduğunu `Collection(Edm.String)` genellikle alanları kullanılan belge tooimplement etiketleme.

        Search term: "cloud computing"
        Content type
           Internal specification (254)
           Video (10) 

Genel olarak, görürseniz modeli sonuçları sürekli olarak çok büyük olduğundan, daha eklemenizi öneririz toogive kullanıcılar hello arama daraltma için daha fazla seçenek filtreler.

### <a name="tips-about-result-count"></a>Sonuç sayısı hakkında ipuçları

**Merhaba hello model Gezinti içindeki öğe sayısını sınırla**

Merhaba Gezinti ağacında her modellenmiş alan için bir varsayılan sınır 10 değer yoktur. Merhaba değerleri listesi tooa yönetilebilir boyutu tuttuğu için bu varsayılan gezinti yapıları için anlamlıdır. Bir değer toocount atayarak hello Varsayılanı geçersiz kılabilirsiniz.

* `&facet=city,count:5`sonuçları derece hello üst bulunan yalnızca hello ilk beş Şehir modeli sonucu olarak döndürüleceğini belirtir. Bir arama terimi "havaalanı" ve 32 eşleşen bir örnek sorgu göz önünde bulundurun. Merhaba sorgu belirtiyorsa `&facet=city,count:5`, ilk beş benzersiz Şehir hello arama sonuçlarında çoğu belgeler bulunmaktadır hello hello modeli sonuçları hello sadece.

Model sonuçları ve arama sonuçları arasında hello fark dikkat edin. Arama sonuçları hello sorguyla eşleşen tüm hello belgelerdir. Model sonuçlar her modeli değerle hello olur. Merhaba örnekte, arama sonuçları hello modeli sınıflandırması listesi (örneğimizde 5) olmayan Şehir adları içerir. Modelleri işaretini kaldırın veya şehir yanı sıra diğer yönleri seçin çok yönlü gezinmeyi filtrelenen sonuçları görünür hale gelmiştir. 

> [!NOTE]
> Ele `count` olduğunda birden çok tür kafa karıştırıcı olabilir. Merhaba aşağıdaki tabloda hello terim Azure Search API, örnek kod ve belgeleri nasıl kullanılacağı kısa bir özeti sunar. 

* `@colorFacet.count`<br/>
  Sunu kodda bir sayı parametresi hello modeli, model sonuç kullanılan toodisplay hello sayısı görmeniz gerekir. Model sonuçlarında sayısı hello modeli terim veya aralık eşleşen belgeleri hello sayısını gösterir.
* `&facet=City,count:12`<br/>
  Bir model sorgu sayısı tooa değeri ayarlayabilirsiniz.  Merhaba varsayılan 10'dur, ancak daha yüksek veya düşük ayarlayabilirsiniz. Ayarı `count:12` alır hello modeli sonuçlarında üst 12 eşleşmeleri göre belge sayısı.
* "`@odata.count`"<br/>
  Merhaba sorgu yanıt olarak, bu değer hello arama sonuçlarında eşleşen öğe hello sayısını gösterir. Ortalama olarak hello toplamı, hello arama terimiyle eşleşen öğeleri toohello varlığını birleştirilen tüm model sonuçları, daha büyük ancak herhangi bir model değeri eşleşme vardır.

**Model sonuçlarında sayılarını elde**

Bir filtre tooa modellenmiş sorgu eklediğinizde, tooretain hello modeli deyimi isteyebilir (örneğin, `facet=Rating&$filter=Rating ge 4`). Teknik olarak, model = değil derecelendirme gereklidir, ancak bunu tutma döndürür hello sayıları derecelendirmeler için model değerlerinin 4 ve üzeri. Örneğin, "4"'i tıklatın ve hello sorgu bir filtre içeren her derecelendirme 4 ve üzeri için büyük veya eşit için çok "4" sayıları döndürülür.  

**Doğru model sayılarını elde emin olun**

Belirli koşullar altında model sayıları hello sonuç kümeleri eşleşmiyor bulabilirsiniz (bkz [Azure Search'te (forum gönderisi) modellenmiş bir gezinmede](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).

Model sayıları toohello parçalama mimarisi tutarsız olabilir. Birden çok parça her arama dizini vardır ve her parça sonra tek bir sonuç birleştirilmiş belge sayısına göre hello ilk N modelleri raporlar. Başkalarının daha az varken bazı parça birçok eşleşen değerleri, varsa, bazı modeli değerleri eksik olan veya altında hello sonuçlarında sayılan bulabilirsiniz.

Bu davranış bugün karşılaşırsanız Bu davranış herhangi bir zamanda değişebilir rağmen çevresinde yapay hello sayısı inflating tarafından çalışabilirsiniz:<number> tooa büyük sayı tooenforce her parça raporlama tam. Varsa hello sayısı değeri: sıfırdan büyük veya eşit toohello sayıdır hello alanında benzersiz değerini, doğru sonuçlar garanti. Ancak, belge sayısını yüksek olduğunda bulunmaktadır performans, bu nedenle bu seçeneği dikkatli kullanın.

### <a name="user-interface-tips"></a>Kullanıcı arabirimi ipuçları
**Model Gezinti bölmesinde her bir alan için etiketler ekleme**

Etiketleri tipik hello HTML veya formunda tanımlanır (`index.cshtml` hello örnek uygulamasında). Azure Search'te model Gezinti etiketleri için API yok veya diğer meta verileri yok.

<a name="rangefacets"></a>

## <a name="filter-based-on-a-range"></a>Bir aralığı tabanlı filtresi
Değerleri aralığı üzerinden olduğunu ortak arama uygulaması gerekli değildir. Aralıkları sayısal veri ve DateTime değerleri için desteklenir. Daha fazla bilgiyi her yaklaşımı hakkında [Search belgeleri (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx).

Azure arama, bir aralık bilgi işlem için iki yaklaşım sağlayarak aralığı yapım basitleştirir. Her iki yaklaşımın için Azure Search hello sağladığınız hello girişleri verilen uygun aralıkların oluşturur. Örneğin, 10 aralık değerleri belirtirseniz | 20 | 30, otomatik olarak oluşturur, 0-10, 10-20, 20-30 aralıkları. Uygulamanızın isteğe bağlı olarak boş aralıkları kaldırabilirsiniz. 

**Yaklaşım 1: hello aralığı parametresini kullanın**  
tooset fiyat modelleri 10 artışlarla belirtirsiniz:`&facet=price,interval:10`

**Yaklaşım 2: değerler listesini kullanın**  
Sayısal veriler için değerler listesi kullanabilirsiniz.  Merhaba modeli aralığının göz önünde bulundurun bir `listPrice` gibi çizilir alan:

  ![Örnek değerler listesi][5]

bir model aralığı gibi bir ekran görüntüsü önceki hello hello toospecify değerler listesini kullanın:

    facet=listPrice,values:10|25|100|500|1000|2500

Her aralık hello önceki aralığı toocreate ayrık aralıklarına kırpılır ve bir uç nokta olarak hello listesinden bir değer bir başlangıç noktası olarak 0 kullanarak yerleşik olarak bulunur. Azure arama modellenmiş bir gezinmede bir parçası olarak bu işlemi yapar. Her aralık yapılandırılması için toowrite koduna sahip değil.

### <a name="build-a-filter-for-a-range"></a>Bir aralık için bir filtre oluşturun
Seçtiğiniz bir aralığı tabanlı toofilter belgeleri hello kullanabilir `"ge"` ve `"lt"` filtre hello aralığının hello uç noktalarını tanımlayan iki parçalı ifadesi işleçler. Seçerseniz, örneğin, aralığı 10-25 için hello bir `listPrice` alanı hello filtre olacaktır `$filter=listPrice ge 10 and listPrice lt 25`. Merhaba örnek kodda hello filtre ifadesi kullanan **priceFrom** ve **priceTo** parametreleri tooset hello uç noktaları. 

  ![Bir değer aralığı için sorgu][6]

<a name="geofacets"></a> 

## <a name="filter-based-on-distance"></a>Uzaklık üzerinde göre filtrele
Kendi ortak toosee bir mağaza, Restoran ya da kendi yakınlık tooyour geçerli konumuna bağlı hedef seçtiğiniz yardımcı filtreler. Bu tür filtresini modellenmiş bir gezinmede gibi görünebilir, ancak bunu yalnızca bir filtredir. Biz buraya uygulama öneriler, belirli tasarım sorunu için özellikle istiyorsunuz, bu için Bahsediyor.

Azure Search'te iki Jeo-uzamsal işlevleri vardır **geo.distance** ve **geo.intersects**.

* Merhaba **geo.distance** işlevi arasında iki nokta içinde kilometre hello uzaklığını döndürür. Bir noktadan bir alan ve diğer hello filtre bir parçası olarak geçirilen bir sabit değer. 
* Merhaba **geo.intersects** işlevi verilen bir noktaya içinde belirli bir Çokgen ise true döndürür. başlangıç noktası bir alan ve hello Çokgen hello filtre bir parçası olarak geçirilen koordinatları sabit listesi olarak belirtilir.

Filtre örneklerde bulabilirsiniz [OData ifadesi sözdizimi (Azure Search)](http://msdn.microsoft.com/library/azure/dn798921.aspx).

<a name="tryitout"></a>

## <a name="try-hello-demo"></a>Merhaba Tanıtımı deneyin
Hello Azure arama proje portalı Demo bu makalede başvurulan hello örnekler yer almaktadır.

-   Bakın ve test hello çalışma demo çevrimiçi adresindeki [Azure arama proje portalı Demo](http://azjobsdemo.azurewebsites.net/).

-   Merhaba kodu hello indirme [Azure-Samples bağlantıların github'da](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).

Arama sonuçları ile çalışırken, hello URL sorgu yapım değişiklikler için izleyin. Tek tek seçerek bu uygulama tooappend modelleri toohello URI olur.

1. toouse hello eşleme hello tanıtım uygulamasını işlevselliğini hello bir Bing Haritalar anahtarı alma [Bing Haritalar Geliştirme Merkezi](https://www.bingmapsportal.com/). Merhaba hello varolan anahtarı üzerinden yapıştırın `index.cshtml` sayfası. Merhaba `BingApiKey` hello ayarı `Web.config` dosya kullanılmaz. 

2. Merhaba uygulamayı çalıştırın. Merhaba isteğe bağlı tura katılın veya hello iletişim kutusunu kapatın.
   
3. "Analist" gibi bir arama terimi girin ve hello arama simgesine tıklayın. hızlı bir şekilde Hello sorgusunu çalıştırır.
   
   Modellenmiş bir gezinmede yapısı da hello Arama sonuçlarıyla döndürülür. Merhaba arama sonuçları sayfasında hello modellenmiş bir gezinmede yapısı her modeli sonucu sayılarını içerir. Hiçbir modelleri seçildi bu nedenle tüm eşleşen sonuç döndürmedi.
   
   ![Modelleri seçmeden önce arama sonuçları][11]

4. Bir iş başlık, konum veya en düşük maaş'ı tıklatın. Modelleri hello ilk Search'te null, ancak değerler aldıkları gibi hello arama sonuçları artık eşleşen öğeleri atılır.
   
   ![Modelleri seçtikten sonra arama sonuçları][12]

5. tooclear hello modellenmiş farklı sorgu davranışları deneyebilirsiniz böylece sorgusu hello `[X]` modelleri tooclear hello modelleri hello seçtikten sonra.
   
<a name="nextstep"></a>

## <a name="learn-more"></a>Daha fazla bilgi edinin
Gözcü [Azure arama derinlemesine](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410). 45:25 hakkında bir tanıtım yoktur tooimplement yönü.

Tasarım ilkeleri modellenmiş gezinmesine daha fazla bilgiler için bağlantılar aşağıdaki hello öneririz:

* [Modellenmiş Ara tasarlama](http://www.uie.com/articles/faceted_search/)
* [Tasarım desenleri: Çok yönlü gezinme](http://alistapart.com/article/design-patterns-faceted-navigation)


<!--Anchors-->
[How toobuild it]: #howtobuildit
[Build hello presentation layer]: #presentationlayer
[Build hello index]: #buildindex
[Check for data quality]: #checkdata
[Build hello query]: #buildquery
[Tips on how toocontrol faceted navigation]: #tips
[Faceted navigation based on range values]: #rangefacets
[Faceted navigation based on GeoPoints]: #geofacets
[Try it out]: #tryitout

<!--Image references-->
[1]: ./media/search-faceted-navigation/azure-search-faceting-example.PNG
[2]: ./media/search-faceted-navigation/Facet-2-CSHTML.PNG
[3]: ./media/search-faceted-navigation/Facet-3-schema.PNG
[4]: ./media/search-faceted-navigation/Facet-4-SearchMethod.PNG
[5]: ./media/search-faceted-navigation/Facet-5-Prices.PNG
[6]: ./media/search-faceted-navigation/Facet-6-buildfilter.PNG
[7]: ./media/search-faceted-navigation/Facet-7-appstart.png
[8]: ./media/search-faceted-navigation/Facet-8-appbike.png
[9]: ./media/search-faceted-navigation/Facet-9-appbikefaceted.png
[10]: ./media/search-faceted-navigation/Facet-10-appTitle.png
[11]: ./media/search-faceted-navigation/faceted-search-before-facets.png
[12]: ./media/search-faceted-navigation/faceted-search-after-facets.png

<!--Link references-->
[Designing for Faceted Search]: http://www.uie.com/articles/faceted_search/
[Design Patterns: Faceted Navigation]: http://alistapart.com/article/design-patterns-faceted-navigation
[Create your first application]: search-create-first-solution.md
[OData expression syntax (Azure Search)]: http://msdn.microsoft.com/library/azure/dn798921.aspx
[Azure Search Adventure Works Demo]: https://azuresearchadventureworksdemo.codeplex.com/
[http://www.odata.org/documentation/odata-version-2-0/overview/]: http://www.odata.org/documentation/odata-version-2-0/overview/ 
[Faceting on Azure Search forum post]: ../faceting-on-azure-search.md?forum=azuresearch
[Search Documents (Azure Search API)]: http://msdn.microsoft.com/library/azure/dn798927.aspx

