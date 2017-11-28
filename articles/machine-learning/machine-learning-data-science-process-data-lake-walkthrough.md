---
title: "Azure Data Lake ile ölçeklenebilir veri bilimi: bir uçtan uca kılavuz | Microsoft Docs"
description: "Nasıl bir veri kümesine toouse Azure Data Lake, toodo veri keşfi ve ikili sınıflandırma görevleri."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="0ea6b-103">Azure Data Lake ile ölçeklenebilir veri bilimi: bir uçtan uca gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="0ea6b-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="0ea6b-104">Bu kılavuz bir ipucu tarafından ücreti ödenen olup olmadığını nasıl toouse Azure Data Lake toodo veri keşfi ve ikili sınıflandırma görevleri hello NYC örneği üzerinde seyahat ve ücreti dataset toopredict ücreti gösterir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-104">This walkthrough shows how toouse Azure Data Lake toodo data exploration and binary classification tasks on a sample of hello NYC taxi trip and fare dataset toopredict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="0ea6b-105">Merhaba hello adımlarda size yol gösterir [takım veri bilimi işlemi](http://aka.ms/datascienceprocess), uçtan uca, veri alım toomodel eğitim ve hello modeli yayımlayan bir web hizmeti toohello dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-105">It walks you through hello steps of hello [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition toomodel training, and then toohello deployment of a web service that publishes hello model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="0ea6b-106">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0ea6b-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="0ea6b-107">Merhaba [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) tüm hello özellikleri gerekli toomake sahip Itanium tabanlı sistemler için veri bilimcilerine toostore veri herhangi boyutu, Şekil ve hız ve tooconduct veri analizi ve makine öğrenme modelleme gelişmiş işleme, için kolay, düşük maliyetli bir şekilde yüksek ölçeklenebilirlik ile.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-107">hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all hello capabilities required toomake it easy for data scientists toostore data of any size, shape and speed, and tooconduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="0ea6b-108">Yalnızca veri gerçekte işlenirken bir iş başına temelinde ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="0ea6b-109">Sorgu yetenek Karışımlar bildirim temelli SQL yapısını hello gücüyle C# tooprovide ölçeklenebilir ile Merhaba bir dil dağıtılmış, Azure Data Lake Analytics U-SQL içerir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-109">Azure Data Lake Analytics includes U-SQL, a language that blends hello declarative nature of SQL with hello expressive power of C# tooprovide scalable distributed query capability.</span></span> <span data-ttu-id="0ea6b-110">Tooprocess sağlar üzerinde okuma, şema uygulayarak yapılandırılmamış verileri özel mantık ekleme ve kullanıcı tanımlı işlevler (UDF'ler) ve genişletilebilirlik tooenable ince tanecikli denetime nasıl içerir ölçekte tooexecute.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-110">It enables you tooprocess unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility tooenable fine grained control over how tooexecute at scale.</span></span> <span data-ttu-id="0ea6b-111">U-SQL, arkasında hello tasarımı felsefesi hakkında daha fazla toolearn bkz [Visual Studio blog gönderisi](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="0ea6b-111">toolearn more about hello design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="0ea6b-112">Data Lake Analytics ayrıca Cortana Analytics Suite’in de önemli bir parçasıdır ve Azure SQL Veri Ambarı, Power BI ve Veri Fabrikası ile birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="0ea6b-113">Bu, tam bulut büyük veri ve Gelişmiş analizi platformu sunar.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="0ea6b-114">Bu kılavuzda hello önkoşulları ve toocomplete hello hello veri bilimi işlemi form Data Lake Analytics ile görevleri ve nasıl kaynakları açıklayarak başlar tooinstall bunları.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-114">This walkthrough begins by describing hello prerequisites and resources that are needed toocomplete hello tasks with Data Lake Analytics that form hello data science process and how tooinstall them.</span></span> <span data-ttu-id="0ea6b-115">U-SQL'yi kullanarak hello veri işleme adımlarını özetler ve göstererek sonucuna sonra nasıl toouse Python ve Azure Machine Learning Studio toobuild ile Hive ve hello Tahmine dayalı modelleri dağıtın.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-115">Then it outlines hello data processing steps using U-SQL and concludes by showing how toouse Python and Hive with Azure Machine Learning Studio toobuild and deploy hello predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="0ea6b-116">U-SQL ve Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0ea6b-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="0ea6b-117">Bu kılavuz, Visual Studio tooedit U-SQL betikleri tooprocess hello dataset kullanılmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-117">This walkthrough recommends using Visual Studio tooedit U-SQL scripts tooprocess hello dataset.</span></span> <span data-ttu-id="0ea6b-118">Merhaba U-SQL betikleri ayrı bir dosyaya sağlanan ve burada açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-118">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="0ea6b-119">Merhaba işlem alma, keşfetme ve hello veri örnekleme içerir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-119">hello process includes ingesting, exploring, and sampling hello data.</span></span> <span data-ttu-id="0ea6b-120">Aynı zamanda, nasıl hello Azure portal işten toorun U-SQL Script gösterir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-120">It also shows how toorun a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="0ea6b-121">Hive tablolarını bir ilişkili Hdınsight küme toofacilitate hello yapı ve dağıtım Azure Machine Learning Studio'da bir ikili sınıflandırma modelinin hello veriler için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-121">Hive tables are created for hello data in an associated HDInsight cluster toofacilitate hello building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="0ea6b-122">Python</span><span class="sxs-lookup"><span data-stu-id="0ea6b-122">Python</span></span>
<span data-ttu-id="0ea6b-123">Bu izlenecek yol da gösteren bir bölüm içeren nasıl toobuild ve Python ile Azure Machine Learning Studio kullanarak Tahmine dayalı bir modeli dağıtın.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-123">This walkthrough also contains a section that shows how toobuild and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="0ea6b-124">Jupyter not defteri hello Python komut dosyalarıyla adımları bu işlem için sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-124">We provide a Jupyter notebook with hello Python scripts for these steps in this process.</span></span> <span data-ttu-id="0ea6b-125">Merhaba dizüstü bazı ek özellik Mühendisliği adımları ve modelleri yapım çok sınıflı sınıflandırma ve ayrıca Burada özetlenen toohello ikili sınıflandırma model modelleme regresyon gibi kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-125">hello notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition toohello binary classification model outlined here.</span></span> <span data-ttu-id="0ea6b-126">Merhaba regresyon görev toopredict hello diğer ipucu özelliklerini temel alarak hello ipucu miktarıdır.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-126">hello regression task is toopredict hello amount of hello tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="0ea6b-127">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0ea6b-127">Azure Machine Learning</span></span>
<span data-ttu-id="0ea6b-128">Azure Machine Learning Studio kullanılan toobuild olan ve hello Tahmine dayalı modelleri dağıtın.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-128">Azure Machine Learning Studio is used toobuild and deploy hello predictive models.</span></span> <span data-ttu-id="0ea6b-129">Bu yapılır iki yaklaşım kullanarak: ilk Python komut dosyaları ve ardından ile Hive tablolarını Hdınsight (Hadoop) kümesinde.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="0ea6b-130">Betikler</span><span class="sxs-lookup"><span data-stu-id="0ea6b-130">Scripts</span></span>
<span data-ttu-id="0ea6b-131">Bu kılavuzda yalnızca hello asıl adımları özetlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-131">Only hello principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="0ea6b-132">Merhaba tam indirebilirsiniz **U-SQL betiği** ve **Jupyter not defteri** gelen [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="0ea6b-132">You can download hello full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ea6b-133">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0ea6b-133">Prerequisites</span></span>
<span data-ttu-id="0ea6b-134">Bu konularda başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-134">Before you begin these topics, you must have hello following:</span></span>

* <span data-ttu-id="0ea6b-135">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-135">An Azure subscription.</span></span> <span data-ttu-id="0ea6b-136">Zaten bir yoksa, bkz: [alma Azure ücretsiz deneme sürümü](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="0ea6b-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="0ea6b-137">[Önerilen] Visual Studio 2013 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="0ea6b-138">Zaten yüklü bu sürümlerinden birini yoksa, ücretsiz bir Community sürümü indirebilirsiniz [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span><span class="sxs-lookup"><span data-stu-id="0ea6b-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="0ea6b-139">Visual Studio yerine hello Azure Portal toosubmit Azure Data Lake sorguları de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-139">Instead of Visual Studio, you can also use hello Azure Portal toosubmit Azure Data Lake queries.</span></span> <span data-ttu-id="0ea6b-140">Nasıl toodo şekilde Visual Studio ile ve hello portal hello bölümünde başlıklı üzerindeki yönergeler size sağlayacaktır **işlem U-SQL verilerle**.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-140">We will provide instructions on how toodo so both with Visual Studio and on hello portal in hello section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="0ea6b-141">Azure Data Lake için veri bilimi ortamını hazırlayın</span><span class="sxs-lookup"><span data-stu-id="0ea6b-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="0ea6b-142">tooprepare hello veri bilimi ortamı bu yönlendirme için kaynakları aşağıdaki hello oluşturun:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-142">tooprepare hello data science environment for this walkthrough, create hello following resources:</span></span>

* <span data-ttu-id="0ea6b-143">Azure Data Lake deposu (ADLS)</span><span class="sxs-lookup"><span data-stu-id="0ea6b-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="0ea6b-144">Azure Data Lake Analytics (ADLA)</span><span class="sxs-lookup"><span data-stu-id="0ea6b-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="0ea6b-145">Azure Blob storage hesabı</span><span class="sxs-lookup"><span data-stu-id="0ea6b-145">Azure Blob storage account</span></span>
* <span data-ttu-id="0ea6b-146">Azure Machine Learning Studio hesabı</span><span class="sxs-lookup"><span data-stu-id="0ea6b-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="0ea6b-147">(Önerilen) Visual Studio için Azure Data Lake araçları</span><span class="sxs-lookup"><span data-stu-id="0ea6b-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="0ea6b-148">Bu bölümde hakkında yönergeler sağlar toocreate her bu kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-148">This section provides instructions on how toocreate each of these resources.</span></span> <span data-ttu-id="0ea6b-149">Hive tablolarını Python, toobuild bir model yerine Azure Machine Learning ile toouse seçerseniz tooprovision Hdınsight (Hadoop) kümesi de gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-149">If you choose toouse Hive tables with Azure Machine Learning, instead of Python, toobuild a model,you will also need tooprovision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="0ea6b-150">Bu alternatif yordam hello uygun aşağıdaki bölümde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-150">This alternative procedure in described in hello appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="0ea6b-151">Merhaba **Azure Data Lake Store** ya da ayrı olarak oluşturulabilir veya hello oluşturduğunuzda **Azure Data Lake Analytics** hello varsayılan depolama.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-151">hello **Azure Data Lake Store** can be created either separately or when you create hello **Azure Data Lake Analytics** as hello default storage.</span></span> <span data-ttu-id="0ea6b-152">Her biri ayrı olarak aşağıdaki bu kaynakları oluşturmak için yönergeler başvurulan ancak hello Data Lake storage hesabını ayrı ayrı oluşturmamış.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-152">Instructions are referenced for creating each of these resources separately below, but hello Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="0ea6b-153">Bir Azure Data Lake deposu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="0ea6b-154">Merhaba bir ADLS oluşturma [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ea6b-154">Create an ADLS from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="0ea6b-155">Ayrıntılar için bkz [Azure Portal'ı kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ea6b-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="0ea6b-156">Merhaba hello kümeye özgü AAD kimliği yukarı emin tooset olması **DataSource** hello dikey **isteğe bağlı yapılandırma** dikey açıklanan vardır.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-156">Be sure tooset up hello Cluster AAD Identity in hello **DataSource** blade of hello **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="0ea6b-158">Bir Azure Data Lake Analytics hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="0ea6b-159">Merhaba bir ADLA hesabı oluşturma [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ea6b-159">Create an ADLA account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="0ea6b-160">Ayrıntılar için bkz [Öğreticisi: Azure Data Lake Azure Portal kullanarak Analytics ile çalışmaya başlama](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ea6b-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="0ea6b-162">Bir Azure Blob storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="0ea6b-163">Merhaba bir Azure Blob storage hesabı oluşturma [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ea6b-163">Create an Azure Blob storage account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="0ea6b-164">Merhaba oluşturulur bir depolama hesabı bölümüne Ayrıntılar için bkz [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="0ea6b-164">For details, see hello Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="0ea6b-166">Bir Azure Machine Learning Studio hesap ayarlama</span><span class="sxs-lookup"><span data-stu-id="0ea6b-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="0ea6b-167">Hello/Azure Machine Learning Studio uygulamasına oturum [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) sayfası.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-167">Sign up/into Azure Machine Learning Studio from hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="0ea6b-168">Tıklatın hello üzerinde **hemen kullanmaya başlayın** düğmesine tıklayın ve ardından "Ücretsiz çalışma" veya "Standart çalışma"'i seçin.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-168">Click on hello **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="0ea6b-169">Bundan sonra Azure ML Studio'da mümkün toocreate denemeler olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-169">After this you will be able toocreate experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="0ea6b-170">[Önerilen] Azure Data Lake Araçları'nı yükleme</span><span class="sxs-lookup"><span data-stu-id="0ea6b-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="0ea6b-171">Visual Studio'dan sürümünüz için Azure Data Lake araçları yükleme [Visual Studio için Azure Data Lake Araçları](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="0ea6b-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="0ea6b-173">Merhaba yükleme başarıyla tamamlandıktan sonra Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-173">After hello installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="0ea6b-174">Merhaba Data Lake sekmesi hello menüsü hello üstünde görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-174">You should see hello Data Lake tab hello menu at hello top.</span></span> <span data-ttu-id="0ea6b-175">Azure hesabınızda oturum açtığınızda Azure kaynaklarınızı hello sol panelinde görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-175">Your Azure resources should appear in hello left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a><span data-ttu-id="0ea6b-177">Merhaba NYC ücreti dönüşleri veri kümesi</span><span class="sxs-lookup"><span data-stu-id="0ea6b-177">hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="0ea6b-178">Merhaba veri burada kullandık genel kullanıma açık bir veri kümesi--hello kümesidir [NYC ücreti dönüşleri dataset](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="0ea6b-178">hello data set we used here is a publicly available dataset -- hello [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="0ea6b-179">Merhaba NYC ücreti seyahat veri yaklaşık 20 GB sıkıştırılmış CSV dosyalarının (sıkıştırılmamış ~ 48 GB) oluşan, 173 milyondan fazla kaydı tek tek dönüşleri ve hello fares her seyahat için ücretli.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-179">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="0ea6b-180">Zaman, anonim hale getirilen (sürücü) lisans numarası korsan saldırılarına ve medallion (ücreti'nın benzersiz kimliği) numarası hello ve her seyahat kayıt hello alma ve teslim konumları içerir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-180">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="0ea6b-181">Merhaba veri hello yıl 2013 tüm dönüşleri kapsayan ve her ay için iki veri kümesi aşağıdaki hello sağlanır:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-181">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

* <span data-ttu-id="0ea6b-182">Merhaba 'trip_data' CSV yolcu, toplama ve dropoff noktaları, seyahat süresi ve seyahat Uzunluk sayısı gibi seyahat ayrıntıları içerir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-182">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="0ea6b-183">Birkaç örnek kayıt şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="0ea6b-184">Merhaba 'trip_fare' CSV ödeme türü, ücreti tutarı, ek ücret ve vergileri, ipuçları ve tolls ve Ücretli hello toplam miktarı gibi her seyahat için ücretli hello ücreti ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-184">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="0ea6b-185">Birkaç örnek kayıt şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="0ea6b-186">Merhaba benzersiz anahtar toojoin seyahat\_veri ve seyahat\_ücreti aşağıdaki üç alanı hello oluşur: medallion, korsan\_lisans ve alma\_datetime.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-186">hello unique key toojoin trip\_data and trip\_fare is composed of hello following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="0ea6b-187">Merhaba ham CSV dosyaları ortak Azure storage blobundan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-187">hello raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="0ea6b-188">Bu katılımı hello için U-SQL betiği hello [katılma seyahat ve ücreti tabloları](#join) bölümü.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-188">hello U-SQL script for this join is in hello [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="0ea6b-189">U-SQL ile verileri işleme</span><span class="sxs-lookup"><span data-stu-id="0ea6b-189">Process data with U-SQL</span></span>
<span data-ttu-id="0ea6b-190">Bu bölümde gösterilen hello veri işleme görevlerini alma, kalite denetimi, keşfetme ve hello veri örnekleme içerir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-190">hello data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling hello data.</span></span> <span data-ttu-id="0ea6b-191">Ayrıca gösteriyoruz nasıl toojoin seyahat ve ücreti tabloları.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-191">We also show how toojoin trip and fare tables.</span></span> <span data-ttu-id="0ea6b-192">Merhaba son bölümü hello Azure portalında bir U-SQL komut dosyası işinden çalışma gösterir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-192">hello final section shows run a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="0ea6b-193">Tooeach alt bağlantılar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-193">Here are links tooeach subsection:</span></span>

* [<span data-ttu-id="0ea6b-194">Veri alımı: ortak blob verileri okuma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="0ea6b-195">Veri Kalitesi denetimleri</span><span class="sxs-lookup"><span data-stu-id="0ea6b-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="0ea6b-196">Veri keşfi</span><span class="sxs-lookup"><span data-stu-id="0ea6b-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="0ea6b-197">Seyahat ve ücreti tabloları birleştirme</span><span class="sxs-lookup"><span data-stu-id="0ea6b-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="0ea6b-198">Veri örnekleme</span><span class="sxs-lookup"><span data-stu-id="0ea6b-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="0ea6b-199">U-SQL işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="0ea6b-200">Merhaba U-SQL betikleri ayrı bir dosyaya sağlanan ve burada açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-200">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="0ea6b-201">Merhaba tam indirebilirsiniz **U-SQL betikleri** gelen [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="0ea6b-201">You can download hello full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="0ea6b-202">tooexecute U-SQL, açık Visual Studio tıklatın **Dosya--> Yeni Proje-->**, seçin **U-SQL projesi**, ad ve tooa klasörüne kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-202">tooexecute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it tooa folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="0ea6b-204">Bu, olası toouse hello Azure Portal tooexecute U-SQL Visual Studio yerine olur.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-204">It is possible toouse hello Azure Portal tooexecute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="0ea6b-205">Toohello Azure Data Lake Analytics kaynak hello Portal gidin ve doğrudan olarak aşağıdaki şekilde hello Resimli sorguları göndermek.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-205">You can navigate toohello Azure Data Lake Analytics resource on hello portal and submit queries directly as illustrated in hello following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="0ea6b-207"><a name="ingest"></a>Veri alımı: ortak blob verileri okuyun</span><span class="sxs-lookup"><span data-stu-id="0ea6b-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="0ea6b-208">hello Azure blob hello verilerde Hello konumu olarak başvurulur  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  ve kullanarak ayıklanabilir **Extractors.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-208">hello location of hello data in hello Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="0ea6b-209">Kendi kapsayıcı adı ve depolama hesabı adı için aşağıdaki komut yerine container_name@blob_storage_account_name hello wasb adresi.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in hello wasb address.</span></span> <span data-ttu-id="0ea6b-210">Merhaba dosya adları aynı biçimde olduğundan, biz kullanabilirsiniz **seyahat\_veri_ {\*\}.csv** tüm 12 seyahat dosyalarında tooread.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-210">Since hello file names are in same format, we can use **trip\_data_{\*\}.csv** tooread in all 12 trip files.</span></span> 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

<span data-ttu-id="0ea6b-211">Merhaba ilk satırda üstbilgileri olduğundan, biz tooremove hello üstbilgileri gerekir ve uygun parçalara sütun türleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-211">Since there are headers in hello first row, we need tooremove hello headers and change column types into appropriate ones.</span></span> <span data-ttu-id="0ea6b-212">İşlenen hello tooAzure Data Lake Storage kullanarak verileri kaydetme ya da geçebiliriz **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ veya tooAzure Blob Depolama hesabı kullanarak  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** .</span><span class="sxs-lookup"><span data-stu-id="0ea6b-212">We can either save hello processed data tooAzure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or tooAzure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="0ea6b-213">Benzer şekilde biz hello ücreti veri kümelerinde okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-213">Similarly we can read in hello fare data sets.</span></span> <span data-ttu-id="0ea6b-214">Azure Data Lake Store sağ tıklatın ve verilerinize toolook seçebilirsiniz **Azure Portal--> Veri Gezgini** veya **dosya Gezgini** Visual Studio içinde.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-214">Right click Azure Data Lake Store, you can choose toolook at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="0ea6b-217"><a name="quality"></a>Veri Kalitesi denetimleri</span><span class="sxs-lookup"><span data-stu-id="0ea6b-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="0ea6b-218">Seyahat ve ücreti tabloları içinde okunduktan sonra veri kalite denetimleri yolu izleyerek hello yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-218">After trip and fare tables have been read in, data quality checks can be done in hello following way.</span></span> <span data-ttu-id="0ea6b-219">CSV dosyaları kaynaklanan hello çıktı tooAzure Blob storage veya Azure Data Lake Store olabilir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-219">hello resulting CSV files can be output tooAzure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="0ea6b-220">Merhaba medallions, benzersiz sayısını ve medallions bulun:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-220">Find hello number of medallions and unique number of medallions:</span></span>

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="0ea6b-221">100'den fazla dönüşleri vardı bu medallions bulun:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="0ea6b-222">Geçersiz kayıtların pickup_longitude bakımından bulun:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="0ea6b-223">Eksik değerleri için bazı değişkenler bulun:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-223">Find missing values for some variables:</span></span>

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="0ea6b-224"><a name="explore"></a>Veri keşfi</span><span class="sxs-lookup"><span data-stu-id="0ea6b-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="0ea6b-225">Daha iyi anlamasına yardımcı hello veri bazı veri araştırması tooget yapabiliriz.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-225">We can do some data exploration tooget a better understanding of hello data.</span></span>

<span data-ttu-id="0ea6b-226">Eğimli ve eğimli olmayan dönüşleri Hello dağıtımını bulun:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-226">Find hello distribution of tipped and non-tipped trips:</span></span>

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="0ea6b-227">İpucu tutar sonlandırma değerlerle Hello dağıtımını bulun: 0,5,10 ve 20 dolar.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-227">Find hello distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="0ea6b-228">Seyahat uzaklığı temel istatistiklerinin bulun:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-228">Find basic statistics of trip distance:</span></span>

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="0ea6b-229">Seyahat uzaklığı, Hello yüzdebirlik değeri Bul:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-229">Find hello percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="0ea6b-230"><a name="join"></a>Seyahat ve ücreti tabloları birleştirme</span><span class="sxs-lookup"><span data-stu-id="0ea6b-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="0ea6b-231">Seyahat ve ücreti tabloları medallion, hack_license ve pickup_time tarafından katılabilir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="0ea6b-232">Her yolcu sayısı düzeyi için hello sayısı kayıtları, ortalama ipucu tutar, ipucu tutar varyansını, Eğimli dönüşleri yüzdesini hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-232">For each level of passenger count, calculate hello number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="0ea6b-233"><a name="sample"></a>Veri örnekleme</span><span class="sxs-lookup"><span data-stu-id="0ea6b-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="0ea6b-234">İlk biz rastgele %0,1 hello veri hello birleştirilmiş tablosundan seçin:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-234">First we randomly select 0.1% of hello data from hello joined table:</span></span>

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="0ea6b-235">Ardından biz stratified örnekleme tarafından ikili değişken tip_class yapın:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="0ea6b-236"><a name="run"></a>U-SQL işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="0ea6b-237">U-SQL betikleri düzenlemeyi tamamladığınızda, Azure Data Lake Analytics hesabınızı kullanarak toohello sunucu gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-237">When you finish editing U-SQL scripts, you can submit them toohello server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="0ea6b-238">Tıklatın **Data Lake**, **işi Gönder**seçin, **Analytics hesabı**, seçin **paralellik**, tıklatıp **Gönder**  düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="0ea6b-240">Merhaba işi başarıyla derlendiğini, izleme için Visual Studio'da işinizin hello durumu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-240">When hello job is complied successfully, hello status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="0ea6b-241">Hello işi çalışması bittikten sonra hello bulma iş verimliliğinizi adımları tooimprove bottleneck ve hatta yeniden yürütme hello iş yürütme işlemi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-241">After hello job finishes running, you can even replay hello job execution process and find out hello bottleneck steps tooimprove your job efficiency.</span></span> <span data-ttu-id="0ea6b-242">TooAzure Portal toocheck hello U-SQL işlerinizin durumunu de gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-242">You can also go tooAzure Portal toocheck hello status of your U-SQL jobs.</span></span>

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="0ea6b-245">Artık Azure Blob storage veya Azure Portalı'nda hello çıktı dosyaları kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-245">Now you can check hello output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="0ea6b-246">Bizim modelleme hello sonraki adımda için stratified hello örnek verileri kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-246">We will use hello stratified sample data for our modeling in hello next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="0ea6b-249">Derleme ve Azure Machine Learning modellerini dağıtma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="0ea6b-250">Biz için iki seçenek kullanılabilir toopull verileri Azure Machine Learning toobuild içine göstermek ve</span><span class="sxs-lookup"><span data-stu-id="0ea6b-250">We demonstrate two options available for you toopull data into Azure Machine Learning toobuild and</span></span> 

* <span data-ttu-id="0ea6b-251">Merhaba ilk seçeneğinde tooan Azure Blob yazılmış hello örneklenen verileri kullanın (Merhaba içinde **veri örnekleme** Yukarıdaki adımı) ve Python toobuild kullanabilir ve Azure Machine Learning modelinden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-251">In hello first option, you use hello sampled data that has been written tooan Azure Blob (in hello **Data sampling** step above) and use Python toobuild and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="0ea6b-252">Hello ikinci seçenekte, doğrudan bir Hive sorgusu kullanarak Azure Data Lake hello verilerde sorgu.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-252">In hello second option, you query hello data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="0ea6b-253">Bu seçenek, yeni bir Hdınsight kümesi oluşturma veya mevcut bir Hdınsight kümesine burada Azure Data Lake Storage noktası toohello NY ücreti verileri hello Hive tabloları kullanın gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where hello Hive tables point toohello NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="0ea6b-254">Biz, hem bu seçenekler aşağıda ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a><span data-ttu-id="0ea6b-255">Seçenek 1: Kullanım Python toobuild ve makine öğrenimi modellerini dağıtma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-255">Option 1: Use Python toobuild and deploy machine learning models</span></span>
<span data-ttu-id="0ea6b-256">toobuild ve Python kullanarak makine öğrenimi modellerini dağıtmak, yerel makinenizde veya Azure Machine Learning Studio'da Jupyter not defteri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-256">toobuild and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="0ea6b-257">Merhaba Jupyter not defteri sağlanan [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) içeren tam kod tooexplore Merhaba, verileri, özellik Mühendisliği, model ve dağıtım görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-257">hello Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains hello full code tooexplore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="0ea6b-258">Bu makalede, yalnızca hello modelleme ve dağıtım gösterir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-258">In this article, we show just hello modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="0ea6b-259">Python kitaplıkları içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-259">Import Python libraries</span></span>
<span data-ttu-id="0ea6b-260">Jupyter not defteri Sipariş toorun hello örnek veya Python komut dosyası Merhaba, hello aşağıdaki Python paketlerini gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-260">In order toorun hello sample Jupyter Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="0ea6b-261">Merhaba AzureML Not Defteri hizmeti kullanıyorsanız, bu paketleri önceden yüklenmiş olmuştur.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-261">If you are using hello AzureML Notebook service, these packages have been pre-installed.</span></span>

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
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a><span data-ttu-id="0ea6b-262">Blob hello verileri okuma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-262">Read in hello data from blob</span></span>
* <span data-ttu-id="0ea6b-263">Bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="0ea6b-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="0ea6b-264">Metin olarak okuyun</span><span class="sxs-lookup"><span data-stu-id="0ea6b-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="0ea6b-266">Sütun adları eklemek ve ayrı sütunlar</span><span class="sxs-lookup"><span data-stu-id="0ea6b-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="0ea6b-267">Bazı sütunları toonumeric değiştirme</span><span class="sxs-lookup"><span data-stu-id="0ea6b-267">Change some columns toonumeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="0ea6b-268">Machine learning modellerini Derleme</span><span class="sxs-lookup"><span data-stu-id="0ea6b-268">Build machine learning models</span></span>
<span data-ttu-id="0ea6b-269">Burada bir seyahat veya eğimli olup olmadığını biz ikili sınıflandırma modeli toopredict oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-269">Here we build a binary classification model toopredict whether a trip is tipped or not.</span></span> <span data-ttu-id="0ea6b-270">Merhaba Jupyter Not Defteri, diğer iki modeli bulabilirsiniz: çok sınıflı sınıflandırma ve regresyon modeli.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-270">In hello Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="0ea6b-271">İlk scikit kullanılabilir toocreate kukla değişkenleri ihtiyacımız-modelleri öğrenin</span><span class="sxs-lookup"><span data-stu-id="0ea6b-271">First we need toocreate dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="0ea6b-272">Merhaba modelleme için veri çerçeve oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-272">Create data frame for hello modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="0ea6b-273">Eğitim ve 60-40 bölünmüş test etme</span><span class="sxs-lookup"><span data-stu-id="0ea6b-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="0ea6b-274">Eğitim kümesindeki Lojistik regresyon</span><span class="sxs-lookup"><span data-stu-id="0ea6b-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="0ea6b-275">Sınama veri kümesi puan</span><span class="sxs-lookup"><span data-stu-id="0ea6b-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="0ea6b-276">Değerlendirme ölçümleri Hesapla</span><span class="sxs-lookup"><span data-stu-id="0ea6b-276">Calculate Evaluation metrics</span></span>
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="0ea6b-277">Web hizmeti API'si derleme ve Python içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="0ea6b-278">Model, oluşturulduktan sonra öğrenme toooperationalize hello makine istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-278">We want toooperationalize hello machine learning model after it has been built.</span></span> <span data-ttu-id="0ea6b-279">Burada hello ikili Lojistik modeli örnek olarak kullanırız.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-279">Here we use hello binary logistic model as an example.</span></span> <span data-ttu-id="0ea6b-280">Merhaba scikit emin olun-yerel makinenize sürümünde 0.15.1 olduğunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-280">Make sure hello scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="0ea6b-281">Azure ML studio hizmeti kullanıyorsanız, bu konuda tooworry yok.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-281">You don't have tooworry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="0ea6b-282">Çalışma alanı kimlik bilgileriniz Azure ML studio ayarlarından bulun.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="0ea6b-283">Azure Machine Learning Studio'da tıklatın **ayarları** --> **adı** --> **yetkilendirme belirteçleri**.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![C3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="0ea6b-285">Web hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="0ea6b-286">Web hizmeti kimlik bilgileri alma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="0ea6b-287">Web hizmeti API'sine çağırın.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-287">Call Web service API.</span></span> <span data-ttu-id="0ea6b-288">Toowait 5-10 saniye sonra hello önceki adıma sahip.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-288">You have toowait 5-10 seconds after hello previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="0ea6b-289">Seçenek 2: Oluşturma ve Azure Machine Learning modellerini doğrudan dağıtma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="0ea6b-290">Azure Machine Learning Studio verileri doğrudan Azure Data Lake Deposu'ndan veri okuyabilir ve ardından kullanılan toocreate olması ve modelleri dağıtın.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used toocreate and deploy models.</span></span> <span data-ttu-id="0ea6b-291">Bu yaklaşım hello Azure Data Lake Store işaret eden bir Hive tablosu kullanır.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-291">This approach uses a Hive table that points at hello Azure Data Lake Store.</span></span> <span data-ttu-id="0ea6b-292">Bu ayrı bir Azure Hdınsight kümesi sağlanması gerekiyorsa, hangi hello Hive tablosu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-292">This requires that a separate Azure HDInsight cluster be provisioned, on which hello Hive table is created.</span></span> <span data-ttu-id="0ea6b-293">bölümler Göster nasıl aşağıdaki hello toodo bu.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-293">hello following sections show how toodo this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="0ea6b-294">Hdınsight Linux kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="0ea6b-295">Hdınsight kümesi (Linux) hello oluşturmak [Azure Portal](http://portal.azure.com). Merhaba Ayrıntılar için bkz **erişim tooAzure Data Lake Store ile bir Hdınsight kümesi oluşturmayı** bölümüne [Azure Portal'ı kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ea6b-295">Create an HDInsight Cluster (Linux) from hello [Azure Portal](http://portal.azure.com).For details, see hello **Create an HDInsight cluster with access tooAzure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="0ea6b-297">Hdınsight'ta Hive tablosu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="0ea6b-298">Artık Azure Machine Learning Studio'da hello önceki adımda Azure Data Lake Store'da depolanan hello verileri kullanarak hello Hdınsight kümesinde kullanılan Hive tabloları toobe oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-298">Now we create Hive tables toobe used in Azure Machine Learning Studio in hello HDInsight cluster using hello data stored in Azure Data Lake Store in hello previous step.</span></span> <span data-ttu-id="0ea6b-299">Yeni oluşturduğunuz Hdınsight kümesi toohello gidin.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-299">Go toohello HDInsight cluster just created.</span></span> <span data-ttu-id="0ea6b-300">Tıklatın **ayarları** --> **özellikleri** --> **küme AAD kimlik** --> **ADLS erişimini**, Azure Data Lake Store hesabınızı okuma hello listesinde eklendiğinden emin olun, yazma ve yürütme hakları.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in hello list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="0ea6b-302">Ardından **Pano** sonraki toohello **ayarları** düğmesi ve bir pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-302">Then click **Dashboard** next toohello **Settings** button and a window will pop up.</span></span> <span data-ttu-id="0ea6b-303">Tıklatın **Hive görünümü** hello hello sayfa ve sağ üst köşesindeki hello görürsünüz **sorgu Düzenleyicisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-303">Click **Hive View** in hello upper right corner of hello page and you will see hello **Query Editor**.</span></span>

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="0ea6b-306">Hive betikleri toocreate aşağıdaki hello tablo yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-306">Paste in hello following Hive scripts toocreate a table.</span></span> <span data-ttu-id="0ea6b-307">veri kaynağının Hello konumdur bu şekilde Azure Data Lake Store başvurusu: **adl://data_lake_store_name.azuredatalakestore.net:443/klasör_adı/dosya_adı**.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-307">hello location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


<span data-ttu-id="0ea6b-308">Merhaba sorgu çalışması sona erdiğinde, hello sonuçlar şöyle görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-308">When hello query finishes running, you will see hello results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="0ea6b-310">Derleme ve Azure Machine Learning Studio'da modelleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="0ea6b-311">Biz hazır toobuild sunulmuştur ve Azure Machine Learning ile bir ipucu Ücretli olsun veya olmasın tahmin modeli dağıtın.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-311">We are now ready toobuild and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="0ea6b-312">Merhaba stratified örnek veri olduğundan bu ikili sınıflandırma kullanılan hazır toobe (veya ipucu) sorun.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-312">hello stratified sample data is ready toobe used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="0ea6b-313">çok sınıflı sınıflandırma (tip_class) kullanarak Tahmine dayalı modelleri hello ve regresyon (tip_amount) ayrıca oluşturulmuş ve Azure Machine Learning Studio ile dağıtılır, ancak burada yalnızca nasıl toohandle hello örneği kullanarak izin ver hello ikili sınıflandırma modeli gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-313">hello predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how toohandle hello case using hello binary classification model.</span></span>

1. <span data-ttu-id="0ea6b-314">Azure hello kullanarak ML Hello Veri Al **veri içeri aktarma** modülü, hello kullanılabilir **veri giriş ve çıkış** bölümü.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-314">Get hello data into Azure ML using hello **Import Data** module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="0ea6b-315">Daha fazla bilgi için bkz: Merhaba [veri içeri aktarma modülü](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) başvuru sayfası.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-315">For more information, see hello [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="0ea6b-316">Seçin **Hive sorgusu** hello olarak **veri kaynağı** hello içinde **özellikleri** paneli.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-316">Select **Hive Query** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="0ea6b-317">Merhaba Hive betiği aşağıdaki Yapıştır hello **Hive veritabanı sorgusu** Düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="0ea6b-317">Paste hello following Hive script in hello **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="0ea6b-318">Merhaba URI, Hdınsight kümesi (Bu Azure Portalı'nda bulunabilir), Hadoop kimlik bilgileri, çıktı verilerini Azure depolama hesabı anahtarı/ad/kapsayıcı adı ve konumu girin.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-318">Enter hello URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="0ea6b-320">Hive tablodan veri okunurken bir ikili sınıflandırma deneme örneği hello aşağıdaki çizimde gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-320">An example of a binary classification experiment reading data from Hive table is shown in hello figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="0ea6b-322">Merhaba deneme oluşturulduktan sonra tıklatın **Web hizmetinin ayarı** --> **Tahmine dayalı Web hizmeti**</span><span class="sxs-lookup"><span data-stu-id="0ea6b-322">After hello experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="0ea6b-324">Tamamlandığında, deneme, Puanlama otomatik olarak oluşturulan çalışma hello tıklatın **Web hizmeti Dağıt**</span><span class="sxs-lookup"><span data-stu-id="0ea6b-324">Run hello automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="0ea6b-326">Merhaba web hizmeti Pano kısa süre içinde görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-326">hello web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="0ea6b-328">Özet</span><span class="sxs-lookup"><span data-stu-id="0ea6b-328">Summary</span></span>
<span data-ttu-id="0ea6b-329">Bu kılavuzu izleyerek Azure Data Lake içinde ölçeklenebilir uçtan uca çözümler oluşturmak için bir veri bilimi ortamı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="0ea6b-330">Bu ortamı kullanılan tooanalyze hello veri bilimi işlemi, veri alım model eğitim üzerinden gelen, hello kurallı adımlarında alma büyük ortak bir dataset, ve ardından hello toohello dağıtımını model bir web hizmeti olarak.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-330">This environment was used tooanalyze a large public dataset, taking it through hello canonical steps of hello Data Science Process, from data acquisition through model training, and then toohello deployment of hello model as a web service.</span></span> <span data-ttu-id="0ea6b-331">U-SQL kullanılan tooprocess oluştu, araştırın ve hello veri örneği.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-331">U-SQL was used tooprocess, explore and sample hello data.</span></span> <span data-ttu-id="0ea6b-332">Python ve Hive Azure Machine Learning Studio toobuild ile kullanılan ve Tahmine dayalı modelleri dağıtın.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-332">Python and Hive were used with Azure Machine Learning Studio toobuild and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="0ea6b-333">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="0ea6b-333">What's next?</span></span>
<span data-ttu-id="0ea6b-334">öğrenme yolu için hello [takım veri bilimi işlem (TDSP)](http://aka.ms/datascienceprocess) Bağlantılar tootopics her açıklayan adım analytics işlem Gelişmiş hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="0ea6b-334">hello learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links tootopics describing each step in hello advanced analytics process.</span></span> <span data-ttu-id="0ea6b-335">İzlenecek yollar üzerinde hello dökümü bir dizi vardır [takım veri bilimi süreci gözden geçirmeleri](data-science-process-walkthroughs.md) bu gösterim nasıl sayfa toouse kaynakları ve çeşitli Tahmine dayalı analiz senaryolarda Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="0ea6b-335">There are a series of walkthroughs itemized on hello [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how toouse resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="0ea6b-336">eylemin Hello takım veri bilimi işlemi: SQL Data Warehouse kullanma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-336">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="0ea6b-337">eylemin Hello takım veri bilimi işlemi: Hdınsight Hadoop kümeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-337">hello Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="0ea6b-338">Merhaba takım veri bilimi işlem: SQL Server kullanma</span><span class="sxs-lookup"><span data-stu-id="0ea6b-338">hello Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="0ea6b-339">Azure Hdınsight'ta Spark veri bilimi işlemi hello kullanma konusuna genel bakış</span><span class="sxs-lookup"><span data-stu-id="0ea6b-339">Overview of hello Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

