---
title: bir Azure Machine Learning modeli aaaHow bir web hizmeti olur | Microsoft Docs
description: "Bir geliştirme, Azure Machine Learning modeli ilerler tooan nasıl denemeler, hello mekanizması genel bir bakış Web hizmeti kullanıma hazır hale getirilmiş."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 25e0c025-f8b0-44ab-beaf-d0f2d485eb91
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 2bbe09fa8fa22662cf8ec4a8b6249d23c87c8ddf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-a-machine-learning-model-progresses-from-an-experiment-tooan-operationalized-web-service"></a>Nasıl bir deneme tooan bir Machine Learning modeli ilerler Web hizmeti kullanıma hazır hale getirilmiş
Azure Machine Learning Studio toodevelop çalıştırın, böylece etkileşimli bir tuval sağlar, test ve yinelemek bir ***denemeler*** Tahmine dayalı bir modeli temsil eden. Çok çeşitli olabilir modülleri vardır:

* Denemenizi giriş verilerini
* Merhaba verileri işlemek
* Machine learning algoritmaları kullanarak bir model eğitme
* Puan hello modeli
* Merhaba sonuçları değerlendirin
* Çıkış son değerleri

İle denemenizi memnun kaldıktan sonra olarak dağıtabilirsiniz bir ***Klasik Azure Machine Learning Web hizmeti*** veya ***yeni Azure Machine Learning Web hizmeti*** böylece kullanıcılar yeni veri gönderme ve geri alma sonuçları.

Bu makalede, nasıl bir geliştirme deneme tooan, Machine Learning modeli ilerler Web hizmeti kullanıma hazır hale getirilmiş, hello mekanizması genel bir bakış sağlar.

