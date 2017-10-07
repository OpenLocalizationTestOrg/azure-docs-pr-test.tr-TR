---
title: "aaaWhat takım veri bilimi işlemi mi?  | Microsoft Belgeleri"
description: "Merhaba takım veri bilimi işlemi, gelişmiş analizler yararlanan akıllı uygulamaları oluşturmak için sistematik bir yöntemdir."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a098aa2e-fd79-4543-8e15-9aae9d8b3ee6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: bradsev
ROBOTS: NOINDEX
redirect_url: data-science-process-overview
redirect_document_id: True
ms.openlocfilehash: 57187be9c884389c13c226eab74aff137f5514a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-team-data-science-process-tdsp"></a>Merhaba takım veri bilimi işlem (TDSP) nedir?
Merhaba [takım veri bilimi işlem (TDSP)](data-science-process-overview.md) sağlayan veri bilimcilerine toocollaborate ekiplerin etkili bir şekilde hello tam yaşam döngüsü gereken etkinliklerin toobuilding akıllı uygulamaları sistematik bir yaklaşım sağlar tooturn ürünler halinde bu uygulamalar. Merhaba TDSP özetlenmektedir sağlamak adımların sırasını **Kılavuzu** nasıl hello araçlarını Kur toodefine hello sorun ve gerekli ortam, ilgili verileri çözümlemek, yapı ve Tahmine dayalı modelleri değerlendirmek ve bu modellerinde dağıtma kuruluş uygulamaları. 

Merhaba adımlar şunlardır **takım veri bilimi işlemi**:  

![CAP iş akışı](./media/machine-learning-data-science-the-cortana-analytics-process/CAP-workflow.png)

Merhaba işlem **yinelemeli**:, yeni anlama ve varolan hello veya düzeltmeler hello modelinde dönüşmesi ve daha önce hello sırayla tamamlandı adımları denetçiye yeni biçim gerektirir. Var olan Kuruluş geliştirme ve işlemleri planlama proje **kolayca uyarlanmış** toowork hello adımları TDSP tanımlı dizisi ile. 

Merhaba hello işleminde adımları tasarımını ve hello bağlı [TDSP öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) ve aşağıda açıklanmıştır.  

## <a name="preparation-steps"></a>Hazırlık adımları
## <a name="p1-plan-hello-analytics-project"></a>P1. Merhaba analytics proje planlama
Analytics projesinde iş hedeflerine ve sorunları tanımlayarak başlatın. Cinsinden belirtilen **iş gereksinimlerini**. Bu adımın merkezi bir hedefi analiz gereksinimlerini toopredict toosatisfy bu gereksinimleri hello (Satış tahmin veya bir sipariş olma olasılığını sahte, örneğin hello) tooidentify hello anahtar iş değişkenleri ' dir. Ek planlama durumda genellikle temel toodevelop hello anlaşılması **veri kaynakları** tooaddress hello proje analitik açısından amaçlarını hello. Seyrek değil, örneğin, varolan sistemleri toocollect gerekir ve veri tooaddress ek tür oturum toofind sorun hello ve hello proje hedeflerinize ulaşmak. Yönergeler için bkz [ortamınız hello takım veri bilimi işlemi için planlama](machine-learning-data-science-plan-your-environment.md) ve [senaryoları Azure Machine Learning, gelişmiş analizler için](machine-learning-data-science-plan-sample-scenarios.md).  

## <a name="p2-setup-analytics-environment"></a>P2. Analiz ortamını ayarlama
Merhaba takım veri bilimi işlemi analytics ortam çeşitli bileşenleri içerir: 

* **Veri çalışma alanları** hello veri analizi ve modelleme, için hazırlanan burada 
* bir **işleme altyapısı** önceden işlenmesi, keşfetme ve hello veri modelleme
* bir **çalışma zamanı altyapısında** toooperationalize analitik modelleri hello ve hello modelleri kullanma hello akıllı istemci uygulamaları çalıştırın.  

