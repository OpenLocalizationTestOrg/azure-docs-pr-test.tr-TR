---
title: Azure Machine Learning aaaALM | Microsoft Docs
description: "Azure Machine Learning Studio uygulama yaşam döngüsü yönetimi en iyi yöntemleri uygulayın"
keywords: "ALM, AML, Azure ML, uygulama yaşam döngüsü yönetimi, sürüm denetimi"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1be6577d-f2c7-425b-b6b9-d5038e52b395
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: haining
ms.openlocfilehash: 99470ff72fea7ab59d9d44f3fded7b9dd49a38c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-lifecycle-management-in-azure-machine-learning-studio"></a>Azure Machine Learning Studio'da uygulama yaşam döngüsü yönetimi
Azure Machine Learning Studio, hello Azure bulut platformunda kullanıma hazır hale getirilmiş, machine learning denemelerini geliştirmek için kullanılan bir araçtır. Bu, Visual Studio IDE ve tek bir platformuna birleştirilmiş ölçeklenebilir bulut hizmeti hello gibi olur. Azure Machine Learning Studio'ya çeşitli varlıklar tooautomated yürütme ve dağıtım, standart uygulama yaşam döngüsü yönetimi (ALM) uygulamaları, sürüm oluşturma'yı ekleyebilirsiniz. Bu makalede hello seçenekleri ve yaklaşımlar bazıları açıklanmaktadır.

## <a name="versioning-experiment"></a>Sürüm oluşturma deneme
Denemelerinizi iki önerilen yöntemler tooversion vardır. Yerleşik çalıştırma geçmişi, bağlı veya JavaScript nesne gösterimi (JSON) biçiminde hello deneme dışarı aktarma ve harici olarak yönetin. Her iki yaklaşımın kendi Artıları ve eksileri ile gelir.

### <a name="experiment-snapshots-using-run-history"></a>Çalıştırma geçmişi kullanarak deneme anlık görüntüler
Hello Azure Machine Learning Studio'da öğrenme deneme hello her tıkladığınızda, hello yürütme modeli **çalıştırmak** hello deneme düzenleyicisinde değişmez bir anlık görüntüsünü hello deneme düğmesine olduğu gönderilen toohello İş Zamanlayıcısı. Bu anlık görüntü listesi hello tıklayarak görüntüleyebilirsiniz **çalıştırma geçmişi** hello komut çubuğunda hello deneme Düzenleyici görünümünde düğmesi.

![Çalıştırma geçmişi düğmesi](media/machine-learning-version-control/runhistory.png)

Daha sonra gönderilen toorun açık hello anlık görüntü hello deneme hello zaman hello deneme sırasında hello adını tıklatarak kilitli modunda olan ve hello anlık görüntü alındıktan. Yalnızca hello geçerli deneme temsil eder, hello listesindeki ilk öğeyi hello bildirimi düzenlenebilir bir durumda. Ayrıca her anlık görüntü çeşitli durumunda olabilir bildirim de dahil olmak üzere tamamlandı (kısmi) çalıştırın, başarısız, başarısız (kısmi) çalıştırmak, durumları ya da taslak.

![Geçmiş listesini çalıştırın.](media/machine-learning-version-control/runhistorylist.png)

Bunu açıldıktan sonra hello anlık görüntü deney yeni bir deneme kaydedin ve sonra değiştirebilirsiniz. Deneme anlık görüntünüz güncelleştirilmiş sürümlerini varlıklar eğitilen model, dönüştürme ya da veri kümesi gibi içeriyorsa, hello anlık görüntü durumdayken hello anlık görüntü hello başvuruları toohello özgün sürümü korur. Kilitli hello kaydederseniz, yeni bir deneme anlık görüntü Azure Machine Learning Studio bu varlıkları daha yeni bir sürümü hello varlığını algılar ve bunları yeni bir deneme hello içinde otomatik olarak güncelleştirir.

Merhaba deneme silerseniz, bu deneme tüm anlık görüntüleri silinir.

