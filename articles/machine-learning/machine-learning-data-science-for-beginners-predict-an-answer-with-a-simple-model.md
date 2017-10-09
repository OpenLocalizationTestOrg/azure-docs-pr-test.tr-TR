---
title: "aaaPredict basit regresyon modeli - Azure Machine Learning ile bir yanıt | Microsoft Docs"
description: "Nasıl toocreate basit bir regresyon modeli toopredict veri bilimi video 4 yeni başlayanlar için bir fiyat. Hedef verilerle doğrusal regresyon içerir."
keywords: "bir model, basit modeli, fiyat tahmini, basit regresyon modeli oluşturma"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: d4270c2237c33b7e898b78a08b292bc9d62e49ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a>Basit model ile yanıtı tahmin etme
## <a name="video-4-data-science-for-beginners-series"></a>Video 4: Yeni başlayanlar seri için veri bilimi
Nasıl toocreate basit regresyon modeli toopredict hello veri bilimi video 4 yeni başlayanlar için de bir Karo bedelinin öğrenin. Biz hedef verilerle bir regresyon modeli çekersiniz.

tooget hello en hello serisi dışında tümünü izleyin. [Videolar toohello listesi gidin](#other-videos-in-this-series)
<br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a>Bu serideki diğer videolar
*Yeni başlayanlar için veri bilimi* beş kısa video içinde hızlı giriş toodata bilimsel olduğu.

* Video 1: [hello 5 sorular veri bilimi yanıtlar](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 dakika 14 saniye)*
* Video 2: [verileriniz için veri bilimi hazır?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 min 56 sn)*
* Video 3: [verilerle yanıt soru](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sn)*
* Video 4: basit bir modelle bir yanıt tahmin etme
* Video 5: [diğer kişilerin çalışma toodo veri bilimi kopyalama](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 dakika 18 saniye)*

## <a name="transcript-predict-an-answer-with-a-simple-model"></a>Dökümü: basit bir modelle bir yanıt tahmin
Merhaba "Veri bilimi için yeni başlayanlar" serisi dördüncü video toohello Hoş Geldiniz. Bunu, biz basit bir model oluşturmak ve tahminde bulunmak.

A *modeli* verilerimizi ilgili basitleştirilmiş bir öykü olduğu. I ı anlamı göstereceğiz.

## <a name="collect-relevant-accurate-connected-enough-data"></a>İlgili, doğru bağlı, yeterli veri toplama
İçin bir Karo tooshop istiyorum söyleyin. Toomy adı 1,35 ayar elmas için bir ayar ile ait bir halka sahip ve tooget ne kadar maliyetlidir hakkında bir fikir istiyor. I not defteri ve Kalem hello mücevher deposuna alın ve ı hello fiyat tüm hello Karo hello çalışması ve ne kadar bunlar içinde carats tartmanız yazın. Merhaba ilk baklava - cihazın 1.01 carats ve $7,366 başlatılıyor.

Şimdi geçtikleri ve diğer Karo hello deposundaki tüm Merhaba bunu.

![Karo veri sütunlarının](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

Bizim listesi iki sütuna sahip olmadığına dikkat edin. Farklı bir öznitelik her sütununda - ağırlık carats ve fiyat - her satırda tek bir Karo temsil eden bir tek veri noktası.

Küçük bir gerçekte oluşturduk veri kümesi burada - bir tablo. Kalite bizim ölçütlerini karşılayan dikkat edin:

* Merhaba veri **ilgili** -ağırlığı olan kesinlikle ilgili tooprice
* Bunun **doğru** -biz biz yazma hello fiyatlar yeniden denetlediniz
* Bunun **bağlı** -boş boşluk yoktur ya bu sütunlar
* Ve anlatıldığı gibi var. **yeterli** veri tooanswer bizim soru

## <a name="ask-a-sharp-question"></a>NET bir soru sorun
Şimdi biz bizim soru NET bir şekilde neden: "ne kadar olacak toobuy 1,35 ayar elmas Maliyet?"

Biz toouse hello bizim veri tooget bir yanıt toohello soru geri kalanı gerekir böylece bizim listesi 1,35 ayar elmas içinde yok.

## <a name="plot-hello-existing-data"></a>Merhaba mevcut verileri Çiz
Biz gerçekleştirirsiniz hello ilk toochart hello ağırlıkları eksen adlı yatay numarası çizgi, çizme şeydir. Biz, aralık ve yarı her ayar için çizgilerine put kapsayan bir satır çekersiniz şekilde hello hello ağırlıkları 0 too2 aralığıdır.

Sonraki dikey eksen toorecord hello fiyat çizme ve toohello yatay ağırlık eksen bağlanın. Bu, ABD Doları birimlerinde olacaktır. Şimdi biz koordinat eksenleri kümesine sahiptir.

![Ağırlık ve fiyat eksenler](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

Geçerli giderek tootake bu veriler artık, içine kapatma bir *dağılım çizim*. Yo toovisualize sayısal veri kümelerini budur.

Merhaba ilk veri noktası için bir dikey satırında 1.01 carats eyeball. Ardından, $7,366 yatay satırında eyeball. Karşıladıklarından burada size bir nokta çizin. Bu bizim ilk elmas temsil eder.

Şimdi Biz bu listede her elmas gidin ve aynı şeyi hello. Biz işiniz bittiğinde, biz alma budur: bir grup noktalar, her Karo.

![Çizim dağılım](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-hello-model-through-hello-data-points"></a>Merhaba modeli hello veri noktaları aracılığıyla çizme
Merhaba noktalar ve squint bakın, şimdi hello koleksiyonu fat, benzer bir satır gibi durur. Bizim işaret alın ve düz bir çizgi geçen çizin.

Oluşturduğumuz bir satır çizerek bir *modeli*. Bu hello gerçek dünya alma ve bir simplistic çizgi sürümü yaparak olarak düşünün. Şimdi hello çizgi yanlış - hello satır tüm hello veri noktaları aracılığıyla Git değil. Ancak yararlı basitleştirme değil.

![Doğrusal regresyon satır](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

Tüm hello nokta tam olarak hello hattı üzerinden geçmez, hello olgu normaldir. Veri bilimcilerine açıklayabilir bu hello model - hello satır - olduğunu söyleyerek ve ardından her nokta bazı sahip *gürültü* veya *farkı* kendisiyle ilişkilendirilmiş. Mükemmel bir ilişki temel hello yoktur ve ardından gürültü ve belirsizlik ekler Merhaba Görünüşün, gerçek dünya yoktur.

Biz tooanswer hello soru çalıştığınızdan *ne kadar?* bu adlı bir *regresyon*. Ve bir çizgide kullanmakta olduğunuz çünkü bu bir *doğrusal regresyon*.

## <a name="use-hello-model-toofind-hello-answer"></a>Merhaba modeli toofind hello yanıt kullanın
Bir model sahibiz ve biz bizim soru sorun artık: ne kadar 1,35 ayar elmas maliyetini?

tooanswer bizim soru biz 1,35 carats göz Küresi ve de dikey çizgi çizme. Merhaba model satır kestiği burada biz yatay çizgi toohello dolar eksen eyeball. Sağ taraftaki 10.000 kadardır. Müzik! Merhaba yanıt olan: 1,35 ayar elmas yaklaşık 10.000 $ maliyetleri.

![Merhaba yanıt hello model üzerinde Bul](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a>Güvenirlik aralığını oluşturma
Bu tahmin olduğunu nasıl kesin doğal toowonder olur. Merhaba 1,35 ayar elmas çok çok yakın gerektirmeyeceğini yararlı tooknow olan $10.000 ya da çok daha yüksek veya düşük. toofigure bu çıkışı, şimdi hello nokta çoğunu içeren hello regresyon satırı geçici Zarf çizin. Bu Zarf adlı bizim *güvenirlik aralığını*: biz çünkü fiyatlar bu Zarf içinde kalan oldukça emin hello geçmiş içinde bunların çoğu vardır. Merhaba üst ve alt bu zarfın hello hello 1,35 ayar satır burada kestiği biz iki daha yatay çizgiler çizebilirsiniz.

![Güvenirlik aralığını](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

Şimdi biz bir şeyler bizim güvenirlik aralığını hakkında söyleyin: güvenle 1,35 ayar elmas hello bedelinin iş hakkında $10.000 - ancak 8000 kadar düşük olabilir ve 12.000 yüksek olabilir dediğimiz.

## <a name="were-done-with-no-math-or-computers"></a>Matematik ya da bilgisayarları bitmek
Hangi veri bilimcilerine toodo ödeme yaptığımız ve onu yalnızca çizerek yaptığımız:

* Biz biz verilerle yanıt bir soru sorular
* Oluşturduğumuz bir *modeli* kullanarak *doğrusal regresyon*
* Biz yapılan bir *tahmin*ile tam bir *güvenirlik aralığını*

Ve matematik veya bilgisayarlar toodo kullanırız alamadık.

Şimdi biz daha fazla bilgi olsaydı, ister...

* Merhaba hello elmas Kes
* renk değişimleri (ne kadar yakın hello elmas toobeing Beyaz'dır)
* Merhaba elmas içindeki içermeler Hello sayısı

.. .then biz olan daha fazla sütun. Bu durumda, Matematik yardımcı olur. İkiden fazla sütuna sahip, sabit toodraw nokta kağıda olur. Merhaba matematik, o satırdaki veya düzlemi tooyour verilerin çok iyi sığacak olanak tanır.

Ayrıca, yalnızca birkaç Karo varsa, yerine biz iki bin veya iki milyon vardı sonra çalışan bir bilgisayarla çok daha hızlı yapabilirsiniz.

Bugün, biz nasıl toodo doğrusal regresyon ve biz verileri kullanarak bir tahmini yapılan hakkında açıklandı.

Merhaba çıkışı emin toocheck "Veri bilimi için yeni başlayanlar" Microsoft Azure Machine learning'in diğer videoları olabilir.

## <a name="next-steps"></a>Sonraki adımlar
* [İlk veri bilimi denemeyi Machine Learning Studio'da deneyin](machine-learning-create-experiment.md)
* [Bir giriş tooMachine alma Microsoft Azure üzerinde öğrenme](machine-learning-what-is-machine-learning.md)
