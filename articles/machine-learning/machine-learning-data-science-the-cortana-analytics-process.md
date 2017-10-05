---
title: "Takım veri bilimi işlemi nedir?  | Microsoft Belgeleri"
description: "Takım veri bilimi işlemi, gelişmiş analizler yararlanan akıllı uygulamaları oluşturmak için sistematik bir yöntemdir."
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
redirect_document_id: TRUE
ms.openlocfilehash: d1ec602b2a69b0bd01bf7b43ef5fed9b8c2781c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-the-team-data-science-process-tdsp"></a>Team Data Science Process (TDSP) nedir?
[Takım veri bilimi işlem (TDSP)](data-science-process-overview.md) etkili bir şekilde bu etkinleştirmek için gereken etkinlikleri tam yaşam üzerinde işbirliği yapmak için veri bilimcilerine ekiplerin sağlayan akıllı uygulamaları oluşturmak için bir sistematik bir yaklaşım sağlar Ürünler halinde uygulamalar. TDSP sağlamak adımların sırasını özetlenmektedir **Kılavuzu** sorun, Araçlar ve ilgili verileri çözümleme, yapı ve Tahmine dayalı modelleri değerlendirmek gerekli ortam ayarlama ve bu modelleri kuruluşta dağıtma hakkında uygulamalar. 

Adımlar şunlardır **takım veri bilimi işlemi**:  

![CAP iş akışı](./media/machine-learning-data-science-the-cortana-analytics-process/CAP-workflow.png)

İşlem **yinelemeli**: anlama, yeni ve mevcut ya da düzeltmeler modelinde dönüşmesi ve önceden sırada tamamlandı adımları denetçiye yeni biçim gerektirir. Var olan Kuruluş geliştirme ve işlemleri planlama proje **kolayca uyarlanmış** adımları TDSP tanımlı dizisi ile çalışmak için. 

İşlemdeki adımlar tasarımını ve bağlı [TDSP öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) ve aşağıda açıklanmıştır.  

## <a name="preparation-steps"></a>Hazırlık adımları
## <a name="p1-plan-the-analytics-project"></a>P1. Analytics proje planlama
Analytics projesinde iş hedeflerine ve sorunları tanımlayarak başlatın. Cinsinden belirtilen **iş gereksinimlerini**. Bu adımı merkezi amacı, bu gereksinimleri karşılamak için tahmin etmek için analiz gereken önemli iş değişkenleri (satış tahmini veya bir sipariş olma olasılığını örneğin sahte) belirlemektir. Ek planlama önemlidir sonra bir anlayış geliştirmek için genellikle **veri kaynakları** proje amaçlarını analitik açısından adresi gerekiyor. Örneğin, varolan sistemler toplamak ve sorun gidermek ve proje hedeflerinize ulaşmak için veri ek türlerini oturum gerektiğini bulmak için genel olarak görülmez, değil. Yönergeler için bkz [ortamınız için takım veri bilimi işlemi planlama](machine-learning-data-science-plan-your-environment.md) ve [senaryoları Azure Machine Learning, gelişmiş analizler için](machine-learning-data-science-plan-sample-scenarios.md).  

## <a name="p2-setup-analytics-environment"></a>P2. Analiz ortamını ayarlama
Takım veri bilimi işlemi analytics ortam çeşitli bileşenleri içerir: 

* **Veri çalışma alanları** veri analizi ve modelleme, için hazırlanan burada 
* bir **işleme altyapısı** önceden işlenmesi, keşfetme ve veri modelleme
* bir **çalışma zamanı altyapısında** analitik modelleri faaliyete ve akıllı istemci modelleri kullanma uygulamaları çalıştırmak için.  

Kurulum olması gereken analytics genellikle çekirdek işletim sistemlerinden ayrı bir ortam parçası altyapısıdır. Ancak genellikle kuruluş içinde birden çok sistemlerden ve aynı zamanda şirket dış kaynaklardan veri yararlanır. Analytics altyapı tamamen bulut tabanlı, olabilir veya bir şirket içi Kurulum veya ikisinin karma. Seçenekler için bkz: [takım veri bilimi işlemi kullanmak için veri bilimi ortamları ayarlama](machine-learning-data-science-environment-setup.md).

## <a name="analytics-steps"></a>Analytics adımlar:
## <a name="1-ingest-data-into-the-analytical-environment"></a>1. Analitik ortamına veri alma
İlk adım ilgili verilerin herhangi birinden gelen veya içinde kuruluş dışına çeşitli kaynaklardan gelen verileri işleneceği bir analitik ortamlara koymaktır. **Biçimi** veri kaynağında hedefi tarafından gerekli biçimi farklı olabilir. Bu nedenle bazı veri dönüştürme de alım araçları tarafından yapılması gerekebilir. Seçenekler için bkz: [analiz için depolama ortamlara veri yükleme](machine-learning-data-science-ingest-data.md)

