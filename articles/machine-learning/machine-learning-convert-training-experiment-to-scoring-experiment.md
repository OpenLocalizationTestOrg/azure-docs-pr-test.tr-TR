---
title: "aaaHow tooprepare modelinizi Azure Machine Learning Studio'daki dağıtımı için | Microsoft Docs"
description: "Tooprepare eğitilen modelinizi bir Web dağıtımı için hizmet nasıl dönüştürerek Machine Learning Studio'da eğitim tooa Tahmine dayalı denemeye denemeler yapın."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: eb943c45-541a-401d-844a-c3337de82da6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: garye
ms.openlocfilehash: d25bc68be63679a803bfc24a9e29e009a9263f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprepare-your-model-for-deployment-in-azure-machine-learning-studio"></a>Nasıl tooprepare modelinizi Azure Machine Learning Studio'daki dağıtımı için

Model ve bir Azure web hizmeti olarak dağıtarak faaliyete toodevelop Tahmine dayalı bir analiz gereken araçları hello azure Machine Learning Studio sağlar.

toodo bunu Studio toocreate adlı bir denemeyi - kullandığınız bir *eğitim denemenizi* - burada eğitme, Puanlama ve modelinizi Düzenle. Memnun kaldıktan sonra modeli hazır toodeploy eğitim deneme tooa dönüştürerek aldığınız *Tahmine dayalı denemeye* tooscore kullanıcı verilerini yapılandırdı.

Bu işlemde örneği görebilirsiniz [izlenecek yol: Azure Machine Learning kredi riski değerlendirmesi için Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md).

Bu makalede derinlemesine eğitim denemenizi Tahmine dayalı bir deneme nasıl dönüştürüldüğü ve bu Tahmine dayalı denemeye nasıl dağıtıldığını hello ayrıntılarını içine alır. Bu ayrıntılar anlayarak öğrenebilir nasıl tooconfigure dağıtılan modeli toomake daha etkili onu.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a>Genel Bakış 

Eğitim deneme tooa Tahmine dayalı denemeye dönüştürme hello işlemi üç adımdan oluşur:

1. Merhaba machine learning eğitilen model algoritması modüllerle değiştirin.
2. Merhaba deneme tooonly Puanlama için gerekli olan bu modüller kesim. Eğitim denemenizi eğitim için gerekli olan, ancak hello modeli eğitildi sonra gerekli olmayan modülleri sayısını içerir.
3. Modelinizi hello web hizmeti kullanıcı verileri nasıl kabul ettiği ve hangi verilerin döndürülür tanımlayın.

> [!TIP]
> Eğitim denemenizi eğitim ve puanlama kendi verilerinizi kullanarak modelinizi ilgilenen. Ancak uygulama dağıtıldıktan sonra kullanıcıların yeni veri tooyour modeli gönderir ve tahmin sonuçlarını döndürür. Dağıtım için hazır, eğitim deneme tooa Tahmine dayalı denemeye tooget dönüştürme gibi bu nedenle, nasıl hello model başkaları tarafından kullanılacak göz önünde bulundurun.
> 
> 

## <a name="set-up-web-service-button"></a>Web hizmetinin ayarı düğmesi
Denemenizi çalıştırdıktan sonra (tıklatın **çalıştırmak** hello deneme tuvalinin hello sonundaki), hello'ı tıklatın **Web hizmetinin ayarı** düğmesini (select hello **Tahmine dayalı Web hizmeti** seçenek). **Web hizmetinin ayarı** eğitim deneme tooa Tahmine dayalı denemenizi dönüştürme üç adımı hello için gerçekleştirir:

1. Merhaba eğitilen model kaydeder **eğitilmiş modeller** hello modül paleti (Merhaba deneme tuvalinin solundaki toohello) bölümü. Ardından hello makine öğrenme algoritmasının yerine geçer ve [Train Model] [ train-model] kaydedilmiş hello modüllerle eğitilmiş model.
2. Denemenizi analiz eder ve yalnızca eğitim için açıkça kullanılmış ve artık gerekmeyen modülleri kaldırır.
3. Bunu ekler _Web hizmeti girişi_ ve _çıkış_ denemenizi (Bu modülleri kabul etmek ve kullanıcı verilerini dönmek) varsayılan konumlarda modüllerine.

Örneğin, hello aşağıdaki örnek census verileri kullanarak iki sınıflı artırılmış karar ağacı modeli trenler deneyin:

