---
title: "Azure Hdınsight sunucusuna aaaIntroduction tooR | Microsoft Docs"
description: "Bilgi nasıl toouse R Server Hdınsight toocreate uygulamaları büyük veri analizi için."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6dc21bf5-4429-435f-a0fb-eea856e0ea96
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: daf7b70a15748d66510a04da370f39c5f26eb4ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#<a name="introduction-toor-server-and-open-source-r-capabilities-on-hdinsight"></a>Giriş tooR sunucu ve açık kaynak hdınsight'ta R özellikleri

Azure Hdınsight kümeleri oluşturduğunuzda Microsoft R Server bir dağıtım seçeneği olarak kullanılabilir. Bu yeni özellik, veri bilimcilerine, istatistikçiler ve dağıtılmış yöntemlerinin analytics hdınsight'ta R programcıları isteğe bağlı erişim tooscalable ile sağlar.

Kümeleri olabilir toohello projeleri ve elinizdeki görevleri uygun şekilde boyutlandırılmış ve artık gerekmediğinde sonra bozuk. Azure Hdınsight parçası olup olmadıklarını olduğundan, bu kümeleri kuruluş düzeyinde 7/24 destek, % 99,9 çalışma süresi, SLA'sı ile gelir ve diğer bileşenler hello Azure ekosistemi ile özelliği toointegrate hello.

Hdınsight'ta R Server neredeyse tüm boyutu, yüklenen tooeither Azure Blob veya Data Lake storage kümelerinde R tabanlı analizi için hello son yetenekleri sağlar. R Server açık kaynak R kurulu olduğundan, yapı hello R tabanlı uygulamalar hello 8000 + R açık kaynak paketlerinden birini yararlanabilirsiniz. ScaleR, Microsoft'un büyük veri analizi paket R Server ile gelen Hello çalışmalarında de kullanılabilir.

kümenin Hello kenar düğümü uygun bir yer tooconnect toohello küme ve toorun R komut dosyalarınızı sağlar. Bir kenar düğümüne ile Merhaba Çekirdeğinde hello kenar düğümü sunucusunun ScaleR hello paralel birkaç ölçeklendirin çalışan hello seçeneğini dağıtılmış işlevlerini sahip. Ayrıca bunları hello hello küme düğümleri arasında ScaleR'ın eşlemesi Hadoop azaltın veya Spark kullanarak işlem bağlamları çalıştırabilirsiniz.

Merhaba modelleri veya çözümlemeler sonucundan indirilebilir tahminleri şirket içi kullanın. Bunlar ayrıca başka bir yerde Azure'da, özellikle aracılığıyla operationalized [Azure Machine Learning Studio](http://studio.azureml.net) [web hizmeti](../machine-learning/machine-learning-publish-a-machine-learning-web-service.md).

