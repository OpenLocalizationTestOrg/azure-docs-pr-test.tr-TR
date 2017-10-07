---
title: "aaaAzure Machine Learning sık sorulan sorular (SSS) | Microsoft Docs"
description: "Azure Machine Learning'e giriş: Kolaylaştırılmış tahmine dayalı modelleme için bir bulut hizmetinin faturalamasını, özelliklerini ve sınırlamalarını kapsayan SSS."
keywords: "machine learning giriş,tahmini modelleme,machine learning nedir"
services: machine-learning
documentationcenter: 
author: garyericson
manager: paulettm
editor: cgronlun
ms.assetid: a4a32a06-dbed-4727-a857-c10da774ce66
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 3af84451dde064c3c9520ee520b541128b1eef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-frequently-asked-questions-billing-capabilities-limitations-and-support"></a>Azure Machine Learning ile ilgili sık sorulan sorular: Faturalama, özellikler, sınırlamalar ve destek
Aşağıda, tahmine dayalı modeller geliştirmeye ve web hizmetleri aracılığıyla çözümleri faaliyete geçirmeye yönelik bir bulut hizmeti olan Azure Machine Learning hakkında sık sorulan bazı sorular (SSS) ve yanıtları verilmiştir. Bu SSS nasıl toouse hello faturalama modeli, özellikler, sınırlamalar ve Destek hello dahil hakkında sorular sağlar.

**Burada olmayan bir sorunuz mu var?**

Azure Machine Learning Forumu yere hello veri bilimi topluluk üyeleri Azure Machine Learning hakkında sorular sorabilirsiniz MSDN'de sahiptir. Hello Azure Machine Learning ekibi hello Forumu izler. Toohello Git [Azure Machine Learning Forumu](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toosearch yanıtlar veya toopost kendi yeni bir soru.

## <a name="general-questions"></a>Genel sorular
**Azure Machine Learning nedir?**

