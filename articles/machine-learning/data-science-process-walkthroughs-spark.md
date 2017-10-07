---
title: "Azure üzerinde PySpark ve Scala kullanarak aaaHDInsight Spark izlenecek | Microsoft Docs"
description: "Hello yol hello takım veri bilimi işlem örnekleri PySpark ve Scala bir Azure Hdınsight Spark toodo Tahmine dayalı analizleri kullanır."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: f8b41a8cae414586570761ba4b4eb4c239cbb981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-spark-data-science-walkthroughs-using-pyspark-and-scala-on-azure"></a>Hdınsight Spark veri bilimi Azure üzerinde PySpark ve Scala kullanarak izlenecek yollar

Bu izlenecek bir Azure Spark küme toodo Tahmine dayalı analizleri PySpark ve Scala kullanın. Bunlar hello takım veri bilimi işlemi özetlenen hello adımları izleyin. Merhaba takım veri bilimi işlemine genel bakış için bkz: [veri bilimi işlemi](data-science-process-overview.md). Hdınsight'ta Spark genel bakış için bkz: [giriş tooSpark hdınsight'ta](../hdinsight/hdinsight-apache-spark-overview.md).

Merhaba takım veri bilimi işlemi yürütme ek veri bilimi talimatları hello tarafından gruplandırılır **platform** kullandıkları: 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]

## <a name="predict-taxi-tips-using-pyspark-on-azure-spark"></a>PySpark Azure Spark kullanarak ücreti ipuçları tahmin etme

Merhaba [Azure hdınsight'ta Spark kullanma](machine-learning-data-science-spark-overview.md) izlenecek yol bir ipucu Ücretli ve tutarlar hello aralığı beklenen Ücretli toobe olup olmadığını New York taksiler toopredict verileri kullanır. Senaryo kullanarak hello takım veri bilimi işlemi kullanan bir [Azure Hdınsight Spark küme](https://azure.microsoft.com/services/hdinsight/) toostore, keşfetme, özellik hello genel kullanıma açık NYC ücreti seyahat mühendislik verileri ve dataset masrafları. Bu genel bakış konusunun, bir Hdınsight Spark kümesi ve hello Jupyter PySpark not defterlerini hello kılavuzun hello kalan kullanılan ayarlar. Bu dizüstü bilgisayarlar şunları nasıl yapacağınızı tooexplore veri ve ardından nasıl toocreate ve modelleri için kullanabilir. Gelişmiş Veri keşfi ve not defteri gösterir nasıl modelleme hello tooinclude çapraz doğrulama, hyper-parametre Süpürme ve model değerlendirme.

### <a name="data-exploration-and-modeling-with-spark"></a>Veri keşfi ve Spark modelleme 
Hello dataset keşfetmek ve oluşturmak, Puanlama ve hello makine öğrenimi modellerini hello aracılığıyla çalışma değerlendirme [hello Spark Mllib'i araç seti ile veri için ikili sınıflandırma ve regresyon model oluşturma](machine-learning-data-science-spark-data-exploration-modeling.md) konu.

### <a name="model-consumption"></a>Model tüketim
Bu konuda, tooscore hello sınıflandırma ve regresyon modeli oluşturulan nasıl toolearn bkz [puanı ve Spark yerleşik makine öğrenimi modellerini değerlendirme](machine-learning-data-science-spark-model-consumption.md).

### <a name="cross-validation-and-hyperparameter-sweeping"></a>Çapraz doğrulama ve hyperparameter Süpürme
Bkz: [veri keşfi ve modelleme Spark ile Gelişmiş](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) modelleri nasıl olabilir üzerinde çapraz doğrulama ve parametre hyper Süpürme kullanılarak eğitilmiş.


## <a name="predict-taxi-tips-using-scala-on-azure-spark"></a>Azure Spark Scala kullanarak ücreti ipuçları tahmin etme

Merhaba [Azure üzerinde Spark ile kullanım Scala](machine-learning-data-science-process-scala-walkthrough.md) izlenecek kullandığını New York taksiler toopredict verilerden bir ipucu Ücretli ve tutarlar hello aralığı beklenen Ücretli toobe. Bunu nasıl toouse Scala denetimli makine öğrenimi görevlerini hello Spark machine learning kitaplığı (Mllib'i) ve SparkML için bir Azure Hdınsight Spark kümesinde paketleri gösterir. Merhaba oluşturduğunu hello görevlerinde anlatılmaktadır [veri bilimi işlemi](http://aka.ms/datascienceprocess): veri alımı ve keşfi, görselleştirme, özellik Mühendisliği, model ve model tüketim. Merhaba modellerinin oluşturulması Lojistik ve doğrusal regresyon, rastgele ormanları ve gradyan boosted ağaçları içerir.


## <a name="next-steps"></a>Sonraki adımlar

Merhaba takım veri bilimi işlemi oluşturan hello anahtar bileşenleri bir tartışma için bkz: [takım veri bilimi işlemine genel bakış](data-science-process-overview.md).

Veri bilimi projelerinizi toostructure kullanabileceğiniz hello takım veri bilimi işlemi yaşam döngüsünün bir tartışma için bkz [takım veri bilimi işlemi yaşam döngüsü](data-science-process-lifecycle.md). Merhaba yaşam döngüsü hello adımları, bunlar çalıştırıldığında izleyen projeleri genellikle başlangıç toofinish özetlenmektedir. 

