---
title: aaaDebug modelinizi Azure Machine Learning | Microsoft Docs
description: "Nasıl toodebug hataları Azure Machine Learning modüllerinin Train Model ve Score Model tarafından üretilen."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: ee38ca8ce38d4fc7add5ba70c80ab9bb2ceaf1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a>Azure Machine Learning’de Model Hatalarını Ayıklama

Bu makalede neden iki hataları aşağıdaki hello birini bir model çalıştırırken karşılaşılabilecek hello olası nedenleri açıklanmaktadır:

* Merhaba [Train Model] [ train-model] modülünde bir hata oluşturur 
* Merhaba [Score Model] [ score-model] modülü hatalı sonuçlar üretir 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a>Train Model modülünün bir hata oluşturur

![image1](./media/machine-learning-debug-models/train_model-1.png)

Merhaba [Train Model] [ train-model] modülü iki girdi bekliyor:

1. Azure Machine Learning tarafından sağlanan modellerin hello koleksiyonundan makine öğrenimi modeline Hello türü.
2. Merhaba eğitim verilerini belirten belirtilen etiket sütunu hello değişken toopredict (Merhaba diğer sütunları toobe özellikleri varsayılır).

Bu modül durumları aşağıdaki hello hata oluşturabilir:

1. Merhaba etiket sütunu yanlış belirtilmiş. Bu etiket hello birden fazla sütun seçildi ya da yanlış sütun dizini seçili meydana gelebilir. Örneğin, bir sütun dizini 30 yalnızca 25 sütunları olan bir giriş veri kümesi ile kullandıysanız hello ikinci durum geçerli olur.

2. Merhaba veri kümesi herhangi bir özellik sütunu içermiyor. Örneğin, hello girdi veri kümesi hello etiket sütun işaretlendiğinden, yalnızca bir sütun varsa olurdu hangi toobuild hello modeliyle hiçbir özellik. Bu durumda, hello [Train Model] [ train-model] modülünde bir hata oluşturur.

3. Merhaba girdi veri kümesi (özellikleri veya etiketi) sonsuz bir değer içeriyor.

## <a name="score-model-module-produces-incorrect-results"></a>Score Model modülünün hatalı sonuçlar üretir

![image2](./media/machine-learning-debug-models/train_test-2.png)

Bir tipik eğitim ve sınama denemesinde denetimli öğrenme için hello [bölünmüş veri] [ split] modülü iki bölüme hello özgün dataset böler: bir parçasıdır kullanılan tootrain hello modeli ve bir bölümü kullanılır tooscore ne kadar iyi hello eğitilen model gerçekleştirir. kullanılan tooscore hello sonra test verileri, sonra hello sonuçları değerlendirilen toodetermine hello hello modeli doğruluğunu olduğu hello eğitilen modelidir.

Merhaba [Score Model] [ score-model] modülü iki giriş gerektirir:

1. Merhaba eğitilen model çıktısını [Train Model] [ train-model] modülü.
2. Merhaba kümesinden farklı bir Puanlama dataset tootrain hello modeli kullanılır.

Merhaba deneme başarılı olsa bile hello olası kullanıcının [Score Model] [ score-model] modülü hatalı sonuçlar üretir. Bazı senaryolarda bu toohappen neden olabilir:

1. Merhaba etiket kategorik ve bir regresyon modeli hello verileri eğitildi belirtilmişse, hatalı bir çıktı hello tarafından üretilen [Score Model] [ score-model] modülü. Regresyon sürekli yanıt değişkeni gerektirdiğinden budur. Bu durumda, daha uygun toouse bir sınıflandırma modeli olacaktır. 

2. Benzer şekilde, bir sınıflandırma modeli kayan nokta numarası hello etiket sütuna sahip bir veri kümesi üzerinde eğitildi, istenmeyen sonuçlara neden olabilir. Yalnızca bu aralık değerleri sınıfların sonlu ve genellikle biraz küçük, küme üzerinde veren bir ayrık yanıt değişken Sınıflandırmayı gerektirmiyor olmasıdır.

3. Veri kümesi Puanlama hello tüm hello kullanılan özellikler tootrain hello modeli içermiyorsa hello [Score Model] [ score-model] bir hata oluşturur.

4. Veri kümesi Puanlama hello satırda eksik bir değer veya özelliklerinden birini sonsuz bir değer içeriyorsa, hello [Score Model] [ score-model] hiçbir çıktı karşılık gelen toothat satır oluşturmaz.

5. Merhaba [Score Model] [ score-model] dataset Puanlama hello içindeki tüm satırların aynı çıktıları üretebilir. Bu, örneğin, örnekleri yaprak düğümü başına en az sayıda hello eğitim örnekleri kullanılabilir hello birden çok toobe sayısı seçilirse karar ormanları kullanarak sınıflandırma çalışılırken gerçekleşebilir.

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

