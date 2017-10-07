---
title: Azure Machine Learning Studio'da aaaCreate metin analiz modelleriniz | Microsoft Docs
description: "Ön işleme metin, N-gram veya özellik karma modülleri kullanarak Azure Machine Learning Studio'daki nasıl toocreate metin analizi modeller"
services: machine-learning
documentationcenter: 
author: rastala
manager: jhubbard
editor: 
ms.assetid: 08cd6723-3ae6-4e99-a924-e650942e461b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: roastala
ms.openlocfilehash: e3799f37ba54bb2ec8815ecf5ed34e145ffb20e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-text-analytics-models-in-azure-machine-learning-studio"></a>Azure Machine Learning Studio’da metin analiz modelleri oluşturma
Metin analizi modelleri faaliyete ve Azure Machine Learning toobuild kullanın. Bu modeller, örneğin, belge sınıflandırma veya düşünceleri çözümleme sorunlarını çözmenize yardımcı olabilir.

Metin analiz denemesi genellikle gerekir:

1. Temizleme ve metin dataset önişle
2. Sayısal özellik vektörlerinin önceden işlenmiş metin ayıklamanızı
3. Sınıflandırma veya regresyon modelini eğitme
4. Puanlama ve hello modeli doğrulama
5. Merhaba modeli tooproduction dağıtma

Bu öğreticide, biz Amazon Kitap incelemeleri veri kümesini kullanarak düşünceleri analiz modeli aracılığıyla yol olarak bu adımları öğrenin (Bu araştırma incelemesine bakın "Biyografileri, Bollywood, müzik kutuları ve Blenders: etki alanı uyarlama düşünceleri sınıflandırma" John Blitzer, işareti Dredze ve Fernando Pereira; İlişkilendirmesini hesaplama Linguistics (ACL) 2007.) Bu veri kümesi gözden geçirme puanları (1-2 veya 4-5) ve serbest biçimli metin oluşur. Merhaba toopredict hello gözden geçirme puan hedeftir: düşük (1 - 2) veya yüksek (4-5).

Bu öğreticide Cortana Intelligence Galerisi kapsamdaki denemeler bulabilirsiniz:

[Kitap incelemeleri tahmin etme](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-1)

