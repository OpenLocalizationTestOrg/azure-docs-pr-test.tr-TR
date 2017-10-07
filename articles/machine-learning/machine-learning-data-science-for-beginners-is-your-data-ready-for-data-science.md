---
title: "aaaIs verilerinizi veri bilimi için hazır mısınız? Veri değerlendirmesi - Azure Machine Learning | Microsoft Docs"
description: "Veri toobe veri bilimi için hazır Hello 4 ölçütlerine öğrenin. Veri bilimi video 2 yeni başlayanlar için temel veri değerlendirme ile somut örnekler toohelp sahiptir."
keywords: "ilgili verileri verileri değerlendirmek, verileri, veri ölçütlerini, veri hazır hazırlayın"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: d502062c-da70-4b21-9054-0bfd9902612e
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: ef6bb680ace771537157dbdd50a4ccce0a3eb7ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="is-your-data-ready-for-data-science"></a>Verileriniz veri bilimi için hazır mı?
## <a name="video-2-data-science-for-beginners-series"></a>Video 2: Veri bilimi yeni başlayanlar seri için
Bilgi nasıl tooevaluate temel ölçütleri toobe veri bilimi için hazır karşıladığından emin, veri toomake.

tooget hello en hello serisi dışında tümünü izleyin. [Videolar toohello listesi gidin](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a>Bu serideki diğer videolar
*Yeni başlayanlar için veri bilimi* beş kısa video içinde hızlı giriş toodata bilimsel olduğu.

* Video 1: [hello 5 sorular veri bilimi yanıtlar](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 dakika 14 saniye)*
* Video 2: verileriniz için veri bilimi hazır mı?
* Video 3: [verilerle yanıt soru](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sn)*
* Video 4: [basit bir modelle bir yanıt tahmin](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sn)*
* Video 5: [diğer kişilerin çalışma toodo veri bilimi kopyalama](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 dakika 18 saniye)*

## <a name="transcript-is-your-data-ready-for-data-science"></a>Dökümü: verileriniz için veri bilimi hazır mı?
Hoş Geldiniz çok "verileriniz için veri bilimi hazır mı?" İkinci video hello serideki hello *yeni başlayanlar için veri bilimi*.  

Veri bilimi vermeden önce istediğiniz yanıtlar Merhaba, toogive sahip, bazı yüksek kaliteli hammaddeleri toowork ile. Yalnızca bir pizza yapma gibi başlangıç hello daha iyi hello malzemeleri hello daha iyi hello son ürün. 

## <a name="criteria-for-data"></a>Veriler için ölçüt
Bu nedenle, veri bilimi hello durumda biz toopull birlikte gereken bazı malzemeleri vardır.

Verileri ihtiyacımız var:

* İlgili
* bağlı
* Doğru
* Yeterli toowork ile

## <a name="is-your-data-relevant"></a>Verilerinizi ilgili mi?
Bu nedenle hello ilk tarifi - ilgili olan verileri ihtiyacımız var.

![İlgili verileri ilgisiz verilerin - karşılaştırması veri değerlendir](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

Merhaba tablosunda hello solda arayın. Biz Boston çubukları dışında yedi kişi yerine, kendi kan Alkol düzeyi, son kullanıcıların oyun hello kırmızı Sox batting ortalama ve Market en yakın hello sütlü hello fiyatını ölçülür.

Bu tüm mükemmel yasal verilerdir. İlgili değil, yalnızca hataya değildir. Bu sayılar arasında belirgin ilişkisi yoktur. I verdiyse sütlü ve hello kırmızı Sox batting ortalama geçerli fiyat Merhaba, kan Alkol İçeriğim tahmin bir yolu yoktur.

Şimdi hello sağ hello tablosuna bakın. Bu süre her birinin gövde yığın ve sayılan hello sahip İçecekler sayısı ölçülür.  Her satırda Hello numaraları diğer ilgili tooeach sunulmuştur. I size my gövde yığın ve hello sayısı sahip Margaritas verdiyse, my kan konumundaki tahmin Alkol içerik hale getirebilir.

## <a name="do-you-have-connected-data"></a>Sahip bağlı veri?
Merhaba sonraki tarifi bağlı verilerdir.

![Bağlı veri bağlantısı kesilmiş verileri - veri ölçütlerini hazır karşılaştırması](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

Hamburgers hello kalitesini bazı ilgili bilgiler aşağıdadır: sıcaklık, patty ağırlık ve hello yerel yemek dergi derecesi maske. Ancak hello boşluklar hello soldaki hello tablosundaki dikkat edin.

Çoğu veri kümelerini bazı değerler eksik. Bu gibi ortak toohave delik olduğunu ve yolları toowork etrafında. Ancak çok fazla eksik olduğundan, verilerinizi İsviçre Peynir gibi toolook başlar.

Merhaba solda hello tablosunda bakarsanız, olmadığından arasındaki ilişkiyi her türlü ile yukarı sabit toocome olduğu kadar eksik veri maske sıcaklık ve patty ağırlık. Bu, bağlantısı kesilmiş veri örneğidir.

Merhaba sağ taraftaki tablo ancak Merhaba, tam ve tamamlandı - bağlı veri örneği.

## <a name="is-your-data-accurate"></a>Verilerinizi geçerli mi?
Merhaba ihtiyacımız sonraki tarifi doğruluğu olur. Burada, dört hedefleri oklarla toohit isteriz bulunmaktadır.

![Doğru verileri yanlış data - veri ölçütlerini karşılaştırması](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

Sağ üstteki hello hello hedef bakın. Biz sağ hello hedef merkezi etrafında sıkı bir gruplandırma açıyor. Doğal olarak, doğru olur. Arasında veri bilimi hello dilde hello hedef hemen altındaki bizim performans da doğru olarak değerlendirilir.

Bu okları hello merkezi çıkışı toomap olsaydı, çok yakın toohello hedef merkezi olduğunu görürsünüz. Merhaba okları kesin olmayan kabul ancak doğru kabul şekilde hello hedef merkezi ortalanmış tüm hello hedef, geçici yayılır.

Şimdi hello sol üst hedefe arayın. Burada bizim okları çok birbirine sıkı bir gruplandırma ulaştı. Kesin ancak hello merkezi şekilde hello hedef merkezi devre dışı olduğundan, bunlar yanlış. Ve Elbette, hello sol alt hedef hello okları yanlış ve kesin. Bu archer daha fazla uygulama gerekir.

## <a name="do-you-have-enough-data-toowork-with"></a>Yeterli veri toowork ile var mı?
Son olarak, malzeme #4 - yeterli veri toohave ihtiyacımız.

![Analiz için yeterli veri var mı? Veri değerlendirme](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

Her veri noktası tablosundaki boyama içinde fırça vuruş olarak düşünün. Yalnızca birkaç tanesi sahip, hello boyama oldukça benzer olabilir - sabit tootell olup olmadığını nedir.

Daha fazla bazı fırça vuruşları eklerseniz, boyama tooget biraz daha keskin başlatır.

Neredeyse hiç yeterli vuruşları sahip olduğunuzda, bazı geniş kararları yeterli toomake görebilirsiniz. Bu bir yere toovisit istediğiniz mi? Açık görünüyor, temiz su gibi – Evet, burada tatile kullanacağım olan arar.

Daha fazla veri ekleme gibi hello resim daha anlaşılır olur ve daha ayrıntılı kararlarını verebilir. Merhaba hello sol bank üzerinde üç Oteller şimdi bakabilirim. Bildiğiniz ı gerçekten hello mimari hello ön planda hello özelliklerini ister. Merhaba üçüncü kat üzerinde kalır,.

İlgili, bağlı, doğru verilerle ve yeterli, tüm hello malzemeleri ihtiyacımız toodo bazı yüksek kaliteli veri bilimi sunuyoruz.

Diğer dört videoları hello çıkışı emin toocheck olması *yeni başlayanlar için veri bilimi* Microsoft Azure Machine learning'in.

## <a name="next-steps"></a>Sonraki adımlar
* [İlk veri bilimi denemeyi Machine Learning Studio'da deneyin](machine-learning-create-experiment.md)
* [Bir giriş tooMachine alma Microsoft Azure üzerinde öğrenme](machine-learning-what-is-machine-learning.md)
