---
title: "aaaProvision hello veri bilimi sanal makine için Linux'ta (Ubuntu) Azure | Microsoft Docs"
description: "Yapılandırma, bir veri bilimi sanal makine için Linux (Ubuntu) üzerinde Azure toodo analiz oluşturmak ve makine."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3bab0ab9-3ea5-41a6-a62a-8c44fdbae43b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 037c126c0a35d8065fc89c591089df73d2b91425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-data-science-virtual-machine-for-linux-ubuntu"></a>Linux (Ubuntu) Hello veri bilimi sanal makine sağlama
Merhaba Linux için veri bilimi sanal makine olduğundan Ubuntu tabanlı Azure üzerinde derin öğrenme ile kolay tooget kolaylaştırır sanal makine görüntüsü başlatıldı. Derin öğrenme araçlar şunlardır:

  * [Caffe](http://caffe.berkeleyvision.org/): hızı, expressivity ve modülerlik için yerleşik bir derin öğrenme çerçevesi
  * [Caffe2](https://github.com/caffe2/caffe2): Caffe platformlar arası sürümü
  * [Hesaplama ağ Araç Seti (CNTK)](https://github.com/Microsoft/CNTK): Microsoft Research yazılım araç Seti'nin öğrenme derin
  * [H2O](https://www.h2o.ai/): bir açık kaynak büyük veri platformu ve grafik kullanıcı arabirimi
  * [Keras](https://keras.io/): Python Theano ve TensorFlow için üst düzey sinir ağı API
  * [MXNet](http://mxnet.io/): birçok dil bağlamalarla esnek ve verimli derin learning kitaplığı
  * [NVIDIA basamak](https://developer.nvidia.com/digits): ortak derin öğrenimi görevlerini basitleştirir grafik bir sistem
  * [TensorFlow](https://www.tensorflow.org/): Google makine zekasından için bir açık kaynak kitaplığı
  * [Theano](http://deeplearning.net/software/theano/): tanımlama, en iyi duruma getirme ve çok boyutlu diziler içeren matematiksel ifadeler verimli bir şekilde değerlendirmek için bir Python kitaplığı
  * [Torch](http://torch.ch/): machine learning algoritmaları için Uluslararası Destek bilimsel hesaplama çerçevesiyle
  * CUDA, cuDNN ve hello NVIDIA sürücüsü
  * Birçok örnek Jupyter Not Defterleri

Merhaba CPU üzerinde de çalışır ancak tüm kitaplıkları hello GPU, sürümleridir.

Merhaba veri bilimi sanal makine için Linux da dahil olmak üzere veri bilimi ve geliştirme etkinlikler için popüler araçları içerir:

* Microsoft R açıkken Microsoft R Server Geliştirici sürümü
* Popüler veri analiz kitaplıkları anaconda Python dağıtımı (sürüm 2.7 ve 3.5) dahil olmak üzere
* JuliaPro - Jale dili popüler bilimsel ve veri analizi kitaplıkları ile seçkin dağıtılması
* Tek başına Spark örneğinde ve tek düğümlü Hadoop (HDFS, Yarn)
* JupyterHub - R, Python, PySpark, Jale tekrar destekleyen çok kullanıcılı bir Jupyter not defteri sunucusu
* Azure Depolama Gezgini
* Azure komut satırı Azure kaynaklarını yönetmek için arabirimi (CLI)
* Machine learning araçları
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): çevrimiçi, karma, allreduce, düşürülmesi, learning2search, etkin, gibi teknikler destekleme sistem öğrenme hızlı bir makine ve etkileşimli öğrenme
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): hızlı ve doğru boosted ağaç uygulama sağlayan bir aracı
  * [Rattle](http://rattle.togaware.com/): ile veri analizi ve makine öğrenimi R kolay hale getirir grafik tabanlı bir aracı
  * [LightGBM](https://github.com/Microsoft/LightGBM): framework artırmanın hızlı, dağıtılmış, yüksek performanslı bir gradyan
* Azure SDK Java, Python, node.js, Ruby, PHP
* Azure Machine Learning ve diğer Azure hizmetleriyle R ve Python için kitaplıkları kullanma
* Geliştirme araçları ve Düzenleyicileri (Rstudio'dan, PyCharm, Intellij, Emacs, VIM)


Veri Bilimi bulunurken bir dizi görev yineleme içerir:

1. Bulma, yükleme ve verilerin önceden işlenmesi
2. Derleme ve modelleri test etme
3. Merhaba modelleri akıllı uygulamalarında tüketimi için dağıtma

Veri bilimcilerine çeşitli araçlar toocomplete bu görevleri kullanın. Oldukça uzun süren toofind hello uygun sürümlerini hello yazılım olabilir ve daha sonra toodownload, derleme ve bu sürümleri yükleyin.

Merhaba Linux için veri bilimi sanal makine bu yük önemli ölçüde kolaylaştırabilir. Toojump başlangıç kullanma analizi projenizi. R, Python, SQL, Java ve C++ dahil olmak üzere çeşitli dillerde görevlerde toowork sağlar. Hello Azure SDK'sını hello VM dahil toobuild verir hello Microsoft bulut platformu için çeşitli hizmetlere Linux'ta kullanarak uygulamalarınızı. Ayrıca, aynı zamanda önceden yüklenmiş Ruby, Perl, PHP ve node.js gibi erişim tooother diller sahip.

Bu veri bilimi VM görüntüsü için yazılım harcamanız yok. Merhaba, sağlama hello sanal makine boyutuna göre uygunluk yalnızca hello Azure donanım kullanım ücretleri ödersiniz. Ücretler hello üzerinde bulunabilir hello hakkında daha ayrıntılı bilgi işlem [VM listeleme hello Azure Marketi sayfasında](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm/).

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Merhaba veri bilimi sanal makine diğer sürümleri
A [CentOS](machine-learning-data-science-linux-dsvm-intro.md) görüntü kullanılabilir Ayrıca, birçok hello aynı Ubuntu görüntü hello gibi araçları. A [Windows](machine-learning-data-science-provision-vm.md) görüntü kullanılabilir de.

## <a name="prerequisites"></a>Ön koşullar
Linux için bir veri bilimi sanal makine oluşturmadan önce bir Azure aboneliğinizin olması gerekir. tooobtain biri bkz [alma Azure ücretsiz deneme sürümü](https://azure.microsoft.com/free/).

## <a name="create-your-data-science-virtual-machine-for-linux"></a>Linux için veri bilimi sanal makine oluşturma
Merhaba adımları toocreate hello Linux için veri bilimi sanal makine örneği aşağıda verilmiştir:

1. Toohello sanal makine üzerinde hello listeleme gidin [Azure portal](https://portal.azure.com/#create/microsoft-ads.linux-data-science-vm-ubuntulinuxdsvmubuntu).
2. Tıklatın **oluşturma** (Merhaba altındaki) hello Sihirbazı yukarı toobring.![ yapılandırma verileri-Bilim-vm](./media/machine-learning-data-science-dsvm-ubuntu-intro/configure-data-science-virtual-machine.png)
3. Aşağıdaki bölümlerde hello toocreate hello Microsoft Veri bilimi sanal makine hello girişleri (sağ şekil önceki hello hello üzerinde numaralandırılan) hello Sihirbazı'nda hello adımların her biri için kullanılan sağlar. Merhaba gerekli girişleri tooconfigure her bu adımları şunlardır:
   
   a. **Temel kavramları**:
   
   * **Ad**: oluşturduğunuz veri bilimi sunucunuzun adını yazın.
   * **Kullanıcı adı**: ilk hesap oturum açma kimliği.
   * **Parola**: ilk hesap parolası (kullanabilirsiniz SSH ortak anahtarı parola yerine).
   * **Abonelik**: birden fazla aboneliğiniz varsa, select hello biri üzerinde hangi hello makine oluşturulur ve fatura toobe. Bu abonelik için kaynak oluşturma ayrıcalıkları olmalıdır.
   * **Kaynak grubu**: yeni bir tane oluşturun veya varolan bir grubu kullanın.
   * **Konum**: en uygun seçim hello veri merkezi. Genellikle, verilerinizden en iyi olduğundan, veya en yakın tooyour fiziksel konumu en hızlı ağ erişimi için hello veri merkezi olur.
   
   b. **Boyutu**:
   
   * İşlev gereksinimi ve maliyet kısıtlamaları karşılayan hello sunucusu türlerinden birini seçin. Seçin **tümünü görüntüle** toosee daha fazla seçenek VM boyutları. GPU eğitim NC sınıfı VM'yi seçin.
   
   c. **Ayarları**:
   
   * **Disk türü**: seçin **Premium** katı hal sürücüsü (SSD) tercih ederseniz. Aksi takdirde seçin **standart**. GPU VM'ler standart bir disk gerektirir.
   * **Depolama hesabı**: aboneliğinizde yeni bir Azure depolama hesabı oluşturma veya mevcut bir hello kullanma üzerinde hello seçildi aynı konuma **Temelleri** hello Sihirbazı.
   * **Diğer parametreler**: Çoğu durumda, yalnızca hello varsayılan değerleri kullanırsınız. tooconsider varsayılan olmayan değerleri, hello bilgilendirme bağlantısını üzerine getirin hello belirli alanları yardımcı olur.
   
   d. **Özet**:
   
   * Girdiğiniz tüm bilgilerin doğru olduğunu doğrulayın.
   
   e. **Satın**:
   
   * toostart sağlama Merhaba, tıklatın **satın**. Bir bağlantı hello işlem toohello koşullarını sağlanır. Merhaba VM hello Seçtiğiniz hello sunucu boyutu hello işlem ötesinde herhangi bir ek ücret yok **boyutu** adım.

Merhaba sağlama yaklaşık 5-10 dakika sürer. Merhaba sağlama hello durumu hello Azure portalı üzerinde görüntülenir.

## <a name="how-tooaccess-hello-data-science-virtual-machine-for-linux"></a>Tooaccess veri bilimi sanal makine için Linux nasıl hello
Hello VM oluşturulduktan sonra SSH kullanarak tooit kaydolabilirsiniz. Hello oluşturulan hello hesap kimlik bilgilerini kullanan **Temelleri** bölüm hello metin kabuk arabirimi için adım 3. Windows, bir SSH istemcisi aracı gibi indirebilirsiniz [Putty](http://www.putty.org). Grafik Masaüstü (X Windows sistemi) tercih ederseniz, Putty iletme X11 kullanın veya hello X2Go istemcisi yükleyin.

> [!NOTE]
> Merhaba X2Go istemci gerçekleştirilen önemli ölçüde testinde iletme X11 daha iyi. Merhaba X2Go istemci için bir grafik Masaüstü arabirimi kullanmanızı öneririz.
> 
> 

## <a name="installing-and-configuring-x2go-client"></a>Yükleme ve X2Go istemci yapılandırma
Merhaba Linux VM zaten X2Go sunucu ve hazır tooaccept istemci bağlantıları ile sağlanır. tooconnect toohello Linux VM grafik Masaüstü Merhaba, istemcide aşağıdaki:

1. İstemci platformunuza hello X2Go istemci yükleyip [X2Go](http://wiki.x2go.org/doku.php/doc:installation:x2goclient).    
2. Merhaba X2Go istemci çalıştırmak ve seçmek **yeni oturum**. İle birden çok sekme yapılandırma penceresi açar. Yapılandırma parametreleri aşağıdaki hello girin:
   * **Oturum sekmesini**:
     * **Ana bilgisayar**: hello ana bilgisayar adı veya IP adresini, Linux veri bilimi VM.
     * **Oturum açma**: hello Linux VM kullanıcı adı.
     * **SSH bağlantı noktası**: 22 hello varsayılan değerinde bırakın.
     * **Oturum türü**: değişiklik hello değeri tooXFCE. Şu anda hello Linux VM yalnızca XFCE Masaüstü destekler.
   * **Ortam sekmesini**: ses desteği ve toouse gerekmiyorsa, Yazdırma İstemcisi devre dışı bırakma bunları.
   * **Paylaşılan Klasörler**: hello Linux VM üzerinde bağlı istemci makinelerden dizinleri istiyorsanız bu sekmedeki hello VM ile tooshare istediğiniz hello istemci makine dizinleri ekleyin.

Merhaba SSH istemcisi veya XFCE grafik Masaüstü hello X2Go istemcisi aracılığıyla kullanarak toohello VM oturum sonra yüklü olan ve hello VM üzerinde yapılandırılmış hello araçlarını kullanarak hazır toostart demektir. XFCE üzerinde uygulamaları menüsü kısayolları ve masaüstü simgelerini hello araçları çoğunu görebilirsiniz.

## <a name="tools-installed-on-hello-data-science-virtual-machine-for-linux"></a>Linux için Hello veri bilimi sanal makine üzerinde yüklü araçları
### <a name="deep-learning-libraries"></a>Derin öğrenme kitaplıkları

#### <a name="cntk"></a>CNTK
Hello Microsoft Bilişsel Toolki - olarak da bilinen CNTK - bir açık, araç seti öğrenme derin bir kaynaktır. Python bağlamaları hello kök ve py35 Conda ortamlarında kullanılabilir. Ayrıca, hello yolu zaten bir komut satırı aracı (cntk) sahiptir.

Örnek Python not defterlerini JupyterHub içinde kullanılabilir. toorun hello komut satırında, temel bir örnek hello Kabuk komutları aşağıdaki hello yürütün:

    cd /home/[USERNAME]/notebooks/CNTK/HelloWorld-LogisticRegression
    cntk configFile=lr_bs.cntk makeMode=false command=Train

Daha fazla bilgi için bkz: Merhaba CNTK bölümünü [GitHub](https://github.com/Microsoft/CNTK)ve hello [CNTK wiki](https://github.com/Microsoft/CNTK/wiki).

#### <a name="caffe"></a>Caffe
Caffe hello Berkeley görme çerçevesinden ve eğitim merkezi öğrenme derin ' dir. /Opt/caffe içinde kullanılabilir. Örnekler /opt/caffe/examples içinde bulunabilir.

#### <a name="caffe2"></a>Caffe2
Caffe2 Caffe üzerinde oluşturulmuş facebook'taki derin öğrenme çerçevedir. Merhaba Conda kök ortamında Python 2.7 içinde kullanılabilir. tooactivate, hello Kabuğu'ndan hello aşağıdaki komutu çalıştırın:

    source /anaconda/bin/activate root

Bazı örnek not defterlerini JupyterHub içinde kullanılabilir.

#### <a name="h2o"></a>H2O
H2O hızlı, bellek içi, dağıtılmış machine learning ve Tahmine dayalı analiz platformu ' dir. Python paket hem Merhaba, kök ve py35 Anaconda ortamlarında yüklenir. R paketi de yüklenir. Merhaba komut satırı Çalıştır gelen toostart H2O `java -jar /dsvm/tools/h2o/current/h2o.jar`; vardır çeşitli [komut satırı seçenekleri](http://docs.h2o.ai/h2o/latest-stable/h2o-docs/starting-h2o.html#from-the-command-line) tooconfigure ister. Merhaba Akış Web kullanıcı Arabirimi başlangıç toohttp://localhost:54321 tooget göz atarak erişilebilir. Örnek not defterlerini de JupyterHub içinde kullanılabilir.

#### <a name="keras"></a>Keras
Keras Tensorflow veya Theano üstte çalıştırabilen Python içinde üst düzey sinir ağı API ' dir. Merhaba kök ve py35 Python ortamlarında kullanılabilir. 

#### <a name="mxnet"></a>MXNet
MXNet verimliliği ve esneklik için tasarlanmış bir derin öğrenme çerçevedir. Merhaba DSVM üzerinde dahil R ve Python bağlamaları vardır. Örnek not defterlerini JupyterHub içinde bulunur ve örnek kod /dsvm/samples/mxnet içinde kullanılabilir.

#### <a name="nvidia-digits"></a>NVIDIA BASAMAK
BASAMAKLI olarak bilinen hello NVIDIA derin öğrenme GPU eğitim sistem, verileri, tasarlama ve eğitim sinir ağları GPU sistemlerde yönetme ve Gelişmiş görselleştirme ile gerçek zamanlı performans izleme gibi bir sistem toosimplify ortak derin öğrenme Görevler ' dir. 

BASAMAK basamak adlı bir hizmet olarak mevcut değil. Merhaba hizmetini başlatın ve başlatılan toohttp://localhost:5000 tooget göz atın.

BASAMAK da yüklü bir Python modülü hello Conda kök ortamında olarak.

#### <a name="tensorflow"></a>TensorFlow
TensorFlow Google derin öğrenme kitaplığıdır. Veri akışı grafikleri kullanma sayısal hesaplama için bir açık kaynak yazılım kitaplığı değil. TensorFlow hello py35 Python ortamında kullanılabilir ve bazı örnek not defterlerini JupyterHub dahil edilir.

#### <a name="theano"></a>Theano
Theano verimli sayısal hesaplama için Python kitaplığıdır. Merhaba kök ve py35 Python ortamlarında kullanılabilir. 

#### <a name="torch"></a>Torch
Torch bir geniş machine learning algoritmaları desteğiyle bilimsel hesaplama çerçevedir. /Dsvm/tools/torch içinde kullanılabilir ve hello th etkileşimli oturum ve luarocks Paket Yöneticisi hello komut satırında kullanılabilir. Örnekler /dsvm/samples/torch içinde kullanılabilir.

PyTorch de hello kök Anaconda ortamında kullanılabilir. İçinde /dsvm/samples/pytorch örnektir.

### <a name="microsoft-r-server"></a>Microsoft R Server
R veri analizi ve makine öğrenme en popüler diller hello biridir. Analizi için toouse R istiyorsanız hello VM hello Microsoft R Aç (MRO) ile Microsoft R Server (MRS) ve matematik çekirdek kitaplığı (MKL) sahiptir. Merhaba MKL matematik işlemleri analitik algoritmaları ortak en iyi duruma getirir. MRO yüzde 100 CRAN R ile uyumlu olan ve içinde CRAN yayımlanan hello R kitaplıkları hiçbirini MRO hello üzerinde yüklenebilir. MRS ölçekleme ve web hizmetlerine R modellerin operationalization sağlar. R programlarınızı Rstudio'dan, VI veya Emacs gibi hello varsayılan düzenleyicileri birinde düzenleyebilirsiniz. Merhaba Emacs Düzenleyicisi'ni kullanıyorsanız, bu hello Emacs paket hello Emacs Düzenleyicisi içinde R dosyalarıyla çalışma basitleştirir, önceden yüklenmiş v (Emacs konuşur istatistiklerini) unutmayın.

toolaunch R konsolu, yalnızca yazdığınız **R** hello Kabuğu'nda. Bu tooan etkileşimli ortamını alır. toodevelop R programınızı genellikle Emacs veya VI gibi bir düzenleyici kullanın ve ardından R'ye içinde hello komut dosyalarını çalıştır Rstudio'dan ile bir tam grafik IDE ortam toodevelop R programınızı sahip.

Ayrıca, tooinstall hello için bir R betiği olan [üst 20 R paketleri](http://www.kdnuggets.com/2015/06/top-20-r-packages.html) istiyorsanız. (Belirtildiği gibi) yazarak girilebilir hello R etkileşimli arabiriminde olduktan sonra bu komut dosyasının çalıştırılması **R** hello Kabuğu'nda.  

### <a name="python"></a>Python
Python kullanarak geliştirme için Anaconda Python 2.7 ve 3.5 dağıtım yüklendi. Bu dağıtım hello içeren Python yaklaşık 300 hello en popüler matematik, mühendislik ve veri analizi paketlerinin yanı sıra temel. Merhaba varsayılan metin düzenleyicisi kullanabilirsiniz. Ayrıca, Spyder, Anaconda Python dağıtımları ile birlikte bir Python IDE kullanabilirsiniz. Spyder gereken bir grafik Masaüstü veya X11 iletme. Kısayol tooSpyder hello grafik Desktop'ta sağlanır.

Biz, Python 2.7 ve 3.5 sahip olduğundan, toospecifically gereken istediğiniz üzerinde toowork hello içinde geçerli oturumu istenen hello Python sürümü (conda ortamı) etkinleştirin. Merhaba etkinleştirme işlemini hello yolu değişken toohello Python'un istenen sürümüyle ayarlar.

Merhaba aşağıdaki hello Kabuğu'ndan tooactivate hello Python 2.7 conda ortamı:

    source /anaconda/bin/activate root

Python 2.7 adresindeki yüklü */anaconda/bin*.

Merhaba aşağıdaki hello Kabuğu'ndan tooactivate hello Python 3.5 conda ortamı:

    source /anaconda/bin/activate py35


Python 3.5 yüklü adresindeki */anaconda/envs/py35/bin*.

Python etkileşimli oturumu tooinvoke yalnızca yazın **python** hello Kabuğu'nda. Bir grafik arabiriminde olan veya yedekleme kümesi iletme X11 varsa, yazabilirsiniz **pycharm** toolaunch hello PyCharm Python IDE.

tooinstall ek Python kitaplıklar, gereksinim duyduğunuz toorun ```conda``` veya ````pip```` komut altında sudo ve (conda veya PIP) tooinstall toohello doğru Python ortamı hello Python Paket Yöneticisi'nin tam yolunu girin. Örneğin:

    sudo /anaconda/bin/pip install <package> #for Python 2.7 environment
    sudo /anaconda/envs/py35/bin/pip install <package> # for Python 3.5 environment


### <a name="jupyter-notebook"></a>Jupyter not defteri
Merhaba Anaconda dağıtım Ayrıca, bir ortam tooshare kodu ve analiz Jupyter not defteri ile birlikte gelir. Merhaba Jupyter not defteri JupyterHub erişilir. Yerel Linux kullanıcı adı ve parola kullanarak oturum açın.

Merhaba Jupyter not defteri sunucu Python 2, Python 3 ve R tekrar önceden yapılandırıldı. "Jupyter Not Defteri" toolaunch hello tarayıcı tooaccess hello not defteri sunucu adlı bir masaüstü simgesi yoktur. Merhaba VM SSH veya X2Go istemcisi kullanıyorsanız, de ziyaret edebilirsiniz [https://localhost:8000 /](https://localhost:8000/) tooaccess hello Jupyter not defteri sunucu.

> [!NOTE]
> Hiçbir sertifika uyarısı alırsanız devam edin.
> 
> 

Herhangi bir ana bilgisayardan hello Jupyter not defteri sunucusuna erişebilir. Yalnızca yazın *https://\<VM DNS adı veya IP adresi\>: 8000 /*

> [!NOTE]
> Merhaba VM sağlandığında bağlantı noktası 8000 hello Güvenlik Duvarı'nda varsayılan olarak açılır.
> 
> 

Biz örnek not defterlerini--bir söz Python ve r birinde paketlenmiş Yerel Linux kullanıcı adı ve parola kullanarak toohello Jupyter not defteri kimlik doğrulaması sonra hello not defteri giriş sayfasında hello bağlantı toohello örneklerini görebilirsiniz. Seçerek yeni bir not defteri oluşturabilirsiniz **yeni**ve ardından hello uygun dil çekirdek. Merhaba görmüyorsanız, **yeni** düğmesini hello tıklatın, **Jupyter** hello üst sol toogo toohello giriş sayfasında hello not defteri sunucusunun simgesi.

### <a name="apache-spark-standalone"></a>Tek başına Apache Spark 
Apache Spark tek başına örneğini hello Spark uygulamalarında yerel olarak ilk önce test ve büyük kümelerinde dağıtma geliştirme Linux DSVM toohelp önceden yüklenir. Merhaba Jupyter çekirdek PySpark programları çalıştırabilir. Jupyter açın ve hello "Yeni" düğmesini tıklatın, kullanılabilir tekrar listesini görürsünüz. "Spark – Python" Hello, Spark Python dilini kullanarak uygulamalar oluşturmanıza olanak tanır hello PySpark Çekirdeği ' dir. Ayrıca, Spark PyCharm veya Spyder toobuild gibi bir Python IDE kullanabilirsiniz program. Bu yana, bu tek başına bir örneğini, hello Spark yığını istemci programı çağırma hello içinde çalışır. Bu daha hızlı hale getirir ve daha kolay tootroubleshoot sorunları toodeveloping bir Spark kümesinde karşılaştırılır. 

Bir örnek PySpark not defteri hello "SparkML" dizini Jupyter ($ giriş/not defterlerini/SparkML/pySpark) hello giriş dizininin altında bulabilirsiniz Jupyter üzerinde sağlanır. 

R için Spark programlama yapıyorsanız Microsoft R Server, SparkR veya sparklyr kullanabilirsiniz. 

Microsoft R Server Spark bağlamda çalıştırmadan önce toodo bir saat Kurulum adım tooenable yerel tek bir düğüm Hadoop HDFS ve Yarn örneği gerekir. Varsayılan olarak, Hadoop Hizmetleri yüklü ancak DSVM hello üzerinde devre dışı. Sipariş tooenable, komutları kök hello ilk kez aşağıdaki toorun hello gerekenler:

    echo -e 'y\n' | ssh-keygen -t rsa -P '' -f ~hadoop/.ssh/id_rsa
    cat ~hadoop/.ssh/id_rsa.pub >> ~hadoop/.ssh/authorized_keys
    chmod 0600 ~hadoop/.ssh/authorized_keys
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa.pub
    chown hadoop:hadoop ~hadoop/.ssh/authorized_keys
    systemctl start hadoop-namenode hadoop-datanode hadoop-yarn

Durdurabilirsiniz hello Hadoop ilgili hizmetleri, bunları çalıştırarak gerekmediğinde ````systemctl stop hadoop-namenode hadoop-datanode hadoop-yarn```` nasıl toodevelop ve test MRS (Merhaba DSVM hello tek başına Spark örneğinde olan) uzaktan Spark bağlamında sağlanan ve hello kullanılabilirolduğunugösterenbirörnek`/dsvm/samples/MRS` dizini. 

### <a name="ides-and-editors"></a>IDE ve düzenleyiciler
Birkaç kod Düzenleyicileri'nin seçeneğiniz vardır. Bu, VI/VIM, Emacs, PyCharm, Rstudio'dan ve Intellij içerir. Intellij, Rstudio'dan ve PyCharm grafik düzenleyicilerden olup ihtiyacınız toobe imzalı tooa grafik Masaüstü toouse bunları. Masaüstü ve uygulama bu düzenleyicilerin sahip menü kısayolları toolaunch bunları.

**VIM** ve **Emacs** metin tabanlı düzenleyiciler şunlardır. Emacs üzerinde biz Emacs konuşur istatistikleri (Merhaba Emacs Düzenleyicisi içinde R ile çalışmayı kolaylaştırır, v) adlı bir eklenti paketi yüklediniz. Daha fazla bilgi bulunabilir [v](http://ess.r-project.org/).

**LaTex** hello texlive paket Emacs eklenti birlikte aracılığıyla yüklenen [auctex](https://www.gnu.org/software/auctex/manual/auctex/auctex.html) LaTex belgelerinizi Emacs içinde yazma basitleştirir paket.  

### <a name="databases"></a>Veritabanları

#### <a name="graphical-sql-client"></a>Grafik SQL istemcisi
**SQuirrel SQL**, tooconnect toodifferent veritabanları (örneğin, Microsoft SQL Server ve MySQL) ve toorun SQL sorguları grafik SQL istemci'nin sağlamış. Bu (Merhaba X2Go istemci, örneğin kullanarak) bir grafik Masaüstü oturumundan çalıştırabilirsiniz. tooinvoke SQuirrel SQL, hello masaüstünde hello simgesinden başlatın veya hello Kabuğu komut aşağıdaki hello çalıştırın.

    /usr/local/squirrel-sql-3.7/squirrel-sql.sh

Merhaba ilk kullanmadan önce sürücüler ve veritabanı diğer adlar ayarlayın. Merhaba JDBC sürücüleri şu adreste bulunabilir:

*/usr/Share/Java/jdbcdrivers*

Daha fazla bilgi için bkz: [SQuirrel SQL](http://squirrel-sql.sourceforge.net/index.php?page=screenshots).

#### <a name="command-line-tools-for-accessing-microsoft-sql-server"></a>Microsoft SQL Server erişmek için komut satırı araçları
Merhaba ODBC sürücü paketi SQL Server için de iki komut satırı araçlarıyla birlikte gelir:

**BCP**: hello bcp yardımcı programı toplu bir kullanıcı tarafından belirtilen biçimde Microsoft SQL Server örneğini ve bir veri dosyası arasında veri kopyalar. Merhaba bcp yardımcı programı kullanılan tooimport çok sayıda yeni satırı SQL Server tablolarını ya da veri dosyalarını tablolara tooexport verileri olabilir. tooimport veri bir tabloya Bu tablo için oluşturulan bir biçim dosyası kullanmak, veya hello yapısını hello tablo ve hello sütunlarını için geçerli veri türlerini anlama.

Daha fazla bilgi için bkz: [bcp ile bağlanma](https://msdn.microsoft.com/library/hh568446.aspx).

**SQLCMD**: hello sqlcmd yardımcı programını, yanı sıra sistem yordamları Transact-SQL deyimi girin ve komut dosyaları hello komut isteminde. Bu yardımcı program ODBC tooexecute Transact-SQL toplu kullanır.

Daha fazla bilgi için bkz: [sqlcmd ile bağlanma](https://msdn.microsoft.com/library/hh568447.aspx).

> [!NOTE]
> Bu yardımcı programı, Linux ve Windows platformları arasında bazı farklar vardır. Ayrıntılar için Hello belgelerine bakın.
> 
> 

#### <a name="database-access-libraries"></a>Veritabanı erişimi kitaplıkları
Kitaplıkları R ve Python tooaccess veritabanlarında kullanılabilir.

* R içinde hello **RODBC** paket veya **dplyr** paket hello veritabanı sunucusunda SQL deyimlerini yürütmek veya tooquery sağlar.
* Python içinde hello **pyodbc** kitaplığı, temel alınan katman hello gibi ODBC ile veritabanı erişimi sağlar.  

### <a name="azure-tools"></a>Azure Araçları
Azure Araçları aşağıdaki hello hello VM üzerinde yüklenir:

* **Azure komut satırı arabirimi**: hello Azure CLI Kabuk komutları aracılığıyla Azure kaynaklarınızı yönetmek ve toocreate sağlar. tooinvoke Azure Araçları Merhaba, yalnızca yazın **azure Yardım**. Daha fazla bilgi için bkz: Merhaba [Azure CLI belge sayfasının](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* **Microsoft Azure Storage Gezgini**: Microsoft Azure Storage Gezgini araçtır, Azure depolama hesabı ve Azure blob'lara ait tooupload ve indirme veri tooand depoladığınız hello nesneleri aracılığıyla kullanılan toobrowse olan bir grafik. Depolama Gezgini hello masaüstü kısayolu simgesinden erişebilirsiniz. Yazarak, bir kabuk isteminde çağırabilirsiniz **StorageExplorer**. Bir X2Go istemciden oturum toobe gerekir veya yedekleme kümesi iletme X11 sahip.
* **Azure kitaplıkları**: hello aşağıdaki hello önceden yüklenmiş kitaplıkları bazıları verilmiştir.
  
  * **Python**: hello Azure ile ilgili kitaplıklar yüklenen python'da **azure**, **azureml**, **pydocumentdb**, ve **pyodbc** . İlk üç kitaplıkları ile Merhaba, Azure depolama hizmetleri, Azure Machine Learning ve Azure Cosmos DB (Azure üzerinde bir NoSQL veritabanı) erişebilir. Merhaba dördüncü kitaplığı, pyodbc (birlikte hello için Microsoft ODBC sürücüsü SQL Server), bir ODBC arabirimini kullanarak erişim tooSQL sunucu, Azure SQL Database ve Azure SQL Data Warehouse python'dan sağlar. Girin **PIP listesi** tüm hello toosee listelenen kitaplıkları. Her iki hello Python 2.7 Bu komutta ve 3.5 ortamları emin toorun olması.
  * **R**: yüklenen hello Azure ile ilgili kitaplıklarında R olan **AzureML** ve **RODBC**.
  * **Java**: Azure Java kitaplıkları hello listesi hello dizininde bulunabilir **/dsvm/sdk/AzureSDKJava** hello VM üzerinde. SQL Server için Azure depolama ve Yönetimi API'leri, Azure Cosmos DB ve JDBC sürücüleri Hello anahtar kitaplıkları alır.  

Merhaba erişebilirsiniz [Azure portal](https://portal.azure.com) hello önceden yüklenmiş Firefox tarayıcısından. Hello Azure portal, oluşturmak, yönetmek ve Azure kaynaklarını izleyin.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning toobuild sağlayan bir tam olarak yönetilen bir bulut hizmetidir, dağıtmak ve Tahmine dayalı analiz çözümlerini paylaşın. Azure Machine Learning Studio'dan denemeler ve modelleri oluşturun. Ziyaret ederek hello veri bilimi sanal makine üzerinde bir web tarayıcısından erişilebileceğini [Microsoft Azure Machine Learning](https://studio.azureml.net).

TooAzure Machine Learning Studio oturumu sonra erişim tooan deneme hello machine learning algoritmaları için mantıksal bir akış burada yapı tuvale sahip. Ayrıca erişim tooa Jupyter not defteri Azure Machine Learning üzerinde barındırılan sahip ve Machine Learning Studio'da hello denemeler sorunsuz bir şekilde çalışabilirsiniz. Merhaba machine learning web hizmeti arabiriminde kaydırma tarafından oluşturulan modelleri faaliyete. Bu, istemcilerin tüm dil tooinvoke tahminleri hello makine öğrenimi modellerinin oluşturulmasına yazılmış sağlar. Daha fazla bilgi için bkz: Merhaba [Machine Learning belge](https://azure.microsoft.com/documentation/services/machine-learning/).

Ayrıca Modellerinizi R veya Python hello VM üzerinde derleme ve Azure Machine learning'de üretimde dağıtın. Biz kitaplıkları R yüklü (**AzureML**) ve Python (**azureml**) tooenable bu işlev.

Nasıl toodeploy Azure Machine Learning R ve Python modelleri hakkında daha fazla bilgi için bkz: [hello veri bilimi sanal makine üzerinde yapabilir on nokta](machine-learning-data-science-vm-do-ten-things.md) (özellikle, hello bölüm "R veya Python kullanarak modelleri oluşturmak ve bunları faaliyete "Azure Machine Learning kullanarak").

> [!NOTE]
> Bu yönergeleri hello Windows sürümü hello veri bilimi VM için yazılmıştır. Ancak var. modelleri tooAzure Machine Learning dağıtmayı sağlanan hello bilgileri uygulanabilir toohello Linux VM.
> 
> 

### <a name="machine-learning-tools"></a>Machine learning araçları
Merhaba VM araçları ve önceden derlenmiş ve yerel olarak yüklenmiş algoritmaları öğrenme birkaç makineyle birlikte gelir. Bunlar:

* **Vowpal Wabbit**: hızlı çevrimiçi öğrenme algoritması.
* **xgboost**: en iyi duruma getirilmiş, boosted ağaç algoritmaları sağlayan bir araç.
* **Rattle**: kolay veri keşfi ve modelleme için bir R tabanlı grafik aracı.
* **Python**: Anaconda Python ile birlikte gelen machine learning algoritmaları Scikit öğrenin gibi kitaplıklarla birlikte gelir. Hello kullanarak diğer kitaplıkları yükleyebilirsiniz `pip install` komutu.
* **LightGBM**: framework artırmanın hızlı, dağıtılmış, yüksek performanslı gradyan karar ağacı algoritmalarına dayalı.
* **R**: machine learning işlevleri içeren zengin bir kitaplık r için kullanılabilir Önceden yüklenmiş hello kitaplıkları bazıları lm, glm, randomForest, rpart. Diğer kitaplıkları çalıştırarak yüklenebilir:
  
        install.packages(<lib name>)

İşte bazı ek bilgiler hello hakkında ilk üç machine learning araçları hello listesinde.

#### <a name="vowpal-wabbit"></a>Vowpal Wabbit
Vowpal Wabbit olan machine learning çevrimiçi, karma, allreduce, düşürülmesi, learning2search, etkin, gibi teknikler kullanır sistem ve etkileşimli öğrenme.

çok basit bir örnek toorun hello aracı hello aşağıdaki:

    cp -r /dsvm/tools/VowpalWabbit/demo vwdemo
    cd vwdemo
    vw house_dataset

Bu dizinde diğer, daha büyük gösterileri vardır. VW hakkında daha fazla bilgi için bkz: [GitHub'un bu bölümünde](https://github.com/JohnLangford/vowpal_wabbit)ve hello [Vowpal Wabbit wiki](https://github.com/JohnLangford/vowpal_wabbit/wiki).

#### <a name="xgboost"></a>xgboost
Bu, tasarlanmış ve boosted (ağacı) algoritmaları için en iyi hale getirilmiş bir kitaplıktır. Bu kitaplık Hello amacı tooprovide büyük ölçekli ağaç ölçeklenebilir, taşınabilir ve doğru olan artırmanın makineler toohello uç toopush hello hesaplama sınırları gerekli ' dir.

Bir R kitaplığı yanı sıra bir komut satırı sağlanır.

toouse R Bu kitaplık, etkileşimli bir R oturumu başlatmak için (yazarak yalnızca **R** hello Kabuğu'nda) ve yük hello kitaplığı.

R isteminde çalıştırarak basit bir örnek aşağıda verilmiştir:

    library(xgboost)

    data(agaricus.train, package='xgboost')
    data(agaricus.test, package='xgboost')
    train <- agaricus.train
    test <- agaricus.test
    bst <- xgboost(data = train$data, label = train$label, max.depth = 2,
                    eta = 1, nthread = 2, nround = 2, objective = "binary:logistic")
    pred <- predict(bst, test$data)

toorun hello xgboost komut satırı hello Kabuğu'nda hello komutları tooexecute şunlardır:

    cp -r /dsvm/tools/xgboost/demo/binary_classification/ xgboostdemo
    cd xgboostdemo
    xgboost mushroom.conf


.Model dosyası belirtilen toohello dizinine yazılır. Bu demo örnek hakkında bilgi bulunabilir [github'da](https://github.com/dmlc/xgboost/tree/master/demo/binary_classification).

Merhaba xgboost hakkında daha fazla bilgi için bkz: [xgboost belge sayfasının](https://xgboost.readthedocs.org/en/latest/)ve kendi [GitHub deposunu](https://github.com/dmlc/xgboost).

#### <a name="rattle"></a>Çıngırağı
Rattle (Merhaba **R** **A**nalytical **T**aracı **T**o **L**kazanmak **E** GUI tabanlı veri keşfi ve modelleme asily) kullanır. İstatistiksel gösterir ve veri, kolayca modellenir dönüşümler veri visual özetlerini hello veri Denetimsiz hem de denetimli modellerinden oluşturur, sunar modelleri performansını grafik hello ve puanları yeni verileri ayarlar. Ayrıca, doğrudan R çalıştırın ya da daha fazla çözümleme için bir başlangıç noktası olarak kullanılan hello işlemlerinde hello UI çoğaltma R kodu oluşturur.

toorun Çıngırağı, bir grafik Masaüstü Oturum açma oturumunda toobe gerekir. Merhaba terminalde yazın ```R``` tooenter hello R ortamı. Merhaba R isteminde aşağıdaki komutları hello girin:

    library(rattle)
    rattle()

Sekmeleri bir dizi artık bir grafik arabirim açılır. Hızlı Başlangıç bir model oluşturmak ve gerekli Çıngırağı toouse bir örnek hava veri kümesi adımlarını hello şunlardır. Bazı hello adımları, istendiğinde tooautomatically yükleme olan ve hello sistemde olmayan bazı gerekli R paketlerini yükleyin.

> [!NOTE]
> Access tooinstall hello paketi hello sistem dizininde (Merhaba varsayılan) yoksa, R konsol penceresi tooinstall paketleri tooyour kişisel kitaplığınızı bir ileti görebilirsiniz. Yanıt *y* bu komut istemlerini görürseniz.
> 
> 

1. **Yürüt**’e tıklayın.
2. Yukarı toouse hello örnek hava veri kümesi isteyip soran bir iletişim kutusu açılır. Tıklatın **Evet** tooload Merhaba örneği.
3. Merhaba tıklatın **modeli** sekmesi.
4. Tıklatın **yürütme** toobuild karar ağacı.
5. Tıklatın **çizin** toodisplay hello karar ağacı.
6. Hello tıklatın **orman** radyo düğmesinin ve tıklayın **yürütme** toobuild rastgele bir orman.
7. Merhaba tıklatın **değerlendir** sekmesi.
8. Hello tıklatın **Risk** radyo düğmesinin ve tıklayın **yürütme** toodisplay iki Risk (kümülatif) performans çizimleri.
9. Merhaba tıklatın **günlük** sekmesini tooshow hello işlemleri önceki hello R kodu oluştur.
   (Tooinsert ihtiyacınız Çıngırağı geçerli sürümünde hello tooa hata, bir  *#*  önüne karakter *... Bu günlüğünü Dışarı Aktar*  hello günlük hello metninde.)
10. Merhaba tıklatın **verme** adlı düğmesi toosave hello R betiği *weather_script. R* toohello giriş klasörü.

Çıngırağı ve r çıkabilirsiniz Oluşturulan hello R betiği değiştirebilir veya toorun olduğu gibi kullanın artık, dilediğiniz zaman toorepeat her şeyi içeren Rattle UI hello içinde yapılmadı. Özellikle yeni başlayanlar için R içinde bu tooquickly analiz yapın ve basit bir grafik arabiriminde otomatik olarak R toomodify kod oluşturma sırasında makine ve/veya öğrenin kolay bir yoludur.

## <a name="next-steps"></a>Sonraki adımlar
İşte öğrenme ve araştırması nasıl devam edebilirsiniz:

* Merhaba [hello Linux için veri bilimi sanal makine üzerinde veri bilimi](machine-learning-data-science-linux-dsvm-walkthrough.md) anlatım gösterir, tooperform birçok ortak veri bilimi hello Linux veri bilimi burada sağlanan VM ile nasıl görevler. 
* Bu makalede açıklanan hello araçları deneyerek veri bilimi VM üzerinde çeşitli veri bilimi araçları hello hello keşfedin. De çalıştırabilirsiniz *dsvm daha fazla bilgi* hello Kabuk hello VM üzerinde yüklü hello araçlarla ilgili temel bir giriş ve işaretçiler toomore bilgi hello sanal makine içinde üzerinde.  
* Toobuild uçtan uca analitik çözümler kullanarak sistematik olarak nasıl hello öğrenin [takım veri bilimi işlemi](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).
* Merhaba ziyaret [Cortana Analytics Galerisi](http://gallery.cortanaanalytics.com) machine learning ve veri analizi, kullanım hello Cortana Analytics Suite örnekleri için.

