---
title: "aaaBuild ve bir Azure VM üzerinde SQL Server kullanarak bir makine öğrenimi modeline dağıtma | Microsoft Docs"
description: "Gelişmiş analizler işlemi ve eylem teknoloji"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="480e5-103">eylemin Hello takım veri bilimi işlemi: SQL Server kullanma</span><span class="sxs-lookup"><span data-stu-id="480e5-103">hello Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="480e5-104">Bu öğreticide, oluşturma ve makine öğrenimi modeline dağıtma hello işleminde size kılavuzluk SQL Server ve genel kullanıma açık bir veri kümesi--hello kullanarak [NYC ücreti dönüşleri](http://www.andresmh.com/nyctaxitrips/) veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="480e5-104">In this tutorial, you walk through hello process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="480e5-105">Merhaba yordamdan sonraki standart veri bilimi akışı: alma ve hello verileri araştırmak, mühendislik özellikleri toofacilitate öğrenme, sonra yapı ve model dağıtma.</span><span class="sxs-lookup"><span data-stu-id="480e5-105">hello procedure follows a standard data science workflow: ingest and explore hello data, engineer features toofacilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="480e5-106"><a name="dataset"></a>NYC ücreti veri kümesi tanımı dönüşleri</span><span class="sxs-lookup"><span data-stu-id="480e5-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="480e5-107">Merhaba NYC ücreti seyahat veri yaklaşık 20 GB sıkıştırılmış CSV dosyaları (~ 48 GB sıkıştırılmamış), 173 milyondan fazla kapsayan tek tek dönüşleri ve hello fares her seyahat için ücretli.</span><span class="sxs-lookup"><span data-stu-id="480e5-107">hello NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="480e5-108">Her seyahat kayıt hello alma ve teslim konumu ve zaman, anonim korsan (sürücü) lisans numarası ve medallion (ücreti'nın benzersiz kimliği) numarasını içerir.</span><span class="sxs-lookup"><span data-stu-id="480e5-108">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="480e5-109">Merhaba veri hello yıl 2013 tüm dönüşleri kapsayan ve her ay için iki veri kümesi aşağıdaki hello sağlanır:</span><span class="sxs-lookup"><span data-stu-id="480e5-109">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="480e5-110">Merhaba 'trip_data' CSV yolcu, toplama ve dropoff noktaları, seyahat süresi ve seyahat Uzunluk sayısı gibi seyahat ayrıntıları içerir.</span><span class="sxs-lookup"><span data-stu-id="480e5-110">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="480e5-111">Birkaç örnek kayıt şunlardır:</span><span class="sxs-lookup"><span data-stu-id="480e5-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="480e5-112">Merhaba 'trip_fare' CSV ödeme türü, ücreti tutarı, ek ücret ve vergileri, ipuçları ve tolls ve Ücretli hello toplam miktarı gibi her seyahat için ücretli hello ücreti ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="480e5-112">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="480e5-113">Birkaç örnek kayıt şunlardır:</span><span class="sxs-lookup"><span data-stu-id="480e5-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="480e5-114">Merhaba benzersiz anahtar toojoin seyahat\_veri ve seyahat\_ücreti hello alanlarının oluşur: medallion, korsan\_lisans ve alma\_datetime.</span><span class="sxs-lookup"><span data-stu-id="480e5-114">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="480e5-115"><a name="mltasks"></a>Tahmin görev örnekleri</span><span class="sxs-lookup"><span data-stu-id="480e5-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="480e5-116">Merhaba üzerinde temel üç tahmin sorunları formüle *İpucu\_tutar*, yani:</span><span class="sxs-lookup"><span data-stu-id="480e5-116">We will formulate three prediction problems based on hello *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="480e5-117">İkili sınıflandırma: bir ipucu bir seyahat, yani ödenmiş olup olmadığına bakılmaksızın tahmin bir *İpucu\_tutar* büyük $0 pozitif bir örnektir küçük, ancak bir *İpucu\_tutar* 0 / negatif bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="480e5-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="480e5-118">Çok sınıflı sınıflandırma: ipucu toopredict hello aralığı Ücretli hello seyahat için.</span><span class="sxs-lookup"><span data-stu-id="480e5-118">Multiclass classification: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="480e5-119">Biz hello bölmek *İpucu\_tutar* beş depo veya sınıfları:</span><span class="sxs-lookup"><span data-stu-id="480e5-119">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="480e5-120">Regresyon görevi: seyahat için ödenen ucunun toopredict hello tutar.</span><span class="sxs-lookup"><span data-stu-id="480e5-120">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="480e5-121"><a name="setup"></a>Kurulum hello Azure veri bilimi ortamı Gelişmiş analiz için</span><span class="sxs-lookup"><span data-stu-id="480e5-121"><a name="setup"></a>Setting Up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="480e5-122">Hello gördüğünüz [ortamınıza planlama](machine-learning-data-science-plan-your-environment.md) Kılavuzu, azure'da hello NYC ücreti dönüşleri veri kümesi ile çeşitli seçenekler toowork vardır:</span><span class="sxs-lookup"><span data-stu-id="480e5-122">As you can see from hello [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options toowork with hello NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="480e5-123">Azure BLOB'ları hello verilerde sonra Azure Machine Learning modeli ile çalışma</span><span class="sxs-lookup"><span data-stu-id="480e5-123">Work with hello data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="480e5-124">SQL Server veritabanı sonra Azure Machine Learning modelinde içine Hello veri yükleme</span><span class="sxs-lookup"><span data-stu-id="480e5-124">Load hello data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="480e5-125">Bu öğreticide biz hello veri tooa SQL sunucusu, veri keşfi, özellik paralel toplu olarak alma işlemi gösterilmektedir mühendislik ve aşağı örnekleme SQL Server Management Studio'yu kullanarak yanı sıra IPython Not Defteri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="480e5-125">In this tutorial we will demonstrate parallel bulk import of hello data tooa SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="480e5-126">[Örnek komutlar](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) ve [IPython not defterlerini](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) Github'da paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="480e5-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="480e5-127">Bir örnek IPython not defteri toowork hello verileri Azure BLOB'ları da hello kullanılabilir aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="480e5-127">A sample IPython notebook toowork with hello data in Azure blobs is also available in hello same location.</span></span>

<span data-ttu-id="480e5-128">Azure veri bilimi ortamınızı tooset:</span><span class="sxs-lookup"><span data-stu-id="480e5-128">tooset up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="480e5-129">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="480e5-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="480e5-130">Bir Azure Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="480e5-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="480e5-131">[Bir veri bilimi sanal makine sağlama](machine-learning-data-science-setup-sql-server-virtual-machine.md), bir SQL sunucusu ve bir IPython dizüstü sunucusu sağlar.</span><span class="sxs-lookup"><span data-stu-id="480e5-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="480e5-132">Merhaba örnek komut dosyaları ve IPython not defterlerini indirilen tooyour veri bilimi sanal makine hello Kurulum işlemi sırasında olacaktır.</span><span class="sxs-lookup"><span data-stu-id="480e5-132">hello sample scripts and IPython notebooks will be downloaded tooyour Data Science virtual machine during hello setup process.</span></span> <span data-ttu-id="480e5-133">Merhaba VM yükleme sonrası betik tamamlandığında hello örnekleri VM Belge Kitaplığı'nda olur:</span><span class="sxs-lookup"><span data-stu-id="480e5-133">When hello VM post-installation script completes, hello samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="480e5-134">Örnek komut dosyaları:`C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="480e5-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="480e5-135">Örnek IPython dizüstü bilgisayarlar:`C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="480e5-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="480e5-136">Burada `<user_name>` VM Windows oturum açma adıdır.</span><span class="sxs-lookup"><span data-stu-id="480e5-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="480e5-137">Toohello örnek klasörler olarak başvuruda bulunacak **örnek betikler** ve **örnek IPython not defterlerini**.</span><span class="sxs-lookup"><span data-stu-id="480e5-137">We will refer toohello sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="480e5-138">Merhaba veri kümesi boyutu, veri kaynağı konumu ve hello seçili Azure hedef ortam bağlı olarak, bu senaryo çok benzer[senaryo \#5: yerel dosyaları büyük bir veri kümesini hedef Azure VM'deki SQL Server](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span><span class="sxs-lookup"><span data-stu-id="480e5-138">Based on hello dataset size, data source location, and hello selected Azure target environment, this scenario is similar too[Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="480e5-139"><a name="getdata"></a>Ortak kaynağından Hello Veri Al</span><span class="sxs-lookup"><span data-stu-id="480e5-139"><a name="getdata"></a>Get hello Data from Public Source</span></span>
<span data-ttu-id="480e5-140">tooget hello [NYC ücreti dönüşleri](http://www.andresmh.com/nyctaxitrips/) dataset ortak konumundan kullandığınız açıklanan hello yöntemlerden herhangi birini [Azure Blob depolama biriminden verileri Taşı tooand](machine-learning-data-science-move-azure-blob.md) toocopy hello veri tooyour yeni sanal makine.</span><span class="sxs-lookup"><span data-stu-id="480e5-140">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour new virtual machine.</span></span>

<span data-ttu-id="480e5-141">AzCopy kullanarak toocopy hello verileri:</span><span class="sxs-lookup"><span data-stu-id="480e5-141">toocopy hello data using AzCopy:</span></span>

1. <span data-ttu-id="480e5-142">Tooyour sanal makine (VM) oturum</span><span class="sxs-lookup"><span data-stu-id="480e5-142">Log in tooyour virtual machine (VM)</span></span>
2. <span data-ttu-id="480e5-143">Merhaba sanal makinenin veri diski yeni bir dizin oluşturun (Not: hello hello bir veri diski olarak VM ile birlikte geçici Disk kullanmayın).</span><span class="sxs-lookup"><span data-stu-id="480e5-143">Create a new directory in hello VM's data disk (Note: Do not use hello Temporary Disk which comes with hello VM as a Data Disk).</span></span>
3. <span data-ttu-id="480e5-144">Bir komut istemi penceresinde aşağıdaki Azcopy komut satırı, (2)'de oluşturduğunuz veri klasörünüz < path_to_data_folder > yerine hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="480e5-144">In a Command Prompt window, run hello following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="480e5-145">Merhaba AzCopy tamamlandığında 24 toplam CSV dosyaları sıkıştırılmış (seyahat için 12\_veri ve seyahat için 12\_ücreti) hello veri klasörde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="480e5-145">When hello AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in hello data folder.</span></span>
4. <span data-ttu-id="480e5-146">Merhaba indirilen dosyaları ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="480e5-146">Unzip hello downloaded files.</span></span> <span data-ttu-id="480e5-147">Sıkıştırılmamış hello dosyalarının bulunduğu hello klasörü not alın.</span><span class="sxs-lookup"><span data-stu-id="480e5-147">Note hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="480e5-148">Bu klasör başvurulan tooas hello olacaktır < yol\_için\_veri\_dosyaları\>.</span><span class="sxs-lookup"><span data-stu-id="480e5-148">This folder will be referred tooas hello <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="480e5-149"><a name="dbload"></a>SQL Server veritabanına veri toplu İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="480e5-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="480e5-150">Merhaba, yükleme ve aktarma büyük miktarlarda veri tooan SQL veritabanı ve sonraki sorguları Performans kullanılarak geliştirilebilir *bölümlenmiş tabloları ve görünümleri*.</span><span class="sxs-lookup"><span data-stu-id="480e5-150">hello performance of loading/transferring large amounts of data tooan SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="480e5-151">Bu bölümde, biz açıklandığı hello yönergeleri [paralel toplu veri içeri aktarma kullanarak SQL bölüm tabloları](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate paralel bölümlenmiş tablolar halinde yeni bir veritabanı ve yük hello verileri.</span><span class="sxs-lookup"><span data-stu-id="480e5-151">In this section, we will follow hello instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate a new database and load hello data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="480e5-152">Tooyour VM açmışken Başlat **SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="480e5-152">While logged in tooyour VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="480e5-153">Windows kimlik doğrulaması kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="480e5-153">Connect using Windows Authentication.</span></span>
   
    ![SSMS bağlanma][12]
3. <span data-ttu-id="480e5-155">Eğer henüz hello SQL Server kimlik doğrulama modu değiştirildi ve yeni bir SQL oturum açma kullanıcı oluşturulan adlı hello betik dosyasını açma **değiştirme\_auth.sql** hello içinde **örnek betikler** klasör.</span><span class="sxs-lookup"><span data-stu-id="480e5-155">If you have not yet changed hello SQL Server authentication mode and created a new SQL login user, open hello script file named **change\_auth.sql** in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="480e5-156">Merhaba varsayılan kullanıcı adı ve parolasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="480e5-156">Change hello  default user name and password.</span></span> <span data-ttu-id="480e5-157">Tıklatın **! Yürütme** hello araç toorun hello komut.</span><span class="sxs-lookup"><span data-stu-id="480e5-157">Click **!Execute** in hello toolbar toorun hello script.</span></span>
   
    ![Komut dosyası yürütme][13]
4. <span data-ttu-id="480e5-159">Doğrulayın ve/veya SQL Server veritabanlarını yeni oluşturulan varsayılan veritabanı ve günlük klasörleri tooensure bir veri diski depolanacak hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="480e5-159">Verify and/or change hello SQL Server default database and log folders tooensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="480e5-160">datawarehousing yükler için en iyi duruma getirilmiş hello SQL Server VM görüntüsü veri ve günlük disklerle önceden yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="480e5-160">hello SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="480e5-161">VM'yi bir veri diski içermeyen ve yeni sanal sabit diskler hello VM Kurulum işlemi sırasında eklediyseniz hello varsayılan klasörler aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="480e5-161">If your VM did not include a Data Disk and you added new virtual hard disks during hello VM setup process, change hello default folders as follows:</span></span>
   
   * <span data-ttu-id="480e5-162">Sol paneli ve tıklatın hello sağ hello SQL Server adı **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="480e5-162">Right-click hello SQL Server name in hello left panel and click **Properties**.</span></span>
     
       ![SQL Server özellikleri][14]
   * <span data-ttu-id="480e5-164">Seçin **veritabanı ayarlarını** hello gelen **sayfa Seç** toohello sol listeleyin.</span><span class="sxs-lookup"><span data-stu-id="480e5-164">Select **Database Settings** from hello **Select a page** list toohello left.</span></span>
   * <span data-ttu-id="480e5-165">Doğrulayın ve/veya hello değiştirme **veritabanı varsayılan konumları** toohello **veri diski** tercih ettiğiniz konumları.</span><span class="sxs-lookup"><span data-stu-id="480e5-165">Verify and/or change hello **Database default locations** toohello **Data Disk** locations of your choice.</span></span> <span data-ttu-id="480e5-166">Yeni veritabanları hello varsayılan konumu ayarlarını oluşturduysanız bulunduğu budur.</span><span class="sxs-lookup"><span data-stu-id="480e5-166">This is where new databases reside if created with hello default location settings.</span></span>
     
       ![SQL veritabanı Varsayılanları][15]  
5. <span data-ttu-id="480e5-168">toocreate yeni bir veritabanı ve dosya grupları toohold kümesi hello bölümlenmiş tablolar, açık hello örnek betik **oluşturma\_db\_default.sql**.</span><span class="sxs-lookup"><span data-stu-id="480e5-168">toocreate a new database and a set of filegroups toohold hello partitioned tables, open hello sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="480e5-169">Merhaba betik adlı yeni bir veritabanı oluşturacak **TaxiNYC** ve hello varsayılan veri konumu 12 grupları.</span><span class="sxs-lookup"><span data-stu-id="480e5-169">hello script will create a new database named **TaxiNYC** and 12 filegroups in hello default data location.</span></span> <span data-ttu-id="480e5-170">Her dosya seyahat bir aylık tutacak\_veri ve seyahat\_masrafları veri.</span><span class="sxs-lookup"><span data-stu-id="480e5-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="480e5-171">İsterseniz Hello veritabanı adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="480e5-171">Modify hello database name, if desired.</span></span> <span data-ttu-id="480e5-172">Tıklatın **! Yürütme** toorun hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="480e5-172">Click **!Execute** toorun hello script.</span></span>
6. <span data-ttu-id="480e5-173">Ardından, iki bölüm tabloları hello seyahat için bir tane oluşturun\_veri ve hello seyahat için başka bir\_ücreti.</span><span class="sxs-lookup"><span data-stu-id="480e5-173">Next, create two partition tables, one for hello trip\_data and another for hello trip\_fare.</span></span> <span data-ttu-id="480e5-174">Açık hello örnek betik **oluşturma\_bölümlenmiş\_table.sql**, hangi olur:</span><span class="sxs-lookup"><span data-stu-id="480e5-174">Open hello sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="480e5-175">Bir bölüm işlevi toosplit hello veri aya göre oluşturun.</span><span class="sxs-lookup"><span data-stu-id="480e5-175">Create a partition function toosplit hello data by month.</span></span>
   * <span data-ttu-id="480e5-176">Bir bölüm düzeni toomap her ayın veri tooa farklı dosya grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="480e5-176">Create a partition scheme toomap each month's data tooa different filegroup.</span></span>
   * <span data-ttu-id="480e5-177">İki bölümlenmiş tabloları eşlenen toohello bölüm düzeni oluşturma: **nyctaxi\_seyahat** hello seyahat tutacak\_veri ve **nyctaxi\_ücreti** hello seyahat tutar \_masrafları veri.</span><span class="sxs-lookup"><span data-stu-id="480e5-177">Create two partitioned tables mapped toohello partition scheme: **nyctaxi\_trip** will hold hello trip\_data and **nyctaxi\_fare** will hold hello trip\_fare data.</span></span>
     
     <span data-ttu-id="480e5-178">Tıklatın **! Yürütme** toorun hello komut dosyası ve hello bölümlenmiş tablolar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="480e5-178">Click **!Execute** toorun hello script and create hello partitioned tables.</span></span>
7. <span data-ttu-id="480e5-179">Merhaba, **örnek betikler** klasörü, iki örnek PowerShell betik veri tooSQL Server tabloları paralel Toplu Almalar toodemonstrate sağlanan vardır.</span><span class="sxs-lookup"><span data-stu-id="480e5-179">In hello **Sample Scripts** folder, there are two sample PowerShell scripts provided toodemonstrate parallel bulk imports of data tooSQL Server tables.</span></span>
   
   * <span data-ttu-id="480e5-180">**BCP\_paralel\_generic.ps1** bir genel komut dosyası tooparallel toplu içeri aktarma bir tabloya verilerdir.</span><span class="sxs-lookup"><span data-stu-id="480e5-180">**bcp\_parallel\_generic.ps1** is a generic script tooparallel bulk import data into a table.</span></span> <span data-ttu-id="480e5-181">Bu komut dosyası tooset hello giriş ve hedef değişkenleri hello yorum hello komut satırlarında belirtildiği şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="480e5-181">Modify this script tooset hello input and target variables as indicated in hello comment lines in hello script.</span></span>
   * <span data-ttu-id="480e5-182">**BCP\_paralel\_nyctaxi.ps1** hello genel komut dosyası, önceden yapılandırılmış bir sürümüdür ve her iki tabloyu hello NYC ücreti dönüş verileri için kullanılan tootooload olabilir.</span><span class="sxs-lookup"><span data-stu-id="480e5-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of hello generic script and can be used tootooload both tables for hello NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="480e5-183">Sağ hello **bcp\_paralel\_nyctaxi.ps1** betik adı ve tıklatın **Düzenle** tooopen PowerShell içinde.</span><span class="sxs-lookup"><span data-stu-id="480e5-183">Right-click hello **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** tooopen it in PowerShell.</span></span> <span data-ttu-id="480e5-184">Gözden geçirme hello önceden değişkenleri ve according tooyour seçili veritabanı adı, giriş veri klasörü, hedef günlük klasörü ve yolları toohello örnek biçim dosyalarını değiştirme **nyctaxi_trip.xml** ve **nyctaxi\_ Fare.xml** (hello sağlanan **örnek betikler** klasörü).</span><span class="sxs-lookup"><span data-stu-id="480e5-184">Review hello preset variables and modify according tooyour selected database name, input data folder, target log folder, and paths toohello  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in hello **Sample Scripts** folder).</span></span>
   
    ![Toplu Veri Al][16]
   
    <span data-ttu-id="480e5-186">Merhaba kimlik doğrulama modu seçin, varsayılan Windows kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="480e5-186">You may also select hello authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="480e5-187">Merhaba araç toorun Hello yeşil oku tıklatın.</span><span class="sxs-lookup"><span data-stu-id="480e5-187">Click hello green arrow in hello toolbar toorun.</span></span> <span data-ttu-id="480e5-188">Merhaba betik 24 toplu içeri aktarma işlemleri paralel 12 bölümlenmiş her tablo için başlatır.</span><span class="sxs-lookup"><span data-stu-id="480e5-188">hello script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="480e5-189">Yukarıdaki küme olarak hello SQL Server varsayılan veri klasörü açarak hello veri içeri aktarma ilerlemesi izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="480e5-189">You may monitor hello data import progress by opening hello SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="480e5-190">Merhaba PowerShell komut dosyası raporları başlangıç ve bitiş saatleri hello.</span><span class="sxs-lookup"><span data-stu-id="480e5-190">hello PowerShell script reports hello starting and ending times.</span></span> <span data-ttu-id="480e5-191">Tüm içeri aktarmalar tam toplu, bitiş saati başlangıç bildirilir.</span><span class="sxs-lookup"><span data-stu-id="480e5-191">When all bulk imports complete, hello ending time is reported.</span></span> <span data-ttu-id="480e5-192">Yani, hello Toplu Almalar başarılıysa hello hedef günlük klasörü tooverify hello hedef günlük klasöründe herhangi bir hata bildirdi denetleyin.</span><span class="sxs-lookup"><span data-stu-id="480e5-192">Check hello target log folder tooverify that hello bulk imports were successful, i.e., no errors reported in hello target log folder.</span></span>
10. <span data-ttu-id="480e5-193">Veritabanınızı artık araştırması, özellik Mühendisliği ve istediğiniz gibi diğer işlemler için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="480e5-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="480e5-194">Merhaba tabloları toohello göre bölümlenir beri **toplama\_datetime** alan, içeren sorguları **toplama\_datetime** hello koşullarında  **Burada** yan tümcesi hello bölüm düzeni yararlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="480e5-194">Since hello tables are partitioned according toohello **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in hello **WHERE** clause will benefit from hello partition scheme.</span></span>
11. <span data-ttu-id="480e5-195">İçinde **SQL Server Management Studio**, sağlanan hello örnek betik keşfedin **örnek\_queries.sql**.</span><span class="sxs-lookup"><span data-stu-id="480e5-195">In **SQL Server Management Studio**, explore hello provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="480e5-196">Merhaba örnek sorgular, Vurgu hello hiçbirini sorgu satırları ardından tıklatın toorun **! Yürütme** hello araç.</span><span class="sxs-lookup"><span data-stu-id="480e5-196">toorun any of hello sample queries, highlight hello query lines then click **!Execute** in hello toolbar.</span></span>
12. <span data-ttu-id="480e5-197">Merhaba NYC ücreti dönüş verileri iki ayrı tablolarda yüklenir.</span><span class="sxs-lookup"><span data-stu-id="480e5-197">hello NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="480e5-198">tooimprove birleştirme işlemleri tooindex hello tabloları kullanmamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="480e5-198">tooimprove join operations, it is highly recommended tooindex hello tables.</span></span> <span data-ttu-id="480e5-199">Merhaba örnek komut dosyası **oluşturma\_bölümlenmiş\_index.sql** bölümlenmiş dizinlerini hello bileşik birleştirme anahtarı oluşturur **medallion, korsan\_lisans ve alma\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="480e5-199">hello sample script **create\_partitioned\_index.sql** creates partitioned indexes on hello composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="480e5-200"><a name="dbexplore"></a>Veri keşfi ve SQL Server'daki özelliği mühendislik</span><span class="sxs-lookup"><span data-stu-id="480e5-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="480e5-201">Bu bölümde, veri keşfi ve özellik nesil doğrudan hello SQL sorguları çalıştırarak gerçekleştiririz **SQL Server Management Studio** hello SQL Server veritabanı kullanılarak oluşturulan önceki.</span><span class="sxs-lookup"><span data-stu-id="480e5-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in hello **SQL Server Management Studio** using hello SQL Server database created earlier.</span></span> <span data-ttu-id="480e5-202">Adlandırılmış bir örnek komut dosyası **örnek\_queries.sql** hello sağlanan **örnek betikler** klasör.</span><span class="sxs-lookup"><span data-stu-id="480e5-202">A sample script named **sample\_queries.sql** is provided in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="480e5-203">Merhaba varsayılandan farklı ise hello betik toochange hello veritabanı adı değiştirin: **TaxiNYC**.</span><span class="sxs-lookup"><span data-stu-id="480e5-203">Modify hello script toochange hello database name, if it is different from hello default: **TaxiNYC**.</span></span>

<span data-ttu-id="480e5-204">Bu alıştırmada, şunları yapacağız:</span><span class="sxs-lookup"><span data-stu-id="480e5-204">In this exercise, we will:</span></span>

* <span data-ttu-id="480e5-205">Çok bağlanmak**SQL Server Management Studio** ya da Windows kimlik doğrulaması veya SQL kimlik doğrulaması ve hello SQL oturum açma adı ve parola kullanarak.</span><span class="sxs-lookup"><span data-stu-id="480e5-205">Connect too**SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and hello SQL login name and password.</span></span>
* <span data-ttu-id="480e5-206">Veri dağıtımları değişen zaman pencereleri birkaç alanların keşfedin.</span><span class="sxs-lookup"><span data-stu-id="480e5-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="480e5-207">Veri Kalitesi hello boylam ve enlem alanlarının araştırın.</span><span class="sxs-lookup"><span data-stu-id="480e5-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="480e5-208">Merhaba üzerinde dayalı çok sınıflı ve ikili sınıflandırma etiketleri oluşturmak **İpucu\_tutar**.</span><span class="sxs-lookup"><span data-stu-id="480e5-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="480e5-209">Özellikler oluşturmak ve işlem/seyahat uzaklıklar karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="480e5-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="480e5-210">Merhaba iki tabloları birleştirme ve kullanılan toobuild modelleri olacaktır rasgele bir örnek ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="480e5-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

<span data-ttu-id="480e5-211">Hazır tooproceed tooAzure Machine Learning olduğunda ya da görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="480e5-211">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="480e5-212">Merhaba nihai SQL sorgu tooextract ve örnek hello veri ve kopyala-yapıştır hello sorguyu doğrudan kaydetmek bir [veri içeri aktarma] [ import-data] Azure Machine Learning modülünde veya</span><span class="sxs-lookup"><span data-stu-id="480e5-212">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="480e5-213">Örneklenen hello kalıcı tasarlanan veri modeli içindeki yeni bir veritabanı oluşturmak için toouse planladığınız tablo hello yeni tablo hello kullanılacağını ve [veri içeri aktarma] [ import-data] Azure Machine Learning modülünde.</span><span class="sxs-lookup"><span data-stu-id="480e5-213">Persist hello sampled and engineered data you plan toouse for model building in a new database table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="480e5-214">Bu bölümde biz hello son sorgu tooextract ve örnek hello verilerini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="480e5-214">In this section we will save hello final query tooextract and sample hello data.</span></span> <span data-ttu-id="480e5-215">Merhaba ikinci yöntem hello gösterilen [veri keşfi ve özellik Mühendisliği IPython Not](#ipnb) bölümü.</span><span class="sxs-lookup"><span data-stu-id="480e5-215">hello second method is demonstrated in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="480e5-216">Merhaba sayısı hello sayfasındaki satır ve sütunları hızlı doğrulanması için daha önce paralel toplu içeri kullanarak tabloları doldurulmuş,</span><span class="sxs-lookup"><span data-stu-id="480e5-216">For a quick verification of hello number of rows and columns in hello tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="480e5-217">Araştırması: Medallion seyahat dağıtım</span><span class="sxs-lookup"><span data-stu-id="480e5-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="480e5-218">Bu örnek, belirli bir süre içinde ile 100'den fazla dönüşleri hello medallion (ücreti sayılar) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="480e5-218">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="480e5-219">Hello sorgu tarafından hello bölümleme düzeni söylediğinizde bu yana bölümlenmiş hello tablo erişimden yararlanan **toplama\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="480e5-219">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="480e5-220">Merhaba tam veri kümesini sorgulama hello bölümlenmiş tablosu kullanın ve/veya dizin tarama ayrıca olun.</span><span class="sxs-lookup"><span data-stu-id="480e5-220">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="480e5-221">Keşfetme: dağıtım medallion ve hack_license tarafından seyahat</span><span class="sxs-lookup"><span data-stu-id="480e5-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="480e5-222">Veri Kalitesi değerlendirmesi: yanlış boylam ve/veya enlem ile kayıtlarını doğrulama</span><span class="sxs-lookup"><span data-stu-id="480e5-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="480e5-223">Merhaba boylam ve/veya enlem alanların hiçbirini ya da geçersiz bir değer içeriyorsa, bu örnek araştırır (radian derece -90 ile 90 arasında olmalıdır), ya da sahip (0, 0) koordinatları.</span><span class="sxs-lookup"><span data-stu-id="480e5-223">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="480e5-224">Keşfetme: Eğimli vs. Değil Eğimli dönüşleri dağıtım</span><span class="sxs-lookup"><span data-stu-id="480e5-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="480e5-225">Bu örnek karşılaştırması belirli bir zaman aralığı (veya hello tam yıl kapsayan varsa hello tam veri kümesi) Eğimli değil Eğimli dönüş hello sayısı bulur.</span><span class="sxs-lookup"><span data-stu-id="480e5-225">This example finds hello number of trips that were tipped vs. not tipped in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="480e5-226">Bu dağıtım için ikili sınıflandırma modelleme daha sonra kullanılan hello ikili etiket dağıtım toobe yansıtır.</span><span class="sxs-lookup"><span data-stu-id="480e5-226">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="480e5-227">Araştırması: Sınıf/Range dağıtım İpucu</span><span class="sxs-lookup"><span data-stu-id="480e5-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="480e5-228">Bu örnek hello dağıtımlarında ipucu aralıklarının belirli bir zaman aralığı (veya hello tam yıl kapsayan varsa hello tam veri kümesi) hesaplar.</span><span class="sxs-lookup"><span data-stu-id="480e5-228">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="480e5-229">Daha sonra çok sınıflı sınıflandırma model için kullanılacak hello etiket sınıfların hello dağıtım budur.</span><span class="sxs-lookup"><span data-stu-id="480e5-229">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="480e5-230">Keşfi: İşlem ve seyahat uzaklığı Karşılaştır</span><span class="sxs-lookup"><span data-stu-id="480e5-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="480e5-231">Bu örnek hello alma ve teslim boylam dönüştürür ve enlem tooSQL Coğrafya noktaları, SQL Coğrafya noktaları fark kullanarak hello seyahat uzaklığı hesaplar ve hello sonuçları karşılaştırma için rastgele bir örneğini döndürür.</span><span class="sxs-lookup"><span data-stu-id="480e5-231">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="480e5-232">Merhaba örneği yalnızca daha önce ele hello veri kalitesi değerlendirme sorgu kullanarak toovalid koordinatları hello sonuçlarını sınırlandırır.</span><span class="sxs-lookup"><span data-stu-id="480e5-232">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="480e5-233">Özellik Mühendisliği SQL sorguları</span><span class="sxs-lookup"><span data-stu-id="480e5-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="480e5-234">Merhaba etiket oluşturma ve Coğrafya dönüştürme araştırması sorguları bölümü sayım hello kaldırarak kullanılan toogenerate etiketleri/özellikleri de olabilir.</span><span class="sxs-lookup"><span data-stu-id="480e5-234">hello label generation and geography conversion exploration queries can also be used toogenerate labels/features by removing hello counting part.</span></span> <span data-ttu-id="480e5-235">Ek özellik Mühendisliği SQL örnekleri hello sağlanan [veri keşfi ve özellik Mühendisliği IPython Not](#ipnb) bölümü.</span><span class="sxs-lookup"><span data-stu-id="480e5-235">Additional feature engineering SQL examples are provided in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="480e5-236">Daha verimli toorun hello özelliği nesil sorguları hello tam veri kümesinin veya büyük bir alt kümesini doğrudan hello SQL Server veritabanı örneği üzerinde çalışan SQL sorgularını kullanarak olur.</span><span class="sxs-lookup"><span data-stu-id="480e5-236">It is more efficient toorun hello feature generation queries on hello full dataset or a large subset of it using SQL queries which run directly on hello SQL Server database instance.</span></span> <span data-ttu-id="480e5-237">Merhaba sorguları yürütülebilir içinde **SQL Server Management Studio**, IPython Not Defteri veya herhangi bir geliştirme aracı/erişebileceğiniz ortamında yerel olarak veya uzaktan veritabanı hello.</span><span class="sxs-lookup"><span data-stu-id="480e5-237">hello queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access hello database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="480e5-238">Model oluşturmanın için verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="480e5-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="480e5-239">Merhaba aşağıdaki birleşimler hello sorgu **nyctaxi\_seyahat** ve **nyctaxi\_ücreti** tabloları, ikili sınıflandırma etiketini oluşturur **Eğimli**, birden çok sınıf sınıflandırma etiketini **İpucu\_sınıfı**ve hello tam birleştirilmiş kümesinden %1 rasgele örnek ayıklar.</span><span class="sxs-lookup"><span data-stu-id="480e5-239">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from hello full joined dataset.</span></span> <span data-ttu-id="480e5-240">Bu sorgu kopyalanır, ardından doğrudan hello yapıştırılan [Azure Machine Learning Studio](https://studio.azureml.net) [veri içeri aktarma] [ import-data] hello SQL Server veritabanından doğrudan veri alımı için Modülü Azure örneği.</span><span class="sxs-lookup"><span data-stu-id="480e5-240">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL Server database instance in Azure.</span></span> <span data-ttu-id="480e5-241">Merhaba sorgu dışlar yanlış kayıtlarıyla (0, 0) koordinatları.</span><span class="sxs-lookup"><span data-stu-id="480e5-241">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <span data-ttu-id="480e5-242"><a name="ipnb"></a>Veri keşfi ve özellik Mühendisliği IPython Not</span><span class="sxs-lookup"><span data-stu-id="480e5-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="480e5-243">Bu bölümde, biz veri keşfi ve özellik oluşturma hello SQL Server veritabanını daha önce oluşturduğunuz Python ve SQL sorguları kullanarak gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="480e5-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL Server database created earlier.</span></span> <span data-ttu-id="480e5-244">Adlandırılmış bir örnek IPython not defteri **machine-Learning-data-science-process-sql-story.ipynb** hello sağlanan **örnek IPython not defterlerini** klasör.</span><span class="sxs-lookup"><span data-stu-id="480e5-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in hello **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="480e5-245">Bu dizüstü bilgisayar da kullanılabilir [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span><span class="sxs-lookup"><span data-stu-id="480e5-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="480e5-246">sıralı büyük verilerle çalışırken, önerilen hello hello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="480e5-246">hello recommended sequence when working with big data is hello following:</span></span>

* <span data-ttu-id="480e5-247">Merhaba veri küçük bir örnek, bir bellek içi veri çerçeveye okuyun.</span><span class="sxs-lookup"><span data-stu-id="480e5-247">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="480e5-248">Bazı Görselleştirme ve explorations hello örneklenen verileri kullanarak gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="480e5-248">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="480e5-249">Merhaba örneklenen verileri kullanarak özellik Mühendisliği ile deneyin.</span><span class="sxs-lookup"><span data-stu-id="480e5-249">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="480e5-250">Büyük veri keşfi veri işleme ve özellik Mühendisliği kullanın Python tooissue SQL sorguları doğrudan hello SQL Server veritabanı hello Azure VM.</span><span class="sxs-lookup"><span data-stu-id="480e5-250">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL Server database in hello Azure VM.</span></span>
* <span data-ttu-id="480e5-251">Azure Machine Learning modeli oluşturma Hello örnek boyutu toouse karar verin.</span><span class="sxs-lookup"><span data-stu-id="480e5-251">Decide hello sample size toouse for Azure Machine Learning model building.</span></span>

<span data-ttu-id="480e5-252">Ne zaman tooproceed tooAzure Machine Learning hazır, ya da olabilir:</span><span class="sxs-lookup"><span data-stu-id="480e5-252">When ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="480e5-253">Merhaba nihai SQL sorgu tooextract ve örnek hello veri ve kopyala-yapıştır hello sorguyu doğrudan kaydetmek bir [veri içeri aktarma] [ import-data] Azure Machine Learning modülünde.</span><span class="sxs-lookup"><span data-stu-id="480e5-253">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="480e5-254">Bu yöntem hello gösterilmiştir [Azure Machine Learning yapı modellerinde](#mlmodel) bölümü.</span><span class="sxs-lookup"><span data-stu-id="480e5-254">This method is demonstrated in hello [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="480e5-255">Örneklenen hello ve yeni bir veritabanı tablosunda derleme modeli için toouse planladığınız tasarlanan verilerinin kalıcı olmasını sonra hello yeni tablo hello kullanın [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="480e5-255">Persist hello sampled and engineered data you plan toouse for model building in a new database table, then use hello new table in hello [Import Data][import-data] module.</span></span>

<span data-ttu-id="480e5-256">birkaç veri keşfi, veri Görselleştirme ve örnekler mühendislik özelliği Hello aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="480e5-256">hello following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="480e5-257">Merhaba örnek SQL IPython not defterinde hello daha fazla örnek için bkz **örnek IPython not defterlerini** klasör.</span><span class="sxs-lookup"><span data-stu-id="480e5-257">For more examples, see hello sample SQL IPython notebook in hello **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="480e5-258">Veritabanı kimlik bilgileri başlatma</span><span class="sxs-lookup"><span data-stu-id="480e5-258">Initialize Database Credentials</span></span>
<span data-ttu-id="480e5-259">Veritabanı bağlantı ayarlarınızda değişkenleri aşağıdaki hello başlatın:</span><span class="sxs-lookup"><span data-stu-id="480e5-259">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="480e5-260">Veritabanı bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="480e5-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="480e5-261">Tablo nyctaxi_trip sayfasındaki satır ve sütunları rapor sayısı</span><span class="sxs-lookup"><span data-stu-id="480e5-261">Report number of rows and columns in table nyctaxi_trip</span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="480e5-262">Toplam satır sayısı 173179759 =</span><span class="sxs-lookup"><span data-stu-id="480e5-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="480e5-263">Toplam sütun sayısı = 14</span><span class="sxs-lookup"><span data-stu-id="480e5-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a><span data-ttu-id="480e5-264">Okuma bileşenini hello SQL Server veritabanı küçük veri örnekten</span><span class="sxs-lookup"><span data-stu-id="480e5-264">Read-in a small data sample from hello SQL Server Database</span></span>
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="480e5-265">Zaman tooread hello örnek Tablo 6.492000 saniyedir</span><span class="sxs-lookup"><span data-stu-id="480e5-265">Time tooread hello sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="480e5-266">Satır ve sütunların sayısı, alınan = (84952, 21)</span><span class="sxs-lookup"><span data-stu-id="480e5-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="480e5-267">Açıklayıcı istatistikleri</span><span class="sxs-lookup"><span data-stu-id="480e5-267">Descriptive Statistics</span></span>
<span data-ttu-id="480e5-268">Hazır tooexplore örneklenen hello veri sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="480e5-268">Now are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="480e5-269">Merhaba açıklayıcı istatistiklerini bakarak ile başlangıç **seyahat\_uzaklığı** (veya diğer) alan:</span><span class="sxs-lookup"><span data-stu-id="480e5-269">We start with looking at descriptive statistics for hello **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="480e5-270">Görselleştirme: Kutusu çizim örneği</span><span class="sxs-lookup"><span data-stu-id="480e5-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="480e5-271">Sonraki hello Kutu Çizimi hello seyahat uzaklığı toovisualize hello quantiles için ele</span><span class="sxs-lookup"><span data-stu-id="480e5-271">Next we look at hello box plot for hello trip distance toovisualize hello quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![#1 Çiz][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="480e5-273">Görselleştirme: Dağıtım çizim örneği</span><span class="sxs-lookup"><span data-stu-id="480e5-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![#2 Çiz][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="480e5-275">Görselleştirme: Çubuğu ve satır çizimleri</span><span class="sxs-lookup"><span data-stu-id="480e5-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="480e5-276">Bu örnekte, beş depo içine hello seyahat uzaklığı bin ve sonuçları binning hello görselleştirin.</span><span class="sxs-lookup"><span data-stu-id="480e5-276">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="480e5-277">Biz depo dağıtım çubuğundaki yukarıda hello çizmek veya aşağıdaki şekilde çizim satır</span><span class="sxs-lookup"><span data-stu-id="480e5-277">We can plot hello above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![#3 Çiz][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![#4 Çiz][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="480e5-280">Görselleştirme: Scatterplot örneği</span><span class="sxs-lookup"><span data-stu-id="480e5-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="480e5-281">Dağılım çizim arasında gösteriyoruz **seyahat\_zaman\_içinde\_saniye** ve **seyahat\_uzaklığı** herhangi bağıntı ise toosee</span><span class="sxs-lookup"><span data-stu-id="480e5-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![#6 Çiz][6]

<span data-ttu-id="480e5-283">Benzer şekilde biz hello ilişkisi denetleyebilirsiniz **oranı\_kod** ve **seyahat\_uzaklığı**.</span><span class="sxs-lookup"><span data-stu-id="480e5-283">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![#8 Çiz][8]

### <a name="sub-sampling-hello-data-in-sql"></a><span data-ttu-id="480e5-285">Alt örnekleme hello SQL verileri</span><span class="sxs-lookup"><span data-stu-id="480e5-285">Sub-Sampling hello Data in SQL</span></span>
<span data-ttu-id="480e5-286">Veri modeli oluşturmaya için hazırlarken [Azure Machine Learning Studio](https://studio.azureml.net), üzerinde hello ya da karar verebilirsiniz **hello veri içeri aktarma modülünde doğrudan SQL sorgu toouse** ya da mühendislik ve örneklenen hello kalıcı hello kullanabilen yeni bir tabloda veri [veri içeri aktarma] [ import-data] basit bir modülüyle **seçin * FROM <,\_yeni\_tablo\_adı >**.</span><span class="sxs-lookup"><span data-stu-id="480e5-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on hello **SQL query toouse directly in hello Import Data module** or persist hello engineered and sampled data in a new table, which you could use in hello [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="480e5-287">Bu bölümde oluşturacağız yeni bir tablo toohold hello örneklenen ve veri mühendislik.</span><span class="sxs-lookup"><span data-stu-id="480e5-287">In this section we will create a new table toohold hello sampled and engineered data.</span></span> <span data-ttu-id="480e5-288">Model oluşturmanın için doğrudan bir SQL sorgusu örneği hello sağlanan [veri keşfi ve özellik Mühendisliği SQL Server'daki](#dbexplore) bölümü.</span><span class="sxs-lookup"><span data-stu-id="480e5-288">An example of a direct SQL query for model building is provided in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="480e5-289">Bir örnek tablo ve Populate hello birleştirilmiş tablolar, %1 ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="480e5-289">Create a Sample Table and Populate with 1% of hello Joined Tables.</span></span> <span data-ttu-id="480e5-290">Varsa Tablo ilk bırakın.</span><span class="sxs-lookup"><span data-stu-id="480e5-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="480e5-291">Bu bölümde, biz hello tabloları birleştirme **nyctaxi\_seyahat** ve **nyctaxi\_ücreti**%1 rasgele örnek ayıklayın ve yeni bir tablo adı örneklenen hello veriyi kalıcı  **nyctaxi\_bir\_yüzde**:</span><span class="sxs-lookup"><span data-stu-id="480e5-291">In this section, we join hello tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist hello sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="480e5-292">Veri keşfi IPython not defterinde SQL sorgularını kullanma</span><span class="sxs-lookup"><span data-stu-id="480e5-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="480e5-293">Bu bölümde, yukarıda oluşturduğumuz hello yeni tabloda kalıcı hello %1 örneklenen verileri kullanarak veri dağıtımları keşfedin.</span><span class="sxs-lookup"><span data-stu-id="480e5-293">In this section, we explore data distributions using hello 1% sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="480e5-294">Benzer explorations isteğe bağlı olarak kullanarak hello özgün tabloları kullanılarak gerçekleştirilebilir Not **TABLESAMPLE** toolimit hello araştırması örnek veya hello sınırlayarak sonuçları hello kullanarak süre verilen tooa **alma \_datetime** hello gösterildiği gibi bölümler [veri keşfi ve özellik Mühendisliği SQL Server'daki](#dbexplore) bölümü.</span><span class="sxs-lookup"><span data-stu-id="480e5-294">Note that similar explorations can be performed using hello original tables, optionally using **TABLESAMPLE** toolimit hello exploration sample or by limiting hello results tooa given time period using hello **pickup\_datetime** partitions, as illustrated in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="480e5-295">Araştırması: Dönüş günlük dağıtımını</span><span class="sxs-lookup"><span data-stu-id="480e5-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="480e5-296">Keşfetme: medallion başına dağıtım seyahat</span><span class="sxs-lookup"><span data-stu-id="480e5-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="480e5-297">IPython not defterinde SQL sorgularını kullanarak özelliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="480e5-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="480e5-298">Bu bölümde yeni etiketler oluşturacağız ve doğrudan SQL sorgularını kullanarak özellik hello %1 örnek tablo üzerinde işletim hello önceki bölümde oluşturduğumuz.</span><span class="sxs-lookup"><span data-stu-id="480e5-298">In this section we will generate new labels and features directly using SQL queries, operating on hello 1% sample table we created in hello previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="480e5-299">Etiket oluşturma: Sınıf etiketleri oluşturmak</span><span class="sxs-lookup"><span data-stu-id="480e5-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="480e5-300">Aşağıdaki örneğine hello etiketleri toouse modelleme için iki kümesi oluştur:</span><span class="sxs-lookup"><span data-stu-id="480e5-300">In hello following example, we generate two sets of labels toouse for modeling:</span></span>

1. <span data-ttu-id="480e5-301">İkili sınıfı etiketleri **Eğimli** (bir ipucu verilir tahmin etmeye)</span><span class="sxs-lookup"><span data-stu-id="480e5-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="480e5-302">Çok sınıflı etiketleri **İpucu\_sınıfı** (Merhaba ipucu depo veya aralık tahmin etmeye)</span><span class="sxs-lookup"><span data-stu-id="480e5-302">Multiclass Labels **tip\_class** (predicting hello tip bin or range)</span></span>
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="480e5-303">Özellik Mühendisliği: Kategorik sütunlar sayısı özellikleri</span><span class="sxs-lookup"><span data-stu-id="480e5-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="480e5-304">Bu örnek, yineleme hello verilerdeki hello sayısı ile her kategori değiştirerek kategorik alan bir sayısal alana dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="480e5-304">This example transforms a categorical field into a numeric field by replacing each category with hello count of its occurrences in hello data.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="480e5-305">Özellik Mühendisliği: Sayısal sütunlar Bin özellikleri</span><span class="sxs-lookup"><span data-stu-id="480e5-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="480e5-306">Bu örnek sürekli bir sayısal alana hazır kategori aralıkları, yani, sayısal alana kategorik alan dönüştürme dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="480e5-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="480e5-307">Özellik Mühendisliği: Ondalık enlem/boylam konumu özelliklerinden Extract</span><span class="sxs-lookup"><span data-stu-id="480e5-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="480e5-308">Bu örnek hello ondalık gösterimini enlem ve/veya boylam alan farklı bir ayrıntı düzeyi birden çok bölgede alanlarına gibi keser ülke, şehir, şehir, engelleme, vb.. Merhaba yeni coğrafi alanlar değil eşlenen tooactual konumları olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="480e5-308">This example breaks down hello decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that hello new geo-fields are not mapped tooactual locations.</span></span> <span data-ttu-id="480e5-309">Eşleme geocode konumları hakkında daha fazla bilgi için bkz: [Bing Haritalar REST Hizmetleri](https://msdn.microsoft.com/library/ff701710.aspx).</span><span class="sxs-lookup"><span data-stu-id="480e5-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="480e5-310">Merhaba featurized tablosunun son form Hello doğrulayın</span><span class="sxs-lookup"><span data-stu-id="480e5-310">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="480e5-311">Şimdi hazır tooproceed toomodel yapı ve model dağıtımda duyuyoruz [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="480e5-311">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="480e5-312">Merhaba veri herhangi bir önceki sürümlerinde, yani tanımlanan hello tahmin sorunları için hazırdır:</span><span class="sxs-lookup"><span data-stu-id="480e5-312">hello data is ready for any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="480e5-313">İkili sınıflandırma: olsun veya olmasın bir ipucu Ücretli bir seyahat için toopredict.</span><span class="sxs-lookup"><span data-stu-id="480e5-313">Binary classification: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="480e5-314">Çok sınıflı sınıflandırma: Ücretli, ipucu önceden tanımlanmış sınıfları toohello göre toopredict hello aralığı.</span><span class="sxs-lookup"><span data-stu-id="480e5-314">Multiclass classification: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="480e5-315">Regresyon görevi: seyahat için ödenen ucunun toopredict hello tutar.</span><span class="sxs-lookup"><span data-stu-id="480e5-315">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="480e5-316"><a name="mlmodel"></a>Azure Machine Learning oluşturma modelleri</span><span class="sxs-lookup"><span data-stu-id="480e5-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="480e5-317">toobegin alıştırma modelleme Merhaba, tooyour Azure Machine Learning çalışma alanına oturum açın.</span><span class="sxs-lookup"><span data-stu-id="480e5-317">toobegin hello modeling exercise, log in tooyour Azure Machine Learning workspace.</span></span> <span data-ttu-id="480e5-318">Machine learning çalışma alanı henüz oluşturmadıysanız, bkz: [bir Azure Machine Learning çalışma alanı oluşturma](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="480e5-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="480e5-319">Azure Machine Learning ile başlatılan tooget bakın [Azure Machine Learning Studio nedir?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="480e5-319">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="480e5-320">Çok oturum[Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="480e5-320">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="480e5-321">Merhaba Studio giriş sayfası bol miktarda bilgi, videoları, öğreticiler, bağlantılar toohello modülleri başvurusu ve diğer kaynakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="480e5-321">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="480e5-322">Azure Machine Learning hakkında daha fazla bilgi için hello başvurun [Azure Machine Learning Belge Merkezi](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="480e5-322">Fore more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="480e5-323">Tipik eğitim denemenizi hello şunlardan oluşur:</span><span class="sxs-lookup"><span data-stu-id="480e5-323">A typical training experiment consists of hello following:</span></span>

1. <span data-ttu-id="480e5-324">Oluşturma bir **+ yeni** deneyin.</span><span class="sxs-lookup"><span data-stu-id="480e5-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="480e5-325">Merhaba veri tooAzure Machine Learning alın.</span><span class="sxs-lookup"><span data-stu-id="480e5-325">Get hello data tooAzure Machine Learning.</span></span>
3. <span data-ttu-id="480e5-326">Önceden işler, dönüştürme ve gerektiği gibi hello veri arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="480e5-326">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="480e5-327">Özellikler gerektiği şekilde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="480e5-327">Generate features as needed.</span></span>
5. <span data-ttu-id="480e5-328">Eğitim/doğrulama/test kümelerine Hello veri bölme (veya ayrı veri kümeleri her).</span><span class="sxs-lookup"><span data-stu-id="480e5-328">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="480e5-329">Bir veya daha fazla makine öğrenimi algoritmaları sorun toosolve öğrenme hello bağlı olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="480e5-329">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="480e5-330">Örneğin, ikili Sınıflandırma, çok sınıflı Sınıflandırma, regresyon.</span><span class="sxs-lookup"><span data-stu-id="480e5-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="480e5-331">Merhaba eğitim veri kümesini kullanarak bir veya daha fazla modelleri eğitme.</span><span class="sxs-lookup"><span data-stu-id="480e5-331">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="480e5-332">Merhaba, eğitilen modellerini kullanarak hello doğrulama dataset puan.</span><span class="sxs-lookup"><span data-stu-id="480e5-332">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="480e5-333">Merhaba modellere toocompute hello ilgili ölçümlerini sorun öğrenme hello değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="480e5-333">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="480e5-334">Merhaba modellerini ve select hello en iyi modeli toodeploy ince.</span><span class="sxs-lookup"><span data-stu-id="480e5-334">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="480e5-335">Bu alıştırmada, biz varsa zaten incelediniz ve SQL Server'daki hello veri mühendislik ve hello örnek boyutu tooingest Azure Machine learning'de karar.</span><span class="sxs-lookup"><span data-stu-id="480e5-335">In this exercise, we have already explored and engineered hello data in SQL Server, and decided on hello sample size tooingest in Azure Machine Learning.</span></span> <span data-ttu-id="480e5-336">bir veya daha fazla karar hello tahmin modellerinin toobuild:</span><span class="sxs-lookup"><span data-stu-id="480e5-336">toobuild one or more of hello prediction models we decided:</span></span>

1. <span data-ttu-id="480e5-337">Merhaba veri tooAzure Machine Learning almak hello kullanarak [veri içeri aktarma] [ import-data] modülü, hello kullanılabilir **veri giriş ve çıkış** bölümü.</span><span class="sxs-lookup"><span data-stu-id="480e5-337">Get hello data tooAzure Machine Learning using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="480e5-338">Merhaba daha fazla bilgi için bkz: [veri içeri aktarma] [ import-data] modül başvuru sayfası.</span><span class="sxs-lookup"><span data-stu-id="480e5-338">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Azure Machine Learning Veri Al][17]
2. <span data-ttu-id="480e5-340">Seçin **Azure SQL veritabanı** hello olarak **veri kaynağı** hello içinde **özellikleri** paneli.</span><span class="sxs-lookup"><span data-stu-id="480e5-340">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="480e5-341">Hello Hello veritabanı DNS adını girin **veritabanı sunucusu adı** alan.</span><span class="sxs-lookup"><span data-stu-id="480e5-341">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="480e5-342">Biçimi:`tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="480e5-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="480e5-343">Merhaba girin **veritabanı adı** hello karşılık gelen alandaki.</span><span class="sxs-lookup"><span data-stu-id="480e5-343">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="480e5-344">Merhaba girin **SQL kullanıcı adı** hello içinde ** sunucu kullanıcı aqccount adı ve hello hello Parolada **Server kullanıcı hesabı parolasını**.</span><span class="sxs-lookup"><span data-stu-id="480e5-344">Enter hello **SQL user name** in hello **Server user aqccount name, and hello password in hello **Server user account password**.</span></span>
6. <span data-ttu-id="480e5-345">Denetleme **herhangi bir sunucu sertifikayı kabul** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="480e5-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="480e5-346">Merhaba, **veritabanı sorgusu** metin alanı düzenleme, hello gerekli veritabanı (Merhaba etiketler gibi hesaplanan alanları dahil) alanları ve aşağı hangi ayıklar örnekleri hello veri istenen toohello örnek boyutu hello sorguyu yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="480e5-346">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="480e5-347">Merhaba aşağıdaki çizimde doğrudan hello SQL Server veritabanından veri okunurken bir ikili sınıflandırma deneme örnektir.</span><span class="sxs-lookup"><span data-stu-id="480e5-347">An example of a binary classification experiment reading data directly from hello SQL Server database is in hello figure below.</span></span> <span data-ttu-id="480e5-348">Benzer denemeler, çok sınıflı sınıflandırma ve regresyon sorunları için oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="480e5-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Azure Machine Learning eğitimi][10]

