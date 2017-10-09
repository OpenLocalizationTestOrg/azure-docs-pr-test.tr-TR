---
title: "5. adım: hello Machine Learning web hizmetini dağıtma | Microsoft Docs"
description: "5. adımını hello geliştirmek Tahmine dayalı bir çözüm izlenecek yol: Tahmine dayalı bir denemeyi Machine Learning Studio'da bir web hizmeti olarak dağıtın."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a>Gözden geçirme adım 5: hello Azure Machine Learning web hizmetini dağıtma
Merhaba kılavuzun hello beşinci adım budur [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Bir Machine Learning çalışma alanı oluşturma](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Mevcut verileri yükleme](machine-learning-walkthrough-2-upload-data.md)
3. [Yeni bir deneme oluşturma](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Eğitmek ve hello modelleri değerlendir](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. **Merhaba web hizmetini dağıtma**
6. [Erişim hello web hizmeti](machine-learning-walkthrough-6-access-web-service.md)

- - -
toogive başka bir fırsat toouse hello Biz bu kılavuzda geliştirilen Tahmine dayalı bir model, biz bunu Azure üzerinde bir web hizmeti olarak dağıtabilirsiniz.

Toothis noktası biz modelimizi eğitim ile denemeler. Ancak dağıtılan hello hizmeti artık toodo eğitim geçiyor - toogenerate yeni tahminleri bizim modelini temel alan hello kullanıcının giriş Puanlama tarafından gittiği. Toodo yapacağız şekilde bazı hazırlık tooconvert bu deneme gelen bir ***eğitim*** tooa denemeler ***Tahmine dayalı*** deneyin. 

Bu üç adımlık bir işlemdir.  

1. Merhaba modelleri kaldırın
2. Merhaba Dönüştür *eğitim denemenizi* içine oluşturduk bir *tahmini deneme*
3. Bir web hizmeti olarak Hello tahmini deneme dağıtma

## <a name="remove-one-of-hello-models"></a>Merhaba modelleri kaldırın

İlk olarak, tootrim bu deneme aşağı biraz ihtiyacımız var. Şu anda iki farklı modelleri hello denemesinde sahip olduğumuz ancak Biz bu web hizmeti olarak dağıttığınızda yalnızca toouse bir model istiyoruz.  

Biz bu boosted hello ağacı modeli hello SVM modeli daha iyi gerçekleştirilen karar varsayalım. Merhaba ilk şey toodo Kaldır hello olacak şekilde [iki sınıflı destek vektör makinesi] [ two-class-support-vector-machine] modülü ve eğitim için kullanılan hello modüller. Tıklayarak toomake hello deneme kopyasını ilk isteyebilirsiniz **Kaydet** tuvale hello hello sonunda deneme.

Modüller aşağıdaki toodelete hello ihtiyacımız var:  

* [İki sınıflı destekli vektör makinesi][two-class-support-vector-machine]
* [Modeli eğitmek] [ train-model] ve [Score Model] [ score-model] bağlı tooit olan modülleri
* [Veri normalleştirin] [ normalize-data] (her ikisi de)
* [Modeli değerlendirin] [ evaluate-model] (biz hello modelleri değerlendirme tamamlanmış olduğundan)

Her modül ve hello Delete anahtar ya da sağ tıklatma hello modülü basın seçip **silmek**. 

![Merhaba SVM modeli kaldırıldı][3a]

Modelimizi bu gibi görünmelidir:

![Merhaba SVM modeli kaldırıldı][3]

Hazır toodeploy ki artık bu model hello kullanarak [iki-Class Boosted karar ağacı][two-class-boosted-decision-tree].

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Merhaba eğitim deneme tooa Tahmine dayalı denemeye Dönüştür

tooget Bu model hazır dağıtımı için tooconvert deneme tooa Tahmine dayalı denemeye eğitim gerekli. Bu üç adımdan oluşur:

1. Merhaba modeli eğittiğimize ve bizim eğitim modüllerini Değiştir kaydedin
2. Eğitim için yalnızca gerekli olan hello deneme tooremove modülleri kırpma
3. Burada hello web hizmeti girişi kabul eder ve burada hello çıktı üretir tanımlayın

El ile yapabileceğimiz ancak tıklayarak üç adımı Neyse gerçekleştirilebilir **Web hizmetinin ayarı** hello deneme tuvalinin hello sonundaki (Merhaba seçerek **Tahmine dayalı Web hizmeti** seçenek).

> [!TIP]
> Daha fazla bilgi isterseniz Tahmine dayalı bir eğitim deneme tooa Dönüştür ne olur denemeler bkz [nasıl tooprepare modelinizi Azure Machine Learning Studio'daki dağıtımı için](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Tıkladığınızda **Web hizmetinin ayarı**, olacaklar:

* Merhaba eğitilen model olan tek dönüştürülmüş tooa **eğitilen Model** modülü ve hello modül paleti toohello içinde depolanan hello solundaki deneme tuvaline (altında bulabilirsiniz **eğitilmiş modeller**)
* Eğitim için kullanılan modülleri kaldırılır; özellikle:
  * [İki sınıflı artırılmış karar ağacı][two-class-boosted-decision-tree]
  * [Train Model][train-model]
  * [Veri bölme][split]
  * Merhaba ikinci [R betiği yürütün] [ execute-r-script] test verileri için kullanılan Modülü
* kaydedilen hello eğitilen model geri hello deneme eklenir
* **Web hizmeti girişi** ve **Web hizmeti çıkış** modülleri eklenir (bunlar hello kullanıcının verileri hello model burada girer ve hello web hizmeti erişildiğinde hangi verilerin döndürülen belirleme)

> [!NOTE]
> Merhaba deneme hello deneme tuvalinin hello üstünde eklenen sekmeleri altında iki bölümden kaydedilir görebilirsiniz. Merhaba özgün eğitim denemenizi olduğu hello sekmesi altında **eğitim denemenizi**, ve yeni oluşturulan Tahmine dayalı denemeye hello altında **Tahmine dayalı denemeye**. Merhaba Tahmine dayalı denemeye hello bir web hizmeti olarak dağıtma ' dir.

Bir ek adım belirli bu deneme tootake ihtiyacımız var.
İki eklediğimiz [R betiği yürütün] [ execute-r-script] modülleri tooprovide ağırlığı toohello veri işlev. Bu modüller hello son modelinde çıkışı olabilmesi için biz eğitim ve test için gerekli bir eli oluştu.
Machine Learning Studio kaldırılmış bir [R betiği yürütün] [ execute-r-script] hello kaldırıldığında Modülü [bölünmüş] [ split] modülü. Biz kaldırabilirsiniz artık diğer hello ve bağlanın [meta verileri Düzenleyicisi] [ metadata-editor] doğrudan çok[Score Model][score-model].    

Bizim deneme gibi görünmelidir:  

![Merhaba, eğitilen modeli Puanlama][4]  

> [!NOTE]
> Biz hello Tahmine dayalı denemesinde hello UCI Almanca kredi kartı verileri dataset neden sol merak ediyor olabilirsiniz. Merhaba hizmet tooscore hello kullanıcının verileri, değil hello özgün veri kümesi, bu nedenle neden hello özgün dataset hello modelinde bırakın geçiyor?
> 
> Hello hizmet özgün kredi kartı verileri hello olmayan geçerlidir. Ancak, hello şeması vardır kaç sütunlar gibi bilgileri içerir ve hangi sütunların sayısal bu verileri, gerekir. Bu şema bilgileri gerekli toointerpret hello kullanıcının verilerdir. Biz bu bileşenlerin Merhaba hizmeti çalışırken hello Puanlama modülü hello dataset şeması sahip olması bağlı bırakın. Merhaba veri değil kullanıldığında, yalnızca hello şema.  
> 
> 

Merhaba denemeyi son bir kez çalıştırın (tıklatın **çalıştırmak**.) Model hello tooverify çalışmaya devam isterseniz, hello hello çıktısını tıklatın [Score Model] [ score-model] modülü ve select **sonuçları görüntüleme**. Merhaba özgün veriler, hello kredi riski değeri ("skoru etiketleri") ve olasılık değeri ("skoru olasılıklar".) Puanlama hello birlikte görüntülendiğini görebilirsiniz 

## <a name="deploy-hello-web-service"></a>Merhaba web hizmetini dağıtma
Merhaba deneme ya da Klasik web hizmeti olarak ya da Azure Resource Manager tabanlı yeni bir web hizmeti olarak dağıtabilirsiniz.

### <a name="deploy-as-a-classic-web-service"></a>Klasik web hizmeti olarak dağıtma
Klasik web hizmeti bizim deneme türetilen toodeploy tıklatın **Web hizmeti Dağıt** hello tuvale ve seçin **Web hizmeti Dağıt [Klasik]**. Machine Learning Studio'da bir web hizmeti olarak hello deneme dağıtır ve toohello Pano, web hizmeti alır. Bu sayfadan toohello deneme döndürebilirsiniz (**görünüm anlık görüntü** veya **görüntülemek son**) ve basit bir sınama hello web hizmetinin çalıştırın (bkz **Test hello web hizmeti** aşağıda). Merhaba web hizmetine (daha ayrıntılı hello sonraki adımda bu kılavuzun) erişebilirsiniz uygulamaları oluşturmak için buradaki bilgiler bulunmaktadır.

![Web hizmeti Panosu][6]

Merhaba tıklatarak hello hizmet yapılandırabilirsiniz **yapılandırma** sekmesi. Burada hello hizmet adını (verilen hello deneme adını varsayılan olarak değil) değiştirebilirsiniz ve bir açıklama girin. Daha fazla kolay etiketleri Merhaba verebilirsiniz girdi ve çıktı verilerini.  

![Merhaba web hizmetini yapılandır][5]  

### <a name="deploy-as-a-new-web-service"></a>Yeni bir web hizmeti olarak dağıtma

> [!NOTE] 
> toodeploy hello abonelik toowhich dağıttığınız yeterli izinlere sahip yeni bir web hizmetini web hizmeti hello. Daha fazla bilgi için bkz: [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir web hizmeti yönetmek](machine-learning-manage-new-webservice.md). 

Yeni bir web hizmeti toodeploy bizim deneme türetilmiş:

1. Tıklatın **Web hizmeti Dağıt** hello tuvale ve seçin **Web hizmeti dağıtma [Yeni]**. Machine Learning Studio toohello Azure Machine Learning web hizmetleri aktarır **dağıtmak deneme** sayfası.

2. Merhaba web hizmeti için bir ad girin. 

3. İçin **fiyat planı**, var olan bir fiyatlandırma planı seçin veya Seç "Yeni Oluştur" ve verin hello yeni bir ad ve select hello aylık plan seçeneği planlayın. Katmanları toohello planları varsayılan bölgeniz ve web hizmetiniz için varsayılan hello planı dağıtılan toothat bölgedir.

4. Tıklatın **dağıtmak**.

Birkaç dakika sonra hello **Hızlı Başlangıç** web hizmetiniz için sayfası açılır.

Merhaba tıklatarak hello hizmet yapılandırabilirsiniz **yapılandırma** sekmesi. Burada hello hizmet değiştirebilirsiniz başlığı ve bir açıklama girin. 

tootest hello web hizmeti, hello tıklatın **Test** sekmesini (bkz **Test hello web hizmeti** aşağıda). Merhaba hello web hizmeti erişebileceği uygulamaları oluşturma hakkında daha fazla bilgi için tıklatın **Tüket** sekmesinde (Merhaba sonraki adım bu kılavuzda daha fazla ayrıntıya çıkar).

> [!TIP]
> Dağıttıktan sonra sonra hello web hizmeti güncelleştirebilirsiniz. Örneğin, modelinizi toochange istiyorsanız, ardından hello eğitim denemenizi düzenleyebilir, hello modeli parametreleri ince ayar ve tıklatın **Web hizmeti Dağıt**, seçme **Web hizmeti Dağıt [Klasik]** veya  **[Yeni] Web hizmetini dağıtma**. Merhaba deneme yeniden dağıttığınızda, artık güncelleştirilmiş model kullanarak hello web hizmeti değiştirir.  
> 
> 

## <a name="test-hello-web-service"></a>Test hello web hizmeti

Merhaba web hizmeti erişildiğinde hello kullanıcının verileri hello girer **Web hizmeti girişi** burada da geçtikten toohello Modülü [Score Model] [ score-model] modülü ve skoru. Merhaba şekilde, biz hello Tahmine dayalı denemeye ayarladınız hello modeli aynı hello özgün kredi riski veri kümesi biçimi hello içinde veri bekliyor.
Merhaba aracılığıyla hello web hizmetinden, toohello kullanıcı Hello sonuçlarının döndürüldüğü **Web hizmeti çıkış** modülü.

> [!TIP]
> Merhaba şekilde yapılandırılmış, hello Tahmine dayalı denemeye hello tüm sahibiz hello sonuçları [Score Model] [ score-model] modülü döndürülür. Bu, tüm hello giriş verisi artı hello kredi riski değeri ve olasılık Puanlama hello içerir. Ancak isterseniz, farklı bir şey dönebilirsiniz - Örneğin, yalnızca hello kredi riski değer döndürebilirsiniz. toodo Bu, INSERT bir [proje sütunları] [ project-columns] modülü arasında [Score Model] [ score-model] ve hello **Web hizmeti çıkış** istemediğiniz tooeliminate sütunları hello web hizmeti tooreturn. 
> 
> 

Klasik web test edebilirsiniz ya da hizmet **Machine Learning Studio** veya hello **Azure Machine Learning Web Hizmetleri** portal.
Yeni bir web hizmeti yalnızca hello test **Machine Learning Web Hizmetleri** portal.

> [!TIP]
> Hello Azure Machine Learning Web Hizmetleri Portalı'nda test edilirken tootest hello istek-yanıt hizmeti kullanabileceğiniz örnek veri oluşturma hello portal olabilir. Merhaba üzerinde **yapılandırma** sayfasında, için "Evet" seçeneğini **örnek veriler etkin?**. Merhaba hello istek-yanıt sekmesinde açtığınızda **Test** sayfasında hello portal hello özgün kredi riski veri kümesinden alınan örnek verileri doldurur.

### <a name="test-a-classic-web-service"></a>Klasik web hizmetini sınama

Machine Learning Studio'da veya hello Machine Learning Web Hizmetleri portalında bir Klasik web hizmeti test edebilirsiniz. 

#### <a name="test-in-machine-learning-studio"></a>Machine Learning Studio'da test

1. Merhaba üzerinde **PANO** hello sayfasında hello web hizmeti için **Test** altında düğmesini **varsayılan uç nokta**. Bir iletişim kutusu açılır ve hello hizmeti için bir giriş verisi hello sorar. Bunlar hello hello özgün kredi riski dataset içinde görünen aynı sütunları olur.  

2. Bir veri kümesi girin ve ardından **Tamam**. 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a>Merhaba Machine Learning Web Hizmetleri Portalı'nda test

1. Merhaba üzerinde **PANO** hello sayfasında hello web hizmeti için **Test Önizleme** altında bağlantı **varsayılan uç nokta**. Merhaba web hizmeti uç noktası için hello Azure Machine Learning Web Hizmetleri portalında Hello test sayfası açılır ve hello hizmeti için bir giriş verisi hello sorar. Bunlar hello hello özgün kredi riski dataset içinde görünen aynı sütunları olur.

2. Tıklatın **Test istek-yanıt**. 

### <a name="test-a-new-web-service"></a>Yeni bir web hizmeti test etme

Yalnızca hello Machine Learning Web Hizmetleri portalında yeni bir web hizmeti test edebilirsiniz.

1. Merhaba, [Azure Machine Learning Web Hizmetleri](https://services.azureml.net/quickstart) portal tıklatın **Test** hello sayfanın üst kısmındaki hello. Merhaba **Test** sayfası açılır ve hello hizmeti verileri girebilirsiniz. Görüntülenen hello giriş alanları hello özgün kredi riski dataset içinde görünen toohello sütunlar karşılık gelir. 

2. Bir veri kümesi girin ve ardından **Test istek-yanıt**.

Merhaba hello test sonuçlarını hello sağ tarafında hello çıkış sütununun hello sayfasında görüntülenir. 


## <a name="manage-hello-web-service"></a>Merhaba web hizmetini yönetme

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a>Merhaba Klasik Azure portalında bir Klasik web hizmeti yönetme

Klasik web hizmeti dağıttıktan sonra sonra hello yönetebilirsiniz [Klasik Azure portalı](https://manage.windowsazure.com).

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com)
2. Merhaba Microsoft Azure Hizmetleri panelinde tıklatın **MACHINE LEARNING**
3. Çalışma alanınızı tıklatın
4. Merhaba tıklatın **Web Hizmetleri** sekmesi
5. Oluşturduğumuz hello web hizmeti
6. Merhaba "varsayılan" uç noktasına tıklayın

Buradan, hello web hizmeti nasıl çalıştığını izlemek gibi şeyler ve kaç tane eşzamanlı çağrıları hello hizmet işleyebilir değiştirerek performans tweaks hale getirebilirsiniz.

Daha ayrıntılı bilgi için bkz.

* [Uç noktaları oluşturma](machine-learning-create-endpoint.md)
* [Web hizmeti ölçeklendirme](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a>Klasik veya yeni bir web hizmeti hello Azure Machine Learning Web Hizmetleri portalında Yönet

Klasik ya da yeni web hizmetinizi dağıttıktan sonra sonra hello yönetebilirsiniz [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/quickstart) portal.

web hizmetinizin toomonitor hello performans:

1. İçinde toohello oturum [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/quickstart) portalı
2. Tıklatın **Web Hizmetleri**
3. Web hizmeti
4. Merhaba tıklatın **Panosu**

- - -
**Sonraki: [erişim hello web hizmeti](machine-learning-walkthrough-6-access-web-service.md)**

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
