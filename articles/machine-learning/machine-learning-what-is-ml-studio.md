---
title: Azure Machine Learning Studio aaaWhat mi? | Microsoft Belgeleri
description: "Kullanıma hazır bir algoritmalar ve modüller kitaplığından hızla model oluşturmaya yönelik bir sürükle ve bırak aracı olan Azure ML Studio'ya genel bakış."
keywords: azure machine learning,azure ml, ml studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e65c8fe1-7991-4a2a-86ef-fd80a7a06269
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: a25f2d9e75d088a37930de98240c6e14c9567fa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-machine-learning-studio"></a>Azure Machine Learning Studio nedir?
Microsoft Azure Machine Learning Studio toobuild, kullanabileceğiniz bir işbirliğine dayalı, sürükle ve bırak aracı olan test ve verilerinizi Tahmine dayalı analiz çözümlerini dağıtma. Machine Learning Studio, modelleri özel uygulamalar veya Excel gibi BI araçları tarafından kolayca kullanılabilen web hizmetleri olarak yayımlar.

Machine Learning Studio, verilerinizin veri bilimi, tahmine dayalı analiz ve bulut kaynakları ile buluştuğu yerdir.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-machine-learning-studio-interactive-workspace"></a>Merhaba Machine Learning Studio etkileşimli çalışma alanı
Tahmine dayalı bir modeli toodevelop, genellikle kullandığınız veri kaynaklardan bir veya daha fazla dönüştürme ve çeşitli veri işleme ve istatistik işlevleri aracılığıyla bu verileri analiz eder ve bir sonuç kümesi oluşturur. Bir modelin bu şekilde geliştirilmesi yinelemeli bir işlemdir. Değiştirirken çeşitli işlevleri ve bunların parametrelerini Merhaba, memnun olana kadar sonuçlarınız yakınsanır eğitilmiş ve verimli bir model sahip.

**Azure Machine Learning Studio** test ve Tahmine dayalı bir modeli üzerinde yinelemek, etkileşimli ve görsel çalışma tooeasily yapı sağlar. Sürükle ve bırak ***veri kümeleri*** ve analiz ***modülleri*** etkileşimli bir tuvale bunları birlikte tooform bağlayarak bir ***denemeler***, Machine Learning çalıştırılması Studio. isterseniz, bir kopyasını kaydedin hello deneme düzenleyin ve yeniden çalıştırın tooiterate model tasarımınızı üzerinde. Hazır olduğunuzda, dönüştürebilir, ***eğitim denemenizi*** tooa ***Tahmine dayalı denemeye***ve olarak yayımlama bir ***web hizmeti*** modelinizi tarafından erişilebilecek böylece Başkalarının.

Programlama gerekmez; Tahmine dayalı analiz modelinizi görsel olarak yalnızca veri kümelerini ve modülleri tooconstruct bağlanma yoktur.

> [!TIP]
> Machine Learning Studio'nun hello özelliklerine genel bakış sağlayan bir diyagram toodownload ve yazdırma bkz [Azure Machine Learning Studio işlevlerine genel bakış diyagramı](machine-learning-studio-overview-diagram.md).
> 
> 

![Azure ML Studio diyagramı: Deneme oluşturma, birçok kaynak için veri okuma, puanlanmış veri yazma, model yazma.][ml-studio-overview]

