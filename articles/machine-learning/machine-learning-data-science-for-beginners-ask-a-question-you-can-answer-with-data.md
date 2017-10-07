---
title: "bir soru verileri yanıt - aaaAsk veri bilimi sorunlarını - Azure Machine Learning | Microsoft Docs"
description: "Nasıl tooformulate sharp veri bilimi soru yeni başlayanlar için veri bilimi içinde video 3 öğrenin. Sınıflandırma ve regresyon soruları karşılaştırması içerir."
keywords: "Veri bilimi sorunları, veri bilimi soruları formüle sorular, regresyon sorular, sınıflandırma sorular, sharp soru"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: 5b9501e3-9964-417a-8ffc-8913103da77b
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 00c328f51e6d9ff6654b5966eb97d6762582f7e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ask-a-question-you-can-answer-with-data"></a>Verilerle yanıtlayabileceğiniz bir soru sorun
## <a name="video-3-data-science-for-beginners-series"></a>Video 3: Yeni başlayanlar seri için veri bilimi
Bilgi nasıl tooformulate video 3 yeni başlayanlar için veri bilimi sorusuna bir veri bilimi sorunla. Bu videoda, Sınıflandırma ve regresyon algoritmalar için sorular karşılaştırması içerir.

tooget hello en hello serisi dışında tümünü izleyin. [Videolar toohello listesi gidin](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Data-science-for-beginners-Ask-a-question-you-can-answer-with-data/player]
>
>

## <a name="other-videos-in-this-series"></a>Bu serideki diğer videolar
*Yeni başlayanlar için veri bilimi* beş kısa video içinde hızlı giriş toodata bilimsel olduğu.

* Video 1: [hello 5 sorular veri bilimi yanıtlar](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 dakika 14 saniye)*
* Video 2: [verileriniz için veri bilimi hazır?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 min 56 sn)*
* Video 3: verilerle yanıtlayabilir bir soru sorun
* Video 4: [basit bir modelle bir yanıt tahmin](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sn)*
* Video 5: [diğer kişilerin çalışma toodo veri bilimi kopyalama](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 dakika 18 saniye)*

## <a name="transcript-ask-a-question-you-can-answer-with-data"></a>Dökümü: verilerle yanıtlayabilir bir soru sorun
"Yeni başlayanlar için veri bilimi." Merhaba serideki toohello üçüncü video Hoş Geldiniz  

Bu birinde verilerle yanıtlayabilir soru formulating için bazı ipuçları elde edersiniz.

Merhaba iki önceki videolar bu serideki ilk izleme, bu videoda dışında daha fazla bilgi alabilirsiniz: "Merhaba 5 soruları veri bilimi yanıtlayabilir" ve "verileriniz için veri bilimi hazır mı?"

## <a name="ask-a-sharp-question"></a>NET bir soru sorun
Nasıl veri bilimi (kategorileri veya etiketleri olarak da adlandırılır) adlarını kullanarak hello ve işlemidir bir yanıt tooa soru toopredict numaralar hakkında açıklandı. Ancak herhangi bir soru olamaz; toobe sahip bir *sharp soru.*

Belirsiz bir soru bir ad veya sayı ile yanıtlanan toobe sahip değil. Sharp soru gerekir.

Sihirli ampul istenir soru truthfully yanıtlayacak bir genie ile bulunan düşünün. Ancak yaramaz genie olan ve kendisine hemen ile alabilirsiniz gibi kendisinin toomake kendi yanıt belirsiz ve kafa karıştırıcı olarak deneyeceksiniz. Toopin ona aşağı bir soruyla kendisi olamaz yardımcı olur ancak ne yapacağımı, bu nedenle airtight istediğiniz tooknow istiyor.

Tooask belirsiz bir soru olsaydı gibi "Benim hisse senedi ile toohappen neler olduğunu?", "Merhaba fiyatı değişir" Merhaba genie yanıt. Gerçek bir yanıt olan, ancak çok yararlı değildir.

