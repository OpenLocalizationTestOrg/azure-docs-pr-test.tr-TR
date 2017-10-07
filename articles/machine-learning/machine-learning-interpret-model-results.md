---
title: "Machine Learning modeli sonuçlarında aaaInterpret | Microsoft Docs"
description: "Nasıl toochoose hello en iyi parametresini kullanarak ve score model çıkışları görselleştirmek için bir algoritma ayarlayın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6230e5ab-a5c0-4c21-a061-47675ba3342c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52161b1aa5ff3e7a63fc4b1bfb7c5e354eabcc50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="interpret-model-results-in-azure-machine-learning"></a>Azure Machine Learning modeli sonuçlarında yorumlama
Bu konuda açıklanmaktadır nasıl toovisualize ve Azure Machine Learning Studio'da tahmin sonuçlarını çevirebilir. Bir model eğitilmiş ve Öngörüler ("Merhaba modeli skoru") en üstünde bitti sonra toounderstand gerekir ve hello tahmin sonuç yorumlama.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Machine learning Azure Machine Learning modellerini dört ana tür vardır:

* Sınıflandırma
* Kümeleme
* regresyon
* Öneren sistemleri

Bu modeller üstünde tahmin için kullanılan hello modülleri şunlardır:

* [Modeli Puanlama] [ score-model] sınıflandırma ve regresyon için Modülü
* [TooClusters Ata] [ assign-to-clusters] kümeleme Modülü
* [Matchbox öneren puan] [ score-matchbox-recommender] önerisi sistemleri

Bu belge, bu modüllerin her biri için nasıl toointerpret tahmin sonuçlarını açıklar. Bu modüller genel bakış için bkz: [nasıl toochoose parametreleri toooptimize, Azure Machine Learning algoritmaları](machine-learning-algorithm-parameters-optimize.md).

Bu konu, tahmin yorumlama ancak değil modeli değerlendirme giderir. Hakkında daha fazla bilgi için tooevaluate modelinizde Bkz [nasıl tooevaluate model Azure Machine Learning performans](machine-learning-evaluate-model-performance.md).

