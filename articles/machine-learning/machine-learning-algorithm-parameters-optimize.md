---
title: "aaaOptimize, Azure Machine Learning algoritmaları | Microsoft Docs"
description: "Nasıl toochoose hello en iyi Azure Machine learning'de algoritma için parametre açıklanmaktadır."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6717e30e-b8d8-4cc1-ad0b-1d4727928d32
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: fbf2f71abdbce19483fb048d67a39cbb368a928e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-parameters-toooptimize-your-algorithms-in-azure-machine-learning"></a>Azure Machine Learning, algoritmaları parametreleri toooptimize seçin
Bu konu, Azure Machine learning'de algoritma için toochoose hello sağ hyperparameter nasıl ayarlanacağını açıklar. Çoğu machine learning algoritmaları parametreleri tooset sahip. Bir modeli eğitmek için bu parametreleri tooprovide değerleri gerekir. Merhaba sürecinin hello eğitilen modeli seçtiğiniz hello modeli parametrelere bağlıdır. Merhaba hello en iyi parametreleri kümesini bulma işlemi olarak bilinir *model seçimi*.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Çeşitli yolları toodo model seçimi vardır. Machine learning'de, çapraz doğrulama model seçimi için en yaygın olarak kullanılan hello yöntemlerden birini, ve hello varsayılan model seçimi yönteminde Azure Machine Learning olur. Azure Machine Learning R ve Python desteklediğinden, R veya Python kullanarak her zaman kendi model seçimi mekanizmaları uygulayabilirsiniz.

Merhaba en iyi parametre kümesi bulma hello işleminde dört adım vardır:

1. **Merhaba parametre alan tanımlayın**: hello algoritması için ilk tooconsider istediğiniz hello tam parametre değerlerini karar verin.
2. **Merhaba çapraz doğrulama ayarlarını tanımla**: nasıl toochoose çapraz doğrulama hello veri kümesi için Katlama karar verin.
3. **Merhaba ölçümü tanımlayın**: hello en iyi doğruluğu gibi parametreleri kümesini belirlemek için hangi ölçüm toouse karar, kök ortalama karesi alınmış hata, kesinlik, geri çağırma veya f-score.
4. **Eğitim, değerlendirmek ve karşılaştırmak**: hello parametre değerlerini benzersiz her birleşimi için çapraz doğrulama tarafından yürütülen ve tanımladığınız hello hata ölçüm üzerinde temel. Değerlendirme ve karşılaştırma sonra hello en gerçekleştirme modeli seçebilirsiniz.

Görüntü aşağıdaki hello Azure Machine Learning ile bu nasıl sağlanabilir gösterir gösterilmektedir.

![Merhaba en iyi parametre kümesi Bul](./media/machine-learning-algorithm-parameters-optimize/fig1.png)

## <a name="define-hello-parameter-space"></a>Merhaba parametre alan tanımlayın
Merhaba parametre hello modeli başlatma adımda kümesi tanımlayabilirsiniz. Merhaba tüm makine öğrenimi algoritma parametresi bölmesini iki Eğitmen modu vardır: *tek bir parametre* ve *parametre aralık*. Parametre aralık modu seçin. Parametre aralık modunda her parametre için birden çok değer girebilirsiniz. Merhaba metin kutusuna, virgülle ayrılmış değerler girebilirsiniz.

![İki sınıflı artırılmış karar ağacı, tek bir parametre](./media/machine-learning-algorithm-parameters-optimize/fig2.png)

 Alternatif olarak, hello maksimum ve minimum noktaları hello kılavuz ve noktaları toobe ile oluşturulan toplam sayısı hello tanımlayabilirsiniz **kullanım aralık oluşturucu**. Varsayılan olarak, hello parametre değerlerini doğrusal bir ölçekte üretilir. Ancak **günlük ölçek** denetlenir hello değerleri hello günlük ölçek oluşturulur (diğer bir deyişle, hello hello bitişik noktalarının yerine kendi fark sabit orandır). Tamsayı Parametreler için kısa çizgi kullanarak bir aralığı tanımlayabilirsiniz. Örneğin, "1-10" anlamına gelir tüm tamsayılar 1 ile 10 arasında (her ikisi de dahil) hello parametre kümesi oluşturur. Karma mod da desteklenir. Örneğin, parametre kümesi'ni hello "1-10, 20, 50" tamsayılar 1-10, 20, içerir ve 50.