> [!IMPORTANT]
> <span data-ttu-id="480e5-350">Veri ayıklama modelleme ve önceki bölümlerde verilen sorgu örnekler örnekleme hello içinde **hello üç modelleme alıştırmaları için tüm etiketleri hello sorguya dahil**.</span><span class="sxs-lookup"><span data-stu-id="480e5-350">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="480e5-351">Önemli bir (gerekli) her alıştırmaları modelleme hello çok adımdır**hariç** gereksiz etiketler Merhaba için iki diğer sorunlar ve diğer hello **hedef sızıntıları**.</span><span class="sxs-lookup"><span data-stu-id="480e5-351">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="480e5-352">İçin örn., ikili Sınıflandırma, kullanırken hello etiket **Eğimli** ve hello alanları dışarıda **İpucu\_sınıfı**, **İpucu\_tutar**, ve **toplam\_tutar**.</span><span class="sxs-lookup"><span data-stu-id="480e5-352">For e.g., when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="480e5-353">Merhaba ikinci hello ipucu kapsıyor beri hedef sızıntıları Ücretli.</span><span class="sxs-lookup"><span data-stu-id="480e5-353">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="480e5-354">tooexclude gereksiz sütunları ve/veya hedef sızıntıları, hello kullanabilir [Select Columns in Dataset sütun] [ select-columns] modül veya hello [Düzenle meta veri] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="480e5-354">tooexclude unnecessary columns and/or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="480e5-355">Daha fazla bilgi için bkz: [Select Columns in Dataset sütun] [ select-columns] ve [Düzenle meta veri] [ edit-metadata] başvuru sayfaları.</span><span class="sxs-lookup"><span data-stu-id="480e5-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="480e5-356"><a name="mldeploy"></a>Azure Machine Learning modellerini dağıtma</span><span class="sxs-lookup"><span data-stu-id="480e5-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="480e5-357">Modeliniz hazır olduğunda, kolayca onu hello deneme doğrudan bir web hizmeti olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="480e5-357">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="480e5-358">Azure Machine Learning web hizmetleri dağıtma hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="480e5-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="480e5-359">toodeploy yeni bir web hizmeti, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="480e5-359">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="480e5-360">Puanlama bir deneme oluşturma.</span><span class="sxs-lookup"><span data-stu-id="480e5-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="480e5-361">Merhaba web hizmetini dağıtın.</span><span class="sxs-lookup"><span data-stu-id="480e5-361">Deploy hello web service.</span></span>