toobe kurulumun hello analytics altyapısı genellikle çekirdek işletim sistemlerinden ayrı bir ortamda bir parçasıdır. Ancak genellikle veri hello kuruluş içinde birden çok sistemlerden yanı sıra kaynakları dış toohello şirketten yararlanır. bir şirket içi Kurulum ya da, karma bir hello iki veya Hello analytics altyapı tamamen bulut tabanlı olabilir. Seçenekler için bkz: [hello takım veri bilimi işlemi kullanmak için veri bilimi ortamları ayarlama](machine-learning-data-science-environment-setup.md).

## <a name="analytics-steps"></a>Analytics adımlar:
## <a name="1-ingest-data-into-hello-analytical-environment"></a>1. Merhaba analitik ortamına veri alma
Merhaba ilk adımı toobring hello ilgili çeşitli kaynaklardan gelen içinde ya da hello veri işleneceği analitik ortamlara dış hello Enterprise verilerdir. Merhaba **biçimi** Merhaba veri kaynağında hello hedefi tarafından gerekli hello biçimi farklı olabilir. Bu nedenle bazı veri dönüştürme hello alım araçları tarafından yapılan toobe da sahip olabilirsiniz. Seçenekler için bkz: [analiz için depolama ortamlara veri yükleme](machine-learning-data-science-ingest-data.md)

Toplama toohello ilk alımında veri, birçok akıllı gerekli toorefresh hello verileri düzenli olarak devam eden öğrenme işleminin bir parçası olarak uygulamalardır. Bu kurulum tarafından yapılabilir bir **veri ardışık** veya iş akışı. Bu hello yinelemeli işleminin bir parçası yeniden oluşturma ve hello akıllı uygulama hello çözümü tarafından kullanılan hello analitik modelleri yeniden değerlendirme içeren hello parçası oluşturur. Örneğin bkz [bir şirket içi SQL server tooSQL Azure Data Factory ile Azure gelen veri taşıma](machine-learning-data-science-move-sql-azure-adf.md).

## <a name="2-explore-and-pre-process-data"></a>2. Veriyi inceleme ve ön işlemden geçirme
Merhaba sonraki adımdır tooobtain hello veri daha derin bir anlayış incelenerek kendi **Özet istatistikleri** , ilişkileri ve böyle teknikleri kullanarak **görselleştirme**. Bu aynı zamanda olup burada, sorunlar **veri kalitesini** ve eksik değerleri, veri türü uyuşmazlığı ve tutarsız veri ilişkileri gibi bütünlüğü işlenir. Ön işleme dönüşümler hello ham verileri daha fazla analiz önce kullanılan tooclean olan ve modelleme yer alabilir. Bir açıklama için bkz: [görevleri tooprepare veri Gelişmiş machine learning için](machine-learning-data-science-prepare-data.md).

## <a name="3-develop-features"></a>3. Özellikler geliştirin
Etki alanı uzmanlar işbirliğiyle veri bilimcilerine yakalama hello belirgin özellikleri hello veri kümesi ve kullanılan toopredict hello anahtar iş değişkenleri planlama sırasında tanımlanan en iyi olabilir hello özellikleri tanımlamanız gerekir. Bu yeni özellikler, var olan verilerden türetilmiş veya toplanan ek veri toobe gerektirebilir. Bu işlem olarak bilinir **özellik Mühendisliği** ve hello etkili Tahmine dayalı analiz sistem oluşturmanın temel adımları biridir. Bu adım, etki alanı uzmanlık ve hello Öngörüler hello veri araştırması adımından elde yaratıcı bir birleşimini gerektirir. Yönergeler için bkz [özellik Mühendisliği hello takım veri bilimi işlemi içinde](machine-learning-data-science-create-features.md).