![İki sınıflı artırılmış karar ağacı, parametre aralığı](./media/machine-learning-algorithm-parameters-optimize/fig3.png)

## <a name="define-cross-validation-folds"></a>Çapraz doğrulama Katlama tanımlayın
Merhaba [bölüm ve örnek] [ partition-and-sample] modülü kullanılan toorandomly Ata Katlama toohello veri olabilir. Merhaba modülü için örnek yapılandırma aşağıdaki hello, biz beş Katlama tanımlayın ve rastgele sayı toohello örnek örnekleri bir Katlama atayın.

![Bölüm ve örnek](./media/machine-learning-algorithm-parameters-optimize/fig4.png)

## <a name="define-hello-metric"></a>Merhaba ölçümü tanımlayın
Merhaba [Model ayarlama Hiperparametreleri] [ tune-model-hyperparameters] modülü empirically hello en iyi verilen algoritması ve veri kümesi için parametre kümesi seçme için destek sağlar. Ayrıca eğitim hello ilişkin tooother bilgi modeli hello **özellikleri** Bu modülün bölmesi hello en iyi parametre kümesini belirlemek için hello ölçüm içerir. Sınıflandırma ve regresyon algoritmalar için iki farklı aşağı açılan liste kutusu sırasıyla sahiptir. Merhaba algoritması odaklanılan bir sınıflandırma algoritmasıdır ise, hello regresyon ölçüm göz ardı edilir ve tersi. Bu belirli örnekte hello ölçümüdür **doğruluğu**.   

![Tarama parametreleri](./media/machine-learning-algorithm-parameters-optimize/fig5.png)

## <a name="train-evaluate-and-compare"></a>Eğitim, değerlendirmek ve karşılaştırma
aynı hello [Model ayarlama Hiperparametreleri] [ tune-model-hyperparameters] modülü eğitir toohello parametre kümesi karşılık gelen, çeşitli ölçümleri değerlendirir ve ardından hello en eğitilen model üzerinde hello temel oluşturan tüm hello modelleri Seçtiğiniz ölçüm. Bu modül iki zorunlu giriş vardır:

* Merhaba eğitimsiz öğrenen
* Merhaba veri kümesi

Merhaba modülü de giriş isteğe bağlı bir veri kümesine sahiptir. Merhaba dataset Katlama bilgi toohello zorunlu dataset girişle bağlayın. Merhaba veri kümesi herhangi bir Katlama bilgi atanmamışsa bir 10-fold çapraz doğrulama otomatik olarak varsayılan olarak yürütülür. Hello Katlama atama yapılmaz ve doğrulama dataset hello isteğe bağlı veri kümesi bağlantı noktalarından sağlanan tren test modu seçilir ve hello ilk veri kümesini kullanılan tootrain hello her parametre birleşimi için modelidir.

![Artırılmış karar ağacı sınıflandırıcı](./media/machine-learning-algorithm-parameters-optimize/fig6a.png)

Merhaba modeli sonra hello doğrulama dataset üzerinde değerlendirilir. Merhaba hello modülü gösterir çıkış bağlantı noktasına parametre değerleri olarak işlevler farklı ölçümleri kalmadı. Merhaba çıkış bağlantı noktasına verir ölçüm seçilen toohello göre toohello en gerçekleştirme modeli karşılık gelen hello eğitilen model sağ (**doğruluğu** bu durumda).  

![Doğrulama veri kümesi](./media/machine-learning-algorithm-parameters-optimize/fig6b.png)

Merhaba tam parametreleri hello sağ çıkış bağlantı noktasına görselleştirme tarafından seçilen görebilirsiniz. Bu model, bir sınama kümesi Puanlama veya bir kullanıma hazır hale getirilmiş web hizmeti modeli olarak kaydettikten sonra kullanılabilir.

<!-- Module References -->
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[tune-model-hyperparameters]: https://msdn.microsoft.com/library/azure/038d91b6-c2f2-42a1-9215-1f2c20ed1b40/
