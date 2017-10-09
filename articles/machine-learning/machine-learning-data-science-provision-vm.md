---
title: Microsoft Veri bilimi sanal makine aaaProvision hello | Microsoft Docs
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
ms.openlocfilehash: 907a3bdc7e480d05e8e245f5e50d632900fcf471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-microsoft-data-science-virtual-machine"></a>Merhaba Microsoft Veri bilimi sanal makine sağlama
Merhaba Microsoft Veri bilimi sanal makine önceden yüklenmiş ve veri analizi ve makine öğrenme için yaygın olarak kullanılan birkaç popüler araçları ile yapılandırılmış bir Windows Azure sanal makine (VM) görüntüsüdür. bulunan hello araçlar şunlardır:

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
  * [Rattle](http://rattle.togaware.com/) (R analitik aracı tooLearn kolayca hello): veri analizi ve R ile GUI tabanlı veri keşfi kolay öğrenme ve otomatik R kod oluşturma ile modelleme makine ile çalışmaya başlama sağlayan bir araç.
  * [mxnet](https://github.com/dmlc/mxnet): verimliliği ve esneklik için tasarlanmış bir derin öğrenme çerçevesi
  * [Weka](http://www.cs.waikato.ac.nz/ml/weka/) : görsel veri araştırma ve makine öğrenimi Java yazılım.
  * [Apache ayrıntıya](https://drill.apache.org/): bir şemasız SQL sorgu alt Hadoop, NoSQL ve bulut depolama.  ODBC ve JDBC arabirimleri tooenable NoSQL ve Power BI, Excel, Tableau gibi standart BI araçlarından dosyaları sorgulama destekler.
* Azure Machine Learning ve diğer Azure hizmetleriyle R ve Python için kitaplıkları kullanma
* Git Bash'i toowork GitHub, Visual Studio Team Services de dahil olmak üzere kaynak kodu depoları dahil olmak üzere Git
* Windows bağlantı noktalarını (awk azaltılabilir, perl, grep, Bul, wget, curl vb. dahil) çeşitli popüler Linux komut satırı yardımcı programlarını komut istemi üzerinden erişilebilir. 

Veri Bilimi bulunurken bir dizi görev yineleme içerir:

1. Bulma, yükleme ve verilerin önceden işlenmesi
2. Derleme ve modelleri test etme
3. Merhaba modelleri akıllı uygulamalarında tüketimi için dağıtma

Araçlar toocomplete çeşitli veri bilimcilerine bu görevleri kullanın. Bunu hello uygun hello yazılım sürümlerini oldukça uzun süren toofind olması ve ardından indirin ve yükleyin. Merhaba Microsoft Veri bilimi sanal makine, önceden yüklenmiş ve yapılandırılmış tüm çeşitli popüler araçları ile Azure'da sağlanabilir bir kullanıma hazır görüntüsü sağlayarak bu yük kolaylaştırabilir. 

Merhaba Microsoft Veri bilimi sanal makine analytics projenizi jump-starts. R, Python, SQL ve C# dahil olmak üzere çeşitli dillerde görevlerde toowork sağlar. Visual Studio IDE toodevelop sağlar ve kolay toouse olan kodunuzu test etmek. Hello Azure SDK'sını hello VM dahil, Microsoft'un bulut platformunda çeşitli Hizmetleri kullanarak uygulamalarınızı toobuild sağlar. 

Bu veri bilimi VM görüntüsü için yazılım harcamanız yok. Yalnızca hello boyutunu hello sanal makine sağlamanız hangi bağımlı hello Azure kullanım ücretleri için ödeme. Ücretler hello fiyatlandırma ayrıntıları bölümü hello üzerinde bulunabilir hello hakkında daha ayrıntılı bilgi işlem [veri bilimi sanal makine](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) sayfası. 

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Merhaba veri bilimi sanal makine diğer sürümleri
A [CentOS](machine-learning-data-science-linux-dsvm-intro.md) görüntü kullanılabilir Ayrıca, birçok hello ile aynı Windows görüntüsünü hello gibi araçları. Bir [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) görüntüdür de çok benzer araçların yanı sıra çerçeveleri öğrenme derin ile kullanılabilir.

## <a name="prerequisites"></a>Ön koşullar
Bir Microsoft Veri bilimi sanal makine oluşturmadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**: tooobtain bir, bkz: [alma Azure ücretsiz deneme sürümü](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Bir Azure depolama hesabı**: toocreate bir, bkz: [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account). Alternatif olarak, hello depolama hesabı toouse hesabınız istemiyorsanız hello VM oluşturma hello işleminin bir parçası olarak oluşturulabilir.

## <a name="create-your-microsoft-data-science-virtual-machine"></a>Microsoft Veri bilimi sanal makine oluşturma
Merhaba Microsoft Veri bilimi sanal makine örneği hello adımları toocreate şunlardır:

1. Toohello sanal makine üzerinde listeleme gidin [Azure portal](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).
2. Select hello **oluşturma** Sihirbazı'na gerçekleştirilecek hello alt toobe düğmesini.![ yapılandırma verileri-Bilim-vm](./media/machine-learning-data-science-provision-vm/configure-data-science-virtual-machine.png)
3. Microsoft Veri bilimi Virtual Machine gerektirir hello kullanılan sihirbaz toocreate hello **girişleri** her hello **beş adımı** üzerinde bu şekil sağında hello numaralandırılır. Merhaba gerekli girişleri tooconfigure her bu adımları şunlardır:
   
   1. **Temel Bilgiler**
      
      1. **Ad**: oluşturduğunuz veri bilimi sunucunuzun adını yazın.
      2. **Kullanıcı adı**: Yönetici hesap oturum açma kimliği.
      3. **Parola**: yönetici hesabı parolası.
      4. **Abonelik**: birden fazla aboneliğiniz varsa, select hello biri üzerinde hangi hello makine oluşturulur ve fatura toobe.
      5. **Kaynak grubu**: yeni bir tane oluşturun veya varolan bir grubu kullanın.
      6. **Konum**: en uygun seçim hello veri merkezi. Genellikle en hızlı ağ erişimi için en yakın tooyour fiziksel konumu veya verilerinizden en iyi sahip hello veri merkezi olur.
   2. **Boyutu**: işlev gereksinimi ve maliyet kısıtlamaları karşılayan hello sunucusu türlerinden birini seçin. Daha fazla seçenek VM boyutları "Tümünü Görüntüle" seçerek alabilirsiniz.
   3. **Ayarları**:
      
      1. **Disk türü**: seçin Premium katı hal sürücüsü (SSD) tercih ederseniz başka seçin "Standard".
      2. **Depolama hesabı**: aboneliğinizde yeni bir Azure depolama hesabı oluşturun veya mevcut bir hello kullanın aynı *konumu* üzerinde hello seçildi **Temelleri** hello Sihirbazı.
      3. **Diğer parametreler**: yalnızca genellikle hello varsayılan değerleri kullanın. Varsayılan olmayan değerleri tooconsider hello kullanımı istemeniz durumunda hello hello belirli alanlar hakkında Yardım için bilgi bağlantısı üzerinden gelebilirsiniz.
   4. **Özet**: girdiğiniz tüm bilgiler doğru olduğundan emin olun.
   5. **Satın**: tıklatın **satın** toostart hello sağlama. Bir bağlantı hello işlem toohello koşullarını sağlanır. Merhaba VM hello Seçtiğiniz hello sunucu boyutu hello işlem ötesinde herhangi bir ek ücret yok **boyutu** adım. 

> [!NOTE]
> Merhaba sağlama yaklaşık 10-20 dakika sürer. Merhaba sağlama hello durumu hello Azure portalı üzerinde görüntülenir.
> 
> 

## <a name="how-tooaccess-hello-microsoft-data-science-virtual-machine"></a>Microsoft Veri bilimi sanal makine tooaccess nasıl hello
Bir kez hello VM oluşturulduğunda, Uzak Masaüstü hello önceki yapılandırılmış hello yönetici hesabı kimlik bilgilerini kullanarak içine yapabilecekleriniz **Temelleri** bölümü. 

VM oluşturup sağlanan sonra yüklü ve yapılandırılmış hello araçlarını kullanmaya hazır toostart demektir. Başlat menüsü kutucukları ve birçok hello araçları masaüstü simgelerini vardır. 

## <a name="how-toocreate-a-strong-password-for-jupyter-and-start-hello-notebook-server"></a>Nasıl toocreate Jupyter ve başlangıç için güçlü bir parola hello not defteri sunucusu
Varsayılan olarak, hello Jupyter not defteri sunucu önceden yapılandırılmış ancak Jupyter parola ayarlanıncaya kadar hello VM üzerinde devre dışı. toocreate hello makinede yüklü hello Jupyter not defteri sunucu için güçlü bir parola, komutu bir komut isteminden veri bilimi sanal makine veya çift olması koşuluyla hello masaüstü kısayolu hello üzerinde aşağıdaki çalışma hello adlı  **Jupyter parolasını Ayarla & Başlangıç** yerel VM yönetici hesabından.

    C:\dsvm\tools\setup\JupyterSetPasswordAndStart.cmd

Merhaba iletileri izleyin ve istendiğinde güçlü bir parola seçin.

Merhaba önceki komut bir parola karması ve onu hello Jupyter yapılandırma dosyasında bulunan deposu oluşturur: **C:\ProgramData\jupyter\jupyter_notebook_config.py** hello parametre adı altında ***c. NotebookApp.password***.

Merhaba komut dosyası da sağlar ve hello Jupyter sunucu hello arka planda çalıştırın. Jupyter sunucusu hello WIndows Görev Zamanlayıcısı'nı windows görevde olarak oluşturulan **Start_IPython_Notebook**.  Tarayıcınız hello Not açmadan önce hello parola ayarlandıktan sonra birkaç saniye boyunca toowait olabilir. Başlıklı hello bölümüne bakın **Jupyter not defteri** nasıl tooaccess Jupyter not defteri sunucu hello üzerinde. 


## <a name="tools-installed-on-hello-microsoft-data-science-virtual-machine"></a>Microsoft Veri bilimi sanal makine Hello üzerinde yüklü araçları

### <a name="microsoft-r-server-developer-edition"></a>Microsoft R Server Geliştirici sürümü
Analizi için toouse R isterseniz hello VM yüklü Microsoft R Server Geliştirici sürümü vardır. Microsoft R Server geniş çapta dağıtılabilir kurumsal sınıf analytics desteklenen R bağlı, ölçeklenebilir ve güvenli platformudur. Büyük veri istatistikleri, Tahmine dayalı modelleme ve makine öğrenimi yetenekleri çeşitli destekleyici, R Server hello tam analytics – keşfi, analizi, Görselleştirme ve modelleme aralığını destekler. Kullanarak ve açık kaynak R genişletme Microsoft R Server tam R betiklerini, İşlevler ve CRAN paketleri, Kurumsal ölçekte tooanalyze veri ile uyumludur. Ayrıca, paralel ve öbekli verilerin işlenmesini ekleyerek hello bellek içi açık kaynak R sınırlamaları da giderir. Bu, verileri ana bellekte uygun'den çok büyük toorun analizi sağlar.  Visual Studio Community Edition VM r ile çalışmak için tam bir IDE sağlar Visual Studio uzantısı için hello R araçlarını içeren hello dahil Ayrıca indirmek ve diğer IDE de gibi kullandığınız [Rstudio'dan](http://www.rstudio.com). 

### <a name="python"></a>Python
Python kullanarak geliştirme için Anaconda Python 2.7 ve 3.5 dağıtım yüklendi. Bu dağıtım hello içeren Python yaklaşık 300 hello en popüler matematik, mühendislik ve veri analizi paketlerinin yanı sıra temel. Python araçları için Visual Studio (Merhaba Visual Studio 2015 Community edition veya boşta veya Spyder gibi Anaconda IDE birlikte hello biri içinde yüklü PTVS) kullanabilirsiniz. Bunlardan birini hello arama çubuğunda arayarak başlatın (**Win** + **S** anahtar).

> [!NOTE]
> toopoint hello Anaconda Python 2.7, Visual Studio için Python araçları ve 3.5, toocreate özel ortamları için her bir sürümü gerekir. tooset hello Visual Studio 2015 Community Edition, bu ortam yollarında gidin çok**Araçları** -> **Python Araçları** -> **Python ortamları** ve ardından **+ özel**. 
> 
> 

Anaconda Python 2.7 C:\Anaconda altında yüklenir ve c:\Anaconda\envs\py35 altında Anaconda Python 3.5 yüklenir. Bkz: [PTVS belgelerine](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) ayrıntılı adımlar için. 

### <a name="jupyter-notebook"></a>Jupyter Notebook
Anaconda dağıtım Ayrıca, bir ortam tooshare kodu ve analiz Jupyter not defteri ile birlikte gelir. Jupyter not defteri sunucu Python 2.7, Python 3.4, Python 3.5 ve R tekrar ile önceden yapılandırılmış. "Not Defteri sunucu Jupyter not defteri toolaunch hello tarayıcı tooaccess hello. adlı bir masaüstü simgesi yok Uzak Masaüstü hello VM kullanıyorsanız, de ziyaret edebilirsiniz [https://localhost:9999 /](https://localhost:9999/) tooaccess hello toohello VM oturum açıldığında Jupyter not defteri sunucu.

> [!NOTE]
> Hiçbir sertifika uyarısı alırsanız devam edin. 
> 
> 

Python birkaç örnek defterlerinde paketlenmiş ve r'de Jupyter not defterlerini göster nasıl hello toowork Microsoft R Server, SQL Server 2016 R Hizmetleri (veritabanı Analytics'i), Python, Microsoft Bilişsel Araç Seti (CNTK) ayrıntılı bilgi ve diğer Azure ile içinde tooJupyter oturum sonra teknolojileri. Toohello Jupyter not defteri bir önceki adımda oluşturduğunuz hello parola kullanarak kimlik doğrulaması sonra hello not defteri giriş sayfasında hello bağlantı toohello örneklerini görebilirsiniz. 

### <a name="visual-studio-2015-community-edition"></a>Visual Studio 2015 Community edition
Visual Studio Community edition Hello VM üzerinde yüklü. Merhaba, boş bir sürüm olduğu küçük ekipleri ve değerlendirme amaçları için kullanabileceğiniz bir Microsoft popüler IDE. Lisans koşullarını hello denetleyebilirsiniz [burada](https://www.visualstudio.com/support/legal/mt171547).  Merhaba Masaüstü simgesi veya hello çift tıklayarak Visual Studio'yu açın **Başlat** menüsü. Ayrıca programlarla arayabilirsiniz **Win** + **S** ve "Visual Studio" girme. C#, Python, R, node.js gibi dillerde projeleri burada oluşturabilirsiniz sonra. Eklentileri de Azure veri Kataloğu, Azure Hdınsight (Hadoop, Spark) ve Azure Data Lake gibi Azure hizmetleriyle kolay toowork hale yüklenir. 

> [!NOTE]
> Değerlendirme süreniz doldu bildiren bir ileti alabilirsiniz. Microsoft hesabı kimlik bilgilerinizi girin veya yeni bir ücretsiz hesap tooget erişim toohello Visual Studio Community Edition oluşturun. 
> 
> 

### <a name="sql-server-2016-developer-edition"></a>SQL Server 2016 Geliştirici sürümü
Bir geliştirici sürümü SQL Server 2016 R Hizmetleri toorun veritabanı Analytics'i hello VM üzerinde sağlanır. R hizmetler geliştirmek ve akıllı uygulamaları dağıtmak için bir platform sağlar. Hello zengin ve güçlü R dil kullanmak ve birçok paketleri hello topluluk toocreate modellerinden hello ve SQL Server verileri için tahminleri oluşturmak. R Hizmetleri (veritabanı-) hello R dil SQL Server ile tümleştirmek için analiz Kapat toohello verileri tutabilirsiniz. Bu hello maliyetleri ve veri taşıma ile ilişkili güvenlik riskleri ortadan kaldırır.

> [!NOTE]
> SQL Server 2016 Hello Geliştirici sürümü yalnızca geliştirme için kullanılabilir ve amacıyla sınayın. Bir lisans toorun gereken üretim içinde. 
> 
> 

Başlatarak hello SQL sunucusuna erişim sağlayabildiğinizden **SQL Server Management Studio**. VM adınızı hello sunucu adı doldurulur. Windows Yönetim Windows hello gibi oturum açıldığında kimlik doğrulaması kullanın. SQL Server Management Studio'da olduktan sonra diğer kullanıcıları oluşturun, veritabanları oluşturmak, veri içeri aktarın ve SQL sorguları çalıştırma. 

Microsoft R, komut bir olarak aşağıdaki hello Çalıştır'ı kullanarak tooenable veritabanı analytics zaman hello sunucu yönetici olarak oturum açtıktan sonra SQL Server management Studio'da eylemi. 

        CREATE LOGIN [%COMPUTERNAME%\SQLRUserGroup] FROM WINDOWS 

        (Please replace hello %COMPUTERNAME% with your VM name)


### <a name="azure"></a>Azure
Birkaç Azure Araçları hello VM üzerinde yüklenir:

* Hello Azure SDK Belgeleri masaüstü kısayolu tooaccess yoktur. 
* **AzCopy**: toomove verileri Microsoft Azure Storage hesabınız ve kullanılır. toosee kullanımı, türü **Azcopy** bir komut istemi toosee hello kullanımı sırasında. 
* **Microsoft Azure Storage Gezgini**: toobrowse, Azure depolama hesabı ve aktarım veri tooand Azure depolama biriminden içinde depolanan hello nesneleri aracılığıyla kullanılır. Yazabilirsiniz **Depolama Gezgini** arama veya Bul üzerinde hello Windows Başlat menüsünden tooaccess bu aracı. 
* **Adlcopy**: toomove veri tooAzure Data Lake kullanılır. toosee kullanımı, türü **adlcopy** bir komut isteminde. 
* **dtui**: toomove veri tooand Azure Cosmos DB'den hello buluttaki bir NoSQL veritabanı kullanılır. Tür **dtui** komut istemi üzerinde. 
* **Microsoft Veri Yönetimi ağ geçidi**: şirket içi veri kaynakları ve bulut arasında veri taşıma sağlar. Azure Data Factory gibi araçlar içinde kullanılır. 
* **Microsoft Azure Powershell**: bir aracı hello Powershell komut dosyası dili de kendi VM'nizi yüklü Azure kaynaklarınızı tooadminister kullanılan. 

### <a name="power-bi"></a>Power BI
toohelp, derleme panoları ve harika görselleştirmeleri hello **Power BI Desktop** yüklendi. Bu aracı toopull verileri farklı kaynaklardan tooauthor kullanması panoları ve raporları ve toopublish bunları toohello bulut. Bilgi için bkz: Merhaba [Power BI](http://powerbi.microsoft.com) site. Power BI desktop hello Başlat menüsünde bulabilirsiniz. 

> [!NOTE]
> Office 365 hesabı tooaccess Power BI gerekir. 
> 
> 

## <a name="additional-microsoft-development-tools"></a>Ek Microsoft geliştirme araçları
Merhaba [ **Microsoft Web Platformu yükleyicisi** ](https://www.microsoft.com/web/downloads/platform.aspx) kullanılan toodiscover kullanılabilir ve diğer Microsoft geliştirme araçları yükleyin. Sağlanan hello Microsoft Veri bilimi sanal makine Masaüstünde kısayol toohello aracı yoktur.  

## <a name="important-directories-on-hello-vm"></a>Merhaba VM önemli dizinleri
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
> Microsoft Veri bilimi sanal makine (önce 3 Eylül 2016) 1.5.0 önce oluşturulan hello örneklerini biraz farklı dizin yapısını tablo önceki hello belirtilenden kullanılır. 
> 
> 

## <a name="next-steps"></a>Sonraki Adımlar
Burada, öğrenme ve araştırması bazı sonraki adımları toocontinue bulunmaktadır. 

* Başlat menüsü ve başlangıç menüsünde listelenen hello araçları kullanıma hello veri bilimi VM hello tıklatarak çeşitli veri bilimi araçları hello keşfedin.
* Çok gidin**C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\RevoScaleR\demoScripts** hello RevoScaleR Kitaplığı'nda veri analizi Kurumsal ölçekte destekler R kullanan örnekler için.  
* Merhaba makale okuma: [hello veri bilimi sanal makine üzerinde yapabileceğiniz 10 şey](http://aka.ms/dsvmtenthings)
* Toobuild uç tooend analitik çözümleri sistematik olarak kullanarak nasıl hello öğrenin [takım veri bilimi işlemi](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).
* Merhaba ziyaret [Cortana Intelligence Galerisi](http://gallery.cortanaintelligence.com) machine learning ve veri analizi, kullanım hello Cortana Intelligence Suite örnekleri için. Ayrıca bir simge üzerinde hello sağladık **Başlat** menü ve hello masaüstünde hello sanal makine toothis Galerisi.

