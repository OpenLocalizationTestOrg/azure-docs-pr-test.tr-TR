---
title: "Microsoft Veri bilimi sanal makine sağlama | Microsoft Docs"
description: "Yapılandırma ve analizi için Azure üzerinde bir veri bilimi sanal makine oluşturun ve makine öğrenme."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e1467c0f-497b-48f7-96a0-7f806a7bec0b
ms.service: machine-learning
ms.workload: data-services
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 76cd54cd234dfe43e8f0d61f0b66f0ed0c09e8b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="provision-the-microsoft-data-science-virtual-machine"></a>Microsoft Veri Bilimi Sanal Makinesini sağlama
Microsoft Veri bilimi sanal makine önceden yüklenmiş ve veri analizi ve makine öğrenme için yaygın olarak kullanılan birkaç popüler araçları ile yapılandırılmış bir Windows Azure sanal makine (VM) görüntüsüdür. Bulunan araçlar şunlardır:

* Microsoft R Server Geliştirici sürümü
* Anaconda Python dağıtımı
* Jupyter Not Defteri (ile R, Python tekrar)
* Visual Studio Community Edition
* Power BI desktop
* SQL Server 2016 Geliştirici sürümü
* Machine learning ve veri analiz araçları
  * [Hesaplama ağ Araç Seti (CNTK)](https://github.com/Microsoft/CNTK): Microsoft Research yazılım araç Seti'nin öğrenme derin.
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): çevrimiçi, karma, allreduce, düşürülmesi, learning2search, etkin, gibi teknikler destekleme sistem öğrenme hızlı bir makine ve etkileşimli öğrenme.
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): hızlı ve doğru boosted ağaç uygulama sağlayan bir araç.
  * [Rattle](http://rattle.togaware.com/) (R analitik aracı için bilgi kolayca): veri analizi ve R ile GUI tabanlı veri keşfi kolay öğrenme ve otomatik R kod oluşturma ile modelleme makine ile çalışmaya başlama sağlayan bir araç.
  * [mxnet](https://github.com/dmlc/mxnet): verimliliği ve esneklik için tasarlanmış bir derin öğrenme çerçevesi
  * [Weka](http://www.cs.waikato.ac.nz/ml/weka/) : görsel veri araştırma ve makine öğrenimi Java yazılım.
  * [Apache ayrıntıya](https://drill.apache.org/): bir şemasız SQL sorgu alt Hadoop, NoSQL ve bulut depolama.  Sorgulama NoSQL ve Power BI, Excel, Tableau gibi standart BI araçları dosyalarından etkinleştirmek için ODBC ve JDBC arabirimleri destekler.
* Azure Machine Learning ve diğer Azure hizmetleriyle R ve Python için kitaplıkları kullanma
* Git Bash'i GitHub, Visual Studio Team Services de dahil olmak üzere kaynak kodu depoları ile çalışmak için de dahil olmak üzere Git
* Windows bağlantı noktalarını (awk azaltılabilir, perl, grep, Bul, wget, curl vb. dahil) çeşitli popüler Linux komut satırı yardımcı programlarını komut istemi üzerinden erişilebilir. 

Veri Bilimi bulunurken bir dizi görev yineleme içerir:

1. Bulma, yükleme ve verilerin önceden işlenmesi
2. Derleme ve modelleri test etme
3. Akıllı uygulamaları tüketimini modellerini dağıtma

Veri bilimcilerine, bu görevleri tamamlamak için çeşitli araçları kullanın. Oldukça uygun yazılım sürümlerini bulmak ve ardından indirin ve yükleyin zun olabilir. Microsoft Veri bilimi sanal makine, önceden yüklenmiş ve yapılandırılmış tüm çeşitli popüler araçları ile Azure'da sağlanabilir bir kullanıma hazır görüntüsü sağlayarak bu yük kolaylaştırabilir. 

Microsoft Veri bilimi sanal makine analytics projenizi jump-starts. R, Python, SQL ve C# dahil olmak üzere çeşitli dillerde görevler üzerinde çalışmanıza olanak tanır. Visual Studio geliştirmek ve kullanımı kolay kodunuzu test etmek için bir IDE sağlar. Azure VM'de bulunan SDK'sı, Microsoft bulut platformu üzerinde çeşitli Hizmetleri kullanarak uygulamalarınızı oluşturmanıza olanak verir. 

Bu veri bilimi VM görüntüsü için yazılım harcamanız yok. Yalnızca hangi bağımlı sağlamanız sanal makine boyutu için Azure kullanım ücretleri ödersiniz. Daha ayrıntılı bilgi işlem ücretleri fiyatlandırma Ayrıntıları bölümünde bulunabilir [veri bilimi sanal makine](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) sayfası. 

## <a name="other-versions-of-the-data-science-virtual-machine"></a>Veri bilimi sanal makinenin diğer sürümleri
A [CentOS](machine-learning-data-science-linux-dsvm-intro.md) görüntüdür de Windows görüntüsü olarak aynı araçları birçoğu ile kullanılabilir. Bir [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) görüntüdür de çok benzer araçların yanı sıra çerçeveleri öğrenme derin ile kullanılabilir.

## <a name="prerequisites"></a>Ön koşullar
Bir Microsoft Veri bilimi sanal makine oluşturmadan önce aşağıdakilere sahip olmanız gerekir:

* **Bir Azure aboneliği**: bir tane almak için bkz: [alma Azure ücretsiz deneme sürümü](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Bir Azure depolama hesabı**: oluşturmak için bkz: [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account). Alternatif olarak, depolama hesabı var olan bir hesabı kullanacak şekilde istemiyorsanız VM oluşturma işleminin bir parçası olarak oluşturulabilir.

## <a name="create-your-microsoft-data-science-virtual-machine"></a>Microsoft Veri bilimi sanal makine oluşturma
Örnek, Microsoft Veri bilimi sanal makine oluşturmak için adımlar şunlardır:

1. Sanal makine üzerinde listeleme gidin [Azure portal](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).
2. Seçin **oluşturma** Sihirbazı'na gerçekleştirilecek altındaki düğmesini.![ yapılandırma verileri-Bilim-vm](./media/machine-learning-data-science-provision-vm/configure-data-science-virtual-machine.png)
3. Microsoft Veri bilimi sanal makine oluşturmak için kullanılan sihirbazın gerektirir **girişleri** her biri için **beş adımı** Bu şekil sağ tarafta numaralandırılır. Bu adımların her biri yapılandırmak için gereken girdiler şunlardır:
   
   1. **Temel Bilgiler**
      
      1. **Ad**: oluşturduğunuz veri bilimi sunucunuzun adını yazın.
      2. **Kullanıcı adı**: Yönetici hesap oturum açma kimliği.
      3. **Parola**: yönetici hesabı parolası.
      4. **Abonelik**: birden fazla aboneliğiniz varsa, bir makine olduğu oluşturulur ve fatura için seçin.
      5. **Kaynak grubu**: yeni bir tane oluşturun veya varolan bir grubu kullanın.
      6. **Konum**: en uygun olan veri merkezi seçin. Genellikle verilerinizden en iyi veya en yakın fiziksel konumunuza en hızlı ağ erişimi için veri merkezi olur.
   2. **Boyutu**: işlev gereksinimi ve maliyet kısıtlamaları karşılayan sunucu türlerinden birini seçin. Daha fazla seçenek VM boyutları "Tümünü Görüntüle" seçerek alabilirsiniz.
   3. **Ayarları**:
      
      1. **Disk türü**: seçin Premium katı hal sürücüsü (SSD) tercih ederseniz başka seçin "Standard".
      2. **Depolama hesabı**: aboneliğinizde yeni bir Azure depolama hesabı oluşturun veya mevcut bir aynı kullanın *konumu* üzerinde seçildi **Temelleri** sihirbazın.
      3. **Diğer parametreler**: yalnızca genellikle varsayılan değerleri kullanın. Durumunda, varsayılan olmayan değerleri kullanmak isteyip istemediğinize karar belirli alanlar hakkında Yardım için bilgi bağlantısı üzerinden gelebilirsiniz.
   4. **Özet**: girdiğiniz tüm bilgiler doğru olduğundan emin olun.
   5. **Satın**: tıklatın **satın** sağlama başlatmak için. Bağlantı işlem koşullarını sağlanır. VM, seçtiğiniz sunucu boyutu işlem ötesinde herhangi bir ek ücret yok **boyutu** adım. 

> [!NOTE]
> Sağlama yaklaşık 10-20 dakika sürer. Sağlama durumu Azure portalda görüntülenir.
> 
> 

## <a name="how-to-access-the-microsoft-data-science-virtual-machine"></a>Microsoft Veri bilimi sanal makine erişme
VM oluşturulduktan sonra Uzak Masaüstü önceki yapılandırdığınız yönetici hesabı kimlik bilgilerini kullanarak içine yapabilecekleriniz **Temelleri** bölümü. 

VM oluşturup sağlanan sonra yüklenmiş ve yapılandırılmış Araçları'nı kullanmaya başlamak hazırsınız. Başlat menüsü döşeme ve araçlarının çoğu masaüstü simgelerini vardır. 

## <a name="how-to-create-a-strong-password-for-jupyter-and-start-the-notebook-server"></a>Jupyter için güçlü bir parola oluşturma ve not defteri sunucuyu Başlat
Varsayılan olarak, Jupyter not defteri sunucunun önceden yapılandırılmış ancak Jupyter parola ayarlanıncaya kadar VM devre dışı. Makinede yüklü Jupyter not defteri sunucu için güçlü bir parola oluşturmak için veri bilimi sanal makinede veya bir komut istemine aşağıdaki komutu olması koşuluyla Masaüstü kısayoluna çift Çalıştır adlı **Jupyter ayarlama Parola & Başlangıç** yerel VM yönetici hesabından.

    C:\dsvm\tools\setup\JupyterSetPasswordAndStart.cmd

İletileri izleyin ve istendiğinde güçlü bir parola seçin.

Önceki komut bir parola karması ve bunu Jupyter yapılandırma dosyasında bulunan deposu oluşturur: **C:\ProgramData\jupyter\jupyter_notebook_config.py** parametre adı altında ***c.NotebookApp.password***.

Komut dosyası da sağlar ve Jupyter server arka planda çalıştırın. WIndows Görev Zamanlayıcısı'nı windows görevde olarak Jupyter sunucusu oluşturulan **Start_IPython_Notebook**.  Tarayıcınız Not açmadan önce parola ayarlandıktan sonra birkaç saniye beklemeniz gerekebilir. Başlıklı bölümüne bakın **Jupyter not defteri** Jupyter not defteri sunucusuna erişmek nasıl. 


## <a name="tools-installed-on-the-microsoft-data-science-virtual-machine"></a>Microsoft Veri bilimi sanal makinede yüklü araçları

### <a name="microsoft-r-server-developer-edition"></a>Microsoft R Server Geliştirici sürümü
R analizi için kullanmak istiyorsanız, VM yüklü Microsoft R Server Geliştirici sürümü vardır. Microsoft R Server geniş çapta dağıtılabilir kurumsal sınıf analytics desteklenen R bağlı, ölçeklenebilir ve güvenli platformudur. Büyük veri istatistikleri, Tahmine dayalı modelleme ve makine öğrenimi yetenekleri çeşitli destekleyici, R Server analytics – keşfi, analizi, Görselleştirme ve modelleme tam aralığını destekler. Kullanarak ve açık kaynak R genişletme Microsoft R Server tam R betiklerini, İşlevler ve kurumsal ölçekte verileri çözümlemek için CRAN paketleri ile uyumludur. Ayrıca, açık kaynak R bellek içi sınırlamaları'nin veri paralel ve öbekli işlenmesini ekleyerek giderir. Bu verileri analytics çok daha büyük ne ana bellekte uygun çalıştırmanıza olanak sağlar.  R ile çalışmak için tam bir IDE sağlar Visual Studio uzantısı için R araçları Visual Studio Community Edition VM dahil içerir Ayrıca indirmek ve diğer IDE de gibi kullandığınız [Rstudio'dan](http://www.rstudio.com). 

### <a name="python"></a>Python
Python kullanarak geliştirme için Anaconda Python 2.7 ve 3.5 dağıtım yüklendi. Bu dağıtım yaklaşık 300 en popüler matematik, mühendislik ve veri analizi paketlerinin yanı sıra temel Python içerir. Python araçları için Visual Studio (Visual Studio 2015 Community edition veya paketlenmiş IDE boşta veya Spyder gibi Anaconda ile biri içinde yüklü PTVS) kullanabilirsiniz. Bu arama çubuğunda arayarak birini başlatabilirsiniz (**Win** + **S** anahtar).

> [!NOTE]
> Anaconda Python 2.7 ve 3.5 Visual Studio için Python araçları işaret etmek için her sürüm için özel ortamları oluşturmanız gerekir. Bu ortam yolları Visual Studio 2015 Community Edition ayarlamak için gidin **Araçları** -> **Python Araçları** -> **Python ortamları**ve ardından **+ özel**. 
> 
> 

Anaconda Python 2.7 C:\Anaconda altında yüklenir ve c:\Anaconda\envs\py35 altında Anaconda Python 3.5 yüklenir. Bkz: [PTVS belgelerine](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) ayrıntılı adımlar için. 

### <a name="jupyter-notebook"></a>Jupyter Notebook
Anaconda dağıtım ayrıca bir Jupyter not defteri ile kod ve analiz paylaşmak için bir ortamı bulunur. Jupyter not defteri sunucu Python 2.7, Python 3.4, Python 3.5 ve R tekrar ile önceden yapılandırılmış. "Jupyter not defteri sunucusuna erişmek için tarayıcı başlatmak için dizüstü bilgisayar adında bir masaüstü simgesi yok Uzak Masaüstü VM kullanıyorsanız, de ziyaret edebilirsiniz [https://localhost:9999 /](https://localhost:9999/) VM'ye oturum açıldığında Jupyter not defteri sunucusuna erişmek için.

> [!NOTE]
> Hiçbir sertifika uyarısı alırsanız devam edin. 
> 
> 

Biz birkaç örnek not defterlerini r ve Python de paketlenmiş Jupyter not defterleri için Jupyter oturum açtığında Microsoft R Server, SQL Server 2016 R Hizmetleri (veritabanı Analytics'i), Python, Microsoft Bilişsel Araç Seti (CNTK) ayrıntılı bilgi ve diğer Azure teknolojileri ile çalışmaya nasıl gösterir. Bir önceki adımda oluşturduğunuz parola kullanarak Jupyter not defteri için kimlik doğrulaması sonra not defteri giriş sayfasında örnekler bağlantısını görebilirsiniz. 

### <a name="visual-studio-2015-community-edition"></a>Visual Studio 2015 Community edition
Visual Studio Community edition VM'de yüklü. Küçük ekipleri ve değerlendirme amaçları için kullanabileceğiniz bir Microsoft popüler IDE boş bir sürümüdür. Lisans sözleşmesinin koşullarını denetleyebilirsiniz [burada](https://www.visualstudio.com/support/legal/mt171547).  Masaüstü simgesini çift tıklayarak Visual Studio'yu açın veya **Başlat** menüsü. Ayrıca programlarla arayabilirsiniz **Win** + **S** ve "Visual Studio" girme. C#, Python, R, node.js gibi dillerde projeleri burada oluşturabilirsiniz sonra. Eklentileri de Azure veri Kataloğu, Azure Hdınsight (Hadoop, Spark) ve Azure Data Lake gibi Azure hizmetleriyle çalışmak uygun hale yüklenir. 

> [!NOTE]
> Değerlendirme süreniz doldu bildiren bir ileti alabilirsiniz. Microsoft hesabı kimlik bilgilerinizi girin veya Visual Studio Community Edition erişmek için yeni bir boş hesabı oluşturun. 
> 
> 

### <a name="sql-server-2016-developer-edition"></a>SQL Server 2016 Geliştirici sürümü
Geliştirici sürümü SQL Server 2016 R hizmetleriyle veritabanı Analytics'i çalıştırmak için VM sağlanır. R hizmetler geliştirmek ve akıllı uygulamaları dağıtmak için bir platform sağlar. Model oluşturma ve SQL Server verileri için tahminleri oluşturmak için zengin ve güçlü R dil ve topluluktan birçok paketleri kullanabilirsiniz. R Hizmetleri (veritabanı-) R dil SQL Server ile tümleştirmek için analiz verileri yakın kullanmaya devam edebilir. Bu veri taşıma ile ilişkili güvenlik riskleri ve maliyetlerini ortadan kaldırır.

> [!NOTE]
> SQL Server 2016 Geliştirici sürümü yalnızca geliştirme ve test amaçları için kullanılabilir. Üretimde çalıştırmak için bir lisansınız olmalıdır. 
> 
> 

SQL server başlatarak erişebilirsiniz **SQL Server Management Studio**. VM adı sunucu adı olarak doldurulur. Windows Windows Yönetici olarak oturum açıldığında kimlik doğrulaması kullanın. SQL Server Management Studio'da olduktan sonra diğer kullanıcıları oluşturun, veritabanları oluşturmak, veri içeri aktarın ve SQL sorguları çalıştırma. 

Veritabanı Analytics'i Microsoft R kullanarak etkinleştirmek için bir tane aşağıdaki komutu çalıştırın zaman sunucu yönetici olarak oturum açtıktan sonra SQL Server management Studio'da eylemi. 

        CREATE LOGIN [%COMPUTERNAME%\SQLRUserGroup] FROM WINDOWS 

        (Please replace the %COMPUTERNAME% with your VM name)


### <a name="azure"></a>Azure
Birkaç Azure Araçları VM'de yüklü:

* Azure SDK Belgeleri erişmek için bir masaüstü kısayolu yoktur. 
* **AzCopy**: Microsoft Azure Storage hesabınız ve dışındaki veri taşımak için kullanılır. Kullanımını görmek için şunu yazın **Azcopy** kullanımını görmek için komut isteminde. 
* **Microsoft Azure Storage Gezgini**: Azure depolama hesabı ve aktarım verilerinizi Azure depolama gelen ve giden içinde depolanan nesneleri göz atmak için kullanılır. Yazabilirsiniz **Depolama Gezgini** içinde arama veya bu aracı erişmek için Windows Başlat menüsünden bulunamıyor. 
* **Adlcopy**: Azure Data Lake verileri taşımak için kullanılır. Kullanımını görmek için şunu yazın **adlcopy** bir komut isteminde. 
* **dtui**: verileri Azure Cosmos DB, bir NoSQL veritabanı bulut üzerinde gelen ve giden taşımak için kullanılır. Tür **dtui** komut istemi üzerinde. 
* **Microsoft Veri Yönetimi ağ geçidi**: şirket içi veri kaynakları ve bulut arasında veri taşıma sağlar. Azure Data Factory gibi araçlar içinde kullanılır. 
* **Microsoft Azure Powershell**: komut dosyası dili de kendi VM'nizi yüklü PowerShell'de Azure kaynaklarınızı yönetmek için kullanılan bir araçtır. 

### <a name="power-bi"></a>Power BI
Panolar ve harika görselleştirmeleri oluşturmanıza yardımcı olmak için **Power BI Desktop** yüklendi. Bu aracı panolarınızı ve raporlarınızı yazmak ve buluta yayımlamak için farklı kaynaklardan veri çekmek için kullanın. Bilgi için bkz: [Power BI](http://powerbi.microsoft.com) site. Power BI desktop Başlat menüsünde bulabilirsiniz. 

> [!NOTE]
> Power BI erişmek için Office 365 hesabı gerekir. 
> 
> 

## <a name="additional-microsoft-development-tools"></a>Ek Microsoft geliştirme araçları
[ **Microsoft Web Platformu yükleyicisi** ](https://www.microsoft.com/web/downloads/platform.aspx) bulmak ve diğer Microsoft geliştirme araçları'nı indirmek için kullanılabilir. Microsoft Veri bilimi sanal makine masaüstünde sağlanan aracı için bir kısayol yoktur.  

## <a name="important-directories-on-the-vm"></a>VM önemli dizinleri
| Öğe | Dizin |
| --- | --- |
| Jupyter not defteri sunucu yapılandırmaları |C:\ProgramData\jupyter |
| Jupyter not defteri örnekleri giriş dizini |c:\dsvm\notebooks |
| Diğer örnekleri |c:\dsvm\samples |
| Anaconda (varsayılan: Python 2.7) |c:\Anaconda |
| Anaconda Python 3.5 ortamı |c:\Anaconda\envs\py35 |
| R Server tek başına örneğini dizini (varsayılan R örneği üzerinde R3.2.2 tabanlı) |C:\Program Files\Microsoft SQL Server\130\R_SERVER |
| R Server-veritabanı örneği dizin (R3.2.2) |C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES |
| Microsoft R Aç (R3.3.1) örnek dizini |C:\Program Files\Microsoft\MRO-3.3.1 |
| Çeşitli araçlar |c:\dsvm\tools |

> [!NOTE]
> Örnekleri, Microsoft Veri bilimi (önce 3 Eylül 2016) 1.5.0 önce oluşturulan sanal makinenin bir biraz farklı dizin yapısı yukarıdaki tabloda belirtilenden kullanılır. 
> 
> 

## <a name="next-steps"></a>Sonraki Adımlar
Öğrenme ve araştırması devam etmek için İleri bazı adımlar şunlardır. 

* Çeşitli veri bilimi araçları veri bilimi VM Başlat menüsünden tıklatıp menüde listelenen araçları kullanıma keşfedin.
* Gidin **C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\RevoScaleR\demoScripts** veri analizi Kurumsal ölçekte destekler R RevoScaleR kitaplıkta kullanan örnekler için.  
* Makaleyi okuyun: [veri bilimi sanal makine yapabileceğiniz 10 şey](http://aka.ms/dsvmtenthings)
* Sistematik olarak kullanarak uçtan uca analitik çözümleri oluşturmayı öğrenin [takım veri bilimi işlemi](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).
* Ziyaret [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com) Cortana Intelligence Suite kullanan machine learning ve veri analizi örnekleri için. Ayrıca bir simge üzerinde sağladık **Başlat** menüsünde ve masaüstünde sanal makinenin Bu galeri.

