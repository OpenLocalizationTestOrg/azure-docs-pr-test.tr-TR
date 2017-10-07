---
title: "Machine Learning Python istemci kitaplığı aaaAccess kümeleriyle | Microsoft Docs"
description: "Yükleme ve hello Python istemci kitaplığı tooaccess kullanın ve Azure Machine Learning veri güvenli bir şekilde bir yerel Python ortamınızdan yönetin."
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a><span data-ttu-id="e994d-103">Python hello Azure Machine Learning Python istemci kitaplığı kullanılarak erişim kümeleriyle</span><span class="sxs-lookup"><span data-stu-id="e994d-103">Access datasets with Python using hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="e994d-104">Microsoft Azure Machine Learning Python istemci kitaplığı Hello önizlemesini güvenli erişim tooyour Azure Machine Learning veri kümelerini yerel Python Ortamı'ndan etkinleştirebilir ve hello oluşturulmasını ve bir çalışma alanı kümelerinde yönetimini sağlar.</span><span class="sxs-lookup"><span data-stu-id="e994d-104">hello preview of Microsoft Azure Machine Learning Python client library can enable secure access tooyour Azure Machine Learning datasets from a local Python environment and enables hello creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="e994d-105">Bu konu hakkında yönergeler sağlar:</span><span class="sxs-lookup"><span data-stu-id="e994d-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="e994d-106">Merhaba Machine Learning Python istemci Kitaplığı'nı yüklemek</span><span class="sxs-lookup"><span data-stu-id="e994d-106">install hello Machine Learning Python client library</span></span> 
* <span data-ttu-id="e994d-107">erişim ve yönergeler de dahil olmak üzere veri kümeleri, karşıya yükleme tooget yetkilendirme tooaccess, yerel Python ortamınızdan Azure Machine Learning veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="e994d-107">access and upload datasets, including instructions on how tooget authorization tooaccess Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="e994d-108">denemeler ara veri kümeleri erişim</span><span class="sxs-lookup"><span data-stu-id="e994d-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="e994d-109">Merhaba Python istemci kitaplığı tooenumerate veri kümelerini kullanan, meta verilerine erişmek, bir veri kümesi hello içeriğini okumak, yeni veri kümeleri oluşturma ve mevcut veri kümelerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e994d-109">use hello Python client library tooenumerate datasets, access metadata, read hello contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="e994d-110"><a name="prerequisites"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e994d-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="e994d-111">Merhaba Python istemci kitaplığı ortamları aşağıdaki hello altında test edilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e994d-111">hello Python client library has been tested under hello following environments:</span></span>

* <span data-ttu-id="e994d-112">Windows, Mac ve Linux</span><span class="sxs-lookup"><span data-stu-id="e994d-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="e994d-113">Python 2.7, 3.3 ve 3.4</span><span class="sxs-lookup"><span data-stu-id="e994d-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="e994d-114">Bu paketleri aşağıdaki hello üzerinde bir bağımlılığa sahiptir:</span><span class="sxs-lookup"><span data-stu-id="e994d-114">It has a dependency on hello following packages:</span></span>

* <span data-ttu-id="e994d-115">istekleri</span><span class="sxs-lookup"><span data-stu-id="e994d-115">requests</span></span>
* <span data-ttu-id="e994d-116">Python dateutil</span><span class="sxs-lookup"><span data-stu-id="e994d-116">python-dateutil</span></span>
* <span data-ttu-id="e994d-117">pandas</span><span class="sxs-lookup"><span data-stu-id="e994d-117">pandas</span></span>

