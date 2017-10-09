---
title: "üzerinde yapabilir aaaTen şeyler hello veri bilimi sanal makine | Microsoft Docs"
description: "Çeşitli veri keşfi ve modelleme görev hello veri bilimi sanal makine üzerinde gerçekleştirin."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 4dfe22f14f00208c63e26ce44b05123c9ac4b850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a>On hello veri bilimi sanal makine üzerinde yapabilecekleriniz
Hello Microsoft Veri bilimi sanal makine (DSVM), tooperform çeşitli veri keşfi ve modelleme görevleri sağlar güçlü veri bilimi geliştirme ortamıdır. Merhaba ortam zaten yerleşik ve beraberinde gelen çeşitli popüler verilerle kolay tooget olun analiz araçları hızlı bir şekilde şirket içi, Bulut veya karma çözümleme dağıtımları kullanmaya. Merhaba DSVM yakından çok sayıda Azure hizmetiyle çalışır ve mümkün tooread ve Azure, Azure SQL Data Warehouse, Azure Data Lake, Azure Storage veya Azure Cosmos veritabanı üzerinde depolanan işlem verileri. Bunu Azure Machine Learning ve Azure Data Factory gibi diğer analiz araçları da kullanabilirsiniz.

Bu makalede biz nasıl yol toouse çeşitli veri bilimi görevler ve diğer Azure hizmetleriyle etkileşime, DSVM tooperform. Merhaba DSVM üzerinde yapabileceğiniz hello şeylerden bazıları şunlardır:

1. Verileri araştırırken hello DSVM Microsoft R Server, Python kullanarak yerel olarak modellerinde geliştirin
2. Verilerinizi Python 2, Python 3, Microsoft R R ölçeklenebilirlik ve performans için tasarlanmış bir kurumsal hazır sürümünü kullanarak bir tarayıcı ile Jupyter not defteri tooexperiment kullanma
3. İstemci uygulamaları basit web Hizmetleri arabirimi kullanarak Modellerinizi erişebilmesi için R ve Python Azure Machine Learning kullanılarak oluşturulan modelleri faaliyete
4. Azure portal veya Powershell kullanarak Azure kaynaklarınızı yönetmek
5. Depolama alanını genişletmek ve büyük ölçekli veri kümeleri paylaşmak /, DSVM takılabilir bir sürücüde olarak Azure File storage oluşturarak tüm ekibinizin arasında kod
6. Kod GitHub kullanarak takımınızla paylaşmak ve deponuz hello önceden yüklenmiş Git istemciler - Git Bash Git GUI kullanarak erişebilirsiniz.
7. Çeşitli Azure veri ve Analiz Hizmetleri Azure blob depolama gibi Azure Data Lake, Azure Hdınsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & veritabanları erişim
8. Raporları ve panoyu Power BI Desktop DSVM hello üzerinde önceden yüklenmiş hello kullanarak oluşturmak ve bunları hello bulut üzerinde dağıtmak
9. Projenizi gerekir, DSVM toomeet dinamik ölçeklendirme
10. Ek araçlar sanal makinenize yükleyin   

