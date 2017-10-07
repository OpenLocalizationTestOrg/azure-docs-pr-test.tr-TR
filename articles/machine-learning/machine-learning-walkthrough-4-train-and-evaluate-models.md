---
title: "4. adım: Eğitmek ve hello Tahmine dayalı analitik modelleri değerlendirme | Microsoft Docs"
description: "4. adımını hello geliştirmek Tahmine dayalı bir çözüm izlenecek yol: eğitme, Puanlama ve Azure Machine Learning Studio'da birden fazla modeli değerlendirin."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a>Gözden geçirme adım 4: Eğitmek ve hello Tahmine dayalı analitik modelleri değerlendir
Bu konu, hello izlenecek hello dördüncü adımı içerir [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Bir Machine Learning çalışma alanı oluşturma](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Mevcut verileri yükleme](machine-learning-walkthrough-2-upload-data.md)
3. [Yeni bir deneme oluşturma](machine-learning-walkthrough-3-create-new-experiment.md)
4. **Eğitmek ve hello modelleri değerlendir**
5. [Merhaba Web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md)
6. [Merhaba Web hizmetine erişim](machine-learning-walkthrough-6-access-web-service.md)

- - -
Biri makine öğrenimi modellerini oluşturmak için Azure Machine Learning Studio'da kullanmanın yararları hello hello özelliği tootry birden fazla türde bir model tek bir deneme zamanında ve hello sonucu karşılaştırın. Bu tür bir deney sorununuzu için hello en iyi çözüm bulmanıza yardımcı olur.

Biz bu kılavuzda geliştirmekte hello denemesinde, biz modelleri iki farklı türde oluşturacak ve sonra bunların Puanlama sonuçları toodecide algoritmayı karşılaştırmak bizim son deneme toouse istiyoruz.  

Biz arasından seçim çeşitli modellerin vardır. toosee hello modelleri kullanılabilir genişletin hello **Machine Learning** hello modül paletindeki düğümünü genişletin ve ardından **modeli Başlat** ve hello düğümü altındaki. Bu deneme Hello amaçları doğrultusunda, biz hello seçersiniz [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] (SVM) ve hello [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] modüller.    

> [!TIP]
> Machine Learning algoritmayı en iyi karar tooget Yardım uygun hello belirli sorun toosolve çalıştığınız için bkz: [nasıl Microsoft Azure Machine Learning için toochoose algoritmaları](machine-learning-algorithm-choice.md).
> 
> 

## <a name="train-hello-models"></a>Merhaba modelleri eğitme

Her iki hello ekleyeceğiz [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] modülü ve [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] bu modülü denemeler yapın.

### <a name="two-class-boosted-decision-tree"></a>İki sınıflı artırılmış karar ağacı

İlk olarak, şirketinizdeki boosted hello karar ağacı modelini ayarlayın.

1. Hello bulur [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] hello modül paleti modülünde hello tuvale sürükleyin.

2. Hello bulur [Train Model] [ train-model] modülü, hello tuvale sürükleyin ve ardından hello hello çıkışına bağlayın [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree]modülü toohello sol giriş bağlantı noktası hello [Train Model] [ train-model] modülü.
   
   Merhaba [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] modülü hello genel modeli, başlatır ve [Train Model] [ train-model] eğitim verileri kullanır tootrain hello modeli. 

3. Merhaba sol hello sol çıkışına bağlayın [R betiği yürütün] [ execute-r-script] modülü toohello sağ giriş bağlantı noktası hello [Train Model] [ train-model] (biz Modülü içinde karar [adım 3](machine-learning-walkthrough-3-create-new-experiment.md) yan hello bölünmüş veri modülünün eğitim sol hello gelen bu izlenecek yol toouse hello veri).
   
   > [!TIP]
   > İki hello girdi ve hello hello çıkışları biri gerekmez [R betiği yürütün] [ execute-r-script] biz bunları eklenmemiş bırakabilirsiniz, bu nedenle bu deneme için modülü. 
   > 
   > 

Bu kısmı hello denemeyi şimdi şuna benzer:  

![Bir model eğitimi][1]

