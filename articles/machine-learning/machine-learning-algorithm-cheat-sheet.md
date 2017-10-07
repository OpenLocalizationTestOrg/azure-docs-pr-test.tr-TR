---
title: "aaaMachine algoritması bilgi sayfası öğrenme | Microsoft Docs"
description: "Bir yazdırılabilir makine öğrenimi algoritması bilgi sayfası Azure Machine Learning Studio'da Tahmine dayalı modeliniz için hello sağ algoritma seçmenize yardımcı olur."
keywords: "Makine öğrenme algoritmasını algoritması bilgi sayfası, kopya sayfası"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e1dc31ec-1acb-463f-ba77-de565d4ddf4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: garye
ms.openlocfilehash: 2bedd77bfc65128a90c6128743016415dd8609d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-algorithm-cheat-sheet-for-microsoft-azure-machine-learning-studio"></a>Microsoft Azure Machine Learning Studio için machine learning algoritması kopya sayfası
Merhaba **Microsoft Azure Machine Learning algoritmasını sayfası kopya** hello sağ algoritması için Tahmine dayalı bir analiz modeli seçmenize yardımcı olur.

[Azure Machine Learning Studio](https://studio.azureml.net/) hello algoritmalarından büyük kitaplığı sahip ***regresyon***, ***sınıflandırma***, ***Kümeleme***ve ***anomali algılama*** aileleri. Her tasarlanmış tooaddress farklı türde bir machine learning sorun içerir.

## <a name="download-machine-learning-algorithm-cheat-sheet"></a>İndirin: Makine öğrenimi algoritması bilgi sayfası
**Burada Hello kopya sayfası indirin: [makine öğrenme algoritmasını kopya sayfası (11 x 17 inç)](http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet-v6.pdf)**

![Makine öğrenimi algoritması bilgi sayfası: öğrenin nasıl toochoose bir makine öğrenimi algoritması.][cheat-sheet]

[cheat-sheet]: ./media/machine-learning-algorithm-cheat-sheet/machine-learning-algorithm-cheat-sheet-small_v_0_6-01.png

Karşıdan yükleyip elinizin altında ve bir algoritma seçme get Yardım tabloid boyutu tookeep hello makine öğrenme algoritmasını kopya sayfası yazdırın.

> [!NOTE]
> Merhaba makalesine bakın [nasıl Microsoft Azure Machine Learning için toochoose algoritmaları](machine-learning-algorithm-choice.md) ayrıntılı kılavuz toousing için bu kopya sayfası.
> 
> 

## <a name="more-help-with-algorithms"></a>Daha fazla yardıma algoritmaları
* Merhaba sağ algoritması artı hello farklı türdeki machine learning algoritmaları ve bunların nasıl kullanıldığı daha derin bir irdelemesi seçmek için bu kopya sayfası kullanarak daha fazla yardım için bkz: [nasıl Microsoft Azure Machine Learningiçintoochoosealgoritmaları](machine-learning-algorithm-choice.md).
* Algoritmaları açıklar ve örnekler sağlayan bir indirilebilir bilgi grafiği için bkz: [indirilebilir bilgi grafiği: Makine öğrenme algoritmasını örneklerle temel](machine-learning-basics-infographic-with-algorithm-examples.md).
* Tüm hello makine öğrenimi algoritma Machine Learning Studio'da kullanılabilen kategoriye göre bir listesi için bkz: [modeli Başlat] [ initialize-model] hello Machine Learning Studio algoritması ve modülü Yardımı'nda.
* Bir tam alfabetik listesi algoritmaları ve Machine Learning Studio'daki modüller için bkz: [Machine Learning Studio modülleri A-Z listesi] [ a-z-list] Machine Learning Studio algoritması ve modülü Yardımı'nda.
* Machine Learning Studio'nun hello özelliklerine genel bakış sağlayan bir diyagram toodownload ve yazdırma bkz [Azure Machine Learning Studio işlevlerine genel bakış diyagramı](machine-learning-studio-overview-diagram.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="notes-and-terminology-definitions-for-hello-machine-learning-algorithm-cheat-sheet"></a>Notlar ve terim tanımları hello makine öğrenme algoritmasının kopya sayfası

* Bu algoritması bilgi sayfası sunulan hello yaklaşık kuralları-in-Flash önerilerdir. Bazı Bükülü ve bazı flagrantly ihlal edildi. Bu, hedeflenen toosuggest bir başlangıç noktası olur. Afraid toorun head-to-head rekabet verileriniz üzerinde birkaç algoritmaları arasında çekinmeyin. Hello ilkeleri her algoritmasının anlama ve verilerinizi oluşturulan hello sistem anlamak için sadece hiçbir yedek yoktur.

* Her makine öğrenme algoritmasını kendi stilde veya *Endüktif sapması*. Belirli bir sorun için çeşitli algoritmalar uygun olabilir ve bir algoritma diğerlerinden daha iyi bir uyum olabilir. Ancak her zaman hello en uygun olan olası tooknow önceden değil. Bu gibi durumlarda birden fazla algoritmaları hello kopya sayfası birlikte listelenir. Uygun bir strateji tootry bir algoritma olabilir ve diğerleri hello hello sonuçları henüz tatmin edici, değilse deneyin. Merhaba bir örnek şudur [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com/) birkaç algoritmaları hello karşı çalışır bir deneme sonuçları verilere ve karşılaştırır hello: [çok sınıfı sınıflandırıcı karşılaştırın: Harf tanıma ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

* Machine learning üç ana kategoriye ayrılır: **denetimli öğrenme**, **Denetimsiz öğrenme**, ve **öğrenmeyi öğrenme**.

  * İçinde **denetimli öğrenme**, her veri noktası etiketli ya da bir kategori veya ilgi alanı değeri ile ilişkilendirilmiş.  Kategorik bir etiket örneği bir görüntü olarak 'Kat' veya 'köpek' atama.  Merhaba satış fiyatı kullanılan car ile ilişkili değer etiketi örnektir. Merhaba denetimli öğrenme toostudy hedefidir çoğu bu gibi örnekler ve toobe mümkün toomake tahminleri gelecekteki veri noktaları hakkında etiketli. Örneğin, yeni fotoğraflar hello hayvan veya doğru satış fiyatları tooother atama araba kullanılan doğru ile tanımlama. Bu makine öğrenme popüler ve kullanışlı bir türde değil. Learning algoritmaları dışında tüm Azure Machine Learning hello modülleri denetimli [K-ortalamaları Kümeleme][k-means-clustering].

  * İçinde **Denetimsiz öğrenme**, veri noktalarına sahip kendileriyle ilişkilendirilmiş etiket yok. Bunun yerine, bir Denetimsiz öğrenme algoritmasını amacı hello tooorganize hello bazı yolu veya toodescribe yapısını verilerdir. Bu K-ortalamaları yaptığı gibi kümeler halinde gruplandırmak veya basit görünmesi karmaşık veri arayan farklı yöntemler bulma anlamına gelebilir.

  * İçinde **öğrenmeyi öğrenme**, hello algoritması yanıt tooeach veri noktasında bir eylem toochoose alır. Burada hello zaman içinde bir noktada sensör okumaları kümesi, veri noktası ve hello algoritması hello robot'ın bir sonraki eylem seçmelisiniz robotics, ortak bir yaklaşımdır. Aynı zamanda bir doğal olan nesnelerin interneti uygulamalar için uygun. Merhaba öğrenme algoritmasını ayrıca bir kısa ne kadar iyi hello karar belirten süresi daha sonra bir ödül sinyali alır. Bunu temel alarak, sipariş tooachieve hello yüksek ödül kendi stratejinize hello algoritması değiştirir. Şu anda Azure ML algoritması modülleri öğrenme hiçbir öğrenmeyi vardır.

* **Bayesian yöntemleri** istatistiksel olarak bağımsız veri noktaları hello olduğu varsayımını yaparsınız. Bir veri noktası Modellenmemiþ sonuçlarındaki hello Bunun anlamı başkalarıyla uncorrelated, diğer bir deyişle, bu tahmin edilemez. Örneğin, kaydedilen hello veri hello hello sonraki Yeraltı treni Eğitimi, günde bir uzaklıkta alınan iki ölçümlere gelene kadar dakika sayısını ise istatistiksel olarak bağımsız olur. Ancak, bir dakika parçalayın alınan iki ölçümlere istatistiksel olarak bağımsız olmayan - hello bir hello diğer hello değerini yüksek oranda Tahmine dayalı bir değerdir.

* **Boosted karar ağacı regresyon** özelliği çakışma veya özellikler arasındaki etkileşimi avantajlarından yararlanır. Belirtilen tüm veri noktası deyişle, bir özellik değerini hello başka bir hello değerini biraz Tahmine dayalı. Örneğin, günlük yüksek/düşük sıcaklık verilerde hello düşük sıcaklık hello gün için bilerek toomake makul tahmin hello yüksek sağlar. Merhaba iki özelliklerinde içerdiği hello bilgi biraz gereksizdir.

* İkiden fazla kategoriye veri sınıflandırma yapılabilir kendiliğinden çok sınıfı sınıflandırıcı kullanarak veya iki sınıflı sınıflandırıcı bir dizi birleştiren bir **ensemble**. Merhaba ensemble yaklaşım her sınıf için ayrı bir iki sınıflı sınıflandırıcı yoktur - her biri iki kategoride hello veri ayırır: "" ve "değil Bu sınıf." Ardından bu sınıflandırıcı hello doğru hello veri noktası atamada oy verin. Bu hello işletimsel arkasında ilkesidir [veya bir vs tüm çoklu sınıflar][one-vs-all-multiclass].

* Lojistik regresyon ve hello Bayes noktası makinesi dahil olmak üzere çeşitli yöntemler varsayın **doğrusal sınıfı sınırları**. Diğer bir deyişle, bunlar bu hello varsayın sınırlarıdır sınıflar arasındaki yaklaşık düz çizgiler (veya hyperplanes içinde hello daha genel durumda). Bu bir özellik görülür hello verilerin, ancak bunu tooseparate çalıştınız sonra kadar bilmiyorsanız genellikle önceden görselleştirme tarafından öğrenilebilecek bir şeydir. Merhaba sınıfı sınırları çok düzensiz bakarsanız, karar ağaçları ile takılıyor, ormanları karar, vektör makineleri veya sinir ağları destekler.

* Sinir ağları kullanılabilir kategorik değişkenlerle oluşturarak bir **kukla değişkeni** her kategori için too1 hello kategori geçerli olduğu, 0 nerede değil durumlarda ayarlama.


<!-- This is how you can embed a link in an image in HTML. Don't know how toodo this in markdown.
<a href="http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet.pdf">
<img src="C:\Users\garye\azure-docs-pr\articles\media\machine-learning-algorithm-cheat-sheet\cheat-sheet-small.png">
</a>
-->

<!-- Module References -->
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx
[initialize-model]: https://msdn.microsoft.com/library/azure/0c67013c-bfbc-428b-87f3-f552d8dd41f6/
[k-means-clustering]: https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/
[one-vs-all-multiclass]: https://msdn.microsoft.com/library/azure/7191efae-b4b1-4d03-a6f8-7205f87be664/
