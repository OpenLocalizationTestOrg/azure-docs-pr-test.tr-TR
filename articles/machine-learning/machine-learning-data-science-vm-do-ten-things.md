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
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a><span data-ttu-id="e654c-103">On hello veri bilimi sanal makine üzerinde yapabilecekleriniz</span><span class="sxs-lookup"><span data-stu-id="e654c-103">Ten things you can do on hello Data science Virtual Machine</span></span>
<span data-ttu-id="e654c-104">Hello Microsoft Veri bilimi sanal makine (DSVM), tooperform çeşitli veri keşfi ve modelleme görevleri sağlar güçlü veri bilimi geliştirme ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="e654c-104">hello Microsoft Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you tooperform various data exploration and modeling tasks.</span></span> <span data-ttu-id="e654c-105">Merhaba ortam zaten yerleşik ve beraberinde gelen çeşitli popüler verilerle kolay tooget olun analiz araçları hızlı bir şekilde şirket içi, Bulut veya karma çözümleme dağıtımları kullanmaya.</span><span class="sxs-lookup"><span data-stu-id="e654c-105">hello environment comes already built and bundled with several popular data analytics tools that make it easy tooget started quickly with your analysis for On-premises, Cloud or hybrid deployments.</span></span> <span data-ttu-id="e654c-106">Merhaba DSVM yakından çok sayıda Azure hizmetiyle çalışır ve mümkün tooread ve Azure, Azure SQL Data Warehouse, Azure Data Lake, Azure Storage veya Azure Cosmos veritabanı üzerinde depolanan işlem verileri.</span><span class="sxs-lookup"><span data-stu-id="e654c-106">hello DSVM works closely with many Azure services and is able tooread and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in Azure Cosmos DB.</span></span> <span data-ttu-id="e654c-107">Bunu Azure Machine Learning ve Azure Data Factory gibi diğer analiz araçları da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-107">It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.</span></span>

<span data-ttu-id="e654c-108">Bu makalede biz nasıl yol toouse çeşitli veri bilimi görevler ve diğer Azure hizmetleriyle etkileşime, DSVM tooperform.</span><span class="sxs-lookup"><span data-stu-id="e654c-108">In this article we walk you through how toouse your DSVM tooperform various data science tasks and interact with other Azure services.</span></span> <span data-ttu-id="e654c-109">Merhaba DSVM üzerinde yapabileceğiniz hello şeylerden bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e654c-109">Here are some of hello things you can do on hello DSVM:</span></span>

1. <span data-ttu-id="e654c-110">Verileri araştırırken hello DSVM Microsoft R Server, Python kullanarak yerel olarak modellerinde geliştirin</span><span class="sxs-lookup"><span data-stu-id="e654c-110">Explore data and develop models locally on hello DSVM using Microsoft R Server, Python</span></span>
2. <span data-ttu-id="e654c-111">Verilerinizi Python 2, Python 3, Microsoft R R ölçeklenebilirlik ve performans için tasarlanmış bir kurumsal hazır sürümünü kullanarak bir tarayıcı ile Jupyter not defteri tooexperiment kullanma</span><span class="sxs-lookup"><span data-stu-id="e654c-111">Use a Jupyter notebook tooexperiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for scalability and performance</span></span>
3. <span data-ttu-id="e654c-112">İstemci uygulamaları basit web Hizmetleri arabirimi kullanarak Modellerinizi erişebilmesi için R ve Python Azure Machine Learning kullanılarak oluşturulan modelleri faaliyete</span><span class="sxs-lookup"><span data-stu-id="e654c-112">Operationalize models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web services interface</span></span>
4. <span data-ttu-id="e654c-113">Azure portal veya Powershell kullanarak Azure kaynaklarınızı yönetmek</span><span class="sxs-lookup"><span data-stu-id="e654c-113">Administer your Azure resources using  Azure portal or Powershell</span></span>
5. <span data-ttu-id="e654c-114">Depolama alanını genişletmek ve büyük ölçekli veri kümeleri paylaşmak /, DSVM takılabilir bir sürücüde olarak Azure File storage oluşturarak tüm ekibinizin arasında kod</span><span class="sxs-lookup"><span data-stu-id="e654c-114">Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File storage as a mountable drive on your DSVM</span></span>
6. <span data-ttu-id="e654c-115">Kod GitHub kullanarak takımınızla paylaşmak ve deponuz hello önceden yüklenmiş Git istemciler - Git Bash Git GUI kullanarak erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-115">Share code with your team using GitHub and access your repository using hello pre-installed Git clients - Git Bash, Git GUI.</span></span>
7. <span data-ttu-id="e654c-116">Çeşitli Azure veri ve Analiz Hizmetleri Azure blob depolama gibi Azure Data Lake, Azure Hdınsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & veritabanları erişim</span><span class="sxs-lookup"><span data-stu-id="e654c-116">Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & databases</span></span>
8. <span data-ttu-id="e654c-117">Raporları ve panoyu Power BI Desktop DSVM hello üzerinde önceden yüklenmiş hello kullanarak oluşturmak ve bunları hello bulut üzerinde dağıtmak</span><span class="sxs-lookup"><span data-stu-id="e654c-117">Build reports and dashboard using hello Power BI Desktop pre-installed on hello DSVM and deploy them on hello cloud</span></span>
9. <span data-ttu-id="e654c-118">Projenizi gerekir, DSVM toomeet dinamik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="e654c-118">Dynamically scale your DSVM toomeet your project needs</span></span>
10. <span data-ttu-id="e654c-119">Ek araçlar sanal makinenize yükleyin</span><span class="sxs-lookup"><span data-stu-id="e654c-119">Install additional tools on your virtual machine</span></span>   

> [!NOTE]
> <span data-ttu-id="e654c-120">Bu makalede listelenen hello ek veri depolama ve Analiz Hizmetleri birçoğu için ek kullanım ücretleri uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e654c-120">Additional usage charges apply for many of hello additional data storage and analytics services listed in this article.</span></span> <span data-ttu-id="e654c-121">Lütfen toohello bakın [Azure fiyatlandırma](https://azure.microsoft.com/pricing/) Ayrıntılar için sayfa.</span><span class="sxs-lookup"><span data-stu-id="e654c-121">Please refer toohello [Azure Pricing](https://azure.microsoft.com/pricing/) page for details.</span></span>
> 
> 

<span data-ttu-id="e654c-122">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="e654c-122">**Prerequisites**</span></span>

