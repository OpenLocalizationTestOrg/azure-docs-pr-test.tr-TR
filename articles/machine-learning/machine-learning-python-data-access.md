---
title: "Machine Learning Python istemci kitaplığı veri kümeleriyle erişim | Microsoft Docs"
description: "Yükleyin ve Python istemci kitaplığı erişmek ve Azure Machine Learning veri bir yerel Python ortamından güvenli bir şekilde yönetmek için kullanın."
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
ms.openlocfilehash: e3ae712e0f8d386f637520fbbff4b348bc86f32d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="access-datasets-with-python-using-the-azure-machine-learning-python-client-library"></a><span data-ttu-id="231de-103">Azure Machine Learning Python istemci kitaplığını kullanarak Python ile veri kümelerine erişim</span><span class="sxs-lookup"><span data-stu-id="231de-103">Access datasets with Python using the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="231de-104">Microsoft Azure Machine Learning Python istemci kitaplığı önizlemesini güvenli erişim Azure Machine Learning veri kümeleriniz için bir yerel Python ortamından etkinleştirebilir ve oluşturulması ve bir çalışma alanı kümelerinde yönetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="231de-104">The preview of Microsoft Azure Machine Learning Python client library can enable secure access to your Azure Machine Learning datasets from a local Python environment and enables the creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="231de-105">Bu konu hakkında yönergeler sağlar:</span><span class="sxs-lookup"><span data-stu-id="231de-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="231de-106">Machine Learning Python istemci Kitaplığı'nı yüklemek</span><span class="sxs-lookup"><span data-stu-id="231de-106">install the Machine Learning Python client library</span></span> 
* <span data-ttu-id="231de-107">erişim ve Azure Machine Learning veri kümelerini yerel Python ortamınızdan erişme yetkisi almak yönergeler de dahil olmak üzere veri kümeleri, karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="231de-107">access and upload datasets, including instructions on how to get authorization to access Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="231de-108">denemeler ara veri kümeleri erişim</span><span class="sxs-lookup"><span data-stu-id="231de-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="231de-109">veri kümeleri listeleme, meta verilerine erişmek, bir veri kümesi içeriğini okumak, yeni veri kümeleri oluşturma ve mevcut veri kümelerini güncelleştirmek için Python istemci kitaplığını kullanma</span><span class="sxs-lookup"><span data-stu-id="231de-109">use the Python client library to enumerate datasets, access metadata, read the contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="231de-110"><a name="prerequisites"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="231de-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="231de-111">Python istemci kitaplığı altında aşağıdaki ortamları test edilmiştir:</span><span class="sxs-lookup"><span data-stu-id="231de-111">The Python client library has been tested under the following environments:</span></span>

* <span data-ttu-id="231de-112">Windows, Mac ve Linux</span><span class="sxs-lookup"><span data-stu-id="231de-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="231de-113">Python 2.7, 3.3 ve 3.4</span><span class="sxs-lookup"><span data-stu-id="231de-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="231de-114">Bunu, aşağıdaki paketleri bir bağımlılığa sahiptir:</span><span class="sxs-lookup"><span data-stu-id="231de-114">It has a dependency on the following packages:</span></span>

* <span data-ttu-id="231de-115">istekleri</span><span class="sxs-lookup"><span data-stu-id="231de-115">requests</span></span>
* <span data-ttu-id="231de-116">Python dateutil</span><span class="sxs-lookup"><span data-stu-id="231de-116">python-dateutil</span></span>
* <span data-ttu-id="231de-117">pandas</span><span class="sxs-lookup"><span data-stu-id="231de-117">pandas</span></span>

