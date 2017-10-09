---
title: "aaaGuide toocreating hello Market için veri hizmeti | Microsoft Docs"
description: "Nasıl toocreate, onaylamak ve dağıtmak için bir veri hizmeti ayrıntılı yönergeler hello üzerinde Azure Market satın alın."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 107baab2-5828-4158-abdf-59a580c80d37
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: e3d88412389d43d104662dc4434363b6ad9475f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-nodes-schema-for-mapping-an-existing-web-service-tooodata-through-csdl"></a>Var olan bir web hizmeti tooOData CSDL aracılığıyla eşleme hello düğümleri şemasını anlama
> [!IMPORTANT]
> **Şu anda artık ekleme duyuyoruz herhangi yeni veri hizmeti yayımcılar. Yeni dataservices listesine onaylanmamış.** Bir SaaS iş uygulaması varsa toopublish istediğiniz AppSource hakkında daha fazla bilgi bulabilirsiniz [burada](https://appsource.microsoft.com/partners). Bir Iaas uygulamalar varsa veya Geliştirici hizmeti misiniz Azure Market'te toopublish gibi daha fazla bilgi bulabilirsiniz [burada](https://azure.microsoft.com/marketplace/programs/certified/).
>
>

Bu belge, bir OData Protokolü tooCSDL eşleme hello düğümü yapısı açıklamak yardımcı olur. XML toonote hello düğümü yapısı iyi biçimlendirilmiş önemlidir. Bu nedenle, OData eşleme tasarlarken kök, üst ve alt şema geçerlidir.

## <a name="ignored-elements"></a>Yoksayılan öğeleri
Merhaba, hello web Service'in meta verileri hello içeri aktarma sırasında hello Azure Marketi arka ucu tarafından kullanılan toobe yapmayacağınız hello yüksek düzey CSDL öğeleri (XML düğümlerini) şunlardır. Bunlar, mevcut olabilir ancak göz ardı edilir.

| Öğesi | Kapsam |
| --- | --- |
| Öğesini kullanarak |Başlangıç düğümü, alt düğümleri ve tüm öznitelikleri |
| Documentation öğesi |Başlangıç düğümü, alt düğümleri ve tüm öznitelikleri |
| ComplexType |Başlangıç düğümü, alt düğümleri ve tüm öznitelikleri |
| İlişkilendirme öğesi |Başlangıç düğümü, alt düğümleri ve tüm öznitelikleri |
| Genişletilmiş özellik |Başlangıç düğümü, alt düğümleri ve tüm öznitelikleri |
| EntityContainer |Merhaba aşağıdaki öznitelikleri göz ardı edilir yalnızca: *genişletir* ve *AssociationSet* |
| Şema |Merhaba aşağıdaki öznitelikleri göz ardı edilir yalnızca: *Namespace* |
| Functionımport |Merhaba aşağıdaki öznitelikleri göz ardı edilir yalnızca: *modu* (ln varsayılan değerini kabul edilir) |
| EntityType |Merhaba aşağıdaki alt düğümler göz ardı edilir yalnızca: *anahtar* ve *PropertyRef* |

Merhaba hello (eklenir ve öğeleri göz ardı) değişiklikleri toohello çeşitli CSDL XML düğümlerini ayrıntılı açıklanmıştır.

## <a name="functionimport-node"></a>Functionımport düğümü
Bir Functionımport düğümü hizmet toohello son kullanıcı kullanıma sunan bir URL (giriş noktası) temsil eder. Merhaba düğümü hello URL nasıl ele, kullanılabilir toohello son kullanıcı parametreleridir ve bu parametrelerin nasıl sağlanır açıklayan sağlar.

Bu düğümün ayrıntılarını [burada] bulundu[MSDNFunctionImportLink](https://msdn.microsoft.com/library/cc716710.aspx)

Merhaba hello ek öznitelikler (veya eklemeler tooattributes) şunlardır hello Functionımport düğümü tarafından sunulur:

**d:BaseUri** -hello URI şablonunu gösterilen tooMarketplace hello REST kaynak. Market hello şablonu tooconstruct sorguları hello REST web hizmeti kullanır. Merhaba URI şablonunu parameterName hello parametresinin hello adı olduğu {parameterName} hello biçiminde hello parametreleri yer tutucular içerir. Örn apiVersion = {apiVersion}.
Parametreleri tooappear URI parametreleri olarak veya hello URI yolu bir parçası olarak izin verilir. Merhaba yolundaki hello görünümünü hello durumda bunlar her zaman zorunlu (null'olarak işaretlenemez). *Örnek:*`d:BaseUri="http://api.MyWeb.com/Site/{url}/v1/visits?start={start}&amp;end={end}&amp;ApiKey=3fadcaa&amp;Format=XML"`

**Ad** -hello hello adını alınan işlev.  Olamaz olması hello hello CSDL tanımlanan diğer adları ile aynı.  Örn Adı "GetModelUsageFile" =

**EntitySet** *(isteğe bağlı)* - hello işlevi bir varlık türleri koleksiyonunu, hello hello değerini döndürürse **EntitySet** hello varlık kümesi toowhich hello koleksiyonu ait olması gerekir. Aksi takdirde hello **EntitySet** özniteliği değil kullanılmalıdır. *Örnek:*`EntitySet="GetUsageStatisticsEntitySet"`

**ReturnType** *(isteğe bağlı)* -hello URI tarafından döndürülen öğelerin hello türünü belirtir.  Merhaba işlevi bir değer döndürmezse, bu öznitelik kullanmayın. Merhaba, desteklenen hello türleri şunlardır:

* **Koleksiyon (<Entity type name>)**: tanımlı varlık türleri koleksiyonunu belirtir. Merhaba EntityType düğümün adı özniteliği hello Hello adı yok. Bir örnek koleksiyonudur (WXC. HourlyResult).
* **Ham (<mime type>)**: ham belge/toohello kullanıcı döndürülen blob belirtir. Örnek Raw(image/jpeg) diğer örnekleri olan:

  * ReturnType="Raw(text/plain)"
  * ReturnType = "derleme (sage. DeleteAllUsageFilesEntity) "*

**d:Paging** -disk belleği REST kaynak hello tarafından nasıl işleneceğini belirtir. parametre değerleri süslü braches içinde kullanılan Merhaba, örneğin sayfa {$page} = & ItemsPerPage sıfırdan küçük = {$size} hello seçenekleri kullanılabilir:

* **Hiçbiri:** hiçbir disk belleği kullanılabilir
* **Atla:** disk belleği mantıksal "Atla" ve "Al" (üst) ile ifade edilir. Sonraki N öğeleri döndürür hello sonra Atla M öğeleri ve Al atlar. Parametre değeri: $skip
* **Take:** Al hello sonraki N öğesini döndürür. Parametre değeri: $take
* **PageSize:** disk belleği mantıksal sayfasını ve boyutu (sayfa başına öğe) ile ifade edilir. Sayfa döndürülen hello geçerli sayfasını temsil eder. Parametre değeri: $page
* **Boyut:** boyutu hello her bir sayfa için döndürülen öğe sayısını temsil eder. Parametre değeri: $size

**d:AllowedHttpMethods** *(isteğe bağlı)* -hangi fiil hello REST kaynak tarafından ele belirtir. Ayrıca, belirtilen kabul edilen fiili toohello kısıtlayan değeri.  Varsayılan POST =.  *Örnek:* `d:AllowedHttpMethods="GET"` hello seçenekleri kullanılabilir:

* **GET:** genellikle kullanılan tooreturn veri
* **POST:** genellikle kullanılan tooinsert yeni veri
* **PUT:** genellikle kullanılan tooupdate veri
* **SİLME:** toodelete veri kullanılan

Merhaba Functionımport düğümü içinde ek alt düğümleri (Merhaba CSDL belgelerinde ele alınmamaktadır) şunlardır:

**d:RequestBody** *(isteğe bağlı)* -hello istek gövdesi olduğundan isteği hello kullanılan tooindicate gönderilen bir gövde toobe bekliyor. Parametreleri hello istek gövdesinde verilebilir. Süslü ayraç içinde örneğin belirtilmiştir {parameterName}. Bu parametreler eşlenmedi hello kullanıcı girişi olduğundan hello gövdesine toohello içerik sağlayıcının hizmeti aktarılan. Merhaba requestBody öğesi adı httpMethod özniteliği var. Merhaba özniteliği iki değer sağlar:

* **POST:** hello bir HTTP POST isteğiyse kullanılan
* **GET:** hello İstek HTTP GET ise kullanılan

    Örnek:

        `<d:RequestBody d:httpMethod="POST">
        <![CDATA[
        <req1:Request xmlns:r1="http://schemas.mysite.com//generic/requests/1" Version="1.0">
        <req1:Query>{Query}</req1:Query><req1:AppId>D453474</req1:AppId>
        <req:DestinationSchemas><req1:Schema>Generic.RequestResponse[1.0]</req1:Schema>
        </req1:DestinationSchemas>
        </req1: Request>
        ]]>
        </d:RequestBody>`

**d:namespaces** ve **d:Namespace** -bu düğüm hello hello işlevi alma (URI uç noktası) tarafından döndürülen XML tanımlanan hello ad alanları açıklar. Merhaba hello arka uç hizmeti tarafından döndürülen XML ad alanları toodifferentiate hello içeriğinin döndürülen herhangi bir sayı içerebilir. **Tüm d:Map veya d:Match XPath sorguları kullandıysanız bu ad alanları, listelenen toobe gerekir.** Merhaba d:Namespaces düğüm d:Namespace düğümleri kümesi/listesi içerir. Bunların her birini hello arka uç hizmeti yanıtında kullanılacak bir ad alanını listeler. Merhaba, hello özniteliği hello d:Namespace düğümünün şunlardır:

* **d:prefix:** hello hizmet tarafından döndürülen hello XML sonuçlarında ör f:FirstName, f hello öneki olduğu f:LastName görüldüğü gibi hello hello ad alanı öneki.
* **d:Uri:** hello sonuç belgede kullanılan hello ad alanının tam URI hello. Merhaba değerini temsil eder çözümlenmiş tooat çalışma zamanı bu hello önekidir.

**d:ErrorHandling** *(isteğe bağlı)* -bu düğüm hata işleme koşulları içerir. Merhaba koşullardan her biri hello içerik sağlayıcının hizmet tarafından döndürülen hello sonuç doğrulanır. Bir koşul HTTP hata kodunu önerilen hello eşleşmesi durumunda bir hata iletisi toohello son kullanıcı döndürülür.

**d:ErrorHandling** *(isteğe bağlı)* ve **d:Condition** *(isteğe bağlı)* -bir koşul düğümü tarafından döndürülen hello sonuç işaretli bir koşul tutar Merhaba içerik sağlayıcının hizmeti. Merhaba hello şunlardır **gerekli** öznitelikleri:

* **d:match:** animasyonun çıktı XML belirli bir düğüm/değeri hello içerik sağlayıcısında mevcut olup olmadığını doğrulayan bir XPath ifadesi. Hello XPath hello çıkış karşı çalışır ve bir eşleşme ya da false hello koşul Aksi durumda ise, true değerini döndürmelidir.
* **d:HttpStatusCode:** hello Marketi tarafından hello servis talebi hello koşul eşleştiğinden döndürülmelidir HTTP durum kodu. Market hataları toohello kullanıcı HTTP durum kodları aracılığıyla signalizes. HTTP durum kodları listesini http://en.wikipedia.org/wiki/HTTP_status_code kullanılabilir
* **d:ErrorMessage:** – ile Merhaba HTTP durum kodu – döndürülen toohello son kullanıcı hello hata iletisi. Bu, tüm gizli içermiyor kolay hata iletisi olmalıdır.

**d:title** *(isteğe bağlı)* -hello işlevi hello başlığı açıklayan sağlar. Merhaba başlık Hello değeri geldiği

* Burada toofind hello başlık hello yanıt hello hizmet isteğinden döndürülen belirten hello isteğe bağlı eşleme özniteliği (xpath).
* - Veya - hello düğüm değeri olarak belirtilen hello başlığı.

**d:Rights** *(isteğe bağlı)* -hello hello işlev ile ilişkili hakları (örneğin telif hakkı). Merhaba hakları Hello değeri geldiği:

* Burada toofind hello hakları hello yanıt hello hizmet isteğinden döndürülen belirten hello isteğe bağlı eşleme özniteliği (xpath).
* - Veya - hello düğüm değeri olarak belirtilen hello hakları.

**d:description** *(isteğe bağlı)* - A kısa hello işlevi için bir açıklama. Merhaba açıklama Hello değeri geldiği

* Burada toofind hello açıklama hello yanıt hello hizmet isteğinden döndürülen belirten hello isteğe bağlı eşleme özniteliği (xpath).
* - Veya – hello düğüm değeri olarak belirtilen hello açıklaması.

**d:EmitSelfLink** - *yukarıdaki örnekte "Functionımport 'disk 'belleği döndürülen veriler aracılığıyla için" konusuna bakın*

**d:EncodeParameterValue** -isteğe bağlı uzantı tooOData

**d:QueryResourceCost** -isteğe bağlı uzantı tooOData

**d:Map** -isteğe bağlı uzantı tooOData

**d:Headers** -isteğe bağlı uzantı tooOData

**d:Headers** -isteğe bağlı uzantı tooOData

**d:Value** -isteğe bağlı uzantı tooOData

**d:HttpStatusCode** -isteğe bağlı uzantı tooOData

**d:ErrorMessage** -isteğe bağlı uzantı tooOData

## <a name="parameter-node"></a>Parametre düğümü
Bu düğümün temsil ettiği hello URI şablonunu bir parçası olarak kullanıma sunulan bir parametre / istek hello Functionımport düğümünde belirtilen gövdesi.

Merhaba "Parametresi öğe" düğümü hakkında çok yararlı Ayrıntılar belge sayfası bulunduğu konum [burada](http://msdn.microsoft.com/library/ee473431.aspx) (kullanımı hello **diğer sürüm** açılır tooselect gerekli tooview belgelerine Merhaba, farklı bir sürüm). *Örnek:*`<Parameter Name="Query" Nullable="false" Mode="In" Type="String" d:Description="Query" d:SampleValues="Rudy Duck" d:EncodeParameterValue="true" MaxLength="255" FixedLength="false" Unicode="false" annotation:StoreGeneratedPattern="Identity"/>`

| Parametre özniteliği | Gereklidir | Değer |
| --- | --- | --- |
| Ad |Evet |Merhaba parametresinin Hello adı. Büyük küçük harf duyarlı!  Merhaba tabanURI harf **Örnek:**`<Property Name="IsDormant" Type="Byte" />` |
| Tür |Evet |Merhaba parametre türü. Merhaba değeri olmalıdır bir **EDMSimpleType** veya hello hello modeli kapsamında olmayan bir karmaşık tür. Daha fazla bilgi için "6 desteklenen parametre/özellik türleri" bölümüne bakın.  (Büyük küçük harfe duyarlı! İlk karakter büyük harf, rest küçük.)  Ayrıca bkz, [kavramsal Model türü (CSDL)][MSDNParameterLink](http://msdn.microsoft.com/library/bb399548.aspx). **Örnek:**`<Property Name="LimitedPartnershipID " Type="Int32" />` |
| Modu |Hayır |**İçinde**, Out ve Inout hello parametresi bir giriş, çıkış veya giriş/çıkış parametresi olduğuna bağlı olarak. (Yalnızca "IN" Azure Marketi'nde kullanılabilir.) **Örnek:**`<Parameter Name="StudentID" Mode="In" Type="Int32" />` |
| maxLength |Hayır |Merhaba en hello parametresinin uzunluğu izin verilir. **Örnek:**`<Property Name="URI" Type="String" MaxLength="100" FixedLength="false" Unicode="false" />` |
| Duyarlılık |Hayır |Merhaba duyarlık hello parametresi. **Örnek:**`<Property Name="PreviousDate" Type="DateTime" Precision="0" />` |
| Ölçek |Hayır |Merhaba parametre ölçeğini Hello. **Örnek:**`<Property Name="SICCode" Type="Decimal" Precision="10" Scale="0" />` |

Merhaba, toohello CSDL belirtimi eklenen hello öznitelikleri şunlardır:

| Parametre özniteliği | Açıklama |
| --- | --- |
| **d:Regex** *(isteğe bağlı)* |Regex ifadesi toovalidate hello giriş değeri Merhaba parametresi kullanılır. Merhaba giriş değeri hello deyimi hello değeri eşleşmiyorsa reddedilir. Bu toospecify de olası değerler, örneğin sağlar ^ [0-9] +? $ tooonly numaraları izin verin. **Örnek:** ' < parametre adı "ad" modu = "İçinde" Type = "Dize" d =: boş değer atanabilir = "false" d:Regex = "^ [a-zA-Z] * $" d:Description "bir boşluk ya da alfasayısal olmayan İngilizce olmayan karakterler içeremez ad" d:SampleValues = "Hasan = |
| **d:Enum** *(isteğe bağlı)* |Bir kanal ayrılmış hello parametresi için geçerli değerlerin listesi. Merhaba değerlerin Hello türü hello parametresinin toomatch tanımlanan hello türü gerekiyor. Örnek: ' İngilizce |
| **d: boş değer atanabilir** *(isteğe bağlı)* |Bir parametre null olup olamayacağını tanımlanmasına olanak sağlar. Merhaba varsayılan değer: true. Ancak, hello URI şablonunu hello yolunda bir parçası olarak sunulan parametreleri null olamaz. Bu parametrelerin – toofalse Hello öznitelik ayarlandığında hello kullanıcı girişi geçersiz kılındı. **Örnek:**`<Parameter Name="BikeType" Type="String" Mode="In" Nullable="false"/>` |
| **d:SampleValue** *(isteğe bağlı)* |Örnek değer toodisplay hello UI bir not toohello istemci olarak.  Olası tooadd ayrılmış bir kanal kullanarak birkaç değerler listesinde, yani ' bir |

## <a name="entitytype-node"></a>EntityType düğümü
Bu düğüm Market toohello son kullanıcıdan döndürülen hello türlerinden birini temsil eder. Ayrıca, toohello son kullanıcı tarafından döndürülen hello içerik sağlayıcının hizmet toohello değerlerini tarafından döndürülen hello çıktısından hello eşleme içerir.

Bu düğümün ayrıntılarını konumunda bulunan [burada](http://msdn.microsoft.com/library/bb399206.aspx) (kullanımı hello **diğer sürüm** açılır tooselect gerekli tooview belgelerine Merhaba, farklı bir sürümü.)

| Öznitelik adı | Gereklidir | Değer |
| --- | --- | --- |
| Ad |Evet |Merhaba varlık türünün Hello adı. **Örnek:**`<EntityType Name="ListOfAllEntities" d:Map="//EntityModel">` |
| BaseType |Hayır |Merhaba tanımlanıyorsa hello varlık türünün temel türü başka bir varlık türünün Hello adı. **Örnek:**`<EntityType Name="PhoneRecord" BaseType="dqs:RequestRecord">` |

Merhaba, toohello CSDL belirtimi eklenen hello öznitelikleri şunlardır:

**d:Map** -hello hizmet çıkış karşı yürütülen bir XPath ifadesi. Merhaba burada where ATOM akışı gibi hello hizmet çıkış yineleyin, öğeleri kümesini içeren varsayılır yineleyin Giriş düğümleri kümesi yok. Her bu düğümler yinelenen bir kayıt içerir. tek bir kaydın hello değerlerini tutan hello bağımsız tekrarlanan düğümde hello içerik sağlayıcının hizmet sonuç belirtilen toopoint sonra hello XPath olur. Örnek: Merhaba hizmetinden çıktı

        `<foo>
          <bar> … content … </bar>
          <bar> … content … </bar>
          <bar> … content … </bar>
        </foo>`

Her hello çubuğu düğümünün hello düğümünde çıkış ve toohello son kullanıcı döndürülen hello gerçek içeriği içeren yinelenen hello olduğundan hello XPath ifadesi /foo/bar olacaktır.

**Anahtar** -bu öznitelik Marketi tarafından göz ardı edilir. REST tabanlı web services, genel bir birincil anahtar sunmayın.

## <a name="property-node"></a>Özelliği düğümü
Bu düğüm hello kaydının bir özellik içerir.

Bu düğümün ayrıntılarını konumunda bulunan [http://msdn.microsoft.com/library/bb399546.aspx](http://msdn.microsoft.com/library/bb399546.aspx) (kullanımı hello **diğer sürüm** açılır tooselect gerekli tooview belgelerine Merhaba, farklı bir sürümü.) *Örnek:*`<EntityType Name="MetaDataEntityType" d:Map="/MyXMLPath">
        <Property Name="Name"     Type="String" Nullable="true" d:Map="./Service/Name" d:IsPrimaryKey="true" DefaultValue=”Joe Doh” MaxLength="25" FixedLength="true" />
        ...
        </EntityType>`

| AttributeName | Gerekli | Değer |
| --- | --- | --- |
| Ad |Evet |Merhaba özelliğinin Hello adı. |
| Tür |Evet |Başlangıç özellik değeri Hello türü. Başlangıç özellik değeri türü olmalıdır bir **EDMSimpleType** veya hello modeli kapsamında (bir tam ad tarafından gösterilen) bir karmaşık türü. Daha fazla bilgi için kavramsal Model türü (CSDL) bakın. |
| Boş değer atanabilir |Hayır |**Doğru** (Merhaba varsayılan değer) veya **False** hello özelliği bir null değere sahip olup bağlı olarak. Not: hello CSDL sürümünü belirtilen hello tarafından [http://schemas.microsoft.com/ado/2006/04/edm](http://schemas.microsoft.com/ado/2006/04/edm) ad alanı, bir karmaşık tür özelliği null atanabilir olmalıdır = "False". |
| defaultValue |Hayır |Merhaba hello özelliğinin varsayılan değeri. |
| maxLength |Hayır |Başlangıç özellik değeri en büyük uzunluğu Hello. |
| FixedLength |Hayır |**Doğru** veya **False** hello özellik değeri fiexed uzunlukta bir dize olarak depolanan bağlı olarak. |
| Duyarlılık |Hayır |Merhaba sayısal değeri basamak tooretain toohello sayısını ifade eder. |
| Ölçek |Hayır |Merhaba sayısal değeri ondalık tooretain maksimum sayısı. |
| Unicode |Hayır |**Doğru** veya **False** olup hello özellik değeri olması bağlı olarak bir UNICODE dizesi depolanır. |
| Harmanlama |Hayır |Merhaba veri kaynağında kullanılan dizisi toobe harmanlama hello belirten bir dize. |
| ConcurrencyMode |Hayır |**Hiçbiri** (Merhaba varsayılan değer) veya **sabit**. Merhaba değeri çok ayarlanırsa**sabit**, iyimser eşzamanlılık denetimlerinde hello özellik değeri kullanılacak. |

Merhaba, toohello CSDL belirtimi eklenen hello ek öznitelikleri şunlardır:

**d:Map** -hello hizmet karşı yürütülen XPath ifadesi çıkış ve hello çıktının bir özellik ayıklar. Merhaba belirtilen XPath göreli toohello yineleyen hello EntityType düğümün XPath Seçili düğüm ' dir. Aynı zamanda statik kaynak her hello gibi bir mutlak XPath tooallow hello özgün hizmeti, çıktı ancak her hello OData hello satır mevcut olması gereken sonra yalnızca bulunan örneğin bir telif hakkı bildirimi gibi düğümler çıkış olası toospecify olan çıktı. Örnek hello hizmetinden:

        `<foo>
          <bar>
           <baz0>… value …</baz0>
           <baz1>… value …</baz1>
           <baz2>… value …</baz2>
          </bar>
        </foo>`

Burada Hello XPath ifadesi ./bar/baz0 tooget hello baz0 düğüm hello içerik sağlayıcının hizmetinden olacaktır.

**d:CharMaxLength** -dize türü için uzunluk üst hello belirtebilirsiniz. DataService CSDL örneğe bakın

**d:IsPrimaryKey** -hello sütun hello tablosunun/görünümünün birincil anahtar hello olup olmadığını gösterir. DataService CSDL örneğe bakın.

**d:isExposed** -hello tablo şemasını sunulur belirler (genellikle gerçek). DataService CSDL örneğe bakın

**d:IsView** *(isteğe bağlı)* - Bu tablo yerine bir görünümü temel alıyorsa true.  DataService CSDL örneğe bakın

**d:Tableschema** -DataService CSDL örnek bakın

**d:ColumnName** -hello tablo/görünüm hello sütununda hello adıdır.  DataService CSDL örneğe bakın

**d:IsReturned** -hello hello hizmet bu değeri toohello istemci göstermiyorsa belirler Boole değeri değil.  DataService CSDL örneğe bakın

**d:IsQueryable** -hello hello sütun bir veritabanı sorgusu kullanılıp kullanılamayacağını belirler Boole değeri değil.   DataService CSDL örneğe bakın

**d:OrdinalPosition** -x, hello tablodaki sütun sayısı 1 toohello gelen hello sütunun sayısal görünümü, x, hello tablo veya hello görünümünde konumudur.  DataService CSDL örneğe bakın

**d:DatabaseDataType** -hello veritabanında, yani SQL veri türü hello sütunun hello veri türüdür. DataService CSDL örneğe bakın

## <a name="supported-parametersproperty-types"></a>Desteklenen parametreler/özellik türleri
Merhaba, parametreleri ve özellikleri için desteklenen hello türleri verilmiştir. (Büyük küçük harf duyarlı)

| İlkel türler | Açıklama |
| --- | --- |
| Null |Bir değer Hello yokluğu temsil eder |
| Boole değeri |Merhaba matematiksel kavramını ikili değerli mantığı temsil eder |
| Bayt |İmzasız 8 bit tam sayı değeri |
| Tarih saat |Tarih ve saat 1 Ocak 1753 gece 12:00:00 gece arasında değişen değerler ile temsil eder 11:59:59 P.M, Aralık 9999 M.S. |
| Ondalık |Sabit duyarlık ve ölçek ile sayı değerleri temsil eder. Bu tür negatif 10'dan arasında değişen bir sayısal değer açıklayabilirsiniz ^ 255 + 1 toopositive 10 ^ 255 -1 |
| Çift |Kayan noktalı sayı ± 2.23e-308 ile ± 1, 79E yaklaşık aralığını değerlerle gösterebilir 15 basamağa duyarlık ile temsil eden +308. **Ondalık tooExel verme sorunu kullanın:** |
| Tek |Kayan noktalı sayı ± 1.18e-38 ile ± 3.40e yaklaşık aralığını değerlerle gösterebilir 7 basamağa duyarlık ile temsil eden +38 |
| GUID |Bir 16 bayt (128-bit) benzersiz tanımlayıcısı değeri temsil eder |
| Int16 |İşaretli 16 bit tam sayı değerini temsil eder |
| Int32 |İşaretli 32 bit tamsayı değeri temsil eder |
| Int64 |İşaretli 64-bit tamsayı değeri temsil eder |
| Dize |Sabit - veya değişken uzunlukta karakter veri temsil eder |

## <a name="see-also"></a>Ayrıca Bkz.
* İçinde anlama ilgileniyorsanız hello genel OData eşleme işlemi ve amacı, bu makalede okuma [veri hizmeti OData eşleme](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview tanımları, yapılar ve yönergeler.
* Örnekler gözden geçirme ilgileniyorsanız, bu makaleyi okuyun [veri hizmeti OData eşleme örnekler](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee örnek kod ve kod sözdizimi ve bağlam anladığınızdan emin olun.
* Bu makaleyi okuyun bir veri hizmeti toohello Azure Marketi'nde yayımlama yolu belirlenen tooreturn toohello [veri hizmeti yayımlama Kılavuzu](marketplace-publishing-data-service-creation.md).