![Eğitim denemenizi][figure1]

Bu deneme Hello modülleri temelde dört farklı işlevleri gerçekleştirir:

![Modül işlevleri][figure2]

Bu eğitim deneme tooa Tahmine dayalı denemeye dönüştürürken bazı bu modüllerin artık gerekli olmayan veya farklı bir amaç şimdi verdikleri:

* **Veri** -Bu örnek veri kümesi hello verilerde Puanlama sırasında kullanılmaz - hello kullanıcı hello web hizmetinin skoru hello veri toobe tedarik. Ancak, bu veri kümesi veri türleri gibi hello meta verilerini hello eğitilen modeli tarafından kullanılır. Bu nedenle böylece bu meta verileri sağlayabilir tookeep hello hello Tahmine dayalı denemeye kümesinde gerekir.

* **Hazırlığı** - Puanlama için bu modülleri olabilir veya gerekli tooprocess hello gelen veri olmayabilir gönderilecek hello kullanıcı verilere bağlı olarak. Merhaba **Web hizmetinin ayarı** düğmesi bu touch değil - toodecide gerek toohandle istediğiniz bunları.
  
    Örneğin, bu örnekte hello örnek veri kümesi eksik değerleri böylece olabilir bir [Clean Missing Data] [ clean-missing-data] modül, bunlarla birlikte toodeal. Ayrıca, gerekli tootrain hello modeli olmayan sütunları hello örnek veri kümesi içerir. Bu nedenle bir [Select Columns in Dataset sütun] [ select-columns] modül, dahil edilen tooexclude bu fazladan sütunlarından hello veri akışı. Puanlama için gönderilen bu hello verileri biliyorsanız hello web hizmeti eksik değerleri olmaz ve ardından hello kaldırabilirsiniz [Clean Missing Data] [ clean-missing-data] modülü. Ancak, hello bu yana [Select Columns in Dataset sütun] [ select-columns] modülü yardımcı hello sütunları tanımlamak verilerin Merhaba, eğitilen model bekler, bu modülün tooremain gerekir.

* **Tren** -bu modülleri kullanılan tootrain hello modeli vardır. Tıkladığınızda **Web hizmetinin ayarı**, bu modüller, eğitilmiş hello modeli içeren tek bir modülü ile değiştirilir. Bu yeni modül hello kaydedilir **eğitilmiş modeller** hello modül paleti bölümü.

* **Puan** - Bu örnekte, hello [bölünmüş veri] [ split] test verileri ve eğitim verileri içinde kullanılan toodivide hello veri akışı modülüdür. Merhaba Tahmine dayalı denemeye, biz artık, bunu Eğitim değil [bölünmüş veri] [ split] kaldırılabilir. Benzer şekilde, hello ikinci [Score Model] [ score-model] modülü ve hello [Evaluate Model] [ evaluate-model] modülü hello test kullanılan toocompare sonuçları Bu modüller olmayacak şekilde veri hello Tahmine dayalı denemeler. Merhaba kalan [Score Model] [ score-model] modülü, ancak gerekli tooreturn hello web hizmeti aracılığıyla bir puan sonuç olur.

İşte tıkladıktan sonra örneğimizde nasıl göründüğünü **Web hizmetinin ayarı**:

![Dönüştürülen tahmini deneme][figure3]

işlerini Hello **Web hizmetinin ayarı** yeterli tooprepare bir web hizmeti olarak dağıtılmış, deneme toobe olabilir. Ancak, bazı ek iş belirli tooyour deneme toodo isteyebilirsiniz.

### <a name="adjust-input-and-output-modules"></a>Giriş ve çıkış modülleri Ayarla
Eğitim denemenizi bazı işleme tooget gerekli makine öğrenme algoritmasını hello formdaki verileri sonra hello vermedi ve eğitim veri kümesi kullanılır. Merhaba web hizmeti aracılığıyla tooreceive beklediğiniz hello verileri bu işlem gerekmez, atlayabilirsiniz: hello hello çıkışına bağlayın **Web hizmeti giriş Modülü** tooa farklı denemenizi modülünde. Merhaba kullanıcının verileri artık bu konumda hello modelindeki ulaşırsınız.

Örneğin, varsayılan olarak **Web hizmetinin ayarı** yerleştirmelerin hello **Web hizmeti girişi** hello yukarıda gösterildiği gibi veri akışı hello üstündeki modülü. Ancak biz el ile Merhaba yerleştirebilirsiniz **Web hizmeti girişi** hello veri işleme modülleri geçmiş:

