---
title: aaaWhat veri bilimi sanal makine mi? | Microsoft Belgeleri
description: "Nasıl tooget anahtar analytics senaryoları ile veri bilimi sanal makineleri yapılması başlatıldı."
keywords: "Veri bilimi araçları, veri bilimi sanal makine, veri bilimi, linux veri bilimi için Araçlar"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d4f91270-dbd2-4290-ab2b-b7bfad0b2703
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: 18c7a75208671c663f3b6be6ee8d0bf666772e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-cloud-based-data-science-virtual-machine-for-linux-and-windows"></a>Giriş toohello Linux ve Windows için veri bilimi sanal makine bulut tabanlı
Merhaba veri bilimi sanal makine (DSVM) veri bilimi özellikle yapmak için Microsoft Azure bulut üzerinde özelleştirilmiş bir VM görüntüsü ' dir. Birçok popüler veri bilimi var ve diğer araçları önceden yüklenmiş ve Gelişmiş analiz için akıllı uygulamalar oluşturmaya toojump başlayın önceden yapılandırılmış. Windows Server ve Linux üzerinde kullanılabilir. DSVM'nin Windows sürümünü Server 2016 ve Server 2012'de sunuyoruz. Merhaba DSVM OpenLogic 7.2 CentOS tabanlı Linux dağıtımları ve Ubuntu 16.04 LTS üzerinde Linux sürümü sunuyoruz. 

Bu konu hello veri bilimi VM ile neler yapabileceğiniz açıklanır hello VM kullanmaya yönelik temel senaryolar hello bazıları özetler, hello temel özellikleri hello Windows ve Linux sürümleri kullanılabilir maddeler halinde listelemektedir ve bunları kullanarak tooget nasıl başlatılacağını hakkında yönergeler sağlar.

## <a name="what-can-i-do-with-hello-data-science-virtual-machine"></a>Merhaba veri bilimi sanal makine ile ne yapabilirim?
Merhaba hello veri bilimi sanal makinenin tüm beceri düzeylerini ve rolleri bir uyuşmazlık boş veri bilimi ortamıyla tooprovide veri uzmanları hedefidir. Bu VM, karşılaştırılabilir bir ortamda, kendi alındı, harcadığınız önemli ölçüde zaman kazandırır. Bunun yerine, veri bilimi projenizi hemen bir yeni oluşturulan VM örneğinde başlatın. 

Merhaba veri bilimi VM tasarlanmış ve geniş kullanım senaryoları ile çalışmak için yapılandırılmış. Projenizi gereksinimleriniz değiştikçe yukarı veya aşağı ortamınızı ölçeklendirebilirsiniz. Mümkün toouse, tercih edilen dili tooprogram veri bilimi görevlerdir. Diğer Araçları'nı yüklemek ve hello sistem tam gereksinimlerinize göre özelleştirin.

## <a name="key-scenarios"></a>Anahtar senaryoları
Bu bölümde bazı senaryoları için hangi hello veri bilimi VM dağıtılabilir önerir.

### <a name="preconfigured-analytics-desktop-in-hello-cloud"></a>Analytics Masaüstü hello bulutta yapılandırılmış
Merhaba veri bilimi VM veri bilimi ekipleri yerel masaüstlerine yönetilen bulut masaüstüyle tooreplace görmek için bir taban çizgisi yapılandırmasını sağlar. Bu taban takımda tüm hello veri bilimcileri hangi tooverify denemeler ile tutarlı ayarladıktan ve işbirliği Yükselt sağlar. Merhaba sysadmin yükünü azaltarak ayrıca maliyetleri düşürür ve tooevaluate, yüklemek ve hello muhafaza hello zamanında kaydetme çeşitli yazılım paketleri gelişmiş analizler toodo gerekli.  

### <a name="data-science-training-and-education"></a>Veri bilimi eğitimi
Kurumsal eğitmenler ve veri bilimi sınıfları genellikle öğretmek eğitimcilere bir sanal makine görüntü tooensure kendi Öğrenciler tutarlı bir kurulum olmasını ve hello örnekleri beklendiği iş sağlar. Merhaba veri bilimi VM hello desteği ve uyumsuzluk sorunları kolaylaştırır için tutarlı bir kurulum bir isteğe bağlı ortam oluşturur. Burada bu ortamları toobe gereken durumlarda sık, özellikle kısa eğitim sınıfları için yerleşik, önemli ölçüde yararlanabilir.