Azure Machine Learning, toocreate kullanmak, test, çalıştırmak ve hello bulutta Tahmine dayalı analitik çözümleri yönetmek, tam olarak yönetilen bir hizmettir. Yalnızca bir tarayıcıyla oturum açabilir, verileri yükleyebilir ve anında makine öğrenimi denemelerine başlayabilirsiniz. Tahmine dayalı sürükle ve bırak modelleme, büyük bir modül paleti ve başlangıç şablonları kitaplığı, ortak makine öğrenimi görevlerini basit ve hızlı hale getirir. Daha fazla bilgi için bkz: Merhaba [Azure Machine Learning hizmetine genel bakış](https://azure.microsoft.com/services/machine-learning/). Önemli terminolojiyi ve kavramları açıklayan bir giriş toomachine öğrenme için bkz: [giriş tooAzure Machine Learning](machine-learning-what-is-machine-learning.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**Machine Learning Studio nedir?**

Machine Learning Studio, bir web tarayıcısı kullanarak erişebileceğiniz bir çalışma ekranı ortamıdır. Machine Learning Studio'da bir uçtan uca oluşturmanıza yardımcı olan bir görsel birleştirme arabirimi modülleri, bir deneme hello şeklinde veri bilimi akışı bir modül paleti barındırır.

Machine Learning Studio hakkında daha fazla bilgi için bkz. [Machine Learning Studio nedir?](machine-learning-what-is-ml-studio.md).

**Merhaba Machine Learning API'si hizmeti nedir?**

Merhaba Machine Learning API'si hizmeti, Machine Learning Studio'ya ölçeklenebilir, hataya dayanıklı web Hizmetleri olarak yerleşik olanlar gibi Tahmine dayalı modelleri toodeploy sağlar. Merhaba Machine Learning API'si hizmeti oluşturan hello web harici uygulamalar ve Tahmine dayalı analiz modelleriniz arasında iletişim için bir arabirim sağlayan REST API'leri hizmetleridir.

Daha fazla bilgi için bkz: [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).

**Klasik web hizmetlerim nerede listelenir? Yeni (Azure Resource Manager tabanlı) web hizmetlerim nerede listelenir?**

Merhaba yeni Azure Resource Manager dağıtım modeli kullanılarak oluşturulmuş hello Klasik dağıtım modeli ve web Hizmetleri kullanılarak oluşturulmuş web hizmetlerini hello listelenen [Microsoft Azure Machine Learning Web Hizmetleri](https://services.azureml.net/) portal.

Klasik web Hizmetleri içinde de listelenen [Machine Learning Studio](http://studio.azureml.net) hello üzerinde **Web Hizmetleri** sekmesi.

## <a name="azure-machine-learning-questions"></a>Azure Machine Learning soruları
**Microsoft Azure Machine Learning web hizmetleri nelerdir?**

Machine Learning web hizmetleri, bir uygulama ile Machine Learning iş akışı puanlama modeli arasında bir arabirim sağlar. Bir dış uygulama, Machine Learning bir iş akışı Puanlama modeli ile gerçek zamanlı ile Azure Machine Learning toocommunicate kullanabilirsiniz. Bir Machine Learning web hizmeti çağrısı tooa tahmin sonuçlarını tooan dış uygulama döndürür. toomake çağrısı tooa web hizmeti, hello web hizmetini dağıttığınızda, oluşturulan bir API anahtarı geçirirsiniz. Machine Learning web hizmetleri, web programlama projeleri için popüler bir mimari seçimi olan REST’i temel alır.

Azure Machine Learning iki tür web hizmeti içerir:

* İstek-yanıt hizmeti (RRS): Düşük gecikme, durum bilgisi olmayan modellere bir arabirim toohello sağlayan yüksek düzeyde ölçeklenebilir hizmet oluşturulan ve Machine Learning Studio kullanılarak dağıtılır.
* Toplu Yürütme Hizmeti (BES): Veri kayıtları için toplu iş yapan zaman uyumsuz bir hizmettir.

Tooconsume hello REST API ve erişim hello web hizmeti birkaç yolu vardır. Örneğin, hello web hizmetini dağıttığınızda sizin için oluşturulan hello örnek kodu kullanarak C#, R veya Python bir uygulama yazabilirsiniz.

Merhaba örnek kod edinilebilir:
- Merhaba Tüket sayfa hello Azure Machine Learning Web Hizmetleri portalında hello web hizmeti
- Machine Learning Studio hello web hizmeti panosundaki API Yardım sayfasında Hello

Sizin için oluşturulan ve Machine Learning Studio hello web hizmeti panosunda mevcuttur hello örnek Microsoft Excel çalışma kitabı de kullanabilirsiniz.

**Merhaba ana güncelleştirmeleri tooAzure Machine Learning nedir?**

Merhaba en son güncelleştirmeler için bkz: [Azure Machine Learning yenilikler](machine-learning-whats-new.md).

## <a name="machine-learning-studio-questions"></a>Machine Learning Studio soruları
### <a name="import-and-export-data-for-machine-learning"></a>Machine Learning için verileri içeri ve dışarı aktarma
**Machine Learning hangi veri kaynaklarını destekliyor?**

Veri tooa Machine Learning Studio denemesine üç şekilde yükleyebilirsiniz:

- Yerel bir dosyayı veri kümesi olarak karşıya yükleme
- Bir modül tooimport verileri bulut veri hizmetlerinden kullanın
- Başka bir denemeden kaydedilen veri kümesini içeri aktarma

desteklenen dosya biçimleri toolearn hakkında daha fazla bilgi için bkz [Machine Learning Studio'da eğitim verilerini içeri aktarma](machine-learning-data-science-import-data.md).

#### <a id="ModuleLimit"></a>Ne kadar büyük hello veri kümesi modüllerim olabilir?
Machine Learning Studio'daki modüller, ortak kullanım durumları için yukarı too10 GB boyutunda yoğun sayısal verili veri kümelerini destekler. Bir modülün birden fazla giriş aldığı durumlarda hello 10 GB değer olan hello tüm giriş boyutlarının toplam. Ayrıca, Hive veya Azure SQL Veritabanı’ndan yapılan sorguları kullanarak daha büyük veri kümelerinden örnek oluşturabilir ya da alımdan önce Sayımlarla Öğrenme ön işlemesini kullanabilirsiniz.  

Merhaba aşağıdaki veri türlerini toolarger veri kümeleri, özellik normalleştirme sırasında genişletebilirsiniz ve 10 GB'den sınırlı tooless şunlardır:

* Seyrek
* Kategorik
* Dizeler
* İkili veriler

Modüller aşağıdaki hello 10 GB'den küçük sınırlı toodatasets şunlardır:

* Öneren modüller
* Synthetic Minority Oversampling Technique (SMOTE) modülü
* Betik modülleri: R, Python, SQL
* Veri boyutu hello çıkış modülleri katılma veya özellik karma gibi girdi veri boyutundan büyük olamaz
* Çapraz doğrulama, Model ayarlama Hiperparametreleri, sıralı regresyon ve yinelemeleri hello sayısı çok büyük olduğunda bir tüm veya çoklu sınıflar

#### <a id="UploadLimit"></a>Karşıya veri hello sınırları nelerdir?
Birkaç GB'den büyük veri kümeleri için veri tooAzure depolama veya Azure SQL Database, karşıya yükleme veya Azure Hdınsight kullanmak yerine doğrudan yerel dosyadan yüklemek.

**Verileri Amazon S3'ten okuyabilir miyim?**

Az miktarda veriniz varsa ve tooexpose istiyorsanız bir HTTP URL'sini, ardından aracılığıyla hello kullanabileceği [veri içeri aktarma] [ import-data] modülü. Büyük miktarlarda veri için onu tooAzure depolama ilk aktarım ve sonra hello [veri içeri aktarma] [ import-data] modülü toobring denemenizi içine.
<!--

<SEE CLOUD DS PROCESS>
-->

**Yerleşik bir görüntü girişi özelliği var mı?**

Merhaba görüntü girişi özelliği hakkında bilgi alabilirsiniz [görüntüleri Al] [ image-reader] başvuru.

### <a name="modules"></a>Modüller
**Merhaba algoritması, veri kaynağı, veri biçimi veya aradığım veri dönüştürme işlemi Azure Machine Learning Studio'da değil. Seçeneklerim neler?**

Toohello gidebilirsiniz [kullanıcı geri bildirim Forumunda](http://go.microsoft.com/fwlink/?LinkId=404231) toosee özellik istekleri biz izleme. Aradığınız bir özellik zaten istenmişse oy tooa isteğiniz ekleyin. Aradığınız hello özellik mevcut değilse yeni bir istek oluşturun. Bu forumda isteğinizin durumunu hello çok görüntüleyebilirsiniz. Biz bu listeyi yakından takip edip hello Özellik kullanılabilirliği durumunu sık sık güncelleştirin. Ayrıca, gerektiğinde R ve Python toocreate özel dönüştürmeleri için yerleşik destek hello kullanabilirsiniz.

**Var olan kodumu Machine Learning Studio'ya getirebilir miyim?**

Evet, var olan R veya Python kodunuzu Machine Learning Studio, aynı Azure Machine Learning öğrencileriyle denemek ve Azure Machine Learning aracılığıyla bir web hizmeti olarak hello çözümü dağıtmak hello içinde çalıştırın içine getirebilirsiniz. Daha fazla bilgi için bkz. [R ile denemenizi genişletme](machine-learning-extend-your-experiment-with-r.md) ve [Azure Machine Learning Studio'da Python makine öğrenimi betiklerini yürütme](machine-learning-execute-python-scripts.md).

**Şuna benzer olası toouse olan [PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language) toodefine bir model?**

Hayır, Predictive Model Markup Language (PMML) desteklenmez. Python toodefine bir modül kod ve özel R kullanabilirsiniz.

**Denememe paralel şekilde kaç modül yürütebilirim?**  

Bir denemede paralel şekilde toofour modülleri yukarı yürütebilir.

### <a name="data-processing"></a>Veri işleme
**Bir özelliği toovisualize (R görselleştirmesinin ötesinde) etkileşimli olarak içindeki verileri hello deneme var mı?**

Bir modülü toovisualize hello veri Hello çıktısını tıklayın ve istatistiklerini alın.

**Sonuçları veya verileri bir tarayıcıda önizlerken satır ve sütunları hello sayısını sınırlıdır. Neden?**

Büyük miktarlarda verinin tooa tarayıcı gönderilebilir, veri boyutu Machine Learning Studio'nun yavaşlamasının sınırlı tooprevent olmasıdır. toovisualize tüm veri/sonuçları Merhaba, buna ait daha iyi toodownload hello veri ve Excel veya başka bir araç kullanın.

### <a name="algorithms"></a>Algoritmalar
**Machine Learning Studio'da hangi mevcut algoritmalar destekleniyor?**

Machine Learning Studio, Microsoft Research'te geliştirilen Ölçeklenebilir Artırılmış Karar ağaçları, Bayes Önerisi sistemleri, Derin Sinir Ağları ve Karar Ormanları gibi teknoloji harikası algoritmaları sağlar. Vowpal Wabbit gibi ölçeklenebilir açık kaynaklı makine öğrenimi paketleri de dahildir. Machine Learning Studio, çok sınıflı ve ikili sınıflandırma, regresyon ve kümeleme için makine öğrenimi algoritmalarını destekler. Merhaba tam listesini görmek [Machine Learning modüllerinin][machine-learning-modules].

**Merhaba doğru Machine Learning algoritmasını toouse verilerim için otomatik olarak öneriyor musunuz?**

Hayır, ancak Machine Learning Studio toocompare hello her algoritması toodetermine sonuçlarını hello sorununuz için doğru olanı çeşitli yolları vardır.

**Bir algoritma yerine başkasını hello sağlanan algoritmalar için çekme üzerinde herhangi bir yönerge var mı?**

Bkz: [nasıl toochoose bir algoritma](machine-learning-algorithm-choice.md).

**Merhaba sağlanan algoritmalar R veya Python ile mi yazılmış?**

Hayır, bu algoritmalar genellikle derlenmiş dillerde tooprovide daha iyi performans yazılır.

**Sağlanan hello algoritmalarının herhangi bir ayrıntıyı misiniz?**

Merhaba belgeler hello algoritmalar hakkında bazı bilgiler sağlar ve ayarlama kullanımınız için açıklanan toooptimize hello algoritma parametreleridir.  

**Çevrimiçi öğrenmeye yönelik herhangi bir destek var mı?**

Hayır, şu anda yalnızca programlama yoluyla yeniden eğitim desteklenir.

**Sinir ağı modelinin hello Katmanlar hello yerleşik modülü kullanarak görselleştirebilir miyim?**

Hayır.

**Kendi modüllerimi C# veya başka bir dilde oluşturabilir miyim?**

Şu anda R toocreate yeni özel Modüller yalnızca kullanabilirsiniz.

### <a name="r-module"></a>R modülü
**Machine Learning Studio'da hangi R paketleri kullanılabilir?**

Machine Learning Studio 400'den CRAN R paketlerini bugün destekler ve hello işte [geçerli listesi](http://az754797.vo.msecnd.net/docs/RPackages.xlsx) dahil olan tüm paketlerin. Ayrıca bkz [denemenizi r ile genişletme](machine-learning-extend-your-experiment-with-r.md) toolearn nasıl tooretrieve bu listeyi. İstediğiniz hello paket bu listede değilse, hello hello hello paketin adını sağlayın [kullanıcı geri bildirim Forumunda](http://go.microsoft.com/fwlink/?LinkId=404231).

**Olası toobuild özel bir R Modülü nedir?**

Evet, daha fazla bilgi için bkz. [Azure Machine Learning'de özel R modülleri yazma](machine-learning-custom-r-modules.md).

**R için bir REPL ortamı var mı?**

Hayır, hello Studio'da R için Read-Eval-yazdırma-döngüsü (REPL) ortamı yoktur.

### <a name="python-module"></a>Python modülü
**Olası toobuild özel bir Python Modülü nedir?**

Şu anda değil ancak bir veya daha fazla kullanabilirsiniz [Python betiği yürütme] [ python] modülleri tooget hello aynı sonucu.

**Python için bir REPL ortamı var mı?**

Machine Learning Studio'da hello Jupyter not defterlerini kullanabilirsiniz. Daha fazla bilgi için bkz. [Azure Machine Learning Studio'da Jupyter Not Defterlerine Giriş](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).

## <a name="web-service"></a>Web hizmeti
### <a name="retrain"></a>Yeniden eğitme
**Azure Machine Learning modellerini program aracılığıyla nasıl yeniden eğitebilirim?**

Merhaba yeniden eğitme API'lerini kullanın. Daha fazla bilgi için bkz. [Machine Learning modellerini programlama aracılığıyla yeniden eğitme](machine-learning-retrain-models-programmatically.md). Örnek kodu hello kullanılabilir ayrıca [Microsoft Azure Machine Learning yeniden eğitme demosu](https://azuremlretrain.codeplex.com/).

### <a name="create"></a>Oluştur
**Merhaba modeli yerel olarak veya bir Internet bağlantısına sahip olmayan bir uygulamada dağıtabilir miyim?**

Hayır.

**Tüm web hizmetleri için beklenen bir temel gecikme süresi var mı?**

Merhaba bkz [Azure abonelik limitleri](../azure-subscription-service-limits.md).

### <a name="use"></a>Kullanım
**Ne zaman toorun Tahmine dayalı bir toplu iş yürütme hizmeti bir istek yanıtı hizmeti karşılaştırması olarak kullanmalıyım?**

Merhaba istek yanıtı hizmeti (RRS) düşük gecikmeli, yüksek ölçekli web hizmetinin kullanılan tooprovide arabirimi toostateless olan modeller oluşturulur ve hello deneme ortamından dağıtılır. Merhaba toplu yürütme hizmeti (BES) zaman uyumsuz olarak bir toplu veri kayıtlarının puanlar bir hizmettir. BES için giriş hello RR kullanan veri girişi ister. Merhaba temel fark BES kayıt bloğunu kaynakları Azure Blob storage, Azure Table storage, Azure SQL Database, Hdınsight (hive sorgusu) ve HTTP kaynakları gibi çeşitli okumasıdır. Daha fazla bilgi için bkz: [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).

**Dağıtılan hello web hizmeti için hello modeli nasıl güncelleştiririm?**

tooupdate zaten dağıtılmış bir hizmet için Tahmine dayalı bir modeli değiştirin ve tooauthor kullanılan hello deneme yeniden çalıştırın ve Merhaba, eğitilen modeli kaydedin. Yeni bir hello kullanılabilen eğitim modeli sürümüne sahip sonra Machine Learning Studio, tooupdate web hizmetiniz isteyip istemediğinizi sorar. Hakkında ayrıntılar için tooupdate dağıtılan web hizmeti için bkz: [Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).

Merhaba Retraining API de kullanabilirsiniz.
Daha fazla bilgi için bkz. [Machine Learning modellerini programlama aracılığıyla yeniden eğitme](machine-learning-retrain-models-programmatically.md). Örnek kodu hello kullanılabilir ayrıca [Microsoft Azure Machine Learning yeniden eğitme demosu](https://azuremlretrain.codeplex.com/).

**Üretim ortamında dağıtılan web hizmetimi nasıl izlerim?**

Tahmine dayalı bir model dağıttıktan sonra Azure Klasik hello izleyebilirsiniz portal (yalnızca klasik web Hizmetleri) veya hello Azure Machine Learning Web Hizmetleri portalı. Dağıtılan her bir hizmet kendine panosuna sahiptir ve burada bu hizmetin izleme bilgilerini görebilirsiniz. Dağıtılmış web hizmetlerinizi nasıl toomanage gördükleri hakkında daha fazla bilgi için [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md) ve [bir Azure Machine Learning çalışma alanını yönetme](machine-learning-manage-workspace.md).

**Burada hello RRS/BES'imin çıktısını görebileceğim bir yer var mı?**

RRS için hello web hizmeti yanıtı genellikle hello sonuç gördüğünüz ' dir. Ayrıca tooAzure Blob Depolama yazabilirsiniz. BES hello çıktısı tooa blob varsayılan olarak yazılır. Hello kullanarak hello çıktı tooa veritabanı veya tablo da yazabilirsiniz [verileri dışa aktar] [ export-data] modülü.

**Yalnızca Machine Learning Studio'da oluşturulan modellerden mi web hizmetleri oluşturabilirim?**

Hayır, doğrudan Jupyter Not Defterlerinden ve RStudio'dan da web hizmetleri oluşturabilirsiniz.

**Hata kodlarıyla ilgili bilgileri nerede bulabilirim?**

Hata kodları ve açıklamaları listesi için bkz: [Machine Learning Hata Kodları](https://msdn.microsoft.com/library/azure/dn905910.aspx).

## <a name="scalability"></a>Ölçeklenebilirlik
**Merhaba web hizmeti hello ölçeklenebilirliği nedir?**

Şu anda hello varsayılan uç nokta, uç nokta başına 20 eş zamanlı RRS isteği ile sağlanır. Uç nokta başına bu too200 eşzamanlı istek ölçeklendirebilirsiniz ve açıklandığı gibi her web hizmeti too10, web hizmeti başına 000 uç noktaları ölçeklendirebilirsiniz [bir Web hizmeti ölçeklendirme](machine-learning-scaling-webservice.md). BES için her bir uç nokta tek seferde 40 istek işleyebilir ve 40'ı aşan ek istekler kuyruğa alınır. Bu kuyruğa alınan istekler hello sıra azaldıkça otomatik olarak çalışır.

**R işleri düğümlere yayılır mı?**

Hayır.  

**Eğitim için ne kadar veri kullanabilirim?**

Machine Learning Studio'daki modüller, ortak kullanım durumları için yukarı too10 GB boyutunda yoğun sayısal verili veri kümelerini destekler. Bir modülün birden fazla giriş, hello toplam aldığı durumlarda tüm girdilerin boyutu 10 GB'tır. Hive sorguları, Azure SQL Veritabanı sorguları ya da alımdan önce [Sayımlarla Öğrenme][counts] modülleriyle ön işleme aracılığıyla daha büyük veri kümelerinden de örnek oluşturabilirsiniz.  

Merhaba aşağıdaki veri türlerini toolarger veri kümeleri, özellik normalleştirme sırasında genişletebilirsiniz ve 10 GB'den sınırlı tooless şunlardır:

* Seyrek
* Kategorik
* Dizeler
* İkili veriler

Modüller aşağıdaki hello 10 GB'den küçük sınırlı toodatasets şunlardır:

* Öneren modüller
* Synthetic Minority Oversampling Technique (SMOTE) modülü
* Betik modülleri: R, Python, SQL
* Veri boyutu hello çıkış modülleri katılma veya özellik karma gibi girdi veri boyutundan büyük olamaz
* Yineleme sayısının çok büyük olduğu durumlarda Çapraz Doğrulama, Model Ayarlama Hiperparametreleri, Sıralı Regresyon ve Tek veya Tüm Çoklu Sınıflar

Birkaç GB'den büyük veri kümeleri için veri tooAzure depolama veya Azure SQL Database, karşıya yükleme veya Hdınsight kullanmak yerine doğrudan yerel dosyadan yüklemek.

**Herhangi bir vektör boyutu sınırlaması var mı?**

Satırları ve sütunları olan her sınırlı toohello .NET sınırlamasına Max int: 2.147.483.647.

**Merhaba web hizmeti çalıştıran hello sanal makineyi hello boyutuna göre ayarlayabilirsiniz?**

Hayır.  

## <a name="security-and-availability"></a>Güvenlik ve kullanılabilirlik
**Varsayılan olarak hello web hizmeti için http uç noktaya hello erişebilecek mi? Erişim toohello uç noktayı nasıl kısıtlama?**

Bir web hizmeti dağıtıldıktan sonra, bu hizmet için varsayılan bir uç noktası oluşturulur. Merhaba varsayılan uç noktası, API anahtarı kullanılarak çağrılabilir. Daha fazla uç'hello Azure Klasik portalında veya program aracılığıyla kullanarak kendi anahtarları ile Web Hizmeti Yönetimi API'leri hello ekleyebilirsiniz. Erişim tuşları gerekli toomake çağrıları toohello web hizmeti aynıdır. Daha fazla bilgi için bkz: [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).

**Azure depolama hesabım bulunamazsa ne olur?**

Merhaba iş akışı yürüttüğünde machine Learning Studio bir kullanıcı tarafından sağlanan Azure depolama hesabı toosave Ara verileri üzerinde kullanır. Bir çalışma alanı oluşturulduğunda, bu depolama hesabını tooMachine Learning Studio'ya sağlanır. Merhaba sonra hello depolama hesabı silinir ve artık bulunabilir, hello çalışma alanı işlemeyi durdurur ve tüm denemelerini çalışma başarısız olur, çalışma alanı oluşturulur.

Merhaba depolama hesabıyla aynı adı hello hello hello depolama hesabını yanlışlıkla sildiyseniz yeniden hello aynı bölgede depolama hesabı silindi. Bundan sonra hello erişim anahtarı yeniden eşitler.

**Depolama hesabımın erişim anahtarı eşitlenmemişse ne olur?**

Merhaba iş akışı yürüttüğünde machine Learning Studio bir kullanıcı tarafından sağlanan Azure depolama hesabı toostore Ara verileri üzerinde kullanır. Bu depolama hesabı, bir çalışma alanı oluşturulduğunda ve hello erişim tuşları bu çalışma alanıyla ilişkili tooMachine Learning Studio sağlanır. Hello çalışma alanı oluşturulduktan sonra hello erişim anahtarlarını değiştirdiyseniz, hello çalışma hello depolama hesabı artık erişemez. Çalışmayı durdurur ve bu çalışma alanındaki tüm denemeler başarısız olur.

Depolama hesabı erişim anahtarlarını değiştirdiyseniz Klasik Azure portalında yeniden eşitleme hello erişim tuşlarını kullanarak hello çalışma alanında hello.  

## <a name="support-and-training"></a>Destek ve eğitim
**Azure Machine Learning için nereden eğitim alabilirim?**

Merhaba [Azure Machine Learning Belge Merkezi](https://azure.microsoft.com/services/machine-learning/) video öğreticiler ve nasıl tooguides barındırır. Bu adım adım kılavuzlar hello Hizmetleri getirir ve verileri içeri aktarma, verileri temizlemenin, Tahmine dayalı modeller oluşturmanın ve Azure Machine Learning kullanarak üretimde dağıtmadan hello veri bilimi yaşam döngüsü açıklanmaktadır.

Sürekli olarak yeni malzeme toohello Machine Learning merkezi ekleriz. Merhaba, Machine Learning Merkezi hakkında ek öğrenme materyalleri için istek göndermeden [kullanıcı geri bildirim Forumunda](https://windowsazure.uservoice.com/forums/257792-machine-learning).

[Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning)'de de eğitim bulabilirsiniz.

**Azure Machine Learning için nasıl destek alabilirim?**

Azure Machine Learning için teknik destek tooget Git çok[Azure Destek](/support/options/)seçip **Machine Learning**.

Azure Machine Learning'in hizmet hakkında sorular sorabileceğiniz bir MSDN topluluk forumu da bulunur. Hello Azure Machine Learning ekibi hello Forumu izler. Çok Git[Azure Forumu](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning).

## <a name="billing-questions"></a>Faturalama soruları
**Machine Learning için faturalama nasıl gerçekleşir?**

Azure Machine Learning iki bileşenden oluşur: Machine Learning Studio ve Machine Learning web hizmetleri.

Machine Learning Studio'yu değerlendirirken ücretsiz faturalandırma katmanını hello kullanabilirsiniz. Merhaba ücretsiz katmanı, ayrıca kapasitesi sınırlı bir Klasik web hizmeti dağıtmanıza olanak tanır.

Standart katmanı, karar verirseniz Azure Machine Learning gereksinimlerinizi karşılayan, için kaydolabilirsiniz hello. toosign oluşturan bir Microsoft Azure aboneliğinizin olması gerekir.

Merhaba standart katmanındaki aylık Machine Learning Studio'da tanımladığınız her çalışma alanı için faturalandırılır. Merhaba Studio'da bir denemeyi çalıştırdığınızda, bir denemeyi çalıştırırken işlem kaynakları faturalandırılır. Ne zaman bir Klasik web hizmeti dağıttığınızda işlemler ve saatleri hello Kullandıkça Öde temelinde faturalandırılır.

Yeni (Resource Manager tabanlı) web hizmetleri, maliyetlerde daha fazla öngörülebilirlik sağlayan faturalandırma planları sunar. Katmanlı fiyatlandırma çok miktarda kapasite isteyen indirimli fiyatlar toocustomers sunar.

Bir plan oluşturduğunuzda, API işlem saatleri ve API işlemlerinin dahil edilen miktarı ile birlikte gelen maliyet sabit tooa uygulayın. Daha fazla dahil edilen miktar gerekli olursa, örnekleri tooyour planı ekleyebilirsiniz. Çok daha fazla dahil edilen miktar gerekli olursa, çok daha fazla dahil edilen miktar ve daha iyi bir indirimli fiyat sağlayan daha yüksek katmanlı bir plan seçebilirsiniz.

Merhaba var olan örneklerdeki dahil edilen miktarlar bitmiş olsa, hello faturalandırma planı katmanı ile ilişkili fazla kullanım oranı hello ek kullanım ücretlendirilir.

> [!NOTE]
Dahil edilen miktarlar 30 günde bir yeniden ayrılır ve kullanılmamış dahil edilen miktarlar sonraki döneme toohello alma değil.

Faturalama ve fiyatlandırma hakkında ek bilgi için bkz. [Machine Learning Fiyatlandırması](https://azure.microsoft.com/pricing/details/machine-learning/).

**Machine Learning'in ücretsiz deneme sürümü var mı?**

 Azure Machine Learning’in [Machine Learning Fiyatlandırması](https://azure.microsoft.com/pricing/details/machine-learning/) bölümünde açıklanan ücretsiz bir abonelik seçeneği vardır. Machine Learning Studio ise çok oturum açtığında kullanılabilir olan bir sekiz saatlik bir hızlı değerlendirme deneme[Machine Learning Studio](https://studio.azureml.net/?selectAccess=true&o=2).

 Ayrıca, bir ücretsiz Azure deneme sürümüne kaydolduğunuzda herhangi bir Azure hizmetini bir ay süreyle deneyebilirsiniz. hello Azure ücretsiz deneme sürümü hakkında daha fazla toolearn ziyaret [Azure ücretsiz deneme hakkında SSS](https://azure.microsoft.com/pricing/free-trial-faq/).

**İşlem nedir?**

İşlem, Azure Machine Learning’in yanıt verdiği bir API çağrısını temsil eder. İstek-Yanıt Hizmeti (RRS) ve Toplu Yürütme Hizmeti (BES) çağrılarındaki işlemler toplanır ve faturalandırma planınıza göre ücretlendirilir.

**Merhaba dahil edilen işlem miktarlarını bir plandaki RRS ve BES işlemleri için kullanabilir miyim?**

Evet, RRS ve BES işlemleriniz toplu hale getirilir ve faturalandırma planınıza göre ücretlendirilir.

**API işlem saati nedir?**

API işlem saati hello fatura API çağrıları al toorun Machine Learning kullanarak işlem kaynaklarını hello süredir birimdir. Tüm çağrılarınız faturalandırma amacıyla toplanır.

**Tipik bir üretim API'si çağrısı ne kadar sürer?**

Üretim API'si çağrı süreleri genellikle yüzlerce milisaniye tooa ile birkaç saniye arasında değişen büyük ölçüde farklılık gösterebilir. Bazı API çağrıları hello hello veri işleme karmaşıklığına ve makine öğrenimi modeline bağlı olarak dakika gerektirebilir. kez toobenchmark hello Machine Learning hizmetindeki bir modelin hello en iyi şekilde tooestimate üretim API'si çağrısı.

**Studio işlem saati nedir?**

Studio işlem saati hello fatura hello toplama süresi denemelerinizi Studio'da işlem kaynaklarını kullanmak için birimdir.

**Yeni (Azure Resource Manager tabanlı) web Hizmetleri içinde ne hello geliştirme/Test katmanının amacı nedir?**

Resource Manager tabanlı web Hizmetleri, faturalandırma planınıza tooprovision kullanabileceğiniz birden çok katmanlarını sağlar. Merhaba geliştirme ve Test fiyatlandırma katmanı tootest izin sınırlı, dahil edilen miktarlar denemenizi bir web hizmeti bir maliyet olmadan sağlar. Nasıl çalışır hello fırsat toosee sahip.

**Ayrı depolama ücretleri var mı?**

Merhaba Machine Learning ücretsiz katmanı gerektirmez veya ayrı bir depolama izin verin. Merhaba Machine Learning standart katmanı kullanıcıların toohave bir Azure depolama hesabı gerektirir. Azure Depolama [ayrı olarak faturalandırılır](https://azure.microsoft.com/pricing/details/storage/).

**Machine Learning yüksek kullanılabilirliği destekler mi?**

Evet. Ayrıntılar için bkz [Machine Learning fiyatlandırması](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) hello hizmet düzeyi sözleşmesi (SLA) açıklaması.

**Üretim API'si çağrılarım, hangi belirli türdeki işlem kaynakları üzerinde çalıştırılır?**

Merhaba Machine Learning hizmeti çok kiracılı bir hizmettir. Merhaba arka uçta kullanılan gerçek işlem kaynakları farklılık gösterir ve performans ve öngörülebilirlik için iyileştirilir.

### <a name="management-of-new-resource-manager-based-web-services"></a>Yeni (Resource Manager tabanlı) web hizmetlerinin yönetimi
**Planımı silersem ne olur?**

Merhaba plan aboneliğinizden kaldırılır ve eşit olarak bölünmüş kullanım için faturalandırılır.

> [!NOTE]
Bir web hizmeti tarafından kullanılmakta olan planları silemezsiniz. toodelete hello planı ya da atamanız gerekir yeni bir plan toohello web hizmeti veya hello web hizmetini silin.

**Plan örneği nedir?**

Plan örneği, planı faturalama tooyour ekleyebileceğiniz dahil edilen miktarlar birimidir. Faturalandırma planınız için bir faturalandırma katmanı seçtiğinizde katman bir örnek ile birlikte gelir. Daha fazla dahil edilen miktar gerekli olursa hello seçili faturalandırma katmanı tooyour planı örneklerini ekleyebilirsiniz.

**Kaç plan örneği ekleyebilirim?**

Bir abonelikte hello geliştirme/Test fiyatlandırma katmanının bir örneğine sahip olabilir.

Standart S1, Standart S2 ve Standart S3 katmanları için gerekli sayıda örnek ekleyebilirsiniz.

> [!NOTE]
Öngörülen kullanımınıza bağlı olarak, miktarları daha eklemiştir daha düşük maliyetli tooupgrade tooa katmanı olmalıdır yerine örnekleri toohello geçerli katmanı ekleyin.

**Plan katmanımı değiştirirsem (yükseltme/eski sürümü yükleme) ne olur?**

Merhaba eski plan silinir ve geçerli kullanım hello bir eşit olarak bölünmüş temelde faturalandırılır. Merhaba dahil edilen tüm miktarlarını hello yükseltilen/indirgenen katmanın içeren yeni bir plan hello dönemi hello kalanı için oluşturulur.

> [!NOTE]
Dahil edilen miktarlar her dönem ayrılır ve dahil edilen miktarların kullanılmayan kısmı sonraki döneme aktarılmaz.

**Merhaba örnekleri bir plandaki artırdığınızda ne olur?**

Miktarları bir eşit olarak bölünmüş temelde dahil edilir ve 24 saat toobe etkili sürebilir.

**Plandaki bir örneği sildiğimde ne olur?**

Merhaba örnek aboneliğinizden kaldırılır ve eşit olarak bölünmüş kullanım için faturalandırılır.

### <a name="sign-up-for-new-resource-manager-based-web-services-plans"></a>Yeni (Resource Manager tabanlı) web hizmetleri için kaydolun
**Bir plana nasıl kaydolabilirim?**

İki yolu toocreate faturalandırma planları var.

Resource Manager tabanlı bir web hizmetini ilk kez dağıtırken mevcut bir planı seçebilir ya da yeni bir plan oluşturabilirsiniz.

Bu şekilde oluşturduğunuz planlar varsayılan bölgenizdedir ve web hizmetinizi dağıtılan toothat bölge olacaktır.

Varsayılan bölgenizden başka toodeploy Hizmetleri tooregions istiyorsanız, hizmetinizi dağıtmadan önce faturalandırma planlarınızı toodefine isteyebilirsiniz.

Bu durumda, toohello Azure Machine Learning Web Hizmetleri portalında oturum açın ve toohello planlar sayfasına gidin. Buradan plan ekleyebilir, silebilir ve mevcut planları değiştirebilirsiniz.

**Hangi planı toostart kapalı ile seçmem gerekir?**

Standart S1 hello ile başlayan katmanı ve hizmetinizin kullanımını izlemek öneririz. Dahil edilen miktarlarınızı hızlıca kullandığınızı fark ettiğinizde örnek eklemek veya tooa daha yüksek katman taşıyın ve daha indirimli fiyatlar alabilirsiniz. Faturalandırma planlarınızı faturalandırma döngünüz boyunca gereken şekilde ayarlayabilirsiniz.

**Hangi bölgeleri hello yeni planları kullanılabilir?**

Merhaba yeni faturalandırma planları hello yeni web hizmetlerini desteklediğimiz hello üç üretim bölgesinde kullanılabilir:

* Orta Güney ABD
* Batı Avrupa
* Güneydoğu Asya

**Birden çok bölgede web hizmetim var. Her bölge için bir planımın olması gerekiyor mu?**

Evet. Plan fiyatlandırması bölgeye göre değişir. Bir web hizmeti tooanother bölge dağıttığınızda, tooassign gereken belirli toothat bölgedir planı bir BT. Daha fazla bilgi için bkz. [Bölgelere göre kullanılabilir ürünler]( https://azure.microsoft.com/regions/services/).

### <a name="new-web-services-overages"></a>Yeni web hizmetleri: Fazla kullanım
**Web hizmeti kullanım sınırımı aşıp aşmadığımı nasıl kontrol edebilirim?**

Tüm planlarınızdaki hello Azure Machine Learning Web Hizmetleri portalında hello planları sayfasında hello kullanımını görüntüleyin. Toohello Portalı'nda oturum açın ve hello ardından **planları** menü seçeneği.

Merhaba, **işlemleri** ve **işlem** Merhaba tablonun sütunlarının, hello planı ve kullanılan hello yüzde dahil hello miktarlarını görebilirsiniz.

**Merhaba kullandığınızda ne olacağını hello geliştirme ve Test fiyatlandırma katmanında miktarlar içerir?**

Bir geliştirme/Test katmanı atanmış toothem fiyatlandırma sahip Hizmetleri hello kadar sonraki döneme ya da Ücretli tooa katmanını taşımak kadar durdurulur.

**Klasik web hizmetleri için ve Yeni (Resource Manager tabanlı) web hizmetlerinin fazla kullanımlarında, İstek-Yanıt Hizmeti (RRS) ve Toplu İş Yürütme Hizmeti (BES) iş yükleri için fiyatlar nasıl hesaplanır?**

Bir RRS iş yükü için bu isteklerle ilişkili hello işlem süresi ve yaptığınız her API işlemi çağrısının için ücretlendirilirsiniz. RRS üretim API'si işlem maliyetleri yaptığınız API çağrıları Hello toplam sayısı (tek işlem için eşit oranda bölünmüş) 1.000 işlem başına fiyatla hello ile çarpılır olarak hesaplanır. RRS API üretim API'si işlem saati maliyetleriniz hello hello hello üretim API'si işlem saati başına fiyat ile çarpımı API işlemlerinin toplam sayısı ile çarpılır her API çağrısı toorun için gereken süreyi olarak hesaplanır.

Örneğin, standart S1 fazla her toorun 0,72 saniye sürebilir 1.000.000 API işlemi neden olacağından (1.000.000 * 0,50 ABD Doları / 1K API işlemi) 500 $ üretim API'si işlem maliyetleri ve (1.000.000 * 0.72 saniye * 2 $/ saat) 400 $olmak üretim API'si işlem içinde Toplam 900 $ için saat.

Bir BES iş yükü için hello aynı ücretlendirilen şekilde. Ancak, hello API işlem maliyetleri gönderdiğiniz toplu iş hello sayısını temsil eder ve hello işlem maliyetleri bu toplu işlerle ilişkili hello işlem süresini temsil eder. BES üretim API'si işlem maliyetleri Hello gönderilen işlerin toplam sayısı (tek işlem için eşit oranda bölünmüş) 1.000 işlem başına fiyatla hello ile çarpılır olarak hesaplanır. BES API üretim API'si işlem saati maliyetleriniz hello hello toplam hello üretim API'si hello fiyatı ile çarpılır işlerin toplam sayısı ile çarpılır işinizi satır sayısı ile çarpılır, iş toorun her satır için gereken süreyi olarak hesaplanır. saat işlem. Merhaba Machine Learning hesaplayıcısı kullandığınızda, her iş toorun tüm satırlarda için gerekli olan zamanı hello işlem ölçer temsil hello toosubmit planlamak ve hello hello işlem başına zaman alanını temsil eden işlerin sayısı birleşik.

Örneğin, Standart S1 fazla kullanımı gerçekleştiğini ve günlük her biri 0,72 saniye süren 500’er satırdan oluşan 100 iş gönderdiğinizi varsayalım. Aylık fazla kullanım maliyetleriniz üretim API’si işlem maliyetlerinden (günde 100 iş = 3.100 iş/ay  0,50 $/1000 API işlemi) 1,55 $ ve üretim API’si işlem saatlerinden (500 satır  0,72 saniye  3.100 İş  2 $/sa) 620 $ olmak üzere toplam 621,55 $ olur.

### <a name="azure-machine-learning-classic-web-services"></a>Azure Machine Learning Klasik web hizmetleri
**Kullandıkça Öde seçeneği hâlâ mevcut mu?**

Evet, Azure Machine Learning’de Klasik web hizmetleri hala kullanılabilmektedir.  

### <a name="azure-machine-learning-free-and-standard-tier"></a>Azure Machine Learning Ücretsiz ve Standart katmanı
**Hello Azure Machine Learning ücretsiz katmanına neler dahildir?**

Hello Azure Machine Learning ücretsiz katmanı hedeflenen tooprovide ayrıntılı giriş toohello Azure Machine Learning Studio'da ' dir. Tek ihtiyacınız olan bir Microsoft hesabı toosign ayarlama. Merhaba ücretsiz katmanı içeren ücretsiz erişim tooone Azure Machine Learning Studio çalışma başına [Microsoft hesabı](https://www.microsoft.com/account/default.aspx). Bu katman ' too10 GB depolama kullanabilir ve modelleri hazırlama API'leri olarak faaliyete. Ücretsiz katmanı iş yükleri bir SLA kapsamında değildir ve yalnızca geliştirme ve kişisel kullanım amaçlıdır. 

Ücretsiz katmanı çalışma alanları hello aşağıdaki sınırlamalar vardır:

* İş yükleri, SQL Server çalıştıran tooan şirket içi sunucusuna bağlanarak verilere erişemez.
* Yeni Resource Manager temel web hizmetleri dağıtılamaz.


**Hello Azure Machine Learning standart katmanına ve planlarına neler dahildir?**

Hello Azure Machine Learning standart katmanı, Azure Machine Learning Studio'nun Ücretli üretim sürümüdür. Hello Azure Machine Learning Studio aylık ücret faturalandırılır üzerinde bir çalışma alanı başına temelinde ve kısmi aylar için eşit oranda bölünür. Azure Machine Learning Studio deneme saatleri, etkin deneme için işlem saati başına faturalandırılır. Fatura, kısmi saatler için eşit olarak bölünür.  

Hello Azure Machine Learning API'si hizmeti, Klasik web hizmeti veya yeni bir (Resource Manager tabanlı) web hizmeti olmasına bağlı olarak faturalandırılır.

ücretler aşağıdaki hello aboneliğiniz için çalışma alanı başına toplanır.

* Machine Learning çalışma alanı aboneliği: hello Machine Learning çalışma alanı abonelik erişim tooa Machine Learning Studio çalışma sağlayan bir aylık ücrettir. Merhaba abonelik gerekli toorun denemeler hello studio ve tooutilize hello üretim API'lerini ' dir.
* Studio deneme saatleri: Bu ölçer Machine Learning Studio'da denemeleri çalıştırarak tahakkuk eden tüm işlem ücretlerini toplar ve çalışan üretim API çağrılarının hello ortam hazırlama.
* Tooan şirket içi modelleriniz eğitim için SQL Server çalıştıran bir sunucuya bağlanmayı ve puanlama verilere erişin.
* Klasik web hizmetleri için:
  * Üretim API’si İşlem Saatleri: Bu ölçüm, üretimde çalışan web hizmetlerinden doğan işlem ücretlerini içerir.
  * Üretim API'si işlemleri (1000'lik bloklar): Bu ölçüm çağrısı tooyour üretim web hizmeti tahakkuk eden ücretleri içerir.

Resource Manager tabanlı web hizmeti hello durumda ücretler, önceki hello dışında toplanmış toohello seçili plan ücretleri şunlardır:

* Standart S1/S2/S3 API planı (birimler): Bu ölçer hello Resource Manager tabanlı web hizmetleri için seçilen örneğin türünü temsil eder.
* Standart S1/S2/S3 fazla kullanım API'si işlem saatleri: Bu ölçüm dahil hello varolan durumlarda miktarlar tüketildikten sonra üretimde çalışan bir Resource Manager tabanlı web hizmetleri doğan işlem ücretlerini içerir. Merhaba ek kullanım ücretlendirilir adresindeki hello S1/S2/S3 plan katmanıyla ilişkili oranı ücretlendirilir.
* Standart S1/S2/S3 fazla kullanım API'si işlemleri (1.000 saniye): Bu ölçüm çağrısı tooyour üretim hello varolan durumlarda sayılarına dahil sonra Resource Manager tabanlı web hizmeti yukarı kullanılır başına tahakkuk eden ücretleri içerir. Merhaba ek kullanım adresindeki doludur hello S1/S2/S3 plan katmanıyla ilişkili oranı ücretlendirilir.
* Dahil edilen miktar API işlem saatleri: Resource Manager tabanlı web Hizmetleri ile bu ölçer API işlem saatleri hello dahil edilen miktarını temsil eder.
* Miktar API işlemleri (1.000) dahil: Resource Manager ile tabanlı web Hizmetleri, bu ölçer hello dahil edilen miktar API işlemlerinin temsil eder.

**Azure Machine Learning Ücretsiz katmanına nasıl kaydolabilirim?**

Tek ihtiyacınız olan bir Microsoft hesabıdır. Çok Git[Azure Machine Learning giriş](https://azure.microsoft.com/services/machine-learning/)ve ardından **Şimdi Başlat**. Microsoft hesabınızla oturum açtığınızda Ücretsiz katmanında sizin için bir çalışma alanı oluşturulur. Tooexplore başlatın ve hemen Machine Learning denemeleri oluşturun.

**Azure Machine Learning Standart katmanına nasıl kaydolabilirim?**

Standart Machine Learning çalışma alanına erişim tooan Azure aboneliği toocreate öncelikle olması gerekir. 30 günlük ücretsiz deneme Azure aboneliği için kaydolabilir ve daha sonra yükseltme tooa Ücretli Azure aboneliği veya Ücretli bir Azure aboneliğinizin hemen satın alabilirsiniz. Erişim toohello abonelik elde ettikten sonra sonra hello Microsoft Azure Klasik portalından bir Machine Learning çalışma alanı oluşturabilirsiniz. Görünüm hello [adım adım yönergeler](https://azure.microsoft.com/trial/get-started-machine-learning-b/).

Alternatif olarak, bir standart Machine Learning çalışma alanı sahibi tooaccess hello sahibin çalışma alanına göre davet.

**Kendi Azure Blob Depolama hesabı toouse hello ücretsiz katmanı ile belirtebilir miyim?**

Hayır, hello standart katmanı eşdeğer toohello hello hello Katmanlar sunulmadan önce kullanılabilir Machine Learning hizmeti sürümüdür.

**Modelleri hello ücretsiz katmanında API olarak öğrenme Makinem dağıtabilir miyim?**

Evet, faaliyete machine learning modellerini toostaging API Hizmetleri hello ücretsiz katmanının bir parçası. tooput API hizmetini üretime hazırlama hello ve kullanıma hazır hale getirilmiş hello hizmeti için bir üretim uç noktası Al, hello standart katmanını kullanmanız gerekir.

**Hello Azure ücretsiz deneme sürümü ve Azure Machine Learning ücretsiz katmanı arasındaki fark nedir?**

Merhaba [Microsoft Azure ücretsiz deneme sürümü](https://azure.microsoft.com/free/) tooany Azure uygulayabilirsiniz krediler bir aylık hizmet sunar. Hello Azure Machine Learning ücretsiz katmanı teklifleri sürekli özellikle tooAzure Machine Learning üretim dışı iş yükleri için erişim.

**Merhaba ücretsiz katmanı toohello standart Katmanı'ndan nasıl bir denemeyi hareket?**

toocopy hello ücretsiz katmanı toohello standart katmanı denemelerinizden:

1. TooAzure Machine Learning Studio'da oturum ve hello ücretsiz çalışma ve standart çalışma hello üst gezinti çubuğundaki çalışma alanı seçicisinde hello hello görebildiğinizden emin olun.
2. Merhaba standart çalışma alanındaysanız tooFree çalışma geçin.
3. Merhaba deneme listesi görünümünde, gibi toocopy ve hello'ı tıklatın, bir denemeyi seçin **kopyalama** komut düğmesi.
4. Açılır hello iletişim kutusundan Hello standart çalışma alanını seçin ve hello ardından **kopyalama** düğmesi.
   Tüm ilişkili veri kümeleri Merhaba, eğitilen model vb. birlikte hello deneme hello standart çalışma alanına kopyalanır.
5. Toorerun ihtiyacınız hello deneme ve web hizmetinizi standart çalışma hello yeniden yayımlayın.

### <a name="studio-workspace"></a>Studio çalışma alanı
**Farklı çalışma alanları için farklı faturalar görür müyüm?**

Çalışma alanı ücretleri tek bir fatura üzerinde, geçerli olan her bir ölçüm için ayrıca listelenir.

**Denemelerim hangi belirli türdeki işlem kaynakları üzerinde çalıştırılacak?**

Merhaba Machine Learning hizmeti çok kiracılı bir hizmettir. Merhaba arka uçta kullanılan gerçek işlem kaynakları farklılık gösterir ve performans ve öngörülebilirlik için iyileştirilir.

### <a name="guest-access"></a>Konuk Erişimi
**Konuk erişimi tooAzure Machine Learning Studio nedir?**

Konuk Erişimi kısıtlı bir deneme deneyimidir. Azure Machine Learning Studio’da herhangi bir maliyet olmadan ve kimlik doğrulaması gerçekleştirmeden denemeler oluşturup çalıştırabilirsiniz. Konuk oturumları kalıcı değildir (kaydedilemez) ve sınırlı tooeight saat. Diğer sınırlamalar ise R ve Python desteğinin olmaması, hazırlık API’lerinin olmaması, kısıtlı veri kümesi boyutu ve kısıtlı depolama kapasitesidir. Karşılaştırma toosign bir Microsoft hesabıyla seçen kullanıcılar Machine Learning daha önce açıklanan kalıcı bir çalışma alanı ile daha kapsamlı özellikler içeren Studio'nun toohello ücretsiz katmanı tam erişimi vardır. Ücretsiz Machine Learning toochoose deneyimi tıklatın **başlamak** üzerinde [https://studio.azureml.net](https://studio.azureml.net)ve ardından **tahmin erişim** ya da oturum açın. Microsoft hesabı.

<!-- Module References -->
[image-reader]: https://msdn.microsoft.com/library/azure/893f8c57-1d36-456d-a47b-d29ae67f5d84/
[join]: https://msdn.microsoft.com/library/azure/124865f7-e901-4656-adac-f4cb08248099/
[machine-learning-modules]: https://msdn.microsoft.com/library/azure/6d9e2516-1343-4859-a3dc-9673ccec9edc/
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[python]: https://msdn.microsoft.com/library/azure/CDB56F95-7F4C-404D-BDE7-5BB972E6F232
[counts]: https://msdn.microsoft.com/library/azure/dn913056.aspx