> [!NOTE]
> Bu makalede listelenen hello ek veri depolama ve Analiz Hizmetleri birçoğu için ek kullanım ücretleri uygulanır. Lütfen toohello bakın [Azure fiyatlandırma](https://azure.microsoft.com/pricing/) Ayrıntılar için sayfa.
> 
> 

**Önkoşullar**

* Bir Azure aboneliği gerekir. Ücretsiz deneme için kaydolabilirsiniz [burada](https://azure.microsoft.com/free/).
* Hello Azure portalı üzerinde veri bilimi sanal makinenin sağlanması için yönergeler [bir sanal makine oluşturma](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a>1. Verileri araştırmak ve modeller Microsoft R Server veya Python kullanarak geliştirme
Merhaba üzerinde sağ DSVM veri analizi, R ve Python toodo gibi diller kullanabilirsiniz.

R için hello Başlat menüsünden veya hello Masaüstü bulunabilir "Revolution R Kurumsal 8.0" adlı bir IDE kullanabilirsiniz. Microsoft, ek kitaplıklara hello açık kaynak/CRAN-R tooenable ölçeklenebilir analizi ve hello özelliği tooanalyze verileri paralel öbekli analiz yaparak izin hello bellek boyutundan büyük üstünde sağlamıştır. Choice benzer, R IDE de yükleyebilirsiniz [Rstudio'dan](https://www.rstudio.com/products/rstudio-desktop/).

Python için Visual Studio Community hello Python araçları Visual Studio (PTVS) uzantısı önceden yüklenmiş olan sürümü gibi bir IDE kullanabilirsiniz. Varsayılan olarak, yalnızca temel bir Python 2.7 (olmadan herhangi bir analiz kitaplığı SciKit, Pandas gibi) üzerinde PTVS yapılandırılır. Sipariş tooenable Anaconda Python 2.7 ve 3.5 toodo hello aşağıdaki gerekir:

* Çok giderek her sürüm için özel ortamları oluşturma**Araçları** -> **Python Araçları** -> **Python ortamları** ve ardından " **+ Özel**"içinde hello Visual Studio 2015 Community Edition
* Bir açıklama girin ve önek yolları olarak hello ortamını ayarlama *c:\anaconda* Anaconda Python 2.7 veya *c:\anaconda\envs\py35* Anaconda Python 3.5 için
* Tıklatın **otomatik algıla** ve ardından **Uygula** toosave hello ortamı.

Visual Studio gibi görünüyor hangi hello özel ortam ayarlarının aşağıda verilmiştir.

![PTVS Kurulumu](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

Merhaba bkz [PTVS belgelerine](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) hakkında ek ayrıntılar için toocreate Python ortamları.

Şimdi yeni bir Python proje toocreate ayarlanır. Çok gidin**dosya** -> **yeni** -> **proje** -> **Python** ve hello türünü seçin Oluşturmakta olduğunuz Python uygulaması. Merhaba Python ortamı hello geçerli proje toohello istenen sürüm (Anaconda 2.7 ya da 3.5) için ayarlayabilirsiniz: sağ hello **Python ortamı**seçin **Ekle/Kaldır Python ortamları**, ve sonra Seç hello ortamı tooassociate hello proje ile istenen. Merhaba ürün PTVS ile çalışma hakkında daha fazla bilgi bulabilirsiniz [belgelerine](https://github.com/Microsoft/PTVS/wiki) sayfası.

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a>2. Bir Jupyter not defteri tooexplore ve model verilerinizi Python veya R ile kullanma
Merhaba Jupyter not defteri veri keşfi ve modelleme için bir tarayıcı tabanlı "IDE" sağlayan güçlü bir ortamdır. Python 2, Python 3 ya da R (açık kaynaklı ve hello Microsoft R Server) bir Jupyter not defteri kullanabilirsiniz.

toolaunch hello Jupyter not defteri hello Başlat menüsü simgesini tıklatın / Masaüstü simgesi başlıklı **Jupyter not defteri**. Merhaba DSVM üzerinde de çok göz atabilirsiniz "https://localhost:9999 /" tooaccess hello Jüpiter dizüstü bilgisayar. İçin bir parola ister, hello sunulan yönergeleri kullanın. ***nasıl toocreate hello Jupyter not defteri sunucuda güçlü bir parola*** hello bölümünü [sağlama hello Microsoft Veri bilimi sanal makine](machine-learning-data-science-provision-vm.md)konu toocreate güçlü parola tooaccess hello Jupyter not defteri. 

Merhaba dizüstü açtıktan sonra DSVM hello önceden paketlenmiş birkaç örnek dizüstü bilgisayarlar içeren bir dizini görmeniz gerekir. Artık şunları yapabilirsiniz:

* Merhaba not defteri toosee hello kodu tıklayın.
* Her bir hücre tuşlarına basarak yürütme **SHIFT-ENTER**.
* Merhaba tüm not tıklayarak çalıştırın **hücre** -> **çalıştırın**
* Merhaba Jupyter simgesi (sol üst köşesinde) üzerinde tıklattıktan sonra tıklatarak yeni bir not defteri oluşturma **yeni** hello sağ ve hello not defteri dili (tekrar olarak da bilinir) seçme düğmesi.   

> [!NOTE]
> Şu anda Python 2.7 destekliyoruz, Python 3.5 ve r hello R çekirdek hem açık kaynak R yanı sıra hello Kurumsal programlama destekleyen ölçeklenebilir Microsoft R Server.   
> 
> 

Hello not defterinde olduktan sonra verilerinizi keşfedin, hello model oluşturma, test seçiminizi kitaplıklarını kullanarak hello modeli.

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a>3. R veya Python ve Operationalize Azure Machine Learning kullanarak bunları kullanarak modelleri oluşturma
Yerleşik ve doğrulandı sonra model hello sonraki adımınız genellikle toodeploy olan üretim içine. Bu istemci uygulamaları tooinvoke hello modeli tahminlerin gerçek zamanlı veya toplu iş modu temelinde sağlar. Azure Machine Learning mekanizması toooperationalize R veya Python ile oluşturulmuş bir model sağlar.

Azure Machine Learning modelinizde faaliyete olduğunda, bir web hizmeti giriş parametreleri geçirin ve çıktı hello modelden Öngörüler almak toomake REST çağrılarını istemcilerinin veren açıktır.   

> [!NOTE]
> Henüz Azure Machine Learning için kaydolmadıysanız, boş bir çalışma alanında ya da standart çalışma hello ziyaret ederek edinebilirsiniz [Azure Machine Learning Studio](https://studio.azureml.net/) giriş sayfası ve tıklayarak üzerinde "Get Started".   
> 
> 

### <a name="build-and-operationalize-python-models"></a>Derleme ve Python faaliyete modelleri
Merhaba SciKit öğrenin kitaplığını kullanarak basit bir model oluşturur bir Python Jupyter not defterinde geliştirilmiş kod parçacığı aşağıda verilmiştir.

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

Merhaba yöntemi toodeploy python modelleri tooAzure Itanium tabanlı sistemler için Machine Learning sarmalayan hello tahmin hello modelinin bir işlevi olarak kullanılan ve Azure makineniz belirtmek hello önceden yüklenmiş Azure Machine Learning python kitaplığı tarafından sağlanan özniteliklerle süsler Learning çalışma alanı kimliği, API anahtarı ve hello giriş ile dönüş parametreleri.  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

Bir istemci çağrılarını toohello web hizmeti şimdi yapabilirsiniz. Merhaba REST API istekleri oluşturmak kolaylık sarmalayıcıları vardır. Bir örnek kod tooconsume hello web hizmeti aşağıda verilmiştir.

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> şu anda üretim Hello Azure Machine Learning kitaplığı yalnızca Python 2.7 üzerinde desteklenir.   
> 
> 

### <a name="build-and-operationalize-r-models"></a>Derleme ve faaliyete R modelleri
Python için yapılan benzer toohow olan bir şekilde hello veri bilimi sanal makine veya başka bir Azure Machine Learning üzerine yerleşik R modelleri dağıtabilirsiniz. Kendi hello adımlardır:

* Çalışma alanı kimliği ve kimlik doğrulama kodu örneği aşağıdaki hello gösterildiği gibi simge settings.json dosya tooprovide oluşturun.
* Merhaba modelinin işlevi tahmin etmek için bir sarmalayıcı yazma.
* çağrı ```publishWebService``` hello Azure Machine Learning kitaplığı toopass hello işlevi sarmalayıcı içinde içinde.  

Burada, kullanılan tooset yukarı, yapı, yayımlama, ve bir Azure Machine Learning web hizmeti olarak modeli tüketen hello yordam ve kod parçacıkları verilmiştir.

#### <a name="setup"></a>Kurulum
1. Yazarak Hello Machine Learning R paketini Yükle ```install.packages("AzureML")``` Revolution R Kurumsal 8.0 IDE veya R IDE.
2. Gelen RTools karşıdan [burada](https://cran.r-project.org/bin/windows/Rtools/). Machine Learning R paketi hello zip hello yol (ve adlandırılmış zip.exe) yardımcı programı toooperationalize gerekir.
3. Adlı bir dizin altında settings.json dosyası oluşturma ```.azureml``` giriş dizininize altında ve Azure Machine Learning alanınızdan hello parametreleri girin:

Settings.JSON dosya yapısı:

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a>R bir model oluşturmak ve Azure Machine Learning ile yayımlama
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function toopublish based on hello model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a>Azure Machine Learning ile dağıtılan hello model kullanma
bir istemci uygulamasından tooconsume hello model, kullandığımız hello Azure Machine Learning kitaplığı toolook hello yukarı web hizmeti hello kullanarak adı tarafından yayımlanan `services` API çağrısı toodetermine hello uç noktası. Yalnızca hello çağrı sonra `consume` işlev ve hello veri çerçeve toobe tahmin içinde geçirin.
koddan hello bir Azure Machine Learning web hizmeti olarak yayımlanan kullanılan tooconsume hello modelidir.

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

Hello Azure Machine Learning R Kitaplığı hakkında daha fazla bilgi bulunabilir [burada](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a>4. Azure portal veya Powershell kullanarak Azure kaynaklarınızı yönetmek
Merhaba DSVM yalnızca verir toobuild analytics çözümünüzü yerel olarak hello sanal makine, ancak Microsoft Azure bulut üzerinde tooaccess hizmetleri sağlar. Azure birkaç işlem, depolama, veri analizi Hizmetleri ve yönetmek ve sizin DSVM erişim diğer hizmetler sağlar.

tooadminister tarayıcı ve noktası toothe kullanabilirsiniz, Azure aboneliği ve bulut kaynaklarınızı [Azure portal](https://portal.azure.com). Azure Powershell tooadminister de, Azure aboneliği ve kaynakların bir komut dosyası aracılığıyla da kullanabilirsiniz.
Azure Powershell hello masaüstünde bir kısayoldan çalıştırmak veya hello Başlat menüsü "Microsoft Azure Powershell" başlıklı. Başvurmak [Microsoft Azure Powershell belgelerine](../powershell-azure-resource-manager.md) Azure aboneliği ve Windows Powershell betiklerini kullanarak kaynakları nasıl yönetebileceğiniz hakkında daha fazla bilgi.

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a>5. Depolama alanınızı paylaşılan dosya sistemiyle genişletme
Veri bilimcilerine büyük veri kümeleri, kod veya başka kaynaklara hello takım içindeki paylaşabilirsiniz. Merhaba DSVM kendisini yaklaşık 70 GB alanınız vardır. tooextend depolama alanınızın kullandığınız hello Azure dosya hizmeti ve DSVM hello üzerinde bağlayın veya bir REST API üzerinden erişim.   

> [!NOTE]
> Merhaba maksimum alan hello Azure dosya hizmeti paylaşımının 5 TB ve tek tek dosya boyutu sınırı 1 TB.   
> 
> 

Azure Powershell toocreate bir Azure dosya hizmeti paylaşımı kullanabilirsiniz. Burada, Azure PowerShell toocreate bir Azure dosya hizmeti paylaşımı altında hello betik toorun verilmiştir.

    # Authenticate tooAzure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under hello FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List hello share tooconfirm that everything worked
    Get-AzureStorageFile -Share $s


Azure dosya paylaşımının oluşturduğunuza göre herhangi bir sanal makine azure'da bağlayabilir. Bu hello VM aynı Azure veri merkezi olarak hello depolama hesabı tooavoid gecikmesi ve veri aktarımı ücretlerine olan önerilir. Merhaba, Azure Powershell çalıştırabilirsiniz DSVM hello komutları toomount hello sürücü şunlardır.

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


Artık herhangi normal bir sürücüye hello VM üzerinde yaptığınız gibi bu sürücüyü erişebilirsiniz.

## <a name="6-share-code-with-your-team-using-github"></a>6. Kod GitHub kullanarak takımınızla paylaşmak
GitHub hello Geliştirici topluluğu tarafından paylaşılan çeşitli teknolojiler kullanılarak farklı araçlar için örnek kod ve kaynakları çok bulabileceğiniz bir kod depodur. Teknoloji tootrack ve Deposu sürümleri hello kod dosyaları hello gibi Git kullanır. GitHub, ayrıca bir platformdur kendi depo toostore ekibinizin paylaşılan kodu ve belgeler, oluşturabileceğiniz sürüm denetimi ve aynı zamanda Denetim erişim tooview olan ve kod katkıda uygular. Lütfen başlangıç adresini ziyaret edin [GitHub yardım sayfalarına](https://help.github.com/) Git kullanma hakkında daha fazla bilgi için. GitHub hello yolları toocollaborate biri olarak ekibinizle kullanın, hello topluluk tarafından geliştirilmiş kodu kullanın ve kod geri toohello topluluğa katkıda.

Merhaba DSVM zaten iyi GUI tooaccess GitHub deposunu komut satırı hem istemci araçları ile yüklenen gelir. Git ve GitHub ile Merhaba komut satırı aracı toowork Git Bash adı verilir. Merhaba DSVM üzerinde yüklü visual Studio hello Git uzantısına sahip. Bu araçları hello Başlat menüsü ve hello Masaüstü için başlangıç simge bulabilirsiniz.

toodownload kodu Github'da depodan hello kullan ```git clone``` komutu. Örneğin hello geçerli dizine Microsoft tarafından yayımlanan toodownload veri bilimi havuzu hello içinde olduktan sonra aşağıdaki komutu çalıştırabilirsiniz ```git-bash```.

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

Visual Studio'da bunu hello aynı kopyalama işlemi. Aşağıdaki ekran görüntüsünde hello nasıl tooaccess Git ve GitHub Visual Studio Araçları gösterir.

![Visual Studio'da Git](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

Git toowork GitHub deponuz github.com'u üzerinde kullanılabilir çeşitli kaynaklardan ile kullanma hakkında daha fazla bilgi bulabilirsiniz. Merhaba [kopya sayfası](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) yararlı bir başvurudur.

## <a name="7-access-various-azure-data-and-analytics-services"></a>7. Çeşitli Azure verileri ve çözümlemeler hizmetlere erişme
### <a name="azure-blob"></a>Azure Blob
Azure blob verileri büyük ve küçük için güvenilir ve ekonomik bulut Depolama ' dir. Bize nasıl veri tooAzure Blob ve bir Azure Blob depolanan verilere erişmek taşıyabilir adresindeki arayın.

**Önkoşul**

* **Azure Blob storage hesabınızdan oluşturma [Azure portal](https://portal.azure.com).**

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Bu hello önceden yüklenmiş komut satırı AzCopy aracı adresindeki bulunduğunda onaylayın ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```. Bu aracı çalıştırırken hello dizin içeren hello azcopy.exe tooyour yol ortam değişkeni tooavoid yazarak hello tam komut yolu ekleyebilirsiniz. AzCopy aracı hakkında daha fazla bilgi için lütfen çok başvurun[AzCopy belgeleri](../storage/common/storage-use-azcopy.md)
* Hello Azure Storage Gezgini aracını başlatın. Adresten yüklenebilir [Microsoft Azure Storage Gezgini](http://storageexplorer.com/). 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

**VM tooAzure Blob ' veri taşıma: AzCopy**

blob depolama ve yerel dosyalarınızı arasında toomove verileri, kullanabileceğiniz AzCopy komut satırında veya PowerShell:

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

Değiştir **C:\myfolder** dosyanızı depolandığı toohello yolu **mystorageaccount** tooyour blob depolama hesabı adı, **mycontainer** toohello kapsayıcı adı **depolama hesabı anahtarı** tooyour blob depolama erişim tuşu. Depolama hesabı kimlik bilgilerinizi bulabilirsiniz [Azure portal](https://portal.azure.com).

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

PowerShell veya bir komut isteminden AzCopy komutunu çalıştırın. Bazı örnek kullanım AzCopy komut şöyledir:

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



Çalıştırdığınız sonra AzCopy komut toocopy tooan dosyanızı gördüğünüz Azure blob Azure Storage Gezgini kısa süre içinde görüntülenir.

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

**VM tooAzure Blob ' veri taşıma: Azure Storage Gezgini**

Azure Depolama Gezgini'ni kullanarak, VM'yi hello yerel dosya verileri de karşıya yükleyebilirsiniz:

* tooupload veri tooa kapsayıcısı, select hello hedef kapsayıcı ve tıklatın hello **karşıya** düğmesini.![ Depolama Gezgini'nde karşıya yükle](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)
* Tıklatın hello üzerinde **...**  hello sağında toohello **dosyaları** kutusunda, bir veya birden çok dosya tooupload hello dosya sisteminden seçin ve'ı tıklatın **karşıya** hello dosyaları karşıya yükleme toobegin.![ Dosyaları tooblob karşıya yükle](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)

**Verileri Azure Blob'tan okuyun: Machine Learning okuyucu Modülü**

Azure Machine Learning Studio'da kullanabileceğiniz bir **veri içeri aktarma modülü** , blob tooread verileri.

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

**Verileri Azure Blob'tan okuyun: Python ODBC**

Kullanabileceğiniz **BlobService** kitaplığı tooread verileri doğrudan Jupyter Not Defteri veya Python programında blob.

İlk olarak, gerekli paketleri içeri aktarın:

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random

Ardından Azure Blob hesabı kimlik bilgilerinizi Tak ve Kullan veri Blobundan okuyun:

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds toodownload "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'hello size of hello data is: %d rows and  %d columns' % df1.shape

Merhaba veriler, veri çerçeve olarak okunur:

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a>Azure Data Lake
Azure Data Lake Store, büyük veri analitik iş yükleri ve uyumlu olan Hadoop dağıtılmış dosya sistemi (HDFS) için hiper ölçekli bir depodur. Merhaba Hadoop ekosistemi ve hello Azure Data Lake Analytics ile çalışır. Nasıl hello Azure Data Lake Store verilerini taşımak ve Azure Data Lake Analytics'i kullanarak analizler çalıştırır gösteriyoruz.

**Önkoşul**

* İçinde Azure Data Lake Analytics oluşturma [Azure portal](https://portal.azure.com).

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* Merhaba **Azure Data Lake Araçları** içinde **Visual Studio** şu anda bulunan [bağlantı](https://www.microsoft.com/download/details.aspx?id=49504) hello Visual Studio Community hello sanal makinede olan sürümü zaten yüklü. Visual Studio başlangıç ve Azure aboneliğinizde oturum sonra Azure Data Analytics hesabınızı ve Visual Studio'nun hello sol panelinde depolama görmeniz gerekir.

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

**VM tooData Lake veri taşıma: Azure Data Lake Gezgini**

Kullanabileceğiniz **Azure Data Lake Explorer** hello yerel dosyaları, sanal makine tooData Lake depolama tooupload verileri.

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

Hello kullanarak, veri taşıma tooor Azure Data Lake gelen veri ardışık düzen tooproductionize oluşturabilir [Azure veri Factory(ADF)](https://azure.microsoft.com/services/data-factory/). Biz toothis başvuran [makale](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide hello adımları toobuild hello veri size ardışık düzenleri.

**Azure Blob tooData Lake veri okuma: U-SQL**

Verileriniz Azure Blob depolama alanına bulunuyorsa, U-SQL sorgusunda Azure depolama blobunu gelen verileri doğrudan okuyabilir. U-SQL sorgusu oluşturma önce bağlantılı tooyour Azure Data Lake blob storage hesabı olduğundan emin olun. Çok Git**Azure portal**, Azure Data Lake Analytics panonuz bulmak, tıklatın **veri kaynağı Ekle**, çok depolama türü seçin**Azure Storage** ve Azure Storage'da takın Anahtar ve hesap adı. Ardından, hello depolama hesabında depolanan mümkün tooreference hello verilerdir.

![Depolama hesabı ve anahtarı girin](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

Visual Studio'da veri blob depolama alanından okuyun, bazı veri işleme, özellik Mühendisliği ve çıktı hello ortaya çıkan veri tooeither Azure Data Lake veya Azure Blob Storage yapın. Blob depolama birimindeki hello veri başvurduğunuzda kullanmak **wasb: / /**; Azure Data Lake, kullanım hello verilerde başvurduğunuzda **swbhdfs: / /**

![Veri çerçevesi](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

Visual Studio'da U-SQL sorguları aşağıdaki hello kullanabilirsiniz:

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    too"swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    too"wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



Merhaba, işin durumunu gösteren bir diyagram sorgunuzu gönderilen toohello sunucusudur sonra görüntülenir.

![İş durumu diyagramı](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

**Data Lake veri sorgulama: U-SQL**

Azure Data Lake Hello dataset alınan sonra kullanabileceğiniz [U-SQL dili](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery ve hello verileri keşfedin. U-SQL dili benzer Systems SQL olmakla birlikte, böylece kullanıcılar özelleştirilmiş modüller, kullanıcı tanımlı işlevler ve vb. yazabilirsiniz bazı C# özellikleri birleştirir. Merhaba önceki adımda hello komut dosyalarını kullanabilirsiniz.

Merhaba sorgu gönderilen tooserver, tripdata_summary sonra. CSV, kısa süre içinde bulunabilir **Azure Data Lake Explorer**, sağ hello dosyası tarafından hello verileri önizleyin.

![Azure Data Lake Gezgini'ndeki Dosya](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

toosee hello dosya bilgileri:

![Dosya Özeti](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a>Hdınsight Hadoop kümeleri
Azure Hdınsight bir yönetilen Apache Hadoop, Spark, HBase ve Storm hello buluttaki hizmetidir. Azure Hdınsight kümeleri hello veri bilimi sanal makineden kolayca çalışabilirsiniz.

**Önkoşul**

* Azure Blob storage hesabınızdan oluşturma [Azure portal](https://portal.azure.com). Bu depolama hesabı, Hdınsight kümeleri için kullanılan toostore verilerdir.

![Azure Blob storage hesabı oluşturma](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Azure Hdınsight Hadoop kümelerini gelen özelleştirme [Azure portalı](machine-learning-data-science-customize-hadoop-cluster.md)
  
  * Hdınsight kümenizle oluşturulduğunda oluşturulan hello depolama hesabı bağlamanız gerekir. Bu depolama hesabı hello küme içinde işlenebilecek verilerine erişmek için kullanılır.

![Hdınsight kümesi ile oluşturulan bağlantı toostorage hesabı](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* Etkinleştirmelisiniz **uzaktan erişim** oluşturulduktan sonra hello küme baş düğümüne toohello. Burada belirttiğiniz (Merhaba küme oluşturma sırasında belirtilen kullanılanlardan farklı) başlangıç uzaktan erişim kimlik bilgilerini Hatırla: hello sonraki yordamda gerekir.

![Uzaktan erişimi etkinleştirin](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* Bir Azure Machine Learning çalışma alanı oluşturun. Makine öğrenimi denemelerine bu Machine Learning çalışma alanında depolanır. Vurgulanan hello seçenekleri portalında hello ekran aşağıdaki gösterildiği gibi seçin:

![Bir Azure Machine Learning çalışma alanı oluşturma](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* Ardından hello parametreleri için çalışma alanınızı girin

![Machine Learning çalışma alanı parametreleri girin](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* IPython Not Defteri kullanarak verileri karşıya yükleyin. İlk gerekli paketleri içeri aktarmak, kimlik bilgilerini takın, bir db depolama hesabınızı oluşturmak ve sonra veri tooHDI kümelerini yüklemek.

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create hello connection tooHive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage tooHDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* Alternatif olarak, bu izleyebilirsiniz [izlenecek](machine-learning-data-science-process-hive-walkthrough.md) tooupload NYC ücreti verileri tooHDI küme. Önemli adımlar şunlardır:
  
  * AzCopy: CSV ait ortak blob tooyour yerel klasörden sıkıştırılmış indirme
  * AzCopy: sıkıştırması açılmış CSV ait yerel klasör tooHDI kümeden karşıya yükle
  * Merhaba baş Hadoop küme düğümüne oturum ve keşif veri analizi için hazırlama

Merhaba veri yüklenen tooHDI küme sonra verilerinizi Azure Storage Gezgini kontrol edebilirsiniz. Ve HDI kümesi içinde oluşturulan bir veritabanı nyctaxidb vardır.

**Veri keşfi: Python Hive sorguları**

Merhaba verileri Hadoop kümesinde olduğundan, hello pyodbc paket tooconnect tooHadoop kullanabilirsiniz kümeleri ve Hive toodo araştırması ve özellik Mühendisliği kullanarak veritabanını sorgula. Merhaba varolan tablolardan hello önkoşul adımda oluşturduğumuz görüntüleyebilirsiniz.

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Var olan tabloları görüntüleme](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

Her ay ve hello sıklıkları kayıt hello sayısı bakalım Eğimli veya hello seyahat tablosunda yok:

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![Çizim kayıtları her ay sayısı](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![İpucu frekansların çizim](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

Biz de toplama konumu ve dropoff konumu arasındaki hello uzaklığı işlem ve toohello karşılaştırmak seyahat uzaklığı.

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![Toplama ve dropoff tablosu](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![Alma/dropoff uzaklığı tootrip uzaklığı çizim](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

Şimdi şimdi modelleme için bir aşağı örneklenen (% 1) veri kümesi hazırlayın. Machine Learning okuyucu modülünde size bu verileri kullanabilirsiniz.

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of hello join into hello preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

Bir süre sonra hello verileri Hadoop kümeleri yüklenen görebilirsiniz:

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Veri tablosu](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

**Machine Learning kullanarak HDI veri okuma: okuyucu Modülü**

Merhaba de kullanabilir **okuyucu** modülü Machine Learning Studio tooaccess hello veritabanındaki Hadoop kümesi. Hello kimlik bilgileri, HDI kümelerin Tak ve Azure depolama hesabı tooenable lık machine learning HDI kümelerde veritabanını kullanarak modelleri oluşturun.

![Okuyucu modülü özellikleri](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

Merhaba puanlanmış veri kümesi ardından görüntülenebilir:

![Puanlanmış veri kümesini görüntülemek](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a>Azure SQL Data Warehouse & veritabanları
Azure SQL Data Warehouse kurumsal sınıf SQL Server deneyimi hizmetiyle bir esnek veri ambarı gibidir.

Bu konuda sağlanan hello yönergeleri izleyerek, Azure SQL Data Warehouse sağlayabilirsiniz [makale](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md). Azure SQL veri ambarı sağlamak sonra bunu kullanabilirsiniz [izlenecek](machine-learning-data-science-process-sqldw-walkthrough.md) araştırması ve modelleme kullanarak verileri hello SQL Data Warehouse içinde toodo veri yükleme.

#### <a name="azure-cosmos-db"></a>Azure Cosmos DB
Azure Cosmos DB hello bulutta bir NoSQL veritabanıdır. JSON gibi belgelerle toowork sağlar ve toostore ve sorgu hello belgeler sağlar.

Koşullar başına adımları tooaccess Azure Cosmos DB DSVM hello aşağıdaki toodo hello gerekir.

1. DocumentDB Python SDK'sını yükleyin (çalıştırmak ```pip install pydocumentdb``` komut isteminden)
2. Bir Azure Cosmos DB hesap oluşturup bir veritabanından [Azure portalı](https://portal.azure.com)
3. "Azure Cosmos DB geçiş aracı" indirin [burada](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) ve tercih ettiğiniz tooa dizine ayıklayın
4. Alma depolanmış JSON verilerini (volcano) bir [ortak blob](https://cahandson.blob.core.windows.net/samples/volcano.json) Cosmos DB aşağıdaki komut parametreleri toohello Geçiş Aracı (Merhaba Cosmos DB geçiş aracı yüklendiği hello dizininden dtui.exe) ile içine. Bu parametreler ile Merhaba kaynak ve hedef konumu girin:
   
    /s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/; AccountKey = [[anahtar]; veritabanı volcano /t.Collection:volcano1 =

Bir kez hello veri içe aktardıktan sonra tooJupyter ve açık hello dizüstü başlıklı gidebilirsiniz *DocumentDBSample* python içeren tooaccess DocumentDB kod ve bazı temel sorgulama yapın. Cosmos DB hakkında daha fazla hello hizmet adresini ziyaret ederek bilgi [belge sayfasının](https://docs.microsoft.com/azure/cosmos-db/).

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a>8. Raporları ve panoyu Power BI Desktop hello kullanarak derleme
Bize Power BI toogain visual Öngörüler hello veri içinde Cosmos DB örnek önceki hello içinde gördüğümüz hello Volcano JSON dosyası görselleştirin. Ayrıntılı adımlar hello kullanılabilir [Power BI makale](../cosmos-db/powerbi-visualize.md). Merhaba üst düzey adımlar şunlardır:

1. Power BI Desktop açın ve "Veri Al" yapın. Merhaba URL'yi belirtin: https://cahandson.blob.core.windows.net/samples/volcano.json
2. Bir liste olarak alınan hello JSON kayıtlar görmeniz gerekir
3. Power BI ile Merhaba aynı çalışabilmeniz için hello listesi tooa tablosunda Dönüştür
4. Genişletme hello sütunlar üzerinde hello tıklayarak genişletin simgesi (Merhaba bir hello sütun sağında hello hello "sol ve sağ ok" simgesine ile)
5. Konum "Kayıt" alanını olduğuna dikkat edin. Merhaba kaydı'nı genişletin ve yalnızca hello koordinatları seçin. Liste sütununu koordinat değil
6. Yeni bir sütun tooconvert hello listesi koordinat sütun hello formülü kullanarak hello koordinat listesi alanı hello iki öğeleri birleştirme virgülle ayrı LatLong sütununa eklemek ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.
7. Son olarak hello Dönüştür ```Elevation``` sütun tooDecimal ve select hello **Kapat** ve **Uygula**.

Adımları önceki yerine, yapıştırabilirsiniz hello adımlar kullanılan komutlar koddan hello hello Gelişmiş Düzenleyici Power bı'da bir sorgu dili toowrite hello veri dönüşümlerine izin verir.

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



Artık Power BI veri modelinizi hello veri içeriyor. Power BI desktop aşağıdaki gibi görünmelidir:

![Power BI desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

Raporlar ve görselleştirmeleri hello veri modelini kullanarak oluşturmaya başlayabilirsiniz. Bu başlangıç adımları izleyebilirsiniz [Power BI makale](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild bir rapor. Merhaba sonuç hello şuna benzeyen bir rapordur.

![Power BI Desktop rapor görünümü - Power BI Bağlayıcısı](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a>9. Projenizi gerekir, DSVM toomeet dinamik ölçeklendirme
Yukarı ve aşağı hello DSVM toomeet, projenin ihtiyaç duyduğu ölçeklendirebilirsiniz. Toouse hello VM hello Akşam veya hafta sonları gerekmiyorsa, yalnızca hello VM hello gelen aşağı kapatabilirsiniz [Azure portal](https://portal.azure.com).

> [!NOTE]
> Merhaba VM üzerinde yalnızca hello işletim sistemi kapatma düğmesini kullanırsanız, bilgi işlem ücretleri.  
> 
> 

Bazı büyük ölçekli analiz toohandle gerekir ve daha fazla CPU ve/veya bellek ve/veya disk kapasitesine ihtiyacınız varsa, VM boyutlarını CPU çekirdekleri, bellek kapasitesi ve (katı hal sürücüleri dahil), bilgi işlem ve bütçe gereksinimlerinize uyan disk türleri açısından büyük seçimine bulabilirsiniz. Merhaba veritabanlarının saatlik işlem fiyatlandırma birlikte tam listesi VM'ler üzerinde hello kullanılabilir [Azure Virtual Machines fiyatlandırması](https://azure.microsoft.com/pricing/details/virtual-machines/) sayfası.

Benzer şekilde, VM işleme kapasitesi, gereksinimini azaltır, (örneğin: önemli iş yükü tooa Hadoop veya bir Spark kümesi taşınmış), hello hello kümeden aşağı ölçeklenebilen [Azure portal](https://portal.azure.com) ve vm'nizin toohello ayarları örneği. Bir ekran görüntüsü aşağıda verilmiştir.

![VM örneği ayarları](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a>10. Ek araçlar sanal makinenize yükleyin
Biz hello ortak veri analizi gereksinimlerini ve, çoğu kaydettiğinizde tooinstall sahip kaçınarak zaman ortamlarınızın tek tek yapılandırmak ve yalnızca kaynaklar için ödeme tarafından paradan tasarruf edebilirsiniz tooaddress olan inanıyoruz çeşitli araçlar paketlenmiş kullanın.

Diğer Azure veri yararlanabilir ve Analiz Hizmetleri bu makale tooenhance analytics ortamınızı profili. Bazı durumlarda, gereksinimlerinize özel bazı üçüncü taraf araçları dahil olmak üzere ek araçlar gerektirebilir anlayın. Gereksinim duyduğunuz hello sanal makine tooinstall yeni araçları tam yönetim erişimi var. Python ve önceden yüklü R ayrıca ek paketleri yükleyebilirsiniz. Python için ya da kullanabilirsiniz ```conda``` veya ```pip```. R için hello kullanabilirsiniz ```install.packages()``` hello R konsol veya hello IDE kullanın ve seçin "**paketleri** -> **yükleme paketleri...** ".

## <a name="summary"></a>Özet
Bunlar, Microsoft Veri bilimi sanal makine hello üzerinde hello yapabileceklerinizden yalnızca bazıları şunlardır. Toomake yapabileceğiniz birçok şey daha vardır, etkili analytics ortam.