> [!NOTE]
> Diğer yolları toodevelop vardır ve makine öğrenimi modellerini dağıtmak, ancak bu makale, Machine Learning Studio nasıl kullandığınıza odaklanmıştır. Örneğin, tooread nasıl toocreate Klasik Tahmine dayalı Web hizmeti r ile blog yayınına bakın hello açıklaması [yapı & dağıtmak Tahmine dayalı Web uygulamaları kullanarak Rstudio'dan ve Azure ML](http://blogs.technet.com/b/machinelearning/archive/2015/09/25/build-and-deploy-a-predictive-web-app-using-rstudio-and-azure-ml.aspx).
> 
> 

Azure Machine Learning Studio tasarlanmış toohelp olsa da, geliştirmek ve dağıtmak bir *Tahmine dayalı analiz modeli*, olası toouse Studio toodevelop Tahmine dayalı bir modeli içermeyen bir deneme değil. Örneğin, bir deneme yalnızca giriş verisi olabilir ve ardından çıkış hello sonuçları yönlendirebilir. Bir Tahmine dayalı analiz deneme gibi Tahmine dayalı olmayan bu deneme bir Web hizmeti olarak dağıtabilirsiniz, ancak hello deneme değil veya eğitim machine learning modeli Puanlama olduğundan daha basit bir işlem değil. Bu şekilde hello tipik toouse Studio olmamasına karşın, Studio nasıl çalıştığı hakkında ile ilgili eksiksiz bir açıklama sunuyoruz biz bunu hello tartışmada içermesi.

## <a name="developing-and-deploying-a-predictive-web-service"></a>Geliştirme ve Tahmine dayalı bir Web hizmetini dağıtma
Geliştirmek ve Machine Learning Studio kullanarak dağıtmak gibi tipik bir çözüm izleyen hello aşamaları şunlardır:

![Dağıtım akışı](media/machine-learning-model-progression-experiment-to-web-service/model-stages-from-experiment-to-web-service.png)

*Şekil 1 - Tipik Tahmine dayalı bir modeli aşamaları*

### <a name="hello-training-experiment"></a>Merhaba eğitim denemenizi
Merhaba ***eğitim denemenizi*** Web hizmetiniz Machine Learning Studio'da geliştirmenin hello ilk aşamasıdır. Merhaba eğitim denemenizi Hello amacı, bir yere toodevelop test yineleme ve sonunda bir machine learning modelini eğitmek toogive budur. Bile birden fazla modeli aynı anda hello en iyi çözüm arayın, ancak işiniz bittiğinde, denemeler eğitilmiş tek bir seçersiniz eğitmek model ve hello kalan hello deneme kısmından ortadan kaldırmak. Bir Tahmine dayalı analiz denemesi geliştirmek ilişkin bir örnek için bkz: [Azure Machine Learning kredi riski değerlendirmesi için Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md).

### <a name="hello-predictive-experiment"></a>Merhaba tahmini deneme
Eğitim denemenizi bir modeli eğittikten sonra tıklatın **Web hizmetinin ayarı** seçip **Tahmine dayalı Web hizmeti** eğitim dönüştürme Machine Learning Studio tooinitiate hello işleminde tooa denemeler ***Tahmine dayalı denemeye***. hello Tahmine dayalı denemeye amacı Merhaba, eğitilen model tooscore yeni verilerle, sonuçta bir Azure Web hizmeti olarak kullanıma hazır hale getirilmiş olma hello amacı toouse olduğu.

Bu dönüştürme için aşağıdaki adımları hello yapılır:

* Tek bir modüle eğitim için kullanılan modülleri Hello kümesi dönüştürmek ve eğitilen model olarak Kaydet
* İlgili olmayan yabancı modülleriniz ortadan tooscoring
* Giriş eklemek ve nihai Web hizmetini kullanacak olan hello bağlantı noktalarını çıkış

Daha fazla değişiklik Tahmine dayalı denemeye hazır toodeploy bir Web hizmeti olarak toomake tooget istediğiniz olabilir. Örneğin, hello Web hizmeti toooutput sonuçları yalnızca bir kısmı istiyorsanız, önce hello çıkış bağlantı noktasına filtreleme modülü ekleyebilirsiniz.

Bu dönüştürme işlemi hello eğitim denemenizi atılan değil. Merhaba işlemi tamamlandığında, Studio'da iki sekme vardır: biri hello eğitim denemenizi, diğeri hello tahmini deneme için. Bu şekilde, Web hizmetini dağıtma ve hello Tahmine dayalı denemeye yeniden önce toohello eğitim denemenizi değişiklikler yapabilirsiniz. Veya başka bir satırlık bir deney hello eğitim deneme toostart bir kopyasını kaydedebilirsiniz.

> [!NOTE]
> Tıkladığınızda **Tahmine dayalı Web hizmeti** eğitim deneme tooa Tahmine dayalı denemenizi otomatik işlemi tooconvert başlatın ve bu da çoğu durumda çalışır. Eğitim denemenizi karmaşık ise (örneğin, birlikte katılma eğitim için birden fazla yol varsa), toodo bu dönüştürme el ile tercih ettiğiniz. Daha fazla bilgi için bkz: [nasıl tooprepare modelinizi Azure Machine Learning Studio'daki dağıtımı için](machine-learning-convert-training-experiment-to-scoring-experiment.md).
> 
> 

### <a name="hello-web-service"></a>Merhaba Web hizmeti
Memnun kaldıktan sonra Tahmine dayalı denemeye hazır, hizmetiniz bir Klasik Web hizmeti olarak dağıtabilir veya yeni Web hizmeti tabanlı Azure Resource Manager. toooperationalize olarak dağıtarak modelinizi bir *Klasik Machine Learning Web hizmeti*, tıklatın **Web hizmeti Dağıt** seçip **Web hizmeti Dağıt [Klasik]**. toodeploy olarak *yeni Machine Learning Web hizmeti*, tıklatın **Web hizmeti Dağıt** seçip **Web hizmeti dağıtma [Yeni]**. Kullanıcılar artık hello Web hizmeti REST API kullanarak veri tooyour modeli gönderebilir ve geri hello sonuçları alabilirsiniz. Daha fazla bilgi için bkz: [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).

## <a name="hello-non-typical-case-creating-a-non-predictive-web-service"></a>Merhaba normal olmayan durum: Tahmine dayalı olmayan bir Web hizmeti oluşturma
Denemenizi eğitmek değil, Tahmine dayalı bir modeli, ardından toocreate eğitim denemenizi ve puanlama deneme gerekmez - yalnızca bir deneme yoktur ve bir Web hizmeti olarak dağıtabilirsiniz. Machine Learning Studio kullanmış olduğunuz hello modülleri çözümleyerek denemenizi Tahmine dayalı bir model içerip içermediğini algılar.

Denemenizi üzerinde yinelendiğinde ve onunla memnun sonra:

1. ' I tıklatın **Web hizmetinin ayarı** seçip **Web hizmeti yeniden eğitme** - giriş ve çıkış düğümlerini otomatik olarak eklenir
2. Tıklatın **çalıştırın**
3. Tıklatın **Web hizmeti Dağıt** seçip **Web hizmeti Dağıt [Klasik]** veya **Web hizmeti dağıtma [Yeni]** toodeploy istediğiniz hello ortamı toowhich bağlı olarak.

Web hizmeti artık dağıtılır ve erişmek ve yalnızca bir Tahmine dayalı Web hizmeti gibi yönetebilirsiniz.

## <a name="updating-your-web-service"></a>Web hizmetiniz güncelleştirme
Bir Web hizmeti olarak denemenizi dağıttığınıza göre yoksa ne ihtiyacınız tooupdate onu?

Bağımlıdır neleri sağlamanız gerektiğine tooupdate:

**Toomodify istediğiniz veya toochange hello giriş veya çıkış istediğiniz hello Web hizmeti verileri nasıl düzenler**

Merhaba modeli değiştirmiyorsanız, ancak yalnızca hello Web hizmeti veri işleme biçimini değiştirme, hello Tahmine dayalı denemeye düzenleyin ve ardından **Web hizmeti Dağıt** seçip **Web hizmeti [Klasik]Dağıt** veya **Web hizmeti dağıtma [Yeni]** yeniden. Merhaba Web hizmeti durdurulursa, hello güncelleştirilmiş Tahmine dayalı denemeye dağıtılır ve hello Web hizmeti yeniden başlatılır.

Örnek aşağıda verilmiştir: Tahmine dayalı denemenizi hello tüm hello ile giriş veri satırının döndürür varsayalım tahmin sonucu. Merhaba Web hizmeti toojust dönüş hello sonucu istediğiniz karar verebilirsiniz. Ekleyebileceğiniz şekilde bir **proje sütunları** hello Tahmine dayalı denemeye modülünde sağ hello bağlantı noktası, çıktı önce hello dışındaki tooexclude sütunları sonucu. Tıkladığınızda **Web hizmeti Dağıt** seçip **Web hizmeti Dağıt [Klasik]** veya **Web hizmeti dağıtma [Yeni]** hello Web hizmeti yeniden güncelleştirilir.

**Yeni veri tooretrain hello modeliyle istiyor**

Machine learning modeli tookeep istiyor ancak tooretrain istersiniz, yeni verilerle iki seçeneğiniz vardır:

1. **Merhaba Web hizmeti çalışırken hello modeli yeniden eğitme** -hello Tahmine dayalı Web hizmeti çalışırken modelinizi tooretrain istiyorsanız, birkaç değişiklik toohello eğitim deneme toomake yaparak bunu yapabilirsiniz, bir *** denemeyi yeniden eğitme***, olarak dağıtabilirsiniz sonra bir  ***yeniden eğitme web* hizmet**. Yönergeler için toodo buna ek olarak, bkz: [yeniden eğitme Machine Learning modellerini programlama aracılığıyla](machine-learning-retrain-models-programmatically.md).
2. **Toohello özgün eğitim denemenizi geri dönün ve farklı eğitim veri toodevelop modelinizi kullanmak** - Tahmine dayalı denemenizi bağlantılı toohello Web hizmeti olan ancak hello eğitim denemenizi doğrudan bu şekilde bağlanmamış. Merhaba özgün eğitim denemenizi değiştirip tıklatın **Web hizmetinin ayarı**, oluşturacağı bir *yeni* Tahmine dayalı, denemeler dağıtıldığında, oluşturacak bir *yeni* Web hizmet. Yalnızca hello özgün Web hizmeti de güncelleştirmez.
   
   Toomodify hello eğitim denemenizi gerekiyorsa, bunu açıp tıklatın **Kaydet** toomake bir kopyası. Bu, olduğu gibi hello özgün eğitim deneme, Tahmine dayalı denemeye ve Web hizmeti bırakır. Bu gibi durumlarda, yeni bir Web hizmeti artık yaptığınız değişikliklerle oluşturabilirsiniz. Ardından karar verebilirsiniz hello yeni Web hizmeti dağıttıktan sonra bir kez olup toostop önceki Web hizmeti hello veya yeni bir hello çalışmasını sağlamak.

**Tootrain farklı bir model istiyorsunuz**

Toomake öğrenme algoritmasının, başka bir makine seçme gibi tooyour özgün Tahmine dayalı denemeye, değişiklikleri istiyorsanız çalışırken farklı eğitim yöntemi, vb. sonra toofollow hello ikinci yordam modelinizi yeniden eğitme için yukarıda açıklanan yeterlidir: Merhaba eğitim denemenizi açın, **Kaydet** toomake bir kopyasını ve yoldan modelinizi geliştirme, hello tahmini deneme oluşturma ve dağıtma hello yeni başlatın hello web hizmeti. Bu yeni bir oluşturacak Web hizmeti, özgün toohello ilgisiz - çalıştıran bir veya iki, hangi tookeep karar verebilirsiniz.

## <a name="next-steps"></a>Sonraki Adımlar
Geliştirme ve deneme hello işlemi hakkında daha fazla ayrıntı için aşağıdaki makaleler hello bakın:

* Merhaba deneme - dönüştürme [nasıl tooprepare modelinizi Azure Machine Learning Studio'daki dağıtımı için](machine-learning-convert-training-experiment-to-scoring-experiment.md)
* Merhaba Web hizmeti - dağıtma [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md)
* yeniden eğitme hello model - [yeniden eğitme Machine Learning modellerini programlama aracılığıyla](machine-learning-retrain-models-programmatically.md)

Merhaba tüm işlem örnekler için bkz:

* [Machine learning Öğreticisi: Azure Machine Learning Studio'da ilk denemenizi oluşturma](machine-learning-create-experiment.md)
* [İzlenecek yol: Azure Machine Learning kredi riski değerlendirmesi için Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)