[Kitap incelemeleri - Tahmine dayalı denemeye tahmin etme](https://gallery.cortanaintelligence.com/Experiment/Predict-Book-Reviews-Predictive-Experiment-1)

## <a name="step-1-clean-and-preprocess-text-dataset"></a>1. adım: Temizleyin ve metin dataset önişle
Biz, hello deneme kategorik düşük ve yüksek demet tooformulate hello sorun iki sınıflı sınıflandırma olarak hello gözden geçirme puanları bölerek başlayın. Kullanırız [Düzenle meta veri](https://msdn.microsoft.com/library/azure/dn905986.aspx) ve [Grup kategorik değerleri](https://msdn.microsoft.com/library/azure/dn906014.aspx) modüller.

![Etiket oluşturma](./media/machine-learning-text-analytics-module-tutorial/create-label.png)

Ardından, metin hello kullanarak temiz [Önişle metin](https://msdn.microsoft.com/library/azure/mt762915.aspx) modülü. Merhaba temizleme hello gürültü hello kümesindeki azaltır, hello en önemli özellikleri bulmak ve geliştirmeye Yardım hello son model doğruluğunu hello. Biz Durma sözcükleri - "" veya "a" - gibi sık kullanılan sözcük ve sayılar, özel karakterler, yinelenen karakterler, e-posta adreslerini ve URL'leri kaldırın. Biz de Dönüştür hello metin toolowercase hello sözcükleri lemmatize ve ardından belirtilir cümle sınırları algılamak "|||" simgesi önceden işlenmiş metin.

![Metin önişle](./media/machine-learning-text-analytics-module-tutorial/preprocess-text.png)

Ne toouse özel Durma sözcükleri listesini istiyorsunuz? İçinde isteğe bağlı giriş olarak geçirebilirsiniz. Ayrıca, özel C# sözdizimi normal ifade tooreplace alt dizeler kullanın ve konuşma parçası sözcükler kaldırın: isimleri, fiilleri veya sıfatları.

Merhaba ön işleme tamamlandıktan sonra biz hello veri tren bölme ve kümelerini test.

## <a name="step-2-extract-numeric-feature-vectors-from-pre-processed-text"></a>2. adım: sayısal özellik vektörlerinin önceden işlenmiş metin ayıklar.
toobuild metin veri için bir model, genellikle tooconvert serbest biçimli metin sayısal özellik vektörleri vardır. Bu örnekte, kullandığımız [N-Gram özelliklerinden ayıklamak metin](https://msdn.microsoft.com/library/azure/mt762916.aspx) modülü tootransform hello metin veri toosuch biçimi. Bu modül boşluk ayrılmış sözcükler sütunu alır ve bir sözlük sözcüklerin veya N-gram dataset içinde görünen sözcüklerin hesaplar. Ardından, her kez sözcük veya N-gram, her bir kayıtta görüntülenir ve bu özellik vektörler oluşturur kaç sayıları sayar. Bu öğreticide, tek tek sözcükleri ve iki sonraki sözcük birleşimlerini bizim özelliği vektörlerinin dahil şekilde N-gram boyutu too2 ayarlarız.

![N-gram Ayıkla](./media/machine-learning-text-analytics-module-tutorial/extract-ngrams.png)

Biz TF uygulamak * tooN-gram ağırlığı IDF (terim sıklığı ters belge sıklığı) sayar. Bu yaklaşım, tek bir kayıtta sık görünür ancak hello tüm veri kümesi arasında nadiren sözcükler ağırlığını ekler. Diğer seçenekler ve başvuracaklarını grafik ikili, TF, içerir.

Metin özellikleri genellikle yüksek boyut sahiptir. Gövde 100.000 benzersiz sözcükler varsa, N-gram kullanılıyorsa, örneğin, özellik alanınızı 100.000 boyutları ya da daha fazla gerekir. Merhaba ayıklamak N-Gram özellikleri modülü seçenekleri tooreduce hello boyut kümesi sağlar. Kısa veya uzun veya çok seyrek veya çok sık toohave önemli Tahmine dayalı değere eşit olan tooexclude sözcükler seçebilirsiniz. Bu öğreticide, 5'ten az kayıtları veya kayıtları % 80'den fazla görünür N-gram dışlayın.

Ayrıca, tahmin hedefle hello çok olan özellikleri bağıntılı özellik seçimi tooselect kullanabilirsiniz. Kikare özellik seçimi tooselect 1000 özellikler kullanırız. Seçili sözcükleri veya N-gram hello sözlüğünü hello sağ Extract N-gram modülü çıktısını tıklayarak görüntüleyebilirsiniz.

Bir alternatif bir yaklaşım toousing ayıklamak N-Gram özellikleri özellik karma modülünü kullanabilirsiniz. Unutmayın ancak [özellik karma](https://msdn.microsoft.com/library/azure/dn906018.aspx) yapı içinde özellik seçimi özelliklerini veya TF yok * IDF başvuracaklarını.

## <a name="step-3-train-classification-or-regression-model"></a>3. adım: sınıflandırma veya regresyon modelini eğitme
Şimdi hello metin dönüştürülmüş toonumeric özellik sütunları olmuştur. Merhaba dataset Dataset tooexclude Sütunları Seç kullandığımız için önceki aşamaları dize sütunlarından hala içeren bunları.

Ardından kullanırız [iki sınıflı Lojistik regresyon](https://msdn.microsoft.com/library/azure/dn905994.aspx) toopredict bizim hedef: yüksek veya düşük gözden geçirme puanı. Bu noktada, hello metin analytics sorun bir normal sınıflandırma sorunla dönüştürülmüş. Azure Machine Learning tooimprove hello modelde kullanılabilen hello araçları kullanabilirsiniz. Örneğin, farklı sınıflandırıcı toofind verin veya tooimprove hello doğruluğu ayarlama hyperparameter kullanmak nasıl doğru sonuçlar çıkışı deneyimleyebilirsiniz.

![Tren ve puanı](./media/machine-learning-text-analytics-module-tutorial/scoring-text.png)

## <a name="step-4-score-and-validate-hello-model"></a>4. adım: Puanlama ve hello modeli doğrulama
Nasıl hello eğitilen model doğrulamak? Biz hello test veri karşı Puanlama ve hello doğruluğu değerlendirin. Ancak, hello modeli N-gram ve ağırlıklarını hello eğitim kümesinden hello sözlüğünü öğrendiniz. Olarak test verileri özelliklerinden ayıklanıyor toocreating hello sözlük mı başlatacağı değil, bu nedenle, biz o dağarcığı ve bu ağırlıkları kullanmanız gerekir. Bu nedenle, biz hello deneme dalı Puanlama ayıklamak N-Gram özellikleri modülü toohello eklemek, eğitim daldan hello çıkış sözlük bağlanmak ve hello sözlük modu yalnızca tooread ayarlayın. Biz de hello minimum too1 örneği ayarlama ve en fazla too100% tarafından N-gram hello frekans tarafından filtresini devre dışı bırakmanız ve hello özellik seçimi devre dışı bırakma.

Merhaba veriler test metin sütununda dönüştürülmüş toonumeric özellik sütunları sonra biz önceki aşamaları sütunlarından eğitim dalında gibi hello dizesi hariç tutun. Ardından Score Model modülü toomake Öngörüler ve Evaluate Model modülü tooevaluate hello doğruluğu kullanırız.

## <a name="step-5-deploy-hello-model-tooproduction"></a>5. adım: hello modeli tooproduction dağıtma
Merhaba, dağıtılan neredeyse hazır toobe tooproduction modelidir. Web hizmeti olarak dağıtıldığında, serbest biçimli metin dizesini giriş olarak alır ve "Yüksek" veya "Düşük" Tahmin Döndür Öğrenilen hello N-gram sözlük tootransform hello metin toofeatures kullanır ve lojistik regresyon modeli toomake tahmin bu özelliklerinden eğitildi. 

tooset hello Tahmine dayalı denemeye yukarı biz ilk hello N-gram sözlük veri kümesi kaydedin ve hello hello eğitim hello deneme dalı Lojistik regresyon modelinden eğitildi. Ardından, biz "Farklı Kaydet" toocreate kullanarak hello deneme deneme grafik tahmini deneme için kaydedin. Biz, hello deneme hello bölünmüş veri modülü ve hello eğitim dalı kaldırın. Biz ardından daha önce kaydettiğiniz hello N-gram dağarcığı ve model tooExtract N-Gram özellikleri ve Score Model modüller, sırasıyla bağlanın. Biz de hello Evaluate Model modülünü Kaldır.

Biz Önişle metin modülü tooremove hello etiket sütunu önce veri kümesi modülünde Sütunları Seç takın ve puanı modülünde "Append puan sütun toodataset" seçeneğinin işaretini kaldırın. Bu şekilde hello web hizmeti toopredict çalışıyor ve yanıt hello giriş özellikleri göstermez hello etiketini istemez.

![Tahmine dayalı denemeye](./media/machine-learning-text-analytics-module-tutorial/predictive-text.png)

Artık bir web hizmeti olarak yayınlanan ve istek-yanıt ya da toplu iş yürütme API'lerini kullanarak adlı bir denemeyi vardır.

## <a name="next-steps"></a>Sonraki Adımlar
Metin analizi modüllerden hakkında bilgi edinin [MSDN belgelerine](https://msdn.microsoft.com/library/azure/dn905886.aspx).

