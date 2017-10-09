---
title: "bir Hadoop aaaExplore veri kümesi ve Azure Machine Learning modellerini oluşturun | Microsoft Docs"
description: "Bir Hdınsight Hadoop kullanan bir uçtan uca senaryo için Hello takım veri bilimi işlemi kullanarak toobuild küme ve genel kullanıma açık bir veri kümesini kullanarak bir modeli dağıtın."
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="6aa04-103">eylemin Hello takım veri bilimi işlemi: kullanım Azure Hdınsight Hadoop kümeleri</span><span class="sxs-lookup"><span data-stu-id="6aa04-103">hello Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="6aa04-104">Bu kılavuzda, kullandığımız hello [takım veri bilimi işlem (TDSP)](data-science-process-overview.md) bir uçtan uca senaryoyu kullanarak bir [Azure Hdınsight Hadoop kümesi](https://azure.microsoft.com/services/hdinsight/) toostore, araştırın ve özellik hello mühendislik verileri genel olarak kullanılabilir [NYC ücreti dönüşleri](http://www.andresmh.com/nyctaxitrips/) hello veri örnek veri kümesi ve toodown.</span><span class="sxs-lookup"><span data-stu-id="6aa04-104">In this walkthrough, we use hello [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore and feature engineer data from hello publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and toodown sample hello data.</span></span> <span data-ttu-id="6aa04-105">Merhaba veri modellerinin Azure Machine Learning toohandle çok sınıflı ve ikili sınıflandırma ve regresyon Tahmine dayalı görevlerle oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6aa04-105">Models of hello data are built with Azure Machine Learning toohandle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="6aa04-106">Gösteren nasıl toohandle veri işleme için Hdınsight Hadoop kullanarak benzer bir senaryo için daha büyük bir (1 terabayttan küçük) veri kümeleri için bkz [takım veri bilimi işlem - 1 TB veri kümesiüzerindeAzureHdınsightHadoopkümelerikullanarak](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="6aa04-106">For a walkthrough that shows how toohandle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="6aa04-107">Olası toouse IPython not defteri tooaccomplish hello hello 1 TB veri kümesini kullanarak sunulan hello izlenecek görevler de olabilir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented hello walkthrough using hello 1 TB dataset.</span></span> <span data-ttu-id="6aa04-108">Bu yaklaşım başvurun tootry gibi hello kullanıcılar [Criteo izlenecek bir Hive ODBC bağlantısı kullanarak](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) konu.</span><span class="sxs-lookup"><span data-stu-id="6aa04-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="6aa04-109"><a name="dataset"></a>NYC ücreti dönüşleri Dataset açıklaması</span><span class="sxs-lookup"><span data-stu-id="6aa04-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="6aa04-110">Merhaba NYC ücreti seyahat veri yaklaşık 20 GB sıkıştırılmış virgülle ayrılmış değerler (CSV) dosyaları (~ 48 GB sıkıştırılmamış), 173 milyondan fazla kapsayan tek tek dönüşleri ve hello fares her seyahat için ücretli.</span><span class="sxs-lookup"><span data-stu-id="6aa04-110">hello NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="6aa04-111">Her seyahat kayıt hello alma ve teslim konumu ve zaman, anonim korsan (sürücü) lisans numarası ve medallion (ücreti'nın benzersiz kimliği) numarasını içerir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-111">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="6aa04-112">Merhaba veri hello yıl 2013 tüm dönüşleri kapsayan ve her ay için iki veri kümesi aşağıdaki hello sağlanır:</span><span class="sxs-lookup"><span data-stu-id="6aa04-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="6aa04-113">Merhaba 'trip_data' CSV dosyaları yolcu, toplama ve dropoff noktaları, seyahat süresi ve seyahat Uzunluk sayısı gibi seyahat ayrıntıları içerir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-113">hello 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="6aa04-114">Birkaç örnek kayıt şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6aa04-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="6aa04-115">Merhaba 'trip_fare' CSV dosyaları için ödeme türü, ücreti tutarı, ek ücret ve vergileri, ipuçları ve tolls ve Ücretli hello toplam miktarı gibi her seyahat Ücretli hello ücreti ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-115">hello 'trip_fare' CSV files contain details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="6aa04-116">Birkaç örnek kayıt şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6aa04-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="6aa04-117">Merhaba benzersiz anahtar toojoin seyahat\_veri ve seyahat\_ücreti hello alanlarının oluşur: medallion, korsan\_lisans ve alma\_datetime.</span><span class="sxs-lookup"><span data-stu-id="6aa04-117">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="6aa04-118">Tüm tooget hello ayrıntıları ilgili tooa belirli seyahat, yeterli toojoin üç anahtarlara sahip olduğu: "medallion" Merhaba "korsan saldırılarına\_lisans" ve "alma\_datetime".</span><span class="sxs-lookup"><span data-stu-id="6aa04-118">tooget all of hello details relevant tooa particular trip, it is sufficient toojoin with three keys: hello "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="6aa04-119">Bunları Hive tablolara kısa süre içinde depolarız zaman biz hello veri bazı ayrıntılar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-119">We describe some more details of hello data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="6aa04-120"><a name="mltasks"></a>Tahmin görev örnekleri</span><span class="sxs-lookup"><span data-stu-id="6aa04-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="6aa04-121">Veri yaklaşan, kendi analize dayalı toomake istediğiniz tahminleri hello tür belirleme işleminize tooinclude gerekir hello görevleri açıklamak yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="6aa04-121">When approaching data, determining hello kind of predictions you want toomake based on its analysis helps clarify hello tasks that you will need tooinclude in your process.</span></span>
<span data-ttu-id="6aa04-122">Biz bu kılavuzda, formülasyonu hello üzerinde temel adres tahmin sorunları üç örnekler *İpucu\_tutar*:</span><span class="sxs-lookup"><span data-stu-id="6aa04-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on hello *tip\_amount*:</span></span>

1. <span data-ttu-id="6aa04-123">**İkili sınıflandırma**: bir ipucu bir seyahat, yani ödenmiş olup olmadığına bakılmaksızın tahmin bir *İpucu\_tutar* büyük $0 pozitif bir örnektir küçük, ancak bir *İpucu\_tutar* 0 / negatif bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="6aa04-124">**Çok sınıflı sınıflandırma**: toopredict hello ipucu tutarlar aralığını Ücretli hello seyahat için.</span><span class="sxs-lookup"><span data-stu-id="6aa04-124">**Multiclass classification**: toopredict hello range of tip amounts paid for hello trip.</span></span> <span data-ttu-id="6aa04-125">Biz hello bölmek *İpucu\_tutar* beş depo veya sınıfları:</span><span class="sxs-lookup"><span data-stu-id="6aa04-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="6aa04-126">**Regresyon görev**: seyahat için ödenen hello ucunun toopredict hello tutar.</span><span class="sxs-lookup"><span data-stu-id="6aa04-126">**Regression task**: toopredict hello amount of hello tip paid for a trip.</span></span>  

## <span data-ttu-id="6aa04-127"><a name="setup"></a>Bir Hdınsight Hadoop kümesi gelişmiş analizler için ayarlama</span><span class="sxs-lookup"><span data-stu-id="6aa04-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-128">Bu genellikle olur bir **yönetici** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-129">Bir Azure ortamı üç adımda Hdınsight kümesi kullanan gelişmiş analiz için ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6aa04-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="6aa04-130">[Depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md): verileri Azure Blob Storage'da depolamak için bu depolama hesabı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="6aa04-131">Hdınsight kümelerinde kullanılan hello verileri da buradadır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-131">hello data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="6aa04-132">[Azure Hdınsight Hadoop özelleştirme Advanced Analytics işlemi ve teknoloji kümeleri Merhaba](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6aa04-132">[Customize Azure HDInsight Hadoop clusters for hello Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="6aa04-133">Bu adım, 64-bit Anaconda Python 2.7 kümeyle tüm düğümlerde yüklü bir Azure Hdınsight Hadoop oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6aa04-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="6aa04-134">Hdınsight kümenizi özelleştirilirken iki önemli adımlar tooremember vardır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-134">There are two important steps tooremember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="6aa04-135">Onu oluştururken Hdınsight kümenize ile 1. adımda oluşturulan toolink hello depolama hesabı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6aa04-135">Remember toolink hello storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="6aa04-136">Bu depolama hesabını hello küme içinde işlenir kullanılan tooaccess verilerdir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-136">This storage account is used tooaccess data that is processed within hello cluster.</span></span>
   * <span data-ttu-id="6aa04-137">Merhaba Küme oluşturulduktan sonra uzaktan erişim toohello hello küme baş düğümüne etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6aa04-137">After hello cluster is created, enable Remote Access toohello head node of hello cluster.</span></span> <span data-ttu-id="6aa04-138">Toohello gidin **yapılandırma** sekmesinde **etkinleştirmek uzak**.</span><span class="sxs-lookup"><span data-stu-id="6aa04-138">Navigate toohello **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="6aa04-139">Bu adım, uzak oturum açma için kullanılan hello kullanıcı kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-139">This step specifies hello user credentials used for remote login.</span></span>
3. <span data-ttu-id="6aa04-140">[Bir Azure Machine Learning çalışma alanı oluşturma](machine-learning-create-workspace.md): Bu Azure Machine Learning çalışma alanı kullanılan toobuild machine learning modellerini alanıdır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used toobuild machine learning models.</span></span> <span data-ttu-id="6aa04-141">Bu görev, ilk veri keşfi tamamladıktan sonra ve hello Hdınsight kümesi kullanarak örnekleme aşağı değinilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-141">This task is addressed after completing an initial data exploration and down sampling using hello HDInsight cluster.</span></span>

## <span data-ttu-id="6aa04-142"><a name="getdata"></a>Ortak bir kaynaktan Hello Veri Al</span><span class="sxs-lookup"><span data-stu-id="6aa04-142"><a name="getdata"></a>Get hello data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-143">Bu genellikle olur bir **yönetici** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-144">tooget hello [NYC ücreti dönüşleri](http://www.andresmh.com/nyctaxitrips/) dataset ortak konumundan kullandığınız açıklanan hello yöntemlerden herhangi birini [Azure Blob depolama biriminden verileri Taşı tooand](machine-learning-data-science-move-azure-blob.md) toocopy hello veri tooyour makine.</span><span class="sxs-lookup"><span data-stu-id="6aa04-144">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour machine.</span></span>

<span data-ttu-id="6aa04-145">Burada nasıl kullanım AzCopy tootransfer hello verileri içeren dosyalar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-145">Here we describe how use AzCopy tootransfer hello files containing data.</span></span> <span data-ttu-id="6aa04-146">toodownload ve AzCopy yükleme sırasında hello yönergeleri izleyerek [hello AzCopy komut satırı yardımcı programı ile çalışmaya başlama](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="6aa04-146">toodownload and install AzCopy follow hello instructions at [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="6aa04-147">Bir komut istemi penceresinden aşağıdaki AzCopy komutları, değiştirme hello sorun *< path_to_data_folder >* hello istenen hedefle:</span><span class="sxs-lookup"><span data-stu-id="6aa04-147">From a Command Prompt window, issue hello following AzCopy commands, replacing *<path_to_data_folder>* with hello desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="6aa04-148">Merhaba kopyalama tamamlandıktan sonra toplam 24 sıkıştırılmış dosya seçilen hello veri klasörü şunlardır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-148">When hello copy completes, a total of 24 zipped files are in hello data folder chosen.</span></span> <span data-ttu-id="6aa04-149">Merhaba indirilen dosyaları toohello sıkıştırmasını yerel makinenizde aynı dizin.</span><span class="sxs-lookup"><span data-stu-id="6aa04-149">Unzip hello downloaded files toohello same directory on your local machine.</span></span> <span data-ttu-id="6aa04-150">Sıkıştırılmamış hello dosyalarının bulunduğu hello klasörü not edin.</span><span class="sxs-lookup"><span data-stu-id="6aa04-150">Make a note of hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="6aa04-151">Bu klasör başvurulan tooas hello olacaktır *< yol\_için\_unzipped_data\_dosyaları\>*  aşağıda değil.</span><span class="sxs-lookup"><span data-stu-id="6aa04-151">This folder will be referred tooas hello *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="6aa04-152"><a name="upload"></a>Merhaba veri toohello varsayılan kapsayıcı Azure Hdınsight Hadoop kümesi karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="6aa04-152"><a name="upload"></a>Upload hello data toohello default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-153">Bu genellikle olur bir **yönetici** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-154">Hello aşağıdaki AzCopy komutları, şu parametreler hello Hadoop kümesi oluştururken belirttiğiniz hello gerçek değerlerle ve hello veri dosyalarını şunu hello yerini alır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-154">In hello following AzCopy commands, replace hello following parameters with hello actual values that you specified when creating hello Hadoop cluster and unzipping hello data files.</span></span>

* <span data-ttu-id="6aa04-155">***&#60; path_to_data_folder >*** makinenizde sıkıştırması açılmış hello veri dosyalarını içeren hello dizin (birlikte yolu)</span><span class="sxs-lookup"><span data-stu-id="6aa04-155">***&#60;path_to_data_folder>*** hello directory (along with path) on your machine that contain hello unzipped data files</span></span>  
* <span data-ttu-id="6aa04-156">***&#60; Hadoop küme depolama hesap adı >*** hello Hdınsight kümenizle ilişkilendirilmiş depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="6aa04-156">***&#60;storage account name of Hadoop cluster>*** hello storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="6aa04-157">***&#60; varsayılan kapsayıcı Hadoop küme >*** , küme tarafından kullanılan hello varsayılan kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="6aa04-157">***&#60;default container of Hadoop cluster>*** hello default container used by your cluster.</span></span> <span data-ttu-id="6aa04-158">Bu hello adını not edin hello varsayılan genellikle aynı adı hello küme olarak kendisi hello kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-158">Note that hello name of hello default container is usually hello same name as hello cluster itself.</span></span> <span data-ttu-id="6aa04-159">Örneğin, "abc123.azurehdinsight.net" Merhaba küme çağrılırsa, hello varsayılan kapsayıcı abc123 ' dir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-159">For example, if hello cluster is called "abc123.azurehdinsight.net", hello default container is abc123.</span></span>
* <span data-ttu-id="6aa04-160">***&#60; depolama hesabı anahtarı >*** hello depolama hesabının, küme tarafından kullanılan başlangıç anahtarı</span><span class="sxs-lookup"><span data-stu-id="6aa04-160">***&#60;storage account key>*** hello key for hello storage account used by your cluster</span></span>

<span data-ttu-id="6aa04-161">Bir komut istemi veya makinenizde bir Windows PowerShell penceresinde, aşağıdaki iki AzCopy komut hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6aa04-161">From a Command Prompt or a Windows PowerShell window in your machine, run hello following two AzCopy commands.</span></span>

<span data-ttu-id="6aa04-162">Bu komut hello seyahat veri çok yükler***nyctaxitripraw*** hello Hadoop kümesi hello varsayılan kapsayıcısında dizin.</span><span class="sxs-lookup"><span data-stu-id="6aa04-162">This command uploads hello trip data too***nyctaxitripraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="6aa04-163">Bu komut hello ücreti verileri çok yükler***nyctaxifareraw*** hello Hadoop kümesi hello varsayılan kapsayıcısında dizin.</span><span class="sxs-lookup"><span data-stu-id="6aa04-163">This command uploads hello fare data too***nyctaxifareraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="6aa04-164">Hello verileri Azure Blob Storage ve hello Hdınsight küme içinde tüketilen hazır toobe şimdi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-164">hello data should now in Azure Blob Storage and ready toobe consumed within hello HDInsight cluster.</span></span>

## <span data-ttu-id="6aa04-165"><a name="#download-hql-files"></a>Hadoop küme baş düğümüne hello günlüğüne ve ve keşif veri analizi için hazırlama</span><span class="sxs-lookup"><span data-stu-id="6aa04-165"><a name="#download-hql-files"></a>Log into hello head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-166">Bu genellikle olur bir **yönetici** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-167">Merhaba kümesinin keşif veri analizi için ve hello veri örnekleme aşağı tooaccess hello baş düğümü özetlenen hello yordamı izleyin [erişim hello Hadoop kümesi, baş düğüm](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="6aa04-167">tooaccess hello head node of hello cluster for exploratory data analysis and down sampling of hello data, follow hello procedure outlined in [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="6aa04-168">Bu kılavuzda, öncelikli olarak yazılmış sorguları kullanırız [Hive](https://hive.apache.org/), bir SQL benzeri sorgu dili, tooperform ön veri explorations.</span><span class="sxs-lookup"><span data-stu-id="6aa04-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, tooperform preliminary data explorations.</span></span> <span data-ttu-id="6aa04-169">Merhaba Hive sorguları .hql dosyalarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-169">hello Hive queries are stored in .hql files.</span></span> <span data-ttu-id="6aa04-170">Biz ardından aşağı içinde Azure Machine Learning modeli oluşturmak için kullanılan bu veri toobe örnek.</span><span class="sxs-lookup"><span data-stu-id="6aa04-170">We then down sample this data toobe used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="6aa04-171">tooprepare hello küme keşif veri analizi için biz karşıdan hello ilgili Hive komut dosyalarını içeren hello .hql dosyaları [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) hello baş düğümünde tooa yerel dizin (C:\temp).</span><span class="sxs-lookup"><span data-stu-id="6aa04-171">tooprepare hello cluster for exploratory data analysis, we download hello .hql files containing hello relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa local directory (C:\temp) on hello head node.</span></span> <span data-ttu-id="6aa04-172">toodo Bu, açık hello **komut istemi** içinden aşağıdaki iki komutu hello küme ve sorunu hello baş düğümüne hello:</span><span class="sxs-lookup"><span data-stu-id="6aa04-172">toodo this, open hello **Command Prompt** from within hello head node of hello cluster and issue hello following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="6aa04-173">Bu iki komutu bu izlenecek yol toohello yerel dizinde gerekli tüm .hql dosyaları indirir ***C:\temp &#92;*** hello baş düğümünde.</span><span class="sxs-lookup"><span data-stu-id="6aa04-173">These two commands will download all .hql files needed in this walkthrough toohello local directory ***C:\temp&#92;*** in hello head node.</span></span>

## <span data-ttu-id="6aa04-174"><a name="#hive-db-tables"></a>Hive veritabanı ve aya göre bölümlenmiş tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="6aa04-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-175">Bu genellikle olur bir **yönetici** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-176">Şimdi hazır toocreate Hive tablolarını bizim NYC ücreti veri kümesi için duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="6aa04-176">We are now ready toocreate Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="6aa04-177">Merhaba Hello baş düğümünde hello Hadoop kümesi, açık ***Hadoop komut satırı*** üzerinde hello Masaüstü hello baş düğümü ve hello komutunu girerek hello Hive dizini girin</span><span class="sxs-lookup"><span data-stu-id="6aa04-177">In hello head node of hello Hadoop cluster, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="6aa04-178">**Bu kılavuzda Hive depo yukarıda hello tüm Hive komutları çalıştırma / directory istemi. Bu yol sorunları otomatik olarak ilgilenebilmek. "Hive dizin istemi" Merhaba terimleri kullanırız "Hive bin / directory istemi" ve bu kılavuzda birbirinin yerine "Hadoop komut satırı".**</span><span class="sxs-lookup"><span data-stu-id="6aa04-178">**Run all Hive commands in this walkthrough from hello above Hive bin/ directory prompt. This will take care of any path issues automatically. We use hello terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="6aa04-179">Merhaba Hive dizin isteminden komutu Hadoop komut satırı hello baş düğüm toosubmit hello Hive sorgusu toocreate Hive veritabanı ve tablo aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="6aa04-179">From hello Hive directory prompt, enter hello following command in Hadoop Command Line of hello head node toosubmit hello Hive query toocreate Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="6aa04-180">Merhaba Merhaba içeriğine işte ***C:\temp\sample\_hive\_oluşturma\_db\_ve\_tables.hql*** Hive veritabanı oluşturan dosya ***nyctaxidb *** ve tabloları ***seyahat*** ve ***ücreti***.</span><span class="sxs-lookup"><span data-stu-id="6aa04-180">Here is hello content of hello ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

    create database if not exists nyctaxidb;

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
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

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
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

<span data-ttu-id="6aa04-181">Bu Hive betiğini iki tablo oluşturur:</span><span class="sxs-lookup"><span data-stu-id="6aa04-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="6aa04-182">Merhaba "seyahat" tablo her kıl (sürücü ayrıntıları, toplama zaman, seyahat uzaklığı ve) seyahat ayrıntılarını içerir</span><span class="sxs-lookup"><span data-stu-id="6aa04-182">hello "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="6aa04-183">Merhaba "ücreti" tablosu ücreti ayrıntıları (ücreti tutarı, ipucu tutarı, tolls ve ek talepler) içerir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-183">hello "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="6aa04-184">Bu yordamları ile ek yardıma gereksinim veya tooinvestigate alternatif olanları istiyorsanız hello bölümüne bakın [gönderme Hive sorguları doğrudan gelen hello Hadoop komut satırı ](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="6aa04-184">If you need any additional assistance with these procedures or want tooinvestigate alternative ones, see hello section [Submit Hive queries directly from hello Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="6aa04-185"><a name="#load-data"></a>Bölümler tarafından veri tooHive tablolar yüklenemiyor</span><span class="sxs-lookup"><span data-stu-id="6aa04-185"><a name="#load-data"></a>Load Data tooHive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-186">Bu genellikle olur bir **yönetici** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-187">doğal tooenable daha hızlı işleme ve sorgu süreleri kullanırız aya göre bölümleme Hello NYC ücreti veri kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-187">hello NYC taxi dataset has a natural partitioning by month, which we use tooenable faster processing and query times.</span></span> <span data-ttu-id="6aa04-188">Aşağıdaki PowerShell komutları hello (Merhaba Hive dizininden hello kullanarak verilen **Hadoop komut satırı**) aya göre bölümlenmiş veri toohello "seyahat" ve "ücreti" Hive tabloları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6aa04-188">hello PowerShell commands below (issued from hello Hive directory using hello **Hadoop Command Line**) load data toohello "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="6aa04-189">Merhaba *örnek\_hive\_yük\_veri\_tarafından\_partitions.hql* dosyasını içeren hello aşağıdaki **yük** komutları.</span><span class="sxs-lookup"><span data-stu-id="6aa04-189">hello *sample\_hive\_load\_data\_by\_partitions.hql* file contains hello following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="6aa04-190">Merhaba araştırması işleminde burada kullandığımız Hive sorguları bir dizi yalnızca tek bir bölüm veya yalnızca birkaç bölümlerinin aramayı içeren unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6aa04-190">Note that a number of Hive queries we use here in hello exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="6aa04-191">Ancak bu sorgular arasında hello tüm verileri çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6aa04-191">But these queries could be run across hello entire data.</span></span>

### <span data-ttu-id="6aa04-192"><a name="#show-db"></a>Merhaba Hdınsight Hadoop kümesi veritabanları Göster</span><span class="sxs-lookup"><span data-stu-id="6aa04-192"><a name="#show-db"></a>Show databases in hello HDInsight Hadoop cluster</span></span>
<span data-ttu-id="6aa04-193">Hdınsight Hadoop kümesi hello Hadoop komut satırı penceresinde, aşağıdaki komut, Hadoop komut satırı hello çalıştırın içinde oluşturulan tooshow hello veritabanlarını:</span><span class="sxs-lookup"><span data-stu-id="6aa04-193">tooshow hello databases created in HDInsight Hadoop cluster inside hello Hadoop Command Line window, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="6aa04-194"><a name="#show-tables"></a>Merhaba nyctaxidb veritabanında Hello Hive tabloları göster</span><span class="sxs-lookup"><span data-stu-id="6aa04-194"><a name="#show-tables"></a>Show hello Hive tables in hello nyctaxidb database</span></span>
<span data-ttu-id="6aa04-195">tooshow hello tablolar hello nyctaxidb veritabanında, aşağıdaki komut, Hadoop komut satırı hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6aa04-195">tooshow hello tables in hello nyctaxidb database, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="6aa04-196">Merhaba tabloları aşağıdaki hello komutu vererek bölümlenir olduğunu doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6aa04-196">We can confirm that hello tables are partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="6aa04-197">Merhaba, çıktı aşağıda gösterilen beklenen:</span><span class="sxs-lookup"><span data-stu-id="6aa04-197">hello expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

<span data-ttu-id="6aa04-198">Benzer şekilde, aşağıdaki hello komutu vererek bu hello ücreti tablonun bölümlenme sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6aa04-198">Similarly, we can ensure that hello fare table is partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="6aa04-199">Merhaba, çıktı aşağıda gösterilen beklenen:</span><span class="sxs-lookup"><span data-stu-id="6aa04-199">hello expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <span data-ttu-id="6aa04-200"><a name="#explore-hive"></a>Veri keşfi ve Hive özellik Mühendisliği</span><span class="sxs-lookup"><span data-stu-id="6aa04-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-201">Bu genellikle olur bir **veri Bilimcisi** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-202">Veri keşfi hello ve Hive sorguları kullanarak veri hello Hive tablolara yüklenen gerçekleştirilebilir hello mühendislik görevlerde özellik.</span><span class="sxs-lookup"><span data-stu-id="6aa04-202">hello data exploration and feature engineering tasks for hello data loaded into hello Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="6aa04-203">Gibi görevleri biz, bu bölümde size yol olduğunu örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6aa04-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="6aa04-204">Her iki tabloda Hello üst 10 kayıtları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="6aa04-204">View hello top 10 records in both tables.</span></span>
* <span data-ttu-id="6aa04-205">Veri dağıtımları değişen zaman pencereleri birkaç alanların keşfedin.</span><span class="sxs-lookup"><span data-stu-id="6aa04-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="6aa04-206">Veri Kalitesi hello boylam ve enlem alanlarının araştırın.</span><span class="sxs-lookup"><span data-stu-id="6aa04-206">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="6aa04-207">Merhaba üzerinde dayalı çok sınıflı ve ikili sınıflandırma etiketleri oluşturmak **İpucu\_tutar**.</span><span class="sxs-lookup"><span data-stu-id="6aa04-207">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="6aa04-208">Özellikler hello doğrudan seyahat uzaklıklar bilgi işlem tarafından oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6aa04-208">Generate features by computing hello direct trip distances.</span></span>

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a><span data-ttu-id="6aa04-209">Keşfetme: hello üst 10 kayıt tablo seyahat görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="6aa04-209">Exploration: View hello top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-210">Bu genellikle olur bir **veri Bilimcisi** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-211">hangi hello verilerin benzer toosee her tablodan 10 kayıt inceleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="6aa04-211">toosee what hello data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="6aa04-212">İki sorguları hello Hive dizin isteminde hello Hadoop komut satırı konsol tooinspect hello kayıtlarında ayrı olarak aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6aa04-212">Run hello following two queries separately from hello Hive directory prompt in hello Hadoop Command Line console tooinspect hello records.</span></span>

<span data-ttu-id="6aa04-213">tooget ilk ay Merhaba tablonun "seyahat" Merhaba gelen üst 10 kayıtları hello:</span><span class="sxs-lookup"><span data-stu-id="6aa04-213">tooget hello top 10 records in hello table "trip" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="6aa04-214">tooget hello üst 10 kayıt hello ilk ay öğesinden "ücreti" Merhaba tablosundaki:</span><span class="sxs-lookup"><span data-stu-id="6aa04-214">tooget hello top 10 records in hello table "fare" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="6aa04-215">Bu genellikle yararlı toosave hello kayıtları tooa kolay görüntüleme için dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-215">It is often useful toosave hello records tooa file for convenient viewing.</span></span> <span data-ttu-id="6aa04-216">Küçük değişiklik toohello sorgu yukarıda bunu gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="6aa04-216">A small change toohello above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a><span data-ttu-id="6aa04-217">Keşfetme: Görünümü hello her hello 12 bölüm kayıt sayısı</span><span class="sxs-lookup"><span data-stu-id="6aa04-217">Exploration: View hello number of records in each of hello 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-218">Bu genellikle olur bir **veri Bilimcisi** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-219">Dönüş hello sayısı hello takvim yılı sırasında nasıl değişeceğini hello ilginizi çekecektir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-219">Of interest is hello how hello number of trips varies during hello calendar year.</span></span> <span data-ttu-id="6aa04-220">Aya göre gruplandırma sağlayan bize toosee dönüşleri bu dağıtımını benzer.</span><span class="sxs-lookup"><span data-stu-id="6aa04-220">Grouping by month allows us toosee what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="6aa04-221">Bu bize hello çıkış sunar:</span><span class="sxs-lookup"><span data-stu-id="6aa04-221">This gives us hello output :</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

<span data-ttu-id="6aa04-222">Burada, hello ilk sütun hello ay ve hello ikinci dönüş hello sayısı söz konusu ay.</span><span class="sxs-lookup"><span data-stu-id="6aa04-222">Here, hello first column is hello month and hello second is hello number of trips for that month.</span></span>

<span data-ttu-id="6aa04-223">Biz de hello toplam kayıt sayısı, hello Hive dizin isteminde komutu aşağıdaki hello vererek bizim seyahat veri kümesinde sayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6aa04-223">We can also count hello total number of records in our trip data set by issuing hello following command at hello Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="6aa04-224">Bu verir:</span><span class="sxs-lookup"><span data-stu-id="6aa04-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="6aa04-225">Merhaba seyahat veri kümesi için gösterilen komutları benzer toothose kullanarak Hive sorguları hello Hive dizin isteminde hello ücreti veri kümesi toovalidate hello kayıt sayısı için verebilir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-225">Using commands similar toothose shown for hello trip data set, we can issue Hive queries from hello Hive directory prompt for hello fare data set toovalidate hello number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="6aa04-226">Bu bize hello çıkış sunar:</span><span class="sxs-lookup"><span data-stu-id="6aa04-226">This gives us hello output:</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

<span data-ttu-id="6aa04-227">Hello tam aynı dönüş sayısı her ay için her iki veri kümesi verdiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6aa04-227">Note that hello exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="6aa04-228">Bu, verileri doğru şekilde yüklendiğinden bu hello hello ilk doğrulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="6aa04-228">This provides hello first validation that hello data has been loaded correctly.</span></span>

<span data-ttu-id="6aa04-229">Merhaba ücreti veri kümesindeki kayıtları toplam sayısı Hello sayım yapılabilir hello Hive dizin isteminden aşağıdaki hello komutunu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="6aa04-229">Counting hello total number of records in hello fare data set can be done using hello command below from hello Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="6aa04-230">Bu verir:</span><span class="sxs-lookup"><span data-stu-id="6aa04-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="6aa04-231">Her iki tablodaki kayıtlarının toplam sayısını Hello olduğunu da hello aynı.</span><span class="sxs-lookup"><span data-stu-id="6aa04-231">hello total number of records in both tables is also hello same.</span></span> <span data-ttu-id="6aa04-232">Bu, verileri doğru şekilde yüklendiğinden bu hello ikinci doğrulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="6aa04-232">This provides a second validation that hello data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="6aa04-233">Araştırması: Medallion seyahat dağıtım</span><span class="sxs-lookup"><span data-stu-id="6aa04-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-234">Bu genellikle olur bir **veri Bilimcisi** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-235">Bu örnek, belirli bir süre içinde ile 100'den fazla dönüşleri hello medallion (ücreti sayılar) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6aa04-235">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="6aa04-236">Hello sorgu avantajları hello gelen bölümlenmiş tabloda erişim hello bölüm değişkeniyle söylediğinizde beri **ay**.</span><span class="sxs-lookup"><span data-stu-id="6aa04-236">hello query benefits from hello partitioned table access since it is conditioned by hello partition variable **month**.</span></span> <span data-ttu-id="6aa04-237">Merhaba sorgu sonuçları dilini tooa yerel dosya queryoutput.tsv `C:\temp` hello baş düğüm üzerinde.</span><span class="sxs-lookup"><span data-stu-id="6aa04-237">hello query results are written tooa local file queryoutput.tsv in `C:\temp` on hello head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="6aa04-238">Merhaba içeriğine işte *örnek\_hive\_seyahat\_sayısı\_tarafından\_medallion.hql* İnceleme için dosya.</span><span class="sxs-lookup"><span data-stu-id="6aa04-238">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="6aa04-239">Merhaba medallion hello NYC ücreti veri kümesindeki bir benzersiz cab tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6aa04-239">hello medallion in hello NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="6aa04-240">Hangi cab hangilerinin belirli bir süre içinde birden çok belirli bir sayıda dönüşleri yapılan isteyerek "meşgul" ayırt edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6aa04-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="6aa04-241">Merhaba aşağıdaki örnek tanımlar birden fazla yüzlerce dönüşleri hello ilk üç ay yapılan cab dosyaları ve sorgu sonuçları tooa yerel dosya, C:\temp\queryoutput.tsv kaydeder hello.</span><span class="sxs-lookup"><span data-stu-id="6aa04-241">hello following example identifies cabs that made more than a hundred trips in hello first three months, and saves hello query results tooa local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="6aa04-242">Merhaba içeriğine işte *örnek\_hive\_seyahat\_sayısı\_tarafından\_medallion.hql* İnceleme için dosya.</span><span class="sxs-lookup"><span data-stu-id="6aa04-242">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="6aa04-243">Hello dizin istemi, aşağıdaki sorun hello komutu yığını:</span><span class="sxs-lookup"><span data-stu-id="6aa04-243">From hello Hive directory prompt, issue hello command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="6aa04-244">Keşfetme: dağıtım medallion ve hack_license tarafından seyahat</span><span class="sxs-lookup"><span data-stu-id="6aa04-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-245">Bu genellikle olur bir **veri Bilimcisi** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-246">Bir veri kümesi keşfetme, sık tooexamine hello co-örnek değerler gruplarının sayısına istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6aa04-246">When exploring a dataset, we frequently want tooexamine hello number of co-occurences of groups of values.</span></span> <span data-ttu-id="6aa04-247">Bu bölüm bir örnek nasıl toodo Bu dolap ve sürücüleri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="6aa04-247">This section provide an example of how toodo this for cabs and drivers.</span></span>

<span data-ttu-id="6aa04-248">Merhaba *örnek\_hive\_seyahat\_sayısı\_tarafından\_medallion\_license.hql* dosya grupları "medallion" ve "hack_license" Merhaba ücreti verileri ve her birleşim sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="6aa04-248">hello *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups hello fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="6aa04-249">İçeriğini aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="6aa04-250">Bu sorgu, cab ve dönüş azalan sayısına göre sıralanmış belirli sürücü birleşimleriyle döndürür.</span><span class="sxs-lookup"><span data-stu-id="6aa04-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="6aa04-251">Dizin istemi Hello Hive, çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6aa04-251">From hello Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="6aa04-252">Merhaba sorgu sonuçları tooa yerel dosya C:\temp\queryoutput.tsv yazılır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-252">hello query results are written tooa local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="6aa04-253">Araştırması: Geçersiz boylam/enlem kayıtlarını denetleyerek veri kalitesini değerlendirme</span><span class="sxs-lookup"><span data-stu-id="6aa04-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-254">Bu genellikle olur bir **veri Bilimcisi** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-255">Ortak amacı keşif veri analizi, geçersiz veya hatalı kayıt çıkışı tooweed ' dir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-255">A common objective of exploratory data analysis is tooweed out invalid or bad records.</span></span> <span data-ttu-id="6aa04-256">Merhaba bu bölümdeki örnek ya da hello boylam veya enlem alanları kadar hello NYC alanı dışında bir değer içeren olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="6aa04-256">hello example in this section determines whether either hello longitude or latitude fields contain a value far outside hello NYC area.</span></span> <span data-ttu-id="6aa04-257">Bu tür kayıtları bir hatalı boylam enlem değerlere sahip olası olduğundan, bunları toobe olan herhangi bir veri modelleme için kullanılan tooeliminate istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6aa04-257">Since it is likely that such records have an erroneous longitude-latitude values, we want tooeliminate them from any data that is toobe used for modeling.</span></span>

<span data-ttu-id="6aa04-258">Merhaba içeriğine işte *örnek\_hive\_kalite\_assessment.hql* İnceleme için dosya.</span><span class="sxs-lookup"><span data-stu-id="6aa04-258">Here is hello content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="6aa04-259">Dizin istemi Hello Hive, çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6aa04-259">From hello Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="6aa04-260">Merhaba *-S* Bu komutta yer alan bağımsız değişkeni hello durum ekran hello harita/azaltın Hive işleri çıktısını gizler.</span><span class="sxs-lookup"><span data-stu-id="6aa04-260">hello *-S* argument included in this command suppresses hello status screen printout of hello Hive Map/Reduce jobs.</span></span> <span data-ttu-id="6aa04-261">Merhaba ekran Yazdır hello Hive sorgusu çıktıyı daha okunabilir hale getirir çünkü bu yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="6aa04-261">This is useful because it makes hello screen print of hello Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="6aa04-262">Araştırması: Seyahat ipuçları ikili sınıfı dağıtımları</span><span class="sxs-lookup"><span data-stu-id="6aa04-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-263">Bu genellikle olur bir **veri Bilimcisi** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-264">Hello özetlenen hello ikili sınıflandırma sorunu için [tahmin görev örnekleri](machine-learning-data-science-process-hive-walkthrough.md#mltasks) bölümüne bir ipucu veya verilen bu yararlı tooknow olup.</span><span class="sxs-lookup"><span data-stu-id="6aa04-264">For hello binary classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful tooknow whether a tip was given or not.</span></span> <span data-ttu-id="6aa04-265">Bu dağıtımı ipuçları, ikili şöyledir:</span><span class="sxs-lookup"><span data-stu-id="6aa04-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="6aa04-266">verilen İpucu (sınıf 1, İpucu\_> $0 tutar)</span><span class="sxs-lookup"><span data-stu-id="6aa04-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="6aa04-267">İpucu yok (sınıfı 0, İpucu\_tutar = $0).</span><span class="sxs-lookup"><span data-stu-id="6aa04-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="6aa04-268">Merhaba *örnek\_hive\_Eğimli\_frequencies.hql* aşağıda gösterilen dosya yapar.</span><span class="sxs-lookup"><span data-stu-id="6aa04-268">hello *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="6aa04-269">Dizin istemi Hello Hive, çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6aa04-269">From hello Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a><span data-ttu-id="6aa04-270">Araştırması: Merhaba çok sınıflı ayarında sınıf dağıtımları</span><span class="sxs-lookup"><span data-stu-id="6aa04-270">Exploration: Class distributions in hello multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-271">Bu genellikle olur bir **veri Bilimcisi** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-272">Hello özetlenen hello çok sınıflı sınıflandırma sorunu için [tahmin görev örnekleri](machine-learning-data-science-process-hive-walkthrough.md#mltasks) bölümünde bu veri kümesi de tooa doğal sınıflandırma burada biz gibi hello ipuçları verilen toopredict hello miktarını kendisini uygundur.</span><span class="sxs-lookup"><span data-stu-id="6aa04-272">For hello multiclass classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself tooa natural classification where we would like toopredict hello amount of hello tips given.</span></span> <span data-ttu-id="6aa04-273">Biz depo toodefine ipucu aralıkları hello sorguda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6aa04-273">We can use bins toodefine tip ranges in hello query.</span></span> <span data-ttu-id="6aa04-274">tooget Merhaba hello için sınıf dağıtımları çeşitli ipucu aralıkları, hello kullanırız *örnek\_hive\_İpucu\_aralığı\_frequencies.hql* dosya.</span><span class="sxs-lookup"><span data-stu-id="6aa04-274">tooget hello class distributions for hello various tip ranges, we use hello *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="6aa04-275">İçeriğini aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-275">Below are its contents.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

<span data-ttu-id="6aa04-276">Hadoop komut satırı konsolundan komutu aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6aa04-276">Run hello following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="6aa04-277">Araştırması: İki boylam enlem konumlar arasında doğrudan uzaklığı işlem</span><span class="sxs-lookup"><span data-stu-id="6aa04-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-278">Bu genellikle olur bir **veri Bilimcisi** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-279">Merhaba doğrudan uzaklık ölçüsü sağlar bize toofind hello tutarsızlık ve hello arasındaki çıkışı gerçek seyahat uzaklığı.</span><span class="sxs-lookup"><span data-stu-id="6aa04-279">Having a measure of hello direct distance allows us toofind out hello discrepancy between it and hello actual trip distance.</span></span> <span data-ttu-id="6aa04-280">Bu özellik bir yolcu küçük olabilir üzerine gelerek becerisiyle Biz bu hello sürücüsünü şekil, büyük olasılıkla tootip kasıtlı olarak gerçekleştirilecek bunları tarafından kadar uzun yol.</span><span class="sxs-lookup"><span data-stu-id="6aa04-280">We motivate this feature by pointing out that a passenger might be less likely tootip if they figure out that hello driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="6aa04-281">Gerçek seyahat uzaklığı ve hello arasında toosee hello karşılaştırma [Haversine uzaklığı](http://en.wikipedia.org/wiki/Haversine_formula) iki boylam enlem noktaları arasında (Merhaba "mükemmel daire" uzaklığı) hello trigonometrik işlevler Hive içinde bu nedenle kullanırız:</span><span class="sxs-lookup"><span data-stu-id="6aa04-281">toosee hello comparison between actual trip distance and hello [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (hello "great circle" distance), we use hello trigonometric functions available within Hive, thus :</span></span>

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

<span data-ttu-id="6aa04-282">Sorguda hello yukarıdaki R Merhaba Dünya mil cinsinden hello yarıçapı ve pi dönüştürülmüş tooradians.</span><span class="sxs-lookup"><span data-stu-id="6aa04-282">In hello query above, R is hello radius of hello Earth in miles, and pi is converted tooradians.</span></span> <span data-ttu-id="6aa04-283">Merhaba boylam enlem noktaları hello NYC alanı gölgeden uzak olan "filtrelenmiş" tooremove değerleri olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6aa04-283">Note that hello longitude-latitude points are "filtered" tooremove values that are far from hello NYC area.</span></span>

<span data-ttu-id="6aa04-284">Bu durumda, "queryoutputdir" adlı bizim sonuçları tooa dizin yazma.</span><span class="sxs-lookup"><span data-stu-id="6aa04-284">In this case, we write our results tooa directory called "queryoutputdir".</span></span> <span data-ttu-id="6aa04-285">Aşağıda gösterilen komutların Hello dizisi önce bu çıktı dizini oluşturur ve hello Hive komutu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-285">hello sequence of commands shown below first creates this output directory, and then runs hello Hive command.</span></span>

<span data-ttu-id="6aa04-286">Dizin istemi Hello Hive, çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6aa04-286">From hello Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="6aa04-287">Merhaba sorgu sonuçları too9 Azure BLOB'ların yazılır ***queryoutputdir/000000\_0*** çok ***queryoutputdir/000008\_0*** hello varsayılan kapsayıcı hello Hadoop kümesi altında.</span><span class="sxs-lookup"><span data-stu-id="6aa04-287">hello query results are written too9 Azure blobs ***queryoutputdir/000000\_0*** too ***queryoutputdir/000008\_0*** under hello default container of hello Hadoop cluster.</span></span>

<span data-ttu-id="6aa04-288">Merhaba tek tek bloblar toosee hello boyutu, komut hello Hive dizin isteminden aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6aa04-288">toosee hello size of hello individual blobs, we run hello following command from hello Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="6aa04-289">belirli bir dosya toosee Merhaba içeriğine söyleyin 000000\_0, Hadoop'ın kullanırız `copyToLocal` komutu, böylece.</span><span class="sxs-lookup"><span data-stu-id="6aa04-289">toosee hello contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="6aa04-290">`copyToLocal`büyük dosyalar için çok yavaş olabilir ve bunları ile kullanım için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="6aa04-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="6aa04-291">Biz hello kullanarak Azure Machine Learning içinde hello verileri araştırmak bir Azure blob bulunan verilere erişmenin önemli bir avantajı olan [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="6aa04-291">A key advantage of having this data reside in an Azure blob is that we may explore hello data within Azure Machine Learning using hello [Import Data][import-data] module.</span></span>

## <span data-ttu-id="6aa04-292"><a name="#downsample"></a>Örnek veriler ve yapı modellerinde Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6aa04-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="6aa04-293">Bu genellikle olur bir **veri Bilimcisi** görev.</span><span class="sxs-lookup"><span data-stu-id="6aa04-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="6aa04-294">Merhaba keşif verileri analiz aşaması sonra artık Azure Machine Learning modellerini oluşturmak için hazır toodown örnek hello veri duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="6aa04-294">After hello exploratory data analysis phase, we are now ready toodown sample hello data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="6aa04-295">Bu bölümde, nasıl toouse bir Hive sorgusu hello sonra erişilen toodown örnek hello verileri olan gösteriyoruz [veri içeri aktarma] [ import-data] Azure Machine Learning modülünde.</span><span class="sxs-lookup"><span data-stu-id="6aa04-295">In this section, we show how toouse a Hive query toodown sample hello data, which is then accessed from hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-hello-data"></a><span data-ttu-id="6aa04-296">Merhaba veri örnekleme aşağı</span><span class="sxs-lookup"><span data-stu-id="6aa04-296">Down sampling hello data</span></span>
<span data-ttu-id="6aa04-297">Bu yordamda iki adımı vardır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-297">There are two steps in this procedure.</span></span> <span data-ttu-id="6aa04-298">İlk biz hello katılma **nyctaxidb.trip** ve **nyctaxidb.fare** tüm kayıtları mevcut üç anahtarları tablolarda: "medallion", "korsan saldırılarına\_lisans", ve "alma\_datetime".</span><span class="sxs-lookup"><span data-stu-id="6aa04-298">First we join hello **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="6aa04-299">Biz sonra bir ikili sınıflandırma etiketi oluşturmak **Eğimli** ve birden çok sınıf sınıflandırma etiketini **İpucu\_sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="6aa04-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="6aa04-300">toobe mümkün toouse hello örneklenen verileri doğrudan hello aşağı [veri içeri aktarma] [ import-data] modül Azure Machine Learning ile gerekli toostore hello sorgu tooan iç Hive tablosu yukarıda hello sonuçlarını olduğu.</span><span class="sxs-lookup"><span data-stu-id="6aa04-300">toobe able toouse hello down sampled data directly from hello [Import Data][import-data] module in Azure Machine Learning, it is necessary toostore hello results of hello above query tooan internal Hive table.</span></span> <span data-ttu-id="6aa04-301">Aşağıda, biz iç bir Hive tablosu oluşturmak ve içeriğini örneklenen verileri aşağı birleştirilmiş hello ile doldurun.</span><span class="sxs-lookup"><span data-stu-id="6aa04-301">In what follows, we create an internal Hive table and populate its contents with hello joined and down sampled data.</span></span>

<span data-ttu-id="6aa04-302">Merhaba sorgusunu uygular standart Hive işlevleri doğrudan toogenerate hello saat, gün, hafta içi (Pazartesi 1 anlamına gelir ve Pazar 7 anlamına gelir) başlangıç hello yılın haftası "toplama\_datetime" alan ve hello alımı ve dropoff arasındaki hello doğrudan uzaklığı konumları.</span><span class="sxs-lookup"><span data-stu-id="6aa04-302">hello query applies standard Hive functions directly toogenerate hello hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from hello "pickup\_datetime" field,  and hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="6aa04-303">Kullanıcılar çok başvurabilir[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) böyle işlevlerin tam listesi için.</span><span class="sxs-lookup"><span data-stu-id="6aa04-303">Users can refer too[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="6aa04-304">Sorgu hello sonra hello sorgu sonuçları hello Azure Machine Learning Studio sığabilecek böylece örnekleri hello veri aşağı.</span><span class="sxs-lookup"><span data-stu-id="6aa04-304">hello query then down samples hello data so that hello query results can fit into hello Azure Machine Learning Studio.</span></span> <span data-ttu-id="6aa04-305">Yalnızca yaklaşık %1 hello özgün veri kümesinin Studio hello alınır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-305">Only about 1% of hello original dataset is imported into hello Studio.</span></span>

<span data-ttu-id="6aa04-306">Merhaba içeriğine aşağıda verilmiştir *örnek\_hive\_hazırlama\_için\_aml\_full.hql* veri modeli Azure Machine Learning ile derleme hazırlar dosya.</span><span class="sxs-lookup"><span data-stu-id="6aa04-306">Below are hello contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

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
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
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
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
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
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

<span data-ttu-id="6aa04-307">toorun hello Hive dizininden bu sorguyu iste:</span><span class="sxs-lookup"><span data-stu-id="6aa04-307">toorun this query, from hello Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="6aa04-308">Şimdi bir iç tablosu "Merhaba kullanılarak erişilebilen nyctaxidb.nyctaxi_downsampled_dataset" sahibiz [veri içeri aktarma] [ import-data] Azure Machine Learning modülünden.</span><span class="sxs-lookup"><span data-stu-id="6aa04-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using hello [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="6aa04-309">Bu veri kümesi Machine Learning modeli oluşturmak için Ayrıca, kullanabiliriz.</span><span class="sxs-lookup"><span data-stu-id="6aa04-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a><span data-ttu-id="6aa04-310">Azure Machine Learning tooaccess hello örneklenen verileri aşağı Hello veri içeri aktarma modülü kullanın</span><span class="sxs-lookup"><span data-stu-id="6aa04-310">Use hello Import Data module in Azure Machine Learning tooaccess hello down sampled data</span></span>
<span data-ttu-id="6aa04-311">Merhaba Hive sorguları verme için önkoşul olarak [veri içeri aktarma] [ import-data] modül Azure Machine Learning, ihtiyacımız tooan Azure Machine Learning çalışma alanına erişmek ve hello toohello kimlik bilgilerini erişim Küme ve onun ilişkili depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="6aa04-311">As prerequisites for issuing Hive queries in hello [Import Data][import-data] module of Azure Machine Learning, we need access tooan Azure Machine Learning workspace and access toohello credentials of hello cluster and its associated storage account.</span></span>

<span data-ttu-id="6aa04-312">Merhaba ilgili bazı Ayrıntılar [veri içeri aktarma] [ import-data] modülü ve hello parametreleri tooinput:</span><span class="sxs-lookup"><span data-stu-id="6aa04-312">Some details on hello [Import Data][import-data] module and hello parameters tooinput :</span></span>

<span data-ttu-id="6aa04-313">**HCatalog sunucusu URI**: hello küme adı olduğundan abc123 sonra yalnızca budur: https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="6aa04-313">**HCatalog server URI**: If hello cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="6aa04-314">**Hadoop kullanıcı hesabı adı** : hello küme için seçilen hello kullanıcı adı (**değil** hello uzaktan erişim kullanıcı adı)</span><span class="sxs-lookup"><span data-stu-id="6aa04-314">**Hadoop user account name** : hello user name chosen for hello cluster (**not** hello remote access user name)</span></span>

<span data-ttu-id="6aa04-315">**Hadoop kullanıcı hesabı parolasını** : hello küme için seçilen hello parola (**değil** hello uzaktan erişim parola)</span><span class="sxs-lookup"><span data-stu-id="6aa04-315">**Hadoop ser account password** : hello password chosen for hello cluster (**not** hello remote access password)</span></span>

<span data-ttu-id="6aa04-316">**Çıktı verilerini konumunu** : Bu toobe Azure seçilir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-316">**Location of output data** : This is chosen toobe Azure.</span></span>

<span data-ttu-id="6aa04-317">**Azure depolama hesabı adı** : hello kümesi ile ilişkili hello varsayılan depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="6aa04-317">**Azure storage account name** : Name of hello default storage account associated with hello cluster.</span></span>

<span data-ttu-id="6aa04-318">**Azure kapsayıcı adı** : Bu hello varsayılan kapsayıcı hello küme adıdır ve olduğundan genellikle hello aynı hello küme adı olarak.</span><span class="sxs-lookup"><span data-stu-id="6aa04-318">**Azure container name** : This is hello default container name for hello cluster, and is typically hello same as hello cluster name.</span></span> <span data-ttu-id="6aa04-319">"Abc123" adlı bir küme için yalnızca abc123 budur.</span><span class="sxs-lookup"><span data-stu-id="6aa04-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6aa04-320">**Hello kullanarak tooquery istediğimiz herhangi bir tablo [veri içeri aktarma] [ import-data] Azure Machine Learning modülünde bir iç tablosu olması gerekir.**</span><span class="sxs-lookup"><span data-stu-id="6aa04-320">**Any table we wish tooquery using hello [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="6aa04-321">Bir ipucu D.db veritabanındaki bir tablo T bir iç tablosu ise belirlemek için aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="6aa04-322">Hello dizin istemi, sorunu hello komutu yığını:</span><span class="sxs-lookup"><span data-stu-id="6aa04-322">From hello Hive directory prompt, issue hello command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="6aa04-323">Bir iç tablosu Hello tablodur ve onu doldurulur, içeriği burada gösterilecek gerekir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-323">If hello table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="6aa04-324">Bir tablo bir iç tablosu olup olmadığını toouse hello Azure Storage Gezgini olan başka bir şekilde toodetermine.</span><span class="sxs-lookup"><span data-stu-id="6aa04-324">Another way toodetermine whether a table is an internal table is toouse hello Azure Storage Explorer.</span></span> <span data-ttu-id="6aa04-325">Merhaba tablo adına göre filtre uygulamak ve toonavigate toohello varsayılan kapsayıcı hello küme adını kullanın.</span><span class="sxs-lookup"><span data-stu-id="6aa04-325">Use it toonavigate toohello default container name of hello cluster, and then filter by hello table name.</span></span> <span data-ttu-id="6aa04-326">Merhaba tablo ve içeriği gösterilirse, bu bir iç tablosu olduğunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="6aa04-326">If hello table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="6aa04-327">Merhaba Hive sorgusu ve hello bir anlık görüntüsünü işte [veri içeri aktarma] [ import-data] Modülü:</span><span class="sxs-lookup"><span data-stu-id="6aa04-327">Here is a snapshot of hello Hive query and hello [Import Data][import-data] module:</span></span>

![Veri içeri aktarma modülü için Hive sorgusu](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="6aa04-329">Örneklenen verileri hello varsayılan kapsayıcısında yer alıyor bizim aşağı itibaren hello Azure Machine Learning elde edilen Hive sorgusu çok basit bir işlemdir ve yalnızca olduğunu not bir "seçin * nyctaxidb.nyctaxi gelen\_altörnekleme\_veri".</span><span class="sxs-lookup"><span data-stu-id="6aa04-329">Note that since our down sampled data resides in hello default container, hello resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="6aa04-330">Merhaba veri kümesi, başlangıç noktası Machine Learning model oluşturmaya yönelik hello olarak artık kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-330">hello dataset may now be used as hello starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="6aa04-331"><a name="mlmodel"></a>Azure Machine Learning modellerini Derleme</span><span class="sxs-lookup"><span data-stu-id="6aa04-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="6aa04-332">Artık mümkün tooproceed toomodel yapı ve model dağıtımda duyuyoruz [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="6aa04-332">We are now able tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="6aa04-333">Merhaba veri hazır bize için yukarıda tanımlanan hello tahmin sorunları adresleme içinde toouse:</span><span class="sxs-lookup"><span data-stu-id="6aa04-333">hello data is ready for us toouse in addressing hello prediction problems identified above:</span></span>

<span data-ttu-id="6aa04-334">**1. İkili sınıflandırma**: olsun veya olmasın bir ipucu Ücretli bir seyahat için toopredict.</span><span class="sxs-lookup"><span data-stu-id="6aa04-334">**1. Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="6aa04-335">**Kullanılan öğrenen:** iki sınıflı Lojistik regresyon</span><span class="sxs-lookup"><span data-stu-id="6aa04-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="6aa04-336">a.</span><span class="sxs-lookup"><span data-stu-id="6aa04-336">a.</span></span> <span data-ttu-id="6aa04-337">Bu sorun için hedef (veya sınıfı) etiketimizi "Eğimli".</span><span class="sxs-lookup"><span data-stu-id="6aa04-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="6aa04-338">Özgün aşağı örneklenen kümemize bu sınıflandırma deneme için hedef sızıntıları olan birkaç sütun içeriyor.</span><span class="sxs-lookup"><span data-stu-id="6aa04-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="6aa04-339">Özellikle: İpucu\_sınıfı, İpucu\_miktarı ve toplam\_zaman sınama sırasında kullanılamaz hello hedef etiketi açığa bilgilerini tutar.</span><span class="sxs-lookup"><span data-stu-id="6aa04-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="6aa04-340">Biz bu sütunları hello kullanarak dikkate kaldırmak [Select Columns in Dataset sütun] [ select-columns] modülü.</span><span class="sxs-lookup"><span data-stu-id="6aa04-340">We remove these columns from consideration using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="6aa04-341">Merhaba anlık aşağıdaki ipucu verilen seyahat için ödeme bizim deneme toopredict gösterir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-341">hello snapshot below shows our experiment toopredict whether or not a tip was paid for a given trip.</span></span>

![Deneme anlık görüntü](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="6aa04-343">b.</span><span class="sxs-lookup"><span data-stu-id="6aa04-343">b.</span></span> <span data-ttu-id="6aa04-344">Bu deneme için bizim hedef etiket dağıtımların yaklaşık 1:1 yoktu.</span><span class="sxs-lookup"><span data-stu-id="6aa04-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="6aa04-345">Merhaba anlık görüntü aşağıdaki hello ikili sınıflandırma sorunu için ipucu sınıfı etiketleri hello dağılımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-345">hello snapshot below shows hello distribution of tip class labels for hello binary classification problem.</span></span>

![İpucu sınıfı etiketleri dağıtılması](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="6aa04-347">Sonuç olarak, size bir AUC 0.987, hello aşağıdaki çizimde gösterildiği gibi edinin.</span><span class="sxs-lookup"><span data-stu-id="6aa04-347">As a result, we obtain an AUC of 0.987 as shown in hello figure below.</span></span>

![AUC değeri](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="6aa04-349">**2. Çok sınıflı sınıflandırma**: toopredict hello aralık hello kullanarak önceden hello seyahat için ücretli ipucu tutarlarının tanımlanan sınıflar.</span><span class="sxs-lookup"><span data-stu-id="6aa04-349">**2. Multiclass classification**: toopredict hello range of tip amounts paid for hello trip, using hello previously defined classes.</span></span>

<span data-ttu-id="6aa04-350">**Kullanılan öğrenen:** çok sınıflı Lojistik regresyon</span><span class="sxs-lookup"><span data-stu-id="6aa04-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="6aa04-351">a.</span><span class="sxs-lookup"><span data-stu-id="6aa04-351">a.</span></span> <span data-ttu-id="6aa04-352">Bu sorun için hedef (veya sınıfı) etiketimizi olan "İpucu\_sınıfı" hangi alabilir beş değerlerden (0,1,2,3,4).</span><span class="sxs-lookup"><span data-stu-id="6aa04-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="6aa04-353">Merhaba ikili sınıflandırma durumda olduğu gibi bu deneme için hedef sızıntıları olan birkaç sütunlar sahip.</span><span class="sxs-lookup"><span data-stu-id="6aa04-353">As in hello binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="6aa04-354">Özellikle: eğimli, İpucu\_tutarı, toplam\_zaman sınama sırasında kullanılamaz hello hedef etiketi açığa bilgilerini tutar.</span><span class="sxs-lookup"><span data-stu-id="6aa04-354">In particular : tipped, tip\_amount, total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="6aa04-355">Biz hello kullanarak bu sütunları kaldırın [Select Columns in Dataset sütun] [ select-columns] modülü.</span><span class="sxs-lookup"><span data-stu-id="6aa04-355">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="6aa04-356">Merhaba anlık görüntü gösterilmektedir hangi Kutusu'na ipucu olan büyük olasılıkla toofall bizim deneme toopredict (sınıfı 0: ipucu = $0, 1 sınıfı: ipucu > 0 ve ipucu < = $5, sınıf 2: ipucu > $5 ve ipucu < = $10, sınıf 3: ipucu > $10 ve ipucu < = $20 Sınıf 4: > $20 ipucu)</span><span class="sxs-lookup"><span data-stu-id="6aa04-356">hello snapshot below shows our experiment toopredict in which bin a tip is likely toofall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![Deneme anlık görüntü](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="6aa04-358">Şimdi bizim gerçek test sınıfı dağıtım nasıl göründüğünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="6aa04-359">Sınıf 0 ve sınıf 1 yaygın olsa da, hello diğer sınıflar nadir olduğunu bakın.</span><span class="sxs-lookup"><span data-stu-id="6aa04-359">We see that while Class 0 and Class 1 are prevalent, hello other classes are rare.</span></span>

![Test sınıfı dağıtım](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="6aa04-361">b.</span><span class="sxs-lookup"><span data-stu-id="6aa04-361">b.</span></span> <span data-ttu-id="6aa04-362">Bu deneme için bizim tahmin accuracies karışıklığı matris toolook kullanırız.</span><span class="sxs-lookup"><span data-stu-id="6aa04-362">For this experiment, we use a confusion matrix toolook at our prediction accuracies.</span></span> <span data-ttu-id="6aa04-363">Bu örnek aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-363">This is shown below.</span></span>

![Karışıklığı Matrisi](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="6aa04-365">Bizim sınıfı accuracies hello yaygın sınıfları oldukça iyi durumdayken hello modeli Tebrikler "öğrenme" hello nadir sınıflarında yapmaz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6aa04-365">Note that while our class accuracies on hello prevalent classes is quite good, hello model does not do a good job of "learning" on hello rarer classes.</span></span>

<span data-ttu-id="6aa04-366">**3. Regresyon görev**: seyahat için ödenen ucunun toopredict hello tutar.</span><span class="sxs-lookup"><span data-stu-id="6aa04-366">**3. Regression task**: toopredict hello amount of tip paid for a trip.</span></span>

<span data-ttu-id="6aa04-367">**Kullanılan öğrenen:** Boosted karar ağacı</span><span class="sxs-lookup"><span data-stu-id="6aa04-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="6aa04-368">a.</span><span class="sxs-lookup"><span data-stu-id="6aa04-368">a.</span></span> <span data-ttu-id="6aa04-369">Bu sorun için hedef (veya sınıfı) etiketimizi olan "İpucu\_tutar".</span><span class="sxs-lookup"><span data-stu-id="6aa04-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="6aa04-370">Bizim hedef sızıntıları bu durumda: eğimli, İpucu\_sınıfı, toplam\_tutar; genellikle zaman sınama sırasında kullanılamıyor hello ipucu tutar hakkında bilgi ortaya bu değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="6aa04-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about hello tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="6aa04-371">Biz hello kullanarak bu sütunları kaldırın [Select Columns in Dataset sütun] [ select-columns] modülü.</span><span class="sxs-lookup"><span data-stu-id="6aa04-371">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="6aa04-372">Başlangıç anlık görüntü belows ipucu verilen hello bizim deneme toopredict hello miktarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6aa04-372">hello snapshot belows shows our experiment toopredict hello amount of hello given tip.</span></span>

![Deneme anlık görüntü](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="6aa04-374">b.</span><span class="sxs-lookup"><span data-stu-id="6aa04-374">b.</span></span> <span data-ttu-id="6aa04-375">Regresyon sorunları, biz hello tahminlerin karesi alınmış hello hata bakarak hello accuracies bizim öngörme ölçmek, katsayısı hello ve gibi hello.</span><span class="sxs-lookup"><span data-stu-id="6aa04-375">For regression problems, we measure hello accuracies of our prediction by looking at hello squared error in hello predictions, hello coefficient of determination, and hello like.</span></span> <span data-ttu-id="6aa04-376">Bunlar aşağıdaki gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="6aa04-376">We show these below.</span></span>

![Tahmin istatistikleri](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="6aa04-378">Merhaba hakkında 0.709, katsayısı olduğunu görmek yaklaşık hello farkı %71 olduğunu belirtmek bizim modeli katsayısını tarafından açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-378">We see that about hello coefficient of determination is 0.709, implying about 71% of hello variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6aa04-379">Azure Machine Learning hakkında daha fazla toolearn ve nasıl tooaccess ve kullanmak, lütfen çok bakın[Machine Learning nedir?](machine-learning-what-is-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="6aa04-379">toolearn more about Azure Machine Learning and how tooaccess and use it, please refer too[What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="6aa04-380">Machine Learning denemelerini Azure Machine learning'de bir grup ile çalmak için çok faydalı bir hello kaynaktır [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="6aa04-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="6aa04-381">Merhaba galeri denemeler genişliğine kapsayan ve Azure Machine Learning yetenekleri hello aralığı içine kapsamlı bir giriş sağlar.</span><span class="sxs-lookup"><span data-stu-id="6aa04-381">hello Gallery covers a gamut of experiments and provides a thorough introduction into hello range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="6aa04-382">Lisans bilgileri</span><span class="sxs-lookup"><span data-stu-id="6aa04-382">License Information</span></span>
<span data-ttu-id="6aa04-383">Bu örnek gözden geçirme ve eşlik eden betikleri hello MIT lisansı altında Microsoft tarafından paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="6aa04-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="6aa04-384">Lütfen hello LICENSE.txt dosyayı daha fazla ayrıntı için GitHub üzerindeki hello örnek kodu hello dizininde iade edin.</span><span class="sxs-lookup"><span data-stu-id="6aa04-384">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="6aa04-385">Başvurular</span><span class="sxs-lookup"><span data-stu-id="6aa04-385">References</span></span>
<span data-ttu-id="6aa04-386">• [Andrés Monroy NYC ücreti dönüşleri indirme sayfası](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="6aa04-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="6aa04-387">• [FOILing NYC ait ücreti seyahat veri Chris Whong tarafından](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="6aa04-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="6aa04-388">• [NYC ücreti ve Limousine devreye sokmak araştırma ve istatistikleri](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="6aa04-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
