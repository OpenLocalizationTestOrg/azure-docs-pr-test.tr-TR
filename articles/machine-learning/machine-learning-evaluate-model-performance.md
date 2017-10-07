---
title: Machine Learning aaaEvaluate modeli performans | Microsoft Docs
description: "Nasıl tooevaluate model Azure Machine Learning performans açıklanmaktadır."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 5dc5348a-4488-4536-99eb-ff105be9b160
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bradsev;garye
ms.openlocfilehash: 03477368758dbb13aa6f54c5d27fb215615d1f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooevaluate-model-performance-in-azure-machine-learning"></a>Nasıl tooevaluate model Azure Machine Learning performansı
Bu makalede nasıl tooevaluate Azure Machine Learning Studio'da bir model performansını hello ve bu görev için hello ölçümleri kullanılabilir kısa bir açıklamasını sağlar gösterilmektedir. Üç yaygın denetimli öğrenme senaryo sunulur: 

* regresyon
* ikili sınıflandırma 
* çok sınıflı sınıflandırma

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Bir model Hello performansını değerlendirmek hello çekirdek hello veri bilimi işlemi aşamada biridir. (Tahminleri) Puanlama nasıl başarılı hello gösteren bir veri kümesi eğitilen modeli tarafından kaldırıldı. 

Azure Machine Learning modeli değerlendirme iki modülleri öğrenme kendi ana makine aracılığıyla destekler: [Evaluate Model] [ evaluate-model] ve [çapraz doğrulama modeli][cross-validate-model]. Bu modüller nasıl machine learning ve istatistikleri yaygın olarak kullanılan ölçümleri sayısı bakımından modelinizi gerçekleştirir toosee izin verin.

## <a name="evaluation-vs-cross-validation"></a>Değerlendirme vs. Çapraz doğrulama
Değerlendirme ve çapraz doğrulama standart yolları toomeasure hello performans modelinizin markalarıdır. Her ikisi de inceleme veya bunlar başka modellerinin karşı karşılaştırmak değerlendirme ölçümleri oluşturur.

[Modeli değerlendirin] [ evaluate-model] giriş (veya 2 başka modellerinin toocompare hello performans istediğinizi 2 içinde çalışması) puanlanmış veri kümesi bekliyor. Bu hello kullanarak modelinizi tootrain gerektiği anlamına gelir [Train Model] [ train-model] modülü ve yapma tahminleri hello kullanarak bazı veri kümesi üzerinde [Score Model] [ score-model] hello sonuçları değerlendirmeden önce modülü. Merhaba değerlendirme etiketleri/olasılıklar tümü hello tarafından çıktı hello true etiketleri birlikte skoru hello dayanır [Score Model] [ score-model] modülü.

Alternatif olarak, çapraz doğrulama tooperform tren puanı değerlendirme işlemleri (10 Katlama) otomatik olarak farklı alt kümelerini hello giriş verilerinin çeşitli kullanabilirsiniz. Merhaba giriş verisi burada bir test için ayrılmıştır ve eğitim için diğer 9 hello 10 parçalara bölünür. Bu işlem 10 kez yinelenir ve hello değerlendirme ölçümleri ortalaması alınır. Bu, bir model toonew veri kümeleri ne kadar iyi generalize belirlemede yardımcı olur. Merhaba [çapraz doğrulama modeli] [ cross-validate-model] modülü eğitimsiz modelinde alır ve bazı veri kümesi ve çıkışları hello değerlendirme sonuçlarını her bir hello 10 Katlama etiketli, ayrıca toohello sonuçları ortalaması.

Aşağıdaki bölümlerde hello biz oluşturacak basit regresyon ve sınıflandırma modelleri ve her iki hello kullanarak kendi performansını değerlendirmek [Evaluate Model] [ evaluate-model] ve hello [çapraz doğrulama Model] [ cross-validate-model] modüller.

