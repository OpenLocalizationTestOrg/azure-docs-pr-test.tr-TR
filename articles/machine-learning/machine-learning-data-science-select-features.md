---
title: "Merhaba takım veri bilimi işlemi aaaFeature seçimde | Microsoft Docs"
description: "Özellik Seçimi Hello amacını açıklayan ve machine learning hello veri geliştirme sürecinin içindeki rollerine örnekler sağlar."
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
ms.openlocfilehash: 54af93c83e4cc6a3670b3ad62490e0f74082b4ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="feature-selection-in-hello-team-data-science-process-tdsp"></a>Özellik Seçimi'nde hello takım veri bilimi işlem (TDSP)
Bu makalede özellik seçimi hello amaçları açıklar ve makine öğrenme hello veri geliştirme sürecinde rolü örnekleri sağlar. Bu örnekler, Azure Machine Learning Studio'dan çizilir. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Mühendislik hello ve çeşitli özellikler hello takım veri bilimi işlem (TDSP) özetlenen bir parçası olan [hello takım veri bilimi işlemi nedir?](data-science-process-overview.md). Özellik Mühendisliği ve seçim olan hello bölümlerini **geliştirmek özellikleri** hello TDSP adımında.

* **özellik Mühendisliği**: Bu işlem toocreate ek ilgili özellikleri özelliklerinden hello varolan ham hello veri ve tooincrease Tahmine dayalı güç toohello öğrenme algoritmasını çalışır.
* **Özellik Seçimi**: Bu işlem bir girişim tooreduce hello boyut hello eğitim sorununun içinde hello anahtar özelliklerin alt kümesini özgün veri seçer.

Normalde **özellik Mühendisliği** uygulanan ilk toogenerate ek özellikler ve hello **özellik seçimi** adımdır gerçekleştirilen tooeliminate ilgisiz, artık ya da son derece bağıntılı Özellikler.

## <a name="filtering-features-from-your-data---feature-selection"></a>Verilerinizden - özellik seçimi filtreleme özellikleri
Özellik Seçimi sınıflandırma veya regresyon görevler gibi Tahmine dayalı modelleme görevleri için eğitim veri kümesi hello yapımı için yaygın olarak uygulanan bir işlemdir. Merhaba, tooselect hello verilerde özellikleri toorepresent hello maksimum farkı en az sayıda kullanarak boyutlarıyla azaltın hello özelliklerinin hello özgün veri kümesinden bir alt kümesi hedeftir. Bu alt özellikler kümesidir, ardından tootrain hello modeli hello yalnızca özellikleri toobe dahil. Özellik Seçimi iki ana amaca hizmet eder.

* İlk olarak, özellik seçimi sıklıkla ortadan kaldırarak ilgisiz, yedekli sınıflandırma doğruluğu artırır veya özellikleri son derece bağıntılı.
* İkinci olarak, hello model Eğitim işlemini daha verimli hale getirir özellikleri sayısı azalır. Bu destek vektör makineleri gibi pahalı tootrain olan öğrencileriyle için özellikle önemlidir.

Özellik Seçimi tooreduce hello birçok özellik hello kullanılan dataset tootrain hello modelinde arama olsa da, genellikle başvurulan tooby hello terimi "boyut azaltma" değil. Özellik Seçimi yöntemleri, bunları değiştirmeden hello verilerdeki özgün özelliklerinin bir kısmı ayıklayın.  Boyut azaltma yöntemleri hello özgün özellikler dönüştürmek ve bu nedenle bunlarda değişiklik tasarlanan özellikleri kullanın. Asıl bileşen analiz, kurallı bağıntı analiz ve tekil değer ayrıştırma boyut azaltma yöntemler örnekleridir.