![Taşıma hello web hizmeti girişi][figure4]

Merhaba web hizmeti artık doğrudan hello Score Model modülünün herhangi bir önişleme olmadan geçecek sağlanan hello verileri girin.

Benzer şekilde, varsayılan olarak **Web hizmetinin ayarı** koyar hello Web hizmeti çıkış modülü, veri akışı hello sonundaki. Bu örnekte, toohello kullanıcı hello hello çıktısını hello web hizmeti döndürülecek [Score Model] [ score-model] hello tam giriş verisi vektör artı sonuçları Puanlama hello içeren modülü.
Tooreturn bir şey farklı tercih ediyorsanız, ancak daha sonra hello önce ek modüller ekleyebilirsiniz **Web hizmeti çıkış** modülü. 

Örneğin, tooreturn yalnızca hello Puanlama sonuçları hello tüm vektör değil giriş verilerinin ekleyip bir [Select Columns in Dataset sütun] [ select-columns] dışındaki tüm sütunları hello sonuçları Puanlama modülü tooexclude. Merhaba taşıma **Web hizmeti çıkış** modülü toohello hello çıktısını [Select Columns in Dataset sütun] [ select-columns] modülü. Merhaba deneme şöyle görünür:

![Merhaba web hizmeti çıkış taşıma][figure5]

### <a name="add-or-remove-additional-data-processing-modules"></a>Ek veri işleme modülleri Ekle Kaldır
Puanlama sırasında ihtiyaç bildiğiniz denemenizi daha fazla modülleri varsa bunlar kaldırılabilir. Örneğin, biz hello taşınmış olduğundan **Web hizmeti girişi** modülü tooa noktası hello modülleri işleme verileri, biz hello kaldırabilirsiniz sonra [Clean Missing Data] [ clean-missing-data] Modülü Merhaba tahmini deneme.

Bizim Tahmine dayalı denemeye şimdi şöyle görünür:

![Ek modülü kaldırma][figure6]


### <a name="add-optional-web-service-parameters"></a>İsteğe bağlı Web hizmeti parametreleri ekleme
Bazı durumlarda, Hello hizmet erişildiğinde tooallow hello kullanıcı, web hizmeti toochange hello davranış modüllerin isteyebilir. *Web hizmeti parametreleri* toodo izin bu.

Yaygın bir örnek ayarlama bir [veri içeri aktarma] [ import-data] hello web hizmeti erişildiğinde hello hello kullanıcısı web hizmeti dağıtılmış şekilde modülü farklı bir veri kaynağına belirtebilirsiniz. Veya yapılandırma bir [verileri dışa aktar] [ export-data] modülü böylece farklı bir hedef belirtilebilir.

Web hizmeti parametreleri tanımlamak ve bir veya daha fazla modülü parametreleri ile ilişkilendirmek ve gerekli veya isteğe bağlı oldukları belirtebilirsiniz. Merhaba kullanıcı hello web hizmetinin hello hizmete erişme ve hello modülü Eylemler uygun şekilde değiştirilir Bu parametreler için değerler sağlar.

Hangi Web hizmeti parametreleri hakkında daha fazla bilgi ve bunları nasıl toouse görmek için [kullanarak Azure Machine Learning Web hizmeti parametreleri][webserviceparameters].

[webserviceparameters]: machine-learning-web-service-parameters.md


## <a name="deploy-hello-predictive-experiment-as-a-web-service"></a>Bir web hizmeti olarak Hello tahmini deneme dağıtma
Merhaba Tahmine dayalı denemeye yeterince hazırlandı, bir Azure web hizmeti olarak dağıtabilirsiniz. Merhaba web hizmetini kullanarak, kullanıcılar veri tooyour modeli gönderebilir ve hello modeli kendi tahminleri döndürür.

Merhaba tam dağıtım işlemi hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning web hizmetini dağıtma][deploy]

[deploy]: machine-learning-publish-a-machine-learning-web-service.md


<!-- Images -->
[figure1]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure1.png
[figure2]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure2.png
[figure3]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure3.png
[figure4]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure4.png
[figure5]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure5.png
[figure6]:./media/machine-learning-convert-training-experiment-to-scoring-experiment/figure6.png


<!-- Module References -->
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[export-data]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/