## <a name="get-started-with-r-on-hdinsight"></a>Hdınsight'ta R kullanmaya başlama
R Server tooinclude bir Hdınsight kümesindeki hello Azure portal kullanarak bir Hdınsight kümesi oluştururken hello R Server küme türü seçmelisiniz. Merhaba R Server küme türü R Server hello veri hello küme düğümlerinin ve R Server tabanlı analiz için giriş bölgesi görevi gören bir edge düğümünü içerir. Bkz: [hdınsight'ta R Server ile çalışmaya başlama](hdinsight-hadoop-r-server-get-started.md) nasıl toocreate hello küme üzerinde bir gözden geçirme.

## <a name="learn-about-data-storage-options"></a>Veri depolama seçenekleri hakkında bilgi edinin
Hdınsight kümeleri hello HDFS dosya sistemi için varsayılan depolama bir Azure Storage hesabı veya bir Azure Data Lake deposu ile ilişkili olabilir. Bu ilişkilendirme hangi verilerin karşıya yüklendiğini sağlar toohello küme depolama Çözümleme sırasında kalıcı yapılır. Merhaba depolama hesabı ve hello hello portal tabanlı karşıya yükleme olanağı dahil olmak üzere seçtiğiniz hello veri aktarımı toohello depolama seçeneği işlemek için çeşitli araçlar vardır [AzCopy](../storage/common/storage-use-azcopy.md) yardımcı programı.

Sağlama işlemi hello birincil depolama seçeneği kullanımda bakılmaksızın hello küme sırasında erişim tooadditional Blob ve Data lake depoları ekleme hello seçeneğiniz vardır. Bkz: [hdınsight'ta R Server kullanmaya başlama](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-get-started) erişim tooadditional hesapları ekleme hakkında bilgi için. Merhaba tamamlayıcı bkz [hdınsight'ta R Server için Azure Depolama Seçenekleri](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-storage) birden çok depolama hesabı kullanma hakkında daha fazla makale toolearn.

Aynı zamanda [Azure dosyaları](../storage/files/storage-how-to-use-files-linux.md) hello kenar düğümünü kullanmak için bir depolama seçeneği olarak. Azure dosyaları toomount Azure Storage toohello Linux dosya sistemi oluşturulmuş bir dosya paylaşımı sağlar. Hdınsight kümesi R Server için bu veri depolama seçenekleri hakkında daha fazla bilgi için bkz: [Azure depolama seçenekleri hdınsight'ta R Server kümeleri için](hdinsight-hadoop-r-server-storage.md).

## <a name="access-r-server-on-hello-cluster"></a>Erişim R hello küme sunucusunda
Sağladığınız bir tarayıcı kullanarak hello kenar düğümüne sunucuda tooinclude Rstudio'dan sunucu hello sağlama işlemi sırasında seçtiğiniz tooR bağlanabilir. Bu hello küme sağlamada yüklemediyseniz, daha sonra ekleyebilirsiniz. Bir küme oluşturulduktan sonra Rstudio'dan sunucusu yükleme hakkında daha fazla bilgi için bkz: [Hdınsight kümelerinde Rstudio'dan Server'ı yükleme](hdinsight-hadoop-r-server-install-r-studio.md). R Server toohello SSH/PuTTY tooaccess hello R konsolunu kullanarak da bağlanabilirsiniz. 

## <a name="develop-and-run-r-scripts"></a>Geliştirme ve R komut dosyalarını çalıştır
oluşturma ve çalıştırma hello R betiklerini toplama toohello açık kaynak R paketler paralel birkaç ölçeklendirin ve hello ScaleR Kitaplığı'nda yordamları dağıtılan hello 8000 + birini kullanabilirsiniz. Genel olarak, R Server ile Merhaba kenar düğümü üzerinde çalışacak bir betik içinde hello R yorumlayıcı bu düğüm üzerinde çalışır. Merhaba, toocall tooHadoop eşleme (RxHadoopMR) azaltın veya Spark (RxSpark) ayarlanmış bir işlem bağlamı ScaleR işleviyle gereken adımları durumlardır. Bu durumda, hello işlevi başvurulan hello verileriyle ilişkili olan bu verileri (görev) hello kümenin düğümleri arasında dağıtılmış bir şekilde çalışır. Merhaba farklı işlem bağlamı seçenekleri hakkında daha fazla bilgi için bkz: [işlem hdınsight'ta R Server için içerik seçeneklerini](hdinsight-hadoop-r-server-compute-contexts.md).

## <a name="operationalize-a-model"></a>Bir model faaliyete
Veri modellemesi tamamlandığında hello modeli toomake tahminleri Azure ve şirket içi'nden ya da yeni veriler için faaliyete geçirebilirsiniz. Bu işlem Puanlama olarak bilinir. Puanlama Hdınsight, Azure Machine Learning veya şirket içi yapılabilir.

### <a name="score-in-hdinsight"></a>Hdınsight'ta puan
Hdınsight, tooscore tooyour depolama hesabı yüklenen, modeli toomake tahminleri yeni bir veri dosyası için çağıran bir R işlevi yazma. Daha sonra geri toohello depolama hesabı hello tahminleri kaydedin. Merhaba rutin isteğe bağlı hello kenar düğümüne kümenizin veya zamanlanmış bir iş kullanarak çalıştırabilirsiniz.  

### <a name="score-in-azure-machine-learning-aml"></a>Puan azure'da makine öğrenme (AML)
kullanarak bir AML web hizmeti, kullanım hello tooscore açık olarak bilinen kaynak Azure Machine Learning R paketi [AzureML](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) toopublish modelinizi bir Azure web hizmeti olarak. Kolaylık olması için bu paket hello kenar düğümüne önceden büyük/küçük harf yüklenir. Ardından, Machine Learning toocreate bir kullanıcı arabirimi hello tesislerde hello web hizmetini kullanın ve ardından Puanlama için gerektiği şekilde hello web hizmetini çağırmak.

Bu seçeneği seçerseniz, hello web hizmetiyle herhangi ScaleR model nesneleri tooequivalent açık kaynak modeli nesneleri için kullanılmak tooconvert gerekir. ScaleR zorlama işlevleri gibi kullandığınız `as.randomForest()` bu dönüştürme için ensemble tabanlı modelleri için.

### <a name="score-on-premises"></a>Puan şirket içi
tooscore modelinizi oluşturduktan sonra şirket içi, R, seri durumdan ve yeni veri Puanlama kullanmak indirme hello modelinde seri hale getirebilir. Daha önce açıklanan hello yaklaşımı kullanarak, yeni verilerinizi puanlamada [Hdınsight'ta Puanlama](#scoring-in-hdinsight) veya kullanarak [DeployR](https://deployr.revolutionanalytics.com/).

## <a name="maintain-hello-cluster"></a>Merhaba küme koru
### <a name="install-and-maintain-r-packages"></a>Yükleme ve R paketleri koru
Kullandığınız hello R paketleri çoğunu hello kenar düğümüne var. çalıştırmak, R betiklerini çoğu adımları bu yana gereklidir. tooinstall ek R paketlerini hello kenar düğümünü, kullanabileceğiniz hello normal `install.packages()` r yöntemi

Yalnızca yordamları hello ScaleR Kitaplığı'ndan hello küme üzerinde kullanıyorsanız, tooinstall ek R paketleri hello veri düğümlerde genellikle gerekmez. Ancak, ek paketler toosupport hello kullanımını gerekebilecek **rxExec** veya **RxDataStep** hello veri düğümlerde yürütme.

Merhaba küme oluşturduktan sonra bu durumlarda, bir komut dosyası eylemi hello ek paketler yüklenebilir. Daha fazla bilgi için bkz: [R sunucusuyla bir Hdınsight kümesi oluşturma](hdinsight-hadoop-r-server-get-started.md).   

### <a name="change-hadoop-map-reduce-memory-settings"></a>Harita Hadoop azaltmak bellek ayarlarını değiştirme
Bir küme değiştirilmiş toochange hello bir harita azaltmak işi çalıştırılırken kullanılabilir tooR sunucu bellek miktarı olabilir. bir küme toomodify hello hello kümeniz için Azure portal dikey penceresi aracılığıyla kullanılabilir Apache Ambari UI kullanın. Tooaccess Ambari UI kümeniz için nasıl hello hakkında yönergeler için bkz: [hello Ambari Web kullanıcı arabirimini kullanarak yönetin Hdınsight kümelerini](hdinsight-hadoop-manage-ambari.md).

Bu da olası toochange hello hello çağrıda çok Hadoop anahtarlarını kullanarak kullanılabilir tooR sunucu olan bellek miktarıdır**RxHadoopMR** gibi:

    hadoopSwitches = "-libjars /etc/hadoop/conf -Dmapred.job.map.memory.mb=6656"  

### <a name="scale-your-cluster"></a>Kümenizi ölçeklendirme
Varolan bir kümeye yukarı veya aşağı hello portalı üzerinden genişletilebilir. Ölçeklendirme, büyük işleme görevler için gereksinim duyabileceğiniz ek kapasite hello elde edebilirsiniz veya boşta olduğunda, bir küme geri ölçeklendirebilirsiniz. Hakkında yönergeler için tooscale bir küme bkz [Hdınsight kümelerini yönetme](hdinsight-administer-use-portal-linux.md).

### <a name="maintain-hello-system"></a>Merhaba sistem koru
Bakım tooapply OS düzeltme ekleri ve diğer güncelleştirmeleri saatlerde bir Hdınsight kümesinde Linux VM'ler temel hello üzerinde gerçekleştirilir. Genellikle, bakım 03:30 da (Merhaba VM hello yerel saate bağlı olarak) her Pazartesi ve Salı yapılır. Güncelleştirmeleri, birden fazla çeyreği hello küme birer birer etkisi yoktur şekilde gerçekleştirilir.  

Merhaba baş düğümler yedekli ve tüm veri düğümleri etkilenen olduğundan, bu süre boyunca çalıştıran herhangi bir işi yavaşlayabilir. Bunlar hala toocompletion, ancak çalışması gerekir. Yıkıcı bir hata, bir küme yeniden oluşturma gerektiren oluşmadığı sürece bu bakım olaylar arasında herhangi bir özel yazılım veya sahip olduğunuz yerel veriler korunur.

## <a name="learn-about-ide-options-for-r-server-on-an-hdinsight-cluster"></a>Hdınsight kümesinde R Server IDE seçenekleri hakkında bilgi edinin
Merhaba Linux kenar düğümüne Hdınsight kümesinin R tabanlı analiz bölgenin giriş hello ' dir. Hdınsight en son sürümlerini sağlamak hello topluluk sürümünü yüklemek için varsayılan bir seçenek [Rstudio'dan Server](https://www.rstudio.com/products/rstudio-server/) hello kenar düğümüne tarayıcı tabanlı bir IDE olarak üzerinde. Bir IDE hello geliştirmeye yönelik olarak Rstudio'dan sunucu kullanımını ve R betiklerinin yürütülmesi hello R konsol kullanmaktan daha önemli ölçüde daha üretken olabilirler. Merhaba küme oluşturma, ancak tooadd istediğiniz durumlarda tooadd Rstudio'dan Server seçerseniz, daha sonra ardından bkz [yükleme R Studio sunucuda Hdınsight kümeleri](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-r-server-install-r-studio). +

Başka bir tam IDE seçeneği Masaüstü IDE tooinstall olduğundan ve bir uzak eşleme azaltın veya Spark işlem bağlamı kullanımı aracılığıyla tooaccess hello kümesi kullanın. Seçenekleriniz Microsoft'un [R araçları Visual Studio için](https://www.visualstudio.com/features/rtvs-vs.aspx) (RTVS) Rstudio'dan ve Walware Eclipse tabanlı [StatET](http://www.walware.de/goto/statet).

Son olarak, yazarak hello R Server hello kenar düğümüne konsolda erişebilmeniz için **R** hello Linux komut isteminde SSH veya PuTY aracılığıyla bağlandıktan sonra. Hello konsol arabirimini kullanırken, bu kullanışlı toorun R betiği geliştirme başka bir pencere için bir metin düzenleyicisi ve kesin ve komut dosyanızı bölümlerini gerektiği gibi hello R konsoluna yapıştırın.

## <a name="learn-about-pricing"></a>Fiyatlandırma hakkında bilgi edinin
Merhaba R Server kümeyle olan bir Hdınsight ile ilişkili ücretleri benzer şekilde toohello ücretleri hello standart Hdınsight kümeleri için yapılandırılmış. Bunlar hello adı, veri ve çekirdek saatlik uplift hello eklenmesi ile kenar düğümler arasında sanal makineleri temel hello hello boyutlandırmasını dayanır. Hdınsight fiyatlandırma ve 30 günlük ücretsiz deneme hello kullanılabilirliği hakkında daha fazla bilgi için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="next-steps"></a>Sonraki adımlar
Aşağıdaki konularda hello nasıl toouse Hdınsight R Server kümeleri, hakkında daha fazla toolearn bakın:

* [Hdınsight'ta R Server kullanmaya başlama](hdinsight-hadoop-r-server-get-started.md)
* [(Küme oluşturma sırasında yüklü değilse) Rstudio'dan sunucu tooHDInsight Ekle](hdinsight-hadoop-r-server-install-r-studio.md)
* [HDInsight üzerinde R Server için işlem bağlamı seçenekleri](hdinsight-hadoop-r-server-compute-contexts.md)
* [HDInsight üzerinde R Server için Azure Depolama seçenekleri](hdinsight-hadoop-r-server-storage.md)