## <a name="get-started-with-machine-learning-studio"></a>Machine Learning Studio ile çalışmaya başlama
İlk girişinizde [Machine Learning Studio](https://studio.azureml.net) hello gördüğünüz **giriş** sayfası. Buradan belgeleri, videoları, web seminerlerini görüntüleyebilir ve diğer değerli kaynakları bulabilirsiniz.

Merhaba sol üst menüsünü tıklatın ![Menü](media/machine-learning-what-is-ml-studio/menu.png) birkaç seçenek göreceksiniz.

### <a name="cortana-intelligence"></a>Cortana Intelligence
Tıklatın **Cortana Intelligence** ve hello toohello giriş sayfasına gidersiniz [Cortana Intelligence Suite](https://www.microsoft.com/cloud-platform/cortana-intelligence-suite). Merhaba Cortana Intelligence Suite tam olarak yönetilen bir büyük veri ve analytics suite tootransform verilerinizi akıllı eyleme Gelişmiş. Merhaba Suite Giriş sayfasına müşteri hikayeleri dahil olmak üzere, tam belgelerine bakın.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Burada, iki seçenek vardır **giriş**, başladığınız, başlangıç sayfası ve **Studio**.

Tıklatın **Studio** ve toohello geçen **Azure Machine Learning Studio**. Öncelikle Microsoft hesabınızı veya iş veya Okul hesabınızı kullanarak toosign istenir. Oturum açtıktan sonra hello solda sekmeleri aşağıdaki hello görürsünüz:

* **PROJELER** - Tek bir projeyi temsil eden denemeler, veri kümeleri, not defterleri ve diğer kaynakların koleksiyonu
* **DENEMELER** - Oluşturup çalıştırdığınız veya taslak olarak kaydettiğiniz denemeler
* **WEB HİZMETLERİ** - Denemelerinizden dağıttığınız web hizmetleri
* **NOT DEFTERLERİ** - Oluşturduğunuz Jupyter not defterleri
* **VERİ KÜMELERİ** - Studio'ya yüklediğiniz veri kümeleri
* **EĞİTİLMİŞ MODELLER** - Denemelerde eğittiğiniz ve Studio'da kaydettiğiniz modeller
* **AYARLARI** -hesabınızı ve kaynaklarınızı tooconfigure kullanabileceğiniz ayarlar koleksiyonu.

### <a name="gallery"></a>Galeri
Tıklatın **galeri** ve toohello geçen  **[Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com/)**. Merhaba Galerisi, burada, bir veri bilimcileri ve geliştiricileri paylaşmak hello Cortana Intelligence Suite bileşenleri kullanılarak oluşturduğu çözümleri bir yerdir.

Merhaba galeri hakkında daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi çözümlerinde Bul](machine-learning-gallery-how-to-use-contribute-publish.md).

## <a name="components-of-an-experiment"></a>Deneme bileşenleri
Bir deneme birbirine bağlamak veri tooanalytical modülleri sağlayan kümelerini oluşur tooconstruct Tahmine dayalı bir modeli. Geçerli bir deneme özellikle şu özelliklere sahiptir:

* Merhaba deneme en az bir veri kümesi ve bir modülü vardır
* Veri kümeleri bağlı yalnızca toomodules olabilir
* Modülleri bağlı tooeither veri kümeleri veya diğer modüller olabilir
* Tüm giriş bağlantı noktaları modülleri için bazı bağlantı toohello verileri olmalıdır akışı
* Her bir modül için gereken tüm parametreler ayarlanmalıdır

Bir denemeyi sıfırdan oluşturabilir veya var olan bir örnek denemeyi şablon olarak kullanabilirsiniz. Daha fazla bilgi için bkz: [kopyalama örnek denemelerini toocreate yeni makine öğrenimi denemelerine](machine-learning-sample-experiments.md).

Basit bir deneme oluşturma örneği için bkz. [Azure Machine Learning Studio'da basit bir deneme oluşturma](machine-learning-create-experiment.md).

Tahmine dayalı bir analiz çözümünün daha kapsamlı bir kılavuzu için bkz. [Azure Machine Learning ile tahmine dayalı bir analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md).

### <a name="datasets"></a>Veri kümeleri
Bir veri kümesi, böylece işlem modelleme hello kullanılabilir tooMachine Learning Studio daha eski verileri karşıya ' dir. Birçok örnek veri kümesi Machine Learning Studio, tooexperiment için bulunur ve ihtiyaç duyarsanız daha fazla veri kümesi yükleyebilirsiniz. Dahil olan veri kümelerine aşağıda birkaç örnek verilmiştir:

* **Çeşitli otomobiller için MPG verileri** - Otomobiller için silindir, beygir gücü, vb. sayısına göre tanımlanan galon başına mil (MPG) değerleri.
* **Meme kanseri verileri** - Meme kanseri tanılama verileri.
* **Orman yangını verileri** - Kuzey doğu Portekiz'de orman yangını boyutları.

Bir deneme oluştururken toohello hello tuvale sol hello veri kümeleri kullanılabilir listesinden seçebilirsiniz.

Machine Learning Studio'da birçok örnek veri kümesi bir listesi için bkz: [Azure Machine Learning Studio'da hello örnek veri kümelerini kullanma](machine-learning-use-sample-datasets.md).

### <a name="modules"></a>Modüller
Bir modül, verilerinizde gerçekleştirebileceğiniz bir algoritmadır. Machine Learning Studio modülleri tootraining, Puanlama ve doğrulama veri giriş işlevleri işlemlerini arasında değişen bir sayısına sahip. Dahil olan modüllere aşağıda birkaç örnek verilmiştir:

* [TooARFF Dönüştür] [ convert-to-arff] -dönüştürür .NET seri hale getirilmiş dataset tooAttribute-ilişki dosyası biçimi (ARFF).
* [Basit İstatistikleri Hesaplama][elementary-statistics] - Ortalama, standart sapma vb. basit istatistikleri hesaplar.
* [Doğrusal Regresyon][linear-regression] - Çevrimiçi bir gradyan düşüşü tabanlı doğrusal regresyon modeli oluşturur.
* [Model Puanlama][score-model] - Eğitilmiş bir sınıflandırma veya regresyon modelini puanlar.

Bir deneme oluştururken toohello hello tuvale sol hello kullanılabilir modül listesinden seçebilirsiniz.  

Bir modül tooconfigure hello modülün iç algoritmalarını kullanabileceğiniz parametreler kümesi olabilir. Merhaba tuval üzerinde bir modül seçtiğinizde hello modülün parametreleri hello görüntülenir **özellikleri** hello tuvalin sağındaki bölmesinde toohello. Bu bölmesinde tootune hello parametrelerinde modelinizi değiştirebilirsiniz.

Bazı Yardım hello büyük kitaplığı machine learning algoritmaları gezinmek için bkz: [nasıl Microsoft Azure Machine Learning için toochoose algoritmaları](machine-learning-algorithm-choice.md).

## <a name="deploying-a-predictive-analytics-web-service"></a>Tahmine dayalı analiz web hizmetini dağıtma
Tahmine dayalı analiz modeliniz hazır olduktan sonra, bunu doğrudan Machine Learning Studio'dan bir web hizmeti olarak dağıtabilirsiniz. Bu işlem hakkında daha ayrıntılı bilgi için bkz. [Bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).

[ml-studio-overview]:./media/machine-learning-what-is-ml-studio/azure-ml-studio-diagram.jpg

<!-- Module References -->
[convert-to-arff]: https://msdn.microsoft.com/library/azure/62d2cece-d832-4a7a-a0bd-f01f03af0960/
[elementary-statistics]: https://msdn.microsoft.com/library/azure/3086b8d4-c895-45ba-8aa9-34f0c944d4d3/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
