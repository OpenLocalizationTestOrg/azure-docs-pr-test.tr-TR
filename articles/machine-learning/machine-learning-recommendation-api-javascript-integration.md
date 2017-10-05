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
redirect_document_id: TRUE
ms.openlocfilehash: 8f27962d097bffc2a03de80244ae41d6573a4bf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a>Azure Machine Learning Önerileri - JavaScript Tümleştirmesi
> [!NOTE]
> Öneriler API Bilişsel hizmeti yerine bu sürümünü kullanarak başlamanız gerekir. Öneriler Bilişsel hizmet bu hizmeti koyacağınız ve tüm yeni özellikler vardır geliştirilmiştir. Toplu işlem desteği, daha iyi API'si Gezgini, bir temizleyici API yüzeyi, daha tutarlı kaydolma/faturalandırma deneyimi, vb. gibi yeni özellikler vardır.
> Daha fazla bilgi edinmek [yeni Bilişsel Service'e geçirme](http://aka.ms/recomigrate)
> 
> 

Bu belge, sitenizi JavaScript kullanarak tümleştirme tarif. JavaScript, veri alım olayları göndermek için ve bir öneri modeli yapı sonra öneriler tüketmeye sağlar. JS yapılan tüm işlemler de sunucu tarafındaki yapılabilir.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Genel bakış
Azure ML önerileri sitenizi tümleştirme 2 aşamalara oluşur:

1. Olayları Azure ML önerileri gönderin. Bu öneri modeli oluşturmaya olanak tanır.
2. Öneriler kullanabilir. Model oluşturulduktan sonra öneriler kullanmasını sağlayabilirsiniz. (Bu belgede bir model oluşturmak nasıl açıklamaz okuma hakkında daha fazla bilgi almak için Hızlı Başlangıç Kılavuzu).

<ins>Aşama ı</ins>

İlk aşamada, bunlar html sayfasında Azure ML önerileri sunucularına (aracılığıyla veri Pazar) ortaya çıktığında olayları göndermek için sayfadaki sağlayan küçük bir JavaScript kitaplığı html sayfalarınıza ekleyin:

![Drawing1][1]

<ins>Aşama II</ins>

Sayfada önerileri göstermek istediğiniz zaman ikinci aşamasında aşağıdaki seçeneklerden birini seçin:

1. sunucunuzda (sayfa işleme aşama) Azure ML önerileri sunucusu önerileri almak için (veri Pazar) çağırır. Sonuçlar öğeleri kimliği listesini içerir. Meta veriler (örn. görüntüler, açıklama) öğeleri sonuçlardan zenginleştirmek ve oluşturulan sayfa tarayıcıya göndermek sunucunuzu gerekir.

![Drawing2][2]

2. diğer seçenek önerilen öğeler basit bir listesini almak için birinci aşaması küçük JavaScript dosyasından kullanmaktır. Burada alınan ilk seçeneğinde olandan daha yalın veridir.

![Drawing3][3]

## <a name="2-prerequisites"></a>2. Ön koşullar
1. API'lerini kullanarak yeni bir model oluşturun. Yapmak Hızlı Başlangıç Kılavuzu bakın.
2. Kodlama, &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; base64 ile. (Bunun için temel kimlik doğrulaması API'leri çağırmak JS kodu etkinleştirmek için kullanılır).

## <a name="3-send-data-acquisition-events-using-javascript"></a>3. JavaScript kullanarak veri alım olayları Gönder
Aşağıdaki adımları gönderen olaylar kolaylaştırır:

1. JQuery kitaplığı kodunuzda içerir. Nuget aşağıdaki URL'de'nden indirebilirsiniz.
   
     http://www.nuget.org/Packages/JQuery/1.8.2
2. Aşağıdaki URL'yi önerileri Java betiği kitaplığından içerir: http://aka.ms/RecoJSLib1
3. Uygun parametrelerle Azure ML önerileri kitaplığı başlatılamıyor.
   
     <script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. Uygun olay gönderin. Tüm olayları türüne aşağıda ayrıntılı bölümüne bakın (örnek olarak, olay tıklayın) <script> varsa (typeof AzureMLRecommendationsEvent "undefined" ==) {         
                     AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({event: "click", item: "18321116"});</script>

### <a name="31----limitations-and-browser-support"></a>3.1.    Sınırlamalar ve tarayıcı desteği
Bu bir başvuru uygulamasıdır ve olarak verilir. Önde gelen tüm tarayıcılar desteklemelidir.

### <a name="32----type-of-events"></a>3.2.    Olay türü
Kitaplık destekleyen olay 5 türü vardır:, öneri'ı tıklatın, Ekle'yi tıklatın alışveriş sepetine alışveriş sepeti ve satın alma kaldırın. Oturum açma adı verilen kullanıcı bağlamı ayarlamak için kullanılan ek bir olay yok.

#### <a name="321-click-event"></a>3.2.1. Tıklama olayı
Bu olay, bir kullanıcının bir öğe üzerinde tıkladığınız dilediğiniz zaman kullanılmalıdır. Genellikle kullanıcı bir öğeyi tıklattığında yeni bir sayfa öğesi ayrıntılarla açıldığında; Bu sayfada, bu olay tetiklenir.

Parametreler:

* "olayı (dize, zorunlu) - tıklayın"
* öğe (dize, zorunlu) - öğesinin benzersiz tanıtıcısı
* ItemName (dize, isteğe bağlı) - öğesinin adı
* itemDescription (dize, isteğe bağlı) - öğenin açıklaması
* itemCategory (dize, isteğe bağlı) - kategori öğesi
  
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
Bu olay, bir kullanıcının önerilen bir öğe olarak Azure ML önerilerden alındı bir öğe üzerinde tıkladığınız dilediğiniz zaman kullanılmalıdır. Genellikle kullanıcı bir öğeyi tıklattığında yeni bir sayfa öğesi ayrıntılarla açıldığında; Bu sayfada, bu olay tetiklenir.

Parametreler:

* Olay (dize, zorunlu) - "recommendationclick"
* öğe (dize, zorunlu) - öğesinin benzersiz tanıtıcısı
* ItemName (dize, isteğe bağlı) - öğesinin adı
* itemDescription (dize, isteğe bağlı) - öğenin açıklaması
* itemCategory (dize, isteğe bağlı) - kategori öğesi
* (dize dizisi, isteğe bağlı) - öneri sorgu oluşturulan oluştururken çekirdeği çekirdeğini oluşturur.
* recoList (dize dizisi, isteğe bağlı) - tıklandığını maddeden öneri isteğin sonucu.
  
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
Bu olay kullanılması gereken kullanıcı alışveriş sepetine bir öğe eklediğinizde.
Parametreler:

* Olay (dize, zorunlu) - "addshopcart"
* öğe (dize, zorunlu) - öğesinin benzersiz tanıtıcısı
* ItemName (dize, isteğe bağlı) - öğesinin adı
* itemDescription (dize, isteğe bağlı) - öğenin açıklaması
* itemCategory (dize, isteğe bağlı) - kategori öğesi
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a>3.2.4. Alışveriş sepeti olay Kaldır
Bu olay, kullanıcı bir öğeyi alışveriş sepetine kaldırdığında kullanılmalıdır.

Parametreler:

* Olay (dize, zorunlu) - "removeshopcart"
* öğe (dize, zorunlu) - öğesinin benzersiz tanıtıcısı
* ItemName (dize, isteğe bağlı) - öğesinin adı
* itemDescription (dize, isteğe bağlı) - öğenin açıklaması
* itemCategory (dize, isteğe bağlı) - kategori öğesi
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a>3.2.5. Satın alma olayı
Bu olay, kullanıcının kendi alışveriş sepeti satın aldığınızda kullanılmalıdır.

Parametreler:

* Olay (dize) - "satın"
* öğeleri - (satın []) bir giriş her biri için madde satın bulunduran dizi.<br><br>
  Satın alınan biçimi:
  * öğe (dize) - öğesinin benzersiz tanımlayıcısı.
  * Count (int veya dize) - satın alınan öğe sayısı.
  * Fiyat (kayan noktalı sayı veya dize) - isteğe bağlı alan - öğenin fiyat.

Aşağıdaki örnek, satın alma 3 gösterir (33, 34, 35) öğeleri iki doldurulmuş tüm alanlar (öğe sayısı, Fiyat) ve biri (öğesi 34) olmadan bir fiyat.

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a>3.2.6. Kullanıcı oturum açma olayı
Azure ML önerileri olay kitaplığı oluşturur ve aynı tarayıcıdan gelen olayları belirlemek amacıyla bir tanımlama bilgisi kullanın. Model sonuçları Azure ML önerileri geliştirmek için tanımlama bilgisi kullanımı geçersiz kılacak olan kullanıcı için benzersiz bir kimlik ayarlamak için etkinleştirir.

Bu olay, kullanıcı oturum açma Web sitenize sonra kullanılmalıdır.

Parametreler:

* Olay (dize) - "userlogin"
* Kullanıcı (dize) - kullanıcının benzersiz tanımlayıcısı.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a>4. JavaScript aracılığıyla önerileri kullanma
Öneri tüketir kod bazı JavaScript olayı tarafından istemci Web sayfası tarafından tetiklenir. Öneri yanıt önerilen öğeler kimlikleri, adlarını ve derecelendirmeleri içeriyor. Yalnızca bir liste görünümünü önerilen öğeler için bu seçeneği kullanmak en iyisidir - sunucu tarafı tümleştirmeye (öğesi'nin meta veri ekleme gibi) daha karmaşık işleme yapılması gerekir.

### <a name="41-consume-recommendations"></a>4.1 önerileri kullanma
Kullanmak için sayfanızı ve AzureMLRecommendationsStart çağırmak için gerekli JavaScript kitaplıklarını yapmanız önerileri içerir. 2 bölümüne bakın.

Bir veya daha fazla öğe için gereken adlı bir yöntemi çağırmak öneriler kullanmak için: AzureMLRecommendationsGetI2IRecommendation.

Parametreler:

* (bir dizeler dizisi) - için önerileri almak için bir veya daha fazla öğe öğeleri. Bir Fbt yapı kullanmak, yalnızca bir öğe burada ayarlayabilirsiniz.
* numberOfResults (int) - gerekli sonuç sayısı.
* includeMetadata (boolean, isteğe bağlı) - meta verileri alan sonucunda doldurulmalıdır 'true' olarak ayarlandığında gösterir.
* İşleme işlevi - önerileri işleyecek bir işlev döndürdü. Bir dizisi olarak döndürülen veriler:
  * Madde - öğesi benzersiz kimliği
  * ad - öğesi adına (varsa kataloğunda var)
  * Derecelendirme - öneri derecelendirme
  * Meta veriler - öğe meta verileri temsil eden bir dize

Örnek: 8 önerileri öğesi "64f6eb0d-947a-4c18-a16c-888da9e228ba" için aşağıdaki kodu istekleri (değil belirleyerek includeMetadata - diyor örtük olarak meta veri gereklidir), bunu daha sonra birleştirme sonuçları bir arabelleğe.

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
