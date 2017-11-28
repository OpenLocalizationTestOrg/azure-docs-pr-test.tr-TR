---
title: "Azure Hdınsight Hadoop kümesi 1 TB veri kümesinde kullanarak eylem - Hello takım veri bilimi işlemi | Microsoft Docs"
description: "Bir Hdınsight Hadoop kullanan bir uçtan uca senaryo için Hello takım veri bilimi işlemi kullanarak toobuild küme ve bir büyük (1 TB) genel kullanıma açık veri kümesini kullanarak bir model dağıtma"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="f7efc-103">Azure Hdınsight Hadoop kümesi 1 TB veri kümesinde kullanarak eylem - Hello takım veri bilimi işlemi</span><span class="sxs-lookup"><span data-stu-id="f7efc-103">hello Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="f7efc-104">Bu kılavuzda, biz kullanarak gösteren bir uçtan uca senaryoda takım veri bilimi işlemi hello bir [Azure Hdınsight Hadoop kümesi](https://azure.microsoft.com/services/hdinsight/) toostore, keşfetme, özellik mühendislik ve aşağı hello birinden örnek verileri genel olarak kullanılabilir [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) veri kümeleri.</span><span class="sxs-lookup"><span data-stu-id="f7efc-104">In this walkthrough, we demonstrate using hello Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data from one of hello publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="f7efc-105">Bu veriler üzerinde Azure Machine Learning toobuild ikili sınıflandırma modeli kullanırız.</span><span class="sxs-lookup"><span data-stu-id="f7efc-105">We use Azure Machine Learning toobuild a binary classification model on this data.</span></span> <span data-ttu-id="f7efc-106">Nasıl toopublish bunlardan birini bir Web hizmeti olarak modelleri de gösterir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-106">We also show how toopublish one of these models as a Web service.</span></span>

<span data-ttu-id="f7efc-107">Ayrıca, bir IPython not defteri tooaccomplish hello görevler bu kılavuzda sunulan olası toouse unutulmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented in this walkthrough.</span></span> <span data-ttu-id="f7efc-108">Bu yaklaşım başvurun tootry gibi hello kullanıcılar [Criteo izlenecek bir Hive ODBC bağlantısı kullanarak](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) konu.</span><span class="sxs-lookup"><span data-stu-id="f7efc-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="f7efc-109"><a name="dataset"></a>Criteo Dataset açıklaması</span><span class="sxs-lookup"><span data-stu-id="f7efc-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="f7efc-110">Merhaba yaklaşık 370 GB sıkıştırılmış gzip TSV dosyaları (~1.3TB sıkıştırılmamış), bir tıklatın tahmin dataset verilerdir Criteo 4.3 milyardan fazla kayıtları kapsayan.</span><span class="sxs-lookup"><span data-stu-id="f7efc-110">hello Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="f7efc-111">24 gün gerçekleştirilecek tarafından kullanılabilir duruma verileri tıklatın [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="f7efc-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="f7efc-112">Veri bilimcilerine Hello kolaylık sağlamak için şu veri kullanılabilir toous tooexperiment ile sıkıştırması açılmış.</span><span class="sxs-lookup"><span data-stu-id="f7efc-112">For hello convenience of data scientists, we have unzipped data available toous tooexperiment with.</span></span>

<span data-ttu-id="f7efc-113">Bu veri kümesi her bir kayıtta 40 sütunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="f7efc-114">Merhaba ilk sütundur kullanıcı olup olmadığını belirten bir etiket sütunu bir **ekleme** (değer 1) veya bir (0 değeri) tıklatın değil</span><span class="sxs-lookup"><span data-stu-id="f7efc-114">hello first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="f7efc-115">sonraki 13 sütunları sayısal, ve</span><span class="sxs-lookup"><span data-stu-id="f7efc-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="f7efc-116">Son 26 kategorik sütunlar:</span><span class="sxs-lookup"><span data-stu-id="f7efc-116">last 26 are categorical columns</span></span>

<span data-ttu-id="f7efc-117">Merhaba sütunları gizlidir ve bir dizi numaralandırılmış adları kullanın: (için hello etiket sütun) "Col1" çok ' Col40 "(Merhaba son Kategorik bir sütun için).</span><span class="sxs-lookup"><span data-stu-id="f7efc-117">hello columns are anonymized and use a series of enumerated names: "Col1" (for hello label column) too'Col40" (for hello last categorical column).</span></span>            

<span data-ttu-id="f7efc-118">İşte hello bir alıntı ilk 20 sütunlarının bu veri kümesine ilişkin iki gözlem (satır):</span><span class="sxs-lookup"><span data-stu-id="f7efc-118">Here is an excerpt of hello first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="f7efc-119">Bu veri kümesi içinde her iki hello sayısal ve kategorik sütunlarında eksik değerleri vardır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-119">There are missing values in both hello numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="f7efc-120">Biz hello eksik değerleri işlemek için basit bir yöntem açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-120">We describe a simple method for handling hello missing values.</span></span> <span data-ttu-id="f7efc-121">Biz Hive tablolara depoladığınızda hello verilerin ek ayrıntılarını incelediniz.</span><span class="sxs-lookup"><span data-stu-id="f7efc-121">Additional details of hello data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="f7efc-122">**Tanımı:** *geçişli tıklatma oranı (Ctrl):* bu hello hello verilerdeki tıklama yüzdesidir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-122">**Definition:** *Clickthrough rate (CTR):* This is hello percentage of clicks in hello data.</span></span> <span data-ttu-id="f7efc-123">Bu Criteo kümesinde yaklaşık %3.3 veya 0.033 hello CTRL değil.</span><span class="sxs-lookup"><span data-stu-id="f7efc-123">In this Criteo dataset, hello CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="f7efc-124"><a name="mltasks"></a>Tahmin görev örnekleri</span><span class="sxs-lookup"><span data-stu-id="f7efc-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="f7efc-125">İki örnek tahmin sorunların bu kılavuzda ele alınmıştır:</span><span class="sxs-lookup"><span data-stu-id="f7efc-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="f7efc-126">**İkili sınıflandırma**: kullanıcı ekleme tıklattınız olup olmadığını tahmin:</span><span class="sxs-lookup"><span data-stu-id="f7efc-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="f7efc-127">Sınıfı 0: Hiçbir tıklatın</span><span class="sxs-lookup"><span data-stu-id="f7efc-127">Class 0: No Click</span></span>
   * <span data-ttu-id="f7efc-128">Sınıf 1:'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="f7efc-128">Class 1: Click</span></span>
2. <span data-ttu-id="f7efc-129">**Regresyon**: kullanıcı özelliklerinden bir reklam tıklatma hello olasılığını tahmin eder.</span><span class="sxs-lookup"><span data-stu-id="f7efc-129">**Regression**: Predicts hello probability of an ad click from user features.</span></span>

## <span data-ttu-id="f7efc-130"><a name="setup"></a>Veri bilimi için ayarlanmış yukarı bir Hdınsight Hadoop kümesi</span><span class="sxs-lookup"><span data-stu-id="f7efc-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="f7efc-131">**Not:** genellikle budur bir **yönetici** görev.</span><span class="sxs-lookup"><span data-stu-id="f7efc-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="f7efc-132">Üç adımda Hdınsight kümeleri ile Tahmine dayalı analiz çözümleri oluşturmak için Azure veri bilimi ortamınızı ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="f7efc-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="f7efc-133">[Depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md): kullanılan toostore verileri Azure Blob Depolama bu depolama hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used toostore data in Azure Blob Storage.</span></span> <span data-ttu-id="f7efc-134">Hdınsight kümelerinde kullanılan hello verileri burada depolanır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-134">hello data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="f7efc-135">[Azure Hdınsight Hadoop kümeleri için veri bilimi özelleştirme](machine-learning-data-science-customize-hadoop-cluster.md): Bu adım, 64-bit Anaconda Python 2.7 tüm düğümlerde yüklü olan bir Azure Hdınsight Hadoop kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f7efc-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="f7efc-136">Merhaba Hdınsight kümesi özelleştirirken iki önemli adımlar (Bu konuda açıklanan) toocomplete vardır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-136">There are two important steps (described in this topic) toocomplete when customizing hello HDInsight cluster.</span></span>
   
   * <span data-ttu-id="f7efc-137">Merhaba depolama hesabı oluşturulduğunda, Hdınsight kümesi ile 1. adımda oluşturulan bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-137">You must link hello storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="f7efc-138">Bu depolama hesabı hello küme içinde işlenebilecek verilerine erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-138">This storage account is used for accessing data that can be processed within hello cluster.</span></span>
   * <span data-ttu-id="f7efc-139">Oluşturulduktan sonra uzaktan erişim toohello hello küme baş düğümüne etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-139">You must enable Remote Access toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="f7efc-140">Burada belirttiğiniz (Merhaba küme oluşturma sırasında belirtilen kullanılanlardan farklı) başlangıç uzaktan erişim kimlik bilgilerini Hatırla: toocomplete gereksinim hello yordamlar.</span><span class="sxs-lookup"><span data-stu-id="f7efc-140">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them toocomplete hello following procedures.</span></span>
3. <span data-ttu-id="f7efc-141">[Azure ML çalışma alanı oluşturma](machine-learning-create-workspace.md): Bu Azure Machine Learning çalışma alanı, sonra ilk veri keşfi ve örnekleme hello Hdınsight kümesinde aşağı makine öğrenimi modellerini oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on hello HDInsight cluster.</span></span>

## <span data-ttu-id="f7efc-142"><a name="getdata"></a>Alma ve ortak bir kaynaktan verileri kullanma</span><span class="sxs-lookup"><span data-stu-id="f7efc-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="f7efc-143">Merhaba [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset erişilebilir hello bağlantıyı tıklatmak hello kullanım koşullarını kabul ederek ve sağlayan bir adı.</span><span class="sxs-lookup"><span data-stu-id="f7efc-143">hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on hello link, accepting hello terms of use, and providing a name.</span></span> <span data-ttu-id="f7efc-144">Bunun nasıl göründüğünü, bir anlık görüntüsünü burada gösterilir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-144">A snapshot of what this looks like is shown here:</span></span>

![Criteo koşullarını kabul edin](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="f7efc-146">Tıklatın **devam tooDownload** tooread hello dataset ve onun kullanılabilirliği hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="f7efc-146">Click **Continue tooDownload** tooread more about hello dataset and its availability.</span></span>

<span data-ttu-id="f7efc-147">Hello verilerin bulunduğu bir ortak [Azure blob depolama](../storage/blobs/storage-dotnet-how-to-use-blobs.md) konumu: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="f7efc-147">hello data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="f7efc-148">Merhaba "wasb" tooAzure Blob depolama konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-148">hello "wasb" refers tooAzure Blob Storage location.</span></span> 

1. <span data-ttu-id="f7efc-149">Bu ortak blob depolama birimindeki Hello veri sıkıştırması açılmış veri üç alt oluşur.</span><span class="sxs-lookup"><span data-stu-id="f7efc-149">hello data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="f7efc-150">alt hello *ham/sayısı/* hello ilk 21 günlük verilerini - gün içeren\_00 tooday\_20</span><span class="sxs-lookup"><span data-stu-id="f7efc-150">hello subfolder *raw/count/* contains hello first 21 days of data - from day\_00 tooday\_20</span></span>
   2. <span data-ttu-id="f7efc-151">alt hello *ham/train/* verileri tek bir gününü oluşur gün\_21</span><span class="sxs-lookup"><span data-stu-id="f7efc-151">hello subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="f7efc-152">alt hello *ham/test/* iki günlük veri oluşur gün\_22 ve günü\_23</span><span class="sxs-lookup"><span data-stu-id="f7efc-152">hello subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="f7efc-153">Kişiler için hello ham gzip verilerle toostart istediğiniz, bu da hello ana klasörde bulunan *ham /* burada NN gider 00 too23 day_NN.gz olarak.</span><span class="sxs-lookup"><span data-stu-id="f7efc-153">For those who want toostart with hello raw gzip data, these are also available in hello main folder *raw/* as day_NN.gz, where NN goes from 00 too23.</span></span>

<span data-ttu-id="f7efc-154">Bir alternatif bir yaklaşım tooaccess keşfedin ve yerel yüklemeleri biz Hive tablolarını oluşturduğunuzda, daha sonra bu kılavuzda açıklanan gerektirmez bu veri modeli.</span><span class="sxs-lookup"><span data-stu-id="f7efc-154">An alternative approach tooaccess, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="f7efc-155"><a name="login"></a>Toohello küme headnode oturum</span><span class="sxs-lookup"><span data-stu-id="f7efc-155"><a name="login"></a>Log in toohello cluster headnode</span></span>
<span data-ttu-id="f7efc-156">Merhaba kümenin kullanım hello toohello headnode toolog [Azure portal](https://ms.portal.azure.com) toolocate hello küme.</span><span class="sxs-lookup"><span data-stu-id="f7efc-156">toolog in toohello headnode of hello cluster, use hello [Azure portal](https://ms.portal.azure.com) toolocate hello cluster.</span></span> <span data-ttu-id="f7efc-157">Sol hello Hello Hdınsight elephant simgesine tıklayın ve sonra kümenizi hello adına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-157">Click hello HDInsight elephant icon on hello left and then double-click hello name of your cluster.</span></span> <span data-ttu-id="f7efc-158">Toohello gidin **yapılandırma** sekmesinde hello sayfanın hello hello BAĞLAN simgesine çift tıklayın ve istendiğinde, uzaktan erişim kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="f7efc-158">Navigate toohello **Configuration** tab, double-click hello CONNECT icon on hello bottom of hello page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="f7efc-159">Bu toohello headnode hello kümesinin götürür.</span><span class="sxs-lookup"><span data-stu-id="f7efc-159">This takes you toohello headnode of hello cluster.</span></span>

<span data-ttu-id="f7efc-160">İşte toohello küme headnode tipik ilk günlüğüne benzer:</span><span class="sxs-lookup"><span data-stu-id="f7efc-160">Here is what a typical first log in toohello cluster headnode looks like:</span></span>

![İçinde toocluster oturum](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="f7efc-162">Merhaba solda hello "Hadoop komutu hello veri keşfi için bizim workhorse satırı" bakın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-162">On hello left, we see hello "Hadoop Command Line", which is our workhorse for hello data exploration.</span></span> <span data-ttu-id="f7efc-163">Biz de iki yararlı URL'leri - "Hadoop Yarn durumu" ve "Hadoop adı düğümü" bakın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="f7efc-164">Merhaba yarn durum URL İş ilerleme durumunu gösterir ve hello adı düğümü URL'si hello küme yapılandırmasına ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-164">hello yarn status URL shows job progress and hello name node URL gives details on hello cluster configuration.</span></span>

<span data-ttu-id="f7efc-165">Şimdi biz ayarlanır ve hazır toobegin ilk bölümü hello izlenecek yol: Hive kullanarak ve Azure Machine Learning için verileri hazırlığı veri keşfi.</span><span class="sxs-lookup"><span data-stu-id="f7efc-165">Now we are set up and ready toobegin first part of hello walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="f7efc-166"><a name="hive-db-tables"></a>Hive veritabanı ve tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="f7efc-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="f7efc-167">toocreate Hive tabloları bizim Criteo veri kümesi için açık hello ***Hadoop komut satırı*** üzerinde hello Masaüstü hello baş düğümü ve hello komutunu girerek hello Hive dizini girin</span><span class="sxs-lookup"><span data-stu-id="f7efc-167">toocreate Hive tables for our Criteo dataset, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="f7efc-168">Tüm Hive komutları bu kılavuzda hello Hive Kutusu'ndan Çalıştır / directory istemi.</span><span class="sxs-lookup"><span data-stu-id="f7efc-168">Run all Hive commands in this walkthrough from hello Hive bin/ directory prompt.</span></span> <span data-ttu-id="f7efc-169">Bu alan yol sorunları otomatik olarak dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f7efc-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="f7efc-170">"Hive dizin istemi" Merhaba terimleri kullanırız "Hive bin / directory istemi" ve "Hadoop komut satırı" birbirinin yerine.</span><span class="sxs-lookup"><span data-stu-id="f7efc-170">We use hello terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="f7efc-171">tooexecute herhangi Hive sorgusu komutları aşağıdaki hello her zaman kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f7efc-171">tooexecute any Hive query, one can always use hello following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="f7efc-172">Hive REPL Hello sonra görünür bir "hive >" oturum, yalnızca kesme ve yapıştırma hello sorgu tooexecute onu.</span><span class="sxs-lookup"><span data-stu-id="f7efc-172">After hello Hive REPL appears with a "hive >"sign, simply cut and paste hello query tooexecute it.</span></span>

<span data-ttu-id="f7efc-173">Merhaba aşağıdaki kod bir veritabanı "criteo" oluşturur ve 4 tablolar oluşturur:</span><span class="sxs-lookup"><span data-stu-id="f7efc-173">hello following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="f7efc-174">bir *sayıları oluşturmak için tablo* gün gününde yerleşik\_00 tooday\_20,</span><span class="sxs-lookup"><span data-stu-id="f7efc-174">a *table for generating counts* built on days day\_00 tooday\_20,</span></span>
* <span data-ttu-id="f7efc-175">bir *tren dataset hello olarak kullanım için tablo* günü yerleşik\_21, ve</span><span class="sxs-lookup"><span data-stu-id="f7efc-175">a *table for use as hello train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="f7efc-176">iki *test tabloları hello olarak kullanmak için veri kümeleri* günü yerleşik\_22 ve günü\_23 sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="f7efc-176">two *tables for use as hello test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="f7efc-177">Biz test kümemize iki farklı tabloya hello gün birini tatil olduğundan ve tatil ve tatil olmayan arasındaki farklar hello geçişli tıklatma kurundan hello modeli algılarsa toodetermine istiyoruz bölün.</span><span class="sxs-lookup"><span data-stu-id="f7efc-177">We split our test dataset into two different tables because one of hello days is a holiday, and we want toodetermine if hello model can detect differences between a holiday and non-holiday from hello clickthrough rate.</span></span>

<span data-ttu-id="f7efc-178">Merhaba betik [örnek &#95; hive & #95 oluşturun; &#95; criteo &#95; veritabanı &#95; ve &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) kolaylık sağlamak için burada görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-178">hello script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

<span data-ttu-id="f7efc-179">Bu tablolar biz yalnızca noktası tooAzure Blob Storage (wasb) konumları dış olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-179">We note that all these tables are external as we simply point tooAzure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="f7efc-180">**Şimdi Bahsediyor iki yolu tooexecute herhangi Hive sorgusu vardır.**</span><span class="sxs-lookup"><span data-stu-id="f7efc-180">**There are two ways tooexecute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="f7efc-181">**Merhaba Hive REPL komut satırı kullanarak**: hello ilk tooissue bir "hive" komutunu ve kopyalama ve bir sorgu Hive REPL komut satırı hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-181">**Using hello Hive REPL command-line**: hello first is tooissue a "hive" command and copy and paste a query at hello Hive REPL command-line.</span></span> <span data-ttu-id="f7efc-182">toodo bunu yapın:</span><span class="sxs-lookup"><span data-stu-id="f7efc-182">toodo this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="f7efc-183">Merhaba sorgu Hello REPL komut satırı kesme ve yapıştırma şimdi yürütür.</span><span class="sxs-lookup"><span data-stu-id="f7efc-183">Now at hello REPL command-line, cutting and pasting hello query executes it.</span></span>
2. <span data-ttu-id="f7efc-184">**Kaydetme sorgular tooa dosya ve hello komutu yürütülürken**: hello ikinci dosyasıdır toosave hello sorguları tooa .hql ([örnek &#95; hive & #95 oluşturun; &#95; criteo &#95; veritabanı &#95; ve &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) ve ardından sorunu hello aşağıdaki tooexecute hello sorgu komutu:</span><span class="sxs-lookup"><span data-stu-id="f7efc-184">**Saving queries tooa file and executing hello command**: hello second is toosave hello queries tooa .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue hello following command tooexecute hello query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="f7efc-185">Veritabanı ve tablo oluşturma onaylayın</span><span class="sxs-lookup"><span data-stu-id="f7efc-185">Confirm database and table creation</span></span>
<span data-ttu-id="f7efc-186">Ardından, biz hello veritabanını hello oluşturmayı hello Hive Kutusu'ndan komutu aşağıdaki hello doğrulatın / directory istemi:</span><span class="sxs-lookup"><span data-stu-id="f7efc-186">Next, we confirm hello creation of hello database with hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="f7efc-187">Bu sunar:</span><span class="sxs-lookup"><span data-stu-id="f7efc-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="f7efc-188">Bu hello yeni veritabanı "criteo" Merhaba oluşturulmasını doğrular.</span><span class="sxs-lookup"><span data-stu-id="f7efc-188">This confirms hello creation of hello new database, "criteo".</span></span>

<span data-ttu-id="f7efc-189">toosee oluşturduğumuz, hangi tabloları biz yalnızca hello komutu burada hello Hive Kutusu'ndan yürütün / directory istemi:</span><span class="sxs-lookup"><span data-stu-id="f7efc-189">toosee what tables we created, we simply issue hello command here from hello Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="f7efc-190">Biz ardından çıktı aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="f7efc-190">We then see hello following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="f7efc-191"><a name="exploration"></a>Veri keşfi kovanında</span><span class="sxs-lookup"><span data-stu-id="f7efc-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="f7efc-192">Biz artık toodo bazı temel veri keşfi kovanında hazır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-192">Now we are ready toodo some basic data exploration in Hive.</span></span> <span data-ttu-id="f7efc-193">Biz hello tren örneklerde hello sayısı sayım tarafından başlamak ve veri tabloları sınayın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-193">We begin by counting hello number of examples in hello train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="f7efc-194">Tren örnek sayısı</span><span class="sxs-lookup"><span data-stu-id="f7efc-194">Number of train examples</span></span>
<span data-ttu-id="f7efc-195">Merhaba içeriğine [örnek &#95; hive &#95; sayısı &#95; eğitimi &#95; Tablo &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) burada gösterilir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-195">hello contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="f7efc-196">Bu verir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="f7efc-197">Alternatif olarak, biri de hello Hive Kutusu'ndan komutu aşağıdaki hello verebileceği / directory istemi:</span><span class="sxs-lookup"><span data-stu-id="f7efc-197">Alternatively, one may also issue hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a><span data-ttu-id="f7efc-198">Test örnekleri hello iki test kümelerindeki sayısı</span><span class="sxs-lookup"><span data-stu-id="f7efc-198">Number of test examples in hello two test datasets</span></span>
<span data-ttu-id="f7efc-199">Biz şimdi hello hello iki test kümelerindeki örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="f7efc-199">We now count hello number of examples in hello two test datasets.</span></span> <span data-ttu-id="f7efc-200">Merhaba içeriğine [örnek &#95; hive &#95; sayısı &#95; criteo &#95; & #95 test; & #95 gün; 22 &#95; Tablo &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f7efc-200">hello contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="f7efc-201">Bu verir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="f7efc-202">Her zamanki gibi biz de hello betik hello Hive Kutusu'ndan çağırabilir / directory hello komutu göndererek iste:</span><span class="sxs-lookup"><span data-stu-id="f7efc-202">As usual, we may also call hello script from hello Hive bin/ directory prompt by issuing hello command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="f7efc-203">Gün bazında hello test veri test örneklerde hello sayısı son olarak, inceleyeceğiz\_23.</span><span class="sxs-lookup"><span data-stu-id="f7efc-203">Finally, we examine hello number of test examples in hello test dataset based on day\_23.</span></span>

<span data-ttu-id="f7efc-204">Merhaba komutu toodo benzer toohello biri yalnızca gösterilen budur (çok başvuran[örnek &#95; hive &#95; sayısı &#95; criteo &#95; & #95 test; & #95 gün; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span><span class="sxs-lookup"><span data-stu-id="f7efc-204">hello command toodo this is similar toohello one just shown (refer too[sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="f7efc-205">Bu sunar:</span><span class="sxs-lookup"><span data-stu-id="f7efc-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a><span data-ttu-id="f7efc-206">Dağıtım hello tren kümesindeki etiket</span><span class="sxs-lookup"><span data-stu-id="f7efc-206">Label distribution in hello train dataset</span></span>
<span data-ttu-id="f7efc-207">Merhaba etiket dağıtım hello tren kümesindeki ilginizi çekecektir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-207">hello label distribution in hello train dataset is of interest.</span></span> <span data-ttu-id="f7efc-208">toosee Bu, içeriğini gösteriyoruz [örnek &#95; hive &#95; criteo &#95; & #95 etiket; & #95 dağıtım; eğitimi &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="f7efc-208">toosee this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="f7efc-209">Merhaba etiket dağıtım verir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-209">This yields hello label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="f7efc-210">Pozitif etiketleri Hello yüzdesi yaklaşık % 3.3 (Merhaba özgün kümesiyle tutarlı) olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-210">Note that hello percentage of positive labels is about 3.3% (consistent with hello original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="f7efc-211">Veri kümesi hello sayısal bazı değişkenler Histogram dağıtımlarını eğitme</span><span class="sxs-lookup"><span data-stu-id="f7efc-211">Histogram distributions of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="f7efc-212">Hive'nın yerel kullanırız "histogram\_sayısal" Merhaba sayısal değişkenlerin hangi hello dağıtım benzer çıkışı toofind işlev.</span><span class="sxs-lookup"><span data-stu-id="f7efc-212">We can use Hive's native "histogram\_numeric" function toofind out what hello distribution of hello numeric variables looks like.</span></span> <span data-ttu-id="f7efc-213">Merhaba içeriğine işte [örnek &#95; hive &#95; criteo &#95; histogram &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="f7efc-213">Here are hello contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="f7efc-214">Merhaba aşağıdaki verir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-214">This yields hello following:</span></span>

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

<span data-ttu-id="f7efc-215">Merhaba YANAL görünümü - Hive görevi görür tooproduce SQL benzeri çıktı hello normal listesi yerine birlikte Aç.</span><span class="sxs-lookup"><span data-stu-id="f7efc-215">hello LATERAL VIEW - explode combination in Hive serves tooproduce a SQL-like output instead of hello usual list.</span></span> <span data-ttu-id="f7efc-216">Not ın Merhaba, bu tablo, hello ilk sütun toohello depo merkezi ve hello ikinci toohello depo sıklığı karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-216">Note that in hello this table, hello first column corresponds toohello bin center and hello second toohello bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="f7efc-217">Veri kümesi hello bazı sayısal değişkenlerin yaklaşık yüzdebirlik değeri eğitme</span><span class="sxs-lookup"><span data-stu-id="f7efc-217">Approximate percentiles of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="f7efc-218">Ayrıca sayısal değişkenleriyle yaklaşık yüzdebirlik değeri hello hesaplaması ilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-218">Also of interest with numeric variables is hello computation of approximate percentiles.</span></span> <span data-ttu-id="f7efc-219">Hive yerel "yüzdelik\_yaklaşık" bunu bize yapar.</span><span class="sxs-lookup"><span data-stu-id="f7efc-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="f7efc-220">Merhaba içeriğine [örnek &#95; hive &#95; criteo &#95; yaklaşık &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f7efc-220">hello contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="f7efc-221">Bu verir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="f7efc-222">Yüzdebirlik değeri hello dağıtımını yakından ilgili toohello histogram dağıtım tüm sayısal değişkenin genellikle, remark.</span><span class="sxs-lookup"><span data-stu-id="f7efc-222">We remark that hello distribution of percentiles is closely related toohello histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a><span data-ttu-id="f7efc-223">Merhaba tren kümesindeki kategorik bazı sütunları için benzersiz değerlerin sayısını bulur</span><span class="sxs-lookup"><span data-stu-id="f7efc-223">Find number of unique values for some categorical columns in hello train dataset</span></span>
<span data-ttu-id="f7efc-224">Merhaba veri keşfi, biz Şimdi Bul, bazı kategorik sütunlar için hello aldıkları benzersiz değerlerin sayısını devam ediliyor.</span><span class="sxs-lookup"><span data-stu-id="f7efc-224">Continuing hello data exploration, we now find, for some categorical columns, hello number of unique values they take.</span></span> <span data-ttu-id="f7efc-225">toodo Bu, içeriğini gösteriyoruz [örnek &#95; hive &#95; criteo &#95; benzersiz &#95; değerleri &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="f7efc-225">toodo this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="f7efc-226">Bu verir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="f7efc-227">Col15 19 M benzersiz değerler olduğunu unutmayın!</span><span class="sxs-lookup"><span data-stu-id="f7efc-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="f7efc-228">"Bir hot kodlama" tooencode gibi naïve teknikler kullanılarak yüksek boyutlu tür kategorik değişkenlerinin uygulanamaz.</span><span class="sxs-lookup"><span data-stu-id="f7efc-228">Using naive techniques like "one-hot encoding" tooencode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="f7efc-229">Özellikle, biz açıklayabilir ve adında güçlü, sağlam bir teknik göstermek [ile öğrenme sayar](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) bu sorunu verimli bir şekilde tackling için.</span><span class="sxs-lookup"><span data-stu-id="f7efc-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="f7efc-230">Biz, bu alt bölümde bazı diğer kategorik sütunlar için de benzersiz değerlerin sayısını hello bakarak sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-230">We end this sub-section by looking at hello number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="f7efc-231">Merhaba içeriğine [örnek &#95; hive &#95; criteo &#95; benzersiz &#95; & #95 değerleri; birden çok &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f7efc-231">hello contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="f7efc-232">Bu verir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="f7efc-233">Yeniden Col20 hariç, tüm diğer hello olduğunu görmek sütunları birçok benzersiz değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="f7efc-233">Again we see that except for Col20, all hello other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a><span data-ttu-id="f7efc-234">Merhaba tren kümesindeki kategorik değişkenleri çiftlerini ortak oluşum sayısı</span><span class="sxs-lookup"><span data-stu-id="f7efc-234">Co-occurrence counts of pairs of categorical variables in hello train dataset</span></span>

<span data-ttu-id="f7efc-235">Ayrıca ilgi kategorik değişkenleri çiftlerini Hello ortak oluşum sayısı olur.</span><span class="sxs-lookup"><span data-stu-id="f7efc-235">hello co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="f7efc-236">Bu hello kod içinde kullanma belirlenebilir [örnek &#95; hive &#95; criteo &#95; eşleştirilmiş &#95; kategorik &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="f7efc-236">This can be determined using hello code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="f7efc-237">Biz sipariş hello sayıları kendi örneği tarafından ters ve 15 hello üstünde bu durumda bakın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-237">We reverse order hello counts by their occurrence and look at hello top 15 in this case.</span></span> <span data-ttu-id="f7efc-238">Bu bize sunar:</span><span class="sxs-lookup"><span data-stu-id="f7efc-238">This gives us:</span></span>

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <span data-ttu-id="f7efc-239"><a name="downsample"></a>Örnek hello veri kümesi Azure Machine Learning için</span><span class="sxs-lookup"><span data-stu-id="f7efc-239"><a name="downsample"></a> Down sample hello datasets for Azure Machine Learning</span></span>
<span data-ttu-id="f7efc-240">Keşfedilen hello veri kümeleri sahip ve nasıl biz Azure Machine Learning modellerini oluşturabilmeleri Biz bu tür herhangi bir değişkeni için (dahil olmak üzere birleşimleri), biz şimdi örnek hello veri kümelerini aşağı araştırması yapabilirsiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-240">Having explored hello datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample hello data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="f7efc-241">Biz odak o hello sorun geri çağırma: örnek öznitelikler (Col2 - Col40 özellik değerleri) kümesi verildiğinde, biz Col1 0 (hiçbir tıklayın) veya 1 (tıklatın) olup olmadığını tahmin.</span><span class="sxs-lookup"><span data-stu-id="f7efc-241">Recall that hello problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="f7efc-242">toodown bizim tren örnek ve hello özgün boyutunun veri kümeleri too1% test, Hive'nın yerel RAND() işlevinin kullanırız.</span><span class="sxs-lookup"><span data-stu-id="f7efc-242">toodown sample our train and test datasets too1% of hello original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="f7efc-243">Merhaba sonraki komut [örnek &#95; hive &#95; criteo &#95; alt örnekleyin &#95; eğitimi &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) hello tren veri kümesi için bunu yapar:</span><span class="sxs-lookup"><span data-stu-id="f7efc-243">hello next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for hello train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="f7efc-244">Bu verir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="f7efc-245">Merhaba betik [örnek &#95; hive &#95; criteo &#95; alt örnekleyin &#95; & #95 test; & #95 gün; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) test verileri için mevcut gün\_22:</span><span class="sxs-lookup"><span data-stu-id="f7efc-245">hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="f7efc-246">Bu verir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="f7efc-247">Son olarak, komut dosyası hello [örnek &#95; hive &#95; criteo &#95; alt örnekleyin &#95; & #95 test; & #95 gün; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) test verileri için mevcut gün\_23:</span><span class="sxs-lookup"><span data-stu-id="f7efc-247">Finally, hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="f7efc-248">Bu verir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="f7efc-249">Bu, biz bizim aşağı örneklenen hazır toouse, eğitim ve test Azure Machine Learning modellerini oluşturmak için veri kümeleri.</span><span class="sxs-lookup"><span data-stu-id="f7efc-249">With this, we are ready toouse our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="f7efc-250">Biz sorunları hello sayısı tablosu Machine Learning tooAzure üzerinde taşımadan önce son önemli bileşeni yoktur.</span><span class="sxs-lookup"><span data-stu-id="f7efc-250">There is a final important component before we move on tooAzure Machine Learning, which is concerns hello count table.</span></span> <span data-ttu-id="f7efc-251">Merhaba sonraki alt bölümde, biz bu biraz ayrıntılı olarak ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-251">In hello next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="f7efc-252"><a name="count"></a>Merhaba sayısı tablosundaki kısa bir tartışma</span><span class="sxs-lookup"><span data-stu-id="f7efc-252"><a name="count"></a> A brief discussion on hello count table</span></span>
<span data-ttu-id="f7efc-253">Gördüğümüz gibi çeşitli kategorik değişkenler çok yüksek bir boyut sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="f7efc-254">Bizim kılavuzda, biz adında güçlü bir teknik sunmak [ile öğrenme sayar](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode verimli ve güçlü bir şekilde bu değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="f7efc-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="f7efc-255">Bu teknik hakkında daha fazla bilgi sağlanan hello içinde bağlantıdır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-255">More information on this technique is in hello link provided.</span></span>

[!NOTE]
><span data-ttu-id="f7efc-256">Bu kılavuzda, count tabloları tooproduce compact gösterimlerini yüksek boyutlu kategorik özellikleri kullanarak odaklanın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-256">In this walkthrough, we focus on using count tables tooproduce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="f7efc-257">Bu hello tek yolu tooencode kategorik özellikleri değildir; diğer teknikleri hakkında daha fazla bilgi için ilgi kullanıcılar kontrol edebilirsiniz [bir-hot-encoding](http://en.wikipedia.org/wiki/One-hot) ve [özellik karma](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="f7efc-257">This is not hello only way tooencode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="f7efc-258">Merhaba sayısı verileri toobuild sayısı tablolarda, hello klasörü ham/sayıma hello veri kullanırız.</span><span class="sxs-lookup"><span data-stu-id="f7efc-258">toobuild count tables on hello count data, we use hello data in hello folder raw/count.</span></span> <span data-ttu-id="f7efc-259">Bölümünde, kullanıcıların gösteriyoruz modelleme hello nasıl toobuild bunlar sayısı sıfırdan veya alternatif olarak toouse kategorik özellikleri için kendi explorations için önceden derlenmiş sayısı tablosu tabloları.</span><span class="sxs-lookup"><span data-stu-id="f7efc-259">In hello modeling section, we show users how toobuild these count tables for categorical features from scratch, or alternatively toouse a pre-built count table for their explorations.</span></span> <span data-ttu-id="f7efc-260">Ne de biz başvurduğunuzda aşağıdaki çok "önceden oluşturulmuş sayısı tablolar", sağladığımız hello sayısı tabloları kullanarak anlama.</span><span class="sxs-lookup"><span data-stu-id="f7efc-260">In what follows, when we refer too"pre-built count tables", we mean using hello count tables that we provide.</span></span> <span data-ttu-id="f7efc-261">Nasıl tooaccess bu tablolar hello sonraki bölümde sağlanan ayrıntılı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="f7efc-261">Detailed instructions on how tooaccess these tables are provided in hello next section.</span></span>

## <span data-ttu-id="f7efc-262"><a name="aml"></a>Azure Machine Learning ile bir model oluşturma</span><span class="sxs-lookup"><span data-stu-id="f7efc-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="f7efc-263">Oluşturma işlemi Azure Machine learning'de modelimizi şu adımları izler:</span><span class="sxs-lookup"><span data-stu-id="f7efc-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="f7efc-264">Merhaba verileri Hive tablolardan Azure Machine Learning alın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-264">Get hello data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="f7efc-265">Merhaba deneme oluşturma: hello veri ve featurize sayısı tablolar ile temizleme</span><span class="sxs-lookup"><span data-stu-id="f7efc-265">Create hello experiment: clean hello data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="f7efc-266">Yapı, eğitme ve puanı hello modeli</span><span class="sxs-lookup"><span data-stu-id="f7efc-266">Build, train, and score hello model</span></span>](#step3)
4. [<span data-ttu-id="f7efc-267">Merhaba modelini değerlendir</span><span class="sxs-lookup"><span data-stu-id="f7efc-267">Evaluate hello model</span></span>](#step4)
5. [<span data-ttu-id="f7efc-268">Web hizmeti olarak Hello modeli yayımlama</span><span class="sxs-lookup"><span data-stu-id="f7efc-268">Publish hello model as a web-service</span></span>](#step5)

<span data-ttu-id="f7efc-269">Artık Azure Machine Learning Studio'da hazır toobuild modelleri bulunur.</span><span class="sxs-lookup"><span data-stu-id="f7efc-269">Now we are ready toobuild models in Azure Machine Learning studio.</span></span> <span data-ttu-id="f7efc-270">Aşağı örneklenen verilerimizi hello kümesindeki Hive tablolarını olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-270">Our down sampled data is saved as Hive tables in hello cluster.</span></span> <span data-ttu-id="f7efc-271">Hello Azure Machine Learning kullanırız **veri içeri aktarma** modülü tooread bu verileri.</span><span class="sxs-lookup"><span data-stu-id="f7efc-271">We use hello Azure Machine Learning **Import Data** module tooread this data.</span></span> <span data-ttu-id="f7efc-272">Bu kümenin Hello kimlik bilgilerini tooaccess hello depolama hesabı hangi aşağıdaki sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-272">hello credentials tooaccess hello storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="f7efc-273"><a name="step1"></a>1. adım: Azure Machine Learning hello veri içeri aktarma modülü kullanılarak Hive tablolarından veri almak ve bir makine öğrenimi denemesinin için seçin</span><span class="sxs-lookup"><span data-stu-id="f7efc-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using hello Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="f7efc-274">Başlangıç seçerek bir **+ yeni** -> **deneme** -> **boş deneme**.</span><span class="sxs-lookup"><span data-stu-id="f7efc-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="f7efc-275">Merhaba öğesinden sonra **arama** hello üst sol, "Veri Al" için arama kutusunu.</span><span class="sxs-lookup"><span data-stu-id="f7efc-275">Then, from hello **Search** box on hello top left, search for "Import Data".</span></span> <span data-ttu-id="f7efc-276">Sürükle ve bırak hello **veri içeri aktarma** toohello deneme tuvaline (Merhaba ekranında hello Orta bölümü) toouse hello modülü veri erişimi için modülünü.</span><span class="sxs-lookup"><span data-stu-id="f7efc-276">Drag and drop hello **Import Data** module on toohello experiment canvas (hello middle portion of hello screen) toouse hello module for data access.</span></span>

<span data-ttu-id="f7efc-277">Hangi hello budur **veri içeri aktarma** gibi görünüyor hello Hive tablodan veri alınırken hata oluştu:</span><span class="sxs-lookup"><span data-stu-id="f7efc-277">This is what hello **Import Data** looks like while getting data from hello Hive table:</span></span>

![Veri içeri aktarma verileri alır](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="f7efc-279">Hello için **veri içeri aktarma** modülü, grafik hello olan sağlanan hello yalnızca örnekleri tür değerleri, hello parametrelerinin hello değerleri tooprovide gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-279">For hello **Import Data** module, hello values of hello parameters that are provided in hello graphic are just examples of hello sort of values you need tooprovide.</span></span> <span data-ttu-id="f7efc-280">İşte bazı genel rehberlik toofill çıkış hello parametresi Merhaba nasıl ayarlanacağını **veri içeri aktarma** modülü.</span><span class="sxs-lookup"><span data-stu-id="f7efc-280">Here is some general guidance on how toofill out hello parameter set for hello **Import Data** module.</span></span>

1. <span data-ttu-id="f7efc-281">"Hive sorgusu" seçin **veri kaynağı**</span><span class="sxs-lookup"><span data-stu-id="f7efc-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="f7efc-282">Merhaba, **Hive veritabanı sorgusu** kutusunda, basit bir SELECT * FROM <,\_veritabanı\_name.your\_tablo\_adı >-yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-282">In hello **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="f7efc-283">**Hcatalog sunucusu URI**: "abc" kümeniz olduğunu sonra yalnızca budur: https://abc.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="f7efc-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="f7efc-284">**Hadoop kullanıcı hesabı adı**: hello küme commissioning hello sırasında seçilen hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="f7efc-284">**Hadoop user account name**: hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="f7efc-285">(Merhaba uzaktan erişim kullanıcı adı değil!)</span><span class="sxs-lookup"><span data-stu-id="f7efc-285">(NOT hello Remote Access user name!)</span></span>
5. <span data-ttu-id="f7efc-286">**Hadoop kullanıcı hesabı parolasını**: hello parolasını hello küme commissioning hello sırasında seçilen hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="f7efc-286">**Hadoop user account password**: hello password for hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="f7efc-287">(Değil hello uzaktan erişim parola!)</span><span class="sxs-lookup"><span data-stu-id="f7efc-287">(NOT hello Remote Access password!)</span></span>
6. <span data-ttu-id="f7efc-288">**Çıktı verilerini konumunu**: "Azure" seçin</span><span class="sxs-lookup"><span data-stu-id="f7efc-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="f7efc-289">**Azure depolama hesabı adı**: Merhaba hello kümeyle ilişkili depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="f7efc-289">**Azure storage account name**: hello storage account associated with hello cluster</span></span>
8. <span data-ttu-id="f7efc-290">**Azure depolama hesabı anahtarı**: hello kümesi ile ilişkili hello depolama hesabı hello anahtarı.</span><span class="sxs-lookup"><span data-stu-id="f7efc-290">**Azure storage account key**: hello key of hello storage account associated with hello cluster.</span></span>
9. <span data-ttu-id="f7efc-291">**Azure kapsayıcı adı**: hello küme adı olduğundan "abc" sonra yalnızca "abc", genellikle budur.</span><span class="sxs-lookup"><span data-stu-id="f7efc-291">**Azure container name**: If hello cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="f7efc-292">Bir kez hello **veri içeri aktarma** sonlandığında (gördüğünüz hello yeşil onay işareti hello modülü üzerinde) veri alma (tercih ettiğiniz bir adla) bir veri kümesi olarak bu verileri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f7efc-292">Once hello **Import Data** finishes getting data (you see hello green tick on hello Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="f7efc-293">Bunun nasıl göründüğünü:</span><span class="sxs-lookup"><span data-stu-id="f7efc-293">What this looks like:</span></span>

![Veri alma veri kaydetme](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="f7efc-295">Sağ hello çıktı hello bağlantı noktası **veri içeri aktarma** modülü.</span><span class="sxs-lookup"><span data-stu-id="f7efc-295">Right-click hello output port of hello **Import Data** module.</span></span> <span data-ttu-id="f7efc-296">Bu gösteren bir **veri kümesi Kaydet** seçeneği ve bir **Görselleştir** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f7efc-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="f7efc-297">Merhaba **Görselleştir** seçeneği tıkladıysanız, bazı Özet istatistikleri için yararlı olan bir sağ panelde birlikte hello veri 100 satırı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f7efc-297">hello **Visualize** option, if clicked, displays 100 rows of hello data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="f7efc-298">toosave veri seçmeniz yeterlidir **veri kümesi Kaydet** ve yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="f7efc-298">toosave data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="f7efc-299">tooselect kaydedilen hello kullanılmak üzere bir machine learning deneme bulun hello kullanarak hello veri kümeleri **arama** hello aşağıdaki şekilde gösterilen kutusu.</span><span class="sxs-lookup"><span data-stu-id="f7efc-299">tooselect hello saved dataset for use in a machine learning experiment, locate hello datasets using hello **Search** box shown in hello following figure.</span></span> <span data-ttu-id="f7efc-300">Yalnızca türünü verdiğiniz hello adı öğrenmek hello sonra dataset kısmen ve sürükleme hello üzerine dataset tooaccess hello ana bölmesi.</span><span class="sxs-lookup"><span data-stu-id="f7efc-300">Then simply type out hello name you gave hello dataset partially tooaccess it and drag hello dataset onto hello main panel.</span></span> <span data-ttu-id="f7efc-301">Merhaba ana panelinden bırakmadan machine learning modelleme kullanmak için seçilir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-301">Dropping it onto hello main panel selects it for use in machine learning modeling.</span></span>

![Merhaba ana panelinin üzerine Drage veri kümesi](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="f7efc-303">Merhaba eğitimi ve hello test veri kümeleri için bunu.</span><span class="sxs-lookup"><span data-stu-id="f7efc-303">Do this for both hello train and hello test datasets.</span></span> <span data-ttu-id="f7efc-304">Ayrıca, toouse hello veritabanı adı ve bu amaçla verdiğiniz tablo adlarının unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-304">Also, remember toouse hello database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="f7efc-305">Merhaba şekilde kullanılan hello değerler yalnızca çizim yaratılır * için:</span><span class="sxs-lookup"><span data-stu-id="f7efc-305">hello values used in hello figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="f7efc-306"><a name="step2"></a>2. adım: Azure Machine Learning toopredict tıklatma ile basit bir deneme oluşturma / hiçbir tıklama</span><span class="sxs-lookup"><span data-stu-id="f7efc-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning toopredict clicks / no clicks</span></span>
<span data-ttu-id="f7efc-307">Bizim Azure ML deneme şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="f7efc-307">Our Azure ML experiment looks like this:</span></span>

![Machine Learning deneme](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="f7efc-309">Şimdi bu deneme anahtar bileşenlerinin hello inceleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="f7efc-309">We now examine hello key components of this experiment.</span></span> <span data-ttu-id="f7efc-310">Bir hatırlatma bizim kaydedilmiş eğitmek ve tooour deneme tuvalinin veri kümelerinin önce test toodrag gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-310">As a reminder, we need toodrag our saved train and test datasets on tooour experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="f7efc-311">Eksik verileri temizleme</span><span class="sxs-lookup"><span data-stu-id="f7efc-311">Clean Missing Data</span></span>
<span data-ttu-id="f7efc-312">Merhaba **Clean Missing Data** modülü mu ne adından da anlaşılacağı: kullanıcı tarafından belirtilen yolla eksik verileri temizler.</span><span class="sxs-lookup"><span data-stu-id="f7efc-312">hello **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="f7efc-313">Bu modüle baktığınızda, biz bu bakın:</span><span class="sxs-lookup"><span data-stu-id="f7efc-313">Looking into this module, we see this:</span></span>

![Eksik verilerini temizle](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="f7efc-315">Burada, tooreplace tüm eksik değerleri 0 ile seçtik.</span><span class="sxs-lookup"><span data-stu-id="f7efc-315">Here, we chose tooreplace all missing values with a 0.</span></span> <span data-ttu-id="f7efc-316">Merhaba bırakmalar hello modülünde bakarak görülebilir diğer seçenekler de vardır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-316">There are other options as well, which can be seen by looking at hello dropdowns in hello module.</span></span>

#### <a name="feature-engineering-on-hello-data"></a><span data-ttu-id="f7efc-317">Özellik Mühendisliği hello verileri</span><span class="sxs-lookup"><span data-stu-id="f7efc-317">Feature engineering on hello data</span></span>
<span data-ttu-id="f7efc-318">Büyük veri kategorik bazı özellikler için benzersiz değerler milyonlarca olabilir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="f7efc-319">Naïve yöntemlerden biri hot yüksek boyutlu kategorik özelliklerden temsil etmek için kodlama gibi tamamen unfeasible kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="f7efc-320">Bu kılavuzda, nasıl toouse sayısı özellikleri yerleşik Azure Machine Learning modüllerinin toogenerate kullanarak bu yüksek boyutlu kategorik değişkenleri gösterimlerini compact göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-320">In this walkthrough, we demonstrate how toouse count features using built-in Azure Machine Learning modules toogenerate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="f7efc-321">Merhaba nihai sonucu daha küçük bir model boyutu, daha hızlı eğitim süreleri, oldukça karşılaştırılabilir toousing olan performans ölçümleri ise başka teknikler.</span><span class="sxs-lookup"><span data-stu-id="f7efc-321">hello end-result is a smaller model size, faster training times, and performance metrics that are quite comparable toousing other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="f7efc-322">Dönüşümler sayım oluşturma</span><span class="sxs-lookup"><span data-stu-id="f7efc-322">Building counting transforms</span></span>
<span data-ttu-id="f7efc-323">toobuild sayısı özellikleri kullanırız hello **yapı sayım dönüştürme** Azure Machine Learning kullanılabilir modül.</span><span class="sxs-lookup"><span data-stu-id="f7efc-323">toobuild count features, we use hello **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="f7efc-324">Merhaba modülü şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="f7efc-324">hello module looks like this:</span></span>

<span data-ttu-id="f7efc-325">![Sayım dönüştürme modülü oluşturmak](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![yapı sayım dönüştürme Modülü](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="f7efc-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f7efc-326">Merhaba, **saymak sütunları** kutusu, biz girin tooperform sayar istediğimiz bu sütunları.</span><span class="sxs-lookup"><span data-stu-id="f7efc-326">In hello **Count columns** box, we enter those columns that we wish tooperform counts on.</span></span> <span data-ttu-id="f7efc-327">Genellikle, bunlar (belirtildiği gibi) yüksek boyutlu kategorik sütun.</span><span class="sxs-lookup"><span data-stu-id="f7efc-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="f7efc-328">Merhaba başlangıcında Biz bu hello Criteo dataset 26 kategorik sütunları belirtilen sahip: Col15 tooCol40 gelen.</span><span class="sxs-lookup"><span data-stu-id="f7efc-328">At hello start, we mentioned that hello Criteo dataset has 26 categorical columns: from Col15 tooCol40.</span></span> <span data-ttu-id="f7efc-329">Burada, biz hepsinde saymak ve bunların dizinlerini (gösterildiği gibi virgülle ayırarak 15 too40) verin.</span><span class="sxs-lookup"><span data-stu-id="f7efc-329">Here, we count on all of them and give their indices (from 15 too40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="f7efc-330">toouse hello modülünde hello MapReduce modu (büyük veri kümeleri için uygundur), biz tooan Hdınsight Hadoop kümesi (Bu amaç için bir özellik araştırması için kullanılan yeniden kullanılabilir hello) ve kimlik bilgileri erişim.</span><span class="sxs-lookup"><span data-stu-id="f7efc-330">toouse hello module in hello MapReduce mode (appropriate for large datasets), we need access tooan HDInsight Hadoop cluster (hello one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="f7efc-331">Merhaba önceki rakamları görünüm gibi (kendi kullanım durumu için ilgili olanla çizim için sağlanan hello değerleri değiştirin) hello doldurulan değerleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-331">hello  previous figures illustrate what hello filled-in values look like (replace hello values provided for illustration with those relevant for your own use-case).</span></span>

![Modülü parametreleri](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="f7efc-333">Yukarıdaki Hello şekil içinde nasıl tooenter hello blob giriş olan gösteriyoruz konumu.</span><span class="sxs-lookup"><span data-stu-id="f7efc-333">In hello figure above, we show how tooenter hello input blob location.</span></span> <span data-ttu-id="f7efc-334">Bu konumda sayısı tabloları oluşturma için ayrılmış hello veri yok.</span><span class="sxs-lookup"><span data-stu-id="f7efc-334">This location has hello data reserved for building count tables on.</span></span>

<span data-ttu-id="f7efc-335">Bu modül çalışması bittikten sonra biz hello dönüştürme için daha sonra hello modülü sağ tıklayıp hello seçerek kaydedebilirsiniz **dönüştürme Kaydet** seçeneği:</span><span class="sxs-lookup"><span data-stu-id="f7efc-335">After this module finishes running, we can save hello transform for later by right-clicking hello module and selecting hello **Save as Transform** option:</span></span>

!["Dönüştürme Kaydet" seçeneğini](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="f7efc-337">Yukarıda gösterilen bizim deneme mimarisinde hello dataset "ytransform2" tam sayı dönüşümü kaydedilmiş tooa karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-337">In our experiment architecture shown above, hello dataset "ytransform2" corresponds precisely tooa saved count transform.</span></span> <span data-ttu-id="f7efc-338">Bu deneme Hello kalanı için kullanılan bu hello okuyucu varsayıyoruz bir **yapı sayım dönüştürme** modülü bazı veri toogenerate sayısı ve ardından olabilir, bu sayıları toogenerate sayısı özellikleri hello tren üzerinde kullanmak ve test veri kümeleri.</span><span class="sxs-lookup"><span data-stu-id="f7efc-338">For hello remainder of this experiment, we assume that hello reader used a **Build Counting Transform** module on some data toogenerate counts, and can then use those counts toogenerate count features on hello train and test datasets.</span></span>

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a><span data-ttu-id="f7efc-339">Hangi özellikleri tooinclude hello tren bir parçası olarak say ve veri kümelerini test seçme</span><span class="sxs-lookup"><span data-stu-id="f7efc-339">Choosing what count features tooinclude as part of hello train and test datasets</span></span>
<span data-ttu-id="f7efc-340">Hazır dönüştürme sayısı sahibiz sonra hello kullanıcı kendi tren hangi özellikleri tooinclude seçin ve test hello kullanan veri Setleri **sayısı tablo parametreleri değiştirmek** modülü.</span><span class="sxs-lookup"><span data-stu-id="f7efc-340">Once we have a count transform ready, hello user can choose what features tooinclude in their train and test datasets using hello **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="f7efc-341">Yalnızca bu modül gösteriyoruz burada eksiksiz olması için ancak Basitlik ilgi gerçekten bunu bizim deneme kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![Count tablo parametreleri değiştirin](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="f7efc-343">Bu durumda, görüldüğü gibi biz yalnızca hello günlük büyük olasılıkla toouse seçmiş ve tooignore hello geri sütun devre dışı.</span><span class="sxs-lookup"><span data-stu-id="f7efc-343">In this case, as can be seen, we have chosen toouse just hello log-odds and tooignore hello back off column.</span></span> <span data-ttu-id="f7efc-344">Biz de hello çöp depo eşiği düzgünleştirme için kaç tane sözde önceki örnekler tooadd gibi parametreleri ayarlayabilirsiniz ve olup toouse herhangi Laplacian gürültü veya değil.</span><span class="sxs-lookup"><span data-stu-id="f7efc-344">We can also set parameters such as hello garbage bin threshold, how many pseudo-prior examples tooadd for smoothing, and whether toouse any Laplacian noise or not.</span></span> <span data-ttu-id="f7efc-345">Bunların tümü Gelişmiş Özellikler ve bu toobe hello varsayılan değerleri özelliği nesil yeni toothis türü olan kullanıcılar için iyi bir başlangıç noktası olduğunu belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-345">All these are advanced features and it is toobe noted that hello default values are a good starting point for users who are new toothis type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-hello-count-features"></a><span data-ttu-id="f7efc-346">Merhaba sayısı özellikleri oluşturmadan veri dönüştürme</span><span class="sxs-lookup"><span data-stu-id="f7efc-346">Data transformation before generating hello count features</span></span>
<span data-ttu-id="f7efc-347">Şimdi biz bizim tren dönüştürme hakkında önemli bir nokta odaklanır ve veri önceki tooactually sayısı özellikleri oluşturma sınayın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-347">Now we focus on an important point about transforming our train and test data prior tooactually generating count features.</span></span> <span data-ttu-id="f7efc-348">İki olduğunu unutmayın **R betiği yürütün** biz hello sayısı dönüştürme tooour verileri uygulamadan önce kullanılan modülleri.</span><span class="sxs-lookup"><span data-stu-id="f7efc-348">Note that there are two **Execute R Script** modules used before we apply hello count transform tooour data.</span></span>

![R betiği modülleri yürütme](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="f7efc-350">Merhaba ilk R betiği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-350">Here is hello first R script:</span></span>

![İlk R betiği](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="f7efc-352">Bu R betiği biz bizim sütunları toonames "Col1" çok yeniden adlandırma "Col40".</span><span class="sxs-lookup"><span data-stu-id="f7efc-352">In this R script, we rename our columns toonames "Col1" too"Col40".</span></span> <span data-ttu-id="f7efc-353">Bu biçim adını Hello sayısı dönüştürme bekliyor olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-353">This is because hello count transform expects names of this format.</span></span>

<span data-ttu-id="f7efc-354">Merhaba ikinci R komut dosyasında, biz hello dağıtım pozitif ve negatif sınıflar arasında dengeleyin (sırasıyla 1 ve 0 sınıfları) aşağı örnekleme hello negatif sınıfı tarafından.</span><span class="sxs-lookup"><span data-stu-id="f7efc-354">In hello second R script, we balance hello distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling hello negative class.</span></span> <span data-ttu-id="f7efc-355">Merhaba R betiği buraya gösterir nasıl toodo bu:</span><span class="sxs-lookup"><span data-stu-id="f7efc-355">hello R script here shows how toodo this:</span></span>

![İkinci R betiği](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="f7efc-357">Basit bir R betiği kullanırız "pos\_neg\_oranı" hello pozitif ve negatif hello sınıflar arasında bir denge tooset hello miktarı.</span><span class="sxs-lookup"><span data-stu-id="f7efc-357">In this simple R script, we use "pos\_neg\_ratio" tooset hello amount of balance between hello positive and hello negative classes.</span></span> <span data-ttu-id="f7efc-358">Bu sınıf dengesizliği genellikle geliştirme sınıflandırma sorunları için performans avantajı hello sınıfı dağıtım olduğu olduğundan toodo (örneğimizde, biz %3.3 pozitif ve negatif %96.7 sınıf olduğunu geri çağırma) eğri önemlidir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-358">This is important toodo since improving class imbalance usually has performance benefits for classification problems where hello class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-hello-count-transformation-on-our-data"></a><span data-ttu-id="f7efc-359">Verilerimizi uygulanan hello sayısı dönüşümü</span><span class="sxs-lookup"><span data-stu-id="f7efc-359">Applying hello count transformation on our data</span></span>
<span data-ttu-id="f7efc-360">Son olarak, biz hello kullanabilirsiniz **uygulamak dönüştürme** modülü tooapply hello bizim tren üzerinde sayısı dönüşümler ve test veri kümeleri.</span><span class="sxs-lookup"><span data-stu-id="f7efc-360">Finally, we can use hello **Apply Transformation** module tooapply hello count transforms on our train and test datasets.</span></span> <span data-ttu-id="f7efc-361">Bu modül bir giriş ve hello eğitmek veya test diğer giriş hello gibi veri kümeleri olarak kaydedilen hello sayısı dönüştürme alır ve sayısı özelliklere sahip verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="f7efc-361">This module takes hello saved count transform as one input and hello train or test datasets as hello other input, and returns data with count features.</span></span> <span data-ttu-id="f7efc-362">Burada gösterilir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-362">It is shown here:</span></span>

![Dönüştürme modülü Uygula](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a><span data-ttu-id="f7efc-364">Merhaba sayısı özellikleri neye benzediğini gösteren bir alıntı</span><span class="sxs-lookup"><span data-stu-id="f7efc-364">An excerpt of what hello count features look like</span></span>
<span data-ttu-id="f7efc-365">Bu örneğimizde hangi hello sayısı özellikler neye benzediğini gösteren yönergeli toosee olur.</span><span class="sxs-lookup"><span data-stu-id="f7efc-365">It is instructive toosee what hello count features look like in our case.</span></span> <span data-ttu-id="f7efc-366">Burada bir alıntı bu göster:</span><span class="sxs-lookup"><span data-stu-id="f7efc-366">Here we show an excerpt of this:</span></span>

![Count özellikleri](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="f7efc-368">Bu alıntı, biz sayılan hello sütunların, biz hello sayılarını elde ve büyük olasılıkla toplama tooany ilgili backoffs oturum olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-368">In this excerpt, we show that for hello columns that we counted on, we get hello counts and log odds in addition tooany relevant backoffs.</span></span>

<span data-ttu-id="f7efc-369">Şimdi hazır toobuild dönüştürülmüş bu veri kümelerini kullanarak bir Azure Machine Learning modeli duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="f7efc-369">We are now ready toobuild an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="f7efc-370">Merhaba sonraki bölümde, bu nasıl yapılabilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-370">In hello next section, we show how this can be done.</span></span>

### <span data-ttu-id="f7efc-371"><a name="step3"></a>3. adım: Oluşturmak, eğitmek ve hello modeli Puanlama</span><span class="sxs-lookup"><span data-stu-id="f7efc-371"><a name="step3"></a> Step 3: Build, train, and score hello model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="f7efc-372">Öğrenen seçimi</span><span class="sxs-lookup"><span data-stu-id="f7efc-372">Choice of learner</span></span>
<span data-ttu-id="f7efc-373">İlk olarak, toochoose bir öğrenen gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-373">First, we need toochoose a learner.</span></span> <span data-ttu-id="f7efc-374">Bizim öğrenen giderek toouse boosted iki sınıf karar ağacı duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="f7efc-374">We are going toouse a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="f7efc-375">Bu öğrenen için hello varsayılan seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f7efc-375">Here are hello default options for this learner:</span></span>

![İki-Class Boosted karar ağacı parametreleri](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="f7efc-377">Bizim deneme için devam eden toochoose hello varsayılan değerleri duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="f7efc-377">For our experiment, we are going toochoose hello default values.</span></span> <span data-ttu-id="f7efc-378">Bu hello genellikle anlamlı olan ve performansı en iyi yolu tooget hızlı temelleri varsayılanlarını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-378">We note that hello defaults are usually meaningful and a good way tooget quick baselines on performance.</span></span> <span data-ttu-id="f7efc-379">Sahip olduğunuz tooonce seçerseniz, parametreleri temel yerleştirmez tarafından performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-379">You can improve on performance by sweeping parameters if you choose tooonce you have a baseline.</span></span>

#### <a name="train-hello-model"></a><span data-ttu-id="f7efc-380">Tren hello modeli</span><span class="sxs-lookup"><span data-stu-id="f7efc-380">Train hello model</span></span>
<span data-ttu-id="f7efc-381">Eğitim için biz yalnızca çağırma bir **Train Model** modülü.</span><span class="sxs-lookup"><span data-stu-id="f7efc-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="f7efc-382">Merhaba iki girişleri tooit hello iki-Class Boosted karar ağacı öğrenen ve tren kümemize verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-382">hello two inputs tooit are hello Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="f7efc-383">Bu aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-383">This is shown here:</span></span>

![Train Model Modülü](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a><span data-ttu-id="f7efc-385">Puan hello modeli</span><span class="sxs-lookup"><span data-stu-id="f7efc-385">Score hello model</span></span>
<span data-ttu-id="f7efc-386">Biz bir modeli eğittikten sonra biz hazır tooscore hello üzerinde kendi performans veri kümesi ve tooevaluate test.</span><span class="sxs-lookup"><span data-stu-id="f7efc-386">Once we have a trained model, we are ready tooscore on hello test dataset and tooevaluate its performance.</span></span> <span data-ttu-id="f7efc-387">Biz hello kullanarak bunu **Score Model** modülü ile birlikte aşağıdaki şekilde, hello gösterildiği bir **Evaluate Model** Modülü:</span><span class="sxs-lookup"><span data-stu-id="f7efc-387">We do this by using hello **Score Model** module shown in hello following figure, along with an **Evaluate Model** module:</span></span>

![Score Model (Model Puanlama) modülü](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="f7efc-389"><a name="step4"></a>4. adım: hello modelini değerlendir</span><span class="sxs-lookup"><span data-stu-id="f7efc-389"><a name="step4"></a> Step 4: Evaluate hello model</span></span>
<span data-ttu-id="f7efc-390">Son olarak, tooanalyze modeli performans isteriz.</span><span class="sxs-lookup"><span data-stu-id="f7efc-390">Finally, we would like tooanalyze model performance.</span></span> <span data-ttu-id="f7efc-391">Genellikle, iki sınıfı (ikili) sınıflandırma sorunu için iyi hello AUC ölçüsüdür.</span><span class="sxs-lookup"><span data-stu-id="f7efc-391">Usually, for two class (binary) classification problems, a good measure is hello AUC.</span></span> <span data-ttu-id="f7efc-392">toovisualize Bu, biz hello kanca **Score Model** modülü tooan **Evaluate Model** için bu modülü.</span><span class="sxs-lookup"><span data-stu-id="f7efc-392">toovisualize this, we hook up hello **Score Model** module tooan **Evaluate Model** module for this.</span></span> <span data-ttu-id="f7efc-393">Tıklatarak **Görselleştir** hello üzerinde **Evaluate Model** modülü bir aşağıdaki hello gibi bir grafik verir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-393">Clicking **Visualize** on hello **Evaluate Model** module yields a graphic like hello following one:</span></span>

![Modül BDT modelini değerlendir](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="f7efc-395">İkili (veya iki sınıf) sınıflandırma sorunları, tahmin doğruluğunu iyi bir ölçü alanı altında eğri (AUC) hello.</span><span class="sxs-lookup"><span data-stu-id="f7efc-395">In binary (or two class) classification problems, a good measure of prediction accuracy is hello Area Under Curve (AUC).</span></span> <span data-ttu-id="f7efc-396">Ne izleyen test kümemize bu modeli kullanarak sonuçları gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="f7efc-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="f7efc-397">tooget Bu, sağ hello çıkış bağlantı noktasına hello **Evaluate Model** modülü ve ardından **Görselleştir**.</span><span class="sxs-lookup"><span data-stu-id="f7efc-397">tooget this, right-click hello output port of hello **Evaluate Model** module and then **Visualize**.</span></span>

![Evaluate Model modülü Görselleştirme](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="f7efc-399"><a name="step5"></a>5. adım: bir Web hizmeti olarak hello modeli yayımlama</span><span class="sxs-lookup"><span data-stu-id="f7efc-399"><a name="step5"></a> Step 5: Publish hello model as a Web service</span></span>
<span data-ttu-id="f7efc-400">Hello özelliği toopublish web hizmetleri fuss en az olarak bir Azure Machine Learning modeli, yaygın olarak kullanılabilir hale getirme için değerli bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-400">hello ability toopublish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="f7efc-401">Bu yapıldığında, herkesin çağrıları toohello web hizmeti tahminleri için ihtiyaç duydukları ve hello web hizmeti, bu Öngörüler hello modeli tooreturn kullanır giriş verileri ile yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7efc-401">Once that is done, anyone can make calls toohello web service with input data that they need predictions for, and hello web service uses hello model tooreturn those predictions.</span></span>

<span data-ttu-id="f7efc-402">toodo Bu, biz bizim eğitilen modeli eğitilen Model nesnesi olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f7efc-402">toodo this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="f7efc-403">Bu hello sağ tıklayarak yapılır **Train Model** modülü ve hello kullanarak **eğitilen modelini Farklı Kaydet** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f7efc-403">This is done by right-clicking hello **Train Model** module and using hello **Save as Trained Model** option.</span></span>

<span data-ttu-id="f7efc-404">Toocreate giriş ve çıkış daha ihtiyacımız bizim web hizmeti için bağlantı noktaları:</span><span class="sxs-lookup"><span data-stu-id="f7efc-404">Next, we need toocreate input and output ports for our web service:</span></span>

* <span data-ttu-id="f7efc-405">bir giriş bağlantı noktası aynı tahminleri için ihtiyacımız hello veri olarak form hello içinde veri alır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-405">an input port takes data in hello same form as hello data that we need predictions for</span></span>
* <span data-ttu-id="f7efc-406">bir çıkış bağlantı noktasına hello skoru etiketleri ve ilişkili hello olasılıklar döndürür.</span><span class="sxs-lookup"><span data-stu-id="f7efc-406">an output port returns hello Scored Labels and hello associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a><span data-ttu-id="f7efc-407">Veri hello giriş bağlantı noktası için birkaç satır seçin</span><span class="sxs-lookup"><span data-stu-id="f7efc-407">Select a few rows of data for hello input port</span></span>
<span data-ttu-id="f7efc-408">Uygun toouse olan bir **geçerli SQL dönüştürme** modülü tooselect yalnızca 10 satır tooserve hello olarak giriş bağlantı noktası verileri.</span><span class="sxs-lookup"><span data-stu-id="f7efc-408">It is convenient toouse an **Apply SQL Transformation** module tooselect just 10 rows tooserve as hello input port data.</span></span> <span data-ttu-id="f7efc-409">Yalnızca bu burada gösterilen hello SQL sorgusunu kullanarak, giriş bağlantı noktası için veri satırı seçin:</span><span class="sxs-lookup"><span data-stu-id="f7efc-409">Select just these rows of data for our input port using hello SQL query shown here:</span></span>

![Giriş bağlantı noktası verileri](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="f7efc-411">Web hizmeti</span><span class="sxs-lookup"><span data-stu-id="f7efc-411">Web service</span></span>
<span data-ttu-id="f7efc-412">Biz artık toorun kullanılan toopublish olabilir küçük bir deneme bizim web hizmeti hazır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-412">Now we are ready toorun a small experiment that can be used toopublish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="f7efc-413">Web hizmeti için giriş verileri oluştur</span><span class="sxs-lookup"><span data-stu-id="f7efc-413">Generate input data for webservice</span></span>
<span data-ttu-id="f7efc-414">Sıfırıncı adım olarak hello sayısı tablo büyük olduğundan biz birkaç satırlık bir test verilerini alın ve çıktı verilerini buradan sayısı özelliklerle oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f7efc-414">As a zeroth step, since hello count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="f7efc-415">Bu bizim webservice için hello giriş veri biçimi olarak hizmet verebilir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-415">This can serve as hello input data format for our webservice.</span></span> <span data-ttu-id="f7efc-416">Bu aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f7efc-416">This is shown here:</span></span>

![BDT giriş verileri oluşturma](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="f7efc-418">Merhaba giriş veri biçimi için şimdi hello hello ÇIKTISINI kullanırız **sayısı Featurizer** modülü.</span><span class="sxs-lookup"><span data-stu-id="f7efc-418">For hello input data format, we now use hello OUTPUT of hello **Count Featurizer** module.</span></span> <span data-ttu-id="f7efc-419">Bu deneme çalıştıran bittikten sonra hello hello çıkış kaydedin **sayısı Featurizer** modülü bir veri kümesi olarak.</span><span class="sxs-lookup"><span data-stu-id="f7efc-419">Once this experiment finishes running, save hello output from hello **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="f7efc-420">Bu veri kümesi hello webservice hello girdi verileri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f7efc-420">This Dataset is used for hello input data in hello webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="f7efc-421">Deneme için Web Yayımlama hizmeti Puanlama</span><span class="sxs-lookup"><span data-stu-id="f7efc-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="f7efc-422">İlk olarak, bu nasıl göründüğünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-422">First, we show what this looks like.</span></span> <span data-ttu-id="f7efc-423">Merhaba temel yapısı bir **Score Model** bizim eğitilen model nesnesi ve birkaç satırlık biz hello kullanarak hello önceki adımlarda oluşturulan giriş verilerini kabul eden modül **sayısı Featurizer** modülü.</span><span class="sxs-lookup"><span data-stu-id="f7efc-423">hello essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in hello previous steps using hello **Count Featurizer** module.</span></span> <span data-ttu-id="f7efc-424">"Sütun Dataset içinde seçin" tooproject hello Scored etiketleri ve hello puan olasılıklar kullanırız.</span><span class="sxs-lookup"><span data-stu-id="f7efc-424">We use "Select Columns in Dataset" tooproject out hello Scored labels and hello Score probabilities.</span></span>

![Veri kümesinde sütun seçme](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="f7efc-426">Nasıl hello fark **Select Columns in Dataset sütun** modülü, 'verileri bir veri kümesinden filtreleme' için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-426">Notice how hello **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="f7efc-427">Biz, burada hello içindekileri göster:</span><span class="sxs-lookup"><span data-stu-id="f7efc-427">We show hello contents here:</span></span>

![Veri kümesi modülünde hello Sütunları Seç ile filtreleme](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="f7efc-429">tooget giriş ve çıkış hello mavi bağlantı noktaları, yalnızca tıklattığınız **webservice hazırlama** sağ hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="f7efc-429">tooget hello blue input and output ports, you simply click **prepare webservice** at hello bottom right.</span></span> <span data-ttu-id="f7efc-430">Bu deneme çalıştırılması de olanak tanır. bize toopublish hello web hizmeti: hello tıklatın **yayımlama WEB hizmeti** hello alt right, gösterilen burada simgesine tıklayın:</span><span class="sxs-lookup"><span data-stu-id="f7efc-430">Running this experiment also allows us toopublish hello web service: click hello **PUBLISH WEB SERVICE** icon at hello bottom right, shown here:</span></span>

![Web hizmeti yayımlama](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="f7efc-432">Hello webservice yayımlandığında, şu nedenle yeniden yönlendirilen tooa sayfası alın:</span><span class="sxs-lookup"><span data-stu-id="f7efc-432">Once hello webservice is published, we get redirected tooa page that looks thus:</span></span>

![Web hizmeti Panosu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="f7efc-434">Biz, hello sol tarafındaki webservices'a için iki bağlantılara bakın:</span><span class="sxs-lookup"><span data-stu-id="f7efc-434">We see two links for webservices on hello left side:</span></span>

* <span data-ttu-id="f7efc-435">Merhaba **istek/yanıt** hizmet (ya da RR) için tek tahminleri tasarlanmıştır ve ne Biz bu Atölye kullanma biçimleridir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-435">hello **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="f7efc-436">Merhaba **toplu iş yürütme** hizmeti (BES) için toplu tahminleri kullanılır ve hello kullanılan giriş verileri toomake tahminleri Azure Blob depolama alanına bulunmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-436">hello **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that hello input data used toomake predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="f7efc-437">Merhaba bağlantıyı tıklatmak **istek/yanıt** bize tooa alır bize veriyor sayfa önceden tamamlanmış C#, python ve r kodu Bu kod rahat çağrıları toohello webservice yapmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f7efc-437">Clicking on hello link **REQUEST/RESPONSE** takes us tooa page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls toohello webservice.</span></span> <span data-ttu-id="f7efc-438">Kimlik doğrulaması için kullanılan toobe bu hello API anahtarı, bu sayfada gereken unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-438">Note that hello API key on this page needs toobe used for authentication.</span></span>

<span data-ttu-id="f7efc-439">Merhaba IPython Not tooa yeni hücreye üzerinden bu python kodu uygun toocopy olur.</span><span class="sxs-lookup"><span data-stu-id="f7efc-439">It is convenient toocopy this python code over tooa new cell in hello IPython notebook.</span></span>

<span data-ttu-id="f7efc-440">Burada python kodu bir parçasını hello doğru API anahtarıyla gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="f7efc-440">Here we show a segment of python code with hello correct API key.</span></span>

![Python kodu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="f7efc-442">Biz hello varsayılan API anahtarı bizim webservices'a 's API anahtarı ile değiştirilen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f7efc-442">Note that we replaced hello default API key with our webservices's API key.</span></span> <span data-ttu-id="f7efc-443">Tıklatarak **çalıştırmak** dizüstü bilgisayar üzerinde bir IPython Bu hücrede yanıt aşağıdaki hello ortaya çıkarır:</span><span class="sxs-lookup"><span data-stu-id="f7efc-443">Clicking **Run** on this cell in an IPython notebook yields hello following response:</span></span>

![IPython yanıt](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="f7efc-445">Merhaba için iki (Merhaba JSON framework hello python komut) biz sorulan hakkında örnekler test bkz, biz geri hello formunda "Scored etiketleri, Scored olasılıklar" cevaplar.</span><span class="sxs-lookup"><span data-stu-id="f7efc-445">We see that for hello two test examples we asked about (in hello JSON framework of hello python script), we get back answers in hello form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="f7efc-446">Bu durumda, biz hello varsayılan değerleri hello önceden tamamlanmış kod seçtiğiniz Not (0'ların tüm sayısal sütunlar ve hello dize tüm kategorik sütunlar için "value") sağlar.</span><span class="sxs-lookup"><span data-stu-id="f7efc-446">Note that in this case, we chose hello default values that hello pre-canned code provides (0's for all numeric columns and hello string "value" for all categorical columns).</span></span>

<span data-ttu-id="f7efc-447">Bu bizim uçtan uca kılavuz gösteren sonucuna nasıl Azure Machine Learning kullanarak toohandle büyük ölçekli veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="f7efc-447">This concludes our end-to-end walkthrough showing how toohandle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="f7efc-448">Biz verilerin bir terabayt başlatıldı, bir tahmin modeli oluşturulan ve hello bulutta bir web hizmeti olarak dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="f7efc-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in hello cloud.</span></span>