Diğerleriyle birlikte, yaygın olarak uygulanan bir kategori denetimli bağlamda özellik seçimi yöntemlerin "dayalı filtre özellik seçimi" adı verilir. Her özellik ve hello target özniteliği arasında Hello bağıntı değerlendirerek istatistiksel ölçü tooassign bir puan tooeach özelliği bu yöntemleri uygulayın. Merhaba özellikleri sonra tutma veya belirli bir özellik ortadan kaldırmak için kullanılan toohelp ayarlanan hello eşiği olabilir hello puana göre sıralanır. Kişi bağıntı, karşılıklı bilgileri ve hello Şi squared test hello istatistiksel ölçümler bu yöntemlerinde kullanılan örneklerindendir.

Azure Machine Learning Studio'daki modüller için özellik seçimi sağlanan vardır. Hello aşağıdaki şekilde gösterildiği gibi bu modülleri dahil [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] ve [Fisher doğrusal Discriminant analiz] [ fisher-linear-discriminant-analysis].

![Özellik Seçimi örneği](./media/machine-learning-data-science-select-features/feature-Selection.png)

Örneğin, hello hello kullanımını göz önünde bulundurun [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] modülü. Kolaylık Hello amaçla toouse hello metni araştırma örneği yukarıda özetlenen devam ediyoruz. Biz 256 özellikler kümesi sonra bir regresyon modeli hello oluşturulan toobuild istediğinizi varsayalım [özellik karma] [ feature-hashing] modülü ve bu hello yanıt değişken hello "Col1" ve kitap temsil eder 1 too5 arasında değişen derecelendirmelerini gözden geçirin. "Özellik yöntemi Puanlama" toobe "Pearson bağıntı" ayarlayarak, "Hedef sütun" toobe "Col1" ve "İstenen özelliklerini sayısı" too50 hello hello. Ardından hello Modülü [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] hello target özniteliği "Col1" ile birlikte 50 özellikleri içeren bir veri kümesi oluşturur. Merhaba aşağıdakileri gösterir hello akışını bu deneme şekil ve yeni tanımlanan giriş parametreleri hello.

![Özellik Seçimi örneği](./media/machine-learning-data-science-select-features/feature-Selection1.png)

Merhaba aşağıdaki şekilde hello ortaya çıkan veri kümeleri gösterilmektedir. Her bir özelliğin hello kendisi arasında Pearson bağıntı üzerinde göre puanlanır ve hedef özniteliği "Col1" Merhaba. üst puanları Hello özelliklerle tutulur.

![Özellik Seçimi örneği](./media/machine-learning-data-science-select-features/feature-Selection2.png)

Seçili hello özelliklerinin Hello karşılık gelen puanları hello aşağıdaki şekilde gösterilmiştir.

![Özellik Seçimi örneği](./media/machine-learning-data-science-select-features/feature-Selection3.png)

Bu uygulama tarafından [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] modülü, 50 dışında özellikleri seçili sahip hello çünkü çoğu bağıntılı özellik hello hedef değişkeni "Col1" ile 256 dayalı hello Puanlama yöntem "Pearson bağıntı".

## <a name="conclusion"></a>Sonuç
Özellik Mühendisliği ve özellik seçimi iki yaygın olarak tasarlanmıştır ve seçilen özellikler tooextract hello anahtar bilgileri hello verilerde bulunan çalışır işleminin eğitim hello hello verimliliğini artırmak kümesidir. Bunlar ayrıca bu modeller tooclassify hello giriş verisi hello gücünü doğru şekilde artırmak ve toopredict sonuçlarını ilgi daha fazla yerine. Ayrıca özellik mühendislik ve seçim toomake hello öğrenme daha pkı'ya tractable birleştirebilirsiniz. Bunu geliştirme tarafından yapar ve sonra Özellikler hello sayısının azaltılması toocalibrate veya train model gerekli. Matematiksel konuşarak hello özellikleri seçili tootrain hello modeli hello veri hello düzenleri açıklayabilir ve sonuçları başarıyla tahmin bağımsız değişkenlerini en az sayıda vardır.

Bu her zaman mutlaka tooperform özellik Mühendisliği veya özellik seçimi olmadığını unutmayın. Olup olmadığını veya gerekli biz sahip veya, biz çekme, hello algoritması toplamak ve hello deneme amacı hello hello verilere bağlıdır.

<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/