### <a name="on-demand-elastic-capacity-for-large-scale-projects"></a>Büyük ölçekli projeleri için isteğe bağlı Esnek Kapasite
Veri bilimi hackathons/competitions veya büyük ölçekli veri modellemesi ve araştırması gerektiren ölçeklendirilmiş kısa süre için genellikle donanım kapasitesi çıkışı. Merhaba veri bilimi VM hello veri bilimi ortamı hızla üzerinde isteğe bağlı çoğaltma, yüksek güçte bilgi işlem kaynakları toobe gerektiren denemeler izin genişletilmiş sunucularda çalıştırmak yardımcı olabilir.

### <a name="short-term-experimentation-and-evaluation"></a>Kısa vadeli deney ve değerlendirme
Merhaba veri bilimi VM kullanılan tooevaluate bulunabilir veya araçları öğrenmek Microsoft R Server, SQL Server gibi Visual Studio Araçları, derin öğrenme Jupyter / ML araç takımları ve yeni araçları, popüler hello en az Kurulum çabayla topluluğu. Merhaba veri bilimi VM hızlı bir şekilde ayarlanabilir beri tanıtımlar çevrimiçi oturumları veya konferans öğreticileri aşağıdaki yönergelerde yürütme yayımlanan denemeler çoğaltma gibi diğer kısa süreli kullanım senaryolarda uygulanabilir.