* <span data-ttu-id="e654c-123">Bir Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="e654c-123">You need an Azure subscription.</span></span> <span data-ttu-id="e654c-124">Ücretsiz deneme için kaydolabilirsiniz [burada](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e654c-124">You can sign up for a free trial [here](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="e654c-125">Hello Azure portalı üzerinde veri bilimi sanal makinenin sağlanması için yönergeler [bir sanal makine oluşturma](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="e654c-125">Instructions for provisioning a Data Science Virtual Machine on hello Azure portal are available at [Creating a virtual machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span></span>

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a><span data-ttu-id="e654c-126">1. Verileri araştırmak ve modeller Microsoft R Server veya Python kullanarak geliştirme</span><span class="sxs-lookup"><span data-stu-id="e654c-126">1. Explore data and develop models using Microsoft R Server or Python</span></span>
<span data-ttu-id="e654c-127">Merhaba üzerinde sağ DSVM veri analizi, R ve Python toodo gibi diller kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-127">You can use languages like R and Python toodo your data analytics right on hello DSVM.</span></span>

<span data-ttu-id="e654c-128">R için hello Başlat menüsünden veya hello Masaüstü bulunabilir "Revolution R Kurumsal 8.0" adlı bir IDE kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-128">For R, you can use an IDE called "Revolution R Enterprise 8.0" that can be found on hello start menu or hello desktop.</span></span> <span data-ttu-id="e654c-129">Microsoft, ek kitaplıklara hello açık kaynak/CRAN-R tooenable ölçeklenebilir analizi ve hello özelliği tooanalyze verileri paralel öbekli analiz yaparak izin hello bellek boyutundan büyük üstünde sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="e654c-129">Microsoft has provided additional libraries on top of hello Open source/CRAN-R tooenable scalable analytics and hello ability tooanalyze data larger than hello memory size allowed by doing parallel chunked analysis.</span></span> <span data-ttu-id="e654c-130">Choice benzer, R IDE de yükleyebilirsiniz [Rstudio'dan](https://www.rstudio.com/products/rstudio-desktop/).</span><span class="sxs-lookup"><span data-stu-id="e654c-130">You can also install an R IDE of your choice like [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span></span>

<span data-ttu-id="e654c-131">Python için Visual Studio Community hello Python araçları Visual Studio (PTVS) uzantısı önceden yüklenmiş olan sürümü gibi bir IDE kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-131">For Python, you can use an IDE like Visual Studio Community Edition which has hello Python Tools for Visual Studio (PTVS) extension pre-installed.</span></span> <span data-ttu-id="e654c-132">Varsayılan olarak, yalnızca temel bir Python 2.7 (olmadan herhangi bir analiz kitaplığı SciKit, Pandas gibi) üzerinde PTVS yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e654c-132">By default, only a basic Python 2.7 is configured on PTVS (without any analytics library like SciKit, Pandas).</span></span> <span data-ttu-id="e654c-133">Sipariş tooenable Anaconda Python 2.7 ve 3.5 toodo hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="e654c-133">In order tooenable Anaconda Python 2.7 and 3.5, you need toodo hello following:</span></span>

* <span data-ttu-id="e654c-134">Çok giderek her sürüm için özel ortamları oluşturma**Araçları** -> **Python Araçları** -> **Python ortamları** ve ardından " **+ Özel**"içinde hello Visual Studio 2015 Community Edition</span><span class="sxs-lookup"><span data-stu-id="e654c-134">Create custom environments for each version by navigating too**Tools** -> **Python Tools** -> **Python Environments** and then clicking "**+ Custom**" in hello Visual Studio 2015 Community Edition</span></span>
* <span data-ttu-id="e654c-135">Bir açıklama girin ve önek yolları olarak hello ortamını ayarlama *c:\anaconda* Anaconda Python 2.7 veya *c:\anaconda\envs\py35* Anaconda Python 3.5 için</span><span class="sxs-lookup"><span data-stu-id="e654c-135">Give a description and set hello environment prefix paths as *c:\anaconda* for Anaconda Python 2.7 OR *c:\anaconda\envs\py35* for Anaconda Python 3.5</span></span>
* <span data-ttu-id="e654c-136">Tıklatın **otomatik algıla** ve ardından **Uygula** toosave hello ortamı.</span><span class="sxs-lookup"><span data-stu-id="e654c-136">Click **Auto Detect** and then **Apply** toosave hello environment.</span></span>

<span data-ttu-id="e654c-137">Visual Studio gibi görünüyor hangi hello özel ortam ayarlarının aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e654c-137">Here is what hello custom environment setup looks like in Visual Studio.</span></span>

![PTVS Kurulumu](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

<span data-ttu-id="e654c-139">Merhaba bkz [PTVS belgelerine](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) hakkında ek ayrıntılar için toocreate Python ortamları.</span><span class="sxs-lookup"><span data-stu-id="e654c-139">See hello [PTVS documentation](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) for additional details on how toocreate Python Environments.</span></span>

<span data-ttu-id="e654c-140">Şimdi yeni bir Python proje toocreate ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="e654c-140">Now you are set up toocreate a new Python project.</span></span> <span data-ttu-id="e654c-141">Çok gidin**dosya** -> **yeni** -> **proje** -> **Python** ve hello türünü seçin Oluşturmakta olduğunuz Python uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e654c-141">Navigate too**File** -> **New** -> **Project** -> **Python** and select hello type of Python application you are building.</span></span> <span data-ttu-id="e654c-142">Merhaba Python ortamı hello geçerli proje toohello istenen sürüm (Anaconda 2.7 ya da 3.5) için ayarlayabilirsiniz: sağ hello **Python ortamı**seçin **Ekle/Kaldır Python ortamları**, ve sonra Seç hello ortamı tooassociate hello proje ile istenen.</span><span class="sxs-lookup"><span data-stu-id="e654c-142">You can set hello Python environment for hello current project toohello desired version (Anaconda 2.7 or 3.5): right-click hello **Python environment**, select **Add/Remove Python Environments**, and then select hello desired environment tooassociate with hello project.</span></span> <span data-ttu-id="e654c-143">Merhaba ürün PTVS ile çalışma hakkında daha fazla bilgi bulabilirsiniz [belgelerine](https://github.com/Microsoft/PTVS/wiki) sayfası.</span><span class="sxs-lookup"><span data-stu-id="e654c-143">You can find more information about working with PTVS on hello product [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span></span>

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a><span data-ttu-id="e654c-144">2. Bir Jupyter not defteri tooexplore ve model verilerinizi Python veya R ile kullanma</span><span class="sxs-lookup"><span data-stu-id="e654c-144">2. Using a Jupyter Notebook tooexplore and model your data with Python or R</span></span>
<span data-ttu-id="e654c-145">Merhaba Jupyter not defteri veri keşfi ve modelleme için bir tarayıcı tabanlı "IDE" sağlayan güçlü bir ortamdır.</span><span class="sxs-lookup"><span data-stu-id="e654c-145">hello Jupyter Notebook is a powerful environment that provides a browser-based "IDE" for data exploration and modeling.</span></span> <span data-ttu-id="e654c-146">Python 2, Python 3 ya da R (açık kaynaklı ve hello Microsoft R Server) bir Jupyter not defteri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-146">You can use Python 2, Python 3 or R (both Open Source and hello Microsoft R Server) in a Jupyter Notebook.</span></span>

<span data-ttu-id="e654c-147">toolaunch hello Jupyter not defteri hello Başlat menüsü simgesini tıklatın / Masaüstü simgesi başlıklı **Jupyter not defteri**.</span><span class="sxs-lookup"><span data-stu-id="e654c-147">toolaunch hello Jupyter Notebook click on hello start menu icon / desktop icon titled **Jupyter Notebook**.</span></span> <span data-ttu-id="e654c-148">Merhaba DSVM üzerinde de çok göz atabilirsiniz "https://localhost:9999 /" tooaccess hello Jüpiter dizüstü bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="e654c-148">On hello DSVM you can also browse too"https://localhost:9999/" tooaccess hello Jupiter Notebook.</span></span> <span data-ttu-id="e654c-149">İçin bir parola ister, hello sunulan yönergeleri kullanın. ***nasıl toocreate hello Jupyter not defteri sunucuda güçlü bir parola*** hello bölümünü [sağlama hello Microsoft Veri bilimi sanal makine](machine-learning-data-science-provision-vm.md)konu toocreate güçlü parola tooaccess hello Jupyter not defteri.</span><span class="sxs-lookup"><span data-stu-id="e654c-149">If it prompts you for a password, use instructions provided in hello ***How toocreate a strong password on hello Jupyter notebook server*** section of hello [Provision hello Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) topic toocreate a strong password tooaccess hello Jupyter notebook.</span></span> 

<span data-ttu-id="e654c-150">Merhaba dizüstü açtıktan sonra DSVM hello önceden paketlenmiş birkaç örnek dizüstü bilgisayarlar içeren bir dizini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e654c-150">Once you have opened hello notebook, you should see a directory that contains a few example notebooks that are pre-packaged into hello DSVM.</span></span> <span data-ttu-id="e654c-151">Artık şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e654c-151">Now you can:</span></span>

* <span data-ttu-id="e654c-152">Merhaba not defteri toosee hello kodu tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e654c-152">click on hello notebook toosee hello code.</span></span>
* <span data-ttu-id="e654c-153">Her bir hücre tuşlarına basarak yürütme **SHIFT-ENTER**.</span><span class="sxs-lookup"><span data-stu-id="e654c-153">execute each cell by pressing **SHIFT-ENTER**.</span></span>
* <span data-ttu-id="e654c-154">Merhaba tüm not tıklayarak çalıştırın **hücre** -> **çalıştırın**</span><span class="sxs-lookup"><span data-stu-id="e654c-154">run hello entire notebook by clicking on **Cell** -> **Run**</span></span>
* <span data-ttu-id="e654c-155">Merhaba Jupyter simgesi (sol üst köşesinde) üzerinde tıklattıktan sonra tıklatarak yeni bir not defteri oluşturma **yeni** hello sağ ve hello not defteri dili (tekrar olarak da bilinir) seçme düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e654c-155">create a new notebook by clicking on hello Jupyter Icon (left top corner) and then clicking **New** button on hello right and then choosing hello notebook language (also known as kernels).</span></span>   

> [!NOTE]
> <span data-ttu-id="e654c-156">Şu anda Python 2.7 destekliyoruz, Python 3.5 ve r hello R çekirdek hem açık kaynak R yanı sıra hello Kurumsal programlama destekleyen ölçeklenebilir Microsoft R Server.</span><span class="sxs-lookup"><span data-stu-id="e654c-156">Currently we support Python 2.7, Python 3.5 and R. hello R kernel supports programming in both Open source R as well as hello enterprise scalable Microsoft R Server.</span></span>   
> 
> 

<span data-ttu-id="e654c-157">Hello not defterinde olduktan sonra verilerinizi keşfedin, hello model oluşturma, test seçiminizi kitaplıklarını kullanarak hello modeli.</span><span class="sxs-lookup"><span data-stu-id="e654c-157">Once you are in hello notebook you can explore your data, build hello model, test hello model using your choice of libraries.</span></span>

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a><span data-ttu-id="e654c-158">3. R veya Python ve Operationalize Azure Machine Learning kullanarak bunları kullanarak modelleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="e654c-158">3. Build models using R or Python and Operationalize them using Azure Machine Learning</span></span>
<span data-ttu-id="e654c-159">Yerleşik ve doğrulandı sonra model hello sonraki adımınız genellikle toodeploy olan üretim içine.</span><span class="sxs-lookup"><span data-stu-id="e654c-159">Once you have built and validated your model hello next step is usually toodeploy it into production.</span></span> <span data-ttu-id="e654c-160">Bu istemci uygulamaları tooinvoke hello modeli tahminlerin gerçek zamanlı veya toplu iş modu temelinde sağlar.</span><span class="sxs-lookup"><span data-stu-id="e654c-160">This allows your client applications tooinvoke hello model predictions on a real time or on a batch mode basis.</span></span> <span data-ttu-id="e654c-161">Azure Machine Learning mekanizması toooperationalize R veya Python ile oluşturulmuş bir model sağlar.</span><span class="sxs-lookup"><span data-stu-id="e654c-161">Azure Machine Learning provides a mechanism toooperationalize a model built in either R or Python.</span></span>

<span data-ttu-id="e654c-162">Azure Machine Learning modelinizde faaliyete olduğunda, bir web hizmeti giriş parametreleri geçirin ve çıktı hello modelden Öngörüler almak toomake REST çağrılarını istemcilerinin veren açıktır.</span><span class="sxs-lookup"><span data-stu-id="e654c-162">When you operationalize your model in Azure Machine Learning, a web service is exposed that allows clients toomake REST calls that pass in input parameters and receive predictions from hello model as outputs.</span></span>   

> [!NOTE]
> <span data-ttu-id="e654c-163">Henüz Azure Machine Learning için kaydolmadıysanız, boş bir çalışma alanında ya da standart çalışma hello ziyaret ederek edinebilirsiniz [Azure Machine Learning Studio](https://studio.azureml.net/) giriş sayfası ve tıklayarak üzerinde "Get Started".</span><span class="sxs-lookup"><span data-stu-id="e654c-163">If you have not yet signed up for Azure Machine Learning, you can obtain a free workspace or a standard workspace by visiting hello [Azure Machine Learning Studio](https://studio.azureml.net/) home page and clicking on "Get Started".</span></span>   
> 
> 

### <a name="build-and-operationalize-python-models"></a><span data-ttu-id="e654c-164">Derleme ve Python faaliyete modelleri</span><span class="sxs-lookup"><span data-stu-id="e654c-164">Build and Operationalize Python models</span></span>
<span data-ttu-id="e654c-165">Merhaba SciKit öğrenin kitaplığını kullanarak basit bir model oluşturur bir Python Jupyter not defterinde geliştirilmiş kod parçacığı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e654c-165">Here is a snippet of code developed in a Python Jupyter Notebook that builds a simple model using hello SciKit-learn library.</span></span>

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

<span data-ttu-id="e654c-166">Merhaba yöntemi toodeploy python modelleri tooAzure Itanium tabanlı sistemler için Machine Learning sarmalayan hello tahmin hello modelinin bir işlevi olarak kullanılan ve Azure makineniz belirtmek hello önceden yüklenmiş Azure Machine Learning python kitaplığı tarafından sağlanan özniteliklerle süsler Learning çalışma alanı kimliği, API anahtarı ve hello giriş ile dönüş parametreleri.</span><span class="sxs-lookup"><span data-stu-id="e654c-166">hello method used toodeploy your python models tooAzure Machine Learning wraps hello prediction of hello model into a function and decorates it with attributes provided by hello pre-installed Azure Machine Learning python library that denote your Azure Machine Learning workspace ID, API Key, and hello input and return parameters.</span></span>  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

<span data-ttu-id="e654c-167">Bir istemci çağrılarını toohello web hizmeti şimdi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-167">A client can now make calls toohello web service.</span></span> <span data-ttu-id="e654c-168">Merhaba REST API istekleri oluşturmak kolaylık sarmalayıcıları vardır.</span><span class="sxs-lookup"><span data-stu-id="e654c-168">There are convenience wrappers that construct hello REST API requests.</span></span> <span data-ttu-id="e654c-169">Bir örnek kod tooconsume hello web hizmeti aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e654c-169">Here is a sample code tooconsume hello web service.</span></span>

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> <span data-ttu-id="e654c-170">şu anda üretim Hello Azure Machine Learning kitaplığı yalnızca Python 2.7 üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e654c-170">hello Azure Machine Learning library is only supported on Python 2.7 currently.</span></span>   
> 
> 

### <a name="build-and-operationalize-r-models"></a><span data-ttu-id="e654c-171">Derleme ve faaliyete R modelleri</span><span class="sxs-lookup"><span data-stu-id="e654c-171">Build and Operationalize R models</span></span>
<span data-ttu-id="e654c-172">Python için yapılan benzer toohow olan bir şekilde hello veri bilimi sanal makine veya başka bir Azure Machine Learning üzerine yerleşik R modelleri dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-172">You can deploy R models built on hello Data Science Virtual Machine or elsewhere onto Azure Machine Learning in a manner that is similar toohow it is done for Python.</span></span> <span data-ttu-id="e654c-173">Kendi hello adımlardır:</span><span class="sxs-lookup"><span data-stu-id="e654c-173">Her are hello steps:</span></span>

* <span data-ttu-id="e654c-174">Çalışma alanı kimliği ve kimlik doğrulama kodu örneği aşağıdaki hello gösterildiği gibi simge settings.json dosya tooprovide oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e654c-174">create a settings.json file tooprovide your workspace ID and auth token as shown in hello following code sample.</span></span>
* <span data-ttu-id="e654c-175">Merhaba modelinin işlevi tahmin etmek için bir sarmalayıcı yazma.</span><span class="sxs-lookup"><span data-stu-id="e654c-175">write a wrapper for hello model's predict function.</span></span>
* <span data-ttu-id="e654c-176">çağrı ```publishWebService``` hello Azure Machine Learning kitaplığı toopass hello işlevi sarmalayıcı içinde içinde.</span><span class="sxs-lookup"><span data-stu-id="e654c-176">call ```publishWebService``` in hello Azure Machine Learning library toopass in hello function wrapper.</span></span>  

<span data-ttu-id="e654c-177">Burada, kullanılan tooset yukarı, yapı, yayımlama, ve bir Azure Machine Learning web hizmeti olarak modeli tüketen hello yordam ve kod parçacıkları verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e654c-177">Here is hello procedure and code snippets that can be used tooset up, build, publish, and consume a model as a web service in Azure Machine Learning.</span></span>

#### <a name="setup"></a><span data-ttu-id="e654c-178">Kurulum</span><span class="sxs-lookup"><span data-stu-id="e654c-178">Setup</span></span>
1. <span data-ttu-id="e654c-179">Yazarak Hello Machine Learning R paketini Yükle ```install.packages("AzureML")``` Revolution R Kurumsal 8.0 IDE veya R IDE.</span><span class="sxs-lookup"><span data-stu-id="e654c-179">Install hello Machine Learning R package by typing ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE or your R IDE.</span></span>
2. <span data-ttu-id="e654c-180">Gelen RTools karşıdan [burada](https://cran.r-project.org/bin/windows/Rtools/).</span><span class="sxs-lookup"><span data-stu-id="e654c-180">Download RTools from [here](https://cran.r-project.org/bin/windows/Rtools/).</span></span> <span data-ttu-id="e654c-181">Machine Learning R paketi hello zip hello yol (ve adlandırılmış zip.exe) yardımcı programı toooperationalize gerekir.</span><span class="sxs-lookup"><span data-stu-id="e654c-181">You need hello zip utility in hello path (and named zip.exe) toooperationalize your R package into Machine Learning.</span></span>
3. <span data-ttu-id="e654c-182">Adlı bir dizin altında settings.json dosyası oluşturma ```.azureml``` giriş dizininize altında ve Azure Machine Learning alanınızdan hello parametreleri girin:</span><span class="sxs-lookup"><span data-stu-id="e654c-182">Create a settings.json file under a directory called ```.azureml``` under your home directory and enter hello parameters from your Azure Machine Learning workspace:</span></span>

<span data-ttu-id="e654c-183">Settings.JSON dosya yapısı:</span><span class="sxs-lookup"><span data-stu-id="e654c-183">settings.json File structure:</span></span>

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a><span data-ttu-id="e654c-184">R bir model oluşturmak ve Azure Machine Learning ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="e654c-184">Build a model in R and publish it in Azure Machine Learning</span></span>
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

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a><span data-ttu-id="e654c-185">Azure Machine Learning ile dağıtılan hello model kullanma</span><span class="sxs-lookup"><span data-stu-id="e654c-185">Consume hello model deployed in Azure Machine Learning</span></span>
<span data-ttu-id="e654c-186">bir istemci uygulamasından tooconsume hello model, kullandığımız hello Azure Machine Learning kitaplığı toolook hello yukarı web hizmeti hello kullanarak adı tarafından yayımlanan `services` API çağrısı toodetermine hello uç noktası.</span><span class="sxs-lookup"><span data-stu-id="e654c-186">tooconsume hello model from a client application, we use hello Azure Machine Learning library toolook up hello published web service by name using hello `services` API call toodetermine hello endpoint.</span></span> <span data-ttu-id="e654c-187">Yalnızca hello çağrı sonra `consume` işlev ve hello veri çerçeve toobe tahmin içinde geçirin.</span><span class="sxs-lookup"><span data-stu-id="e654c-187">Then you just call hello `consume` function and pass in hello data frame toobe predicted.</span></span>
<span data-ttu-id="e654c-188">koddan hello bir Azure Machine Learning web hizmeti olarak yayımlanan kullanılan tooconsume hello modelidir.</span><span class="sxs-lookup"><span data-stu-id="e654c-188">hello following code is used tooconsume hello model published as an Azure Machine Learning web service.</span></span>

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

<span data-ttu-id="e654c-189">Hello Azure Machine Learning R Kitaplığı hakkında daha fazla bilgi bulunabilir [burada](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span><span class="sxs-lookup"><span data-stu-id="e654c-189">More information about hello Azure Machine Learning R library can be found [here](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span></span>

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a><span data-ttu-id="e654c-190">4. Azure portal veya Powershell kullanarak Azure kaynaklarınızı yönetmek</span><span class="sxs-lookup"><span data-stu-id="e654c-190">4. Administer your Azure resources using Azure portal or Powershell</span></span>
<span data-ttu-id="e654c-191">Merhaba DSVM yalnızca verir toobuild analytics çözümünüzü yerel olarak hello sanal makine, ancak Microsoft Azure bulut üzerinde tooaccess hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e654c-191">hello DSVM not only allows you toobuild your analytics solution locally on hello virtual machine, but also allows you tooaccess services on Microsoft's Azure cloud.</span></span> <span data-ttu-id="e654c-192">Azure birkaç işlem, depolama, veri analizi Hizmetleri ve yönetmek ve sizin DSVM erişim diğer hizmetler sağlar.</span><span class="sxs-lookup"><span data-stu-id="e654c-192">Azure provides several compute, storage, data analytics services and other services that you can administer and access from your DSVM.</span></span>

<span data-ttu-id="e654c-193">tooadminister tarayıcı ve noktası toothe kullanabilirsiniz, Azure aboneliği ve bulut kaynaklarınızı [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e654c-193">tooadminister your Azure subscription and cloud resources you can use your browser and point toothe [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e654c-194">Azure Powershell tooadminister de, Azure aboneliği ve kaynakların bir komut dosyası aracılığıyla da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-194">You can also use Azure Powershell tooadminister your Azure subscription and resources via a script.</span></span>
<span data-ttu-id="e654c-195">Azure Powershell hello masaüstünde bir kısayoldan çalıştırmak veya hello Başlat menüsü "Microsoft Azure Powershell" başlıklı.</span><span class="sxs-lookup"><span data-stu-id="e654c-195">You can run Azure Powershell from a shortcut on hello desktop or from hello start menu titled "Microsoft Azure Powershell".</span></span> <span data-ttu-id="e654c-196">Başvurmak [Microsoft Azure Powershell belgelerine](../powershell-azure-resource-manager.md) Azure aboneliği ve Windows Powershell betiklerini kullanarak kaynakları nasıl yönetebileceğiniz hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="e654c-196">Refer to [Microsoft Azure Powershell documentation](../powershell-azure-resource-manager.md) for more information on how you can administer your Azure subscription and resources using Windows Powershell scripts.</span></span>

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a><span data-ttu-id="e654c-197">5. Depolama alanınızı paylaşılan dosya sistemiyle genişletme</span><span class="sxs-lookup"><span data-stu-id="e654c-197">5. Extend your storage space with a shared file system</span></span>
<span data-ttu-id="e654c-198">Veri bilimcilerine büyük veri kümeleri, kod veya başka kaynaklara hello takım içindeki paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-198">Data scientists can share large datasets, code or other resources within hello team.</span></span> <span data-ttu-id="e654c-199">Merhaba DSVM kendisini yaklaşık 70 GB alanınız vardır.</span><span class="sxs-lookup"><span data-stu-id="e654c-199">hello DSVM itself has about 70GB of space available.</span></span> <span data-ttu-id="e654c-200">tooextend depolama alanınızın kullandığınız hello Azure dosya hizmeti ve DSVM hello üzerinde bağlayın veya bir REST API üzerinden erişim.</span><span class="sxs-lookup"><span data-stu-id="e654c-200">tooextend your storage, you can use hello Azure File Service and either mount it on hello DSVM or access it via a REST API.</span></span>   

> [!NOTE]
> <span data-ttu-id="e654c-201">Merhaba maksimum alan hello Azure dosya hizmeti paylaşımının 5 TB ve tek tek dosya boyutu sınırı 1 TB.</span><span class="sxs-lookup"><span data-stu-id="e654c-201">hello maximum space of hello Azure File Service share is 5TB and individual file size limit is 1TB.</span></span>   
> 
> 

<span data-ttu-id="e654c-202">Azure Powershell toocreate bir Azure dosya hizmeti paylaşımı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-202">You can use Azure Powershell toocreate an Azure File Service share.</span></span> <span data-ttu-id="e654c-203">Burada, Azure PowerShell toocreate bir Azure dosya hizmeti paylaşımı altında hello betik toorun verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e654c-203">Here is hello script toorun under Azure PowerShell toocreate an Azure File service share.</span></span>

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


<span data-ttu-id="e654c-204">Azure dosya paylaşımının oluşturduğunuza göre herhangi bir sanal makine azure'da bağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="e654c-204">Now that you have created an Azure file share, you can mount it in any virtual machine in Azure.</span></span> <span data-ttu-id="e654c-205">Bu hello VM aynı Azure veri merkezi olarak hello depolama hesabı tooavoid gecikmesi ve veri aktarımı ücretlerine olan önerilir.</span><span class="sxs-lookup"><span data-stu-id="e654c-205">It is highly recommended that hello VM is in same Azure data center as hello storage account tooavoid latency and data transfer charges.</span></span> <span data-ttu-id="e654c-206">Merhaba, Azure Powershell çalıştırabilirsiniz DSVM hello komutları toomount hello sürücü şunlardır.</span><span class="sxs-lookup"><span data-stu-id="e654c-206">Here are hello commands toomount hello drive on hello DSVM that you can run on Azure Powershell.</span></span>

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


<span data-ttu-id="e654c-207">Artık herhangi normal bir sürücüye hello VM üzerinde yaptığınız gibi bu sürücüyü erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-207">Now you can access this drive as you would any normal drive on hello VM.</span></span>

## <a name="6-share-code-with-your-team-using-github"></a><span data-ttu-id="e654c-208">6. Kod GitHub kullanarak takımınızla paylaşmak</span><span class="sxs-lookup"><span data-stu-id="e654c-208">6. Share code with your team using GitHub</span></span>
<span data-ttu-id="e654c-209">GitHub hello Geliştirici topluluğu tarafından paylaşılan çeşitli teknolojiler kullanılarak farklı araçlar için örnek kod ve kaynakları çok bulabileceğiniz bir kod depodur.</span><span class="sxs-lookup"><span data-stu-id="e654c-209">GitHub is a code repository where you can find a lot of sample code and sources for different tools using various technologies shared by hello developer community.</span></span> <span data-ttu-id="e654c-210">Teknoloji tootrack ve Deposu sürümleri hello kod dosyaları hello gibi Git kullanır.</span><span class="sxs-lookup"><span data-stu-id="e654c-210">It uses Git as hello technology tootrack and store versions of hello code files.</span></span> <span data-ttu-id="e654c-211">GitHub, ayrıca bir platformdur kendi depo toostore ekibinizin paylaşılan kodu ve belgeler, oluşturabileceğiniz sürüm denetimi ve aynı zamanda Denetim erişim tooview olan ve kod katkıda uygular.</span><span class="sxs-lookup"><span data-stu-id="e654c-211">GitHub is also a platform where you can create your own repository toostore your team's shared code and documentation, implement version control and also control who have access tooview and contribute code.</span></span> <span data-ttu-id="e654c-212">Lütfen başlangıç adresini ziyaret edin [GitHub yardım sayfalarına](https://help.github.com/) Git kullanma hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e654c-212">Please visit hello [GitHub help pages](https://help.github.com/) for more information on using Git.</span></span> <span data-ttu-id="e654c-213">GitHub hello yolları toocollaborate biri olarak ekibinizle kullanın, hello topluluk tarafından geliştirilmiş kodu kullanın ve kod geri toohello topluluğa katkıda.</span><span class="sxs-lookup"><span data-stu-id="e654c-213">You can use GitHub as one of hello ways toocollaborate with your team, use code developed by hello community and contribute code back toohello community.</span></span>

<span data-ttu-id="e654c-214">Merhaba DSVM zaten iyi GUI tooaccess GitHub deposunu komut satırı hem istemci araçları ile yüklenen gelir.</span><span class="sxs-lookup"><span data-stu-id="e654c-214">hello DSVM already comes loaded with client tools on both command-line as well GUI tooaccess GitHub repository.</span></span> <span data-ttu-id="e654c-215">Git ve GitHub ile Merhaba komut satırı aracı toowork Git Bash adı verilir.</span><span class="sxs-lookup"><span data-stu-id="e654c-215">hello command-line tool toowork with Git and GitHub is called Git Bash.</span></span> <span data-ttu-id="e654c-216">Merhaba DSVM üzerinde yüklü visual Studio hello Git uzantısına sahip.</span><span class="sxs-lookup"><span data-stu-id="e654c-216">Visual Studio installed on hello DSVM has hello Git extensions.</span></span> <span data-ttu-id="e654c-217">Bu araçları hello Başlat menüsü ve hello Masaüstü için başlangıç simge bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-217">You can find start-up icons for these tools on hello start menu and hello desktop.</span></span>

<span data-ttu-id="e654c-218">toodownload kodu Github'da depodan hello kullan ```git clone``` komutu.</span><span class="sxs-lookup"><span data-stu-id="e654c-218">toodownload code from a GitHub repository you use hello ```git clone``` command.</span></span> <span data-ttu-id="e654c-219">Örneğin hello geçerli dizine Microsoft tarafından yayımlanan toodownload veri bilimi havuzu hello içinde olduktan sonra aşağıdaki komutu çalıştırabilirsiniz ```git-bash```.</span><span class="sxs-lookup"><span data-stu-id="e654c-219">For example toodownload data science repository published by Microsoft into hello current directory you can run hello following command once you are in ```git-bash```.</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="e654c-220">Visual Studio'da bunu hello aynı kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="e654c-220">In Visual Studio, you can do hello same clone operation.</span></span> <span data-ttu-id="e654c-221">Aşağıdaki ekran görüntüsünde hello nasıl tooaccess Git ve GitHub Visual Studio Araçları gösterir.</span><span class="sxs-lookup"><span data-stu-id="e654c-221">hello  following screen-shot shows how tooaccess Git and GitHub tools in Visual Studio.</span></span>

![Visual Studio'da Git](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

<span data-ttu-id="e654c-223">Git toowork GitHub deponuz github.com'u üzerinde kullanılabilir çeşitli kaynaklardan ile kullanma hakkında daha fazla bilgi bulabilirsiniz. Merhaba [kopya sayfası](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) yararlı bir başvurudur.</span><span class="sxs-lookup"><span data-stu-id="e654c-223">You can find more information on using Git toowork with your GitHub repository from several resources available on github.com. hello [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is a useful reference.</span></span>

## <a name="7-access-various-azure-data-and-analytics-services"></a><span data-ttu-id="e654c-224">7. Çeşitli Azure verileri ve çözümlemeler hizmetlere erişme</span><span class="sxs-lookup"><span data-stu-id="e654c-224">7. Access various Azure data and analytics services</span></span>
### <a name="azure-blob"></a><span data-ttu-id="e654c-225">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="e654c-225">Azure Blob</span></span>
<span data-ttu-id="e654c-226">Azure blob verileri büyük ve küçük için güvenilir ve ekonomik bulut Depolama ' dir.</span><span class="sxs-lookup"><span data-stu-id="e654c-226">Azure blob is a reliable, economical cloud storage for data big and small.</span></span> <span data-ttu-id="e654c-227">Bize nasıl veri tooAzure Blob ve bir Azure Blob depolanan verilere erişmek taşıyabilir adresindeki arayın.</span><span class="sxs-lookup"><span data-stu-id="e654c-227">Let us look at how you can move data tooAzure Blob and access data stored in an Azure Blob.</span></span>

<span data-ttu-id="e654c-228">**Önkoşul**</span><span class="sxs-lookup"><span data-stu-id="e654c-228">**Prerequisite**</span></span>

* <span data-ttu-id="e654c-229">**Azure Blob storage hesabınızdan oluşturma [Azure portal](https://portal.azure.com).**</span><span class="sxs-lookup"><span data-stu-id="e654c-229">**Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).**</span></span>

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="e654c-231">Bu hello önceden yüklenmiş komut satırı AzCopy aracı adresindeki bulunduğunda onaylayın ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span><span class="sxs-lookup"><span data-stu-id="e654c-231">Confirm that hello pre-installed command-line AzCopy tool is found at ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span></span> <span data-ttu-id="e654c-232">Bu aracı çalıştırırken hello dizin içeren hello azcopy.exe tooyour yol ortam değişkeni tooavoid yazarak hello tam komut yolu ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-232">You can add hello directory containing hello azcopy.exe tooyour PATH environment variable tooavoid typing hello full command path when running this tool.</span></span> <span data-ttu-id="e654c-233">AzCopy aracı hakkında daha fazla bilgi için lütfen çok başvurun[AzCopy belgeleri](../storage/common/storage-use-azcopy.md)</span><span class="sxs-lookup"><span data-stu-id="e654c-233">For more info on AzCopy tool please refer too[AzCopy documentation](../storage/common/storage-use-azcopy.md)</span></span>
* <span data-ttu-id="e654c-234">Hello Azure Storage Gezgini aracını başlatın.</span><span class="sxs-lookup"><span data-stu-id="e654c-234">Start hello Azure Storage Explorer tool.</span></span> <span data-ttu-id="e654c-235">Adresten yüklenebilir [Microsoft Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e654c-235">It can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

<span data-ttu-id="e654c-237">**VM tooAzure Blob ' veri taşıma: AzCopy**</span><span class="sxs-lookup"><span data-stu-id="e654c-237">**Move data from VM tooAzure Blob: AzCopy**</span></span>

<span data-ttu-id="e654c-238">blob depolama ve yerel dosyalarınızı arasında toomove verileri, kullanabileceğiniz AzCopy komut satırında veya PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e654c-238">toomove data between your local files and blob storage, you can use AzCopy in command-line or PowerShell:</span></span>

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

<span data-ttu-id="e654c-239">Değiştir **C:\myfolder** dosyanızı depolandığı toohello yolu **mystorageaccount** tooyour blob depolama hesabı adı, **mycontainer** toohello kapsayıcı adı **depolama hesabı anahtarı** tooyour blob depolama erişim tuşu.</span><span class="sxs-lookup"><span data-stu-id="e654c-239">Replace **C:\myfolder** toohello path where your file is stored, **mystorageaccount** tooyour blob storage account name, **mycontainer** toohello container name, **storage account key** tooyour blob storage access key.</span></span> <span data-ttu-id="e654c-240">Depolama hesabı kimlik bilgilerinizi bulabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e654c-240">You can find your storage account credentials in [Azure portal](https://portal.azure.com).</span></span>

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

<span data-ttu-id="e654c-242">PowerShell veya bir komut isteminden AzCopy komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e654c-242">Run AzCopy command in PowerShell or from a command prompt.</span></span> <span data-ttu-id="e654c-243">Bazı örnek kullanım AzCopy komut şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e654c-243">Here is some example usage of AzCopy command:</span></span>

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



<span data-ttu-id="e654c-244">Çalıştırdığınız sonra AzCopy komut toocopy tooan dosyanızı gördüğünüz Azure blob Azure Storage Gezgini kısa süre içinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e654c-244">Once you run your AzCopy command toocopy tooan Azure blob you see your file shows up in Azure Storage Explorer shortly.</span></span>

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

<span data-ttu-id="e654c-246">**VM tooAzure Blob ' veri taşıma: Azure Storage Gezgini**</span><span class="sxs-lookup"><span data-stu-id="e654c-246">**Move data from VM tooAzure Blob: Azure Storage Explorer**</span></span>

<span data-ttu-id="e654c-247">Azure Depolama Gezgini'ni kullanarak, VM'yi hello yerel dosya verileri de karşıya yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e654c-247">You can also upload data from hello local file in your VM using Azure Storage Explorer:</span></span>

* <span data-ttu-id="e654c-248">tooupload veri tooa kapsayıcısı, select hello hedef kapsayıcı ve tıklatın hello **karşıya** düğmesini.![ Depolama Gezgini'nde karşıya yükle](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="e654c-248">tooupload data tooa container, select hello target container and click hello **Upload** button.![Upload in Storage Explorer](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span></span>
* <span data-ttu-id="e654c-249">Tıklatın hello üzerinde **...**  hello sağında toohello **dosyaları** kutusunda, bir veya birden çok dosya tooupload hello dosya sisteminden seçin ve'ı tıklatın **karşıya** hello dosyaları karşıya yükleme toobegin.![ Dosyaları tooblob karşıya yükle](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="e654c-249">Click on hello **...** toohello right of hello **Files** box, select one or multiple files tooupload from hello file system and click **Upload** toobegin uploading hello files.![Upload files tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span></span>

<span data-ttu-id="e654c-250">**Verileri Azure Blob'tan okuyun: Machine Learning okuyucu Modülü**</span><span class="sxs-lookup"><span data-stu-id="e654c-250">**Read data from Azure Blob: Machine Learning reader module**</span></span>

<span data-ttu-id="e654c-251">Azure Machine Learning Studio'da kullanabileceğiniz bir **veri içeri aktarma modülü** , blob tooread verileri.</span><span class="sxs-lookup"><span data-stu-id="e654c-251">In Azure Machine Learning Studio you can use an **Import Data module** tooread data from your blob.</span></span>

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

<span data-ttu-id="e654c-253">**Verileri Azure Blob'tan okuyun: Python ODBC**</span><span class="sxs-lookup"><span data-stu-id="e654c-253">**Read data from Azure Blob: Python ODBC**</span></span>

<span data-ttu-id="e654c-254">Kullanabileceğiniz **BlobService** kitaplığı tooread verileri doğrudan Jupyter Not Defteri veya Python programında blob.</span><span class="sxs-lookup"><span data-stu-id="e654c-254">You can use **BlobService** library tooread data directly from blob in a Jupyter Notebook or Python program.</span></span>

<span data-ttu-id="e654c-255">İlk olarak, gerekli paketleri içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="e654c-255">First, import required packages:</span></span>

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

<span data-ttu-id="e654c-256">Ardından Azure Blob hesabı kimlik bilgilerinizi Tak ve Kullan veri Blobundan okuyun:</span><span class="sxs-lookup"><span data-stu-id="e654c-256">Then plug in your Azure Blob account credentials and read data from Blob:</span></span>

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

<span data-ttu-id="e654c-257">Merhaba veriler, veri çerçeve olarak okunur:</span><span class="sxs-lookup"><span data-stu-id="e654c-257">hello data is read in as a data frame:</span></span>

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a><span data-ttu-id="e654c-259">Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="e654c-259">Azure Data Lake</span></span>
<span data-ttu-id="e654c-260">Azure Data Lake Store, büyük veri analitik iş yükleri ve uyumlu olan Hadoop dağıtılmış dosya sistemi (HDFS) için hiper ölçekli bir depodur.</span><span class="sxs-lookup"><span data-stu-id="e654c-260">Azure Data Lake Storage is a hyper-scale repository for big data analytics workloads and compatible with Hadoop Distributed File System (HDFS).</span></span> <span data-ttu-id="e654c-261">Merhaba Hadoop ekosistemi ve hello Azure Data Lake Analytics ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="e654c-261">It works with both hello Hadoop ecosystem and hello Azure Data Lake Analytics.</span></span> <span data-ttu-id="e654c-262">Nasıl hello Azure Data Lake Store verilerini taşımak ve Azure Data Lake Analytics'i kullanarak analizler çalıştırır gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="e654c-262">We show how you can move data into hello Azure Data Lake Store and run analytics using Azure Data Lake Analytics.</span></span>

<span data-ttu-id="e654c-263">**Önkoşul**</span><span class="sxs-lookup"><span data-stu-id="e654c-263">**Prerequisite**</span></span>

* <span data-ttu-id="e654c-264">İçinde Azure Data Lake Analytics oluşturma [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e654c-264">Create your Azure Data Lake Analytics in [Azure portal](https://portal.azure.com).</span></span>

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* <span data-ttu-id="e654c-266">Merhaba **Azure Data Lake Araçları** içinde **Visual Studio** şu anda bulunan [bağlantı](https://www.microsoft.com/download/details.aspx?id=49504) hello Visual Studio Community hello sanal makinede olan sürümü zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="e654c-266">hello  **Azure Data Lake Tools** in **Visual Studio** found at this  [link](https://www.microsoft.com/download/details.aspx?id=49504) is already installed on hello Visual Studio Community Edition which is on hello virtual machine.</span></span> <span data-ttu-id="e654c-267">Visual Studio başlangıç ve Azure aboneliğinizde oturum sonra Azure Data Analytics hesabınızı ve Visual Studio'nun hello sol panelinde depolama görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e654c-267">After starting Visual Studio and logging in your Azure subscription, you should see your Azure Data Analytics account and storage in hello left panel of Visual Studio.</span></span>

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

<span data-ttu-id="e654c-269">**VM tooData Lake veri taşıma: Azure Data Lake Gezgini**</span><span class="sxs-lookup"><span data-stu-id="e654c-269">**Move data from VM tooData Lake: Azure Data Lake Explorer**</span></span>

<span data-ttu-id="e654c-270">Kullanabileceğiniz **Azure Data Lake Explorer** hello yerel dosyaları, sanal makine tooData Lake depolama tooupload verileri.</span><span class="sxs-lookup"><span data-stu-id="e654c-270">You can use **Azure Data Lake Explorer** tooupload data from hello local files in your Virtual Machine tooData Lake storage.</span></span>

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

<span data-ttu-id="e654c-272">Hello kullanarak, veri taşıma tooor Azure Data Lake gelen veri ardışık düzen tooproductionize oluşturabilir [Azure veri Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="e654c-272">You can also build a data pipeline tooproductionize your data movement tooor from Azure Data Lake using hello [Azure Data Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span></span> <span data-ttu-id="e654c-273">Biz toothis başvuran [makale](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide hello adımları toobuild hello veri size ardışık düzenleri.</span><span class="sxs-lookup"><span data-stu-id="e654c-273">We refer you toothis [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide you through hello steps toobuild hello data pipelines.</span></span>

<span data-ttu-id="e654c-274">**Azure Blob tooData Lake veri okuma: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="e654c-274">**Read data from Azure Blob tooData Lake: U-SQL**</span></span>

<span data-ttu-id="e654c-275">Verileriniz Azure Blob depolama alanına bulunuyorsa, U-SQL sorgusunda Azure depolama blobunu gelen verileri doğrudan okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="e654c-275">If your data resides in Azure Blob storage, you can directly read data from Azure storage blob in U-SQL query.</span></span> <span data-ttu-id="e654c-276">U-SQL sorgusu oluşturma önce bağlantılı tooyour Azure Data Lake blob storage hesabı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e654c-276">Before composing your U-SQL query, make sure your blob storage account is linked tooyour Azure Data Lake.</span></span> <span data-ttu-id="e654c-277">Çok Git**Azure portal**, Azure Data Lake Analytics panonuz bulmak, tıklatın **veri kaynağı Ekle**, çok depolama türü seçin**Azure Storage** ve Azure Storage'da takın Anahtar ve hesap adı.</span><span class="sxs-lookup"><span data-stu-id="e654c-277">Go too**Azure portal**, find your Azure Data Lake Analytics dashboard, click **Add Data Source**, select storage type too**Azure Storage** and plug in your Azure Storage Account Name and Key.</span></span> <span data-ttu-id="e654c-278">Ardından, hello depolama hesabında depolanan mümkün tooreference hello verilerdir.</span><span class="sxs-lookup"><span data-stu-id="e654c-278">Then you are able tooreference hello data stored in hello storage account.</span></span>

![Depolama hesabı ve anahtarı girin](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

<span data-ttu-id="e654c-280">Visual Studio'da veri blob depolama alanından okuyun, bazı veri işleme, özellik Mühendisliği ve çıktı hello ortaya çıkan veri tooeither Azure Data Lake veya Azure Blob Storage yapın.</span><span class="sxs-lookup"><span data-stu-id="e654c-280">In Visual Studio, you can read data from blob storage, do some data manipulation, feature engineering, and output hello resulting data tooeither Azure Data Lake or Azure Blob Storage.</span></span> <span data-ttu-id="e654c-281">Blob depolama birimindeki hello veri başvurduğunuzda kullanmak **wasb: / /**; Azure Data Lake, kullanım hello verilerde başvurduğunuzda **swbhdfs: / /**</span><span class="sxs-lookup"><span data-stu-id="e654c-281">When you reference hello data in blob storage, use **wasb://**; when you reference hello data in Azure Data Lake, use **swbhdfs://**</span></span>

![Veri çerçevesi](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

<span data-ttu-id="e654c-283">Visual Studio'da U-SQL sorguları aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e654c-283">You may use hello following U-SQL queries in Visual Studio:</span></span>

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



<span data-ttu-id="e654c-284">Merhaba, işin durumunu gösteren bir diyagram sorgunuzu gönderilen toohello sunucusudur sonra görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e654c-284">After your query is submitted toohello server, a diagram showing hello status of your job is displayed.</span></span>

![İş durumu diyagramı](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

<span data-ttu-id="e654c-286">**Data Lake veri sorgulama: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="e654c-286">**Query data in Data Lake: U-SQL**</span></span>

<span data-ttu-id="e654c-287">Azure Data Lake Hello dataset alınan sonra kullanabileceğiniz [U-SQL dili](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery ve hello verileri keşfedin.</span><span class="sxs-lookup"><span data-stu-id="e654c-287">After hello dataset is ingested into Azure Data Lake, you can use [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery and explore hello data.</span></span> <span data-ttu-id="e654c-288">U-SQL dili benzer Systems SQL olmakla birlikte, böylece kullanıcılar özelleştirilmiş modüller, kullanıcı tanımlı işlevler ve vb. yazabilirsiniz bazı C# özellikleri birleştirir. Merhaba önceki adımda hello komut dosyalarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-288">U-SQL language is similar tooT-SQL, but combines some features from C# so that users can write customized modules, user-defined functions, and etc. You can use hello scripts in hello previous step.</span></span>

<span data-ttu-id="e654c-289">Merhaba sorgu gönderilen tooserver, tripdata_summary sonra. CSV, kısa süre içinde bulunabilir **Azure Data Lake Explorer**, sağ hello dosyası tarafından hello verileri önizleyin.</span><span class="sxs-lookup"><span data-stu-id="e654c-289">After hello query is submitted tooserver, tripdata_summary.CSV can be found shortly in **Azure Data Lake Explorer**, you may preview hello data by right-click hello file.</span></span>

![Azure Data Lake Gezgini'ndeki Dosya](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

<span data-ttu-id="e654c-291">toosee hello dosya bilgileri:</span><span class="sxs-lookup"><span data-stu-id="e654c-291">toosee hello file information:</span></span>

![Dosya Özeti](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a><span data-ttu-id="e654c-293">Hdınsight Hadoop kümeleri</span><span class="sxs-lookup"><span data-stu-id="e654c-293">HDInsight Hadoop Clusters</span></span>
<span data-ttu-id="e654c-294">Azure Hdınsight bir yönetilen Apache Hadoop, Spark, HBase ve Storm hello buluttaki hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="e654c-294">Azure HDInsight is a managed Apache Hadoop, Spark, HBase, and Storm service on hello cloud.</span></span> <span data-ttu-id="e654c-295">Azure Hdınsight kümeleri hello veri bilimi sanal makineden kolayca çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-295">You can work easily with Azure HDInsight clusters from hello data science virtual machine.</span></span>

<span data-ttu-id="e654c-296">**Önkoşul**</span><span class="sxs-lookup"><span data-stu-id="e654c-296">**Prerequisite**</span></span>

* <span data-ttu-id="e654c-297">Azure Blob storage hesabınızdan oluşturma [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e654c-297">Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e654c-298">Bu depolama hesabı, Hdınsight kümeleri için kullanılan toostore verilerdir.</span><span class="sxs-lookup"><span data-stu-id="e654c-298">This storage account is used toostore data for HDInsight clusters.</span></span>

![Azure Blob storage hesabı oluşturma](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="e654c-300">Azure Hdınsight Hadoop kümelerini gelen özelleştirme [Azure portalı](machine-learning-data-science-customize-hadoop-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="e654c-300">Customize Azure HDInsight Hadoop Clusters from [Azure portal](machine-learning-data-science-customize-hadoop-cluster.md)</span></span>
  
  * <span data-ttu-id="e654c-301">Hdınsight kümenizle oluşturulduğunda oluşturulan hello depolama hesabı bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e654c-301">You must link hello storage account created with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="e654c-302">Bu depolama hesabı hello küme içinde işlenebilecek verilerine erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e654c-302">This storage account is used for accessing data that can be processed within hello cluster.</span></span>

![Hdınsight kümesi ile oluşturulan bağlantı toostorage hesabı](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* <span data-ttu-id="e654c-304">Etkinleştirmelisiniz **uzaktan erişim** oluşturulduktan sonra hello küme baş düğümüne toohello.</span><span class="sxs-lookup"><span data-stu-id="e654c-304">You must enable **Remote Access** toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="e654c-305">Burada belirttiğiniz (Merhaba küme oluşturma sırasında belirtilen kullanılanlardan farklı) başlangıç uzaktan erişim kimlik bilgilerini Hatırla: hello sonraki yordamda gerekir.</span><span class="sxs-lookup"><span data-stu-id="e654c-305">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them in hello subsequent procedure.</span></span>

![Uzaktan erişimi etkinleştirin](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* <span data-ttu-id="e654c-307">Bir Azure Machine Learning çalışma alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e654c-307">Create an Azure Machine Learning workspace.</span></span> <span data-ttu-id="e654c-308">Makine öğrenimi denemelerine bu Machine Learning çalışma alanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="e654c-308">Your Machine Learning Experiments are stored in this Machine Learning workspace.</span></span> <span data-ttu-id="e654c-309">Vurgulanan hello seçenekleri portalında hello ekran aşağıdaki gösterildiği gibi seçin:</span><span class="sxs-lookup"><span data-stu-id="e654c-309">Select hello highlighted options in Portal as shown in hello following screenshot:</span></span>

![Bir Azure Machine Learning çalışma alanı oluşturma](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* <span data-ttu-id="e654c-311">Ardından hello parametreleri için çalışma alanınızı girin</span><span class="sxs-lookup"><span data-stu-id="e654c-311">Then enter hello parameters for your workspace</span></span>

![Machine Learning çalışma alanı parametreleri girin](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* <span data-ttu-id="e654c-313">IPython Not Defteri kullanarak verileri karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e654c-313">Upload data using IPython Notebook.</span></span> <span data-ttu-id="e654c-314">İlk gerekli paketleri içeri aktarmak, kimlik bilgilerini takın, bir db depolama hesabınızı oluşturmak ve sonra veri tooHDI kümelerini yüklemek.</span><span class="sxs-lookup"><span data-stu-id="e654c-314">First import required packages, plug in credentials, create a db in your storage account, then load data tooHDI clusters.</span></span>

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


* <span data-ttu-id="e654c-315">Alternatif olarak, bu izleyebilirsiniz [izlenecek](machine-learning-data-science-process-hive-walkthrough.md) tooupload NYC ücreti verileri tooHDI küme.</span><span class="sxs-lookup"><span data-stu-id="e654c-315">Alternately,  you can follow this [walkthrough](machine-learning-data-science-process-hive-walkthrough.md) tooupload NYC Taxi data tooHDI cluster.</span></span> <span data-ttu-id="e654c-316">Önemli adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e654c-316">Major steps include:</span></span>
  
  * <span data-ttu-id="e654c-317">AzCopy: CSV ait ortak blob tooyour yerel klasörden sıkıştırılmış indirme</span><span class="sxs-lookup"><span data-stu-id="e654c-317">AzCopy: download zipped CSV's from public blob tooyour local folder</span></span>
  * <span data-ttu-id="e654c-318">AzCopy: sıkıştırması açılmış CSV ait yerel klasör tooHDI kümeden karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="e654c-318">AzCopy: upload unzipped CSV's from local folder tooHDI cluster</span></span>
  * <span data-ttu-id="e654c-319">Merhaba baş Hadoop küme düğümüne oturum ve keşif veri analizi için hazırlama</span><span class="sxs-lookup"><span data-stu-id="e654c-319">Log into hello head node of Hadoop cluster and prepare for exploratory data analysis</span></span>

<span data-ttu-id="e654c-320">Merhaba veri yüklenen tooHDI küme sonra verilerinizi Azure Storage Gezgini kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-320">After hello data is loaded tooHDI cluster, you can check your data in Azure Storage Explorer.</span></span> <span data-ttu-id="e654c-321">Ve HDI kümesi içinde oluşturulan bir veritabanı nyctaxidb vardır.</span><span class="sxs-lookup"><span data-stu-id="e654c-321">And you have a database nyctaxidb created in HDI cluster.</span></span>

<span data-ttu-id="e654c-322">**Veri keşfi: Python Hive sorguları**</span><span class="sxs-lookup"><span data-stu-id="e654c-322">**Data exploration: Hive Queries in Python**</span></span>

<span data-ttu-id="e654c-323">Merhaba verileri Hadoop kümesinde olduğundan, hello pyodbc paket tooconnect tooHadoop kullanabilirsiniz kümeleri ve Hive toodo araştırması ve özellik Mühendisliği kullanarak veritabanını sorgula.</span><span class="sxs-lookup"><span data-stu-id="e654c-323">Since hello data is in Hadoop cluster, you can use hello pyodbc package tooconnect tooHadoop Clusters and query database using Hive toodo exploration and feature engineering.</span></span> <span data-ttu-id="e654c-324">Merhaba varolan tablolardan hello önkoşul adımda oluşturduğumuz görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-324">You can view hello existing tables we created in hello prerequisite step.</span></span>

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Var olan tabloları görüntüleme](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

<span data-ttu-id="e654c-326">Her ay ve hello sıklıkları kayıt hello sayısı bakalım Eğimli veya hello seyahat tablosunda yok:</span><span class="sxs-lookup"><span data-stu-id="e654c-326">Let's look at hello number of records in each month and hello frequencies of tipped or not in hello trip table:</span></span>

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

<span data-ttu-id="e654c-329">Biz de toplama konumu ve dropoff konumu arasındaki hello uzaklığı işlem ve toohello karşılaştırmak seyahat uzaklığı.</span><span class="sxs-lookup"><span data-stu-id="e654c-329">We can also compute hello distance between pickup location and dropoff location and then compare it toohello trip distance.</span></span>

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

<span data-ttu-id="e654c-332">Şimdi şimdi modelleme için bir aşağı örneklenen (% 1) veri kümesi hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="e654c-332">Now let's prepare a down-sampled (1%) set of data for modeling.</span></span> <span data-ttu-id="e654c-333">Machine Learning okuyucu modülünde size bu verileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-333">We can use this data in Machine Learning reader module.</span></span>

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

<span data-ttu-id="e654c-334">Bir süre sonra hello verileri Hadoop kümeleri yüklenen görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e654c-334">After a while, you can see hello data has been loaded in Hadoop clusters:</span></span>

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Veri tablosu](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

<span data-ttu-id="e654c-336">**Machine Learning kullanarak HDI veri okuma: okuyucu Modülü**</span><span class="sxs-lookup"><span data-stu-id="e654c-336">**Read data from HDI using Machine Learning: reader module**</span></span>

<span data-ttu-id="e654c-337">Merhaba de kullanabilir **okuyucu** modülü Machine Learning Studio tooaccess hello veritabanındaki Hadoop kümesi.</span><span class="sxs-lookup"><span data-stu-id="e654c-337">You may also use hello **reader** module in Machine Learning Studio tooaccess hello database in Hadoop cluster.</span></span> <span data-ttu-id="e654c-338">Hello kimlik bilgileri, HDI kümelerin Tak ve Azure depolama hesabı tooenable lık machine learning HDI kümelerde veritabanını kullanarak modelleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e654c-338">Plug in hello credentials of your HDI clusters and Azure Storage Account tooenable build ing machine learning models using database in HDI clusters.</span></span>

![Okuyucu modülü özellikleri](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

<span data-ttu-id="e654c-340">Merhaba puanlanmış veri kümesi ardından görüntülenebilir:</span><span class="sxs-lookup"><span data-stu-id="e654c-340">hello scored dataset can then be viewed:</span></span>

![Puanlanmış veri kümesini görüntülemek](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a><span data-ttu-id="e654c-342">Azure SQL Data Warehouse & veritabanları</span><span class="sxs-lookup"><span data-stu-id="e654c-342">Azure SQL Data Warehouse & databases</span></span>
<span data-ttu-id="e654c-343">Azure SQL Data Warehouse kurumsal sınıf SQL Server deneyimi hizmetiyle bir esnek veri ambarı gibidir.</span><span class="sxs-lookup"><span data-stu-id="e654c-343">Azure SQL Data Warehouse is an elastic data warehouse as a service with enterprise-class SQL Server experience.</span></span>

<span data-ttu-id="e654c-344">Bu konuda sağlanan hello yönergeleri izleyerek, Azure SQL Data Warehouse sağlayabilirsiniz [makale](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e654c-344">You can provision your Azure SQL Data Warehouse by following hello instructions provided in this [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span></span> <span data-ttu-id="e654c-345">Azure SQL veri ambarı sağlamak sonra bunu kullanabilirsiniz [izlenecek](machine-learning-data-science-process-sqldw-walkthrough.md) araştırması ve modelleme kullanarak verileri hello SQL Data Warehouse içinde toodo veri yükleme.</span><span class="sxs-lookup"><span data-stu-id="e654c-345">Once you provision your Azure SQL Data Warehouse, you can use this [walkthrough](machine-learning-data-science-process-sqldw-walkthrough.md) toodo data upload, exploration and modeling using data within hello SQL Data Warehouse.</span></span>

#### <a name="azure-cosmos-db"></a><span data-ttu-id="e654c-346">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e654c-346">Azure Cosmos DB</span></span>
<span data-ttu-id="e654c-347">Azure Cosmos DB hello bulutta bir NoSQL veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="e654c-347">Azure Cosmos DB is a NoSQL database in hello cloud.</span></span> <span data-ttu-id="e654c-348">JSON gibi belgelerle toowork sağlar ve toostore ve sorgu hello belgeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="e654c-348">It allows you toowork with documents like JSON and allows you toostore and query hello documents.</span></span>

<span data-ttu-id="e654c-349">Koşullar başına adımları tooaccess Azure Cosmos DB DSVM hello aşağıdaki toodo hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="e654c-349">You need toodo hello following per-requisites steps tooaccess Azure Cosmos DB from hello DSVM.</span></span>

1. <span data-ttu-id="e654c-350">DocumentDB Python SDK'sını yükleyin (çalıştırmak ```pip install pydocumentdb``` komut isteminden)</span><span class="sxs-lookup"><span data-stu-id="e654c-350">Install DocumentDB Python SDK (Run ```pip install pydocumentdb``` from command prompt)</span></span>
2. <span data-ttu-id="e654c-351">Bir Azure Cosmos DB hesap oluşturup bir veritabanından [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="e654c-351">Create an Azure Cosmos DB account and a database from [Azure portal](https://portal.azure.com)</span></span>
3. <span data-ttu-id="e654c-352">"Azure Cosmos DB geçiş aracı" indirin [burada](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) ve tercih ettiğiniz tooa dizine ayıklayın</span><span class="sxs-lookup"><span data-stu-id="e654c-352">Download "Azure Cosmos DB Migration Tool" from [here](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) and extract tooa directory of your choice</span></span>
4. <span data-ttu-id="e654c-353">Alma depolanmış JSON verilerini (volcano) bir [ortak blob](https://cahandson.blob.core.windows.net/samples/volcano.json) Cosmos DB aşağıdaki komut parametreleri toohello Geçiş Aracı (Merhaba Cosmos DB geçiş aracı yüklendiği hello dizininden dtui.exe) ile içine.</span><span class="sxs-lookup"><span data-stu-id="e654c-353">Import JSON data (volcano data) stored on a [public blob](https://cahandson.blob.core.windows.net/samples/volcano.json) into Cosmos DB with following command parameters toohello migration tool (dtui.exe from hello directory where you installed hello Cosmos DB Migration Tool).</span></span> <span data-ttu-id="e654c-354">Bu parametreler ile Merhaba kaynak ve hedef konumu girin:</span><span class="sxs-lookup"><span data-stu-id="e654c-354">Enter hello source and target location with these parameters:</span></span>
   
    <span data-ttu-id="e654c-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/; AccountKey = [[anahtar]; veritabanı volcano /t.Collection:volcano1 =</span><span class="sxs-lookup"><span data-stu-id="e654c-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span></span>

<span data-ttu-id="e654c-356">Bir kez hello veri içe aktardıktan sonra tooJupyter ve açık hello dizüstü başlıklı gidebilirsiniz *DocumentDBSample* python içeren tooaccess DocumentDB kod ve bazı temel sorgulama yapın.</span><span class="sxs-lookup"><span data-stu-id="e654c-356">Once you import hello data, you can go tooJupyter and open hello notebook titled *DocumentDBSample* which contains python code tooaccess DocumentDB and do some basic querying.</span></span> <span data-ttu-id="e654c-357">Cosmos DB hakkında daha fazla hello hizmet adresini ziyaret ederek bilgi [belge sayfasının](https://docs.microsoft.com/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="e654c-357">You can learn more about Cosmos DB by visiting hello service [documentation page](https://docs.microsoft.com/azure/cosmos-db/).</span></span>

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a><span data-ttu-id="e654c-358">8. Raporları ve panoyu Power BI Desktop hello kullanarak derleme</span><span class="sxs-lookup"><span data-stu-id="e654c-358">8. Build reports and dashboard using hello Power BI Desktop</span></span>
<span data-ttu-id="e654c-359">Bize Power BI toogain visual Öngörüler hello veri içinde Cosmos DB örnek önceki hello içinde gördüğümüz hello Volcano JSON dosyası görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="e654c-359">Let us visualize hello Volcano JSON file that we saw in hello preceding Cosmos DB example in Power BI toogain visual insights into hello data.</span></span> <span data-ttu-id="e654c-360">Ayrıntılı adımlar hello kullanılabilir [Power BI makale](../cosmos-db/powerbi-visualize.md).</span><span class="sxs-lookup"><span data-stu-id="e654c-360">Detailed steps are available in hello [Power BI article](../cosmos-db/powerbi-visualize.md).</span></span> <span data-ttu-id="e654c-361">Merhaba üst düzey adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e654c-361">Here are hello high-level steps:</span></span>

1. <span data-ttu-id="e654c-362">Power BI Desktop açın ve "Veri Al" yapın.</span><span class="sxs-lookup"><span data-stu-id="e654c-362">Open Power BI Desktop and do "Get Data".</span></span> <span data-ttu-id="e654c-363">Merhaba URL'yi belirtin: https://cahandson.blob.core.windows.net/samples/volcano.json</span><span class="sxs-lookup"><span data-stu-id="e654c-363">Specify hello URL as: https://cahandson.blob.core.windows.net/samples/volcano.json</span></span>
2. <span data-ttu-id="e654c-364">Bir liste olarak alınan hello JSON kayıtlar görmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="e654c-364">You should see hello JSON records imported as a list</span></span>
3. <span data-ttu-id="e654c-365">Power BI ile Merhaba aynı çalışabilmeniz için hello listesi tooa tablosunda Dönüştür</span><span class="sxs-lookup"><span data-stu-id="e654c-365">Convert hello list tooa table so Power BI can work with hello same</span></span>
4. <span data-ttu-id="e654c-366">Genişletme hello sütunlar üzerinde hello tıklayarak genişletin simgesi (Merhaba bir hello sütun sağında hello hello "sol ve sağ ok" simgesine ile)</span><span class="sxs-lookup"><span data-stu-id="e654c-366">Expand hello columns by clicking on hello expand icon (hello one with hello "left arrow and a right arrow" icon on hello right of hello column)</span></span>
5. <span data-ttu-id="e654c-367">Konum "Kayıt" alanını olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e654c-367">Notice that location is a "Record" field.</span></span> <span data-ttu-id="e654c-368">Merhaba kaydı'nı genişletin ve yalnızca hello koordinatları seçin.</span><span class="sxs-lookup"><span data-stu-id="e654c-368">Expand hello record and select only hello coordinates.</span></span> <span data-ttu-id="e654c-369">Liste sütununu koordinat değil</span><span class="sxs-lookup"><span data-stu-id="e654c-369">Coordinate is a list column</span></span>
6. <span data-ttu-id="e654c-370">Yeni bir sütun tooconvert hello listesi koordinat sütun hello formülü kullanarak hello koordinat listesi alanı hello iki öğeleri birleştirme virgülle ayrı LatLong sütununa eklemek ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span><span class="sxs-lookup"><span data-stu-id="e654c-370">Add a new column tooconvert hello list coordinate column into a comma separate LatLong column concatenating hello two elements in hello coordinate list field using hello formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span></span>
7. <span data-ttu-id="e654c-371">Son olarak hello Dönüştür ```Elevation``` sütun tooDecimal ve select hello **Kapat** ve **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="e654c-371">Finally convert hello ```Elevation``` column tooDecimal and select hello **Close** and **Apply**.</span></span>

<span data-ttu-id="e654c-372">Adımları önceki yerine, yapıştırabilirsiniz hello adımlar kullanılan komutlar koddan hello hello Gelişmiş Düzenleyici Power bı'da bir sorgu dili toowrite hello veri dönüşümlerine izin verir.</span><span class="sxs-lookup"><span data-stu-id="e654c-372">Instead of preceding steps, you can paste hello following code that scripts out hello steps used in hello Advanced Editor in Power BI that allows you toowrite hello data transformations in a query language.</span></span>

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



<span data-ttu-id="e654c-373">Artık Power BI veri modelinizi hello veri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="e654c-373">You now have hello data in your Power BI data model.</span></span> <span data-ttu-id="e654c-374">Power BI desktop aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="e654c-374">Your Power BI desktop should appear as follows:</span></span>

![Power BI desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

<span data-ttu-id="e654c-376">Raporlar ve görselleştirmeleri hello veri modelini kullanarak oluşturmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-376">You can start building reports and visualizations using hello data model.</span></span> <span data-ttu-id="e654c-377">Bu başlangıç adımları izleyebilirsiniz [Power BI makale](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild bir rapor.</span><span class="sxs-lookup"><span data-stu-id="e654c-377">You can follow hello steps in this [Power BI article](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild a report.</span></span> <span data-ttu-id="e654c-378">Merhaba sonuç hello şuna benzeyen bir rapordur.</span><span class="sxs-lookup"><span data-stu-id="e654c-378">hello end result is a report that looks like hello following.</span></span>

![Power BI Desktop rapor görünümü - Power BI Bağlayıcısı](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a><span data-ttu-id="e654c-380">9. Projenizi gerekir, DSVM toomeet dinamik ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="e654c-380">9. Dynamically scale your DSVM toomeet your project needs</span></span>
<span data-ttu-id="e654c-381">Yukarı ve aşağı hello DSVM toomeet, projenin ihtiyaç duyduğu ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-381">You can scale up and down hello DSVM toomeet your project needs.</span></span> <span data-ttu-id="e654c-382">Toouse hello VM hello Akşam veya hafta sonları gerekmiyorsa, yalnızca hello VM hello gelen aşağı kapatabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e654c-382">If you don't need toouse hello VM in hello evening or weekends, you can just shut down hello VM from hello [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="e654c-383">Merhaba VM üzerinde yalnızca hello işletim sistemi kapatma düğmesini kullanırsanız, bilgi işlem ücretleri.</span><span class="sxs-lookup"><span data-stu-id="e654c-383">You incur compute charges if you use just hello Operating system shutdown button on hello VM.</span></span>  
> 
> 

<span data-ttu-id="e654c-384">Bazı büyük ölçekli analiz toohandle gerekir ve daha fazla CPU ve/veya bellek ve/veya disk kapasitesine ihtiyacınız varsa, VM boyutlarını CPU çekirdekleri, bellek kapasitesi ve (katı hal sürücüleri dahil), bilgi işlem ve bütçe gereksinimlerinize uyan disk türleri açısından büyük seçimine bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-384">If you need toohandle some large-scale analysis and need more CPU and/or memory and/or disk capacity you can find a large choice of VM sizes in terms of CPU cores, memory capacity and disk types (including Solid state drives) that meet your compute and budgetary needs.</span></span> <span data-ttu-id="e654c-385">Merhaba veritabanlarının saatlik işlem fiyatlandırma birlikte tam listesi VM'ler üzerinde hello kullanılabilir [Azure Virtual Machines fiyatlandırması](https://azure.microsoft.com/pricing/details/virtual-machines/) sayfası.</span><span class="sxs-lookup"><span data-stu-id="e654c-385">hello full list of VMs along with their hourly compute pricing is available on hello [Azure Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span></span>

<span data-ttu-id="e654c-386">Benzer şekilde, VM işleme kapasitesi, gereksinimini azaltır, (örneğin: önemli iş yükü tooa Hadoop veya bir Spark kümesi taşınmış), hello hello kümeden aşağı ölçeklenebilen [Azure portal](https://portal.azure.com) ve vm'nizin toohello ayarları örneği.</span><span class="sxs-lookup"><span data-stu-id="e654c-386">Similarly, if your need for VM processing capacity reduces (for example: you moved a major workload tooa Hadoop or a Spark cluster), you can scale down hello cluster from hello [Azure portal](https://portal.azure.com) and going toohello settings of your VM instance.</span></span> <span data-ttu-id="e654c-387">Bir ekran görüntüsü aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e654c-387">Here is a screenshot.</span></span>

![VM örneği ayarları](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a><span data-ttu-id="e654c-389">10. Ek araçlar sanal makinenize yükleyin</span><span class="sxs-lookup"><span data-stu-id="e654c-389">10. Install additional tools on your virtual machine</span></span>
<span data-ttu-id="e654c-390">Biz hello ortak veri analizi gereksinimlerini ve, çoğu kaydettiğinizde tooinstall sahip kaçınarak zaman ortamlarınızın tek tek yapılandırmak ve yalnızca kaynaklar için ödeme tarafından paradan tasarruf edebilirsiniz tooaddress olan inanıyoruz çeşitli araçlar paketlenmiş kullanın.</span><span class="sxs-lookup"><span data-stu-id="e654c-390">We have packaged several tools that we believe are able tooaddress many of hello common data analytics needs and that should save you time by avoiding having tooinstall and configure your environments one by one and save you money by paying only for resources that you use.</span></span>

<span data-ttu-id="e654c-391">Diğer Azure veri yararlanabilir ve Analiz Hizmetleri bu makale tooenhance analytics ortamınızı profili.</span><span class="sxs-lookup"><span data-stu-id="e654c-391">You can leverage other Azure data and analytics services profiled in this article tooenhance your analytics environment.</span></span> <span data-ttu-id="e654c-392">Bazı durumlarda, gereksinimlerinize özel bazı üçüncü taraf araçları dahil olmak üzere ek araçlar gerektirebilir anlayın.</span><span class="sxs-lookup"><span data-stu-id="e654c-392">We understand that in some cases your needs may require additional tools, including some proprietary third-party tools.</span></span> <span data-ttu-id="e654c-393">Gereksinim duyduğunuz hello sanal makine tooinstall yeni araçları tam yönetim erişimi var.</span><span class="sxs-lookup"><span data-stu-id="e654c-393">You have full administrative access on hello virtual machine tooinstall new tools you need.</span></span> <span data-ttu-id="e654c-394">Python ve önceden yüklü R ayrıca ek paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e654c-394">You can also install additional packages in Python and R that are not pre-installed.</span></span> <span data-ttu-id="e654c-395">Python için ya da kullanabilirsiniz ```conda``` veya ```pip```.</span><span class="sxs-lookup"><span data-stu-id="e654c-395">For Python you can use either ```conda``` or ```pip```.</span></span> <span data-ttu-id="e654c-396">R için hello kullanabilirsiniz ```install.packages()``` hello R konsol veya hello IDE kullanın ve seçin "**paketleri** -> **yükleme paketleri...** ".</span><span class="sxs-lookup"><span data-stu-id="e654c-396">For R you can use hello ```install.packages()``` in hello R console or use hello IDE and choose "**Packages** -> **Install Packages...**".</span></span>

## <a name="summary"></a><span data-ttu-id="e654c-397">Özet</span><span class="sxs-lookup"><span data-stu-id="e654c-397">Summary</span></span>
<span data-ttu-id="e654c-398">Bunlar, Microsoft Veri bilimi sanal makine hello üzerinde hello yapabileceklerinizden yalnızca bazıları şunlardır.</span><span class="sxs-lookup"><span data-stu-id="e654c-398">These are just some of hello things you can do on hello Microsoft Data Science Virtual Machine.</span></span> <span data-ttu-id="e654c-399">Toomake yapabileceğiniz birçok şey daha vardır, etkili analytics ortam.</span><span class="sxs-lookup"><span data-stu-id="e654c-399">There are many more things you can do toomake it an effective analytics environment.</span></span>