<span data-ttu-id="231de-118">Bir Python dağıtımı gibi kullanmanızı öneririz [Anaconda](http://continuum.io/downloads#all) veya [Kanopi](https://store.enthought.com/downloads/), Python, IPython gelen ve yukarıda listelenen üç paketleri yüklü.</span><span class="sxs-lookup"><span data-stu-id="231de-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and the three packages listed above installed.</span></span> <span data-ttu-id="231de-119">IPython kesinlikle gerekli olmamakla birlikte, düzenleme ve etkileşimli olarak verileri görselleştirmek için harika bir ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="231de-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="231de-120"><a name="installation"></a>Azure Machine Learning Python istemci kitaplığı yükleme</span><span class="sxs-lookup"><span data-stu-id="231de-120"><a name="installation"></a>How to install the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="231de-121">Bu konuda açıklanan görevleri tamamlamak için ayrıca Azure Machine Learning Python istemci kitaplığı yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="231de-121">The Azure Machine Learning Python client library must also be installed to complete the tasks outlined in this topic.</span></span> <span data-ttu-id="231de-122">Kullanılabilir [Python paket dizini](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="231de-122">It is available from the [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="231de-123">Python ortamınızda yüklemek için yerel Python ortamınızdan aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="231de-123">To install it in your Python environment, run the following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="231de-124">Alternatif olarak, indirin ve kaynaklardan yüklemek [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="231de-124">Alternatively, you can download and install from the sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="231de-125">Makinenizde git varsa, doğrudan git deposundan yüklemek için PIP kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="231de-125">If you have git installed on your machine, you can use pip to install directly from the git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="231de-126"><a name="datasetAccess"></a>Veri kümeleri erişmek için Studio kod parçacıklarını kullanma</span><span class="sxs-lookup"><span data-stu-id="231de-126"><a name="datasetAccess"></a>Use Studio Code snippets to access datasets</span></span>
<span data-ttu-id="231de-127">Python istemci kitaplığı programlı erişim çalıştırılmış denemeler, var olan veri kümelerine sağlar.</span><span class="sxs-lookup"><span data-stu-id="231de-127">The Python client library gives you programmatic access to your existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="231de-128">Studio web arabiriminden indirmek ve veri kümeleri konumu makinenizde Pandas DataFrame nesne olarak seri durumdan için gerekli tüm bilgileri içeren kod parçacıkları oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="231de-128">From the Studio web interface, you can generate code snippets that include all the necessary information to download and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="231de-129"><a name="security"></a>Veri erişimi için güvenlik</span><span class="sxs-lookup"><span data-stu-id="231de-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="231de-130">Python istemci kitaplığı ile kullanmak üzere çalışma alanı kimliği ve yetkilendirme içerir Studio tarafından sağlanan kod parçacıkları belirteci.</span><span class="sxs-lookup"><span data-stu-id="231de-130">The code snippets provided by Studio for use with the Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="231de-131">Bu çalışma alanınıza tam erişim sağlamak ve parola gibi korunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="231de-131">These provide full access to your workspace and must be protected, like a password.</span></span>

<span data-ttu-id="231de-132">Güvenlik nedenleriyle, kod parçacığı işlevleri yalnızca yap rollerine sahip kullanıcılar için kullanılabilir **sahibi** çalışma alanı için.</span><span class="sxs-lookup"><span data-stu-id="231de-132">For security reasons, the code snippet functionality is only available to users that have their role set as **Owner** for the workspace.</span></span> <span data-ttu-id="231de-133">Azure Machine Learning Studio'da gösterilir rolünüze **kullanıcılar** altında sayfa **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="231de-133">Your role is displayed in Azure Machine Learning Studio on the **USERS** page under **Settings**.</span></span>

![Güvenlik][security]

<span data-ttu-id="231de-135">Rolünüze olarak ayarlanmamışsa **sahibi**, ya da istek sahibi olarak ortamına yeniden davet edilme veya kod parçacığı ile sağlamak için çalışma alanının sahibi sormak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="231de-135">If your role is not set as **Owner**, you can either request to be reinvited as an owner, or ask the owner of the workspace to provide you with the code snippet.</span></span>

<span data-ttu-id="231de-136">Yetkilendirme belirteci edinmek için aşağıdakilerden birini yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="231de-136">To obtain the authorization token, you can do one of the following:</span></span>

* <span data-ttu-id="231de-137">Bir belirteci için bir sahibinden isteyin.</span><span class="sxs-lookup"><span data-stu-id="231de-137">Ask for a token from an owner.</span></span> <span data-ttu-id="231de-138">Sahipleri kendi yetkilendirme belirteçleri Studio'da kendi çalışma alanı ayarları sayfasından erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="231de-138">Owners can access their authorization tokens from the Settings page of their workspace in Studio.</span></span> <span data-ttu-id="231de-139">Seçin **ayarları** tıklatın ve sol bölmede **YETKİLENDİRME BELİRTEÇLERİ** birincil ve ikincil belirteçleri görmek için.</span><span class="sxs-lookup"><span data-stu-id="231de-139">Select **Settings** from the left pane and click **AUTHORIZATION TOKENS** to see the primary and secondary tokens.</span></span>  <span data-ttu-id="231de-140">Birincil veya ikincil yetkilendirme belirteçleri kod parçacığında kullanılabilse de sahipleri yalnızca ikincil yetkilendirme belirteçleri paylaşıma önerilir.</span><span class="sxs-lookup"><span data-stu-id="231de-140">Although either the primary or the secondary authorization tokens can be used in the code snippet, it is recommended that owners only share the secondary authorization tokens.</span></span>

![Yetkilendirme belirteçleri](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="231de-142">Sahibi rolüne Yükseltilecek isteyin.</span><span class="sxs-lookup"><span data-stu-id="231de-142">Ask to be promoted to role of owner.</span></span>  <span data-ttu-id="231de-143">Bunu yapmak için geçerli bir çalışma alanı sahibi ilk çalışma alanından kaldırın sonra ona bir sahibi olarak yeniden davet gerekir.</span><span class="sxs-lookup"><span data-stu-id="231de-143">To do this, a current owner of the workspace needs to first remove you from the workspace then re-invite you to it as an owner.</span></span>

<span data-ttu-id="231de-144">Geliştiriciler çalışma alanı kimliği ve yetkilendirme aldıktan sonra belirteç, bunlar bağımsız olarak kendi rolleri kod parçacığını kullanarak çalışma erişebilir.</span><span class="sxs-lookup"><span data-stu-id="231de-144">Once developers have obtained the workspace id and authorization token, they are able to access the workspace using the code snippet regardless of their role.</span></span>

<span data-ttu-id="231de-145">Yetkilendirme belirteçleri yönetilir **YETKİLENDİRME BELİRTEÇLERİ** altında sayfa **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="231de-145">Authorization tokens are managed on the **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="231de-146">Bunları yeniden oluşturabilirsiniz, ancak bu yordamı olan önceki belirtece erişimi iptal eder.</span><span class="sxs-lookup"><span data-stu-id="231de-146">You can regenerate them, but this procedure revokes access to the previous token.</span></span>

### <span data-ttu-id="231de-147"><a name="accessingDatasets"></a>Yerel bir Python uygulama erişim veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="231de-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="231de-148">Machine Learning Studio'da tıklatın **veri KÜMELERİ** sol gezinti çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="231de-148">In Machine Learning Studio, click **DATASETS** in the navigation bar on the left.</span></span>
2. <span data-ttu-id="231de-149">Erişmek istediğiniz veri kümesini seçin.</span><span class="sxs-lookup"><span data-stu-id="231de-149">Select the dataset you would like to access.</span></span> <span data-ttu-id="231de-150">Veri kümeleri birini seçebilirsiniz **MY veri KÜMELERİ** listesi veya **örnekleri** listesi.</span><span class="sxs-lookup"><span data-stu-id="231de-150">You can select any of the datasets from the **MY DATASETS** list or from the **SAMPLES** list.</span></span>
3. <span data-ttu-id="231de-151">Alt araç çubuğundan tıklatın **veri erişim kodu oluştur**.</span><span class="sxs-lookup"><span data-stu-id="231de-151">From the bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="231de-152">Verileri Python istemci kitaplığı ile uyumlu bir biçimde ise, bu düğmesi devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="231de-152">If the data is in a format incompatible with the Python client library, this button is disabled.</span></span>
   
    ![Veri kümeleri][datasets]
4. <span data-ttu-id="231de-154">Kod parçacığı görünür ve panonuza kopyalayın penceresinden seçin.</span><span class="sxs-lookup"><span data-stu-id="231de-154">Select the code snippet from the window that appears and copy it to your clipboard.</span></span>
   
    ![Erişim kodu][dataset-access-code]
5. <span data-ttu-id="231de-156">Kodu yerel Python uygulamanızı not defterinize yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="231de-156">Paste the code into the notebook of your local Python application.</span></span>
   
    ![Not Defteri][ipython-dataset]

## <span data-ttu-id="231de-158"><a name="accessingIntermediateDatasets"></a>Machine Learning denemelerini ara veri kümeleri erişim</span><span class="sxs-lookup"><span data-stu-id="231de-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="231de-159">Bir denemeyi Machine Learning Studio'da çalıştırıldıktan sonra Ara veri kümeleri modülleri çıkış düğümlerdeki erişmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="231de-159">After an experiment is run in the Machine Learning Studio, it is possible to access the intermediate datasets from the output nodes of modules.</span></span> <span data-ttu-id="231de-160">Ara veri kümeleri oluşturulan ve model aracı çalıştırdığınızda ara adımlar için kullanılan verilerdir.</span><span class="sxs-lookup"><span data-stu-id="231de-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="231de-161">Veri biçimi Python istemci kitaplığı ile uyumlu olduğu sürece ara veri kümeleri erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="231de-161">Intermediate datasets can be accessed as long as the data format is compatible with the Python client library.</span></span>

<span data-ttu-id="231de-162">Aşağıdaki biçimler desteklenir (Bu sabittir içinde `azureml.DataTypeIds` sınıfı):</span><span class="sxs-lookup"><span data-stu-id="231de-162">The following formats are supported (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="231de-163">Düz metin</span><span class="sxs-lookup"><span data-stu-id="231de-163">PlainText</span></span>
* <span data-ttu-id="231de-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="231de-164">GenericCSV</span></span>
* <span data-ttu-id="231de-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="231de-165">GenericTSV</span></span>
* <span data-ttu-id="231de-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="231de-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="231de-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="231de-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="231de-168">Modül çıkış düğüm üzerinde gelerek biçimi belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="231de-168">You can determine the format by hovering over a module output node.</span></span> <span data-ttu-id="231de-169">Düğüm adı bir araç ipucu ile birlikte görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="231de-169">It is displayed along with the node name, in a tooltip.</span></span>

<span data-ttu-id="231de-170">Bazı modüller gibi [bölünmüş] [ split] adlı bir biçimde çıktı modülü `Dataset`, Python istemci kitaplığı tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="231de-170">Some of the modules, such as the [Split][split] module, output to a format named `Dataset`, which is not supported by the Python client library.</span></span>

![Veri kümesi biçimi][dataset-format]

<span data-ttu-id="231de-172">Dönüştürme modülü gibi kullanmanıza gerek [CSV'ye Dönüştür][convert-to-csv], bir çıktı biçimi desteklenen bir biçime almak için.</span><span class="sxs-lookup"><span data-stu-id="231de-172">You need to use a conversion module, such as [Convert to CSV][convert-to-csv], to get an output into a supported format.</span></span>

![GenericCSV biçimi][csv-format]

<span data-ttu-id="231de-174">Aşağıdaki adımlar, bir deneme oluşturur, çalıştırır ve Ara dataset erişen bir örnek gösterir.</span><span class="sxs-lookup"><span data-stu-id="231de-174">The following steps show an example that creates an experiment, runs it and accesses the intermediate dataset.</span></span>

1. <span data-ttu-id="231de-175">Yeni bir deneme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="231de-175">Create a new experiment.</span></span>
2. <span data-ttu-id="231de-176">INSERT bir **yetişkin Census gelir ikili sınıflandırma dataset** modülü.</span><span class="sxs-lookup"><span data-stu-id="231de-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="231de-177">INSERT bir [bölünmüş] [ split] modülü ve kendi giriş veri kümesi modülü çıktıya bağlanın.</span><span class="sxs-lookup"><span data-stu-id="231de-177">Insert a [Split][split] module, and connect its input to the dataset module output.</span></span>
4. <span data-ttu-id="231de-178">INSERT bir [CSV'ye Dönüştür] [ convert-to-csv] modülü ve kendi giriş birine bağlanın [bölünmüş] [ split] modülü çıkarır.</span><span class="sxs-lookup"><span data-stu-id="231de-178">Insert a [Convert to CSV][convert-to-csv] module and connect its input to one of the [Split][split] module outputs.</span></span>
5. <span data-ttu-id="231de-179">Denemeyi kaydedin, çalıştırmak ve çalışan bitmesini bekleyin.</span><span class="sxs-lookup"><span data-stu-id="231de-179">Save the experiment, run it, and wait for it to finish running.</span></span>
6. <span data-ttu-id="231de-180">Çıktı düğümü tıklatın [CSV'ye Dönüştür] [ convert-to-csv] modülü.</span><span class="sxs-lookup"><span data-stu-id="231de-180">Click the output node on the [Convert to CSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="231de-181">Bağlam menüsü görüntülendiğinde seçin **veri erişim kodu oluştur**.</span><span class="sxs-lookup"><span data-stu-id="231de-181">When the context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Bağlam menüsü][experiment]
8. <span data-ttu-id="231de-183">Kod parçacığı seçin ve görüntülenen penceresinden panonuza kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="231de-183">Select the code snippet and copy it to your clipboard from the window that appears.</span></span>
   
    ![Erişim kodu][intermediate-dataset-access-code]
9. <span data-ttu-id="231de-185">Kodu defterinizde yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="231de-185">Paste the code in your notebook.</span></span>
   
    ![Not Defteri][ipython-intermediate-dataset]
10. <span data-ttu-id="231de-187">Matplotlib kullanarak verileri Görselleştir.</span><span class="sxs-lookup"><span data-stu-id="231de-187">You can visualize the data using matplotlib.</span></span> <span data-ttu-id="231de-188">Bu yaş sütunu için bir histogram görüntüler:</span><span class="sxs-lookup"><span data-stu-id="231de-188">This displays in a histogram for the age column:</span></span>
    
    ![Çubuk grafik][ipython-histogram]

## <span data-ttu-id="231de-190"><a name="clientApis"></a>Erişim, okuma, oluşturma ve veri kümelerini yönetmek için makine öğrenme Python istemci kitaplığını kullanma</span><span class="sxs-lookup"><span data-stu-id="231de-190"><a name="clientApis"></a>Use the Machine Learning Python client library to access, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="231de-191">Çalışma alanı</span><span class="sxs-lookup"><span data-stu-id="231de-191">Workspace</span></span>
<span data-ttu-id="231de-192">Çalışma alanı Python istemci kitaplığı için giriş noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="231de-192">The workspace is the entry point for the Python client library.</span></span> <span data-ttu-id="231de-193">Sağlamak `Workspace` sınıfı çalışma alanı kimliği ve yetkilendirme belirteci örnek oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="231de-193">Provide the `Workspace` class with your workspace id and authorization token to create an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="231de-194">Veri kümeleri listeleme</span><span class="sxs-lookup"><span data-stu-id="231de-194">Enumerate datasets</span></span>
<span data-ttu-id="231de-195">Belirli bir çalışma alanı tüm veri kümelerinin numaralandırmak için:</span><span class="sxs-lookup"><span data-stu-id="231de-195">To enumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="231de-196">Yalnızca kullanıcı tarafından oluşturulan veri kümelerinin numaralandırmak için:</span><span class="sxs-lookup"><span data-stu-id="231de-196">To enumerate just the user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="231de-197">Yalnızca örnek veri kümeleri numaralandırmak için:</span><span class="sxs-lookup"><span data-stu-id="231de-197">To enumerate just the example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="231de-198">Bir veri kümesi (büyük küçük harfe duyarlı) adı tarafından erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="231de-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="231de-199">Ya da dizin tarafından erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="231de-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="231de-200">Meta Veriler</span><span class="sxs-lookup"><span data-stu-id="231de-200">Metadata</span></span>
<span data-ttu-id="231de-201">Veri kümeleri içerik yanı sıra meta veriler bulunur.</span><span class="sxs-lookup"><span data-stu-id="231de-201">Datasets have metadata, in addition to content.</span></span> <span data-ttu-id="231de-202">(Ara veri kümeleri bu kural için bir özel durumdur ve meta verileri yok.)</span><span class="sxs-lookup"><span data-stu-id="231de-202">(Intermediate datasets are an exception to this rule and do not have any metadata.)</span></span>

<span data-ttu-id="231de-203">Bazı meta veri değerleri, oluşturma sırasında kullanıcı tarafından atanır:</span><span class="sxs-lookup"><span data-stu-id="231de-203">Some metadata values are assigned by the user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="231de-204">Başkaları tarafından Azure ML atanan değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="231de-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="231de-205">Bkz: `SourceDataset` kullanılabilir meta veriler hakkında daha fazla bilgi için sınıf.</span><span class="sxs-lookup"><span data-stu-id="231de-205">See the `SourceDataset` class for more on the available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="231de-206">İçeriğini okuma</span><span class="sxs-lookup"><span data-stu-id="231de-206">Read contents</span></span>
<span data-ttu-id="231de-207">Machine Learning Studio tarafından otomatik olarak sağlanan kod parçacıkları indirin ve Pandas DataFrame nesne kümesine seri durumdan.</span><span class="sxs-lookup"><span data-stu-id="231de-207">The code snippets provided by Machine Learning Studio automatically download and deserialize the dataset to a Pandas DataFrame object.</span></span> <span data-ttu-id="231de-208">Bu gerçekleştirilir `to_dataframe` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="231de-208">This is done with the `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="231de-209">Ham verileri indirmek ve seri durumundan kendiniz gerçekleştirmek tercih ederseniz, bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="231de-209">If you prefer to download the raw data, and perform the deserialization yourself, that is an option.</span></span> <span data-ttu-id="231de-210">Şu anda Python istemci kitaplığı seri durumdan çıkarılamıyor'ARFF ' gibi biçimler için tek seçenek budur.</span><span class="sxs-lookup"><span data-stu-id="231de-210">At the moment, this is the only option for formats such as 'ARFF', which the Python client library cannot deserialize.</span></span>

<span data-ttu-id="231de-211">Metin olarak içeriği okunamıyor:</span><span class="sxs-lookup"><span data-stu-id="231de-211">To read the contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="231de-212">İçeriği ikili olarak okumak için:</span><span class="sxs-lookup"><span data-stu-id="231de-212">To read the contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="231de-213">Ayrıca bir akış içeriğine açabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="231de-213">You can also just open a stream to the contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="231de-214">Yeni bir veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="231de-214">Create a new dataset</span></span>
<span data-ttu-id="231de-215">Python istemci kitaplığı veri kümeleri Python programınızdan yüklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="231de-215">The Python client library allows you to upload datasets from your Python program.</span></span> <span data-ttu-id="231de-216">Bu veri kümeleri sonra çalışma alanınızda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="231de-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="231de-217">Bir Pandas DataFrame verileriniz varsa, aşağıdaki kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="231de-217">If you have your data in a Pandas DataFrame, use the following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="231de-218">Verilerinizi zaten serileştirilmiş, kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="231de-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="231de-219">Python istemci kitaplığı Pandas DataFrame aşağıdaki biçimlerden için seri hale getiremiyor (Bu sabittir içinde `azureml.DataTypeIds` sınıfı):</span><span class="sxs-lookup"><span data-stu-id="231de-219">The Python client library is able to serialize a Pandas DataFrame to the following formats (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="231de-220">Düz metin</span><span class="sxs-lookup"><span data-stu-id="231de-220">PlainText</span></span>
* <span data-ttu-id="231de-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="231de-221">GenericCSV</span></span>
* <span data-ttu-id="231de-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="231de-222">GenericTSV</span></span>
* <span data-ttu-id="231de-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="231de-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="231de-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="231de-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="231de-225">Mevcut bir veri kümesini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="231de-225">Update an existing dataset</span></span>
<span data-ttu-id="231de-226">Var olan bir dataset eşleşen bir ada sahip yeni bir veri kümesi yüklemeye çalışırsanız bir çakışma hatası almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="231de-226">If you try to upload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="231de-227">Mevcut bir veri kümesini güncelleştirmek için önce mevcut veri kümesini başvuru almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="231de-227">To update an existing dataset, you first need to get a reference to the existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="231de-228">Ardından `update_from_dataframe` seri hale getirmek ve Azure veri kümesine içeriğini değiştirmek için:</span><span class="sxs-lookup"><span data-stu-id="231de-228">Then use `update_from_dataframe` to serialize and replace the contents of the dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="231de-229">Farklı bir biçime verilerini seri hale getirmek istiyorsanız, isteğe bağlı için bir değer belirtin `data_type_id` parametresi.</span><span class="sxs-lookup"><span data-stu-id="231de-229">If you want to serialize the data to a different format, specify a value for the optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="231de-230">İsteğe bağlı olarak yeni bir açıklama için bir değer belirterek ayarlayabileceğiniz `description` parametresi.</span><span class="sxs-lookup"><span data-stu-id="231de-230">You can optionally set a new description by specifying a value for the `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up to feb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to feb 2015'

<span data-ttu-id="231de-231">İsteğe bağlı olarak yeni bir ad için bir değer belirterek ayarlayabileceğiniz `name` parametresi.</span><span class="sxs-lookup"><span data-stu-id="231de-231">You can optionally set a new name by specifying a value for the `name` parameter.</span></span> <span data-ttu-id="231de-232">Şu andan itibaren yalnızca yeni bir ad kullanarak dataset almak.</span><span class="sxs-lookup"><span data-stu-id="231de-232">From now on, you'll retrieve the dataset using the new name only.</span></span> <span data-ttu-id="231de-233">Aşağıdaki kod, verileri, ad ve açıklama güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="231de-233">The following code updates the data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up to feb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up to feb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="231de-234">`data_type_id`, `name` Ve `description` parametreler isteğe bağlıdır ve varsayılan önceki değerlerine.</span><span class="sxs-lookup"><span data-stu-id="231de-234">The `data_type_id`, `name` and `description` parameters are optional and default to their previous value.</span></span> <span data-ttu-id="231de-235">`dataframe` Parametresi gereklidir her zaman.</span><span class="sxs-lookup"><span data-stu-id="231de-235">The `dataframe` parameter is always required.</span></span>

<span data-ttu-id="231de-236">Verilerinizi zaten serileştirilmiş kullanırsanız `update_from_raw_data` yerine `update_from_dataframe`.</span><span class="sxs-lookup"><span data-stu-id="231de-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="231de-237">Yalnızca içinde geçirirseniz `raw_data` yerine `dataframe`, benzer şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="231de-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

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