### <a name="deep-learning"></a>Derin öğrenme
Merhaba veri bilimi VM derin learning algoritmaları GPU (grafik işlem birimleri) tabanlı donanım kullanarak eğitim modeli için kullanılabilir. Azure bulut özellikleri ölçeklendirme VM, DSVM gerek göredir hello bulut üzerinde temel GPU donanım kullanmanıza yardımcı olur. Bir geçirebilirsiniz tooa GPU tabanlı VM büyük modeli eğitimindeki veya yüksek hızlı hesaplamalar tutma sırasında aynı işletim sistemi diski hello.  DSVM Hello Windows Server 2016 sürümünü GPU sürücüleriyle çerçeveler ve hello learning algoritmaları derin GPU sürümü önceden yüklenmiş olarak gelir. Hello Linux üzerinde derin üzerinde GPU öğrenme yalnızca hello üzerinde etkin [veri bilimi sanal makine (Ubuntu) Linux sürümü için](http://aka.ms/dsvm/ubuntu). Tüm hello derin öğrenme çerçeveleri geri dönüş toohello CPU modu; bu durumda olur hello Windows/Ubuntu-2016 sürümünü veri bilimi VM toonon GPU tabanlı Azure sanal makinesi dağıtabilirsiniz. Daha önce Windows Server 2012 için biz yayımlanan bir [derin Araç Seti öğrenme](http://aka.ms/dsvm/deeplearning) ancak artık Windows tabanlı derin öğrenme iş yükleri için Windows Server 2016 kullanmanızı öneririz. Merhaba DSVM Hello CentOS tabanlı Linux sürümü CPU hello Araçlar (CNTK, Tensorflow, MXNet) öğrenme derin bazıları oluşturur ama hello GPU sürücüleri ve çerçeveleri ile önceden yüklenmiş gelmez yalnızca hello içerir. 

## <a name="whats-included-in-hello-data-science-vm"></a>Merhaba veri bilimi VM neler dahildir?
Merhaba veri bilimi sanal makine, birçok popüler veri bilimi ve zaten yüklenmiş ve yapılandırılmış araçları öğrenme derin vardır. Ayrıca, çeşitli Azure verileri ve çözümlemeler ürünleri ile kolay toowork olun araçlar içerir. Keşfetmek ve büyük ölçekli veri hello Microsoft R Server veya SQL Server 2016 kullanarak kümeleri Tahmine dayalı modelleri oluşturun. Bir ana bilgisayar diğer Araçları'nın hello açık kaynak topluluktan ve Microsoft: de dahil, aynı zamanda örnek kod ve dizüstü bilgisayarlar. Merhaba aşağıdaki tabloda maddeler halinde listelemektedir ve hello ana bileşenler hello Windows ve Linux sürümleri hello veri bilimi sanal makine dahil karşılaştırır.


| **Aracı**                                                           | **Windows sürümü** | **Linux sürümü** |
| :------------------------------------------------------------------ |:-------------------:|:------------------:|
| [Microsoft R açık](https://mran.microsoft.com/open/) önceden yüklenmiş popüler paketleriyle   |E                      | E             |
| [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/) içeren Geliştirici sürümü <br />  &nbsp;&nbsp;&nbsp;&nbsp;* [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started) paralel ve dağıtılmış yüksek performanslı R framework<br />  &nbsp;&nbsp;&nbsp;&nbsp;* [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) -Microsoft'tan yeni durumu resim ML algoritmaları <br />  &nbsp;&nbsp;&nbsp;&nbsp;* [R Operationalization](https://msdn.microsoft.com/microsoft-r/operationalize/about)                                            |E                      | E <br/> (MicrosoftML henüz kullanılabilir değil)|
| [Microsoft Office](https://products.office.com/en-us/business/office-365-proplus-business-software) paylaşılan etkinleştirme - Excel, Word ve PowerPoint profesyonel artı   |E                      |N              |
| [Anaconda Python](https://www.continuum.io/) 2.7, önceden yüklenmiş popüler paketleriyle 3.5    |E                      |E              |
| [JuliaPro](https://juliacomputing.com/products/juliapro.html) önceden yüklenmiş Jale dil için popüler paketleriyle                         |E                      |E              |
| İlişkisel Veritabanları                                                            | [SQL Server 2016 SP1](https://www.microsoft.com/sql-server/sql-server-2016) <br/> Geliştirici sürümü| [PostgreSQL](https://www.postgresql.org/) |
| Veritabanı Araçları                                                       | * SQL Server Management Studio <br/>* SQL Server Integration Services<br/>* [BCP, sqlcmd](https://docs.microsoft.com/sql/tools/command-prompt-utility-reference-database-engine)<br /> * ODBC/JDBC sürücüleri| * [SQuirreL SQL](http://squirrel-sql.sourceforge.net/) (sorgulama. aracı), <br /> * bcp, sqlcmd <br /> * ODBC/JDBC sürücüleri|
| SQL Server R hizmetleriyle ölçeklenebilir veritabanı analizi | E     |N              |
| **[Jupyter not defteri sunucu](http://jupyter.org/) aşağıdaki çekirdekleri ile**                                  | E     | E |
|     &nbsp;&nbsp;&nbsp;&nbsp;* R | E | E |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Python 2.7 & 3.5 | E | E |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Jale | E | E |
|     &nbsp;&nbsp;&nbsp;&nbsp;* PySpark | N | E |
|     &nbsp;&nbsp;&nbsp;&nbsp;* [Sparkmagic](https://github.com/jupyter-incubator/sparkmagic) | N | Y (yalnızca Ubuntu) |
|     &nbsp;&nbsp;&nbsp;&nbsp;* SparkR     | N | E |
| JupyterHub (çok kullanıcılı not defterlerini sunucusu)| N | E |
| **Geliştirme araçları, IDE ve Kod Düzenleyicisi**| | |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Visual Studio 2017 (Community Edition)](https://www.visualstudio.com/community/) > Git eklentisi, Azure Hdınsight (Hadoop), Data Lake, SQL Server veri araçları ile [Node.js](https://github.com/Microsoft/nodejstools), [Python](http://aka.ms/ptvs), ve [R Visual Studio (RTVS) için araçları](http://microsoft.github.io/RTVS-docs/) | E | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Visual Studio Code](https://code.visualstudio.com/) | E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Rstudio'dan Masaüstü](https://www.rstudio.com/products/rstudio/#Desktop) | E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Rstudio'dan sunucu](https://www.rstudio.com/products/rstudio/#Server) | N | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [PyCharm](https://www.jetbrains.com/pycharm/) | N | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Atom](https://atom.io/) | N | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Juno (Jale IDE)](http://junolab.org/)| E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* VIM ve Emacs | E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* Git ve Gitbash'i | E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* OpenJDK | E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* .net framework | E | N |
| Desktop'a | E | N |
| SDK'ları tooaccess Azure ve Cortana Intelligence Suite Hizmetleri | E | E |
| **Veri taşıma ve Yönetim Araçları** | | |
| &nbsp;&nbsp;&nbsp;&nbsp;* Azure Storage Gezgini | E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Azure CLI](https://docs.microsoft.com/cli/azure/overview) | E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* Azure Powershell | E | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Azcopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy) | E | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Adlcopy (Azure Data Lake Store)](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob) | E | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [DocDB veri geçiş aracı](https://docs.microsoft.com/azure/documentdb/documentdb-import-data) | E | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Microsoft Veri Yönetimi ağ geçidi](https://msdn.microsoft.com/library/dn879362.aspx) : OnPrem ve bulut arasında veri taşıma | E | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* UNIX/Linux komut satırı yardımcı programları | E | E |
| [Apache ayrıntıya](http://drill.apache.org) veri keşfi için | E | E |
| **Machine Learning araçları** |||
| &nbsp;&nbsp;&nbsp;&nbsp;* İle tümleştirme [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) (R, Python) | E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Xgboost](https://github.com/dmlc/xgboost) | E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit) | E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Weka](http://www.cs.waikato.ac.nz/ml/weka/) | E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Çıngırağı](http://rattle.togaware.com/) | E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [LightGBM](https://github.com/Microsoft/LightGBM) | N | Y (yalnızca Ubuntu) |
| &nbsp;&nbsp;&nbsp;&nbsp;* [H2O](https://www.h2o.ai/h2o/) | N | Y (yalnızca Ubuntu) |
| **GPU tabanlı derin öğrenme araçları** |Windows Server 2016 sürümü  |Ubuntu sürüm |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Microsoft Bilişsel Araç Seti (CNTK)](http://cntk.ai) | E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Tensorflow](https://www.tensorflow.org/) | E | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [MXNet](http://mxnet.io/) | E | E|
| &nbsp;&nbsp;&nbsp;&nbsp;* [Caffe & Caffe2](https://github.com/caffe2/caffe2) | N | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Torch](http://torch.ch/) | N | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Theano](https://github.com/Theano/Theano) | N | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Keras](https://keras.io/)| N | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [NVIDIA basamak](https://github.com/NVIDIA/DIGITS) | N | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* [CUDA, CUDNN, NVIDIA sürücüsü](https://developer.nvidia.com/cuda-toolkit) | E | E |
| **Büyük veri Platformu (yalnızca Devtest)**|||
| &nbsp;&nbsp;&nbsp;&nbsp;* Yerel [Spark](http://spark.apache.org/) tek başına | N | E |
| &nbsp;&nbsp;&nbsp;&nbsp;* Yerel [Hadoop](http://hadoop.apache.org/) (HDFS, YARN) | N | E |



## <a name="how-tooget-started-with-hello-windows-data-science-vm"></a>Tooget hello Windows veri bilimi VM ile çalışmaya nasıl
* İstenen hello Windows DSVM edition örneği giderek oluşturun
  * [Windows Server 2016 DSVM dayalı](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-ads.windows-data-science-vm)
  
  or 
  * [Windows Server 2012 DSVM dayalı](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) 
* Merhaba tıklatın **BT almak artık** düğmesi.
* Oturum açma toohello VM hello VM oluştururken belirttiğiniz hello kimlik bilgilerini kullanarak Uzak Masaüstü.
* toodiscover ve başlatma hello Araçlar kullanılabilir'hello **Başlat** menüsü.

## <a name="get-started-with-hello-linux-data-science-vm"></a>Merhaba Linux veri bilimi VM ile çalışmaya başlama
* İstenen hello örneğini oluşturmak çok gezinme tarafından Linux DSVM edition
  * [Ubuntu DSVM dayalı](http://aka.ms/dsvm/ubuntu)

  or

  * [OpenLogic CentOS DSVM dayalı](http://aka.ms/dsvm/centos)

  
* Merhaba tıklatın **Şimdi Al** düğmesi.
* Oturum açma toohello VM Putty veya SSH komutu gibi bir SSH istemcisi, hello kimlik bilgilerini kullanarak hello VM oluştururken belirttiğiniz.
* Merhaba Kabuk isteminde dsvm daha fazla bilgi girin.
* İçin grafik bir masaüstü, istemci platformunuza hello X2Go istemci indirme [burada](http://wiki.x2go.org/doku.php/doc:installation:x2goclient) ve hello Linux veri bilimi VM belgedeki hello yönergeleri izleyerek [sağlama hello Linux veri bilimi sanal makine](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).

## <a name="next-steps"></a>Sonraki adımlar
### <a name="for-hello-windows-data-science-vm"></a>Merhaba Windows veri bilimi VM
* Nasıl toorun belirli hello Windows sürümünde kullanılabilir araçları ile ilgili daha fazla bilgi için bkz: [sağlama hello Microsoft Veri bilimi sanal makine](machine-learning-data-science-provision-vm.md) ve
* Tooperform hello Windows VM üzerinde veri bilimi projeniz için gereken çeşitli görevleri nasıl görürüm hakkında daha fazla bilgi için [hello veri bilimi sanal makine üzerinde yapabilir on nokta](machine-learning-data-science-vm-do-ten-things.md).

### <a name="for-hello-linux-data-science-vm"></a>Merhaba Linux veri bilimi VM
* Nasıl toorun belirli hello Linux sürümünde kullanılabilir araçları ile ilgili daha fazla bilgi için bkz: [sağlama hello Linux veri bilimi sanal makine](machine-learning-data-science-linux-dsvm-intro.md).
* Gösteren tooperform birçok ortak veri bilimi hello Linux VM ile nasıl görevler için bkz [hello Linux veri bilimi sanal makine üzerinde veri bilimi](machine-learning-data-science-linux-dsvm-walkthrough.md).

