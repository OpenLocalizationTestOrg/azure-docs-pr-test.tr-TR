---
title: "Özellik Seçimi takım veri bilimi işleminde | Microsoft Docs"
description: "Özellik Seçimi amacını açıklayan ve machine learning veri geliştirme sürecinin içindeki rollerine örnekler sağlar."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 878541f5-1df8-4368-889a-ced6852aba47
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: ab97ee8278be567ff46d9b0f762d3c5c6cafa412
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="feature-selection-in-the-team-data-science-process-tdsp"></a>Team Data Science Process’te (TDSP) özellik seçimi
Bu makalede özellik seçimi amaçları açıklar ve makine öğrenme veri geliştirme işleminde rolü örnekleri sağlar. Bu örnekler, Azure Machine Learning Studio'dan çizilir. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Mühendislik ve çeşitli özellikler, takım veri bilimi işlemi (özetlenen TDSP) bir parçası olduğu [takım veri bilimi işlemi nedir?](data-science-process-overview.md). Özellik Mühendisliği ve seçim olan bölümleri **geliştirmek özellikleri** TDSP adımında.

* **özellik Mühendisliği**: Bu işlem veri varolan ham özelliklerinden ek ilgili özellikler oluşturmak ve öğrenme algoritmasında Tahmine dayalı güç artırmak için çalışır.
* **Özellik Seçimi**: Bu işlem özgün veri özelliklerinin anahtar kısmı eğitim sorun boyut azaltmak girişimi seçer.

Normalde **özellik Mühendisliği** ek özellikler oluşturmak için önce uygulanır ve daha sonra **özellik seçimi** adım ilgisiz, artık ya da son derece bağıntılı özellikleri ortadan kaldırmak için gerçekleştirilir.

## <a name="filtering-features-from-your-data---feature-selection"></a>Verilerinizden - özellik seçimi filtreleme özellikleri
Özellik Seçimi sınıflandırma veya regresyon görevler gibi Tahmine dayalı modelleme görevleri için eğitim veri kümesi yapımı için yaygın olarak uygulanan bir işlemdir. Maksimum veri varyans temsil etmek için en az bir özellik kümesi kullanarak boyutlarıyla azaltın özgün veri kümesinden özelliklerinin bir alt kümesi seçmek için belirtilir. Bu alt özellikler kümesini özelliklerdir, daha sonra modeli eğitmek için eklenmesi yalnızca. Özellik Seçimi iki ana amaca hizmet eder.

* İlk olarak, özellik seçimi sıklıkla ortadan kaldırarak ilgisiz, yedekli sınıflandırma doğruluğu artırır veya özellikleri son derece bağıntılı.
* İkinci olarak, model Eğitim işlemini daha verimli hale getirir özellikleri sayısını azaltır. Bu destek vektör makineler gibi eğitmek pahalıdır öğrencileriyle için özellikle önemlidir.

Özellik Seçimi modeli eğitmek için kullanılan veri kümesi özellikleri sayısını azaltmak arama karşın, bu genellikle "boyut azaltma" terimi tarafından başvurmaz. Özellik Seçimi yöntemleri, bunları değiştirmeden veri özgün özelliklerinin bir kısmı ayıklayın.  Boyut azaltma yöntemleri özgün özellikler dönüştürmek ve bu nedenle bunlarda değişiklik tasarlanan özellikleri kullanın. Asıl bileşen analiz, kurallı bağıntı analiz ve tekil değer ayrıştırma boyut azaltma yöntemler örnekleridir.

Diğerleriyle birlikte, yaygın olarak uygulanan bir kategori denetimli bağlamda özellik seçimi yöntemlerin "dayalı filtre özellik seçimi" adı verilir. Her bir özellik ve hedef öznitelik arasındaki bağıntıyı değerlendirerek bu yöntemlerin her bir özellik için bir puan atamak için istatistiksel bir ölçü uygulayın. Özellikleri, ardından tutma veya belirli bir özellik ortadan kaldırmak için eşiği ayarlamanıza yardımcı olması için kullanılabilir puana göre sıralanır. Kişi bağıntı, karşılıklı bilgileri ve Şi squared test bu yöntemlerinde kullanılan istatistiksel ölçümler örneklerindendir.

Azure Machine Learning Studio'daki modüller için özellik seçimi sağlanan vardır. Aşağıdaki çizimde gösterildiği gibi bu modülleri dahil [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] ve [Fisher doğrusal Discriminant analiz] [ fisher-linear-discriminant-analysis].

![Özellik Seçimi örneği](./media/machine-learning-data-science-select-features/feature-Selection.png)

Örneğin, kullanımını düşünün [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] modülü. Kolaylık olması amacıyla, yukarıda özetlenen metni araştırma örneği kullanmaya devam ediyoruz. Biz 256 özellikler kümesi aracılığıyla oluşturduktan sonra bir regresyon modeli oluşturmak istediğinizi varsayalım [özellik karma] [ feature-hashing] modülü ve yanıt değişkeni "Col1" olduğunu ve bir kitap gözden geçirme temsil eder 1 ile 5 arasında değişen derecelendirmeleri. "Puanlama yöntemi özellik" ayarlayarak "Pearson bağıntı", "hedef sütun" olacak şekilde "Col1" ve "istenen özelliklerini"sayısı 50. Ardından Modülü [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] target özniteliği "Col1" ile birlikte 50 özellikleri içeren bir veri kümesi oluşturur. Aşağıdaki şekilde bu deneme ve yeni tanımlanan giriş parametreleri akışı gösterilmektedir.

![Özellik Seçimi örneği](./media/machine-learning-data-science-select-features/feature-Selection1.png)

Sonuçta elde edilen veri kümeleri aşağıdaki şekilde gösterilmiştir. Her bir özelliğin tabanlı kendisi ve hedef öznitelik "Col1" arasında Pearson bağıntı üzerinde puanlanır. Üst puanları özelliklerle tutulur.

![Özellik Seçimi örneği](./media/machine-learning-data-science-select-features/feature-Selection2.png)

Seçilen özelliklerin karşılık gelen puanları aşağıdaki çizimde gösterilmektedir.

![Özellik Seçimi örneği](./media/machine-learning-data-science-select-features/feature-Selection3.png)

Bu uygulama tarafından [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] modülü, 50 dışı özellikler "Col1" hedef değişkeni en bağıntılı özelliklerle sahip oldukları için seçili 256 dayalı Puanlama yöntemi "Pearson bağıntı".

## <a name="conclusion"></a>Sonuç
Özellik Mühendisliği ve özellik seçimi iki yaygın olarak tasarlanmıştır ve seçilen özellikler anahtar bilgileri ayıklamak için deneme verilerde bulunan eğitim işlem verimliliğini artırmak kümesidir. Bunlar ayrıca giriş verileri doğru şekilde sınıflandırmak ve sonuçları ilgi daha yerine tahmin etmek için bu modeller gücü geliştirin. Öğrenme daha pkı'ya tractable yapma özelliği mühendislik ve seçim birleştirebilirsiniz. Bunu arttırma ve ayarlama veya modeli eğitmek için gereken özellikleri sayısının azaltılması yapar. Matematiksel konuşarak, modeli eğitmek için seçilen özellikler en az bağımsız değişkenlerinin veri desenleri açıklar ve sonuçları başarıyla tahmin kümesidir.

Bunu değil her zaman mutlaka özellik Mühendisliği veya özellik seçimi gerçekleştirmek için olduğunu unutmayın. Olup olmadığını veya gerekli olması veya toplama veriler, biz çekme algoritması ve deneme amacı bağlıdır.

<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/