Ek olarak ilk alım veri birçok akıllı uygulama verileri düzenli olarak devam eden öğrenme işleminin bir parçası yenilemek için gereklidir. Bu kurulum tarafından yapılabilir bir **veri ardışık** veya iş akışı. Bu yeniden oluşturma ve çözüm dağıtma akıllı uygulama tarafından kullanılan analitik modelleri yeniden değerlendirme içeren işleminin yinelemeli bir bölümü parçası oluşturur. Örneğin bkz [veri taşıma bir şirket içi SQL Server'dan Azure Data Factory ile SQL Azure](machine-learning-data-science-move-sql-azure-adf.md).

## <a name="2-explore-and-pre-process-data"></a>2. Veriyi inceleme ve ön işlemden geçirme
Sonraki adım verilerinizin daha derin bir anlayış incelenerek elde edilir, **Özet istatistikleri** , ilişkileri ve böyle teknikleri kullanarak **görselleştirme**. Bu aynı zamanda olup burada, sorunlar **veri kalitesini** ve eksik değerleri, veri türü uyuşmazlığı ve tutarsız veri ilişkileri gibi bütünlüğü işlenir. Ön işleme dönüşümler ek analizler önce ham verileri temizlemek için kullanılır ve modelleme gerçekleşebilir. Bir açıklama için bkz: [veri Gelişmiş için hazırlamak üzere görevleri makine öğrenme](machine-learning-data-science-prepare-data.md).

## <a name="3-develop-features"></a>3. Özellikler geliştirin
Etki alanı uzmanlar işbirliğiyle veri bilimcilerine veri kümesinin belirgin özellikleri yakalama ve planlama sırasında tanımlanan anahtar iş değişkenleri tahmin etmek için en iyi kullanılabilir özellikler tanımlamanız gerekir. Bu yeni özellikler, var olan verilerden türetilmiş veya toplanacak ek veri gerektirebilir. Bu işlem olarak bilinir **özellik Mühendisliği** ve etkili Tahmine dayalı analiz sistem oluşturmanın temel adımları biridir. Bu adım, etki alanı uzmanlık yaratıcı bir birleşimini ve veri araştırması adımda elde edilen Öngörüler gerektirir. Yönergeler için bkz [özellik Mühendisliği takım veri bilimi işleminde](machine-learning-data-science-create-features.md).

## <a name="4-create-predictive-models"></a>4. Tahmine dayalı modeller oluşturma
Veri bilimcilerine planlama adımı temizlenmiş verileri kullanarak ve featurized tanımlanan iş gereksinimleri tarafından tanımlanan anahtar değişkenleri tahmin etmek için analitik modelleri oluşturabilir. Machine learning sistemlerini destekleyen birden çok **algoritmaları modelleme** , çok çeşitli durumlarda uygulanabilir. Yönergeler için bkz [takım Azure Machine Learning algoritmaları seçme](machine-learning-algorithm-choice.md).

Veri bilimcilerine kendi tahmin görev için en uygun model seçmeniz gerekir ve birden fazla modeli sonuçlarından en iyi sonuçları elde etmek için bir arada kullanılabilir gerektiğini seyrek değil. Modelleme için giriş verileri genellikle rastgele üç kısma ayrılmıştır:

* bir eğitim veri kümesi 
* bir doğrulama veri kümesi 
* bir sınama veri kümesi 

Modelleri kullanılarak oluşturulan **eğitim veri kümesi**. Modelleri çalıştırarak ve tahmin hatalarla ölçme modelleri (parametrelerle olarak ayarlanmış) en iyi birleşimi seçili **doğrulama veri kümesi**. Son olarak **sınama veri kümesi** seçilen modeli eğitmek veya model doğrulamak için kullanılmamış bağımsız verileri performansını değerlendirmek için kullanılır.  Yordamlar için bkz: [Azure Machine Learning modeli performansını değerlendirmek nasıl](machine-learning-evaluate-model-performance.md).

## <a name="5-deploy-and-consume-models"></a>5. Dağıtma ve modelleri kullanma
Biz de gerçekleştirmek modelleri kümesi oluşturduktan sonra olabilirler **kullanıma hazır hale getirilmiş** kullanacak diğer uygulamalar için. İş gereksinimlerine bağlı olarak, ya da tahminleri yapılan **gerçek zamanlı** veya bir **toplu** temel. Kullanıma hazır hale getirilmiş için modelleri ile kullanıma sahip bir **API arabirimini açın** , kolayca tüketilen çeşitli uygulamalardan gibi çevrimiçi Web sitesi, elektronik tablolar, panolar veya iş ve arka uç uygulamalarının satır. Bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="summary-and-next-steps"></a>Özet ve sonraki adımlar
[Takım veri bilimi işlemi](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) tekrarlayan adımlar dizisi olarak Modellenen, **kılavuzluk** akıllı uygulamaları oluşturmak için gelişmiş analizler kullanmak için gereken görevler. Her adım, ayrıca çeşitli Microsoft teknolojileri açıklanan görevleri tamamlamak için nasıl kullanılacağı hakkında ayrıntılar sağlar. 

TDSP belirli türlerdeki belgenizdeki değil sırada **belgelerine** yapıları, veri keşfi, model oluşturma ve değerlendirme sonuçlarını belge en iyi uygulamadır ve analiz böylece ilgili kod kaydetmek için yinelendiğinde gerekli olduğunda. Bu ayrıca analytics iş kullanılmasını benzer veri ve tahmin görevleri içeren diğer uygulamalar üzerinde çalışırken sağlar.

Tam işlem için tüm adımları gösteren uçtan uca talimatlara **belirli senaryolar** de sağlanır. , Örneğin bakın:

* [Eylem takım veri bilimi işleminde: SQL Server kullanma](machine-learning-data-science-process-sql-walkthrough.md)
* [Eylem takım veri bilimi işleminde: Hdınsight Hadoop kümeleri kullanarak](machine-learning-data-science-process-hive-walkthrough.md).
* [Veri bilimi Azure HD.mdnsight üzerinde Spark kullanma](machine-learning-data-science-spark-overview.md)
* [Azure Data Lake içinde ölçeklenebilir veri bilimi: bir uçtan uca gözden geçirme](machine-learning-data-science-process-data-lake-walkthrough.md)

