---
title: "Machine Learning öneriler: JavaScript tümleştirme | Microsoft Docs"
description: "Azure Machine Learning önerileri - JavaScript tümleştirmesi - belgeleri"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a>Azure Machine Learning Önerileri - JavaScript Tümleştirmesi
> [!NOTE]
> Merhaba önerileri API Bilişsel hizmeti yerine bu sürümünü kullanarak başlamanız gerekir. Merhaba önerileri Bilişsel hizmet bu hizmeti koyacağınız ve tüm hello yeni özellikler vardır geliştirilmiştir. Toplu işlem desteği, daha iyi API'si Gezgini, bir temizleyici API yüzeyi, daha tutarlı kaydolma/faturalandırma deneyimi, vb. gibi yeni özellikler vardır.
> Daha fazla bilgi edinmek [geçiş toohello yeni Bilişsel hizmeti](http://aka.ms/recomigrate)
> 
> 

Bu belge tarif nasıl toointegrate, sitenizi JavaScript kullanarak. bir öneri modeli yapı sonra hello JavaScript toosend veri alım olayları ve tooconsume öneriler sağlar. JS yapılan tüm işlemler de sunucu tarafındaki yapılabilir.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Genel bakış
Azure ML önerileri sitenizi tümleştirme 2 aşamalara oluşur:

1. Olayları Azure ML önerileri gönderin. Bu toobuild bir öneri modeli olanak tanır.
2. Merhaba önerileri kullanabilir. Merhaba model oluşturulduktan sonra Başlangıç önerileri kullanmasını sağlayabilirsiniz. (Bu belgede, nasıl okuma toobuild bir model hello Hızlı Başlangıç Kılavuzu tooget hakkında daha fazla bilgi açıklamaz).

<ins>Aşama ı</ins>

Azure ML önerileri sunucularına (aracılığıyla veri Pazar) hello html sayfasında oluşurken hello sağlayan küçük bir JavaScript kitaplığı html sayfalarınıza ekleme Birinci aşama sayfa toosend olaylarının hello:

![Drawing1][1]

<ins>Aşama II</ins>

Hello tooshow hello önerileri hello sayfasında istediğinizde İkinci aşama, aşağıdaki seçenekleri şu hello birini seçin:

1. sunucunuzda (sayfa işleme aşamasında hello) Azure ML önerileri Server (aracılığıyla veri Pazar) tooget önerileri çağırır. Merhaba sonuçları öğeleri kimliği listesini içerir. Sunucunuz tooenrich hello sonuçları Meta veriler (örn. görüntüler, açıklama) hello öğelerle gerekir ve sayfa toohello tarayıcı oluşturulan hello gönderin.

![Drawing2][2]

2. hello diğer seçenek toouse hello küçük JavaScript aşaması bir tooget basit önerilen öğelerin listesini dosyasıdır. Burada alınan hello hello ilk seçeneğinde hello'den daha yalın verilerdir.

![Drawing3][3]

## <a name="2-prerequisites"></a>2. Ön koşullar
1. Merhaba API'lerini kullanarak yeni bir model oluşturun. Merhaba Hızlı Başlangıç Kılavuzu nasıl toodo onu.
2. Kodlama, &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; base64 ile. (Bu hello temel kimlik doğrulaması tooenable hello JS kod toocall hello API'leri kullanılır).

## <a name="3-send-data-acquisition-events-using-javascript"></a>3. JavaScript kullanarak veri alım olayları Gönder
Aşağıdaki adımları hello gönderen olaylar kolaylaştırır:

1. JQuery kitaplığı kodunuzda içerir. URL aşağıdaki hello nuget'nden indirebilirsiniz.
   
     http://www.nuget.org/Packages/JQuery/1.8.2
2. URL aşağıdaki hello Hello önerileri Java betiği kitaplığından içerir: http://aka.ms/RecoJSLib1
3. Merhaba uygun parametrelerle Azure ML önerileri kitaplığı başlatılamıyor.
   
     <script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. Gönderme hello uygun olayı. Tüm olayları türüne aşağıda ayrıntılı bölümüne bakın (örnek olarak, olay tıklayın) <script> varsa (typeof AzureMLRecommendationsEvent "undefined" ==) {         
                     AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({event: "click", item: "18321116"});</script>

### <a name="31----limitations-and-browser-support"></a>3.1.    Sınırlamalar ve tarayıcı desteği
Bu bir başvuru uygulamasıdır ve olarak verilir. Önde gelen tüm tarayıcılar desteklemelidir.

### <a name="32----type-of-events"></a>3.2.    Olay türü
Kitaplık destekler hello 5 olay türü vardır: tıklatın, öneri tıklayın, tooShop Sepeti, Ekle, Kaldır alışveriş sepeti ve satın alma. Oturum açma adı verilen kullanılan tooset hello kullanıcı bağlamı ek bir olay yok.

#### <a name="321-click-event"></a>3.2.1. Tıklama olayı
Bu olay, bir kullanıcının bir öğe üzerinde tıkladığınız dilediğiniz zaman kullanılmalıdır. Genellikle kullanıcı bir öğeyi tıklattığında yeni bir sayfa hello öğe ayrıntıları açıldıktan; Bu sayfada, bu olay tetiklenir.

Parametreler:

* "olayı (dize, zorunlu) - tıklayın"
* öğe (dize, zorunlu) - hello öğesinin benzersiz tanıtıcısı
* ItemName (dize, isteğe bağlı) - hello öğesinin hello adı
* itemDescription (dize, isteğe bağlı) - hello öğenin hello açıklaması
* itemCategory (dize, isteğe bağlı) - hello öğesinin hello kategorisi
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

Veya isteğe bağlı verileri olan:

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a>3.2.2. Öneri, olay'ı tıklatın
Bu olay, bir kullanıcının önerilen bir öğe olarak Azure ML önerilerden alındı bir öğe üzerinde tıkladığınız dilediğiniz zaman kullanılmalıdır. Genellikle kullanıcı bir öğeyi tıklattığında yeni bir sayfa hello öğe ayrıntıları açıldıktan; Bu sayfada, bu olay tetiklenir.

Parametreler:

* Olay (dize, zorunlu) - "recommendationclick"
* öğe (dize, zorunlu) - hello öğesinin benzersiz tanıtıcısı
* ItemName (dize, isteğe bağlı) - hello öğesinin hello adı
* itemDescription (dize, isteğe bağlı) - hello öğenin hello açıklaması
* itemCategory (dize, isteğe bağlı) - hello öğesinin hello kategorisi
* oluştururken Çekirdeği (dize dizisi, isteğe bağlı) - hello öneri sorgu oluşturulan oluştururken çekirdeği hello.
* recoList (dize dizisi, isteğe bağlı) - tıklandığını hello maddeden hello öneri isteğinin sonucunu hello.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

Veya isteğe bağlı verileri olan:

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a>3.2.3. Alışveriş sepeti olay Ekle
Bu olay kullanılmalıdır hello kullanıcı alışveriş sepeti öğesi toohello eklediğinizde.
Parametreler:

* Olay (dize, zorunlu) - "addshopcart"
* öğe (dize, zorunlu) - hello öğesinin benzersiz tanıtıcısı
* ItemName (dize, isteğe bağlı) - hello öğesinin hello adı
* itemDescription (dize, isteğe bağlı) - hello öğenin hello açıklaması
* itemCategory (dize, isteğe bağlı) - hello öğesinin hello kategorisi
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a>3.2.4. Alışveriş sepeti olay Kaldır
Bu olay Hello kullanıcı bir öğeyi toohello alışveriş sepeti kaldırdığında kullanılmalıdır.

Parametreler:

* Olay (dize, zorunlu) - "removeshopcart"
* öğe (dize, zorunlu) - hello öğesinin benzersiz tanıtıcısı
* ItemName (dize, isteğe bağlı) - hello öğesinin hello adı
* itemDescription (dize, isteğe bağlı) - hello öğenin hello açıklaması
* itemCategory (dize, isteğe bağlı) - hello öğesinin hello kategorisi
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a>3.2.5. Satın alma olayı
Bu olay Hello kullanıcı kendi alışveriş sepeti satın aldığınızda kullanılmalıdır.

Parametreler:

* Olay (dize) - "satın"
* öğeleri - (satın []) bir giriş her biri için madde satın bulunduran dizi.<br><br>
  Satın alınan biçimi:
  * öğe (dize) - hello öğesinin benzersiz tanımlayıcısı.
  * Count (int veya dize) - satın alınan öğe sayısı.
  * Fiyat (kayan noktalı sayı veya dize) - isteğe bağlı alan - hello fiyatı hello öğesi.

Merhaba örnekte gösterilir 3 satın öğeleri (33 34, 35), iki doldurulmuş tüm alanlar (öğe sayısı, Fiyat) ve biri (öğesi 34) olmadan bir fiyat.

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a>3.2.6. Kullanıcı oturum açma olayı
Azure ML önerileri olay kitaplığı oluşturur ve kullanım bir tanımlama bilgisinde nereden geldiğini sipariş tooidentify olayları aynı tarayıcı hello. Sipariş tooimprove hello modelinde tooset hello tanımlama bilgisi kullanımı geçersiz kılacak olan kullanıcı için benzersiz bir kimlik sonuçları Azure ML önerileri sağlar.

Bu olay hello kullanıcı oturum açma tooyour site sonra kullanılmalıdır.

Parametreler:

* Olay (dize) - "userlogin"
* Kullanıcı (dize) - hello kullanıcının benzersiz kimliği.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a>4. JavaScript aracılığıyla önerileri kullanma
Merhaba öneri tüketir hello kod bazı JavaScript olayı tarafından hello istemcinin Web sayfası tarafından tetiklenir. Merhaba öneri yanıt önerilen öğeleri kimlikleri, adlarını ve derecelendirmelerine hello içeriyor. Bu seçeneği yalnızca bir listesini görüntülemek için önerilen öğelerin - (Merhaba öğesi'nin meta verilerin eklenmesi gibi) işleme daha karmaşık hello hello sunucu tarafı tümleştirme üzerinde yapılmalıdır en iyi toouse olur.

### <a name="41-consume-recommendations"></a>4.1 önerileri kullanma
tooinclude hello gereksinim tooconsume öneriler sayfası ve toocall AzureMLRecommendationsStart JavaScript kitaplıkları gereklidir. 2 bölümüne bakın.

tooconsume önerileri bir veya daha fazla öğe için bir yöntem olarak adlandırılan toocall gerekir: AzureMLRecommendationsGetI2IRecommendation.

Parametreler:

* (bir dizeler dizisi) - bir veya daha fazla öğe tooget önerileri için öğeleri. Bir Fbt yapı kullanmak, yalnızca bir öğe burada ayarlayabilirsiniz.
* numberOfResults (int) - gerekli sonuç sayısı.
* includeMetadata (boolean, isteğe bağlı) - varsa too'true ayarlamak ' hello sonucunda o hello meta veri alanı doldurulur gösterir.
* İşleme işlevi - hello önerileri işleyecek bir işlev döndürdü. Merhaba veri bir dizi döndürdü:
  * Madde - öğesi benzersiz kimliği
  * ad - öğesi adına (varsa kataloğunda var)
  * Derecelendirme - öneri derecelendirme
  * Meta veriler - hello öğesinin hello meta verileri temsil eden bir dize

Örnek: "64f6eb0d-947a-4c18-a16c-888da9e228ba" öğesi için 8 önerileri koddan hello istekleri (değil belirleyerek includeMetadata - diyor örtük olarak meta veri gereklidir), bunu daha sonra birleştirme hello sonuçları bir arabelleğe.

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