### <a name="exportimport-experiment-in-json-format"></a>JSON biçiminde içeri/dışarı aktarma deneme
gönderilen toorun olduğu her zaman çalıştır hello geçmiş anlık görüntüleri Azure Machine Learning Studio'da bir değişmez hello deneme sürümünü tutun. Ayrıca hello deneme yerel bir kopyasını kaydedin ve Team Foundation Server gibi tooyour sık kullanılan kaynak denetim sistemi iade ve daha sonra bu yerel dosyadan bir denemeyi yeniden oluşturun. Merhaba kullanabilirsiniz [Azure Machine Learning PowerShell](http://aka.ms/amlps) cmdlet'leri [ *verme AmlExperimentGraph* ](https://github.com/hning86/azuremlps#export-amlexperimentgraph) ve [  *İçeri aktarma AmlExperimentGraph* ](https://github.com/hning86/azuremlps#import-amlexperimentgraph) tooaccomplish.

Merhaba JSON hello metinsel gösterimini denemeler başvuru tooassets bir veri kümesi veya bir modeli gibi hello çalışma alanında içerebilir grafik dosyasıdır. Seri hale getirilmiş bir hello varlık sürümü içermiyor. Geri hello çalışma alanına tooimport hello JSON belgesi çalışırsanız, başvurulan hello varlıklar hello ile aynı varolmalıdır varlık hello denemesinde başvurulan kimlikleri. Aksi takdirde mümkün tooaccess içeri hello deneme olmaz.

## <a name="versioning-trained-model"></a>Sürüm oluşturma eğitilen modeli
Bir Azure Machine Learning eğitilen model .iLearner dosyası olarak bilinen bir biçime serileştirilmiş ve hello çalışma alanıyla ilişkilendirilmiş hello Azure Blob Depolama hesabında depolanır. Tek yönlü tooget hello .iLearner dosyasının bir kopyasını API yeniden eğitme hello ' dir. [Bu makalede](machine-learning-retrain-models-programmatically.md) API yeniden eğitme hello nasıl çalıştığını açıklar. Merhaba üst düzey adımları şunlardır:

1. Eğitim denemenizi ayarlayın.
2. Bir web hizmeti çıkış bağlantı noktasına toohello Train Model modülü veya Model Hyperparameter ayarlamak veya R modeli oluşturma gibi hello eğitilen model üreten hello modülü ekleyin.
3. Eğitim denemenizi çalıştırın ve ardından bir model eğitim web hizmeti olarak dağıtabilirsiniz.
4. Merhaba hello eğitim web hizmeti uç noktası BES çağırın ve hello istenen .iLearner dosya adı ve Blob Depolama hesabı konumu depolanacağı yeri belirtin.
5. Merhaba BES çağırdıktan sonra toplama üretilen hello .iLearner dosya tamamlanır.

Başka bir şekilde tooretrieve hello .iLearner hello PowerShell komutunu dosyasıdır [ *indirme AmlExperimentNodeOutput*](https://github.com/hning86/azuremlps#download-amlexperimentnodeoutput). Bu, yalnızca bir kopyasını hello .iLearner dosya hello gerek tooretrain hello model program aracılığıyla tooget istiyorsanız daha kolay olabilir.

Merhaba, eğitilen modeli içeren hello .iLearner dosyasını oluşturduktan sonra daha sonra kendi Sürüm stratejisi tercih edebilirsiniz. Merhaba stratejisi öncesi/sonek bir adlandırma kuralı olarak uygulama ve yalnızca Blob Depolama hello .iLearner dosyasında bırakarak ya da kopyalama/sürüm denetimi sisteminize almadan olarak kadar basit olabilir.

Merhaba kaydedilmiş .iLearner dosyası sonra dağıtılmış web Hizmetleri aracılığıyla Puanlama için kullanılabilir.

## <a name="versioning-web-service"></a>Sürüm oluşturma web hizmeti
Bir Azure Machine Learning deneme web hizmetlerinden iki tür dağıtabilirsiniz. Merhaba Klasik web hizmeti hello çalışma yanı sıra hello deneme ile sıkı şekilde bağlı. artık hello özgün deneme veya hello çalışma ile bağlı ve hello Azure Resource Manager framework Hello yeni web hizmetini kullanır.

### <a name="classic-web-service"></a>Klasik web hizmeti
Klasik web hizmeti tooversion hello web hizmeti uç noktası yapısı, avantajından yararlanabilirsiniz. Tipik bir akışı şöyledir:

1. Tahmine dayalı denemenizi varsayılan bir uç içeren yeni bir Klasik web hizmeti dağıtın.
2. Hello hello deneme ve eğitilmiş model geçerli sürümü kullanıma sunan ep2 adlı yeni bir uç noktası oluşturun.
3. Geri dönün ve Tahmine dayalı denemeye ve eğitilen model güncelleştirin.
4. Ardından hello varsayılan uç güncelleştirecektir hello Tahmine dayalı denemeye yeniden dağıtın. Ancak bu ep2 değiştirmez.
5. Merhaba yeni sürümünü hello deneme ve eğitilen modelini gösterir ep3 adlı başka bir uç nokta oluşturun.
6. Toostep 3 gerekirse dönün.

Zaman içinde çok sayıda uç nokta oluşturuldu olabilir hello aynı web hizmeti. Her uç nokta hello zaman içinde nokta hello eğitilen model sürümünü içeren hello deneme zaman noktası kopyasını temsil eder. Modeli Puanlama hello çalışma için etkili bir şekilde hello bir sürümünü seçerek anlamına gelir hangi uç nokta toocall eğitilmiş dış mantığı toodetermine sonra kullanabilirsiniz.

Birçok aynı web hizmeti uç noktalarını da oluşturabilir ve hello .iLearner dosya toohello uç nokta tooachieve benzer etkisi farklı sürümlerini düzeltme eki. [Bu makalede](machine-learning-create-models-and-endpoints-with-powershell.md) daha ayrıntılı olarak açıklanmaktadır nasıl tooaccomplish.

### <a name="new-web-service"></a>Yeni web hizmeti
Yeni Azure Resource Manager tabanlı web hizmeti oluşturursanız, hello uç nokta yapı artık mevcut değil. Bunun yerine, web hizmeti tanımının (WSD) dosyaları, JSON biçiminde hello kullanarak Tahmine dayalı denemenizi oluşturabilirsiniz [verme AmlWebServiceDefinitionFromExperiment](https://github.com/hning86/azuremlps#export-amlwebservicedefinitionfromexperiment) PowerShell komutunu veya hello kullanarak[ *Verme AzureRmMlWebservice* ](https://msdn.microsoft.com/library/azure/mt767935.aspx) PowerShell komutunu dağıtılmış Resource Manager tabanlı web hizmeti.

Dışarı hello sonra WSD dosya ve sürüm denetimi, ayrıca hello WSD yeni bir web hizmeti olarak farklı bir Azure bölgesindeki farklı bir web hizmeti planındaki dağıtabilirsiniz. Yalnızca yapılandırmanın yanı sıra hello hizmet planı kimliği yeni web hello uygun depolama hesabı sağladığınız emin olun toopatch farklı .iLearner dosyalarında hello WSD dosyasını değiştirebilirsiniz ve güncelleştirme hello konum başvurusu hello eğitilmiş model ve yeni bir web hizmeti olarak dağıtabilir.

## <a name="automate-experiment-execution-and-deployment"></a>Deneme yürütme ve dağıtımı otomatik hale getirme
Bir önemli ALM toobe mümkün tooautomate hello yürütme ve dağıtım sürecindeki hello uygulamasının yönüdür. Azure Machine Learning ile bunu hello kullanarak gerçekleştirebilirsiniz [PowerShell Modülü](http://aka.ms/amlps). İlgili tooa standart otomatik ALM yürütme/dağıtım işlemi hello kullanarak uçtan uca adımları bir örneği burada verilmiştir [Azure Machine Learning Studio PowerShell Modülü](http://aka.ms/amlps). Her, bağlantılı tooone veya bu adım, tooaccomplish kullanabileceğiniz daha fazla PowerShell cmdlet'leri adımdır.

1. [Bir veri kümesi karşıya](https://github.com/hning86/azuremlps#upload-amldataset).
2. Merhaba çalışma alanından bir eğitim denemenizi kopyalayın bir [çalışma](https://github.com/hning86/azuremlps#copy-amlexperiment) veya [galeri](https://github.com/hning86/azuremlps#copy-amlexperimentfromgallery), veya [alma](https://github.com/hning86/azuremlps#import-amlexperimentgraph) bir [dışarı](https://github.com/hning86/azuremlps#export-amlexperimentgraph) gelen denemeler Yerel disk.
3. [Merhaba dataset güncelleştirme](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) hello eğitim denemenizi içinde.
4. [Merhaba eğitim denemeyi çalıştırın](https://github.com/hning86/azuremlps#start-amlexperiment).
5. [Merhaba, eğitilen modeli yükseltmek](https://github.com/hning86/azuremlps#promote-amltrainedmodel).
6. [Tahmine dayalı denemeye kopyalama](https://github.com/hning86/azuremlps#copy-amlexperiment) hello çalışma alanına.
7. [Güncelleştirme hello eğitilen modeli](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) hello Tahmine dayalı denemeye içinde.
8. [Merhaba Tahmine dayalı denemeyi çalıştırın](https://github.com/hning86/azuremlps#start-amlexperiment).
9. [Bir web hizmetini dağıtma](https://github.com/hning86/azuremlps#new-amlwebservice) hello Tahmine dayalı denemeye gelen.
10. Test hello web hizmeti [RRS](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) veya [BES](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint) uç noktası.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba karşıdan [Azure Machine Learning Studio PowerShell](http://aka.ms/amlps) modülü ve başlangıç tooautomate ALM görevlerinizi.
* Nasıl çok öğrenin[oluşturmak ve yalnızca tek bir deneme kullanarak ML modelleri çok sayıda yönetmek](machine-learning-create-models-and-endpoints-with-powershell.md) PowerShell ve API yeniden eğitme aracılığıyla.
* Daha fazla bilgi edinmek [Azure Machine Learning web hizmetlerini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).
