---
title: "Azure arama için aaaLucene sorgu örnekler | Microsoft Docs"
description: "Lucene sorgu söz dizimi belirsiz arama, yakınlık araması, terim artırma, normal ifade araması ve joker karakterle arama için."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: Lucene query analyzer syntax
ms.assetid: 147f360d-a5ce-4d7b-a909-c8b65bfb748c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: liamca
ms.openlocfilehash: d859cf697ef9485a49e9e0591b68e812ffa55f1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="lucene-query-syntax-examples-for-building-queries-in-azure-search"></a>Lucene sorgu söz dizimi örnekler Azure arama sorguları oluşturmak için
Azure arama sorguları oluşturmak, her iki hello varsayılan kullanabilirsiniz [Basit Sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) veya hello alternatif [Lucene sorgu ayrıştırıcı Azure Search'te](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search). Merhaba Lucene sorgu ayrıştırıcı alan kapsamlı sorgular, benzer arama, yakınlık araması, terim artırma ve normal ifade araması gibi daha karmaşık sorgu yapıları destekler.

Bu makalede, sorgu işlemleri kullanılabilir hello tam sözdizimi kullanılırken gösteren örneklerle geçebilirsiniz.

## <a name="viewing-hello-examples-in-jsfiddle"></a>JSFiddle hello örneklerde görüntüleme

Bu makaledeki örneklerde hello önceden yüklenmiş bir arama dizini karşı çalışan yürütülebilir sorguları tümü [JSFiddle](https://jsfiddle.net), komut dosyası ve HTML test etmek için bir çevrimiçi Kod Düzenleyicisi. 

toorun bunları sağ hello sorgu örnek URL'leri tooopen ayrı bir tarayıcı penceresinde JSFiddle üzerinde.

> [!NOTE]
> Merhaba aşağıdaki örneklerde yararlanan işleri kullanılabilir hello tarafından sağlanan bir veri kümesini temel oluşan bir arama dizinini [New York OpenData Şehir](https://nycopendata.socrata.com/) girişimi. Bu veriler, geçerli veya tam düşünülmemelidir. Microsoft tarafından sağlanan bir korumalı alan hizmet Hello dizin açıktır. Bu sorguları bir Azure aboneliği veya Azure Search tootry gerekmez.
>


## <a name="how-tooinvoke-full-lucene-parsing"></a>Tooinvoke nasıl tam Lucene ayrıştırma

Bu makaledeki örneklerde hello tümünün hello belirtin **queryType tam =** hello Lucene sorgu ayrıştırıcısı tarafından işlenen o hello tam sözdizimi gösteren parametre arayın. 

**Örnek 1** --yeni bir tarayıcı içinde sayfa sorgu parçacığı tooopen aşağıdaki sağ hello JSFiddle yükler ve çalıştırır sorgu hello:

* [& queryType tam = & arama = *](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*)

Merhaba yeni tarayıcı penceresinde hello JavaScript kaynak ve HTML çıkışını yan yana sunulur. Merhaba betik tam bir sorgu (yalnızca hello parçacığı, hello bağlantıyı gösterildiği gibi) başvuruda bulunuyor. Merhaba tam sorgu, her örneğin hello URL'lerde gösterilir. 

Bu sorgu belgeleri de New York şehrinde işleri dizinimize (bir korumalı alan hizmeti yüklenmiş nycjobs) döndürür. Konuyu uzatmamak amacıyla, yalnızca iş başlıkları döndürülen hello sorgu belirtir. Merhaba tam temel sorgu aşağıdaki gibidir:

    http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*

Merhaba **searchFields** parametresi hello arama toojust hello iş başlığı alanı kısıtlar. Merhaba **queryType** çok ayarlanır**tam**, bu sorgu için Azure Search toouse hello Lucene sorgu ayrıştırıcı talimatı verir.

> [!NOTE]
> Sorgu işlemi arka planda için bkz: [nasıl tam metin araması Azure Search'te çalışır](search-lucene-query-architecture.md). Arama parametreleri hakkında daha fazla bilgi için bkz: [Search belgeleri (Azure Search Hizmeti REST API'si)](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).
>

### <a name="fielded-query-operation"></a>Fielded sorgu işlemi
Bu makaledeki örneklerde hello belirterek değiştirebilirsiniz bir **fieldname:searchterm** yapım toodefine burada hello alan tek bir sözcük ve hello arama terimi ayrıca tek bir sözcük veya tümcecik, bir fielded sorgu işlemi Boole işleçleri ile isteğe bağlı olarak. Bazı örnekler hello şunları içerir:

* business_title:(senior NOT junior)
* Durum: ("New York" ve "Yeni bölgesi")

Merhaba konum alanı iki farklı şehirlerde arama bu durumda olduğu gibi tek bir varlık olarak değerlendirilen her iki dizeleri toobe istiyorsanız emin tooput tırnak işaretleri içinde birden çok dizeleri olun. Ayrıca, NOT ile gördüğünüz gibi hello işleci katılamayacağını emin olun ve and

Belirtilen hello alan **fieldname:searchterm** aranabilir alan olması gerekir. Bkz: [Create Index (Azure Search Hizmeti REST API'si)](https://docs.microsoft.com/rest/api/searchservice/create-index) dizin öznitelikleri alan tanımlarında nasıl kullanıldığı hakkında bilgi.

**Örnek 2** --sağ hello aşağıdaki kod parçacığında iş başlıkları hello ile arar terim bunlara Kıdemli ancak değil çırak bu sorguyu sorgu:

* [& queryType tam = & arama business_title:senior değil = çırak](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:senior+NOT+junior)

## <a name="fuzzy-search-example"></a>Benzer arama örneği
Benzer arama eşleştiğini bulur benzer yapım olması koşuluyla. Başına [Lucene belgelerine](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html), benzer aramaları temel [Damerau Levenshtein uzaklığı](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance).

toodo benzer arama hello tilde Ekle "~" isteğe bağlı parametresi, hello düzenleme uzaklığını belirtir 0 ve 2 ' arasında bir değer tek bir sözcük hello sonunda simgesi. Örneğin, "mavi ~" veya "mavi ~ 1" döndürebildiği mavi, mavi ve Yapıştırıcı işlevi görür.

**Örnek 3** --sağ hello aşağıdaki kod parçacığında sorgu. Bu sorgu, (burada, yanlış yazılmış) hello terim ilişkilendirme işleriyle arar:

* [& queryType tam = & arama business_title:asosiate = ~](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:asosiate~)

> [!Note]
> Belirsiz sorguları olmayan [analiz](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis), olabilen dallanma veya lemmatization bekliyorsanız, şaşırtıcı. Sözcük analiz yalnızca tam koşullarınızda gerçekleştirilen (terim sorgu veya tümcecik sorgusu). Sorgu türleri (önek sorgu, joker karakter sorgu, regex sorgu, benzer sorgu) tamamlanmamış koşullarla hello analysis aşaması atlayarak toohello sorgu ağacında, doğrudan eklenir. Merhaba yalnızca tamamlanmamış sorgu terimlerinin üzerinde gerçekleştirilen dönüştürmeyi lowercasing.
>

## <a name="proximity-search-example"></a>Yakınlık arama örneği
Yakınlık aramalar diğer bir belgede kullanılan toofind terimleri gerçekleşir. Bir tilde Ekle "~" tümcecik hello sonunda simge izlenen hello yakınlık sınır oluşturmak sözcükler hello sayısına göre. Örneğin, "otel havaalanı" ~ 5 hello koşulları otel ve havaalanı birbiriyle 5 sözcük içinde bir belgede bulacaksınız.

**Örnek 4** --sağ hello sorgu. İşlerini hello terimi "Kıdemli analist" ile birden fazla sözcük ayrıldığı arayın:

* [& queryType tam = & arama business_title =: "Kıdemli analist" ~ 1](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~1)

**Örnek 5** --hello sözcükler hello terimi "Kıdemli analist" arasında kaldırmayı yeniden deneyin.

* [& queryType tam = & arama business_title =: "Kıdemli analist" ~ 0](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~0)

## <a name="term-boosting-examples"></a>Örnekler artırmanın terimi
Terim artırma hello içeriyorsa, daha yüksek bir belge terimi, hello terim içermeyen göreli toodocuments boosted tooranking başvuruyor. Bu, belirli alanları yerine belirli terimleri Puanlama profilleri artırabilir, profilleri Puanlama farklıdır. Merhaba aşağıdaki örnek hello farklar göstermeye yardımcı olur.

Artırır bir Puanlama profili eşleşen belirli bir alana gibi göz önünde bulundurun **Tarz** hello musicstoreindex örnekte. Terim artırma artırma kullanılan toofurther arama diğerlerinden daha yüksek koşulları belirli olabilir. Örneğin, "rock ^ 2 elektronik" Merhaba hello arama terimlerini içeren belgeleri artıracak **Tarz** alan hello dizindeki diğer aranabilir alanları daha yüksek. Ayrıca, hello arama terimi "rock" içeren belgeleri diğer arama terimi "Merhaba terim artırma değeri (2) sonucunda elektronik" Merhaba daha yüksek derece verilecek.

tooboost bir terimini, kullanım hello düzeltme işareti, "^", simge arama hello terim hello sonunda bir artırma faktörle (sayı). daha yüksek hello yükseltme faktörü hello hello daha ilgili hello terim göreli tooother arama terimleri olacaktır. Varsayılan olarak, hello yükseltme faktörü 1'dir. Merhaba artırmaya factor pozitif olması gerekse de (örneğin, 0.2) 1'den küçük olabilir.

**Örnek 6** --sağ hello sorgu. "Nerede biz sözcükler bilgisayar hem analist sonuç yok henüz hello sonuçları hello üstünde olan analist işleri görmek bilgisayar analist" Merhaba terim işleriyle arayın.

* [& queryType tam = & arama business_title:computer analist =](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

**Örnek 7** --yeniden deneyin, her iki sözcük yoksa bu zaman artırmanın hello terim bilgisayarla hello terim analist sonuçlanır.

* [& queryType tam = & arama business_title:computer = ^ 2 analisti](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

## <a name="regular-expression-example"></a>Normal ifade örneği
Normal ifade araması hello içeriği eğik arasında "/", içinde belgelenen hello olarak dayalı bir eşleşme bulur [RegExp sınıfı](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html).

**Örnek 8** --sağ hello sorgu. Merhaba terim Kıdemli veya alt düzey işleriyle arayın.

* `&queryType=full&$select=business_title&search=business_title:/(Sen|Jun)ior/`

Bu örnek için Hello URL hello sayfasında düzgün şekilde işlenmez. Geçici bir çözüm olarak aşağıdaki hello URL'sini kopyalayın ve hello tarayıcı URL adresine yapıştırın:`http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:/(Sen|Jun)ior/)`

## <a name="wildcard-search-example"></a>Joker karakter arama örneği
Birden çok için genellikle tanınan söz dizimini kullanabilirsiniz (\*) ya da tek (?) karakteri joker aramalar. Merhaba Lucene sorgu ayrıştırıcı tek bir terim ve bir deyimi bu simgeleri hello kullanımını desteklediğini unutmayın.

**Örnek 9** --sağ hello sorgu. 'İş başlıkları programlama hello hüküm ve programcı da dahil hello önek prog' içeren işleri arayın.

* [& queryType tam & $select = business_title & arama = business_title:prog* =](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:prog*)

Kullanarak bir * veya? bir arama hello ilk karakteri olarak simge.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba Lucene sorgu ayrıştırıcı kodunuzda belirtmeyi deneyin. hem .NET hem de hello REST API için arama yukarı tooset nasıl sorgular bağlantılar aşağıdaki hello açıklanmaktadır. Bu makale toospecify hello öğrendiklerinizi tooapply ihtiyacınız olacak şekilde Hello bağlantıları kullanın hello varsayılan basit sözdizimi **queryType**.

* [Merhaba .NET SDK kullanarak, Azure Search dizininizi sorgulama](search-query-dotnet.md)
* [Azure Search hello REST API kullanarak dizininizi sorgulama](search-query-rest-api.md)

## <a name="see-also"></a>Ayrıca bkz.

 [Azure Search'te nasıl tam metin araması çalışır](search-lucene-query-architecture.md)