<span data-ttu-id="480e5-362">bir Puanlama denemeler toocreate bir **tamamlandı** deneme eğitim, tıklatın **oluşturma PUANLAMA DENEMELER** hello alt eylem çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="480e5-362">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Azure Puanlama][18]

<span data-ttu-id="480e5-364">Azure Machine Learning toocreate hello eğitim denemenizi hello bileşenlerini temel alan bir Puanlama deneme deneyecek.</span><span class="sxs-lookup"><span data-stu-id="480e5-364">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="480e5-365">Özellikle, çıkarır:</span><span class="sxs-lookup"><span data-stu-id="480e5-365">In particular, it will:</span></span>

1. <span data-ttu-id="480e5-366">Merhaba, eğitilen model kaydetmek ve hello model eğitim modüllerini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="480e5-366">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="480e5-367">Bir mantıksal tanımlamak **giriş bağlantı noktası** toorepresent hello giriş veri şeması bekleniyordu.</span><span class="sxs-lookup"><span data-stu-id="480e5-367">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="480e5-368">Bir mantıksal tanımlamak **çıkış bağlantı noktasına** toorepresent hello beklenen web hizmeti çıkış şeması.</span><span class="sxs-lookup"><span data-stu-id="480e5-368">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="480e5-369">Deneme Puanlama hello oluşturulduğunda, gözden geçirin ve gerektiği gibi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="480e5-369">When hello scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="480e5-370">Merhaba hizmeti çağrıldığında bunlar kullanılamaz tipik ayarlama tooreplace hello girdi veri kümesi ve/veya sorgu etiket alanları hariç biri ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="480e5-370">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="480e5-371">Ayrıca, hello iyi bir uygulama tooreduce hello boyutunu veri kümesi ve/veya sorgu tooa birkaç kayıtları, yeterli tooindicate hello giriş şemasını giriş unutulmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="480e5-371">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="480e5-372">Merhaba çıkış bağlantı noktasına ilişkin tüm giriş alanları ortak tooexclude olduğundan ve yalnızca hello dahil **skoru etiketleri** ve **skoru olasılıklar** hello kullanarak çıktıyı hello içinde [veri kümesinde Sütun Seç ] [ select-columns] modülü.</span><span class="sxs-lookup"><span data-stu-id="480e5-372">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="480e5-373">Deneme Puanlama bir örnek hello aşağıdaki çizimde gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="480e5-373">A sample scoring experiment is in hello figure below.</span></span> <span data-ttu-id="480e5-374">Ne zaman toodeploy, hazır hello tıklatın **yayımlama WEB hizmeti** hello alt eylem çubuğunda düğmesi.</span><span class="sxs-lookup"><span data-stu-id="480e5-374">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Azure Machine Learning yayımlama][11]