Tootell hello ihtiyacımız artık [Train Model] [ train-model] modülü hello model toopredict hello kredi riski değeri istiyoruz.

1. Select hello [Train Model] [ train-model] modülü. Merhaba, **özellikleri** bölmesinde tıklatın **başlatma Sütun seçiciyi**.

2. Merhaba, **tek bir sütun seçin** iletişim kutusunda, türü "Kredi riski" Merhaba arama alanında altında **kullanılabilir sütunlar**, aşağıda "Kredi riski"'ı seçin ve hello sağ ok düğmesine tıklayın ( **>** ) toomove "çok kredi riski"**seçili sütun**. 

    ![Merhaba Train Model modülü için Hello kredi riski sütun seçin][0]

3. Merhaba tıklatın **Tamam** onay işareti.

### <a name="two-class-support-vector-machine"></a>Çift Sınıflı Destek Vektör Makinesi

Ardından, hello SVM modelini ayarlayın.  

Öncelikle, SVM hakkında biraz açıklama. Artırılmış karar ağaçları iyi herhangi bir türde özellikleri ile çalışmaz. Doğrusal bir sınıflandırıcı Hello SVM modülü oluşturur olduğundan, tüm sayısal özellikleri hello olduğunda ancak ürettiği hello modeli hello en iyi test hatalı aynı ölçek. tüm sayısal tooconvert özellikleri toohello aynı ölçeklendirme, bir "Tanh" dönüştürmesi kullanıyoruz (Merhaba ile [normalleştirin veri] [ normalize-data] Modülü). Bu bizim numaraları hello [0,1] aralığına dönüştürür. dize özellikleri toocategorical Özellikler'i ve ardından toobinary 0/1 özellikler Hello SVM modülü dönüştürür, biz olmayan şekilde toomanually dize özellikleri dönüştürme. Ayrıca, biz tootransform hello kredi riski sütun (sütun 21) istemediğiniz - sayısal ancak bu eğitim hello değeri hello modeli toopredict tooleave ihtiyacımız şekilde, tek başına.  

Merhaba SVM modeli yukarı tooset hello aşağıdaki:

1. Hello bulur [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] hello modül paleti modülünde hello tuvale sürükleyin.

2. Sağ hello [Train Model] [ train-model] modülü, select **kopyalama**ve ardından hello tuvale sağ tıklatın ve seçin **Yapıştır**. Merhaba hello kopyasını [Train Model] [ train-model] modülüne sahip hello hello özgün olarak aynı sütun seçimi.

3. Merhaba Hello çıkışına bağlayın [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] modülü toohello sol giriş bağlantı noktası Merhaba, ikinci [Train Model] [ train-model] Modül.

4. Hello bulur [normalleştirin veri] [ normalize-data] modülü ve hello tuvale sürükleyin.

