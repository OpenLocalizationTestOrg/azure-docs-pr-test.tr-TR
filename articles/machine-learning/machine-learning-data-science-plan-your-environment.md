---
title: "aaaIdentify senaryoları ve Azure - Analytics'i işleminizi planlama | Microsoft Docs"
description: "Gelişmiş analitikler için bir dizi anahtar soru dikkate alarak planlayın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 421520dd-7728-4d29-889c-ebe6a0a6fb07
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: e445973be0d020a4f9949e5c9d8554fbbd4b515f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooidentify-scenarios-and-plan-for-advanced-analytics-data-processing"></a>Nasıl tooidentify senaryoları planlama analytics veri işleme Gelişmiş ve
Hangi kaynaklara bir ortam toodo ayarı Gelişmiş analitik veri kümesi üzerinde işleme tooinclude planlama yapmalıyım? Bu makalede bir dizi hello görevleri ve ilgili kaynakları tanımlanmasına yardımcı olacak soruları tooask senaryonuz önerir. Tahmine dayalı analiz için üst düzey adımları Hello düzenini özetlenen içinde [hello takım veri bilimi işlem (TDSP) nedir?](data-science-process-overview.md). Bu adımların her biri belirli kaynaklar hello görevleri ilgili tooyour belirli senaryo için gerektirir. önemli sorular tooidentify, senaryo sorunu veri Lojistik, özellikleri, hello kalitesini hello veri kümeleri ve hello araçları ve toodo hello analiz tercih dilleri hello.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="logistic-questions-data-locations-and-movement"></a>Lojistik sorular: veri konumları ve taşıma
Merhaba Lojistik soruları ilgilendiren hello hello konumunu **veri kaynağı**, hello **hedef** Azure ve hello veri taşımayı gereksinimleri, hello zamanlama, tutar ve kaynaklar dahil söz konusu. Merhaba veri hello analytics işlemi sırasında birkaç kez taşınmış toobe gerekebilir. Yaygın bir senaryo toomove yerel depolama Azure ile ilgili bazı forma, ardından Machine Learning Studio uygulamasına verilerdir.

1. **Veri kaynağınızı nedir?** Yerel veya hello bulutta mı? Örneğin:
   
   * Merhaba veriler bir HTTP adresi genel olarak kullanılabilir.
   * Merhaba verileri yerel/ağ dosya konumunda yer alıyor.
   * Merhaba, bir SQL Server veritabanında verilerdir.
   * Merhaba veriler bir Azure depolama kapsayıcısında depolanır
2. **Hello Azure hedef nedir?** Burada, toobe işleme veya modelleme gerekiyor mu? Örneğin:
   
   * Azure Blob Depolama
   * SQL Azure veritabanı
   * Azure VM’lerde SQL Server
   * Hdınsight (Hadoop Azure üzerinde) veya Hive tabloları
   * Azure Machine Learning
   * Edilebilme Azure sanal sabit diskler.
