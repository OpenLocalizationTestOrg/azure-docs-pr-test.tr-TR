---
title: "aaaHow toopage arama sonuçları Azure Search'te | Microsoft Docs"
description: "Sayfa numaralandırma Azure Search'te, Microsoft Azure üzerinde barındırılan bulut arama hizmeti."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a>Azure Search'te nasıl toopage arama sonuçları
Bu makalede, nasıl toouse hello Azure Search Hizmeti REST API'si tooimplement standart öğeleri arama sonuçları sayfası, toplam sayıları, belge alma, sıralamalar ve gezinti gibi hakkında yönergeleri sunar.

Aşağıda belirtilen her durumda, verileri veya bilgi tooyour arama sonuçları sayfasını katkıda sayfasıyla ilgili seçenekleri hello belirlenmiş [arama belge](http://msdn.microsoft.com/library/azure/dn798927.aspx) gönderilen istekleri tooyour Azure Search hizmeti. İstekleri GET komutu, yol ve ne istenen hello hizmet bildirmek sorgu parametreleri ile nasıl tooformulate hello yanıt içerir.

> [!NOTE]
> Geçerli bir istek bir hizmet URL'si ve yol, HTTP fiili gibi öğeleri içerir `api-version`ve benzeri. Konuyu uzatmamak amacıyla, ilgili toopagination olan hello örnekler toohighlight yalnızca hello sözdizimi kırpılır. Lütfen hello bakın [Azure Search Hizmeti REST API'si](http://msdn.microsoft.com/library/azure/dn798935.aspx) isteği sözdizimi hakkında ayrıntılar için belgelere.
> 
> 

## <a name="total-hits-and-page-counts"></a>Toplam İsabet ve sayfa sayıları
Merhaba bir sorgudan döndürülen sonuç sayısı ve bu döndürme daha küçük parçalar sonuçların toplam gösteren, tüm arama sayfaları temel toovirtually olur.

![][1]

Azure Search'te hello kullan `$count`, `$top`, ve `$skip` parametreleri tooreturn bu değerleri. Merhaba aşağıdaki örnekte gösterilir olarak döndürülen toplam isabet sayısı için bir örnek istek `@OData.count`:

        GET /indexes/onlineCatalog/docs?$count=true

15 grupları belgelerde almak ve ayrıca hello ilk sayfasına başlangıç hello toplam isabet sayısı göster:

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

Sonuçları sayfa numaralandırma, gerektiren her ikisi de `$top` ve `$skip`, burada `$top` kaç öğeleri tooreturn bir toplu işlemde belirtir ve `$skip` kaç öğeleri tooskip belirtir. Hello Örneğin, aşağıdaki her bir sayfa hello sonraki 15 öğeleri gösterir hello artımlı atlar hello içinde belirtildiği `$skip` parametresi.

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a>Düzen
Arama sonuçları sayfasında, bir küçük resim, alanlarının alt kümesini ve bir bağlantı tooa tam ürün sayfasını tooshow isteyebilirsiniz.

 ![][2]

Azure Search'te kullanacağınız `$select` ve arama bu deneyim tooimplement komutu.

tooreturn bir alt alanların döşeli düzeni için:

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

Görüntüleri ve medya dosyaları doğrudan aranabilir değildir ve tooreduce maliyetler Azure Blob Depolama alanı gibi başka bir depolama Platform depolanması gerekir. Başlangıç dizini ve belgeleri, hello dış içeriği hello URL adresini depolayan bir alan tanımlayın. Ardından, bir resim başvurusu hello alanını kullanabilirsiniz. Merhaba URL toohello görüntü hello belgede olmalıdır.

Ürün açıklaması sayfa için tooretrieve bir **onClick** olay, kullanım [arama belge](http://msdn.microsoft.com/library/azure/dn798929.aspx) hello belge tooretrieve hello anahtarı toopass. başlangıç anahtarı Hello veri türü `Edm.String`. Bu örnek, *246810*. 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a>İlgi, derecelendirme veya fiyat göre sırala
Sıralama genellikle toorelevance varsayılan ancak ortak toomake alternatif sıralamalar kullanıma hazır, böylelikle müşterilerin hızla varolan sonuçları farklı bir sıralama düzeni içinde sırasını yeniden ayarlaması sıralar.

 ![][3]

Azure Search'te sıralama üzerinde hello dayanır `$orderby` olarak dizin oluşturulmuş tüm alanlar için ifade`"Sortable": true.`

İlgi kesinlikle profilleri Puanlama ile ilişkilidir. Daha fazla veya daha güçlü eşleşme ile toodocuments bir arama terimi giderek daha yüksek puanları ile tüm sonuçları metin analiz ve İstatistikler toorank siparişte kullanır hello varsayılan Puanlama, kullanabilirsiniz.

Alternatif sıralamalar genellikle ilişkili olan **onClick** geri tooa yöntemi, arama olayları hello sıralama düzeni oluşturur. Örneğin, bu sayfa öğesi verilen:

 ![][4]

Seçili hello sıralama seçeneği giriş olarak kabul eder ve bu seçenek ile ilişkili hello ölçütlerine sıralı bir listesi döndüren bir yöntem oluşturursunuz.

 ![][5]

> [!NOTE]
> Varsayılan Hello Puanlama birçok senaryo için yeterli olmakla birlikte, bunun yerine özel bir Puanlama profili ilgi alma öneririz. Özel bir Puanlama profili daha yararlı tooyour iş bir şekilde tooboost öğeleri sağlar. Bkz: [Puanlama profili Ekle](http://msdn.microsoft.com/library/azure/dn798928.aspx) daha fazla bilgi için. 
> 
> 

## <a name="faceted-navigation"></a>Çok yönlü gezinme
Arama gezinti genellikle hello yan veya bir sayfanın üst kısmında bulunan bir sonuçlar sayfası üzerinde yaygındır. Azure Search'te modellenmiş bir gezinmede önceden tanımlanmış filtrelere göre kendi kendine yönlendirilmiş arama sağlar. Bkz: [Azure Search'te modellenmiş bir gezinmede](search-faceted-navigation.md) Ayrıntılar için.

## <a name="filters-at-hello-page-level"></a>Merhaba sayfa düzeyinde filtreleri
Çözüm tasarımınızın belirli türlerdeki içerik (örneğin, hello hello sayfanın başında listelenen bölümleri olan bir çevrimiçi perakende uygulama) için ayrılmış arama sayfalar dahil, bir filtre ifadesi yanında ekleyebilirsiniz bir **onClick** olay tooopen bir sayfa makale bir durumda. 

Bir filtre ile veya olmadan arama ifadesi gönderebilirsiniz. Örneğin, hello aşağıdaki isteği marka, eşleşen belgeleri döndüren adına filtre uygular.

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

Bkz: [Search belgeleri (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) hakkında daha fazla bilgi için `$filter` ifadeler.

## <a name="see-also"></a>Ayrıca Bkz.
* [Azure Search Hizmeti REST API'si](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [Dizin işlemleri](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [Belge işlemleri](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [Video ve Azure Search öğreticileri](search-video-demo-tutorial-list.md)
* [Azure Search'te modellenmiş bir gezinmede](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