5. Merhaba sol hello sol çıkışına bağlayın [R betiği yürütün] [ execute-r-script] modül toohello girişi Bu modülün (bildirim hello çıkış bağlantı noktasına bir modülün başka bir modül'den bağlı toomore olabilir).

6. Merhaba çıkış bağlantı noktasına sol hello bağlanmak [normalleştirin veri] [ normalize-data] modülü toohello sağ giriş bağlantı noktası hello ikinci [Train Model] [ train-model] modülü.

Bu bizim deneme kısmı bu gibi görünmelidir:  

![Eğitim hello ikinci modeli][2]  

Şimdi hello yapılandırmak [normalleştirin veri] [ normalize-data] Modülü:

1. Tooselect hello tıklatın [normalleştirin veri] [ normalize-data] modülü. Merhaba, **özellikleri** bölmesinde, **Tanh** hello için **dönüştürme yöntemi** parametresi.

2. Tıklatın **başlatma Sütun seçiciyi**, "Hiçbir sütun" seçin **şununla Başla**seçin **INCLUDE** hello ilk açılır menüde seçin **sütun türü**ikinci açılır hello ve seçin **sayısal** içinde hello üçüncü açılır. Bu, tüm hello sayısal sütunlar (ve yalnızca sayısal) dönüştürüldüğünden belirtir.

3. Tıklatın artı (+) toohello bu satırın sağ hello - bu bırakmalar satırının oluşturur. Seçin **hariç** hello ilk açılır menüde seçin **sütun adları** ikinci açılır hello ve "Merhaba metin alanında risk kredi" girin. Bu, hello kredi riski sütuna dikkate belirtir (Bu olduğundan bu sütun sayısal ve bunu dönüştürülmüş biz bunu siz bıraksanız toodo ihtiyacımız).

4. Merhaba tıklatın **Tamam** onay işareti.  

    ![Merhaba normalleştirin veri modülü sütunlarını seçin][5]

Merhaba [normalleştirin veri] [ normalize-data] modülüdür şimdi kümesi tooperform hello kredi riski sütun dışında tüm sayısal sütunlarda Tanh dönüştürme.  

## <a name="score-and-evaluate-hello-models"></a>Puanlama ve hello modelleri değerlendir

Merhaba tarafından ayrıldı verileri test etme hello kullanırız [bölünmüş veri] [ split] modülü tooscore bizim eğitilmiş modeller. Biz, ardından daha iyi sonuçlar oluşturulan hello iki modelleri toosee hello sonuçlarını karşılaştırabilirsiniz.  

### <a name="add-hello-score-model-modules"></a>Merhaba Score Model modülleri ekleme

1. Hello bulur [Score Model] [ score-model] modülü ve hello tuvale sürükleyin.

2. Merhaba bağlanmak [Train Model] [ train-model] toohello bağlandı Modülü [iki-Class Boosted karar ağacı] [ two-class-boosted-decision-tree] modülü toohello sol giriş başlangıç bağlantı noktası [Score Model] [ score-model] modülü.

3. Merhaba sağ bağlanmak [R betiği yürütün] [ execute-r-script] Modülü (test verilerimizi) toohello sağ giriş bağlantı noktası hello [Score Model] [ score-model] modülü.

    ![Score Model modülünün bağlı][6]
   
   Merhaba [Score Model] [ score-model] modülü şimdi veri hello modeli aracılığıyla çalıştırmak, test hello hello kredi bilgileri alın ve karşılaştırma hello tahminleri hello modeli oluşturur hello gerçek ile kredi riski verileri test etme hello sütun.

4. Kopyalama ve yapıştırma hello [Score Model] [ score-model] modülü toocreate ikinci bir kopyası.

5. Merhaba SVM modeli Hello çıkışına bağlayın (diğer bir deyişle, başlangıç bağlantı noktası hello çıktı [Train Model] [ train-model] toohello bağlandı Modülü [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] Modülü) toohello giriş bağlantı noktası hello ikinci [Score Model] [ score-model] modülü.

6. Merhaba SVM modeli için aynı dönüşüm toohello test verileri toohello eğitim verilerini yaptığımız gibi hello toodo sahip. Merhaba şekilde kopyalayıp [normalleştirin veri] [ normalize-data] modülü toocreate ikinci kopya ve toohello sağ bağlamak [R betiği yürütün] [ execute-r-script] modülü.

7. Merhaba sol hello çıktısını ikinci bağlanmak [normalleştirin veri] [ normalize-data] modülü toohello sağ giriş bağlantı noktası hello ikinci [Score Model] [ score-model] Modül.

    ![Bağlı her iki Score Model modülleri][7]

### <a name="add-hello-evaluate-model-module"></a>Merhaba Evaluate Model Modül Ekle

tooevaluate iki Puanlama sonuçları hello ve bunları karşılaştırır, kullandığımız bir [Evaluate Model] [ evaluate-model] modülü.  

1. Hello bulur [Evaluate Model] [ evaluate-model] modülü ve hello tuvale sürükleyin.

2. Merhaba Hello çıkış bağlantı noktasına bağlanmak [Score Model] [ score-model] hello ile ilişkilendirilmiş modül boosted karar ağacı modeli sol toohello giriş hello bağlantı noktası [Evaluate Model] [ evaluate-model] modülü.

3. Merhaba diğer bağlanmak [Score Model] [ score-model] modülü toohello sağ giriş bağlantı noktası.  

    ![Modeli değerlendirin bağlı Modülü][8]

### <a name="run-hello-experiment-and-check-hello-results"></a>Merhaba denemeyi çalıştırın ve hello sonuçlarını kontrol edin

toorun Merhaba deneme, hello tıklatın **çalıştırmak** hello tuvale aşağıdaki düğmesine. Birkaç dakika sürebilir. Dönen göstergesi her modül çalışıp çalışmadığını ve ardından hello modülünün tamamladığında yeşil bir onay işareti gösterir gösterir. Tüm hello modülleri bir onay işareti varsa, hello deneme çalışması sona erdi.

Merhaba deneme bu gibi görünmelidir:  

![Her iki modeli değerlendirme][3]

toocheck hello sonuçları hello hello çıkış bağlantı noktasına tıklayın [Evaluate Model] [ evaluate-model] modülü ve select **Görselleştir**.  

Merhaba [Evaluate Model] [ evaluate-model] modülü eğriler ve toocompare hello hello iki puanlanmış modelleri sonuçlarını izin ölçümleri çifti oluşturur. Alıcı işleci karakteristiğini (ROC) Eğriler, duyarlık/geri çağırma Eğriler ya da yükseltme Eğriler olarak hello sonuçlarını görüntüleyebilirsiniz. Görüntülenen ek verileri karışıklığı matrisi, hello eğri (AUC) hello alanında toplu değerlerini ve diğer ölçümleri içerir. Taşıma hello kaydırıcı tarafından sola veya sağa hello eşik değerini değiştirin ve ölçümleri hello kümesi nasıl etkilediği bakın.  

toohello hello grafiğin sağına tıklayın **veri kümesi belirtmek** veya **dataset toocompare skoru** toohighlight hello ilişkili eğrisi ve toodisplay hello ilişkili aşağıdaki ölçümleri. Merhaba Eğriler Hello göstergede "veri kümesi belirtmek" hello, giriş bağlantı noktası sol toohello karşılık gelen [Evaluate Model] [ evaluate-model] modül - Örneğimizde, bu boosted hello karar ağacı modelidir. "Veri kümesi toocompare skoru" toohello sağ giriş bağlantı noktasını - hello SVM modeli Bu örnekte karşılık gelir. Bu etiketler birine tıkladığınızda, bu model için hello eğri vurgulanır ve hello grafiği aşağıdaki gösterildiği gibi hello karşılık gelen ölçümleri görüntülenir.  

![Modelleri için ROC Eğriler][4]

Bu değerleri inceleyerek, aradığınız sonuçları hello en yakın toogiving modeldir karar verebilirsiniz. Geri dönün ve parametre değerlerini hello farklı modellerde değiştirerek denemenizi üzerinde yineleme. 

Merhaba Bilim ve bu sonuçları yorumlayarak ve hello modeli performans ayarlama resim, bu kılavuzda dış hello kapsamını olur. Ek Yardım için aşağıdaki makaleler hello okuyun:
- [Nasıl tooevaluate model Azure Machine Learning performansı](machine-learning-evaluate-model-performance.md)
- [Azure Machine Learning, algoritmaları parametreleri toooptimize seçin](machine-learning-algorithm-parameters-optimize.md)
- [Azure Machine Learning modeli sonuçlarında yorumlama](machine-learning-interpret-model-results.md)

> [!TIP]
> Merhaba deneme bu yineleme kaydını her çalıştırdığınızda hello çalıştırma geçmişi korunur. Bu yinelemeleri görüntülemek ve tıklayarak tooany, geri dönüp **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE** hello tuvale aşağıda. De tıklayabilirsiniz **önceki Çalıştır** hello içinde **özellikleri** hemen önceki bölmesinde tooreturn toohello yineleme hello bir açık olması.
> 
> Tıklayarak denemenizin herhangi bir yinelemesini kopyasını yapabilirsiniz **SAVE AS** hello tuvale aşağıda. 
> Merhaba deneme kullanmak **Özet** ve **açıklama** özellikleri tookeep, deneme yinelemelerini çalıştınız kaydını.
> 
> Daha fazla ayrıntı için bkz: [Azure Machine Learning Studio'da deneme yinelemelerini yönetme](machine-learning-manage-experiment-iterations.md).  
> 
> 

- - -
**Sonraki: [hello web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md)**

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