3. **Nasıl toomove hello veri mısınız?**  aşağıdaki konularda hello hello yordamları ve kaynakları kullanılabilir tooingest veya yük verisine çeşitli farklı depolama ve ortamlar işleme ana hatlarıyla.
   
   * [Analiz için depolama ortamlara veri yükleme](machine-learning-data-science-ingest-data.md)
   * [Çeşitli veri kaynaklarından Azure Machine Learning Studio'da eğitim verilerinizi almak](machine-learning-data-science-import-data.md).
4. **Merhaba verilerinin düzenli bir zamanlamaya göre taşınmış veya geçiş sırasında değiştirilmiş toobe gerekiyor mu?** Veri gereksinimlerini toobe sürekli geçişi olduğunda, hem şirket içi erişir ve bulut kaynaklarına eklendiyse veya hello veri işlem yapılan işlem veya değiştiren toobe gerekir ya da iş mantığı sahip özellikle karma bir senaryoda, Azure veri fabrikası (ADF) kullanmayı düşünün Geçirilmekte olan hello indirmelere içinde tooit eklendi. Daha fazla bilgi için bkz: [gelen bir şirket içi SQL server tooSQL Azure Azure Data Factory ile veri taşıma](machine-learning-data-science-move-sql-azure-adf.md)
5. **Taşınan toobe tooAzure hello verilerin ne kadar mi?** Çok büyük veri kümeleri belirli ortamları hello depolama kapasitesini aşabilir. Örneğin, boyutu sınırları hello tartışma için Machine Learning Studio hello sonraki bölümde bakın. Bu gibi durumlarda hello veri örneği hello Çözümleme sırasında kullanılabilir. Bir veri kümesinin nasıl toodown örnek çeşitli Azure ortamlarda Ayrıntılar için bkz [örnek hello takım veri bilimi işlemi verileri](machine-learning-data-science-sample-data.md).

## <a name="data-characteristics-questions-type-format-and-size"></a>Veri özellikleri soruları: türünü, biçimi ve boyutu
Bu soruları anahtar tooplanning, depolama ve her biri uygun toovarious ortamlar, işleme, veri türleri ve her biri bazı kısıtlamalar vardır.

1. **Başlangıç veri türleri nelerdir?** Örneğin:
   
   * Sayısal
   * Kategorik
   * Dizeler
   * İkili
2. **Verilerinizin nasıl biçimlendirilmiş?** Örneğin:
   
   * Virgülle ayrılmış (CSV) veya sekmeyle ayrılmış (TSV) düz dosyalar
   * Sıkıştırılmış veya sıkıştırılmamış
   * Azure BLOB'ları
   * Hadoop Hive tabloları
   * SQL Server tabloları
3. **Verilerinizi büyüklüğü nedir?**
   
   * Küçük: 2 GB'tan daha az
   * Orta: 2GB ve 10GB'değerinden büyük
   * Büyük: 10GB daha büyük

Hello Azure Machine Learning Studio ortamı örneğin alın:

* Merhaba veri biçimleri ve Azure Machine Learning Studio tarafından desteklenen türleri listesi için bkz: [veri biçimleri ve desteklenen veri türlerini](machine-learning-data-science-import-data.md#data-formats-and-data-types-supported) bölümü.
* Hello Azure Machine Learning Studio için veri sınırlamaları hakkında daha fazla bilgi için bkz: **nasıl büyük hello veri kümesi modüllerim da olabilir?** bölümünü [alma ve Machine Learning için verileri dışarı aktarma](machine-learning-faq.md#machine-learning-studio-questions)

Merhaba analytics işleminde kullanılan diğer Azure hizmetleriyle hello sınırlamaları hakkında daha fazla bilgi için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).

## <a name="data-quality-questions-exploration-and-pre-processing"></a>Veri Kalitesi soruları: araştırması ve ön işleme
1. **Verileriniz hakkında ne biliyor musunuz?** Toogain bir anlayın gerektiğinde veri temel özellikleri keşfedin. Ne düzenleri veya sergiler, eğilimlerin aykırı değerlerini nedir veya kaç değerleri eksik. Bu adım, hello en uygun özellikleri önermek veya analizini yazın varsayımlar formulating ve ek veri toplama için planları formulating gerekli ön işleme hello kapsamını belirlemek için önemlidir. Açıklayıcı istatistikleri hesaplama ve görselleştirmeleri çizme veri İnceleme için yararlı tekniklerle aynıdır. Nasıl tooexplore bir veri kümesi çeşitli Azure ortamlarda, bkz. Ayrıntılar için [hello takım veri bilimi işlemi keşfedin](machine-learning-data-science-explore-data.md).
2. **Merhaba verilerin önceden işlenmesi veya temizleme gerektiriyor mu?**
   Ön işleme ve veri temizleme dataset machine learning için etkili bir şekilde kullanılabilmesi için önce genellikle gerçekleştirilmesi gereken önemli görevlerdir. Ham verileri gürültülü ve güvenilmeyen görülür ve değerleri eksik olabilir. Bu tür veriler için modelleme kullanarak yanıltıcı sonuçlara yol açabilir. Bir açıklama için bkz: [görevleri tooprepare veri Gelişmiş machine learning için](machine-learning-data-science-prepare-data.md).

## <a name="tools-and-languages-questions"></a>Araçlar ve dilleri soruları
Çok sayıda veya bağlı olarak hangi dilleri ve geliştirme ortamları veya Araçlar, gereken en conformable kullanarak burada seçenekleri vardır.

1. **Dilleri neler toouse çözümleme için tercih ettiğiniz?**  
   
   * R
   * Python
   * SQL
2. **Hangi Araçlar veri analizi için kullanmalısınız?**
   
   * [Microsoft Azure Powershell](/powershell/azure/overview) -komut dosyası dili tooadminister Azure kaynaklarınızı bir komut dosyası dili kullanılır.
   * [Azure Machine Learning Studio](machine-learning-what-is-ml-studio.md)
   * [Devir analizi](http://www.revolutionanalytics.com/revolution-r-open)
   * [Rstudio'dan](http://www.rstudio.com)
   * [Visual Studio için Python Araçları](http://microsoft.github.io/PTVS/)
   * [Anaconda](https://www.continuum.io/why-anaconda)
   * [Jupyter Not Defterleri](http://jupyter.org/)
   * [Microsoft Power BI](http://powerbi.microsoft.com)

## <a name="identify-your-advanced-analytics-scenario"></a>Gelişmiş analizler senaryonuz tanımlayın
Hello önceki bölümdeki hello sorulara verdiğiniz yanıtlara verdikten sonra en iyi hangi senaryonun durumunuza uygun hazır toodetermine demektir. Merhaba örnek senaryolar özetlenen içinde [senaryoları Azure Machine Learning, gelişmiş analizler için](machine-learning-data-science-plan-sample-scenarios.md).

