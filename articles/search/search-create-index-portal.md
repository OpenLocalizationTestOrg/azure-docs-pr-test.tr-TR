---
title: "aaa \"(portalı - Azure Search) dizin oluşturma | Microsoft Docs\""
description: "Hello Azure Portal kullanarak bir dizin oluşturun."
services: search
manager: jhubbard
author: heidisteen
documentationcenter: 
ms.assetid: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/20/2017
ms.author: heidist
ms.openlocfilehash: 4c5d663499bf73a8883690aa9482b6ba59d1ddf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-azure-portal"></a>Hello Azure Portal kullanarak Azure Search dizini oluşturma
> [!div class="op_single_selector"]
> * [Genel Bakış](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

Merhaba yerleşik dizin designer'ı Azure portal tooprototype kullanın veya oluşturma bir [arama dizini](search-what-is-an-index.md) toorun Azure Search hizmet üzerinde. 

## <a name="prerequisites"></a>Ön koşullar

Bu makalede varsayar bir [Azure aboneliği](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ve [Azure Search Hizmeti](search-create-service-portal.md).  

## <a name="find-your-search-service"></a>Arama hizmetinizi bulma
1. Toohello Azure portal sayfasında oturum açın ve hello gözden [arama hizmetleri aboneliğiniz için](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)
2. Azure Search hizmetinizi seçin.

## <a name="name-hello-index"></a>Adı hello dizini

1. Hello tıklatın **Ekle dizin** hello komut çubuğunda hello sayfanın üst kısmındaki hello düğmesi.
2. Azure Search dizininizi olarak adlandırın. 
   * Bir harf ile başlamalıdır.
   * Yalnızca küçük harf, rakam veya kesik çizgi kullanın ("-").
   * Merhaba adı too60 karakterleri sınırlandırır.

  Merhaba dizin adı hello uç nokta URL'si bağlantıları toohello dizini ve hello Azure Search REST API'sini HTTP istekleri göndermek için kullanılan bir parçası olur.

## <a name="define-hello-fields-of-your-index"></a>Dizininizi Hello alanlarını tanımlayın

Dizin oluşturma içeren bir *alanlar koleksiyonu* dizininizdeki hello aranabilir verileri tanımlayan. Daha açık belirtmek gerekirse, ayrı ayrı karşıya belgelerinin hello yapısını belirtir. Merhaba alanlar koleksiyonu adlı ve, dizin öznitelikleri toodetermine hello alan nasıl kullanılabileceğini yazılan gerekli ve isteğe bağlı alanları içerir.

1. Hello içinde **eklemek dizin** dikey penceresinde tıklatın **alanları >** tooslide hello alan tanımı dikey penceresini açın. 

2. Oluşturulan hello kabul *anahtar* türü Edm.String alan. Varsayılan olarak, hello alan adlı *kimliği* ancak hello dize karşılayan sürece adlandırabilirsiniz [adlandırma kurallarını](https://docs.microsoft.com/rest/api/searchservice/Naming-rules). Her Azure Search dizini için bir anahtar alanı zorunludur ve bir dize olmalıdır.

3. Toofully belirtmeniz hello belgeleri karşıya yükleyecek alanlar ekleyin. Belgeler oluşur, bir *kimliği*, *otel adı*, *adresi*, *Şehir*, ve *bölge*, oluşturma bir karşılık gelen alan hello dizindeki her biri için. Gözden geçirme hello [Tasarım Kılavuzu hello bölümünde aşağıdaki](#design) özniteliklerini ayarlama hakkında Yardım için.

4. İsteğe bağlı olarak kullanılan herhangi bir alan dahili olarak filtre ifadelerinde ekleyin. Merhaba alan özniteliklerinde tooexclude alanları arama işlemlerinin ayarlayabilirsiniz.

5. Tamamlandığında tıklatarak **Tamam** toosave ve hello dizin oluşturun.

## <a name="tips-for-adding-fields"></a>Alanlar ekleyerek ipuçları

Merhaba Portalı'nda bir dizin oluşturma klavye yoğun bağlıdır. Adımları bu iş akışı izleyerek en aza indirir:

1. İlk olarak, adları girerek ve veri türleri ayarlama hello alan listesi oluşturun.

2. Ardından, her özniteliği toobulk hello üstündeki hello onay kutularını kullan tüm alanlar için hello ayarını etkinleştirin ve hello kutularını gerektirmez az alan seçmeli olarak temizleyin. Örneğin, dize alanları genellikle aranamaz. Bu nedenle, tıklatabilir **alınabilir** ve **aranabilir** hello tooboth dönüş hello değerleri alan arama sonuçlarında yanı sıra hello alanı tam metin araması izin. 

<a name="design"></a>
## <a name="design-guidance-for-setting-attributes"></a>Öznitelikleri ayarlamak için Tasarım Kılavuzu

Herhangi bir zamanda yeni alanlar ekleyebilirsiniz, ancak varolan alan tanımları hello dizin hello ömrü boyunca kilitli olduğunu. Bu nedenle, geliştiriciler genellikle hello portal Basit Dizin oluşturma, test fikirleri veya hello portal sayfalarına toolook bir ayarını kullanarak kullanın. Bir dizin tasarımı üzerinden sık yineleme hello dizini kolayca yeniden böylece kod tabanlı bir yaklaşım izlerseniz daha verimli olur.

Merhaba dizin kaydedilmeden önce Çözümleyicileri ve ilgili alanları ile ilişkilendirilir. Her sekmeli sayfa tooadd dil Çözümleyicileri veya ilgili tooyour dizin tanımı aracılığıyla emin tooclick olabilir.

Dize alanları olarak genellikle işaretlenir **aranabilir** ve **alınabilir**.

Kullanılan alanları toonarrow arama sonuçlarında **sıralanabilir**, **Filterable**, ve **modellenebilir**.

Alan öznitelikleri nasıl bir alan, onu tam metin araması, modellenmiş bir gezinmede, sıralama işlemi ve benzeri kullanılan gibi kullanıldığını belirler. Aşağıdaki tablonun hello her özniteliği açıklar.

|Öznitelik|Açıklama|  
|---------------|-----------------|  
|**aranabilir**|Tam metin aranabilir, konu toolexical çözümlemesi dizin oluşturma sırasında sözcük bölme gibi. "Güneşli gün" gibi aranabilir alan tooa değeri ayarlarsanız, dahili olarak, hello tek tek belirteçleri "güneşli" ve "gün" olarak bölünür. Ayrıntılar için bkz [nasıl tam metin arama works](search-lucene-query-architecture.md).|  
|**filtrelenebilir**|Başvurulan **$filter** sorgular. Türünde filtrelenebilir alanlar `Edm.String` veya `Collection(Edm.String)` yalnızca tam eşleşme için karşılaştırmaları; bu nedenle Sözcük bölünmesi, uygulanabilecek değil. Örneğin, böyle bir alan f çok ayarlarsanız "güneşli gün", `$filter=f eq 'sunny'` herhangi bir eşleşme bulur ancak `$filter=f eq 'sunny day'` olur. |  
|**sıralanabilir**|Varsayılan olarak hello sistem sonuçları puana göre sıralar, ancak hello belgeleri alanlara göre sıralama yapılandırabilirsiniz. Türünde alanlar `Collection(Edm.String)` olamaz **sıralanabilir**. |  
|**modellenebilir**|Genellikle bir isabet sayısı (örneğin, belirli bir şehirde Oteller) kategoriye içeren sunu arama sonuçlarının kullanılır. Bu seçenek türü alanlarla kullanılamaz `Edm.GeographyPoint`. Türünde alanlar `Edm.String` olan **filtrelenebilir**, **sıralanabilir**, veya **modellenebilir** en çok 32 kilobaytı uzunluğunda olabilir. Ayrıntılar için bkz [Create Index (REST API'si)](https://docs.microsoft.com/rest/api/searchservice/create-index).|  
|**anahtarı**|Belgeler hello dizini içinde benzersiz tanımlayıcısı. Merhaba anahtar alan olarak yalnızca bir alanın seçtiniz ve türünde olmalıdır `Edm.String`.|  
|**alınabilir**|Bir arama sonucunda Hello alan döndürdü olup olmadığını belirler. Toouse bir alan istediğinizde bu kullanışlıdır (gibi *Kar marjı*) bir filtre olarak sıralama veya mekanizması, Puanlama ancak yapmak istediğiniz hello alan toobe görünür toohello son kullanıcı değil. Bu öznitelik olmalıdır `true` için `key` alanları.|  

## <a name="create-hello-hotels-index-used-in-example-api-sections"></a>Örnek API bölümlerde kullanılan hello Oteller dizini oluşturma

Azure Search API belgelerine içeren basit bir özelliğe sahip olan kod örnekleri *Oteller* dizini. Hello dizin tanımı dizin tanımı sırasında belirtilen hello Fransızca Dil Çözümleyicisi dahil olmak üzere, gördüğünüz aşağıdaki Hello ekran görüntülerinde hangi alıştırmada hello portalında olarak yeniden oluşturabilirsiniz.

![](./media/search-create-index-portal/field-definitions.png)

![](./media/search-create-index-portal/set-analyzer.png)

## <a name="next-steps"></a>Sonraki adımlar

Azure Search dizini oluşturduktan sonra toohello sonraki adıma geçebilirsiniz: [aranabilir verileri hello dizine yüklemek](search-what-is-data-import.md).

Alternatif olarak, dizinleri daha derin göz ele geçirebilir. Ayrıca toohello alanlar koleksiyonu, bir dizin çözümleyiciler, profilleri ve CORS ayarları Puanlama ilgili de belirtir. Merhaba portal sekmeli sayfaları hello en yaygın öğeleri tanımlamak için sağlar: alanları, Çözümleyicileri ve ilgili. toocreate veya diğer öğeleri değiştirmek, hello REST API veya .NET SDK'sını kullanabilirsiniz.

## <a name="see-also"></a>Ayrıca bkz.

 [Tam metin araması nasıl çalışır?](search-lucene-query-architecture.md)  
 [Arama hizmeti REST API'si](https://docs.microsoft.com/rest/api/searchservice/) [.NET SDK'sı](https://docs.microsoft.com/dotnet/api/overview/azure/search?view=azure-dotnet)