Ancak tooask "ne my hisse senedi 's satış fiyatı sonraki hafta?", hello genie olamaz Yardım ancak belirli bir size gibi keskin bir soru olsaydı yanıtlayın ve satış fiyatını tahmin etmek.

## <a name="examples-of-your-answer-target-data"></a>Yanıtınız örnekleri: hedef veri
Sorunuzun yanıtını formüle sonra toosee verilerinizi hello yanıt örnekleri olup olmadığını denetleyin.

Bizim Soru "Ne my hisse senedi 's satış fiyatı sonraki hafta olacak?" ise Daha sonra toomake verilerimizi hello stok fiyat geçmişi içerdiğinden emin sağlayın.

Bizim Soru "hangi otomobil my Donanma içinde giderek toofail ilk?" ise Daha sonra toomake verilerimizi önceki hataları hakkında bilgi içerdiğinden emin sağlayın.

![Hedef verileri - yanıtınız örnekleri. Bir veri bilimi soru formüle.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/target-data.png)

Bu örnek yanıt olarak bir hedef adı verilir. Biz nelerdir bir hedefi olan bir kategori veya bir sayı olup olmadığını toopredict gelecekteki veri noktaları hakkında çalışıyor.

Herhangi bir hedef veri yoksa, tooget bazı gerekir. Sorunuzu olmadan mümkün tooanswer olmayacaktır.

## <a name="reformulate-your-question"></a>Sorunuzu reformulate
Bazen, soru tooget daha kullanışlı bir yanıtı yeniden ifade et.

Merhaba Soru "Bu veri noktası A veya B mi?" Merhaba kategorisi (adını veya etiketi), bir şeyin tahmin eder. tooanswer, kullandığımız bir *sınıflandırma algoritmasıdır*.

Merhaba Soru "Ne kadar?" veya "Kaç?" bir miktar tahmin eder. tooanswer, kullandığımız bir *regresyon algoritması*.

toosee Biz bu, dönüştürebilirsiniz nasıl bakalım "hangi haber Öykü hello en ilginç toothis okuyucu mi?" Merhaba soru Bu çok sayıda olasılıklar - arasından tek bir seçim tahminini diğer bir deyişle "Bu A veya B veya C D mi?" ister - ve bir sınıflandırma algoritmasıdır kullanırsınız.

Ancak yeniden ifade olarak et değilse bu soruyu daha kolay tooanswer olabilir "Bu liste toothis okuyucu üzerinde her hikayesinin nasıl ilginç?" Şimdi bir sayısal puan her makale verebilirsiniz ve kolay tooidentify hello Puanlama yüksek makale ise. Merhaba sınıflandırma soru regresyon soru içine yeniden budur veya ne kadar?

![Sorunuzu reformulate. Sınıflandırma soru regresyon soru karşılaştırması.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/classification-question-vs-regression-question.png)

Nasıl bir soru bir ipucu toowhich algoritmasıdır isteyin, bir yanıt verebilirsiniz.

Algoritma - haber Öykü örneğimizde - hello olanlar gibi bazı aileleri yakından ilişkilidir bulabilirsiniz. Size sunar, soru toouse hello algoritması reformulate hello en yararlı yanıt.

Ancak, en önemlisi, o sharp soru - verilerle yanıtlayabilir hello soru sorun. Ve hello doğru verileri tooanswer sahip olduğundan emin olun.

Verilerle yanıtlayabilir bir soru sormak bazı temel ilkeleri hakkında açıklandı.

Merhaba çıkışı emin toocheck "Veri bilimi için yeni başlayanlar" Microsoft Azure Machine learning'in diğer videoları olabilir.

## <a name="next-steps"></a>Sonraki adımlar
* [İlk veri bilimi denemeyi Machine Learning Studio'da deneyin](machine-learning-create-experiment.md)
* [Bir giriş tooMachine alma Microsoft Azure üzerinde öğrenme](machine-learning-what-is-machine-learning.md)
