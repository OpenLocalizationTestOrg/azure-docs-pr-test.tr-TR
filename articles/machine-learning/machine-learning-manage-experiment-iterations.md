---
title: aaaManage yineleme Machine Learning Studio'da deneme | Microsoft Docs
description: "Nasıl toomanage denemeler Azure Machine Learning Studio'da yineleme"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: bd30c048ce063811b1b2de8ce6d71e99ba975713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a>Azure Machine Learning Studio’da deneme yinelemelerini yönetme
Tahmine dayalı analiz modeli geliştirmek olduğu yinelemeli süreç - hello değiştirme gibi çeşitli işlevleri ve denemenizi parametrelerinin memnun olana kadar sonuçlarınız yakınsanır eğitilmiş ve verimli bir model sahip. Anahtar toothis işlem izleme hello çeşitli yinelemelerini deneme parametreleri ve yapılandırmaları olduğu.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Önceki çalışmalarını gözden geçirebilirsiniz denemelerinizi sipariş toochallenge herhangi bir zamanda, yeniden ziyaret ve sonuçta onaylayın ya da önceki varsayımlar daraltın. Bir deneme çalıştırdığınızda, Machine Learning Studio Çalıştır hello veri kümesi, modül ve bağlantı noktası bağlantıları ve parametreleri de dahil olmak üzere geçmişini tutar. Bu geçmiş ayrıca sonuçları, başlatma ve durdurma sürelerini, günlük iletilerini ve yürütme durumu gibi çalışma zamanı bilgileri yakalar. Geri hiçbir zaman tooreview hello uygulanmasına deneme ve Ara sonuçların Geçmişi'de bu çalışır hiçbirini bakabilirsiniz. Deneme toolaunch, önceki bir çalışmasında yeni bir soru ve bulma aşaması çözümleri modelleme, yol toocreating basit, karmaşık veya hatta ensemble üzerinde bile kullanabilirsiniz.

> [!NOTE]
> Önceki bir çalışmasında bir deneme görüntülediğinizde hello deneme sürümünün kilitli ve düzenlenemez. Ancak, bir kopyasını tıklayarak kaydedebileceğiniz **SAVE AS** ve hello kopya için yeni bir ad sağlar. Machine Learning Studio, ardından çalıştırın ve düzenleyebileceği hello yeni kopya, açılır. Bu kopyası denemenizi hello kullanılabilir **DENEMELER** diğer tüm denemelerinizi birlikte listesi.
> 
> 

## <a name="viewing-hello-prior-run"></a>Görüntüleme hello önceki Çalıştır
En az bir kez çalıştır bir deneme açık olduğunda hello deneme yürütülmesi tıklatarak yukarıdaki hello görüntüleyebilirsiniz **önceki Çalıştır** hello Özellikler bölmesinde.

Örneğin, bir deneme oluşturmak ve 11: 23'te bu sürümlerini çalıştıran varsayalım 11:42 ve 11:55. Merhaba son çalışması hello deneme (11:55) açın ve'ı tıklatırsanız **önceki Çalıştır**, 11:42 çalıştırdığınız hello sürümü açılır.

## <a name="viewing-hello-run-history"></a>Görüntüleme hello çalıştırma geçmişi
Merhaba önceki çalışmalarını deneme tıklatarak görüntüleyebileceğiniz **çalıştırma geçmişini görüntüle** açık bir deney olarak.

Örneğin, hello ile bir deneme oluşturduğunuzu varsayalım [doğrusal regresyon] [ linear-regression] modülü ve tooobserve hello etkisini, hello değerini değiştirmek istiyorsanız **öğrenme oranı** üzerinde Deneme sonuçlarınızı. Hello denemeyi birden çok kez bu parametre için farklı değerler ile aşağıdaki gibi çalıştırın:

| Öğrenme hızı değeri | Çalıştırma başlangıç zamanı |
| --- | --- |
| 0.1 |11/9/2014 4:18:58 pm |
| 0.2 |11/9/2014 4:24:33 pm |
| 0.4 |11/9/2014 4:28:36 pm |
| 0.5 |11/9/2014 4:33:31 pm |

Tıklatırsanız **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE**, bu çalıştırır listesi Bkz:

![Örnek çalıştırma geçmişi][runhistory]

Herhangi bir anlık görüntüsünü hello denemeler, çalıştırdığınız hello aynı anda bu çalıştırır tooview birini tıklatın. Merhaba yapılandırma, parametre değerleri, açıklamalar ve sonuçları tüm korunan toogive olan, eksiksiz bir kaydı denemenizi bu çalışması ile.

> [!TIP]
> toodocument, hello deneme yinelemelerini her çalıştırdığınızda hello başlık değiştirebilirsiniz, hello güncelleştirebilirsiniz **Özet** hello hello Özellikler bölmesinde denemeler ve ekleme veya güncelleştirme tek tek modülleri açıklamaları toorecord değişikliklerinizi. Merhaba başlık, özetini ve modül açıklamaları hello deneme her yürütülmesi kaydedilir.
> 
> 

Merhaba denemeler Hello listesi **DENEMELER** sekmesi Machine Learning Studio'da bir denemeyi en son sürümünü hello her zaman görüntüler. Merhaba deneme, önceki bir çalışmasında açarsanız (kullanarak **önceki Çalıştır** veya **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE**), tıklatarak toohello taslak sürüm dönebilirsiniz **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE** ve seçme Merhaba sahip yineleme bir **durumu** , **düzenlenebilir**.

## <a name="iterating-on-a-previous-run"></a>Önceki bir çalışmasında üzerinde yineleme
Tıkladığınızda **önceki Çalıştır** veya **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE** ve önceki bir çalışmasında açın, tamamlanmış bir deneme salt okunur modunda görüntüleyebilirsiniz.

Toobegin denemenizi hello şekilde yapılandırdığınız, bir önceki çalıştırma için başlayarak, bir yinelemeye istiyorsanız açma hello çalıştırın ve tıklayarak bunu yapabilirsiniz **SAVE AS**. Yeni bir başlık, boş bir çalıştırma geçmişi ve tüm hello bileşenleri ve parametre değerlerini önceki hello çalıştırmak ile yeni bir deneme oluşturur. Bu yeni bir deneme hello listelenen **DENEMELERİNİ** hello Machine Learning Studio giriş sayfasının ve sekmede değiştirebilirsiniz ve bu, yeni bir başlatma run denemenizi bu yinelemesi geçmişini. 

Örneğin, hello deneme çalıştırma geçmişi hello önceki bölümde gösterilen olduğunu varsayalım. Merhaba neler tooobserve istediğiniz **öğrenme oranı** parametresi too0.4 ve hello için farklı değerler deneyin **eğitim dönemlerinde sayısı** parametresi.

1. Tıklatın **ÇALIŞTIRMA GEÇMİŞİNİ GÖRÜNTÜLE** ve 4:28:36 (hangi ayarladığınız hello parametre değeri too0.4) pm çalıştırdığınız hello deneme hello yinelemesi açın.
2. Tıklatın **SAVE AS**.
3. Yeni bir başlık girin ve hello tıklayın **Tamam** onay işareti. Merhaba deneme yeni bir kopyası oluşturulur.
4. Merhaba değiştirme **eğitim dönemlerinde sayısı** parametresi.
5. Tıklatın **çalıştırmak**.

Şimdi toomodify devam etmek ve yeni bir çalıştırma geçmişi toorecord çalışmanızı oluşturma denemenizi, bu sürümü çalıştırın.

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