## <a name="evaluating-a-regression-model"></a>Bir regresyon modeli değerlendirme
Biz toopredict boyutları, beygir gücü, altyapısı belirtimlerin vb. gibi bazı özellikleri kullanılarak bir otomobilin fiyatını istediğinizi varsayalım. Bu tipik regresyon sorunudur, burada, hedef değişkeni hello (*fiyat*) sürekli sayısal bir değerdir. Size hello özellik değerleri belirli bir araba tahmin etmek, bu otomobil fiyatını hello Basit doğrusal regresyon modelini uygun olamaz. Bu regresyon modeli kullanılan tooscore hello biz eğitilmiş aynı veri kümesi. Tüm hello otomobiller için tahmin edilen fiyatları sahip hello sonra ne kadar hello tahminleri hello gerçek fiyatlar ortalama sapma adresindeki bakarak biz hello modeli hello performansını değerlendirebilirsiniz. tooillustrate bunu hello kullanırız *otomobil fiyat verileri (ham) dataset* hello bulunan **kaydedilen veri kümeleri** Azure Machine Learning Studio bölümünde.

### <a name="creating-hello-experiment"></a>Merhaba deneme oluşturma
Azure Machine Learning Studio'daki modüller tooyour çalışma alanı aşağıdaki hello ekleyin:

* Otomobil fiyat verileri (ham)
* [Doğrusal regresyon][linear-regression]
* [Train Model][train-model]
* [Score Model][score-model]
* [Modeli değerlendirin][evaluate-model]

Aşağıda Şekil 1 ve hello kümesi hello Etiket sütununda gösterildiği gibi Hello bağlantı noktalarını bağlamak [Train Model] [ train-model] modülü çok*fiyat*.

![Bir regresyon modeli değerlendirme](media/machine-learning-evaluate-model-performance/1.png)

Şekil 1 '. Bir regresyon modeli değerlendiriliyor.

### <a name="inspecting-hello-evaluation-results"></a>Merhaba değerlendirme sonuçlarını İnceleme
Çalışan hello deneme hello çıkış bağlantı noktasına hello üzerinde tıklatabilirsiniz [Evaluate Model] [ evaluate-model] modülü ve select *Görselleştir* toosee hello değerlendirme sonuçları. regresyon modelleri için kullanılabilir değerlendirme ölçümleri hello: *ortalama mutlak hata*, *kök ortalama mutlak hata*, *göreli mutlak hata*,  *Göreli karesi alınmış hata*ve hello *Coefficient of Determination*.

"error" Buraya temsil eden hello birbirinden hello terim hello tahmin edilen değer ile Merhaba true değeri. Merhaba mutlak bir değer veya hello bu farkı kare genellikle hesaplanan toocapture hello tüm örneklerde, hata hello hello birbirinden olarak büyüklüğünü tahmin ve true değeri bazı durumlarda negatif toplam markalarıdır. Merhaba hata ölçümleri hello Tahmine dayalı bir regresyon modeli hello ortalama kendi tahminleri hello true değerlerinden sapmasını bakımından performansını ölçme. Alt hata değerlerini hello modeli tahminleri yaparken daha doğru anlamına gelir. Bir genel hata ölçümü modeli hello 0 anlamına gelir hello verilere mükemmel uyduğunu.

Merhaba katsayısı olarak da bilinen R olan kare, ayrıca ne kadar iyi hello modeli hello veri uygun ölçü standart bir yoludur. Merhaba modeli tarafından açıklanan değişim hello oranını olarak yorumlanacak. Yüksek bir oranda bu durumda, daha iyi 1 burada bir mükemmel gösterir.

![Doğrusal regresyon değerlendirme ölçümleri](media/machine-learning-evaluate-model-performance/2.png)

Şekil 2. Doğrusal regresyon değerlendirme ölçümleri.

### <a name="using-cross-validation"></a>Doğrulama kullanma
Daha önce belirtildiği gibi yinelenen eğitim gerçekleştirebilirsiniz, Puanlama ve kullanılarak otomatik olarak değerlendirmeleri hello [çapraz doğrulama modeli] [ cross-validate-model] modülü. Tüm yapmanız gereken bu durumda olan bir veri kümesi, bir eğitimsiz modeli ve [çapraz doğrulama modeli] [ cross-validate-model] Modülü (aşağıdaki şekilde bakın). Tooset hello etiket sütunu çok gerektiğini unutmayın*fiyat* hello içinde [çapraz doğrulama modeli] [ cross-validate-model] modülünün özellikleri.

![Çapraz-doğrularken bir regresyon modeli](media/machine-learning-evaluate-model-performance/3.png)