<span data-ttu-id="480e5-376">toorecap, bu gözden geçirme öğreticide büyük ortak veri kümesi eğitim ve bir Azure Machine Learning web hizmeti dağıtma veri alım toomodel tüm hello şekilde ile çalışan bir Azure veri bilimi ortam oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="480e5-376">toorecap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all hello way from data acquisition toomodel training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="480e5-377">Lisans bilgileri</span><span class="sxs-lookup"><span data-stu-id="480e5-377">License Information</span></span>
<span data-ttu-id="480e5-378">Bu örnek gözden geçirme ve kendi eşlik eden komut dosyaları ve IPython notebook(s) paylaşıldığı Microsoft tarafından hello MIT lisansı altında.</span><span class="sxs-lookup"><span data-stu-id="480e5-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="480e5-379">Lütfen hello LICENSE.txt dosyayı daha fazla ayrıntı için GitHub üzerindeki hello örnek kodu hello dizininde iade edin.</span><span class="sxs-lookup"><span data-stu-id="480e5-379">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="480e5-380">Başvurular</span><span class="sxs-lookup"><span data-stu-id="480e5-380">References</span></span>
<span data-ttu-id="480e5-381">• [Andrés Monroy NYC ücreti dönüşleri indirme sayfası](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="480e5-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="480e5-382">• [FOILing NYC ait ücreti seyahat veri Chris Whong tarafından](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="480e5-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="480e5-383">• [NYC ücreti ve Limousine devreye sokmak araştırma ve istatistikleri](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="480e5-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