<span data-ttu-id="e994d-118">Bir Python dağıtımı gibi kullanmanızı öneririz [Anaconda](http://continuum.io/downloads#all) veya [Kanopi](https://store.enthought.com/downloads/), Python, IPython gelen ve yukarıda listelenen hello üç paketleri yüklü.</span><span class="sxs-lookup"><span data-stu-id="e994d-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and hello three packages listed above installed.</span></span> <span data-ttu-id="e994d-119">IPython kesinlikle gerekli olmamakla birlikte, düzenleme ve etkileşimli olarak verileri görselleştirmek için harika bir ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="e994d-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="e994d-120"><a name="installation"></a>Nasıl tooinstall hello Azure Machine Learning Python istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="e994d-120"><a name="installation"></a>How tooinstall hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="e994d-121">Hello Azure Machine Learning Python istemci kitaplığı da yüklü toocomplete hello görevleri bu konuda anlatılan olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e994d-121">hello Azure Machine Learning Python client library must also be installed toocomplete hello tasks outlined in this topic.</span></span> <span data-ttu-id="e994d-122">Hello kullanılabilir [Python paket dizini](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="e994d-122">It is available from hello [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="e994d-123">tooinstall Python ortamınızda çalışması hello aşağıdaki komut, yerel Python ortamınızdan:</span><span class="sxs-lookup"><span data-stu-id="e994d-123">tooinstall it in your Python environment, run hello following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="e994d-124">Alternatif olarak, indirin ve hello kaynaklardan yüklemek [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="e994d-124">Alternatively, you can download and install from hello sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="e994d-125">Makinenizde git varsa, doğrudan hello git deposundan PIP tooinstall kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e994d-125">If you have git installed on your machine, you can use pip tooinstall directly from hello git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="e994d-126"><a name="datasetAccess"></a>Studio kod parçacıkları tooaccess veri kümelerini kullanma</span><span class="sxs-lookup"><span data-stu-id="e994d-126"><a name="datasetAccess"></a>Use Studio Code snippets tooaccess datasets</span></span>
<span data-ttu-id="e994d-127">Merhaba Python istemci kitaplığı çalıştırılmış denemeler programlı erişim tooyour mevcut veri kümeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e994d-127">hello Python client library gives you programmatic access tooyour existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="e994d-128">Merhaba Studio web arabiriminden konumu makinenizde Pandas DataFrame nesne olarak seri durumdan veri kümeleri ve tüm hello gerekli bilgileri toodownload içeren kod parçacıkları oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="e994d-128">From hello Studio web interface, you can generate code snippets that include all hello necessary information toodownload and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="e994d-129"><a name="security"></a>Veri erişimi için güvenlik</span><span class="sxs-lookup"><span data-stu-id="e994d-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="e994d-130">kod parçacıkları hello Python istemci kitaplığı ile kullanmak üzere çalışma alanı kimliği ve yetkilendirme içerir Studio tarafından sağlanan hello belirteci.</span><span class="sxs-lookup"><span data-stu-id="e994d-130">hello code snippets provided by Studio for use with hello Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="e994d-131">Bunlar tam erişim tooyour çalışma sağlayın ve parola gibi korunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e994d-131">These provide full access tooyour workspace and must be protected, like a password.</span></span>

<span data-ttu-id="e994d-132">Güvenlik nedenleriyle hello kod parçacığı işlevleri olarak ayarlayın, rolde kullanılabilir toousers Only'dir **sahibi** hello çalışma alanı için.</span><span class="sxs-lookup"><span data-stu-id="e994d-132">For security reasons, hello code snippet functionality is only available toousers that have their role set as **Owner** for hello workspace.</span></span> <span data-ttu-id="e994d-133">Rolünüze üzerinde hello Azure Machine Learning Studio'da görüntülenir **kullanıcılar** altında sayfa **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e994d-133">Your role is displayed in Azure Machine Learning Studio on hello **USERS** page under **Settings**.</span></span>

![Güvenlik][security]

<span data-ttu-id="e994d-135">Rolünüze olarak ayarlanmamışsa **sahibi**, istek sahibi olarak ortamına yeniden davet toobe veya hello çalışma tooprovide hello sahibi isteyin hello kod parçacığını sizinle.</span><span class="sxs-lookup"><span data-stu-id="e994d-135">If your role is not set as **Owner**, you can either request toobe reinvited as an owner, or ask hello owner of hello workspace tooprovide you with hello code snippet.</span></span>

<span data-ttu-id="e994d-136">tooobtain hello yetkilendirme belirtecini hello aşağıdakilerden birini yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e994d-136">tooobtain hello authorization token, you can do one of hello following:</span></span>

* <span data-ttu-id="e994d-137">Bir belirteci için bir sahibinden isteyin.</span><span class="sxs-lookup"><span data-stu-id="e994d-137">Ask for a token from an owner.</span></span> <span data-ttu-id="e994d-138">Sahipleri kendi yetkilendirme belirteçleri Studio'da kendi çalışma alanının hello Ayarları sayfasından erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e994d-138">Owners can access their authorization tokens from hello Settings page of their workspace in Studio.</span></span> <span data-ttu-id="e994d-139">Seçin **ayarları** sol bölmesinde ve tıklatın hello gelen **YETKİLENDİRME BELİRTEÇLERİ** toosee hello birincil ve ikincil belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="e994d-139">Select **Settings** from hello left pane and click **AUTHORIZATION TOKENS** toosee hello primary and secondary tokens.</span></span>  <span data-ttu-id="e994d-140">Hello birincil veya ikincil yetkilendirme belirteçleri hello hello kod parçacığında kullanılabilse de sahipleri yalnızca hello ikincil yetkilendirme belirteçleri paylaşıma önerilir.</span><span class="sxs-lookup"><span data-stu-id="e994d-140">Although either hello primary or hello secondary authorization tokens can be used in hello code snippet, it is recommended that owners only share hello secondary authorization tokens.</span></span>

![Yetkilendirme belirteçleri](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="e994d-142">Yükseltilen toobe toorole sahibinin isteyin.</span><span class="sxs-lookup"><span data-stu-id="e994d-142">Ask toobe promoted toorole of owner.</span></span>  <span data-ttu-id="e994d-143">toodo bu hello çalışma gereksinimlerini toofirst geçerli sahibini hello çalışma alanından kaldırmak daha sonra yeniden davet tooit sahibi olarak.</span><span class="sxs-lookup"><span data-stu-id="e994d-143">toodo this, a current owner of hello workspace needs toofirst remove you from hello workspace then re-invite you tooit as an owner.</span></span>

<span data-ttu-id="e994d-144">Geliştiriciler hello çalışma alanı kimliği ve yetkilendirme aldıktan sonra rolleri bakılmaksızın hello kod parçacığını kullanarak mümkün tooaccess hello çalışma oldukları belirteç.</span><span class="sxs-lookup"><span data-stu-id="e994d-144">Once developers have obtained hello workspace id and authorization token, they are able tooaccess hello workspace using hello code snippet regardless of their role.</span></span>

<span data-ttu-id="e994d-145">Yetkilendirme belirteçleri hello üzerinde yönetilen **YETKİLENDİRME BELİRTEÇLERİ** altında sayfa **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e994d-145">Authorization tokens are managed on hello **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="e994d-146">Bunları yeniden oluşturabilirsiniz, ancak bu yordamı erişim toohello önceki belirteci iptal eder.</span><span class="sxs-lookup"><span data-stu-id="e994d-146">You can regenerate them, but this procedure revokes access toohello previous token.</span></span>

### <span data-ttu-id="e994d-147"><a name="accessingDatasets"></a>Yerel bir Python uygulama erişim veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="e994d-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="e994d-148">Machine Learning Studio'da tıklatın **veri KÜMELERİ** hello sol gezinti çubuğunda hello.</span><span class="sxs-lookup"><span data-stu-id="e994d-148">In Machine Learning Studio, click **DATASETS** in hello navigation bar on hello left.</span></span>
2. <span data-ttu-id="e994d-149">Tooaccess istediğiniz hello veri kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="e994d-149">Select hello dataset you would like tooaccess.</span></span> <span data-ttu-id="e994d-150">Hello hello veri kümelerini seçebilirsiniz **MY veri KÜMELERİ** listesi veya hello **örnekleri** listesi.</span><span class="sxs-lookup"><span data-stu-id="e994d-150">You can select any of hello datasets from hello **MY DATASETS** list or from hello **SAMPLES** list.</span></span>
3. <span data-ttu-id="e994d-151">Merhaba alt araç çubuğundan tıklatın **veri erişim kodu oluştur**.</span><span class="sxs-lookup"><span data-stu-id="e994d-151">From hello bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="e994d-152">Merhaba veri hello Python istemci kitaplığı ile uyumlu bir biçimde ise, bu düğmesi devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="e994d-152">If hello data is in a format incompatible with hello Python client library, this button is disabled.</span></span>
   
    ![Veri kümeleri][datasets]
4. <span data-ttu-id="e994d-154">Merhaba kod parçacığını görünür hello penceresinden seçin ve tooyour panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e994d-154">Select hello code snippet from hello window that appears and copy it tooyour clipboard.</span></span>
   
    ![Erişim kodu][dataset-access-code]
5. <span data-ttu-id="e994d-156">Merhaba kodu yerel Python uygulamanızı hello not defterinize yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="e994d-156">Paste hello code into hello notebook of your local Python application.</span></span>
   
    ![Not Defteri][ipython-dataset]

## <span data-ttu-id="e994d-158"><a name="accessingIntermediateDatasets"></a>Machine Learning denemelerini ara veri kümeleri erişim</span><span class="sxs-lookup"><span data-stu-id="e994d-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="e994d-159">Bir denemeyi Machine Learning Studio hello çalıştırıldıktan sonra olası tooaccess modüllerin hello çıkış düğümlerinden hello ara veri kümeleri var.</span><span class="sxs-lookup"><span data-stu-id="e994d-159">After an experiment is run in hello Machine Learning Studio, it is possible tooaccess hello intermediate datasets from hello output nodes of modules.</span></span> <span data-ttu-id="e994d-160">Ara veri kümeleri oluşturulan ve model aracı çalıştırdığınızda ara adımlar için kullanılan verilerdir.</span><span class="sxs-lookup"><span data-stu-id="e994d-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="e994d-161">Merhaba veri biçimi hello Python istemci kitaplığı ile uyumlu olduğu sürece ara veri kümeleri erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="e994d-161">Intermediate datasets can be accessed as long as hello data format is compatible with hello Python client library.</span></span>

<span data-ttu-id="e994d-162">Merhaba aşağıdaki biçimleri desteklenir (sabittir bu hello `azureml.DataTypeIds` sınıfı):</span><span class="sxs-lookup"><span data-stu-id="e994d-162">hello following formats are supported (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="e994d-163">Düz metin</span><span class="sxs-lookup"><span data-stu-id="e994d-163">PlainText</span></span>
* <span data-ttu-id="e994d-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="e994d-164">GenericCSV</span></span>
* <span data-ttu-id="e994d-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="e994d-165">GenericTSV</span></span>
* <span data-ttu-id="e994d-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="e994d-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="e994d-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="e994d-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="e994d-168">Modül çıkış düğüm üzerinde gelerek hello biçimi belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e994d-168">You can determine hello format by hovering over a module output node.</span></span> <span data-ttu-id="e994d-169">Merhaba düğüm adı, bir araç ipucu ile birlikte görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e994d-169">It is displayed along with hello node name, in a tooltip.</span></span>

<span data-ttu-id="e994d-170">Bazı hello gibi hello modüllerin [bölünmüş] [ split] modülü, çıktı tooa biçimi adlı `Dataset`, hello Python istemci kitaplığı tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e994d-170">Some of hello modules, such as hello [Split][split] module, output tooa format named `Dataset`, which is not supported by hello Python client library.</span></span>

![Veri kümesi biçimi][dataset-format]

<span data-ttu-id="e994d-172">Toouse dönüştürme modülü gibi gereken [Dönüştür tooCSV][convert-to-csv], tooget desteklenen bir biçime bir çıktı.</span><span class="sxs-lookup"><span data-stu-id="e994d-172">You need toouse a conversion module, such as [Convert tooCSV][convert-to-csv], tooget an output into a supported format.</span></span>

![GenericCSV biçimi][csv-format]

<span data-ttu-id="e994d-174">Merhaba aşağıdaki adımlar, bir deneme oluşturur, çalıştırır ve hello Ara dataset erişen bir örnek gösterir.</span><span class="sxs-lookup"><span data-stu-id="e994d-174">hello following steps show an example that creates an experiment, runs it and accesses hello intermediate dataset.</span></span>

1. <span data-ttu-id="e994d-175">Yeni bir deneme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e994d-175">Create a new experiment.</span></span>
2. <span data-ttu-id="e994d-176">INSERT bir **yetişkin Census gelir ikili sınıflandırma dataset** modülü.</span><span class="sxs-lookup"><span data-stu-id="e994d-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="e994d-177">INSERT bir [bölünmüş] [ split] modül ve giriş toohello dataset modülü çıktısını bağlanın.</span><span class="sxs-lookup"><span data-stu-id="e994d-177">Insert a [Split][split] module, and connect its input toohello dataset module output.</span></span>
4. <span data-ttu-id="e994d-178">INSERT bir [Dönüştür tooCSV] [ convert-to-csv] modülü ve kendi giriş tooone Merhaba, bağlanmak [bölünmüş] [ split] modülü çıkarır.</span><span class="sxs-lookup"><span data-stu-id="e994d-178">Insert a [Convert tooCSV][convert-to-csv] module and connect its input tooone of hello [Split][split] module outputs.</span></span>
5. <span data-ttu-id="e994d-179">Merhaba deneme kaydetmek, çalıştırmak ve bekleyin çalıştıran toofinish.</span><span class="sxs-lookup"><span data-stu-id="e994d-179">Save hello experiment, run it, and wait for it toofinish running.</span></span>
6. <span data-ttu-id="e994d-180">Merhaba Hello çıkış düğümüne tıklayın [Dönüştür tooCSV] [ convert-to-csv] modülü.</span><span class="sxs-lookup"><span data-stu-id="e994d-180">Click hello output node on hello [Convert tooCSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="e994d-181">Merhaba bağlam menüsü görüntülendiğinde seçin **veri erişim kodu oluştur**.</span><span class="sxs-lookup"><span data-stu-id="e994d-181">When hello context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Bağlam menüsü][experiment]
8. <span data-ttu-id="e994d-183">Merhaba kod parçacığını seçin ve görüntülenen hello penceresinden tooyour panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e994d-183">Select hello code snippet and copy it tooyour clipboard from hello window that appears.</span></span>
   
    ![Erişim kodu][intermediate-dataset-access-code]
9. <span data-ttu-id="e994d-185">Merhaba kodu defterinizde yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="e994d-185">Paste hello code in your notebook.</span></span>
   
    ![Not Defteri][ipython-intermediate-dataset]
10. <span data-ttu-id="e994d-187">Matplotlib kullanarak hello veri görselleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e994d-187">You can visualize hello data using matplotlib.</span></span> <span data-ttu-id="e994d-188">Bu hello yaş sütunu için bir histogram görüntüler:</span><span class="sxs-lookup"><span data-stu-id="e994d-188">This displays in a histogram for hello age column:</span></span>
    
    ![Çubuk grafik][ipython-histogram]

## <span data-ttu-id="e994d-190"><a name="clientApis"></a>Merhaba Machine Learning Python istemci kitaplığı tooaccess kullanın, okuma, oluşturma ve veri kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="e994d-190"><a name="clientApis"></a>Use hello Machine Learning Python client library tooaccess, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="e994d-191">Çalışma alanı</span><span class="sxs-lookup"><span data-stu-id="e994d-191">Workspace</span></span>
<span data-ttu-id="e994d-192">Merhaba çalışma hello için giriş hello Python istemci kitaplığı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="e994d-192">hello workspace is hello entry point for hello Python client library.</span></span> <span data-ttu-id="e994d-193">Merhaba sağlamak `Workspace` , çalışma alanı kimliği ve yetkilendirme belirteci toocreate ile sınıfının bir örneği:</span><span class="sxs-lookup"><span data-stu-id="e994d-193">Provide hello `Workspace` class with your workspace id and authorization token toocreate an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="e994d-194">Veri kümeleri listeleme</span><span class="sxs-lookup"><span data-stu-id="e994d-194">Enumerate datasets</span></span>
<span data-ttu-id="e994d-195">tooenumerate belirli bir çalışma alanındaki tüm veri kümeleri:</span><span class="sxs-lookup"><span data-stu-id="e994d-195">tooenumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="e994d-196">tooenumerate yalnızca hello veri kümeleri kullanıcı oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="e994d-196">tooenumerate just hello user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="e994d-197">tooenumerate yalnızca hello örnek veri kümeleri:</span><span class="sxs-lookup"><span data-stu-id="e994d-197">tooenumerate just hello example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="e994d-198">Bir veri kümesi (büyük küçük harfe duyarlı) adı tarafından erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e994d-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="e994d-199">Ya da dizin tarafından erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e994d-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="e994d-200">Meta Veriler</span><span class="sxs-lookup"><span data-stu-id="e994d-200">Metadata</span></span>
<span data-ttu-id="e994d-201">Veri kümeleri meta verileri, toplama toocontent sahip.</span><span class="sxs-lookup"><span data-stu-id="e994d-201">Datasets have metadata, in addition toocontent.</span></span> <span data-ttu-id="e994d-202">(Ara veri kümelerini bir özel durum toothis kuralı olan ve meta verileri yok.)</span><span class="sxs-lookup"><span data-stu-id="e994d-202">(Intermediate datasets are an exception toothis rule and do not have any metadata.)</span></span>

<span data-ttu-id="e994d-203">Bazı meta veri değerlerinin hello kullanıcı tarafından oluşturma sırasında atanır:</span><span class="sxs-lookup"><span data-stu-id="e994d-203">Some metadata values are assigned by hello user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="e994d-204">Başkaları tarafından Azure ML atanan değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e994d-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="e994d-205">Merhaba bkz `SourceDataset` sınıfı üzerinde daha fazla hello kullanılabilir meta veriler için.</span><span class="sxs-lookup"><span data-stu-id="e994d-205">See hello `SourceDataset` class for more on hello available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="e994d-206">İçeriğini okuma</span><span class="sxs-lookup"><span data-stu-id="e994d-206">Read contents</span></span>
<span data-ttu-id="e994d-207">Machine Learning Studio tarafından otomatik olarak sağlanan hello kod parçacıkları indirin ve hello dataset tooa Pandas DataFrame nesne seri durumdan.</span><span class="sxs-lookup"><span data-stu-id="e994d-207">hello code snippets provided by Machine Learning Studio automatically download and deserialize hello dataset tooa Pandas DataFrame object.</span></span> <span data-ttu-id="e994d-208">Bu hello ile yapılır `to_dataframe` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="e994d-208">This is done with hello `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="e994d-209">Toodownload hello ham verileri tercih ve hello seri durumdan çıkarma kendiniz gerçekleştirmek istiyorsanız, bir seçenek olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="e994d-209">If you prefer toodownload hello raw data, and perform hello deserialization yourself, that is an option.</span></span> <span data-ttu-id="e994d-210">Merhaba şu anda 'ARFF' hangi hello Python istemci kitaplığı seri durumdan çıkarılamıyor, gibi biçimler için hello tek seçenek budur.</span><span class="sxs-lookup"><span data-stu-id="e994d-210">At hello moment, this is hello only option for formats such as 'ARFF', which hello Python client library cannot deserialize.</span></span>

<span data-ttu-id="e994d-211">metin olarak tooread hello içeriği:</span><span class="sxs-lookup"><span data-stu-id="e994d-211">tooread hello contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="e994d-212">tooread hello içeriğini ikili olarak:</span><span class="sxs-lookup"><span data-stu-id="e994d-212">tooread hello contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="e994d-213">Ayrıca bir akış toohello içeriği açabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e994d-213">You can also just open a stream toohello contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="e994d-214">Yeni bir veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e994d-214">Create a new dataset</span></span>
<span data-ttu-id="e994d-215">Merhaba Python istemci kitaplığı Python programınızdan tooupload veri kümeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e994d-215">hello Python client library allows you tooupload datasets from your Python program.</span></span> <span data-ttu-id="e994d-216">Bu veri kümeleri sonra çalışma alanınızda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e994d-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="e994d-217">Bir Pandas DataFrame verileriniz varsa, kodu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e994d-217">If you have your data in a Pandas DataFrame, use hello following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="e994d-218">Verilerinizi zaten serileştirilmiş, kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e994d-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="e994d-219">Merhaba Python istemci Pandas DataFrame toohello aşağıdaki biçimler mümkün tooserialize kitaplığıdır (sabittir bu hello `azureml.DataTypeIds` sınıfı):</span><span class="sxs-lookup"><span data-stu-id="e994d-219">hello Python client library is able tooserialize a Pandas DataFrame toohello following formats (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="e994d-220">Düz metin</span><span class="sxs-lookup"><span data-stu-id="e994d-220">PlainText</span></span>
* <span data-ttu-id="e994d-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="e994d-221">GenericCSV</span></span>
* <span data-ttu-id="e994d-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="e994d-222">GenericTSV</span></span>
* <span data-ttu-id="e994d-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="e994d-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="e994d-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="e994d-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="e994d-225">Mevcut bir veri kümesini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="e994d-225">Update an existing dataset</span></span>
<span data-ttu-id="e994d-226">Tooupload var olan bir dataset eşleşen bir ada sahip yeni bir veri kümesi çalışırsanız, bir çakışma hatası almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e994d-226">If you try tooupload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="e994d-227">var olan bir dataset tooupdate, önce tooget bir başvuru toohello mevcut veri kümesini gerekir:</span><span class="sxs-lookup"><span data-stu-id="e994d-227">tooupdate an existing dataset, you first need tooget a reference toohello existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="e994d-228">Ardından `update_from_dataframe` azure'da hello dataset tooserialize ve Değiştir hello içeriğini:</span><span class="sxs-lookup"><span data-stu-id="e994d-228">Then use `update_from_dataframe` tooserialize and replace hello contents of hello dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="e994d-229">Tooserialize hello veri tooa farklı biçimi istiyorsanız, isteğe bağlı hello için bir değer belirtin `data_type_id` parametresi.</span><span class="sxs-lookup"><span data-stu-id="e994d-229">If you want tooserialize hello data tooa different format, specify a value for hello optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="e994d-230">Hello için bir değer belirterek isteğe bağlı olarak yeni bir açıklama ayarlayabilirsiniz `description` parametresi.</span><span class="sxs-lookup"><span data-stu-id="e994d-230">You can optionally set a new description by specifying a value for hello `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

<span data-ttu-id="e994d-231">İsteğe bağlı olarak yeni bir ad hello için bir değer belirterek ayarlayabileceğiniz `name` parametresi.</span><span class="sxs-lookup"><span data-stu-id="e994d-231">You can optionally set a new name by specifying a value for hello `name` parameter.</span></span> <span data-ttu-id="e994d-232">Şu andan itibaren yalnızca yeni adı hello kullanarak hello dataset almak.</span><span class="sxs-lookup"><span data-stu-id="e994d-232">From now on, you'll retrieve hello dataset using hello new name only.</span></span> <span data-ttu-id="e994d-233">koddan hello hello verileri, ad ve açıklama güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e994d-233">hello following code updates hello data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="e994d-234">Merhaba `data_type_id`, `name` ve `description` parametreler isteğe bağlıdır ve varsayılan tootheir önceki değer.</span><span class="sxs-lookup"><span data-stu-id="e994d-234">hello `data_type_id`, `name` and `description` parameters are optional and default tootheir previous value.</span></span> <span data-ttu-id="e994d-235">Merhaba `dataframe` parametresi gereklidir her zaman.</span><span class="sxs-lookup"><span data-stu-id="e994d-235">hello `dataframe` parameter is always required.</span></span>

<span data-ttu-id="e994d-236">Verilerinizi zaten serileştirilmiş kullanırsanız `update_from_raw_data` yerine `update_from_dataframe`.</span><span class="sxs-lookup"><span data-stu-id="e994d-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="e994d-237">Yalnızca içinde geçirirseniz `raw_data` yerine `dataframe`, benzer şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="e994d-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