Şekil 3 '. Çapraz-bir regresyon modeli doğrulanıyor.

Çalışan hello deneme hello sağ çıkış bağlantı noktasına hello üzerinde tıklayarak hello değerlendirme sonuçlarını inceleyebilirsiniz [çapraz doğrulama modeli] [ cross-validate-model] modülü. Bu her bir yineleme (Katlama) için hello ölçümleri ayrıntılı görünümünü sağlar ve her hello ölçümleri (Şekil 4) sonuçlarını hello ortalaması.

![Çapraz doğrulama sonuçlarını bir regresyon modeli](media/machine-learning-evaluate-model-performance/4.png)

Şekil 4 '. Çapraz doğrulama sonuçlarını bir regresyon modeli.

## <a name="evaluating-a-binary-classification-model"></a>Bir ikili sınıflandırma modeli değerlendirme
Örneğin yalnızca iki olası sonucunu bir ikili sınıflandırma senaryosunda hello hedef değişkeni vardır: {0, 1} veya {yanlış, doğru}, {negatif, pozitif}. Bir veri kümesi yetişkin çalışanların bazı verilmiştir varsayın demografik ve İstihdam değişkenleri ve toopredict hello gelir düzeyi, bir ikili değişken hello değerlerle sorulur {"< 50 K =", "> 50K"}. Diğer bir deyişle, küçük veya buna eşit olmak hello çalışanlar hello negatif sınıfı temsil eder yıl ve hello sınıfı temsil eder, diğer tüm çalışanlar pozitif başına too50K. Merhaba regresyon senaryo olduğu gibi biz bir modeli eğitmek, bazı veriler Puanlama ve hello sonuçları değerlendirin. Burada ana fark Hello hello Azure Machine Learning hesaplar ölçümleri ve çıkışları seçimdir. tooillustrate hello gelir düzeyi tahmin senaryosu, kullanacağız hello [yetişkin](http://archive.ics.uci.edu/ml/datasets/Adult) dataset toocreate bir Azure Machine Learning denemek ve iki sınıflı Lojistik regresyon modeli, yaygın olarak kullanılan bir ikili hello performansını değerlendirmek Sınıflandırıcı.

### <a name="creating-hello-experiment"></a>Merhaba deneme oluşturma
Azure Machine Learning Studio'daki modüller tooyour çalışma alanı aşağıdaki hello ekleyin:

* Yetişkin Census gelir ikili sınıflandırma veri kümesi
* [İki sınıflı Lojistik regresyon][two-class-logistic-regression]
* [Train Model][train-model]
* [Score Model][score-model]
* [Modeli değerlendirin][evaluate-model]

Aşağıda Şekil 5 ve hello kümesi hello Etiket sütununda gösterildiği gibi Hello bağlantı noktalarını bağlamak [Train Model] [ train-model] modülü çok*gelir*.

![Bir ikili sınıflandırma modeli değerlendirme](media/machine-learning-evaluate-model-performance/5.png)

Şekil 5. Bir ikili sınıflandırma modeli değerlendiriliyor.

### <a name="inspecting-hello-evaluation-results"></a>Merhaba değerlendirme sonuçlarını İnceleme
Çalışan hello deneme hello çıkış bağlantı noktasına hello üzerinde tıklatabilirsiniz [Evaluate Model] [ evaluate-model] modülü ve select *Görselleştir* toosee hello değerlendirme sonuçlarını (Şekil 7). ikili sınıflandırma modelleri için kullanılabilir değerlendirme ölçümleri hello: *doğruluğu*, *duyarlık*, *geri çağırma*, *F1 puan*, ve *AUC*. Ayrıca, doğru pozitif sonuç, false negatif, hatalı pozitif sonuç ve doğru negatif hello sayısını gösteren bir karışıklığı matris hello modülü çıkarır yanı *ROC*, *duyarlık/geri çağırma*ve *Yükselt* Eğriler.

Doğruluk yalnızca hello oranı doğru sınıflandırılmış örneklerinin ' dir. Bu genellikle, bir sınıflandırıcı değerlendirirken bakmak hello ilk ölçümüdür. Ancak, hello test verileri olduğunda (burada hello örnekleri çoğu hello sınıfların tooone ait) dengesini ya da daha fazla ilgilendiğiniz performans hello hello sınıfların ya da bir doğruluk gerçekten sınıflandırıcı hello verimliliğini yakalamaz. Merhaba örneklerinin % 99 küçük veya buna eşit kazanma kişilerin burada temsil eden bazı veriler üzerinde test ettiğiniz Hello gelir level sınıflandırma senaryoda varsayın yıllık too50K. Merhaba sınıfı tahmin ederek çalışmasını olası tooachieve 0.99 doğruluğu olan "< 50 K =" tüm örnekleri için. Merhaba sınıflandırıcı bu durumda genel bir iyi işi yapmanın toobe görünür, ancak gerçekte tooclassify herhangi hello high-income kişiler (Merhaba % 1) doğru başarısız olur.

Bu nedenle, hello değerlendirme daha belirli yönlerini Yakalama yardımcı toocompute ek ölçümler değil. Bu tür ölçümleri Hello ayrıntılarını geçmeden önce bu önemli toounderstand hello karışıklığı matris ikili sınıflandırma değerlendirme olur. Merhaba Eğitim kümesi etiketleri yalnızca 2 olası değerler üzerinde hangi biz genellikle sürebilir hello sınıfı tooas olumlu veya olumsuz bakın. bir sınıflandırıcı doğru şekilde tahmin hello pozitif ve negatif örnekleri true pozitif sonuç (TP) ve doğru negatif (TN) adlandırılır. Benzer şekilde, yanlış sınıflandırılmış hello örnekleri hatalı pozitif sonuç (FP) ve false negatif (FN) adı verilir. Merhaba karışıklığı matris yalnızca hello bu kategorilerin her biri 4 altında kalan örneklerinin sayısını gösteren bir tablo ' dir. Azure Machine Learning hello iki sınıf hello kümesindeki hello pozitif sınıfı olduğu otomatik olarak karar verir. Merhaba sınıfı etiketleri Boole veya tamsayı olan ve ardından hello 'true' veya '1' etiketli örnekleri hello pozitif sınıfı atanır. Merhaba etiketleri dizeleri varsa hello gelir kümesinin hello durumda olduğu gibi hello etiketleri alfabetik olarak sıralanır ve hello ikinci düzey hello pozitif sınıfı olsa hello ilk düzeyi toobe hello negatif sınıfı seçilir.

![İkili sınıflandırma karışıklığı Matrisi](media/machine-learning-evaluate-model-performance/6a.png)

Şekil 6. İkili sınıflandırma karışıklığı matrisi.

Toohello gelir sınıflandırma sorunu geri dönerseniz, kullanılan hello sınıflandırıcı hello performansını iyileştirmemize yardımcı birkaç değerlendirme soruları anlamak tooask istersiniz. Çok doğal bir soru: ' tahmin edilen toobe getirisi kim hello hello kişiler dışında model > 50 kaç doğru şekilde sınıflandırıldığını K (TP + FP) (TP)?' Hello bakarak bu soruyu yanıtlanması **duyarlık** hello oranını doğru olarak sınıflandırıldığını pozitif sonuç olduğunu hello modelinin: TP/(TP+FP). Başka bir ortak Soru "tüm hello yüksek kazanç çalışanlar ile gelir dışında > 50 kaç sınıflandırıcı hello k (TP + FN) sınıflandırmak doğru (TP)". Gerçekte hello budur **geri çağırma**, veya hello true pozitif oranı: hello sınıflandırıcı TP/(TP+FN). Duyarlık geri çekme arasındaki belirgin bir denge olduğunu fark edebilirsiniz. Örneğin, görece dengeli bir veri kümesi verildiğinde, çoğunlukla pozitif örnekleri tahmin bir sınıflandırıcı sahip olabilir yüksek bir geri çağırma, ancak yerine düşük duyarlılık birçok hello negatif örneklerinin gibi çok sayıda hatalı pozitif sonuç elde edilen misclassified. Bu iki ölçümleri nasıl farklılık, bir çizim toosee tıklayabilirsiniz hello ' DUYARLIK/geri ÇAĞIRMA' hello değerlendirme sonucu çıkış sayfa eğrisindeki üzerinde (Şekil 7 parçası sol üst).

![İkili sınıflandırma değerlendirme sonuçları](media/machine-learning-evaluate-model-performance/7.png)

Şekil 7. İkili sınıflandırma değerlendirme sonuçları.

Başka bir sık kullanılan ölçüm hello ilgili **F1 puan**, hem duyarlık hem de geri çağırma dikkate alır. 2 bu ölçümleri hello harmonik olduğundan ve bu nedenle hesaplanır: F1 = 2 (x duyarlık geri çekme) / (duyarlık + geri çağırma). Merhaba F1 puanı, tek bir sayı en iyi yolu toosummarize hello hesaplanmasında olmakla birlikte her zaman iyi bir uygulama toolook hem duyarlık hem de geri çağırma birlikte toobetter anlamak sınıflandırıcı nasıl davranacağını olur.

Ayrıca, bir hello true pozitif oranı ve yanlış pozitif hızını hello hello inceleyebilirsiniz **alıcı işletim karakteristiğini (ROC)** eğri ve karşılık gelen hello **alanı altında eğri (AUC) hello** değeri. Merhaba yakın bu eğri toohello üst sol alt köşe, hello daha iyi hello sınıflandırıcı 's performans (Merhaba yanlış pozitif hızı en aza indirme sırasında bu en yüksek düzeyde hello true pozitif hızı). Çizim, Kapat toohello çapraz olan Eğriler Merhaba, olan toomake tahminleri eğilimindedir sınıflandırıcı sonucundan kapatmak toorandom tahmin.

### <a name="using-cross-validation"></a>Doğrulama kullanma
Merhaba regresyon örnekteki biz çapraz doğrulama toorepeatedly tren gerçekleştirmek, Puanlama ve farklı veri alt kümesi hello otomatik olarak değerlendirin. Benzer şekilde, biz hello kullanabilirsiniz [çapraz doğrulama modeli] [ cross-validate-model] modülü, bir eğitimsiz Lojistik regresyon modeli ve bir veri kümesi. Merhaba etiket sütunu çok ayarlanmalıdır*gelir* hello içinde [çapraz doğrulama modeli] [ cross-validate-model] modülünün özellikleri. Çalışan hello deneme ve hello sağ tıklayarak hello bağlantı noktası çıkış sonra [çapraz doğrulama modeli] [ cross-validate-model] modülü, biz görebilir hello ikili sınıflandırma ölçüm değerleri her Katlama, ayrıca toohello Ortalama ve standart sapma her. 

![Çapraz-doğrulama ikili sınıflandırma modeli](media/machine-learning-evaluate-model-performance/8.png)

Şekil 8'de. Çapraz-ikili sınıflandırma Model doğrulama.

![Bir ikili sınıflandırıcı çapraz doğrulama sonuçlarını](media/machine-learning-evaluate-model-performance/9.png)

Şekil 9. Bir ikili sınıflandırıcı çapraz doğrulama sonuçları.

## <a name="evaluating-a-multiclass-classification-model"></a>Bir çok sınıflı sınıflandırma modeli değerlendirme
Bu deneme hello popüler kullanacağız [Iris](http://archive.ics.uci.edu/ml/datasets/Iris "Iris") 3 farklı türleri (sınıflar) hello iris tesis örneklerini içeren veri kümesi. 4 özellik değerlerini (sepal uzunluğu/genişlik ve petal uzunluğu/genişlik) her örneği vardır. Biz Hello önceki denemelerde eğittiğiniz ve test edilmiş hello modelleri kullanarak aynı veri kümeleri hello. Burada, hello kullanacağız [bölünmüş veri] [ split] modülü toocreate 2 hello veri kümelerine hello üzerinde ilk olarak, eğitmek ve puanlama ve üzerinde hello değerlendirmek ikinci. Merhaba Iris dataset üzerinde hello genel olarak kullanılabilir [UCI Machine Learning deposu](http://archive.ics.uci.edu/ml/index.html)ve kullanarak indirilebilir bir [veri içeri aktarma] [ import-data] modülü.

### <a name="creating-hello-experiment"></a>Merhaba deneme oluşturma
Azure Machine Learning Studio'daki modüller tooyour çalışma alanı aşağıdaki hello ekleyin:

* [Veri alma][import-data]
* [Veya çoklu sınıflar karar orman][multiclass-decision-forest]
* [Veri bölme][split]
* [Train Model][train-model]
* [Score Model][score-model]
* [Modeli değerlendirin][evaluate-model]

Aşağıda Şekil 10'da gösterildiği gibi Hello bağlantı bağlayın.

Merhaba etiket sütun dizini hello ayarlamak [Train Model] [ train-model] modülü too5. Başlık satırı yok Hello veri kümesi gerekiyor ancak hello beşinci sütununda etiketleridir o hello sınıf biliyoruz.

Tıklatın hello üzerinde [veri içeri aktar] [ import-data] modülü ve kümesi hello *veri kaynağı* özelliği çok*Web URL'si HTTP üzerinden*ve hello *URL*  toohttp://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data.

Merhaba eğitim için kullanılan örnekleri toobe kümesi hello bölümü [bölünmüş veri] [ split] Modülü (örneğin 0,7).

![Çok sınıflı sınıflandırıcı değerlendirme](media/machine-learning-evaluate-model-performance/10.png)

Şekil 10. Çok sınıflı sınıflandırıcı değerlendirme

### <a name="inspecting-hello-evaluation-results"></a>Merhaba değerlendirme sonuçlarını İnceleme
Merhaba denemeyi çalıştırmak ve hello çıkış bağlantı noktasında tıklatın [Evaluate Model][evaluate-model]. Merhaba değerlendirme sonuçlarını karışıklığı matris hello formunda bu durumda sunulur. Merhaba matrisi hello gerçek tüm 3 sınıfları için tahmin edilen örnekleri ve gösterir.

![Çok sınıflı sınıflandırma değerlendirme sonuçları](media/machine-learning-evaluate-model-performance/11.png)

Şekil 11. Çok sınıflı sınıflandırma değerlendirme sonuçları.

### <a name="using-cross-validation"></a>Doğrulama kullanma
Daha önce belirtildiği gibi yinelenen eğitim gerçekleştirebilirsiniz, Puanlama ve kullanılarak otomatik olarak değerlendirmeleri hello [çapraz doğrulama modeli] [ cross-validate-model] modülü. Bir veri kümesi, bir eğitimsiz modeli gerekir ve bir [çapraz doğrulama modeli] [ cross-validate-model] Modülü (aşağıdaki şekilde bakın). Merhaba tooset hello etiket sütunu yeniden ihtiyacınız [çapraz doğrulama modeli] [ cross-validate-model] Modülü (5 Bu durumda sütun dizini). Çalışan hello deneme ve hello sağ tıklayarak hello bağlantı noktası çıkış sonra [çapraz doğrulama modeli][cross-validate-model], her Katlama yanı sıra için ortalama ve standart sapma hello hello ölçüm değerleri inceleyebilirsiniz. Burada görüntülenen hello hello benzer toohello hello ikili sınıflandırma durumda ele alınan olanları ölçümleridir. Ancak, genel olumlu veya olumsuz sınıfı yok olduğundan çok sınıflı sınıflandırmasında bilgi işlem hello true pozitif/negatif ve yanlış pozitif/negatif bir sınıf başına temelinde sayım tarafından yapıldığını unutmayın. Örneğin, ne zaman bilgi işlem hello duyarlılık veya geri çağırma işlemi hello 'Iris-setosa' sınıfı, onu bu hello pozitif sınıf ve negatif olarak diğerlerini olduğu varsayılır.

![Çapraz-doğrulama çok sınıflı sınıflandırma modeli](media/machine-learning-evaluate-model-performance/12.png)

Şekil 12. Çapraz-çok sınıflı sınıflandırma Model doğrulama.

![Çapraz doğrulama sonuçlarını çok sınıflı sınıflandırma modeli](media/machine-learning-evaluate-model-performance/13.png)

Şekil 13. Çapraz doğrulama sonuçlarını çok sınıflı sınıflandırma modeli.

<!-- Module References -->
[cross-validate-model]: https://msdn.microsoft.com/library/azure/75fb875d-6b86-4d46-8bcc-74261ade5826/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[multiclass-decision-forest]: https://msdn.microsoft.com/library/azure/5e70108d-2e44-45d9-86e8-94f37c68fe86/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-logistic-regression]: https://msdn.microsoft.com/library/azure/b0fd7660-eeed-43c5-9487-20d9cc79ed5d/