Yeni tooAzure Machine Learning olan ve başlatılan bir basit deneme tooget oluşturmaya yardımcı olmak için bkz: ihtiyacınız varsa [Azure Machine Learning Studio'da basit bir deneme oluşturmak](machine-learning-create-experiment.md) Azure Machine Learning Studio'da.

## <a name="classification"></a>Sınıflandırma
Sınıflandırma sorunları iki alt kategorileri şunlardır:

* Yalnızca iki sınıf (iki sınıflı veya ikili sınıflandırma) sorunları
* İkiden fazla sınıfları (çok sınıfı sınıflandırma) sorunları

Azure Machine Learning için bu türleri sınıflandırmaya sahip farklı modülleri toodeal olsa da, kendi tahmin sonuçları yorumlayarak hello yöntemleri benzerdir.

### <a name="two-class-classification"></a>İki sınıflı sınıflandırma
**Örnek deneme**

İki sınıflı sınıflandırma sorunu iris çiçekler hello sınıflandırılması örnektir. Merhaba, bunların özelliklerini temel alarak tooclassify iris çiçekler görevdir. Merhaba Iris veri Azure Machine Learning ile sağlanan bir alt kümesini hello popüler kümesidir [Iris veri kümesi](http://en.wikipedia.org/wiki/Iris_flower_data_set) iki sağındaki (0 ve 1 sınıflar) çiçek yalnızca örneklerini içeren. Her çiçek (sepal uzunluğu, sepal genişlik, petal uzunluğu ve petal genişliği) için dört özellikler vardır.

![İris deneme ekran görüntüsü](./media/machine-learning-interpret-model-results/1.png)

Şekil 1 '. Iris iki sınıflı sınıflandırma sorunu deneme

Bir deneme gerçekleştirilen toosolve Şekil 1'de gösterildiği gibi bu sorun olmuştur. İki sınıflı artırılmış karar ağacı modeli eğitilmiş ve skoru. Merhaba hello tahmin sonuçlarını görselleştirme artık [Score Model] [ score-model] hello hello çıkış bağlantı noktasına tıklayarak Modülü [Score Model] [ score-model]modülü ve ardından **Görselleştir**.

![Score model Modülü](./media/machine-learning-interpret-model-results/1_1.png)

Bu Şekil 2'de gösterildiği gibi sonuçları Puanlama hello getirir.

![İris iki sınıflı sınıflandırma deneme sonuçları](./media/machine-learning-interpret-model-results/2.png)

Şekil 2. İki sınıflı sınıflandırma score model sonucunda Görselleştirme

**Sonuç yorumlama**

Merhaba sonuçlar tablosunda altı sütun vardır. Merhaba sol dört sütun hello dört özellikleridir. Merhaba sağda iki sütun, skoru etiketleri ve skoru olasılıklar hello tahmin sonuçlarını vardır. Merhaba skoru olasılıklar sütun gösterir hello olasılık çiçek toohello pozitif sınıfı (sınıf 1) ait. Örneğin, ilk numara var. ilk çiçek hello 0.028571 olasılık tooClass 1 ait hello sütun (0.028571) anlamına gelir hello. Merhaba skoru etiketleri sütun gösterir hello her çiçek için sınıf tahmin. Bu hello skoru olasılıklar sütunu temel alır. Bir çiçek olasılığını belirtmek hello 0,5 büyükse, sınıf 1 olarak tahmin. Aksi takdirde sınıfı 0 tahmin.

**Web hizmet yayımı**

Merhaba tahmin sonuçlarını anlamış ve ses nitelendirilmiştir sonra böylece çeşitli uygulamalar dağıtmak ve tüm yeni Iris çiçek üzerinde tooobtain sınıfı tahminleri çağrı hello deneme bir web hizmeti olarak yayımlanabilir. toolearn toochange bir eğitim Puanlama deneme deneyin ve bir web hizmeti olarak yayımlama nasıl bkz [yayımlama hello Azure Machine Learning web hizmeti](machine-learning-walkthrough-5-publish-web-service.md). Bu yordam ile Puanlama bir deneme, Şekil 3'te gösterildiği gibi sağlar.

![Deneme Puanlama işleminin ekran görüntüsü](./media/machine-learning-interpret-model-results/3.png)

Şekil 3 '. Puanlama hello iris iki sınıflı sınıflandırma sorunu deneme

Şimdi tooset hello giriş ve çıkış hello web hizmeti için gerekir. Merhaba giriş hello sağ giriş bağlantı noktasıdır [Score Model][score-model], Iris çiçek özellikleri giriş hello. Merhaba hello çıkış seçimine olup, ilgi bağlıdır hello sınıfı (puanlanmış etiketi) tahmin, hello skoru olasılık ya da her ikisini de. Bu örnekte, her ikisinde de ilginizi varsayılır. tooselect hello çıktı sütunları, kullanmak istediğiniz bir [veri kümesinde Sütun Seç] [ select-columns] modülü. ' I tıklatın [veri kümesinde Sütun Seç][select-columns], tıklatın **başlatma Sütun seçiciyi**seçip **skoru etiketleri** ve **skoru olasılıklar**. Merhaba çıkış bağlantı noktasına ayarlandıktan sonra [veri kümesinde Sütun Seç] [ select-columns] ve yeniden çalıştırmayı, hazır toopublish hello Puanlama deneme bir web hizmeti olarak tıklayarak **WEB'i Yayımla Hizmet**. Merhaba son deneme Şekil 4 gibi görünüyor.

![Merhaba iris iki sınıflı sınıflandırma deneme](./media/machine-learning-interpret-model-results/4.png)

Şekil 4 '. Bir iris iki sınıflı sınıflandırma sorununun son Puanlama deneme

Merhaba web hizmetini çalıştırmak ve bir test örneğinin bazı özellik değerleri girin sonra iki sayının hello sonucunu döndürür. Merhaba ilk sayı hello etiket belirtmek ve hello ikinci olasılık skoru hello. Bu çiçek sınıfı 1 olarak 0.9655 olasılık ile tahmin.

![Test yorumlama score model](./media/machine-learning-interpret-model-results/4_1.png)

![Puanlama test sonuçları](./media/machine-learning-interpret-model-results/5.png)

Şekil 5. Web hizmeti sonucu iris iki sınıflı sınıflandırma

### <a name="multi-class-classification"></a>Birden çok sınıf sınıflandırma
**Örnek deneme**

Bu deneme içinde bir harf tanıma görev çok sınıflı sınıflandırma örneği olarak gerçekleştirin. Merhaba sınıflandırıcı toopredict belirli bir deneme hello elle yazılmış görüntülerden ayıklanan bazı elle yazılmış öznitelik değerleri temel harf (sınıfı).

![Harf tanıma örneği](./media/machine-learning-interpret-model-results/5_1.png)

Merhaba eğitim verileri içinde elle yazılmış harf görüntülerden ayıklanan 16 özellikler vardır. Merhaba 26 harf bizim 26 sınıfları oluşturur. Bir sınama veri kümesi kümesinde çok sınıflı sınıflandırma eğitmek bir denemeyi harf tanıma için model ve hello üzerinde aynı tahmin 6 gösterir özelliğini kullanın.

![Harf tanıma çok sınıflı sınıflandırma deneme](./media/machine-learning-interpret-model-results/6.png)

Şekil 6. Harf tanıma çok sınıflı sınıflandırma sorunu deneme

Merhaba Hello sonuçlarını görselleştirme [Score Model] [ score-model] hello çıkış bağlantı noktasına tıklayarak Modülü [Score Model] [ score-model] modülü ve ardından tıklatarak **Görselleştir**, içerik Şekil 7'de gösterildiği gibi görmeniz gerekir.

![Score model sonuçları](./media/machine-learning-interpret-model-results/7.png)

Şekil 7. Birden çok sınıf sınıflandırma içinde Puanlama modeli sonuçlarını Görselleştirme

**Sonuç yorumlama**

Merhaba sol 16 sütundan hello test kümesinin hello özellik değerleri temsil eder. Merhaba sütunlar skoru olasılıklar sınıf "XX" için yalnızca hello skoru olasılıklar sütun gibi hello iki sınıflı durumda olduğu gibi adlara sahip. Bunlar, karşılık gelen bir giriş hello hello olasılık belirli bir sınıfına denk gösterir. Örneğin, hello ilk giriş için bir "A", "B" ve benzeri olduğunu 0.000451 olasılık olduğunu 0.003571 olasılık yoktur. Merhaba son sütun (Scored etiketleri) olan hello aynı skoru etiketleri hello iki sınıflı durumda. Hello en büyük olasılık hello karşılık gelen bir giriş tahmin edilen sınıfının hello gibi skoru hello sınıfıyla seçer. Örneğin, hello en büyük olasılık toobe bir "F" (0.916995) sahip olduğundan hello ilk giriş etiketi skoru hello "F" dosyasıdır.

**Web hizmet yayımı**

Etiket etiket skoru hello için her giriş ve hello olasılık skoru hello de alabilirsiniz. Merhaba temel mantığı toofind hello en büyük olasılıklar skoru tüm hello arasında olasılıktır. toodo bunu toouse hello gereksinim [R betiği yürütün] [ execute-r-script] modülü. Merhaba R kodu Şekil 8'de gösterilen ve Şekil 9'hello deneme hello sonucunu gösterilir.

![R kod örneği](./media/machine-learning-interpret-model-results/8.png)

Şekil 8'de. Merhaba etiketlerinin olasılıklar skoru etiketleri ve hello ayıklanacağı R kodu ilişkili

![Deneme sonucu](./media/machine-learning-interpret-model-results/9.png)

Şekil 9. Merhaba harf tanıma çok sınıflı sınıflandırma sorununun son Puanlama deneme

Yayımlama hello web hizmetini çalıştırmak ve bazı giriş özellik değerleri girin sonra hello Şekil 10 görülüyor sonuç döndürdü. Bu elle yazılmış harf ayıklanan 16 özelliklerini 0.9715 olasılık ile tahmin edilen toobe "T" dir.

![Sınama yorumlama puan Modülü](./media/machine-learning-interpret-model-results/9_1.png)

![Test sonucu](./media/machine-learning-interpret-model-results/10.png)

Şekil 10. Web hizmeti sonucu çok sınıflı sınıflandırma

## <a name="regression"></a>regresyon
Regresyon sorunları sınıflandırma sorunlarında farklıdır. Bir sınıflandırma sorunu gibi hangi sınıfın ait olduğu bir iris çiçek toopredict ayrık sınıfları deniyorsunuz. Ancak bir regresyon sorununun örneği aşağıdaki hello görebileceğiniz gibi toopredict bir araba fiyatını hello gibi sürekli bir değişken çalıştığınız.

**Örnek deneme**

Otomobil fiyat tahmini regresyon için örnek olarak kullanın. Toopredict hello fiyat yapma, yakıt türü, gövde türü ve sürücü tekerleği dahil olmak üzere kendi özelliklerini temel alarak bir araba çalışıyorsunuz. Merhaba deneme Şekil 11'de gösterilir.

![Otomobil fiyat regresyon denemesini](./media/machine-learning-interpret-model-results/11.png)

Şekil 11. Otomobil fiyat regresyon sorun deneme

Görselleştirme hello [Score Model] [ score-model] modülü, hello sonuç Şekil 12 gibi görünüyor.

![Otomobil fiyat tahmini soruna yönelik Puanlama sonuçları](./media/machine-learning-interpret-model-results/12.png)

Şekil 12. Merhaba otomobil fiyat tahmini soruna yönelik Puanlama sonucu

**Sonuç yorumlama**

Bu Puanlama sonuç hello sonuç sütununu puanlanmış etiketler var. Merhaba, her araba için tahmin edilen fiyat hello numaralarıdır.

**Web hizmet yayımı**

Bir web hizmeti içine hello regresyon denemesini yayımlamak ve çağrısından hello içinde otomobil fiyat tahmini için hello iki sınıflı sınıflandırma olduğu gibi kullanım örneği.

![Otomobil fiyat regresyon sorun için deneme Puanlama](./media/machine-learning-interpret-model-results/13.png)

Şekil 13. Bir otomobil fiyat regresyon sorununun deneme Puanlama

Merhaba Hello web hizmetini çalıştıran Şekil 14 görülüyor sonuç döndürdü. Bu otomobil için tahmin edilen fiyat Hello $15,085.52 olur.

![Sınama yorumlama Puanlama Modülü](./media/machine-learning-interpret-model-results/13_1.png)

![Puanlama modülü sonuçları](./media/machine-learning-interpret-model-results/14.png)

Şekil 14. Web hizmeti bir otomobil fiyat regresyon sorun sonucu

## <a name="clustering"></a>Kümeleme
**Örnek deneme**

Merhaba Iris veri kümesini yeniden toobuild bir kümeleme deneme kullanalım. Burada yalnızca özelliklere sahiptir ve kümeleme için kullanılabilir böylece hello sınıfı etiketleri hello veri kümesindeki çıkışı filtreleyebilirsiniz. Bu iris kullanım, kümeleri toobe iki iki sınıf halinde hello çiçekler küme anlamına gelir hello eğitim işlemi sırasında hello sayısını belirtin. Merhaba deneme Şekil 15'te gösterilir.

![Iris kümeleme sorun denemeler](./media/machine-learning-interpret-model-results/15.png)

Şekil 15. Iris kümeleme sorun denemeler

Merhaba eğitim veri kümesinin başından başlayarak gerçekte etiketleri tek başına yok kümeleme sınıflandırma farklıdır. Kümeleme grupları eğitim veri kümesi örneklerinin ayrı kümeler halinde hello. Merhaba eğitim işlemi sırasında özelliklerine hello farklarını öğrenerek hello modeli etiketleri girişleri hello. Bundan sonra hello eğitilen model kullanılabilir toofurther sınıflandırmak gelecekteki girişleri. Biz kümeleme sorun içinde ilgilendiğiniz hello sonucunun iki bölümü vardır. Merhaba ilk bölümü hello eğitim veri kümesi etiketleme ve hello ikinci hello eğitilen model ile yeni bir veri kümesi sınıflandırma.

Merhaba hello sonuç ilk bölümü çıkış bağlantı noktasına sol hello tıklayarak canlandırılabilir [tren kümeleme modelinde] [ train-clustering-model] ve ardından **Görselleştir**. Şekil 16'Hello görselleştirme gösterilir.

![Kümeleme sonucu](./media/machine-learning-interpret-model-results/16.png)

Şekil 16. Sonuç hello eğitim veri kümesi için kümeleme Görselleştirme

Yeni girişlerle hello eğitilen kümeleme modeli, kümeleme hello ikinci bölümü Hello sonucunu şekil 17'de gösterilir.

![Sonuç kümeleme Görselleştirme](./media/machine-learning-interpret-model-results/17.png)

Şekil 17. Yeni bir veri kümesi üzerinde sonuç kümeleme Görselleştirme

**Sonuç yorumlama**

Farklı deneme aşamaları hello iki bölümden Hello sonuçlarını gövdesi rağmen göründükleri aynı hello ve hello yorumlanır aynı şekilde. Merhaba ilk dört sütun özellikleridir. Merhaba son sütun, atamaları hello tahmin sonucudur. aynı sayı tahmin hello atanan girişleri hello diğer bir deyişle, aynı küme hello toobe benzerlikler (Bu deneme kullanır hello varsayılan Euclidean uzaklığı ölçüm) bir şekilde paylaşır. Kümeleri toobe 2 hello sayısı belirtilmediğinden atamaları hello girişleri 0 veya 1 etiketlenir.

**Web hizmet yayımı**

Bir web hizmetine deneme kümeleme hello yayımlayın ve kümeleme Öngörüler aynı şekilde hello iki sınıflı sınıflandırmasında kullanım örneği hello için çağırın.

![Deneme iris kümeleme sorunu Puanlama](./media/machine-learning-interpret-model-results/18.png)

Şekil 18. Deneme iris kümeleme sorununun Puanlama

Sonra hello web hizmetini çalıştırmak hello şekil 19 görülüyor sonuç döndürdü. Bu çiçek 0 kümedeki tahmin edilen toobe ' dir.

![Test Puanlama modülü yorumlama](./media/machine-learning-interpret-model-results/18_1.png)

![Puanlama modülü sonuç](./media/machine-learning-interpret-model-results/19.png)

Şekil 19. Web hizmeti sonucu iris iki sınıflı sınıflandırma

## <a name="recommender-system"></a>Öneren sistem
**Örnek deneme**

Öneren sistemleri için örnek olarak hello Restoran öneri sorun kullanabilirsiniz: müşteriler kendi derecelendirme geçmiş temelinde Restoran öneririz. Merhaba giriş verileri üç bölümden oluşur:

* Müşterilerden Restoran derecelendirme
* Müşteri özellik verileri
* Restoran özelliği verileri

Biz ile Merhaba yapabilir birkaç şey vardır [tren Matchbox öneren] [ train-matchbox-recommender] Azure Machine Learning modülünde:

* Verilen kullanıcı ve madde derecelendirmesi tahmin etme
* Kullanıcıya verilen öğeleri tooa önerilir
* Kullanıcıya verilen kullanıcılar ilgili tooa Bul
* Öğe verilen öğeleri ilgili tooa Bul

Toodo hello hello dört seçeneklerinde seçerek istediğinizi seçebilirsiniz **öneren tahmin türü** menüsü. Burada tüm dört senaryolar üzerinden yol.

![Matchbox öneren](./media/machine-learning-interpret-model-results/19_1.png)

Tipik bir Azure Machine Learning deneme öneren sistemi Şekil 20 gibi görünüyor. Bu öneren sistem modüller toouse nasıl görürüm hakkında bilgi için [tren matchbox öneren] [ train-matchbox-recommender] ve [puan matchbox öneren] [ score-matchbox-recommender].

![Öneren sistem deneme](./media/machine-learning-interpret-model-results/20.png)

Şekil 20. Öneren sistem deneme

**Sonuç yorumlama**

**Verilen kullanıcı ve madde derecelendirmesi tahmin etme**

Seçerek **derecelendirme tahmin** altında **öneren tahmin türü**, verilen kullanıcı ve öğesi için derecelendirme sistem toopredict hello hello öneren istiyoruz. Merhaba hello görselleştirme [puan Matchbox öneren] [ score-matchbox-recommender] çıkış şekil 21 gibi görünüyor.

![Tahmin derecelendirme hello öneren sistemi--sonucunu puan](./media/machine-learning-interpret-model-results/21.png)

Şekil 21. Merhaba öneren sistem--derecelendirme tahmin Hello puan sonucu Görselleştirme

Merhaba ilk iki sütun hello giriş verisi tarafından sağlanan hello kullanıcı öğesi çiftleridir. Merhaba üçüncü sütun bir kullanıcı belirli bir öğe için tahmin edilen derecesi hello. Örneğin, hello ilk satırda U1048 olduğu müşteri toorate Restoran 135026 2 olarak tahmin.

**Kullanıcıya verilen öğeleri tooa önerilir**

Seçerek **öğesi öneri** altında **öneren tahmin türü**, kullanıcıya verilen sistem toorecommend öğeleri tooa hello öneren istiyoruz. Bu senaryoda Hello son parametre toochoose olan *öğe seçimi önerilen*. Merhaba seçeneği **gelen derecelendirilmiş öğeleri (model değerlendirme)** hello eğitim işlemi sırasında model değerlendirme öncelikle içindir. Bu tahmin aşaması için seçeneğini belirledik **gelen tüm öğeleri**. Merhaba hello görselleştirme [puan Matchbox öneren] [ score-matchbox-recommender] çıkış Şekil 22 gibi görünüyor.

![Öneren sistem--öğesi öneri puan sonucu](./media/machine-learning-interpret-model-results/22.png)

Şekil 22. Merhaba öneren sistem--öğesi öneri puan sonucunu Görselleştirme

kullanıcı kimliklerini toorecommend öğeleri için verilen hello altı sütunları temsil hello ilk hello giriş verisi tarafından sağlanan gibi hello. Merhaba diğer beş sütunlar toohello kullanıcı ilgi azalan düzende önerilen hello öğeler temsil eder. Örneğin, hello ilk satırda hello en Restoran müşteri U1048 135018, 134975, 135021 ve 132862 tarafından izlenen 134986 önerilir.

**Kullanıcıya verilen kullanıcılar ilgili tooa Bul**

Seçerek **ilgili kullanıcıları** altında **öneren tahmin türü**, sistem toofind ilgili kullanıcılara verilen tooa kullanıcı hello öneren istiyoruz. Benzer Tercihler sahip hello kullanıcılar ilgili kullanıcılardır. Bu senaryoda Hello son parametre toochoose olan *ilgili kullanıcı seçimi*. Merhaba seçeneği **gelen kullanıcılar, derecelendirilmiş öğeleri (model değerlendirme)** hello eğitim işlemi sırasında model değerlendirme öncelikle içindir. Seçin **tüm kullanıcıların** bu tahmin aşaması için. Merhaba hello görselleştirme [puan Matchbox öneren] [ score-matchbox-recommender] çıkış şekil 23 gibi görünüyor.

![Öneren sistem--ilgili kullanıcıları puan sonucu](./media/machine-learning-interpret-model-results/23.png)

Şekil 23. Merhaba öneren sisteminin--ilgili kullanıcıları Puanlama sonuçlarını Görselleştirme

ilk hello hello altı sütunları gösterir hello kullanıcı gerekli kimlikleri toofind verilen kullanıcılar, giriş verisi tarafından sağlanan gibi ilgili. Merhaba diğer beş sütun deposu hello hello kullanıcının ilgi azalan düzende tahmin edilen ilgili kullanıcıları. Örneğin, hello ilk satırında, müşteri U1048 için en uygun müşteri hello U1066, U1044, U1017 ve U1072 tarafından izlenen U1051 ' dir.

**Öğe verilen öğeleri ilgili tooa Bul**

Seçerek **ilgili öğeler** altında **öneren tahmin türü**, sistem toofind ilgili öğeler verilen tooa öğesini hello öneren istiyoruz. Öğeleri hello öğeleri büyük olasılıkla toobe beğendiğinizi hello tarafından aynı ilgili kullanıcı. Bu senaryoda Hello son parametre toochoose olan *ilgili öğe seçimi*. Merhaba seçeneği **gelen derecelendirilmiş öğeleri (model değerlendirme)** hello eğitim işlemi sırasında model değerlendirme öncelikle içindir. Seçeneğini belirledik **gelen tüm öğeleri** bu tahmin aşaması için. Merhaba hello görselleştirme [puan Matchbox öneren] [ score-matchbox-recommender] çıkış şekil 24 gibi görünüyor.

![Puan sonuç öneren sisteminin--ilgili öğeler](./media/machine-learning-interpret-model-results/24.png)

Şekil 24. Merhaba öneren sisteminin--ilgili öğeler Puanlama sonuçlarını Görselleştirme

Merhaba gerekli öğe kimliklerinin verilen hello altı sütunları temsil hello ilk toofind hello giriş verisi tarafından sağlanan gibi öğeleri, ilgili. Merhaba diğer beş sütun deposu hello uygunluk açısından azalan düzende hello öğesinin tahmin edilen ilgili öğeler. Örneğin, hello ilk satırda hello en uygun öğesinin 135026 135035, 132875, 135055 ve 134992 tarafından izlenen 135074 öğesidir.

**Web hizmet yayımı**

web hizmetleri tooget tahminleri olarak bu denemeler yayımlama hello her hello dört senaryo için benzer işlemidir. Burada size hello ikinci senaryo (kullanıcı verilen öneri öğeleri tooa) örnek olarak alın. İzleyebileceğiniz hello diğer üç yordamın aynısını hello.

Öneren sistem modeli olarak kaydetme hello eğitilmiş ve hello giriş verisi tooa filtreleme tek bir kullanıcı kimliği sütunu olarak istenen, Şekil 25 olduğu gibi hello deneme bağlanacağını ve web hizmeti olarak yayımlama.

![Deneme hello Restoran öneri sorununun Puanlama](./media/machine-learning-interpret-model-results/25.png)

Şekil 25. Deneme hello Restoran öneri sorununun Puanlama

Merhaba Hello web hizmetini çalıştıran şekil 26 görülüyor sonuç döndürdü. Merhaba beş önerilen Restoran kullanıcı U1048 için 134986, 135018, 134975, 135021 ve 132862 ' dir.

![Öneren sistem hizmeti örneği](./media/machine-learning-interpret-model-results/25_1.png)

![Örnek deneme sonuçları](./media/machine-learning-interpret-model-results/26.png)

Şekil 26. Web hizmeti Restoran öneri sorun sonucu

<!-- Module References -->
[assign-to-clusters]: https://msdn.microsoft.com/library/azure/eed3ee76-e8aa-46e6-907c-9ca767f5c114/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-matchbox-recommender]: https://msdn.microsoft.com/library/azure/55544522-9a10-44bd-884f-9a91a9cec2cd/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-clustering-model]: https://msdn.microsoft.com/library/azure/bb43c744-f7fa-41d0-ae67-74ae75da3ffd/
[train-matchbox-recommender]: https://msdn.microsoft.com/library/azure/fa4aa69d-2f1c-4ba4-ad5f-90ea3a515b4c/