## <a name="4-create-predictive-models"></a>4. Tahmine dayalı modeller oluşturma
Veri bilimcilerine toopredict hello anahtar değişkenleri planlama adımı temizlenmiş verileri kullanarak ve featurized hello tanımlanan hello iş gereksinimleri tarafından tanımlanan analitik modelleri oluşturabilir. Machine learning sistemlerini destekleyen birden çok **algoritmaları modelleme** durumlarda uygulanabilir tooa çeşitli olan. Yönergeler için bkz [nasıl toochoose algoritmaları takım Azure Machine Learning için](machine-learning-algorithm-choice.md).

Veri bilimcilerine kendi tahmin görev için en uygun model hello seçmeniz gerekir ve birden fazla modeli sonuçlarından birleştirilmiş toobe tooobtain hello en iyi sonuçlar almanız seyrek değil. Merhaba modelleme için giriş verileri genellikle rastgele üç kısma ayrılmıştır:

* bir eğitim veri kümesi 
* bir doğrulama veri kümesi 
* bir sınama veri kümesi 

Merhaba modelleri hello kullanarak yerleşiktir **eğitim veri kümesi**. Merhaba modelleri (parametrelerle olarak ayarlanmış) en iyi birleşimi çalıştırarak hello modeller ve hello hello tahmin hataları ölçme seçili **doğrulama veri kümesi**. Son olarak hello **sınama veri kümesi** seçilen hello model kullanılan tootrain değildi bağımsız veri üzerinde kullanılan tooevaluate hello performansı veya hello modeli doğrulama.  Yordamlar için bkz: [nasıl tooevaluate model Azure Machine Learning performans](machine-learning-evaluate-model-performance.md).

## <a name="5-deploy-and-consume-models"></a>5. Dağıtma ve modelleri kullanma
Biz de gerçekleştirmek modelleri kümesi oluşturduktan sonra olabilirler **kullanıma hazır hale getirilmiş** diğer uygulamaları tooconsume için. Merhaba iş gereksinimlerine bağlı olarak, ya da tahminleri yapılan **gerçek zamanlı** veya bir **toplu** temel. kullanıma hazır hale getirilmiş toobe hello modelleri ile kullanıma sunulan toobe sahip bir **API arabirimini açın** , kolayca tüketilen çeşitli uygulamalardan gibi çevrimiçi Web sitesi, elektronik tablolar, panolar veya iş ve arka uç uygulamalarının satır. Bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="summary-and-next-steps"></a>Özet ve sonraki adımlar
Hello [takım veri bilimi işlemi](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) tekrarlayan adımlar dizisi olarak Modellenen, **kılavuzluk** hello görevlerde gerekli toouse analytics toobuild akıllı uygulamaları Gelişmiş. Her adım toouse çeşitli Microsoft teknolojileri toocomplete hello görevleri nasıl açıklanan ayrıntıları da sağlar. 

TDSP belirli türlerdeki belgenizdeki değil sırada **belgelerine** yapılar hello veri keşfi, model oluşturma ve değerlendirme en iyi yöntem toodocument hello sonuçlar olduğunu ve toosave hello ilgili kod çözümleme hello şekilde gerekli olduğunda yinelendiğinde. Bu da benzer veri ve tahmin görevleri içeren diğer uygulamalar üzerinde çalışırken analytics iş hello kullanılmasını sağlar.

Tam için hello işlemdeki tüm hello adımları gösteren uçtan uca talimatlara **belirli senaryolar** de sağlanır. , Örneğin bakın:

* [eylemin Hello takım veri bilimi işlemi: SQL Server kullanma](machine-learning-data-science-process-sql-walkthrough.md)
* [eylemin Hello takım veri bilimi işlemi: Hdınsight Hadoop kümeleri kullanarak](machine-learning-data-science-process-hive-walkthrough.md).
* [Veri bilimi Azure HD.mdnsight üzerinde Spark kullanma](machine-learning-data-science-spark-overview.md)
* [Azure Data Lake içinde ölçeklenebilir veri bilimi: bir uçtan uca gözden geçirme](machine-learning-data-science-process-data-lake-walkthrough.md)

